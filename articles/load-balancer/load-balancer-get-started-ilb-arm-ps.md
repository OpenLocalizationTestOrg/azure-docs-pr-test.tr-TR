---
title: "aaaCreate Azure iç yük dengeleyici - PowerShell | Microsoft Docs"
description: "Toocreate bir iç yük dengeleyici Kaynak Yöneticisi'nde PowerShell kullanarak nasıl öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 4b9657c77aa32a142de49ff7871ed6a396b22223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a>PowerShell kullanarak iç yük dengeleyici oluşturma

> [!div class="op_single_selector"]
> * [Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Şablon](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).  Bu makalede, kullanarak yer almaktadır hello yerine çoğu yeni dağıtımlar için Microsoft önerir hello Resource Manager dağıtım modeli [Klasik dağıtım modeli](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

Aşağıdaki adımları hello nasıl toocreate bir iç yük dengeleyici PowerShell ile Azure Resource Manager kullanarak açıklanmaktadır. Azure Resource Manager ile Merhaba öğeleri toocreate bir iç yük dengeleyici ayrı ayrı yapılandırılır ve toocreate bir yük dengeleyici bileşik.

Nesneleri toodeploy bir yük dengeleyici aşağıdaki hello yapılandırmak ve toocreate gerekir:

* Ön uç IP yapılandırması - hello özel IP adresi gelen ağ trafiği için yapılandırın
* Arka uç adres havuzu - ön uç IP havuzundan gelen hello yükü dengelenmiş trafiği alacak hello ağ arabirimleri yapılandıracağınız
* Yük Dengeleme kuralları - kaynak ve yerel bağlantı noktası yapılandırmasını hello için yük dengeleyici.
* Yoklamaları - hello sistem durum araştırması hello sanal makine örnekleri için yapılandırır.
* Gelen NAT kuralları - başlangıç bağlantı noktası kuralları toodirectly erişim hello sanal makine örneklerinden biri yapılandırır.

Azure Resource Manager içindeki yük dengeleyici bileşenleri hakkında daha fazla bilgi için bkz. [Azure Resource Manager yük dengeleyici desteği](load-balancer-arm.md).

Merhaba aşağıdaki adımlarda açıklanmaktadır nasıl tooconfigure iki sanal makineler arasında bir yük dengeleyici.

## <a name="setup-powershell-toouse-resource-manager"></a>PowerShell toouse Resource Manager Kurulumu

Hello en son ürün sürümüne hello Azure modülü için PowerShell sahip ve doğru şekilde, Azure aboneliğinizin tooaccess Kurulum PowerShell sahip olduğunuzdan emin olun.

### <a name="step-1"></a>1. Adım

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>2. Adım

Merhaba hesabının Hello abonelikleri kontrol edin

```powershell
Get-AzureRmSubscription
```

Kimlik bilgilerinizle istendiğinde tooAuthenticate olacaktır.

### <a name="step-3"></a>3. Adım

Azure abonelikleri toouse hangisinin seçin.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a>Yük dengeleyici için Kaynak Grubu oluşturma

Yeni bir kaynak grubu oluşturma (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın)

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir. Bu kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır. Bir yük dengeleyicinin kullanacağı toocreate aynı hello tüm komutları emin olun kaynak grubu.

Hello biz Yukarıdaki örnek "NRP-RG adlı" "Batı ABD" konumlu bir kaynak grubu oluşturduk.

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a>Ön uç IP havuzu için Sanal Ağ ve özel IP adresi oluşturma

Merhaba sanal ağ için bir alt ağ oluşturur ve toovariable $backendSubnet atar

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

Sanal ağ oluşturma:

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

Merhaba sanal ağ oluşturur ve hello alt lb alt olması toohello sanal ağ NRPVNet ekler ve toovariable $vnet atar

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a>Ön uç IP havuzu ve arka uç adres havuzu oluşturma

Merhaba gelen için bir ön uç IP havuzu ayarlama yük dengeleyici ağ trafiği ve arka uç adres havuzu tooreceive hello yükü dengelenmiş trafiği.

### <a name="step-1"></a>1. Adım

Merhaba gelen ağ trafiğini uç olacağı hello alt 10.0.2.0/24 için Hello özel IP adresi 10.0.2.5 kullanarak bir ön uç IP havuzu oluşturun.

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a>2. Adım

Bir arka uç adres havuzu ayarlama tooreceive gelen trafiği ön uç IP havuzundan kullanılır:

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a>LB kuralları, NAT kuralları, araştırma ve yük dengeleyici oluşturma

Merhaba ön uç IP havuzu ve hello arka uç adres havuzu oluşturduktan sonra toohello yük dengeleyici kaynak ait toocreate hello kuralları gerekir:

### <a name="step-1"></a>1. Adım

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

Yukarıdaki Hello örnek öğeleri aşağıdaki hello oluşturuluyor:

* Tüm gelen tooport 3441 trafiği NAT kuralı tooport 3389 geçer.
* tooport 3442 trafiği tüm gelen, ikinci bir NAT kuralı tooport 3389 geçer.
* yükleyecek bir yük dengeleyici kuralı genel bağlantı noktası 80 toolocal 80 numaralı bağlantı noktasında hello arka uç adres havuzundaki tüm gelen trafiği dengeler.
* Araştırma kuralı, bir yolu "HealthProbe.aspx" Merhaba sistem durumunu denetler

### <a name="step-2"></a>2. Adım

Merhaba yük dengeleyici (NAT kuralları, yük dengeleyici kuralları, araştırma yapılandırmaları) tüm nesnelerin araya ekleme oluşturun:

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a>Ağ arabirimlerini oluşturma

Merhaba iç yük dengeleyici oluşturduktan sonra hangi ağ arabirimleri hello gelen yük dengeli ağ trafiği NAT kuralları ve araştırma alacaksınız tanımlayın. Hello ağ arabirimi, bu durumda tek tek yapılandırılır ve tooa sanal makineyi daha sonra atanabilir.

### <a name="step-1"></a>1. Adım

Merhaba kaynak sanal ağ ve alt ağ toocreate ağ arabirimlerini Al:

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

Bu adım toohello yük dengeleyici arka uç havuzuna ait ve bu ağ arabirimi için RDP hello ilk NAT kuralında ilişkilendirmek bir ağ arabirimi oluşturur:

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a>2. Adım

LB-Nic2-BE adında ikinci bir ağ arabirimi oluşturma:

Bu adımı ikinci bir ağ arabirimi oluşturur, geri aynı yük dengeleyici havuzu sonlandırmak ve hello ikinci NAT kuralı ilişkilendirme için RDP oluşturulan toohello atama:

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

Merhaba sonuç hello şunları gösterir:

    $backendnic1

Beklenen çıktı:

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
                           "PublicIpAddress": {
                             "Id": null
                           },
                           "LoadBalancerBackendAddressPools": [
                             {
                               "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                             }
                           ],
                           "LoadBalancerInboundNatRules": [
                             {
                               "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                             }
                           ],
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3"></a>3. Adım

Merhaba komutu Ekle AzureRmVMNetworkInterface tooassign hello NIC tooa sanal makine kullanın.

Adım adım yönergeler toocreate bir sanal makine hello ve tooa NIC atayın bulabilir hello belgelerine aşağıdaki: [Azure PowerShell kullanarak bir VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

## <a name="add-hello-network-interface"></a>Merhaba ağ arabirimi ekleyin

Oluşturulan bir sanal makine zaten varsa, aşağıdaki adımları hello ile Merhaba ağ arabirimi ekleyebilirsiniz:

### <a name="step-1"></a>1. Adım

(Bunu, henüz yapmadıysanız) hello yük dengeleyici kaynak bir değişkene yükleyin. kullanılan hello çağrılan $lb ve kullanım hello hello yük dengeleyici kaynak aynı adlarından yukarıda oluşturduğunuz değişkenidir.

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a>2. Adım

Yük hello arka uç yapılandırması tooa değişkeni.

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a>3. Adım

Önceden oluşturulmuş hello ağ arabirimi bir değişkene yükleyin. kullanılan hello değişken $NIC adıdır kullanılan hello ağ arabirimi adı olduğu hello aynı örnek hello yukarıdaki.

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a>4. Adım

Merhaba arka uç yapılandırması hello ağ arabiriminde değiştirin.

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a>5. Adım

Merhaba ağ arabirimi nesnesi kaydedin.

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

Bir ağ arabirimi toohello yük dengeleyici arka uç havuzuna eklendikten sonra ağ trafiğini hello Yük Dengeleme kuralları bu yük dengeleyici kaynak için temel almayı başlatır.

## <a name="update-an-existing-load-balancer"></a>Mevcut yük dengeleyiciyi güncelleştirme

### <a name="step-1"></a>1. Adım
Yukarıdaki hello örneğindeki Hello yük dengeleyicinin kullanılması, yük dengeleyici nesne toovariable Get-AzureRmLoadBalancer kullanarak $slb atayın

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a>2. Adım

Merhaba, aşağıdaki örneğine, hello ön uç bağlantı noktası 81'i kullanarak yeni bir gelen NAT kuralı ekleyeceksiniz ve hello geri için bağlantı noktası 8181 bitiş havuzu tooan varolan yük dengeleyicisi

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a>3. Adım

Set-AzureLoadBalancer kullanarak hello yeni yapılandırmayı kaydedin

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a>Yük dengeleyici kaldırma

Merhaba komutu Kaldır AzureRmLoadBalancer toodelete "NRP-"NRP-RG"adlı LB" bir kaynak grubunda adlı önceden oluşturulmuş yük dengeleyici kullanın

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> İsteğe bağlı hello kullanabilirsiniz geçiş - Force tooavoid hello istemi silme işlemi için.

## <a name="next-steps"></a>Sonraki adımlar

[Yük dengeleyici dağıtım modu yapılandırma](load-balancer-distribution-mode.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)
