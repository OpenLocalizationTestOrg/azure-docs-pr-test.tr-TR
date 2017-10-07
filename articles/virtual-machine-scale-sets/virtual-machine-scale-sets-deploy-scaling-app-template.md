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
# <a name="deploy-an-autoscaling-app-using-a-template"></a><span data-ttu-id="f6ac9-103">Şablon kullanarak bir otomatik ölçeklendirme uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="f6ac9-103">Deploy an autoscaling app using a template</span></span>

<span data-ttu-id="f6ac9-104">[Azure Resource Manager şablonları](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) mükemmel şekilde toodeploy ilgili kaynaklar gruplarıdır.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way toodeploy groups of related resources.</span></span> <span data-ttu-id="f6ac9-105">Bu öğretici derlemeler [dağıtmak basit ölçek kümesini](virtual-machine-scale-sets-mvss-start.md) ve nasıl toodeploy bir Azure Resource Manager şablonu kullanarak bir ölçekte basit otomatik ölçeklendirmeyi uygulama ayarlama açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-105">This tutorial builds on [Deploy a simple scale set](virtual-machine-scale-sets-mvss-start.md) and describes how toodeploy a simple autoscaling application on a scale set using an Azure Resource Manager template.</span></span>  <span data-ttu-id="f6ac9-106">PowerShell'i, CLI veya hello portal kullanarak otomatik ölçeklendirmeyi ayarlayalım de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-106">You can also set up autoscaling using PowerShell, CLI, or hello portal.</span></span> <span data-ttu-id="f6ac9-107">Daha fazla bilgi edinmek için bkz. [Otomatik ölçeklendirmeye genel bakış](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f6ac9-107">For more information, see [Autoscale overview](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

## <a name="two-quickstart-templates"></a><span data-ttu-id="f6ac9-108">İki hızlı başlangıç şablonu</span><span class="sxs-lookup"><span data-stu-id="f6ac9-108">Two quickstart templates</span></span>
<span data-ttu-id="f6ac9-109">Ölçek kümesi dağıtırken bir [VM Uzantısını](../virtual-machines/virtual-machines-windows-extensions-features.md) kullanarak bir platform görüntüsü üzerine yeni yazılım yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-109">When you deploy a scale set you can install new software on a platform image using a [VM Extension](../virtual-machines/virtual-machines-windows-extensions-features.md).</span></span> <span data-ttu-id="f6ac9-110">VM uzantısı, dağıtım sonrası yapılandırma ve Azure sanal makinelerinde uygulama dağıtımı gibi otomasyon görevleri sunan küçük bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-110">A VM extension is a small application that provides post-deployment configuration and automation tasks on Azure virtual machines, such as deploying an app.</span></span> <span data-ttu-id="f6ac9-111">' Nde sağlanan iki farklı örnek şablonları [Azure/azure-hızlı başlangıç-şablonları](https://github.com/Azure/azure-quickstart-templates) VM uzantıları kullanarak toodeploy ölçeği otomatik ölçeklendirmeyi uygulamasını nasıl ayarlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-111">Two different sample templates are provided in [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) which show how toodeploy an autoscaling application onto a scale set using VM extensions.</span></span>

### <a name="python-http-server-on-linux"></a><span data-ttu-id="f6ac9-112">Linux’ta Python HTTP sunucusu</span><span class="sxs-lookup"><span data-stu-id="f6ac9-112">Python HTTP server on Linux</span></span>
<span data-ttu-id="f6ac9-113">Merhaba [Linux Python HTTP sunucusunda](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) örnek şablonu Linux ölçek kümesinde çalışan Basit otomatik ölçeklendirmeyi uygulama dağıtır.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-113">hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) sample template deploys a simple autoscaling application running on a Linux scale set.</span></span>  <span data-ttu-id="f6ac9-114">[Bottle](http://bottlepy.org/docs/dev/), bir Python web çerçevesi ve basit bir HTTP sunucusu, özel bir komut dosyası VM uzantısı kullanılarak ayarlanan hello ölçeğinde her bir VM üzerinde dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-114">[Bottle](http://bottlepy.org/docs/dev/), a Python web framework, and a simple HTTP server are deployed on each VM in hello scale set using a custom script VM extension.</span></span> <span data-ttu-id="f6ac9-115">tüm sanal makineler arasında ortalama CPU kullanımı % 60'den büyük olduğunda ve hello ortalama CPU kullanımı % 30'den az olduğunda ölçeklendirir hello ölçek ölçekler ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-115">hello scale set scales up when average CPU utilization across all VMs is greater than 60% and scales down when hello average CPU utilization is less than 30%.</span></span>

<span data-ttu-id="f6ac9-116">Ayrıca toohello ölçek kaynak hello kümesi *azuredeploy.json* örnek şablonu ayrıca sanal ağ, genel IP adresi, yük dengeleyici ve otomatik ölçeklendirme ayarlarını kaynakları bildirir.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-116">In addition toohello scale set resource, hello *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span>  <span data-ttu-id="f6ac9-117">Bir şablonda bu kaynakları oluşturma hakkında daha fazla bilgi edinmek için bkz. [Otomatik ölçeklendirmeli Linux ölçek kümesi](virtual-machine-scale-sets-linux-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="f6ac9-117">For more information on creating these resources in a template, see [Linux scale set with autoscale](virtual-machine-scale-sets-linux-autoscale.md).</span></span>

<span data-ttu-id="f6ac9-118">Merhaba, *azuredeploy.json* şablonu, hello `extensionProfile` hello özelliğinin `Microsoft.Compute/virtualMachineScaleSets` kaynağı özel betik uzantısı belirtir.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-118">In hello *azuredeploy.json* template, hello `extensionProfile` property of hello `Microsoft.Compute/virtualMachineScaleSets` resource specifies a custom script extension.</span></span> <span data-ttu-id="f6ac9-119">`fileUris`Merhaba komut dosyaları konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-119">`fileUris` specifies hello script(s) location.</span></span> <span data-ttu-id="f6ac9-120">Bu durumda, iki dosyaları: *workserver.py*, basit bir HTTP sunucusu tanımlar ve *installserver.sh*Bottle yükler ve başlatır hello HTTP sunucusu.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-120">In this case, two files: *workserver.py*, which defines a simple HTTP server, and *installserver.sh*, which installs Bottle and starts hello HTTP server.</span></span> <span data-ttu-id="f6ac9-121">`commandToExecute`Merhaba ölçek kümesi dağıtıldıktan sonra hello komutu toorun belirtir.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-121">`commandToExecute` specifies hello command toorun after hello scale set has been deployed.</span></span>

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

### <a name="aspnet-mvc-application-on-windows"></a><span data-ttu-id="f6ac9-122">Windows’da ASP.NET MVC uygulaması</span><span class="sxs-lookup"><span data-stu-id="f6ac9-122">ASP.NET MVC application on Windows</span></span>
<span data-ttu-id="f6ac9-123">Merhaba [ASP.NET MVC uygulaması Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) örnek şablonu IIS'de Windows ölçek kümesinde çalışan basit bir ASP.NET MVC uygulaması dağıtır.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-123">hello [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) sample template deploys a simple ASP.NET MVC app running in IIS on Windows scale set.</span></span>  <span data-ttu-id="f6ac9-124">IIS ve hello MVC uygulama dağıtılan hello kullanarak [PowerShell istenen durum yapılandırması (DSC)](virtual-machine-scale-sets-dsc.md) VM uzantısı.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-124">IIS and hello MVC app are deployed using hello [PowerShell desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) VM extension.</span></span>  <span data-ttu-id="f6ac9-125">Merhaba ölçek kümesinde ölçekler (VM örneği aynı anda) CPU kullanımı olduğunda % 50'den büyük 5 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-125">hello scale set scales up (on VM instance at a time) when CPU utilization is greater than 50% for 5 minutes.</span></span> 

<span data-ttu-id="f6ac9-126">Ayrıca toohello ölçek kaynak hello kümesi *azuredeploy.json* örnek şablonu ayrıca sanal ağ, genel IP adresi, yük dengeleyici ve otomatik ölçeklendirme ayarlarını kaynakları bildirir.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-126">In addition toohello scale set resource, hello *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span> <span data-ttu-id="f6ac9-127">Bu şablon, uygulama yükseltme işlemini de gösterir.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-127">This template also demonstrates application upgrade.</span></span>  <span data-ttu-id="f6ac9-128">Bir şablonda bu kaynakları oluşturma hakkında daha fazla bilgi edinmek için bkz. [Otomatik ölçeklendirmeli Windows ölçek kümesi](virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="f6ac9-128">For more information on creating these resources in a template, see [Windows scale set with autoscale](virtual-machine-scale-sets-windows-autoscale.md).</span></span>

<span data-ttu-id="f6ac9-129">Merhaba, *azuredeploy.json* şablonu, hello `extensionProfile` hello özelliğinin `Microsoft.Compute/virtualMachineScaleSets` kaynağı belirtir bir [istenen durum yapılandırması (DSC)](virtual-machine-scale-sets-dsc.md) IIS ve varsayılan yükleyen uzantısı WebDeploy paketi Web uygulamasından.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-129">In hello *azuredeploy.json* template, hello `extensionProfile` property of hello `Microsoft.Compute/virtualMachineScaleSets` resource specifies a [desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) extension which installs IIS and a default web app from a WebDeploy package.</span></span>  <span data-ttu-id="f6ac9-130">Merhaba *IISInstall.ps1* komut dosyası IIS hello sanal makineye yükler ve hello bulunan *DSC* klasör.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-130">hello *IISInstall.ps1* script installs IIS on hello virtual machine and is found in hello *DSC* folder.</span></span>  <span data-ttu-id="f6ac9-131">Merhaba MVC web uygulaması hello bulunan *WebDeploy* klasör.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-131">hello MVC web app is found in hello *WebDeploy* folder.</span></span>  <span data-ttu-id="f6ac9-132">Merhaba yolları toohello yükleme betiği ve hello web uygulaması hello tanımlanmış `powershelldscZip` ve `webDeployPackage` hello parametrelerinde *azuredeploy.parameters.json* dosya.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-132">hello paths toohello install script and hello web app are defined in hello `powershelldscZip` and `webDeployPackage` parameters in hello *azuredeploy.parameters.json* file.</span></span> 

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

## <a name="deploy-hello-template"></a><span data-ttu-id="f6ac9-133">Merhaba şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="f6ac9-133">Deploy hello template</span></span>
<span data-ttu-id="f6ac9-134">Merhaba en basit yolu toodeploy hello [Linux Python HTTP sunucusunda](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) veya [ASP.NET MVC uygulaması Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) şablonudur toouse hello **tooAzure dağıtmak** düğmesi hello bulundu Merhaba readme dosyalarında github'da.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-134">hello simplest way toodeploy hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) template is toouse hello **Deploy tooAzure** button found in hello in hello readme files in GitHub.</span></span>  <span data-ttu-id="f6ac9-135">PowerShell veya Azure CLI toodeploy hello örnek şablonları de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-135">You can also use PowerShell or Azure CLI toodeploy hello sample templates.</span></span>

### <a name="powershell"></a><span data-ttu-id="f6ac9-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6ac9-136">PowerShell</span></span>
<span data-ttu-id="f6ac9-137">Kopya hello [Linux Python HTTP sunucusunda](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) veya [ASP.NET MVC uygulaması Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) hello GitHub deposuna tooa klasöründeki dosyaları, yerel bilgisayarınızda.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-137">Copy hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) files from hello GitHub repo tooa folder on your local computer.</span></span>  <span data-ttu-id="f6ac9-138">Açık hello *azuredeploy.parameters.json* hello dosya ve güncelleştirme hello varsayılan değerleri `vmssName`, `adminUsername`, ve `adminPassword` parametreleri.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-138">Open hello *azuredeploy.parameters.json* file and update hello default values of hello `vmssName`, `adminUsername`, and `adminPassword` parameters.</span></span> <span data-ttu-id="f6ac9-139">PowerShell Betiği çok aşağıdaki hello Kaydet*deploy.ps1* hello içinde hello aynı klasöre *azuredeploy.json* şablonu.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-139">Save hello following PowerShell script too*deploy.ps1* in hello same folder as hello *azuredeploy.json* template.</span></span> <span data-ttu-id="f6ac9-140">toodeploy hello örnek çalıştırmak şablon hello *deploy.ps1* bir PowerShell komut penceresi betikten.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-140">toodeploy hello sample template run hello *deploy.ps1* script from a PowerShell command window.</span></span>

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

### <a name="azure-cli"></a><span data-ttu-id="f6ac9-141">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f6ac9-141">Azure CLI</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="f6ac9-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f6ac9-142">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
