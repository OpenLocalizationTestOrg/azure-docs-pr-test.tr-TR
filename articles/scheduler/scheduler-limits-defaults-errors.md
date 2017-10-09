---
title: "aaaScheduler sınırları ve Varsayılanları"
description: "Scheduler sınırları ve Varsayılanları"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 88f4a3e9-6dbd-4943-8543-f0649d423061
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 6fe0600d3ce3249d5aab1b877369b175316b5437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-limits-and-defaults"></a>Scheduler sınırları ve Varsayılanları
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a>Zamanlayıcı kotaları, sınırları, Varsayılanları ve kısıtlamaları
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="hello-x-ms-request-id-header"></a>Merhaba x-ms-request-id üstbilgisi
Adlı bir yanıt üstbilgisi Zamanlayıcı hizmeti Hello karşı yapılan her isteği döndürür**x-ms-request-id**. Bu başlığı hello isteği benzersiz olarak tanımlayan genel olmayan bir değer içerir.

Bir istek tutarlı bir şekilde ise başarısız olan ve doğruladıktan hello isteği düzgün şeklide, bu değer tooreport hello hata tooMicrosoft kullanabilir. X-ms-request-id, hello yaklaşık zaman hello değeri, raporunuza dahil hello abonelik, iş koleksiyonu ve/veya iş tanıtıcısı hello ve hello çalıştı isteği hello işlem türü bu hello isteği yapıldı.

## <a name="see-also"></a>Ayrıca Bkz.
 [Scheduler nedir?](scheduler-intro.md)

 [Azure Scheduler kavramları, terminolojisi ve varlık hiyerarşisi](scheduler-concepts-terms.md)

 [Zamanlayıcı hello Azure portalını kullanmaya başlama](scheduler-get-started-portal.md)

 [Azure Scheduler’da planlar ve faturalama](scheduler-plans-billing.md)

 [Azure Scheduler REST API başvurusu](https://msdn.microsoft.com/library/mt629143)

 [Azure Scheduler PowerShell cmdlet’leri başvurusu](scheduler-powershell-reference.md)

 [Yüksek Azure Scheduler kullanılabilirliği ve güvenilirliği](scheduler-high-availability-reliability.md)

 [Azure Scheduler giden bağlantı kimlik doğrulaması](scheduler-outbound-authentication.md)

