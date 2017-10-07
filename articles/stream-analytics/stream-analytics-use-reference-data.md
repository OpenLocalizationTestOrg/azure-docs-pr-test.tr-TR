---
title: "Stream Analytics içinde aaaUse başvuru verileri ve arama tabloları | Microsoft Docs"
description: "Stream Analytics sorgu başvuru verileri kullanın"
keywords: "Arama tablosu, başvuru verileri"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 06103be5-553a-4da1-8a8d-3be9ca2aff54
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: fb1d18fba920db5e097d0c95d333e8e8390d1589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-reference-data-or-lookup-tables-in-a-stream-analytics-input-stream"></a>Başvuru verileri veya arama tabloları bir akış analizi Giriş akışı kullanma
Başvuru verileri (arama tablosu olarak da bilinir) statik sınırlı bir veri kümesi veya yavaşlamasının doğası gereği değiştirme tooperform arama veya toocorrelate veri akışı ile kullanılır. başvuru verileri toomake kullanımını, Azure Stream Analytics işinde genellikle kullanacağınız bir [başvuru veri birleştirme](https://msdn.microsoft.com/library/azure/dn949258.aspx) Sorgunuzdaki. Akış analizi başvuru verileri için hello depolama katmanı olarak Azure Blob Depolama kullanır ve Azure Data Factory başvurusuyla, gelen, başvuru verileri olarak kullanmak için dönüştürülmüş ve/veya kopyalanan tooAzure Blob Depolama veri olabilir [bulut tabanlı herhangi bir sayıda ve Şirket içi veri depolarına](../data-factory/data-factory-data-movement-activities.md). Başvuru verileri hello hello blob adı alanında belirtilen tarih artan BLOB'lar (Merhaba giriş yapılandırmada tanımlanan) dizisi olarak modellenir. Bu **yalnızca** toohello hello dizinin sonuna bir tarih/saat kullanarak eklenmesini destekler **büyük** bir hello sırasında hello son blob tarafından belirtilen hello daha.

Akış analizi sahip bir **blob 100 MB sınırı** ancak işleri hello kullanarak birden çok başvuru BLOB'lar işlenebilecek **yol deseni** özelliği.


## <a name="configuring-reference-data"></a>Başvuru verileri yapılandırma
tooconfigure başvuru verilerinizi önce toocreate türünde bir girdi gerekir **başvuru verileri**. Merhaba tabloda tooprovide açıklamasını ile Merhaba başvuru veri girişi oluşturulurken gerekir her bir özellik açıklanmaktadır:


<table>
<tbody>
<tr>
<td>Özellik adı</td>
<td>Açıklama</td>
</tr>
<tr>
<td>Giriş diğer adı</td>
<td>Merhaba iş sorgu tooreference bu giriş kullanılacak bir kolay ad.</td>
</tr>
<tr>
<td>Depolama hesabı</td>
<td>Merhaba depolama hesabı bloblarınızın bulunduğu Hello adı. Hello ise, akış analizi işi aynı abonelik, seçebileceğiniz, hello açılır.</td>
</tr>
<tr>
<td>Depolama hesabı anahtarı</td>
<td>Merhaba depolama hesabıyla ilişkili hello gizli anahtar. Hello Hello depolama hesabı ise, bu otomatik olarak doldurulur, Stream Analytics işi aynı abonelik.</td>
</tr>
<tr>
<td>Depolama kapsayıcısı</td>
<td>Kapsayıcılar hello Microsoft Azure Blob hizmeti depolanan BLOB'lar için mantıksal bir gruplandırmasını sağlar. Blob toohello Blob hizmeti karşıya yüklediğinde, o blob için bir kapsayıcı belirtmeniz gerekir.</td>
</tr>
<tr>
<td>Yol deseni</td>
<td>Merhaba yolu toolocate hello belirtilen kapsayıcı içinde bloblarınızın kullanılır. Hello yol içinde şu 2 değişkenin hello bir veya daha fazla örneğini toospecify seçebilirsiniz:<BR>{date} {time}<BR>Örnek 1: products/{date}/{time}/product-list.csv<BR>Örnek 2: products/{date}/product-list.csv
</tr>
<tr>
<td>[İsteğe bağlı] tarih biçimi</td>
<td>Belirttiğiniz yol deseni hello içinde {date} kullandıysanız, bloblarınızın organize edilmiştir hello tarih biçimi hello açılan listeden desteklenen biçimlerden birini seçebilirsiniz.<BR>Örnek: YYYY/AA/GG, GG/AA/YYYY, vs.</td>
</tr>
<tr>
<td>[İsteğe bağlı] saat biçimi</td>
<td>Belirttiğiniz yol deseni hello içinde {time} kullandıysanız, bloblarınızın organize edilmiştir hello saat biçimi hello açılan listeden desteklenen biçimlerden birini seçebilirsiniz.<BR>Örnek: Ss, ss/dd veya HH mm</td>
</tr>
<tr>
<td>Olayı seri hale getirme biçimi</td>
<td>sorgularınızın beklediğiniz hello şekilde Stream Analytics çalışıp çalışmadığından emin toomake hangi serileştirme biçimini gelen veri akışları için kullanmakta olduğunuz tooknow gerekir. Başvuru verileri için CSV ve JSON hello desteklenen biçimler şunlardır.</td>
</tr>
<tr>
<td>Encoding</td>
<td>Merhaba, kodlama biçimi yalnızca şu anda desteklenen. UTF-8 dir</td>
</tr>
</tbody>
</table>

## <a name="generating-reference-data-on-a-schedule"></a>Başvuru verileri bir zamanlama oluşturma
Başvuru verileri yavaş değişen bir veri kümesi ise, başvuru verileri yenilemek için destek hello {date} ve {time} değiştirme belirteçleri kullanarak hello giriş yapılandırmasında bir yol deseni belirterek etkinleştirilir. Bu yol deseni temel alınarak güncelleştirildi hello başvuru veri tanımlarını Yukarı Akış analizi seçer. Örneğin, bir düzeni `sample/{date}/{time}/products.csv` bir tarih biçimi ile **"YYYY-AA-GG"** ve bir saat biçimini **"Ss-dd"** güncelleştirilmiş hello blob Yukarı Akış analizi toopick bildirir `sample/2015-04-16/17-30/products.csv` 17:30:00 saatleri Nisan üzerinde adresindeki 16, 2015 UTC saat dilimi.

> [!NOTE]
> Şu anda yalnızca hello makine süresini hello blob adı kodlanmış toohello zaman ilerler, akış analizi işleri hello blob yenileme için bakın. Örneğin, hello iş şuna `sample/2015-04-16/17-30/products.csv` 17:30:00 saatleri 16 Nisan 2015 UTC üzerinde daha olası ancak daha önce hiçbir bölge Zaman hemen sonra. İçinde *hiçbir zaman* bulunduğundan sonuncu hello daha önce kodlanmış bir zaman bir blob arayın.
> 
> Örneğin Merhaba iş hello blob bulduğunda `sample/2015-04-16/17-30/products.csv` 17:30:00 saatleri 16 Nisan 2015'ten önce kodlanmış bir tarih ile herhangi bir dosya yoksayacak bunu geç ulaşan varsa `sample/2015-04-16/17-25/products.csv` blob hello oluşturulan aynı kapsayıcı hello iş onu kullanmaz.
> 
> Benzer şekilde, `sample/2015-04-16/17-30/products.csv` yalnızca 10:03 PM 16 Nisan 2015 oluşturulur ancak hiçbir blob daha önceki bir tarihi ile Merhaba kapsayıcıda mevcut olduğundan, hello iş 10:03 PM 16 Nisan 2015 başlayarak bu dosyayı kullanmak ve o zamana kadar hello önceki başvuru verileri kullanın.
> 
> Bir özel durum toothis hello işi geçmişe toore işlem verileri gerektiğinde veya hello iş ilk kez başlatıldığında ' dir. Başlangıçta süresi hello işi hello en son blob hello işi başlatmadan önce belirtilen süre üretilen için arıyor. Bu var. tooensure yapılır bir **boş** hello işi başladığında veri kümesi başvurusu. Bir bulunamazsa hello iş tanılama aşağıdaki hello görüntüler: `Initializing input without a valid reference data blob for UTC time <start time>`.
> 
> 

[Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) Stream Analytics tooupdate başvuru veri tanımlarını tarafından gerekli güncelleştirilmiş hello BLOB'ları oluşturma kullanılan tooorchestrate hello görev olabilir. Veri Fabrikası düzenler ve hello taşınmasını ve dönüştürülmesini veri otomatikleştiren bir bulut tabanlı veri tümleştirme hizmetidir. Veri Fabrikası destekleyen [tooa çok sayıda bulut tabanlı ve şirket içi veri depolarına bağlanma](../data-factory/data-factory-data-movement-activities.md) ve taşıma verileri kolayca belirttiğiniz düzenli bir zamanlamaya göre. Daha fazla bilgi ve nasıl tooset Data Factory yukarı kanal toogenerate başvuru verileri, önceden tanımlanmış bir zamanlamayla yenilenir akış analizi için adım adım yönergeler için bu denetleyin [GitHub örnek](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs).

## <a name="tips-on-refreshing-your-reference-data"></a>Başvuru verileriniz yenilenirken ipuçları
1. Başvuru verileri BLOB'ları üzerine Stream Analytics tooreload hello blob neden olmaz ve bazı durumlarda hello iş toofail neden olabilir. Merhaba önerilen yolu toochange başvuru verileri aynı kapsayıcı ve yol deseni tanımlanan hello iş girişinde hello kullanarak yeni bir blob tooadd olduğundan ve bir tarih/saat **büyük** bir hello sırasında hello son blob tarafından belirtilen hello daha.
2. Başvuru verileri BLOB'ları olan **değil** hello blob'un "Son değiştirilme" zamanı ancak yalnızca başlangıç saatini ve tarihini hello {date} ve {time} değişimler kullanarak hello blob adında belirtilen tarafından sıralanan.
3. Bazı durumlarda üzerinde bir iş zamanında geri gitmeniz gerekir, bu nedenle başvuru verileri BLOB'ları değiştirilmiş silinmiş ya da gerekir değil.

## <a name="get-help"></a>Yardım alın
Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.

## <a name="next-steps"></a>Sonraki adımlar
Sunulan tooStream Analytics, hello nesnelerin interneti verilerini analytics akış için yönetilen bir hizmet olan. Bu hizmet hakkında daha fazla toolearn bakın:

* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.get.started]: stream-analytics-get-started.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
