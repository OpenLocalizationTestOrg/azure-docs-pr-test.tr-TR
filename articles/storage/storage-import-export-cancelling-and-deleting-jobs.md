---
title: "aaaCancel ve bir Azure içeri/dışarı aktarma işini silmek | Microsoft Docs"
description: "Nasıl toocancel ve delete işleri Merhaba Microsoft Azure içeri/dışarı aktarma hizmeti hakkında bilgi edinin."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 5d2aba510dafd0ca9a10f5643f721e7059a6a8f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="c2a15-103">İptal etme ve Azure içeri/dışarı aktarma işleri siliniyor</span><span class="sxs-lookup"><span data-stu-id="c2a15-103">Canceling and deleting Azure Import/Export jobs</span></span>

<span data-ttu-id="c2a15-104">Hello önce bir işi iptal edilecek istek `Packaging` arama hello tarafından durum [güncelleştirme işi özellikleri](/rest/api/storageimportexport/jobs#Jobs_Update) işlemi ve ayarı hello `CancelRequested` öğesi çok`true`.</span><span class="sxs-lookup"><span data-stu-id="c2a15-104">You can request that a job be cancelled before it is in hello `Packaging` state by calling hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and setting hello `CancelRequested` element too`true`.</span></span> <span data-ttu-id="c2a15-105">en iyi çaba ilkesine göre Hello işleri iptal edilir.</span><span class="sxs-lookup"><span data-stu-id="c2a15-105">hello job will be cancelled on a best-effort basis.</span></span> <span data-ttu-id="c2a15-106">Veri aktarma hello işleminde sürücüleri varsa veri iptal talep edilen sonra aktarılan toobe devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="c2a15-106">If drives are in hello process of transferring data, data may continue toobe transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="c2a15-107">İşi iptal edildi toohello taşınır `Completed` belirtin ve 90 gün boyunca, bu noktada silinecektir tutulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c2a15-107">A cancelled job will move toohello `Completed` state and be kept for 90 days, at which point it will be deleted.</span></span>

 <span data-ttu-id="c2a15-108">toodelete bir işi çağrısı hello [iş Sil](/rest/api/storageimportexport/jobs#Jobs_Delete) hello işi sevk edilmiş önce işlemi (*yani*, hello iş hello olsa `Creating` durumu).</span><span class="sxs-lookup"><span data-stu-id="c2a15-108">toodelete a job, call hello [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before hello job has shipped (*i.e.*, while hello job is in hello `Creating` state).</span></span> <span data-ttu-id="c2a15-109">Hello olduğunda bir iş ayrıca silebilirsiniz `Completed` durumu.</span><span class="sxs-lookup"><span data-stu-id="c2a15-109">You can also delete a job when it is in hello `Completed` state.</span></span> <span data-ttu-id="c2a15-110">Bir işi silindikten sonra kendi bilgilerini ve durumunu artık hello REST API erişilebilir veya Azure portal hello.</span><span class="sxs-lookup"><span data-stu-id="c2a15-110">After a job has been deleted, its information and status are no longer accessible via hello REST API or hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2a15-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c2a15-111">Next steps</span></span>

* [<span data-ttu-id="c2a15-112">Merhaba içeri/dışarı aktarma hizmeti REST API'si kullanma</span><span class="sxs-lookup"><span data-stu-id="c2a15-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
