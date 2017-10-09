---
title: "aaaSensitive verileri - Microsoft tehdit modelleme aracı - Azure | Microsoft Docs"
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
ms.openlocfilehash: 8a18f43af439241ba193ccf668971ddc4655355f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-sensitive-data--mitigations"></a>Güvenlik çerçeve: Hassas verileri | Azaltıcı Etkenler 
| Ürün/hizmet | Makale |
| --------------- | ------- |
| **Makine güven sınırı** | <ul><li>[Hassas bilgiler içeriyorsa, ikili dosyaları gizlenmiş emin olun](#binaries-info)</li><li>[Şifrelenmiş dosya sistemi (EFS) kullanarak kullanılan tooprotect gizli kullanıcıya özgü verileri önerilir](#efs-user)</li><li>[Hello dosya sisteminde hello uygulama tarafından depolanan hassas verilerin şifrelendiğinden emin olun](#filesystem)</li></ul> | 
| **Web uygulaması** | <ul><li>[Hassas içerikleri hello tarayıcıda önbelleğe alınmamış emin olun](#cache-browser)</li><li>[Hassas verileri içeren Web uygulamanızın yapılandırma dosyalarını bölümlerini şifrele](#encrypt-data)</li><li>[Açıkça hello otomatik tamamlama HTML öznitelik hassas formlar ve girişleri devre dışı bırak](#autocomplete-input)</li><li>[Hassas verileri Hello kullanıcının ekranda görüntülenen maskelenir emin olun](#data-mask)</li></ul> | 
| **Veritabanı** | <ul><li>[Dinamik veri ayrıcalıklı olmayan toolimit gizli verilerin açığa maskeleme kullanıcıları uygulama](#dynamic-users)</li><li>[Parolaları karma güvenlik biçiminde depolandığından emin olun](#salted-hash)</li><li>[Veritabanı sütunlarını postalardaki hassas verilerin şifrelendiğinden emin olun](#db-encrypted)</li><li>[Bu veritabanı düzeyi şifreleme (TDE) etkin olduğundan emin olun](#tde-enabled)</li><li>[Veritabanı Yedeklemeleri şifrelendiğinden emin olun](#backup)</li></ul> | 
| **Web API** | <ul><li>[API tarayıcının depoda depolanmaz bu hassas verileri ilgili tooWeb emin olun](#api-browser)</li></ul> | 
| Azure belge DB | <ul><li>[Documentdb'de depolanan hassas verileri şifrele](#encrypt-docdb)</li></ul> | 
| **Azure Iaas VM güven sınırı** | <ul><li>[Sanal makineler tarafından kullanılan Azure Disk şifrelemesi tooencrypt diskleri kullanmak](#disk-vm)</li></ul> | 
| **Service Fabric güven sınırı** | <ul><li>[Service Fabric uygulamaları parolaları şifrelemek](#fabric-apps)</li></ul> | 
| **Dynamics CRM** | <ul><li>[Güvenlik modelleme gerçekleştirebilir ve iş birimleri/takımlar kullanmak gerektiğinde](#modeling-teams)</li><li>[Kritik varlıklar üzerinde erişim tooshare özelliği simge durumuna küçült](#entities)</li><li>[Merhaba Dynamics CRM paylaşım özelliğini ve iyi güvenlik uygulamaları ile ilişkili hello riskleri tren kullanıcılar](#good-practices)</li><li>[Özel Durum Yönetimi'nde yapılandırma ayrıntıları gösteren proscribing geliştirme standartları Kuralı Ekle](#exception-mgmt)</li></ul> | 
| **Azure Depolama** | <ul><li>[Rest (Önizleme) verileri için Azure Storage hizmeti şifreleme (SSE) kullanın](#sse-preview)</li><li>[İstemci tarafı şifreleme toostore hassas verileri Azure depolama alanında kullanın](#client-storage)</li></ul> | 
| **Mobil istemci** | <ul><li>[Duyarlı veya toophones yerel depolama yazılan PII veri şifreleme](#pii-phones)</li><li>[Tooend kullanıcılara dağıtmadan önce oluşturulan ikili dosyaları belirsizleştirirseniz](#binaries-end)</li></ul> | 
| **WCF** | <ul><li>[Set clientCredentialType tooCertificate ya da Windows](#cert)</li><li>[WCF güvenlik modu etkin değil](#security)</li></ul> | 

## <a id="binaries-info"></a>Hassas bilgiler içeriyorsa, ikili dosyaları gizlenmiş emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Makine güven sınırı | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Hassas bilgiler ters gereken hassas iş mantığı ticari sırlar içeriyorsa, ikili dosyaları gizlenmiş emin olun. Toostop derlemelerinin mühendislik ters budur. Araçlar `CryptoObfuscator` bu amaç için kullanılabilir. |

## <a id="efs-user"></a>Şifrelenmiş dosya sistemi (EFS) kullanarak kullanılan tooprotect gizli kullanıcıya özgü verileri önerilir

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Makine güven sınırı | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Şifrelenmiş dosya sistemi (EFS) kullanarak kullanılan tooprotect gizli kullanıcıya özgü fiziksel erişimi toohello bilgisayarla rakiplerin verilerdir göz önünde bulundurun. |

## <a id="filesystem"></a>Hello dosya sisteminde hello uygulama tarafından depolanan hassas verilerin şifrelendiğinden emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Makine güven sınırı | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Hello dosya sisteminde hello uygulama tarafından depolanan hassas verilerin şifrelendiğinden emin olun (örneğin, DPAPI kullanarak), EFS zorlanamaz varsa |

## <a id="cache-browser"></a>Hassas içerikleri hello tarayıcıda önbelleğe alınmamış emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel, Web Forms, MVC5, MVC6 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Tarayıcılar önbelleğe alma ve geçmiş amacıyla bilgi depolayabilir. Bu önbelleğe alınan dosyaları hello geçici Internet dosyaları klasörünün hello durumda Internet Explorer gibi bir klasörde depolanır. Bu sayfaları yeniden adlandırılır, hello tarayıcı bunları kendi önbellekten görüntüler. Hassas bilgilerin olduğu (örneğin, kendi adres, kredi kartı bilgileri, sosyal güvenlik numarası veya kullanıcı adı) görüntülenen toohello kullanıcı sonra bu bilgiler, tarayıcının önbelleğinde depolanan ve bu nedenle alınabilir hello tarayıcının önbellek inceleniyor aracılığıyla olabilir veya yalnızca hello tarayıcının "Geri" düğmesine basarak. Ön bellek denetimi yanıt üstbilgi değeri çok "no-store" tüm sayfalar için ayarlayın. |

### <a name="example"></a>Örnek
```XML
<configuration>
  <system.webServer>
   <httpProtocol>
    <customHeaders>
        <add name="Cache-Control" value="no-cache" />
        <add name="Pragma" value="no-cache" />
        <add name="Expires" value="-1" />
    </customHeaders>
  </httpProtocol>
 </system.webServer>
</configuration>
```

### <a name="example"></a>Örnek
Bu filtre uygulanabilir. Aşağıdaki örnek kullanılabilir: 
```C#
public override void OnActionExecuting(ActionExecutingContext filterContext)
        {
            if (filterContext == null || (filterContext.HttpContext != null && filterContext.HttpContext.Response != null && filterContext.HttpContext.Response.IsRequestBeingRedirected))
            {
                //// Since this is MVC pipeline, this should never be null.
                return;
            }

            var attributes = filterContext.ActionDescriptor.GetCustomAttributes(typeof(System.Web.Mvc.OutputCacheAttribute), false);
            if (attributes == null || **Attributes**.Count() == 0)
            {
                filterContext.HttpContext.Response.Cache.SetNoStore();
                filterContext.HttpContext.Response.Cache.SetCacheability(HttpCacheability.NoCache);
                filterContext.HttpContext.Response.Cache.SetExpires(DateTime.UtcNow.AddHours(-1));
                if (!filterContext.IsChildAction)
                {
                    filterContext.HttpContext.Response.AppendHeader("Pragma", "no-cache");
                }
            }

            base.OnActionExecuting(filterContext);
        }
``` 

## <a id="encrypt-data"></a>Hassas verileri içeren Web uygulamanızın yapılandırma dosyalarını bölümlerini şifrele

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Nasıl yapılır: ASP.NET 2.0 kullanarak DPAPI yapılandırma bölümlerinin şifrelemek](https://msdn.microsoft.com/library/ff647398.aspx), [korumalı bir yapılandırma sağlayıcısı belirtme](https://msdn.microsoft.com/library/68ze1hb2.aspx), [kullanarak Azure anahtar kasası tooprotect uygulama parolaları](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/) |
| **Adımları** | Yapılandırma dosyaları gibi hello Web.config appsettings.json durumda sık kullanılan kullanıcı adları, parolalar, veritabanı bağlantı dizelerini ve şifreleme anahtarları dahil olmak üzere toohold hassas bilgileri. Bu bilgileri korumak, uygulamanızın savunmasız tooattackers veya kötü niyetli kullanıcıların hesap kullanıcı adları ve parolalar, veritabanı adları ve sunucu adları gibi hassas bilgileri alma olur. (Azure/şirket içi) Hello dağıtım türüne göre hello hassas DPAPI veya Azure anahtar kasası gibi hizmetleri kullanarak yapılandırma dosyalarını bölümlerini şifreler. |

## <a id="autocomplete-input"></a>Açıkça hello otomatik tamamlama HTML öznitelik hassas formlar ve girişleri devre dışı bırak

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [MSDN: otomatik tamamlama özniteliği](http://msdn.microsoft.com/library/ms533486(VS.85).aspx), [HTML AutoComplete seçeneğini kullanarak](http://msdn.microsoft.com/library/ms533032.aspx), [HTML temizleme Güvenlik Açığı](http://technet.microsoft.com/security/bulletin/MS10-071), [otomatik tamamlama., yeniden?](http://blog.mindedsecurity.com/2011/10/autocompleteagain.html) |
| **Adımları** | Merhaba otomatik tamamlama özniteliği bir form otomatik tamamlama açmak veya kapatmak olup olmayacağını belirtir. Otomatik Tamamlama açık olduğunda, hello tarayıcı otomatik olarak tam değerleri değerlerine göre önce o hello kullanıcının girdiği. Örneğin, yeni bir ad ve parola bir formda girilir ve hello form gönderildiğinde, hello tarayıcı hello parola kaydedilmiş sorar. Bundan sonra hello form görüntülendiğinde hello adı ve parola otomatik olarak doldurulur veya hello adı girildiğinde tamamlandı. Yerel erişimi olan bir saldırgan hello düz metin parolası hello tarayıcı önbelleğinden elde edilemedi. Otomatik Tamamlama varsayılan olarak etkindir ve onu açıkça devre dışı bırakılması gerekir. |

### <a name="example"></a>Örnek
```C#
<form action="Login.aspx" method="post " autocomplete="off" >
      Social Security Number: <input type="text" name="ssn" />
      <input type="submit" value="Submit" />    
</form>
```

## <a id="data-mask"></a>Hassas verileri Hello kullanıcının ekranda görüntülenen maskelenir emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Parolalar, kredi kartı numaraları SSN vb. gibi hassas verileri Merhaba ekranında görüntülendiğinde maskelenmiş. Merhaba verilere (örn., Kama gezinme parolalar, kullanıcıların SSN numaralarını görüntüleme destek personeli) yetkisiz tooprevent personelin budur. Bu veri öğeleri düz metin olarak görünür değildir ve uygun şekilde maskelenmiş emin olun. Bu (örneğin,. giriş olarak kabul ederken yapılan verdiğiniz toobe sahiptir Giriş türü = "parola") geri Merhaba ekranında görüntüleme yanı sıra (örn., görüntü yalnızca hello hello kredi kartı numarasının son 4 basamağı). |

## <a id="dynamic-users"></a>Dinamik veri ayrıcalıklı olmayan toolimit gizli verilerin açığa maskeleme kullanıcıları uygulama

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | SQL Azure, OnPrem |
| **Öznitelikleri**              | SQL sürüm - V12, SQL sürümü - MsSQL2016 |
| **Başvuruları**              | [Dinamik veri maskeleme](https://msdn.microsoft.com/library/mt130841) |
| **Adımları** | dinamik veri maskeleme Hello amacı da görüntüleme erişimi toohello verileri olmaması gereken kullanıcılar engelleyen gizli verilerin toolimit açığa budur. Dinamik veri maskeleme doğrudan toohello veritabanına bağlanma ve parça hello gizli verilerin açığa kapsamlı sorguları çalıştırma tooprevent veritabanı kullanıcıları hedefleyin değil. Dinamik veri maskeleme olan Tamamlayıcı tooother SQL Server güvenlik özellikleri (Denetim, şifreleme, satır düzeyi güvenlik...) ve toouse önerilir bunları birlikte bu özellik ayrıca sipariş toobetter hello gizli verilerin korunmasını hello içinde Veritabanı. Bu özellik yalnızca SQL Server 2016 ile başlayan ve Azure SQL veritabanı tarafından desteklenip desteklenmediğini unutmayın. |

## <a id="salted-hash"></a>Parolaları karma güvenlik biçiminde depolandığından emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Parola Hashing .NET Crypto API'ları kullanma](http://docs.asp.net/en/latest/security/data-protection/consumer-apis/password-hashing.html) |
| **Adımları** | Parolalar özel kullanıcı deposu veritabanlarında depolanması. Parola karmaları salt değerlerle yerine depolanması gerekir. Merhaba salt hello kullanıcı için her zaman benzersizdir ve 150.000 en düşük iş faktörü yineleme sayısı ile Merhaba parolası depolamayı deneme yanılma yapma tooeliminate hello olasılığını döngü önce b-crypt, s-crypt veya PBKDF2 geçerli emin olun.| 

## <a id="db-encrypted"></a>Veritabanı sütunlarını postalardaki hassas verilerin şifrelendiğinden emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | SQL sürümü - tüm |
| **Başvuruları**              | [SQL Server'da hassas verileri şifrelemek](https://technet.microsoft.com/library/ff848751(v=sql.105).aspx), [nasıl yapılır: SQL Server bir sütun, verileri şifrelemek](https://msdn.microsoft.com/library/ms179331), [sertifika tarafından şifrele](https://msdn.microsoft.com/library/ms188061) |
| **Adımları** | Kredi kartı numaraları gibi hassas verileri hello veritabanında şifrelenmiş toobe sahiptir. Veri sütun düzeyinde şifreleme kullanılarak şifrelenir veya hello şifreleme işlevleri kullanarak bir uygulama işlevi. |

## <a id="tde-enabled"></a>Bu veritabanı düzeyi şifreleme (TDE) etkin olduğundan emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [SQL Server saydam veri şifrelemesi (TDE) Anlama](https://technet.microsoft.com/library/bb934049(v=sql.105).aspx) |
| **Adımları** | Saydam veri şifreleme (TDE) özelliğini bir veritabanındaki hassas verileri şifrelemek içinde SQL server yardımcı olur ve bir sertifika ile kullanılan tooencrypt hello veri hello anahtarları koruyun. Bu herkes hello anahtarları olmadan hello veri kullanmasını önler. TDE verileri koruduğu "durağan" Merhaba veri ve günlük dosyaları anlamına gelir,. Merhaba özelliği toocomply pek çok yasalar, düzenlemeler ve çeşitli sektörün oluşturduğu yönergeleri sağlar. |

## <a id="backup"></a>Veritabanı Yedeklemeleri şifrelendiğinden emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | SQL Azure, OnPrem |
| **Öznitelikleri**              | SQL sürüm - V12, SQL sürümü - MsSQL2014 |
| **Başvuruları**              | [SQL veritabanı yedekleme şifreleme](https://msdn.microsoft.com/library/dn449489) |
| **Adımları** | SQL Server Yedekleme oluşturulurken hello özelliği tooencrypt hello veri vardır. Merhaba şifreleme algoritması ve hello Şifreleyici (sertifika veya asimetrik anahtar) belirterek bir yedek oluşturulduğunda, şifrelenmiş bir yedek dosya oluşturmayı seçebilirsiniz. |

## <a id="api-browser"></a>API tarayıcının depoda depolanmaz bu hassas verileri ilgili tooWeb emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web API | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | MVC 5, MVC 6 |
| **Öznitelikleri**              | Kimlik sağlayıcısı - ADFS, kimlik sağlayıcısı - Azure AD |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>Belirli uygulamalarında hassas yapıları ilgili tooWeb API'nin kimlik doğrulaması tarayıcının yerel depolama alanına depolanır. Örneğin, Azure AD kimlik doğrulama yapıları adal.idtoken, adal.nonce.idtoken, adal.access.token.key, adal.token.keys, adal.state.login, adal.session.state, adal.expiration.key vb. ister.</p><p>Tüm bu yapıtların sonra bile kullanılabilir oturumu veya tarayıcı kapalı. Bir saldırganın toothese yapıları erişim alırsa, klasöründe tooaccess hello korumalı kaynaklar (API) kullanabilirsiniz. Tüm hassas yapıları ilgili tooWeb API tarayıcının depoda depolanmaz emin olun. İstemci-tarafı depolama olduğu kaçınılmaz durumlarda (örneğin, tek sayfa uygulamaları (örtük Openıdconnect/OAuth akış yararlanan SPA) gerek yerel olarak toostore erişim belirteçleri), kullanım depolama seçenekleriyle Kalıcılık sahip değil. Örneğin, SessionStorage tooLocalStorage tercih eder.</p>| 

### <a name="example"></a>Örnek
JavaScript kod parçacığı aşağıda Hello yerel depolama alanına kimlik doğrulaması yapıları depolayan bir özel kimlik doğrulama kitaplığı arasındadır. Bu tür uygulamalar kaçınılmalıdır. 
```javascript
ns.AuthHelper.Authenticate = function () {
window.config = {
instance: 'https://login.microsoftonline.com/',
tenant: ns.Configurations.Tenant,
clientId: ns.Configurations.AADApplicationClientID,
postLogoutRedirectUri: window.location.origin,
cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
};
```

## <a id="encrypt-docdb"></a>Cosmos DB içinde depolanan hassas verileri şifrele

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure belge DB | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Belge DB depolamadan önce uygulama düzeyinde hassas verileri şifrelemek veya herhangi bir duyarlı veri Azure Storage veya Azure SQL gibi diğer depolama çözümleri depolayın| 

## <a id="disk-vm"></a>Sanal makineler tarafından kullanılan Azure Disk şifrelemesi tooencrypt diskleri kullanmak

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Iaas VM güven sınırı | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Azure Disk Şifrelemesi'ni kullanarak tooencrypt diskleri kullanılan, sanal makineleriniz tarafından](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) |
| **Adımları** | <p>Azure Disk şifrelemesi şu anda önizlemede olan yeni bir özelliktir. Bu özellik tooencrypt hello işletim sistemi ve bir Iaas sanal makine tarafından kullanılan veri disklerle sağlar. Windows için hello sürücüler, endüstri standardı BitLocker şifreleme teknolojisi kullanılarak şifrelenir. Linux için hello diskleri hello DM-Crypt teknolojisi kullanılarak şifrelenir. Bu Azure anahtar kasası tooallow ile toocontrol tümleşik ve hello disk şifreleme anahtarlarını yönetme. Hello Azure Disk şifrelemesi çözümü üç müşteri şifreleme senaryoları aşağıdaki hello destekler:</p><ul><li>Müşteri şifreli VHD dosyaları ve Azure anahtar kasasında depolanan müşteri tarafından sağlanan şifreleme anahtarlarını oluşturulan yeni Iaas VM'ler şifrelemeyi etkinleştirin.</li><li>Azure Market hello oluşturulan yeni Iaas VM'ler şifrelemeyi etkinleştirin.</li><li>Zaten Azure'da çalışan Iaas VM'ler şifrelemeyi etkinleştirin.</li></ul>| 

## <a id="fabric-apps"></a>Service Fabric uygulamaları parolaları şifrelemek

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Service Fabric güven sınırı | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Ortam - Azure |
| **Başvuruları**              | [Service Fabric uygulamaları parolaları yönetme](https://azure.microsoft.com/documentation/articles/service-fabric-application-secret-management/) |
| **Adımları** | Gizli depolama bağlantı dizeleri, parolalar veya düz metin olarak işleneceğini olmayan diğer değerleri gibi herhangi bir önemli bilgi olabilir. Azure anahtar kasası toomanage anahtarları ve gizli anahtarları service fabric uygulamaları kullanın. |

## <a id="modeling-teams"></a>Güvenlik modelleme gerçekleştirebilir ve iş birimleri/takımlar kullanmak gerektiğinde

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Dynamics CRM | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Güvenlik modelleme gerçekleştirebilir ve iş birimleri/takımlar kullanmak gerektiğinde |

## <a id="entities"></a>Kritik varlıklar üzerinde erişim tooshare özelliği simge durumuna küçült

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Dynamics CRM | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Kritik varlıklar üzerinde erişim tooshare özelliği simge durumuna küçült |

## <a id="good-practices"></a>Merhaba Dynamics CRM paylaşım özelliğini ve iyi güvenlik uygulamaları ile ilişkili hello riskleri tren kullanıcılar

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Dynamics CRM | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Merhaba Dynamics CRM paylaşım özelliğini ve iyi güvenlik uygulamaları ile ilişkili hello riskleri tren kullanıcılar |

## <a id="exception-mgmt"></a>Özel Durum Yönetimi'nde yapılandırma ayrıntıları gösteren proscribing geliştirme standartları Kuralı Ekle

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Dynamics CRM | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Özel durum yönetimi geliştirme dışında yapılandırma ayrıntıları gösteren proscribing geliştirme standartları kuralı içerir. Bu kod gözden geçirme ya da düzenli denetleme bir parçası olarak test edin.|

## <a id="sse-preview"></a>Rest (Önizleme) verileri için Azure Storage hizmeti şifreleme (SSE) kullanın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Storage | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | StorageType - Blob |
| **Başvuruları**              | [Azure Storage hizmeti şifreleme (Önizleme) bekleyen veri için](https://azure.microsoft.com/documentation/articles/storage-service-encryption/) |
| **Adımları** | <p>Azure Storage hizmeti şifreleme (SSE) bekleyen veri için korumak ve Kuruluş güvenliği ve uyumluluk taahhüt veri toomeet korumaya yardımcı olur. Bu özellik ile Azure depolama otomatik olarak veri önceki toopersisting toostorage şifreler ve önceki tooretrieval şifresini çözer. Merhaba şifreleme, şifre çözme ve anahtar yönetimi tamamen saydam toousers. SSE ekleme blobları ve sayfa BLOB'ları yalnızca tooblock BLOB'lar geçerlidir. Merhaba diğer tablolar, kuyruklar ve dosyaları da dahil olmak üzere veri türleri şifrelenmez.</p><p>Şifreleme ve şifre çözme iş akışı:</p><ul><li>Merhaba müşteri hello depolama hesabı üzerinde şifrelemeyi etkinleştirir</li><li>Yeni veri (PUT Blob, PUT bloğu, PUT sayfası, vb.) tooBlob depolama hello müşteri yazdığında; Her yazma 256 bit AES Şifrelemesini hello güçlü blok şifrelemeler kullanılabilir biri kullanılarak şifrelenir</li><li>Merhaba müşteri tooaccess verileri (Blob alma, vb.) gerektiğinde veri toohello kullanıcı döndürmeden önce otomatik olarak çözülür</li><li>Şifreleme devre dışı bırakılırsa, yeni yazma artık şifrelenir ve mevcut şifrelenmiş verileri hello kullanıcı tarafından yeniden yazılmıştır kadar şifrelenmiş kalır. Şifreleme etkinken yazma tooBlob depolama şifrelenir. etkinleştirme/hello depolama hesabı için şifrelemeyi devre dışı bırakma arasında geçiş hello kullanıcıyla veri Hello durumunu değiştirmez</li><li>Tüm şifreleme anahtarları depolanan, şifrelenmiş ve Microsoft tarafından yönetilen</li></ul><p>Lütfen şu anda unutmayın, hello anahtarları hello şifreleme için kullanılan Microsoft tarafından yönetilir. Microsoft hello anahtarları başlangıçta oluşturur ve iç Microsoft İlkesi tarafından tanımlandığı şekilde hello güvenli depolama hello normal döndürme yanı sıra hello anahtarları yönetin. Hello gelecekteki, müşterilerin hello özelliği toomanage kendi alacağı > şifreleme anahtarları ve anahtarlar toocustomer yönetilen anahtarlardan Microsoft tarafından yönetilen bir geçiş yolu sağlar.</p>| 

## <a id="client-storage"></a>İstemci tarafı şifreleme toostore hassas verileri Azure depolama alanında kullanın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Storage | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [İstemci tarafı şifreleme ve Microsoft Azure depolama için Azure anahtar kasası](https://azure.microsoft.com/documentation/articles/storage-client-side-encryption/), [Öğreticisi: şifrelemek ve şifresini çözmek Azure anahtar kasası kullanılarak Microsoft Azure Storage blobları](https://azure.microsoft.com/documentation/articles/storage-encrypt-decrypt-blobs-key-vault/), [verileri güvenli depolama Azure Blob içinde Azure şifreleme uzantılı depolama](https://blogs.msdn.microsoft.com/partnercatalystteam/2015/06/17/storing-data-securely-in-azure-blob-storage-with-azure-encryption-extensions/) |
| **Adımları** | <p>.NET Nuget paketi için Azure Storage istemci kitaplığı Hello tooAzure depolama karşıya yükleme ve toohello istemci indirilirken verilerin şifresini çözmek önce istemci uygulamalar içinde verilerin şifrelenmesi destekler. Merhaba kitaplık ayrıca depolama hesabı anahtarı yönetimi için Azure anahtar kasası ile tümleştirmeyi destekler. Aşağıda, istemci tarafı şifreleme çalışma biçimine kısa bir açıklaması verilmiştir:</p><ul><li>simetrik anahtar bir kerelik kullan bir içerik şifreleme anahtarı (CEK) Hello Azure Storage istemci SDK oluşturur</li><li>Müşteri verileri bu CEK kullanılarak şifrelenir</li><li>Merhaba CEK sonra (Merhaba anahtar şifreleme anahtarı (KEK) kullanılarak şifrelenir) paketlenir. Merhaba KEK anahtar bir tanımlayıcıyla tanımlanır ve asimetrik anahtar çifti ya da bir simetrik anahtar olması ve yerel olarak yönetilebilir veya Azure anahtar kasasında depolanan. Merhaba depolama istemcinin kendisi hiçbir zaman erişim toohello KEK olur. Yalnızca, anahtar kasası tarafından sağlanan hello anahtar kaydırma algoritması çağırır. Müşteriler toouse özel sağlayıcılar anahtarı sarmalama/bunlar istiyorsanız açmak için seçebilir</li><li>Merhaba şifrelenmiş verileri ise toohello Azure depolama hizmeti karşıya yüklendi. Alt düzey uygulama ayrıntılarını hello başvurular bölümüne Hello bağlantılarını denetleyin.</li></ul>|

## <a id="pii-phones"></a>Duyarlı veya toophones yerel depolama yazılan PII veri şifreleme

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Mobil istemci | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel, Xamarin  |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Ayarları ve özellikleri cihazlarınızda Microsoft Intune ilkeleriyle yönetme](https://docs.microsoft.com/intune/deploy-use/manage-settings-and-features-on-your-devices-with-microsoft-intune-policies#create-a-configuration-policy), [Anahtarlık Valet](https://components.xamarin.com/view/square.valet) |
| **Adımları** | <p>Merhaba uygulaması kullanıcının PII (e-posta, telefon numarası, ad, Soyadı, Tercihler vb.) gibi hassas bilgileri yazıyorsa -mobile'nın dosya sisteminde sonra onu toohello yerel dosya sistemi yazmadan önce şifrelenmelidir. Merhaba uygulaması Kurumsal uygulama ise, Windows Intune kullanarak yayımlama uygulama hello olasılığını keşfedin.</p>|

### <a name="example"></a>Örnek
Intune aşağıdaki güvenlik ilkeleri toosafeguard hassas verilerle yapılandırılabilir: 
```C#
Require encryption on mobile device    
Require encryption on storage cards
Allow screen capture
```

### <a name="example"></a>Örnek
Merhaba uygulaması bir kurumsal uygulama, ardından anahtar deposu sağlanan kullanım platformu değilse, anahtarlıklar toostore şifreleme anahtarlarını, şifreleme işlemi kullanarak hello dosya sistemi üzerinde gerçekleştirilebilir. Kod parçacığını nasıl tooaccess xamarin kullanarak Anahtarlık anahtar gösterir: 
```C#
        protected static string EncryptionKey
        {
            get
            {
                if (String.IsNullOrEmpty(_Key))
                {
                    var query = new SecRecord(SecKind.GenericPassword);
                    query.Service = NSBundle.MainBundle.BundleIdentifier;
                    query.Account = "UniqueID";

                    NSData uniqueId = SecKeyChain.QueryAsData(query);
                    if (uniqueId == null)
                    {
                        query.ValueData = NSData.FromString(System.Guid.NewGuid().ToString());
                        var err = SecKeyChain.Add(query);
                        _Key = query.ValueData.ToString();
                    }
                    else
                    {
                        _Key = uniqueId.ToString();
                    }
                }

                return _Key;
            }
        }
```

## <a id="binaries-end"></a>Tooend kullanıcılara dağıtmadan önce oluşturulan ikili dosyaları belirsizleştirirseniz

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Mobil istemci | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [.Net için şifre gizleme](http://www.ssware.com/cryptoobfuscator/obfuscator-net.htm) |
| **Adımları** | Oluşturulan ikili dosyaları (apk içindeki derlemelerde) karıştırılmış toostop derlemelerinin mühendislik geriye doğru olması gerekir. Araçlar `CryptoObfuscator` bu amaç için kullanılabilir. |

## <a id="cert"></a>Set clientCredentialType tooCertificate ya da Windows

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | WCF | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | .NET framework 3 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Adımları** | Şifrelenmemiş bir kanal üzerinden düz metin parola ile bir UsernameToken kullanarak hello SOAP iletilerini bulmak hello parola tooattackers kullanıma sunar. Merhaba UsernameToken kullanan hizmet sağlayıcılar, parolaları düz metin olarak gönderilir kabul edebilir. Düz metin parolalarını şifrelenmemiş bir kanal üzerinden gönderme hello SOAP iletisi bulmak hello kimlik bilgisi tooattackers getirebilir. | 

### <a name="example"></a>Örnek
Merhaba aşağıdaki WCF hizmet sağlayıcısı yapılandırmasını hello UsernameToken kullanır: 
```
<security mode="Message"> 
<message clientCredentialType="UserName" />
``` 
ClientCredentialType tooCertificate ya da Windows ayarlayın. 

## <a id="security"></a>WCF güvenlik modu etkin değil

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | WCF | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel, .NET Framework 3 |
| **Öznitelikleri**              | Güvenlik modu - taşıma, güvenlik modu - iletisi |
| **Başvuruları**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Krallık Fortify](https://vulncat.fortify.com/en/vulncat/index.html), [WCF güvenlik temel ilkeleri dergisi kod](http://www.codemag.com/article/0611051) |
| **Adımları** | Taşıma veya ileti güvenlik tanımlandı. İletileri aktarım olmadan veya güvenlik hello bütünlüğü veya gizliliği hello iletilerinin garanti edemez ileti iletme uygulamalar. WCF güvenlik bağlama tooNone ayarladığınızda, taşıma ve ileti güvenliği devre dışı bırakılır. |

### <a name="example"></a>Örnek
Merhaba aşağıdaki yapılandırma hello güvenlik modu tooNone ayarlar. 
```
<system.serviceModel> 
  <bindings> 
    <wsHttpBinding> 
      <binding name=""MyBinding""> 
        <security mode=""None""/> 
      </binding> 
  </bindings> 
</system.serviceModel> 
```

### <a name="example"></a>Örnek
Tüm hizmet bağlamaları arasında güvenlik modu beş olası güvenlik modu bulunmaktadır: 
* yok. Güvenlik kapatır. 
* Taşıma. Aktarım güvenliği karşılıklı kimlik doğrulaması ve ileti koruması için kullanır. 
* İleti. İleti güvenliği için karşılıklı kimlik doğrulama ve ileti koruması kullanır. 
* Her ikisi de. Taşıma ve ileti düzeyi güvenlik (yalnızca MSMQ bu destekler) için toosupply ayarları sağlar. 
* TransportWithMessageCredential. Kimlik bilgileri hello iletisi ve ileti koruma ile aktarılır ve sunucu kimlik doğrulaması hello Aktarım katmanı tarafından sağlanır. 
* TransportCredentialOnly. İstemci kimlik bilgileri hello Aktarım katmanı ile aktarılır ve ileti koruma uygulanır. Taşıma ve ileti güvenlik tooprotect hello bütünlüğü ve gizliliği iletilerinin kullanın. Merhaba yapılandırma aşağıdaki ileti kimlik bilgileri ile Merhaba hizmet toouse taşıma güvenliği söyler.
```
<system.serviceModel>
  <bindings>
    <wsHttpBinding>
    <binding name=""MyBinding""> 
    <security mode=""TransportWithMessageCredential""/> 
    <message clientCredentialType=""Windows""/> 
    </binding> 
  </bindings> 
</system.serviceModel> 
```
