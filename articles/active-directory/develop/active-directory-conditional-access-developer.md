---
title: "aaaDeveloper Azure Active Directory koşullu erişim için Kılavuzu | Microsoft Docs"
description: "Geliştirici Kılavuzu ve Azure AD koşullu erişim senaryoları"
services: active-directory
keywords: 
author: danieldobalian
manager: mbaldwin
editor: PatAltimore
ms.author: dadobali
ms.date: 07/19/2017
ms.assetid: 115bdab2-e1fd-4403-ac15-d4195e24ac95
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.openlocfilehash: 589393f5d084d64872b372d895dc889f300592bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="developer-guidance-for-azure-active-directory-conditional-access"></a>Azure Active Directory koşullu erişim için Geliştirici Kılavuzu

Azure Active Directory (AD) uygulamanızı birkaç yolu toosecure sunar ve hizmet koruyun.  Bu benzersiz özellikleri koşullu erişim biridir.  Koşullu erişim, geliştiricilerin ve kurumsal müşteriler tooprotect hizmetler dahil olmak üzere çok sayıda sağlar:

* Multi-factor authentication
* Kayıtlı cihazlar tooaccess belirli hizmetleri yalnızca Intune izin verme
* Kullanıcı konumları ve IP kısıtlama aralıkları

Koşullu erişim hello tam özellikleri hakkında daha fazla bilgi için bkz: [hello Klasik Azure portalı koşullu erişim](../active-directory-conditional-access.md). 

Bu makalede, hangi koşullu erişim toodevelopers yapı uygulamaları için Azure AD anlamına gelir üzerinde odaklanın.  Bilgisi varsayar [tek](active-directory-integrating-applications.md) ve [çok kiracılı](active-directory-devhowto-multi-tenant-overview.md) uygulamaları ve [ortak kimlik doğrulama desenler](active-directory-authentication-scenarios.md).

Biz, koşullu erişim ilkelerinin uygulandığı olabilir üzerinde denetime sahip değilseniz kaynaklara erişme hello etkisi dalın.  Ayrıca, biz hello hello üzerinde-temsili akış, koşullu erişim etkilerini web uygulamaları hello Microsoft Graph erişme ve API'larını çağırma keşfedin.

## <a name="how-does-conditional-access-impact-an-app"></a>Koşullu erişim uygulama nasıl etkiler?

### <a name="app-topologies-impacted"></a>Etkilenen uygulama topolojileri

En yaygın durumlarda, koşullu erişim bir uygulamanın davranışı değiştirmez veya hello geliştiriciden herhangi bir değişiklik gerektirmez.  Bir uygulama bir hizmet için bir belirteç dolaylı ya da sessizce istediğinde yalnızca belirli durumlarda bir uygulama toohandle koşullu erişim "zorluklarını" kod değişiklikleri gerektirir.  Etkileşimli bir oturum açma isteği gerçekleştirme olarak kadar basit olabilir. 

Özellikle, hello aşağıdaki senaryolar kod toohandle koşullu erişim "zorluklar" gerektirir: 

* Merhaba Microsoft Graph erişen uygulamaları
* Uygulamaları Hello üzerinde-temsili akış gerçekleştirme
* Uygulamaları birden çok Hizmetleri/kaynaklara erişme
* Tek sayfa uygulamaları ADAL.js kullanma

Koşullu erişim ilkeleri uygulanan toohello uygulama olabilir, ancak uygulanan tooa web API uygulamanızı de olabilir erişir. toolearn nasıl tooconfigure bir koşullu erişim ilkesi, lütfen bakın hakkında daha fazla bilgi [Azure Active Directory koşullu erişimi kullanmaya başlama](../active-directory-conditional-access-azuread-connected-apps.md#configure-per-application-access-rules).

Merhaba senaryosu bağlı olarak, bir kuruluş müşteri uygulamak ve herhangi bir zamanda koşullu erişim ilkeleri kaldırmak.  Yeni bir ilke uygulandığında, uygulama toocontinue çalışmasını için sırayla tooimplement hello "sınama" işleme gerekir. Örnek hello sınama işleme gösterilmektedir. 

### <a name="conditional-access-examples"></a>Koşullu erişim örnekleri

Başkalarının olduğu gibi çalışır ancak bazı senaryolar kod değişiklikleri toohandle koşullu erişim gerektirir.  Merhaba fark bazı fikirler verir koşullu erişim toodo çok faktörlü kimlik doğrulaması kullanan bazı senaryolar verilmiştir.

* Bir tek Kiracı iOS uygulaması oluşturmak ve bir koşullu erişim ilkesi uygula.  Merhaba uygulama bir kullanıcı oturum açtığında ve erişim tooan API isteği değil.  Merhaba kullanıcı oturum açtığında hello ilkesi otomatik olarak çağrılır ve hello kullanıcı tooperform multi-Factor authentication (MFA) gerekir. 
* Diğer hizmetler arasında hello Microsoft Graph tooaccess Exchange, kullanan bir çok kiracılı web uygulaması oluşturuyorsanız.  Bu uygulamayı uyarlar bir enterprise müşterileri bir ilke SharePoint Online'da ayarlar.  Merhaba web uygulaması için MS Graph bir belirteç istediğinde, tüm Microsoft Service bir ilkenin geçerli olduğu (özellikle grafik erişilebilen hizmetler).  Bu son kullanıcı MFA için istenir. Merhaba durumda hello son kullanıcı oturum geçerli belirteçlerini imzalı, bir talep "challenge" toohello web uygulamasına döndürülür.  
* Orta katman hizmet tooaccess hello Microsoft Graph kullanan yerel bir uygulama oluşturmakta olduğunuz.  Bir kuruluş müşteri bu uygulamayı kullanarak hello şirket ilkesi tooExchange çevrimiçi geçerlidir.  Bir son kullanıcı oturum açtığında hello yerel uygulama erişim toohello orta katman isteklerini ve hello belirteci gönderir.  Merhaba orta katman üzerinde-temsili akış toorequest erişim toohello MS Graph gerçekleştirir.  Bu noktada, bir talep "challenge" toohello orta katman sunulur. Merhaba orta katman hello koşullu erişim ilkesi ile toocomply gereken hello sınama geri toohello yerel uygulama, gönderir.

### <a name="complying-with-a-conditional-access-policy"></a>Koşullu erişim ilkesi ile uymak

Merhaba oturum kurulduğunda birçok farklı uygulama Topolojileri için bir koşullu erişim ilkesi değerlendirilir.  Bir koşullu erişim ilkesi hello kesinliği uygulamaları ve hizmetleri üzerinde çalıştığı gibi çalışır, hangi çağrılması hello noktası yoğun bir şekilde bağlıdır hello senaryosunda tooaccomplish çalıştığınız.

Uygulamanızı tooaccess koşullu erişim ilkesi ile bir hizmeti çalıştığında, bir koşullu erişim challenge karşılaşabilirsiniz.  Bu sorunu hello kodlanmış `claims` Azure AD'den bir yanıt gelir veya Microsoft Graph hello parametre.  Bu sınama parametre bir örneği burada verilmiştir: 

```
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

Geliştiriciler, bu sorunu ele ve yeni istek tooAzure AD ekleyin.  Bu durum geçirme hello son kullanıcı tooperform herhangi bir eylem gerekli toocomply hello koşullu erişim ilkesi ile ister. Senaryoları aşağıdaki hello hello hata ve nasıl tooextract hello parametre özellikleri açıklanmıştır. 

## <a name="scenarios"></a>Senaryolar

### <a name="prerequisites"></a>Ön koşullar

Azure AD koşullu erişim, bulunan bir özelliktir [Azure AD Premium](../active-directory-whatis.md#choose-an-edition).  Lisans hello gereksinimleri hakkında daha fazla bilgiyi [lisanssız kullanım raporu](../active-directory-conditional-access-unlicensed-usage-report.md).  Geliştiriciler hello katılma [Microsoft Developer Network](https://msdn.microsoft.com/dn308572.aspx), ücretsiz aboneliği toohello Azure AD Premium içeren Enterprise Mobility Suite içerir.

### <a name="considerations-for-specific-scenarios"></a>Belirli senaryolar için ilgili önemli noktalar

yalnızca bilgi aşağıdaki hello Bu koşullu erişim senaryolarda geçerlidir:

* Merhaba Microsoft Graph erişen uygulamaları
* Uygulamaları Hello üzerinde-temsili akış gerçekleştirme
* Uygulamaları birden çok Hizmetleri/kaynaklara erişme
* Tek sayfa uygulamaları ADAL.js kullanma

Aşağıdaki bölümlerde hello senaryoları daha karmaşık biz ortak elde edersiniz.  ilkeye işletim hello çekirdeği koşullu erişim ilkeleri hello süredir hello belirteci istenen Microsoft Graph hello erişilen sürece uygulanan bir koşullu erişim ilkesine sahip hello hizmeti değerlendirilir olur.

### <a name="scenario-app-accessing-hello-microsoft-graph"></a>Senaryo: hello Microsoft Graph erişme uygulama

Bir web uygulamasına erişim toohello Microsoft Graph istediğinde bu senaryoda, biz hello çalışması yol. Merhaba koşullu erişim ilkesi, bu durumda tooSharePoint, Exchange veya Microsoft Graph hello aracılığıyla bir iş yükü olarak erişilen başka bir hizmet atanabilir.  Bu örnekte, Sharepoint Online'da koşullu erişim ilkesi bulunmamaktadır varsayalım.

![Uygulama Hello Microsoft Graph Akış Diyagramı erişme](media/active-directory-conditional-access-developer/app-accessing-microsoft-graph-scenario.png)

Merhaba uygulama ilk yetkilendirme toohello koşullu erişimi olmadan bir aşağı akış iş yükü erişim gerektiren Microsoft Graph ister.  herhangi bir ilke çağırmadan Hello istek başarılı olur ve hello uygulama için Microsoft Graph belirteçlerini alır.  Bu noktada, hello uygulama hello erişim belirteci bir taşıyıcı isteğinde istenen hello uç noktası için kullanabilir. Şimdi, örneğin tooaccess Microsoft Graph, Sharepoint Online bir uç noktasını hello uygulama gerekir:`https://graph.microsoft.com/v1.0/me/mySite`

Merhaba yeni istek yeni bir belirteç verilen olmadan gerçekleştirebilmek için hello uygulamanın zaten hello Microsoft Graph için geçerli bir belirteci yok. Bu istek başarısız olur ve bir talep challenge, Microsoft Graph biçiminde hello bir HTTP 403 Yasak ile verildiği bir ```WWW-Authenticate``` sınaması.
Merhaba yanıt bir örneği burada verilmiştir: 

```
HTTP 403; Forbidden 
error=insufficient_claims
www-authenticate="Bearer realm="", authorization_uri="https://login.windows.net/common/oauth2/authorize", client_id="<GUID>", error=insufficient_claims, claims={"access_token":{"polids":{"essential":true,"values":["<GUID>"]}}}"
```

Merhaba talepleri içinde hello iştir ```WWW-Authenticate``` hello sonraki istek için ayrıştırılmış tooextract hello talep parametresi olabilir üstbilgi.  Eklenen toohello yeni istek olduktan sonra Azure AD hello kullanıcı ve hello uygulama imzalama şimdi hello koşullu erişim ilkesi uyumlu olduğunda tooevaluate hello koşullu erişim ilkesi bilir.  Merhaba isteği toohello Sharepoint Online yinelenen uç nokta başarılı olur.

Toohello nasıl toohandle hello sınama talep gösteren kod örnekleri için bkz [.NET masaüstü kod örneği](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) ADAL .NET veya hello [üzerinde-adına-kodunu örnek](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca) ADAL .NET için.

### <a name="scenario-app-performing-hello-on-behalf-of-flow"></a>Senaryo: hello üzerinde-temsili akış gerçekleştirme uygulama

Bu senaryoda, yerel bir uygulama bir web hizmeti/API çağrılarının hello çalışması yol.  Buna karşılık, bu hizmeti yapar [hello "üzerinde-temsili" akış](active-directory-authentication-scenarios.md#application-types-and-scenarios) toocall bir aşağı akış hizmeti.  Bu örnekte, koşullu erişim ilkesi toohello aşağı akış hizmetimizi (Web API 2) uyguladıysanız ve sunucu/arka plan programı uygulama yerine yerel bir uygulama kullanarak. 

![Uygulama Hello üzerinde-adına-Akış Diyagramı gerçekleştirme](media/active-directory-conditional-access-developer/app-performing-on-behalf-of-scenario.png)

Web API 1 her zaman hello aşağı akış API isabet değil gibi hello ilk belirteç isteği, Web API 1 için çok faktörlü kimlik doğrulaması için hello son kullanıcı istemez.  Web API 1 toorequest üzerinde-adına-of belirteci hello kullanıcı için Web API 2 çalışır sonra hello kullanıcı çok faktörlü kimlik doğrulaması ile oturum imzalamamış beri hello istek başarısız olur.

Azure AD bazı ilginç veriler sahip bir HTTP yanıtı döndürür: 

> [!NOTE]
> Bu örnekte, çok faktörlü kimlik doğrulaması hata açıklaması, ancak çeşitli `interaction_required` ilgili olası tooconditional erişim.  

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API 2 App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

Bizim Web API 1'de, biz hello hata catch `error=interaction_required`ve geri hello gönderme `claims` sınama toohello masaüstü uygulaması.  Bu noktada, hello Masaüstü uygulama yeni bir yapabilir `acquireToken()` çağırın ve hello ilave `claims`ek sorgu dizesi parametresi olarak sınama.  Bu yeni istek hello kullanıcı toodo çok faktörlü kimlik doğrulaması gerektirir ve bu yeni belirteci geri tooWeb API 1 ve tam hello üzerinde-temsili akış gönderin.

Bu senaryo, çıkışı tootry bkz bizim [.NET kod örneği](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca).  Nasıl toopass talep sınama geri uygulamasından Web API'si 1 toohello yerel hello ve hello istemci app içinde yeni bir istek oluşturun gösterir. 

### <a name="scenario-app-accessing-multiple-services"></a>Senaryo: uygulama birden çok hizmetlere erişme

Bu senaryoda, bunlardan biri atanan bir koşullu erişim ilkesine sahip bir web uygulaması iki hizmet erişen hello çalışması yol.  Uygulama mantığınızı bağlı olarak, uygulamanızı erişim tooboth web hizmetleri gerektirmeyen bir yolu bulunabilir.  Bu senaryoda, bir belirteç istemek hello sipariş hello son kullanıcı deneyimini önemli bir rol oynar.

Web hizmeti A ve B sahibiz ve web hizmeti B uygulanan bizim koşullu erişim ilkesine sahip varsayalım.  Merhaba ilk etkileşimli kimlik doğrulama isteği için her iki hizmet izni gerektirse hello koşullu erişim ilkesini her durumda gerekli değildir.  Merhaba uygulama web hizmeti B için bir belirteç isterse hello İlkesi çağrılır ve web hizmeti bir sonraki istekleri de başarılı şekilde.

![Uygulama Hizmetleri birden çok akış diyagramı erişme](media/active-directory-conditional-access-developer/app-accessing-multiple-services-scenario.png)

Alternatif olarak, Hello uygulama web hizmeti bir for başlangıçta bir belirteç isterse, hello son kullanıcı hello koşullu erişim ilkesi çağrılmaz.  Bu hello uygulama geliştiricisi toocontrol hello son kullanıcı deneyimi sağlar ve her durumda çağrılan hello koşullu erişim ilkesi toobe zorla sağlamaz. Merhaba hassas hello uygulama daha sonra b web hizmeti için bir belirteç isteklerini varsa durumdur Bu noktada, hello son kullanıcı hello koşullu erişim ilkesi ile toocomply gerekir.  Merhaba uygulama bulunduğunda çok`acquireToken`, aşağıdaki hata (hello Aşağıdaki diyagramda gösterilmiştir) hello oluşturabilirsiniz: 

```
HTTP 400; Bad Request
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
``` 

![Uygulama yeni bir belirteç isteme birden çok hizmetlere erişme](media/active-directory-conditional-access-developer/app-accessing-multiple-services-new-token.png)

Merhaba uygulama hello ADAL kitaplığı kullanıyorsanız, bir hata tooacquire hello belirteci her zaman etkileşimli olarak yeniden denenir.  Bu etkileşimli istek oluştuğunda hello son kullanıcı hello fırsat toocomply hello koşullu erişimle sahiptir.  Merhaba isteği sürece bu doğrudur bir `AcquireTokenSilentAsync` veya `PromptBehavior.Never` ; bu durumda tooperform etkileşimli bir hello uygulamanın ihtiyacı ```AcquireToken``` toogive hello son kullanım hello fırsat toocomply hello İlkesi ile istek. 

### <a name="scenario-single-page-app-spa-using-adaljs"></a>Senaryo: Tek sayfa uygulaması (ADAL.js kullanarak SPA)

Bu senaryoda, biz tek sayfalı uygulama (SPA) varsa, biz hello çalışması yol, ADAL.js toocall kullanarak bir koşullu erişim web API korumalı.  Bu basit bir mimaridir ancak koşullu erişim geçici bir çözüm geliştirirken dikkate toobe gereken bazı küçük farklar vardır.

ADAL.js içinde belirteçleri elde birkaç işlevleri vardır: `login()`, `acquireToken(...)`, `acquireTokenPopup(…)`, ve `acquireTokenRedirect(…)`. 

* `login()`etkileşimli bir oturum açma isteği aracılığıyla bir kimliği belirteci alır ancak (korumalı koşullu erişim web API dahil) herhangi bir hizmeti için erişim belirteçleri elde değil.  
* `acquireToken(…)`ardından olması kullanılan toosilently elde edebilirsiniz bir erişim belirteci hiçbir durumda UI göstermez anlamına gelir.  
* `acquireTokenPopup(…)`ve `acquireTokenRedirect(…)` kullanılan iki toointeractively isteği bunlar her zaman göster oturum açma Arabirimine yani bir kaynak için bir belirteç olan.

Bir uygulamanın bir erişim belirteci toocall bir Web API ihtiyacı olduğunda çalışır bir `acquireToken(…)`.  Merhaba belirteci oturum süresi doldu veya koşullu erişim ilkesi ile toocomply ihtiyacımız, ardından hello *acquireToken* işlev başarısız olur ve hello uygulama kullandığı `acquireTokenPopup()` veya `acquireTokenRedirect()`.

![ADAL akış diyagramı kullanarak tek sayfa uygulaması](media/active-directory-conditional-access-developer/spa-using-adal-scenario.png)

Şimdi bir koşullu erişim Senaryomuzda örnekle yol.  Merhaba son kullanıcı yalnızca hello sitesinde landed ve bir oturum yok.  Biz gerçekleştirmek bir `login()` çağrı, bir kimliği olmadan çok faktörlü kimlik doğrulaması belirteci alma.  Ardından hello kullanıcı hello uygulama toorequest verileri bir Web API gerektiren bir düğme kadardır.  Merhaba uygulama çalıştığında toodo bir `acquireToken()` araması ancak başarısız hello kullanıcı henüz çok faktörlü kimlik doğrulaması gerçekleştirmediği ve hello koşullu erişim ilkesi ile toocomply gerekiyor.

Azure AD HTTP yanıtı aşağıdaki geri hello gönderir: 

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
```

Bizim uygulamanın toocatch hello ihtiyacı `error=interaction_required`.  Merhaba uygulama daha sonra ya da kullanabilirsiniz `acquireTokenPopup()` veya `acquireTokenRedirect()` üzerinde hello aynı kaynak.  Merhaba, çok faktörlü kimlik doğrulamasını zorunlu toodo kullanıcıdır. Merhaba kullanıcı hello çok faktörlü kimlik doğrulaması tamamlandıktan sonra hello uygulama baştan verilen hello için erişim belirtecini istenen kaynak.

Bu senaryo, çıkışı tootry bkz bizim [JS SPA üzerinde-adına-kodunu örnek](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca).  Bu kod örneği, hello koşullu erişim ilkesini ve web bu senaryo ile JS SPA toodemonstrate önceki kayıtlı API kullanır. Nasıl tooproperly tanıtıcı hello talep sınama ve Web API için kullanılan bir erişim belirteci almak gösterir. Alternatif olarak, genel kullanıma hello [Angular.js kod örneği](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) Açısal SPA hakkında yönergeler için


## <a name="see-also"></a>Ayrıca bkz.

* toolearn hello yetenekleri hakkında daha fazla bilgi görmek [Azure AD'de koşullu erişim](../active-directory-conditional-access.md).
* Daha fazla Azure AD kod örnekleri için bkz: [Github deposuna kod örnekleri](https://github.com/azure-samples?utf8=%E2%9C%93&q=active-directory). 
* Merhaba ADAL SDK'ın ve erişim hello başvuru belgeleri hakkında daha fazla bilgi için bkz: [kitaplığı Kılavuzu](active-directory-authentication-libraries.md).
* çok kiracılı senaryoları hakkında daha fazla toolearn bkz [nasıl toosign hello çok kiracılı desenini kullanarak kullanıcıların](active-directory-devhowto-multi-tenant-overview.md).
