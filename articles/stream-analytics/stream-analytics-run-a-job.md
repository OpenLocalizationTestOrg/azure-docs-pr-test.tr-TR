---
title: "Stream Analytics işleri akış aaaHow toostart | Microsoft Docs"
description: "İş akışında Azure Stream Analytics çalışma şeklini | yol kesimi öğrenme."
keywords: "Akış işi"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 67aa14860c38cbd0535d0ec4f23729445d0185c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a>Nasıl bir akış toorun iş Azure akış analizi
Bir iş girişi, sorgu ve çıktı tümü hello Stream Analytics işi başlatabilirsiniz belirtilmedi.

toostart işinizi:

1. Merhaba iş panosundan hello Klasik Azure Portalı'nda tıklatın **Başlat** hello sayfanın hello sonundaki.
   
   ![Başlangıç iş düğmesi](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   Hello Azure portal'ı tıklatın **Başlat** hello sayfanın üst kısmındaki, iş.
   
   ![Azure portal başlangıç işi düğmesi](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. Belirtin bir **Başlat çıktı** bu işi çıkış üretmeyi başlayacağını değeri toodetermine. Merhaba önceden başlatılmamış işleri için varsayılan ayar olan **iş başlangıç saati**, o hello iş başka bir deyişle, veriler işlenirken hemen başlar. Ayrıca belirtebilirsiniz bir **özel** hello zaman geçmiş (için geçmiş verileri tüketme) veya hello gelecekteki (gelecekteki bir süreye kadar işleme toodelay). Bir iş önceden başlatıldığında ve durdurulduğunda, durumları hello için seçenek **son durdurulma zamanı** sipariş tooresume hello hello son çıkış zamanı işten bulunur ve veri kaybını önlemek.  
   
   ![Zaman iş akışı Başlat](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Azure portal başlangıç akış işi zaman](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. Seçiminizi onaylayın. Merhaba iş durumu çok değiştirir*başlangıç* ve kısa süre içinde çok taşınır*çalıştıran* hello işi başladıktan sonra. Merhaba hello ilerlemesini izleyebilirsiniz **Başlat** hello işleminde **bildirim hub'ı**:
   
   ![Akış işi ilerleme durumu](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![İşin ilerleme durumunu akış azure portalı](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a>Yardım alın
Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

