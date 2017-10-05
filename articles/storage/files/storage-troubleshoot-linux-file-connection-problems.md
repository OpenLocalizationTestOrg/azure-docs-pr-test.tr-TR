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
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a>Linux Azure File storage sorunlarını giderme

Bu makalede, Linux istemcilerden bağlandığınızda, Microsoft Azure dosya depolama alanına ilgili genel sorunları listeler. Ayrıca olası nedenleri ve çözümlemeleri için bu sorunları sağlar.

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-to-open-a-file"></a>"[izni reddedildi] Disk kotası aşıldı" bir dosyayı açmaya çalıştığınızda

Linux aşağıdakine benzer bir hata iletisini alıyorsunuz:

**<filename>[izni reddedildi] Disk kotası aşıldı**

### <a name="cause"></a>Nedeni

Bir dosya için izin verilen eşzamanlı açık tanıtıcıların üst sınırına ulaştınız.

### <a name="solution"></a>Çözüm

Bazı tanıtıcıları kapatarak eşzamanlı açık tanıtıcı sayısını azaltın ve işlemi yeniden deneyin. Daha fazla bilgi için bkz: [Microsoft Azure Storage performans ve ölçeklenebilirlik Yapılacaklar listesi](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-file-storage-in-linux"></a>Yavaş dosya Linux Azure File storage gelen ve giden kopyalama

-   Belirli bir en düşük g/ç boyutu gereksinim yoksa, en iyi performans için g/ç boyutu 1 MB kullanmanızı öneririz.
-   Son yazma işlemlerini kullanarak genişletme dosya boyutunu bildiğiniz ve dosyada unwritten bir kuyruk sıfır içerdiğinde yazılımınızı uyumluluk sorunları yaşıyorsanız değil, önceden bir genişletme yazma her yazma yapmak yerine dosya boyutunu ayarlayın.
-   Sağ copy yöntemini kullanın:
    -   Kullanım [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) iki dosya paylaşımları arasında herhangi bir aktarım için.
    -   Kullanım [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) bir şirket içi bilgisayar dosya paylaşımlarına arasında.

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a>"Error(112) bağlayın: ana bilgisayar kapalı olduğu" yeniden bağlanma zaman aşımı nedeniyle

"112" bağlama hata istemci uzun bir süredir boşta Linux istemcide oluşur. Genişletilmiş boşta kalma süresi sonra istemci bağlantısını keser ve bağlantı zaman aşımına uğruyor.  

### <a name="cause"></a>Nedeni

Bağlantı aşağıdaki nedenlerle boşta olabilir:

-   Varsayılan "yumuşak" Bağlama seçeneği kullanıldığında bir TCP bağlantısı sunucuya yeniden oluşturmayı engelle ağ iletişim hatası
-   Eski tekrar içinde mevcut olmayan son yeniden bağlanma düzeltmeleri

### <a name="solution"></a>Çözüm

Bu yeniden bağlanma sorunu Linux çekirdek şimdi aşağıdaki değişiklikleri bir parçası olarak sabit:

- [Düzeltme yeniden smb3 oturum değil erteleme soket uzun yeniden sonra yeniden](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [Yuva hemen yeniden sonra echo hizmeti çağırın](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [CIFS: yeniden bağlanma sırasında olası Bellek Bozulması Düzelt](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [CIFS: bir olası çift mutex (çekirdek v4.9 ve üzeri) yeniden bağlanma sırasında kilitleme Düzelt](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

Ancak, bu değişiklikleri henüz tüm Linux dağıtımları için bağlantı noktası kurulmuş değil. Bu düzeltme ve diğer yeniden bağlanmayı düzeltmeleri aşağıdaki popüler Linux tekrar yapılır: 4.4.40, 4.8.16 ve 4.9.1. Bu önerilen çekirdek sürümlerinden birine yükselterek bu düzeltmenin elde edebilirsiniz.

### <a name="workaround"></a>Geçici çözüm

Sabit bağlama belirterek bu soruna geçici çözüm bulabilirsiniz. Bu, bağlantı kurulana kadar veya açıkça kesintiye uğrarsa ve ağ zaman aşımı nedeniyle hataları önlemek için kullanılan kadar beklemek için istemci zorlar. Ancak, bu geçici çözüm belirsiz bekler neden olabilir. Bağlantıları gerekli olarak durdurmak hazırlıklı olun.

En son çekirdek sürümlerine yükseltemiyorsanız her 30 saniye veya daha az yazma Azure Dosya paylaşımındaki dosya tutarak bu soruna geçici çözüm. Bu dosya üzerinde oluşturulan veya değiştirilen tarih yeniden yazma işlemi gibi bir yazma işlemi olmalıdır. Aksi takdirde, önbelleğe alınan sonuçları alabilirsiniz ve işleminizi yeniden bağlanmayı tetikleyebilir değil.

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a>"Error(115) bağlayın: İşlem Sürüyor" olduğunda, bağlama Azure File storage SMB 3.0 kullanarak

### <a name="cause"></a>Nedeni

Şifreleme özellikleri SMB 3. 0 ' ' ı desteklemez henüz bazı Linux dağıtımları ve bunlar için bağlama Azure nedeniyle eksik bir özellik SMB 3.0 kullanarak dosya depolama denerseniz, kullanıcılar "115" hata mesajı alabilirsiniz.

### <a name="solution"></a>Çözüm

Linux için SMB 3.0 şifreleme özelliği 4.11 Çekirdeği'nde sunulmuştur. Bu özellik Azure dosya paylaşımının şirket içi veya farklı bir Azure bölgesindeki bağlama sağlar. Yayımlama zaman bu işlevselliği Ubuntu 17.04 ve Ubuntu 16.10 backported olmuştur. Linux SMB istemci şifreleme desteklemiyorsa, SMB 2.1 dosya depolama hesabı ile aynı veri merkezinde olan bir Azure Linux VM'den kullanarak Azure File storage bağlayın.

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a>Bir Azure dosya paylaşımında yavaş performans üzerinde bir Linux VM takılı

### <a name="cause"></a>Nedeni

Olası bir nedeni yavaş performans önbelleğe almayı devre dışı bırakılır.

### <a name="solution"></a>Çözüm

Önbelleğe alma devre dışı olup olmadığını denetlemek için Ara **önbellek =** girişi. 

**Önbellek = none** önbelleğe almayı devre dışı olduğunu belirtir.  Varsayılan bağlama komutunu kullanarak veya açıkça ekleyerek paylaşımı yeniden **önbellek strict =** seçeneği varsayılan önbelleğe alma emin olmak için bağlama komutu ya da "katı" önbelleğe alma modu etkinleştirildi.

Bazı senaryolarda **serverino** bağlama seçeneği neden olabilecek **ls** her dizin girişi karşı stat çalıştırılacak komutu. Büyük bir dizin listelerken Bu davranış performans düşüşüne neden olur. Bağlama seçenekleri kontrol edebilirsiniz, **/etc/fstab** girişi:

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

Ayrıca çalıştırarak doğru seçeneklerini kullanılıp kullanılmadığını kontrol edebilirsiniz **sudo bağlama | grep CIFS** komutunu ve aşağıdaki örnek çıkış gibi çıktısını denetleniyor:

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

Varsa **önbellek strict =** veya **serverino** seçenektir değil sunmak, çıkarın ve bağlama Azure File storage yeniden bağlama komutunu çalıştırarak [belgelerine](../storage-how-to-use-files-linux.md). Ardından, yeniden denetle **/etc/fstab** girişi doğru seçeneği vardır.

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-to-linux"></a>Linux için Windows dosyaları kopyalarken'zaman damgaları kaybolduğundan

Linux/Unix platformlarda **cp -p** komutu başarısız olursa dosya 1 ve 2 dosyasını farklı kullanıcılar tarafından sahip olunan.

### <a name="cause"></a>Nedeni

Force bayrağını **f** içinde COPYFILE sonuçları yürütülürken **cp -p -f** UNIX üzerinde. Bu komut, size ait olmayan dosyanın zaman damgası korumak de başarısız olur.

### <a name="workaround"></a>Geçici çözüm

Depolama hesabı kullanıcı dosyaları kopyalamak için kullanın:

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun.

Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) hızla çözülmüş sorununuzu almak için.
