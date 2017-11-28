<span data-ttu-id="cc070-101">Azure’da artık iki hata ayıklama özelliği desteklenmektedir: Azure Sanal Makineler Kaynak Yöneticisi dağıtım modelinde Konsol Çıktısı ve Ekran Görüntüsü desteği vardır.</span><span class="sxs-lookup"><span data-stu-id="cc070-101">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="cc070-102">Azure’a kendi görüntünüzü ekleme ve hatta bir platform görüntüsünden önyükleme yapma sırasında bir Sanal Makineni önyüklenebilir olmayan bir duruma gelmesinin birçok nedeni olabilir.</span><span class="sxs-lookup"><span data-stu-id="cc070-102">When bringing your own image to Azure or even booting one of the platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="cc070-103">Bu özellikler sanal makinelerinizin önyükleme hatalarını kolayca tanılamanızı ve düzeltmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc070-103">These features enable you to easily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="cc070-104">Linux sanal makineleri için Portal'dan konsol oturum çıktısını kolayca görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cc070-104">For Linux Virtual Machines, you can easily view the output of your console log from the Portal:</span></span>

![Azure portalına](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="cc070-106">Ancak, hem Windows hem de Linux sanal makineleri için Azure, hiper yöneticiden VM'nin ekran görüntüsünü görmenizi de sağlar:</span><span class="sxs-lookup"><span data-stu-id="cc070-106">However, for both Windows and Linux Virtual Machines, Azure also enables you to see a screenshot of the VM from the hypervisor:</span></span>

![Hata](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

<span data-ttu-id="cc070-108">Bu özelliklerin her ikisi de tüm bölgelerdeki Azure sanal makineler için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="cc070-108">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="cc070-109">Not, ekran görüntüleri ve çıktının depolama hesabınızda görünmesi 10 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="cc070-109">Note, screenshots, and output can take up to 10 minutes to appear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="cc070-110">Sık karşılaşılan önyükleme hataları</span><span class="sxs-lookup"><span data-stu-id="cc070-110">Common boot errors</span></span>

- [<span data-ttu-id="cc070-111">0xC000000E</span><span class="sxs-lookup"><span data-stu-id="cc070-111">0xC000000E</span></span>](https://support.microsoft.com/help/4010129)
- [<span data-ttu-id="cc070-112">0xC000000F</span><span class="sxs-lookup"><span data-stu-id="cc070-112">0xC000000F</span></span>](https://support.microsoft.com/help/4010130)
- [<span data-ttu-id="cc070-113">0xC0000011</span><span class="sxs-lookup"><span data-stu-id="cc070-113">0xC0000011</span></span>](https://support.microsoft.com/help/4010134)
- [<span data-ttu-id="cc070-114">0xC0000034</span><span class="sxs-lookup"><span data-stu-id="cc070-114">0xC0000034</span></span>](https://support.microsoft.com/help/4010140)
- [<span data-ttu-id="cc070-115">0xC0000098</span><span class="sxs-lookup"><span data-stu-id="cc070-115">0xC0000098</span></span>](https://support.microsoft.com/help/4010137)
- [<span data-ttu-id="cc070-116">0xC00000BA</span><span class="sxs-lookup"><span data-stu-id="cc070-116">0xC00000BA</span></span>](https://support.microsoft.com/help/4010136)
- [<span data-ttu-id="cc070-117">0xC000014C</span><span class="sxs-lookup"><span data-stu-id="cc070-117">0xC000014C</span></span>](https://support.microsoft.com/help/4010141)
- [<span data-ttu-id="cc070-118">0xC0000221</span><span class="sxs-lookup"><span data-stu-id="cc070-118">0xC0000221</span></span>](https://support.microsoft.com/help/4010132)
- [<span data-ttu-id="cc070-119">0xC0000225</span><span class="sxs-lookup"><span data-stu-id="cc070-119">0xC0000225</span></span>](https://support.microsoft.com/help/4010138)
- [<span data-ttu-id="cc070-120">0xC0000359</span><span class="sxs-lookup"><span data-stu-id="cc070-120">0xC0000359</span></span>](https://support.microsoft.com/help/4010135)
- [<span data-ttu-id="cc070-121">0xC0000605</span><span class="sxs-lookup"><span data-stu-id="cc070-121">0xC0000605</span></span>](https://support.microsoft.com/help/4010131)
- [<span data-ttu-id="cc070-122">Bir işletim sistemi bulunamadı</span><span class="sxs-lookup"><span data-stu-id="cc070-122">An operating system wasn't found</span></span>](https://support.microsoft.com/help/4010142)
- [<span data-ttu-id="cc070-123">Önyükleme hatası veya INACCESSIBLE_BOOT_DEVICE</span><span class="sxs-lookup"><span data-stu-id="cc070-123">Boot failure or INACCESSIBLE_BOOT_DEVICE</span></span>](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="cc070-124">Yeni bir sanal makine üzerinde tanılamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="cc070-124">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="cc070-125">Önizleme Portalı'ndan yeni bir sanal makine oluştururken dağıtım modeli açılır menüsünde **Azure Resource Manager**’ı seçin:</span><span class="sxs-lookup"><span data-stu-id="cc070-125">When creating a new Virtual Machine from the Preview Portal, select the **Azure Resource Manager** from the deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="cc070-127">Burada bu tanılama dosyalarını yerleştirmek istediğiniz depolama hesabını seçmek için izleme seçeneğini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cc070-127">Configure the Monitoring option to select the storage account where you would like to place these diagnostic files.</span></span>
 
    ![VM oluşturma](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="cc070-129">Bir Azure Resource Manager şablonu dağıtıyorsanız, sanal makine kaynağınıza gidin ve tanılama profili bölümünü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cc070-129">If you are deploying from an Azure Resource Manager template, navigate to your Virtual Machine resource and append the diagnostics profile section.</span></span> <span data-ttu-id="cc070-130">"2015-06-15" API sürümü üst bilgisini kullanmayı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cc070-130">Remember to use the “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="cc070-131">Tanılama profili, bu günlükleri yerleştirmek istediğiniz depolama hesabını seçmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc070-131">The diagnostics profile enables you to select the storage account where you want to put these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

<span data-ttu-id="cc070-132">Önyükleme tanılaması etkin bir örnek sanal makine dağıtmak için buradaki depomuza göz atın.</span><span class="sxs-lookup"><span data-stu-id="cc070-132">To deploy a sample Virtual Machine with boot diagnostics enabled, check out our repo here.</span></span>

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="cc070-133">Mevcut bir sanal makineyi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="cc070-133">Update an existing virtual machine</span></span> ##

<span data-ttu-id="cc070-134">Portal üzerinden önyükleme tanılamasını etkinleştirmek için mevcut bir sanal makineyi Portalı aracılığıyla da güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc070-134">To enable boot diagnostics through the Portal, you can also update an existing Virtual Machine through the Portal.</span></span> <span data-ttu-id="cc070-135">Önyükleme Tanılaması seçeneğini ve Kaydet’i seçin.</span><span class="sxs-lookup"><span data-stu-id="cc070-135">Select the Boot Diagnostics option and Save.</span></span> <span data-ttu-id="cc070-136">Etkili olması için VM'yi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="cc070-136">Restart the VM to take effect.</span></span>

![Mevcut VM’yi güncelleştirme](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

