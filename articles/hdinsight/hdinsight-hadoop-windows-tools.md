---
title: "aaaUse hdınsight'ta - Azure Hadoop ile Windows bilgisayarı | Microsoft Docs"
description: "Bir Windows PC hadoop'ta Hdınsight üzerinde çalışır. PowerShell, Visual Studio ve Linux araçlarıyla sorgu kümeleri ve yönetin. .NET ile büyük veri çözümleri geliştirin."
services: hdinsight
keywords: "windows, hadoop'ta windows için hadoop"
author: cjgronlund
manager: jhubbard
ms.author: cgronlun
ms.date: 05/17/2017
ms.topic: article
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 7c93f16e93349c0b8fb1abd55320c2c172b93aa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="work-in-hello-hadoop-ecosystem-on-hdinsight-from-a-windows-pc"></a>Bir Windows PC hdınsight'ta Hadoop ekosistemine Hello çalışma

Hdınsight'ta Hadoop ekosistemine hello çalışmak için geliştirme ve hello Windows bilgisayarı yönetim seçenekleri öğrenin. 

Hdınsight Apache Hadoop ve Hadoop bileşenleri, açık kaynaklı teknolojileri Linux'ta geliştirilen temel alır. Hdınsight sürüm 3.4 ve daha yüksek hello Ubuntu Linux dağıtım hello OS hello küme için temel olarak kullanır. Ancak, bir Windows istemci ya da Windows geliştirme ortamı Hdınsight ile çalışabilirsiniz.

## <a name="use-powershell-for-deployment-and-management-tasks"></a>Dağıtım ve yönetim görevleri için PowerShell kullanın
Azure PowerShell toocontrol kullanın ve Windows'dan hdınsight'ta dağıtım ve yönetim görevlerini otomatikleştiren bir komut dosyası ortamıdır.

PowerShell ile gerçekleştirebileceğiniz görevleri örnekleri:

* [PowerShell kullanarak kümeleri oluşturma](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [PowerShell kullanarak Hive sorguları çalıştırma](hdinsight-hadoop-use-hive-powershell.md)
* [PowerShell ile kümelerini yönetme](hdinsight-administer-use-powershell.md)

Çok adımları[Azure PowerShell'i yükleme ve yapılandırma](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooget hello en son sürümü. Değiştirilen toobe toouse hello yeni cmdlet'leri Azure Resource Manager için gereken komut dosyalarınız varsa, bkz: [tooAzure Resource Manager tabanlı geliştirme araçlarına Hdınsight kümeleri geçirme](hdinsight-hadoop-development-using-azure-resource-manager.md).

## <a name="utilities-you-can-run-in-a-browser"></a>Bir tarayıcıda çalıştırmak yardımcı programları
Merhaba aşağıdaki yardımcı programlar bir web tarayıcıda çalışan kullanıcı Arabirimi vardır:
* **[Azure bulut Kabuğu (Önizleme)](https://docs.microsoft.com/azure/cloud-shell/quickstart)**  tarayıcınızda çalıştıran bir etkileşimli, komut satırı kabuğu olan ve Azure portalı içinden hello.
* **[Ambari Web kullanıcı arabirimini](hdinsight-hadoop-manage-ambari.md)**  bir yönetim ve izleme yardımcı programı hello işleri, farklı türde kullanılan toomanage gibi olabilir Azure portalında kullanılabilir:
    * [Ambari REST API hello ile kullanma](hdinsight-hadoop-manage-ambari-rest-api.md)
    * [Ambari Hive görünümünü](hdinsight-hadoop-use-hive-ambari-view.md)
    * [Ambari Tez görünümünde](hdinsight-debug-ambari-tez-view.md)

## <a name="data-lake-hadoop-tools-for-visual-studio"></a>Visual Studio için Data Lake (Hadoop) araçları
Visual Studio toodeploy için Data Lake araçları kullanmak ve Storm topolojilerini yönetin. Data Lake araçları hello toodevelop C# Storm topolojileri Visual Studio ile sağlayan SCP.NET SDK de yükler.

Aşağıdaki örnekler, toohello geçmeden önce [yükleyin ve Visual Studio için Data Lake araçları deneyin](hdinsight-hadoop-visual-studio-tools-get-started.md). 

Visual Studio için Visual Studio ve Data Lake araçları ile gerçekleştirebileceğiniz görevleri örnekleri:
* [Dağıtma ve Storm topolojilerini Visual Studio'dan yönetme](hdinsight-storm-deploy-monitor-topology-linux.md)
* [Visual Studio kullanarak Storm için C# topolojileri geliştirme](hdinsight-storm-develop-csharp-visual-studio-topology.md). Merhaba bitleri örnek şablonları içeren Storm Topolojileri için Azure Cosmos DB ve SQL veritabanı gibi toodatabases bağlanabilir.

## <a name="visual-studio-and-hello-net-sdk"></a>Visual Studio ve hello .NET SDK'sı 

Büyük veri uygulamaları geliştirmek ve Visual Studio hello .NET SDK'sı toomanage kümeleriyle kullanın. Diğer IDE görevleri aşağıdaki Merhaba kullanabilirsiniz ancak Visual Studio örnekleri gösterilir.

Merhaba Visual Studio .NET SDK ile gerçekleştirebileceğiniz görevleri örnekleri:
* [Veri kümeleri oluşturma ve bir .NET Framework uygulamasından Hdınsight'ta çalışma](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* [Merhaba .NET SDK kullanarak Hive sorguları çalıştırma](hdinsight-hadoop-use-hive-dotnet-sdk.md)
* [C# kullanıcı tanımlı işlevler Hive veya Pig Hadoop akış ile kullanma](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

> İpucu Windows tabanlı Hdınsight kümeleri ile .NET çözümleri çalıştırıyorsanız, iyi zaman tooplan bir geçiş olduğunu tooLinux tabanlı kümeler. Daha fazla bilgi için bkz: [geçirmek .NET çözümü Windows tabanlı Hdınsight için tooLinux tabanlı Hdınsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).

## <a name="intellij-idea-and-eclipse-ide-for-spark-clusters"></a>Intellij Idea ve Spark kümeleri için Eclipse IDE
Her ikisi de [Intellij Idea](https://www.jetbrains.com/idea/download) ve hello [Eclipse IDE](https://www.eclipse.org/downloads/) için kullanılabilir:
* Geliştirme ve Hdınsight Spark kümesi üzerinde bir Scala Spark uygulamasının gönderin.
* Spark küme kaynaklarını erişin.
* Geliştirme ve Scala Spark uygulama yerel olarak çalıştırın.

Bu makaleler Göster nasıl: 
* Intellij Idea: [hello Intellij eklenti için Azure Araç Seti ve hello Scala SDK kullanarak Oluştur Spark uygulamaları.](hdinsight-apache-spark-intellij-tool-plugin.md)
* IDE veya Scala IDE Eclipse için eclipse: [oluşturma Spark uygulamaları ve hello Eclipse için Azure Araç Seti](hdinsight-apache-spark-eclipse-tool-plugin.md) 


## <a name="notebooks-on-spark-for-data-scientists"></a>Spark üzerinde veri bilimcilerine dizüstü bilgisayarlar 
Hdınsight'ta Apache Spark kümeleri Zeppelin not defterlerini ve Jupyter not defterleri ile kullanılabilir çekirdekler içerir. 

* [Nasıl toouse tekrar üzerinde Spark kümeleri Jupyter not defterlerini tootest Spark uygulamaları ile bilgi edinin](hdinsight-apache-spark-zeppelin-notebook.md)
* [Nasıl toouse Zeppelin not defterlerini Spark kümeleri toorun Spark işlerinin öğrenin](hdinsight-apache-spark-jupyter-notebook-kernels.md) 


## <a name="run-linux-based-tools-and-technologies-on-windows"></a>Linux tabanlı araçlar ve teknolojiler Windows'ta çalıştırma

Burada bir araç veya yalnızca Linux üzerinde kullanılabilir teknolojisi kullanmalıdır bir durumla karşılaşırsanız, aşağıdaki seçenekleri şu hello göz önünde bulundurun:

* **Windows 10 (beta) bash** Windows'da Linux alt sistemi sağlar. Bash toomaintain adanmış bir Linux yüklemesine gerek kalmadan Linux yardımcı programını çalıştırın toodirectly sağlar. [Yükleyin ve Windows 10'hello Bash beta çalıştırın](https://msdn.microsoft.com/commandline/wsl/install_guide)
* **Windows için docker** toomany Linux tabanlı araçlar erişim sağlar ve doğrudan Windows çalıştırabilirsiniz. Örneğin, Windows doğrudan kovanından Docker toorun hello Beeline istemci kullanabilirsiniz. Ayrıca Docker toorun yerel Jupyter not defteri kullanın ve hdınsight'ta tooSpark uzaktan bağlanın. [Docker için Windows ile çalışmaya başlama](https://docs.docker.com/docker-for-windows/)
* **[MobaXTerm](http://mobaxterm.mobatek.net/)**  bir SSH bağlantısı üzerinden toographically Gözat hello küme dosya sistemi sağlar.

## <a name="next-steps"></a>Sonraki adımlar
Linux tabanlı kümelerde yeni tooworking değilseniz, makaleler izleyin hello bakın:
* [Hadoop, Kafka, Spark veya diğer kümeleri Kur](hdinsight-hadoop-provision-linux-clusters.md)
* [Linux'ta Hdınsight kümeleri için ipuçları](hdinsight-hadoop-linux-information.md)