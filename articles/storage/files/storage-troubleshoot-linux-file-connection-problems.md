---
title: "Linux aaaTroubleshoot Azure File storage sorunlarını | Microsoft Docs"
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
ms.openlocfilehash: 4bdc3c6ed2e48f245060a03632fca9bd14d33545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a><span data-ttu-id="e98a8-103">Linux Azure File storage sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="e98a8-103">Troubleshoot Azure File storage problems in Linux</span></span>

<span data-ttu-id="e98a8-104">Bu makalede ilgili tooMicrosoft Azure File storage Linux istemcilerden bağlandığınızda olan ortak sorunlar listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="e98a8-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Linux clients.</span></span> <span data-ttu-id="e98a8-105">Ayrıca olası nedenleri ve çözümlemeleri için bu sorunları sağlar.</span><span class="sxs-lookup"><span data-stu-id="e98a8-105">It also provides possible causes and resolutions for these problems.</span></span>

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a><span data-ttu-id="e98a8-106">"[izni reddedildi] Disk kotası aşıldı" tooopen bir dosya çalıştığınızda</span><span class="sxs-lookup"><span data-stu-id="e98a8-106">"[permission denied] Disk quota exceeded" when you try tooopen a file</span></span>

<span data-ttu-id="e98a8-107">Linux hello aşağıdakine benzer bir hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="e98a8-107">In Linux, you receive an error message that resembles hello following:</span></span>

<span data-ttu-id="e98a8-108">**<filename>[izni reddedildi] Disk kotası aşıldı**</span><span class="sxs-lookup"><span data-stu-id="e98a8-108">**<filename> [permission denied] Disk quota exceeded**</span></span>

### <a name="cause"></a><span data-ttu-id="e98a8-109">Nedeni</span><span class="sxs-lookup"><span data-stu-id="e98a8-109">Cause</span></span>

<span data-ttu-id="e98a8-110">Bir dosya için izin verilen eşzamanlı açık tanıtıcıların hello üst sınırına ulaştınız.</span><span class="sxs-lookup"><span data-stu-id="e98a8-110">You have reached hello upper limit of concurrent open handles that are allowed for a file.</span></span>

### <a name="solution"></a><span data-ttu-id="e98a8-111">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e98a8-111">Solution</span></span>

<span data-ttu-id="e98a8-112">Bazı tanıtıcıları kapatarak Hello eşzamanlı açık tanıtıcı sayısını azaltın ve hello işlemi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="e98a8-112">Reduce hello number of concurrent open handles by closing some handles, and then retry hello operation.</span></span> <span data-ttu-id="e98a8-113">Daha fazla bilgi için bkz: [Microsoft Azure Storage performans ve ölçeklenebilirlik Yapılacaklar listesi](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e98a8-113">For more information, see [Microsoft Azure Storage performance and scalability checklist](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a><span data-ttu-id="e98a8-114">Yavaş dosya Linux Azure File storage tooand kopyalama</span><span class="sxs-lookup"><span data-stu-id="e98a8-114">Slow file copying tooand from Azure File storage in Linux</span></span>

-   <span data-ttu-id="e98a8-115">Belirli bir en düşük g/ç boyutu gereksinim yoksa, en iyi performans için g/ç boyutu hello gibi 1 MB kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="e98a8-115">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="e98a8-116">Merhaba son yazma işlemlerini kullanarak genişletme dosya boyutunu bildiğiniz ve hello dosyada unwritten bir kuyruk sıfır içerdiğinde yazılımınızı uyumluluk sorunları yaşıyorsanız değil, önceden bir genişletme her yazma yapmak yerine hello dosya boyutu ayarlama yazma.</span><span class="sxs-lookup"><span data-stu-id="e98a8-116">If you know hello final size of a file that you are extending by using writes, and your software doesn’t experience compatibility problems when an unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="e98a8-117">Merhaba sağ copy yöntemini kullanın:</span><span class="sxs-lookup"><span data-stu-id="e98a8-117">Use hello right copy method:</span></span>
    -   <span data-ttu-id="e98a8-118">Kullanım [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) iki dosya paylaşımları arasında herhangi bir aktarım için.</span><span class="sxs-lookup"><span data-stu-id="e98a8-118">Use [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="e98a8-119">Kullanım [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) bir şirket içi bilgisayar dosya paylaşımlarına arasında.</span><span class="sxs-lookup"><span data-stu-id="e98a8-119">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a><span data-ttu-id="e98a8-120">"Error(112) bağlayın: ana bilgisayar kapalı olduğu" yeniden bağlanma zaman aşımı nedeniyle</span><span class="sxs-lookup"><span data-stu-id="e98a8-120">"Mount error(112): Host is down" because of a reconnection time-out</span></span>

<span data-ttu-id="e98a8-121">"112" bağlama hata Hello istemci uzun bir süredir boşta hello Linux istemcide oluşur.</span><span class="sxs-lookup"><span data-stu-id="e98a8-121">A "112" mount error occurs on hello Linux client when hello client has been idle for a long time.</span></span> <span data-ttu-id="e98a8-122">Genişletilmiş boşta kalma süresi sonra hello istemci bağlantısını keser ve hello bağlantı zaman aşımına uğruyor.</span><span class="sxs-lookup"><span data-stu-id="e98a8-122">After extended idle time, hello client disconnects and hello connection times out.</span></span>  

### <a name="cause"></a><span data-ttu-id="e98a8-123">Nedeni</span><span class="sxs-lookup"><span data-stu-id="e98a8-123">Cause</span></span>

<span data-ttu-id="e98a8-124">Merhaba bağlantı nedeniyle aşağıdaki hello için boşta olabilir:</span><span class="sxs-lookup"><span data-stu-id="e98a8-124">hello connection can be idle for hello following reasons:</span></span>

-   <span data-ttu-id="e98a8-125">Merhaba varsayılan "yumuşak" Bağlama seçeneği kullanıldığında bir TCP bağlantı toohello sunucusu yeniden oluşturmayı engelle ağ iletişim hatası</span><span class="sxs-lookup"><span data-stu-id="e98a8-125">Network communication failures that prevent re-establishing a TCP connection toohello server when hello default “soft” mount option is used</span></span>
-   <span data-ttu-id="e98a8-126">Eski tekrar içinde mevcut olmayan son yeniden bağlanma düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="e98a8-126">Recent reconnection fixes that are not present in older kernels</span></span>

### <a name="solution"></a><span data-ttu-id="e98a8-127">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e98a8-127">Solution</span></span>

<span data-ttu-id="e98a8-128">Bu yeniden bağlanma sorunu hello Linux Çekirdeği'nde şimdi aşağıdaki değişiklikler hello bir parçası olarak sabit:</span><span class="sxs-lookup"><span data-stu-id="e98a8-128">This reconnection problem in hello Linux kernel is now fixed as part of hello following changes:</span></span>

- [<span data-ttu-id="e98a8-129">Düzeltme yeniden toonot smb3 oturum erteleme soket uzun yeniden sonra yeniden</span><span class="sxs-lookup"><span data-stu-id="e98a8-129">Fix reconnect toonot defer smb3 session reconnect long after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [<span data-ttu-id="e98a8-130">Yuva hemen yeniden sonra echo hizmeti çağırın</span><span class="sxs-lookup"><span data-stu-id="e98a8-130">Call echo service immediately after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [<span data-ttu-id="e98a8-131">CIFS: yeniden bağlanma sırasında olası Bellek Bozulması Düzelt</span><span class="sxs-lookup"><span data-stu-id="e98a8-131">CIFS: Fix a possible memory corruption during reconnect</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [<span data-ttu-id="e98a8-132">CIFS: bir olası çift mutex (çekirdek v4.9 ve üzeri) yeniden bağlanma sırasında kilitleme Düzelt</span><span class="sxs-lookup"><span data-stu-id="e98a8-132">CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later)</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

<span data-ttu-id="e98a8-133">Tooall hello henüz Linux dağıtımları ancak, bu değişiklikleri bağlantı noktası kurulmuş değil.</span><span class="sxs-lookup"><span data-stu-id="e98a8-133">However, these changes might not be ported yet tooall hello Linux distributions.</span></span> <span data-ttu-id="e98a8-134">Bu düzeltme ve diğer yeniden bağlanmayı düzeltmeleri popüler Linux tekrar aşağıdaki hello yapılır: 4.4.40, 4.8.16 ve 4.9.1.</span><span class="sxs-lookup"><span data-stu-id="e98a8-134">This fix and other reconnection fixes are made in hello following popular Linux kernels: 4.4.40, 4.8.16, and 4.9.1.</span></span> <span data-ttu-id="e98a8-135">Bu önerilen çekirdek sürümlerinin tooone yükselterek bu düzeltmenin elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e98a8-135">You can get this fix by upgrading tooone of these recommended kernel versions.</span></span>

### <a name="workaround"></a><span data-ttu-id="e98a8-136">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="e98a8-136">Workaround</span></span>

<span data-ttu-id="e98a8-137">Sabit bağlama belirterek bu soruna geçici çözüm bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e98a8-137">You can work around this problem by specifying a hard mount.</span></span> <span data-ttu-id="e98a8-138">Bu, bağlantı kurulana kadar veya açıkça kesintiye uğrarsa ve kullanılan tooprevent hataları ağ zaman aşımı nedeniyle olabilir kadar hello istemci toowait zorlar.</span><span class="sxs-lookup"><span data-stu-id="e98a8-138">This forces hello client toowait until a connection is established or until it’s explicitly interrupted and can be used tooprevent errors because of network time-outs.</span></span> <span data-ttu-id="e98a8-139">Ancak, bu geçici çözüm belirsiz bekler neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="e98a8-139">However, this workaround might cause indefinite waits.</span></span> <span data-ttu-id="e98a8-140">Hazırlanan toostop bağlantıları gerektiği gibi olabilir.</span><span class="sxs-lookup"><span data-stu-id="e98a8-140">Be prepared toostop connections as necessary.</span></span>

<span data-ttu-id="e98a8-141">Toohello son çekirdek sürümleri yükseltemiyorsanız 30 saniye tooevery yazma hello Azure dosya paylaşımı veya daha az bir dosya tutarak bu soruna geçici çözüm.</span><span class="sxs-lookup"><span data-stu-id="e98a8-141">If you cannot upgrade toohello latest kernel versions, you can work around this problem by keeping a file in hello Azure file share that you write tooevery 30 seconds or less.</span></span> <span data-ttu-id="e98a8-142">Merhaba yeniden yazma işlemi oluşturulan veya hello dosyada değişiklik tarihi gibi bu bir yazma işlemi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e98a8-142">This must be a write operation, such as rewriting hello created or modified date on hello file.</span></span> <span data-ttu-id="e98a8-143">Aksi takdirde, önbelleğe alınan sonuçları alabilirsiniz ve işleminizi hello yeniden bağlanmayı tetikleyebilir değil.</span><span class="sxs-lookup"><span data-stu-id="e98a8-143">Otherwise, you might get cached results, and your operation might not trigger hello reconnection.</span></span>

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a><span data-ttu-id="e98a8-144">"Error(115) bağlayın: İşlem Sürüyor" olduğunda, bağlama Azure File storage SMB 3.0 kullanarak</span><span class="sxs-lookup"><span data-stu-id="e98a8-144">"Mount error(115): Operation now in progress" when you mount Azure File storage by using SMB 3.0</span></span>

### <a name="cause"></a><span data-ttu-id="e98a8-145">Nedeni</span><span class="sxs-lookup"><span data-stu-id="e98a8-145">Cause</span></span>

<span data-ttu-id="e98a8-146">Şifreleme özellikleri SMB 3. 0 ' ' ı desteklemez henüz bazı Linux dağıtımları ve bunlar toomount Azure File storage nedeniyle eksik bir özellik SMB 3.0 kullanılarak çalışırsanız kullanıcılar "115" hata mesajı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e98a8-146">Some Linux distributions do not yet support encryption features in SMB 3.0 and users might receive a "115" error message if they try toomount Azure File storage by using SMB 3.0 because of a missing feature.</span></span>

### <a name="solution"></a><span data-ttu-id="e98a8-147">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e98a8-147">Solution</span></span>

<span data-ttu-id="e98a8-148">Linux için SMB 3.0 şifreleme özelliği 4.11 Çekirdeği'nde sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="e98a8-148">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="e98a8-149">Bu özellik Azure dosya paylaşımının şirket içi veya farklı bir Azure bölgesindeki bağlama sağlar.</span><span class="sxs-lookup"><span data-stu-id="e98a8-149">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="e98a8-150">Yayımlama Hello anda bu işlevselliği backported tooUbuntu 17.04 ve Ubuntu 16.10 olarak adlandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="e98a8-150">At hello time of publishing, this functionality has been backported tooUbuntu 17.04 and Ubuntu 16.10.</span></span> <span data-ttu-id="e98a8-151">Linux SMB istemci şifreleme desteklemiyorsa, SMB 2.1 içinde bir Azure Linux VM'den kullanarak Azure File storage bağlama dosya depolama hesabı hello gibi aynı veri merkezinde hello.</span><span class="sxs-lookup"><span data-stu-id="e98a8-151">If your Linux SMB client does not support encryption, mount Azure File storage by using SMB 2.1 from an Azure Linux VM that's in hello same datacenter as hello File storage account.</span></span>

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a><span data-ttu-id="e98a8-152">Bir Azure dosya paylaşımında yavaş performans üzerinde bir Linux VM takılı</span><span class="sxs-lookup"><span data-stu-id="e98a8-152">Slow performance on an Azure file share mounted on a Linux VM</span></span>

### <a name="cause"></a><span data-ttu-id="e98a8-153">Nedeni</span><span class="sxs-lookup"><span data-stu-id="e98a8-153">Cause</span></span>

<span data-ttu-id="e98a8-154">Olası bir nedeni yavaş performans önbelleğe almayı devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="e98a8-154">One possible cause of slow performance is disabled caching.</span></span>

### <a name="solution"></a><span data-ttu-id="e98a8-155">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e98a8-155">Solution</span></span>

<span data-ttu-id="e98a8-156">toocheck önbelleğe almayı devre dışı bırakılıp bırakılmayacağını Merhaba Ara **önbellek =** girişi.</span><span class="sxs-lookup"><span data-stu-id="e98a8-156">toocheck whether caching is disabled, look for hello **cache=** entry.</span></span> 

<span data-ttu-id="e98a8-157">**Önbellek = none** önbelleğe almayı devre dışı olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="e98a8-157">**Cache=none** indicates that caching is disabled.</span></span>  <span data-ttu-id="e98a8-158">Yeniden bağlama hello paylaşımı hello varsayılan bağlama komutunu kullanarak veya açıkça hello ekleyerek **önbellek strict =** önbelleğe alma veya "katı" önbelleğe alma modu varsayılan seçeneği toohello bağlama komutu tooensure etkindir.</span><span class="sxs-lookup"><span data-stu-id="e98a8-158">Remount hello share by using hello default mount command or by explicitly adding hello **cache=strict** option toohello mount command tooensure that default caching or "strict" caching mode is enabled.</span></span>

<span data-ttu-id="e98a8-159">Bazı senaryolarda hello **serverino** bağlama seçeneği hello neden **ls** komutu toorun stat her dizin girişi karşı.</span><span class="sxs-lookup"><span data-stu-id="e98a8-159">In some scenarios, hello **serverino** mount option can cause hello **ls** command toorun stat against every directory entry.</span></span> <span data-ttu-id="e98a8-160">Büyük bir dizin listelerken Bu davranış performans düşüşüne neden olur.</span><span class="sxs-lookup"><span data-stu-id="e98a8-160">This behavior results in performance degradation when you're listing a big directory.</span></span> <span data-ttu-id="e98a8-161">Merhaba takma seçeneklerini kontrol edebilirsiniz, **/etc/fstab** girişi:</span><span class="sxs-lookup"><span data-stu-id="e98a8-161">You can check hello mount options in your **/etc/fstab** entry:</span></span>

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

<span data-ttu-id="e98a8-162">Ayrıca hello çalıştırarak hello doğru seçeneklerini kullanılıp kullanılmadığını kontrol edebilirsiniz **sudo bağlama | grep CIFS** komut ve örnek çıktı aşağıdaki hello gibi çıktısını denetleniyor:</span><span class="sxs-lookup"><span data-stu-id="e98a8-162">You can also check whether hello correct options are being used by running hello  **sudo mount | grep cifs** command and checking its output, such as hello following example output:</span></span>

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

<span data-ttu-id="e98a8-163">Merhaba, **önbellek strict =** veya **serverino** seçenektir değil sunmak, çıkarın ve bağlama Azure File storage yeniden hello hello bağlama komutu çalıştırarak [belgelerine](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e98a8-163">If hello **cache=strict** or **serverino** option is not present, unmount and mount Azure File storage again by running hello mount command from hello [documentation](../storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="e98a8-164">Ardından, o hello yeniden denetle **/etc/fstab** girişi hello doğru seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="e98a8-164">Then, recheck that hello **/etc/fstab** entry has hello correct options.</span></span>

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a><span data-ttu-id="e98a8-165">Windows tooLinux dosyaları kopyalarken'zaman damgaları kaybolduğundan</span><span class="sxs-lookup"><span data-stu-id="e98a8-165">Time stamps were lost in copying files from Windows tooLinux</span></span>

<span data-ttu-id="e98a8-166">Linux/Unix platformlarda hello **cp -p** komutu başarısız olursa dosya 1 ve 2 dosyasını farklı kullanıcılar tarafından sahip olunan.</span><span class="sxs-lookup"><span data-stu-id="e98a8-166">On Linux/Unix platforms, hello **cp -p** command fails if file 1 and file 2 are owned by different users.</span></span>

### <a name="cause"></a><span data-ttu-id="e98a8-167">Nedeni</span><span class="sxs-lookup"><span data-stu-id="e98a8-167">Cause</span></span>

<span data-ttu-id="e98a8-168">Force bayrağını hello **f** içinde COPYFILE sonuçları yürütülürken **cp -p -f** UNIX üzerinde.</span><span class="sxs-lookup"><span data-stu-id="e98a8-168">hello force flag **f** in COPYFILE results in executing **cp -p -f** on Unix.</span></span> <span data-ttu-id="e98a8-169">Bu komut ayrıca toopreserve hello zaman damgası sahip olmadığınız hello dosyasının başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="e98a8-169">This command also fails toopreserve hello time stamp of hello file that you don't own.</span></span>

### <a name="workaround"></a><span data-ttu-id="e98a8-170">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="e98a8-170">Workaround</span></span>

<span data-ttu-id="e98a8-171">Merhaba depolama hesabı kullanıcı hello dosyaları kopyalamak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="e98a8-171">Use hello storage account user for copying hello files:</span></span>

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a><span data-ttu-id="e98a8-172">Yardım mı gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="e98a8-172">Need help?</span></span> <span data-ttu-id="e98a8-173">Desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="e98a8-173">Contact support.</span></span>

<span data-ttu-id="e98a8-174">Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) , sorunun giderilmiş hızla tooget.</span><span class="sxs-lookup"><span data-stu-id="e98a8-174">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
