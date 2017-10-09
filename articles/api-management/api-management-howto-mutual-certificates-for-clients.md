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
# <a name="how-toosecure-apis-using-client-certificate-authentication-in-api-management"></a>Toosecure API'lerini kullanan istemci kimlik doğrulama sertifikasını API Yönetimi

API Management sağlar hello yetenek toosecure erişim tooAPIs (yani, istemci tooAPI yönetim) istemci sertifikalarını kullanan. Şu anda hello bir sertifikanın parmak izini istemci istenen değerle kontrol edebilirsiniz. Ayrıca, tooAPI yönetim hello parmak izi varolan sertifikalara karşı karşıya kontrol edebilirsiniz.  

Erişim toohello arka uç hizmeti istemci sertifikalarını (yani, API Management tooback uç) kullanan bir API güvenliğini sağlama hakkında daha fazla bilgi için bkz: [nasıl toosecure arka uç hizmetlerini kullanan istemci kimlik doğrulama sertifikası](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)

## <a name="checking-hello-expiration-date"></a>Merhaba sona erme tarihi denetleniyor

İlkeleri Hello sertifikanın süresi dolmuş yapılandırılmış toocheck olabilir:

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-issuer-and-subject"></a>Merhaba veren ve konu denetleniyor

İlkeler yapılandırılmış toocheck hello veren ve bir istemci sertifikasının konu olabilir:

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-thumbprint"></a>Merhaba parmak izi denetleniyor

İlkeler yapılandırılmış toocheck hello bir sertifikanın parmak izini istemci olabilir:

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-tooapi-management"></a>TooAPI yönetim karşıya bir parmak izi sertifikalara karşı denetleniyor

Merhaba aşağıdaki örnekte nasıl tooAPI yönetim toocheck hello bir sertifikanın parmak izini istemci sertifikalara karşı karşıya gösterilmektedir: 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a>Sonraki adım

*  [Nasıl toosecure arka uç hizmetlerini kullanan istemci kimlik doğrulama sertifikası](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [Nasıl tooupload sertifikaları](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

