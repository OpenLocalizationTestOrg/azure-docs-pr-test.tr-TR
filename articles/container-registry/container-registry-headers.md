---
title: "aaaAzure kapsayıcı kayıt defteri depoları | Microsoft Docs"
description: "Nasıl toouse Azure kapsayıcı kayıt defteri depoları Docker görüntüleri"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Azure kapsayıcı kayıt defteri depoları

Azure kapsayıcı kayıt defterleri, hizmetleri ve orchestrators birçok ile uyumludur. toomake bunu daha kolay tootrack hello kaynak hizmet ve aracılarının içinden ACR kullanılır, biz başlatıldı hello Docker.config dosyasında hello Docker üstbilgi alanı kullanma.



## <a name="viewing-repositories-in-hello-portal"></a>Depoları hello Portal görüntüleme

Merhaba ACR üstbilgileri hello biçimi izleyin:
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* Bulut: Azure, Azure yığın veya diğer kamu veya Ülkeye özel Azure bulut. Azure yığını ve kamu Bulutlar şu anda desteklenmemektedir karşın, bu parametre gelecekteki destek sağlar.
* Hizmet: hello hizmetin adı.
* Optionalservicename: isteğe bağlı bir parametre alt Servisleri veya toospecify bir SKU hizmetler için (örn: web uygulamaları Azure/app-service/web-apps ile karşılık gelir).

İş ortağı Hizmetleri ve orchestrators kullanmaları toouse özel üstbilgi değerleri toohelp bizim telemetri ile markalarıdır. Kullanıcılar, böylece isterlerse toohello üstbilgi geçirilen hello değeri değiştirebilirsiniz.

Aşağıda ACR ortakları toouse toopopulate hello "X-Meta-kaynak-Client" alan istiyoruz hello değerler şunlardır:

| Hizmet Adı              | Üstbilgi                                |
| ------------------------- | ------------------------------------- |
| Azure Container Service   | Azure/işlem/azure-kapsayıcı-hizmeti |
| Uygulama hizmeti - Web uygulamaları    | Azure/app-service/web-apps            |
| Uygulama hizmeti - Logic Apps  | Azure/app-service/logic-apps          |
| Batch                     | işlem/Azure/toplu                   |
| Bulut konsol             | Bulut/Azure-konsol                   |
| İşlevler                 | işlem/Azure/işlevleri               |
| Nesnelerin interneti - Hub  | IOT/Azure/hub                         |
| HDInsight                 | Veri/Azure/hdınsight                  |
| Jenkins                   | Azure/jenkins                         |
| Machine Learning          | Azure/data/machile-öğrenme           |
| Service Fabric            | Azure/işlem/service-yapı          |
| VSTS                      | Azure/vsts                            |


## <a name="next-steps"></a>Sonraki adımlar
[Kayıt defterleri, desteklenen hello hizmetler ve orchestrators hakkında daha fazla bilgi edinin](container-registry-intro.md)
