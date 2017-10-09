---
title: "aaaTroubleshoot performans sorunları ve veritabanınızı en iyi duruma getirme | Microsoft Docs"
description: "Performans önerileri tooyour SQL veritabanı yanı sıra Temizle toogain performansınızla ilgili bilgiler hello sorguları veritabanına karşı çalıştırma performansını nasıl hello Uygula"
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: e948d30ac74eecf45420d5d77ef55e3c0b6f3f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a>Performans sorunlarını gidermek ve veritabanınızı en iyi duruma getirme

Veritabanı performansının düşük olmasına yol açan yaygın nedenler, dizinlerin eksik olması ve sorguların hatalı bir şekilde iyileştirilmesidir. Bu öğreticide, öğrenin:
> [!div class="checklist"]
> * Gözden geçirin, uygulayın ve performans geliştirme önerileri geri
> * Yüksek kaynak kullanımı sorgularıyla Bul
> * Uzun süre çalışan sorgular Bul

> Performans sorunlarını – örneğin tooreceive bir öneri dizin eksik olan bir veritabanı üzerinde sürekli bir iş yükü gerekir.
>

## <a name="log-in-toohello-azure-portal"></a>Toohello Azure portalında oturum açın

İçinde toohello oturum [Azure portal](https://portal.azure.com/).

## <a name="review-and-apply-a-recommendation"></a>Gözden geçirin ve öneri uygulayın

Bu adımları tooapply bir öneri, veritabanınız için hello sisteminden izleyin:

1. Merhaba tıklatın **performans önerileri** hello veritabanı Dikey Menüde.

    ![Performans önerisi](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. Öneriler Hello listeden etkin bir öneri seçin. Bu örnekte, dizin oluştur.

    ![öneri seçin](./media/sql-database-performance-tutorial/create_index.png)

3. Merhaba tıklayarak Hello öneriyi uygulamak **Uygula** düğmesi. İsteğe bağlı olarak, hello öneri ayrıntılarını gözden geçirin ve çok tıklayarak yürütülebilir hello T-SQL betiği bkz **betiği görüntüle** düğmesi.

    ![öneriyi](./media/sql-database-performance-tutorial/apply.png)

4. [İsteğe bağlı] Otomatik olarak uygulanan önerileri toobe için otomatik olarak ayarlamayı etkinleştirin.

    ![otomatik olarak ayarlama](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a>Bir öneri geri

Merhaba veritabanı Danışmanı uygulanan her bir öneri izler. Otomatik olarak bir öneri hello iş yükünü artırmak değil ise döndürülecek. El ile bir öneri dönme mümkün olsa da çoğu durumda şart değildir. toorevert bir öneri:

1. Toohello performans önerileri menü gidin ve uygulanan hello önerileri birini seçin.

    ![öneri seçin](./media/sql-database-performance-tutorial/select.png)

2. Merhaba Ayrıntıları Görüntüle'yi tıklatın **Revert**.

    ![öneri geri](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a>Merhaba tüketir hello sorgu çoğu kaynakları bulun

Merhaba tüketen bu adımları toofind hello sorgu en fazla kaynak izleyin:

1. Tıklatın hello üzerinde **sorgu performansı öngörüleri** hello veritabanı Dikey Menüde.

    ![Sorgu öngörüleri](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. Bir kaynak türü seçin.

    ![Sorgu öngörüleri](./media/sql-database-performance-tutorial/select_resource_type.png)

3. Merhaba ilk sorgu hello tablosunda seçin.

    ![Sorgu öngörüleri](./media/sql-database-performance-tutorial/select_query.png)

4. Merhaba sorgu ayrıntılarını gözden geçirin.

    ![Sorgu öngörüleri](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a>Merhaba uzun çalışan sorgu Bul

1. TooQuery performansı öngörüleri gidin ve seçin hello **uzun süre çalışan sorgular** sekmesi.

    ![Sorgu öngörüleri](./media/sql-database-performance-tutorial/long_running.png)

3. Merhaba ilk sorgu hello tablosunda seçin.

    ![Sorgu öngörüleri](./media/sql-database-performance-tutorial/select_first_query.png)

4. Merhaba sorgu ayrıntılarını gözden geçirin.

    ![Sorgu öngörüleri](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a>Sonraki adımlar 
Veritabanı performansının düşük olmasına yol açan yaygın nedenler, dizinlerin eksik olması ve sorguların hatalı bir şekilde iyileştirilmesidir. Bu öğreticide için öğrenilen:
> [!div class="checklist"]
> * Gözden geçirin, uygulayın ve performans geliştirme önerileri geri
> * Yüksek kaynak kullanımı sorgularıyla Bul
> * Uzun süre çalışan sorgular Bul

[SQL veritabanı performans ayarlama ipuçları](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
