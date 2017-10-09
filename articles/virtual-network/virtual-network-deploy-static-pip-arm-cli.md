---
title: bir statik genel IP adresi - Azure CLI 2.0'yle bir VM'yi aaaCreate | Microsoft Docs
description: "Nasıl toocreate ile bir statik genel IP adresini kullanarak bir VM hello Azure komut satırı arabirimi (CLI) 2.0 öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486060463486462dd8336734a7ad23c4a2cba452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-20"></a>Hello Azure CLI 2.0 kullanarak bir statik genel IP adresiyle bir VM oluşturma

> [!div class="op_single_selector"]
> * [Azure portal](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md)
> * [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [Şablon](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (Klasik)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Bu makalede, Microsoft hello Klasik dağıtım modeli yerine çoğu yeni dağıtımlar için önerir hello Resource Manager dağıtım modeli kullanılarak kapsar.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name = "create"></a>Merhaba VM oluşturma

Hello Azure CLI 2.0 (Bu makalede) veya hello kullanarak bu görevi tamamlayabilirsiniz [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md). Merhaba değerleri "" Merhaba senaryodan ayarlarla kaynakları izleyin hello adımları hello değişkenleri oluşturun. Ortamınız için uygun şekilde Hello değerlerini değiştirin.

1. Merhaba yüklemek [Azure CLI 2.0](/cli/azure/install-az-cli2) , zaten yüklü değilse.
2. Merhaba hello adımları tamamlayarak Linux VM'ler için bir SSH ortak ve özel anahtar çifti oluşturma [Linux VM'ler için bir SSH ortak ve özel anahtar çifti oluşturma](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. Oturum açma hello komutuyla bir komut kabuğu'ndan `az login`.
4. Bir Linux veya Mac bilgisayarda aşağıdaki hello komut dosyası çalıştırarak Hello VM oluşturun. Hello Azure genel IP adresi, sanal ağ, ağ arabirimi ve VM kaynakları tüm bulunmalıdır hello aynı konumu. Merhaba kaynakları tüm tooexist hello yok ancak aynı kaynak grubunda, yaptıkları komut dosyası izleyen hello.

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using hello --allocation-method Static option.
# If you do not specify this option, hello address is allocated dynamically. hello address is assigned toothe
# resource from a pool of IP adresses unique tooeach Azure region. hello DnsName must be unique within the
# Azure location it's created in. Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists hello ranges for each region.

PipName="PIPWEB1"
DnsName="iaasstoryws1"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static \
--dns-name $DnsName

# Create a virtual network with one subnet

VnetName="TestVNet"
VnetPrefix="192.168.0.0/16"
SubnetName="FrontEnd"
SubnetPrefix="192.168.1.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $SubnetName \
--subnet-prefix $SubnetPrefix

# Create a network interface connected toohello VNet with a static private IP address and associate hello public IP address
# resource toohello NIC.

NicName="NICWEB1"
PrivateIpAddress="192.168.1.101"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $SubnetName \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress \
--public-ip-address $PipName

# Create a new VM with hello NIC

VmName="WEB1"

# Replace hello value for hello VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable with a value for *urn* from hello output returned by entering
# hello `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace hello following value with hello path tooyour public key file.
SshKeyValue="~/.ssh/id_rsa.pub"

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $NicName \
--admin-username $Username \
--ssh-key-value $SshKeyValue
# If creating a Windows VM, remove hello previous line and you'll be prompted for hello password you want tooconfigure for hello VM.
```

Ayrıca toocreating VM, hello komut dosyası oluşturur:
- Tek bir premium disk varsayılan olarak yönetilen, ancak oluşturabileceğiniz hello disk türü için diğer seçeneğiniz vardır. Okuma hello [hello Azure CLI 2.0 kullanarak bir Linux VM oluşturma](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Ayrıntılar için makale.
- Sanal ağ, alt ağ, NIC ve ortak IP adresi kaynakları. Alternatif olarak, kullanabileceğiniz *varolan* sanal ağ, alt ağ, NIC veya ortak IP adresi kaynakları. nasıl toouse varolan ağ kaynakları yerine ek kaynakları oluşturma girin toolearn `az vm create -h`.

## <a name = "validate"></a>VM oluşturma ve genel IP adresi doğrula

1. Merhaba komutu girin `az resource list --resouce-group IaaSStory --output table` toosee hello komut dosyası tarafından oluşturulan hello kaynakların listesi. Çıktı döndürülen hello beş kaynakları olmalıdır: ağ arabirimi, disk, genel IP adresi, sanal ağ ve bir sanal makine.
2. Merhaba komutu girin `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`. Çıktı döndürülen hello hello değeri Not **IPADDRESS** ve o hello değerini **Publicıpallocationmethod** olan *statik*.
3. Komutu aşağıdaki hello yürütmeden önce hello <> kaldırmak, değiştirmek *kullanıcıadı* hello için kullanılan hello adla **kullanıcı adı** hello komut dosyası ve değiştirme değişkeni *IPADDRESS* hello ile **IPADDRESS** hello önceki adımdaki. Çalışma hello şu komutu tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`. 

## <a name= "clean-up"></a>Merhaba VM ve ilişkili kaynakları Kaldır

Üretimde kullanmaz, bu alıştırmada oluşturulan hello kaynakları silmeniz önerilir. Sağlanan sürece ücretler, VM, genel IP adresi ve disk kaynakları uygulanır. Bu alıştırmada, aşağıdaki adımları tam hello sırasında oluşturulan tooremove hello kaynakları:

1. Merhaba çalıştırmak hello kaynak grubunda tooview hello kaynakları `az resource list --resource-group IaaSStory` komutu.
2. Bu makalede hello komut dosyası tarafından oluşturulan hello kaynakları dışında hello kaynak grubunda hiç kaynak yok onaylayın. 
3. tüm kaynaklar hello çalıştırmak Bu alıştırmada oluşturulan toodelete `az group delete -n IaaSStory` komutu. Merhaba komut hello kaynak grubu ve içerdiği tüm hello kaynakları siler.

## <a name="next-steps"></a>Sonraki adımlar

Herhangi bir ağ trafiği, bu makaledeki VM oluşturulan hello gelen tooand akabilir. Bir NSG içinde hello ağ arabirimi, hello alt ağ ya da her ikisini de tooand akabilir hello trafiğini sınırlandırmak gelen ve giden kurallar tanımlayabilirsiniz. Merhaba okuma Nsg'ler hakkında daha fazla toolearn [NSG genel bakış](virtual-networks-nsg.md) makalesi.
