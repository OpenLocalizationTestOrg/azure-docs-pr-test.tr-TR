---
title: "Azure uygulama hizmetinde API uygulamaları için aaaService asıl kimlik doğrulaması | Microsoft Docs"
description: "Bilgi nasıl hizmet senaryoları için Azure App Service'te tooprotect bir API uygulaması."
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
ms.openlocfilehash: 94d9ee11f38293df4a2fd815ef02c59cc6defed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-principal-authentication-for-api-apps-in-azure-app-service"></a>Azure uygulama hizmetinde API uygulamaları için hizmet asıl kimlik doğrulaması
## <a name="overview"></a>Genel Bakış
Bu makalede açıklanır nasıl toouse App Service kimlik doğrulaması için *iç* tooAPI uygulamalara erişim. Bir iç toobe kaynaklarda yalnızca kendi uygulama kodu tarafından istediğiniz bir API uygulamasına sahip olduğu bir senaryodur. Bu senaryo Hello önerilen yolu tooimplement App Service'te toouse Azure AD tooprotect hello API uygulaması adı verilir. Uygulama Kimliği (hizmet sorumlusu) kimlik bilgilerini sağlayarak Azure AD'den alma bir taşıyıcı belirteci ile korunan hello API uygulaması çağırın. Merhaba alternatifleri toousing Azure AD için bkz: **hizmeti için kimlik doğrulama** hello bölümünü [Azure App Service kimlik doğrulamasına genel bakış](../app-service/app-service-authentication-overview.md#service-to-service-authentication).

Bu makalede, şunları öğreneceksiniz:

* Nasıl toouse Azure Active Directory (Azure AD) tooprotect bir API uygulamasını kimliği doğrulanmamış erişim.
* Nasıl bir API uygulaması, web uygulaması ya da Azure AD hizmet sorumlusu (uygulama kimliği) kimlik bilgilerini kullanarak mobil uygulama tooconsume korumalı bir API uygulaması. Hakkında bilgi için bir mantık uygulamasından tooconsume bkz [Logic apps ile App Service üzerinde barındırılan özel API'nizi kullanma](../logic-apps/logic-apps-custom-hosted-api.md).
* Oturum açmış kullanıcılarda tarafından bir tarayıcıdan toomake API uygulaması bu hello korumalı emin nasıl çağrılamaz.
* Nasıl toomake bu hello korumalı API uygulaması emin yalnızca çağrılabilir tarafından belirli bir Azure AD hizmet sorumlusu.

Merhaba makale iki bölüm içerir:

* Merhaba [nasıl tooconfigure hizmet asıl kimlik doğrulaması Azure App Service'te](#authconfig) bölümde açıklanmıştır genel nasıl tooconfigure kimlik doğrulaması herhangi bir API uygulama ve API uygulaması tooconsume hello nasıl korumalı. Bu bölümde, .NET, Node.js ve Java dahil App Service tarafından desteklenen tooall çerçeveleri eşit oranda geçerlidir.
* Merhaba ile başlayan [hello .NET kullanmaya Başlarken öğreticilerine devam etme](#tutorialstart) bölümünde, hello öğretici kılavuzları, App Service içinde çalışan .NET örnek uygulaması için bir "iç erişim" senaryosu yapılandırılırken aracılığıyla. 

## <a id="authconfig"></a>Nasıl tooconfigure hizmet Azure App Service'te asıl kimlik doğrulaması
Bu bölümde tooany API uygulaması geçerli olan genel yönergeleri sağlar. Adımları belirli toohello tooDo listesi .NET örnek uygulaması için çok Git[hello .NET API uygulamaları öğretici serisi etmeden](#tutorialstart).

1. Merhaba, [Azure portal](https://portal.azure.com/), toohello gidin **ayarları** tooprotect istediğiniz ve hello bulur hello API uygulaması dikey **özellikleri** 'yetıklayın**Kimlik doğrulama / yetkilendirme**.
   
    ![Kimlik doğrulama/yetkilendirme Azure portalında](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. Merhaba, **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **üzerinde**.
3. Merhaba, **istek kimliği doğrulanmamış olduğunda eylem tootake** aşağı açılan listesinden, **Azure Active Directory ile oturum aç** .
4. Altında **kimlik doğrulama sağlayıcıları**seçin **Azure Active Directory**.
   
    ![Kimlik doğrulama/yetkilendirme dikey Azure portalında](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. Merhaba yapılandırma **Azure Active Directory ayarları** dikey toocreate yeni bir Azure AD uygulaması ya da kullanım zaten varsa var olan Azure AD uygulaması toouse istiyor.
   
    İç senaryoları genellikle bir API uygulamasını çağıran bir API uygulaması içerir. Ayrı Azure kullanabileceğiniz her API uygulaması için AD uygulamaları ya da tek bir Azure AD uygulaması.
   
    Bu dikey hakkında ayrıntılı yönergeler için bkz: [nasıl tooconfigure App Service uygulama toouse Azure Active Directory oturum açma](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
6. Merhaba kimlik doğrulama sağlayıcısı yapılandırma dikey bittiğinde, tıklatın **Tamam**.
7. Merhaba, **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **kaydetmek**.
   
    ![Kaydet’e tıklayın.](./media/app-service-api-dotnet-service-principal-auth/authsave.png)

Bu yapıldığında, uygulama hizmeti yalnızca istekleri yapılandırılmış hello Azure AD kiracısında arayanlara izin verir. Hiçbir kimlik doğrulama veya yetkilendirme kodu hello korumalı bir API uygulaması gereklidir. Merhaba taşıyıcı belirteci toohello API uygulaması yaygın olarak kullanılan talep birlikte HTTP üstbilgilerinde geçirilir ve bir hizmet sorumlusu gibi belirli bir çağıran istekleri arasındadır kod toovalidate, bu bilgileri okuyabilir.

Bu kimlik doğrulama işlev hello çalışır tüm diller için aynı şekilde bu uygulama hizmeti destekler, .NET, Node.js ve Java dahil olmak üzere. 

#### <a name="how-tooconsume-hello-protected-api-app"></a>API uygulaması tooconsume hello nasıl korumalı
Merhaba çağıran bir Azure AD taşıyıcı belirteci ile API çağrıları sağlamanız gerekir. tooget hizmet asıl kimlik bilgilerini kullanarak bir taşıyıcı belirteci hello çağıran kullanır Active Directory Authentication Library (ADAL için [.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory), [Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs), veya [Java](https://github.com/AzureAD/azure-activedirectory-library-for-java)). bir belirteç tooget, ADAL çağrıları hello kodu bilgisinden tooADAL hello sağlar:

* Azure AD kiracınıza Hello adı.
* Merhaba istemci kimliği ve istemci gizli anahtarı (uygulama anahtarı) hello arayanla ilişkili hello Azure AD uygulaması.
* Merhaba hello ile ilişkili Azure AD uygulaması Hello istemci kimliği API uygulaması korumalı. (Yalnızca bir Azure AD uygulaması kullandıysanız, bu olduğu hello aynı istemci kimliği hello arayan için bir tane hello gibi.)

Bu değerler hello hello Azure AD sayfalarında kullanılabilir [Klasik Azure portalı](https://manage.windowsazure.com/).

Hello belirteci aldıktan sonra hello arayan, HTTP isteklerini hello yetkilendirme üst bilgisinde içerir.  Uygulama hizmeti hello belirteci doğrular ve API uygulaması hello istekleri tooreach hello korumalı sağlar.

#### <a name="how-tooprotect-hello-api-app-from-access-by-users-in-hello-same-tenant"></a>Nasıl hello bulunan kullanıcılar tarafından erişim tooprotect hello API uygulamasını aynı Kiracı
Taşıyıcı belirteçlerini aynı Kiracı Merhaba geçerli değerlendirilir hello kullanıcılar için API uygulaması korumalı.  Yalnızca bir hizmet sorumlusu çağırabilirsiniz tooensure istiyorsanız, korumalı API uygulaması Merhaba, API uygulaması toovalidate hello hello belirteci talepleri aşağıdaki hello kodda korumalı ekleyin:

* `appid`Merhaba arayanla ilişkili hello Azure AD uygulama Hello istemci kimliği olmalıdır. 
* `oid`(`objectidentifier`) hello arayanın hello hizmet asıl kimliği olmalıdır. 

App Service ayrıca hello sağlar `objectidentifier` hello X-MS-CLIENT-PRINCIPAL-ID üstbilgisinde talep.

### <a name="how-tooprotect-hello-api-app-from-browser-access"></a>Nasıl tooprotect hello tarayıcı erişimi API uygulaması
Korumalı hello API uygulaması kodda Taleplerde doğrulamaz ve ayrı bir kullanırsanız, Azure AD uygulaması hello API uygulaması, korumalı için Azure AD uygulama yanıt URL'si bu hello değil hello API uygulamasının temel URL'si hello aynı olduğundan emin olun. Merhaba yanıt URL'si doğrudan korumalı toohello API uygulaması işaret ediyorsa, hello aynı Azure AD kiracısında bir kullanıcı, toohello API uygulamasına göz atın, oturum açın ve başarıyla hello API çağrısı.

## <a id="tutorialstart"></a>Merhaba .NET API uygulamaları öğretici serisi etmeden
Merhaba Node.js ve Java öğretici seri için API uygulamaları izliyorsanız, toohello atla [sonraki adımlar](#next-steps) bölümü. 

Bu makalenin sonraki bölümlerinde Hello hello .NET API uygulamaları öğretici serisi devam eder ve hello tamamladığınızı varsaymaktadır [kullanıcı kimlik doğrulaması öğretici](app-service-api-dotnet-user-principal-auth.md) ve kullanıcı kimlik doğrulaması ile Azure'da çalışan Merhaba örnek uygulaması etkin.

## <a name="set-up-authentication-in-azure"></a>Azure kimlik doğrulaması ayarlama
Bu bölümde bu hello yalnızca HTTP istekleri tooreach hello veri katmanı API uygulaması verir; bu nedenle hello geçerli Azure sahip olanları uygulama hizmeti yapılandırma AD taşıyıcı belirteçlerini. 

Bölümden hello içinde hello orta katman API uygulamasını toosend uygulama kimlik bilgilerini tooAzure AD yapılandırmak, bir taşıyıcı belirteci ulaşırsınız ve hello taşıyıcı belirteci toohello veri katmanı API uygulaması Gönder. Bu işlem hello şemada gösterilmiştir.

![Hizmet kimlik doğrulama diyagramı](./media/app-service-api-dotnet-service-principal-auth/appdiagram.png)

Aşağıdaki hello öğretici yönergeleri sırasında sorunları alıyorsanız hello bkz [sorun giderme](#troubleshooting) hello öğretici hello sonunda bölüm. 

1. Merhaba, [Azure portal](https://portal.azure.com/), toohello gidin **ayarları** hello Todolistdataapı (veri katman) API uygulaması için oluşturduğunuz ve ardından hello API uygulaması dikey **ayarları**.
2. Merhaba, **ayarları** dikey penceresinde, Bul hello **özellikleri** bölümünde ve ardından **kimlik doğrulama / yetkilendirme**.
   
    ![Kimlik doğrulama/yetkilendirme Azure portalında](./media/app-service-api-dotnet-user-principal-auth/features.png)
3. Merhaba, **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **üzerinde**.
4. Merhaba, **istek kimliği doğrulanmamış olduğunda eylem tootake** aşağı açılan listesinden, **Azure Active Directory ile oturum aç**.
   
    Yalnızca istekleri ulaşma hello API uygulamasını kimliği doğrulanmış uygulama hizmeti tooensure neden hello ayar budur. Geçerli taşıyıcı belirteçlerini olan istekler için uygulama hizmeti hello belirteçleri toohello API uygulama boyunca aktarır ve bu bilgileri HTTP üstbilgileri yaygın olarak kullanılan talep toomake ile doldurur daha kolay kullanılabilir tooyour kodu.
5. Altında **kimlik doğrulama sağlayıcıları**, tıklatın **Azure Active Directory**.
   
    ![Kimlik doğrulama/yetkilendirme dikey Azure portalında](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
6. Merhaba, **Azure Active Directory ayarları** dikey penceresinde tıklatın **Express**.
   
    Merhaba ile **Express** seçeneği Azure otomatik olarak Azure AD içinde bir AAD uygulaması oluşturabilir [Kiracı](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    Her Azure hesabı otomatik olarak bir tane var olduğundan, Kiracı toocreate yok.
7. Altında **yönetim modu**, tıklatın **yeni AD uygulaması oluştur** zaten seçili değilse.
   
    Hello portal takılan hello **oluşturma uygulama** giriş kutusuna bir varsayılan değere sahip. Varsayılan olarak, Azure AD uygulaması hello adlı aynı hello API uygulaması gibi hello. İsterseniz, farklı bir ad girebilirsiniz.
   
    ![Azure AD ayarları](./media/app-service-api-dotnet-service-principal-auth/aadsettings.png)
   
    **Not**: alternatif olarak, tek bir Azure AD kullanabilir her ikisi de arama API uygulaması hello ve hello korumalı API uygulaması için uygulama. Bu alternatif seçerseniz, hello ihtiyaç duymaz **yeni AD uygulaması oluştur** Azure AD uygulaması öğreticide daha önce hello kullanıcı kimlik doğrulaması zaten oluşturulduğundan burada seçeneği. Bu öğretici için kullanacağınız API uygulaması ve hello çağırma hello korumalı API uygulaması için Azure AD uygulamaları ayırın.
8. Hello hello değeri Not **oluşturma uygulama** giriş kutusu; bu AAD uygulamasını hello Klasik Azure portalı daha sonra göreceğiz.
9. **Tamam** düğmesine tıklayın.
10. Merhaba, **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **kaydetmek**.
    
    ![Kaydet’e tıklayın.](./media/app-service-api-dotnet-service-principal-auth/saveauth.png)
    
    Uygulama hizmeti ile bir Azure Active Directory uygulaması oluşturur **oturum açma URL'si** ve **yanıt URL'si** toohello URL API uygulamanızın'otomatik olarak ayarlanır. Merhaba ikinci değer, AAD Kiracı toolog kullanıcılar ve erişim hello API uygulaması sağlar.

### <a name="verify-that-hello-api-app-is-protected"></a>Bu hello API uygulama korunan doğrulayın
1. Toohello hello API uygulaması URL'sini bir tarayıcıda gidin: hello içinde **API uygulaması** dikey penceresinde hello Azure portal altında hello bağlantısını tıklatın **URL**. 
   
    Kimliği doğrulanmamış istekler tooreach hello API uygulaması izin verilmediğinden, yeniden yönlendirilen tooa oturum açma ekranı demektir. 
   
    Tarayıcınız toohello Swagger kullanıcı arabirimini gidin, tarayıcınızı zaten oturum açmış--bu durumda, bir InPrivate veya Incognito penceresi açın ve toohello Swagger kullanıcı Arabirimi URL gidin.
2. AAD kiracınızda bir kullanıcının kimlik bilgileriyle oturum açın.
   
   Oturum açarken hello tarayıcıda hello "başarıyla oluşturuldu" sayfası görüntülenir.

## <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>Merhaba Todolistapı projesi tooacquire yapılandırmak ve hello Azure AD belirteci Gönder
Bu bölümde görevleri hello:

* Azure AD uygulama kimlik bilgilerini tooacquire bir belirteç kullanan hello orta katman API uygulamasında kodu ekleyin ve toohello veri katmanı API uygulaması ile HTTP istekleri göndermek.
* Gereksinim duyduğunuz hello kimlik bilgileri, Azure AD'den alın.
* Azure uygulama hizmeti çalışma zamanı ortamı hello orta katman API uygulaması ayarlarında içine Hello kimlik bilgilerini girin. 

### <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>Merhaba Todolistapı projesi tooacquire yapılandırmak ve hello Azure AD belirteci Gönder
Aşağıdaki değişiklikler Visual Studio'da hello Todolistapı projesinde hello olun.

1. Tüm hello hello kod açıklamadan çıkarın *ServicePrincipal.cs* dosya.
   
    Bu, .NET tooacquire hello Azure AD taşıyıcı belirteci için ADAL kullanır hello koddur.  Daha sonra hello Azure çalışma zamanı ortamında ayarlarız birkaç yapılandırma değerlerini kullanır. Merhaba kod aşağıdadır: 
   
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
   
    **Not:** bu kodunu hello ADAL hello projede yüklü .NET NuGet paket (Microsoft.IdentityModel.Clients.activedirectory tarafından) gerektirir. Bu proje sıfırdan oluşturuyorsanız, bu paket tooinstall gerekir. Bu paket hello API uygulaması proje yeni şablon tarafından otomatik olarak yüklenmez.
2. İçinde *denetleyicileri/ToDoListController*, hello hello kodda açıklamadan çıkarın `NewDataAPIClient` hello yetkilendirme üstbilgisinde hello belirteci tooHTTP isteklerini ekler yöntemi.
   
        client.HttpClient.DefaultRequestHeaders.Authorization =
            new AuthenticationHeaderValue("Bearer", ServicePrincipal.GetS2SAccessTokenForProdMSA().AccessToken);
3. Merhaba Todolistapı projesini dağıtma. (Merhaba projesine sağ tıklayın ve ardından **Publish > Publish**.)
   
    Visual Studio Başlangıç projesini dağıtır ve bir tarayıcı toohello web uygulamanızın temel URL'yi açar. Bu bir tarayıcıdan girişimi toogo tooa Web API'sini temel URL için normal bir 403 hata sayfası gösterilir.
4. Kapat hello tarayıcı.

### <a name="get-azure-ad-configuration-values"></a>Azure AD yapılandırma değerlerini alma
1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com/), çok Git**Azure Active Directory**.
2. Merhaba üzerinde **Directory** sekmesinde, AAD kiracınızın tıklayın.
3. Tıklatın **uygulamaları > Şirketimin sahip olduğu uygulamalar**ve ardından hello onay işaretine tıklayın.
4. Uygulamaları Hello listesinde hello hello Todolistdataapı (veri katman) API uygulaması için kimlik doğrulaması etkinleştirildiğinde Azure sizin için oluşturulmuş bir hello adına tıklayın.
5. Merhaba tıklatın **yapılandırma** sekmesi.
6. Kopya hello **istemci kimliği** değer ve nedenini bildirmeden bir yerde alabilirsiniz ondan daha sonra kaydedin. 
7. Merhaba Klasik Azure portalına geri dönün toohello listesi **Şirketimin sahip olduğu uygulamalar**ve hello orta katman Todolistapı API uygulaması (Merhaba, oluşturulan hello önceki öğreticide değil için oluşturduğunuz hello AAD uygulama'yı tıklatın Bu öğreticide oluşturulan hello).
8. Merhaba tıklatın **yapılandırma** sekmesi.
9. Kopya hello **istemci kimliği** değer ve nedenini bildirmeden bir yerde alabilirsiniz ondan daha sonra kaydedin.
10. Altında **anahtarları**seçin **1 yıl** hello gelen **seçin süresi** aşağı açılan liste.
11. **Kaydet** düğmesine tıklayın.
    
     ![Uygulama anahtarı oluştur](./media/app-service-api-dotnet-service-principal-auth/genkey.png)
12. Merhaba anahtar değerini kopyalayın ve nedenini bildirmeden bir yerde ondan daha sonra alabilirsiniz kaydedin.
    
     ![Yeni uygulama anahtarı kopyalayın](./media/app-service-api-dotnet-service-principal-auth/genkeycopy.png)

### <a name="configure-azure-ad-settings-in-hello-middle-tier-api-apps-runtime-environment"></a>Merhaba orta katman API uygulamanın çalışma zamanı ortamında Azure AD ayarları yapılandırma
1. Toohello Git [Azure portal](https://portal.azure.com/)ve ardından toohello gidin **API uygulaması** dikey penceresinde hello Todolistapı (orta katman) projesini barındıran hello API uygulaması için.
2. **Ayarlar > Uygulama Ayarları**’na tıklayın.
3. Merhaba, **uygulama ayarları** bölümünde, aşağıdaki hello anahtarları ve değerleri ekleyin:
   
   | **Anahtar** | IDA: yetkilisi |
   | --- | --- |
   | **Değer** |https://Login.microsoftonline.com/ {Azure AD Kiracı adınızı} |
   | **Örnek** |https://Login.microsoftonline.com/contoso.onmicrosoft.com |
   
   | **Anahtar** | IDA: ClientID |
   | --- | --- |
   | **Değer** |Uygulama (orta katman - Todolistapı) çağırma hello istemci kimliği |
   | **Örnek** |960adec2-b74a-484A-960adec2-b74a-484A |
   
   | **Anahtar** | IDA: ClientSecret |
   | --- | --- |
   | **Değer** |Uygulama (orta katman - Todolistapı) çağırma hello uygulama anahtarı |
   | **Örnek** |e65e8fc9-5f6b-48E8-e65e8fc9-5f6b-48E8 |
   
   | **Anahtar** | IDA: kaynak |
   | --- | --- |
   | **Değer** |Uygulama adında hello istemci kimliği (veri katmanı - Todolistdataapı) |
   | **Örnek** |e65e8fc9-5f6b-48E8-e65e8fc9-5f6b-48E8 |
   
    **Not**: için `ida:Resource`, uygulamanın adlı hello kullandığınızdan emin olun **istemci kimliği** ve kendi **uygulama kimliği URI'si**.
   
    `ida:ClientId`ve `ida:Resource` farklı değerleri Bu öğretici için kullandığınız olduğundan hello orta katman ve veri katmanı için Azure AD applicaations ayırın. Tek bir kullanıyorsanız API uygulaması ve hello çağırma hello için Azure AD uygulaması korumalı API uygulaması, aynı değeri hem de hello kullanırsınız `ida:ClientId` ve `ida:Resource`.
   
    hello projenin Web.config dosyasında veya hello Azure çalışma zamanı ortamı depolanabilir şekilde hello kod ConfigurationManager tooget bu değerleri kullanır. Azure App Service'te bir ASP.NET uygulaması çalışırken, ortam ayarları otomatik olarak Web.config ayarları geçersiz kılar. Ortam ayarları olan genellikle bir [daha güvenli şekilde toostore hassas bilgileri karşılaştırıldığında tooa Web.config dosyasında](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).
4. **Kaydet** düğmesine tıklayın.
   
    ![Kaydet’e tıklayın.](./media/app-service-api-dotnet-service-principal-auth/appsettings.png)

### <a name="test-hello-application"></a>Merhaba uygulamayı test etme
1. Bir tarayıcıda toohello hello AngularJS ön uç web uygulamasının HTTPS URL'sini gidin.
2. Merhaba tıklatın **tooDo listesi** sekmesi ve Azure AD kiracınızda bir kullanıcının kimlik bilgilerini oturum. 
3. Merhaba uygulaması çalışma Yapılacaklar öğelerini tooverify ekleyin.
   
    ![tooDo Listesi Sayfası](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)
   
    Merhaba uygulaması beklendiği gibi çalışmazsa, tüm hello Azure portal girdiğiniz hello ayarlarını denetleyin. Hello ayarlarının tümünü toobe doğru görünüyorsa, hello bkz [sorun giderme](#troubleshooting) Bu öğreticinin ilerleyen bölümlerinde.

## <a name="protect-hello-api-app-from-browser-access"></a>Merhaba API uygulaması tarayıcı erişime karşı koruyun
Bu öğretici için oluşturduğunuz ayrı bir hello Todolistdataapı (veri katman) API uygulaması için Azure AD uygulaması. Uygulama hizmeti bir AAD uygulaması oluşturduğunda, gördüğünüz gibi bir kullanıcı toogo toohello API uygulamasının URL'sini bir tarayıcı ve günlük etkinleştirir şekilde hello AAD uygulamayı yapılandırır. Bu bir son kullanıcı, Azure AD kiracınız, yalnızca bir hizmet sorumlusu mümkündür, API tooaccess hello gösterir. 

API uygulaması korumalı hello herhangi bir kod yazmadan olmadan tooprevent tarayıcı erişimi isterseniz hello değiştirebilirsiniz **yanıt URL'si** hello AAD uygulaması ana URL böylece hello API uygulamanın farklı. 

### <a name="disable-browser-access"></a>Tarayıcı erişimini devre dışı bırakma
1. Merhaba Klasik portalın içinde **yapılandırma** sekmesinde Merhaba TodoListService oluşturulduğu Merhaba AAD uygulaması için hello hello değeri değiştirin **yanıt URL'si** böylece geçerli URL ancak değil hello API uygulamanızın olan alan URL.
2. **Kaydet** düğmesine tıklayın.

### <a name="verify-browser-access-no-longer-works"></a>Tarayıcı erişimi artık çalıştığını doğrulayın
Daha önce toohello API uygulaması URL'sini bir tarayıcı üzerinden tek bir kullanıcının kimlik bilgileriyle oturum açarak gidebileceği doğrulandı. Bu bölümde, bu artık mümkün olduğunu doğrulayın. 

1. Yeni bir tarayıcı penceresinde hello API uygulaması URL'sini toohello tekrar gidin.
2. Ne zaman günlüğüne toodo şekilde istenir.
3. Oturum açma başarılı olur, ancak tooan hata sayfasının yol açar.
   
    Merhaba AAD uygulama yapılandırılmış hello AAD Kiracı kullanıcılar oturum açın ve bir tarayıcıdan hello API'sine erişim. Toohello web uygulamanızın URL'sine giderek ve daha fazla yapılacak iş öğeleri ekleme doğrulayabilir bir hizmet asıl belirteci kullanarak hello API uygulaması erişmeye devam edebilirsiniz.

## <a name="restrict-access-tooa-particular-service-principal"></a>Erişim tooa belirli bir hizmet asıl kısıtla
Şimdi, bir kullanıcı için bir belirteç elde edebilirsiniz herhangi bir çağırıcı sağ veya Azure AD kiracınızda hizmet sorumlusu hello Todolistdataapı (veri katman) API uygulaması arayabilirsiniz. Bu hello veri katmanı API uygulaması yalnızca hello Todolistapı (orta katman) API uygulaması'ndan ve yalnızca belirli bir hizmet asıl gelen çağrıları kabul emin toomake isteyebilirsiniz. 

Kod toovalidate hello ekleyerek bu kısıtlamaları ekleyebilirsiniz `appid` ve `objectidentifier` gelen çağrıları talep.

Bu öğretici için uygulama kimliği ve hizmet asıl kimliği doğrudan denetleyici eylemleri doğrular hello kodu koyun.  Alternatifleri olan toouse özel `Authorize` özniteliği ya da toodo bu doğrulama başlangıç dizileriniz (örneğin OWIN ara yazılımı). Merhaba ikinci bir örnek için bkz: [Bu örnek uygulama](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs). 

Değişiklikleri toohello Todolistdataapı projesini aşağıdaki hello olun.

1. Açık hello *Controllers/TodoListController.cs* dosya.
2. Ayarlama hello satırlardaki açıklamayı Kaldır `trustedCallerClientId` ve `trustedCallerServicePrincipalId`.
   
        private static string trustedCallerClientId = ConfigurationManager.AppSettings["todo:TrustedCallerClientId"];
        private static string trustedCallerServicePrincipalId = ConfigurationManager.AppSettings["todo:TrustedCallerServicePrincipalId"];
3. Merhaba CheckCallerId yöntemi Hello kodda açıklamadan çıkarın. Bu yöntem, her eylem yönteminin hello denetleyicideki hello başlangıç çağrılır. 
   
        private static void CheckCallerId()
        {
            string currentCallerClientId = ClaimsPrincipal.Current.FindFirst("appid").Value;
            string currentCallerServicePrincipalId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            if (currentCallerClientId != trustedCallerClientId || currentCallerServicePrincipalId != trustedCallerServicePrincipalId)
            {
                throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "hello appID or service principal ID is not hello expected value." });
            }
        }
4. Merhaba Todolistdataapı projesi tooAzure uygulama hizmeti yeniden dağıtın.
5. Tarayıcınızda, toohello AngularJS ön uç web uygulamanızın HTTPS URL'sine gidin ve hello giriş sayfası hello tıklayın **tooDo listesi** sekmesi.
   
    geri toohello bitiş çağrıları başarısız olduğundan Merhaba uygulaması işe yaramaz. Gerçek AppID ve objectıdentifier Hello yeni kodu denetimi ancak henüz hello doğru değerlerin toocheck yok karşı bunları. Merhaba tarayıcı geliştirici araçları konsolunu hello sunucu bir HTTP 401 hata döndürüyor bildirir.
   
    ![Geliştirici hatası Konsolu araçları](./media/app-service-api-dotnet-service-principal-auth/webapperror.png)
   
    Aşağıdaki adımları hello hello beklenen değerleri yapılandırın.
6. Azure AD PowerShell kullanarak, hello değerini hello hizmet asıl hello hello TodoListWebApp projesi için oluşturduğunuz Azure AD uygulaması için alın.
   
    a. Yönergeler için Azure PowerShell tooinstall ve tooyour abonelik bağlanmak, bkz: [Azure PowerShell kullanarak Azure Resource Manager ile](../powershell-azure-resource-manager.md).
   
    b. tooget hizmet asıl adı listesi yürütme hello `Login-AzureRmAccount` komutunu ve ardından hello `Get-AzureRmADServicePrincipal` komutu.
   
    c. Merhaba objectID hello için hizmet sorumlusu hello Todolistapı uygulamasının bulmak ve, daha sonra kopyalayabilirsiniz bir konuma kaydedin.
7. Hello Azure portal, toohello API uygulaması dikey hello Todolistdataapı projesine dağıtılan hello API uygulaması için gidin.
8. Tıklatın **ayarlar > Uygulama ayarları**.
9. Merhaba, **uygulama ayarları** bölümünde, aşağıdaki hello anahtarları ve değerleri ekleyin:
   
   | **Anahtar** | TODO:TrustedCallerServicePrincipalId |
   | --- | --- |
   | **Değer** |Uygulama arama hizmetini asıl kimliği |
   | **Örnek** |4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072 |
   
   | **Anahtar** | TODO:TrustedCallerClientId |
   | --- | --- |
   | **Değer** |Uygulama - hello Todolistapı Azure AD uygulamadan kopyalanan çağırma, istemci kimliği |
   | **Örnek** |960adec2-b74a-484A-960adec2-b74a-484A |
10. **Kaydet** düğmesine tıklayın.
    
     ![Kaydet’e tıklayın.](./media/app-service-api-dotnet-service-principal-auth/trustedcaller.png)
11. Tarayıcınızda, toohello web uygulamanızın URL'sine dönün ve hello giriş sayfası hello tıklatın **tooDo listesi** sekmesi.
    
     Bu zaman Merhaba uygulaması hello güvenilen arayan uygulama kimliği ve hizmet asıl kimliği hello beklenen değer olduğundan beklendiği gibi çalışır.
    
     ![tooDo Listesi Sayfası](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)

## <a name="building-hello-projects-from-scratch"></a>Sıfırdan Hello projeler derleme
Merhaba iki Web API projeleri hello kullanarak oluşturulmuş **Azure API uygulaması** proje şablonu ve bir Yapılacaklar listesi denetleyicisiyle değiştirerek hello varsayılan değerleri denetleyicisi. Azure AD hizmet sorumlusu belirteçleri hello Todolistapı projesinde alınırken için hello [Active Directory Authentication Library (ADAL) .NET için](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) NuGet paketi yüklendi.

Hakkında bilgi çok oluşturmak için bir AngularJS tek sayfalı uygulama ToDoListAngular gibi bir Web API arka uç ile bkz [ellere üzerindeki Laboratuvar: tek sayfa uygulama (SPA) ASP.NET Web API ve Angular.js yapı](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Hakkında bilgi için bkz tooadd Azure AD kimlik doğrulama kodu [güvenli hale getirme AngularJS tek sayfa uygulamaları Azure AD ile](../active-directory/active-directory-devquickstarts-angular.md).

## <a name="troubleshooting"></a>Sorun giderme
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Todolistapı (orta katman) ve Todolistdataapı (veri katmanı) karıştırmayın emin olun. Örneğin, bu öğreticide, kimlik doğrulama toohello veri katmanı API uygulaması eklemek **ancak hello uygulama anahtarı hello hello orta katman API uygulaması için oluşturduğunuz Azure AD uygulaması gelen gerekir**.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba son hello API uygulamaları serisi öğreticide budur. 

Azure Active Directory hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın.

* [Azure AD Geliştirici Kılavuzu](http://aka.ms/aaddev)
* [Azure AD senaryoları](http://aka.ms/aadscenarios)
* [Azure AD örnekleri](http://aka.ms/aadsamples)
  
    Merhaba [WebApp-Webapı-OAuth2-AppIdentity-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet) örnek benzer toowhat, bu öğreticide, ancak App Service kimlik doğrulama kullanmadan gösterilir.

Diğer yolları hakkında bilgi toodeploy Visual Studio tooAPI uygulamalar, Visual Studio kullanarak veya projeler için [dağıtımı otomatikleştirme](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) gelen bir [kaynak denetimi sisteminden](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control), bkz: [nasıl toodeploy bir Azure App Service uygulaması](../app-service-web/web-sites-deploy.md).

