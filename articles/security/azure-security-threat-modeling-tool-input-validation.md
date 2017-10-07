---
title: "aaaInput doğrulama - Microsoft tehdit modelleme aracı - Azure | Microsoft Docs"
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
ms.openlocfilehash: 823503881f4bae292ef021834d5e64acf2a0f54a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-input-validation--mitigations"></a>Güvenlik çerçevesi: Giriş doğrulama | Azaltıcı Etkenler 
| Ürün/hizmet | Makale |
| --------------- | ------- |
| **Web uygulaması** | <ul><li>[XSLT güvenilmeyen stil sayfalarını kullanarak tüm dönüşümler için komut dosyası devre dışı bırak](#disable-xslt)</li><li>[Kullanıcı denetlenebilir içeriği içerebilir her sayfanın MIME otomatik algılaması dışında çevrilir emin olun](#out-sniffing)</li><li>[Sağlamlaştırmak veya XML varlık çözümleme devre dışı bırakma](#xml-resolution)</li><li>[HTTP.sys kullanan uygulamalar URL Standartlaştırma doğrulama gerçekleştirme](#app-verification)</li><li>[Uygun denetimleri dosyaların kullanıcılardan kabul ederken karşılandığından emin olun](#controls-users)</li><li>[Tür kullanımı uyumlu parametreleri veri erişimi için Web uygulamasında kullanıldığından emin olun](#typesafe)</li><li>[Ayrı model bağlama sınıflarını kullanın veya bağlama filtresi tooprevent MVC yığın atama güvenlik açığı listeler](#binding-mvc)</li><li>[Güvenilmeyen web çıkış önceki toorendering kodlama](#rendering)</li><li>[Giriş doğrulaması ve tüm dize türünde Model özelliklerini filtrelemesine](#typemodel)</li><li>[Tüm karakterleri, örneğin, Zengin Metin Düzenleyicisi'ni kabul eden form alanlarını temizleme işlemi uygulanmalıdır](#richtext)</li><li>[Yerleşik kodlama olmayan DOM öğeleri toosinks atamayın](#inbuilt-encode)</li><li>[Tüm doğrulama yeniden yönlendirmeleri hello uygulamadaki kapalı veya güvenli bir şekilde tamamlandı](#redirect-safe)</li><li>[Uygulama giriş doğrulaması denetleyicisi yöntemler tarafından kabul edilen tüm dize türü parametreleri](#string-method)</li><li>[Normal ifade tooprevent DoS toobad normal ifadeler nedeniyle işleme için üst sınır zaman aşımını ayarlama](#dos-expression)</li><li>[Razor görünümleri Html.Raw kullanmaktan kaçının](#html-razor)</li></ul> | 
| **Veritabanı** | <ul><li>[Dinamik sorgular saklı yordamlarda kullanmayın](#stored-proc)</li></ul> |
| **Web API** | <ul><li>[Model doğrulama Web API yöntemlerini yapıldığından emin olun](#validation-api)</li><li>[Web API yöntemleri tarafından kabul edilen tüm dize tür parametrelerindeki giriş doğrulaması uygulama](#string-api)</li><li>[Tür kullanımı uyumlu parametreleri Web API'si veri erişimi için kullanıldığından emin olun](#typesafe-api)</li></ul> | 
| **Azure belge DB** | <ul><li>[DocumentDB için parametreli SQL sorgularını kullan](#sql-docdb)</li></ul> | 
| **WCF** | <ul><li>[Şema bağlama aracılığıyla WCF girişi doğrulama](#schema-binding)</li><li>[Parametre denetçiler aracılığıyla WCF girişi doğrulama](#parameters)</li></ul> |

## <a id="disable-xslt"></a>XSLT güvenilmeyen stil sayfalarını kullanarak tüm dönüşümler için komut dosyası devre dışı bırak

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [XSLT güvenlik](https://msdn.microsoft.com/library/ms763800(v=vs.85).aspx), [XsltSettings.EnableScript özelliği](http://msdn.microsoft.com/library/system.xml.xsl.xsltsettings.enablescript.aspx) |
| **Adımları** | XSLT destekleyen hello kullanarak stil sayfaları komut dosyası `<msxml:script>` öğesi. Bu, bir XSLT dönüşümü kullanılan özel işlevler toobe sağlar. Merhaba betik hello hello dönüştürme gerçekleştirme hello işlem bağlamında çalıştırılır. XSLT betik yürütmesinde bir güvenilmeyen ortamı tooprevent güvenilmeyen kod zaman devre dışı bırakılması gerekir. *.NET kullanıyorsanız:* varsayılan olarak XSLT komut dosyası devre dışı; ancak, açıkça hello etkinleştirilmemiş olduğundan emin olmalısınız `XsltSettings.EnableScript` özelliği.|

### <a name="example"></a>Örnek 

```C#
XsltSettings settings = new XsltSettings();
settings.EnableScript = true; // WRONG: THIS SHOULD BE SET toofalse
```

### <a name="example"></a>Örnek
XSLT komut dosyası, MSXML 6.0 kullanarak kullanıyorsanız, varsayılan olarak devre dışıdır; Ancak, bunu açıkça hello XML DOM nesnesi özelliği AllowXsltScript üzerinden etkinleştirilmemiş olduğundan emin olmalısınız. 

```C#
doc.setProperty("AllowXsltScript", true); // WRONG: THIS SHOULD BE SET toofalse
```

### <a name="example"></a>Örnek
MSXML 5 kullanıyorsanız veya aşağıda XSLT komut dosyası varsayılan olarak etkindir ve açıkça gerekir devre dışı bırakın. Merhaba XML DOM nesnesi özelliği AllowXsltScript toofalse ayarlayın. 

```C#
doc.setProperty("AllowXsltScript", false); // CORRECT. Setting toofalse disables XSLT scripting.
```

## <a id="out-sniffing"></a>Kullanıcı denetlenebilir içeriği içerebilir her sayfanın MIME otomatik algılaması dışında çevrilir emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [IE8 Güvenlik bölümü V - kapsamlı koruma](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)  |
| **Adımları** | <p>Kullanıcı denetlenebilir içeriği içerebilir her bir sayfa için hello HTTP üstbilgisi kullanmalısınız `X-Content-Type-Options:nosniff`. toocomply bu gereksinime ya da kümesi hello gerekli üstbilgisi yalnızca kullanıcı denetlenebilir içerik içerebilir sayfalar için sayfa tarafından olabilir veya genel hello uygulamadaki tüm sayfalar için ayarlayabilirsiniz.</p><p>Her bir web sunucusundan teslim dosya ilişkili bir türü [MIME türü](http://en.wikipedia.org/wiki/Mime_type) (olarak da adlandırılan bir *içerik türü*) hello İhlale hello içeriğin (diğer bir deyişle, görüntü, metin, uygulama, vb.) açıklanır</p><p>Merhaba içerik türü seçenekleri X başlığıdır geliştiricilerinin sağlayan bir HTTP üstbilgisi toospecify içeriklerini MIME sniffed olmamalıdır. Tasarlanmış toomitigate MIME algılaması saldırıları başlığıdır. Internet Explorer 8 (IE8) bu başlığı için destek eklendi</p><p>Yalnızca Internet Explorer 8 (IE8) kullanıcılarının X-içerik-tür-seçeneklerden yararlanabilir. Internet Explorer'ın önceki sürümlerini şu anda hello X-içerik-tür-Options üstbilgisi dikkate almaz</p><p>Internet Explorer 8 (ve üstü) hello yalnızca başlıca tarayıcılar tooimplement MIME algılaması çevirin özelliği. Diğer ana tarayıcılar (Firefox, Safari, Chrome) benzer özellikleri varsa ve uyguladığınızda, bu öneri de bu tarayıcılar için güncelleştirilmiş tooinclude sözdizimi olacaktır</p>|

### <a name="example"></a>Örnek
tooenable hello gerekli üstbilgisi hello uygulamasındaki tüm sayfalar için genel olarak, hello aşağıdakilerden birini yapabilirsiniz: 

* Merhaba uygulaması Internet Information Services (IIS) 7 tarafından barındırılıyorsa hello web.config dosyasında hello üstbilgisi Ekle 

```
<system.webServer> 
  <httpProtocol> 
    <customHeaders> 
      <add name=""X-Content-Type-Options"" value=""nosniff""/>
    </customHeaders>
  </httpProtocol>
</system.webServer> 
```

* Merhaba aracılığıyla Hello üstbilgisi Ekle genel uygulama\_BeginRequest 

``` 
void Application_BeginRequest(object sender, EventArgs e)
{
  this.Response.Headers[""X-Content-Type-Options""] = ""nosniff"";
} 
```

* Uygulama özel HTTP modülü 

``` 
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
        if (application.Response.Headers[""X-Content-Type-Options ""] != null) 
          return; 
        application.Response.Headers.Add(""X-Content-Type-Options "", ""nosniff""); 
      } 
  } 

``` 

* Yalnızca belirli sayfaları için gereken üstbilgi hello tooindividual yanıtları ekleyerek etkinleştirebilirsiniz: 

```
this.Response.Headers[""X-Content-Type-Options""] = ""nosniff""; 
``` 

## <a id="xml-resolution"></a>Sağlamlaştırmak veya XML varlık çözümleme devre dışı bırakma

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [XML varlık genişletme](http://capec.mitre.org/data/definitions/197.html), [XML hizmet reddi saldırılarına ve savunma](http://msdn.microsoft.com/magazine/ee335713.aspx), [MSXML güvenliğine genel bakış](http://msdn.microsoft.com/library/ms754611(v=VS.85).aspx), [MSXML kod güvenliğini sağlamak için en iyi uygulamalar](http://msdn.microsoft.com/library/ms759188(VS.85).aspx), [NSXMLParserDelegate Protokolü başvurusu](http://developer.apple.com/library/ios/#documentation/cocoa/reference/NSXMLParserDelegate_Protocol/Reference/Reference.html), [dış başvuruları çözme](https://msdn.microsoft.com/library/5fcwybb2.aspx) |
| **Adımları**| <p>Yaygın olarak kullanılmaz rağmen izin veren hello XML Ayrıştırıcı tooexpand makrosu varlıklar hello belge kendisini içinde veya dış kaynaklardan tanımlanan değerlerle XML özelliği yoktur. Örneğin, metin her zaman hello böylece hello belge bir varlık "Şirket" adı "Microsoft" Merhaba değerle tanımlayabilir "&companyname;", otomatik olarak değiştirilir Microsoft hello metinle hello belgede görüntülenir. Veya, bir varlık "bir dış web hizmeti toofetch hello geçerli değeri Microsoft hisse senedi başvuran MSFTStock" Merhaba belge tanımlayabilirsiniz.</p><p>Sonra her zaman "&MSFTStock;" hello belgede bunu otomatik olarak değiştirilir hello geçerli stok fiyatıyla görünür. Ancak, bu işlev kötüye toocreate reddi (DoS) hizmet koşulları olabilir. Bir saldırgan, birden çok varlık toocreate hello sistemdeki tüm kullanılabilir bellek tüketir üstel genişletme XML Bomba yerleştirebilirsiniz. </p><p>Alternatif olarak, kendisinin geri akışları bir dış başvuru sonsuz bir veri miktarı oluşturabilir veya, yalnızca hello iş parçacığı askıda kalır. Tamamen kendi uygulama değil, kullanıyorsanız veya el ile Merhaba miktarda bellek ve bu işlevselliği ise Merhaba uygulaması varlık çözümlemesi için tüketebileceği süre sınırı sonuç olarak, tüm takımlar iç ve/veya dış XML varlık çözümleme devre dışı bırakmanız gerekir kesinlikle gerekli. Varlık çözümleme, uygulamanız tarafından gerekli değildir, sonra da devre dışı bırakın. </p>|

### <a name="example"></a>Örnek
.NET Framework kodunu yaklaşımlar aşağıdaki hello kullanabilirsiniz:

```C#
XmlTextReader reader = new XmlTextReader(stream);
reader.ProhibitDtd = true;

XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);

// for .NET 4
XmlReaderSettings settings = new XmlReaderSettings();
settings.DtdProcessing = DtdProcessing.Prohibit;
XmlReader reader = XmlReader.Create(stream, settings);
```
Bu hello varsayılan değeri Not `ProhibitDtd` içinde `XmlReaderSettings` ancak doğrudur `XmlTextReader` false olur. In kapsama kullanıyorsanız, tooset ProhibitDtd tootrue açıkça gerekmez, ancak güvenliği artırmak amacıyla için bunu yapmanız önerilir. Ayrıca hello XmlDocument sınıfı varsayılan varlık çözümleme izin verildiğini unutmayın. 

### <a name="example"></a>Örnek
XML belgelerine uymasıdır, kullanım hello toodisable varlık çözümlenmek `XmlDocument.Load(XmlReader)` hello aşırı yükleme yöntemi ve hello uygun özellikleri hello XmlReader bağımsız değişkeni toodisable çözümlemesinde hello kod aşağıdaki gösterildiği gibi: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);
XmlDocument doc = new XmlDocument();
doc.Load(reader);
```

### <a name="example"></a>Örnek
Varlık çözümlemeyi devre dışı bırakma, uygulamanız için mümkün değilse, hello XmlReaderSettings.MaxCharactersFromEntities özelliği tooa uygun değere tooyour uygulamanın gereksinimlerine göre ayarlayın. Bu olası üstel genişletme DoS saldırıları hello etkisini sınırlar. koddan hello Bu yaklaşımın bir örnek sağlar: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
XmlReader reader = XmlReader.Create(stream, settings);
```

### <a name="example"></a>Örnek
Tooresolve satır içi varlıkları gerekiyorsa ancak tooresolve dış varlıklar gerekmez hello XmlReaderSettings.XmlResolver özelliği toonull ayarlayın. Örneğin: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
settings.XmlResolver = null;
XmlReader reader = XmlReader.Create(stream, settings);
```
Msxml6 içinde ProhibitDTD tootrue (DTD işlemeyi devre dışı bırakma) varsayılan olarak ayarlanır. Apple OSX/iOS kodu için kullanabileceğiniz iki XML ayrıştırıcıları vardır: NSXMLParser ve libXML2. 

## <a id="app-verification"></a>HTTP.sys kullanan uygulamalar URL Standartlaştırma doğrulama gerçekleştirme

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>Http.sys kullanan herhangi bir uygulama bu yönergeleri izlemelidir:</p><ul><li>Merhaba URL uzunluğu toono birden fazla 16.384 karakter (ASCII veya Unicode) sınırlayın. Merhaba varsayılan Internet Information Services (IIS) 6 ayarına göre hello mutlak URL uzunluğu üst sınırı budur. Web siteleri bu değerden daha kısa bir süre için mümkünse çaba</li><li>Bunlar hello kurallı kullanım kuralları hello .NET FX yararlanır gibi hello standart .NET Framework dosyası g/ç sınıfları (örneğin, FILESTREAM) kullanın</li><li>Açıkça bilinen dosya adları, bir izin verilenler listesi oluşturma</li><li>Açıkça bilinen dosya türleri, değil hizmet UrlScan reddeder reddetme: exe bat, cmd, com, htw, IDA, IDQ, htr, IDC, shtm [l], stm, yazıcı, INI, pol, verilerinin dosyaları</li><li>Özel durumlar aşağıdaki hello catch:<ul><li>System.ArgumentException (için aygıt adları)</li><li>System.NotSupportedException (için veri akışları)</li><li>System.IO.FileNotFoundException (için geçersiz kaçış karakterli dosya adları)</li><li>System.IO.directorynotfoundexception (için geçersiz kaçış karakterli dizin)</li></ul></li><li>*Sağlamadığı* tooWin32 dosya g/ç API'leri çağırın. Geçersiz bir URL düzgün biçimde 400 hatası toohello kullanıcı dönün ve hello gerçek hata günlüğüne.</li></ul>|

## <a id="controls-users"></a>Uygun denetimleri dosyaların kullanıcılardan kabul ederken karşılandığından emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Kısıtlanmamış karşıya dosya yükleme](https://www.owasp.org/index.php/Unrestricted_File_Upload), [dosya imza tablosu](http://www.garykessler.net/library/file_sigs.html) |
| **Adımları** | <p>Karşıya yüklenen dosyaların önemli riski tooapplications temsil eder.</p><p>Merhaba ilk saldırıların çoğu bazı kod toohello sistem toobe saldırıya tooget adımdır. Ardından hello saldırı, yalnızca bir şekilde tooget hello kodu yürütülen toofind gerekir. Bir dosyayı karşıya yükleme kullanarak hello ilk adımı gerçekleştirmek hello saldırgan yardımcı olur. sınırsız dosya karşıya yükleme Hello sonuçlarını, tam sistem devralma dahil olmak üzere, bir aşırı yüklenmiş dosya sistemi veya saldırıları tooback uç sistemleri ve basit tahrifatı iletme veritabanı değişebilir.</p><p>Hangi hello uygulama karşıya hello dosyasıyla yapar ve özellikle depolandığı bağlıdır. Sunucu tarafı dosya yüklemeleriyle doğrulanması eksik. Güvenlik denetimleri aşağıdaki dosyayı karşıya yüklemeyi işlevselliği için uygulanması gerekir:</p><ul><li>Dosya uzantısı onay (izin verilen dosya türü için geçerli bir kümesi kabul)</li><li>En büyük dosya boyutu sınırı</li><li>Dosya karşıya yüklenen toowebroot olmamalıdır; Başlangıç konumu sistem dışı sürücü üzerinde bir dizin olmalıdır</li><li>Merhaba karşıya yüklenen dosya adına sahip olacağı şekilde bazı rastgele tooprevent dosyasının üzerine yazar için adlandırma kuralı gelmelidir</li><li>Dosyalar için virüsten koruma toohello disk yazmadan önce taranmış</li><li>Merhaba dosya adını ve diğer meta verileri (örneğin, dosya yolu) için kötü amaçlı karakter doğrulandığından emin olmak</li><li>Dosya biçimi imza işaretlenmelidir, tooprevent masqueraded dosya karşıya bir kullanıcının (örneğin, bir exe dosyası uzantısı tootxt değiştirerek karşıya yükleme)</li></ul>| 

### <a name="example"></a>Örnek
Merhaba son noktası için dosya biçimi imza doğrulaması ile ilgili ayrıntılar için aşağıda toohello sınıfı bakın: 

```C#
        private static Dictionary<string, List<byte[]>> fileSignature = new Dictionary<string, List<byte[]>>
                    {
                    { ".DOC", new List<byte[]> { new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 } } },
                    { ".DOCX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".PDF", new List<byte[]> { new byte[] { 0x25, 0x50, 0x44, 0x46 } } },
                    { ".ZIP", new List<byte[]> 
                                            {
                                              new byte[] { 0x50, 0x4B, 0x03, 0x04 },
                                              new byte[] { 0x50, 0x4B, 0x4C, 0x49, 0x54, 0x55 },
                                              new byte[] { 0x50, 0x4B, 0x53, 0x70, 0x58 },
                                              new byte[] { 0x50, 0x4B, 0x05, 0x06 },
                                              new byte[] { 0x50, 0x4B, 0x07, 0x08 },
                                              new byte[] { 0x57, 0x69, 0x6E, 0x5A, 0x69, 0x70 }
                                                }
                                            },
                    { ".PNG", new List<byte[]> { new byte[] { 0x89, 0x50, 0x4E, 0x47, 0x0D, 0x0A, 0x1A, 0x0A } } },
                    { ".JPG", new List<byte[]>
                                    {
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE1 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE8 }
                                    }
                                    },
                    { ".JPEG", new List<byte[]>
                                        { 
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE2 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE3 }
                                        }
                                        },
                    { ".XLS", new List<byte[]>
                                            {
                                              new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 },
                                              new byte[] { 0x09, 0x08, 0x10, 0x00, 0x00, 0x06, 0x05, 0x00 },
                                              new byte[] { 0xFD, 0xFF, 0xFF, 0xFF }
                                            }
                                            },
                    { ".XLSX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".GIF", new List<byte[]> { new byte[] { 0x47, 0x49, 0x46, 0x38 } } }
                };

        public static bool IsValidFileExtension(string fileName, byte[] fileData, byte[] allowedChars)
        {
            if (string.IsNullOrEmpty(fileName) || fileData == null || fileData.Length == 0)
            {
                return false;
            }

            bool flag = false;
            string ext = Path.GetExtension(fileName);
            if (string.IsNullOrEmpty(ext))
            {
                return false;
            }

            ext = ext.ToUpperInvariant();

            if (ext.Equals(".TXT") || ext.Equals(".CSV") || ext.Equals(".PRN"))
            {
                foreach (byte b in fileData)
                {
                    if (b > 0x7F)
                    {
                        if (allowedChars != null)
                        {
                            if (!allowedChars.Contains(b))
                            {
                                return false;
                            }
                        }
                        else
                        {
                            return false;
                        }
                    }
                }

                return true;
            }

            if (!fileSignature.ContainsKey(ext))
            {
                return true;
            }

            List<byte[]> sig = fileSignature[ext];
            foreach (byte[] b in sig)
            {
                var curFileSig = new byte[b.Length];
                Array.Copy(fileData, curFileSig, b.Length);
                if (curFileSig.SequenceEqual(b))
                {
                    flag = true;
                    break;
                }
            }

            return flag;
        }
```

## <a id="typesafe"></a>Tür kullanımı uyumlu parametreleri veri erişimi için Web uygulamasında kullanıldığından emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>Merhaba parametreler koleksiyonu kullanırsanız, bir hazır değer yerine yürütülebilir kod olarak olarak SQL davranır hello giriş olabilir. Parametreler koleksiyonu Hello giriş verisi kullanılan tooenforce türünü ve uzunluğu kısıtlamalar olabilir. Değerleri hello aralığın dışında bir özel durum tetikler. Tür kullanımı uyumlu SQL parametre kullanılmazsa, saldırganlar filtrelenmemiş hello girişinde katıştırılmış mümkün tooexecute ekleme saldırıları olabilir.</p><p>SQL oluşturma filtrelenmemiş girişle oluşabilecek tooavoid olası SQL ekleme saldırıları sorguladığında türü güvenli parametrelerini kullanın. Saklı yordamlar ve dinamik SQL deyimleri ile tür güvenli parametreleri kullanabilirsiniz. Parametreleri yürütülebilir kod değil de, hello veritabanı tarafından değişmez değerler olarak kabul edilir. Parametreler, türü ve uzunluğu için de denetlenir.</p>|

### <a name="example"></a>Örnek 
Merhaba aşağıdaki kod nasıl toouse yazın hello SqlParameterCollection güvenli parametrelerle bir saklı yordamı çağrılırken gösterir. 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
Önceki kod örneğinde hello hello giriş değeri 11 karakterden uzun olamaz. Merhaba veri toohello türü veya hello parametresi tarafından tanımlanan uzunluk uyuşmadığı hello SqlParameter sınıfı bir özel durum oluşturur. 

## <a id="binding-mvc"></a>Ayrı model bağlama sınıflarını kullanın veya bağlama filtresi tooprevent MVC yığın atama güvenlik açığı listeler

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | MVC5, MVC6 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Meta veri öznitelikleri](http://msdn.microsoft.com/library/system.componentmodel.dataannotations.metadatatypeattribute), [ortak anahtarı Güvenlik Açığı ve azaltma](https://github.com/blog/1068-public-key-security-vulnerability-and-mitigation), [Kılavuzu tooMass ASP.NET MVC atamasını](http://odetocode.com/Blogs/scott/archive/2012/03/11/complete-guide-to-mass-assignment-in-asp-net-mvc.aspx), [MVC kullanarak EF ile çalışmaya başlama](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application#overpost) |
| **Adımları** | <ul><li>**Güvenlik açıkları aşırı gönderim için ne zaman görmeliyim? -** Güvenlik açıkları aşırı gönderim giriş kullanıcıdan modeli sınıfları bağlamak herhangi bir yeri oluşabilir. MVC gibi çerçeveleri düz eski CLR nesnelerini (POCOs) dahil olmak üzere özel .NET sınıfları kullanıcı verilerini temsil edebilir. MVC kullanıcı girişi ilgilenmek için kullanışlı bir temsilini sağlayarak bu modeli sınıfları hello isteği verilerle otomatik olarak doldurur. Bu sınıfların hello kullanıcı tarafından ayarlanmamalıdır özellikleri eklediğinizde, hello uygulama Merhaba uygulaması hiçbir zaman amaçlı veri kullanıcı denetimini izin savunmasız tooover nakil saldırıları olabilir. MVC model bağlama gibi POCO nesneleri toorepresent veritabanı verileri kullanarak veritabanı erişim teknolojileri Entity Framework gibi nesne/ilişkisel mappers gibi genellikle de destekler. Bu veri modeli sınıflarını hello sağlamak kullanıcı girişi ile ilgili MVC yaptığı gibi veritabanı verileriyle ilgili olarak aynı kolaylık sağlamak. MVC ve hello veritabanı POCO nesneleri gibi benzer modelleri desteklemediğinden aynı hem amacıyla sınıfları kolay tooreuse hello gibi görünüyor. Bu yöntem başarısız toopreserve sorunları ve istenmeyen özellikleri olduğu tek bir ortak alan ayrılmasıdır atlayarak nakil saldırılarını etkinleştirme toomodel bağlama açık.</li><li>**Neden ı my filtrelenmemiş veritabanı modeli sınıflarını parametreleri toomy MVC eylemler olarak kullanmamanız gerekir? -** Çünkü MVC model bağlama bağlamak herhangi bir şey bu sınıfta. Eyleminizi veritabanı sınıfı hello Şekil veri olduğunu söylüyor olduğundan veri görünümünüzde, kötü niyetli bir kullanıcının dahil bu verilerle bir HTTP isteği göndermek görünmez hello ve MVC gladly onu bağlayacaksınız olsa bile kullanıcı girdisi kabul etmelidir.</li><li>**Model bağlama için kullanılan hello şekli hakkında neden önemli? -** Kullanarak ASP.NET MVC model bağlama aşırı geniş kapsamlı modelleri ile bir uygulama tooover nakil saldırıları kullanıma sunar. Atlayarak nakil hedeflenen, bir hesap için bir öğe veya hello güvenlik ayrıcalıklarını hello fiyatı geçersiz kılma gibi hangi hello Geliştirici aşan saldırganlar toochange uygulama veri sağlayabilir. Uygulamalar, model bağlama aracılığıyla hangi güvenilmeyen giriş tooallow için eylem özgü modelleri (veya belirli izin verilen özellik filtresi listeleri) bağlama tooprovide açık bir sözleşmeyi kullanmalıdır.</li><li>**Kod yalnızca çoğaltma ayrı bağlama modelleri sorun mu yaşıyorsunuz? -** Hayır, sağlasa da, sorunları ayrılması yöneliktir. Eylem yöntemleri veritabanı modellerinde yeniden kullanırsanız, sınıf bir HTTP isteğindeki hello kullanıcı tarafından ayarlanmış herhangi bir özelliği (veya alt özellik) yorumlarını. Bu istemezsiniz olursa MVC toodo gereksinim duyduğunuz bir filtre listesi ya da ayrı sınıf şekli tooshow MVC hangi verilerin, bunun yerine Giriş kullanıcıdan gelebilir.</li><li>**Kullanıcı girişi için ayrı bağlama modelleri varsa, ı my veri ek açıklaması öznitelikleri tooduplicate var mı? -** Gerekmez. MetadataTypeAttribute hello veritabanı model sınıfı toolink toohello meta verilerini bir model bağlama sınıfını kullanabilirsiniz. Merhaba MetadataTypeAttribute tarafından başvurulan türü hello yalnızca not hello (daha az özellik ancak fazla sahip olabilir) türüne başvuran bir kısmı olması gerekir.</li><li>**Verileri geri ve İleri kullanıcı giriş modelleri ve veritabanı modelleri arasında taşıma yorucu olabilir. Yansıma kullanarak tüm özellikleri kopyalayabilir yalnızca miyim? -** Evet. Merhaba hello bağlama modellerinde görünen yalnızca kullanıcı girişi için güvenli toobe belirlediğiniz hello olanları özelliklerdir. Bu iki modelleri arasında ortak mevcut tüm özellikleri üzerinden yansıma toocopy kullanarak engelleyen güvenlik neden yoktur.</li><li>**Ne hakkında [bağlayın (dışarıda = "â €¦")]. Ayrı bağlama modelleri sahip olmak yerine kullanabilir miyim? -** Bu yaklaşım önerilmez. Kullanma [bağlayın (dışarıda = "â €¦")] herhangi bir yeni özellik, varsayılan olarak bağlanabilir anlamına gelir. Yeni bir özellik eklendiğinde, ek adım tooremember tookeep şeyler güvenli yerine varsayılan olarak güvenli olacak hello tasarım sahip. Merhaba Geliştirici bağlı olarak bir özellik eklenir her zaman bu liste denetimi risklidir.</li><li>**Olduğundan [bağlayın (içerme = "â €¦")] düzenleme işlemleri için yararlı? -** No [Bağlayın (içerme = "â €¦")] yalnızca (yeni veriler toplayarak) stili ekleme işlemleri için uygundur. (Mevcut verileri düzeltilmesi) stilini güncelleştir işlemleri için ayrı bağlama modelleri olması veya izin verilen özellikleri tooUpdateModel veya TryUpdateModel açık bir listesi geçirme gibi başka bir yaklaşım kullanın. Ekleme bir [bağlayın (içerme = "â €¦")] düzenleme işlemi öznitelikte MVC bir nesne örneğini oluşturmak ve diğerlerini varsayılan değerlerinde bırakın hello özellikleri, listelenen yalnızca ayarlamak anlamına gelir. Merhaba veri kalıcı olduğunda tamamen herhangi belirtilmemişse özellikleri tootheir Varsayılanları hello değerlerini sıfırlama hello varolan varlık yerini alır. IsAdmin atlanırsa, örneğin, bir [bağlayın (içerme = "â €¦")] adı bu eylem düzenlenmiş herhangi bir kullanıcı bir Düzenle işlem öznitelikte sıfırlama tooIsAdmin olacaktır = false (herhangi bir düzenlenen kullanıcı yönetici durumu kaybeder). Tooprevent toocertain özelliklerini günceller istiyorsanız, diğer yaklaşımlar yukarıda hello birini kullanın. MVC araç bazı sürümleri denetleyicisi sınıflarıyla oluşturmak Not [bağlamak (içerme = "â €¦")] düzenleme eylemleri ve bu listeden bir özellik kaldırma atlayarak nakil saldırılarını önlemeye kapsıyor. Ancak, yukarıda açıklandığı gibi bu yaklaşımı beklendiği gibi çalışmaz ve bunun yerine herhangi bir veri atlanmış hello özelliklerine tootheir varsayılan değerlerine sıfırlar.</li><li>**Oluşturma işlemleri için kullanarak uyarılar vardır [bağlayın (içerme = "â €¦")] ayrı bağlama modelleri yerine? -** Evet. Önce tüm atlayarak nakil güvenlik açıkları Azaltıcı için iki ayrı yaklaşım koruma gerektiren düzenleme senaryolar için bu yaklaşım çalışmaz. İkinci ve ayrı bağlama modelleri kalıcılığı için kullanılan kullanıcı giriş ve hello şekil için kullanılan hello şekli arasında sorunları ayrılması zorunlu bir şey [bağlamak (içerme = "â €¦")] yapın. Üçüncü unutmayın [bağlayın (içerme = "â €¦")] yalnızca üst düzey özellikleri; işleyebilir yalnızca alt özellikleri (örneğin, "Details.Name") bölümünü hello özniteliğinde izin veremez. Son olarak ve belki de en önemlisi, kullanarak [bağlayın (içerme = "â €¦")] herhangi bir zaman hello sınıf model bağlama için kullanılan hatırlanan gereken ek bir adım ekler. Yeni bir eylem yöntemi toohello veri sınıfı doğrudan bağlar ve tooinclude unutması durumunda bir [bağlamak (içerme = "â €¦")] özniteliği olabilir savunmasız tooover nakil saldırıları, bu nedenle hello [bağlamak (INCLUDE = "â €¦")] yaklaşımdır varsayılan biraz daha az güvenli. Kullanırsanız [bağlayın (içerme = "â €¦")], her zaman tooremember toospecify dikkatli olun, veri sınıfları eylem yöntemi parametrelerine görünen her zaman.</li><li>**Oluşturma işlemleri için koyma hakkında neler hello [bağlayın (içerme = "â €¦")] hello modeli sınıfının kendisi öznitelikte? Bu yaklaşım hello gerek tooremember koyma hello öznitelikte her eylem yöntemi önlenir? -** Bazı durumlarda bu yaklaşım çalışır. Kullanma [bağlamak (INCLUDE = "â €¦")] hello model türündeki kendisini (yerine bu sınıfı kullanarak eylem parametrelerini), hello gerek tooremember tooinclude hello önlemek [bağlamak (Ekle = "â €¦")] her eylem yöntemi özniteliği. Merhaba özniteliğini doğrudan hello sınıfı üzerinde etkili bir şekilde kullanarak model bağlama amacıyla bu sınıfın ayrı bir yüzey alanını oluşturur. Ancak, bu yaklaşım, model bağlama bir şeklin model sınıfı başına yalnızca sağlar. Bir eylem yönteminin tooallow model bağlama bir alanın (kullanıcı rollerini güncelleştiren Örneğin, yalnızca yönetici eylem) gerekir ve bu alan tooprevent model bağlama diğer eylemler ihtiyacınız varsa bu yaklaşımı çalışmaz. Her sınıf yalnızca bir model bağlama şeklin olabilir; farklı eylemler farklı model bağlama şekiller gerekiyorsa, bunlar ayrı ya da ayrı model bağlama sınıfları kullanarak şekiller veya ayrı toorepresent ihtiyaç duydukları [bağlayın (içerme = "â €¦")] hello eylem yöntemleri özniteliklerinde.</li><li>**Ne modelleri bağlama? Görünüm model olarak aynı anlama hello misiniz? -** İki ilgili kavramları şunlardır. bir eylem kullanılan tooa model sınıfı bağlama modelini başvuruyor hello parametre listesi (Merhaba şekil MVC model bağlama toohello eylem yönteminden geçirilen) bir terimdir. Merhaba terim görünüm modeli tooa modeli sınıfı bir eylem yöntemi tooa görünümünden geçirilen ifade eder. Bir görünüm özgü modeli kullanarak bir eylem yöntemi tooa görünümünden veri geçirme için ortak bir yaklaşımdır. Genellikle, bu şeklin model bağlama için uygundur ve her iki yerde de aynı modeli kullanılan kullanılan toorefer hello hello terim görünüm modeli olabilir. toobe kesin, bu yordam özellikle ne yığın atama amaçlar için önemli olan toohello eylem geçirilen hello şekli odaklanan modeller, bağlama hakkında alınmaktadır.</li></ul>| 

## <a id="rendering"></a>Güvenilmeyen web çıkış önceki toorendering kodlama

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel, Web Forms, MVC5, MVC6 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Nasıl ASP.NET tooprevent siteler arası komut dosyası](http://msdn.microsoft.com/library/ms998274.aspx), [siteler arası komut dosyası](http://cwe.mitre.org/data/definitions/79.html), [XSS (siteler arası komut dosyası) önleme kopya sayfası](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet) |
| **Adımları** | Siteler arası komut dosyası (XSS yaygın olarak kısaltılır) Çevrimiçi hizmetler veya tüm uygulama/hello web girişten tüketen bileşen için saldırı vektörü olur. XSS Güvenlik Açıkları bir saldırgan, bir güvenlik açığı web uygulaması aracılığıyla başka bir kullanıcının makinede tooexecute komut dosyası izin verebilir. Kötü amaçlı komut dosyalarını kullanılan toosteal tanımlama bilgileri ve aksi halde bir kurbanın makine JavaScript aracılığıyla değiştirmesine. Kullanıcı girişini doğrulama, doğru biçimlendirildiğinden olduktan ve bir web sayfasında işlenmeden önce kodlama XSS engelledi. Giriş doğrulama ve çıktı kodlama Web koruma kitaplığı kullanılarak yapılabilir. Yönetilen kod için (C\#, VB.net, vb.), kullanın veya daha fazla uygun kodlama yöntemleri hello burada hello kullanıcı girişini bildirilmiş hello bağlam bağlı olarak Web koruma (Anti-XSS) kitaplığı:| 

### <a name="example"></a>Örnek

```C#
* Encoder.HtmlEncode 
* Encoder.HtmlAttributeEncode 
* Encoder.JavaScriptEncode 
* Encoder.UrlEncode
* Encoder.VisualBasicScriptEncode 
* Encoder.XmlEncode 
* Encoder.XmlAttributeEncode 
* Encoder.CssEncode 
* Encoder.LdapEncode 
```

## <a id="typemodel"></a>Giriş doğrulaması ve tüm dize türünde Model özelliklerini filtrelemesine

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel, MVC5, MVC6 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Doğrulama ekleme](http://www.asp.net/mvc/overview/getting-started/introduction/adding-validation), [MVC uygulamasındaki Model verileri doğrulama](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx), [ilkeleri için ASP.NET MVC uygulamalarınızı yönlendirmede](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Adımları** | <p>Merhaba uygulaması kötü amaçlı kullanıcı girişleri karşı korunması gerektiğini hello uygulama tooensure kullanılmadan önce tüm hello giriş parametreleri doğrulanması gerekir. Sunucu tarafında bir beyaz liste doğrulama stratejisi ile normal ifade doğrulamaları kullanarak hello giriş değerleri doğrulayın. Kullanıcı girişleri unsanitized / toohello yöntemleri geçirilen parametre yerleştirme güvenlik açıkları kodu neden olabilir.</p><p>Web uygulamaları için giriş noktaları form alanları, QueryStrings, tanımlama bilgileri, HTTP üst bilgilerine ve web hizmeti parametreleri de dahil edebilirsiniz.</p><p>Merhaba aşağıdaki giriş doğrulama denetimlerini model bağlama sırasında gerçekleştirilmesi gerekir:</p><ul><li>Yanıtta normal ifade ek açıklama, izin verilen karakterler ve izin verilen maksimum uzunluğu kabul etmek için Hello model özellikleri açıklama</li><li>Merhaba denetleyici yöntemlerine ModelState geçerlilik gerçekleştirmeniz gerekir</li></ul>|

## <a id="richtext"></a>Tüm karakterleri, örneğin, Zengin Metin Düzenleyicisi'ni kabul eden form alanlarını temizleme işlemi uygulanmalıdır

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Güvenli olmayan giriş kodlamak](https://msdn.microsoft.com/library/ff647397.aspx#paght000003_step3), [HTML temizleyici](https://github.com/mganss/HtmlSanitizer) |
| **Adımları** | <p>Toouse istediğiniz tüm static işaretleme etiketlerini tanımlayın. Toosafe HTML öğeleri gibi biçimlendirme toorestrict yaygın bir uygulamadır `<b>` (kalın) ve `<i>` (italik).</p><p>Merhaba verileri, HTML olarak kodlanacak yazmadan önce onu. Kötü amaçlı komut dosyaları toobe neden olarak güvenli yürütülebilir kod olarak değil metin olarak işlenen bu yapar.</p><ol><li>ASP.NET istek hello ekleyerek doğrulama hello ValidateRequest devre dışı bırak "false" özniteliği toohello sayfa yönergesi @ =</li><li>Merhaba dize girişi hello HtmlEncode yöntemi ile kodlayın</li><li>StringBuilder ve onun Değiştir yöntemi tooselectively kaldırmak hello HTML öğelerde toopermit istediğiniz kodlama hello çağrı kullanın</li></ol><p>Merhaba sayfa içinde hello başvuruları devre dışı bırakır ASP.NET istek doğrulama ayarlayarak `ValidateRequest="false"`. Onu HTML olarak kodlar hello giriş ve seçmeli olarak hello verir `<b>` ve `<i>` alternatif olarak, bir .NET kitaplığı HTML Temizleme için de kullanılabilir.</p><p>HtmlSanitizer HTML parçalarının ve tooXSS saldırılara yol açabilecek yapıları belgelerden Temizleme için bir .NET kitaplıktır. AngleSharp tooparse kullanır, işlemek ve HTML ve CSS işlenemiyor. Bir NuGet paketi olarak HtmlSanitizer yüklenebilir ve ilgili HTML veya CSS temizleme yöntemleri, geçerli hello sunucu tarafında aracılığıyla hello kullanıcı girişi geçirilebilir. Lütfen unutmayın, güvenlik denetimi olarak temizleme yalnızca son seçeneği olarak düşünülmelidir.</p><p>Giriş doğrulama ve çıktı kodlama daha iyi güvenlik denetimleri olarak kabul edilir.</p> |

## <a id="inbuilt-encode"></a>Yerleşik kodlama olmayan DOM öğeleri toosinks atamayın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Varsayılan kodlama birçok javascript işlevleri desteklemez. Bu tür işlevler aracılığıyla güvenilmeyen giriş tooDOM öğelerini atarken site komut dosyası (XSS) yürütmeleri sonuçlanabilir.| 

### <a name="example"></a>Örnek
Güvensiz örnekleri şunlardır: 

```
document.getElementByID("div1").innerHtml = value;
$("#userName").html(res.Name);
return $('<div/>').html(value)
$('body').append(resHTML);   
```
Kullanmayan `innerHtml`; bunun yerine kullanın `innerText`. Benzer şekilde, yerine, `$("#elm").html()`, kullanın`$("#elm").text()` 

## <a id="redirect-safe"></a>Tüm doğrulama yeniden yönlendirmeleri hello uygulamadaki kapalı veya güvenli bir şekilde tamamlandı

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Merhaba OAuth 2.0 yetkilendirme Framework - açık yeniden yönlendiricileri](http://tools.ietf.org/html/rfc6749#section-10.15) |
| **Adımları** | <p>Yeniden yönlendirme tooa kullanıcı tarafından sağlanan konumu gerektiren uygulama tasarımı hello olası yeniden yönlendirme hedefleri tooa önceden tanımlanmış "safe" listesi siteler veya etki alanları sınırlamak gerekir. Merhaba uygulamadaki tüm yeniden yönlendirmeleri kapalı güvenli olması gerekir.</p><p>toodo bu:</p><ul><li>Tüm yeniden yönlendirmeleri tanımlayın</li><li>Her yeniden yönlendirme için uygun bir hafifletme. Uygun Azaltıcı Etkenler yeniden yönlendirme beyaz liste veya kullanıcı onayı içerir. Bir web sitesi veya bir açık yeniden yönlendirme güvenlik açığı hizmetiyle Facebook/OAuth/Openıd kimlik sağlayıcıları kullanıyorsa, bir saldırganın bir kullanıcının oturum açma belirteci çalabilir ve o kullanıcının kimliğine bürün. Bu devralınan bir risk RFC 6749 "hello OAuth 2.0 yetkilendirme Framework" belgelenen OAuth kullanıldığında, 10.15 "açmak yönlendiren" bölümünde benzer şekilde, zıpkınla kimlik avı saldırıları tarafından açık yeniden yönlendirmeleri kullanarak kullanıcıların kimlik bilgilerini tehlikeye girebilir</li></ul>|

## <a id="string-method"></a>Uygulama giriş doğrulaması denetleyicisi yöntemler tarafından kabul edilen tüm dize türü parametreleri

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel, MVC5, MVC6 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Model verileri MVC uygulamasındaki doğrulama](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx), [ilkeleri için ASP.NET MVC uygulamalarınızı yönlendirmede](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Adımları** | Yalnızca basit veri türü ve değil modelleri bağımsız değişken olarak kabul yöntemleri için normal ifade kullanarak giriş doğrulaması yapılmalıdır. Burada Regex.IsMatch geçerli regex desenle kullanılmalıdır. Hello giriş eşleşmezse, belirtilen normal ifade Merhaba, denetim daha fazla devam etmemelisiniz ve doğrulama hatası ile ilgili yeterli bir uyarı görüntülenmesi gerekir.| 

## <a id="dos-expression"></a>Normal ifade tooprevent DoS toobad normal ifadeler nedeniyle işleme için üst sınır zaman aşımını ayarlama

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel, Web Forms, MVC5, MVC6  |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [DefaultRegexMatchTimeout özelliği](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.defaultregexmatchtimeout.aspx) |
| **Adımları** | tooensure hizmet reddi saldırılarına karşı çok sayıda geri dönüş neden, normal ifadeler, hatalı oluşturulmuş hello genel varsayılan zaman aşımı ayarlayın. Merhaba işleme süresi üst sınırı hello tanımlı daha uzun sürüyorsa, zaman aşımı özel durumu throw. Hiçbir şey yapılandırılmışsa, hello zaman aşımını sonsuz olacaktır.| 

### <a name="example"></a>Örnek
Merhaba işleme 5 saniyeden daha uzun sürerse gibi hello aşağıdaki yapılandırma bir RegexMatchTimeoutException özel durum oluşturacak: 

```C#
<httpRuntime targetFramework="4.5" defaultRegexMatchTimeout="00:00:05" />
```

## <a id="html-razor"></a>Razor görünümleri Html.Raw kullanmaktan kaçının

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | MVC5, MVC6 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| Adım | ASP.Net Web sayfaları (Razor) gerçekleştirmek otomatik HTML kodlaması. Katıştırılmış kod nuggets (@ blokları) tarafından yazdırılan tüm otomatik olarak HTML ile kodlanmış dizelerdir. Ancak, ne zaman `HtmlHelper.Raw` yöntemi çağrıldığında, HTML kodlu olmayan biçimlendirme döndürür. Varsa `Html.Raw()` yardımcı yöntemi kullanıldığında, Razor sağladığı hello otomatik kodlama koruma atlar.|

### <a name="example"></a>Örnek
Güvenli olmayan bir örnek aşağıda verilmiştir: 

```C#
<div class="form-group">
            @Html.Raw(Model.AccountConfirmText)
        </div>
        <div class="form-group">
            @Html.Raw(Model.PaymentConfirmText)
        </div>
</div>
```
Kullanmayın `Html.Raw()` toodisplay biçimlendirme gerekmedikçe. Bu yöntem örtük olarak kodlama çıkış gerçekleştirmez. Örneğin diğer ASP.NET Yardımcıları kullanın,`@Html.DisplayFor()` 

## <a id="stored-proc"></a>Dinamik sorgular saklı yordamlarda kullanmayın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>Bir SQL ekleme saldırısı güvenlik açıklarını komutlarda giriş doğrulaması toorun rasgele hello veritabanındaki kullanır. Uygulamanızı giriş tooconstruct dinamik kullandığında veritabanı SQL deyimleri tooaccess hello oluşabilir. Kodunuzu ham kullanıcı girişi içeren dizeleri geçirilen saklı yordamlar kullanılıyorsa da oluşabilir. Merhaba saldırgan Hello SQL ekleme saldırısında kullanarak, hello veritabanında rasgele komutları çalıştırabilirsiniz. Tüm SQL deyimleri (Merhaba SQL deyimlerini saklı yordamlarda dahil) parametreli gerekir. Parametreli SQL deyimlerini sorunsuz (tek tırnak gibi) özel bir anlamı tooSQL kesin türü belirtilmiş olduğundan olan karakterleri kabul eder. |

### <a name="example"></a>Örnek
Güvenli olmayan dinamik saklı yordam örneği aşağıdadır: 

```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteria]
(
  @productName nvarchar(200) = NULL,
  @startPrice float = NULL,
  @endPrice float = NULL
)
AS
 BEGIN
  DECLARE @sql nvarchar(max)
  SELECT @sql = ' SELECT ProductID, ProductName, Description, UnitPrice, ImagePath' +
       ' FROM dbo.Products WHERE 1 = 1 '
       PRINT @sql
  IF @productName IS NOT NULL
     SELECT @sql = @sql + ' AND ProductName LIKE ''%' + @productName + '%'''
  IF @startPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice > ''' + CONVERT(VARCHAR(10),@startPrice) + ''''
  IF @endPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice < ''' + CONVERT(VARCHAR(10),@endPrice) + ''''

  PRINT @sql
  EXEC(@sql)
 END
```

### <a name="example"></a>Örnek
Aynı saklı yordam güvenli bir şekilde uygulanan hello aşağıdadır: 
```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteriaSecure]
(
             @productName nvarchar(200) = NULL,
             @startPrice float = NULL,
             @endPrice float = NULL
)
AS
       BEGIN
             SELECT ProductID, ProductName, Description, UnitPrice, ImagePath
             FROM dbo.Products where
             (@productName IS NULL or ProductName like '%'+ @productName +'%')
             AND
             (@startPrice IS NULL or UnitPrice > @startPrice)
             AND
             (@endPrice IS NULL or UnitPrice < @endPrice)         
       END
```

## <a id="validation-api"></a>Model doğrulama Web API yöntemlerini yapıldığından emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web API | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | MVC5, MVC6 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [ASP.NET Web API'de model doğrulama](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) |
| **Adımları** | Bir istemci veri tooa web API gönderdiğinde, herhangi bir işlem yapmadan önce zorunlu toovalidate hello veri değil. ASP.NET Web modelleri girdi olarak kabul API'leri için veri ek açıklamaları hello modelinin hello özelliklerindeki modelleri tooset doğrulama kuralları kullanın.|

### <a name="example"></a>Örnek
koddan hello gösteren aynı hello: 

```C#
using System.ComponentModel.DataAnnotations;

namespace MyApi.Models
{
    public class Product
    {
        public int Id { get; set; }
        [Required]
        [RegularExpression(@"^[a-zA-Z0-9]*$", ErrorMessage="Only alphanumeric characters are allowed.")]
        public string Name { get; set; }
        public decimal Price { get; set; }
        [Range(0, 999)]
        public double Weight { get; set; }
    }
}
```

### <a name="example"></a>Örnek
Merhaba eylem yönteminde hello API denetleyicilerinin hello modeli geçerliliğini açıkça aşağıda gösterildiği gibi kullanıma toobe sahiptir: 

```C#
namespace MyApi.Controllers
{
    public class ProductsController : ApiController
    {
        public HttpResponseMessage Post(Product product)
        {
            if (ModelState.IsValid)
            {
                // Do something with hello product (not shown).

                return new HttpResponseMessage(HttpStatusCode.OK);
            }
            else
            {
                return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
            }
        }
    }
}
```

## <a id="string-api"></a>Web API yöntemleri tarafından kabul edilen tüm dize tür parametrelerindeki giriş doğrulaması uygulama

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web API | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel, MVC 5, MVC 6 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Model verileri MVC uygulamasındaki doğrulama](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx), [ilkeleri için ASP.NET MVC uygulamalarınızı yönlendirmede](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Adımları** | Yalnızca basit veri türü ve değil modelleri bağımsız değişken olarak kabul yöntemleri için normal ifade kullanarak giriş doğrulaması yapılmalıdır. Burada Regex.IsMatch geçerli regex desenle kullanılmalıdır. Hello giriş eşleşmezse, belirtilen normal ifade Merhaba, denetim daha fazla devam etmemelisiniz ve doğrulama hatası ile ilgili yeterli bir uyarı görüntülenmesi gerekir.|

## <a id="typesafe-api"></a>Tür kullanımı uyumlu parametreleri Web API'si veri erişimi için kullanıldığından emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web API | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>Merhaba parametreler koleksiyonu kullanırsanız, bir hazır değer yerine yürütülebilir kod olarak olarak SQL davranır hello giriş olabilir. Parametreler koleksiyonu Hello giriş verisi kullanılan tooenforce türünü ve uzunluğu kısıtlamalar olabilir. Değerleri hello aralığın dışında bir özel durum tetikler. Tür kullanımı uyumlu SQL parametre kullanılmazsa, saldırganlar filtrelenmemiş hello girişinde katıştırılmış mümkün tooexecute ekleme saldırıları olabilir.</p><p>SQL oluşturma filtrelenmemiş girişle oluşabilecek tooavoid olası SQL ekleme saldırıları sorguladığında türü güvenli parametrelerini kullanın. Saklı yordamlar ve dinamik SQL deyimleri ile tür güvenli parametreleri kullanabilirsiniz. Parametreleri yürütülebilir kod değil de, hello veritabanı tarafından değişmez değerler olarak kabul edilir. Parametreler, türü ve uzunluğu için de denetlenir.</p>|

### <a name="example"></a>Örnek
Merhaba aşağıdaki kod nasıl toouse yazın hello SqlParameterCollection güvenli parametrelerle bir saklı yordamı çağrılırken gösterir. 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
Önceki kod örneğinde hello hello giriş değeri 11 karakterden uzun olamaz. Merhaba veri toohello türü veya hello parametresi tarafından tanımlanan uzunluk uyuşmadığı hello SqlParameter sınıfı bir özel durum oluşturur. 

## <a id="sql-docdb"></a>Cosmos DB için parametreli SQL sorgularını kullan

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure belge DB | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Documentdb'de SQL parametrelemeyi Duyurusu](https://azure.microsoft.com/blog/announcing-sql-parameterization-in-documentdb/) |
| **Adımları** | DocumentDB yalnızca salt okunur sorguları destekler; ancak, SQL ekleme sorguları kullanıcı girişi ile birleştirerek oluşturulur, yine de mümkündür. Bunlar döndürmemelidir erişme hello içinde bir kullanıcı toogain erişim toodata mümkün olabilir kötü amaçlı SQL sorguları hazırlayın tarafından aynı koleksiyonu. Sorguları oluşturulan parametreli SQL sorguları kullanıcı girişini temel alarak kullanın. |

## <a id="schema-binding"></a>Şema bağlama aracılığıyla WCF girişi doğrulama

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | WCF | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel, NET Framework 3 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [MSDN](https://msdn.microsoft.com/library/ff647820.aspx) |
| **Adımları** | <p>Doğrulama eksikliği toodifferent türü ekleme saldırıları yol açar.</p><p>İleti doğrulama savunma hello koruma WCF uygulamanızın tek bir çizgi temsil eder. Bu yaklaşımda, kötü amaçlı bir istemci tarafından saldırılara karşı şemaları tooprotect WCF Hizmeti işlemlerini kullanarak iletileri doğrulayın. Merhaba istemci tooprotect hello istemci saldırılara karşı tarafından kötü amaçlı bir hizmeti tarafından alınan tüm iletileri doğrulayın. İleti doğrulama kılar olası toovalidate iletileri işlemleri ileti sözleşmeleri veya yapılamaz veri sözleşmeleri kullandığında parametre doğrulaması kullanarak. İleti doğrulama şemaları, böylece daha fazla esneklik sağlayan ve geliştirme zamanı azaltarak içinde toocreate Doğrulama mantığı sağlar. Şemalar veri temsili standartları oluşturma hello kuruluş içindeki farklı uygulamalar arasında yeniden kullanılabilir. Ayrıca, iş mantığı temsil eden sözleşmeleri içeren daha karmaşık veri türleri kullandığında ileti doğrulama, tooprotect işlemler sağlar.</p><p>tooperform ileti doğrulama, önce bu işlemler tarafından tüketilen hizmeti ve hello veri türlerinizi hello işlemleri temsil eden bir şema oluşturun. Özel istemci ileti denetçisi ve özel dağıtıcısı denetçisi toovalidate hello ileti hello hizmet denetleyicisinden gönderilen/alınan uygulayan bir .NET sınıf oluşturursunuz. Ardından, hem hello istemci hem de hello hizmeti bir özel uç noktası davranışı tooenable ileti doğrulama uygulamadan. Son olarak, bir özel yapılandırma öğesi, tooexpose hello özel uç noktası davranışı hello hizmet veya hello istemci hello yapılandırma dosyasında genişletilmiş sağlayan hello sınıfı üzerinde uygulamak"</p>|

## <a id="parameters"></a>Parametre denetçiler aracılığıyla WCF girişi doğrulama

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | WCF | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel, NET Framework 3 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [MSDN](https://msdn.microsoft.com/library/ff647875.aspx) |
| **Adımları** | <p>Giriş ve veri doğrulama savunma hello koruma WCF uygulamanızın önemli bir satır temsil eder. WCF Hizmeti işlemlerini tooprotect hello hizmetinde saldırılara karşı kötü amaçlı bir istemci tarafından kullanıma sunulan tüm parametreleri doğrulamalıdır. Buna karşılık, ayrıca hello istemci tooprotect hello istemci saldırılara karşı tarafından kötü amaçlı bir hizmeti tarafından alınan tüm dönüş değerleri doğrulamalıdır</p><p>WCF özel uzantılar oluşturarak toocustomize hello WCF çalışma zamanı davranışı izin farklı genişletilebilirlik noktaları sağlar. Denetçiler ve parametre denetçiler iki genişletilebilirlik mekanizması iletisi toogain büyük verileri üzerinde denetime sahip bir istemci ve hizmet arasında geçirme hello kullanılır. Giriş doğrulaması için parametre denetçiler kullanın ve yalnızca bir hizmet ve bu moddan akan tooinspect hello tüm ileti gerektiğinde ileti denetçileri kullanmanız gerekir.</p><p>tooperform giriş doğrulaması, bir .NET sınıfını oluşturmak ve hizmetinizi işlemlerini sipariş toovalidate parametrelerinde özel parametre denetçisi uygulamak. Özel uç noktası davranışı tooenable doğrulama hem hello istemci hem de hello hizmet ardından gerçekleştireceksiniz. Son olarak, tooexpose hello özel uç noktası davranışı hello hizmet veya hello istemci hello yapılandırma dosyasında genişletilmiş sağlayan hello sınıfı üzerinde özel yapılandırma öğesi gerçekleştireceksiniz</p>|
