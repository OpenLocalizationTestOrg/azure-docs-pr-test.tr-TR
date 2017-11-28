---
title: aaaUpload VHD tooAzure DevTest Labs AzCopy kullanarak dosya | Microsoft Docs
description: "AzCopy kullanarak VHD dosyasını toolab ait depolama hesabı karşıya yükle"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a><span data-ttu-id="be086-103">AzCopy kullanarak VHD dosyasını toolab ait depolama hesabı karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="be086-103">Upload VHD file toolab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="be086-104">Azure DevTest Labs'de VHD dosyaları kullanılan tooprovision sanal makinelerdir kullanılan toocreate özel resimler olabilir.</span><span class="sxs-lookup"><span data-stu-id="be086-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="be086-105">Aşağıdaki adımları Merhaba, hello AzCopy komut satırı yardımcı programını tooupload kullanılarak üzerinden bir VHD dosyası tooa Laboratuvar ait depolama hesabı yol.</span><span class="sxs-lookup"><span data-stu-id="be086-105">hello following steps walk you through using hello AzCopy command-line utility tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="be086-106">VHD dosyasını yüklediğiniz sonra hello [bölüm'sonraki adımlar](#next-steps) nasıl toocreate hello özel bir görüntüden VHD dosyasını karşıya göstermeye bazı makaleleri listeler.</span><span class="sxs-lookup"><span data-stu-id="be086-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="be086-107">Diskleri ve Azure içinde VHD'leri hakkında daha fazla bilgi için bkz: [diskler ve sanal makineler için VHD'ler hakkında](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="be086-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="be086-108">AzCopy yalnızca Windows bir komut satırı yardımcı programıdır.</span><span class="sxs-lookup"><span data-stu-id="be086-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="be086-109">Adım adım yönergeler</span><span class="sxs-lookup"><span data-stu-id="be086-109">Step-by-step instructions</span></span>

<span data-ttu-id="be086-110">Merhaba adımları ilerlemesi tooAzure DevTest Labs kullanarak bir VHD'yi karşıya size dosya [AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="be086-110">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="be086-111">Merhaba hello Azure portal kullanarak hello Laboratuvar ait depolama hesabı adını alın:</span><span class="sxs-lookup"><span data-stu-id="be086-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

1. <span data-ttu-id="be086-112">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="be086-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="be086-113">Seçin **daha fazla hizmet**ve ardından **DevTest Labs** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="be086-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="be086-114">Merhaba istenen Laboratuvar labs Hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="be086-114">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="be086-115">Merhaba Laboratuvar'ın dikey penceresinde, seçin **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="be086-115">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="be086-116">Merhaba Laboratuvar üzerinde **yapılandırma** dikey penceresinde, select **özel görüntülerini (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="be086-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="be086-117">Merhaba üzerinde **özel görüntüleri** dikey penceresinde, seçin **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="be086-117">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="be086-118">Merhaba üzerinde **özel görüntü** dikey penceresinde, select **VHD**.</span><span class="sxs-lookup"><span data-stu-id="be086-118">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="be086-119">Merhaba üzerinde **VHD** dikey penceresinde, select **PowerShell kullanarak bir VHD'yi karşıya**.</span><span class="sxs-lookup"><span data-stu-id="be086-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![PowerShell kullanarak VHD karşıya yükle](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="be086-121">Merhaba **PowerShell kullanarak bir görüntüyü karşıya yüklemeden** dikey penceresinde görüntüler çağrısı toohello **Ekle AzureVhd** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="be086-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="be086-122">İlk parametre hello (*hedef*) blob kapsayıcısı için URI hello içerir (*yükler*) biçimi aşağıdaki hello içinde:</span><span class="sxs-lookup"><span data-stu-id="be086-122">hello first parameter (*Destination*) contains hello URI for a blob container (*uploads*) in hello following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="be086-123">Merhaba Not daha sonraki adımlarda kullanılmak üzere tam URI.</span><span class="sxs-lookup"><span data-stu-id="be086-123">Make note of hello full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="be086-124">AzCopy kullanarak hello VHD dosyasını karşıya yükle:</span><span class="sxs-lookup"><span data-stu-id="be086-124">Upload hello VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="be086-125">[Merhaba en güncel AzCopy sürümünü karşıdan yükleyip](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="be086-125">[Download and install hello latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="be086-126">Bir komut penceresi açın ve toohello AzCopy yükleme dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="be086-126">Open a command window and navigate toohello AzCopy installation directory.</span></span> <span data-ttu-id="be086-127">İsteğe bağlı olarak, hello AzCopy yükleme konumu tooyour sistem yolu ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be086-127">Optionally, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="be086-128">Varsayılan olarak, AzCopy yüklü toohello directory aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="be086-128">By default, AzCopy is installed toohello following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="be086-129">Merhaba depolama hesabı anahtarı ve blob kapsayıcısı URI kullanarak, komut hello komut isteminde aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="be086-129">Using hello storage account key and blob container URI, run hello following command at hello command prompt.</span></span> <span data-ttu-id="be086-130">Merhaba *vhdFileName* değeri tırnak toobe gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="be086-130">hello *vhdFileName* value needs toobe in quotes.</span></span> <span data-ttu-id="be086-131">VHD dosyasını karşıya yükleme işleminin hello hello hello VHD dosyasının boyutunu ve bağlantı hızınıza bağlı olarak uzun olabilir.</span><span class="sxs-lookup"><span data-stu-id="be086-131">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="be086-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="be086-132">Next steps</span></span>

- [<span data-ttu-id="be086-133">Azure DevTest Labs hello Azure portal kullanarak bir VHD dosyasında özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="be086-133">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="be086-134">Azure DevTest Labs PowerShell kullanarak bir VHD dosyasında özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="be086-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)