---
title: "aaaWhat uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir? | Microsoft Belgeleri"
description: "Azure Active Directory tooenable tek oturum açma tooall işiniz için gereken hello SaaS ve web uygulamaları kullanın."
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 75d1a3fd-b3c5-4495-a5c8-c4c24145ff00
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curyand
ms.openlocfilehash: 429522cbd570ab27359c4630c5a6d7b25b692ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-application-access-and-single-sign-on-with-azure-active-directory"></a>Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?
Çoklu oturum açma mümkün tooaccess olan tüm hello uygulamaları ve yalnızca bir kez tek bir kullanıcı hesabı kullanarak oturum açma tarafından toodo iş ihtiyacınız kaynakları anlamına gelir. Oturum açıldıktan sonra tüm gerekli tooauthenticate olmadan gereksinim duyduğunuz hello uygulamaları erişebilirsiniz (örn. bir parola yazın) ikinci kez.

Birçok kuruluş yazılım için son kullanıcı üretkenliğini Office 365, kutusunu ve Salesforce gibi bir hizmet (SaaS) uygulamaları olarak kullanır. Tarihsel olarak, BT personeliniz tooindividually oluşturma ve güncelleştirme her SaaS uygulamasının kullanıcı hesaplarında ve kullanıcınız tooremember her SaaS uygulaması için bir parola.

Azure Active Directory şirket içi Active Directory hello bulutunu kullanıcılar toouse etkinleştirme birincil kuruluş hesabı toonot yalnızca oturum açma tootheir etki alanına katılmış aygıtlar ve şirket kaynakları, aynı zamanda tüm hello web ve SaaS uygulamaları genişletir işlerini için gerekli.

Bu nedenle yalnızca kullanıcıların kullanıcı adlarını birden çok kümesini toomanage yoktur ve parolalar, uygulamalarına erişim otomatik olarak sağlanan XML'deki sağlanan veya kuruluş Grup üyeleri ve durumlarını ayrıca bir çalışanları olarak göre. Azure Active Directory güvenlik tanıtır ve, toocentrally etkinleştirmek erişim İdaresi denetimleri SaaS uygulamaları arasında kullanıcıların erişimini yönetin.

Azure AD, kolay tümleştirme toomany bugünün popüler SaaS uygulamalarının sağlar; kimlik ve erişim yönetimi sağlar, doğrudan oturum açma kullanıcı toosingle tooapplications sağlar veya bulmak ve bunları Office 365 veya hello Azure AD erişim paneli gibi portaldan başlatın.

Merhaba tümleştirme Hello mimarisi dört ana yapı taşları aşağıdaki hello oluşur:

* Çoklu oturum açma kuruluş hesaplarıyla Azure AD'de göre SaaS uygulamalarını kullanıcılara tooaccess sağlar. Çoklu oturum açma hangi kullanıcıların tooauthenticate tooan uygulamanın kendi tek bir kurumsal hesap kullanarak sağlar ' dir.
* Kullanıcı hazırlama, kullanıcı sağlama ve Windows Server Active Directory ve/veya Azure AD içinde yapılan değişiklikleri SaaS dayanarak hedef içine sağlamayı kaldırma özelliklerini sağlar. Bir sağlanan çoklu oturum açma doğrulandıktan sonra ne kullanıcı yetkili toobe toouse bir uygulama sağlar hesabıdır.
* SaaS tek bir nokta uygulama erişimi ve yönetimiyle hello özelliği toodelegate uygulama erişim karar yapma ve onaylar tooanyone hello kuruluşunuzdaki hello Azure Yönetim Portalı Merkezi uygulama erişim yönetimi sağlar
* Raporlama ve Azure AD'de kullanıcı etkinliğini izleme birleşik

## <a name="how-does-single-sign-on-with-azure-active-directory-work"></a>Çoklu oturum açma özelliği, Azure Active Directory ile nasıl kullanılır?
Bir kullanıcı "açtığında" tooan uygulaması, bunlar kendilerine olan gerekli tooprove oldukları bir kimlik doğrulama işlemi gidin. Çoklu oturum açma, bu genellikle hello uygulaması, depolanan bir parola girerek yapılır ve hello kullanıcının gerekli tooknow, bu parolayı.

Azure AD içinde tooapplications üç farklı şekilde toosign destekler:

* **Federe çoklu oturum açma** uygulamaları tooredirect tooAzure kendi parolasını istemek yerine, kullanıcı kimlik doğrulaması için AD sağlar. Bu uygulamalar için destek gibi SAML 2.0, WS-Federasyon veya Openıd Connect, protokoller ve çoklu oturum açma işleminin hello richest modudur desteklenir.
* **Parola tabanlı çoklu oturum açma** güvenli uygulama parola depolama ve bir web tarayıcı uzantısı veya mobil uygulama kullanarak yeniden yürütme sağlar. Bu hello uygulama tarafından sağlanan hello varolan oturum açma işlemini yararlanır ancak bir yönetici toomanage hello parolaları sağlar ve hello kullanıcı tooknow hello parola gerektirmez.
* **Varolan çoklu oturum açma** tüm mevcut çoklu oturum açma hello uygulama için ayarlanmadı, ancak bu uygulamaları bağlı toobe toohello Office 365 veya Azure AD erişim paneli portalları sağlayan ve ayrıca sağlar özelliğini Azure AD tooleverage sağlar ek zaman hello uygulamaları var. başlatılan Azure AD'de raporlama.

Bir uygulamaya bir kullanıcı kimlik doğrulaması sonra da bir hesap kaydı sağlanan Merhaba uygulaması bildiren hello uygulamayı toohave ihtiyaç duydukları burada var. izinler ve erişim düzeyi olan hello uygulamasının içinde. Bu hesap kaydını Hello sağlama ya da otomatik olarak gerçekleşebileceği veya hello kullanıcı oturum açma tek erişimi sağlanan önce el ile bir yönetici tarafından ortaya çıkabilir.

 Bu tek oturum açma modları ve aşağıda sağlama hakkında daha ayrıntılı bilgi.

### <a name="federated-single-sign-on"></a>Federasyon çoklu oturum açma
Federasyon çoklu oturum açma tooa üçüncü taraf SaaS uygulamada Azure AD'den hello kullanıcı hesabı bilgilerini kullanarak Azure AD tarafından oturumunuz otomatik olarak, kuruluş toobe içinde hello kullanıcıların oturum açma sağlar sağlar.

Bu senaryoda, zaten Azure AD ile oturumunuz açıldı ve bir üçüncü taraf SaaS uygulaması tarafından denetlenen tooaccess kaynakları istediğinizde Federasyon yeniden kimliği doğrulanmış bir kullanıcı toobe hello gereksinimini ortadan kaldırır.

Azure AD Federasyon çoklu oturum açma hello SAML 2.0, WS-Federasyon destekleyen uygulamalarla destekleyebilir veya Openıd connect protokoller.

Ayrıca bkz: [için sertifikaları yönetme federe çoklu oturum açma](active-directory-sso-certs.md)

### <a name="password-based-single-sign-on"></a>Parola tabanlı çoklu oturum açma
Parola tabanlı çoklu oturum açma yapılandırma tooa üçüncü taraf SaaS uygulamada hello kullanıcı hesabı bilgileri Merhaba üçüncü taraf SaaS uygulaması kullanarak Azure AD tarafından oturumunuz otomatik olarak, kuruluş toobe hello kullanıcılar sağlar. Bu özelliği etkinleştirdiğinizde, Azure AD toplar ve güvenli bir şekilde hello kullanıcı hesabı bilgilerini ve hello ilgili parola depolar.

Azure AD çoklu oturum açma parola tabanlı bir HTML tabanlı oturum açma sayfası olduğu tüm bulut tabanlı uygulamaları için üzerinde destekleyebilir. Özel tarayıcı eklentisi kullanarak AAD hello kullanıcının oturum açma aracılığıyla güvenli bir şekilde hello dizininden hello kullanıcı adı ve parola hello gibi uygulama kimlik bilgilerini alma işlemine otomatikleştirir ve bu kimlik bilgileri hello uygulamanın oturum açma sayfası içine girer Merhaba kullanıcı adına. İki kullanım örnekleri şunlardır:

1. **Yönetici kimlik bilgilerini yöneten** – Yöneticiler oluşturmak ve uygulama kimlik bilgilerini yönetebilir ve bu kimlik bilgileri toousers veya toohello uygulamasına erişmesi grupları atayın. Bu durumda, hello son kullanıcı tooknow hello kimlik bilgileri gerektirmez, ancak yalnızca kullanıcıların erişim panelinde veya sağlanan bağlantı üzerinden tıklayarak tek oturum açma erişimi toohello uygulama hala kazanır. Bu, hem de son yapabildiği bunlar değil tooremember gerekir veya uygulamaya özgü parolaları yönetme kullanıcılar için kullanışlı yanı sıra Merhaba yönetici tarafından hello kimlik yaşam döngüsü yönetimi sağlar. Merhaba kimlik hello otomatik oturum açma işlemi sırasında hello son kullanıcıdan gizlenmiş olan; ancak web hata ayıklama araçları ve kullanıcıların kullanarak hello kullanıcı tarafından teknik olarak bulunabilir ve yöneticiler izlemeniz gereken hello hello gibi aynı güvenlik ilkeleri kimlik bilgileri sunulan doğrudan hello kullanıcı tarafından. Yönetici tarafından sağlanan kimlik bilgileri, sosyal medya veya belge paylaşımı uygulamalar gibi çok sayıda kullanıcı arasında paylaşılan hesap erişim sağlarken çok yararlı olur.
2. **Kullanıcı kimlik bilgilerini yöneten** – yöneticiler uygulamaları tooend kullanıcıları veya grupları atayın ve hello son kullanıcıların tooenter Merhaba uygulaması kullanıcıların erişim panelinde ilk kez hello için erişme doğrudan bağlı kendi kimlik bilgilerine izin ver. Son kullanıcılar yapabildiği toocontinually ihtiyaç duydukları değil hello uygulamaya özgü parolaları hello uygulamaya erişim her zaman girin. Bu bir kolaylık oluşturur. Bu kullanım örneği, bir sürüm taş tooadministrative yönetim yapabildiği hello yönetici Merhaba uygulaması için yeni kimlik bilgileri ileriki bir tarihte hello uygulama erişim hello son kullanıcı deneyimi değiştirmeden ayarlayabilir hello kimlik bilgileri olarak da kullanılabilir.

Kimlik bilgileri, her iki durumda da şifrelenmiş bir duruma hello dizininde depolanır ve HTTPS üzerinden hello otomatik oturum açma işlemi sırasında yalnızca geçirilir. Parola tabanlı, çoklu oturum açma kullanarak, Azure AD Federasyon protokolleri destekleme kapasitesine sahip olmayan uygulamalar için uygun kimlik erişim yönetimi çözümü sunar.

Parola tabanlı SSO bir tarayıcı uzantısı toosecurely hello uygulama ve kullanıcı belirli bilgileri Al Azure AD'den kullanır ve toohello hizmet uygulayın. Azure AD tarafından desteklenen çoğu üçüncü taraf SaaS uygulamaları bu özelliği desteklemez.

Parola tabanlı, SSO için hello son kullanıcının tarayıcılar olabilir:

* Internet Explorer 8, 9, 10, 11--Windows 7 veya sonraki sürümlerde (Ayrıca bkz. [IE Uzantısı Dağıtım Kılavuzu'na](active-directory-saas-ie-group-policy.md))
* Chrome--Windows 7 veya daha sonra ve MacOS x veya sonraki sürümlerde
* Firefox 26,0 veya daha sonra--Windows XP SP2 veya sonraki ve Mac OS X 10,6 veya üzeri

**Not:** hello parola tabanlı SSO uzantısı kullanılabilir kenar Windows 10 için tarayıcı uzantıları köşesi desteklendiğinde haline gelir.

### <a name="existing-single-sign-on"></a>Varolan çoklu oturum açma
Bir uygulama için çoklu oturum açmayı yapılandırırken hello Azure Yönetim Portalı, "mevcut çoklu oturum açma" üçüncü bir seçenek sağlar. Bu seçenek yalnızca bağlantı tooan uygulaması hello yönetici toocreate sağlar ve hello erişim panelinde seçili kullanıcıların yerleştirin.

Örneğin, varsa tooauthenticate kullanıcıların Active Directory Federasyon Hizmetleri 2.0 kullanan bir uygulama yapılandırılmış, bir yönetici'hello erişim paneline seçeneği toocreate "var olan çoklu oturum açma" Merhaba bağlantı tooit kullanabilirsiniz. Kullanıcılar hello bağlantı eriştiğinde, Active Directory Federasyon Hizmetleri 2.0 veya ne olursa olsun varolan tek oturum açma çözümü hello uygulama tarafından sağlanan kullanılarak doğrulanır.

### <a name="user-provisioning"></a>Kullanıcı hazırlama
Select uygulamaları için Azure AD otomatik kullanıcı sağlamayı ve hesaplarının hello Azure Yönetim Portalı, Windows Server Active Directory veya Azure AD kimlik bilgilerinizi kullanarak içinde üçüncü taraf SaaS uygulamalarında sağlamayı kaldırma özelliklerini sağlar. Bir kullanıcı, bu uygulamalardan birini için Azure AD'de izin verildiğinde, bir hesap otomatik olarak (Merhaba hedef SaaS uygulamasına sağlanan) oluşturulabilir.

Bir kullanıcı silindi veya Azure AD içinde kendi bilgilerini değiştirir, bu değişiklikler de hello SaaS uygulamasına yansıtılır. Bu anlamına gelir, otomatik kimlik yaşam döngüsü yönetimi yapılandırma, yöneticilerin toocontrol sağlar ve otomatik sağlama ve SaaS uygulamalardan sağlamayı kaldırma özelliklerini sağlayın. Azure AD'de bu Otomasyon kimlik yaşam döngüsü yönetimi kullanıcı sağlamayı tarafından etkinleştirilir.

toolearn daha, fazla [otomatik kullanıcı hazırlama ve sağlamayı kaldırma işlemlerini tooSaaS uygulamalar](active-directory-saas-app-provisioning.md)

## <a name="get-started-with-hello-azure-ad-application-gallery"></a>Hello Azure AD uygulama Galerisi'ni kullanmaya başlama
Hazır tooget başladı? toodeploy çoklu oturum açma Azure AD arasında ve kuruluşunuzun kullandığı, SaaS uygulamaları bu yönergeleri izleyin.

### <a name="using-hello-azure-ad-application-gallery"></a>Hello Azure AD uygulama Galerisi'ni kullanma
Merhaba [Azure Active Directory Uygulama galerisinde](https://azure.microsoft.com/marketplace/active-directory/all/) toosupport Azure Active Directory ile çoklu oturum açma biçimi bilinen uygulamaların bir listesini sağlar.

![][1]

Burada, destekledikleri hangi özellikleri tarafından uygulamaları bulmak için bazı ipuçları verilmektedir:

* Azure AD otomatik sağlama ve hello tüm "Öne çıkan" uygulamalar için sağlamayı kaldırma özelliklerini destekler [Azure Active Directory Uygulama galerisinde](https://azure.microsoft.com/marketplace/active-directory/all/).
* Özellikle destekleyen Federasyon uygulamaların bir listesini federe tekli SAML, WS-Federasyon gibi protokolünü kullanarak oturum veya Openıd Connect bulunabilir [burada](http://social.technet.microsoft.com/wiki/contents/articles/20235.azure-active-directory-application-gallery-federated-saas-apps.aspx).

Uygulamanızı bulduktan sonra izleme hello adım adım yönergeler hello uygulama galerisinde sunulan tarafından kullanmaya başlayabilir ve çoklu oturum açmayı hello Azure Yönetim Portalı tooenable.

### <a name="application-not-in-hello-gallery"></a>Uygulama hello Galerisi'nde?
Uygulamanızı hello Azure AD uygulama galerisinde bulunmazsa, bu seçenekler vardır:

* **Kullanmakta olduğunuz listede bulunmayan bir uygulama ekleyin** -kullanım hello özel kategori hello uygulama galerisinde hello Azure Yönetim Portalı tooconnect kuruluşunuz kullanarak listelenmemiş bir uygulama içinde. SAML 2.0 federe bir uygulama olarak destekleyen herhangi bir uygulama veya bir HTML tabanlı oturum açma sayfası bir parola SSO uygulama olarak olduğu herhangi bir uygulama ekleyebilirsiniz. Bu makalede daha fazla ayrıntı için bakın [kendi uygulamanızı ekleme](active-directory-saas-custom-apps.md).
* **Geliştirme kendi uygulama Ekle** - hello uygulaması geliştirdiyseniz, kendiniz hello Azure AD Geliştirici belgeleri federe tooimplement çoklu oturum açma hello yönergeleri izleyin veya Azure AD grafik API'si hello kullanarak sağlama. Daha fazla bilgi için şu kaynaklara bakın:
  
  * [Azure AD için Kimlik Doğrulama Senaryoları](active-directory-authentication-scenarios.md)
  * [https://github.com/AzureADSamples/WebApp-MultiTenant-OpenIdConnect-dotnet](https://github.com/AzureADSamples/WebApp-MultiTenant-OpenIdConnect-DotNet)
  * [https://github.com/AzureADSamples/WebApp-WebAPI-MultiTenant-OpenIdConnect-dotnet](https://github.com/AzureADSamples/WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet)
  * [https://github.com/AzureADSamples/NativeClient-WebAPI-MultiTenant-WindowsStore](https://github.com/AzureADSamples/NativeClient-WebAPI-MultiTenant-WindowsStore)
* **Bir uygulama tümleştirmesi isteği** -istek Merhaba uygulaması gereken kullanma desteği hello [Azure AD geri bildirim Forumunda](https://feedback.azure.com/forums/169401-azure-active-directory/).

### <a name="using-hello-azure-management-portal"></a>Hello Azure yönetim portalını kullanarak
Azure Yönetim Portalı tooconfigure hello uygulama çoklu oturum açma hello hello Active Directory uzantısını kullanabilirsiniz. İlk adım olarak, tooselect hello hello portalı Active Directory bölümünde bir dizinden gerekir:

![][2]

toomanage, üçüncü taraf SaaS uygulamalarınıza hello seçili dizinin uygulamalar sekmesine hello geçiş yapabilirsiniz. Bu görünüm, yöneticilerin sağlar:

* Yeni uygulamalar hello Azure AD galeri yanı sıra geliştirdiğiniz uygulamalar ekleme
* Tümleşik uygulamalar Sil
* Önceden tümleştirilmiş hello uygulamalarını yönetme

Bir üçüncü taraf SaaS uygulaması için tipik yönetim görevleri şunlardır:

* Çoklu oturum açma parolasını SSO kullanarak veya varsa hello hedef SaaS için SSO Federasyon Azure AD ile etkinleştirme
* İsteğe bağlı olarak, kullanıcı sağlama ve sağlamayı kaldırma özelliklerini (kimlik yaşam döngüsü yönetimi) kullanıcı için hazırlama etkinleştirme
* Burada kullanıcı sağlamayı etkin uygulamalar için hangi kullanıcıların erişimi seçerek toothat uygulama

Federasyon çoklu oturum açmayı destekleyen galeri uygulamaları için yapılandırma genellikle tooprovide ek yapılandırma ayarlarını ve meta veri toocreate sertifikaları gibi hello üçüncü taraf uygulama ve Azure AD arasında federe güven gerektirir. Merhaba Yapılandırma Sihirbazı'nı hello ayrıntılarını anlatılmaktadır ve kolay erişim toohello SaaS uygulama belirli veri sizinle ve yönergeler sağlar.

Otomatik kullanıcı sağlamayı desteklemeyen galeri uygulamalar için bu hesaplarınızdaki Merhaba SaaS uygulaması, toogive Azure AD izinleri toomanage gerektirir. En azından, kimlik bilgileri Azure AD toohello hedef uygulama kimliği doğrulanırken kullanması gereken tooprovide gerekir. Ek yapılandırma ayarlarını sağlanan toobe gerekmediğini Merhaba uygulaması hello gereksinimlerine bağlıdır.

## <a name="deploying-azure-ad-integrated-applications-toousers"></a>Tümleşik uygulamalar toousers Azure AD dağıtma
Azure AD toodeploy uygulamaları tooend-kuruluşunuzdaki kullanıcıların çeşitli özelleştirilebilir yollar sağlar:

* Azure AD erişim paneli
* Office 365 uygulama Başlatıcı
* Oturum açma doğrudan toofederated uygulamalar
* Ayrıntılı bağlantılar toofederated, parola tabanlı veya var olan uygulamalar

Hangi yöntemler, kuruluşunuzda toodeploy seçtiğiniz kümeleri yerdir.

### <a name="azure-ad-access-panel"></a>Azure AD erişim paneli
Merhaba erişim paneli https://myapps.microsoft.com en son kullanıcı bir kurumsal hesap ile Azure Active Directory tooview sağlayan web tabanlı bir portal olan ve atanmış olması başlatma bulut tabanlı uygulamalar toowhich erişim verilen hello Azure AD tarafından Yönetici. Bir son kullanıcı ile varsa [Azure Active Directory Premium](https://azure.microsoft.com/pricing/details/active-directory/), hello erişim paneli üzerinden Self Servis Grup Yönetimi özellikleri de kullanabilir.

![][3]

Merhaba erişim paneli hello Azure Yönetim Portalı ' ayrıdır ve kullanıcıların toohave bir Azure aboneliği veya Office 365 aboneliği gerektirmez.

Merhaba hello Azure AD erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

### <a name="office-365-application-launcher"></a>Office 365 uygulama Başlatıcı
Office 365 dağıtmış olan kuruluşlar için Azure AD ile toousers atanan uygulamalar https://portal.office.com/myapps hello Office 365 portalında da görüntülenir. Bu kolay ve kullanıcılar için uygun bir kuruluş toolaunch uygulamalarını toouse ikinci bir portal gerek kalmadan kolaylaştırır ve uygulama Office 365 kullanan kurumlar için çözüm başlatma hello önerilir.

![][4]

Merhaba Office 365 uygulama Başlatıcı hakkında daha fazla bilgi için bkz: [hello Office 365 uygulama Başlatıcısı'nda görünen uygulamanızı sahip](https://msdn.microsoft.com/office/office365/howto/connect-your-app-to-o365-app-launcher).

### <a name="direct-sign-on-toofederated-apps"></a>Oturum açma doğrudan toofederated uygulamalar
SAML 2.0, WS-Federasyon veya Openıd destekleyen en Federasyon uygulamalarına Ayrıca kullanıcıların toostart hello uygulama için destek hello özelliği bağlanın ve sonra Azure AD üzerinden otomatik yeniden yönlendirme veya bir bağlantı toosign tıklayarak açtığınız. Bu hizmet sağlayıcısı olarak bilinir-oturum açma başlatılan ve en Federasyon uygulamalarına hello Azure AD uygulama galerisinde Bu destek (hello Azure Yönetim Portalı'hello uygulamanın tek oturum açma Yapılandırma Sihirbazı'ndan bağlı hello belgelerine bakın Ayrıntılar için).

![][5]

### <a name="direct-sign-on-links-for-federated-password-based-or-existing-apps"></a>Federasyon, parola tabanlı veya var olan uygulamalar için doğrudan oturum açma bağlantılar
Azure AD parola tabanlı çoklu oturum açma, varolan çoklu oturum açma ve herhangi bir biçimde Federasyon çoklu oturum açmayı destekleyen doğrudan tek oturum açma bağlantılar tooindividual uygulamalar da destekler.

Bir kullanıcı hello Azure üzerinden göndermek özel olarak hazırlanmış URL'leri bu bağlantılardır AD oturum açma işlemine hello kullanıcı gerektirmeden belirli bir uygulama başlatma, bunları, hello Azure AD erişim paneli veya Office 365. Bu tek oturum açma URL'leri hello ekran görüntüsünde gösterildiği gibi hello hello Azure Yönetim Portalı, Active Directory bölümünü önceden tümleştirilmiş herhangi bir uygulamada hello Pano sekmesi altında bulunabilir.

![][6]

Bu bağlantılar kopyalanabilir ve bir oturum açma tooprovide bağlantı seçili toohello uygulaması istediğiniz yere yapıştırılan. Bu, bir e-posta veya kullanıcı uygulama erişimi için ayarlamış olduğunuz tüm özel web tabanlı portal olabilir. Bir Azure AD doğrudan tek oturum açma URL'sini Twitter bir örneği burada verilmiştir:

`https://myapps.microsoft.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

Hello erişim paneli benzer tooorganization özgü URL'leri, bu URL hello myapps.microsoft.com etki hello etkin ya da doğrulanan etki alanlarının dizininiz için ekleyerek daha fazla özelleştirebilirsiniz. Bu, tüm kurumsal markayı hemen hello oturum açma sayfasında hello kullanıcı tooenter kullanıcı Kimliğini ilk gerek yüklendi sağlar:

`https://myapps.microsoft.com/contosobuild.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

Yetkili bir kullanıcı bu uygulamaya özgü bağlantılardan birini tıkladığında, bunlar ilk (Bunlar zaten oturum açmış durumda değilsiniz varsayılarak), Kurumsal oturum açma sayfasına bakın ve oturum açma işleminden sonra hello adresinden erişim Paneli'nde ilk durdurma olmadan yeniden yönlendirilen tootheir uygulama şunlardır. Merhaba kullanıcı tooaccess uygulama hello parola tabanlı, çoklu oturum açma tarayıcı uzantısı gibi hello ön koşullar eksikse hello bağlantı hello kullanıcı tooinstall hello eksik uzantısı ister. Merhaba bağlantı URL'si de Merhaba uygulaması için hello tek oturum açma yapılandırması değişirse sabit kalır.

Bu bağlantıları hello kullanın hello olarak aynı erişim denetimi mekanizmaları erişim paneli ve Office 365 ve bu kullanıcılar veya atanan hello Azure Yönetim Portalı'nda toohello uygulama grupları yalnızca toosuccessfully kimlik doğrulaması. Ancak, yetkilendirilmemiş herhangi bir kullanıcı oldukları erişim verilmemiş ve erişim sahip oldukları bir bağlantı tooload hello erişim paneli tooview kullanılabilir uygulamaları belirtilen açıklayan bir ileti görürsünüz.

## <a name="related-articles"></a>İlgili makaleler
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Cloud App Discovery ile bulut uygulamaları tasdik bulma](active-directory-cloudappdiscovery-whatis.md)
* [Giriş tooManaging erişim tooApps](active-directory-managing-access-to-apps.md)
* [Dış kimlikler Azure AD'de yönetmek için özellikleri karşılaştırma](active-directory-b2b-compare-external-identities.md)

<!--Image references-->
[1]: ./media/active-directory-appssoaccess-whatis/onlineappgallery.png
[2]: ./media/active-directory-appssoaccess-whatis/azuremgmtportal.png
[3]: ./media/active-directory-appssoaccess-whatis/accesspanel.png
[4]: ./media/active-directory-appssoaccess-whatis/officeapphub.png
[5]: ./media/active-directory-appssoaccess-whatis/workdaymobile.png
[6]: ./media/active-directory-appssoaccess-whatis/deeplink.png
