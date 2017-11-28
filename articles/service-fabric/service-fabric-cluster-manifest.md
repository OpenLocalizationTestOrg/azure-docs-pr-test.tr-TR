---
title: "aaaConfigure Azure Service Fabric tek başına kümenizi | Microsoft Docs"
description: "Bilgi nasıl tooconfigure tek başına veya özel Service Fabric kümesi."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dekapur
ms.openlocfilehash: ce2ad387162a05668bbd3a271c754776fe471850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a><span data-ttu-id="99000-103">Tek başına Windows kümesi için yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="99000-103">Configuration settings for standalone Windows cluster</span></span>
<span data-ttu-id="99000-104">Bir tek başına Service Fabric kümesi kullanarak tooconfigure nasıl hello bu makalede ***ClusterConfig.JSON*** dosya.</span><span class="sxs-lookup"><span data-stu-id="99000-104">This article describes how tooconfigure a standalone Service Fabric cluster using hello ***ClusterConfig.JSON*** file.</span></span> <span data-ttu-id="99000-105">Bu dosya toospecify bilgileri hello Service Fabric düğümleri ve IP adresleri, farklı türlerde düğümleri gibi hello ağ topolojisi arıza/yükseltme etki alanları, bakımından yanı sıra hello küme, hello güvenlik yapılandırmaları için tek başına kullanabilirsiniz Küme.</span><span class="sxs-lookup"><span data-stu-id="99000-105">You can use this file toospecify information such as hello Service Fabric nodes and their IP addresses, different types of nodes on hello cluster, hello security configurations as well as hello network topology in terms of fault/upgrade domains, for your standalone cluster.</span></span>

<span data-ttu-id="99000-106">Olduğunda, [hello tek başına Service Fabric paketi Yükle](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), birkaç hello ClusterConfig.JSON dosyasının indirilen tooyour iş makine örneklerdir.</span><span class="sxs-lookup"><span data-stu-id="99000-106">When you [download hello standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), a few samples of hello ClusterConfig.JSON file are downloaded tooyour work machine.</span></span> <span data-ttu-id="99000-107">Merhaba örnekleri sahip *DevCluster* adlarını, aynı makine, mantıksal düğümleri gibi hello üç tüm düğümlerde ile bir küme oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="99000-107">hello samples having *DevCluster* in their names will help you create a cluster with all three nodes on hello same machine, like logical nodes.</span></span> <span data-ttu-id="99000-108">Bunlar dışında en azından bir düğümün bir birincil düğüm olarak işaretlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="99000-108">Out of these, at least one node must be marked as a primary node.</span></span> <span data-ttu-id="99000-109">Bu küme bir geliştirme veya test ortamı için yararlıdır ve bir üretim kümesi olarak desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="99000-109">This cluster is useful for a development or test environment and is not supported as a production cluster.</span></span> <span data-ttu-id="99000-110">Merhaba örnekleri sahip *MultiMachine* adlarında, her bir düğümde ayrı bir makine ile bir üretim kalite kümesi oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="99000-110">hello samples having *MultiMachine* in their names, will help you create a production quality cluster, with each node on a separate machine.</span></span>

1. <span data-ttu-id="99000-111">*ClusterConfig.Unsecure.DevCluster.JSON* ve *ClusterConfig.Unsecure.MultiMachine.JSON* nasıl toocreate güvenli olmayan bir test veya üretim küme sırasıyla Göster.</span><span class="sxs-lookup"><span data-stu-id="99000-111">*ClusterConfig.Unsecure.DevCluster.JSON* and *ClusterConfig.Unsecure.MultiMachine.JSON* show how toocreate an unsecured test or production cluster respectively.</span></span> 
2. <span data-ttu-id="99000-112">*ClusterConfig.Windows.DevCluster.JSON* ve *ClusterConfig.Windows.MultiMachine.JSON* toocreate test veya üretim küme güvenliği nasıl kullanarak Göster [Windows Güvenliği](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="99000-112">*ClusterConfig.Windows.DevCluster.JSON* and  *ClusterConfig.Windows.MultiMachine.JSON* show how toocreate test or production cluster, secured using [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span>
3. <span data-ttu-id="99000-113">*ClusterConfig.X509.DevCluster.JSON* ve *ClusterConfig.X509.MultiMachine.JSON* toocreate test veya üretim küme güvenliği nasıl kullanarak Göster [X509 sertifika tabanlı güvenlik](service-fabric-windows-cluster-x509-security.md).</span><span class="sxs-lookup"><span data-stu-id="99000-113">*ClusterConfig.X509.DevCluster.JSON* and *ClusterConfig.X509.MultiMachine.JSON* show how toocreate test or production cluster, secured using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span></span> 

<span data-ttu-id="99000-114">İnceleyeceğiz artık çeşitli bölümlerini hello bir ***ClusterConfig.JSON*** olarak aşağıdaki dosya.</span><span class="sxs-lookup"><span data-stu-id="99000-114">Now we will examine hello various sections of a ***ClusterConfig.JSON*** file as below.</span></span>

## <a name="general-cluster-configurations"></a><span data-ttu-id="99000-115">Genel küme yapılandırmaları</span><span class="sxs-lookup"><span data-stu-id="99000-115">General cluster configurations</span></span>
<span data-ttu-id="99000-116">Bu hello geniş küme belirli yapılandırmalar, aşağıdaki hello JSON parçacığında gösterildiği gibi kapsar.</span><span class="sxs-lookup"><span data-stu-id="99000-116">This covers hello broad cluster specific configurations, as shown in hello JSON snippet below.</span></span>

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

<span data-ttu-id="99000-117">Herhangi bir kolay ad tooyour Service Fabric küme toohello atayarak verebilirsiniz **adı** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="99000-117">You can give any friendly name tooyour Service Fabric cluster by assigning it toohello **name** variable.</span></span> <span data-ttu-id="99000-118">Merhaba **clusterConfigurationVersion** kümenizin; hello sürüm numarası, Service Fabric kümesi yükseltme her zaman artırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="99000-118">hello **clusterConfigurationVersion** is hello version number of your cluster; you should increase it every time you upgrade your Service Fabric cluster.</span></span> <span data-ttu-id="99000-119">Merhaba ancak bırakmalısınız **apiVersion** toohello varsayılan değeri.</span><span class="sxs-lookup"><span data-stu-id="99000-119">You should however leave hello **apiVersion** toohello default value.</span></span>

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a><span data-ttu-id="99000-120">Merhaba küme düğümlerinde</span><span class="sxs-lookup"><span data-stu-id="99000-120">Nodes on hello cluster</span></span>
<span data-ttu-id="99000-121">Hello kullanarak Service Fabric kümenizde hello düğümleri yapılandırabilirsiniz **düğümleri** bölümünde, aşağıdaki kod parçacığında gösterildiği hello olarak.</span><span class="sxs-lookup"><span data-stu-id="99000-121">You can configure hello nodes on your Service Fabric cluster by using hello **nodes** section, as hello following snippet shows.</span></span>

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

<span data-ttu-id="99000-122">Service Fabric kümesi en az 3 düğümleri içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="99000-122">A Service Fabric cluster must contain at least 3 nodes.</span></span> <span data-ttu-id="99000-123">Kurulumunuzu göre daha fazla düğüm toothis bölümüne ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99000-123">You can add more nodes toothis section as per your setup.</span></span> <span data-ttu-id="99000-124">Aşağıdaki tablonun hello her düğüm için hello yapılandırma ayarları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="99000-124">hello following table explains hello configuration settings for each node.</span></span>

| <span data-ttu-id="99000-125">**Düğüm yapılandırması**</span><span class="sxs-lookup"><span data-stu-id="99000-125">**Node configuration**</span></span> | <span data-ttu-id="99000-126">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="99000-126">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="99000-127">nodeName</span><span class="sxs-lookup"><span data-stu-id="99000-127">nodeName</span></span> |<span data-ttu-id="99000-128">Herhangi bir kolay ad toohello düğümü verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99000-128">You can give any friendly name toohello node.</span></span> |
| <span data-ttu-id="99000-129">IP adresi</span><span class="sxs-lookup"><span data-stu-id="99000-129">iPAddress</span></span> |<span data-ttu-id="99000-130">Bir komut penceresi açıp yazarak, düğümün IP adresini Hello bulmak `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="99000-130">Find out hello IP address of your node by opening a command window and typing `ipconfig`.</span></span> <span data-ttu-id="99000-131">Not hello IPv4 adresi ve toohello Ata **IPADDRESS** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="99000-131">Note hello IPV4 address and assign it toohello **iPAddress** variable.</span></span> |
| <span data-ttu-id="99000-132">nodeTypeRef</span><span class="sxs-lookup"><span data-stu-id="99000-132">nodeTypeRef</span></span> |<span data-ttu-id="99000-133">Her düğüm farklı düğüm türü atanabilir.</span><span class="sxs-lookup"><span data-stu-id="99000-133">Each node can be assigned a different node type.</span></span> <span data-ttu-id="99000-134">Merhaba [düğüm türleri](#nodetypes) hello aşağıdaki bölümde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="99000-134">hello [node types](#nodetypes) are defined in hello section below.</span></span> |
| <span data-ttu-id="99000-135">faultDomain</span><span class="sxs-lookup"><span data-stu-id="99000-135">faultDomain</span></span> |<span data-ttu-id="99000-136">Hello başarısız olabilir hata etki alanları etkinleştir küme yöneticileri toodefine hello fiziksel düğümde aynı tooshared fiziksel bağımlılıkları zaman.</span><span class="sxs-lookup"><span data-stu-id="99000-136">Fault domains enable cluster administrators toodefine hello physical nodes that might fail at hello same time due tooshared physical dependencies.</span></span> |
| <span data-ttu-id="99000-137">upgradeDomain</span><span class="sxs-lookup"><span data-stu-id="99000-137">upgradeDomain</span></span> |<span data-ttu-id="99000-138">Yükseltme etki alanları tanımlamak Service Fabric adresindeki hello hakkında aynı yükseltmeleri için kapatıldığından düğüm kümesi saat.</span><span class="sxs-lookup"><span data-stu-id="99000-138">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about hello same time.</span></span> <span data-ttu-id="99000-139">Fiziksel gereksinimlere göre sınırlı değildir gibi yükseltme etki alanları, hangi düğümleri tooassign toowhich seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99000-139">You can choose which nodes tooassign toowhich Upgrade domains, as they are not limited by any physical requirements.</span></span> |

## <a name="cluster-properties"></a><span data-ttu-id="99000-140">Küme Özellikleri</span><span class="sxs-lookup"><span data-stu-id="99000-140">Cluster properties</span></span>
<span data-ttu-id="99000-141">Merhaba **özellikleri** hello ClusterConfig.JSON bölümünde şu kullanılan tooconfigure hello küme şekildedir.</span><span class="sxs-lookup"><span data-stu-id="99000-141">hello **properties** section in hello ClusterConfig.JSON is used tooconfigure hello cluster as follows.</span></span>

<a id="reliability"></a>

### <a name="reliability"></a><span data-ttu-id="99000-142">Güvenilirlik</span><span class="sxs-lookup"><span data-stu-id="99000-142">Reliability</span></span>
<span data-ttu-id="99000-143">Merhaba kavramı **reliabilityLevel** hello çoğaltmaların sayısı veya hello birincil hello küme düğümlerinde çalıştırabilirsiniz hello Service Fabric Sistem Hizmetleri örnekleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="99000-143">hello concept of **reliabilityLevel** defines hello number of replicas or instances of hello Service Fabric system services that can run on hello primary nodes of hello cluster.</span></span> <span data-ttu-id="99000-144">Bu hizmetler hello güvenilirliğini belirler ve bu nedenle küme hello.</span><span class="sxs-lookup"><span data-stu-id="99000-144">It determines hello reliability of these services and hence hello cluster.</span></span> <span data-ttu-id="99000-145">Merhaba hello sistem tarafından hesaplanan küme oluşturma ve yükseltme zamanında değerdir.</span><span class="sxs-lookup"><span data-stu-id="99000-145">hello value is calcuated by hello system at cluster creation and upgrade time.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="99000-146">Tanılama</span><span class="sxs-lookup"><span data-stu-id="99000-146">Diagnostics</span></span>
<span data-ttu-id="99000-147">Merhaba **diagnosticsStore** bölümü sağlar, tooconfigure parametreleri tooenable tanılama ve sorun giderme düğümü veya küme hataları hello aşağıdaki kod parçacığında gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="99000-147">hello **diagnosticsStore** section allows you tooconfigure parameters tooenable diagnostics and troubleshooting node or cluster failures, as shown in hello following snippet.</span></span> 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

<span data-ttu-id="99000-148">Merhaba **meta veri** küme tanılama açıklaması ve kurulumunuzu uygun şekilde ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99000-148">hello **metadata** is a description of your cluster diagnostics and can be set as per your setup.</span></span> <span data-ttu-id="99000-149">Bu değişkenler ETW İzleme günlükleri, kilitlenme bilgi dökümleri yanı sıra performans sayaçlarını toplama de yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="99000-149">These variables help in collecting ETW trace logs, crash dumps as well as performance counters.</span></span> <span data-ttu-id="99000-150">Okuma [işaretlenemedi](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) ve [ETW İzleme](https://msdn.microsoft.com/library/ms751538.aspx) ETW hakkında daha fazla bilgi için izleme günlüklerine.</span><span class="sxs-lookup"><span data-stu-id="99000-150">Read [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) for more information on ETW trace logs.</span></span> <span data-ttu-id="99000-151">Tüm günlükleri de dahil olmak üzere [kilitlenme dökümleri](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) ve [performans sayaçları](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) yönlendirilmiş toohello olabilir **connectionString** makinenizde klasör.</span><span class="sxs-lookup"><span data-stu-id="99000-151">All logs including [Crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) can be directed toohello **connectionString** folder on your machine.</span></span> <span data-ttu-id="99000-152">Aynı zamanda *AzureStorage* tanılama depolamak için.</span><span class="sxs-lookup"><span data-stu-id="99000-152">You can also use *AzureStorage* for storing diagnostics.</span></span> <span data-ttu-id="99000-153">Aşağıdaki örnek kod parçacığında için bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="99000-153">See below for a sample snippet.</span></span>

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a><span data-ttu-id="99000-154">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="99000-154">Security</span></span>
<span data-ttu-id="99000-155">Merhaba **güvenlik** bölüm güvenli tek başına Service Fabric kümesi için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="99000-155">hello **security** section is necessary for a secure standalone Service Fabric cluster.</span></span> <span data-ttu-id="99000-156">Aşağıdaki kod parçacığında hello bu bölümün parçası gösterir.</span><span class="sxs-lookup"><span data-stu-id="99000-156">hello following snippet shows a part of this section.</span></span>

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

<span data-ttu-id="99000-157">Merhaba **meta veri** güvenli kümenizi açıklaması ve kurulumunuzu uygun şekilde ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99000-157">hello **metadata** is a description of your secure cluster and can be set as per your setup.</span></span> <span data-ttu-id="99000-158">Merhaba **ClusterCredentialType** ve **ServerCredentialType** hello küme ve hello düğümler uygulayan güvenlik hello türü belirlenemedi.</span><span class="sxs-lookup"><span data-stu-id="99000-158">hello **ClusterCredentialType** and **ServerCredentialType** determine hello type of security that hello cluster and hello nodes will implement.</span></span> <span data-ttu-id="99000-159">Tooeither ayarlanabilir *X509* bir sertifika tabanlı güvenlik için veya *Windows* bir Azure Active Directory tabanlı güvenlik için.</span><span class="sxs-lookup"><span data-stu-id="99000-159">They can be set tooeither *X509* for a certificate-based security, or *Windows* for an Azure Active Directory-based security.</span></span> <span data-ttu-id="99000-160">Merhaba hello geri kalanı **güvenlik** bölüm hello güvenlik hello türünü tabanlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="99000-160">hello rest of hello **security** section will be based on hello type of hello security.</span></span> <span data-ttu-id="99000-161">Okuma [sertifikalar tabanlı güvenlik tek başına kümedeki](service-fabric-windows-cluster-x509-security.md) veya [tek başına kümede Windows Güvenliği](service-fabric-windows-cluster-windows-security.md) nasıl toofill hello çıkışı rest hello hakkında bilgi için **güvenlik**bölümü.</span><span class="sxs-lookup"><span data-stu-id="99000-161">Read [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md) for information on how toofill out hello rest of hello **security** section.</span></span>

<a id="nodetypes"></a>

### <a name="node-types"></a><span data-ttu-id="99000-162">Düğüm türleri</span><span class="sxs-lookup"><span data-stu-id="99000-162">Node Types</span></span>
<span data-ttu-id="99000-163">Merhaba **nodeTypes** bölüm kümenizi sahip hello düğümleri hello türünü açıklar.</span><span class="sxs-lookup"><span data-stu-id="99000-163">hello **nodeTypes** section describes hello type of hello nodes that your cluster has.</span></span> <span data-ttu-id="99000-164">En az bir düğüm türü, aşağıdaki hello parçacığında gösterildiği gibi bir küme için belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="99000-164">At least one node type must be specified for a cluster, as shown in hello snippet below.</span></span> 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

<span data-ttu-id="99000-165">Merhaba **adı** bu belirli düğüm türü için hello kolay addır.</span><span class="sxs-lookup"><span data-stu-id="99000-165">hello **name** is hello friendly name for this particular node type.</span></span> <span data-ttu-id="99000-166">Bu düğüm türünde bir düğüm toocreate atamak kolay ad toohello **nodeTypeRef** bu düğüm için değişken belirtildiği gibi [yukarıda](#clusternodes).</span><span class="sxs-lookup"><span data-stu-id="99000-166">toocreate a node of this node type, assign its friendly name toohello **nodeTypeRef** variable for that node, as mentioned [above](#clusternodes).</span></span> <span data-ttu-id="99000-167">Her düğüm türü için kullanılacak hello bağlantı uç tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="99000-167">For each node type, define hello connection endpoints that will be used.</span></span> <span data-ttu-id="99000-168">Bu kümedeki başka bir uç nokta ile çakışmadığından sürece, bu bağlantı uç noktaları için herhangi bir bağlantı noktası numarası seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99000-168">You can choose any port number for these connection endpoints, as long as they do not conflict with any other endpoints in this cluster.</span></span> <span data-ttu-id="99000-169">Çok düğümlü bir küme içinde olacaktır bir veya daha fazla birincil düğüm (yani **isPrimary** çok ayarlamak*true*) hello bağlı olarak [ **reliabilityLevel** ](#reliability).</span><span class="sxs-lookup"><span data-stu-id="99000-169">In a multi-node cluster, there will be one or more primary nodes (i.e. **isPrimary** set too*true*), depending on hello [**reliabilityLevel**](#reliability).</span></span> <span data-ttu-id="99000-170">Okuma [Service Fabric kümesi kapasite planlama konuları](service-fabric-cluster-capacity.md) hakkında bilgi için **nodeTypes** ve **reliabilityLevel**ve hangi birincil ve hello tooknow birincil olmayan düğüm türleri.</span><span class="sxs-lookup"><span data-stu-id="99000-170">Read [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on **nodeTypes** and **reliabilityLevel**, and tooknow what are primary and hello non-primary node types.</span></span> 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a><span data-ttu-id="99000-171">Uç noktaları tooconfigure hello düğüm türleri kullanılır</span><span class="sxs-lookup"><span data-stu-id="99000-171">Endpoints used tooconfigure hello node types</span></span>
* <span data-ttu-id="99000-172">*clientConnectionEndpointPort* hello istemci API'leri kullanırken hello istemci tooconnect toohello küme tarafından kullanılan hello bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="99000-172">*clientConnectionEndpointPort* is hello port used by hello client tooconnect toohello cluster, when using hello client APIs.</span></span> 
* <span data-ttu-id="99000-173">*clusterConnectionEndpointPort* hangi hello düğümleri birbiriyle hello bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="99000-173">*clusterConnectionEndpointPort* is hello port at which hello nodes communicate with each other.</span></span>
* <span data-ttu-id="99000-174">*leaseDriverEndpointPort* hello düğümleri hala etkin olup olmadığını hello küme kira sürücü toofind tarafından kullanılan hello bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="99000-174">*leaseDriverEndpointPort* is hello port used by hello cluster lease driver toofind out if hello nodes are still active.</span></span> 
* <span data-ttu-id="99000-175">*serviceConnectionEndpointPort* hello uygulamaları tarafından kullanılan başlangıç bağlantı noktası ve bu belirli düğüm üzerindeki hello Service Fabric istemcisi ile toocommunicate bir düğümde dağıtılan Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="99000-175">*serviceConnectionEndpointPort* is hello port used by hello applications and services deployed on a node, toocommunicate with hello Service Fabric client on that particular node.</span></span>
* <span data-ttu-id="99000-176">*httpGatewayEndpointPort* hello Service Fabric Explorer tooconnect toohello küme tarafından kullanılan hello bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="99000-176">*httpGatewayEndpointPort* is hello port used by hello Service Fabric Explorer tooconnect toohello cluster.</span></span>
* <span data-ttu-id="99000-177">*ephemeralPorts* hello geçersiz kılma [hello işletim sistemi tarafından kullanılan dinamik bağlantı noktaları](https://support.microsoft.com/kb/929851).</span><span class="sxs-lookup"><span data-stu-id="99000-177">*ephemeralPorts* override hello [dynamic ports used by hello OS](https://support.microsoft.com/kb/929851).</span></span> <span data-ttu-id="99000-178">Service Fabric uygulaması bağlantı noktaları olarak parçası kullanır ve hello kalan hello işletim sistemi için kullanılabilir olacak.</span><span class="sxs-lookup"><span data-stu-id="99000-178">Service Fabric will use a part of these as application ports and hello remaining will be available for hello OS.</span></span> <span data-ttu-id="99000-179">Tüm amaçlar için hello örnek JSON dosyalarında verilen hello aralıkları kullanabilmek için de bu aralık toohello var olan bir aralığı hello işletim sistemi, mevcut eşlenir.</span><span class="sxs-lookup"><span data-stu-id="99000-179">It will also map this range toohello existing range present in hello OS, so for all purposes, you can use hello ranges given in hello sample JSON files.</span></span> <span data-ttu-id="99000-180">Merhaba fark hello başlangıç ve hello uç bağlantı noktaları arasında en az 255 emin toomake gerekir.</span><span class="sxs-lookup"><span data-stu-id="99000-180">You need toomake sure that hello difference between hello start and hello end ports is at least 255.</span></span> <span data-ttu-id="99000-181">Bu aralık hello işletim sistemiyle paylaşılan beri bu fark, düşükse çakışmaları çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="99000-181">You may run into conflicts if this difference is too low, since this range is shared with hello operating system.</span></span> <span data-ttu-id="99000-182">Çalıştırarak yapılandırılmış hello dinamik bağlantı noktası aralığını görmek `netsh int ipv4 show dynamicport tcp`.</span><span class="sxs-lookup"><span data-stu-id="99000-182">See hello configured dynamic port range by running `netsh int ipv4 show dynamicport tcp`.</span></span>
* <span data-ttu-id="99000-183">*applicationPorts* hello Service Fabric uygulamaları tarafından kullanılan hello bağlantı noktalarıdır.</span><span class="sxs-lookup"><span data-stu-id="99000-183">*applicationPorts* are hello ports that will be used by hello Service Fabric applications.</span></span> <span data-ttu-id="99000-184">Merhaba uygulama bağlantı noktası aralığı büyüklükte toocover hello uç nokta gereksinim uygulamalarınızın olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="99000-184">hello application port range should be large enough toocover hello endpoint requirement of your applications.</span></span> <span data-ttu-id="99000-185">Bu aralık hello makinede, yani hello hello dinamik bağlantı noktası aralığından özel *ephemeralPorts* hello yapılandırmasında belirlenen aralık.</span><span class="sxs-lookup"><span data-stu-id="99000-185">This range should be exclusive from hello dynamic port range on hello machine, i.e. hello *ephemeralPorts* range as set in hello configuration.</span></span>  <span data-ttu-id="99000-186">Yeni bağlantı noktaları gereklidir, aynı zamanda her hello Güvenlik Duvarı'nı bu bağlantı noktaları açma ilgilenebilmek Service Fabric bunları kullanın.</span><span class="sxs-lookup"><span data-stu-id="99000-186">Service Fabric will use these whenever new ports are required, as well as take care of opening hello firewall for these ports.</span></span> 
* <span data-ttu-id="99000-187">*reverseProxyEndpointPort* bir isteğe bağlı ters proxy uç noktadır.</span><span class="sxs-lookup"><span data-stu-id="99000-187">*reverseProxyEndpointPort* is an optional reverse proxy endpoint.</span></span> <span data-ttu-id="99000-188">Bkz: [Service Fabric Ters Proxy](service-fabric-reverseproxy.md) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="99000-188">See [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) for more details.</span></span> 

### <a name="log-settings"></a><span data-ttu-id="99000-189">Günlük ayarları</span><span class="sxs-lookup"><span data-stu-id="99000-189">Log Settings</span></span>
<span data-ttu-id="99000-190">Merhaba **fabricSettings** bölümü tooset hello kök dizinler hello Service Fabric veri ve günlükleri için sağlar.</span><span class="sxs-lookup"><span data-stu-id="99000-190">hello **fabricSettings** section allows you tooset hello root directories for hello Service Fabric data and logs.</span></span> <span data-ttu-id="99000-191">Bunlar yalnızca hello ilk küme oluşturma sırasında özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99000-191">You can customize these only during hello initial cluster creation.</span></span> <span data-ttu-id="99000-192">Aşağıda bu bölüm için bir örnek parçacığı konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="99000-192">See below for a sample snippet of this section.</span></span>

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

<span data-ttu-id="99000-193">İşletim sistemi çökme (Crash karşı) daha fazla güvenilirlik sağladığından bir işletim sistemi olmayan sürücü hello FabricDataRoot olarak ve FabricLogRoot kullanarak önerilir.</span><span class="sxs-lookup"><span data-stu-id="99000-193">We recommended using a non-OS drive as hello FabricDataRoot and FabricLogRoot as it provides more reliability against OS crashes.</span></span> <span data-ttu-id="99000-194">Yalnızca hello veri kök özelleştirirseniz, ardından hello günlük kök hello veri kökü altındaki bir düzey yerleştirilecek olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="99000-194">Note that if you customize only hello data root, then hello log root will be placed one level below hello data root.</span></span>

### <a name="stateful-reliable-service-settings"></a><span data-ttu-id="99000-195">Durum bilgisi olan güvenilir hizmet ayarları</span><span class="sxs-lookup"><span data-stu-id="99000-195">Stateful Reliable Service Settings</span></span>
<span data-ttu-id="99000-196">Merhaba **KtlLogger** bölümü güvenilir hizmetler için tooset hello genel yapılandırma ayarlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="99000-196">hello **KtlLogger** section allows you tooset hello global configuration settings for Reliable Services.</span></span> <span data-ttu-id="99000-197">Bu ayarlar hakkında daha fazla ayrıntı için okuma [durum bilgisi olan güvenilir hizmetler yapılandırma](service-fabric-reliable-services-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="99000-197">For more details on these settings read [Configure stateful reliable services](service-fabric-reliable-services-configuration.md).</span></span>
<span data-ttu-id="99000-198">Aşağıdaki örnek Hello alır toochange hello hello paylaşılan işlem günlüğü tooback durum bilgisi olan hizmetler için herhangi bir güvenilir koleksiyonu nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="99000-198">hello example below shows how toochange hello hello shared transaction log that gets created tooback any reliable collections for stateful services.</span></span>

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a><span data-ttu-id="99000-199">Eklenti Özellikleri</span><span class="sxs-lookup"><span data-stu-id="99000-199">Add-on features</span></span>
<span data-ttu-id="99000-200">tooconfigure eklenti özellikleri hello apiVersion yapılandırılmış olarak ' 04-2017' veya daha yüksek olmalıdır ve yapılandırılmış toobe addonFeatures gerekiyor:</span><span class="sxs-lookup"><span data-stu-id="99000-200">tooconfigure add-on features, hello apiVersion should be configured as '04-2017' or higher, and addonFeatures needs toobe configured:</span></span>

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a><span data-ttu-id="99000-201">Kapsayıcı desteği</span><span class="sxs-lookup"><span data-stu-id="99000-201">Container support</span></span>
<span data-ttu-id="99000-202">windows server kapsayıcı ve tek başına kümeleri için hyper-v kapsayıcı için tooenable kapsayıcı desteği, hello 'DnsService' Eklenti özelliğinin etkin toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="99000-202">tooenable container support for both windows server container and hyper-v container for standalone clusters, hello 'DnsService' add-on feature needs toobe enabled.</span></span>


## <a name="next-steps"></a><span data-ttu-id="99000-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="99000-203">Next steps</span></span>
<span data-ttu-id="99000-204">Tek başına küme kurulumunuzu uygun şekilde yapılandırılmış ClusterConfig.JSON dosyanın tamamını olduktan sonra kümenizi aşağıdaki hello makale dağıtabilirsiniz [bir tek başına Service Fabric kümesi oluştur](service-fabric-cluster-creation-for-windows-server.md) ve çok devam[Service Fabric Explorer ile kümenizi görselleştirme](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="99000-204">Once you have a complete ClusterConfig.JSON file configured as per your standalone cluster setup, you can deploy your cluster by following hello article [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md) and then proceed too[visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

