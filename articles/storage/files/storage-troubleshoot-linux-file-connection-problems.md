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
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a>Linux Azure File storage sorunlarını giderme

Bu makalede ilgili tooMicrosoft Azure File storage Linux istemcilerden bağlandığınızda olan ortak sorunlar listelenmiştir. Ayrıca olası nedenleri ve çözümlemeleri için bu sorunları sağlar.

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a>"[izni reddedildi] Disk kotası aşıldı" tooopen bir dosya çalıştığınızda

Linux hello aşağıdakine benzer bir hata iletisini alıyorsunuz:

**<filename>[izni reddedildi] Disk kotası aşıldı**

### <a name="cause"></a>Nedeni

Bir dosya için izin verilen eşzamanlı açık tanıtıcıların hello üst sınırına ulaştınız.

### <a name="solution"></a>Çözüm

Bazı tanıtıcıları kapatarak Hello eşzamanlı açık tanıtıcı sayısını azaltın ve hello işlemi yeniden deneyin. Daha fazla bilgi için bkz: [Microsoft Azure Storage performans ve ölçeklenebilirlik Yapılacaklar listesi](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a>Yavaş dosya Linux Azure File storage tooand kopyalama

-   Belirli bir en düşük g/ç boyutu gereksinim yoksa, en iyi performans için g/ç boyutu hello gibi 1 MB kullanmanızı öneririz.
-   Merhaba son yazma işlemlerini kullanarak genişletme dosya boyutunu bildiğiniz ve hello dosyada unwritten bir kuyruk sıfır içerdiğinde yazılımınızı uyumluluk sorunları yaşıyorsanız değil, önceden bir genişletme her yazma yapmak yerine hello dosya boyutu ayarlama yazma.
-   Merhaba sağ copy yöntemini kullanın:
    -   Kullanım [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) iki dosya paylaşımları arasında herhangi bir aktarım için.
    -   Kullanım [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) bir şirket içi bilgisayar dosya paylaşımlarına arasında.

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a>"Error(112) bağlayın: ana bilgisayar kapalı olduğu" yeniden bağlanma zaman aşımı nedeniyle

"112" bağlama hata Hello istemci uzun bir süredir boşta hello Linux istemcide oluşur. Genişletilmiş boşta kalma süresi sonra hello istemci bağlantısını keser ve hello bağlantı zaman aşımına uğruyor.  

### <a name="cause"></a>Nedeni

Merhaba bağlantı nedeniyle aşağıdaki hello için boşta olabilir:

-   Merhaba varsayılan "yumuşak" Bağlama seçeneği kullanıldığında bir TCP bağlantı toohello sunucusu yeniden oluşturmayı engelle ağ iletişim hatası
-   Eski tekrar içinde mevcut olmayan son yeniden bağlanma düzeltmeleri

### <a name="solution"></a>Çözüm

Bu yeniden bağlanma sorunu hello Linux Çekirdeği'nde şimdi aşağıdaki değişiklikler hello bir parçası olarak sabit:

- [Düzeltme yeniden toonot smb3 oturum erteleme soket uzun yeniden sonra yeniden](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [Yuva hemen yeniden sonra echo hizmeti çağırın](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [CIFS: yeniden bağlanma sırasında olası Bellek Bozulması Düzelt](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [CIFS: bir olası çift mutex (çekirdek v4.9 ve üzeri) yeniden bağlanma sırasında kilitleme Düzelt](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

Tooall hello henüz Linux dağıtımları ancak, bu değişiklikleri bağlantı noktası kurulmuş değil. Bu düzeltme ve diğer yeniden bağlanmayı düzeltmeleri popüler Linux tekrar aşağıdaki hello yapılır: 4.4.40, 4.8.16 ve 4.9.1. Bu önerilen çekirdek sürümlerinin tooone yükselterek bu düzeltmenin elde edebilirsiniz.

### <a name="workaround"></a>Geçici çözüm

Sabit bağlama belirterek bu soruna geçici çözüm bulabilirsiniz. Bu, bağlantı kurulana kadar veya açıkça kesintiye uğrarsa ve kullanılan tooprevent hataları ağ zaman aşımı nedeniyle olabilir kadar hello istemci toowait zorlar. Ancak, bu geçici çözüm belirsiz bekler neden olabilir. Hazırlanan toostop bağlantıları gerektiği gibi olabilir.

Toohello son çekirdek sürümleri yükseltemiyorsanız 30 saniye tooevery yazma hello Azure dosya paylaşımı veya daha az bir dosya tutarak bu soruna geçici çözüm. Merhaba yeniden yazma işlemi oluşturulan veya hello dosyada değişiklik tarihi gibi bu bir yazma işlemi olmalıdır. Aksi takdirde, önbelleğe alınan sonuçları alabilirsiniz ve işleminizi hello yeniden bağlanmayı tetikleyebilir değil.

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a>"Error(115) bağlayın: İşlem Sürüyor" olduğunda, bağlama Azure File storage SMB 3.0 kullanarak

### <a name="cause"></a>Nedeni

Şifreleme özellikleri SMB 3. 0 ' ' ı desteklemez henüz bazı Linux dağıtımları ve bunlar toomount Azure File storage nedeniyle eksik bir özellik SMB 3.0 kullanılarak çalışırsanız kullanıcılar "115" hata mesajı alabilirsiniz.

### <a name="solution"></a>Çözüm

Linux için SMB 3.0 şifreleme özelliği 4.11 Çekirdeği'nde sunulmuştur. Bu özellik Azure dosya paylaşımının şirket içi veya farklı bir Azure bölgesindeki bağlama sağlar. Yayımlama Hello anda bu işlevselliği backported tooUbuntu 17.04 ve Ubuntu 16.10 olarak adlandırılmıştır. Linux SMB istemci şifreleme desteklemiyorsa, SMB 2.1 içinde bir Azure Linux VM'den kullanarak Azure File storage bağlama dosya depolama hesabı hello gibi aynı veri merkezinde hello.

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a>Bir Azure dosya paylaşımında yavaş performans üzerinde bir Linux VM takılı

### <a name="cause"></a>Nedeni

Olası bir nedeni yavaş performans önbelleğe almayı devre dışı bırakılır.

### <a name="solution"></a>Çözüm

toocheck önbelleğe almayı devre dışı bırakılıp bırakılmayacağını Merhaba Ara **önbellek =** girişi. 

**Önbellek = none** önbelleğe almayı devre dışı olduğunu belirtir.  Yeniden bağlama hello paylaşımı hello varsayılan bağlama komutunu kullanarak veya açıkça hello ekleyerek **önbellek strict =** önbelleğe alma veya "katı" önbelleğe alma modu varsayılan seçeneği toohello bağlama komutu tooensure etkindir.

Bazı senaryolarda hello **serverino** bağlama seçeneği hello neden **ls** komutu toorun stat her dizin girişi karşı. Büyük bir dizin listelerken Bu davranış performans düşüşüne neden olur. Merhaba takma seçeneklerini kontrol edebilirsiniz, **/etc/fstab** girişi:

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

Ayrıca hello çalıştırarak hello doğru seçeneklerini kullanılıp kullanılmadığını kontrol edebilirsiniz **sudo bağlama | grep CIFS** komut ve örnek çıktı aşağıdaki hello gibi çıktısını denetleniyor:

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

Merhaba, **önbellek strict =** veya **serverino** seçenektir değil sunmak, çıkarın ve bağlama Azure File storage yeniden hello hello bağlama komutu çalıştırarak [belgelerine](../storage-how-to-use-files-linux.md). Ardından, o hello yeniden denetle **/etc/fstab** girişi hello doğru seçeneği vardır.

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a>Windows tooLinux dosyaları kopyalarken'zaman damgaları kaybolduğundan

Linux/Unix platformlarda hello **cp -p** komutu başarısız olursa dosya 1 ve 2 dosyasını farklı kullanıcılar tarafından sahip olunan.

### <a name="cause"></a>Nedeni

Force bayrağını hello **f** içinde COPYFILE sonuçları yürütülürken **cp -p -f** UNIX üzerinde. Bu komut ayrıca toopreserve hello zaman damgası sahip olmadığınız hello dosyasının başarısız olur.

### <a name="workaround"></a>Geçici çözüm

Merhaba depolama hesabı kullanıcı hello dosyaları kopyalamak için kullanın:

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun.

Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) , sorunun giderilmiş hızla tooget.
