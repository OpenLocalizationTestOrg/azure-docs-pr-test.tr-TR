---
title: "Azure portalından Azure Dosya depolamayı yönetme | Microsoft Docs"
description: "Azure portalından Azure Dosya depolamayı yönetmeyi öğrenin."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: d8ffb4359b0efe8da2f3bccb81c987bdeedf1a39
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="how-to-use-azure-file-storage-from-the-azure-portal"></a><span data-ttu-id="d502b-103">Azure portalından Azure Dosya depolamayı yönetme</span><span class="sxs-lookup"><span data-stu-id="d502b-103">How to use Azure File storage from the Azure Portal</span></span>
<span data-ttu-id="d502b-104">[Azure portalı](https://portal.azure.com), Azure Dosya paylaşımlarını yönetmek için bir kullanıcı arabirimi sunar.</span><span class="sxs-lookup"><span data-stu-id="d502b-104">The [Azure portal](https://portal.azure.com) provides a user interface for managing Azure File storage.</span></span> <span data-ttu-id="d502b-105">Web tarayıcınızdan aşağıdaki eylemleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d502b-105">You can perform the following actions from your web browser:</span></span>

* <span data-ttu-id="d502b-106">Dosya Paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d502b-106">Create a File Share</span></span>
* <span data-ttu-id="d502b-107">Dosya paylaşımınızda dosyaları karşıya yükleme ve indirme.</span><span class="sxs-lookup"><span data-stu-id="d502b-107">Upload and download files to and from your file share.</span></span>
* <span data-ttu-id="d502b-108">Her dosya paylaşımının gerçek kullanımını izleme.</span><span class="sxs-lookup"><span data-stu-id="d502b-108">Monitor the actual usage of each file share.</span></span>
* <span data-ttu-id="d502b-109">Dosya paylaşımının boyut kotasını ayarlama.</span><span class="sxs-lookup"><span data-stu-id="d502b-109">Adjust the file share size quota.</span></span>
* <span data-ttu-id="d502b-110">Windows veya Linux istemcisinden dosya paylaşımınızı bağlamak için bağlama komutlarını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d502b-110">Copy the mount commands to use to mount your file share from a Windows or Linux client.</span></span>

## <a name="create-file-share"></a><span data-ttu-id="d502b-111">Dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d502b-111">Create file share</span></span>
1. <span data-ttu-id="d502b-112">Azure Portal’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d502b-112">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="d502b-113">Gezinti menüsünde, **Depolama hesapları** veya **Depolama hesapları (klasik)** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d502b-113">On the navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
    
    ![Portalda dosya paylaşımı oluşturmayı gösteren ekran görüntüsü](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. <span data-ttu-id="d502b-115">Depolama hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="d502b-115">Choose your storage account.</span></span>

    ![Portalda dosya paylaşımı oluşturmayı gösteren ekran görüntüsü](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. <span data-ttu-id="d502b-117">"Dosyalar" hizmetini seçin.</span><span class="sxs-lookup"><span data-stu-id="d502b-117">Choose "Files" service.</span></span>

    ![Portalda dosya paylaşımı oluşturmayı gösteren ekran görüntüsü](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. <span data-ttu-id="d502b-119">"Dosya paylaşımları" seçeneğine tıklayın ve ilk dosya paylaşımınızı oluşturmak üzere bağlantıyı takip edin.</span><span class="sxs-lookup"><span data-stu-id="d502b-119">Click "File shares" and follow the link to create your first file share.</span></span>

    ![Portalda dosya paylaşımı oluşturmayı gösteren ekran görüntüsü](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. <span data-ttu-id="d502b-121">İlk dosya paylaşımınızı oluşturmak üzere dosya paylaşımının adını ve boyutunu (en fazla 5120 GB) girin.</span><span class="sxs-lookup"><span data-stu-id="d502b-121">Fill in the file share name and the size of the file share (up to 5120 GB) to create your first file share.</span></span> <span data-ttu-id="d502b-122">Dosya paylaşımı oluşturulduktan sonra, SMB 2.1 veya SMB 3.0 destekleyen herhangi bir dosya sisteminden bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d502b-122">Once the file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span> <span data-ttu-id="d502b-123">Dosya paylaşımında bulunan **Kota**’ya tıklayarak dosyanızın boyutunu en fazla 5120 GB’a kadar değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d502b-123">You could click on **Quota** on the file share to change the size of the file up to 5120 GB.</span></span> <span data-ttu-id="d502b-124">Azure Dosya depolama kullanıldığında depolamanın tahmini maliyetini hesaplamak lütfen [Azure Fiyatlandırma Hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/)’na bakın.</span><span class="sxs-lookup"><span data-stu-id="d502b-124">Please refer to [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) to estimate the storage cost of using Azure File storage.</span></span>

    ![Portalda dosya paylaşımı oluşturmayı gösteren ekran görüntüsü](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a><span data-ttu-id="d502b-126">Dosyaları yükleme ve indirme</span><span class="sxs-lookup"><span data-stu-id="d502b-126">Upload and download files</span></span>
1. <span data-ttu-id="d502b-127">Daha önce oluşturduğunuz bir dosya paylaşımını seçin.</span><span class="sxs-lookup"><span data-stu-id="d502b-127">Choose one file share your have already created.</span></span>

    ![Portaldan dosya yükleme ve indirmeyi gösteren ekran görüntüsü](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. <span data-ttu-id="d502b-129">Yüklenen dosyalar için kullanıcı arabirimini açmak üzere **Yükle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d502b-129">Click **Upload** to open the user interface for files uploading.</span></span>

    ![Portaldan dosya yüklemeyi gösteren ekran görüntüsü](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-to-file-share"></a><span data-ttu-id="d502b-131">Dosya paylaşımına bağlanma</span><span class="sxs-lookup"><span data-stu-id="d502b-131">Connect to file share</span></span>
-  <span data-ttu-id="d502b-132">Dosya paylaşımını bağlamak üzere Windows ve Linux’tan komut satırı almak için **Bağlan**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d502b-132">Click **Connect** to get the command line for mounting the file share from Windows and Linux.</span></span> <span data-ttu-id="d502b-133">Linux kullanıcıları için, diğer Linux dağıtımlarına yönelik daha fazla bağlama yönergesini [Azure Dosya depolamayı Linux ile kullanma](storage-how-to-use-files-linux.md) bölümünde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d502b-133">For Linux users, you can also refer to [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md) for more mounting instructions for other Linux distributions.</span></span>

    ![Dosya paylaşımını bağlamayı gösteren ekran görüntüsü](media/storage-file-how-to-use-files-portal/use-files-portal-connect.png)
-  <span data-ttu-id="d502b-135">Windows veya Linux’ta dosya paylaşımı bağlama ve Azure VM veya şirket içi makinenizde çalıştırma için komutları kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d502b-135">You can copy the commands for mounting file share on Windows or Linux and run it from you Azure VM or on-premises machine.</span></span>

    ![Windows ve Linux için bağlama komutlarını gösteren ekran görüntüsü](media/storage-file-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

<span data-ttu-id="d502b-137">**İpucu:**</span><span class="sxs-lookup"><span data-stu-id="d502b-137">**Tip:**</span></span>  
<span data-ttu-id="d502b-138">Bağlama için depolama hesabı erişim anahtarını, bağlan sayfasının en altındaki **Bu depolama hesabı için erişim anahtarlarını görüntüleyin** alanına tıklayarak bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d502b-138">To find the storage account access key for mounting, click on **View access keys for this storage account** at the bottom of the connect page.</span></span>

## <a name="see-also"></a><span data-ttu-id="d502b-139">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d502b-139">See also</span></span>
<span data-ttu-id="d502b-140">Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.</span><span class="sxs-lookup"><span data-stu-id="d502b-140">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="d502b-141">SSS</span><span class="sxs-lookup"><span data-stu-id="d502b-141">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="d502b-142">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="d502b-142">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)