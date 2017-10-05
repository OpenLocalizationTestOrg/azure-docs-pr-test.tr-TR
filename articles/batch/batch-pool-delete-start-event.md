---
title: "Azure Batch havuzu delete başlangıç olayı | Microsoft Docs"
description: "Batch havuzu delete başlangıç olayı referansı."
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
ms.openlocfilehash: f8a5241dce422e5c826ab428da6d7bc93284a1cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="pool-delete-start-event"></a><span data-ttu-id="8829f-103">Havuz delete başlangıç olayı</span><span class="sxs-lookup"><span data-stu-id="8829f-103">Pool delete start event</span></span>

 <span data-ttu-id="8829f-104">Bir havuzu silme işlemi başlatıldığında bu olay yayınlanır.</span><span class="sxs-lookup"><span data-stu-id="8829f-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="8829f-105">Zaman uyumsuz bir olay havuzu silme olduğuna göre silme işlemi tamamlandıktan sonra yayınlaması için bir havuz Sil Tamam olayını bekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8829f-105">Since the pool delete is an asynchronous event, you can expect a pool delete complete event to be emitted once the delete operation completes.</span></span>

 <span data-ttu-id="8829f-106">Aşağıdaki örnek, havuzu silme başlangıç olayı gövdesi gösterir.</span><span class="sxs-lookup"><span data-stu-id="8829f-106">The following example shows the body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="8829f-107">Öğesi</span><span class="sxs-lookup"><span data-stu-id="8829f-107">Element</span></span>|<span data-ttu-id="8829f-108">Tür</span><span class="sxs-lookup"><span data-stu-id="8829f-108">Type</span></span>|<span data-ttu-id="8829f-109">Notlar</span><span class="sxs-lookup"><span data-stu-id="8829f-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="8829f-110">id</span><span class="sxs-lookup"><span data-stu-id="8829f-110">id</span></span>|<span data-ttu-id="8829f-111">Dize</span><span class="sxs-lookup"><span data-stu-id="8829f-111">String</span></span>|<span data-ttu-id="8829f-112">Havuzun kimliği.</span><span class="sxs-lookup"><span data-stu-id="8829f-112">The id of the pool.</span></span>|