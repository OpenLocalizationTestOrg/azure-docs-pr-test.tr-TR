---
title: aaaHow toomanage hello Azure portal'dan Azure File storage | Microsoft Docs
description: "Toouse hello Azure portal toomanage Azure File storage öğrenin."
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
ms.openlocfilehash: 385b99ac1c3d97ca79059ae8229afb53f1e825cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a><span data-ttu-id="df561-103">Nasıl toouse Azure dosya depolama biriminden hello Azure portalı</span><span class="sxs-lookup"><span data-stu-id="df561-103">How toouse Azure File storage from hello Azure Portal</span></span>
<span data-ttu-id="df561-104">Merhaba [Azure portal](https://portal.azure.com) Azure File storage yönetmek için bir kullanıcı arabirimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="df561-104">hello [Azure portal](https://portal.azure.com) provides a user interface for managing Azure File storage.</span></span> <span data-ttu-id="df561-105">Web tarayıcınızdan eylemleri aşağıdaki hello gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="df561-105">You can perform hello following actions from your web browser:</span></span>

* <span data-ttu-id="df561-106">Dosya Paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="df561-106">Create a File Share</span></span>
* <span data-ttu-id="df561-107">Karşıya yükleme ve dosyaları tooand dosya paylaşımından indirin.</span><span class="sxs-lookup"><span data-stu-id="df561-107">Upload and download files tooand from your file share.</span></span>
* <span data-ttu-id="df561-108">Her dosya paylaşımına Hello gerçek kullanımını izleyin.</span><span class="sxs-lookup"><span data-stu-id="df561-108">Monitor hello actual usage of each file share.</span></span>
* <span data-ttu-id="df561-109">Merhaba dosya paylaşım boyutu kotasını ayarlama.</span><span class="sxs-lookup"><span data-stu-id="df561-109">Adjust hello file share size quota.</span></span>
* <span data-ttu-id="df561-110">Merhaba bağlama komutları toouse toomount, dosya paylaşımı bir Windows veya Linux istemciden kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="df561-110">Copy hello mount commands toouse toomount your file share from a Windows or Linux client.</span></span>

## <a name="create-file-share"></a><span data-ttu-id="df561-111">Dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="df561-111">Create file share</span></span>
1. <span data-ttu-id="df561-112">Toohello Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="df561-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="df561-113">Merhaba Gezinti menüsünde **depolama hesapları** veya **depolama hesapları (Klasik)**.</span><span class="sxs-lookup"><span data-stu-id="df561-113">On hello navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
    
    ![Nasıl toocreate dosya paylaşımı hello Portalı'nda gösteren ekran görüntüsü](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. <span data-ttu-id="df561-115">Depolama hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="df561-115">Choose your storage account.</span></span>

    ![Nasıl toocreate dosya paylaşımı hello Portalı'nda gösteren ekran görüntüsü](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. <span data-ttu-id="df561-117">"Dosyalar" hizmetini seçin.</span><span class="sxs-lookup"><span data-stu-id="df561-117">Choose "Files" service.</span></span>

    ![Nasıl toocreate dosya paylaşımı hello Portalı'nda gösteren ekran görüntüsü](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. <span data-ttu-id="df561-119">"Dosya paylaşımları" seçeneğine tıklayın ve ilk dosya paylaşımı hello bağlantı toocreate izleyin.</span><span class="sxs-lookup"><span data-stu-id="df561-119">Click "File shares" and follow hello link toocreate your first file share.</span></span>

    ![Nasıl toocreate dosya paylaşımı hello Portalı'nda gösteren ekran görüntüsü](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. <span data-ttu-id="df561-121">Merhaba dosya paylaşımı adı ve hello dosya paylaşımı (yukarı too5120 GB) toocreate hello boyutunu ilk dosya paylaşımınızı doldurun.</span><span class="sxs-lookup"><span data-stu-id="df561-121">Fill in hello file share name and hello size of hello file share (up too5120 GB) toocreate your first file share.</span></span> <span data-ttu-id="df561-122">Merhaba dosya paylaşımı oluşturulduktan sonra SMB 2.1 veya SMB 3.0 destekleyen herhangi bir dosya sisteminden bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df561-122">Once hello file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span> <span data-ttu-id="df561-123">Tıklayarak **kota** hello dosya paylaşımı toochange hello boyutu hello dosyasını too5120 GB yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="df561-123">You could click on **Quota** on hello file share toochange hello size of hello file up too5120 GB.</span></span> <span data-ttu-id="df561-124">Lütfen çok başvurun[Azure fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/) tooestimate hello depolama maliyeti Azure File storage kullanma.</span><span class="sxs-lookup"><span data-stu-id="df561-124">Please refer too[Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) tooestimate hello storage cost of using Azure File storage.</span></span>

    ![Nasıl toocreate dosya paylaşımı hello Portalı'nda gösteren ekran görüntüsü](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a><span data-ttu-id="df561-126">Dosyaları yükleme ve indirme</span><span class="sxs-lookup"><span data-stu-id="df561-126">Upload and download files</span></span>
1. <span data-ttu-id="df561-127">Daha önce oluşturduğunuz bir dosya paylaşımını seçin.</span><span class="sxs-lookup"><span data-stu-id="df561-127">Choose one file share your have already created.</span></span>

    ![Nasıl tooupload ve yükleme dosyalarından portal hello gösteren ekran görüntüsü](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. <span data-ttu-id="df561-129">Tıklatın **karşıya** hello kullanıcı arabirimi yüklenen dosyalar için açın.</span><span class="sxs-lookup"><span data-stu-id="df561-129">Click **Upload** to open hello user interface for files uploading.</span></span>

    ![Tooupload hello Portalı'ndan nasıl dosyaları gösteren ekran görüntüsü](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a><span data-ttu-id="df561-131">Toofile paylaşımına bağlanmak</span><span class="sxs-lookup"><span data-stu-id="df561-131">Connect toofile share</span></span>
-  <span data-ttu-id="df561-132">Tıklatın **Bağlan** Windows ve Linux bağlama hello dosya paylaşımı için hello komut satırı alınamadı.</span><span class="sxs-lookup"><span data-stu-id="df561-132">Click **Connect** to get hello command line for mounting hello file share from Windows and Linux.</span></span> <span data-ttu-id="df561-133">Linux kullanıcıları için aynı zamanda çok başvurabilirsiniz[nasıl toouse Linux Azure File storage](storage-how-to-use-files-linux.md) diğer Linux dağıtımları için daha fazla bağlama yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="df561-133">For Linux users, you can also refer too[How toouse Azure File storage with Linux](storage-how-to-use-files-linux.md) for more mounting instructions for other Linux distributions.</span></span>

    ![Nasıl toomount hello dosya paylaşımını gösteren ekran görüntüsü](media/storage-file-how-to-use-files-portal/use-files-portal-connect.png)
-  <span data-ttu-id="df561-135">Dosya komutları Windows veya Linux'ta paylaşma ve çalıştırın, Azure VM veya şirket içi makinede hello kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df561-135">You can copy hello commands for mounting file share on Windows or Linux and run it from you Azure VM or on-premises machine.</span></span>

    ![Windows ve Linux için hello bağlama komutları gösteren ekran görüntüsü](media/storage-file-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

<span data-ttu-id="df561-137">**İpucu:**</span><span class="sxs-lookup"><span data-stu-id="df561-137">**Tip:**</span></span>  
<span data-ttu-id="df561-138">toofind hello depolama hesabının erişim anahtarı bağlama, tıklayın **görünüm erişim için bu depolama hesabı anahtarları** hello hello altındaki sayfayı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="df561-138">toofind hello storage account access key for mounting, click on **View access keys for this storage account** at hello bottom of hello connect page.</span></span>

## <a name="see-also"></a><span data-ttu-id="df561-139">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="df561-139">See also</span></span>
<span data-ttu-id="df561-140">Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.</span><span class="sxs-lookup"><span data-stu-id="df561-140">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="df561-141">SSS</span><span class="sxs-lookup"><span data-stu-id="df561-141">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="df561-142">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="df561-142">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)