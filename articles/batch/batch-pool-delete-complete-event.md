---
title: "aaa \"Azure Batch havuzu Sil Tamam olayını | Microsoft Docs\""
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
ms.openlocfilehash: 494c371e48ebfb1bf3d2973a7401829a939ba141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="1a5b8-103">Havuz Sil Tamam olayını</span><span class="sxs-lookup"><span data-stu-id="1a5b8-103">Pool delete complete event</span></span>

 <span data-ttu-id="1a5b8-104">Bir havuzu silme işlemi tamamlandığında bu olay yayınlanır.</span><span class="sxs-lookup"><span data-stu-id="1a5b8-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="1a5b8-105">Merhaba aşağıdaki örnek bir havuzu Sil Tamam olayını hello gövdesi gösterir.</span><span class="sxs-lookup"><span data-stu-id="1a5b8-105">hello following example shows hello body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="1a5b8-106">Öğesi</span><span class="sxs-lookup"><span data-stu-id="1a5b8-106">Element</span></span>|<span data-ttu-id="1a5b8-107">Tür</span><span class="sxs-lookup"><span data-stu-id="1a5b8-107">Type</span></span>|<span data-ttu-id="1a5b8-108">Notlar</span><span class="sxs-lookup"><span data-stu-id="1a5b8-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="1a5b8-109">id</span><span class="sxs-lookup"><span data-stu-id="1a5b8-109">id</span></span>|<span data-ttu-id="1a5b8-110">Dize</span><span class="sxs-lookup"><span data-stu-id="1a5b8-110">String</span></span>|<span data-ttu-id="1a5b8-111">Merhaba havuzun Hello kimliği.</span><span class="sxs-lookup"><span data-stu-id="1a5b8-111">hello id of hello pool.</span></span>|
|<span data-ttu-id="1a5b8-112">startTime</span><span class="sxs-lookup"><span data-stu-id="1a5b8-112">startTime</span></span>|<span data-ttu-id="1a5b8-113">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="1a5b8-113">DateTime</span></span>|<span data-ttu-id="1a5b8-114">Merhaba havuzunu silme hello zaman başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="1a5b8-114">hello time hello pool delete started.</span></span>|
|<span data-ttu-id="1a5b8-115">endTime</span><span class="sxs-lookup"><span data-stu-id="1a5b8-115">endTime</span></span>|<span data-ttu-id="1a5b8-116">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="1a5b8-116">DateTime</span></span>|<span data-ttu-id="1a5b8-117">Merhaba hello havuzunu silme süresi tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="1a5b8-117">hello time hello pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="1a5b8-118">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="1a5b8-118">Remarks</span></span>
<span data-ttu-id="1a5b8-119">Durumları ve havuzu yeniden boyutlandırma işlemi için hata kodları hakkında daha fazla bilgi için bkz: [bir hesaptan bir havuzunu silme](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span><span class="sxs-lookup"><span data-stu-id="1a5b8-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>