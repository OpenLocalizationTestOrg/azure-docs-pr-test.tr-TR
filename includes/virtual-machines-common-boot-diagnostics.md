<span data-ttu-id="d7843-101">Azure’da artık iki hata ayıklama özelliği desteklenmektedir: Azure Sanal Makineler Kaynak Yöneticisi dağıtım modelinde Konsol Çıktısı ve Ekran Görüntüsü desteği vardır.</span><span class="sxs-lookup"><span data-stu-id="d7843-101">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="d7843-102">Kendi görüntü tooAzure veya hello platform görüntüleri bile önyükleme biri getirilirken bir sanal makine önyüklenebilir olmayan bir duruma neden alır birçok nedeni olabilir.</span><span class="sxs-lookup"><span data-stu-id="d7843-102">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="d7843-103">Bu özellikler, tooeasily tanılamak ve sanal makinelerinizi önyükleme hatalarını kurtarıp etkinleştir.</span><span class="sxs-lookup"><span data-stu-id="d7843-103">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="d7843-104">Linux sanal makineleri için hello Portal, konsol günlüğünden hello çıktısını kolayca görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d7843-104">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Azure portalına](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="d7843-106">Ancak, Windows ve Linux sanal makineleri için Azure ayrıca bir ekran görüntüsünü hello VM hello hiper yönetici gelen toosee sağlar:</span><span class="sxs-lookup"><span data-stu-id="d7843-106">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![Hata](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

<span data-ttu-id="d7843-108">Bu özelliklerin her ikisi de tüm bölgelerdeki Azure sanal makineler için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="d7843-108">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="d7843-109">Not, ekran görüntüleri ve çıktı too10 dakika tooappear depolama hesabınızdaki yukarı alabilir.</span><span class="sxs-lookup"><span data-stu-id="d7843-109">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="d7843-110">Sık karşılaşılan önyükleme hataları</span><span class="sxs-lookup"><span data-stu-id="d7843-110">Common boot errors</span></span>

- [<span data-ttu-id="d7843-111">0xC000000E</span><span class="sxs-lookup"><span data-stu-id="d7843-111">0xC000000E</span></span>](https://support.microsoft.com/help/4010129)
- [<span data-ttu-id="d7843-112">0xC000000F</span><span class="sxs-lookup"><span data-stu-id="d7843-112">0xC000000F</span></span>](https://support.microsoft.com/help/4010130)
- [<span data-ttu-id="d7843-113">0xC0000011</span><span class="sxs-lookup"><span data-stu-id="d7843-113">0xC0000011</span></span>](https://support.microsoft.com/help/4010134)
- [<span data-ttu-id="d7843-114">0xC0000034</span><span class="sxs-lookup"><span data-stu-id="d7843-114">0xC0000034</span></span>](https://support.microsoft.com/help/4010140)
- [<span data-ttu-id="d7843-115">0xC0000098</span><span class="sxs-lookup"><span data-stu-id="d7843-115">0xC0000098</span></span>](https://support.microsoft.com/help/4010137)
- [<span data-ttu-id="d7843-116">0xC00000BA</span><span class="sxs-lookup"><span data-stu-id="d7843-116">0xC00000BA</span></span>](https://support.microsoft.com/help/4010136)
- [<span data-ttu-id="d7843-117">0xC000014C</span><span class="sxs-lookup"><span data-stu-id="d7843-117">0xC000014C</span></span>](https://support.microsoft.com/help/4010141)
- [<span data-ttu-id="d7843-118">0xC0000221</span><span class="sxs-lookup"><span data-stu-id="d7843-118">0xC0000221</span></span>](https://support.microsoft.com/help/4010132)
- [<span data-ttu-id="d7843-119">0xC0000225</span><span class="sxs-lookup"><span data-stu-id="d7843-119">0xC0000225</span></span>](https://support.microsoft.com/help/4010138)
- [<span data-ttu-id="d7843-120">0xC0000359</span><span class="sxs-lookup"><span data-stu-id="d7843-120">0xC0000359</span></span>](https://support.microsoft.com/help/4010135)
- [<span data-ttu-id="d7843-121">0xC0000605</span><span class="sxs-lookup"><span data-stu-id="d7843-121">0xC0000605</span></span>](https://support.microsoft.com/help/4010131)
- [<span data-ttu-id="d7843-122">Bir işletim sistemi bulunamadı</span><span class="sxs-lookup"><span data-stu-id="d7843-122">An operating system wasn't found</span></span>](https://support.microsoft.com/help/4010142)
- [<span data-ttu-id="d7843-123">Önyükleme hatası veya INACCESSIBLE_BOOT_DEVICE</span><span class="sxs-lookup"><span data-stu-id="d7843-123">Boot failure or INACCESSIBLE_BOOT_DEVICE</span></span>](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="d7843-124">Yeni bir sanal makine üzerinde tanılamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="d7843-124">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="d7843-125">Önizleme portalı hello yeni bir sanal makine oluştururken, hello seçin **Azure Resource Manager** gelen hello dağıtım modeli açılır:</span><span class="sxs-lookup"><span data-stu-id="d7843-125">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="d7843-127">Bu tanılama dosyaları Hello tooplace oluşturulacağı yeri izleme seçeneği tooselect hello depolama hesabı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d7843-127">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![VM oluşturma](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="d7843-129">Bir Azure Resource Manager şablonu dağıtıyorsanız, tooyour sanal makine kaynağı gidin ve hello tanılama profil bölümü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d7843-129">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="d7843-130">Toouse hello "2015-06-15" API sürümü üstbilgisi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d7843-130">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="d7843-131">Merhaba tanılama profili Bu günlükler tooput istediğiniz yere tooselect hello depolama hesabını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="d7843-131">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

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

<span data-ttu-id="d7843-132">Örnek bir sanal makine önyükleme tanılaması etkin, burada bizim depodaki kullanıma toodeploy.</span><span class="sxs-lookup"><span data-stu-id="d7843-132">toodeploy a sample Virtual Machine with boot diagnostics enabled, check out our repo here.</span></span>

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="d7843-133">Mevcut bir sanal makineyi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="d7843-133">Update an existing virtual machine</span></span> ##

<span data-ttu-id="d7843-134">tooenable önyükleme tanılaması hello Portal aracılığıyla, mevcut bir sanal makine hello Portal aracılığıyla güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7843-134">tooenable boot diagnostics through hello Portal, you can also update an existing Virtual Machine through hello Portal.</span></span> <span data-ttu-id="d7843-135">Select hello önyükleme tanılaması seçeneği ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d7843-135">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="d7843-136">Merhaba VM tootake etkisi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="d7843-136">Restart hello VM tootake effect.</span></span>

![Mevcut VM’yi güncelleştirme](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

