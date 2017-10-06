---
title: aaaAzure AD hizmeti tooService Auth OAuth2.0 kullanarak | Microsoft Docs
description: "Bu makalede nasıl toouse HTTP iletileri tooimplement hizmet hello OAuth2.0 istemci kimlik bilgileri verin akışı kullanarak tooservice kimlik doğrulaması açıklanmaktadır."
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: a7f939d9-532d-4b6d-b6d3-95520207965d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: f4bfd4ea8a7de1929c7dcf7ad65a156edff74f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# İstemci kimlik bilgilerini (paylaşılan gizliliği veya sertifika) kullanarak hizmet tooservice çağrıları
Merhaba OAuth 2.0 istemci kimlik bilgileri verin akış izin veren bir web hizmeti (*gizli istemci*) toouse başka çağrılırken tooauthenticate bir kullanıcının kimliğine bürünmek yerine kendi kimlik bilgilerini web hizmeti. Bu senaryoda, hello genellikle bir orta katman web hizmeti, arka plan programı hizmeti veya web sitesi istemcidir. Daha yüksek bir güvence düzeyi için Azure AD (yerine bir paylaşılan gizlilik) bir sertifika bir kimlik bilgisi olarak hizmet toouse çağırma hello de sağlar.

## Akış Diyagramı istemci kimlik bilgileri verin
Merhaba Aşağıdaki diyagramda nasıl akış works Azure Active Directory'de (Azure AD) hello istemci kimlik bilgileri verin açıklanmaktadır.

![OAuth2.0 istemci kimlik bilgileri verin akışı](media/active-directory-protocols-oauth-service-to-service/active-directory-protocols-oauth-client-credentials-grant-flow.jpg)

1. Merhaba istemci uygulaması toohello Azure AD belirteci verme endpoint kimliğini doğrular ve bir erişim belirteci ister.
2. Hello Azure AD belirteci verme bitiş noktası sorunları hello erişim belirteci.
3. Merhaba erişim belirteci kaynak güvenli kullanılan tooauthenticate toohello ' dir.
4. Kaynak güvenli hello verilerden toohello web uygulaması döndürülür.

## Azure AD'de Hello Hizmetleri Kaydet
Hizmet çağırma hello ve Azure Active Directory (Azure AD) hizmeti alma hello kaydedin. Ayrıntılı yönergeler için bkz: [uygulamaları Azure Active Directory ile tümleştirme](active-directory-integrating-applications.md).

## İstek bir erişim belirteci
toorequest bir erişim belirteci bir HTTP POST toohello Kiracı özgü Azure AD uç nokta kullanın.

```
https://login.microsoftonline.com/<tenant id>/oauth2/token
```

## Hizmetten hizmete erişim belirteci isteği
Merhaba istemci uygulaması toobe güvenli bir paylaşılan gizlilik veya bir sertifika olup olmadığını seçer bağlı olarak iki durumlar vardır.

### İlk durumda: bir paylaşılan gizlilik ile erişim belirteci isteği
Paylaşılan gizlilik kullanırken, hizmetten hizmete erişim belirteci isteği şu parametreler hello içerir:

| Parametre |  | Açıklama |
| --- | --- | --- |
| grant_type |Gerekli |İstenen hello belirtir türü verin. Bir istemci kimlik bilgileri sağlama akışında hello değeri olmalıdır **client_credentials**. |
| client_id |Gerekli |Web hizmeti çağırma hello Hello Azure AD istemci kimliğini belirtir. uygulamanın istemci kimliği, hello çağrılırken toofind hello [Azure portal](https://portal.azure.com), tıklatın **Active Directory**, anahtar dizini, hello uygulama'yı tıklatın. Merhaba client_id olan hello *uygulama kimliği* |
| client_secret |Gerekli |Web hizmeti veya arka plan programı uygulaması Azure AD'de çağırma hello için kayıtlı bir anahtar girin. toocreate bir anahtarında hello Azure portal'ı tıklatın **Active Directory**, dizin anahtarı, hello uygulama'yı tıklatın, tıklatın **ayarları**, tıklatın **anahtarları**, ve bir anahtar ekleyin.|
| Kaynak |Gerekli |Merhaba web hizmeti alma hello uygulama kimliği URI'sini girin. toofind hello uygulama kimliği URI'si hello Azure portal'ı tıklatın **Active Directory**anahtar dizini, hello hizmet uygulaması'nı tıklatın ve ardından **ayarları** ve **özellikleri** |

#### Örnek
Merhaba aşağıdaki HTTP POST hello https://service.contoso.com/ web hizmeti için bir erişim belirteci ister. Merhaba `client_id` hello erişim belirteci istekleri hello web hizmeti tanımlar.

```
POST /contoso.com/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&client_id=625bc9f6-3bf6-4b6d-94ba-e97cf07a22de&client_secret=qkDwDJlDfig2IpeuUZYKH1Wb8q1V0ju6sILxQQqhJ+s=&resource=https%3A%2F%2Fservice.contoso.com%2F
```

### İkinci durumda: bir sertifika ile erişim belirteci isteği
Hizmetten hizmete erişim belirteci isteği bir sertifika ile şu parametreler hello içerir:

| Parametre |  | Açıklama |
| --- | --- | --- |
| grant_type |Gerekli |Belirtir hello istenen yanıt türü. Bir istemci kimlik bilgileri sağlama akışında hello değeri olmalıdır **client_credentials**. |
| client_id |Gerekli |Web hizmeti çağırma hello Hello Azure AD istemci kimliğini belirtir. uygulamanın istemci kimliği, hello çağrılırken toofind hello [Azure portal](https://portal.azure.com), tıklatın **Active Directory**, anahtar dizini, hello uygulama'yı tıklatın. Merhaba client_id olan hello *uygulama kimliği* |
| client_assertion_type |Gerekli |Merhaba değeri olmalıdır`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |Gerekli | Uygulamanız için kimlik bilgileri olarak toocreate gerekir ve hello işaretiyle sertifika onayı ifade (bir JSON Web belirteci) kayıtlı. Hakkında bilgi edinin [sertifika kimlik bilgileri](active-directory-certificate-credentials.md) toolearn nasıl tooregister hello onaylama, sertifika ve hello biçimi.|
| Kaynak | Gerekli |Merhaba web hizmeti alma hello uygulama kimliği URI'sini girin. toofind hello uygulama kimliği URI'si hello Azure portal'ı tıklatın **Active Directory**hello dizin'i tıklatın, hello uygulama'yı tıklatın ve ardından **yapılandırma**. |

Neredeyse olarak hello parametreleridir bildirimi hello hello isteği hello durumunda olduğu gibi aynı tarafından paylaşılan gizliliği hello client_secret parametresi tarafından iki parametre değiştirilir dışında: client_assertion_type ve client_assertion.

#### Örnek
HTTP POST aşağıdaki hello bir sertifika ile Merhaba https://service.contoso.com/ web hizmeti için bir erişim belirteci ister. Merhaba `client_id` hello erişim belirteci istekleri hello web hizmeti tanımlar.

```
POST /<tenant_id>/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

resource=https%3A%2F%contoso.onmicrosoft.com%2Ffc7664b4-cdd6-43e1-9365-c2e1c4e1b3bf&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

### Hizmetten hizmete erişim belirteci yanıtı

Başarılı yanıt JSON OAuth 2.0 yanıt şu parametreler hello ile içerir:

| Parametre | Açıklama |
| --- | --- |
| access_token |Merhaba istenen erişim belirteci. Web hizmeti çağırma hello web hizmeti alma Bu belirteci tooauthenticate toohello kullanabilirsiniz. |
| token_type |Merhaba belirteç türü değeri gösterir. yalnızca Azure AD destekler türü hello **taşıyıcı**. Merhaba taşıyıcı belirteçlerini hakkında daha fazla bilgi için bkz: [OAuth 2.0 yetkilendirme Framework: taşıyıcı belirteci kullanımı (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt). |
| expires_in |Ne kadar süreyle hello erişim belirteci (saniye olarak) geçerli değil. |
| expires_on |Merhaba erişim belirtecinin süresi dolduğunda hello süre. Başlangıç tarihi 1970'ten hello saniyeyi temsil edilir-01-01T0:0:0Z UTC hello süre kadar. Önbelleğe alınan belirteçleri kullanılan toodetermine hello ömrü değerdir. |
| not_before |Merhaba zaman hangi hello erişim belirteci kullanılabilir duruma gelir. Başlangıç tarihi 1970'ten hello saniyeyi temsil edilir-01-01T0:0:0Z UTC geçerlilik süresini hello belirteci için kadar.|
| Kaynak |Merhaba web hizmeti alma hello uygulama kimliği URI'si. |

#### Yanıt örneği
Merhaba aşağıdaki örnek bir erişim belirteci tooa web hizmeti için bir başarı yanıt tooa istek gösterir.

```
{
"access_token":"eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0ODI2NywibmJmIjoxMzg4NDQ4MjY3LCJleHAiOjEzODg0NTIxNjcsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsInN1YiI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZS8iLCJhcHBpZCI6ImQxN2QxNWJjLWM1NzYtNDFlNS05MjdmLWRiNWYzMGRkNThmMSIsImFwcGlkYWNyIjoiMSJ9.aqtfJ7G37CpKV901Vm9sGiQhde0WMg6luYJR4wuNR2ffaQsVPPpKirM5rbc6o5CmW1OtmaAIdwDcL6i9ZT9ooIIicSRrjCYMYWHX08ip-tj-uWUihGztI02xKdWiycItpWiHxapQm0a8Ti1CWRjJghORC1B1-fah_yWx6Cjuf4QE8xJcu-ZHX0pVZNPX22PHYV5Km-vPTq2HtIqdboKyZy3Y4y3geOrRIFElZYoqjqSv5q9Jgtj5ERsNQIjefpyxW3EwPtFqMcDm4ebiAEpoEWRN4QYOMxnC9OUBeG9oLA0lTfmhgHLAtvJogJcYFzwngTsVo6HznsvPWy7UP3MINA",
"token_type":"Bearer",
"expires_in":"3599",
"expires_on":"1388452167",
"resource":"https://service.contoso.com/"
}
```

## Ayrıca bkz.
* [Azure AD'de OAuth 2.0](active-directory-protocols-oauth-code.md)
* [Örnek C# hello hizmet tooservice çağrısı bir paylaşılan gizlilik ile](https://github.com/Azure-Samples/active-directory-dotnet-daemon) ve [örnek C# hello hizmet tooservice çağrısı bir sertifika ile](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential)
