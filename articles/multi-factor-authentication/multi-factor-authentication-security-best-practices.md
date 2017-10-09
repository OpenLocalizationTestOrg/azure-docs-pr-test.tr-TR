---
title: "MFA için en iyi uygulamaları aaaSecurity | Microsoft Docs"
description: "Bu belgede Azure MFA ile Azure hesaplarını kullanarak geçici en iyi yöntemler sağlar"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3be7d968-96bb-4320-8701-869fd04a2595
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 7f18c2592764878b842d81783b321a05f29ee3d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-best-practices-for-using-azure-multi-factor-authentication-with-azure-ad-accounts"></a>Azure AD hesapları ile Azure çok faktörlü kimlik doğrulaması kullanmak için güvenlik en iyi uygulamalar

İki aşamalı doğrulama, kendi kimlik doğrulama işlemi tooenhance istediğiniz çoğu kuruluş için tercih edilen hello seçimdir. Azure multi-Factor Authentication (MFA), kullanıcılar için basit bir oturum açma deneyimi sağlarken kendi güvenlik ve uyumluluk gereksinimlerini karşılayan şirketler yardımcı olur. Bu makalede Azure MFA hello benimseme için planlarken göz önünde bulundurmanız bazı ipuçları yer almaktadır.

## <a name="deploy-azure-mfa-in-hello-cloud"></a>Merhaba bulutta Azure MFA dağıtma

İki yolu tooenable Azure MFA tüm kullanıcılarınız için vardır.

* Her bir kullanıcı (ya da Azure MFA, Azure AD Premium veya Enterprise Mobility + Security) için lisans satın alma
* Multi-Factor Auth sağlayıcısı ve ödeme kullanıcı başına veya kimlik doğrulaması başına oluşturur.

### <a name="licenses"></a>Lisansları
![EMS](./media/multi-factor-authentication-security-best-practices/ems.png)

Azure AD Premium veya Enterprise Mobility + güvenlik lisansları varsa zaten Azure MFA gerekir. Kuruluşunuz, herhangi bir şey ek tooextend hello iki aşamalı doğrulama yetenek tooall kullanıcılar gerek yoktur. Yalnızca tooassign lisans tooa kullanıcı gerekir ve ardından MFA üzerinde kapatabilirsiniz.

Çok faktörlü kimlik doğrulamayı ayarlama, ipuçları aşağıdaki hello göz önünde bulundurun:

* Bir kimlik doğrulaması başına çok faktörlü yetki sağlayıcı oluşturmayın. Bunu yaparsanız, doğrulama istekleri zaten lisanslara sahip kullanıcılardan ödeme bitiş.
* Tüm kullanıcılar için yeterince lisansa sahip değilseniz, bir kullanıcı başına çok faktörlü yetki sağlayıcı toocover hello rest, kuruluşunuzun oluşturabilirsiniz. 
* Azure AD Connect, yalnızca bir Azure AD dizini ile şirket içi Active Directory ortamınızı eşitlenip eşitlenmediğini gerekli. Şirket içi örneğini Active Directory ile eşitlenmemiş bir Azure AD dizini kullanıyorsanız, Azure AD Connect gerekmez.

### <a name="multi-factor-auth-provider"></a>Multi-Factor Auth sağlayıcısı
![Multi-Factor Auth sağlayıcısı](./media/multi-factor-authentication-security-best-practices/authprovider.png)

Daha sonra Azure MFA dahil lisansları yoksa, MFA kimlik doğrulama sağlayıcısı oluşturabilirsiniz. 

Merhaba Auth sağlayıcısı oluştururken, tooselect bir dizin gerekir ve aşağıdaki ayrıntılara hello göz önünde bulundurun:

* Azure AD directory toocreate multi-Factor Auth sağlayıcısı gerekli değildir, ancak daha fazla işlevsellik biriyle alın. Merhaba Auth sağlayıcısı Azure AD dizini ile ilişkilendirdiğinizde özellikler aşağıdaki hello etkinleştirilir:  
  * Kullanıcılarınızın iki aşamalı doğrulama tooall genişletme  
  * Genel Yöneticiler hello Yönetim Portalı, özel Karşılama ve raporlar gibi ek özellikler sunar.
* Şirket içi Active Directory ortamınızı bir Azure AD diziniyle eşitliyorsanız DirSync veya AAD eşitleme gerekir. Şirket içi örneğini Active Directory ile eşitlenmemiş bir Azure AD dizini kullanıyorsanız, DirSync veya AAD eşitleme gerekmez.
* En iyi şekilde, iş gereksinimlerinize en uygun hello tüketim modelini seçin. Merhaba kullanım modeli seçtikten sonra değiştiremezsiniz. Merhaba iki model şunlardır:
  * Kimlik doğrulaması başına: her doğrulama için giderler. Bu model, belirli kullanıcılar için değil, belirli bir uygulama erişen herkesin için iki aşamalı doğrulamayı istiyorsanız kullanın.
  * Etkin kullanıcı başına: Azure MFA için etkinleştirme her bir kullanıcı için giderler. Bazı kullanıcılar Azure AD Premium veya Enterprise Mobility Suite lisansları ve bazı olmadan varsa, bu model kullanın.

### <a name="supportability"></a>Desteklenebilirlik
Kullanıcıların çoğunun alışkın toousing yalnızca parolaları tooauthenticate olduğundan, şirketinizin tooall kullanıcıların bu işlemi ile ilgili bilgi sağlar önemlidir. Bu tanıma kullanıcılar Önemsiz sorunları ilgili tooMFA için Yardım masanıza başvurun hello olasılığını azaltır. Ancak, geçici olarak MFA devre dışı bırakma gerekli olduğu bazı senaryolar vardır. Yönergeleri toounderstand nasıl aşağıdaki kullanım hello toohandle bu senaryoları:

* Merhaba mobil uygulaması ya da telefon bildirim veya telefon görüşmesi almıyor çünkü burada hello kullanıcı oturum açamaz teknik destek personeli toohandle senaryolarınızı eğitmek. Teknik destek için [bir kerelik geçiş etkinleştirmek](multi-factor-authentication-whats-next.md#one-time-bypass) tooallow kullanıcı tooauthenticate "iki aşamalı doğrulamayı atlayarak" tarafından tek bir kez. Merhaba atlama geçicidir ve belirtilen sayıda saniye geçtikten sonra süresi dolar.
* Merhaba göz önünde bulundurun [güvenilen IP'leri yetenek](multi-factor-authentication-whats-next.md#trusted-ips) şekilde toominimize iki aşamalı doğrulamayı olarak Azure MFA içinde. Bu özellikle, yönetilen ya da Federasyon Kiracı Yöneticiler hello şirketin yerel intranetten imzalama kullanıcılar için iki aşamalı doğrulamayı devre dışı bırakabilir. Merhaba özellikleri, Azure AD Premium, Enterprise Mobility Suite ya da Azure multi-Factor Authentication lisanslara sahip Azure AD kiracılar için kullanılabilir.

## <a name="best-practices-for-an-on-premises-deployment"></a>Bir şirket içi dağıtım için en iyi yöntemler
Daha sonra şirket tooleverage kendi altyapı tooenable MFA karar verdiyseniz, Azure multi-Factor Authentication sunucusu şirket içi toodeploy gerekir. Merhaba MFA sunucusu bileşenleri diyagramı aşağıdaki hello gösterilir:

![Varsayılan MFA sunucusu bileşenleri: konsol, eşitleme altyapısı, Yönetim Portalı, bulut hizmeti](./media/multi-factor-authentication-security-best-practices/server.png) \*varsayılan olarak yüklenmeyen \** varsayılan olarak etkin değildir ancak yüklü

Azure multi-Factor Authentication sunucusu bulut Federasyon kullanarak kaynaklarına ve şirket içi kaynakların güvenliğini sağlayabilirsiniz. AD FS sahip ve Azure AD kiracınıza Federasyon olması gerekir.
Çok faktörlü kimlik doğrulama sunucusu kurma, aşağıdaki ayrıntılara hello göz önünde bulundurun:

* Merhaba ilk doğrulama adımı gerçekleştirilen sonra Active Directory Federasyon Hizmetleri (AD FS) kullanarak Azure AD kaynaklarını güvenli hale getirme, AD FS kullanarak şirket içi. Merhaba ikinci adım, hello talebi onaylanmasıyla şirket içi gerçekleştirilir bağlıdır.
* Tooinstall hello Azure multi-Factor Authentication sunucusu, AD FS federasyon sunucusu yok. Ancak, AD FS için multi-Factor Authentication bağdaştırıcısı hello bir Windows Server 2012 AD FS çalıştıran R2 üzerinde yüklü olmalıdır. Desteklenen bir sürüm olduğu sürece hello sunucu başka bir bilgisayara yükleyin ve hello AD FS bağdaştırıcısını ayrı olarak AD FS federasyon sunucunuz üzerinde yükleyin. 
* Merhaba multi-Factor Authentication AD FS Bağdaştırıcısı Yükleme Sihirbazı, Active Directory'de PhoneFactor Admins adlı bir güvenlik grubu oluşturur ve AD FS hizmet hesabı toothis grubunuzun ekler. Hello PhoneFactor Admins grubu, etki alanı denetleyicisinde oluşturulan ve bu hello AD FS hizmet hesabının bu grubun üyesi olduğunu doğrulayın. Gerekirse, hello AD FS hizmet hesabı toohello PhoneFactor Admins grubu, etki alanı denetleyicisinde el ile ekleyin.

### <a name="user-portal"></a>Kullanıcı Portalı
Merhaba Kullanıcı Portalı Self Servis kapasitelerini ve tam bir kullanıcı yönetimi özellik kümesi sağlar. Bir Internet Information Server (IIS) web sitesini çalıştırır. Bu bileşen yönergeleri tooconfigure aşağıdaki hello kullan:

* IIS 6 veya daha büyük kullanın
* Yükleyin ve ASP.NET v2.0.507207 kaydedin
* Bu sunucuyu bir çevre ağında dağıtılan emin olun

### <a name="app-passwords"></a>Uygulama parolaları
Kuruluşunuz SSO Azure AD ile birleştirildiyse ve Azure MFA kullanma toobe kalacaklarını, ardından aşağıdaki ayrıntılara Merhaba dikkat edin:

* Merhaba uygulama parolası, Azure AD tarafından doğrulanır ve bu nedenle Federasyon atlar. Federasyon yalnızca uygulama parolaları ayarlarken kullanılır.
* Federasyon (SSO) kullanıcıları için parolalar hello kuruluş kimliği saklanır. Merhaba kullanıcı hello şirketten ayrılırsa, bu bilgileri DirSync kullanarak tooflow tooorganizational kimliği var. Hesap devre dışı bırakma/silme, devre dışı bırakma/silme, uygulama parolaları Azure AD'de gecikmeler toothree saatleri toosync yukarı sürebilir.
* Şirket için İstemci Erişimi Denetimi ayarları Uygulama Parolası tarafından onaylanmaz.
* Günlüğe kaydetme ve denetim şirket içi kimlik doğrulama özelliği için uygulama parolaları kullanılabilir.
* Bazı gelişmiş mimari tasarımları istemcilerle burada kimlik doğrulamasında bağlı olarak iki aşamalı doğrulamayı kullanırken, kuruluş kullanıcı adı ve parolaları ve uygulama parolaları birleşimini kullanarak gerektirebilir. Bir şirket içi altyapı karşı kimlik doğrulaması istemcileri için bir kuruluş kullanıcı adı ve parola kullanırsınız. Azure AD karşı kimlik doğrulaması istemcileri için hello uygulama parolası kullanırsınız.
* Varsayılan olarak, kullanıcıların uygulama parolaları oluşturulamıyor. Tooallow kullanıcılar toocreate uygulama parolaları gereksinim duyarsanız, hello seçin **tarayıcı olmayan uygulamalara kullanıcıların toocreate uygulama parolaları toosign izin** seçeneği.

## <a name="additional-considerations"></a>Ek hususlar
Ek hususlar için bu listeyi kullanın ve şirket içi yönergeler her bileşen için dağıtılabilir:

- Azure Multi-Factor Authentication’ı [Active Directory Federasyon Hizmetleri](multi-factor-authentication-get-started-adfs.md) ile ayarlayın.
- Ayarlama ve yapılandırma ile Azure MFA sunucusu hello [RADIUS kimlik doğrulaması](multi-factor-authentication-get-started-server-radius.md).
- Ayarlama ve yapılandırma ile Azure MFA sunucusu hello [IIS kimlik doğrulaması](multi-factor-authentication-get-started-server-iis.md).
- Ayarlama ve yapılandırma ile Azure MFA sunucusu hello [Windows kimlik doğrulaması](multi-factor-authentication-get-started-server-windows.md).
- Ayarlama ve yapılandırma ile Azure MFA sunucusu hello [LDAP kimlik doğrulaması](multi-factor-authentication-get-started-server-ldap.md).
- Ayarlama ve yapılandırma ile Azure MFA sunucusu hello [Uzak Masaüstü Ağ geçidi ve Azure multi-Factor Authentication sunucusu RADIUS kullanan](multi-factor-authentication-get-started-server-rdg.md).
- Ayarlama ve hello Azure MFA sunucusu arasında eşitlemeyi yapılandırın ve [Windows Server Active Directory](multi-factor-authentication-get-started-server-dirint.md).
- [Hello Azure çok faktörlü kimlik doğrulama sunucusu mobil uygulama Web Hizmeti'ni dağıtma](multi-factor-authentication-get-started-server-webservice.md).
- [Gelişmiş VPN yapılandırma Azure çok faktörlü kimlik doğrulamasıyla](multi-factor-authentication-advanced-vpn-configurations.md) LDAP veya RADIUS kullanarak Cisco ASA, Citrix Netscaler ve Juniper/Pulse Secure VPN cihazları için.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, Azure MFA için bazı en iyi uygulamaları vurgular olsa da, MFA dağıtımınızı planlarken kullanabileceğiniz kaynaklar vardır. Merhaba aşağıda bu süreçte yardımcı olabilecek bazı anahtar makaleler vardır:

* [Azure multi-Factor Authentication raporlarında](multi-factor-authentication-manage-reports.md)
* [Merhaba iki aşamalı doğrulama kayıt deneyimi](multi-factor-authentication-end-user-first-time.md)
* [Azure çok faktörlü kimlik doğrulaması ile ilgili SSS](multi-factor-authentication-faq.md)

