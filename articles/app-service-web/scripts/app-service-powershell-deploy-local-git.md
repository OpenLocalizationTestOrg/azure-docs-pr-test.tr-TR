---
title: "Azure PowerShell Betiği örnek - bir web uygulaması oluşturma ve yerel bir Git deposu koddan dağıtma | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - bir web uygulaması oluşturma ve yerel bir Git deposu koddan dağıtma"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5a927f23-8e70-45fd-9aae-980d4e7a007d
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 855b8c643bf2a742e763bda2e2c21c6a86331aac
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="a9bb9-103">Bir web uygulaması oluşturma ve yerel bir Git deposu koddan dağıtma</span><span class="sxs-lookup"><span data-stu-id="a9bb9-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="a9bb9-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur ve bir yerel Git deposu, web uygulama kodunuzda dağıtır.</span><span class="sxs-lookup"><span data-stu-id="a9bb9-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="a9bb9-105">Gerekirse, bulunan yönergeleri kullanarak Azure PowerShell'i yükleme [Azure PowerShell Kılavuzu](/powershell/azure/overview)ve ardından çalıştırın `Login-AzureRmAccount` Azure ile bir bağlantı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="a9bb9-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="a9bb9-106">Ayrıca, uygulama kodunuz yerel bir Git deposu kaydedilmiş gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9bb9-106">Also, your application code needs to be committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="a9bb9-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="a9bb9-107">Sample script</span></span>

<span data-ttu-id="a9bb9-108">[!code-powershell[Ana](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "bir web uygulaması oluşturma ve yerel bir Git deposu koddan dağıtma")]</span><span class="sxs-lookup"><span data-stu-id="a9bb9-108">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a9bb9-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="a9bb9-109">Clean up deployment</span></span> 

<span data-ttu-id="a9bb9-110">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu, web uygulaması ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a9bb9-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="a9bb9-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="a9bb9-111">Script explanation</span></span>

<span data-ttu-id="a9bb9-112">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="a9bb9-112">This script uses the following commands.</span></span> <span data-ttu-id="a9bb9-113">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="a9bb9-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a9bb9-114">Komut</span><span class="sxs-lookup"><span data-stu-id="a9bb9-114">Command</span></span> | <span data-ttu-id="a9bb9-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="a9bb9-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a9bb9-116">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a9bb9-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a9bb9-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a9bb9-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a9bb9-118">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="a9bb9-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="a9bb9-119">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a9bb9-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="a9bb9-120">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="a9bb9-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="a9bb9-121">Bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a9bb9-121">Creates a web app.</span></span> |
| [<span data-ttu-id="a9bb9-122">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="a9bb9-122">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="a9bb9-123">Bir kaynak bir kaynak grubu olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="a9bb9-123">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="a9bb9-124">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="a9bb9-124">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="a9bb9-125">Web uygulamanızın yayımlama profili alın.</span><span class="sxs-lookup"><span data-stu-id="a9bb9-125">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a9bb9-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a9bb9-126">Next steps</span></span>

<span data-ttu-id="a9bb9-127">Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a9bb9-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a9bb9-128">Azure App Service Web Apps ek Azure Powershell örnekleri bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a9bb9-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
