---
title: "Azure CLI betik örnek - şablon dağıtma | Microsoft Docs"
description: "Bir Azure Resource Manager şablonunu dağıtmak için örnek komut dosyası."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 974230f349aec46fde58e69658e05a13bff4296f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-manager-template-deployment---azure-cli-script"></a><span data-ttu-id="98bfc-103">Azure Resource Manager şablon dağıtımı - Azure CLI komut dosyası</span><span class="sxs-lookup"><span data-stu-id="98bfc-103">Azure Resource Manager template deployment - Azure CLI script</span></span>

<span data-ttu-id="98bfc-104">Bu komut dosyasını bir Resource Manager şablonu bir kaynak grubu aboneliğinizde dağıtır.</span><span class="sxs-lookup"><span data-stu-id="98bfc-104">This script deploys a Resource Manager template to a resource group in your subscription.</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="98bfc-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="98bfc-105">Sample script</span></span>

```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely to cause confusing bugs when looping arrays or arguments (e.g. $@)

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
    echo "Enter a location below to create a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file to be used
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

#login to azure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set the default subscription id
az account set --subscription $subscriptionId

#Check for existing RG
if [ $(az group exists --name $resourceGroupName) == 'false' ]; then
    echo "Resource group with name" $resourceGroupName "could not be found. Creating new resource group.."
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

## <a name="clean-up-deployment"></a><span data-ttu-id="98bfc-106">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="98bfc-106">Clean up deployment</span></span> 

<span data-ttu-id="98bfc-107">Kaynak grubu ve tüm kaynaklarını kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="98bfc-107">Run the following command to remove the resource group and all its resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="98bfc-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="98bfc-108">Script explanation</span></span>

<span data-ttu-id="98bfc-109">Bu komut dosyası dağıtımı oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="98bfc-109">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="98bfc-110">Komut belirli belgeleri tablo bağlanan her öğe.</span><span class="sxs-lookup"><span data-stu-id="98bfc-110">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="98bfc-111">Komut</span><span class="sxs-lookup"><span data-stu-id="98bfc-111">Command</span></span> | <span data-ttu-id="98bfc-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="98bfc-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="98bfc-113">az grubu var.</span><span class="sxs-lookup"><span data-stu-id="98bfc-113">az group exists</span></span>](/cli/azure/group#exists) | <span data-ttu-id="98bfc-114">Kaynak grubu mevcut olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="98bfc-114">Checks whether resource group exists.</span></span> |
| [<span data-ttu-id="98bfc-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="98bfc-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="98bfc-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="98bfc-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="98bfc-117">az grup dağıtımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="98bfc-117">az group deployment create</span></span>](/cli/azure/group/deployment#create) | <span data-ttu-id="98bfc-118">Bir dağıtımı başlatın.</span><span class="sxs-lookup"><span data-stu-id="98bfc-118">Start a deployment.</span></span>  |
| [<span data-ttu-id="98bfc-119">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="98bfc-119">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="98bfc-120">Tüm kaynaklar da dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="98bfc-120">Deletes a resource group including all its resources.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="98bfc-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="98bfc-121">Next steps</span></span>
* <span data-ttu-id="98bfc-122">Şablon dağıtımı için giriş için bkz [Resource Manager şablonları ve Azure PowerShell ile kaynakları dağıtmak](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="98bfc-122">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="98bfc-123">Bir SAS belirteci gerektiren şablonu dağıtma hakkında daha fazla bilgi için bkz: [dağıtma özel şablonu SAS belirteci ile](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="98bfc-123">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="98bfc-124">Şablonda parametreleri tanımlamak için bkz: [şablonları yazma](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="98bfc-124">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="98bfc-125">Kuruluşların abonelikleri etkili bir şekilde yönetmek için Resource Manager'ı nasıl kullanabileceği hakkında yönergeler için bkz. [Azure kurumsal iskelesi: öngörücü abonelik idaresi](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="98bfc-125">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

