---
title: "Bir küme için bir Azure yük dengeleyici kuralı oluşturma"
description: "Azure Service Fabric kümesi için bağlantı noktalarını açmak için bir Azure yük dengeleyici yapılandırın."
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
ms.openlocfilehash: c99c4d9f343ca97fd3cd363fb54feaf5507bb77c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a><span data-ttu-id="9d7dc-103">Service Fabric kümesi için bağlantı noktalarını açın</span><span class="sxs-lookup"><span data-stu-id="9d7dc-103">Open ports for a Service Fabric cluster</span></span>

<span data-ttu-id="9d7dc-104">Yük Dengeleyici, Azure Service Fabric kümesi ile dağıtılmış bir düğüm üzerinde çalışan ve uygulamanızın trafiğini yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-104">The load balancer deployed with your Azure Service Fabric cluster directs traffic to your app running on a node.</span></span> <span data-ttu-id="9d7dc-105">Farklı bir bağlantı noktası kullanmak için uygulamanızı değiştirirseniz, bu bağlantı noktasını kullanıma (veya farklı bir bağlantı noktası rota gerekir), Azure yük dengeleyici.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-105">If you change your app to use a different port, you must expose that port (or route a different port) in the Azure Load Balancer.</span></span>

<span data-ttu-id="9d7dc-106">Azure service fabric kümesi dağıtıldığında, bir yük dengeleyici sizin için otomatik olarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-106">When you deployed your service fabric cluster to Azure, a load balancer was automatically created for you.</span></span> <span data-ttu-id="9d7dc-107">Bir yük dengeleyici yoksa bkz [bir Internet'e yönelik Yük Dengeleyici yapılandırma](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9d7dc-107">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

## <a name="configure-service-fabric"></a><span data-ttu-id="9d7dc-108">Service fabric yapılandırın</span><span class="sxs-lookup"><span data-stu-id="9d7dc-108">Configure service fabric</span></span>

<span data-ttu-id="9d7dc-109">Service Fabric uygulamanızı **ServiceManifest.xml** yapılandırma dosyasını, uygulamanızın bekliyor kullanmak için uç noktalar tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-109">Your Service Fabric application **ServiceManifest.xml** config file defines the endpoints your application expects to use.</span></span> <span data-ttu-id="9d7dc-110">(Veya farklı bir) kullanıma sunmak için bir uç nokta tanımlamak için yapılandırma dosyası güncelleştirildikten sonra Yük Dengeleyici güncelleştirilmelidir bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-110">After the config file has been updated to define an endpoint, the load balancer must be updated to expose that (or a different) port.</span></span> <span data-ttu-id="9d7dc-111">Hizmet yapı uç noktası oluşturma hakkında daha fazla bilgi için bkz: [bir uç nokta Kurulum](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="9d7dc-111">For more information on how to create the service fabric endpoint, see [Setup an Endpoint](service-fabric-service-manifest-resources.md).</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="9d7dc-112">Yük Dengeleyici kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9d7dc-112">Create a load balancer rule</span></span>

<span data-ttu-id="9d7dc-113">Yük Dengeleyici kuralı bir internet'e yönelik bağlantı açar ve uygulamanız tarafından kullanılan iç düğümün bağlantı trafiğini iletir.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-113">A load balancer rule opens up an internet-facing port and forwards traffic to the internal node's port used by your application.</span></span> <span data-ttu-id="9d7dc-114">Bir yük dengeleyici yoksa bkz [bir Internet'e yönelik Yük Dengeleyici yapılandırma](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9d7dc-114">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

<span data-ttu-id="9d7dc-115">Yük Dengeleyici kuralı oluşturmak için aşağıdaki bilgileri toplayın gerekir:</span><span class="sxs-lookup"><span data-stu-id="9d7dc-115">To create a load balancer rule, you need to collect the following information:</span></span>

- <span data-ttu-id="9d7dc-116">Yük dengeleyicisi adı.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-116">Load balancer name.</span></span>
- <span data-ttu-id="9d7dc-117">Yük Dengeleyici ve service fabric küme kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-117">Resource group of the load balancer and service fabric cluster.</span></span>
- <span data-ttu-id="9d7dc-118">Dış bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-118">External port.</span></span>
- <span data-ttu-id="9d7dc-119">İç bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-119">Internal port.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="9d7dc-120">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9d7dc-120">Azure CLI</span></span>
>[!NOTE]
><span data-ttu-id="9d7dc-121">Yük Dengeleyici adını belirlemek gerekiyorsa, hızlı bir şekilde tüm yük dengeleyicileri ve ilişkili kaynak grupların listesini almak için bu komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-121">If you need to determine the name of the load balancer, use this command to quickly get a list of all load balancers and the associated resource groups.</span></span>
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

<span data-ttu-id="9d7dc-122">Yalnızca bir yük dengeleyici kuralı ile oluşturmak için tek bir komut alır **Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-122">It only takes a single command to create a load balancer rule with the **Azure CLI**.</span></span> <span data-ttu-id="9d7dc-123">Her iki yeni bir kural oluşturmak için yük dengeleyici ve kaynak grubunun adını bilmeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-123">You just need to know both the name of the load balancer and resource group to create a new rule.</span></span>

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

<span data-ttu-id="9d7dc-124">Azure CLI komutu aşağıdaki tabloda açıklanan birkaç parametreleri içerir:</span><span class="sxs-lookup"><span data-stu-id="9d7dc-124">The Azure CLI command has a few parameters that are described in the following table:</span></span>

| <span data-ttu-id="9d7dc-125">Parametre</span><span class="sxs-lookup"><span data-stu-id="9d7dc-125">Parameter</span></span> | <span data-ttu-id="9d7dc-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9d7dc-126">Description</span></span> |
| --------- | ----------- |
| `--backend-port`  | <span data-ttu-id="9d7dc-127">Service fabric uygulaması bağlantı noktası için dinliyor.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-127">The port the service fabric application is listening to.</span></span> |
| `--frontend-port` | <span data-ttu-id="9d7dc-128">Bağlantı noktası yük dengeleyicinin dış bağlantılar için kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-128">The port the load balancer exposes for external connections.</span></span> |
| `-lb-name` | <span data-ttu-id="9d7dc-129">Değiştirmek için yük dengeleyicinin adı.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-129">The name of the load balancer to change.</span></span> |
| `-g`       | <span data-ttu-id="9d7dc-130">Yük Dengeleyici ve service fabric kümesi sahip kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-130">The resource group that has both the load balancer and service fabric cluster.</span></span> |
| `-n`       | <span data-ttu-id="9d7dc-131">Kural seçilen adı.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-131">The chosen name of the rule.</span></span> |


>[!NOTE]
><span data-ttu-id="9d7dc-132">Azure CLI ile bir yük dengeleyici oluşturma hakkında daha fazla bilgi için bkz: [Azure CLI ile bir yük dengeleyici oluşturma](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9d7dc-132">For more information on how to create a load balancer with the Azure CLI, see [Create a load balancer with the Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="9d7dc-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d7dc-133">PowerShell</span></span>

>[!NOTE]
><span data-ttu-id="9d7dc-134">Yük Dengeleyici adını belirlemek gerekiyorsa, hızlı bir şekilde tüm yük dengeleyicileri ve ilişkili kaynak grupların listesini almak için bu komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-134">If you need to determine the name of the load balancer, use this command to quickly get a list of all load balancers and associated resource groups.</span></span>
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

<span data-ttu-id="9d7dc-135">PowerShell Azure CLI biraz daha karmaşıktır.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-135">PowerShell is a little more complicated than the Azure CLI.</span></span> <span data-ttu-id="9d7dc-136">Kavramsal olarak, bir kural oluşturmak için aşağıdaki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-136">Conceptually, do the following steps to create a rule.</span></span>

1. <span data-ttu-id="9d7dc-137">Yük Dengeleyici Azure'dan alın.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-137">Get the load balancer from Azure.</span></span>
2. <span data-ttu-id="9d7dc-138">Bir kural oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-138">Create a rule.</span></span>
3. <span data-ttu-id="9d7dc-139">Kuralı yük dengeleyiciye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-139">Add the rule to the load balancer.</span></span>
4. <span data-ttu-id="9d7dc-140">Yük Dengeleyici güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-140">Update the load balancer.</span></span>

```powershell
# Get the load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create the rule based on information from the load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add the rule to the load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update the load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

<span data-ttu-id="9d7dc-141">İlgili `New-AzureRmLoadBalancerRuleConfig` komutu, `-FrontendPort` yük dengeleyici gösteren dış bağlantıları için bağlantı noktasını temsil eder ve `-BackendPort` service fabric uygulaması için dinlediği bağlantı noktasını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="9d7dc-141">Regarding the `New-AzureRmLoadBalancerRuleConfig` command, the `-FrontendPort` represents the port the load balancer exposes for external connections, and the `-BackendPort` represents the port the service fabric app is listening to.</span></span>

>[!NOTE]
><span data-ttu-id="9d7dc-142">PowerShell ile bir yük dengeleyici oluşturma hakkında daha fazla bilgi için bkz: [PowerShell ile bir yük dengeleyici oluşturma](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9d7dc-142">For more information on how to create a load balancer with PowerShell, see [Create a load balancer with PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span></span>

