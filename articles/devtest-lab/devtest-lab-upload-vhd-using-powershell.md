---
title: aaaUpload VHD tooAzure DevTest Labs PowerShell kullanarak dosya | Microsoft Docs
description: "PowerShell kullanarak VHD dosyasını toolab ait depolama hesabı karşıya yükle"
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
ms.openlocfilehash: 9c3ee96e212457b0ef8203714b419350cb97f895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-powershell"></a><span data-ttu-id="1a3ac-103">PowerShell kullanarak VHD dosyasını toolab ait depolama hesabı karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="1a3ac-103">Upload VHD file toolab's storage account using PowerShell</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="1a3ac-104">Azure DevTest Labs'de VHD dosyaları kullanılan tooprovision sanal makinelerdir kullanılan toocreate özel resimler olabilir.</span><span class="sxs-lookup"><span data-stu-id="1a3ac-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="1a3ac-105">Merhaba aşağıdaki adımlar, PowerShell tooupload kullanılarak üzerinden bir VHD dosyası tooa Laboratuvar ait depolama hesabı yol.</span><span class="sxs-lookup"><span data-stu-id="1a3ac-105">hello following steps walk you through using PowerShell tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="1a3ac-106">VHD dosyasını yüklediğiniz sonra hello [bölüm'sonraki adımlar](#next-steps) nasıl toocreate hello özel bir görüntüden VHD dosyasını karşıya göstermeye bazı makaleleri listeler.</span><span class="sxs-lookup"><span data-stu-id="1a3ac-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="1a3ac-107">Diskleri ve Azure içinde VHD'leri hakkında daha fazla bilgi için bkz: [diskler ve sanal makineler için VHD'ler hakkında](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="1a3ac-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="1a3ac-108">Adım adım yönergeler</span><span class="sxs-lookup"><span data-stu-id="1a3ac-108">Step-by-step instructions</span></span>

<span data-ttu-id="1a3ac-109">Merhaba aşağıdaki tooAzure DevTest Labs PowerShell kullanarak bir VHD'yi karşıya aracılığıyla dosyası ilerlemesi adımları.</span><span class="sxs-lookup"><span data-stu-id="1a3ac-109">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using PowerShell.</span></span> 

1. <span data-ttu-id="1a3ac-110">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="1a3ac-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="1a3ac-111">Seçin **daha fazla hizmet**ve ardından **DevTest Labs** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="1a3ac-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="1a3ac-112">Merhaba istenen Laboratuvar labs Hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="1a3ac-112">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="1a3ac-113">Merhaba Laboratuvar'ın dikey penceresinde, seçin **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="1a3ac-113">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="1a3ac-114">Merhaba Laboratuvar üzerinde **yapılandırma** dikey penceresinde, select **özel görüntülerini (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="1a3ac-114">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="1a3ac-115">Merhaba üzerinde **özel görüntüleri** dikey penceresinde, seçin **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1a3ac-115">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="1a3ac-116">Merhaba üzerinde **özel görüntü** dikey penceresinde, select **VHD**.</span><span class="sxs-lookup"><span data-stu-id="1a3ac-116">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="1a3ac-117">Merhaba üzerinde **VHD** dikey penceresinde, select **PowerShell kullanarak bir VHD'yi karşıya**.</span><span class="sxs-lookup"><span data-stu-id="1a3ac-117">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![PowerShell kullanarak VHD karşıya yükle](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. <span data-ttu-id="1a3ac-119">Merhaba üzerinde **PowerShell kullanarak bir görüntüyü karşıya yüklemeden** dikey penceresinde, kopya oluşturulan hello PowerShell komut dosyası tooa metin düzenleyici.</span><span class="sxs-lookup"><span data-stu-id="1a3ac-119">On hello **Upload an image using PowerShell** blade, copy hello generated PowerShell script tooa text editor.</span></span>

1. <span data-ttu-id="1a3ac-120">Merhaba değiştirme **LocalFilePath** hello parametresinin **Ekle AzureVhd** cmdlet toopoint toohello hello tooupload istediğiniz VHD dosyasının konumunu.</span><span class="sxs-lookup"><span data-stu-id="1a3ac-120">Modify hello **LocalFilePath** parameter of hello **Add-AzureVhd** cmdlet toopoint toohello location of hello VHD file you want tooupload.</span></span>

1. <span data-ttu-id="1a3ac-121">Merhaba bir PowerShell isteminde çalıştırın **Ekle AzureVhd** cmdlet (değiştiren hello ile **LocalFilePath** parametresi).</span><span class="sxs-lookup"><span data-stu-id="1a3ac-121">At a PowerShell prompt, run hello **Add-AzureVhd** cmdlet (with hello modified **LocalFilePath** parameter).</span></span>

> [!WARNING] 
> 
> <span data-ttu-id="1a3ac-122">VHD dosyasını karşıya yükleme işleminin hello hello hello VHD dosyasının boyutunu ve bağlantı hızınıza bağlı olarak uzun olabilir.</span><span class="sxs-lookup"><span data-stu-id="1a3ac-122">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a3ac-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1a3ac-123">Next steps</span></span>

- [<span data-ttu-id="1a3ac-124">Azure DevTest Labs hello Azure portal kullanarak bir VHD dosyasında özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="1a3ac-124">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="1a3ac-125">Azure DevTest Labs PowerShell kullanarak bir VHD dosyasında özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="1a3ac-125">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
