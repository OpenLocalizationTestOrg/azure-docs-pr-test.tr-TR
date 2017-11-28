---
title: "aaaAzure PowerShell komut dosyası örneği - bir web uygulaması oluşturma ve yerel bir Git deposu koddan dağıtma | Microsoft Docs"
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
ms.openlocfilehash: a90996658bf0b609315460324d0dcd3a411a6512
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="df8aa-103">Bir web uygulaması oluşturma ve yerel bir Git deposu koddan dağıtma</span><span class="sxs-lookup"><span data-stu-id="df8aa-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="df8aa-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur ve bir yerel Git deposu, web uygulama kodunuzda dağıtır.</span><span class="sxs-lookup"><span data-stu-id="df8aa-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="df8aa-105">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](/powershell/azure/overview)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="df8aa-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="df8aa-106">Ayrıca, uygulama kodunuzun yerel bir Git deposu kaydedilen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="df8aa-106">Also, your application code needs toobe committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="df8aa-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="df8aa-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]

## <a name="clean-up-deployment"></a><span data-ttu-id="df8aa-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="df8aa-108">Clean up deployment</span></span> 

<span data-ttu-id="df8aa-109">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, web uygulaması ve tüm ilişkili kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="df8aa-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="df8aa-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="df8aa-110">Script explanation</span></span>

<span data-ttu-id="df8aa-111">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="df8aa-111">This script uses hello following commands.</span></span> <span data-ttu-id="df8aa-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="df8aa-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="df8aa-113">Komut</span><span class="sxs-lookup"><span data-stu-id="df8aa-113">Command</span></span> | <span data-ttu-id="df8aa-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="df8aa-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="df8aa-115">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="df8aa-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="df8aa-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="df8aa-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="df8aa-117">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="df8aa-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="df8aa-118">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="df8aa-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="df8aa-119">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="df8aa-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="df8aa-120">Bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="df8aa-120">Creates a web app.</span></span> |
| [<span data-ttu-id="df8aa-121">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="df8aa-121">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="df8aa-122">Bir kaynak bir kaynak grubu olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="df8aa-122">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="df8aa-123">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="df8aa-123">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="df8aa-124">Web uygulamanızın yayımlama profili alın.</span><span class="sxs-lookup"><span data-stu-id="df8aa-124">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="df8aa-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="df8aa-125">Next steps</span></span>

<span data-ttu-id="df8aa-126">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="df8aa-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="df8aa-127">Azure App Service Web Apps ek Azure Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="df8aa-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
