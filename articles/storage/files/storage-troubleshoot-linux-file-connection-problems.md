---
title: "Linux Azure File storage sorunlarını giderme | Microsoft Docs"
description: "Linux Azure File storage sorunlarını giderme"
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: genli
ms.openlocfilehash: 0cab2e3540afdbdc64cb77fca4b9219c77258166
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a><span data-ttu-id="2618a-103">Linux Azure File storage sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="2618a-103">Troubleshoot Azure File storage problems in Linux</span></span>

<span data-ttu-id="2618a-104">Bu makalede, Linux istemcilerden bağlandığınızda, Microsoft Azure dosya depolama alanına ilgili genel sorunları listeler.</span><span class="sxs-lookup"><span data-stu-id="2618a-104">This article lists common problems that are related to Microsoft Azure File storage when you connect from Linux clients.</span></span> <span data-ttu-id="2618a-105">Ayrıca olası nedenleri ve çözümlemeleri için bu sorunları sağlar.</span><span class="sxs-lookup"><span data-stu-id="2618a-105">It also provides possible causes and resolutions for these problems.</span></span>

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-to-open-a-file"></a><span data-ttu-id="2618a-106">"[izni reddedildi] Disk kotası aşıldı" bir dosyayı açmaya çalıştığınızda</span><span class="sxs-lookup"><span data-stu-id="2618a-106">"[permission denied] Disk quota exceeded" when you try to open a file</span></span>

<span data-ttu-id="2618a-107">Linux aşağıdakine benzer bir hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="2618a-107">In Linux, you receive an error message that resembles the following:</span></span>

<span data-ttu-id="2618a-108">**<filename>[izni reddedildi] Disk kotası aşıldı**</span><span class="sxs-lookup"><span data-stu-id="2618a-108">**<filename> [permission denied] Disk quota exceeded**</span></span>

### <a name="cause"></a><span data-ttu-id="2618a-109">Nedeni</span><span class="sxs-lookup"><span data-stu-id="2618a-109">Cause</span></span>

<span data-ttu-id="2618a-110">Bir dosya için izin verilen eşzamanlı açık tanıtıcıların üst sınırına ulaştınız.</span><span class="sxs-lookup"><span data-stu-id="2618a-110">You have reached the upper limit of concurrent open handles that are allowed for a file.</span></span>

### <a name="solution"></a><span data-ttu-id="2618a-111">Çözüm</span><span class="sxs-lookup"><span data-stu-id="2618a-111">Solution</span></span>

<span data-ttu-id="2618a-112">Bazı tanıtıcıları kapatarak eşzamanlı açık tanıtıcı sayısını azaltın ve işlemi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="2618a-112">Reduce the number of concurrent open handles by closing some handles, and then retry the operation.</span></span> <span data-ttu-id="2618a-113">Daha fazla bilgi için bkz: [Microsoft Azure Storage performans ve ölçeklenebilirlik Yapılacaklar listesi](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2618a-113">For more information, see [Microsoft Azure Storage performance and scalability checklist](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-file-storage-in-linux"></a><span data-ttu-id="2618a-114">Yavaş dosya Linux Azure File storage gelen ve giden kopyalama</span><span class="sxs-lookup"><span data-stu-id="2618a-114">Slow file copying to and from Azure File storage in Linux</span></span>

-   <span data-ttu-id="2618a-115">Belirli bir en düşük g/ç boyutu gereksinim yoksa, en iyi performans için g/ç boyutu 1 MB kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="2618a-115">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as the I/O size for optimal performance.</span></span>
-   <span data-ttu-id="2618a-116">Son yazma işlemlerini kullanarak genişletme dosya boyutunu bildiğiniz ve dosyada unwritten bir kuyruk sıfır içerdiğinde yazılımınızı uyumluluk sorunları yaşıyorsanız değil, önceden bir genişletme yazma her yazma yapmak yerine dosya boyutunu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2618a-116">If you know the final size of a file that you are extending by using writes, and your software doesn’t experience compatibility problems when an unwritten tail on the file contains zeros, then set the file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="2618a-117">Sağ copy yöntemini kullanın:</span><span class="sxs-lookup"><span data-stu-id="2618a-117">Use the right copy method:</span></span>
    -   <span data-ttu-id="2618a-118">Kullanım [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) iki dosya paylaşımları arasında herhangi bir aktarım için.</span><span class="sxs-lookup"><span data-stu-id="2618a-118">Use [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="2618a-119">Kullanım [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) bir şirket içi bilgisayar dosya paylaşımlarına arasında.</span><span class="sxs-lookup"><span data-stu-id="2618a-119">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a><span data-ttu-id="2618a-120">"Error(112) bağlayın: ana bilgisayar kapalı olduğu" yeniden bağlanma zaman aşımı nedeniyle</span><span class="sxs-lookup"><span data-stu-id="2618a-120">"Mount error(112): Host is down" because of a reconnection time-out</span></span>

<span data-ttu-id="2618a-121">"112" bağlama hata istemci uzun bir süredir boşta Linux istemcide oluşur.</span><span class="sxs-lookup"><span data-stu-id="2618a-121">A "112" mount error occurs on the Linux client when the client has been idle for a long time.</span></span> <span data-ttu-id="2618a-122">Genişletilmiş boşta kalma süresi sonra istemci bağlantısını keser ve bağlantı zaman aşımına uğruyor.</span><span class="sxs-lookup"><span data-stu-id="2618a-122">After extended idle time, the client disconnects and the connection times out.</span></span>  

### <a name="cause"></a><span data-ttu-id="2618a-123">Nedeni</span><span class="sxs-lookup"><span data-stu-id="2618a-123">Cause</span></span>

<span data-ttu-id="2618a-124">Bağlantı aşağıdaki nedenlerle boşta olabilir:</span><span class="sxs-lookup"><span data-stu-id="2618a-124">The connection can be idle for the following reasons:</span></span>

-   <span data-ttu-id="2618a-125">Varsayılan "yumuşak" Bağlama seçeneği kullanıldığında bir TCP bağlantısı sunucuya yeniden oluşturmayı engelle ağ iletişim hatası</span><span class="sxs-lookup"><span data-stu-id="2618a-125">Network communication failures that prevent re-establishing a TCP connection to the server when the default “soft” mount option is used</span></span>
-   <span data-ttu-id="2618a-126">Eski tekrar içinde mevcut olmayan son yeniden bağlanma düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="2618a-126">Recent reconnection fixes that are not present in older kernels</span></span>

### <a name="solution"></a><span data-ttu-id="2618a-127">Çözüm</span><span class="sxs-lookup"><span data-stu-id="2618a-127">Solution</span></span>

<span data-ttu-id="2618a-128">Bu yeniden bağlanma sorunu Linux çekirdek şimdi aşağıdaki değişiklikleri bir parçası olarak sabit:</span><span class="sxs-lookup"><span data-stu-id="2618a-128">This reconnection problem in the Linux kernel is now fixed as part of the following changes:</span></span>

- [<span data-ttu-id="2618a-129">Düzeltme yeniden smb3 oturum değil erteleme soket uzun yeniden sonra yeniden</span><span class="sxs-lookup"><span data-stu-id="2618a-129">Fix reconnect to not defer smb3 session reconnect long after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [<span data-ttu-id="2618a-130">Yuva hemen yeniden sonra echo hizmeti çağırın</span><span class="sxs-lookup"><span data-stu-id="2618a-130">Call echo service immediately after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [<span data-ttu-id="2618a-131">CIFS: yeniden bağlanma sırasında olası Bellek Bozulması Düzelt</span><span class="sxs-lookup"><span data-stu-id="2618a-131">CIFS: Fix a possible memory corruption during reconnect</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [<span data-ttu-id="2618a-132">CIFS: bir olası çift mutex (çekirdek v4.9 ve üzeri) yeniden bağlanma sırasında kilitleme Düzelt</span><span class="sxs-lookup"><span data-stu-id="2618a-132">CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later)</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

<span data-ttu-id="2618a-133">Ancak, bu değişiklikleri henüz tüm Linux dağıtımları için bağlantı noktası kurulmuş değil.</span><span class="sxs-lookup"><span data-stu-id="2618a-133">However, these changes might not be ported yet to all the Linux distributions.</span></span> <span data-ttu-id="2618a-134">Bu düzeltme ve diğer yeniden bağlanmayı düzeltmeleri aşağıdaki popüler Linux tekrar yapılır: 4.4.40, 4.8.16 ve 4.9.1.</span><span class="sxs-lookup"><span data-stu-id="2618a-134">This fix and other reconnection fixes are made in the following popular Linux kernels: 4.4.40, 4.8.16, and 4.9.1.</span></span> <span data-ttu-id="2618a-135">Bu önerilen çekirdek sürümlerinden birine yükselterek bu düzeltmenin elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2618a-135">You can get this fix by upgrading to one of these recommended kernel versions.</span></span>

### <a name="workaround"></a><span data-ttu-id="2618a-136">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="2618a-136">Workaround</span></span>

<span data-ttu-id="2618a-137">Sabit bağlama belirterek bu soruna geçici çözüm bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2618a-137">You can work around this problem by specifying a hard mount.</span></span> <span data-ttu-id="2618a-138">Bu, bağlantı kurulana kadar veya açıkça kesintiye uğrarsa ve ağ zaman aşımı nedeniyle hataları önlemek için kullanılan kadar beklemek için istemci zorlar.</span><span class="sxs-lookup"><span data-stu-id="2618a-138">This forces the client to wait until a connection is established or until it’s explicitly interrupted and can be used to prevent errors because of network time-outs.</span></span> <span data-ttu-id="2618a-139">Ancak, bu geçici çözüm belirsiz bekler neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="2618a-139">However, this workaround might cause indefinite waits.</span></span> <span data-ttu-id="2618a-140">Bağlantıları gerekli olarak durdurmak hazırlıklı olun.</span><span class="sxs-lookup"><span data-stu-id="2618a-140">Be prepared to stop connections as necessary.</span></span>

<span data-ttu-id="2618a-141">En son çekirdek sürümlerine yükseltemiyorsanız her 30 saniye veya daha az yazma Azure Dosya paylaşımındaki dosya tutarak bu soruna geçici çözüm.</span><span class="sxs-lookup"><span data-stu-id="2618a-141">If you cannot upgrade to the latest kernel versions, you can work around this problem by keeping a file in the Azure file share that you write to every 30 seconds or less.</span></span> <span data-ttu-id="2618a-142">Bu dosya üzerinde oluşturulan veya değiştirilen tarih yeniden yazma işlemi gibi bir yazma işlemi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2618a-142">This must be a write operation, such as rewriting the created or modified date on the file.</span></span> <span data-ttu-id="2618a-143">Aksi takdirde, önbelleğe alınan sonuçları alabilirsiniz ve işleminizi yeniden bağlanmayı tetikleyebilir değil.</span><span class="sxs-lookup"><span data-stu-id="2618a-143">Otherwise, you might get cached results, and your operation might not trigger the reconnection.</span></span>

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a><span data-ttu-id="2618a-144">"Error(115) bağlayın: İşlem Sürüyor" olduğunda, bağlama Azure File storage SMB 3.0 kullanarak</span><span class="sxs-lookup"><span data-stu-id="2618a-144">"Mount error(115): Operation now in progress" when you mount Azure File storage by using SMB 3.0</span></span>

### <a name="cause"></a><span data-ttu-id="2618a-145">Nedeni</span><span class="sxs-lookup"><span data-stu-id="2618a-145">Cause</span></span>

<span data-ttu-id="2618a-146">Şifreleme özellikleri SMB 3. 0 ' ' ı desteklemez henüz bazı Linux dağıtımları ve bunlar için bağlama Azure nedeniyle eksik bir özellik SMB 3.0 kullanarak dosya depolama denerseniz, kullanıcılar "115" hata mesajı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2618a-146">Some Linux distributions do not yet support encryption features in SMB 3.0 and users might receive a "115" error message if they try to mount Azure File storage by using SMB 3.0 because of a missing feature.</span></span>

### <a name="solution"></a><span data-ttu-id="2618a-147">Çözüm</span><span class="sxs-lookup"><span data-stu-id="2618a-147">Solution</span></span>

<span data-ttu-id="2618a-148">Linux için SMB 3.0 şifreleme özelliği 4.11 Çekirdeği'nde sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="2618a-148">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="2618a-149">Bu özellik Azure dosya paylaşımının şirket içi veya farklı bir Azure bölgesindeki bağlama sağlar.</span><span class="sxs-lookup"><span data-stu-id="2618a-149">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="2618a-150">Yayımlama zaman bu işlevselliği Ubuntu 17.04 ve Ubuntu 16.10 backported olmuştur.</span><span class="sxs-lookup"><span data-stu-id="2618a-150">At the time of publishing, this functionality has been backported to Ubuntu 17.04 and Ubuntu 16.10.</span></span> <span data-ttu-id="2618a-151">Linux SMB istemci şifreleme desteklemiyorsa, SMB 2.1 dosya depolama hesabı ile aynı veri merkezinde olan bir Azure Linux VM'den kullanarak Azure File storage bağlayın.</span><span class="sxs-lookup"><span data-stu-id="2618a-151">If your Linux SMB client does not support encryption, mount Azure File storage by using SMB 2.1 from an Azure Linux VM that's in the same datacenter as the File storage account.</span></span>

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a><span data-ttu-id="2618a-152">Bir Azure dosya paylaşımında yavaş performans üzerinde bir Linux VM takılı</span><span class="sxs-lookup"><span data-stu-id="2618a-152">Slow performance on an Azure file share mounted on a Linux VM</span></span>

### <a name="cause"></a><span data-ttu-id="2618a-153">Nedeni</span><span class="sxs-lookup"><span data-stu-id="2618a-153">Cause</span></span>

<span data-ttu-id="2618a-154">Olası bir nedeni yavaş performans önbelleğe almayı devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="2618a-154">One possible cause of slow performance is disabled caching.</span></span>

### <a name="solution"></a><span data-ttu-id="2618a-155">Çözüm</span><span class="sxs-lookup"><span data-stu-id="2618a-155">Solution</span></span>

<span data-ttu-id="2618a-156">Önbelleğe alma devre dışı olup olmadığını denetlemek için Ara **önbellek =** girişi.</span><span class="sxs-lookup"><span data-stu-id="2618a-156">To check whether caching is disabled, look for the **cache=** entry.</span></span> 

<span data-ttu-id="2618a-157">**Önbellek = none** önbelleğe almayı devre dışı olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="2618a-157">**Cache=none** indicates that caching is disabled.</span></span>  <span data-ttu-id="2618a-158">Varsayılan bağlama komutunu kullanarak veya açıkça ekleyerek paylaşımı yeniden **önbellek strict =** seçeneği varsayılan önbelleğe alma emin olmak için bağlama komutu ya da "katı" önbelleğe alma modu etkinleştirildi.</span><span class="sxs-lookup"><span data-stu-id="2618a-158">Remount the share by using the default mount command or by explicitly adding the **cache=strict** option to the mount command to ensure that default caching or "strict" caching mode is enabled.</span></span>

<span data-ttu-id="2618a-159">Bazı senaryolarda **serverino** bağlama seçeneği neden olabilecek **ls** her dizin girişi karşı stat çalıştırılacak komutu.</span><span class="sxs-lookup"><span data-stu-id="2618a-159">In some scenarios, the **serverino** mount option can cause the **ls** command to run stat against every directory entry.</span></span> <span data-ttu-id="2618a-160">Büyük bir dizin listelerken Bu davranış performans düşüşüne neden olur.</span><span class="sxs-lookup"><span data-stu-id="2618a-160">This behavior results in performance degradation when you're listing a big directory.</span></span> <span data-ttu-id="2618a-161">Bağlama seçenekleri kontrol edebilirsiniz, **/etc/fstab** girişi:</span><span class="sxs-lookup"><span data-stu-id="2618a-161">You can check the mount options in your **/etc/fstab** entry:</span></span>

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

<span data-ttu-id="2618a-162">Ayrıca çalıştırarak doğru seçeneklerini kullanılıp kullanılmadığını kontrol edebilirsiniz **sudo bağlama | grep CIFS** komutunu ve aşağıdaki örnek çıkış gibi çıktısını denetleniyor:</span><span class="sxs-lookup"><span data-stu-id="2618a-162">You can also check whether the correct options are being used by running the  **sudo mount | grep cifs** command and checking its output, such as the following example output:</span></span>

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

<span data-ttu-id="2618a-163">Varsa **önbellek strict =** veya **serverino** seçenektir değil sunmak, çıkarın ve bağlama Azure File storage yeniden bağlama komutunu çalıştırarak [belgelerine](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2618a-163">If the **cache=strict** or **serverino** option is not present, unmount and mount Azure File storage again by running the mount command from the [documentation](../storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="2618a-164">Ardından, yeniden denetle **/etc/fstab** girişi doğru seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="2618a-164">Then, recheck that the **/etc/fstab** entry has the correct options.</span></span>

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-to-linux"></a><span data-ttu-id="2618a-165">Linux için Windows dosyaları kopyalarken'zaman damgaları kaybolduğundan</span><span class="sxs-lookup"><span data-stu-id="2618a-165">Time stamps were lost in copying files from Windows to Linux</span></span>

<span data-ttu-id="2618a-166">Linux/Unix platformlarda **cp -p** komutu başarısız olursa dosya 1 ve 2 dosyasını farklı kullanıcılar tarafından sahip olunan.</span><span class="sxs-lookup"><span data-stu-id="2618a-166">On Linux/Unix platforms, the **cp -p** command fails if file 1 and file 2 are owned by different users.</span></span>

### <a name="cause"></a><span data-ttu-id="2618a-167">Nedeni</span><span class="sxs-lookup"><span data-stu-id="2618a-167">Cause</span></span>

<span data-ttu-id="2618a-168">Force bayrağını **f** içinde COPYFILE sonuçları yürütülürken **cp -p -f** UNIX üzerinde.</span><span class="sxs-lookup"><span data-stu-id="2618a-168">The force flag **f** in COPYFILE results in executing **cp -p -f** on Unix.</span></span> <span data-ttu-id="2618a-169">Bu komut, size ait olmayan dosyanın zaman damgası korumak de başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="2618a-169">This command also fails to preserve the time stamp of the file that you don't own.</span></span>

### <a name="workaround"></a><span data-ttu-id="2618a-170">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="2618a-170">Workaround</span></span>

<span data-ttu-id="2618a-171">Depolama hesabı kullanıcı dosyaları kopyalamak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="2618a-171">Use the storage account user for copying the files:</span></span>

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a><span data-ttu-id="2618a-172">Yardım mı gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="2618a-172">Need help?</span></span> <span data-ttu-id="2618a-173">Desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="2618a-173">Contact support.</span></span>

<span data-ttu-id="2618a-174">Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) hızla çözülmüş sorununuzu almak için.</span><span class="sxs-lookup"><span data-stu-id="2618a-174">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your problem resolved quickly.</span></span>
