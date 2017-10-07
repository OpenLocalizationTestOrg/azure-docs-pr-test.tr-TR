---
title: Azure Stream Analytics aaaDebug sorgular SELECT INTO kullanarak | Microsoft Docs
description: "Örnek veri Orta sorgu SELECT INTO deyimleri akış analizi kullanarak"
keywords: 
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
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a>Sorgular SELECT INTO deyimleri kullanarak hata ayıklama

Gerçek zamanlı veri işleme, hangi hello verilerin bilerek hello Hello ortadaki sorgu yararlı olabilir görülüyor. Giriş veya bir Azure akış analizi işi adımlardan birden çok kez okunabilir olduğundan, ek SELECT INTO deyimleri yazabilirsiniz. Bunun yapılması ara veri depolama alanına çıkarır ve gibi hello veri hello doğruluğunu incelemek olanak tanır *izlemek değişkenleri* yapın, hata ayıklama bir program.

## <a name="use-select-into-toocheck-hello-data-stream"></a>SELECT INTO toocheck hello veri akışını kullan

Merhaba bir Azure akış analizi işi aşağıdaki örnek sorguda bir akış girişi, iki başvuru verileri girdi ve çıktı tooAzure Table Storage sahiptir. Merhaba sorgu hello olay hub'ı ve adı ve kategori iki başvuru BLOB'lar tooget hello bilgileri verileri birleştirir:

![SELECT INTO örnek sorgu](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

Merhaba işi çalışıyor, ancak hello çıktıda hiçbir olay üretilen unutmayın. Merhaba üzerinde **izleme** hello girişi veri oluşturan, ancak Merhaba, hangi adımın tanımadığınız görebilirsiniz burada gösterilen kutucuğu **katılma** nedeniyle tüm hello bırakılan olayları toobe.

![Merhaba izleme kutucuğu](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
Bu durumda, birkaç ek SELECT INTO deyimleri çok "Merhaba Ara birleştirme sonuçlarının ve hello girdiden okunan hello veri oturum" ekleyebilirsiniz.

Bu örnekte, iki yeni "geçici çıkış verir." ekledik Bunlar, istediğiniz herhangi bir havuz olabilir. Burada size Azure Storage örnek olarak kullanın:

![Ek SELECT INTO deyimleri ekleme](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

Ardından hello sorgu şöyle yazabilirsiniz:

![SELECT INTO yeniden sorgu](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

Şimdi hello işi yeniden başlatın ve birkaç dakika çalışmasına olanak tanır. Ardından temp1 ve temp2 tabloları izleyerek Visual Studio Cloud Explorer tooproduce hello sorgu:

**temp1 tablo**
![SELECT INTO temp1 tablosu](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)

**temp2 tablo**
![SELECT INTO temp2 tablosu](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)

Gördüğünüz gibi temp1 ve temp2 veriniz varsa ve hello ad sütunu doğru temp2 doldurulur. Ancak, hala hiçbir veri çıkışı, çünkü bir şeyler yanlış:

![SELECT INTO output1 tablosuyla veri yok](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

Hello veri örnekleme tarafından hello sorunu hello ile neredeyse emin olabilirsiniz ikinci birleştirme. Merhaba blobundan hello başvuru verileri indirin ve göz atın:

![SELECT INTO başvuru tablosu](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

Gördüğünüz gibi bu başvuru verileri hello GUID hello biçimi hello hello [sütundan] temp2 biçimlerinin farklıdır. İşte bu nedenle hello veri beklendiği gibi output1 içinde gelmesini alamadık.

Merhaba veri biçimi düzeltin, tooreference blob karşıya yükleme ve yeniden deneyin:

![SELECT INTO geçici tablo](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

Bu süre hello çıktı hello verileri biçimlendirilmiş ve beklendiği gibi doldurulur.

![SELECT INTO son tablo](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a>Yardım alın

Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Sonraki adımlar

* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

