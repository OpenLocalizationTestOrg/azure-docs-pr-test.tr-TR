---
title: "aaaException Yönetimi - Microsoft tehdit modelleme aracı - Azure | Microsoft Docs"
description: "Azaltıcı Etkenler hello tehdit modelleme Aracı kullanıma sunulan tehditleri"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 247096c10deeca94ebb9b19df7ba60e442ca1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-exception-management--mitigations"></a><span data-ttu-id="87115-103">Güvenlik çerçevesi: Özel durum yönetimi | Azaltıcı Etkenler</span><span class="sxs-lookup"><span data-stu-id="87115-103">Security Frame: Exception Management | Mitigations</span></span> 
| <span data-ttu-id="87115-104">Ürün/hizmet</span><span class="sxs-lookup"><span data-stu-id="87115-104">Product/Service</span></span> | <span data-ttu-id="87115-105">Makale</span><span class="sxs-lookup"><span data-stu-id="87115-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="87115-106">**WCF**</span><span class="sxs-lookup"><span data-stu-id="87115-106">**WCF**</span></span> | <ul><li>[<span data-ttu-id="87115-107">WCF - dahil etmeyin serviceDebug düğümü yapılandırma dosyasında</span><span class="sxs-lookup"><span data-stu-id="87115-107">WCF- Do not include serviceDebug node in configuration file</span></span>](#servicedebug)</li><li>[<span data-ttu-id="87115-108">WCF - dahil etmeyin serviceMetadata düğümü yapılandırma dosyasında</span><span class="sxs-lookup"><span data-stu-id="87115-108">WCF- Do not include serviceMetadata node in configuration file</span></span>](#servicemetadata)</li></ul> |
| <span data-ttu-id="87115-109">**Web API**</span><span class="sxs-lookup"><span data-stu-id="87115-109">**Web API**</span></span> | <ul><li>[<span data-ttu-id="87115-110">ASP.NET Web API'de uygun özel durum işleme yapıldığından emin olun</span><span class="sxs-lookup"><span data-stu-id="87115-110">Ensure that proper exception handling is done in ASP.NET Web API </span></span>](#exception)</li></ul> |
| <span data-ttu-id="87115-111">**Web uygulaması**</span><span class="sxs-lookup"><span data-stu-id="87115-111">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="87115-112">Hata iletileri güvenlik ayrıntıları gösterme</span><span class="sxs-lookup"><span data-stu-id="87115-112">Do not expose security details in error messages </span></span>](#messages)</li><li>[<span data-ttu-id="87115-113">Varsayılan hata sayfası işleme uygulama</span><span class="sxs-lookup"><span data-stu-id="87115-113">Implement Default error handling page </span></span>](#default)</li><li>[<span data-ttu-id="87115-114">IIS dağıtım yöntemini tooRetail ayarlayın</span><span class="sxs-lookup"><span data-stu-id="87115-114">Set Deployment Method tooRetail in IIS</span></span>](#deployment)</li><li>[<span data-ttu-id="87115-115">Özel durumlar güvenli bir şekilde başarısız olması</span><span class="sxs-lookup"><span data-stu-id="87115-115">Exceptions should fail safely</span></span>](#fail)</li></ul> |

## <span data-ttu-id="87115-116"><a id="servicedebug"></a>WCF - dahil etmeyin serviceDebug düğümü yapılandırma dosyasında</span><span class="sxs-lookup"><span data-stu-id="87115-116"><a id="servicedebug"></a>WCF- Do not include serviceDebug node in configuration file</span></span>

| <span data-ttu-id="87115-117">Başlık</span><span class="sxs-lookup"><span data-stu-id="87115-117">Title</span></span>                   | <span data-ttu-id="87115-118">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="87115-118">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="87115-119">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="87115-119">**Component**</span></span>               | <span data-ttu-id="87115-120">WCF</span><span class="sxs-lookup"><span data-stu-id="87115-120">WCF</span></span> | 
| <span data-ttu-id="87115-121">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="87115-121">**SDL Phase**</span></span>               | <span data-ttu-id="87115-122">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="87115-122">Build</span></span> |  
| <span data-ttu-id="87115-123">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="87115-123">**Applicable Technologies**</span></span> | <span data-ttu-id="87115-124">Genel, NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="87115-124">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="87115-125">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="87115-125">**Attributes**</span></span>              | <span data-ttu-id="87115-126">Yok</span><span class="sxs-lookup"><span data-stu-id="87115-126">N/A</span></span>  |
| <span data-ttu-id="87115-127">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="87115-127">**References**</span></span>              | <span data-ttu-id="87115-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Krallık Fortify](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="87115-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="87115-129">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="87115-129">**Steps**</span></span> | <span data-ttu-id="87115-130">Windows Communication Framework (WCF) hizmetlerini hata ayıklama bilgileri yapılandırılmış tooexpose olabilir.</span><span class="sxs-lookup"><span data-stu-id="87115-130">Windows Communication Framework (WCF) services can be configured tooexpose debugging information.</span></span> <span data-ttu-id="87115-131">Hata ayıklama bilgileri üretim ortamlarında kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="87115-131">Debug information should not be used in production environments.</span></span> <span data-ttu-id="87115-132">Merhaba `<serviceDebug>` etiketi hello hata ayıklama bilgileri özelliği için bir WCF hizmeti etkin olup olmadığını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="87115-132">hello `<serviceDebug>` tag defines whether hello debug information feature is enabled for a WCF service.</span></span> <span data-ttu-id="87115-133">Merhaba özniteliği IncludeExceptionDetailInFaults tootrue ayarlarsanız, özel durum bilgilerini hello uygulamasından tooclients döndürülür.</span><span class="sxs-lookup"><span data-stu-id="87115-133">If hello attribute includeExceptionDetailInFaults is set tootrue, exception information from hello application will be returned tooclients.</span></span> <span data-ttu-id="87115-134">Saldırganlar hello ek bilgi hedeflenen çıktı toomount saldırılar hello framework, veritabanı veya hello uygulama tarafından kullanılan kaynaklar hata ayıklama elde yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87115-134">Attackers can leverage hello additional information they gain from debugging output toomount attacks targeted on hello framework, database, or other resources used by hello application.</span></span> |

### <a name="example"></a><span data-ttu-id="87115-135">Örnek</span><span class="sxs-lookup"><span data-stu-id="87115-135">Example</span></span>
<span data-ttu-id="87115-136">Merhaba aşağıdaki yapılandırma dosyası içerir hello `<serviceDebug>` etiketi:</span><span class="sxs-lookup"><span data-stu-id="87115-136">hello following configuration file includes hello `<serviceDebug>` tag:</span></span> 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
<span data-ttu-id="87115-137">Merhaba hizmetinde hata ayıklama bilgilerini devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="87115-137">Disable debugging information in hello service.</span></span> <span data-ttu-id="87115-138">Bu hello kaldırarak gerçekleştirilebilir `<serviceDebug>` , uygulamanızın yapılandırma dosyasından etiketi.</span><span class="sxs-lookup"><span data-stu-id="87115-138">This can be accomplished by removing hello `<serviceDebug>` tag from your application's configuration file.</span></span> 

## <span data-ttu-id="87115-139"><a id="servicemetadata"></a>WCF - dahil etmeyin serviceMetadata düğümü yapılandırma dosyasında</span><span class="sxs-lookup"><span data-stu-id="87115-139"><a id="servicemetadata"></a>WCF- Do not include serviceMetadata node in configuration file</span></span>

| <span data-ttu-id="87115-140">Başlık</span><span class="sxs-lookup"><span data-stu-id="87115-140">Title</span></span>                   | <span data-ttu-id="87115-141">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="87115-141">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="87115-142">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="87115-142">**Component**</span></span>               | <span data-ttu-id="87115-143">WCF</span><span class="sxs-lookup"><span data-stu-id="87115-143">WCF</span></span> | 
| <span data-ttu-id="87115-144">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="87115-144">**SDL Phase**</span></span>               | <span data-ttu-id="87115-145">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="87115-145">Build</span></span> |  
| <span data-ttu-id="87115-146">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="87115-146">**Applicable Technologies**</span></span> | <span data-ttu-id="87115-147">Genel</span><span class="sxs-lookup"><span data-stu-id="87115-147">Generic</span></span> |
| <span data-ttu-id="87115-148">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="87115-148">**Attributes**</span></span>              | <span data-ttu-id="87115-149">Genel, NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="87115-149">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="87115-150">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="87115-150">**References**</span></span>              | <span data-ttu-id="87115-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Krallık Fortify](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="87115-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="87115-152">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="87115-152">**Steps**</span></span> | <span data-ttu-id="87115-153">Genel olarak bir hizmet hakkında bilgileri gösterme nasıl hello hizmet yararlanabilir içine değerli bilgiler da sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="87115-153">Publicly exposing information about a service can provide attackers with valuable insight into how they might exploit hello service.</span></span> <span data-ttu-id="87115-154">Merhaba `<serviceMetadata>` etiketi hello meta veri yayımlama özelliğini etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="87115-154">hello `<serviceMetadata>` tag enables hello metadata publishing feature.</span></span> <span data-ttu-id="87115-155">Hizmet meta verileri genel olarak erişilebilir olmamalıdır hassas bilgiler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="87115-155">Service metadata could contain sensitive information that should not be publicly accessible.</span></span> <span data-ttu-id="87115-156">En azından, yalnızca güvenilen kullanıcıların tooaccess meta verileri hello ve bilgileri gereksiz sunulmaz olun izin verir.</span><span class="sxs-lookup"><span data-stu-id="87115-156">At a minimum, only allow trusted users tooaccess hello metadata and ensure that unnecessary information is not exposed.</span></span> <span data-ttu-id="87115-157">Daha iyi bir yöntem tamamen hello özelliği toopublish meta verileri devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="87115-157">Better yet, entirely disable hello ability toopublish metadata.</span></span> <span data-ttu-id="87115-158">Güvenli bir WCF yapılandırma hello içermeyecek `<serviceMetadata>` etiketi.</span><span class="sxs-lookup"><span data-stu-id="87115-158">A safe WCF configuration will not contain hello `<serviceMetadata>` tag.</span></span> |

## <span data-ttu-id="87115-159"><a id="exception"></a>ASP.NET Web API'de uygun özel durum işleme yapıldığından emin olun</span><span class="sxs-lookup"><span data-stu-id="87115-159"><a id="exception"></a>Ensure that proper exception handling is done in ASP.NET Web API</span></span>

| <span data-ttu-id="87115-160">Başlık</span><span class="sxs-lookup"><span data-stu-id="87115-160">Title</span></span>                   | <span data-ttu-id="87115-161">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="87115-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="87115-162">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="87115-162">**Component**</span></span>               | <span data-ttu-id="87115-163">Web API</span><span class="sxs-lookup"><span data-stu-id="87115-163">Web API</span></span> | 
| <span data-ttu-id="87115-164">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="87115-164">**SDL Phase**</span></span>               | <span data-ttu-id="87115-165">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="87115-165">Build</span></span> |  
| <span data-ttu-id="87115-166">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="87115-166">**Applicable Technologies**</span></span> | <span data-ttu-id="87115-167">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="87115-167">MVC 5, MVC 6</span></span> |
| <span data-ttu-id="87115-168">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="87115-168">**Attributes**</span></span>              | <span data-ttu-id="87115-169">Yok</span><span class="sxs-lookup"><span data-stu-id="87115-169">N/A</span></span>  |
| <span data-ttu-id="87115-170">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="87115-170">**References**</span></span>              | <span data-ttu-id="87115-171">[Özel durum işleme ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model ASP.NET Web API doğrulama](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span><span class="sxs-lookup"><span data-stu-id="87115-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span></span> |
| <span data-ttu-id="87115-172">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="87115-172">**Steps**</span></span> | <span data-ttu-id="87115-173">Bir HTTP yanıtının durum koduyla içine çevrilen varsayılan olarak, ASP.NET Web API en Yakalanmayan Özel durumları`500, Internal Server Error`</span><span class="sxs-lookup"><span data-stu-id="87115-173">By default, most uncaught exceptions in ASP.NET Web API are translated into an HTTP response with status code `500, Internal Server Error`</span></span>|

### <a name="example"></a><span data-ttu-id="87115-174">Örnek</span><span class="sxs-lookup"><span data-stu-id="87115-174">Example</span></span>
<span data-ttu-id="87115-175">Merhaba API tarafından döndürülen toocontrol hello durum kodu `HttpResponseException` aşağıda gösterildiği gibi kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="87115-175">toocontrol hello status code returned by hello API, `HttpResponseException` can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        throw new HttpResponseException(HttpStatusCode.NotFound);
    }
    return item;
}
```

### <a name="example"></a><span data-ttu-id="87115-176">Örnek</span><span class="sxs-lookup"><span data-stu-id="87115-176">Example</span></span>
<span data-ttu-id="87115-177">Merhaba özel durum yanıt üzerinde daha fazla denetlemek için hello `HttpResponseMessage` aşağıda gösterildiği gibi sınıfı kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="87115-177">For further control on hello exception response, hello `HttpResponseMessage` class can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        var resp = new HttpResponseMessage(HttpStatusCode.NotFound)
        {
            Content = new StringContent(string.Format("No product with ID = {0}", id)),
            ReasonPhrase = "Product ID Not Found"
        }
        throw new HttpResponseException(resp);
    }
    return item;
}
```
<span data-ttu-id="87115-178">toocatch işlenmemiş hello türünde olmayan özel durumları `HttpResponseException`, özel durum filtreleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="87115-178">toocatch unhandled exceptions that are not of hello type `HttpResponseException`, Exception Filters can be used.</span></span> <span data-ttu-id="87115-179">Özel durum filtreleri uygulamak hello `System.Web.Http.Filters.IExceptionFilter` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="87115-179">Exception filters implement hello `System.Web.Http.Filters.IExceptionFilter` interface.</span></span> <span data-ttu-id="87115-180">Merhaba en basit yolu toowrite bir özel durum filtresi olduğu hello gelen tooderive `System.Web.Http.Filters.ExceptionFilterAttribute` sınıfı ve hello OnException yöntemini geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="87115-180">hello simplest way toowrite an exception filter is tooderive from hello `System.Web.Http.Filters.ExceptionFilterAttribute` class and override hello OnException method.</span></span> 

### <a name="example"></a><span data-ttu-id="87115-181">Örnek</span><span class="sxs-lookup"><span data-stu-id="87115-181">Example</span></span>
<span data-ttu-id="87115-182">Dönüştüren bir filtre işte `NotImplementedException` özel durumlar HTTP durum kodu içine `501, Not Implemented`:</span><span class="sxs-lookup"><span data-stu-id="87115-182">Here is a filter that converts `NotImplementedException` exceptions into HTTP status code `501, Not Implemented`:</span></span> 
```C#
namespace ProductStore.Filters
{
    using System;
    using System.Net;
    using System.Net.Http;
    using System.Web.Http.Filters;

    public class NotImplExceptionFilterAttribute : ExceptionFilterAttribute 
    {
        public override void OnException(HttpActionExecutedContext context)
        {
            if (context.Exception is NotImplementedException)
            {
                context.Response = new HttpResponseMessage(HttpStatusCode.NotImplemented);
            }
        }
    }
}
```

<span data-ttu-id="87115-183">Çeşitli yolları tooregister bir Web API özel durum filtresi vardır:</span><span class="sxs-lookup"><span data-stu-id="87115-183">There are several ways tooregister a Web API exception filter:</span></span>
- <span data-ttu-id="87115-184">Eylem tarafından</span><span class="sxs-lookup"><span data-stu-id="87115-184">By action</span></span>
- <span data-ttu-id="87115-185">Denetleyici tarafından</span><span class="sxs-lookup"><span data-stu-id="87115-185">By controller</span></span>
- <span data-ttu-id="87115-186">Genel</span><span class="sxs-lookup"><span data-stu-id="87115-186">Globally</span></span>

### <a name="example"></a><span data-ttu-id="87115-187">Örnek</span><span class="sxs-lookup"><span data-stu-id="87115-187">Example</span></span>
<span data-ttu-id="87115-188">tooapply hello filtre tooa belirli bir eylemi, hello filtre özniteliği toohello Eylem Ekle:</span><span class="sxs-lookup"><span data-stu-id="87115-188">tooapply hello filter tooa specific action, add hello filter as an attribute toohello action:</span></span> 
```C#
public class ProductsController : ApiController
{
    [NotImplExceptionFilter]
    public Contact GetContact(int id)
    {
        throw new NotImplementedException("This method is not implemented");
    }
}
```
### <a name="example"></a><span data-ttu-id="87115-189">Örnek</span><span class="sxs-lookup"><span data-stu-id="87115-189">Example</span></span>
<span data-ttu-id="87115-190">tooapply hello filtre tooall hello eylemleri bir `controller`, bir öznitelik toohello hello filtre eklemek `controller` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="87115-190">tooapply hello filter tooall of hello actions on a `controller`, add hello filter as an attribute toohello `controller` class:</span></span> 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a><span data-ttu-id="87115-191">Örnek</span><span class="sxs-lookup"><span data-stu-id="87115-191">Example</span></span>
<span data-ttu-id="87115-192">tooapply hello tooall Web API denetleyicilerinin genel filtre, hello filtre toohello bir örnek ekler `GlobalConfiguration.Configuration.Filters` koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="87115-192">tooapply hello filter globally tooall Web API controllers, add an instance of hello filter toohello `GlobalConfiguration.Configuration.Filters` collection.</span></span> <span data-ttu-id="87115-193">Özel durum filtreleri bu koleksiyonda tooany Web API denetleyici eylemi uygular.</span><span class="sxs-lookup"><span data-stu-id="87115-193">Exception filters in this collection apply tooany Web API controller action.</span></span> 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a><span data-ttu-id="87115-194">Örnek</span><span class="sxs-lookup"><span data-stu-id="87115-194">Example</span></span>
<span data-ttu-id="87115-195">Model doğrulama için aşağıda gösterildiği gibi tooCreateErrorResponse yöntemi hello model durumu geçirilebilir:</span><span class="sxs-lookup"><span data-stu-id="87115-195">For model validation, hello model state can be passed tooCreateErrorResponse method as shown below:</span></span> 
```C#
public HttpResponseMessage PostProduct(Product item)
{
    if (!ModelState.IsValid)
    {
        return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
    }
    // Implementation not shown...
}
```

<span data-ttu-id="87115-196">Olağanüstü işleme ve ASP.Net Web API model doğrulama hakkında ek ayrıntılar için hello başvuruları bölümdeki onay hello bağlantılar</span><span class="sxs-lookup"><span data-stu-id="87115-196">Check hello links in hello references section for additional details about exceptional handling and model validation in ASP.Net Web API</span></span> 

## <span data-ttu-id="87115-197"><a id="messages"></a>Hata iletileri güvenlik ayrıntıları gösterme</span><span class="sxs-lookup"><span data-stu-id="87115-197"><a id="messages"></a>Do not expose security details in error messages</span></span>

| <span data-ttu-id="87115-198">Başlık</span><span class="sxs-lookup"><span data-stu-id="87115-198">Title</span></span>                   | <span data-ttu-id="87115-199">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="87115-199">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="87115-200">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="87115-200">**Component**</span></span>               | <span data-ttu-id="87115-201">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="87115-201">Web Application</span></span> | 
| <span data-ttu-id="87115-202">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="87115-202">**SDL Phase**</span></span>               | <span data-ttu-id="87115-203">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="87115-203">Build</span></span> |  
| <span data-ttu-id="87115-204">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="87115-204">**Applicable Technologies**</span></span> | <span data-ttu-id="87115-205">Genel</span><span class="sxs-lookup"><span data-stu-id="87115-205">Generic</span></span> |
| <span data-ttu-id="87115-206">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="87115-206">**Attributes**</span></span>              | <span data-ttu-id="87115-207">Yok</span><span class="sxs-lookup"><span data-stu-id="87115-207">N/A</span></span>  |
| <span data-ttu-id="87115-208">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="87115-208">**References**</span></span>              | <span data-ttu-id="87115-209">Yok</span><span class="sxs-lookup"><span data-stu-id="87115-209">N/A</span></span>  |
| <span data-ttu-id="87115-210">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="87115-210">**Steps**</span></span> | <p><span data-ttu-id="87115-211">Genel hata iletileri, önemli uygulama verileri dahil olmak üzere olmadan toohello kullanıcı doğrudan sağlanır.</span><span class="sxs-lookup"><span data-stu-id="87115-211">Generic error messages are provided directly toohello user without including sensitive application data.</span></span> <span data-ttu-id="87115-212">Gizli verilerin örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="87115-212">Examples of sensitive data include:</span></span></p><ul><li><span data-ttu-id="87115-213">Sunucu adları</span><span class="sxs-lookup"><span data-stu-id="87115-213">Server names</span></span></li><li><span data-ttu-id="87115-214">Bağlantı dizeleri</span><span class="sxs-lookup"><span data-stu-id="87115-214">Connection strings</span></span></li><li><span data-ttu-id="87115-215">Kullanıcı adları</span><span class="sxs-lookup"><span data-stu-id="87115-215">Usernames</span></span></li><li><span data-ttu-id="87115-216">Parolaları</span><span class="sxs-lookup"><span data-stu-id="87115-216">Passwords</span></span></li><li><span data-ttu-id="87115-217">SQL yordamları</span><span class="sxs-lookup"><span data-stu-id="87115-217">SQL procedures</span></span></li><li><span data-ttu-id="87115-218">Dinamik SQL hatalarının ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="87115-218">Details of dynamic SQL failures</span></span></li><li><span data-ttu-id="87115-219">Yığın izleme ve kod satırları</span><span class="sxs-lookup"><span data-stu-id="87115-219">Stack trace and lines of code</span></span></li><li><span data-ttu-id="87115-220">Bellekte depolanan değişkenleri</span><span class="sxs-lookup"><span data-stu-id="87115-220">Variables stored in memory</span></span></li><li><span data-ttu-id="87115-221">Sürücü ve klasör konumları</span><span class="sxs-lookup"><span data-stu-id="87115-221">Drive and folder locations</span></span></li><li><span data-ttu-id="87115-222">Uygulama yükleme noktaları</span><span class="sxs-lookup"><span data-stu-id="87115-222">Application install points</span></span></li><li><span data-ttu-id="87115-223">Ana bilgisayar yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="87115-223">Host configuration settings</span></span></li><li><span data-ttu-id="87115-224">Diğer iç uygulama ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="87115-224">Other internal application details</span></span></li></ul><p><span data-ttu-id="87115-225">Bir uygulamadaki tüm hataları yakalama ve genel hata iletileri sağlayarak, yanı sıra IIS içinde özel hatalar etkinleştirme bilgilerin açığa çıkmasına engellemeye yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="87115-225">Trapping all errors within an application and providing generic error messages, as well as enabling custom errors within IIS will help prevent information disclosure.</span></span> <span data-ttu-id="87115-226">SQL Server veritabanı ve .NET özel durum işleme, diğer hata mimarileri işleme arasında özellikle ayrıntılı ve son derece kullanışlı tooa kötü amaçlı kullanıcı uygulamanızı profil var.</span><span class="sxs-lookup"><span data-stu-id="87115-226">SQL Server database and .NET Exception handling, among other error handling architectures, are especially verbose and extremely useful tooa malicious user profiling your application.</span></span> <span data-ttu-id="87115-227">Bir sınıf içeriğini hello .NET özel durum sınıfından türetilen ve böylece beklenmeyen bir özel durum yanlışlıkla değil uygun özel durum işleme sahip olduğundan emin olun görüntü hello doğrudan toohello kullanıcı gerçekleşmedi doğrudan yapın.</span><span class="sxs-lookup"><span data-stu-id="87115-227">Do not directly display hello contents of a class derived from hello .NET Exception class, and ensure that you have proper exception handling so that an unexpected exception isn't inadvertently raised directly toohello user.</span></span></p><ul><li><span data-ttu-id="87115-228">Genel hata doğrudan doğrudan hello özel durum/hata iletisi bulundu koyma belirli Ayrıntılar soyut toohello kullanıcı iletileri sağlayın</span><span class="sxs-lookup"><span data-stu-id="87115-228">Provide generic error messages directly toohello user that abstract away specific details found directly in hello exception/error message</span></span></li><li><span data-ttu-id="87115-229">Değil görüntü hello içeriğini bir .NET özel doğrudan toohello kullanıcı sınıfı</span><span class="sxs-lookup"><span data-stu-id="87115-229">Do not display hello contents of a .NET exception class directly toohello user</span></span></li><li><span data-ttu-id="87115-230">Tüm hata iletilerini yakalayabilir ve uygunsa hello kullanıcıyı bir genel hata iletisini gönderilen toohello uygulama istemci yoluyla bildirin.</span><span class="sxs-lookup"><span data-stu-id="87115-230">Trap all error messages and if appropriate inform hello user via a generic error message sent toohello application client</span></span></li><li><span data-ttu-id="87115-231">Özellikle hello toohello kullanıcı dönüş doğrudan değerinden hello özel durum sınıfı hello içeriğini gösterme `.ToString()`, veya hello ileti veya StackTrace özelliklerinin hello değerleri.</span><span class="sxs-lookup"><span data-stu-id="87115-231">Do not expose hello contents of hello Exception class directly toohello user, especially hello return value from `.ToString()`, or hello values of hello Message or StackTrace properties.</span></span> <span data-ttu-id="87115-232">Güvenli bir şekilde bu bilgilerini günlüğe kaydetme ve daha zararsız ileti toohello kullanıcı görüntüleme</span><span class="sxs-lookup"><span data-stu-id="87115-232">Securely log this information and display a more innocuous message toohello user</span></span></li></ul>|

## <span data-ttu-id="87115-233"><a id="default"></a>Varsayılan hata sayfası işleme uygulama</span><span class="sxs-lookup"><span data-stu-id="87115-233"><a id="default"></a>Implement Default error handling page</span></span>

| <span data-ttu-id="87115-234">Başlık</span><span class="sxs-lookup"><span data-stu-id="87115-234">Title</span></span>                   | <span data-ttu-id="87115-235">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="87115-235">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="87115-236">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="87115-236">**Component**</span></span>               | <span data-ttu-id="87115-237">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="87115-237">Web Application</span></span> | 
| <span data-ttu-id="87115-238">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="87115-238">**SDL Phase**</span></span>               | <span data-ttu-id="87115-239">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="87115-239">Build</span></span> |  
| <span data-ttu-id="87115-240">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="87115-240">**Applicable Technologies**</span></span> | <span data-ttu-id="87115-241">Genel</span><span class="sxs-lookup"><span data-stu-id="87115-241">Generic</span></span> |
| <span data-ttu-id="87115-242">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="87115-242">**Attributes**</span></span>              | <span data-ttu-id="87115-243">Yok</span><span class="sxs-lookup"><span data-stu-id="87115-243">N/A</span></span>  |
| <span data-ttu-id="87115-244">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="87115-244">**References**</span></span>              | <span data-ttu-id="87115-245">[ASP.NET hata sayfası ayarlarını Düzenle iletişim kutusu](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="87115-245">[Edit ASP.NET Error Pages Settings Dialog Box](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span></span> |
| <span data-ttu-id="87115-246">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="87115-246">**Steps**</span></span> | <p><span data-ttu-id="87115-247">Bir ASP.NET uygulaması başarısız olur ve bir HTTP/1.x 500 İç sunucu hatası neden olan veya bir özellik yapılandırması (istek filtreleme gibi) bir sayfa görüntülenmesini engeller, bir hata iletisi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="87115-247">When an ASP.NET application fails and causes an HTTP/1.x 500 Internal Server Error, or a feature configuration (such as Request Filtering) prevents a page from being displayed, an error message will be generated.</span></span> <span data-ttu-id="87115-248">Yöneticiler, kolay iletisi toohello istemci, ayrıntılı hata iletisi toohello istemci ya da yalnızca ayrıntılı hata iletisi toolocalhost Merhaba uygulaması görüntülenmelidir olsun veya olmasın seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87115-248">Administrators can choose whether or not hello application should display a friendly message toohello client, detailed error message toohello client, or detailed error message toolocalhost only.</span></span> <span data-ttu-id="87115-249">Merhaba <customErrors> hello web.config etiketinde üç modu vardır:</span><span class="sxs-lookup"><span data-stu-id="87115-249">hello <customErrors> tag in hello web.config has three modes:</span></span></p><ul><li><span data-ttu-id="87115-250">**Üzerinde:** özel hatalar etkin olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="87115-250">**On:** Specifies that custom errors are enabled.</span></span> <span data-ttu-id="87115-251">Hiçbir defaultRedirect özniteliği belirtilmezse, kullanıcılar genel bir hata görür.</span><span class="sxs-lookup"><span data-stu-id="87115-251">If no defaultRedirect attribute is specified, users see a generic error.</span></span> <span data-ttu-id="87115-252">Merhaba özel hatalar toohello uzak istemciler ve toohello yerel konak gösterilir</span><span class="sxs-lookup"><span data-stu-id="87115-252">hello custom errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="87115-253">**Kapalı:** özel hatalar devre dışı olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="87115-253">**Off:** Specifies that custom errors are disabled.</span></span> <span data-ttu-id="87115-254">Merhaba ayrıntılı ASP.NET hataları toohello uzak istemciler ve toohello yerel konak gösterilir</span><span class="sxs-lookup"><span data-stu-id="87115-254">hello detailed ASP.NET errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="87115-255">**RemoteOnly:** özel hatalar yalnızca toohello uzak istemciler gösterilir ve ASP.NET hatalarının toohello yerel ana görüntüleneceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="87115-255">**RemoteOnly:** Specifies that custom errors are shown only toohello remote clients, and that ASP.NET errors are shown toohello local host.</span></span> <span data-ttu-id="87115-256">Bu hello varsayılan değerdir</span><span class="sxs-lookup"><span data-stu-id="87115-256">This is hello default value</span></span></li></ul><p><span data-ttu-id="87115-257">Açık hello `web.config` hello uygulama/sitesi için dosya ve hello etiketi ya da sahip olduğundan emin olun `<customErrors mode="RemoteOnly" />` veya `<customErrors mode="On" />` tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="87115-257">Open hello `web.config` file for hello application/site and ensure that hello tag has either `<customErrors mode="RemoteOnly" />` or `<customErrors mode="On" />` defined.</span></span></p>|

## <span data-ttu-id="87115-258"><a id="deployment"></a>IIS dağıtım yöntemini tooRetail ayarlayın</span><span class="sxs-lookup"><span data-stu-id="87115-258"><a id="deployment"></a>Set Deployment Method tooRetail in IIS</span></span>

| <span data-ttu-id="87115-259">Başlık</span><span class="sxs-lookup"><span data-stu-id="87115-259">Title</span></span>                   | <span data-ttu-id="87115-260">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="87115-260">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="87115-261">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="87115-261">**Component**</span></span>               | <span data-ttu-id="87115-262">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="87115-262">Web Application</span></span> | 
| <span data-ttu-id="87115-263">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="87115-263">**SDL Phase**</span></span>               | <span data-ttu-id="87115-264">Dağıtım</span><span class="sxs-lookup"><span data-stu-id="87115-264">Deployment</span></span> |  
| <span data-ttu-id="87115-265">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="87115-265">**Applicable Technologies**</span></span> | <span data-ttu-id="87115-266">Genel</span><span class="sxs-lookup"><span data-stu-id="87115-266">Generic</span></span> |
| <span data-ttu-id="87115-267">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="87115-267">**Attributes**</span></span>              | <span data-ttu-id="87115-268">Yok</span><span class="sxs-lookup"><span data-stu-id="87115-268">N/A</span></span>  |
| <span data-ttu-id="87115-269">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="87115-269">**References**</span></span>              | <span data-ttu-id="87115-270">[Dağıtım öğesi (ASP.NET Ayarlar Şeması)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="87115-270">[deployment Element (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span></span> |
| <span data-ttu-id="87115-271">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="87115-271">**Steps**</span></span> | <p><span data-ttu-id="87115-272">Merhaba `<deployment retail>` anahtar üretim IIS sunucuları tarafından kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="87115-272">hello `<deployment retail>` switch is intended for use by production IIS servers.</span></span> <span data-ttu-id="87115-273">Merhaba en iyi olası performans ile çalışmasını kullanılan toohelp uygulamalar bu anahtarıdır ve uygulama yeteneği toogenerate İzleme çıktısı sayfasında, devre dışı bırakma hello özelliği toodisplay devre dışı bırakarak leakages hello mümkün olan en küçük güvenlik bilgileri ayrıntılı hata iletileri tooend kullanıcılar ve devre dışı bırakma hello hata ayıklama anahtarı.</span><span class="sxs-lookup"><span data-stu-id="87115-273">This switch is used toohelp applications run with hello best possible performance and least possible security information leakages by disabling hello application's ability toogenerate trace output on a page, disabling hello ability toodisplay detailed error messages tooend users, and disabling hello debug switch.</span></span></p><p><span data-ttu-id="87115-274">Çoğu zaman, anahtarlar ve geliştirici odaklı başarısız gibi seçenekler izleme istek ve hata ayıklama, etkin geliştirme sırasında etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="87115-274">Often times, switches and options that are developer-focused, such as failed request tracing and debugging, are enabled during active development.</span></span> <span data-ttu-id="87115-275">Herhangi bir üretim sunucusu üzerinde hello dağıtım yöntemi tooretail ayarlanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="87115-275">It is recommended that hello deployment method on any production server be set tooretail.</span></span> <span data-ttu-id="87115-276">Merhaba machine.config dosyasını açın ve emin `<deployment retail="true" />` kalır tootrue ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="87115-276">open hello machine.config file and ensure that `<deployment retail="true" />` remains set tootrue.</span></span></p>|

## <span data-ttu-id="87115-277"><a id="fail"></a>Özel durumlar güvenli bir şekilde başarısız olması</span><span class="sxs-lookup"><span data-stu-id="87115-277"><a id="fail"></a>Exceptions should fail safely</span></span>

| <span data-ttu-id="87115-278">Başlık</span><span class="sxs-lookup"><span data-stu-id="87115-278">Title</span></span>                   | <span data-ttu-id="87115-279">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="87115-279">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="87115-280">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="87115-280">**Component**</span></span>               | <span data-ttu-id="87115-281">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="87115-281">Web Application</span></span> | 
| <span data-ttu-id="87115-282">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="87115-282">**SDL Phase**</span></span>               | <span data-ttu-id="87115-283">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="87115-283">Build</span></span> |  
| <span data-ttu-id="87115-284">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="87115-284">**Applicable Technologies**</span></span> | <span data-ttu-id="87115-285">Genel</span><span class="sxs-lookup"><span data-stu-id="87115-285">Generic</span></span> |
| <span data-ttu-id="87115-286">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="87115-286">**Attributes**</span></span>              | <span data-ttu-id="87115-287">Yok</span><span class="sxs-lookup"><span data-stu-id="87115-287">N/A</span></span>  |
| <span data-ttu-id="87115-288">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="87115-288">**References**</span></span>              | [<span data-ttu-id="87115-289">Güvenli bir şekilde başarısız</span><span class="sxs-lookup"><span data-stu-id="87115-289">Fail securely</span></span>](https://www.owasp.org/index.php/Fail_securely) |
| <span data-ttu-id="87115-290">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="87115-290">**Steps**</span></span> | <span data-ttu-id="87115-291">Uygulama güvenli bir şekilde başarısız olması.</span><span class="sxs-lookup"><span data-stu-id="87115-291">Application should fail safely.</span></span> <span data-ttu-id="87115-292">Hangi belirli karar yapılan, temel bir Boole değeri döndürür herhangi bir yöntemini dikkatle oluşturulan özel durum bloğu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="87115-292">Any method that returns a Boolean value, based on which certain decision is made, should have exception block carefully created.</span></span> <span data-ttu-id="87115-293">Son olarak, ne zaman hello özel durum bloğu carelessly yazılmış toowhich güvenlik sorunları Katlama mantıksal hataları miktarda vardır.</span><span class="sxs-lookup"><span data-stu-id="87115-293">There are lot of logical errors due toowhich security issues creep in, when hello exception block is written carelessly.</span></span>|

### <a name="example"></a><span data-ttu-id="87115-294">Örnek</span><span class="sxs-lookup"><span data-stu-id="87115-294">Example</span></span>
```C#
        public static bool ValidateDomain(string pathToValidate, Uri currentUrl)
        {
            try
            {
                if (!string.IsNullOrWhiteSpace(pathToValidate))
                {
                    var domain = RetrieveDomain(currentUrl);
                    var replyPath = new Uri(pathToValidate);
                    var replyDomain = RetrieveDomain(replyPath);

                    if (string.Compare(domain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                    {
                        //// Adding additional check tooenable CMS urls if they are not hosted on same domain.
                        if (!string.IsNullOrWhiteSpace(Utilities.CmsBase))
                        {
                            var cmsDomain = RetrieveDomain(new Uri(Utilities.Base.Trim()));
                            if (string.Compare(cmDomain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                            {
                                return false;
                            }
                            else
                            {
                                return true;
                            }
                        }

                        return false;
                    }
                }

                return true;
            }
            catch (UriFormatException ex)
            {
                LogHelper.LogException("Utilities:ValidateDomain", ex);
                return true;
            }
        }
```
<span data-ttu-id="87115-295">Bazı özel durum oluşursa hello yöntemi yukarıda her zaman True döndürür.</span><span class="sxs-lookup"><span data-stu-id="87115-295">hello above method will always return True, if some exception happens.</span></span> <span data-ttu-id="87115-296">Merhaba son kullanıcı hatalı biçimlendirilmiş bir URL sağlıyorsa, hello tarayıcı gizliliğinize, ancak hello `Uri()` Oluşturucusu değil, bu bir özel durum oluşturur ve hello kurban toohello geçerli ancak hatalı biçimlendirilmiş URL alınır.</span><span class="sxs-lookup"><span data-stu-id="87115-296">If hello end user provides a malformed URL, that hello browser respects, but hello `Uri()` constructor doesn't, this will throw an exception, and hello victim will be taken toohello valid but malformed URL.</span></span> 
