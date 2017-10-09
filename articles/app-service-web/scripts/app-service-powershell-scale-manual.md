---
title: "aaaAzure PowerShell komut dosyası örneği - bir web uygulaması el ile ölçeklendirin | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - bir web uygulaması elle ölçeklendirme"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: de5d4285-9c7d-4735-a695-288264047375
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c749031fbe6c6bcbb25395387b4f32b2ba75cef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="24bc5-103">Bir web uygulaması elle ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="24bc5-103">Scale a web app manually</span></span>

<span data-ttu-id="24bc5-104">Bu senaryoda, bir kaynak grubu toocreate öğreneceksiniz uygulama hizmeti planı ve web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="24bc5-104">In this scenario you will learn toocreate a resource group, app service plan and web app.</span></span> <span data-ttu-id="24bc5-105">Ardından hello App Service planı tek örnek toomultiple örneklerinden ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="24bc5-105">You will then scale hello App Service Plan from a single instance toomultiple instances.</span></span>

<span data-ttu-id="24bc5-106">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](/powershell/azure/overview)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="24bc5-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="24bc5-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="24bc5-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]

## <a name="clean-up-deployment"></a><span data-ttu-id="24bc5-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="24bc5-108">Clean up deployment</span></span> 

<span data-ttu-id="24bc5-109">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, web uygulaması ve tüm ilişkili kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="24bc5-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="24bc5-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="24bc5-110">Script explanation</span></span>

<span data-ttu-id="24bc5-111">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="24bc5-111">This script uses hello following commands.</span></span> <span data-ttu-id="24bc5-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="24bc5-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="24bc5-113">Komut</span><span class="sxs-lookup"><span data-stu-id="24bc5-113">Command</span></span> | <span data-ttu-id="24bc5-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="24bc5-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="24bc5-115">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="24bc5-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="24bc5-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="24bc5-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="24bc5-117">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="24bc5-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="24bc5-118">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="24bc5-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="24bc5-119">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="24bc5-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="24bc5-120">Bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="24bc5-120">Creates a web app.</span></span> |
| [<span data-ttu-id="24bc5-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="24bc5-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="24bc5-122">Web uygulamanızın yapılandırmasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="24bc5-122">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="24bc5-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="24bc5-123">Next steps</span></span>

<span data-ttu-id="24bc5-124">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="24bc5-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="24bc5-125">Azure App Service Web Apps ek Azure Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="24bc5-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
