---
title: "aaaCreate hello Azure CLI 1.0 ile eksiksiz bir Linux ortamı | Microsoft Docs"
description: "Tüm hello Azure CLI 1.0 kullanarak plan hello depolama, bir Linux VM, bir sanal ağ ve alt ağ, bir yük dengeleyici, bir NIC, ortak bir IP ve bir ağ güvenlik grubu oluşturun."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 7fe00e138704fe9c9a1c9b87a7dd1afd6174e527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-environment-with-hello-azure-cli-10"></a>Azure CLI 1.0 hello ile eksiksiz bir Linux ortamı oluşturma
Bu makalede, bir yük dengeleyici ve geliştirme ve basit bilgi işlem için yararlı olan VM'ler çifti ile basit bir ağ oluşturun. Biz komutu tarafından komut hello işleminde size kılavuzluk, iki çalışma kadar gelen herhangi bir yere hello Internet üzerinde bağlayabilirsiniz Linux VM'ler toowhich güvenli. Ardından, toomore karmaşık ağlar ve ortamları taşıyabilirsiniz.

Merhaba yol boyunca hello Resource Manager dağıtım modeli sağlar ve hakkında ne kadar güç sağlar hello bağımlılık hiyerarşi öğrenin. Merhaba sistem nasıl yapılandırıldığını gördükten sonra bu çok daha hızlı bir şekilde kullanarak yeniden oluşturmak için kullanabileceğiniz [Azure Resource Manager şablonları](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Ayrıca, hello bölümleri ortamınızın nasıl bir araya getireceğinizi öğrenin sonra şablonları tooautomate oluşturarak bunları olur daha kolay.

Merhaba ortamı içerir:

* İki VM bir kullanılabilirlik kümesi içinde.
* Yük Dengeleyici Yük Dengeleme kuralı bağlantı noktası 80 ile.
* Ağ güvenlik grubu (NSG), VM istenmeyen trafiğinden tooprotect kuralları.

toocreate bu özel ortam hello son gereksinim [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Kaynak Yöneticisi modunda (`azure config mode arm`). Ayrıca aracı ayrıştırma JSON gerekir. Bu örnekte [jq](https://stedolan.github.io/jq/).


## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- [Azure CLI 1.0](#quick-commands) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için


## <a name="quick-commands"></a>Hızlı komutlar
Tooquickly gerekiyorsa hello görevi, hello bölüm ayrıntıları hello aşağıdaki komutları tooupload VM tooAzure temel. Her adım başlangıç hello belgenin hello kalan bulunabilir bilgi ve içerik daha ayrıntılı [burada](#detailed-walkthrough).

Bilgisayarınızda yüklü olduğundan emin olun [Azure CLI 1.0 hello](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) oturum açmış ve Resource Manager modunu kullanma:

```azurecli
azure config mode arm
```

Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adlarında `myResourceGroup`, `mystorageaccount`, ve `myVM`.

Merhaba kaynak grubu oluşturun. Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westeurope` konumu:

```azurecli
azure group create -n myResourceGroup -l westeurope
```

Merhaba kaynak grubu hello JSON ayrıştırıcısı kullanarak doğrulayın:

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Merhaba depolama hesabı oluşturun. Merhaba aşağıdaki örnek adlı bir depolama hesabı oluşturur `mystorageaccount`. (Merhaba depolama hesabı adı gerekir benzersiz olması, bu nedenle, kendi benzersiz bir ad sağlayın.)

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

Merhaba depolama hesabı hello JSON ayrıştırıcısı kullanarak doğrulayın:

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

Merhaba sanal ağ oluşturun. Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur `myVnet`:

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

Bir alt ağ oluşturun. Merhaba aşağıdaki örnek adlı bir alt ağı oluşturur `mySubnet`:

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

Merhaba sanal ağ ve alt hello JSON ayrıştırıcısı kullanarak doğrulayın:

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

Genel IP oluşturun. Merhaba aşağıdaki örnekte oluşturur adlı ortak IP `myPublicIP` hello DNS adı ile `mypublicdns`. (Merhaba DNS adı gerekir benzersiz olması, bu nedenle, kendi benzersiz bir ad sağlayın.)

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

Merhaba yük dengeleyicisi oluşturun. Merhaba aşağıdaki örnek adlı bir yük dengeleyici oluşturur `myLoadBalancer`:

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

Merhaba yük dengeleyici için bir ön uç IP havuzu oluşturun ve hello genel IP ilişkilendirin. Merhaba aşağıdaki örnek adlı bir ön uç IP havuzu oluşturur `mySubnetPool`:

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

Merhaba yük dengeleyici için Hello arka uç IP havuzu oluşturun. Merhaba aşağıdaki örnekte oluşturur adlı bir arka uç IP havuzu `myBackEndPool`:

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

SSH gelen ağ adresi çevirisi (NAT) kuralları hello yük dengeleyici için oluşturun. Merhaba aşağıdaki örnekte oluşturur iki yük dengeleyici kuralları, `myLoadBalancerRuleSSH1` ve `myLoadBalancerRuleSSH2`:

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

Merhaba web oluşturmak yük dengeleyici gelen NAT kuralları hello için. Merhaba aşağıdaki örnek adlı bir yük dengeleyici kuralı oluşturur `myLoadBalancerRuleWeb`:

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

Merhaba yük dengeleyici durum araştırması oluşturun. Merhaba aşağıdaki örnek adlı bir TCP araştırması oluşturur `myHealthProbe`:

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

Merhaba yük dengeleyici, IP havuzları ve NAT kuralları hello JSON ayrıştırıcısı kullanarak doğrulayın:

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

Merhaba ilk ağ arabirim kartı (NIC) oluşturun. Hello yerine `#####-###-###` bölümleri, kendi Azure aboneliği ID'ye sahip Aboneliğinizi hello çıktısında kimliği not ettiğiniz **jq** oluşturmakta hello kaynakları incelediğinizde. Abonelik Kimliğinizle de görüntüleyebilirsiniz `azure account list`.

Merhaba aşağıdaki örnekte oluşturur adlı bir NIC `myNic1`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

Merhaba ikinci NIC oluşturun Merhaba aşağıdaki örnekte oluşturur adlı bir NIC `myNic2`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

Merhaba iki NIC hello JSON ayrıştırıcısı kullanarak doğrulayın:

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

Merhaba ağ güvenlik grubu oluşturun. Merhaba aşağıdaki örnek adlı bir ağ güvenlik grubu oluşturur `myNetworkSecurityGroup`:

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

Merhaba ağ güvenlik grubu için iki gelen kuralı ekleyin. Merhaba aşağıdaki örnekte oluşturur iki kural `myNetworkSecurityGroupRuleSSH` ve `myNetworkSecurityGroupRuleHTTP`:

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

Merhaba ağ güvenlik grubu ve gelen kuralları hello JSON ayrıştırıcısı kullanarak doğrulayın:

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

Merhaba ağ güvenliği bağlama toohello iki NIC grubu:

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

Merhaba kullanılabilirlik kümesi oluşturun. Merhaba aşağıdaki örnekte oluşturur kullanılabilirlik adlandırılmış kümesi `myAvailabilitySet`:

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

Oluşturma ilk Linux VM hello. Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM1`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

Merhaba oluşturma Linux VM ikinci. Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM2`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

Merhaba JSON ayrıştırıcı tooverify bu her şeyi, oluşturulmuş kullanın:

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

Yeni ortam tooa şablonu tooquickly yeniden oluşturmanız yeni örneklerinizi dışarı aktarın:

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a>Ayrıntılı kılavuz
Merhaba izleyin ayrıntılı adımlar ortamınızı yapı gibi her komutun ne yaptığını açıklanmaktadır. Bu kavramlar, kendi özel ortamınız için geliştirme veya üretim derlerken faydalıdır.

Bilgisayarınızda yüklü olduğundan emin olun [Azure CLI 1.0 hello](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) oturum açmış ve Resource Manager modunu kullanma:

```azurecli
azure config mode arm
```

Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adlarında `myResourceGroup`, `mystorageaccount`, ve `myVM`.

## <a name="create-resource-groups-and-choose-deployment-locations"></a>Kaynak grupları oluşturun ve dağıtım konumları seçin
Azure kaynak gruplarını yapılandırma bilgilerini ve meta veri tooenable hello mantıksal Yönetimi kaynak dağıtımlarını içeren mantıksal dağıtım varlıklardır. Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westeurope` konumu:

```azurecli
azure group create --name myResourceGroup --location westeurope
```

Çıktı:

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a>Depolama hesabı oluşturma
Tooadd istediğiniz depolama hesapları olan ek veri disklerinin ve VM diskleri için gerekir. Kaynak grupları oluşturun sonra hemen hemen depolama hesapları oluşturun.

Merhaba burada kullandığımız `azure storage account create` komutunu hello hello hesabı, hello kaynak grubu konumunu geçirme denetler ve istediğiniz depolama destek hello türü. Merhaba aşağıdaki örnek adlı bir depolama hesabı oluşturur `mystorageaccount`:

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

Çıktı:

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

Bizim kaynak grubunda hello kullanarak tooexamine `azure group show` komutu, hello kullanalım [jq](https://stedolan.github.io/jq/) aracı ile birlikte hello `--json` Azure CLI seçeneği. (Kullanabileceğiniz **jsawk** veya tooparse tercih ettiğiniz herhangi bir dil kitaplığı hello JSON.)

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Çıktı:

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

Merhaba CLI kullanarak tooinvestigate hello depolama hesabı, önce tooset hello hesap adlarını ve anahtarları gerekir. Aşağıdaki seçtiğiniz bir adla örneğine hello hello depolama hesabında Hello adını değiştirin:

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

Ardından, depolama bilgilerinizi kolayca görüntüleyebilirsiniz:

```azurecli
azure storage container list
```

Çıktı:

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a>Bir sanal ağ ve alt ağ oluşturun
Sonraki tooneed toocreate Azure ve Vm'lerinizi oluşturabileceğiniz bir alt ağ içinde çalışan bir sanal ağ oluşturacağız. Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur `myVnet` hello ile `192.168.0.0/16` adres öneki:

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

Çıktı:

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

Yeniden hello--json seçeneği kullanalım `azure group show` ve `jq` toosee nasıl KAYNAKLARIMIZI oluşturmakta olduğumuz. Şimdi sahip olduğumuz bir `storageAccounts` kaynak ve `virtualNetworks` kaynak.  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Çıktı:

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

Şimdi bir alt ağ hello oluşturalım `myVnet` sanal ağ içinde hangi hello VM'ler dağıtılır. Merhaba kullanırız `azure network vnet subnet create` zaten oluşturduğumuz hello kaynakları birlikte komutu: Merhaba `myResourceGroup` kaynak grubu ve hello `myVnet` sanal ağ. Aşağıdaki örneğine hello adlı hello alt eklediğimiz `mySubnet` hello alt ağ adresi öneki ile `192.168.1.0/24`:

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

Çıktı:

```azurecli
info:    Executing command network vnet subnet create
+ Looking up hello subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up hello subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

Merhaba alt mantıksal olarak hello sanal ağ içinde olduğundan, biz biraz farklı bir komutla hello alt ağ bilgilerini arayın. Merhaba komutu kullanırız `azure network vnet show`, ancak kullanarak tooexamine hello JSON çıktısını devam `jq`.

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

Çıktı:

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a>Genel IP adresi oluşturma
Şimdi biz tooyour yük dengeleyici atamak hello genel IP adresi (PIP) oluşturalım. Merhaba Internet gelen tooconnect tooyour VM'ler hello kullanarak sağlar `azure network public-ip create` komutu. Merhaba varsayılan adres dinamik olduğundan, adlandırılmış bir DNS girişi hello oluşturuyoruz **cloudapp.azure.com** hello kullanarak etki alanı `--domain-name-label` seçeneği. Merhaba aşağıdaki örnekte oluşturur adlı ortak IP `myPublicIP` hello DNS adı ile `mypublicdns`. Merhaba DNS adının benzersiz olması gerektiğinden, kendi benzersiz DNS adını belirtin:

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

Çıktı:

```azurecli
info:    Executing command network public-ip create
+ Looking up hello public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up hello public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

ile görebilirsiniz hello ortak IP adresini de üst düzey bir kaynak olduğundan `azure group show`.

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Çıktı:

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

Merhaba tam kullanarak hello hello alt etki alanının tam etki alanı adı (FQDN) de dahil olmak üzere daha fazla kaynak ayrıntılarını araştırabilirsiniz `azure network public-ip show` komutu. Merhaba ortak IP adresi kaynağı mantıksal olarak ayrıldı, ancak belirli bir adresi yok henüz atanmamış. bir IP adresi tooobtain, tooneed değil henüz oluşturduk bir yük dengeleyici oluşturacağız.

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

Çıktı:

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a>Bir yük dengeleyici ve IP havuzları oluşturma
Bir yük dengeleyici oluşturduğunuzda, toodistribute trafiği arasında birden çok VM sağlar. Ayrıca, Bakım veya ağır yükten hello olayı içinde toouser isteklerine yanıt birden çok VM çalıştırarak artıklık tooyour uygulama da sağlar. Merhaba aşağıdaki örnek adlı bir yük dengeleyici oluşturur `myLoadBalancer`:

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

Çıktı:

```azurecli
info:    Executing command network lb create
+ Looking up hello load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

Bizim yük dengeleyici sağlandığından bazı IP havuzları oluşturmak oldukça boş olur. Toocreate iki IP havuzları istiyoruz bizim yük dengeleyici, biri hello ön uç için diğeri hello arka uç için. Merhaba ön uç IP havuzu herkese görünür. Ayrıca, biz hello daha önce oluşturduğumuz PIP atamak hello konumu toowhich unutulmamalıdır. Ardından hello arka uç havuzu gibi bir konuma bizim VM'ler tooconnect için kullanırız. Bu şekilde hello trafiği hello yük dengeleyici toohello VM'ler akabilir.

İlk olarak, bizim ön uç IP havuzu oluşturalım. Merhaba aşağıdaki örnekte oluşturur adlı bir ön uç havuzu `myFrontEndPool`:

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

Çıktı:

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up hello load balancer "myLoadBalancer"
+ Looking up hello public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

Merhaba nasıl kullandık Not `--public-ip-name` toopass hello geçiş `myPublicIP` daha önce oluşturduğumuz. Merhaba ortak IP adresi toohello yük dengeleyici tooreach sağlar, VM'ler hello Internet üzerindeki.

Ardından, bizim ikinci IP havuzu bizim arka uç trafiği için bu süre oluşturalım. Merhaba aşağıdaki örnekte oluşturur adlı bir arka uç havuzu `myBackEndPool`:

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

Çıktı:

```azurecli
info:    Executing command network lb address-pool create
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

Bizim yük dengeleyici ile bakarak nasıl çalıştığını görebiliriz `azure network lb show` hello JSON çıktısını inceleyerek:

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

Çıktı:

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a>Yük dengeleyicisi NAT kuralları oluşturma
Bizim yük dengeleyici üzerinden akan tooget trafiği gelen veya giden eylemleri belirtin toocreate ağ adresi çevirisi (NAT) kuralları ihtiyacımız. Merhaba Protokolü toouse belirtin, sonra istediğiniz gibi dış bağlantı noktaları toointernal bağlantı noktalarını eşleyin. Bizim ortamı için SSH bizim yük dengeleyici tooour VM'ler izin veren bazı kurallar oluşturalım. (Bu, daha sonra oluşturuyoruz) bizim Vm'lerinde TCP bağlantı noktaları 4222 ve 4223 toodirect tooTCP bağlantı 22 ayarlarız. Merhaba aşağıdaki örnek adlı bir kural oluşturur `myLoadBalancerRuleSSH1` toomap TCP bağlantı noktası 4222 tooport 22:

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

Çıktı:

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

Merhaba yordamı, ikinci NAT kuralı için SSH için yineleyin. Merhaba aşağıdaki örnek adlı bir kural oluşturur `myLoadBalancerRuleSSH2` toomap TCP bağlantı noktası 4223 tooport 22:

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

Şimdi de tane hello kural tooour IP havuzları takma web trafiği için TCP bağlantı noktası 80 için NAT kuralı oluşturun. Biz hello kural tooan hello kural tooour VM'ler ayrı ayrı takma yerine IP havuzu kanca varsa biz ekleyebilir veya VM'ler hello IP havuzundan kaldırabilirsiniz. Merhaba yük dengeleyici trafik akışını hello otomatik olarak ayarlar. Merhaba aşağıdaki örnek adlı bir kural oluşturur `myLoadBalancerRuleWeb` toomap TCP bağlantı noktası 80 tooport 80:

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

Çıktı:

```azurecli
info:    Executing command network lb rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a>Bir yük dengeleyici durum araştırması oluştur
Bir sistem durumu araştırması düzenli aralıklarla hello bizim yük dengeleyici toomake işletim ve toorequests tanımlanan yanıt emin olan VM'ler üzerinde denetimleri. Bunlar gelen kaldırdıysanız değil, kullanıcılar olan olmayan işlemi tooensure toothem yönlendirilmiş. Aralıklarla ve zaman aşımı değerlerinin yanı sıra hello durumu araştırması için özel denetimleri tanımlayabilirsiniz. Sistem durumu araştırmalarının hakkında daha fazla bilgi için bkz: [yük dengeleyici yoklamaları](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Merhaba aşağıdaki örnekte oluşturur bir TCP durumu araştırılan adlandırılmış `myHealthProbe`:

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

Çıktı:

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

Burada, 15 saniye bizim durumu denetimleri için bir aralığı belirtildi. Biz, en fazla dört araştırmalar (Merhaba barındıran artık çalışmıyor hello yük dengeleyici varsaymadan önce bir dakika) eksik.

## <a name="verify-hello-load-balancer"></a>Merhaba yük dengeleyici doğrulayın
Şimdi hello yük dengeleyici yapılandırması yapılır. Yaptığınız hello adımlar şunlardır:

1. Bir yük dengeleyici oluşturuldu.
2. Bir ön uç IP havuzu oluşturduğunuz ve bir ortak IP tooit atanmış.
3. Sanal makineleri bağlanabileceği bir arka uç IP havuzu oluşturuldu.
4. SSH toohello VM'ler Yönetim için web uygulamamız için TCP bağlantı noktası 80 sağlayan bir kural ile birlikte izin veren NAT kuralları oluşturuldu.
5. Sistem durumu araştırma tooperiodically onay hello VM'ler eklendi. Bu sistem durumu araştırma kullanıcılar tooaccess artık çalışmıyor veya içerik hizmet veren bir VM denemeyin sağlar.

Şimdi, yük dengeleyici şimdi gibi göründüğünü gözden geçirin:

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

Çıktı:

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-toouse-with-hello-linux-vm"></a>Bir NIC toouse hello ile Linux VM oluşturma
NIC program aracılığıyla kullanılabilir olduklarından kuralları tootheir kullanım uygulayabilirsiniz. Birden fazla olabilir. Merhaba aşağıdaki `azure network nic create` komutu, hello NIC toohello yük arka uç IP Havuzu'nu bağlanmasını ve NAT kuralı toopermit SSH trafiği hello ile ilişkilendirin.

Hello yerine `#####-###-###` bölümleri, kendi Azure aboneliği ID'ye sahip Aboneliğinizi hello çıktısında kimliği not ettiğiniz `jq` oluşturmakta hello kaynakları incelediğinizde. Abonelik Kimliğinizle de görüntüleyebilirsiniz `azure account list`.

Merhaba aşağıdaki örnekte oluşturur adlı bir NIC `myNic1`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

Çıktı:

```azurecli
info:    Executing command network nic create
+ Looking up hello subnet "mySubnet"
+ Looking up hello network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

Merhaba kaynak doğrudan inceleyerek hello ayrıntılarını görebilirsiniz. Hello kullanarak hello kaynağın incelemeniz `azure network nic show` komutu:

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

Çıktı:

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

Oluşturuyoruz artık tooour arka uç IP havuzundaki yeniden takma, ikinci bir NIC hello. Bu zaman hello ikinci NAT kuralı SSH trafiğe izin verir. Merhaba aşağıdaki örnekte oluşturur adlı bir NIC `myNic2`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a>Bir ağ güvenlik grubu ve kuralları oluşturma
Bir ağ güvenlik grubu oluşturun ve yöneten gelen kuralları hello artık toohello NIC erişim Bir ağ güvenlik grubu uygulanan tooa NIC veya alt ağ olabilir. Vm'leriniz ve bu moddan kuralları toocontrol hello trafik akışını tanımlayın. Merhaba aşağıdaki örnek adlı bir ağ güvenlik grubu oluşturur `myNetworkSecurityGroup`:

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

Merhaba NSG tooallow için gelen kuralı hello ekleyelim gelen bağlantı noktası 22 (toosupport SSH) bağlantı. Merhaba aşağıdaki örnek adlı bir kural oluşturur `myNetworkSecurityGroupRuleSSH` tooallow TCP bağlantı noktası 22:

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

Şimdi hello NSG tooallow için gelen kuralı hello ekleyelim gelen bağlantı noktası 80 (toosupport web trafiği) bağlantı. Merhaba aşağıdaki örnek adlı bir kural oluşturur `myNetworkSecurityGroupRuleHTTP` tooallow TCP bağlantı noktası 80 üzerinde:

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> Merhaba gelen kuralı, gelen ağ bağlantıları için bir filtredir. Bu örnekte, hello NSG toohello tüm istek tooport 22 bizim VM NIC toohello geçirilen anlamına gelir VM'ler sanal NIC bağlayın. Bu gelen kuralı bir ağ bağlantısı hakkında ve bir uç nokta hakkında hangi hakkında Klasik dağıtımlarda olması. tooopen bir bağlantı noktası, hello bırakın gerekir `--source-port-range` çok Ayarla '\*' (Merhaba varsayılan değer) tooaccept gelen istekleri **herhangi** bağlantı noktası isteme. Bağlantı noktaları genellikle dinamik.
>
>

## <a name="bind-toohello-nic"></a>Toohello NIC bağlama
Merhaba NSG toohello NIC'ler bağlayın. Tooconnect bizim NIC'ler bizim ağ güvenlik grubuyla ihtiyacımız var. Bizim NIC'ler her ikisi de yukarı toohook hem komutları çalıştırın:

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a>Kullanılabilirlik kümesi oluşturma
Kullanılabilirlik Yardım yayılan hata etki alanları ve yükseltme etki alanları arasında Vm'leriniz ayarlar. Kullanılabilirlik kümesi Vm'leriniz için oluşturalım. Merhaba aşağıdaki örnekte oluşturur kullanılabilirlik adlandırılmış kümesi `myAvailabilitySet`:

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

Sanal makineler, ortak bir güç kaynağı ve ağ anahtarı paylaşmak gruplandırması hata etki alanlarını tanımlayın. Varsayılan olarak, kullanılabilirlik kümesi içinde yapılandırılmış hello sanal makineleri toothree hata etki alanları arasında ayrılır. Merhaba bir donanım sorunundan birinde bu hata etki alanları, uygulamanızı çalıştıran her VM etkilemez olur. Azure otomatik olarak VM'ler hello hata etki alanlarında bunları bir kullanılabilirlik kümesine yerleştirdiğinizde dağıtır.

Yükseltme etki alanları belirtmek sanal makineler ve hello yeniden temel alınan fiziksel donanım grupları aynı anda. Yükseltme etki alanları yeniden başlatılır hello sıra planlı bakım sırasında sıralı olmayabilir, ancak aynı anda yalnızca bir yükseltme yeniden başlatıldı. Yeniden Azure otomatik olarak Vm'leriniz yükseltme etki alanları arasında bir kullanılabilirlik sitede yerleştirme sırasında dağıtır.

Daha fazla bilgi edinin [VM'ler hello kullanılabilirliğini yönetme](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="create-hello-linux-vms"></a>Merhaba Linux VM'ler oluşturma
Internet'ten erişilebilen toosupport VM'ler hello depolama ve ağ kaynaklarını oluşturduğunuzu düşünün. Şimdi şimdi bunları VM'ler oluşturun ve bir parola sahip olmayan bir SSH anahtarı ile güvenli. Bu durumda, bir Ubuntu VM tabanlı hello üzerinde toocreate yapacağız en son LTS. Biz kullanarak bu görüntü bilgilerini bulun `azure vm image list`açıklandığı gibi [Azure VM görüntülerini bulma](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Merhaba komutunu kullanarak bir görüntü seçtik `azure vm image list westeurope canonical | grep LTS`. Bu durumda, kullandığımız `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`. Merhaba son alanı için biz geçirmek `latest` böylece hello gelecekte biz her zaman en son yapı hello alın. (kullanırız hello dizesi `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).

Bu zaten oluşturdu tanıdık tooanyone sonraki adımdır bir ssh rsa ortak ve özel anahtarı eşleştirin Linux veya Mac kullanarak **ssh-keygen - t rsa -b 2048**. Tüm sertifika anahtar çiftleri varsa değil, `~/.ssh` dizin oluşturabilirsiniz bunları:

* Hello kullanarak otomatik olarak `azure vm create --generate-ssh-keys` seçeneği.
* Kullanarak el ile [hello yönergeleri toocreate bunları kendiniz](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Alternatif olarak, hello kullanabilirsiniz `--admin-password` yöntemi tooauthenticate SSH bağlantılarınızı hello VM sonra oluşturulur. Bu yöntem genellikle daha az güvenlidir.

Bizim tüm kaynaklara ve bilgi ile birlikte hello getirerek hello VM oluşturuyoruz `azure vm create` komutu:

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

Çıktı:

```azurecli
info:    Executing command vm create
+ Looking up hello VM "myVM1"
info:    Verifying hello public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using hello VM Size "Standard_DS1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Looking up hello storage account mystorageaccount
+ Looking up hello availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up hello NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in hello NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    hello storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by hello parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

Varsayılan SSH anahtarları kullanılarak tooyour VM hemen bağlanabilir. Merhaba yük dengeleyici üzerinden geçirme bu yana hello uygun bağlantı noktasını belirttiğinizden emin olun. (Bizim ilk VM için hello NAT kuralı tooforward bağlantı noktası 4222 tooour VM ayarlarız.)

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

Çıktı:

```bash
hello authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

Tane hello ikinci VM oluşturun aynı şekilde:

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

Merhaba şimdi kullanabileceğiniz `azure vm show myResourceGroup myVM1` oluşturmuş olduğunuz tooexamine komutu. Bu noktada, Ubuntu Vm'leriniz yük dengeleyici arkasında (parolalar devre dışı bırakıldığı için), yalnızca, SSH anahtar çifti ile içine imzalayabilirsiniz Azure'da kullanıyorsunuz. Nginx veya httpd yükleyin, bir web uygulaması dağıtma ve hello trafiğini hello yük dengeleyici tooboth hello VM'lerin aktığı.

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

Çıktı:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "TestVM1"
+ Looking up hello NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-hello-environment-as-a-template"></a>Merhaba ortamı şablon olarak dışarı aktarma
Bir ek geliştirme ortamı hello toocreate ne istediğiniz bu ortam yerleşik göre aynı parametreleri veya eşleşecek bir üretim ortamında? Resource Manager, ortamınız için tüm hello parametreleri tanımlayan JSON şablonlarını kullanır. Bu JSON şablonunu başvurarak tüm ortamlar oluşturun. Yapabilecekleriniz [JSON şablonları el ile oluşturabilir](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya var olan bir ortam toocreate hello JSON şablonunu verdiğiniz:

```azurecli
azure group export --name myResourceGroup
```

Bu komut hello oluşturur `myResourceGroup.json` geçerli çalışma dizini dosyasında. Bu şablonu kullanarak bir ortam oluşturduğunuzda, hello yük dengeleyici, ağ arabirimleri ya da VM'ler için hello adları dahil olmak üzere tüm hello kaynak adları istenir. Merhaba ekleyerek bu adları şablon dosyanızın doldurabilirsiniz `-p` veya `--includeParameterDefaultValue` parametresi toohello `azure group export` daha önce gösterilen komutu. JSON şablonunu toospecify hello kaynak adları, düzenlemek veya [parameters.json dosyası oluşturma](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) hello kaynak adları belirtir.

şablonunuzu bir ortamdan toocreate:

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

Tooread isteyebilirsiniz [nasıl hakkında daha fazla şablonlardan toodeploy](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Nasıl tooincrementally güncelleştirme ortamlarda, hello parametreleri dosyasını kullanın ve şablonları bir tek bir depolama konumundan erişim hakkında bilgi edinin.

## <a name="next-steps"></a>Sonraki adımlar
Artık birden çok ağ bileşenleri ve VM'ler ile çalışmaya hazır toobegin demektir. Burada sunulan hello çekirdek bileşenlerini kullanarak, bu örnek ortamı toobuild uygulamanızı kullanabilirsiniz.
