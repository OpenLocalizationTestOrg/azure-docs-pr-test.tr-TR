---
title: ".NET SDK'sı - Azure hdınsight'ta Hadoop kümelerini yönetme | Microsoft Docs"
description: "Hdınsight .NET SDK kullanarak hdınsight'ta Hadoop kümeleri için yönetim görevlerini gerçekleştirmek öğrenin."
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
ms.openlocfilehash: c10471425fa1202ddb7fe35d0adf4ef33509f268
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="4b5ba-103">.NET SDK kullanarak hdınsight'ta Hadoop kümelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="4b5ba-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="4b5ba-104">Kullanarak Hdınsight kümelerini yönetme öğrenin [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="4b5ba-104">Learn how to manage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="4b5ba-105">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="4b5ba-105">**Prerequisites**</span></span>

<span data-ttu-id="4b5ba-106">Bu makaleye başlamadan önce aşağıdakilere sahip olmanız ve aşağıdaki işlemleri yapmış olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4b5ba-106">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="4b5ba-107">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-107">**An Azure subscription**.</span></span> <span data-ttu-id="4b5ba-108">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="4b5ba-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-to-azure-hdinsight"></a><span data-ttu-id="4b5ba-109">Azure Hdınsight Bağlan</span><span class="sxs-lookup"><span data-stu-id="4b5ba-109">Connect to Azure HDInsight</span></span>

<span data-ttu-id="4b5ba-110">Aşağıdaki Nuget paketlerini gerekir:</span><span class="sxs-lookup"><span data-stu-id="4b5ba-110">You need the following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="4b5ba-111">Aşağıdaki kod örneği, Azure aboneliğinizin altında Hdınsight kümeleri yönetebilmeniz için önce Azure'a bağlanmak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-111">The following code sample shows you how to connect to Azure before you can administer HDInsight clusters under your Azure subscription.</span></span>

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
            // This is the GUID for the PowerShell client. Used for interactive logins in this example.
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

                System.Console.WriteLine("Press ENTER to continue");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate to an Azure subscription and retrieve an authentication token
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
                // Create a client for the Resource manager and set the subscription ID
                var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
                resourceManagementClient.SubscriptionId = SubscriptionId;
                // Register the HDInsight provider
                var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
            }
        }
    }

<span data-ttu-id="4b5ba-112">Bu programı çalıştırdığınızda bir istem göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="4b5ba-113">İstemi görmek istemiyorsanız, bkz: [etkileşimli olmayan kimlik doğrulama .NET Hdınsight uygulamaları oluşturma](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="4b5ba-113">If you don't want to see the prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="4b5ba-114">Küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b5ba-114">Create clusters</span></span>
<span data-ttu-id="4b5ba-115">Bkz: [.NET SDK kullanarak Hdınsight oluşturma Linux tabanlı kümelerde](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="4b5ba-115">See [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="4b5ba-116">Liste kümeleri</span><span class="sxs-lookup"><span data-stu-id="4b5ba-116">List clusters</span></span>
<span data-ttu-id="4b5ba-117">Aşağıdaki kod parçacığını kümeleri ve bazı özellikler listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="4b5ba-117">The following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="4b5ba-118">Küme silme</span><span class="sxs-lookup"><span data-stu-id="4b5ba-118">Delete clusters</span></span>
<span data-ttu-id="4b5ba-119">Aşağıdaki kod parçacığını eşzamanlı veya zaman uyumsuz olarak bir küme silmek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="4b5ba-119">Use the following code snippet to delete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="4b5ba-120">Kümeleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="4b5ba-120">Scale clusters</span></span>
<span data-ttu-id="4b5ba-121">Özellik ölçeklendirme küme kümeye yeniden oluşturmak zorunda kalmadan Azure Hdınsight'ta çalıştıran bir küme tarafından kullanılan çalışan düğümü sayısını değiştirmenize izin verir.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-121">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="4b5ba-122">Yalnızca, Hdınsight sürüm 3.1.3 ile kümeleri veya üzeri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="4b5ba-123">Kümenizin sürümünü emin değilseniz, Özellikler sayfasını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-123">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="4b5ba-124">Bkz: [listesi ve Göster kümeleri](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="4b5ba-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="4b5ba-125">Her tür Hdınsight tarafından desteklenen küme için veri düğüm sayısını değiştirme etkisi:</span><span class="sxs-lookup"><span data-stu-id="4b5ba-125">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="4b5ba-126">Hadoop</span><span class="sxs-lookup"><span data-stu-id="4b5ba-126">Hadoop</span></span>
  
    <span data-ttu-id="4b5ba-127">Sorunsuz bir şekilde tüm bekleyen veya çalışan işler etkilemeden çalıştıran bir Hadoop kümesinde çalışan düğümü sayısını da artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-127">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="4b5ba-128">İşlemi devam ederken yeni işleri da gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-128">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="4b5ba-129">Kümenin her zaman işlevsel bir durumda bırakılır böylece bir ölçeklendirme işlemi hatalar düzgün bir şekilde ele alınır.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-129">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="4b5ba-130">Bir Hadoop kümesine veri düğüm sayısını azaltarak ölçeklendirilir, bazı kümedeki hizmetleri yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-130">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="4b5ba-131">Bu işleri bekleyen tüm çalışan ve ölçeklendirme işlemi tamamlandığında başarısız olmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-131">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="4b5ba-132">İşlemi tamamlandıktan sonra ancak, sunmaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-132">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="4b5ba-133">HBase</span><span class="sxs-lookup"><span data-stu-id="4b5ba-133">HBase</span></span>
  
    <span data-ttu-id="4b5ba-134">Sorunsuz bir şekilde ekleyebilir veya çalışırken, HBase kümesi düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-134">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="4b5ba-135">Bölgesel sunucular otomatik olarak ölçeklendirme işlemi tamamladıktan birkaç dakika içinde dengeli.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-135">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="4b5ba-136">Ancak, küme headnode günlüğe kaydetme ve bir komut istemi penceresinden aşağıdaki komutları çalıştırarak el ile de bölgesel sunucular dengeleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4b5ba-136">However, you can also manually balance the regional servers by logging into the headnode of cluster and running the following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="4b5ba-137">Storm</span><span class="sxs-lookup"><span data-stu-id="4b5ba-137">Storm</span></span>
  
    <span data-ttu-id="4b5ba-138">Sorunsuz bir şekilde ekleyebilir veya çalışırken Storm kümeniz veri düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-138">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="4b5ba-139">Ancak ölçeklendirme işlemi başarıyla tamamlandıktan sonra topoloji yeniden dengelemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-139">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>
  
    <span data-ttu-id="4b5ba-140">İki yolla yeniden dengelenmesi gerçekleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="4b5ba-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="4b5ba-141">Storm web kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="4b5ba-141">Storm web UI</span></span>
  * <span data-ttu-id="4b5ba-142">Komut satırı arabirimi (CLI) aracı</span><span class="sxs-lookup"><span data-stu-id="4b5ba-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="4b5ba-143">Lütfen [Apache Storm belgelerine](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-143">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="4b5ba-144">Hdınsight kümesinde Storm web kullanıcı Arabirimi kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="4b5ba-144">The Storm web UI is available on the HDInsight cluster:</span></span>
    
    ![Hdınsight Storm ölçek yeniden dengeleyin](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    <span data-ttu-id="4b5ba-146">Storm topolojisini yeniden dengelemeniz CLI komutunu kullanma örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="4b5ba-146">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>
    
        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="4b5ba-147">Aşağıdaki kod parçacığını bir küme eşzamanlı veya zaman uyumsuz olarak yeniden boyutlandırma gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="4b5ba-147">The following code snippet shows how to resize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="4b5ba-148">GRANT/revoke erişim</span><span class="sxs-lookup"><span data-stu-id="4b5ba-148">Grant/revoke access</span></span>
<span data-ttu-id="4b5ba-149">Hdınsight kümeleri (Bu hizmetlerin tümü için RESTful uç noktaları vardır) aşağıdaki HTTP web hizmetleri vardır:</span><span class="sxs-lookup"><span data-stu-id="4b5ba-149">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="4b5ba-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="4b5ba-150">ODBC</span></span>
* <span data-ttu-id="4b5ba-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="4b5ba-151">JDBC</span></span>
* <span data-ttu-id="4b5ba-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="4b5ba-152">Ambari</span></span>
* <span data-ttu-id="4b5ba-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="4b5ba-153">Oozie</span></span>
* <span data-ttu-id="4b5ba-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="4b5ba-154">Templeton</span></span>

<span data-ttu-id="4b5ba-155">Varsayılan olarak, bu hizmetleri için erişim verilir.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-155">By default, these services are granted for access.</span></span> <span data-ttu-id="4b5ba-156">İptal etme / erişim izninin.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-156">You can revoke/grant the access.</span></span> <span data-ttu-id="4b5ba-157">İptal etmek için:</span><span class="sxs-lookup"><span data-stu-id="4b5ba-157">To revoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="4b5ba-158">Vermek için:</span><span class="sxs-lookup"><span data-stu-id="4b5ba-158">To grant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="4b5ba-159">Verme/erişimi iptal ederek, küme kullanıcı adı ve parola sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-159">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="4b5ba-160">Bu, Portal üzerinden de yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-160">This can also be done via the Portal.</span></span> <span data-ttu-id="4b5ba-161">Bkz: [yönetmek Azure portalını kullanarak Hdınsight][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="4b5ba-161">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="4b5ba-162">HTTP kullanıcı kimlik bilgilerini güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="4b5ba-162">Update HTTP user credentials</span></span>
<span data-ttu-id="4b5ba-163">Yordamın aynısını olan [Grant/revoke HTTP erişimi](#grant/revoke-access). Küme HTTP erişim verilmişse, öncelikle iptal gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-163">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="4b5ba-164">Ve ardından yeni HTTP kullanıcı kimlik bilgileriyle erişim verin.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-164">And then grant the access with new HTTP user credentials.</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="4b5ba-165">Varsayılan depolama hesabı bulunamadı</span><span class="sxs-lookup"><span data-stu-id="4b5ba-165">Find the default storage account</span></span>
<span data-ttu-id="4b5ba-166">Aşağıdaki kod parçacığını varsayılan depolama hesabı adı ve bir küme için varsayılan depolama hesabı anahtarı alma gösterir.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-166">The following code snippet demonstrates how to get the default storage account name and the default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="4b5ba-167">İşlerini gönderme</span><span class="sxs-lookup"><span data-stu-id="4b5ba-167">Submit jobs</span></span>
<span data-ttu-id="4b5ba-168">**MapReduce işleri göndermek için**</span><span class="sxs-lookup"><span data-stu-id="4b5ba-168">**To submit MapReduce jobs**</span></span>

<span data-ttu-id="4b5ba-169">Bkz: [hdınsight'ta Hadoop MapReduce çalıştırma örnekleri](hdinsight-hadoop-run-samples-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4b5ba-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="4b5ba-170">**Hive işlerini göndermek için**</span><span class="sxs-lookup"><span data-stu-id="4b5ba-170">**To submit Hive jobs**</span></span> 

<span data-ttu-id="4b5ba-171">Bkz: [.NET SDK kullanarak Hive sorgularını çalıştırma](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="4b5ba-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="4b5ba-172">**Pig işleri göndermek için**</span><span class="sxs-lookup"><span data-stu-id="4b5ba-172">**To submit Pig jobs**</span></span>

<span data-ttu-id="4b5ba-173">Bkz: [.NET SDK kullanarak çalıştırmak Pig işleri](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="4b5ba-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="4b5ba-174">**Sqoop işlerini göndermek için**</span><span class="sxs-lookup"><span data-stu-id="4b5ba-174">**To submit Sqoop jobs**</span></span>

<span data-ttu-id="4b5ba-175">Bkz: [Hdınsight ile Sqoop kullanma](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="4b5ba-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="4b5ba-176">**Oozie işlerini göndermek için**</span><span class="sxs-lookup"><span data-stu-id="4b5ba-176">**To submit Oozie jobs**</span></span>

<span data-ttu-id="4b5ba-177">Bkz: [tanımlamak ve Hdınsight'ta bir iş akışını çalıştırmak için Hadoop ile kullanım Oozie](hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="4b5ba-177">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="4b5ba-178">Azure Blob depolama alanına veri yükleme</span><span class="sxs-lookup"><span data-stu-id="4b5ba-178">Upload data to Azure Blob storage</span></span>
<span data-ttu-id="4b5ba-179">Bkz. [HDInsight'a veri yükleme][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="4b5ba-179">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="4b5ba-180">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-180">See Also</span></span>
* [<span data-ttu-id="4b5ba-181">Hdınsight .NET SDK'sı başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="4b5ba-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="4b5ba-182">[Hdınsight Azure Portalı'nı kullanarak yönetme][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="4b5ba-182">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="4b5ba-183">[Bir komut satırı arabirimi kullanarak Hdınsight yönetme][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="4b5ba-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="4b5ba-184">[Hdınsight kümeleri oluşturma][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="4b5ba-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="4b5ba-185">[HDInsight'a veri yükleme][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="4b5ba-185">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="4b5ba-186">[Azure HDInsight'ı Kullanmaya Başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="4b5ba-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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


