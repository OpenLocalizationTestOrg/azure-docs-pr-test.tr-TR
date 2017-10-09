---
title: "kullanarak bir sanal ağ aaaCreate hello Azure CLI 1.0 | Microsoft Docs"
description: "Azure CLI 1.0 kullanarak bir sanal ağ toocreate hello nasıl öğrenin | Resource Manager."
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f48a8b23a5994164b71c9b51ee8a6810d17f9392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli"></a>Hello Azure CLI kullanarak bir sanal ağ oluşturma

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure'un iki dağıtım modeli vardır: Azure Resource Manager ve klasik. Microsoft, kaynakları hello Resource Manager dağıtım modeli üzerinden oluşturma önerir. Merhaba iki modelleri arasındaki farklar hakkında daha fazla bilgi toolearn hello okuma hello [anlamak Azure dağıtım modelleri](../azure-resource-manager/resource-manager-deployment-model.md) makalesi.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- [Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için
- [Azure CLI 1.0](#create-a-virtual-network) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a>Sanal ağ oluşturma

kullanarak bir sanal ağ toocreate Azure CLI, aşağıdaki adımları tam hello hello:

1. Azure CLI aşağıdaki hello tarafından adımları hello hello yükleyip [hello Azure CLI yükleyip](../cli-install-nodejs.md) makalesi.

2. VNet ve bir alt ağ oluşturun:

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    Beklenen çıktı:
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    Kullanılan parametreler:

   * **--vnet**. Merhaba VNet toobe oluşturulan adı. Bizim senaryomuz için bu *TestVNet* ’tir.
   * **-e (veya--adres alanı)**. VNet adres alanı. Bizim senaryomuz için *192.168.0.0*
   * **-i (veya - CIDR)**. Ağ maskesi CIDR biçiminde. Bizim senaryomuz için *16*.
   * **-n (veya--alt ağ adı**). Merhaba ilk alt ağ adı. Bizim senaryomuz için bu *FrontEnd* ’dir.
   * **-p (veya--alt başlangıç IP'sini)**. Alt ağ veya alt ağ adres alanı için başlangıç IP adresi. Bizim senaryomuz için *192.168.1.0*.
   * **-r (veya--alt ağ CIDR)**. Alt ağ için CIDR biçiminde ağ maskesi. Bizim senaryomuz için *24*.
   * **-l (veya --location)**. Merhaba VNet oluşturulduğu azure bölgesi. Bizim senaryomuz için *Orta ABD*.

3. Bir alt ağ oluşturun:

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    Beklenen çıktı:

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    Kullanılan parametreler:

   * **-t (veya--vnet-ad**. Merhaba hello alt oluşturulacağı Vnet'in adı. Bizim senaryomuz için bu *TestVNet* ’tir.
   * **-n (veya --name)**. Merhaba yeni alt ağ adı. Bizim senaryomuz için *arka uç*.
   * **-a (veya--adres-önek)**. Alt ağ CIDR bloğu. Dört bizim senaryomuz *192.168.2.0/24*.
   
4. Yeni VNet tooview hello özelliklerini hello:

    ```azurecli
    azure network vnet show
    ```
   
    Beklenen çıktı:
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a>Sonraki adımlar

Bilgi nasıl tooconnect:

- Merhaba okuyarak sanal makine (VM) tooa sanal ağ [bir Linux VM oluşturma](../virtual-machines/linux/quick-create-cli.md) makalesi. Merhaba makaleleri hello adımlarda bir VNet ve alt ağ oluşturmak yerine, bir VM'ye mevcut VNet ve alt ağ tooconnect seçebilirsiniz.
- sanal ağ tooother sanal ağlar hello okuyarak hello [sanal ağlara bağlanma](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) makalesi.
- bir siteden siteye sanal özel ağ (VPN) veya expressroute bağlantı hattı kullanarak hello sanal ağ tooan şirket içi ağ. Bilgi hello okuyarak nasıl [bir siteden siteye VPN kullanarak bir VNet tooan şirket içi ağ bağlanmak](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) ve [VNet tooan expressroute bağlantı hattı bağlantı](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).
