---
title: "bir bulut hizmeti için aaaMutiple VIP'ler"
description: "MultiVIP genel bakış ve nasıl tooset bir bulut hizmeti üzerinde birden çok Vip"
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
ms.openlocfilehash: b3e0f2b24968cb75a7064484a09ffe94505bb70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="3780a-103">Birden çok Vip bir bulut hizmeti için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3780a-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="3780a-104">Hello Azure tarafından sağlanan bir IP adresi kullanarak genel Internet üzerinden Azure bulut hizmetlerine erişebilir.</span><span class="sxs-lookup"><span data-stu-id="3780a-104">You can access Azure cloud services over hello public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="3780a-105">Bu genel IP adresi başvurulan tooas VIP (sanal IP) olan bağlı olduğu bu yana toohello Azure yük dengeleyici ve hello bulut hizmeti içindeki sanal makine (VM) örnekleri hello değil.</span><span class="sxs-lookup"><span data-stu-id="3780a-105">This public IP address is referred tooas a VIP (virtual IP) since it is linked toohello Azure load balancer, and not hello Virtual Machine (VM) instances within hello cloud service.</span></span> <span data-ttu-id="3780a-106">Bir bulut hizmeti içinde herhangi bir VM örneğine tek bir VIP kullanarak erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3780a-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="3780a-107">Ancak, hangi ihtiyacınız olabilecek birden çok VIP senaryolar vardır bir giriş noktası toohello aynı bulut hizmeti.</span><span class="sxs-lookup"><span data-stu-id="3780a-107">However, there are scenarios in which you may need more than one VIP as an entry point toohello same cloud service.</span></span> <span data-ttu-id="3780a-108">Örneğin, bulut hizmetinizin her site için farklı bir müşteri barındırılan olarak hello varsayılan bağlantı noktası 443'ü kullanarak SSL bağlantısı gerektiren veya Kiracı birden çok Web sitesi barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="3780a-108">For instance, your cloud service may host multiple websites that require SSL connectivity using hello default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="3780a-109">Bu senaryoda, her Web sitesi için toohave farklı genel kullanıma yönelik bir IP adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3780a-109">In this scenario, you need toohave a different public facing IP address for each website.</span></span> <span data-ttu-id="3780a-110">Merhaba diyagramda hello üzerinde aynı birden çok SSL sertifikaları için bir tipik çok kiracılı web ile gerek duyduğu barındırma gösterilmiştir genel bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="3780a-110">hello diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on hello same public port.</span></span>

![Çoklu VIP SSL senaryosu](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="3780a-112">Yukarıdaki tüm VIP'ler kullanım hello hello örnekte aynı genel bağlantı noktası (443) ve trafiği yeniden yönlendirilen tooone ya da daha fazla yük dengeli sanal makinelerin hello iç IP adresi hello bulut hizmetinin tüm hello Web siteleri barındırmak için bir benzersiz özel bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="3780a-112">In hello example above, all VIPs use hello same public port (443) and traffic is redirected tooone or more load balanced VMs on a unique private port for hello internal IP address of hello cloud service hosting all hello websites.</span></span>

> [!NOTE]
> <span data-ttu-id="3780a-113">Başka bir durum gerektiren hello kullan hello birden çok Vip barındırma hello aynı sanal makinelerin kümesi üzerinde birden çok SQL AlwaysOn Kullanılabilirlik grubu dinleyicileri.</span><span class="sxs-lookup"><span data-stu-id="3780a-113">Another situation requiring hello use hello multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on hello same set of Virtual Machines.</span></span>

<span data-ttu-id="3780a-114">VIP'ler dinamik varsayılan toohello bulut hizmeti atanan hello gerçek IP adresi zaman içinde değişebilir anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3780a-114">VIPs are dynamic by default, which means that hello actual IP address assigned toohello cloud service may change over time.</span></span> <span data-ttu-id="3780a-115">oluşmasını, bir VIP hizmetiniz için ayırabilirsiniz olduğunu tooprevent.</span><span class="sxs-lookup"><span data-stu-id="3780a-115">tooprevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="3780a-116">toolearn ayrılmış VIP'ler hakkında daha fazla bilgi görmek [ayrılmış genel IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="3780a-116">toolearn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3780a-117">Lütfen bakın [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses/) üzerinde VIP'ler fiyatlandırma ve ayrılmış IP hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="3780a-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="3780a-118">PowerShell tooverify Merhaba, bulut Hizmetleri tarafından kullanılan VIP'ler kullanın yanı sıra ekleyin ve VIP'ler kaldırmak, bir VIP tooan uç noktası ilişkilendirmek ve Yük Dengeleme özgü bir VIP yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3780a-118">You can use PowerShell tooverify hello VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP tooan endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="3780a-119">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="3780a-119">Limitations</span></span>

<span data-ttu-id="3780a-120">Şu anda çoklu VIP senaryoları aşağıdaki sınırlı toohello işlevdir:</span><span class="sxs-lookup"><span data-stu-id="3780a-120">At this time, Multi VIP functionality is limited toohello following scenarios:</span></span>

* <span data-ttu-id="3780a-121">**Iaas yalnızca**.</span><span class="sxs-lookup"><span data-stu-id="3780a-121">**IaaS only**.</span></span> <span data-ttu-id="3780a-122">Bu gibi durumlarda, çoklu VIP yalnızca VM içermesi için bulut hizmetlerini etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3780a-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="3780a-123">Çoklu VIP PaaS rol örnekleri senaryolarla kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="3780a-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="3780a-124">**Yalnızca PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="3780a-124">**PowerShell only**.</span></span> <span data-ttu-id="3780a-125">PowerShell kullanarak yalnızca çoklu VIP yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3780a-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="3780a-126">Bu sınırlamaların geçicidir ve herhangi bir zamanda değişebilir.</span><span class="sxs-lookup"><span data-stu-id="3780a-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="3780a-127">Emin toorevisit bu sayfa tooverify gelecekteki değişiklikler yapın.</span><span class="sxs-lookup"><span data-stu-id="3780a-127">Make sure toorevisit this page tooverify future changes.</span></span>

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a><span data-ttu-id="3780a-128">Nasıl tooadd bir VIP tooa bulut hizmeti</span><span class="sxs-lookup"><span data-stu-id="3780a-128">How tooadd a VIP tooa cloud service</span></span>
<span data-ttu-id="3780a-129">tooadd bir VIP tooyour hizmeti, hello aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3780a-129">tooadd a VIP tooyour service, run hello following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="3780a-130">Bu komut, aşağıdaki örnek bir sonuç benzer toohello görüntüler:</span><span class="sxs-lookup"><span data-stu-id="3780a-130">This command displays a result similar toohello following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a><span data-ttu-id="3780a-131">Nasıl bir bulut hizmetinden bir VIP tooremove</span><span class="sxs-lookup"><span data-stu-id="3780a-131">How tooremove a VIP from a cloud service</span></span>
<span data-ttu-id="3780a-132">tooremove hello VIP tooyour hizmeti üzerinde aşağıdaki PowerShell komutunu çalıştırma hello hello örnekte ekledi:</span><span class="sxs-lookup"><span data-stu-id="3780a-132">tooremove hello VIP added tooyour service in hello example above, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="3780a-133">Hiçbir ilişkili uç noktaları tooit varsa, yalnızca bir VIP kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3780a-133">You can only remove a VIP if it has no endpoints associated tooit.</span></span>


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="3780a-134">Nasıl bir bulut hizmeti tooretrieve VIP bilgileri</span><span class="sxs-lookup"><span data-stu-id="3780a-134">How tooretrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="3780a-135">tooretrieve hello VIP'ler PowerShell Betiği aşağıdaki hello çalıştırmak bir bulut hizmetiyle ilişkili:</span><span class="sxs-lookup"><span data-stu-id="3780a-135">tooretrieve hello VIPs associated with a cloud service, run hello following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="3780a-136">Aşağıdaki örnek bir sonuç benzer toohello Hello betik görüntüler:</span><span class="sxs-lookup"><span data-stu-id="3780a-136">hello script displays a result similar toohello following sample:</span></span>

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

<span data-ttu-id="3780a-137">Bu örnekte, 3 hello bulut hizmeti olan VIP'ler:</span><span class="sxs-lookup"><span data-stu-id="3780a-137">In this example, hello cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="3780a-138">**Vıp1** olan varsayılan VIP Merhaba, IsDnsProgrammedName hello değeri tootrue ayarlandığından, biliyor.</span><span class="sxs-lookup"><span data-stu-id="3780a-138">**Vip1** is hello default VIP, you know that because hello value for IsDnsProgrammedName is set tootrue.</span></span>
* <span data-ttu-id="3780a-139">**Vıp2** ve **Vip3** herhangi bir IP adresi yok olarak kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="3780a-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="3780a-140">Bir uç nokta toohello VIP ilişkilendirirseniz yalnızca kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3780a-140">They will only be used if you associate an endpoint toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="3780a-141">Bir uç nokta ile ilişkili olduğunda, aboneliğiniz için ek VIP'ler yalnızca ücretlendirilir.</span><span class="sxs-lookup"><span data-stu-id="3780a-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="3780a-142">Fiyatlandırma hakkında daha fazla bilgi için bkz: [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="3780a-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a><span data-ttu-id="3780a-143">Nasıl tooassociate bir VIP tooan uç noktası</span><span class="sxs-lookup"><span data-stu-id="3780a-143">How tooassociate a VIP tooan endpoint</span></span>

<span data-ttu-id="3780a-144">PowerShell komutunu aşağıdaki hello çalıştırmak bir bulut hizmeti tooan uç noktasında bir VIP tooassociate:</span><span class="sxs-lookup"><span data-stu-id="3780a-144">tooassociate a VIP on a cloud service tooan endpoint, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="3780a-145">Merhaba komut oluşturur bağlantılı toohello VIP adlı bir uç nokta *vıp2* bağlantı noktasında *80*ve toohello adlı VM bağlantılar *myVM1* bir bulut hizmetinde adlı  *myService* kullanarak *TCP* bağlantı noktasında *8080*.</span><span class="sxs-lookup"><span data-stu-id="3780a-145">hello command creates an endpoint linked toohello VIP called *Vip2* on port *80*, and links it toohello VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="3780a-146">tooverify hello yapılandırması, hello aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3780a-146">tooverify hello configuration, run hello following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="3780a-147">Hello çıkış benzer toohello örnek aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="3780a-147">hello output looks similar toohello following example:</span></span>

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

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="3780a-148">Tooenable nasıl Yük Dengeleme özgü bir VIP</span><span class="sxs-lookup"><span data-stu-id="3780a-148">How tooenable load balancing on a specific VIP</span></span>

<span data-ttu-id="3780a-149">Yük Dengeleyici amaçları için birden çok sanal makine tek bir VIP ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3780a-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="3780a-150">Örneğin, adlandırılmış bir bulut hizmetine sahip *myService*ve adlı iki sanal makine *myVM1* ve *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="3780a-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="3780a-151">Ve bunların adlı birden çok Vip bulut hizmetiniz sahip *vıp2*.</span><span class="sxs-lookup"><span data-stu-id="3780a-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="3780a-152">Tüm tooport trafiği tooensure istiyorsanız *81* üzerinde *vıp2* arasında dengeli *myVM1* ve *myVM2* bağlantı noktasında *8181* çalıştırın hello aşağıdaki PowerShell komut dosyası:</span><span class="sxs-lookup"><span data-stu-id="3780a-152">If you want tooensure that all traffic tooport *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run hello following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="3780a-153">Ayrıca, yük dengeleyici toouse farklı bir VIP güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3780a-153">You can also update your load balancer toouse a different VIP.</span></span> <span data-ttu-id="3780a-154">Örneğin, hello aşağıdaki PowerShell komutu çalıştırırsanız, hello Yük Dengeleme kümesi toouse vıp1 adlı bir VIP değişir:</span><span class="sxs-lookup"><span data-stu-id="3780a-154">For example, if you run hello PowerShell command below, you will change hello load balancing set toouse a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="3780a-155">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="3780a-155">Next Steps</span></span>

[<span data-ttu-id="3780a-156">Azure Yük Dengeleme için günlük analizi</span><span class="sxs-lookup"><span data-stu-id="3780a-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="3780a-157">Internet kullanıma yönelik Yük Dengeleyici genel bakış</span><span class="sxs-lookup"><span data-stu-id="3780a-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="3780a-158">Yük Dengeleyici Internet'e üzerinde çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="3780a-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="3780a-159">Sanal ağ genel bakış</span><span class="sxs-lookup"><span data-stu-id="3780a-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="3780a-160">Ayrılmış IP REST API'leri</span><span class="sxs-lookup"><span data-stu-id="3780a-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
