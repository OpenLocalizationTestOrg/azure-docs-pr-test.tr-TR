---
title: aaaWhat olan Azure Search | Microsoft Docs
description: "Azure arama, tam olarak yönetilen barındırılan bulut arama hizmetidir. Bu özellik genel bakışı daha fazla bilgi edinin."
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 50bed849-b716-4cc9-bbbc-b5b34e2c6153
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/26/2017
ms.author: ashmaka
ms.openlocfilehash: b38a7e93a7f0e0d5f8a3779858032271b3883778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-search"></a>Azure Search nedir?
Azure arama geliştiricilere API'ler sağlar ve web, mobil ve kurumsal uygulamalarda, veriler üzerinde zengin arama deneyimi eklemek için Araçlar bir bulut hizmet olarak arama çözümüdür.

Basit bir işlevselliği kullanıma sunulan [REST API](/rest/api/searchservice/) veya [.NET SDK'sı](search-howto-dotnet-sdk.md) hello yapısında arama teknolojisi karmaşıklığını maskeleyerek. Toplama tooAPIs içinde hello Azure portal yönetim ve prototip oluşturma desteği sağlar. Altyapı ve kullanılabilirlik Microsoft tarafından yönetilir.

<a name="feature-drilldown"></a>

## <a name="feature-summary"></a>Özellik Özeti

| Kategori | Özellikler |
|----------|----------|
|Tam metin araması ve metin analizi | [**Tam metin araması** ](search-lucene-query-architecture.md) çoğu arama tabanlı uygulamalar için birincil kullanım örneği değil. Desteklenen bir söz dizimi kullanılarak sorguları şeklide: <br/><br/>[**Basit Sorgu söz dizimi**](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search), mantıksal işleçler, tümcecik arama işleçleri, sonek işleçleri, öncelik işleçleri sunar.<br/><br/>[**Lucene sorgu söz dizimi** ](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) tüm Basit Sorgu desteğiyle birlikte benzer arama, yakınlık araması terim artırma ve normal ifadeleri sunar.| 
| Veri tümleştirmesi | JSON veri yapısı gönderilen sağlanan azure Search dizinlerini herhangi bir kaynaktan verileri kabul etmek. <br/><br/> İsteğe bağlı olarak, azure'da desteklenen veri kaynakları için kullanabileceğiniz [ **dizin oluşturucular** ](search-indexer-overview.md) tooautomatically gezinme [Azure SQL veritabanı](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md), [Azure Cosmos DB](search-howto-index-documentdb.md), veya [Azure Blob Depolama](search-howto-indexing-azure-blob-storage.md) toosync search dizininizi birincil veri deposuyla ilgili içerik. Azure Blob dizin oluşturucular gerçekleştirebilir *belge çözme* için [ana dosya biçimleri dizin](search-howto-indexing-azure-blob-storage.md), Microsoft Office, PDF ve HTML belgeleri de dahil olmak üzere. |
| Arama analizi | [**Özel sözcük çözümleyiciler** ](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) ses eşleşen kullanarak karmaşık arama sorguları ve normal ifadeler için kullanılabilir. |
| Dil desteği | [**Dil Çözümleyicileri** ](https://docs.microsoft.com/rest/api/searchservice/language-support) Lucene yanı sıra Microsoft kullanıcının doğal dil işlemciler 56 farklı dillerde toointelligently tanıtıcı dile özgü linguistics kullanılabilir dahil olmak üzere fiil zamanlarını, cinsiyetiniz, düzensiz çoğul adlar (örneğin, 'fareler' ve ' fare'), word XML'deki bileşik, sözcük bölme (için dilleri boşluk) ve daha fazla. |
| Coğrafi arama | Azure arama akıllıca, filtreleri, işler ve coğrafi konumları görüntüler. Kullanıcıların sağlayan tooexplore verilerine dayalı bir arama sonucu tooa fiziksel konum hello yakınlık üzerinde. [Bu videoyu izleyin](https://channel9.msdn.com/Shows/Data-Exposed/Azure-Search-and-Geospatial-Data) veya [Bu örnek gözden](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs) toolearn daha fazla. |
| Kullanıcı deneyimi özellikleri | [**Arama önerileri** ](https://docs.microsoft.com/rest/api/searchservice/suggesters) arama çubuğunda yazarken tamamlanan sorgular için etkinleştirilebilir. Kullanıcıların kısmi arama giriş girerken gerçek belgeleri dizininize önerilir. <br/><br/>[**Modellenmiş bir gezinmede** ](https://docs.microsoft.com/azure/search/search-faceted-navigation) tek sorgu parametresi etkinleştirilir. Azure arama kategorilerini liste arkasındaki hello kod olarak (örneğin, toofilter katalog öğeleri fiyat-range veya marka) bağımsız filtrelemesi için kullanabileceğiniz bir modellenmiş bir gezinmede yapısı döndürür. <br/><br/> [**Filtreler** ](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) modellenmiş bir gezinmede kullanılan tooincorporate uygulamanızın UI içine olabilir, sorgu formülasyonu geliştirmek ve filtre kullanıcı veya Geliştirici belirtilen ölçütlere bağlı. Filtreler Hello OData sözdizimini kullanarak oluşturun.<br/><br/> [**İsabet vurgulama** ](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) anahtar sözcüğü arama sonuçlarında eşleşen görsel bir form atting tooa uygular. Hangi alanların vurgulanan parçacıkları dönüş seçebilirsiniz.<br/><br/>[**Sıralama** ](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) hello dizin şemasını aracılığıyla birden çok alan için sunulan ve bir tek arama parametresiyle sorgu zamanında yükseğe.<br/><br/> [**Disk belleği** ](search-pagination-page-layout.md) ve arama sonuçlarınızı azaltma kolay ince ayar yapılmış hello denetimiyle arama sonuçlarınızı Azure Search sunar.  
| İlgi Düzeyi | [**Basit Puanlama** ](/rest/api/searchservice/add-scoring-profiles-to-a-search-index) Azure Search'ün anahtar avantajdır. Bir işlev hello değerlerinin kendilerini belgeler gibi Puanlama kullanılan toomodel ilgi profillerdir. Örneğin, yeni ürünleri isteyebilir veya ürünleri tooappear hello arama sonuçlarında daha yüksek indirimli. İzlenen ve ayrı olarak depolanan müşteri arama tercihlerinize göre dayalı kişiselleştirilmiş Puanlama için etiketler kullanarak Puanlama profilleri de oluşturabilirsiniz. |
| İzleme ve Raporlama | [**Arama trafiği analytics** ](search-traffic-analytics.md) hangi kullanıcıların hello arama kutusuna yazmaya toplanan ve çözümlenen toounlock Öngörüler şunlardır. <br/><br/>Sorguları ikinci, gecikme ve azaltma her ölçümleri yakalanan ve ek yapılandırma gerektirmeden portal sayfalarında bildirdi. Ayrıca İzleyici dizin kolayca ve gerektiğinde kapasite ayarlayabilmesi belge sayar. Daha fazla bilgi için bkz: [Hizmet Yönetimi](search-manage.md) |
| Prototip oluşturma ve denetleme araçları | Merhaba portalında hello kullanabilirsiniz [ **verilerini İçeri Aktar Sihirbazı** ](search-import-data-portal.md) tooconfigure dizin oluşturucular, dizin Tasarımcı toostand bir dizin oluşturan ve [ **arama Gezgini** ](search-explorer.md) tootest sorgular ve puanlama profilleri daraltın. Tüm dizin tooview şemasına da açabilirsiniz. |
| Altyapı | Merhaba **yüksek oranda kullanılabilir platform** son derece güvenilir arama servis deneyimi sağlar. Düzgün şekilde genişletilmiş zaman [Azure Search sunar % 99,9 SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).<br/><br/> **Tam olarak yönetilen ve ölçeklenebilir** bir uçtan uca çözümü olarak Azure arama kesinlikle hiçbir altyapı Yönetimi gerektirir. Hizmetiniz, daha fazla belge depolama, daha yüksek sorgu yüklerinin veya her ikisi de iki boyut toohandle ölçeklendirme tarafından uyarlanmış tooyour gereksinimleri olabilir.

## <a name="how-it-works"></a>Nasıl çalışır?
### <a name="step-1-provision-service"></a>1. adım: Sağlama hizmeti
Bir Azure Search hizmetini hello dönmesi [Azure portal](https://portal.azure.com/) veya hello aracılığıyla [Azure kaynak yönetimi API](/rest/api/searchmanagement/). Diğer aboneleriyle paylaşılan ya da hello ücretsiz hizmeti seçebilirsiniz veya [katmanı Ücretli](https://azure.microsoft.com/pricing/details/search/) yalnızca hizmetiniz tarafından kullanılan kaynakları dedicates. Ücretli katmanlarda iki boyut bir hizmetini ölçeklendirebilirsiniz: 

- Kapasite toohandle ağır sorgunuzu yükler çoğaltmaları toogrow ekleyin.   
- Daha fazla belge için bölümleri toogrow depolama ekleyin. 

Belge depolama ve sorgu işleme ayrı olarak işleme üretim gereksinimlerine göre resourcing ayarlama.

### <a name="step-2-create-index"></a>2. adım: dizin oluşturma
Aranabilir içeriği yükleyebilir önce ilk Azure Search dizini tanımlamanız gerekir. Verilerinizi tutan ve arama sorguları kabul edebileceği bir veritabanı tablosu gibi dizinidir. Merhaba dizin şeması toomap tooreflect hello yapısı tanımladığınız hello belgelerin toosearch, bir veritabanında benzer toofields istiyor.

Bir şema hello Azure oluşturulabilir portal ya da program aracılığıyla kullanarak hello [.NET SDK'sı](search-howto-dotnet-sdk.md) veya [REST API](/rest/api/searchservice/).

### <a name="step-3-index-data"></a>3. adım: Dizin verileri
Bir dizin tanımla sonra hazır tooupload içerik demektir. İtme veya çekme modeli kullanabilirsiniz.

Merhaba çekme modeli, dış veri kaynaklarından verileri alır. Üzerinden desteklenen *dizin oluşturucular* kolaylaştırmak ve bağlanma, okuma ve verileri seri hale getirme gibi veri alımı yönlerini otomatik hale getirme. [Dizin oluşturucular](/rest/api/searchservice/Indexer-operations) Azure Cosmos DB, Azure SQL Database, Azure Blob Storage ve SQL Server bir Azure VM ile barındırılan için kullanılabilir. Bir dizin oluşturucu için isteğe bağlı veya zamanlanan veri yenileme yapılandırabilirsiniz.

Merhaba gönderme modeli hello SDK veya REST API'leri, güncelleştirilmiş belgeleri tooan dizin göndermek için kullanılan sağlanır. Merhaba JSON biçimini kullanarak herhangi bir veri kümesinden alınan veri gönderebilir. Bkz: [ekleme, güncelleştirme veya silme belgeleri](/rest/api/searchservice/addupdate-or-delete-documents) veya [nasıl toouse hello .NET SDK'sı)](search-howto-dotnet-sdk.md) veri Yükleme Kılavuzu.

### <a name="step-4-search"></a>Adım 4: arama
Bir dizin doldurduktan sonra şunları yapabilirsiniz [arama sorguları göndermek](/rest/api/searchservice/Search-Documents) tooyour Hizmeti uç noktası basit HTTP kullanarak istekleri REST API veya hello .NET SDK'sı ile.

## <a name="how-it-compares"></a>Nasıl karşılaştırır

Müşteriler genellikle isteyin nasıl [tam metin araması Azure Search'te](search-lucene-query-architecture.md) karşılaştırır [tam metin araması](https://en.wikipedia.org/wiki/Full_text_search) kendi veritabanı üründeki. Azure Search dil özellikleri daha zengin ve daha esnek ve Lucene sorguları, Lucene ve Microsoft, ses veya diğer özel girişleri için özel çözümleyiciler dil Çözümleyicileri ve hello özelliği toomerge verilerden desteğiyle bizim yanıt olan birden çok kaynak hello arama dizini içinde. 

Başka bir ton arama çözümü hello tüm arama deneyimi adresleri noktasıdır. Örneğin, bağımsız filtrelemesi isabet vurgulama ve typeahead Sorgu önerileri için özel Puanlama sonuçlarını, modellenmiş bir gezinmede isteyebilirsiniz. 

İzlemek ve sorgu etkinliği anlamak için araçları ayrıca bir arama çözümü karar öğeli. Örneğin, Azure Search destekler [trafiği analytics arama](search-traffic-analytics.md) geçişli tıklatma hızı için ölçümleri, üst arar, tıklama ve benzeri olmadan arar. Burada arama, bir eklenti ürünlerinde olası toofind olduğunuz bu özellikleri.

Kaynak kullanımı başka bir konudur. Doğal dil arama pkı'ya yoğun görülür. Bazı müşterilerimizin işlem için yolu toopreserve makine kaynakları olarak arama işlemleri tooAzure arama Boşaltılan. Harici hale getirerek aramada ölçek toomatch sorgu toplu kolayca ayarlayabilirsiniz.

Ayrılmış arama ile toogo karar verdim sonra sonraki bir bulut hizmeti veya bir şirket içi sunucu arasında bir karardır. İstiyorsanız, bir bulut hizmeti hello doğru seçimdir bir [anahtar teslim çözümüyle en az ek yükü ve Bakım ve ayarlanabilir ölçek](#cloud-service-advantage).

Merhaba bulut kip içinde birkaç sağlayıcıları tam metin araması, coğrafi arama ve hello özelliği toohandle belirli bir düzeyde arama girişleri belirsizlik ile karşılaştırılabilir temel özellikleri sunar. Genellikle, sahip bir [özel özellik](#feature-drilldown), veya hello kolaylığı ve genel Basitlik API'leri, Araçlar ve hello en iyi sığacak şekilde belirler yönetimi.

Bulut sağlayıcıda Azure arama içerik depoları ve arama bilgileri alma ve içerik gezinti için öncelikle bağlı uygulamaları için Azure üzerinde veritabanları üzerinde tam metin arama iş yükleri için güçlü olur. Anahtar gücü şunları içerir:

+ Merhaba dizin katmanında Azure veri tümleştirme (gezginleri)
+ Merkezi Yönetim için Azure portalı
+ Azure ölçek, güvenilirlik ve dünya çapındaki kullanılabilirliği
+ Çözümleyiciler 56 dillerde düz tam metin araması için ile dil ve özel analizi
+ [Çekirdek özellikleri ortak toosearch odaklı uygulamalar](#feature-drilldown): Puanlama, olduğunu, öneriler, eş anlamlıları, coğrafi arama ve daha fazla.

> [!Note]
> toobe NET, Azure olmayan veri kaynakları tam olarak desteklenir, ancak dizin oluşturucular yerine daha kod Kullanımı Yoğun gönderme yöntemi kullanır. Bizim API'lerini kullanarak, tüm JSON belge koleksiyonu tooan Azure Search dizini iletebildiğiniz.

Müşterilerimizin arasında bu mümkün tooleverage hello yelpazedeki Azure arama özellikleri çevrimiçi katalogları, iş programlar ve belge bulma uygulamaları içerir.

## <a name="rest-api--net-sdk"></a>REST API | .net SDK'sı

Birçok görevi hello Portalı'nda gerçekleştirilebilir olsa da, Azure Search toointegrate arama işlevini var olan uygulamalara isteyen geliştiriciler için yöneliktir. programlama arabirimleri aşağıdaki hello kullanılabilir.

|Platform |Açıklama |
|-----|------------|
|[REST](/rest/api/searchservice/) | Tüm programlama platform ve dili, Xamarin, Java ve JavaScript gibi tarafından desteklenen HTTP komutları|
|[.NET SDK](search-howto-dotnet-sdk.md) | .NET Framework hedefleme diğer yönetilen kod dilleri hello ve verimli C# kodlama hello REST API için .NET sarmalayıcı sunar |

## <a name="free-trial"></a>Ücretsiz deneme
Azure aboneleri için [hello ücretsiz katmanı hizmetinde sağlamak](search-create-service-portal.md).

Bir abone değilseniz, yapabilecekleriniz [ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F). Ücretli Azure hizmetlerini denemek için krediler alırsınız. Kullanıldıktan sonra hello hesabı sürdürebilir ve kullanmak [Azure Hizmetleri serbest](https://azure.microsoft.com/free/). Açıkça ayarlarınızı değiştirip ücret toobe isteyin sürece kredi kartınızdan asla ücret kesilir.

Alternatif olarak, [MSDN abone Avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): MSDN aboneliğiniz size kredi verir Ücretli Azure hizmetlerinizi kullanabildiğiniz her ay. 

## <a name="how-tooget-started"></a>Tooget nasıl başlatılacağını

1. Bir hizmet hello oluşturma [ücretsiz katmanı](search-create-service-portal.md).

2. Bir veya daha fazla öğreticileri aşağıdaki hello adım. 

  + [Nasıl toouse hello .NET SDK'sı](search-howto-dotnet-sdk.md) hello ana yönetilen kodda adımları gösterir.  
  + [Merhaba REST API'si ile çalışmaya başlama](https://github.com/Azure-Samples/search-rest-api-getting-started) gösterir hello aynı hello REST API kullanarak adımları.  
  + [Merhaba portalında, ilk dizininizi oluşturma](search-get-started-portal.md) hello portal'ın yerleşik dizin oluşturma ve prototip özelliklerini gösterir.   

Arama motorları hello ortak bilgi alma mobil uygulamalarda, hello web ve kurumsal veri depolarına sürücülerdir. Azure Search'te bir arama deneyimi benzer toothose büyük ticari web sitelerinde oluşturmak için Araçlar verir.

Liam Cavanagh program Yöneticisi'nden bu 9 dakikalık videoda, bir arama motoru tümleştirme uygulamanızı nasıl yararlanabilir öğrenin. Kısa gösterileri Azure Search ve normal bir iş akışı benzer anahtar özellikleri kapsar. 

>[!VIDEO https://channel9.msdn.com/Events/Connect/2016/138/player]
 
+ Kapak anahtar özellikleri ve kullanım örnekleri 0-3 dakika.
+ 3-4 dakika kapsayan hizmet sağlama. 
+ 4-6 dakika veri içeri aktarma Sihirbazı'nı kullanılan toocreate hello yerleşik Gayrimenkul dataset kullanarak dizini ele alınmaktadır.
+ 6-9 dakika arama Gezgini ve çeşitli sorguları ele alınmaktadır.


