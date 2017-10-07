---
title: "hdınsight'ta Hadoop Pig aaaUse | Microsoft Docs"
description: "Bilgi nasıl toouse Pig hdınsight'ta Hadoop ile."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 90850f2c742b8954c66ce277127e01b14fc3906f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a>Hdınsight'ta Hadoop ile pig kullanma

Bilgi nasıl toouse [Apache Pig](http://pig.apache.org/) Hdınsight ile...

Pig olan bir platform olarak bilinen bir yordam dilini kullanarak Hadoop için programlar oluşturma için *Pig Latin*. Pig olan oluşturmak için bir alternatif tooJava *MapReduce* çözümleri ve bunu Azure Hdınsight ile birlikte. Aşağıdaki tablo toodiscover hello Hdınsight ile Pig kullanılabilir çeşitli şekillerde hello kullan:

| **Bu** isterseniz... | .. .an **etkileşimli** Kabuk | ... **toplu** işleme | .. hemen bu **küme işletim sistemi** | .. .from bu **istemci işletim sistemi** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux, UNIX, Mac OS X veya Windows |
| [REST API](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux veya Windows |Linux, UNIX, Mac OS X veya Windows |
| [Hadoop için .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux veya Windows |Windows (için şimdi) |
| [Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux veya Windows |Windows |
| [Uzak Masaüstü](hdinsight-hadoop-use-pig-remote-desktop.md) (Hdınsight 3.2 ve 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="why"></a>Pig neden kullanılır?

Hadoop MapReduce kullanarak veri işleme hello zorluklardan biri, işleme mantığı yalnızca bir eşleme ve azaltma işlevini kullanarak uygular. Genellikle karmaşık işleme sahip olan birden çok MapReduce işlemlere işleme toobreak tooachieve istenen hello sonuç birbirine zincirlenmiş.

Pig tooproduce hello istenen çıkış aracılığıyla veri akışları hello dönüşümleri bir dizi olarak işleme toodefine sağlar.

Merhaba Pig Latin dili, toodescribe hello veri akışından bir veya daha fazla dönüşümleri, tooproduce hello istenen çıkış aracılığıyla ham giriş sağlar. Pig Latin programlar bu genel model izleyin:

* **Yük**: hello dosya sisteminden yönetilen veri toobe okuma

* **Dönüştürme**: hello verileri işlemek

* **Döküm veya mağaza**: çıktı veri toohello ekran veya işleme için mağaza

### <a name="user-defined-functions"></a>Kullanıcı tanımlı işlevler

Pig Latin kullanıcı tanımlı işlevler (UDF), Pig Latin içinde zor toomodel mantığı uygulamak tooinvoke dış bileşenlere sağlayan de destekler.

Pig Latin hakkında daha fazla bilgi için bkz: [Pig Latin başvuru el ile 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) ve [Pig Latin başvuru el ile 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).

UDF'ler ile Pig kullanma örneği için aşağıdaki belgeleri hello bakın:

* [Pig hdınsight'ta ile DataFu kullanmak](hdinsight-hadoop-use-pig-datafu-udf.md) -DataFu Apache tarafından tutulan yararlı UDF'ler koleksiyonudur
* [Python Pig ve hdınsight'ta Hive kullanma](hdinsight-python.md)
* [C# Hive veya Pig hdınsight'ta ile kullanma](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <a id="data"></a>Örnek veri

Hdınsight sağlar hello depolanan çeşitli örnek veri kümeleri, `/example/data` ve `/HdiSamples` dizinleri. Bu dizinleri, kümeniz için hello varsayılan depolama arasındadır. Bu belgedeki Hello Pig örnek kullanır hello *log4j* dosya `/example/data/sample.log`.

Hello dosyası içindeki her bir günlükteki içeren bir dizi alanlarının oluşan bir `[LOG LEVEL]` alan tooshow hello türü ve hello önem derecesi, örneğin:

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

Merhaba önceki örnekte hello günlük düzeyi hatasıdır.

> [!NOTE]
> Hello kullanarak log4j dosyasını oluşturabilirsiniz [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) aracı günlüğe kaydetme ve bu dosyayı tooyour blob karşıya yükleyin. Bkz: [karşıya veri tooHDInsight](hdinsight-upload-data.md) yönergeler için. BLOB'ları Azure depolama alanında Hdınsight ile nasıl kullanıldığı konusunda daha fazla bilgi için bkz: [kullanım Azure Blob Storage Hdınsight ile](hdinsight-hadoop-use-blob-storage.md).

## <a id="job"></a>Örnek Proje

Merhaba aşağıdaki Pig Latin iş yükler hello `sample.log` Hdınsight kümenizin hello varsayılan depolama biriminden dosya. Ardından, bir dizi nasıl sayıma birçok kez her günlük düzeyi içinde oluştu hello giriş verilerini neden dönüşümleri gerçekleştirir. Merhaba sonuçları tooSTDOUT yazılır.

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

Merhaba aşağıdaki görüntüde her hangi bir dönüşüm toohello veri mu özetini gösterir.

![Merhaba dönüşümleri grafik gösterimi][image-hdi-pig-data-transformation]

## <a id="run"></a>Merhaba Pig Latin işini çalıştır

Hdınsight, Pig Latin işleri çeşitli yöntemler kullanarak çalıştırabilirsiniz. Hangi yöntemi sizin için uygun olan tablo toodecide aşağıdaki hello kullanın ve sonra kılavuz hello bağlantıyı izleyin.

| **Bu** isterseniz... | .. .an **etkileşimli** Kabuk | ... **toplu** işleme | .. hemen bu **küme işletim sistemi** | .. .from bu **istemci** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux, UNIX, Mac OS X veya Windows |
| [Curl](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux veya Windows |Linux, UNIX, Mac OS X veya Windows |
| [Hadoop için .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux veya Windows |Windows (için şimdi) |
| [Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux veya Windows |Windows |
| [Uzak Masaüstü](hdinsight-hadoop-use-pig-remote-desktop.md) (Hdınsight 3.2 ve 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="pig-and-sql-server-integration-services"></a>Pig ve SQL Server Integration Services

SQL Server Integration Services (SSIS) toorun Pig işi kullanabilirsiniz. Hello Azure Feature Pack SSIS için Hdınsight'ta Pig işlerle çalışma bileşenleri aşağıdaki hello sağlar.

* [Azure Hdınsight Pig görevi][pigtask]

* [Azure aboneliği Bağlantı Yöneticisi][connectionmanager]

Hello Azure Feature Pack hakkında daha fazla bilgi için SSIS [burada][ssispack].

## <a id="nextsteps"></a>Sonraki adımlar
Göre nasıl toouse aşağıdaki kullanım Merhaba, Hdınsight ile Pig tooexplore diğer yolları toowork Azure Hdınsight ile bağlantıları öğrendiniz.

* [Veri tooHDInsight karşıya yükle][hdinsight-upload-data]
* [HDInsight ile Hive kullanma][hdinsight-use-hive]
* [Hdınsight ile Sqoop kullanma](hdinsight-use-sqoop.md)
* [Oozie Hdınsight ile kullanma](hdinsight-use-oozie.md)
* [Hdınsight ile MapReduce işleri kullanma][hdinsight-use-mapreduce]

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
