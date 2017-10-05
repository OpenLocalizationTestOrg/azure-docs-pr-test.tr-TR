---
title: "İptal etmek ve bir Azure içeri/dışarı aktarma işini silmek | Microsoft Docs"
description: "İptal etmek ve Microsoft Azure içeri/dışarı aktarma hizmeti için silme hakkında bilgi edinin."
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
ms.openlocfilehash: 1e989c72fc03697bf6d2e515ff53003703665d1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="05da5-103">İptal etme ve Azure içeri/dışarı aktarma işleri siliniyor</span><span class="sxs-lookup"><span data-stu-id="05da5-103">Canceling and deleting Azure Import/Export jobs</span></span>

 <span data-ttu-id="05da5-104">Bir işi olarak önce iptal istemek için `Packaging` durum, çağrı [güncelleştirme işi özellikleri](/rest/api/storageimportexport/jobs#Jobs_Update) işlemi ve kümesi `CancelRequested` öğesine `true`.</span><span class="sxs-lookup"><span data-stu-id="05da5-104">To request that a job be canceled before it is in the `Packaging` state, call the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and set the `CancelRequested` element to `true`.</span></span> <span data-ttu-id="05da5-105">En iyi çaba ilkesine göre işleri iptal edilir.</span><span class="sxs-lookup"><span data-stu-id="05da5-105">The job is canceled on a best-effort basis.</span></span> <span data-ttu-id="05da5-106">Veri aktarma işlemi yapıyor sürücülerdir, veri iptal talep edilen sonra aktarılacak devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="05da5-106">If drives are in the process of transferring data, data may continue to be transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="05da5-107">İptal edilen işi taşınır `Completed` durum ve 90 gün boyunca, bu noktada, silindiğinden tutulur.</span><span class="sxs-lookup"><span data-stu-id="05da5-107">A canceled job is moved to the `Completed` state and is kept for 90 days, at which point it is deleted.</span></span>

 <span data-ttu-id="05da5-108">Bir işi silmek için arama [iş Sil](/rest/api/storageimportexport/jobs#Jobs_Delete) iş sevk edilmiş önce işlemi (diğer bir deyişle, iş, aktarılırken `Creating` durumu).</span><span class="sxs-lookup"><span data-stu-id="05da5-108">To delete a job, call the [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before the job has shipped (that is, while the job is in the `Creating` state).</span></span> <span data-ttu-id="05da5-109">İçinde olduğunda bir iş ayrıca silebilirsiniz `Completed` durumu.</span><span class="sxs-lookup"><span data-stu-id="05da5-109">You can also delete a job when it is in the `Completed` state.</span></span> <span data-ttu-id="05da5-110">Bir işi silindikten sonra kendi bilgilerini ve durumunu artık REST API veya Azure portalı erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="05da5-110">After a job is deleted, its information and status are no longer accessible via the REST API or the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05da5-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="05da5-111">Next steps</span></span>

* [<span data-ttu-id="05da5-112">İçeri/dışarı aktarma hizmeti REST API'si kullanma</span><span class="sxs-lookup"><span data-stu-id="05da5-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
