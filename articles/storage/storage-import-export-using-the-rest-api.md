---
title: "Azure içeri/dışarı aktarma hizmeti REST API kullanarak | Microsoft Docs"
description: "Azure içeri/dışarı aktarma hizmeti REST API'si, nasıl yapılır ve başvuru malzeme dahil olmak üzere kullanmak için kaynakların nerede bulacağını öğrenin."
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
ms.openlocfilehash: e4f5ca289f4bd87574e448d37a1154b222f221f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-importexport-service-rest-api"></a><span data-ttu-id="bce4f-103">Azure İçeri/Dışarı Aktarma hizmeti REST API’sini kullanma</span><span class="sxs-lookup"><span data-stu-id="bce4f-103">Using the Azure Import/Export service REST API</span></span>

<span data-ttu-id="bce4f-104">Microsoft Azure içeri/dışarı aktarma hizmetini içeri/dışarı aktarma işleri programsal denetimi etkinleştirmek için bir REST API gösterir.</span><span class="sxs-lookup"><span data-stu-id="bce4f-104">The Microsoft Azure Import/Export service exposes a REST API to enable programmatic control of import/export jobs.</span></span> <span data-ttu-id="bce4f-105">REST API tüm ile gerçekleştirebileceğiniz içeri/dışarı aktarma işlemlerini gerçekleştirmek için kullanabileceğiniz [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bce4f-105">You can use the REST API to perform all of the import/export operations that you can perform with the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="bce4f-106">Ayrıca, REST API Klasik portalda şu anda kullanılabilir olmayan bir işin tamamlanma sorgulama gibi bazı ayrıntılı işlemleri gerçekleştirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bce4f-106">Additionally, you can use the REST API to perform certain granular operations, such as querying the percentage completion of a job, which are not currently available in the classic portal.</span></span>

<span data-ttu-id="bce4f-107">Bkz: [Blob depolama alanına veri aktarmak için Microsoft Azure içeri/dışarı aktarma hizmeti kullanılarak](storage-import-export-service.md) içeri/dışarı aktarma hizmeti ve klasik Portalı'nı oluşturmak ve içeri aktarma yönetmek ve işleri dışarı aktarmak için nasıl kullanılacağını gösteren bir eğitim genel bakış.</span><span class="sxs-lookup"><span data-stu-id="bce4f-107">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the classic portal to create and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="bce4f-108">Hizmet uç noktaları</span><span class="sxs-lookup"><span data-stu-id="bce4f-108">Service endpoints</span></span>

<span data-ttu-id="bce4f-109">Azure içeri/dışarı aktarma hizmeti kaynak sağlayıcısı için Azure Resource Manager ve içeri/dışarı aktarma işleri yönetmek için bir REST API kümesi aşağıdaki HTTPS uç noktada sağlar:</span><span class="sxs-lookup"><span data-stu-id="bce4f-109">The Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at the following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="bce4f-110">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="bce4f-110">Versioning</span></span>

<span data-ttu-id="bce4f-111">İçeri/dışarı aktarma hizmeti isteklerine belirtmelisiniz `api-version` parametresi ve değeri ayarlayın `2016-11-01`.</span><span class="sxs-lookup"><span data-stu-id="bce4f-111">Requests to the Import/Export service must specify the `api-version` parameter and set its value to `2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="bce4f-112">İçeri/dışarı aktarma hizmeti işlemleri</span><span class="sxs-lookup"><span data-stu-id="bce4f-112">Import/Export service operations</span></span>

[<span data-ttu-id="bce4f-113">İçeri aktarma işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="bce4f-113">Creating an import job</span></span>](storage-import-export-creating-an-import-job.md)

[<span data-ttu-id="bce4f-114">Dışarı aktarma işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="bce4f-114">Creating an export job</span></span>](storage-import-export-creating-an-export-job.md)

[<span data-ttu-id="bce4f-115">Bir iş için durum bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="bce4f-115">Retrieving state information for a job</span></span>](storage-import-export-retrieving-state-info-for-a-job.md)

[<span data-ttu-id="bce4f-116">İşleri numaralandırma</span><span class="sxs-lookup"><span data-stu-id="bce4f-116">Enumerating jobs</span></span>](storage-import-export-enumerating-jobs.md)

[<span data-ttu-id="bce4f-117">İşleri iptal etme ve silme</span><span class="sxs-lookup"><span data-stu-id="bce4f-117">Cancelling and deleting jobs</span></span>](storage-import-export-cancelling-and-deleting-jobs.md)

[<span data-ttu-id="bce4f-118">Yedekleme sürücü bildirimleri</span><span class="sxs-lookup"><span data-stu-id="bce4f-118">Backing Up drive manifests</span></span>](storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="bce4f-119">İçeri/Dışarı Aktarma işleri için tanılama ve hata kurtarma</span><span class="sxs-lookup"><span data-stu-id="bce4f-119">Diagnostics and error recovery for Import/Export jobs</span></span>](storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="bce4f-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bce4f-120">Next steps</span></span>

* [<span data-ttu-id="bce4f-121">Depolama içeri/dışarı aktarma REST</span><span class="sxs-lookup"><span data-stu-id="bce4f-121">Storage Import/Export REST</span></span>](/rest/api/storageimportexport)
