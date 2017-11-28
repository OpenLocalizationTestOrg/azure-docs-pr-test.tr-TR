---
title: "API Management - Azure API Management sertifika kimlik doğrulaması kullanan istemci API'ları güvenli | Microsoft Docs"
description: "İstemci sertifikalarını kullanan API'lerine erişimi güvenli öğrenin"
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
ms.openlocfilehash: d3d51d0575a6d2dacced931601d48eb1e51a4051
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-secure-apis-using-client-certificate-authentication-in-api-management"></a><span data-ttu-id="a5680-103">Sertifika kimlik doğrulaması API Management istemcisini kullanarak API güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="a5680-103">How to secure APIs using client certificate authentication in API Management</span></span>

<span data-ttu-id="a5680-104">API Management güvenli API'leri (yani, API Management istemcisini) erişim olanağı sunar istemci sertifikalarını kullanan.</span><span class="sxs-lookup"><span data-stu-id="a5680-104">API Management provides the capability to secure access to APIs (i.e., client to API Management) using client certificates.</span></span> <span data-ttu-id="a5680-105">Şu anda, istenen değerle istemci sertifikanın parmak izini kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5680-105">Currently, you can check the thumbprint of a client certificate against a desired value.</span></span> <span data-ttu-id="a5680-106">Ayrıca karşı API Management yüklenen mevcut sertifika parmak izini kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5680-106">You can also check the thumbprint against existing certificates uploaded to API Management.</span></span>  

<span data-ttu-id="a5680-107">İstemci sertifikalarını (yani, arka uç için API Management) kullanan bir API'nin arka uç hizmetine erişim güvenliğini sağlama hakkında daha fazla bilgi için bkz: [arka uç hizmetlerini kullanan istemci sertifikası kimlik doğrulaması güvenliğini sağlama](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span><span class="sxs-lookup"><span data-stu-id="a5680-107">For information about securing access to the back-end service of an API using client certificates (i.e., API Management to back-end), see [How to secure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span></span>

## <a name="checking-the-expiration-date"></a><span data-ttu-id="a5680-108">Sona erme tarihini denetleniyor</span><span class="sxs-lookup"><span data-stu-id="a5680-108">Checking the expiration date</span></span>

<span data-ttu-id="a5680-109">İlkeleri, sertifikanın geçerlilik süresinin dolup olmadığını denetlemek için yapılandırılabilir:</span><span class="sxs-lookup"><span data-stu-id="a5680-109">Below policies can be configured to check if the certificate is expired:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-issuer-and-subject"></a><span data-ttu-id="a5680-110">Sertifikayı veren ve konu denetleniyor</span><span class="sxs-lookup"><span data-stu-id="a5680-110">Checking the issuer and subject</span></span>

<span data-ttu-id="a5680-111">İlkeleri veren ve bir istemci sertifikasının konu denetlemek için yapılandırılabilir:</span><span class="sxs-lookup"><span data-stu-id="a5680-111">Below policies can be configured to check the issuer and subject of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-thumbprint"></a><span data-ttu-id="a5680-112">Parmak izi denetleniyor</span><span class="sxs-lookup"><span data-stu-id="a5680-112">Checking the thumbprint</span></span>

<span data-ttu-id="a5680-113">İlkeleri, bir sertifikanın parmak izini istemci denetlemek için yapılandırılabilir:</span><span class="sxs-lookup"><span data-stu-id="a5680-113">Below policies can be configured to check the thumbprint of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-to-api-management"></a><span data-ttu-id="a5680-114">API Management karşıya bir parmak izi sertifikalara karşı denetleniyor</span><span class="sxs-lookup"><span data-stu-id="a5680-114">Checking a thumbprint against certificates uploaded to API Management</span></span>

<span data-ttu-id="a5680-115">Aşağıdaki örnek, bir sertifikanın parmak izini istemci API Management karşıya sertifikalara karşı denetleyin gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="a5680-115">The following example shows how to check the thumbprint of a client certificate against certificates uploaded to API Management:</span></span> 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a><span data-ttu-id="a5680-116">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="a5680-116">Next step</span></span>

*  [<span data-ttu-id="a5680-117">Arka uç hizmetlerini kullanan istemci sertifikası kimlik doğrulaması güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="a5680-117">How to secure back-end services using client certificate authentication</span></span>](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [<span data-ttu-id="a5680-118">Nasıl sertifikalarını karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="a5680-118">How to upload certificates</span></span>](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

