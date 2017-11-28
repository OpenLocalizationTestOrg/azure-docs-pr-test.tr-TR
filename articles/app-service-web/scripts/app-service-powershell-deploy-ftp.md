---
title: "Azure PowerShell Betiği örnek - karşıya yükleme dosyalarını FTP kullanarak bir web uygulamasına | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - karşıya yükleme dosyalarını FTP kullanarak bir web uygulaması için"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: b7d46d6f-44fd-454c-8008-87dab6eefbc1
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 96b99110b63b037746fcc40eb15db5d718eb71a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="upload-files-to-a-web-app-using-ftp"></a><span data-ttu-id="6e465-103">Bir web uygulamasına FTP kullanarak dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="6e465-103">Upload files to a web app using FTP</span></span>

<span data-ttu-id="6e465-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur ve FTP kullanarak web uygulama kodunuzda dağıtır (aracılığıyla [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span><span class="sxs-lookup"><span data-stu-id="6e465-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span></span>

<span data-ttu-id="6e465-105">Gerekirse, bulunan yönergeleri kullanarak Azure PowerShell'i yükleme [Azure PowerShell Kılavuzu](/powershell/azure/overview)ve ardından çalıştırın `Login-AzureRmAccount` Azure ile bir bağlantı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="6e465-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="6e465-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="6e465-106">Sample script</span></span>

<span data-ttu-id="6e465-107">[!code-powershell[Ana](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "FTP kullanarak bir web uygulaması dosyaları karşıya yükleme")]</span><span class="sxs-lookup"><span data-stu-id="6e465-107">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files to a web app using FTP")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6e465-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="6e465-108">Clean up deployment</span></span> 

<span data-ttu-id="6e465-109">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu, web uygulaması ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6e465-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="6e465-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="6e465-110">Script explanation</span></span>

<span data-ttu-id="6e465-111">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="6e465-111">This script uses the following commands.</span></span> <span data-ttu-id="6e465-112">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="6e465-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6e465-113">Komut</span><span class="sxs-lookup"><span data-stu-id="6e465-113">Command</span></span> | <span data-ttu-id="6e465-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="6e465-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6e465-115">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6e465-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="6e465-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6e465-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6e465-117">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="6e465-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="6e465-118">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6e465-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="6e465-119">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="6e465-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="6e465-120">Bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6e465-120">Creates a web app.</span></span> |
| [<span data-ttu-id="6e465-121">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="6e465-121">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="6e465-122">Web uygulamanızın yayımlama profili alın.</span><span class="sxs-lookup"><span data-stu-id="6e465-122">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6e465-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6e465-123">Next steps</span></span>

<span data-ttu-id="6e465-124">Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6e465-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="6e465-125">Azure App Service Web Apps ek Azure Powershell örnekleri bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6e465-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
