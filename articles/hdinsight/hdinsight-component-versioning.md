---
title: "aaaHadoop bileşenleri ve sürümleri - Azure Hdınsight | Microsoft Docs"
description: "Merhaba Hadoop bileşenleri ve Hdınsight ve hello hizmet düzeyleri bu Hortonworks veri platformu bulut dağıtımını kullanılabilir sürümlerde öğrenin."
keywords: "hadoop sürümleri, hadoop ekosistemi bileşenlerini, hadoop bileşenleri nasıl toocheck hadoop sürümü"
services: hdinsight
editor: cgronlun
manager: asadk
author: bprakash
tags: azure-portal
documentationcenter: 
ms.assetid: 367b3f4a-f7d3-4e59-abd0-5dc59576f1ff
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: bprakash
ms.openlocfilehash: b661d901b0113458c3501ec06454fc8841189672
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-hadoop-components-and-versions-available-with-hdinsight"></a>Merhaba Hadoop bileşenleri ve Hdınsight ile kullanılabilir sürümlerini nelerdir?

Merhaba Apache Hadoop ekosistemi bileşenlerini ve Microsoft Azure hdınsight'ta sürümleri hakkında bilgi edinin gibi standart ve Premium hizmet düzeyleri hello. Ayrıca, bilgi nasıl toocheck hdınsight'ta Hadoop bileşen sürümü. 

Bulut dağıtım sürümünün Hortonworks veri Platformu (HDP) her Hdınsight sürümüdür.

## <a name="hadoop-components-available-with-different-hdinsight-versions"></a>Hadoop bileşenleri farklı Hdınsight sürümleri ile kullanılabilir
Azure Hdınsight herhangi bir zamanda dağıtılabilir birden çok Hadoop küme sürümlerindeki destekler. Her sürüm seçimi hello HDP dağıtım belirli bir sürümü ve o dağıtım içinde bulunan bileşenleri kümesi oluşturur. 17 Şubat 2017'dan sonra Azure Hdınsight tarafından kullanılan hello varsayılan küme sürüm 3.5 ve HDP 2.5 üzerinde temel alır.

Hdınsight küme sürümleri ile ilişkili hello bileşen sürümü, aşağıdaki tablonun hello listelenir. 

> [!NOTE]
> Merhaba Hdınsight hizmeti için Hello varsayılan sürüm verilmeksizin. Bir sürüm bağımlılığı varsa hello .NET SDK'sı, Azure PowerShell ve Azure CLI ile kümelerinizi oluşturduğunuzda hello Hdınsight sürüm belirtin.

| Bileşen | Hdınsight 3.6 (varsayılan) | Hdınsight 3.5 | Hdınsight 3.4 | Hdınsight 3.3 | Hdınsight 3.2 | Hdınsight 3.1 | Hdınsight 3.0 |
| --- | --- | --- | --- | --- | --- | --- |--- |
| Hortonworks Veri Platformu |2.6 |2.5 |2.4 |2.3 |2.2 |2.1.7 |2.0 |
| Apache Hadoop ve YARN |2.7.3 |2.7.3 |2.7.1 |2.7.1 |2.6.0 |2.4.0 |2.2.0 |
| Apache Tez |0.7.0 |0.7.0 |0.7.0 |0.7.0 |0.5.2 |0.4.0 |-|
| Apache Pig |0.16.0 |0.16.0 |0.15.0 |0.15.0 |0.14.0 |0.12.1 |0.12.0 |
| Apache Hive ve HCatalog |1.2.1 |1.2.1 |1.2.1 |1.2.1 |0.14.0 |0.13.1 |0.12.0 |
| Apache Hive2 | 2.1.0 |-|-|-|-|-|-|
| Apache Tez Hive2 | 0.8.4 |-|-|-|-|-|-|
| Apache bırakabilmenizi | 0.7.0 |0.6.0 |-|-|-|-|-|
| Apache HBase |1.1.2 |1.1.2 |1.1.2 |1.1.1 |0.98.4 |0.98.0 |-|
| Apache Sqoop |1.4.6 |1.4.6 |1.4.6 |1.4.6 |1.4.5 |1.4.4 |1.4.4 |
| Apache Oozie |4.2.0 |4.2.0 |4.2.0 |4.2.0 |4.1.0 |4.0.0 |4.0.0 |
| Apache Zookeeper |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.5 |3.4.5 |
| Apache Storm |1.1.0 |1.0.1 |0.10.0 |0.10.0 |0.9.3 |0.9.1 |-|
| Apache Mahout |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0 |0.9.0 |-|
| Apache Phoenix |4.7.0 |4.7.0 |4.4.0 |4.4.0 |4.2.0 |4.0.0.2.1.7.0-2162 |-|
| Apache Spark |2.1.0 (yalnızca Linux) |1.6.2 + 2.0 (yalnızca Linux) |1.6.0 (yalnızca Linux) |1.5.2 (deneysel yapı Linux yalnızca) |1.3.1 (yalnızca Windows) |-|-|
| Apache Kafka | 0.10.0 | 0.10.0 | 0.9.0 |-|-|-|-|
| Apache Ambari | 2.5.0 | 2.4.0 | 2.2.1 | 2.1.0 |-|-|-|
| Apache Zeppelin | 0.7.0 |-|-|-|-|-|-|
| Mono |4.2.1 |4.2.1 |3.2.8 |-|-|-|

## <a name="check-for-current-hadoop-component-version-information"></a>Geçerli Hadoop bileşen sürüm bilgilerini denetleme

Hdınsight küme sürümleri ile ilişkili hello Hadoop ekosistemi bileşen sürümlerini güncelleştirmeleri tooHDInsight ile değiştirebilirsiniz. toocheck hello Hadoop bileşenleri ve hangi sürümlerinin bir küme için kullanılan tooverify hello Ambari REST API kullanın. Merhaba **GetComponentInformation** komutu hizmet bileşenleri hakkında bilgi alır. Merhaba Ayrıntılar için bkz [Ambari belgelerine][ambari-docs].

Windows kümeleri için başka bir şekilde toocheck hello bileşen sürümü Uzak Masaüstü'nü kullanarak toolog tooa kümedeki verilir ve hello hello C:\apps\dist\ dizinin içeriğini inceleyin.

> [!IMPORTANT]
> Linux hello yalnızca Hdınsight sürüm 3.4 veya üstü kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz: [Windows devre dışı bırakma hdınsight'ta](#hdinsight-windows-retirement).

### <a name="release-notes"></a>Sürüm notları

Bkz: [Hdınsight sürüm notları](hdinsight-release-notes.md) ek Sürüm Notları'hello son Hdınsight sürümleri üzerinde.

## <a name="supported-hdinsight-versions"></a>Desteklenen Hdınsight sürümleri
Merhaba aşağıdaki tabloda hello hello Azure portalı üzerinde şu anda kullanılabilir Hdınsight sürümleri listelenmiştir. tooeach Hdınsight sürüm karşılık hello HDP sürümleri hello ürün sürüm tarihleri ile birlikte listelenir. bilinen zaman hello destek sona erme ve sona erme tarihleri de sağlanır.

> [!NOTE]
> Bir sürümünün süresi doldu için destek sonra onu hello Microsoft Klasik Azure Portalı aracılığıyla kullanılamayabilir. Ancak, küme sürümlerindeki toobe hello kullanarak kullanılabilir devam `Version` hello Windows PowerShell parametresinde [yeni AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619331.aspx) komut ve sona erme tarihi hello sürüm kadar .NET SDK'sı hello.
> 
> İki baş düğümler ile yüksek oranda kullanılabilir küme Hdınsight sürüm 2.1 ve üzeri için varsayılan olarak dağıtılır. Hdınsight sürüm 1.6 kümeler için kullanılamaz.

| Hdınsight sürümü | HDP sürüm | VM İŞLETİM SİSTEMİ | Yüksek kullanılabilirlik | Sürüm tarihi | Hello Azure portal kullanılabilirliği | Destek sona erme tarihi | Sona erme tarihi |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Hdınsight 3.6 |HDP 2.6 |Ubuntu 16 |Evet |4 Nisan 2017 |Evet | | |
| Hdınsight 3.5 |HDP 2,5 |Ubuntu 16 |Evet |30 Eylül 2016 |Evet |5 Eylül 2017 |31 May 2018 |
| Hdınsight 3.4 |2.4 HDP |Ubuntu 14.0.4 LTS |Evet |29 Mart 2016 |Evet |29 Aralık 2016 |9 Ocak 2018 |
| Hdınsight 3.3 |2.3 HDP |Windows Server 2012 R2 |Evet |2 aralık 2015 |Evet |27 Haziran 2016 |31 Temmuz 2018 |
| Hdınsight 3.3 |2.3 HDP |Ubuntu 14.0.4 LTS |Evet |2 aralık 2015 |Evet |27 Haziran 2016 |31 Temmuz 2017 |
| Hdınsight 3.2 |HDP 2.2 |Ubuntu 12.04 LTS veya Windows Server 2012 R2 |Evet |18 Şubat 2015 |Hayır |1 Mart 2016 |1 Nisan 2017 |
| Hdınsight 3.1 |HDP 2.1 |Windows Server 2012 R2 |Evet |24 Haziran 2014 |Hayır |18 Mayıs 2015 |30 Haziran 2016 |
| Hdınsight 3.0 |HDP 2.0 |Windows Server 2012 R2 |Evet |11 Şubat 2014 |Hayır |17 Eylül 2014 |30 Haziran 2015 |
| Hdınsight 2.1 |HDP 1.3 |Windows Server 2012 R2 |Evet |28 Ekim 2013 |Hayır |12 Mayıs 2014 |31 Mayıs 2015 |
| Hdınsight 1.6 |HDP 1.1 | |Hayır |28 Ekim 2013 |Hayır |26 Nisan 2014 |31 Mayıs 2015 |

## <a name="hdinsight-windows-retirement"></a>Hdınsight Windows devre dışı bırakma
Microsoft Azure Hdınsight sürüm 3.3 Windows'da Hdınsight son sürümü hello oluştu. Merhaba devre dışı bırakma Windows'da Hdınsight için 31 Temmuz 2018 tarihidir. Tüm Hdınsight kümeleri Windows 3.3 veya önceki sürümlerde varsa, 31 Temmuz 2018 önce tooHDInsight (Hdınsight sürüm 3.5 veya sonrasını) Linux'ta geçirmeniz gerekir. Toohello geçirme Linux işletim sistemi tooretain hello özelliği toocreate etkinleştirir veya Hdınsight kümelerinizi yeniden boyutlandırın. Hdınsight sürüm 3.3 Windows için destek, 27 Haziran 2016 tarihinde süresi doldu.

Hdınsight sürüm 3.4 ile başlayarak, Microsoft Hdınsight hello üzerinde yalnızca Linux işletim sistemi yayımladı. Sonuç olarak, Hdınsight içinde hello bileşenlerinin bazılarını yalnızca Linux için kullanılabilir. Apache bırakabilmenizi, Kafka, etkileşimli Hive, Spark, Hdınsight uygulamaları, bunlar ve Azure Data Lake Store hello birincil dosya sistemi olarak. Merhaba üzerinde yalnızca Linux işletim sistemi Hdınsight'ın gelecek sürümlerinde kullanılabilir. Hiçbir gelecek sürümlerde Windows'da hdınsight olacaktır. 

## <a name="faqs"></a>SSS

### <a name="what-is-hello-timeline-for-retiring-hdinsight-on-windows"></a>Windows'da Hdınsight devre dışı bırakma hello zaman çizelgesi nedir?
31 Temmuz 2018 hello Windows'da Hdınsight için devre dışı bırakma tarihidir. Hello planlanan tarihten bölgeniz için farklıdır, ayrı olarak size bildirilecek. 

### <a name="what-is-hello-impact-of-retiring-hdinsight-on-windows-for-existing-customers"></a>Hdınsight Windows üzerinde var olan müşteriler için devre dışı bırakma hello etkisi nedir?
Windows'da Hdınsight kullanımdan kaldırıldıktan sonra yeni bir Hdınsight Windows Küme oluşturun veya var olan bir Hdınsight Windows kümesine yeniden boyutlandırma olamaz. Hdınsight sürüm 3.3 desteği, 27 Haziran 2016 tarihinde süresi doldu. Bu nedenle, destek veya hata düzeltmeleri Hdınsight 3.3 veya önceki sürümlerinde yoktur. Merhaba üzerinde yalnızca Linux işletim sistemi Hdınsight'ın gelecek sürümlerinde kullanılabilir. Hiçbir gelecek sürümlerde Windows'da hdınsight olacaktır.
 
### <a name="which-versions-of-hdinsight-on-windows-are-affected"></a>Windows'da Hdınsight'ın hangi sürümleri etkilenen?
Azure Hdınsight sürüm 3.3 Hdınsight için Windows hello son sürümü değil. Windows'da Hdınsight kullanımdan önce tüm Hdınsight kümeleri 3.3 veya önceki bir sürümü olmalıdır Windows tooHDInsight sürüm 3.5 veya sonrasını Linux'ta geçirildi. Linux üzerinde kümeleri tooHDInsight geçirme tooretain hello özelliği toocreate yeni kümeleri sağlar veya var olan kümeleri yeniden boyutlandırabilirsiniz. 

### <a name="what-do-i-need-toodo"></a>Ne toodo gerekir?
Hdınsight Windows kümeleri desteklenen tooa Hdınsight Linux kümenizi 31 Temmuz 2018 önce geçirin. Merhaba daha fazla bilgi edinin [Hdınsight geçiş belge](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). Merhaba listesi Azure Hdınsight sürümleri hakkında daha fazla ayrıntı için bkz [desteklenen sürümleri](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-component-versioning#supported-hdinsight-versions). 

### <a name="where-do-i-find-hello-cluster-os-type"></a>Merhaba küme işletim sistemi türü nereden bulabilirim?
Hello Azure portal, toohello Hdınsight kümesine Genel Bakış sayfasına gidin ve bulmak **küme türü** altında **Essentials**. Bu sayfada Hello küme işletim sistemi türleri listelenmektedir. 

### <a name="i-cant-migrate-tooan-hdinsight-linux-cluster-by-july-31-2018-what-is-hello-impact-toomy-hdinsight-windows-cluster"></a>31 Temmuz 2018 tarafından tooan Hdınsight Linux kümesi geçişi yapamazsınız. Merhaba etkisi toomy Hdınsight Windows kümesi nedir?
Merhaba Hdınsight Windows küme olarak çalışır-olduğu, ancak yeni bir Hdınsight Windows Küme oluşturun veya var olan bir Hdınsight Windows kümesine yeniden boyutlandırma olamaz. 

### <a name="my-cluster-has-a-net-dependency-how-do-i-resolve-this-dependency-on-linux"></a>My küme .NET bağımlılığa sahiptir. Bu bağımlılık Linux'ta nasıl giderebilirim?
Hello kullanarak Linux küme bağımlılığı çözümleyebilir [Mono proje](http://www.mono-project.com/). Bu açık kaynak uygulaması .NET, Hdınsight Linux kümeleri için kullanılabilir. Merhaba daha fazla bilgi edinin [Hdınsight geçiş belge](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). 

### <a name="im-a-new-customer-for-hdinsight-on-windows-how-can-i-create-an-hdinsight-windows-cluster"></a>Windows'da Hdınsight için yeni bir müşteri ben. Bir Hdınsight Windows Küme nasıl oluşturabilir miyim?
3 Temmuz 2017 itibariyle yalnızca varolan Hdınsight Windows müşterileri yeni Hdınsight Windows kümeleri oluşturabilirsiniz. Yeni müşteriler, PowerShell veya hello SDK kullanarak bir Hdınsight Windows Küme hello Azure portal oluşturulamıyor. Yeni müşteriler Linux Hdınsight kümesi oluşturmanızı öneririz. Mevcut müşterilerin yeni Hdınsight Windows hello kadar Windows'da Hdınsight tarihten kümeleri oluşturabilirsiniz. 

### <a name="is-there-a-pricing-impact-associated-with-moving-from-hdinsight-on-windows-toohdinsight-on-linux"></a>Hdınsight Linux üzerinde Windows tooHDInsight üzerinde taşıma ile ilişkili bir fiyatlandırma etki var mı?
Hayır, hello fiyatlandırma olduğu hello aynı ya da OS Hdınsight için. 

### <a name="what-are-hello-customer-advantages-associated-with-hello-move-tooonly-using-hdinsight-on-linux"></a>Merhaba ile ilişkili hello müşteri avantajları nelerdir Linux'ta Hdınsight kullanarak tooonly taşıma?
* Zaman-açık kaynak büyük veri teknolojileri hello Hdınsight hizmeti aracılığıyla market
* Büyük topluluk ve destek için ekosistemi
* Hadoop ve diğer büyük veri teknolojileri için özelliği tooexercise etkin geliştirme hello tarafından açık kaynak topluluğu

### <a name="does-hdinsight-on-linux-provide-additional-functionality-beyond-what-is-available-in-hdinsight-on-windows"></a>Linux'ta Hdınsight Windows'da hdınsight'ta kullanılabilenleri ötesinde ek işlevsellik sağlar mı?
Hdınsight sürüm 3.4 ile başlayarak, Microsoft Hdınsight hello üzerinde yalnızca Linux işletim sistemi yayımladı. Sonuç olarak, Hdınsight içinde hello bileşenlerinin bazılarını yalnızca Linux için kullanılabilir. Apache bırakabilmenizi, Kafka, etkileşimli Hive, Spark, Hdınsight uygulamaları, bunlar ve Azure Data Lake Store hello birincil dosya sistemi olarak. 

## <a name="service-level-agreement-for-hdinsight-cluster-versions"></a>Hdınsight küme sürümleri için hizmet düzeyi sözleşmesi
Merhaba hizmet düzeyi sözleşmesi (SLA) cinsinden tanımlanır bir _destek penceresi_. Merhaba destek hello süre bir Hdınsight kümesi sürüm Microsoft Müşteri Hizmetleri ve desteği tarafından desteklenen bir penceredir. Merhaba sürüm varsa, bir _destek sona erme tarihi_ , geçtikten, hello Hdınsight kümesi hello destek penceresi dışında. Merhaba listesi desteklenen sürümleri hakkında daha fazla bilgi için bkz [desteklenen Hdınsight küme sürümleri](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). Belirtilen bir Hdınsight sürüm (yeni bir X + 1 sürümünü kullanıma sunulduktan sonra) X Hello destek sona erme tarihini sonraki sürümleri hello hesaplanır:  

* Formül 1: Merhaba Hdınsight küme sürümü X serbest bırakıldığında 180 gün toohello tarih ekleyin.
* Formül 2: ne zaman hello Hdınsight küme sürümü X + 1 Azure portalında kullanılabilir hale getirileceğini 90 gün toohello tarih ekleyin.

Merhaba _tarihten_ geçmesi hello küme sürümü oluşturulamıyor Hdınsight'ta başlangıç tarihidir. 31 Temmuz 2017 başlayarak, o tarihten sonra Hdınsight kümesi boyutlandırılamaz. 

> [!NOTE]
> Hdınsight Windows kümeleri (2.1, 3.0, 3.1, 3.2 ve 3.3 dahil olmak üzere sürümler) Azure konuk işletim sistemi ailesi sürüm 4, Windows Server 2012 R2 hello 64-bit sürümünü kullanan çalıştırın. Azure konuk işletim sistemi ailesi sürüm 4 hello .NET Framework sürüm 4.0, 4.5, 4.5.1 ve 4.5.2 destekler.

## <a name="hortonworks-release-notes-associated-with-hdinsight-versions"></a>Hortonworks sürüm notları Hdınsight sürümleri ile ilişkili

Merhaba bölüm hello Hortonworks veri platformu dağıtımları ve Hdınsight ile kullanılan Apache bileşenleri için toorelease notları bağlantılar sağlar.
* Hdınsight küme sürümü 3.6 temel alan bir Hadoop dağıtımı kullanır [Hortonworks veri platformu 2.6](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.0/bk_release-notes/content/ch_relnotes.html).
* Hdınsight kümesi sürüm 3.5 temel alan bir Hadoop dağıtımı kullanır [Hortonworks veri platformu 2.5](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.5.0/bk_release-notes/content/ch_relnotes_v250.html). Hdınsight kümesi sürüm 3.5 olduğu hello _varsayılan_ hello Azure portalında oluşturulan Hadoop kümesi.
* Hdınsight kümesi sürüm 3.4 temel alan bir Hadoop dağıtımı kullanır [Hortonworks veri platformu 2.4](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html).
* Hdınsight küme sürümü 3.3 temel alan bir Hadoop dağıtımı kullanır [Hortonworks veri platformu 2.3](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html).

  * [Apache Storm sürüm notları](https://storm.apache.org/2015/11/05/storm0100-released.html) hello Apache Web sitesinde kullanılabilir.
  * [Apache Hive sürüm notları](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12332384&styleName=Text&projectId=12310843) hello Apache Web sitesinde kullanılabilir.
* Hdınsight kümesi sürüm 3.2 temel alan bir Hadoop dağıtımı kullanır [Hortonworks veri platformu 2.2][hdp-2-2].

  * Kullanılabilir aşağıdaki gibi olan belirli Apache bileşenleri için sürüm notları: [0.14 Hive](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310843&version=12326450), [Pig 0.14](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310730&version=12326954), [HBase 0.98.4](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310753&version=12326810), [Phoenix 4.2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12315120&version=12327581), [M/R 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310941&version=12327180), [HDFS 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310942&version=12327181), [YARN 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12313722&version=12327197), [ortak](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310240&version=12327179), [Tez 0.5.2](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314426&version=12328742), [Ambari 2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12312020&version=12327486), [Storm 0.9.3](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314820&version=12327112), ve [Oozie 4.1.0'da](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12324960&projectId=12311620).
* Hdınsight kümesi sürüm 3.1 kullanan temel alan bir Hadoop dağıtım [Hortonworks veri platformu 2.1.7][hdp-2-1-7]. Kasım, 7, 2014 önce oluşturulan Hdınsight 3.1 kümeleri temel [Hortonworks veri platformu 2.1.1][hdp-2-1-1].
* Hdınsight kümesi sürüm 3.0 temel alan bir Hadoop dağıtımı kullanır [Hortonworks veri platformu 2.0][hdp-2-0-8].
* Hdınsight kümesi sürüm 2.1 temel alan bir Hadoop dağıtımı kullanır [Hortonworks veri platformu 1.3][hdp-1-3-0].
* Hdınsight kümesi sürüm 1.6 temel alan bir Hadoop dağıtımı kullanır [Hortonworks veri platformu 1.1][hdp-1-1-0].

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standart ve HDInsight Premium

Azure Hdınsight iki kategoride hello büyük veri Bulutu teklifleri sunar: _standart_ ve _Premium_. Merhaba aşağıdaki tabloda kullanılabilir olan özellikleri listeler _yalnızca_ Hdınsight Premium içinde. Hdınsight standart ve Premium hello tabloda açıkça açıklanmayan özellikleri kullanılabilir.

> [!NOTE]
> Merhaba Hdınsight Premium sunumu şu anda önizlemede yalnızca Linux kümeleri için kullanılabilir.

| Hdınsight Premium özelliği | Açıklama |
| --- | --- |
| Etki alanına katılmış Hdınsight kümeleri |Kurumsal düzeyde güvenlik Hdınsight kümeleri tooAzure Active Directory (Azure AD) etki alanlarını ekleyin. Hdınsight Premium Azure AD toolog tooan Hdınsight kümesinde aracılığıyla doğrulanabilir, kuruluş çalışanların bir listesini yapılandırabilirsiniz. Hello kuruluş yöneticisi, Hive güvenlik için rol tabanlı erişim denetimi kullanarak yapılandırabilir [Apache bırakabilmenizi](http://hortonworks.com/apache/ranger/) ve veri erişim toouse yalnızca gerektiği kadar sınırlayabilirsiniz. Son olarak, hello Yöneticisi çalışanlar tarafından erişilen veri denetleyebilirsiniz ve böylece şirket kaynaklarını İdaresi yüksek derecede elde ilkeleri, değişiklikleri tooaccess denetleyebilirsiniz. Daha fazla bilgi için bkz: [etki alanına katılmış Hdınsight kümeleri yapılandırma](hdinsight-domain-joined-configure.md). |

### <a name="cluster-types-supported-in-hdinsight-premium"></a>Hdınsight Premium içinde desteklenen küme türleri
Merhaba aşağıdaki tabloda, Hdınsight Premium içinde desteklenen hello küme türleri listelenmektedir.

| Küme türü | Standart | Premium (Önizleme) |
| --- | --- | --- |
| Hadoop |Evet |Evet (yalnızca Hdınsight 3.6) |
| Spark |Evet |Hayır |
| HBase |Evet |Hayır |
| Storm |Evet |Hayır |
| R Server |Evet |Hayır |
| Etkileşimli Hive (Önizleme) |Evet |Hayır |
| Kafka (Önizleme) |Evet |Hayır | 

### <a name="support-for-azure-data-lake-store-in-hdinsight-premium"></a>Hdınsight Premium, Azure Data Lake Store desteği

Hdınsight Premium kümeleri, Azure Data Lake Store birincil depolama alanı olarak kullanılmasını desteklemez. Ancak, Azure Data Lake Store Hdınsight Premium kümeleriyle eklenti depolama olarak kullanabilirsiniz.

### <a name="pricing-and-sla"></a>Fiyatlandırma ve SLA
Hdınsight Premium için fiyatlandırma ve SLA hakkında bilgi için bkz: [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="default-node-configuration-and-virtual-machine-sizes-for-clusters"></a>Kümeler için varsayılan düğümü yapılandırması ve sanal makine boyutları
Aşağıdaki tablolar listesi hello varsayılan sanal makine (VM) boyutları Hdınsight kümeleri hello.

> [!IMPORTANT]
> Bir kümede 32'den fazla alt düğüm gerekirse, bir baş düğüm boyutu en az 8 çekirdek ve 14 GB RAM ile seçmeniz gerekir.
> 
> 

* Desteklenen tüm bölgeler Brezilya Güney ve Japonya Batı dışında:

  | Küme türü | Hadoop | HBase | Storm | Spark | R Server |
  | --- | --- | --- | --- | --- | --- |
  | HEAD: varsayılan VM boyutu |D3 v2 |D3 v2 |A3 |D12 v2 |D12 v2 |
  | HEAD: VM boyutları önerilir |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |A3, A4, A5 |D12 v2, D13 v2, D14 v2 |D12 v2, D13 v2, D14 v2 |
  | Çalışan: varsayılan VM boyutu |D3 v2 |D3 v2 |D3 v2 |Windows: D12 v2; Linux: D4 v2 |Windows: D12 v2; Linux: D4 v2 |
  | Çalışan: VM boyutları önerilir |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |Windows: D12 v2 D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |Windows: D12 v2 D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |
  | ZooKeeper: varsayılan VM boyutu | |A3 |A2 | | |
  | ZooKeeper: VM boyutları önerilir | |A3, A4, A5 |A2, A3, A4 | | |
  | Edge: varsayılan VM boyutu | | | | |Windows: D12 v2; Linux: D4 v2 |
  | Kenar: VM boyutu önerilir | | | | |Windows: D12 v2 D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |
* Brezilya Güney ve yalnızca Japonya Batı (v2 boyutları):

  | Küme türü | Hadoop | HBase | Storm | Spark | R Server |
  | --- | --- | --- | --- | --- | --- |
  | HEAD: varsayılan VM boyutu |D3 |D3 |A3 |D12 |D12 |
  | HEAD: VM boyutları önerilir |D3, D4, D12 |D3, D4, D12 |A3, A4, A5 |D12, D13, D14 |D12, D13, D14 |
  | Çalışan: varsayılan VM boyutu |D3 |D3 |D3 |Windows: D12; Linux: D4 |Windows: D12; Linux: D4 |
  | Çalışan: VM boyutları önerilir |D3, D4, D12 |D3, D4, D12 |D3, D4, D12 |Windows: D12, D13, D14; Linux: D4, D12, D13, D14 |Windows: D12, D13, D14; Linux: D4, D12, D13, D14 |
  | ZooKeeper: varsayılan VM boyutu | |A2 |A2 | | |
  | ZooKeeper: VM boyutları önerilir | |A2, A3, A4 |A2, A3, A4 | | |
  | Edge: varsayılan VM boyutları | | | | |Windows: D12; Linux: D4 |
  | Edge: VM boyutları önerilir | | | | |Windows: D12, D13, D14; Linux: D4, D12, D13, D14 |

> [!NOTE]
> - HEAD olarak bilinir *Nimbus* hello Storm için küme türü.
> - Çalışan olarak bilinir *Supervisor* hello Storm için küme türü.
> - Çalışan olarak bilinir *bölge* türü Merhaba HBase kümesi.

## <a name="next-steps"></a>Sonraki adımlar
- [Hadoop, Spark ve Hdınsight hakkında daha fazla bilgi için Kurulum küme](hdinsight-hadoop-provision-linux-clusters.md)
- [Bir Windows PC Hdınsight'ta Hadoop ile çalışma](hdinsight-hadoop-windows-tools.md)

[Supported HDInsight versions]:(#supported-hdinsight-versions)

[image-hdi-versioning-versionscreen]: ./media/hdinsight-component-versioning/hdi-versioning-version-screen.png

[wa-forums]: http://azure.microsoft.com/support/forums/

[connect-excel-with-hive-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md

[hdp-2-2]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[ambari-docs]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[zookeeper]: http://zookeeper.apache.org/
