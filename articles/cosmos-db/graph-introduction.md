---
title: "Giriş tooAzure Cosmos DB Graph API | Microsoft Docs"
description: "Apache TinkerPop hello hello Gremlin grafik sorgu dilini kullanarak düşük gecikme süresi ile nasıl Azure Cosmos DB toostore, sorgu ve çapraz yoğun grafikleri kullanabileceğinizi öğrenin."
services: cosmos-db
author: dennyglee
documentationcenter: 
ms.assetid: b916644c-4f28-4964-95fe-681faa6d6e08
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/21/2017
ms.author: denlee
ms.openlocfilehash: a4e79a4aa27976966baf0554928026177991ff69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-graph-api"></a>Giriş tooAzure Cosmos DB: grafik API'si

[Azure Cosmos DB](introduction.md) olan hello görev açısından kritik uygulamalar için Microsoft Genel dağıtılmış, birden çok model veritabanı hizmeti. Azure Cosmos DB sağlar [anahtar teslim genel dağıtım](distribute-data-globally.md), [üretilen iş ve depolama esnek ölçeklendirme](partition-data.md) dünya, tek basamaklı milisaniyelik gecikme hello 99, adresindeki [beş iyi tanımlanmış tutarlılık düzeylerini](consistency-levels.md), desteğiyle tüm yüksek oranda kullanılabilirlik garanti [endüstri lideri SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure Cosmos DB [verileri otomatik olarak dizinler](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) toodeal şema ve dizin yönetimi ile gerektirmeden. Çok modelli olan bu hizmet belge, anahtar-değer, grafik ve sütunlu veri modellerini destekler.

![Gremlin, grafik ve Azure Cosmos DB](./media/graph-introduction/graph-gremlin.png)

Hello Azure Cosmos DB grafik API'si sağlar:

- Grafik modelleme
- Çapraz geçiş API'leri
- Anahtar teslim genel dağıtım
- Esnek depolama ve işleme gecikmeleri okuma 10 MS'den kısa ve hello 99 en az 15 ms ölçeklendirme
- Otomatik anlık sorgu kullanılabilirlik ile dizin oluşturma
- İnce ayarlanabilir tutarlılık düzeyleri
- % 99,99 kullanılabilirlik dahil olmak üzere kapsamlı SLA

tooquery Azure Cosmos DB, kullanabileceğiniz hello [Apache TinkerPop](http://tinkerpop.apache.org) grafik geçişi dil [Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps), veya diğer TinkerPop uyumlu grafik sistemleri [Apache Spark GraphX](spark-connector-graph.md).

Bu makalede hello Azure Cosmos DB grafik API'sini genel bir bakış sağlar ve nasıl onu toostore yoğun grafikleri köşeleri ve kenarları milyarlarca ile kullanabileceğiniz açıklanmaktadır. Merhaba grafikleri milisaniyelik gecikme süresi ile sorgular ve hello grafik yapısı ve şema kolayca geliştirin.

## <a name="graph-database"></a>Grafik veritabanı
Merhaba gerçek dünyada göründüğü gibi veri doğal olarak bağlanır. Geleneksel veri modelleme varlıklarını odaklanır. Birçok uygulama için de bulunmaktadır gerek toomodel veya toomodel varlıkları ve ilişkileri doğal olarak artar.

A [grafik](http://mathworld.wolfram.com/Graph.html) oluşur yapısıdır [köşeleri](http://mathworld.wolfram.com/GraphVertex.html) ve [kenarları](http://mathworld.wolfram.com/GraphEdge.html). Köşeleri ve kenarları özelliklerinin rastgele bir sayı olabilir. Köşeleri bir kişi, yer veya olay gibi ayrı nesneleri gösterir. Kenarları köşeleri arasındaki ilişkileri gösterir. Örneğin, bir kişinin başka bir kişiye bildirin, bir olay söz konusu ve kısa süre önce bir konumda bırakıldı. Merhaba köşeleri ve kenarları hakkında bilgi express özellikleri. Örnek özellikleri adı, yaşı ve zaman damgası ve/veya bir ağırlık sahip kenar köşe içerir. Bu model olarak daha resmi olarak bilinen bir [özelliği grafik](http://tinkerpop.apache.org/docs/current/reference/#intro). Azure Cosmos DB hello özelliği grafik modelini destekler.

Örneğin, kişiler, mobil aygıtlar, ilgi alanları ve işletim sistemleri arasında grafik gösterir ilişkiler hello aşağıdaki örnek.

![Kişilerin, cihazların ve ilgi gösteren örnek veritabanı](./media/graph-introduction/sample-graph.png)

Grafikleri yararlı toounderstand çok çeşitli veri kümelerinde Bilimsel, teknoloji ve iş ' dir. Grafik veritabanları, bunları birçok senaryoları için kullanışlıdır grafikleri doğal ve verimli bir şekilde depolamak ve modeli sağlar. Bu kullanım gereksinimini şema esnekliği ve hızlı yineleme genellikle de örnekleri çünkü grafik veritabanları genellikle NoSQL veritabanlarıdır.

Grafikleri Romanım ve teknik modelleme güçlü verileri sunar. Ancak bu olgu tek başına yeterli neden toouse bir grafik veritabanı değil. Birçok kullanım örnekleri ve grafik çapraz geçişlerine içeren desenler için grafikleri geleneksel NoSQL ve SQL veritabanları büyüklük daha iyi performans gösterir. Bu performans farkı daha fazla arkadaş, arkadaş gibi birden fazla ilişkiye çapraz geçiş yapan zaman yükseltilmiş.

Derinlik ilk arama, avantajlarına ilk arama ve Dijkstra'nın algoritması, sosyal ağ, içerik yönetimi, Jeo-uzamsal gibi çeşitli etki alanlarına toosolve sorunları gibi grafik algoritmalarıyla grafik veritabanları sağlayan hello hızlı çapraz geçişlerine birleştirebilirsiniz, ve öneriler.

## <a name="planet-scale-graphs-with-azure-cosmos-db"></a>Azure Cosmos DB ile Planet ölçek grafikleri
Azure Cosmos DB genel dağıtım, depolama ve işleme, otomatik dizin oluşturma ve sorgu, ince ayarlanabilir tutarlılık düzeyleri ve hello TinkerPop standardı desteği ölçeklendirme esnek sunan tam olarak yönetilen grafik bir veritabanıdır.  

![Azure Cosmos DB graph mimarisi](./media/graph-introduction/cosmosdb-graph-architecture.png)

Azure Cosmos DB sunar hello aşağıdaki Ayrıştırılan karşılaştırıldığında yetenekleri tooother grafik hello Pazar veritabanlarında:

* Esnek bir şekilde ölçeklenebilir işleme ve depolama

 Merhaba gerçek dünya grafiklerde hello tek bir sunucu kapasitesini ötesinde tooscale gerekir. Azure Cosmos DB ile grafikleri sorunsuz bir şekilde birden çok sunucu arasında ölçeklendirebilirsiniz. Ayrıca, bağımsız olarak, erişim düzenlerini esas alarak, grafik hello verimini ölçeklendirebilirsiniz. Azure Cosmos DB destekleyen toovirtually ölçeklendirebilirsiniz grafik veritabanları sınırsız depolama boyutlarına ve sağlanan işleme.

* Bölgeli çoğaltma

 Azure Cosmos DB saydam hesabınızla ilişkilendirdiğiniz, grafik veri tooall bölgeleri çoğaltır. Çoğaltma genel erişim toodata gerektiren toodevelop uygulamalar sağlar. Tutarlılık, kullanılabilirlik ve performans ve karşılık gelen garanti hello alanlarında bileşim vardır. Azure Cosmos DB çok girişli API'leri ile saydam bölgesel yük devretme sağlar. Merhaba Dünya çapında işleme ve depolama özellikler esnek ölçeklendirebilirsiniz.

* Hızlı sorguları ve çapraz geçişlerine tanıdık Gremlin sözdizimi ile

 Heterojen köşeleri ve kenarları depolayın ve tanıdık bir Gremlin söz dizimi aracılığıyla bu belgeleri sorgulayın. Azure Cosmos DB bir derecede eşzamanlı, kilidi serbest, günlük yapılı dizin oluşturma teknolojisi tooautomatically dizin tüm içerik kullanır. Gerçek zamanlı zengin sorgulara bu yeteneği sağlar ve çapraz geçişlerine hello olmadan toospecify şema ipuçları, ikincil dizinler veya görünümler gerekir. Daha fazla bilgi edinin [sorgu Gremlin kullanarak grafikleri](gremlin-support.md).

* Tam olarak yönetilen

 Azure Cosmos DB Merhaba, gerek toomanage veritabanı ve makine kaynaklarını ortadan kaldırır. Tam olarak yönetilen bir Microsoft Azure hizmet olarak değil gerek toomanage sanal makineleri yapın, dağıtmak ve yazılım yapılandırma ölçeklendirmeyi yönetmeniz veya karmaşık veri katmanı yükseltmeleriyle uğraşmanız. Her grafik otomatik olarak yedeklenmesini ve bölgesel arızalara karşı korunur. Kolayca Azure Cosmos DB hesap eklemek ve işletim ve veritabanınızı yönetmek yerine, uygulamanızın üzerinde odaklanabiliriz gerek duyduğunuz kapasite sağlayın.

* Otomatik dizin oluşturma

 Varsayılan olarak, Azure Cosmos DB otomatik olarak tüm hello özellikleri düğümler ve hello grafik kenarları içinde dizinler ve beklediğiniz veya herhangi bir şemayı ya da ikincil dizinlerin oluşturulmasını gerektirir.

* Apache TinkerPop ile uyumluluk

 Azure Cosmos DB yerel olarak hello açık kaynak Apache TinkerPop standart destekler ve diğer TinkerPop etkin grafik sistemleriyle tümleştirilebilir. Bu nedenle, kolayca Titan veya Neo4j, gibi başka bir grafik veritabanından geçirmek veya gibi grafik analytics çerçeveleri ile Azure Cosmos DB kullanılsın [Apache Spark GraphX](spark-connector-graph.md).

* İnce ayarlanabilir tutarlılık düzeyleri

 Beş iyi tanımlanmış tutarlılık düzeyleri tooachieve en iyi dengeyi tutarlılık ve performans arasında seçin. Azure Cosmos DB sorgular ve okuma işlemleri için beş farklı tutarlılık düzeyi sunar: güçlü, sınırlanmış eskime durumu, oturum, tutarlı ön ek ve son. Bu ayrıntılı ve iyi tanımlanmış tutarlılık düzeyleri tutarlılık, kullanılabilirlik ve gecikme süresi arasında toomake ses dengelerin izin verin. Daha fazla bilgi edinin [toomaximize kullanılabilirlik ve documentdb'de performans düzeyleri tutarlılık kullanarak](consistency-levels.md).

Azure Cosmos DB de kullanabilir, belge ve grafik, gibi birden çok modelleri içinde hello aynı kapsayıcıları/veritabanları. Bir belge koleksiyonu toostore grafik verileri Belgeleri yan yana kullanabilirsiniz. Gremlin sorguları tooquery hello aynı verileri bir grafik olarak ve JSON hem SQL sorgularını kullanabilirsiniz.

## <a name="getting-started"></a>Başlarken
Hello Azure komut satırı arabirimi (CLI), Azure Powershell veya Azure portalıyla graph API toocreate Azure Cosmos DB hesapları için destek hello kullanabilirsiniz. Hesapları oluşturduktan sonra hello Azure portalında bir hizmet uç noktası gibi sağlar `https://<youraccount>.graphs.azure.com`, WebSocket ön uç için Gremlin sağlar. Hello gibi TinkerPop uyumlu araçlarınızı yapılandırabilirsiniz [Gremin konsol](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console), Java, Node.js veya herhangi bir Gremlin istemci sürücüsü tooconnect toothis uç noktası ve yapı uygulamalar.

Merhaba aşağıdaki tabloda popüler Gremlin sürücüleri Azure Cosmos DB karşı kullanabileceğiniz gösterilmektedir:

| İndir | Belgeler |
| --- | --- |
| [Java](https://mvnrepository.com/artifact/com.tinkerpop.gremlin/gremlin-java) |[Gremlin JavaDoc](http://tinkerpop.apache.org/javadocs/current/full/) |
| [Node.js](https://www.npmjs.com/package/gremlin) |[Github'da gremlin JavaScript](https://github.com/jbmusso/gremlin-javascript) |
| [Gremlin konsol](https://tinkerpop.apache.org/downloads.html) |[TinkerPop belgeleri](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console) |

Azure Cosmos DB ayrıca Gremlin genişletme yöntemleri hello üstünde olan bir .NET kitaplığı sağlar [Azure Cosmos DB SDK'ları](documentdb-sdk-dotnet.md) NuGet aracılığıyla. Bu kitaplığı, "bir işlem" Gremlin sunucusu sağlar tooconnect kullanabileceğiniz doğrudan tooDocumentDB veri bölümler.

| İndir | Belgeler |
| --- | --- |
| [.NET](https://www.nuget.org/packages/Microsoft.Azure.Graphs/) |[Microsoft.Azure.Graphs](https://msdn.microsoft.com/library/azure/dn948556.aspx) |

Hello kullanarak [Azure Cosmos DB öykünücüsü](local-emulator.md), hello grafik API'si toodevelop ve test yerel olarak bir Azure aboneliği oluşturmak veya herhangi bir maliyet olmadan kullanabilirsiniz. Uygulamanızı hello öykünücüsü nasıl çalıştığını ile memnun kaldığınızda, toousing hello buluttaki bir Azure Cosmos DB hesabını geçiş yapabilirsiniz.

## <a name="scenarios-for-graph-support-of-azure-cosmos-db"></a>Azure Cosmos DB grafik desteği için senaryolar
Azure Cosmos DB grafik desteği kullanıldığı bazı senaryolar verilmiştir:

* Sosyal ağlar

 Müşterileriniz ve diğer kişilerle kendi etkileşimler hakkındaki verileri birleştirerek, kişiselleştirilmiş deneyimleri geliştirmek, müşteri davranışı tahmin etmek veya kişiler başkalarıyla benzer ilgi alanları ile bağlanabilirsiniz. Azure Cosmos DB sosyal ağlar kullanılan toomanage olması ve müşteri tercihlerini ve veri izleyebilirsiniz.

* Öneri altyapısı

 Bu senaryo, hello perakende sektörün yaygın olarak kullanılır. Ürünleri, kullanıcıları ve satın alma, gözatma veya bir öğe derecelendirme gibi kullanıcı etkileşimleri hakkında bilgi birleştirerek özelleştirilmiş öneriler oluşturabilirsiniz. Düşük gecikme süresi ve esnek ölçek yerel hello Azure Cosmos DB grafik desteği bu etkileşimleri modelleme için idealdir.

* Jeo-uzamsal

 Birçok uygulama telekomünikasyon, lojistik ve seyahat planlama iki konum arasında hello kısa ve en uygun rotayı bulmak veya toofind ilgilendiğiniz bir alanda bir konum gerekir. Azure Cosmos DB bu sorunları için doğal bir Sığdırma ' dir.

* Nesnelerin İnterneti

 Hello ağ ve bir grafik Modellenen IOT cihazları arasındaki bağlantıları ile aygıtları ve varlıkları hello durumu daha iyi anlamasına oluşturun ve nasıl hello ağın bir parçası olarak değişikliklerin başka bir bölümü olası etkileyebileceğini öğrenin.

## <a name="next-steps"></a>Sonraki adımlar
Azure Cosmos DB grafik desteği hakkında daha fazla toolearn bakın:

* Merhaba ile çalışmaya başlama [Azure Cosmos DB grafik Öğreticisi](create-graph-dotnet.md).
* Hakkında bilgi edinin çok[sorgu Azure Cosmos Gremlin kullanarak DB grafiklerde](gremlin-support.md).
