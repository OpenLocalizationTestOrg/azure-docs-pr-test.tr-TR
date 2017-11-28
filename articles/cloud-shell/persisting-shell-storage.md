---
title: "Azure bulut Kabuğu (Önizleme) aaaPersist dosyaları | Microsoft Docs"
description: "Azure bulut Kabuk dosyaları nasıl devam ederse gözden geçirme."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: b230453d5551c545553d63559741950206e4f1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a><span data-ttu-id="314e0-103">Azure bulut Kabuk dosyalarında Sürdür</span><span class="sxs-lookup"><span data-stu-id="314e0-103">Persist files in Azure Cloud Shell</span></span>
<span data-ttu-id="314e0-104">Bulut Kabuk oturumlarında Azure dosya depolama toopersist dosyaları yararlanır.</span><span class="sxs-lookup"><span data-stu-id="314e0-104">Cloud Shell takes advantage of Azure File storage toopersist files across sessions.</span></span>

## <a name="set-up-a-clouddrive-file-share"></a><span data-ttu-id="314e0-105">Ayarlanmış bir `clouddrive` dosya paylaşımı</span><span class="sxs-lookup"><span data-stu-id="314e0-105">Set up a `clouddrive` file share</span></span>
<span data-ttu-id="314e0-106">Bulut Kabuk ilk Başlat, yeni veya varolan bir dosya paylaşımı toopersist dosyalardaki oturumları tooassociate ister.</span><span class="sxs-lookup"><span data-stu-id="314e0-106">On initial start, Cloud Shell prompts you tooassociate a new or existing file share toopersist files across sessions.</span></span>

### <a name="create-new-storage"></a><span data-ttu-id="314e0-107">Yeni depolama alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="314e0-107">Create new storage</span></span>

<span data-ttu-id="314e0-108">Temel ayarlar kullanın ve yalnızca bir abonelik seçin, bulut Kabuk üç kaynakları tooyou en yakın olan desteklenen hello bölgede sizin adınıza oluşturur:</span><span class="sxs-lookup"><span data-stu-id="314e0-108">When you use basic settings and select only a subscription, Cloud Shell creates three resources on your behalf in hello supported region that's nearest tooyou:</span></span>
* <span data-ttu-id="314e0-109">Kaynak grubu:`cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="314e0-109">Resource group: `cloud-shell-storage-<region>`</span></span>
* <span data-ttu-id="314e0-110">Depolama hesabı:`cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="314e0-110">Storage account: `cs<uniqueGuid>`</span></span>
* <span data-ttu-id="314e0-111">Dosya Paylaşımı:`cs-<user>-<domain>-com-<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="314e0-111">File share: `cs-<user>-<domain>-com-<uniqueGuid>`</span></span>

![Merhaba abonelik ayarı](media/basic-storage.png)

<span data-ttu-id="314e0-113">Merhaba dosya paylaşımı bağladığı olarak `clouddrive` içinde `$Home` dizin.</span><span class="sxs-lookup"><span data-stu-id="314e0-113">hello file share mounts as `clouddrive` in your `$Home` directory.</span></span> <span data-ttu-id="314e0-114">Merhaba dosya paylaşımının ayrıca ve, otomatik olarak oluşturulan bir 5 GB görüntüsü güncelleştirir ve devam ederse kullanılan toostore olduğundan, `$Home` dizin.</span><span class="sxs-lookup"><span data-stu-id="314e0-114">hello file share is also used toostore a 5-GB image that's created for you and that automatically updates and persists your `$Home` directory.</span></span> <span data-ttu-id="314e0-115">Bu tek seferlik bir işlemdir ve sonraki oturumlarda hello dosya paylaşımına otomatik olarak bağlar.</span><span class="sxs-lookup"><span data-stu-id="314e0-115">This is a one-time action, and hello file share mounts automatically in subsequent sessions.</span></span>

### <a name="use-existing-resources"></a><span data-ttu-id="314e0-116">Var olan kaynakları kullanın</span><span class="sxs-lookup"><span data-stu-id="314e0-116">Use existing resources</span></span>

<span data-ttu-id="314e0-117">Gelişmiş seçeneği hello kullanarak, var olan kaynakların ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="314e0-117">By using hello advanced option, you can associate existing resources.</span></span> <span data-ttu-id="314e0-118">Merhaba depolama Kurulum istemi belirdiğinde seçin **Göster Gelişmiş ayarları** tooview ek seçenekler.</span><span class="sxs-lookup"><span data-stu-id="314e0-118">When hello storage setup prompt appears, select **Show advanced settings** tooview additional options.</span></span> <span data-ttu-id="314e0-119">Var olan dosya paylaşımları alma 5 GB kullanıcı görüntü toopersist, `$Home` dizin.</span><span class="sxs-lookup"><span data-stu-id="314e0-119">Existing file shares receive a 5-GB user image toopersist your `$Home` directory.</span></span> <span data-ttu-id="314e0-120">Merhaba aşağı açılır menüler yerel olarak yedekli & coğrafi olarak yedekli depolama hesapları ve bulut Kabuk bölgeniz için filtrelenir.</span><span class="sxs-lookup"><span data-stu-id="314e0-120">hello drop-down menus are filtered for your Cloud Shell region and for local-redundant & geo-redundant storage accounts.</span></span>

![Kaynak grubu ayarını hello](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a><span data-ttu-id="314e0-122">Bir Azure kaynak İlkesi ile kaynak oluşturma kısıtla</span><span class="sxs-lookup"><span data-stu-id="314e0-122">Restrict resource creation with an Azure resource policy</span></span>
<span data-ttu-id="314e0-123">Bulut Kabuğu'nda oluşturduğunuz depolama hesapları ile etiketlenmiş `ms-resource-usage:azure-cloud-shell`.</span><span class="sxs-lookup"><span data-stu-id="314e0-123">Storage accounts that you create in Cloud Shell are tagged with `ms-resource-usage:azure-cloud-shell`.</span></span> <span data-ttu-id="314e0-124">Toodisallow kullanıcıların bulut Kabuğu'nda depolama hesapları oluşturmak istiyorsanız, oluşturma bir [etiketleri için Azure kaynak İlkesi](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) bu belirli etiketi tarafından tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="314e0-124">If you want toodisallow users from creating storage accounts in Cloud Shell, create an [Azure resource policy for tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) that are triggered by this specific tag.</span></span>

## <a name="how-cloud-shell-works"></a><span data-ttu-id="314e0-125">Bulut Kabuk nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="314e0-125">How Cloud Shell works</span></span>
<span data-ttu-id="314e0-126">Bulut kabuk dosyalar yöntemler aşağıdaki hello her ikisi de ile devam eder:</span><span class="sxs-lookup"><span data-stu-id="314e0-126">Cloud Shell persists files through both of hello following methods:</span></span>
* <span data-ttu-id="314e0-127">Bir disk görüntüsünü oluşturma, `$Home` directory toopersist tüm içeriği hello dizini içinde.</span><span class="sxs-lookup"><span data-stu-id="314e0-127">Creating a disk image of your `$Home` directory toopersist all contents within hello directory.</span></span> <span data-ttu-id="314e0-128">Merhaba disk görüntüsü belirtilen dosya paylaşımınıza kaydedildi `acc_<User>.img` adresindeki `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, ve değişiklikleri otomatik olarak eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="314e0-128">hello disk image is saved in your specified file share as `acc_<User>.img` at `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, and it automatically syncs changes.</span></span>

* <span data-ttu-id="314e0-129">Belirtilen dosya paylaşımı olarak takma `clouddrive` içinde `$Home` doğrudan dosya paylaşımı etkileşim için dizin.</span><span class="sxs-lookup"><span data-stu-id="314e0-129">Mounting your specified file share as `clouddrive` in your `$Home` directory for direct file share interaction.</span></span> <span data-ttu-id="314e0-130">`/Home/<User>/clouddrive`çok eşlenen`fileshare.storage.windows.net/fileshare`.</span><span class="sxs-lookup"><span data-stu-id="314e0-130">`/Home/<User>/clouddrive` is mapped too`fileshare.storage.windows.net/fileshare`.</span></span>
 
> [!NOTE]
> <span data-ttu-id="314e0-131">Tüm dosyaları, `$Home` SSH anahtarları gibi dizini, bağlı dosya paylaşımında depolanan, kullanıcı disk görüntüsü kaldı.</span><span class="sxs-lookup"><span data-stu-id="314e0-131">All files in your `$Home` directory, such as SSH keys, are persisted in your user disk image, which is stored in your mounted file share.</span></span> <span data-ttu-id="314e0-132">Bilgileri kalıcı sırasında en iyi yöntemleri uygulamak, `$Home` dizin ve bağlı dosya paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="314e0-132">Apply best practices when you persist information in your `$Home` directory and mounted file share.</span></span>

## <a name="use-hello-clouddrive-command"></a><span data-ttu-id="314e0-133">Kullanım hello `clouddrive` komutu</span><span class="sxs-lookup"><span data-stu-id="314e0-133">Use hello `clouddrive` command</span></span>
<span data-ttu-id="314e0-134">Bulut kabuğunda denilen bir komut çalıştırabilirsiniz `clouddrive`, hangi, toomanually güncelleştirme hello dosya paylaşımı o takılı tooCloud Kabuk etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="314e0-134">With Cloud Shell, you can run a command called `clouddrive`, which enables you toomanually update hello file share that's mounted tooCloud Shell.</span></span>
<span data-ttu-id="314e0-135">![Merhaba "clouddrive" komutunu çalıştırarak](media/clouddrive-h.png)</span><span class="sxs-lookup"><span data-stu-id="314e0-135">![Running hello "clouddrive" command](media/clouddrive-h.png)</span></span>

## <a name="mount-a-new-clouddrive"></a><span data-ttu-id="314e0-136">Yeni bir bağlama`clouddrive`</span><span class="sxs-lookup"><span data-stu-id="314e0-136">Mount a new `clouddrive`</span></span>

### <a name="prerequisites-for-manual-mounting"></a><span data-ttu-id="314e0-137">El ile bağlama için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="314e0-137">Prerequisites for manual mounting</span></span>
<span data-ttu-id="314e0-138">Hello kullanarak bulut kabuğu ile ilişkili hello dosya paylaşımı güncelleştirebilirsiniz `clouddrive mount` komutu.</span><span class="sxs-lookup"><span data-stu-id="314e0-138">You can update hello file share that's associated with Cloud Shell by using hello `clouddrive mount` command.</span></span>

<span data-ttu-id="314e0-139">Varolan bir dosya paylaşımını bağlama hello depolama hesapları olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="314e0-139">If you mount an existing file share, hello storage accounts must be:</span></span>
* <span data-ttu-id="314e0-140">Yerel olarak yedekli depolama veya coğrafi olarak yedekli depolama toosupport dosya paylaşımları.</span><span class="sxs-lookup"><span data-stu-id="314e0-140">Locally-redundant storage or geo-redundant storage toosupport file shares.</span></span>
* <span data-ttu-id="314e0-141">Atanan bölgenizde bulunur.</span><span class="sxs-lookup"><span data-stu-id="314e0-141">Located in your assigned region.</span></span> <span data-ttu-id="314e0-142">Merhaba bölge ekleme olduğunda hello kaynak grubu adı içinde listelenen toois atanan `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="314e0-142">When you are onboarding, hello region you are assigned toois listed in hello resource group name `cloud-shell-storage-<region>`.</span></span>

### <a name="supported-storage-regions"></a><span data-ttu-id="314e0-143">Desteklenen depolama bölgeleri</span><span class="sxs-lookup"><span data-stu-id="314e0-143">Supported storage regions</span></span>
<span data-ttu-id="314e0-144">Hello Azure dosyaları hello aynı bulunmalıdır bölge onlara bağlanması hello bulut Kabuk makine olarak.</span><span class="sxs-lookup"><span data-stu-id="314e0-144">hello Azure files must reside in hello same region as hello Cloud Shell machine that you're mounting them to.</span></span> <span data-ttu-id="314e0-145">Bulut Kabuk kümeleri şu anda bölgeleri aşağıdaki hello mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="314e0-145">Cloud Shell clusters currently exist in hello following regions:</span></span>
|<span data-ttu-id="314e0-146">Alan</span><span class="sxs-lookup"><span data-stu-id="314e0-146">Area</span></span>|<span data-ttu-id="314e0-147">Bölge</span><span class="sxs-lookup"><span data-stu-id="314e0-147">Region</span></span>|
|---|---|
|<span data-ttu-id="314e0-148">Kuzey ve Güney Amerika</span><span class="sxs-lookup"><span data-stu-id="314e0-148">Americas</span></span>|<span data-ttu-id="314e0-149">Doğu ABD, Orta Güney ABD, Batı ABD</span><span class="sxs-lookup"><span data-stu-id="314e0-149">East US, South Central US, West US</span></span>|
|<span data-ttu-id="314e0-150">Avrupa</span><span class="sxs-lookup"><span data-stu-id="314e0-150">Europe</span></span>|<span data-ttu-id="314e0-151">Kuzey Avrupa, Batı Avrupa</span><span class="sxs-lookup"><span data-stu-id="314e0-151">North Europe, West Europe</span></span>|
|<span data-ttu-id="314e0-152">Asya Pasifik</span><span class="sxs-lookup"><span data-stu-id="314e0-152">Asia Pacific</span></span>|<span data-ttu-id="314e0-153">Hindistan Orta, Güneydoğu Asya</span><span class="sxs-lookup"><span data-stu-id="314e0-153">India Central, Southeast Asia</span></span>|

### <a name="hello-clouddrive-mount-command"></a><span data-ttu-id="314e0-154">Merhaba `clouddrive mount` komutu</span><span class="sxs-lookup"><span data-stu-id="314e0-154">hello `clouddrive mount` command</span></span>

> [!NOTE]
> <span data-ttu-id="314e0-155">Yeni bir dosya paylaşımı takma varsa, yeni bir kullanıcı görüntüsü için oluşturulur, `$Home` dizin, çünkü, önceki `$Home` görüntü hello önceki dosya paylaşımında tutulur.</span><span class="sxs-lookup"><span data-stu-id="314e0-155">If you're mounting a new file share, a new user image is created for your `$Home` directory, because your previous `$Home` image is kept in hello previous file share.</span></span>

<span data-ttu-id="314e0-156">Merhaba çalıştırmak `clouddrive mount` şu parametreler hello komutunu:</span><span class="sxs-lookup"><span data-stu-id="314e0-156">Run hello `clouddrive mount` command with hello following parameters:</span></span>

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

<span data-ttu-id="314e0-157">Daha fazla ayrıntı tooview çalıştırın `clouddrive mount -h`, aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="314e0-157">tooview more details, run `clouddrive mount -h`, as shown here:</span></span>

![Çalışan hello ' clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a><span data-ttu-id="314e0-159">Çıkarın`clouddrive`</span><span class="sxs-lookup"><span data-stu-id="314e0-159">Unmount `clouddrive`</span></span>
<span data-ttu-id="314e0-160">Bu bağlı tooCloud Kabuk dilediğiniz zaman bir dosya paylaşımı çıkarın.</span><span class="sxs-lookup"><span data-stu-id="314e0-160">You can unmount a file share that's mounted tooCloud Shell at any time.</span></span> <span data-ttu-id="314e0-161">Dosya paylaşımınızı kaldırılan olduktan sonra bir sonraki oturumu istendiğinde toomount yeni bir dosya paylaşımı önceki tooyour olacaktır.</span><span class="sxs-lookup"><span data-stu-id="314e0-161">Once your file share is unmounted, you will be prompted toomount a new file share prior tooyour next session.</span></span>

<span data-ttu-id="314e0-162">Bulut Kabuğu'ndan tooremove bir dosya paylaşımı:</span><span class="sxs-lookup"><span data-stu-id="314e0-162">tooremove a file share from Cloud Shell:</span></span>
1. <span data-ttu-id="314e0-163">`clouddrive unmount` öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="314e0-163">Run `clouddrive unmount`.</span></span>
2. <span data-ttu-id="314e0-164">Onayla ve hello istemleri onaylayın.</span><span class="sxs-lookup"><span data-stu-id="314e0-164">Acknowledge and confirm hello prompts.</span></span>

<span data-ttu-id="314e0-165">El ile silmeniz sürece dosya paylaşımınıza tooexist devam eder.</span><span class="sxs-lookup"><span data-stu-id="314e0-165">Your file share will continue tooexist unless you delete it manually.</span></span> <span data-ttu-id="314e0-166">Bulut Kabuk, artık bu dosya paylaşımı için sonraki oturumlarda arar.</span><span class="sxs-lookup"><span data-stu-id="314e0-166">Cloud Shell will no longer search for this file share on subsequent sessions.</span></span>

<span data-ttu-id="314e0-167">Daha fazla ayrıntı tooview çalıştırın `clouddrive unmount -h`, aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="314e0-167">tooview more details, run `clouddrive unmount -h`, as shown here:</span></span>

![Çalışan hello ' clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> <span data-ttu-id="314e0-169">Bu komutu çalıştıran herhangi bir kaynağa silmez.</span><span class="sxs-lookup"><span data-stu-id="314e0-169">Running this command will not delete any resources.</span></span> <span data-ttu-id="314e0-170">El ile bir kaynak grubu, depolama hesabı veya dosya paylaşımı siliniyor eşlenen Kabuk kalıcı olarak silinecek tooCloud, `$Home` directory görüntü ve herhangi bir dosya paylaşımı dosyalarında.</span><span class="sxs-lookup"><span data-stu-id="314e0-170">Manually deleting a resource group, storage account, or file share that is mapped tooCloud Shell will permanently delete your `$Home` directory image and any other files in your file share.</span></span> <span data-ttu-id="314e0-171">Bu eylem geri alınamaz.</span><span class="sxs-lookup"><span data-stu-id="314e0-171">This action cannot be undone.</span></span>

## <a name="list-clouddrive-file-shares"></a><span data-ttu-id="314e0-172">Liste `clouddrive` dosya paylaşımları</span><span class="sxs-lookup"><span data-stu-id="314e0-172">List `clouddrive` file shares</span></span>
<span data-ttu-id="314e0-173">hangi dosya paylaşımı bağlı olarak toodiscover `clouddrive`, hello aşağıdaki komutu çalıştırarak `df` komutu.</span><span class="sxs-lookup"><span data-stu-id="314e0-173">toodiscover which file share is mounted as `clouddrive`, run hello following `df` command.</span></span> 

<span data-ttu-id="314e0-174">Merhaba dosya yolu tooclouddrive hello URL'de, depolama hesabı adı ve dosya paylaşımı gösterir.</span><span class="sxs-lookup"><span data-stu-id="314e0-174">hello file path tooclouddrive shows your storage account name and file share in hello URL.</span></span> <span data-ttu-id="314e0-175">Örneğin, `//storageaccountname.file.core.windows.net/filesharename`</span><span class="sxs-lookup"><span data-stu-id="314e0-175">For example, `//storageaccountname.file.core.windows.net/filesharename`</span></span>

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-toocloud-shell"></a><span data-ttu-id="314e0-176">Aktarım yerel dosyaları tooCloud Kabuk</span><span class="sxs-lookup"><span data-stu-id="314e0-176">Transfer local files tooCloud Shell</span></span>
<span data-ttu-id="314e0-177">Merhaba `clouddrive` dizin eşitlemeler hello Azure portal depolama dikey ile.</span><span class="sxs-lookup"><span data-stu-id="314e0-177">hello `clouddrive` directory syncs with hello Azure portal storage blade.</span></span> <span data-ttu-id="314e0-178">Bu dikey tootransfer yerel dosyaları tooor dosya paylaşımından kullanın.</span><span class="sxs-lookup"><span data-stu-id="314e0-178">Use this blade tootransfer local files tooor from your file share.</span></span> <span data-ttu-id="314e0-179">Merhaba dikey yenilediğinizde bulut Kabuk içinde dosyalar hello dosya depolama GUI yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="314e0-179">Updating files from within Cloud Shell is reflected in hello file storage GUI when you refresh hello blade.</span></span>

### <a name="download-files"></a><span data-ttu-id="314e0-180">Dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="314e0-180">Download files</span></span>

![Yerel dosya listesi](media/download.png)
1. <span data-ttu-id="314e0-182">Hello Azure portal, toohello bağlı dosya paylaşımına gidin.</span><span class="sxs-lookup"><span data-stu-id="314e0-182">In hello Azure portal, go toohello mounted file share.</span></span>
2. <span data-ttu-id="314e0-183">Merhaba hedef dosya seçin.</span><span class="sxs-lookup"><span data-stu-id="314e0-183">Select hello target file.</span></span>
3. <span data-ttu-id="314e0-184">Select hello **karşıdan** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="314e0-184">Select hello **Download** button.</span></span>

### <a name="upload-files"></a><span data-ttu-id="314e0-185">Dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="314e0-185">Upload files</span></span>

![Yerel dosya toobe karşıya](media/upload.png)
1. <span data-ttu-id="314e0-187">Tooyour bağlı dosya paylaşımına gidin.</span><span class="sxs-lookup"><span data-stu-id="314e0-187">Go tooyour mounted file share.</span></span>
2. <span data-ttu-id="314e0-188">Select hello **karşıya** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="314e0-188">Select hello **Upload** button.</span></span>
3. <span data-ttu-id="314e0-189">Merhaba dosya veya tooupload istediğiniz dosyaları seçin.</span><span class="sxs-lookup"><span data-stu-id="314e0-189">Select hello file or files that you want tooupload.</span></span>
4. <span data-ttu-id="314e0-190">Merhaba karşıya yükleme onaylayın.</span><span class="sxs-lookup"><span data-stu-id="314e0-190">Confirm hello upload.</span></span>

<span data-ttu-id="314e0-191">Erişilebilen hello dosyaların görmelisiniz, `clouddrive` bulut Kabuğu'nda dizin.</span><span class="sxs-lookup"><span data-stu-id="314e0-191">You should now see hello files that are accessible in your `clouddrive` directory in Cloud Shell.</span></span>

## <a name="next-steps"></a><span data-ttu-id="314e0-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="314e0-192">Next steps</span></span>
[<span data-ttu-id="314e0-193">Bulut Kabuk hızlı başlangıç</span><span class="sxs-lookup"><span data-stu-id="314e0-193">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="314e0-194">
[Azure File storage hakkında bilgi edinin](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span><span class="sxs-lookup"><span data-stu-id="314e0-194">
[Learn about Azure File storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span></span> <br><span data-ttu-id="314e0-195">
[Depolama etiketler hakkında bilgi edinin](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span><span class="sxs-lookup"><span data-stu-id="314e0-195">
[Learn about storage tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span></span> <br>
