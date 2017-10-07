---
title: "aaaScaling medyayı işleme genel bakış | Microsoft Docs"
description: "Bu konu Azure Media Services ile ölçeklendirme medyayı işleme bir genel bakıştır."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 780ef5c2-3bd6-4261-8540-6dee77041387
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: d17531f79d4c1e0d0fa544c4fb5c083684e706fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-media-processing-overview"></a>Ölçeklendirme medyayı işleme genel bakış
Bu sayfayı neden ve nasıl genel bir fikir veren tooscale medyayı işleme. 

## <a name="overview"></a>Genel Bakış
Bir Media Services hesabı bir ayrılmış birim görevleri işleme medyanızı işlenme hello hızı belirleyen türü ile ilişkilidir. Merhaba aşağıdaki arasında seçim yapabilirsiniz ayrılmış birim türleri: **S1**, **S2**, veya **S3**. Örneğin, aynı kodlama işi çalıştıktan daha hızlı hello kullandığınızda hello **S2** ayrılmış birim türü karşılaştırma toohello **S1** türü. Daha fazla bilgi için bkz: Merhaba [ayrılmış birim türleri](https://azure.microsoft.com/blog/high-speed-encoding-with-azure-media-services/).

Ayrıca toospecifying hello ayrılmış birim türü, ayrılmış birimleri ile hesabınızı tooprovision belirtebilirsiniz. sağlanan ayrılmış birim Hello sayısı belirli bir hesap eşzamanlı olarak işlenebilecek ortam görevleri hello sayısını belirler. Örneğin, beş medya görevler eşzamanlı olarak kadar uzun çalışıyor olacak beş ayrılmış birimler, hesabınız varsa, olarak vardır görevleri toobe işlenir. Merhaba Kalan görevler hello kuyrukta bekler ve sıralı olarak çalışan bir görev tamamlandığında işlemek için toplanmış. Bir hesap sağlanan tüm ayrılan birimler yoksa, ardından görevleri sırayla çekilir. Bu durumda, hello bir görev tamamlama arasındaki süre bekleyin ve hello sonraki bir başlangıç kaynakları hello kullanılabilirliğini hello sistemde bağlıdır.

## <a name="choosing-between-different-reserved-unit-types"></a>Farklı ayrılmış birim türleri arasında seçme
Aşağıdaki tablonun hello arasında farklı kodlama hızları seçerken karar vermenize yardımcı olur. Ayrıca, bazı Kıyaslama durumlar sağlar ve kendi testlerinizi üzerinde gerçekleştirebileceğiniz toodownload videolar kullanabilirsiniz SAS URL'leri sağlar:

| Senaryolar | **S1** | **S2** | **S3** |
| --- | --- | --- | --- |
| Hedeflenen kullanım örneği |Tek bit hızlı kodlama. <br/>Dosyaları SD veya çözümler altında hassas, düşük maliyetli değildir zaman. |Tek bit hızlı ve Çoklu bit hızı kodlaması.<br/>SD ve HD kodlama için normal kullanım. |Tek bit hızlı ve Çoklu bit hızı kodlaması.<br/>Tam HD ve 4K çözümleme videolar. Hassas ve hızlı bir döngü kodlama zaman. |
| Kıyaslama |[Giriş dosyası: 5 dakika uzun 29.97 adresindeki 640x360p Çerçeve/saniye](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_360p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D).<br/><br/>Tooa tek bit hızlı MP4 dosyası, kodlama hello aynı çözünürlüğü yaklaşık 11 dakika sürer. |[Giriş dosyası: 5 dakika uzun 29.97 adresindeki 1280x720p Çerçeve/saniye](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_720p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D)<br/><br/>"H264 Çoklu bit hızı ile 720 p" kodlama yaklaşık 5 dakika sürer hazır.<br/><br/>İle kodlama "H264 Çoklu bit hızı 720p" hazır yaklaşık 11.5 dakika sürer. |[Giriş dosyası: 5 dakika uzun 29.97 adresindeki 1920x1080p Çerçeve/saniye](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_1080p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D). <br/><br/>"H264 Çoklu bit hızı ile 1080 p" kodlama yaklaşık 2.7 dakika sürer hazır.<br/><br/>İle kodlama "H264 Çoklu bit hızı 1080p" hazır yaklaşık 5.7 dakika sürer. |

## <a name="considerations"></a>Dikkat edilmesi gerekenler
> [!IMPORTANT]
> Bu bölümde açıklanan konuları gözden geçirin.  
> 
> 

* Azure Media Indexer kullanarak işleri dizin oluşturma dahil olmak üzere tüm medyayı işleme parallelizing için ayrılan birimler çalışır.  Bununla birlikte kodlamadan farklı olarak, dizin oluşturma işleri daha hızlı ayrılmış birimlerde daha hızlı işlenmez.
* Paylaşılan hello kullanıyorsanız havuzu, diğer bir deyişle, olmaksızın herhangi ayrılmış birimleri sonra kodla görevlerinizi sahip aynı performans S1 RUs gibi hello. Ancak, görevlerinizi sıraya alınmış durumda harcayabilir herhangi bir üst sınır toohello saati yoktur ve belirli bir zamanda, tek en fazla görev çalıştırırsınız.
* veri merkezleri aşağıdaki hello hello sağlamıyorsa **S2** ayrılmış birim türü: Brezilya Güney ve Hindistan Batı.
* Merhaba aşağıdaki veri merkezi hello sunmaz **S3** ayrılmış birim türü: Hindistan Batı.

## <a name="billing"></a>Faturalandırma

Medya Ayrılmış Birimlerinin fiili olarak kullanıldığı dakika sayısı üzerinden ücretlendirilirsiniz. Ayrıntılı bir açıklama için hello hello SSS bölümüne bakın [Media Services fiyatlandırma](https://azure.microsoft.com/pricing/details/media-services/) sayfası.   

## <a name="quotas-and-limitations"></a>Kotalar ve sınırlamalar
Kotalar ve kısıtlamalar hakkında bilgi için ve nasıl tooopen bir destek bileti bkz [kotaları ve kısıtlamaları](media-services-quotas-and-limitations.md).

## <a name="next-step"></a>Sonraki adım
Bu teknolojilerden birine görevle işleme medya ölçeklendirme hello elde: 

> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portal](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

