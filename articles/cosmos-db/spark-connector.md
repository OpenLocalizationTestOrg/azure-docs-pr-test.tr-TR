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
# <a name="accelerate-real-time-big-data-analytics-with-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="b9247-104">Merhaba Spark tooAzure Cosmos DB Bağlayıcısı ile gerçek zamanlı büyük veri analizi hızlandırmak</span><span class="sxs-lookup"><span data-stu-id="b9247-104">Accelerate real-time big-data analytics with hello Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="b9247-105">Merhaba Spark tooAzure Cosmos DB bağlayıcı Azure Cosmos DB tooact bir giriş kaynağı ya da Apache Spark işleri için çıkış havuzu olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="b9247-105">hello Spark tooAzure Cosmos DB connector enables Azure Cosmos DB tooact as an input source or output sink for Apache Spark jobs.</span></span> <span data-ttu-id="b9247-106">Bağlanma [Spark](http://spark.apache.org/) çok[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) burada kullanabileceğiniz Azure Cosmos DB tooquickly sorunları sürdüremiyor ve veri sorgulama, özelliği toosolve hızlı taşıma veri bilimi hızlandırır.</span><span class="sxs-lookup"><span data-stu-id="b9247-106">Connecting [Spark](http://spark.apache.org/) too[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelerates your ability toosolve fast-moving data science problems where you can use Azure Cosmos DB tooquickly persist and query data.</span></span> <span data-ttu-id="b9247-107">Merhaba Spark tooAzure Cosmos DB bağlayıcı verimli bir şekilde hello yerel Azure Cosmos yönetilen DB dizinleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="b9247-107">hello Spark tooAzure Cosmos DB connector efficiently utilizes hello native Azure Cosmos DB managed indexes.</span></span> <span data-ttu-id="b9247-108">Merhaba dizinler güncelleştirilebilir sütunları analiz gerçekleştirmek ve nesnelerin interneti (IOT) toodata Bilim ve analizi senaryolarından aralığı verileri hızlı genel değiştirme karşı filtreleme itme aşağı koşulu dağıtılmış sağlar.</span><span class="sxs-lookup"><span data-stu-id="b9247-108">hello indexes enable updateable columns when you perform analytics and push-down predicate filtering against fast-changing globally distributed data, which range from Internet of Things (IoT) toodata science and analytics scenarios.</span></span>

<span data-ttu-id="b9247-109">Spark GraphX ve hello Gremlin grafik Azure Cosmos DB API'leri ile çalışmak için bkz: [Spark ve Apache TinkerPop Gremlin kullanarak grafik analytics gerçekleştirmek](spark-connector-graph.md).</span><span class="sxs-lookup"><span data-stu-id="b9247-109">For working with Spark GraphX and hello Gremlin graph APIs of Azure Cosmos DB, see [Perform graph analytics using Spark and Apache TinkerPop Gremlin](spark-connector-graph.md).</span></span>

## <a name="download"></a><span data-ttu-id="b9247-110">İndir</span><span class="sxs-lookup"><span data-stu-id="b9247-110">Download</span></span>

<span data-ttu-id="b9247-111">tooget başlatıldı, hello hello Spark tooAzure Cosmos DB Bağlayıcısı (Önizleme) yükleme [azure cosmosdb spark](https://github.com/Azure/azure-cosmosdb-spark/) github'daki.</span><span class="sxs-lookup"><span data-stu-id="b9247-111">tooget started, download hello Spark tooAzure Cosmos DB connector (preview) from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repository on GitHub.</span></span>

## <a name="connector-components"></a><span data-ttu-id="b9247-112">Bağlayıcı bileşenleri</span><span class="sxs-lookup"><span data-stu-id="b9247-112">Connector components</span></span>

<span data-ttu-id="b9247-113">Merhaba bağlayıcı bileşenlerini aşağıdaki hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="b9247-113">hello connector utilizes hello following components:</span></span>

* <span data-ttu-id="b9247-114">[Azure Cosmos DB](http://documentdb.com) özellikler esnek coğrafi bölgeler arasında herhangi bir sayı işleme ve depolama ölçek ve müşteriler tooprovision sağlar.</span><span class="sxs-lookup"><span data-stu-id="b9247-114">[Azure Cosmos DB](http://documentdb.com) enables customers tooprovision and elastically scale both throughput and storage across any number of geographical regions.</span></span> <span data-ttu-id="b9247-115">Merhaba hizmeti sunar:</span><span class="sxs-lookup"><span data-stu-id="b9247-115">hello service offers:</span></span>
   * <span data-ttu-id="b9247-116">Anahtar kapatma [genel dağıtım](distribute-data-globally.md) ve yatay ölçek</span><span class="sxs-lookup"><span data-stu-id="b9247-116">Turn key [global distribution](distribute-data-globally.md) and horizontal scale</span></span>
   * <span data-ttu-id="b9247-117">Tek basamaklı gecikmeleri hello 99 adresindeki garanti</span><span class="sxs-lookup"><span data-stu-id="b9247-117">Guaranteed single digit latencies at hello 99th percentile</span></span>
   * [<span data-ttu-id="b9247-118">Birden çok iyi tanımlanmış tutarlılık modelleri</span><span class="sxs-lookup"><span data-stu-id="b9247-118">Multiple well-defined consistency models</span></span>](consistency-levels.md)
   * <span data-ttu-id="b9247-119">Çok girişli özellikleriyle yüksek oranda kullanılabilirlik garanti</span><span class="sxs-lookup"><span data-stu-id="b9247-119">Guaranteed high availability with multi-homing capabilities</span></span>
   * <span data-ttu-id="b9247-120">Tüm özellikleri endüstri lideri tarafından kapsamlı yedeklenen [hizmet düzeyi sözleşmelerine](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLA).</span><span class="sxs-lookup"><span data-stu-id="b9247-120">All features are backed by industry-leading, comprehensive [service level agreements](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLAs).</span></span>

* <span data-ttu-id="b9247-121">[Apache Spark](http://spark.apache.org/) hızı, kullanımı kolay, gelişmiş analizler yerleşik bir güçlü açık kaynaklı işleme altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="b9247-121">[Apache Spark](http://spark.apache.org/) is a powerful open source processing engine that's built around speed, ease of use, and sophisticated analytics.</span></span>

* <span data-ttu-id="b9247-122">[Azure hdınsight'ta Apache Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) , Apache Spark kritik dağıtımlar için hello bulutta kullanarak dağıtabileceğiniz [Azure Hdınsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="b9247-122">[Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) so that you can deploy Apache Spark in hello cloud for mission-critical deployments by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="b9247-123">Resmi olarak desteklenen sürümler:</span><span class="sxs-lookup"><span data-stu-id="b9247-123">Officially supported versions:</span></span>

| <span data-ttu-id="b9247-124">Bileşen</span><span class="sxs-lookup"><span data-stu-id="b9247-124">Component</span></span> | <span data-ttu-id="b9247-125">Sürüm</span><span class="sxs-lookup"><span data-stu-id="b9247-125">Version</span></span> |
|---------|-------|
|<span data-ttu-id="b9247-126">Apache Spark</span><span class="sxs-lookup"><span data-stu-id="b9247-126">Apache Spark</span></span>|<span data-ttu-id="b9247-127">2.0+</span><span class="sxs-lookup"><span data-stu-id="b9247-127">2.0+</span></span>|
| <span data-ttu-id="b9247-128">Scala</span><span class="sxs-lookup"><span data-stu-id="b9247-128">Scala</span></span>| <span data-ttu-id="b9247-129">2.11</span><span class="sxs-lookup"><span data-stu-id="b9247-129">2.11</span></span>|
| <span data-ttu-id="b9247-130">Azure DocumentDB Java SDK'sı</span><span class="sxs-lookup"><span data-stu-id="b9247-130">Azure DocumentDB Java SDK</span></span> | <span data-ttu-id="b9247-131">1.10.0</span><span class="sxs-lookup"><span data-stu-id="b9247-131">1.10.0</span></span> |

<span data-ttu-id="b9247-132">Bu makalede, Python (pyDocumentDB) kullanarak bazı basit örneklerini çalıştırma ve Scala arabirimleri hello yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b9247-132">This article helps you run some simple samples by using Python (via pyDocumentDB) and hello Scala interfaces.</span></span>

<span data-ttu-id="b9247-133">İki yaklaşım tooconnect Apache Spark ve Azure Cosmos DB vardır:</span><span class="sxs-lookup"><span data-stu-id="b9247-133">There are two approaches tooconnect Apache Spark and Azure Cosmos DB:</span></span>
- <span data-ttu-id="b9247-134">Merhaba aracılığıyla pyDocumentDB kullanmak [Azure DocumentDB Python SDK'sı](https://github.com/Azure/azure-documentdb-python).</span><span class="sxs-lookup"><span data-stu-id="b9247-134">Use pyDocumentDB via hello [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span></span>
- <span data-ttu-id="b9247-135">Bir Java tabanlı Spark tooAzure Cosmos DB hello yararlanarak oluşturmanıza [Azure DocumentDB Java SDK'sı](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="b9247-135">Create a Java-based Spark tooAzure Cosmos DB connector by utilizing hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

## <a name="pydocumentdb-implementation"></a><span data-ttu-id="b9247-136">pyDocumentDB uygulama</span><span class="sxs-lookup"><span data-stu-id="b9247-136">pyDocumentDB implementation</span></span>
<span data-ttu-id="b9247-137">Merhaba geçerli [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) hello Aşağıdaki diyagramda gösterildiği gibi tooconnect Spark tooAzure Cosmos DB sağlar:</span><span class="sxs-lookup"><span data-stu-id="b9247-137">hello current [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) enables you tooconnect Spark tooAzure Cosmos DB as shown in hello following diagram:</span></span>

![Spark tooAzure pyDocumentDB DB aracılığıyla Cosmos DB veri akışı](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-hello-pydocumentdb-implementation"></a><span data-ttu-id="b9247-139">Veri akışı hello pyDocumentDB uygulama</span><span class="sxs-lookup"><span data-stu-id="b9247-139">Data flow of hello pyDocumentDB implementation</span></span>

<span data-ttu-id="b9247-140">Merhaba veri akışı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="b9247-140">hello data flow is as follows:</span></span>

1. <span data-ttu-id="b9247-141">Merhaba Spark ana düğüm toohello Azure Cosmos DB ağ geçidi düğümü pyDocumentDB üzerinden bağlanır.</span><span class="sxs-lookup"><span data-stu-id="b9247-141">hello Spark master node connects toohello Azure Cosmos DB gateway node via pyDocumentDB.</span></span> <span data-ttu-id="b9247-142">Bir kullanıcı yalnızca hello Spark ve Azure Cosmos DB bağlantıları belirtir.</span><span class="sxs-lookup"><span data-stu-id="b9247-142">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="b9247-143">Bağlantıları toohello ilgili ana ve ağ geçidi düğümleri saydam toohello kullanıcısıysanız.</span><span class="sxs-lookup"><span data-stu-id="b9247-143">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="b9247-144">Merhaba ağ geçidi düğümü Azure Cosmos hello sorgu daha sonra hello veri düğümlerini hello koleksiyonunun bölümlerinde karşı çalıştığı DB hello sorgusu yapar.</span><span class="sxs-lookup"><span data-stu-id="b9247-144">hello gateway node makes hello query against Azure Cosmos DB where hello query subsequently runs against hello collection's partitions in hello data nodes.</span></span> <span data-ttu-id="b9247-145">Bu sorguları için Hello yanıt toohello ağ geçidi düğümü ve bu sonuç kümesi toohello Spark ana düğüm döndürülür geri gönderilir.</span><span class="sxs-lookup"><span data-stu-id="b9247-145">hello response for those queries is sent back toohello gateway node, and that result set is returned toohello Spark master node.</span></span>
3. <span data-ttu-id="b9247-146">Sonraki sorguları (örneğin, bir Spark DataFrame) toohello Spark çalışan düğümleri işleme gönderilir.</span><span class="sxs-lookup"><span data-stu-id="b9247-146">Subsequent queries (for example, against a Spark DataFrame) are sent toohello Spark worker nodes for processing.</span></span>

<span data-ttu-id="b9247-147">Spark Azure Cosmos DB arasındaki iletişimi sınırlı toohello Spark ana düğüm ve Azure Cosmos DB ağ geçidi düğümleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="b9247-147">Communication between Spark and Azure Cosmos DB is limited toohello Spark master node and Azure Cosmos DB gateway nodes.</span></span>  <span data-ttu-id="b9247-148">Merhaba sorguları hello Aktarım katmanı bu iki düğüm arasında verir kadar hızlı gidin.</span><span class="sxs-lookup"><span data-stu-id="b9247-148">hello queries go as fast as hello transport layer between these two nodes allows.</span></span>

### <a name="install-pydocumentdb"></a><span data-ttu-id="b9247-149">PyDocumentDB yükleyin</span><span class="sxs-lookup"><span data-stu-id="b9247-149">Install pyDocumentDB</span></span>
<span data-ttu-id="b9247-150">Kullanarak, sürücü düğümde pyDocumentDB yükleyebilirsiniz **PIP**, örneğin:</span><span class="sxs-lookup"><span data-stu-id="b9247-150">You can install pyDocumentDB on your driver node by using **pip**, for example:</span></span>

```
pip install pyDocumentDB
```


### <a name="connect-spark-tooazure-cosmos-db-via-pydocumentdb"></a><span data-ttu-id="b9247-151">Spark tooAzure Cosmos DB pyDocumentDB aracılığıyla bağlanma</span><span class="sxs-lookup"><span data-stu-id="b9247-151">Connect Spark tooAzure Cosmos DB via pyDocumentDB</span></span>
<span data-ttu-id="b9247-152">Merhaba Basitlik hello iletişim taşıma pyDocumentDB görece basit kullanarak Spark tooAzure Cosmos DB sorgudan yürütülmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="b9247-152">hello simplicity of hello communication transport makes execution of a query from Spark tooAzure Cosmos DB by using pyDocumentDB relatively simple.</span></span>

<span data-ttu-id="b9247-153">kod parçacığı gösterir nasıl aşağıdaki hello Spark bağlamda toouse pyDocumentDB.</span><span class="sxs-lookup"><span data-stu-id="b9247-153">hello following code snippet shows how toouse pyDocumentDB in a Spark context.</span></span>

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

<span data-ttu-id="b9247-154">Merhaba kod parçacığında belirtildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="b9247-154">As noted in hello code snippet:</span></span>

* <span data-ttu-id="b9247-155">Hello Azure Cosmos DB Python SDK'sını (`pyDocumentDB`) hello içeren tüm gerekli bağlantı parametrelerini hello.</span><span class="sxs-lookup"><span data-stu-id="b9247-155">hello Azure Cosmos DB Python SDK (`pyDocumentDB`) contains hello all hello necessary connection parameters.</span></span> <span data-ttu-id="b9247-156">Örneğin, hello hello çoğaltma ve öncelik sırasını okuma konumları parametre seçer tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="b9247-156">For example, hello preferred locations parameter chooses hello read replica and priority order.</span></span>
*  <span data-ttu-id="b9247-157">Merhaba gerekli kitaplıkları içeri aktarma ve yapılandırma, **masterKey** ve **konak** toocreate hello Azure Cosmos DB *istemci* (**pydocumentdb.document_ İstemci**).</span><span class="sxs-lookup"><span data-stu-id="b9247-157">Import hello necessary libraries and configure your **masterKey** and **host** toocreate hello Azure Cosmos DB *client* (**pydocumentdb.document_client**).</span></span>


### <a name="execute-spark-queries-via-pydocumentdb"></a><span data-ttu-id="b9247-158">PyDocumentDB Spark sorgularını Yürüt</span><span class="sxs-lookup"><span data-stu-id="b9247-158">Execute Spark Queries via pyDocumentDB</span></span>
<span data-ttu-id="b9247-159">Merhaba önceki parçacığında hello kullanılarak oluşturulmuş örnekleri kullan hello Azure Cosmos DB örneği aşağıdaki hello salt okunur anahtarları belirtildi.</span><span class="sxs-lookup"><span data-stu-id="b9247-159">hello following examples use hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="b9247-160">Merhaba aşağıdaki kod parçacığını bağlayan toohello **airports.codes** hello DoctorWho hesabı olarak koleksiyonunda daha önce belirtilen ve bir sorgu tooextract hello havaalanı Şehir Washington durumunda çalışır.</span><span class="sxs-lookup"><span data-stu-id="b9247-160">hello following code snippet connects toohello **airports.codes** collection in hello DoctorWho account as specified earlier and runs a query tooextract hello airport cities in Washington state.</span></span>

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

<span data-ttu-id="b9247-161">Aracılığıyla Hello sorgu yürütüldükten sonra **sorgu**, hello sonucu olan bir **query_iterable. QueryIterable** diğer bir deyişle dönüştürülmüş tooa Python listesi.</span><span class="sxs-lookup"><span data-stu-id="b9247-161">After hello query has been executed via **query**, hello result is a **query_iterable.QueryIterable** that is converted tooa Python list.</span></span> <span data-ttu-id="b9247-162">Python listesini koddan hello kullanarak kolayca dönüştürülmüş tooa Spark DataFrame olabilir:</span><span class="sxs-lookup"><span data-stu-id="b9247-162">A Python list can be easily converted tooa Spark DataFrame by using hello following code:</span></span>

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-hello-pydocumentdb-tooconnect-spark-tooazure-cosmos-db"></a><span data-ttu-id="b9247-163">Merhaba pyDocumentDB tooconnect Spark tooAzure Cosmos DB neden kullanılır?</span><span class="sxs-lookup"><span data-stu-id="b9247-163">Why use hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB?</span></span>
<span data-ttu-id="b9247-164">Cosmos pyDocumentDB kullanarak DB. genellikle senaryoları için Spark tooAzure bağlanma burada:</span><span class="sxs-lookup"><span data-stu-id="b9247-164">Connecting Spark tooAzure Cosmos DB by using pyDocumentDB is typically for scenarios where:</span></span>

* <span data-ttu-id="b9247-165">Toouse Python istiyor.</span><span class="sxs-lookup"><span data-stu-id="b9247-165">You want toouse Python.</span></span>
* <span data-ttu-id="b9247-166">Görece küçük bir sonuç Azure Cosmos DB tooSpark kümesi iade ettiğiniz.</span><span class="sxs-lookup"><span data-stu-id="b9247-166">You are returning a relatively small result set from Azure Cosmos DB tooSpark.</span></span> <span data-ttu-id="b9247-167">Temel alınan veri kümesi Azure Cosmos veritabanı hello Not oldukça büyük olabilir.</span><span class="sxs-lookup"><span data-stu-id="b9247-167">Note that hello underlying dataset in Azure Cosmos DB can be quite large.</span></span> <span data-ttu-id="b9247-168">Koşul filtreleri Azure Cosmos DB kaynağınız karşı çalışan filtreleri, diğer bir deyişle, uyguladığınızı.</span><span class="sxs-lookup"><span data-stu-id="b9247-168">You are applying filters, that is, running predicate filters, against your Azure Cosmos DB source.</span></span>  

## <a name="spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="b9247-169">Spark tooAzure Cosmos DB Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="b9247-169">Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="b9247-170">Merhaba Spark tooAzure Cosmos DB bağlayıcı yararlanan hello [Azure DocumentDB Java SDK'sı](https://github.com/Azure/azure-documentdb-java) ve verileri hello Aşağıdaki diyagramda gösterildiği gibi Azure Cosmos DB hello Spark çalışan düğümleri arasında taşır:</span><span class="sxs-lookup"><span data-stu-id="b9247-170">hello Spark tooAzure Cosmos DB connector utilizes hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) and moves data between hello Spark worker nodes and Azure Cosmos DB as shown in hello following diagram:</span></span>

![Veri akışı hello Spark tooAzure Cosmos DB Bağlayıcısı](./media/spark-connector/spark-connector.png)

<span data-ttu-id="b9247-172">Merhaba veri akışı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="b9247-172">hello data flow is as follows:</span></span>

1. <span data-ttu-id="b9247-173">Merhaba Spark ana düğüm toohello Azure Cosmos DB ağ geçidi düğümü tooobtain hello bölüm Haritası bağlanır.</span><span class="sxs-lookup"><span data-stu-id="b9247-173">hello Spark master node connects toohello Azure Cosmos DB gateway node tooobtain hello partition map.</span></span> <span data-ttu-id="b9247-174">Bir kullanıcı yalnızca hello Spark ve Azure Cosmos DB bağlantıları belirtir.</span><span class="sxs-lookup"><span data-stu-id="b9247-174">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="b9247-175">Bağlantıları toohello ilgili ana ve ağ geçidi düğümleri saydam toohello kullanıcısıysanız.</span><span class="sxs-lookup"><span data-stu-id="b9247-175">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="b9247-176">Bu bilgiler geri toohello Spark ana düğüm sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b9247-176">This information is provided back toohello Spark master node.</span></span>  <span data-ttu-id="b9247-177">Bu noktada, mümkün tooparse hello query toodetermine hello bölümleri ve konumlarını Azure Cosmos tooaccess gereken veritabanı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b9247-177">At this point, you should be able tooparse hello query toodetermine hello partitions and their locations in Azure Cosmos DB that you need tooaccess.</span></span>
3. <span data-ttu-id="b9247-178">Bu bilgiler iletilen toohello Spark çalışan düğümü olur.</span><span class="sxs-lookup"><span data-stu-id="b9247-178">This information is transmitted toohello Spark worker nodes.</span></span>
4. <span data-ttu-id="b9247-179">tooextract veri hello ve hello veri toohello Spark bölümleri hello Spark alt düğümler dönüş doğrudan hello Spark çalışan düğümleri toohello Azure Cosmos DB bölümleri bağlanır.</span><span class="sxs-lookup"><span data-stu-id="b9247-179">hello Spark worker nodes connect toohello Azure Cosmos DB partitions directly tooextract hello data and return hello data toohello Spark partitions in hello Spark worker nodes.</span></span>

<span data-ttu-id="b9247-180">Merhaba veri taşıma hello Spark çalışan düğümleri ve hello Azure Cosmos DB veri düğümleri (bölümler) olduğundan Spark Azure Cosmos DB arasındaki iletişimi önemli ölçüde daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="b9247-180">Communication between Spark and Azure Cosmos DB is significantly faster because hello data movement is between hello Spark worker nodes and hello Azure Cosmos DB data nodes (partitions).</span></span>

### <a name="build-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="b9247-181">Merhaba Spark tooAzure Cosmos DB bağlayıcısı oluşturun</span><span class="sxs-lookup"><span data-stu-id="b9247-181">Build hello Spark tooAzure Cosmos DB connector</span></span>
<span data-ttu-id="b9247-182">Şu anda hello bağlayıcı proje maven kullanır.</span><span class="sxs-lookup"><span data-stu-id="b9247-182">Currently, hello connector project uses maven.</span></span> <span data-ttu-id="b9247-183">toobuild hello bağlayıcı bağımlılıklar olmadan çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b9247-183">toobuild hello connector without dependencies, you can run:</span></span>
```
mvn clean package
```
<span data-ttu-id="b9247-184">Merhaba JAR en son sürümlerini hello hello indirebilirsiniz *serbest* klasör.</span><span class="sxs-lookup"><span data-stu-id="b9247-184">You can also download hello latest versions of hello JAR from hello *releases* folder.</span></span>

### <a name="include-hello-azure-cosmos-db-spark-jar"></a><span data-ttu-id="b9247-185">Hello Azure Cosmos DB Spark JAR Ekle</span><span class="sxs-lookup"><span data-stu-id="b9247-185">Include hello Azure Cosmos DB Spark JAR</span></span>
<span data-ttu-id="b9247-186">Herhangi bir kod çalıştırmadan önce tooinclude hello Azure Cosmos DB Spark JAR gerekir.</span><span class="sxs-lookup"><span data-stu-id="b9247-186">Before you execute any code, you need tooinclude hello Azure Cosmos DB Spark JAR.</span></span>  <span data-ttu-id="b9247-187">Merhaba kullanıyorsanız **spark Kabuk**, hello kullanarak hello JAR içerebilir sonra **--Kavanoz** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="b9247-187">If you are using hello **spark-shell**, then you can include hello JAR by using hello **--jars** option.</span></span>  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

<span data-ttu-id="b9247-188">Bağımlılıklar olmadan tooexecute hello JAR koddan hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="b9247-188">If you want tooexecute hello JAR without dependencies, use hello following code:</span></span>

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

<span data-ttu-id="b9247-189">Azure Hdınsight Jupyter Not Defteri hizmeti gibi bir Not Defteri hizmeti kullanıyorsanız, hello kullanabilirsiniz **spark Sihirli** komutlar:</span><span class="sxs-lookup"><span data-stu-id="b9247-189">If you are using a notebook service such as Azure HDInsight Jupyter notebook service, you can use hello **spark magic** commands:</span></span>

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

<span data-ttu-id="b9247-190">Merhaba **Kavanoz** etkinleştirir, tooinclude iki hello Jar'lar komutu için gereken **azure cosmosdb spark** (kendisi ve da hello Azure DocumentDB Java SDK'sı) ve çıkarma **scala-yansıtmak** Livy çağırır hello ile etkilemediğinden emin (Jupyter not defteri > Livy > Spark).</span><span class="sxs-lookup"><span data-stu-id="b9247-190">hello **jars** command enables you tooinclude hello two JARs that are needed for **azure-cosmosdb-spark** (itself and hello Azure DocumentDB Java SDK) and exclude **scala-reflect** so that it does not interfere with hello Livy calls (Jupyter notebook > Livy > Spark).</span></span>

### <a name="connect-spark-tooazure-cosmos-db-using-hello-connector"></a><span data-ttu-id="b9247-191">Spark bağlanmak tooAzure Cosmos DB kullanarak hello Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="b9247-191">Connect Spark tooAzure Cosmos DB using hello connector</span></span>
<span data-ttu-id="b9247-192">Merhaba iletişimi aktarım biraz daha karmaşık olsa da, Spark tooAzure bir sorgu yürütülürken Cosmos hello bağlayıcısını kullanarak DB önemli ölçüde daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="b9247-192">Although hello communication transport is a little more complicated, executing a query from Spark tooAzure Cosmos DB by using hello connector is significantly faster.</span></span>

<span data-ttu-id="b9247-193">Aşağıdaki kod parçacığını hello nasıl toouse hello Spark bağlamda bağlayıcı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b9247-193">hello following code snippet shows how toouse hello connector in a Spark context.</span></span>

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

<span data-ttu-id="b9247-194">Merhaba kod parçacığında belirtildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="b9247-194">As noted in hello code snippet:</span></span>

- <span data-ttu-id="b9247-195">**Azure cosmosdb spark** hello içeren tüm tercih edilen hello konumlarını dahil gerekli bağlantı parametrelerini hello.</span><span class="sxs-lookup"><span data-stu-id="b9247-195">**azure-cosmosdb-spark** contains hello all hello necessary connection parameters, which include hello preferred locations.</span></span> <span data-ttu-id="b9247-196">Örneğin, çoğaltma ve öncelik sırasını hello okuma seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9247-196">For example, you can choose hello read replica and priority order.</span></span>
- <span data-ttu-id="b9247-197">Yalnızca hello gerekli kitaplıkları içeri aktarma ve masterKey ve ana bilgisayar toocreate hello Azure Cosmos DB istemcinizi yapılandırmak.</span><span class="sxs-lookup"><span data-stu-id="b9247-197">Just import hello necessary libraries and configure your masterKey and host toocreate hello Azure Cosmos DB client.</span></span>

### <a name="execute-spark-queries-via-hello-connector"></a><span data-ttu-id="b9247-198">Merhaba bağlayıcısı aracılığıyla Spark sorgularını Yürüt</span><span class="sxs-lookup"><span data-stu-id="b9247-198">Execute Spark queries via hello connector</span></span>

<span data-ttu-id="b9247-199">Merhaba önceki parçacığında hello kullanılarak oluşturulmuş örnek kullanır hello Azure Cosmos DB örneği aşağıdaki hello salt okunur anahtarları belirtildi.</span><span class="sxs-lookup"><span data-stu-id="b9247-199">hello following example uses hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="b9247-200">Merhaba aşağıdaki kod parçacığını toohello DepartureDelays.flights_pcoll koleksiyonunda (Merhaba DoctorWho hesabını daha önce belirtildiği gibi) bağlanır ve bir sorgu tooextract hello uçuş gecikme bilgilerinin İstanbul departing uçuşlar çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="b9247-200">hello following code snippet connects toohello DepartureDelays.flights_pcoll collection (in hello DoctorWho account as specified earlier) and runs a query tooextract hello flight delay information of flights that are departing from Seattle.</span></span>

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-hello-spark-tooazure-cosmos-db-connector-implementation"></a><span data-ttu-id="b9247-201">Merhaba Spark tooAzure Cosmos DB bağlayıcı uygulama neden kullanılır?</span><span class="sxs-lookup"><span data-stu-id="b9247-201">Why use hello Spark tooAzure Cosmos DB connector implementation?</span></span>

<span data-ttu-id="b9247-202">Cosmos hello bağlayıcısını kullanarak DB. genellikle senaryoları için Spark tooAzure bağlanma burada:</span><span class="sxs-lookup"><span data-stu-id="b9247-202">Connecting Spark tooAzure Cosmos DB by using hello connector is typically for scenarios where:</span></span>

* <span data-ttu-id="b9247-203">Toouse Scala istediğiniz ve tooinclude de belirtildiği gibi bir Python sarmalayıcı güncelleştirme [sorunu 3: ekleme Python sarmalayıcı ve örnekler](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span><span class="sxs-lookup"><span data-stu-id="b9247-203">You want toouse Scala and update it tooinclude a Python wrapper as noted in [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span></span>
* <span data-ttu-id="b9247-204">Çok miktarda veri tootransfer Apache Spark Azure Cosmos DB arasındaki sahip.</span><span class="sxs-lookup"><span data-stu-id="b9247-204">You have a large amount of data tootransfer between Apache Spark and Azure Cosmos DB.</span></span>

<span data-ttu-id="b9247-205">toogive hello sorgu performans farkı hakkında bir fikir gördüğünüz hello [sorgu Test çalışmalarını wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span><span class="sxs-lookup"><span data-stu-id="b9247-205">toogive you an idea of hello query performance difference, see hello [Query Test Runs wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span></span>

## <a name="distributed-aggregation-example"></a><span data-ttu-id="b9247-206">Dağıtılmış toplama örneği</span><span class="sxs-lookup"><span data-stu-id="b9247-206">Distributed aggregation example</span></span>
<span data-ttu-id="b9247-207">Bu bölümde bazı örnekleri nasıl dağıtılmış toplamalar ve analizi birlikte Apache Spark ve Azure Cosmos DB kullanarak bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9247-207">This section provides some examples of how you can do distributed aggregations and analytics by using Apache Spark and Azure Cosmos DB together.</span></span> <span data-ttu-id="b9247-208">Destekleyen zaten toplamalar, Azure Cosmos DB hello ele alınmıştır [Planet ölçek toplamalar Azure Cosmos DB blog ile](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span><span class="sxs-lookup"><span data-stu-id="b9247-208">Azure Cosmos DB already supports aggregations, which is discussed in hello [Planet scale aggregates with Azure Cosmos DB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span></span> <span data-ttu-id="b9247-209">İşte nasıl onu toohello sonraki yapabileceğiniz Apache Spark düzeyi.</span><span class="sxs-lookup"><span data-stu-id="b9247-209">Here is how you can take it toohello next level with Apache Spark.</span></span>

<span data-ttu-id="b9247-210">Bu toplamaları başvuru toohello olduğunu unutmayın [Spark tooAzure Cosmos DB bağlayıcı dizüstü](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span><span class="sxs-lookup"><span data-stu-id="b9247-210">Note that these aggregations are in reference toohello [Spark tooAzure Cosmos DB Connector notebook](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span></span>

### <a name="connect-tooflights-sample-data"></a><span data-ttu-id="b9247-211">Tooflights örnek verileri Bağlan</span><span class="sxs-lookup"><span data-stu-id="b9247-211">Connect tooflights sample data</span></span>
<span data-ttu-id="b9247-212">Bu toplama örnekler depolanan bazı uçuş performans veri erişim bizim **DoctorWho** Azure Cosmos DB veritabanı.</span><span class="sxs-lookup"><span data-stu-id="b9247-212">These aggregation examples access some flight performance data that's stored in our **DoctorWho** Azure Cosmos DB database.</span></span> <span data-ttu-id="b9247-213">tooconnect tooit kod parçacığını aşağıdaki tooutilize hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b9247-213">tooconnect tooit, you need tooutilize hello following code snippet:</span></span>

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

<span data-ttu-id="b9247-214">Bu parçacığıyla de giderek toorun aktarımları Azure Cosmos DB tooSpark verilerden filtrelenmiş kümesi hello temel bir sorgu hello ikinci dağıtılmış toplamalar burada gerçekleştirebilirsiniz duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="b9247-214">With this snippet, we are also going toorun a base query that transfers hello filtered set of data from Azure Cosmos DB tooSpark where hello latter can perform distributed aggregates.</span></span> <span data-ttu-id="b9247-215">Bu durumda, sizden Seattle (SEA) gelen çok uçuşlar için istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="b9247-215">In this case, we are asking for flights that depart from Seattle (SEA).</span></span>

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

<span data-ttu-id="b9247-216">Merhaba aşağıdaki sonuçları Jupyter Not Defteri hizmeti hello hello sorguları çalıştırarak üretilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b9247-216">hello following results were generated by running hello queries from hello Jupyter notebook service.</span></span>  <span data-ttu-id="b9247-217">Tüm hello kod parçacıkları genel ve özel olmayan tooany hizmet olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b9247-217">Note that all hello code snippets are generic and not specific tooany service.</span></span>

### <a name="running-limit-and-count-queries"></a><span data-ttu-id="b9247-218">Çalışan sınırı ve sayısı sorguları</span><span class="sxs-lookup"><span data-stu-id="b9247-218">Running LIMIT and COUNT queries</span></span>
<span data-ttu-id="b9247-219">Yalnızca gibi olduğunuz kullanılan tooin SQL/Spark SQL, şimdi başlangıçta bir **sınırı** sorgu:</span><span class="sxs-lookup"><span data-stu-id="b9247-219">Just like you're used tooin SQL/Spark SQL, let's start off with a **LIMIT** query:</span></span>

![Spark sınırı sorgu](./media/spark-connector/spark-sql-query.png)

<span data-ttu-id="b9247-221">Merhaba sonraki basit ve hızlı sorgudur **sayısı** sorgu:</span><span class="sxs-lookup"><span data-stu-id="b9247-221">hello next query is a simple and fast **COUNT** query:</span></span>

![Spark sayım sorgusu](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a><span data-ttu-id="b9247-223">GROUP BY sorgusu</span><span class="sxs-lookup"><span data-stu-id="b9247-223">GROUP BY query</span></span>
<span data-ttu-id="b9247-224">Bu sonraki kümesinde biz kolayca çalıştırabilirsiniz **GROUP BY** bizim Azure Cosmos DB veritabanı sorguları:</span><span class="sxs-lookup"><span data-stu-id="b9247-224">In this next set, we can easily run **GROUP BY** queries against our Azure Cosmos DB database:</span></span>

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Spark GROUP BY sorgu grafiği](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a><span data-ttu-id="b9247-226">ORDER BY ayrı sorgu</span><span class="sxs-lookup"><span data-stu-id="b9247-226">DISTINCT, ORDER BY query</span></span>
<span data-ttu-id="b9247-227">Burada da bir **DISTINCT, ORDER BY** sorgu:</span><span class="sxs-lookup"><span data-stu-id="b9247-227">And here is a **DISTINCT, ORDER BY** query:</span></span>

![Spark GROUP BY sorgu grafiği](./media/spark-connector/order-by-query.png)

### <a name="continue-hello-flight-data-analysis"></a><span data-ttu-id="b9247-229">Merhaba uçuş veri analizi devam</span><span class="sxs-lookup"><span data-stu-id="b9247-229">Continue hello flight data analysis</span></span>
<span data-ttu-id="b9247-230">Aşağıdaki örnek sorgular toocontinue hello uçuş veri analizini hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b9247-230">You can use hello following example queries toocontinue analysis of hello flight data:</span></span>

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a><span data-ttu-id="b9247-231">İstanbul departing üst 5 Gecikmeli hedefleri (şehir)</span><span class="sxs-lookup"><span data-stu-id="b9247-231">Top 5 delayed destinations (cities) departing from Seattle</span></span>
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Spark üst gecikmeler grafiği](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a><span data-ttu-id="b9247-233">Hedef Şehir İstanbul departing Medyan gecikmelerinden Hesapla</span><span class="sxs-lookup"><span data-stu-id="b9247-233">Calculate median delays by destination cities departing from Seattle</span></span>
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Spark Medyan gecikmeler grafiği](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a><span data-ttu-id="b9247-235">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b9247-235">Next steps</span></span>

<span data-ttu-id="b9247-236">Henüz yapmadıysanız, hello Spark tooAzure Cosmos DB Bağlayıcısı hello indirme [azure cosmosdb spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub deposunu ve hello depodaki hello ek kaynakları araştırın:</span><span class="sxs-lookup"><span data-stu-id="b9247-236">If you haven't already, download hello Spark tooAzure Cosmos DB connector from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository and explore hello additional resources in hello repo:</span></span>

* [<span data-ttu-id="b9247-237">Dağıtılmış toplamalar örnekleri</span><span class="sxs-lookup"><span data-stu-id="b9247-237">Distributed Aggregations Examples</span></span>](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)
* [<span data-ttu-id="b9247-238">Örnek komut dosyaları ve dizüstü bilgisayarlar</span><span class="sxs-lookup"><span data-stu-id="b9247-238">Sample Scripts and Notebooks</span></span>](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)

<span data-ttu-id="b9247-239">Tooreview hello isteyebilirsiniz [Apache Spark SQL, DataFrames ve veri kümeleri Kılavuzu](http://spark.apache.org/docs/latest/sql-programming-guide.html) ve hello [Azure hdınsight'ta Apache Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="b9247-239">You might also want tooreview hello [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and hello [Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) article.</span></span>
