---
title: "aaa \"Azure Batch görev başarısız olay | Microsoft Docs\""
description: "Toplu Görev başvurusunu olay başarısız."
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
ms.openlocfilehash: e92604671650900072ba27f807501b704329e865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="task-fail-event"></a>Görev başarısız olayı

 Bu olay, bir hata ile bir görev tamamlandıktan sonra yayınlanır. Şu anda tüm sıfır olmayan çıkış kodları hata olarak kabul edilir. Bu olay yayılan *ek olarak* bir görevi tamamlamak olay ve bir görev başarısız olduğunda kullanılan toodetect olabilir.


 Merhaba aşağıdaki örnek hello gövdesi bir görevin başarısız olay gösterir.

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
        "startTime": "2016-09-08T16:32:23.799Z",
        "endTime": "2016-09-08T16:34:00.666Z",
        "exitCode": 1,
        "retryCount": 2,
        "requeueCount": 0
    }
}
```

|Öğe adı|Tür|Notlar|
|------------------|----------|-----------|
|İş kimliği|Dize|Başlangıç görevini içeren hello işin Hello kimliği.|
|id|Dize|Merhaba görev Hello kimliği.|
|taskType|Dize|Başlangıç görevinin Hello türü. Bu, her bir iş yöneticisi görevi olduğunu gösteren'JobManager ' veya 'kullanıcı bir iş yöneticisi görevi değil belirten' olabilir. Bu olay, iş hazırlama görevleri, iş sürüm görevleri veya başlangıç görevleri için gösterilen değil.|
|systemTaskVersion|Int32|Bir görev hello iç yeniden deneme sayacı budur. Dahili olarak hello toplu işlem hizmeti görevi tooaccount geçici sorunlar için yeniden deneyebilir. Bu sorunları işlem düğümlerinden iç zamanlama hataları veya deneme toorecover hatalı bir duruma içerebilir.|
|[nodeInfo](#nodeInfo)|Karmaşık türü|Merhaba işlem düğümü üzerinde hangi hello görevi çalıştı hakkında bilgiler içerir.|
|[multiInstanceSettings](#multiInstanceSettings)|Karmaşık türü|Birden çok işlem düğümleri gerektiren çok örnekli görev hello görev olduğunu belirtir.  Bkz: [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) Ayrıntılar için.|
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
|numberOfInstances|Int32|işlem düğümü başlangıç görevi tarafından istenen Hello sayısı.|

###  <a name="constraints"></a>kısıtlamaları

|Öğe adı|Tür|Notlar|
|------------------|----------|-----------|
|maxTaskRetryCount|Int32|en fazla kaç kez hello görev denenen hello. çıkış kodu sıfır değilse hello toplu işlem hizmeti görevi yeniden dener.<br /><br /> Bu değer özellikle hello yeniden deneme sayısı kontrol edin. Merhaba Batch hizmeti hello görev bir kez dener ve ardından toothis yeniden deneme sınırı. Örneğin, Hello en fazla yeniden deneme sayısı 3 ise, toplu bir görev too4 (bir ilk deneyin ve 3 yeniden denemeyi) kez çalışır.<br /><br /> Merhaba maksimum yeniden deneme sayısının 0 olması durumunda hello toplu işlem hizmetinin görevleri yeniden denemez.<br /><br /> Merhaba en fazla yeniden deneme sayısı -1 ise, hello Batch hizmetinin görevleri sınır olmaksızın yeniden dener.<br /><br /> 0 (yeniden deneme) Hello varsayılan değerdir.|


###  <a name="executionInfo"></a>executionInfo

|Öğe adı|Tür|Notlar|
|------------------|----------|-----------|
|startTime|Tarih saat|hangi hello görevin çalışmaya başladığı anda Hello. Karşılık gelen toohello 'Çalışıyor' **çalıştıran** hello görev kaynak dosyaları veya uygulama paketleri belirtiyorsa, indirme ya da bunlar dağıtma başlatılan hangi hello görev hello zaman hello başlangıç zamanı yansıtır şekilde belirtin.  Merhaba görev yeniden ya da yeniden deneme işlemi, hangi hello görev en son zaman çalışmaya başladığı hello budur.|
|endTime|Tarih saat|Merhaba zaman hangi hello görev tamamlandı.|
|exitCode|Int32|Merhaba görev Hello çıkış kodu.|
|retryCount|Int32|Merhaba görev hello Batch hizmeti tarafından denenen sayısı hello. toohello MaxTaskRetryCount belirtilen sıfır olmayan çıkış kodu ile bulunup bulunmadığını hello görev denenir.|
|requeueCount|Int32|Merhaba Batch hizmeti tarafından bir kullanıcı isteği hello sonucu olarak hello görev yeniden kuyruğa sayısı hello.<br /><br /> Yeniden boyutlandırma veya hello havuzu küçültme) bir havuz (veya ne zaman hello işi devre dışı bırakılıyor, hello kullanıcı düğümlerden çalışan hello düğümlerinde görevleri belirtebilirsiniz hello kullanıcı kaldırır çalıştırılmak üzere yeniden kuyruğa olduğunda. Bu sayı, şu nedenlerden dolayı kaç kez hello görev sıraya izler.|
