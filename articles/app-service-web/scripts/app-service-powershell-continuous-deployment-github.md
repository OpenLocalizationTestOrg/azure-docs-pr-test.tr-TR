---
title: "Azure PowerShell Betiği örnek - github'dan sürekli dağıtımı ile bir web uygulaması oluşturma | Microsoft Docs"
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
ms.openlocfilehash: fc594a94bb64ceb88370be8617036a73402ade4e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="b7fcc-103">Sürekli dağıtım github'dan bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b7fcc-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="b7fcc-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur ve GitHub depodan sürekli dağıtım ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b7fcc-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="b7fcc-105">Sürekli dağıtım olmadan GitHub dağıtımı için bkz: [bir web uygulaması oluşturma ve dağıtma github'dan kod](app-service-powershell-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="b7fcc-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span></span>

<span data-ttu-id="b7fcc-106">Gerekirse, bulunan yönergeleri kullanarak Azure PowerShell'i yükleme [Azure PowerShell Kılavuzu](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b7fcc-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="b7fcc-107">Ayrıca, emin olun:</span><span class="sxs-lookup"><span data-stu-id="b7fcc-107">Also, ensure that:</span></span>

- <span data-ttu-id="b7fcc-108">Azure ile bir bağlantı kullanılarak oluşturulup oluşturulmadığını `az login` komutu.</span><span class="sxs-lookup"><span data-stu-id="b7fcc-108">A connection with Azure has been created using the `az login` command.</span></span>
- <span data-ttu-id="b7fcc-109">Uygulama, sahip olduğunuz bir genel veya özel GitHub deposunda kodudur.</span><span class="sxs-lookup"><span data-stu-id="b7fcc-109">The application code is in a public or private GitHub repository that you own.</span></span>
- <span data-ttu-id="b7fcc-110">Sahip olduğunuz [GitHub hesabınızda bir erişim belirteci oluşturulan](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span><span class="sxs-lookup"><span data-stu-id="b7fcc-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span></span>

## <a name="sample-script"></a><span data-ttu-id="b7fcc-111">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="b7fcc-111">Sample script</span></span>

<span data-ttu-id="b7fcc-112">[!code-powershell[Ana](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "github'dan sürekli dağıtımı ile bir web uygulaması oluşturma")]</span><span class="sxs-lookup"><span data-stu-id="b7fcc-112">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b7fcc-113">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="b7fcc-113">Clean up deployment</span></span> 

<span data-ttu-id="b7fcc-114">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu, web uygulaması ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b7fcc-114">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="b7fcc-115">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="b7fcc-115">Script explanation</span></span>

<span data-ttu-id="b7fcc-116">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="b7fcc-116">This script uses the following commands.</span></span> <span data-ttu-id="b7fcc-117">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="b7fcc-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b7fcc-118">Komut</span><span class="sxs-lookup"><span data-stu-id="b7fcc-118">Command</span></span> | <span data-ttu-id="b7fcc-119">Notlar</span><span class="sxs-lookup"><span data-stu-id="b7fcc-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b7fcc-120">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b7fcc-120">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b7fcc-121">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b7fcc-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b7fcc-122">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="b7fcc-122">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="b7fcc-123">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b7fcc-123">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="b7fcc-124">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="b7fcc-124">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="b7fcc-125">Bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b7fcc-125">Creates a web app.</span></span> |
| [<span data-ttu-id="b7fcc-126">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="b7fcc-126">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="b7fcc-127">Bir kaynak bir kaynak grubu olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="b7fcc-127">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b7fcc-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b7fcc-128">Next steps</span></span>

<span data-ttu-id="b7fcc-129">Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b7fcc-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b7fcc-130">Azure App Service Web Apps ek Azure Powershell örnekleri bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b7fcc-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
