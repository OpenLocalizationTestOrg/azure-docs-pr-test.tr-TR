---
title: "aaa \"Azure Batch görev başlangıç olayı | Microsoft Docs\""
description: "Toplu Görev Başlangıç olayı referansı."
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
ms.openlocfilehash: 2cb066be1578741125e9081a84a2b7c74dc8356a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="task-start-event"></a>Görev Başlangıç olayı

 Bir görev bir işlem düğümünde zamanlanmış toostart silindikten sonra bu olay hello Zamanlayıcı tarafından yayınlanır. Merhaba görev denenen ya da yeniden kuyruğa bu olay yeniden hello aynı görevi, ancak hello yeniden deneme sayısı ve sistem görev sürümü buna göre güncelleştirilir yayınlaması olduğunu unutmayın.


 Merhaba aşağıdaki örnek bir görev başlangıç olayı hello gövdesi gösterir.

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "retryCount": 0
    }
}
```

|Öğe adı|Tür|Notlar|
|------------------|----------|-----------|
|İş kimliği|Dize|Başlangıç görevini içeren hello işin Hello kimliği.|
|id|Dize|Merhaba görev Hello kimliği.|
|taskType|Dize|Başlangıç görevinin Hello türü. Bu, her bir iş yöneticisi görevi olduğunu gösteren'JobManager ' veya 'kullanıcı bir iş yöneticisi görevi değil belirten' olabilir.|
|systemTaskVersion|Int32|Bir görev hello iç yeniden deneme sayacı budur. Dahili olarak hello toplu işlem hizmeti görevi tooaccount geçici sorunlar için yeniden deneyebilir. Bu sorunları işlem düğümlerinden iç zamanlama hataları veya deneme toorecover hatalı bir duruma içerebilir.|
|[nodeInfo](#nodeInfo)|Karmaşık türü|Merhaba işlem düğümü üzerinde hangi hello görevi çalıştı hakkında bilgiler içerir.|
|[multiInstanceSettings](#multiInstanceSettings)|Karmaşık türü|Çok örnekli görev birden çok işlem düğümleri gerektiren hello görev olduğunu belirtir.  Bkz: [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) Ayrıntılar için.|
|[kısıtlamaları](#constraints)|Karmaşık türü|toothis görev uygulamak hello yürütme kısıtlamaları.|
|[executionInfo](#executionInfo)|Karmaşık türü|Başlangıç görevi hello yürütme hakkında bilgiler içerir.|

###  <a name="nodeInfo"></a>nodeInfo

|Öğe adı|Tür|Notlar|
|------------------|----------|-----------|
|poolId|Dize|Görev hangi hello çalıştı hello havuzun Hello kimliği.|
|nodeId|Dize|Görev hangi hello çalıştı hello düğümün Hello kimliği.|

###  <a name="multiInstanceSettings"></a>multiInstanceSettings

|Öğe adı|Tür|Notlar|
|------------------|----------|-----------|
|numberOfInstances|Int|işlem düğümü başlangıç görevi tarafından istenen Hello sayısı.|

###  <a name="constraints"></a>kısıtlamaları

|Öğe adı|Tür|Notlar|
|------------------|----------|-----------|
|maxTaskRetryCount|Int32|en fazla kaç kez hello görev denenen hello. çıkış kodu sıfır değilse hello toplu işlem hizmeti görevi yeniden dener.<br /><br /> Bu değer özellikle hello yeniden deneme sayısı kontrol edin. Merhaba Batch hizmeti hello görev bir kez dener ve ardından toothis yeniden deneme sınırı. Örneğin, Hello en fazla yeniden deneme sayısı 3 ise, toplu bir görev too4 (bir ilk deneyin ve 3 yeniden denemeyi) kez çalışır.<br /><br /> Merhaba maksimum yeniden deneme sayısının 0 olması durumunda hello toplu işlem hizmetinin görevleri yeniden denemez.<br /><br /> Merhaba en fazla yeniden deneme sayısı -1 ise, hello Batch hizmetinin görevleri sınır olmaksızın yeniden dener.<br /><br /> 0 (yeniden deneme) Hello varsayılan değerdir.|

###  <a name="executionInfo"></a>executionInfo

|Öğe adı|Tür|Notlar|
|------------------|----------|-----------|
|retryCount|Int32|Merhaba görev hello Batch hizmeti tarafından denenen sayısı hello. toohello MaxTaskRetryCount belirtilen sıfır olmayan çıkış kodu ile bulunup bulunmadığını hello görev denenir|
