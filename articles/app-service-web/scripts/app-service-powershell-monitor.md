---
title: "aaaAzure PowerShell komut dosyası örneği - web sunucu günlükleri ile bir web uygulaması izleme | Microsoft Docs"
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
ms.openlocfilehash: efaae1e19f5153e33d1f5d5decadb9f6c4649f8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="9607c-103">Web sunucu günlükleri ile bir web uygulaması izleme</span><span class="sxs-lookup"><span data-stu-id="9607c-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="9607c-104">Bu senaryoda, bir kaynak grubu, uygulama hizmeti planı, web uygulaması oluşturun ve hello web uygulama tooenable web sunucu günlükleri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9607c-104">In this scenario you will create a resource group, app service plan, web app and configure hello web app tooenable web server logs.</span></span> <span data-ttu-id="9607c-105">Daha sonra gözden geçirme için hello günlük dosyalarını indirir.</span><span class="sxs-lookup"><span data-stu-id="9607c-105">You will then download hello log files for review.</span></span>

<span data-ttu-id="9607c-106">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](/powershell/azure/overview)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="9607c-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="9607c-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="9607c-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9607c-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="9607c-108">Clean up deployment</span></span> 

<span data-ttu-id="9607c-109">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, web uygulaması ve tüm ilişkili kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="9607c-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="9607c-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="9607c-110">Script explanation</span></span>

<span data-ttu-id="9607c-111">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="9607c-111">This script uses hello following commands.</span></span> <span data-ttu-id="9607c-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="9607c-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9607c-113">Komut</span><span class="sxs-lookup"><span data-stu-id="9607c-113">Command</span></span> | <span data-ttu-id="9607c-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="9607c-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9607c-115">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9607c-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="9607c-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9607c-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9607c-117">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="9607c-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="9607c-118">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9607c-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="9607c-119">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="9607c-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="9607c-120">Bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9607c-120">Creates a web app.</span></span> |
| [<span data-ttu-id="9607c-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="9607c-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="9607c-122">Web uygulamanızın yapılandırmasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="9607c-122">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="9607c-123">Get-AzureRMWebAppMetrics</span><span class="sxs-lookup"><span data-stu-id="9607c-123">Get-AzureRMWebAppMetrics</span></span>](/powershell/module/azurerm.websites/get-azurermwebappmetrics) | <span data-ttu-id="9607c-124">Web uygulamanızın ölçümleri alır.</span><span class="sxs-lookup"><span data-stu-id="9607c-124">Gets a web app's metrics.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9607c-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9607c-125">Next steps</span></span>

<span data-ttu-id="9607c-126">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9607c-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="9607c-127">Azure App Service Web Apps ek Azure Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9607c-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
