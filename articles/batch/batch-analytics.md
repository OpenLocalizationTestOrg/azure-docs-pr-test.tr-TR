---
title: aaaAzure toplu analizi | Microsoft Docs
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
ms.openlocfilehash: 462fbad1ac522b485ae18c1e8891b9d2cabd45e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="batch-analytics"></a><span data-ttu-id="6d915-103">Toplu analizi</span><span class="sxs-lookup"><span data-stu-id="6d915-103">Batch Analytics</span></span>
<span data-ttu-id="6d915-104">Toplu analizi Hello konularında hello olay ve Uyarılar için toplu service kaynakları kullanılabilir için başvuru bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="6d915-104">hello topics in Batch Analytics contain reference information for hello events and alerts available for Batch service resources.</span></span>

<span data-ttu-id="6d915-105">Bkz: [Azure Batch tanılama günlük](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) etkinleştirme ve toplu tanılama günlüklerini kullanma hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="6d915-105">See [Azure Batch diagnostic logging](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) for more information on enabling and consuming Batch diagnostic logs.</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="6d915-106">Tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="6d915-106">Diagnostic logs</span></span>

<span data-ttu-id="6d915-107">Hello Azure Batch hizmetinin belirli Batch kaynaklarını hello ömrü boyunca tanılama günlük olayları aşağıdaki hello yayar.</span><span class="sxs-lookup"><span data-stu-id="6d915-107">hello Azure Batch service emits hello following diagnostic log events during hello lifetime of certain Batch resources.</span></span>

<span data-ttu-id="6d915-108">**Hizmeti oturum açma olayları**</span><span class="sxs-lookup"><span data-stu-id="6d915-108">**Service Log events**</span></span>
* [<span data-ttu-id="6d915-109">Havuz oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d915-109">Pool create</span></span>](batch-pool-create-event.md)
* [<span data-ttu-id="6d915-110">Havuzu silme Başlat</span><span class="sxs-lookup"><span data-stu-id="6d915-110">Pool delete start</span></span>](batch-pool-delete-start-event.md)
* [<span data-ttu-id="6d915-111">Havuzu silme tamamlandı</span><span class="sxs-lookup"><span data-stu-id="6d915-111">Pool delete complete</span></span>](batch-pool-delete-complete-event.md)
* [<span data-ttu-id="6d915-112">Havuzu yeniden boyutlandırma Başlat</span><span class="sxs-lookup"><span data-stu-id="6d915-112">Pool resize start</span></span>](batch-pool-resize-start-event.md)
* [<span data-ttu-id="6d915-113">Tam havuzu yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="6d915-113">Pool resize complete</span></span>](batch-pool-resize-complete-event.md)
* [<span data-ttu-id="6d915-114">Görev Başlat</span><span class="sxs-lookup"><span data-stu-id="6d915-114">Task start</span></span>](batch-task-start-event.md)
* [<span data-ttu-id="6d915-115">Görev tamamlandı</span><span class="sxs-lookup"><span data-stu-id="6d915-115">Task complete</span></span>](batch-task-complete-event.md)
* [<span data-ttu-id="6d915-116">Görev başarısız</span><span class="sxs-lookup"><span data-stu-id="6d915-116">Task fail</span></span>](batch-task-fail-event.md)