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
ms.openlocfilehash: 13456a8e7652850baacb53730cc7bb1520b0a4c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="a867b-103">İptal etme ve Azure içeri/dışarı aktarma işleri siliniyor</span><span class="sxs-lookup"><span data-stu-id="a867b-103">Canceling and deleting Azure Import/Export jobs</span></span>

 <span data-ttu-id="a867b-104">daha önce bir işi iptal toorequest olan hello `Packaging` durum, çağrı hello [güncelleştirme işi özellikleri](/rest/api/storageimportexport/jobs#Jobs_Update) işlemi ve kümesi hello `CancelRequested` öğesi çok`true`.</span><span class="sxs-lookup"><span data-stu-id="a867b-104">toorequest that a job be canceled before it is in hello `Packaging` state, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and set hello `CancelRequested` element too`true`.</span></span> <span data-ttu-id="a867b-105">en iyi çaba ilkesine göre Hello işleri iptal edilir.</span><span class="sxs-lookup"><span data-stu-id="a867b-105">hello job is canceled on a best-effort basis.</span></span> <span data-ttu-id="a867b-106">Veri aktarma hello işleminde sürücüleri varsa veri iptal talep edilen sonra aktarılan toobe devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="a867b-106">If drives are in hello process of transferring data, data may continue toobe transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="a867b-107">Taşınan toohello iptal edilmiş iş `Completed` durum ve 90 gün boyunca, bu noktada, silindiğinden tutulur.</span><span class="sxs-lookup"><span data-stu-id="a867b-107">A canceled job is moved toohello `Completed` state and is kept for 90 days, at which point it is deleted.</span></span>

 <span data-ttu-id="a867b-108">toodelete bir işi çağrısı hello [iş Sil](/rest/api/storageimportexport/jobs#Jobs_Delete) hello işi sevk edilmiş önce işlemi (diğer bir deyişle, hello iş hello ederken `Creating` durumu).</span><span class="sxs-lookup"><span data-stu-id="a867b-108">toodelete a job, call hello [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before hello job has shipped (that is, while hello job is in hello `Creating` state).</span></span> <span data-ttu-id="a867b-109">Hello olduğunda bir iş ayrıca silebilirsiniz `Completed` durumu.</span><span class="sxs-lookup"><span data-stu-id="a867b-109">You can also delete a job when it is in hello `Completed` state.</span></span> <span data-ttu-id="a867b-110">Bir işi silindikten sonra kendi bilgilerini ve durumunu artık hello REST API erişilebilir veya Azure portal hello.</span><span class="sxs-lookup"><span data-stu-id="a867b-110">After a job is deleted, its information and status are no longer accessible via hello REST API or hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a867b-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a867b-111">Next steps</span></span>

* [<span data-ttu-id="a867b-112">Merhaba içeri/dışarı aktarma hizmeti REST API'si kullanma</span><span class="sxs-lookup"><span data-stu-id="a867b-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
