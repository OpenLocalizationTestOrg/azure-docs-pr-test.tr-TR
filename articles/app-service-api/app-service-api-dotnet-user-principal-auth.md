---
title: "Azure uygulama hizmetinde API uygulamaları için aaaUser kimlik doğrulaması | Microsoft Docs"
description: "Nasıl tooprotect sağlayarak Azure App Service'deki bir API uygulamasına erişim yalnızca tooauthenticated kullanıcılar hakkında bilgi edinin."
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
ms.openlocfilehash: 4702fc77fcfe736405e22b033c35d22ae3c5a300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a>Azure uygulama hizmetinde API uygulamaları için kullanıcı kimlik doğrulaması
## <a name="overview"></a>Genel Bakış
Bu makalede nasıl tooprotect, yalnızca kimliği doğrulanmış kullanıcılar için bir Azure API uygulaması işleyememesi gösterilmektedir. Merhaba makalede hello okuduğunuz varsayılır [Azure App Service kimlik doğrulamasına genel bakış](../app-service/app-service-authentication-overview.md).

Şunları öğreneceksiniz:

* Nasıl tooconfigure ayrıntılarıyla Azure Active Directory (Azure AD) için bir kimlik doğrulama sağlayıcısı.
* Nasıl tooconsume kullanarak korumalı bir API uygulaması hello [Active Directory Authentication Library (ADAL) JavaScript için](https://github.com/AzureAD/azure-activedirectory-library-for-js).

Merhaba makale iki bölüm içerir:

* Merhaba [nasıl tooconfigure kullanıcı kimlik doğrulaması Azure App Service'te](#authconfig) bölümde açıklanmıştır genel nasıl herhangi bir API uygulaması için tooconfigure kullanıcı kimlik doğrulaması ve .NET dahil App Service tarafından desteklenen tooall çerçeveleri eşit oranda geçerlidir Node.js ve Java.
* Merhaba ile başlayan [hello .NET API Apps öğreticileri etmeden](#tutorialstart) bölümünde, örnek bir uygulama bir .NET ile yapılandırma yoluyla geri uç ve bir AngularJS ön uç, Azure Active Directory kullanıcı için kullanmayacağından makale kılavuzları hello kimlik doğrulaması. 

## <a id="authconfig"></a>Nasıl Azure App Service'te tooconfigure kullanıcı kimlik doğrulaması
Bu bölümde tooany API uygulaması geçerli olan genel yönergeleri sağlar. Adımları belirli toohello tooDo listesi .NET örnek uygulaması için çok Git[hello .NET kullanmaya Başlarken öğreticilerine devam etme](#tutorialstart).

1. Merhaba, [Azure portal](https://portal.azure.com/), toohello gidin **ayarları** tooprotect, Bul hello istediğiniz hello API uygulaması dikey **özellikleri** bölümünde ve ardından  **Kimlik doğrulama / yetkilendirme**.
   
    ![Azure portal kimlik doğrulama/yetkilendirme](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. Merhaba, **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **üzerinde**.
3. Hello hello seçeneklerden birini belirleyin **istek kimliği doğrulanmamış olduğunda eylem tootake** aşağı açılan liste.
   
   * API uygulamanız yalnızca kimliği doğrulanmış çağrıları tooreach istiyorsanız, hello birini tercih **ile oturum...**  seçenekleri. Bu seçenek, içinde çalışan herhangi bir kod yazmak zorunda kalmadan, tooprotect hello API uygulaması sağlar.
   * API uygulamanız tüm çağrılar tooreach istiyorsanız, tercih **isteğine izin ver (hiçbir işlem)**. Bu seçenek kimliği doğrulanmamış toodirect arayanlar tooa seçimine kimlik doğrulama sağlayıcılarını kullanabilirsiniz. Bu seçenek ile toowrite kod toohandle yetkiye sahip.
     
     Daha fazla bilgi için bkz. [Azure App Service’de API Apps için kimlik doğrulama ve yetkilendirme](app-service-api-authentication.md#multiple-protection-options).
4. Bir veya daha fazla hello seçin **kimlik doğrulama sağlayıcıları**.
   
    Merhaba görüntü Azure AD tarafından kimliği doğrulanmış tüm arayanlar toobe gerektiren seçimler gösterilmektedir.
   
    ![Azure portal kimlik doğrulama/yetkilendirme dikey penceresi](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    Bir kimlik doğrulama sağlayıcısı seçtiğinizde, hello portal bu sağlayıcı için bir yapılandırma dikey penceresinde görüntüler. 
   
    Nasıl tooconfigure hello kimlik doğrulama sağlayıcısı yapılandırma dikey açıklayan ayrıntılı yönergeler için bkz: [nasıl tooconfigure App Service uygulama toouse Azure Active Directory oturum açma](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). (Azure AD hakkındaki tooan makale hello bağlantı gider, ancak hello makalesi kendisini tooarticles hello için diğer kimlik doğrulama sağlayıcıları bağlantı sekme içerir.)
5. Merhaba kimlik doğrulama sağlayıcısı yapılandırma dikey bittiğinde, tıklatın **Tamam**.
6. Merhaba, **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **kaydetmek**.

Bu yapıldığında, uygulama hizmeti hello API uygulaması düşmeden önce tüm API çağrıları kimliğini doğrular. Merhaba kimlik doğrulama hizmetleri iş hello aynı .NET, Node.js ve Java dahil olmak üzere uygulama hizmetini destekleyen tüm diller için. 

API çağrıları toomake kimlik doğrulaması, hello çağıran hello kimlik doğrulama sağlayıcısının OAuth 2.0 taşıyıcı belirteci hello yetkilendirme üstbilgisinde HTTP isteklerini içerir. Merhaba belirteci hello kimlik doğrulama sağlayıcısının SDK kullanılarak edinilebilir.

## <a id="tutorialstart"></a>Merhaba .NET API uygulamaları öğreticilerine devam etme
API uygulamaları için hello Node.js ve Java öğreticileri izliyorsanız, toohello sonraki makalede atla [API uygulamaları için hizmet asıl kimlik doğrulaması](app-service-api-dotnet-service-principal-auth.md). 

API uygulamaları için .NET Öğreticisi serisi hello izleyen ve Merhaba örnek uygulaması hello yönergelerine uygun olarak zaten dağıttıysanız [ilk](app-service-api-dotnet-get-started.md) ve [ikinci](app-service-api-cors-consume-javascript.md) öğreticileri, Atla toohello [ayarlama Uygulama hizmeti ve Azure AD kimlik doğrulaması](#azureauth) bölümü.

Bu öğretici hello birinci ve ikinci öğreticileri geçmeden toofollow istiyorsanız, otomatik bir işlem toodeploy hello örnek uygulamanın kullanarak tooget nasıl başlatılacağını açıklayan adımları izleyerek hello.

> [!NOTE]
> Merhaba aşağıdaki adımlar, aynı başlangıç noktası tek bir istisna ilk iki öğreticileri hello gibi toohello alırsınız: Visual Studio olmaz zaten biliyor hangi web uygulaması veya her proje dağıtılan API uygulaması. Bu öğreticideki açıklayan tam yönergeler sahip olmaz anlamına nasıl toodeploy toohello sağ hedefler. Açık nasıl toodo hello dağıtım, kendi adımları memnun değilseniz, daha iyi toofollow hello öğretici serisinde hello olan [ilk öğreticide](app-service-api-dotnet-get-started.md) bu toostart'den otomatik dağıtım işlemi.
> 
> 

1. Hello listelenen hello Önkoşullar tümüne sahip olduğunuzdan emin olun [ilk öğreticide](app-service-api-dotnet-get-started.md). Toplama toohello Önkoşullar listelenen bu kimlik doğrulama öğreticiler App Service web apps ve Visual Studio API uygulamaları ile çalıştıktan ve Azure portal hello varsayalım.
2. Merhaba tıklatın **tooAzure dağıtmak** hello düğmesini [tooDo listesi örnek depo Benioku dosyası](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) toodeploy hello API apps ve hello web uygulaması. Web uygulaması ve API uygulaması adları daha sonra bu toolook kullanabileceğiniz gibi oluşturulan, hello Azure kaynak grubu not edin.
3. İndirme veya kopya hello [tooDo listesi örnek depo](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) , ile yerel olarak Visual Studio'da karşılaşmayacağınızı tooget hello kodu.

## <a id="azureauth"></a>Uygulama hizmeti ve Azure AD kimlik doğrulaması ayarlama
Artık kullanıcıların kimliğinin doğrulanmasını gerek kalmadan Azure App Service'te çalışan hello uygulama vardır. Bu bölümde kimlik doğrulama görevleri aşağıdaki hello yaparak ekleyin:

* Merhaba orta katman API uygulamasını çağırmak için uygulama hizmeti toorequire Azure Active Directory (Azure AD) kimlik doğrulamasını yapılandırın.
* Azure AD uygulaması oluşturun.
* Hello Azure AD uygulama toosend hello taşıyıcı belirteci oturum açma toohello AngularJS ön uç sonra yapılandırın. 

Aşağıdaki hello öğretici yönergeleri sırasında sorunları alıyorsanız hello bkz [sorun giderme](#troubleshooting) hello öğretici hello sonunda bölüm. 

### <a name="configure-authentication-for-hello-middle-tier-api-app"></a>Merhaba orta katman API uygulaması için kimlik doğrulamasını yapılandırma
1. Merhaba, [Azure portal](https://portal.azure.com/), toohello gidin **ayarları** oluşturduğunuz hello API uygulaması dikey penceresinde hello Todolistapı projesi için bulma hello **özellikleri** bölümünde ve ardından tıklatın **kimlik doğrulama / yetkilendirme**.
   
    ![Azure portal kimlik doğrulama/yetkilendirme](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. Merhaba, **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **üzerinde**.
3. Merhaba, **istek kimliği doğrulanmamış olduğunda eylem tootake** aşağı açılan listesinden, **Azure Active Directory ile oturum aç**.
   
    Bu seçenek, hiçbir unauathenticated istek hello API uygulaması ulaşabileceği sağlar. 
4. Altında **kimlik doğrulama sağlayıcıları**, tıklatın **Azure Active Directory**.
   
    ![Azure portal kimlik doğrulama/yetkilendirme dikey penceresi](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. Merhaba, **Azure Active Directory ayarları** dikey penceresinde tıklatın **Express**
   
    ![Azure portal kimlik doğrulama/yetkilendirme Express seçeneği](./media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    Merhaba ile **Express** seçeneği, uygulama hizmeti otomatik olarak oluşturabilir Azure AD uygulaması, Azure AD'de [Kiracı](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    Her Azure hesabı otomatik olarak bir tane var olduğundan, Kiracı toocreate yok.
6. Altında **yönetim modu**, tıklatın **yeni AD uygulaması oluştur** seçili değilse ve fark hello hello değer **uygulama oluşturma** metin kutusu; bu AAD göreceğiz Merhaba Klasik Azure portalı daha sonra uygulama.
   
    ![Azure portalında Azure AD ayarları](./media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    Azure, Azure AD kiracınızda hello Belirtilen adda bir Azure AD uygulaması otomatik olarak oluşturur. Varsayılan olarak, Azure AD uygulaması hello adlı aynı hello API uygulaması gibi hello. İsterseniz, farklı bir ad girebilirsiniz.
7. **Tamam** düğmesine tıklayın.
8. Merhaba, **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **kaydetmek**.
   
    ![Kaydet’e tıklayın.](./media/app-service-api-dotnet-user-principal-auth/authsave.png)

Artık yalnızca Azure AD kiracınızdaki kullanıcıların hello API uygulaması çağırabilirsiniz.

### <a name="optional-test-hello-api-app"></a>İsteğe bağlı: hello API uygulamayı test etme
1. Toohello hello API uygulaması URL'sini bir tarayıcıda gidin: hello içinde **API uygulaması** dikey penceresinde hello Azure portal altında hello bağlantısını tıklatın **URL**.  
   
    Kimliği doğrulanmamış istekler tooreach hello API uygulaması izin verilmediğinden, yeniden yönlendirilen tooa oturum açma ekranı demektir.
   
    Tarayıcınız toohello "başarıyla oluşturuldu" sayfası kalırsa, hello tarayıcı zaten oturum açmış olabilirsiniz--bu durumda, bir InPrivate veya Incognito penceresi açın ve toohello API uygulamanızın URL'sine gidin.
2. Azure AD kiracınızda bir kullanıcı için kimlik bilgilerini kullanarak oturum açın.
   
    Oturum açarken hello tarayıcıda hello "başarıyla oluşturuldu" sayfası görüntülenir.
3. Kapat hello tarayıcı.

### <a name="configure-hello-azure-ad-application"></a>Merhaba Azure AD uygulaması yapılandırma
Azure AD kimlik doğrulaması için yapılandırıldığında, uygulama hizmeti bir Azure AD uygulaması oluşturuldu. Varsayılan olarak yapılandırılmış tooprovide hello taşıyıcı belirteci toohello API uygulamasının URL'si Merhaba yeni Azure AD uygulaması oluştu. Bu bölümde hello Azure AD uygulama tooprovide hello taşıyıcı belirteci toohello AngularJS ön uç yerine doğrudan toohello orta katman API uygulamasını yapılandırın. Merhaba AngularJS ön uç hello API uygulamasını çağıran hello belirteci toohello API uygulaması gönderir.

> [!NOTE]
> tookeep hello işlemi kadar basit, Bu öğretici, tek bir Azure AD kullanır hello ön uç ve hello orta katman API uygulaması için uygulama. Toouse iki Azure AD uygulama başka bir seçenektir. Bu durumda toogive hello ön uç ait Azure AD uygulama izni toocall hello Orta katmanın Azure AD uygulaması gerekir. Birden çok uygulama bu yaklaşım izinleri tooeach katmanı üzerinde daha ayrıntılı denetim verirsiniz.
> 
> 

1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com/), çok Git**Azure Active Directory**.
   
   Gereksinim duyduğunuz belirli Azure Active Directory ayarları tooare hello mevcut Azure portalından henüz kullanılamıyor eriştiğinden toouse hello Klasik portal sahip.
2. Merhaba üzerinde **Directory** sekmesinde, AAD kiracınızın tıklayın.
   
   ![Azure AD Klasik portalında](./media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. Tıklatın **uygulamaları > Şirketimin sahip olduğu uygulamalar**ve ardından hello onay işaretine tıklayın.
   
   Toorefresh hello sayfa toosee hello yeni uygulama da olabilir.
4. Uygulamaları Hello listesinde hello API uygulamanız için kimlik doğrulaması etkinleştirildiğinde Azure sizin için oluşturulmuş bir hello adına tıklayın.
   
   ![Azure AD uygulamalar sekmesi](./media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. **Yapılandır**'a tıklayın.
   
   ![Azure AD Yapılandır sekmesi](./media/app-service-api-dotnet-user-principal-auth/configure.png)
6. Ayarlama **oturum açma URL'si** AngularJS web uygulamanız, hiçbir eğik toohello URL.
   
   Örneğin: https://todolistangular.azurewebsites.net
   
   ![Oturum açma URL'si](./media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. Ayarlama **yanıt URL'si** web uygulamanıza hiçbir eğik toohello URL'si.
   
   Örneğin: https://todolistsangular.azurewebsites.net
8. **Kaydet** düğmesine tıklayın.
   
   ![Yanıt URL'si](./media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. Merhaba sayfasının Hello altında tıklatın **Yönet bildirimi > indirme bildirimi**.
   
   ![Bildirim indirin](./media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. Merhaba dosya tooa konumu, düzenleyebileceğiniz indirin.
11. Merhaba indirilen hello bildirim dosyasında arama `oauth2AllowImplicitFlow` özelliği. Bu özellikten hello değerini değiştirin `false` çok`true`ve hello dosyasını kaydedin.
    
    Bu ayar, bir JavaScript tek sayfalı uygulama erişimi için gereklidir. Merhaba Oauth 2.0 taşıyıcı belirteci toobe hello URL parçadaki döndürülen sağlar.
12. Tıklatın **Yönet bildirimi > karşıya yükleme bildirimi**ve adım önceki hello güncelleştirilmiş hello dosya karşıya yükleme.
    
    ![Bildirim karşıya yükle](./media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. Kopya hello **istemci kimliği** değer ve bir yere alabilirsiniz ondan daha sonra kaydedin.

## <a name="configure-hello-todolistangular-project-toouse-authentication"></a>Merhaba ToDoListAngular projesi toouse kimlik doğrulamasını yapılandırma
Bu bölümde JS tooacquire Azure AD'den hello oturum açan kullanıcı için bir taşıyıcı belirteç için Active Directory Authentication Library (ADAL) kullanan şekilde hello AngularJS ön uç değiştirin. Merhaba kod hello belirteci toohello orta katman, gönderilen HTTP isteklerinde hello Aşağıdaki diyagramda gösterildiği gibi içerir. 

![Kullanıcı kimlik doğrulama diyagramı](./media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

Değişiklikleri toofiles hello ToDoListAngular projesinde aşağıdaki hello olun.

1. Açık hello *Index.cshtml* dosya.
2. JS komut dosyaları için Active Directory Authentication Library (ADAL) hello başvuru hello satırlardaki yorumları kaldırın.
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. Açık hello *app/scripts/app.js* dosya.
4. Açıklama kod bloğunu hello çıkışı için "olmadan kimlik doğrulaması" olarak işaretlenmiş ve kod bloğunu hello "ile kimlik doğrulaması için" olarak işaretlenmiş açıklamadan çıkarın.
   
    Bu değişiklik hello ADAL JS kimlik doğrulama sağlayıcısı başvuruyor ve yapılandırma değerleri tooit sağlar. Aşağıdaki adımları hello Azure AD uygulaması ve API uygulaması için hello yapılandırma değerlerini ayarlayın.
5. Merhaba ayarlar hello kodda `endpoints` değişken, ayarlanmış hello API URL toohello hello Todolistapı projesi için oluşturduğunuz ve ayarlama hello API uygulaması URL'sini hello hello Klasik Azure Portalı ' kopyaladığınız Azure AD uygulama kimliği toohello istemci kimliği.
   
    Merhaba kod aşağıdaki örneğine benzer toohello sunulmuştur.
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. Hello çağrı çok`adalProvider.init`ayarlayın `tenant` tooyour Kiracı adı ve `clientId` hello önceki adımda kullanılan toosame değer.
   
    Merhaba kod aşağıdaki örneğine benzer toohello sunulmuştur.
   
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
   
    Bu değişiklikler çok`app.js` hello çağıran kodu ve API adlı hello hello aynı Azure AD uygulama olduğunu belirtin.
7. Açık hello *app/scripts/homeCtrl.js* dosya.
8. Açıklama kod bloğunu hello çıkışı için "olmadan kimlik doğrulaması" olarak işaretlenmiş ve kod bloğunu hello "ile kimlik doğrulaması için" olarak işaretlenmiş açıklamadan çıkarın.
9. Açık hello *app/scripts/indexCtrl.js* dosya.
10. Açıklama kod bloğunu hello çıkışı için "olmadan kimlik doğrulaması" olarak işaretlenmiş ve kod bloğunu hello "ile kimlik doğrulaması için" olarak işaretlenmiş açıklamadan çıkarın.

### <a name="deploy-hello-todolistangular-project-tooazure"></a>Merhaba ToDoListAngular projesi tooAzure dağıtma
1. İçinde **Çözüm Gezgini**hello ToDoListAngular projesine sağ tıklayın ve ardından **Yayımla**.
2. **Yayımla**’ta tıklayın.
   
    Visual Studio Başlangıç projesini dağıtır ve bir tarayıcı toohello web uygulamanızın temel URL'yi açar. Bu bir tarayıcıdan girişimi toogo tooa Web API'sini temel URL için normal bir 403 hata sayfası gösterilir.
   
    Merhaba uygulaması test edebilmemiz toomake bir değişiklik toohello orta katman API uygulaması hala sahip olursunuz.
3. Kapat hello tarayıcı.

## <a name="configure-hello-todolistapi-project-toouse-authentication"></a>Merhaba Todolistapı projesi toouse kimlik doğrulamasını yapılandırma
Şu anda Todolistapı projesi gönderir hello "*" Merhaba olarak `owner` değeri tooToDoListDataAPI. Bu bölümde hello kod toosend hello hello oturum açmış kullanıcının Kimliğini değiştirin.

Aşağıdaki değişiklikler hello Todolistapı projesinde hello olun.

1. Açık hello *Controllers/ToDoListController.cs* dosya ve ayarlar her eylem yöntemindeki hello satırı açıklamadan kaldırmasına `owner` toohello Azure AD `NameIdentifier` talep değeri. Örneğin:
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    **Önemli**: hello kodda açıklamadan çıkarın yok `ToDoListDataAPI` yöntemi; bu daha sonra hello hizmet asıl kimlik doğrulaması öğretici için gerçekleştirirsiniz.

### <a name="deploy-hello-todolistapi-project-tooazure"></a>Merhaba Todolistapı projesi tooAzure dağıtma
1. İçinde **Çözüm Gezgini**hello Todolistapı projesine sağ tıklayın ve ardından **Yayımla**.
2. **Yayımla**’ta tıklayın.
   
    Visual Studio Başlangıç projesini dağıtır ve bir tarayıcı toohello API uygulamasının temel URL'yi açar.
3. Kapat hello tarayıcı.

### <a name="test-hello-application"></a>Merhaba uygulamayı test etme
1. Merhaba web uygulamasının toohello URL'sini Git **HTTPS değil HTTP kullanarak**.
2. Merhaba tıklatın **tooDo listesi** sekmesi.
   
    İçinde istendiğinde toolog var.
3. Bir kullanıcının AAD kiracınızda hello kimlik bilgilerinizle oturum açın.
4. Merhaba **tooDo listesi** sayfası görüntülenir.
   
   ![tooDo Listesi Sayfası](./media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   Şimdiye kadar bunların tümünü sahibi bırakıldığından Yapılacaklar öğelerini görüntülenen "*". Merhaba orta katman öğeleri hello oturum açan kullanıcı için şimdi isteme ve hiçbiri henüz oluşturulmadı.
5. Merhaba uygulaması çalışma yeni yapılacak iş öğeleri tooverify ekleyin.
6. Başka bir tarayıcı penceresinde hello Todolistdataapı API uygulaması için Swagger kullanıcı Arabirimi URL toohello gidin ve tıklayın **ToDoList > almak**. Hello için bir yıldız işareti girin `owner` parametre ve ardından **deneyin**.
   
   Merhaba yanıt hello yeni yapılacak iş öğeleri hello sahibi özelliğindeki hello gerçek Azure AD kullanıcı kimliği olduğunu gösterir.
   
   ![JSON yanıt sahibinin kimliği](./media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-hello-projects-from-scratch"></a>Sıfırdan Hello projeler derleme
Merhaba iki Web API projeleri hello kullanarak oluşturulmuş **Azure API uygulaması** proje şablonu ve bir Yapılacaklar listesi denetleyicisiyle değiştirerek hello varsayılan değerleri denetleyicisi. 

Bir Web API 2 arka uç ile bir AngularJS tek sayfalı uygulama hakkında bilgi çok oluşturmak için bkz: [ellere üzerindeki Laboratuvar: tek sayfa uygulama (SPA) ASP.NET Web API ve Angular.js yapı](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Hakkında bilgi için tooadd Azure AD kimlik doğrulama kodu, kaynakları aşağıdaki hello bakın:

* [AngularJS tek güvenli hale getirme sayfasında Azure AD ile uygulamaları](../active-directory/active-directory-devquickstarts-angular.md).
* [ADAL JS v1 Tanıtımı](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a>Sorun giderme
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Todolistapı (orta katman) ve Todolistdataapı (veri katmanı) karıştırmayın emin olun. Örneğin, kimlik doğrulama toohello orta katman API uygulaması, hello veri katmanı eklediğinizi doğrulayın. 
* Merhaba AngularJS kaynak kodu başvuruları hello orta katman API uygulaması URL'sini (Todolistapı, Todolistdataapı değil) ve hello Azure AD istemci kimliği doğru olduğuna emin olun 

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide nasıl toouse bir API uygulaması için uygulama hizmeti kimlik doğrulama ve nasıl toocall hello API uygulaması kullanarak ADAL JS kitaplığı hello öğrendiniz. Merhaba sonraki öğreticide şunları nasıl çok öğreneceksiniz[hizmet senaryoları için güvenli erişim tooyour API uygulaması](app-service-api-dotnet-service-principal-auth.md).

