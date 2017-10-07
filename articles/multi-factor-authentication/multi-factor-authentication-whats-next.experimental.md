---
title: Azure MFA aaaConfigure | Microsoft Docs
description: "Bu hangi toodo MFA ile sonraki açıklayan hello Azure multi-Factor authentication sayfasıdır.  Bu raporlar, sahtekarlık Uyarısı, bir kerelik atlama, özel sesli mesajları, önbelleğe alma, güvenilen IP'leri ve uygulama parolaları içerir."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 75af734e-4b12-40de-aba4-b68d91064ae8
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: kgremban
ms.openlocfilehash: db7d87d95b73fed78d3ce599fd03da9692851663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-settings"></a>Azure çok faktörlü kimlik doğrulama ayarlarını yapılandırın
Bu makalede Azure çok faktörlü kimlik doğrulaması ve çalışıyor olduğundan göre yönetmenize yardımcı olur.  Azure multi-Factor Authentication dışında en tooget hello Yardım çeşitli konuları kapsar.  Tüm bu özellikler Azure çok faktörlü kimlik doğrulaması her sürümünde kullanılabilir.

| Özellik | Açıklama | 
|:--- |:--- |
| [Sahtekarlık Uyarısı](#fraud-alert) |Sahtekarlık uyarısı yapılandırılmış ve böylece kullanıcılarınızın kaynaklarını sahte denemeleri tooaccess rapor ayarlayın. |
| [Bir kerelik atlama](#one-time-bypass) |Bir kerelik geçiş kullanıcının tooauthenticate "çok faktörlü kimlik doğrulamasını atlayarak" tek bir kez sağlar. |
| [Özel sesli mesajları](#custom-voice-messages) |Özel sesli mesajları toouse izin kendi kayıtları veya çok faktörlü kimlik doğrulamasıyla tebrikler. |
| [Önbelleğe alma](#caching-in-azure-multi-factor-authentication) |Sonraki kimlik doğrulama girişimleri otomatik olarak başarılı böylece önbelleğe alma tooset belirli bir süre sağlar. |
| [Güvenilen IP'leri](#trusted-ips) |Federe veya yönetilen bir Kiracı Yöneticiler hello şirketin yerel intranetten oturum açtığında, kullanıcıların güvenilen IP'leri toobypass iki aşamalı doğrulamayı kullanabilirsiniz. |
| [Uygulama parolaları](#app-passwords) |Bir uygulama parolası MFA algılayan toobypass çok faktörlü kimlik doğrulaması değil ve çalışmaya devam bir uygulama sağlar. |
| [Anımsanan cihazlar ve tarayıcılar için çok faktörlü kimlik doğrulaması unutmayın](#remember-multi-factor-authentication-for-devices-that-users-trust) |MFA kullanarak bir kullanıcı başarıyla oturum sonra gün sayısı kümesini için tooremember cihazların sağlar. |
| [Seçilebilir doğrulama yöntemleri](#selectable-verification-methods) |Kullanıcıların toouse için kullanılabilir toochoose hello kimlik doğrulama yöntemleri sağlar. |

## <a name="access-hello-azure-mfa-management-portal"></a>Erişim hello Azure MFA Yönetim Portalı

Bu makalede ele alınan hello özellikleri hello Azure multi-Factor Authentication Yönetim Portalı yapılandırılır. MFA Yönetim Portalı hello Klasik Azure Portalı aracılığıyla tooaccess hello iki yolu vardır. Merhaba, önce bir çok faktörlü yetki sağlayıcı yöneterek Yapılandır. Merhaba, ikinci hello MFA hizmet ayarları aracılığıyla Yapılandır. 

### <a name="use-an-authentication-provider"></a>Bir kimlik doğrulama sağlayıcısı kullanın

Tüketim tabanlı MFA için çok faktörlü yetki sağlayıcı kullanıyorsanız bu yöntem tooaccess hello yönetim portalını kullanın.

tooaccess MFA Yönetim Portalı aracılığıyla Azure multi-Factor Auth sağlayıcısı Merhaba, hello Klasik Azure portalı bir Yöneticiyseniz ve select hello Active Directory seçeneği oturum açın. Merhaba tıklatın **çok faktörlü kimlik doğrulama sağlayıcıları** sekmesine, ardından dizininizi seçin ve hello tıklayın **Yönet** hello altındaki düğmesi.

### <a name="use-hello-mfa-service-settings-page"></a>Merhaba MFA Hizmeti Ayarları sayfası kullanın 

Lisanslar aşağıdaki hello biri varsa hello MFA Hizmeti Ayarları sayfası kullanabilirsiniz:
- Azure MFA
- Azure AD Premium 
- Enterprise Mobility + Security

tooaccess MFA Yönetim Portalı aracılığıyla hello MFA hizmet ayarları sayfasında, oturum hello Klasik Azure portalında yönetici olarak açın hello ve hello Active Directory seçeneğini seçin. Dizininizin tıklayın ve hello ardından **yapılandırma** sekmesi. Merhaba çok faktörlü kimlik doğrulaması bölümü altında seçin **hizmet ayarlarını Yönet**. Merhaba MFA Hizmeti Ayarları sayfası Hello altındaki hello tıklatın **Git toohello portal** bağlantı.


## <a name="fraud-alert"></a>Sahtekarlık Uyarısı
Sahtekarlık uyarısı yapılandırılmış ve böylece kullanıcılarınızın kaynaklarını sahte denemeleri tooaccess rapor ayarlayın.  Kullanıcıların sahtekarlık hello mobil uygulama ile ya da telefon üzerinden bildirebilirsiniz.

### <a name="set-up-fraud-alert"></a>Sahtekarlık uyarısı ayarla
1. Merhaba yönergeleri hello sayfanın üst kısmındaki bu başına MFA Yönetim Portalı toohello gidin.
2. Hello Azure multi-Factor Authentication Yönetim Portalı'da, tıklatın **ayarları** hello yapılandırma bölümüne altında.
3. Merhaba sahtekarlık uyarısı bölüm hello ayarları sayfasının altında hello denetleyin **toosubmit sahtekarlık uyarısı kullanıcıların** onay kutusu.
4. Seçin **kaydetmek** tooapply değişikliklerinizi. 

### <a name="configuration-options"></a>Yapılandırma seçenekleri

- **Sahtekarlık bildirildiğinde kullanıcıyı engelle** - bir kullanıcı raporları sahtekarlık hesaplarında engellenir.
- **TooReport sırasında sahtekarlık ilk selamlama kod** -kullanıcıların normalde # tooconfirm iki aşamalı doğrulamayı tuşuna basın. Bunlar tooreport sahtekarlık istiyorsanız # basmadan önce bir kod girin. Bu kodu **0** varsayılan olarak, ancak özelleştirebilirsiniz.

> [!NOTE]
> Microsoft'un varsayılan sesli karşılamalar kullanıcılar toopress &#0; toosubmit bir sahtekarlık uyarısı isteyin. Toouse 0 dışında bir kod istiyorsanız, kaydedin ve kendi özel sesli karşılamalar uygun yönergeleri ile karşıya yükleyin.

![Sahtekarlık uyarısı seçenekleri - ekran görüntüsü](./media/multi-factor-authentication-whats-next/fraud.png)

### <a name="how-users-report-fraud"></a>Kullanıcıların sahtekarlık raporu 
Sahtekarlık uyarısı iki yolla bildirilebilir.  Ya yoluyla hello mobil uygulama hello telefon.  

#### <a name="report-fraud-with-hello-mobile-app"></a>Merhaba mobil uygulama ile sahtekarlığı bildir
1. Bir doğrulama tooyour telefon gönderildiğinde, tooopen hello Microsoft Authenticator uygulamasını seçin.
2. Seçin **reddetme** hello bildirim. 
3. Seçin **rapor sahtekarlık**.
4. Kapat hello uygulama.

#### <a name="report-fraud-with-a-phone"></a>Bir telefon sahtekarlığı bildir
1. Bir doğrulama araması tooyour telefon geldiğinde, yanıtlayın.  
2. tooreport Sahtekarlık (varsayılan 0'dır) hello sahtekarlık kodunu girin ve # işaretini hello. Ardından, bir sahtekarlık uyarısı gönderildi bildirilir.
3. Son hello çağrısı.

### <a name="view-fraud-reports"></a>Sahtekarlık raporlarını görüntüle
1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Merhaba sol tarafta, Active Directory'yi seçin.
3. Merhaba üstünde seçin **çok faktörlü kimlik doğrulama sağlayıcıları** tooshow, çok faktörlü kimlik doğrulama sağlayıcıları listesi.
4. Çok faktörlü yetki sağlayıcı seçin ve tıklatın **Yönet** hello sayfanın hello sonundaki. Hello Azure multi-Factor Authentication Yönetim Portalı'nı açar.
5. Hello Azure multi-Factor Authentication Yönetim Portalı, altında bir raporu görüntüle'yi tıklatın **sahtekarlık Uyarısı**.
6. Merhaba raporda tooview istediğiniz hello tarih aralığını belirtin. Ayrıca, kullanıcı adları, telefon numaraları ve hello kullanıcının durumunu da belirtebilirsiniz.
7. Tıklatın **çalıştırmak** tooshow sahtekarlık uyarısı bir rapor. Tıklatın **verme tooCSV** tooexport hello rapor istiyorsanız.

## <a name="one-time-bypass"></a>Bir kerelik atlama
Bir kerelik geçiş, iki aşamalı doğrulama gerçekleştirmeden, tek bir kez kullanıcı tooauthenticate sağlar. Merhaba atlama geçicidir ve belirtilen sayıda saniye geçtikten sonra süresi dolar. Burada hello mobil uygulaması ya da telefon bildirim veya telefon görüşmesi almıyor durumlarda Hello kullanıcı istenen hello kaynak erişebilmesi için bir kerelik geçiş etkinleştirebilirsiniz.

### <a name="create-a-one-time-bypass"></a>Bir kerelik geçiş oluşturmak
1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Merhaba yönergeleri hello sayfanın üst kısmındaki bu başına MFA Yönetim Portalı toohello gidin.
3. Azure MFA sağlayıcınızı hello adını görürseniz ile Merhaba sol bir  **+**  sonraki tooit hello tıklatın  **+** . Farklı MFA sunucusu çoğaltma gruplarına ve hello Azure varsayılan grup gösterilir. Merhaba uygun grubu seçin.
4. Kullanıcı Yönetim'in altında seçin **bir kerelik geçiş**.
5. Merhaba bir kerelik geçiş sayfasında, tıklatın **yeni bir kerelik geçiş**.

  ![Bulut](./media/multi-factor-authentication-whats-next/create1.png)

6. Merhaba username, hello süresi hello atlama ve hello atlama hello nedenini girin. Tıklatın **atlama**.
7. Merhaba zaman sınırı hemen gereksinimlerini toosign hello tek seferlik atlama önce sona kadar hello kullanıcı etkinleşen. 

### <a name="view-hello-one-time-bypass-report"></a>Görünüm hello tek seferlik atlama raporu
1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Merhaba sol tarafta, Active Directory'yi seçin.
3. Merhaba üstünde seçin **çok faktörlü kimlik doğrulama sağlayıcıları** tooshow, çok faktörlü kimlik doğrulama sağlayıcıları listesi.
4. Çok faktörlü yetki sağlayıcı seçin ve tıklatın **Yönet** hello sayfanın hello sonundaki. Hello Azure multi-Factor Authentication Yönetim Portalı'nı açar.
5. Hello Azure multi-Factor Authentication Yönetim Portalı, Görünüm bir raporu altında hello sol tıklayın **bir kerelik geçiş**.
6. Merhaba raporda tooview istediğiniz hello tarih aralığını belirtin. Ayrıca, kullanıcı adları, telefon numaraları ve hello kullanıcının durumunu da belirtebilirsiniz.
7. Tıklatın **çalıştırmak** tooshow bir raporun atlar. Tıklatın **verme tooCSV** tooexport hello rapor istiyorsanız.

## <a name="custom-voice-messages"></a>Özel sesli mesajları
Özel sesli mesajları toouse izin kendi kayıtları veya iki aşamalı doğrulama için tebrikler. Toplama tooor tooreplace hello Microsoft kayıtlarında özel sesli mesajları kullanabilirsiniz.

Başlamadan önce bunlardan dikkat edin:

* Merhaba desteklenen dosya biçimleri .wav ve .mp3 olacaktır.
* Merhaba dosya boyutu sınırını 5 MB'tır.
* Kimlik doğrulama iletileri 20 saniyeden daha kısa olmalıdır. Merhaba doğrulama süresi dolmadan önce 20 saniyeden daha uzun iletileri yeterli zaman toorespond hello kullanıcılar vermeyin.

### <a name="set-up-a-custom-message"></a>Özel ileti ayarlayın

Özel ileti iki bölümden toocreating vardır. İlk olarak, selamlama iletisine karşıya yükleyin ve ardından, kullanıcılarınız için açın.

tooupload özel ileti:

1. Merhaba desteklenen dosya biçimleri birini kullanarak bir özel sesli ileti oluşturun.
2. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
3. Merhaba yönergeleri hello sayfanın üst kısmındaki bu başına MFA Yönetim Portalı toohello gidin.
4. Hello Azure multi-Factor Authentication Yönetim Portalı'da, tıklatın **sesli mesajlar** hello yapılandırma bölümüne altında.
5. Merhaba yapılandırma üzerinde: iletileri sayfa sesli, tıklatın **yeni bir sesli mesajı**.
   ![Bulut](./media/multi-factor-authentication-whats-next/custom1.png)
6. Merhaba yapılandırma üzerinde: yeni ses iletileri sayfasında, tıklatın **ses dosyalarını yönetme**.
   ![Bulut](./media/multi-factor-authentication-whats-next/custom2.png)
7. Merhaba yapılandırma üzerinde: ses dosyalarını sayfasında, tıklatın **ses dosyasını karşıya yükle**.
   ![Bulut](./media/multi-factor-authentication-whats-next/custom3.png)
8. Merhaba yapılandırma üzerinde: ses dosyasını karşıya yükle'ye tıklayın **Gözat** ve tooyour sesli mesaj gidin, tıklatın **açık**.
9. Bir açıklama ekleyin ve tıklatın **karşıya**.
10. Merhaba sesli mesaj yüklendikten sonra bir ileti hello dosyası başarıyla karşıya yüklediğiniz onaylar.

tooturn hello iletideki kullanıcılarınız için:

1. Hello solda tıklatın **sesli mesajlar**.
2. Hello sesli iletiler bölümü altında tıklatın **yeni bir sesli mesajı**.
3. Hello ifadesini Dil açılan bir dil seçin.
4. Belirli bir uygulama için bu iletiyi hello uygulama kutusuna belirtin.
5. Hello ileti türü açılır, yeni özel iletisiyle geçersiz kılınmış hello ileti türü toobe seçin.
6. Ses dosyası açılan Hello hello ilk bölümünde karşıya yüklediğiniz hello ses dosyası seçin.
7. **Oluştur**'a tıklayın. Bir ileti, sesli iletiyi başarıyla oluşturdunuz onaylar.
    ![Bulut](./media/multi-factor-authentication-whats-next/custom5.png)</center>

## <a name="caching-in-azure-multi-factor-authentication"></a>Azure çok faktörlü kimlik doğrulaması önbelleğe alma
Bu süre içinde sonraki kimlik doğrulama girişimleri otomatik olarak başarılı böylece önbelleğe alma tooset belirli bir süre sağlar. Merhaba ilk istek hala devam ederken VPN gibi şirket içi sistemlerde fazla doğrulama isteği gönderdiğinizde, önbelleğe alma kullanılır. Merhaba sonraki istekleri toosucceed otomatik olarak hello sonra arkasından hello ilk doğrulama devam ediyor başarılı olur. 

Önbelleğe alma, oturum açma işlemleri tooAzure AD kullanılan hedeflenen toobe değil.

### <a name="set-up-caching"></a>Önbelleğe almayı kurmak 
1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Merhaba yönergeleri hello sayfanın üst kısmındaki bu başına MFA Yönetim Portalı toohello gidin.
3. Hello Azure multi-Factor Authentication Yönetim Portalı'da, tıklatın **önbelleğe alma** hello yapılandırma bölümüne altında.
4. Tıklatın **yeni önbellek** hello yapılandırma önbelleğe alma sayfasında.
5. Merhaba önbellek türü ve hello önbellek saniye seçin. **Oluştur**'a tıklayın.

<center>![Bulut](./media/multi-factor-authentication-whats-next/cache.png)</center>

## <a name="trusted-ips"></a>Güvenilen IP'ler
Güvenilen IP'leri Azure mfa federe veya yönetilen bir Kiracı Yöneticiler toobypass iki aşamalı doğrulamayı kullanabileceğiniz bir özelliktir. Hangi hello şirketin yerel intranetten imzalama kullanıcılar için kullanılır. Bu özellik, hello Azure çok faktörlü kimlik doğrulaması, değil hello ücretsiz sürüm Yöneticiler için tam sürümü ile kullanılabilir. Nasıl tooget hello Azure multi-Factor Authentication'ın tam sürümünü hakkında daha fazla bilgi için bkz: [Azure çok faktörlü kimlik doğrulaması](multi-factor-authentication.md).

| Azure AD Kiracı türü | Kullanılabilir güvenilen IP Seçenekleri |
|:--- |:--- |
| Yönetilen |<li>Belirli IP adresi aralıkları – Yöneticiler hello şirketin intranetten imzalama kullanıcılar için iki aşamalı doğrulamayı atlayan bir IP adresi aralığı belirtebilirsiniz.</li> |
| Federasyon |<li>Tüm federe kullanıcılar - tüm Federasyon oturum açan kullanıcılar, gelen içinde hello kuruluş AD FS tarafından verilen bir talep kullanan iki aşamalı doğrulamayı atlayacaktır.</li><br><li>Belirli IP adresi aralıkları – Yöneticiler hello şirketin intranetten imzalama kullanıcılar için iki aşamalı doğrulamayı atlayan bir IP adresi aralığı belirtebilirsiniz. |

Bu yalnızca gelen works bir şirket intranetindeki atlama. 

**Son kullanıcı deneyimi corpnet içinde:**

Güvenilen IP'ler devre dışı bırakıldığında, iki aşamalı doğrulamayı tarayıcı akışları için gereklidir ve uygulama parolaları eski zengin istemci uygulamaları için gereklidir. 

Güvenilen IP'ler etkinleştirildiğinde, iki aşamalı doğrulamayı olan *değil* tarayıcı akışları için gereklidir. Uygulama parolaları *değil* hello kullanıcı zaten bir uygulama parolası oluşturulmuş kurmadı koşuluyla eski zengin istemci uygulamaları için gerekli. Bir uygulama parolası kullanımda olduğunda, gerekli kalır. 

**Son kullanıcı deneyimi dış corpnet:**

Güvenilen IP'ler veya etkinleştirilip etkinleştirilmeyeceğini iki aşamalı doğrulamayı tarayıcı akışları için gereklidir ve uygulama parolaları eski zengin istemci uygulamaları için gereklidir. 

### <a name="tooenable-trusted-ips"></a>tooenable güvenilen IP'leri
1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Bu makalenin hello başında hello yönergeleri başına toohello MFA Hizmeti Ayarları sayfası gidin.
3. Merhaba hizmet ayarları sayfasında, güvenilen IP'ler altında iki seçeneğiniz vardır:
   
   * **My intranetten gelen Federasyon kullanıcılarının istekleri için** – hello kutuyu. AD FS tarafından verilen bir talep kullanarak hello şirket ağı atlama iki aşamalı doğrulamayı gelen oturum açan tüm Federasyon kullanıcıları.
   * **Belirli bir ortak IP aralığını gelen istekleri için** – hello IP adreslerini CIDR gösterimini kullanarak sağlanan hello metin kutusuna girin. Örneğin: hello aralığı xxx.xxx.xxx.1 – IP adresleri için xxx.xxx.xxx.0/24 xxx.xxx.xxx.254 ya da tek bir IP adresi xxx.xxx.xxx.xxx/32. Too50 IP adres aralıklarını girebilirsiniz. Bu IP adreslerinden oturum açan kullanıcıların iki aşamalı Doğrulamayı atla.
4. **Kaydet** düğmesine tıklayın.
5. Merhaba güncelleştirmeler uygulandıktan sonra tıklayın **Kapat**.

![Güvenilen IP'ler](./media/multi-factor-authentication-whats-next/trustedips3.png)

## <a name="app-passwords"></a>Uygulama parolaları
Bazı uygulamalar, Office 2010 gibi eski veya ve Apple Mail iki aşamalı doğrulamayı desteklemez. Bunlar, yapılandırılmış tooaccept ikinci doğrulama değil. toouse bu uygulamaları geleneksel parolanız yerine toouse "uygulama parolaları" gerekir. Hello uygulama parolası hello uygulama toobypass iki aşamalı doğrulama sağlar ve çalışmaya devam edin.

> [!NOTE]
> Merhaba Office 2013 istemcilerin için modern kimlik doğrulaması
> 
> Office 2013 istemciler (Outlook gibi) ve yeni destek modern kimlik doğrulama protokolleri ve iki aşamalı doğrulama ile etkin toowork olabilir. Etkinleştirildikten sonra uygulama parolaları bu istemciler için gerekli değildir.  Daha fazla bilgi için bkz: [Office 2013 modern kimlik doğrulaması genel önizlemesi Duyuruldu](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).

### <a name="important-things-tooknow-about-app-passwords"></a>Uygulama parolaları hakkında önemli noktalar tooknow
Uygulama parolaları hakkında bilinmesi önemli şeyler listesi aşağıda verilmiştir.

* Her uygulama için bir kez hello giriş kutusuna uygulama parolaları yeniden girilmesi gerekir. Kullanıcıların yoksa bunları tookeep izini ve her zaman girin.
* Merhaba gerçek parola otomatik olarak oluşturulur ve hello kullanıcı tarafından sağlanmaz. Merhaba otomatik olarak oluşturulan parolanın bir saldırgan tooguess için daha zordur ve daha güvenlidir.
* Kullanıcı başına 40 parolalık bir sınırı yoktur. 
* Parolalar ve şirket içi senaryolarda hello uygulama parolası Kurumsal kimlik dışında hello bilinen değil bu yana başarısız olan başlatılabilir kullanım önbelleğe uygulamalar. Örnek şirket içi Exchange e-postaları ancak arşivlenen hello posta hello bulutta. Merhaba aynı parola çalışmaz.
* Çok faktörlü kimlik doğrulaması başlatıldığında, bazı tarayıcı olmayan istemciler ile parolanızı kullanabilirsiniz. Yönetim görevleri için uygulama parolaları kullanamazsınız. Güçlü parola toorun PowerShell komut dosyalarıyla bir hizmet hesabı oluşturun ve o hesap için iki aşamalı doğrulamayı etkinleştirmeyin emin olun.

> [!WARNING]
> Uygulama parolaları burada istemcileri hem şirket içi ile iletişim kurmak ve Otomatik bulma uç noktaları bulut Karma ortamlarda çalışmıyor. Etki alanı parolaları gerekli tooauthenticate şirket içi ve uygulama parolaları hello bulut ile gerekli tooauthenticate.

### <a name="naming-guidance-for-app-passwords"></a>Uygulama parolaları için adlandırma Kılavuzu
Uygulama parolası adlarının üzerinde kullanıldıkları hello aygıt yansıtmalıdır. Örneğin, tarayıcı olmayan uygulamalara sahip bir dizüstü bilgisayarınız varsa, dizüstü adlı bir uygulama parolası oluşturmanız ve bu uygulama parolasını kullanın. Ardından, başka bir oluşturun uygulama parolası aynı uygulamaları, masaüstü bilgisayarınızda Merhaba Masaüstü adlı. 

Microsoft, cihaz, uygulama başına değil bir uygulama parolası başına bir uygulama parolası oluşturma önerir.

### <a name="federated-sso-app-passwords"></a>Federasyon (SSO) uygulama parolaları
Azure AD şirket içi Windows Server Active Directory etki alanı Hizmetleri (AD DS) ile Federasyon (çoklu oturum açma) destekler. Kuruluşunuz Azure AD ile birleştirildiyse ve Azure multi-Factor Authentication kullanarak toobe kalacaklarını, uygulama parolaları hakkında hello bilgi sizin için önemli. Bu bölüm, yalnızca toofederated (SSO) müşterileri geçerlidir.

* Uygulama parolaları Azure AD tarafından doğrulanır ve bu nedenle Federasyon atlayabilir. Federasyon yalnızca etkin bir şekilde uygulama parolaları ayarlarken kullanılır.
* Federasyon (SSO) kullanıcılar için biz hiçbir zaman hello pasif akış aksine toohello kimlik sağlayıcıyı (IDP) gidin. Merhaba parolaları hello kuruluş kimliği depolanır. Merhaba kullanıcı hello şirketten ayrılırsa, bu bilgileri gerçek zamanında DirSync kullanarak tooflow tooorganizational kimliği var. Hesap devre dışı bırakma/silme, Azure AD'de uygulama parolasını devre dışı bırakma/silme geciktirme toothree saatleri toosync yukarı sürebilir.
* Şirket için İstemci Erişimi Denetimi ayarları Uygulama Parolası tarafından onaylanmaz.
* Günlüğe kaydetme/denetleme yeteneği şirket içi kimlik doğrulaması uygulama parolası için kullanılabilir değildir.
* Bazı gelişmiş mimari tasarımları kuruluş kullanıcı adı, parola ve uygulama parolaları bileşimini iki aşamalı doğrulamayı istemcileriyle kullanırken gerektirebilir. Ancak burada kimlik doğrulamasında üzerinde bağlıdır. Bir şirket içi altyapı karşı kimlik doğrulaması istemcileri için bir kuruluş kullanıcı adı ve parola kullanırsınız. Azure AD karşı kimlik doğrulaması istemcileri için hello uygulama parolası kullanırsınız.

  Örneğin, bu örnekleri oluşan bir mimari olduğunu varsayalım:

  * Şirket içi örneğinizi Azure AD ile Active Directory federasyonunu
  * Exchange online kullanıyorsanız
  * Özel olarak şirket içi Lync kullanma
  * Azure multi-Factor Authentication kullanma

  ![Proofup](./media/multi-factor-authentication-whats-next/federated.png)

  Bu durumlarda, şu adımları izlemelisiniz:

  * İmzalarken-tooLync kuruluşların kullanıcı adı ve parola kullanın.
  * Çevrimiçi tooExchange bağlayan bir Outlook istemcisi aracılığıyla tooaccess hello adres defteri çalışırken, bir uygulama parolasını kullanın.

### <a name="allow-app-password-creation"></a>Uygulama parolası oluşturmaya izin ver
Varsayılan olarak, kullanıcılar uygulama parolaları oluşturamaz, ancak kendiniz hello özelliğini etkinleştirebilirsiniz. tooallow kullanıcılar özelliği toocreate uygulama parolaları Merhaba, hello aşağıdaki yordamı kullanın:

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Bu makalenin hello başında hello yönergeleri başına toohello MFA Hizmeti Ayarları sayfası gidin.
3. Merhaba radyo düğmesini seçin sonraki çok**tarayıcı olmayan uygulamalara kullanıcıların toocreate uygulama parolaları toosign izin**.

![Uygulama parolaları oluşturma](./media/multi-factor-authentication-whats-next/trustedips3.png)

### <a name="create-app-passwords"></a>Uygulama parolaları oluşturma
Kullanıcıların uygulama parolaları, ilk kaydı sırasında oluşturabilirsiniz. Bunlar toocreate uygulama parolaları verir hello kayıt işlemini hello sonunda seçeneği sunulur.

Kullanıcıların uygulama parolaları kayıttan sonra oluşturabilirsiniz. Bunlar, uygulama parolaları hello hello Azure portal veya hello Office 365 portalı ayarlarına değiştirerek oluşturabilirsiniz. Daha fazla bilgi ve kullanıcılarınız için ayrıntılı adımlar için bkz: [Azure çok faktörlü kimlik doğrulaması'ndaki uygulama parolaları nedir](./end-user/multi-factor-authentication-end-user-app-passwords.md).

## <a name="remember-multi-factor-authentication-for-devices-that-users-trust"></a>Kullanıcıların güven cihazlar için çok faktörlü kimlik doğrulaması unutmayın
Cihazlar ve kullanıcılar güven tüm MFA kullanıcılar için boş bir özelliktir; tarayıcılar için çok faktörlü kimlik doğrulaması anımsama. Çok faktörlü kimlik doğrulaması sağlayan kullanıcılar tooby geçiş oturum açtıktan sonra gün sayısı kümesini MFA'ya. Bu özellik hello sayısı kullanıcı hello üzerinde iki aşamalı doğrulamayı gerçekleştirebilir en aza indirerek kullanılabilirlik iyileştirir aynı aygıt.

Bir hesap veya aygıt aşılırsa, ancak, güvenilen cihazlar için MFA hatırlama güvenliği etkileyebilir. Bir kurumsal hesap güvenliği tehlikeye girdiğinde veya güvenilir bir cihaz kaybolur veya çalınırsa, çok ihtiyacınız[tüm cihazlarda çok faktörlü kimlik doğrulama geri](multi-factor-authentication-manage-users-and-devices.md#restore-mfa-on-all-remembered-devices-for-a-user). Bu işlem tüm cihazlar güvenilen hello durumundan iptal eder ve gerekli tooperform iki aşamalı doğrulamayı yeniden hello kullanıcıdır. Ayrıca kullanıcılar toorestore MFA hello yönergeleri ile kendi cihazlarda söyleyebilirsiniz içinde [iki aşamalı doğrulama için ayarlarınızı yönetme](./end-user/multi-factor-authentication-end-user-manage-settings.md#require-two-step-verification-again-on-a-device-youve-marked-as-trusted)

### <a name="how-it-works"></a>Nasıl çalışır?

Çok faktörlü kimlik doğrulaması çalışır bir kullanıcı hello ettiğinde hello tarayıcıda kalıcı bir tanımlama bilgisi ayarlayarak hatırlamak "için sorma **X** gün" oturum açma sırasında kutusu. Merhaba tanımlama bilgisi süresi doluncaya kadar hello kullanıcı MFA için yeniden bu tarayıcıdan istenmez. Merhaba kullanıcı üzerinde farklı bir tarayıcı açarsa aynı cihaz veya temizler hello kendi tanımlama bilgileri yeniden oldukları istendiğinde tooverify. 

Merhaba "için sorma **X** gün" modern kimlik doğrulama desteği olup olmadığına bakılmaksızın, onay kutusu tarayıcı olmayan uygulamaları üzerinde gösterilen değil. Bu uygulamalar her saat yeni erişim belirteçleri sağlamak yenileme belirteçleri kullanın. Bir yenileme belirteci doğrulandığında, Azure AD hello son zaman iki aşamalı doğrulamayı yapılandırılmış hello gün sayısı içinde gerçekleştirilen denetler. 

Conclusion, güvenilen cihazlara MFA hatırlama kimlik doğrulamaları (hangi normalde her zaman sor) web uygulamalarını hello sayısını azaltır. Ancak aynı zamanda kimlik doğrulama (hangi normalde her 90 günde isteyin) modern kimlik doğrulaması istemcileri için hello sayısını artırır.

> [!NOTE]
>Bu özellik kullanıcıların hello Azure MFA sunucusu aracılığıyla AD FS için iki aşamalı doğrulamayı veya bir üçüncü taraf MFA çözümü gerçekleştirdiğinizde hello "Oturumumu açık bırak" özelliği AD FS ile uyumlu değil. Kullanıcılarınızın "Oturumumu açık bırak" AD FS seçerseniz ve ayrıca MFA için cihazlarını güvenilir olarak işaretlemek, hello "MFA unutmayın" gün sayısı sona erdikten sonra bunlar mümkün tooverify olmayacaktır. Azure AD yeni iki aşamalı doğrulama isteklerini, ancak AD FS belirteciyle hello özgün MFA talep ve iki aşamalı doğrulamayı yeniden gerçekleştirmek yerine tarihi döndürür. Bu işlem Azure arasında doğrulama döngüsü kapalı ayarlar AD ve AD FS. 

### <a name="enable-remember-multi-factor-authentication"></a>Anımsa çok faktörlü kimlik doğrulamasını etkinleştir
1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Bu makalenin hello başında hello yönergeleri başına toohello MFA Hizmeti Ayarları sayfası gidin.
3. Merhaba hizmet ayarları sayfasında, kullanıcı cihaz ayarları altında yönetmek, hello denetleyin **kullanıcıların güvendikleri cihazlarda tooremember çok faktörlü kimlik doğrulaması izin** kutusu.
   ![Aygıtları unutmayın](./media/multi-factor-authentication-whats-next/remember.png)
4. Merhaba tooallow hello güvenilen cihazları toobypass iki aşamalı doğrulamayı istediğiniz gün sayısını ayarlayın. Merhaba varsayılan değer 14 gündür.
5. **Kaydet** düğmesine tıklayın.
6. **Kapat**’a tıklayın.

### <a name="mark-a-device-as-trusted"></a>Bir aygıt güvenilen olarak işaretle

Bu özelliği etkinleştirdiğinizde, kullanıcılar bir aygıtın ne zaman güvenilir olarak işaretleyebilir denetleyerek oturum **bir daha sorma**.

![-Ekran görüntüsü sorma](./media/multi-factor-authentication-whats-next/trusted.png)

## <a name="selectable-verification-methods"></a>Seçilebilir doğrulama yöntemleri
Hangi doğrulama yöntemleri, kullanıcılarınız için kullanılabilir seçebilirsiniz. Aşağıdaki tablonun hello her yöntem kısa bir genel bakış sağlar.

Kullanıcılarınız için MFA hesaplarına kaydettiğinizde, bunlar, etkin hello seçenekleri dışında tercih edilen doğrulama yöntemi seçin. kendi kayıt işlemi için Başlangıç Kılavuzu kapsanan [Hesabımı iki aşamalı doğrulama için ayarlama](multi-factor-authentication-end-user-first-time.md)

| Yöntem | Açıklama |
|:--- |:--- |
| Çağrı toophone |Otomatik bir sesli aramayla yerleştirir. Merhaba kullanıcı yanıtlar hello çağırın ve # tuşuna bastığında hello telefon tuş tooauthenticate. Bu telefon numarası eşitlenmiş tooon içi Active Directory'de değil. |
| Metin iletisi toophone |Doğrulama kodunu içeren bir kısa mesaj gönderir. Merhaba, istendiğinde tooeither yanıt toohello metni, hello doğrulama kodu ya da tooenter hello doğrulama hello oturum açma arabirimine koda iletisiyle kullanıcıdır. |
| Mobil uygulama üzerinden bildirim |Anında iletme bildirimi tooyour telefonunuza veya kayıtlı cihazınıza gönderir. Merhaba kullanıcı hello bildirim görünümleri ve seçer **doğrula** toocomplete doğrulama. <br>Merhaba Microsoft Authenticator uygulaması için kullanılabilir [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), ve [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |
| Mobil uygulamadan alınan doğrulama kodu |Merhaba Microsoft Authenticator uygulamasını her 30 saniyede yeni bir OATH doğrulama kodu oluşturur. Merhaba kullanıcı oturum açma hello arabirimine bu doğrulama kodu girer.<br>Merhaba Microsoft Authenticator uygulaması için kullanılabilir [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), ve [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |

### <a name="how-tooenabledisable-authentication-methods"></a>Nasıl tooenable/devre dışı bırak kimlik doğrulama yöntemleri
1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Bu makalenin hello başında hello yönergeleri başına toohello MFA Hizmeti Ayarları sayfası gidin.
3. Merhaba hizmet ayarları sayfasında, doğrulama seçeneklerini seçin/toouse istediğiniz hello seçenekleri seçimini kaldırın.
   ![Doğrulama seçenekleri](./media/multi-factor-authentication-whats-next/authmethods.png)
4. **Kaydet** düğmesine tıklayın.
5. **Kapat**’a tıklayın.
