---
title: "aaaCreate Azure iç yük dengeleyici - Klasik PowerShell | Microsoft Docs"
description: "Toocreate bir iç yük dengeleyici hello Klasik dağıtım modelinde PowerShell kullanarak nasıl öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 3be93168-3787-45a5-a194-9124fe386493
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 382db80c42ffab09905513019b72e85a4f9dfeff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a><span data-ttu-id="f328f-103">PowerShell kullanarak iç yük dengeleyici (klasik) oluşturmaya başlama</span><span class="sxs-lookup"><span data-stu-id="f328f-103">Get started creating an internal load balancer (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f328f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f328f-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="f328f-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f328f-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="f328f-106">Bulut hizmetleri</span><span class="sxs-lookup"><span data-stu-id="f328f-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="f328f-107">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f328f-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="f328f-108">Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="f328f-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="f328f-109">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="f328f-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="f328f-110">Nasıl çok öğrenin[hello Resource Manager modelini kullanarak bu adımları uygulamadan](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f328f-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="f328f-111">Sanal makineler için iç yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="f328f-111">Create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="f328f-112">bir iç yük dengeleyicisi ayarlayın ve bunların trafiğini tooit göndereceğiniz sunucuları hello toocreate toodo hello aşağıdaki vardır:</span><span class="sxs-lookup"><span data-stu-id="f328f-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you have toodo hello following:</span></span>

1. <span data-ttu-id="f328f-113">İç yük iş yükünün bir yük dengeli kümesi hello sunucular arasında dengeli gelen trafik toobe hello uç nokta olacak Dengeleme örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f328f-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="f328f-114">Merhaba gelen trafiği almak toohello sanal makineleri karşılık gelen uç noktalarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f328f-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="f328f-115">Kendi trafiği toohello sanal IP (VIP) adresi iç Yük Dengeleme hello örneğinin toosend hello trafiği toobe yük dengeli gönderme hello sunucularını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f328f-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

### <a name="step-1-create-an-internal-load-balancing-instance"></a><span data-ttu-id="f328f-116">1. Adım: İç Yük Dengeleme örneği oluşturun</span><span class="sxs-lookup"><span data-stu-id="f328f-116">Step 1: Create an Internal Load Balancing instance</span></span>

<span data-ttu-id="f328f-117">Var olan bir bulut hizmetini veya bölgesel bir sanal ağ altında dağıtılan bir bulut hizmeti için bir iç Yük Dengeleme örneği ile Windows PowerShell komutlarını aşağıdaki hello oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f328f-117">For an existing cloud service or a cloud service deployed under a regional virtual network, you can create an Internal Load Balancing instance with hello following Windows PowerShell commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

<span data-ttu-id="f328f-118">Unutmayın hello bu kullanımını [Ekle AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet hello DefaultProbe parametre kümesi kullanır.</span><span class="sxs-lookup"><span data-stu-id="f328f-118">Note that this use of hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet uses hello DefaultProbe parameter set.</span></span> <span data-ttu-id="f328f-119">Ek parametre kümeleri hakkında daha fazla bilgi için bkz. [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="f328f-119">For more information on additional parameter sets, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span></span>

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a><span data-ttu-id="f328f-120">2. adım: uç noktaları toohello iç Yük Dengeleme örneği ekleme</span><span class="sxs-lookup"><span data-stu-id="f328f-120">Step 2: Add endpoints toohello Internal Load Balancing instance</span></span>

<span data-ttu-id="f328f-121">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f328f-121">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
$lbsetname="lbset"
$prot="tcp"
$locport=1433
$pubport=1433
$ilb="ilbset"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -Lbset $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a><span data-ttu-id="f328f-122">3. adım: sunucuları toosend kendi trafiği toohello yeni iç Yük Dengeleme uç noktasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f328f-122">Step 3: Configure your servers toosend their traffic toohello new Internal Load Balancing endpoint</span></span>

<span data-ttu-id="f328f-123">Sahip çok yapılandırdığınız hello sunucuları, trafiğine giderek toobe yükü dengelenmiş toouse hello yeni IP adresi (Merhaba VIP) hello iç Yük Dengeleme örnek olacak.</span><span class="sxs-lookup"><span data-stu-id="f328f-123">You have too configure hello servers whose traffic is going toobe load balanced toouse hello new IP address (hello VIP) of hello Internal Load Balancing instance.</span></span> <span data-ttu-id="f328f-124">Bu örnek hangi hello üzerinde iç Yük Dengeleme dinleme hello adresidir.</span><span class="sxs-lookup"><span data-stu-id="f328f-124">This is hello address on which hello Internal Load Balancing instance is listening.</span></span> <span data-ttu-id="f328f-125">Çoğu durumda, toojust gereksinim ekleyin veya hello VIP hello örneğinin iç Yük Dengeleme için bir DNS kaydı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f328f-125">In most cases, you need toojust add or modify a DNS record for hello VIP of hello Internal Load Balancing instance.</span></span>

<span data-ttu-id="f328f-126">Başlangıç IP adresi hello iç Yük Dengeleme örnek hello oluşturma sırasında belirtilen zaten hello VIP varsa.</span><span class="sxs-lookup"><span data-stu-id="f328f-126">If you specified hello IP address during hello creation of hello Internal Load Balancing instance, you already have hello VIP.</span></span> <span data-ttu-id="f328f-127">Aksi takdirde, komutları aşağıdaki hello gelen hello VIP görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f328f-127">Otherwise, you can see hello VIP from hello following commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="f328f-128">toouse bu komutları doldurun hello değerleri ve Kaldır merhaba < ve >.</span><span class="sxs-lookup"><span data-stu-id="f328f-128">toouse these commands, fill in hello values and remove hello < and >.</span></span> <span data-ttu-id="f328f-129">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f328f-129">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="f328f-130">Merhaba Get-AzureInternalLoadBalancer komutu görüntüsünü Merhaba, hello IP adresini not edin ve hello gerekli değişiklikleri tooyour sunucuları veya trafiği toohello VIP gönderilir DNS kayıtları tooensure olun.</span><span class="sxs-lookup"><span data-stu-id="f328f-130">From hello display of hello Get-AzureInternalLoadBalancer command, note hello IP address and make hello necessary changes tooyour servers or DNS records tooensure that traffic gets sent toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="f328f-131">Merhaba Microsoft Azure platformu statik, genel olarak yönlendirilebilir bir IPv4 adresi çeşitli yönetim senaryoları için kullanır.</span><span class="sxs-lookup"><span data-stu-id="f328f-131">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="f328f-132">Başlangıç IP adresi 168.63.129.16 değil.</span><span class="sxs-lookup"><span data-stu-id="f328f-132">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="f328f-133">Bu IP adresinin güvenlik duvarları tarafından engellenmesi beklenmeyen davranışlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="f328f-133">This IP address should not be blocked by any firewalls, because it can cause unexpected behavior.</span></span>
> <span data-ttu-id="f328f-134">Saygı tooAzure ile iç Yük Dengeleme, bu IP adresi, yük dengelenmiş bir küme içinde sanal makineler için hello yük dengeleyici toodetermine hello sistem durumu araştırmalarının izleme tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f328f-134">With respect tooAzure Internal Load Balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load balanced set.</span></span> <span data-ttu-id="f328f-135">Bir ağ güvenlik grubu kullanılan toorestrict trafiği tooAzure sanal makineleri bir dahili yük dengeli kümesindeki ya uygulanan tooa sanal ağ alt ağı ise, bir ağ güvenlik kuralı tooallow trafiği 168.63.129.16 eklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="f328f-135">If a Network Security Group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa Virtual Network Subnet, ensure that a Network Security Rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="example-of-internal-load-balancing"></a><span data-ttu-id="f328f-136">İç yük dengeleme örneği</span><span class="sxs-lookup"><span data-stu-id="f328f-136">Example of internal load balancing</span></span>

<span data-ttu-id="f328f-137">iki örnek yapılandırmalar için yük dengeli kümesi oluşturma hello son tooend işlemiyle toostep gördüğünüz hello bölümler.</span><span class="sxs-lookup"><span data-stu-id="f328f-137">toostep you through hello end-tooend process of creating a load-balanced set for two example configurations, see hello following sections.</span></span>

### <a name="an-internet-facing-multi-tier-application"></a><span data-ttu-id="f328f-138">İnternet'e yönelik, çok katmanlı uygulama</span><span class="sxs-lookup"><span data-stu-id="f328f-138">An Internet facing, multi-tier application</span></span>

<span data-ttu-id="f328f-139">Tooprovide İnternete dönük web sunucuları kümesi için bir yük dengeli veritabanı hizmeti istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="f328f-139">You want tooprovide a load balanced database service for  a set of Internet-facing web servers.</span></span> <span data-ttu-id="f328f-140">İki sunucu kümesi de tek bir Azure bulut hizmetinde.</span><span class="sxs-lookup"><span data-stu-id="f328f-140">Both sets of servers are hosted in a single Azure cloud service.</span></span> <span data-ttu-id="f328f-141">Web sunucusu trafiği tooTCP bağlantı noktası 1433 hello veritabanı katmanı iki sanal makine arasında dağıtılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f328f-141">Web server traffic tooTCP port 1433 must be distributed among two virtual machines in hello database tier.</span></span> <span data-ttu-id="f328f-142">Şekil 1'hello yapılandırmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f328f-142">Figure 1 shows hello configuration.</span></span>

![Merhaba veritabanı katmanı için iç yük dengeli kümesi](./media/load-balancer-internal-getstarted/IC736321.png)

<span data-ttu-id="f328f-144">Merhaba yapılandırması hello aşağıdakilerden oluşur:</span><span class="sxs-lookup"><span data-stu-id="f328f-144">hello configuration consists of hello following:</span></span>

* <span data-ttu-id="f328f-145">Merhaba sanal makineleri barındıran hello mevcut bulut hizmeti mytestcloud adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="f328f-145">hello existing cloud service hosting hello virtual machines is named mytestcloud.</span></span>
* <span data-ttu-id="f328f-146">Merhaba iki varolan veritabanı sunucuları DB1, DB2 adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="f328f-146">hello two existing database servers are named DB1, DB2.</span></span>
* <span data-ttu-id="f328f-147">Merhaba web katmanı Web sunucularının hello veritabanı katmanı toohello veritabanı sunucuları hello özel IP adresini kullanarak bağlanın.</span><span class="sxs-lookup"><span data-stu-id="f328f-147">Web servers in hello web tier connect toohello database servers in hello database tier by using hello private IP address.</span></span> <span data-ttu-id="f328f-148">Başka bir seçenek hello sanal ağ için kendi DNS toouse olan ve hello iç yük dengeleyici kümesi için bir A kaydı el ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f328f-148">Another option is toouse your own DNS for hello virtual network and manually register an A record for hello internal load balancer set.</span></span>

<span data-ttu-id="f328f-149">Merhaba aşağıdaki komutları yapılandırma adlı yeni bir iç Yük Dengeleme örnek **ILBset** ve toohello iki veritabanı sunucularına karşılık gelen uç noktaları toohello sanal makineleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f328f-149">hello following commands configure a new Internal Load Balancing instance named **ILBset** and add endpoints toohello virtual machines corresponding toohello two database servers:</span></span>

```powershell
$svc="mytestcloud"
$ilb="ilbset"
Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb
$prot="tcp"
$locport=1433
$pubport=1433
$epname="TCP-1433-1433"
$lbsetname="lbset"
$vmname="DB1"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM

$epname="TCP-1433-1433-2"
$vmname="DB2"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

## <a name="remove-an-internal-load-balancing-configuration"></a><span data-ttu-id="f328f-150">İç Yük Dengeleme yapılandırmasını kaldırma</span><span class="sxs-lookup"><span data-stu-id="f328f-150">Remove an Internal Load Balancing configuration</span></span>

<span data-ttu-id="f328f-151">sanal makine örneğinden bir iç yük dengeleyici, aşağıdaki komutları kullanın hello bir uç nokta olarak tooremove:</span><span class="sxs-lookup"><span data-stu-id="f328f-151">tooremove a virtual machine as an endpoint from an internal load balancer instance, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="f328f-152">toouse bu komutları doldurun hello kaldırma hello değerlerde < ve >.</span><span class="sxs-lookup"><span data-stu-id="f328f-152">toouse these commands, fill in hello values, removing hello < and >.</span></span>

<span data-ttu-id="f328f-153">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f328f-153">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="f328f-154">tooremove aşağıdaki komutları kullanın hello bir bulut hizmeti bir iç yük dengeleyici örneği:</span><span class="sxs-lookup"><span data-stu-id="f328f-154">tooremove an internal load balancer instance from a cloud service, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

<span data-ttu-id="f328f-155">Bu komutlar, toouse hello değer girin ve hello Kaldır < ve >.</span><span class="sxs-lookup"><span data-stu-id="f328f-155">toouse these commands, fill in hello value and remove hello < and >.</span></span>

<span data-ttu-id="f328f-156">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f328f-156">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a><span data-ttu-id="f328f-157">İç yük dengeleyici cmdlet'leri hakkında ek bilgi</span><span class="sxs-lookup"><span data-stu-id="f328f-157">Additional information about internal load balancer cmdlets</span></span>

<span data-ttu-id="f328f-158">tooobtain komutlar Windows PowerShell isteminde aşağıdaki hello çalıştırmak, iç Yük Dengeleme cmdlet'leri hakkında ek bilgi:</span><span class="sxs-lookup"><span data-stu-id="f328f-158">tooobtain additional information about Internal Load Balancing cmdlets, run hello following commands at a Windows PowerShell prompt:</span></span>

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a><span data-ttu-id="f328f-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f328f-159">Next steps</span></span>

[<span data-ttu-id="f328f-160">Kaynak IP benzeşimi kullanarak yük dengeleyici dağıtım modunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f328f-160">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="f328f-161">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f328f-161">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

