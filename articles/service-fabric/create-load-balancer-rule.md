---
title: "aaaCreate bir küme için bir Azure yük dengeleyici kuralı"
description: "Azure Service Fabric kümesi için bir Azure yük dengeleyici tooopen bağlantı noktalarını yapılandırın."
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a><span data-ttu-id="4d44b-103">Service Fabric kümesi için bağlantı noktalarını açın</span><span class="sxs-lookup"><span data-stu-id="4d44b-103">Open ports for a Service Fabric cluster</span></span>

<span data-ttu-id="4d44b-104">Azure Service Fabric kümenizle dağıtılan hello yük dengeleyici bir düğümde çalışan trafiği tooyour uygulama yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="4d44b-104">hello load balancer deployed with your Azure Service Fabric cluster directs traffic tooyour app running on a node.</span></span> <span data-ttu-id="4d44b-105">Uygulama toouse farklı bir bağlantı noktasını değiştirirseniz, bu bağlantı noktasını kullanıma (veya farklı bir bağlantı noktası rota gerekir) hello Azure yük dengeleyici içinde.</span><span class="sxs-lookup"><span data-stu-id="4d44b-105">If you change your app toouse a different port, you must expose that port (or route a different port) in hello Azure Load Balancer.</span></span>

<span data-ttu-id="4d44b-106">Service fabric kümesi tooAzure dağıtıldığında, bir yük dengeleyici sizin için otomatik olarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="4d44b-106">When you deployed your service fabric cluster tooAzure, a load balancer was automatically created for you.</span></span> <span data-ttu-id="4d44b-107">Bir yük dengeleyici yoksa bkz [bir Internet'e yönelik Yük Dengeleyici yapılandırma](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4d44b-107">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

## <a name="configure-service-fabric"></a><span data-ttu-id="4d44b-108">Service fabric yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4d44b-108">Configure service fabric</span></span>

<span data-ttu-id="4d44b-109">Service Fabric uygulamanızı **ServiceManifest.xml** yapılandırma dosyasını, uygulamanızın bekliyor toouse hello uç noktaları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="4d44b-109">Your Service Fabric application **ServiceManifest.xml** config file defines hello endpoints your application expects toouse.</span></span> <span data-ttu-id="4d44b-110">Hello config dosya güncelleştirilmiş toodefine bir uç nokta oluşturulduktan sonra hello yük dengeleyici güncelleştirilmiş tooexpose o (veya farklı bir) olmalıdır bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="4d44b-110">After hello config file has been updated toodefine an endpoint, hello load balancer must be updated tooexpose that (or a different) port.</span></span> <span data-ttu-id="4d44b-111">Nasıl toocreate hello hizmet yapı uç noktası ile ilgili daha fazla bilgi için bkz: [bir uç nokta Kurulum](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4d44b-111">For more information on how toocreate hello service fabric endpoint, see [Setup an Endpoint](service-fabric-service-manifest-resources.md).</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="4d44b-112">Yük Dengeleyici kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d44b-112">Create a load balancer rule</span></span>

<span data-ttu-id="4d44b-113">Yük Dengeleyici kuralı, bir internet'e yönelik bağlantı açar ve uygulamanız tarafından kullanılan trafiği toohello iç düğümün bağlantı iletir.</span><span class="sxs-lookup"><span data-stu-id="4d44b-113">A load balancer rule opens up an internet-facing port and forwards traffic toohello internal node's port used by your application.</span></span> <span data-ttu-id="4d44b-114">Bir yük dengeleyici yoksa bkz [bir Internet'e yönelik Yük Dengeleyici yapılandırma](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4d44b-114">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

<span data-ttu-id="4d44b-115">toocreate bir yük dengeleyici kuralı için aşağıdaki bilgilerle toocollect hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="4d44b-115">toocreate a load balancer rule, you need toocollect hello following information:</span></span>

- <span data-ttu-id="4d44b-116">Yük dengeleyicisi adı.</span><span class="sxs-lookup"><span data-stu-id="4d44b-116">Load balancer name.</span></span>
- <span data-ttu-id="4d44b-117">Kaynak grubu Merhaba, yük dengeleyici ve service fabric kümesi.</span><span class="sxs-lookup"><span data-stu-id="4d44b-117">Resource group of hello load balancer and service fabric cluster.</span></span>
- <span data-ttu-id="4d44b-118">Dış bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="4d44b-118">External port.</span></span>
- <span data-ttu-id="4d44b-119">İç bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="4d44b-119">Internal port.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="4d44b-120">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4d44b-120">Azure CLI</span></span>
>[!NOTE]
><span data-ttu-id="4d44b-121">Merhaba yük dengeleyici toodetermine hello adı gerekiyorsa, bu komutu tooquickly get tüm yük dengeleyicileri ve ilişkili hello kaynak grupları listesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4d44b-121">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and hello associated resource groups.</span></span>
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

<span data-ttu-id="4d44b-122">Yük Dengeleyici kuralı hello ile yalnızca tek bir komut toocreate alır **Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="4d44b-122">It only takes a single command toocreate a load balancer rule with hello **Azure CLI**.</span></span> <span data-ttu-id="4d44b-123">Tooknow hello yük dengeleyici ve kaynak grubu toocreate yeni bir kural hem hello adını yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="4d44b-123">You just need tooknow both hello name of hello load balancer and resource group toocreate a new rule.</span></span>

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

<span data-ttu-id="4d44b-124">Hello Azure CLI komutu aşağıdaki tablonun hello açıklanan birkaç parametreleri içerir:</span><span class="sxs-lookup"><span data-stu-id="4d44b-124">hello Azure CLI command has a few parameters that are described in hello following table:</span></span>

| <span data-ttu-id="4d44b-125">Parametre</span><span class="sxs-lookup"><span data-stu-id="4d44b-125">Parameter</span></span> | <span data-ttu-id="4d44b-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4d44b-126">Description</span></span> |
| --------- | ----------- |
| `--backend-port`  | <span data-ttu-id="4d44b-127">Merhaba bağlantı noktası hello service fabric uygulaması için dinliyor.</span><span class="sxs-lookup"><span data-stu-id="4d44b-127">hello port hello service fabric application is listening to.</span></span> |
| `--frontend-port` | <span data-ttu-id="4d44b-128">başlangıç bağlantı noktası hello yük dengeleyici çıkarır dış bağlantıları için.</span><span class="sxs-lookup"><span data-stu-id="4d44b-128">hello port hello load balancer exposes for external connections.</span></span> |
| `-lb-name` | <span data-ttu-id="4d44b-129">Yük Dengeleyici toochange hello Hello adı.</span><span class="sxs-lookup"><span data-stu-id="4d44b-129">hello name of hello load balancer toochange.</span></span> |
| `-g`       | <span data-ttu-id="4d44b-130">Merhaba yük dengeleyici ve service fabric kümesi sahip hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="4d44b-130">hello resource group that has both hello load balancer and service fabric cluster.</span></span> |
| `-n`       | <span data-ttu-id="4d44b-131">Merhaba hello kuralın adını seçildi.</span><span class="sxs-lookup"><span data-stu-id="4d44b-131">hello chosen name of hello rule.</span></span> |


>[!NOTE]
><span data-ttu-id="4d44b-132">Bir yük dengeleyici hello Azure CLI ile nasıl toocreate bakın hakkında daha fazla bilgi için [hello Azure CLI ile bir yük dengeleyici oluşturma](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4d44b-132">For more information on how toocreate a load balancer with hello Azure CLI, see [Create a load balancer with hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="4d44b-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d44b-133">PowerShell</span></span>

>[!NOTE]
><span data-ttu-id="4d44b-134">Merhaba yük dengeleyici toodetermine hello adı gerekiyorsa, bu komutu tooquickly get tüm yük dengeleyicileri ve ilişkili kaynak grupları listesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4d44b-134">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and associated resource groups.</span></span>
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

<span data-ttu-id="4d44b-135">PowerShell Azure CLI hello biraz daha karmaşıktır.</span><span class="sxs-lookup"><span data-stu-id="4d44b-135">PowerShell is a little more complicated than hello Azure CLI.</span></span> <span data-ttu-id="4d44b-136">Kavramsal olarak, aşağıdaki adımları toocreate hello bir kural yapın.</span><span class="sxs-lookup"><span data-stu-id="4d44b-136">Conceptually, do hello following steps toocreate a rule.</span></span>

1. <span data-ttu-id="4d44b-137">Merhaba yük dengeleyici Azure'dan alın.</span><span class="sxs-lookup"><span data-stu-id="4d44b-137">Get hello load balancer from Azure.</span></span>
2. <span data-ttu-id="4d44b-138">Bir kural oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4d44b-138">Create a rule.</span></span>
3. <span data-ttu-id="4d44b-139">Merhaba kural toohello yük dengeleyiciye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4d44b-139">Add hello rule toohello load balancer.</span></span>
4. <span data-ttu-id="4d44b-140">Merhaba yük dengeleyicisi güncelleştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="4d44b-140">Update hello load balancer.</span></span>

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

<span data-ttu-id="4d44b-141">Merhaba ilgili `New-AzureRmLoadBalancerRuleConfig` , hello komut `-FrontendPort` temsil hello bağlantı noktası hello yük dengeleyici gösteren dış bağlantılar ve hello `-BackendPort` temsil hello bağlantı noktası hello service fabric uygulaması dinlerken.</span><span class="sxs-lookup"><span data-stu-id="4d44b-141">Regarding hello `New-AzureRmLoadBalancerRuleConfig` command, hello `-FrontendPort` represents hello port hello load balancer exposes for external connections, and hello `-BackendPort` represents hello port hello service fabric app is listening to.</span></span>

>[!NOTE]
><span data-ttu-id="4d44b-142">Bir yük dengeleyici PowerShell ile nasıl toocreate bakın hakkında daha fazla bilgi için [PowerShell ile bir yük dengeleyici oluşturma](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4d44b-142">For more information on how toocreate a load balancer with PowerShell, see [Create a load balancer with PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span></span>

