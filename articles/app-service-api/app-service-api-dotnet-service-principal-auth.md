---
title: "Azure uygulama hizmetinde API uygulamaları için hizmet asıl kimlik doğrulaması | Microsoft Docs"
description: "Azure App Service'te API uygulaması hizmet senaryoları için korumayı öğrenin."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 7ca0bab2-1d29-4d51-b779-dce0edd34f8b
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 95653287546bbe358111ed16af0c30a53caff2b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="service-principal-authentication-for-api-apps-in-azure-app-service"></a>Azure uygulama hizmetinde API uygulamaları için hizmet asıl kimlik doğrulaması
## <a name="overview"></a>Genel Bakış
Bu makalede, App Service kimlik doğrulaması için kullanılacak açıklanmaktadır *iç* API uygulamalara erişim. Bir iç yalnızca kendi uygulama kodu tarafından tüketilebilir olmasını istediğiniz bir API uygulamasına sahip olduğu bir senaryodur. Bu senaryo App Service'te uygulamak için önerilen yol, çağrılan API uygulaması korumak için Azure AD kullanmaktır. Uygulama Kimliği (hizmet sorumlusu) kimlik bilgilerini sağlayarak Azure AD'den alma bir taşıyıcı belirteci ile korumalı API uygulaması çağırın. Azure AD kullanarak alternatifleri için bkz: **hizmeti için kimlik doğrulama** bölümünü [Azure App Service kimlik doğrulamasına genel bakış](../app-service/app-service-authentication-overview.md#service-to-service-authentication).

Bu makalede, şunları öğreneceksiniz:

* Azure Active Directory (Azure AD) bir API uygulamasını kimliği doğrulanmamış erişimden korumak için nasıl kullanılacağını.
* Azure AD hizmet sorumlusu (uygulama kimliği) kimlik bilgilerini kullanarak JavaScript'ten bir API uygulaması, web uygulaması veya mobil uygulama korumalı bir API uygulaması kullanma yapma. JavaScript'ten bir mantık uygulaması kullanma hakkında daha fazla bilgi için bkz: [Logic apps ile App Service üzerinde barındırılan özel API'nizi kullanma](../logic-apps/logic-apps-custom-hosted-api.md).
* Korumalı API uygulaması oturum açan kullanıcılar tarafından bir tarayıcıdan çağrılamaz emin olmak nasıl.
* Korumalı API uygulaması yalnızca belirli bir Azure tarafından çağrılabilir emin olmak için AD hizmeti nasıl sorumlu.

Makale iki bölüm içerir:

* [Azure App Service'te hizmet asıl kimlik doğrulaması yapılandırma konusunda](#authconfig) bölümde açıklanmıştır Genel API uygulaması için kimlik doğrulaması yapılandırma ve korumalı API uygulaması kullanma. Bu bölümde, .NET, Node.js ve Java dahil App Service tarafından desteklenen tüm çerçeveler için eşit oranda geçerlidir.
* İle başlayarak [.NET kullanmaya Başlarken öğreticilerine devam etme](#tutorialstart) bölümünde, öğreticiyi kılavuzları, App Service içinde çalışan .NET örnek uygulaması için bir "iç erişim" senaryosu yapılandırılırken aracılığıyla. 

## <a id="authconfig"></a>Azure App Service'te hizmet asıl kimlik doğrulamasını yapılandırma
Bu bölümde, tüm API uygulamaları için geçerli olan genel yönergeleri sağlar. Adımları belirli yapmak listesi .NET örnek uygulaması, Git [.NET API uygulamaları öğretici serisi etmeden](#tutorialstart).

1. İçinde [Azure portal](https://portal.azure.com/), gitmek **ayarları** korumak ve ardından bulmak istediğiniz API uygulaması dikey **özellikleri** 'ye tıklayın  **Kimlik doğrulama / yetkilendirme**.
   
    ![Kimlik doğrulama/yetkilendirme Azure portalında](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. İçinde **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **üzerinde**.
3. İçinde **isteğin kimliği doğrulanmamış olduğunda gerçekleştirilecek eylem** aşağı açılan listesinden, **Azure Active Directory ile oturum aç** .
4. Altında **kimlik doğrulama sağlayıcıları**seçin **Azure Active Directory**.
   
    ![Kimlik doğrulama/yetkilendirme dikey Azure portalında](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. Yapılandırma **Azure Active Directory ayarları** dikey yeni bir Azure AD uygulaması veya kullanmak istediğiniz bir zaten varsa, bir var olan bir Azure AD uygulaması kullanın.
   
    İç senaryoları genellikle bir API uygulamasını çağıran bir API uygulaması içerir. Ayrı Azure kullanabileceğiniz her API uygulaması için AD uygulamaları ya da tek bir Azure AD uygulaması.
   
    Bu dikey hakkında ayrıntılı yönergeler için bkz: [uygulama hizmeti uygulamanızı Azure Active Directory oturum açma kullanacak şekilde yapılandırmak nasıl](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
6. Kimlik doğrulama sağlayıcısı yapılandırma dikey bittiğinde, tıklatın **Tamam**.
7. İçinde **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **kaydetmek**.
   
    ![Kaydet’e tıklayın.](./media/app-service-api-dotnet-service-principal-auth/authsave.png)

Bu yapıldığında, uygulama hizmeti yalnızca istekleri Gelen yapılandırılmış içinde arayanlara izin veren Azure AD kiracısı. Hiçbir kimlik doğrulama veya yetkilendirme kodu korumalı bir API uygulaması gereklidir. Taşıyıcı belirteci genellikle birlikte API uygulaması için kullanılan HTTP üstbilgilerinin Taleplerde geçirilir ve bir hizmet sorumlusu gibi belirli bir çağıran gelen istekleri olduğunu doğrulamak için kodu, bu bilgileri okuyabilir.

Bu kimlik doğrulama işlev .NET, Node.js ve Java dahil olmak üzere uygulama hizmetini destekleyen tüm diller için aynı şekilde çalışır. 

#### <a name="how-to-consume-the-protected-api-app"></a>Korumalı API uygulaması kullanma
Çağıran bir Azure AD taşıyıcı belirteci ile API çağrıları sağlamanız gerekir. Hizmet asıl kimlik bilgilerini kullanarak bir taşıyıcı belirteci almak için Active Directory kimlik doğrulama kitaplığı çağıran kullanır (için ADAL [.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory), [Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs), veya [Java](https://github.com/AzureAD/azure-activedirectory-library-for-java)). Bir belirteç almak üzere ADAL çağıran kodu ADAL için aşağıdaki bilgileri sağlar:

* Azure AD kiracınızın adıdır.
* İstemci kimliği ve arayanla ilişkili Azure AD uygulamasının istemci parolası (uygulama anahtarı).
* Korumalı API uygulaması ile ilişkili Azure AD uygulamasının istemci kimliği. (Yalnızca bir Azure AD uygulaması kullandıysanız, çağıran için aynı istemci Kimliğine budur.)

Bu değerler Azure AD sayfalarını kullanılabilir [Klasik Azure portalı](https://manage.windowsazure.com/).

Belirteci aldıktan sonra çağrıyı yapan, HTTP isteklerini yetkilendirme üst içerir.  Uygulama hizmeti, belirteci doğrular ve korumalı API uygulamasına erişmek isteklere izin verir.

#### <a name="how-to-protect-the-api-app-from-access-by-users-in-the-same-tenant"></a>API uygulaması aynı Kiracı kullanıcılar tarafından erişimden korumak nasıl
Taşıyıcı belirteçlerini aynı Kiracı kullanıcılar için korumalı API uygulaması için geçerli olarak kabul edilir.  Yalnızca bir hizmet sorumlusu korumalı API uygulaması çağırabilirsiniz emin olmak istiyorsanız, aşağıdaki talepleri belirteci doğrulamak için korumalı API uygulamasında kodu ekleyin:

* `appid`arayanla ilişkili Azure AD uygulamasının istemci kimliği olmalıdır. 
* `oid`(`objectidentifier`) arayan hizmet asıl kimliği olmalıdır. 

Uygulama hizmeti de sağlar `objectidentifier` X-MS-CLIENT-PRINCIPAL-ID üstbilgisinde talep.

### <a name="how-to-protect-the-api-app-from-browser-access"></a>API uygulaması tarayıcı erişime karşı korumak nasıl
Korumalı API uygulama kodunda Taleplerde doğrulamaz ve ayrı bir kullanırsanız, korumalı API uygulaması için Azure AD uygulaması Azure AD uygulama yanıt URL'si API uygulamasının temel URL'si ile aynı olmadığından emin olun. Yanıt URL'si korumalı API uygulamasına doğrudan işaret ediyorsa, bir kullanıcı aynı Azure AD kiracısı, API uygulamasına göz atın, oturum açın ve başarıyla API çağrısı.

## <a id="tutorialstart"></a>.NET API uygulamaları öğretici serisi etmeden
API uygulamaları için Node.js ve Java öğretici serisi izliyorsanız, geçin [sonraki adımlar](#next-steps) bölümü. 

Bu makalenin sonraki bölümlerinde .NET API uygulamaları öğretici serisi devam eder ve, tamamladığınızı varsaymaktadır [kullanıcı kimlik doğrulaması öğretici](app-service-api-dotnet-user-principal-auth.md) ve kullanıcı kimlik doğrulaması etkin Azure'da çalışan örnek uygulama.

## <a name="set-up-authentication-in-azure"></a>Azure kimlik doğrulaması ayarlama
Bu bölümde sağlayan veri katmanı API uygulaması ulaşmak için yalnızca HTTP isteklerini geçerli Azure sahip olanları; böylece uygulama hizmeti yapılandırma AD taşıyıcı belirteçlerini. 

Aşağıdaki bölümde, orta katman API uygulaması için Azure AD uygulama kimlik bilgilerini göndermek, bir taşıyıcı belirteç geri almak ve veri katmanı API uygulaması taşıyıcı belirteci göndermek için yapılandırın. Bu işlem aşağıdaki çizimde gösterilmiştir.

![Hizmet kimlik doğrulama diyagramı](./media/app-service-api-dotnet-service-principal-auth/appdiagram.png)

Öğretici yönergeleri izleyerek çalışırken sorunlarla karşılaşırsanız, bkz: [sorun giderme](#troubleshooting) öğreticinin sonunda bölüm. 

1. İçinde [Azure portal](https://portal.azure.com/), gitmek **ayarları** Todolistdataapı (veri katman) API uygulaması için oluşturduğunuz ve ardından API uygulaması dikey **ayarları**.
2. İçinde **ayarları** dikey penceresinde Bul **özellikleri** bölümünde ve ardından **kimlik doğrulama / yetkilendirme**.
   
    ![Kimlik doğrulama/yetkilendirme Azure portalında](./media/app-service-api-dotnet-user-principal-auth/features.png)
3. İçinde **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **üzerinde**.
4. İçinde **isteğin kimliği doğrulanmamış olduğunda gerçekleştirilecek eylem** aşağı açılan listesinden, **Azure Active Directory ile oturum aç**.
   
    Uygulama emin olmak, yalnızca istekleri ulaşma API uygulamasını kimliği doğrulanmış hizmeti neden olan ayar budur. Geçerli taşıyıcı belirteçlerini olan istekler için uygulama hizmeti boyunca belirteçleri API uygulamasına aktarır ve HTTP üstbilgileri bu bilgileri kodunuzu daha kolay kullanılabilir hale getirmek için yaygın olarak kullanılan talepleri ile doldurur.
5. Altında **kimlik doğrulama sağlayıcıları**, tıklatın **Azure Active Directory**.
   
    ![Kimlik doğrulama/yetkilendirme dikey Azure portalında](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
6. İçinde **Azure Active Directory ayarları** dikey penceresinde tıklatın **Express**.
   
    İle **Express** seçeneği Azure otomatik olarak Azure AD içinde bir AAD uygulaması oluşturabilir [Kiracı](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    Her Azure hesabı otomatik olarak bir tane var olduğundan, Kiracı oluşturmanız gerekmez.
7. Altında **yönetim modu**, tıklatın **yeni AD uygulaması oluştur** zaten seçili değilse.
   
    Portal takılan **oluşturma uygulama** giriş kutusuna bir varsayılan değere sahip. Varsayılan olarak, Azure AD uygulaması aynı API uygulaması olarak adlandırılır. İsterseniz, farklı bir ad girebilirsiniz.
   
    ![Azure AD ayarları](./media/app-service-api-dotnet-service-principal-auth/aadsettings.png)
   
    **Not**: alternatif olarak, tek bir Azure AD kullanabilir arama API uygulaması hem de korumalı API uygulaması için uygulama. Bu alternatif seçerseniz, ihtiyacınız olmayan **yeni AD uygulaması oluştur** Azure AD uygulaması kullanıcı kimlik doğrulaması öğreticide daha önce zaten oluşturulduğundan burada seçeneği. Bu öğretici için kullanacağınız arama API uygulaması ve korumalı API uygulaması için Azure AD uygulamaları ayırın.
8. İçinde değeri Not **oluşturma uygulama** giriş kutusu; bu AAD uygulamasını Klasik Azure portalındaki daha sonra göreceğiz.
9. **Tamam** düğmesine tıklayın.
10. İçinde **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **kaydetmek**.
    
    ![Kaydet’e tıklayın.](./media/app-service-api-dotnet-service-principal-auth/saveauth.png)
    
    Uygulama hizmeti ile bir Azure Active Directory uygulaması oluşturur **oturum açma URL'si** ve **yanıt URL'si** otomatik olarak API uygulamanızın URL'sine ayarlayın. İkinci değer, kullanıcıların oturum açma ve API uygulamasına erişmek için AAD kiracınızda sağlar.

### <a name="verify-that-the-api-app-is-protected"></a>API uygulaması korunduğunu doğrulayın
1. Bir tarayıcıda API uygulamasının URL'sine gidin: içinde **API uygulaması** dikey Azure portalında tıklayın altındaki bağlantı **URL**. 
   
    Kimliği doğrulanmamış istekler API uygulamasına erişmesine izin verilmediği için oturum açma ekranına yeniden yönlendirilir. 
   
    Tarayıcınız Swagger kullanıcı arabirimini giderseniz, tarayıcınızı zaten oturum açmış olabilirsiniz--bu durumda, bir InPrivate veya Incognito penceresi açın ve Swagger kullanıcı Arabirimi URL'sine gidin.
2. AAD kiracınızda bir kullanıcının kimlik bilgileriyle oturum açın.
   
   Oturum açtınız, tarayıcıda "başarıyla oluşturuldu" sayfası görüntülenir.

## <a name="configure-the-todolistapi-project-to-acquire-and-send-the-azure-ad-token"></a>Todolistapı projesi edinmeli ve Azure AD belirteci göndermek için yapılandırma
Bu bölümde aşağıdaki görevleri yapın:

* Bir belirteç almak ve veri katmanı API uygulaması ile HTTP istekleri göndermek için Azure AD uygulama kimlik bilgilerini kullanan Orta katman API uygulamasında kodu ekleyin.
* Gereksinim duyduğunuz kimlik bilgileri, Azure AD'den alın.
* Azure uygulama hizmeti çalışma zamanı ortamı orta katman API uygulaması ayarlarında içine kimlik bilgilerini girin. 

### <a name="configure-the-todolistapi-project-to-acquire-and-send-the-azure-ad-token"></a>Todolistapı projesi edinmeli ve Azure AD belirteci göndermek için yapılandırma
Visual Studio Todolistapı projesinde aşağıdaki değişiklikleri yapın.

1. Tüm kod açıklamadan çıkarın *ServicePrincipal.cs* dosya.
   
    Bu Azure AD taşıyıcı belirtecini almak için .NET için ADAL kullanan koddur.  Daha sonra Azure çalışma zamanı ortamında ayarlarız birkaç yapılandırma değerlerini kullanır. Kod aşağıdaki gibidir: 
   
        public static class ServicePrincipal
        {
            static string authority = ConfigurationManager.AppSettings["ida:Authority"];
            static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
            static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
            static string resource = ConfigurationManager.AppSettings["ida:Resource"];
   
            public static AuthenticationResult GetS2SAccessTokenForProdMSA()
            {
                return GetS2SAccessToken(authority, resource, clientId, clientSecret);
            }
   
            static AuthenticationResult GetS2SAccessToken(string authority, string resource, string clientId, string clientSecret)
            {
                var clientCredential = new ClientCredential(clientId, clientSecret);
                AuthenticationContext context = new AuthenticationContext(authority, false);
                AuthenticationResult authenticationResult = context.AcquireToken(
                    resource,
                    clientCredential);
                return authenticationResult;
            }
        }
   
    **Not:** hangi projede zaten yüklüyse, .NET NuGet paketi (Microsoft.IdentityModel.Clients.activedirectory tarafından) için ADAL bu kodu gerektirir. Bu proje sıfırdan oluşturuyorsanız, bu paketi yüklemek gerekir. Bu paket API uygulaması yeni proje şablonu tarafından otomatik olarak yüklenmez.
2. İçinde *denetleyicileri/ToDoListController*, kodda açıklamadan çıkarın `NewDataAPIClient` HTTP belirteç ekler yöntemi yetkilendirme üst bilgi ister.
   
        client.HttpClient.DefaultRequestHeaders.Authorization =
            new AuthenticationHeaderValue("Bearer", ServicePrincipal.GetS2SAccessTokenForProdMSA().AccessToken);
3. Todolistapı projesine dağıtın. (Projeye sağ tıklayın ve ardından **Publish > Publish**.)
   
    Visual Studio projesini dağıtır ve web uygulamanızın temel URL'sini bir tarayıcı penceresinde açar. Bu bir Web API temel URL'yi bir tarayıcı üzerinden Git girişimi için normal bir 403 hata sayfası gösterilir.
4. Tarayıcıyı kapatın.

### <a name="get-azure-ad-configuration-values"></a>Azure AD yapılandırma değerlerini alma
1. İçinde [Klasik Azure portalı](https://manage.windowsazure.com/)gidin **Azure Active Directory**.
2. Üzerinde **Directory** sekmesinde, AAD kiracınızın tıklayın.
3. Tıklatın **uygulamaları > Şirketimin sahip olduğu uygulamalar**ve ardından onay işaretine tıklayın.
4. Uygulamalar listesinde Todolistdataapı (veri katman) API uygulaması için kimlik doğrulaması etkinleştirildiğinde, Azure oluşturduğunuz birinin adına tıklayın.
5. **Configure (Yapılandır)** sekmesine tıklayın.
6. Kopya **istemci kimliği** değer ve nedenini bildirmeden bir yerde alabilirsiniz ondan daha sonra kaydedin. 
7. Azure Klasik portalı Git geri listesini **Şirketimin sahip olduğu uygulamalar**ve (önceki öğreticide oluşturduğunuz, bir değil, oluşturduğunuz bir orta katman Todolistapı API uygulaması için oluşturduğunuz AAD uygulama'yı tıklatın Bu öğreticide).
8. **Configure (Yapılandır)** sekmesine tıklayın.
9. Kopya **istemci kimliği** değer ve nedenini bildirmeden bir yerde alabilirsiniz ondan daha sonra kaydedin.
10. Altında **anahtarları**seçin **1 yıl** gelen **seçin süresi** aşağı açılan liste.
11. **Kaydet** düğmesine tıklayın.
    
     ![Uygulama anahtarı oluştur](./media/app-service-api-dotnet-service-principal-auth/genkey.png)
12. Anahtar değerini kopyalayın ve nedenini bildirmeden bir yerde ondan daha sonra alabilirsiniz kaydedin.
    
     ![Yeni uygulama anahtarı kopyalayın](./media/app-service-api-dotnet-service-principal-auth/genkeycopy.png)

### <a name="configure-azure-ad-settings-in-the-middle-tier-api-apps-runtime-environment"></a>Orta katman API uygulamanın çalışma zamanı ortamında Azure AD ayarları yapılandırma
1. Git [Azure portal](https://portal.azure.com/)ve ardından gidin **API uygulaması** dikey penceresinde Todolistapı (orta katman) projesini barındıran API uygulaması için.
2. **Ayarlar > Uygulama Ayarları**’na tıklayın.
3. İçinde **uygulama ayarları** bölümünde, aşağıdaki anahtarları ve değerleri ekleyin:
   
   | **Anahtar** | IDA: yetkilisi |
   | --- | --- |
   | **Değer** |https://Login.microsoftonline.com/ {Azure AD Kiracı adınızı} |
   | **Örnek** |https://Login.microsoftonline.com/contoso.onmicrosoft.com |
   
   | **Anahtar** | IDA: ClientID |
   | --- | --- |
   | **Değer** |Arama (orta katman - Todolistapı) uygulamasının istemci kimliği |
   | **Örnek** |960adec2-b74a-484A-960adec2-b74a-484A |
   
   | **Anahtar** | IDA: ClientSecret |
   | --- | --- |
   | **Değer** |Uygulama anahtarı çağıran uygulamanın (orta katman - Todolistapı) |
   | **Örnek** |e65e8fc9-5f6b-48E8-e65e8fc9-5f6b-48E8 |
   
   | **Anahtar** | IDA: kaynak |
   | --- | --- |
   | **Değer** |Çağrılan uygulamasının istemci kimliği (veri katmanı - Todolistdataapı) |
   | **Örnek** |e65e8fc9-5f6b-48E8-e65e8fc9-5f6b-48E8 |
   
    **Not**: için `ida:Resource`, çağrılan uygulamanın kullandığınızdan emin olun **istemci kimliği** ve kendi **uygulama kimliği URI'si**.
   
    `ida:ClientId`ve `ida:Resource` farklı değerleri Bu öğretici için kullandığınız olduğundan veri katmanı ve orta katman için Azure AD applicaations ayırın. Tek bir kullanıyorsanız Azure AD uygulaması arama API uygulaması ve korumalı API uygulaması için aynı değere hem de kullanacağınız `ida:ClientId` ve `ida:Resource`.
   
    Kod ConfigurationManager projenin Web.config dosyasında veya Azure çalışma zamanı ortamı depolanabilir şekilde bu değerleri almak için kullanır. Azure App Service'te bir ASP.NET uygulaması çalışırken, ortam ayarları otomatik olarak Web.config ayarları geçersiz kılar. Ortam ayarları olan genellikle bir [Web.config dosyasına karşılaştırıldığında hassas bilgileri depolamak için yol'daha güvenli](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).
4. **Kaydet** düğmesine tıklayın.
   
    ![Kaydet’e tıklayın.](./media/app-service-api-dotnet-service-principal-auth/appsettings.png)

### <a name="test-the-application"></a>Uygulamayı test etme
1. AngularJS ön uç web uygulamasının HTTPS URL'sini bir tarayıcıda gidin.
2. Tıklatın **Yapılacaklar listesi** sekmesi ve Azure AD kiracınızda bir kullanıcının kimlik bilgilerini oturum. 
3. Uygulamanın çalıştığını doğrulamak için yapılacaklar öğelerini ekleyin.
   
    ![Sayfa, yapılacaklar listesi](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)
   
    Uygulamanın beklendiği gibi çalışmazsa, Azure portalında girdiğiniz tüm ayarları denetleyin. Tüm ayarlar doğru görünüyorsa, bkz: [sorun giderme](#troubleshooting) Bu öğreticinin ilerleyen bölümlerinde.

## <a name="protect-the-api-app-from-browser-access"></a>API uygulaması tarayıcı erişime karşı koruyun
Bu öğretici için oluşturduğunuz ayrı bir Todolistdataapı (veri katman) API uygulaması için Azure AD uygulaması. Uygulama hizmeti bir AAD uygulaması oluşturduğunda, gördüğünüz gibi AAD uygulaması bir tarayıcıda API uygulamasının URL'sine gidin ve oturum açmak kullanıcının sağlayan bir şekilde yapılandırır. Bir son kullanıcı, API erişmek için Azure AD kiracınız, yalnızca bir hizmet sorumlusu, mümkündür anlamına gelir. 

Korumalı bir API uygulaması hiçbir kod yazmadan tarayıcı erişimi engellemek isterseniz değiştirebileceğiniz **yanıt URL'si** AAD uygulamada ana URL böylece API uygulamasının farklı. 

### <a name="disable-browser-access"></a>Tarayıcı erişimini devre dışı bırakma
1. Klasik portalın içinde **yapılandırma** sekmesinde TodoListService için oluşturulmuş AAD uygulama için değeri değiştirin **yanıt URL'si** böylece geçerli bir URL ancak API uygulamasının URL değil olan alan.
2. **Kaydet** düğmesine tıklayın.

### <a name="verify-browser-access-no-longer-works"></a>Tarayıcı erişimi artık çalıştığını doğrulayın
Daha önce API uygulaması URL'sini bir tarayıcı üzerinden tek bir kullanıcının kimlik bilgileriyle oturum açarak gidebileceği doğrulandı. Bu bölümde, bu artık mümkün olduğunu doğrulayın. 

1. Yeni bir tarayıcı penceresinde tekrar API uygulamasının URL'sine gidin.
2. Bunu yapmak isteyip istemediğiniz sorulduğunda oturum açın.
3. Oturum açma başarılı olur, ancak bir hata sayfası için yol açar.
   
    AAD uygulama yapılandırılmış kullanıcılar AAD kiracısında oturum açın ve bir tarayıcıdan API'sine erişim. Web uygulamanızın URL'sine giderek ve daha fazla yapılacak iş öğeleri ekleme doğrulayabilir bir hizmet asıl belirteci kullanarak API uygulamasına erişmeye devam edebilirsiniz.

## <a name="restrict-access-to-a-particular-service-principal"></a>Belirli hizmet sorumlusuna erişimi kısıtlama
Şimdi, bir kullanıcı için bir belirteç elde edebilirsiniz herhangi bir çağırıcı sağ veya Azure AD kiracınızda hizmet sorumlusu Todolistdataapı (veri katman) API uygulaması arayabilirsiniz. Veri katmanı API uygulaması yalnızca Todolistapı (orta katman) API uygulaması'ndan ve yalnızca belirli bir hizmet asıl gelen çağrıları kabul emin olmak isteyebilirsiniz. 

Doğrulanacak kodu ekleyerek bu kısıtlamaları ekleyebilirsiniz `appid` ve `objectidentifier` gelen çağrıları talep.

Bu öğretici için uygulama kimliği ve denetleyici eylemleri de doğrudan hizmet asıl kimlik doğrulama kodu koyun.  Alternatifleri olan özel bir kullanmak için `Authorize` özniteliği ya da bu doğrulamanın yapılacağı (örneğin OWIN ara yazılımı), başlangıç serileri. İkincisi, bir örnek için bkz [Bu örnek uygulama](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs). 

Todolistdataapı projesine aşağıdaki değişiklikleri yapın.

1. Açık *Controllers/TodoListController.cs* dosya.
2. Ayarlama satırlardaki açıklamayı Kaldır `trustedCallerClientId` ve `trustedCallerServicePrincipalId`.
   
        private static string trustedCallerClientId = ConfigurationManager.AppSettings["todo:TrustedCallerClientId"];
        private static string trustedCallerServicePrincipalId = ConfigurationManager.AppSettings["todo:TrustedCallerServicePrincipalId"];
3. CheckCallerId yöntemi kodda açıklamadan çıkarın. Bu yöntem, her eylem yöntemi denetleyicideki başlangıcında çağrılır. 
   
        private static void CheckCallerId()
        {
            string currentCallerClientId = ClaimsPrincipal.Current.FindFirst("appid").Value;
            string currentCallerServicePrincipalId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            if (currentCallerClientId != trustedCallerClientId || currentCallerServicePrincipalId != trustedCallerServicePrincipalId)
            {
                throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "The appID or service principal ID is not the expected value." });
            }
        }
4. Azure App Service'e Todolistdataapı projesini yeniden dağıtın.
5. Tarayıcınızda, AngularJS ön uç web uygulamanızın HTTPS URL'si ve giriş sayfasına git tıklatın **Yapılacaklar listesi** sekmesi.
   
    Arka uç çağrılar başarısız olduğundan uygulama çalışmıyor. Yeni kod gerçek AppID ve objectıdentifier denetliyor, ancak bunlara karşı denetlemek için doğru değerleri henüz yok. Tarayıcının geliştirici araçları konsolunu, sunucunun bir HTTP 401 hata döndürmektir bildirir.
   
    ![Geliştirici hatası Konsolu araçları](./media/app-service-api-dotnet-service-principal-auth/webapperror.png)
   
    Aşağıdaki adımlarda beklenen değerleri yapılandırın.
6. Azure AD PowerShell kullanarak, TodoListWebApp projesi için oluşturduğunuz Azure AD uygulaması için hizmet sorumlusu değerini alın.
   
    a. Azure PowerShell'i yükleyin ve aboneliğinize bağlanma hakkında daha fazla yönerge için bkz: [Azure PowerShell kullanarak Azure Resource Manager ile](../powershell-azure-resource-manager.md).
   
    b. Hizmet sorumluları listesini almak için yürütme `Login-AzureRmAccount` komutu ardından `Get-AzureRmADServicePrincipal` komutu.
   
    c. Todolistapı uygulama hizmet sorumlusu için objectID bulun ve, daha sonra kopyalayabilirsiniz bir konuma kaydedin.
7. Azure portalında Todolistdataapı projesine dağıtılan API uygulaması için API uygulaması dikey penceresine gidin.
8. Tıklatın **ayarlar > Uygulama ayarları**.
9. İçinde **uygulama ayarları** bölümünde, aşağıdaki anahtarları ve değerleri ekleyin:
   
   | **Anahtar** | TODO:TrustedCallerServicePrincipalId |
   | --- | --- |
   | **Değer** |Uygulama arama hizmetini asıl kimliği |
   | **Örnek** |4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072 |
   
   | **Anahtar** | TODO:TrustedCallerClientId |
   | --- | --- |
   | **Değer** |Todolistapı Azure AD uygulamadan kopyalanan uygulama - çağırma, istemci kimliği |
   | **Örnek** |960adec2-b74a-484A-960adec2-b74a-484A |
10. **Kaydet** düğmesine tıklayın.
    
     ![Kaydet’e tıklayın.](./media/app-service-api-dotnet-service-principal-auth/trustedcaller.png)
11. Tarayıcınız, web uygulamanızın URL'sine dönüş ve giriş sayfasını tıklatın **Yapılacaklar listesi** sekmesi.
    
     Bu sefer uygulama güvenilen arayan uygulama kimliği ve hizmet asıl kimliği beklenen değer olduğundan beklendiği gibi çalışır.
    
     ![Sayfa, yapılacaklar listesi](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)

## <a name="building-the-projects-from-scratch"></a>Sıfırdan projeler derleme
İki Web API projeleri kullanılarak oluşturulan **Azure API uygulaması** proje şablonu ve varsayılan değerleri denetleyicisi ToDoList denetleyicisiyle değiştirme. Azure AD hizmet sorumlusu belirteçleri Todolistapı projesinde alınırken için [Active Directory Authentication Library (ADAL) .NET için](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) NuGet paketi yüklendi.

ToDoListAngular gibi bir Web API'si arka ucuna sahip bir AngularJS tek sayfalı uygulama oluşturma hakkında daha fazla bilgi için bkz: [ellere üzerindeki Laboratuvar: tek sayfa uygulama (SPA) ASP.NET Web API ve Angular.js yapı](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Azure AD kimlik doğrulama kodu ekleme hakkında daha fazla bilgi için bkz: [güvenli hale getirme AngularJS tek sayfa uygulamaları Azure AD ile](../active-directory/active-directory-devquickstarts-angular.md).

## <a name="troubleshooting"></a>Sorun giderme
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Todolistapı (orta katman) ve Todolistdataapı (veri katmanı) karıştırmayın emin olun. Örneğin, bu öğreticide, kimlik doğrulaması veri katmanı API uygulaması için ekleme **ancak uygulama anahtarı orta katman API uygulaması için oluşturduğunuz Azure AD uygulaması gelmelidir**.

## <a name="next-steps"></a>Sonraki adımlar
Bu API uygulamaları serideki son öğreticidir. 

Azure Active Directory hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın.

* [Azure AD Geliştirici Kılavuzu](http://aka.ms/aaddev)
* [Azure AD senaryoları](http://aka.ms/aadscenarios)
* [Azure AD örnekleri](http://aka.ms/aadsamples)
  
    [WebApp-Webapı-OAuth2-AppIdentity-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet) ne Bu öğreticide, ancak App Service kimlik doğrulama kullanmadan gösterilen için örnek benzerdir.

Visual Studio kullanarak veya API uygulamaları için Visual Studio projeleri dağıtmanın farklı yöntemleri hakkında bilgi için [dağıtımı otomatikleştirme](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) gelen bir [kaynak denetimi sisteminden](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control), bkz: [Azure dağıtma App Service uygulaması](../app-service-web/web-sites-deploy.md).

