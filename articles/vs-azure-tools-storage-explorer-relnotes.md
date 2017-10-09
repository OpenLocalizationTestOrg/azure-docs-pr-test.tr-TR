---
title: "aaaMicrosoft Azure Storage Gezgini (Önizleme) sürüm notları | Microsoft Docs"
description: "Microsoft Azure Storage Gezgini (Önizleme) için sürüm notları"
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a><span data-ttu-id="83f00-103">Microsoft Azure Storage Gezgini (Önizleme) sürüm notları</span><span class="sxs-lookup"><span data-stu-id="83f00-103">Microsoft Azure Storage Explorer (Preview) release notes</span></span>

<span data-ttu-id="83f00-104">Bu makalede Azure Storage Gezgini 0.8.16 için (Önizleme), önceki sürümler için sürüm notları yanı sıra sürüm notları hello sürüm içerir.</span><span class="sxs-lookup"><span data-stu-id="83f00-104">This article contains hello release notes for Azure Storage Explorer 0.8.16 (Preview) release, as well as release notes for previous versions.</span></span>

<span data-ttu-id="83f00-105">[Microsoft Azure Storage Gezgini (Önizleme)](./vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, macOS ve Linux Azure Storage verilerle tooeasily çalışma sağlayan bir tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="83f00-105">[Microsoft Azure Storage Explorer (Preview)](./vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span>

## <a name="version-0816-preview"></a><span data-ttu-id="83f00-106">Sürüm 0.8.16 (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="83f00-106">Version 0.8.16 (Preview)</span></span>
<span data-ttu-id="83f00-107">8/21/2017</span><span class="sxs-lookup"><span data-stu-id="83f00-107">8/21/2017</span></span>

### <a name="download-azure-storage-explorer-0816-preview"></a><span data-ttu-id="83f00-108">Azure Depolama Gezgini (Önizleme) 0.8.16 indirin</span><span class="sxs-lookup"><span data-stu-id="83f00-108">Download Azure Storage Explorer 0.8.16 (Preview)</span></span>
- [<span data-ttu-id="83f00-109">Windows için Azure Storage Gezgini 0.8.16 (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="83f00-109">Azure Storage Explorer 0.8.16 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=708343)
- [<span data-ttu-id="83f00-110">Mac için Azure Storage Gezgini 0.8.16 (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="83f00-110">Azure Storage Explorer 0.8.16 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=708342)
- [<span data-ttu-id="83f00-111">Linux için Azure Storage Gezgini 0.8.16 (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="83f00-111">Azure Storage Explorer 0.8.16 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a><span data-ttu-id="83f00-112">Yeni</span><span class="sxs-lookup"><span data-stu-id="83f00-112">New</span></span>
* <span data-ttu-id="83f00-113">Bir blob açtığınızda, bir değişiklik algılandığında, Depolama Gezgini tooupload hello indirilen dosya ister</span><span class="sxs-lookup"><span data-stu-id="83f00-113">When you open a blob, Storage Explorer will prompt you tooupload hello downloaded file if a change is detected</span></span>
* <span data-ttu-id="83f00-114">Gelişmiş Azure yığın oturum açma deneyimi</span><span class="sxs-lookup"><span data-stu-id="83f00-114">Enhanced Azure Stack sign-in experience</span></span>
* <span data-ttu-id="83f00-115">Çok sayıda küçük karşıya/indirilmesi geliştirilmiş hello performans dosyaları hello aynı saat</span><span class="sxs-lookup"><span data-stu-id="83f00-115">Improved hello performance of uploading/downloading many small files at hello same time</span></span>


### <a name="fixes"></a><span data-ttu-id="83f00-116">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="83f00-116">Fixes</span></span>
* <span data-ttu-id="83f00-117">Bazı blob türleri için çok bir karşıya yükleme çakışması sırasında "replace" seçme bazen hello karşıya yükleme yeniden başlatılıyor neden olur.</span><span class="sxs-lookup"><span data-stu-id="83f00-117">For some blob types, choosing too"replace" during an upload conflict would sometimes result in hello upload being restarted.</span></span> 
* <span data-ttu-id="83f00-118">0.8.15 sürümünde yüklemeleri bazen %99 kabin.</span><span class="sxs-lookup"><span data-stu-id="83f00-118">In version 0.8.15, uploads would sometimes stall at 99%.</span></span>
* <span data-ttu-id="83f00-119">Henüz mevcut tooupload tooa dizin seçerseniz dosyaları tooa dosya paylaşımı, karşıya yüklenirken, yükleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="83f00-119">When uploading files tooa file share, if you chose tooupload tooa directory which did not yet exist, your upload would fail.</span></span>
* <span data-ttu-id="83f00-120">Depolama Gezgini hatalı zaman damgaları paylaşılan erişim imzaları ve tablo sorguları oluşturma.</span><span class="sxs-lookup"><span data-stu-id="83f00-120">Storage Explorer was incorrectly generating time stamps for shared access signatures and table queries.</span></span>


<span data-ttu-id="83f00-121">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="83f00-121">Known Issues</span></span>
* <span data-ttu-id="83f00-122">Bir ad ve anahtar bağlantı dizesi kullanarak şu an çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="83f00-122">Using a name and key connection string does not currently work.</span></span> <span data-ttu-id="83f00-123">Merhaba sonraki sürümde düzeltilecektir.</span><span class="sxs-lookup"><span data-stu-id="83f00-123">It will be fixed in hello next release.</span></span> <span data-ttu-id="83f00-124">O zamana kadar kullandığınız adı ve anahtar ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83f00-124">Until then you can use attach with name and key.</span></span>
* <span data-ttu-id="83f00-125">Merhaba indirme tooopen geçersiz bir Windows dosya adına sahip bir dosya çalışırsanız, bir dosya bulunamadı hatası neden olur.</span><span class="sxs-lookup"><span data-stu-id="83f00-125">If you try tooopen a file with an invalid Windows file name, hello download will result in a file not found error.</span></span>
* <span data-ttu-id="83f00-126">"İptal" görevde tıkladıktan sonra bu görev toocancel bir süre devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="83f00-126">After clicking "Cancel" on a task, it may take a while for that task toocancel.</span></span> <span data-ttu-id="83f00-127">Hello Azure Depolama düğümü kitaplığı kısıtlamasıdır.</span><span class="sxs-lookup"><span data-stu-id="83f00-127">This is a limitation of hello Azure Storage Node library.</span></span>
* <span data-ttu-id="83f00-128">Bir blob karşıya yükleme işlemini tamamladıktan sonra hello karşıya yükleme başlatılan hello sekmesini yenilenir.</span><span class="sxs-lookup"><span data-stu-id="83f00-128">After completing a blob upload, hello tab which initiated hello upload is refreshed.</span></span> <span data-ttu-id="83f00-129">Bu önceki davranış farklıdır ve ayrıca geri toohello kök olduğunuz hello kapsayıcısının gerçekleştirilecek toobe neden olur.</span><span class="sxs-lookup"><span data-stu-id="83f00-129">This is a change from previous behavior, and will also cause you toobe taken back toohello root of hello container you are in.</span></span>
* <span data-ttu-id="83f00-130">Yanlış PIN/akıllı kart sertifika hello sonra sipariş toohave toorestart gerekir seçerseniz Depolama Gezgini kararı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="83f00-130">If you choose hello wrong PIN/Smartcard certificate, then you will need toorestart in order toohave Storage Explorer forget that decision.</span></span>
* <span data-ttu-id="83f00-131">Merhaba Hesap Ayarları panelini tooreenter kimlik bilgileri toofilter abonelikleri gerektiğini gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="83f00-131">hello account settings panel may show that you need tooreenter credentials toofilter subscriptions.</span></span>
* <span data-ttu-id="83f00-132">BLOB'lar (ayrı ayrı veya yeniden adlandırılmış blob kapsayıcısı içinde) yeniden adlandırma anlık görüntüleri korumaz.</span><span class="sxs-lookup"><span data-stu-id="83f00-132">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="83f00-133">Diğer tüm özellikleri ve meta veri BLOB'lar, dosyalar ve varlıklar için bir yeniden adlandırma sırasında korunur.</span><span class="sxs-lookup"><span data-stu-id="83f00-133">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="83f00-134">Azure yığın şu anda dosya paylaşımlarını desteklemez ancak dosya paylaşımlarına düğümü ekli bir Azure yığın depolama hesabı altında görünmeye devam eder.</span><span class="sxs-lookup"><span data-stu-id="83f00-134">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span>
* <span data-ttu-id="83f00-135">Ubuntu 14.04 kullanıcıları, GCC olan toodate tooensure gerekir - bu hello çalıştırarak yapılabilir komutları izleyerek ve, makinenin yeniden başlatılması:</span><span class="sxs-lookup"><span data-stu-id="83f00-135">For users on Ubuntu 14.04, you will need tooensure GCC is up toodate - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* <span data-ttu-id="83f00-136">Ubuntu 17.04 kullanıcıları, tooinstall GConf gerekir - bu komutları aşağıdaki ve, makinenin yeniden başlatılması hello çalıştıran yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="83f00-136">For users on Ubuntu 17.04, you will need tooinstall GConf - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a><span data-ttu-id="83f00-137">Sürüm 0.8.14 (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="83f00-137">Version 0.8.14 (Preview)</span></span>
<span data-ttu-id="83f00-138">06/22/2017</span><span class="sxs-lookup"><span data-stu-id="83f00-138">06/22/2017</span></span>

### <a name="download-azure-storage-explorer-0814-preview"></a><span data-ttu-id="83f00-139">Azure Depolama Gezgini (Önizleme) 0.8.14 indirin</span><span class="sxs-lookup"><span data-stu-id="83f00-139">Download Azure Storage Explorer 0.8.14 (Preview)</span></span>
* [<span data-ttu-id="83f00-140">Windows Azure Depolama Gezgini (Önizleme) 0.8.14 indirin</span><span class="sxs-lookup"><span data-stu-id="83f00-140">Download Azure Storage Explorer 0.8.14 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=809306)
* [<span data-ttu-id="83f00-141">Mac için Azure Storage Gezgini (Önizleme) 0.8.14 indirin</span><span class="sxs-lookup"><span data-stu-id="83f00-141">Download Azure Storage Explorer 0.8.14 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=809307)
* [<span data-ttu-id="83f00-142">Linux için Azure Storage Gezgini (Önizleme) 0.8.14 indirin</span><span class="sxs-lookup"><span data-stu-id="83f00-142">Download Azure Storage Explorer 0.8.14 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a><span data-ttu-id="83f00-143">Yeni</span><span class="sxs-lookup"><span data-stu-id="83f00-143">New</span></span>

* <span data-ttu-id="83f00-144">Sipariş tootake avantajlarından birkaç kritik güvenlik güncelleştirmeleri, güncelleştirilmiş Elektron sürüm too1.7.2</span><span class="sxs-lookup"><span data-stu-id="83f00-144">Updated Electron version too1.7.2 in order tootake advantage of several critical security updates</span></span>
* <span data-ttu-id="83f00-145">Artık hızlı bir şekilde hello çevrimiçi sorun giderme kılavuzu hello Yardım menüsünden erişebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="83f00-145">You can now quickly access hello online troubleshooting guide from hello help menu</span></span>
* <span data-ttu-id="83f00-146">Depolama Gezgini sorun giderme [Kılavuzu][2]</span><span class="sxs-lookup"><span data-stu-id="83f00-146">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="83f00-147">[Yönergeler] [ 3] tooan Azure yığın abonelik bağlanma</span><span class="sxs-lookup"><span data-stu-id="83f00-147">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

### <a name="known-issues"></a><span data-ttu-id="83f00-148">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="83f00-148">Known Issues</span></span>

* <span data-ttu-id="83f00-149">Merhaba Sil klasör onay iletişim düğmeleri hello fare tıklamaları Linux'ta kaydetme yok.</span><span class="sxs-lookup"><span data-stu-id="83f00-149">Buttons on hello delete folder confirmation dialog don't register with hello mouse clicks on Linux.</span></span> <span data-ttu-id="83f00-150">Geçici çözüm toouse hello Enter anahtarı.</span><span class="sxs-lookup"><span data-stu-id="83f00-150">Workaround is toouse hello Enter key</span></span>
* <span data-ttu-id="83f00-151">Yanlış PIN/akıllı kart sertifika hello sonra sipariş toohave Depolama Gezgini toorestart gerekir seçerseniz hello karar unuttunuz</span><span class="sxs-lookup"><span data-stu-id="83f00-151">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="83f00-152">BLOB'ları veya aynı hello yüklenen dosyalar 3'ten fazla gruba sahip zaman hatalara neden olabilir</span><span class="sxs-lookup"><span data-stu-id="83f00-152">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="83f00-153">Merhaba Hesap Ayarları panelini sipariş toofilter abonelikleri tooreenter kimlik bilgilerine ihtiyacınız gösterebilir</span><span class="sxs-lookup"><span data-stu-id="83f00-153">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="83f00-154">BLOB'lar (ayrı ayrı veya yeniden adlandırılmış blob kapsayıcısı içinde) yeniden adlandırma anlık görüntüleri korumaz.</span><span class="sxs-lookup"><span data-stu-id="83f00-154">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="83f00-155">Diğer tüm özellikleri ve meta veri BLOB'lar, dosyalar ve varlıklar için bir yeniden adlandırma sırasında korunur.</span><span class="sxs-lookup"><span data-stu-id="83f00-155">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="83f00-156">Azure yığın şu anda dosya paylaşımlarını desteklemez ancak dosya paylaşımlarına düğümü ekli bir Azure yığın depolama hesabı altında görünmeye devam eder.</span><span class="sxs-lookup"><span data-stu-id="83f00-156">Although Azure Stack doesn't currently support File Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="83f00-157">Gcc sürüm güncelleştirilmiş veya yükseltilmiş – adımları tooupgrade Ubuntu 14.04 yükleme gereksinimleri aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="83f00-157">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a><span data-ttu-id="83f00-158">Önceki sürümler</span><span class="sxs-lookup"><span data-stu-id="83f00-158">Previous releases</span></span>

* [<span data-ttu-id="83f00-159">Sürüm 0.8.13</span><span class="sxs-lookup"><span data-stu-id="83f00-159">Version 0.8.13</span></span>](#version-0813)
* [<span data-ttu-id="83f00-160">Sürüm 0.8.12 / 0.8.11 / 0.8.10</span><span class="sxs-lookup"><span data-stu-id="83f00-160">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>](#version-0812--0811--0810)
* [<span data-ttu-id="83f00-161">Sürüm 0.8.9 / 0.8.8</span><span class="sxs-lookup"><span data-stu-id="83f00-161">Version 0.8.9 / 0.8.8</span></span>](#version-089--088)
* [<span data-ttu-id="83f00-162">Sürüm 0.8.7</span><span class="sxs-lookup"><span data-stu-id="83f00-162">Version 0.8.7</span></span>](#version-087)
* [<span data-ttu-id="83f00-163">Sürüm 0.8.6</span><span class="sxs-lookup"><span data-stu-id="83f00-163">Version 0.8.6</span></span>](#version-086)
* [<span data-ttu-id="83f00-164">Sürüm 0.8.5</span><span class="sxs-lookup"><span data-stu-id="83f00-164">Version 0.8.5</span></span>](#version-085)
* [<span data-ttu-id="83f00-165">Sürüm 0.8.4</span><span class="sxs-lookup"><span data-stu-id="83f00-165">Version 0.8.4</span></span>](#version-084)
* [<span data-ttu-id="83f00-166">Sürüm 0.8.3</span><span class="sxs-lookup"><span data-stu-id="83f00-166">Version 0.8.3</span></span>](#version-083)
* [<span data-ttu-id="83f00-167">Sürüm 0.8.2</span><span class="sxs-lookup"><span data-stu-id="83f00-167">Version 0.8.2</span></span>](#version-082)
* [<span data-ttu-id="83f00-168">Sürüm 0.8.0</span><span class="sxs-lookup"><span data-stu-id="83f00-168">Version 0.8.0</span></span>](#version-080)
* [<span data-ttu-id="83f00-169">Sürüm 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="83f00-169">Version 0.7.20160509.0</span></span>](#version-07201605090)
* [<span data-ttu-id="83f00-170">Sürüm 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="83f00-170">Version 0.7.20160325.0</span></span>](#version-07201603250)
* [<span data-ttu-id="83f00-171">Sürüm 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="83f00-171">Version 0.7.20160129.1</span></span>](#version-07201601291)
* [<span data-ttu-id="83f00-172">Sürüm 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="83f00-172">Version 0.7.20160105.0</span></span>](#version-07201601050)
* [<span data-ttu-id="83f00-173">Sürüm 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="83f00-173">Version 0.7.20151116.0</span></span>](#version-07201511160)


### <a name="version-0813"></a><span data-ttu-id="83f00-174">Sürüm 0.8.13</span><span class="sxs-lookup"><span data-stu-id="83f00-174">Version 0.8.13</span></span>
<span data-ttu-id="83f00-175">12.05.2017</span><span class="sxs-lookup"><span data-stu-id="83f00-175">05/12/2017</span></span>

#### <a name="new"></a><span data-ttu-id="83f00-176">Yeni</span><span class="sxs-lookup"><span data-stu-id="83f00-176">New</span></span>

* <span data-ttu-id="83f00-177">Depolama Gezgini sorun giderme [Kılavuzu][2]</span><span class="sxs-lookup"><span data-stu-id="83f00-177">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="83f00-178">[Yönergeler] [ 3] tooan Azure yığın abonelik bağlanma</span><span class="sxs-lookup"><span data-stu-id="83f00-178">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

#### <a name="fixes"></a><span data-ttu-id="83f00-179">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="83f00-179">Fixes</span></span>

* <span data-ttu-id="83f00-180">Sabit: Karşıya dosya yükleme yetersiz bellek hatası neden, yüksek şansınız</span><span class="sxs-lookup"><span data-stu-id="83f00-180">Fixed: File upload had a high chance of causing an out of memory error</span></span>
* <span data-ttu-id="83f00-181">Sabit: Artık PIN/akıllı kart ile oturum</span><span class="sxs-lookup"><span data-stu-id="83f00-181">Fixed: You can now sign in with PIN/Smartcard</span></span>
* <span data-ttu-id="83f00-182">Sabit: Portalda şimdi works Azure Çin, Azure Almanya, Azure ABD devlet kurumları ve Azure yığın açın</span><span class="sxs-lookup"><span data-stu-id="83f00-182">Fixed: Open in Portal now works with Azure China, Azure Germany, Azure US Government, and Azure Stack</span></span>
* <span data-ttu-id="83f00-183">Sabit: klasör tooa blob kapsayıcısı karşıya yüklenirken "Geçersiz işlemi" hata bazen oluşacak</span><span class="sxs-lookup"><span data-stu-id="83f00-183">Fixed: While uploading a folder tooa blob container, an "Illegal operation" error would sometimes occur</span></span>
* <span data-ttu-id="83f00-184">Sabit: Tümünü Seç anlık görüntüleri yönetirken devre dışı bırakıldı</span><span class="sxs-lookup"><span data-stu-id="83f00-184">Fixed: Select all was disabled while managing snapshots</span></span>
* <span data-ttu-id="83f00-185">Sabit: hello temel blob hello meta verileri, anlık görüntüleri hello özelliklerini görüntüledikten sonra üzerine</span><span class="sxs-lookup"><span data-stu-id="83f00-185">Fixed: hello metadata of hello base blob might get overwritten after viewing hello properties of its snapshots</span></span>

#### <a name="known-issues"></a><span data-ttu-id="83f00-186">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="83f00-186">Known Issues</span></span>

* <span data-ttu-id="83f00-187">Yanlış PIN/akıllı kart sertifika hello sonra sipariş toohave Depolama Gezgini toorestart gerekir seçerseniz hello karar unuttunuz</span><span class="sxs-lookup"><span data-stu-id="83f00-187">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="83f00-188">Merhaba yakınlaştırma düzeyini veya uzaklaştırılacağını olsa da, kısa bir süre içinde toohello varsayılan düzeyini sıfırlayabilir</span><span class="sxs-lookup"><span data-stu-id="83f00-188">While zoomed in or out, hello zoom level may momentarily reset toohello default level</span></span>
* <span data-ttu-id="83f00-189">BLOB'ları veya aynı hello yüklenen dosyalar 3'ten fazla gruba sahip zaman hatalara neden olabilir</span><span class="sxs-lookup"><span data-stu-id="83f00-189">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="83f00-190">Merhaba Hesap Ayarları panelini sipariş toofilter abonelikleri tooreenter kimlik bilgilerine ihtiyacınız gösterebilir</span><span class="sxs-lookup"><span data-stu-id="83f00-190">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="83f00-191">BLOB'lar (ayrı ayrı veya yeniden adlandırılmış blob kapsayıcısı içinde) yeniden adlandırma anlık görüntüleri korumaz.</span><span class="sxs-lookup"><span data-stu-id="83f00-191">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="83f00-192">Diğer tüm özellikleri ve meta veri BLOB'lar, dosyalar ve varlıklar için bir yeniden adlandırma sırasında korunur.</span><span class="sxs-lookup"><span data-stu-id="83f00-192">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="83f00-193">Azure yığın şu anda dosya paylaşımlarını desteklemez ancak dosya paylaşımlarına düğümü ekli bir Azure yığın depolama hesabı altında görünmeye devam eder.</span><span class="sxs-lookup"><span data-stu-id="83f00-193">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="83f00-194">Gcc sürüm güncelleştirilmiş veya yükseltilmiş – adımları tooupgrade Ubuntu 14.04 yükleme gereksinimleri aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="83f00-194">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a><span data-ttu-id="83f00-195">Sürüm 0.8.12 / 0.8.11 / 0.8.10</span><span class="sxs-lookup"><span data-stu-id="83f00-195">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>
<span data-ttu-id="83f00-196">04/07/2017</span><span class="sxs-lookup"><span data-stu-id="83f00-196">04/07/2017</span></span>

#### <a name="new"></a><span data-ttu-id="83f00-197">Yeni</span><span class="sxs-lookup"><span data-stu-id="83f00-197">New</span></span>

* <span data-ttu-id="83f00-198">Merhaba güncelleştirme bildirimden bir güncelleştirmeyi yüklediğinizde Depolama Gezgini otomatik olarak kapatılacak</span><span class="sxs-lookup"><span data-stu-id="83f00-198">Storage Explorer will now automatically close when you install an update from hello update notification</span></span>
* <span data-ttu-id="83f00-199">Sık erişilen kaynaklarla çalışmak için Gelişmiş bir deneyim yerinde hızlı erişim sağlar</span><span class="sxs-lookup"><span data-stu-id="83f00-199">In-place quick access provides an enhanced experience for working with your frequently accessed resources</span></span>
* <span data-ttu-id="83f00-200">Merhaba Blob kapsayıcısına düzenleyicisinde kiralık blob ait sanal makine artık görebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="83f00-200">In hello Blob Container editor, you can now see which virtual machine a leased blob belongs to</span></span>
* <span data-ttu-id="83f00-201">Merhaba sol tarafındaki paneli şimdi daraltabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="83f00-201">You can now collapse hello left side panel</span></span>
* <span data-ttu-id="83f00-202">Bulma şimdi hello'de çalışır aynı saat indirme</span><span class="sxs-lookup"><span data-stu-id="83f00-202">Discovery now runs at hello same time as download</span></span>
* <span data-ttu-id="83f00-203">İstatistikleri hello Blob kapsayıcısı, dosya paylaşımı ve tablo düzenleyicileri toosee hello boyutunu kaynak ya da seçimi kullanın</span><span class="sxs-lookup"><span data-stu-id="83f00-203">Use Statistics in hello Blob Container, File Share, and Table editors toosee hello size of your resource or selection</span></span>
* <span data-ttu-id="83f00-204">Oturum açma Active Directory (AAD) tooAzure Azure yığın hesapları dayalı artık kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83f00-204">You can now sign-in tooAzure Active Directory (AAD) based Azure Stack accounts.</span></span> 
* <span data-ttu-id="83f00-205">Karşıya yükleme arşiv üzerinde 32 MB tooPremium depolama hesapları dosyaları artık şunları yapabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="83f00-205">You can now upload archive files over 32MB tooPremium storage accounts</span></span>
* <span data-ttu-id="83f00-206">Geliştirilmiş erişilebilirlik desteği</span><span class="sxs-lookup"><span data-stu-id="83f00-206">Improved accessibility support</span></span>
* <span data-ttu-id="83f00-207">Artık güvenilir Base-64 ekleyebilirsiniz kodlanmış X.509 SSL sertifikalarını giderek tooEdit tarafından -&gt; SSL sertifikalarını -&gt; alma sertifikaları</span><span class="sxs-lookup"><span data-stu-id="83f00-207">You can now add trusted Base-64 encoded X.509 SSL certificates by going tooEdit -&gt; SSL Certificates -&gt; Import Certificates</span></span>

#### <a name="fixes"></a><span data-ttu-id="83f00-208">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="83f00-208">Fixes</span></span>

* <span data-ttu-id="83f00-209">Sabit: bir hesabın kimlik yenilendikten sonra hello ağaç görünümü bazen otomatik olarak yeniler değil</span><span class="sxs-lookup"><span data-stu-id="83f00-209">Fixed: after refreshing an account's credentials, hello tree view would sometimes not automatically refresh</span></span>
* <span data-ttu-id="83f00-210">Sabit: öykünücüsü kuyruklar ve tablolar için bir SAS oluşturma geçersiz bir URL neden olur</span><span class="sxs-lookup"><span data-stu-id="83f00-210">Fixed: generating a SAS for emulator queues and tables would result in an invalid URL</span></span>
* <span data-ttu-id="83f00-211">Sabit: proxy etkinken premium depolama hesapları artık Genişletilebilir</span><span class="sxs-lookup"><span data-stu-id="83f00-211">Fixed: premium storage accounts can now be expanded while a proxy is enabled</span></span>
* <span data-ttu-id="83f00-212">Sabit: hello Uygula düğmesini seçili 1 veya 0 hesapları varsa Yönetim sayfasında çalışmayan hello hesaplarında</span><span class="sxs-lookup"><span data-stu-id="83f00-212">Fixed: hello apply button on hello accounts management page would not work if you had 1 or 0 accounts selected</span></span>
* <span data-ttu-id="83f00-213">Sabit: çakışma çözümü gerektiren BLOB karşıya yükleme - 0.8.11 içinde sabit başarısız olabilir</span><span class="sxs-lookup"><span data-stu-id="83f00-213">Fixed: uploading blobs that require conflict resolutions may fail - fixed in 0.8.11</span></span> 
* <span data-ttu-id="83f00-214">Sabit: geri bildirim gönderme 0.8.12 içinde sabit 0.8.11 içinde-hatalı olan</span><span class="sxs-lookup"><span data-stu-id="83f00-214">Fixed: sending feedback was broken in 0.8.11 - fixed in 0.8.12</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="83f00-215">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="83f00-215">Known Issues</span></span>

* <span data-ttu-id="83f00-216">Too0.8.10 yükselttikten sonra toorefresh gerekir tüm kimlik bilgilerinizi.</span><span class="sxs-lookup"><span data-stu-id="83f00-216">After upgrading too0.8.10, you will need toorefresh all of your credentials.</span></span>
* <span data-ttu-id="83f00-217">Giriş veya çıkış uzaklaştırılacağını olsa da, hello yakınlaştırma düzeyini kısa bir süre içinde toohello varsayılan düzeyini sıfırlayabilir.</span><span class="sxs-lookup"><span data-stu-id="83f00-217">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="83f00-218">BLOB'ları veya aynı hello yüklenen dosyalar 3'ten fazla gruba sahip zaman hatalara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="83f00-218">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>
* <span data-ttu-id="83f00-219">Merhaba Hesap Ayarları panelini sipariş toofilter abonelikleri tooreenter kimlik bilgilerine ihtiyacınız gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="83f00-219">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions.</span></span>
* <span data-ttu-id="83f00-220">BLOB'lar (ayrı ayrı veya yeniden adlandırılmış blob kapsayıcısı içinde) yeniden adlandırma anlık görüntüleri korumaz.</span><span class="sxs-lookup"><span data-stu-id="83f00-220">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="83f00-221">Diğer tüm özellikleri ve meta veri BLOB'lar, dosyalar ve varlıklar için bir yeniden adlandırma sırasında korunur.</span><span class="sxs-lookup"><span data-stu-id="83f00-221">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="83f00-222">Azure yığın şu anda dosya paylaşımlarını desteklemez ancak dosya paylaşımlarına düğümü ekli bir Azure yığın depolama hesabı altında görünmeye devam eder.</span><span class="sxs-lookup"><span data-stu-id="83f00-222">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="83f00-223">Gcc sürüm güncelleştirilmiş veya yükseltilmiş – adımları tooupgrade Ubuntu 14.04 yükleme gereksinimleri aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="83f00-223">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a><span data-ttu-id="83f00-224">Sürüm 0.8.9 / 0.8.8</span><span class="sxs-lookup"><span data-stu-id="83f00-224">Version 0.8.9 / 0.8.8</span></span>
<span data-ttu-id="83f00-225">02/23/2017</span><span class="sxs-lookup"><span data-stu-id="83f00-225">02/23/2017</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="83f00-226">Yeni</span><span class="sxs-lookup"><span data-stu-id="83f00-226">New</span></span>

* <span data-ttu-id="83f00-227">Depolama Gezgini 0.8.9 hello güncelleştirmeleri için en son sürümünü otomatik olarak indirir.</span><span class="sxs-lookup"><span data-stu-id="83f00-227">Storage Explorer 0.8.9 will automatically download hello latest version for updates.</span></span>
* <span data-ttu-id="83f00-228">Düzeltme: bir portal kullanarak bir depolama hesabı hatayla sonuçlandı SAS URI'sini tooattach oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="83f00-228">Hotfix: using a portal generated SAS URI tooattach a storage account would result in an error.</span></span>
* <span data-ttu-id="83f00-229">Şimdi oluşturmak, yönetmek ve blob anlık görüntüleri yükseltin.</span><span class="sxs-lookup"><span data-stu-id="83f00-229">You can now create, manage, and promote blob snapshots.</span></span>
* <span data-ttu-id="83f00-230">Şimdi tooAzure Çin, Azure Almanya ve Azure ABD devlet kurumları hesaplarında oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="83f00-230">You can now sign in tooAzure China, Azure Germany, and Azure US Government accounts.</span></span>
* <span data-ttu-id="83f00-231">Şimdi hello yakınlaştırma düzeyini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83f00-231">You can now change hello zoom level.</span></span> <span data-ttu-id="83f00-232">Uzaklaştır, ve yakınlaştırma sıfırlama hello Görünüm menüsünde tooZoom Hello seçenekleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="83f00-232">Use hello options in hello View menu tooZoom In, Zoom Out, and Reset Zoom.</span></span>
* <span data-ttu-id="83f00-233">Unicode karakterler, BLOB'lar ve dosyalar için kullanıcı meta verilerde artık desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="83f00-233">Unicode characters are now supported in user metadata for blobs and files.</span></span>
* <span data-ttu-id="83f00-234">Erişilebilirlik geliştirmeleri.</span><span class="sxs-lookup"><span data-stu-id="83f00-234">Accessibility improvements.</span></span>
* <span data-ttu-id="83f00-235">Merhaba sonraki sürüme ait sürüm notları hello güncelleştirme bildirimden görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="83f00-235">hello next version's release notes can be viewed from hello update notification.</span></span> <span data-ttu-id="83f00-236">Merhaba geçerli sürüm notları hello Yardım menüsünden de görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83f00-236">You can also view hello current release notes from hello Help menu.</span></span>

#### <a name="fixes"></a><span data-ttu-id="83f00-237">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="83f00-237">Fixes</span></span>

* <span data-ttu-id="83f00-238">Sabit: hello sürüm numarası artık doğru şekilde Windows Denetim Masası'nda görüntülenir</span><span class="sxs-lookup"><span data-stu-id="83f00-238">Fixed: hello version number is now correctly displayed in Control Panel on Windows</span></span>
* <span data-ttu-id="83f00-239">Sabit: arama artık sınırlı too50, 000 düğümleri değil</span><span class="sxs-lookup"><span data-stu-id="83f00-239">Fixed: search is no longer limited too50,000 nodes</span></span>
* <span data-ttu-id="83f00-240">Sabit: hello hedef dizin zaten mevcut değilse karşıya yükleme tooa dosya paylaşımı sürekli başlar</span><span class="sxs-lookup"><span data-stu-id="83f00-240">Fixed: upload tooa file share spun forever if hello destination directory did not already exist</span></span>
* <span data-ttu-id="83f00-241">Sabit: kararlılığı uzun ve indirmelere için</span><span class="sxs-lookup"><span data-stu-id="83f00-241">Fixed: improved stability for long uploads and downloads</span></span>

#### <a name="known-issues"></a><span data-ttu-id="83f00-242">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="83f00-242">Known Issues</span></span>

* <span data-ttu-id="83f00-243">Giriş veya çıkış uzaklaştırılacağını olsa da, hello yakınlaştırma düzeyini kısa bir süre içinde toohello varsayılan düzeyini sıfırlayabilir.</span><span class="sxs-lookup"><span data-stu-id="83f00-243">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="83f00-244">Hızlı erişim yalnızca abonelik temel öğeleri ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="83f00-244">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="83f00-245">Yerel kaynaklar veya anahtar veya SAS belirteci üzerinden bağlı kaynakları bu sürümde desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="83f00-245">Local resources or resources attached via key or SAS token are not supported in this release.</span></span>
* <span data-ttu-id="83f00-246">Hızlı erişim birkaç saniye toonavigate toohello hedef kaynak, sahip olduğunuz kaç kaynak bağlı olarak devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="83f00-246">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have.</span></span>
* <span data-ttu-id="83f00-247">BLOB'ları veya aynı hello yüklenen dosyalar 3'ten fazla gruba sahip zaman hatalara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="83f00-247">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>

<span data-ttu-id="83f00-248">12/16/2016</span><span class="sxs-lookup"><span data-stu-id="83f00-248">12/16/2016</span></span>
### <a name="version-087"></a><span data-ttu-id="83f00-249">Sürüm 0.8.7</span><span class="sxs-lookup"><span data-stu-id="83f00-249">Version 0.8.7</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="83f00-250">Yeni</span><span class="sxs-lookup"><span data-stu-id="83f00-250">New</span></span>

* <span data-ttu-id="83f00-251">Nasıl bir güncelleştirme hello başında tooresolve çakışmaları indirin veya oturum hello etkinlikleri penceresindeki kopyalamak seçebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="83f00-251">You can choose how tooresolve conflicts at hello beginning of an update, download or copy session in hello Activities window</span></span>
* <span data-ttu-id="83f00-252">Sekme toosee hello tam bir yol hello depolama kaynağı getirin</span><span class="sxs-lookup"><span data-stu-id="83f00-252">Hover over a tab toosee hello full path of hello storage resource</span></span>
* <span data-ttu-id="83f00-253">Bir sekmede tıklattığınızda hello sol taraftaki gezinti bölmesindeki konumuyla eşitler</span><span class="sxs-lookup"><span data-stu-id="83f00-253">When you click on a tab, it synchronizes with its location in hello left side navigation pane</span></span>

#### <a name="fixes"></a><span data-ttu-id="83f00-254">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="83f00-254">Fixes</span></span>

* <span data-ttu-id="83f00-255">Sabit: Depolama Gezgini güvenilen uygulama Mac üzerinde sunulmuştur</span><span class="sxs-lookup"><span data-stu-id="83f00-255">Fixed: Storage Explorer is now a trusted app on Mac</span></span>
* <span data-ttu-id="83f00-256">Sabit: Ubuntu 14.04 yeniden desteklenir</span><span class="sxs-lookup"><span data-stu-id="83f00-256">Fixed: Ubuntu 14.04 is again supported</span></span>
* <span data-ttu-id="83f00-257">Sabit: Bazen hello eklemek UI abonelikler yüklenirken yanıp sönen hesabı</span><span class="sxs-lookup"><span data-stu-id="83f00-257">Fixed: Sometimes hello add account UI flashes when loading subscriptions</span></span>
* <span data-ttu-id="83f00-258">Sabit: Bazen tüm depolama kaynaklarını hello sol taraftaki Gezinti Bölmesi'nde listelenen</span><span class="sxs-lookup"><span data-stu-id="83f00-258">Fixed: Sometimes not all storage resources were listed in hello left side navigation pane</span></span>
* <span data-ttu-id="83f00-259">Sabit: hello eylem bölmesinde bazen boş eylemler görüntülenir</span><span class="sxs-lookup"><span data-stu-id="83f00-259">Fixed: hello action pane sometimes displayed empty actions</span></span>
* <span data-ttu-id="83f00-260">Sabit: hello pencere boyutu son kapatılan hello oturumundan şimdi korunur</span><span class="sxs-lookup"><span data-stu-id="83f00-260">Fixed: hello window size from hello last closed session is now retained</span></span>
* <span data-ttu-id="83f00-261">Sabit: Hello için birden çok sekme açabilirsiniz hello bağlam menüsünü kullanarak aynı kaynak</span><span class="sxs-lookup"><span data-stu-id="83f00-261">Fixed: You can open multiple tabs for hello same resource using hello context menu</span></span>

#### <a name="known-issues"></a><span data-ttu-id="83f00-262">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="83f00-262">Known Issues</span></span>

* <span data-ttu-id="83f00-263">Hızlı erişim yalnızca abonelik temel öğeleri ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="83f00-263">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="83f00-264">Yerel kaynaklar veya anahtar veya SAS belirteci üzerinden bağlı kaynakları bu sürümde desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="83f00-264">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="83f00-265">Hızlı erişim birkaç saniye toonavigate toohello hedef kaynak, sahip olduğunuz kaç kaynak bağlı olarak alabilir</span><span class="sxs-lookup"><span data-stu-id="83f00-265">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="83f00-266">BLOB'ları veya aynı hello yüklenen dosyalar 3'ten fazla gruba sahip zaman hatalara neden olabilir</span><span class="sxs-lookup"><span data-stu-id="83f00-266">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="83f00-267">Bundan sonra kabaca 50.000 düğümlere - arama arama tanıtıcıları performansı etkilenebilir veya işlenmeyen bir özel duruma neden olabilir</span><span class="sxs-lookup"><span data-stu-id="83f00-267">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>
* <span data-ttu-id="83f00-268">Merhaba macOS üzerinde hello Depolama Gezgini'ni kullanarak ilk kez isteyen kullanıcının izni tooaccess Anahtarlık için birden çok komut istemlerini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83f00-268">For hello first time using hello Storage Explorer on macOS, you might see multiple prompts asking for user's permission tooaccess keychain.</span></span> <span data-ttu-id="83f00-269">Merhaba istemi yeniden göstermeyecektir şekilde her zaman izin ver seçeneğini öneririz</span><span class="sxs-lookup"><span data-stu-id="83f00-269">We suggest you select Always Allow so hello prompt won't show up again</span></span>

<span data-ttu-id="83f00-270">11/18/2016</span><span class="sxs-lookup"><span data-stu-id="83f00-270">11/18/2016</span></span>
### <a name="version-086"></a><span data-ttu-id="83f00-271">Sürüm 0.8.6</span><span class="sxs-lookup"><span data-stu-id="83f00-271">Version 0.8.6</span></span>

#### <a name="new"></a><span data-ttu-id="83f00-272">Yeni</span><span class="sxs-lookup"><span data-stu-id="83f00-272">New</span></span>

* <span data-ttu-id="83f00-273">Artık PIN Hizmetleri toohello hızlı erişim için kolay gezinme en sık kullanılan yapabilecekleriniz</span><span class="sxs-lookup"><span data-stu-id="83f00-273">You can now pin most frequently used services toohello Quick Access for easy navigation</span></span>
* <span data-ttu-id="83f00-274">Artık farklı sekmelerde birden çok düzenleyicileri açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83f00-274">You can now open multiple editors in different tabs.</span></span> <span data-ttu-id="83f00-275">Tek tooopen geçici sekmesini tıklatın. çift tooopen kalıcı sekmesini tıklatın. Ayrıca hello geçici sekmesini toomake üzerinde kalıcı sekmesini tıklatabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="83f00-275">Single click tooopen a temporary tab; double click tooopen a permanent tab. You can also click on hello temporary tab toomake it a permanent tab</span></span>
* <span data-ttu-id="83f00-276">Fark edilebilir performans yapmış olduğunuz ve kararlılık geliştirmeleri için hızlı makinelerde büyük dosyalar için özellikle indirir ve yükler</span><span class="sxs-lookup"><span data-stu-id="83f00-276">We have made noticeable performance and stability improvements for uploads and downloads, especially for large files on fast machines</span></span>
* <span data-ttu-id="83f00-277">Boş "sanal" klasörler şimdi blob kapsayıcı oluşturulabilir</span><span class="sxs-lookup"><span data-stu-id="83f00-277">Empty "virtual" folders can now be created in blob containers</span></span>
* <span data-ttu-id="83f00-278">Şimdi arama yapmak için iki seçeneğiniz vardır böylece biz bizim yeni Gelişmiş substring arama ile kapsamlı arama yeniden sunulmuştur:</span><span class="sxs-lookup"><span data-stu-id="83f00-278">We have re-introduced scoped search with our new enhanced substring search, so you now have two options for searching:</span></span> 
    * <span data-ttu-id="83f00-279">Genel arama - yalnızca hello arama metin kutusuna bir arama terimi girin</span><span class="sxs-lookup"><span data-stu-id="83f00-279">Global search - just enter a search term into hello search textbox</span></span>
    * <span data-ttu-id="83f00-280">Kapsamlı arama - hello Büyüteç simgesini sonraki tooa düğümü, ardından hello yolu, bir arama terimi toohello sonuna ekleyin veya sağ tıklatın ve "Arama gelen burada" seçin</span><span class="sxs-lookup"><span data-stu-id="83f00-280">Scoped search - click hello magnifying glass icon next tooa node, then add a search term toohello end of hello path, or right-click and select "Search from Here"</span></span>
* <span data-ttu-id="83f00-281">Çeşitli temalar ekledik: açık (varsayılan), koyu, yüksek karşıtlık siyah ve yüksek karşıtlık beyaz.</span><span class="sxs-lookup"><span data-stu-id="83f00-281">We have added various themes: Light (default), Dark, High Contrast Black, and High Contrast White.</span></span> <span data-ttu-id="83f00-282">TooEdit - Git&gt; Temalar toochange tema tercihinizi</span><span class="sxs-lookup"><span data-stu-id="83f00-282">Go tooEdit -&gt; Themes toochange your theming preference</span></span>
* <span data-ttu-id="83f00-283">Blob ve dosya özelliklerini değiştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="83f00-283">You can modify Blob and file properties</span></span>
* <span data-ttu-id="83f00-284">Kodlanmış (base64) ve kodlanmamış iletileri artık desteklenmektedir</span><span class="sxs-lookup"><span data-stu-id="83f00-284">We now support encoded (base64) and unencoded queue messages</span></span>
* <span data-ttu-id="83f00-285">Linux üzerinde bir 64-bit işletim sistemi sunulmuştur gerekli.</span><span class="sxs-lookup"><span data-stu-id="83f00-285">On Linux, a 64-bit OS is now required.</span></span> <span data-ttu-id="83f00-286">Bu sürüm için yalnızca 64-bit Ubuntu 16.04.1 destekliyoruz LTS</span><span class="sxs-lookup"><span data-stu-id="83f00-286">For this release we only support 64-bit Ubuntu 16.04.1 LTS</span></span>
* <span data-ttu-id="83f00-287">Biz bizim logosu güncelleştirilmiş!</span><span class="sxs-lookup"><span data-stu-id="83f00-287">We have updated our logo!</span></span>

#### <a name="fixes"></a><span data-ttu-id="83f00-288">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="83f00-288">Fixes</span></span>

* <span data-ttu-id="83f00-289">Sabit: ekran dondurma sorunları</span><span class="sxs-lookup"><span data-stu-id="83f00-289">Fixed: Screen freezing problems</span></span>
* <span data-ttu-id="83f00-290">Sabit: Gelişmiş Güvenlik</span><span class="sxs-lookup"><span data-stu-id="83f00-290">Fixed: Enhanced security</span></span>
* <span data-ttu-id="83f00-291">Sabit: Bazen yinelenen ekli hesapları görünmez</span><span class="sxs-lookup"><span data-stu-id="83f00-291">Fixed: Sometimes duplicate attached accounts could appear</span></span>
* <span data-ttu-id="83f00-292">Sabit: Blob tanımlanmamış bir içerik türüne sahip bir özel durum da oluşturabilir</span><span class="sxs-lookup"><span data-stu-id="83f00-292">Fixed: A blob with an undefined content type could generate an exception</span></span>
* <span data-ttu-id="83f00-293">Sabit: Boş bir tablo üzerinde açılış hello sorgu paneli mümkün değildi</span><span class="sxs-lookup"><span data-stu-id="83f00-293">Fixed: Opening hello Query Panel on an empty table was not possible</span></span>
* <span data-ttu-id="83f00-294">Sabit: arama hatalarda değişir</span><span class="sxs-lookup"><span data-stu-id="83f00-294">Fixed: Varies bugs in Search</span></span>
* <span data-ttu-id="83f00-295">Sabit: "Daha yük" tıklatıldığında 50 too100 yüklenen kaynak hello sayısı artar</span><span class="sxs-lookup"><span data-stu-id="83f00-295">Fixed: Increased hello number of resources loaded from 50 too100 when clicking "Load More"</span></span>
* <span data-ttu-id="83f00-296">Sabit: bir hesap olarak imzalı değilse ilk çalıştırılmasında biz şimdi bu hesap için tüm abonelikleri varsayılan olarak seçin</span><span class="sxs-lookup"><span data-stu-id="83f00-296">Fixed: On first run, if an account is signed into, we now select all subscriptions for that account by default</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="83f00-297">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="83f00-297">Known Issues</span></span>

* <span data-ttu-id="83f00-298">Bu sürümü hello Depolama Gezgini, Ubuntu 14.04 üzerinde çalışmaz</span><span class="sxs-lookup"><span data-stu-id="83f00-298">This release of hello Storage Explorer does not run on Ubuntu 14.04</span></span>
* <span data-ttu-id="83f00-299">tooopen aynı kaynak değil sürekli tıklayın hello için birden fazla sekme hello aynı kaynak.</span><span class="sxs-lookup"><span data-stu-id="83f00-299">tooopen multiple tabs for hello same resource, do not continuously click on hello same resource.</span></span> <span data-ttu-id="83f00-300">Üzerinde başka bir kaynak'ı tıklatın ve geri dönün ve hello özgün kaynak tooopen yeniden başka bir sekmede tıklatın</span><span class="sxs-lookup"><span data-stu-id="83f00-300">Click on another resource and then go back and then click on hello original resource tooopen it again in another tab</span></span> 
* <span data-ttu-id="83f00-301">Hızlı erişim yalnızca abonelik temel öğeleri ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="83f00-301">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="83f00-302">Yerel kaynaklar veya anahtar veya SAS belirteci üzerinden bağlı kaynakları bu sürümde desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="83f00-302">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="83f00-303">Hızlı erişim birkaç saniye toonavigate toohello hedef kaynak, sahip olduğunuz kaç kaynak bağlı olarak alabilir</span><span class="sxs-lookup"><span data-stu-id="83f00-303">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="83f00-304">BLOB'ları veya aynı hello yüklenen dosyalar 3'ten fazla gruba sahip zaman hatalara neden olabilir</span><span class="sxs-lookup"><span data-stu-id="83f00-304">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="83f00-305">Bundan sonra kabaca 50.000 düğümlere - arama arama tanıtıcıları performansı etkilenebilir veya işlenmeyen bir özel duruma neden olabilir</span><span class="sxs-lookup"><span data-stu-id="83f00-305">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>

<span data-ttu-id="83f00-306">10/03/2016</span><span class="sxs-lookup"><span data-stu-id="83f00-306">10/03/2016</span></span>
### <a name="version-085"></a><span data-ttu-id="83f00-307">Sürüm 0.8.5</span><span class="sxs-lookup"><span data-stu-id="83f00-307">Version 0.8.5</span></span>

#### <a name="new"></a><span data-ttu-id="83f00-308">Yeni</span><span class="sxs-lookup"><span data-stu-id="83f00-308">New</span></span>

* <span data-ttu-id="83f00-309">Tooattach tooStorage kullanım Portal tarafından oluşturulan SAS anahtarları artık açabilir hesapları ve kaynakları</span><span class="sxs-lookup"><span data-stu-id="83f00-309">Can now use Portal-generated SAS keys tooattach tooStorage Accounts and resources</span></span>

#### <a name="fixes"></a><span data-ttu-id="83f00-310">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="83f00-310">Fixes</span></span>

* <span data-ttu-id="83f00-311">Sabit: bazen arama sırasında yarış durumu Genişletilebilir olmayan düğümler toobecome neden</span><span class="sxs-lookup"><span data-stu-id="83f00-311">Fixed: race condition during search sometimes caused nodes toobecome non-expandable</span></span>
* <span data-ttu-id="83f00-312">Sabit: "HTTP kullan" tooStorage hesapları hesap adı ve anahtar ile bağlanırken çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="83f00-312">Fixed: "Use HTTP" doesn't work when connecting tooStorage Accounts with account name and key</span></span>
* <span data-ttu-id="83f00-313">Sabit: SAS anahtarları (olanlar için özel Portal tarafından oluşturulan) "sondaki eğik çizgi" bir hata döndürür</span><span class="sxs-lookup"><span data-stu-id="83f00-313">Fixed: SAS keys (specially Portal-generated ones) return a "trailing slash" error</span></span>
* <span data-ttu-id="83f00-314">Sabit: tablo alma sorunları</span><span class="sxs-lookup"><span data-stu-id="83f00-314">Fixed: table import issues</span></span>
    * <span data-ttu-id="83f00-315">Bölüm anahtarı ve satır anahtarını bazen tersine</span><span class="sxs-lookup"><span data-stu-id="83f00-315">Sometimes partition key and row key were reversed</span></span>
    * <span data-ttu-id="83f00-316">"Bölüm anahtarlarını null" oluşturulamıyor tooread</span><span class="sxs-lookup"><span data-stu-id="83f00-316">Unable tooread "null" Partition Keys</span></span>

#### <a name="known-issues"></a><span data-ttu-id="83f00-317">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="83f00-317">Known Issues</span></span>

* <span data-ttu-id="83f00-318">Bundan sonra kabaca 50.000 düğümlere - arama arama tanıtıcıları performans etkilenmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="83f00-318">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>
* <span data-ttu-id="83f00-319">Tooexpand dosyaları çalışılırken bir hata gösterir şekilde azure yığın dosyaları, şu anda desteklemiyor</span><span class="sxs-lookup"><span data-stu-id="83f00-319">Azure Stack doesn't currently support Files, so trying tooexpand Files will show an error</span></span>

<span data-ttu-id="83f00-320">09/12/2016</span><span class="sxs-lookup"><span data-stu-id="83f00-320">09/12/2016</span></span>
### <a name="version-084"></a><span data-ttu-id="83f00-321">Sürüm 0.8.4</span><span class="sxs-lookup"><span data-stu-id="83f00-321">Version 0.8.4</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="83f00-322">Yeni</span><span class="sxs-lookup"><span data-stu-id="83f00-322">New</span></span>

* <span data-ttu-id="83f00-323">Doğrudan bağlantılar toostorage hesapları, kapsayıcıları, kuyruklar, tablolar oluşturmak veya dosya paylaşımları paylaşım ve kolay tooyour - Windows kaynaklara ve Mac OS destek</span><span class="sxs-lookup"><span data-stu-id="83f00-323">Generate direct links toostorage accounts, containers, queues, tables, or file shares for sharing and easy access tooyour resources - Windows and Mac OS support</span></span>
* <span data-ttu-id="83f00-324">Blob kapsayıcılar, tablolar, kuyruklar, dosya paylaşımları veya hello arama kutusuna depolama hesaplarından arayın</span><span class="sxs-lookup"><span data-stu-id="83f00-324">Search for your blob containers, tables, queues, file shares, or storage accounts from hello search box</span></span>
* <span data-ttu-id="83f00-325">Merhaba Tablo Sorgu Oluşturucusu sorgu yan tümcelerinde şimdi gruplandırabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="83f00-325">You can now group clauses in hello table query builder</span></span>
* <span data-ttu-id="83f00-326">Yeniden adlandırın ve blob kapsayıcıları, dosya paylaşımları, tablolar, BLOB'lar, blob klasörleri, dosyaları ve dizinlerden SAS bağlı hesapları ve kapsayıcılar içinde kopyala/yapıştır</span><span class="sxs-lookup"><span data-stu-id="83f00-326">Rename and copy/paste blob containers, file shares, tables, blobs, blob folders, files and directories from within SAS-attached accounts and containers</span></span>
* <span data-ttu-id="83f00-327">Yeniden adlandırma ve kopyalama kapsayıcıları blob ve dosya paylaşımları artık özellikleri ve meta verileri koru</span><span class="sxs-lookup"><span data-stu-id="83f00-327">Renaming and copying blob containers and file shares now preserve properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="83f00-328">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="83f00-328">Fixes</span></span>

* <span data-ttu-id="83f00-329">Sabit: boolean veya ikili özellikleri içermiyorsa tablo varlıkları düzenlenemez.</span><span class="sxs-lookup"><span data-stu-id="83f00-329">Fixed: cannot edit table entities if they contain boolean or binary properties</span></span>

#### <a name="known-issues"></a><span data-ttu-id="83f00-330">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="83f00-330">Known Issues</span></span>

* <span data-ttu-id="83f00-331">Bundan sonra kabaca 50.000 düğümlere - arama arama tanıtıcıları performans etkilenmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="83f00-331">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>

<span data-ttu-id="83f00-332">08/03/2016</span><span class="sxs-lookup"><span data-stu-id="83f00-332">08/03/2016</span></span>
### <a name="version-083"></a><span data-ttu-id="83f00-333">Sürüm 0.8.3</span><span class="sxs-lookup"><span data-stu-id="83f00-333">Version 0.8.3</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="83f00-334">Yeni</span><span class="sxs-lookup"><span data-stu-id="83f00-334">New</span></span>

* <span data-ttu-id="83f00-335">Kapsayıcılar, tablolar, dosya paylaşımları yeniden adlandırma</span><span class="sxs-lookup"><span data-stu-id="83f00-335">Rename containers, tables, file shares</span></span>
* <span data-ttu-id="83f00-336">Gelişmiş Sorgu Oluşturucu deneyim</span><span class="sxs-lookup"><span data-stu-id="83f00-336">Improved Query builder experience</span></span>
* <span data-ttu-id="83f00-337">Özelliği toosave ve yük sorguları</span><span class="sxs-lookup"><span data-stu-id="83f00-337">Ability toosave and load queries</span></span>
* <span data-ttu-id="83f00-338">Doğrudan bağlantılarını toostorage hesapları veya kapsayıcıları, kuyruklar, tablolar veya dosya paylaşımı ve kolayca kaynaklarınıza erişmek için paylaşımları (yalnızca Windows - macOS desteği yakında!)</span><span class="sxs-lookup"><span data-stu-id="83f00-338">Direct links toostorage accounts or containers, queues, tables, or file shares for sharing and easily accessing your resources (Windows-only - macOS support coming soon!)</span></span>
* <span data-ttu-id="83f00-339">Özelliği toomanage CORS kuralları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="83f00-339">Ability toomanage and configure CORS rules</span></span>

#### <a name="fixes"></a><span data-ttu-id="83f00-340">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="83f00-340">Fixes</span></span>

* <span data-ttu-id="83f00-341">Sabit: Microsoft Accounts yeniden kimlik doğrulaması 8-12 saatte gerektirir</span><span class="sxs-lookup"><span data-stu-id="83f00-341">Fixed: Microsoft Accounts require re-authentication every 8-12 hours</span></span>

#### <a name="known-issues"></a><span data-ttu-id="83f00-342">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="83f00-342">Known Issues</span></span>

* <span data-ttu-id="83f00-343">Bazen hello UI dondurulmuş görünebilir - hello penceresinin ekranı kaplamasını bu sorunu çözmenize yardımcı olur</span><span class="sxs-lookup"><span data-stu-id="83f00-343">Sometimes hello UI might appear frozen - maximizing hello window helps resolve this issue</span></span>
* <span data-ttu-id="83f00-344">macOS yükleme yükseltilmiş izinler gerektirebilir</span><span class="sxs-lookup"><span data-stu-id="83f00-344">macOS install may require elevated permissions</span></span>
* <span data-ttu-id="83f00-345">Hesap Ayarları panelini sipariş toofilter abonelikleri tooreenter kimlik bilgilerine ihtiyacınız gösterebilir</span><span class="sxs-lookup"><span data-stu-id="83f00-345">Account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="83f00-346">Yeniden adlandırma dosya paylaşımları, blob kapsayıcıları ve tablolar değil korumak meta verileri veya dosya paylaşım kotası, ortak erişim düzeyi veya erişim ilkeleri gibi hello kapsayıcısı üzerinde diğer özellikleri</span><span class="sxs-lookup"><span data-stu-id="83f00-346">Renaming file shares, blob containers, and tables does not preserve metadata or other properties on hello container, such as file share quota, public access level or access policies</span></span>
* <span data-ttu-id="83f00-347">BLOB'lar (ayrı ayrı veya yeniden adlandırılmış blob kapsayıcısı içinde) yeniden adlandırma anlık görüntüleri korumaz.</span><span class="sxs-lookup"><span data-stu-id="83f00-347">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="83f00-348">Diğer tüm özellikleri ve meta veri BLOB'lar, dosyalar ve varlıklar için bir yeniden adlandırma sırasında korunur</span><span class="sxs-lookup"><span data-stu-id="83f00-348">All other properties and metadata for blobs, files and entities are preserved during a rename</span></span>
* <span data-ttu-id="83f00-349">Kopyalama veya kaynakları yeniden adlandırma SAS bağlı hesapları içinde çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="83f00-349">Copying or renaming resources does not work within SAS-attached accounts</span></span>

<span data-ttu-id="83f00-350">07/07/2016</span><span class="sxs-lookup"><span data-stu-id="83f00-350">07/07/2016</span></span>
### <a name="version-082"></a><span data-ttu-id="83f00-351">Sürüm 0.8.2</span><span class="sxs-lookup"><span data-stu-id="83f00-351">Version 0.8.2</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="83f00-352">Yeni</span><span class="sxs-lookup"><span data-stu-id="83f00-352">New</span></span>

* <span data-ttu-id="83f00-353">Depolama hesapları abonelikler tarafından gruplandırılır; Geliştirme depolama ve anahtar veya SAS aracılığıyla bağlı kaynakları (yerel ve iliştirildiği) düğümünde gösterilir</span><span class="sxs-lookup"><span data-stu-id="83f00-353">Storage Accounts are grouped by subscriptions; development storage and resources attached via key or SAS are shown under (Local and Attached) node</span></span>
* <span data-ttu-id="83f00-354">"Azure hesap ayarları" panelinde hesaplarından Oturumu Kapat</span><span class="sxs-lookup"><span data-stu-id="83f00-354">Sign off from accounts in "Azure Account Settings" panel</span></span>
* <span data-ttu-id="83f00-355">Proxy ayarları tooenable yapılandırma ve oturum açma yönetme</span><span class="sxs-lookup"><span data-stu-id="83f00-355">Configure proxy settings tooenable and manage sign-in</span></span>
* <span data-ttu-id="83f00-356">Oluşturma ve blob kira bölün</span><span class="sxs-lookup"><span data-stu-id="83f00-356">Create and break blob leases</span></span>
* <span data-ttu-id="83f00-357">Açık blob kapsayıcılar, kuyruklar, tablolar ve tek bir tıklatmayla dosyaları</span><span class="sxs-lookup"><span data-stu-id="83f00-357">Open blob containers, queues, tables, and files with single-click</span></span>

#### <a name="fixes"></a><span data-ttu-id="83f00-358">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="83f00-358">Fixes</span></span>

* <span data-ttu-id="83f00-359">Sabit: .NET veya Java kitaplıklarıyla eklenen iletileri kuyruğa düzgün base64 kodlaması çözülür değil</span><span class="sxs-lookup"><span data-stu-id="83f00-359">Fixed: queue messages inserted with .NET or Java libraries are not properly decoded from base64</span></span>
* <span data-ttu-id="83f00-360">Sabit: $metrics tablolar için Blob Storage hesapları gösterilmez</span><span class="sxs-lookup"><span data-stu-id="83f00-360">Fixed: $metrics tables are not shown for Blob Storage accounts</span></span>
* <span data-ttu-id="83f00-361">Sabit: tablolar düğümünü yerel (Geliştirme) depolama için çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="83f00-361">Fixed: tables node does not work for local (Development) storage</span></span>

#### <a name="known-issues"></a><span data-ttu-id="83f00-362">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="83f00-362">Known Issues</span></span>

* <span data-ttu-id="83f00-363">macOS yükleme yükseltilmiş izinler gerektirebilir</span><span class="sxs-lookup"><span data-stu-id="83f00-363">macOS install may require elevated permissions</span></span>

<span data-ttu-id="83f00-364">06/15/2016</span><span class="sxs-lookup"><span data-stu-id="83f00-364">06/15/2016</span></span>
### <a name="version-080"></a><span data-ttu-id="83f00-365">Sürüm 0.8.0</span><span class="sxs-lookup"><span data-stu-id="83f00-365">Version 0.8.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="83f00-366">Yeni</span><span class="sxs-lookup"><span data-stu-id="83f00-366">New</span></span>

* <span data-ttu-id="83f00-367">Dosya Paylaşımı desteği: görüntüleme, karşıya yükleme, indirme, dosyaları ve dizinleri, SAS URI'ler kopyalama (oluşturma ve bağlanma)</span><span class="sxs-lookup"><span data-stu-id="83f00-367">File share support: viewing, uploading, downloading, copying files and directories, SAS URIs (create and connect)</span></span>
* <span data-ttu-id="83f00-368">SAS URI'ler veya hesap anahtarlarla tooStorage bağlanmak için kullanıcı deneyimi geliştirildi</span><span class="sxs-lookup"><span data-stu-id="83f00-368">Improved user experience for connecting tooStorage with SAS URIs or account keys</span></span>
* <span data-ttu-id="83f00-369">Tablo sorgusu sonuçlarını dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="83f00-369">Export table query results</span></span>
* <span data-ttu-id="83f00-370">Tablo sütun yeniden sıralamayı ve özelleştirme</span><span class="sxs-lookup"><span data-stu-id="83f00-370">Table column reordering and customization</span></span>
* <span data-ttu-id="83f00-371">$Logs blob kapsayıcıları ve $metrics tabloları depolama hesapları için etkin Ölçümleriyle görüntüleme</span><span class="sxs-lookup"><span data-stu-id="83f00-371">Viewing $logs blob containers and $metrics tables for Storage Accounts with enabled metrics</span></span>
* <span data-ttu-id="83f00-372">Geliştirilmiş dışarı aktarma ve davranış alma, artık özellik değeri türü içerir</span><span class="sxs-lookup"><span data-stu-id="83f00-372">Improved export and import behavior, now includes property value type</span></span>

#### <a name="fixes"></a><span data-ttu-id="83f00-373">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="83f00-373">Fixes</span></span>

* <span data-ttu-id="83f00-374">Sabit: karşıya yükleme veya büyük BLOB'ları indirme tamamlanmamış yüklemeleri/yüklemeler neden olabilir</span><span class="sxs-lookup"><span data-stu-id="83f00-374">Fixed: uploading or downloading large blobs can result in incomplete uploads/downloads</span></span>
* <span data-ttu-id="83f00-375">Sabit: düzenleme, ekleme ya da bir sayısal dize değeri ("1") sahip bir varlık alma toodouble dönüştürür</span><span class="sxs-lookup"><span data-stu-id="83f00-375">Fixed: editing, adding, or importing an entity with a numeric string value ("1") will convert it toodouble</span></span>
* <span data-ttu-id="83f00-376">Sabit: Oluşturulamıyor tooexpand hello tablo düğümünde hello yerel geliştirme ortamı</span><span class="sxs-lookup"><span data-stu-id="83f00-376">Fixed: Unable tooexpand hello table node in hello local development environment</span></span>

#### <a name="known-issues"></a><span data-ttu-id="83f00-377">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="83f00-377">Known Issues</span></span>

* <span data-ttu-id="83f00-378">$metrics tabloları Blob Depolama hesapları için görünür değildir</span><span class="sxs-lookup"><span data-stu-id="83f00-378">$metrics tables are not visible for Blob Storage accounts</span></span>
* <span data-ttu-id="83f00-379">Merhaba iletileri Base64 kodlama kullanılarak kodlanır, program aracılığıyla eklenen iletileri kuyruğa düzgün görüntülenmeyebilir</span><span class="sxs-lookup"><span data-stu-id="83f00-379">Queue messages added programmatically may not be displayed correctly if hello messages are encoded using Base64 encoding</span></span>

<span data-ttu-id="83f00-380">05/17/2016</span><span class="sxs-lookup"><span data-stu-id="83f00-380">05/17/2016</span></span>
### <a name="version-07201605090"></a><span data-ttu-id="83f00-381">Sürüm 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="83f00-381">Version 0.7.20160509.0</span></span>

#### <a name="new"></a><span data-ttu-id="83f00-382">Yeni</span><span class="sxs-lookup"><span data-stu-id="83f00-382">New</span></span>

* <span data-ttu-id="83f00-383">Daha iyi hata uygulaması için işleme kilitleniyor</span><span class="sxs-lookup"><span data-stu-id="83f00-383">Better error handling for app crashes</span></span>

#### <a name="fixes"></a><span data-ttu-id="83f00-384">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="83f00-384">Fixes</span></span>

* <span data-ttu-id="83f00-385">Oturum açma kimlik bilgileri gerekli olduğunda burada bilgi çubuğu iletileri bazen görünmüyor sabit hata</span><span class="sxs-lookup"><span data-stu-id="83f00-385">Fixed bug where InfoBar messages sometimes don't show up when sign-in credentials were required</span></span>

#### <a name="known-issues"></a><span data-ttu-id="83f00-386">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="83f00-386">Known Issues</span></span>

* <span data-ttu-id="83f00-387">Tablolar: Ekleme, düzenleme, veya "1" veya "1.0" gibi muğlak sayısal bir değere sahip bir özelliği olan bir varlık alma ve kullanıcı çalıştığında toosend hello gibi bir `Edm.String`, hello değeri gelen geri hello istemcisi bir Edm.Double olarak API aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="83f00-387">Tables: Adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>

<span data-ttu-id="83f00-388">03/31/2016</span><span class="sxs-lookup"><span data-stu-id="83f00-388">03/31/2016</span></span>

### <a name="version-07201603250"></a><span data-ttu-id="83f00-389">Sürüm 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="83f00-389">Version 0.7.20160325.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="83f00-390">Yeni</span><span class="sxs-lookup"><span data-stu-id="83f00-390">New</span></span>

* <span data-ttu-id="83f00-391">Tablo desteği: görüntüleme, sorgulanırken, dışa aktarma, içeri aktarma ve varlıklar için CRUD işlemleri</span><span class="sxs-lookup"><span data-stu-id="83f00-391">Table support: viewing, querying, export, import, and CRUD operations for entities</span></span>
* <span data-ttu-id="83f00-392">Sıra desteği: görüntüleme, ekleme, dequeueing iletileri</span><span class="sxs-lookup"><span data-stu-id="83f00-392">Queue support: viewing, adding, dequeueing messages</span></span>
* <span data-ttu-id="83f00-393">Depolama hesapları için SAS URI oluşturma</span><span class="sxs-lookup"><span data-stu-id="83f00-393">Generating SAS URIs for Storage Accounts</span></span>
* <span data-ttu-id="83f00-394">SAS URI'ler bağlanan tooStorage hesaplarıyla</span><span class="sxs-lookup"><span data-stu-id="83f00-394">Connecting tooStorage Accounts with SAS URIs</span></span>
* <span data-ttu-id="83f00-395">Gelecekteki güncelleştirmeleri tooStorage Explorer ilişkin güncelleştirme bildirimlerini</span><span class="sxs-lookup"><span data-stu-id="83f00-395">Update notifications for future updates tooStorage Explorer</span></span>
* <span data-ttu-id="83f00-396">Güncelleştirilmiş Görünüm</span><span class="sxs-lookup"><span data-stu-id="83f00-396">Updated look and feel</span></span>

#### <a name="fixes"></a><span data-ttu-id="83f00-397">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="83f00-397">Fixes</span></span>

* <span data-ttu-id="83f00-398">Performans ve güvenilirlik geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="83f00-398">Performance and reliability improvements</span></span>

### <a name="known-issues-amp-mitigations"></a><span data-ttu-id="83f00-399">Bilinen sorunlar &amp; Azaltıcı Etkenler</span><span class="sxs-lookup"><span data-stu-id="83f00-399">Known Issues &amp; Mitigations</span></span>

* <span data-ttu-id="83f00-400">İndirme büyük blob dosyaların düzgün çalışmıyor - AzCopy kullanırken, biz bu soruna öneririz</span><span class="sxs-lookup"><span data-stu-id="83f00-400">Download of large blob files does not work correctly - we recommend using AzCopy while we address this issue</span></span> 
* <span data-ttu-id="83f00-401">Hesap kimlik bilgilerini değil alınan ya da hello giriş klasörü bulunamıyor veya yazılamaz önbelleğe</span><span class="sxs-lookup"><span data-stu-id="83f00-401">Account credentials will not be retrieved nor cached if hello home folder cannot be found or cannot be written to</span></span>
* <span data-ttu-id="83f00-402">Biz ekleme, düzenleme veya "1" veya "1.0" gibi muğlak sayısal bir değere sahip bir özelliği olan bir varlık alma ve hello kullanıcı çalışırsa toosend olarak bir `Edm.String`, hello değeri gelen geri hello istemcisi bir Edm.Double olarak API aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="83f00-402">If we are adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>
* <span data-ttu-id="83f00-403">Çok satırlı kayıtları içeren CSV dosyalarını içeri aktarırken hello veri kesilmiş Tasarımlı karıştırılmış veya</span><span class="sxs-lookup"><span data-stu-id="83f00-403">When importing CSV files with multiline records, hello data may get chopped or scrambled</span></span>

<span data-ttu-id="83f00-404">02/03/2016</span><span class="sxs-lookup"><span data-stu-id="83f00-404">02/03/2016</span></span>

### <a name="version-07201601291"></a><span data-ttu-id="83f00-405">Sürüm 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="83f00-405">Version 0.7.20160129.1</span></span>

#### <a name="fixes"></a><span data-ttu-id="83f00-406">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="83f00-406">Fixes</span></span>

* <span data-ttu-id="83f00-407">Karşıya yükleme, indirme ve BLOB kopyalama genel performansı</span><span class="sxs-lookup"><span data-stu-id="83f00-407">Improved overall performance when uploading, downloading and copying blobs</span></span>

<span data-ttu-id="83f00-408">01/14/2016</span><span class="sxs-lookup"><span data-stu-id="83f00-408">01/14/2016</span></span>

### <a name="version-07201601050"></a><span data-ttu-id="83f00-409">Sürüm 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="83f00-409">Version 0.7.20160105.0</span></span>

#### <a name="new"></a><span data-ttu-id="83f00-410">Yeni</span><span class="sxs-lookup"><span data-stu-id="83f00-410">New</span></span>

* <span data-ttu-id="83f00-411">Linux desteği (eşlik özellikleri tooOSX)</span><span class="sxs-lookup"><span data-stu-id="83f00-411">Linux support (parity features tooOSX)</span></span>
* <span data-ttu-id="83f00-412">BLOB kapsayıcıları ile paylaşılan erişim imzaları (SAS) anahtar Ekle</span><span class="sxs-lookup"><span data-stu-id="83f00-412">Add blob containers with Shared Access Signatures (SAS) key</span></span>
* <span data-ttu-id="83f00-413">Azure Çin için depolama hesapları ekleme</span><span class="sxs-lookup"><span data-stu-id="83f00-413">Add Storage Accounts for Azure China</span></span>
* <span data-ttu-id="83f00-414">Özel uç noktaları ile depolama hesapları ekleme</span><span class="sxs-lookup"><span data-stu-id="83f00-414">Add Storage Accounts with custom endpoints</span></span>
* <span data-ttu-id="83f00-415">Metin ve resim içeriği BLOB'ları hello açabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="83f00-415">Open and view hello contents text and picture blobs</span></span>
* <span data-ttu-id="83f00-416">Blob özellikleri ve meta verileri görüntüleyin ve düzenleyin</span><span class="sxs-lookup"><span data-stu-id="83f00-416">View and edit blob properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="83f00-417">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="83f00-417">Fixes</span></span>

* <span data-ttu-id="83f00-418">Sabit: karşıya yükleme veya indirme çok sayıda BLOB (500 +) bazen hello uygulama toohave beyaz bir ekran neden olabilir</span><span class="sxs-lookup"><span data-stu-id="83f00-418">Fixed: uploading or download a large number of blobs (500+) may sometimes cause hello app toohave a white screen</span></span> 
* <span data-ttu-id="83f00-419">Sabit: hello kapsayıcı hello odaklanmak yeniden ayarlayana kadar blob kapsayıcısı genel erişim düzeyi ayarlanırken hello yeni değer güncelleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="83f00-419">Fixed: when setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container.</span></span> <span data-ttu-id="83f00-420">Ayrıca, hello iletişim her zaman çok varsayılan olarak "hiçbir ortak erişim" ve hello gerçek geçerli değer değil.</span><span class="sxs-lookup"><span data-stu-id="83f00-420">Also, hello dialog always defaults too"No public access", and not hello actual current value.</span></span>
* <span data-ttu-id="83f00-421">Daha iyi genel klavye/erişilebilirlik ve kullanıcı Arabirimi desteği</span><span class="sxs-lookup"><span data-stu-id="83f00-421">Better overall keyboard/accessibility and UI support</span></span>
* <span data-ttu-id="83f00-422">Boşluk ile uzun olduğunda içerik haritalarında geçmiş metin sarmalar</span><span class="sxs-lookup"><span data-stu-id="83f00-422">Breadcrumbs history text wraps when it's long with white space</span></span>
* <span data-ttu-id="83f00-423">Giriş doğrulaması SAS iletişim destekler</span><span class="sxs-lookup"><span data-stu-id="83f00-423">SAS dialog supports input validation</span></span>
* <span data-ttu-id="83f00-424">Kullanıcı kimlik bilgilerinin süresi dolmuş olsa bile yerel depolama toobe kullanılabilir devam eder</span><span class="sxs-lookup"><span data-stu-id="83f00-424">Local storage continues toobe available even if user credentials have expired</span></span>
* <span data-ttu-id="83f00-425">Merhaba blob explorer hello sağ tarafında açılan blob kapsayıcısı silindiğinde, kapalı</span><span class="sxs-lookup"><span data-stu-id="83f00-425">When an opened blob container is deleted, hello blob explorer on hello right side is closed</span></span>

#### <a name="known-issues"></a><span data-ttu-id="83f00-426">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="83f00-426">Known Issues</span></span>

* <span data-ttu-id="83f00-427">Gcc sürüm güncelleştirilmiş veya yükseltilmiş – adımları tooupgrade Linux yükleme gereksinimleri aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="83f00-427">Linux install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span> 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

<span data-ttu-id="83f00-428">11/18/2015</span><span class="sxs-lookup"><span data-stu-id="83f00-428">11/18/2015</span></span>
### <a name="version-07201511160"></a><span data-ttu-id="83f00-429">Sürüm 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="83f00-429">Version 0.7.20151116.0</span></span>

#### <a name="new"></a><span data-ttu-id="83f00-430">Yeni</span><span class="sxs-lookup"><span data-stu-id="83f00-430">New</span></span>

* <span data-ttu-id="83f00-431">macOS ve Windows sürümleri</span><span class="sxs-lookup"><span data-stu-id="83f00-431">macOS, and Windows versions</span></span>
* <span data-ttu-id="83f00-432">Depolama hesaplarınızı tooview içinde oturum – Kurumsal hesap, Microsoft, 2FA, Account kullanın.</span><span class="sxs-lookup"><span data-stu-id="83f00-432">Sign in tooview your Storage Accounts – use your Org Account, Microsoft Account, 2FA, etc.</span></span>
* <span data-ttu-id="83f00-433">Yerel geliştirme depolama (depolama öykünücüsünü kullanma yalnızca Windows)</span><span class="sxs-lookup"><span data-stu-id="83f00-433">Local development storage (use storage emulator, Windows-only)</span></span>
* <span data-ttu-id="83f00-434">Azure Resource Manager ve klasik kaynak desteği</span><span class="sxs-lookup"><span data-stu-id="83f00-434">Azure Resource Manager and Classic resource support</span></span>
* <span data-ttu-id="83f00-435">Oluşturma ve BLOB, kuyruk veya tablo silme</span><span class="sxs-lookup"><span data-stu-id="83f00-435">Create and delete blobs, queues, or tables</span></span>
* <span data-ttu-id="83f00-436">Belirli BLOB, kuyruk veya tablo Ara</span><span class="sxs-lookup"><span data-stu-id="83f00-436">Search for specific blobs, queues, or tables</span></span>
* <span data-ttu-id="83f00-437">Blob kapsayıcıları Merhaba içeriğine keşfedin</span><span class="sxs-lookup"><span data-stu-id="83f00-437">Explore hello contents of blob containers</span></span>
* <span data-ttu-id="83f00-438">Görüntülemek ve dizinleri gidin</span><span class="sxs-lookup"><span data-stu-id="83f00-438">View and navigate through directories</span></span>
* <span data-ttu-id="83f00-439">Karşıya yükleyin, indirin ve BLOB'ları ve klasörleri silme</span><span class="sxs-lookup"><span data-stu-id="83f00-439">Upload, download, and delete blobs and folders</span></span>
* <span data-ttu-id="83f00-440">Blob özellikleri ve meta verileri görüntüleyin ve düzenleyin</span><span class="sxs-lookup"><span data-stu-id="83f00-440">View and edit blob properties and metadata</span></span>
* <span data-ttu-id="83f00-441">SAS anahtarları oluştur</span><span class="sxs-lookup"><span data-stu-id="83f00-441">Generate SAS keys</span></span>
* <span data-ttu-id="83f00-442">Yönetmek ve depolanan erişim ilkeleri (SAP) oluşturun</span><span class="sxs-lookup"><span data-stu-id="83f00-442">Manage and create Stored Access Policies (SAP)</span></span>
* <span data-ttu-id="83f00-443">Ön eke göre BLOB Ara</span><span class="sxs-lookup"><span data-stu-id="83f00-443">Search for blobs by prefix</span></span>
* <span data-ttu-id="83f00-444">Sürükleme 'n açılan dosyaları tooupload veya indirme</span><span class="sxs-lookup"><span data-stu-id="83f00-444">Drag 'n drop files tooupload or download</span></span>

#### <a name="known-issues"></a><span data-ttu-id="83f00-445">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="83f00-445">Known Issues</span></span>

* <span data-ttu-id="83f00-446">Merhaba kapsayıcı hello odaklanmak yeniden ayarlayana kadar blob kapsayıcısı genel erişim düzeyi ayarlanırken hello yeni değer güncelleştirilmez</span><span class="sxs-lookup"><span data-stu-id="83f00-446">When setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container</span></span>
* <span data-ttu-id="83f00-447">Hello iletişim tooset hello genel erişim düzeyi açtığınızda, bu her zaman "Public erişim yok" hello varsayılan ve hello gerçek geçerli değer değil gösterir</span><span class="sxs-lookup"><span data-stu-id="83f00-447">When you open hello dialog tooset hello public access level, it always shows "No public access" as hello default, and not hello actual current value</span></span>
* <span data-ttu-id="83f00-448">İndirilen BLOB'ları yeniden adlandırılamıyor</span><span class="sxs-lookup"><span data-stu-id="83f00-448">Cannot rename downloaded blobs</span></span>
* <span data-ttu-id="83f00-449">Etkinlik günlüğü girişleri bazen "bir sürüyor takılıyor" ne zaman bir hata oluşur ve hello hata görüntülenmiyor belirtin.</span><span class="sxs-lookup"><span data-stu-id="83f00-449">Activity log entries will sometimes get "stuck" in an in progress state when an error occurs, and hello error is not displayed</span></span>
* <span data-ttu-id="83f00-450">Bazen kilitleniyor kapatır tamamen tooupload çalışırken beyaz veya çok sayıda BLOB indirin</span><span class="sxs-lookup"><span data-stu-id="83f00-450">Sometimes crashes or turns completely white when trying tooupload or download a large number of blobs</span></span>
* <span data-ttu-id="83f00-451">Bazen bir kopyalama işlemi iptal ediliyor çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="83f00-451">Sometimes canceling a copy operation does not work</span></span>
* <span data-ttu-id="83f00-452">Geçersiz bir ad girin ve toocreate devam (sırası/blob/tablosu) kapsayıcı oluşturma sırasında başka farklı kapsayıcı türü altında odak hello yeni tür ayarlanamaz</span><span class="sxs-lookup"><span data-stu-id="83f00-452">During creating a container (blob/queue/table), if you input an invalid name and proceed toocreate another under a different container type you cannot set focus on hello new type</span></span>
* <span data-ttu-id="83f00-453">Yeni bir klasör oluşturulamaz veya klasörünü yeniden adlandırın</span><span class="sxs-lookup"><span data-stu-id="83f00-453">Can't create new folder or rename folder</span></span>




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md