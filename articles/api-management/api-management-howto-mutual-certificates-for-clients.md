---
title: "aaaSecure API'leri API Management - Azure API Management istemci sertifikası kimlik doğrulaması kullanarak | Microsoft Docs"
description: "Nasıl toosecure erişim istemci sertifikalarını kullanan tooAPIs öğrenin"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: apimpm
ms.openlocfilehash: 6ff78bda3d429829da79d0dc4d652f19669cc919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-apis-using-client-certificate-authentication-in-api-management"></a><span data-ttu-id="b057b-103">Toosecure API'lerini kullanan istemci kimlik doğrulama sertifikasını API Yönetimi</span><span class="sxs-lookup"><span data-stu-id="b057b-103">How toosecure APIs using client certificate authentication in API Management</span></span>

<span data-ttu-id="b057b-104">API Management sağlar hello yetenek toosecure erişim tooAPIs (yani, istemci tooAPI yönetim) istemci sertifikalarını kullanan.</span><span class="sxs-lookup"><span data-stu-id="b057b-104">API Management provides hello capability toosecure access tooAPIs (i.e., client tooAPI Management) using client certificates.</span></span> <span data-ttu-id="b057b-105">Şu anda hello bir sertifikanın parmak izini istemci istenen değerle kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b057b-105">Currently, you can check hello thumbprint of a client certificate against a desired value.</span></span> <span data-ttu-id="b057b-106">Ayrıca, tooAPI yönetim hello parmak izi varolan sertifikalara karşı karşıya kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b057b-106">You can also check hello thumbprint against existing certificates uploaded tooAPI Management.</span></span>  

<span data-ttu-id="b057b-107">Erişim toohello arka uç hizmeti istemci sertifikalarını (yani, API Management tooback uç) kullanan bir API güvenliğini sağlama hakkında daha fazla bilgi için bkz: [nasıl toosecure arka uç hizmetlerini kullanan istemci kimlik doğrulama sertifikası](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span><span class="sxs-lookup"><span data-stu-id="b057b-107">For information about securing access toohello back-end service of an API using client certificates (i.e., API Management tooback-end), see [How toosecure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span></span>

## <a name="checking-hello-expiration-date"></a><span data-ttu-id="b057b-108">Merhaba sona erme tarihi denetleniyor</span><span class="sxs-lookup"><span data-stu-id="b057b-108">Checking hello expiration date</span></span>

<span data-ttu-id="b057b-109">İlkeleri Hello sertifikanın süresi dolmuş yapılandırılmış toocheck olabilir:</span><span class="sxs-lookup"><span data-stu-id="b057b-109">Below policies can be configured toocheck if hello certificate is expired:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-issuer-and-subject"></a><span data-ttu-id="b057b-110">Merhaba veren ve konu denetleniyor</span><span class="sxs-lookup"><span data-stu-id="b057b-110">Checking hello issuer and subject</span></span>

<span data-ttu-id="b057b-111">İlkeler yapılandırılmış toocheck hello veren ve bir istemci sertifikasının konu olabilir:</span><span class="sxs-lookup"><span data-stu-id="b057b-111">Below policies can be configured toocheck hello issuer and subject of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-thumbprint"></a><span data-ttu-id="b057b-112">Merhaba parmak izi denetleniyor</span><span class="sxs-lookup"><span data-stu-id="b057b-112">Checking hello thumbprint</span></span>

<span data-ttu-id="b057b-113">İlkeler yapılandırılmış toocheck hello bir sertifikanın parmak izini istemci olabilir:</span><span class="sxs-lookup"><span data-stu-id="b057b-113">Below policies can be configured toocheck hello thumbprint of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-tooapi-management"></a><span data-ttu-id="b057b-114">TooAPI yönetim karşıya bir parmak izi sertifikalara karşı denetleniyor</span><span class="sxs-lookup"><span data-stu-id="b057b-114">Checking a thumbprint against certificates uploaded tooAPI Management</span></span>

<span data-ttu-id="b057b-115">Merhaba aşağıdaki örnekte nasıl tooAPI yönetim toocheck hello bir sertifikanın parmak izini istemci sertifikalara karşı karşıya gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="b057b-115">hello following example shows how toocheck hello thumbprint of a client certificate against certificates uploaded tooAPI Management:</span></span> 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a><span data-ttu-id="b057b-116">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="b057b-116">Next step</span></span>

*  [<span data-ttu-id="b057b-117">Nasıl toosecure arka uç hizmetlerini kullanan istemci kimlik doğrulama sertifikası</span><span class="sxs-lookup"><span data-stu-id="b057b-117">How toosecure back-end services using client certificate authentication</span></span>](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [<span data-ttu-id="b057b-118">Nasıl tooupload sertifikaları</span><span class="sxs-lookup"><span data-stu-id="b057b-118">How tooupload certificates</span></span>](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

