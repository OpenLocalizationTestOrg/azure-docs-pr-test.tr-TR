---
title: "Bir bulut hizmeti için birden çok VIP'ler"
description: "MultiVIP ve bir bulut hizmetinde birden çok Vip ayarlama genel bakış"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 85f6d26a-3df5-4b8e-96a1-92b2793b5284
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: f40e0501eed8d5f296e7c79d8a35705a695ae6fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="c3d50-103">Birden çok Vip bir bulut hizmeti için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c3d50-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="c3d50-104">Azure tarafından sağlanan bir IP adresi kullanarak genel Internet üzerinden Azure bulut hizmetlerine erişebilir.</span><span class="sxs-lookup"><span data-stu-id="c3d50-104">You can access Azure cloud services over the public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="c3d50-105">Bu genel IP adresi VIP (sanal IP) adlandırılır Azure yük dengeleyiciye bağlı ve sanal makine (VM) bulut hizmetinde örnekleri.</span><span class="sxs-lookup"><span data-stu-id="c3d50-105">This public IP address is referred to as a VIP (virtual IP) since it is linked to the Azure load balancer, and not the Virtual Machine (VM) instances within the cloud service.</span></span> <span data-ttu-id="c3d50-106">Bir bulut hizmeti içinde herhangi bir VM örneğine tek bir VIP kullanarak erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3d50-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="c3d50-107">Ancak, bir veya daha çok VIP olarak bir giriş noktası aynı bulut hizmetine gerekebilir senaryo vardır.</span><span class="sxs-lookup"><span data-stu-id="c3d50-107">However, there are scenarios in which you may need more than one VIP as an entry point to the same cloud service.</span></span> <span data-ttu-id="c3d50-108">Örneğin, bulut hizmetinizin her site için farklı bir müşteri barındırılan olarak varsayılan bağlantı noktası 443'ü kullanarak SSL bağlantısı gerektiren veya Kiracı birden çok Web sitesi barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="c3d50-108">For instance, your cloud service may host multiple websites that require SSL connectivity using the default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="c3d50-109">Bu senaryoda, farklı genel kullanıma yönelik bir IP adresi her Web sitesi için olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3d50-109">In this scenario, you need to have a different public facing IP address for each website.</span></span> <span data-ttu-id="c3d50-110">Aşağıdaki diyagram tipik bir çok kiracılı web birden çok SSL sertifikaları aynı ortak bağlantı noktasına sahip barındırma gösterir.</span><span class="sxs-lookup"><span data-stu-id="c3d50-110">The diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on the same public port.</span></span>

![Çoklu VIP SSL senaryosu](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="c3d50-112">Yukarıdaki örnekte, tüm VIP'ler aynı genel bağlantı noktası (443) kullanın ve trafik birine yönlendirilir veya daha fazla yük dengeli sanal makinelerin tüm Web siteleri barındırma bulut hizmetinin iç IP adresi için bir benzersiz özel bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c3d50-112">In the example above, all VIPs use the same public port (443) and traffic is redirected to one or more load balanced VMs on a unique private port for the internal IP address of the cloud service hosting all the websites.</span></span>

> [!NOTE]
> <span data-ttu-id="c3d50-113">Birden çok Vip kullanımı gerektiren başka bir durum aynı sanal makineler kümesi üzerinde birden çok SQL AlwaysOn Kullanılabilirlik grubu dinleyicileri barındırıyor.</span><span class="sxs-lookup"><span data-stu-id="c3d50-113">Another situation requiring the use the multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on the same set of Virtual Machines.</span></span>

<span data-ttu-id="c3d50-114">VIP'ler dinamik varsayılan olarak bulut hizmetine atanan gerçek IP adresi zaman içinde değişebilir anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c3d50-114">VIPs are dynamic by default, which means that the actual IP address assigned to the cloud service may change over time.</span></span> <span data-ttu-id="c3d50-115">Oluşmasını önlemek için hizmetiniz için bir VIP ayırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3d50-115">To prevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="c3d50-116">Ayrılmış VIP'ler hakkında daha fazla bilgi için bkz: [ayrılmış genel IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="c3d50-116">To learn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c3d50-117">Lütfen bakın [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses/) üzerinde VIP'ler fiyatlandırma ve ayrılmış IP hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="c3d50-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="c3d50-118">Bulut hizmetlerinizi tarafından kullanılan VIP'ler doğrulamak için PowerShell kullanın yanı sıra ekleyin ve VIP'ler kaldırmak, bir uç nokta için bir VIP ilişkilendirmek ve Yük Dengeleme özgü bir VIP yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c3d50-118">You can use PowerShell to verify the VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP to an endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="c3d50-119">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="c3d50-119">Limitations</span></span>

<span data-ttu-id="c3d50-120">Şu anda aşağıdaki senaryolar için çoklu VIP işlevselliği sınırlıdır:</span><span class="sxs-lookup"><span data-stu-id="c3d50-120">At this time, Multi VIP functionality is limited to the following scenarios:</span></span>

* <span data-ttu-id="c3d50-121">**Iaas yalnızca**.</span><span class="sxs-lookup"><span data-stu-id="c3d50-121">**IaaS only**.</span></span> <span data-ttu-id="c3d50-122">Bu gibi durumlarda, çoklu VIP yalnızca VM içermesi için bulut hizmetlerini etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3d50-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="c3d50-123">Çoklu VIP PaaS rol örnekleri senaryolarla kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="c3d50-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="c3d50-124">**Yalnızca PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c3d50-124">**PowerShell only**.</span></span> <span data-ttu-id="c3d50-125">PowerShell kullanarak yalnızca çoklu VIP yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3d50-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="c3d50-126">Bu sınırlamaların geçicidir ve herhangi bir zamanda değişebilir.</span><span class="sxs-lookup"><span data-stu-id="c3d50-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="c3d50-127">Gelecekteki değişiklikleri doğrulamak için bu sayfayı yeniden ziyaret etmeniz emin olun.</span><span class="sxs-lookup"><span data-stu-id="c3d50-127">Make sure to revisit this page to verify future changes.</span></span>

## <a name="how-to-add-a-vip-to-a-cloud-service"></a><span data-ttu-id="c3d50-128">Bir bulut hizmeti için bir VIP ekleme</span><span class="sxs-lookup"><span data-stu-id="c3d50-128">How to add a VIP to a cloud service</span></span>
<span data-ttu-id="c3d50-129">Bir VIP hizmetinize eklemek için aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c3d50-129">To add a VIP to your service, run the following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="c3d50-130">Bu komut, aşağıdaki örneğe benzer bir sonuç görüntüler:</span><span class="sxs-lookup"><span data-stu-id="c3d50-130">This command displays a result similar to the following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-to-remove-a-vip-from-a-cloud-service"></a><span data-ttu-id="c3d50-131">Bir bulut hizmetinden bir VIP kaldırma</span><span class="sxs-lookup"><span data-stu-id="c3d50-131">How to remove a VIP from a cloud service</span></span>
<span data-ttu-id="c3d50-132">Yukarıdaki örnekte hizmetinizi eklenen VIP kaldırmak için aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c3d50-132">To remove the VIP added to your service in the example above, run the following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="c3d50-133">Kendisine ilişkili hiçbir uç noktası varsa, yalnızca bir VIP kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3d50-133">You can only remove a VIP if it has no endpoints associated to it.</span></span>


## <a name="how-to-retrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="c3d50-134">Bir bulut hizmetinden VIP bilgi alma</span><span class="sxs-lookup"><span data-stu-id="c3d50-134">How to retrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="c3d50-135">Bir bulut hizmetiyle ilişkili VIP'ler almak için aşağıdaki PowerShell betiğini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c3d50-135">To retrieve the VIPs associated with a cloud service, run the following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="c3d50-136">Komut dosyasını aşağıdaki örneğe benzer bir sonuç görüntüler:</span><span class="sxs-lookup"><span data-stu-id="c3d50-136">The script displays a result similar to the following sample:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

<span data-ttu-id="c3d50-137">Bu örnekte, bulut hizmeti 3 olan VIP'ler:</span><span class="sxs-lookup"><span data-stu-id="c3d50-137">In this example, the cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="c3d50-138">**Vıp1** varsayılan VIP olup, bildiğiniz IsDnsProgrammedName değeri ayarlanamıyor çünkü true.</span><span class="sxs-lookup"><span data-stu-id="c3d50-138">**Vip1** is the default VIP, you know that because the value for IsDnsProgrammedName is set to true.</span></span>
* <span data-ttu-id="c3d50-139">**Vıp2** ve **Vip3** herhangi bir IP adresi yok olarak kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="c3d50-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="c3d50-140">VIP için bir uç nokta ilişkilendirirseniz yalnızca kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c3d50-140">They will only be used if you associate an endpoint to the VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="c3d50-141">Bir uç nokta ile ilişkili olduğunda, aboneliğiniz için ek VIP'ler yalnızca ücretlendirilir.</span><span class="sxs-lookup"><span data-stu-id="c3d50-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="c3d50-142">Fiyatlandırma hakkında daha fazla bilgi için bkz: [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="c3d50-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-to-associate-a-vip-to-an-endpoint"></a><span data-ttu-id="c3d50-143">Bir uç nokta için bir VIP ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="c3d50-143">How to associate a VIP to an endpoint</span></span>

<span data-ttu-id="c3d50-144">Bir bulut hizmeti için bir bitiş noktasına bir VIP ilişkilendirmek için aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c3d50-144">To associate a VIP on a cloud service to an endpoint, run the following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="c3d50-145">Komutu adlı VIP bağlı bir uç nokta oluşturuyor *vıp2* bağlantı noktasında *80*ve adlı VM'ye bağlantılar *myVM1* bir bulut hizmetinde adlı *myService* kullanarak *TCP* bağlantı noktasında *8080*.</span><span class="sxs-lookup"><span data-stu-id="c3d50-145">The command creates an endpoint linked to the VIP called *Vip2* on port *80*, and links it to the VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="c3d50-146">Yapılandırmayı doğrulamak için aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c3d50-146">To verify the configuration, run the following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="c3d50-147">Çıktı aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="c3d50-147">The output looks similar to the following example:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         : 191.238.74.13
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

## <a name="how-to-enable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="c3d50-148">Yük Dengeleme özgü bir VIP etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c3d50-148">How to enable load balancing on a specific VIP</span></span>

<span data-ttu-id="c3d50-149">Yük Dengeleyici amaçları için birden çok sanal makine tek bir VIP ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3d50-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="c3d50-150">Örneğin, adlandırılmış bir bulut hizmetine sahip *myService*ve adlı iki sanal makine *myVM1* ve *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="c3d50-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="c3d50-151">Ve bunların adlı birden çok Vip bulut hizmetiniz sahip *vıp2*.</span><span class="sxs-lookup"><span data-stu-id="c3d50-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="c3d50-152">Tüm bağlantı noktasına trafiği emin olmak istiyorsanız *81* üzerinde *vıp2* arasında dengeli *myVM1* ve *myVM2* bağlantı noktasında *8181* , aşağıdaki PowerShell betiğini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c3d50-152">If you want to ensure that all traffic to port *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run the following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="c3d50-153">Ayrıca, farklı bir VIP kullanmak için yük dengeleyici güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3d50-153">You can also update your load balancer to use a different VIP.</span></span> <span data-ttu-id="c3d50-154">Örneğin, aşağıdaki PowerShell komutu çalıştırırsanız, Yük Dengeleme vıp1 adlı bir VIP kullanılacak kümesi değişir:</span><span class="sxs-lookup"><span data-stu-id="c3d50-154">For example, if you run the PowerShell command below, you will change the load balancing set to use a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="c3d50-155">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="c3d50-155">Next Steps</span></span>

[<span data-ttu-id="c3d50-156">Azure Yük Dengeleme için günlük analizi</span><span class="sxs-lookup"><span data-stu-id="c3d50-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="c3d50-157">Internet kullanıma yönelik Yük Dengeleyici genel bakış</span><span class="sxs-lookup"><span data-stu-id="c3d50-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="c3d50-158">Yük Dengeleyici Internet'e üzerinde çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c3d50-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="c3d50-159">Sanal ağ genel bakış</span><span class="sxs-lookup"><span data-stu-id="c3d50-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="c3d50-160">Ayrılmış IP REST API'leri</span><span class="sxs-lookup"><span data-stu-id="c3d50-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
