---
title: "birden çok NIC - Azure CLI 2.0'yle bir VM'yi aaaCreate | Microsoft Docs"
description: "Nasıl toocreate kullanarak birden çok NIC ile VM hello Azure CLI 2.0 öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac0291a978e2c8682c69104915196cc6c4fcf8dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-20"></a>Bir VM ile birden çok NIC hello Azure CLI 2.0 kullanarak oluşturma

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).  Bu makalede, kullanarak yer almaktadır hello yerine çoğu yeni dağıtımlar için Microsoft önerir hello Resource Manager dağıtım modeli [Klasik dağıtım modeli](virtual-network-deploy-multinic-classic-cli.md).
>

## <a name="create"></a>Merhaba VM oluşturma

Hello Azure CLI 2.0 (Bu makalede) veya hello kullanarak bu görevi tamamlayabilirsiniz [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md). Merhaba değerleri "" Merhaba senaryodan ayarlarla kaynakları izleyin hello adımları hello değişkenleri oluşturun. Ortamınız için uygun şekilde Hello değerlerini değiştirin.

1. Merhaba yüklemek [Azure CLI 2.0](/cli/azure/install-az-cli2) , zaten yüklü değilse.
2. Merhaba hello adımları tamamlayarak Linux VM'ler için bir SSH ortak ve özel anahtar çifti oluşturma [Linux VM'ler için bir SSH ortak ve özel anahtar çifti oluşturma](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. Oturum açma hello komutuyla bir komut kabuğu'ndan `az login`.
4. Bir Linux veya Mac bilgisayarda aşağıdaki hello komut dosyası çalıştırarak Hello VM oluşturun. Merhaba betiği oluşturur bir kaynak grubu, bir sanal ağ (VNet) iki alt ağı, iki NIC ve hello iki NIC ile VM ile bağlı tooit. Merhaba NIC'ler biri bağlı tooone alt ağı ve bir statik genel ve özel IP adresi atanır. Merhaba diğer NIC bağlı toohello diğer alt ağıdır ve özel bir statik IP adresi ve ortak IP adresi atanır. Merhaba NIC, ortak IP adresi, sanal ağ ve VM kaynakları tüm bulunmalıdır hello aynı konumu ve abonelik. Merhaba kaynakları tüm tooexist hello yok ancak aynı kaynak grubunda, yaptıkları komut dosyası izleyen hello.

```bash
#!/bin/sh

RgName="Multi-NIC-VM"
Location="westus"

# Create a resource group.
az group create \
--name $RgName \
--location $Location

# hello address is assigned toohello resource from a pool of IP adresses unique tooeach Azure region. 
# Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists
# hello ranges for each region.

PipName="PIP-WEB"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static

# Create a virtual network with one subnet

VnetName="VNet1"
VnetPrefix="10.0.0.0/16"
VnetSubnet1Name="Front-End"
VnetSubnet1Prefix="10.0.0.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnet1Name \
--subnet-prefix $VnetSubnet1Prefix

# Create a second subnet within hello VNet

VnetSubnet2Name="Back-end"
VnetSubnet2Prefix="10.0.1.0/24"
az network vnet subnet create \
--vnet-name $VnetName \
--resource-group $RgName \
--name $VnetSubnet2Name \
--address-prefix $VnetSubnet2Prefix

# Create a network interface connected tooone of hello subnets. hello NIC is assigned a single dynamic private and
# public IP address by default, but you can instead, assign static addresses, or no public IP address at all.
# You can also assign multiple private or public IP addresses tooeach NIC. toolearn more about IP addressing
# options for NICs, enter hello az network nic create -h command.

Nic1Name="NIC-FE"
PrivateIpAddress1="10.0.0.5"

az network nic create \
--name $Nic1Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress1 \
--public-ip-address $PipName

# Create a second network interface and connect it toohello other subnet. Though multiple NICs attached toohello same
# VM can be connected toodifferent subnets, hello subnets must all be within hello same VNet. Add additional NICs as necessary.

Nic2Name="NIC-BE"
PrivateIpAddress2="10.0.1.5"

az network nic create \
--name $Nic2Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet2Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress2

# Create a VM and attach hello two NICs.

VmName="WEB"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article. Not all VM sizes support
# more than one NIC, so be sure tooselect a VM size that supports hello number of NICs you want tooattach toohello VM.
# You must create hello VM with at least two NICs if you want tooadd more after VM creation. If you create a VM with
# only one NIC, you can't add additional NICs toohello VM after VM creation, regardless of how many NICs hello VM supports.
# hello VM size specified in hello following variable supports two NICs.

VmSize="Standard_DS2"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello output returned by entering the
# az vm image list command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file.

SshKeyValue="~/.ssh/id_rsa.pub"

# Before executing hello following command, add variable names of additional NICs you may have added toohello script that
# you want tooattach toohello VM. If creating a Windows VM, remove hello **ssh-key-value** line and you'll be prompted for
# hello password you want tooconfigure for hello VM.

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $Nic1Name $Nic2Name \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

Ayrıca toocreating iki NIC ile VM, hello komut dosyası oluşturur:
- Tek bir premium disk varsayılan olarak yönetilen, ancak oluşturabileceğiniz hello disk türü için diğer seçeneğiniz vardır. Okuma hello [hello Azure CLI 2.0 kullanarak bir Linux VM oluşturma](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Ayrıntılar için makale.
- Sanal ağı iki alt ağ ve tek bir ortak IP adresi. Alternatif olarak, kullanabileceğiniz *varolan* sanal ağ, alt ağ, NIC veya ortak IP adresi kaynakları. nasıl toouse varolan ağ kaynakları yerine ek kaynakları oluşturma girin toolearn `az vm create -h`.

## <a name = "validate"></a>VM oluşturma ve NIC doğrula

1. Merhaba komutu girin `az resource list --resouce-group Multi-NIC-VM --output table` toosee hello komut dosyası tarafından oluşturulan hello kaynakların listesi. Çıktı döndürülen hello altı kaynakları olmalıdır: iki NIC, bir disk, bir ortak IP adresi, bir sanal ağ ve bir sanal makine.
2. Merhaba komutu girin `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`. Çıktı döndürülen hello hello değeri Not **IPADDRESS** ve o hello değerini **Publicıpallocationmethod** olan *statik*.
3. Merhaba <> kaldırmak komutu aşağıdaki hello çalıştırmadan önce değiştirmek *kullanıcı adı* hello için kullanılan hello adla **kullanıcı adı** hello komut dosyası ve değiştirme değişkeni *IPADDRESS* hello ile **IPADDRESS** hello önceki adımdaki. Çalışma hello şu komutu tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`. 
4. Merhaba toohello VM bağlandıktan sonra çalıştırmak `sudo ifconfig` komutu toosee *eth0* ve *eth1* arabirimleri. Her NIC'nin hello Azure DHCP sunucuları tarafından hello komut dosyasında belirtilen hello statik özel IP adresleri atanmıştır. Merhaba toohello NIC'ler atanan IP ve MAC adreslerinin VM silinmiş hello kadar değiştirmeyin. Bağlantı toohello bilgisayar devre dışı bırakabilirsiniz gibi bir işletim sistemi içinde IP adresleme değiştirmemenizi öneririz. Ağ adresi çevrilen tooand hello özel IP adresinden hello Azure altyapısı tarafından oldukları gibi ortak IP adresleri hello işletim sistemi içinde görünmez.

## <a name= "clean-up"></a>Merhaba VM ve ilişkili kaynakları Kaldır

Üretimde kullanmaz, bu alıştırmada oluşturulan hello kaynakları silmeniz önerilir. Sağlanan sürece ücretler, VM, genel IP adresi ve disk kaynakları uygulanır. Bu alıştırmada, aşağıdaki adımları tam hello sırasında oluşturulan tooremove hello kaynakları:
1. Merhaba çalıştırmak hello kaynak grubunda tooview hello kaynakları `az resource list --resource-group Multi-NIC-VM` komutu.
2. Bu makalede hello komut dosyası tarafından oluşturulan hello kaynakları dışında hello kaynak grubunda hiç kaynak yok onaylayın. 
3. tüm kaynaklar hello çalıştırmak Bu alıştırmada oluşturulan toodelete `az group delete --name Multi-NIC-VM` komutu. Merhaba komut hello kaynak grubu ve içerdiği tüm hello kaynakları siler.

## <a name="next-steps"></a>Sonraki adımlar

Herhangi bir ağ trafiği, bu makaledeki VM oluşturulan hello gelen tooand akabilir. Bir NSG içinde her ağ arabirimi, her alt ağ ya da her ikisini de tooand akabilir hello trafiğini sınırlandırmak gelen ve giden kurallar tanımlayabilirsiniz. Merhaba okuma Nsg'ler hakkında daha fazla toolearn [NSG genel bakış](virtual-networks-nsg.md) makalesi.
