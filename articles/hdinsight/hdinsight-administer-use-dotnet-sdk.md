---
title: "aaaManage Hadoop kümeleri - Azure .NET SDK'sı hdınsight'ta | Microsoft Docs"
description: "Yönetim tooperform Merhaba Hdınsight .NET SDK kullanarak hdınsight'ta Hadoop kümelerinin nasıl görevleri öğrenin."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: fd134765-c2a0-488a-bca6-184d814d78e9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d8bbf966b7eba3e943dfb2f764d15d8e52b9be71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a>.NET SDK kullanarak hdınsight'ta Hadoop kümelerini yönetme
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Kullanarak nasıl toomanage Hdınsight kümeleri öğrenin [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).

**Önkoşullar**

Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="connect-tooazure-hdinsight"></a>TooAzure Hdınsight Bağlan

Nuget paketleri aşağıdaki hello gerekir:

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

Merhaba aşağıdaki kod örneği, nasıl Azure aboneliğinizde Hdınsight yönetebilmeniz için önce tooconnect tooAzure kümeleri gösterir.

    using System;
    using Microsoft.Azure;
    using Microsoft.Azure.Management.HDInsight;
    using Microsoft.Azure.Management.HDInsight.Models;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    using Microsoft.Rest.Azure.Authentication;

    namespace HDInsightManagement
    {
        class Program
        {
            private static HDInsightManagementClient _hdiManagementClient;
            // Replace with your AAD tenant ID if necessary
            private const string TenantId = UserTokenProvider.CommonTenantId; 
            private const string SubscriptionId = "<Your Azure Subscription ID>";
            // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
            private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";

            static void Main(string[] args)
            {
                // Authenticate and get a token
                var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
                // Flag subscription for HDInsight, if it isn't already.
                EnableHDInsight(authToken);
                // Get an HDInsight management client
                _hdiManagementClient = new HDInsightManagementClient(authToken);

                // insert code here

                System.Console.WriteLine("Press ENTER toocontinue");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate tooan Azure subscription and retrieve an authentication token
            /// </summary>
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
        }
    }

Bu programı çalıştırdığınızda bir istem göreceksiniz.  Toosee hello istemi istemiyorsanız, bkz: [etkileşimli olmayan kimlik doğrulama .NET Hdınsight uygulamaları oluşturma](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

## <a name="create-clusters"></a>Küme oluşturma
Bkz: [kullanarak Hdınsight'ta oluşturma Linux tabanlı kümelerde hello .NET SDK'sı](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)

## <a name="list-clusters"></a>Liste kümeleri
Merhaba aşağıdaki kod parçacığını kümeleri ve bazı özellikler listelenmektedir:

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a>Küme silme
Kod parçacığı toodelete bir küme eşzamanlı veya zaman uyumsuz olarak aşağıdaki hello kullan: 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

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
  
    Sorunsuz bir şekilde ekleme veya düğümleri tooyour HBase kümesi çalışırken kaldırın. Bölgesel sunucuları işlemi ölçeklendirme hello tamamladıktan birkaç dakika içinde otomatik olarak dengeli. Ancak, küme ve komutlar bir komut istemi penceresinden aşağıdaki çalışan hello hello headnode açarak el ile de hello bölgesel sunucular dengeleyebilirsiniz:
  
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
    
    ![Hdınsight Storm ölçek yeniden dengeleyin](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    Örneği nasıl toouse hello CLI komutu toorebalance hello Storm topolojisini:
    
        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

kod parçacığı gösterir nasıl aşağıdaki hello tooresize bir küme eşzamanlı veya zaman uyumsuz olarak:

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a>GRANT/revoke erişim
Hdınsight kümeleri HTTP web Hizmetleri (Bu hizmetlerin tümü için RESTful uç noktaları vardır) aşağıdaki hello vardır:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Varsayılan olarak, bu hizmetleri için erişim verilir. İptal etme/hello erişim izninin. toorevoke:

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

toogrant:

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> Verme/hello erişimi iptal ederek, hello küme kullanıcı adı ve parola sıfırlanır.
> 
> 

Bu ayrıca hello Portal yapılabilir. Bkz: [kullanarak Hdınsight yönetmek hello Azure portal][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>HTTP kullanıcı kimlik bilgilerini güncelleştirin
Aynı hello olan yordamı [Grant/revoke HTTP erişimi](#grant/revoke-access). Merhaba küme hello HTTP erişim verilmişse, öncelikle iptal gerekir.  Ve ardından yeni HTTP kullanıcı kimlik bilgileriyle hello erişim verin.

## <a name="find-hello-default-storage-account"></a>Merhaba varsayılan depolama hesabı bulunamadı
Aşağıdaki kod parçacığını hello nasıl tooget varsayılan depolama hesabı adı hello ve küme için varsayılan depolama hesabı anahtarı hello gösterir.

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a>İşlerini gönderme
**toosubmit MapReduce işleri**

Bkz: [hdınsight'ta Hadoop MapReduce çalıştırma örnekleri](hdinsight-hadoop-run-samples-linux.md).

**toosubmit Hive işleri** 

Bkz: [.NET SDK kullanarak Hive sorgularını çalıştırma](hdinsight-hadoop-use-hive-dotnet-sdk.md).

**toosubmit Pig işleri**

Bkz: [.NET SDK kullanarak çalıştırmak Pig işleri](hdinsight-hadoop-use-pig-dotnet-sdk.md).

**toosubmit Sqoop işleri**

Bkz: [Hdınsight ile Sqoop kullanma](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).

**toosubmit Oozie işleri**

Bkz: [Hadoop toodefine ve çalışma Hdınsight bir iş akışında kullanmak Oozie](hdinsight-use-oozie-linux-mac.md).

## <a name="upload-data-tooazure-blob-storage"></a>Veri tooAzure Blob Depolama yükleme
Bkz: [karşıya veri tooHDInsight][hdinsight-upload-data].

## <a name="see-also"></a>Ayrıca Bkz.
* [Hdınsight .NET SDK'sı başvuru belgeleri](https://msdn.microsoft.com/library/mt271028.aspx)
* [Hdınsight hello Azure portal kullanarak yönetme][hdinsight-admin-portal]
* [Bir komut satırı arabirimi kullanarak Hdınsight yönetme][hdinsight-admin-cli]
* [Hdınsight kümeleri oluşturma][hdinsight-provision]
* [Veri tooHDInsight karşıya yükle][hdinsight-upload-data]
* [Azure HDInsight'ı Kullanmaya Başlama][hdinsight-get-started]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-portal-linux.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md


