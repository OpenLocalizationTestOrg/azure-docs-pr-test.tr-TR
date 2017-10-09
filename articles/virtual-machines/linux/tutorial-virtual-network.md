---
title: "aaaAzure sanal ağlar ve Linux sanal makineleri | Microsoft Docs"
description: "Öğretici - Azure sanal ağlar ve Linux sanal makineleri hello Azure CLI ile yönetme"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a>Azure sanal ağlar ve Linux sanal makineleri hello Azure CLI ile yönetme

Azure sanal makineler, iç ve dış ağ iletişimi için Azure ağ kullanın. Bu öğreticide iki sanal makine dağıtma ve bu VM'ler için Azure ağı yapılandırma açıklanmaktadır. bir uygulama hello öğreticide dağıtılmamış ancak bu öğreticide hello örnekler hello VM'ler bir veritabanı arka uç, web uygulamasıyla barındırıyorsanız varsayar. Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * Sanal ağ dağıtma
> * Bir alt ağ içinde bir sanal ağ oluşturma
> * Sanal makineler tooa alt ağ ekleme
> * Sanal makine ortak IP adreslerini yönetin
> * Gelen Internet trafiği güvenli
> * VM tooVM trafiği güvenli


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="vm-networking-overview"></a>VM ağ genel bakış

Azure sanal ağları sanal makineler arasında güvenli ağ bağlantıları etkinleştirmek için Internet ve Azure SQL veritabanı gibi diğer Azure hizmetleriyle hello. Sanal ağlar alt ağ olarak adlandırılan mantıksal parçalara bölünür. Alt ağlar kullanılır toocontrol ağ akışı ve güvenlik sınırı. VM dağıtırken, genellikle ekli tooa alt ağ olan bir sanal ağ arabirimi içerir.

## <a name="deploy-virtual-network"></a>Sanal ağ dağıtma

Bu öğreticide, tek bir sanal ağı iki alt ağ ile oluşturulur. Bir web uygulamasını barındırmak için bir ön uç alt ağı ve bir veritabanı sunucusunu barındırmak için bir arka uç alt ağ.

Bir sanal ağ oluşturmadan önce bir kaynak grubuyla oluşturmanız [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myRGNetwork* hello eastus konumda.

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a>Sanal ağ oluşturma

Bize hello [az ağ vnet oluşturma](/cli/azure/network/vnet#create) komutu toocreate bir sanal ağ. Bu örnekte, adlandırılmış hello ağ *mvVnet* ve bir adres öneki belirtilen *10.0.0.0/16*. Bir alt ağ da bir ad oluşturulur *mySubnetFrontEnd* ve bir önek *10.0.1.0/24*. Daha sonra Bu öğreticide bir ön uç VM bağlı toothis alt'dir. 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a>Alt ağ oluşturma

Yeni bir alt ağ hello kullanarak toohello sanal ağ eklenir [az ağ sanal alt oluşturmak](/cli/azure/network/vnet/subnet#create) komutu. Bu örnekte, hello alt adlı *mySubnetBackEnd* ve bir adres öneki belirtilen *10.0.2.0/24*. Bu alt ağ ile tüm arka uç hizmetlerini kullanılır.

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

Bu noktada, ağ oluşturulduğundan ve iki alt ağ, ön uç Hizmetleri için bir tane ve arka uç hizmetlerini için başka bir içine bölümlenmiş. Merhaba sonraki bölümde, sanal makine oluşturulur ve toothese alt bağlı.

## <a name="understand-public-ip-address"></a>Genel IP adresi anlama

Azure kaynaklarını toobe genel bir IP adresi üzerinde erişilebilir sağlayan Internet hello. Merhaba öğreticinin bu bölümünde, bir VM nasıl toowork ortak IP adresleri toodemonstrate oluşturulur.

### <a name="allocation-method"></a>Ayırma yöntemi

Bir ortak IP adresi dinamik veya statik olarak ayrılabilir. Varsayılan olarak, dinamik olarak ayrılan ortak IP adresi. Bir VM serbest bırakıldığında dinamik IP adresleri serbest bırakılır. Bu davranış, VM ayırmayı kaldırma içeren herhangi bir işlem sırasında hello IP adresi toochange neden olur.

Merhaba ayırma yöntemi toostatic, ayarlanabilir tooa VM bile deallocated durumundayken atanan başlangıç IP adresi kalmasını sağlar. Statik olarak ayrılmış bir IP adresi kullanırken, başlangıç IP adresi kendisini belirtilemez. Bunun yerine, kullanılabilir adresler havuzundan tahsis edilir.

### <a name="dynamic-allocation"></a>Dinamik ayırma

Bir VM ile Merhaba oluşturulurken [az vm oluşturma](/cli/azure/vm#create) hello varsayılan genel IP adresi ayırma yöntemi dinamik komutu. Aşağıdaki örneğine hello VM dinamik bir IP adresi ile oluşturulur. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a>Statik ayırma

Hello kullanarak bir sanal makine oluştururken [az vm oluşturma](/cli/azure/vm#create) hello içeriyor, komut `--public-ip-address-allocation static` bağımsız değişkeni tooassign bir statik genel IP adresi. Bu işlem değil gösterilmiştir Bu öğreticide, ancak hello sonraki bölümde dinamik olarak ayrılan bir IP adresi değiştirilen tooa statik adresi ayrılır. 

### <a name="change-allocation-method"></a>Ayırma yöntemini değiştirme

Başlangıç IP adresi ayırma yöntemi hello kullanılarak değiştirilebilir [az ağ ortak IP güncelleştirmesi](/cli/azure/network/public-ip#update) komutu. Bu örnekte, IP adresi ayırma yöntemini ön uç VM değiştirildiğinde hello hello toostatic.

İlk olarak, hello VM serbest bırakma.

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

Kullanım hello [az ağ ortak IP güncelleştirmesi](/cli/azure/network/public-ip#update) tooupdate hello ayırma yöntemi komutu. Bu durumda, hello `--allocation-method` çok ayarlı*statik*.

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

Merhaba VM başlatın.

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a>Ortak IP adresi yok

Genellikle, bir VM toobe üzerinden erişilebilir gerekmez Internet hello. toocreate genel bir IP adresi kullanım hello olmadan bir VM `--public-ip-address ""` bağımsız değişkeni çift tırnak işareti boş dizi. Bu yapılandırma Bu öğreticinin ilerleyen bölümlerinde gösterilmektedir

## <a name="secure-network-traffic"></a>Ağ trafiğinin güvenliğini sağlayın

Bir ağ güvenlik grubu (NSG) izin veren veya reddeden ağ trafiği tooresources tooAzure sanal ağ (VNet) bağlı güvenlik kurallarının bir listesini içerir. Nsg'ler ilişkili toosubnets veya tek tek ağ arabirimleri olabilir. Bir NSG'yi bir ağ arabirimi ile ilişkili olduğunda, yalnızca VM hello ilişkilendirilen geçerlidir. Bir NSG'yi ilişkili tooa alt olduğunda hello kuralları tooall kaynaklara bağlı toohello alt uygulayın. 

### <a name="network-security-group-rules"></a>Ağ güvenlik grubu kuralları

NSG kuralları üzerinden trafik izin verilen veya reddedilen ağ bağlantı noktalarını tanımlar. böylece belirli sistemleri veya alt ağlar arasında trafiği denetlenir hello kuralları kaynak ve hedef IP adresi aralıklarını içerebilir. NSG kuralları da dahil bir öncelik (1 arasında — ve 4096). Kuralları hello öncelik sırasına göre değerlendirilir. 100 önceliğine sahip bir kural 200 önceliğine sahip bir kural önce değerlendirilir.

Tüm NSG'ler bir varsayılan kurallar kümesini içerir. Merhaba varsayılan kurallar silinemez ancak hello en düşük öncelik atandığı için oluşturduğunuz hello kurallarıyla kılınabilir.

- **Sanal ağ** - kaynaklanan trafiği ve sanal ağ içinde bitiş hem gelen ve giden yönlerde izin verilir.
- **Internet** - giden trafiğe izin verilir, ancak gelen trafik engellenir.
- **Yük Dengeleyici** -izin Azure'nın yük dengeleyici tooprobe hello durumunu VM'ler ve rol örnekleri. Yük dengelenmiş bir küme kullanmıyorsanız bu kuralı geçersiz kılabilirsiniz.

### <a name="create-network-security-groups"></a>Ağ güvenlik grupları oluşturma

Merhaba aynı ağ güvenlik grubu oluşturulan hello kullanarak bir VM olarak zaman [az vm oluşturma](/cli/azure/vm#create) komutu. Bunu yaparken hello NSG hello VM'ler ağ arabirimiyle ilişkilendirilmiş ve bir NSG kuralı bağlantı noktası otomatik olarak oluşturulan tooallow trafiğine *22* herhangi bir kaynaktan. Bu öğreticide daha önce ön uç VM ile otomatik olarak oluşturulan ön uç NSG hello hello. Bir NSG kuralı da otomatik olarak oluşturulan için bağlantı noktası 22 oluştu. 

Bazı durumlarda yararlı toopre olabilir-zaman varsayılan SSH kuralları oluşturulmaması gerektiğini veya hello NSG ekli tooa alt zaman olmalıdır gibi bir NSG oluşturun. 

Kullanım hello [az ağ nsg oluşturma](/cli/azure/network/nsg#create) komutu toocreate bir ağ güvenlik grubu.

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

Merhaba NSG tooa ağ arabirimi ilişkilendirme yerine bir alt ağ ile ilişkili. Bu yapılandırmada, ekli toohello alt VM hello NSG kuralları devralır.

Merhaba mevcut alt adlı güncelleştirme *mySubnetBackEnd* ile yeni NSG hello.

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

Ekli toohello olan bir sanal makine, şimdi oluşturmak *mySubnetBackEnd*. Bu hello fark `--nsg` bağımsız değişkeni boş çift tırnak işareti değerine sahip. Bir NSG'yi hello VM ile oluşturulan toobe gerekmez. Merhaba VM ile arka uç NSG önceden oluşturulmuş hello korumalı ekli toohello arka uç alt ağıdır. Bu NSG toohello VM geçerlidir. Ayrıca, bu hello burada fark `--public-ip-address` bağımsız değişkeni boş çift tırnak işareti değerine sahip. Bu yapılandırma, bir ortak IP adresi olmadan bir VM oluşturur. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a>Gelen trafiği güvenli

Merhaba ön uç VM oluşturulduğunda, bir NSG kuralı bağlantı noktası 22 tooallow gelen trafiği oluşturuldu. Bu kural, SSH bağlantıları toohello VM sağlar. Bu örnekte, trafiğin de bağlantı noktası izin verilmesi gerektiğini *80*. Bu yapılandırma VM hello üzerinde erişilen web uygulama toobe sağlar.

Kullanım hello [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create) komutu toocreate bağlantı noktası için bir kural *80*.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

Merhaba ön uç VM artık yalnızca bağlantı noktası üzerinde erişilebilir *22* ve bağlantı noktası *80*. Diğer tüm gelen trafiği hello ağ güvenlik grubu engellendi. Yararlı toovisualize hello NSG kuralı yapılandırmaları olabilir. Dönüş hello NSG kural hello yapılandırmayla [az ağ kuralı listesi](/cli/azure/network/nsg/rule#list) komutu. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

Çıktı:

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a>VM tooVM trafiği güvenli

Ağ güvenlik grubu kuralları da VM'ler arasında uygulayabilirsiniz. Bu örnekte, ön uç VM ile toocommunicate gereken hello hello arka uç VM bağlantı noktasında *22* ve *3306*. Bu yapılandırma SSH bağlantılara izin ön uç VM hello ve ayrıca hello ön uç VM toocommunicate arka uç MySQL veritabanına sahip bir uygulama ver. Diğer tüm trafik hello ön uç ve arka uç sanal makineler arasında engellenmelidir.

Kullanım hello [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create) komutu toocreate bağlantı noktası 22 için bir kural. Bu hello fark `--source-address-prefix` bağımsız değişken değerini belirtir *10.0.1.0/24*. Bu yapılandırma, yalnızca hello ön uç alt ağından gelen trafiği NSG hello izin verildiğini sağlar.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

Şimdi 3306 noktasından MySQL trafiği için bir kural ekleyin.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

Nsg'ler bir varsayılan kural izin verme olduğundan son olarak, tüm hello VM'ler arasında aynı trafiği sanal ağ, bir kural oluşturulabilir hello arka uç Nsg'ler tooblock için tüm trafiği. Burada bu hello fark `--priority` değerini verilen *300*, her ikisi de NSG ve MySQL kuralları hello daha düşük olduğu. Bu yapılandırma, SSH ve MySQL trafiği NSG hello izin verilir sağlar.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

Merhaba arka uç VM artık yalnızca bağlantı noktası üzerinde erişilebilir *22* ve bağlantı noktası *3306* hello ön uç alt ağından. Diğer tüm gelen trafiği hello ağ güvenlik grubu engellendi. Yararlı toovisualize hello NSG kuralı yapılandırmaları olabilir. Dönüş hello NSG kural hello yapılandırmayla [az ağ kuralı listesi](/cli/azure/network/nsg/rule#list) komutu. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

Çıktı:

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide oluşturduğunuz ve Azure ağları ilgili toovirtual makineler olarak güvenli. Şunları öğrendiniz:

> [!div class="checklist"]
> * Sanal ağ dağıtma
> * Bir alt ağ içinde bir sanal ağ oluşturma
> * Sanal makineler tooa alt ağ ekleme
> * Sanal makine ortak IP adreslerini yönetin
> * Gelen Internet trafiği güvenli
> * VM tooVM trafiği güvenli

Azure Yedekleme'yi kullanarak sanal makinelerde verilerin güvenliğini sağlama hakkında toohello sonraki öğretici toolearn ilerleyin. 

> [!div class="nextstepaction"]
> [Azure'daki Linux sanal makineleri yedekleyin](./tutorial-backup-vms.md)
