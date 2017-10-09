---
title: "Akış analizi için bir veri analizi işleme işi aaaHow toocreate | Microsoft Docs"
description: "Akış analizi için veri analizi işlem işi oluşturma | yol kesimi öğrenme."
keywords: "veri analizi işleme"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: d4a3c89d8862d59688d06a1719b063efa2ab1c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a>Nasıl toocreate veri analizi işleme iş akış analizi için
Merhaba en üst düzey Azure akış analizi, akış analizi işi kaynaktır.  Aşağıdakilerden birini oluşur veya daha fazla veri kaynakları, hello veri dönüştürme ifade bir sorgu ve sonuçları yazılan bir veya daha fazla çıkış hedefleri giriş. Bunlar birlikte hello kullanıcı tooperform veri analizi için veri akışı işleme senaryolarına etkinleştirin.

Akış analizi kullanarak toostart yeni bir akış analizi işi oluşturarak başlayın.  Merhaba İş başlayana kadar bu eylem hiçbir fatura şifrelemelerini unutmayın.

1. Çevrimiçi Hello üzerinde oturum [Klasik Azure portalı](http://manage.windowsazure.com) veya hello [Azure portal](https://portal.azure.com/).
2. Merhaba portalında: **Yeni'yi**, ardından **Veri Hizmetleri** veya **veri analizi** portal ve ardından bağlı olarak **Azure akış analizi** veya **akış analizi** ve ardından **hızlı Oluştur**.
   
   ![Veri analizi işleme işi Sihirbazı](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![İş işleme veri analizi oluşturma](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. Merhaba hello Stream Analytics işi için istenen yapılandırmayı belirtin.
   
   * Merhaba, **iş adı** kutusunda, bir ad tooidentify hello akış analizi işi'ni girin. Ne zaman hello **iş adı** doğrulandı, hello iş adı kutusunda yeşil bir onay işareti görünür. Merhaba **iş adı** yalnızca alfasayısal karakterler ve hello içerebilir '-' karakteri ve 3 ile 63 karakter arasında olmalıdır.
   * Kullanım **bölge** hello Azure portal'ın veya **konumu** hello Azure portal toospecify hello toorun hello iş coğrafi konumu.
   * Azure portal kullanarak Merhaba, seçin veya bir depolama hesabı toouse hello olarak oluşturun **bölgesel izleme depolama hesabı**. Bu bölgede çalıştıran tüm Stream Analytics işleri için veri izleme kullanılan toostore bu depolama hesabıdır.
   * Azure portal kullanarak Merhaba, yeni bir belirtin veya varolan **kaynak grubu** toohold ilgili uygulamanız için kaynakları.
4. Merhaba yeni akış analizi işi seçenekleri yapılandırıldıktan sonra tıklatın **Stream Analytics işi oluşturmak**. Oluşturulan hello Stream Analytics işi toobe birkaç dakika sürebilir. toocheck hello durum hello bildirimler hub'ındaki hello ilerlemesini izleyebilirsiniz.
   
   ![Veri analizi işleme iş bildirimler hub'ı](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Azure portal veri analitik işleme işi oluştur işi](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. Merhaba yeni iş durumunu gösterir **oluşturulan**. Bu hello fark **Başlat** düğmesi devre dışıdır. Merhaba işi başlatmadan önce hello iş girişi, sorgu ve çıktı yapılandırın.
   
   ![Veri analizi işleme iş durumu](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Azure portal veri analitik iş durumunu işleme](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a>Yardım alın
Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

