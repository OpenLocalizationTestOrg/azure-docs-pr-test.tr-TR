---
title: "birden çok NIC - Azure Resource Manager şablonu ile bir VM aaaCreate | Microsoft Docs"
description: "Bir VM ile birden çok NIC bir Azure Resource Manager şablonu kullanarak oluşturun."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 486f7dd5-cf2f-434c-85d1-b3e85c427def
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5d9ffcbd40c72dc18ae6de38e739eb5e45bf669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a>Bir şablon kullanarak birden çok NIC ile VM oluşturma
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).  Bu makalede, kullanarak yer almaktadır hello yerine çoğu yeni dağıtımlar için Microsoft önerir hello Resource Manager dağıtım modeli [Klasik dağıtım modeli](virtual-network-deploy-multinic-classic-ps.md).
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Merhaba aşağıdaki adımları kullanın adlı bir kaynak grubu *IaaSStory* hello WEB sunucuları ve bir kaynak grubu için adlı *IaaSStory arka uç* hello DB sunucuları için.

## <a name="prerequisites"></a>Ön koşullar
DB sunucuları hello oluşturabilmeniz için önce toocreate hello gerekir *IaaSStory* hello gereken tüm kaynakların bu senaryo için kaynak grubuyla. Bu kaynaklar toocreate tamamlamak hello adımları izleyin:

1. Çok gidin[hello şablon sayfasına](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).
2. Merhaba şablon sayfasındaki sağ toohello **üst kaynak grubu**, tıklatın **tooAzure dağıtmak**.
3. Gerekirse, hello parametre değerlerini değiştirmek sonra hello Azure Önizleme portalı toodeploy hello kaynak grubunda hello adımları izleyin.

> [!IMPORTANT]
> Depolama hesabı adları benzersiz olduğundan emin olun. Azure üzerinde yinelenen depolama hesabı adları sahip olamaz.
> 

## <a name="understand-hello-deployment-template"></a>Merhaba dağıtım şablonu anlama
Bu belgeleri ile sağlanan hello şablonunun dağıtmadan önce ne yaptığını anladığınızdan emin olun. Aşağıdaki adımları hello hello şablon iyi bir genel bakış sağlar:

1. Çok gidin[hello şablon sayfasına](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).
2. Tıklatın **azuredeploy.json** tooopen hello şablon dosyası.
3. Bildirim hello *osType* aşağıda listelenen parametre. Bu parametre kullanılan tooselect olan hangi VM görüntü toouse hello veritabanı sunucusu, birden çok işletim sistemi için ilgili ayarları.

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS toouse for VMs: Windows or Ubuntu."
      }
    },
    ```

4. Değişkenleri toohello listesini kaydırın ve hello hello tanımını denetleyin **dbVMSetting** değişkenleri, aşağıda listelenen. Hello bulunan hello dizi öğeleri birini aldığı **dbVMSettings** değişkeni. Yazılım geliştirme ifadeyle bilginiz varsa, hello görüntüleyebilirsiniz **dbVMSettings** değişken karma tablo veya bir sözlük olarak.

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. Toodeploy Windows hello arka uçta SQL çalıştıran VM'ler karar verdiğinizi varsayalım. Değeri hello **osType** olacaktır *Windows*ve hello **dbVMSetting** değişkeni aşağıda listelenen hello hello ilk değeri temsil eden hello öğesi içerebilir **dbVMSettings** değişkeni.

    ```json
    "Windows": {
      "vmSize": "Standard_DS3",
      "publisher": "MicrosoftSQLServer",
      "offer": "SQL2014SP1-WS2012R2",
      "sku": "Standard",
      "version": "latest",
      "vmName": "DB",
      "osdisk": "osdiskdb",
      "datadisk": "datadiskdb",
      "nicName": "NICDB",
      "ipAddress": "192.168.2.",
      "extensionDeployment": "",
      "avsetName": "ASDB",
      "remotePort": 3389,
      "dbPort": 1433
    },
    ```

6. Bildirim hello **vmSize** hello değeri içeren *Standard_DS3*. Yalnızca belirli VM boyutları için birden çok NIC hello kullanımına izin verin. Hangi VM boyutları hello okuyarak birden çok NIC destek doğrulayabilirsiniz [Windows VM boyutları](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ve [Linux VM boyutları](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) makaleleri.

7. Çok ilerleyin**kaynakları** ve bildirimi hello ilk öğe. Bir depolama hesabı açıklar. Bu depolama hesabını her veritabanı VM tarafından kullanılan kullanılan toomaintain hello veri disklerinin olacaktır. Bu senaryoda, her veritabanı VM normal depolamada depolanan bir işletim sistemi diski ve SSD (premium) depolamada depolanan iki veri diski var.

    ```json
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[parameters('prmStorageName')]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "Storage Account - Premium"
      },
      "properties": {
      "accountType": "[parameters('prmStorageType')]"
      }
    },
    ```

8. Aşağıda listelenen toohello sonraki kaynak kaydırın. Bu kaynak NIC VM her veritabanında veritabanı erişimi için kullanılan hello temsil eder. Bildirim hello hello kullanımını **kopya** bu kaynak işlevinde. Merhaba şablon sağlar, toodeploy istediğiniz gibi hello üzerinde birçok VM tabanlı olarak **dbCount** parametresi. Bu nedenle toocreate gerekir hello NIC aynı miktarda her VM için bir tane veritabanı erişimi için.

    ```json
    {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[concat(variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DB DA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(4))]",
            "subnet": {
              "id": "[variables('backEndSubnetRef')]"
            }
          }
         }
       ] 
     }
    },
    ```

9. Aşağıda listelenen toohello sonraki kaynak kaydırın. Bu kaynak NIC her veritabanındaki VM yönetimi için kullanılan hello temsil eder. Bir kez daha, bu NIC'ler birini her veritabanı için VM gerekir. Bildirim hello **networkSecurityGroup** erişim tooRDP/SSH toothis NIC yalnızca izin veren bir NSG bağlama öğesi.

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[concat(variables('dbVMSetting').nicName, '-RA-',copyindex(1))]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "NetworkInterfaces - DB RA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "networkSecurityGroup": {
             "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('remoteAccessNSGName'))]"
             },
             "privateIPAllocationMethod": "Static",
             "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(54))]",
             "subnet": {
              "id": "[variables('backEndSubnetRef')]"
             }
           }
          }
        ]
      }
    },
```

10. Aşağıda listelenen toohello sonraki kaynak kaydırın. Bu kaynak, tüm veritabanı VM'ler tarafından paylaşılan bir kullanılabilirlik kümesi toobe temsil eder. Bu şekilde, her zaman olacağını bir VM bakım sırasında çalışan ayarlamak hello içinde garanti.

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/availabilitySets",
      "name": "[variables('dbVMSetting').avsetName]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "AvailabilitySet - DB"
      }
    },
    ```

11. Toohello sonraki kaynak kaydırın. Bu kaynak hello veritabanı VM'ler, hello ilk birkaç satırı aşağıda listelenen görülen temsil eder. Bildirim hello hello kullanımını **kopya** yeniden işlev, birden çok VM oluşturduğunuz sağlama dayalı hello üzerinde **dbCount** parametresi. Ayrıca hello fark **dependsOn** koleksiyonu. VM, hello kullanılabilirlik kümesi ve hello depolama hesabı ile birlikte dağıtılan hello önce oluşturulan gerekli toobe olan iki NIC listeler.

    ```json
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('dbVMSetting').vmName,copyindex(1))]",
    "location": "[variables('location')]",
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-RA-', copyindex(1))]",
      "[concat('Microsoft.Compute/availabilitySets/', variables('dbVMSetting').avsetName)]",
      "[concat('Microsoft.Storage/storageAccounts/', parameters('prmStorageName'))]"
    ],
    "tags": {
      "displayName": "VMs - DB"
    },
    "copy": {
      "name": "dbvmcount",
      "count": "[parameters('dbCount')]"
    },
    ```

12. Aşağı kaydırın hello VM kaynak toohello **networkProfile** aşağıda listelenen öğesi. Her VM için başvuru olan iki NIC olduğuna dikkat edin. Bir VM için birden çok NIC oluşturduğunuzda, hello ayarlamalısınız **birincil** hello NIC'ler birinin özelliği çok*true*, ve rest çok hello*false*.

    ```json
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-DA-',copyindex(1)))]",
          "properties": { "primary": true }
        },
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-RA-',copyindex(1)))]",
          "properties": { "primary": false }
        }
      ]
    }
    ```

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a>Kullanarak Hello ARM şablonu dağıtma toodeploy tıklatın

> [!IMPORTANT]
> Merhaba izlediğinizden emin olun [ön koşullar](#Pre-requisites) hello yönergeleri izleyerek önce adımları.
> 

Merhaba örnek şablonunda kullanılabilir hello genel depo yukarıda açıklanan hello varsayılan kullanılan değerler toogenerate hello senaryosu içeren bir parametre dosyası kullanır. toodeploy tıklatın toodeploy, bu şablonu kullanarak izleyin [bu bağlantıyı](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), sağ toohello **arka uç kaynak grubu (belgelere bakın)** tıklatın **tooAzure dağıtmak**, Değiştir Varsayılan parametre değerlerini gerekirse hello ve hello hello Portalı'ndaki yönergeleri izleyin.

Aşağıdaki Hello şekilde hello yeni kaynak grubu Merhaba içeriğine dağıtımdan sonra gösterilmektedir.

![Arka uç kaynak grubu](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-hello-template-by-using-powershell"></a>PowerShell kullanarak Hello şablonu dağıtma
PowerShell kullanarak yüklediğiniz toodeploy hello şablon PowerShell'i yükleme ve hello hello adımları izleyerek yapılandırma [PowerShell'i yükleme ve yapılandırma](/powershell/azure/overview) makalesi ve hello aşağıdaki adımları tamamlayın:

Merhaba çalıştırmak  **`New-AzureRmResourceGroup`**  kullanarak bir kaynak grubu cmdlet toocreate hello şablonu.

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

Beklenen çıktı:

    ResourceGroupName : IaaSStory-Backend
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions  NotActions
                        =======  ==========
                        *
        Resources         :
                        Name                 Type                                 Location
                        ===================  ===================================  ========
                        ASDB                 Microsoft.Compute/availabilitySets   westus  
                        DB1                  Microsoft.Compute/virtualMachines    westus  
                        DB2                  Microsoft.Compute/virtualMachines    westus  
                        NICDB-DA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-DA-2           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-2           Microsoft.Network/networkInterfaces  westus  
                        wtestvnetstorageprm  Microsoft.Storage/storageAccounts    westus  
    ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Hello Azure CLI kullanarak Hello şablonu dağıtma
hello Azure CLI kullanarak toodeploy hello şablon hello adımları izleyin.

1. Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.
2. Merhaba çalıştırmak  **`azure config mode`**  aşağıda gösterildiği gibi komut tooswitch tooResource Yöneticisi modu.

    ```azurecli
    azure config mode arm
    ```

    Çıktı aşağıdaki Hello beklenen:

        info:    New mode is arm

3. Açık hello [parametre dosyası](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json)içeriğini seçin ve tooa dosyayı bilgisayarınıza kaydedin. Bu örnekte, hello parametreler dosyası çok kaydettik*parameters.json*.
4. Merhaba çalıştırmak  **`azure group deployment create`**  cmdlet toodeploy hello hello şablonu ve parametre kullanarak yeni Vnet'i, yukarıda indirdiğiniz ve değiştirdiğiniz dosyaları. Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    Beklenen çıktı:
   
        info:    Executing command group create
        + Getting resource group IaaSStory-Backend
        + Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

