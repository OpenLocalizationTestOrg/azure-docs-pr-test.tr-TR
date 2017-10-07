---
title: "Azure Active Directory'de uygulama yönetimi için dizin aaaArticle | Microsoft Azure"
description: "Nasıl toocustomize hello sona erme tarihini, Federasyon sertifikalarını ve nasıl toorenew sertifikalar yakında dolacak öğrenin."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 5321b8e4-2afa-4dfe-8d53-4add7abb5ec8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: f8a584baa94dc50e279899074f50160978256559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="article-index-for-application-management-in-azure-active-directory"></a>Azure Active Directory'de Uygulama Yönetimi için Makale Dizini
Bu sayfa, Azure Active Directory (Azure AD) çeşitli uygulama ile ilgili özellikler hakkında hello yazılan her belge kapsamlı bir listesini sağlar.

Bir kısa giriş tooeach önemli özellik alanı yanı sıra, aradığınız hangi bilgilere bağlı olarak hangi makaleleri tooread yönergeler yoktur.

## <a name="overview-articles"></a>Genel Bakış makaleleri
Merhaba makaleleri aşağıdaki iyi yalnızca Azure AD uygulama yönetimi özelliklerinden kısa bir açıklama istediğiniz olanlar için başlangıç noktaları.

| Makale Kılavuzu |  |
|:---:| --- |
| Azure AD çözdü bir giriş toohello uygulama yönetimi sorunları |[Azure Active Directory (AD) ile uygulamaları yönetme](active-directory-enable-sso-scenario.md) |
| Merhaba genel bir bakış tooenabling çoklu oturum açma izni olan tanımlama özelliğini, Azure AD'de çeşitli özellikler ilgili erişim tooapps ve kullanıcıların uygulamaları nasıl başlatma |[Uygulama erişimi ve Azure Active Directory'de çoklu oturum açma](active-directory-appssoaccess-whatis.md) |
| Merhaba farklı adımlar uygulamaları Azure AD ile tümleştirdiğinizde bakma |[Azure Active Directory uygulamaları ile tümleştirme](active-directory-integrating-applications-getting-started.md)<br /><br />[Çoklu oturum açma tooSaaS uygulamaları etkinleştirme](active-directory-sso-integrate-saas-apps.md)<br /><br />[Erişim tooApps yönetme](active-directory-managing-access-to-apps.md) |
| Uygulamaları Azure AD'de nasıl temsil edildiğini bir teknik açıklama |[Uygulamaları tooAzure AD neden ve nasıl eklenir](active-directory-how-applications-are-added.md) |

## <a name="troubleshooting-articles"></a>Sorun giderme makaleleri
Bu bölümde toorelevant sorun giderme kılavuzları hızlı erişim sağlar. Bu sayfayı hello geri kalan her özellik alanı hakkında daha fazla bilgi bulunabilir.

| Özellik alanı |  |
|:---:| --- |
| Federasyon çoklu oturum açma |[Sorun giderme SAML tabanlı çoklu oturum açma](active-directory-saml-debugging.md) |
| Parola tabanlı çoklu oturum açma |[Merhaba erişim paneli uzantısı Internet Explorer için sorun giderme](active-directory-saas-ie-troubleshooting.md) |
| Uygulama Proxy'si |[Uygulama Proxy sorun giderme kılavuzu](active-directory-application-proxy-troubleshoot.md) |
| Çoklu oturum açma şirket içi arasında AD ve Azure AD |[Parola eşitleme sorunlarını giderme](connect/active-directory-aadconnectsync-implement-password-synchronization.md#troubleshoot-password-synchronization)<br /><br />[Parola geri yazma sorunlarını giderme](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| Dinamik grup üyelikleri |[Dinamik grup üyeliklerini sorunlarını giderme](active-directory-accessmanagement-troubleshooting.md) |

## <a name="single-sign-on-sso"></a>Çoklu Oturum Açma (SSO)
### <a name="federated-single-sign-on-sign-into-many-apps-using-one-identity"></a>Federasyon çoklu oturum açma: Oturum bir kimlik kullanarak birçok uygulamaları açın
Çoklu oturum açma çeşitli uygulamaları ve Hizmetleri yalnızca bir kimlik bilgileri kümesi kullanarak kullanıcıların tooaccess sağlar. Federasyon, çoklu oturum açma etkinleştirebilirsiniz bir yöntemdir. Kullanıcılar Federasyon uygulamalarda toosign çalıştığında, bunlar Azure Active Directory'de olan ve daha sonra başarılı bir kimlik doğrulaması sırasında yeniden yönlendirilen geri toohello uygulama tarafından işlenen yeniden yönlendirilen tootheir kuruluşunuzun resmi oturum açma sayfası alırsınız.

| Makale Kılavuzu |  |
|:---:| --- |
| Bir giriş toofederation ve diğer türleri oturum açma |[Azure AD ile çoklu oturum açma](active-directory-appssoaccess-whatis.md) |
| SaaS uygulamaları ile Azure AD ile önceden tümleştirilmiş binlerce Basitleştirilmiş tek oturum açma yapılandırma adımları |[Hello Azure AD uygulama Galerisi'ni kullanmaya başlama](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)<br /><br />[Federasyon desteği önceden tümleştirilmiş uygulamaların tam listesi](http://aka.ms/aadfederatedapps)<br /><br />[Nasıl tooAdd uygulamanızı toohello Azure AD uygulama galerisinde](active-directory-app-gallery-listing.md) |
| 150'den fazla uygulama öğreticileri nasıl tooconfigure çoklu oturum açma uygulamalar gibi üzerinde [Salesforce](active-directory-saas-salesforce-tutorial.md), [ServiceNow](active-directory-saas-servicenow-tutorial.md), [Google Apps](active-directory-saas-google-apps-tutorial.md), [Workday](active-directory-saas-workday-tutorial.md)ve çok daha fazlası |[İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md) |
| Nasıl toomanually ayarlama ve çoklu oturum açma yapılandırmanızı özelleştirin |[Nasıl tooConfigure federe çoklu oturum açma tooApps hello Azure Active Directory Uygulama galerisinde bulunmayan](active-directory-saas-custom-apps.md)<br /><br />[İçinde talep tooCustomize verilen nasıl Pre-Integrated uygulamalar için SAML belirteci hello](active-directory-saml-claims-customization.md) |
| Merhaba SAML protokolünü kullanan Federasyon uygulamaları için sorun giderme kılavuzu |[Sorun giderme SAML tabanlı çoklu oturum açma](active-directory-saml-debugging.md) |
| Nasıl tooconfigure uygulamanızın sertifikanın sona erme tarihi ve nasıl toorenew sertifikalarınızı |[Federasyon tek oturum açma için Azure Active Directory'de sertifikaları yönetme](active-directory-sso-certs.md) |

Federasyon çoklu oturum açma için Azure AD kullanıcı başına tooten uygulamaları Yukarı'nin tüm sürümlerinde kullanılabilir. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) sınırsız uygulamaları destekler. Kuruluşunuzun varsa [Azure AD temel](https://azure.microsoft.com/pricing/details/active-directory/) veya [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), yapabilecekleriniz sonra [kullanım grupları tooassign erişim toofederated uygulamaları](#managing-access-to-applications).

### <a name="password-based-single-sign-on-account-sharing-and-sso-for-non-federated-apps"></a>Parola tabanlı çoklu oturum açma: hesap paylaşımı ve SSO Federasyon olmayan uygulamalar için
Federasyon, parolaları tooSaaS uygulamaları güvenli bir şekilde depolamak ve otomatik olarak kullanıcılar konusu uygulamalarda oturum Azure AD teklifleri parola yönetimi özellikleri desteklemeyen tooenable tek oturum açma tooapplications. Kolayca yeni oluşturulan hesaplar için kimlik bilgilerini dağıtmak ve takım hesapları birden çok kişiyle paylaşabilirsiniz. Kullanıcılar, erişimi verilir tooknow hello kimlik bilgilerini toohello hesapları mutlaka gerekmez.

| Makale Kılavuzu |  |
|:---:| --- |
| Bir giriş toohow parola tabanlı SSO çalışır ve kısa bir teknik genel bakış |[Parola tabanlı çoklu oturum açma Azure AD ile](active-directory-appssoaccess-whatis.md#password-based-single-sign-on) |
| Hello senaryoları özetini ilgili tooaccount paylaşımı ve bu sorunları Azure AD tarafından nasıl çözülür |[Azure AD ile hesapları paylaşma](active-directory-sharing-accounts.md) |
| Merhaba parola belirli uygulamalar için düzenli aralıklarla otomatik olarak değiştir |[Otomatik parola Rollover (Önizleme)](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/) |
| Dağıtım ve Kılavuzlar hello Azure AD parola yönetimi uzantısı hello Internet Explorer sürümüne yönelik sorun giderme |[Nasıl tooDeploy hello erişim paneli uzantısı Grup İlkesi'ni kullanarak Internet Explorer için](active-directory-saas-ie-group-policy.md)<br /><br />[Merhaba erişim paneli uzantısı Internet Explorer için sorun giderme](active-directory-saas-ie-troubleshooting.md) |

Parola tabanlı çoklu oturum açma için Azure AD kullanıcı başına tooten uygulamaları Yukarı'nin tüm sürümlerinde kullanılabilir. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) sınırsız uygulamaları destekler. Kuruluşunuzun varsa [Azure AD temel](https://azure.microsoft.com/pricing/details/active-directory/) veya [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), yapabilecekleriniz sonra [kullanım grupları tooassign erişim tooapplications](#managing-access-to-applications). Otomatik parola geçiş bir [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) özelliği.

### <a name="app-proxy-single-sign-on-and-remote-access-tooon-premises-applications"></a>Uygulama Ara sunucusu: Çoklu oturum açma ve Uzaktan erişim tooon içi uygulamalar
Ardından özel ağınızdaki kullanıcılar ve cihazlar hello Ağ dışından tarafından erişilen toobe gereken uygulamalarınız varsa, Azure AD uygulama proxy'si tooenable güvenli uzaktan erişim toothose uygulamaları kullanabilirsiniz.

| Makale Kılavuzu |  |
|:---:| --- |
| Azure AD uygulama proxy'si ve nasıl çalıştığı genel bakış |[Tooon içi uygulamalara güvenli uzaktan erişim sağlama](active-directory-application-proxy-get-started.md) |
| Öğreticiler nasıl tooconfigure uygulama proxy'si ve nasıl toopublish ilk uygulamanızı |[Nasıl tooSet Azure AD uygulaması Proxy ayarlama](active-directory-application-proxy-enable.md)<br /><br />[Nasıl tooSilently yükleme hello uygulama Proxy Bağlayıcısı](active-directory-application-proxy-silent-installation.md)<br /><br />[Nasıl tooPublish uygulaması proxy'si kullanarak uygulamalar](active-directory-application-proxy-publish.md)<br /><br />[Nasıl tooUse kendi etki alanı adı](active-directory-application-proxy-custom-domains.md) |
| Uygulama Ara sunucusu ile yayımlanan nasıl tooenable tek uygulamalar için oturum açma ve koşullu erişim |[Çoklu oturum açma uygulama proxy'si ile uygulama](active-directory-application-proxy-sso-using-kcd.md)<br /><br />[Koşullu erişim ve uygulama proxy'si](active-directory-application-proxy-conditional-access.md) |
| Nasıl hakkında yönergeler senaryoları aşağıdaki hello için uygulama proxy'si toouse |[Nasıl tooSupport yerel istemci uygulamaları](active-directory-application-proxy-native-client.md)<br /><br />[Nasıl tooSupport talep kullanan uygulamalar](active-directory-application-proxy-claims-aware-apps.md)<br /><br />[Ayrı ağlar ve konumları nasıl yayımlanan tooSupport uygulamaları](active-directory-application-proxy-connectors.md) |
| Uygulama proxy'si için sorun giderme kılavuzu |[Uygulama Proxy sorun giderme kılavuzu](active-directory-application-proxy-troubleshoot.md) |

Uygulama proxy'si için Azure AD kullanıcı başına tooten uygulamaları Yukarı'nin tüm sürümlerinde kullanılabilir. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) sınırsız uygulamaları destekler. Kuruluşunuzun varsa [Azure AD temel](https://azure.microsoft.com/pricing/details/active-directory/) veya [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), yapabilecekleriniz sonra [kullanım grupları tooassign erişim tooapplications](#managing-access-to-applications).

De ilginizi çekebilir [Azure AD etki alanı Hizmetleri](../active-directory-domain-services/active-directory-ds-overview.md), olanak sağlayan toomigrate hala hello kimlik çağıran çalışırken, şirket içi uygulamalar tooAzure bu uygulamaları gerekir.

### <a name="enabling-single-sign-on-between-azure-ad-and-on-premises-ad"></a>Çoklu oturum açma Azure AD arasında etkinleştirme ve şirket içi AD
Kuruluşunuzun şirket içi hello bulut Azure Active Directory'yi birlikte Windows Server Active Directory koruyorsa, ardından, büyük olasılıkla tooenable çoklu oturum açma bu iki sistem arasında isteyeceksiniz. Azure AD Connect (Bu iki sistemleri birlikte tümleştirir hello aracı), çoklu oturum açmayı ayarlama için birden çok seçenek sunar: ADFS veya başka bir Federasyon sağlayıcı Federasyon kurmak veya parola eşitlemeyi etkinleştir.

| Makale Kılavuzu |  |
|:---:| --- |
| Karma ortamlar yönetme hakkında bilgi yanı sıra Azure AD Connect, sunulan hello tek oturum açma seçenekleri hakkında genel bakış |[Kullanıcı oturum açma seçenekleri Azure AD'de Bağlan](active-directory-aadconnect-user-signin.md) |
| Her ikisi de ortamlarıyla yönetmek için genel rehberlik Active Directory ve Azure Active Directory şirket içi |[Azure AD karma kimlik tasarımı hakkında dikkat edilecek noktalar](active-directory-hybrid-identity-design-considerations-overview.md)<br /><br />[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) |
| Parola Eşitleme tooenable SSO kullanma yönergeleri |[Azure AD ile parola eşitlemeyi uygulama Bağlan](active-directory-aadconnectsync-implement-password-synchronization.md)<br /><br />[Parola eşitleme sorunlarını giderme](https://support.microsoft.com/en-us/kb/2855271) |
| Parola geri yazma tooenable SSO kullanma yönergeleri |[Azure AD'de parola yönetimine Başlarken](active-directory-passwords-getting-started.md)<br /><br />[Parola Geri Yazma Sorunlarını Giderme](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| Üçüncü taraf kimlik sağlayıcıları tooenable SSO kullanma yönergeleri |[Çoklu oturum açma uyumlu üçüncü taraf kimlik sağlayıcıları, kullanılabilir tooEnable listesi](https://aka.ms/ssoproviders) |
| Windows 10 kullanıcıları hello yararları tek oturum açma aracılığıyla Azure AD katılımını nasıl keyfini çıkarabilirsiniz |[Bulut özelliklerini tooWindows 10 cihaz Azure Active Directory katılım aracılığıyla genişletme](active-directory-azureadjoin-overview.md) |

Azure AD Connect için kullanılabilir [Azure Active Directory'nin tüm sürümlerinde](https://azure.microsoft.com/pricing/details/active-directory/). Azure AD Self Servis parola sıfırlama için kullanılabilir [Azure AD temel](https://azure.microsoft.com/pricing/details/active-directory/) ve [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/). Parola geri yazma tooon içi ad bir [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) özelliği.

### <a name="conditional-access-enforce-additional-security-requirements-for-high-risk-apps"></a>Koşullu erişim: yüksek riskli uygulamalar için ek güvenlik gereksinimleri uygulama
Çoklu oturum açma tooyour uygulamalar ve kaynaklar ayarladıktan sonra, ardından daha duyarlı uygulamalar her oturum açma toothat uygulama belirli güvenlik gereksinimlerine zorlayarak güvenliğini sağlayabilirsiniz. Örneğin, Azure AD toodemand tüm erişim tooa belirli uygulama her zaman gerektiğini çok faktörlü kimlik doğrulaması, bu uygulama bu işlevselliği innately destekleyip desteklemediğini bağımsız olarak kullanabilirsiniz. Başka bir ortak koşullu erişim kullanıcıların bağlı toohello kuruluşunuzun olması toorequire sipariş tooaccess ağında özellikle duyarlı bir uygulamaya güvenilen örnektir.

| Makale Kılavuzu |  |
|:---:| --- |
| Bir giriş toohello koşullu erişim yetenekleri sunulan Azure AD arasında Office365 ve Intune |[Koşullu erişim ile risk yönetme](active-directory-conditional-access.md) |
| Nasıl tooenable koşullu erişim için kaynak türleri aşağıdaki hello |[SaaS uygulamaları için koşullu erişim](active-directory-conditional-access-azuread-connected-apps.md)<br /><br />[Office 365 Hizmetleri için koşullu erişim](active-directory-conditional-access-device-policies.md)<br /><br />[Şirket içi uygulamalar için koşullu erişim](active-directory-conditional-access.md)<br /><br />[Azure AD uygulama proxy'si şirket içi uygulamalar için koşullu erişim yayımlanan](active-directory-application-proxy-conditional-access.md) |

| Azure Active Directory'de tooregister aygıtlarla tooenable cihaz temelli koşullu erişim ilkelerini nasıl sipariş | [Azure Active Directory cihaz kaydı genel bakış](active-directory-conditional-access-device-registration-overview.md)<br /><br />[Nasıl tooEnable etki alanına katılmış Windows cihazlar için otomatik cihaz kaydı](active-directory-conditional-access-automatic-device-registration.md)<br />— [Adımları için Windows 8.1 cihazları](active-directory-conditional-access-automatic-device-registration-setup.md)<br />— [Adımları için Windows 7 aygıtları](active-directory-conditional-access-automatic-device-registration-setup.md) |

| Nasıl toouse hello iki aşamalı doğrulama için Microsoft Authenticator uygulaması | [Microsoft Authenticator](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

Koşullu erişim bir [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) özelliği.

## <a name="apps--azure-ad"></a>Uygulamalar ve Azure AD
### <a name="cloud-app-discovery-find-which-saas-apps-are-being-used-in-your-organization"></a>Cloud App Discovery: kuruluşunuzda hangi SaaS uygulamaları kullanılan Bul
Cloud App Discovery hangi SaaS uygulamaları hello kuruluşun genelinde kullanılan öğrenin BT departmanları yardımcı olur. Uygulama kullanımı ölçebilirsiniz ve BT denetim ve Azure AD ile tümleşik altında böylece onun hangi uygulamaların engeller en hello faydalanırsınız belirleyebilir popülerliği getirildi.

| Makale Kılavuzu |  |
|:---:| --- |
| Nasıl çalıştığına ilişkin genel bir bakış |[Cloud App Discovery ile bulut uygulamaları tasdik bulma](active-directory-cloudappdiscovery-whatis.md) |
| Derin Dalış nasıl içine, gizlilik üzerinde yanıtları tooquestions ile çalışır |[Güvenlik ve gizlilik konuları](active-directory-cloudappdiscovery-security-and-privacy-considerations.md) |
| Sık Sorulan Sorular |[Cloud App Discovery hakkında SSS](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx) |
| Cloud App Discovery dağıtmak için öğreticileri |[Grup İlkesi Dağıtım Kılavuzu](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)<br /><br />[System Center Dağıtım Kılavuzu](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)<br /><br />[Proxy sunucuları özel bağlantı noktaları ile yükleme](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md) |
| Merhaba güncelleştirmeleri toohello Cloud App Discovery aracısı için günlük değiştirme |[Değişiklik günlüğü](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx) |

Cloud App Discovery bir [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) özelliği.

### <a name="automatically-provision-and-deprovision-user-accounts-in-saas-apps"></a>Otomatik olarak sağlamak ve kullanıcı hesapları SaaS uygulamalarında yetkisini kaldırma
Merhaba oluşturulması, Bakım ve kullanıcı kimlikleri Dropbox, Salesforce, ServiceNow ve daha fazlası gibi SaaS uygulamalarında kaldırılmasını otomatikleştirin. Eşleşen ve Azure AD arasında varolan kimlik eşitleme ve SaaS uygulamalarınıza ve kullanıcıların hello kuruluştan ayrılan bırakılarak otomatik olarak hesaplar erişimi denetleme.

| Makale Kılavuzu |  |
|:---:| --- |
| Nasıl çalıştığı hakkında bilgi edinin ve toocommon soruları yanıtlar Bul |[Kullanıcı hazırlama ve sağlamayı kaldırma işlemlerini tooSaaS uygulamaları otomatikleştirme](active-directory-saas-app-provisioning.md) |
| Bilgileri Azure AD arasında nasıl eşlendi yapılandırmak ve SaaS uygulamanız |[Öznitelik eşlemelerini özelleştirme](active-directory-saas-customizing-attribute-mappings.md)<br><br>[Özellik eşlemeleri için ifade yazma](active-directory-saas-writing-expressions-for-attribute-mappings.md) |
| Nasıl hello SCIM'yi protokolünü destekleyen sağlama tooany uygulama tooenable otomatik |[Otomatik kullanıcı hazırlama tooany SCIM-Enabled uygulama ayarlama](active-directory-scim-provisioning.md) |
| Nasıl tooreport üzerinde ve kullanıcı hazırlama sorun giderme |[Otomatik kullanıcı sağlamayı raporlama](active-directory-saas-provisioning-reporting.md)<br><br>[Sağlama bildirimleri](active-directory-saas-account-provisioning-notifications.md)<br><br>[Kullanıcı sağlama sorunlarını giderme](active-directory-application-provisioning-content-map.md) |
| Öznitelik değerlerine göre sağlanan tooan uygulama alır sınırı |[Kapsam belirleme filtreleri](active-directory-saas-scoping-filters.md) |

Otomatik kullanıcı sağlamayı tooten uygulamalar kullanıcı başına yedeklemek için Azure AD'in tüm sürümlerinde kullanılabilir. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) sınırsız uygulamaları destekler. Kuruluşunuzun varsa [Azure AD temel](https://azure.microsoft.com/pricing/details/active-directory/) veya [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), yapabilecekleriniz sonra [hangi kullanıcıların sağlanan grupları toomanage kullanmak](#managing-access-to-applications).

### <a name="building-applications-that-integrate-with-azure-ad"></a>Azure AD ile tümleştirmek uygulamaları oluşturma
Kuruluşunuz geliştirme veya satır iş kolu (LoB) uygulamaları koruma ya da bir uygulama geliştiricisi Azure Active Directory kullanan müşteriler sahip değilseniz, öğreticiler aşağıdaki hello yardımcı olur, uygulamalarınızın Azure AD ile tümleştirin.

| Makale Kılavuzu |  |
|:---:| --- |
| BT uzmanları ve uygulamaları Azure AD ile tümleştirme uygulama geliştiricileri için yönergeler |[Azure AD için uygulama geliştirmek için Hello BT Uzmanı'nın Kılavuzu](active-directory-applications-guiding-developers-for-lob-applications.md)<br /><br />[Azure Active Directory için Hello Geliştirici Kılavuzu](active-directory-developers-guide.md) |
| Tooapplication satıcılar kendi uygulamaları toohello Azure AD uygulama galerisinde nasıl ekleyebilirsiniz |[Hello Azure Active Directory Uygulama galerisinde uygulamanızı listeleme](active-directory-app-gallery-listing.md) |
| Nasıl toomanage erişim Azure Active Directory'yi kullanarak toodeveloped uygulamaları |[Nasıl tooEnable geliştirilen uygulamaları için kullanıcı ataması](active-directory-applications-guiding-developers-requiring-user-assignment.md)<br /><br />[Kullanıcıların tooyour uygulama atama](active-directory-applications-guiding-developers-assigning-users.md)<br /><br />[Atama Grup tooyour uygulama](active-directory-applications-guiding-developers-assigning-groups.md) |

Tüketiciye yönelik uygulamalar geliştiriyorsanız, kullanarak ilgilenebilirsiniz [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) kendi kimlik sistemi toomanage toodevelop yok böylece kullanıcılarınızın. [Daha fazla bilgi edinin](../active-directory-b2c/active-directory-b2c-overview.md).

## <a name="managing-access-tooapplications"></a>Erişim tooApplications yönetme
### <a name="using-groups-and-self-service-toomanage-who-has-access-toowhich-apps"></a>Gruplar ve erişim toowhich uygulamaları sahip Self Servis toomanage kullanarak
toohelp toowhich erişimine sahip gereken yönettiğiniz, Azure Active Directory tooset atamaları ve izinleri gruplarını kullanarak ölçekte sağlar. BT, gereksinim duyan kullanıcılar yalnızca izni istemesini tooenable Self Servis özellikleri seçebilirsiniz.

| Makale Kılavuzu |  |
|:---:| --- |
| Azure AD erişim yönetim özelliklerine genel bakış |[Giriş tooManaging erişim tooApps](active-directory-managing-access-to-apps.md)<br /><br />[Azure AD'de erişim yönetimi nasıl çalışır?](active-directory-manage-groups.md)<br /><br />[Nasıl tooUse grupları tooManage erişim tooSaaS uygulamalar](active-directory-accessmanagement-group-saasapps.md) |
| Self Servis yönetimine, uygulamaların ve grupları izin ver |[Self Servis uygulama yönetimi](active-directory-self-service-application-access.md)<br /><br />[Self Servis Grup Yönetimi](active-directory-accessmanagement-self-service-group-management.md) |
| Azure AD'de, grupları ayarlama yönergeleri |[Nasıl tooCreate güvenlik grupları](active-directory-accessmanagement-manage-groups.md)<br /><br />[Nasıl tooDesignate bir grubun sahiplerini](active-directory-accessmanagement-managing-group-owners.md)<br /><br />[TooUse hello "tüm kullanıcılar" Grup nasıl](active-directory-accessmanagement-dedicated-groups.md) |
| Kullanım dinamik grupların tooautomatically öznitelik tabanlı üyelik kurallarını kullanarak grup üyeliğini doldurmak |[Dinamik grup üyeliğini: Gelişmiş kurallar](active-directory-accessmanagement-groups-with-advanced-rules.md)<br /><br />[Dinamik grup üyeliklerini sorunlarını giderme](active-directory-accessmanagement-troubleshooting.md) |

Grup tabanlı bir uygulamaya erişim yönetimi için kullanılabilir [Azure AD temel](https://azure.microsoft.com/pricing/details/active-directory/) ve [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/). Self Servis Grup Yönetimi, uygulama kendi kendine yönetimi ve dinamik grupların [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) özellikleri.

### <a name="b2b-collaboration-enable-partner-access-tooapplications"></a>B2B işbirliği: iş ortağı erişim tooapplications etkinleştir
İşinizin diğer şirketlerle işbirliği değilse, toomanage ortak erişim tooyour Kurumsal uygulamalara gereksinim olasıdır. Azure Active Directory B2B işbirliği uygulamalarınızı iş ortakları ile kolay ve güvenli şekilde tooshare sağlar.

| Makale Kılavuzu |  |
|:---:| --- |
| Farklı Azure AD genel bir bakış dış kullanıcılar gibi yönetmenize yardımcı ortakları olduğunu, müşteriler, vb. içerir. |[Dış kimlikler Azure AD'de yönetmek için özellikleri karşılaştırma](active-directory-b2b-compare-external-identities.md) |
| Bir giriş tooB2B işbirliği ve nasıl tooget başlatıldı |[Basit, güvenli, Azure AD ile bulut iş ortağı tümleştirme](active-directory-b2b-what-is-azure-ad-b2b.md)<br /><br />[Azure Active Directory B2B işbirliği](active-directory-b2b-collaboration-overview.md) |
| Azure AD B2B işbirliği halinde daha derin Dalış ve nasıl toouse, |[B2B işbirliği: Nasıl çalışır?](active-directory-b2b-how-it-works.md)<br /><br />[Azure AD B2B işbirliği geçerli sınırlamaları](active-directory-b2b-current-limitations.md)<br /><br />[Azure AD B2B işbirliği kullanımının ayrıntılı kılavuz](active-directory-b2b-detailed-walkthrough.md) |
| Azure AD B2B işbirliği nasıl çalıştığı hakkında teknik bilgi makalelerle başvurusu |[İş ortağı kullanıcılar eklemek için CSV dosya biçimi](active-directory-b2b-references-csv-file-format.md)<br /><br />[Azure AD B2B işbirliği tarafından etkilenen kullanıcı öznitelikleri](active-directory-b2b-references-external-user-object-attribute-changes.md)<br /><br />[İş ortağı kullanıcılar için kullanıcı belirteci biçimi](active-directory-b2b-references-external-user-token-format.md) |

B2B işbirliği için şu anda kullanılabilir [Azure Active Directory'nin tüm sürümlerinde](https://azure.microsoft.com/pricing/details/active-directory/).

### <a name="access-panel-a-portal-for-accessing-apps-and-self-service-features"></a>Erişim paneli: uygulamaları ve Self Servis özelliklerine erişmek için bir portal
Hello Azure AD erişim paneli, burada son kullanıcılar, uygulamaları ve toomanage izin erişim hello Self Servis özellikleri, uygulamaları ve grup üyeliklerini başlatabilirsiniz ' dir. Ayrıca toohello erişim paneli, SSO özellikli uygulamalar erişmek için diğer seçenekleri hello aşağıdaki listede eklenir.

| Makale Kılavuzu |  |
|:---:| --- |
| Merhaba farklı seçenekler tek oturum açma uygulamaları toousers dağıtmak için kullanılabilir karşılaştırması |[Azure AD tümleşik uygulamalarını tooUsers dağıtma](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) |
| Merhaba erişim paneli ve kendi mobil eşdeğer MyApps genel bakış |[Giriş tooAccess paneli ve MyApps](active-directory-saas-access-panel-introduction.md)<br />— [iOS](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8)<br />— [Android](https://play.google.com/store/apps/details?id=com.microsoft.myapps) |
| Azure AD tooaccess uygulamalardan Office 365 Web sitesi nasıl hello |[Merhaba Office 365 uygulama Başlatıcı kullanma](https://support.office.com/en-us/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a) |
| Intune Managed Browser mobil uygulama tooaccess Azure AD uygulamaları nasıl hello |[Intune yönetilen tarayıcı](https://technet.microsoft.com/en-us/library/dn878029.aspx)<br />— [iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8)<br />— [Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser) |
| Nasıl derin bağlantılar tooinitiate kullanarak tooaccess Azure AD uygulamaları çoklu oturum açmayı |[Oturum açma doğrudan bağlantılar tooYour uygulamaları alma](active-directory-appssoaccess-whatis.md#direct-sign-on-links-for-federated-password-based-or-existing-apps) |

Erişim paneli yüklenebilir [Azure Active Directory'nin tüm sürümlerinde](https://azure.microsoft.com/pricing/details/active-directory/).

### <a name="reports-easily-audit-app-access-changes-and-monitor-sign-ins-tooapps"></a>Raporları: Uygulama erişim değişikliklerini denetleme ve oturum açma işlemleri tooapps izlemek kolayca
Azure Active Directory çeşitli raporlar sağlar ve toohelp uyarılar, kuruluşunuzun erişim tooapplications izleyin. Anormal oturum açma işlemlerine tooyour uygulamalar için uyarılar alabilir ve ne zaman ve neden bir kullanıcıların erişim tooan uygulaması değişmiş izleyebilirsiniz.

| Makale Kılavuzu |  |
|:---:| --- |
| Raporlama özellikleri Azure Active Directory'de hello genel bakış |[Başlarken Azure AD raporlama](active-directory-reporting-getting-started.md) |
| Toomonitor nasıl hello oturum açmalarına ve kullanıcılarınızın uygulama kullanımı |[Erişim ve kullanım raporları görüntüleyin](active-directory-view-access-usage-reports.md) |
| Toowho yapılan değişiklikleri izleme belirli bir uygulamaya erişmek için |[Azure Active Directory Denetim Raporu olayları](active-directory-reporting-audit-events.md) |
| Raporlama API'sini kullanarak bu raporları tercih edilen tooyour araçların hello verileri dışa hello |[Hello Azure AD raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md) |

hangi raporların Azure Active Directory, farklı sürümlerine dahil toosee [burayı](active-directory-view-access-usage-reports.md).

## <a name="see-also"></a>Ayrıca bkz.
[Azure Active Directory nedir?](active-directory-whatis.md)

[Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/)

[Azure Active Directory etki alanı Hizmetleri](https://azure.microsoft.com/services/active-directory-ds/)

[Azure çok faktörlü kimlik doğrulaması](https://azure.microsoft.com/services/multi-factor-authentication/)
