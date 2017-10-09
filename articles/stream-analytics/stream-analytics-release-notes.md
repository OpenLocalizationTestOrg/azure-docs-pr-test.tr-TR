---
title: "aaaStream Analytics sürüm notları | Microsoft Docs"
description: "Stream Analytics sürüm notları"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5e59f893-cd2c-43fb-9eca-c146ce637203
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/03/2017
ms.author: jeffstok
ms.openlocfilehash: 1426ebc260be19fbde60518b25501fe53d908d46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-release-notes"></a>Stream Analytics sürüm notları

## <a name="notes-for-06142017-update-of-stream-analytics-tools-for-visual-studio"></a>Stream Analytics araçları 06/14/2017 güncelleştirme Visual Studio için Notlar
Bu güncelleştirme, Visual Studio Tools for paketidir. Bu sürüm hello aşağıdaki yeni özellikler içerir.

| Başlık | Açıklama |
| --- | --- |
| Java komut dosyası Düzenleyicisi desteği |Komut dosyası işlevleri, java oluşturduktan sonra hello yerel java komut dosyası Düzenleyicisi deneyimi keyfini çıkarabilirsiniz.|
| Görünüm iş yürütme zamanı hata iletisi | İş yürütme sırasında çalışma zamanı hataları varsa, hello görünen zaman penceresi ayarlayarak bunları hello hataları sekmesinde görüntüleyebilirsiniz. Varsayılan olarak son 30 dakika boyunca hello hata iletilerini gösterir. |
| Yerel test giriş CSV ve Avro desteği | JSON yanı sıra, artık yerel test girdi için CSV ve Avro dosya biçimi kullanabilir.|

## <a name="notes-for-05032017-update-of-stream-analytics"></a>Stream Analytics 03/05/2017 güncelleştirilmesi için Notlar
Bu güncelleştirme bizim için sorun giderme belgelerine sürümüdür.

Merhaba [sorun giderme kılavuzu](stream-analytics-troubleshooting-guide.md) ve diğer belgeleri serbest bırakıldı. Lütfen gözden geçirin, geri bildirim Hoş Geldiniz.

## <a name="notes-for-04242017-update-of-stream-analytics-tools-for-visual-studio"></a>Stream Analytics araçları 24/04/2017 güncelleştirme Visual Studio için Notlar
Bu güncelleştirme, Visual Studio Tools for paketidir. Bu sürüm hello aşağıdaki yeni özellikler içerir.

| Başlık | Açıklama |
| --- | --- |
| Visual Studio'da yerel test sonucu görüntüleyin | tooview hello çıktı hello yerel sonucunu sınamak, yalnızca hello çıkış konsol penceresinde ENTER tuşuna basın veya kapatın. Visual Studio'da penceresinde, tablo biçiminde Hello sonuç gösterilir. |
| Çıkış JSON biçiminde yerel sonucu | Yerel bir test çalıştırdığınızda, hem JSON hem de CSV dosya biçimleri gibi hello elde edilen sonucu oluşturulur. |
| BLOB/tablo depolama girdi/çıktı verilerini Önizleme | Çift bir blob veya tablo depolama hello iş görünümünde giriş/çıkış tıklayarak, Visual Studio içinde hello verileri kolayca önizleyebilirsiniz. |
| Giriş/Çıkış hata iletisini görüntüleme | Bazı çalışma zamanı hataları ilgili tooyou işin girişleri veya çıkışları varsa, bunu burada üzerine gelme üzerinde hello iş diyagramında gösterilir toosee hello ayrıntılı hata iletisi.|


## <a name="notes-for-02012017-release-of-stream-analytics"></a>Stream Analytics 02/01/2017 sürümünün notları
Bu sürüm, güncelleştirmenin ardından hello içerir.

| Başlık | Açıklama |
| --- | --- |
| JavaScript kullanıcı tanımlı işlevler (UDF) Tanıtımı |[Java kullanıcı tanımlı işlevler](stream-analytics-javascript-user-defined-functions.md) sorgular oluşturma ek esneklik için kullanıma sunulmuştur. |
| Visual Studio ve akış analizi için giriş araçları |[Visual Studio Araçları](stream-analytics-tools-for-visual-studio.md) artık için hata ayıklama ve büyük yardımcı programı kullanılabilir. |
| Tanılama günlük Tanıtımı |[Tanılama günlük](stream-analytics-job-diagnostic-logs.md) için ek sorun giderme seçenekleri kullanıma sunulmuştur. |
| Giriş Jeo-uzamsal işlevleri |[Jeo-uzamsal işlevleri](http://msdn.microsoft.com/library/mt778980(Azure.100).aspx) genel kullanıma sunulmuştur. |

## <a name="notes-for-04152016-release-of-stream-analytics"></a>Akış analizi, 15/04/2016 sürüm notları
Bu sürüm, güncelleştirmenin ardından hello içerir.

| Başlık | Açıklama |
| --- | --- |
| Power BI için genel kullanılabilirlik çıkarır |[Power BI çıkışınızın](stream-analytics-power-bi-dashboard.md) genel kullanıma sunulmuştur. Power BI için Hello 90 günlük yetkilendirme sona erme kaldırılmıştır. Burada yetkilendirme gereken yenilendi toobe senaryoları hakkında daha fazla bilgi için bkz: Merhaba [yetkilendirmeyi yenileyin](stream-analytics-power-bi-dashboard.md#renew-authorization) Power BI panosu oluşturma bölümü. |

## <a name="notes-for-03032016-release-of-stream-analytics"></a>Akış analizi, 03/03/2016 sürüm notları
Bu sürüm, güncelleştirmenin ardından hello içerir.

| Başlık | Açıklama |
| --- | --- |
| Yeni akış analizi sorgu dili öğeleri |SAQL artık sahiptir [GetType](https://msdn.microsoft.com/library/azure/mt643890.aspx "GetType MSDN sayfasını"), [TRY_CAST](https://msdn.microsoft.com/library/azure/mt643735.aspx "TRY_CAST MSDN sayfasını") ve [regexmatch'İŞLEVİNİN] (https://msdn.microsoft.com/library/azure/mt643891.aspx "Regexmatch'İŞLEVİNİN MSDN sayfasını"). |

## <a name="notes-for-12102015-release-of-stream-analytics"></a>Akış analizi, 12/10/2015 sürüm notları
Bu sürüm, güncelleştirmenin ardından hello içerir.

| Başlık | Açıklama |
| --- | --- |
| REST API sürümü güncelleştirme |Merhaba REST API sürümü güncelleştirilmiş too2015-10-01 olmuştur. Ayrıntılar, MSDN üzerinde bulunabilir [Stream Analytics Yönetimi REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx) ve [akış analizi, Machine Learning tümleştirme](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md). |
| Azure Machine Learning tümleştirme |Azure Machine Learning kullanıcı tanımlı işlevler için destek bu sürüm ile birlikte gelir. Merhaba bkz [öğretici](stream-analytics-machine-learning-integration-tutorial.md) hello yanı sıra daha fazla bilgi için [genel blog duyuru](http://blogs.technet.com/b/machinelearning/archive/2015/12/10/apply-azure-ml-as-a-function-in-azure-stream-analytics.aspx). |

## <a name="notes-for-11122015-release-of-stream-analytics"></a>Akış analizi, 11/12/2015 sürüm notları
Bu sürüm, güncelleştirmenin ardından hello içerir.

| Başlık | Açıklama |
| --- | --- |
| Yeni davranışını seçin |Genişletilmiş tooallow Stream Analytics SELECT * özellik erişimcisini iç içe geçmiş kaydı olarak. Daha fazla bilgi için bakın [http://msdn.microsoft.com/library/mt622759.aspx](http://msdn.microsoft.com/library/mt622759.aspx "karmaşık veri türlerini"). |

## <a name="notes-for-10222015-release-of-stream-analytics"></a>Akış analizi, 22/10/2015 sürüm notları
Bu sürüm hello şu güncelleştirmeleri içerir.

| Başlık | Açıklama |
| --- | --- |
| Ek sorgu dil özellikleri |Akış analizi genişletilmiş hello sorgu dili özellikler aşağıdaki hello dahil ederek: [ABS](https://msdn.microsoft.com/library/azure/mt574054.aspx), [TAVAN](https://msdn.microsoft.com/library/azure/mt605286.aspx), [EXP](https://msdn.microsoft.com/library/azure/mt605289.aspx), [kat](https://msdn.microsoft.com/library/azure/mt605240.aspx), [Güç](https://msdn.microsoft.com/library/azure/mt605287.aspx), [oturum](https://msdn.microsoft.com/library/azure/mt605290.aspx), [KARE](https://msdn.microsoft.com/library/azure/mt605288.aspx), ve [SQRT](https://msdn.microsoft.com/library/azure/mt605238.aspx). |
| Birleşik kısıtlamaları kaldırıldı |Bu sürüm sorguda 15 Toplamaların hello sınırlamayı kaldırır. Hiçbir toohello sayısı sınırı sorgu başına toplamalar artık yoktur. |
| Eklenen grubu tarafından System.Timestamp özelliği |Merhaba [GROUP BY](https://msdn.microsoft.com/library/azure/dn835023.aspx) işlevi artık ya da window_type için izin verir veya [System.Timestamp](https://msdn.microsoft.com/library/azure/mt598501.aspx). |
| Dönen ve windows atlaması için eklenen UZAKLIĞI |Varsayılan olarak, [dönen](https://msdn.microsoft.com/library/azure/dn835055.aspx) ve [Hopping](https://msdn.microsoft.com/library/azure/dn835041.aspx) windows karşı süresini sıfır hizalı (1/1/0001 12:00:00 AM UTC). özel bir uzaklık (veya hizalama) Hello yeni (isteğe bağlı) parametre 'offsetsize' olarak belirtebilirsiniz. |

## <a name="notes-for-09292015-release-of-stream-analytics"></a>Akış analizi, 29/09/2015 sürüm notları
Bu sürüm hello şu güncelleştirmeleri içerir.

| Başlık | Açıklama |
| --- | --- |
| Azure IOT paketi genel Önizleme |Akış analizi hello hello Azure IOT paketi genel önizlemesini dahil edilir. |
| Azure Portal tümleştirme |Toplama toocontinued bulunması hello Azure Yönetim Portalı'nda, Stream Analytics hello şimdi tümleşik [Azure Portal](https://azure.microsoft.com/overview/preview-portal/). Stream Analytics işlevselliği hello Önizleme portalında şu anda Power BI yapılandırma ve tooor yeni oluşturma gözatma çıkış tarayıcı içi sorgu testi, desteği olmadan hello Azure Yönetim Portalı'nda hello işlevlerinin bir alt kümesini sunulan olduğuna dikkat edin Giriş ve çıkış kaynakları Aboneliklerde erişebilirsiniz. |
| Cosmos DB çıkış desteği |Akış analizi işleri şimdi çıktı çok[Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/). |
| IOT Hub giriş desteği |Akış analizi işleri, artık IOT hub'ları verileri işleyebilen. |
| Zaman damgası tarafından heterojen olayları için |Tek veri akışı zaman damgaları farklı alanlara sahip birden çok olay türünü içeriyorsa, artık kullanabilirsiniz [TIMESTAMP BY](http://msdn.microsoft.com/library/mt573293.aspx) alanlarla ifadeleri toospecify farklı zaman damgası her örneği için. |

## <a name="notes-for-09102015-release-of-stream-analytics"></a>Akış analizi, 10/09/2015 sürüm notları
Bu sürüm hello şu güncelleştirmeleri içerir.

| Başlık | Açıklama |
| --- | --- |
| Powerbı grupları için destek |Stream Analytics işleri şimdi yazabilirler çok diğer Power BI kullanıcıları ile veri paylaşımı tooenable[Powerbı grupları](stream-analytics-define-outputs.md#power-bi) Power BI hesabınızı içinde. |

## <a name="notes-for-08202015-release-of-stream-analytics"></a>Akış analizi, 20/08/2015 sürüm notları
Bu sürüm hello şu güncelleştirmeleri içerir.

| Başlık | Açıklama |
| --- | --- |
| Eklenen son işlevi |Merhaba [son](http://msdn.microsoft.com/library/mt421186.aspx) işlevi artık kullanılabilir durumdadır, Stream Analytics işlerini, belirli bir zaman çerçevesi içinde bir olay akışında tooretrieve hello en son olay etkinleştirme. |
| Yeni dizi işlevleri |Dizi işlevleri [GetArrayElement](http://msdn.microsoft.com/library/mt270218.aspx), [GetArrayElements](http://msdn.microsoft.com/library/mt298451.aspx) ve [GetArrayLength](http://msdn.microsoft.com/library/mt270226.aspx) kullanıma sunulmuştur. |
| Yeni kayıt işlevleri |Kayıt işlevleri [GetRecordProperties](http://msdn.microsoft.com/library/mt270221.aspx) ve [getrecordpropertyvalue'öğesinin](http://msdn.microsoft.com/library/mt270220.aspx) kullanıma sunulmuştur. |

## <a name="notes-for-07302015-release-of-stream-analytics"></a>Akış analizi, 07/30/2015 sürüm notları
Bu sürüm hello şu güncelleştirmeleri içerir.

| Başlık | Açıklama |
| --- | --- |
| Power BI kurum Azure kimliğinden ayrılmış kimliği |Bu özellik sağlar [Power BI çıkışı](stream-analytics-power-bi-dashboard.md) ASA işleri herhangi bir Azure hesabı türü (Live ID veya kurum kimliği) altında. Ayrıca, Azure hesabınız için bir kuruluş kimliğine sahip ve Power BI çıkışı yetkilendirmek için farklı bir tane kullanın. |
| Hizmet veri yolu kuyrukları çıkış desteği |[Hizmet veri yolu kuyrukları](stream-analytics-define-outputs.md#service-bus-queues) çıkışları Stream Analytics işlerine hazırdır. |
| Hizmet veri yolu konuları çıkış desteği |[Hizmet veri yolu konuları](stream-analytics-define-outputs.md#service-bus-topics) çıkışları Stream Analytics işlerine hazırdır. |

## <a name="notes-for-07092015-release-of-stream-analytics"></a>Akış analizi, 07/09/2015 sürüm notları
Bu sürüm hello şu güncelleştirmeleri içerir.

| Başlık | Açıklama |
| --- | --- |
| Özel Blob çıkış bölümlendirme |BLOB Depolama çıkışları şimdi BLOB çıkış bir seçenek toospecify hello sıklığı yazılır ve veri yolu klasör yapısı hello yapısı ve hello biçimini çıkış izin verin. |

## <a name="notes-for-05032015-release-of-stream-analytics"></a>Akış analizi, 03/05/2015 sürüm notları
Bu sürüm hello şu güncelleştirmeleri içerir.

| Başlık | Açıklama |
| --- | --- |
| Artan en büyük değer sırası tolerans penceresi |Merhaba sırası tolerans penceresi için en büyük boyut Hello şimdi 59:59 (dd: ss): |
| JSON çıktı biçimi: Ayrılmış satırı veya dizi |Şimdi tooBlob depolama veya olay hub'ı toooutput ya da bir dizi olarak JSON nesnelerinin veya JSON nesnelerini içeren yeni bir satır ayırma tarafından alırken bir seçenek yoktur. |

## <a name="notes-for-04162015-release-of-stream-analytics"></a>Akış analizi, 16/04/2015 sürüm notları
| Başlık | Açıklama |
| --- | --- |
| Azure depolama hesabı yapılandırmasında gecikme |Akış analizi işi hello için bölgede ilk kez oluştururken, yeni bir depolama hesabı istendiğinde toocreate olması veya bu bölgede Stream Analytics işlerini izleme için var olan bir hesap belirtin. Son toolatency izleme yapılandırılırken, başka bir Stream Analytics işi 30 dakika içinde aynı bölgede hello gösteren yerine ikinci bir depolama hesabının hello belirtmek için sorar hello oluşturmak son hello izleme depolama birinde yapılandırılmış Aşağı açılan hesap. gereksiz bir depolama hesabı oluşturma tooavoid bu bölgede başka işler sağlamadan önce ilk kez hello için bölgede bir işi oluşturduktan sonra 30 dakika bekleyin. |
| Proje yükseltme |Şu anda Stream Analytics, Canlı düzenlemeler toohello tanımı veya çalışan bir işi yapılandırılmasını desteklemez. Sipariş toochange hello giriş, çıkış, sorgu, Ölçek veya çalışan bir işi yapılandırmasını, hello iş durdurmanız gerekir. |
| Giriş kaynağından çıkarımı yapılan veri türleri |CREATE TABLE deyimi kullanılmazsa, giriş biçiminden türetilmiş hello giriş türü, örneğin CSV tüm alanları dize. Alanları gerek toobe açıkça sipariş tooavoid türü uyuşmazlığı hataları hello CAST işlevini kullanarak toohello sağ türünü dönüştürülür. |
| Eksik alanların null değerler olarak yüzdelik |Merhaba giriş kaynağı var olmayan bir alan başvuran hello çıkış olay null değerler neden olur. |
| SELECT deyimi ifadelerle gelmelidir |Sorgunuzda, alt sorgular deyimleri ile tanımlanan SELECT deyimi izlemeniz gerekir. |
| Bellek sorunu |Düzen dışı olayları ve/veya karmaşık sorgular durum, büyük bir miktarını hello iş toorun yetersiz bellek, bir işin kaynaklanan neden olabilecek bakımı için büyük bir tolerans ile akış analizi işi yeniden başlatın. Merhaba başlatma ve durdurma işlemlerini hello işin işlem günlükleri görünür olacaktır. tooavoid Bu davranış, birden çok bölüm arasında out ölçek hello sorgu. Bir sonraki sürümde bu sınırlamaya bunları yeniden başlatmak yerine etkilenen işlerini performansı önemli tarafından ele alınacaktır. |
| Büyük blob girişleri yükü zaman damgası olmadan bellek yetersiz soruna neden olabilir |Blob depolama biriminden büyük dosyaları kullanma, zaman damgası alanı zaman damgası tarafından belirtilmezse, Stream Analytics işleri toocrash neden olabilir. tooavoid Bu sorun, her bir blob altında 10 MB boyutunda tutun. |
| SQL veritabanı olay birim sınırlaması |SQL veritabanı bir çıktı hedefi olarak kullanırken, çıktı verilerini çok yüksek miktarda hello Stream Analytics işi tootime çıkışı neden olabilir. ya da bu sorunu tooresolve toplamalar veya filtre işleçleri kullanarak hello çıktı miktarının azaltılmasını veya Azure Blob Depolama veya olay hub'ları bir çıktı hedefi olarak bunun yerine seçin. |
| Power BI veri kümeleri yalnızca bir tablo içerebilir |Powerbı sağlanan bir veri kümesinde birden fazla tablo desteklemiyor. |

## <a name="get-help"></a>Yardım alın
Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)
