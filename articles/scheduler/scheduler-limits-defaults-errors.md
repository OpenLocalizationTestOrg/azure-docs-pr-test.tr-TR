---
title: "Scheduler sınırları ve Varsayılanları"
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
ms.openlocfilehash: db6b1c196cb468f41c7a7ce34758de346b522abb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-limits-and-defaults"></a><span data-ttu-id="f48f2-103">Scheduler sınırları ve Varsayılanları</span><span class="sxs-lookup"><span data-stu-id="f48f2-103">Scheduler Limits and Defaults</span></span>
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a><span data-ttu-id="f48f2-104">Zamanlayıcı kotaları, sınırları, Varsayılanları ve kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="f48f2-104">Scheduler Quotas, Limits, Defaults, and Throttles</span></span>
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="the-x-ms-request-id-header"></a><span data-ttu-id="f48f2-105">X-ms-request-id üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="f48f2-105">The x-ms-request-id Header</span></span>
<span data-ttu-id="f48f2-106">Adlı bir yanıt üstbilgisi karşı Zamanlayıcı hizmeti yapılan her isteği döndürür**x-ms-request-id**.</span><span class="sxs-lookup"><span data-stu-id="f48f2-106">Every request made against the Scheduler service returns a response header named**x-ms-request-id**.</span></span> <span data-ttu-id="f48f2-107">Bu başlığı istek benzersiz olarak tanımlayan genel olmayan bir değer içerir.</span><span class="sxs-lookup"><span data-stu-id="f48f2-107">This header contains an opaque value that uniquely identifies the request.</span></span>

<span data-ttu-id="f48f2-108">Bir istek sürekli olarak başarısız oluyor ve istek düzgün şeklide doğruladıktan, Microsoft'a hata raporu için bu değeri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f48f2-108">If a request is consistently failing and you have verified that the request is properly formulated, you may use this value to report the error to Microsoft.</span></span> <span data-ttu-id="f48f2-109">Raporunuzda, x-ms-request-id, isteği yapıldı yaklaşık zaman değeri, abonelik, iş koleksiyonu ve/veya iş ve istek çalıştı işlemi türünü tanımlayıcısını içerir.</span><span class="sxs-lookup"><span data-stu-id="f48f2-109">In your report, include the value of x-ms-request-id, the approximate time that the request was made, the identifier of the subscription, job collection, and/or job, and the type of operation that the request attempted.</span></span>

## <a name="see-also"></a><span data-ttu-id="f48f2-110">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f48f2-110">See Also</span></span>
 [<span data-ttu-id="f48f2-111">Scheduler nedir?</span><span class="sxs-lookup"><span data-stu-id="f48f2-111">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="f48f2-112">Azure Scheduler kavramları, terminolojisi ve varlık hiyerarşisi</span><span class="sxs-lookup"><span data-stu-id="f48f2-112">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="f48f2-113">Azure portalında Scheduler’ı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="f48f2-113">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="f48f2-114">Azure Scheduler’da planlar ve faturalama</span><span class="sxs-lookup"><span data-stu-id="f48f2-114">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="f48f2-115">Azure Scheduler REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="f48f2-115">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="f48f2-116">Azure Scheduler PowerShell cmdlet’leri başvurusu</span><span class="sxs-lookup"><span data-stu-id="f48f2-116">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="f48f2-117">Yüksek Azure Scheduler kullanılabilirliği ve güvenilirliği</span><span class="sxs-lookup"><span data-stu-id="f48f2-117">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="f48f2-118">Azure Scheduler giden bağlantı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="f48f2-118">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

