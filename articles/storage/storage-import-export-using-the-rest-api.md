---
title: "aaaUsing hello Azure içeri/dışarı aktarma hizmeti REST API'si | Microsoft Docs"
description: "Burada toofind kaynakları'hello Azure içeri/dışarı aktarma kullanmak için REST API, her iki nasıl tooand başvuru malzemesinde dahil olmak üzere hizmet öğrenin."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: a01c170b1bc9c2b2ce9086d39de78a39fafb2c8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a>Hello Azure içeri/dışarı aktarma hizmeti REST API kullanma

Merhaba Microsoft Azure içeri/dışarı aktarma hizmeti REST API'si tooenable programsal denetim içeri/dışarı aktarma işlerinin kullanıma sunar. Tüm hello içeri/dışarı aktarma hello ile gerçekleştirebileceğiniz işlemler hello REST API tooperform kullanabileceğiniz [Azure portal](https://portal.azure.com/). Ayrıca, hello Klasik portalda şu anda kullanılabilir olmayan bir işin hello tamamlanma sorgulama gibi bazı ayrıntılı işlemleri hello REST API tooperform kullanabilirsiniz.

Bkz: [hello Microsoft Azure içeri/dışarı aktarma hizmeti tooTransfer veri tooBlob depolama kullanarak](storage-import-export-service.md) hello içeri/dışarı aktarma hizmeti ve nasıl toouse Klasik portal toocreate hello ve içeri aktarma yönetmek gösteren bir eğitim genel bakış ve işleri dışa aktarın.

## <a name="service-endpoints"></a>Hizmet uç noktaları

Hello Azure içeri/dışarı aktarma hizmeti kaynak sağlayıcısı için Azure Resource Manager ve bir dizi REST API hello içeri/dışarı aktarma işleri yönetmek için HTTPS uç noktası şu anda sağlar:

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a>Sürüm oluşturma

Toohello içeri/dışarı aktarma hizmeti hello belirtmelisiniz istekleri `api-version` parametresi ve değeri çok ayarlayın`2016-11-01`.

## <a name="importexport-service-operations"></a>İçeri/dışarı aktarma hizmeti işlemleri

[İçeri aktarma işi oluşturma](storage-import-export-creating-an-import-job.md)

[Dışarı aktarma işi oluşturma](storage-import-export-creating-an-export-job.md)

[Bir iş için durum bilgilerini alma](storage-import-export-retrieving-state-info-for-a-job.md)

[İşleri numaralandırma](storage-import-export-enumerating-jobs.md)

[İşleri iptal etme ve silme](storage-import-export-cancelling-and-deleting-jobs.md)

[Yedekleme sürücü bildirimleri](storage-import-export-backing-up-drive-manifests.md)

[İçeri/Dışarı Aktarma işleri için tanılama ve hata kurtarma](storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a>Sonraki adımlar

* [Depolama içeri/dışarı aktarma REST](/rest/api/storageimportexport)
