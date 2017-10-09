---
title: "aaaCommon Azure Cosmos DB örnekleri ve senaryoları kullanın | Microsoft Docs"
description: "Beş kullanım için Azure Cosmos DB Hello üst hakkında bilgi edinin: kullanıcı oluşturulan içeriği, olay günlüğü, katalog verilerini, kullanıcı tercihlerini veri ve nesnelerin interneti (IOT)."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: eca68a58-1a8c-4851-8cf8-6e4d2b889905
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: mimig
ms.openlocfilehash: 115a418e7b18d5033c4d7e64591bf302aea0190b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="common-azure-cosmos-db-use-cases"></a>Ortak Azure Cosmos DB kullanım durumları
Bu makalede Azure Cosmos DB için birkaç ortak kullanım durumları genel bir bakış sağlar.  Cosmos DB ile Uygulamanızı geliştirirken hello önerileri bu makalede bir başlangıç noktası olarak hizmet.   

Bu makaleyi okuduktan sonra aşağıdaki soruları mümkün tooanswer hello olması: 

* Merhaba ortak kullanım durumları için Azure Cosmos DB nelerdir?
* Merhaba perakende uygulamaları için Azure Cosmos DB kullanmanın avantajları nelerdir?
* Nesnelerin interneti (IOT) sistemleri için bir veri deposu olarak Azure Cosmos DB kullanarak hello yararları nelerdir?
* Merhaba web ve mobil uygulamaları için Azure Cosmos DB kullanmanın avantajları nelerdir?

## <a name="introduction"></a>Giriş
[Azure Cosmos DB](../cosmos-db/introduction.md) Microsoft'un Genel dağıtılmış veritabanı hizmetidir. Merhaba tasarlanmış tooallow müşteriler tooelastically hizmetidir (ve bağımsız olarak) coğrafi bölgeler arasında herhangi bir sayı işleme ve depolama ölçeklendirin. Azure Cosmos DB hizmettir hello ilk Genel dağıtılmış veritabanı hello Pazar bugün toooffer içinde kapsamlı [hizmet düzeyi sözleşmelerine](https://azure.microsoft.com/support/legal/sla/cosmos-db/) verimlilik, gecikme, kullanılabilirlik ve tutarlılık. 

Hello Azure Cosmos DB proje içinde 2011 Geliştirici-Microsoft içindeki büyük Internet ölçekli uygulamalar tarafından karşılaştığı kalınan "Proje Floransa" tooaddress başlatıldı. Bu sorunları benzersiz tooMicrosoft's uygulamaları olmayan, hello biçiminde 2015'te toomake Azure Cosmos DB genel olarak kullanılabilir tooexternal geliştiriciler karar Gözlemleme [Azure DocumentDB](https://azure.microsoft.com/blog/documentdb-moving-to-general-availability/). Merhaba hizmeti ubiquitously içinde Microsoft dahili olarak kullanılır ve harici olarak Azure geliştiriciler tarafından kullanılan hello hızlı büyüyen hizmetler biridir. 

Azure Cosmos DB çok çeşitli uygulamalar ve kullanım örnekleri içinde kullanılan genel bir dağıtılmış, birden çok model veri tabanıdır. Herhangi bir için iyi bir seçimdir olan [sunucusuz](http://azure.com/serverless) düşük milisaniyelik sipariş yanıt sürelerini gerekir ve hızlı bir şekilde ve genel tooscale gereken uygulama. Birden çok veri modelleri destekler (anahtar-değer, belgeler, grafikler ve sütun) ve veriler için birçok API'lere erişim dahil olmak üzere [MongoDB](mongodb-introduction.md), [DocumentDB SQL](documentdb-introduction.md), [Gremlin](graph-introduction.md)ve [ Azure tabloları](table-introduction.md) yerel olarak ve Genişletilebilir bir biçimde. 

Merhaba aşağıdaki genel ambition ile yüksek performanslı uygulamalar için oldukça uygun hale bazı Azure Cosmos DB öznitelikleridir.

* Azure Cosmos DB yerel olarak yüksek kullanılabilirlik ve ölçeklenebilirlik için verilerinizi bölümler. Azure Cosmos DB % 99,99 kullanılabilirlik, performans, düşük gecikme süresi ve tutarlılığı garanti sunar.
* Azure Cosmos DB yedeklenen SSD depolama ile düşük gecikme süreli milisaniyelik sipariş yanıt sürelerini sahiptir.
* Tam esneklik ve düşük maliyet performans oranı için tutarlılık düzeylerini nihai, tutarlı öneki, oturum ve sınırlanmış eskime durumu gibi Azure Cosmos veritabanı desteği sağlar. Veritabanı Hizmet düzeyleri tutarlılık Azure Cosmos DB olarak kadar esnekliği sağlar. 
* Azure Cosmos DB bağımsız olarak depolama ve işleme ölçümler bir esnek veri kolay fiyatlandırma modeli vardır.
* Azure Cosmos DB'ın ayrılmış işleme modeli okuma/yazma CPU/bellek/IOPS donanım temel hello yerine sayısı bakımından toothink sağlar.
* Azure Cosmos DB'ın tasarım sağlar toomassive istek birimleri ölçeklendirme günde istek trilyon sipariş hello.

Bu öznitelikler faydalı web, mobil, oyun ve düşük yanıt sürelerini gerekir ve okuma ve yazma işlemleri oldukça büyük miktardaki toohandle gereken IOT uygulamaları.

## <a name="iot-and-telematics"></a>IoT ve telematikler
IOT kullanım örnekleri, yaygın olarak nasıl bunlar, işlem, alma, bazı desenleri paylaşabilir ve verileri depolamak.  İlk olarak, bu sistemler tooingest WINS'e aygıt algılayıcılar çeşitli yerel ayarların verilerini gerekir. Ardından, bu sistemler işlemek ve akış veri tooderive gerçek zamanlı Öngörüler analiz edin. Merhaba verilerdir sonra toplu analiz için toocold depolama arşivlenir. Microsoft Azure IOT için uygulanabilir zengin Hizmetleri Azure Cosmos DB, Azure Event Hubs, Azure akış analizi, Azure bildirim hub'ı, Azure Machine Learning, Azure Hdınsight ve Power BI dahil olmak üzere kullanım sunar. 

![Azure Cosmos DB IOT başvuru mimarisi](./media/use-cases/iot.png)

Düşük gecikme süresine sahip yüksek verimlilik veri alımı sunduğu gibi veri WINS'e Azure Event Hubs tarafından alınan. Gerçek zamanlı bilgiler için işlenen toobe gereken alınan veriler funneled tooAzure Stream Analytics gerçek zamanlı analiz için olabilir. Adhoc sorgulamak için Azure Cosmos Veritabanına veri yüklenebilir. Merhaba veriler Azure Cosmos Veritabanına yüklendikten sonra hello sorgulanan hazır toobe verilerdir. Ayrıca, yeni verileri ve değişiklikleri tooexisting verileri üzerinde değişiklik Akış okunabilir. Değişiklik akışı bir kalıcı, sıralı tooCosmos DB koleksiyonlarında depolar günlük değişiklikler yalnızca ekleyin. Merhaba tüm veriler veya yalnızca değişiklikleri toodata Azure Cosmos veritabanı olarak başvuru verileri gerçek zamanlı analiz bir parçası olarak kullanılabilir. Ayrıca, veriler daha fazla iyileştirilmiştir ve bağlanan Azure Cosmos DB veri tooHDInsight Pig, Hive veya harita/azaltın işleri için işlenir.  Gelişmiş veri geri tooAzure Cosmos DB yüklenir ve raporlama için.   

Hello Azure Cosmos DB, EventHubs ve Storm kullanan örnek bir IOT çözüm için bkz: [hdınsight storm örnekler deposu github'da](https://github.com/hdinsight/hdinsight-storm-examples/).

IOT için Azure teklifleri hakkında daha fazla bilgi için bkz: [oluşturma Merhaba, bilgisayarınızı interneti](http://www.microsoft.com/server-cloud/internet-of-things.aspx). 

## <a name="retail-and-marketing"></a>Perakende ve pazarlama
Azure Cosmos DB hello Windows mağazası ve XBox Live çalıştıran Microsoft'un kendi e-ticaret platformlarda, yaygın olarak kullanılır. Bu ayrıca hello perakende sektörün ve ardışık düzen işleme sırayla kaynak Hizmeti'nden olay Kataloğu verilerini depolamak için kullanılır.

Katalog verileri kullanım senaryoları depolamak ve kişiler, yerler ve ürünler gibi varlıklar için bir dizi sorgulama içerir. Bazı katalog verilerini kullanıcı hesapları, ürün katalogları, IOT cihaz kayıt defterleri ve fatura malzemeleri sistemlerinin gösterilebilir. Bu veriler için öznitelikler değişebilir ve süresi toofit uygulama gereksinimleri değiştirebilirsiniz.

Bir ürün kataloğu örneği öğesini bölümleri tedarikçi için göz önünde bulundurun. Her bölümü kendi öznitelikleri paylaşan tüm bölümleri toplama toohello ortak öznitelikleri olabilir. Ayrıca, belirli bir bölümü için öznitelikler için yeni bir model serbest bırakıldığında yıl aşağıdaki hello değiştirebilirsiniz. Esnek şemaları ve hiyerarşik verileri Azure Cosmos DB destekler ve bu nedenle, ürün kataloğu verilerini depolamak için uygundur.

![Azure Cosmos DB perakende katalog başvuru mimarisi](./media/use-cases/product-catalog.png)

Azure Cosmos DB toopower olay yönelimli mimarileri kullanarak kaynak Hizmeti'nden olayı için sık kullanılan kendi [akış değiştirmek](change-feed.md) işlevselliği. Hello değişiklik akış aşağı akış mikro özelliği tooreliably hello ve artımlı olarak okuma ekler ve güncelleştirmeleri (örneğin, sipariş olayları) tooan Azure Cosmos DB yapılan sağlar. Bu işlev kalıcı bir olay depolamak durumu değiştirme olayları ve birçok mikro arasında sürücü sipariş işleme iş akışı için bir ileti aracısı olarak çevrelerini tooprovide olabilir (hangi uygulanabilir olarak [sunucusuz Azure işlevleri](http://azure.com/serverless)).

![Ardışık Düzen referans mimarisi sıralama Azure Cosmos DB](./media/use-cases/event-sourcing.png)

Ayrıca, Apache Spark işleri aracılığıyla büyük veri analizi için Hdınsight ile Azure Cosmos DB içinde depolanan verileri tümleştirilebilir. Hello Azure Cosmos DB için Spark Bağlayıcısı hakkında daha fazla bilgi için bkz: [Cosmos DB ve Hdınsight Spark işini Çalıştır](spark-connector.md).

## <a name="gaming"></a>Oyun
Merhaba veritabanı katmanı oyun uygulamaları önemli bir bileşenidir. Modern oyunlar mobil/konsol istemcilerde grafik işleme gerçekleştirir, ancak özelleştirilmiş hello bulut toodeliver üzerinde kullanır ve kişiselleştirilmiş içerik oyun istatistikleri, sosyal medya tümleştirme ve yüksek puan liderlik gibi. Oyunlar genellikle okumalar tek milisaniyelik gecikme süreleri gerektiren ve etkileyici bir oyun deneyimi tooprovide yazar. Oyun veritabanı toobe hızlı gerekir ve yeni oyun başlatır ve özellik güncelleştirmeleri sırasında mümkün toohandle yoğun ani isteği oranlarının içinde olmalıdır.

Azure Cosmos DB gibi oyunlar tarafından kullanılan [taramasını ölü hello: Hayır ADAM'ın kara](https://azure.microsoft.com/blog/the-walking-dead-no-mans-land-game-soars-to-1-with-azure-documentdb/) tarafından [sonraki oyunlar](http://www.nextgames.com/), ve [hale 5: veli](https://azure.microsoft.com/blog/how-halo-5-guardians-implemented-social-gameplay-using-azure-documentdb/). Azure Cosmos DB toogame geliştiriciler hello aşağıdaki avantaj sağlar:

* Azure Cosmos DB verir ölçeklendirilmiş performans toobe yukarı veya aşağı özellikler esnek. Bu profili ve düzinelerce gelen istatistikleri güncelleştirme oyunlar toohandle sağlayan tek bir API çağrısı yaparak eş zamanlı oyun toomillions.
* Milisaniye okur ve toohelp Yazar azure Cosmos DB destekler herhangi gecikmelere oyun sırasında kaçının.
* Azure Cosmos DB'ın otomatik dizin oluşturma sağlar gerçek zamanlı birden çok farklı özelliklere göre filtre uygulamak için örneğin, kendi iç player kimlikleri tarafından oynatıcıları bulun veya kendi GameCenter, Facebook, Google kimlikleri veya sorgu tabanlı bir kılavuzu player üyeliği. Karmaşık dizin oluşturma veya parçalama altyapısı oluşturmadan bu mümkündür.
* Oyun Sohbet iletilerini, player Kılavuzu üyelikleri, tamamlandı zorluklar, yüksek puan liderlik ve sosyal grafikleri gibi sosyal esnek bir şema ile daha kolay tooimplement özellikleridir.
* Bir yönetilen platform olarak-hizmet (PaaS) olarak Azure Cosmos DB hızlı yineleme için gerekli minimum kurulum ve yönetim iş tooallow ve zaman toomarket azaltır.

![Azure Cosmos DB oyun başvuru mimarisi](./media/use-cases/gaming.png)

## <a name="web-and-mobile-applications"></a>Web uygulamaları ve mobil uygulamalar
Azure Cosmos DB web ve mobil uygulamaları içinde yaygın olarak kullanılır ve üçüncü taraf hizmetleri ile zengin kişiselleştirilmiş deneyimleri geliştirmek için tümleştirme sosyal etkileşimleri modelleme için uygundur. Merhaba Cosmos DB SDK'ları kullanılan yapı zengin iOS ve Android uygulamaları hello popüler kullanarak olabilir [Xamarin framework](mobile-apps-with-xamarin.md).  

### <a name="social-applications"></a>Sosyal uygulamaları
Bir ortak kullanım durumu için Azure Cosmos DB toostore ve sorgu oluşturulan kullanıcı (UGC) web, mobil ve sosyal medya uygulamalarının içeriktir. Bazı UGC sohbet oturumları, tweet'leri, blog gönderileri, derecelendirme ve yorum gösterilebilir. Genellikle, sosyal medya uygulamalarında hello UGC serbest biçimli metin, özellikler, etiketler ve katı yapısı tarafından sınırlanmış değil ilişkileri karışım olur. İçerik sohbetleri gibi açıklamalar ve gönderileri Cosmos DB'de gerektirmeden dönüşümleri veya karmaşık nesne toorelational eşleme Katmanlar depolanabilir.  Veri özellikleri eklenebilir veya geliştiricilerin böylece hızlı geliştirme yükseltme hello uygulama kodu yineleme olarak toomatch gereksinimlerini kolayca değiştirilemiyor.  

Üçüncü taraf sosyal ağlarla tümleştirme uygulamaları toochanging şemaları bu ağlardan yanıtlaması gerekir. Verileri otomatik olarak varsayılan olarak Cosmos DB sıralı olarak herhangi bir zamanda sorgulanan hazır toobe verilerdir. Bu nedenle, bu uygulamaların ilgili gereksinimlerine göre hello esneklik tooretrieve tahminleri vardır.

Birçok hello sosyal uygulamaları genel ölçeğinde çalıştırılacak ve tahmin edilemeyen kullanım biçimlerine sergiler. Merhaba veri deposu ölçeklendirme esneklik hello uygulama katmanı toomatch kullanımı isteğe bağlı olarak gereklidir.  Out ek veri bölümlerini Cosmos DB hesabı altında ekleyerek ölçeklendirebilirsiniz.  Ayrıca, birçok bölgeye ek Cosmos DB hesapları da oluşturabilirsiniz. Cosmos DB hizmet bölge kullanılabilirliği için bkz: [Azure bölgeleri](https://azure.microsoft.com/regions/#services).

![Azure Cosmos DB web uygulaması başvuru mimarisi](./media/use-cases/apps-with-global-reach.png)

### <a name="personalization"></a>Kişiselleştirme
Günümüzde, modern uygulamalar karmaşık görünümleri ve deneyimleri ile gelir. Bunlar toouser tercihlerine veya kapımıza yemek ve gereksinimlerini markalama genellikle dinamik. Bu nedenle, uygulamaların toobe mümkün tooretrieve kişiselleştirilmiş ayarları gerekiyor etkili bir şekilde toorender kullanıcı Arabirimi öğeleri ve deneyimleri hızla. 

Yalnızca basit değildir ancak JavaScript tarafından kolayca yorumlanabilen JSON, Cosmos DB tarafından desteklenen bir biçim etkili biçim toorepresent UI düzeni verileri aynıdır. Cosmos DB düşük gecikme süreli yazma işlemleri ile hızlı okuma izin ince ayarlanabilir tutarlılık düzeyleri sunar. Bu nedenle, kullanıcı Arabirimi Düzen veri Cosmos DB JSON belgelerde olduğu gibi bir etkili bir şekilde tooget kişiselleştirilmiş ayarları dahil olmak üzere bu verileri hello kablo depolama.

![Azure Cosmos DB web uygulaması başvuru mimarisi](./media/use-cases/personalization.png)

## <a name="next-steps"></a>Sonraki adımlar
Azure Cosmos DB ile başlatılan tooget izleyin bizim [hızlı başlangıçlar](create-documentdb-dotnet.md), hangi yol, bir hesap ve Cosmos DB ile çalışmaya başlama oluşturmada size. 

Veya tooread Cosmos DB kullanan müşteriler hakkında daha fazla bilgi isterseniz, hello aşağıdaki müşteri hikayeleri kullanılabilir:

* [Jet.com](https://jet.com). E-ticaret karşıt gözler hello üst nokta, hello Microsoft Bulutu üzerinde çalışan, genel bir ölçekte Cosmos DB yararlanır.
* [Asos.com](http://www.asos.com/). Asos.com bir İngiliz çevrimiçi moda ve güzelliği deposudur. Öncelikle Küçük yaştaki yetişkinler amaçlayan, Asos üzerinde 850 markalar ve bunun yanı sıra kendi dizi giysisinin ve Donatılar satıyor.
* [Toyota](https://www.toyota.com/). Toyota Motor Japonca öğesini üretici bir şirkettir. Toyota Cosmos DB genel IOT uygulama için kullanılabilir.
* [Citrix](https://customers.microsoft.com/story/citrix). Azure Service Fabric ve Azure Cosmos DB kullanarak çoklu oturum açma çözüm Citrix geliştirir
* [TEXA](https://customers.microsoft.com/story/texaspa) zamanı, para, gaz TEXA'ın devrim niteliğinde IOT çözüm araç sahipleri için yardımcı olur — ve büyük olasılıkla yaşar.
* [Domino'nın Pizza](https://www.dominos.com). Domino'nın Pizza Inc. Amerikan pizza Restoran zinciri ' dir.
* [Johnson denetimleri](http://www.johnsoncontrols.com). Johnson denetimler, genel büyük teknoloji ve çok çeşitli müşteriler 150'den fazla ülkede hizmet veren çok endüstri lideri ' dir.
* [Microsoft Windows, Evrensel deposu, Azure IOT Hub, Xbox Live ve diğer Internet ölçekli Hizmetler](https://azure.microsoft.com/blog/how-azure-documentdb-planet-scale-nosql-helps-run-microsoft-s-own-businesses/). Nasıl Microsoft Azure Cosmos DB kullanarak yüksek düzeyde ölçeklenebilir hizmetler oluşturur.
* [Microsoft Data ve analiz takım](https://customers.microsoft.com/story/microsoftdataandanalytics). Microsoft'un verileri ve çözümlemeler takım başarır Azure Cosmos DB ile planet ölçekli büyük veri toplama
* [Sulekha.com](https://customers.microsoft.com/story/sulekha-uses-azure-documentdb-to-connect-customers-and-businesses-across-india). Sulekha Azure Cosmos DB tooconnect müşteriler ve işletmeler arasında Hindistan kullanır.
* [NewOrbit](https://customers.microsoft.com/story/neworbit-takes-flight-with-azure-documentdb). NewOrbit Azure Cosmos DB ile uçuş alır.
* [Affinio](https://customers.microsoft.com/doclink/affinio-switches-from-aws-to-azure-documentdb-to-harness-social-data-at-scale). AWS tooAzure Cosmos DB tooharness sosyal veri ölçekte gelen Affinio geçer.
* [Sonraki oyunları](https://azure.microsoft.com//blog/the-walking-dead-no-mans-land-game-soars-to-1-with-azure-documentdb/). Merhaba Walking atılacak: Hayır adam Halk kara oyun yükselmesi çok #1 desteklenen Azure Cosmos DB tarafından.
* [Hale](https://azure.microsoft.com/blog/how-halo-5-guardians-implemented-social-gameplay-using-azure-documentdb/). Nasıl hale 5 Azure Cosmos DB kullanarak sosyal oyunlar uygulanmadı.
* [Cortana Analytics Galerisi](https://azure.microsoft.com/blog/cortana-analytics-gallery-a-scalable-community-site-built-on-azure-documentdb/). Cortana Analytics Galerisi - Azure Cosmos DB'de yerleşik ölçeklenebilir topluluk sitesi.
* [Kolay](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18602). Tümleştirici önde gelen esnek bulut teknolojileri ile dakika cinsinden çokuluslu firmalarından genel bilgiler sağlar.
* [Haber Cumhuriyeti](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18639). Toohello haber tooprovide Bilgileri'ni amacıyla katılımcı kullanıcılarının için ekleniyor. 
* [GG uluslararası](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18653). Merhaba dünya genelinde tutarlı renk için önemli markalar tooSGS açın. Ve GG tooAzure kapatır.
* [Telenor](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18608). Genel öncü Telenor hello bulut toomove bir başlangıç hello hızıyla kullanır. 
* [XOMNI](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18667). Hızlı arama ve hello kolay veri akışını gelecekteki çalışır hello Hello deposu.
* [Nucleo](https://customers.microsoft.com/story/azure-based-software-platform-breaks-down-barriers-bet). İşletmelerin ve müşteriler arasındaki engelleri aşağı Azure tabanlı yazılım platformu keser.
* [Weka](https://customers.microsoft.com/story/weka-smart-fridge-improves-vaccine-management-so-more-people-can-be-protected-against-diseases). Daha fazla kişinin diseases karşı korunmak için weka akıllı Fridge vaccine yönetim artırır.
* [Turuncu Tribes](https://customers.microsoft.com/story/theres-more-to-that-food-app-than-meets-the-eye-or-the-mouth). Hello göz veya hello ağzınıza karşılayıp olandan daha fazla toothat yemek uygulama yok.
* [Gerçek Madrid](https://customers.microsoft.com/story/real-madrid-brings-the-stadium-closer-to-450-million-f). Gerçek Madrid hello stadyum daha yakından too450 milyon fanlar hello Microsoft Cloud ile Merhaba Dünya çevresinde getirir.
* [Tuku](https://customers.microsoft.com/story/tuku-makes-car-buying-fun-with-help-from-azure-services). Azure hizmetlerinden Yardım keyif satın araba TUKU yapar
