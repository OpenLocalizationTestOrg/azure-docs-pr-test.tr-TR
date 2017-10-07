---
title: "bir Azure sanal ağ (Klasik) - ağ yapılandırma dosyası aaaConfigure | Microsoft Docs"
description: "Bilgi nasıl toocreate ve dışarı aktarma, değiştirme ve bir ağ yapılandırma dosyasını içeri sanal ağları (Klasik) değiştirin."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c29b9059-22b0-444e-bbfe-3e35f83cde2f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 009108d4315b4b7146d3f1cf2436ee211d2d89ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a>Bir ağ yapılandırma dosyası kullanarak bir sanal ağ (Klasik) yapılandırma
> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager dağıtım modeli kullanmanızı önerir.

Oluşturun ve bir ağ yapılandırma dosyası hello Azure komut satırı arabirimi (CLI) 1.0 veya Azure PowerShell kullanarak bir sanal ağ (Klasik) yapılandırın. Oluşturma veya bir ağ yapılandırma dosyası kullanarak hello Azure Resource Manager dağıtım modeli aracılığıyla bir sanal ağ değiştiremezsiniz. Hello Azure portal toocreate kullanın veya bir ağ yapılandırma dosyası kullanarak bir sanal ağ (Klasik) değiştirme, kullanabilirsiniz ancak Azure portal toocreate olmadan bir ağ yapılandırma dosyası kullanarak bir sanal ağ (Klasik), hello olamaz.

Oluşturma ve bir ağ yapılandırma dosyası ile bir sanal ağ (Klasik) yapılandırma dışarı aktarma, değiştirme ve hello dosya alma gerektirir.

## <a name="export"></a>Bir ağ yapılandırma dosyası dışarı aktarma

PowerShell veya hello Azure CLI tooexport bir ağ yapılandırma dosyası kullanabilirsiniz. Hello Azure CLI bir json dosyası verirken PowerShell bir XML dosyasına dışarı aktarır.

### <a name="powershell"></a>PowerShell
 
1. [Azure PowerShell'i yükleyin ve tooAzure içinde oturum](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Değiştirme hello dizin (ve onu var olduğundan emin olun) ve hello filename aşağıdaki komut istenen sonra çalışma hello komutu tooexport hello ağ yapılandırma dosyası olarak:

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>Azure CLI 1.0

1. [Hello Azure CLI 1.0 yüklemek](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Azure CLI 1.0 komut isteminden adımları kalan hello tamamlayın.
2. İçinde tooAzure hello girerek oturum `azure login` komutu.
3. Merhaba girerek asm modunda olduğunuzdan emin olun `azure config mode asm` komutu.
4. Değiştirme hello dizin (ve onu var olduğundan emin olun) ve hello filename aşağıdaki komut istenen sonra çalışma hello komutu tooexport hello ağ yapılandırma dosyası olarak:
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a>Oluşturma veya bir ağ yapılandırma dosyasını değiştirme

Bir ağ yapılandırma XML dosyasını (PowerShell kullanırken) veya bir json dosyası (hello Azure CLI kullanırken) dosyasıdır. Merhaba dosyasını bir metin veya XML/json düzenleyicide düzenleyebilirsiniz. Merhaba [ağ yapılandırma dosyası şeması ayarları](https://msdn.microsoft.com/library/azure/jj157100.aspx) makale tüm ayarları için ayrıntılarını içerir. Hello ayarları ek açıklaması için bkz: [sanal ağlar ve ayarları görüntüle](virtual-network-manage-network.md#view-vnet). Merhaba değişiklikleri toohello dosya yapın:

- Uymalıdır hello şema veya içeri aktarma hello ağ yapılandırma dosyası başarısız olur.
- Aboneliğiniz için var olan tüm ağ ayarlarını üzerine yazma, bu nedenle değişiklikler yaparken dikkatli. Örneğin, izleyin hello örnek ağ yapılandırması dosyaları başvuru. Merhaba özgün dosya bulunan iki söyleyin **VirtualNetworkSite** örnekleri ve değişti, hello örneklerde gösterildiği gibi. Merhaba dosyasını içe aktardığınızda, Azure hello için sanal ağ hello siler **VirtualNetworkSite** hello dosyasında kaldırdığınız örneği. Hiçbir kaynak yoktu hello sanal ağında Basitleştirilmiş bu senaryo varsayar gibi olsaydı, hello sanal ağ silinemedi ve hello alma başarısız olurdu.

> [!IMPORTANT]
> Azure göz önünde bulundurur bir şey sahip bir alt tooit olarak dağıtılan **kullanımda**. Bir alt ağ kullanımdayken değiştirilemez. Ağ yapılandırma dosyasında alt ağ bilgilerini değiştirmeden önce değiştirilen değil toohello alt tooa farklı alt dağıtmış olan herhangi bir şey taşıyın. Bkz: [bir VM veya rol örneğine tooa farklı alt taşıma](virtual-networks-move-vm-role-to-subnet.md) Ayrıntılar için.

### <a name="example-xml-for-use-with-powershell"></a>PowerShell ile kullanılmak üzere XML örneği

Merhaba aşağıdaki örnek ağ yapılandırma dosyası adlı bir sanal ağ oluşturur *myVirtualNetwork* bir adres alanı ile *10.0.0.0/16* hello içinde *Doğu ABD* Azure bölge. Merhaba sanal ağ içeren bir alt ağ *mySubnet* bir adres öneki ile *10.0.0.0/24*.

```xml
<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns />
    <VirtualNetworkSites>
      <VirtualNetworkSite name="myVirtualNetwork" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="mySubnet">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

Merhaba ağ yapılandırma dosyasını dışarı aktardığınız hiç içerik içeriyorsa, hello XML hello önceki örnekte kopyalayın ve yeni bir dosyaya yapıştırın.

### <a name="example-json-for-use-with-hello-azure-cli-10"></a>Örnek JSON hello Azure CLI 1.0 ile kullanmak için

Merhaba aşağıdaki örnek ağ yapılandırma dosyası adlı bir sanal ağ oluşturur *myVirtualNetwork* bir adres alanı ile *10.0.0.0/16* hello içinde *Doğu ABD* Azure bölge. Merhaba sanal ağ içeren bir alt ağ *mySubnet* bir adres öneki ile *10.0.0.0/24*.

```json
{
   "VirtualNetworkConfiguration" : {
      "Dns" : "",
      "VirtualNetworkSites" : [
         {
            "AddressSpace" : [ "10.0.0.0/16" ],
            "Location" : "East US",
            "Name" : "myVirtualNetwork",
            "Subnets" : [
               {
                  "AddressPrefix" : "10.0.0.0/24",
                  "Name" : "mySubnet"
               }
            ]
         }
      ]
   }
}
```

Merhaba ağ yapılandırma dosyasını dışarı aktardığınız hiç içerik içeriyorsa, hello json hello önceki örnekte kopyalayın ve yeni bir dosyaya yapıştırın.

## <a name="import"></a>Ağ yapılandırma dosyasını içeri aktarın

PowerShell veya hello Azure CLI tooimport bir ağ yapılandırma dosyası kullanabilirsiniz. PowerShell Hello Azure CLI bir json dosyası alırken bir XML dosyası içeri aktarır. Merhaba alma başarısız olursa, o hello dosya hello ile uyumlu onaylayın [ağ yapılandırma şeması](https://msdn.microsoft.com/library/azure/jj157100.aspx). 

### <a name="powershell"></a>PowerShell
 
1. [Azure PowerShell'i yükleyin ve tooAzure içinde oturum](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Başlangıç dizini ve gerektiğinde komutu aşağıdaki hello dosya değiştirin, ardından hello komutu tooimport hello ağ yapılandırma dosyasını çalıştırın:
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>Azure CLI 1.0

1. [Hello Azure CLI 1.0 yüklemek](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Azure CLI 1.0 komut isteminden adımları kalan hello tamamlayın.
2. İçinde tooAzure hello girerek oturum `azure login` komutu.
3. Merhaba girerek asm modunda olduğunuzdan emin olun `azure config mode asm` komutu.
4. Başlangıç dizini ve gerektiğinde komutu aşağıdaki hello dosya değiştirin, ardından hello komutu tooimport hello ağ yapılandırma dosyasını çalıştırın:

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
