---
title: "IPv6 - Azure CLI ile aaaCreate bir Internet'e yönelik Yük Dengeleyici | Microsoft Docs"
description: "Nasıl toocreate Azure Resource Manager kullanarak bir Internet'e yönelik Yük Dengeleyici IPv6 hello Azure CLI öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "IPv6, azure yük dengeleyici, çift yığın, genel IP, yerel IPv6, mobil, IOT"
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7ff75ac90d74a74e3d0c27672b36fbd955a086a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-hello-azure-cli"></a>Internet'e yönelik Yük Dengeleyici IPv6 Azure kaynağı hello Azure CLI kullanarak Yöneticisi'nde oluşturun

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [Azure CLI](load-balancer-ipv6-internet-cli.md)
> * [Şablon](load-balancer-ipv6-internet-template.md)

Azure Load Balancer bir Katman 4 (TCP, UDP) yük dengeleyicidir. Merhaba yük dengeleyici, gelen trafiği bulut Hizmetleri sağlıklı hizmet örnekleri veya bir yük dengeleyici kümesindeki sanal makineler arasında dağıtarak yüksek kullanılabilirlik sağlar. Ayrıca, Azure Load Balancer bu hizmetleri birden çok bağlantı noktasında, birden çok IP adresinde ya da her ikisinde birden sağlayabilir.

## <a name="example-deployment-scenario"></a>Örnek dağıtım senaryosu

Merhaba Aşağıdaki diyagramda gösterilmektedir hello yük dengeleme çözümü bu makalede açıklanan hello örnek şablon kullanılarak dağıtılan.

![Yük dengeleyici senaryosu](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

Bu senaryoda aşağıdaki Azure kaynakları hello oluşturacak:

* iki sanal makine (VM)
* atanan IPv4 ve IPv6 adreslerinin her VM için bir sanal ağ arabirimi
* bir IPv4 ve IPv6 genel IP adresi olan bir Internet'e yönelik Yük Dengeleyici
* Merhaba iki sanal makineleri bir kullanılabilirlik kümesi toothat içerir
* iki Yük Dengeleme kuralları toomap hello ortak VIP'ler toohello özel uç noktaları

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>Hello Azure CLI kullanarak hello çözümü dağıtma

Aşağıdaki adımları hello nasıl toocreate Internet'e yönelik Yük Dengeleyici CLI ile Azure Resource Manager kullanarak gösterir. Azure Resource Manager ile her bir kaynak oluşturulur ve ayrı ayrı yapılandırılır ve toocreate kaynak bir araya getirin.

oluşturma ve nesneleri aşağıdaki hello yapılandırma toodeploy bir yük dengeleyici:

* Ön uç IP yapılandırması: Gelen ağ trafiği için genel IP adreslerini içerir.
* Arka uç adres havuzu - hello yük dengeleyici gelen hello sanal makineleri tooreceive ağ trafiği için ağ arabirimlerine (NIC'ler) içerir.
* Yük Dengeleme kuralları - hello yük dengeleyici tooport hello arka uç adres havuzundaki ortak bir bağlantı noktası eşleme kurallarını içerir.
* Gelen NAT kuralları - noktasında hello yük dengeleyici tooa hello arka uç adres havuzundaki belirli bir sanal makine için genel bir bağlantı noktası eşleme kurallarını içerir.
* Yoklamaları - sistem durumu kullanılan araştırmalar toocheck kullanılabilirliği hello arka uç adres havuzundaki sanal makineler örnekleri içerir.

Daha fazla bilgi için bkz. [Yük Dengeleyici için Azure Resource Manager desteği](load-balancer-arm.md).

## <a name="set-up-your-cli-environment-toouse-azure-resource-manager"></a>CLI ortamı toouse Azure Resource Manager ayarlayın

Bu örnekte, biz bir PowerShell komut penceresinde hello CLI araçlarını çalışıyor. Hello Azure PowerShell cmdlet'lerini kullanmayan ancak PowerShell'in komut dosyası özellikleri tooimprove okunabilirlik ve yeniden kullanırız.

1. Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.
2. Merhaba çalıştırmak **azure config modu** komutu tooswitch tooResource Yöneticisi modu.

    ```azurecli
    azure config mode arm
    ```

    Beklenen çıktı:

        info:    New mode is arm

3. İçinde tooAzure oturum ve Aboneliklerin listesini alın.

    ```azurecli
    azure login
    ```

    İstendiğinde Azure kimlik bilgilerinizi girin.

    ```azurecli
    azure account list
    ```

    Merhaba aboneliğini toouse seçin. Merhaba sonraki adımınız hello abonelik kimliği not edin.

4. Merhaba CLI komutları ile kullanmak için PowerShell değişkenleri ayarlayın.

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a>Bir kaynak grubu, bir yük dengeleyici, bir sanal ağ ve alt ağlar oluşturun

1. Kaynak grubu oluşturma

    ```azurecli
    azure group create $rgName $location
    ```

2. Yük dengeleyici oluşturma

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. Bir sanal ağ (VNet) oluşturun.

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    Bu VNet iki alt ağ oluşturun.

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-hello-front-end-pool"></a>Ortak IP adresleri hello ön uç havuzu için oluşturma

1. Merhaba PowerShell değişkenlerini ayarlamak

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. Bir ortak IP adresi hello ön uç IP havuzu oluşturun.

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > Merhaba yük dengeleyicisi hello etki alanı etiketi hello ortak IP FQDN'sini kullanır. Bu yük dengeleyici FQDN hello gibi hello bulut hizmeti adı kullanan Klasik dağıtım değişiklik.
    > Bu örnekte, hello FQDN'sidir *contoso09152016.southcentralus.cloudapp.azure.com*.

## <a name="create-front-end-and-back-end-pools"></a>Ön uç ve arka uç havuzları oluşturma

Bu örnek hello hello yük dengeleyici gelen ağ trafiğini alan hello ön uç IP havuzu ve burada hello ön uç havuzu hello yük dengeli ağ trafiği gönderir hello arka uç IP havuzu oluşturur.

1. Merhaba PowerShell değişkenlerini ayarlamak

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. Merhaba genel IP Hello önceki adımı ve hello yük dengeleyici oluşturulan ilişkilendirme bir ön uç IP havuzu oluşturun.

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-hello-probe-nat-rules-and-lb-rules"></a>Merhaba araştırma, NAT kuralları ve LB kuralları oluşturma

Bu örnekte aşağıdaki öğelerindeki hello oluşturur:

* bir araştırma kural toocheck bağlantı tooTCP bağlantı noktası 80
* NAT kuralı tootranslate 3389 numaralı bağlantı noktası 3389 tooport tüm gelen trafiği için RDP<sup>1</sup>
* NAT kuralı tootranslate 3389 numaralı bağlantı noktası 3391 tooport tüm gelen trafiği için RDP<sup>1</sup>
* bir yük dengeleyici kuralı toobalance hello arka uç havuzundaki tüm gelen trafiği hello üzerinde bağlantı noktası 80 tooport 80 giderir.

<sup>1</sup> NAT kurallardır hello yük dengeleyicinin arkasındaki ilişkili tooa belirli bir sanal makine örneği. Merhaba ağ trafiği 3389 numaralı bağlantı noktasına ulaşan toohello belirli bir sanal makine ve bağlantı noktası hello NAT kuralıyla ilişkili gönderilir. NAT kuralı için bir protokol (UDP veya TCP) belirtmeniz gerekir. Her iki protokole olamaz toohello aynı bağlantı noktasını atanmış.

1. Merhaba PowerShell değişkenlerini ayarlamak

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. Merhaba araştırması oluştur

    Merhaba aşağıdaki örnek denetleyen bir TCP araştırması bağlantı tooback uç TCP bağlantı noktası 80 için 15 dakikada oluşturur. Bunu hello arka uç kaynak kullanılamıyor sonra iki ardışık hatalarını işaretler.

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. Toohello arka uç kaynaklarına RDP bağlantılara izin veren gelen NAT kuralları oluşturma

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. Bir yük dengeleyici trafiği toodifferent arka uç bağlantı noktaları bağlı olarak hangi ön uç alınan hello isteği gönderme kuralları oluşturma

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. Ayarlarınızı denetleyin

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    Beklenen çıktı:

        info:    Executing command network lb show
        info:    Looking up hello load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a>NIC’leri oluşturma

NIC oluşturun ve bunları tooNAT kuralları, yük dengeleyici kuralları ve araştırmalar ilişkilendirin.

1. Merhaba PowerShell değişkenlerini ayarlamak

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. Her arka uç için bir NIC oluşturun ve IPv6 yapılandırmasını ekleyin.

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-hello-back-end-vm-resources-and-attach-each-nic"></a>Merhaba arka uç VM kaynakları oluşturun ve her NIC ekleme

toocreate VM'ler, bir depolama hesabınızın olması gerekir. Yük Dengeleme için hello sanal makineleri bir kullanılabilirlik kümesi toobe üyeleri gerekir. Sanal makineleri oluşturma hakkında daha fazla bilgi için bkz: [Azure PowerShell kullanarak bir VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)

1. Merhaba PowerShell değişkenlerini ayarlamak

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > Bu örnek düz metin hello VM'ler için hello kullanıcı adını ve parolasını kullanır. Kullanarak hello temizleyin kimlik bilgileri değiştiğinde uygun dikkatli olunması gerekir. Merhaba daha güvenli bir yöntem PowerShell kimlik bilgilerini işleme bilgi için bkz: [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet'i.

2. Merhaba depolama hesabı ve kullanılabilirlik kümesi oluştur

    Merhaba VM'ler oluşturduğunuzda, mevcut bir depolama hesabını kullanabilir. komutu aşağıdaki hello yeni bir depolama hesabı oluşturur.

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    Ardından, hello kullanılabilirlik kümesi oluşturun.

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. İle ilişkili hello NIC Hello sanal makineler oluşturma

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a>Sonraki adımlar

[Bir iç yük dengeleyici yapılandırmaya başlayın](load-balancer-get-started-ilb-arm-cli.md)

[Yük dengeleyici dağıtım modu yapılandırma](load-balancer-distribution-mode.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)
