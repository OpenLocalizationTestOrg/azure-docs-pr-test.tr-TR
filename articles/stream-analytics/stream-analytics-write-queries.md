---
title: Stream Analytics aaaHow toowrite sorgularda | Microsoft Docs
description: "Akış analizi ve sorgu veri sorguları yazma | yol kesimi öğrenme."
keywords: "nasıl toowrite sorgular, sorgu veri sorguları yazma, bir sorgu yazın"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b943c34f10afd2b21789afbd341c471a5f168729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowrite-queries-in-stream-analytics"></a>Toowrite Stream Analytics içinde nasıl sorgular
Akış işleme mantığı Azure akış analizi de sorgu yazma "bir iş başlatılır ve hello iş ulaştığında gibi verileri yürütülen önce tanımlı bir durumu sorgu" olarak uygulanır. Merhaba veri dönüştürme SQL benzeri bir sorgu dili ifade eklenen dil uzantıları gibi büyük ölçüde T-SQL bir alt bazı olduğu [Pencereleme](https://msdn.microsoft.com/library/azure/dn835019.aspx) tooexpress zamana bağlı semantiği kullanılır.

## <a name="writing-queries"></a>Sorgu yazma:
1. Hello Azure Yönetim Portalı'da, Stream Analytics işinde tıklatın **sorgu**.
   
    ![Seçme sorgusu](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    Hello Azure Portal'ı tıklatın **sorgu**.
   
    ![Sorgu Önizleme'yi seçin](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. Yeni işlerin başlamanıza yardımcı bir sorgu şablonu toohelp vardır. "geçiş" şablonu gerçekleştirir hello sorgu bu projeleri giriş olaylarını tüm alanları hello çıktı.  
   
   * İşiniz için en az bir giriş ve çıkış tanımladıysanız, giriş ve çıkış önce kullanmak istediğiniz hello hello diğer adları ile Merhaba yer tutucu "[YourOutputAlias]" ve "[YourInputAlias]" alanları değiştirebilirsiniz. Ayrıca, hala yazar ve sorgunuzu hello Klasik Azure portalı girişleri ve çıkışları hello işinde tanımlamadan test kullanabilirsiniz.
   * Daha fazla işlem daha basit bir geçiş diski tooperform isterseniz hello sorgu tanımı düzenleyebilirsiniz. Sorgu yazma ile başlatılan tooget ele desenleri yakalanır bazı yaygın sorgusu göz [burada](stream-analytics-stream-analytics-query-patterns.md).  
   
   ![Sorgu veri penceresi](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a>toovalidate sorgu verileri çalışma:
Sorgunuzu hello tarayıcıda test verileri içeren bir veya daha fazla yerel JSON dosyaları çalıştırarak beklendiği gibi davranır test edebilirsiniz. Bu hello iş başlatmaz veya herhangi fatura ödenmesi gerekebilir.

> [!NOTE]
> Şu anda tarayıcı içi sorgu testi hello Azure Portal desteklenmiyor.  
> 
> 

1. (Aksi halde hello Test düğmesi devre dışı bırakılır) hello sorguda herhangi bir hata olduğundan emin olun ve ardından hello Test düğmesine tıklayın.  
   
   ![Test verileri Sorgulama](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. İstendiğinde toospecify dosyaları her hello sorguda başvurulan hello girdi olacaktır. Bu örnekte, hello şablon sorgu olarak kaldığını-hello iletişim "yourinputalias" adlı bir giriş istemeden, olduğundan.  
   
   ![Test verileri sorgusu](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. Tooa test dosyasını bulun. Birkaç örnek dosyalarını kullanılabilir [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) ve kendi veri akışı girişlerini hello hello Giriş sekmesinde örnek verileri işlevi aracılığıyla gelen örnek veri alabilirsiniz.  
   
   ![Sorgu giriş](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. Merhaba iletişim kapattıktan sonra sorgunuzu hello test verileri çalışır ve hello sorgu sayfanın hello sonundaki hello sonuçları görürsünüz.  
   
   ![Sorgu özeti](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a>Yardım alın
Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

