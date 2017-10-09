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
# <a name="pool-delete-start-event"></a>Havuz delete başlangıç olayı

 Bir havuzu silme işlemi başlatıldığında bu olay yayınlanır. Zaman uyumsuz bir olay Hello havuzu silme olduğuna göre hello sildikten sonra işlemi yayılan bir havuzu Sil Tamam olayını toobe tamamlandıktan bekleyebilirsiniz.

 Merhaba aşağıdaki örnek havuzu silme başlangıç olayı hello gövdesi gösterir.

```
{
    "id": "myPool1"
}
```

|Öğesi|Tür|Notlar|
|-------------|----------|-----------|
|id|Dize|Merhaba havuzun Hello kimliği.|
