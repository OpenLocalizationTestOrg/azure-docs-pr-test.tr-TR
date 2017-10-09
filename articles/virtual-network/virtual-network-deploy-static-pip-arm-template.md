---
title: "bir statik genel IP adresi - Azure Resource Manager şablonu ile bir VM aaaCreate | Microsoft Docs"
description: "Nasıl toocreate VM bir statik genel IP adresi bir Azure Resource Manager şablonu kullanarak öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d551085a-c7ed-4ec6-b4c3-e9e1cebb774c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a8640ed4fad06b0e09820e6114fd6789db73847
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a>Bir Azure Resource Manager şablonu kullanarak bir statik genel IP adresiyle bir VM oluşturma

> [!div class="op_single_selector"]
> * [Azure portal](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI](virtual-network-deploy-static-pip-arm-cli.md)
> * [Şablon](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (Klasik)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md). Bu makalede, Microsoft hello Klasik dağıtım modeli yerine çoğu yeni dağıtımlar için önerir hello Resource Manager dağıtım modeli kullanılarak kapsar.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a>Bir şablon dosyasındaki ortak IP adresi kaynakları
Görüntüleme ve hello karşıdan yükleme [örnek şablonu](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).

Merhaba aşağıdaki bölümde yukarıdaki hello senaryoyu temel hello genel IP kaynağı, hello tanımını gösterir:

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('webVMSetting').pipName]",
  "location": "[variables('location')]",
  "properties": {
    "publicIPAllocationMethod": "Static"
  },
  "tags": {
    "displayName": "PublicIPAddress - Web"
  }
},
```

Bildirim hello **Publicıpallocationmethod** çok ayarlama özelliği*statik*. Bu özellik ya da olabilir *dinamik* (varsayılan değer) veya *statik*. Merhaba atanan genel IP adresi hiçbir zaman değiştirecek toostatic garanti ayarlama.

Merhaba aşağıdaki bölümde hello ilişkilendirmesini hello ortak IP adresinin ağ arabirimi gösterir:

```json
  {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('webVMSetting').nicName]",
    "location": "[variables('location')]",
    "tags": {
    "displayName": "NetworkInterface - Web"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('webVMSetting').pipName)]",
      "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
          "privateIPAllocationMethod": "Static",
          "privateIPAddress": "[variables('webVMSetting').ipAddress]",
          "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('webVMSetting').pipName)]"
          },
          "subnet": {
            "id": "[variables('frontEndSubnetRef')]"
          }
        }
      }
    ]
  }
},
```

Bildirim hello **Publicıpaddress** toohello işaret eden özellik **kimliği** adlı bir kaynağın **variables('webVMSetting').pipName**. Yukarıda gösterilen hello genel IP kaynağı hello adını olmasıdır.

Merhaba ağ arabirimi yukarıdaki hello son olarak, listelenen **networkProfile** hello oluşturulan VM özelliği.

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Kullanarak Hello şablonu dağıtma toodeploy tıklatın

Merhaba örnek şablonunda kullanılabilir hello genel depo yukarıda açıklanan hello varsayılan kullanılan değerler toogenerate hello senaryosu içeren bir parametre dosyası kullanır. toodeploy tıklatın toodeploy, bu şablonu kullanarak tıklatın **tooAzure dağıtmak** hello Readme.md dosyasında hello [statik PIP VM](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) şablonu. İsterseniz Hello varsayılan parametre değerlerini değiştirin ve hello boş parametreler için değerler girin.  Merhaba portal toocreate statik genel IP adresine sahip bir sanal makine Hello yönergeleri izleyin.

## <a name="deploy-hello-template-by-using-powershell"></a>PowerShell kullanarak Hello şablonu dağıtma

PowerShell kullanarak yüklediğiniz toodeploy hello şablonunu hello adımları izleyin.

1. Azure PowerShell'i hiç kullanmadıysanız, tam hello hello adımları [nasıl tooInstall ve yapılandırma Azure PowerShell](/powershell/azure/overview) makalesi.
2. Bir PowerShell konsolunda hello çalıştırın `New-AzureRmResourceGroup` cmdlet toocreate yeni bir kaynak grubu, gerekirse. Oluşturulan bir kaynak grubu zaten varsa, toostep 3 gidin.

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    Beklenen çıktı:
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. Bir PowerShell konsolunda hello çalıştırın `New-AzureRmResourceGroupDeployment` cmdlet toodeploy hello şablonu.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    Beklenen çıktı:
   
        DeploymentName    : DeployVM
        ResourceGroupName : PIPTEST
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
                            Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/mas
                            ter/IaaS-Story/03-Static-public-IP/azuredeploy.json
                            ContentVersion : 1.0.0.0
   
        Parameters        :
                            Name                      Type                       Value     
                            ========================  =========================  ==========
                            vnetName                  String                     WTestVNet
                            vnetPrefix                String                     192.168.0.0/16
                            frontEndSubnetName        String                     FrontEnd  
                            frontEndSubnetPrefix      String                     192.168.1.0/24
                            storageAccountNamePrefix  String                     iaasestd  
                            stdStorageType            String                     Standard_LRS
                            osType                    String                     Windows   
                            adminUsername             String                     adminUser
                            adminPassword             SecureString                         
   
        Outputs           :

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Hello Azure CLI kullanarak Hello şablonu dağıtma
hello Azure CLI, tam hello aşağıdaki adımları kullanarak toodeploy hello şablonu:

1. Hiç Azure CLI kullanmadıysanız, hello hello adımları [hello Azure CLI yükleyip](../cli-install-nodejs.md) makale tooinstall ve yapılandırın.
2. Merhaba çalıştırmak `azure config mode` aşağıda gösterildiği gibi komut tooswitch tooResource Yöneticisi modu.

    ```azurecli
    azure config mode arm
    ```

    Merhaba hello komutunun çıktısını yukarıdaki beklenen:

        info:    New mode is arm

3. Açık hello [parametre dosyası](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json)içeriğini seçin ve tooa dosyayı bilgisayarınıza kaydedin. Bu örnekte, hello parametreleri adlı tooa dosyasına kaydedilir *parameters.json*. İsterseniz hello dosyası içinde Hello parametre değerlerini değiştirmek ancak en azından hello Admınpassword parametresi tooa benzersiz ve karmaşık bir parola hello değerini değiştirmek önerilir.
4. Merhaba çalıştırmak `azure group deployment create` cmd toodeploy hello hello şablonu ve parametre kullanarak yeni Vnet'i, yukarıda indirdiğiniz ve değiştirdiğiniz dosyaları. Merhaba aşağıdaki komutta, <path> hello yoluna sahip hello dosyasına kaydedilir. 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    Beklenen çıktı: (kullanılan parametre değerlerini listeler)

        info:    Executing command group create
        + Getting resource group PIPTEST2
        + Creating resource group PIPTEST2
        info:    Created resource group PIPTEST2
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/PIPTEST2
        data:    Name:                PIPTEST2
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

