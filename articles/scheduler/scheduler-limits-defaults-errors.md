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
# <a name="scheduler-limits-and-defaults"></a><span data-ttu-id="b0131-103">Scheduler sınırları ve Varsayılanları</span><span class="sxs-lookup"><span data-stu-id="b0131-103">Scheduler Limits and Defaults</span></span>
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a><span data-ttu-id="b0131-104">Zamanlayıcı kotaları, sınırları, Varsayılanları ve kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="b0131-104">Scheduler Quotas, Limits, Defaults, and Throttles</span></span>
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="hello-x-ms-request-id-header"></a><span data-ttu-id="b0131-105">Merhaba x-ms-request-id üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="b0131-105">hello x-ms-request-id Header</span></span>
<span data-ttu-id="b0131-106">Adlı bir yanıt üstbilgisi Zamanlayıcı hizmeti Hello karşı yapılan her isteği döndürür**x-ms-request-id**. Bu başlığı hello isteği benzersiz olarak tanımlayan genel olmayan bir değer içerir.</span><span class="sxs-lookup"><span data-stu-id="b0131-106">Every request made against hello Scheduler service returns a response header named**x-ms-request-id**. This header contains an opaque value that uniquely identifies hello request.</span></span>

<span data-ttu-id="b0131-107">Bir istek tutarlı bir şekilde ise başarısız olan ve doğruladıktan hello isteği düzgün şeklide, bu değer tooreport hello hata tooMicrosoft kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="b0131-107">If a request is consistently failing and you have verified that hello request is properly formulated, you may use this value tooreport hello error tooMicrosoft.</span></span> <span data-ttu-id="b0131-108">X-ms-request-id, hello yaklaşık zaman hello değeri, raporunuza dahil hello abonelik, iş koleksiyonu ve/veya iş tanıtıcısı hello ve hello çalıştı isteği hello işlem türü bu hello isteği yapıldı.</span><span class="sxs-lookup"><span data-stu-id="b0131-108">In your report, include hello value of x-ms-request-id, hello approximate time that hello request was made, hello identifier of hello subscription, job collection, and/or job, and hello type of operation that hello request attempted.</span></span>

## <a name="see-also"></a><span data-ttu-id="b0131-109">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="b0131-109">See Also</span></span>
 [<span data-ttu-id="b0131-110">Scheduler nedir?</span><span class="sxs-lookup"><span data-stu-id="b0131-110">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="b0131-111">Azure Scheduler kavramları, terminolojisi ve varlık hiyerarşisi</span><span class="sxs-lookup"><span data-stu-id="b0131-111">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="b0131-112">Zamanlayıcı hello Azure portalını kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b0131-112">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="b0131-113">Azure Scheduler’da planlar ve faturalama</span><span class="sxs-lookup"><span data-stu-id="b0131-113">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="b0131-114">Azure Scheduler REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="b0131-114">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="b0131-115">Azure Scheduler PowerShell cmdlet’leri başvurusu</span><span class="sxs-lookup"><span data-stu-id="b0131-115">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="b0131-116">Yüksek Azure Scheduler kullanılabilirliği ve güvenilirliği</span><span class="sxs-lookup"><span data-stu-id="b0131-116">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="b0131-117">Azure Scheduler giden bağlantı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="b0131-117">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

