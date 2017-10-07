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
# <a name="customize-swashbuckle-generated-api-definitions"></a><span data-ttu-id="87142-103">Swashbuckle tarafından oluşturulan API tanımlarını özelleştirme</span><span class="sxs-lookup"><span data-stu-id="87142-103">Customize Swashbuckle-generated API definitions</span></span>
## <a name="overview"></a><span data-ttu-id="87142-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="87142-104">Overview</span></span>
<span data-ttu-id="87142-105">Bu makalede açıklanır nasıl toocustomize Swashbuckle toohandle yaygın senaryolar istediğiniz tooalter hello varsayılan davranışı:</span><span class="sxs-lookup"><span data-stu-id="87142-105">This article explains how toocustomize Swashbuckle toohandle common scenarios where you may want tooalter hello default behavior:</span></span>

* <span data-ttu-id="87142-106">Denetleyici yöntemi aşırı yüklemeleri için yinelenen işlemi tanımlayıcıları Swashbuckle oluşturur</span><span class="sxs-lookup"><span data-stu-id="87142-106">Swashbuckle generates duplicate operation identifiers for overloads of controller methods</span></span>
* <span data-ttu-id="87142-107">Bir yöntemin geçerli yanıttan HTTP 200 (Tamam), yalnızca Swashbuckle bu hello varsayar.</span><span class="sxs-lookup"><span data-stu-id="87142-107">Swashbuckle assumes that hello only valid response from a method is HTTP 200 (OK)</span></span> 

## <a name="customize-operation-identifier-generation"></a><span data-ttu-id="87142-108">İşlem tanımlayıcısı nesil özelleştirme</span><span class="sxs-lookup"><span data-stu-id="87142-108">Customize operation identifier generation</span></span>
<span data-ttu-id="87142-109">Swashbuckle, denetleyici adı ve yöntem adı birleştirerek Swagger işlemi tanımlayıcıları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="87142-109">Swashbuckle generates Swagger operation identifiers by concatenating controller name and method name.</span></span> <span data-ttu-id="87142-110">Bir yöntemin birden çok aşırı olduğunda bu deseni bir sorun oluşturur: Swashbuckle geçersiz Swagger JSON olduğu yinelenen işlem kimlikleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="87142-110">This pattern creates a problem when you have multiple overloads of a method: Swashbuckle generates duplicate operation ids, which is invalid Swagger JSON.</span></span>

<span data-ttu-id="87142-111">Örneğin, denetleyici koddan hello Swashbuckle toogenerate üç Contact_Get işlem kimlikleri neden olur.</span><span class="sxs-lookup"><span data-stu-id="87142-111">For example, hello following controller code causes Swashbuckle toogenerate three Contact_Get operation ids.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

<span data-ttu-id="87142-112">Bu örneğin hello aşağıdaki gibi benzersiz adlar hello yöntemleri vererek hello sorunu el ile çözebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="87142-112">You can solve hello problem manually by giving hello methods unique names, such as hello following for this example:</span></span>

* <span data-ttu-id="87142-113">Al</span><span class="sxs-lookup"><span data-stu-id="87142-113">Get</span></span>
* <span data-ttu-id="87142-114">GetById</span><span class="sxs-lookup"><span data-stu-id="87142-114">GetById</span></span>
* <span data-ttu-id="87142-115">GetPage</span><span class="sxs-lookup"><span data-stu-id="87142-115">GetPage</span></span>

<span data-ttu-id="87142-116">Merhaba, benzersiz işlem kimlikleri otomatik olarak oluşturmasını tooextend Swashbuckle toomake alternatiftir.</span><span class="sxs-lookup"><span data-stu-id="87142-116">hello alternative is tooextend Swashbuckle toomake it automatically generate unique operation ids.</span></span>

<span data-ttu-id="87142-117">Merhaba aşağıdaki adımları kullanarak Swashbuckle toocustomize nasıl hello Göster *SwaggerConfig.cs* hello Visual Studio API Apps Preview proje şablonu tarafından hello projeye dahil dosyası.</span><span class="sxs-lookup"><span data-stu-id="87142-117">hello following steps show how toocustomize Swashbuckle by using hello *SwaggerConfig.cs* file that is included in hello project by hello Visual Studio API Apps Preview project template.</span></span>  <span data-ttu-id="87142-118">Dağıtım bir API uygulaması olarak yapılandırdığınız bir Web API projesinde, Swashbuckle de özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87142-118">You can also customize Swashbuckle in a Web API project that you configure for deployment as an API app.</span></span>

1. <span data-ttu-id="87142-119">Bir özel Oluştur `IOperationFilter` uygulama</span><span class="sxs-lookup"><span data-stu-id="87142-119">Create a custom `IOperationFilter` implementation</span></span> 
   
    <span data-ttu-id="87142-120">Merhaba `IOperationFilter` arabirimi hello Swagger meta veri işlemi çeşitli yönlerini toocustomize istediğiniz Swashbuckle kullanıcılar için bir genişletilebilirlik noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="87142-120">hello `IOperationFilter` interface provides an extensibility point for Swashbuckle users who want toocustomize various aspects of hello Swagger metadata process.</span></span> <span data-ttu-id="87142-121">Hello aşağıdaki kodu hello işlemi kimliği oluşturma davranışı değiştirmenin bir yöntemi gösterir.</span><span class="sxs-lookup"><span data-stu-id="87142-121">hello following code demonstrates one method of changing hello operation-id-generation behavior.</span></span> <span data-ttu-id="87142-122">Merhaba kod parametre adları toohello işlem kimliği adı ekler.</span><span class="sxs-lookup"><span data-stu-id="87142-122">hello code appends parameter names toohello operation id name.</span></span>  
   
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
2. <span data-ttu-id="87142-123">İçinde *App_Start\SwaggerConfig.cs* dosyasını, arama hello `OperationFilter` yöntemi toocause Swashbuckle toouse hello yeni `IOperationFilter` uygulaması.</span><span class="sxs-lookup"><span data-stu-id="87142-123">In *App_Start\SwaggerConfig.cs* file, call hello `OperationFilter` method toocause Swashbuckle toouse hello new `IOperationFilter` implementation.</span></span>
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    <span data-ttu-id="87142-124">Merhaba *SwaggerConfig.cs* Swashbuckle NuGet paketi hello tarafından bırakılan dosyası genişletilebilirlik noktaları birçok kılınan örnekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="87142-124">hello *SwaggerConfig.cs* file that is dropped in by hello Swashbuckle NuGet package contains many commented-out examples of extensibility points.</span></span> <span data-ttu-id="87142-125">Merhaba ek açıklamalar burada gösterilmiyor.</span><span class="sxs-lookup"><span data-stu-id="87142-125">hello additional comments are not shown here.</span></span> 
   
    <span data-ttu-id="87142-126">Bu değişikliği yaptıktan sonra `IOperationFilter` uygulama kullanılır ve oluşturulan benzersiz işlem kimlikleri toobe neden olur.</span><span class="sxs-lookup"><span data-stu-id="87142-126">After you make this change, your `IOperationFilter` implementation is used and causes unique operation ids toobe generated.</span></span>
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a><span data-ttu-id="87142-127">Yanıt kodu 200 dışında izin ver</span><span class="sxs-lookup"><span data-stu-id="87142-127">Allow response codes other than 200</span></span>
<span data-ttu-id="87142-128">Varsayılan olarak, Swashbuckle bir HTTP 200 (Tamam) yanıt hello varsayar *yalnızca* yasal bir Web API yöntemi yanıtı.</span><span class="sxs-lookup"><span data-stu-id="87142-128">By default, Swashbuckle assumes that an HTTP 200 (OK) response is hello *only* legitimate response from a Web API method.</span></span> <span data-ttu-id="87142-129">Bazı durumlarda, bir özel durum hello istemci tooraise neden olmadan diğer yanıt kodları tooreturn isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87142-129">In some cases, you may want tooreturn other response codes without causing hello client tooraise an exception.</span></span>  <span data-ttu-id="87142-130">Örneğin, hello aşağıdaki Web API kodunda hello istemci tooaccept istersiniz bir senaryo bir 200 veya 404 yanıtı geçerli yanıtlarını olarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="87142-130">For example, hello following Web API code demonstrates a scenario in which you would want hello client tooaccept either a 200 or a 404 as valid responses.</span></span>

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

<span data-ttu-id="87142-131">Bu senaryoda, yalnızca bir meşru HTTP durum kodu, HTTP 200 hello Swashbuckle varsayılan olarak üretir Swagger belirtir.</span><span class="sxs-lookup"><span data-stu-id="87142-131">In this scenario, hello Swagger that Swashbuckle generates by default specifies only one legitimate HTTP status code, HTTP 200.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

<span data-ttu-id="87142-132">Visual Studio için hello istemci hello Swagger API tanımı toogenerate kod kullandığından, bir HTTP 200 dışındaki herhangi bir yanıt için bir özel durum başlatır istemci kodu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="87142-132">Since Visual Studio uses hello Swagger API definition toogenerate code for hello client, it creates client code that raises an exception for any response other than an HTTP 200.</span></span> <span data-ttu-id="87142-133">Bu örnek Web API yöntemi için oluşturulan bir C# istemci aşağıdaki Hello kodu arasındadır.</span><span class="sxs-lookup"><span data-stu-id="87142-133">hello code below is from a C# client generated for this sample Web API method.</span></span>

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

<span data-ttu-id="87142-134">Swashbuckle XML açıklamaları veya hello kullanarak bunu oluşturur, beklenen HTTP yanıt kodları hello listesi özelleştirme iki yolu sağlar `SwaggerResponse` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="87142-134">Swashbuckle provides two ways of customizing hello list of expected HTTP response codes that it generates, using XML comments or hello `SwaggerResponse` attribute.</span></span> <span data-ttu-id="87142-135">Merhaba özniteliği kolaydır, ancak yalnızca Swashbuckle 5.1.5 veya sonraki sürümlerinde.</span><span class="sxs-lookup"><span data-stu-id="87142-135">hello attribute is easier, but it is only available in Swashbuckle 5.1.5 or later.</span></span> <span data-ttu-id="87142-136">Merhaba API uygulamaları önizleme yeni proje şablonu Visual Studio 2013'te içerir Swashbuckle sürüm 5.0.0, hello şablon kullandı ve tooupdate Swashbuckle istemiyorsanız, tek seçeneğiniz toouse XML açıklamaları gelir.</span><span class="sxs-lookup"><span data-stu-id="87142-136">hello API Apps preview new-project template in Visual Studio 2013 includes Swashbuckle version 5.0.0, so if you used hello template and don't want tooupdate Swashbuckle, your only option is toouse XML comments.</span></span> 

### <a name="customize-expected-response-codes-using-xml-comments"></a><span data-ttu-id="87142-137">XML açıklamaları kullanarak beklenen yanıt kodlarını özelleştirme</span><span class="sxs-lookup"><span data-stu-id="87142-137">Customize expected response codes using XML comments</span></span>
<span data-ttu-id="87142-138">Swashbuckle sürümünüzü 5.1.5 önce ise, bu yöntemi toospecify yanıt kodlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="87142-138">Use this method toospecify response codes if your Swashbuckle version is earlier than 5.1.5.</span></span>

1. <span data-ttu-id="87142-139">İlk olarak, XML belge açıklamaları için HTTP yanıt kodları toospecify istediğiniz hello yöntemleri üzerinden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="87142-139">First, add XML documentation comments over hello methods you wish toospecify HTTP response codes for.</span></span> <span data-ttu-id="87142-140">Yukarıda gösterilen ve uygulama hello XML belgeleri tooit aşağıdaki örneğine hello gibi bir kod neden olacağından hello örnek Web API eylemi yapılıyor.</span><span class="sxs-lookup"><span data-stu-id="87142-140">Taking hello sample Web API action shown above and applying hello XML documentation tooit would result in code like hello following example.</span></span> 
   
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
2. <span data-ttu-id="87142-141">Yönergeler hello ekleyin *SwaggerConfig.cs* toodirect Swashbuckle toomake hello XML belge dosyası kullanımını dosya.</span><span class="sxs-lookup"><span data-stu-id="87142-141">Add instructions in hello *SwaggerConfig.cs* file toodirect Swashbuckle toomake use of hello XML documentation file.</span></span>
   
   * <span data-ttu-id="87142-142">Açık *SwaggerConfig.cs* ve hello üzerinde bir yöntem oluşturma *SwaggerConfig* sınıfı toospecify hello yolu toohello belge XML dosyası.</span><span class="sxs-lookup"><span data-stu-id="87142-142">Open *SwaggerConfig.cs* and create a method on hello *SwaggerConfig* class toospecify hello path toohello documentation XML file.</span></span> 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * <span data-ttu-id="87142-143">Aşağı kaydırın hello *SwaggerConfig.cs* hello kılınan kod satırı, aşağıda gösterilen hello ekran benzeyen görene kadar dosya.</span><span class="sxs-lookup"><span data-stu-id="87142-143">Scroll down in hello *SwaggerConfig.cs* file until you see hello commented-out line of code resembling hello screen shot below.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * <span data-ttu-id="87142-144">Swagger oluşturma sırasında işleme hello satır tooenable hello XML açıklamaları açıklamadan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="87142-144">Uncomment hello line tooenable hello XML comments processing during Swagger generation.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. <span data-ttu-id="87142-145">Sipariş toogenerate hello XML belge dosyası, hello projenin özelliklerine gidin ve aşağıdaki hello ekran görüntüsünde gösterildiği gibi hello XML belge dosyası etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="87142-145">In order toogenerate hello XML documentation file, go into hello project's properties and enable hello XML documentation file as shown in hello screenshot below.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

<span data-ttu-id="87142-146">Bu adımları gerçekleştirdikten sonra hello Swagger JSON Swashbuckle tarafından oluşturulan hello XML açıklamaları belirtilen hello HTTP yanıt kodları yansıtır.</span><span class="sxs-lookup"><span data-stu-id="87142-146">Once you perform these steps, hello Swagger JSON generated by Swashbuckle will reflect hello HTTP response codes that you specified in hello XML comments.</span></span> <span data-ttu-id="87142-147">Bu yeni JSON yükü Hello ekran görüntüsü aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="87142-147">hello screenshot below demonstrates this new JSON payload.</span></span> 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

<span data-ttu-id="87142-148">REST API için Visual Studio tooregenerate hello istemci kodu kullandığınızda, hello C# kodu her iki hello HTTP Tamam ve bulunamadı durum kodları toohandle Merhaba null dönüş nasıl üzerinde kullanıcı kodu toomake kararlarınızı izin vererek, bir özel durum yükseltmeden kabul eder Kayıt başvurun.</span><span class="sxs-lookup"><span data-stu-id="87142-148">When you use Visual Studio tooregenerate hello client code for your REST API, hello C# code accepts both hello HTTP OK and Not Found status codes without raising an exception, allowing your consuming code toomake decisions on how toohandle hello return of a null Contact record.</span></span> 

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

<span data-ttu-id="87142-149">Bu Tanıtım için Hello kod bulunabilir [bu GitHub deposunu](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse).</span><span class="sxs-lookup"><span data-stu-id="87142-149">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse).</span></span> <span data-ttu-id="87142-150">Web API Hello yanı sıra ile XML belgeleri yorumları artırıldığında bu API için oluşturulan istemci içeren bir konsol uygulama projesi projesidir.</span><span class="sxs-lookup"><span data-stu-id="87142-150">Along with hello Web API project marked up with XML documentation comments is a Console Application project that contains a generated client for this API.</span></span> 

### <a name="customize-expected-response-codes-using-hello-swaggerresponse-attribute"></a><span data-ttu-id="87142-151">Merhaba SwaggerResponse özniteliğini kullanarak beklenen yanıt kodlarını Özelleştir</span><span class="sxs-lookup"><span data-stu-id="87142-151">Customize expected response codes using hello SwaggerResponse attribute</span></span>
<span data-ttu-id="87142-152">Merhaba [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) özniteliktir ve sonrasında Swashbuckle 5.1.5 içinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="87142-152">hello [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) attribute is available in Swashbuckle 5.1.5 and later.</span></span> <span data-ttu-id="87142-153">Projenizde önceki bir sürümü yüklü durumda, bu bölümde nasıl tooupdate hello Swashbuckle NuGet paketini bu öznitelik kullanabilmesi için açıklayarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="87142-153">In case you have an earlier version in your project, this section starts by explaining how tooupdate hello Swashbuckle NuGet package so that you can use this attribute.</span></span>

1. <span data-ttu-id="87142-154">İçinde **Çözüm Gezgini**, Web API projenize sağ tıklatın ve **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="87142-154">In **Solution Explorer**, right-click your Web API project and click **Manage NuGet Packages**.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. <span data-ttu-id="87142-155">Merhaba tıklatın *güncelleştirme* düğmesine bir sonraki toohello *Swashbuckle* NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="87142-155">Click hello *Update* button next toohello *Swashbuckle* NuGet package.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. <span data-ttu-id="87142-156">Merhaba eklemek *SwaggerResponse* toohello Web API eylem yöntemleri toospecify geçerli HTTP yanıtı kodları istediğiniz öznitelikler.</span><span class="sxs-lookup"><span data-stu-id="87142-156">Add hello *SwaggerResponse* attributes toohello Web API action methods for which you want toospecify valid HTTP response codes.</span></span> 
   
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
4. <span data-ttu-id="87142-157">Ekleme bir `using` hello özniteliğin ad alanı bildirimi:</span><span class="sxs-lookup"><span data-stu-id="87142-157">Add a `using` statement for hello attribute's namespace:</span></span>
   
        using Swashbuckle.Swagger.Annotations;
5. <span data-ttu-id="87142-158">Toohello Gözat */swagger/docs/v1* hello çeşitli HTTP yanıt kodları görünür durumda olur ve proje URL'sini hello Swagger JSON.</span><span class="sxs-lookup"><span data-stu-id="87142-158">Browse toohello */swagger/docs/v1* URL of your project and hello various HTTP response codes will be visible in hello Swagger JSON.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

<span data-ttu-id="87142-159">Bu Tanıtım için Hello kod bulunabilir [bu GitHub deposunu](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes).</span><span class="sxs-lookup"><span data-stu-id="87142-159">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes).</span></span> <span data-ttu-id="87142-160">Merhaba birlikte Web API projesi hello ile donatılmış *SwaggerResponse* bu API için oluşturulan istemci içeren bir konsol uygulama projesi bir özniteliktir.</span><span class="sxs-lookup"><span data-stu-id="87142-160">Along with hello Web API project decorated with hello *SwaggerResponse* attribute is a Console Application project that contains a generated client for this API.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="87142-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="87142-161">Next steps</span></span>
<span data-ttu-id="87142-162">Bu makalede, işlem kimlikleri ve geçerli yanıt kodları toocustomize hello yolu Swashbuckle nasıl oluşturur göstermiştir.</span><span class="sxs-lookup"><span data-stu-id="87142-162">This article has shown how toocustomize hello way Swashbuckle generates operation ids and valid response codes.</span></span> <span data-ttu-id="87142-163">Daha fazla bilgi için bkz: [github'da Swashbuckle](https://github.com/domaindrivendev/Swashbuckle).</span><span class="sxs-lookup"><span data-stu-id="87142-163">For more information, see [Swashbuckle on GitHub](https://github.com/domaindrivendev/Swashbuckle).</span></span>

