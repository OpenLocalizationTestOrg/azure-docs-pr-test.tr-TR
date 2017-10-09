---
title: "aaaMonitor ve Hadoop Ambari REST API - Azure Hdınsight ile yönetme | Microsoft Docs"
description: "Bilgi nasıl toouse Ambari toomonitor ve Azure hdınsight'ta Hadoop kümelerini yönetebilirsiniz. Bu belgede nasıl toouse hello Ambari REST API Hdınsight ile dahil kümeleri öğreneceksiniz."
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
ms.openlocfilehash: 1866a77c8e402231bccbcfba7174253aca41339b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-rest-api"></a><span data-ttu-id="b4949-104">Merhaba Ambari REST API kullanarak Hdınsight kümelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="b4949-104">Manage HDInsight clusters by using hello Ambari REST API</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="b4949-105">Nasıl toouse Ambari REST API toomanage hello ve Azure hdınsight'ta Hadoop kümelerini izleme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="b4949-105">Learn how toouse hello Ambari REST API toomanage and monitor Hadoop clusters in Azure HDInsight.</span></span>

<span data-ttu-id="b4949-106">Apache Ambari hello yönetimi ve Hadoop kümesi kolay toouse web kullanıcı Arabirimi ve REST API'si sağlayarak izlemenin basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="b4949-106">Apache Ambari simplifies hello management and monitoring of a Hadoop cluster by providing an easy toouse web UI and REST API.</span></span> <span data-ttu-id="b4949-107">Ambari hello Linux işletim sistemi kullanan Hdınsight kümelerine dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="b4949-107">Ambari is included on HDInsight clusters that use hello Linux operating system.</span></span> <span data-ttu-id="b4949-108">Ambari toomonitor hello küme kullanın ve yapılandırma değişikliklerini yapın.</span><span class="sxs-lookup"><span data-stu-id="b4949-108">You can use Ambari toomonitor hello cluster and make configuration changes.</span></span>

## <span data-ttu-id="b4949-109"><a id="whatis"></a>Ambari nedir</span><span class="sxs-lookup"><span data-stu-id="b4949-109"><a id="whatis"></a>What is Ambari</span></span>

<span data-ttu-id="b4949-110">[Apache Ambari](http://ambari.apache.org) web kullanılan tooprovision olması, yönetmek ve Hadoop kümelerini izleme kullanıcı Arabirimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b4949-110">[Apache Ambari](http://ambari.apache.org) provides web UI that can be used tooprovision, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="b4949-111">Geliştiriciler tümleştirebilir Bu yetenekler uygulamalarına hello kullanarak [Ambari REST API'leri](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="b4949-111">Developers can integrate these capabilities into their applications by using hello [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="b4949-112">Ambari, Linux tabanlı Hdınsight kümeleri ile varsayılan olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b4949-112">Ambari is provided by default with Linux-based HDInsight clusters.</span></span>

## <a name="how-toouse-hello-ambari-rest-api"></a><span data-ttu-id="b4949-113">Nasıl toouse hello Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="b4949-113">How toouse hello Ambari REST API</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4949-114">Merhaba bilgileri ve bu belgedeki örneklerde Linux işletim sistemi kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b4949-114">hello information and examples in this document require an HDInsight cluster that uses Linux operating system.</span></span> <span data-ttu-id="b4949-115">Daha fazla bilgi için bkz: [Hdınsight kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b4949-115">For more information, see [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

<span data-ttu-id="b4949-116">Bu belgedeki örneklerde Hello hello Uluç Kabuğu (bash) ve PowerShell için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b4949-116">hello examples in this document are provided for both hello Bourne shell (bash) and PowerShell.</span></span> <span data-ttu-id="b4949-117">örnekler GNU ile test edilmiş hello bash 4.3.11 bash, ancak diğer UNIX Kabukları ile çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4949-117">hello bash examples were tested with GNU bash 4.3.11, but should work with other Unix shells.</span></span> <span data-ttu-id="b4949-118">Merhaba PowerShell örnekleri PowerShell 5.0 ile test edilmiş, ancak PowerShell 3.0 veya üstünü çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4949-118">hello PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span></span>

<span data-ttu-id="b4949-119">Merhaba kullanıyorsanız __Uluç Kabuk__ (Bash) hello aşağıdaki yüklü olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="b4949-119">If using hello __Bourne shell__ (Bash), you must have hello following installed:</span></span>

* <span data-ttu-id="b4949-120">[cURL](http://curl.haxx.se/): cURL REST API'leri ile kullanılan toowork hello komut satırından olabilir bir yardımcı olan.</span><span class="sxs-lookup"><span data-stu-id="b4949-120">[cURL](http://curl.haxx.se/): cURL is a utility that can be used toowork with REST APIs from hello command line.</span></span> <span data-ttu-id="b4949-121">Bu belgede, hello Ambari REST API ile kullanılan toocommunicate değil.</span><span class="sxs-lookup"><span data-stu-id="b4949-121">In this document, it is used toocommunicate with hello Ambari REST API.</span></span>

<span data-ttu-id="b4949-122">Bash veya PowerShell kullanarak olup olmadığını oluşturmuş olmanız da gerekir [jq](https://stedolan.github.io/jq/) yüklü.</span><span class="sxs-lookup"><span data-stu-id="b4949-122">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span></span> <span data-ttu-id="b4949-123">Jq JSON belgeleri ile çalışmaya yönelik bir yardımcı programdır.</span><span class="sxs-lookup"><span data-stu-id="b4949-123">Jq is a utility for working with JSON documents.</span></span> <span data-ttu-id="b4949-124">İçinde kullanılan **tüm** Bash örnekler, hello ve **bir** hello PowerShell örnekler.</span><span class="sxs-lookup"><span data-stu-id="b4949-124">It is used in **all** hello Bash examples, and **one** of hello PowerShell examples.</span></span>

### <a name="base-uri-for-ambari-rest-api"></a><span data-ttu-id="b4949-125">Temel Ambari Rest API için URI</span><span class="sxs-lookup"><span data-stu-id="b4949-125">Base URI for Ambari Rest API</span></span>

<span data-ttu-id="b4949-126">Merhaba hello Hdınsight Ambari REST API için ana URI olan https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, burada **CLUSTERNAME** hello kümenizin adıdır.</span><span class="sxs-lookup"><span data-stu-id="b4949-126">hello base URI for hello Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4949-127">Hello Hello küme adı tam olarak nitelenmiş sırasında etki alanı adı (FQDN) bölümü hello URI (CLUSTERNAME.azurehdinsight.net) büyük/küçük harfe duyarlıdır, diğer oluşum hello URI içindeki büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="b4949-127">While hello cluster name in hello fully qualified domain name (FQDN) part of hello URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in hello URI are case-sensitive.</span></span> <span data-ttu-id="b4949-128">Örneğin, kümenizi adlı `MyCluster`, geçerli URI'ler hello aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b4949-128">For example, if your cluster is named `MyCluster`, hello following are valid URIs:</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> <span data-ttu-id="b4949-129">URI'ler hello hello adı ikinci oluşum hello değil çünkü bir hata döndürür hello aşağıdaki durumu düzeltin.</span><span class="sxs-lookup"><span data-stu-id="b4949-129">hello following URIs return an error because hello second occurrence of hello name is not hello correct case.</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a><span data-ttu-id="b4949-130">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="b4949-130">Authentication</span></span>

<span data-ttu-id="b4949-131">Hdınsight üzerinde tooAmbari bağlanırken HTTPS gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b4949-131">Connecting tooAmbari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="b4949-132">Merhaba yönetici hesabı adını kullan (Merhaba varsayılandır **yönetici**) ve küme oluşturma sırasında sağlanan parola.</span><span class="sxs-lookup"><span data-stu-id="b4949-132">Use hello admin account name (hello default is **admin**) and password you provided during cluster creation.</span></span>

## <a name="examples-authentication-and-parsing-json"></a><span data-ttu-id="b4949-133">Örnekler: Kimlik doğrulaması ve JSON ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="b4949-133">Examples: Authentication and parsing JSON</span></span>

<span data-ttu-id="b4949-134">Örnek hello nasıl toomake hello bir GET isteği temel Ambari REST API gösterir:</span><span class="sxs-lookup"><span data-stu-id="b4949-134">hello following examples demonstrate how toomake a GET request against hello base Ambari REST API:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> <span data-ttu-id="b4949-135">Bu belgedeki Hello Bash örneklerde varsayımlar aşağıdaki hello olun:</span><span class="sxs-lookup"><span data-stu-id="b4949-135">hello Bash examples in this document make hello following assumptions:</span></span>
>
> * <span data-ttu-id="b4949-136">Merhaba oturum açma için hello küme adıdır hello varsayılan değerini `admin`.</span><span class="sxs-lookup"><span data-stu-id="b4949-136">hello login name for hello cluster is hello default value of `admin`.</span></span>
> * <span data-ttu-id="b4949-137">`$PASSWORD`Merhaba Hdınsight oturum açma komut Hello parolasını içerir.</span><span class="sxs-lookup"><span data-stu-id="b4949-137">`$PASSWORD` contains hello password for hello HDInsight login command.</span></span> <span data-ttu-id="b4949-138">Bu değer kullanılarak ayarlanır `PASSWORD='mypassword'`.</span><span class="sxs-lookup"><span data-stu-id="b4949-138">You can set this value by using `PASSWORD='mypassword'`.</span></span>
> * <span data-ttu-id="b4949-139">`$CLUSTERNAME`Merhaba hello küme adını içerir.</span><span class="sxs-lookup"><span data-stu-id="b4949-139">`$CLUSTERNAME` contains hello name of hello cluster.</span></span> <span data-ttu-id="b4949-140">Bu değer kullanılarak ayarlanır`set CLUSTERNAME='clustername'`</span><span class="sxs-lookup"><span data-stu-id="b4949-140">You can set this value by using `set CLUSTERNAME='clustername'`</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> <span data-ttu-id="b4949-141">Bu belgedeki Hello PowerShell örnekleri varsayımlar aşağıdaki hello olun:</span><span class="sxs-lookup"><span data-stu-id="b4949-141">hello PowerShell examples in this document make hello following assumptions:</span></span>
>
> * <span data-ttu-id="b4949-142">`$creds`hello Yöneticisi oturum açma ve hello küme parolasını içeren bir kimlik bilgisi nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="b4949-142">`$creds` is a credential object that contains hello admin login and password for hello cluster.</span></span> <span data-ttu-id="b4949-143">Bu değer kullanılarak ayarlanır `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` ve istendiğinde hello kimlik bilgileri sağlama.</span><span class="sxs-lookup"><span data-stu-id="b4949-143">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` and providing hello credentials when prompted.</span></span>
> * <span data-ttu-id="b4949-144">`$clusterName`Merhaba hello küme adını içeren bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="b4949-144">`$clusterName` is a string that contains hello name of hello cluster.</span></span> <span data-ttu-id="b4949-145">Bu değer kullanılarak ayarlanır `$clusterName="clustername"`.</span><span class="sxs-lookup"><span data-stu-id="b4949-145">You can set this value by using `$clusterName="clustername"`.</span></span>

<span data-ttu-id="b4949-146">Örneklerin her ikisi de bilgi benzer toohello aşağıdaki örneğine ile başlayan bir JSON belgesi döndürün:</span><span class="sxs-lookup"><span data-stu-id="b4949-146">Both examples return a JSON document that begins with information similar toohello following example:</span></span>

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

### <a name="parsing-json-data"></a><span data-ttu-id="b4949-147">JSON verilerini ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="b4949-147">Parsing JSON data</span></span>

<span data-ttu-id="b4949-148">Merhaba aşağıdaki örnek kullanır `jq` tooparse hello JSON yanıt belge ve yalnızca hello görüntülemek `health_report` hello sonuçlarından bilgi.</span><span class="sxs-lookup"><span data-stu-id="b4949-148">hello following example uses `jq` tooparse hello JSON response document and display only hello `health_report` information from hello results.</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

<span data-ttu-id="b4949-149">PowerShell 3.0 ve üstü sağlar hello `ConvertFrom-Json` hello JSON belgesi ile daha kolay toowork powershell'den bir nesne dönüştürür cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="b4949-149">PowerShell 3.0 and higher provides hello `ConvertFrom-Json` cmdlet, which converts hello JSON document into an object that is easier toowork with from PowerShell.</span></span> <span data-ttu-id="b4949-150">Merhaba aşağıdaki örnek kullanır `ConvertFrom-Json` toodisplay yalnızca hello `health_report` hello sonuçlarından bilgi.</span><span class="sxs-lookup"><span data-stu-id="b4949-150">hello following example uses `ConvertFrom-Json` toodisplay only hello `health_report` information from hello results.</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> <span data-ttu-id="b4949-151">Ancak bu belgenin kullanımı çoğu örneklerde `ConvertFrom-Json` toodisplay öğeleri hello yanıt belgeden hello [güncelleştirme Ambari yapılandırma](#example-update-ambari-configuration) örnek jq kullanır.</span><span class="sxs-lookup"><span data-stu-id="b4949-151">While most examples in this document use `ConvertFrom-Json` toodisplay elements from hello response document, hello [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span></span> <span data-ttu-id="b4949-152">Bu örnek tooconstruct Jq kullanılan hello JSON yanıt belgeden yeni bir şablon.</span><span class="sxs-lookup"><span data-stu-id="b4949-152">Jq is used in this example tooconstruct a new template from hello JSON response document.</span></span>

<span data-ttu-id="b4949-153">Merhaba REST API tam başvuru için bkz: [Ambari API Başvurusu V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="b4949-153">For a complete reference of hello REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

## <a name="example-get-hello-fqdn-of-cluster-nodes"></a><span data-ttu-id="b4949-154">Örnek: Merhaba küme düğümlerinin FQDN Al</span><span class="sxs-lookup"><span data-stu-id="b4949-154">Example: Get hello FQDN of cluster nodes</span></span>

<span data-ttu-id="b4949-155">Hdınsight ile çalışırken, bir küme düğümü tooknow hello tam etki alanı adı (FQDN) gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="b4949-155">When working with HDInsight, you may need tooknow hello fully qualified domain name (FQDN) of a cluster node.</span></span> <span data-ttu-id="b4949-156">Merhaba FQDN hello için çeşitli örnekler aşağıdaki hello kullanarak hello kümedeki düğümlerin kolayca alabilir:</span><span class="sxs-lookup"><span data-stu-id="b4949-156">You can easily retrieve hello FQDN for hello various nodes in hello cluster using hello following examples:</span></span>

* <span data-ttu-id="b4949-157">**Tüm düğümler**</span><span class="sxs-lookup"><span data-stu-id="b4949-157">**All nodes**</span></span>

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

* <span data-ttu-id="b4949-158">**Baş düğümler**</span><span class="sxs-lookup"><span data-stu-id="b4949-158">**Head nodes**</span></span>

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

* <span data-ttu-id="b4949-159">**Çalışan düğümü**</span><span class="sxs-lookup"><span data-stu-id="b4949-159">**Worker nodes**</span></span>

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

* <span data-ttu-id="b4949-160">**Zookeeper düğümleri**</span><span class="sxs-lookup"><span data-stu-id="b4949-160">**Zookeeper nodes**</span></span>

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

## <a name="example-get-hello-internal-ip-address-of-cluster-nodes"></a><span data-ttu-id="b4949-161">Örnek: küme düğümlerinin hello iç IP adresi al</span><span class="sxs-lookup"><span data-stu-id="b4949-161">Example: Get hello internal IP address of cluster nodes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4949-162">Internet üzerinden erişilebilir değil hello doğrudan bu bölümdeki hello örnekleri tarafından döndürülen hello IP adresleridir.</span><span class="sxs-lookup"><span data-stu-id="b4949-162">hello IP addresses returned by hello examples in this section are not directly accessible over hello internet.</span></span> <span data-ttu-id="b4949-163">Yalnızca hello hello Hdınsight kümesi içeren Azure sanal ağ içinde erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="b4949-163">They are only accessible within hello Azure Virtual Network that contains hello HDInsight cluster.</span></span>
>
> <span data-ttu-id="b4949-164">Hdınsight ve sanal ağlarla çalışma hakkında daha fazla bilgi için bkz: [özel bir Azure Virtual Network kullanarak genişletme Hdınsight yetenekleri](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="b4949-164">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="b4949-165">toofind başlangıç IP adresi, küme düğümleri hello iç tam etki alanı adını (FQDN) hello bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4949-165">toofind hello IP address, you must know hello internal fully qualified domain name (FQDN) of hello cluster nodes.</span></span> <span data-ttu-id="b4949-166">Merhaba FQDN olduktan sonra başlangıç IP adresi hello konağının sonra alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4949-166">Once you have hello FQDN, you can then get hello IP address of hello host.</span></span> <span data-ttu-id="b4949-167">Merhaba aşağıdaki örneklerde önce tüm hello konak düğümleri FQDN'sini hello için Ambari sorgu ve ardından Ambari başlangıç IP adresi her konak için sorgular.</span><span class="sxs-lookup"><span data-stu-id="b4949-167">hello following examples first query Ambari for hello FQDN of all hello host nodes, then query Ambari for hello IP address of each host.</span></span>

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

## <a name="example-get-hello-default-storage"></a><span data-ttu-id="b4949-168">Örnek: Merhaba varsayılan depolama Al</span><span class="sxs-lookup"><span data-stu-id="b4949-168">Example: Get hello default storage</span></span>

<span data-ttu-id="b4949-169">Bir Hdınsight kümesi oluştururken hello varsayılan depolama alanı olarak bir Azure depolama hesabı veya Data Lake Store hello küme için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4949-169">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as hello default storage for hello cluster.</span></span> <span data-ttu-id="b4949-170">Merhaba Küme oluşturulduktan sonra bu bilgileri Ambari tooretrieve kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4949-170">You can use Ambari tooretrieve this information after hello cluster has been created.</span></span> <span data-ttu-id="b4949-171">Örneğin, tooread/yazma veri toohello kapsayıcı Hdınsight dışında istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="b4949-171">For example, if you want tooread/write data toohello container outside HDInsight.</span></span>

<span data-ttu-id="b4949-172">Merhaba aşağıdaki örneklerde hello varsayılan depolama yapılandırması hello kümeden Al:</span><span class="sxs-lookup"><span data-stu-id="b4949-172">hello following examples retrieve hello default storage configuration from hello cluster:</span></span>

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
> <span data-ttu-id="b4949-173">Bu örnekler hello ilk uygulanan yapılandırma toohello sunucu dönüşü (`service_config_version=1`) bu bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="b4949-173">These examples return hello first configuration applied toohello server (`service_config_version=1`) which contains this information.</span></span> <span data-ttu-id="b4949-174">Küme oluşturulduktan sonra değiştiren bir değer almak, toolist hello yapılandırma sürümlerini gerekir ve hello en son almak.</span><span class="sxs-lookup"><span data-stu-id="b4949-174">If you retrieve a value that has been modified after cluster creation, you may need toolist hello configuration versions and retrieve hello latest one.</span></span>

<span data-ttu-id="b4949-175">Merhaba dönüş değeri örnek Merhaba, benzer tooone şöyledir:</span><span class="sxs-lookup"><span data-stu-id="b4949-175">hello return value is similar tooone of hello following examples:</span></span>

* <span data-ttu-id="b4949-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-Bu değer bu hello küme varsayılan depolama için bir Azure Storage hesabı kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="b4949-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that hello cluster is using an Azure Storage account for default storage.</span></span> <span data-ttu-id="b4949-177">Merhaba `ACCOUNTNAME` hello hello depolama hesabının adını bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="b4949-177">hello `ACCOUNTNAME` value is hello name of hello storage account.</span></span> <span data-ttu-id="b4949-178">Merhaba `CONTAINER` bölümüdür hello blob kapsayıcısının hello depolama hesabındaki hello adı.</span><span class="sxs-lookup"><span data-stu-id="b4949-178">hello `CONTAINER` portion is hello name of hello blob container in hello storage account.</span></span> <span data-ttu-id="b4949-179">Merhaba, hello hello kümesi için HDFS uyumlu depolama hello kökündeki kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="b4949-179">hello container is hello root of hello HDFS compatible storage for hello cluster.</span></span>

* <span data-ttu-id="b4949-180">`adl://home`-Bu değer bu hello küme varsayılan depolama için bir Azure Data Lake Store kullandığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b4949-180">`adl://home` - This value indicates that hello cluster is using an Azure Data Lake Store for default storage.</span></span>

    <span data-ttu-id="b4949-181">toofind hello Data Lake Store hesap adını, örnek hello kullan:</span><span class="sxs-lookup"><span data-stu-id="b4949-181">toofind hello Data Lake Store account name, use hello following examples:</span></span>

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

    <span data-ttu-id="b4949-182">Merhaba dönüş değeri çok benzer`ACCOUNTNAME.azuredatalakestore.net`, burada `ACCOUNTNAME` hello Data Lake Store hesabı hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="b4949-182">hello return value is similar too`ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is hello name of hello Data Lake Store account.</span></span>

    <span data-ttu-id="b4949-183">toofind hello dizini hello küme, örnek kullanım hello için hello depolama alanını içeren bir Data Lake Store içinde:</span><span class="sxs-lookup"><span data-stu-id="b4949-183">toofind hello directory within Data Lake Store that contains hello storage for hello cluster, use hello following examples:</span></span>

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

    <span data-ttu-id="b4949-184">Merhaba dönüş değeri çok benzer`/clusters/CLUSTERNAME/`.</span><span class="sxs-lookup"><span data-stu-id="b4949-184">hello return value is similar too`/clusters/CLUSTERNAME/`.</span></span> <span data-ttu-id="b4949-185">Bu değer, hello Data Lake Store hesabı içinde bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="b4949-185">This value is a path within hello Data Lake Store account.</span></span> <span data-ttu-id="b4949-186">Bu yol hello hello hello küme için HDFS uyumlu bir dosya sistemi köküdür.</span><span class="sxs-lookup"><span data-stu-id="b4949-186">This path is hello root of hello HDFS compatible file system for hello cluster.</span></span> 

> [!NOTE]
> <span data-ttu-id="b4949-187">Merhaba `Get-AzureRmHDInsightCluster` tarafından sağlanan cmdlet [Azure PowerShell](/powershell/azure/overview) döndürür hello küme için depolama bilgilerini de hello.</span><span class="sxs-lookup"><span data-stu-id="b4949-187">hello `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](/powershell/azure/overview) also returns hello storage information for hello cluster.</span></span>


## <a name="example-get-configuration"></a><span data-ttu-id="b4949-188">Örnek: Get yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b4949-188">Example: Get configuration</span></span>

1. <span data-ttu-id="b4949-189">Kümeniz için uygun olan hello yapılandırmalarını alma.</span><span class="sxs-lookup"><span data-stu-id="b4949-189">Get hello configurations that are available for your cluster.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    <span data-ttu-id="b4949-190">Bu örnek hello geçerli yapılandırmasını içeren bir JSON belgesi döndürür (Merhaba tarafından tanımlanan *etiketi* değeri) hello kümeye yüklü hello bileşenleri için.</span><span class="sxs-lookup"><span data-stu-id="b4949-190">This example returns a JSON document containing hello current configuration (identified by hello *tag* value) for hello components installed on hello cluster.</span></span> <span data-ttu-id="b4949-191">Merhaba aşağıdaki bir Spark kümesi türünden döndürülen hello verilerden bir alıntı örnektir.</span><span class="sxs-lookup"><span data-stu-id="b4949-191">hello following example is an excerpt from hello data returned from a Spark cluster type.</span></span>
   
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

2. <span data-ttu-id="b4949-192">İlgilendiğiniz hello bileşeni için Hello yapılandırma alın.</span><span class="sxs-lookup"><span data-stu-id="b4949-192">Get hello configuration for hello component that you are interested in.</span></span> <span data-ttu-id="b4949-193">Örneğin, aşağıdaki Hello yerine `INITIAL` hello önceki isteğinden döndürülen hello etiket değeri.</span><span class="sxs-lookup"><span data-stu-id="b4949-193">In hello following example, replace `INITIAL` with hello tag value returned from hello previous request.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    <span data-ttu-id="b4949-194">Bu örnek hello hello geçerli yapılandırmasını içeren bir JSON belgesi döndürür `core-site` bileşeni.</span><span class="sxs-lookup"><span data-stu-id="b4949-194">This example returns a JSON document containing hello current configuration for hello `core-site` component.</span></span>

## <a name="example-update-configuration"></a><span data-ttu-id="b4949-195">Örnek: Güncelleştirme yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b4949-195">Example: Update configuration</span></span>

1. <span data-ttu-id="b4949-196">Ambari hello "istenen yapılandırma" depolar hello geçerli yapılandırmasını alın:</span><span class="sxs-lookup"><span data-stu-id="b4949-196">Get hello current configuration, which Ambari stores as hello "desired configuration":</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="b4949-197">Bu örnek hello geçerli yapılandırmasını içeren bir JSON belgesi döndürür (Merhaba tarafından tanımlanan *etiketi* değeri) hello kümeye yüklü hello bileşenleri için.</span><span class="sxs-lookup"><span data-stu-id="b4949-197">This example returns a JSON document containing hello current configuration (identified by hello *tag* value) for hello components installed on hello cluster.</span></span> <span data-ttu-id="b4949-198">Merhaba aşağıdaki bir Spark kümesi türünden döndürülen hello verilerden bir alıntı örnektir.</span><span class="sxs-lookup"><span data-stu-id="b4949-198">hello following example is an excerpt from hello data returned from a Spark cluster type.</span></span>
   
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
   
    <span data-ttu-id="b4949-199">Bu listeden hello bileşenin toocopy hello adı gerekir (örneğin, **spark\_thrift\_sparkconf** ve hello **etiketi** değeri.</span><span class="sxs-lookup"><span data-stu-id="b4949-199">From this list, you need toocopy hello name of hello component (for example, **spark\_thrift\_sparkconf** and hello **tag** value.</span></span>

2. <span data-ttu-id="b4949-200">Merhaba bileşeni ve etiket için Hello yapılandırma komutları aşağıdaki hello kullanarak Al:</span><span class="sxs-lookup"><span data-stu-id="b4949-200">Retrieve hello configuration for hello component and tag by using hello following commands:</span></span>
   
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
    > <span data-ttu-id="b4949-201">Değiştir **spark thrift sparkconf** ve **ilk** hello bileşeni ve tooretrieve hello yapılandırması için istediğiniz etiketi.</span><span class="sxs-lookup"><span data-stu-id="b4949-201">Replace **spark-thrift-sparkconf** and **INITIAL** with hello component and tag that you want tooretrieve hello configuration for.</span></span>
   
    <span data-ttu-id="b4949-202">Jq Hdınsight'ta yeni bir yapılandırma şablonuna alınan kullanılan tooturn hello verilerdir.</span><span class="sxs-lookup"><span data-stu-id="b4949-202">Jq is used tooturn hello data retrieved from HDInsight into a new configuration template.</span></span> <span data-ttu-id="b4949-203">Özellikle, bu örnekler hello aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b4949-203">Specifically, these examples perform hello following actions:</span></span>
   
    * <span data-ttu-id="b4949-204">Merhaba dizesi "Sürüm" ve depolanan hello tarihi içeren benzersiz bir değer oluşturur `newtag`.</span><span class="sxs-lookup"><span data-stu-id="b4949-204">Creates a unique value containing hello string "version" and hello date, which is stored in `newtag`.</span></span>

    * <span data-ttu-id="b4949-205">Merhaba yeni istenen yapılandırma için bir kök belge oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b4949-205">Creates a root document for hello new desired configuration.</span></span>

    * <span data-ttu-id="b4949-206">Alır hello Merhaba içeriğine `.items[]` dizi ve altında hello ekler **desired_config** öğesi.</span><span class="sxs-lookup"><span data-stu-id="b4949-206">Gets hello contents of hello `.items[]` array and adds it under hello **desired_config** element.</span></span>

    * <span data-ttu-id="b4949-207">Siler hello `href`, `version`, ve `Config` öğeleri, bu öğeleri gerekli toosubmit yeni bir yapılandırma değildir.</span><span class="sxs-lookup"><span data-stu-id="b4949-207">Deletes hello `href`, `version`, and `Config` elements, as these elements aren't needed toosubmit a new configuration.</span></span>

    * <span data-ttu-id="b4949-208">Ekler bir `tag` değerini bir öğesiyle `version#################`.</span><span class="sxs-lookup"><span data-stu-id="b4949-208">Adds a `tag` element with a value of `version#################`.</span></span> <span data-ttu-id="b4949-209">Merhaba sayısal bölümü üzerinde hello geçerli tarih temel alır.</span><span class="sxs-lookup"><span data-stu-id="b4949-209">hello numeric portion is based on hello current date.</span></span> <span data-ttu-id="b4949-210">Her yapılandırma benzersiz bir etiketi olması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="b4949-210">Each configuration must have a unique tag.</span></span>
     
    <span data-ttu-id="b4949-211">Merhaba veri toohello son olarak, kaydedilen `newconfig.json` belge.</span><span class="sxs-lookup"><span data-stu-id="b4949-211">Finally, hello data is saved toohello `newconfig.json` document.</span></span> <span data-ttu-id="b4949-212">Merhaba belge yapısı aşağıdaki örneğine benzer toohello görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="b4949-212">hello document structure should appear similar toohello following example:</span></span>
     
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

3. <span data-ttu-id="b4949-213">Açık hello `newconfig.json` hello belge ve değiştirebilir ve ekleyebilir değerlerde `properties` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="b4949-213">Open hello `newconfig.json` document and modify/add values in hello `properties` object.</span></span> <span data-ttu-id="b4949-214">Merhaba aşağıdaki örnek değişiklikleri hello değerini `"spark.yarn.am.memory"` gelen `"1g"` çok`"3g"`.</span><span class="sxs-lookup"><span data-stu-id="b4949-214">hello following example changes hello value of `"spark.yarn.am.memory"` from `"1g"` too`"3g"`.</span></span> <span data-ttu-id="b4949-215">Ayrıca ekler `"spark.kryoserializer.buffer.max"` değerini `"256m"`.</span><span class="sxs-lookup"><span data-stu-id="b4949-215">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span></span>
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    <span data-ttu-id="b4949-216">Yapmayı değişiklikleri tamamladıktan sonra hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b4949-216">Save hello file once you are done making modifications.</span></span>

4. <span data-ttu-id="b4949-217">Aşağıdaki komutları toosubmit güncelleştirilmiş hello yapılandırma tooAmbari hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b4949-217">Use hello following commands toosubmit hello updated configuration tooAmbari.</span></span>
   
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
   
    <span data-ttu-id="b4949-218">Bu komutlar hello Merhaba içeriğine gönderme **newconfig.json** dosya toohello küme hello yeni istenen yapılandırması gibi.</span><span class="sxs-lookup"><span data-stu-id="b4949-218">These commands submit hello contents of hello **newconfig.json** file toohello cluster as hello new desired configuration.</span></span> <span data-ttu-id="b4949-219">Merhaba isteği bir JSON belgesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="b4949-219">hello request returns a JSON document.</span></span> <span data-ttu-id="b4949-220">Merhaba **versionTag** bu belgedeki öğe gönderildi ve hello hello sürüm eşleşmelidir **yapılandırmalar** nesne, istenen hello yapılandırma değişiklikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b4949-220">hello **versionTag** element in this document should match hello version you submitted, and hello **configs** object contains hello configuration changes you requested.</span></span>

### <a name="example-restart-a-service-component"></a><span data-ttu-id="b4949-221">Örnek: bir hizmet bileşeni yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="b4949-221">Example: Restart a service component</span></span>

<span data-ttu-id="b4949-222">Bu noktada, hello Ambari web kullanıcı Arabirimi bakarsanız, hello Spark hizmeti hello Yeni yapılandırmanın etkili olması için önce yeniden toobe gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="b4949-222">At this point, if you look at hello Ambari web UI, hello Spark service indicates that it needs toobe restarted before hello new configuration can take effect.</span></span> <span data-ttu-id="b4949-223">Aşağıdaki adımları toorestart hello hizmet hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b4949-223">Use hello following steps toorestart hello service.</span></span>

1. <span data-ttu-id="b4949-224">Merhaba Spark hizmeti tooenable Bakım modu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="b4949-224">Use hello following tooenable maintenance mode for hello Spark service:</span></span>

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
   
    <span data-ttu-id="b4949-225">Bu komutlar, bakım modunu açar bir JSON belgesi toohello sunucu gönderin.</span><span class="sxs-lookup"><span data-stu-id="b4949-225">These commands send a JSON document toohello server that turns on maintenance mode.</span></span> <span data-ttu-id="b4949-226">Merhaba hizmeti artık isteği aşağıdaki hello kullanarak bakım modunda olduğunu doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b4949-226">You can verify that hello service is now in maintenance mode using hello following request:</span></span>
   
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
   
    <span data-ttu-id="b4949-227">Merhaba dönüş değeri olan `ON`.</span><span class="sxs-lookup"><span data-stu-id="b4949-227">hello return value is `ON`.</span></span>

2. <span data-ttu-id="b4949-228">Ardından, tooturn hello hizmet dışı aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="b4949-228">Next, use hello following tooturn off hello service:</span></span>

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
    
    <span data-ttu-id="b4949-229">Merhaba yanıt benzer toohello örneği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="b4949-229">hello response is similar toohello following example:</span></span>
   
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
    > <span data-ttu-id="b4949-230">Merhaba `href` bu URI tarafından döndürülen değer hello küme düğümü hello iç IP adresini kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="b4949-230">hello `href` value returned by this URI is using hello internal IP address of hello cluster node.</span></span> <span data-ttu-id="b4949-231">toouse dış hello kümeden değiştirmek hello '10.0.0.18:8080' bölümü hello hello küme FQDN'si ile.</span><span class="sxs-lookup"><span data-stu-id="b4949-231">toouse it from outside hello cluster, replace hello \`10.0.0.18:8080' portion with hello FQDN of hello cluster.</span></span> 
    
    <span data-ttu-id="b4949-232">komutları aşağıdaki hello hello isteği hello durumunu alabilir:</span><span class="sxs-lookup"><span data-stu-id="b4949-232">hello following commands retrieve hello status of hello request:</span></span>

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

    <span data-ttu-id="b4949-233">Yanıtın `COMPLETED` bu hello isteğini tamamladı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b4949-233">A response of `COMPLETED` indicates that hello request has finished.</span></span>

3. <span data-ttu-id="b4949-234">Merhaba önceki istek tamamlandığında toostart hello hizmeti aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b4949-234">Once hello previous request completes, use hello following toostart hello service.</span></span>
   
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
    <span data-ttu-id="b4949-235">Merhaba hizmeti şimdi hello yeni yapılandırma kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="b4949-235">hello service is now using hello new configuration.</span></span>

4. <span data-ttu-id="b4949-236">Son olarak, Bakım Modu kapalı tooturn aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b4949-236">Finally, use hello following tooturn off maintenance mode.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="b4949-237">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b4949-237">Next steps</span></span>

<span data-ttu-id="b4949-238">Merhaba REST API tam başvuru için bkz: [Ambari API Başvurusu V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="b4949-238">For a complete reference of hello REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

