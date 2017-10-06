---
title: aaaConnecting Apache Spark tooAzure Cosmos DB | Microsoft Docs
description: "Bu öğretici toolearn tooconnect Apache Spark tooAzure Cosmos DB dağıtılmış tooperform toplamalar ve veri sciences Microsoft'tan hello çok kiracılı Genel dağıtılmış veritabanı sistemde sağlayan hello Azure Cosmos DB Spark Bağlayıcısı hakkında kullanın hello bulut için tasarlanmıştır."
keywords: Apache spark
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: c4f46007-2606-4273-ab16-29d0e15c0736
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: denlee
ms.openlocfilehash: 70b496fc5ca8f65675f0224e749637f5d533c346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="accelerate-real-time-big-data-analytics-with-hello-spark-tooazure-cosmos-db-connector"></a>Merhaba Spark tooAzure Cosmos DB Bağlayıcısı ile gerçek zamanlı büyük veri analizi hızlandırmak

Merhaba Spark tooAzure Cosmos DB bağlayıcı Azure Cosmos DB tooact bir giriş kaynağı ya da Apache Spark işleri için çıkış havuzu olarak sağlar. Bağlanma [Spark](http://spark.apache.org/) çok[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) burada kullanabileceğiniz Azure Cosmos DB tooquickly sorunları sürdüremiyor ve veri sorgulama, özelliği toosolve hızlı taşıma veri bilimi hızlandırır. Merhaba Spark tooAzure Cosmos DB bağlayıcı verimli bir şekilde hello yerel Azure Cosmos yönetilen DB dizinleri kullanır. Merhaba dizinler güncelleştirilebilir sütunları analiz gerçekleştirmek ve nesnelerin interneti (IOT) toodata Bilim ve analizi senaryolarından aralığı verileri hızlı genel değiştirme karşı filtreleme itme aşağı koşulu dağıtılmış sağlar.

Spark GraphX ve hello Gremlin grafik Azure Cosmos DB API'leri ile çalışmak için bkz: [Spark ve Apache TinkerPop Gremlin kullanarak grafik analytics gerçekleştirmek](spark-connector-graph.md).

## <a name="download"></a>İndir

tooget başlatıldı, hello hello Spark tooAzure Cosmos DB Bağlayıcısı (Önizleme) yükleme [azure cosmosdb spark](https://github.com/Azure/azure-cosmosdb-spark/) github'daki.

## <a name="connector-components"></a>Bağlayıcı bileşenleri

Merhaba bağlayıcı bileşenlerini aşağıdaki hello kullanır:

* [Azure Cosmos DB](http://documentdb.com) özellikler esnek coğrafi bölgeler arasında herhangi bir sayı işleme ve depolama ölçek ve müşteriler tooprovision sağlar. Merhaba hizmeti sunar:
   * Anahtar kapatma [genel dağıtım](distribute-data-globally.md) ve yatay ölçek
   * Tek basamaklı gecikmeleri hello 99 adresindeki garanti
   * [Birden çok iyi tanımlanmış tutarlılık modelleri](consistency-levels.md)
   * Çok girişli özellikleriyle yüksek oranda kullanılabilirlik garanti
   * Tüm özellikleri endüstri lideri tarafından kapsamlı yedeklenen [hizmet düzeyi sözleşmelerine](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLA).

* [Apache Spark](http://spark.apache.org/) hızı, kullanımı kolay, gelişmiş analizler yerleşik bir güçlü açık kaynaklı işleme altyapısıdır.

* [Azure hdınsight'ta Apache Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) , Apache Spark kritik dağıtımlar için hello bulutta kullanarak dağıtabileceğiniz [Azure Hdınsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).

Resmi olarak desteklenen sürümler:

| Bileşen | Sürüm |
|---------|-------|
|Apache Spark|2.0+|
| Scala| 2.11|
| Azure DocumentDB Java SDK'sı | 1.10.0 |

Bu makalede, Python (pyDocumentDB) kullanarak bazı basit örneklerini çalıştırma ve Scala arabirimleri hello yardımcı olur.

İki yaklaşım tooconnect Apache Spark ve Azure Cosmos DB vardır:
- Merhaba aracılığıyla pyDocumentDB kullanmak [Azure DocumentDB Python SDK'sı](https://github.com/Azure/azure-documentdb-python).
- Bir Java tabanlı Spark tooAzure Cosmos DB hello yararlanarak oluşturmanıza [Azure DocumentDB Java SDK'sı](https://github.com/Azure/azure-documentdb-java).

## <a name="pydocumentdb-implementation"></a>pyDocumentDB uygulama
Merhaba geçerli [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) hello Aşağıdaki diyagramda gösterildiği gibi tooconnect Spark tooAzure Cosmos DB sağlar:

![Spark tooAzure pyDocumentDB DB aracılığıyla Cosmos DB veri akışı](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-hello-pydocumentdb-implementation"></a>Veri akışı hello pyDocumentDB uygulama

Merhaba veri akışı aşağıdaki gibidir:

1. Merhaba Spark ana düğüm toohello Azure Cosmos DB ağ geçidi düğümü pyDocumentDB üzerinden bağlanır. Bir kullanıcı yalnızca hello Spark ve Azure Cosmos DB bağlantıları belirtir. Bağlantıları toohello ilgili ana ve ağ geçidi düğümleri saydam toohello kullanıcısıysanız.
2. Merhaba ağ geçidi düğümü Azure Cosmos hello sorgu daha sonra hello veri düğümlerini hello koleksiyonunun bölümlerinde karşı çalıştığı DB hello sorgusu yapar. Bu sorguları için Hello yanıt toohello ağ geçidi düğümü ve bu sonuç kümesi toohello Spark ana düğüm döndürülür geri gönderilir.
3. Sonraki sorguları (örneğin, bir Spark DataFrame) toohello Spark çalışan düğümleri işleme gönderilir.

Spark Azure Cosmos DB arasındaki iletişimi sınırlı toohello Spark ana düğüm ve Azure Cosmos DB ağ geçidi düğümleri ' dir.  Merhaba sorguları hello Aktarım katmanı bu iki düğüm arasında verir kadar hızlı gidin.

### <a name="install-pydocumentdb"></a>PyDocumentDB yükleyin
Kullanarak, sürücü düğümde pyDocumentDB yükleyebilirsiniz **PIP**, örneğin:

```
pip install pyDocumentDB
```


### <a name="connect-spark-tooazure-cosmos-db-via-pydocumentdb"></a>Spark tooAzure Cosmos DB pyDocumentDB aracılığıyla bağlanma
Merhaba Basitlik hello iletişim taşıma pyDocumentDB görece basit kullanarak Spark tooAzure Cosmos DB sorgudan yürütülmesini sağlar.

kod parçacığı gösterir nasıl aşağıdaki hello Spark bağlamda toouse pyDocumentDB.

```
# Import Necessary Libraries
import pydocumentdb
from pydocumentdb import document_client
from pydocumentdb import documents
import datetime

# Configuring hello connection policy (allowing for endpoint discovery)
connectionPolicy = documents.ConnectionPolicy()
connectionPolicy.EnableEndpointDiscovery
connectionPolicy.PreferredLocations = ["Central US", "East US 2", "Southeast Asia", "Western Europe","Canada Central"]


# Set keys tooconnect tooAzure Cosmos DB
masterKey = 'le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA=='
host = 'https://doctorwho.documents.azure.com:443/'
client = document_client.DocumentClient(host, {'masterKey': masterKey}, connectionPolicy)
```

Merhaba kod parçacığında belirtildiği gibi:

* Hello Azure Cosmos DB Python SDK'sını (`pyDocumentDB`) hello içeren tüm gerekli bağlantı parametrelerini hello. Örneğin, hello hello çoğaltma ve öncelik sırasını okuma konumları parametre seçer tercih edilir.
*  Merhaba gerekli kitaplıkları içeri aktarma ve yapılandırma, **masterKey** ve **konak** toocreate hello Azure Cosmos DB *istemci* (**pydocumentdb.document_ İstemci**).


### <a name="execute-spark-queries-via-pydocumentdb"></a>PyDocumentDB Spark sorgularını Yürüt
Merhaba önceki parçacığında hello kullanılarak oluşturulmuş örnekleri kullan hello Azure Cosmos DB örneği aşağıdaki hello salt okunur anahtarları belirtildi. Merhaba aşağıdaki kod parçacığını bağlayan toohello **airports.codes** hello DoctorWho hesabı olarak koleksiyonunda daha önce belirtilen ve bir sorgu tooextract hello havaalanı Şehir Washington durumunda çalışır.

```
# Configure Database and Collections
databaseId = 'airports'
collectionId = 'codes'

# Configurations hello Azure Cosmos DB client will use tooconnect toohello database and collection
dbLink = 'dbs/' + databaseId
collLink = dbLink + '/colls/' + collectionId

# Set query parameter
querystr = "SELECT c.City FROM c WHERE c.State='WA'"

# Query documents
query = client.QueryDocuments(collLink, querystr, options=None, partition_key=None)

# Query for partitioned collections
# query = client.QueryDocuments(collLink, query, options= { 'enableCrossPartitionQuery': True }, partition_key=None)

# Push into list `elements`
elements = list(query)
```

Aracılığıyla Hello sorgu yürütüldükten sonra **sorgu**, hello sonucu olan bir **query_iterable. QueryIterable** diğer bir deyişle dönüştürülmüş tooa Python listesi. Python listesini koddan hello kullanarak kolayca dönüştürülmüş tooa Spark DataFrame olabilir:

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-hello-pydocumentdb-tooconnect-spark-tooazure-cosmos-db"></a>Merhaba pyDocumentDB tooconnect Spark tooAzure Cosmos DB neden kullanılır?
Cosmos pyDocumentDB kullanarak DB. genellikle senaryoları için Spark tooAzure bağlanma burada:

* Toouse Python istiyor.
* Görece küçük bir sonuç Azure Cosmos DB tooSpark kümesi iade ettiğiniz. Temel alınan veri kümesi Azure Cosmos veritabanı hello Not oldukça büyük olabilir. Koşul filtreleri Azure Cosmos DB kaynağınız karşı çalışan filtreleri, diğer bir deyişle, uyguladığınızı.  

## <a name="spark-tooazure-cosmos-db-connector"></a>Spark tooAzure Cosmos DB Bağlayıcısı

Merhaba Spark tooAzure Cosmos DB bağlayıcı yararlanan hello [Azure DocumentDB Java SDK'sı](https://github.com/Azure/azure-documentdb-java) ve verileri hello Aşağıdaki diyagramda gösterildiği gibi Azure Cosmos DB hello Spark çalışan düğümleri arasında taşır:

![Veri akışı hello Spark tooAzure Cosmos DB Bağlayıcısı](./media/spark-connector/spark-connector.png)

Merhaba veri akışı aşağıdaki gibidir:

1. Merhaba Spark ana düğüm toohello Azure Cosmos DB ağ geçidi düğümü tooobtain hello bölüm Haritası bağlanır. Bir kullanıcı yalnızca hello Spark ve Azure Cosmos DB bağlantıları belirtir. Bağlantıları toohello ilgili ana ve ağ geçidi düğümleri saydam toohello kullanıcısıysanız.
2. Bu bilgiler geri toohello Spark ana düğüm sağlanır.  Bu noktada, mümkün tooparse hello query toodetermine hello bölümleri ve konumlarını Azure Cosmos tooaccess gereken veritabanı olmalıdır.
3. Bu bilgiler iletilen toohello Spark çalışan düğümü olur.
4. tooextract veri hello ve hello veri toohello Spark bölümleri hello Spark alt düğümler dönüş doğrudan hello Spark çalışan düğümleri toohello Azure Cosmos DB bölümleri bağlanır.

Merhaba veri taşıma hello Spark çalışan düğümleri ve hello Azure Cosmos DB veri düğümleri (bölümler) olduğundan Spark Azure Cosmos DB arasındaki iletişimi önemli ölçüde daha hızlıdır.

### <a name="build-hello-spark-tooazure-cosmos-db-connector"></a>Merhaba Spark tooAzure Cosmos DB bağlayıcısı oluşturun
Şu anda hello bağlayıcı proje maven kullanır. toobuild hello bağlayıcı bağımlılıklar olmadan çalıştırabilirsiniz:
```
mvn clean package
```
Merhaba JAR en son sürümlerini hello hello indirebilirsiniz *serbest* klasör.

### <a name="include-hello-azure-cosmos-db-spark-jar"></a>Hello Azure Cosmos DB Spark JAR Ekle
Herhangi bir kod çalıştırmadan önce tooinclude hello Azure Cosmos DB Spark JAR gerekir.  Merhaba kullanıyorsanız **spark Kabuk**, hello kullanarak hello JAR içerebilir sonra **--Kavanoz** seçeneği.  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

Bağımlılıklar olmadan tooexecute hello JAR koddan hello kullanın:

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

Azure Hdınsight Jupyter Not Defteri hizmeti gibi bir Not Defteri hizmeti kullanıyorsanız, hello kullanabilirsiniz **spark Sihirli** komutlar:

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

Merhaba **Kavanoz** etkinleştirir, tooinclude iki hello Jar'lar komutu için gereken **azure cosmosdb spark** (kendisi ve da hello Azure DocumentDB Java SDK'sı) ve çıkarma **scala-yansıtmak** Livy çağırır hello ile etkilemediğinden emin (Jupyter not defteri > Livy > Spark).

### <a name="connect-spark-tooazure-cosmos-db-using-hello-connector"></a>Spark bağlanmak tooAzure Cosmos DB kullanarak hello Bağlayıcısı
Merhaba iletişimi aktarım biraz daha karmaşık olsa da, Spark tooAzure bir sorgu yürütülürken Cosmos hello bağlayıcısını kullanarak DB önemli ölçüde daha hızlıdır.

Aşağıdaki kod parçacığını hello nasıl toouse hello Spark bağlamda bağlayıcı gösterir.

```
// Import Necessary Libraries
import org.joda.time._
import org.joda.time.format._
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Configure connection tooyour collection
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

Merhaba kod parçacığında belirtildiği gibi:

- **Azure cosmosdb spark** hello içeren tüm tercih edilen hello konumlarını dahil gerekli bağlantı parametrelerini hello. Örneğin, çoğaltma ve öncelik sırasını hello okuma seçebilirsiniz.
- Yalnızca hello gerekli kitaplıkları içeri aktarma ve masterKey ve ana bilgisayar toocreate hello Azure Cosmos DB istemcinizi yapılandırmak.

### <a name="execute-spark-queries-via-hello-connector"></a>Merhaba bağlayıcısı aracılığıyla Spark sorgularını Yürüt

Merhaba önceki parçacığında hello kullanılarak oluşturulmuş örnek kullanır hello Azure Cosmos DB örneği aşağıdaki hello salt okunur anahtarları belirtildi. Merhaba aşağıdaki kod parçacığını toohello DepartureDelays.flights_pcoll koleksiyonunda (Merhaba DoctorWho hesabını daha önce belirtildiği gibi) bağlanır ve bir sorgu tooextract hello uçuş gecikme bilgilerinin İstanbul departing uçuşlar çalıştırır.

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-hello-spark-tooazure-cosmos-db-connector-implementation"></a>Merhaba Spark tooAzure Cosmos DB bağlayıcı uygulama neden kullanılır?

Cosmos hello bağlayıcısını kullanarak DB. genellikle senaryoları için Spark tooAzure bağlanma burada:

* Toouse Scala istediğiniz ve tooinclude de belirtildiği gibi bir Python sarmalayıcı güncelleştirme [sorunu 3: ekleme Python sarmalayıcı ve örnekler](https://github.com/Azure/azure-cosmosdb-spark/issues/3).
* Çok miktarda veri tootransfer Apache Spark Azure Cosmos DB arasındaki sahip.

toogive hello sorgu performans farkı hakkında bir fikir gördüğünüz hello [sorgu Test çalışmalarını wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).

## <a name="distributed-aggregation-example"></a>Dağıtılmış toplama örneği
Bu bölümde bazı örnekleri nasıl dağıtılmış toplamalar ve analizi birlikte Apache Spark ve Azure Cosmos DB kullanarak bunu yapabilirsiniz. Destekleyen zaten toplamalar, Azure Cosmos DB hello ele alınmıştır [Planet ölçek toplamalar Azure Cosmos DB blog ile](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/). İşte nasıl onu toohello sonraki yapabileceğiniz Apache Spark düzeyi.

Bu toplamaları başvuru toohello olduğunu unutmayın [Spark tooAzure Cosmos DB bağlayıcı dizüstü](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).

### <a name="connect-tooflights-sample-data"></a>Tooflights örnek verileri Bağlan
Bu toplama örnekler depolanan bazı uçuş performans veri erişim bizim **DoctorWho** Azure Cosmos DB veritabanı. tooconnect tooit kod parçacığını aşağıdaki tooutilize hello gerekir:

```
// Import Spark tooAzure Cosmos DB connector
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Connect tooAzure Cosmos DB Database
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US 2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

Bu parçacığıyla de giderek toorun aktarımları Azure Cosmos DB tooSpark verilerden filtrelenmiş kümesi hello temel bir sorgu hello ikinci dağıtılmış toplamalar burada gerçekleştirebilirsiniz duyuyoruz. Bu durumda, sizden Seattle (SEA) gelen çok uçuşlar için istiyoruz.

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

Merhaba aşağıdaki sonuçları Jupyter Not Defteri hizmeti hello hello sorguları çalıştırarak üretilmiştir.  Tüm hello kod parçacıkları genel ve özel olmayan tooany hizmet olduğunu unutmayın.

### <a name="running-limit-and-count-queries"></a>Çalışan sınırı ve sayısı sorguları
Yalnızca gibi olduğunuz kullanılan tooin SQL/Spark SQL, şimdi başlangıçta bir **sınırı** sorgu:

![Spark sınırı sorgu](./media/spark-connector/spark-sql-query.png)

Merhaba sonraki basit ve hızlı sorgudur **sayısı** sorgu:

![Spark sayım sorgusu](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a>GROUP BY sorgusu
Bu sonraki kümesinde biz kolayca çalıştırabilirsiniz **GROUP BY** bizim Azure Cosmos DB veritabanı sorguları:

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Spark GROUP BY sorgu grafiği](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a>ORDER BY ayrı sorgu
Burada da bir **DISTINCT, ORDER BY** sorgu:

![Spark GROUP BY sorgu grafiği](./media/spark-connector/order-by-query.png)

### <a name="continue-hello-flight-data-analysis"></a>Merhaba uçuş veri analizi devam
Aşağıdaki örnek sorgular toocontinue hello uçuş veri analizini hello kullanabilirsiniz:

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a>İstanbul departing üst 5 Gecikmeli hedefleri (şehir)
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Spark üst gecikmeler grafiği](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a>Hedef Şehir İstanbul departing Medyan gecikmelerinden Hesapla
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Spark Medyan gecikmeler grafiği](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a>Sonraki adımlar

Henüz yapmadıysanız, hello Spark tooAzure Cosmos DB Bağlayıcısı hello indirme [azure cosmosdb spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub deposunu ve hello depodaki hello ek kaynakları araştırın:

* [Dağıtılmış toplamalar örnekleri](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)
* [Örnek komut dosyaları ve dizüstü bilgisayarlar](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)

Tooreview hello isteyebilirsiniz [Apache Spark SQL, DataFrames ve veri kümeleri Kılavuzu](http://spark.apache.org/docs/latest/sql-programming-guide.html) ve hello [Azure hdınsight'ta Apache Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) makalesi.
