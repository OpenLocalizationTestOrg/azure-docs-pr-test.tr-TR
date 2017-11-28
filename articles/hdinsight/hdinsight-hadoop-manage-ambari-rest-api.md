---
title: "İzleme ve Hadoop Ambari REST API - Azure Hdınsight ile yönetme | Microsoft Docs"
description: "Azure hdınsight'ta Hadoop kümelerini yönetmek ve izlemek için Ambari kullanmayı öğrenin. Bu belgede, Hdınsight kümeleriyle dahil Ambari REST API kullanmayı öğreneceksiniz."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2400530f-92b3-47b7-aa48-875f028765ff
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 7960d83bce22d4f671d61e9aaf55561bc24308f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-hdinsight-clusters-by-using-the-ambari-rest-api"></a><span data-ttu-id="3af02-104">Ambari REST API kullanarak Hdınsight kümelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="3af02-104">Manage HDInsight clusters by using the Ambari REST API</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="3af02-105">Azure hdınsight'ta Hadoop kümelerini izlemek için Ambari REST API kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3af02-105">Learn how to use the Ambari REST API to manage and monitor Hadoop clusters in Azure HDInsight.</span></span>

<span data-ttu-id="3af02-106">Apache Ambari, yönetim ve kolay bir web kullanıcı Arabirimi ve REST API kullanmayı sağlayarak Hadoop kümesi izleme basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="3af02-106">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span></span> <span data-ttu-id="3af02-107">Ambari, Linux işletim sistemi kullanan Hdınsight kümelerine dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="3af02-107">Ambari is included on HDInsight clusters that use the Linux operating system.</span></span> <span data-ttu-id="3af02-108">Ambari, kümeyi izlemek ve yapılandırma değişiklikleri yapmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3af02-108">You can use Ambari to monitor the cluster and make configuration changes.</span></span>

## <span data-ttu-id="3af02-109"><a id="whatis"></a>Ambari nedir</span><span class="sxs-lookup"><span data-stu-id="3af02-109"><a id="whatis"></a>What is Ambari</span></span>

<span data-ttu-id="3af02-110">[Apache Ambari](http://ambari.apache.org) web sağlamak, yönetmek ve Hadoop kümeleri izlemek için kullanılan kullanıcı Arabirimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="3af02-110">[Apache Ambari](http://ambari.apache.org) provides web UI that can be used to provision, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="3af02-111">Geliştiriciler tümleştirebilir Bu yetenekler uygulamalarına kullanarak [Ambari REST API'leri](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="3af02-111">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="3af02-112">Ambari, Linux tabanlı Hdınsight kümeleri ile varsayılan olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="3af02-112">Ambari is provided by default with Linux-based HDInsight clusters.</span></span>

## <a name="how-to-use-the-ambari-rest-api"></a><span data-ttu-id="3af02-113">Ambari REST API kullanma</span><span class="sxs-lookup"><span data-stu-id="3af02-113">How to use the Ambari REST API</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3af02-114">Bu belgedeki örneklerde ve bilgi Linux işletim sistemi kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3af02-114">The information and examples in this document require an HDInsight cluster that uses Linux operating system.</span></span> <span data-ttu-id="3af02-115">Daha fazla bilgi için bkz: [Hdınsight kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3af02-115">For more information, see [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

<span data-ttu-id="3af02-116">Bu belgedeki örneklerde Uluç Kabuğu (bash) ve PowerShell için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="3af02-116">The examples in this document are provided for both the Bourne shell (bash) and PowerShell.</span></span> <span data-ttu-id="3af02-117">Örnekler GNU ile test edilmiş bash 4.3.11 bash, ancak diğer UNIX Kabukları ile çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3af02-117">The bash examples were tested with GNU bash 4.3.11, but should work with other Unix shells.</span></span> <span data-ttu-id="3af02-118">PowerShell örneklerini PowerShell 5.0 ile test edilmiş, ancak PowerShell 3.0 veya üstünü çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3af02-118">The PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span></span>

<span data-ttu-id="3af02-119">Kullanıyorsanız __Uluç Kabuk__ (Bash) aşağıdakilerin yüklü olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="3af02-119">If using the __Bourne shell__ (Bash), you must have the following installed:</span></span>

* <span data-ttu-id="3af02-120">[cURL](http://curl.haxx.se/): cURL olduğundan komut satırından REST API'leri ile çalışmak için kullanılan bir yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="3af02-120">[cURL](http://curl.haxx.se/): cURL is a utility that can be used to work with REST APIs from the command line.</span></span> <span data-ttu-id="3af02-121">Bu belgede, Ambari REST API'si ile iletişim kurmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3af02-121">In this document, it is used to communicate with the Ambari REST API.</span></span>

<span data-ttu-id="3af02-122">Bash veya PowerShell kullanarak olup olmadığını oluşturmuş olmanız da gerekir [jq](https://stedolan.github.io/jq/) yüklü.</span><span class="sxs-lookup"><span data-stu-id="3af02-122">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span></span> <span data-ttu-id="3af02-123">Jq JSON belgeleri ile çalışmaya yönelik bir yardımcı programdır.</span><span class="sxs-lookup"><span data-stu-id="3af02-123">Jq is a utility for working with JSON documents.</span></span> <span data-ttu-id="3af02-124">İçinde kullanılan **tüm** Bash örnekler ve **bir** PowerShell örnekler.</span><span class="sxs-lookup"><span data-stu-id="3af02-124">It is used in **all** the Bash examples, and **one** of the PowerShell examples.</span></span>

### <a name="base-uri-for-ambari-rest-api"></a><span data-ttu-id="3af02-125">Temel Ambari Rest API için URI</span><span class="sxs-lookup"><span data-stu-id="3af02-125">Base URI for Ambari Rest API</span></span>

<span data-ttu-id="3af02-126">Https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, hdınsight'ta Ambari REST API için ana URI olduğu yere **CLUSTERNAME** kümenizin adıdır.</span><span class="sxs-lookup"><span data-stu-id="3af02-126">The base URI for the Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3af02-127">URI (CLUSTERNAME.azurehdinsight.net) tam etki alanı adı (FQDN) parçası olarak küme adı büyük küçük harf duyarsız olsa da, diğer örnekleri URI büyük küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="3af02-127">While the cluster name in the fully qualified domain name (FQDN) part of the URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in the URI are case-sensitive.</span></span> <span data-ttu-id="3af02-128">Örneğin, kümenizi adlı `MyCluster`, geçerli URI'ler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3af02-128">For example, if your cluster is named `MyCluster`, the following are valid URIs:</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> <span data-ttu-id="3af02-129">Aşağıdaki URI'ler ikinci oluşum adının doğru durumda olmadığı için bir hata döndürür.</span><span class="sxs-lookup"><span data-stu-id="3af02-129">The following URIs return an error because the second occurrence of the name is not the correct case.</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a><span data-ttu-id="3af02-130">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="3af02-130">Authentication</span></span>

<span data-ttu-id="3af02-131">Hdınsight üzerinde Ambari bağlanma HTTPS gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3af02-131">Connecting to Ambari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="3af02-132">Yönetici hesabı adı kullanın (varsayılan **yönetici**) ve küme oluşturma sırasında sağlanan parola.</span><span class="sxs-lookup"><span data-stu-id="3af02-132">Use the admin account name (the default is **admin**) and password you provided during cluster creation.</span></span>

## <a name="examples-authentication-and-parsing-json"></a><span data-ttu-id="3af02-133">Örnekler: Kimlik doğrulaması ve JSON ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="3af02-133">Examples: Authentication and parsing JSON</span></span>

<span data-ttu-id="3af02-134">Aşağıdaki örnekler bir GET isteği temel Ambari REST API'sine karşı nasıl yapılacağını göstermek:</span><span class="sxs-lookup"><span data-stu-id="3af02-134">The following examples demonstrate how to make a GET request against the base Ambari REST API:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> <span data-ttu-id="3af02-135">Bu belgedeki Bash örnekler aşağıdaki varsayımlar olun:</span><span class="sxs-lookup"><span data-stu-id="3af02-135">The Bash examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="3af02-136">Küme için oturum açma adı varsayılan değeri `admin`.</span><span class="sxs-lookup"><span data-stu-id="3af02-136">The login name for the cluster is the default value of `admin`.</span></span>
> * <span data-ttu-id="3af02-137">`$PASSWORD`Hdınsight oturum açma komut parolasını içerir.</span><span class="sxs-lookup"><span data-stu-id="3af02-137">`$PASSWORD` contains the password for the HDInsight login command.</span></span> <span data-ttu-id="3af02-138">Bu değer kullanılarak ayarlanır `PASSWORD='mypassword'`.</span><span class="sxs-lookup"><span data-stu-id="3af02-138">You can set this value by using `PASSWORD='mypassword'`.</span></span>
> * <span data-ttu-id="3af02-139">`$CLUSTERNAME`Küme adını içerir.</span><span class="sxs-lookup"><span data-stu-id="3af02-139">`$CLUSTERNAME` contains the name of the cluster.</span></span> <span data-ttu-id="3af02-140">Bu değer kullanılarak ayarlanır`set CLUSTERNAME='clustername'`</span><span class="sxs-lookup"><span data-stu-id="3af02-140">You can set this value by using `set CLUSTERNAME='clustername'`</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> <span data-ttu-id="3af02-141">Bu belgedeki PowerShell örnekleri aşağıdaki varsayımlar olun:</span><span class="sxs-lookup"><span data-stu-id="3af02-141">The PowerShell examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="3af02-142">`$creds`yönetici oturum açma ve küme için parola içeren bir kimlik bilgisi nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="3af02-142">`$creds` is a credential object that contains the admin login and password for the cluster.</span></span> <span data-ttu-id="3af02-143">Bu değer kullanılarak ayarlanır `$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"` ve istendiğinde kimlik bilgileri sağlama.</span><span class="sxs-lookup"><span data-stu-id="3af02-143">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"` and providing the credentials when prompted.</span></span>
> * <span data-ttu-id="3af02-144">`$clusterName`Küme adını içeren bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="3af02-144">`$clusterName` is a string that contains the name of the cluster.</span></span> <span data-ttu-id="3af02-145">Bu değer kullanılarak ayarlanır `$clusterName="clustername"`.</span><span class="sxs-lookup"><span data-stu-id="3af02-145">You can set this value by using `$clusterName="clustername"`.</span></span>

<span data-ttu-id="3af02-146">Örneklerin her ikisi de aşağıdaki örneğe benzer bilgiler ile başlayan bir JSON belgesi döndürün:</span><span class="sxs-lookup"><span data-stu-id="3af02-146">Both examples return a JSON document that begins with information similar to the following example:</span></span>

```json
{
"href" : "http://10.0.0.10:8080/api/v1/clusters/CLUSTERNAME",
"Clusters" : {
    "cluster_id" : 2,
    "cluster_name" : "CLUSTERNAME",
    "health_report" : {
    "Host/stale_config" : 0,
    "Host/maintenance_state" : 0,
    "Host/host_state/HEALTHY" : 7,
    "Host/host_state/UNHEALTHY" : 0,
    "Host/host_state/HEARTBEAT_LOST" : 0,
    "Host/host_state/INIT" : 0,
    "Host/host_status/HEALTHY" : 7,
    "Host/host_status/UNHEALTHY" : 0,
    "Host/host_status/UNKNOWN" : 0,
    "Host/host_status/ALERT" : 0
    ...
```

### <a name="parsing-json-data"></a><span data-ttu-id="3af02-147">JSON verilerini ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="3af02-147">Parsing JSON data</span></span>

<span data-ttu-id="3af02-148">Aşağıdaki örnek kullanır `jq` JSON yanıt belge ayrıştırma ve yalnızca görüntülemek için `health_report` sonuçları bilgileri.</span><span class="sxs-lookup"><span data-stu-id="3af02-148">The following example uses `jq` to parse the JSON response document and display only the `health_report` information from the results.</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

<span data-ttu-id="3af02-149">PowerShell 3.0 ve üstü sağlar `ConvertFrom-Json` Powershell'den çalışmak daha kolay olan bir nesneyi JSON belgesini dönüştürür cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="3af02-149">PowerShell 3.0 and higher provides the `ConvertFrom-Json` cmdlet, which converts the JSON document into an object that is easier to work with from PowerShell.</span></span> <span data-ttu-id="3af02-150">Aşağıdaki örnek kullanır `ConvertFrom-Json` yalnızca görüntülenecek `health_report` sonuçları bilgileri.</span><span class="sxs-lookup"><span data-stu-id="3af02-150">The following example uses `ConvertFrom-Json` to display only the `health_report` information from the results.</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> <span data-ttu-id="3af02-151">Ancak bu belgenin kullanımı çoğu örneklerde `ConvertFrom-Json` yanıt belgedeki öğeleri görüntülemek için [güncelleştirme Ambari yapılandırma](#example-update-ambari-configuration) örnek jq kullanır.</span><span class="sxs-lookup"><span data-stu-id="3af02-151">While most examples in this document use `ConvertFrom-Json` to display elements from the response document, the [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span></span> <span data-ttu-id="3af02-152">Jq Bu örnekte, JSON yanıt belgeden yeni bir şablon oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3af02-152">Jq is used in this example to construct a new template from the JSON response document.</span></span>

<span data-ttu-id="3af02-153">REST API tam başvuru için bkz: [Ambari API Başvurusu V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="3af02-153">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

## <a name="example-get-the-fqdn-of-cluster-nodes"></a><span data-ttu-id="3af02-154">Örnek: küme düğümleri FQDN'sini Al</span><span class="sxs-lookup"><span data-stu-id="3af02-154">Example: Get the FQDN of cluster nodes</span></span>

<span data-ttu-id="3af02-155">Hdınsight ile çalışırken, bir küme düğümü tam etki alanı adını (FQDN) bilmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="3af02-155">When working with HDInsight, you may need to know the fully qualified domain name (FQDN) of a cluster node.</span></span> <span data-ttu-id="3af02-156">Aşağıdaki örnekleri kullanarak çeşitli düğümleri için FQDN'yi kolayca alabilir:</span><span class="sxs-lookup"><span data-stu-id="3af02-156">You can easily retrieve the FQDN for the various nodes in the cluster using the following examples:</span></span>

* <span data-ttu-id="3af02-157">**Tüm düğümler**</span><span class="sxs-lookup"><span data-stu-id="3af02-157">**All nodes**</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" \
    | jq '.items[].Hosts.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.Hosts.host_name
    ```

* <span data-ttu-id="3af02-158">**Baş düğümler**</span><span class="sxs-lookup"><span data-stu-id="3af02-158">**Head nodes**</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HDFS/components/NAMENODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/NAMENODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* <span data-ttu-id="3af02-159">**Çalışan düğümü**</span><span class="sxs-lookup"><span data-stu-id="3af02-159">**Worker nodes**</span></span>

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/DATANODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/DATANODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* <span data-ttu-id="3af02-160">**Zookeeper düğümleri**</span><span class="sxs-lookup"><span data-stu-id="3af02-160">**Zookeeper nodes**</span></span>

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

## <a name="example-get-the-internal-ip-address-of-cluster-nodes"></a><span data-ttu-id="3af02-161">Örnek: küme düğümlerinin iç IP adresi al</span><span class="sxs-lookup"><span data-stu-id="3af02-161">Example: Get the internal IP address of cluster nodes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3af02-162">Bu bölümdeki örnekleri tarafından döndürülen IP adresleri internet üzerinden doğrudan erişilebilir değildir.</span><span class="sxs-lookup"><span data-stu-id="3af02-162">The IP addresses returned by the examples in this section are not directly accessible over the internet.</span></span> <span data-ttu-id="3af02-163">Yalnızca Azure sanal Hdınsight kümesi içeren ağ içinde erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="3af02-163">They are only accessible within the Azure Virtual Network that contains the HDInsight cluster.</span></span>
>
> <span data-ttu-id="3af02-164">Hdınsight ve sanal ağlarla çalışma hakkında daha fazla bilgi için bkz: [özel bir Azure Virtual Network kullanarak genişletme Hdınsight yetenekleri](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="3af02-164">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="3af02-165">IP adresini bulmak için küme düğümleri iç tam etki alanı adını (FQDN) bilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3af02-165">To find the IP address, you must know the internal fully qualified domain name (FQDN) of the cluster nodes.</span></span> <span data-ttu-id="3af02-166">FQDN olduktan sonra ana bilgisayarın IP adresi sonra alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3af02-166">Once you have the FQDN, you can then get the IP address of the host.</span></span> <span data-ttu-id="3af02-167">Aşağıdaki örnekler ilk düğümlerinin tüm ana bilgisayar FQDN için Ambari sorgu ve ardından her ana bilgisayarın IP adresini Ambari sorgular.</span><span class="sxs-lookup"><span data-stu-id="3af02-167">The following examples first query Ambari for the FQDN of all the host nodes, then query Ambari for the IP address of each host.</span></span>

```bash
for HOSTNAME in $(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" | jq -r '.items[].Hosts.host_name')
do
    IP=$(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts/$HOSTNAME" | jq -r '.Hosts.ip')
  echo "$HOSTNAME <--> $IP"
done
```

```powershell
$uri = "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts"
$resp = Invoke-WebRequest -Uri $uri -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
foreach($item in $respObj.items) {
    $hostName = [string]$item.Hosts.host_name
    $hostInfoResp = Invoke-WebRequest -Uri "$uri/$hostName" `
        -Credential $creds
    $hostInfoObj = ConvertFrom-Json $hostInfoResp 
    $hostIp = $hostInfoObj.Hosts.ip
    "$hostName <--> $hostIp"
}
```

## <a name="example-get-the-default-storage"></a><span data-ttu-id="3af02-168">Örnek: varsayılan depolama alanı alabilir</span><span class="sxs-lookup"><span data-stu-id="3af02-168">Example: Get the default storage</span></span>

<span data-ttu-id="3af02-169">Bir Hdınsight kümesi oluştururken, varsayılan depolama alanı olarak bir Azure depolama hesabı ya da Data Lake Store küme için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3af02-169">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as the default storage for the cluster.</span></span> <span data-ttu-id="3af02-170">Ambari, Küme oluşturulduktan sonra bu bilgileri almak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3af02-170">You can use Ambari to retrieve this information after the cluster has been created.</span></span> <span data-ttu-id="3af02-171">Örneğin, okuma/veri Hdınsight dışında kapsayıcıya yazma istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="3af02-171">For example, if you want to read/write data to the container outside HDInsight.</span></span>

<span data-ttu-id="3af02-172">Aşağıdaki örnekler, varsayılan depolama yapılandırması kümeden Al:</span><span class="sxs-lookup"><span data-stu-id="3af02-172">The following examples retrieve the default storage configuration from the cluster:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
| jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'
```

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties.'fs.defaultFS'
```

> [!IMPORTANT]
> <span data-ttu-id="3af02-173">Bu örnekler sunucuya uygulanan ilk yapılandırmaya dönmek (`service_config_version=1`) bu bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="3af02-173">These examples return the first configuration applied to the server (`service_config_version=1`) which contains this information.</span></span> <span data-ttu-id="3af02-174">Küme oluşturulduktan sonra değiştiren bir değer almak, yapılandırma sürümlerini listelemek ve en son almak gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="3af02-174">If you retrieve a value that has been modified after cluster creation, you may need to list the configuration versions and retrieve the latest one.</span></span>

<span data-ttu-id="3af02-175">Dönüş değeri aşağıdaki örneklerde birine benzer:</span><span class="sxs-lookup"><span data-stu-id="3af02-175">The return value is similar to one of the following examples:</span></span>

* <span data-ttu-id="3af02-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-Bu değer, kümenin varsayılan depolama için bir Azure Storage hesabı kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="3af02-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that the cluster is using an Azure Storage account for default storage.</span></span> <span data-ttu-id="3af02-177">`ACCOUNTNAME` Değeri, depolama hesabının adıdır.</span><span class="sxs-lookup"><span data-stu-id="3af02-177">The `ACCOUNTNAME` value is the name of the storage account.</span></span> <span data-ttu-id="3af02-178">`CONTAINER` Bölümüdür depolama hesabındaki blob kapsayıcısının adı.</span><span class="sxs-lookup"><span data-stu-id="3af02-178">The `CONTAINER` portion is the name of the blob container in the storage account.</span></span> <span data-ttu-id="3af02-179">Kapsayıcı küme için HDFS uyumlu depolama köküdür.</span><span class="sxs-lookup"><span data-stu-id="3af02-179">The container is the root of the HDFS compatible storage for the cluster.</span></span>

* <span data-ttu-id="3af02-180">`adl://home`-Bu değer, kümenin varsayılan depolama için bir Azure Data Lake Store kullandığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="3af02-180">`adl://home` - This value indicates that the cluster is using an Azure Data Lake Store for default storage.</span></span>

    <span data-ttu-id="3af02-181">Data Lake Store hesap adını bulmak için aşağıdaki örneklerde kullanın:</span><span class="sxs-lookup"><span data-stu-id="3af02-181">To find the Data Lake Store account name, use the following examples:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.hostname'
    ```

    <span data-ttu-id="3af02-182">Dönüş değeri benzer `ACCOUNTNAME.azuredatalakestore.net`, burada `ACCOUNTNAME` Data Lake Store hesabı adıdır.</span><span class="sxs-lookup"><span data-stu-id="3af02-182">The return value is similar to `ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is the name of the Data Lake Store account.</span></span>

    <span data-ttu-id="3af02-183">Küme için depolama alanını içeren bir Data Lake Store içinde dizin bulmak için aşağıdaki örneklerde kullanın:</span><span class="sxs-lookup"><span data-stu-id="3af02-183">To find the directory within Data Lake Store that contains the storage for the cluster, use the following examples:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.mountpoint'
    ```

    <span data-ttu-id="3af02-184">Dönüş değeri benzer `/clusters/CLUSTERNAME/`.</span><span class="sxs-lookup"><span data-stu-id="3af02-184">The return value is similar to `/clusters/CLUSTERNAME/`.</span></span> <span data-ttu-id="3af02-185">Bu değer, Data Lake Store hesabındaki bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="3af02-185">This value is a path within the Data Lake Store account.</span></span> <span data-ttu-id="3af02-186">Küme için HDFS uyumlu bir dosya sisteminin kök yoludur.</span><span class="sxs-lookup"><span data-stu-id="3af02-186">This path is the root of the HDFS compatible file system for the cluster.</span></span> 

> [!NOTE]
> <span data-ttu-id="3af02-187">`Get-AzureRmHDInsightCluster` Tarafından sağlanan cmdlet [Azure PowerShell](/powershell/azure/overview) ayrıca küme için Depolama bilgileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3af02-187">The `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](/powershell/azure/overview) also returns the storage information for the cluster.</span></span>


## <a name="example-get-configuration"></a><span data-ttu-id="3af02-188">Örnek: Get yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3af02-188">Example: Get configuration</span></span>

1. <span data-ttu-id="3af02-189">Kümeniz için kullanılabilir olan yapılandırmaları alın.</span><span class="sxs-lookup"><span data-stu-id="3af02-189">Get the configurations that are available for your cluster.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    <span data-ttu-id="3af02-190">Bu örnek geçerli yapılandırmasını içeren bir JSON belgesi döndürür (tarafından tanımlanan *etiketi* değeri) kümeye yüklü bileşenleri için.</span><span class="sxs-lookup"><span data-stu-id="3af02-190">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="3af02-191">Aşağıdaki örnek bir Spark kümesi türünden döndürülen verileri bir alıntı aynıdır.</span><span class="sxs-lookup"><span data-stu-id="3af02-191">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
   ```json
   "spark-metrics-properties" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-fairscheduler" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-sparkconf" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   }
   ```

2. <span data-ttu-id="3af02-192">İlgilendiğiniz bileşeni için yapılandırma alın.</span><span class="sxs-lookup"><span data-stu-id="3af02-192">Get the configuration for the component that you are interested in.</span></span> <span data-ttu-id="3af02-193">Aşağıdaki örnekte `INITIAL` etiket değeri ile önceki istekten döndürdü.</span><span class="sxs-lookup"><span data-stu-id="3af02-193">In the following example, replace `INITIAL` with the tag value returned from the previous request.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    <span data-ttu-id="3af02-194">Bu örnek için geçerli yapılandırmasını içeren bir JSON belgesi döndürür `core-site` bileşeni.</span><span class="sxs-lookup"><span data-stu-id="3af02-194">This example returns a JSON document containing the current configuration for the `core-site` component.</span></span>

## <a name="example-update-configuration"></a><span data-ttu-id="3af02-195">Örnek: Güncelleştirme yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3af02-195">Example: Update configuration</span></span>

1. <span data-ttu-id="3af02-196">"İstenen yapılandırma" Ambari depolar geçerli yapılandırmasını alın:</span><span class="sxs-lookup"><span data-stu-id="3af02-196">Get the current configuration, which Ambari stores as the "desired configuration":</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="3af02-197">Bu örnek geçerli yapılandırmasını içeren bir JSON belgesi döndürür (tarafından tanımlanan *etiketi* değeri) kümeye yüklü bileşenleri için.</span><span class="sxs-lookup"><span data-stu-id="3af02-197">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="3af02-198">Aşağıdaki örnek bir Spark kümesi türünden döndürülen verileri bir alıntı aynıdır.</span><span class="sxs-lookup"><span data-stu-id="3af02-198">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
    ```json
    "spark-metrics-properties" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-fairscheduler" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-sparkconf" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    }
    ```
   
    <span data-ttu-id="3af02-199">Bu listeden bileşenin adını kopyalamanız gerekir (örneğin, **spark\_thrift\_sparkconf** ve **etiketi** değeri.</span><span class="sxs-lookup"><span data-stu-id="3af02-199">From this list, you need to copy the name of the component (for example, **spark\_thrift\_sparkconf** and the **tag** value.</span></span>

2. <span data-ttu-id="3af02-200">Etiket ve Bileşen yapılandırmasını aşağıdaki komutları kullanarak Al:</span><span class="sxs-lookup"><span data-stu-id="3af02-200">Retrieve the configuration for the component and tag by using the following commands:</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=spark-thrift-sparkconf&tag=INITIAL" \
    | jq --arg newtag $(echo version$(date +%s%N)) '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    ```powershell
    $epoch = Get-Date -Year 1970 -Month 1 -Day 1 -Hour 0 -Minute 0 -Second 0
    $now = Get-Date
    $unixTimeStamp = [math]::truncate($now.ToUniversalTime().Subtract($epoch).TotalMilliSeconds)
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=spark-thrift-sparkconf&tag=INITIAL" `
        -Credential $creds
    $resp.Content | jq --arg newtag "version$unixTimeStamp" '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    > [!NOTE]
    > <span data-ttu-id="3af02-201">Değiştir **spark thrift sparkconf** ve **ilk** bileşeni ve yapılandırmasını almak istediğiniz etiketi.</span><span class="sxs-lookup"><span data-stu-id="3af02-201">Replace **spark-thrift-sparkconf** and **INITIAL** with the component and tag that you want to retrieve the configuration for.</span></span>
   
    <span data-ttu-id="3af02-202">Jq Hdınsight'ta yeni bir yapılandırma şablonuna alınan verileri döndürmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3af02-202">Jq is used to turn the data retrieved from HDInsight into a new configuration template.</span></span> <span data-ttu-id="3af02-203">Özellikle, bu örnekler aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3af02-203">Specifically, these examples perform the following actions:</span></span>
   
    * <span data-ttu-id="3af02-204">"Sürüm" dizesi ve depolanan tarihi içeren benzersiz bir değer oluşturur `newtag`.</span><span class="sxs-lookup"><span data-stu-id="3af02-204">Creates a unique value containing the string "version" and the date, which is stored in `newtag`.</span></span>

    * <span data-ttu-id="3af02-205">Yeni istenen yapılandırma için bir kök belge oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3af02-205">Creates a root document for the new desired configuration.</span></span>

    * <span data-ttu-id="3af02-206">İçeriğini alır `.items[]` dizi ve altında ekler **desired_config** öğesi.</span><span class="sxs-lookup"><span data-stu-id="3af02-206">Gets the contents of the `.items[]` array and adds it under the **desired_config** element.</span></span>

    * <span data-ttu-id="3af02-207">Siler `href`, `version`, ve `Config` öğeleri, bu öğeleri gerekli olmayan yeni bir yapılandırma göndermek için.</span><span class="sxs-lookup"><span data-stu-id="3af02-207">Deletes the `href`, `version`, and `Config` elements, as these elements aren't needed to submit a new configuration.</span></span>

    * <span data-ttu-id="3af02-208">Ekler bir `tag` değerini bir öğesiyle `version#################`.</span><span class="sxs-lookup"><span data-stu-id="3af02-208">Adds a `tag` element with a value of `version#################`.</span></span> <span data-ttu-id="3af02-209">Öğesinin sayısal bölümü geçerli tarih temel alır.</span><span class="sxs-lookup"><span data-stu-id="3af02-209">The numeric portion is based on the current date.</span></span> <span data-ttu-id="3af02-210">Her yapılandırma benzersiz bir etiketi olması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="3af02-210">Each configuration must have a unique tag.</span></span>
     
    <span data-ttu-id="3af02-211">Son olarak, verileri kaydedilen `newconfig.json` belge.</span><span class="sxs-lookup"><span data-stu-id="3af02-211">Finally, the data is saved to the `newconfig.json` document.</span></span> <span data-ttu-id="3af02-212">Belge yapısı aşağıdaki örneğe benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="3af02-212">The document structure should appear similar to the following example:</span></span>
     
     ```json
    {
        "Clusters": {
            "desired_config": {
            "tag": "version1459260185774265400",
            "type": "spark-thrift-sparkconf",
            "properties": {
                ....
            },
            "properties_attributes": {
                ....
            }
        }
    }
    ```

3. <span data-ttu-id="3af02-213">Açık `newconfig.json` belge ve değiştirebilir ve ekleyebilir değerleri `properties` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3af02-213">Open the `newconfig.json` document and modify/add values in the `properties` object.</span></span> <span data-ttu-id="3af02-214">Aşağıdaki örnek değerini değiştirir `"spark.yarn.am.memory"` gelen `"1g"` için `"3g"`.</span><span class="sxs-lookup"><span data-stu-id="3af02-214">The following example changes the value of `"spark.yarn.am.memory"` from `"1g"` to `"3g"`.</span></span> <span data-ttu-id="3af02-215">Ayrıca ekler `"spark.kryoserializer.buffer.max"` değerini `"256m"`.</span><span class="sxs-lookup"><span data-stu-id="3af02-215">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span></span>
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    <span data-ttu-id="3af02-216">Yapmayı değişiklikleri tamamladıktan sonra dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3af02-216">Save the file once you are done making modifications.</span></span>

4. <span data-ttu-id="3af02-217">Ambari güncelleştirilmiş yapılandırmaya göndermek için aşağıdaki komutları kullanın.</span><span class="sxs-lookup"><span data-stu-id="3af02-217">Use the following commands to submit the updated configuration to Ambari.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" -X PUT -d @newconfig.json "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
    ```

    ```powershell
    $newConfig = Get-Content .\newconfig.json
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body $newConfig
    $resp.Content
    ```
   
    <span data-ttu-id="3af02-218">Bu komutlar içeriğini gönderme **newconfig.json** yeni istenen yapılandırma olarak dosyaya.</span><span class="sxs-lookup"><span data-stu-id="3af02-218">These commands submit the contents of the **newconfig.json** file to the cluster as the new desired configuration.</span></span> <span data-ttu-id="3af02-219">İstek bir JSON belgesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3af02-219">The request returns a JSON document.</span></span> <span data-ttu-id="3af02-220">**VersionTag** bu belgedeki öğe gönderdiğiniz, sürüm eşleşmelidir ve **yapılandırmalar** nesne, istenen yapılandırma değişiklikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="3af02-220">The **versionTag** element in this document should match the version you submitted, and the **configs** object contains the configuration changes you requested.</span></span>

### <a name="example-restart-a-service-component"></a><span data-ttu-id="3af02-221">Örnek: bir hizmet bileşeni yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="3af02-221">Example: Restart a service component</span></span>

<span data-ttu-id="3af02-222">Bu noktada, Ambari web kullanıcı Arabirimi bakarsanız, Spark hizmeti yeni yapılandırmanın etkili olması için önce yeniden başlatılması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="3af02-222">At this point, if you look at the Ambari web UI, the Spark service indicates that it needs to be restarted before the new configuration can take effect.</span></span> <span data-ttu-id="3af02-223">Hizmetini yeniden başlatmak için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="3af02-223">Use the following steps to restart the service.</span></span>

1. <span data-ttu-id="3af02-224">Bir Spark hizmeti için bakım modunu etkinleştirmek için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="3af02-224">Use the following to enable maintenance mode for the Spark service:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}'
    $resp.Content
    ```
   
    <span data-ttu-id="3af02-225">Bu komutlar bir JSON belgesi bakım modunu açar sunucusuna gönderir.</span><span class="sxs-lookup"><span data-stu-id="3af02-225">These commands send a JSON document to the server that turns on maintenance mode.</span></span> <span data-ttu-id="3af02-226">Hizmet artık aşağıdaki isteği kullanarak bakım modunda olduğunu doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3af02-226">You can verify that the service is now in maintenance mode using the following request:</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK" \
    | jq .ServiceInfo.maintenance_state
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK2" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.ServiceInfo.maintenance_state
    ```
   
    <span data-ttu-id="3af02-227">Dönüş değeri `ON`.</span><span class="sxs-lookup"><span data-stu-id="3af02-227">The return value is `ON`.</span></span>

2. <span data-ttu-id="3af02-228">Ardından, hizmeti kapatmak için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="3af02-228">Next, use the following to turn off the service:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}'
    $resp.Content
    ```
    
    <span data-ttu-id="3af02-229">Yanıt aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="3af02-229">The response is similar to the following example:</span></span>
   
    ```json
    {
        "href" : "http://10.0.0.18:8080/api/v1/clusters/CLUSTERNAME/requests/29",
        "Requests" : {
            "id" : 29,
            "status" : "Accepted"
        }
    }
    ```
    
    > [!IMPORTANT]
    > <span data-ttu-id="3af02-230">`href` Bu URI tarafından döndürülen değer, küme düğümü iç IP adresini kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="3af02-230">The `href` value returned by this URI is using the internal IP address of the cluster node.</span></span> <span data-ttu-id="3af02-231">Buradan küme dışında kullanmak için '10.0.0.18:8080' bölümüne küme FQDN ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3af02-231">To use it from outside the cluster, replace the \`10.0.0.18:8080' portion with the FQDN of the cluster.</span></span> 
    
    <span data-ttu-id="3af02-232">Aşağıdaki komutları isteğinin durumunu al:</span><span class="sxs-lookup"><span data-stu-id="3af02-232">The following commands retrieve the status of the request:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/requests/29" \
    | jq .Requests.request_status
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/requests/29" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.Requests.request_status
    ```

    <span data-ttu-id="3af02-233">Yanıtın `COMPLETED` istek tamamladığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="3af02-233">A response of `COMPLETED` indicates that the request has finished.</span></span>

3. <span data-ttu-id="3af02-234">Önceki istek tamamlandığında, hizmeti başlatmak için aşağıdakileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="3af02-234">Once the previous request completes, use the following to start the service.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```
   
    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}'
    ```
    <span data-ttu-id="3af02-235">Hizmet yeni yapılandırmayı şimdi kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="3af02-235">The service is now using the new configuration.</span></span>

4. <span data-ttu-id="3af02-236">Son olarak, bakım modunu devre dışı bırakmak için aşağıdakileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="3af02-236">Finally, use the following to turn off maintenance mode.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}'
    ```

## <a name="next-steps"></a><span data-ttu-id="3af02-237">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3af02-237">Next steps</span></span>

<span data-ttu-id="3af02-238">REST API tam başvuru için bkz: [Ambari API Başvurusu V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="3af02-238">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

