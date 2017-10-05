---
title: "Azure Batch havuzu Sil Tamam olayını | Microsoft Docs"
description: "Batch havuzundaki başvurusunu complete olayını silin."
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
ms.openlocfilehash: 890f2ba7fda37060c56177868d6214d517d91831
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="bbcd8-103">Havuz Sil Tamam olayını</span><span class="sxs-lookup"><span data-stu-id="bbcd8-103">Pool delete complete event</span></span>

 <span data-ttu-id="bbcd8-104">Bir havuzu silme işlemi tamamlandığında bu olay yayınlanır.</span><span class="sxs-lookup"><span data-stu-id="bbcd8-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="bbcd8-105">Aşağıdaki örnek, bir havuz Sil Tamam olayını gövdesi gösterir.</span><span class="sxs-lookup"><span data-stu-id="bbcd8-105">The following example shows the body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="bbcd8-106">Öğesi</span><span class="sxs-lookup"><span data-stu-id="bbcd8-106">Element</span></span>|<span data-ttu-id="bbcd8-107">Tür</span><span class="sxs-lookup"><span data-stu-id="bbcd8-107">Type</span></span>|<span data-ttu-id="bbcd8-108">Notlar</span><span class="sxs-lookup"><span data-stu-id="bbcd8-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="bbcd8-109">id</span><span class="sxs-lookup"><span data-stu-id="bbcd8-109">id</span></span>|<span data-ttu-id="bbcd8-110">Dize</span><span class="sxs-lookup"><span data-stu-id="bbcd8-110">String</span></span>|<span data-ttu-id="bbcd8-111">Havuzun kimliği.</span><span class="sxs-lookup"><span data-stu-id="bbcd8-111">The id of the pool.</span></span>|
|<span data-ttu-id="bbcd8-112">startTime</span><span class="sxs-lookup"><span data-stu-id="bbcd8-112">startTime</span></span>|<span data-ttu-id="bbcd8-113">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="bbcd8-113">DateTime</span></span>|<span data-ttu-id="bbcd8-114">Havuzunu silme zamanı başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="bbcd8-114">The time the pool delete started.</span></span>|
|<span data-ttu-id="bbcd8-115">EndTime</span><span class="sxs-lookup"><span data-stu-id="bbcd8-115">endTime</span></span>|<span data-ttu-id="bbcd8-116">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="bbcd8-116">DateTime</span></span>|<span data-ttu-id="bbcd8-117">Tamamlanan havuzunu silme zamanı.</span><span class="sxs-lookup"><span data-stu-id="bbcd8-117">The time the pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="bbcd8-118">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="bbcd8-118">Remarks</span></span>
<span data-ttu-id="bbcd8-119">Durumları ve havuzu yeniden boyutlandırma işlemi için hata kodları hakkında daha fazla bilgi için bkz: [bir hesaptan bir havuzunu silme](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span><span class="sxs-lookup"><span data-stu-id="bbcd8-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>