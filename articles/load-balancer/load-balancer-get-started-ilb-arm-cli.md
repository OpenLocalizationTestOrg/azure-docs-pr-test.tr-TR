---
title: "Azure CLI aaaCreate bir dahili yük dengeleyici - | Microsoft Docs"
description: "Nasıl toocreate kullanarak iç yük dengeleyiciye hello Azure CLI Kaynak Yöneticisi'nde öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3aea6fdb07600f0d661ec6b8ffc784b03380a127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a>Hello Azure CLI kullanarak bir iç yük dengeleyici oluşturma

> [!div class="op_single_selector"]
> * [Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Şablon](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).  Bu makalede, kullanarak yer almaktadır hello yerine çoğu yeni dağıtımlar için Microsoft önerir hello Resource Manager dağıtım modeli [Klasik dağıtım modeli](load-balancer-get-started-ilb-classic-cli.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a>Hello Azure CLI kullanarak Hello çözümü dağıtma

Aşağıdaki adımları hello nasıl toocreate bir Internet'e yönelik Yük Dengeleyici CLI ile Azure Kaynak Yöneticisi'ni kullanarak gösterir. Azure Resource Manager ile her bir kaynak oluşturulur ve ayrı ayrı yapılandırılır ve toocreate kaynak bir araya getirin.

Nesneleri toodeploy bir yük dengeleyici aşağıdaki hello yapılandırmak ve toocreate gerekir:

* **Ön uç IP yapılandırması**: Gelen ağ trafiği için genel IP adreslerini içerir
* **Arka uç adres havuzu**: hello yük dengeleyiciden hello sanal makineleri tooreceive ağ trafiğini etkinleştiren ağ arabirimlerine (NIC'ler) içerir
* **Yük Dengeleme kuralları**: hello yük dengeleyici tooport hello arka uç adres havuzundaki ortak bir bağlantı noktası eşleme kurallarını içerir
* **Gelen NAT kuralları**: bağlantı noktasında hello yük dengeleyici tooa hello arka uç adres havuzundaki belirli bir sanal makine için genel bir bağlantı noktası eşleme kurallarını içerir
* **Yoklamaları**: kullanılan toocheck hello kullanılabilirlik hello arka uç adres havuzundaki sanal makineler örnekleri olan sistem durumu araştırmalarının içerir

Daha fazla bilgi için bkz. [Yük Dengeleyici için Azure Resource Manager desteği](load-balancer-arm.md).

## <a name="set-up-cli-toouse-resource-manager"></a>CLI toouse Kaynak Yöneticisi'ni ayarlayın

1. Azure CLI hiç kullanmadıysanız bkz [yükleyin ve hello Azure CLI yapılandırma](../cli-install-nodejs.md). Sonra Azure hesabınızı ve aboneliğinizi toohello noktaya Hello talimatlarını izleyin.
2. Merhaba çalıştırmak **azure config modu** tooswitch tooResource Yöneticisi modu, aşağıdaki gibi komutu:

    ```azurecli
    azure config mode arm
    ```

    Beklenen çıktı:

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a>Adım adım iç yük dengeleyici oluşturma

1. TooAzure oturum açın.

    ```azurecli
    azure login
    ```

    İstendiğinde Azure kimlik bilgilerinizi girin.

2. Merhaba komutu araçları tooAzure Resource Manager modunu değiştirin.

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Azure Resource Manager’daki tüm kaynaklar bir kaynak grubuyla ilişkilendirilmiştir. Henüz yapmadıysanız, bir kaynak grubu oluşturun.

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a>İç yük dengeleyici kümesi oluşturma

1. İç yük dengeleyici oluşturma

    Senaryo aşağıdaki hello, Doğu ABD bölgesinde nrprg adlı bir kaynak grubu oluşturulur.

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > Sanal ağlar ve sanal ağ alt ağları gibi bir iç yük dengeleyicileri için tüm kaynakları olmalıdır hello aynı kaynak grubunu ve de aynı hello bölgesi.

2. Merhaba iç yük dengeleyici için bir ön uç IP adresi oluşturun.

    kullandığınız başlangıç IP adresi hello alt ağ aralığında sanal ağınızın olması gerekir.

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. Merhaba arka uç adres havuzu oluşturun.

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    Ön uç IP adresi ve arka uç adres havuzu tanımladıktan sonra yük dengeleyici kurallarını, gelen NAT kurallarını ve özel sistem durumu araştırmalarını oluşturabilirsiniz.

4. Merhaba iç yük dengeleyici için yük dengeleyici kuralı oluşturun.

    Merhaba önceki adımları izlediğinizde, hello komutu dinleme tooport 1433 için bir yük dengeleyici kuralı hello ön uç havuzu ve gönderen yük dengeli ağ trafiği toohello arka uç adres havuzu, ayrıca bağlantı noktası 1433'ü kullanarak oluşturur.

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. Gelen NAT kurallarını oluşturun.

    Gelen NAT kuralları tooa belirli bir sanal makine örneği ziyaret kullanılan toocreate yük dengeleyicideki noktalarıdır. Merhaba önceki adımları Uzak Masaüstü için iki NAT kuralı oluşturuldu.

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. Sistem durumu araştırmalarının hello yük dengeleyici için oluşturun.

    Bir sistem durumu araştırması tüm sanal makine örnekleri toomake ağ trafiğinin gönderebilir emin denetler. Merhaba sanal makine örneği başarısız araştırma denetimleri ile Merhaba yük dengeleyiciden tekrar çevrimiçi duruma geçtiğinde ve bir araştırma denetimi sağlıklı olduğunu belirler kadar kaldırılır.

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > Merhaba Microsoft Azure platformu statik, genel olarak yönlendirilebilir bir IPv4 adresi çeşitli yönetim senaryoları için kullanır. Başlangıç IP adresi 168.63.129.16 değil. Bu IP adresinin güvenlik duvarları tarafından engellenmesi beklenmeyen davranışlara neden olabilir.
    > Saygı tooAzure iç Yük Dengeleme ile bu IP adresi yük dengeli kümesinde sanal makineler için hello yük dengeleyici toodetermine hello sistem durumu araştırmalarının izleme tarafından kullanılır. Bir ağ güvenlik grubu kullanılan toorestrict trafiği tooAzure sanal makineleri bir dahili yük dengeli kümesindeki ya uygulanan tooa sanal ağ alt ise, bir ağ güvenlik kuralı tooallow trafiği 168.63.129.16 eklendiğinden emin olun.

## <a name="create-nics"></a>NIC’leri oluşturma

Toocreate NIC gerekir (veya var olanları değiştirme) ve tooNAT kuralları, yük dengeleyici kuralları ve araştırmalar ilişkilendirebilirsiniz.

1. Adlı bir NIC oluşturun *lb nıc1 olması*ve hello ile ilişkilendirmek *rdp1* NAT kuralı ve hello *beilb* arka uç adres havuzu.

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
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

2. Adlı bir NIC oluşturun *lb nic2 olması*ve hello ile ilişkilendirmek *rdp2* NAT kuralı ve hello *beilb* arka uç adres havuzu.

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. Adlı bir sanal makine oluşturmak *DB1*ve hello adlı NIC ile ilişkilendirme *lb nıc1 olması*. Bir depolama hesabı olarak adlandırılan *web1nrp* komutu çalıştırır aşağıdaki hello önce oluşturulur:

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > Bir yük dengeleyici gerek toobe içinde Vm'lerde aynı kullanılabilirlik kümesinde hello. Kullanım `azure availset create` toocreate kullanılabilirlik kümesi.

4. Adlı sanal makine (VM) oluşturma *DB2*ve hello adlı NIC ile ilişkilendirme *lb nic2 olması*. Bir depolama hesabı olarak adlandırılan *web1nrp* komutu aşağıdaki hello çalıştırmadan önce oluşturuldu.

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a>Yük dengeleyici silme

tooremove bir yük dengeleyici hello aşağıdaki komutu kullanın:

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a>Sonraki adımlar

[Kaynak IP benzeşimi kullanarak yük dengeleyici dağıtım modunu yapılandırma](load-balancer-distribution-mode.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)

