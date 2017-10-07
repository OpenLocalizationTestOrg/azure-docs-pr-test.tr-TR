---
title: "aaaMove bir VM'ye (Klasik) veya Bulut Hizmetleri rol örneği tooa farklı alt ağ - Azure PowerShell | Microsoft Docs"
description: "Bilgi nasıl toomove VM'ler (Klasik) ve bulut Hizmetleri rolü örnekleri PowerShell kullanarak tooa farklı alt ağ."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: de4135c7-dc5b-4ffa-84cc-1b8364b7b427
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8d2de56f42a91be4a665414ea9641ffd46588fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-tooa-different-subnet-using-powershell"></a>Bir VM'yi (Klasik) veya PowerShell kullanarak bulut Hizmetleri rol örneği tooa farklı alt ağ taşıma
PowerShell toomove, VM'lerin (Klasik) bir alt ağ tooanother hello kullanabileceğiniz aynı sanal ağ (VNet). Rol örnekleri hello CSCFG dosyası düzenleme yerine PowerShell kullanarak taşınabilir.

> [!NOTE]
> Bu makalede toomove VM'ler yalnızca hello Klasik dağıtım modeli nasıl dağıtılacağını açıklar.
> 
> 

Neden VM'ler tooanother alt taşıma? Alt ağ geçiş olduğunda yararlı hello eski alt ağı çok küçük ve son genişletilemiyor o alt ağdaki sanal makineleri çalıştıran tooexisting. Bu durumda, yeni, büyük bir alt ağ oluşturmak ve hello VM'ler toohello yeni alt ağ geçirmek ardından geçiş tamamlandıktan sonra eski boş alt hello silebilirsiniz.

## <a name="how-toomove-a-vm-tooanother-subnet"></a>Nasıl toomove VM tooanother alt ağı
bir VM toomove Merhaba örneği aşağıda şablon olarak kullanıp hello kümesi AzureSubnet PowerShell cmdlet'ini çalıştırın. Merhaba aşağıdaki örnekte, biz TestVM mevcut alt ağ üzerinden, taşıdığınız tooSubnet-2. Ortamınızı emin tooedit hello örnek tooreflect olabilir. Her bir yordam bir parçası olarak hello güncelleştirme-AzureVM cmdlet'ini çalıştırdığınızda, hello güncelleştirme işleminin bir parçası, VM başlayacaktır unutmayın.

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

VM için statik iç özel IP belirtilmişse, bu ayarı hello VM tooa yeni alt taşımadan önce tooclear gerekir. Bu durumda, hello aşağıdakileri kullanın:

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="toomove-a-role-instance-tooanother-subnet"></a>bir rol örneği tooanother alt toomove
bir rol örneği toomove hello CSCFG dosyasını düzenleyin. Merhaba aşağıdaki örnekte, biz "Role0" sanal ağında taşıyor *vnetname adlı* mevcut alt ağdan çok*alt ağ-2*. Merhaba rol örneği zaten dağıtılmış olduğundan, hello alt ağ adı yalnızca değiştireceğiz = alt ağ-2. Ortamınızı emin tooedit hello örnek tooreflect olabilir.

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
