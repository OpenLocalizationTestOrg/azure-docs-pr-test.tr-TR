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
ms.openlocfilehash: fc7e1007ad632cf6f771c2545644f8de43c8f181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a><span data-ttu-id="dbbe0-103">Hello Azure içeri/dışarı aktarma hizmeti REST API kullanma</span><span class="sxs-lookup"><span data-stu-id="dbbe0-103">Using hello Azure Import/Export service REST API</span></span>

<span data-ttu-id="dbbe0-104">Merhaba Microsoft Azure içeri/dışarı aktarma hizmeti REST API'si tooenable programsal denetim içeri/dışarı aktarma işlerinin kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="dbbe0-104">hello Microsoft Azure Import/Export service exposes a REST API tooenable programmatic control of import/export jobs.</span></span> <span data-ttu-id="dbbe0-105">Tüm hello içeri/dışarı aktarma hello ile gerçekleştirebileceğiniz işlemler hello REST API tooperform kullanabileceğiniz [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="dbbe0-105">You can use hello REST API tooperform all of hello import/export operations that you can perform with hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="dbbe0-106">Ayrıca, hello tamamlanma hello Klasik Azure portalında şu anda kullanılabilir değil bir işin sorgulama gibi belirli ayrıntılı işlemler hello REST API tooperform kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dbbe0-106">Additionally, you can use hello REST API tooperform certain granular operations, such as querying hello percentage completion of a job, which is not currently available in hello Azure classic portal.</span></span>

<span data-ttu-id="dbbe0-107">Bkz: [hello Microsoft Azure içeri/dışarı aktarma hizmeti tooTransfer veri tooBlob depolama kullanarak](../storage-import-export-service.md) hello içeri/dışarı aktarma hizmeti ve nasıl toouse Klasik portal toocreate hello ve içeri aktarma yönetmek gösteren bir eğitim genel bakış ve işleri dışa aktarın.</span><span class="sxs-lookup"><span data-stu-id="dbbe0-107">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](../storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello classic portal toocreate and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="dbbe0-108">Hizmet uç noktaları</span><span class="sxs-lookup"><span data-stu-id="dbbe0-108">Service endpoints</span></span>

<span data-ttu-id="dbbe0-109">Hello Azure içeri/dışarı aktarma hizmeti kaynak sağlayıcısı için Azure Resource Manager ve bir dizi REST API hello içeri/dışarı aktarma işleri yönetmek için HTTPS uç noktası şu anda sağlar:</span><span class="sxs-lookup"><span data-stu-id="dbbe0-109">hello Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at hello following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="dbbe0-110">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="dbbe0-110">Versioning</span></span>

<span data-ttu-id="dbbe0-111">Toohello içeri/dışarı aktarma hizmeti hello belirtmelisiniz istekleri `api-version` parametresi ve değeri çok ayarlayın`2016-11-01`.</span><span class="sxs-lookup"><span data-stu-id="dbbe0-111">Requests toohello Import/Export service must specify hello `api-version` parameter and set its value too`2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="dbbe0-112">İçeri/dışarı aktarma hizmeti işlemleri</span><span class="sxs-lookup"><span data-stu-id="dbbe0-112">Import/Export service operations</span></span>

[<span data-ttu-id="dbbe0-113">İçeri aktarma işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="dbbe0-113">Creating an import job</span></span>](../storage-import-export-creating-an-import-job.md)

[<span data-ttu-id="dbbe0-114">Dışarı aktarma işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="dbbe0-114">Creating an export job</span></span>](../storage-import-export-creating-an-export-job.md)

[<span data-ttu-id="dbbe0-115">Bir iş için durum bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="dbbe0-115">Retrieving state information for a job</span></span>](storage-import-export-retrieving-state-info-for-a-job.md)

[<span data-ttu-id="dbbe0-116">İşleri numaralandırma</span><span class="sxs-lookup"><span data-stu-id="dbbe0-116">Enumerating jobs</span></span>](../storage-import-export-enumerating-jobs.md)

[<span data-ttu-id="dbbe0-117">İşleri iptal etme ve silme</span><span class="sxs-lookup"><span data-stu-id="dbbe0-117">Cancelling and deleting jobs</span></span>](storage-import-export-cancelling-and-deleting-jobs.md)

[<span data-ttu-id="dbbe0-118">Yedekleme sürücü bildirimleri</span><span class="sxs-lookup"><span data-stu-id="dbbe0-118">Backing Up drive manifests</span></span>](../storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="dbbe0-119">İçeri/Dışarı Aktarma işleri için tanılama ve hata kurtarma</span><span class="sxs-lookup"><span data-stu-id="dbbe0-119">Diagnostics and error recovery for Import/Export jobs</span></span>](../storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="dbbe0-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dbbe0-120">Next steps</span></span>

* [<span data-ttu-id="dbbe0-121">Depolama içeri/dışarı aktarma REST</span><span class="sxs-lookup"><span data-stu-id="dbbe0-121">Storage Import/Export REST</span></span>](/rest/api/storageimportexport)
