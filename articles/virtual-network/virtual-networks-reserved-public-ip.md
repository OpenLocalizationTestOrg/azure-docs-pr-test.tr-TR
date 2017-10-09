---
title: "aaaManage Azure ayrılmış IP adresi (Klasik) - PowerShell | Microsoft Docs"
description: "Ayrılmış IP adresleri (Klasik) anlamak ve nasıl toomanage bunları PowerShell kullanarak."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: c0a77b2ab8b1ab9bef6015c903eb735ea4358a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reserved-ip-addresses-classic"></a>Ayrılmış IP adresleri (Klasik)

> [!div class="op_single_selector"]
> * [Azure portal](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI](virtual-network-deploy-static-pip-arm-cli.md)
> * [Şablon](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (Klasik)](virtual-networks-reserved-public-ip.md)

Azure'daki IP adresleri iki kategoriye ayrılır: dinamik ve ayrılmış. Azure tarafından yönetilen ortak IP adresleri, varsayılan olarak dinamik. Bu IP adresi (VIP) verilen bulut hizmeti için kullanılan hello anlamına gelir veya tooaccess kaynakları kapatıldı veya durduruldu (serbest bırakıldığında) bir VM veya rol örneğine doğrudan (ILPIP) zaman tootime ' değiştirebilirsiniz.

değiştirmesini tooprevent IP adresleri, bir IP adresi ayırabilirsiniz. Ayrılmış IP'ler sağlayarak bu hello IP adresi kalır kaynakları kapatmak gibi aynı hello veya durduruldu (serbest bırakıldığında) hello bulut hizmeti için yalnızca bir VIP olarak kullanılabilir. Ayrıca, bir VIP tooa ayrılmış IP adresi olarak kullanılan varolan dinamik IP dönüştürebilirsiniz.

> [!IMPORTANT]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Bir statik genel IP adresini kullanarak tooreserve nasıl hello öğrenin [Resource Manager dağıtım modeli](virtual-network-ip-addresses-overview-arm.md).

IP hakkında daha fazla toolearn adresleri Azure'da, hello okuma [IP adreslerini](virtual-network-ip-addresses-overview-classic.md) makalesi.

## <a name="when-do-i-need-a-reserved-ip"></a>Ayrılmış IP olduğunda gerekiyor mu?
* **IP hello tooensure aboneliğinizde ayrılmış istediğiniz**. Aboneliğiniz hiçbir koşulda tooreserve serbest bırakılmaz bir IP adresi istiyorsanız, ayrılmış bir genel IP kullanmanız gerekir.  
* **Bulut hizmetiniz ile IP toostay bile çapraz durduruldu veya durumu (VM'ler) serbest istediğiniz**. Değişmez bir IP adresi kullanarak erişilen, hizmet toobe istiyorsanız bile hello VM bulut hizmeti kapatıldığından veya (serbest bırakıldığında) durdurun.
* **Azure giden trafiği tahmin edilebilir bir IP adresi kullanan tooensure istediğiniz**. Şirket içi, yapılandırılmış güvenlik duvarı tooallow yalnızca trafiğinizi belirli IP adresleri olabilir. Bir IP ayırarak hello kaynak IP bilmeniz adres ve tooan IP değişikliği, güvenlik duvarı kuralları tooupdate olması gerekmez.

## <a name="faq"></a>SSS
1. Tüm Azure hizmetlerini bir ayrılmış IP kullanabilir miyim? <br>
    Hayır. Ayrılmış IP'ler yalnızca VM'ler ve bulut hizmeti örnek rolleriniz VIP kullanıma sunulan için kullanılabilir.
2. Kaç tane ayrılmış IP'ler sahip olabilir miyim? <br>
    Merhaba Ayrıntılar için bkz [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) makalesi.
3. Herhangi bir ücret için ayrılmış IP'ler var mı? <br>
    Bazen. Merhaba fiyatlandırma ayrıntıları için bkz: [ayrılmış IP adresi fiyatlandırma ayrıntıları](http://go.microsoft.com/fwlink/?LinkID=398482) sayfası.
4. Bir IP adresi nasıl yedek? <br>
    PowerShell hello kullanabileceğiniz [Azure Yönetimi REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), veya hello [Azure portal](https://portal.azure.com) tooreserve bir Azure bölgesindeki bir IP adresi. Ayrılmış bir IP adresi ilişkili tooyour abonelik değil.
5. Benzeşim grubu tabanlı sanal ağlar ile ayrılmış bir IP kullanabilir miyim? <br>
    Hayır. Ayrılmış IP'ler yalnızca Bölgesel sanal ağlar desteklenir. Ayrılmış IP, benzeşim gruplarıyla ilişkili sanal ağlar için desteklenmez. Merhaba VNet bir bölge veya benzeşim grubu ile ilişkilendirme hakkında daha fazla bilgi için bkz: [hakkında bölgesel sanal ağlara ve benzeşim grupları](virtual-networks-migrate-to-regional-vnet.md) makalesi.

## <a name="manage-reserved-vips"></a>Ayrılmış VIP'ler yönetme

Yüklenmesini ve PowerShell hello hello adımları tamamlayarak yapılandırılmış [yükleyin ve PowerShell yapılandırma](/powershell/azure/overview) makalesi. 

Ayrılmış IP'ler kullanmadan önce tooyour abonelik eklemeniz gerekir. toocreate genel IP hello havuzundan ayrılmış IP adresleri hello bulunan *Orta ABD* konumu, hello aşağıdaki komutu çalıştırın:

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

Ancak, IP yüklenmekte olan belirtemezsiniz fark ayrılmış. tooview hangi IP adresleri, aboneliğinizde hello aşağıdaki PowerShell komutunu çalıştırın, ayrılmış ve fark hello değerlerini *Reservedıpname* ve *adres*:

```powershell
Get-AzureReservedIP
```

Beklenen çıktı:

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
>PowerShell ile ayrılmış bir IP adresi oluşturduğunuzda, bir kaynak grubu toocreate hello ayrılmış IP belirtemezsiniz. Bir kaynak grubu içine adlı azure yerler *varsayılan ağ* otomatik olarak. Hello kullanarak hello ayrılmış IP oluşturursanız [Azure portal](http://portal.azure.com), seçtiğiniz herhangi bir kaynak grubu belirtebilirsiniz. Merhaba ayrılmış IP bir kaynak grubunda dışında oluşturursanız, *varsayılan ağ* başvuru her ancak hello IP komutlarıyla gibi ayrılmış `Get-AzureReservedIP` ve `Remove-AzureReservedIP`, hello adı başvurmalıdır*Grup kaynak grubu adı ayrılmış-IP-name*.  Adlı bir ayrılmış IP oluşturursanız, örneğin, *myReservedIP* bir kaynak grubunda adlı *myResourceGroup*, hello ayrılmış IP olarak hello adını başvurmalıdır *Grup myResourceGroup myReservedIP*.   

Bir IP ayrılmış sonra onu silene kadar ilişkili tooyour abonelik kalır. toodelete ayrılmış bir IP aşağıdaki PowerShell komutunu çalıştırma hello:

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-hello-ip-address-of-an-existing-cloud-service"></a>Var olan bir bulut hizmetinin başlangıç IP adresi ayırın
Merhaba ekleyerek, var olan bir bulut hizmetini hello IP adresi ayırabilirsiniz `-ServiceName` parametresi. bir bulut hizmeti tooreserve hello IP adresini *TestService* hello içinde *Orta ABD* konumu, hello aşağıdaki PowerShell komutunu çalıştırın:

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-tooa-new-cloud-service"></a>Ayrılmış IP tooa yeni bir bulut hizmeti ilişkilendirme
Hello aşağıdaki betiği yeni bir ayrılmış IP oluşturur, ardından tooa adlı yeni bulut hizmeti ilişkilendirir *TestService*.

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> Bir bulut hizmeti ile ayrılmış bir IP toouse oluşturduğunuzda, hala toohello VM başvurabilmek *VIP:&lt;bağlantı noktası numarası >* gelen iletişimi için. IP ayırma toohello VM doğrudan bağlanabilirsiniz anlamına gelmez. Merhaba ayrılmış IP toohello bulut atanmış VM dağıtılan için o hello hizmet. Tooconnect tooa VM IP tarafından doğrudan isterseniz, bir örnek düzeyinde ortak IP tooconfigure gerekir. Örnek düzeyinde ortak IP tooyour VM doğrudan atanmış (bir ILPIP olarak adlandırılır) genel IP türüdür. Ayrılamaz. Daha fazla bilgi için hello okuma [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) makalesi.
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a>Ayrılmış IP çalışan dağıtımdan kaldırın
tooremove ayrılmış IP hello aşağıdaki PowerShell komutunu çalıştırın tooa yeni bulut hizmeti, ekledi:

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> Ayrılmış bir IP adresinden çalışan bir dağıtımını kaldırma hello ayırma aboneliğinizden kaldırmaz. Yalnızca aboneliğiniz başka bir kaynak tarafından kullanılan hello IP toobe serbest bırakır.
> 

## <a name="associate-a-reserved-ip-tooa-running-deployment"></a>Dağıtım çalıştıran ayrılmış bir IP tooa ilişkilendirme
Merhaba aşağıdaki komutları adlı bir bulut hizmeti Oluştur *TestService2* adlı yeni bir VM ile *TestVM2*. ayrılmış IP'si adlı Hello varolan *MyReservedIP* ilişkili toohello bulut hizmeti olduğundan.

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-tooa-cloud-service-by-using-a-service-configuration-file"></a>Hizmet yapılandırma dosyası kullanarak bir ayrılmış IP tooa bulut hizmeti ilişkilendirin
Ayrıca, bir hizmet yapılandırma (CSCFG) dosyası kullanarak bir ayrılmış IP tooa bulut hizmeti ilişkilendirebilirsiniz. Merhaba aşağıdaki örnek xml nasıl tooconfigure bir bulut hizmeti toouse ayrılmış bir VIP adlı gösterir *MyReservedIP*:

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a>Sonraki adımlar
* Anlamak nasıl [IP adresleme](virtual-network-ip-addresses-overview-classic.md) hello Klasik dağıtım modelinde çalışır.
* Hakkında bilgi edinin [ayrılmış özel IP adresi](virtual-networks-reserved-private-ip.md).
* Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP) adresleri](virtual-networks-instance-level-public-ip.md).

