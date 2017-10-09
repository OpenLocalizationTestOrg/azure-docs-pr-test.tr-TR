---
title: "işlem ve hizmet günlükleri kullanarak Stream Analytics içinde aaaDebug | Microsoft Docs"
description: "Nasıl toouse Stream Analytics işlem günlükleri"
keywords: "Hizmet Günlükleri"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a2ed9676-f0bd-4398-87c8-a592779ac728
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: d3dd27706ccc879a724e1894b33d47021d972f31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a>Stream Analytics işleri hizmet ve işlem günlüklerini kullanarak hata ayıklama
Tüm Azure hizmetlerini tedarik işlem günlüğü iletileri toousers toorecord ayrıntıları toomanagement işlemleri ile ilgili. Hata ayıklama gibi zamana başlangıç tooprocessing toooutput iş durumu, işin ilerleme durumunu ve hata iletileri tootrack hello işinin ilerlemesini görüntülemek amacıyla bu bilgileri Azure Stream Analytics içinde kullanılabilir.

## <a name="find-operation-logs-in-hello-azure-management-portal"></a>Hello Azure Yönetim Portalı'nda işlem günlüklerini bulma
İşlem günlükleri iki yolla erişilebilir:  

* Merhaba Stream Analytics işi Panosu  
* Yönetim Hizmetleri hello Klasik Azure portalında  

## <a name="dashboard-of-hello-stream-analytics-job"></a>Merhaba Stream Analytics işi Panosu
Akış analizi işi günlüklerini karşılık gelen bir bağlantı toohello hello işin Pano sekmesinde görüntülenir. Bu bağlantıya tıklayın, belirli bir iş son günlükleri gösterir şekilde hello filtreleri ayarlarsınız.

  ![Yönetim Hizmetleri günlükleri seçin](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a>Yönetim Hizmetleri
toomanually akış analizi ve diğer hizmetleri hello Klasik Azure Portalı'nda toohello işlem günlükleri gidin:

1. Tıklayın **Yönetim Hizmetleri** hello içinde [Klasik Azure portalında](https://manage.windowsazure.com).
2. Seçin **Stream Analytics** için **türü** ve hello işi için hello adını **hizmet adı**.  
   
   ![Akış analizi seçin](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-hello-azure-portal"></a>Denetim günlüklerini hello Azure portal Bul
hello Azure portal, Stream Analytics işinde için işlem günlüklerini toofind tıklatın **Gözat** ve ardından **denetim günlüklerini**.

  ![Azure portal Stream Analytics seçin](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

Bu hello olaylarından tüm kaynaklar için son 7 gün aboneliğinizde gösteren dikey pencere açılır.  Merhaba tıklayarak toosee olayları belirtin tür ya da zaman çerçevesi filtreleyebilirsiniz **filtre** komutu.

  ![Azure portal Stream Analytics seçin](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a>Günlüğü ayrıntılarının alınması
İşiniz için zaman aralığını ve durum tooview hello günlükleri göre filtreleyebilirsiniz.

Üzerinde hello Hello Azure Yönetim Portalı'nda tıklatın **ayrıntıları** seçili olay hakkında daha fazla ayrıntı hello penceresi tooview hello altındaki düğme. 

  ![Ayrıntılarını seçin](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

Azure portal, bir günlük girişi toosee tıklatıldığında Hello içindeki ayrıntılı olayları hello.

  ![Azure portal ayrıntılarını seçin](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

Buradan, hello açabilirsiniz **ayrıntı** hello olayda dikey.

  ![Azure portal ayrıntılarını seçin](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a>Başarısız bir işi hata ayıklama
Hello Azure Yönetim Portalı'nda hello arama simgesine tıklayın ve 'başarısız' yazın. Bu, hataları olan tüm günlükleri sonucunu verir. 

  ![Başarısız bir işi hata ayıklama](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

Hello Azure portal, ileti tooview düzeyine göre filtreleyebilirsiniz **kritik** olaylar.

  ![Azure portal hata ayıklama](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

Merhaba hataları herhangi birini seçin ve üzerinde hello tıklatın **ayrıntıları** hello hata hakkında daha fazla bilgi için.  Bazı hata iletileri de nasıl toomitigate hello sorun hakkında bilgi sağlar. 

  ![İşlem ayrıntıları](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

Toocontact gerektiğinde [Destek](https://azure.microsoft.com/support/options/) ya da bilgi toohello takım hello aracılığıyla sağlayın [MSDN Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), hello işlem ayrıntıları, lütfen unutmayın, özellikle hello **bağıntı kimliği**. 

## <a name="get-help"></a>Yardım alın
Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

