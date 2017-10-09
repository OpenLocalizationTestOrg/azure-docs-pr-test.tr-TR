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
# <a name="security-frame-exception-management--mitigations"></a>Güvenlik çerçevesi: Özel durum yönetimi | Azaltıcı Etkenler 
| Ürün/hizmet | Makale |
| --------------- | ------- |
| **WCF** | <ul><li>[WCF - dahil etmeyin serviceDebug düğümü yapılandırma dosyasında](#servicedebug)</li><li>[WCF - dahil etmeyin serviceMetadata düğümü yapılandırma dosyasında](#servicemetadata)</li></ul> |
| **Web API** | <ul><li>[ASP.NET Web API'de uygun özel durum işleme yapıldığından emin olun](#exception)</li></ul> |
| **Web uygulaması** | <ul><li>[Hata iletileri güvenlik ayrıntıları gösterme](#messages)</li><li>[Varsayılan hata sayfası işleme uygulama](#default)</li><li>[IIS dağıtım yöntemini tooRetail ayarlayın](#deployment)</li><li>[Özel durumlar güvenli bir şekilde başarısız olması](#fail)</li></ul> |

## <a id="servicedebug"></a>WCF - dahil etmeyin serviceDebug düğümü yapılandırma dosyasında

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | WCF | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel, NET Framework 3 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Krallık Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Adımları** | Windows Communication Framework (WCF) hizmetlerini hata ayıklama bilgileri yapılandırılmış tooexpose olabilir. Hata ayıklama bilgileri üretim ortamlarında kullanılmamalıdır. Merhaba `<serviceDebug>` etiketi hello hata ayıklama bilgileri özelliği için bir WCF hizmeti etkin olup olmadığını tanımlar. Merhaba özniteliği IncludeExceptionDetailInFaults tootrue ayarlarsanız, özel durum bilgilerini hello uygulamasından tooclients döndürülür. Saldırganlar hello ek bilgi hedeflenen çıktı toomount saldırılar hello framework, veritabanı veya hello uygulama tarafından kullanılan kaynaklar hata ayıklama elde yararlanabilirsiniz. |

### <a name="example"></a>Örnek
Merhaba aşağıdaki yapılandırma dosyası içerir hello `<serviceDebug>` etiketi: 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
Merhaba hizmetinde hata ayıklama bilgilerini devre dışı bırakın. Bu hello kaldırarak gerçekleştirilebilir `<serviceDebug>` , uygulamanızın yapılandırma dosyasından etiketi. 

## <a id="servicemetadata"></a>WCF - dahil etmeyin serviceMetadata düğümü yapılandırma dosyasında

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | WCF | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Genel, NET Framework 3 |
| **Başvuruları**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Krallık Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Adımları** | Genel olarak bir hizmet hakkında bilgileri gösterme nasıl hello hizmet yararlanabilir içine değerli bilgiler da sağlayabilir. Merhaba `<serviceMetadata>` etiketi hello meta veri yayımlama özelliğini etkinleştirir. Hizmet meta verileri genel olarak erişilebilir olmamalıdır hassas bilgiler içerebilir. En azından, yalnızca güvenilen kullanıcıların tooaccess meta verileri hello ve bilgileri gereksiz sunulmaz olun izin verir. Daha iyi bir yöntem tamamen hello özelliği toopublish meta verileri devre dışı bırakın. Güvenli bir WCF yapılandırma hello içermeyecek `<serviceMetadata>` etiketi. |

## <a id="exception"></a>ASP.NET Web API'de uygun özel durum işleme yapıldığından emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web API | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | MVC 5, MVC 6 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Özel durum işleme ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model ASP.NET Web API doğrulama](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) |
| **Adımları** | Bir HTTP yanıtının durum koduyla içine çevrilen varsayılan olarak, ASP.NET Web API en Yakalanmayan Özel durumları`500, Internal Server Error`|

### <a name="example"></a>Örnek
Merhaba API tarafından döndürülen toocontrol hello durum kodu `HttpResponseException` aşağıda gösterildiği gibi kullanılabilir: 
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

### <a name="example"></a>Örnek
Merhaba özel durum yanıt üzerinde daha fazla denetlemek için hello `HttpResponseMessage` aşağıda gösterildiği gibi sınıfı kullanılabilir: 
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
toocatch işlenmemiş hello türünde olmayan özel durumları `HttpResponseException`, özel durum filtreleri kullanılabilir. Özel durum filtreleri uygulamak hello `System.Web.Http.Filters.IExceptionFilter` arabirimi. Merhaba en basit yolu toowrite bir özel durum filtresi olduğu hello gelen tooderive `System.Web.Http.Filters.ExceptionFilterAttribute` sınıfı ve hello OnException yöntemini geçersiz kılın. 

### <a name="example"></a>Örnek
Dönüştüren bir filtre işte `NotImplementedException` özel durumlar HTTP durum kodu içine `501, Not Implemented`: 
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

Çeşitli yolları tooregister bir Web API özel durum filtresi vardır:
- Eylem tarafından
- Denetleyici tarafından
- Genel

### <a name="example"></a>Örnek
tooapply hello filtre tooa belirli bir eylemi, hello filtre özniteliği toohello Eylem Ekle: 
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
### <a name="example"></a>Örnek
tooapply hello filtre tooall hello eylemleri bir `controller`, bir öznitelik toohello hello filtre eklemek `controller` sınıfı: 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a>Örnek
tooapply hello tooall Web API denetleyicilerinin genel filtre, hello filtre toohello bir örnek ekler `GlobalConfiguration.Configuration.Filters` koleksiyonu. Özel durum filtreleri bu koleksiyonda tooany Web API denetleyici eylemi uygular. 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a>Örnek
Model doğrulama için aşağıda gösterildiği gibi tooCreateErrorResponse yöntemi hello model durumu geçirilebilir: 
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

Olağanüstü işleme ve ASP.Net Web API model doğrulama hakkında ek ayrıntılar için hello başvuruları bölümdeki onay hello bağlantılar 

## <a id="messages"></a>Hata iletileri güvenlik ayrıntıları gösterme

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>Genel hata iletileri, önemli uygulama verileri dahil olmak üzere olmadan toohello kullanıcı doğrudan sağlanır. Gizli verilerin örnekleri şunlardır:</p><ul><li>Sunucu adları</li><li>Bağlantı dizeleri</li><li>Kullanıcı adları</li><li>Parolaları</li><li>SQL yordamları</li><li>Dinamik SQL hatalarının ayrıntıları</li><li>Yığın izleme ve kod satırları</li><li>Bellekte depolanan değişkenleri</li><li>Sürücü ve klasör konumları</li><li>Uygulama yükleme noktaları</li><li>Ana bilgisayar yapılandırma ayarları</li><li>Diğer iç uygulama ayrıntıları</li></ul><p>Bir uygulamadaki tüm hataları yakalama ve genel hata iletileri sağlayarak, yanı sıra IIS içinde özel hatalar etkinleştirme bilgilerin açığa çıkmasına engellemeye yardımcı olur. SQL Server veritabanı ve .NET özel durum işleme, diğer hata mimarileri işleme arasında özellikle ayrıntılı ve son derece kullanışlı tooa kötü amaçlı kullanıcı uygulamanızı profil var. Bir sınıf içeriğini hello .NET özel durum sınıfından türetilen ve böylece beklenmeyen bir özel durum yanlışlıkla değil uygun özel durum işleme sahip olduğundan emin olun görüntü hello doğrudan toohello kullanıcı gerçekleşmedi doğrudan yapın.</p><ul><li>Genel hata doğrudan doğrudan hello özel durum/hata iletisi bulundu koyma belirli Ayrıntılar soyut toohello kullanıcı iletileri sağlayın</li><li>Değil görüntü hello içeriğini bir .NET özel doğrudan toohello kullanıcı sınıfı</li><li>Tüm hata iletilerini yakalayabilir ve uygunsa hello kullanıcıyı bir genel hata iletisini gönderilen toohello uygulama istemci yoluyla bildirin.</li><li>Özellikle hello toohello kullanıcı dönüş doğrudan değerinden hello özel durum sınıfı hello içeriğini gösterme `.ToString()`, veya hello ileti veya StackTrace özelliklerinin hello değerleri. Güvenli bir şekilde bu bilgilerini günlüğe kaydetme ve daha zararsız ileti toohello kullanıcı görüntüleme</li></ul>|

## <a id="default"></a>Varsayılan hata sayfası işleme uygulama

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [ASP.NET hata sayfası ayarlarını Düzenle iletişim kutusu](https://technet.microsoft.com/library/dd569096(WS.10).aspx) |
| **Adımları** | <p>Bir ASP.NET uygulaması başarısız olur ve bir HTTP/1.x 500 İç sunucu hatası neden olan veya bir özellik yapılandırması (istek filtreleme gibi) bir sayfa görüntülenmesini engeller, bir hata iletisi oluşturulur. Yöneticiler, kolay iletisi toohello istemci, ayrıntılı hata iletisi toohello istemci ya da yalnızca ayrıntılı hata iletisi toolocalhost Merhaba uygulaması görüntülenmelidir olsun veya olmasın seçebilirsiniz. Merhaba <customErrors> hello web.config etiketinde üç modu vardır:</p><ul><li>**Üzerinde:** özel hatalar etkin olduğunu belirtir. Hiçbir defaultRedirect özniteliği belirtilmezse, kullanıcılar genel bir hata görür. Merhaba özel hatalar toohello uzak istemciler ve toohello yerel konak gösterilir</li><li>**Kapalı:** özel hatalar devre dışı olduğunu belirtir. Merhaba ayrıntılı ASP.NET hataları toohello uzak istemciler ve toohello yerel konak gösterilir</li><li>**RemoteOnly:** özel hatalar yalnızca toohello uzak istemciler gösterilir ve ASP.NET hatalarının toohello yerel ana görüntüleneceğini belirtir. Bu hello varsayılan değerdir</li></ul><p>Açık hello `web.config` hello uygulama/sitesi için dosya ve hello etiketi ya da sahip olduğundan emin olun `<customErrors mode="RemoteOnly" />` veya `<customErrors mode="On" />` tanımlanmış.</p>|

## <a id="deployment"></a>IIS dağıtım yöntemini tooRetail ayarlayın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Dağıtım öğesi (ASP.NET Ayarlar Şeması)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx) |
| **Adımları** | <p>Merhaba `<deployment retail>` anahtar üretim IIS sunucuları tarafından kullanılmak üzere tasarlanmıştır. Merhaba en iyi olası performans ile çalışmasını kullanılan toohelp uygulamalar bu anahtarıdır ve uygulama yeteneği toogenerate İzleme çıktısı sayfasında, devre dışı bırakma hello özelliği toodisplay devre dışı bırakarak leakages hello mümkün olan en küçük güvenlik bilgileri ayrıntılı hata iletileri tooend kullanıcılar ve devre dışı bırakma hello hata ayıklama anahtarı.</p><p>Çoğu zaman, anahtarlar ve geliştirici odaklı başarısız gibi seçenekler izleme istek ve hata ayıklama, etkin geliştirme sırasında etkinleştirilir. Herhangi bir üretim sunucusu üzerinde hello dağıtım yöntemi tooretail ayarlanması önerilir. Merhaba machine.config dosyasını açın ve emin `<deployment retail="true" />` kalır tootrue ayarlayın.</p>|

## <a id="fail"></a>Özel durumlar güvenli bir şekilde başarısız olması

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Güvenli bir şekilde başarısız](https://www.owasp.org/index.php/Fail_securely) |
| **Adımları** | Uygulama güvenli bir şekilde başarısız olması. Hangi belirli karar yapılan, temel bir Boole değeri döndürür herhangi bir yöntemini dikkatle oluşturulan özel durum bloğu olmalıdır. Son olarak, ne zaman hello özel durum bloğu carelessly yazılmış toowhich güvenlik sorunları Katlama mantıksal hataları miktarda vardır.|

### <a name="example"></a>Örnek
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
Bazı özel durum oluşursa hello yöntemi yukarıda her zaman True döndürür. Merhaba son kullanıcı hatalı biçimlendirilmiş bir URL sağlıyorsa, hello tarayıcı gizliliğinize, ancak hello `Uri()` Oluşturucusu değil, bu bir özel durum oluşturur ve hello kurban toohello geçerli ancak hatalı biçimlendirilmiş URL alınır. 
