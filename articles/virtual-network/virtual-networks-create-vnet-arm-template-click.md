---
title: "bir sanal ağ aaaCreate | Azure Resource Manager şablonu | Microsoft Docs"
description: "Nasıl toocreate sanal bir ağ bir Azure Resource Manager şablonu kullanarak öğrenin."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 69530861-2f97-4a6e-b336-a7baf2690044
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b9c289433ff2a84bec19eac25fa28ab40d131c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a>Bir Azure Resource Manager şablonu kullanarak bir sanal ağ oluşturma

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure'un iki dağıtım modeli vardır: Azure Resource Manager ve klasik. Microsoft, kaynakları hello Resource Manager dağıtım modeli üzerinden oluşturma önerir. Merhaba iki modelleri arasındaki farklar hakkında daha fazla bilgi toolearn hello okuma hello [anlamak Azure dağıtım modelleri](../azure-resource-manager/resource-manager-deployment-model.md) makalesi.
 
Bu makalede nasıl toocreate bir sanal ağ üzerinden hello Resource Manager dağıtım modeli bir Azure Resource Manager şablonu kullanarak açıklanmaktadır. Ayrıca, bir VNet kaynak diğer araçları kullanarak Yöneticisi aracılığıyla oluşturabilir veya liste aşağıdaki hello farklı bir seçeneği seçerek hello Klasik dağıtım modeli üzerinden bir VNet oluşturun:

> [!div class="op_single_selector"]
- [Portal](virtual-networks-create-vnet-arm-pportal.md)
- [PowerShell](virtual-networks-create-vnet-arm-ps.md)
- [CLI](virtual-networks-create-vnet-arm-cli.md)
- [Şablon](virtual-networks-create-vnet-arm-template-click.md)
- [Portal (Klasik)](virtual-networks-create-vnet-classic-pportal.md)
- [PowerShell (Klasik)](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [CLI (Klasik)](virtual-networks-create-vnet-classic-cli.md)

Şunları öğreneceksiniz nasıl toodownload değiştirmek ve var olan ARM şablonunu github'dan ve hello şablonu GitHub, PowerShell ve Azure CLI hello dağıtabilirsiniz.

Merhaba ARM şablonunu doğrudan github'dan, herhangi bir değişiklik yapılmadan dağıtıyorsanız çok atla[github'dan şablon dağıtma](#deploy-the-arm-template-by-using-click-to-deploy).

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>İndirme ve hello Azure Resource Manager şablonu anlama
Merhaba Github'dan VNet ve iki alt ağ oluşturmak için varolan şablonunu indirebilir, istediğiniz ve yeniden tüm değişiklikleri yapın. toodo, bu nedenle, hello aşağıdaki adımları tamamlayın:

1. Çok gidin[hello örnek şablon sayfasına](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).
2. **azuredeploy.json** ve **RAW** öğelerine sırayla tıklayın.
3. Merhaba dosya tooa bilgisayarınızda yerel bir klasöre kaydedin.
4. Şablonları hakkında bilginiz varsa 7 toostep atlayın.
5. Kaydettiğiniz hello dosyasını açın ve altındaki hello içeriğe bakın **parametreleri** satırında 5. ARM şablonu parametreleri, dağıtım sırasında doldurulabilecek değerler için bir yer tutucu sağlar.
   
   | Parametre | Açıklama |
   | --- | --- |
   | **konum** |Merhaba Vnet'in oluşturulacağı azure bölgesi |
   | **vnetName** |Hello için ad yeni VNet |
   | **addressPrefix** |Adres alanı CIDR biçiminde VNet, hello için |
   | **subnet1Name** |Hello için ad ilk sanal ağ |
   | **subnet1Prefix** |Merhaba ilk alt ağ için CIDR bloğu |
   | **subnet2Name** |Hello için ad ikinci VNet |
   | **subnet2Prefix** |Merhaba ikinci alt ağ için CIDR bloğu |
   
   > [!IMPORTANT]
   > GitHub’da tutulan Azure Resource Manager şablonları zaman içinde değişebilir. Kullanmadan önce hello şablonu denetlediğinizden emin olun.
   > 
   > 
6. Merhaba içeriği altında denetleyin **kaynakları** ve hello aşağıdakilere dikkat edin:
   
   * **type**. Merhaba şablon tarafından oluşturulan kaynak türü. Bu durumda, bir VNet’i temsil eden **Microsoft.Network/virtualNetworks**.
   * **name**. Merhaba kaynak adı. Bildirim hello kullanımını **[parameters('vnetName')]**, hangi anlamına gelir hello giriş olarak dağıtımı sırasında hello kullanıcı ya da bir parametre dosyası tarafından sağlanan ad olacaktır.
   * **properties**. Merhaba kaynak özelliklerinin listesi. Bu şablon, VNet oluşturulduğu sırada hello adres alanı ve alt ağ özelliklerini kullanır.
7. Geri çok gidin[hello örnek şablon sayfasına](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).
8. **azuredeploy-parameters.json** ve **RAW** öğelerine sırayla tıklayın.
9. Merhaba dosya tooa bilgisayarınızda yerel bir klasöre kaydedin.
10. Yeni kaydettiğiniz hello dosyasını açın ve hello parametreleri hello değerlerini düzenleyin. Toodeploy hello hello senaryoda açıklanan VNet altındaki değerler aşağıdaki hello kullan:

    ```json
        {
          "location": {
            "value": "Central US"
          },
          "vnetName": {
              "value": "TestVNet"
          },
          "addressPrefix": {
              "value": "192.168.0.0/16"
          },
          "subnet1Name": {
              "value": "FrontEnd"
          },
          "subnet1Prefix": {
            "value": "192.168.1.0/24"
          },
          "subnet2Name": {
              "value": "BackEnd"
          },
          "subnet2Prefix": {
              "value": "192.168.2.0/24"
          }
        }
    ```

11. Merhaba dosyasını kaydedin.


## <a name="deploy-hello-template-using-powershell"></a>PowerShell kullanarak hello şablonu dağıtma

PowerShell kullanarak yüklediğiniz adımları toodeploy hello şablonunu aşağıdaki hello tamamlayın:

1. Yükleme ve Azure PowerShell hello hello adımları izleyerek yapılandırma [nasıl tooInstall ve yapılandırma Azure PowerShell](/powershell/azure/overview) makalesi.
2. Komut toocreate aşağıdaki hello yeni bir kaynak grubu çalıştırın:

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    Merhaba komut oluşturur adlı bir kaynak grubu *TestRG* hello içinde *Orta ABD* azure bölgesi. Kaynak grupları hakkında daha fazla bilgi için [Azure Resource Manager’a Genel Bakış](../azure-resource-manager/resource-group-overview.md)’ı ziyaret edin.

    Beklenen çıktı:

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. Toodeploy Merhaba, yukarıda indirdiğiniz ve değiştirdiğiniz hello şablonu ve parametre dosyalarını kullanarak yeni Vnet'i komutu aşağıdaki hello çalıştırın:

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    Beklenen çıktı:
   
        DeploymentName    : TestVNetDeployment
        ResourceGroupName : TestRG
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
        Parameters        :
                            Name             Type                       Value
                            ===============  =========================  ==========
                            location         String                     Central US
                            vnetName         String                     TestVNet
                            addressPrefix    String                     192.168.0.0/16
                            subnet1Prefix    String                     192.168.1.0/24
                            subnet1Name      String                     FrontEnd
                            subnet2Prefix    String                     192.168.2.0/24
                            subnet2Name      String                     BackEnd
   
        Outputs           :
4. Çalışma hello şu komutu tooview hello hello özelliklerini yeni VNet:

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    Beklenen çıktı:

        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : centralus
        Id                : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              :
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              },
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="deploy-hello-template-using-click-to-deploy"></a>Dağıtmak için kullanarak hello şablonu dağıtma

Microsoft ve açık toohello topluluk tarafından tutulan önceden tanımlanmış Azure Resource Manager şablonları karşıya yüklenen tooa GitHub deposunu yeniden kullanabilirsiniz. Bu şablonlar Github'dan sınırsız dağıtılabilir veya indirilir ve gereksinimlerinizi toofit değiştirdi. toodeploy iki alt ağa sahip VNet oluşturan bir şablonu aşağıdaki adımları tam hello:

1. Tarayıcıdan çok gidin[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).
2. Şablonları hello listesini kaydırın ve tıklayın **101-vnet-two-subnets**. Merhaba denetleyin **README.md** aşağıda gösterildiği gibi dosya.

    ![Github’da READEME.md dosyası](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. Tıklatın **tooAzure dağıtmak**. Gerekiyorsa, Azure oturum açma kimlik bilgilerinizi girin. 
4. Merhaba, **parametreleri** dikey penceresinde, yeni VNet toouse toocreate istediğiniz ve ardından hello değerleri girin **Tamam**. Merhaba aşağıdaki şekilde hello senaryo için hello değerleri gösterir:
   
    ![ARM şablonu parametreleri](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. Tıklatın **kaynak grubu** seçip bir kaynak grubu tooadd Vnet'e hello veya tıklatın **Yeni Oluştur** tooadd hello VNet tooa yeni kaynak grubu. Merhaba aşağıdaki şekilde hello kaynak olarak adlandırılan yeni bir kaynak grubu için Grup ayarları gösterilmektedir **TestRG**:

    ![Kaynak grubu](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. Gerekirse, hello değiştirmek **abonelik** ve **konumu** ayarlarını.
7. Toosee hello VNet hello parçasında olarak istemiyorsanız **Sabitle**, devre dışı **PIN tooStartboard**.
8. Tıklatın **yasal koşulları**hello koşullarını okuyun ve tıklatın **satın** tooagree. 
9. Tıklatın **oluşturma** toocreate hello VNet.
   
    ![Önizleme portalında dağıtım kutucuğu gönderiliyor](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. Merhaba dağıtım tamamlandıktan sonra hello Azure portal'ı tıklatın **daha fazla hizmet**, türü *sanal ağlar* görünen hello filtre kutusuna sanal ağlar toosee hello sanal ağlar dikey penceresinde'ye tıklayın. Merhaba dikey penceresinde tıklayın *TestVNet*. Merhaba, *TestVNet* dikey penceresinde tıklatın **alt ağlar** hello resim aşağıdaki gösterildiği gibi toosee oluşturulan hello alt ağlar:
    
     ![Önizleme portalında VNet oluşturma](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a>Sonraki adımlar

Bilgi nasıl tooconnect:

- Bir sanal makine (VM) tooa sanal ağla okuma hello [bir Windows VM oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md) veya [bir Linux VM oluşturma](../virtual-machines/linux/quick-create-portal.md) makaleleri. Merhaba makaleleri hello adımlarda bir VNet ve alt ağ oluşturmak yerine, bir VM'ye mevcut VNet ve alt ağ tooconnect seçebilirsiniz.
- sanal ağ tooother sanal ağlar hello okuyarak hello [sanal ağlara bağlanma](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) makalesi.
- bir siteden siteye sanal özel ağ (VPN) veya expressroute bağlantı hattı kullanarak hello sanal ağ tooan şirket içi ağ. Bilgi hello okuyarak nasıl [bir siteden siteye VPN kullanarak bir VNet tooan şirket içi ağ bağlanmak](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) ve [VNet tooan expressroute bağlantı hattı bağlantı](../expressroute/expressroute-howto-linkvnet-arm.md) makaleleri.
