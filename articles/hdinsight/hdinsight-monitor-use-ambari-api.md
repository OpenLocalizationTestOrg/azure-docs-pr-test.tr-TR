---
title: "kullanarak Hdınsight'ta Hadoop kümelerinin aaaMonitor hello Ambari API - Azure | Microsoft Docs"
description: "Merhaba Apache Ambari API'ları oluşturmak, yönetmek ve Hadoop kümelerini izleme için kullanın. Sezgisel işleci Araçlar ve API'ler Hadoop hello karmaşıklığını gizleyin."
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
ms.openlocfilehash: d61a8aae5ddfcd7d44f2e4cc899e0a4da5e5fdcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-hello-ambari-api"></a><span data-ttu-id="85c50-104">Merhaba Ambari API kullanarak hdınsight'ta Hadoop kümelerini izleme</span><span class="sxs-lookup"><span data-stu-id="85c50-104">Monitor Hadoop clusters in HDInsight using hello Ambari API</span></span>
<span data-ttu-id="85c50-105">Ambari API kullanarak nasıl toomonitor Hdınsight kümeleri hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="85c50-105">Learn how toomonitor HDInsight clusters by using Ambari APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="85c50-106">Bu makaledeki Hello bilgiler hello Ambari REST API salt okunur bir sürümünü sağlayın öncelikle Windows tabanlı Hdınsight kümeleri için ' dir.</span><span class="sxs-lookup"><span data-stu-id="85c50-106">hello information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of hello Ambari REST API.</span></span> <span data-ttu-id="85c50-107">Linux tabanlı kümeler için bkz: [yönetmek Hadoop kümeleri Ambari kullanarak](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="85c50-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
> 
> 

## <a name="what-is-ambari"></a><span data-ttu-id="85c50-108">Ambari nedir?</span><span class="sxs-lookup"><span data-stu-id="85c50-108">What is Ambari?</span></span>
<span data-ttu-id="85c50-109">[Apache Ambari] [ ambari-home] hazırlamak, yönetmek ve Apache Hadoop kümelerini izleme için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85c50-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span></span> <span data-ttu-id="85c50-110">İşleç araçlarının sezgisel bir koleksiyonunu ve sağlam bir Hadoop, kümelerin hello çalışmasını kolaylaştırarak, hello karmaşıklığını Gizle API kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="85c50-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide hello complexity of Hadoop, simplifying hello operation of clusters.</span></span> <span data-ttu-id="85c50-111">Hello API'ler hakkında daha fazla bilgi için bkz: [Ambari API Başvurusu][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="85c50-111">For more information about hello APIs, see [Ambari API Reference][ambari-api-reference].</span></span> 

<span data-ttu-id="85c50-112">Hdınsight şu anda yalnızca hello Ambari izleme özelliğini destekler.</span><span class="sxs-lookup"><span data-stu-id="85c50-112">HDInsight currently supports only hello Ambari monitoring feature.</span></span> <span data-ttu-id="85c50-113">Ambari API 1.0 Hdınsight sürüm 3.0 ve 2.1 kümeleri tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="85c50-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span></span> <span data-ttu-id="85c50-114">Bu makalede, Hdınsight sürüm 3.1 ve 2.1 kümelerinde erişilirken Ambari API yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="85c50-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span></span> <span data-ttu-id="85c50-115">Merhaba anahtar arasındaki hello iki hello bileşenlerinin bazılarını hello giriş yeni Capabilities (örneğin, iş geçmişi sunucusu hello) ile değiştirilmiştir farktır.</span><span class="sxs-lookup"><span data-stu-id="85c50-115">hello key difference between hello two is that some of hello components have changed with hello introduction of new capabilities (such as hello Job History Server).</span></span> 

<span data-ttu-id="85c50-116">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="85c50-116">**Prerequisites**</span></span>

<span data-ttu-id="85c50-117">Bu öğreticiye başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="85c50-117">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="85c50-118">**Azure PowerShell içeren bir iş istasyonu**.</span><span class="sxs-lookup"><span data-stu-id="85c50-118">**A workstation with Azure PowerShell**.</span></span>
* <span data-ttu-id="85c50-119">(İsteğe bağlı) [cURL][curl].</span><span class="sxs-lookup"><span data-stu-id="85c50-119">(Optional) [cURL][curl].</span></span> <span data-ttu-id="85c50-120">tooinstall, bkz: [sürümleri ve indirmeleri cURL][curl-download].</span><span class="sxs-lookup"><span data-stu-id="85c50-120">tooinstall it, see [cURL Releases and Downloads][curl-download].</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="85c50-121">Ne zaman Windows hello seçenek değerleri için tek tırnak işareti yerine çift tırnak işaretleri kullan hello cURL komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="85c50-121">When use hello cURL command in Windows, use double-quotation marks instead of single-quotation marks for hello option values.</span></span>
  > 
  > 
* <span data-ttu-id="85c50-122">**Azure Hdınsight kümesi**.</span><span class="sxs-lookup"><span data-stu-id="85c50-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="85c50-123">Küme hazırlama hakkında yönergeler için bkz: [Hdınsight kullanmaya başlama] [ hdinsight-get-started] veya [Hdınsight kümeleri hazırlama][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="85c50-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="85c50-124">Başlangıç Öğreticisi aracılığıyla veri toogo aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="85c50-124">You need hello following data toogo through hello tutorial:</span></span>
  
  | <span data-ttu-id="85c50-125">Küme özelliği</span><span class="sxs-lookup"><span data-stu-id="85c50-125">Cluster property</span></span> | <span data-ttu-id="85c50-126">Azure PowerShell değişken adı</span><span class="sxs-lookup"><span data-stu-id="85c50-126">Azure PowerShell variable name</span></span> | <span data-ttu-id="85c50-127">Değer</span><span class="sxs-lookup"><span data-stu-id="85c50-127">Value</span></span> | <span data-ttu-id="85c50-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="85c50-128">Description</span></span> |
  | --- | --- | --- | --- |
  |   <span data-ttu-id="85c50-129">Hdınsight küme adı</span><span class="sxs-lookup"><span data-stu-id="85c50-129">HDInsight cluster name</span></span> |<span data-ttu-id="85c50-130">$clusterName</span><span class="sxs-lookup"><span data-stu-id="85c50-130">$clusterName</span></span> | |<span data-ttu-id="85c50-131">Hdınsight kümenize Hello adı.</span><span class="sxs-lookup"><span data-stu-id="85c50-131">hello name of your HDInsight cluster.</span></span> |
  |   <span data-ttu-id="85c50-132">Küme kullanıcı</span><span class="sxs-lookup"><span data-stu-id="85c50-132">Cluster username</span></span> |<span data-ttu-id="85c50-133">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="85c50-133">$clusterUsername</span></span> | |<span data-ttu-id="85c50-134">Merhaba küme oluşturulduğu belirtilen küme kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="85c50-134">Cluster user name specified when hello cluster was created.</span></span> |
  |   <span data-ttu-id="85c50-135">Küme parolası</span><span class="sxs-lookup"><span data-stu-id="85c50-135">Cluster password</span></span> |<span data-ttu-id="85c50-136">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="85c50-136">$clusterPassword</span></span> | |<span data-ttu-id="85c50-137">Küme kullanıcı parolası.</span><span class="sxs-lookup"><span data-stu-id="85c50-137">Cluster user password.</span></span> |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a><span data-ttu-id="85c50-138">Hemen başlayın</span><span class="sxs-lookup"><span data-stu-id="85c50-138">Jump-start</span></span>
<span data-ttu-id="85c50-139">Toouse Ambari toomonitor Hdınsight kümeleri birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="85c50-139">There are several ways toouse Ambari toomonitor HDInsight clusters.</span></span>

<span data-ttu-id="85c50-140">**Azure PowerShell’i kullanma**</span><span class="sxs-lookup"><span data-stu-id="85c50-140">**Use Azure PowerShell**</span></span>

<span data-ttu-id="85c50-141">Azure PowerShell Betiği aşağıdaki hello alır hello MapReduce işi İzleyicisi bilgileri *bir Hdınsight 3.5 kümesindeki.*</span><span class="sxs-lookup"><span data-stu-id="85c50-141">hello following Azure PowerShell script gets hello MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span></span>  <span data-ttu-id="85c50-142">Merhaba anahtar Biz bu ayrıntıları hello YARN hizmeti (MapReduce yerine) çekme farktır.</span><span class="sxs-lookup"><span data-stu-id="85c50-142">hello key difference is that we pull these details from hello YARN service (rather than MapReduce).</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

<span data-ttu-id="85c50-143">PowerShell Betiği aşağıdaki hello alır hello MapReduce işi İzleyicisi bilgileri *bir Hdınsight 2.1 kümesindeki*:</span><span class="sxs-lookup"><span data-stu-id="85c50-143">hello following PowerShell script gets hello MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

<span data-ttu-id="85c50-144">Merhaba çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="85c50-144">hello output is:</span></span>

![Jobtracker'a çıkış][img-jobtracker-output]

<span data-ttu-id="85c50-146">**cURL kullanma**</span><span class="sxs-lookup"><span data-stu-id="85c50-146">**Use cURL**</span></span>

<span data-ttu-id="85c50-147">Merhaba aşağıdaki örnek küme bilgilerini cURL kullanarak alır:</span><span class="sxs-lookup"><span data-stu-id="85c50-147">hello following example gets cluster information by using cURL:</span></span>

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

<span data-ttu-id="85c50-148">Merhaba çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="85c50-148">hello output is:</span></span>

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

<span data-ttu-id="85c50-149">**Merhaba 8/10/2014 sürümü için**:</span><span class="sxs-lookup"><span data-stu-id="85c50-149">**For hello 10/8/2014 release**:</span></span>

<span data-ttu-id="85c50-150">Ne zaman kullanarak izin ver hello Ambari uç noktası, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}" Merhaba *host_name* alan Merhaba ana bilgisayar adı yerine hello düğümünün Hello tam etki alanı adı (FQDN) döndürür.</span><span class="sxs-lookup"><span data-stu-id="85c50-150">When using hello Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", hello *host_name* field returns hello fully qualified domain name (FQDN) of hello node instead of hello host name.</span></span> <span data-ttu-id="85c50-151">Merhaba 8/10/2014 sürümünden önce bu örnek döndürülen yalnızca "**headnode0**".</span><span class="sxs-lookup"><span data-stu-id="85c50-151">Before hello 10/8/2014 release, this example returned simply "**headnode0**".</span></span> <span data-ttu-id="85c50-152">Merhaba 8/10/2014 sürümünden sonra hello FQDN Al "**headnode0. { ClusterDNS} .azurehdinsight .net**", bir hello önceki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="85c50-152">After hello 10/8/2014 release, you get hello FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in hello previous example.</span></span> <span data-ttu-id="85c50-153">Bu değişiklik, bir sanal ağ (VNET) içinde birden çok küme türleri (örneğin, HBase ve Hadoop) dağıtıldığı gerekli toofacilitate senaryoları oluştu.</span><span class="sxs-lookup"><span data-stu-id="85c50-153">This change was required toofacilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span></span> <span data-ttu-id="85c50-154">Bu, örneğin, Hadoop için bir arka uç platform olarak HBase kullanarak olur.</span><span class="sxs-lookup"><span data-stu-id="85c50-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

## <a name="ambari-monitoring-apis"></a><span data-ttu-id="85c50-155">Ambari API izleme</span><span class="sxs-lookup"><span data-stu-id="85c50-155">Ambari monitoring APIs</span></span>
<span data-ttu-id="85c50-156">Merhaba aşağıdaki tabloda bazı hello en yaygın Ambari izleme API çağrıları yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="85c50-156">hello following table lists some of hello most common Ambari monitoring API calls.</span></span> <span data-ttu-id="85c50-157">Merhaba API'si hakkında daha fazla bilgi için bkz: [Ambari API Başvurusu][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="85c50-157">For more information about hello API, see [Ambari API Reference][ambari-api-reference].</span></span>

| <span data-ttu-id="85c50-158">İzleyici API çağrısı</span><span class="sxs-lookup"><span data-stu-id="85c50-158">Monitor API call</span></span> | <span data-ttu-id="85c50-159">URI</span><span class="sxs-lookup"><span data-stu-id="85c50-159">URI</span></span> | <span data-ttu-id="85c50-160">Açıklama</span><span class="sxs-lookup"><span data-stu-id="85c50-160">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85c50-161">Kümeleri Al</span><span class="sxs-lookup"><span data-stu-id="85c50-161">Get clusters</span></span> |`/api/v1/clusters` | |
| <span data-ttu-id="85c50-162">Küme bilgilerini al.</span><span class="sxs-lookup"><span data-stu-id="85c50-162">Get cluster info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |<span data-ttu-id="85c50-163">kümeler, hizmetleri, ana bilgisayarlar</span><span class="sxs-lookup"><span data-stu-id="85c50-163">clusters, services, hosts</span></span> |
| <span data-ttu-id="85c50-164">Hizmetlerini Al</span><span class="sxs-lookup"><span data-stu-id="85c50-164">Get services</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |<span data-ttu-id="85c50-165">Hizmetleri içerir: hdfs, mapreduce</span><span class="sxs-lookup"><span data-stu-id="85c50-165">Services include: hdfs, mapreduce</span></span> |
| <span data-ttu-id="85c50-166">Hizmetleri bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="85c50-166">Get services info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| <span data-ttu-id="85c50-167">Hizmet bileşenlerini Al</span><span class="sxs-lookup"><span data-stu-id="85c50-167">Get service components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |<span data-ttu-id="85c50-168">HDFS: iş, datanodeMapReduce: jobtracker'a; tasktracker</span><span class="sxs-lookup"><span data-stu-id="85c50-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span></span> |
| <span data-ttu-id="85c50-169">Bileşen bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="85c50-169">Get component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |<span data-ttu-id="85c50-170">ServiceComponentInfo, ana bilgisayar bileşenleri, ölçümleri</span><span class="sxs-lookup"><span data-stu-id="85c50-170">ServiceComponentInfo, host-components, metrics</span></span> |
| <span data-ttu-id="85c50-171">Konaklar Al</span><span class="sxs-lookup"><span data-stu-id="85c50-171">Get hosts</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |<span data-ttu-id="85c50-172">headnode0, workernode0</span><span class="sxs-lookup"><span data-stu-id="85c50-172">headnode0, workernode0</span></span> |
| <span data-ttu-id="85c50-173">Ana bilgisayar bilgilerini al.</span><span class="sxs-lookup"><span data-stu-id="85c50-173">Get host info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| <span data-ttu-id="85c50-174">Ana bilgisayar bileşenlerini Al</span><span class="sxs-lookup"><span data-stu-id="85c50-174">Get host components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |<span data-ttu-id="85c50-175">İş, resourcemanager</span><span class="sxs-lookup"><span data-stu-id="85c50-175">namenode, resourcemanager</span></span> |
| <span data-ttu-id="85c50-176">Ana bileşeni bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="85c50-176">Get host component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |<span data-ttu-id="85c50-177">HostRoles, bileşen, ana bilgisayar, ölçümleri</span><span class="sxs-lookup"><span data-stu-id="85c50-177">HostRoles, component, host, metrics</span></span> |
| <span data-ttu-id="85c50-178">Yapılandırmalarını alma</span><span class="sxs-lookup"><span data-stu-id="85c50-178">Get configurations</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |<span data-ttu-id="85c50-179">Yapılandırma türleri: çekirdek site, site hdfs, mapred site, hive site</span><span class="sxs-lookup"><span data-stu-id="85c50-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |
| <span data-ttu-id="85c50-180">Yapılandırma bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="85c50-180">Get configuration info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |<span data-ttu-id="85c50-181">Yapılandırma türleri: çekirdek site, site hdfs, mapred site, hive site</span><span class="sxs-lookup"><span data-stu-id="85c50-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |

## <a name="next-steps"></a><span data-ttu-id="85c50-182">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="85c50-182">Next Steps</span></span>
<span data-ttu-id="85c50-183">Öğrendiğiniz artık nasıl Ambari API izleme toouse çağırır.</span><span class="sxs-lookup"><span data-stu-id="85c50-183">Now you have learned how toouse Ambari monitoring API calls.</span></span> <span data-ttu-id="85c50-184">toolearn daha bakın:</span><span class="sxs-lookup"><span data-stu-id="85c50-184">toolearn more, see:</span></span>

* <span data-ttu-id="85c50-185">[Hello Azure portal kullanarak Hdınsight kümelerini yönetme][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="85c50-185">[Manage HDInsight clusters using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="85c50-186">[Azure PowerShell kullanarak Hdınsight kümelerini yönetme][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="85c50-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="85c50-187">[Komut satırı arabirimi kullanarak Hdınsight kümelerini yönetme][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="85c50-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="85c50-188">[Hdınsight belgeleri][hdinsight-documentation]</span><span class="sxs-lookup"><span data-stu-id="85c50-188">[HDInsight documentation][hdinsight-documentation]</span></span>
* <span data-ttu-id="85c50-189">[Hdınsight kullanmaya başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="85c50-189">[Get started with HDInsight][hdinsight-get-started]</span></span>

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
