---
title: "aaaConfigure yük dengeleyici her zaman açık SQL için | Microsoft Docs"
description: "Yük Dengeleyici toowork her zaman SQL ve nasıl tooleverage powershell toocreate yük dengeleyici hello SQL uygulaması için yapılandırın"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac6200b18f725dadee2555b80055327d379417d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a><span data-ttu-id="f75e0-103">Yük Dengeleyici SQL için her zaman yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f75e0-103">Configure load balancer for SQL always on</span></span>

<span data-ttu-id="f75e0-104">SQL Server AlwaysOn Kullanılabilirlik grupları şimdi ILB ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f75e0-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span></span> <span data-ttu-id="f75e0-105">Kullanılabilirlik grubu SQL Server'ın flagship için yüksek kullanılabilirlik ve olağanüstü durum kurtarma çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="f75e0-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="f75e0-106">Merhaba kullanılabilirlik grubu dinleyicisi sağlayan istemci uygulamaları tooseamlessly hello hello yapılandırmasında hello çoğaltmaların sayısı yedeklemiş toohello birincil çoğaltma bağlanın.</span><span class="sxs-lookup"><span data-stu-id="f75e0-106">hello Availability Group Listener allows client applications tooseamlessly connect toohello primary replica, irrespective of hello number of hello replicas in hello configuration.</span></span>

<span data-ttu-id="f75e0-107">Merhaba dinleyicisi (DNS) ad eşlenen tooa yük dengeli IP adresi ve Azure'nın yük dengeleyici hello gelen trafiği tooonly hello birincil sunucusu hello çoğaltma kümesinde yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="f75e0-107">hello listener (DNS) name is mapped tooa load-balanced IP address and Azure's load balancer directs hello incoming traffic tooonly hello primary server in hello replica set.</span></span>

<span data-ttu-id="f75e0-108">ILB desteği SQL Server AlwaysOn (dinleyici) uç noktaları için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f75e0-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span></span> <span data-ttu-id="f75e0-109">Şimdi hello dinleyicisi hello erişilebilirliğini üzerinde denetimi yoktur ve hello yük dengeli IP adresi, sanal ağ (VNet) belirli bir alt ağdan seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f75e0-109">You now have control over hello accessibility of hello listener and can choose hello load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span></span>

<span data-ttu-id="f75e0-110">Merhaba Dinleyicide ILB kullanarak, SQL sunucusu uç noktası hello (örneğin Server 1433; tcp:ListenerName, = veritabanı DatabaseName =) yalnızca tarafından erişilebilen:</span><span class="sxs-lookup"><span data-stu-id="f75e0-110">By using ILB on hello listener, hello SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="f75e0-111">Aynı sanal ağ hizmetleri ve Vm'lerde hello</span><span class="sxs-lookup"><span data-stu-id="f75e0-111">Services and VMs in hello same Virtual network</span></span>
* <span data-ttu-id="f75e0-112">Hizmetler ve bağlı şirket içi ağ üzerinden VM'ler</span><span class="sxs-lookup"><span data-stu-id="f75e0-112">Services and VMs from connected on-premises network</span></span>
* <span data-ttu-id="f75e0-113">Hizmetler ve VM'lerin birbirine bağlı sanal ağlar</span><span class="sxs-lookup"><span data-stu-id="f75e0-113">Services and VMs from interconnected VNets</span></span>

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

<span data-ttu-id="f75e0-115">Şekil 1 - SQL AlwaysOn Internet'e yönelik Yük Dengeleyici ile yapılandırılmış</span><span class="sxs-lookup"><span data-stu-id="f75e0-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span></span>

## <a name="add-internal-load-balancer-toohello-service"></a><span data-ttu-id="f75e0-116">İç yük dengeleyici toohello Hizmet Ekle</span><span class="sxs-lookup"><span data-stu-id="f75e0-116">Add Internal Load Balancer toohello service</span></span>

1. <span data-ttu-id="f75e0-117">Aşağıdaki örneğine hello biz 'Alt ağ-1' adlı bir alt ağ içeren bir sanal ağ yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="f75e0-117">In hello following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="f75e0-118">Her bir VM üzerinde ILB için yük dengeli uç noktaları ekleme</span><span class="sxs-lookup"><span data-stu-id="f75e0-118">Add load balanced endpoints for ILB on each VM</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="f75e0-119">Merhaba yukarıdaki örnekte, 2 VM'ın adlandırılan "sqlsvc1" ve "sqlsvc2" çalışan elinizde "Sqlsvc" Merhaba buluta hizmet.</span><span class="sxs-lookup"><span data-stu-id="f75e0-119">In hello example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in hello cloud service "Sqlsvc".</span></span> <span data-ttu-id="f75e0-120">ILB ile Merhaba oluşturduktan sonra `DirectServerReturn` geçiş, eklediğiniz yük dengeli uç noktalar toohello ILB tooallow SQL tooconfigure hello dinleyicileri hello kullanılabilirlik grupları için.</span><span class="sxs-lookup"><span data-stu-id="f75e0-120">After creating hello ILB with `DirectServerReturn` switch, you add load balanced endpoints toohello ILB tooallow SQL tooconfigure hello listeners for hello availability groups.</span></span>

<span data-ttu-id="f75e0-121">SQL AlwaysOn hakkında daha fazla bilgi için bkz: [Azure'da AlwaysOn Kullanılabilirlik grubu için bir iç yük dengeleyici yapılandırma](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="f75e0-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="f75e0-122">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f75e0-122">See Also</span></span>
[<span data-ttu-id="f75e0-123">Internet'e yönelik Yük Dengeleyici yapılandırma kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="f75e0-123">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="f75e0-124">Bir iç yük dengeleyici yapılandırma kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="f75e0-124">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="f75e0-125">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f75e0-125">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="f75e0-126">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f75e0-126">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
