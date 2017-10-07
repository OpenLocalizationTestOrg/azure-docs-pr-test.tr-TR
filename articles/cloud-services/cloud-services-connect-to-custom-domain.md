---
title: "bir bulut hizmeti tooa aaaConnect özel etki alanı denetleyicisi | Microsoft Docs"
description: "Bilgi nasıl tooconnect web/çalışan rolleri tooa özel AD etki alanı PowerShell ve AD etki alanı uzantısı kullanma"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1e2d7c87-d254-4e7a-a832-67f84411ec95
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 9540190ccf17c03e55159c6c68429eee29e0a558
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a>Azure bulut Hizmetleri rolleri tooa özel AD etki alanı denetleyicisi Azure'da barındırılan bağlanma
Sanal ağ (VNet) İlk Azure içinde ayarlarsınız. Bir Active Directory etki alanı denetleyicisi (bir Azure sanal makinede barındırılan) toohello VNet sonra ekleyeceğiz. Ardından, biz mevcut bulut hizmeti rolleri toohello VNet önceden oluşturulmuş ekleyin, sonra toohello etki alanı denetleyicisine bağlanma.

Başlamadan önce birkaç şey tookeep unutmayın:

1. Bu öğreticide PowerShell kullanır, böylece Azure PowerShell yüklenmiş olması ve toogo hazır olduğundan emin olun. Azure PowerShell ayar tooget Yardımı'na bakın [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).
2. AD etki alanı denetleyicisi ve Web/çalışan rolü örneklerinizi hello VNet toobe gerekir.

Bu adım adım kılavuz izleyin ve herhangi bir sorunla çalıştırırsanız, bize hello hello makalenin sonunda bir yorum yazın. Birisi tooyou geri alırsınız (Evet, biz yorumları okuma).

Merhaba bulut hizmeti tarafından başvurulan hello ağ olmalıdır bir **Klasik sanal ağ**.

## <a name="create-a-virtual-network"></a>Bir sanal ağ oluşturma
Azure'da hello Azure portal veya PowerShell kullanarak bir sanal ağ oluşturabilirsiniz. Bu öğretici için PowerShell kullanacağız. kullanarak bir sanal ağ toocreate hello Azure portal, bkz: [sanal ağ oluştur](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

```powershell
#Create Virtual Network

$vnetStr =
@"<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
    <VirtualNetworkConfiguration>
    <VirtualNetworkSites>
        <VirtualNetworkSite name="[your-vnet-name]" Location="West US">
        <AddressSpace>
            <AddressPrefix>[your-address-prefix]</AddressPrefix>
        </AddressSpace>
        <Subnets>
            <Subnet name="[your-subnet-name]">
            <AddressPrefix>[your-subnet-range]</AddressPrefix>
            </Subnet>
        </Subnets>
        </VirtualNetworkSite>
    </VirtualNetworkSites>
    </VirtualNetworkConfiguration>
</NetworkConfiguration>
"@;

$vnetConfigPath = "<path-to-vnet-config>"
Set-AzureVNetConfig -ConfigurationPath $vnetConfigPath
```

## <a name="create-a-virtual-machine"></a>Bir Sanal Makine Oluşturun
Merhaba sanal ağ kurmayı tamamladıktan sonra toocreate bir AD etki alanı denetleyicisi gerekir. Bu öğretici için size bir AD etki alanı denetleyicisi üzerinde bir Azure sanal makine ayarlarını yapacak.

toodo Bu, PowerShell komutlarını aşağıdaki hello kullanarak aracılığıyla bir sanal makine oluşturun:

```powershell
# Initialize variables
# VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.

$vnetname = '<your-vnet-name>'
$subnetname = '<your-subnet-name>'
$vmsvc1 = '<your-hosted-service>'
$vm1 = '<your-vm-name>'
$username = '<your-username>'
$password = '<your-password>'
$affgrp = '<your- affgrp>'

# Create a VM and add it toohello Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a>Sanal makine tooa etki alanı denetleyicisine Yükselt
tooconfigure hello sanal makine bir AD etki alanı denetleyicisi toohello VM toolog ve gerekir yapılandırın.

toolog toohello VM içinde kullanım hello komutları aşağıdaki PowerShell aracılığıyla hello RDP dosyasını alabilirsiniz:

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

Toohello VM oturumunuz sonra sanal makineniz aşağıdaki hello adım adım kılavuzu bir AD etki alanı denetleyicisi olarak ayarlamak [nasıl müşteriniz AD etki alanı denetleyicisi yukarı tooset](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).

## <a name="add-your-cloud-service-toohello-virtual-network"></a>Bulut hizmeti toohello sanal ağ ekleme
Ardından, bulut hizmeti dağıtım toohello tooadd gerekir yeni VNet. toodo Bu, Visual Studio kullanarak hello ilgili bölümlerine tooyour cscfg ekleyerek, bulut hizmeti cscfg değiştirebilir veya hello düzenleyiciyi.

```xml
<ServiceConfiguration serviceName="[hosted-service-name]" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="[os-family]" osVersion="*">
    <Role name="[role-name]">
    <Instances count="[number-of-instances]" />
    </Role>
    <NetworkConfiguration>

    <!--optional-->
    <Dns>
        <DnsServers><DnsServer name="[dns-server-name]" IPAddress="[ip-address]" /></DnsServers>
    </Dns>
    <!--optional-->

    <!--VNet settings
        VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.-->
    <VirtualNetworkSite name="[virtual-network-name]" />
    <AddressAssignments>
        <InstanceAddress roleName="[role-name]">
        <Subnets>
            <Subnet name="[subnet-name]" />
        </Subnets>
        </InstanceAddress>
    </AddressAssignments>
    <!--VNet settings-->

    </NetworkConfiguration>
</ServiceConfiguration>
```

Sonraki bulut Hizmetleri projeyi oluşturun ve tooAzure dağıtın. Bulut Hizmetleri paket tooAzure dağıtma ile tooget Yardımı'na bakın [nasıl tooCreate ve bir bulut hizmeti dağıtma](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)

## <a name="connect-your-webworker-roles-toohello-domain"></a>Web/çalışan rolleri toohello etki alanınızın Bağlan
Bulut hizmeti projenizi Azure üzerinde dağıtıldığında, başlangıç AD etki alanı uzantısını kullanarak rol örnekleri toohello özel AD etki alanınızın bağlayın. tooadd hello AD etki alanı uzantısı tooyour mevcut bulut Hizmetleri dağıtımı ve hello özel etki alanına katılma, PowerShell komutlarını aşağıdaki hello yürütün:

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension toohello cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

Ve bu kadar.

Bulut hizmetlerinizi birleştirilmiş tooyour özel etki alanı denetleyicisi olmalıdır. Kullanılabilir farklı seçenekler hakkında daha fazla hello toolearn isterseniz tooconfigure AD etki alanı uzantısını kullanım hello PowerShell nasıl yardımcı olur. Örnekler izleyin birkaç:

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
