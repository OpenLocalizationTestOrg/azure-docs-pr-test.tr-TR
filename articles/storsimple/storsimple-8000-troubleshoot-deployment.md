---
title: "aaaTroubleshoot StorSimple 8000 serisi dağıtım sorunlarını | Microsoft Docs"
description: "Açıklar nasıl StorSimple ilk kez dağıttığınızda oluşan toodiagnose ve düzeltme hataları."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: a55a4b277c8afe25f1d5a43ab8d7a90436123410
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storsimple-device-deployment-issues"></a>StorSimple cihaz dağıtım sorunlarını giderme
## <a name="overview"></a>Genel Bakış
Bu makalede, Microsoft Azure StorSimple dağıtımınız için yararlı sorun giderme kılavuzu verilmiştir. Sık karşılaşılan sorunları, olası nedenler ve önerilen adımları toohelp StorSimple yapılandırdığınızda karşılaşabileceğiniz sorunları gidermek açıklar. 

Bu bilgiler tooboth hello StorSimple 8000 serisi fiziksel aygıt ve hello StorSimple bulut uygulaması geçerlidir.

> [!NOTE]
> Yüz aygıt yapılandırma ile ilgili sorunları hello aygıt hello için ilk kez dağıtırken veya hello aygıt çalışır durumda bunlar daha sonra ortaya çıkabilir oluşabilir. Bu makalede, ilk kez dağıtım sorunlarını giderme odaklanır. tootroubleshoot işletimsel bir aygıtı Git çok[kullanım hello Tanılama Aracı tootroubleshoot işletimsel bir aygıt](storsimple-8000-diagnostics.md).

Bu makalede ayrıca StorSimple dağıtım sorunlarını giderme için hello araçları açıklar ve adım adım sorun giderme örnek sağlar.

## <a name="first-time-deployment-issues"></a>İlk kez dağıtım sorunları
Bir sorunu yaşayıp cihazınız hello için ilk kez dağıtırken çalıştırırsanız hello aşağıdakileri göz önünde bulundurun:

* Fiziksel bir aygıtı gideriyorsanız hello donanım yüklendi ve açıklandığı şekilde yapılandırılmış olduğundan emin olun [StorSimple 8100 cihazınız yüklemek](storsimple-8100-hardware-installation.md) veya [StorSimple 8600 model CihazınızıYükleme](storsimple-8600-hardware-installation.md).
* Dağıtım önkoşulları denetleyin. Hello açıklanan tüm hello bilgilere sahip olduğunuzdan emin olun [dağıtım yapılandırma denetim listesi](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist).
* Merhaba sorun açıklanan hello StorSimple sürüm notları toosee gözden geçirin. Merhaba sürüm notları bilinen yükleme sorunları için geçici çözümler içerir. 

Aygıt dağıtımı sırasında hello en yaygın hello Kurulum Sihirbazı'nı çalıştırdığınızda ve ne zaman, Windows PowerShell aracılığıyla hello cihaz storsimple için yüz ortaya kullanıcıların verir. (StorSimple tooregister için Windows PowerShell kullanın ve StorSimple Cihazınızı yapılandırın. Cihaz kaydı hakkında daha fazla bilgi için bkz: [adım 3: yapılandırmak ve storsimple için Windows PowerShell aracılığıyla cihazınızın](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)).

Aşağıdaki bölümlerde hello hello StorSimple cihazı hello için ilk defa yapılandırdığınızda karşılaştığınız sorunları çözmenize yardımcı olabilir.

## <a name="first-time-setup-wizard-process"></a>İlk kez Kurulum Sihirbazı işlemi
Aşağıdaki adımları hello hello Kurulum Sihirbazı işlemi özetlenir. Ayrıntılı kurulum bilgi için bkz: [şirket içi StorSimple Cihazınızı dağıtma](storsimple-8000-deployment-walkthrough-u2.md).

1. Merhaba çalıştırmak [Invoke-HcsSetupWizard](https://technet.microsoft.com/library/dn688135.aspx) adımları kalan hello yönlendirecek cmdlet toostart hello Kurulum Sihirbazı. 
2. Merhaba ağ yapılandırın: hello Kurulum Sihirbazı'nı, StorSimple Cihazınızda hello veri 0 ağ arabirimi için ağ ayarlarını yapılandırmanıza olanak sağlar. Bu ayarları hello şunları içerir:
   * Sanal IP (VIP), alt ağ maskesi ve ağ geçidi – hello [kümesi HcsNetInterface](https://technet.microsoft.com/library/dn688161.aspx) cmdlet hello arka planda gerçekleştirilir. StorSimple Cihazınızda hello IP adresi, alt ağ maskesi ve ağ geçidi hello veri 0 ağ arabirimi için yapılandırır.
   * Birincil DNS sunucusunu – hello [kümesi HcsDnsClientServerAddress](https://technet.microsoft.com/library/dn688172.aspx) cmdlet hello arka planda gerçekleştirilir. StorSimple çözümünüzün hello DNS ayarlarını yapılandırır.
   * NTP sunucusu – hello [kümesi HcsNtpClientServerAddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet hello arka planda gerçekleştirilir. StorSimple çözümünüzün hello NTP sunucusu ayarlarını yapılandırır.
   * İsteğe bağlı web proxy – hello [kümesi HcsWebProxy](https://technet.microsoft.com/library/dn688154.aspx) cmdlet hello arka planda gerçekleştirilir. Ayarlar ve StorSimple çözümünüzün için hello web proxy yapılandırması sağlar.
3. Merhaba parolasını ayarla: hello sonraki adımdır tooset hello cihaz Yöneticisi parolasını ayarlama.
   Merhaba cihaz Yöneticisi parolası tooyour aygıtta kullanılan toolog ' dir. Merhaba varsayılan cihaz parolası **Parola1**.
        
     > [!IMPORTANT]
     > Parolalar önce kayıt toplanan, ancak yalnızca hello aygıt başarıyla kaydettikten sonra uygulanır. Bir parola hatası tooapply ise (Merhaba karmaşıklık gereksinimlerini karşılayan) parolaları toplanan hello gerekli kadar istendiğinde toosupply hello parola yeniden olur.
     
4. Merhaba kaydedilecek: hello son adım, Microsoft Azure'da çalışan hello StorSimple Aygıt Yöneticisi'ni hizmetiyle tooregister hello aygıttır. Merhaba kayıt gerektirir çok[hello hizmet kayıt anahtarını alın](storsimple-8000-manage-service.md#get-the-service-registration-key) gelen Azure portal hello ve hello Kurulum Sihirbazı'nda sağlayın. **Merhaba cihaz sorunsuz kaydedildikten sonra hizmet verileri şifreleme anahtarı tooyou sağlanır. Bu şifreleme anahtarı güvenli bir yerde, olacağından tookeep tooregister hello hizmetiyle tüm sonraki cihazlar gerekli olduğundan emin olun.**

## <a name="common-errors-during-device-deployment"></a>Aygıt dağıtımı sırasında ortak hataları
ne zaman karşılaşabileceğiniz tablolar listesi hello sık karşılaşılan, hello:

* Merhaba gerekli ağ ayarlarını yapılandırın.
* Merhaba isteğe bağlı web proxy ayarlarını yapılandırın.
* Merhaba cihaz Yöneticisi parolasını ayarla.
* Merhaba cihazı kaydedin.

## <a name="errors-during-hello-required-network-settings"></a>Merhaba gerekli ağ ayarlarını sırasında hatalar
| Hayır. | Hata iletisi | Olası nedenler | Önerilen eylem |
| --- | --- | --- | --- |
| 1 |Invoke-HcsSetupWizard: Bu komut yalnızca hello etkin denetleyicisinde çalıştırılabilir. |Yapılandırma hello pasif denetleyicisinde gerçekleştirildi. |Bu komut hello etkin denetleyicisinden çalıştırın. Daha fazla bilgi için bkz: [Cihazınızı etkin bir denetleyicisindeki tanımlamak](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device). |
| 2 |Invoke-HcsSetupWizard: Cihaz hazır değil. |Veri 0 hello ağ bağlantısı sorunları vardır. |Veri 0 Hello fiziksel ağ bağlantısını denetleyin. |
| 3 |Invoke-HcsSetupWizard: Hello ağdaki başka bir sistem ile bir IP adresi çakışması yoktur (HRESULT özel durumu: 0x80070263). |DATA 0 için sağlanan hello IP zaten başka bir sistem tarafından kullanılıyor oluştu. |Kullanımda olmadığından yeni bir IP sağlar. |
| 4 |Invoke-HcsSetupWizard: Küme kaynağı başarısız oldu. (HRESULT özel durumu: 0x800713AE). |Yinelenen VIP. sağlanan hello IP zaten kullanımda. |Kullanımda olmadığından yeni bir IP sağlar. |
| 5 |Invoke-HcsSetupWizard: Geçersiz bir IPv4 adresi. |Başlangıç IP adresi hatalı bir biçimde sağlanır. |Merhaba biçimini denetleyin ve IP adresiniz yeniden sağlayın. Daha fazla bilgi için bkz: [IPv4 adresleme][1]. |
| 6 |Invoke-HcsSetupWizard: Geçersiz IPv6 adresi. |Başlangıç IP adresi hatalı bir biçimde sağlanır. |Merhaba biçimini denetleyin ve IP adresiniz yeniden sağlayın. Daha fazla bilgi için bkz: [IPv6 adresleme][2]. |
| 7 |Invoke-HcsSetupWizard: Hello Bitiş Noktası Eşleştiricisi kullanılabilir daha fazla uç nokta yok. (HRESULT özel durumu: 0x800706D9) |Merhaba küme işlevselliğini çalışmıyor. |[Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) sonraki adımlar için. |

## <a name="errors-during-hello-optional-web-proxy-settings"></a>Merhaba isteğe bağlı web proxy ayarları sırasında hatalar
| Hayır. | Hata iletisi | Olası nedenler | Önerilen eylem |
| --- | --- | --- | --- |
| 1 |Invoke-HcsSetupWizard: Geçersiz parametre (HRESULT özel durumu: 0x80070057) |Merhaba proxy ayarlarını sağlanan hello parametrelerden biri geçerli değil. |Merhaba URI hello doğru biçimde sağlanmadı. Aşağıdaki biçimi kullanın hello: http://*<IP address or FQDN of hello web proxy server>*:*<TCP port number>* |
| 2 |Invoke-HcsSetupWizard: RPC sunucusu kullanılamıyor (HRESULT özel durumu: 0x800706ba) |Merhaba kök nedeni hello aşağıdakilerden biridir:<ol><li>Merhaba kümesi yedeklemek değildir.</li><li>Merhaba pasif denetleyiciyi hello etkin denetleyicisi ile iletişim kuramıyor ve Pasif denetleyicisinden hello komutunu çalıştırın.</li></ol> |Bağlı olarak Hello kök neden:<ol><li>[Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) toomake emin bu hello kümedir ayarlama.</li><li>Merhaba etkin denetleyicisinden Hello komutunu çalıştırın. Merhaba pasif denetleyicisinden toorun hello komutunun istiyorsanız, tooensure gerekir bu hello pasif denetleyiciyi hello etkin denetleyicisi ile iletişim kurabilir. Çok gerekir[Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) Bu bağlantı bozuk ise.</li></ol> |
| 3 |Invoke-HcsSetupWizard: RPC çağrısı başarısız oldu (HRESULT özel durumu: 0x800706be) |Küme çalışmıyor. |[Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) toomake emin bu hello kümedir ayarlama. |
| 4 |Invoke-HcsSetupWizard: Küme kaynağı bulunamadı (HRESULT özel durumu: 0x8007138f) |Merhaba küme kaynağı bulunamadı. Bu durum Hello yükleme doğru değildi ortaya çıkar. |Tooreset hello aygıt toohello fabrika varsayılan ayarlarına gerekebilir. [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) toocreate bir küme kaynağı. |
| 5 |Invoke-HcsSetupWizard: Küme kaynağı çevrimiçi değil (HRESULT özel durumu: 0x8007138c) |Küme kaynaklarının çevrimiçi değildir. |[Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) sonraki adımlar için. |

## <a name="errors-related-toodevice-administrator-password"></a>Hatalarla ilgili toodevice yönetici parolası
Merhaba varsayılan cihaz Yöneticisi parolası **Parola1**. Bu parolayı hello ilk oturum açtıktan sonra süresi dolar; Bu nedenle, toouse hello Kurulum Sihirbazı'nı toochange gerekir. Merhaba aygıt hello için ilk kez kaydederken yeni bir cihaz Yöneticisi parolasını sağlamanız gerekir. 

Parolalarınızı hello aşağıdaki gereksinimleri karşıladığından emin olun:

* Cihaz Yöneticisi parolası 8 ile 15 karakter uzunluğunda olmalıdır.
* Parolalar, 3, 4 karakter türleri aşağıdaki hello içermelidir: küçük harfler, büyük harf, sayısal ve özel. 
* Parolanızı olamaz olması hello son 24 parola hello gibi aynı.

Ayrıca, her yıl parolaların süreleri göz önünde bulundurun ve yalnızca hello aygıt başarıyla kaydettikten sonra değiştirilebilir. Merhaba kayıt herhangi bir nedenle başarısız olursa, hello parolaları değiştirilmez.

Cihaz Yöneticisi parolası ile ilgili daha fazla bilgi için çok Git[kullanım hello StorSimple cihaz Yöneticisi hizmeti toochange StorSimple parolanızı](storsimple-8000-change-passwords.md).

Bir veya daha fazla hello Aygıt Yöneticisi ve StorSimple Snapshot Manager parolalarını ayarlarken aşağıdaki hatalar hello karşılaşabilirsiniz.

| Hayır. | Hata iletisi | Önerilen eylem |
| --- | --- | --- |
| 1 |Merhaba parola hello en fazla uzunluğu aşıyor. |Cihaz Yöneticisi parolası 8-15 karakter uzunluğunda olmalıdır. |
| 2 |Merhaba parola gerekli hello uzunluğu karşılamıyor. |Cihaz Yöneticisi parolası 8-15 karakter uzunluğunda olmalıdır.|
| 3 |Merhaba parola küçük harf karakterler içermelidir. |Parolalar, 3, 4 karakter türleri aşağıdaki hello içermelidir: küçük harfler, büyük harf, sayısal ve özel. Parolanız şu gereksinimleri karşıladığından emin olun. |
| 4 |Merhaba parola sayısal karakter içermelidir. |Parolalar, 3, 4 karakter türleri aşağıdaki hello içermelidir: küçük harfler, büyük harf, sayısal ve özel. Parolanız şu gereksinimleri karşıladığından emin olun. |
| 5 |Merhaba parola özel karakterler içermelidir. |Parolalar, 3, 4 karakter türleri aşağıdaki hello içermelidir: küçük harfler, büyük harf, sayısal ve özel. Parolanız şu gereksinimleri karşıladığından emin olun. |
| 6 |Merhaba parola 4 karakter türleri aşağıdaki hello 3 içermelidir: büyük harf, küçük harfler, sayısal ve özel. |Parolanız karakter gerekli hello türlerini içermiyor. Parolanız şu gereksinimleri karşıladığından emin olun. |
| 7 |Parametre onay eşleşmiyor. |Parolanızı tüm gereksinimlerini karşıladığından ve bunu doğru girdiğinizden emin olun. |
| 8 |Parolanızı hello varsayılan aynı olamaz. |Merhaba varsayılan parola *Parola1*. Merhaba ilk kez oturum açtıktan sonra bu parolayı toochange gerekir. |
| 9 |Girdiğiniz hello parola hello aygıt parolası eşleşmiyor. Lütfen hello parolayı yeniden yazın. |Merhaba parolayı denetleyin ve yeniden yazın. |

Hello cihaz kaydedilir, ancak yalnızca başarılı kayıttan sonra uygulanan önce parolaları toplanır. Merhaba parola kurtarma iş akışı kayıtlı hello aygıt toobe gerektirir.

> [!IMPORTANT]
> Başarılı olana dek üst üste dener toocollect hello parola hello yazılım sonra genel olarak, bir deneme tooapply bir parola, başarısız olur. Nadir durumlarda, hello parola uygulanamaz. Bu durumda, hello kaydedilecek ve devam edin, ancak hello parolaları değiştirilmeyecektir. Hello Azure portal hello kaydından sonra hello cihaz Yöneticisi parolasını değiştirebilirsiniz.


Merhaba hello StorSimple cihaz Yöneticisi hizmeti üzerinden Azure portal hello parolayı sıfırlayabilirsiniz. Daha fazla bilgi için çok Git[değişiklik hello cihaz Yöneticisi parolası](storsimple-8000-change-passwords.md#change-the-device-administrator-password).

## <a name="errors-during-device-registration"></a>Cihaz kaydı sırasında hatalar
Microsoft Azure tooregister hello aygıtta çalışan hello StorSimple cihaz Yöneticisi hizmeti kullanın. Bir veya daha fazla cihaz kaydı sırasında sorunları aşağıdaki hello karşılaştığınız.

| Hayır. | Hata iletisi | Olası nedenler | Önerilen eylem |
| --- | --- | --- | --- |
| 1 |Hata 350027: tooregister hello aygıtı hello StorSimple cihaz Yöneticisi ile başarısız oldu. | |Birkaç dakika bekleyin ve ardından hello işlemi yeniden deneyin. Merhaba sorun devam ederse [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md). |
| 2 |Hata 350013: Hello cihaz kaydedilirken bir hata oluştu. Bu tooincorrect hizmet kayıt anahtarını olabilir. | |Lütfen hello aygıt yeniden hello doğru hizmet kayıt anahtarı ile kaydedin. Daha fazla bilgi için bkz: [hello hizmet kayıt anahtarını al.](storsimple-8000-manage-service.md#get-the-service-registration-key) |
| 3 |Aygıt Yöneticisi hizmeti kimlik doğrulama tooStorSimple hata 350063: Geçirildi ancak kayıt başarısız oldu. Lütfen hello işlemi bir süre sonra yeniden deneyin. |Bu hata, ACS ile kimlik doğrulaması başarılı ancak hello kaydı yapılan çağrı toohello hizmeti başarısız oldu gösterir. Bu aralıklı ağ sistemimizde sorun sonucu olabilir. |Merhaba sorunu ederse [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md). |
| 4 |Hata 350049: hello hizmet kaydı sırasında erişilemedi. |Toohello hizmet Hello çağrısı yapıldığında, bir web özel durumu aldı. Bazı durumlarda bu hello işlemi daha sonra yeniden denenerek sabit. |Lütfen IP adresi ve DNS adı denetleyin ve hello işlemi yeniden deneyin. Merhaba sorun devam ederse [Microsoft Support başvurun.](storsimple-8000-contact-microsoft-support.md) |
| 5 |Hata 350031: hello cihaz zaten kayıtlı. | |Kullanılabilir eylem gerekli. |
| 6 |Hata 350016: Cihaz kaydı başarısız oldu. | |Merhaba kayıt anahtarının doğru olduğundan emin olun. |
| 7 |Invoke-HcsSetupWizard: Cihazınız kaydedilirken bir hata oluştu; Bu tooincorrect IP adresi veya DNS adı olabilir. Lütfen ağ ayarlarınızı denetleyin ve yeniden deneyin. Merhaba sorun devam ederse [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md). (Hata 350050) |Cihazınızı Ağ dışından hello ping atabilir emin olun. Merhaba kayıt, bağlantı toooutside ağ yoksa bu hata ile başarısız olabilir. Bu hata, bir veya daha fazlasını hello birleşimi olabilir:<ul><li>Yanlış IP</li><li>Hatalı alt ağ</li><li>Yanlış ağ geçidi</li><li>DNS ayarları yanlış</li></ul> |Merhaba hello adımlarına bakın [adım adım sorun giderme örnek](#step-by-step-storsimple-troubleshooting-example). |
| 8 |Invoke-HcsSetupWizard: tooan iç hizmet hatası [0x1FBE2] hello geçerli işlemi başarısız oldu. Lütfen hello işlemi bir süre sonra yeniden deneyin. Merhaba sorun devam ederse, lütfen Microsoft Support başvurun. |Bu, hizmet veya aracı için tüm kullanıcı görünmez hataların durum genel bir hatadır. Merhaba en yaygın nedeni, hello ACS kimlik doğrulamasının başarısız olabilir. Hello hatanın olası nedenlerinden hello NTP sunucusu yapılandırma sorunları ve saati hello aygıtta düzgün ayarlanmamış olmasıdır. |(Sorunları varsa) başlangıç saati düzeltin ve hello kayıt işlemi yeniden deneyin. Merhaba Set-HcsSystem - saat dilimi komutu tooadjust hello saat dilimi kullanırsanız, her sözcüğün hello saat dilimi (örneğin "Pasifik Standart Saati") büyük harfe çevirme.  Bu sorun devam ederse [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) sonraki adımlar için. |
| 9 |Uyarı: hello cihaz etkinleştirilemedi. Cihaz yöneticinize ve StorSimple Snapshot Manager parolaları değiştirilmedi. |Merhaba kaydı başarısız olursa hello Aygıt Yöneticisi ve StorSimple Snapshot Manager parolaları değiştirilmez. | |

## <a name="tools-for-troubleshooting-storsimple-deployments"></a>StorSimple dağıtım sorunlarını giderme araçları
StorSimple StorSimple çözümünüzün tootroubleshoot kullanabileceğiniz çeşitli araçlar içerir. Bunlar:

* Paketler ve cihaz günlükleri destekler.
* Sorun giderme için özellikle tasarlanmış cmdlet.

## <a name="support-packages-and-device-logs-available-for-troubleshooting"></a>Paketler ve cihaz günlükleri kullanılabilir sorun giderme için destek
Bir destek paketi hello Microsoft Support takım aygıt sorunları giderme konusunda yardımcı olabilecek tüm hello ilgili günlükleri içerir. StorSimple toogenerate sonra destek personeli ile paylaşabilir bir şifrelenmiş destek paketi için Windows PowerShell'i kullanabilirsiniz.

### <a name="tooview-hello-logs-or-hello-contents-of-hello-support-package"></a>tooview hello günlükleri veya hello Merhaba içeriğine destek paketi
1. Bölümünde açıklandığı gibi StorSimple toogenerate destek paketi için Windows PowerShell kullanmak [oluşturma ve Destek Paketi yönetmek](storsimple-8000-create-manage-support-package.md).
2. Merhaba karşıdan [şifre çözme betik](https://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) , istemci bilgisayarda yerel olarak.
3. Bu [adım adım yordam](storsimple-8000-create-manage-support-package.md#edit-a-support-package) tooopen ve şifre çözme hello destek paketi.
4. Merhaba etw/etvx biçiminde günlüklerin destek paketi şifresi. Windows Olay Görüntüleyicisi'nde bu dosyalar, aşağıdaki adımları tooview hello gerçekleştirebilirsiniz:
   
   1. Merhaba çalıştırmak **eventvwr** Windows istemciniz üzerinde komutu. Bu hello Olay Görüntüleyicisi'ni başlatır.
   2. Merhaba, **Eylemler** bölmesinde tıklatın **açık kaydedilmiş günlük** ve noktası toohello günlük dosyaları etvx/etw biçiminde (Merhaba destek paketi). Merhaba dosya artık görüntüleyebilirsiniz. Merhaba dosyayı açtıktan sonra sağ tıklayın ve metin olarak hello dosyasını kaydedin.
      
      > [!IMPORTANT]
      > Merhaba de kullanabilirsiniz **Get-WinEvent** cmdlet tooopen Windows PowerShell'de bu dosyalar. Daha fazla bilgi için bkz: [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx) hello Windows PowerShell cmdlet başvuru belgeleri içinde.
     
5. Merhaba günlükleri Olay Görüntüleyicisi'nde açtığınızda, sorunları içeren günlükler aşağıdaki hello arayın toohello aygıt yapılandırması ile ilgili:
   
   * hcs_pfconfig/Operational günlük
   * hcs_pfconfig/Config
6. Merhaba günlük dosyalarında dizeleri için ilgili toohello cmdlet'leri hello Kurulum Sihirbazı tarafından adlı arayın. Bkz: [ilk kez Kurulum Sihirbazı işlemi](#first-time-setup-wizard-process) bu cmdlet'leri listesi.
7. Merhaba hello sorunun nedenini çıkışı mümkün toofigure emin değilseniz, yapabilecekleriniz [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) sonraki adımlar için. Kullanım hello adımları [bir destek isteği oluşturmak](storsimple-8000-contact-microsoft-support.md#create-a-support-request) olduğunda, Microsoft Yardım için Support başvurun.

## <a name="cmdlets-available-for-troubleshooting"></a>Sorun giderme için uygun cmdlet'leri
Aşağıdaki Windows PowerShell cmdlet'leri toodetect bağlantı hatalar hello kullanın.

* `Get-NetAdapter`: Bu cmdlet toodetect hello sistem durumunu ağ arabirimlerinin kullanın.
* `Test-Connection`: Bu cmdlet toocheck hello ağ bağlantısı içinde ve dışında hello ağ kullanın.
* `Test-HcsmConnection`: Bu cmdlet toocheck hello bağlantısını başarıyla kayıtlı bir cihazla kullanın.
* `Sync-HcsTime`: Kullanın Bu cmdlet toodisplay aygıt tarih ve saati eşitleme hello NTP sunucusu ile zorlar.
* `Enable-HcsPing`ve `Disable-HcsPing`: Bu cmdlet'leri tooallow hello konakları tooping hello ağ arabirimleri, StorSimple Cihazınızda kullanın. Varsayılan olarak, hello StorSimple ağ arabirimleri tooping istekleri yanıt vermez.
* `Trace-HcsRoute`: Bu cmdlet bir rota izleme aracı olarak kullanın. Paketleri tooeach yönlendirici hello yolu tooa son hedef sunucudaki bir süre boyunca gönderir ve her adımın döndürülen Karşılama paketleri göre sonuçları hesaplar. Bu yana `Trace-HcsRoute` hangi yönlendiriciler saptayabilirler veya bağlantıları ağ sorunlara neden verilen yönlendirici veya bağlantı sırasında paket kaybı hello derecesini gösterir.
* `Get-HcsRoutingTable`: Bu cmdlet toodisplay hello yerel IP yönlendirme tablosu kullanın.

## <a name="troubleshoot-with-hello-get-netadapter-cmdlet"></a>Merhaba Get-NetAdapter cmdlet ile ilgili sorunları giderme
İlk kez aygıt dağıtımı için ağ arabirimleri yapılandırdığınızda hello aygıt hello hizmetiyle henüz kaydedilmediğinden hello donanım durum hello StorSimple cihaz Yöneticisi hizmeti kullanıcı Arabirimi kullanılabilir değil. Ayrıca, hello **donanım durumu** dikey değil her zaman doğru yansıtacak hello aygıt hello durumunu özellikle hizmet eşitleme etkileyen bir sorun varsa. Bu durumlarda hello kullanabilirsiniz `Get-NetAdapter` cmdlet toodetermine hello ağ arabirimleri ve sistem durumunu.

### <a name="toosee-a-list-of-all-hello-network-adapters-on-your-device"></a>toosee aygıtınızdaki tüm hello ağ bağdaştırıcılarının bir listesini
1. StorSimple için Windows PowerShell'i başlatın ve ardından `Get-NetAdapter`. 
2. Merhaba Hello çıktısını kullanmak `Get-NetAdapter` cmdlet'i ve yönergeleri toounderstand aşağıdaki hello Merhaba, ağ arabiriminin durumu.
   
   * Merhaba arabirimi sağlam ve etkin ise, hello **İfındex** durum gösterilir olarak **yukarı**.
   * Merhaba arabirimi sağlıklı olduğundan ancak (bir ağ kablosu) fiziksel olarak bağlı değil, hello **İfındex** olarak gösterilen **devre dışı**.
   * Merhaba arabirimi sağlıklı ancak etkin değil ise, hello **İfındex** durum gösterilir olarak **NotPresent**.
   * Merhaba arabirimi yoksa, bu listede görünmez. Merhaba StorSimple cihaz Yöneticisi hizmeti kullanıcı Arabirimi hala bu arabirimi başarısız durumda gösterir.

Hakkında daha fazla bilgi için toouse Bu cmdlet, çok Git[GetNetAdapter](https://technet.microsoft.com/library/jj130867.aspx) hello Windows PowerShell cmdlet başvurusunun içinde.

Merhaba aşağıdaki bölümlerde Göster hello çıktısını örnekleri `Get-NetAdapter` cmdlet'i.

 Bu örnekte, denetleyici 0 hello pasif denetleyiciyi olduğu ve aşağıdaki gibi yapılandırılmış:

* Veri 0, veri 1, veri 2 ve veri 3 ağ arabirimleri hello aygıtta vardı.
* Veri 4 ve verileri 5 ağ arabirim kartları mevcut değil; Bu nedenle, hello çıktısında listelenmemiştir.
* Veri 0 etkinleştirildi.

Denetleyici 1 hello etkin denetleyicisi olduğundan ve aşağıdaki gibi yapılandırılmış:

* Veri 0, veri 1, veri 2, veri 3, veri 4 ve verileri 5 ağ arabirimleri hello aygıtta vardı.
* Veri 0 etkinleştirildi.

**Örnek çıktı – denetleyici 0**

Merhaba, denetleyici 0 (Merhaba pasif denetleyiciyi) hello çıktısı aşağıdadır. Veri 1, veri 2 ve veri 3 bağlı değil. Merhaba aygıtta olmadıklarından veri 4 ve verileri 5 listelenmemiştir.

     Controller0>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter #2     17       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter        14       NotPresent
     Ethernet 2           HCS VNIC                                    13       Up
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up


**Örnek çıktı – Denetleyici 1**

Merhaba, 1 (Merhaba etkin denetleyicisi) denetleyicisinden hello çıkışı aşağıdadır. Yalnızca hello aygıt ağ arabiriminde yapılandırılan veri 0 hello ve çalışıyor.

     Controller1>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter        18       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter #2     19       NotPresent
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up
     Ethernet 2           HCS VNIC                                    13       Up
     DATA5                Intel(R) Gigabit ET Dual Port Server...     14       NotPresent
     DATA4                Intel(R) Gigabit ET Dual Port Serv...#2     17       NotPresent


## <a name="troubleshoot-with-hello-test-connection-cmdlet"></a>Merhaba Bağlantıyı Sına cmdlet ile ilgili sorunları giderme
Merhaba kullanabilirsiniz `Test-Connection` cmdlet toodetermine StorSimple Cihazınızı Ağ dışından toohello olup bağlanabilir. Merhaba DNS dahil olmak üzere tüm hello ağ parametreleri hello Kurulum Sihirbazı'nda doğru yapılandırılmışsa hello kullanabilirsiniz `Test-Connection` cmdlet tooping outlook.com gibi hello ağ dışında bilinen bir adres.

Ping devre dışı bırakılırsa, bu cmdlet ping tootroubleshoot bağlantı sorunları etkinleştirmeniz gerekir.

Merhaba çıktı örnekleri aşağıdaki hello bkz `Test-Connection` cmdlet'i.

> [!NOTE]
> Merhaba ilk örnekte hello cihaz yanlış DNS ile yapılandırılır. Merhaba ikinci örnekte hello DNS doğrudur.

**Örnek çıktı – yanlış DNS**

Aşağıdaki örnek hello DNS çözümlenirse, hello gösteren hiçbir çıktı hello IPv4 ve IPv6 adresleri için yoktur. Bu ağ dışında hiçbir bağlantı toohello ve doğru DNS sağlanan toobe gerekiyor anlamına gelir.

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com

**Örnek çıktı – doğru DNS**

Aşağıdaki örnek hello hello DNS döndürür IPv4 adresi, DNS doğru bir şekilde yapılandırıldığından bu hello belirten hello. Bu ağ dışından bağlantı toohello olduğunu doğrular.

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194

## <a name="troubleshoot-with-hello-test-hcsmconnection-cmdlet"></a>Merhaba Test HcsmConnection cmdlet ile ilgili sorunları giderme
Kullanım hello `Test-HcsmConnection` cmdlet'i zaten bir aygıt için bağlı tooand, StorSimple cihaz Yöneticisi hizmetine kayıtlı. Bu cmdlet, kayıtlı bir cihazla hello karşılık gelen StorSimple cihaz Yöneticisi hizmeti arasında hello bağlantısı doğrulamanıza yardımcı olur. StorSimple için Windows PowerShell üzerinde bu komutu çalıştırabilirsiniz.

### <a name="toorun-hello-test-hcsmconnection-cmdlet"></a>toorun hello Test HcsmConnection cmdlet'i
1. Merhaba cihazın kayıtlı olduğundan emin olun.
2. Merhaba cihaz durumunu kontrol edin. Merhaba aygıt, Bakım modunda veya çevrimdışı devre dışı bırakılmışsa aşağıdaki hatalar hello birini görebilirsiniz:
   
   * ErrorCode.CiSDeviceDecommissioned – bu hello aygıt devre dışı olduğunu gösterir.
   * ErrorCode.DeviceNotReady – bu hello aygıt bakım modunda olduğunu gösterir.
   * ErrorCode.DeviceNotReady – bu hello aygıtın çevrimiçi olduğunu gösterir.
3. Bu hello StorSimple Aygıt Yöneticisi hizmetinin çalıştığından emin olun (Merhaba kullanmak [Get-ClusterResource](https://technet.microsoft.com/library/ee461004.aspx) cmdlet'i). Merhaba hizmeti çalışmıyorsa, aşağıdaki hatalar hello görebilirsiniz:
   
   * ErrorCode.CiSApplianceAgentNotOnline
   * ErrorCode.CisPowershellScriptHcsError – Bu, Get-ClusterResource çalıştırdığınızda istisna olduğunu gösterir.
4. Merhaba erişim denetimi Hizmeti'nden (ACS) belirteci denetleyin. Bir web özel durum oluşturursa, bir ağ geçidi sorun, eksik bir proxy kimlik doğrulaması, yanlış bir DNS veya kimlik doğrulama hatası hello sonucu olabilir. Aşağıdaki hatalar hello görebilirsiniz:
   
   * ErrorCode.CiSApplianceGateway – bu gösterir HttpStatusCode.BadGateway özel durum: hello adı çözümleyicisini hello ana bilgisayar adını çözümleyemiyor.
   * ErrorCode.CiSApplianceProxy – bu gösterir (HTTP durum kodu 407) HttpStatusCode.ProxyAuthenticationRequired özel durum: hello istemci hello proxy sunucusu ile doğrulanamıyor.
   * ErrorCode.CiSApplianceDNSError – bu gösterir WebExceptionStatus.NameResolutionFailure özel durum: hello adı çözümleyicisini hello ana bilgisayar adını çözümleyemiyor.
   * ErrorCode.CiSApplianceACSError – bu hello hizmet kimlik doğrulama hatası döndürdü, ancak bağlantısı olduğunu gösterir.
     
     Bir web özel oluşturmadığını ErrorCode.CiSApplianceFailure için kontrol edin. Bu, o hello Gereci başarısız gösterir.
5. Merhaba bulut hizmeti bağlantısını denetleyin. Merhaba hizmeti bir web özel durum oluşturursa, aşağıdaki hatalar hello görebilirsiniz:
   
   * ErrorCode.CiSApplianceGateway – bu gösterir HttpStatusCode.BadGateway özel durum: başka bir proxy veya hello özgün sunucudan bir ara proxy sunucusunun bozuk bir isteği aldı.
   * ErrorCode.CiSApplianceProxy – bu gösterir (HTTP durum kodu 407) HttpStatusCode.ProxyAuthenticationRequired özel durum: hello istemci hello proxy sunucusu ile doğrulanamıyor.
   * ErrorCode.CiSApplianceDNSError – bu gösterir WebExceptionStatus.NameResolutionFailure özel durum: hello adı çözümleyicisini hello ana bilgisayar adını çözümleyemiyor.
   * ErrorCode.CiSApplianceACSError – bu hello hizmet kimlik doğrulama hatası döndürdü, ancak bağlantısı olduğunu gösterir.
     
     Bir web özel oluşturmadığını ErrorCode.CiSApplianceSaasServiceError için kontrol edin. Bu hello StorSimple cihaz Yöneticisi hizmeti ile ilgili bir sorun olduğunu gösterir.
6. Azure Service Bus bağlantısını denetleyin. Merhaba aygıt toohello Service Bus bağlanamıyor ErrorCode.CiSApplianceServiceBusError gösterir.

Günlük dosyaları CiSCommandletLog0Curr.errlog hello ve CiSAgentsvc0Curr.errlog özel durum ayrıntıları gibi daha fazla bilgi bulunur.

Nasıl toouse hello cmdlet'i hakkında daha fazla bilgi için çok Git[Test HcsmConnection](https://technet.microsoft.com/library/dn715782.aspx) hello Windows PowerShell başvuru belgeleri.

> [!IMPORTANT]
> Merhaba etkin ve hello pasif denetleyiciyi için bu cmdlet'i çalıştırabilirsiniz.

Merhaba çıktı örnekleri aşağıdaki hello bkz `Test-HcsmConnection` cmdlet'i.

**Örnek çıktı – StorSimple güncelleştirme 3'ü çalıştıran başarıyla kayıtlı cihaz**

      Controller1>Test-HcsmConnection

      Checking device registration state  ... Success
      Device registered successfully

      Checking primary NTP server [time.windows.com] ... Success

      Checking web proxy  ... NOT SET

      Checking primary IPv4 DNS server [10.222.118.154] ... Success
      Checking primary IPv6 DNS server  ... NOT SET
      Checking secondary IPv4 DNS server [10.222.120.24] ... Success
      Checking secondary IPv6 DNS server  ... NOT SET

      Checking device online  ... Success

      Checking device authentication  ... This will take a few minutes.
      Checking device authentication  ... Success

      Checking connectivity from device tooservice  ... This will take a few minutes.

      Checking connectivity from device tooservice  ... Success

      Checking connectivity from service toodevice  ... Success

      Checking connectivity tooMicrosoft Update servers  ... Success
      Controller1>

**Örnek çıktı – çevrimdışı cihaz** 

Bu örnek durumuna sahip bir aygıttan olan **çevrimdışı** hello Azure Portalı'nda.

     Checking device registrationstate: Success
     Device is registered successfully
     Checking connectivity from device tooSaaS.. Failure

Merhaba aygıt hello geçerli web proxy yapılandırması'nı kullanarak bağlanamadı. Bu hello web proxy yapılandırması ile ilgili bir sorunu veya bir ağ bağlantısı sorunu olabilir. Bu durumda, web proxy ayarlarının doğru olduğundan ve web proxy sunucularınızın çevrimiçi ve erişilebilir olduğundan emin olmanız gerekir.

## <a name="troubleshoot-with-hello-sync-hcstime-cmdlet"></a>Merhaba eşitleme HcsTime cmdlet ile ilgili sorunları giderme
Bu cmdlet toodisplay hello aygıt zaman kullanın. Merhaba aygıt zaman hello NTP sunucusu ile bir uzaklık varsa, daha sonra Bu cmdlet'i tooforce kullanabilirsiniz-başlangıç saati, NTP sunucusu ile eşitleme.
- Başlangıç uzaklığı hello aygıt NTP sunucusu arasındaki 5 dakikadan daha büyükse bir uyarı görürsünüz. 
- Başlangıç uzaklığı 15 dakika aşarsa hello aygıt çevrimdışı olarak geçer. Bu cmdlet tooforce bir saat eşitlemesi kullanmaya devam edebilirsiniz. 
- Ancak, hello uzaklığı 15 saat aşarsa, ardından mümkün tooforce eşitleme başlangıç zamanı olmaz ve bir hata iletisi gösterilir.

**Örnek çıktı – eşitleme HcsTime kullanarak zorlanmış zaman eşitleme**

     Controller0>Sync-HcsTime
     hello current device time is 4/24/2015 4:05:40 PM UTC.

     Time difference between NTP server and appliance is 00.0824069 seconds. Do you want tooresync time with NTP server?
     [Y] Yes [N] No (Default is "Y"): Y
     Controller0>

## <a name="troubleshoot-with-hello-enable-hcsping-and-disable-hcsping-cmdlets"></a>Merhaba HcsPing etkinleştirme ve devre dışı bırakma HcsPing cmdlet'lerle ilgili sorunları giderme
Merhaba ağ arabirimleri, Cihazınızda tooICMP ping isteklerine yanıt bu cmdlet'leri tooensure kullanın. Varsayılan olarak, hello StorSimple ağ arabirimleri tooping istekleri yanıt vermez. Cihazınızı çevrimiçi ve erişilebilir ise bu cmdlet kullanılarak hello en kolay yolu tooknow olur.

**Örnek çıktı – HcsPing etkinleştirme ve devre dışı bırakma HcsPing**

     Controller0>
     Controller0>Enable-HcsPing
     Successfully enabled ping.
     Controller0>
     Controller0>
     Controller0>Disable-HcsPing
     Successfully disabled ping.
     Controller0>

## <a name="troubleshoot-with-hello-trace-hcsroute-cmdlet"></a>Merhaba izleme HcsRoute cmdlet ile ilgili sorunları giderme
Bu cmdlet, bir rota izleme aracı olarak kullanın. Paketleri tooeach yönlendirici hello yolu tooa son hedef sunucudaki bir süre boyunca gönderir ve her adımın döndürülen Karşılama paketleri göre sonuçları hesaplar. Merhaba cmdlet'i belirtilen herhangi bir yönlendiricide veya bağlantı paket kaybı hello derecesini gösterildiğinden hangi yönlendiriciler saptayabilirler veya bağlantıları ağ sorunlarına neden.

**Nasıl tootrace hello izleme HcsRoute sahip bir paket yolu gösteren bir örnek çıktı**

     Controller0>Trace-HcsRoute -Target 10.126.174.25

     Tracing route toocontoso.com [10.126.174.25]
     over a maximum of 30 hops:
       0  HCSNode0 [10.126.173.90]
       1  contoso.com [10.126.174.25]

     Computing statistics for 25 seconds...
                 Source tooHere   This Node/Link
     Hop  RTT    Lost/Sent = Pct  Lost/Sent = Pct  Address
       0                                           HCSNode0 [10.126.173.90]
                                     0/ 100 =  0%   |
       1    0ms     0/ 100 =  0%     0/ 100 =  0%  contoso.com
      [10.126.174.25]

     Trace complete.

## <a name="troubleshoot-with-hello-get-hcsroutingtable-cmdlet"></a>Merhaba Get-HcsRoutingTable cmdlet ile ilgili sorunları giderme
Bu cmdlet tooview hello yönlendirme tablosu StorSimple cihazınız için kullanın. Bir yönlendirme tablosu, veri paketlerinin Internet Protokolü (IP) ağ üzerinden yolculuk burada yönlendirilirsiniz belirlemenize yardımcı olabilir kurallar kümesidir.

Merhaba yönlendirme tablosu hello arabirimler gösterilir ve hello yollar veri toohello hello ağ geçidi belirtilen ağlar. Ayrıca, hello karar veren hello gerçekleştirilecek yolu tooreach belirli bir hedef için olan hello Yönlendirme ölçüsünü verir. Merhaba alt hello yönlendirme ölçüm, hello daha yüksek hello tercih.

Örneğin, 2 ağ arabirimleri, veri 2 ve veri 3, bağlı toohello Internet varsa. Merhaba yönlendirme ölçümleri veri 2 ve veri 3 için 15 ve 261 sırasıyla olduğunda hello alt yönlendirme ölçüye sahip veri 2 hello tercih edilen arabirim tooreach hello Internet kullanılan olur.

StorSimple Cihazınızda güncelleştirme 1 çalıştırıyorsanız, DATA 0 ağ arabirimindeki hello bulut trafiği için en yüksek öncelik hello sahiptir. Bu, hello bulut trafiği olsa bile diğer bulut etkin arabirimleri, 0 VERİLERİNE yönlendirilecektir anlamına gelir.

Merhaba çalıştırırsanız `Get-HcsRoutingTable` (hello) aşağıdaki örnekte gösterildiği gibi herhangi bir parametre hello cmdlet belirtmeden cmdlet IPv4 ve IPv6 yönlendirme tablolarını çıktı. Alternatif olarak, belirtebilirsiniz `Get-HcsRoutingTable -IPv4` veya `Get-HcsRoutingTable -IPv6` tooget ilgili bir yönlendirme tablosu.

      Controller0>
      Controller0>Get-HcsRoutingTable
      ===========================================================================
      Interface List
       14...00 50 cc 79 63 40 ......Intel(R) 82574L Gigabit Network Connection
       12...02 9a 0a 5b 98 1f ......Microsoft Failover Cluster Virtual Adapter
       13...28 18 78 bc 4b 85 ......HCS VNIC
        1...........................Software Loopback Interface 1
       21...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
       22...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #3
      ===========================================================================

      IPv4 Route Table
      ===========================================================================
      Active Routes:
      Network Destination        Netmask          Gateway       Interface  Metric
                0.0.0.0          0.0.0.0  192.168.111.100  192.168.111.101     15
              127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
              127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
        127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
            169.254.0.0      255.255.0.0         On-link     169.254.1.235    261
          169.254.1.235  255.255.255.255         On-link     169.254.1.235    261
        169.254.255.255  255.255.255.255         On-link     169.254.1.235    261
          192.168.111.0    255.255.255.0         On-link   192.168.111.101    266
        192.168.111.101  255.255.255.255         On-link   192.168.111.101    266
        192.168.111.255  255.255.255.255         On-link   192.168.111.101    266
              224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
              224.0.0.0        240.0.0.0         On-link     169.254.1.235    261
              224.0.0.0        240.0.0.0         On-link   192.168.111.101    266
        255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        255.255.255.255  255.255.255.255         On-link     169.254.1.235    261
        255.255.255.255  255.255.255.255         On-link   192.168.111.101    266
      ===========================================================================
      Persistent Routes:
        Network Address          Netmask  Gateway Address  Metric
                0.0.0.0          0.0.0.0  192.168.111.100       5
      ===========================================================================

      IPv6 Route Table
      ===========================================================================
      Active Routes:
       If Metric Network Destination      Gateway
        1    306 ::1/128                  On-link
       13    276 fd99:4c5b:5525:d80b::/64 On-link
       13    276 fd99:4c5b:5525:d80b::1/128
                                          On-link
       13    276 fd99:4c5b:5525:d80b::3/128
                                          On-link
       13    276 fe80::/64                On-link
       12    261 fe80::/64                On-link
       13    276 fe80::17a:4eba:7c80:727f/128
                                          On-link
       12    261 fe80::fc97:1a53:e81a:3454/128
                                          On-link
        1    306 ff00::/8                 On-link
       13    276 ff00::/8                 On-link
       12    261 ff00::/8                 On-link
       14    266 ff00::/8                 On-link
      ===========================================================================
      Persistent Routes:
        None

      Controller0>

## <a name="step-by-step-storsimple-troubleshooting-example"></a>Adım adım StorSimple sorun giderme örneği
Merhaba aşağıdaki örnek StorSimple dağıtımı adım adım sorun giderme gösterir. Merhaba örnek senaryoda, cihaz kaydı bir hello ağ ayarlarını veya hello DNS adı yanlış olduğunu belirten hata iletisi ile başarısız olur.

döndürülen hello hata iletisi şudur:

     Invoke-HcsSetupWizard: An error has occurred while registering hello device. This could be due tooincorrect IP address or DNS name. Please check your network settings and try again. If hello problems persist, contact Microsoft Support.
     +CategoryInfo: Not specified
     +FullyQualifiedErrorID: CiSClientCommunicationErros, Microsoft.HCS.Management.PowerShell.Cmdlets.InvokeHcsSetupWizardCommand

Merhaba hata hello aşağıdakilerden birini nedeni olabilir:

* Yanlış donanım yükleme
* Hatalı ağ arabirimi
* Hatalı IP adresi, alt ağ maskesi, ağ geçidi, birincil DNS sunucusu veya web proxy
* Hatalı kayıt anahtarı
* Yanlış güvenlik duvarı ayarları

### <a name="toolocate-and-fix-hello-device-registration-problem"></a>Merhaba cihaz kayıt sorunu toolocate ve düzeltme
1. Cihaz yapılandırmanızı denetleyin: hello etkin denetleyicisinde çalıştırın `Invoke-HcsSetupWizard`.
   
   > [!NOTE]
   > Merhaba etkin denetleyicisinde Hello Kurulum Sihirbazı'nı çalıştırmanız gerekir. bağlı toohello etkin denetleyicisi hello seri konsolunda sunulan hello başlık bakma olduğunuz tooverify. Merhaba başlık bağlı toocontroller 0 veya 1 denetleyicisi olup ve hello denetleyicisi etkin veya Pasif olduğunu gösterir. Daha fazla bilgi için çok Git[Cihazınızı etkin bir denetleyicisindeki tanımlamak](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device).
   
2. Merhaba aygıtın düzgün kablolu emin olun: hello ağ geri düzlemi hello aygıtta kablo kontrol edin. Merhaba kablo belirli toohello aygıt modelidir. Daha fazla bilgi için çok Git[StorSimple 8100 cihazınız yüklemek](storsimple-8100-hardware-installation.md) veya [StorSimple 8600 model Cihazınızı yüklemek](storsimple-8600-hardware-installation.md).
   
   > [!NOTE]
   > 10 GbE ağ bağlantı noktası kullanıyorsanız, QSFP SFP bağdaştırıcısı ve SFP kablolar sağlanan toouse hello gerekir. Daha fazla bilgi için bkz: Merhaba [kablo, anahtarlar ve hello 10 GbE bağlantı noktaları için önerilen ileticileri listesi](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
  
3. Merhaba ağ arabirimi Hello durumunu doğrulayın:
   
   * Merhaba Get-NetAdapter cmdlet'i toodetect hello durumunu hello ağ arabirimleri için veri 0 kullanın. 
   * Merhaba bağlantı çalışmıyorsa hello **ifındex** durum, bu hello arabirimidir aşağı olmadığını gösterir. Ardından hello bağlantı noktası toohello Gereci ve toohello anahtar toocheck hello ağ bağlantısı gerekir. Hatalı kabloları çıkışı toorule de gerekir. 
   * Bu başlangıç bağlantı noktası hello etkin denetleyicisinde başarısız oldu veri 0 şüpheleniyorsanız, bu bağlanarak onaylayabilirsiniz toohello veri 0 denetleyicisi 1 bağlantı noktası. tooconfirm Bu, denetleyici 0 hello aygıttan arkasına hello gelen hello ağ kablosunu hello kablo toocontroller 1 bağlanmak ve hello Get-NetAdapter cmdlet'i yeniden çalıştırın.
     Veri başarısız olursa bir denetleyicisinde bağlantı noktası 0 hello [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) sonraki adımlar için. Sisteminizde tooreplace hello denetleyicisi gerekebilir.
4. Merhaba bağlantı toohello anahtar doğrulayın:
   
   * Veri 0 ağ arabirimlerindeki denetleyici 0 ve denetleyici 1, birincil muhafazada hello üzerinde olduğundan emin olun aynı alt ağ. 
   * Merhaba hub veya yönlendirici denetleyin. Genellikle, her iki denetleyicileri toohello bağlanmalısınız aynı hub veya yönlendirici. 
   * Hello anahtarları hello bağlantı için kullandığınız her iki denetleyicilerinin hello için veri 0 sahip olduğunuzdan emin olun aynı vLAN.
5. Kullanıcı hataları kaldırın:
   
   * Merhaba Kurulum Sihirbazı'nı yeniden çalıştırın (çalıştırma **Invoke-HcsSetupWizard**) ve girin hello değerleri yeniden toomake hiçbir hata bulunmadığından emin. 
   * Merhaba kayıt doğrulayın kullanılan anahtarı. Merhaba aynı kayıt anahtarı kullanılan tooconnect birden çok aygıtları tooa StorSimple cihaz Yöneticisi hizmeti olabilir. Merhaba yordamı kullanın [hello hizmet kayıt anahtarını Al](storsimple-8000-manage-service.md#get-the-service-registration-key) kullanmakta olduğunuz tooensure hello doğru kayıt anahtarı.
     
     > [!IMPORTANT]
     > Çalıştıran birden çok hizmetleriniz varsa, kullanılan tooregister hello aygıt hello uygun hizmet için tooensure bu hello kayıt anahtarı gerekir. Merhaba yanlış StorSimple cihaz Yöneticisi hizmeti ile bir cihazı kaydettiyseniz, çok gerekir[Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) sonraki adımlar için. (Veri kaybına neden olabilir) hello cihazı fabrika ayarlarına tooperform olabilir toothen connect, hedeflenen toohello hizmeti.
     > 
     > 
6. Ağ dışından bağlantı toohello sahip hello Bağlantıyı Sına cmdlet tooverify kullanın. Daha fazla bilgi için çok Git[hello Bağlantıyı Sına cmdlet ile ilgili sorunları giderme](#troubleshoot-with-the-test-connection-cmdlet).
7. Güvenlik Duvarı Engelleme denetleyin. Bu hello sanal doğruladıysanız IP (VIP), alt ağ, ağ geçidi ve DNS ayarları doğru ve bağlantı sorunları görmeye devam sonra güvenlik duvarı, cihaz ve ağ dışından hello arasındaki iletişimi engelliyor olabilir. StorSimple Cihazınızda giden iletişim için 80 ve 443 numaralı bağlantı noktalarını kullanılabilir olmasını tooensure gerekir. Daha fazla bilgi için bkz: [StorSimple cihazınız için ağ gereksinimleri](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device).
8. Merhaba günlüklerine bakın. Çok Git[desteği paketleri ve cihaz günlükleri kullanılabilir sorun giderme için](#support-packages-and-device-logs-available-for-troubleshooting).
9. Merhaba önceki adımları hello sorunu çözmezse [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) Yardım için.

## <a name="next-steps"></a>Sonraki adımlar
[Nasıl toouse hello Tanılama Aracı tootroubleshoot StorSimple cihazını öğrenin](storsimple-8000-diagnostics.md).

<!--Link references-->

[1]: https://technet.microsoft.com/library/dd379547(v=ws.10).aspx
[2]: https://technet.microsoft.com/library/dd392266(v=ws.10).aspx 
