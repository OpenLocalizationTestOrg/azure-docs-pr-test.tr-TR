---
title: Azure sanal makineleri - PowerShell aaaMultiple IP adreslerinin | Microsoft Docs
description: "Nasıl tooassign birden çok IP adresleri öğrenin PowerShell kullanarak tooa sanal makine | Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c44ea62f-7e54-4e3b-81ef-0b132111f1f8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/24/2017
ms.author: jdial;annahar
ms.openlocfilehash: df54c4386ce13521e660a3e7208c8c1ab1459bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-powershell"></a>PowerShell kullanarak toovirtual makineler birden çok IP adresi atayın

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

Bu makalede nasıl toocreate sanal makineye (VM) üzerinden hello Azure Resource Manager dağıtım modeli PowerShell kullanarak açıklanmaktadır. Birden çok IP adresi hello Klasik dağıtım modeli aracılığıyla oluşturulan tooresources atanamaz. Merhaba okuma Azure dağıtım modelleri hakkında daha fazla toolearn [dağıtım modellerini anlama](../resource-manager-deployment-model.md) makalesi.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Birden çok IP adresiyle bir VM oluşturma

izleyin hello adımlarda hello senaryosunda açıklandığı şekilde nasıl toocreate örneği VM ile birden çok IP adresleri, açıklanmaktadır. Değişken değerleri, uygulamanız için gereken şekilde değiştirin.

1. Bir PowerShell komut istemi açın ve tam hello kalan tek bir PowerShell oturumunda bu bölümdeki adımları. Zaten yüklü ve yapılandırılmış PowerShell sahip değilseniz, tam hello hello adımları [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) makalesi.
2. Oturum açma tooyour hello hesabıyla `login-azurermaccount` komutu.
3. Değiştir *myResourceGroup* ve *westus* bir adı ve seçtiğiniz konum. Bir kaynak grubu oluşturun. Kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. Bir sanal ağ (VNet) ve alt ağ hello oluşturmak hello kaynak grubu ile aynı konumda:

    ```powershell
    
    # Create a subnet configuration
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name MySubnet `
    -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $VNet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyVNet `
    -AddressPrefix 10.0.0.0/16 `
    -Subnet $subnetConfig

    # Get hello subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. Bir ağ güvenlik grubu (NSG) ve bir kural oluşturun. Merhaba NSG korur hello VM gelen ve giden kurallarını kullanma. Bu durumda, bağlantı noktası 3389 için gelen masaüstü bağlantılarına izin veren bir gelen kuralı oluşturulur.

    ```powershell
    
    # Create an inbound network security group rule for port 3389

    $NSGRule = New-AzureRmNetworkSecurityRuleConfig `
    -Name MyNsgRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow
    
    # Create a network security group
    $NSG = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyNetworkSecurityGroup `
    -SecurityRules $NSGRule
    ```

6. Merhaba NIC Hello birincil IP yapılandırmasını tanımlayın Değişiklik 10.0.0.4 tooa oluşturduğunuz, önceden tanımlanmış hello değer kullanmadıysanız hello alt ağdaki geçerli bir adresi. Statik bir IP adresi atamadan önce zaten kullanımda olmadığı ilk onaylamanız önerilir. Merhaba komutu girin `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`. Başlangıç adresi varsa, hello döndürür çıktı *doğru*. Kullanılabilir durumda değilse, hello döndürür çıktı *False* ve kullanılabilir adresleri listesi. 

    Komutları, aşağıdaki hello içinde **< Değiştir-ile-bilgisayarınızı-benzersiz-adı > merhaba benzersiz DNS adı toouse ile değiştirin.** bir Azure bölgesi içindeki tüm ortak IP adresleri arasında Hello adının benzersiz olması gerekir. Bu isteğe bağlı bir parametredir. Tooconnect toohello VM yalnızca istiyorsanız kaldırılması hello ortak IP adresi kullanarak.

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    Birden çok IP yapılandırmaları tooa NIC atadığınızda, bir yapılandırma hello atanmalıdır *-birincil*.

    > [!NOTE]
    > Nominal bir ücret ortak IP adresine sahip. IP hakkında daha fazla adres fiyatlandırma toolearn okuma hello [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses) sayfası. Bir abonelikte kullanılabilir genel IP adresleri sınırı toohello sayısı yoktur. Merhaba okuma hello sınırları hakkında daha fazla toolearn [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) makalesi.

7. Merhaba NIC için ikincil IP yapılandırmaları Hello tanımlayın Ekleyebilir veya gerektiği gibi yapılandırmaları kaldırabilirsiniz. Her IP yapılandırması atanan özel bir IP adresi olmalıdır. Her yapılandırma isteğe bağlı olarak atanmış bir genel IP adresi olabilir.

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName2 = "IPConfig-2"
    $IpConfig2     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName2 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.5 `
    -PublicIpAddress $PublicIP2
        
    $IpConfigName3 = "IpConfig-3"
    $IpConfig3 = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IPConfigName3 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.6
    ```

8. Merhaba NIC oluşturun ve hello üç IP yapılandırmaları tooit ilişkilendirin:

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    >Bu makalede tooone NIC atanmış tüm yapılandırmalar olsa, birden çok IP yapılandırmaları tooevery bağlı NIC toohello VM atayabilirsiniz. nasıl toocreate birden çok NIC ile VM okuma toolearn hello [bir VM ile birden çok NIC oluşturma](virtual-network-deploy-multinic-arm-ps.md) makalesi.

9. Merhaba VM hello aşağıdaki komutları girerek oluşturabilirsiniz:

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted tooenter a sername and password for hello VM you're reating.
    $cred = Get-Credential
    
    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
    -VMName MyVM `
    -VMSize Standard_DS1_v2 | `
    Set-AzureRmVMOperatingSystem -Windows `
    -ComputerName MyVM `
    -Credential $cred | `
    Set-AzureRmVMSourceImage `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest | `
    Add-AzureRmVMNetworkInterface `
    -Id $NIC.Id
    
    # Create hello VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. Ekle hello özel IP adresleri toohello VM işletim sistemi işletim sisteminizin hello hello adımları tamamlayarak [eklemek IP adresleri tooa VM işletim sistemi](#os-config) bu makalenin. Merhaba ortak IP adresleri toohello işletim sistemi eklemeyin.

## <a name="add"></a>IP adreslerini tooa VM ekleme

Özel ve genel IP adresleri tooa NIC izleyin hello adımları tamamlayarak ekleyebilirsiniz. Merhaba hello bölümleri aşağıdaki örneklerde, zaten bir VM hello açıklanan hello üç IP yapılandırmasına sahip olduğunu varsayın [senaryo](#Scenario) Bu makale, ancak gerekli değildir, yapın.

1. Bir PowerShell komut istemi açın ve tam hello kalan tek bir PowerShell oturumunda bu bölümdeki adımları. Zaten yüklü ve yapılandırılmış PowerShell sahip değilseniz, tam hello hello adımları [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) makalesi.
2. Merhaba "değerini" hello NIC bulunmaktadır tooadd IP adresi tooand hello kaynak grubunu ve konumu hello istediğiniz NIC $Variables toohello adı aşağıdaki hello değiştirin:

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    Merhaba toochange istediğiniz NIC hello adını bilmiyorsanız, komutları aşağıdaki hello girin ve ardından hello önceki değişkenlerin hello değerleri değiştirin:

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. Bir değişken oluşturun ve NIC hello aşağıdaki komutu yazarak varolan toohello ayarlayın:

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. Aşağıdaki komutları hello değiştirme *MyVNet* ve *MySubnet* NIC bağlı hello VNet ve alt ağ hello toohello adları. NIC bağlı hello komutları tooretrieve hello VNet ve alt ağ nesneleri hello girin:

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    NIC bağlı hello VNet veya alt ağ adı hello bilmiyorsanız, komutu aşağıdaki hello girin:
    ```powershell
    $MyNIC.IpConfigurations
    ```
    Merhaba çıktısında metin benzer toohello örnek çıktı aşağıdaki için bakın:
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    Bu çıkışı *MyVnet* hello VNet olduğu ve *MySubnet* hello alt hello NIC bağlı değil.

5. Aşağıdaki bölümlerde, gereksinimlerinize göre hello Hello adımları tamamlayın:

    **Özel bir IP adresi Ekle**

    özel bir IP adresi tooa NIC tooadd, bir IP yapılandırması oluşturmanız gerekir. Merhaba aşağıdaki komutu bir yapılandırma 10.0.0.7 ile bir statik IP adresi oluşturur. Statik bir IP adresi belirtirken, hello alt ağ için kullanılmayan bir adres olmalıdır. Başlangıç adresi tooensure bulunur hello girerek önce test önerilir `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` komutu. Başlangıç IP adresi varsa, hello döndürür çıktı *doğru*. Kullanılabilir durumda değilse, hello döndürür çıktı *yanlış*ve kullanılabilir adresleri listesi.

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    Benzersiz yapılandırma adları ve özel IP adresleri (yapılandırmaları statik IP adresleriyle) kullanarak gereksinim duyduğunuz kadar çok yapılandırmaları oluşturun.

    İşletim sisteminizin hello hello adımları tamamlayarak Hello özel IP adresi toohello VM işletim sistemi Ekle [eklemek IP adresleri tooa VM işletim sistemi](#os-config) bu makalenin.

    **Bir ortak IP adresi Ekle**

    Bir ortak IP adresi, bir ortak IP adresi kaynak tooeither yeni bir IP yapılandırması veya var olan IP yapılandırmasını ilişkilendirerek eklenir. Gereksinim duyduğunuz kadar izleyin, hello bölümlerden biri hello adımlarını tamamlayın.

    > [!NOTE]
    > Nominal bir ücret ortak IP adresine sahip. IP hakkında daha fazla adres fiyatlandırma toolearn okuma hello [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses) sayfası. Bir abonelikte kullanılabilir genel IP adresleri sınırı toohello sayısı yoktur. Merhaba okuma hello sınırları hakkında daha fazla toolearn [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) makalesi.
    >

    - **Merhaba ortak IP adresi kaynak tooa yeni IP yapılandırmasını ilişkilendirin**
    
        Yeni bir IP yapılandırmasında bir ortak IP adresi eklediğinizde, tüm IP yapılandırmalarının özel bir IP adresi olması gerektiği için özel bir IP adresi eklemelisiniz. Varolan bir ortak IP adresi kaynağı ekleyin veya yeni bir tane oluşturun. toocreate yeni bir hello aşağıdaki komutu girin:
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        Özel statik IP adresi ve ilişkili hello yeni bir IP yapılandırmasıyla toocreate *myPublicIp3* genel IP adresi kaynak, komutu aşağıdaki hello girin:

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - **Merhaba ortak IP adresi kaynak tooan mevcut IP yapılandırmasını ilişkilendirin**

        Genel bir IP adresi kaynağı yalnızca zaten ilişkili olmayan ilişkili tooan IP yapılandırması olabilir. Komutu aşağıdaki hello girerek bir IP yapılandırması ilişkili bir ortak IP adresi olup olmadığını belirleyebilirsiniz:

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        Çıktı benzer toohello aşağıdakilere bakın:

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        Merhaba itibaren **Publicıpaddress** sütunu için *IpConfig 3* olduğundan, hiçbir ortak IP adresi kaynağı şu anda ilişkili tooit boştur. Bir var olan ortak IP adresi kaynak tooIpConfig-3 ekleyin veya komut toocreate bir aşağıdaki hello girin:

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        Tooassociate hello ortak IP adresi adlı kaynak toohello mevcut IP yapılandırması komutu aşağıdaki hello girin *IpConfig 3*:
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. Merhaba NIC hello yeni IP yapılandırması ile komutu aşağıdaki hello girerek ayarlayın:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. Görünüm hello özel IP adresleri ve ortak IP adresi atanmış kaynaklar toohello girerek NIC hello komutu aşağıdaki hello:

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. İşletim sisteminizin hello hello adımları tamamlayarak Hello özel IP adresi toohello VM işletim sistemi Ekle [eklemek IP adresleri tooa VM işletim sistemi](#os-config) bu makalenin. Merhaba ortak IP adresi toohello işletim sistemi eklemeyin.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
