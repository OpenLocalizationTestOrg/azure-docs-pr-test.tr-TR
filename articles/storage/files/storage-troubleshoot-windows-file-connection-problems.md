---
title: "Windows'ta aaaTroubleshoot Azure File storage sorunlarını | Microsoft Docs"
description: "Windows Azure File storage sorunlarını giderme"
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
ms.date: 06/28/2017
ms.author: genli
ms.openlocfilehash: 19529d8af5d98790e2e381cd21ad4d0284acb124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a>Windows Azure File storage sorunlarını giderme

Bu makalede Windows istemcilerinden gelen bağlandığınızda, ilgili tooMicrosoft Azure File storage genel sorunları listeler. Ayrıca olası nedenleri ve çözümlemeleri için bu sorunları sağlar. Ayrıca bu makalede toohello sorun giderme adımları, aynı zamanda [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) , Windows hello emin olmak için istemci ortamın doğru önkoşulları vardır. Bu makalede açıklanan hello belirtileri ve ortam, tooget en iyi performans ayarlama yardımcı çoğunu algılanması AzFileDiagnostics otomatikleştirir. Bu bilgileri hello bulabilirsiniz [Azure dosya paylaşımları sorun gidericisini](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) adımları tooassist sağlayan sorunlarıyla bağlanma/eşleme/bağlama Azure dosya paylaşımlarını.


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a>Hata 53, hata 67 veya hata bağlama ya da Azure dosya paylaşımının çıkarın 87

Bir dosya paylaşımı şirket içi veya farklı bir veri merkezinde toomount çalıştığınızda aşağıdaki hatalar hello alabilirsiniz:

- 53 sistem hatası oluştu. Merhaba ağ yolu bulunamadı.
- 67 sistem hatası oluştu. Merhaba ağ adı bulunamıyor.
- 87 sistem hatası oluştu. Merhaba parametresi geçersiz.

### <a name="cause-1-unencrypted-communication-channel"></a>1. neden: Şifrelenmemiş bir iletişim kanalı

Güvenlik nedenleriyle, tooAzure dosya paylaşımları hello iletişim kanalını şifreli değildir ve hello bağlantı denemesi yapılan değil engellenen bağlantıları hello Azure dosya paylaşımları bulunduğu aynı veri merkezinde hello. Yalnızca hello kullanıcının istemci işletim sistemi SMB şifrelemesi destekliyorsa iletişim kanalı şifreleme sağlanır.

Windows 8, Windows Server 2012 ve sonraki sürümlerinde her sistem şifrelemeyi destekleyen SMB 3.0 içeren isteklerin anlaşmaları.

### <a name="solution-for-cause-1"></a>Neden 1 için çözüm

Merhaba aşağıdakilerden birini yapan bir istemciden Bağlan:

- Windows 8 ve Windows Server 2012 veya sonraki sürümler Hello gereksinimlerini karşılayan
- Merhaba, bir sanal makineden aynı bağlayan hello Azure dosya paylaşımı için kullanılan Azure depolama hesabı hello gibi veri merkezi

### <a name="cause-2-port-445-is-blocked"></a>Neden 2: Bağlantı noktası 445 engellendi

Bağlantı noktası 445 giden iletişim tooan Azure File storage datacenter engellenirse, sistem hatası 53 veya sistem hatası 67 ortaya çıkabilir. toosee hello izin veren veya bağlantı noktası 445, erişimden izin vermeyecek ISS'ler özetini Git çok[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).

toounderstand bu hello "Sistem hata 53" iletisi arkasında hello neden olup olmadığını Portqry tooquery hello TCP:445 uç noktası kullanabilirsiniz. Merhaba TCP:445 endpoint filtre olarak görüntüleniyorsa hello TCP bağlantı noktası engellendi. Örnek bir sorgu şöyledir:

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

TCP bağlantı noktası 445 hello ağ yol kuralı tarafından engellenirse çıktı aşağıdaki hello görürsünüz:

  `TCP port 445 (microsoft-ds service): FILTERED`

Hakkında daha fazla bilgi için bkz toouse Portqry, [hello Portqry.exe komut satırı yardımcı programının açıklaması](https://support.microsoft.com/help/310099).

### <a name="solution-for-cause-2"></a>Neden 2 için çözüm

BT departmanı tooopen 445 bağlantı noktası ile giden çok çalışma[Azure IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="cause-3-ntlmv1-is-enabled"></a>3. neden: NTLMv1 etkin

NTLMv1 iletişimi hello istemcide etkinse, sistem hatası 53 veya sistem hatası 87 ortaya çıkabilir. Azure File storage yalnızca NTLMv2 kimlik doğrulamasını destekler. Etkin NTLMv1 sahip daha az güvenli bir istemci oluşturur. Bu nedenle, iletişim için Azure File storage engellendi. 

toodetermine bu hello hatasının hello neden olup olmadığını doğrulayın aşağıdaki kayıt defteri alt anahtarı bu hello tooa değeri 3 ayarlanır:

**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**

Daha fazla bilgi için bkz: Merhaba [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) TechNet'te konu.

### <a name="solution-for-cause-3"></a>Neden 3 için çözüm

Merhaba geri **LmCompatibilityLevel** değeri 3'te kayıt defteri alt anahtarını aşağıdaki hello toohello varsayılan değeri:

  **HKLM\SYSTEM\CurrentControlSet\Control\Lsa**

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a>Hata 1816 "yeterli kotası kullanılabilir tooprocess bu komuttur" tooan Azure dosya paylaşımı kopyaladığınızda

### <a name="cause"></a>Nedeni

Hata 1816, burada hello dosya paylaşımı takılı hello bilgisayar için bir dosya izin verilen eşzamanlı açık tanıtıcıların sayısı üst sınırı hello ulaştığında oluşur.

### <a name="solution"></a>Çözüm

Bazı tanıtıcıları kapatarak Hello eşzamanlı açık tanıtıcı sayısını azaltın ve yeniden deneyin. Daha fazla bilgi için bkz: [Microsoft Azure Storage performans ve ölçeklenebilirlik Yapılacaklar listesi](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a>Windows Azure File storage tooand kopyalama yavaş dosya

Tootransfer dosyaları toohello Azure dosya hizmeti çalıştığınızda yavaş performans görebilirsiniz.

- Belirli bir en düşük g/ç boyutu gereksinim yoksa, en iyi performans için g/ç boyutu hello gibi 1 MB kullanmanızı öneririz.
-   Biliyorsanız hello son ile genişletme dosya boyutunu yazar ve hello hello dosyada unwritten tail sıfırlar, önceden bir genişletme yazma her yazma yapmak yerine sonra hello dosya boyutunu Ayarla içerdiğinde yazılımınızı uyumluluk sorunlarına sahip değil.
-   Merhaba sağ copy yöntemini kullanın:
    -   Kullanım [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) iki dosya paylaşımları arasında herhangi bir aktarım için.
    -   Kullanım [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) bir şirket içi bilgisayar dosya paylaşımlarına arasında.

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a>Windows 8.1 veya Windows Server 2012 R2 için ilgili önemli noktalar

Windows 8.1 veya Windows Server 2012 R2 çalıştıran istemciler için olduğundan emin olun, hello [KB3114025](https://support.microsoft.com/help/3114025) düzeltme yüklenir. Bu düzeltme oluşturma hello performansını artırır ve tanıtıcıları kapatın.

Komut dosyası toocheck hello düzeltmesinin yüklü olup olmadığını aşağıdaki hello çalıştırabilirsiniz:

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

Düzeltme yüklüyse, hello aşağıdaki çıktısı görüntülenir:

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> Windows Server 2012 R2 Azure Marketi görüntülerinde düzeltme aralık 2015'ten başlayarak varsayılan olarak yüklenen KB3114025 sahip.

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a>Bir sürücü harfine sahip bir klasör bulunmadığından **Bilgisayarım**

Yönetici olarak net Kullan'ı kullanarak Azure dosya paylaşımının eşlerseniz hello toobe göründükten eksik.

### <a name="cause"></a>Nedeni

Varsayılan olarak, bir yönetici olarak Windows dosya Gezgini çalışmaz. Bir yönetici komut isteminden net kullanım çalıştırırsanız, yönetici olarak hello ağ sürücüsü eşlemeli. Eşlenen sürücüler kullanıcı merkezli olduğundan, farklı bir kullanıcı hesabı altında bağlarsanız oturum hello kullanıcı hesabı hello sürücüleri görüntülemez.

### <a name="solution"></a>Çözüm
Merhaba paylaşımı, yönetici olmayan komut satırından bağlayın. Alternatif olarak, izleyebilirsiniz [bu TechNet konusuna](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** kayıt defteri değeri.

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a>Merhaba depolama hesabı eğik içeriyorsa net use komutu başarısız olur.

### <a name="cause"></a>Nedeni

eğik çizgi (/) Hello net use komutunu bir komut satırı seçeneği olarak yorumlar. Kullanıcı hesap adınızı eğik çizgiyle başlıyorsa, hello sürücü eşleştirmesi başarısız olur.

### <a name="solution"></a>Çözüm

Merhaba soruna geçici bir çözüm adımları toowork aşağıdaki hello birini kullanabilirsiniz:

- Merhaba aşağıdaki PowerShell komutunu çalıştırın:

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  Bir toplu iş dosyasından bu şekilde hello komutu çalıştırabilirsiniz:

  `Echo new-smbMapping ... | powershell -command –`

- Merhaba eğik hello ilk karakter olmadıkça hello anahtar toowork--bu soruna geçici bir çözüm etrafında çift tırnak işareti koyun. İse, hello etkileşimli mod kullanın ve parolanızı ayrı ayrı girin ya da, anahtarları tooget eğik çizgiyle başlamaması bir anahtarı yeniden oluşturmak.

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a>Uygulama veya hizmet bağlı Azure dosya depolama sürücü erişemiyor

### <a name="cause"></a>Nedeni

Kullanıcı başına bağlı sürücüler. Uygulama veya hizmet hello takılı hello sürücü bir daha farklı bir kullanıcı hesabı altında çalışıyorsa, Merhaba uygulaması hello sürücü görmezsiniz.

### <a name="solution"></a>Çözüm

Çözümleri aşağıdaki hello birini kullanın:

-   Hello Hello sürücü bağlama hello uygulamayı içeren aynı kullanıcı hesabı. PsExec gibi bir araç kullanabilirsiniz.
- Merhaba depolama hesabı adı ve anahtar hello kullanıcı adı ve parola parametrelerini hello net use komutunu içinde geçirin.

Bu yönergeleri izledikten sonra hello net kullanım hello sistem/ağ hizmeti hesabı için çalıştırdığınızda aşağıdaki hata iletisi alabilirsiniz: "1312 sistem hatası oluştu. Belirtilen oturum yok. Bunu zaten kapatılmış olabilir." Bu meydana gelirse, toonet kullanım geçirilen o hello kullanıcı adı, etki alanı bilgileri içerdiğinden emin olun (örneğin: "[depolama hesabı adı]. file.core.windows .net").

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a>"Şifreleme desteklemeyen tooa hedef dosyasını kopyaladığınız" hatası

Bir dosya hello ağ üzerinden kopyaladığınızda hello düz metin olarak aktarılan ve hello hedefte yeniden şifrelenir hello kaynak bilgisayarda, şifresi çözülen dosyasıdır. Ancak, şifrelenmiş bir dosya toocopy çalışırken aşağıdaki hata hello görebilirsiniz: "Şifrelemeyi desteklemiyor hello dosya tooa hedef kopyalıyorsunuz."

### <a name="cause"></a>Nedeni
Şifreleme Dosya Sistemi (EFS) kullanıyorsanız, bu sorun oluşabilir. BitLocker ile şifrelenmiş dosyaları kopyalanan tooAzure dosya depolama olabilir. Ancak, Azure File storage NTFS EFS desteklemez.

### <a name="workaround"></a>Geçici çözüm
toocopy hello ağ üzerinden dosya, ilk şifresini gerekir. Yöntemler aşağıdaki hello birini kullanın:

- Kullanım hello **/d kopyalama** komutu. Şifrelenmiş hello verir hello hedefte şifresi çözülen dosyaları olarak kaydedilen toobe dosyaları.
- Kayıt defteri anahtarını aşağıdaki hello ayarlayın:
  - Yol HKLM\Software\Policies\Microsoft\Windows\System =
  - Değer türü = DWORD
  - Adı CopyFileAllowDecryptedRemoteDestination =
  - Değer = 1

Bu ayar hello kayıt defteri toonetwork paylaşımları yapılan tüm kopyalama işlemleri etkiler unutmayın.

## <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun.
Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) , sorunun giderilmiş hızla tooget.
