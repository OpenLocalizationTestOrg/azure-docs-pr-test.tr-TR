---
title: "Azure uygulama hizmeti IP kısıtlamaları | Microsoft Docs"
description: "Azure App Service ile IP kısıtlamaları kullanma"
author: btardif
manager: stefsch
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: 3be1f4bd-8a81-4565-8a56-528c037b24bd
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/23/2017
ms.author: byvinyal
ms.openlocfilehash: 22e05af889b4e792dcc6f6fc438e8a58674b9f0e
ms.sourcegitcommit: 28178ca0364e498318e2630f51ba6158e4a09a89
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/24/2018
---
# <a name="azure-app-service-static-ip-restrictions"></a>Azure uygulama hizmeti statik IP kısıtlamaları #

IP kısıtlamaları, uygulamanızı erişmesine izin verilen IP adreslerinin listesi tanımlamanıza olanak sağlar. İzin verilenler listesine tek tek IP adresleri içerebilir veya bir IP adresi aralığı bir alt ağ maskesi kullanılarak tanımlanmış.

Uygulama için bir istek bir istemciden oluşturulduğunda, IP adresi izin verilenler listesine göre değerlendirilir. IP adresi listede değilse, uygulama ile yanıtlar bir [HTTP 403](https://en.wikipedia.org/wiki/HTTP_403) durum kodu.

IP kısıtlamaları, çalışma zamanında uygulamanızı tüketir web.config dosyasında tanımlanır. Belirli koşullar altında IP kısıtlamaları mantığı HTTP ardışık düzeninde önce bazı modülü yürütülen. Bu durumda istek farklı bir HTTP hata kodu ile başarısız olur.

IP kısıtlamaları uygulamanıza atanan aynı uygulama hizmeti planı örneklerinde değerlendirilir.

Uygulamanız için bir IP kısıtlama Kuralı Ekle için açmak üzere menüyü kullanın **ağ**>**IP kısıtlamaları** ve tıklayın **IP kısıtlamalarını yapılandırma**

! [IP kısıtlamaları] (media/app-service-ip-restrictions/ip-restrictions.png)

Buradan, uygulamanız için tanımlanan IP kısıtlama kuralları listesini gözden geçirebilirsiniz.

![Liste IP kısıtlamaları](media/app-service-ip-restrictions/browse-ip-restrictions.png)

Tıklatabilirsiniz **[+] Ekle** yeni bir IP kısıtlama kuralı eklemek için.

![IP kısıtlamaları Ekle](media/app-service-ip-restrictions/add-ip-restrictions.png)
