---
title: "Tüm Azure içeri/dışarı aktarma işleriniz listesi | MicrosoftDocs"
description: "Tüm bir Abonelikteki Azure içeri/dışarı aktarma hizmeti işlerini listelemek öğrenin."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f2e619be-1bbd-4a54-9472-9e2f70a83b64
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 1977bfc0e516088310f45ecdd960287eeed2c2d8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="enumerating-jobs-in-the-azure-importexport-service"></a><span data-ttu-id="829ab-103">Azure içeri/dışarı aktarma hizmeti işlerinde numaralandırma</span><span class="sxs-lookup"><span data-stu-id="829ab-103">Enumerating jobs in the Azure Import/Export service</span></span>
<span data-ttu-id="829ab-104">Bir Abonelikteki tüm işleri Numaralandırılacak çağrısı [listesi işleri](/rest/api/storageimportexport/jobs#Jobs_List) işlemi.</span><span class="sxs-lookup"><span data-stu-id="829ab-104">To enumerate all jobs in a subscription, call the [List Jobs](/rest/api/storageimportexport/jobs#Jobs_List) operation.</span></span> <span data-ttu-id="829ab-105">`List Jobs`işlerini ve bunun yanı sıra aşağıdaki öznitelikler listesi döndürür:</span><span class="sxs-lookup"><span data-stu-id="829ab-105">`List Jobs` returns a list of jobs as well as the following attributes:</span></span>

-   <span data-ttu-id="829ab-106">İşin (içeri veya dışarı) türü</span><span class="sxs-lookup"><span data-stu-id="829ab-106">The type of job (Import or Export)</span></span>

-   <span data-ttu-id="829ab-107">Geçerli iş durumu</span><span class="sxs-lookup"><span data-stu-id="829ab-107">The current job state</span></span>

-   <span data-ttu-id="829ab-108">İş depolama hesabını ilişkili</span><span class="sxs-lookup"><span data-stu-id="829ab-108">The job's associated storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="829ab-109">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="829ab-109">Next steps</span></span>

* [<span data-ttu-id="829ab-110">İçeri/dışarı aktarma hizmeti REST API'si kullanma</span><span class="sxs-lookup"><span data-stu-id="829ab-110">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
