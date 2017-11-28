## <a name="overview"></a><span data-ttu-id="005a0-101">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="005a0-101">Overview</span></span>
<span data-ttu-id="005a0-102">Bir Kaynak Grubunda [Azure Market](https://azure.microsoft.com/marketplace/)’ten edinilen bir görüntüyü dağıtarak yeni bir sanal makine (VM) oluşturduğunuzda, varsayılan işletim sistemi sürücüsü 127 GB’tır.</span><span class="sxs-lookup"><span data-stu-id="005a0-102">When you create a new virtual machine (VM) in a Resource Group by deploying an image from [Azure Marketplace](https://azure.microsoft.com/marketplace/), the default OS drive is 127 GB.</span></span> <span data-ttu-id="005a0-103">VM’ye veri diskleri eklemek (kaç tane ekleyebileceğiniz seçtiğiniz SKU’ya bağlıdır) mümkün olmasına, hatta uygulamaları ve yoğun CPU kullanımlı iş yüklerini bu ek disklere yüklemeniz önerilmesine rağmen, sıklıkla müşterilerin aşağıdaki gibi belirli senaryoları etkinleştirmesi için işletim sistemi sürücüsünü genişletmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="005a0-103">Even though it’s possible to add data disks to the VM (how many depending upon the SKU you’ve chosen) and moreover it’s recommended to install applications and CPU intensive workloads on these addendum disks, oftentimes customers need to expand the OS drive to support certain scenarios such as following:</span></span>

1. <span data-ttu-id="005a0-104">İşletim sistemi sürücüsüne bileşen yükleyen eski uygulamaları destekleme.</span><span class="sxs-lookup"><span data-stu-id="005a0-104">Support legacy applications that install components on OS drive.</span></span>
2. <span data-ttu-id="005a0-105">Fiziksel bir bilgisayarı veya sanal makineyi daha büyük bir işletim sistemi sürücüsüne sahip şirket içi kaynaktan geçirme.</span><span class="sxs-lookup"><span data-stu-id="005a0-105">Migrate a physical PC or virtual machine from on-premises with a larger OS drive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="005a0-106">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır: Resource Manager ve Klasik.</span><span class="sxs-lookup"><span data-stu-id="005a0-106">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="005a0-107">Bu makalede Resource Manager modelinin kullanımı anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="005a0-107">This article covers using the Resource Manager model.</span></span> <span data-ttu-id="005a0-108">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="005a0-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> 
> 

## <a name="resize-the-os-drive"></a><span data-ttu-id="005a0-109">İşletim sistemi sürücüsünü yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="005a0-109">Resize the OS drive</span></span>
<span data-ttu-id="005a0-110">Bu makalede, [Azure Powershell](/powershell/azureps-cmdlets-docs)’in kaynak yöneticisi modüllerini kullanarak işletim sistemi sürücüsünü yeniden boyutlandırma görevini gerçekleştireceğiz.</span><span class="sxs-lookup"><span data-stu-id="005a0-110">In this article we’ll accomplish the task of resizing the OS drive using resource manager modules of [Azure Powershell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="005a0-111">Powershell ISE veya Powershell pencerenizi yönetim modunda açın ve aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="005a0-111">Open your Powershell ISE or Powershell window in administrative mode and follow the steps below:</span></span>

1. <span data-ttu-id="005a0-112">Aşağıdakileri yaparak Microsoft Azure hesabınızda kaynak yönetimi modunda oturum açın ve aboneliğinizi seçin:</span><span class="sxs-lookup"><span data-stu-id="005a0-112">Sign-in to your Microsoft Azure account in resource management mode and select your subscription as follows:</span></span>
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. <span data-ttu-id="005a0-113">Aşağıdakileri yaparak kaynak grubunuzun adını ve VM adını ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="005a0-113">Set your resource group name and VM name as follows:</span></span>
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. <span data-ttu-id="005a0-114">Aşağıdakileri yaparak sanal makineniz için bir başvuru edinin:</span><span class="sxs-lookup"><span data-stu-id="005a0-114">Obtain a reference to your VM as follows:</span></span>
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. <span data-ttu-id="005a0-115">Aşağıdakileri yaparak diski yeniden boyutlandırmadan önce VM’yi durdurun:</span><span class="sxs-lookup"><span data-stu-id="005a0-115">Stop the VM before resizing the disk as follows:</span></span>
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. <span data-ttu-id="005a0-116">İşte beklediğimiz an geldi!</span><span class="sxs-lookup"><span data-stu-id="005a0-116">And here comes the moment we’ve been waiting for!</span></span> <span data-ttu-id="005a0-117">Aşağıdakileri yaparak işletim sistemi diskinin boyutunu istenen değere ayarlayın ve VM’yi güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="005a0-117">Set the size of the OS disk to the desired value and update the VM as follows:</span></span>
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > <span data-ttu-id="005a0-118">Yeni boyut mevcut disk boyutundan büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="005a0-118">The new size should be greater than the existing disk size.</span></span> <span data-ttu-id="005a0-119">İzin verilen en büyük boyut 1023 GB’tır.</span><span class="sxs-lookup"><span data-stu-id="005a0-119">The maximum allowed is 1023 GB.</span></span>
   > 
   > 
6. <span data-ttu-id="005a0-120">VM güncelleştirmesi biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="005a0-120">Updating the VM may take a few seconds.</span></span> <span data-ttu-id="005a0-121">Komutun yürütülmesi tamamlandığında aşağıdakileri yaparak VM’yi yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="005a0-121">Once the command finishes executing, restart the VM as follows:</span></span>
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

<span data-ttu-id="005a0-122">Hepsi bu!</span><span class="sxs-lookup"><span data-stu-id="005a0-122">And that’s it!</span></span> <span data-ttu-id="005a0-123">Şimdi RDP ile sanal makinenize girin, Bilgisayar Yönetimi’ni (veya Disk Yönetimi) açın ve yeni ayrılan alanı kullanarak sürücüyü genişletin.</span><span class="sxs-lookup"><span data-stu-id="005a0-123">Now RDP into the VM, open Computer Management (or Disk Management) and expand the drive using the newly allocated space.</span></span>

## <a name="summary"></a><span data-ttu-id="005a0-124">Özet</span><span class="sxs-lookup"><span data-stu-id="005a0-124">Summary</span></span>
<span data-ttu-id="005a0-125">Bu makalede, PowerShell’in Azure Resource Manager modüllerini kullanarak bir IaaS sanal makinesinin işletim sistemi sürücüsünü genişlettik.</span><span class="sxs-lookup"><span data-stu-id="005a0-125">In this article, we used Azure Resource Manager modules of Powershell to expand the OS drive of an IaaS virtual machine.</span></span> <span data-ttu-id="005a0-126">Aşağıda başvurabilmeniz için betiğin tamamının kopyası verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="005a0-126">Reproduced below is the complete script for your reference:</span></span>

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a><span data-ttu-id="005a0-127">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="005a0-127">Next Steps</span></span>
<span data-ttu-id="005a0-128">Bu makalede öncelikli olarak sanal makinenin işletim sistemi diskini genişletmeye odaklanmış olsak da geliştirilen betik, tek bir kod satırının değiştirilmesiyle VM’ye bağlı veri disklerinin genişletilmesi için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="005a0-128">Though in this article, we focused primarily on expanding the OS disk of the VM, the developed script may also be used for expanding the data disks attached to the VM by changing a single line of code.</span></span> <span data-ttu-id="005a0-129">Örneğin, VM’ye bağlı ilk veri diskini genişletmek için ```StorageProfile``` öğesinin ```OSDisk``` nesnesini ```DataDisks``` dizisi ile değiştirin ve aşağıda gösterildiği gibi sayısal bir dizin kullanarak ilk bağlanan veri diskinin başvurusunu edinin:</span><span class="sxs-lookup"><span data-stu-id="005a0-129">For example, to expand the first data disk attached to the VM, replace the ```OSDisk``` object of ```StorageProfile``` with ```DataDisks``` array and use a numeric index to obtain a reference to first attached data disk, as shown below:</span></span>

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
<span data-ttu-id="005a0-130">Benzer şekilde, yukarıdaki gibi bir dizini ya da diskin ```Name``` özelliğini aşağıda gösterildiği gibi kullanarak sanal makinenize bağlı diğer veri disklerine de başvurabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="005a0-130">Similarly you may reference other data disks attached to the VM, either by using an index as shown above or the ```Name``` property of the disk as illustrated below:</span></span>

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

<span data-ttu-id="005a0-131">Azure Resource Manager sanal makinesine disk bağlama hakkında bilgi edinmek istiyorsanız bu [makaleyi](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) inceleyin.</span><span class="sxs-lookup"><span data-stu-id="005a0-131">If you want to find out how to attach disks to an Azure Resource Manager VM, check this [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

