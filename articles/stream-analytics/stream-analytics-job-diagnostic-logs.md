---
title: "Tanılama günlükleri ile aaaTroubleshoot Azure akış analizi | Microsoft Docs"
description: "Microsoft Azure'da nasıl tooanalyze tanılama akış analizi işleri günlüklerini öğrenin."
keywords: 
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
ms.openlocfilehash: 600fce73636dd137f8f3a137f1d77b59b4a88801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-stream-analytics-by-using-diagnostics-logs"></a>Azure Stream Analytics tanılama günlükleri kullanarak sorun giderme

Bazen, bir Azure akış analizi işi beklenmedik bir şekilde işlemeyi durdurur. Önemli toobe mümkün tootroubleshoot olayı bu tür değil. Merhaba olay beklenmeyen sorgu sonucu, bağlantı toodevices veya bir beklenmeyen hizmet kesintisi tarafından neden olabilir. Merhaba Stream Analytics tanılama günlüklerine yardımcı olabilecek oluşur ve kurtarma zamanı azaltmak sorunları hello nedenini belirlemek.

## <a name="log-types"></a>Günlük türleri

Akış analizi günlükleri iki tür sunar: 
* [Etkinlik günlükleri](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) (her zaman açıktır). Etkinlik günlükleri işleri üzerinde gerçekleştirilen işlemler fikir verir.
* [Tanılama günlüklerini](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) (yapılandırılabilir). Tanılama günlükleri daha zengin bir işlemle gerçekleşen her şeyi fikir sağlar. Merhaba iş silindiğinde tanılama hello iş oluşturulduğunda başlangıç ve bitiş günlüğe kaydeder. Bunlar olayları hello iş güncelleştirildiği ve çalışırken kapsar.

> [!NOTE]
> Azure Storage, Azure Event Hubs'a ve Azure günlük analizi tooanalyze uyumsuz verileri gibi hizmetler kullanabilirsiniz. Fiyatlandırma modeli bu hizmetlerin hello göre sizden ücret kesilir.
>

## <a name="turn-on-diagnostics-logs"></a>Tanılama günlüklerini Aç

Tanılama günlükleri **kapalı** varsayılan olarak. tooturn tanılama günlükleri üzerinde aşağıdaki adımları tamamlayın:

1.  Toohello Azure portalında oturum açın ve iş dikey penceresi akış toohello gidin. Altında **izleme**seçin **tanılama günlükleri**.

    ![Dikey gezinti toodiagnostics günlükleri](./media/stream-analytics-job-diagnostic-logs/image1.png)  

2.  Seçin **tanılamayı açın**.

    ![Tanılama günlüklerini Aç](./media/stream-analytics-job-diagnostic-logs/image2.png)

3.  Merhaba üzerinde **tanılama ayarları** sayfası için **durum**seçin **üzerinde**.

    ![Tanılama günlükleri için Durumu Değiştir](./media/stream-analytics-job-diagnostic-logs/image3.png)

4.  İstediğiniz hello arşivleme hedefi (depolama hesabı, olay hub'ı, günlük analizi) olarak ayarlayın. Ardından, toocollect (yürütme, yazma) istediğiniz günlükleri hello kategorilerini seçin. 

5.  Merhaba yeni tanılama yapılandırmayı kaydedin.

Merhaba tanılama yapılandırması yaklaşık 10 dakika tootake etkili olur. Bundan sonra hello günlüklerini yapılandırılmış hello arşivleme hedef görünen başlangıç (bunları hello görebilirsiniz **tanılama günlükleri** sayfa):

![Dikey gezinti toodiagnostics günlükleri - arşivleme hedefleri](./media/stream-analytics-job-diagnostic-logs/image4.png)

Tanılama yapılandırma hakkında daha fazla bilgi için bkz: [toplamak ve Azure kaynaklarınızı Tanılama verileri kullanma](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs).

## <a name="diagnostics-log-categories"></a>Kategoriler tanılama günlük

Şu anda, tanılama günlüklerini iki kategorisi Yakala:

* **Yazma**. Yakalamaları oturum ilgili toojob işlemlerini yazma olaylarını: iş oluşturma, ekleme ve girişleri ve çıkışları ekleme ve hello sorgu, başlatma ve durdurma hello iş güncelleştirme, silme.
* **Yürütme**. İş yürütme sırasında meydana gelen olayları yakalar:
    * Bağlantı hataları
    * Dahil olmak üzere, veri işleme hatalar:
        * Toohello uygun olmayan olaylar sorgu tanımı (eşleşmeyen alan türleri ve değerleri, eksik alanların vb.)
        * İfade değerlendirme hataları
    * Diğer olayları ve hataları

## <a name="diagnostics-logs-schema"></a>Tanılama günlüklerini şeması

Tüm günlükler JSON biçiminde depolanır. Her giriş ortak dize alanları aşağıdaki hello sahiptir:

Ad | Açıklama
------- | -------
time | Merhaba günlüğünün zaman damgası (UTC içinde).
resourceId | İşlemi hello hello kaynak Kimliğini, büyük harf yapıldı. Merhaba abonelik kimliği, hello kaynak grubu ve hello iş adı içerir. Örneğin,   **/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT. STREAMINGJOBS/STREAMANALYTICS/MYSTREAMINGJOB**.
category | Kategori ya da oturum **yürütme** veya **yazma**.
operationName | Oturum hello işlemin adı. Örneğin, **olayları göndermek: SQL çıktı yazma hatası toomysqloutput**.
durum | Merhaba işlem durumu. Örneğin, **başarısız** veya **başarılı**.
düzeyi | Günlük düzeyi. Örneğin, **hata**, **uyarı**, veya **bilgilendirici**.
properties | JSON bir dize olarak serileştirilmiş günlük girişi özgü ayrıntısı. Daha fazla bilgi için aşağıdaki bölümlerde hello bakın.

### <a name="execution-log-properties-schema"></a>Yürütme günlüğü özellikleri şeması

Yürütme günlüklerini Stream Analytics işi yürütme sırasında gerçekleşen olayları hakkında bilgi vardır. Özellikler Hello şeması, olay hello türüne bağlı olarak değişir. Şu anda, yürütme günlüklerini türleri aşağıdaki hello vardır:

### <a name="data-errors"></a>Veri hataları

Merhaba iş verileri işlerken oluşan herhangi bir hata Bu günlükler kategorisindedir. Bu günlükler en sık okunan, veri seri hale getirme, sırasında oluşturulur ve yazma işlemleri. Bu günlükler bağlantı hataları içermez. Bağlantı hataları, genel olaylar olarak kabul edilir.

Ad | Açıklama
------- | -------
Kaynak | Merhaba işinin adını giriş veya hello hatanın oluştuğu çıktı.
İleti | Merhaba hata ile ilişkili ileti.
Tür | Hata türü. Örneğin, **DataConversionError**, **CsvParserError**, veya **ServiceBusPropertyColumnMissingError**.
Veriler | Yararlıdır verileri içeren tooaccurately hello hatanın hello kaynağı bulun. Boyutuna bağlı olarak konu tootruncation.

Merhaba bağlı olarak **operationName** değerine veri hatalarını sahip şema aşağıdaki hello:
* **Olayları sıralamak**. Seri hale olayları olay okuma işlemleri sırasında oluşur. Bunlar durum, Hello hello giriş verileri hello sorgu şeması şu nedenlerden biriyle karşılamadığı oluşur:
    * *Tür uyumsuzluğu (de) olay sırasında seri*: hello hatasına neden hello alan tanımlar.
    * *Bir olay, geçersiz bir seri hale getirme okuyamıyor*: hello konumda hello hatanın oluştuğu hello giriş verileri hakkında bilgileri listeler. Blob giriş, uzaklık ve hello veri örneği için BLOB adı içerir.
* **Olayları göndermek**. Yazma işlemleri sırasında olaylarından gönderin. Bunlar hello hataya olay akışı hello tanımlayın.

### <a name="generic-events"></a>Genel olaylar

Genel olaylar şey kapsar.

Ad | Açıklama
-------- | --------
Hata | (isteğe bağlı) Hata bilgileri. Genellikle, varsa bu özel durum bilgilerini adıdır.
İleti| Günlük iletisi.
Tür | İleti türü. Hataların toointernal kategori eşler. Örneğin, **JobValidationError** veya **BlobOutputAdapterInitializationFailure**.
Bağıntı Kimliği | [GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) hello iş yürütme, benzersiz şekilde tanımlar. Başlangıç saati hello tüm yürütme günlüğü girişlerini iş başlatır sahip hello işi durur hello kadar aynı **bağıntı kimliği** değeri.

## <a name="next-steps"></a>Sonraki adımlar

* [Giriş tooStream analizi](stream-analytics-introduction.md)
* [Stream Analytics ile çalışmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Stream Analytics işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Stream Analytics sorgu dili başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Stream Analytics Yönetimi REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)
