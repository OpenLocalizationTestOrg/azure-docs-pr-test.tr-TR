---
title: "aaaCustomize Swashbuckle tarafından oluşturulan API tanımlarını"
description: "Bilgi nasıl Azure App Service'deki bir API uygulaması için Swashbuckle tarafından oluşturulan toocustomize Swagger API'si tanımlar."
services: app-service\api
documentationcenter: .net
author: bradygaster
manager: erikre
editor: jimbe
ms.assetid: 6b8cbc38-d282-4a0f-b0c5-762631bae6f3
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: e31c665f8993533c5ec9a935e42cce34f86a5ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-swashbuckle-generated-api-definitions"></a>Swashbuckle tarafından oluşturulan API tanımlarını özelleştirme
## <a name="overview"></a>Genel Bakış
Bu makalede açıklanır nasıl toocustomize Swashbuckle toohandle yaygın senaryolar istediğiniz tooalter hello varsayılan davranışı:

* Denetleyici yöntemi aşırı yüklemeleri için yinelenen işlemi tanımlayıcıları Swashbuckle oluşturur
* Bir yöntemin geçerli yanıttan HTTP 200 (Tamam), yalnızca Swashbuckle bu hello varsayar. 

## <a name="customize-operation-identifier-generation"></a>İşlem tanımlayıcısı nesil özelleştirme
Swashbuckle, denetleyici adı ve yöntem adı birleştirerek Swagger işlemi tanımlayıcıları oluşturur. Bir yöntemin birden çok aşırı olduğunda bu deseni bir sorun oluşturur: Swashbuckle geçersiz Swagger JSON olduğu yinelenen işlem kimlikleri oluşturur.

Örneğin, denetleyici koddan hello Swashbuckle toogenerate üç Contact_Get işlem kimlikleri neden olur.

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

Bu örneğin hello aşağıdaki gibi benzersiz adlar hello yöntemleri vererek hello sorunu el ile çözebilirsiniz:

* Al
* GetById
* GetPage

Merhaba, benzersiz işlem kimlikleri otomatik olarak oluşturmasını tooextend Swashbuckle toomake alternatiftir.

Merhaba aşağıdaki adımları kullanarak Swashbuckle toocustomize nasıl hello Göster *SwaggerConfig.cs* hello Visual Studio API Apps Preview proje şablonu tarafından hello projeye dahil dosyası.  Dağıtım bir API uygulaması olarak yapılandırdığınız bir Web API projesinde, Swashbuckle de özelleştirebilirsiniz.

1. Bir özel Oluştur `IOperationFilter` uygulama 
   
    Merhaba `IOperationFilter` arabirimi hello Swagger meta veri işlemi çeşitli yönlerini toocustomize istediğiniz Swashbuckle kullanıcılar için bir genişletilebilirlik noktası sağlar. Hello aşağıdaki kodu hello işlemi kimliği oluşturma davranışı değiştirmenin bir yöntemi gösterir. Merhaba kod parametre adları toohello işlem kimliği adı ekler.  
   
        using Swashbuckle.Swagger;
        using System.Web.Http.Description;
   
        namespace ContactsList
        {
            public class MultipleOperationsWithSameVerbFilter : IOperationFilter
            {
                public void Apply(
                    Operation operation,
                    SchemaRegistry schemaRegistry,
                    ApiDescription apiDescription)
                {
                    if (operation.parameters != null)
                    {
                        operation.operationId += "By";
                        foreach (var parm in operation.parameters)
                        {
                            operation.operationId += string.Format("{0}",parm.name);
                        }
                    }
                }
            }
        }
2. İçinde *App_Start\SwaggerConfig.cs* dosyasını, arama hello `OperationFilter` yöntemi toocause Swashbuckle toouse hello yeni `IOperationFilter` uygulaması.
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    Merhaba *SwaggerConfig.cs* Swashbuckle NuGet paketi hello tarafından bırakılan dosyası genişletilebilirlik noktaları birçok kılınan örnekleri içerir. Merhaba ek açıklamalar burada gösterilmiyor. 
   
    Bu değişikliği yaptıktan sonra `IOperationFilter` uygulama kullanılır ve oluşturulan benzersiz işlem kimlikleri toobe neden olur.
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a>Yanıt kodu 200 dışında izin ver
Varsayılan olarak, Swashbuckle bir HTTP 200 (Tamam) yanıt hello varsayar *yalnızca* yasal bir Web API yöntemi yanıtı. Bazı durumlarda, bir özel durum hello istemci tooraise neden olmadan diğer yanıt kodları tooreturn isteyebilirsiniz.  Örneğin, hello aşağıdaki Web API kodunda hello istemci tooaccept istersiniz bir senaryo bir 200 veya 404 yanıtı geçerli yanıtlarını olarak gösterir.

    [ResponseType(typeof(Contact))]
    public HttpResponseMessage Get(int id)
    {
        var contacts = GetContacts();

        var requestedContact = contacts.FirstOrDefault(x => x.Id == id);

        if (requestedContact == null)
        {
            return Request.CreateResponse(HttpStatusCode.NotFound);
        }
        else
        {
            return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
        }
    }

Bu senaryoda, yalnızca bir meşru HTTP durum kodu, HTTP 200 hello Swashbuckle varsayılan olarak üretir Swagger belirtir.

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

Visual Studio için hello istemci hello Swagger API tanımı toogenerate kod kullandığından, bir HTTP 200 dışındaki herhangi bir yanıt için bir özel durum başlatır istemci kodu oluşturur. Bu örnek Web API yöntemi için oluşturulan bir C# istemci aşağıdaki Hello kodu arasındadır.

    if (statusCode != HttpStatusCode.OK)
    {
        HttpOperationException<object> ex = new HttpOperationException<object>();
        ex.Request = httpRequest;
        ex.Response = httpResponse;
        ex.Body = null;
        if (shouldTrace)
        {
            ServiceClientTracing.Error(invocationId, ex);
        }
        throw ex;
    } 

Swashbuckle XML açıklamaları veya hello kullanarak bunu oluşturur, beklenen HTTP yanıt kodları hello listesi özelleştirme iki yolu sağlar `SwaggerResponse` özniteliği. Merhaba özniteliği kolaydır, ancak yalnızca Swashbuckle 5.1.5 veya sonraki sürümlerinde. Merhaba API uygulamaları önizleme yeni proje şablonu Visual Studio 2013'te içerir Swashbuckle sürüm 5.0.0, hello şablon kullandı ve tooupdate Swashbuckle istemiyorsanız, tek seçeneğiniz toouse XML açıklamaları gelir. 

### <a name="customize-expected-response-codes-using-xml-comments"></a>XML açıklamaları kullanarak beklenen yanıt kodlarını özelleştirme
Swashbuckle sürümünüzü 5.1.5 önce ise, bu yöntemi toospecify yanıt kodlarını kullanın.

1. İlk olarak, XML belge açıklamaları için HTTP yanıt kodları toospecify istediğiniz hello yöntemleri üzerinden ekleyin. Yukarıda gösterilen ve uygulama hello XML belgeleri tooit aşağıdaki örneğine hello gibi bir kod neden olacağından hello örnek Web API eylemi yapılıyor. 
   
        /// <summary>
        /// Returns hello specified contact.
        /// </summary>
        /// <param name="id">hello ID of hello contact.</param>
        /// <returns>A contact record with an HTTP 200, or null with an HTTP 404.</returns>
        /// <response code="200">OK</response>
        /// <response code="404">Not Found</response>
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
   
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
2. Yönergeler hello ekleyin *SwaggerConfig.cs* toodirect Swashbuckle toomake hello XML belge dosyası kullanımını dosya.
   
   * Açık *SwaggerConfig.cs* ve hello üzerinde bir yöntem oluşturma *SwaggerConfig* sınıfı toospecify hello yolu toohello belge XML dosyası. 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * Aşağı kaydırın hello *SwaggerConfig.cs* hello kılınan kod satırı, aşağıda gösterilen hello ekran benzeyen görene kadar dosya. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * Swagger oluşturma sırasında işleme hello satır tooenable hello XML açıklamaları açıklamadan çıkarın. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. Sipariş toogenerate hello XML belge dosyası, hello projenin özelliklerine gidin ve aşağıdaki hello ekran görüntüsünde gösterildiği gibi hello XML belge dosyası etkinleştirin. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

Bu adımları gerçekleştirdikten sonra hello Swagger JSON Swashbuckle tarafından oluşturulan hello XML açıklamaları belirtilen hello HTTP yanıt kodları yansıtır. Bu yeni JSON yükü Hello ekran görüntüsü aşağıda gösterilmiştir. 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

REST API için Visual Studio tooregenerate hello istemci kodu kullandığınızda, hello C# kodu her iki hello HTTP Tamam ve bulunamadı durum kodları toohandle Merhaba null dönüş nasıl üzerinde kullanıcı kodu toomake kararlarınızı izin vererek, bir özel durum yükseltmeden kabul eder Kayıt başvurun. 

        if (statusCode != HttpStatusCode.OK && statusCode != HttpStatusCode.NotFound)
        {
            HttpOperationException<object> ex = new HttpOperationException<object>();
            ex.Request = httpRequest;
            ex.Response = httpResponse;
            ex.Body = null;
            if (shouldTrace)
            {
                ServiceClientTracing.Error(invocationId, ex);
            }
                throw ex;
        }

Bu Tanıtım için Hello kod bulunabilir [bu GitHub deposunu](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse). Web API Hello yanı sıra ile XML belgeleri yorumları artırıldığında bu API için oluşturulan istemci içeren bir konsol uygulama projesi projesidir. 

### <a name="customize-expected-response-codes-using-hello-swaggerresponse-attribute"></a>Merhaba SwaggerResponse özniteliğini kullanarak beklenen yanıt kodlarını Özelleştir
Merhaba [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) özniteliktir ve sonrasında Swashbuckle 5.1.5 içinde kullanılabilir. Projenizde önceki bir sürümü yüklü durumda, bu bölümde nasıl tooupdate hello Swashbuckle NuGet paketini bu öznitelik kullanabilmesi için açıklayarak başlatır.

1. İçinde **Çözüm Gezgini**, Web API projenize sağ tıklatın ve **NuGet paketlerini Yönet**. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. Merhaba tıklatın *güncelleştirme* düğmesine bir sonraki toohello *Swashbuckle* NuGet paketi. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. Merhaba eklemek *SwaggerResponse* toohello Web API eylem yöntemleri toospecify geçerli HTTP yanıtı kodları istediğiniz öznitelikler. 
   
        [SwaggerResponse(HttpStatusCode.OK)]
        [SwaggerResponse(HttpStatusCode.NotFound)]
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
4. Ekleme bir `using` hello özniteliğin ad alanı bildirimi:
   
        using Swashbuckle.Swagger.Annotations;
5. Toohello Gözat */swagger/docs/v1* hello çeşitli HTTP yanıt kodları görünür durumda olur ve proje URL'sini hello Swagger JSON. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

Bu Tanıtım için Hello kod bulunabilir [bu GitHub deposunu](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes). Merhaba birlikte Web API projesi hello ile donatılmış *SwaggerResponse* bu API için oluşturulan istemci içeren bir konsol uygulama projesi bir özniteliktir. 

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, işlem kimlikleri ve geçerli yanıt kodları toocustomize hello yolu Swashbuckle nasıl oluşturur göstermiştir. Daha fazla bilgi için bkz: [github'da Swashbuckle](https://github.com/domaindrivendev/Swashbuckle).

