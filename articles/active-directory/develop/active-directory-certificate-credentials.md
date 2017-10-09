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
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="88537-103">Uygulama kimlik doğrulaması için sertifika kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="88537-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="88537-104">Azure Active Directory Uygulama toouse kendi kimlik bilgilerini kimlik doğrulaması, örneğin, hello OAuth 2.0 istemci kimlik bilgilerini verme akış ve hello üzerinde-temsili akış sağlar.</span><span class="sxs-lookup"><span data-stu-id="88537-104">Azure Active Directory allows an application toouse its own credentials for authentication, for example, in hello OAuth 2.0 Client Credentials Grant flow and hello On-Behalf-Of flow.</span></span>
<span data-ttu-id="88537-105">Bir kullanılabilir kimlik bilgisi Merhaba uygulaması sahip bir sertifika ile imzalanmış bir JSON Web Token(JWT) onaylama biçimidir.</span><span class="sxs-lookup"><span data-stu-id="88537-105">One form of credential that can be used is a JSON Web Token(JWT) assertion signed with a certificate that hello application owns.</span></span>

## <a name="format-of-hello-assertion"></a><span data-ttu-id="88537-106">Merhaba onaylama biçimi</span><span class="sxs-lookup"><span data-stu-id="88537-106">Format of hello assertion</span></span>
<span data-ttu-id="88537-107">toocompute hello onaylama, büyük olasılıkla istediğiniz toouse hello biri birçok [JSON Web belirteci](https://jwt.io/) hello dili kitaplıklarında.</span><span class="sxs-lookup"><span data-stu-id="88537-107">toocompute hello assertion, you probably want toouse one of hello many [JSON Web Token](https://jwt.io/) libraries in hello language of your choice.</span></span> <span data-ttu-id="88537-108">Merhaba belirteci tarafından taşınan hello bilgiler verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="88537-108">hello information carried by hello token is:</span></span>

#### <a name="header"></a><span data-ttu-id="88537-109">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="88537-109">Header</span></span>

| <span data-ttu-id="88537-110">Parametre</span><span class="sxs-lookup"><span data-stu-id="88537-110">Parameter</span></span> |  <span data-ttu-id="88537-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="88537-111">Remark</span></span> |
| --- | --- | --- |
| `alg` | <span data-ttu-id="88537-112">Olmalıdır **RS256**</span><span class="sxs-lookup"><span data-stu-id="88537-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="88537-113">Olmalıdır **JWT**</span><span class="sxs-lookup"><span data-stu-id="88537-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="88537-114">Merhaba X.509 Sertifika SHA-1 parmak izi olmalıdır</span><span class="sxs-lookup"><span data-stu-id="88537-114">Should be hello X.509 Certificate SHA-1 thumbprint</span></span> |

#### <a name="claims-payload"></a><span data-ttu-id="88537-115">Talep (yükü)</span><span class="sxs-lookup"><span data-stu-id="88537-115">Claims (Payload)</span></span>

| <span data-ttu-id="88537-116">Parametre</span><span class="sxs-lookup"><span data-stu-id="88537-116">Parameter</span></span> |  <span data-ttu-id="88537-117">Açıklama</span><span class="sxs-lookup"><span data-stu-id="88537-117">Remark</span></span> |
| --- | --- | --- |
| `aud` | <span data-ttu-id="88537-118">İzleyici: olmalıdır  **https://login.microsoftonline.com/*tenant_Id*  /oauth2/token **</span><span class="sxs-lookup"><span data-stu-id="88537-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="88537-119">Sona erme tarihi: hello belirtecinin süresi dolduğunda başlangıç tarihi.</span><span class="sxs-lookup"><span data-stu-id="88537-119">Expiration date: hello date when hello token expires.</span></span> <span data-ttu-id="88537-120">Merhaba saat 1 Ocak 1970'ten hello saniyeyi temsil edilir (1970'ten-01-01T0:0:0Z) hello zaman hello belirteci geçerlilik süresi doluncaya kadar UTC.</span><span class="sxs-lookup"><span data-stu-id="88537-120">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token validity expires.</span></span>|
| `iss` | <span data-ttu-id="88537-121">Sertifikayı veren: Merhaba client_id (Merhaba istemci hizmeti uygulama kimliği) olması gerekir</span><span class="sxs-lookup"><span data-stu-id="88537-121">Issuer: should be hello client_id (Application Id of hello client service)</span></span> |
| `jti` | <span data-ttu-id="88537-122">GUID: Merhaba JWT kimliği</span><span class="sxs-lookup"><span data-stu-id="88537-122">GUID: hello JWT ID</span></span> |
| `nbf` | <span data-ttu-id="88537-123">Önce değil: tarih hello önce hangi hello belirteç kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="88537-123">Not Before: hello date before which hello token cannot be used.</span></span> <span data-ttu-id="88537-124">Merhaba saat 1 Ocak 1970'ten hello saniyeyi temsil edilir (1970'ten-01-01T0:0:0Z) hello zaman hello belirteci verilmiş kadar UTC.</span><span class="sxs-lookup"><span data-stu-id="88537-124">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token was issued.</span></span> |
| `sub` | <span data-ttu-id="88537-125">Konu: olarak için `iss`, hello client_id (Merhaba istemci hizmeti uygulama kimliği) olması gerekir</span><span class="sxs-lookup"><span data-stu-id="88537-125">Subject: As for `iss`, should be hello client_id (Application Id of hello client service)</span></span> |

#### <a name="signature"></a><span data-ttu-id="88537-126">İmza</span><span class="sxs-lookup"><span data-stu-id="88537-126">Signature</span></span>
<span data-ttu-id="88537-127">Merhaba imzası hesaplanan hello açıklandığı gibi hello sertifika uygulama [JSON Web belirteci RFC7519 belirtimi](https://tools.ietf.org/html/rfc7519)</span><span class="sxs-lookup"><span data-stu-id="88537-127">hello signature is computed applying hello certificate as described in hello [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

### <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="88537-128">Kodu çözülmüş JWT onaylama örneği</span><span class="sxs-lookup"><span data-stu-id="88537-128">Example of a decoded JWT assertion</span></span>
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

### <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="88537-129">Kodlanmış bir JWT onaylama örneği</span><span class="sxs-lookup"><span data-stu-id="88537-129">Example of an encoded JWT assertion</span></span>
<span data-ttu-id="88537-130">dize aşağıdaki hello kodlanmış onaylama örneğidir.</span><span class="sxs-lookup"><span data-stu-id="88537-130">hello following string is an example of encoded assertion.</span></span> <span data-ttu-id="88537-131">Dikkatle bakarsanız, nokta (.) ile ayrılmış üç bölüm görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="88537-131">If you look carefully, you notice three sections separated by dots (.).</span></span>
<span data-ttu-id="88537-132">Hello ilk bölümü hello başlığı, hello ikinci hello yükü kodlar ve hello son hello imza hello ilk iki bölüm hello içerikten hello sertifikalarla hesaplanan değil.</span><span class="sxs-lookup"><span data-stu-id="88537-132">hello first section encodes hello header, hello second hello payload, and hello last is hello signature computed with hello certificates from hello content of hello first two sections.</span></span>
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="88537-133">Azure AD ile sertifikanızı kaydedin</span><span class="sxs-lookup"><span data-stu-id="88537-133">Register your certificate with Azure AD</span></span>
<span data-ttu-id="88537-134">Azure AD'de Merhaba istemci uygulaması olan tooassociate hello sertifika kimlik, tooedit hello uygulama bildirimi gerekir.</span><span class="sxs-lookup"><span data-stu-id="88537-134">tooassociate hello certificate credential with hello client application in Azure AD, you need tooedit hello application manifest.</span></span>
<span data-ttu-id="88537-135">Bir sertifikanın tutma sahip, toocompute gerekir:</span><span class="sxs-lookup"><span data-stu-id="88537-135">Having hold of a certificate, you need toocompute:</span></span>
- <span data-ttu-id="88537-136">`$base64Thumbprint`, hangi olduğu hello hello sertifikası karma base64 kodlaması</span><span class="sxs-lookup"><span data-stu-id="88537-136">`$base64Thumbprint`, which is hello base64 encoding of hello certificate Hash</span></span>
- <span data-ttu-id="88537-137">`$base64Value`, hangi olduğu hello hello sertifika ham verileri base64 kodlaması</span><span class="sxs-lookup"><span data-stu-id="88537-137">`$base64Value`, which is hello base64 encoding of hello certificate raw data</span></span>

<span data-ttu-id="88537-138">Ayrıca tooprovide bir GUID tooidentify hello anahtar hello uygulama bildiriminde gerekir (`$keyId`)</span><span class="sxs-lookup"><span data-stu-id="88537-138">you also need tooprovide a GUID tooidentify hello key in hello application manifest (`$keyId`)</span></span>

<span data-ttu-id="88537-139">Hello Azure uygulaması kaydı Merhaba istemci uygulaması için hello uygulama bildirimini açın ve hello yerine *keyCredentials* şema aşağıdaki hello kullanarak yeni sertifika bilgisi özelliğiyle:</span><span class="sxs-lookup"><span data-stu-id="88537-139">In hello Azure app registration for hello client application, open hello application manifest, and replace hello *keyCredentials* property with your new certificate information using hello following schema:</span></span>
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

<span data-ttu-id="88537-140">Merhaba düzenlemeleri toohello uygulama bildirimini kaydedin ve tooAzure AD yükleyin.</span><span class="sxs-lookup"><span data-stu-id="88537-140">Save hello edits toohello application manifest, and upload tooAzure AD.</span></span> <span data-ttu-id="88537-141">Merhaba keyCredentials özelliği birden çok değerli olduğundan daha zengin anahtar yönetimi için birden çok sertifika karşıya.</span><span class="sxs-lookup"><span data-stu-id="88537-141">hello keyCredentials property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
