---
title: "aaa \"Azure Batch havuzu delete başlangıç olayı | Microsoft Docs\""
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
ms.openlocfilehash: 79bb28bffc760a49cc0a95062f5086dc96c6a795
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-start-event"></a><span data-ttu-id="3b2b9-103">Havuz delete başlangıç olayı</span><span class="sxs-lookup"><span data-stu-id="3b2b9-103">Pool delete start event</span></span>

 <span data-ttu-id="3b2b9-104">Bir havuzu silme işlemi başlatıldığında bu olay yayınlanır.</span><span class="sxs-lookup"><span data-stu-id="3b2b9-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="3b2b9-105">Zaman uyumsuz bir olay Hello havuzu silme olduğuna göre hello sildikten sonra işlemi yayılan bir havuzu Sil Tamam olayını toobe tamamlandıktan bekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b2b9-105">Since hello pool delete is an asynchronous event, you can expect a pool delete complete event toobe emitted once hello delete operation completes.</span></span>

 <span data-ttu-id="3b2b9-106">Merhaba aşağıdaki örnek havuzu silme başlangıç olayı hello gövdesi gösterir.</span><span class="sxs-lookup"><span data-stu-id="3b2b9-106">hello following example shows hello body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="3b2b9-107">Öğesi</span><span class="sxs-lookup"><span data-stu-id="3b2b9-107">Element</span></span>|<span data-ttu-id="3b2b9-108">Tür</span><span class="sxs-lookup"><span data-stu-id="3b2b9-108">Type</span></span>|<span data-ttu-id="3b2b9-109">Notlar</span><span class="sxs-lookup"><span data-stu-id="3b2b9-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="3b2b9-110">id</span><span class="sxs-lookup"><span data-stu-id="3b2b9-110">id</span></span>|<span data-ttu-id="3b2b9-111">Dize</span><span class="sxs-lookup"><span data-stu-id="3b2b9-111">String</span></span>|<span data-ttu-id="3b2b9-112">Merhaba havuzun Hello kimliği.</span><span class="sxs-lookup"><span data-stu-id="3b2b9-112">hello id of hello pool.</span></span>|
