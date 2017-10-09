---
title: "aaaManage Hadoop kümeleri PowerShell - Azure ile hdınsight'ta | Microsoft Docs"
description: "Tooperform yönetim hello için Azure PowerShell kullanarak hdınsight'ta Hadoop kümelerinin nasıl görevleri öğrenin."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: bfdfa754-18e5-4ef9-b0d6-2dbdcebc0283
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 3df082d752fa8c703db82a54b82b740290af6729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a>Azure PowerShell kullanarak hdınsight'ta Hadoop kümelerini yönetme
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Azure PowerShell toocontrol kullanın ve hello dağıtımı ve Yönetimi azure'da iş yüklerinizin otomatikleştirmek bir güçlü komut dosyası ortamıdır. Bu makalede, Azure hdınsight'ta toomanage Hadoop kümelerini yerel bir Azure PowerShell konsol hello üzerinden kullanarak Windows PowerShell kullanma öğreneceksiniz. Merhaba Hdınsight PowerShell cmdlet'leri Hello listesi için bkz [Hdınsight cmdlet başvurusu][hdinsight-powershell-reference].

**Önkoşullar**

Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="install-azure-powershell"></a>Azure PowerShell'i yükleme
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

Azure PowerShell sürüm 0.9 yüklediyseniz x, bunu yeni bir sürümünü yüklemeden önce kaldırmalısınız.

Merhaba toocheck hello sürümü PowerShell yüklü:

    Get-Module *azure*

toouninstall hello eski sürümü, hello Denetim Masası'ndaki Programlar ve Özellikler çalıştırın.

## <a name="create-clusters"></a>Küme oluşturma
Bkz: [Azure PowerShell kullanarak Hdınsight oluşturma Linux tabanlı kümelerde](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)

## <a name="list-clusters"></a>Liste kümeleri
Komut toolist aşağıdaki hello tüm kümelerin hello geçerli abonelikte kullanın:

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a>Küme Göster
Aşağıdaki komut tooshow ayrıntılara hello geçerli abonelikte belirli bir kümenin hello kullan:

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a>Küme silme
Komut toodelete bir küme aşağıdaki hello kullan:

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

Merhaba küme içeren hello kaynak grubunu kaldırarak bir küme de silebilirsiniz. Lütfen unutmayın, bu hello varsayılan depolama hesabı dahil olmak üzere hello grubundaki tüm hello kaynaklarını siler.

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a>Kümeleri ölçeklendirme
özellik ölçeklendirme hello küme toochange hello Azure Hdınsight'ta toore gerek kalmadan çalışan bir küme tarafından kullanılan çalışan düğüm sayısı sağlar-hello kümesi oluşturun.

> [!NOTE]
> Yalnızca, Hdınsight sürüm 3.1.3 ile kümeleri veya üzeri desteklenir. Kümenizin hello sürümü değilseniz hello özellikler sayfasını kontrol edebilirsiniz.  Bkz: [listesi ve Göster kümeleri](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
>
>

hello etkisini, her tür Hdınsight tarafından desteklenen küme için veri düğümünün hello numarasını değiştirmek için:

* Hadoop

    Sorunsuz bir şekilde hello tüm bekleyen veya çalışan işler etkilemeden çalıştıran bir Hadoop kümesinde çalışan düğümü sayısını da artırabilirsiniz. Merhaba işlemi devam ederken yeni işleri da gönderilebilir. Böylece Hello küme her zaman işlevsel bir durumda bırakılır bir ölçeklendirme işlemi hatalar düzgün bir şekilde ele alınır.

    Bir Hadoop kümesine veri düğümlerini hello sayısını azaltarak ölçeklendirilir, bazı hello kümedeki hello hizmetleri yeniden başlatılır. Bu, tüm çalışan ve işleri toofail hello tamamlanma işlemi ölçeklendirme Merhaba, bekleyen neden olur. Hello işlemi tamamlandıktan sonra ancak, hello sunmaları olabilir.
* HBase

    Sorunsuz bir şekilde ekleme veya düğümleri tooyour HBase kümesi çalışırken kaldırın. Bölgesel sunucuları işlemi ölçeklendirme hello tamamladıktan birkaç dakika içinde otomatik olarak dengeli. Ancak, küme ve komutlar bir komut istemi penceresinden aşağıdaki çalışan hello toohello headnode oturum açarak hello bölgesel sunucular el ile de dengeleyebilirsiniz:

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* Storm

    Sorunsuz bir şekilde ekleyebilir veya çalışırken veri düğümleri tooyour Storm kümesi kaldırabilirsiniz. Ancak hello ölçekleme işlemi başarıyla tamamlandıktan sonra toorebalance hello topoloji gerekir.

    İki yolla yeniden dengelenmesi gerçekleştirilebilir:

  * Storm web kullanıcı Arabirimi
  * Komut satırı arabirimi (CLI) aracı

    Lütfen toohello bakın [Apache Storm belgelerine](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) daha fazla ayrıntı için.

    Merhaba Storm web kullanıcı Arabirimi hello Hdınsight kümesinde kullanılabilir:

    ![Hdınsight storm ölçek yeniden dengeleyin](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    Örneği nasıl toouse hello CLI komutu toorebalance hello Storm topolojisini:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

toochange hello bir istemci makinesinden komutu aşağıdaki hello çalıştırmak, Azure PowerShell kullanarak Hadoop küme boyutu:

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a>GRANT/revoke erişim
Hdınsight kümeleri HTTP web Hizmetleri (Bu hizmetlerin tümü için RESTful uç noktaları vardır) aşağıdaki hello vardır:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Varsayılan olarak, bu hizmetleri için erişim verilir. İptal etme/hello erişim izninin. toorevoke:

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

toogrant:

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter hello Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter hello HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> Verme/hello erişimi iptal ederek, hello küme kullanıcı adı ve parola sıfırlanır.
>
>

Bu ayrıca hello Portal yapılabilir. Bkz: [kullanarak Hdınsight yönetmek hello Azure portal][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>HTTP kullanıcı kimlik bilgilerini güncelleştirin
Aynı hello olan yordamı [Grant/revoke HTTP erişimi](#grant/revoke-access). Merhaba küme hello HTTP erişim verilmişse, öncelikle iptal gerekir.  Ve ardından yeni HTTP kullanıcı kimlik bilgileriyle hello erişim verin.

## <a name="find-hello-default-storage-account"></a>Merhaba varsayılan depolama hesabı bulunamadı
PowerShell Betiği aşağıdaki hello nasıl tooget varsayılan depolama hesabı adı hello ve küme için varsayılan depolama hesabı anahtarı hello gösterir.

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a>Merhaba kaynak grup bulunamıyor
Merhaba Kaynak Yöneticisi modunda tooan Azure kaynak grubu her Hdınsight kümesine ait.  toofind hello kaynak grubu:

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a>İşlerini gönderme
**toosubmit MapReduce işleri**

Bkz: [Windows tabanlı Hdınsight Hadoop MapReduce çalıştırma örnekleri](hdinsight-run-samples.md).

**toosubmit Hive işleri**

Bkz: [PowerShell kullanarak Hive sorgularını çalıştırma](hdinsight-hadoop-use-hive-powershell.md).

**toosubmit Pig işleri**

Bkz: [çalıştırmak Pig işleri PowerShell kullanarak](hdinsight-hadoop-use-pig-powershell.md).

**toosubmit Sqoop işleri**

Bkz: [Hdınsight ile Sqoop kullanma](hdinsight-use-sqoop.md).

**toosubmit Oozie işleri**

Bkz: [Hadoop toodefine ve çalışma Hdınsight bir iş akışında kullanmak Oozie](hdinsight-use-oozie.md).

## <a name="upload-data-tooazure-blob-storage"></a>Veri tooAzure Blob Depolama yükleme
Bkz: [karşıya veri tooHDInsight][hdinsight-upload-data].

## <a name="see-also"></a>Ayrıca Bkz.
* [Hdınsight cmdlet başvuru belgeleri][hdinsight-powershell-reference]
* [Hdınsight hello Azure portal kullanarak yönetme][hdinsight-admin-portal]
* [Bir komut satırı arabirimi kullanarak Hdınsight yönetme][hdinsight-admin-cli]
* [Hdınsight kümeleri oluşturma][hdinsight-provision]
* [Veri tooHDInsight karşıya yükle][hdinsight-upload-data]
* [Hadoop işlerini programlı olarak gönderme][hdinsight-submit-jobs]
* [Azure HDInsight'ı Kullanmaya Başlama][hdinsight-get-started]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-ps-provision]: ./media/hdinsight-administer-use-powershell/HDI.PS.Provision.png
