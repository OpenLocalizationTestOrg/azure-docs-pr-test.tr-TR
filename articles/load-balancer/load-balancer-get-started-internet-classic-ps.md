---
title: "Klasik Azure PowerShell aaaCreate bir Internet'e yönelik Yük Dengeleyici - | Microsoft Docs"
description: "Nasıl toocreate Internet'e yönelik Yük Dengeleyici PowerShell kullanarak Klasik modda öğrenin"
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
ms.openlocfilehash: 76d9a712a0acda223fc86b80be9c35c0ed9f3a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a><span data-ttu-id="46cde-103">PowerShell’de İnternet’e yönelik yük dengeleyici (klasik) oluşturmaya başlama</span><span class="sxs-lookup"><span data-stu-id="46cde-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="46cde-104">Klasik Azure portalı</span><span class="sxs-lookup"><span data-stu-id="46cde-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="46cde-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="46cde-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="46cde-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="46cde-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="46cde-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="46cde-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="46cde-108">Azure kaynaklarıyla çalışmadan önce Azure'da şu anda iki dağıtım modeli olduğunu önemli toounderstand olduğu: Azure Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="46cde-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="46cde-109">Azure kaynaklarıyla çalışmadan önce [dağıtım modellerini ve araçlarlarını](../azure-classic-rm.md) iyice anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="46cde-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="46cde-110">Bu makalenin hello üstünde hello sekmeleri tıklayarak farklı araçlarla ilgili hello belgeleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46cde-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="46cde-111">Bu makalede, hello Klasik dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="46cde-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="46cde-112">Ayrıca [nasıl toocreate Internet'e yönelik Yük Dengeleyici Azure Resource Manager kullanarak bilgi](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="46cde-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a><span data-ttu-id="46cde-113">PowerShell kullanarak iç yük dengeleyici kurma</span><span class="sxs-lookup"><span data-stu-id="46cde-113">Set up load balancer using PowerShell</span></span>

<span data-ttu-id="46cde-114">powershell kullanarak bir yük dengeleyici yukarı tooset hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="46cde-114">tooset up a load balancer using powershell, follow hello steps below:</span></span>

1. <span data-ttu-id="46cde-115">Azure PowerShell'i hiç kullanmadıysanız bkz [nasıl tooInstall ve yapılandırma Azure PowerShell](/powershell/azure/overview) ve tüm hello yolu toohello toosign Azure'da sonlandırmak ve aboneliğinizi seçin hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="46cde-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="46cde-116">Bir sanal makine oluşturduktan sonra PowerShell cmdlet'leri tooadd bir yük dengeleyici tooa sanal makine kullanabilirsiniz hello içinde aynı bulut hizmeti.</span><span class="sxs-lookup"><span data-stu-id="46cde-116">After creating a virtual machine, you can use PowerShell cmdlets tooadd a load balancer tooa virtual machine within hello same cloud service.</span></span>

<span data-ttu-id="46cde-117">Hello aşağıdaki örnek, bir yük dengeleyici Küme hizmeti "mytestcloud" (veya myctestcloud.cloudapp.net) hello uç noktaları hello için yük dengeleyici toovirtual ekleme makineler "webfarm" toocloud adlı ekleyeceksiniz "web1" ve "web2" adlı.</span><span class="sxs-lookup"><span data-stu-id="46cde-117">In hello following example you will add a load balancer set called "webfarm" toocloud service "mytestcloud" (or myctestcloud.cloudapp.net) , adding hello endpoints for hello load balancer toovirtual machines named "web1" and "web2".</span></span> <span data-ttu-id="46cde-118">Merhaba yük dengeleyici ağ trafiği 80 numaralı bağlantı noktasında alır ve yükünü dengeleyen hello yerel uç (Bu örnek bağlantı noktası 80) tarafından tanımlanan hello sanal makineler arasında TCP kullanarak.</span><span class="sxs-lookup"><span data-stu-id="46cde-118">hello load balancer receives network traffic on port 80 and load balances between hello virtual machines defined by hello local endpoint (in this case port 80) using TCP.</span></span>

### <a name="step-1"></a><span data-ttu-id="46cde-119">1. Adım</span><span class="sxs-lookup"><span data-stu-id="46cde-119">Step 1</span></span>

<span data-ttu-id="46cde-120">Merhaba ilk VM "web1" için bir yük dengeli uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="46cde-120">Create a load balanced endpoint for hello first VM "web1"</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a><span data-ttu-id="46cde-121">2. Adım</span><span class="sxs-lookup"><span data-stu-id="46cde-121">Step 2</span></span>

<span data-ttu-id="46cde-122">Merhaba ikinci hello kullanarak VM "web2" aynı dengeleyici kümesi adı yüklemek için başka bir uç noktası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="46cde-122">Create another endpoint for hello second VM  "web2" using hello same load balancer set name</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a><span data-ttu-id="46cde-123">Yük dengeleyiciden sanal makineyi kaldırma</span><span class="sxs-lookup"><span data-stu-id="46cde-123">Remove a virtual machine from a load balancer</span></span>

<span data-ttu-id="46cde-124">Remove-AzureEndpoint tooremove hello yük dengeleyiciden sanal makine uç noktası kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="46cde-124">You can use Remove-AzureEndpoint tooremove a virtual machine endpoint from hello load balancer</span></span>

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a><span data-ttu-id="46cde-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="46cde-125">Next steps</span></span>

<span data-ttu-id="46cde-126">[İç yük dengeleyici oluşturmaya başlayabilir](load-balancer-get-started-ilb-classic-ps.md) ve belirli bir yük dengeleyici ağ trafiği davranışı için [dağıtım modu](load-balancer-distribution-mode.md) türünü yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46cde-126">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="46cde-127">Uygulamanızı tookeep bağlantıları canlı bir yük dengeleyicinin arkasındaki sunucular için gerekiyorsa, daha fazla hakkında anlayabileceği [boşta bir yük dengeleyici için TCP zaman aşımı ayarları](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="46cde-127">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="46cde-128">Azure yük dengeleyici kullanırken toolearn boştaki bağlantı davranışı konusunda yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="46cde-128">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>
