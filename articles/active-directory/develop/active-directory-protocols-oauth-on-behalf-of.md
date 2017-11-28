---
title: "OAuth2.0 üzerinde-adına-Of taslak belirtim kullanarak aaaAzure AD hizmeti tooservice auth | Microsoft Docs"
description: "Bu makalede nasıl toouse HTTP iletileri tooimplement tooservice kullanarak hizmet kimlik doğrulaması izin ver hello OAuth2.0 üzerinde-temsili akış açıklanmaktadır."
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 09f6f318-e88b-4024-9ee1-e7f09fb19a82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 55b7fcfe6c0223bddedd8d8fa2defcb5769b43c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# Merhaba üzerinde-temsili akış temsilci atanan kullanıcı kimliğini kullanarak hizmet tooservice çağırır
Merhaba OAuth 2.0 On-Behalf-Of akışı, sırayla toocall gereken bir uygulama hizmeti/web API'si, burada çağırır hello kullanım örneği başka bir hizmet/web API işlevi görür. Merhaba toopropagate hello kullanıcı kimliği ve hello istek zincirinin aracılığıyla izinlere temsilci olur. Merhaba orta katman toomake kimlik doğrulaması istekleri toohello aşağı akış hizmeti için Azure Active Directory (Azure AD), bir erişim belirteci toosecure hello kullanıcı adına gerekir.

## Üzerinde-adına-Akış Diyagramı
Bu hello kullanıcının kimlik doğrulaması hello kullanarak bir uygulama üzerinde varsayın [OAuth 2.0 yetkilendirme kodu izin akışı](active-directory-protocols-oauth-code.md). Bu noktada, Merhaba uygulaması hello kullanıcının talepleri ve onay tooaccess hello orta katman web API (API A) ile bir erişim belirteci (belirteci A) sahiptir. Şimdi, API A toomake kimliği doğrulanmış isteği toohello Aşağı Akış web API'si (API B) gerekir.

izleyin hello adımlar hello üzerinde-temsili akış oluşturur ve hello diyagramı aşağıdaki hello yardımıyla açıklanmıştır.

![OAuth2.0 üzerinde-temsili akış](media/active-directory-protocols-oauth-on-behalf-of/active-directory-protocols-oauth-on-behalf-of-flow.png)


1. İstek tooAPI hello belirteci A. ile Merhaba istemci uygulaması yapar
2. API A toohello Azure AD belirteci verme endpoint kimliğini doğrular ve bir belirteç tooaccess API B'nin istekleri
3. Hello Azure AD belirteci verme endpoint belirteci bir API A'ın kimlik bilgilerini doğrular ve sorunları API B (belirteç B) için erişim belirteci hello.
4. Merhaba belirteci B hello yetkilendirme üstbilgisinde hello isteği tooAPI B. ayarlanır
5. Kaynak güvenli hello verilerden API B'nin tarafından döndürülür

## Merhaba uygulaması ve hizmeti Azure AD'de kaydetme
Merhaba istemci uygulaması hem hello orta katman hizmet Azure AD'de kaydedin.
### Merhaba orta katman hizmet kaydı
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Hesabınızda ve hello altında Hello üst çubuğunda tıklatın **Directory** listesinde, burada istediğiniz tooregister uygulamanızı hello Active Directory Kiracı seçin.
3. Tıklayın **daha Hizmetleri** sol taraftaki gezinti hello ve seçin **Azure Active Directory**.
4. Tıklayın **uygulama kayıtlar** ve **yeni uygulama kaydı**.
5. Merhaba uygulama için kolay bir ad girin ve hello uygulama türünü seçin. Oturum açma kümesi hello URL veya yeniden yönlendirme URL'si toohello temel URL Hello uygulama türüne göre. Tıklayın **oluşturma** toocreate Merhaba uygulaması.
6. Halen hello Azure portal'ın sırasında uygulamanızı seçin ve tıklayın **ayarları**. Merhaba Ayarlar menüsünden seçin **anahtarları** ve bir anahtar add - 1 yıl veya 2 yıl anahtar bir süre seçin. Bu sayfayı kaydedin, hello anahtar değeri görüntülenir, kopyalama ve güvenli bir yerde hello değeri kaydetmek,-uygulamanızda - bu anahtar sonraki tooconfigure hello uygulama ayarları gerekir, bu anahtarı değeri tarafından görüntülenen yeniden ya da alınabilir olmayacaktır. diğer anlamına gelir, bu nedenle kayıt Lütfen onu hello Azure Portalı ' görünür olur olmaz.

### Merhaba istemci uygulaması kaydetme
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Hesabınızda ve hello altında Hello üst çubuğunda tıklatın **Directory** listesinde, burada istediğiniz tooregister uygulamanızı hello Active Directory Kiracı seçin.
3. Tıklayın **daha Hizmetleri** sol taraftaki gezinti hello ve seçin **Azure Active Directory**.
4. Tıklayın **uygulama kayıtlar** ve **yeni uygulama kaydı**.
5. Merhaba uygulama için kolay bir ad girin ve hello uygulama türünü seçin. Oturum açma kümesi hello URL veya yeniden yönlendirme URL'si toohello temel URL Hello uygulama türüne göre. Tıklayın **oluşturma** toocreate Merhaba uygulaması.
6. -Hello ayarları menüsünde uygulamanız için izinlerini yapılandırabilir, hello seçin **gerekli izinleri** bölümünde, tıklayın **Ekle**, ardından **bir API seçin**ve türü hello Merhaba metin kutusuna hello orta katman hizmet adı. Ardından, tıklatın **Select izinleri** seçip ' erişim *hizmet adı*'.

### Bilinen istemci uygulamaları yapılandır
Bu senaryoda, hello orta katman hizmet tooaccess hello aşağı akış API onayı hiçbir kullanıcı etkileşimi tooobtain hello kullanıcının sahiptir. Bu nedenle, aşağı akış API sunulabilir seçeneği toogrant erişim toohello hello ön kimlik doğrulaması sırasında hello izin adım bir parçası olarak.
tooachieve Bu, Azure AD'de hello istemci ve orta katman tarafından tek bir iletişim kutusuna hello gerekmemektedir birleştirir hello orta katman hizmet hello kaydı tooexplicitly bağlama hello istemci uygulamasının kaydı izleyin hello adımları.
1. Toohello orta katman hizmet kayıt gidin ve tıklayın **bildirim** tooopen hello bildirim Düzenleyici.
2. Merhaba bildiriminde hello bulun `knownClientApplications` dizi özelliği ve öğe hello hello istemci uygulamanın istemci Kimliğini ekleyin.
3. Merhaba bildirimi hello Kaydet düğmesine tıklayarak kaydedin.

## Hizmet tooservice erişim belirteci isteği
toorequest bir erişim belirteci bir HTTP POST toohello Kiracı özgü Azure AD uç noktası şu parametreler hello olun.

```
https://login.microsoftonline.com/<tenant>/oauth2/token
```
Merhaba istemci uygulaması toobe güvenli bir paylaşılan gizlilik veya bir sertifika olup olmadığını seçer bağlı olarak iki durumlar vardır.

### İlk durumda: bir paylaşılan gizlilik ile erişim belirteci isteği
Paylaşılan gizlilik kullanırken, hizmetten hizmete erişim belirteci isteği şu parametreler hello içerir:

| Parametre |  | Açıklama |
| --- | --- | --- |
| grant_type |Gerekli | Merhaba belirteç isteği Hello türü. JWT'nin kullanmak için bir istek hello değeri olmalıdır **urn: ietf:params:oauth:grant-türü: jwt-taşıyıcı**. |
| onaylama işlemi |Gerekli | Merhaba istekte kullanılan hello belirteci Hello değeri. |
| client_id |Gerekli | Merhaba uygulama kimliği toohello arama hizmeti Azure AD ile kayıt sırasında atanır. hello Azure Yönetim Portalı toofind hello uygulama kimliği tıklatın **Active Directory**hello dizin'i tıklatın ve hello uygulama adına tıklayın. |
| client_secret |Gerekli | Azure AD'de hizmet çağırma hello için Hello anahtar kaydedildi. Bu değer kayıt hello aynı anda not. |
| Kaynak |Gerekli | Merhaba hizmet (güvenli kaynak) alma hello uygulama kimliği URI'si. toofind hello uygulama kimliği URI'si hello Azure Yönetim Portalı, tıklatın **Active Directory**hello dizin'i tıklatın, hello uygulama adı'ı tıklatın, tıklatın **tüm ayarları** ve ardından **özellikleri** . |
| requested_token_use |Gerekli | Merhaba isteğin nasıl işleneceğini belirtir. Hello üzerinde-temsili akış, hello değeri olmalıdır **on_behalf_of**. |
| Kapsam |Gerekli | Boşlukla ayrılmış hello belirteç isteği kapsamları listesi. Openıd Connect için kapsam hello **openıd** belirtilmesi gerekir.|

#### Örnek
Merhaba aşağıdaki HTTP POST hello https://graph.windows.net web API'si için bir erişim belirteci ister. Merhaba `client_id` hello erişim belirteci istekleri hello hizmeti tanımlar.

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_secret=0Y1W%2BY3yYb3d9N8vSjvm8WrGzVZaAaHbHHcGbcgG%2BoI%3D
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

### İkinci durumda: bir sertifika ile erişim belirteci isteği
Hizmetten hizmete erişim belirteci isteği bir sertifika ile şu parametreler hello içerir:

| Parametre |  | Açıklama |
| --- | --- | --- |
| grant_type |Gerekli | Merhaba belirteç isteği Hello türü. JWT'nin kullanmak için bir istek hello değeri olmalıdır **urn: ietf:params:oauth:grant-türü: jwt-taşıyıcı**. |
| onaylama işlemi |Gerekli | Merhaba istekte kullanılan hello belirteci Hello değeri. |
| client_id |Gerekli | Merhaba uygulama kimliği toohello arama hizmeti Azure AD ile kayıt sırasında atanır. hello Azure Yönetim Portalı toofind hello uygulama kimliği tıklatın **Active Directory**hello dizin'i tıklatın ve hello uygulama adına tıklayın. |
| client_assertion_type |Gerekli |Merhaba değeri olmalıdır`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |Gerekli | Uygulamanız için kimlik bilgileri olarak toocreate gerekir ve hello işaretiyle sertifika onayı ifade (bir JSON Web belirteci) kayıtlı.  Hakkında bilgi edinin [sertifika kimlik bilgileri](active-directory-certificate-credentials.md) toolearn nasıl tooregister hello onaylama, sertifika ve hello biçimi.|
| Kaynak |Gerekli | Merhaba hizmet (güvenli kaynak) alma hello uygulama kimliği URI'si. toofind hello uygulama kimliği URI'si hello Azure Yönetim Portalı, tıklatın **Active Directory**hello dizin'i tıklatın, hello uygulama adı'ı tıklatın, tıklatın **tüm ayarları** ve ardından **özellikleri** . |
| requested_token_use |Gerekli | Merhaba isteğin nasıl işleneceğini belirtir. Hello üzerinde-temsili akış, hello değeri olmalıdır **on_behalf_of**. |
| Kapsam |Gerekli | Boşlukla ayrılmış hello belirteç isteği kapsamları listesi. Openıd Connect için kapsam hello **openıd** belirtilmesi gerekir.|

Neredeyse olarak hello parametreleridir bildirimi hello hello isteği hello durumunda olduğu gibi aynı tarafından paylaşılan gizliliği hello client_secret parametresi tarafından iki parametre değiştirilir dışında: client_assertion_type ve client_assertion.

#### Örnek
HTTP POST aşağıdaki hello hello https://graph.windows.net web API ile bir sertifika için bir erişim belirteci ister. Merhaba `client_id` hello erişim belirteci istekleri hello hizmeti tanımlar.

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer
&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

## Hizmet tooservice erişim belirteci yanıtı
Başarılı yanıt şu parametreler hello JSON OAuth 2.0 yanıtıyla ' dir.

| Parametre | Açıklama |
| --- | --- |
| token_type |Merhaba belirteç türü değeri gösterir. yalnızca Azure AD destekler türü hello **taşıyıcı**. Merhaba taşıyıcı belirteçlerini hakkında daha fazla bilgi için bkz: [OAuth 2.0 yetkilendirme Framework: taşıyıcı belirteci kullanımı (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt). |
| Kapsam |Merhaba belirtecinde verilen erişim kapsamını Hello. |
| expires_in |zaman hello erişim belirteci Hello uzunluğu (saniye olarak) geçerli değil. |
| expires_on |Merhaba erişim belirtecinin süresi dolduğunda hello süre. Başlangıç tarihi 1970'ten hello saniyeyi temsil edilir-01-01T0:0:0Z UTC hello süre kadar. Önbelleğe alınan belirteçleri kullanılan toodetermine hello ömrü değerdir. |
| Kaynak |Merhaba hizmet (güvenli kaynak) alma hello uygulama kimliği URI'si. |
| access_token |Merhaba istenen erişim belirteci. Hizmet çağırma hello Bu belirteci tooauthenticate toohello alıcı hizmetini kullanabilirsiniz. |
| id_token |Merhaba istenen kimliği belirteci. Hizmet çağırma hello bu tooverify hello kullanıcının kimliğini kullanın ve hello kullanıcı bir oturumla başlayın. |
| refresh_token |Merhaba yenileme belirteci hello için erişim belirteci istedi. Hizmet çağırma hello Hello geçerli erişim belirtecinin süresi dolduktan sonra bu belirteci toorequest başka bir erişim belirteci kullanabilirsiniz. |

### Başarılı yanıt örnek
Merhaba aşağıdaki örnek hello https://graph.windows.net web API'si için bir erişim belirteci başarı yanıt tooa talebi gösterir.

```
{
    "token_type":"Bearer",
    "scope":"User.Read",
    "expires_in":"43482",
    "ext_expires_in":"302683",
    "expires_on":"1493466951",
    "not_before":"1493423168",
    "resource":"https://graph.windows.net",
    "access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ",
    "refresh_token":"AQABAAAAAABnfiG-mA6NTae7CdWW7QfdjKGu9-t1scy_TDEmLi4eLQMjJGt_nAoVu6A4oSu1KsRiz8XyQIPKQxSGfbf2FoSK-hm2K8TYzbJuswYusQpJaHUQnSqEvdaCeFuqXHBv84wjFhuanzF9dQZB_Ng5za9xKlUENrNtlq9XuLNVKzxEyeUM7JyxzdY7JiEphWImwgOYf6II316d0Z6-H3oYsFezf4Xsjz-MOBYEov0P64UaB5nJMvDyApV-NWpgklLASfNoSPGb67Bc02aFRZrm4kLk-xTl6eKE6hSo0XU2z2t70stFJDxvNQobnvNHrAmBaHWPAcC3FGwFnBOojpZB2tzG1gLEbmdROVDp8kHEYAwnRK947Py12fJNKExUdN0njmXrKxNZ_fEM33LHW1Tf4kMX_GvNmbWHtBnIyG0w5emb-b54ef5AwV5_tGUeivTCCysgucEc-S7G8Cz0xNJ_BOiM_4bAv9iFmrm9STkltpz0-Tftg8WKmaJiC0xXj6uTf4ZkX79mJJIuuM7XP4ARIcLpkktyg2Iym9jcZqymRkGH2Rm9sxBwC4eeZXM7M5a7TJ-5CqOdfuE3sBPq40RdEWMFLcrAzFvP0VDR8NKHIrPR1AcUruat9DETmTNJukdlJN3O41nWdZOVoJM-uKN3uz2wQ2Ld1z0Mb9_6YfMox9KTJNzRzcL52r4V_y3kB6ekaOZ9wQ3HxGBQ4zFt-2U0mSszIAA",
    "id_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8yNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IvIiwiaWF0IjoxNDkzNDIzMTY4LCJuYmYiOjE0OTM0MjMxNjgsImV4cCI6MTQ5MzQ2Njk1MSwiYW1yIjpbInB3ZCJdLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXRpIjoieEN3ZnpoYS1QMFdKUU9MeENHZ0tBQSIsInZlciI6IjEuMCJ9."
}
```

### Hata yanıtı örneği
Bir koşullu erişim ilkesi ayarlayabilirsiniz çok faktörlü kimlik doğrulaması gibi Hello aşağı akış API varsa, Azure AD belirteç uç noktası tarafından tooacquire bir erişim belirteci hello aşağı akış API çalışırken bir hata yanıtı döndürülür. Böylece Merhaba istemci uygulaması hello kullanıcı etkileşimi toosatisfy hello koşullu erişim ilkesi sağlayabilir hello orta katman hizmet bu hata toohello istemci uygulaması yüzey.

```
{
    "error":"interaction_required",
    "error_description":"AADSTS50079: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must enroll in multi-factor authentication tooaccess 'bf8d80f9-9098-4972-b203-500f535113b1'.\r\nTrace ID: b72a68c3-0926-4b8e-bc35-3150069c2800\r\nCorrelation ID: 73d656cf-54b1-4eb2-b429-26d8165a52d7\r\nTimestamp: 2017-05-01 22:43:20Z",
    "error_codes":[50079],
    "timestamp":"2017-05-01 22:43:20Z",
    "trace_id":"b72a68c3-0926-4b8e-bc35-3150069c2800",
    "correlation_id":"73d656cf-54b1-4eb2-b429-26d8165a52d7",
    "claims":"{\"access_token\":{\"polids\":{\"essential\":true,\"values\":[\"9ab03e19-ed42-4168-b6b7-7001fb3e933a\"]}}}"
}
```

## Kaynak güvenli hello erişim belirteci tooaccess hello kullanın
Merhaba belirteçte ayarı hello tarafından web API'si, artık Hello orta katman hizmet aşağı hello kimlik doğrulaması belirteci yukarıda alınan toomake istekleri toohello kullanarak `Authorization` üstbilgi.

### Örnek
```
GET /me?api-version=2013-11-08 HTTP/1.1
Host: graph.windows.net
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ
```

## Sonraki adımlar
Merhaba OAuth 2.0 protokolü ve istemci kimlik bilgilerini kullanarak başka bir şekilde tooperform hizmet tooservice kimlik doğrulama hakkında daha fazla bilgi edinin.
* [Hizmet tooservice auth OAuth 2.0 istemci kimlik bilgileri sağlama Azure AD'de kullanma](active-directory-protocols-oauth-service-to-service.md)
* [Azure AD'de OAuth 2.0](active-directory-protocols-oauth-code.md)
