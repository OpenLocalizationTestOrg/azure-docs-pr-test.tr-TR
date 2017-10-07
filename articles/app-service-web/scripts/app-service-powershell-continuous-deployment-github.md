---
title: "PowerShell komut dosyası örneği - aaaAzure github'dan sürekli dağıtım bir web uygulaması oluşturma | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - github'dan sürekli dağıtımı ile bir web uygulaması oluşturma"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 42f901f8-02f7-4869-b22d-d99ef59f874c
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: c2f260a06bce9af6d11ad4033931d3dc18da8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="f401b-103">Sürekli dağıtım github'dan bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="f401b-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="f401b-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur ve GitHub depodan sürekli dağıtım ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f401b-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="f401b-105">Sürekli dağıtım olmadan GitHub dağıtımı için bkz: [bir web uygulaması oluşturma ve dağıtma github'dan kod](app-service-powershell-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="f401b-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span></span>

<span data-ttu-id="f401b-106">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f401b-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="f401b-107">Ayrıca, emin olun:</span><span class="sxs-lookup"><span data-stu-id="f401b-107">Also, ensure that:</span></span>

- <span data-ttu-id="f401b-108">Hello kullanarak Azure ile bağlantı oluşturuldu `az login` komutu.</span><span class="sxs-lookup"><span data-stu-id="f401b-108">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="f401b-109">sahip olduğunuz bir genel veya özel GitHub deposunda Hello uygulama kodudur.</span><span class="sxs-lookup"><span data-stu-id="f401b-109">hello application code is in a public or private GitHub repository that you own.</span></span>
- <span data-ttu-id="f401b-110">Sahip olduğunuz [GitHub hesabınızda bir erişim belirteci oluşturulan](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span><span class="sxs-lookup"><span data-stu-id="f401b-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span></span>

## <a name="sample-script"></a><span data-ttu-id="f401b-111">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="f401b-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f401b-112">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="f401b-112">Clean up deployment</span></span> 

<span data-ttu-id="f401b-113">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, web uygulaması ve tüm ilişkili kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="f401b-113">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="f401b-114">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="f401b-114">Script explanation</span></span>

<span data-ttu-id="f401b-115">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="f401b-115">This script uses hello following commands.</span></span> <span data-ttu-id="f401b-116">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="f401b-116">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f401b-117">Komut</span><span class="sxs-lookup"><span data-stu-id="f401b-117">Command</span></span> | <span data-ttu-id="f401b-118">Notlar</span><span class="sxs-lookup"><span data-stu-id="f401b-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f401b-119">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f401b-119">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f401b-120">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f401b-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f401b-121">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="f401b-121">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="f401b-122">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f401b-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f401b-123">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="f401b-123">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="f401b-124">Bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f401b-124">Creates a web app.</span></span> |
| [<span data-ttu-id="f401b-125">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="f401b-125">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="f401b-126">Bir kaynak bir kaynak grubu olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="f401b-126">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f401b-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f401b-127">Next steps</span></span>

<span data-ttu-id="f401b-128">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f401b-128">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f401b-129">Azure App Service Web Apps ek Azure Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f401b-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
