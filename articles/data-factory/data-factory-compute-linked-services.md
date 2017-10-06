---
title: "Azure Data Factory ile desteklenen aaaCompute ortamları | Microsoft Docs"
description: "Azure Data Factory işlem hatlarını (örneğin, Azure Hdınsight) tootransform veya işlem verilerde kullanabilirsiniz bilgi işlem ortamları hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6877a7e8-1a58-4cfb-bbd3-252ac72e4145
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 07/25/2017
ms.author: shlo
ms.openlocfilehash: aba7d7de695bc1c7d475f1e741ee3b3e884151c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="compute-environments-supported-by-azure-data-factory"></a>Azure Data Factory ile desteklenen ortamlar işlem
Bu makalede tooprocess kullanın veya veri dönüştürme farklı işlem ortamları açıklanmaktadır. Ayrıca, farklı yapılandırmaları (isteğe bağlı karşılaştırması Getir kendi) Bu işlem ortamları tooan Azure veri fabrikası bağlama bağlı hizmetler yapılandırırken Data Factory ile desteklenen ayrıntılarını sağlar.

Merhaba aşağıdaki tabloda bilgi işlem ortamları üzerlerinde çalıştırabilirsiniz Data Factory ve hello etkinlikler tarafından desteklenen bir listesini sağlar. 

| İşlem ortamı | Etkinlikler |
| --- | --- |
| [İsteğe bağlı Hdınsight kümesi](#azure-hdinsight-on-demand-linked-service) veya [kendi Hdınsight kümenizi](#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop akış](data-factory-hadoop-streaming-activity.md) |
| [Azure toplu işlem](#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| [Azure Machine Learning](#azure-machine-learning-linked-service) |[Machine Learning etkinlikleri: Toplu Yürütme ve Kaynak Güncelleştirme](data-factory-azure-ml-batch-execution-activity.md) |
| [Azure Data Lake Analytics](#azure-data-lake-analytics-linked-service) |[Data Lake Analytics U-SQL](data-factory-usql-activity.md) |
| [Azure SQL](#azure-sql-linked-service), [Azure SQL veri ambarı](#azure-sql-data-warehouse-linked-service), [SQL Server](#sql-server-linked-service) |[Saklı Yordam](data-factory-stored-proc-activity.md) |

## <a name="supported-hdinsight-versions-in-azure-data-factory"></a>Azure veri fabrikası'nda desteklenen Hdınsight sürümleri
Azure Hdınsight herhangi bir zamanda dağıtılabilir birden çok Hadoop küme sürümlerindeki destekler. Her sürüm seçimi hello Hortonworks veri Platformu (HDP) dağıtım belirli bir sürümü ve o dağıtım içinde bulunan bileşenleri kümesi oluşturur. Microsoft Hdınsight tooprovide son Hadoop ekosistemi bileşenlerini ve düzeltmeleri Desteklenen sürümlerin listesi hello güncelleştiriliyor tutar. Merhaba Hdınsight 3.2 1 Nisan 2017 kullanım dışıdır. Ayrıntılı bilgi için bkz: [desteklenen Hdınsight sürümleri](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).

Bu etkinlikler karşı Hdınsight 3.2 kümeleri çalıştıran var olan Azure Data Factory etkiler. Etkilenen veri fabrikaları bölüm tooupdate aşağıdaki hello kullanıcılar toofollow hello yönergeleri hello öneririz:

### <a name="for-linked-services-pointing-tooyour-own-hdinsight-clusters"></a>Bağlı hizmetler için tooyour kendi Hdınsight kümeleri işaret eden
* **Hdınsight bağlı tooyour işaret eden hizmetler Hdınsight 3.2 veya kümeleri aşağıda sahibi:**

  Azure Data Factory destekleyen kendi Hdınsight kümeleri HDI 3.1 çok gönderiliyor işleri tooyour[en son desteklenen hello Hdınsight sürüm](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions). Ancak, 1 Nisan 2017 kısmında belgelenen hello kullanımdan ilkesini temel alarak sonra Hdınsight 3.2 kümesi artık oluşturabilirsiniz [desteklenen Hdınsight sürümleri](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).  

  **Öneriler:** 
  * Testleri tooensure hello uyumluluğunu hello bu bağlı hizmetler çok başvuru etkinlikleri gerçekleştirmek[en son desteklenen hello Hdınsight sürüm](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) kısmında belgelenen bilgilerle [Hadoop bileşenleri ile kullanılabilir farklı Hdınsight sürümleri](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) ve [Hortonworks sürüm notları Hdınsight sürümleri ile ilişkili](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).
  * Hdınsight 3.2 kümenizi çok yükseltme[en son desteklenen hello Hdınsight sürüm](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello en son Hadoop ekosistemi bileşenlerini ve düzeltmeler. 

* **Hdınsight bağlı tooyour işaret eden hizmetler 3.3 veya kümeleri üzerinde Hdınsight sahibi:**

  Azure Data Factory destekleyen kendi Hdınsight kümeleri HDI 3.1 çok gönderiliyor işleri tooyour[en son desteklenen hello Hdınsight sürüm](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions). 
  
  **Öneriler:** 
  * Herhangi bir işlem, veri fabrikası açısından gereklidir. Hdınsight daha düşük bir sürümü varsa, ancak hala çok yükseltme öneririz[en son desteklenen hello Hdınsight sürüm](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello en son Hadoop ekosistemi bileşenlerini ve düzeltmeler.

### <a name="for-hdinsight-on-demand-linked-services"></a>Hizmetleri için isteğe bağlı Hdınsight bağlı
* **Sürüm 3.2 veya Hdınsight isteğe bağlı Hizmetleri JSON tanımında aşağıda belirtilmiştir:**
  
  Azure Data Factory sürüm 3.3 veya'dan daha fazla isteğe bağlı Hdınsight kümeleri oluşturulmasını destekler **15/05/2017** veya sonraki sürümleri. Ve, var olan isteğe bağlı Hdınsight bağlı hizmetler çok genişletilmiş 3.2 için destek sonuna hello**15/07/2017**.  

  **Öneriler:** 
  * Testleri tooensure hello uyumluluğunu hello bu bağlı hizmetler çok başvuru etkinlikleri gerçekleştirmek [en son desteklenen hello Hdınsight sürüm](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) kısmında belgelenen bilgilerle [Hadoop bileşenleri ile kullanılabilir farklı Hdınsight sürümleri](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) ve [Hortonworks sürüm notları Hdınsight sürümleri ile ilişkili](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).
  * Önce **15/07/2017**, isteğe bağlı HDI bağlantılı hizmet JSON tanımında hello Version özelliği çok güncelleştirme[en son desteklenen hello Hdınsight sürüm](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello son Hadoop ekosistemi bileşenlerini ve giderir. Ayrıntılı JSON tanımını toohello başvuran [Azure Hdınsight isteğe bağlı hizmeti örnek](#azure-hdinsight-on-demand-linked-service). 

* **İsteğe bağlı Hdınsight bağlı Hizmetleri belirtilmemiş sürümü:**
  
  Azure Data Factory sürüm 3.3 veya'dan daha fazla isteğe bağlı Hdınsight kümeleri oluşturulmasını destekler **15/05/2017** veya sonraki sürümleri. Ve Destek tooexisting isteğe bağlı Hdınsight bağlı 3.2 Hizmetleri hello sonuna çok Genişletilmiş**15/07/2017**. 

  Önce **15/07/2017**, boş bırakılırsa, sürüm hello varsayılan değerler ve osType özellikleri şunlardır: 

  | Özellik | Varsayılan değer | Gerekli |
  | --- | --- | --- |
  Sürüm   | Windows kümesi ve HDI 3.2 Linux kümesi için HDI 3.1.| Hayır
  osType | Windows Hello varsayılandır | Hayır

  Sonra **15/07/2017**, boş bırakılırsa, sürüm hello varsayılan değerler ve osType özellikleri şunlardır:

  | Özellik | Varsayılan değer | Gerekli |
  | --- | --- | --- |
  Sürüm   | Windows kümesi ve Linux kümesi için 3.5 HDI 3.3.    | Hayır
  osType | Linux Hello varsayılandır   | Hayır

  **Öneriler:** 
  * Önce **15/07/2017**, testleri tooensure hello uyumluluğunu hello bu bağlı hizmetler çok başvuru etkinlikleri gerçekleştirmek[en son desteklenen hello Hdınsight sürüm](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) belgelenmiş ile içinde [Hadoop bileşenleri farklı Hdınsight sürümleriyle kullanılabilir](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) ve [Hortonworks sürüm notları Hdınsight sürümleri ile ilişkili](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).  
  * Sonra **15/07/2017**, açıkça belirttiğiniz osType ve sürüm değerlerini toooverride hello varsayılan ayarlar isterseniz emin olun. 

>[!Note]
>Şu anda Azure Data Factory birincil deposu olarak Azure Data Lake Store kullanarak Hdınsight kümelerini desteklemiyor. Azure Storage Hdınsight kümeleri için birincil depolama alanı olarak kullanın. 
>  
>  

## <a name="on-demand-compute-environment"></a>İsteğe bağlı bilgi işlem ortamı
Bu tür yapılandırma hello bilgi işlem ortamı tam olarak hello Azure Data Factory hizmeti tarafından yönetilir. Bu otomatik olarak bir iş gönderilen tooprocess veri önce hello Data Factory hizmeti tarafından oluşturulan ve hello iş tamamlandığında kaldırıldı. Hello isteğe bağlı bilgi işlem ortamı için bağlı hizmet oluşturma yapılandırın ve iş yürütme, küme yönetimi ve eylemler önyükleme için ayrıntılı ayarları denetler.

> [!NOTE]
> Merhaba isteğe bağlı yapılandırma şu anda yalnızca Azure Hdınsight kümeleri için desteklenir.
> 
> 

## <a name="azure-hdinsight-on-demand-linked-service"></a>Azure Hdınsight isteğe bağlı
Hello Azure Data Factory hizmetine otomatik olarak bir Windows/Linux tabanlı isteğe bağlı Hdınsight küme tooprocess veriler oluşturabilir. Merhaba küme hello depolama hesabı (Merhaba JSON özelliğinde linkedServiceName) ile aynı bölgeye hello kümesi ile ilişkili hello oluşturulur. Merhaba depolama hesabı, genel amaçlı standart Azure depolama hesabınızın olması gerekir. 

Not hello aşağıdaki **önemli** noktaları hakkında isteğe bağlı Hdınsight bağlı hizmeti:

* Merhaba isteğe bağlı görüyor musunuz Azure aboneliğinizde oluşturduğunuz Hdınsight kümesi. Hello Azure Data Factory hizmetine hello isteğe bağlı Hdınsight kümesi sizin adınıza yönetir.
* Hello günlükleri küme bir isteğe bağlı Hdınsight üzerinde çalıştırılan işler hello Hdınsight kümesi ile ilişkili toohello depolama hesabı kopyalanır. Bu günlükler hello hello Azure portalında erişebileceğiniz **etkinlik çalışma ayrıntıları** dikey. Bkz: [izleme ve yönetme ardışık düzen](data-factory-monitor-manage-pipelines.md) Ayrıntılar için makale.
* Yalnızca hello zaman hello Hdınsight kümesi yukarı olduğunda ve çalışan işleri için sizden ücret kesilir.

> [!IMPORTANT]
> Genellikle sürer **20 dakika** veya daha fazla tooprovision Azure Hdınsight küme isteğe bağlı.
> 
> 

### <a name="example"></a>Örnek
JSON aşağıdaki hello Linux tabanlı isteğe bağlı Hdınsight bağlı hizmeti tanımlar. Merhaba Data Factory hizmetinin otomatik olarak oluşturur bir **Linux tabanlı** veri dilimi işlerken Hdınsight kümesi. 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

bir Windows tabanlı Hdınsight kümesi toouse ayarlamak **osType** çok**windows** veya hello varsayılan değer olarak hello özelliği kullanmayın: windows.  

> [!IMPORTANT]
> Merhaba Hdınsight kümesi oluşturur bir **varsayılan kapsayıcı** hello JSON belirtilen hello blob depolamada (**linkedServiceName**). Hdınsight Hello küme silindiğinde bu kapsayıcıyı silmez. Bu davranış tasarım gereğidir. Mevcut canlı bir küme olmadıkça işlenen toobe bir dilim gerekir her zaman isteğe bağlı Hdınsight bağlı hizmetiyle, Hdınsight kümesi oluşturulur (**timeToLive**) ve hello işlem bittiğinde silinir. 
> 
> Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz. Bunları hello işlerin sorunları giderilmesi için ihtiyacınız yoksa, toodelete isteyebilirsiniz bunları tooreduce hello depolama maliyeti. Bu kapsayıcıların Hello adları izleyen bir desen: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`. Gibi araçlar kullanın [Microsoft Storage Gezgini](http://storageexplorer.com/) toodelete kapsayıcılarında Azure blob depolama.
> 
> 

### <a name="properties"></a>Özellikler
| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği çok ayarlanmalıdır**HDInsightOnDemand**. |Evet |
| ClusterSize |Merhaba kümede çalışan/veri düğüm sayısı. Merhaba Hdınsight kümesi hello için bu özelliği belirtmeniz çalışan düğüm sayısı ile birlikte 2 baş düğümler ile oluşturulur. Merhaba düğümleri olan 24 çekirdek 4 çalışan düğümlü bir küme alır, böylece 4 çekirdeğe sahip Standard_D3 boyutunu (4\*4 = 16 çekirdek çalışan düğümleri artı 2\*4 = 8 çekirdek baş düğümler için). Bkz: [Hdınsight oluşturma Linux tabanlı Hadoop kümeleri](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) hello Standard_D3 katmanı hakkında ayrıntılı bilgi için. |Evet |
| TimeToLive |Merhaba boşta kalma süresi hello isteğe bağlı Hdınsight kümesi için izin verilen. Ne kadar süreyle hello isteğe bağlı Hdınsight kümesi hello kümedeki diğer etkin iş yok varsa bir etkinlik tamamlandıktan sonra canlı kalır belirtir.<br/><br/>Bir etkinlik 6 dakika ve timetolive sürerse Örneğin, too5 dakika, 5 dakika sonra hello için Canlı hello küme kalır hello etkinlik işleme 6 dakika ayarlandı. Başka bir etkinlik hello 6 dakika penceresiyle yürütülürse, hello tarafından işlenir aynı küme.<br/><br/>İsteğe bağlı Hdınsight kümesi oluşturma (biraz sürebilir), pahalı bir işlem olduğundan bu ayar isteğe bağlı Hdınsight kümesi yeniden kullanarak bir veri fabrikası gerekli tooimprove performansını kullanın.<br/><br/>Timetolive değeri too0 ayarlarsanız, hello küme hello etkinlik tamamlandıktan hemen sonra silindi. Yüksek bir değer ayarlarsanız, hello küme gereksiz yere yüksek maliyetlerini kaynaklanan boşta kalmasını ancak. Bu nedenle, gereksinimlerinize göre hello uygun değere ayarlamak önemlidir.<br/><br/>Merhaba timetolive özellik değerini uygun şekilde ayarlarsanız, birden çok ardışık düzen hello isteğe bağlı Hdınsight kümesi hello örneğini paylaşabilirsiniz.  |Evet |
| Sürüm |Merhaba Hdınsight küme sürümü. Merhaba varsayılan 3.1 Windows kümesi için ve Linux kümesi için 3.2 değerdir. |Hayır |
| linkedServiceName | Azure depolama bağlı hizmeti toobe depolamak ve veri işleme için Hello isteğe bağlı küme tarafından kullanılan. Merhaba Hdınsight kümesi hello aynı oluşturulan bu Azure depolama hesabı bölgeye.<p>Şu anda bir Azure Data Lake Store hello depolama alanı olarak kullanan bir isteğe bağlı Hdınsight kümesi oluşturulamıyor. Bir Azure Data Lake Store'da işleme Hdınsight toostore hello sonuç verileri istiyorsanız hello Azure Blob Storage toohello Azure Data Lake Store kopyalama etkinliği toocopy hello verilerden kullanın. </p>  | Evet |
| additionalLinkedServiceNames |Böylece Hello Data Factory hizmetinin bunları sizin adınıza kaydedebilirsiniz hello Hdınsight için ek depolama hesapları hizmeti bağlı belirtir. Bu depolama hesaplarından hello olmalıdır hello aynı oluşturulur hello Hdınsight kümesi ile aynı bölgeye linkedServiceName tarafından belirtilen hello depolama hesabı bölgeye. |Hayır |
| osType |İşletim sistemi türü. İzin verilen değerler: (varsayılan) Windows ve Linux |Hayır |
| hcatalogLinkedServiceName |Azure SQL bağlı Hello adını noktası toohello HCatalog veritabanı hizmeti. Merhaba isteğe bağlı Hdınsight kümesi hello meta depo hello Azure SQL veritabanı kullanılarak oluşturulur. |Hayır |

#### <a name="additionallinkedservicenames-json-example"></a>additionalLinkedServiceNames JSON örneği

```json
"additionalLinkedServiceNames": [
    "otherLinkedServiceName1",
    "otherLinkedServiceName2"
  ]
```

### <a name="advanced-properties"></a>Gelişmiş Özellikler
Merhaba ayrıntılı yapılandırma hello isteğe bağlı Hdınsight kümesinin özelliklerini aşağıdaki hello de belirtebilirsiniz.

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| coreConfiguration |Merhaba çekirdek yapılandırma parametreleri (olduğu gibi core-site.xml) için hello Hdınsight küme toobe oluşturulan belirtir. |Hayır |
| hBaseConfiguration |Merhaba Hdınsight kümesi için Hello HBase yapılandırma parametreleri (hbase-site.xml) belirtir. |Hayır |
| hdfsConfiguration |Merhaba Hdınsight kümesi için Hello HDFS yapılandırma parametreleri (hdfs-site.xml) belirtir. |Hayır |
| hiveConfiguration |Merhaba Hdınsight kümesi için Hello hive yapılandırma parametreleri (hive-site.xml) belirtir. |Hayır |
| mapReduceConfiguration |Merhaba Hdınsight kümesi için Hello MapReduce yapılandırma parametreleri (mapred-site.xml) belirtir. |Hayır |
| oozieConfiguration |Merhaba Hdınsight kümesi için Hello Oozie yapılandırma parametreleri (oozie-site.xml) belirtir. |Hayır |
| stormConfiguration |Merhaba Hdınsight kümesi için Hello Storm yapılandırma parametreleri (storm-site.xml) belirtir. |Hayır |
| yarnConfiguration |Merhaba Hdınsight kümesi için Hello Yarn yapılandırma parametreleri (yarn-site.xml) belirtir. |Hayır |

#### <a name="example--on-demand-hdinsight-cluster-configuration-with-advanced-properties"></a>Örnek – Gelişmiş özellikleri ile isteğe bağlı Hdınsight küme yapılandırması

```json
{
  "name": " HDInsightOnDemandLinkedService",
  "properties": {
    "type": "HDInsightOnDemand",
    "typeProperties": {
      "clusterSize": 16,
      "timeToLive": "01:30:00",
      "linkedServiceName": "adfods1",
      "coreConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "hiveConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "mapReduceConfiguration": {
        "mapreduce.reduce.java.opts": "-Xmx4000m",
        "mapreduce.map.java.opts": "-Xmx4000m",
        "mapreduce.map.memory.mb": "5000",
        "mapreduce.reduce.memory.mb": "5000",
        "mapreduce.job.reduce.slowstart.completedmaps": "0.8"
      },
      "yarnConfiguration": {
        "yarn.app.mapreduce.am.resource.mb": "5000",
        "mapreduce.map.memory.mb": "5000"
      },
      "additionalLinkedServiceNames": [
        "datafeeds",
        "adobedatafeed"
      ]
    }
  }
}
```

### <a name="node-sizes"></a>Düğümü boyutları
Aşağıdaki özelliklere hello kullanarak head, veri ve zookeeper düğümleri hello boyutlarını belirtebilirsiniz: 

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| headNodeSize |Merhaba baş düğüm Hello boyutunu belirtir. Merhaba varsayılan değer: Standard_D3. Merhaba bkz **düğümü boyutları belirtme** ayrıntıları bölümü. |Hayır |
| dataNodeSize |Merhaba veri düğümü Hello boyutunu belirtir. Merhaba varsayılan değer: Standard_D3. |Hayır |
| zookeeperNodeSize |Merhaba Zoo Keeper düğümü Hello boyutunu belirtir. Merhaba varsayılan değer: Standard_D3. |Hayır |

#### <a name="specifying-node-sizes"></a>Düğümü boyutları belirtme
Merhaba bkz [sanal makine boyutları](../virtual-machines/linux/sizes.md) makale için gereksinim duyduğunuz toospecify hello özellikleri hello önceki bölümünde belirtildiği için dize değeri. Merhaba değerlerine gereksinim tooconform toohello **cmdlet'leri & API'leri** hello makalesinde başvurulan. Merhaba makalesinde görebilirsiniz gibi hello veri düğümü (varsayılan) büyük boyutta senaryonuz için yeterince iyi olmayabilir 7 GB bellek vardır. 

Toocreate D4 boyutta baş düğümler ve çalışan düğümleri istiyorsanız belirtin **Standard_D4** headNodeSize ve dataNodeSize özellikleri hello değeri olarak. 

```json
"headNodeSize": "Standard_D4",    
"dataNodeSize": "Standard_D4",
```

Bu özellikler için yanlış bir değer belirtirseniz, hello aşağıdaki alabilirsiniz **hata:** başarısız toocreate küme. Özel durum: Oluşturulamıyor toocomplete hello küme oluşturma işlemi. İşlem '400' koduyla başarısız oldu. Küme geride bırakma durumu: 'Hata'. İleti: 'PreClusterCreationValidationFailure'. Bu hatayı aldığınızda hello kullandığınızdan emin olun **CMDLET & API'leri** hello hello tablosundan ad [sanal makine boyutları](../virtual-machines/linux/sizes.md) makalesi.  

## <a name="bring-your-own-compute-environment"></a>Kendi işlem ortamınızda Getir
Bu tür yapılandırma, kullanıcılar veri fabrikasında bağlı hizmet olarak zaten mevcut olan bir bilgi işlem ortamı kaydedin. Merhaba bilgi işlem ortamı hello kullanıcı tarafından yönetilir ve hello Data Factory hizmetinin tooexecute hello etkinliklerini kullanır.

Bu yapılandırma türü ortamları Hello aşağıdaki işlem için desteklenir:

* Azure Hdınsight
* Azure Batch
* Azure Machine Learning
* Azure Data Lake Analytics
* Azure SQL DB, Azure SQL DW, SQL Server

## <a name="azure-hdinsight-linked-service"></a>Azure Hdınsight bağlı hizmeti
Data Factory ile kendi Hdınsight kümenizi Azure Hdınsight bağlı hizmeti tooregister oluşturabilirsiniz.

### <a name="example"></a>Örnek

```json
{
  "name": "HDInsightLinkedService",
  "properties": {
    "type": "HDInsight",
    "typeProperties": {
      "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
      "userName": "admin",
      "password": "<password>",
      "linkedServiceName": "MyHDInsightStoragelinkedService"
    }
  }
}
```

### <a name="properties"></a>Özellikler
| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği çok ayarlanmalıdır**Hdınsight**. |Evet |
| clusterUri |Merhaba hello Hdınsight kümesinin URI. |Evet |
| kullanıcı adı |Tooconnect tooan olan bir Hdınsight kümesine kullanılan hello kullanıcı toobe Hello adı belirtin. |Evet |
| password |Merhaba kullanıcı hesabı için parola belirtin. |Evet |
| linkedServiceName | Hdınsight kümesi hello tarafından kullanılan hello toohello Azure blob depolama başvuruyor Azure Storage bağlı hizmeti adı. <p>Şu anda bu özellik için bir Azure Data Lake Store bağlı belirtemezsiniz. Merhaba Hdınsight kümesine erişim toohello Data Lake Store varsa, Hive/Pig komut dosyalarından hello Azure Data Lake Store verilerde erişebilir. </p>  |Evet |

## <a name="azure-batch-linked-service"></a>Azure toplu işlem hizmeti bağlı
Batch havuzundaki sanal makineler (VM'ler) tooa data Factory bağlantılı Azure Batch hizmeti tooregister oluşturabilirsiniz. .NET özel etkinlikler Azure Batch ya da Azure Hdınsight kullanarak çalıştırabilirsiniz.

Yeni tooAzure Batch hizmeti kullanıyorsanız aşağıdaki konularda bakın:

* [Azure Batch Temelleri](../batch/batch-technical-overview.md) hello Azure Batch hizmetinin genel bakış.
* [AzureBatchAccount yeni](https://msdn.microsoft.com/library/mt125880.aspx) cmdlet toocreate bir Azure Batch hesabı (veya) [Azure portal](../batch/batch-account-create-portal.md) toocreate hello Azure Batch hesabı Azure portal kullanarak. Bkz: [PowerShell kullanarak toomanage Azure toplu işlem hesabı](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) konu hello cmdlet'ini kullanarak hakkında ayrıntılı yönergeler için.
* [Yeni-AzureBatchPool](https://msdn.microsoft.com/library/mt125936.aspx) cmdlet toocreate bir Azure Batch havuzu.

### <a name="example"></a>Örnek

```json
{
  "name": "AzureBatchLinkedService",
  "properties": {
    "type": "AzureBatch",
    "typeProperties": {
      "accountName": "<Azure Batch account name>",
      "accessKey": "<Azure Batch account key>",
      "poolName": "<Azure Batch pool name>",
      "linkedServiceName": "<Specify associated storage linked service reference here>"
    }
  }
}
```

Append "**.\< bölge adı\>**"Merhaba için batch hesabınızın toohello ad **accountName** özelliği. Örnek:

```json
"accountName": "mybatchaccount.eastus"
```

Başka bir seçenek tooprovide hello batchUri endpoint hello örnek aşağıdaki gösterildiği gibi olur:

```json
"accountName": "adfteam",
"batchUri": "https://eastus.batch.azure.com",
```

### <a name="properties"></a>Özellikler
| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği çok ayarlanmalıdır**AzureBatch**. |Evet |
| accountName |Hello Azure Batch hesabı adı. |Evet |
| accessKey |Hello Azure Batch hesabı için erişim anahtarı. |Evet |
| poolName |Sanal makinelerin hello havuzunun adı. |Evet |
| linkedServiceName |Hello Azure Storage bağlı hizmeti Azure bağlı Batch hizmeti ile ilişkili adı. Bu bağlı hizmetin dosyaları hazırlama için kullanılan toorun hello etkinliği ve hello Etkinlik yürütme günlüklerini depolamak gerekli. |Evet |

## <a name="azure-machine-learning-linked-service"></a>Azure Machine Learning hizmeti bağlı
Bir Azure Machine Learning bağlantılı hizmet tooregister bir Machine Learning toplu Puanlama uç noktası tooa veri fabrikası oluşturun.

### <a name="example"></a>Örnek

```json
{
  "name": "AzureMLLinkedService",
  "properties": {
    "type": "AzureML",
    "typeProperties": {
      "mlEndpoint": "https://[batch scoring endpoint]/jobs",
      "apiKey": "<apikey>"
    }
  }
}
```

### <a name="properties"></a>Özellikler
| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| Tür |Merhaba type özelliği ayarlanmalıdır: **AzureML**. |Evet |
| mlEndpoint |Merhaba toplu işlem Puanlama URL'sini. |Evet |
| apikey ile yapılan |Merhaba, çalışma alanı modelinin API yayımladı. |Evet |

## <a name="azure-data-lake-analytics-linked-service"></a>Azure Data Lake Analytics hizmeti bağlı
Oluşturduğunuz bir **Azure Data Lake Analytics** bağlantılı hizmet toolink bir Azure Data Lake Analytics işlem hizmeti tooan Azure data factory. Merhaba Data Lake Analytics U-SQL etkinliği hello ardışık düzende toothis bağlantılı hizmeti anlamına gelmektedir. 

Merhaba aşağıdaki tabloda Merhaba açıklamalarına hello JSON tanımını kullanılan genel özellikleri sağlar. Daha fazla hizmet sorumlusu ve kullanıcı kimlik bilgileri doğrulaması arasında seçim yapabilirsiniz.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| **türü** |Merhaba type özelliği ayarlanmalıdır: **AzureDataLakeAnalytics**. |Evet |
| **accountName** |Azure Data Lake Analytics hesap adı. |Evet |
| **dataLakeAnalyticsUri** |Azure Data Lake Analytics URI. |Hayır |
| **Subscriptionıd** |Azure abonelik kimliği |Hayır (belirtilmezse, veri fabrikası kullanılan hello abonelik). |
| **resourceGroupName** |Azure kaynak grubu adı |Hayır (belirtilmezse, veri fabrikası kullanılan hello kaynak grubu). |

### <a name="service-principal-authentication-recommended"></a>(Önerilen) hizmet asıl kimlik doğrulaması
Kayıt, hello Azure Active Directory (Azure AD) ve grant uygulama varlık toouse hizmet asıl kimlik doğrulaması, tooData Lake Store erişin. Ayrıntılı adımlar için bkz: [hizmeti için kimlik doğrulama](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Kullandığınız değerler aşağıdaki hello Not toodefine hello bağlantılı hizmeti:
* Uygulama Kimliği
* Uygulama anahtarı 
* Kiracı Kimliği

Aşağıdaki özelliklere hello belirterek hizmet asıl kimlik doğrulamasını kullan:

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| **servicePrincipalId** | Merhaba uygulamanın istemci kimliği belirtin. | Evet |
| **servicePrincipalKey** | Merhaba uygulamanın anahtarını belirtin. | Evet |
| **Kiracı** | Uygulamanızın bulunduğu altında Hello Kiracı bilgileri (etki alanı adı veya Kiracı kimliği) belirtin. Vurgulama hello fare hello sağ üst köşesindeki hello Azure portal tarafından alabilir. | Evet |

**Örnek: Hizmet asıl kimlik doğrulaması**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Kullanıcı kimlik bilgileri doğrulaması
Alternatif olarak, aşağıdaki özelliklere hello belirterek Data Lake Analytics için kullanıcı kimlik bilgilerinin kullanabilirsiniz:

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| **Yetkilendirme** | Merhaba tıklatın **Authorize** hello Data Factory Düzenleyici'düğmesine tıklayın ve hello otomatik olarak oluşturulur yetkilendirme URL'si toothis özelliği atar kimlik bilgilerinizi girin. | Evet |
| **SessionID** | Merhaba OAuth yetkilendirme oturumundan OAuth oturum kimliği. Her oturum kimliği benzersiz olup yalnızca bir kez kullanılabilir. Merhaba Data Factory Düzenleyici kullandığınızda bu ayarı otomatik olarak oluşturulur. | Evet |

**Örnek: Kullanıcı kimlik bilgileri doğrulaması**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>Belirteç süre sonu
Merhaba oluşturulan hello kullanarak Yetkilendirme kodu **Authorize** düğmesi süre sonra süresi dolar. Farklı türlerdeki kullanıcı hesapları için hello bitiş zamanları için aşağıdaki tablonun hello bakın. Aşağıdaki hata iletisini hello görebilirsiniz zaman kimlik doğrulaması'nı hello **belirtecinin süresi dolmadan**: kimlik bilgisi işlemi hatası: invalid_grant - AADSTS70002: Kimlik doğrulanırken hata oluştu. AADSTS70008: hello erişim izninin süresi doldu veya iptal sağlanan. İzleme kimliği: d18629e8-af88-43c5-88e3-d8419eb1fca1 bağıntı kimliği: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 zaman damgası: 2015-12-15 21:09:31Z

| Kullanıcı türü | Kullanım süresi sonu |
|:--- |:--- |
| Azure Active Directory tarafından yönetilmeyen kullanıcı hesapları (@hotmail.com, @live.comvb..) |12 saat |
| Azure Active Directory (AAD tarafından) yönetilen kullanıcı hesapları |14 gün sonra hello son dilim çalıştırın. <br/><br/>90 OAuth tabanlı bağlantılı hizmette dayanan bir dilim 14 günde bir en az bir kez çalıştırılıyorsa, gün. |

tooavoid/Çöz bu hata, hello kullanarak yeniden yetkilendirin **Authorize** düğmesini hello **belirtecinin süresi dolmadan** ve hello bağlantılı hizmeti yeniden dağıtın. Değerleri de oluşturabilirsiniz **SessionID** ve **yetkilendirme** kullanılarak programlı olarak kod şu şekilde özellikleri:

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

Bkz: [AzureDataLakeStoreLinkedService sınıfı](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService sınıfı](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), ve [AuthorizationSessionGetResponse sınıfı](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) ayrıntıları konuları Merhaba kod içinde kullanılan hello Data Factory sınıfları hakkında. Bir başvuru ekleyin: Merhaba WindowsFormsWebAuthenticationDialog sınıfı için Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll. 

## <a name="azure-sql-linked-service"></a>Azure SQL bağlı hizmeti
Azure SQL bağlı hizmeti oluşturma ve hello ile kullanma [saklı yordam etkinliği](data-factory-stored-proc-activity.md) tooinvoke Data Factory işlem hattı bir saklı yordam. Bkz: [Azure SQL Bağlayıcısı](data-factory-azure-sql-connector.md#linked-service-properties) makale bu bağlı hizmetin hakkında ayrıntılı bilgi için.

## <a name="azure-sql-data-warehouse-linked-service"></a>Bağlı hizmetin Azure SQL veri ambarı
Bir Azure SQL Data Warehouse bağlı hizmet oluşturma ve hello ile kullanma [saklı yordam etkinliği](data-factory-stored-proc-activity.md) tooinvoke Data Factory işlem hattı bir saklı yordam. Bkz: [Azure SQL Data Warehouse Bağlayıcısı](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) makale bu bağlı hizmetin hakkında ayrıntılı bilgi için.

## <a name="sql-server-linked-service"></a>SQL Server hizmeti bağlı
Bir SQL Server bağlantılı hizmet oluşturma ve hello ile kullanma [saklı yordam etkinliği](data-factory-stored-proc-activity.md) tooinvoke Data Factory işlem hattı bir saklı yordam. Bkz: [SQL Server Bağlayıcısı](data-factory-sqlserver-connector.md#linked-service-properties) makale bu bağlı hizmetin hakkında ayrıntılı bilgi için.

