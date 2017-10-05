---
title: "AzCopy kullanarak Azure DevTest Labs için VHD dosyasını karşıya | Microsoft Docs"
description: "AzCopy kullanarak Laboratuvar ait depolama hesabı için VHD dosyasını karşıya yükle"
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
ms.openlocfilehash: a4f43354740d9f17570932b0b9c753f46d67dc33
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-azcopy"></a><span data-ttu-id="bacc6-103">AzCopy kullanarak Laboratuvar ait depolama hesabı için VHD dosyasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="bacc6-103">Upload VHD file to lab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="bacc6-104">Azure DevTest Labs'de VHD dosyaları, sanal makineler sağlamak için kullanılan özel görüntülerinizi oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bacc6-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="bacc6-105">Aşağıdaki adımlar bir VHD dosyasının Laboratuvar ait depolama hesabına yüklemek için AzCopy komut satırı yardımcı programını kullanarak aracılığıyla yol.</span><span class="sxs-lookup"><span data-stu-id="bacc6-105">The following steps walk you through using the AzCopy command-line utility to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="bacc6-106">VHD dosyası yüklediğiniz sonra [bölüm'sonraki adımlar](#next-steps) karşıya yüklenen VHD dosyasından özel bir görüntü oluşturmak nasıl çalışılacağını bazı makaleleri listeler.</span><span class="sxs-lookup"><span data-stu-id="bacc6-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="bacc6-107">Diskleri ve Azure içinde VHD'leri hakkında daha fazla bilgi için bkz: [diskler ve sanal makineler için VHD'ler hakkında](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="bacc6-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="bacc6-108">AzCopy yalnızca Windows bir komut satırı yardımcı programıdır.</span><span class="sxs-lookup"><span data-stu-id="bacc6-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="bacc6-109">Adım adım yönergeler</span><span class="sxs-lookup"><span data-stu-id="bacc6-109">Step-by-step instructions</span></span>

<span data-ttu-id="bacc6-110">Aşağıdaki adımlar bir VHD dosyası aracılığıyla karşıya yükleme Azure DevTest Labs kullanmaya yol [AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="bacc6-110">The following steps walk you through uploading a VHD file to Azure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="bacc6-111">Azure portalını kullanarak laboratuar ait depolama hesabı adını alın:</span><span class="sxs-lookup"><span data-stu-id="bacc6-111">Get the name of the lab's storage account using the Azure portal:</span></span>

1. <span data-ttu-id="bacc6-112">[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="bacc6-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="bacc6-113">**More services**’i (Daha fazla hizmet’i) seçip ardından listeden **DevTest Labs**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="bacc6-113">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="bacc6-114">İstenen Laboratuvar labs listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="bacc6-114">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="bacc6-115">Laboratuvar 's dikey penceresinde, seçin **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="bacc6-115">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="bacc6-116">Laboratuvar üzerinde **yapılandırma** dikey penceresinde, select **özel görüntülerini (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="bacc6-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="bacc6-117">Üzerinde **özel görüntüleri** dikey penceresinde, seçin **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="bacc6-117">On the **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="bacc6-118">Üzerinde **özel görüntü** dikey penceresinde, select **VHD**.</span><span class="sxs-lookup"><span data-stu-id="bacc6-118">On the **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="bacc6-119">Üzerinde **VHD** dikey penceresinde, select **PowerShell kullanarak bir VHD'yi karşıya**.</span><span class="sxs-lookup"><span data-stu-id="bacc6-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![PowerShell kullanarak VHD karşıya yükle](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="bacc6-121">**PowerShell kullanarak bir görüntüyü karşıya yüklemeden** dikey penceresinde görüntüler yapılan bir çağrı **Ekle AzureVhd** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bacc6-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="bacc6-122">İlk parametre (*hedef*) blob kapsayıcısı için URI içerir (*yükler*) şu biçimde:</span><span class="sxs-lookup"><span data-stu-id="bacc6-122">The first parameter (*Destination*) contains the URI for a blob container (*uploads*) in the following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="bacc6-123">Sonraki adımlarda kullanılmak üzere tam URI not edin.</span><span class="sxs-lookup"><span data-stu-id="bacc6-123">Make note of the full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="bacc6-124">AzCopy kullanarak VHD dosyasını karşıya yükle:</span><span class="sxs-lookup"><span data-stu-id="bacc6-124">Upload the VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="bacc6-125">[En güncel AzCopy sürümünü karşıdan yükleyip](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="bacc6-125">[Download and install the latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="bacc6-126">Bir komut penceresi açın ve AzCopy yükleme dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="bacc6-126">Open a command window and navigate to the AzCopy installation directory.</span></span> <span data-ttu-id="bacc6-127">İsteğe bağlı olarak, sistem yolunuza AzCopy yükleme konumu ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bacc6-127">Optionally, you can add the AzCopy installation location to your system path.</span></span> <span data-ttu-id="bacc6-128">Varsayılan olarak, AzCopy şu dizine yüklenir:</span><span class="sxs-lookup"><span data-stu-id="bacc6-128">By default, AzCopy is installed to the following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="bacc6-129">Depolama hesabı anahtarı ve blob kapsayıcısı URI kullanarak, komut istemine aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bacc6-129">Using the storage account key and blob container URI, run the following command at the command prompt.</span></span> <span data-ttu-id="bacc6-130">*VhdFileName* değeri tırnak işaretleri içine olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bacc6-130">The *vhdFileName* value needs to be in quotes.</span></span> <span data-ttu-id="bacc6-131">VHD dosyasını karşıya yükleme işlemi VHD dosyasını ve bağlantı hızı boyutuna bağlı olarak uzun olabilir.</span><span class="sxs-lookup"><span data-stu-id="bacc6-131">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="bacc6-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bacc6-132">Next steps</span></span>

- [<span data-ttu-id="bacc6-133">Azure DevTest Labs Azure portalını kullanarak bir VHD dosyasında özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="bacc6-133">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="bacc6-134">Azure DevTest Labs PowerShell kullanarak bir VHD dosyasında özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="bacc6-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)