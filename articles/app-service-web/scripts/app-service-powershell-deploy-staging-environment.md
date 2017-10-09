---
title: "aaaAzure PowerShell komut dosyası örneği - bir web uygulaması oluşturma ve ortam hazırlama kodu tooa dağıtma | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - bir web uygulaması oluşturma ve ortam hazırlama kodu tooa dağıtma"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 27cf0680-c3a9-4a58-9f71-6dec09f6b874
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5c74b962955770637173f1fd4f49342fec54ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="124a3-103">Bir web uygulaması oluşturma ve ortam hazırlama kodu tooa dağıtma</span><span class="sxs-lookup"><span data-stu-id="124a3-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="124a3-104">Bu örnek betik "Hazırlama" adlı bir ek dağıtım yuvası ile App Service'te bir web uygulaması oluşturur ve ardından "yuvası Hazırlama" örnek uygulama toohello dağıtır.</span><span class="sxs-lookup"><span data-stu-id="124a3-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

<span data-ttu-id="124a3-105">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](/powershell/azure/overview)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="124a3-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="124a3-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="124a3-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code tooa staging environment")]

## <a name="clean-up-deployment"></a><span data-ttu-id="124a3-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="124a3-107">Clean up deployment</span></span> 

<span data-ttu-id="124a3-108">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, web uygulaması ve tüm ilişkili kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="124a3-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="124a3-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="124a3-109">Script explanation</span></span>

<span data-ttu-id="124a3-110">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="124a3-110">This script uses hello following commands.</span></span> <span data-ttu-id="124a3-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="124a3-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="124a3-112">Komut</span><span class="sxs-lookup"><span data-stu-id="124a3-112">Command</span></span> | <span data-ttu-id="124a3-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="124a3-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="124a3-114">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="124a3-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="124a3-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="124a3-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="124a3-116">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="124a3-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="124a3-117">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="124a3-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="124a3-118">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="124a3-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="124a3-119">Bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="124a3-119">Creates a web app.</span></span> |
| [<span data-ttu-id="124a3-120">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="124a3-120">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="124a3-121">Bir uygulama hizmeti planı toochange fiyatlandırma katmanı değiştirir.</span><span class="sxs-lookup"><span data-stu-id="124a3-121">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="124a3-122">AzureRmWebAppSlot yeni</span><span class="sxs-lookup"><span data-stu-id="124a3-122">New-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/new-azurermwebappslot) | <span data-ttu-id="124a3-123">Bir web uygulaması için bir dağıtım yuvası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="124a3-123">Creates a deployment slot for a web app.</span></span> |
| [<span data-ttu-id="124a3-124">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="124a3-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="124a3-125">Bir kaynak bir kaynak grubu olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="124a3-125">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="124a3-126">Takas AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="124a3-126">Swap-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/swap-azurermwebappslot) | <span data-ttu-id="124a3-127">Web uygulamanızın dağıtım yuvası üretime değiştirir.</span><span class="sxs-lookup"><span data-stu-id="124a3-127">Swaps a web app's deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="124a3-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="124a3-128">Next steps</span></span>

<span data-ttu-id="124a3-129">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="124a3-129">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="124a3-130">Azure App Service Web Apps ek Azure Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="124a3-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
