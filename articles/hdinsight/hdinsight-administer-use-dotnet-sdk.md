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
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="88de3-103">.NET SDK kullanarak hdınsight'ta Hadoop kümelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="88de3-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="88de3-104">Kullanarak nasıl toomanage Hdınsight kümeleri öğrenin [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="88de3-104">Learn how toomanage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="88de3-105">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="88de3-105">**Prerequisites**</span></span>

<span data-ttu-id="88de3-106">Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="88de3-106">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="88de3-107">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="88de3-107">**An Azure subscription**.</span></span> <span data-ttu-id="88de3-108">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="88de3-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-tooazure-hdinsight"></a><span data-ttu-id="88de3-109">TooAzure Hdınsight Bağlan</span><span class="sxs-lookup"><span data-stu-id="88de3-109">Connect tooAzure HDInsight</span></span>

<span data-ttu-id="88de3-110">Nuget paketleri aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="88de3-110">You need hello following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="88de3-111">Merhaba aşağıdaki kod örneği, nasıl Azure aboneliğinizde Hdınsight yönetebilmeniz için önce tooconnect tooAzure kümeleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="88de3-111">hello following code sample shows you how tooconnect tooAzure before you can administer HDInsight clusters under your Azure subscription.</span></span>

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

<span data-ttu-id="88de3-112">Bu programı çalıştırdığınızda bir istem göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="88de3-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="88de3-113">Toosee hello istemi istemiyorsanız, bkz: [etkileşimli olmayan kimlik doğrulama .NET Hdınsight uygulamaları oluşturma](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="88de3-113">If you don't want toosee hello prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="88de3-114">Küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="88de3-114">Create clusters</span></span>
<span data-ttu-id="88de3-115">Bkz: [kullanarak Hdınsight'ta oluşturma Linux tabanlı kümelerde hello .NET SDK'sı](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="88de3-115">See [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="88de3-116">Liste kümeleri</span><span class="sxs-lookup"><span data-stu-id="88de3-116">List clusters</span></span>
<span data-ttu-id="88de3-117">Merhaba aşağıdaki kod parçacığını kümeleri ve bazı özellikler listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="88de3-117">hello following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="88de3-118">Küme silme</span><span class="sxs-lookup"><span data-stu-id="88de3-118">Delete clusters</span></span>
<span data-ttu-id="88de3-119">Kod parçacığı toodelete bir küme eşzamanlı veya zaman uyumsuz olarak aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="88de3-119">Use hello following code snippet toodelete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="88de3-120">Kümeleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="88de3-120">Scale clusters</span></span>
<span data-ttu-id="88de3-121">özellik ölçeklendirme hello küme toochange hello Azure Hdınsight'ta toore gerek kalmadan çalışan bir küme tarafından kullanılan çalışan düğüm sayısı sağlar-hello kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="88de3-121">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="88de3-122">Yalnızca, Hdınsight sürüm 3.1.3 ile kümeleri veya üzeri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="88de3-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="88de3-123">Kümenizin hello sürümü değilseniz hello özellikler sayfasını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88de3-123">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="88de3-124">Bkz: [listesi ve Göster kümeleri](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="88de3-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="88de3-125">hello etkisini, her tür Hdınsight tarafından desteklenen küme için veri düğümünün hello numarasını değiştirmek için:</span><span class="sxs-lookup"><span data-stu-id="88de3-125">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="88de3-126">Hadoop</span><span class="sxs-lookup"><span data-stu-id="88de3-126">Hadoop</span></span>
  
    <span data-ttu-id="88de3-127">Sorunsuz bir şekilde hello tüm bekleyen veya çalışan işler etkilemeden çalıştıran bir Hadoop kümesinde çalışan düğümü sayısını da artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88de3-127">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="88de3-128">Merhaba işlemi devam ederken yeni işleri da gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="88de3-128">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="88de3-129">Böylece Hello küme her zaman işlevsel bir durumda bırakılır bir ölçeklendirme işlemi hatalar düzgün bir şekilde ele alınır.</span><span class="sxs-lookup"><span data-stu-id="88de3-129">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="88de3-130">Bir Hadoop kümesine veri düğümlerini hello sayısını azaltarak ölçeklendirilir, bazı hello kümedeki hello hizmetleri yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="88de3-130">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="88de3-131">Bu, tüm çalışan ve işleri toofail hello tamamlanma işlemi ölçeklendirme Merhaba, bekleyen neden olur.</span><span class="sxs-lookup"><span data-stu-id="88de3-131">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="88de3-132">Hello işlemi tamamlandıktan sonra ancak, hello sunmaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="88de3-132">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="88de3-133">HBase</span><span class="sxs-lookup"><span data-stu-id="88de3-133">HBase</span></span>
  
    <span data-ttu-id="88de3-134">Sorunsuz bir şekilde ekleme veya düğümleri tooyour HBase kümesi çalışırken kaldırın.</span><span class="sxs-lookup"><span data-stu-id="88de3-134">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="88de3-135">Bölgesel sunucuları işlemi ölçeklendirme hello tamamladıktan birkaç dakika içinde otomatik olarak dengeli.</span><span class="sxs-lookup"><span data-stu-id="88de3-135">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="88de3-136">Ancak, küme ve komutlar bir komut istemi penceresinden aşağıdaki çalışan hello hello headnode açarak el ile de hello bölgesel sunucular dengeleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="88de3-136">However, you can also manually balance hello regional servers by logging into hello headnode of cluster and running hello following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="88de3-137">Storm</span><span class="sxs-lookup"><span data-stu-id="88de3-137">Storm</span></span>
  
    <span data-ttu-id="88de3-138">Sorunsuz bir şekilde ekleyebilir veya çalışırken veri düğümleri tooyour Storm kümesi kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88de3-138">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="88de3-139">Ancak hello ölçekleme işlemi başarıyla tamamlandıktan sonra toorebalance hello topoloji gerekir.</span><span class="sxs-lookup"><span data-stu-id="88de3-139">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>
  
    <span data-ttu-id="88de3-140">İki yolla yeniden dengelenmesi gerçekleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="88de3-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="88de3-141">Storm web kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="88de3-141">Storm web UI</span></span>
  * <span data-ttu-id="88de3-142">Komut satırı arabirimi (CLI) aracı</span><span class="sxs-lookup"><span data-stu-id="88de3-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="88de3-143">Lütfen toohello bakın [Apache Storm belgelerine](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="88de3-143">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="88de3-144">Merhaba Storm web kullanıcı Arabirimi hello Hdınsight kümesinde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="88de3-144">hello Storm web UI is available on hello HDInsight cluster:</span></span>
    
    ![Hdınsight Storm ölçek yeniden dengeleyin](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    <span data-ttu-id="88de3-146">Örneği nasıl toouse hello CLI komutu toorebalance hello Storm topolojisini:</span><span class="sxs-lookup"><span data-stu-id="88de3-146">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>
    
        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="88de3-147">kod parçacığı gösterir nasıl aşağıdaki hello tooresize bir küme eşzamanlı veya zaman uyumsuz olarak:</span><span class="sxs-lookup"><span data-stu-id="88de3-147">hello following code snippet shows how tooresize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="88de3-148">GRANT/revoke erişim</span><span class="sxs-lookup"><span data-stu-id="88de3-148">Grant/revoke access</span></span>
<span data-ttu-id="88de3-149">Hdınsight kümeleri HTTP web Hizmetleri (Bu hizmetlerin tümü için RESTful uç noktaları vardır) aşağıdaki hello vardır:</span><span class="sxs-lookup"><span data-stu-id="88de3-149">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="88de3-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="88de3-150">ODBC</span></span>
* <span data-ttu-id="88de3-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="88de3-151">JDBC</span></span>
* <span data-ttu-id="88de3-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="88de3-152">Ambari</span></span>
* <span data-ttu-id="88de3-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="88de3-153">Oozie</span></span>
* <span data-ttu-id="88de3-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="88de3-154">Templeton</span></span>

<span data-ttu-id="88de3-155">Varsayılan olarak, bu hizmetleri için erişim verilir.</span><span class="sxs-lookup"><span data-stu-id="88de3-155">By default, these services are granted for access.</span></span> <span data-ttu-id="88de3-156">İptal etme/hello erişim izninin.</span><span class="sxs-lookup"><span data-stu-id="88de3-156">You can revoke/grant hello access.</span></span> <span data-ttu-id="88de3-157">toorevoke:</span><span class="sxs-lookup"><span data-stu-id="88de3-157">toorevoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="88de3-158">toogrant:</span><span class="sxs-lookup"><span data-stu-id="88de3-158">toogrant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="88de3-159">Verme/hello erişimi iptal ederek, hello küme kullanıcı adı ve parola sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="88de3-159">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="88de3-160">Bu ayrıca hello Portal yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="88de3-160">This can also be done via hello Portal.</span></span> <span data-ttu-id="88de3-161">Bkz: [kullanarak Hdınsight yönetmek hello Azure portal][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="88de3-161">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="88de3-162">HTTP kullanıcı kimlik bilgilerini güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="88de3-162">Update HTTP user credentials</span></span>
<span data-ttu-id="88de3-163">Aynı hello olan yordamı [Grant/revoke HTTP erişimi](#grant/revoke-access). Merhaba küme hello HTTP erişim verilmişse, öncelikle iptal gerekir.</span><span class="sxs-lookup"><span data-stu-id="88de3-163">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="88de3-164">Ve ardından yeni HTTP kullanıcı kimlik bilgileriyle hello erişim verin.</span><span class="sxs-lookup"><span data-stu-id="88de3-164">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="88de3-165">Merhaba varsayılan depolama hesabı bulunamadı</span><span class="sxs-lookup"><span data-stu-id="88de3-165">Find hello default storage account</span></span>
<span data-ttu-id="88de3-166">Aşağıdaki kod parçacığını hello nasıl tooget varsayılan depolama hesabı adı hello ve küme için varsayılan depolama hesabı anahtarı hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="88de3-166">hello following code snippet demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="88de3-167">İşlerini gönderme</span><span class="sxs-lookup"><span data-stu-id="88de3-167">Submit jobs</span></span>
<span data-ttu-id="88de3-168">**toosubmit MapReduce işleri**</span><span class="sxs-lookup"><span data-stu-id="88de3-168">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="88de3-169">Bkz: [hdınsight'ta Hadoop MapReduce çalıştırma örnekleri](hdinsight-hadoop-run-samples-linux.md).</span><span class="sxs-lookup"><span data-stu-id="88de3-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="88de3-170">**toosubmit Hive işleri**</span><span class="sxs-lookup"><span data-stu-id="88de3-170">**toosubmit Hive jobs**</span></span> 

<span data-ttu-id="88de3-171">Bkz: [.NET SDK kullanarak Hive sorgularını çalıştırma](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="88de3-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="88de3-172">**toosubmit Pig işleri**</span><span class="sxs-lookup"><span data-stu-id="88de3-172">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="88de3-173">Bkz: [.NET SDK kullanarak çalıştırmak Pig işleri](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="88de3-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="88de3-174">**toosubmit Sqoop işleri**</span><span class="sxs-lookup"><span data-stu-id="88de3-174">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="88de3-175">Bkz: [Hdınsight ile Sqoop kullanma](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="88de3-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="88de3-176">**toosubmit Oozie işleri**</span><span class="sxs-lookup"><span data-stu-id="88de3-176">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="88de3-177">Bkz: [Hadoop toodefine ve çalışma Hdınsight bir iş akışında kullanmak Oozie](hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="88de3-177">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="88de3-178">Veri tooAzure Blob Depolama yükleme</span><span class="sxs-lookup"><span data-stu-id="88de3-178">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="88de3-179">Bkz: [karşıya veri tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="88de3-179">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="88de3-180">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="88de3-180">See Also</span></span>
* [<span data-ttu-id="88de3-181">Hdınsight .NET SDK'sı başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="88de3-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="88de3-182">[Hdınsight hello Azure portal kullanarak yönetme][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="88de3-182">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="88de3-183">[Bir komut satırı arabirimi kullanarak Hdınsight yönetme][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="88de3-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="88de3-184">[Hdınsight kümeleri oluşturma][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="88de3-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="88de3-185">[Veri tooHDInsight karşıya yükle][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="88de3-185">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="88de3-186">[Azure HDInsight'ı Kullanmaya Başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="88de3-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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


