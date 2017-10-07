---
title: "Hdınsight toocustomize kümelerinde - Azure R aaaUse | Microsoft Docs"
description: "Bilgi nasıl tooinstall R kullanarak komut dosyası eylemi ve Hdınsight kümelerinde R kullanın."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bf5adf2e18dc43a743b29fd1567fad731b9c3ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a>HDInsight'taki Hadoop kümelerinde R programını yükleme ve kullanma

Toocustomize Windows Hdınsight kümesi R ile betik eylemi kullanarak nasıl temel ve nasıl hdınsight'ta R toouse kümeleri öğrenin. Merhaba [Hdınsight teklifi](https://azure.microsoft.com/pricing/details/hdinsight/) R Server Hdınsight kümenize bir parçası olarak içerir. Bu R betiklerini toouse MapReduce ve Spark dağıtılmış toorun hesaplamalar sağlar. Daha fazla bilgi için bkz. [HDInsight R Server kullanmaya başlama](hdinsight-hadoop-r-server-get-started.md). Linux tabanlı bir kümeyle R kullanma hakkında daha fazla bilgi için bkz: [yükleme ve kullanma R Hdınsight Hadoop kümeleri (Linux) üzerinde](hdinsight-hadoop-r-scripts-linux.md).

Kullanarak Azure Hdınsight (Hadoop, Storm, HBase, Spark) kümede herhangi bir türde üzerinde R yükleyebilirsiniz *betik eylemi*. Hdınsight kümesinde bir örnek komut dosyası tooinstall R Salt okunur Azure depolama blobunu gelen kullanılabilir [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).

**İlgili makaleler**

* [Yükleme ve Hdınsight Hadoop kümeleri (Linux) R kullanma](hdinsight-hadoop-r-scripts-linux.md)
* [Hdınsight'ta Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md): Hdınsight kümeleri oluşturma hakkında genel bilgiler
* [Betik eylemi kullanarak Hdınsight kümesi özelleştirme][hdinsight-cluster-customize]: betik eylemi kullanarak Hdınsight kümelerini özelleştirme hakkında genel bilgiler
* [Hdınsight için betik eylemi betikleri geliştirme](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a>R nedir?
Merhaba <a href="http://www.r-project.org/" target="_blank">R proje istatistiksel bilgi işlem için</a> bir açık kaynak dili ve istatistiksel bilgi işlem ortamı. R yüzlerce yapı içinde istatistik işlevleri ve işlev ve nesne odaklı programlama yönlerini birleştirir kendi programlama dili sağlar. Yoğun grafik yetenekleri de sağlar. R hello tercih edilen programlama için en profesyonel istatistikçiler ve çeşitli alanları bilimcilerine ortamıdır.

R Azure Blob Storage (WASB) ile uyumlu, böylelikle var. depolanan verileri R kullanarak işlenebilir.  

## <a name="install-r"></a>R yükleme
A [örnek komut dosyası](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) tooinstall R Hdınsight kümesinde, Azure storage'da salt okunur bir blob'nden edinilebilir. Bu bölümde nasıl toouse hello örnek betik hello Azure Portal kullanarak hello küme oluşturulurken bir hata ile ilgili yönergeler sağlar.

> [!NOTE]
> Merhaba örnek betik, Hdınsight kümesi sürüm 3.1 sunulmuştur. Hdınsight küme sürümleri hakkında daha fazla bilgi için bkz: [Hdınsight küme sürümleri](hdinsight-component-versioning.md).
>
>

1. Hello Portalı ' bir Hdınsight kümesi oluştururken tıklatın **isteğe bağlı yapılandırma**ve ardından **betik eylemleri**.
2. Merhaba üzerinde **betik eylemleri** sayfasında, aşağıdaki değerleri hello girin:

    ![Betik eylemi toocustomize bir küme kullanın](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "kullanım betik eylemi toocustomize küme")

    <table border='1'>
        <tr><th>Özellik</th><th>Değer</th></tr>
        <tr><td>Ad</td>
            <td>Örneğin, hello betik eylemi için bir ad belirtmeniz <b>R yükleme</b>.</td></tr>
        <tr><td>Betik URI'si</td>
            <td>Çağrılan toocustomize hello küme, örneğin, hello URI toohello komut dosyasını belirtin <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></td></tr>
        <tr><td>Düğüm Türü</td>
            <td>Merhaba özelleştirme betik çalıştığı hello düğüm belirtin. Seçebileceğiniz <b>tüm düğümleri</b>, <b>Head yalnızca düğümlerin</b>, veya <b>çalışan düğümleri</b> yalnızca.
        <tr><td>Parametreler</td>
            <td>Merhaba komut dosyası için gereken Hello parametreleri belirtin. Ancak, bunu boş bırakabilirsiniz şekilde hello betik tooinstall R herhangi bir parametre gerektirmez.</td></tr>
    </table>

    Birden fazla betik eylemi tooinstall hello kümede birden çok bileşen ekleyebilirsiniz. Merhaba komut dosyaları ekledikten sonra hello küme crating hello onay işareti toostart'ı tıklatın.

Azure PowerShell veya Hdınsight .NET SDK'sı hello kullanarak Hdınsight'ta hello betik tooinstall R de kullanabilirsiniz. Bu yordamları için yönergeler bu makalenin sonraki bölümlerinde verilmiştir.

## <a name="run-r-scripts"></a>R betiği çalıştırın
Bu bölümde, nasıl toorun bir R betiği hello Hadoop küme Hdınsight ile açıklanmaktadır.

1. **Uzak Masaüstü Bağlantısı toohello küme kurmak**: hello Portal, yüklü R ile oluşturduğunuz hello küme için Uzak masaüstünü etkinleştir ve toohello kümesine bağlanın. Yönergeler için bkz: [RDP kullanarak tooHDInsight kümelerine bağlanmak](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).
2. **Açık hello R konsol**: hello R yükleme hello baş düğüm hello masaüstünde bir bağlantı toohello R konsol koyar. ' I tıklatın, üzerinde tooopen hello R konsol.
3. **Merhaba R betiği çalıştırma**: hello R betiği, yapıştırma seçerek ve ENTER tuşuna basarak doğrudan hello R konsolundan çalıştırılabilir. Burada, hello 1 sayıları too100 oluşturur ve bunları 2 ile çarpar basit bir örnek komut verilmiştir.

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

r ile yüklenen hello ilk iki satır çağrısı hello RHadoop kitaplıkları son satırı baskı siparişi hello sonuçları toohello konsol hello. Merhaba çıktı aşağıdaki gibi görünmelidir:

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a>R işlemleri PowerShell kullanarak yükleme
Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  Merhaba örnek gösterilmektedir nasıl tooinstall Azure PowerShell kullanarak Spark. Toocustomize hello betik toouse gerek [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).

## <a name="install-r-using-net-sdk"></a>.NET SDK kullanarak R yükleme
Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). Merhaba örnek gösterilmektedir nasıl tooinstall Spark hello .NET SDK kullanarak. Toocustomize hello betik toouse gerek [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).

## <a name="see-also"></a>Ayrıca bkz.
* [Yükleme ve Hdınsight Hadoop kümeleri (Linux) R kullanma](hdinsight-hadoop-r-scripts-linux.md)
* [Hdınsight'ta Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md): Hdınsight kümeleri oluşturma hakkında genel bilgiler
* [Betik eylemi kullanarak Hdınsight kümesi özelleştirme][hdinsight-cluster-customize]: betik eylemi kullanarak Hdınsight kümelerini özelleştirme hakkında genel bilgiler
* [Hdınsight için betik eylemi betikleri geliştirme](hdinsight-hadoop-script-actions.md)
* [Yükleme ve Spark Hdınsight kümelerinde kullanma][hdinsight-install-spark]: betik eylemi örnek Spark yükleme hakkında
* [Hdınsight kümelerinde Giraph yükleme](hdinsight-hadoop-giraph-install.md): betik eylemi örnek Giraph yükleme hakkında
* [Hdınsight kümelerinde Solr yükleme](hdinsight-hadoop-solr-install-linux.md): Solr yükleme hakkında örnek betik eylemi.

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
