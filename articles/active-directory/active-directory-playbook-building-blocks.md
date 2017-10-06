---
title: "Active Directory kavram playbook yapı taşlarını kanıtını aaaAzure | Microsoft Docs"
description: "Keşfetmek ve hızlı bir şekilde kimlik ve erişim yönetimi senaryoları uygulayan"
services: active-directory
keywords: "Azure active directory, playbook, kavram kanıtı, PT"
documentationcenter: 
author: dstefanMSFT
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: dstefan
ms.openlocfilehash: e54148330a123baf27d7e0f73469ff2a24c0efcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-building-blocks"></a>Azure Active Directory kavram playbook kanıtını: yapı taşları

## <a name="catalog-of-roles"></a>Rollerin Kataloğu

| Rol | Açıklama | Prototip (PT) sorumluluk kanıtı |
| --- | --- | --- |
| **Kimlik mimarisi / geliştirme ekibi** | Bu genellikle hello çözümü tasarlarken, prototipleri uygulayan, onayları sürücüler ve son olarak devre dışı toooperations aktarır hello bir Ekiptir | Merhaba ortamları sağlamak ve hello olanları değerlendirilirken hello farklı senaryolar hello yönetilebilirlik açısından |
| **Şirket içi kimlik işletim ekibi** | Merhaba farklı kimlik kaynakları şirket içi yönetir: Active Directory ormanları, LDAP dizinleri, ik sistemleri ve Federasyon kimlik sağlayıcıları. | Tooon içi kaynaklara erişmek için hello PoC senaryoları gerekli sağlar.<br/>Bunlar mümkün olduğunca az söz konusu|
| **Uygulama teknik sahipleri** | Teknik sahiplerini hello farklı bulut uygulamaları ve Azure AD ile tümleştirme hizmetleri | SaaS uygulamaları (test etmek için örnekler) büyük olasılıkla ayrıntılarını sağlayın |
| **Azure AD genel yönetici** | Hello Azure AD yapılandırmasını yönetir | Tooconfigure hello eşitleme hizmeti kimlik bilgilerini sağlayın. Genellikle aynı ekip kimlik mimari olarak PoC sırasında hello ancak hello işlemleri aşamasında ayrı|
| **Veritabanı ekibi** | Merhaba veritabanı altyapısı sahipleri | Erişim tooSQL ortamı (ADFS veya Azure AD Connect) için belirli bir senaryoyu hazırlıklar sağlar.<br/>Bunlar mümkün olduğunca az söz konusu |
| **Ağ ekibi** | Merhaba ağ altyapısı sahipleri | Merhaba eşitleme hello ağ düzeyinde gerekli erişim sunucuları tooproperly hello veri kaynaklarına erişim sağlamak ve bulut hizmetlerini (güvenlik duvarı kuralları, açılan bağlantı noktaları, IPSec kuralları vb.) |
| **Güvenlik ekibi** | Merhaba güvenlik stratejisini tanımlar, güvenlik raporları çeşitli kaynaklardan analiz eder ve bulguları üzerinde aşağıdaki. | Değerlendirme senaryoları hedef güvenlik sağlar |

## <a name="common-prerequisites-for-all-building-blocks"></a>Tüm yapı taşlarını ortak önkoşulları

Azure AD Premium herhangi POC için gereken bazı ön koşullar aşağıda verilmiştir.

| Önkoşul | Kaynaklar |
| --- | --- |
| Geçerli bir Azure aboneliği ile tanımlanan azure AD kiracısı | [Nasıl tooget bir Azure Active Directory Kiracı](active-directory-howto-tenant.md)<br/>**Not:** zaten Azure AD Premium lisansına sahip bir ortamınız varsa, toohttps://aka.ms/accessaad giderek sıfır cap aboneliği alabilirsiniz <br/>Hakkında daha fazla bilgi edinin: https://blogs.technet.microsoft.com/enterprisemobility/2016/02/26/azure-ad-mailbag-azure-subscriptions-and-azure-ad-2/ ve https://technet.microsoft.com/library/dn832618.aspx |
| Tanımlanan ve doğrulanan etki alanları | [Özel etki alanı adı tooAzure Active Directory ekleme](active-directory-domains-add-azure-portal.md)<br/>**Not:** Power BI bir azure AD Kiracı hello altında sağlanan gibi bazı iş yükleri kapsar. toocheck belirli bir etki alanı ilişkili tooa Kiracı ise toohttps://login.microsoftonline.com/ {domain}/v2.0/.well-known/openid-configuration gidin. Merhaba etki alanı zaten tooa Kiracı atanmış sonra başarılı bir yanıt almak ve devralır gerekli. Bu durumda, Ek Yardım için Microsoft ile iletişime geçin. Merhaba devralma seçenekleri hakkında daha fazla bilgi edinin: [Azure için Self Servis kaydolma nedir?](active-directory-self-service-signup.md) |
| Azure AD Premium veya EMS deneme etkin | [Azure Active Directory Premium bir ay süreyle ücretsiz](https://azure.microsoft.com/trial/get-started-active-directory/) |
| TooPoC kullanıcıları Azure AD Premium veya EMS lisansları atayıp | [Kendinizin ve kullanıcılarınızın Azure Active Directory'de lisans](active-directory-licensing-get-started-azure-portal.md) |
| Azure AD genel yönetici kimlik bilgileri | [Azure Active Directory'de yönetici rolleri atama](active-directory-assign-admin-roles-azure-portal.md) |
| İsteğe bağlıdır ancak önerilir: bir geri dönüş olarak paralel laboratuvar ortamı | [Azure AD Connect Önkoşulları](./connect/active-directory-aadconnect-prerequisites.md) |

## <a name="directory-synchronization---password-hash-sync-phs---new-installation"></a>Dizin eşitleme - parola karması eşitlemesi (PHS) - yeni yükleme

Yaklaşık bir saat tooComplete: 1. 000'den az PoC kullanıcılar için bir saat

### <a name="pre-requisites"></a>Ön koşullar

| Önkoşul | Kaynaklar |
| --- | --- |
| Sunucu tooRun Azure AD Connect | [Azure AD Connect Önkoşulları](./connect/active-directory-aadconnect-prerequisites.md) |
| Hedef hello POC kullanıcılar aynı etki alanı ve bir güvenlik grubu ve OU parçası | [Azure AD Connect özel yüklemesi](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) |
| Azure AD Connect POC tanımlanır hello için gerekli özellikleri | [Azure Active Directory ile Active Directory connect - eşitleme yapılandırma özellikleri](./connect/active-directory-aadconnect.md#configure-sync-features) |
| Şirket içi kimlik bilgileri gerekli ve bulut ortamları  | [Azure AD Connect: Hesaplar ve izinler](./connect/active-directory-aadconnect-accounts-permissions.md) |

### <a name="steps"></a>Adımlar

| Adım | Kaynaklar |
| --- | --- |
| Hello Azure AD Connect'in en son sürümünü indirme | [Microsoft Azure Active Directory Connect indirin](https://www.microsoft.com/download/details.aspx?id=47594) |
| Azure AD Connect yükleme hello en basit yolu ile: Express <br/>1. Filtre toohello hedef OU toominimize hello eşitleme Döngüsü süresi<br/>2. Kullanıcılar hedef kümesi hello şirket içi grubunda seçin.<br/>3. Diğer POC Temalar göre hello gerekli hello özellikleri dağıtma | [Azure AD Connect: Özel yükleme: etki alanı ve OU filtreleme](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) <br/>[Azure AD Connect: Özel yükleme: Grup tabanlı filtreleme](./connect/active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups)<br/>[Azure AD Connect: şirket içi kimliklerinizi Azure Active Directory ile tümleştirme: eşitleme özellikleri yapılandırma](./connect/active-directory-aadconnect.md#configure-sync-features) |
| Hello Azure AD Connect kullanıcı arabirimini açın ve tamamlanmış (içeri aktarma, eşitleme ve dışa aktarma) çalıştıran hello profilleri bakın | [Azure AD Connect eşitleme: Scheduler](./connect/active-directory-aadconnectsync-feature-scheduler.md) |
| Açık hello [Azure AD yönetim portalında](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/), toohello "Tüm kullanıcılar" dikey penceresine gidin, "Kaynak yetki başlangıcı" sütun ve hello kullanıcılara görünür, bkz: "Windows Server'dan AD" geliyormuş gibi doğru işaretlenmiş ekleme | [Azure AD Yönetim Portalı](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) |

### <a name="considerations"></a>Dikkat edilmesi gerekenler

1. Ara hello güvenlik hususlarını parola karması eşitlemesi sırasında [burada](./connect/active-directory-aadconnectsync-implement-password-synchronization.md).  Parola karma eşitlemesi pilot üretim kullanıcılar için bir seçenek değil tam olarak, aşağıdaki alternatifleri hello göz önünde bulundurun:
   * Test kullanıcılarını hello üretim etki alanında oluşturun. Başka bir hesap eşitleme emin olun
   * Taşıma tooan UAT ortamı
2.  Toopursue Federasyon istiyorsanız faydalı toounderstand hello maliyetleri hello POC ötesinde şirket içi kimlik sağlayıcısı ile bir Federasyon çözüm ilişkili olan ve hello karşı sizin yararınıza ölçü görmek:
    * Yüksek kullanılabilirlik için toodesign alacak şekilde hello kritik yolunda bulunuyor.
    * Bir şirket içi hizmet toocapacity planı ihtiyacınız olan
    * Bu toomonitor/korumak/düzeltme eki gereken bir şirket içi hizmet olduğundan

Daha fazla bilgi edinin: [anlama Office 365 kimlik ve Azure Active Directory - Federal Kimlik](https://support.office.com/article/Understanding-Office-365-identity-and-Azure-Active-Directory-06a189e7-5ec6-4af2-94bf-a22ea225a7a9#bk_federated)

## <a name="branding"></a>Markalama

Yaklaşık bir saat tooComplete: 15 dakika

### <a name="pre-requisites"></a>Ön koşullar

| Önkoşul | Kaynaklar |
| --- | --- |
| Varlıklar (görüntüleri, logolar, vb.); En iyi görselliğini emin hello varlıklar boyutları önerilen hello sahip olun. | [Şirket tooyour oturum açma sayfasında hello Azure Active Directory markası ekleme](active-directory-branding-custom-signon-azure-portal.md) |
| İsteğe bağlı: hello ortam bir ADFS sunucusu varsa, erişim toohello sunucu toocustomize web teması | [AD FS kullanıcı oturum açma özelleştirme](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/ad-fs-user-sign-in-customization) |
| İstemci bilgisayar tooperform son kullanıcı oturum açma deneyimi |  |
| İsteğe bağlı: Mobil cihazları toovalidate deneyimi |  |

### <a name="steps"></a>Adımlar

| Adım | Kaynaklar |
| --- | --- |
| TooAzure AD Git Yönetim Portalı | [Azure AD yönetim portalında - şirket markası](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/LoginTenantBranding) |
| Merhaba varlıkları hello oturum açma sayfasına (kahramanı logosu, küçük logo, etiketler, vb.) için karşıya yükleyin. AD FS varsa, isteğe bağlı olarak Hizala hello ADFS oturum açma sayfaları ile aynı varlıklar | [Tooyour oturum açma ve erişim paneli sayfasında şirket markası ekleme: özelleştirilebilir öğeler](active-directory-add-company-branding.md) |
| Birkaç dakika hello değişiklik toofully etkili için bekleyin |  |
| POC kullanıcı kimlik bilgisi toohttps://myapps.microsoft.com Hello ile oturum açın |  |
| Merhaba görünüm tarayıcıda onaylayın | [Tooyour oturum açma ve erişim paneli sayfasında şirket markası ekleme](active-directory-add-company-branding.md) |
| İsteğe bağlı olarak, hello görünüm diğer aygıtları onaylayın |  |

### <a name="considerations"></a>Dikkat edilmesi gerekenler

Merhaba eski görünüm hello özelleştirme sonrasında kalırsa hello tarayıcı istemci önbelleğini temizlemek ve hello işlemi yeniden deneyin.

## <a name="group-based-licensing"></a>Lisans grup tabanlı

Yaklaşık bir saat tooComplete: 10 dakika

### <a name="pre-requisites"></a>Ön koşullar

| Önkoşul | Kaynaklar |
| --- | --- |
| Tüm POC kullanıcılar bir güvenlik grubu (Bulut veya şirket içi) bir parçasıdır | [Bir grup oluşturun ve Azure Active Directory'de üye ekleme](active-directory-groups-create-azure-portal.md) |

### <a name="steps"></a>Adımlar

| Adım | Kaynaklar |
| --- | --- |
| Azure AD yönetim portalında toolicenses dikey penceresine gidin | [Azure AD yönetim portalında: lisanslama](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) |
| Merhaba lisansları toohello güvenlik grubunu POC kullanıcılarla atayın. | [Azure Active Directory'de kullanıcı lisansları tooa grubu atayın](active-directory-licensing-group-assignment-azure-portal.md) |

### <a name="considerations"></a>Dikkat edilmesi gerekenler

Sorunları durumunda çok Git[senaryoları, sınırlamaları ve grupları toomanage Azure Active Directory'de Lisansı'nı kullanma bilinen sorunlar](active-directory-licensing-group-advanced.md)

## <a name="saas-federated-sso-configuration"></a>SaaS Federasyon SSO yapılandırma

Yaklaşık bir saat tooComplete: 60 dakika

### <a name="pre-requisites"></a>Ön koşullar

| Önkoşul | Kaynaklar |
| --- | --- |
| Merhaba SaaS uygulaması kullanılabilir ortamının sınayın. Bu kılavuzda, örnek olarak ServiceNow kullanırız.<br/>Mevcut veri kalitesini ve eşlemeleri gezinme üzerinde bir test örneği toominimize uyuşmazlık toouse kesinlikle öneririz. | Toohttps://Developer.servicenow.com/App.do# Git! / ev toostart hello sürecini, bir test örneği alma |
| Yönetici erişim toohello ServiceNow Yönetim Konsolu | [Öğretici: ServiceNow Azure Active Directory Tümleştirme](active-directory-saas-servicenow-tutorial.md) |
| Hedef Kullanıcılar tooassign hello uygulamaya kümesi. Merhaba PoC kullanıcıları içeren bir güvenlik grubu önerilir. <br/>Oluşturma hello Grup uygun değilse, hello kullanıcılar hello PoC için toodirectly toohello uygulama atama | [Azure Active Directory'de bir kullanıcı veya grup tooan kuruluş uygulama atama](active-directory-coreapps-assign-user-azure-portal.md) |

### <a name="steps"></a>Adımlar

| Adım | Kaynaklar |
| --- | --- |
| Başlangıç Öğreticisi tooall aktörler Microsoft Documentation gelen paylaşma  | [Öğretici: ServiceNow Azure Active Directory Tümleştirme](active-directory-saas-servicenow-tutorial.md) |
| Çalışma Toplantı ayarlayın ve her aktör ile Merhaba öğretici adımları izleyin. | [Öğretici: ServiceNow Azure Active Directory Tümleştirme](active-directory-saas-servicenow-tutorial.md) |
| Merhaba Önkoşullar belirlenen hello uygulama toohello grubu atayın. Hello POC hello kapsamda koşullu erişimi varsa, daha sonra yeniden ziyaret ve MFA ekleyin ve benzer. <br/>Bu işlem (yapılandırılmışsa) sağlama hello kazandırın unutmayın |  [Azure Active Directory'de bir kullanıcı veya grup tooan kuruluş uygulama atama](active-directory-coreapps-assign-user-azure-portal.md) <br/>[Bir grup oluşturun ve Azure Active Directory'de üye ekleme](active-directory-groups-create-azure-portal.md) |
| Azure AD yönetim portalında tooadd ServiceNow uygulama Galerisi'nden kullanın| [Azure AD Yönetim Portalı: Kurumsal uygulamalar](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/Overview) <br/>[Azure Active Directory'de Kurumsal Uygulama Yönetimi'nde yenilikler](active-directory-enterprise-apps-whats-new-azure-portal.md) |
| "ServiceNow uygulamasının dikey"çoklu oturum açmayı"SAML tabanlı oturum açmayı" etkinleştirin |  |
| ServiceNow URL'niz ile "Oturum üzerinde URL'si" ve "Tanımlayıcı" alanları doldurun<br/>Merhaba kutuyu çok "Make yeni sertifika active"<br/>ve ayarları kaydedin |  |
| Aç "ServiceNow yapılandırma" dikey penceresinde hello paneli tooview hello alt tooconfigure ServiceNow yönergeler için özelleştirilmiş |  |
| Yönergeler tooconfigure ServiceNow izleyin |  |
| ServiceNow uygulama "Hazırlama" dikey penceresinde "Otomatik" sağlamayı etkinleştir | [Kullanıcı hesabı hello yeni Azure portalında Kurumsal uygulamaları için sağlama yönetme](active-directory-enterprise-apps-manage-provisioning.md) |
| Sağlama işlemini tamamlarken birkaç dakika bekleyin.  Hello sırada, raporları sağlama hello üzerinde kontrol edebilirsiniz |  |
| İçinde toohttps://myapps.microsoft.com/ erişimi olan bir test kullanıcı olarak oturum açın | [Merhaba erişim paneli nedir?](active-directory-saas-access-panel-introduction.md) |
| Yeni oluşturduğunuz Merhaba uygulaması hello kutucuğuna tıklayın. Erişimi onaylayın |  |
| İsteğe bağlı olarak, hello uygulama kullanım raporlarını kontrol edebilirsiniz. Bazı zaman toosee hello trafiği hello raporlarında toowait gereken şekilde bazı gecikme olduğuna dikkat edin. | [Hello Azure Active Directory portalında oturum açma etkinliği raporları: yönetilen uygulamaların kullanımı](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Azure Active Directory rapor bekletme ilkeleri](active-directory-reporting-retention.md) |

### <a name="considerations"></a>Dikkat edilmesi gerekenler

1. Yukarıdaki [öğretici](active-directory-saas-servicenow-tutorial.md) tooold Azure AD yönetim deneyimi başvuruyor. Ancak PoC temel [Hızlı Başlangıç](active-directory-enterprise-apps-whats-new-azure-portal.md#quick-start-get-going-with-your-new-application-right-away) karşılaşırsınız.
2. Merhaba hedef uygulama hello Galerisi'nde mevcut değilse, "kendi uygulamanızı getir" kullanabilirsiniz. Daha fazla bilgi edinin: [Kurumsal Uygulama Yönetimi Azure Active Directory'deki yenilikler: tek bir yerden özel uygulamalar ekleme](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

## <a name="saas-password-sso-configuration"></a>SaaS parola SSO yapılandırma

Yaklaşık bir saat tooComplete: 15 dakika

### <a name="pre-requisites"></a>Ön koşullar

| Önkoşul | Kaynaklar |
| --- | --- |
| Test ortamı SaaS uygulamaları için. Parola SSO HipChat ve Twitter örneğidir. Başka herhangi bir uygulama için başlangıç sayfasının html oturum açma formu ile hello tam URL gerekir. | [Microsoft Azure Marketi twitter](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[Microsoft Azure Market'te HipChat](https://azuremarketplace.microsoft.com/marketplace/apps/aad.hipchat) |
| Merhaba uygulamaları için hesapları sınayın. | [Twitter için kaydolun](https://twitter.com/signup?lang=en)<br/>[Ücretsiz kaydolun: HipChat](https://www.hipchat.com/sign_up) |
| Hedef Kullanıcılar tooassign hello uygulamaya kümesi. Bir güvenlik grubunun hello kullanıcıları önerilir. | [Azure Active Directory'de bir kullanıcı veya grup tooan kuruluş uygulama atama](active-directory-coreapps-assign-user-azure-portal.md) |
| Yerel yönetici erişimi tooa bilgisayar toodeploy hello Internet Explorer, Chrome veya Firefox için erişim paneli uzantısı | [IE için erişim paneli uzantısı](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Chrome için erişim paneli uzantısı](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Firefox için erişim paneli uzantısı](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>Adımlar

| Adım | Kaynaklar |
| --- | --- |
| Merhaba tarayıcı uzantısı yükleyin | [IE için erişim paneli uzantısı](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Chrome için erişim paneli uzantısı](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Firefox için erişim paneli uzantısı](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| Galeriden uygulamayı yapılandırma | [Azure Active Directory'de Kurumsal Uygulama Yönetimi'nde yenilikler: hello yeni ve geliştirilmiş uygulama Galerisi](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| Parola SSO yapılandırın | [Merhaba yeni Azure portalında Kurumsal uygulamaları için çoklu oturum açmayı yönetme: parola tabanlı oturum açma](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Merhaba Önkoşullar belirlenen hello uygulama toohello grubu atayın | [Azure Active Directory'de bir kullanıcı veya grup tooan kuruluş uygulama atama](active-directory-coreapps-assign-user-azure-portal.md) |
| İçinde toohttps://myapps.microsoft.com/ erişimi olan bir test kullanıcı olarak oturum açın |  |
| Yeni oluşturduğunuz Merhaba uygulaması hello kutucuğuna tıklayın. | [Merhaba erişim paneli nedir?: parola tabanlı SSO kimlik sağlama olmadan](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| Merhaba uygulama kimlik bilgileri sağlayın | [Merhaba erişim paneli nedir?: parola tabanlı SSO kimlik sağlama olmadan](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| Merhaba tarayıcı ve yineleme hello oturumu kapatın. Bu sefer orada hello kullanıcı sorunsuz erişim toohello uygulama görmeniz gerekir. |  |
| İsteğe bağlı olarak, hello uygulama kullanım raporlarını kontrol edebilirsiniz. Bazı zaman toosee hello trafiği hello raporlarında toowait gereken şekilde bazı gecikme olduğuna dikkat edin. | [Hello Azure Active Directory portalında oturum açma etkinliği raporları: yönetilen uygulamaların kullanımı](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Azure Active Directory rapor bekletme ilkeleri](active-directory-reporting-retention.md) |

### <a name="considerations"></a>Dikkat edilmesi gerekenler

Merhaba hedef uygulama hello Galerisi'nde mevcut değilse, "kendi uygulamanızı getir" kullanabilirsiniz. Daha fazla bilgi edinin: [Kurumsal Uygulama Yönetimi Azure Active Directory'deki yenilikler: tek bir yerden özel uygulamalar ekleme](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 Aşağıdaki gereksinimleri göz hello tutun:
   * Uygulama bilinen oturum açma URL'si olması gerekir
   * Merhaba oturum açma sayfasında bir HTML formuna hello tarayıcı uzantıları otomatik olarak doldurmak bir daha fazla metin alanları ile içermelidir. Minimum Hello, kullanıcı adı ve parola içermelidir.

## <a name="saas-shared-accounts-configuration"></a>SaaS paylaşılan hesaplarını yapılandırma

Yaklaşık bir saat tooComplete: 30 dakika

### <a name="pre-requisites"></a>Ön koşullar

| Önkoşul | Kaynaklar |
| --- | --- |
| Hedef uygulamaların listesini hello ve oturum açma tam URL'leri önceden hello. Örnek olarak, Twitter kullanabilirsiniz. | [Microsoft Azure Marketi twitter](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[Twitter için kaydolun](https://twitter.com/signup?lang=en) |
| Bu SaaS uygulaması için kimlik bilgisi paylaşılan. | [Azure AD kullanarak hesapları paylaşma](active-directory-sharing-accounts.md)<br/>[Azure AD parola toplama devretme Facebook, Twitter ve LinkedIn önizlemeye otomatik! -Enterprise Mobility and Security Blog] (https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/) |
| Kimlik bilgileri erişecek en az iki takım üyeleri için aynı hesabı hello. Güvenlik grubunun bir parçası olmalıdır. | [Azure Active Directory'de bir kullanıcı veya grup tooan kuruluş uygulama atama](active-directory-coreapps-assign-user-azure-portal.md) |
| Yerel yönetici erişimi tooa bilgisayar toodeploy hello Internet Explorer, Chrome veya Firefox için erişim paneli uzantısı | [IE için erişim paneli uzantısı](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Chrome için erişim paneli uzantısı](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Firefox için erişim paneli uzantısı](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>Adımlar

| Adım | Kaynaklar |
| --- | --- |
| Merhaba tarayıcı uzantısı yükleyin | [IE için erişim paneli uzantısı](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Chrome için erişim paneli uzantısı](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Firefox için erişim paneli uzantısı](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| Galeriden uygulamayı yapılandırma | [Azure Active Directory'de Kurumsal Uygulama Yönetimi'nde yenilikler: hello yeni ve geliştirilmiş uygulama Galerisi](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| Parola SSO yapılandırın | [Merhaba yeni Azure portalında Kurumsal uygulamaları için çoklu oturum açmayı yönetme: parola tabanlı oturum açma](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Kimlik bilgileri atarken Hello Önkoşullar belirlenen hello uygulama toohello grubu atayın | [Azure Active Directory'de bir kullanıcı veya grup tooan kuruluş uygulama atama](active-directory-coreapps-assign-user-azure-portal.md) |
| Bu erişim uygulama hello olarak farklı kullanıcı olarak oturum **aynı hesabı paylaşılan.**  |  |
| İsteğe bağlı olarak, hello uygulama kullanım raporlarını kontrol edebilirsiniz. Bazı zaman toosee hello trafiği hello raporlarında toowait gereken şekilde bazı gecikme olduğuna dikkat edin. | [Hello Azure Active Directory portalında oturum açma etkinliği raporları: yönetilen uygulamaların kullanımı](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Azure Active Directory rapor bekletme ilkeleri](active-directory-reporting-retention.md) |


### <a name="considerations"></a>Dikkat edilmesi gerekenler

Merhaba hedef uygulama hello Galerisi'nde mevcut değilse, "kendi uygulamanızı getir" kullanabilirsiniz. Daha fazla bilgi edinin: [Kurumsal Uygulama Yönetimi Azure Active Directory'deki yenilikler: tek bir yerden özel uygulamalar ekleme](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 Aşağıdaki gereksinimleri göz hello tutun:
   * Uygulama bilinen oturum açma URL'si olması gerekir
   * Merhaba oturum açma sayfasında bir HTML formuna hello tarayıcı uzantıları otomatik olarak doldurmak bir daha fazla metin alanları ile içermelidir. Minimum Hello, kullanıcı adı ve parola içermelidir.

## <a name="app-proxy-configuration"></a>Uygulama Proxy Yapılandırması

Yaklaşık bir saat tooComplete: 20 dakika

### <a name="pre-requisites"></a>Ön koşullar

| Önkoşul | Kaynaklar |
| --- | --- |
| Bir Microsoft Azure AD basic veya premium aboneliği ve bir genel yönetici olan bir Azure AD dizini | [Azure Active Directory sürümleri](active-directory-editions.md) |
| Bir web uygulaması şirket içi tooconfigure uzaktan erişim için istediğiniz barındırılan |  |
| Merhaba uygulama Proxy Bağlayıcısı yükleyebilmek için Windows Server 2012 R2 veya Windows 8.1 veya sonraki bir sürümü çalıştıran bir sunucu | [Azure AD uygulama proxy'si bağlayıcılar anlama](application-proxy-understand-connectors.md) |
| Merhaba yolunda bir güvenlik duvarı varsa, bağlayıcı HTTPS (TCP) yapabilirsiniz, hello toohello uygulama proxy'si bilmediğinden, açık olduğundan emin olun | [Hello Azure portalında uygulama ara sunucusunu etkinleştirme: uygulama ara sunucusu önkoşulları](active-directory-application-proxy-enable.md#application-proxy-prerequisites) |
| Kuruluşunuz proxy kullanıyorsa sunucuları tooconnect toohello Internet, hello blog bakmak için mevcut şirket içi proxy sunucuları ile çalışma sonrası Al ayrıntıları hakkında tooconfigure bunları | [Mevcut şirket içi proxy sunucuları ile çalışma](application-proxy-working-with-proxy-servers.md) |


### <a name="steps"></a>Adımlar

| Adım | Kaynaklar |
| --- | --- |
| Bir bağlayıcı hello sunucusuna yükleyin | [Hello Azure portalında uygulama ara sunucusunu etkinleştirme: yükleme ve bağlayıcı hello kaydetme](active-directory-application-proxy-enable.md#install-and-register-a-connector) |
| Azure ad uygulama proxy'si uygulama olarak Hello şirket içi uygulama yayımlama | [Azure AD uygulama proxy'si ile uygulama yayımlama](application-proxy-publish-azure-portal.md) |
| Test kullanıcıları atayın | [Azure AD uygulama proxy'si ile uygulama yayımlama: bir test kullanıcısı Ekle](application-proxy-publish-azure-portal.md#add-a-test-user) |
| İsteğe bağlı olarak, çoklu oturum açma deneyimini kullanıcılarınız için yapılandırın | [Çoklu oturum açma ile Azure AD uygulama proxy'si sağlayın](application-proxy-sso-azure-portal.md) |
| Kullanıcı tooMyApps portalında oturum açarak uygulamayı sınayın atanmış. | https://myapps.microsoft.com |

### <a name="considerations"></a>Dikkat edilmesi gerekenler

1. Şirket ağınızda hello bağlayıcı koyma öneririz, ancak alırken durumlarda hello buluta yerleştirmek daha iyi performans görürsünüz. Daha fazla bilgi edinin: [Azure Active Directory Uygulama proxy'si kullanırken ağ topolojisi hakkında önemli noktalar](application-proxy-network-topology-considerations.md)
2. Daha fazla güvenlik ayrıntıları ve nasıl bu özellikle güvenli uzaktan erişim sağlar için yalnızca giden bağlantılar koruma tarafından çözüm bakın: [Azure AD uygulama proxy'si kullanarak uygulamalar uzaktan erişim için güvenlik konuları](application-proxy-security-considerations.md)

## <a name="generic-ldap-connector-configuration"></a>Genel LDAP Bağlayıcısı yapılandırması

Yaklaşık bir saat tooComplete: 60 dakika

> [!IMPORTANT]
> Bu, FIM/MIM aşina gerektiren gelişmiş bir yapılandırmadır. Üretimde Biz bu yapılandırma hakkında sorular öneri kullandıysanız geçtikleri [Premier Destek](https://support.microsoft.com/premier).

### <a name="pre-requisites"></a>Ön koşullar

| Önkoşul | Kaynaklar |
| --- | --- |
| Azure AD Connect yüklenir ve yapılandırılır. | Yapı Taşı: [dizin eşitleme - parola karması eşitlemesi](#directory-synchronization--password-hash-sync-phs--new-installation) |
| ADLDS örneği toplantı gereksinimleri | [Genel LDAP Bağlayıcısı teknik başvuru: hello genel LDAP Bağlayıcısı genel bakış](./connect/active-directory-aadconnectsync-connector-genericldap.md#overview-of-the-generic-ldap-connector) |
| Kullanıcıların kullanmadığınız iş yükleri ve bu iş yükleri ile ilişkili öznitelikleri listesi | [Azure AD Connect eşitleme: öznitelikleri eşitlenir tooAzure Active Directory](./connect/active-directory-aadconnectsync-attributes-synchronized.md) |


### <a name="steps"></a>Adımlar

| Adım | Kaynaklar |
| --- | --- |
| Genel LDAP Bağlayıcısı Ekle | [Genel LDAP Bağlayıcısı teknik başvuru: yeni bir bağlayıcı oluşturun](./connect/active-directory-aadconnectsync-connector-genericldap.md#create-a-new-connector) |
| (Tam içeri aktarma, delta içeri aktarma, tam eşitleme, delta eşitleme, dışa aktarma) oluşturulan Bağlayıcısı için çalıştırma profillerini oluşturma | [Bir yönetim aracı çalıştırma profili oluştur](https://technet.microsoft.com/library/jj590219(v=ws.10).aspx)<br/> [Bağlayıcıları hello Azure AD Connect Eşitleme Hizmeti Yöneticisi ile kullanma](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md)|
| Tam içeri aktarma profili çalıştırın ve bağlayıcı alanı nesne olduğunu doğrulayın | [Bağlayıcı alanı nesne arayın](https://technet.microsoft.com/library/jj590287(v=ws.10).aspx)<br/>[Azure AD Connect Eşitleme Hizmeti Yöneticisi hello ile bağlayıcıları kullanma: arama bağlayıcı alanı](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md#search-connector-space) |
| Böylece meta veri deposu nesneleri iş yükleri için gerekli öznitelikler eşitleme kuralları oluşturma | [Azure AD Connect eşitleme: en iyi uygulamalar hello varsayılan yapılandırmasını değiştirmek için: değişiklikleri tooSynchronization kuralları](./connect/active-directory-aadconnectsync-best-practices-changing-default-configuration.md#changes-to-synchronization-rules)<br/>[Azure AD Connect eşitleme: bildirim temelli hazırlama anlama](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning.md)<br/>[Azure AD Connect eşitleme: bildirim temelli hazırlama ifadeleri anlama](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |
| Tam eşitleme döngüsü Başlat | [Azure AD Connect eşitleme: Zamanlayıcı: hello Zamanlayıcısı'nı Başlat](./connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler) |
| Sorun giderme hataları durumunda yapın | [TooAzure AD eşitlemiyor nesneyi sorun giderme](./connect/active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) |
| LDAP kullanıcı oturum açma ve hello uygulamaya erişim olduğunu doğrulayın | https://myapps.microsoft.com |

### <a name="considerations"></a>Dikkat edilmesi gerekenler

> [!IMPORTANT]
> Bu, FIM/MIM aşina gerektiren gelişmiş bir yapılandırmadır. Üretimde Biz bu yapılandırma hakkında sorular öneri kullandıysanız geçtikleri [Premier Destek](https://support.microsoft.com/premier).

## <a name="groups---delegated-ownership"></a>Grupları - temsilci sahipliği

Yaklaşık bir saat tooComplete: 10 dakika

### <a name="pre-requisites"></a>Ön koşullar

| Önkoşul | Kaynaklar |
| --- | --- |
| SaaS uygulaması (Federasyon SSO veya parola SSO) zaten yapılandırıldı | Yapı Taşı: [SaaS Federasyon SSO yapılandırma](#saas-federated-sso-configuration) |
| #1'deki erişim toohello uygulama atanmış bir bulut Grup tanımlanır | Yapı Taşı: [SaaS Federasyon SSO yapılandırma](#saas-federated-sso-configuration) <br/>[Bir grup oluşturun ve Azure Active Directory'de üye ekleme](active-directory-groups-create-azure-portal.md) |
| Kimlik bilgileri hello Grup sahibi için kullanılabilir | [Azure Active Directory grupları ile erişim tooresources yönetme](active-directory-manage-groups.md) |
| Merhaba bilgi çalışanı erişilirken hello uygulamalar için kimlik bilgilerini tanımlanan | [Merhaba erişim paneli nedir?](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>Adımlar

| Adım | Kaynaklar |
| --- | --- |
| Erişim toohello uygulama verilen hello grubunu tanımlayın ve hello sahibi verilen yapılandırma grubu| [Azure Active Directory'deki bir gruba Hello ayarlarını yönetin](active-directory-groups-settings-azure-portal.md) |
| Erişim paneli grupları sekmesinde hello grup üyeliği bkz Hello Grup sahibi olarak oturum açın | [Azure Active Directory grupları Management sayfası](https://account.activedirectory.windowsazure.com/r/#/groups) |
| Tootest istediğiniz hello bilgi çalışanı Ekle |  |
| Merhaba bilgi çalışanı olarak oturum açın, hello döşeme kullanılabilir onaylayın | [Merhaba erişim paneli nedir?](active-directory-saas-access-panel-introduction.md) |

### <a name="considerations"></a>Dikkat edilmesi gerekenler

Merhaba uygulaması etkin sağlama varsa, hello uygulama hello bilgi çalışanı olarak erişmeden önce toocomplete sağlama hello için birkaç dakika toowait gerekebilir.

## <a name="saas-and-identity-lifecycle"></a>SaaS ve kimlik yaşam döngüsü

### <a name="pre-requisites"></a>Ön koşullar

| Önkoşul | Kaynaklar |
| --- | --- |
| SaaS uygulaması (Federasyon SSO veya parola SSO) zaten yapılandırıldı | Yapı Taşı: [SaaS Federasyon SSO yapılandırma](#saas-federated-sso-configuration) |
| #1'deki erişim toohello uygulama atanmış bir bulut Grup tanımlanır | Yapı Taşı: [SaaS Federasyon SSO yapılandırma](#saas-federated-sso-configuration) <br/>[Bir grup oluşturun ve Azure Active Directory'de üye ekleme](active-directory-groups-create-azure-portal.md) |
| Merhaba bilgi çalışanı erişilirken hello uygulamalar için kimlik bilgilerini tanımlanan | [Merhaba erişim paneli nedir?](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>Adımlar

| Adım | Kaynaklar |
| --- | --- |
| Kaldırma hello kullanıcının hello Grup hello uygulama çok atanan| [Azure Active Directory kiracınızdaki kullanıcıların Grup üyeliğini yönetme](active-directory-groups-members-azure-portal.md) |
| Sağlamayı kaldırma özelliklerini için birkaç dakika bekleyin | [SaaS, kullanıcı uygulama sağlama Azure AD'de otomatik: otomatik sağlama işi ne yapar?](active-directory-saas-app-provisioning.md#how-does-automated-provisioning-work) |
| Ayrı bir tarayıcı oturumunda hello bilgi çalışanı toomy uygulamaları portal oturum açın ve bu kutucuğu eksik onaylayın | http://myapps.microsoft.com |


### <a name="considerations"></a>Dikkat edilmesi gerekenler

Merhaba PoC senaryo tooleavers ve/veya Mazeret senaryoları tahmin. Merhaba kullanıcı devre dışı, şirket içi AD veya kaldırıldı, artık bir şekilde toolog toohello SaaS uygulaması.

## <a name="self-service-access-tooapplication-management"></a>Self Servis erişim tooApplication Yönetimi

Yaklaşık bir saat tooComplete: 10 dakika

### <a name="pre-requisites"></a>Ön koşullar

| Önkoşul | Kaynaklar |
| --- | --- |
| Erişim toohello uygulamaları hello güvenlik grubunun bir parçası olarak isteyeceğini POC kullanıcıları tanımlayın | Yapı Taşı: [SaaS Federasyon SSO yapılandırma](#saas-federated-sso-configuration) |
| Dağıtılan hedef uygulama | Yapı Taşı: [SaaS Federasyon SSO yapılandırma](#saas-federated-sso-configuration) |

### <a name="steps"></a>Adımlar

| Adım | Kaynaklar |
| --- | --- |
| Azure AD yönetim portalında tooEnterprise uygulamalar dikey gidin | [Azure AD yönetim portalında: Kurumsal uygulamalar](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/AllApps/menuId/) |
| Ön koşullar uygulamadan kendini hizmeti ile yapılandırma | [Azure Active Directory'de Kurumsal Uygulama Yönetimi'nde yenilikler: Self Servis uygulama erişimi yapılandırma](active-directory-enterprise-apps-whats-new-azure-portal.md#configure-self-service-application-access) |
| Merhaba bilgi çalışanı toomy uygulamaları portal oturum açın | http://myapps.microsoft.com |
| Fark "+ uygulama Ekle" op hello sayfasının düğmesini. Tooget erişim toohello uygulama kullanma |  |

### <a name="considerations"></a>Dikkat edilmesi gerekenler

Seçilen hello uygulamaların hemen toohello uygulama giderek bazı hatalara neden olabilecek şekilde gereksinimleri, sağlama olabilir. Azure ad ile sağlama seçilen Merhaba uygulaması destekliyorsa ve yapılandırıldığından, bu son tooend çalışan bir fırsat tooshow hello tüm akışı kullanabilirsiniz. Merhaba Yapı bloğu için bkz: [SaaS Federasyon SSO yapılandırma](#saas-federated-sso-configuration) daha fazla önerileri için

## <a name="self-service-password-reset"></a>Self Servis parola sıfırlama

Yaklaşık bir saat tooComplete: 15 dakika

### <a name="pre-requisites"></a>Ön koşullar

| Önkoşul | Kaynaklar |
| --- | --- |
| Kiracınızda Self Servis parola yönetimini etkinleştirin. | [Azure Active Directory parola BT yöneticileri için sıfırlama](active-directory-passwords.md) |
| Şirket içi parola geri yazma toomanage parolaları etkinleştirin. Bunu gerektiren belirli Azure AD Not sürümleri Bağlan | [Parola Geri Yazma önkoşulları](active-directory-passwords-writeback.md) |
| Bu işlevselliği kullanmak ve bir güvenlik grubunun üyesi olduğundan emin olun hello PoC kullanıcıları belirleyin. Merhaba kullanıcıların yönetici olmayanlar toofully gösterimi hello yeteneğinin olması gerekir | [Özelleştirme: Azure AD parola yönetimi: erişimi kısıtla toopassword Sıfırla](active-directory-passwords-writeback.md) |


### <a name="steps"></a>Adımlar

| Adım | Kaynaklar |
| --- | --- |
| TooAzure AD gidin Yönetim Portalı: parola sıfırlama | [Azure AD yönetim portalında: Parola sıfırlama](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset) |
| Merhaba parola sıfırlama İlkesi belirler. POC amacıyla, telefon araması ve soru- cevap kullanabilirsiniz Oturum tooaccess panelinde gerekli tooenable kayıt toobe önerilir. |  |
| Oturumu kapatın ve bir bilgi çalışanı oturum açın |  |
| 2. adım yapılandırıldığı şekilde Hello Self Servis parola sıfırlama verileri kaynağı | http://aka.MS/ssprsetup |
| Kapat hello tarayıcı |  |
| 4. adımda kullanılan hello bilgi çalışanı olarak Hello oturum açma işlemini Başlat |  |
| Merhaba parola sıfırlama | [Kendi parolanızı güncelleştirin: parolamı sıfırla](active-directory-passwords-update-your-own-password.md) |
| Tooon içi kaynakların yanı sıra, yeni parola tooAzure AD oturum açma deneyin |  |

### <a name="considerations"></a>Dikkat edilmesi gerekenler

1. Yükseltme hello Azure AD Connect toocause uyuşmazlık olacaksa, ardından karşı bulut hesapları kullanmayı düşünün veya ayrı bir ortamda karşı demo olun
2. başka bir ilke Hello yöneticilerin sahip ve hello Yöneticisi kullanarak hesabı tooreset hello parolası hello PoC taint ve karışıklığa neden. Normal bir kullanıcı hesabı tootest hello sıfırlama işlemleri kullandığınızdan emin olun


## <a name="azure-multi-factor-authentication-with-phone-calls"></a>Azure multi-Factor Authentication telefon çağrısı ile

Yaklaşık bir saat tooComplete: 10 dakika

### <a name="pre-requisites"></a>Ön koşullar

| Önkoşul | Kaynaklar |
| --- | --- |
| MFA kullanacağı POC kullanıcıları tanımlayın  |  |
| MFA testini iyi alımını ile telefon  | [Azure Multi-Factor Authentication nedir?](../multi-factor-authentication/multi-factor-authentication.md) |

### <a name="steps"></a>Adımlar

| Adım | Kaynaklar |
| --- | --- |
| Çok gidin "Kullanıcılar ve Gruplar" dikey Azure AD yönetim portalında | [Azure AD yönetim portalında: Kullanıcılar ve gruplar](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Overview/menuId/) |
| "Tüm kullanıcılar" dikey seçin |  |
| Merhaba üst Seç "Çok faktörlü kimlik doğrulaması" düğme çubuğu | URL için Azure MFA portalı doğrudan: https://aka.ms/mfaportal |
| Merhaba "Kullanıcı" ayarlarında hello PoC kullanıcıları seçin ve MFA için etkinleştir | [Azure Multi-Factor Authentication’da Kullanıcı Durumları](../multi-factor-authentication/multi-factor-authentication-get-started-user-states.md) |
| Merhaba PoC kullanıcı ve hello güçlü işlemiyle ilerlemesi olarak oturum açın  |  |

### <a name="considerations"></a>Dikkat edilmesi gerekenler

1. Bu yapı taşı açıkça MFA bir kullanıcı için tüm oturum ayarlama Hello PoC adımları. MFA hakkında daha fazla bilgi devreye koşullu erişim ve kimlik koruması gibi diğer araçları vardır hedeflenen senaryoları. Bu bir şey olacaktır POC tooproduction taşırken tooconsider.
2. Bu yapı taşı Hello PoC adımlarda hello expedience için MFA yöntemi olarak telefon aramaları açıkça kullanıyor. POC tooproduction geçiş gibi hello gibi uygulamaları kullanmanızı öneririz [Microsoft Authenticator](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) , mümkün olduğunda ikinci öğe olarak.
Daha fazla bilgi edinin: [taslak NIST özel yayını 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html)

## <a name="mfa-conditional-access-for-saas-applications"></a>SaaS uygulamaları için MFA koşullu erişim

Yaklaşık bir saat tooComplete: 10 dakika

### <a name="pre-requisites"></a>Ön koşullar

| Önkoşul | Kaynaklar |
| --- | --- |
| PoC kullanıcılar tootarget hello ilkesi tanımlayın. Bu kullanıcılar bir güvenlik grubu tooscope hello koşullu erişim ilkesinde olmalıdır | [SaaS Federasyon SSO yapılandırma](#saas-federated-sso-configuration) |
| SaaS uygulamasına zaten yapılandırıldı |  |
| PoC kullanıcılara atanmış toohello uygulama |  |
| Kimlik toohello POC kullanıcı kullanılabilir |  |
| POC kullanıcı MFA için kayıtlı. Bir telefon ile iyi almayı kullanma | http://aka.MS/ssprsetup |
| Merhaba iç ağ aygıtı. Merhaba iç adres aralığındaki yapılandırılmış IP adresi | IP adresi Bul: https://www.bing.com/search?q=what%27s+my+ip |
| (Merhaba taşıyıcı ağını kullanarak bir telefon olabilir) hello dış ağ aygıtı |  |

### <a name="steps"></a>Adımlar

| Adım | Kaynaklar |
| --- | --- |
| TooAzure AD Git Yönetim Portalı: koşullu erişim dikey penceresi | [Azure AD yönetim portalında: Koşullu erişim](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) |
| Koşullu erişim ilkesi oluşturun:<br/>-Hedef PoC kullanıcılar "Kullanıcılar ve Gruplar" altında<br/>-"Bulut uygulamalarını" altında hedef PoC uygulama<br/>-Güvenilen olanları "Koşullar" altında "Konumları" -> dışında tüm konumların hedef **Not:** güvenilen IP'leri yapılandırılmış [MFA portalı](https://account.activedirectory.windowsazure.com/UserManagement/MfaSettings.aspx)<br/>-Çok faktörlü kimlik doğrulaması "Verme" altında gerektir | [Azure Active Directory'de koşullu erişimi kullanmaya başlama: İlke yapılandırma adımları](active-directory-conditional-access-azure-portal-get-started.md#policy-configuration-steps) |
| Erişim kurumsal ağ içinde uygulama | [Azure Active Directory'de koşullu erişimi kullanmaya başlama: hello ilkeyi test etme](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |
| Ortak ağ erişim uygulamadan | [Azure Active Directory'de koşullu erişimi kullanmaya başlama: hello ilkeyi test etme](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |

### <a name="considerations"></a>Dikkat edilmesi gerekenler

Federasyon kullanıyorsanız, iç/dış talep şirket ağı durumuyla hello şirket içi kimlik sağlayıcıyı (IDP) toocommunicate hello kullanabilirsiniz. Toomanage hello karmaşık tooassess olması ve büyük kuruluşlarda yönetmek IP adreslerinin listesi gerek kalmadan bu tekniği kullanabilirsiniz. Bu kurulum, hello "Gezici ağ" senaryo (Merhaba iç ağdan ve oturum açmış anahtarları sırasında bir kafe gibi konumları günlüğü bir kullanıcı) için hesap ve hello kavradığınızdan emin olun. Daha fazla bilgi edinin: [Azure multi-Factor Authentication ve AD FS ile bulut kaynakları güvenliğini sağlama: güvenilen IP'leri Federasyon kullanıcıları için](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md#trusted-ips-for-federated-users)

## <a name="privileged-identity-management-pim"></a>Privileged Identity Management (PIM)

Yaklaşık bir saat tooComplete: 15 dakika

### <a name="pre-requisites"></a>Ön koşullar

| Önkoşul | Kaynaklar |
| --- | --- |
| Merhaba PIM POC parçası olacak hello genel yönetici tanımlayın | [Azure AD Privileged Identity Management kullanmaya başlayın](active-directory-privileged-identity-management-getting-started.md) |
| Merhaba güvenlik yöneticisi olacak hello genel yönetici tanımlayın | [Azure AD Privileged Identity Management kullanmaya başlayın](active-directory-privileged-identity-management-getting-started.md)<br/> [Azure Active Directory PIM farklı yönetim rolleri](active-directory-privileged-identity-management-roles.md) |
| İsteğe bağlı: hello genel yönetici e-posta olup olmadığını onaylayın erişim PIM tooexercise e-posta bildirimleri | [Azure AD Privileged Identity Management nedir?: hello rol etkinleştirme ayarlarını yapılandırma](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)


### <a name="steps"></a>Adımlar

| Adım | Kaynaklar |
| --- | --- |
| Oturum açma toohttps://portal.azure.com genel yönetici (GA) ve önyükleme hello PIM dikey olarak. Bu adımı gerçekleştirir genel yönetici Hello hello güvenlik yönetici olarak sağlanmış.  Şimdi bu aktör GA1 çağırın | [Azure AD Privileged Identity Management Hello Güvenlik Sihirbazı'nı kullanma](active-directory-privileged-identity-management-security-wizard.md) |
| Merhaba genel yönetici tanımlamak ve kalıcı tooeligible taşıyın. Bu gelen hello daha anlaşılır olması için 1. adımda kullanılan ayrı bir yönetici olmanız gerekir. Şimdi bu aktör GA2 çağırın | [Azure AD Privileged Identity Management: Nasıl tooadd veya bir kullanıcı rolünü kaldır](active-directory-privileged-identity-management-how-to-add-role-to-user.md)<br/>[Azure AD Privileged Identity Management nedir?: hello rol etkinleştirme ayarlarını yapılandırma](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)  |
| Şimdi, GA2 toohttps://portal.azure.com oturum açın ve "Kullanıcı ayarları" değiştirmeyi deneyin. Bazı seçenekler gri unutmayın. | |
| Yeni bir sekme ve hello aynı oturum adım 3, şimdi toohttps://portal.azure.com gidin ve hello PIM dikey toohello Pano ekleyin. | [Nasıl tooactivate veya Azure AD Privileged Identity Management rollerinde devre dışı bırakma: Merhaba Privileged Identity Management uygulaması ekleyin](active-directory-privileged-identity-management-how-to-activate-role.md#add-the-privileged-identity-management-application) |
| İstek etkinleştirme toohello genel yönetici rolü | [Nasıl tooactivate veya Azure AD Privileged Identity Management rollerinde devre dışı bırakma: rol etkinleştirme](active-directory-privileged-identity-management-how-to-activate-role.md#activate-a-role) |
| GA2 hiçbir zaman MFA için kaydolduysanız, kaydı Azure MFA için gerekli olduğunu unutmayın |  |
| Adım 3'te toohello özgün sekmesine geri dönün ve hello tarayıcı hello Yenile düğmesini tıklatın. "Kullanıcı ayarları" erişim toochange şimdi sahip gerektiğini unutmayın | |
| İsteğe bağlı olarak, genel Yöneticiler e-posta etkinleştirilmiş varsa, bilgisayarınızda GA1 ve GA2'ın gelen kutusunu kontrol edin ve etkinleştirilmekte olan hello rolünün hello bildirim görebilirsiniz |  |
| 8 hello denetim geçmişini kontrol edin ve hello rapor tooconfirm hello GA2 ayrıcalıkların gösterilen gözlemleyin. | [Azure AD Privileged Identity Management nedir?: rol etkinliği gözden geçirin](active-directory-privileged-identity-management-configure.md#review-role-activity) |

### <a name="considerations"></a>Dikkat edilmesi gerekenler

Bu özellik Azure AD Premium P2 ve/veya EMS E5 parçasıdır

## <a name="discovering-risk-events"></a>Risk olaylarını keşfetme

Yaklaşık bir saat tooComplete: 20 dakika

### <a name="pre-requisites"></a>Ön koşullar

| Önkoşul | Kaynaklar |
| --- | --- |
| Tor tarayıcı aygıtla indirilir ve yüklenir | [Tor tarayıcı yükleyin](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Erişim tooPOC kullanıcı toodo hello oturum açma | [Azure Active Directory kimlik koruması Kılavuzu](active-directory-identityprotection-playbook.md) |

### <a name="steps"></a>Adımlar

| Adım | Kaynaklar |
| --- | --- |
| Açık tor tarayıcı | [Tor tarayıcı yükleyin](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Toohttps://myapps.microsoft.com hello POC kullanıcı hesabı ile oturum | [Azure Active Directory kimlik koruması Kılavuzu: Risk olaylarını benzetimini yapma](active-directory-identityprotection-playbook.md#simulating-risk-events) |
| 5-7 dakika bekleyin |  |
| Genel yönetici toohttps://portal.azure.com oturum açın ve hello kimlik koruması dikey penceresini açın | https://aka.MS/aadipgetstarted |
| Açık hello risk olaylar dikey penceresi. "Oturum açma işlemleri anonim IP adreslerinden" altında bir girdi görmeniz gerekir  | [Azure Active Directory kimlik koruması Kılavuzu: Risk olaylarını benzetimini yapma](active-directory-identityprotection-playbook.md#simulating-risk-events) |

### <a name="considerations"></a>Dikkat edilmesi gerekenler

Bu özellik Azure AD Premium P2 ve/veya EMS E5 parçasıdır

## <a name="deploying-sign-in-risk-policies"></a>Oturum açma riski ilkelerini dağıtma

Yaklaşık bir saat tooComplete: 10 dakika

### <a name="pre-requisites"></a>Ön koşullar

| Önkoşul | Kaynaklar |
| --- | --- |
| Tor tarayıcı aygıtla indirilir ve yüklenir | [Tor tarayıcı yükleyin](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Sınama sırasında POC kullanıcı toodo hello günlük olarak erişim |  |
| POC kullanıcı MFA ile kaydedilir. İyi alma olan bir telefon toouse emin olun | Yapı Taşı: [Azure çok faktörlü kimlik doğrulama telefon aramaları](#azure-multi-factor-authentication-with-phone-calls) |


### <a name="steps"></a>Adımlar

| Adım | Kaynaklar |
| --- | --- |
| Genel yönetici toohttps://portal.azure.com oturum açın ve hello kimlik koruması dikey penceresini açın | https://aka.MS/aadipgetstarted |
| Oturum açma risk ilkesine aşağıdaki gibi etkinleştirin:<br/>-Atanan: POC kullanıcı<br/>-Koşullar: Oturum açma riski Orta veya yüksek (oturum açma anonim konumdan kabul Orta risk düzeyi)<br/>-Denetimleri: MFA gerektirir | [Azure Active Directory kimlik koruması Kılavuzu: oturum açma riski](active-directory-identityprotection-playbook.md#sign-in-risk) |
| Açık tor tarayıcı | [Tor tarayıcı yükleyin](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Toohttps://myapps.microsoft.com hello PoC kullanıcı hesabı ile oturum |  |
| Bildirim hello MFA sınama | [Azure AD kimlik koruması ile karşılaştığında oturum açma: oturum açma riskli kurtarma](active-directory-identityprotection-flows.md#risky-sign-in-recovery)

### <a name="considerations"></a>Dikkat edilmesi gerekenler

Bu özellik Azure AD Premium P2 ve/veya EMS E5 parçasıdır. toolearn risk olaylar hakkında daha fazla ziyaret edin: [Azure Active Directory risk olayları](active-directory-reporting-risk-events.md)

## <a name="configuring-certificate-based-authentication"></a>Sertifika tabanlı kimlik doğrulamasını yapılandırma

Yaklaşık bir saat toocomplete: 20 dakika

### <a name="pre-requisites"></a>Ön koşullar

| Önkoşul | Kaynaklar |
| --- | --- |
| Sağlanan kullanıcı sertifikadan (Windows, iOS veya Android) Kuruluş PKI aygıtla | [Kullanıcı sertifikalarını dağıtma](https://msdn.microsoft.com/library/cc770857.aspx) |
| Azure AD etki alanı ADFS ile Federasyon | [Azure AD Connect ve federasyon](./connect/active-directory-aadconnectfed-whatis.md)<br/>[Active Directory Sertifika Hizmetleri'ne Genel Bakış](https://technet.microsoft.com/library/hh831740.aspx)|
| İOS cihazları için Microsoft Authenticator uygulamasının yüklü olması | [Merhaba Microsoft Authenticator uygulaması ile çalışmaya başlama](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

### <a name="steps"></a>Adımlar

| Adım | Kaynaklar |
| --- | --- |
| "Sertifika kimlik doğrulamasını" ADFS etkinleştirin | [Kimlik doğrulama ilkelerini yapılandırmasını: tooconfigure birincil kimlik doğrulaması genel olarak, Windows Server 2012 R2](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-authentication-policies#to-configure-primary-authentication-globally-in-windows-server-2012-r2) |
| İsteğe bağlı: Sertifika kimlik doğrulaması Azure AD'de Exchange Active Sync istemciler için etkinleştirme | [Azure Active Directory'de sertifika tabanlı kimlik doğrulaması kullanmaya başlama](active-directory-certificate-based-authentication-get-started.md) |
| TooAccess Masası gidin ve kullanıcı sertifikası kullanılarak kimlik doğrulaması | https://myapps.microsoft.com |

### <a name="considerations"></a>Dikkat edilmesi gerekenler

Bu dağıtımın uyarılar hakkında daha fazla ziyaret toolearn: [ADFS: sertifika kimlik doğrulaması Azure AD ile & Office 365](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/)



> [!NOTE]
> Kullanıcı sertifikası elinde korunmalıdır. Aygıtları yönetme tarafından ya da akıllı kartlar durumunda PIN ile.



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]
