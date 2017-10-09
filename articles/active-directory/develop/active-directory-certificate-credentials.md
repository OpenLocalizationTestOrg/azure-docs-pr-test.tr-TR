---
title: Azure AD kimlik bilgilerini aaaCertificate | Microsoft Docs
description: "Bu makalede hello kayıt ve uygulama kimlik doğrulaması için sertifika kimlik bilgileri kullanımını açıklanır"
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 88f0c64a-25f7-4974-aca2-2acadc9acbd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 3508803112ac06268d553db86ab74812aa53e455
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-credentials-for-application-authentication"></a>Uygulama kimlik doğrulaması için sertifika kimlik bilgileri

Azure Active Directory Uygulama toouse kendi kimlik bilgilerini kimlik doğrulaması, örneğin, hello OAuth 2.0 istemci kimlik bilgilerini verme akış ve hello üzerinde-temsili akış sağlar.
Bir kullanılabilir kimlik bilgisi Merhaba uygulaması sahip bir sertifika ile imzalanmış bir JSON Web Token(JWT) onaylama biçimidir.

## <a name="format-of-hello-assertion"></a>Merhaba onaylama biçimi
toocompute hello onaylama, büyük olasılıkla istediğiniz toouse hello biri birçok [JSON Web belirteci](https://jwt.io/) hello dili kitaplıklarında. Merhaba belirteci tarafından taşınan hello bilgiler verilmiştir:

#### <a name="header"></a>Üstbilgi

| Parametre |  Açıklama |
| --- | --- | --- |
| `alg` | Olmalıdır **RS256** |
| `typ` | Olmalıdır **JWT** |
| `x5t` | Merhaba X.509 Sertifika SHA-1 parmak izi olmalıdır |

#### <a name="claims-payload"></a>Talep (yükü)

| Parametre |  Açıklama |
| --- | --- | --- |
| `aud` | İzleyici: olmalıdır  **https://login.microsoftonline.com/*tenant_Id*  /oauth2/token ** |
| `exp` | Sona erme tarihi: hello belirtecinin süresi dolduğunda başlangıç tarihi. Merhaba saat 1 Ocak 1970'ten hello saniyeyi temsil edilir (1970'ten-01-01T0:0:0Z) hello zaman hello belirteci geçerlilik süresi doluncaya kadar UTC.|
| `iss` | Sertifikayı veren: Merhaba client_id (Merhaba istemci hizmeti uygulama kimliği) olması gerekir |
| `jti` | GUID: Merhaba JWT kimliği |
| `nbf` | Önce değil: tarih hello önce hangi hello belirteç kullanılamaz. Merhaba saat 1 Ocak 1970'ten hello saniyeyi temsil edilir (1970'ten-01-01T0:0:0Z) hello zaman hello belirteci verilmiş kadar UTC. |
| `sub` | Konu: olarak için `iss`, hello client_id (Merhaba istemci hizmeti uygulama kimliği) olması gerekir |

#### <a name="signature"></a>İmza
Merhaba imzası hesaplanan hello açıklandığı gibi hello sertifika uygulama [JSON Web belirteci RFC7519 belirtimi](https://tools.ietf.org/html/rfc7519)

### <a name="example-of-a-decoded-jwt-assertion"></a>Kodu çözülmüş JWT onaylama örneği
```
{
  "alg": "RS256",
  "typ": "JWT",
  "x5t": "gx8tGysyjcRqKjFPnd7RFwvwZI0"
}
.
{
  "aud": "https: //login.microsoftonline.com/contoso.onmicrosoft.com/oauth2/token",
  "exp": 1484593341,
  "iss": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05",
  "jti": "22b3bb26-e046-42df-9c96-65dbd72c1c81",
  "nbf": 1484592741,  
  "sub": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05"
}
.
"Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"

```

### <a name="example-of-an-encoded-jwt-assertion"></a>Kodlanmış bir JWT onaylama örneği
dize aşağıdaki hello kodlanmış onaylama örneğidir. Dikkatle bakarsanız, nokta (.) ile ayrılmış üç bölüm görürsünüz.
Hello ilk bölümü hello başlığı, hello ikinci hello yükü kodlar ve hello son hello imza hello ilk iki bölüm hello içerikten hello sertifikalarla hesaplanan değil.
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a>Azure AD ile sertifikanızı kaydedin
Azure AD'de Merhaba istemci uygulaması olan tooassociate hello sertifika kimlik, tooedit hello uygulama bildirimi gerekir.
Bir sertifikanın tutma sahip, toocompute gerekir:
- `$base64Thumbprint`, hangi olduğu hello hello sertifikası karma base64 kodlaması
- `$base64Value`, hangi olduğu hello hello sertifika ham verileri base64 kodlaması

Ayrıca tooprovide bir GUID tooidentify hello anahtar hello uygulama bildiriminde gerekir (`$keyId`)

Hello Azure uygulaması kaydı Merhaba istemci uygulaması için hello uygulama bildirimini açın ve hello yerine *keyCredentials* şema aşağıdaki hello kullanarak yeni sertifika bilgisi özelliğiyle:
```
"keyCredentials": [
    {
        "customKeyIdentifier": "$base64Thumbprint",
        "keyId": "$keyid",
        "type": "AsymmetricX509Cert",
        "usage": "Verify",
        "value":  "$base64Value"
    }
]
```

Merhaba düzenlemeleri toohello uygulama bildirimini kaydedin ve tooAzure AD yükleyin. Merhaba keyCredentials özelliği birden çok değerli olduğundan daha zengin anahtar yönetimi için birden çok sertifika karşıya.
