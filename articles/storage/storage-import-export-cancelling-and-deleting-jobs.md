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
# <a name="canceling-and-deleting-azure-importexport-jobs"></a>İptal etme ve Azure içeri/dışarı aktarma işleri siliniyor

Hello önce bir işi iptal edilecek istek `Packaging` arama hello tarafından durum [güncelleştirme işi özellikleri](/rest/api/storageimportexport/jobs#Jobs_Update) işlemi ve ayarı hello `CancelRequested` öğesi çok`true`. en iyi çaba ilkesine göre Hello işleri iptal edilir. Veri aktarma hello işleminde sürücüleri varsa veri iptal talep edilen sonra aktarılan toobe devam edebilir.

 İşi iptal edildi toohello taşınır `Completed` belirtin ve 90 gün boyunca, bu noktada silinecektir tutulmalıdır.

 toodelete bir işi çağrısı hello [iş Sil](/rest/api/storageimportexport/jobs#Jobs_Delete) hello işi sevk edilmiş önce işlemi (*yani*, hello iş hello olsa `Creating` durumu). Hello olduğunda bir iş ayrıca silebilirsiniz `Completed` durumu. Bir işi silindikten sonra kendi bilgilerini ve durumunu artık hello REST API erişilebilir veya Azure portal hello.

## <a name="next-steps"></a>Sonraki adımlar

* [Merhaba içeri/dışarı aktarma hizmeti REST API'si kullanma](storage-import-export-using-the-rest-api.md)
