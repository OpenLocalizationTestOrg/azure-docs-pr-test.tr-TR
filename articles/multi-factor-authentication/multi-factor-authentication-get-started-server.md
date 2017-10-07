---
title: "aaaGetting başlatılan Azure çok faktörlü kimlik doğrulama sunucusu | Microsoft Docs"
description: "Bu tooget Azure MFA sunucusu ile çalışmaya nasıl açıklayan hello Azure multi-Factor authentication sayfasıdır."
services: multi-factor-authentication
keywords: "kimlik doğrulama sunucusu, azure multi factor authentication uygulaması etkinleştirme sayfası, kimlik doğrulama sunucusu indirme"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: e94120e4-ed77-44b8-84e4-1c5f7e186a6b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 92a6a586eb96375e92a9455ad64e67221001db81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-multi-factor-authentication-server"></a>Hello Azure multi-Factor Authentication sunucusu ile çalışmaya başlama

<center>![Şirket içi MFA](./media/multi-factor-authentication-get-started-server/server2.png)</center>

Toouse multi-Factor Authentication sunucusu şirket içi belirledik, şimdi yapmalarını. Bu sayfayı hello sunucusu ve şirket içi Active Directory ile ayarlama yeni bir yüklemesini ele alınmaktadır. Zaten hello MFA server yüklü ve tooupgrade arıyorsanız, bkz: [yükseltme toohello en son Azure çok faktörlü kimlik doğrulama sunucusu](multi-factor-authentication-server-upgrade.md). Yalnızca hello web hizmeti yükleme hakkında bilgi arıyorsanız bkz [dağıtma hello Azure multi-Factor Authentication sunucusu mobil uygulama Web hizmeti](multi-factor-authentication-get-started-server-webservice.md).

## <a name="plan-your-deployment"></a>Dağıtımınızı planlama

Hello Azure çok faktörlü kimlik doğrulama sunucusu indirmeden önce yük ve yüksek oranda kullanılabilirlik gereksinimleri nelerdir hakkında düşünün. Bu bilgi toodecide nasıl ve nerede kullanmak toodeploy.

İyi bir kılavuz hello ihtiyacınız bellek miktarını hello sayısı, kullanıcı için düzenli olarak tooauthenticate bekler.

| Kullanıcılar | RAM |
| ----- | --- |
| 1-10.000 | 4 GB |
| 10.001-50.000 | 8 GB |
| 50.001-100.000 | 12 GB |
| 100.000-200.001 | 16 GB |
| 200.001+ | 32 GB |

Yüksek kullanılabilirlik için birden çok sunucu yukarı tooset gereksinim veya Yük Dengeleme? Bu yapılandırma Azure MFA sunucusu ile ayarlama yolları tooset mevcuttur. İlk Azure MFA sunucusu yüklediğinizde, hello Yöneticisi olur. Herhangi bir ek sunucu bağımlı olur ve otomatik olarak kullanıcılar ve yapılandırma hello şablonu ile eşitleyin. Ardından, bir birincil sunucusunu yapılandırmak ve hareket hello rest sahip olarak yedekleme veya Yük Dengeleme tüm hello sunucular arasında ayarlayabilirsiniz.

Bir şablonu Azure MFA sunucusu çevrimdışı olduğunda, hello bağımlı sunucuları işlemi iki aşamalı doğrulama isteklerini yine görüntüleyebilirsiniz. Ancak, ekleyemezsiniz yeni ve mevcut kullanıcılar güncelleştiremiyor ayarlarına olana kadar hello ana tekrar çevrimiçi ya astı yükseltilmiş.

### <a name="prepare-your-environment"></a>Ortamınızı hazırlama

Azure çok faktörlü kimlik doğrulaması için kullanmakta olduğunuz hello sunucu hello aşağıdaki gereksinimleri karşıladığından emin olun:

| Azure Multi-Factor Authentication Sunucusu Gereksinimleri | Açıklama |
|:--- |:--- |
| Donanım |<li>200 MB boş sabit disk alanı</li><li>x32 veya x64 özellikli işlemci</li><li>1 GB veya daha fazla RAM</li> |
| Yazılım |<li>Windows Server 2008 veya üst sürümü hello ana bilgisayar sunucu işletim sistemi ise</li><li>Windows 7 veya üst sürümü hello ana bilgisayar istemci işletim sistemi ise</li><li>Microsoft .NET 4.0 Framework</li><li>IIS 7.0 ya da yüklüyorsanız büyük kullanıcı portalı veya web hizmeti SDK'sını hello</li> |

### <a name="azure-mfa-server-components"></a>Azure MFA Sunucusu Bileşenleri

Azure MFA sunucusunu oluşturan üç web bileşeni şunlardır:

* Web hizmeti SDK - ile iletişim diğer bileşenleri hello ve hello Azure MFA uygulama sunucusunda yüklü etkinleştirir
* Kullanıcı Portalı - kullanıcıların tooenroll Azure çok faktörlü kimlik doğrulama (MFA) verir ve hesaplarını korumalarını bir IIS web sitesi.
* Mobil uygulama Web hizmeti - hello Microsoft Authenticator uygulaması gibi bir mobil uygulama için iki aşamalı doğrulamayı kullanarak sağlar.

Her üç bileşenin hello üzerinde yüklenebilir hello sunucusu internet'e yönelik ise aynı sunucu. Merhaba bileşenlerini parçalamak, hello Web hizmeti SDK'sı hello Azure MFA uygulama sunucusunda yüklü olduğundan ve hello Kullanıcı Portalı ve mobil uygulama Web hizmeti bir internet'e yönelik sunucuda yüklü.

### <a name="azure-multi-factor-authentication-server-firewall-requirements"></a>Azure Multi-Factor Authentication Sunucusu güvenlik duvarı gereksinimleri

Her MFA sunucusunun bağlantı noktası 443 giden toohello adresleri aşağıdaki üzerinde mümkün toocommunicate olması gerekir:

* https://pfd.phonefactor.net
* https://pfd2.phonefactor.net
* https://css.phonefactor.net

Giden güvenlik duvarları bağlantı noktası 443 üzerinde kısıtlarsanız, IP adres aralıklarını aşağıdaki hello açın:

| IP Alt ağı | Ağ maskesi | IP aralığı |
|:---: |:---: |:---: |
| 134.170.116.0/25 |255.255.255.128 |134.170.116.1 – 134.170.116.126 |
| 134.170.165.0/25 |255.255.255.128 |134.170.165.1 – 134.170.165.126 |
| 70.37.154.128/25 |255.255.255.128 |70.37.154.129 – 70.37.154.254 |

Merhaba olay onayı özelliği kullanmadığınız ve kullanıcılarınızın mobil uygulamaları tooverify aygıtlardan hello şirket ağında kullanmadığınız, yalnızca aralıkları aşağıdaki hello gerekir:

| IP Alt ağı | Ağ maskesi | IP aralığı |
|:---: |:---: |:---: |
| 134.170.116.72/29 |255.255.255.248 |134.170.116.72 – 134.170.116.79 |
| 134.170.165.72/29 |255.255.255.248 |134.170.165.72 – 134.170.165.79 |
| 70.37.154.200/29 |255.255.255.248 |70.37.154.201 – 70.37.154.206 |

## <a name="download-hello-azure-multi-factor-authentication-server"></a>Hello Azure multi-Factor Authentication Sunucusu'nu indirme

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) yönetici olarak.
2. Merhaba solda seçin **Active Directory**
3. **Kullanıcılar ve gruplar**’a tıklayın.
4. **Tüm kullanıcılar**’a tıklayın.
5. **Multi-Factor Authentication**’a tıklayın.
6. **Multi-factor authentication** altında, **Hizmet ayarları**'nı seçin

   ![Hizmet ayarları sayfası](./media/multi-factor-authentication-get-started-server/servicesettings.png)

6. Merhaba ekranında hello altında Hello Hizmetleri ayarları sayfasında, tıklatın **Git toohello portal**. Yeni bir sayfa açılır.
7. **İndirmeler**’e tıklayın.
8. Merhaba tıklatın **karşıdan** bağlamak ve hello yükleyici kaydedin.

   ![MFA sunucusu indirme](./media/multi-factor-authentication-get-started-server/download4.png)

9. Bu sayfa, biz tooit sonra çalışan hello yükleyici başvuruda bulunacak şekilde açık tutun.

## <a name="install-and-configure-hello-azure-multi-factor-authentication-server"></a>Yükleme ve hello Azure çok faktörlü kimlik doğrulama sunucusu yapılandırma

Merhaba sunucuyu indirdiğinize göre yükleyin ve yapılandırın. Üzerinde yüklüyorsanız bu hello sunucu Planlama bölüm hello listelenen gereksinimleri karşıladığından emin olun.

1. Merhaba yürütülebilir çift tıklayın.
2. Merhaba yükleme klasörünü seçin ekranında, hello klasörün doğru olduğundan emin olun ve tıklayın **sonraki**.
3. Merhaba yüklemesi tamamlandıktan sonra tıklayın **son**.  Merhaba Yapılandırma Sihirbazı'nı başlatır.
4. Hello Yapılandırma Sihirbazı Hoş Geldiniz ekranında, denetleme **Atla kullanarak kimlik doğrulaması Yapılandırma Sihirbazı'nı hello** tıklatıp **sonraki**.  Merhaba sihirbaz kapanır ve hello sunucu başlatır.

   ![Bulut](./media/multi-factor-authentication-get-started-server/skip2.png)

5. Biz hello sunucusundan indirilen geri hello sayfasında hello tıklayın **etkinleştirme kimlik bilgileri oluştur** düğmesi. Bu bilgiler hello hello kutularda Azure MFA sunucusu sağlanan kopyalayın ve tıklayın **etkinleştirme**.

## <a name="send-users-an-email"></a>Kullanıcılara e-posta gönderme

tooease piyasaya çıkma, MFA sunucusu toocommunicate Kullanıcılarınızla izin verin. MFA sunucusu, bir e-posta tooinform gönderebilir bunları bunlar için iki aşamalı doğrulamayı kaydettirilen.

Kullanıcılarınızın iki aşamalı doğrulama için nasıl yapılandırdığınıza göre e-posta gönderdiğiniz hello belirlenmesi. Örneğin, mümkün tooimport telefon numaralarını hello şirket dizininden varsa, kullanıcıların hangi tooexpect bilmesi hello e-posta hello varsayılan telefon numaralarını içermelidir. Telefon numaralarını içeri değil ya da kullanıcılarınızın toouse hello mobil uygulama kalacaklarını, bunları toocomplete yönlendiren bir e-posta Gönder hesap kaydını. Köprü toohello Azure multi-Factor Authentication Kullanıcı Portalı hello e-postayla içerir.

Merhaba içeriğine hello e-posta, hello kullanıcı (telefon araması, SMS veya mobil uygulama) için ayarlanmış doğrulama hello yöntemine bağlı olarak değişir.  Kimlik doğrulaması sırasında hello kullanıcı bir PIN gerekli toouse ise, örneğin, hello e-posta bunları ne ilk PIN'ini ayarlandığından söyler.  Kullanıcılar kendi ilk doğrulama sırasında kendi PIN gerekli toochange olan.

### <a name="configure-email-and-email-templates"></a>E-posta ve e-posta şablonlarını yapılandırma

Bu e-postaları göndermek için hello sol tooset hello ayarlarını Hello e-posta simgesine tıklayın. Bu sayfa hello denetleyerek hello SMTP posta sunucusunu ve gönderme e-posta bilgilerinin nerede girebilirsiniz **gönderme toousers e-postalar** onay kutusu.

![MFA Sunucusu E-posta yapılandırması](./media/multi-factor-authentication-get-started-server/email1.png)

Merhaba e-posta içeriği sekmesinde ndan kullanılabilir toochoose olan hello e-posta şablonlarını görebilirsiniz. Nasıl kullanıcılar tooperform iki aşamalı doğrulamayı yapılandırdığınıza bağlı olarak, en uygun hello şablonunu seçin.

![MFA Sunucusu E-posta şablonları](./media/multi-factor-authentication-get-started-server/email2.png)

## <a name="import-users-from-active-directory"></a>Kullanıcıları Active Directory'den içeri aktarma

Merhaba sunucu yüklü artık tooadd kullanıcılar isteyeceksiniz. Bunları el ile kullanıcıları Active Directory'den içe aktarmak veya Active Directory ile Otomatik eşitlemeyi yapılandırma toocreate seçebilirsiniz.

### <a name="manual-import-from-active-directory"></a>Active Directory'den elle içeri aktarma

1. Hello Azure MFA sunucusu hello soldaki seçin **kullanıcılar**.
2. Merhaba altındaki seçin **Active Directory'den içeri aktar**.
3. Şimdi, ya da tek tek kullanıcılara veya arama hello AD dizini için OU'lar için içindeki kullanıcılarla birlikte arayabilirsiniz.  Bu durumda, hello kullanıcıların OU'sunu belirtin.
4. Hello sağ tüm hello kullanıcıları vurgulayın **alma**.  Başarılı olduğunuzu belirten bir açılır pencere görmeniz gerekir.  Kapat hello içeri aktarma penceresini açın.

   ![MFA Sunucusu kullanıcı içeri aktarma](./media/multi-factor-authentication-get-started-server/import2.png)

### <a name="automated-synchronization-with-active-directory"></a>Active Directory ile otomatik eşitleme

1. Hello Azure MFA sunucusu hello soldaki seçin **dizin tümleştirme**.
2. Toohello gidin **eşitleme** sekmesi.
3. Merhaba altındaki seçin **Ekle**
4. Merhaba, **Eşitleme öğesi Ekle** görüntülenen kutusunda hello etki alanı OU seçin **veya** güvenlik grubu, ayarları, yöntem Varsayılanları ve dil varsayılan olarak bu eşitleme için görev ve tıklatın**Eklemek**.
5. Etiketli onay hello kutusunu **Active Directory ile eşitlemeyi etkinleştir** ve bir **eşitleme aralığı** bir dakika ile 24 saat arasında.

## <a name="how-hello-azure-multi-factor-authentication-server-handles-user-data"></a>Hello Azure multi-Factor Authentication sunucusu kullanıcı verileri nasıl işler?

Merhaba çok faktörlü kimlik doğrulama (MFA) şirket içi Server kullandığınızda, bir kullanıcının veri hello şirket içi sunucularda depolanır. Kalıcı kullanıcı verileri hello bulutta depolanır. Merhaba kullanıcı iki aşamalı doğrulama gerçekleştirdiğinde, MFA sunucusu hello veri toohello Azure MFA bulut hizmeti tooperform hello doğrulama gönderir. Bu kimlik doğrulama istekleri toohello bulut hizmetine gönderildiğinde, böylece hello Müşteri'nin kimlik doğrulama/kullanım raporlarında kullanılabilir hello aşağıdaki alanları hello istekte ve günlüklerde gönderilir. Bunlar etkinleştirilebilir veya çok faktörlü kimlik doğrulama sunucusu hello içinde devre dışı şekilde bazı hello alanlar isteğe bağlıdır. Merhaba MFA sunucusu toohello MFA bulut hizmeti Hello iletişim 443 giden bağlantı noktası üzerinden SSL/TLS kullanır. Bu alanlar aşağıdaki gibidir:

* Benzersiz Kimlik - kullanıcı adı veya iç MFA sunucusu kimliği
* Adı ve soyadı (isteğe bağlı)
* E-posta adresi (isteğe bağlı)
* Telefon numarası - sesli arama veya SMS kimlik doğrulaması yapılırken
* Cihaz belirteci - Mobil uygulama kimlik doğrulaması yaparken
* Kimlik doğrulaması modu
* Kimlik doğrulaması sonucu
* MFA Sunucusu adı
* MFA Sunucusu IP’si
* İstemci IP’si - varsa

Ayrıca toohello alanları yukarıdaki hello doğrulama sonucu (başarılı/reddedildi) ve reddetme nedeni de hello kimlik doğrulama verileri birlikte depolanır ve hello kimlik doğrulama/kullanım raporları ile de kullanılabilir.

## <a name="back-up-and-restore-azure-mfa-server"></a>Azure MFA Sunucusunu yedekleme ve geri yükleme

İyi bir yedeğiniz olduğundan emin olma önemli adım tootake sistemiyle olur.

Azure MFA sunucusu tooback olun hello bir kopyasına sahip **C:\Program Files\Multi-Factor Authentication Server\Data** hello dahil olmak üzere klasörü **PhoneFactor.pfdata** dosya. 

Geri yükleme bir durumda gerekli tam hello adımları takip ediyor:

1. Azure MFA sunucusunu yeni bir sunucuya yeniden yükleyin.
2. Etkinleştirme yeni Azure MFA sunucusu hello.
3. Stop hello **MultiFactorAuth** hizmet.
4. Merhaba üzerine **PhoneFactor.pfdata** kopya yedeği hello ile.
5. Merhaba Başlat **MultiFactorAuth** hizmet.

Merhaba yeni şimdi hazır ve çalışır hello özgün yedeklenen yapılandırması ve kullanıcı verileriyle sunucusudur.

## <a name="next-steps"></a>Sonraki adımlar

- Ayarlama ve hello yapılandırma [kullanıcı portalı](multi-factor-authentication-get-started-portal.md) kullanıcı Self Servis için.
- Ayarlama ve yapılandırma ile Azure MFA sunucusu hello [Active Directory Federasyon Hizmeti](multi-factor-authentication-get-started-adfs.md), [RADIUS kimlik doğrulaması](multi-factor-authentication-get-started-server-radius.md), veya [LDAP kimlik doğrulaması](multi-factor-authentication-get-started-server-ldap.md).
- [RADIUS kullanan Uzak Masaüstü Ağ Geçidi ve Azure Multi-Factor Authentication Sunucusu](multi-factor-authentication-get-started-server-rdg.md)’nu kurun ve yapılandırın.
- [Hello Azure çok faktörlü kimlik doğrulama sunucusu mobil uygulama Web Hizmeti'ni dağıtma](multi-factor-authentication-get-started-server-webservice.md).
- [Azure Multi-Factor Authentication ve üçüncü taraf VPN’ler ile gelişmiş senaryolar](multi-factor-authentication-advanced-vpn-configurations.md).
