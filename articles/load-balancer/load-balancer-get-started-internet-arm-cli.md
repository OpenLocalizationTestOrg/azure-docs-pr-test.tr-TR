---
title: "Azure CLI aaaCreate bir Internet'e yönelik Yük Dengeleyici - | Microsoft Docs"
description: "Nasıl toocreate Kaynak Yöneticisi'ni kullanarak bir Internet'e yönelik Yük Dengeleyici hello Azure CLI öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: cadb5edb3b4a4e2f0813109d027eaafdc7ef7303
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-load-balancer-using-hello-azure-cli"></a>İnternet'Hello Azure CLI kullanarak bir yük dengeleyici oluşturma

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Şablon](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır. Ayrıca [nasıl toocreate Internet'e yönelik Yük Dengeleyici Klasik dağıtım kullanarak bilgi edinin](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>Hello Azure CLI kullanarak hello çözümü dağıtma

Aşağıdaki adımları hello nasıl toocreate Internet'e yönelik Yük Dengeleyici CLI ile Azure Resource Manager kullanarak gösterir. Azure Resource her bir kaynak oluşturulur ve ayrı ayrı yapılandırılır Manager ile birlikte toocreate kaynak sonra yerleştirin.

Oluşturma ve nesneleri toodeploy bir yük dengeleyici aşağıdaki hello yapılandırmanız gerekir:

* Ön uç IP yapılandırması: Gelen ağ trafiği için genel IP adreslerini içerir.
* Arka uç adres havuzu - hello yük dengeleyici gelen hello sanal makineleri tooreceive ağ trafiği için ağ arabirimlerine (NIC'ler) içerir.
* Yük Dengeleme kuralları - hello yük dengeleyici tooport hello arka uç adres havuzundaki ortak bir bağlantı noktası eşleme kurallarını içerir.
* Gelen NAT kuralları - noktasında hello yük dengeleyici tooa hello arka uç adres havuzundaki belirli bir sanal makine için genel bir bağlantı noktası eşleme kurallarını içerir.
* Yoklamaları - sistem durumu kullanılan araştırmalar toocheck kullanılabilirliği hello arka uç adres havuzundaki sanal makineler örnekleri içerir.

Daha fazla bilgi için bkz. [Yük Dengeleyici için Azure Resource Manager desteği](load-balancer-arm.md).

## <a name="set-up-cli-toouse-resource-manager"></a>CLI toouse Kaynak Yöneticisi'ni ayarlayın

1. Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.
2. Merhaba çalıştırmak **azure config modu** aşağıda gösterildiği gibi komut tooswitch tooResource Yöneticisi modu.

    ```azurecli
        azure config mode arm
    ```

    Beklenen çıktı:

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>Bir sanal ağ ve hello ön uç IP havuzu için bir ortak IP adresi oluştur

1. Adlı bir sanal ağ (VNet) oluşturma *NRPVnet* hello Doğu ABD konumunda bir kaynak grubu kullanarak adlı *NRPRG*.

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    *NRPVnet* içinde *NRPVnetSubnet* adına ve 10.0.0.0/24 CIDR bloğuna sahip bir alt ağ oluşturun.

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. Adlı bir ortak IP adresi oluşturma *NRPPublicIP* DNS adına sahip bir ön uç IP havuzu tarafından kullanılan toobe *loadbalancernrp.eastus.cloudapp.azure.com*. aşağıdaki hello komutu hello statik ayırma türü kullanır ve 4 dakika boşta kalma zaman aşımı.

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > Merhaba yük dengeleyici hello etki alanı etiketi hello ortak IP FQDN'sini kullanır. Bu yük dengeleyici tam etki alanı adı (FQDN) hello gibi hello bulut hizmeti kullanan Klasik dağıtım değişiklik.
   > Bu örnekte, hello FQDN'sidir *loadbalancernrp.eastus.cloudapp.azure.com*.

## <a name="create-a-load-balancer"></a>Yük dengeleyici oluşturma

Merhaba aşağıdaki komutu adlı bir yük dengeleyici oluşturur *NRPlb* hello içinde *NRPRG* hello kaynak grubunda *Doğu ABD* Azure konumu.

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a>Ön uç IP havuzu ve arka uç adres havuzu oluşturma
Bu örnek nasıl hello hello gelen ağ trafiğini alan toocreate hello ön uç IP havuzu yük dengeleyici ve arka uç IP havuzu burada hello ön uç havuzu hello yük dengeli ağ trafiği gönderir hello gösterir.

1. Merhaba genel IP Hello önceki adımı ve hello yük dengeleyici oluşturulan ilişkilendirme bir ön uç IP havuzu oluşturun.

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. Bir arka uç adres havuzu ayarlama tooreceive gelen trafiği hello ön uç IP havuzundan kullanılır.

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a>LB kurallarını, NAT kurallarını ve araştırmayı oluşturma

Bu örnekte aşağıdaki öğelerindeki hello oluşturur.

* NAT kuralı tootranslate bağlantı noktası 21 tooport 22 tüm gelen trafiği<sup>1</sup>
* NAT kuralı tootranslate bağlantı noktası 23 tooport 22 tüm gelen trafiği
* bir yük dengeleyici kuralı toobalance hello arka uç havuzundaki tüm gelen trafiği hello üzerinde bağlantı noktası 80 tooport 80 giderir.
* bir araştırma kural toocheck hello sistem durumu adlı bir sayfada *HealthProbe.aspx*.

<sup>1</sup> NAT kurallardır hello yük dengeleyicinin arkasındaki ilişkili tooa belirli bir sanal makine örneği. 21 bağlantı noktasına ulaşan hello ağ trafiği, bağlantı noktası 22 Bu NAT kuralı ile ilişkili tooa belirli bir sanal makine gönderilir. NAT kuralı için bir protokol (UDP veya TCP) belirtmeniz gerekir. Her iki protokole olamaz toohello aynı bağlantı noktasını atanmış.

1. Merhaba NAT kuralları oluşturun.

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. Yük dengeleyici kuralı oluşturun.

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. Durum araştırması oluşturun.

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. Ayarlarınızı denetleyin.

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    Beklenen çıktı:

        info:    Executing command network lb show
        + Looking up hello load balancer "nrplb"
        + Looking up hello public ip "NRPPublicIP"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb
        data:    Name                            : nrplb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : eastus
        data:    Provisioning State              : Succeeded
        data:    Frontend IP configurations:
        data:      Name                          : NRPfrontendpool
        data:      Provisioning state            : Succeeded
        data:      Public IP address id          : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/publicIPAddresses/NRPPublicIP
        data:      Public IP allocation method   : Static
        data:      Public IP address             : 40.114.13.145
        data:
        data:    Backend address pools:
        data:      Name                          : NRPbackendpool
        data:      Provisioning state            : Succeeded
        data:
        data:    Load balancing rules:
        data:      Name                          : HTTP
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 80
        data:      Backend port                  : 80
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:      Backend address pool          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:
        data:    Inbound NAT rules:
        data:      Name                          : ssh1
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 21
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:      Name                          : ssh2
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 23
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:    Probes:
        data:      Name                          : healthprobe
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Http
        data:      Port                          : 80
        data:      Interval in seconds           : 15
        data:      Number of probes              : 4
        data:
        info:    network lb show command OK

## <a name="create-nics"></a>NIC’leri oluşturma

Toocreate NIC gerekir (veya var olanları değiştirme) ve tooNAT kuralları, yük dengeleyici kuralları ve araştırmalar ilişkilendirebilirsiniz.

1. Adlı bir NIC oluşturun *lb nıc1 olması*ve hello ile ilişkilendirmek *rdp1* NAT kuralı ve hello *NRPbackendpool* arka uç adres havuzu.

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    Beklenen çıktı:

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. Adlı bir NIC oluşturun *lb nic2 olması*ve hello ile ilişkilendirmek *rdp2* NAT kuralı ve hello *NRPbackendpool* arka uç adres havuzu.

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. Adlı sanal makine (VM) oluşturma *web1*ve hello adlı NIC ile ilişkilendirme *lb nıc1 olması*. Bir depolama hesabı olarak adlandırılan *web1nrp* aşağıdaki hello komutu çalıştırmadan önce oluşturuldu.

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > Bir yük dengeleyici gerek toobe içinde Vm'lerde aynı kullanılabilirlik kümesinde hello. Kullanım `azure availset create` toocreate kullanılabilirlik kümesi.

    Merhaba çıkış benzer toohello aşağıdaki gibi olmalıdır:

        info:    Executing command vm create
        + Looking up hello VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account web1nrp
        + Looking up hello availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up hello NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in hello NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > Merhaba iletidir **yapılandırılmış Publicıp olmadan bir NIC budur** hello NIC oluşturulan hello yük dengeleyici genel IP adresi kullanarak tooInternet bağlanma hello yük dengeleyici için bu yana beklenir.

    Merhaba itibaren *lb nıc1 olması* NIC hello ile ilişkili *rdp1* NAT kuralı, çok bağlanabilir*web1* 3441 hello yük dengeleyicideki bağlantı noktası üzerinden RDP kullanarak.

4. Adlı sanal makine (VM) oluşturma *web2*ve hello adlı NIC ile ilişkilendirme *lb nic2 olması*. Bir depolama hesabı olarak adlandırılan *web1nrp* aşağıdaki hello komutu çalıştırmadan önce oluşturuldu.

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a>Mevcut yük dengeleyiciyi güncelleştirme
Var olan bir yük dengeleyiciye başvuran kurallar ekleyebilirsiniz. Merhaba sonraki örnekte yeni bir yük dengeleyici kuralı tooan varolan yük dengeleyicisi eklenir **NRPlb**

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a>Yük dengeleyici silme
Komut tooremove bir yük dengeleyici aşağıdaki hello kullan:

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a>Sonraki adımlar
[Bir iç yük dengeleyici yapılandırmaya başlayın](load-balancer-get-started-ilb-arm-cli.md)

[Yük dengeleyici dağıtım modu yapılandırma](load-balancer-distribution-mode.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)
