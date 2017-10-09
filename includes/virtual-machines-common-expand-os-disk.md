## <a name="overview"></a><span data-ttu-id="8b230-101">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="8b230-101">Overview</span></span>
<span data-ttu-id="8b230-102">Oluşturduğunuzda, yeni bir sanal makine (VM) bir kaynak grubunda bir görüntüden dağıtarak [Azure Marketi](https://azure.microsoft.com/marketplace/), hello varsayılan işletim sistemi sürücüsü olan 127 GB.</span><span class="sxs-lookup"><span data-stu-id="8b230-102">When you create a new virtual machine (VM) in a Resource Group by deploying an image from [Azure Marketplace](https://azure.microsoft.com/marketplace/), hello default OS drive is 127 GB.</span></span> <span data-ttu-id="8b230-103">Olası tooadd veri diskleri toohello (kaç bağlı olarak SKU hello sırasında seçtiğiniz) VM, ayrıca önerilen tooinstall uygulamaları ve CPU yoğun iş yükleri bu eki disklerdeki ise rağmen müşterilerin tooexpand hello OS görmemeleri gerekir aşağıdaki gibi belirli senaryolar toosupport sürücü:</span><span class="sxs-lookup"><span data-stu-id="8b230-103">Even though it’s possible tooadd data disks toohello VM (how many depending upon hello SKU you’ve chosen) and moreover it’s recommended tooinstall applications and CPU intensive workloads on these addendum disks, oftentimes customers need tooexpand hello OS drive toosupport certain scenarios such as following:</span></span>

1. <span data-ttu-id="8b230-104">İşletim sistemi sürücüsüne bileşen yükleyen eski uygulamaları destekleme.</span><span class="sxs-lookup"><span data-stu-id="8b230-104">Support legacy applications that install components on OS drive.</span></span>
2. <span data-ttu-id="8b230-105">Fiziksel bir bilgisayarı veya sanal makineyi daha büyük bir işletim sistemi sürücüsüne sahip şirket içi kaynaktan geçirme.</span><span class="sxs-lookup"><span data-stu-id="8b230-105">Migrate a physical PC or virtual machine from on-premises with a larger OS drive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b230-106">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır: Resource Manager ve Klasik.</span><span class="sxs-lookup"><span data-stu-id="8b230-106">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="8b230-107">Bu makalede, hello Resource Manager modelini kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="8b230-107">This article covers using hello Resource Manager model.</span></span> <span data-ttu-id="8b230-108">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="8b230-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> 
> 

## <a name="resize-hello-os-drive"></a><span data-ttu-id="8b230-109">Merhaba işletim sistemi sürücüsü yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="8b230-109">Resize hello OS drive</span></span>
<span data-ttu-id="8b230-110">Bu makalede biz hello işletim sistemi sürücüsü resource manager modüllerini kullanarak yeniden boyutlandırma, hello görevi [Azure Powershell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="8b230-110">In this article we’ll accomplish hello task of resizing hello OS drive using resource manager modules of [Azure Powershell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="8b230-111">Yönetici modunda Powershell ISE veya Powershell penceresi açın ve aşağıdaki hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="8b230-111">Open your Powershell ISE or Powershell window in administrative mode and follow hello steps below:</span></span>

1. <span data-ttu-id="8b230-112">Oturum açma tooyour Microsoft Azure kaynak yönetimi modunda hesabınızı ve aboneliğinizi aşağıdaki gibi seçin:</span><span class="sxs-lookup"><span data-stu-id="8b230-112">Sign-in tooyour Microsoft Azure account in resource management mode and select your subscription as follows:</span></span>
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. <span data-ttu-id="8b230-113">Aşağıdakileri yaparak kaynak grubunuzun adını ve VM adını ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="8b230-113">Set your resource group name and VM name as follows:</span></span>
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. <span data-ttu-id="8b230-114">Başvuru tooyour VM aşağıdaki gibi alın:</span><span class="sxs-lookup"><span data-stu-id="8b230-114">Obtain a reference tooyour VM as follows:</span></span>
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. <span data-ttu-id="8b230-115">Merhaba VM hello disk aşağıdaki gibi yeniden boyutlandırma önce durdurun:</span><span class="sxs-lookup"><span data-stu-id="8b230-115">Stop hello VM before resizing hello disk as follows:</span></span>
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. <span data-ttu-id="8b230-116">Ve biz beklediğinden hello şu anda İşte!</span><span class="sxs-lookup"><span data-stu-id="8b230-116">And here comes hello moment we’ve been waiting for!</span></span> <span data-ttu-id="8b230-117">Merhaba işletim sistemi disk istenen toohello değeri Hello boyutunu ayarlayın ve hello VM şu şekilde güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="8b230-117">Set hello size of hello OS disk toohello desired value and update hello VM as follows:</span></span>
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > <span data-ttu-id="8b230-118">Merhaba yeni boyutu hello mevcut disk boyutundan daha büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b230-118">hello new size should be greater than hello existing disk size.</span></span> <span data-ttu-id="8b230-119">Merhaba izin verilen en fazla 1023 GB'tır.</span><span class="sxs-lookup"><span data-stu-id="8b230-119">hello maximum allowed is 1023 GB.</span></span>
   > 
   > 
6. <span data-ttu-id="8b230-120">Güncelleştirme hello VM birkaç saniye sürebilir.</span><span class="sxs-lookup"><span data-stu-id="8b230-120">Updating hello VM may take a few seconds.</span></span> <span data-ttu-id="8b230-121">Hello VM Hello komutu yürütme tamamlandıktan sonra aşağıdaki gibi yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="8b230-121">Once hello command finishes executing, restart hello VM as follows:</span></span>
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

<span data-ttu-id="8b230-122">Hepsi bu!</span><span class="sxs-lookup"><span data-stu-id="8b230-122">And that’s it!</span></span> <span data-ttu-id="8b230-123">Şimdi hello VM RDP'ye Bilgisayar Yönetimi (veya Disk Yönetimi) açın ve yeni ayrılmış alanı hello kullanarak hello sürücüyü genişletin.</span><span class="sxs-lookup"><span data-stu-id="8b230-123">Now RDP into hello VM, open Computer Management (or Disk Management) and expand hello drive using hello newly allocated space.</span></span>

## <a name="summary"></a><span data-ttu-id="8b230-124">Özet</span><span class="sxs-lookup"><span data-stu-id="8b230-124">Summary</span></span>
<span data-ttu-id="8b230-125">Bu makalede, Azure Resource Manager modüllerini Powershell tooexpand hello bir Iaas sanal makinenin işletim sistemi sürücüsü kullandık.</span><span class="sxs-lookup"><span data-stu-id="8b230-125">In this article, we used Azure Resource Manager modules of Powershell tooexpand hello OS drive of an IaaS virtual machine.</span></span> <span data-ttu-id="8b230-126">Aşağıda çoğaltılamaz hello daha sonra başvurmak üzere tam komut dosyası vardır:</span><span class="sxs-lookup"><span data-stu-id="8b230-126">Reproduced below is hello complete script for your reference:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8b230-127">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="8b230-127">Next Steps</span></span>
<span data-ttu-id="8b230-128">Bu makalede, biz öncelikle hello VM hello işletim sistemi diski genişletme üzerinde odaklanmış olsa hello geliştirilmiş komut dosyası ayrıca tek satırlık bir kod değiştirerek hello veri diskleri ekli toohello VM genişletmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8b230-128">Though in this article, we focused primarily on expanding hello OS disk of hello VM, hello developed script may also be used for expanding hello data disks attached toohello VM by changing a single line of code.</span></span> <span data-ttu-id="8b230-129">Örneğin, tooexpand hello ilk veri diski ekli toohello VM, hello yerine ```OSDisk``` nesnesinin ```StorageProfile``` ile ```DataDisks``` dizi ve sayısal dizin tooobtain bir başvuru toofirst ekli veri diski aşağıda gösterildiği gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="8b230-129">For example, tooexpand hello first data disk attached toohello VM, replace hello ```OSDisk``` object of ```StorageProfile``` with ```DataDisks``` array and use a numeric index tooobtain a reference toofirst attached data disk, as shown below:</span></span>

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
<span data-ttu-id="8b230-130">Benzer şekilde, diğer veri diskleri ekli toohello VM, yukarıda gösterildiği gibi bir dizin kullanarak ya da başvuru veya hello ```Name``` aşağıda gösterildiği gibi hello disk özelliği:</span><span class="sxs-lookup"><span data-stu-id="8b230-130">Similarly you may reference other data disks attached toohello VM, either by using an index as shown above or hello ```Name``` property of hello disk as illustrated below:</span></span>

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

<span data-ttu-id="8b230-131">Nasıl tooattach tooan Azure Resource Manager VM diskleri çıkışı toofind istiyorsanız, bunu işaretleyin [makale](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8b230-131">If you want toofind out how tooattach disks tooan Azure Resource Manager VM, check this [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

