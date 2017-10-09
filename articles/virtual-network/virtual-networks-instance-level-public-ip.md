---
title: "aaaAzure örnek düzeyinde ortak IP (Klasik) adresleri | Microsoft Docs"
description: "Örnek düzeyinde ortak IP (ILPIP) adresleri anlamak ve nasıl toomanage bunları PowerShell kullanarak."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 07eef6ec-7dfe-4c4d-a2c2-be0abfb48ec5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 832143ee6fdd80b634e1cebfddc759a8cacda583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="instance-level-public-ip-classic-overview"></a>Örnek düzeyinde ortak IP (Klasik) genel bakış
Bir örnek düzeyinde ortak IP (ILPIP), VM veya rol örneğine bulunan toohello bulut hizmeti yerine tooa VM veya Bulut Hizmetleri rol örneği doğrudan atayabilir genel bir IP adresi ' dir. Bir ILPIP tooyour bulut hizmetine atanan hello sanal IP (VIP) hello yerini almaz. Bunun yerine, tooconnect kullanabileceğiniz ek bir IP adresi olduğundan doğrudan tooyour VM'deki veya rol örneği.

> [!IMPORTANT]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft, VM'ler Resource Manager aracılığıyla oluşturma önerir. Anladığınızdan emin olun nasıl [IP adreslerini](virtual-network-ip-addresses-overview-classic.md) Azure içinde çalışır.

![ILPIP VIP arasındaki fark](./media/virtual-networks-instance-level-public-ip/Figure1.png)

Şekil 1'de gösterildiği gibi hello bulut hizmeti, bir VIP kullanarak erişildiğinde, başlangıç sırasında tek tek sanal makineleri normalde VIP kullanılarak erişilir:&lt;bağlantı noktası numarası&gt;. Bir ILPIP tooa atayarak, VM olabilir belirli VM, doğrudan bu IP adresi kullanılarak erişilir.

Azure'da bulut hizmeti oluşturduğunuzda, karşılık gelen DNS A kayıtlarını otomatik olarak tooallow erişim toohello hizmeti bir tam etki alanı adı (FQDN) aracılığıyla hello gerçek VIP kullanmak yerine oluşturulur. Merhaba erişim toohello VM'deki veya rol örneğindeki FQDN DEĞERİNE göre hello ILPIP yerine sağlayan bir ILPIP için aynı işlem gerçekleşir. Örneğin, adlı bir bulut hizmeti oluşturursanız, *contosoadservice*, ve adında bir web rolü yapılandırma *contosoweb* iki örnekleriyle A aşağıdaki Azure yazmaçlar hello kayıtları hello örnekleri için:

* contosoweb\_IN_0.contosoadservice.cloudapp.net
* contosoweb\_IN_1.contosoadservice.cloudapp.net 

> [!NOTE]
> Her VM veya rol örneği için yalnızca bir ILPIP atayabilirsiniz. Abonelik başına too5 ILPIPs kullanabilirsiniz. ILPIPs multi-NIC VM'ler için desteklenmez.
> 
> 

## <a name="why-would-i-request-an-ilpip"></a>Bir ILPIP isteme neden?
Merhaba bulut kullanmak yerine VIP toobe mümkün tooconnect tooyour VM istediğiniz veya rol örneği bir IP adresi tarafından atanan doğrudan tooit, hizmet:&lt;bağlantı noktası numarası&gt;, VM veya rol örneği için bir ILPIP isteyin.

* **Etkin FTP** -ILPIP tooa VM atayarak onu herhangi bir bağlantı noktasında trafik alabilir. Uç noktaları hello VM tooreceive trafiği için gerekli değildir.  (Https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) [FTP Protokolü genel bakış] hello FTP Protokolü hakkında ayrıntılı bilgi için bkz.
* **Giden IP** - VM hello giden trafiği eşlenen toohello hello kaynağı olarak ILPIP ve hello ILPIP benzersiz olarak tanımlayan hello VM tooexternal varlıklar.

> [!NOTE]
> Geçmiş Hello içinde bir ILPIP adresi başvurulan tooas genel bir IP (PIP) adresi oluştu.
> 

## <a name="manage-an-ilpip-for-a-vm"></a>Bir VM için bir ILPIP yönetme
görevleri aşağıdaki hello toocreate, Ata ve Kaldır vm'lerden ILPIPs etkinleştirin:

### <a name="how-toorequest-an-ilpip-during-vm-creation-using-powershell"></a>Nasıl toorequest PowerShell kullanarak VM oluşturma sırasında bir ILPIP
PowerShell Betiği aşağıdaki hello adlı bir bulut hizmeti oluşturur *FTPService*, Azure'dan bir görüntü alır, adlandırılmış bir VM'nin oluşturur *FTPInstance* bir ILPIP kümeleri hello VM toouse alınan hello görüntü kullanma ve hello VM toohello yeni hizmet ekler:

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-tooretrieve-ilpip-information-for-a-vm"></a>Nasıl bir VM için tooretrieve ILPIP bilgileri
tooview hello VM oluşturulan hello önceki komut dosyasıyla ILPIP bilgileri hello için hello aşağıdaki PowerShell komutunu çalıştırın ve başlangıç değerleri uyun *Publicıpaddress* ve *PublicIPName*:

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

Beklenen çıktı:
 
    DeploymentName              : FTPService
    Name                        : FTPInstance
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : ReadyRole
    IpAddress                   : 100.74.118.91
    InstanceStateDetails        : 
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : FTPInstance
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : FTPInstance
    AvailabilitySetName         : 
    DNSName                     : http://ftpservice888.cloudapp.net/
    Status                      : ReadyRole
    GuestAgentStatus            :   Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 104.43.142.188
    PublicIPName                : ftpip
    NetworkInterfaces           : {}
    ServiceName                 : FTPService
    OperationDescription        : Get-AzureVM
    OperationId                 : 568d88d2be7c98f4bbb875e4d823718e
    OperationStatus             : OK

### <a name="how-tooremove-an-ilpip-from-a-vm"></a>Nasıl tooremove bir VM'den bir ILPIP
tooremove hello ILPIP toohello VM hello aşağıdaki PowerShell komutunu çalıştırın hello önceki betikte eklendi:

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-tooadd-an-ilpip-tooan-existing-vm"></a>Nasıl tooadd ILPIP tooan var olan VM
tooadd ILPIP toohello önceki, hello komut dosyası kullanılarak oluşturulan VM hello aşağıdaki komutu çalıştırın:

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a>Bulut Hizmetleri rol örneği için bir ILPIP yönetme

tooadd ILPIP tooa bulut Hizmetleri rol örneği, aşağıdaki adımları tam hello:

1. Merhaba tamamlayarak hello bulut hizmeti hello adımları için hello .cscfg dosyasını indirin [tooConfigure Cloud Services nasıl](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) makale.
2. Merhaba ekleyerek güncelleştirme hello .cscfg dosyası `InstanceAddress` öğesi. Merhaba aşağıdaki örnek ekler adlı bir ILPIP *MyPublicIP* adlı tooa rol örneği *WebRole1*: 

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ILPIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
          <ConfigurationSettings>
        <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
          </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <InstanceAddress roleName="WebRole1">
        <PublicIPs>
          <PublicIP name="MyPublicIP" domainNameLabel="MyPublicIP" />
            </PublicIPs>
          </InstanceAddress>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>
    ```
3. Merhaba tamamlayarak hello bulut hizmeti hello adımları hello .cscfg dosyasını karşıya [tooConfigure Cloud Services nasıl](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) makale.

## <a name="next-steps"></a>Sonraki adımlar
* Anlamak nasıl [IP adresleme](virtual-network-ip-addresses-overview-classic.md) hello Klasik dağıtım modelinde çalışır.
* Hakkında bilgi edinin [ayrılmış IP'ler](virtual-networks-reserved-public-ip.md).
