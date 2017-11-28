---
title: "-Azure Ambari API kullanarak hdınsight'ta Hadoop kümelerini izleme | Microsoft Docs"
description: "Apache Ambari API'ları oluşturmak, yönetmek ve Hadoop kümelerini izleme için kullanın. Sezgisel işleci Araçlar ve API'ler Hadoop karmaşıklığını gizleyin."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
editor: cgronlun
manager: jhubbard
ms.assetid: 052135b3-d497-4acc-92ff-71cee49356ff
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: b6fc2098027690eb76b69b1427f0e9541b8a7a69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-the-ambari-api"></a><span data-ttu-id="97e60-104">Ambari API'sini kullanarak HDInsight'ta Hadoop kümelerini izleme</span><span class="sxs-lookup"><span data-stu-id="97e60-104">Monitor Hadoop clusters in HDInsight using the Ambari API</span></span>
<span data-ttu-id="97e60-105">Ambari API kullanarak Hdınsight kümelerini izlemek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="97e60-105">Learn how to monitor HDInsight clusters by using Ambari APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="97e60-106">Bu makaledeki bilgiler Ambari REST API salt okunur bir sürümünü sağlayın öncelikle Windows tabanlı Hdınsight kümeleri için ' dir.</span><span class="sxs-lookup"><span data-stu-id="97e60-106">The information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of the Ambari REST API.</span></span> <span data-ttu-id="97e60-107">Linux tabanlı kümeler için bkz: [yönetmek Hadoop kümeleri Ambari kullanarak](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="97e60-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
> 
> 

## <a name="what-is-ambari"></a><span data-ttu-id="97e60-108">Ambari nedir?</span><span class="sxs-lookup"><span data-stu-id="97e60-108">What is Ambari?</span></span>
<span data-ttu-id="97e60-109">[Apache Ambari] [ ambari-home] hazırlamak, yönetmek ve Apache Hadoop kümelerini izleme için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="97e60-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span></span> <span data-ttu-id="97e60-110">Bu, kümelerin çalışmasını kolaylaştırarak, işleç araçlarının sezgisel bir koleksiyonunu ve Hadoop’un karmaşıklığı gizleyen sağlam bir API kümesini içerir.</span><span class="sxs-lookup"><span data-stu-id="97e60-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide the complexity of Hadoop, simplifying the operation of clusters.</span></span> <span data-ttu-id="97e60-111">API'ler hakkında daha fazla bilgi için bkz: [Ambari API Başvurusu][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="97e60-111">For more information about the APIs, see [Ambari API Reference][ambari-api-reference].</span></span> 

<span data-ttu-id="97e60-112">Hdınsight şu anda yalnızca Ambari izleme özelliğini destekler.</span><span class="sxs-lookup"><span data-stu-id="97e60-112">HDInsight currently supports only the Ambari monitoring feature.</span></span> <span data-ttu-id="97e60-113">Ambari API 1.0 Hdınsight sürüm 3.0 ve 2.1 kümeleri tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="97e60-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span></span> <span data-ttu-id="97e60-114">Bu makalede, Hdınsight sürüm 3.1 ve 2.1 kümelerinde erişilirken Ambari API yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="97e60-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span></span> <span data-ttu-id="97e60-115">İkisi arasındaki temel fark, bazı bileşenleri (örneğin, iş geçmişi sunucusu) yeni özellikler girişiyle değişmiş ' dir.</span><span class="sxs-lookup"><span data-stu-id="97e60-115">The key difference between the two is that some of the components have changed with the introduction of new capabilities (such as the Job History Server).</span></span> 

<span data-ttu-id="97e60-116">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="97e60-116">**Prerequisites**</span></span>

<span data-ttu-id="97e60-117">Bu öğreticiye başlamadan önce aşağıdaki öğelere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="97e60-117">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="97e60-118">**Azure PowerShell içeren bir iş istasyonu**.</span><span class="sxs-lookup"><span data-stu-id="97e60-118">**A workstation with Azure PowerShell**.</span></span>
* <span data-ttu-id="97e60-119">(İsteğe bağlı) [cURL][curl].</span><span class="sxs-lookup"><span data-stu-id="97e60-119">(Optional) [cURL][curl].</span></span> <span data-ttu-id="97e60-120">Yüklemek için bkz: [sürümleri ve indirmeleri cURL][curl-download].</span><span class="sxs-lookup"><span data-stu-id="97e60-120">To install it, see [cURL Releases and Downloads][curl-download].</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="97e60-121">Windows'da çift tırnak işaretleri kullan seçeneği değerleri için tek tırnak işareti yerine ne zaman cURL komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="97e60-121">When use the cURL command in Windows, use double-quotation marks instead of single-quotation marks for the option values.</span></span>
  > 
  > 
* <span data-ttu-id="97e60-122">**Azure Hdınsight kümesi**.</span><span class="sxs-lookup"><span data-stu-id="97e60-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="97e60-123">Küme hazırlama hakkında yönergeler için bkz: [Hdınsight kullanmaya başlama] [ hdinsight-get-started] veya [Hdınsight kümeleri hazırlama][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="97e60-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="97e60-124">Öğreticiyi incelemek için aşağıdaki veriler gerekir:</span><span class="sxs-lookup"><span data-stu-id="97e60-124">You need the following data to go through the tutorial:</span></span>
  
  | <span data-ttu-id="97e60-125">Küme özelliği</span><span class="sxs-lookup"><span data-stu-id="97e60-125">Cluster property</span></span> | <span data-ttu-id="97e60-126">Azure PowerShell değişken adı</span><span class="sxs-lookup"><span data-stu-id="97e60-126">Azure PowerShell variable name</span></span> | <span data-ttu-id="97e60-127">Değer</span><span class="sxs-lookup"><span data-stu-id="97e60-127">Value</span></span> | <span data-ttu-id="97e60-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="97e60-128">Description</span></span> |
  | --- | --- | --- | --- |
  |   <span data-ttu-id="97e60-129">Hdınsight küme adı</span><span class="sxs-lookup"><span data-stu-id="97e60-129">HDInsight cluster name</span></span> |<span data-ttu-id="97e60-130">$clusterName</span><span class="sxs-lookup"><span data-stu-id="97e60-130">$clusterName</span></span> | |<span data-ttu-id="97e60-131">Hdınsight kümenizin adıdır.</span><span class="sxs-lookup"><span data-stu-id="97e60-131">The name of your HDInsight cluster.</span></span> |
  |   <span data-ttu-id="97e60-132">Küme kullanıcı</span><span class="sxs-lookup"><span data-stu-id="97e60-132">Cluster username</span></span> |<span data-ttu-id="97e60-133">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="97e60-133">$clusterUsername</span></span> | |<span data-ttu-id="97e60-134">Küme oluşturulduğu belirtilen küme kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="97e60-134">Cluster user name specified when the cluster was created.</span></span> |
  |   <span data-ttu-id="97e60-135">Küme parolası</span><span class="sxs-lookup"><span data-stu-id="97e60-135">Cluster password</span></span> |<span data-ttu-id="97e60-136">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="97e60-136">$clusterPassword</span></span> | |<span data-ttu-id="97e60-137">Küme kullanıcı parolası.</span><span class="sxs-lookup"><span data-stu-id="97e60-137">Cluster user password.</span></span> |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a><span data-ttu-id="97e60-138">Hemen başlayın</span><span class="sxs-lookup"><span data-stu-id="97e60-138">Jump-start</span></span>
<span data-ttu-id="97e60-139">Hdınsight kümeleri izlemek için Ambari kullanmak için birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="97e60-139">There are several ways to use Ambari to monitor HDInsight clusters.</span></span>

<span data-ttu-id="97e60-140">**Azure PowerShell’i kullanma**</span><span class="sxs-lookup"><span data-stu-id="97e60-140">**Use Azure PowerShell**</span></span>

<span data-ttu-id="97e60-141">MapReduce işi İzleyicisi bilgileri aşağıdaki Azure PowerShell betiğini alır *bir Hdınsight 3.5 kümesindeki.*</span><span class="sxs-lookup"><span data-stu-id="97e60-141">The following Azure PowerShell script gets the MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span></span>  <span data-ttu-id="97e60-142">Biz bu ayrıntıları YARN hizmet (yerine MapReduce) çekme anahtar farktır.</span><span class="sxs-lookup"><span data-stu-id="97e60-142">The key difference is that we pull these details from the YARN service (rather than MapReduce).</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

<span data-ttu-id="97e60-143">Aşağıdaki PowerShell betiğini MapReduce işi İzleyicisi bilgileri alır *bir Hdınsight 2.1 kümesindeki*:</span><span class="sxs-lookup"><span data-stu-id="97e60-143">The following PowerShell script gets the MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

<span data-ttu-id="97e60-144">Çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="97e60-144">The output is:</span></span>

![Jobtracker'a çıkış][img-jobtracker-output]

<span data-ttu-id="97e60-146">**cURL kullanma**</span><span class="sxs-lookup"><span data-stu-id="97e60-146">**Use cURL**</span></span>

<span data-ttu-id="97e60-147">Aşağıdaki örnek, cURL kullanarak küme bilgilerini alır:</span><span class="sxs-lookup"><span data-stu-id="97e60-147">The following example gets cluster information by using cURL:</span></span>

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

<span data-ttu-id="97e60-148">Çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="97e60-148">The output is:</span></span>

    {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/",
     "Clusters":{"cluster_name":"hdi0211v2.azurehdinsight.net","version":"2.1.3.0.432823"},
     "services"[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/hdfs",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"hdfs"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/mapreduce",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"mapreduce"}}],
     "hosts":[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/headnode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/workernode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0.{ClusterDNS}.azurehdinsight.net"}}]}

<span data-ttu-id="97e60-149">**8/10/2014 sürümü için**:</span><span class="sxs-lookup"><span data-stu-id="97e60-149">**For the 10/8/2014 release**:</span></span>

<span data-ttu-id="97e60-150">Ambari uç nokta kullanılırken "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}" *host_name* alan ana bilgisayar adı yerine düğümün tam etki alanı adını (FQDN) döndürür.</span><span class="sxs-lookup"><span data-stu-id="97e60-150">When using the Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", the *host_name* field returns the fully qualified domain name (FQDN) of the node instead of the host name.</span></span> <span data-ttu-id="97e60-151">8/10/2014 yayınlanmadan önce bu örnek döndürülen yalnızca "**headnode0**".</span><span class="sxs-lookup"><span data-stu-id="97e60-151">Before the 10/8/2014 release, this example returned simply "**headnode0**".</span></span> <span data-ttu-id="97e60-152">8/10/2014 yayınlanmasından sonra FQDN Al "**headnode0. { ClusterDNS} .azurehdinsight .net**", bir önceki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="97e60-152">After the 10/8/2014 release, you get the FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in the previous example.</span></span> <span data-ttu-id="97e60-153">Bu değişiklik, birden çok küme türleri (örneğin, HBase ve Hadoop) bir sanal ağ (VNET) burada dağıtılabilir senaryolarını kolaylaştırmak için gerekiyordu.</span><span class="sxs-lookup"><span data-stu-id="97e60-153">This change was required to facilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span></span> <span data-ttu-id="97e60-154">Bu, örneğin, Hadoop için bir arka uç platform olarak HBase kullanarak olur.</span><span class="sxs-lookup"><span data-stu-id="97e60-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

## <a name="ambari-monitoring-apis"></a><span data-ttu-id="97e60-155">Ambari API izleme</span><span class="sxs-lookup"><span data-stu-id="97e60-155">Ambari monitoring APIs</span></span>
<span data-ttu-id="97e60-156">Aşağıdaki tabloda bazı yaygın Ambari API çağrıları izleme yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="97e60-156">The following table lists some of the most common Ambari monitoring API calls.</span></span> <span data-ttu-id="97e60-157">API'si hakkında daha fazla bilgi için bkz: [Ambari API Başvurusu][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="97e60-157">For more information about the API, see [Ambari API Reference][ambari-api-reference].</span></span>

| <span data-ttu-id="97e60-158">İzleyici API çağrısı</span><span class="sxs-lookup"><span data-stu-id="97e60-158">Monitor API call</span></span> | <span data-ttu-id="97e60-159">URI</span><span class="sxs-lookup"><span data-stu-id="97e60-159">URI</span></span> | <span data-ttu-id="97e60-160">Açıklama</span><span class="sxs-lookup"><span data-stu-id="97e60-160">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="97e60-161">Kümeleri Al</span><span class="sxs-lookup"><span data-stu-id="97e60-161">Get clusters</span></span> |`/api/v1/clusters` | |
| <span data-ttu-id="97e60-162">Küme bilgilerini al.</span><span class="sxs-lookup"><span data-stu-id="97e60-162">Get cluster info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |<span data-ttu-id="97e60-163">kümeler, hizmetleri, ana bilgisayarlar</span><span class="sxs-lookup"><span data-stu-id="97e60-163">clusters, services, hosts</span></span> |
| <span data-ttu-id="97e60-164">Hizmetlerini Al</span><span class="sxs-lookup"><span data-stu-id="97e60-164">Get services</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |<span data-ttu-id="97e60-165">Hizmetleri içerir: hdfs, mapreduce</span><span class="sxs-lookup"><span data-stu-id="97e60-165">Services include: hdfs, mapreduce</span></span> |
| <span data-ttu-id="97e60-166">Hizmetleri bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="97e60-166">Get services info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| <span data-ttu-id="97e60-167">Hizmet bileşenlerini Al</span><span class="sxs-lookup"><span data-stu-id="97e60-167">Get service components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |<span data-ttu-id="97e60-168">HDFS: iş, datanodeMapReduce: jobtracker'a; tasktracker</span><span class="sxs-lookup"><span data-stu-id="97e60-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span></span> |
| <span data-ttu-id="97e60-169">Bileşen bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="97e60-169">Get component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |<span data-ttu-id="97e60-170">ServiceComponentInfo, ana bilgisayar bileşenleri, ölçümleri</span><span class="sxs-lookup"><span data-stu-id="97e60-170">ServiceComponentInfo, host-components, metrics</span></span> |
| <span data-ttu-id="97e60-171">Konaklar Al</span><span class="sxs-lookup"><span data-stu-id="97e60-171">Get hosts</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |<span data-ttu-id="97e60-172">headnode0, workernode0</span><span class="sxs-lookup"><span data-stu-id="97e60-172">headnode0, workernode0</span></span> |
| <span data-ttu-id="97e60-173">Ana bilgisayar bilgilerini al.</span><span class="sxs-lookup"><span data-stu-id="97e60-173">Get host info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| <span data-ttu-id="97e60-174">Ana bilgisayar bileşenlerini Al</span><span class="sxs-lookup"><span data-stu-id="97e60-174">Get host components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |<span data-ttu-id="97e60-175">İş, resourcemanager</span><span class="sxs-lookup"><span data-stu-id="97e60-175">namenode, resourcemanager</span></span> |
| <span data-ttu-id="97e60-176">Ana bileşeni bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="97e60-176">Get host component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |<span data-ttu-id="97e60-177">HostRoles, bileşen, ana bilgisayar, ölçümleri</span><span class="sxs-lookup"><span data-stu-id="97e60-177">HostRoles, component, host, metrics</span></span> |
| <span data-ttu-id="97e60-178">Yapılandırmalarını alma</span><span class="sxs-lookup"><span data-stu-id="97e60-178">Get configurations</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |<span data-ttu-id="97e60-179">Yapılandırma türleri: çekirdek site, site hdfs, mapred site, hive site</span><span class="sxs-lookup"><span data-stu-id="97e60-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |
| <span data-ttu-id="97e60-180">Yapılandırma bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="97e60-180">Get configuration info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |<span data-ttu-id="97e60-181">Yapılandırma türleri: çekirdek site, site hdfs, mapred site, hive site</span><span class="sxs-lookup"><span data-stu-id="97e60-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |

## <a name="next-steps"></a><span data-ttu-id="97e60-182">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="97e60-182">Next Steps</span></span>
<span data-ttu-id="97e60-183">Şimdi Ambari API çağrıları izleme kullanmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="97e60-183">Now you have learned how to use Ambari monitoring API calls.</span></span> <span data-ttu-id="97e60-184">Daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="97e60-184">To learn more, see:</span></span>

* <span data-ttu-id="97e60-185">[Azure portalını kullanarak Hdınsight kümelerini yönetme][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="97e60-185">[Manage HDInsight clusters using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="97e60-186">[Azure PowerShell kullanarak Hdınsight kümelerini yönetme][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="97e60-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="97e60-187">[Komut satırı arabirimi kullanarak Hdınsight kümelerini yönetme][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="97e60-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="97e60-188">[Hdınsight belgeleri][hdinsight-documentation]</span><span class="sxs-lookup"><span data-stu-id="97e60-188">[HDInsight documentation][hdinsight-documentation]</span></span>
* <span data-ttu-id="97e60-189">[Hdınsight kullanmaya başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="97e60-189">[Get started with HDInsight][hdinsight-get-started]</span></span>

[ambari-home]: http://ambari.apache.org/
[ambari-api-reference]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[microsoft-hadoop-SDK]: http://hadoopsdk.codeplex.com/wikipage?title=Ambari%20Monitoring%20Client

[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-documentation]: https://docs.microsoft.com/azure/hdinsight/
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[img-jobtracker-output]: ./media/hdinsight-monitor-use-ambari-api/hdi.ambari.monitor.jobtracker.output.png
