---
title: "Azure Active Directory ve API Management ile Web API arka uç aaaProtect | Microsoft Docs"
description: "Bilgi nasıl tooprotect Azure Active Directory ve API Management ile Web API arka uç."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a>Nasıl tooprotect Azure Active Directory ve API Management ile Web API arka uç
Video gösterileri nasıl aşağıdaki hello toobuild bir Web API arka ucu ve Azure Active Directory ve API Management ile OAuth 2.0 protokolünü kullanarak koruyabilirsiniz.  Ek bilgi için hello hello videoda adımlar ve bu makalede genel bir bakış sağlar. Bu 24 dakikalık videoyu şunların nasıl yapıldığını gösterir için:

* Bir Web API arka ucu oluşturmak ve aad'ye - 1: 30'da başlayan güvenli
* API Management - 7:10 Başlangıç Hello API aktarın
* 9:09 başlayan hello Geliştirici Portalı toocall hello API - yapılandırın
* Bir masaüstü uygulaması toocall hello API - 18:08 başlayan yapılandırın
* JWT doğrulama İlkesi toopre yapılandırma-20:47 başlayan isteklerini - yetkilendirmek

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a>Azure AD dizini oluşturma
Web API yedeklenen ilk olmalıdır Azure Active Directory'yi kullanarak toosecure bir AAD kiracısı. Bu videoda adlı bir kiracı **APIMDemo** kullanılır. toocreate bir AAD kiracısı oturum açma toohello [Klasik Azure portalı](https://manage.windowsazure.com) tıklatıp **yeni**->**uygulama hizmetleri**->**etkin Dizin**->**Directory**->**özel Oluştur**. 

![Azure Active Directory][api-management-create-aad-menu]

Bu örnekte adlı bir dizin **APIMDemo** adlı varsayılan etki alanı ile oluşturulan **DemoAPIM.onmicrosoft.com**. Bu dizin hello video kullanılır.

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a>Azure Active Directory tarafından güvenliği sağlanan bir Web API hizmet oluşturma
Bu adımda, Visual Studio 2013 kullanarak bir Web API arka uç oluşturulur. Merhaba video, bu adım 1: 30'da başlar. Visual Studio tıklatın toocreate Web API arka uç projesi **dosya**->**yeni**->**proje**ve seçin **ASP.NET Web Uygulama** hello gelen **Web** şablonları listesi. Bu video hello adlı projesi **APIMAADDemo**. Tıklatın **Tamam** toocreate hello projesi. 

![Visual Studio][api-management-new-web-app]

Tıklatın **Web API** hello gelen **şablon listesini seçin** toocreate bir Web API projesi. Azure Directory kimlik doğrulaması tooconfigure tıklatın **kimlik doğrulamayı Değiştir**.

![Yeni Proje][api-management-new-project]

Tıklatın **Kurumsal hesaplar**ve hello belirtin **etki alanı** AAD kiracınızın. Bu örnek hello etki alanıdır **DemoAPIM.onmicrosoft.com**. dizininizin hello etki hello elde edilebilir **etki alanları** dizininizin sekmesi.

![Etki Alanları][api-management-aad-domains]

Hello istenen hello ayarlarını yapılandırma **kimlik doğrulamayı Değiştir** iletişim kutusu ve tıklatın **Tamam**.

![Kimlik doğrulamayı Değiştir][api-management-change-authentication]

Tıkladığınızda **Tamam** Visual Studio, Azure AD dizininizi uygulamanızla tooregister deneyecek ve Visual Studio tarafından istendiğinde toosign de olabilir. Dizininiz için bir yönetici hesabı kullanarak oturum açın.

![TooVisual Studio oturum][api-management-sign-in-vidual-studio]

Bu proje bir Azure Web API onay hello olarak tooconfigure kutusunda **hello buluttaki konağa** ve ardından **Tamam**.

![Yeni Proje][api-management-new-project-cloud]

İstendiğinde toosign tooAzure içinde olabilir ve ardından hello Web uygulaması yapılandırabilirsiniz.

![Yapılandırma][api-management-configure-web-app]

Bu örnekte yeni bir **uygulama hizmeti planı** adlı **APIMAADDemo** belirtilir.

Tıklatın **Tamam** tooconfigure Web uygulaması hello ve başlangıç projesi oluşturun.

## <a name="add-hello-code-toohello-web-api-project"></a>Merhaba kod toohello Web API projesi ekleme
Merhaba video sonraki adımda Hello hello kod toohello Web API projesi ekler. Bu adım 4:35 başlatır.

Bu örnekte Hello Web API'sini bir model ve bir denetleyici kullanarak bir temel hesaplayıcı hizmet uygular. tooadd hello modeli hello hizmeti için sağ **modelleri** içinde **Çözüm Gezgini** ve **Ekle**, **sınıfı**. Ad hello sınıfı `CalcInput` tıklatıp **Ekle**.

Merhaba aşağıdakileri ekleyin `using` hello deyimi toohello üst `CalcInput.cs` dosya.

```c#
using Newtonsoft.Json;
```

Oluşturulan hello sınıfı koddan hello ile değiştirin.

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

Sağ **denetleyicileri** içinde **Çözüm Gezgini** ve **Ekle**->**denetleyicisi**. Seçin **Web API 2 denetleyici - boş** tıklatıp **Ekle**. Tür **CalcController** Merhaba Denetleyici adı ve'ı tıklatın **Ekle**.

![Denetleyici ekleme][api-management-add-controller]

Merhaba aşağıdakileri ekleyin `using` hello deyimi toohello üst `CalcController.cs` dosya.

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

Oluşturulan hello denetleyici sınıfını koddan hello ile değiştirin. Bu kod hello uygulayan `Add`, `Subtract`, `Multiply`, ve `Divide` hello temel hesaplayıcı API'si işlemleri.

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

Tuşuna **F6** toobuild ve hello çözüm doğrulayın.

## <a name="publish-hello-project-tooazure"></a>Yayımlama Hello proje tooAzure
Bu adım hello Visual Studio yayımlanan tooAzure projesidir. Merhaba video, bu adım 5:45 başlatır.

toopublish proje tooAzure Merhaba, hello sağ **APIMAADDemo** seçin ve Visual Studio Proje **Yayımla**. Hello Hello varsayılan ayarları koruyun **Web'i Yayımla** iletişim kutusu ve tıklatın **Yayımla**.

![Web yayımlama][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a>Azure AD toohello arka uç hizmeti uygulama izinleri
Yeni bir uygulama hello arka uç hizmeti için Azure AD dizininizi hello yapılandırma bölümü ve Web API projenizin yayımlama işlemi olarak oluşturulur. Merhaba video Bu adım 6:13 başlayan toohello Web API'si arka uç izinleri verilir.

![Uygulama][api-management-aad-backend-app]

Merhaba uygulama tooconfigure hello gerekli izinleri Hello adına tıklayın. Toohello gidin **yapılandırma** sekmesi ve toohello aşağı **izinleri tooother uygulamaları** bölümü. Merhaba tıklatın **uygulama izinleri** yanında aşağı açılan **Windows** **Azure Active Directory**, hello kutuyu **dizinverileriniokuma**, tıklatıp **kaydetmek**.

![İzinleri ekleme][api-management-aad-add-permissions]

> [!NOTE]
> Varsa **Windows** **Azure Active Directory** olan izinleri tooother uygulamalar'ın altında listelenen değil, tıklatın **uygulama ekleme** ve hello listesinden ekleyin.
> 
> 

Merhaba Not **uygulama kimliği URI'si** Azure AD uygulaması hello API Management Geliştirici Portalı için yapılandırıldığında, bir sonraki adımda kullanmak için.

![Uygulama Kimliği URI][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a>API yönetime Hello Web API alma
API hello Azure portalı erişilen hello API yayımcı portalında yapılandırılır. tooreach, tıklatın **yayımcı portalına** API Management hizmetinizin hello araç çubuğundan. Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [ilk API'nizi yönetme] [ Manage your first API] Öğreticisi.

![Yayımcı portalı][api-management-management-console]

İşlemleri olabilir [tooAPIs el ile eklenen](api-management-howto-add-operations.md), veya içeri aktarılabilir. Bu videoda, Swagger biçiminde 6:40 başlangıç işlemleri alınır.

Adlı bir dosya oluşturun `calcapi.json` ile içeriği aşağıdaki ve tooyour bilgisayara kaydedin. Bu hello olun `host` özniteliği tooyour Web API'si arka uç noktaları. Bu örnekte `"host": "apimaaddemo.azurewebsites.net"` kullanılır.

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

tooimport hello hesaplayıcı API'sini, tıklatın **API'leri** hello gelen **API Management** sol hello ve ardından menüsünde **içeri aktarma API'si**.

![API’yi İçeri Aktar düğmesi][api-management-import-api]

Aşağıdaki adımları tooconfigure hello hesaplayıcı API'si hello gerçekleştirin.

1. ' I tıklatın **dosyasından**, toohello Gözat `calculator.json` dosyayı kaydedilmiş ve hello tıklayın **Swagger** radyo düğmesi.
2. Tür **calc** hello içine **Web API'si URL soneki** metin kutusu.
3. Tıklatın hello **ürünler (isteğe bağlı)** kutusuna ve seçin **Starter**.
4. Tıklatın **kaydetmek** tooimport hello API.

![Yeni API ekle][api-management-import-new-api]

Merhaba API içeri aktarıldığında hello hello API için Özet sayfasında hello yayımcı Portalı'nda görüntülenir.

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a>Hello API hello Geliştirici portalından başarısız olan çağrı
Bu noktada, hello API API yönetime içeri aktarıldı ancak hello arka uç hizmeti Azure AD kimlik doğrulaması ile korunduğu için henüz başarılı bir şekilde hello Geliştirici portalından çağrılamaz. Bu 7: hello aşağıdaki adımları kullanarak 40 başlayan hello video gösterilmiştir.

Tıklatın **Geliştirici Portalı** hello sağ üst tarafındaki hello yayımcı portalı.

![Geliştirici portalı][api-management-developer-portal-menu]

Tıklatın **API'leri** hello tıklatıp **hesaplayıcı** API.

![Geliştirici portalı][api-management-dev-portal-apis]

Tıklatın **deneyin**.

![Deneyin][api-management-dev-portal-try-it]

Tıklatın **Gönder** ve Not hello yanıt durumu **401 Yetkisiz**.

![Gönder][api-management-dev-portal-send-401]

Merhaba istek yetkisiz çünkü Hello arka uç API'si Azure Active Directory tarafından korunur. Başarılı bir şekilde hello API çağırmadan önce hello Geliştirici Portalı OAuth 2.0 kullanan yapılandırılmış tooauthorize geliştiriciler olması gerekir. Bu işlem hello aşağıdaki bölümlerde açıklanmıştır.

## <a name="register-hello-developer-portal-as-an-aad-application"></a>Bir AAD uygulaması olarak kayıt hello Geliştirici Portalı
OAuth 2.0 kullanan hello Geliştirici Portalı tooauthorize geliştiriciler yapılandırmada hello ilk tooregister hello Geliştirici Portalı bir AAD uygulaması adımdır. Bu 8:27 hello videoda başlayarak gösterilmiştir.

Bu örnekte bu videoda, ilk adımı hello toohello Azure AD kiracısı gidin **APIMDemo** toohello giderek **uygulamaları** sekmesi.

![Yeni uygulama][api-management-aad-new-application-devportal]

Merhaba tıklatın **Ekle** düğmesini toocreate yeni bir Azure Active Directory uygulaması ve seçin **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.

![Yeni uygulama][api-management-new-aad-application-menu]

Seçin **Web uygulaması ve/veya Web API**, bir ad girin ve hello İleri okuna tıklayın. Bu örnekte **APIMDeveloperPortal** kullanılır.

![Yeni uygulama][api-management-aad-new-application-devportal-1]

İçin **oturum açma URL'si** API Management hizmetiniz hello URL'sini girin ve ilave `/signin`. Bu örnekte `https://contoso5.portal.azure-api.net/signin` kullanılır.

İçin **uygulama kimliği URL'si** API Management hizmetiniz hello URL'sini girin ve bazı benzersiz karakterler ekleyin. Bunlar istenen herhangi bir karakter olabilir ve bu örnekte `https://contoso5.portal.azure-api.net/dp` kullanılır. Ne zaman hello istenen **uygulama özellikleri** olan yapılandırılmış, hello onay işareti toocreate hello uygulamaya tıklayın.

![Yeni uygulama][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a>Bir API Management OAuth 2.0 yetkilendirme sunucusu yapılandırın
Merhaba sonraki tooconfigure bir OAuth 2.0 yetkilendirme Sunucusu API Management adımdır. Bu adım 9:43 başlayan video hello gösterilmiştir.

Tıklatın **güvenlik** hello API Management menüden hello sol tarafta, **OAuth 2.0**ve ardından **yetkilendirme eklemek** sunucu.

![Yetkilendirme Sunucusu Ekle][api-management-add-authorization-server]

Hello bir ad ve isteğe bağlı bir açıklama girin **adı** ve **açıklama** alanları. Bu alanlar hello API Management hizmet örneği içinde kullanılan tooidentify hello OAuth 2.0 yetkilendirme sunucusu olur. Bu örnekte **yetkilendirme sunucusu demo** kullanılır. Daha sonra bir API için kimlik doğrulaması için kullanılan bir OAuth 2.0 server toobe belirttiğinizde, bu ad seçer.

Hello için **istemci kayıt sayfası URL'si** bir yer tutucu değerini girin `http://localhost`.  Merhaba **istemci kayıt sayfası URL'si** toohello sayfasında, kullanıcıların noktaları toocreate kullanın ve kullanıcı hesaplarının yönetimini desteklemek için OAuth 2.0 sağlayıcıları kendi hesaplarını yapılandırın. Bu örnekte, kullanıcıların değil oluşturun ve yer tutucu kullanılmak üzere kendi hesaplarını yapılandırın.

![Yetkilendirme Sunucusu Ekle][api-management-add-authorization-server-1]

Ardından, belirtin **yetkilendirme uç noktası URL'si** ve **belirteç uç nokta URL'si**.

![Yetkilendirme sunucusu][api-management-add-authorization-server-1a]

Bu değerleri hello alınabilir **uygulama uç noktaları** hello hello Geliştirici Portalı için oluşturulmuş AAD uygulaması sayfasında. tooaccess hello uç noktaları gidin toohello **yapılandırma** sekmesinde Merhaba AAD uygulaması için **uç noktaları görüntülemek**.

![Uygulama][api-management-aad-devportal-application]

![Uç noktalarını görüntüle][api-management-aad-view-endpoints]

Kopya hello **OAuth 2.0 yetkilendirme uç noktası** ve hello yapıştırma **yetkilendirme uç noktası URL'si** metin kutusu.

![Yetkilendirme Sunucusu Ekle][api-management-add-authorization-server-2]

Kopya hello **OAuth 2.0 belirteç uç noktası** ve hello yapıştırma **belirteç uç nokta URL'si** metin kutusu.

![Yetkilendirme Sunucusu Ekle][api-management-add-authorization-server-2a]

Ayrıca hello belirteç uç noktası, toopasting adlı bir ek gövde parametresini ekleyin **kaynak** ve hello hello değeri için kullanmak **uygulama kimliği URI'si** hello AAD uygulaması olan hello arka uç hizmeti için gelen Merhaba Visual Studio projesi yayımlandığında oluşturulur.

![Uygulama Kimliği URI][api-management-aad-sso-uri]

Ardından, hello istemci kimlik bilgilerini belirtin. İstediğiniz hello kaynak hello kimlik bilgilerini bunlar tooaccess, bu durumda hello Geliştirici Portalı.

![İstemci kimlik bilgileri][api-management-client-credentials]

tooget hello **istemci kimliği**, toohello gidin **yapılandırma** hello hello Geliştirici Portalı ve kopyalama hello için AAD uygulama sekmesinde **istemci kimliği**.

tooget hello **gizli** hello tıklatın **seçin süresi** hello açılan **anahtarları** bölüm ve bir aralık belirtin. Bu örnekte, 1 yıl kullanılır.

![İstemci kimliği][api-management-aad-client-id]

Tıklatın **kaydetmek** toosave hello yapılandırma ve görüntü hello anahtarı. 

> [!IMPORTANT]
> Bu anahtarı not edin. Hello Azure Active Directory yapılandırması penceresini kapattığınızda hello anahtarı yeniden görüntülenemiyor.
> 
> 

Kopya hello anahtar toohello Pano, anahtar geri toohello yayımcı portalına hello hello anahtarı yapıştırın **gizli** metin kutusuna, tıklatıp **kaydetmek**.

![Yetkilendirme Sunucusu Ekle][api-management-add-authorization-server-3]

Hemen hello istemci kimlik bilgileri aşağıdaki yetkilendirme kodu verme olur. Bu yetkilendirme kodu kopyalayın ve anahtar geri tooyour Azure AD Geliştirici Portalı uygulaması sayfasını yapılandırmak ve hello yetkilendirme verme hello yapıştırma **yanıt URL'si** alan öğesini tıklatıp **kaydetmek** yeniden.

![Yanıt URL'si][api-management-aad-reply-url]

Merhaba sonraki tooconfigure hello hello Geliştirici Portalı AAD uygulama izinlerini adımdır. Tıklatın **uygulama izinleri** ve hello kutuyu **dizin verilerini okuma**. Tıklatın **kaydetmek** bu değiştirin ve ardından toosave **uygulama eklemek**.

![İzinleri ekleme][api-management-add-devportal-permissions]

Merhaba arama simgesine tıklayın türü **APIM** hello içine kutusundan başlayarak, seçin **APIMAADDemo**ve hello onay işareti toosave'ı tıklatın.

![İzinleri ekleme][api-management-aad-add-app-permissions]

Tıklatın **izinlere temsilci** için **APIMAADDemo** ve hello kutuyu **erişim APIMAADDemo**, tıklatıp **kaydetmek**. Bu hello Geliştirici Portalı Uygulama tooaccess hello arka uç hizmeti sağlar.

![İzinleri ekleme][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a>OAuth 2.0 kullanıcı yetkilendirme hello hesaplayıcı API'si için etkinleştirme
Merhaba OAuth 2.0 sunucusu yapılandırılır, API'nizi hello güvenlik ayarlarını belirtebilirsiniz. Bu adım hello 14: 30'da başlayan video gösterilmiştir.

Tıklatın **API'leri** hello soldaki menüden ve tıklatın **hesaplayıcı** tooview ve ayarlarını yapılandırın.

![Hesaplayıcı API'sini][api-management-calc-api]

Toohello gidin **güvenlik** sekmesinde, hello denetleyin **OAuth 2.0** onay kutusunu seçin hello istenen yetkilendirme hello sunucudan **yetkilendirme sunucusu** aşağı açılır ve'ı tıklatın **Kaydetmek**.

![Hesaplayıcı API'sini][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a>Merhaba hesaplayıcı API'si hello Geliştirici Portalı'ndan başarıyla çağırın
Merhaba OAuth 2.0 yetkilendirme API hello üzerinde yapılandırılmış, işlemlerini başarıyla hello Geliştirici Merkezi'nden çağrılabilir. Bu adım hello 15: 00'dan başlayarak video gösterilmiştir.

Geri toohello gidin **iki tamsayı Ekle** işlemi hello hesap makinesi hizmetinin hello Geliştirici Portalı ve tıklatın **deneyin**. Not hello yeni öğesini hello **yetkilendirme** eklediğiniz karşılık gelen toohello yetkilendirme sunucusu bölüm.

![Hesaplayıcı API'sini][api-management-calc-authorization-server]

Seçin **yetkilendirme kodu** hello yetkilendirme açılan dan listesinde ve hello hesap toouse hello kimlik bilgilerini girin. Merhaba hesabıyla oturum açmış istenebilir değil.

![Hesaplayıcı API'sini][api-management-devportal-authorization-code]

Tıklatın **Gönder** ve Not hello **yanıt durumu** , **200 Tamam** ve hello yanıt içeriği hello işlemde hello sonucu.

![Hesaplayıcı API'sini][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a>Bir masaüstü uygulaması toocall hello API yapılandırın
Sonraki yordamda hello video Hello 16: 30'da başlatılır ve basit masaüstü uygulaması toocall hello API yapılandırır. Merhaba ilk adımı tooregister hello masaüstü uygulaması, Azure AD ve erişim toohello dizin ve toohello arka uç hizmeti verin. 18: 25'hello hesaplayıcı API'sini üzerinde bir işlemi çağırma Merhaba masaüstü uygulaması Tanıtımı yoktur.

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a>JWT doğrulama İlkesi toopre yapılandırma-isteklerini yetkilendirmek
Merhaba hello video son yordamda 20:48 başlar ve nasıl gösterir toouse hello [doğrulamak JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) İlkesi toopre-hello erişim belirteçleri her gelen istek doğrulayarak isteklerini yetkilendirmek. Merhaba isteği hello doğrulamak JWT ilke tarafından doğrulanmaz, hello isteği API Management tarafından engellenir ve toohello arka uç geçmedi.

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

Yapılandırma ve bu ilkeyi kullanarak başka bir sunum için bkz: [bulut kapak bölüm 177: diğer API Management Özellikler](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve too13:50 ileri sarma. Too15:00 hello İlkesi Düzenleyicisi'nde yapılandırılan toosee hello İlkesi sarma ve ardından yetkilendirme belirtecini too18:50 hem ile hem de hello olmadan hello Geliştirici Portalı'ndan bir işlem çağırma, bir örnek için gerekli.

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi denetleyin [videolar](https://azure.microsoft.com/documentation/videos/index/?services=api-management) API Management hakkında.
* Diğer yolları toosecure için arka uç hizmetinizin bkz [karşılıklı sertifika kimlik doğrulaması](api-management-howto-mutual-certificates.md).

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md
