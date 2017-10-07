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
# <a name="batch-analytics"></a>Toplu analizi
Toplu analizi Hello konularında hello olay ve Uyarılar için toplu service kaynakları kullanılabilir için başvuru bilgileri içerir.

Bkz: [Azure Batch tanılama günlük](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) etkinleştirme ve toplu tanılama günlüklerini kullanma hakkında daha fazla bilgi.

## <a name="diagnostic-logs"></a>Tanılama günlükleri

Hello Azure Batch hizmetinin belirli Batch kaynaklarını hello ömrü boyunca tanılama günlük olayları aşağıdaki hello yayar.

**Hizmeti oturum açma olayları**
* [Havuz oluşturma](batch-pool-create-event.md)
* [Havuzu silme Başlat](batch-pool-delete-start-event.md)
* [Havuzu silme tamamlandı](batch-pool-delete-complete-event.md)
* [Havuzu yeniden boyutlandırma Başlat](batch-pool-resize-start-event.md)
* [Tam havuzu yeniden boyutlandırma](batch-pool-resize-complete-event.md)
* [Görev Başlat](batch-task-start-event.md)
* [Görev tamamlandı](batch-task-complete-event.md)
* [Görev başarısız](batch-task-fail-event.md)