---
title: aaaUpload VHD dosya tooAzure DevTest Labs Microsoft Azure Storage Gezgini kullanma | Microsoft Docs
description: "Microsoft Azure Storage Gezgini kullanarak VHD dosyasını toolab ait depolama hesabı karşıya yükle"
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
ms.openlocfilehash: 686691e3676cea4b2d7cd8bf045bc43a792c667e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-microsoft-azure-storage-explorer"></a><span data-ttu-id="9977e-103">Microsoft Azure Storage Gezgini kullanarak VHD dosyasını toolab ait depolama hesabı karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="9977e-103">Upload VHD file toolab's storage account using Microsoft Azure Storage Explorer</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="9977e-104">Azure DevTest Labs'de VHD dosyaları kullanılan tooprovision sanal makinelerdir kullanılan toocreate özel resimler olabilir.</span><span class="sxs-lookup"><span data-stu-id="9977e-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="9977e-105">Bu makalede gösterilmektedir nasıl toouse [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooupload VHD dosyası tooa Laboratuvar ait depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="9977e-105">This article illustrates how toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="9977e-106">VHD dosyasını yüklediğiniz sonra hello [bölüm'sonraki adımlar](#next-steps) nasıl toocreate hello özel bir görüntüden VHD dosyasını karşıya göstermeye bazı makaleleri listeler.</span><span class="sxs-lookup"><span data-stu-id="9977e-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="9977e-107">Diskleri ve Azure içinde VHD'leri hakkında daha fazla bilgi için bkz: [diskler ve sanal makineler için VHD'ler hakkında](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="9977e-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="9977e-108">Adım adım yönergeler</span><span class="sxs-lookup"><span data-stu-id="9977e-108">Step-by-step instructions</span></span>

<span data-ttu-id="9977e-109">Merhaba, bir VHD karşıya aracılığıyla dosya kullanarak tooDevTest Labs adımları ilerlemesi [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="9977e-109">hello following steps walk you through uploading a VHD file tooDevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>

1. <span data-ttu-id="9977e-110">[Microsoft Azure Storage Gezgini hello hello en son sürümünü karşıdan yükleyip](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="9977e-110">[Download and install hello latest version of hello Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span></span>

1. <span data-ttu-id="9977e-111">Merhaba hello Azure portal kullanarak hello Laboratuvar ait depolama hesabı adını alın:</span><span class="sxs-lookup"><span data-stu-id="9977e-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

    1. <span data-ttu-id="9977e-112">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="9977e-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
    
    1. <span data-ttu-id="9977e-113">Seçin **daha fazla hizmet**ve ardından **DevTest Labs** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="9977e-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
    
    1. <span data-ttu-id="9977e-114">Merhaba istenen Laboratuvar labs Hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="9977e-114">From hello list of labs, select hello desired lab.</span></span>  
    
    1. <span data-ttu-id="9977e-115">Merhaba Laboratuvar'ın dikey penceresinde, seçin **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="9977e-115">On hello lab's blade, select **Configuration**.</span></span> 
    
    1. <span data-ttu-id="9977e-116">Merhaba Laboratuvar üzerinde **yapılandırma** dikey penceresinde, select **özel görüntülerini (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="9977e-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>
    
    1. <span data-ttu-id="9977e-117">Merhaba üzerinde **özel görüntüleri** dikey penceresinde, seçin **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="9977e-117">On hello **Custom images** blade, Select **+Add**.</span></span> 
    
    1. <span data-ttu-id="9977e-118">Merhaba üzerinde **özel görüntü** dikey penceresinde, select **VHD**.</span><span class="sxs-lookup"><span data-stu-id="9977e-118">On hello **Custom image** blade, select **VHD**.</span></span>
    
    1. <span data-ttu-id="9977e-119">Merhaba üzerinde **VHD** dikey penceresinde, select **PowerShell kullanarak bir VHD'yi karşıya**.</span><span class="sxs-lookup"><span data-stu-id="9977e-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>
    
        ![PowerShell kullanarak VHD karşıya yükle][0]
    
    1. <span data-ttu-id="9977e-121">Merhaba **PowerShell kullanarak bir görüntüyü karşıya yüklemeden** dikey penceresinde görüntüler çağrısı toohello **Ekle AzureVhd** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="9977e-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="9977e-122">İlk parametre hello (*hedef*) biçimi aşağıdaki hello hello laboratuvarda hello depolama hesabı adını içerir:</span><span class="sxs-lookup"><span data-stu-id="9977e-122">hello first parameter (*Destination*) contains hello storage account name for hello lab in hello following format:</span></span>
    
        <span data-ttu-id="9977e-123">https://<Storage-ACCOUNT-Name>.BLOB.Core.Windows.NET/uploads/...</span><span class="sxs-lookup"><span data-stu-id="9977e-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span></span> 

    1. <span data-ttu-id="9977e-124">Sonraki adımlarda kullanılmak üzere hello depolama hesabı adını not edin.</span><span class="sxs-lookup"><span data-stu-id="9977e-124">Make note of hello storage account name as it is used in later steps.</span></span>
    
1. <span data-ttu-id="9977e-125">Tooan Depolama Gezgini'ni kullanarak Azure Abonelik hesabına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="9977e-125">Connect tooan Azure subscription account using Storage Explorer.</span></span>

    > [!TIP] 
    > 
    > <span data-ttu-id="9977e-126">Depolama Gezgini çeşitli bağlantı seçenekleri destekler.</span><span class="sxs-lookup"><span data-stu-id="9977e-126">Storage Explorer supports several connection options.</span></span> <span data-ttu-id="9977e-127">Bu bölümde Azure aboneliğinizle ilişkili bağlantı tooa depolama hesabı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9977e-127">This section illustrates connecting tooa storage account associated with your Azure subscription.</span></span> <span data-ttu-id="9977e-128">toosee Depolama Gezgini tarafından desteklenen diğer bağlantı seçenekleri Merhaba, toohello makalesine başvurun [Depolama Gezgini ile çalışmaya başlama](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="9977e-128">toosee hello other connection options supported by Storage Explorer, refer toohello article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>
 
    1. <span data-ttu-id="9977e-129">Depolama Gezgini'ni açın.</span><span class="sxs-lookup"><span data-stu-id="9977e-129">Open Storage Explorer.</span></span>
    
    1. <span data-ttu-id="9977e-130">Depolama Gezgini'nde seçin **Azure hesap ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="9977e-130">In Storage Explorer, select **Azure Account settings**.</span></span> 
    
        ![Azure hesap ayarları][1]
    
    1. <span data-ttu-id="9977e-132">Hello sol bölmede oturum açtığınız hello Microsoft hesapları görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9977e-132">hello left pane displays hello Microsoft accounts you've logged in to.</span></span> <span data-ttu-id="9977e-133">tooconnect tooanother hesabı, select **Hesap Ekle**, en az bir etkin Azure aboneliği ile ilişkili bir Microsoft hesabıyla hello iletişim kutuları toosign izleyin.</span><span class="sxs-lookup"><span data-stu-id="9977e-133">tooconnect tooanother account, select **Add an account**, and follow hello dialogs toosign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>
    
        ![Hesap ekleme][2]
    
    1. <span data-ttu-id="9977e-135">Başarıyla bir Microsoft hesabıyla oturum açtıktan sonra hello sol bölmesinde bu hesapla ilişkili Azure abonelikleri hello ile doldurur.</span><span class="sxs-lookup"><span data-stu-id="9977e-135">Once you successfully sign in with a Microsoft account, hello left pane populates with hello Azure subscriptions associated with that account.</span></span> <span data-ttu-id="9977e-136">Select hello hangi toowork istediğiniz ve ardından Azure abonelikleri **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="9977e-136">Select hello Azure subscriptions with which you want toowork, and then select **Apply**.</span></span> <span data-ttu-id="9977e-137">(Seçme **tüm abonelikleri** değiştirir hello tüm seçimi veya hello hiçbiri Azure abonelikleri listelenen.)</span><span class="sxs-lookup"><span data-stu-id="9977e-137">(Selecting **All subscriptions** toggles hello selection of all or none of hello listed Azure subscriptions.)</span></span>
    
        ![Azure aboneliklerini seçme][3]
    
    1. <span data-ttu-id="9977e-139">Hello sol bölmede seçili hello Azure abonelikleriyle ilişkilendirilen hello depolama hesapları gösterilir.</span><span class="sxs-lookup"><span data-stu-id="9977e-139">hello left pane displays hello storage accounts associated with hello selected Azure subscriptions.</span></span>
    
        ![Seçili Azure abonelikleri][4]

1. <span data-ttu-id="9977e-141">Merhaba Laboratuvar'ın depolama hesabını bulun:</span><span class="sxs-lookup"><span data-stu-id="9977e-141">Locate hello lab's storage account:</span></span>

    1. <span data-ttu-id="9977e-142">Merhaba Depolama Gezgini sol bölmesinde, bulun ve hello hello Laboratuvar sahip Azure aboneliği için hello düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="9977e-142">In hello Storage Explorer left pane, locate, and expand hello node for hello Azure subscription that owns hello lab.</span></span>
    
    1. <span data-ttu-id="9977e-143">Merhaba aboneliğinin düğümünde genişletin **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="9977e-143">Under hello subscription's node, expand **Storage Accounts**.</span></span>

    1. <span data-ttu-id="9977e-144">Hello Laboratuvar ait depolama hesabı düğüm tooreveal düğümleri genişletin **Blob kapsayıcıları**, **dosya paylaşımları**, **sıraları**, ve **tabloları**.</span><span class="sxs-lookup"><span data-stu-id="9977e-144">Expand hello lab's storage account node tooreveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.</span></span>
    
    1. <span data-ttu-id="9977e-145">Merhaba genişletin **Blob kapsayıcıları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="9977e-145">Expand hello **Blob Containers** node.</span></span>
    
    1. <span data-ttu-id="9977e-146">Merhaba yüklemeleri blob kapsayıcı toodisplay hello sağ bölmede içeriğini seçin.</span><span class="sxs-lookup"><span data-stu-id="9977e-146">Select hello uploads blob container toodisplay its contents in hello right pane.</span></span>
        
        ![Dizin karşıya yükle][5]

1. <span data-ttu-id="9977e-148">Depolama Gezgini'ni kullanarak hello VHD dosyasını karşıya yükle:</span><span class="sxs-lookup"><span data-stu-id="9977e-148">Upload hello VHD file using Storage Explorer:</span></span>

    1. <span data-ttu-id="9977e-149">Merhaba Depolama Gezgini sağ bölmede, hello hello blobları listesini görmelisiniz **yükler** hello Laboratuvar'ın depolama hesabının blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="9977e-149">In hello Storage Explorer right pane, you should see a listing of hello blobs in hello **uploads** blob container of hello lab's storage account.</span></span> <span data-ttu-id="9977e-150">Merhaba blob Düzenleyicisi araç çubuğunda seçin **karşıya yükle**</span><span class="sxs-lookup"><span data-stu-id="9977e-150">On hello blob editor toolbar, select **Upload**</span></span> 
        
        ![Düğme karşıya yükle][6]
    
    1. <span data-ttu-id="9977e-152">Merhaba gelen **karşıya** açılır menüsünde, select **dosyaları karşıya yükleme...** .</span><span class="sxs-lookup"><span data-stu-id="9977e-152">From hello **Upload** drop-down menu, select **Upload files...**.</span></span>
    
    1. <span data-ttu-id="9977e-153">Merhaba üzerinde **dosyaları karşıya yükleme** iletişim, select hello üç nokta.</span><span class="sxs-lookup"><span data-stu-id="9977e-153">On hello **Upload files** dialog, select hello ellipsis.</span></span>
        
        ![Dosya seçin][8]  

    1. <span data-ttu-id="9977e-155">Merhaba üzerinde **Select dosyaları tooupload** iletişim kutusunda, Gözat toohello istenen VHD dosyasını seçin ve ardından **açık**.</span><span class="sxs-lookup"><span data-stu-id="9977e-155">On hello **Select files tooupload** dialog, browse toohello desired VHD file, select it, and then select **Open**.</span></span>
    
    1. <span data-ttu-id="9977e-156">Zaman toohello döndürülen **dosyaları karşıya yükleme** iletişim kutusunda, değişiklik **Blob türü** çok**sayfa blobu**.</span><span class="sxs-lookup"><span data-stu-id="9977e-156">When returned toohello **Upload files** dialog, change **Blob type** too**Page Blob**.</span></span>
    
    1. <span data-ttu-id="9977e-157">**Karşıya Yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="9977e-157">Select **Upload**.</span></span>

        ![Dosya seçin][9]  
    
    1. <span data-ttu-id="9977e-159">Depolama Gezgini Hello **etkinlik günlüğü** bölmesi hello karşıdan yükleme durumu (birlikte bağlantılar toocancel hello karşıya yükleme) gösterir.</span><span class="sxs-lookup"><span data-stu-id="9977e-159">hello Storage Explorer **Activity Log** pane shows hello download status (along with links toocancel hello upload).</span></span> <span data-ttu-id="9977e-160">VHD dosyasını karşıya yükleme işleminin hello hello hello VHD dosyasının boyutunu ve bağlantı hızınıza bağlı olarak uzun olabilir.</span><span class="sxs-lookup"><span data-stu-id="9977e-160">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span> 

        ![Dosya karşıya yükleme durumu][10]  

## <a name="next-steps"></a><span data-ttu-id="9977e-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9977e-162">Next steps</span></span>

- [<span data-ttu-id="9977e-163">Azure DevTest Labs hello Azure portal kullanarak bir VHD dosyasında özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="9977e-163">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="9977e-164">Azure DevTest Labs PowerShell kullanarak bir VHD dosyasında özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="9977e-164">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
