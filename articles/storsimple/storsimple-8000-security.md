---
title: "aaaStorSimple 8000 serisi güvenlik | Microsoft Docs"
description: "Merhaba güvenlik ve StorSimple hizmeti, cihaz ve şirket içinde ve hello bulut veri koruma gizlilik özellikleri açıklar."
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
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 48dd449d2908c21fe05d0ed37a4dc6f3e306e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-security-and-data-protection"></a>StorSimple güvenlik ve veri koruması

## <a name="overview"></a>Genel Bakış

Güvenlik herkes hello teknolojisi gizli veya özel verilerle özellikle kullanıldığında, yeni bir teknoloji benimsenmesi için önemli bir konudur. Farklı teknolojiler değerlendirirken, daha yüksek riskleri ve veri koruması maliyetlerini dikkate almanız gerekir. Microsoft Azure StorSimple bir güvenlik ve gizlilik çözüm veri koruması için tooensure yardımcı sağlar:

* **Gizlilik** – yalnızca yetkili varlıklar verilerinizi görüntüleyebilirsiniz.
* **Bütünlük** – yalnızca yetkili varlıklar değiştirebilir veya verilerinizi silebilirsiniz.

Merhaba Microsoft Azure StorSimple çözümünüzle birbiriyle etkileşimde dört ana bileşenden oluşur:

* **Microsoft Azure üzerinde barındırılan StorSimple cihaz Yöneticisi hizmeti** – tooconfigure ve sağlama kullanmak hello yönetim hizmeti hello StorSimple cihazı.
* **StorSimple cihazı** –, veri merkezinizde yüklü fiziksel bir cihaz. Tüm ana bilgisayarlar ve verileri oluşturmak istemciler toohello StorSimple cihazı bağlayın ve hello aygıt hello verileri yöneten ve toohello Azure bulut taşır uygun şekilde.
* **İstemcileri/ana bağlı toohello aygıt** – hello altyapınızdaki toohello StorSimple cihazı bağlanan istemciler ve korumalı toobe gereken verileri oluşturabilir.
* **Bulut depolama** – hello hello Azure bulut verilerinin depolandığı konum.

Merhaba aşağıdaki bölümlerde her bu bileşenleri ve bunlar üzerinde depolanan hello verilerin korunmasına yardımcı olma hello StorSimple güvenlik özellikleri açıklanmaktadır. Ayrıca, Microsoft Azure StorSimple güvenliği ve hello yanıtlarını ilgili olabilecek soruların listesini içerir.

## <a name="storsimple-device-manager-service-protection"></a>StorSimple cihaz Yöneticisi hizmeti koruma

Merhaba StorSimple cihaz Yöneticisi hizmeti, bir yönetim hizmeti Microsoft Azure üzerinde barındırılan ve kuruluşunuzun temin tüm StorSimple cihazlar toomanage kullanılan ' dir. Merhaba StorSimple cihaz Yöneticisi hizmeti, kuruluş kimlik bilgilerini toolog toohello bir web tarayıcısı aracılığıyla Azure portal kullanarak erişebilirsiniz.

Erişim toohello StorSimple cihaz Yöneticisi hizmeti, kuruluşunuz StorSimple içeren bir Azure aboneliği sahip olmasını gerektirir. Aboneliğinizi hello Azure portalına erişebilir hello özellikleri yönetir. Kuruluşunuzun bir Azure aboneliğine sahip değil ve bunlarla ilgili daha fazla toolearn istiyorsanız, bkz [Azure'a kuruluş olarak kaydolma](../active-directory/sign-up-organization.md).

Azure'da Hello StorSimple cihaz Yöneticisi hizmeti barındırıldığından, hello Azure güvenlik özellikleri tarafından korunur. Microsoft Azure tarafından sağlanan hello güvenlik özellikleri hakkında daha fazla bilgi için toohello Git [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/security/).

## <a name="storsimple-device-protection"></a>StorSimple cihaz koruma

Merhaba StorSimple cihazı katı hal sürücüleri (SSD) ve sabit disk sürücülerinin (HDD'ler), yedek denetleyicileri ve otomatik yük devretme yetenekleri ile birlikte içeren bir şirket içi karma depolama aygıttır. Merhaba denetleyicileri katmanlama, şu anda kullanılan (veya sık kullanılan) verileri yerel depolama (Merhaba StorSimple cihazı veya şirket içi sunucuları) üzerinde daha az sık kullanılan veri toohello bulut taşırken yerleştirme depolama yönetin.

Yalnızca StorSimple cihazları toojoin hello Azure aboneliğinizde oluşturduğunuz StorSimple cihaz Yöneticisi hizmeti izin verilen yetkili. tooauthorize bir aygıt, onu hello StorSimple cihaz Yöneticisi hizmeti ile Merhaba hizmet kayıt anahtarı sağlayarak kaydetmeniz gerekir. Merhaba hizmet kayıt anahtarını hello Azure portalında oluşturulan bir 128-bit rastgele anahtardır.

![Hizmet kayıt anahtarı](./media/storsimple-security/ServiceRegistrationKey.png)

toolearn nereden hizmet kayıt anahtarı, Git çok[2. adım: hello hizmet kayıt anahtarını Al](storsimple-8000-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).

Merhaba hizmet kayıt anahtarını 100 + karakterler içeren uzun bir anahtardır. Başlangıç anahtarı kopyalayın ve böylece tooauthorize ek cihazları gerektiği şekilde kullanılabilmesi için güvenli bir konumda metin dosyasına kaydedin. İlk aygıtınızı kaydettikten sonra hello hizmet kayıt anahtarını kaybolursa, StorSimple cihaz Yöneticisi hizmeti hello yeni bir anahtar oluşturabilirsiniz. Bu, var olan cihazların Merhaba işlemini etkilemez.

Bir cihaz kaydedildikten sonra Microsoft Azure ile belirteçleri toocommunicate kullanır. Merhaba hizmet kayıt anahtarı, cihaz kaydından sonra kullanılmaz.

> [!NOTE]
> Her kullanıldıktan sonra hello hizmet kayıt anahtarını yeniden oluşturmak öneririz.


## <a name="protect-your-storsimple-solution-via-passwords"></a>StorSimple çözümünüzün parolaları aracılığıyla koruma

Parolalar bilgisayar güvenlik önemli bir özelliği olan ve yaygın olarak kullanılan hello StorSimple çözümde toohelp verilerinizi yalnızca erişilebilir tooauthorized kullanıcılar olduğundan emin olun. StorSimple parolalarını aşağıdaki tooconfigure hello sağlar:

* StorSimple cihaz Yöneticisi parolası
* Kimlik Doğrulama Protokolü (CHAP) başlatıcı ve hedef parolaları sınama
* StorSimple Snapshot Manager parolası

### <a name="windows-powershell-for-storsimple-and-hello-storsimple-device-administrator-password"></a>StorSimple ve hello StorSimple cihaz Yöneticisi parolası için Windows PowerShell

StorSimple için Windows PowerShell toomanage hello StorSimple cihazı kullanabileceğiniz komut satırı arabirimidir. StorSimple için Windows PowerShell tooregister olanak tanıyan özellikler Cihazınızı olduğundan, Cihazınızda hello ağ arabirimi yapılandırmak, belirli türden güncelleştirmeler yüklemeniz, Cihazınızı hello destek oturum erişerek sorun giderme ve hello cihaz durumunu değiştir . StorSimple için Windows PowerShell hello aygıtta bağlanan toohello seri konsolu veya Windows PowerShell uzaktan iletişimini kullanarak erişebilirsiniz.

PowerShell uzaktan iletişimini HTTPS veya HTTP üzerinden yapılabilir. HTTPS üzerinden uzaktan yönetim etkinleştirilmiş olsa toodownload hello uzaktan yönetimi gerekir sertifika hello aygıttan ve hello uzak istemciye yükleyin. PowerShell uzaktan iletişimi hakkında daha fazla bilgi için çok Git[tooyour StorSimple cihazı uzaktan bağlanmak](storsimple-8000-remote-connect.md).

StorSimple tooconnect toohello aygıt için Windows PowerShell kullandıktan sonra tooprovide hello cihaz Yöneticisi parolası toolog toohello aygıtta gerekir.

![Cihaz yöneticisi parolası](./media/storsimple-security/DeviceAdminPW.png)

Aklınızda en iyi uygulamaları izleyerek hello tutun:

* Uzaktan Yönetim varsayılan olarak kapalıdır. Merhaba StorSimple cihaz Yöneticisi hizmeti tooenable kullanabilirsiniz. En iyi güvenlik uygulaması olarak uzaktan erişim, başlangıç sırasında yalnızca gerçekten gerekli süre etkin olması.
* Merhaba parolayı değiştirirseniz, emin toonotify beklenmedik bağlantı kaybı yaşanmaz tüm uzaktan erişim kullanıcıları olması.
* Merhaba StorSimple cihaz Yöneticisi hizmeti, var olan parolaların alınamıyor: Bu yalnızca bunları sıfırlayabilirsiniz. Onu unutulursa, tooreset bir parolaya sahip değil, tüm parolaların güvenli bir yerde depolamanız önerilir. Tooreset parola gerekiyorsa, parolanızı sıfırlamanız önce emin toonotify tüm kullanıcıların olması.

Bir seri bağlantı toohello aygıtı kullanarak hello Windows PowerShell arabirimi erişebilir. Ayrıca, uzaktan HTTP veya ek güvenlik sağlayan HTTPS kullanarak erişebilirsiniz. HTTPS seri ya da HTTP bağlantısı değerinden daha yüksek düzeyde güvenlik sağlar. Ancak, toouse HTTPS, önce bir sertifika hello aygıt erişecek hello istemci bilgisayara yüklemeniz gerekir. Merhaba StorSimple cihaz Yöneticisi hizmeti hello cihaz yapılandırma sayfasında hello uzaktan erişim sertifikası yükleyebilir. Uzaktan erişim için Hello sertifika kaybolursa, yeni bir sertifika indirin ve yetkili toouse uzaktan yönetimi tooall istemciler yayar.

### <a name="challenge-handshake-authentication-protocol-chap-initiator-and-target-passwords"></a>Kimlik Doğrulama Protokolü (CHAP) başlatıcı ve hedef parolaları sınama

CHAP, StorSimple cihaz toovalidate hello uzak istemcilerin kimliğini hello tarafından kullanılan bir kimlik doğrulama düzenidir. Merhaba doğrulama bir paylaşılan parolasını temel alır. CHAP tek yönlü olabilir (tek yönlü) veya karşılıklı (çift yönlü). Tek yönlü CHAP ile Merhaba hedef (Merhaba StorSimple cihaz) Başlatıcı (ana bilgisayar) kimliğini doğrular. Karşılıklı veya ters CHAP hello hedef hello Başlatıcı kimlik doğrulaması ve hello Başlatıcı hello hedef sonra kimlik doğrulaması gerektirir. StorSimple yapılandırılmış toouse ya da bir yöntem olabilir.

CHAP yapılandırdığınızda hello aşağıdakilere dikkat edin:

* Merhaba CHAP kullanıcı adı 233'den az karakter içermelidir.
* Merhaba CHAP parolası 12 ile 16 arasında karakter olması gerekir. Toouse çalışırken daha uzun bir kullanıcı adı ve parola kimlik doğrulama hatası hello Windows ana bilgisayarda neden olur.
* Merhaba kullanamazsınız hello CHAP başlatıcı ve hello CHAP hedefi için aynı parolayı.
* Merhaba parola ayarladıktan sonra onu değiştirilebilir ancak geri alınamaz. Merhaba parolası değiştirilirse, toohello StorSimple cihazı başarıyla bağlanabilmesi emin toonotify tüm uzaktan erişim kullanıcıları olabilir.

CHAP hakkında daha fazla bilgi ve nasıl tooconfigure StorSimple çözümünüz için çok[StorSimple cihazınız için CHAP yapılandırma](storsimple-8000-configure-chap.md).

### <a name="storsimple-snapshot-manager-password"></a>StorSimple Snapshot Manager parolası

StorSimple Snapshot Manager birim grupları ve hello Windows birim gölge kopyası hizmeti toogenerate uygulamayla tutarlı yedeklemeler kullanan bir Microsoft Yönetim Konsolu (MMC) ek bileşenidir. Ayrıca, StorSimple Snapshot Manager toocreate yedekleme zamanlamaları ve kopya kullanın veya birimleri geri yükleyebilirsiniz.

Bir aygıt toouse StorSimple Snapshot Manager yapılandırırken, gerekli tooprovide hello StorSimple Snapshot Manager parolası olacaktır. Bu parola ilk Windows PowerShell'de StorSimple için kayıt sırasında ayarlanır. Merhaba parola ayrıca ayarlayın ve StorSimple cihaz Yöneticisi hizmeti hello değiştirildi. Bu parolayı hello cihazı ile StorSimple Snapshot Manager kimliğini doğrular.

![StorSimple Snapshot Manager parolası](./media/storsimple-security/SnapshotMgrPassword.png)

Merhaba StorSimple Snapshot Manager parolası 14 too15 karakter olmalıdır ve 3 veya daha büyük harf, küçük harfler, sayısal ve özel karakter bir bileşimi içermesi gerekir. Merhaba StorSimple Snapshot Manager parolası ayarladıktan sonra onu değiştirilebilir ancak geri alınamaz. Merhaba parolayı değiştirirseniz, tüm uzak kullanıcılar emin toonotify olabilir.

StorSimple anlık görüntü Yöneticisi hakkında daha fazla bilgi için çok Git[StorSimple anlık görüntü Yöneticisi nedir?](storsimple-what-is-snapshot-manager.md)

### <a name="password-best-practices"></a>Parola en iyi uygulamalar

Merhaba aşağıdaki kullanmanızı öneririz yönergeleri toohelp StorSimple parolalarını güçlü ve iyi korumalı olduğundan emin olun:

* Parolalarınızı üç ayda değiştirin. Merhaba parolaları değiştirme yıllık zorlanır.
* Güçlü parolalar kullanın. Daha fazla bilgi için çok Git[güçlü parolalar oluşturma ve bunları korumak](http://blogs.microsoft.com/cybertrust/2014/08/25/create-stronger-passwords-and-protect-them/).
* Her zaman için farklı erişim düzenekler farklı parolalar kullanın; Her belirttiğiniz hello parolaların benzersiz olmalıdır.
* Parolalar değil yetkili tooaccess hello StorSimple cihazı olan kimseyle paylaşmayın.
* Bir parola başkalarının önünde hakkında konuşurken değil veya parola hello biçiminde ipucu.
* Bir hesap veya parola aşılmış şüpheleniyorsanız hello olay tooyour bilgi güvenliği bölümü bildirin.
* Tüm parolaları hassas, gizli bilgi kabul eder. 

## <a name="storsimple-data-protection"></a>StorSimple veri koruması

Bu bölümde Aktarımdaki verileri ve depolanan verilerin korunmasına hello StorSimple güvenlik özellikleri açıklanmaktadır.

Diğer bölümlerinde açıklandığı gibi parolalar kullanılan tooauthorize olan ve erişim tooyour StorSimple çözümü kazanmadan önce kullanıcıların kimlik doğrulaması. Depolama sistemleri arasında ve onu depolandığı sürece aktarıldığı sırada başka bir güvenlik önlemleri yetkisiz kullanıcılardan veri koruyor. Merhaba aşağıdaki bölümlerde StorSimple ile sağlanan hello veri koruma özellikleri açıklanmaktadır.

> [!NOTE]
> Yinelenenleri kaldırma hello StorSimple cihazı ve Microsoft Azure depolama alanında depolanan veriler için ek koruma sağlar. Veri yinelenenler kaldırılmadığında hello veri nesneleri hello kullanılan meta verileri toomap ayrı olarak depolanır ve bunlara erişim: birim yapısına, dosya sistemi veya dosya adı göre kullanılabilir depolama düzeyi bağlam tooreconstruct hello verisi yok.


## <a name="protect-data-flowing-through-hello-service"></a>Merhaba hizmeti aracılığıyla akan verileri koruma

Merhaba birincil amacı hello StorSimple cihaz Yöneticisi hizmeti, toomanage olan ve hello StorSimple cihazı yapılandırın. Microsoft Azure'da Hello StorSimple cihaz Yöneticisi hizmeti çalışır. Hello Azure portal tooenter aygıt yapılandırma verilerini kullanın ve ardından Microsoft Azure hello StorSimple cihaz Yöneticisi hizmeti toosend hello veri toohello cihazı kullanır. Saklı bilgi asimetrik anahtar çiftlerini toohelp bir sistem olun hello Azure hizmeti güvenliğinin aşılmasına oluşturmayacaktır StorSimple kullanır.

![Yürütülen veri şifrelemesi](./media/storsimple-security/DataEncryption.png)

Merhaba asimetrik anahtar sistem hello hizmeti aracılığıyla şu şekilde akar hello verilerin korunmasına yardımcı olur:

1. Asimetrik ortak ve özel anahtar çifti kullanan bir veri şifreleme sertifikası hello cihazda oluşturulması ve kullanılan tooprotect hello veriler. Merhaba ilk cihaz kaydedildiğinde hello anahtarları oluşturulur.
2. Merhaba veri şifreleme sertifikası anahtarları tarafından hello ilk cihaz kaydı sırasında rastgele oluşturulan güçlü bir 128-bit anahtar hello hizmet verileri şifreleme anahtarı tarafından korunan bir kişisel bilgi değişimi (.pfx) dosyasına dışarı aktarılır.
3. Merhaba sertifikanın ortak anahtarının Hello kullanılabilir toohello StorSimple cihaz Yöneticisi hizmeti güvenli bir şekilde yapılır ve hello özel anahtarı hello aygıtla kalır.
4. Ortak anahtarı girme hello hizmeti kullanılarak şifrelenen veriler hello ve hello cihazda depolanan hello özel anahtarını kullanarak şifresi, o hello Azure hizmet sağlama toohello aygıt akan hello verilerin şifresini çözemez.

aygıtta hello hizmetine kayıtlı yalnızca hello ilk Hello hizmet verileri şifreleme anahtarı oluşturulur. Merhaba hizmetine kayıtlı tüm sonraki cihazlar hello kullanmalısınız aynı hizmet verileri şifreleme anahtarı.

> [!IMPORTANT]
> Çok önemli toomake hello hizmet verileri şifreleme anahtarı bir kopyasıdır ve güvenli bir konuma kaydedin. Merhaba hizmet verileri şifreleme anahtarı bir kopyasını bir yetkili kişi tarafından erişilebilir ve kolayca iletildiğinden toohello aygıt yönetici olabilir bir şekilde depolanması gerekir.
> 
> Microsoft Destek ekibiyle Hello hizmet verileri şifreleme anahtarı kaybolursa, çevrimiçi bir durumda en az bir aygıt sahip sağlanan tooretrieve yardımcı olabilir. Bunu alındıktan sonra hello hizmet verileri şifreleme anahtarı değiştirmenizi öneririz. Yönergeler için çok gidin[değişiklik hello hizmet verileri şifreleme anahtarı](storsimple-service-dashboard.md#change-the-service-data-encryption-key).

Merhaba seçerek hello hizmet verileri şifreleme anahtarı ve hello karşılık gelen veri şifreleme sertifikasını değiştirebilirsiniz **değişiklik hizmeti veri şifreleme anahtarı** hello hizmet panosunu seçeneği. veri güvenliği tehlikeye tooensure, bir fiziksel StorSimple cihazı toochange hello hizmet verileri şifreleme anahtarı kullanmanız gerekir. Merhaba şifreleme anahtarları değiştirilmesi tüm cihazlar hello yeni anahtarla güncelleştirilmesini gerektirir. Bu nedenle, tüm cihazlar çevrimiçi olduğunda hello anahtar değiştirmenizi öneririz. Cihaz çevrimdışı ise, kendi anahtarları farklı bir zamanda değiştirilebilir. Hello cihazları güncel anahtarlarla mümkün toorun yedeklemeler olmaya devam eder, ancak hello anahtar güncelleştirilene kadar bunlar mümkün toorestore veri olmaz. Daha fazla bilgi için çok Git[kullanım hello StorSimple Aygıt Yöneticisi'ni hizmet panosunu](storsimple-8000-service-dashboard.md).

Merhaba hizmet verileri şifreleme anahtarı ve hello veri şifreleme sertifikasını süresi dolmaz. Ancak, hello hizmet verileri şifreleme değiştirmenizi öneririz anahtar yıllık toohelp önlemek anahtar güvenliğinin aşılması.

## <a name="protect-data-at-rest"></a>Rest verileri koruma

Merhaba StorSimple cihazı, katmanlarda yerel olarak ve kullanım sıklığı bağlı olarak hello bulutta depolayarak veri yönetir. Tüm uygun şekilde veri toohello bulut taşır bağlı toohello aygıt gönderme veri toohello cihazı makineleri barındırır. Veri hello aygıt toohello buluttan güvenli bir şekilde hello Internet aktarılır. Her bir cihaz tüm paylaşılan birimler aygıtta ortaya çıkarır bir iSCSI hedefi vardır. Tüm verileri toocloud depolama gönderilmeden önce şifrelenir. 

![Bulut depolama şifreleme anahtarı](./media/storsimple-security/CloudStorageEncryption.png)

toohelp hello güvenlik sağlamak ve veri bütünlüğünü toohello bulut taşınmış, StorSimple toodefine bulut depolama şifreleme anahtarları gibi sağlar:

* Birim kapsayıcısı oluşturduğunuzda hello bulut depolama şifreleme anahtarı belirtin. başlangıç anahtarı değiştirilemiyor veya daha sonra eklenebilir.
* Tüm birimlerin bir birim kapsayıcısı paylaşımda aynı şifreleme anahtarını hello. Farklı bir form belirli bir birimin şifreleme istiyorsanız, o birim yeni bir birim kapsayıcısı toohost oluşturmanızı öneririz.
* Merhaba StorSimple cihaz Yöneticisi hizmeti hello bulut depolama şifreleme anahtarı girdiğinizde hello anahtarı hello ortak kısmını hello hizmet verileri şifreleme anahtarı kullanarak ve toohello aygıt gönderilen şifrelenir.
* Hello bulut depolama şifreleme anahtarı herhangi bir yere hello hizmetinde depolanmaz ve yalnızca toohello cihaz denir.
* Bir bulut depolama şifreleme anahtarı belirtmek isteğe bağlıdır. Merhaba konak toohello aygıt şifrelenmiş veriler gönderebilir.

### <a name="additional-security-best-practices"></a>Ek güvenlik en iyi uygulamalar

* Trafik bölünmesi: Kurumsal bir ağda kullanıcı trafiğinden, iSCSI SAN tamamen ayrı bir ağ dağıtımı ve burada fiziksel yalıtım bir seçenek değildir VLAN'ları kullanarak yalıtmak. İSCSI depolama için ayrılmış bir ağ hello güvenliği ve iş açısından kritik verilerinizi performansını garanti. Kurumsal bir LAN üzerinden depolama ve kullanıcı trafiği karıştırma önerilmez ve gecikme süresini artırmak ve ağ hatalarına neden.
* Konak tarafındaki ağ güvenliği için TCP/IP'yi aktarım motoru (TOE) destekleyen ağ arabirimleri kullanın. TOE hello ağ bağdaştırıcısında TCP işleyerek CPU yükünü azaltır.

## <a name="protect-data-via-storage-accounts"></a>Depolama hesapları üzerinden veri koruma

Her bir Microsoft Azure aboneliği bir veya daha fazla depolama hesabı oluşturabilirsiniz. (Bir depolama hesabı benzersiz bir ad alanı hello Azure bulut depolanan verilerle çalışmak için sağlar.) Erişim tooa depolama hesabı, bu depolama hesabıyla ilişkili hello abonelik ve erişim anahtarları tarafından denetlenir.

Bir depolama hesabı oluşturduğunuzda, Microsoft Azure hello StorSimple cihazı hello depolama hesabı eriştiğinde biri kimlik doğrulaması için kullanılan iki 512 bit depolama erişim tuşu oluşturur. Bu anahtarlar yalnızca biri kullanımda olduğunu unutmayın. Merhaba başka bir anahtar, toorotate hello anahtarları düzenli aralıklarla izin vererek yedekte tutulur. toorotate anahtarları hello ikincil anahtarı etkin ve silme hello birincil anahtar olun. Daha sonra hello sonraki döndürme sırasında kullanmak için yeni bir anahtar oluşturabilirsiniz. (Güvenlik nedeniyle, birçok veri merkezleri anahtar döndürme gerektirir.)

Bu anahtar döndürme için en iyi uygulamaları izlemeniz önerilir:

* Toohelp olun depolama hesabınıza yetkisiz kullanıcılar tarafından erişilmez depolama hesabı anahtarlarını düzenli olarak döndürme.
* Düzenli aralıklarla Azure yöneticinize değiştirin veya bu hello Azure portal toodirectly erişim hello depolama hesabı hello depolama bölümünü kullanarak hello birincil veya ikincil anahtarı yeniden gerekir.

## <a name="protect-data-via-encryption"></a>Veri şifreleme aracılığıyla koruma

StorSimple tooprotect veri depolanan şifreleme algoritmalarını aşağıdaki veya StorSimple çözümünüzün hello bileşenler arasında seyahat hello kullanır.

| Algoritması | Anahtar uzunluğu | Uygulamalar/protokolleri/açıklamaları |
| --- | --- | --- |
| RSA |2048 |RSA PKCS 1 v1.5 toohello aygıt gönderilen Azure portal tooencrypt yapılandırma verilerini hello tarafından kullanılır: Örneğin, depolama hesabının kimlik bilgilerini, StorSimple cihazı yapılandırma ve bulut depolama şifreleme anahtarları. |
| AES |256 |Merhaba StorSimple aygıttan toohello Azure portal gönderilmeden önce AES CBC ile kullanılan tooencrypt hello ortak hello hizmet verileri şifreleme anahtarı bölümüdür. Merhaba veri toohello bulut depolama hesabı gönderilmeden önce de hello StorSimple cihaz tooencrypt verileri tarafından kullanılır. |

## <a name="storsimple-cloud-appliance-security"></a>StorSimple bulut uygulaması güvenliği

[!INCLUDE [storsimple Cloud Appliance security](../../includes/storsimple-virtual-device-security.md)]

## <a name="frequently-asked-questions-faq"></a>Sık sorulan sorular (SSS)

Bazı hakkında sorular ve yanıtlar güvenlik ve Microsoft Azure StorSimple Hello aşağıda verilmiştir.

**S:** Hizmetim tehlikeye. Ne sonraki adımlarım olması gerekiyor mu?

**Y:** hello hizmet verileri şifreleme anahtarı ve hello depolama hesabı anahtarlarını katmanlama veriler için kullanılan hello depolama hesabı için hemen değiştirmelisiniz. Yönergeler için aşağıdaki adrese gidin:

* [Değişiklik hello hizmet verileri şifreleme anahtarı](storsimple-service-dashboard.md#change-the-service-data-encryption-key)
* [Depolama hesaplarının anahtar döndürme](storsimple-8000-manage-storage-accounts.md#key-rotation-of-storage-accounts)

**S:** hello hizmet kayıt anahtarı için soran yeni bir StorSimple cihazı vardır. Bunu nasıl aldığını?

**Y:** hello StorSimple cihaz Yöneticisi hizmeti ilk oluşturduğunuzda bu anahtarı oluşturuldu. Merhaba StorSimple cihaz Yöneticisi hizmeti tooconnect toohello cihaz kullandığınızda, hello hizmet hızlı başlangıç sayfası tooview veya yeniden oluşturma hello hizmet kayıt anahtarını kullanabilirsiniz. Yeni bir hizmet kayıt anahtarı oluşturma hello var olan kayıtlı cihazları etkilemez. Yönergeler için aşağıdaki adrese gidin:

* [Görüntülemek veya hello hizmet kayıt anahtarını yeniden oluşturma](storsimple-8000-manage-service.md##regenerate-the-service-registration-key)

**S:** my hizmet verileri şifreleme anahtarı kaybolur. Ne yapmalıyım?

**Y:** Microsoft Destek'e başvurun. Cihaz ve Yardım (en az bir aygıt çevrimiçi olması koşuluyla) başlangıç anahtarı alıp tooa destek oturumunda kaydedebilirsiniz. Merhaba hizmet verileri şifreleme anahtarı edindikten sonra tooensure değiştirmelisiniz hemen hello yeni anahtara yalnızca tooyou denir. Yönergeler için aşağıdaki adrese gidin:

* [Değişiklik hello hizmet verileri şifreleme anahtarı](storsimple-service-dashboard.md#change-the-service-data-encryption-key)

**S:** ı bir hizmet verileri şifreleme anahtarı değişikliği için bir cihaz yetkili ancak hello anahtar değiştirme işlemi başlatılamadı. Ne yapmalıyım?

**Y:** hello zaman aşımı süresi sona erdi, tooreauthorize hello aygıt hello hizmet verileri şifreleme anahtarı değişikliği için ihtiyacınız ve hello işlemini yeniden başlatın.

**S:** hello hizmet verileri şifreleme anahtarı değiştirildi, ancak ı bırakamıyor tooupdate hello diğer cihazları 4 saat içinde. Toostart yeniden var mı?

**Y:** hello 4 saatlik süre olan hello değişiklik yalnızca başlatmaktan. Üzerinde hello güncelleştirme işlemini başlattıktan sonra hello StorSimple cihaz yetkili, tüm cihazlar güncelleştirilinceye kadar hello yetkilendirme geçerlidir.

**S:** Mız StorSimple Yöneticisi hello şirket sol. Ne yapmalıyım?

**Y:** değiştirme ve sıfırlama hello erişim toohello StorSimple cihazı izin ve hello hizmet verileri şifreleme anahtarı tooensure hello yeni bilgiler toounauthorized personel bilinmiyor değiştirme parolaları. Yönergeler için aşağıdaki adrese gidin:

* [Storsimple parolalarınızı Hello StorSimple cihaz Yöneticisi hizmeti toochange kullanın](storsimple-8000-change-passwords.md)
* [Değişiklik hello hizmet verileri şifreleme anahtarı](storsimple-service-dashboard.md#change-the-service-data-encryption-key)
* [StorSimple cihazınız için CHAP yapılandırma](storsimple-8000-configure-chap.md)

**S:** toohello StorSimple cihazı bağlanan tooprovide hello StorSimple Snapshot Manager parolası tooa konak istiyor, ancak hello parola kullanılabilir değil. Ne yapabilirim?

**Y:** hello parolanızı unuttuysanız, yeni bir tane oluşturmanız gerekir. Ardından, yeni bir parola tooinform parola hello tüm mevcut kullanıcılar değiştirildi ve bunların istemcileri toouse güncelleştirmeniz gerekir hello emin olun. Yönergeler için aşağıdaki adrese gidin:

* [Merhaba StorSimple Snapshot Manager parolasını değiştirme](storsimple-8000-change-passwords.md#set-the-storsimple-snapshot-manager-password)
* [Bir cihaz kimlik doğrulaması](storsimple-snapshot-manager-manage-devices.md#authenticate-a-device)

**S:** hello cihazda uzaktan erişim toohello StorSimple için Windows PowerShell için hello sertifikası değiştirildi. My uzaktan erişim istemcilerinin nasıl güncelleştiririm?

**Y:** StorSimple cihaz Yöneticisi hizmeti hello hello yeni sertifikayı indirin ve hello sertifika deposunda, uzaktan erişim istemcilerinin yüklü toobe sağlayın. Yönergeler için aşağıdaki adrese gidin:

* [Sertifika İçeri Aktar cmdlet'i](https://technet.microsoft.com/library/hh848630.aspx)

**S:** hello StorSimple cihaz Yöneticisi hizmeti aşılıp aşılmadığını korumalı my veri?

**Y:** bir web tarayıcısında görüntülediğinizde hizmet yapılandırma verilerini ortak anahtarınızla her zaman şifrelenir. Merhaba hizmet erişim toohello özel anahtar olmadığından hello hizmet almayacak mümkün toosee herhangi bir veri olabilir. Merhaba StorSimple cihaz Yöneticisi hizmeti aşılıp aşılmadığını üzerinde etkisi yoktur, hello StorSimple cihaz Yöneticisi hizmeti depolanan hiçbir anahtarları olarak.

**S:** birisi erişim toohello veri şifreleme sertifikasını elde ederse, verilerimi tehlikeye?

**Y:** Microsoft Azure hello Müşteri'nin veri şifreleme anahtarı (.pfx dosyası) şifrelenmiş biçimde depolar. Yalnızca erişim toohello .pfx dosyasını alma seçeneği Hello .pfx dosyası şifrelenir ve hello StorSimple hizmeti hello hizmet verileri şifreleme anahtarı toodecrypt hello .pfx dosyası yoktur çünkü tüm gizli kullanıma değil.

**S:** kamu varlık verilerim için Microsoft isterse ne olur?

**Y:** hello verilerin tümünü hello hizmette şifrelenir ve hello özel anahtarı tutulur hello aygıtla hello devlet olmadığından varlık hello müşteri hello verilerini kaldırmasını isteyebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

[StorSimple Cihazınızı dağıtma](storsimple-8000-deployment-walkthrough-u2.md).

