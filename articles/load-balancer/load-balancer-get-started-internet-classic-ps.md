---
title: "İnternet’e yönelik yük dengeleyicisi oluşturma - Azure PowerShell klasik | Microsoft Docs"
description: "Klasik modda PowerShell kullanarak İnternet’e yönelik yük dengeleyici oluşturmayı öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 1a41f3ba199fb692c111ea6a40ddb09605f91da2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a><span data-ttu-id="4777d-103">PowerShell’de İnternet’e yönelik yük dengeleyici (klasik) oluşturmaya başlama</span><span class="sxs-lookup"><span data-stu-id="4777d-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4777d-104">Klasik Azure portalı</span><span class="sxs-lookup"><span data-stu-id="4777d-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="4777d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4777d-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="4777d-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4777d-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="4777d-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="4777d-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="4777d-108">Azure kaynaklarıyla çalışmadan önce Azure’da şu anda iki dağıtım modeli olduğunu anlamak önemlidir: Azure Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="4777d-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="4777d-109">Azure kaynaklarıyla çalışmadan önce [dağıtım modellerini ve araçlarlarını](../azure-classic-rm.md) iyice anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4777d-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="4777d-110">Bu makalenin en üstündeki sekmelere tıklayarak farklı araçlarla ilgili belgeleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4777d-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="4777d-111">Bu makale, klasik dağıtım modelini kapsamaktadır.</span><span class="sxs-lookup"><span data-stu-id="4777d-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="4777d-112">[Azure Resource Manager kullanarak İnternet’e yönelik yük dengeleyici oluşturma](load-balancer-get-started-internet-arm-ps.md) sayfasını da inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4777d-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a><span data-ttu-id="4777d-113">PowerShell kullanarak iç yük dengeleyici kurma</span><span class="sxs-lookup"><span data-stu-id="4777d-113">Set up load balancer using PowerShell</span></span>

<span data-ttu-id="4777d-114">PowerShell kullanarak yük dengeleyici oluşturmak için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="4777d-114">To set up a load balancer using powershell, follow the steps below:</span></span>

1. <span data-ttu-id="4777d-115">Daha önce Azure PowerShell kullanmadıysanız, [Azure PowerShell’i Yükleme ve Yapılandırma](/powershell/azure/overview) sayfasına gidin ve Azure’da oturum açıp aboneliğinizi seçmek için talimatları sonuna kadar uygulayın.</span><span class="sxs-lookup"><span data-stu-id="4777d-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="4777d-116">Sanal makine oluşturduktan sonra PowerShell cmdlet’lerini kullanarak aynı bulut hizmeti içindeki bir sanal makineye yük dengeleyici ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4777d-116">After creating a virtual machine, you can use PowerShell cmdlets to add a load balancer to a virtual machine within the same cloud service.</span></span>

<span data-ttu-id="4777d-117">Aşağıdaki örnekte "web1" ve "web2" adlı sanal makinelere yük dengeleyici uç noktaları ekleyerek "mytestcloud" (veya myctestcloud.cloudapp.net) bulut hizmetine "webfarm" adlı bir yük dengeleyici kümesi ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="4777d-117">In the following example you will add a load balancer set called "webfarm" to cloud service "mytestcloud" (or myctestcloud.cloudapp.net) , adding the endpoints for the load balancer to virtual machines named "web1" and "web2".</span></span> <span data-ttu-id="4777d-118">Yük dengeleyici 80 numaralı bağlantı noktasından ağ trafiğini alır ve TCP kullanarak yerel uç noktası (bu durumda 80 numaralı bağlantı noktası) tarafından tanımlanan sanal makineler arasında yük dengeleme gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="4777d-118">The load balancer receives network traffic on port 80 and load balances between the virtual machines defined by the local endpoint (in this case port 80) using TCP.</span></span>

### <a name="step-1"></a><span data-ttu-id="4777d-119">1. Adım</span><span class="sxs-lookup"><span data-stu-id="4777d-119">Step 1</span></span>

<span data-ttu-id="4777d-120">İlk VM olan "web1" için yük dengeli uç nokta oluşturma</span><span class="sxs-lookup"><span data-stu-id="4777d-120">Create a load balanced endpoint for the first VM "web1"</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a><span data-ttu-id="4777d-121">2. Adım</span><span class="sxs-lookup"><span data-stu-id="4777d-121">Step 2</span></span>

<span data-ttu-id="4777d-122">İkinci VM olan "web2" için aynı yük dengeleyici kümesi adını kullanarak başka bir uç nokta oluşturma</span><span class="sxs-lookup"><span data-stu-id="4777d-122">Create another endpoint for the second VM  "web2" using the same load balancer set name</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a><span data-ttu-id="4777d-123">Yük dengeleyiciden sanal makineyi kaldırma</span><span class="sxs-lookup"><span data-stu-id="4777d-123">Remove a virtual machine from a load balancer</span></span>

<span data-ttu-id="4777d-124">Bir sanal makine uç noktasını yük dengeleyiciden kaldırmak için Remove-AzureEndpoint komutunu kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4777d-124">You can use Remove-AzureEndpoint to remove a virtual machine endpoint from the load balancer</span></span>

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a><span data-ttu-id="4777d-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4777d-125">Next steps</span></span>

<span data-ttu-id="4777d-126">[İç yük dengeleyici oluşturmaya başlayabilir](load-balancer-get-started-ilb-classic-ps.md) ve belirli bir yük dengeleyici ağ trafiği davranışı için [dağıtım modu](load-balancer-distribution-mode.md) türünü yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4777d-126">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="4777d-127">Uygulamanızın yük dengeleyici arkasındaki sunucular için bağlantıları canlı tutması gerekiyorsa [yük dengeleyici için boşta kalma TCP zaman aşımı ayarları](load-balancer-tcp-idle-timeout.md) hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4777d-127">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="4777d-128">Bu, Azure Load Balancer kullanırken boşta kalan bağlantı davranışları hakkında bilgi edinmenizi sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="4777d-128">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span></span>
