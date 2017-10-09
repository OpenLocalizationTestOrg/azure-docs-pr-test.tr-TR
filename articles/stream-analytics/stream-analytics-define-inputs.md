---
title: "Veri bağlantısı: veri akışı olay akışının girişlerinde | Microsoft Docs"
description: "Bir veri bağlantısı tooStream Analytics 'Girişleri' adlı ayarlama hakkında bilgi edinin. Giriş olayları veri akışından içerir ve ayrıca veri başvuru."
keywords: "veri akışı, veri bağlantısı, olay akışı"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 8155823c-9dd8-4a6b-8393-34452d299b68
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/05/2017
ms.author: samacha
ms.openlocfilehash: be2008f159061c5c9be9d0314c27fa67193e3269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-connection-learn-about-data-stream-inputs-from-events-toostream-analytics"></a>Veri bağlantısı: olayları tooStream Analytics akış girişlerinde hakkındaki verileri öğrenin
Hello veri bağlantısı tooa Stream Analytics işi olan bir akış başvurulan tooas hello işin bir veri kaynağından olayların *giriş*. Akış analizi dahil olmak üzere Azure veri kaynakları ile veri akışı, birinci sınıf tümleştirme sahip [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/), [Azure IOT Hub](https://azure.microsoft.com/services/iot-hub/), ve [Azure Blob Depolama](https://azure.microsoft.com/services/storage/blobs/). Bu kaynaklardan hello olabilir giriş aynı Azure aboneliğinden analytics işi olarak veya farklı bir abonelik.

## <a name="data-input-types-data-stream-and-reference-data"></a>Veri türleri giriş: veri akış ve başvuru verileri
Veri tooa veri kaynağına itildiği gibi hello akış analizi işi tarafından tüketilen ve gerçek zamanlı olarak işlenen. Girişleri iki türlerine bölünen: veri akışı girişleri ve başvuru verileri girdi.

### <a name="data-stream-inputs"></a>Veri akışı girişleri
Veri akışı bir sınırsız olayları zamanla dizisidir. Akış analizi işleri, en az bir veri akış girişi eklemeniz gerekir. Olay hub'ları, IOT Hub ve Blob Depolama veri akışı giriş kaynağı olarak desteklenir. Olay hub'ları kullanılan toocollect olay birden çok cihazları ve Hizmetleri akışlarıdır. Bu akışlar, sosyal medya Etkinlik Akışları, hisse senedi ticareti bilgi veya algılayıcı verileri içerebilir. IOT hub'ları, nesnelerin interneti (IOT) senaryolarında bağlı aygıtlardan en iyi duruma getirilmiş toocollect verilerdir.  BLOB Depolama günlük dosyaları gibi bir akış olarak toplu veri alma için bir giriş kaynağı kullanılabilir.  

### <a name="reference-data"></a>Başvuru verileri
Akış analizi, aynı zamanda giriş olarak bilinen destekler *başvuru verileri*. Bu, ya da statik yardımcı verilerdir veya değişen yavaş. Genellikle, bağıntı ve aramalar gerçekleştirmek için kullanılır. Örneğin, bir SQL birleştirme toolook statik değerleri gerçekleştireceği kadar hello veri akışı giriş toodata hello başvuru verilerinde verileri birleştirebilirsiniz. Azure Blob Depolama şu anda yalnızca desteklenen hello giriş başvuru verileri kaynağıdır. Başvuru veri kaynağı BLOB'lar sınırlı too100 MB boyutunda.

toocreate başvuru veri girişleri nasıl görürüm toolearn [kullanım başvuru verileri](stream-analytics-use-reference-data.md).  

## <a name="create-data-stream-input-from-event-hubs"></a>Veri akış girişine olay hub'larından oluşturma

Azure Event Hubs sağlayan yüksek düzeyde ölçeklenebilir olay ingestors yayımlama-abonelik. Böylece işlemek ve veri bağlı cihazlarınız ve uygulamalarınız tarafından üretilen oldukça büyük miktardaki hello analiz bir event hub saniye başına milyonlarca olayı toplayabilirsiniz. Olay hub'ları ve akış analizi birlikte sağlayın, uçtan uca çözüm ile gerçek zamanlı analiz için — olay hub'ları olayları Azure'da gerçek zamanlı akış olanak tanır ve akış analizi işleri, bu olayları gerçek zamanlı işleyebilir. Örneğin, web tıklama, sensör okumaları veya çevrimiçi günlük olayları tooEvent hub gönderebilirsiniz. Daha sonra gerçek zamanlı filtreleme, toplama ve bağıntı hello giriş veri akışları olarak Stream Analytics işleri toouse olay hub'ları da oluşturabilirsiniz.

Akış analizi, olay hub'ten gelen olayların Hello varsayılan zaman damgası olan olay hello hello zaman damgası olan hello event hub'ında, gelen `EventEnqueuedUtcTime`. tooprocess hello olay yükünde bir zaman damgası kullanarak bir akış olarak veri Merhaba, hello kullanmalısınız [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) anahtar sözcüğü.

### <a name="consumer-groups"></a>Tüketici grupları
Her akış analizi olay hub'ı giriş toohave kendi tüketici grubu yapılandırmanız gerekir. Bir işi kendi kendine birleşim içerdiğinde ya da birden fazla giriş varsa, bazı giriş aşağı birden fazla okuyucu tarafından okuyabilir. Bu durum hello tek bir tüketici grubundaki okuyucu sayısını etkiler. tooavoid aşan hello olay hub'ları bölüm başına tüketici grubu başına beş okuyucuların, onu bir tüketici grubunda her akış analizi işi için en iyi bir yöntem toodesignate sınırıdır. Olay hub'ı başına 20 tüketici grupları sınırı yoktur. Daha fazla bilgi için bkz: [Event Hubs Programlama Kılavuzu](../event-hubs/event-hubs-programming-guide.md).

### <a name="configure-an-event-hub-as-a-data-stream-input"></a>Bir event hub giriş veri akışı yapılandırın
Merhaba aşağıdaki tabloda açıklanmaktadır hello her bir özellik **yeni giriş** dikey penceresinde hello giriş olarak bir olay hub'ı yapılandırırken Azure portalı.

| Özellik | Açıklama |
| --- | --- |
| **Giriş diğer adı** |Bu hello işin sorgu tooreference kullandığınız kolay bir ad girin. |
| **Hizmet veri yolu ad alanı** |Mesajlaşma varlıkları kümesine ilişkin bir kapsayıcıdır bir Azure hizmet veri yolu ad. Yeni bir olay hub'ı oluşturduğunuzda aynı zamanda bir hizmet veri yolu ad alanı oluşturun. |
| **Olay hub'ı adı** |Merhaba olay hub'ı toouse giriş olarak Hello adı. |
| **Olay hub'ı ilke adı** |toohello event hub'ı erişimi sağlayan paylaşılan erişim ilkesi hello. Her paylaşılan erişim ilkesinin bir adı, ayarlayın ve erişim anahtarları izinleri vardır. |
| **Olay hub tüketici grubu** (isteğe bağlı) |Merhaba tüketici grubu toouse tooingest verileri hello olay hub'ı. Herhangi bir tüketici grubu belirtilirse, hello Stream Analytics işi hello varsayılan bir tüketici grubu kullanır. Her akış analizi işi için ayrı bir tüketici grubundaki kullanmanızı öneririz. |
| **Olayı seri hale getirme biçimi** |Merhaba seri hale getirme biçimi (JSON, CSV veya Avro) hello gelen veri akışının. |
| **Kodlama** | UTF-8 şu anda yalnızca desteklenen hello kodlama biçimidir. |

Verilerinizi bir event hub'ından, meta veri alanlarını, Stream Analytics sorgu aşağıdaki erişim toohello vardır:

| Özellik | Açıklama |
| --- | --- |
| **EventProcessedUtcTime** |Başlangıç tarihi ve saati hello olay akış analizi tarafından işlendi. |
| **EventEnqueuedUtcTime** |Başlangıç tarihi ve saati hello olayın olay hub'ları tarafından alındı. |
| **PartitionID** |Merhaba giriş bağdaştırıcısı Hello sıfır tabanlı bölüm kimliği. |

Örneğin, bu alanları kullanarak, aşağıdaki örneğine hello gibi bir sorgu yazabilirsiniz:

````
SELECT
    EventProcessedUtcTime,
    EventEnqueuedUtcTime,
    PartitionId
FROM Input
````

## <a name="create-data-stream-input-from-iot-hub"></a>IOT Hub'ından veri akış girişi oluşturun
Azure IOT Hub, yüksek düzeyde ölçeklenebilir yayımlama-abone olma IOT senaryoları için en iyi duruma getirilmiş olay yutucu ' dir.

Stream Analytics bir IOT hub'ten gelen olayların Hello varsayılan zaman damgası olan olay hello hello zaman damgası olan hello IOT hub, gelen `EventEnqueuedUtcTime`. tooprocess hello olay yükünde bir zaman damgası kullanarak bir akış olarak veri Merhaba, hello kullanmalısınız [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) anahtar sözcüğü.

> [!NOTE]
> İle gönderilen iletileri bir `DeviceClient` özelliği işlenebilir.
> 
> 

### <a name="consumer-groups"></a>Tüketici grupları
Her akış analizi IOT hub giriş toohave kendi tüketici grubu yapılandırmanız gerekir. Bir işi kendi kendine birleşim içerdiğinde ya da birden fazla giriş varsa, bazı giriş aşağı birden fazla okuyucu tarafından okuyabilir. Bu durum hello tek bir tüketici grubundaki okuyucu sayısını etkiler. tooavoid aşan hello Azure IOT Hub tüketici grubu bölüm başına başına beş okuyucuların, onu bir tüketici grubunda her akış analizi işi için en iyi bir yöntem toodesignate sınırıdır.

### <a name="configure-an-iot-hub-as-a-data-stream-input"></a>Giriş veri akışı IOT hub'ı yapılandırma
Merhaba aşağıdaki tabloda açıklanmaktadır hello her bir özellik **yeni giriş** dikey penceresinde hello giriş olarak bir IOT hub'ı yapılandırırken Azure portalı.

| Özellik | Açıklama |
| --- | --- |
| **Giriş diğer adı** |Bu hello işin sorgu tooreference kullandığınız kolay bir ad girin.|
| **IOT hub'ı** |Merhaba IOT hub toouse giriş olarak Hello adı. |
| **Uç noktası** |Merhaba IOT hub'ına yönelik Hello uç noktası.|
| **Paylaşılan erişim ilkesi adı** |toohello IOT hub'ı erişim sağlayan hello paylaşılan erişim ilkesi. Her paylaşılan erişim ilkesinin bir adı, ayarlayın ve erişim anahtarları izinleri vardır. |
| **Paylaşılan Erişim İlkesi anahtarı** |Merhaba paylaşılan erişim anahtarı tooauthorize erişim toohello IOT hub'ı kullanılır. |
| **Tüketici grubu** (isteğe bağlı) |Merhaba tüketici grubu toouse tooingest verileri hello IOT hub'ı. Herhangi bir tüketici grubu belirtilirse, akış analizi işi hello varsayılan bir tüketici grubu kullanır. Her akış analizi işi için farklı bir tüketici grubundaki kullanmanızı öneririz. |
| **Olayı seri hale getirme biçimi** |Merhaba seri hale getirme biçimi (JSON, CSV veya Avro) hello gelen veri akışının. |
| **Kodlama** |UTF-8 şu anda yalnızca desteklenen hello kodlama biçimidir. |

Verilerinizi bir IOT hub'ından, meta veri alanlarını, Stream Analytics sorgu aşağıdaki erişim toohello vardır:

| Özellik | Açıklama |
| --- | --- |
| **EventProcessedUtcTime** |Başlangıç tarihi ve saati hello olay işlendi. |
| **EventEnqueuedUtcTime** |Başlangıç tarihi ve saati hello olay hello IOT hub tarafından alındı. |
| **PartitionID** |Merhaba giriş bağdaştırıcısı Hello sıfır tabanlı bölüm kimliği. |
| **IoTHub.MessageId** | Toocorrelate iki yönlü iletişim IOT hub ' kullandığı kimliği. |
| **IoTHub.CorrelationId** |İleti yanıtlarını ve geri bildirim IOT hub'ın kullanılan kimliği. |
| **IoTHub.ConnectionDeviceId** |Merhaba kimlik doğrulama kimliği bu iletiyi toosend kullanılır. Bu değer servicebound iletileri hello IOT hub tarafından damgalandı. |
| **IoTHub.ConnectionDeviceGenerationId** |Merhaba Hello oluşturma kimliği kullanılan toosend olan cihaz bu ileti kimliği. Bu değer servicebound iletileri hello IOT hub tarafından damgalandı. |
| **IoTHub.EnqueuedTime** |Merhaba zaman selamlama iletisine hello IOT hub tarafından ne zaman alındı. |
| **IoTHub.StreamId** |Merhaba gönderen aygıt tarafından eklenen özel olay özelliği. |


## <a name="create-data-stream-input-from-blob-storage"></a>Blob depolama alanından veri akış girişi oluşturun
Büyük miktarda yapılandırılmamış verileri toostore hello bulutta ile senaryoları için Azure Blob Depolama uygun maliyetli ve ölçeklenebilir bir çözüm sunar. Blob Depolama birimindeki verileri genellikle kalan verileri olarak kabul edilir. Ancak, bu veri akışı akış analizi tarafından işlenebilir. Blob Depolama Stream Analytics girişle tipik bir senaryo günlük işlemesidir. Bu senaryoda, telemetri verilerini bir sisteminden yakalanan ve gereksinimlerini toobe ayrıştırılır ve işlenen tooextract anlamlı veri.

Merhaba varsayılan zaman damgası Stream Analytics içinde Blob Depolama olayların blob hello hello zaman damgası son değiştirildiği olduğu olduğu `BlobLastModifiedUtcTime`. tooprocess hello olay yükünde bir zaman damgası kullanarak bir akış olarak veri Merhaba, hello kullanmalısınız [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) anahtar sözcüğü.

CSV biçimlendirilmiş girişleri *gerektiren* hello veri kümesi için bir başlık satırı toodefine alanları. Ayrıca, tüm üstbilgisi satır alanları benzersiz olması gerekir.

> [!NOTE]
> Akış analizi, içerik tooan mevcut blob eklemeyi desteklemez. Akış analizi blob yalnızca bir kez görüntüler ve hello blob hello iş hello veri okuma sonra gerçekleşen değişiklikleri işlenmez. En iyi uygulama tooupload tüm hello verilerinin bir kez ve ardından olayları toothat blob deposu eklememek.
> 

### <a name="configure-blob-storage-as-a-data-stream-input"></a>BLOB Depolama giriş veri akışı yapılandırın

Merhaba aşağıdaki tabloda açıklanmaktadır hello her bir özellik **yeni giriş** dikey penceresinde hello giriş olarak Blob Depolama Birimi yapılandırırken Azure portalı.

| Özellik | Açıklama |
| --- | --- |
| **Giriş diğer adı** | Bu hello işin sorgu tooreference kullandığınız kolay bir ad girin. |
| **Depolama hesabı** | Merhaba blob dosyalarının bulunduğu hello depolama hesabı Hello adı. |
| **Depolama hesabı anahtarı** | Merhaba depolama hesabıyla ilişkili hello gizli anahtar. |
| **Kapsayıcı** | Merhaba blob giriş Hello kapsayıcısı. Kapsayıcılar hello Microsoft Azure Blob hizmeti depolanan BLOB'lar için mantıksal bir gruplandırmasını sağlar. Blob toohello Azure Blob Depolama hizmetinin karşıya yüklediğinde, o blob için bir kapsayıcı belirtmeniz gerekir. |
| **Yol deseni** (isteğe bağlı) | Merhaba dosya yolu toolocate hello BLOB'lar hello belirtilen kapsayıcı içinde kullanılır. Merhaba yol içinde üç değişkenleri aşağıdaki hello bir veya daha fazla örneğini belirtebilirsiniz: `{date}`, `{time}`, veya`{partition}`<br/><br/>Örnek 1:`cluster1/logs/{date}/{time}/{partition}`<br/><br/>Örnek 2:`cluster1/logs/{date}`<br/><br/>Merhaba `*` karakter hello yol öneki için izin verilen bir değer değil. Yalnızca geçerli <a HREF="https://msdn.microsoft.com/library/azure/dd135715.aspx">Azure blob karakter</a> izin verilir. |
| **Tarih biçimi** (isteğe bağlı) | Merhaba yolunda hello tarih değişken kullanırsanız, hangi hello dosyaları düzenlenir tarih biçimi hello. Örnek:`YYYY/MM/DD` |
| **Saat biçimi** (isteğe bağlı) |  Merhaba yolunda hello zaman değişken kullanırsanız, hangi hello dosyaları düzenlenir saat biçiminde hello. Şu anda yalnızca desteklenen hello değerdir `HH`. |
| **Olayı seri hale getirme biçimi** | Merhaba seri hale getirme biçimi (JSON, CSV veya Avro) gelen veri akışları için. |
| **Kodlama** | CSV ve JSON için UTF-8 şu anda yalnızca desteklenen hello kodlama biçimidir. |

Verilerinizi bir Blob Depolama kaynaktan geldiğinde, meta veri alanlarını, Stream Analytics sorgu aşağıdaki erişim toohello vardır:

| Özellik | Açıklama |
| --- | --- |
| **BlobName** |Olay hello hello giriş blob Hello adını geldiği. |
| **EventProcessedUtcTime** |Başlangıç tarihi ve saati hello olay akış analizi tarafından işlendi. |
| **BlobLastModifiedUtcTime** |Başlangıç tarihi ve saati bu hello blob son değiştirildi. |
| **PartitionID** |Merhaba giriş bağdaştırıcısı Hello sıfır tabanlı bölüm kimliği. |

Örneğin, bu alanları kullanarak, aşağıdaki örneğine hello gibi bir sorgu yazabilirsiniz:

````
SELECT
    BlobName,
    EventProcessedUtcTime,
    BlobLastModifiedUtcTime
FROM Input
````

## <a name="get-help"></a>Yardım alın
Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Sonraki adımlar
Azure veri bağlantı seçenekleri hakkında Stream Analytics işleri öğrendiniz. Stream Analytics hakkında daha fazla toolearn bakın:

* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
