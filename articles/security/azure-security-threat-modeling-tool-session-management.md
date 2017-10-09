---
title: "aaaSession Yönetimi - Microsoft tehdit modelleme aracı - Azure | Microsoft Docs"
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
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a>Güvenlik çerçevesi: Oturum yönetimi | Makaleler 
| Ürün/hizmet | Makale |
| --------------- | ------- |
| **Azure AD**    | <ul><li>[Azure AD kullanırken ADAL yöntemleri kullanarak uygulama uygun oturum kapatma](#logout-adal)</li></ul> |
| IOT cihaz | <ul><li>[Sonlu yaşam süreleri için oluşturulan SaS belirteci kullanın](#finite-tokens)</li></ul> |
| **Azure belge DB** | <ul><li>[Minimum belirteci yaşam süreleri için oluşturulan kaynak belirteçleri kullanın](#resource-tokens)</li></ul> |
| **ADFS** | <ul><li>[ADFS kullanırken WsFederation yöntemleri kullanarak uygulama uygun oturum kapatma](#wsfederation-logout)</li></ul> |
| **Kimlik sunucusu** | <ul><li>[Kimlik sunucusu kullanılırken uygulama uygun oturum kapatma](#proper-logout)</li></ul> |
| **Web uygulaması** | <ul><li>[HTTPS üzerinden kullanılabilir uygulamaları güvenli tanımlama bilgileri kullanmalıdır](#https-secure-cookies)</li><li>[Tüm http tabanlı uygulama http tanımlama bilgisi tanımı için yalnızca belirtmeniz gerekir](#cookie-definition)</li><li>[ASP.NET web sayfaları siteler arası istek sahteciliği (CSRF) saldırılarını karşı azaltmak](#csrf-asp)</li><li>[Oturum etkin olmama ömrü için ayarlama](#inactivity-lifetime)</li><li>[Uygulama hello uygulamasından uygun oturum kapatma](#proper-app-logout)</li></ul> |
| **Web API** | <ul><li>[ASP.NET Web API siteler arası istek sahteciliği (CSRF) saldırılarını karşı azaltmak](#csrf-api)</li></ul> |

## <a id="logout-adal"></a>Azure AD kullanırken ADAL yöntemleri kullanarak uygulama uygun oturum kapatma

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure AD | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Merhaba uygulaması Azure AD tarafından verilen erişim belirtecini kullanır, hello oturum kapatma olay işleyicisi çağırmalıdır |

### <a name="example"></a>Örnek
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a>Örnek
Session.Abandon() yöntemini çağırarak, kullanıcının oturumunu destroy. Yöntemini aşağıdaki kullanıcı oturum kapatma güvenli uygulamasını gösterir:
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <a id="finite-tokens"></a>Sonlu yaşam süreleri için oluşturulan SaS belirteci kullanın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT cihaz | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | SaS belirteci tooAzure IOT Hub kimlik doğrulaması için oluşturulan sınırlı süre sonu dönemi olması gerekir. Merhaba SaS belirteci yaşam süreleri tooa minimum toolimit hello süreyi hello belirteçleri güvenliğinin ihlal edilmesi durumunda bunlar çalınabilir tutun.|

## <a id="resource-tokens"></a>Minimum belirteci yaşam süreleri için oluşturulan kaynak belirteçleri kullanın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure belge DB | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Kaynak belirteci tooa en düşük değer, Hello timespan azaltın. Kaynak belirteçleri 1 saatlik varsayılan geçerli timespan vardır.|

## <a id="wsfederation-logout"></a>ADFS kullanırken WsFederation yöntemleri kullanarak uygulama uygun oturum kapatma

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | ADFS | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Merhaba uygulaması tarafından ADFS STS belirteç dayalıysa, hello oturum kapatma olay işleyicisi WSFederationAuthenticationModule.FederatedSignOut() yöntemi toolog hello kullanıcı çıkışı çağırmanız gerekir. Ayrıca hello geçerli oturum yok edilmesi ve hello oturum belirteç değeri sıfırlayın ve nullified.|

### <a name="example"></a>Örnek
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <a id="proper-logout"></a>Kimlik sunucusu kullanılırken uygulama uygun oturum kapatma

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Kimlik sunucusu | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [IdentityServer3 federe oturum kapatma](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| **Adımları** | Dış kimlik sağlayıcıları ile Merhaba özelliği toofederate IdentityServer destekler. Bir Yukarı Akış kimlik sağlayıcısı dışında bir kullanıcı oturum açtığında hello kullanıcı oturumu kapattığında hello Protokolü kullanıldığında, bağlı olarak bunun olası tooreceive bir bildirim olabilir. Kullanıcı çıkışı istemcilerine de kaydolabilirsiniz şekilde hello IdentityServer toonotify sağlar. Merhaba başvurular bölümündeki hello uygulama ayrıntılarını Hello belgelerine bakın.|

## <a id="https-secure-cookies"></a>HTTPS üzerinden kullanılabilir uygulamaları güvenli tanımlama bilgileri kullanmalıdır

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | EnvironmentType - OnPrem |
| **Başvuruları**              | [httpCookies Ögesi (ASP.NET Ayarlar Şeması)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure özelliği](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx) |
| **Adımları** | Tanımlama bilgileri, yalnızca erişilebilir toohello etki alanı için bunlar kapsamlı normalde bilgileridir. Ne yazık ki, HTTPS üzerinden oluşturulan tanımlama bilgilerini HTTP üzerinden erişilebilir olması için "etki alanı" Merhaba tanımını hello Protokolü içermez. tanımlama bilgisi hello toohello tarayıcı yalnızca HTTPS üzerinden kullanılabilir olması Hello "güvenli" özniteliği belirtir. HTTPS üzerinden ayarlamak tüm tanımlama bilgilerini hello kullandığınızdan emin olun **güvenli** özniteliği. Merhaba gereksinim hello requireSSL özniteliği tootrue ayarlayarak hello web.config dosyasında uygulanabilir. Merhaba tercih edilen yaklaşım hello zorunlu kılacak çünkü olan **güvenli** ek kod değişikliklerini özniteliği hello gerek toomake olmadan tüm geçerli ve gelecekteki olan tanımlama bilgileri.|

### <a name="example"></a>Örnek
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
HTTP kullanılan tooaccess Merhaba uygulaması olsa bile hello ayarı zorunlu kılınır. HTTP kullanılıyorsa, uygulama tooaccess Merhaba, hello hello tanımlama bilgilerini hello güvenli özniteliği ve hello tarayıcı ile ayarlandığından Merhaba uygulaması bunları göndermez ayarı sonları geri toohello uygulama.

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Web Forms, MVC5 |
| **Öznitelikleri**              | EnvironmentType - OnPrem |
| **Başvuruları**              | Yok  |
| **Adımları** | RequireSSL tooTrue ayarı tarafından Hello web uygulamasıdır bağlı olan taraf hello ve hello IDP ADFS sunucusu olduğunda hello FedAuth belirtecin güvenli özniteliği yapılandırılabilir `system.identityModel.services` web.config bölümünü:|

### <a name="example"></a>Örnek
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <a id="cookie-definition"></a>Tüm http tabanlı uygulama http tanımlama bilgisi tanımı için yalnızca belirtmeniz gerekir

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Güvenli tanımlama bilgisi özniteliği](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| **Adımları** | siteler arası (XSS) saldırısı ile bilgilerin açığa çıkmasına hello riskini toomitigate, yeni bir öznitelik - httpOnly - sunulan toocookies oluştu ve önde gelen tüm tarayıcılar tarafından desteklenir. bir tanımlama bilgisi komut dosyası aracılığıyla erişilebilir değil Hello özniteliği belirtir. HttpOnly tanımlama bilgilerini kullanarak bir web uygulaması hello tanımlama bilgisine dahil hassas bilgileri komut dosyası çalınması ve tooan saldırganın Web gönderilen olduğunu hello olasılığını azaltır. |

### <a name="example"></a>Örnek
Tanımlama bilgileri kullanan tüm HTTP tabanlı uygulamalar HttpOnly yapılandırma web.config dosyasında aşağıdaki uygulayarak hello tanımlama bilgisi tanımında belirtmeniz gerekir:
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Web formları |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [FormsAuthentication.RequireSSL özelliği](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| **Adımları** | Merhaba RequireSSL özellik değeri, hello yapılandırma öğesinin hello requireSSL özniteliğini kullanarak bir ASP.NET uygulaması için hello yapılandırma dosyasında ayarlanır. SSL (Güvenli Yuva Katmanı) ayarı hello requireSSL özniteliği tarafından gerekli tooreturn hello form kimlik doğrulaması tanımlama bilgisi toohello sunucusu olup olmadığını, ASP.NET uygulamanız için hello Web.config dosyasında belirtebilirsiniz.|

### <a name="example"></a>Örnek 
Merhaba aşağıdaki kod örneğinde hello requireSSL öznitelik hello Web.config dosyasında ayarlar.
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | MVC5 |
| **Öznitelikleri**              | EnvironmentType - OnPrem |
| **Başvuruları**              | [Windows Identity Foundation (WIF) yapılandırması – Bölüm II](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| **Adımları** | tooset httpOnly özniteliği FedAuth tanımlama bilgilerinin hideFromCsript öznitelik değeri tooTrue ayarlamanız gerekir. |

### <a name="example"></a>Örnek
Aşağıdaki yapılandırma hello doğru yapılandırması gösterilmektedir:
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <a id="csrf-asp"></a>ASP.NET web sayfaları siteler arası istek sahteciliği (CSRF) saldırılarını karşı azaltmak

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Siteler arası istek sahtekarlığı (CSRF veya XSRF), bir saldırgan, farklı bir kullanıcının bir web sitesi kurulan oturum hello güvenlik bağlamında eylemleri gerçekleştirebilirsiniz saldırı türüdür. Merhaba hedef toomodify ya da hello hedeflenen web sitesi yalnızca oturum tanımlama bilgileri tooauthenticate alınan isteği dayalıysa içeriği silin. Bir saldırgan, üzerinde hello kullanıcı zaten oturum açık bir siteden bir URL bir komut ile farklı bir kullanıcının tarayıcı tooload alarak bu güvenlik açığından yararlanabilir. Gibi farklı bir web sitesi barındırma tarafından bir kaynak hello savunmasız sunucu veya alınırken hello kullanıcı tooclick bağlantı yükler, bir saldırganın toodo için birçok yolu vardır. Merhaba sunucu bir ek belirteç toohello istemci gönderir, bu tüm gelecekteki isteklerin belirteçte istemci tooinclude hello ve tüm gelecekteki isteklerin toohello geçerli oturum gibi ile ilgili bir belirteç içerdiğini doğrular gerektirir hello saldırı önlenebilir Merhaba ASP.NET AntiForgeryToken ya da ViewState kullanıyor. |

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | MVC5, MVC6 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [ASP.NET MVC ve Web sayfaları XSRF/CSRF önleme](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| **Adımları** | Anti-CSRF ve ASP.NET MVC forms - kullanım hello `AntiForgeryToken` yardımcı yöntemi görünümleri; put bir `Html.AntiForgeryToken()` forma Merhaba, örneğin,|

### <a name="example"></a>Örnek
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a>Örnek
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>Örnek
Merhaba aynı zaman, bir tanımlama bilgisi ile aynı hello rastgele gizli değer yukarıda gösterilen olarak değeri hello __RequestVerificationToken olarak adlandırılan Html.AntiForgeryToken() verir hello ziyaretçi. Ardından, toovalidate gelen bir form post hello [ValidateAntiForgeryToken] filtre toohello hedef eylem yöntemine ekleyin. Örneğin:
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
Denetleyen yetkilendirme Filtresi:
* Merhaba gelen istek __RequestVerificationToken adlı bir tanımlama bilgisi içeriyor
* Merhaba gelen istek sahip bir `Request.Form` __RequestVerificationToken adlı giriş
* Bu tanımlama bilgisi ve `Request.Form` varsayılarak tüm değerleri Eşleştir iyi, hello isteği geçtiği normal olarak. Ancak değilse, ardından bir Yetkilendirme hatası iletisi "gerekli sahteciliğe karşı koruma belirteci belirtilmedi veya geçersiz". 

### <a name="example"></a>Örnek
Anti-CSRF ve AJAX: JSON verilerini, HTML form verilerini bir AJAX İsteği Gönder çünkü hello form simgesi AJAX istekleri için bir sorun olabilir. Özel bir HTTP üstbilgisi toosend hello belirteçleri bir çözümdür. Merhaba aşağıdaki kodu Razor sözdizimi toogenerate hello belirteçleri kullanır ve ardından hello belirteçleri tooan AJAX isteği ekler. 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>Örnek
Merhaba isteği işlerken hello belirteçleri hello isteği başlığından ayıklayın. Ardından toovalidate hello belirteçleri hello AntiForgery.Validate yöntemini çağırın. Merhaba belirteçleri geçerli değilse hello doğrulama yöntemi bir özel durum oluşturur.
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Web formları |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Take avantajı, ASP.NET yerleşik özellikleri tooFend Kapalı Web saldırıları](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| **Adımları** | Her kullanıcı - kullanıcı kimliği için değişir ViewStateUserKey tooa rasgele dize ayarlayarak WebForm tabanlı uygulamalarda CSRF saldırıları azaltmak için veya daha iyi henüz, oturum kimliği Kimliktir öngörülemeyen, oturum zaman aşımına uğradı ve bir kullanıcı başına temelinde değişir olduğundan bir teknik ve sosyal nedeniyle için oturum kimliği daha iyi bir uyum sayısıdır.|

### <a name="example"></a>Örnek
Sayfalarınızın tümünü toohave gereksinim hello kod aşağıdadır:
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <a id="inactivity-lifetime"></a>Oturum etkin olmama ömrü için ayarlama

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [HttpSessionState.Timeout özelliği](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx) |
| **Adımları** | Oturum zaman aşımı, kullanıcı herhangi bir eylem bir web sitesinde (web sunucusu tarafından tanımlanan) bir aralık boyunca gerçekleştirmez olduğunda olay hello gerçekleşen temsil eder. Sunucu tarafında olay Merhaba, hello kullanıcı oturumu too'invalid hello durumunu değiştir ' (örneğin "artık kullanılmıyor") ve (içine bulunan tüm verileri silme) hello web sunucusu toodestroy talimatını. Merhaba aşağıdaki kod örneğinde hello zaman aşımı oturum özniteliği too15 dakika hello Web.config dosyasında ayarlar.|

### <a name="example"></a>Örnek
'''XML kodunu <configuration> < system.web > <sessionState mode="InProc" cookieless="true" timeout="15" /> < /system.web ></configuration>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Web formları |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Öğe forms kimlik doğrulaması için (ASP.NET Ayarlar Şeması)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx) |
| **Adımları** | Merhaba Forms kimlik doğrulaması bileti tanımlama bilgisi zaman aşımı too15 dakika ayarlayın|

### <a name="example"></a>Örnek
'''XML kodu<forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a>Örnek
Ayrıca hello ADFS sunucusunda powershell komutunu aşağıdaki hello yürüterek bir SAML talep belirtecinin ömrü verilen ADFS too15 ayarlanmalıdır hello dakika:
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <a id="proper-app-logout"></a>Uygulama hello uygulamasından uygun oturum kapatma

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Doğru oturum kapatma düğmesi kullanıcı basarsa oturum açtığınızda hello uygulamadan gerçekleştirin. Oturum kapatma sırasında uygulama kullanıcının oturumunu destroy de sıfırlama ve sıfırlama ve kimlik doğrulama tanımlama bilgisi değeri nullifying yanı sıra oturum tanımlama bilgisi değerini iptal edilmez. Birden çok oturumu bağlı tooa tek kullanıcı kimliği olduğunda, ayrıca, bunlar topluca hello sunucu tarafındaki zaman aşımı veya oturum kapatma ile bitmelidir. Son olarak, her sayfada oturum kapatma işlevselliği kullanılabilir olduğundan emin olun. |

## <a id="csrf-api"></a>ASP.NET Web API siteler arası istek sahteciliği (CSRF) saldırılarını karşı azaltmak

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web API | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Siteler arası istek sahtekarlığı (CSRF veya XSRF), bir saldırgan, farklı bir kullanıcının bir web sitesi kurulan oturum hello güvenlik bağlamında eylemleri gerçekleştirebilirsiniz saldırı türüdür. Merhaba hedef toomodify ya da hello hedeflenen web sitesi yalnızca oturum tanımlama bilgileri tooauthenticate alınan isteği dayalıysa içeriği silin. Bir saldırgan, üzerinde hello kullanıcı zaten oturum açık bir siteden bir URL bir komut ile farklı bir kullanıcının tarayıcı tooload alarak bu güvenlik açığından yararlanabilir. Gibi farklı bir web sitesi barındırma tarafından bir kaynak hello savunmasız sunucu veya alınırken hello kullanıcı tooclick bağlantı yükler, bir saldırganın toodo için birçok yolu vardır. Merhaba sunucu bir ek belirteç toohello istemci gönderir, bu tüm gelecekteki isteklerin belirteçte istemci tooinclude hello ve tüm gelecekteki isteklerin toohello geçerli oturum gibi ile ilgili bir belirteç içerdiğini doğrular gerektirir hello saldırı önlenebilir Merhaba ASP.NET AntiForgeryToken ya da ViewState kullanıyor. |

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web API | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | MVC5, MVC6 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [ASP.NET Web API'de siteler arası istek sahtekarlığı (CSRF) saldırılarını önleme](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| **Adımları** | Anti-CSRF ve AJAX: JSON verilerini, HTML form verilerini bir AJAX İsteği Gönder çünkü hello form simgesi AJAX istekleri için bir sorun olabilir. Özel bir HTTP üstbilgisi toosend hello belirteçleri bir çözümdür. Merhaba aşağıdaki kodu Razor sözdizimi toogenerate hello belirteçleri kullanır ve ardından hello belirteçleri tooan AJAX isteği ekler. |

### <a name="example"></a>Örnek
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>Örnek
Merhaba isteği işlerken hello belirteçleri hello isteği başlığından ayıklayın. Ardından toovalidate hello belirteçleri hello AntiForgery.Validate yöntemini çağırın. Merhaba belirteçleri geçerli değilse hello doğrulama yöntemi bir özel durum oluşturur.
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a>Örnek
Anti-CSRF ve ASP.NET MVC forms - kullanım hello AntiForgeryToken yardımcı yöntemi görünümleri; Örneğin, bir Html.AntiForgeryToken() hello forma koyun,
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a>Örnek
Yukarıdaki örnekte Hello hello aşağıdaki gibi bir şey çıkarır:
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>Örnek
Merhaba aynı zaman, bir tanımlama bilgisi ile aynı hello rastgele gizli değer yukarıda gösterilen olarak değeri hello __RequestVerificationToken olarak adlandırılan Html.AntiForgeryToken() verir hello ziyaretçi. Ardından, toovalidate gelen bir form post hello [ValidateAntiForgeryToken] filtre toohello hedef eylem yöntemine ekleyin. Örneğin:
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
Denetleyen yetkilendirme Filtresi:
* Merhaba gelen istek __RequestVerificationToken adlı bir tanımlama bilgisi içeriyor
* Merhaba gelen istek sahip bir `Request.Form` __RequestVerificationToken adlı giriş
* Bu tanımlama bilgisi ve `Request.Form` varsayılarak tüm değerleri Eşleştir iyi, hello isteği geçtiği normal olarak. Ancak değilse, ardından bir Yetkilendirme hatası iletisi "gerekli sahteciliğe karşı koruma belirteci belirtilmedi veya geçersiz".

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web API | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | MVC5, MVC6 |
| **Öznitelikleri**              | Kimlik sağlayıcısı - ADFS, kimlik sağlayıcısı - Azure AD |
| **Başvuruları**              | [Bireysel hesaplar ve ASP.NET Web API 2.2 yerel oturum açma ile Web API güvenliğini sağlama](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| **Adımları** | OAuth 2.0 kullanarak Hello Web API güvenliği, yalnızca hello belirteci geçerliyse sonra bir taşıyıcı belirteci yetkilendirme isteği üstbilgisi ve verir erişim toohello istekte bekler. Tanımlama bilgisi tabanlı kimlik doğrulaması, tarayıcılar hello taşıyıcı belirteçleri toorequests eklemeyin. İstemci tooexplicitly gereken Hello isteyen hello taşıyıcı belirteci hello istek üstbilgisi ekleyin. Bu nedenle, OAuth 2.0 kullanan korumalı ASP.NET Web API için taşıyıcı belirteçlerini CSRF saldırılarına karşı savunma hattı olarak değerlendirilir. Merhaba MVC hello uygulama kısmı form kimlik doğrulaması (yani, tanımlama bilgileri kullanır) kullanıyorsa, sahteciliğe karşı koruma belirteçleri hello MVC web uygulaması tarafından kullanılan toobe gerektiğini unutmayın. |

### <a name="example"></a>Örnek
Merhaba Web API sahip toobe haberdar toorely yalnızca taşıyıcı belirteçlerini ve tanımlama bilgileri üzerinde değil. Yapılandırmada aşağıdaki hello tarafından yapılabilir `WebApiConfig.Register` yöntemi: '''C-Sharp kod yapılandırma. SuppressDefaultHostAuthentication(); Config. Filters.Add (yeni HostAuthenticationFilter(OAuthDefaults.AuthenticationType));
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.
