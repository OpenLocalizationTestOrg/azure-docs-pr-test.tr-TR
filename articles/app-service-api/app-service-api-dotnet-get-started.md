---
title: "API uygulamaları ve App Service'te ASP.NET ile çalışmaya aaaGet | Microsoft Docs"
description: "Nasıl toocreate, dağıtmayı ve Azure App Service'te bir ASP.NET API uygulamasını Visual Studio 2015 kullanarak kullanmayı öğrenin."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: ddc028b2-cde0-4567-a6ee-32cb264a830a
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: alkarche
ms.openlocfilehash: d3e90f1585907d183b0435c6cafc5585bc1e29ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a>Azure App Service’de API Apps, ASP.NET ve Swagger kullanmaya başlama
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

Merhaba ilk bir dizi budur nasıl toouse özelliklerini Azure uygulama hizmetine Göster öğreticileri geliştirmek ve RESTful API'lerini barındırmak için yararlıdır.  Bu öğretici, Swagger biçiminde API meta veri desteğini ele alınmaktadır.

Şunları öğreneceksiniz:

* Nasıl toocreate dağıtıp [API uygulamaları](app-service-api-apps-why-best-platform.md) Visual Studio 2015 yerleşik araçlarını kullanarak Azure App Service'te.
* Hello kullanarak tooautomate API bulma Swashbuckle NuGet paketini nasıl toodynamically Swagger API'si meta verilerini oluşturur.
* Nasıl toouse Swagger API'si meta verileri tooautomatically bir API uygulaması için istemci kodu oluşturur.

## <a name="sample-application-overview"></a>Örnek uygulamaya genel bakış
Bu öğreticide, bir basit bir yapılacaklar listesi örnek uygulaması ile çalışırsınız. Merhaba uygulaması tek sayfalı uygulama (SPA) ön uç, ASP.NET Web API'si Orta katmanına ve ASP.NET Web API'si veri katmanına sahip.

![API Apps örnek uygulama diyagramı](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

Merhaba ekran görüntüsü işte [AngularJS](https://angularjs.org/) ön uç.

![API Apps örnek uygulama toodo listesi](./media/app-service-api-dotnet-get-started/todospa.png)

Merhaba Visual Studio çözümü üç projeyi içerir:

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* **ToDoListAngular** -hello ön uç: hello Orta katmanı çağıran bir AngularJS SPA.
* **Todolistapı** -hello orta katman: yapılacak işler öğelerinde CRUD işlemleri tooperform hello veri katmanını çağıran bir ASP.NET Web API projesi.
* **Todolistdataapı** -hello veri katman: yapılacak işler öğelerinde CRUD işlemleri gerçekleştiren bir ASP.NET Web API projesi.

Merhaba üç katmanlı yapı, API Apps kullanarak uygulayabileceğiniz ve burada yalnızca gösterim amacıyla kullanılan birçok mimarisi biridir. Her katmandaki Hello kod olası toodemonstrate API Apps özelliklerini kadar basit hale getirir; Örneğin, hello veri katmanı Kalıcılık mekanizması olarak veritabanı yerine sunucu belleği kullanır.

Bu öğreticiyi tamamladığınızda, hello iki Web API projelerini ve App Service API uygulamalarında hello bulutta çalışan sahip olacaksınız.

Merhaba serideki sonraki öğretici Hello hello SPA ön uç toohello bulut dağıtır.

## <a name="prerequisites"></a>Ön koşullar
* ASP.NET Web API - öğretici yönergeleri hello varsayın nasıl temel bilgiye sahip ASP.NET ile toowork [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) Visual Studio.
* Azure hesabı - [Ücretsiz bir Azure hesabı açabilir](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) veya [Visual Studio abonelik avantajlarını etkinleştirebilirsiniz](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
  
    Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/). Burada, Uygulama Hizmetleri’nde hemen bir kısa süreli başlangıç uygulaması oluşturabilirsiniz; **kredi kartı gerekmez** ve hiçbir taahhüt yoktur.
* Visual Studio 2015'hello ile [.NET için Azure SDK](https://azure.microsoft.com/downloads/archive-net-downloads/) -, zaten yoksa hello SDK Visual Studio 2015 otomatik olarak yükler..
  
  * Visual Studio’da Yardım -> Microsoft Visual Studio Hakkında’ya tıklayın ve "Azure App Service Tools v2.9.1" veya sonraki bir sürümün yüklü olduğundan emin olun.
    
    ![Azure App Tools sürümü](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > Merhaba SDK bağımlılıkları kaç makinenizde zaten bağlı olarak, yükleme hello SDK tooa yarım saat veya daha fazla birkaç dakikadan uzun bir zaman ele geçirebilir.
    > 
    > 

## <a name="download-hello-sample-application"></a>Merhaba örnek uygulamayı indirin
1. Merhaba karşıdan [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) deposu.
   
    Merhaba tıklayabilirsiniz **ZIP'i indir** yerel makinenizde düğmesini veya kopya hello deposu.
2. Visual Studio 2015 veya 2013 Hello ToDoList çözümünü açın.
   
   1. Her çözüm tootrust gerekir.
         ![Güvenlik Uyarısı](./media/app-service-api-dotnet-get-started/securitywarning.png)
3. Merhaba çözüm (CTRL + SHIFT + B) toorestore hello NuGet paketleri oluşturun.
   
    Dağıtmadan önce toosee hello uygulama işleminde isterseniz, yerel olarak çalıştırabilirsiniz. Todolistdataapı başlangıç projesi ve çalışma hello çözümü olduğundan emin olun. Tarayıcınızda toosee HTTP 403 hata beklemelisiniz.

## <a name="use-swagger-api-metadata-and-ui"></a>Swagger API meta verileri ve kullanıcı arabirimi kullanma
[Swagger](http://swagger.io/) 2.0 API meta verileri desteği Azure App Service’de yerleşiktir. Her API uygulama meta verileri hello API için Swagger JSON biçiminde döndüren bir URL uç noktası belirtebilir. Merhaba Bu uç noktadan döndürülen meta veri olabilir toogenerate istemci kodu kullanılır.

Bir ASP.NET Web API projesi dinamik olarak Swagger meta verileri hello kullanarak oluşturabilirsiniz [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet paketi. Merhaba Swashbuckle NuGet paketi indirdiğiniz hello Todolistdataapı ve Todolistapı projelerinde zaten yüklüdür.

Merhaba öğreticinin bu bölümünde, oluşturulan hello Swagger 2.0 meta verileri oluşturmayı inceler ve ardından hello Swagger meta verileri temel alan UI test çıkışı deneyin.

1. Merhaba Todolistdataapı projesini ayarlayın (**değil** hello Todolistapı projesi) hello başlangıç projesi olarak.
   
    ![ToDoDataAPI ayarını Başlangıç Projesi olarak belirleyin](./media/app-service-api-dotnet-get-started/startupproject.png)
2. F5 tuşuna basın veya tıklatın **hata ayıklama > hata ayıklamayı Başlat** toorun Merhaba projeyi hata ayıklama modunda.
   
    Merhaba tarayıcı açar ve hello HTTP 403 hata sayfası görüntülenir.
3. Tarayıcınızın adres çubuğuna, ekleme `swagger/docs/v1` toohello sonuna hello satır ve Return tuşuna basın. (URL hello `http://localhost:45914/swagger/docs/v1`.)
   
    Bu API hello için Swashbuckle tooreturn Swagger 2.0 JSON meta verileri tarafından kullanılan hello varsayılan URL'dir.
   
    Merhaba tarayıcı Internet Explorer kullanıyorsanız, toodownload ister bir *v1.json* dosya.
   
    ![IE’de JSON meta veriler indirme](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    Chrome, Firefox veya Microsoft Edge kullanıyorsanız, hello tarayıcı hello tarayıcı penceresinde hello JSON görüntüler. Farklı tarayıcılar JSON dosyasını farklı şekilde işler ve tarayıcı pencereniz tam olarak hello örnekteki gibi görünmeyebilir.
   
    ![Chrome’da JSON meta verileri](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    Merhaba aşağıdaki örnek hello ilk bölümü hello hello API, Swagger meta verilerini gösterir hello için hello tanımıyla yöntemi alın. Bu meta veriler, hangi sürücü hello Swagger hello aşağıdaki adımları kullanın ve hello öğretici tooautomatically daha sonraki bir bölüme kullanın UI istemci kodu oluştur ' dir.
   
        {
          "swagger": "2.0",
          "info": {
            "version": "v1",
            "title": "ToDoListDataAPI"
          },
          "host": "localhost:45914",
          "schemes": [ "http" ],
          "paths": {
            "/api/ToDoList": {
              "get": {
                "tags": [ "ToDoList" ],
                "operationId": "ToDoList_GetByOwner",
                "consumes": [ ],
                "produces": [ "application/json", "text/json", "application/xml", "text/xml" ],
                "parameters": [
                  {
                    "name": "owner",
                    "in": "query",
                    "required": true,
                    "type": "string"
                  }
                ],
                "responses": {
                  "200": {
                    "description": "OK",
                    "schema": {
                      "type": "array",
                      "items": { "$ref": "#/definitions/ToDoItem" }
                    }
                  }
                },
                "deprecated": false
              },
4. Merhaba tarayıcınızı kapatın ve Visual Studio hata ayıklamayı durdurun.
5. Merhaba Todolistdataapı proje **Çözüm Gezgini**açın hello *App_Start\SwaggerConfig.cs* dosya ve sonra aşağı tooline 174 ve koddan hello açıklamadan çıkarın kaydırma.
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    Merhaba *SwaggerConfig.cs* dosya projede hello Swashbuckle paketini yüklediğinizde oluşturulur. Merhaba dosya yolları tooconfigure Swashbuckle sayısını sağlar.
   
    Swagger aşağıdaki hello kullanan kullanıcı Arabirimi adımları etkinleştirir hello kaldırdığını hello kodu. Hello API uygulaması proje şablonunu kullanarak bir Web API projesi oluşturduğunuzda, bu kod çıkışı varsayılan olarak bir güvenlik önlemi olarak eklenir.
6. Merhaba projeyi tekrar çalıştırın.
7. Tarayıcınızın adres çubuğuna, ekleme `swagger` toohello sonuna hello satır ve Return tuşuna basın. (URL hello `http://localhost:45914/swagger`.)
8. Merhaba Swagger kullanıcı Arabirimi sayfası görüntülendiğinde **ToDoList** toosee hello yöntemler kullanılabilir.
   
    ![Swagger kullanıcı arabirimi kullanılabilir yöntemleri](./media/app-service-api-dotnet-get-started/methods.png)
9. Merhaba ilk tıklatın **almak** hello listesinde düğmesi.
10. Merhaba, **parametreleri** bölümünde, hello hello değeri olarak bir yıldız işareti girin `owner` parametre ve ardından **deneyin**.
    
    Sonraki öğreticilerde kimlik doğrulama eklediğinizde, orta katman hello hello gerçek kullanıcı kimliği toohello veri katmanı sağlar. Hello uygulama kimlik doğrulama etkin olmadan çalışırken şu an için tüm görevler kendi sahibinin kimliği yıldız işareti olacaktır.
    
    ![Swagger kullanıcı arabirimini deneyin](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    Merhaba Swagger kullanıcı arabirimini hello ToDoList alma yöntemini çağırır ve hello yanıt kodunu ve JSON sonuçlarını görüntüler.
    
    ![Swagger kullanıcı arabirimini deneyin sonuçları](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. Tıklatın **Post**ve ardından hello kutusunda altında **Model şeması**.
    
    Merhaba hello Post yöntemi için parametre değeri belirtebileceğiniz hello model şeması prefills hello giriş kutusunu tıklatarak. (Internet Explorer'da bu işe yaramazsa, farklı bir tarayıcı kullanın veya hello parametre değeri hello sonraki adımda el ile girebilirsiniz.)  
    
    ![Swagger kullanıcı arabirimini deneyin Gönder](./media/app-service-api-dotnet-get-started/post.png)
12. Değişiklik hello JSON hello `todo` giriş parametresi aşağıdaki örneğine hello gibi görünüyor. böylece kutusunda ya da kendi açıklama metninizle değiştirin:
    
        {
          "ID": 2,
          "Description": "buy hello dog a toy",
          "Owner": "*"
        }
13. **Deneyin**’e tıklayın.
    
    Merhaba ToDoList API başarı belirten bir HTTP 204 yanıtı döndürür.
14. Merhaba ilk tıklatın **almak** düğmesini tıklatın ve ardından hello sayfanın bu bölümünde hello tıklatın **deneyin** düğmesi.
    
    Merhaba Get yöntemi yanıtı şimdi hello yeni toodo öğesi içerir.
15. İsteğe bağlı: hello Put, Delete, ayrıca deneyin ve kimliği yöntemlerle alın.
16. Merhaba tarayıcınızı kapatın ve Visual Studio hata ayıklamayı durdurun.

Swashbuckle her ASP.NET Web API projesi ile çalışır. Tooadd Swagger meta veri oluşturma tooan mevcut proje istiyorsanız, yalnızca hello Swashbuckle paketini yükleyin.

> [!NOTE]
> Swagger meta verileri her API işlemi için benzersiz bir kimlik içerir. Varsayılan olarak, Swashbuckle Web API denetleyicisi yöntemleriniz için yinelenen Swagger işlemi kimlikleri oluşturabilir. Bu durum, denetleyiciniz `Get()` ve `Get(id)` gibi, HTTP yöntemleriyle aşırı yüklü olduğunda gerçekleşir. Nasıl toohandle aşırı yüklemeler hakkında daha fazla bilgi için bkz: [özelleştirme Swashbuckle tarafından oluşturulan API tanımlarını](app-service-api-dotnet-swashbuckle-customize.md). Visual Studio'da hello Azure API uygulaması şablonu kullanarak bir Web API projesi oluşturursanız, benzersiz işlem kimlikleri oluşturan kod otomatik olarak toohello eklenen *SwaggerConfig.cs* dosya.  
> 
> 

## <a id="createapiapp"></a>Azure'da API uygulaması oluşturma ve kod tooit dağıtma
Bu bölümde, Visual Studio hello tümleştirilmiştir Azure araçlarını kullanırsınız **Web'i Yayımla** Sihirbazı toocreate yeni bir API uygulamasına. Ardından hello Todolistdataapı projesi toohello yeni API uygulamasına dağıtmak ve hello Swagger kullanıcı arabirimini çalıştırarak hello API çağrısı.

1. İçinde **Çözüm Gezgini**hello Todolistdataapı projesine sağ tıklayın ve ardından **Yayımla**.
   
    ![Visual Studio’ya Yayımla'ya tıklama](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. Merhaba, **profil** hello adımında **Web'i Yayımla** Sihirbazı'nı tıklatın **Microsoft Azure App Service**.
   
   ![Web’de Yayımla sihirbazında Azure App Service’e tıklama](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. Zaten yapmadıysanız tooyour Azure hesabı oturum veya süresi dolduysa, kimlik bilgilerinizi yenileyin.
4. Buna hello App Service iletişim kutusunda, hello Azure'ı seçin **abonelik** toouse istediğiniz ve ardından **yeni**.
   
    ![App Service iletişim kutusunda Yeni’ye tıklama](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    Merhaba **barındırma** hello sekmesinde **App Service Oluştur** iletişim kutusu görüntülenir.
   
    Swashbuckle yüklü olan bir Web API projesi dağıttığınız için Visual Studio bir API uygulaması toocreate istediğinizi varsayar. Bu hello tarafından belirtilir **API uygulaması adı** başlık ve tarafından bu hello olgu hello **türünü değiştir** aşağı açılan liste çok ayarlamak**API uygulaması**.
   
    ![App Service iletişim kutusunda Uygulama türü](./media/app-service-api-dotnet-get-started/apptype.png)
5. Girin bir **API uygulaması adı** hello benzersiz *azurewebsites.net* etki alanı. Visual Studio'nun önerdiği hello varsayılan adı kabul edebilirsiniz.
   
    Başka birinin önceden kullandığı bir adı girerseniz, kırmızı bir ünlem işareti toohello sağ bakın.
   
    Merhaba hello API uygulamasının URL'si olacaktır `{API app name}.azurewebsites.net`.
6. Merhaba, **kaynak grubu** açılır menüsünde tıklatın **yeni**ve ardından isterseniz "isterseniz ToDoListGroup" ya da başka bir ad girin.
   
    Kaynak grubu API uygulamaları, veritabanları, sanal makineler ve benzerleri gibi Azure kaynakları koleksiyonudur.    Kolay toodelete tüm hello öğretici için oluşturduğunuz Azure kaynaklarını hello tek bir adımda kolaylaştırır Bu öğretici için en iyi toocreate yeni bir kaynak grubu demektir.
   
    Bu kutu mevcut [kaynak grubunu](../azure-resource-manager/resource-group-overview.md) seçmenize ya da aboneliklerinizdeki kaynak grubunda olanlardan farklı bir ad yazarak yeni bir tane oluşturmanıza olanak tanır.
7. Merhaba tıklatın **yeni** düğmesine bir sonraki toohello **App Service planı** açılır.
   
    Merhaba gösteren ekran görüntüsü için örnek değerleri **API uygulaması adı**, **abonelik**, ve **kaynak grubu** --değerlerinizi farklı olacaktır.
   
    ![App Service iletişim kutusu oluşturma](./media/app-service-api-dotnet-get-started/createas.png)
   
    Aşağıdaki adımları hello hello yeni kaynak grubu için bir uygulama hizmeti planı oluşturun. Bir uygulama hizmeti planı, API uygulamanızın üzerinde çalışacağı hello işlem kaynaklarını belirtir. Örneğin, hello ücretsiz katmanı seçerseniz API uygulamanız paylaşılan Vm'lerinde bazı Ücretli katmanlarda ayrılmış sanal makine çalışırken çalışır. App Service planları hakkında bilgi için bkz. [App Service planlarına genel bakış](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
8. Merhaba, **App Service planı Yapılandır** iletişim kutusunda, tercih ederseniz, "ToDoListPlan" ya da başka bir ad girin.
9. Merhaba, **konumu** aşağı açılan listesinde, en yakın tooyou hello konumu seçin.
   
    Bu ayar, uygulamanızın hangi Azure veri merkezinde çalıştırılacağını belirtir. Bir konum kapatmak tooyou toominimize seçin [gecikme](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).
10. Merhaba, **boyutu** açılır menüsünde tıklatın **serbest**.
    
    Bu öğretici için hello ücretsiz fiyatlandırma katmanı yeterli ölçüde performans sunacaktır.
11. Merhaba, **App Service planı Yapılandır** iletişim kutusunda, tıklatın **Tamam**.
    
    ![App Service Planı Yapılandır iletişim kutusunda Tamam’a tıklama](./media/app-service-api-dotnet-get-started/configasp.png)
12. Merhaba, **App Service Oluştur** iletişim kutusu, tıklatın **oluşturma**.
    
    ![App Service Oluştur iletişim kutusunda Oluştur’a tıklama](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    Visual Studio hello API uygulaması ve tüm gerekli hello ayarlarını hello API uygulaması için sahip bir yayımlama profili oluşturur. Merhaba açar sonra **Web'i Yayımla** kullanacağınız Sihirbazı toodeploy hello projesi.
    
    Merhaba **Web'i Yayımla** Sihirbazı açılır hello üzerinde **bağlantı** sekmesidir (aşağıda gösterilen).
    
    Merhaba üzerinde **bağlantı** hello sekmesinde, **Server** ve **Site adı** ayarları noktası tooyour API uygulaması. Merhaba **kullanıcı adı** ve **parola** Azure'un sizin için oluşturduğu dağıtım kimlik bilgileridir. Dağıtımdan sonra Visual Studio tarayıcı toohello açılır **hedef URL** (Merhaba tek amacıdır olan **hedef URL**).  
13. **İleri**’ye tıklayın.
    
    ![Web'i Yayımla sihirbazının Bağlantı sekmesinde İleri'ye tıklama](./media/app-service-api-dotnet-get-started/connnext.png)
    
    Merhaba sonraki sekme kullanılabilir hello **ayarları** sekmesidir (aşağıda gösterilen). Burada bir hata ayıklama derlemesi için hello derleme yapılandırma sekmesini toodeploy değiştirebilirsiniz [uzaktan hata ayıklama](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug). Merhaba ayrıca sekmede birkaç farklı **dosya yayımlama seçeneği**:
    
    * Hedefteki ek dosyaları kaldır
    * Yayımlama sırasında ön derleme yap
    * Merhaba App_Data klasöründeki dosyaları dışarıda bırak
    
    Bu öğreticide bunlardan biri gerekmez. Bunların ne yaptıklarına ilişkin ayrıntılı açıklamalar için bkz. [Nasıl yapılır: Visual Studio’da Tek Tıklamayla Yayımlamayı Kullanarak Web Projesi Dağıtma](https://msdn.microsoft.com/library/dd465337.aspx).
14. **İleri**’ye tıklayın.
    
    ![Web’i Yayımla sihirbazının Ayarlar sekmesi İleri’ye tıklama](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    Sonraki hello olduğu **Önizleme** hangi dosyaların proje toohello API uygulamanızdan kopyalanan toobe giderek bir fırsat toosee sağlayan sekmesidir (aşağıda gösterilen),. Tooearlier zaten dağıtılmış bir proje tooan API uygulaması dağıtıyorsanız, yalnızca değiştirilen dosyalar kopyalanır. Toosee kopyalanacak dosyaların bir listesini istiyorsanız hello tıklatabilirsiniz **önizlemeyi Başlat** düğmesi.
15. **Yayımla**’ta tıklayın.
    
    ![Web’i Yayımla sihirbazının Önizleme sekmesinde Yayımla’ya tıklama](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    Visual Studio hello Todolistdataapı projesi toohello yeni API uygulamasına dağıtır. Merhaba **çıkış** penceresi başarılı dağıtımı günlüğe kaydeder ve bir tarayıcı açılır pencere toohello URL hello API uygulamasının "başarıyla oluşturuldu" sayfası görüntülenir.
    
    ![Çıktı penceresi başarılı dağıtım](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Yeni API uygulaması başarıyla oluşturuldu sayfası](./media/app-service-api-dotnet-get-started/appcreated.png)
16. Merhaba tarayıcının adres çubuğunda "swagger" toohello URL'sini ekleyin ve ardından Enter tuşuna basın. (URL hello `http://{apiappname}.azurewebsites.net/swagger`.)
    
    Merhaba tarayıcı aynı Swagger daha önce gördüğünüzle kullanıcı arabirimini, ancak şimdi hello bulutta çalışan hello görüntüler. GET yöntemi hello ve geri toohello varsayılan 2 yapılacak işler öğelerine döndüğünüzü görün deneyin. daha önce yaptığınız hello değişiklikler hello yerel makine bellekte kaydedildi.
17. Açık hello [Azure portal](https://portal.azure.com/).
    
    Hello Azure portal, API uygulamaları gibi Azure kaynakları yöneten için bir web arabirimidir.
18. **Diğer Hizmetler > Uygulama Hizmetleri**’ne tıklayın.
    
    ![Uygulama Hizmetleri’ne Gözatma](./media/app-service-api-dotnet-get-started/browseas.png)
19. Merhaba, **uygulama hizmetleri** dikey penceresinde, bulma ve yeni API uygulamanızı'ı tıklatın. (Toohello sağ açın windows hello Azure portal, olarak adlandırılan *dikey*.)
    
    ![Uygulama Hizmetleri dikey penceresi](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    İki dikey pencere açılır. Bir dikey pencerede hello API uygulamasına genel bir bakış ve bir görüntüleyip değiştirmek ayarları uzun bir listesi varsa.
20. Merhaba, **ayarları** dikey penceresinde, Bul hello **API** 'ye tıklayın **API tanımı**.
    
    ![Ayarlar dikey penceresinde API Tanımı](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    Merhaba **API tanımı** dikey penceresi JSON biçiminde Swagger 2.0 meta verileri döndürür hello URL'yi belirtmenize olanak sağlar. Visual Studio hello API uygulaması oluşturduğunda, hello API uygulaması, daha önce gördüğünüz Swashbuckle tarafından oluşturulan meta verileri temel için hello API tanımı URL toohello varsayılan değeri ayarlar URL'si artı `/swagger/docs/v1`.
    
    ![API tanımı URL'si](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    Bunun için bir API uygulaması toogenerate istemci kodu seçtiğinizde, Visual Studio hello meta verileri bu URL'den alır.

## <a id="codegen"></a>Merhaba veri katmanı için istemci kodu oluştur
Azure API uygulamaları Swagger tümleştirme hello avantajları otomatik kod oluşturma biridir. Oluşturulan istemci sınıfları API uygulamasını çağıran bir daha kolay toowrite kod kolaylaştırır.

Merhaba Todolistapı projesinin oluşturulan hello istemci kodu zaten sahip, ancak aşağıdaki adımları hello silin ve nasıl toodo hello kod oluşturma toosee yeniden.

1. Visual Studio'da **Çözüm Gezgini**, hello Todolistapı projesi, hello silme *Todolistdataapı* klasör. **Dikkat: Merhaba Todolistdataapı projesini yalnızca hello klasörünü silin.**
   
    ![Oluşturulan istemci kodunu silme](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    Bu klasör, toogo hakkında olduğunuz hello kod oluşturma işlemi kullanılarak oluşturuldu.
2. Merhaba Todolistapı projesine sağ tıklayın ve ardından **Ekle > REST API istemcisi**.
   
    ![Visual Studio'da REST API istemcisi ekleme](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. Merhaba, **REST API istemcisi Ekle** iletişim kutusu, tıklatın **Swagger URL'si**ve ardından **Azure varlığını Seç**.
   
    ![Azure Varlığını Seç](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. Merhaba, **uygulama hizmeti** iletişim kutusunda, Bu öğretici için kullanmakta olduğunuz hello kaynak grubunu genişletin ve API uygulamanızı seçin ve ardından **Tamam**.
   
    ![Kod oluşturma için API uygulaması seçme](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    Toohello döndüğünüzde dikkat **REST API istemcisi Ekle** iletişim kutusunda, hello metin kutusuna doldurulmuş hello API tanımı oturum hello Portalı'nda daha önce gördüğünüz URL değeri.
   
    ![API Tanımı URL'si](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > Kod oluşturma için bir alternatif yol tooget meta verileri hello Gözat iletişim kutusunu kullanmak yerine doğrudan tooenter hello URL'dir. Veya tooAzure dağıtmadan önce toogenerate istemci kodu istiyorsanız hello Web API projesini yerel olarak çalıştırmak, hello dosyayı Kaydet hello Swagger JSON dosyasını sağlayan toohello URL gidin ve hello kullanabilirsiniz **mevcut bir Swagger meta veri dosyasıseçin**seçeneği.
   > 
   > 
5. Merhaba, **REST API istemcisi Ekle** iletişim kutusu, tıklatın **Tamam**.
   
    Visual Studio hello API uygulamasının adını alan bir klasör oluşturur ve istemci sınıfları oluşturur.
   
    ![Oluşturulan istemci için kod dosyaları](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. Merhaba Todolistapı projesinde, açık *Controllers\ToDoListController.cs* toosee hello kodu 40 satırında oluşturulan hello istemcisini kullanarak hello API'sini çağırır.
   
    Get yöntemi çağrıları hello ve aşağıdaki kod parçacığında hello hello kod hello istemci nesnesini nasıl başlatır gösterir.
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));
            return client;
        }
   
        public async Task<IEnumerable<ToDoItem>> Get()
        {
            using (var client = NewDataAPIClient())
            {
                var results = await client.ToDoList.GetByOwnerAsync(owner);
                return results.Select(m => new ToDoItem
                {
                    Description = m.Description,
                    ID = (int)m.ID,
                    Owner = m.Owner
                });
            }
        }
   
    Merhaba Oluşturucu parametresini alır hello uç nokta URL'si hello `toDoListDataAPIURL` uygulama ayarı. Merhaba Web.config dosyasında bu, yerel IIS Express URL'sini hello API proje hello uygulama yerel olarak çalıştırabilmeniz için kümesi toohello değerdir. Merhaba Oluşturucu parametresini atlarsanız, hello varsayılan uç hello koddan oluşturulan hello URL'dir.
7. İstemci sınıfınız, API uygulaması adınıza göre farklı bir ad ile oluşturulur; Merhaba kodda değişiklik *Controllers\ToDoListController.cs* hello türü adı ne projenizde oluşturulan böylece eşleşir. Örneğin, API Uygulamanıza ToDoListDataAPI071316 adını verdiyseniz kodu değiştirin:
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

toothis:

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-toohost-hello-middle-tier"></a>Bir API uygulaması toohost hello orta katman oluşturma
Daha önce [hello veri katmanı API uygulaması oluşturdunuz ve kodu tooit dağıtılan](#createapiapp).  Merhaba izleyin artık hello orta katman API uygulaması için aynı yordamı.

1. İçinde **Çözüm Gezgini**, sağ hello orta katman Todolistapı projesine (değil hello veri katmanı Todolistdataapı) ve ardından **Yayımla**.
   
    ![Visual Studio’ya Yayımla'ya tıklama](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. Merhaba, **profil** hello sekmesinde **Web'i Yayımla** Sihirbazı'nı tıklatın **Microsoft Azure App Service**.
3. Merhaba, **uygulama hizmeti** iletişim kutusu, tıklatın **yeni**.
4. Merhaba, **barındırma** hello sekmesinde **App Service Oluştur** iletişim kutusunda, hello varsayılanı kabul **API uygulaması adı** hello benzersiz bir ad girin veya  *azurewebsites.NET* etki alanı.
5. Hello Azure'ı seçin **abonelik** , kullanmakta olduğunuz.
6. Merhaba, **kaynak grubu** açılan listesinde, hello seçin daha önce oluşturduğunuz aynı kaynak grubu.
7. Merhaba, **uygulama hizmeti planı** açılan listesinde, hello seçin önceden oluşturduğunuz planı. Bu varsayılan toothat değer kullanılacak.
8. **Oluştur**'a tıklayın.
   
    Visual Studio hello API uygulamasını oluşturur, bunun için bir yayımlama profili oluşturur ve görüntüler hello **bağlantı** hello adımında **Web'i Yayımla** Sihirbazı.
9. Merhaba, **bağlantı** hello adımında **Web'i Yayımla** Sihirbazı'nı tıklatın **Yayımla**.
   
   Visual Studio hello Todolistapı projesi toohello yeni API uygulamasına dağıtır ve tarayıcı toohello hello API uygulaması URL'sini açar. Merhaba "başarıyla oluşturuldu" sayfası görüntülenir.

## <a name="configure-hello-middle-tier-toocall-hello-data-tier"></a>Merhaba orta katman toocall hello veri katmanını yapılandırın
Merhaba orta katman API uygulamasını çağırdıysanız, hala hello Web.config dosyasındaki hello localhost URL'sini kullanarak toocall hello veri katmanı isteriz. Bu bölümde hello orta katman API uygulamasındaki bir ortam ayarına hello veri katmanı API uygulaması URL'sini girin. Merhaba hello orta katman API uygulamasındaki kod hello veri katmanı URL ayarını aldığında hello ortamı ayarı ne hello Web.config dosyasında geçersiz kılar.

1. Toohello Git [Azure portal](https://portal.azure.com/)ve ardından toohello gidin **API uygulaması** toohost hello Todolistapı (orta katman) proje oluşturulan hello API uygulaması dikey penceresinde.
2. İçinde API uygulamasının hello **ayarları** dikey penceresinde tıklatın **uygulama ayarları**.
3. İçinde API uygulamasının hello **uygulama ayarları** dikey penceresinde, toohello aşağı **uygulama ayarları** bölümünde ve hello aşağıdakileri ekleyin anahtar ve değer. Merhaba değer hello ilk API Bu öğreticide yayımlanan uygulama hello URL'si olacaktır.
   
   | **Anahtar** | toDoListDataAPIURL |
   | --- | --- |
   | **Değer** |https://{your data tier API app name}.azurewebsites.net |
   | **Örnek** |https://todolistdataapi.azurewebsites.net |
4. **Kaydet** düğmesine tıklayın.
   
    ![Uygulama Ayarları için Kaydet’e tıklama](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    Merhaba kod Azure içinde çalıştığında, bu değer şimdi hello Web.config dosyasındaki hello localhost URL'sini geçersiz kılar.

## <a name="test"></a>Test etme
1. Bir tarayıcı penceresinde hello yeni orta katman Todolistapı için oluşturduğunuz API uygulaması URL'sini toohello göz atın. Merhaba API uygulamasının ana dikey hello portalında hello URL'de tıklayarak buradan ulaşabilirsiniz.
2. Merhaba tarayıcının adres çubuğunda "swagger" toohello URL'sini ekleyin ve ardından Enter tuşuna basın. (URL hello `http://{apiappname}.azurewebsites.net/swagger`.)
   
    Merhaba tarayıcı görüntüler hello aynı Swagger Todolistdataapı için daha önce ancak şimdi gördüğünüzle kullanıcı arabirimini `owner` hello orta katman API uygulaması sizin için bu değeri toohello veri katmanı API uygulamasına gönderdiği için hello alma işlemi için gerekli bir alan değil. (Kimlik doğrulaması öğreticilerini hello hello orta katman hello için gerçek kullanıcı kimliklerini gönderir `owner` parametresi; şimdi onu bir yıldız işareti kodlamak için.)
3. GET yöntemi hello ve hello orta katman API uygulaması hello diğer yöntemleri toovalidate başarıyla hello veri katmanı API uygulamasını çağıran deneyin.
   
    ![Swagger kullanıcı arabirimi Alma yöntemi](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a>Sorun giderme
Bu öğreticiyi izlerken bir sorunla karşılaşırsanız, bazı sorun giderme fikirlerini burada bulabilirsiniz.

* Merhaba hello en son sürümünü kullandığınızdan emin olun [.NET için Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003).
* Merhaba proje adı benzerdir (Todolistapı, Todolistdataapı) ikisidir. Öğeleri bir projeyle çalışırken hello yönergelerde açıklandığı gibi görünmüyorsa, hello doğru projeyi açtığınızdan emin olun.
* Kurumsal bir ağda bulunuyorsanız ve bir güvenlik duvarı üzerinden toodeploy tooAzure uygulama hizmeti çalışıyorsanız, bağlantı noktası 443 ve 8172 Web dağıtımı için açık olduğundan emin olun. Bu bağlantı noktalarını açamıyorsanız, diğer dağıtım yöntemlerini kullanabilirsiniz.  Bkz: [, uygulama tooAzure uygulama hizmeti dağıtmak](../app-service-web/web-sites-deploy.md).
* Yanlışlıkla hello yanlış projeyi tooan API uygulama dağıtır ve daha sonra hello doğru bir tooit dağıtma "rota adları benzersiz olmalıdır" hataları--bu hataları alabilirsiniz. toocorrect Bu, yeniden dağıtın hello doğru projeyi toohello API uygulaması ve hello **ayarları** hello sekmesinde **Web'i Yayımla** Sihirbazı'nı seçin **hedeftekiekdosyalarıKaldır**.

Azure App Service'de ASP.NET API uygulamanızı çalıştırdıktan sonra sorun giderme sürecini kolaylaştıracak Visual Studio özellikleri hakkında daha fazla toolearn isteyebilirsiniz. Günlüğe kaydetme, uzaktan hata ayıklama ve çok daha fazlası hakkında bilgi edinmek için bkz. [Visual Studio’da Azure App Service uygulamalarının sorunlarını giderme](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).

## <a name="next-steps"></a>Sonraki adımlar
Nasıl toodeploy mevcut Web API projeleri tooAPI apps, API uygulamaları için istemci kodu oluşturmak ve .NET istemcilerinden API uygulamalarını kullanmayı gördünüz. Bu serideki sonraki öğretici Hello gösterir nasıl çok[JavaScript istemcilerinden CORS tooconsume API uygulamalarını kullanmak](app-service-api-cors-consume-javascript.md).

İstemci kodu oluşturma hakkında daha fazla bilgi için bkz: Merhaba [Azure/AutoRest](https://github.com/azure/autorest) Github.com'u havuzda. Oluşturulan hello istemcisini kullanarak sorunlarıyla ilgili Yardım için açık bir [hello AutoRest deposunda sorunu](https://github.com/azure/autorest/issues).

Toocreate yeni API uygulaması projeleri sıfırdan istiyorsanız hello kullanın **Azure API uygulaması** şablonu.

![Visual Studio’da API Uygulaması şablonu](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

Merhaba **Azure API uygulaması** proje şablonudur eşdeğer toochoosing hello **boş** ASP.NET 4.5.2 şablonu hello onay kutusunu tooadd Web API desteği tıklayarak ve hello Swashbuckle NuGet paketi yükleniyor. Ayrıca, bazı Swashbuckle yapılandırma tasarlanmış kod tooprevent hello oluşturulmasını yinelenen Swagger işlem kimlikleri hello şablon ekler. Bir API uygulaması projesi oluşturduktan sonra tooan API uygulaması hello dağıtabilirsiniz Bu öğreticide gördüğünüz şekilde.

