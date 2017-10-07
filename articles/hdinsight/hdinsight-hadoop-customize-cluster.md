---
title: "komut dosyası Eylemler - Azure Hdınsight kümeleri aaaCustomize kullanarak | Microsoft Docs"
description: "Betik eylemi kullanarak nasıl toocustomize Hdınsight kümeleri hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a>Betik eylemi kullanarak Windows tabanlı Hdınsight kümelerini özelleştirme
**Betik eylemi** kullanılan tooinvoke olabilir [özel komut dosyaları](hdinsight-hadoop-script-actions.md) bir kümede ek yazılım yüklemek için hello küme oluşturma işlemi sırasında.

Bu makaledeki Hello bilgiler belirli tooWindows tabanlı Hdınsight kümeleri ' dir. Linux tabanlı kümeler için bkz: [özelleştirme Linux tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md).

> [!IMPORTANT]
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Hdınsight kümeleri dahil olmak üzere ek Azure depolama hesapları gibi başka yöntemlerle de, çeşitli özelleştirilebilir, hello Hadoop değiştirme yapılandırma dosyaları (core-site.xml, hive-site.xml, vb.) veya paylaşılan içine kitaplıklar (örn., Hive, Oozie) ekleme Merhaba küme ortak konumlarda. Bu özelleştirmeler hello Azure Hdınsight .NET SDK'sı, Azure PowerShell aracılığıyla yapılabilir veya Azure portal hello. Daha fazla bilgi için bkz: [Hdınsight'ta oluşturmak Hadoop kümeleri][hdinsight-provision-cluster].

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a>Betik eylemi hello küme oluşturma işlemi
Bir küme oluşturulmakta hello işlemi içinde iken betik eylemi yalnızca kullanılır. Betik eylemi hello oluşturma işlemi sırasında çalıştırıldığında hello Aşağıdaki diyagramda gösterilmektedir:

![Hdınsight küme özelleştirme ve küme oluşturma sırasında aşamaları][img-hdi-cluster-states]

Merhaba komut dosyası çalıştırılırken hello küme hello girer **ClusterCustomization** aşaması. Bu aşamada hello betik hello sistem yönetici hesabı altında çalışır, tüm hello üzerinde paralel hello kümedeki düğümler belirtilen ve hello düğümler üzerinde tam yönetici ayrıcalıkları sağlar.

> [!NOTE]
> Sırasında hello küme düğümleri üzerinde yönetici ayrıcalıklarına sahip olduğundan **ClusterCustomization** aşama, durdurma ve Hadoop ile ilgili hizmetlerin gibi hizmetler başlatma gibi hello betik tooperform işlemleri kullanabilir. Merhaba komut dosyasının bir parçası olarak emin olmalısınız, hello komut dosyası çalıştırma tamamlanmadan önce bu hello Ambari Hizmetleri ve diğer Hadoop ile ilgili hizmetlerin hazır ve çalışır; dolayısıyla. Bu hizmetler gerekli toosuccessfully, hello sağlık ve hello küme durumunu, oluşturulurken onaylaması. Bu hizmetler etkiler kümedeki herhangi bir yapılandırma değiştirirseniz, sağlanan hello yardımcı işlevleri kullanmanız gerekir. Yardımcı işlevleri hakkında daha fazla bilgi için bkz: [Hdınsight betik eylemi geliştirme betikleri][hdinsight-write-script].
>
>

Hello çıkış ve hello Hata günlüklerini hello komut dosyası için hello küme için belirtilen hello varsayılan depolama hesabında depolanır. Merhaba günlükleri hello adı olan bir tabloda depolanır **u < \cluster-name-fragment >< \time-stamp > setuplog**. Merhaba betiği tüm düğümlerde hello (baş düğüm ve çalışan düğümleri) hello küme Çalıştır toplama günlüklerinden bunlar.

Her küme belirtilen hello sırayla çağrılır birden çok betik eylemleri kabul edebilir. Bir komut dosyasını olması çalıştıran hello baş düğüm, hello çalışan düğümleri veya her ikisi de.

Hdınsight Hdınsight kümelerinde bileşenleri aşağıdaki birkaç betikleri tooinstall hello sağlar:

| Ad | Betik |
| --- | --- |
| **Spark yükleyin** |https://hdiconfigactions.BLOB.Core.Windows.NET/sparkconfigactionv03/Spark-installer-v03.ps1. Bkz: [yükleme ve kullanma hdınsight'ta Spark kümeleri][hdinsight-install-spark]. |
| **R yükleme** |https://hdiconfigactions.BLOB.Core.Windows.NET/rconfigactionv02/r-installer-v02.ps1. Bkz: [yükleme ve kullanma R Hdınsight kümelerinde][hdinsight-install-r]. |
| **Solr yükleyin** |https://hdiconfigactions.BLOB.Core.Windows.NET/solrconfigactionv01/solr-installer-v01.ps1. Bkz: [yükleme ve kullanma Solr hdınsight kümeleri](hdinsight-hadoop-solr-install.md). |
| - **Giraph yükleyin** |https://hdiconfigactions.BLOB.Core.Windows.NET/giraphconfigactionv01/giraph-installer-v01.ps1. Bkz: [yükleme ve kullanma Giraph hdınsight kümeleri](hdinsight-hadoop-giraph-install.md). |
| **Ön yük Hıve kitaplıkları** |https://hdiconfigactions.BLOB.Core.Windows.NET/setupcustomhivelibsv01/Setup-customhivelibs-v01.ps1. Bkz: [eklemek Hive kitaplıkları Hdınsight kümeleri hakkında](hdinsight-hadoop-add-hive-libraries.md) |

## <a name="call-scripts-using-hello-azure-portal"></a>Hello Azure portal kullanarak komut dosyalarını arayın
**Azure portal Hello**

1. Konusunda açıklandığı gibi bir küme oluşturmaya başlamak [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md).
2. Hello için isteğe bağlı yapılandırma bölümünde **betik eylemleri** dikey penceresinde tıklatın **betik eylemi eklemek** tooprovide aşağıda gösterildiği gibi hello betik eylemi hakkında ayrıntıları:

    ![Betik eylemi toocustomize bir küme kullanın](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "kullanım betik eylemi toocustomize küme")

    <table border='1'>
        <tr><th>Özellik</th><th>Değer</th></tr>
        <tr><td>Ad</td>
            <td>Merhaba betik eylemi için bir ad belirtin.</td></tr>
        <tr><td>Betik URI'si</td>
            <td>Çağrılan toocustomize hello küme hello URI toohello komut dosyasını belirtin. s</td></tr>
        <tr><td>HEAD/çalışan</td>
            <td>Merhaba düğüm belirtin (**Head** veya **çalışan**) hangi hello özelleştirme betiğini çalıştırın.</b>.
        <tr><td>Parametreler</td>
            <td>Merhaba komut dosyası için gereken Hello parametreleri belirtin.</td></tr>
    </table>

    Birden çok bileşeni tek bir betik eylemi tooinstall birden çok ENTER tooadd hello kümede tuşuna basın.
3. Tıklatın **seçin** toosave hello betik eylemi yapılandırmasını ve küme oluşturma ile devam edin.

## <a name="call-scripts-using-azure-powershell"></a>Azure PowerShell kullanarak komut dosyalarını arayın
Bu aşağıdaki PowerShell betiğini tooinstall Windows üzerinde Spark Hdınsight kümesi nasıl dayalı gösterir.  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


tooinstall diğer yazılım ihtiyacınız olacak hello betik tooreplace hello komut dosyası:

İstendiğinde, hello küme için hello kimlik bilgilerini girin. Merhaba küme oluşturulmadan önce birkaç dakika sürebilir.

## <a name="call-scripts-using-net-sdk"></a>.NET SDK kullanarak komut dosyalarını arayın
Merhaba aşağıdaki örnek tooinstall Windows üzerinde Spark Hdınsight kümesi nasıl dayalı gösterir. tooinstall diğer yazılım ihtiyacınız olacak hello kod tooreplace hello komut dosyası.

**toocreate Spark Hdınsight kümesiyle**

1. Visual Studio'da bir C# konsol uygulaması oluşturun.
2. Hello ifadesini Nuget Paket Yöneticisi konsolu hello aşağıdaki komutu çalıştırın.

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. Using deyimleri hello Program.cs dosyasında aşağıdaki kullanım hello:

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. Merhaba kodu hello aşağıdaki hello sınıfıyla yerleştirin:

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
        /// <returns></returns>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/",
                ClientId,
                new Uri("urn:ietf:wg:oauth:2.0:oob"),
                PromptBehavior.Always,
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for hello Resource manager and set hello subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register hello HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. Tuşuna **F5** toorun Merhaba uygulaması.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>Hdınsight kümelerinde kullanılan açık kaynaklı yazılım desteği
Merhaba Microsoft Azure Hdınsight hizmeti bir ekosistemi Hadoop biçimlendirilmiş açık kaynak teknolojileri kullanarak toobuild büyük veri uygulamaları hello bulutta sağlayan esnek bir platformdur. Microsoft Azure hello açıklandığı gibi bu genel düzeyde bir destek açık kaynak teknolojileri için sağlar **destek kapsamı** hello bölümünü <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure destek SSS Web sitesine</a>. Merhaba Hdınsight hizmeti, aşağıda açıklandığı gibi ek düzeyde hello bileşenlerinin bazılarını desteği sağlar.

Merhaba Hdınsight hizmeti açık kaynak bileşenlerini iki tür vardır:

* **Yerleşik bileşenlerini** -bu bileşenler Hdınsight kümelerinde önceden yüklenmiş ve hello küme çekirdek işlevselliğini sağlar. Örneğin, YARN ResourceManager, hello Hive sorgu dili (HiveQL) ve hello Mahout kitaplık toothis kategori ait. Küme bileşenlerin tam bir listesi kullanılabilir [Hdınsight tarafından sağlanan hello Hadoop küme sürümlerindeki yenilikler nelerdir?](hdinsight-component-versioning.md) </a>.
* **Özel bileşenler** -, hello küme, bir kullanıcı olarak yükleyebilir veya herhangi bir bileşeni hello topluluk bulunan ya da sizin tarafınızdan oluşturulan, iş yükü kullanın.

Yerleşik bileşenlerini tam olarak desteklenir ve Microsoft Support tooisolate Yardım ve sorunları ilgili toothese bileşenler çözümlenemiyor.

> [!WARNING]
> Merhaba Hdınsight kümesi ile sağlanan bileşenler tam olarak desteklenir ve Microsoft Support tooisolate Yardım ve sorunları ilgili toothese bileşenler çözümlenemiyor.
>
> Özel bileşenlerini almak ticari koşulların elverdiği oranda makul destek toohelp, toofurther hello sorun giderme. Merhaba sorunu çözmek veya tooengage kullanılabilir kanalları hello için bu teknoloji derin uzmanlık bulunduğu kaynak teknolojileri açtığınız isteyen neden olabilir. Örneğin, olduğu gibi kullanılabilecek birçok topluluk siteleri vardır: [Hdınsight için MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Apache projeleri proje siteleri de [http://apache.org](http://apache.org), örneğin: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).
>
>

Merhaba Hdınsight hizmeti toouse özel bileşenleri çeşitli yöntemler sağlar. Nasıl bir bileşeni kullanılan veya hello kümeye yüklü bağımsız olarak, hello aynı düzeyde desteği için geçerlidir. Özel bileşenler Hdınsight kümelerinde kullanılabilir hello en yaygın şekilde listesi aşağıdadır:

1. İş gönderme - Hadoop veya diğer tür execute veya özel bileşenleri kullanan işi gönderilen toohello kümesi olabilir.
2. Küme özelleştirme - küme oluşturma sırasında ek ayarlar ve hello küme düğümlerinde yüklü özel bileşenleri belirtebilirsiniz.
3. Örnekler - popüler özel bileşenleri, Microsoft ve diğerleri için bu bileşenlerin hello Hdınsight kümelerinde nasıl kullanılabileceğini örnek sağlayabilir. Bu örnekler desteği olmadan sağlanır.

## <a name="develop-script-action-scripts"></a>Betik eylemi betikleri geliştirme
Bkz: [Hdınsight betik eylemi geliştirme betikleri][hdinsight-write-script].

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
