---
title: "aaaCustomize kullanarak önyükleme - Azure Hdınsight kümeleri | Microsoft Docs"
description: "Önyükleme kullanarak nasıl toocustomize Hdınsight kümeleri hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ab2ebf0c-e961-4e95-8151-9724ee22d769
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 0029680fd1aa0e9e6aa9cdf667256c31b7ddc565
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hdinsight-clusters-using-bootstrap"></a>Önyükleme kullanarak Hdınsight kümelerini özelleştirme

Bazı durumlarda, dahil tooconfigure hello yapılandırma dosyalarını istiyor:

* clusterIdentity.xml
* Core-site.xml
* Gateway.XML
* hbase env.xml
* hbase-site.xml
* hdfs-site.xml
* Hive env.xml
* Hive-site.xml
* mapred site
* oozie-site.xml
* oozie env.xml
* Storm-site.xml
* Tez-site.xml
* webhcat-site.xml
* yarn-site.xml

Önyükleme üç yöntem toouse vardır:

* Azure PowerShell kullanma
* .NET SDK kullanma
* Azure Resource Manager şablonu kullanma

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

Ek bileşenler Hdınsight kümesinde hello oluşturulma zamanı sırasında yükleme hakkında daha fazla bilgi için bkz:

* [Betik eylemi (Linux) kullanarak Hdınsight kümelerini özelleştirme](hdinsight-hadoop-customize-cluster-linux.md)

## <a name="use-azure-powershell"></a>Azure PowerShell kullanma
PowerShell koddan hello Hive yapılandırmasını özelleştirir:

    # hive-site.xml configuration
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $existingResourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $clusterSizeInNodes `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -Config $config 

Tam çalışan bir PowerShell Betiği bulunabilir [ek A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample).

**tooverify hello değiştirin:**

1. Toohello üzerinde oturum [Azure portal](https://portal.azure.com).
2. Merhaba sol menüden **Hdınsight kümeleri**. Göremiyorsanız, tıklatın **daha fazla hizmet** ilk.
3. Merhaba PowerShell Betiği kullanılarak oluşturduğunuz hello kümesine tıklayın.
4. Tıklatın **Pano** Ambari UI hello dikey tooopen hello üstten hello.
5. Tıklatın **Hive** hello sol menüden.
6. Tıklatın **HiveServer2** gelen **Özet**.
7. Merhaba tıklatın **yapılandırmalar** sekmesi.
8. Tıklatın **Hive** hello sol menüden.
9. Merhaba tıklatın **Gelişmiş** sekmesi.
10. Aşağı kaydırın ve ardından **hive site Gelişmiş**.
11. Ara **hive.metastore.client.socket.timeout** hello bölümünde.

Diğer yapılandırma dosyalarını özelleştirme hakkında daha fazla bazı örnekler:

    # hdfs-site.xml configuration
    $HdfsConfigValues = @{ "dfs.blocksize"="64m" } #default is 128MB in HDI 3.0 and 256MB in HDI 2.1

    # core-site.xml configuration
    $CoreConfigValues = @{ "ipc.client.connect.max.retries"="60" } #default 50

    # mapred-site.xml configuration
    $MapRedConfigValues = @{ "mapreduce.task.timeout"="1200000" } #default 600000

    # oozie-site.xml configuration
    $OozieConfigValues = @{ "oozie.service.coord.normal.default.timeout"="150" }  # default 120

Daha fazla bilgi için bkz: başlıklı Azim Uddin'ın blog [özelleştirme Hdınsight kümesi oluşturma](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx).

## <a name="use-net-sdk"></a>.NET SDK kullanma
Bkz: [.NET SDK kullanarak Hdınsight'ta oluşturma Linux tabanlı kümelerde hello](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).

## <a name="use-resource-manager-template"></a>Kullanım Resource Manager şablonu
Resource Manager şablonunda önyükleme kullanabilirsiniz:

    "configurations": {
        …
        "hive-site": {
            "hive.metastore.client.connect.retry.delay": "5",
            "hive.execution.engine": "mr",
            "hive.security.authorization.manager": "org.apache.hadoop.hive.ql.security.authorization.DefaultHiveAuthorizationProvider"
        }
    }


![Hdınsight Hadoop kümesi önyükleme Azure Resource Manager şablonu özelleştirir](./media/hdinsight-hadoop-customize-cluster-bootstrap/hdinsight-customize-cluster-bootstrap-arm.png)

## <a name="see-also"></a>Ayrıca bkz.
* [Hdınsight'ta Hadoop kümeleri oluşturma] [ hdinsight-provision-cluster] nasıl toocreate bir Hdınsight küme diğer özel seçenekleri kullanarak yönergeler sağlar.
* [Hdınsight için betik eylemi betikleri geliştirme][hdinsight-write-script]
* [Yükleme ve Spark Hdınsight kümelerinde kullanma][hdinsight-install-spark]
* [Yükleme ve Hdınsight kümelerinde R kullanma][hdinsight-install-r]
* [Yükleme ve Hdınsight kümelerinde Solr kullanma](hdinsight-hadoop-solr-install.md).
* [Yükleme ve Hdınsight kümelerinde Giraph kullanma](hdinsight-hadoop-giraph-install.md).

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Küme oluşturma sırasında aşamaları"

## <a name="appx-a-powershell-sample"></a>Appx A: PowerShell örnek
Bu PowerShell Betiği Hdınsight kümesi oluşturur ve Hive ayarı özelleştirir:

    ####################################
    # Set these variables
    ####################################
    #region - used for creating Azure service names
    $nameToken = "<ENTER AN ALIAS>" 
    #endregion

    #region - cluster user accounts
    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"

    $sshUserName = "sshuser" #HDInsight ssh user name
    $sshPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"
    #endregion

    ####################################
    # Service names and varialbes
    ####################################
    #region - service names
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    $location = "East US 2"
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    ####################################
    # Connect tooAzure
    ####################################
    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create an HDInsight cluster
    ####################################
    # Create dependent components
    ####################################
    Write-Host "Creating a resource group ..." -ForegroundColor Green
    New-AzureRmResourceGroup `
        -Name  $resourceGroupName `
        -Location $location

    Write-Host "Creating hello default storage account and default blob container ..."  -ForegroundColor Green
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS

    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageContext #use hello cluster name as hello container name

    ####################################
    # Create a configuration object
    ####################################
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    ####################################
    # Create an HDInsight cluster
    ####################################
    $httpPW = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$httpPW)

    $sshPW = ConvertTo-SecureString -String $sshPassword -AsPlainText -Force
    $sshCredential = New-Object System.Management.Automation.PSCredential($sshUserName,$sshPW)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -Location $location `
        -ClusterSizeInNodes 1 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -SshCredential $sshCredential `
        -Config $config

    ####################################
    # Verify hello cluster
    ####################################
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName

    #endregion
