---
title: "Azure Stream Analytics içinde AAA örnekleme girişleri | Microsoft Docs"
description: "Akış analizi işleri giderirken sorunları belirlemenize."
keywords: "Giriş, giriş örnekleme sorun giderme"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a>Azure Stream Analytics Giriş akışı örnekleme

Azure akış analizi kullanarak, bir dosyadan gelen ve sorguları toostart gerek kalmadan hello Portalı'nda test ya da bir işi durdurmak giriş olaylarını örnek oluşturabilirsiniz.

## <a name="testing-your-query"></a>Sorgunuz test etme

Merhaba Hello Stream Analytics işi Ayrıntılar bölmesinde, açmak **sorgu Düzenleyicisi'ni** hello sorgu adı altında dikey **sorgu**. (Hiçbir sorgu henüz oluşturulduğundan bizim örnek senaryoda hello tıklatın **< >** yer tutucu.)

![Merhaba Stream Analytics sorgu Düzenleyicisi](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

sorgunuzu oluşturmak için zengin bir düzenleyici dikey penceresinde hello hello önceki sürümünde olduğu gibi görüntülenir. Merhaba dikey yeni bir güncelleştirildi artık bu gösterir hello giriş ve hello sorgu tarafından kullanılan ve bu proje için tanımlanan çıkış sol bölme.

![Merhaba Stream Analytics sorgu Düzenleyicisi'ni girdilerin ve listeleri çıkarır](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

Ayrıca gösterilen bir ek giriş ve çıkış, tanımlanmamış'dır. İle başlayan hello yeni sorgu şablonu geliyor. Bunlar değiştirebilir veya hatta hello sorgu düzenlerken tamamen kaybolur. Bunları şu an için güvenle yoksayabilirsiniz.

Örnek giriş verilerle tootest girişlerinizi hiçbirini sağ tıklayın ve ardından **dosyasından örnek verileri yükleme**.

![Stream Analytics sorgu Düzenleyicisi'ni karşıya yükleme örnek veri dosyası komutundan hello](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

Merhaba karşıya yükleme tamamlandıktan sonra tıklayın **Test** tootest hello bu sorgusu örnek yalnızca sağlanan verileri.

![Merhaba Stream Analytics sorgu Düzenleyicisi'ni Test düğmesi](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

Daha sonra kullanmak üzere toosave hello test çıkışı istiyorsanız, sorgunuzu hello çıktısını hello tarayıcı bağlantı toohello indirme sonuçlarını ile görüntülenir. Artık kolayca ve yinelemeli olarak Sorgunuzu değiştirin ve tekrar tekrar hello çıkış nasıl değiştiğini toosee test.

![Stream Analytics sorgu Düzenleyicisi'ni örnek çıkış](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

Görüntü önceki hello içinde ikinci bir çıkış eklendi, adlı **HighAvgTempOutput**.

Sorguda birden çok çıkış kullandığınızda, ayrı ayrı her çıktı için hello sonuçları görmek ve kolayca aralarında geçiş.

Merhaba Sonuçlardan memnun kaldığınızda, sorgunuzu kaydedebilir, işinizi Başlat, arkanıza yaslanın ve akış analizi, hello Sihirli izleyin.

## <a name="get-help"></a>Yardım alın

Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)
