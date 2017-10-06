---
title: "aaaCORS desteği App Service'te | Microsoft Docs"
description: "Nasıl toouse CORS desteği Azure Azure App Service'te öğrenin."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 4f980a97-b9f5-4d1d-87ab-82b60bb96e1c
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/27/2016
ms.author: alkarche
ms.openlocfilehash: c229378b75840bc0f7b2eefc3df3031233f9b494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a>CORS kullanarak JavaScript’ten bir API uygulaması kullanma
Uygulama hizmeti için yerleşik destek sunar [arası kaynak kaynak paylaşımı (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), JavaScript istemcilerinin toomake etki alanları arası sağlayan API uygulamalarında barındırılan tooAPIs çağırır. App Service CORS erişim tooyour API API'nizi hiçbir kod yazmadan yapılandırmanıza olanak sağlar.

Bu makale iki bölüm içerir:

* Merhaba [nasıl tooconfigure CORS](#corsconfig) bölümde açıklanmıştır genel nasıl tooconfigure CORS herhangi bir API uygulaması, web uygulaması veya mobil uygulama. Ayrıca .NET, Node.js ve Java dahil App Service tarafından desteklenen tooall çerçeveleri eşit oranda geçerlidir. 
* Merhaba ile başlayan [hello .NET kullanmaya Başlarken öğreticilerine devam etme](#tutorialstart) bölümünde hello makaledir CORS desteği yaptıklarınızın üzerine ekleme yaparak gösteren bir eğitim [hello ilk API Apps başlangıç öğreticisinde ](app-service-api-dotnet-get-started.md). 

## <a id="corsconfig"></a>Nasıl tooconfigure Azure App Service'de CORS
Hello Azure portal veya kullanarak CORS'yi yapılandırın [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) araçları.

#### <a name="configure-cors-in-hello-azure-portal"></a>Hello Azure portal CORS'yi yapılandırın
1. Bir tarayıcıda toohello Git [Azure portal](https://portal.azure.com/).
2. Tıklatın **uygulama hizmetleri**ve ardından API uygulamanızın hello adına tıklayın.
   
    ![Portalda API uygulamasını seçin](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. Merhaba, **ayarları** hello toohello sağındaki açılan dikey **API uygulaması** dikey penceresinde, Bul hello **API** bölümünde ve ardından **CORS**.
   
   ![Ayarlar dikey penceresinden CORS’yi seçin](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. Merhaba metin kutusuna hello URL veya tooallow JavaScript çağrılarını toocome gelen istediğiniz URL'leri girin.

    Örneğin, todolistangular adlı, JavaScript uygulama tooa web uygulamasına dağıttıysanız, "https://todolistangular.azurewebsites.net" girin. Alternatif olarak, tüm kaynak etki alanlarının kabul edildiğini bir yıldız işareti (*) toospecify girebilirsiniz.


1. **Kaydet** düğmesine tıklayın.
   
   ![Kaydet’e tıklayın.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   Tıklattıktan sonra **kaydetmek**, hello API uygulaması JavaScript kabul hello gelen çağrıları belirtilen URL.

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a>Azure Resource Manager araçlarını kullanarak CORS’yi yapılandırın
Kullanarak bir API uygulaması için CORS yapılandırabilirsiniz [Azure Resource Manager şablonları](../azure-resource-manager/resource-group-authoring-templates.md) gibi komut satırı araçlarında [Azure PowerShell](/powershell/azureps-cmdlets-docs) ve hello [Azure CLI](../cli-install-nodejs.md). 

Merhaba hello CORS özelliğini ayarlayan bir Azure Resource Manager şablonu örneği için açık [Bu öğreticinin örnek uygulamasının için hello deposundaki azuredeploy.json dosyasını](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json). Merhaba aşağıdaki örneğine hello gibi görünüyor hello şablon bölümünü bulun:

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <a id="tutorialstart"></a>Merhaba .NET kullanmaya Başlarken Öğreticisine devam etme
Merhaba Node.js ve Java kullanmaya başlama serisini API uygulamaları için takip ediyorsanız, kullanmaya başlama serisini alma tamamlanmış hello sahip. Toohello atla [sonraki adımlar](#next-steps) bölümünde API uygulamaları hakkında daha fazla öğrenme toofind yönelik öneriler.

Merhaba bu makalenin sonraki bölümlerinde hello .NET kullanmaya Başlarken serisinin devamıdır ve başarıyla tamamlandığını varsayar [hello ilk öğreticide](app-service-api-dotnet-get-started.md).

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a>Merhaba ToDoListAngular projesi tooa yeni web uygulaması dağıtma
İçinde [hello ilk öğreticide](app-service-api-dotnet-get-started.md), orta katman API uygulamasını ve veri katmanı API uygulaması oluşturdunuz. Bu öğreticide, çağrıları hello orta katman API uygulamasını bir tek sayfalı uygulama (SPA) web uygulaması oluşturun. Merhaba SPA toowork tooenable CORS hello orta katman API uygulaması sahip. 

Merhaba, [ToDoList örnek uygulamasında](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), hello ToDoListAngular projedir hello orta katman Todolistapı Web API projesini çağıran basit bir AngularJS istemci. JavaScript kodu hello hello *app/scripts/todoListSvc.js* dosya hello AngularJS HTTP sağlayıcısını kullanarak hello API çağırır. 

        angular.module('todoApp')
        .factory('todoListSvc', ['$http', function ($http) {

            $http.defaults.useXDomain = true;
            delete $http.defaults.headers.common['X-Requested-With']; 

            return {
                getItems : function(){
                    return $http.get(apiEndpoint + '/api/TodoList');
                },

                /* Get by ID, Put, and Delete methods not shown */

                postItem : function(item){
                    return $http.post(apiEndpoint + '/api/TodoList', item);
                }
            };
        }]);

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a>Merhaba ToDoListAngular projesi için yeni bir web uygulaması oluşturma
Merhaba yordamı toocreate yeni bir App Service web uygulaması ve proje dağıtma tooit olduğu için gördüğünüz benzer toowhat [oluşturma ve hello bu serideki ilk öğreticide bir API uygulamasına dağıtma](app-service-api-dotnet-get-started.md#createapiapp). Bu hello uygulama türü farktır yalnızca Hello: **Web uygulaması** yerine **API uygulaması**.  Merhaba iletişim kutularının ekran görüntüleri için bkz: 

1. İçinde **Çözüm Gezgini**hello ToDoListAngular projesine sağ tıklayın ve ardından **Yayımla**.
2. Merhaba, **profil** hello sekmesinde **Web'i Yayımla** Sihirbazı'nı tıklatın **Microsoft Azure App Service**.
3. Merhaba, **uygulama hizmeti** iletişim kutusu, tıklatın **yeni**.
4. Merhaba, **barındırma** hello sekmesinde **App Service Oluştur** iletişim kutusuna bir **Web uygulaması adı** hello benzersiz *azurewebsites.net* etki alanı. 
5. Hello Azure'ı seçin **abonelik** ile toowork istiyor.
6. Merhaba, **kaynak grubu** aşağı açılan listesinde, hello seçin daha önce oluşturduğunuz aynı kaynak grubu.
7. Merhaba, **uygulama hizmeti planı** aşağı açılan listesinde, hello seçin önceden oluşturduğunuz planı. 
8. **Oluştur**'a tıklayın.
   
    Visual Studio hello web uygulamasını oluşturur, bunun için bir yayımlama profili oluşturur ve görüntüler hello **bağlantı** hello adımında **Web'i Yayımla** Sihirbazı.
   
    Henüz **Yayımla**’ya tıklamayın. Bölümden hello, App Service'te çalışan hello yeni web uygulaması toocall hello orta katman API uygulamasını yapılandırın. 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a>Web uygulaması ayarları içinde Hello orta katman URL'yi ayarlayın
1. Toohello Git [Azure portal](https://portal.azure.com/)ve ardından toohello gidin **Web uygulaması** toohost hello TodoListAngular (ön uç) projesini oluşturulan hello web uygulaması dikey penceresinde.
2. **Ayarlar > Uygulama Ayarları**’na tıklayın.
3. Merhaba, **uygulama ayarları** bölümünde, hello aşağıdakileri ekleyin anahtar ve değer:
   
   | Anahtar | Değer | Örnek |
   | --- | --- | --- |
   | toDoListAPIURL |https://{orta katman API uygulamanızın adı}.azurewebsites.net |https://todolistapi0121.azurewebsites.net |
4. **Kaydet** düğmesine tıklayın.
   
    Merhaba kod Azure içinde çalıştığında, bu değer hello olduğu hello localhost URL'sini geçersiz kılar *Web.config* dosya. 
   
    Merhaba ayar değerini hello kodu içinde *Index.cshtml*:
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    Merhaba kodda *todoListSvc.js* hello ayarı kullanır:
   
        return {
            getItems : function(){
                return $http.get(apiEndpoint + '/api/TodoList');
            },
            getItem : function(id){
                return $http.get(apiEndpoint + '/api/TodoList/' + id);
            },
            postItem : function(item){
                return $http.post(apiEndpoint + '/api/TodoList', item);
            },
            putItem : function(item){
                return $http.put(apiEndpoint + '/api/TodoList/', item);
            },
            deleteItem : function(id){
                return $http({
                    method: 'DELETE',
                    url: apiEndpoint + '/api/TodoList/' + id
                });
            }
        };

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a>Merhaba ToDoListAngular web projesi toohello yeni web uygulaması dağıtma
* Visual Studio'da, hello **bağlantı** hello adımında **Web'i Yayımla** Sihirbazı'nı tıklatın **Yayımla**.
  
   Visual Studio hello ToDoListAngular projesi toohello yeni web uygulamasına dağıtır ve hello web uygulamasının bir tarayıcı toohello URL'sini açar. 

### <a name="test-hello-application-without-cors-enabled"></a>CORS'yi etkinleştirmeden Hello uygulamayı test etme
1. Tarayıcınızda geliştirici araçları hello konsol penceresi açın.
2. Merhaba AngularJS kullanıcı arabirimini görüntüleyen hello tarayıcı penceresinde hello tıklatın **tooDo listesi** bağlantı.
   
    Merhaba JavaScript kodu toocall hello orta katman API uygulaması çalışır ancak hello ön uç geri hello farklı bir etki alanında son çalıştığından hello çağrı başarısız olur. Merhaba tarayıcının geliştirici araçları konsol penceresi bir çıkış noktaları arası hata iletisi gösterir.
   
    ![Çıkış noktaları arası hata iletisi](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a>Merhaba orta katman API uygulaması CORS'yi yapılandırın
Bu bölümde, hello orta katman Todolistapı API uygulaması azure'da hello CORS ayarını yapılandırın. Bu ayar hello orta katman API uygulaması tooreceive JavaScript çağrılarını hello ToDoListAngular projesi için oluşturduğunuz web uygulamasından hello izin verir.

1. Bir tarayıcıda toohello Git [Azure portal](https://portal.azure.com/).
2. Tıklatın **uygulama hizmetleri**ve ardından Todolistapı (orta katman) API hello uygulama tıklayın.
   
    ![Portalda API uygulamasını seçin](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. Merhaba, **ayarları** hello toohello sağındaki açılan dikey **API uygulaması** dikey penceresinde, Bul hello **API** bölümünde ve ardından **CORS**.
   
   ![Portalda CORS’yi seçme](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. Merhaba metin kutusuna hello ToDoListAngular (ön uç) web uygulaması için hello URL'sini girin. Örneğin, todolistangular0121 adlı hello ToDoListAngular projesi tooa web uygulamasına dağıttıysanız, hello URL'den çağrılarına izin vermek `https://todolistangular0121.azurewebsites.net`.
   
   Alternatif olarak, tüm kaynak etki alanlarının kabul edildiğini bir yıldız işareti (*) toospecify girebilirsiniz.
5. **Kaydet** düğmesine tıklayın.
   
   ![Kaydet’e tıklayın.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   Tıklattıktan sonra **kaydetmek**, hello API uygulaması JavaScript kabul hello gelen çağrıları belirtilen URL. Bu ekran görüntüsünde hello Todolistapı0223 API uygulaması hello ToDoListAngular web uygulamasından JavaScript istemci çağrılarını kabul eder.

### <a name="test-hello-application-with-cors-enabled"></a>CORS'yi Hello uygulamayı test etme
* Bir tarayıcı toohello hello web uygulamasının HTTPS URL'sini açın. 
  
    Bu zaman hello uygulaması, görüntülemek, ekleme, düzenleme ve yapılacaklar öğelerini silme sağlar. 
  
    ![örnek uygulaması tooDo liste sayfası](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a>App Service CORS ile Web API CORS karşılaştırması
Bir Web API projesinde hello yükleyebilirsiniz [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet paketi toospecify kodu JavaScript API'nizi kabul edeceği hangi etki alanlarının çağırır.

Web API CORS desteği App Service CORS desteğinden daha esnektir. Örneğin, kodda farklı eylem yöntemleri için farklı kabul edilen çıkış noktaları belirtebilirken, App Service CORS’de bir API uygulamasının tüm yöntemleri için bir kabul edilen çıkış noktası kümesi belirtirsiniz.

> [!NOTE]
> Toouse denemeyin Web API CORS ve App Service CORS bir API uygulamasında. App Service CORS öncelik kazanır ve Web API CORS’nin hiçbir etkisi olmaz. Örneğin, App Service'te bir kaynak etki alanı etkinleştirirseniz ve Web API kodunuzdaki tüm çıkış noktası etki alanlarını etkinleştirmek, Azure API uygulamanız yalnızca Azure içinde belirtilen hello etki alanından çağrılarını kabul eder.
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a>Nasıl Web API kodunda CORS'yi tooenable
Aşağıdaki adımları hello Web API CORS desteğini etkinleştirme hello işlemi özetlenir. Daha fazla bilgi için bkz. [ASP.NET Web API 2’de Çıkış Noktaları Arası İstekleri Etkinleştirme](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).

1. Bir Web API projesinde hello yüklemek [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet paketi.
2. Dahil bir `config.EnableCors()` hello kod satırı **kaydetmek** hello yöntemi **WebApiConfig** aşağıdaki örneğine hello olduğu gibi sınıfı. 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // hello following line enables you toocontrol CORS by using Web API code
                config.EnableCors();
   
                // Web API routes
                config.MapHttpAttributeRoutes();
   
                config.Routes.MapHttpRoute(
                    name: "DefaultApi",
                    routeTemplate: "api/{controller}/{id}",
                    defaults: new { id = RouteParameter.Optional }
                );
            }
        }
3. Web API denetleyicinizde eklemek bir `using` hello bildirimi `System.Web.Http.Cors` ad alanı ve hello ekleyin `EnableCors` özniteliği toohello denetleyici sınıfı veya tooindividual eylem yöntemleri. Aşağıdaki örneğine hello CORS desteğini toohello tüm denetleyiciye uygulanır.
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a>API Apps ile Azure API Management kullanma
Bir API uygulamasıyla Azure API Management kullanıyorsanız, CORS'yi API Management yerine hello API uygulamasında yapılandırın. Daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [Azure API Management’a Genel Bakış (video: CORS 12:10’da başlar)](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [API Management etki alanları arası ilkeler](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a>Sorun giderme
Bu öğreticiyi izlerken bir sorunla karşılaşırsanız, bazı sorun giderme fikirlerini burada bulabilirsiniz.

* Merhaba hello en son sürümünü kullandığınızdan emin olun [Visual Studio 2015 için .NET için Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003).
* Girdiğinizden emin olun `https` hello CORS ayarını ve kullandığınızdan emin olun `https` toorun hello ön uç web uygulaması.
* Hello CORS ayarını girdiğiniz hello orta katman API uygulaması, hello ön uç web uygulamasında değil olduğundan emin olun.
* CORS'yi hem uygulama kodunda hem de Azure App Service içinde yapılandırıyorsanız hello App Service CORS ayarının uygulama kodunda yaptığınız ne olursa olsun kılar unutmayın. 

Daha fazla sorun gidermeyi basitleştiren Visual Studio özellikleri hakkında toolearn bkz [Visual Studio'daki sorun giderme Azure uygulama hizmetinde uygulamaları](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, nasıl tooenable App Service CORS desteği böylece istemci JavaScript kodunun farklı bir etki alanında bir API çağrısı gördünüz. toolearn hello okuma API uygulamaları hakkında daha fazla [App Service'te giriş tooauthentication](../app-service/app-service-authentication-overview.md), ve toohello Git [API uygulamaları için kullanıcı kimlik doğrulaması](app-service-api-dotnet-user-principal-auth.md) Öğreticisi.

