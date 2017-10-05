---
title: "Azure uygulama hizmetinde API uygulamaları için kullanıcı kimlik doğrulaması | Microsoft Docs"
description: "Azure App Service'deki bir API uygulaması yalnızca kimliği doğrulanmış kullanıcılar için erişime izin vererek korumayı öğrenin."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 3896760d-46ff-4b67-b98a-edd233f24758
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: a5b713f3a60b3886d813438496d704f464d914e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a>Azure uygulama hizmetinde API uygulamaları için kullanıcı kimlik doğrulaması
## <a name="overview"></a>Genel Bakış
Bu makalede, böylece yalnızca kimliği doğrulanan kullanıcılar bunu bir Azure API uygulaması korunacak gösterilmiştir. Makalede, okuduğunuz varsayılır [Azure App Service kimlik doğrulamasına genel bakış](../app-service/app-service-authentication-overview.md).

Şunları öğreneceksiniz:

* Azure Active Directory (Azure AD) ilişkin ayrıntılı bir kimlik doğrulama sağlayıcısı yapılandırma
* Korumalı bir API uygulaması kullanmalarını nasıl [Active Directory Authentication Library (ADAL) JavaScript için](https://github.com/AzureAD/azure-activedirectory-library-for-js).

Makale iki bölüm içerir:

* [Azure App Service'te kullanıcı kimlik doğrulamasını yapılandırmak nasıl](#authconfig) bölüm App Service tarafından desteklenen tüm çerçeveler için eşit oranda geçerlidir ve genel bir API uygulaması için kullanıcı kimlik doğrulamasını yapılandırmak nasıl açıklar .NET, Node.js ve Java dahil olmak üzere.
* İle başlayarak [.NET API Apps öğreticileri etmeden](#tutorialstart) bölümünde, makale size yol gösterir, böylece kullanıcı kimlik doğrulaması için Azure Active Directory kullanan örnek bir uygulama .NET arka ucu ve bir AngularJS ön uç ile yapılandırma yoluyla. 

## <a id="authconfig"></a>Azure App Service'te kullanıcı kimlik doğrulaması yapılandırma
Bu bölümde, tüm API uygulamaları için geçerli olan genel yönergeleri sağlar. Adımları belirli yapmak listesi .NET örnek uygulaması, Git [.NET kullanmaya Başlarken öğreticilerine devam etme](#tutorialstart).

1. İçinde [Azure portal](https://portal.azure.com/), gitmek **ayarları** korumak, bulmak istediğiniz API uygulaması dikey **özellikleri** bölümünde ve ardından **kimlik doğrulama / yetkilendirme**.
   
    ![Azure portal kimlik doğrulama/yetkilendirme](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. İçinde **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **üzerinde**.
3. Seçeneklerden birini seçin **isteğin kimliği doğrulanmamış olduğunda gerçekleştirilecek eylem** aşağı açılan liste.
   
   * API uygulamanız ulaşmak için yalnızca kimliği doğrulanmış çağrıları istiyorsanız, aşağıdakilerden birini tercih **ile oturum...**  seçenekleri. Bu seçenek, API uygulaması içinde çalışan herhangi bir kod yazmak zorunda kalmadan korumanızı sağlar.
   * API uygulamanız ulaşmak için tüm çağrıları istiyorsanız, tercih **isteğine izin ver (hiçbir işlem)**. Kimlik doğrulama sağlayıcıları seçimine kimliği doğrulanmamış arayanlara yönlendirmek için bu seçeneği kullanın. Bu seçenek ile yetkilendirme işlemek için kod yazmak zorunda.
     
     Daha fazla bilgi için bkz. [Azure App Service’de API Apps için kimlik doğrulama ve yetkilendirme](app-service-api-authentication.md#multiple-protection-options).
4. Bir veya daha fazlasını seçin **kimlik doğrulama sağlayıcıları**.
   
    Görüntüyü Azure AD tarafından doğrulanmasını tüm arayanlar gerektiren seçimler gösterilmektedir.
   
    ![Azure portal kimlik doğrulama/yetkilendirme dikey penceresi](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    Bir kimlik doğrulama sağlayıcısı seçtiğinizde, portal bu sağlayıcı için bir yapılandırma dikey penceresinde görüntüler. 
   
    Kimlik doğrulama sağlayıcısı yapılandırma dikey yapılandırmaya yönelik adım ayrıntılı yönergeler için bkz: [uygulama hizmeti uygulamanızı Azure Active Directory oturum açma kullanacak şekilde yapılandırmak nasıl](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). (Azure AD hakkındaki bir makalede bağlantıyı gider, ancak makale için diğer kimlik doğrulama sağlayıcıları makalelerine bağlantı sekme içerir.)
5. Kimlik doğrulama sağlayıcısı yapılandırma dikey bittiğinde, tıklatın **Tamam**.
6. İçinde **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **kaydetmek**.

Bu yapıldığında, App Service API uygulaması düşmeden önce tüm API çağrıları kimliğini doğrular. Kimlik doğrulama hizmetleri aynı .NET, Node.js ve Java dahil olmak üzere uygulama hizmetini destekleyen tüm diller için çalışır. 

Arayan kimliği doğrulanmış API çağrıları yapma HTTP isteklerini yetkilendirme üst bilgisi kimlik doğrulama sağlayıcısının OAuth 2.0 taşıyıcı belirteci içerir. Belirteç kimlik doğrulama sağlayıcısının SDK kullanılarak edinilebilir.

## <a id="tutorialstart"></a>.NET API uygulamaları öğreticilerine devam etme
API uygulamaları için Node.js ve Java öğreticileri izliyorsanız, sonraki makaleyi atla [API uygulamaları için hizmet asıl kimlik doğrulaması](app-service-api-dotnet-service-principal-auth.md). 

API uygulamaları için .NET Öğreticisi serisi izlediğinden ve örnek uygulama konusunda belirtildiği şekilde zaten dağıttıysanız [ilk](app-service-api-dotnet-get-started.md) ve [ikinci](app-service-api-cors-consume-javascript.md) öğreticileri, atlamak için [uygulama hizmeti ve Azure AD kimlik doğrulaması ayarlama](#azureauth) bölümü.

Birinci ve ikinci öğreticileri olmadan bu öğreticiyi izleyin istiyorsanız, örnek uygulamayı dağıtmak için otomatik bir işlem kullanarak başlayacağınızı açıklayan aşağıdaki adımları uygulayın.

> [!NOTE]
> Aşağıdaki adımları ilk iki öğreticiler, tek bir istisna olarak kaldırdıysanız aynı başlangıç noktasına alın: Visual Studio olmaz zaten biliyor hangi web uygulaması veya her proje dağıtılan API uygulaması. Bu öğreticideki doğru hedeflere dağıtmak açıklanmaktadır tam yönergeler olmayacaktır anlamına gelir. Dağıtım adımları kendi yapmak nasıl getirme ile memnun değilseniz, öğretici serisinde izlemek daha iyi [ilk öğreticide](app-service-api-dotnet-get-started.md) ile başlamak daha bu dağıtım işlemi otomatik.
> 
> 

1. Tüm listelenen önkoşulları sahip olduğunuzdan emin olun [ilk öğreticide](app-service-api-dotnet-get-started.md). Listelenen önkoşullara ek olarak, bu kimlik doğrulama öğreticiler App Service web apps ve API apps Visual Studio ve Azure portal ile çalıştıktan varsayalım.
2. Tıklatın **Azure'a Dağıt** düğmesini [Yapılacaklar listesi örnek depo Benioku dosyası](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) API uygulamaları ve web uygulamasını dağıtmak için. Bu kullanabileceğiniz gibi web uygulaması ve API uygulama adlarının aramak için sonraki oluşturduğu Azure kaynak grubu not edin.
3. İndirme veya kopyalama [Yapılacaklar listesi örnek depo](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) , ile yerel olarak Visual Studio'da karşılaşmayacağınızı kodu alın.

## <a id="azureauth"></a>Uygulama hizmeti ve Azure AD kimlik doğrulaması ayarlama
Artık kullanıcıların kimliğinin doğrulanmasını gerek kalmadan Azure App Service içinde çalışan uygulama vardır. Bu bölümde aşağıdaki görevleri yaparak kimlik doğrulaması ekleyin:

* Uygulama hizmeti orta katman API uygulamasını çağırmak için Azure Active Directory (Azure AD) kimlik doğrulama gerektirecek şekilde yapılandırın.
* Azure AD uygulaması oluşturun.
* Taşıyıcı belirteci oturum açma işleminden sonra AngularJS ön ucu göndermek için Azure AD uygulaması yapılandırın. 

Öğretici yönergeleri izleyerek çalışırken sorunlarla karşılaşırsanız, bkz: [sorun giderme](#troubleshooting) öğreticinin sonunda bölüm. 

### <a name="configure-authentication-for-the-middle-tier-api-app"></a>Orta katman API uygulaması için kimlik doğrulamasını yapılandırma
1. İçinde [Azure portal](https://portal.azure.com/), gitmek **ayarları** Todolistapı projesi için oluşturduğunuz API uygulaması dikey bulmak **özellikleri** bölümünde ve ardından **kimlik doğrulama / yetkilendirme**.
   
    ![Azure portal kimlik doğrulama/yetkilendirme](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. İçinde **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **üzerinde**.
3. İçinde **isteğin kimliği doğrulanmamış olduğunda gerçekleştirilecek eylem** aşağı açılan listesinden, **Azure Active Directory ile oturum aç**.
   
    Bu seçenek, hiçbir unauathenticated istek API uygulaması ulaşabileceği sağlar. 
4. Altında **kimlik doğrulama sağlayıcıları**, tıklatın **Azure Active Directory**.
   
    ![Azure portal kimlik doğrulama/yetkilendirme dikey penceresi](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. İçinde **Azure Active Directory ayarları** dikey penceresinde tıklatın **Express**
   
    ![Azure portal kimlik doğrulama/yetkilendirme Express seçeneği](./media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    İle **Express** seçeneği, uygulama hizmeti otomatik olarak oluşturabilir Azure AD uygulaması, Azure AD'de [Kiracı](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    Her Azure hesabı otomatik olarak bir tane var olduğundan, Kiracı oluşturmanız gerekmez.
6. Altında **yönetim modu**, tıklatın **yeni AD uygulaması oluştur** seçili değilse ve içinde değeri dikkat edin **oluşturma uygulama** metin kutusu; bu AAD uygulamasını Klasik Azure portalındaki daha sonra göreceğiz.
   
    ![Azure portalında Azure AD ayarları](./media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    Azure, Azure AD kiracınıza belirtilen ada sahip bir Azure AD uygulaması otomatik olarak oluşturur. Varsayılan olarak, Azure AD uygulaması aynı API uygulaması olarak adlandırılır. İsterseniz, farklı bir ad girebilirsiniz.
7. **Tamam** düğmesine tıklayın.
8. İçinde **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **kaydetmek**.
   
    ![Kaydet’e tıklayın.](./media/app-service-api-dotnet-user-principal-auth/authsave.png)

Artık yalnızca Azure AD kiracınızdaki kullanıcıların API uygulaması çağırabilirsiniz.

### <a name="optional-test-the-api-app"></a>İsteğe bağlı: Test API uygulaması
1. Bir tarayıcıda API uygulamasının URL'sine gidin: içinde **API uygulaması** dikey Azure portalında tıklayın altındaki bağlantı **URL**.  
   
    Kimliği doğrulanmamış istekler API uygulamasına erişmesine izin verilmediği için oturum açma ekranına yeniden yönlendirilir.
   
    Tarayıcınız "başarıyla oluşturuldu" sayfası kalırsa, tarayıcı zaten oturum açmış olabilirsiniz--bu durumda, bir InPrivate veya Incognito penceresi açın ve API uygulamasının URL'sine gidin.
2. Azure AD kiracınızda bir kullanıcı için kimlik bilgilerini kullanarak oturum açın.
   
    Oturum açtınız, tarayıcıda "başarıyla oluşturuldu" sayfası görüntülenir.
3. Tarayıcıyı kapatın.

### <a name="configure-the-azure-ad-application"></a>Azure AD uygulaması yapılandırma
Azure AD kimlik doğrulaması için yapılandırıldığında, uygulama hizmeti bir Azure AD uygulaması oluşturuldu. Varsayılan olarak yeni Azure AD uygulama, taşıyıcı belirteci API uygulamasının URL'sine sağlamak üzere yapılandırıldı. Bu bölümde taşıyıcı belirtecine AngularJS ön ucu yerine doğrudan orta katman API uygulamasını sağlamak için Azure AD uygulaması yapılandırın. API uygulaması çağırdığında AngularJS ön uç belirteci API uygulamasına gönderir.

> [!NOTE]
> Ön uç ve orta için uygulama işlem tutmak için olabildiğince basit, Bu öğretici kullanır tek Azure AD bir API uygulaması katmanı. İki Azure AD uygulamaları başka bir seçenektir. Bu durumda orta katman Azure AD uygulaması çağırmak için ön uç ait Azure AD uygulama izin vermesi gerekir. Bu çok sayıda uygulama yaklaşımı her katman için izinleri üzerinde daha ayrıntılı denetim verirsiniz.
> 
> 

1. İçinde [Klasik Azure portalı](https://manage.windowsazure.com/)gidin **Azure Active Directory**.
   
   Erişmesi gereken belirli Azure Active Directory ayarları henüz mevcut Azure portalından kullanılabilir olmadığından Klasik portal kullanmak zorunda.
2. Üzerinde **Directory** sekmesinde, AAD kiracınızın tıklayın.
   
   ![Azure AD Klasik portalında](./media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. Tıklatın **uygulamaları > Şirketimin sahip olduğu uygulamalar**ve ardından onay işaretine tıklayın.
   
   Yeni uygulama görmek için sayfayı yenilemeniz gerekebilir.
4. Uygulamalar listesinde API uygulamanız için kimlik doğrulaması etkinleştirildiğinde, Azure oluşturduğunuz birinin adına tıklayın.
   
   ![Azure AD uygulamalar sekmesi](./media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. **Yapılandır**'a tıklayın.
   
   ![Azure AD Yapılandır sekmesi](./media/app-service-api-dotnet-user-principal-auth/configure.png)
6. Ayarlama **oturum açma URL'si** AngularJS web uygulamanızı, hiçbir eğik URL'si.
   
   Örneğin: https://todolistangular.azurewebsites.net
   
   ![Oturum açma URL'si](./media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. Ayarlama **yanıt URL'si** web uygulamanıza hiçbir eğik URL'si.
   
   Örneğin: https://todolistsangular.azurewebsites.net
8. **Kaydet** düğmesine tıklayın.
   
   ![Yanıt URL'si](./media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. Sayfanın alt kısmındaki tıklatın **Yönet bildirimi > indirme bildirimi**.
   
   ![Bildirim indirin](./media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. Dosya, düzenleyebileceğiniz bir konuma indirin.
11. İndirilen bildirim dosyasında arama `oauth2AllowImplicitFlow` özelliği. Bu özelliği değerini değiştirme `false` için `true`ve ardından dosyayı kaydedin.
    
    Bu ayar, bir JavaScript tek sayfalı uygulama erişimi için gereklidir. URL parçadaki döndürülecek Oauth 2.0 taşıyıcı belirteci sağlar.
12. Tıklatın **Yönet bildirimi > karşıya yükleme bildirimi**ve önceki adımda güncelleştirilmiş dosyasını karşıya yükleyin.
    
    ![Bildirim karşıya yükle](./media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. Kopya **istemci kimliği** değer ve bir yere alabilirsiniz ondan daha sonra kaydedin.

## <a name="configure-the-todolistangular-project-to-use-authentication"></a>ToDoListAngular projesi kimlik doğrulaması kullanacak şekilde yapılandırma
Bu bölümde oturum açmış kullanıcının Azure AD'den bir taşıyıcı belirtecini almak üzere Active Directory Authentication Library (ADAL) JS için kullandığı şekilde AngularJS ön uç değiştirin. Kod belirteç orta bağlayıcıya gönderilen HTTP isteklerinde aşağıdaki çizimde gösterildiği gibi içerir. 

![Kullanıcı kimlik doğrulama diyagramı](./media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

ToDoListAngular projesini dosyalarında aşağıdaki değişiklikleri yapın.

1. Açık *Index.cshtml* dosya.
2. Active Directory Authentication Library (ADAL) JS betikler için başvuru satırlardaki yorumları kaldırın.
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. Açık *app/scripts/app.js* dosya.
4. "Kimlik doğrulaması" için işaretlenmiş kod bloğunu çıkışı açıklama ve "ile kimlik doğrulaması" için işaretlenmiş kod bloğunu açıklamadan çıkarın.
   
    Bu değişiklik ADAL JS kimlik doğrulama sağlayıcısı başvuruyor ve onu yapılandırma değerlerini sağlar. Aşağıdaki adımlarda Azure AD uygulaması ve API uygulaması için yapılandırma değerlerini ayarlayın.
5. Ayarlar kodda `endpoints` değişkeni, Todolistapı projesi için oluşturduğunuz ve Azure Klasik portalından kopyalandığından istemci kimliği kümesi Azure AD uygulama kimliği bu API URL API uygulamasının URL'sine ayarlayın.
   
    Kod artık aşağıdaki örneğe benzer.
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. Çağrısında `adalProvider.init`ayarlayın `tenant` için Kiracı adınızı ve `clientId` önceki adımda kullanılan aynı değeri.
   
    Kod artık aşağıdaki örneğe benzer.
   
        adalProvider.init(
            {
                instance: 'https://login.microsoftonline.com/', 
                tenant: 'contoso.onmicrosoft.com',
                clientId: '1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3',
                extraQueryParameter: 'nux=1',
                endpoints: endpoints
            },
            $httpProvider
            );
   
    Bu değişiklikler `app.js` çağıran kodu ve çağrılan API aynı Azure AD uygulama içinde olduğunu belirtin.
7. Açık *app/scripts/homeCtrl.js* dosya.
8. "Kimlik doğrulaması" için işaretlenmiş kod bloğunu çıkışı açıklama ve "ile kimlik doğrulaması" için işaretlenmiş kod bloğunu açıklamadan çıkarın.
9. Açık *app/scripts/indexCtrl.js* dosya.
10. "Kimlik doğrulaması" için işaretlenmiş kod bloğunu çıkışı açıklama ve "ile kimlik doğrulaması" için işaretlenmiş kod bloğunu açıklamadan çıkarın.

### <a name="deploy-the-todolistangular-project-to-azure"></a>ToDoListAngular projesini Azure'a dağıtma
1. **Çözüm Gezgini**’nde ToDoListAngular projesine sağ tıklayın ve ardından **Yayımla**’ya tıklayın.
2. **Yayımla**’ta tıklayın.
   
    Visual Studio projesini dağıtır ve web uygulamanızın temel URL'sini bir tarayıcı penceresinde açar. Bu bir Web API temel URL'yi bir tarayıcı üzerinden Git girişimi için normal bir 403 hata sayfası gösterilir.
   
    Uygulamayı test önce için orta katman API uygulaması değişiklik çözümlenmedi.
3. Tarayıcıyı kapatın.

## <a name="configure-the-todolistapi-project-to-use-authentication"></a>Todolistapı projesi kimlik doğrulaması kullanacak şekilde yapılandırma
Şu anda Todolistapı projesine gönderir "*" olarak `owner` Todolistdataapı değeri. Bu bölümde oturum açmış kullanıcının Kimliğini göndermek için kodu değiştirin.

Todolistapı projesinde aşağıdaki değişiklikleri yapın.

1. Açık *Controllers/ToDoListController.cs* dosya ve ayarlar her eylem yöntemindeki satırı açıklamadan kaldırmasına `owner` Azure ad `NameIdentifier` talep değeri. Örneğin:
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    **Önemli**: kodda açıklamadan çıkarın yok `ToDoListDataAPI` yöntemi; bu daha sonra hizmet asıl kimlik doğrulaması öğretici için gerçekleştirirsiniz.

### <a name="deploy-the-todolistapi-project-to-azure"></a>Todolistapı projesini Azure'a dağıtma
1. İçinde **Çözüm Gezgini**, Todolistapı projesine sağ tıklayın ve ardından **Yayımla**.
2. **Yayımla**’ta tıklayın.
   
    Visual Studio projesini dağıtır ve API uygulamasının temel URL'sini bir tarayıcı açar.
3. Tarayıcıyı kapatın.

### <a name="test-the-application"></a>Uygulamayı test etme
1. Web uygulamasının URL'sini gidin **HTTPS değil HTTP kullanarak**.
2. Tıklatın **Yapılacaklar listesi** sekmesi.
   
    Oturum açma istenir.
3. AAD kiracınızda bir kullanıcının kimlik bilgileriyle oturum açın.
4. **Yapılacaklar listesi** sayfası görüntülenir.
   
   ![Sayfa, yapılacaklar listesi](./media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   Şimdiye kadar bunların tümünü sahibi bırakıldığından Yapılacaklar öğelerini görüntülenen "*". Orta katman öğeleri oturum açan kullanıcı için şimdi isteme ve hiçbiri henüz oluşturulmadı.
5. Uygulamanın çalıştığını doğrulamak için yeni yapılacak iş öğeleri ekleyin.
6. Başka bir tarayıcı penceresinde Todolistdataapı API uygulaması için Swagger kullanıcı Arabirimi URL'sine gidin ve **ToDoList > almak**. İçin bir yıldız işareti girin `owner` parametre ve ardından **deneyin**.
   
   Yanıt yeni yapılacak iş öğeleri gerçek olduğunu gösterir. Owner özelliği Azure AD kullanıcı kimliği.
   
   ![JSON yanıt sahibinin kimliği](./media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-the-projects-from-scratch"></a>Sıfırdan projeler derleme
İki Web API projeleri kullanılarak oluşturulan **Azure API uygulaması** proje şablonu ve varsayılan değerleri denetleyicisi ToDoList denetleyicisiyle değiştirme. 

AngularJS tek sayfalı uygulama ile Web API 2 arka plan oluşturma hakkında daha fazla bilgi için bkz: [ellere üzerindeki Laboratuvar: tek sayfa uygulama (SPA) ASP.NET Web API ve Angular.js yapı](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Azure AD kimlik doğrulama kodu ekleme hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

* [AngularJS tek güvenli hale getirme sayfasında Azure AD ile uygulamaları](../active-directory/active-directory-devquickstarts-angular.md).
* [ADAL JS v1 Tanıtımı](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a>Sorun giderme
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Todolistapı (orta katman) ve Todolistdataapı (veri katmanı) karıştırmayın emin olun. Örneğin, veri katmanı orta katman API uygulaması için kimlik doğrulama eklediğinizi doğrulayın. 
* AngularJS kaynak kodu orta katman API uygulaması URL'sini (Todolistapı, Todolistdataapı değil) ve doğru Azure başvurduğundan emin olun AD istemci kimliği 

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide bir API uygulaması için uygulama hizmeti kimlik doğrulaması kullanmak ve ADAL JS kitaplığı kullanarak API uygulamasını çağırmak öğrendiniz. Sonraki öğreticide şunları öğreneceksiniz nasıl [güvenli API uygulamanıza erişimi hizmeti senaryoları için](app-service-api-dotnet-service-principal-auth.md).

