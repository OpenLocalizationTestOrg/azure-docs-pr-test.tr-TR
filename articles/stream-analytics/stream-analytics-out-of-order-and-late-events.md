---
title: "İşleme olayı sırası ve Azure akış Analizi ile lateness | Microsoft Docs"
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
ms.openlocfilehash: a48e48c5fc65d0ffbb7c23f426a4b06dcd568821
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stream-analytics-event-order-handling"></a>Azure Stream Analytics olay sipariş işleme

Olayları bir zamana bağlı veri akışında olayı alındığında süresiyle her olay kaydedilir. Bazı koşullar, bazı olaylar bazen gönderildikleri farklı bir sırada almaya olay akışları neden olabilir. Bunun gerçekleşmesi için basit bir TCP yeniden aktarım ya da bile bir saat gönderen aygıtı ve alıcı olay hub'ı arasında kaymasına neden olabilir. "Noktalama" olayları olay varış yokluğu zamanında ilerletmek için alınan olay akışlar için de eklenir. Bunlar "bildirim 3 dakika bana oturum yok olduğunda oluşur." gibi senaryolarda gerekli

Sırayla olmayan giriş akışları ya da şunlardır:
* Sıralanmış (ve bu nedenle **Gecikmeli**).
* Sistem tarafından bir kullanıcı tarafından belirtilen ilkesine göre ayarlanır.


## <a name="lateness-tolerance"></a>Lateness dayanıklılık
Akış analizi, bu senaryo türlerini göstereceği. Akış analizi "çıkış sıra" ve "geç" olayları için sahiptir. Bu olaylar aşağıdaki yollarla işlediği:

* Sıranın dışında ancak kümesi tolerans dahilinde gelmesini olaylar **zaman damgası tarafından kaldırılmasında**.
* Dayanıklılık daha sonra gelen olaylar **bırakılan veya ayarlanmış**.
    * **Ayarlanmış**: kabul edilebilir en son zaman gelmedi görünecek şekilde ayarlanmış.
    * **Bırakılan**: atılır.

![Stream Analytics olay işleme](media/stream-analytics-event-handling/stream-analytics-event-handling.png)

## <a name="reduce-the-number-of-out-of-order-events"></a>Düzen dışı olayların sayısını azaltın

Stream Analytics (örneğin, pencerelenmiş toplamlar veya zamana bağlı birleştirmeler) gelen olayları işlerken zamana bağlı bir dönüşüm uygulandığından, Stream Analytics gelen olayları zaman damgası sırasına göre sıralar.

"Zaman damgası tarafından" anahtar sözcüğü olduğunda **değil** kullanıldığında, Azure Event Hubs olay sıraya alma süresi varsayılan olarak kullanılır. Olay hub'ları olay hub'ın her bölüm zaman damgasını monotonicity güvence altına alır. Ayrıca, tüm bölümleri olaylarından zaman damgası sırayla birleştirilecek garanti eder. Bu iki olay hub'ları garantiler hiçbir sipariş olayları emin olun.

Bazı durumlarda, gönderenin zaman damgası kullanabilmeniz için önemlidir. Bu durumda, bir zaman damgası olay yükü gelen "zaman damgası tarafından." kullanarak seçilir. Bu senaryolarda, bir veya daha fazla olay misorder kaynakları sunulan:

* Olay üreticileri saati eğriltir vardır. Üreticileri, farklı bilgisayarlardan olduğunda farklı saatler sahip oldukları için bu yaygındır.
* Hedef olay hub'ına olayların kaynağından bir ağ gecikme olur.
* Saat eğriltir olay hub'ı bölümler arasında mevcut. Akış analizi, ilk olay enqueue zamanına göre tüm olay hub'ı bölümleri olaylarından sıralar. Ardından, hatalı sıralanmış olayları için veri akışı inceler.

Yapılandırma sekmesinde, aşağıdaki varsayılanlar bakın:

![Stream Analytics sipariş işleme](media/stream-analytics-event-handling/stream-analytics-out-of-order-handling.png)

0 saniye düzen dışı tolerans penceresi kullanırsanız, tüm olayları her zaman sırada olduğundan ettiği taraf olduğunu. Hatalı sıralanmış olay üç kaynağını göz önüne alındığında, bu durum geçerlidir düşüktür. 

Bir olay misorder düzeltmek Stream Analytics izin vermek için sıfır olmayan düzen dışı tolerans penceresi belirtebilirsiniz. Akış analizi kadar bu pencere olaylarını arabelleğe alır ve ardından bunları seçtiğiniz zaman damgası kullanarak yeniden sıralar. Ardından, zamana bağlı dönüşümünü uygular. Bir 3 saniyelik penceresi başlatın ve saatine göre olay sayısını azaltmak için değer ayarlayın. 

Ara belleğe almanın bir yan etkisi çıkış olmasıdır **saat tutarında Gecikmeli**. Düzen dışı olayların sayısını azaltmak için değer ayarlamak ve iş gecikme düşük tutun.

## <a name="get-help"></a>Yardım alın
Ek Yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Sonraki adımlar
* [Stream Analytics'e giriş](stream-analytics-introduction.md)
* [Stream Analytics ile çalışmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Stream Analytics işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Stream Analytics sorgu dili başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Stream Analytics Yönetimi REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)