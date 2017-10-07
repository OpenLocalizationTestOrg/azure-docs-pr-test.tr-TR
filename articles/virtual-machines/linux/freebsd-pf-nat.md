---
title: "aaaUse FreeBSD'ın paket filtresi toocreate bir Güvenlik Duvarı'nda Azure | Microsoft Docs"
description: "Bilgi nasıl toodeploy NAT FreeBSD'ın kullanarak güvenlik duvarı PF azure'da."
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/20/2017
ms.author: kyliel
ms.openlocfilehash: 3d3a5dde2ca03ba6fc384581c786f5eb746e6d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-freebsds-packet-filter-toocreate-a-secure-firewall-in-azure"></a>Nasıl toouse FreeBSD'ın paket filtresi toocreate azure'da güvenli bir güvenlik duvarı
Bu makalede tanıtılır nasıl toodeploy ortak web sunucusu senaryo için Azure Resource Manager şablonu aracılığıyla FreeBSD'ın Packer filtresini kullanarak bir NAT güvenlik duvarı.

## <a name="what-is-pf"></a>PF nedir?
PF (paket filtresi, ayrıca pf yazılan) bir BSD lisanslı durum bilgisi olan paket filtre saldırısından için yazılım merkezi bir parçası olarak bilinir. PF beri hızlı bir şekilde gelişmiştir ve artık kullanılabilir diğer güvenlik duvarları üzerinden çeşitli avantajları vardır. Ağ adresi çevirisi (NAT) günden itibaren ardından Paket Zamanlayıcısı'nı PF içinde olan ve etkin kuyruk yönetimi tümleşik PF yapılarak hello ALTQ tümleştirme, PF'ın yapılandırması aracılığıyla yapılandırılabilir. Yük devretme ve artıklık, oturum kimlik doğrulaması ve ftp proxy tooease saldırısından hello zor FTP Protokolü, authpf pfsync ve CARP gibi özellikleri de PF. genişletilmiş Kısacası, PF güçlü ve zengin bir Güvenlik Duvarı ' dir. 

## <a name="get-started"></a>başlarken
Web sunucuları için hello bulutta güvenli bir güvenlik duvarını ayarı ilgilendiğiniz sonra başlayalım durumunda. Bu Azure Resource Manager şablonu tooset ağ topolojinizi kullanılan hello komut uygulayabilir.
PF ve iki FreeBSD sanal makineye yüklenmiş ve yapılandırılmış hello Nginx web sunucusu ile kullanarak NAT /redirection gerçekleştiren hello Azure Resource Manager şablonu FreeBSD sanal makine kurun. Ayrıca tooperforming NAT hello iki web sunucuları için çıkış trafiği, hello NAT/yeniden yönlendirme sanal makine HTTP isteklerini karşılar ve toohello iki web sunucusu hepsini şekilde yönlendirir. Merhaba VNet hello özel yönlendirilemeyen IP adresi alanı 10.0.0.2/24 kullanır ve hello şablon hello parametrelerini değiştirebilirsiniz. Hello Azure Resource Manager şablonu toooverride Azure varsayılan yolların hello hedef IP adresine göre tekil yollar koleksiyonudur tüm VNet kullanılan hello için yol tablosu da tanımlar. 

![pf_topology](./media/freebsd-pf-nat/pf_topology.jpg)
    
### <a name="deploy-through-azure-cli"></a>Azure CLI aracılığıyla dağıtma
Merhaba son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login). [az group create](/cli/azure/group#create) ile bir kaynak grubu oluşturun. Merhaba aşağıdaki örnekte oluşturur bir kaynak grubu adı `myResourceGroup` hello içinde `West US` konumu.

```azurecli
az group create --name myResourceGroup --location westus
```

Ardından, hello şablonu dağıtmak [pf freebsd Kurulum](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup) ile [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create). Karşıdan [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/pf-freebsd-setup/azuredeploy.parameters.json) altında hello aynı yol ve kendi kaynak değerleri aşağıdaki gibi tanımlayın `adminPassword`, `networkPrefix`, ve `domainNamePrefix`. 

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeploymentName \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/pf-freebsd-setup/azuredeploy.json \
    --parameters '@azuredeploy.parameters.json' --verbose
```

Yaklaşık beş dakika sonra hello bilgilerinin alırsınız `"provisioningState": "Succeeded"`. Ssh toohello ön uç VM (NAT) yapabilecekleriniz sonra veya hello genel IP adresi veya hello ön uç VM (NAT) FQDN'sini kullanarak bir tarayıcıda Nginx web sunucusuna erişim. Merhaba aşağıdaki örnek FQDN ve toohello ön uç VM (NAT) hello atanan genel IP adresi listeler `myResourceGroup` kaynak grubu. 

```azurecli
az network public-ip list --resource-group myResourceGroup
```
    
## <a name="next-steps"></a>Sonraki adımlar
Azure'da kendi NAT yukarı tooset istiyor musunuz? Kaynak, ücretsiz ancak güçlü açılsın mı? Ardından PF iyi bir seçimdir. Merhaba şablonunu kullanarak [pf freebsd Kurulum](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup), hepsini bir kez deneme yük dengeleme FreeBSD'ın kullanarak yalnızca bir NAT güvenlik duvarı yukarı beş dakika tooset gerekir PF ortak web sunucusu senaryosu için azure'da. 

Azure'da FreeBSD toolearn hello sunulması istiyorsanız, çok başvurmak[Azure ile ilgili giriş tooFreeBSD](freebsd-intro-on-azure.md).

Tooknow PF hakkında daha fazla bilgi istiyorsanız, çok başvuran[FreeBSD el kitabı](https://www.freebsd.org/doc/handbook/firewalls-pf.html) veya [PF-Kullanıcı Kılavuzu](https://www.freebsd.org/doc/handbook/firewalls-pf.html).
