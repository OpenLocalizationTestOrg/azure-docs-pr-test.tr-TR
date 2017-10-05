---
title: Azure toplu analizi | Microsoft Docs
description: "Azure toplu analizi için başvuru."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 7d634e1bb595a84b8af339e5bc5a483a7849e7f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="batch-analytics"></a><span data-ttu-id="59402-103">Toplu analizi</span><span class="sxs-lookup"><span data-stu-id="59402-103">Batch Analytics</span></span>
<span data-ttu-id="59402-104">Konular toplu analizi, olaylar ve Uyarılar için toplu service kaynakları kullanılabilir için başvuru bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="59402-104">The topics in Batch Analytics contain reference information for the events and alerts available for Batch service resources.</span></span>

<span data-ttu-id="59402-105">Bkz: [Azure Batch tanılama günlük](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) etkinleştirme ve toplu tanılama günlüklerini kullanma hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="59402-105">See [Azure Batch diagnostic logging](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) for more information on enabling and consuming Batch diagnostic logs.</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="59402-106">Tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="59402-106">Diagnostic logs</span></span>

<span data-ttu-id="59402-107">Azure Batch hizmeti aşağıdaki tanılama günlük olayları belirli Batch kaynaklarını ömrü boyunca yayar.</span><span class="sxs-lookup"><span data-stu-id="59402-107">The Azure Batch service emits the following diagnostic log events during the lifetime of certain Batch resources.</span></span>

<span data-ttu-id="59402-108">**Hizmeti oturum açma olayları**</span><span class="sxs-lookup"><span data-stu-id="59402-108">**Service Log events**</span></span>
* [<span data-ttu-id="59402-109">Havuz oluşturma</span><span class="sxs-lookup"><span data-stu-id="59402-109">Pool create</span></span>](batch-pool-create-event.md)
* [<span data-ttu-id="59402-110">Havuzu silme Başlat</span><span class="sxs-lookup"><span data-stu-id="59402-110">Pool delete start</span></span>](batch-pool-delete-start-event.md)
* [<span data-ttu-id="59402-111">Havuzu silme tamamlandı</span><span class="sxs-lookup"><span data-stu-id="59402-111">Pool delete complete</span></span>](batch-pool-delete-complete-event.md)
* [<span data-ttu-id="59402-112">Havuzu yeniden boyutlandırma Başlat</span><span class="sxs-lookup"><span data-stu-id="59402-112">Pool resize start</span></span>](batch-pool-resize-start-event.md)
* [<span data-ttu-id="59402-113">Tam havuzu yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="59402-113">Pool resize complete</span></span>](batch-pool-resize-complete-event.md)
* [<span data-ttu-id="59402-114">Görev Başlat</span><span class="sxs-lookup"><span data-stu-id="59402-114">Task start</span></span>](batch-task-start-event.md)
* [<span data-ttu-id="59402-115">Görev tamamlandı</span><span class="sxs-lookup"><span data-stu-id="59402-115">Task complete</span></span>](batch-task-complete-event.md)
* [<span data-ttu-id="59402-116">Görev başarısız</span><span class="sxs-lookup"><span data-stu-id="59402-116">Task fail</span></span>](batch-task-fail-event.md)