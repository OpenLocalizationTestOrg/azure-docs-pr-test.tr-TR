---
title: "Azure Stream Analytics sorgu SELECT INTO kullanarak hata ayıklama | Microsoft Docs"
description: "Örnek veri Orta sorgu SELECT INTO deyimleri akış analizi kullanarak"
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: samacha
ms.openlocfilehash: 6ffa756eef0cfa44d7dd397e43afbf054ac2df7a
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a>Sorgular SELECT INTO deyimleri kullanarak hata ayıklama

Gerçek zamanlı veri işleme, verileri nasıl ortasında sorgu göründüğünü bilerek yararlı olabilir. Giriş veya bir Azure akış analizi işi adımlardan birden çok kez okunabilir olduğundan, ek SELECT INTO deyimleri yazabilirsiniz. Bunun yapılması ara veri depolama alanına çıkarır ve gibi veri doğruluğunu incelemek olanak tanır *izlemek değişkenleri* yapın, hata ayıklama bir program.

## <a name="use-select-into-to-check-the-data-stream"></a>SELECT INTO veri akışını denetlemek için kullanın:

Bir Azure akış analizi işi aşağıdaki örnek sorguda bir akış girişi, iki başvuru verileri girdi ve çıktı Azure tablo depolaması sahiptir. Sorgu adı ve kategori bilgilerini almak için iki başvuru BLOB'ları ve olay hub'ı verileri birleştirir:

![SELECT INTO örnek sorgu](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

İş çalışıyor, ancak çıktıda hiçbir olay üretilen unutmayın. Üzerinde **izleme** kutucuğu, burada, veriler girişi oluşturan, ancak hangi adımında tanımadığınız görebilirsiniz gösterilen **katılma** tüm olayları bırakılmasına neden oldu.

![İzleme kutucuğu](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
Bu durumda, "Ara birleştirme sonuçlarının ve girdiden okunan verileri günlüğe kaydetmek için" birkaç ek SELECT INTO deyimleri ekleyebilirsiniz.

Bu örnekte, iki yeni "geçici çıkış verir." ekledik Bunlar, istediğiniz herhangi bir havuz olabilir. Burada size Azure Storage örnek olarak kullanın:

![Ek SELECT INTO deyimleri ekleme](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

Ardından, sorgu şöyle yazabilirsiniz:

![SELECT INTO yeniden sorgu](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

Şimdi işi yeniden başlatın ve birkaç dakika çalışmasına olanak tanır. Ardından sorgu temp1 ve Visual Studio bulut aşağıdaki tablolarda üretmek için Gezgini ile temp2:

**temp1 tablo**
![SELECT INTO temp1 tablosu](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)

**temp2 tablo**
![SELECT INTO temp2 tablosu](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)

Gördüğünüz gibi temp1 ve temp2 veriniz varsa ve ad sütunu doğru temp2 doldurulur. Ancak, hala hiçbir veri çıkışı, çünkü bir şeyler yanlış:

![SELECT INTO output1 tablosuyla veri yok](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

Veri örnekleme tarafından sorunu ikinci birleşim ile neredeyse emin olabilirsiniz. Başvuru verileri blob üzerinden yükleyin ve bir göz atın:

![SELECT INTO başvuru tablosu](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

Gördüğünüz gibi bu başvuru verilerinde GUID biçimi biçimden farklı [sütundan] temp2. İşte bu nedenle veri output1 içinde beklendiği gibi ulaşmasını alamadık.

Veri biçimi düzeltin, blob başvurusu ve yeniden denemek için bunu yükleyin:

![SELECT INTO geçici tablo](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

Bu süre, veri çıkışı biçimlendirilmiş ve beklendiği gibi doldurulur.

![SELECT INTO son tablo](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a>Yardım alın

Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Sonraki adımlar

* [Azure Stream Analytics'e giriş](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

