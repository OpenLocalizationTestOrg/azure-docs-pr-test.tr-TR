---
title: "Azure PowerShell Betiği örnek - İzleyici web sunucu günlükleri ile bir web uygulaması | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - İzleyici web sunucu günlükleri ile bir web uygulaması"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5805d7cd-9e56-4eba-bd85-75b013690ff5
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 34a3dd318cb9896342fce870922ecd113b3ed08d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="6ad8f-103">Web sunucu günlükleri ile bir web uygulaması izleme</span><span class="sxs-lookup"><span data-stu-id="6ad8f-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="6ad8f-104">Bu senaryoda, bir kaynak grubu, uygulama hizmeti planı, web uygulaması oluşturmak ve web sunucusu günlüklerini etkinleştirmek için web uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6ad8f-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span></span> <span data-ttu-id="6ad8f-105">Ardından, gözden geçirme için günlük dosyalarını indirir.</span><span class="sxs-lookup"><span data-stu-id="6ad8f-105">You will then download the log files for review.</span></span>

<span data-ttu-id="6ad8f-106">Gerekirse, bulunan yönergeleri kullanarak Azure PowerShell'i yükleme [Azure PowerShell Kılavuzu](/powershell/azure/overview)ve ardından çalıştırın `Login-AzureRmAccount` Azure ile bir bağlantı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="6ad8f-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="6ad8f-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="6ad8f-107">Sample script</span></span>

<span data-ttu-id="6ad8f-108">[!code-powershell[Ana](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "web sunucu günlükleri ile bir web uygulaması izleme")]</span><span class="sxs-lookup"><span data-stu-id="6ad8f-108">[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6ad8f-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="6ad8f-109">Clean up deployment</span></span> 

<span data-ttu-id="6ad8f-110">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu, web uygulaması ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6ad8f-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="6ad8f-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="6ad8f-111">Script explanation</span></span>

<span data-ttu-id="6ad8f-112">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="6ad8f-112">This script uses the following commands.</span></span> <span data-ttu-id="6ad8f-113">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="6ad8f-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6ad8f-114">Komut</span><span class="sxs-lookup"><span data-stu-id="6ad8f-114">Command</span></span> | <span data-ttu-id="6ad8f-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="6ad8f-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6ad8f-116">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6ad8f-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="6ad8f-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6ad8f-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6ad8f-118">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="6ad8f-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="6ad8f-119">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6ad8f-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="6ad8f-120">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="6ad8f-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="6ad8f-121">Bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6ad8f-121">Creates a web app.</span></span> |
| [<span data-ttu-id="6ad8f-122">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="6ad8f-122">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="6ad8f-123">Web uygulamanızın yapılandırmasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="6ad8f-123">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="6ad8f-124">Get-AzureRMWebAppMetrics</span><span class="sxs-lookup"><span data-stu-id="6ad8f-124">Get-AzureRMWebAppMetrics</span></span>](/powershell/module/azurerm.websites/get-azurermwebappmetrics) | <span data-ttu-id="6ad8f-125">Web uygulamanızın ölçümleri alır.</span><span class="sxs-lookup"><span data-stu-id="6ad8f-125">Gets a web app's metrics.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6ad8f-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6ad8f-126">Next steps</span></span>

<span data-ttu-id="6ad8f-127">Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6ad8f-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="6ad8f-128">Azure App Service Web Apps ek Azure Powershell örnekleri bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6ad8f-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
