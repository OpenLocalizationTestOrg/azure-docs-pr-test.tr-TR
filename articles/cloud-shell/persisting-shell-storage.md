---
title: "Azure bulut Kabuğu (Önizleme) dosyalarında kalıcı | Microsoft Docs"
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
ms.openlocfilehash: 61a8bfcf3704f361432400771d8fcc8b81927b53
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a><span data-ttu-id="09224-103">Azure bulut Kabuk dosyalarında Sürdür</span><span class="sxs-lookup"><span data-stu-id="09224-103">Persist files in Azure Cloud Shell</span></span>
<span data-ttu-id="09224-104">Bulut Kabuk oturumlarında dosyaları kalıcı hale getirmek için Azure File storage yararlanır.</span><span class="sxs-lookup"><span data-stu-id="09224-104">Cloud Shell takes advantage of Azure File storage to persist files across sessions.</span></span>

## <a name="set-up-a-clouddrive-file-share"></a><span data-ttu-id="09224-105">Ayarlanmış bir `clouddrive` dosya paylaşımı</span><span class="sxs-lookup"><span data-stu-id="09224-105">Set up a `clouddrive` file share</span></span>
<span data-ttu-id="09224-106">İlk Başlat, bulut Kabuk oturumlarında dosyaları kalıcı hale getirmek için yeni veya varolan bir dosya paylaşımı ilişkilendirmek isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="09224-106">On initial start, Cloud Shell prompts you to associate a new or existing file share to persist files across sessions.</span></span>

### <a name="create-new-storage"></a><span data-ttu-id="09224-107">Yeni depolama alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="09224-107">Create new storage</span></span>

<span data-ttu-id="09224-108">Temel ayarlar kullanın ve yalnızca bir abonelik seçin, bulut Kabuk üç kaynakları en yakın olan desteklenen bölgede sizin adınıza oluşturur:</span><span class="sxs-lookup"><span data-stu-id="09224-108">When you use basic settings and select only a subscription, Cloud Shell creates three resources on your behalf in the supported region that's nearest to you:</span></span>
* <span data-ttu-id="09224-109">Kaynak grubu:`cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="09224-109">Resource group: `cloud-shell-storage-<region>`</span></span>
* <span data-ttu-id="09224-110">Depolama hesabı:`cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="09224-110">Storage account: `cs<uniqueGuid>`</span></span>
* <span data-ttu-id="09224-111">Dosya Paylaşımı:`cs-<user>-<domain>-com-<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="09224-111">File share: `cs-<user>-<domain>-com-<uniqueGuid>`</span></span>

![Abonelik ayarı](media/basic-storage.png)

<span data-ttu-id="09224-113">Dosya Paylaşımı bağladığı olarak `clouddrive` içinde `$Home` dizin.</span><span class="sxs-lookup"><span data-stu-id="09224-113">The file share mounts as `clouddrive` in your `$Home` directory.</span></span> <span data-ttu-id="09224-114">Dosya Paylaşımı Ayrıca, sizin yerinize oluşturulur ve otomatik olarak güncelleştirir ve devam ederse, 5 GB görüntü depolamak için kullanılan, `$Home` dizin.</span><span class="sxs-lookup"><span data-stu-id="09224-114">The file share is also used to store a 5-GB image that's created for you and that automatically updates and persists your `$Home` directory.</span></span> <span data-ttu-id="09224-115">Bu tek seferlik bir işlemdir ve dosya paylaşımı sonraki oturumlarda otomatik olarak bağlar.</span><span class="sxs-lookup"><span data-stu-id="09224-115">This is a one-time action, and the file share mounts automatically in subsequent sessions.</span></span>

### <a name="use-existing-resources"></a><span data-ttu-id="09224-116">Var olan kaynakları kullanın</span><span class="sxs-lookup"><span data-stu-id="09224-116">Use existing resources</span></span>

<span data-ttu-id="09224-117">Gelişmiş seçeneğini kullanarak, var olan kaynakların ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09224-117">By using the advanced option, you can associate existing resources.</span></span> <span data-ttu-id="09224-118">Depolama Kurulum istemi belirdiğinde seçin **Göster Gelişmiş ayarları** ek seçenekleri görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="09224-118">When the storage setup prompt appears, select **Show advanced settings** to view additional options.</span></span> <span data-ttu-id="09224-119">Var olan dosya paylaşımları kalıcı hale getirmek için 5 GB kullanıcı görüntüsü almak, `$Home` dizin.</span><span class="sxs-lookup"><span data-stu-id="09224-119">Existing file shares receive a 5-GB user image to persist your `$Home` directory.</span></span> <span data-ttu-id="09224-120">Aşağı açılır menüler yerel olarak yedekli & coğrafi olarak yedekli depolama hesapları ve bulut Kabuk bölgeniz için filtrelenir.</span><span class="sxs-lookup"><span data-stu-id="09224-120">The drop-down menus are filtered for your Cloud Shell region and for local-redundant & geo-redundant storage accounts.</span></span>

![Kaynak grubu ayarı](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a><span data-ttu-id="09224-122">Bir Azure kaynak İlkesi ile kaynak oluşturma kısıtla</span><span class="sxs-lookup"><span data-stu-id="09224-122">Restrict resource creation with an Azure resource policy</span></span>
<span data-ttu-id="09224-123">Bulut Kabuğu'nda oluşturduğunuz depolama hesapları ile etiketlenmiş `ms-resource-usage:azure-cloud-shell`.</span><span class="sxs-lookup"><span data-stu-id="09224-123">Storage accounts that you create in Cloud Shell are tagged with `ms-resource-usage:azure-cloud-shell`.</span></span> <span data-ttu-id="09224-124">Bulut Kabuğu'nda depolama hesapları oluşturma kullanıcıların engellemek istiyorsanız oluşturma bir [etiketleri için Azure kaynak İlkesi](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) bu belirli etiketi tarafından tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="09224-124">If you want to disallow users from creating storage accounts in Cloud Shell, create an [Azure resource policy for tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) that are triggered by this specific tag.</span></span>

## <a name="how-cloud-shell-works"></a><span data-ttu-id="09224-125">Bulut Kabuk nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="09224-125">How Cloud Shell works</span></span>
<span data-ttu-id="09224-126">Bulut kabuk dosyalar aşağıdaki yöntemlerin her ikisi de ile devam eder:</span><span class="sxs-lookup"><span data-stu-id="09224-126">Cloud Shell persists files through both of the following methods:</span></span>
* <span data-ttu-id="09224-127">Bir disk görüntüsünü oluşturma, `$Home` dizini içindeki tüm içeriği kalıcı hale getirmek için dizin.</span><span class="sxs-lookup"><span data-stu-id="09224-127">Creating a disk image of your `$Home` directory to persist all contents within the directory.</span></span> <span data-ttu-id="09224-128">Disk görüntüsü, belirtilen dosya paylaşımı olarak kaydedilir `acc_<User>.img` adresindeki `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, ve değişiklikleri otomatik olarak eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="09224-128">The disk image is saved in your specified file share as `acc_<User>.img` at `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, and it automatically syncs changes.</span></span>

* <span data-ttu-id="09224-129">Belirtilen dosya paylaşımı olarak takma `clouddrive` içinde `$Home` doğrudan dosya paylaşımı etkileşim için dizin.</span><span class="sxs-lookup"><span data-stu-id="09224-129">Mounting your specified file share as `clouddrive` in your `$Home` directory for direct file share interaction.</span></span> <span data-ttu-id="09224-130">`/Home/<User>/clouddrive`eşlenmiş `fileshare.storage.windows.net/fileshare`.</span><span class="sxs-lookup"><span data-stu-id="09224-130">`/Home/<User>/clouddrive` is mapped to `fileshare.storage.windows.net/fileshare`.</span></span>
 
> [!NOTE]
> <span data-ttu-id="09224-131">Tüm dosyaları, `$Home` SSH anahtarları gibi dizini, bağlı dosya paylaşımında depolanan, kullanıcı disk görüntüsü kaldı.</span><span class="sxs-lookup"><span data-stu-id="09224-131">All files in your `$Home` directory, such as SSH keys, are persisted in your user disk image, which is stored in your mounted file share.</span></span> <span data-ttu-id="09224-132">Bilgileri kalıcı sırasında en iyi yöntemleri uygulamak, `$Home` dizin ve bağlı dosya paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="09224-132">Apply best practices when you persist information in your `$Home` directory and mounted file share.</span></span>

## <a name="use-the-clouddrive-command"></a><span data-ttu-id="09224-133">Kullanım `clouddrive` komutu</span><span class="sxs-lookup"><span data-stu-id="09224-133">Use the `clouddrive` command</span></span>
<span data-ttu-id="09224-134">Bulut kabuğunda denilen bir komut çalıştırabilirsiniz `clouddrive`, bağlı dosya paylaşımı için bulut Kabuk el ile güncelleştirmeniz sağlar.</span><span class="sxs-lookup"><span data-stu-id="09224-134">With Cloud Shell, you can run a command called `clouddrive`, which enables you to manually update the file share that's mounted to Cloud Shell.</span></span>
<span data-ttu-id="09224-135">!["Clouddrive" komutunu çalıştırarak](media/clouddrive-h.png)</span><span class="sxs-lookup"><span data-stu-id="09224-135">![Running the "clouddrive" command](media/clouddrive-h.png)</span></span>

## <a name="mount-a-new-clouddrive"></a><span data-ttu-id="09224-136">Yeni bir bağlama`clouddrive`</span><span class="sxs-lookup"><span data-stu-id="09224-136">Mount a new `clouddrive`</span></span>

### <a name="prerequisites-for-manual-mounting"></a><span data-ttu-id="09224-137">El ile bağlama için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="09224-137">Prerequisites for manual mounting</span></span>
<span data-ttu-id="09224-138">Kullanarak bulut kabuğu ile ilişkili dosya paylaşımı güncelleştirebilirsiniz `clouddrive mount` komutu.</span><span class="sxs-lookup"><span data-stu-id="09224-138">You can update the file share that's associated with Cloud Shell by using the `clouddrive mount` command.</span></span>

<span data-ttu-id="09224-139">Varolan bir dosya paylaşımını bağlama depolama hesapları olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="09224-139">If you mount an existing file share, the storage accounts must be:</span></span>
* <span data-ttu-id="09224-140">Yerel olarak yedekli depolama veya coğrafi olarak yedekli depolama dosya paylaşımları desteği.</span><span class="sxs-lookup"><span data-stu-id="09224-140">Locally-redundant storage or geo-redundant storage to support file shares.</span></span>
* <span data-ttu-id="09224-141">Atanan bölgenizde bulunur.</span><span class="sxs-lookup"><span data-stu-id="09224-141">Located in your assigned region.</span></span> <span data-ttu-id="09224-142">Onboarding olduğunda, kaynak grubu adı atandığınız bölge listelenen `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="09224-142">When you are onboarding, the region you are assigned to is listed in the resource group name `cloud-shell-storage-<region>`.</span></span>

### <a name="supported-storage-regions"></a><span data-ttu-id="09224-143">Desteklenen depolama bölgeleri</span><span class="sxs-lookup"><span data-stu-id="09224-143">Supported storage regions</span></span>
<span data-ttu-id="09224-144">Azure dosyaları kendilerine bağlanması bulut Kabuk makine ile aynı bölgede bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="09224-144">The Azure files must reside in the same region as the Cloud Shell machine that you're mounting them to.</span></span> <span data-ttu-id="09224-145">Bulut Kabuk kümeleri şu anda aşağıdaki bölgelerde mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="09224-145">Cloud Shell clusters currently exist in the following regions:</span></span>
|<span data-ttu-id="09224-146">Alan</span><span class="sxs-lookup"><span data-stu-id="09224-146">Area</span></span>|<span data-ttu-id="09224-147">Bölge</span><span class="sxs-lookup"><span data-stu-id="09224-147">Region</span></span>|
|---|---|
|<span data-ttu-id="09224-148">Kuzey ve Güney Amerika</span><span class="sxs-lookup"><span data-stu-id="09224-148">Americas</span></span>|<span data-ttu-id="09224-149">Doğu ABD, Orta Güney ABD, Batı ABD</span><span class="sxs-lookup"><span data-stu-id="09224-149">East US, South Central US, West US</span></span>|
|<span data-ttu-id="09224-150">Avrupa</span><span class="sxs-lookup"><span data-stu-id="09224-150">Europe</span></span>|<span data-ttu-id="09224-151">Kuzey Avrupa, Batı Avrupa</span><span class="sxs-lookup"><span data-stu-id="09224-151">North Europe, West Europe</span></span>|
|<span data-ttu-id="09224-152">Asya Pasifik</span><span class="sxs-lookup"><span data-stu-id="09224-152">Asia Pacific</span></span>|<span data-ttu-id="09224-153">Hindistan Orta, Güneydoğu Asya</span><span class="sxs-lookup"><span data-stu-id="09224-153">India Central, Southeast Asia</span></span>|

### <a name="the-clouddrive-mount-command"></a><span data-ttu-id="09224-154">`clouddrive mount` Komutu</span><span class="sxs-lookup"><span data-stu-id="09224-154">The `clouddrive mount` command</span></span>

> [!NOTE]
> <span data-ttu-id="09224-155">Yeni bir dosya paylaşımı takma varsa, yeni bir kullanıcı görüntüsü için oluşturulur, `$Home` dizin, çünkü, önceki `$Home` görüntü önceki dosya paylaşımındaki tutulur.</span><span class="sxs-lookup"><span data-stu-id="09224-155">If you're mounting a new file share, a new user image is created for your `$Home` directory, because your previous `$Home` image is kept in the previous file share.</span></span>

<span data-ttu-id="09224-156">Çalıştırma `clouddrive mount` komutunu aşağıdaki parametrelerle:</span><span class="sxs-lookup"><span data-stu-id="09224-156">Run the `clouddrive mount` command with the following parameters:</span></span>

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

<span data-ttu-id="09224-157">Daha fazla ayrıntı görüntülemek için çalıştırın `clouddrive mount -h`, aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="09224-157">To view more details, run `clouddrive mount -h`, as shown here:</span></span>

![Çalışan ' clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a><span data-ttu-id="09224-159">Çıkarın`clouddrive`</span><span class="sxs-lookup"><span data-stu-id="09224-159">Unmount `clouddrive`</span></span>
<span data-ttu-id="09224-160">Bulut Kabuk herhangi bir anda takılı bir dosya paylaşımı çıkarın.</span><span class="sxs-lookup"><span data-stu-id="09224-160">You can unmount a file share that's mounted to Cloud Shell at any time.</span></span> <span data-ttu-id="09224-161">Dosya paylaşımınızı kaldırılan olduktan sonra sonraki oturumunuz önce yeni bir dosya paylaşımını bağlama istenir.</span><span class="sxs-lookup"><span data-stu-id="09224-161">Once your file share is unmounted, you will be prompted to mount a new file share prior to your next session.</span></span>

<span data-ttu-id="09224-162">Bulut Kabuğu'ndan bir dosya paylaşımını kaldırmak için:</span><span class="sxs-lookup"><span data-stu-id="09224-162">To remove a file share from Cloud Shell:</span></span>
1. <span data-ttu-id="09224-163">`clouddrive unmount` öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="09224-163">Run `clouddrive unmount`.</span></span>
2. <span data-ttu-id="09224-164">Onayla ve istemleri onaylayın.</span><span class="sxs-lookup"><span data-stu-id="09224-164">Acknowledge and confirm the prompts.</span></span>

<span data-ttu-id="09224-165">Dosya paylaşımınızı el ile silmediğiniz sürece var olmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="09224-165">Your file share will continue to exist unless you delete it manually.</span></span> <span data-ttu-id="09224-166">Bulut Kabuk, artık bu dosya paylaşımı için sonraki oturumlarda arar.</span><span class="sxs-lookup"><span data-stu-id="09224-166">Cloud Shell will no longer search for this file share on subsequent sessions.</span></span>

<span data-ttu-id="09224-167">Daha fazla ayrıntı görüntülemek için çalıştırın `clouddrive unmount -h`, aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="09224-167">To view more details, run `clouddrive unmount -h`, as shown here:</span></span>

![Çalışan ' clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> <span data-ttu-id="09224-169">Bu komutu çalıştıran herhangi bir kaynağa silmez.</span><span class="sxs-lookup"><span data-stu-id="09224-169">Running this command will not delete any resources.</span></span> <span data-ttu-id="09224-170">El ile bir kaynak grubu, depolama hesabı veya Bulut Kabuk eşlenmiş dosya paylaşımı kalıcı olarak silindiğinde, `$Home` directory görüntü ve herhangi bir dosya paylaşımı dosyalarında.</span><span class="sxs-lookup"><span data-stu-id="09224-170">Manually deleting a resource group, storage account, or file share that is mapped to Cloud Shell will permanently delete your `$Home` directory image and any other files in your file share.</span></span> <span data-ttu-id="09224-171">Bu eylem geri alınamaz.</span><span class="sxs-lookup"><span data-stu-id="09224-171">This action cannot be undone.</span></span>

## <a name="list-clouddrive-file-shares"></a><span data-ttu-id="09224-172">Liste `clouddrive` dosya paylaşımları</span><span class="sxs-lookup"><span data-stu-id="09224-172">List `clouddrive` file shares</span></span>
<span data-ttu-id="09224-173">Hangi dosya paylaşımı olarak takılı bulmak için `clouddrive`, aşağıdaki komutu çalıştırarak `df` komutu.</span><span class="sxs-lookup"><span data-stu-id="09224-173">To discover which file share is mounted as `clouddrive`, run the following `df` command.</span></span> 

<span data-ttu-id="09224-174">URL'de, depolama hesabı adı ve dosya paylaşımı clouddrive dosya yolu gösterir.</span><span class="sxs-lookup"><span data-stu-id="09224-174">The file path to clouddrive shows your storage account name and file share in the URL.</span></span> <span data-ttu-id="09224-175">Örneğin, `//storageaccountname.file.core.windows.net/filesharename`</span><span class="sxs-lookup"><span data-stu-id="09224-175">For example, `//storageaccountname.file.core.windows.net/filesharename`</span></span>

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

## <a name="transfer-local-files-to-cloud-shell"></a><span data-ttu-id="09224-176">Bulut kabuğu için yerel dosya aktarımı</span><span class="sxs-lookup"><span data-stu-id="09224-176">Transfer local files to Cloud Shell</span></span>
<span data-ttu-id="09224-177">`clouddrive` Dizin eşitlemeler Azure portal depolama dikey ile.</span><span class="sxs-lookup"><span data-stu-id="09224-177">The `clouddrive` directory syncs with the Azure portal storage blade.</span></span> <span data-ttu-id="09224-178">Bu dikey veya dosya paylaşımından yerel dosyalar aktarmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="09224-178">Use this blade to transfer local files to or from your file share.</span></span> <span data-ttu-id="09224-179">Dikey yenilediğinizde bulut Kabuk içinde dosyalar dosya depolama GUI yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="09224-179">Updating files from within Cloud Shell is reflected in the file storage GUI when you refresh the blade.</span></span>

### <a name="download-files"></a><span data-ttu-id="09224-180">Dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="09224-180">Download files</span></span>

![Yerel dosya listesi](media/download.png)
1. <span data-ttu-id="09224-182">Azure portalında bağlı dosya paylaşımına gidin.</span><span class="sxs-lookup"><span data-stu-id="09224-182">In the Azure portal, go to the mounted file share.</span></span>
2. <span data-ttu-id="09224-183">Hedef dosya seçin.</span><span class="sxs-lookup"><span data-stu-id="09224-183">Select the target file.</span></span>
3. <span data-ttu-id="09224-184">Seçin **karşıdan** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="09224-184">Select the **Download** button.</span></span>

### <a name="upload-files"></a><span data-ttu-id="09224-185">Dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="09224-185">Upload files</span></span>

![Karşıya yüklenecek yerel dosyaları](media/upload.png)
1. <span data-ttu-id="09224-187">Bağlı dosya paylaşımına gidin.</span><span class="sxs-lookup"><span data-stu-id="09224-187">Go to your mounted file share.</span></span>
2. <span data-ttu-id="09224-188">Seçin **karşıya** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="09224-188">Select the **Upload** button.</span></span>
3. <span data-ttu-id="09224-189">Dosya veya karşıya yüklemek istediğiniz dosyaları seçin.</span><span class="sxs-lookup"><span data-stu-id="09224-189">Select the file or files that you want to upload.</span></span>
4. <span data-ttu-id="09224-190">Karşıya yükleme onaylayın.</span><span class="sxs-lookup"><span data-stu-id="09224-190">Confirm the upload.</span></span>

<span data-ttu-id="09224-191">İçinde erişilebilir olan dosyaların görmelisiniz, `clouddrive` bulut Kabuğu'nda dizin.</span><span class="sxs-lookup"><span data-stu-id="09224-191">You should now see the files that are accessible in your `clouddrive` directory in Cloud Shell.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09224-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="09224-192">Next steps</span></span>
[<span data-ttu-id="09224-193">Bulut Kabuk hızlı başlangıç</span><span class="sxs-lookup"><span data-stu-id="09224-193">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="09224-194">
[Azure File storage hakkında bilgi edinin](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span><span class="sxs-lookup"><span data-stu-id="09224-194">
[Learn about Azure File storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span></span> <br><span data-ttu-id="09224-195">
[Depolama etiketler hakkında bilgi edinin](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span><span class="sxs-lookup"><span data-stu-id="09224-195">
[Learn about storage tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span></span> <br>
