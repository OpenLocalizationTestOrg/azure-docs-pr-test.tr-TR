---
title: Active Directory PoC Playbook uygulama aaaAzure | Microsoft Docs
description: "Keşfetmek ve hızlı bir şekilde kimlik ve erişim yönetimi senaryoları uygulayan"
services: active-directory
keywords: "Azure active directory, playbook, kavram kanıtı, PT"
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 4d61f1432d5f1c15cd88fda4824cf1c1de64c712
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-implementation"></a>Azure Active Directory Playbook kavram kanıtı: uygulama

## <a name="foundation---syncing-ad-tooazure-ad"></a>Foundation - AD tooAzure AD eşitleniyor 

Karma kimlik hello hello kuruluş bir şirket içi dizin zaten yüklemiş olan müşterilerin çoğu temelidir. Merhaba burada toointentionally hedeftir olarak daha az zaman burada hello gerçek kimlik ve erişim senaryoları mümkün tooshow hello değeri olarak ayırın. 

| Senaryo | Yapı taşları| 
| --- | --- |  
| [Şirket içi kimlik toohello bulut genişletme](#extending-your-on-premises-identity-to-the-cloud) | [Dizin eşitleme - parola karması eşitlemesi](active-directory-playbook-building-blocks.md#directory-synchronization---password-hash-sync-phs---new-installation) <br/>**Not**: DirSync/ADSync veya Azure AD Connect'in önceki sürümlerinde zaten varsa, bu adım isteğe bağlıdır. Bu kılavuzdaki bazı senaryolar, Azure AD Connect daha yeni sürümü gerektirebilir.  <br/>[Markalama](active-directory-playbook-building-blocks.md#branding) | 
| [Grupları kullanarak Azure AD lisans atama](#assigning-azure-ad-licenses-using-groups) | [Lisans grup tabanlı](active-directory-playbook-building-blocks.md#group-based-licensing) |


### <a name="extending-your-on-premises-identity-toohello-cloud"></a>Şirket içi kimlik toohello bulut genişletme 

1. Bob hello Active Directory contoso'da yöneticisidir. Kullanıcı bir kullanıcı kümesi için bir hizmet olarak hello gereksinim tooenable kimliğini alır. Azure AD Connect Sihirbazı yürütme sonrasında hello hedef kullanıcıların kimliklerini kullanılabilir hello bulutta hello. 
2. Bob hello hedef kullanıcılar, biri Susie tooaccess Azure Active Directory'ye erişim paneli hello ve aynen doğrulanabilir onaylamak ister. Susie markalı oturum açma sayfası ve gelecekteki uygulama erişimini etkinleştirmek için hazır olan bir boş erişim paneli görür.

### <a name="assigning-azure-ad-licenses-using-groups"></a>Grupları kullanarak Azure AD lisans atama 

1. Bob hello Azure AD genel yönetici olan ve Azure ad hello ilk dağıtımının bir parçası olarak tooallocate Azure AD lisansları tooa belirli kullanıcıları kümesini istiyor.
2. Bob, pilot kullanıcıları hello için bir grup oluşturur. 
3. Bob hello lisansları toohello Grup atar
4. Merhaba bilgi çalışanları birini Susie kendi iş işlevlerinin bir parçası olarak toohello güvenlik grubuna eklenir
5. Bir süre sonra erişim toohello Azure AD premium lisansı Susie sahiptir. Bu daha hello POC senaryoları daha sonra olanak tanır.

## <a name="theme---lots-of-apps-one-identity"></a>Tema - çok sayıda uygulamalar, bir kimlik

| Senaryo | Yapı taşları| 
| --- | --- |  
| [SaaS uygulamaları - Federasyon SSO tümleştirme](#integrate-saas-applications---federated-sso) | [SaaS Federasyon SSO yapılandırma](active-directory-playbook-building-blocks.md#saas-federated-sso-configuration) <br/>[Grupları - temsilci sahipliği](active-directory-playbook-building-blocks.md#groups---delegated-ownership) |
| [SaaS uygulamaları - parola SSO tümleştirme](#integrate-saas-applications---password-sso) | [SaaS parola SSO yapılandırma](active-directory-playbook-building-blocks.md#saas-password-sso-configuration) |
| [SSO ve kimlik yaşam döngüsü olayları](#sso-and-identity-lifecycle-events) | [SaaS ve kimlik yaşam döngüsü](active-directory-playbook-building-blocks.md#saas-and-identity-lifecycle) |
| [Güvenli erişim tooShared hesapları](#secure-access-to-shared-accounts) | [SaaS paylaşılan hesaplarını yapılandırma](active-directory-playbook-building-blocks.md#saas-shared-accounts-configuration) |
| [Güvenli uzaktan erişim tooOn içi uygulamaları](#secure-remote-access-to-on-premises-applications) | [Uygulama Proxy Yapılandırması](active-directory-playbook-building-blocks.md#app-proxy-configuration) |
| [LDAP kimlik tooAzure AD Eşitle](#synchronize-ldap-identities-to-azure-ad) |  [Genel LDAP Bağlayıcısı yapılandırması](active-directory-playbook-building-blocks.md#generic-ldap-connector-configuration) |

### <a name="integrate-saas-applications---federated-sso"></a>SaaS uygulamaları - Federasyon SSO tümleştirme 

1. Bob hello Azure AD genel yönetici olan ve bir istek hello pazarlama departmanı tooenable erişim tootheir ServiceNow örneği alır. Bob hello adım adım öğretici Azure AD belgelerinde bulur ve onu izleyen ve temsilciler kullanıcılar toohello uygulama tooKevin, pazarlama ekibinin hello head atamasının hello. 
2. Kevin ServiceNow yetkilendirmeler hello sahibi olarak oturum açması ve Susie toohello uygulama atar. Susie'nın profili ServiceNow içinde otomatik olarak oluşturulmuş Kevin ayrıca bildirimler
3. Susie hello pazarlama departmanındaki bir bilgi çalışanı ' dir. Kendisi kaydeder, tooazure AD ve tüm SaaS uygulamaları aynen tooin myapps portal atanan bulur. Buradan, aynen sorunsuz bir şekilde erişim tooServiceNow alır.
4. Merhaba pazarlama departmanı ServiceNow kimin tooaudit istemektedir. Bob bir etkinlik raporu indirir ve e-posta Kevin ile paylaşır.  

### <a name="sso-and-identity-lifecycle-events"></a>SSO ve kimlik yaşam döngüsü olayları

1. Bir Mazeret Susie alır ve şirket ilkesi tarafından hello AD hesabı geçici devre dışı olan şirket içi. Susie tooAzure AD şimdi oturum açamaz ve ServiceNow etkinleştirilemez. 
2. Susie tooSales pazarlama gelen yanal hareket yapar. Kevin kendi erişim ServiceNow kaldırır. Susie hello azure ad myapps günlüğe kaydeder ve artık hello ServiceNow döşeme görür. 10 dakika sonra Susie hesap ServiceNow Yönetim Konsolu'ndan devre dışı bırakıldı Kevin onaylar.

### <a name="integrate-saas-applications---password-sso"></a>SaaS uygulamaları - parola SSO tümleştirme

1. Bob erişim tooAtlassian HipChat yapılandırır. Parola SSO tümleştirme ve grant erişim tooSusie HipChat sahip
2. Susie toohello myapps Portalı'nda günlüğe kaydeder ve bir bağlantı toodownload hello aynen indirmeleri Azure AD IE tarayıcı uzantısı görür
3. Tıklatıldığında, bunları kendi HipChat kullanıcı adı ve parola kimlik bilgileri sorulur. Bu tek seferlik bir işlemdir ve tamamladıktan sonra erişim tooHipChat olan
4. Daha sonra birkaç gün Susie myapps portal açar ve HipChat yeniden tıklar. Bu sefer orada aynen sorunsuz erişim alır
5. Kevin, hello HipChat uygulama sahibi Merhaba uygulaması kimin tooaudit istemektedir. Bob denetim raporu indirir ve e-posta Kevin ile paylaşır. 

### <a name="secure-access-tooshared-accounts"></a>Güvenli erişim tooShared hesapları 

1. Bob görevli toosecure paylaşılan hello Twitter tanıtıcı hello satış ekibinin üyeleri için değil. Kendisi Twitter SSO uygulaması ekler ve hello satış ekibi toohello güvenlik grubunun atar. Kendisine hello kimlik bilgilerini Paylaşılan toohello hesabı verilen ve kendisine hello sistemde sağlar. 
2. Twitter kimlik bilgileri paylaşımı artık farkında toomultiple kişilerin güvenilir değil. Bob hello Twitter parola otomatik geçişi sağlar.
3. Susie, hello satış ekibinin bir üyesi toohello myapps Portalı'nda günlüğe kaydeder ve bir bağlantı toodownload hello Azure AD IE tarayıcı uzantısı görür. Aynen yükler.
4. Tıklatıldığında aynen get erişim doğrudan tooTwitter. Aynen hello parola bilmez.
5. ARNOLD ayrıca hello satış ekibi bir parçasıdır. Adım 3-4 Susie aynı deneyimi hello sahip
6. Merhaba satış departmanı Twitter kimin tooaudit istemektedir. Bob bir etkinlik raporu indirir ve e-posta Kevin ile paylaşır. 

### <a name="secure-remote-access-tooon-premises-applications"></a>Güvenli uzaktan erişim tooOn içi uygulamaları

1. Bob, hello Azure AD genel yönetici, yararlı birkaç şirket içi uzaktan çalışırken Merhaba giderleri uygulaması gibi kaynaklar tooenable çalışanlar tooaccess çok sayıda isteği aldı. Kendisine hello izleyen [uygulama proxy'si belgelerine](active-directory-application-proxy-enable.md) tooinstall bağlayıcı ve giderler uygulama proxy'si uygulama yayımlama. 
2. Bob hello dış giderleri uygulama URL'si Susie ile uzaktan erişim ihtiyacı hello çalışanlar birini paylaşır. Aynen hello bağlantı erişir ve AAD karşı kimlik doğrulaması sonra kendisinin mümkün tooaccess hello giderleri uygulaması ve üretken toobe devam uzaktan oluştu. 
3. Bob, aynı işlemi ve gerektiğinde erişim toousers vermiş kullanarak toopublish ek şirket içi uygulamaları hello sonra devam eder. Kendisine koşullu erişim ve çok faktörlü kimlik doğrulamasını hello ekler kendisinin yayımlar daha duyarlı uygulamalar, tooensure ek güvenlik.

### <a name="synchronize-ldap-identities-tooazure-ad"></a>LDAP kimlik tooAzure AD Eşitle

1. Bob'ın şirket karmaşık kimlik altyapısı sahiptir. Çoğu hello kullanıcılar, Windows Server Active Directory etki alanı Hizmetleri (EKLER içinde) korunur. Bazıları, ik sistemi içindeki Active Directory Basit Dizin Hizmetleri (ADLDS) tarafından yönetilir.
2. Bob (aynı zamanda bu EKLER mevcut olmayan) tüm kullanıcılara yönelik erişim tooSaaS uygulamaların etkinleştirme ile görevli.
3. Bob Azure AD Connect ADLDS genel LDAP Bağlayıcısı toopull verileri yapılandırır.
4. LDAP kullanıcılar meta veri deposu ve tooAzure AD alanına doldurulur Bob eşitleme kuralları oluşturur, bu nedenle
5. Her SaaS uygulamasını kullanarak LDAP kullanıcının eriştiği olan Susie kimlik eşitlendi



> [!IMPORTANT] 
> Bu, FIM/MIM aşina gerektiren gelişmiş bir yapılandırmadır. Üretimde Biz bu yapılandırma hakkında sorular öneri kullandıysanız geçtikleri [Premier Destek](https://support.microsoft.com/premier).



## <a name="theme---increase-your-security"></a>Tema - artış güvenlik 

| Senaryo | Yapı taşları| 
| --- | --- |  
| [Güvenli yönetici hesabına erişimi](#secure-administrator-account-access) | [Telefon görüşmesi ile Azure MFA](active-directory-playbook-building-blocks.md#azure-multi-factor-authentication-with-phone-calls) |
| [Uygulamalar için güvenli erişim](#secure-access-to-applications) | [SaaS uygulamaları için koşullu erişim](active-directory-playbook-building-blocks.md#mfa-conditional-access-for-saas-applications) |
| [Yalnızca zaman içinde yönetim etkinleştir](#enable-just-in-time-jit-administration) | [Privileged Identity Management](active-directory-playbook-building-blocks.md#privileged-identity-management-pim) |
| [Risk üzerinde temel kimlikleri koru](#protect-identities-based-on-risk) | [Risk olaylarını keşfetme](active-directory-playbook-building-blocks.md#discovering-risk-events) <br/>[Oturum açma riski ilkelerini dağıtma](active-directory-playbook-building-blocks.md#deploying-sign-in-risk-policies) |
| [Sertifika tabanlı kimlik doğrulaması kullanarak parolaları kimlik doğrulaması](#authenticate-without-passwords-using-certificate-based-authentication) | [Sertifika tabanlı kimlik doğrulamasını yapılandırma](active-directory-playbook-building-blocks.md#configuring-certificate-based-authentication)

### <a name="secure-administrator-account-access"></a>Güvenli yönetici hesabına erişimi

1. Bob hello Azure AD genel yönetici olur. Müşterinizle Stuart hello hizmetinin ortak yönetici olarak belirledi. 
2. Bob tooalways MFA tooimprove hello güvenlik tutumunu gerektiren Stuart'ın hesabını yapılandırır
3. Kendi telefon numarası toocontinue hello oturum açma Stuart kaydeder toohello Azure portal ve tooregister gerektiğini bildirimler
4. Stuart sonraki oturum açmayı artık çok faktörlü kimlik doğrulamasıyla korunur ve kendisine şimdi bir telefon araması tooverify kendi kimliğini alır.

### <a name="secure-access-tooapplications"></a>Güvenli erişim tooapplications

1. Kevin hello iş ServiceNow sahibidir. Merhaba şirket, bu kullanıcıların toologin MFA ile artık hello kurumsal ağ dışından erişirken istemektedir.
2. Bir koşullu erişim ilkesi toohello ServiceNow uygulama tooenable MFA dışından erişim için Bob, bizim Azure AD genel yönetici ekler
3. Susie, bizim bilgi çalışanı uygulamaları portalımı günlüğe kaydeder ve hello ServiceNow döşeme tıklar. Aynen yüküyle şimdi MFA ile.

### <a name="enable-just-in-time-jit-administration"></a>Zamanında (JIT) yönetiminde sadece etkinleştir

1. Bob ve Fatih Azure AD genel yönetici yaşıyor. Tooenable JIT erişim toohello yönetim rolleri istedikleri ve aynı zamanda roller hello hello kullanımını tookeep kayıtlarda ayrıcalıklı.
2. Bob hello Güvenlik Yöneticisi olur ve PIM hello Azure AD kiracısında sağlar. Hatay kendisi ve Fatih'ın genel yönetici rolü üyeliği kalıcı tooeligible çevirir.
3. Bob ve Fatih şimdi gerektiren herhangi yapılması tooAzure AD değiştirmeden önce rollerine hello Azure portal üzerinden etkinleştirme yapılandırması. 

### <a name="protect-identities-based-on-risk"></a>Risk üzerinde temel kimlikleri koru 

1. Susie, tor tarayıcıdan oturum açmayı bir bilgi çalışanı çalışır. 
2. Bob hello Azure AD Identity protection Panosu denetler ve anonim bir IP adresinden Susie'nın oturum açma görür. MFA ile kullanıcıların toochallenge böyle erişen Hello güvenlik ekibine istediği
3. Orta veya yüksek risk olayları için Azure AD Identity Protection ilkesini toochallenge MFA Bob sağlar
4. Zaman gider ve Susie Tor tarayıcıdan yeniden bağlanır. Bu süre, aynen görürsünüz hello MFA sınama

### <a name="authenticate-without-passwords-using-certificate-based-authentication"></a>Sertifika tabanlı kimlik doğrulaması kullanarak parolaları kimlik doğrulaması

1. Bob için parola kullanımını bir kimlik doğrulama faktörü olarak uygulamalarını engelliyor finansal kuruluştan, genel yönetici içindir.
2. Bob etkinleştirir ve ADFS ve Azure AD sertifika kimlik doğrulamasını zorunlu kılar
3. Uygulamaya erişmeyi olsa Susie sertifikayla tooauthenticate istenir

## <a name="theme---scale-with-self-service"></a>Tema - Self Servis ölçekli

| Senaryo | Yapı taşları| 
| --- | --- |  
| [Self Servis parola sıfırlama](#self-service-password-reset) | [Self Servis parola sıfırlama](active-directory-playbook-building-blocks.md#self-service-password-reset) |
| [Self Servis erişim tooApplications](#self-service-access-to-applications) | [Self Servis erişim tooApplications](active-directory-playbook-building-blocks.md#self-service-access-to-application-management) |

### <a name="self-service-password-reset"></a>Self Servis parola sıfırlama 

1. Bob hello Azure AD genel yönetici ve etkinleştirir Self Servis parola yönetimi tooa kullanıcı alt kümesini Susie dahil olmak üzere, ' dir. 
2. Olayların gelecekte parola sıfırlama için Susie toomyapps portal bkz: ileti tooregister kendi güvenlik bilgileri kaydeder ve.
3. Sar birkaç gün Susie kendi parolayı unutması ve Azure AD Portalı aracılığıyla sıfırlar

### <a name="self-service-access-tooapplications"></a>Self Servis erişim tooApplications 

1. Kevin hello iş ServiceNow sahibidir. Kullanıcılar çok "için aynı anda eklemek yerine isteğe bağlı oturum" istediği
2. Bob, bizim Azure AD genel yönetici değiştirir hello ServiceNow uygulama tooenable self servis istekleri
3. Uygulamaları portalımı Susie, bizim bilgi çalışanı günlüğe kaydeder ve tıklama "daha fazla uygulama Ekle" düğmesi hello ve ServiceNow uygulamalar önerilen hello biri olarak bakın. Ardından kendisinin geri toomy uygulamaları portal gider ve Merhaba ServiceNow uygulaması bakın.

[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]