---
title: "Azure İç yük dengeleyicisi oluşturma - PowerShell klasik | Microsoft Docs"
description: "Klasik dağıtım modelinde PowerShell kullanarak iç yük dengeleyici oluşturmayı öğrenin"
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
ms.openlocfilehash: f701fb3564c62cf8088cc4362a10c5e2c2301ae6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a><span data-ttu-id="ac22e-103">PowerShell kullanarak iç yük dengeleyici (klasik) oluşturmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ac22e-103">Get started creating an internal load balancer (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac22e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac22e-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="ac22e-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ac22e-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="ac22e-106">Bulut hizmetleri</span><span class="sxs-lookup"><span data-stu-id="ac22e-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="ac22e-107">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ac22e-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="ac22e-108">Bu makale klasik dağıtım modelini incelemektedir.</span><span class="sxs-lookup"><span data-stu-id="ac22e-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="ac22e-109">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="ac22e-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="ac22e-110">[Bu adımları Resource Manager modeli kullanarak gerçekleştirmeyi](load-balancer-get-started-ilb-arm-ps.md) öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ac22e-110">Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="ac22e-111">Sanal makineler için iç yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="ac22e-111">Create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="ac22e-112">İç yük dengeleyici kümesi ve trafiğini bu kümeye gönderecek sunucuları oluşturmak için aşağıdaki adımları uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ac22e-112">To create an internal load balancer set and the servers that will send their traffic to it, you have to do the following:</span></span>

1. <span data-ttu-id="ac22e-113">Gelen trafiğin uç noktası olacak ve bu trafiğe yük dengeli bir kümenin sunucularında yük dengelemesi yapacak bir İç Yük Dengeleme örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ac22e-113">Create an instance of Internal Load Balancing that will be the endpoint of incoming traffic to be load balanced across the servers of a load-balanced set.</span></span>
2. <span data-ttu-id="ac22e-114">Gelen trafiği alacak sanal makinelere karşılık gelen uç noktalar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ac22e-114">Add endpoints corresponding to the virtual machines that will be receiving the incoming traffic.</span></span>
3. <span data-ttu-id="ac22e-115">Yük dengelemesi yapılacak trafiği gönderecek sunucuları trafiklerini İç Yük Dengeleme örneğinin sanal IP (VIP) adresine gönderecek şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ac22e-115">Configure the servers that will be sending the traffic to be load balanced to send their traffic to the virtual IP (VIP) address of the Internal Load Balancing instance.</span></span>

### <a name="step-1-create-an-internal-load-balancing-instance"></a><span data-ttu-id="ac22e-116">1. Adım: İç Yük Dengeleme örneği oluşturun</span><span class="sxs-lookup"><span data-stu-id="ac22e-116">Step 1: Create an Internal Load Balancing instance</span></span>

<span data-ttu-id="ac22e-117">Mevcut bir bulut hizmeti veya bölgesel sanal ağ üzerine dağıtılmış bulut hizmeti için aşağıdaki Windows PowerShell komutlarını kullanarak İç Yük Dengeleme örneğin oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ac22e-117">For an existing cloud service or a cloud service deployed under a regional virtual network, you can create an Internal Load Balancing instance with the following Windows PowerShell commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of the subnet within your virtual network>"
$IP="<The IPv4 address to use on the subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

<span data-ttu-id="ac22e-118">Bu [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet örneğinde DefaultProbe parametre kümesi kullanıldığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="ac22e-118">Note that this use of the [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet uses the DefaultProbe parameter set.</span></span> <span data-ttu-id="ac22e-119">Ek parametre kümeleri hakkında daha fazla bilgi için bkz. [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac22e-119">For more information on additional parameter sets, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span></span>

### <a name="step-2-add-endpoints-to-the-internal-load-balancing-instance"></a><span data-ttu-id="ac22e-120">2. Adım: İç Yük Dengeleme örneğine uç noktaları ekleyin</span><span class="sxs-lookup"><span data-stu-id="ac22e-120">Step 2: Add endpoints to the Internal Load Balancing instance</span></span>

<span data-ttu-id="ac22e-121">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ac22e-121">Here is an example:</span></span>

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

### <a name="step-3-configure-your-servers-to-send-their-traffic-to-the-new-internal-load-balancing-endpoint"></a><span data-ttu-id="ac22e-122">3. Adım: Sunucularınızı trafiklerini yeni İç Yük Dengeleme uç noktasına gönderecek şekilde yapılandırın</span><span class="sxs-lookup"><span data-stu-id="ac22e-122">Step 3: Configure your servers to send their traffic to the new Internal Load Balancing endpoint</span></span>

<span data-ttu-id="ac22e-123">Yük dengelemesi uygulanacak trafiğe sahip sunucuları İç Yük Dengeleme örneğinin yeni IP adresini (VIP) kullanacak şekilde yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac22e-123">You have to  configure the servers whose traffic is going to be load balanced to use the new IP address (the VIP) of the Internal Load Balancing instance.</span></span> <span data-ttu-id="ac22e-124">Bu, İç Yük Dengeleme örneğinin dinlediği adrestir.</span><span class="sxs-lookup"><span data-stu-id="ac22e-124">This is the address on which the Internal Load Balancing instance is listening.</span></span> <span data-ttu-id="ac22e-125">Çoğu durumda tek yapmanız gereken İç Yük Dengeleme örneği VIP’sinin DNS kaydını yapmak veya değiştirmektir.</span><span class="sxs-lookup"><span data-stu-id="ac22e-125">In most cases, you need to just add or modify a DNS record for the VIP of the Internal Load Balancing instance.</span></span>

<span data-ttu-id="ac22e-126">İç Yük Dengeleme örneğini oluştururken IP adresi belirttiyseniz VIP’ye sahipsiniz demektir.</span><span class="sxs-lookup"><span data-stu-id="ac22e-126">If you specified the IP address during the creation of the Internal Load Balancing instance, you already have the VIP.</span></span> <span data-ttu-id="ac22e-127">Belirtmediyseniz VIP’yi görmek için aşağıdaki komutları kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ac22e-127">Otherwise, you can see the VIP from the following commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="ac22e-128">Bu komutları kullanmak için istenen değerleri yazıp < ve > işaretlerini silin.</span><span class="sxs-lookup"><span data-stu-id="ac22e-128">To use these commands, fill in the values and remove the < and >.</span></span> <span data-ttu-id="ac22e-129">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ac22e-129">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="ac22e-130">Get-AzureInternalLoadBalancer komutu ekranındaki IP adresini not edin ve trafiğin VIP’ye gönderildiğinden emin olmak için sunucularınızda veya DNS kayıtlarınızda gerekli değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="ac22e-130">From the display of the Get-AzureInternalLoadBalancer command, note the IP address and make the necessary changes to your servers or DNS records to ensure that traffic gets sent to the VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="ac22e-131">Microsoft Azure platformu, farklı yönetim senaryoları için genel olarak yönlendirilebilen statik bir IPv4 adresi kullanır.</span><span class="sxs-lookup"><span data-stu-id="ac22e-131">The Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="ac22e-132">IP adresi: 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="ac22e-132">The IP address is 168.63.129.16.</span></span> <span data-ttu-id="ac22e-133">Bu IP adresinin güvenlik duvarları tarafından engellenmesi beklenmeyen davranışlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="ac22e-133">This IP address should not be blocked by any firewalls, because it can cause unexpected behavior.</span></span>
> <span data-ttu-id="ac22e-134">Azure İç Yük Dengeleme açısından bu IP adresi, araştırmaların yük dengeleyiciden izlenerek yük dengeli kümede yer alan sanal makinelerin durumunun belirlenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ac22e-134">With respect to Azure Internal Load Balancing, this IP address is used by monitoring probes from the load balancer to determine the health state for virtual machines in a load balanced set.</span></span> <span data-ttu-id="ac22e-135">Bir iç yük dengeli kümedeki Azure sanal makinelerine gelen trafiği kısıtlamak için bir Ağ Güvenlik Grubu kullanılması veya Sanal Alt Ağ uygulanması halinde 168.63.129.16 adresinden gelen trafiğe izin verecek şekilde bir Ağ Güvenlik Kuralının uygulandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="ac22e-135">If a Network Security Group is used to restrict traffic to Azure virtual machines in an internally load-balanced set or is applied to a Virtual Network Subnet, ensure that a Network Security Rule is added to allow traffic from 168.63.129.16.</span></span>

## <a name="example-of-internal-load-balancing"></a><span data-ttu-id="ac22e-136">İç yük dengeleme örneği</span><span class="sxs-lookup"><span data-stu-id="ac22e-136">Example of internal load balancing</span></span>

<span data-ttu-id="ac22e-137">İki örnek yapılandırma için yük dengeli küme oluşturmayla ilgili adım adım talimatlar için aşağıdaki bölümlere bakın.</span><span class="sxs-lookup"><span data-stu-id="ac22e-137">To step you through the end-to end process of creating a load-balanced set for two example configurations, see the following sections.</span></span>

### <a name="an-internet-facing-multi-tier-application"></a><span data-ttu-id="ac22e-138">İnternet'e yönelik, çok katmanlı uygulama</span><span class="sxs-lookup"><span data-stu-id="ac22e-138">An Internet facing, multi-tier application</span></span>

<span data-ttu-id="ac22e-139">İnternet’e yönelik web sunucusu kümesi için yük dengeli veritabanı hizmeti sunmak istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="ac22e-139">You want to provide a load balanced database service for  a set of Internet-facing web servers.</span></span> <span data-ttu-id="ac22e-140">İki sunucu kümesi de tek bir Azure bulut hizmetinde.</span><span class="sxs-lookup"><span data-stu-id="ac22e-140">Both sets of servers are hosted in a single Azure cloud service.</span></span> <span data-ttu-id="ac22e-141">1433 numaralı TCP bağlantı noktasına gelen web sunucusu trafiğinin veritabanı katmanındaki iki sanal makineye dağıtılması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="ac22e-141">Web server traffic to TCP port 1433 must be distributed among two virtual machines in the database tier.</span></span> <span data-ttu-id="ac22e-142">Yapılandırma Şekil 1’de gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ac22e-142">Figure 1 shows the configuration.</span></span>

![Veritabanı katmanı için iç yük dengeli küme](./media/load-balancer-internal-getstarted/IC736321.png)

<span data-ttu-id="ac22e-144">Yapılandırma şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="ac22e-144">The configuration consists of the following:</span></span>

* <span data-ttu-id="ac22e-145">Sanal makineleri barındıran mevcut bulut hizmeti mytestcloud olarak adlandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="ac22e-145">The existing cloud service hosting the virtual machines is named mytestcloud.</span></span>
* <span data-ttu-id="ac22e-146">Mevcut iki veritabanı sunucusu DB1 ve DB2 olarak adlandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="ac22e-146">The two existing database servers are named DB1, DB2.</span></span>
* <span data-ttu-id="ac22e-147">Web katmanındaki web sunucuları, veritabanı katmanındaki veritabanı sunucularına özel IP adresini kullanarak bağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ac22e-147">Web servers in the web tier connect to the database servers in the database tier by using the private IP address.</span></span> <span data-ttu-id="ac22e-148">Diğer bir seçenek de sanal ağ için kendi DNS sunucunuzu kullanmak ve iç yük dengeleyici kümesi için A kaydı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="ac22e-148">Another option is to use your own DNS for the virtual network and manually register an A record for the internal load balancer set.</span></span>

<span data-ttu-id="ac22e-149">Aşağıdaki komutlar **ILBset** adlı yeni bir İç Yük Dengeleme örneği yapılandırır ve iki veritabanına karşılık gelen sanal makinelere uç noktalar ekler:</span><span class="sxs-lookup"><span data-stu-id="ac22e-149">The following commands configure a new Internal Load Balancing instance named **ILBset** and add endpoints to the virtual machines corresponding to the two database servers:</span></span>

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

## <a name="remove-an-internal-load-balancing-configuration"></a><span data-ttu-id="ac22e-150">İç Yük Dengeleme yapılandırmasını kaldırma</span><span class="sxs-lookup"><span data-stu-id="ac22e-150">Remove an Internal Load Balancing configuration</span></span>

<span data-ttu-id="ac22e-151">Bir sanal makineyi iç yük dengeleme örneğinin uç noktası olmaktan çıkarmak için şu komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="ac22e-151">To remove a virtual machine as an endpoint from an internal load balancer instance, use the following commands:</span></span>

```powershell
$svc="<Cloud service name>"
$vmname="<Name of the VM>"
$epname="<Name of the endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="ac22e-152">Bu komutları kullanmak için istenen değerleri yazıp < ve > işaretlerini silin.</span><span class="sxs-lookup"><span data-stu-id="ac22e-152">To use these commands, fill in the values, removing the < and >.</span></span>

<span data-ttu-id="ac22e-153">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ac22e-153">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="ac22e-154">Bir bulut hizmetindeki iç yük dengeleyici örneğini kaldırmak için şu komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="ac22e-154">To remove an internal load balancer instance from a cloud service, use the following commands:</span></span>

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

<span data-ttu-id="ac22e-155">Bu komutları kullanmak için istenen değerleri yazıp < ve > işaretlerini silin.</span><span class="sxs-lookup"><span data-stu-id="ac22e-155">To use these commands, fill in the value and remove the < and >.</span></span>

<span data-ttu-id="ac22e-156">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ac22e-156">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a><span data-ttu-id="ac22e-157">İç yük dengeleyici cmdlet'leri hakkında ek bilgi</span><span class="sxs-lookup"><span data-stu-id="ac22e-157">Additional information about internal load balancer cmdlets</span></span>

<span data-ttu-id="ac22e-158">İç Yük Dengeleyici cmdlet’leri hakkında ek bilgi almak için Windows PowerShell komut isteminde şu komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ac22e-158">To obtain additional information about Internal Load Balancing cmdlets, run the following commands at a Windows PowerShell prompt:</span></span>

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a><span data-ttu-id="ac22e-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ac22e-159">Next steps</span></span>

[<span data-ttu-id="ac22e-160">Kaynak IP benzeşimi kullanarak yük dengeleyici dağıtım modunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ac22e-160">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="ac22e-161">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ac22e-161">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

