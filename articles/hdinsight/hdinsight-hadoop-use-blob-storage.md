---
title: "aaaQuery verileri HDFS uyumlu Azure depolama - Azure Hdınsight | Microsoft Docs"
description: "Azure depolama ve Azure Data Lake Store toostore tooquery verilerini nasıl sonuçları öğrenin çözümleme."
keywords: "blob depolama,hdfs,yapılandırılmış veriler,yapılandırılmamış veriler,data lake store,Hadoop girdisi,Hadoop çıktısı, hadoop depolama, hdfs girdisi,hdfs çıktısı,hdfs depolama,wasb azure"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1d2e65f2-16de-449e-915f-3ffbc230f815
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: jgao
ms.openlocfilehash: 1032d60424b65e3c0c54a25c7c15970b017a788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a>Azure HDInsight kümeleri ile Azure Depolama'yı kullanma

Hdınsight kümesi tooanalyze verilerin hello verileri Azure Storage, Azure Data Lake Store veya her ikisi de depolayabilirsiniz. Her iki depolama seçeneklerini kullanıcı verilerini kaybetmeden hesaplama için kullanılan Hdınsight kümeleri toosafely delete etkinleştirin.

Hadoop hello varsayılan dosya sistemi kavramını destekler. Merhaba varsayılan dosya sistemi varsayılan şema ve yetkilisi anlamına gelir. Kullanılan tooresolve göreli yollar da olabilir. Merhaba Hdınsight küme oluşturma işlemi sırasında hello varsayılan dosya sistemi olarak Azure storage'da bir blob kapsayıcısını belirtin veya Hdınsight 3.5 ile birlikte, Azure Storage veya Azure Data Lake Store birkaç istisna dışında hello varsayılan dosya sistemi olarak seçebilirsiniz. Merhaba desteklenebilirlik Data Lake Store hello varsayılan ve bağlantılı depolama alanı kullanma Bkz [Hdınsight kümesi için kullanılabilirliklerinin](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).

Bu makalede Azure Depolama'nın HDInsight kümeleri ile nasıl çalıştığı hakkında bilgi edinebilirsiniz. Data Lake Store Hdınsight kümeleri ile nasıl çalışır toolearn bkz [kullanım Azure Data Lake Store ile Azure Hdınsight kümeleri](hdinsight-hadoop-use-data-lake-store.md). HDInsight kümesi oluşturma hakkında daha fazla bilgi için bkz. [HDInsight'ta Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).

Azure depolama, HDInsight ile sorunsuz bir şekilde tümleşen, sağlam ve genel amaçlı bir depolama çözümüdür. Hdınsight bir blob kapsayıcısını Azure Storage'da hello varsayılan dosya sistemi olarak hello küme için kullanabilirsiniz. Hadoop dağıtılmış dosya sistemi (HDFS) arabirimi aracılığıyla, Hdınsight'taki bileşenler hello kümesini BLOB olarak depolanan doğrudan yapılandırılmış veya yapılandırılmamış veriler üzerinde çalışabilir.

> [!WARNING]
> Azure Depolama hesabı oluşturmanın birden fazla yolu vardır. Aşağıdaki tablonun hello Hdınsight ile hangi seçenekleri desteklenen bilgileri sağlar:
> 
> | Depolama hesabı türü | Depolama katmanı | HDInsight ile desteklenen |
> | ------- | ------- | ------- |
> | Genel amaçlı Depolama Hesabı | Standart | __Evet__ |
> | &nbsp; | Premium | Hayır |
> | Blob Depolama Hesabı | Sık Erişimli | Hayır |
> | &nbsp; | Seyrek Erişimli | Hayır |

Hello varsayılan blob kapsayıcısı iş verilerini depolamak için kullanmanızı önermiyoruz. Her kullanım tooreduce sonra Hello varsayılan blob kapsayıcısını silmek depolama maliyeti iyi bir uygulamadır. Not Bu hello varsayılan kapsayıcı içeren uygulama ve sistem günlükleri. Emin tooretrieve hello günlükleri hello kapsayıcı silmeden önce yapın.

Bir blob kapsayıcısının birden fazla küme için paylaşımı desteklenmez.

## <a name="hdinsight-storage-architecture"></a>HDInsight depolama mimarisi
Aşağıdaki diyagramda hello hello Azure Storage kullanarak Hdınsight depolama mimarisine ilişkin özet görünümünü sağlar:

![Hadoop kümeleri Blob storage'da yapılandırılmış ve yapılandırılmamış verileri depolamak ve hello HDFS API'sini tooaccess kullanın. ] (./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "Hdınsight depolama mimarisi")

Hdınsight, yerel olarak erişim toohello dağıtılmış dosya sistemi toohello işlem düğümlerine ekli sağlar. Bu dosya sistemi kullanılarak erişilebilir hello tam URI, örneğin:

    hdfs://<namenodehost>/<path>

Ayrıca, Hdınsight Azure depolama alanında depolanır tooaccess veri sağlar. Merhaba sözdizimi aşağıdaki gibidir:

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

HDInsight kümeleriyle Azure Depolama hesabını kullanırken dikkat etmeniz gereken bazı noktalar mevcuttur.

* **Bağlı tooa küme hello depolama hesaplarındaki kapsayıcılar:** hello hesap adı ve anahtar oluşturma sırasında hello kümeyle ilişkilendirildiğinden, bu kapsayıcılardaki blob'lara tam erişim toohello sahip.

* **Genel kapsayıcılar veya genel BLOB'lar olmayan depolama hesaplarındaki bağlı tooa küme:** salt okunur izni toohello bloblar hello kapsayıcılarında sahiptir.
  
  > [!NOTE]
  > Genel kapsayıcılar tooget kapsayıcı meta verilerini almak ve bu kapsayıcıda bulunan tüm BLOB listesini sağlar. Yalnızca hello tam URL'yi biliyorsanız genel BLOB'lar tooaccess hello BLOB'lar izin verin. Daha fazla bilgi için bkz: <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">kısıtlamak erişim toocontainers ve blobları</a>.
  > 
  > 
* **Tooa küme bağlı olmayan depolama hesaplarındaki özel kapsayıcılar:** hello WebHCat işleri gönderdiğinizde hello depolama hesabını tanımlamadığınız sürece Merhaba kapsayıcılara hello blobları erişemiyor. Bu, bu makalenin sonraki bölümlerinde açıklanmıştır.

Merhaba oluşturma işlemi ve bunların anahtarların tanımlanan hello depolama hesapları %HADOOP_HOME%/conf/core-site.xml hello küme düğümlerinde depolanır. Hdınsight Hello varsayılan davranışı hello core-site.xml dosyasında tanımlanan toouse hello depolama hesapları değildir. [Ambari](./hdinsight-hadoop-manage-ambari.md) kullanarak bu ayarı değiştirebilirsiniz.

Hive, MapReduce, Hadoop akış ve Pig dahil olmak üzere birden çok WebHCat işleri kendileriyle birlikte depolama hesapları açıklaması ve meta veriler taşıyabilir. (Bu şu anda yalnızca Pig depolama hesapları ile çalışmakta, ancak meta verilerle çalışmamaktadır.) Daha fazla bilgi için bkz. [Alternatif Depolama Hesapları ve Meta Depolarla HDInsight Kümesi kullanma](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).

Bloblar yapılandırılmış ve yapılandırılmamış veriler için kullanılabilir. Blob kapsayıcıları, verileri anahtar/değer çiftleri olarak depolar ve dizin hiyerarşisi bulunmaz. Ancak, Hello eğik çizgi karakteri (/) görünür bir dosyayı dizin yapısında depolanmış gibi hello anahtar adı toomake içinde kullanılabilir. Örneğin, bir blob'un anahtarı *input/log1.txt* şeklinde olabilir. Gerçek *giriş* dizin var, ancak hello hello anahtar adında eğik çizgi karakteri varlığını toohello, bir dosya yolu hello görünümünü sahiptir.

## <a id="benefits"></a>Azure Depolamanın yararları
performans maliyetini birlikte bulunduruyorsanız hesaplama kümeleri ve depolama kaynaklarını hello hesaplama kümeleri Kapat toohello depolama hesabı kaynaklarına hello Azure bölgesi, burada hello yüksek hızlı ağ kolaylaştırır oluşturulan hello yolu tarafından azaltılan Hello kapsanan Merhaba işlem düğümleri için etkili verileri Azure depolama içinde tooaccess hello.

HDFS yerine Azure depolama alanında hello veri depolamanın çeşitli avantajları vardır:

* **Verileri yeniden kullanma ve paylaşma:** HDFS hello verilerde hello işlem kümesi içinde bulunur. Erişim toohello yalnızca hello uygulamaları hesaplamak için küme hello verileri HDFS API'lerini kullanarak kullanabilirsiniz. Azure depolama alanında Hello veriler erişilebilir hello HDFS API'lerini veya hello aracılığıyla [Blob Storage REST API'leri][blob-storage-restAPI]. Bu nedenle, daha büyük bir uygulamaları (diğer Hdınsight kümeleri dahil olmak üzere) ve araçları kullanılan tooproduce olması ve hello verileri kullanmak.
* **Veri arşivleme:** verileri Azure depolama alanında depolamak hello Hdınsight kümelerini kullanıcı verilerini kaybetmeden güvenle silinmiş hesaplama toobe için kullanılan sağlar.
* **Veri depolama maliyeti:** hello uzun vadeli bir işlem kümesi hello maliyeti Azure depolama hello Maliyet değerinden yüksek olduğundan hello veri Azure storage'da depolamaktan daha maliyetlidir; DFS veri depolama. Ek olarak, Hello veri her işlem kümesi oluşturmada yeniden toobe sahip olmadığından veri yükleme maliyetlerinden de tasarruf edersiniz.
* **Esnek ölçeklendirme:** hdfs size ölçeklendirilmiş dosya sistemi ile hello ölçek, kümeniz için oluşturduğunuz düğüm hello sayısı tarafından belirlenir. Merhaba ölçeğin değiştirilmesi hello esnek ölçeklendirme Azure depolama alanında otomatik olarak Al özelliklere bağlı olan daha daha karmaşık bir işlem haline gelebilir.
* **Coğrafi çoğaltma:** Azure depolamanız coğrafi olarak çoğaltılabilir. Bu size coğrafi kurtarma ve veri yedekliği sağlamakla birlikte, coğrafi olarak çoğaltılmış bir yük devretme toohello konum performansınızı ciddi bir şekilde etkiler ve ek ücrete neden olabilir. Bizim önerimiz toochoose hello coğrafi çoğaltma akıllıca gelir ve yalnızca hello verilerin hello değerini hello ek maliyetlere ise.

Bazı MapReduce işleri ve paketleri Azure depolama alanında toostore gerçekten istemediğiniz Ara sonuçlar oluşturabilir. Talebi toostore hello verilerde seçebilirler, yerel HDFS hello. Aslında, HDInsight Hive işleri ve diğer işlemlerdeki bu ara sonuçların bazıları için DFS kullanır.

> [!NOTE]
> Çoğu HDFS komutu (örneğin, <b>ls</b>, <b>copyFromLocal</b> ve <b>mkdir</b>) hala beklendiği gibi çalışmaktadır. (Başvurulan tooas DFS olan) belirli toohello yerel HDFS uygulamasına, gibi komutları yalnızca hello <b>fschk</b> ve <b>dfsadmin</b>, Azure depolama alanında farklı bir davranış gösterebilir.
> 
> 

## <a name="create-blob-containers"></a>Blob kapsayıcıları oluşturma
toouse BLOB'ları önce oluşturduğunuz bir [Azure depolama hesabı][azure-storage-create]. Bunun bir parçası olarak hello depolama hesabının oluşturulduğu bir Azure bölgesi belirtin. Merhaba küme ve hello depolama hesabı hello barındırılmalıdır aynı bölgede. Merhaba Hive meta depo SQL Server veritabanı ve Oozie meta depo SQL Server veritabanı içinde de bulunmalıdır aynı bölgede hello.

Nerede olursa olsun, oluşturduğunuz her blob Azure Storage hesabınızı tooa kapsayıcısında aittir. Bu kapsayıcı HDInsight dışında oluşturulmuş bir blob veya bir HDInsight kümesi için oluşturulan bir kapsayıcı olabilir.

Merhaba varsayılan Blob kapsayıcısı iş geçmişi ve günlükleri gibi kümeye özel bilgileri depolar. Varsayılan Blob kapsayıcısını birden çok HDInsight kümesiyle paylaşmayın. Bu durum iş geçmişinin bozulmasına neden olabilir. Her biri için farklı bir kapsayıcı küme ve paylaşılan veri hello varsayılan depolama hesabı yerine tüm ilgili kümelerin dağıtımında belirtilen bağlantılı depolama hesabına yerleştirmek toouse önerilir. Bağlantılı Depolama hesaplarını yapılandırma hakkında daha fazla bilgi için bkz: [HDInsight kümeleri oluşturma][hdinsight-creation]. Ancak Hello özgün Hdınsight kümesi silindikten sonra varsayılan depolama kapsayıcısını yeniden kullanabilirsiniz. HBase kümeleri için aslında hello HBase tablo şemasını ve verileri silinmiş bir HBase kümesi tarafından kullanılan hello varsayılan blob kapsayıcısını kullanarak yeni bir HBase kümesi oluşturarak tutabilirsiniz.

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-hello-azure-portal"></a>Hello Azure portalını kullanın
Hello Portalı ' bir Hdınsight kümesi oluştururken, hello (aşağıda gösterildiği gibi) seçenekleri tooprovide hello depolama hesabı ayrıntıları sahip. Bir ek depolama alanı hesabı hello kümesi ile ilişkili ve bu durumda, Data Lake Store hello ek depolama alanı olarak başka bir Azure Storage blobu seçin veya isteyip istemediğinizi de belirtebilirsiniz.

![HDInsight hadoop oluşturma veri kaynağı](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> Merhaba Hdınsight kümesi farklı bir konumda bir ek depolama alanı hesabı kullanarak desteklenmiyor.


### <a name="use-azure-powershell"></a>Azure PowerShell kullanma
Varsa, [Azure PowerShell'i yükleyip][powershell-install], bir depolama hesabı ve kapsayıcı hello Azure PowerShell komut istemi toocreate aşağıdaki hello kullanabilirsiniz:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $SubscriptionID = "<Your Azure Subscription ID>"
    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"

    $StorageAccountName = "<New Azure Storage Account Name>"
    $containerName = "<New Azure Blob Container Name>"

    Add-AzureRmAccount
    Select-AzureRmSubscription -SubscriptionId $SubscriptionID

    # Create resource group
    New-AzureRmResourceGroup -name $ResourceGroupName -Location $Location

    # Create default storage account
    New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS 

    # Create default blob containers
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -StorageAccountName $StorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer -Name $containerName -Context $destContext

### <a name="use-azure-cli"></a>Azure CLI kullanma

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

Varsa [hello Azure CLI yükleyip](../cli-install-nodejs.md), hello şu komutu kullanılan tooa depolama hesabı ve kapsayıcı olabilir.

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> Merhaba `--type` parametresi hello depolama hesabı nasıl yinelendiğini gösterir. Daha fazla bilgi için bkz. [Azure Storage çoğaltma](../storage/storage-redundancy.md). ZRS, sayfa blobu, dosya, tablo veya kuyruğu desteklemediğinden, ZRS kullanmayın.
> 
> 

Merhaba depolama hesabı oluşturulur istendiğinde toospecify hello coğrafi bölge var. Hello hello depolama hesabı oluşturmanız gerekir Hdınsight kümenizi oluşturmayı planladığınızla aynı bölgede.

Merhaba depolama hesabı oluşturulduktan sonra komutu tooretrieve hello depolama hesabı anahtarlarını aşağıdaki hello kullan:

    azure storage account keys list <storageaccountname>

toocreate bir kapsayıcı hello aşağıdaki komutu kullanın:

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a>Azure depolamada dosyaları adresleme
Hdınsight'ta Azure depolama alanında dosyalara erişmek için hello URI düzeni şöyledir:

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

Merhaba URI şeması şifrelenmemiş erişim sağlar (Merhaba ile *wasb:* önek) ve SSL şifreli erişim (ile *wasbs*). Kullanmanızı öneririz *wasbs* mümkün olduğunda, içinde bulunduğu erişilirken verileri azure'da aynı bölgede bile hello olduğunda.

Merhaba &lt;BlobStorageContainerName&gt; Azure depolama hello blob kapsayıcısında hello adını tanımlar.
Merhaba &lt;StorageAccountName&gt; hello Azure depolama hesabı adını tanımlar. Tam uygun etki alanı adı (FQDN) gereklidir.

Ne &lt;BlobStorageContainerName&gt; ya da &lt;StorageAccountName&gt; belirtildiyse, hello varsayılan dosya sistemi kullanılır. Merhaba varsayılan dosya sistemindeki Hello dosyaları için göreli bir yol veya mutlak bir yol kullanabilirsiniz. Örneğin, hello *hadoop mapreduce examples.jar* Hdınsight kümeleriyle gelen dosya hello aşağıdakilerden birini kullanarak başvurulan tooby olabilir:

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> Merhaba dosya adı <i>hadoop examples.jar</i> Hdınsight sürüm 2.1 ve 1.6 kümelerinde.
> 
> 

Merhaba &lt;yolu&gt; hello dosya veya dizin HDFS yol adıdır. Azure depolamadaki kapsayıcılar anahtar-değer depoları olduğundan, doğru hiyerarşik dosya sistemi yoktur. Bir blob anahtarındaki bir eğik çizgi karakteri (/) dizin ayırıcı olarak yorumlanır. Örneğin, hello blob adı *hadoop mapreduce examples.jar* değil:

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> Hdınsight dışındaki BLOB'lar ile çalışırken, yardımcı programların çoğu değil hello WASB biçimini tanımaz ve bunun yerine bir temel yol biçimi gibi bekler `example/jars/hadoop-mapreduce-examples.jar`.
> 
> 

## <a name="access-blobs"></a>Bloblara erişme 


### <a name="access-blobs-using-azure-powershell"></a> Azure PowerShell'i kullanma
> [!NOTE]
> Bu bölümdeki Hello komutlar blob'larda depolanan PowerShell tooaccess verileri kullanarak, temel bir örnek sağlar. Hdınsight ile çalışmak için özelleştirilmiş daha tam özellikli bir örneğin hello bkz [Hdınsight Araçları](https://github.com/Blackmist/hdinsight-tools).
> 
> 

Komut toolist hello blob ile ilgili cmdlet'leri aşağıdaki hello kullan:

    Get-Command *blob*

![Blob’la ilgili PowerShell cmdlet’lerinin listesi.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a>Dosyaları karşıya yükleme
Bkz: [karşıya veri tooHDInsight][hdinsight-upload-data].

#### <a name="download-files"></a>Dosyaları indirme
Merhaba aşağıdaki komut dosyasını bir blok blobu toohello geçerli klasöre indirir. Önce çalışan hello betik, yazma izinlerine sahip olduğu hello dizin tooa klasörü değiştirin.

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # hello storage account used for hello default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # hello default file system container has hello same name as hello cluster.
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    # Use Add-AzureAccount if you haven't connected tooyour Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List hello downloaded file ..." -ForegroundColor Green
    cat "./$blob"

Merhaba kaynak grubu adı ve hello küme adını vererek, hello aşağıdaki kodu kullanabilirsiniz:

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a>Dosyaları silme
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a>Dosyaları listeleme
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a>Tanımlanmamış depolama hesabı kullanarak Hive sorgularını çalıştırma
Bu örnek nasıl toolist sırasında tanımlanmamış depolama hesabındaki bir klasör hello oluşturma işlemi gösterir.
$clusterName = "<HDInsightClusterName>"

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a>Azure CLI kullanma
Komut toolist hello blob ile ilgili komutları aşağıdaki hello kullan:

    azure storage blob

**Azure CLI tooupload bir dosya kullanma örneği**

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**Azure CLI toodownload bir dosya kullanma örneği**

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

**Azure CLI toodelete bir dosya kullanma örneği**

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**Azure CLI toolist dosyaları kullanma örneği**

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a>Ek depolama hesaplarını kullanma

Hdınsight kümesi oluştururken, onunla tooassociate istediğiniz hello Azure depolama hesabı belirtin. Ayrıca toothis depolama hesabı, ek depolama hesapları hello aynı ekleyebileceğiniz Azure aboneliği veya farklı Azure abonelikleri hello oluşturma işlemi sırasında veya bir küme oluşturulduktan sonra. Ek depolama hesapları ekleme hakkında yönergeler için bkz. [HDInsight kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).

> [!WARNING]
> Merhaba Hdınsight kümesi farklı bir konumda bir ek depolama alanı hesabı kullanarak desteklenmiyor.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, nasıl öğrenilen toouse HDFS uyumlu Azure storage Hdınsight ile. Bu, toobuild ölçeklenebilir, uzun vadeli, arşivleme verileri edinme çözümleri ve kullanım depolanan hello içindeki Hdınsight toounlock hello bilgileri yapılandırılmış ve yapılandırılmamış verileri sağlar.

Daha fazla bilgi için bkz.

* [Azure HDInsight'ı Kullanmaya Başlama][hdinsight-get-started]
* [Azure Data Lake Store ile çalışmaya başlama](../data-lake-store/data-lake-store-get-started-portal.md)
* [Veri tooHDInsight karşıya yükle][hdinsight-upload-data]
* [HDInsight ile Hive kullanma][hdinsight-use-hive]
* [HDInsight ile Pig kullanma][hdinsight-use-pig]
* [Hdınsight ile Azure Storage paylaşılan erişim imzaları toorestrict erişim toodata kullanma][hdinsight-use-sas]

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
