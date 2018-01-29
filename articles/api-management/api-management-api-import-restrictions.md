---
title: "Azure API Management API alma bilinen sorunlar ve kısıtlama | Microsoft Docs"
description: "Bilinen sorunlar ve açık API, WSDL veya WADL biçimlerini kullanarak Azure API Management içe kısıtlamalar ayrıntıları."
services: api-management
documentationcenter: 
author: vladvino
manager: vlvinogr
editor: 
ms.assetid: 7a5a63f0-3e72-49d3-a28c-1bb23ab495e2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2017
ms.author: apipm
ms.openlocfilehash: 758babce3ed387ed4864f1934650cf701bda788f
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/04/2017
---
# <a name="api-import-restrictions-and-known-issues"></a>API içeri aktarma kısıtlamaları ve bilinen sorunlar
## <a name="about-this-list"></a>Bu liste hakkında
Bir API içeri aktarırken, bazı kısıtlamalar gelen veya başarıyla içeri aktarmadan önce düzeltilinceye gereken sorunları tanımlamak. Bu makale belgeleri bunlar, organize API tarafından alma biçimi.

## <a name="open-api"></a>API/Swagger açın
Açık API belgenizi alma hata alıyorsanız, doğrulandı, - ya da Tasarımcısı'nı kullanarak Azure portalında (Tasarım - ön uç - API Belirtimi Düzenleyiciyi Aç), emin olun veya bir üçüncü taraf aracı gibi <a href="http://www.swagger.io">Swagger Editor</a>.

* **Ana bilgisayar adı** APIM bir ana bilgisayar adı özniteliği gerektirir.
* **Temel yolu** APIM temel yol özniteliği gerektirir.
* **Düzenleri** APIM bir şema dizisi gerektirir. 

## <a name="wsdl"></a>WSDL
WSDL dosyaları veya bir SOAP ve REST API'si arka ucu olarak hizmet SOAP doğrudan API'ları oluşturmak için kullanılır.

* **WSDL: import** -şu anda APIM bu özniteliği kullanılarak API'leri desteklemez. Müşteriler, bir belgeye alınan öğeleri birleştirmeniz gerekir.
* **Birden çok bölümü olan iletiler** şu anda, bu tür iletilerin APIM desteklemiyor.
* **WCF wsHttpBinding** Windows Communication Foundation ile oluşturulan SOAP Hizmetleri basicHttpBinding kullanması gereken - wsHttpBinding desteklenmiyor.
* **MTOM** MTOM kullanan hizmetler <em>olabilir</em> çalışır. Resmi desteği şu anda önerilmez.
* **Özyineleme** türlerini tanımlanan yinelemeli olarak (örneğin, bir dizi kendileri için bakın) APIM tarafından desteklenmez.

## <a name="wadl"></a>WADL
Şu anda hiçbir bilinen WADL alma sorunları vardır.
