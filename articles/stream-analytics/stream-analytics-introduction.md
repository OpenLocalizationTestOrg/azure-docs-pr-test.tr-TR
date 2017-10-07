---
title: aaaIntroduction tooStream Analytics | Microsoft Docs
description: "Merhaba nesnelerin interneti (IOT) akış verilerini analiz etmenize gerçek zamanlı olarak sağlayan bir yönetilen hizmet olan Stream Analytics hakkında bilgi edinin."
keywords: "hizmet olarak analytics, yönetilen hizmetler, akış işleme, streaming analytics, stream analytics nedir"
services: stream-analytics
documentationcenter: 
author: jenniehubbard
manager: jhubbard
editor: cgronlun
ms.assetid: 613c9b01-d103-46e0-b0ca-0839fee94ca8
ms.service: stream-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/08/2017
ms.author: jhubbard
ms.openlocfilehash: 6dd7ea1d358bcc94e927a3e699a2771a25104d72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-stream-analytics"></a>Stream Analytics nedir?

Azure Stream Analytics, akış verilerine gerçek zamanlı analitik hesaplamalar eklemenizi sağlayan tam yönetimli bir olay işleme sistemidir. Merhaba verileri, cihazlar, algılayıcılar, web siteleri, sosyal medya akışları, uygulamalar, altyapı sistemleri ve daha fazla gelebilir. 

## <a name="what-can-i-do-with-stream-analytics"></a>Stream Analytics'te ne yapabilirim?

Stream Analytics tooexamine yüksek miktarda veri aygıtları veya işlemler akışının kullanın, hello veri akışından bilgi ayıklamak ve desenleri, eğilimleri ve ilişkileri bakın. Ne hello verilerde olduğuna bağlı olarak, uygulama görevleri gerçekleştirebilirsiniz. Örneğin, uyarılar oluşturacak, Otomasyon iş akışlarını devre dışı kazandırın, Raporlama Aracı Power BI gibi bilgileri tooa akış veya sonraki araştırma verilerini depolamak. 

Örnekler:

* Finansal hizmet şirketleri tarafından sunulan kişiselleştirilmiş, gerçek zamanlı borsa analizi ve uyarılar.
* İşlem verilerinin incelenmesiyle gerçek zamanlı sahtekarlık algılama. 
* Veri ve kimlik koruması hizmetleri.
* Fiziksel nesnelere takılı sensörler ve aktüatörler tarafından üretilen verilerin analiz edilmesi (Nesnelerin İnterneti, IoT).
* Web tıklama dizisi çözümlemeleri.
* Belirli bir zaman aralığındaki müşteri deneyimi kötüye gittiğinde uyarı oluşturma gibi müşteri ilişkileri yönetimi (CRM) uygulamaları.

## <a name="how-does-stream-analytics-work"></a>Stream Analytics nasıl çalışır?

Bu diyagramda, nasıl veri alınan, analiz ve sunu veya eylem için gönderilen gösteren hello Stream Analytics ardışık düzeni gösterilir. 

![Stream Analytics işlem hattı](./media/stream-analytics-introduction/stream_analytics_intro_pipeline.png)

Stream Analytics bir veri kaynağından gelen akışla başlar. Merhaba verileri Azure'da bir Azure olay hub'ı veya IOT hub'ı kullanarak bir aygıttan alınan. Merhaba verileri Azure Blob Storage gibi bir veri deposundan da çekebilir. 

tooexamine hello akışı, akış analizi oluşturma *iş* hello veri burada geldiğini belirtir. Merhaba iş ayrıca belirtir bir *dönüştürme*&mdash;nasıl toolook verilerin, desenleri veya ilişkiler. Bu görev için Stream Analytics belirli bir zaman aralığında toplanan akış verilerinin filtrelenmesini, sıralanmasını, toplanmasını ve birleştirilmesini destekleyen SQL benzeri bir sorgu dilini destekler.

Son olarak, bir çıktı toosend hello dönüştürülmüş verileri hello işini belirtir. Bu, hangi toodo yanıt toohello bilgileri analiz denetlemenize olanak tanır. Örneğin, yanıt tooanalysis içinde şunu yapabilirsiniz:

* Bir komut toochange bir aygıtın ayarlarını gönderin. 
* Bulgularına göre eylemde bir işlem tarafından izlenen veri tooa sırası gönderin. 
* Raporlama veri tooa Power BI panosuna gönderin.
* Data Lake Store, SQL Server veritabanına veya Azure Blob veya tablo depolama gibi veri toostorage gönderin.

Bir iş çalışırken işi izleyebilir ve saniye başına işlenen olay sayısını ayarlayabilirsiniz. Aynı zamanda sorun giderme amacıyla tanılama günlüğü oluşturan işler de oluşturabilirsiniz.

## <a name="key-capabilities-and-benefits"></a>Temel işlevler ve avantajlar

Akış analizi tasarlanmış toobe kolay toouse, esnek, ölçeklenebilir tooany iş boyut ve ekonomik ' dir.

### <a name="connectivity-toomany-inputs-and-outputs"></a>Bağlantı toomany girişleri ve çıkışları

Doğrudan akış analizi bağlanan çok[Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) ve [Azure IOT Hub](https://azure.microsoft.com/services/iot-hub/) akış alımı ve hello [Azure Blob Depolama hizmetinin](https://docs.microsoft.com/azure/storage/storage-introduction#blob-storage-accounts) tooingest geçmiş verileri. Olay hub'larından veri alıyorsanız Stream Analytics'i diğer veri kaynakları ve işleme sistemleriyle birlikte kullanabilirsiniz.

İş girdisi aynı zamanda başvuru bilgilerini (statik veya yavaş değişen veriler) de içerebilir. Akış veri toothis başvuru veri tooperform arama işlemleri hello katılabilir, veritabanı sorgularını ile aynı şekilde.

Stream Analytics iş çıktısını birçok yöne yönlendirme. Azure Storage bloblarında ya da tablo, Azure SQL DB, Azure Data Lake depoları veya Azure Cosmos DB gibi toostorage yazabilirsiniz. Buradan, Azure Hdınsight toplu analizi için hello veri geçebilir. Olay hub'ları, Azure Service Bus konu başlıklarına veya sıraları gibi başka bir işlem tarafından hello çıktı tooanother hizmet tüketimi için gönderebilir. Görselleştirme hello çıktı tooPower BI gönderebilir.

### <a name="ease-of-use"></a>Kullanım kolaylığı

toodefine dönüşümleri, basit, bildirim temelli kullanma [Stream Analytics sorgu dilini](https://msdn.microsoft.com/library/azure/dn834998.aspx) olanak tanıyan karmaşık çözümlemeler programlama ile oluşturun. Merhaba sorgu dili veri akışı kendi giriş olarak alır. Hello verileri sıralamak ve filtre değerleri topla, hesaplamalar, verileri (içinde akış veya tooreference veri) katılma ve Jeo-uzamsal işlevlerini kullanın sonra kullanabilirsiniz. Merhaba canlı akış alan ayıklayabilirsiniz örnek verileri kullanarak sorguları sınayabilirsiniz ve IntelliSense ve sözdizimi denetimi kullanarak hello portal sorgularda düzenleyebilirsiniz.

### <a name="extensible-query-language"></a>Genişletilebilir sorgu dili

Tanımlama ve ek işlevleri yürütmesini hello sorgu dili hello özelliklerini genişletebilirsiniz. İşlev çağrıları hello Azure Machine Learning hizmeti tootake avantajı Azure Machine Learning çözümlerinin tanımlayabilirsiniz. Ayrıca, sipariş tooperform karmaşık hesaplamalar Stream Analytics sorgu parçası olarak JavaScript kullanıcı tanımlı işlevler (UDF'ler) tümleştirebilirsiniz.

### <a name="scalability"></a>Ölçeklenebilirlik

Akış analizi too1 GB saniye başına gelen veri yukarı işleyebilir. İle tümleştirme [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) ve [Azure IOT Hub](https://azure.microsoft.com/services/iot-hub/) bağlı cihazlar, tıklama ve günlük dosyaları, tooname gelen işleri tooingest milyonlarca gelen Saniyede olayların birkaç sağlar. Olay hub'ları Hello bölüm özelliğini kullanarak, mantıksal adımlara hesaplamalar bölüm, her hello özelliği toobe daha fazla ile tooincrease ölçeklenebilirlik bölümlenmiş.

### <a name="low-cost"></a>Düşük maliyet

Bir bulut hizmeti olarak Stream Analytics düşük maliyeti yapmalarını en iyi duruma getirilmiş toolet ' dir. Üzerinde akış birimi kullanımı ve hello hello sistemin işlediği veri miktarına göre kullandıkça, ücret ödersiniz. Kullanım hello işlenen olayların hacmine göre türetilmiş ve işlem gücü hello miktarını hello küme toohandle içinde akış analizi işleri sağlandı.

### <a name="reliability-quick-recovery-and-repeatability"></a>Güvenilirlik, hızlı kurtarma ve tekrarlama

Yönetilen bir hizmet hello bulutta Stream Analytics Veri kaybını önlemeye yardımcı olur ve iş sürekliliği sağlar. Hataları oluşursa hello hizmeti yerleşik kurtarma özellikleri sağlar. Hello yapılandırabilmeye ile toointernally devam durumu, olası tooarchive olayı ve her zaman aynı sonuçları hello alma hello gelecekteki işlemede yeniden tekrarlanabilir sonuçlar hello hizmet sağlar. Bu geçmişe toogo sağlar ve hesaplamalar kök neden analizi, durum çözümlemesi vb. gerçekleştirirken araştırın.

## <a name="next-steps"></a>Sonraki adımlar

* [IoT cihazlarından gelen girdiler ve sorgularla çalışmayı deneyerek](stream-analytics-get-started-with-azure-stream-analytics-to-process-data-from-iot-devices.md) başlangıç yapın.
* Derleme bir [uçtan uca Stream Analytics çözüm](stream-analytics-real-time-fraud-detection.md) telefon meta veri toolook sahte çağrıları için inceler.
* Merhaba akış analizi için SQL benzeri sorgu dili ve gibi benzersiz kavramları hakkında bilgi edinin [penceresi işlevleri](stream-analytics-window-functions.md).
* Nasıl çok öğrenin[ölçeklendirme akış analizi işleri](stream-analytics-scale-jobs.md). 
* Nasıl çok öğrenin[akış analizi ve Azure Machine Learning tümleştirme](stream-analytics-machine-learning-integration-tutorial.md).
* Hello tooyour Stream Analytics soruları yanıtlar bulmak [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

