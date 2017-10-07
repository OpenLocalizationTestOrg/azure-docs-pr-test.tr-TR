---
title: "aaaStatic iç özel IP - Azure VM - Klasik"
description: "Statik iç IP (Dıps) Anlama ve nasıl toomanage bunları"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 93444c6f-af1b-41f8-a035-77f5c0302bf0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.openlocfilehash: 5abe1c59f2f3ed19bcf56c269dfe57ac32d4f601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a>Nasıl tooset statik iç özel IP adresi (Klasik) PowerShell'i kullanma
Çoğu durumda, sanal makine için statik iç IP adresi toospecify gerekmez. Bir sanal ağdaki sanal makineleri otomatik olarak bir iç IP adresi, belirttiğiniz bir aralıktan alır. Ancak bazı durumlarda, belirli bir VM için bir statik IP adresi belirtme mantıklıdır. Örneğin, VM'yi giderek toorun DNS veya bir etki alanı denetleyicisi olacaktır. Statik iç IP adresi hello VM bile bir Dur/deprovision durumu ile birlikte kalır. 

> [!IMPORTANT]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft en yeni dağıtımların hello kullanmanızı önerir [Resource Manager dağıtım modeli](virtual-networks-static-private-ip-arm-ps.md).
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a>Nasıl belirli bir IP adresi olup olmadığını tooverify
Merhaba, tooverify IP adresi *10.0.0.7* adlı sanal ağ içinde kullanılabilir *TestVnet*hello aşağıdaki PowerShell komutunu çalıştırın ve hello değerini doğrulamak *IsAvailable*:

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> Güvenli bir ortamda yukarıda tootest hello komutu istiyorsanız hello yönergeleri izleyin [bir sanal ağ (Klasik) oluşturmak](virtual-networks-create-vnet-classic-pportal.md) toocreate adlı bir vnet *TestVnet* ve hello kullandığından emin olun  *10.0.0.0/8* adres alanı.
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a>Nasıl toospecify bir VM oluşturulurken statik iç IP
Merhaba aşağıdaki PowerShell komut dosyası adlı yeni bir bulut hizmeti oluşturur *TestService*, Azure'dan bir görüntü alır sonra adlandırılmış bir VM'nin oluşturur *TestVM* hello alınan hello görüntü kullanarak yeni bulut hizmetinde ayarlar hello adlı bir alt ağdaki VM toobe *Subnet-1*ve ayarlar *10.0.0.7* hello VM için statik iç IP olarak:

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a>Nasıl tooretrieve statik iç IP bilgileri bir VM için
VM yukarıdaki hello betiği ile oluşturulan tooview hello statik iç IP bilgileri hello hello aşağıdaki PowerShell komutunu çalıştırın ve başlangıç değerleri uyun *IPADDRESS*:

    Get-AzureVM -Name TestVM -ServiceName TestService

    DeploymentName              : TestService
    Name                        : TestVM
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 10.0.0.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : TestVM
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : rsR2-797
    AvailabilitySetName         : 
    DNSName                     : http://testservice000.cloudapp.net/
    Status                      : Provisioning
    GuestAgentStatus            : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 
    PublicIPName                : 
    NetworkInterfaces           : {}
    ServiceName                 : TestService
    OperationDescription        : Get-AzureVM
    OperationId                 : 34c1560a62f0901ab75cde4fed8e8bd1
    OperationStatus             : OK

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a>Nasıl tooremove bir VM'den statik iç IP
tooremove hello statik iç IP toohello VM yukarıdaki hello betik eklenen hello aşağıdaki PowerShell komutunu çalıştırın:

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a>Nasıl tooadd bir statik iç IP tooan var olan VM
bir statik iç IP toohello komutu aşağıdaki yukarıdaki çalışma hello komut dosyası kullanılarak oluşturulan VM tooadd:

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a>Sonraki adımlar
[Ayrılmış IP](virtual-networks-reserved-public-ip.md)

[Örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md)

[Ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx)

