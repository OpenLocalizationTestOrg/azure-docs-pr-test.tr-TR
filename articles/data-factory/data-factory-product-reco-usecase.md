---
title: "aaaData Fabrika kullanım örneği - ürün önerileri"
description: "Diğer hizmetlerin yanı sıra Azure Data Factory kullanarak uygulanan bir kullanım durumu hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6f1523c7-46c3-4b8d-9ed6-b847ae5ec4ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: d7912965fe4762d64e8ca3c28381ea6187f36631
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---product-recommendations"></a>Kullanım Örneği - Ürün Önerileri
Azure Data Factory birçok kullanılan hizmetler tooimplement hello Cortana Intelligence Suite Çözüm Hızlandırıcıları, biridir.  Bkz: [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics) bu paketi hakkında ayrıntılar için sayfa. Bu belgede, Azure kullanıcıların zaten Çözüldü ve Azure Data Factory ve diğer Cortana Intelligence Bileşen Hizmetleri kullanılarak uygulanan ortak bir kullanım örneği açıklanmaktadır.

## <a name="scenario"></a>Senaryo
Müşteriler toopurchase ürünlerini yaygın olarak istediğiniz tooentice bunları oldukları ürünlerle büyük olasılıkla toobe ilginizi ve bu nedenle büyük olasılıkla toobuy sunarak çevrimiçi Perakendeciler. tooaccomplish Bu, çevrimiçi Perakendeciler gereksinim toocustomize kendi kullanıcının çevrimiçi deneyimi, belirli bir kullanıcı için kişiselleştirilmiş ürün önerilerini kullanarak. Bu kişiselleştirilmiş geçerli ve geçmiş alışveriş davranışı verilerini üzerinde ürün bilgilerini göre yapılan toobe yeni markalar ve ürün ve müşteri Segment veri sunulan önerilerdir.  Ayrıca, bunlar birlikte, tüm kullanıcıların genel kullanım davranış analizini göre hello kullanıcı ürün önerilerini sağlayabilir.

Bu perakende Hello amacı toooptimize kullanıcı tıklatın satış dönüştürmeleri için olduğundan ve daha yüksek satış gelirinin kazanırsınız.  Bunlar, bu dönüştürme Müşteri ilgi alanları ve Eylemler dayalı olarak bağlamsal, davranış tabanlı ürün öneriler sunarak elde edin. Bu kullanım durumu için örnek olarak, müşterileri için toooptimize isteyen işletmeler çevrimiçi Perakendeciler kullanın. Ancak, bu ilkeler, müşterilerinin kendi mal ve hizmet çevresinde tooengage istediği tooany iş uygulayın ve müşterilerin satın alma kişiselleştirilmiş ürün önerilerini deneyiminizi geliştirmek.

## <a name="challenges"></a>Zorlukları
Birçok zorluklar mevcuttur, çevrimiçi Perakendeciler yüz tooimplement kullanım örneği bu tür çalışırken. 

İlk olarak, farklı boyutlarda ve şekiller verilerin birden çok veri kaynaklarından alınan gerekir hem şirket içi ve hello bulutta. Merhaba kullanıcı hello çevrimiçi perakende site gözatar olarak bu veriler ürün verilerini, geçmiş müşteri davranışı verileri ve kullanıcı verilerini içerir. 

İkinci, kişiselleştirilmiş ürün önerilerini makul ve doğru şekilde hesaplanan tahmin ve gerekir. Ayrıca tooproduct, marka ve müşteri verileri davranışı ve tarayıcı, çevrimiçi Perakendeciler hello kullanıcıdan ayrıca hello en iyi ürün önerilerini hello belirlenmesi, geçmiş satın alma işlemleri toofactor tooinclude müşteri geri bildirimi gerekir. 

Üçüncü hello önerileri hemen teslim edilebilir toohello kullanıcı tooprovide sorunsuz gözatma ve deneyimi satın alma ve gerekir hello en son ve ilgili öneriler sağlar. 

Son olarak, perakende genel yukarı satış izleyerek kendi yaklaşım toomeasure hello verimliliğini gerekir ve çapraz satış tıklatın dönüştürme satış başarı ve tootheir gelecekteki önerileri ayarlayın.

## <a name="solution-overview"></a>Çözüme genel bakış
Bu örnek kullanım örneği Çözüldü ve Azure Data Factory ve de dahil olmak üzere diğer Cortana Intelligence component services kullanarak gerçek Azure kullanıcılar tarafından uygulanan [Hdınsight](https://azure.microsoft.com/services/hdinsight/) ve [Power BI](https://powerbi.microsoft.com/).

Merhaba çevrimiçi satıcısı kendi veri depolama seçenekleri hello iş akışı boyunca olarak Azure Blob Depolama, bir şirket içi SQL server, Azure SQL DB ve bir ilişkisel veri reyonu kullanır.  Merhaba blob deposu, müşteri bilgileri, müşteri davranışı verileri ve ürün bilgi verilerini içerir. Merhaba ürün bilgisi verileri ürün marka bilgileri ve ürün kataloğu içerir şirket içi bir SQL veri ambarında depolanır. 

Tüm hello veriler birleştirilmiş ve ürünleri hello Web sitesinde hello kataloğunda hello kullanıcı gözatar müşteri ilgi alanları ve Eylemler, tabanlı bir ürün öneri sistem kişiselleştirilmiş toodeliver önerileri içine ssas'nin. Merhaba müşterileri de toohello ürün bakarak bir kullanıcı ilgili tooany olmayan genel Web sitesi kullanım düzenlerini esas alarak ilgili ürünler bakın.

![Kullanım örneği diyagramı](./media/data-factory-product-reco-usecase/diagram-1.png)

Ham web günlüğü dosyalarını gigabayt olarak yarı yapılandırılmış dosyaları günlük hello çevrimiçi satıcısında'nın Web sitesinden üretilir. Ham web günlüğü dosyalarını hello ve hello müşteri ve ürün kataloğu bilgilerini düzenli olarak veri fabrikasının genel olarak dağıtılmış veri taşıma hizmeti olarak kullanarak bir Azure Blob depolama alanına alınan. Merhaba ham günlük dosyalarını hello gün için uzun vadeli depolama için blob depolama birimindeki (yıl ve ay) bölümlenir.  [Azure Hdınsight](https://azure.microsoft.com/services/hdinsight/) Hive veya Pig betikleri kullanarak ölçekli depolama ve işlem alınan hello günlüklerini hello blob kullanılan toopartition hello ham günlük dosyalarında olduğu. veriler bölümlenmiş web günlüklerini hello sonra işlenen tooextract hello girişleri öneri sistem toogenerate kişiselleştirilmiş hello ürün önerilerini öğrenme bir makine için gerekli.

Merhaba Bu örnekte hello machine learning için kullanılan öneri öneri platformundan öğrenme bir açık kaynak makine sistemidir [Apache Mahout](http://mahout.apache.org/).  Tüm [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) veya özel model uygulanan toohello senaryo olabilir.  Genel kullanım düzenlerini esas alarak hello Web sitesinde öğeleri ve hello bireysel kullanıcıyı temel alarak toogenerate kişiselleştirilmiş hello önerileri arasında kullanılan toopredict hello benzerlik Hello Mahout modelidir.

Son olarak, hello sonuç kişiselleştirilmiş ürün önerilerini tüketimi hello satıcısında Web sitesi tarafından taşınan tooa ilişkisel veri reyonu kümesidir.  Hello sonuç kümesi, doğrudan blob depolama alanından başka bir uygulama tarafından erişilemedi veya diğer tüketicilerin ve kullanım örnekleri için tooadditional depoları taşınır.

## <a name="benefits"></a>Avantajlar
Kendi ürün öneri stratejisi en iyi duruma getirme ve iş hedeflerini ile hizalama hello çözüm hello çevrimiçi Satıcısı'nın ticaret ve hedefleri pazarlama karşılıyor. Ayrıca, mümkün toooperationalize olan ve hello ürün öneri akışını verimli, güvenilir ve uygun maliyetli bir şekilde yönetin. Merhaba yaklaşım yaptığı kolay kendileri için tooupdate kendi model ve satış tıklatın dönüştürme başarıları hello ölçüler üzerinde temel verimliliğinden ince ayar yapma. Azure Data Factory kullanarak kendi zaman alabilir ve pahalı el ile bulut kaynak yönetimi mümkün tooabandon olan ve tooon isteğe bulut kaynak yönetimi taşıyın. Bu nedenle, mümkün toosave sürenin, para ve bunların zamanı toosolution dağıtımı azaltır. Veri çizgileri görünümleri ve işletimsel hizmet durumu kolay toovisualize hale geldi ve hello Data Factory sezgisel izleme ve yönetim hello Azure portal ' kullanılabilir kullanıcı Arabirimi ile ilgili sorunları giderme. Kendi çözüm şimdi zamanlanmış ve böylece bitmiş veri güvenilir bir şekilde üretilen ve toousers teslim ve verileri ve işleme bağımlılıkları insan etkileşimi olmadan otomatik olarak yönetilir yönetilir.

Bu kişiselleştirilmiş alışveriş deneyimi sağlayarak hello daha fazla rekabet çekici bir müşteri oluşturulan çevrimiçi satıcısında deneyimi ve bu nedenle satış ve genel müşteri memnuniyetini artırın.

