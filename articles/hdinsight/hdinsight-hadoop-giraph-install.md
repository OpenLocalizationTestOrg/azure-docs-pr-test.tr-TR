---
title: "Giraph hadoop'ta aaaInstall ve kullanım Hdınsight'ta - Azure kümeleri | Microsoft Docs"
description: "Toocustomize Hdınsight küme nasıl ile Giraph ve nasıl öğrenin toouse Giraph."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a>Yükleme ve Windows tabanlı Hdınsight kümelerinde Giraph kullanma

Betik eylemi kullanarak Giraph ile toocustomize Windows Hdınsight kümesi nasıl ve ne öğrenin toouse Giraph tooprocess büyük ölçekli grafikleri. Linux tabanlı bir kümeyle Giraph kullanma hakkında daha fazla bilgi için bkz: [yükleme Giraph Hdınsight Hadoop kümeleri (Linux) üzerinde](hdinsight-hadoop-giraph-install-linux.md).

> [!IMPORTANT]
> Merhaba Windows tabanlı Hdınsight kümeleri ile bu belgeyi yalnızca çalışma adımları. Hdınsight yalnızca Windows'da Hdınsight 3.4 ' düşük sürümleri için kullanılabilir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement). Hakkında bilgi için bir Linux tabanlı Hdınsight kümesinde tooinstall Giraph bkz [yükleme Giraph Hdınsight Hadoop kümeleri (Linux) üzerinde](hdinsight-hadoop-giraph-install-linux.md).


Kullanarak Azure Hdınsight (Hadoop, Storm, HBase, Spark) kümede herhangi bir türde üzerinde Giraph yükleyebilirsiniz *betik eylemi*. Hdınsight kümesinde bir örnek komut dosyası tooinstall Giraph salt okunur Azure depolama blobunu gelen kullanılabilir [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1). Merhaba örnek betik yalnızca Hdınsight küme sürümü ile 3.1 çalışır. Hdınsight küme sürümleri hakkında daha fazla bilgi için bkz: [Hdınsight küme sürümleri](hdinsight-component-versioning.md).

**İlgili makaleler**

* [Giraph Hdınsight Hadoop kümeleri (Linux) yükleyin](hdinsight-hadoop-giraph-install-linux.md)
* [Hdınsight'ta Hadoop kümeleri oluşturma](hdinsight-provision-clusters.md): Hdınsight kümeleri oluşturma hakkında genel bilgi.
* [Betik eylemi kullanarak Hdınsight kümesi özelleştirme][hdinsight-cluster-customize]: betik eylemi kullanarak Hdınsight kümelerini özelleştirme hakkında genel bilgi.
* [Hdınsight için betik eylemi betikleri geliştirme](hdinsight-hadoop-script-actions.md).

## <a name="what-is-giraph"></a>Giraph nedir?
<a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> tooperform grafik Hadoop kullanarak işleme sağlar ve Azure Hdınsight ile kullanılabilir. Grafikleri hello Internet gibi büyük bir ağdaki yönlendiricileri arasındaki hello bağlantıları gibi nesneler arasındaki ilişkileri modellemek veya sosyal ağlarda (bazen başvurulan tooas sosyal grafiği) arasındaki ilişkileri kişiler. Grafik işleme hello bir grafik nesneleri arasındaki ilişkiler hakkında tooreason gibi sağlar:

* Geçerli ilişkilere dayanan olası arkadaş tanımlama.
* Merhaba kısa rotayı bir ağda iki bilgisayar arasında tanımlayıcı.
* Web sayfalarının Hello sayfa derecesini hesaplama.

## <a name="install-giraph-using-portal"></a>Portal kullanarak Giraph yükleyin
1. Hello kullanarak bir küme oluşturmaya başlamak **özel Oluştur** konusunda açıklandığı gibi seçeneği [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-provision-clusters.md).
2. Hello üzerinde **betik eylemleri** sayfa hello Sihirbazı'nın tıklatın **betik eylemi eklemek** tooprovide aşağıda gösterildiği gibi hello betik eylemi hakkında ayrıntıları:

    ![Betik eylemi toocustomize bir küme kullanın](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "kullanım betik eylemi toocustomize küme")

    <table border='1'>
        <tr><th>Özellik</th><th>Değer</th></tr>
        <tr><td>Ad</td>
            <td>Merhaba betik eylemi için bir ad belirtin. Örneğin, <b>yükleme Giraph</b>.</td></tr>
        <tr><td>Betik URI'si</td>
            <td>Çağrılan toocustomize hello küme hello Tekdüzen Kaynak Tanımlayıcısı (URI) toohello komut dosyasını belirtin. Örneğin, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></td></tr>
        <tr><td>Düğüm Türü</td>
            <td>Merhaba özelleştirme betik çalıştığı hello düğüm belirtin. Seçebileceğiniz <b>tüm düğümleri</b>, <b>Head yalnızca düğümlerin</b>, veya <b>yalnızca çalışan düğümleri</b>.
        <tr><td>Parametreler</td>
            <td>Merhaba komut dosyası için gereken Hello parametreleri belirtin. Bunu boş bırakabilirsiniz şekilde hello betik tooinstall Giraph herhangi bir parametre gerektirmez.</td></tr>
    </table>

    Birden fazla betik eylemi tooinstall hello kümede birden çok bileşen ekleyebilirsiniz. Merhaba komut dosyaları ekledikten sonra hello küme oluşturma hello onay işareti toostart tıklayın.

## <a name="use-giraph"></a>Giraph kullanma
Merhaba SimpleShortestPathsComputation örnek toodemonstrate hello basic kullanırız <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> hello en kısa yolu bir grafik nesneler arasındaki bulmak için uygulama. Merhaba SimpleShortestPathsComputation örneği ve görünüm hello sonuçları kullanarak bir iş çalıştırmak adımları tooupload hello örnek veriler ve hello örnek jar, aşağıdaki hello kullanın.

1. Örnek veri dosyası tooAzure Blob storage'ı yükleyin. Yerel iş istasyonunda, adlı yeni bir dosya oluşturun **tiny_graph.txt**. Satırlardan hello içermelidir:

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    Merhaba tiny_graph.txt dosya toohello birincil depolama Hdınsight kümenizin karşıya yükleyin. Yönergeler için tooupload verileri, görmek [hdınsight'ta Hadoop işleri için verileri karşıya yükleme](hdinsight-upload-data.md).

    Bu veri hello biçimi kullanarak bir yönlendirilmiş grafik nesneler arasındaki ilişkiyi tanımlayan [kaynak\_kimliği, kaynak\_değeri [[hedef\_kimliği], [Kenar\_değer],...]]. Her satır arasındaki bir ilişkiyi temsil eder bir **kaynak\_kimliği** nesne ve bir veya daha fazla **taşınmaya\_kimliği** nesneleri. Merhaba **kenar\_değeri** (veya ağırlık), hello gücü veya hello bağlantı uzaklığı olarak düşünülebilir **source_id** ve **taşınmaya\_kimliği**.

    Çıkış çizilmiş ve nesneleri arasındaki hello uzaklığı olarak hello değeri (veya ağırlık) kullanarak, verileri yukarıda hello şuna benzeyebilir:

    ![Daireler arasında değişen uzaklığı satır olarak çizilen tiny_graph.txt](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. Merhaba SimpleShortestPathsComputation örneği çalıştırın. Giriş olarak hello tiny_graph.txt dosyasını kullanarak aşağıdaki Azure PowerShell cmdlet'leri toorun hello örneğine hello kullanın.

    > [!IMPORTANT]
    > Azure Service Manager kullanılarak HDInsight kaynaklarının yönetilmesi için Azure PowerShell desteği **kullanım dışı bırakılmış** ve 1 Ocak 2017 tarihinde kaldırılmıştır. Azure Resource Manager ile çalışan hello adımları bu belgenin kullanımı hello yeni Hdınsight cmdlet'lerini.
    >
    > Lütfen başlangıç adımları izleyin [yüklemek ve Azure PowerShell yapılandırma](/powershell/azureps-cmdlets-docs) tooinstall hello en son Azure PowerShell sürümü. Komut dosyalarınız varsa bu gereksinimi toobe Azure Resource Manager ile çalışma toouse hello yeni cmdlet'leri değişiklik için bkz: [geçiş tooAzure Resource Manager tabanlı geliştirme araçları Hdınsight kümeleri için](hdinsight-hadoop-development-using-azure-resource-manager.md) daha fazla bilgi için.

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    Yukarıdaki örnek Hello yerine **clustername** Giraph yüklü olan Hdınsight kümenize hello adı.
3. Merhaba sonuçları görüntüleyin. Merhaba işi tamamlandıktan sonra hello sonuçları hello iki çıktı dosyalarında depolanır **wasb: / / / örnek/çıkış/shotestpaths** klasör. Merhaba dosyaları çağrılır **bölümü m 00001** ve **bölümü m 00002**. Aşağıdaki adımları toodownload ve görünüm hello çıktı hello gerçekleştirin:

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    Bu hello oluşturacak **çıkış/örnek/shortestpaths** dizin yapısını hello geçerli dizinde iş istasyonu ve indirme hello iki çıktı dosyaları toothat konumu.

    Kullanım hello **kat** cmdlet toodisplay hello hello dosyaların içeriğini:

        Cat example/output/shortestpaths/part*

    Hello çıktı toohello aşağıdaki benzer görünmelidir:

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    Merhaba SimpleShortestPathComputation örnek nesne kimliği 1 ile sabit kodlanmış toostart olan ve hello en kısa yolu tooother nesneleri bulun. Hello çıktı olarak okumanız gereken şekilde `destination_id distance`, uzaklığı hello değeri (veya ağırlık) seyahat hello kenarlarının nesne kimliği 1 ve hello hedef kimliği arasında olduğu

    Bu görselleştirme, hello kısa yolları kimliği 1 ile tüm diğer nesnelerin arasında seyahat hello sonuçları doğrulayabilirsiniz. Kimliği 1 ve kimliği 4 arasındaki en kısa yolu hello Not 5'tir. Merhaba toplam aralıklarını budur <span style="color:orange">kimliği 1 ve 3</span>ve ardından <span style="color:red">kimliği 3 ve 4</span>.

    ![Nesnelerin arasında çizilmiş kısa yolları daireler olarak çizme](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a>Giraph işlemleri PowerShell kullanarak yükleme
Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  Merhaba örnek gösterilmektedir nasıl tooinstall Azure PowerShell kullanarak Spark. Toocustomize hello betik toouse gerek [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).

## <a name="install-giraph-using-net-sdk"></a>.NET SDK kullanarak Giraph yükleyin
Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). Merhaba örnek gösterilmektedir nasıl tooinstall Spark hello .NET SDK kullanarak. Toocustomize hello betik toouse gerek [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).

## <a name="see-also"></a>Ayrıca bkz.
* [Giraph Hdınsight Hadoop kümeleri (Linux) yükleyin](hdinsight-hadoop-giraph-install-linux.md)
* [Hdınsight'ta Hadoop kümeleri oluşturma](hdinsight-provision-clusters.md): Hdınsight kümeleri oluşturma hakkında genel bilgi.
* [Betik eylemi kullanarak Hdınsight kümesi özelleştirme][hdinsight-cluster-customize]: betik eylemi kullanarak Hdınsight kümelerini özelleştirme hakkında genel bilgi.
* [Hdınsight için betik eylemi betikleri geliştirme](hdinsight-hadoop-script-actions.md).
* [Yükleme ve Spark Hdınsight kümelerinde kullanma][hdinsight-install-spark]: Spark yükleme hakkında örnek betik eylemi.
* [Hdınsight kümelerinde R yüklemek][hdinsight-install-r]: betik eylemi örnek r yükleme hakkında
* [Hdınsight kümelerinde Solr yükleme](hdinsight-hadoop-solr-install.md): Solr yükleme hakkında örnek betik eylemi.

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
