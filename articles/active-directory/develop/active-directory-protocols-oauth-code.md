---
title: "aaaUnderstand hello OAuth 2.0 yetkilendirme kodu akışını Azure AD'de | Microsoft Docs"
description: "Bu makalede toouse HTTP iletileri tooauthorize nasıl erişim tooweb uygulamaları ve web API'leri Azure Active Directory ve OAuth 2.0 kullanarak kiracınızda açıklanmaktadır."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: de3412cb-5fde-4eca-903a-4e9c74db68f2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4a6fe67d786a5fcb87d1059c2e94ba0c88d26cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# OAuth 2.0 ile Azure Active Directory kullanarak erişim tooweb uygulamaları yetkilendirmek
Azure Active Directory (Azure AD), tooauthorize erişim tooweb uygulamaları ve web API'leri Azure AD kiracınızda OAuth 2.0 tooenable kullanır. Bu kılavuz dilden bağımsızdır ve açıklar nasıl toosend ve bizim açık kaynak kitaplıkları kullanmadan HTTP iletileri alabilirsiniz.

Merhaba OAuth 2.0 yetkilendirme kodu akışını açıklanan [4.1 hello OAuth 2.0 belirtimi bölüm](https://tools.ietf.org/html/rfc6749#section-4.1). Kullanılan tooperform kimlik doğrulama ve yetkilendirme web uygulamaları dahil olmak üzere çoğu uygulama türleri ve yerel olarak yüklü uygulamalar.

[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)]

## OAuth 2.0 yetkilendirme akışı
Yüksek düzeyde, bir uygulama için hello tüm yetkilendirme akışı biraz şöyle:

![OAuth kimlik doğrulama kodu akışı](media/active-directory-protocols-oauth-code/active-directory-oauth-code-flow-native-app.png)

## İstek bir kimlik doğrulama kodu
Merhaba yetkilendirme kodu akışı başlar hello kullanıcı toohello yönlendirerek hello istemcisiyle `/authorize` uç noktası. Bu istekte hello istemci hello kullanıcıdan tooacquire gereken hello izinleri gösterir. Sayfasından uygulamanızın Azure Klasik portalında hello hello OAuth 2.0 uç noktaları alabilirsiniz **uç noktalarını görüntüle** düğmesini hello alt bölümü.

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&resource=https%3A%2F%2Fservice.contoso.com%2F
&state=12345
```

| Parametre |  | Açıklama |
| --- | --- | --- |
| Kiracı |Gerekli |Merhaba `{tenant}` değeri hello isteği hello yolunda hello uygulamasına oturum kullanılan toocontrol olabilir.  Merhaba izin verilen değerler: Kiracı tanımlayıcıları, örneğin, `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` veya `contoso.onmicrosoft.com` veya `common` Kiracı bağımsız belirteçleri |
| client_id |Gerekli |Azure AD ile kaydolurken hello uygulama kimliği atanan tooyour uygulama. Bu hello Azure portalında bulabilirsiniz. Tıklatın **Active Directory**hello dizin, hello uygulamayı seçin ve öğesini tıklatın **Yapılandır** |
| response_type |Gerekli |İçermelidir `code` hello yetkilendirme kodu akışı. |
| redirect_uri |Önerilen |Burada kimlik doğrulama yanıtları gönderilebilen veya uygulamanız tarafından alınan, uygulamanızın Hello redirect_uri.  Bu tam olarak bir url kodlanmış olmalıdır dışında hello Portalı'nda kayıtlı hello redirect_uris eşleşmelidir.  Yerel & mobil uygulamaları için hello varsayılan değeri kullanması gereken `urn:ietf:wg:oauth:2.0:oob`. |
| response_mode |Önerilen |Kullanılan toosend hello elde edilen belirteci geri tooyour uygulama olmalıdır hello yöntemini belirtir.  Olabilir `query` veya `form_post`. |
| durum |Önerilen |Ayrıca hello belirteci yanıtta döndürülen hello isteği dahil bir değer. Rastgele oluşturulan benzersiz bir değer tipik olarak kullanılan [siteler arası istek sahteciliğini saldırılarını önleme](http://tools.ietf.org/html/rfc6749#section-10.12).  hello sayfa veya görünüm üzerinde oldukları gibi Hello kimlik doğrulama isteği oluşmadan önce hello durumu ayrıca kullanılan tooencode hello uygulamasında hello kullanıcının durumu hakkındaki bilgilerdir. |
| Kaynak |İsteğe bağlı |Merhaba uygulama kimliği URI'si hello Web API (güvenli kaynak). toofind hello uygulama kimliği URI'sini hello web API, hello Azure Portal'ı tıklatın **Active Directory**, hello dizin'i tıklatın, hello uygulama'yı tıklatın ve ardından **yapılandırma**. |
| istemi |İsteğe bağlı |Gerekli bir kullanıcı etkileşimi Hello türünü gösterir.<p> Geçerli değerler şunlardır: <p> *oturum açma*: hello kullanıcı istendiğinde tooreauthenticate olması gerekir. <p> *onay*: kullanıcı izni verildi, ancak güncelleştirilmiş toobe gerekiyor. Merhaba kullanıcı istendiğinde tooconsent olmalıdır. <p> *admin_consent*: bir yönetici kendi kuruluşunuzdaki tüm kullanıcılar adına istendiğinde tooconsent olmalıdır |
| login_hint |İsteğe bağlı |Kullanıcı adlarını önceden biliyorsanız kullanılan toopre dolgu hello kullanıcı adı/e-posta adresi alanı hello kullanıcı oturum açma hello sayfanın olabilir.  Genellikle uygulamaları yeniden kimlik doğrulaması, bir önceki oturum bileşeninden hello kullanıcı adı zaten ayıklanan sırasında bu parametreyi kullanın hello kullanarak `preferred_username` talep. |
| domain_hint |İsteğe bağlı |Merhaba Kiracı veya kullanıcı hello etki alanı hakkında bir ipucu içinde toosign kullanması gereken sağlar. Merhaba hello domain_hint hello Kiracı için kaydedilmiş bir etki alanı değeridir. Merhaba Kiracı Federasyon tooan şirket içi dizin ise, AAD toohello belirtilen Kiracı federasyon sunucusuna yönlendirir. |

> [!NOTE]
> Merhaba kullanıcı kuruluşun parçası ise, hello kuruluş yöneticisi onayı veya hello kullanıcı adına reddetmek ya hello kullanıcı tooconsent izin verir. yalnızca Merhaba yönetici izin verdiğinde hello kullanıcı hello seçeneği tooconsent verilir.
>
>

Merhaba kullanıcı tooenter bu noktada, sorular kendi kimlik bilgilerini ve onay toohello izinleri belirtilen hello `scope` sorgu parametresi. Merhaba kullanıcı kimliğini doğrular ve izin veren sonra Azure AD yanıt tooyour uygulama hello gönderir. `redirect_uri` isteğiniz adresi.

### Başarılı yanıt
Başarılı yanıt şöyle:

```
GET  HTTP/1.1 302 Found
Location: http://localhost/myapp/?code= AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA&session_state=7B29111D-C220-4263-99AB-6F6E135D75EF&state=D79E5777-702E-4260-9A62-37F75FF22CCE
```

| Parametre | Açıklama |
| --- | --- |
| admin_consent |Merhaba değeri True ise bir yönetici tooa onay isteği istemi rıza. |
| Kod |İstenen hello uygulama hello yetkilendirme kodu. Merhaba uygulaması hello yetkilendirme kodu toorequest bir erişim belirteci hello hedef kaynak için kullanabilirsiniz. |
| session_state |Merhaba geçerli kullanıcı oturumunu tanımlayan benzersiz bir değerdir. Bu değer bir GUID olduğundan ancak İnceleme geçirilen genel olmayan bir değer olarak değerlendirilmelidir. |
| durum |Bir durum parametresi hello istekte yer alıyorsa hello aynı değere hello yanıt olarak görünmelidir. Merhaba yanıt kullanmadan önce hello istek ve yanıtta hello durum değerlerinin aynı olduğundan emin hello uygulama tooverify için iyi bir uygulamadır. Bu toodetect yardımcı [siteler arası istek sahteciliği (CSRF) saldırılarını](https://tools.ietf.org/html/rfc6749#section-10.12) hello istemci karşı. |

### Hata yanıtı
Hata yanıtları toohello da gönderilebilir `redirect_uri` böylece Merhaba uygulaması bunları uygun şekilde işleyebilir.

```
GET http://localhost:12345/?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Parametre | Açıklama |
| --- | --- |
| error |Merhaba, bölüm 5.2 içinde tanımlanmış bir hata kodu değer [OAuth 2.0 yetkilendirme Framework](http://tools.ietf.org/html/rfc6749). Merhaba sonraki tabloda Azure AD döndürür hello hata kodları açıklanmaktadır. |
| error_description |Merhaba hatanın ayrıntılı bir açıklaması. Bu ileti belirtmezseniz toobe son kullanıcı dostu. |
| durum |Merhaba durum değeri hello istekte gönderilen ve hello yanıt tooprevent siteler arası istek sahtekarlığı (CSRF) saldırılarını döndürülen bir rastgele oluşturulmuş yeniden olmayan değeridir. |

#### Yetkilendirme uç noktası hataları için hata kodları
Merhaba aşağıdaki tabloda açıklanmaktadır hello hello döndürülebilecek çeşitli hata kodları `error` hello hata yanıtı parametresi.

| Hata kodu | Açıklama | İstemci eylemi |
| --- | --- | --- |
| invalid_request |Eksik gerekli parametre gibi protokol hatası. |Düzeltin ve hello isteği yeniden gönderin. Bu geliştirme hata ve genellikle ilk test sırasında yakalandı. |
| unauthorized_client |Merhaba istemci uygulaması olmadığından toorequest bir yetki kodu izin verilir. |Bu durum genellikle, Merhaba istemci uygulaması Azure AD'de kayıtlı değil veya toohello kullanıcının Azure AD kiracısı eklenmez genellikle ortaya çıkar. Merhaba uygulaması hello uygulama yüklemek ve tooAzure AD eklemek için yönerge hello kullanıcıyla isteyebilir. |
| ACCESS_DENIED |Kaynak sahibi izin reddedildi |Merhaba istemci uygulaması hello kullanıcı izin sürece devam edemiyor hello kullanıcı bildirebilir. |
| unsupported_response_type |Merhaba yetkilendirme sunucusu hello istekte hello yanıt türünü desteklemiyor. |Düzeltin ve hello isteği yeniden gönderin. Bu geliştirme hata ve genellikle ilk test sırasında yakalandı. |
| server_error |Merhaba sunucu beklenmeyen bir hatayla karşılaştı. |Merhaba isteği yeniden deneyin. Bu hatalar geçici koşulları neden olabilir. Merhaba istemci uygulaması toohello kullanıcı açıklayan yanıt tooa geçici hata ertelendi. |
| temporarily_unavailable |Merhaba geçici olarak meşgul toohandle hello isteği sunucusudur. |Merhaba isteği yeniden deneyin. Merhaba istemci uygulaması toohello kullanıcı açıklayan yanıt tooa geçici koşul ertelendi. |
| invalid_resource |Merhaba hedef kaynak mevcut değil, Azure AD, bulunamıyor veya düzgün yapılandırılmamış olduğundan geçerli değil. |Bu, varsa, hello kaynak hello Kiracı yapılandırılmadı gösterir. Merhaba uygulaması hello uygulama yüklemek ve tooAzure AD eklemek için yönerge hello kullanıcıyla isteyebilir. |

## Merhaba yetkilendirme kodu toorequest bir erişim belirteci kullanın
Bir yetkilendirme kodu edindiğiniz ve hello kullanıcı tarafından izin verilen göre bir POST isteği toohello göndererek hello kod bir erişim belirteci toohello istenen kaynak için kullanmak `/token` uç noktası:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded
grant_type=authorization_code
&client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA
&redirect_uri=https%3A%2F%2Flocalhost%2Fmyapp%2F
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=p@ssw0rd

//NOTE: client_secret only required for web apps
```

| Parametre |  | Açıklama |
| --- | --- | --- |
| Kiracı |Gerekli |Merhaba `{tenant}` değeri hello isteği hello yolunda hello uygulamasına oturum kullanılan toocontrol olabilir.  Merhaba izin verilen değerler: Kiracı tanımlayıcıları, örneğin, `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` veya `contoso.onmicrosoft.com` veya `common` Kiracı bağımsız belirteçleri |
| client_id |Gerekli |Azure AD ile kaydolurken hello uygulama kimliği atanan tooyour uygulama. Bu hello Azure Klasik portalında bulabilirsiniz. Tıklatın **Active Directory**hello dizin, hello uygulamayı seçin ve öğesini tıklatın **Yapılandır** |
| grant_type |Gerekli |Olmalıdır `authorization_code` hello yetkilendirme kodu akışı. |
| Kod |Gerekli |Merhaba `authorization_code` hello önceki bölümde edindiğiniz |
| redirect_uri |Gerekli |aynı hello `redirect_uri` kullanılan tooacquire hello olan değer `authorization_code`. |
| client_secret |Web uygulamaları için gerekli |Merhaba uygulama kayıt Portalı'nda uygulamanız için oluşturduğunuz hello uygulama gizli anahtarı.  Client_secrets güvenilir bir şekilde cihazlarda depolanamaz çünkü yerel bir uygulamada kullanılmamalıdır.  Web uygulamaları ve web hello özelliği toostore hello sahip API'leri için gerekli olan `client_secret` hello sunucu tarafında güvenli bir şekilde. |
| Kaynak |Yetkilendirme kodu isteğinde başka isteğe bağlı belirttiyseniz gereklidir |Merhaba uygulama kimliği URI'si hello Web API (güvenli kaynak). |

hello Azure Yönetim Portalı toofind hello uygulama kimliği URI'si tıklatın **Active Directory**hello dizin'i tıklatın, hello uygulama'yı tıklatın ve ardından **yapılandırma**.

### Başarılı yanıt
Azure AD, bir erişim belirteci üzerine başarılı bir yanıt döndürür. toominimize ağ çağrıları hello istemci uygulamasından ve bunların ilişkili gecikme süresi, Merhaba istemci uygulaması hello OAuth 2.0 yanıt belirtilen hello belirteç ömrü için erişim belirteçleri önbelleğe. toodetermine hello belirteç ömrü, her iki hello kullan `expires_in` veya `expires_on` parametre değerleri.

Bir web API kaynak döndürürse bir `invalid_token` hata kodu, bu gösterebilir hello kaynak hello belirtecini süresi doldu belirledi. Merhaba istemci ve kaynak saatleri farklı (bir "saat eğriltme" olarak bilinir) varsa, hello kaynak hello belirteci hello istemci önbelleğinden temizlenmeden önce hello belirteci toobe süresi düşünebilirsiniz. Bu gerçekleşirse, hala hesaplanan yaşam süresi içinde olsa bile hello belirteci hello önbelleğinden temizleyin.

Başarılı yanıt şöyle:

```
{
  "access_token": " eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1388444763",
  "resource": "https://service.contoso.com/",
  "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA",
  "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
  "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ."
}

```

| Parametre | Açıklama |
| --- | --- |
| access_token |Merhaba istenen erişim belirteci. Merhaba uygulaması web API'si gibi kaynak güvenli Bu belirteci tooauthenticate toohello kullanabilir. |
| token_type |Merhaba belirteç türü değeri gösterir. Merhaba yalnızca yazın Azure AD desteklediği taşıyıcı biçimde. Taşıyıcı belirteçlerini hakkında daha fazla bilgi için bkz: [OAuth2.0 yetkilendirme Framework: taşıyıcı belirteci kullanımı (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt) |
| expires_in |Ne kadar süreyle hello erişim belirteci (saniye olarak) geçerli değil. |
| expires_on |Merhaba erişim belirtecinin süresi dolduğunda hello süre. Başlangıç tarihi 1970'ten hello saniyeyi temsil edilir-01-01T0:0:0Z UTC hello süre kadar. Önbelleğe alınan belirteçleri kullanılan toodetermine hello ömrü değerdir. |
| Kaynak |Merhaba uygulama kimliği URI'si hello Web API (güvenli kaynak). |
| Kapsam |Kimliğe bürünme, toohello istemci uygulaması izinler. Merhaba varsayılan izni `user_impersonation`. Kaynak güvenli hello Hello sahibi Azure AD içinde ek değerler kaydedebilirsiniz. |
| refresh_token |Bir OAuth 2.0 yenileme belirteci. Merhaba geçerli erişim belirtecinin süresi dolduktan sonra bu belirteci tooacquire ek erişim belirteçleri hello uygulamasını kullanabilir.  Yenileme belirteçlerini uzun süreli ve uzun süre için kullanılan tooretain erişim tooresources olabilir. |
| id_token |Bir imzasız JSON Web Token (JWT). Merhaba uygulama can base64Url açtığınız hello kullanıcının bu belirteci toorequest bilgilerini hello kesimleri kodunu çözer. Hello uygulama hello değerleri önbelleğe ve bunları görüntüler, ancak, bunlar üzerinde herhangi bir yetkilendirme veya güvenlik sınırları için güvenmemelisiniz. |

### JWT belirteci talepleri
Merhaba JWT belirteci hello hello değeri `id_token` parametresi hello talepler aşağıdaki kodu:

```
{
 "typ": "JWT",
 "alg": "none"
}.
{
 "aud": "2d4d11a2-f814-46a7-890a-274a72a7309e",
 "iss": "https://sts.windows.net/7fe81447-da57-4385-becb-6de57f21477e/",
 "iat": 1388440863,
 "nbf": 1388440863,
 "exp": 1388444763,
 "ver": "1.0",
 "tid": "7fe81447-da57-4385-becb-6de57f21477e",
 "oid": "68389ae2-62fa-4b18-91fe-53dd109d74f5",
 "upn": "frank@contoso.com",
 "unique_name": "frank@contoso.com",
 "sub": "JWvYdCWPhhlpS1Zsf7yYUxShUwtUm5yzPmw_-jX3fHY",
 "family_name": "Miller",
 "given_name": "Frank"
}.
```

JSON web belirteçlerini hakkında daha fazla bilgi için bkz: Merhaba [JWT IETF taslak belirtimi](http://go.microsoft.com/fwlink/?LinkId=392344). Merhaba belirteç türleri ve talepler hakkında daha fazla bilgi için okuma [desteklenen belirteç ve talep türleri](active-directory-token-and-claims.md)

Merhaba `id_token` parametresi hello şu talep türlerini içerir:

| Talep türü | Açıklama |
| --- | --- |
| aud |İzleyici hello belirteci. Merhaba belirteci tooa istemci uygulaması verildiğinde hello İzleyici hello olduğu `client_id` hello istemci. |
| exp |Süre sonu zamanı. Merhaba belirtecinin süresi dolduğunda hello süre. Merhaba belirteci toobe için geçerli, hello geçerli tarih/saat değerinden küçük veya buna eşit olmalıdır toohello `exp` değeri. Merhaba saat 1 Ocak 1970'ten hello saniyeyi temsil edilir (1970'ten-01-01T0:0:0Z) hello zaman hello belirteci verilmiş kadar UTC. |
| family_name |Kullanıcının soyadı. Merhaba uygulaması, bu değeri görüntüleyebilirsiniz. |
| given_name |Kullanıcının adı. Merhaba uygulaması, bu değeri görüntüleyebilirsiniz. |
| IAT |Aynı anda verdi. hello zaman zaman hello JWT verilmiş. Merhaba saat 1 Ocak 1970'ten hello saniyeyi temsil edilir (1970'ten-01-01T0:0:0Z) hello zaman hello belirteci verilmiş kadar UTC. |
| ISS |Merhaba Belirteç Verenin tanımlar |
| NBF |Değil süreden önce. Merhaba belirteci etkin olduğunda hello süre. Merhaba belirteci toobe için geçerli, hello geçerli tarih/saat değerinden büyük veya eşit toohello Nbf değeri olmalıdır. Merhaba saat 1 Ocak 1970'ten hello saniyeyi temsil edilir (1970'ten-01-01T0:0:0Z) hello zaman hello belirteci verilmiş kadar UTC. |
| OID |Azure AD'de hello kullanıcı nesnesinin nesne tanımlayıcısını (ID). |
| Sub |Belirteç konu tanımlayıcısı. Belirteç hello hello kullanıcı açıklar için kalıcı ve sabit bir tanımlayıcı budur. Mantığı önbelleğe alma işleminde, bu değeri kullanın. |
| komutu |Merhaba belirteç hello Azure AD Kiracı tanımlayıcısını (ID) Kiracı. |
| unique_name |Görüntülenen toohello kullanıcı için benzersiz bir tanımlayıcıyı olabilir. Genellikle bir kullanıcı asıl adı (UPN) budur. |
| UPN |Merhaba kullanıcının kullanıcı asıl adı. |
| ver |Sürüm. Merhaba JWT belirteci, genellikle 1.0 sürümü Hello. |

### Hata yanıtı
Merhaba istemci çağrılarını belirteci verme uç noktası doğrudan hello çünkü hello belirteci verme uç noktası HTTP hata kodları, hatalardır. Ayrıca toohello HTTP durum kodu hello Azure AD belirteci verme endpoint hello hatasını açıklayan nesneleri ile bir JSON belgesini de döndürür.

Bir örnek hata yanıtı şuna:

```
{
  "error": "invalid_grant",
  "error_description": "AADSTS70002: Error validating credentials. AADSTS70008: hello provided authorization code or refresh token is expired. Send a new interactive authorization request for this user and resource.\r\nTrace ID: 3939d04c-d7ba-42bf-9cb7-1e5854cdce9e\r\nCorrelation ID: a8125194-2dc8-4078-90ba-7b6592a7f231\r\nTimestamp: 2016-04-11 18:00:12Z",
  "error_codes": [
    70002,
    70008
  ],
  "timestamp": "2016-04-11 18:00:12Z",
  "trace_id": "3939d04c-d7ba-42bf-9cb7-1e5854cdce9e",
  "correlation_id": "a8125194-2dc8-4078-90ba-7b6592a7f231"
}
```
| Parametre | Açıklama |
| --- | --- |
| error |Oluşan hataları kullanılan tooclassify türde olabilir ve kullanılan tooreact tooerrors olabilir bir hata kodu dizesi. |
| error_description |Bir geliştirici yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |
| error_codes |Tanılamada yardımcı olabilecek STS özgü hata kodları listesi. |
| timestamp |Merhaba hata gerçekleştiği hello süre. |
| trace_id |Tanılamada yardımcı olabilecek hello isteği için benzersiz bir tanımlayıcı. |
| correlation_id |Tanılama'bileşenlerinde yardımcı olabilecek hello isteği için benzersiz bir tanımlayıcı. |

#### HTTP durum kodları
Merhaba aşağıdaki tabloda belirteci verme uç nokta döndürür hello hello HTTP durum kodları listelenmektedir. Bazı durumlarda, hello hata kodu yeterli toodescribe hello yanıt olmakla birlikte, hatalar varsa, JSON eşlik tooparse hello gereken belge ve hata kodunun inceleyin.

| HTTP kodu | Açıklama |
| --- | --- |
| 400 |Varsayılan HTTP kodu. Çoğu durumda kullanıldığı ve genellikle tooa yanlış biçimli istek. Düzeltin ve hello isteği yeniden gönderin. |
| 401 |Kimlik doğrulaması başarısız oldu. Örneğin, hello isteği hello client_secret parametresi eksik. |
| 403 |Yetkilendirme başarısız oldu. Örneğin, hello kullanıcı izni tooaccess hello kaynak yok. |
| 500 |Merhaba hizmeti bir iç hata oluştu. Merhaba isteği yeniden deneyin. |

#### Belirteç uç noktası hataları için hata kodları
| Hata kodu | Açıklama | İstemci eylemi |
| --- | --- | --- |
| invalid_request |Eksik gerekli parametre gibi protokol hatası. |Düzeltin ve hello isteği yeniden gönderin |
| invalid_grant |Merhaba yetkilendirme kodu geçersiz veya süresi doldu. |Yeni bir istek toohello deneyin `/authorize` uç noktası |
| unauthorized_client |Merhaba kimliği doğrulanmış istemci yetkilendirilmez toouse Bu yetki türü. |Bu durum genellikle, Merhaba istemci uygulaması Azure AD'de kayıtlı değil veya toohello kullanıcının Azure AD kiracısı eklenmez genellikle ortaya çıkar. Merhaba uygulaması hello uygulama yüklemek ve tooAzure AD eklemek için yönerge hello kullanıcıyla isteyebilir. |
| invalid_client |İstemci kimlik doğrulaması başarısız oldu. |Merhaba istemci kimlik bilgileri geçerli değil. toofix, hello Uygulama Yöneticisi hello kimlik bilgilerini güncelleştirir. |
| unsupported_grant_type |Merhaba yetkilendirme sunucusu hello yetkilendirme verme türünü desteklemiyor. |Değişiklik hello hello istek türü verin. Bu tür bir hata yalnızca geliştirme sırasında gerçekleşmesi gerektiğini ve ilk test sırasında algılandı. |
| invalid_resource |Merhaba hedef kaynak mevcut değil, Azure AD, bulunamıyor veya düzgün yapılandırılmamış olduğundan geçerli değil. |Bu, varsa, hello kaynak hello Kiracı yapılandırılmadı gösterir. Merhaba uygulaması hello uygulama yüklemek ve tooAzure AD eklemek için yönerge hello kullanıcıyla isteyebilir. |
| interaction_required |Merhaba isteği kullanıcı etkileşimi gerektirir. Örneğin, bir ek kimlik doğrulama adım gereklidir. | Etkileşimli olmayan bir istek yerine hello etkileşimli yetkilendirme talebi ile aynı yeniden deneme kaynak. |
| temporarily_unavailable |Merhaba geçici olarak meşgul toohandle hello isteği sunucusudur. |Merhaba isteği yeniden deneyin. Merhaba istemci uygulaması toohello kullanıcı açıklayan yanıt tooa geçici koşul ertelendi. |

## Merhaba erişim belirteci tooaccess hello kaynak kullanın
Başarıyla edindiğiniz göre bir `access_token`, hello dahil ederek hello belirteci isteklerini tooWeb API ' larını kullanabilirsiniz `Authorization` üstbilgi. Merhaba [RFC 6750](http://www.rfc-editor.org/rfc/rfc6750.txt) belirtimi nasıl HTTP isteklerini tooaccess toouse taşıyıcı belirteçler korunan kaynakları açıklar.

### Örnek istek
```
GET /data HTTP/1.1
Host: service.contoso.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ
```

### Hata yanıtı
RFC 6750 sorunu HTTP durum kodları uygulamak güvenli kaynaklar. Merhaba isteği kimlik doğrulama kimlik bilgileri içermiyor veya hello belirteç, hello yanıt eksik bulunduran bir `WWW-Authenticate` üstbilgi. Bir isteği başarısız olduğunda, hello kaynak sunucu hello HTTP durum kodu ve bir hata kodu ile yanıt verir.

Merhaba istemci isteği hello taşıyıcı belirteci içermez zaman hello başarısız bir yanıt örneği aşağıdadır:

```
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer authorization_uri="https://login.microsoftonline.com/contoso.com/oauth2/authorize",  error="invalid_token",  error_description="hello access token is missing.",
```

#### Hata parametreleri
| Parametre | Açıklama |
| --- | --- |
| authorization_uri |Merhaba hello yetkilendirme sunucusu URI'si (fiziksel uç noktası). Bu değer hello sunucu bulma uç noktasından hakkında daha fazla bilgi tooget bir arama anahtar olarak da kullanılır. <p><p> Merhaba istemci o hello doğrulamak gerekir yetkilendirme sunucusu güvenilir. Azure AD tarafından korumalı Hello kaynak hello URL https://login.microsoftonline.com ile başlayan yeterli tooverify veya Azure AD destekleyen başka bir ana bilgisayar adı olur. Bir kiracı özgü kaynak her zaman bir kiracı özel yetkilendirme URI döndürmelidir. |
| error |Merhaba, bölüm 5.2 içinde tanımlanmış bir hata kodu değer [OAuth 2.0 yetkilendirme Framework](http://tools.ietf.org/html/rfc6749). |
| error_description |Merhaba hatanın ayrıntılı bir açıklaması. Bu ileti belirtmezseniz toobe son kullanıcı dostu. |
| resource_id |Merhaba kaynak benzersiz tanımlayıcısını döndürür hello. Merhaba istemci uygulaması bu tanımlayıcı hello hello değeri olarak kullanabileceğiniz `resource` hello kaynak için bir belirteç istediğinde parametresi. <p><p> Önemlidir bu değer istemci uygulaması tooverify Merhaba, kötü amaçlı bir hizmete mümkün tooinduce aksi olabilir bir **ayrıcalık yükseltme** saldırısı <p><p> bir saldırı önleme hello tooverify için stratejisi önerilen hello `resource_id` eşleşmeleri erişilen hello web API'si URL tabanı hello. Örneğin, https://service.contoso.com/data erişilen, hello `resource_id` htttps://service.contoso.com/ olabilir. Merhaba istemci uygulaması gerekir Reddet bir `resource_id` , değil başlamak hello temel URL ile güvenilir bir alternatif yolu tooverify hello kimliği değilse. |

#### Taşıyıcı düzeni hata kodları
Merhaba RFC 6750 belirtimi aşağıdaki hatalar hello WWW-Authenticate üstbilgisi ve taşıyıcı düzeni hello yanıt olarak kullanan kaynakları için hello tanımlar.

| HTTP durum kodu | Hata kodu | Açıklama | İstemci eylemi |
| --- | --- | --- | --- |
| 400 |invalid_request |Merhaba isteği düzgün biçimlendirilmemiş. Örneğin, bir parametre eksik olabilir veya kullanarak hello aynı parametre iki kez. |Merhaba hatayı düzeltin ve hello isteği yeniden deneyin. Bu tür bir hata yalnızca geliştirme sırasında gerçekleşmesi gerektiğini ve ilk testinde algılandı. |
| 401 |invalid_token |Merhaba erişim belirteci eksik, geçersiz veya iptal edilir. Merhaba hello error_description parametresinin değerini ek ayrıntılar sağlar. |Yeni bir belirteç hello yetkilendirme sunucusundan isteyin. Merhaba yeni belirteci başarısız olursa, beklenmeyen bir hata oluştu. Bir hata iletisi toohello kullanıcı göndermek ve rastgele gecikme sonra yeniden deneyin. |
| 403 |insufficient_scope |Merhaba erişim belirteci hello kimliğe bürünme izinleri gerekli tooaccess hello kaynak içermiyor. |Yeni bir yetkilendirme isteği toohello yetkilendirme uç noktası gönderin. Merhaba yanıt hello kapsam parametresi içeriyorsa, hello kapsam değeri hello isteği toohello kaynağında kullanın. |
| 403 |insufficient_access |Merhaba konu hello belirtecin gerekli tooaccess hello kaynaktır hello izinleri yok. |Komut istemi hello kullanıcı toouse farklı bir hesap veya toorequest izinleri toohello kaynak belirtildi. |

## Yenileme hello erişim belirteçleri
Erişim belirteçleri, kısa süreli ve kaynaklara erişim toocontinue süresi dolan yenilenmesi gerekir. Merhaba yenileyebilirsiniz `access_token` başka gönderme tarafından `POST` toohello isteği `/token` endpoint ancak bu kez hello sağlama `refresh_token` hello yerine `code`.

Yenileme belirteçleri belirtilen yaşam süresi yok. Genellikle, yenileme belirteçleri hello ömrü oldukça uzun. Ancak, bazı durumlarda, yenileme belirteçleri sona, iptal edilen veya hello istenen eylem için yeterli ayrıcalıkları yok. Uygulamanız doğru hello belirteci verme bitiş noktası tarafından döndürülen tooexpect ve tanıtıcı hataları gerekir.

Bir yenileme belirteci hatası ile bir yanıt aldığınızda, hello geçerli yenileme belirteci atmak ve yeni bir yetkilendirme kodu isteyin veya belirteç erişim. Özellikle, ne zaman bir yenileme kullanarak belirteci hello yetkilendirme kodu verme akış hello yanıtta alırsanız `interaction_required` veya `invalid_grant` hata kodları hello yenileme belirteci atmak ve yeni bir yetkilendirme kodu isteyin.

Örnek istek toohello **Kiracı özgü** uç noktası (Merhaba de kullanabilirsiniz **ortak** uç nokta) tooget bir yenileme belirteci kullanarak yeni bir erişim belirteci şu şekilde görünür:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&grant_type=refresh_token
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

### Başarılı yanıt
Başarılı bir token yanıt gibi görünür:

```
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1460404526",
  "resource": "https://service.contoso.com/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "refresh_token": "AwABAAAAv YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl PM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfmVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA"
}
```
| Parametre | Açıklama |
| --- | --- |
| token_type |Merhaba simge türü. yalnızca desteklenen hello değer **taşıyıcı**. |
| expires_in |Merhaba hello belirteç ömrü saniye kaldı. Tipik bir değer 3600 (bir saat) ' dir. |
| expires_on |Başlangıç tarihi ve saati üretileceği hello belirtecinin süresi doluyor. Başlangıç tarihi 1970'ten hello saniyeyi temsil edilir-01-01T0:0:0Z UTC hello süre kadar. |
| Kaynak |Merhaba tanımlayan kaynak güvenli hello erişim belirtecini kullanılan tooaccess olabilir. |
| Kapsam |Kimliğe bürünme, toohello yerel istemci uygulaması izinler. Merhaba varsayılan izni **user_impersonation**. Merhaba hedef kaynak Hello sahibi alternatif değerler Azure AD'de kaydedebilirsiniz. |
| access_token |İstenen hello yeni bir erişim belirteci. |
| refresh_token |Bu yanıt Hello sona erdiğinde, kullanılan toorequest yeni erişim belirteçleri olabilecek bir yeni OAuth 2.0 refresh_token. |

### Hata yanıtı
Bir örnek hata yanıtı şuna:

```
{
  "error": "invalid_resource",
  "error_description": "AADSTS50001: hello application named https://foo.microsoft.com/mail.read was not found in hello tenant named 295e01fc-0c56-4ac3-ac57-5d0ed568f872.  This can happen if hello application has not been installed by hello administrator of hello tenant or consented tooby any user in hello tenant.  You might have sent your authentication request toohello wrong tenant.\r\nTrace ID: ef1f89f6-a14f-49de-9868-61bd4072f0a9\r\nCorrelation ID: b6908274-2c58-4e91-aea9-1f6b9c99347c\r\nTimestamp: 2016-04-11 18:59:01Z",
  "error_codes": [
    50001
  ],
  "timestamp": "2016-04-11 18:59:01Z",
  "trace_id": "ef1f89f6-a14f-49de-9868-61bd4072f0a9",
  "correlation_id": "b6908274-2c58-4e91-aea9-1f6b9c99347c"
}
```

| Parametre | Açıklama |
| --- | --- |
| error |Oluşan hataları kullanılan tooclassify türde olabilir ve kullanılan tooreact tooerrors olabilir bir hata kodu dizesi. |
| error_description |Bir geliştirici yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |
| error_codes |Tanılamada yardımcı olabilecek STS özgü hata kodları listesi. |
| timestamp |Merhaba hata gerçekleştiği hello süre. |
| trace_id |Tanılamada yardımcı olabilecek hello isteği için benzersiz bir tanımlayıcı. |
| correlation_id |Tanılama'bileşenlerinde yardımcı olabilecek hello isteği için benzersiz bir tanımlayıcı. |

Merhaba hata kodları ve önerilen istemci eylem hello açıklaması için bkz: [belirteç uç noktası hataları için hata kodları](#error-codes-for-token-endpoint-errors).
