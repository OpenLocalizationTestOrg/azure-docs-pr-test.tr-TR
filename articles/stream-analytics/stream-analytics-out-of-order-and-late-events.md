---
title: "aaaHandling olayı sırası ve Azure akış Analizi ile lateness | Microsoft Docs"
description: "Stream Analytics veri akışında düzen dışı ya da geç olaylarla işleyişi hakkında bilgi edinin."
keywords: "bozuk, geç, olayları"
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
ms.openlocfilehash: 87c028662fbafbf4f72f57f215d017f65bb649f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-event-order-handling"></a>Azure Stream Analytics olay sipariş işleme

Olayları bir zamana bağlı veri akışında her olay kaydedilir hello süresiyle bu hello olayı aldı. Bazı koşullar toooccasionally alma olay akışları bazı olaylar gönderildikleri farklı bir sırada neden olabilir. Basit bir TCP'nin veya bile bir saat eğriltme cihaz ve olay hub'ı alma hello gönderme hello arasındaki bu toooccur neden olabilir. "Noktalama" olaylar ayrıca eklenir tooreceived olay akışları, olay varış hello yokluğu tooadvance hello süre. Bunlar "bildirim 3 dakika bana oturum yok olduğunda oluşur." gibi senaryolarda gerekli

Sırayla olmayan giriş akışları ya da şunlardır:
* Sıralanmış (ve bu nedenle **Gecikmeli**).
* Tooa kullanıcı tarafından belirtilen ilke göre hello sistem tarafından ayarlanır.


## <a name="lateness-tolerance"></a>Lateness dayanıklılık
Akış analizi, bu senaryo türlerini göstereceği. Akış analizi "çıkış sıra" ve "geç" olayları için sahiptir. Bu yolu izleyerek hello olayları işler:

* Sıralama dışında ulaşır ancak içinde hello toleransını ayarlayın olaylar **zaman damgası tarafından kaldırılmasında**.
* Dayanıklılık daha sonra gelen olaylar **bırakılan veya ayarlanmış**.
    * **Ayarlanmış**: ayarlanmış tooappear toohave hello son kabul edilebilir zaman gelmedi.
    * **Bırakılan**: atılır.

![Stream Analytics olay işleme](media/stream-analytics-event-handling/stream-analytics-event-handling.png)

## <a name="reduce-hello-number-of-out-of-order-events"></a>Düzen dışı olayları Hello sayısını azaltın

Stream Analytics (örneğin, pencerelenmiş toplamlar veya zamana bağlı birleştirmeler) gelen olayları işlerken zamana bağlı bir dönüşüm uygulandığından, Stream Analytics gelen olayları zaman damgası sırasına göre sıralar.

Merhaba "zaman damgası tarafından" anahtar sözcüğü olduğunda **değil** kullanıldığında, hello Azure Event Hubs olay sıraya alma süresi varsayılan olarak kullanılır. Olay hub'ları hello zaman damgası hello olay hub'ın her bir bölüm monotonicity güvence altına alır. Ayrıca, tüm bölümleri olaylarından zaman damgası sırayla birleştirilecek garanti eder. Bu iki olay hub'ları garantiler hiçbir sipariş olayları emin olun.

Bazı durumlarda, toouse hello gönderenin zaman damgası için önemlidir. Bu durumda, bir zaman damgası hello olay yükü öğesinden "zaman damgası tarafından." kullanarak seçilir. Bu senaryolarda, bir veya daha fazla olay misorder kaynakları sunulan:

* Olay üreticileri saati eğriltir vardır. Üreticileri, farklı bilgisayarlardan olduğunda farklı saatler sahip oldukları için bu yaygındır.
* Ağ gecikmesi hello olayları toohello hedef olay hub'ının hello kaynağından yoktur.
* Saat eğriltir olay hub'ı bölümler arasında mevcut. Akış analizi, ilk olay enqueue zamanına göre tüm olay hub'ı bölümleri olaylarından sıralar. Ardından, hatalı sıralanmış olayları için hello veri akışı inceler.

Merhaba yapılandırma sekmesinde Varsayılanları aşağıdaki hello bakın:

![Stream Analytics sipariş işleme](media/stream-analytics-event-handling/stream-analytics-out-of-order-handling.png)

0 saniye hello düzen dışı tolerans penceresi kullanırsanız, tüm olayları hello zaman sırada olduğundan ettiği taraf olduğunu. Hatalı sıralanmış olay Hello üç kaynağını göz önüne alındığında, bu durum geçerlidir düşüktür. 

tooallow Stream Analytics toocorrect bir olay misorder, sıfır olmayan düzen dışı tolerans penceresi belirtebilirsiniz. Stream Analytics toothat penceresi ve bunları kullanarak seçtiğiniz zaman damgası hello yeniden verilen siparişler olaylarını arabelleğe alır. Ardından, hello zamana bağlı dönüştürme uygulanır. Bir 3 saniyelik penceresi başlatın ve hello değeri tooreduce hello saatine göre olayların sayısını ayarlayın. 

Merhaba ara belleğe almanın bir yan etkisi hello çıkış olmasıdır **tarafından hello aynı Gecikmeli süreyi**. Merhaba değeri tooreduce hello düzen dışı olayların sayısını ayarlamak ve hello iş gecikme düşük tutun.

## <a name="get-help"></a>Yardım alın
Ek Yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooStream analizi](stream-analytics-introduction.md)
* [Stream Analytics ile çalışmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Stream Analytics işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Stream Analytics sorgu dili başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Stream Analytics Yönetimi REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)