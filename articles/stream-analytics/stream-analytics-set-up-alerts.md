---
title: "Stream Analytics sorguları için uyarılar aaaSet | Microsoft Docs"
description: "Uyarı anlama akış analizi"
keywords: "Uyarıları ayarlayın"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/26/2017
ms.author: jeffstok
ms.openlocfilehash: 7b1d90d1468311186567c8518e0283ea6b88c3f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a>Azure Stream Analytics işleri için uyarıları ayarlama
## <a name="introduction-monitor-page"></a>Giriş: İzleme sayfası
Ölçüm belirttiğiniz bir koşul ulaştığında bir uyarı uyarılar tootrigger ayarlayabilirsiniz. Örneğin, bir uyarı için bir koşul hello aşağıdaki gibi ayarlayabilirsiniz:

`If there are zero input events in hello last 5 minutes, send email notification toosa-admin@example.com`

Kuralları hello portal üzerinden ölçümleri üzerinde ayarlanabilir veya yapılandırılabilir [program aracılığıyla](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) işlem günlükleri veriler üzerinde.

## <a name="set-up-alerts-in-hello-azure-portal"></a>Hello Azure portal'te uyarıları ayarlama
1. Hello Azure portal, hello Stream Analytics işi için bir uyarı toocreate istediğiniz açın. 

2. Merhaba, **iş** dikey penceresinde hello tıklatın **izleme** bölümü.  

3. Merhaba, **ölçüm** dikey penceresinde hello tıklatın **uyarı Ekle** komutu.

      ![Azure portal Kurulumu](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. Bir ad ve açıklama girin.

5. Merhaba seçiciler toodefine hello koşul altında hangi hello uyarı gönderilir kullanın.

6. Merhaba uyarı nereye hakkında bilgi sağlar.

      ![Bir Azure akış analizi işi için bir uyarı ayarlama](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

Uyarıları hello Azure portal yapılandırma hakkında daha ayrıntılı bilgi için bkz: [uyarı bildirimleri alma](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).  


## <a name="get-help"></a>Yardım alın
Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-get-started.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

