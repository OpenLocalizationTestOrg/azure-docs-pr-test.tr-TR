---
title: "bir Azure sanal makine ölçek kümesi üzerinde bir uygulama aaaDeploy | Microsoft Docs"
description: "Toodeploy basit otomatik ölçeklendirmeyi uygulama bir Azure Resource Manager şablonu kullanarak bir sanal makine ölçekte öğrenin."
services: virtual-machine-scale-sets
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 6fccc310312cabfcdddfcbcd2d154fc5cc440417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-autoscaling-app-using-a-template"></a>Şablon kullanarak bir otomatik ölçeklendirme uygulaması dağıtma

[Azure Resource Manager şablonları](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) mükemmel şekilde toodeploy ilgili kaynaklar gruplarıdır. Bu öğretici derlemeler [dağıtmak basit ölçek kümesini](virtual-machine-scale-sets-mvss-start.md) ve nasıl toodeploy bir Azure Resource Manager şablonu kullanarak bir ölçekte basit otomatik ölçeklendirmeyi uygulama ayarlama açıklanmaktadır.  PowerShell'i, CLI veya hello portal kullanarak otomatik ölçeklendirmeyi ayarlayalım de ayarlayabilirsiniz. Daha fazla bilgi edinmek için bkz. [Otomatik ölçeklendirmeye genel bakış](virtual-machine-scale-sets-autoscale-overview.md).

## <a name="two-quickstart-templates"></a>İki hızlı başlangıç şablonu
Ölçek kümesi dağıtırken bir [VM Uzantısını](../virtual-machines/virtual-machines-windows-extensions-features.md) kullanarak bir platform görüntüsü üzerine yeni yazılım yükleyebilirsiniz. VM uzantısı, dağıtım sonrası yapılandırma ve Azure sanal makinelerinde uygulama dağıtımı gibi otomasyon görevleri sunan küçük bir uygulamadır. ' Nde sağlanan iki farklı örnek şablonları [Azure/azure-hızlı başlangıç-şablonları](https://github.com/Azure/azure-quickstart-templates) VM uzantıları kullanarak toodeploy ölçeği otomatik ölçeklendirmeyi uygulamasını nasıl ayarlanacağını gösterir.

### <a name="python-http-server-on-linux"></a>Linux’ta Python HTTP sunucusu
Merhaba [Linux Python HTTP sunucusunda](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) örnek şablonu Linux ölçek kümesinde çalışan Basit otomatik ölçeklendirmeyi uygulama dağıtır.  [Bottle](http://bottlepy.org/docs/dev/), bir Python web çerçevesi ve basit bir HTTP sunucusu, özel bir komut dosyası VM uzantısı kullanılarak ayarlanan hello ölçeğinde her bir VM üzerinde dağıtılır. tüm sanal makineler arasında ortalama CPU kullanımı % 60'den büyük olduğunda ve hello ortalama CPU kullanımı % 30'den az olduğunda ölçeklendirir hello ölçek ölçekler ayarlayın.

Ayrıca toohello ölçek kaynak hello kümesi *azuredeploy.json* örnek şablonu ayrıca sanal ağ, genel IP adresi, yük dengeleyici ve otomatik ölçeklendirme ayarlarını kaynakları bildirir.  Bir şablonda bu kaynakları oluşturma hakkında daha fazla bilgi edinmek için bkz. [Otomatik ölçeklendirmeli Linux ölçek kümesi](virtual-machine-scale-sets-linux-autoscale.md).

Merhaba, *azuredeploy.json* şablonu, hello `extensionProfile` hello özelliğinin `Microsoft.Compute/virtualMachineScaleSets` kaynağı özel betik uzantısı belirtir. `fileUris`Merhaba komut dosyaları konumunu belirtir. Bu durumda, iki dosyaları: *workserver.py*, basit bir HTTP sunucusu tanımlar ve *installserver.sh*Bottle yükler ve başlatır hello HTTP sunucusu. `commandToExecute`Merhaba ölçek kümesi dağıtıldıktan sonra hello komutu toorun belirtir.

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "lapextension",
                "properties": {
                  "publisher": "Microsoft.Azure.Extensions",
                  "type": "CustomScript",
                  "typeHandlerVersion": "2.0",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "fileUris": [
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
                    ],
                    "commandToExecute": "bash installserver.sh"
                  }
                }
              }
            ]
          }
```

### <a name="aspnet-mvc-application-on-windows"></a>Windows’da ASP.NET MVC uygulaması
Merhaba [ASP.NET MVC uygulaması Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) örnek şablonu IIS'de Windows ölçek kümesinde çalışan basit bir ASP.NET MVC uygulaması dağıtır.  IIS ve hello MVC uygulama dağıtılan hello kullanarak [PowerShell istenen durum yapılandırması (DSC)](virtual-machine-scale-sets-dsc.md) VM uzantısı.  Merhaba ölçek kümesinde ölçekler (VM örneği aynı anda) CPU kullanımı olduğunda % 50'den büyük 5 dakikadır. 

Ayrıca toohello ölçek kaynak hello kümesi *azuredeploy.json* örnek şablonu ayrıca sanal ağ, genel IP adresi, yük dengeleyici ve otomatik ölçeklendirme ayarlarını kaynakları bildirir. Bu şablon, uygulama yükseltme işlemini de gösterir.  Bir şablonda bu kaynakları oluşturma hakkında daha fazla bilgi edinmek için bkz. [Otomatik ölçeklendirmeli Windows ölçek kümesi](virtual-machine-scale-sets-windows-autoscale.md).

Merhaba, *azuredeploy.json* şablonu, hello `extensionProfile` hello özelliğinin `Microsoft.Compute/virtualMachineScaleSets` kaynağı belirtir bir [istenen durum yapılandırması (DSC)](virtual-machine-scale-sets-dsc.md) IIS ve varsayılan yükleyen uzantısı WebDeploy paketi Web uygulamasından.  Merhaba *IISInstall.ps1* komut dosyası IIS hello sanal makineye yükler ve hello bulunan *DSC* klasör.  Merhaba MVC web uygulaması hello bulunan *WebDeploy* klasör.  Merhaba yolları toohello yükleme betiği ve hello web uygulaması hello tanımlanmış `powershelldscZip` ve `webDeployPackage` hello parametrelerinde *azuredeploy.parameters.json* dosya. 

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Powershell.DSC",
                "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.9",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('powershelldscUpdateTagVersion')]",
                  "settings": {
                    "configuration": {
                      "url": "[variables('powershelldscZipFullPath')]",
                      "script": "IISInstall.ps1",
                      "function": "InstallIIS"
                    },
                    "configurationArguments": {
                      "nodeName": "localhost",
                      "WebDeployPackagePath": "[variables('webDeployPackageFullPath')]"
                    }
                  }
                }
              }
            ]
          }
```

## <a name="deploy-hello-template"></a>Merhaba şablonu dağıtma
Merhaba en basit yolu toodeploy hello [Linux Python HTTP sunucusunda](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) veya [ASP.NET MVC uygulaması Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) şablonudur toouse hello **tooAzure dağıtmak** düğmesi hello bulundu Merhaba readme dosyalarında github'da.  PowerShell veya Azure CLI toodeploy hello örnek şablonları de kullanabilirsiniz.

### <a name="powershell"></a>PowerShell
Kopya hello [Linux Python HTTP sunucusunda](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) veya [ASP.NET MVC uygulaması Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) hello GitHub deposuna tooa klasöründeki dosyaları, yerel bilgisayarınızda.  Açık hello *azuredeploy.parameters.json* hello dosya ve güncelleştirme hello varsayılan değerleri `vmssName`, `adminUsername`, ve `adminPassword` parametreleri. PowerShell Betiği çok aşağıdaki hello Kaydet*deploy.ps1* hello içinde hello aynı klasöre *azuredeploy.json* şablonu. toodeploy hello örnek çalıştırmak şablon hello *deploy.ps1* bir PowerShell komut penceresi betikten.

```powershell
param(
 [Parameter(Mandatory=$True)]
 [string]
 $subscriptionId,

 [Parameter(Mandatory=$True)]
 [string]
 $resourceGroupName,

 [string]
 $resourceGroupLocation,

 [Parameter(Mandatory=$True)]
 [string]
 $deploymentName,

 [string]
 $templateFilePath = "template.json",

 [string]
 $parametersFilePath = "parameters.json"
)

<#
.SYNOPSIS
    Registers RPs
#>
Function RegisterRP {
    Param(
        [string]$ResourceProviderNamespace
    )

    Write-Host "Registering resource provider '$ResourceProviderNamespace'";
    Register-AzureRmResourceProvider -ProviderNamespace $ResourceProviderNamespace;
}

#******************************************************************************
# Script body
# Execution begins here
#******************************************************************************
$ErrorActionPreference = "Stop"

# sign in
Write-Host "Logging in...";
Login-AzureRmAccount;

# select subscription
Write-Host "Selecting subscription '$subscriptionId'";
Select-AzureRmSubscription -SubscriptionID $subscriptionId;

# Register RPs
$resourceProviders = @("microsoft.compute","microsoft.insights","microsoft.network");
if($resourceProviders.length) {
    Write-Host "Registering resource providers"
    foreach($resourceProvider in $resourceProviders) {
        RegisterRP($resourceProvider);
    }
}

#Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $resourceGroupName -ErrorAction SilentlyContinue
if(!$resourceGroup)
{
    Write-Host "Resource group '$resourceGroupName' does not exist. toocreate a new resource group, please enter a location.";
    if(!$resourceGroupLocation) {
        $resourceGroupLocation = Read-Host "resourceGroupLocation";
    }
    Write-Host "Creating resource group '$resourceGroupName' in location '$resourceGroupLocation'";
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else{
    Write-Host "Using existing resource group '$resourceGroupName'";
}

# Start hello deployment
Write-Host "Starting deployment...";
if(Test-Path $parametersFilePath) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath -TemplateParameterFile $parametersFilePath;
} else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath;
}
```

### <a name="azure-cli"></a>Azure CLI
```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely toocause confusing bugs when looping arrays or arguments (e.g. $@)

usage() { echo "Usage: $0 -i <subscriptionId> -g <resourceGroupName> -n <deploymentName> -l <resourceGroupLocation>" 1>&2; exit 1; }

declare subscriptionId=""
declare resourceGroupName=""
declare deploymentName=""
declare resourceGroupLocation=""

# Initialize parameters specified from command line
while getopts ":i:g:n:l:" arg; do
    case "${arg}" in
        i)
            subscriptionId=${OPTARG}
            ;;
        g)
            resourceGroupName=${OPTARG}
            ;;
        n)
            deploymentName=${OPTARG}
            ;;
        l)
            resourceGroupLocation=${OPTARG}
            ;;
        esac
done
shift $((OPTIND-1))

#Prompt for parameters is some required parameters are missing
if [[ -z "$subscriptionId" ]]; then
    echo "Subscription Id:"
    read subscriptionId
    [[ "${subscriptionId:?}" ]]
fi

if [[ -z "$resourceGroupName" ]]; then
    echo "ResourceGroupName:"
    read resourceGroupName
    [[ "${resourceGroupName:?}" ]]
fi

if [[ -z "$deploymentName" ]]; then
    echo "DeploymentName:"
    read deploymentName
fi

if [[ -z "$resourceGroupLocation" ]]; then
    echo "Enter a location below toocreate a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file toobe used
templateFilePath="template.json"

if [ ! -f "$templateFilePath" ]; then
    echo "$templateFilePath not found"
    exit 1
fi

#parameter file path
parametersFilePath="parameters.json"

if [ ! -f "$parametersFilePath" ]; then
    echo "$parametersFilePath not found"
    exit 1
fi

if [ -z "$subscriptionId" ] || [ -z "$resourceGroupName" ] || [ -z "$deploymentName" ]; then
    echo "Either one of subscriptionId, resourceGroupName, deploymentName is empty"
    usage
fi

#login tooazure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set hello default subscription id
az account set --name $subscriptionId

set +e

#Check for existing RG
az group show $resourceGroupName 1> /dev/null

if [ $? != 0 ]; then
    echo "Resource group with name" $resourceGroupName "could not be found. Creating new resource group.."
    set -e
    (
        set -x
        az group create --name $resourceGroupName --location $resourceGroupLocation 1> /dev/null
    )
    else
    echo "Using existing resource group..."
fi

#Start deployment
echo "Starting deployment..."
(
    set -x
    az group deployment create --name $deploymentName --resource-group $resourceGroupName --template-file $templateFilePath --parameters $parametersFilePath
)

if [ $?  == 0 ];
 then
    echo "Template has been successfully deployed"
fi
```

## <a name="next-steps"></a>Sonraki adımlar

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
