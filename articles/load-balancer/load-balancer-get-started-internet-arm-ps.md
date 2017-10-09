---
title: "aaaCreate bir Azure Internet'e yönelik Yük Dengeleyici - PowerShell | Microsoft Docs"
description: "Nasıl toocreate bir Internet'e yönelik Yük Dengeleyici Kaynak Yöneticisi'nde PowerShell kullanarak bilgi edinin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e4e0e5271bc83c23fc62c0910e784c57d2b30065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started"></a>PowerShell kullanarak Resource Manager’da İnternet’e yönelik yük dengeleyici oluşturma

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Şablon](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır. Ayrıca [nasıl toocreate bir Internet'e yönelik Yük Dengeleyici hello Klasik dağıtım modelini kullanarak bilgi](load-balancer-get-started-internet-classic-cli.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-by-using-azure-powershell"></a>Azure PowerShell kullanarak Hello çözümü dağıtma

yordamları izleyerek hello nasıl toocreate bir Internet'e yönelik Yük Dengeleyici PowerShell ile Azure Kaynak Yöneticisi'ni kullanarak açıklanmaktadır. Azure Resource Manager ile her bir kaynak oluşturulur ve ayrı ayrı yapılandırılır ve toocreate bir yük dengeleyici bir araya getirin.

Oluşturma ve nesneleri toodeploy bir yük dengeleyici aşağıdaki hello yapılandırmanız gerekir:

* Ön uç IP yapılandırması: Gelen ağ trafiği için genel IP (PIP) adreslerini içerir.
* Arka uç adres havuzu: hello yük dengeleyici gelen hello sanal makineleri tooreceive ağ trafiği için ağ arabirimlerine (NIC'ler) içerir.
* Yük Dengeleme kuralları: hello arka uç adres havuzu hello yük dengeleyici tooa bağlantı noktası üzerinde genel bir bağlantı noktası eşleme kurallarını içerir.
* Gelen NAT kuralları: bağlantı noktasında hello yük dengeleyici tooa hello arka uç adres havuzundaki belirli bir sanal makine için genel bir bağlantı noktası eşleme kurallarını içerir.
* Sonda: sistem durumu kullanılan araştırmalar toocheck hello arka uç adres havuzu sanal makine örneklerinin kullanılabilirliğini içerir.

Daha fazla bilgi için bkz. [Yük Dengeleyici için Azure Resource Manager desteği](load-balancer-arm.md).

## <a name="set-up-powershell-toouse-resource-manager"></a>Resource Manager PowerShell toouse ayarlayın

Merhaba son üretim hello Azure Resource Manager modülü sürümü için PowerShell bulunduğundan emin olun:

1. TooAzure oturum açın.

    ```powershell
    Login-AzureRmAccount
    ```

    İstendiğinde kimlik bilgilerinizi girin.

2. Merhaba hesabının Hello abonelikleri kontrol edin.

    ```powershell
    Get-AzureRmSubscription
    ```

3. Azure abonelikleri toouse hangisinin seçin.

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. Bir kaynak grubu oluşturun. (Mevcut bir kaynak grubunu kullanıyorsanız bu adımı atlayın.)

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>Bir sanal ağ ve hello ön uç IP havuzu için bir ortak IP adresi oluştur

1. Alt ağ ve sanal ağ oluşturun.

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. Adlı bir Azure ortak IP adresi kaynağı oluşturma **Publicıp**, hello DNS adına sahip bir ön uç IP havuzu tarafından kullanılan toobe **loadbalancernrp.westus.cloudapp.azure.com**. komutu aşağıdaki hello hello kullanır statik ayırma türü.

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > Merhaba yük dengeleyicisi hello etki alanı etiketi hello ortak IP FQDN'sini için önek olarak kullanır. Bu yük dengeleyici FQDN hello gibi hello bulut hizmeti kullanan hello Klasik dağıtım modelinden, farklı değildir.
   > Bu örnekte, hello FQDN'sidir **loadbalancernrp.westus.cloudapp.azure.com**.

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a>Ön uç IP havuzu ve arka uç adres havuzu oluşturma

1. Adlı bir ön uç IP havuzu oluşturma **LB ön uç** hello kullanan **Publicıp** kaynak.

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. **LB-backend** adlı bir arka uç adres havuzu oluşturun.

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a>NAT kuralları, yük dengeleyici kuralı, araştırma ve yük dengeleyici oluşturma

Bu örnekte aşağıdaki öğelerindeki hello oluşturur:

* Tüm gelen trafiği üzerinde bağlantı noktası 3441 tooport 3389 NAT kuralı tootranslate
* Tüm gelen trafiği üzerinde bağlantı noktası 3442 tooport 3389 NAT kuralı tootranslate
* Bir araştırma kural toocheck hello sistem durumu adlı bir sayfada **HealthProbe.aspx**
* Bir yük dengeleyici kuralı toobalance hello üzerinde bağlantı noktası 80 tooport 80 tüm gelen trafiği hello arka uç havuzundaki adresleri
* Tüm bu nesneleri kullanan yük dengeleyici

Şu adımları uygulayın:

1. Merhaba NAT kuralları oluşturun.

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. Durum araştırması oluşturun. Bir araştırma iki yolu tooconfigure vardır:

    HTTP araştırma

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    TCP araştırma

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. Yük dengeleyici kuralı oluşturun.

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. Merhaba yük dengeleyici hello daha önce oluşturduğunuz nesneleri kullanarak oluşturursunuz.

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a>NIC’leri oluşturma

Ağ arabirimleri oluşturun (veya var olanları değiştirme) ve ardından bunları tooNAT kuralları, yük dengeleyici kuralları ve araştırmalar ilişkilendirin:

1. Merhaba sanal ağ ve bir sanal ağ alt hello NIC'ler oluşturulan toobe gereken yeri alın.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. Adlı bir NIC oluşturun **lb nıc1 olması**ve hello ilk NAT kuralında ve hello ilk (ve yalnızca) arka uç adres havuzu ile ilişkilendirin.

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. Adlı bir NIC oluşturun **lb nic2 olması**ve hello ikinci NAT kuralı ve hello ilk (ve yalnızca) arka uç adres havuzu ile ilişkilendirin.

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. Merhaba NIC'ler denetleyin.

        $backendnic1

    Beklenen çıktı:

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
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
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. Kullanım hello `Add-AzureRmVMNetworkInterface` cmdlet tooassign hello NIC'ler toodifferent VM'ler.

## <a name="create-a-virtual-machine"></a>Sanal makine oluşturma

Sanal makine oluşturma ve NIC atama talimatları için bkz. [PowerShell kullanarak Azure VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

## <a name="add-hello-network-interface-toohello-load-balancer"></a>Merhaba ağ arabirimi toohello yük dengeleyici ekleme

1. Merhaba yük dengeleyici Azure'dan alın.

    (Bunu, henüz yapmadıysanız) hello yük dengeleyici kaynak bir değişkene yükleyin. Merhaba değişkeni çağrılır **$lb**. Merhaba aynı daha önce oluşturduğunuz hello yük dengeleyici kaynaktan adları kullanın.

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. Yük hello arka uç yapılandırması tooa değişkeni.

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. Önceden oluşturulmuş hello ağ arabirimi bir değişkene yükleyin. Merhaba değişken adı **$nic**. Merhaba ağ arabirimi adı olduğu hello aynı hello önceki örnek.

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. Merhaba arka uç yapılandırması hello ağ arabiriminde değiştirin.

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. Merhaba ağ arabirimi nesnesi kaydedin.

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    Bir ağ arabirimi toohello yük dengeleyici arka uç havuzuna eklendikten sonra ağ trafiğini hello Yük Dengeleme kuralları bu yük dengeleyici kaynak için temel almayı başlatır.

## <a name="update-an-existing-load-balancer"></a>Mevcut yük dengeleyiciyi güncelleştirme

1. Yük Dengeleyici gelen Hello kullanarak hello önceki örnekte, bir yük dengeleyici nesne toohello değişkeni Ata **$slb** kullanarak `Get-AzureLoadBalancer`.

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. Aşağıdaki örnek hello, bağlantı noktası 81 hello ön uç havuzunda ve bağlantı noktası 8181 hello arka uç havuzu--tooan varolan yük dengeleyicisi kullanarak gelen NAT kuralı--ekleyin.

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. Kullanarak Hello yeni yapılandırmayı kaydedin `Set-AzureLoadBalancer`.

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a>Yük dengeleyici kaldırma

Hello komutunu `Remove-AzureLoadBalancer` toodelete adlı önceden oluşturulmuş yük dengeleyici **NRP LB** bir kaynak grubunda **NRP RG**.

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> Merhaba isteğe bağlı bir anahtar kullandığınız **-Force** tooavoid hello istemi silme işlemi için.

## <a name="next-steps"></a>Sonraki adımlar

[Bir iç yük dengeleyici yapılandırmaya başlayın](load-balancer-get-started-ilb-arm-ps.md)

[Yük dengeleyici dağıtım modu yapılandırma](load-balancer-distribution-mode.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)
