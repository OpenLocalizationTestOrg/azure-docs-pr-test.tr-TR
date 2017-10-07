---
title: "aaaConfiguration Yönetimi - Microsoft tehdit modelleme aracı - Azure | Microsoft Docs"
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
ms.openlocfilehash: 77aa4352fa61e928a1b7a4ff1d488a55d3d9b970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-configuration-management--mitigations"></a>Güvenlik çerçevesi: Yapılandırma yönetimi | Azaltıcı Etkenler 
| Ürün/hizmet | Makale |
| --------------- | ------- |
| **Web uygulaması** | <ul><li>[İçerik güvenlik ilkesi (CSP) uygulamak ve satır içi javascript devre dışı bırak](#csp-js)</li><li>[Tarayıcının XSS filtresi etkinleştir](#xss-filter)</li><li>[ASP.NET uygulamaları izleme ve önceki toodeployment hata ayıklama devre dışı bırakmanız gerekir](#trace-deploy)</li><li>[Yalnızca güvenilir kaynaklardan gelen erişim üçüncü taraf JavaScript'ler](#js-trusted)</li><li>[Kimliği doğrulanmış ASP.NET sayfaları UI Redressing veya savunma tıklatın jacking dahil emin olun](#ui-defenses)</li><li>[ASP.NET Web uygulamalarını CORS etkinse, yalnızca güvenilir kaynaklara izin verildiğinden emin olun](#cors-aspnet)</li><li>[ASP.NET sayfaları ValidateRequest özniteliği etkinleştir](#validate-aspnet)</li><li>[JavaScript kitaplıklarını en son sürümlerini yerel olarak barındırılan kullanın](#local-js)</li><li>[Otomatik MIME algılaması devre dışı bırak](#mime-sniff)</li><li>[Windows Azure Web siteleri tooavoid sağlayan üzerinde standart sunucu başlıkları Kaldır](#standard-finger)</li></ul> |
| **Veritabanı** | <ul><li>[Veritabanı altyapısı erişimi için bir Windows Güvenlik Duvarı'nı yapılandırma](#firewall-db)</li></ul> |
| **Web API** | <ul><li>[ASP.NET Web API CORS etkinse, yalnızca güvenilir kaynaklara izin verildiğinden emin olun](#cors-api)</li><li>[Hassas verileri içeren Web API'nin yapılandırma dosyalarını bölümlerini şifrele](#config-sensitive)</li></ul> |
| **IOT cihaz** | <ul><li>[Tüm yönetim arabirimleri güçlü kimlik bilgileriyle güvenli olduğundan emin olmak](#admin-strong)</li><li>[Bilinmeyen kod cihazlarda yürütülemiyor emin olun](#unknown-exe)</li><li>[İşletim sistemi ve ek IOT cihaz bölümlerle bit kilidi şifrele](#partition-iot)</li><li>[Yalnızca hello minimum Hizmetleri/özellikleri aygıtlarda etkin olduğundan emin olun](#min-enable)</li></ul> |
| **IOT alan ağ geçidi** | <ul><li>[İşletim sistemi ve ek IOT alan ağ geçidi bölümlerle bit kilidi şifrele](#field-bit-locker)</li><li>[Merhaba alan ağ geçidi Hello varsayılan oturum açma kimlik bilgilerini yükleme sırasında değiştirilir emin olun](#default-change)</li></ul> |
| **IOT bulut ağ geçidi** | <ul><li>[Bu hello bulut ağ geçidi toodate ayarlama işlemi tookeep hello bağlı aygıtları üretici yazılımı uygulayan emin olun](#cloud-firmware)</li></ul> |
| **Makine güven sınırı** | <ul><li>[Aygıtları son nokta güvenlik denetimleri kuruluş ilkelerini uygun şekilde yapılandırılmış olduğundan emin olun](#controls-policies)</li></ul> |
| **Azure Depolama** | <ul><li>[Azure depolama erişim anahtarlarını güvenli yönetim emin olun](#secure-keys)</li><li>[CORS'yi Azure depolama alanında etkinse, yalnızca güvenilir kaynaklara izin verildiğinden emin olun](#cors-storage)</li></ul> |
| **WCF** | <ul><li>[WCF'ın hizmeti özellik azaltma etkinleştir](#throttling)</li><li>[Meta veri aracılığıyla WCF bilginin açığa çıkması](#info-metadata)</li></ul> | 

## <a id="csp-js"></a>İçerik güvenlik ilkesi (CSP) uygulamak ve satır içi javascript devre dışı bırak

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Bir giriş tooContent Güvenlik İlkesi](http://www.html5rocks.com/en/tutorials/security/content-security-policy/), [içerik güvenlik ilkesi başvurusu](http://content-security-policy.com/), [güvenlik özellikleri](https://developer.microsoft.com/microsoft-edge/platform/documentation/dev-guide/security/), [giriş toocontent Güvenlik İlkesi](https://docs.webplatform.org/wiki/tutorials/content-security-policy), [CSP kullanabilir miyim?](http://caniuse.com/#feat=contentsecuritypolicy) |
| **Adımları** | <p>İçerik güvenlik ilkesi (CSP) web uygulama sahipleri toohave denetim sitelerinde katıştırılmış hello içerikteki sağlayan bir savunma, güvenlik, standart, bir W3C mekanizmadır. CSP hello web sunucusunda bir HTTP yanıt üst bilgisi olarak eklenir ve hello istemci tarafında tarayıcılar tarafından zorlanır. Beyaz liste tabanlı bir ilke olduğunu - JavaScript yüklenebilir gibi bir Web sitesi hangi etkin içerik güvenilir etki alanlarından kümesi bildirebilirsiniz.</p><p>CSP güvenlik avantajlarından aşağıdaki hello sağlar:</p><ul><li>**XSS karşı koruma:** bir saldırgan, bir sayfa savunmasız tooXSS ise, 2 yollarla yararlanabilir:<ul><li>Eklenmeye `<script>malicious code</script>`. Bu yararlanma tooCSP'ın temel kısıtlama-1 nedeniyle çalışmaz</li><li>Eklenmeye `<script src=”http://attacker.com/maliciousCode.js”/>`. Merhaba denetlenen saldırgan etki alanlarının CSP'ın beyaz olmayacaktır bu yana bu yararlanma çalışmaz</li></ul></li><li>**Veri exfiltration üzerinde denetim:** bir Web sayfasındaki kötü amaçlı içerik tooconnect tooan dış Web sitesi ve çalar veri çalışırsa, CSP tarafından hello bağlantı iptal edilecek. Merhaba hedef etki alanına CSP'ın beyaz olmayacaktır Bunun nedeni</li><li>**Tıklatın jacking karşı savunma:** tıklatın jacking bir saldırı tekniği olan, bir saldırganın kullanarak orijinal bir Web sitesi çerçeve ve kullanıcı Arabirimi öğeleri kullanıcılar tooclick zorlar. Şu anda tıklatın jacking korunmanın bir yanıt üstbilgisi-X-Frame-Options yapılandırılarak elde edilir. Tüm tarayıcılar bu başlığı saygı ve iletme CSP giderek standart yol toodefend tıklatın jacking karşı olacaktır</li><li>**Gerçek zamanlı saldırı raporlama:** ekleme saldırının CSP özellikli bir Web sitesi varsa, tarayıcılar hello Web sunucusu üzerinde yapılandırılmış bir bildirim tooan uç noktası otomatik olarak tetikler. Bu şekilde, CSP gerçek zamanlı bir uyarı sistem olarak görev yapar.</li></ul> |

### <a name="example"></a>Örnek
Örnek İlkesi: 
```C#
Content-Security-Policy: default-src 'self'; script-src 'self' www.google-analytics.com 
```
Bu ilke yalnızca hello web uygulamasının server ve google analytics server gelen komut dosyalarını tooload sağlar. Başka bir siteden yüklenen komut dosyalarını reddedilir. Bir Web sitesinde CSP etkinleştirildiğinde, hello aşağıdaki otomatik olarak devre dışı toomitigate XSS saldırılarını özellikleridir. 

### <a name="example"></a>Örnek
Satır içi komut dosyaları çalıştırmaz. Satır içi komut dosyaları örnekleri aşağıda verilmiştir 
```javascript
<script> some Javascript code </script>
Event handling attributes of HTML tags (e.g., <button onclick=”function(){}”>
javascript:alert(1);
```

### <a name="example"></a>Örnek
Dizeleri kodu olarak değerlendirilmez. 
```javascript
Example: var str="alert(1)"; eval(str);
```

## <a id="xss-filter"></a>Tarayıcının XSS filtresi etkinleştir

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [XSS koruma filtresi](https://www.owasp.org/index.php/List_of_useful_HTTP_headers#X-XSS-Protection) |
| **Adımları** | <p>X XSS koruma yanıt üstbilgisi yapılandırma denetimleri hello tarayıcının siteler arası komut dosyası filtresi. Bu yanıt üstbilgisi değerleri aşağıdaki sahip olabilir:</p><ul><li>`0:`Bu durum, hello filtresi devre dışı bırakır</li><li>`1: Filter enabled`Siteler arası komut dosyası saldırı algılanırsa, sipariş toostop hello saldırısında, hello tarayıcı hello sayfa temizlenmeye</li><li>`1: mode=block : Filter enabled`. XSS saldırısı algılandığında hello sayfa temizlenmeye yerine hello tarayıcı hello sayfasının işleme engeller.</li><li>`1: report=http://[YOURDOMAIN]/your_report_URI : Filter enabled`. Merhaba tarayıcı hello sayfası ve rapor hello ihlali temizlenmeye.</li></ul><p>Bu CSP ihlali raporları toosend ayrıntıları tooa tercih ettiğiniz URI kullanılarak Chromium işlevdir. Merhaba son 2 seçenekleri güvenli değerleri olarak kabul edilir.</p>|

## <a id="trace-deploy"></a>ASP.NET uygulamaları izleme ve önceki toodeployment hata ayıklama devre dışı bırakmanız gerekir

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Genel Bakış hata ayıklama ASP.NET](http://msdn2.microsoft.com/library/ms227556.aspx), [ASP.NET izlemeye genel bakış](http://msdn2.microsoft.com/library/bb386420.aspx), [nasıl yapılır: bir ASP.NET uygulaması için izlemeyi etkinleştirmek](http://msdn2.microsoft.com/library/0x5wc973.aspx), [nasıl yapılır: ASP.NET uygulamaları için hata ayıklamayı etkinleştir](http://msdn2.microsoft.com/library/e8z01xdh(VS.80).aspx) |
| **Adımları** | İzleme başlangıç sayfası için etkinleştirildiğinde, ayrıca isteyen her tarayıcı iç sunucu durumu ve iş akışı hakkında veri içerir hello izleme bilgileri alır. Bu bilgileri güvenlik duyarlı olabilir. Hata ayıklama hello sayfa için etkinleştirildiğinde, tam yığın izleme verileri hello sunucu sonucu gerçekleştiği hataları toohello tarayıcı sunulmuştur. Bu verileri hello sunucunun iş akışıyla ilgili güvenlik bakımından hassas bilgiler getirebilir. |

## <a id="js-trusted"></a>Yalnızca güvenilir kaynaklardan gelen erişim üçüncü taraf JavaScript'ler

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | üçüncü taraf JavaScript'ler yalnızca güvenilir kaynaklardan gelen başvurulan. Merhaba başvuru uç noktalar, her zaman SSL olmalıdır. |

## <a id="ui-defenses"></a>Kimliği doğrulanmış ASP.NET sayfaları UI Redressing veya savunma tıklatın jacking dahil emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Savunma kopya sayfası tıklatın jacking OWASP](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet), [tıklatın jacking ile X-Frame-Options mücadele IE iç-Ayrıntılar](https://blogs.msdn.microsoft.com/ieinternals/2010/03/30/combating-click-jacking-with-x-frame-options/) |
| **Adımları** | <p>tıklatın jacking olarak da bilinen bir "UI redress", saldırısıdır bir saldırganın birden çok saydam veya donuk katmanları tootrick bir kullanıcı bir düğme veya bağlantı tıklamak kullandığında tooclick hello en üst düzey sayfasında planlayan zaman başka bir sayfada.</p><p>Katmanlama, kötü amaçlı bir sayfa hello kurbanın sayfasını yükler IFRAME ile hazırlayın tarafından sağlanır. Bu nedenle, hello saldırgan "ele" için kendi sayfası anlamına gelir ve büyük olasılıkla başka bir uygulama, etki alanı veya her ikisi tarafından sahip olunan tooanother sayfa yönlendirme tıklatır. tooprevent tıklatın jacking saldırıları, diğer etki alanlarından çerçeveleme, hello tarayıcı toonot yönlendiren kümesi hello uygun X-Frame-Options HTTP yanıt üstbilgilerini izin ver</p>|

### <a name="example"></a>Örnek
Merhaba X-FRAME-OPTIONS üstbilgisi IIS web.config ayarlanabilir. Web.config kod parçacığını hiçbir zaman Çerçeveli siteler için: 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="DENY"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

### <a name="example"></a>Örnek
Tarafından yalnızca Çerçeveli siteler için Web.config kod sayfaları hello aynı etki alanı: 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="SAMEORIGIN"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

## <a id="cors-aspnet"></a>ASP.NET Web uygulamalarını CORS etkinse, yalnızca güvenilir kaynaklara izin verildiğinden emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Web Forms, MVC5 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>Tarayıcı güvenlik bir web sayfası AJAX istekleri tooanother etki alanı bulunmasını önler. Bu kısıtlama hello aynı kaynak ilkesi adı verilir ve kötü amaçlı bir siteyi başka bir siteden hassas verileri okumasını önler. Ancak, bazen gerekli tooexpose API'leri güvenli olabilir, diğer siteleri kullanmasını sağlayabilirsiniz. Çıkış noktaları kaynak paylaşımı (CORS) arası bir sunucu toorelax hello kaynak aynı ilke sağlayan bir W3C standardıdır. CORS kullanarak, bir sunucu açıkça bazı cross-origin istekleri başkalarının reddetme çalışırken izin verebilirsiniz.</p><p>CORS daha güvenli ve JSONP gibi önceki teknikler daha esnektir. Özünde, CORS etkinleştirme tooadding birkaç HTTP yanıt üstbilgilerini çevirir (Access - Control-*) toohello web uygulaması ve bu yolla birkaç içinde yapılır.</p>|

### <a name="example"></a>Örnek
Erişim tooWeb.config varsa, CORS koddan hello eklenebilir: 
```XML
<system.webServer>
    <httpProtocol>
      <customHeaders>
        <clear />
        <add name="Access-Control-Allow-Origin" value="http://example.com" />
      </customHeaders>
    </httpProtocol>
```

### <a name="example"></a>Örnek
Erişim tooweb.config kullanılabilir durumda değilse, CORS CSharp koddan hello ekleyerek yapılandırılabilir: 
```C#
HttpContext.Response.AppendHeader("Access-Control-Allow-Origin", "http://example.com")
```

Lütfen kaynakları "Access-Control-Allow-Origin" öznitelik listesi hello kritik tooensure olduğuna dikkat edin ayarlayın çıkış tooa sonlu ve güvenilir kümesi. Tooconfigure bu açamayacağı başarısız (örn., ayar hello değeri olarak ' *') kötü amaçlı siteleri tootrigger origin istekleri arası toohello web uygulaması sağlayacak > herhangi bir kısıtlama olmadan, böylece hello uygulama savunmasız tooCSRF saldırıları yapma. 

## <a id="validate-aspnet"></a>ASP.NET sayfaları ValidateRequest özniteliği etkinleştir

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Web Forms, MVC5 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [İstek doğrulama - komut dosyası saldırılarını önleme](http://www.asp.net/whitepapers/request-validation) |
| **Adımları** | <p>İstek doğrulama, bir ASP.NET özelliği sürüm 1.1, bu yana hello sunucu içerik içeren beklemediğiniz kodlanmış HTML kabul etmesini engeller. Bu özellik tasarlanmıştır toohelp yapabildiği istemci komut dosyası kodu veya HTML olabilir depolanır ve tooother kullanıcılara sunulan bilmeyerek gönderilen tooa sunucu, bazı komut dosyası ekleme saldırıları önlemek. Hala tüm giriş verilerini doğrulamak ve HTML kodlama, uygun olduğunda öneririz.</p><p>İstek doğrulama, potansiyel olarak tehlikeli olabilecek değerler tüm giriş verilerini tooa listesi karşılaştırarak gerçekleştirilir. Bir eşleşme olursa, ASP.NET başlatır bir `HttpRequestValidationException`. Varsayılan olarak, istek doğrulama özelliği etkinleştirilir.</p>|

### <a name="example"></a>Örnek
Ancak, bu özellik sayfa düzeyinde devre dışı bırakılabilir: 
```XML
<%@ Page validateRequest="false" %> 
```
veya uygulama düzeyinde 
```XML
<configuration>
   <system.web>
      <pages validateRequest="false" />
   </system.web>
</configuration>
```
İstek doğrulama özellik desteklenmiyor ve MVC6 ardışık düzen parçası olmayan unutmayın. 

## <a id="local-js"></a>JavaScript kitaplıklarını en son sürümlerini yerel olarak barındırılan kullanın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>JQuery kullanmalısınız gibi standart JavaScript kitaplıklarını kullanarak geliştiriciler bilinen güvenlik açıkları içermeyen ortak JavaScript kitaplıklarını sürümleri onaylanmış. Eski sürümlerine bilinen güvenlik açıkları için güvenlik düzeltmelerini içerdikleri beri iyi bir uygulama toouse hello en son hello kitaplıkları sürümüdür.</p><p>Merhaba en son sürüm toocompatibility nedenleri kullanılamıyorsa, en düşük sürümlerle aşağıda hello kullanılmalıdır.</p><p>Kabul edilebilir en düşük sürümler:</p><ul><li>**JQuery**<ul><li>JQuery 1.7.1</li><li>JQueryUI 1.10.0</li><li>JQuery 1.9 doğrula</li><li>JQuery Mobile 1.0.1</li><li>JQuery döngüsü 2.99</li><li>JQuery DataTables 1.9.0</li></ul></li><li>**AJAX Denetim Araç Seti**<ul><li>AJAX Denetim Araç Seti 40412</li></ul></li><li>**ASP.NET Web formları ve Ajax**<ul><li>ASP.NET Web formları ve Ajax 4</li><li>ASP.NET Ajax 3.5</li></ul></li><li>**ASP.NET MVC**<ul><li>ASP.NET MVC 3.0</li></ul></li></ul><p>Hiçbir zaman genel CDN'ler gibi dış sitelerden herhangi bir JavaScript kitaplığı yüklenemiyor</p>|

## <a id="mime-sniff"></a>Otomatik MIME algılaması devre dışı bırak

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [IE8 güvenlik bölümü V: kapsamlı koruma](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx), [MIME türü](http://en.wikipedia.org/wiki/Mime_type) |
| **Adımları** | Merhaba içerik türü seçenekleri X başlığıdır geliştiricilerinin sağlayan bir HTTP üstbilgisi toospecify içeriklerini MIME sniffed olmamalıdır. Tasarlanmış toomitigate MIME algılaması saldırıları başlığıdır. Kullanıcı denetlenebilir içeriği içerebilir her bir sayfa için hello HTTP üst bilgisi X kullanmalısınız-içerik-tür-seçenekleri: nosniff. Merhaba aşağıdakilerden birini yapın tooenable hello gerekli üstbilgisi hello uygulamasındaki tüm sayfalar için genel olarak,|

### <a name="example"></a>Örnek
Internet Information Services (IIS tarafından) 7 veya sonraki sürümleri Merhaba uygulaması barındırılıyorsa hello üstbilgi hello web.config dosyasına ekleyin. 
```XML
<system.webServer>
<httpProtocol>
<customHeaders>
<add name="X-Content-Type-Options" value="nosniff"/>
</customHeaders>
</httpProtocol>
</system.webServer>
```

### <a name="example"></a>Örnek
Merhaba aracılığıyla Hello üstbilgisi Ekle genel uygulama\_BeginRequest 
```C#
void Application_BeginRequest(object sender, EventArgs e)
{
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
}
```

### <a name="example"></a>Örnek
Uygulama özel HTTP modülü 
```C#
public class XContentTypeOptionsModule : IHttpModule
{
#region IHttpModule Members
public void Dispose()
{
}
public void Init(HttpApplication context)
{
context.PreSendRequestHeaders += newEventHandler(context_PreSendRequestHeaders);
}
#endregion
void context_PreSendRequestHeaders(object sender, EventArgs e)
{
HttpApplication application = sender as HttpApplication;
if (application == null)
  return;
if (application.Response.Headers["X-Content-Type-Options "] != null)
  return;
application.Response.Headers.Add("X-Content-Type-Options ", "nosniff");
}
}
```

### <a name="example"></a>Örnek
Yalnızca belirli sayfaları için gereken üstbilgi hello tooindividual yanıtları ekleyerek etkinleştirebilirsiniz: 

```C#
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
```

## <a id="standard-finger"></a>Windows Azure Web siteleri tooavoid sağlayan üzerinde standart sunucu başlıkları Kaldır

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | EnvironmentType - Azure |
| **Başvuruları**              | [Standart sunucu üstbilgiler Windows Azure Web sitelerindeki kaldırılıyor](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/) |
| **Adımları** | X-gücü-tarafından sunucu gibi üstbilgileri X AspNet sürüm ortaya hello sunucusu ve teknolojileri temel hello hakkında bilgi. Toosuppress önerilir böylece sağlayan önleme bu üstbilgileri uygulama hello |

## <a id="firewall-db"></a>Veritabanı altyapısı erişimi için bir Windows Güvenlik Duvarı'nı yapılandırma

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | SQL Azure, OnPrem |
| **Öznitelikleri**              | Yok, SQL sürümü - V12 |
| **Başvuruları**              | [Nasıl tooconfigure bir Azure SQL veritabanı Güvenlik Duvarı](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/), [veritabanı altyapısı erişimi için bir Windows Güvenlik Duvarı'nı yapılandırma](https://msdn.microsoft.com/library/ms175043) |
| **Adımları** | Güvenlik Duvarı sistemlerini yetkisiz erişim toocomputer kaynakları önlemeye yardımcı olur. tooaccess bir güvenlik duvarı üzerinden hello SQL Server veritabanı altyapısı örneği, SQL Server tooallow Erişim çalıştıran hello bilgisayarda hello güvenlik duvarını yapılandırmanız gerekir |

## <a id="cors-api"></a>ASP.NET Web API CORS etkinse, yalnızca güvenilir kaynaklara izin verildiğinden emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web API | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | MVC 5 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [ASP.NET Web API 2 çıkış noktaları arası istekleri etkinleştirme](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api), [ASP.NET Web API - ASP.NET Web API 2 CORS desteği](https://msdn.microsoft.com/magazine/dn532203.aspx) |
| **Adımları** | <p>Tarayıcı güvenlik bir web sayfası AJAX istekleri tooanother etki alanı bulunmasını önler. Bu kısıtlama hello aynı kaynak ilkesi adı verilir ve kötü amaçlı bir siteyi başka bir siteden hassas verileri okumasını önler. Ancak, bazen gerekli tooexpose API'leri güvenli olabilir, diğer siteleri kullanmasını sağlayabilirsiniz. Çıkış noktaları kaynak paylaşımı (CORS) arası bir sunucu toorelax hello kaynak aynı ilke sağlayan bir W3C standardıdır.</p><p>CORS kullanarak, bir sunucu açıkça bazı cross-origin istekleri başkalarının reddetme çalışırken izin verebilirsiniz. CORS daha güvenli ve JSONP gibi önceki teknikler daha esnektir.</p>|

### <a name="example"></a>Örnek
Hello App_Start/WebApiConfig.cs, kod toohello WebApiConfig.Register yöntemi aşağıdaki hello ekleme 
```C#
using System.Web.Http;
namespace WebService
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // New code
            config.EnableCors();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
        }
    }
}
```

### <a name="example"></a>Örnek
EnableCors öznitelik bir denetleyicide uygulanan tooaction yöntemleri aşağıdaki gibi olabilir: 

```C#
public class ResourcesController : ApiController
{
  [EnableCors("http://localhost:55912", // Origin
              null,                     // Request headers
              "GET",                    // HTTP methods
              "bar",                    // Response headers
              SupportsCredentials=true  // Allow credentials
  )]
  public HttpResponseMessage Get(int id)
  {
    var resp = Request.CreateResponse(HttpStatusCode.NoContent);
    resp.Headers.Add("bar", "a bar value");
    return resp;
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "PUT",                          // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "POST",                         // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
}
```

Lütfen çıkış EnableCors öznitelik listesi hello kritik tooensure olduğuna dikkat edin ayarlayın çıkış tooa sonlu ve güvenilir kümesi. Tooconfigure bu açamayacağı başarısız (örn., hello değeri olarak ayarlama ' *') kötü amaçlı siteleri tootrigger kaynak istekleri toohello API herhangi bir kısıtlamanın olmadığı çapraz sağlayacak > böylece hello API savunmasız tooCSRF saldırıları yapma. Denetleyici düzeyinde EnableCors tasarlanabilir. 

### <a name="example"></a>Örnek
bir sınıftaki belirli bir yöntem üzerinde toodisable CORS özniteliği aşağıda gösterildiği gibi kullanılabilir DisableCors hello: 
```C#
[EnableCors("http://example.com", "Accept, Origin, Content-Type", "POST")]
public class ResourcesController : ApiController
{
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  // CORS not allowed because of hello [DisableCors] attribute
  [DisableCors]
  public HttpResponseMessage Delete(int id)
  {
    return Request.CreateResponse(HttpStatusCode.NoContent);
  }
}
```

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web API | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | MVC 6 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [ASP.NET Core 1.0 (CORS) çıkış noktaları arası istekleri etkinleştirme](https://docs.asp.net/en/latest/security/cors.html) |
| **Adımları** | <p>ASP.NET Core 1.0 CORS ara yazılımı kullanarak veya MVC kullanarak etkinleştirilebilir. Aynı CORS Hizmetleri kullanılır, ancak hello MVC tooenable CORS hello kullanırken CORS Ara değil.</p>|

**Yaklaşım 1** etkinleştirme CORS ara yazılımı ile: hello tüm uygulama için CORS tooenable hello CORS ara yazılımı toohello isteği hello UseCors genişletme yöntemi kullanarak işlem hattı ekleyin. Bir çıkış noktaları arası ilkesi hello CorsPolicyBuilder sınıfını kullanarak hello CORS Ara eklerken belirtilebilir. Vardır iki yolu toodo bu:

### <a name="example"></a>Örnek
Merhaba ilk toocall UseCors bir lambda sahip olur. Merhaba lambda CorsPolicyBuilder nesnesini alır: 
```C#
public void Configure(IApplicationBuilder app)
{
    app.UseCors(builder =>
        builder.WithOrigins("http://example.com")
        .WithMethods("GET", "POST", "HEAD")
        .WithHeaders("accept", "content-type", "origin", "x-custom-header"));
}
```

### <a name="example"></a>Örnek
Hello ikinci toodefine bir ya da daha fazla CORS ilkeleri ve ardından hello İlkesi tarafından çalışma zamanında adında adı. 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddCors(options =>
    {
        options.AddPolicy("AllowSpecificOrigin",
            builder => builder.WithOrigins("http://example.com"));
    });
}
public void Configure(IApplicationBuilder app)
{
    app.UseCors("AllowSpecificOrigin");
    app.Run(async (context) =>
    {
        await context.Response.WriteAsync("Hello World!");
    });
}
```

**Yaklaşım 2** etkinleştirme CORS mvc'de: geliştiricileri MVC tooapply alternatif olarak kullanabilir eylem, denetleyici başına veya genel olarak tüm denetleyicileri için başına belirli CORS.

### <a name="example"></a>Örnek
Eylem başına: toospecify belirli bir eylemi için CORS ilkesinin hello [EnableCors] özniteliği toohello eylemi ekleyin. Merhaba ilke adı belirtin. 
```C#
public class HomeController : Controller
{
    [EnableCors("AllowSpecificOrigin")] 
    public IActionResult Index()
    {
        return View();
    }
```

### <a name="example"></a>Örnek
Denetleyici: 
```C#
[EnableCors("AllowSpecificOrigin")]
public class HomeController : Controller
{
```

### <a name="example"></a>Örnek
Genel olarak: 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    services.Configure<MvcOptions>(options =>
    {
        options.Filters.Add(new CorsAuthorizationFilterFactory("AllowSpecificOrigin"));
    });
}
```
Lütfen çıkış EnableCors öznitelik listesi hello kritik tooensure olduğuna dikkat edin ayarlayın çıkış tooa sonlu ve güvenilir kümesi. Tooconfigure bu açamayacağı başarısız (örn., hello değeri olarak ayarlama ' *') kötü amaçlı siteleri tootrigger kaynak istekleri toohello API herhangi bir kısıtlamanın olmadığı çapraz sağlayacak > böylece hello API savunmasız tooCSRF saldırıları yapma. 

### <a name="example"></a>Örnek
Denetleyici veya eylemin, kullanım hello [DisableCors] özniteliği için CORS toodisable. 
```C#
[DisableCors]
    public IActionResult About()
    {
        return View();
    }
```

## <a id="config-sensitive"></a>Hassas verileri içeren Web API'nin yapılandırma dosyalarını bölümlerini şifrele

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web API | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Nasıl yapılır: ASP.NET 2.0 kullanarak DPAPI yapılandırma bölümlerinin şifrelemek](https://msdn.microsoft.com/library/ff647398.aspx), [korumalı bir yapılandırma sağlayıcısı belirtme](https://msdn.microsoft.com/library/68ze1hb2.aspx), [kullanarak Azure anahtar kasası tooprotect uygulama parolaları](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/) |
| **Adımları** | Yapılandırma dosyaları gibi hello Web.config appsettings.json durumda sık kullanılan kullanıcı adları, parolalar, veritabanı bağlantı dizelerini ve şifreleme anahtarları dahil olmak üzere toohold hassas bilgileri. Bu bilgileri korumak, uygulamanızın savunmasız tooattackers veya kötü niyetli kullanıcıların hesap kullanıcı adları ve parolalar, veritabanı adları ve sunucu adları gibi hassas bilgileri alma olur. (Azure/şirket içi) Hello dağıtım türüne göre hello hassas DPAPI veya Azure anahtar kasası gibi hizmetleri kullanarak yapılandırma dosyalarını bölümlerini şifreler. |

## <a id="admin-strong"></a>Tüm yönetim arabirimleri güçlü kimlik bilgileriyle güvenli olduğundan emin olmak

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT cihaz | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Her yönetim hello aygıt arabirimleri veya alan ağ geçidi çıkarır güçlü kimlik bilgilerini kullanarak korunması. Ayrıca, WiFi, SSH herhangi diğer bir arabirimleri ister, dosya paylaşımları, FTP güçlü kimlik bilgileri ile güvenli hale getirilmelidir. Varsayılan Zayıf parolalar kullanılmamalıdır. |

## <a id="unknown-exe"></a>Bilinmeyen kod cihazlarda yürütülemiyor emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT cihaz | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Güvenli Önyükleme ve Windows 10 IOT Core üzerinde bit kilidi cihaz şifrelemeyi etkinleştirme](https://developer.microsoft.com/windows/iot/win10/sb_bl) |
| **Adımları** | UEFI Güvenli Önyükleme kısıtlayan hello sistem tooonly belirtilen yetkilisi tarafından imzalanmış ikili dosyaların yürütülmesine izin verebilir. Bu özellik bilinmeyen kod hello platformuna yürütülen ve büyük olasılıkla bunu hello güvenlik tutumunu zayıflatmanın engeller. UEFI Güvenli Önyükleme etkinleştirmek ve kod imzalama için güvenilen sertifika yetkilileri listesi hello kısıtlayın. Güvenilen başlangıç yetkililerinden biriyle kullanarak hello cihaza dağıtılan tüm kod oturum açın. |

## <a id="partition-iot"></a>İşletim sistemi ve ek IOT cihaz bölümlerle bit kilidi şifrele

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT cihaz | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Windows 10 IOT Core hafif bir sürümüdür ve TPM hello gerekli ölçümleri yürütür UEFI'da hello gerekli preOS Protokolü dahil olmak üzere hello platformunda hello varlığını üzerinde güçlü bir bağımlılığa sahip bit kilidi cihaz şifreleme uygular. Bu preOS ölçümlerinin işletim sistemi daha sonra hello OS nasıl başlatıldı kesin kaydını sahip o hello emin olun. Herhangi bir duyarlı veri depolamak durumda bit kasası ve herhangi bir ek bölümü de kullanarak işletim sistemi bölümleri şifreleyin. |

## <a id="min-enable"></a>Yalnızca hello minimum Hizmetleri/özellikleri aygıtlarda etkin olduğundan emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT cihaz | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Etkinleştirmeyin veya herhangi bir özellik veya hello hello hello çözüm çalışması için gerekli olmayan işletim sistemi Hizmetleri'nde kapatın. İçin örneğin hello cihaz dağıtılan bir UI toobe gerektirmiyorsa, Windows IOT Core gözetimsiz modunda yüklemeniz gerekir. |

## <a id="field-bit-locker"></a>İşletim sistemi ve ek IOT alan ağ geçidi bölümlerle bit kilidi şifrele

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT alan ağ geçidi | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Windows 10 IOT Core hafif bir sürümüdür ve TPM hello gerekli ölçümleri yürütür UEFI'da hello gerekli preOS Protokolü dahil olmak üzere hello platformunda hello varlığını üzerinde güçlü bir bağımlılığa sahip bit kilidi cihaz şifreleme uygular. Bu preOS ölçümlerinin işletim sistemi daha sonra hello OS nasıl başlatıldı kesin kaydını sahip o hello emin olun. Herhangi bir duyarlı veri depolamak durumda bit kasası ve herhangi bir ek bölümü de kullanarak işletim sistemi bölümleri şifreleyin. |

## <a id="default-change"></a>Merhaba alan ağ geçidi Hello varsayılan oturum açma kimlik bilgilerini yükleme sırasında değiştirilir emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT alan ağ geçidi | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Merhaba alan ağ geçidi Hello varsayılan oturum açma kimlik bilgilerini yükleme sırasında değiştirilir emin olun |

## <a id="cloud-firmware"></a>Bu hello bulut ağ geçidi toodate ayarlama işlemi tookeep hello bağlı aygıtları üretici yazılımı uygulayan emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT bulut ağ geçidi | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Ağ geçidi seçim - Azure IOT Hub |
| **Başvuruları**              | [IOT Hub cihaz yönetimine genel bakış](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-overview/), [nasıl tooupdate cihaz üretici yazılımı](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-device-jobs/) |
| **Adımları** | LWM2M hello açık mobil Alliance IOT cihaz yönetimi için gelen bir protokoldür. Azure IOT cihaz yönetimi ile fiziksel cihazları Cihaz işleri kullanarak toointeract sağlar. Bu hello bulut ağ geçidi bir işlem tooroutinely Koru hello aygıtı ve diğer yapılandırma verilerini Azure IOT Hub cihaz yönetimini kullanarak toodate uygulayan emin olun. |

## <a id="controls-policies"></a>Aygıtları son nokta güvenlik denetimleri kuruluş ilkelerini uygun şekilde yapılandırılmış olduğundan emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Makine güven sınırı | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Aygıtları bit kilidi disk düzeyinde şifreleme, güncelleştirilmiş imzalarla virüsten koruma gibi son nokta güvenlik denetimleri, ana bilgisayar tabanlı güvenlik duvarı, işletim sistemi yükseltme, vb. Kurumsal güvenlik ilkelerini uygun şekilde yapılandırılmış ilkeler Grup dikkat emin olun. |

## <a id="secure-keys"></a>Azure depolama erişim anahtarlarını güvenli yönetim emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Storage | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Azure depolama Güvenlik Kılavuzu - bilgisayarınızı depolama hesabı anahtarlarını yönetme](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_managing-your-storage-account-keys) |
| **Adımları** | <p>Anahtar depolama: Toostore hello Azure depolama erişim tuşlarını gizli olarak Azure anahtar Kasası'nda önerilir ve başlangıç anahtarı anahtar Kasası'nı alıp hello uygulamalara sahip. Bu son toohello aşağıdaki önerilir nedenler:</p><ul><li>Merhaba uygulaması hiçbir zaman hello depolama anahtar sabit kodlanmış birisi toohello anahtarları belirli izinsiz erişim sağlama, o avenue kaldıran bir yapılandırma dosyası sahip olacaktır</li><li>Erişim toohello tuşları, Azure Active Directory kullanılarak denetlenebilir. Başka bir deyişle, bir hesap sahibi tooretrieve hello anahtarları Azure anahtar kasası ihtiyaç duyan uygulamalar toohello sayıda erişim verebilirsiniz. Diğer uygulamalar, özellikle izin verme olmadan mümkün tooaccess hello anahtarları olmayacaktır.</li><li>Anahtarını yeniden üretme: Güvenlik nedenleriyle toohave bir işlemde yer tooregenerate Azure depolama erişim tuşlarını önerilir. Makale neden ve nasıl tooplan anahtarını yeniden üretme konusunda belgelenir için hello Azure depolama Güvenlik Kılavuzu ile ilgili ayrıntılar başvurusu</li></ul>|

## <a id="cors-storage"></a>CORS'yi Azure depolama alanında etkinse, yalnızca güvenilir kaynaklara izin verildiğinden emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Storage | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Hello Azure Storage Hizmetleri için CORS desteği](https://msdn.microsoft.com/library/azure/dn535601.aspx) |
| **Adımları** | Azure depolama tooenable CORS – arası kaynak paylaşımı kaynak sağlar. Her Depolama hesabı için bu depolama hesabı hello kaynaklara erişebilir etki alanları belirtebilirsiniz. Varsayılan olarak, CORS tüm hizmetleri devre dışıdır. CORS hello REST API veya hello depolama istemci kitaplığı toocall hello yöntemleri tooset hello hizmet ilkelerinden birini kullanarak etkinleştirebilirsiniz. |

## <a id="throttling"></a>WCF'ın hizmeti özellik azaltma etkinleştir

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | WCF | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | .NET framework 3 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Krallık Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Adımları** | <p>Bir sınır hello yerleştirme değil kullanımını sistem kaynakları Kaynak Tükenmesi ve sonuçta hizmet reddine neden olabilir.</p><ul><li>**Açıklama:** Windows Communication Foundation (WCF) hello özelliği toothrottle hizmet istekleri sunar. Çok fazla sayıda istemci isteklerini izin vererek, bir sistem bölgesini doldurmak ve kaynaklarını tüketebilir. Merhaba üzerinde tooa hizmet istekleri yalnızca az sayıda izin vererek, diğer yandan hello hizmetini kullanarak yetkili kullanıcıları engelleyebilir. Her hizmet yapılandırılmış tek tek bizi tooand tooallow hello uygun miktarda kaynak olmalıdır.</li><li>**Öneriler** etkinleştirmek WCF'ın Hizmeti azaltma özelliğini ve kümesi sınırları, uygulamanız için uygun.</li></ul>|

### <a name="example"></a>Örnek
Merhaba, azaltma etkinleştirildi ile örnek bir yapılandırma aşağıdadır:
```
<system.serviceModel> 
  <behaviors>
    <serviceBehaviors>
    <behavior name="Throttled">
    <serviceThrottling maxConcurrentCalls="[YOUR SERVICE VALUE]" maxConcurrentSessions="[YOUR SERVICE VALUE]" maxConcurrentInstances="[YOUR SERVICE VALUE]" /> 
  ...
</system.serviceModel> 
```

## <a id="info-metadata"></a>Meta veri aracılığıyla WCF bilginin açığa çıkması

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | WCF | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | .NET framework 3 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Krallık Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Adımları** | Meta veri hello sistemi hakkında bilgi edinin ve saldırı form planı saldırganlar yardımcı olabilir. WCF hizmetleri yapılandırılmış tooexpose meta verileri olabilir. Meta veri ayrıntılı hizmet açıklaması bilgilerini sağlar ve üretim ortamlarında yayını değil. Merhaba `HttpGetEnabled`  /  `HttpsGetEnabled` hello ServiceMetaData sınıfının özelliklerine tanımlayan bir hizmet hello meta verileri açığa çıkarır | 

### <a name="example"></a>Örnek
Aşağıdaki Hello kodu WCF toobroadcast bir hizmetin meta veri bildirir.
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior();
smb.HttpGetEnabled = true; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb); 
```
Hizmet meta verilerini bir üretim ortamında yayın değil. Merhaba de ayarlamak / sınıf toofalse hello ServiceMetaData de özellikleri. 

### <a name="example"></a>Örnek
Aşağıdaki Hello kodu, bir hizmetin meta veri WCF toonot yayın bildirir. 
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior(); 
smb.HttpGetEnabled = false; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb);
```
