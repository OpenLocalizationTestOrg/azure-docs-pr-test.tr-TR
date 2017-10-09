---
title: "aaaHow tooconfigure verilerin çıktısını alır, Stream Analytics işleri | Microsoft Docs"
description: "Çıkış akış analizi işleri için yapılandırma | yol kesimi öğrenme."
keywords: "Çıkış, verileri veri taşıma"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a>Nasıl Stream Analytics işleri tooconfigure verilerin çıktısını alır

Azure Stream Analytics işleri bağlı tooone veya bağlantı tooan mevcut veri havuzunu tanımlamak daha fazla veri çıkışlarını olabilir. Stream Analytics işiniz işler ve gelen verileri dönüştüren gibi veri çıkış olayları akışı tooyour iş çıktısı yazılır.

Stream Analytics veri çıkışları kullanılan toosource gerçek zamanlı panolar veya uyarıları, tetikleyici veri taşıma iş akışları veya toplu iş daha sonra işlemek için yalnızca arşiv verileri olabilir. Akış analizi birinci sınıf burada ayrıntılı şekilde belgelenen birkaç Azure hizmetleriyle tümleştirme vardır.

bir çıkış tooyour Stream Analytics işi tooadd:

1. Merhaba, [Azure portal](https://portal.azure.com), işinizi açın ve'ı tıklatın **çıkışları** ve ardından **Ekle** görünür hello çıkışları dikey penceresinde.
   
    ![Çıkış ekleme](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. Hello bu çıkış için bir kolay ad **çıkış diğer adları** kutusu. Bu ad, işin bir sorguyu daha sonra toorefer toohello çıkış kullanılabilir.  
   
    Gerekli hello bağlantı özelliklerini tooconnect tooyour Çıktı Hello kalan doldurun.  Bu alanlar çıktı türüne göre değişir ve burada ayrıntılı olarak tanımlanır.  
   
    ![Veri taşıma türü seçin](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. Merhaba çıktı türüne bağlı olarak nasıl hello veri seri hale getirilmiş biçimlendirilmiş veya toospecify gerekebilir. Her çıktı türü için Hello belirli serileştirme ayarlarını aşağıda belirtilmiştir.
   
    Merhaba gerekli bağlantı özelliklerini tooconnect tooyour veri kaynağının Hello kalan doldurun. Bu alanlar giriş ve kaynak türü türüne göre değişir ve ayrıntılı hello olarak tanımlanan [işi oluştur makale](stream-analytics-create-a-job.md).  

> [!Note]
>
> Tüm çıktı öğesi eklenen toohello işleri hello iş başlatıldı ve akan olayları başlatmak için önce bulunmalıdır. Blob Depolama çıkış olarak kullanırsanız, örneğin, hello iş bir depolama hesabı otomatik olarak oluşturmaz. Merhaba ASA işi başlatılmadan önce hello kullanıcı tarafından oluşturulan toobe gerekir.
> 
 

## <a name="get-help"></a>Yardım alın
Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

