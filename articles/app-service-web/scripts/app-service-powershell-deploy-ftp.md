---
title: "aaaAzure PowerShell komut dosyası örneği - FTP kullanarak karşıya yükleme dosyaları tooa web uygulaması | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - FTP kullanarak karşıya yükleme dosyaları tooa web uygulaması"
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
ms.openlocfilehash: 32a0a529e94c1315cc6730faf23fca2693c50ffb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-tooa-web-app-using-ftp"></a><span data-ttu-id="07572-103">FTP kullanarak dosyaları tooa web uygulaması karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="07572-103">Upload files tooa web app using FTP</span></span>

<span data-ttu-id="07572-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur ve FTP kullanarak web uygulama kodunuzda dağıtır (aracılığıyla [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span><span class="sxs-lookup"><span data-stu-id="07572-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span></span>

<span data-ttu-id="07572-105">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](/powershell/azure/overview)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="07572-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="07572-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="07572-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files tooa web app using FTP")]

## <a name="clean-up-deployment"></a><span data-ttu-id="07572-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="07572-107">Clean up deployment</span></span> 

<span data-ttu-id="07572-108">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, web uygulaması ve tüm ilişkili kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="07572-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="07572-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="07572-109">Script explanation</span></span>

<span data-ttu-id="07572-110">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="07572-110">This script uses hello following commands.</span></span> <span data-ttu-id="07572-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="07572-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="07572-112">Komut</span><span class="sxs-lookup"><span data-stu-id="07572-112">Command</span></span> | <span data-ttu-id="07572-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="07572-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="07572-114">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="07572-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="07572-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="07572-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="07572-116">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="07572-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="07572-117">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="07572-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="07572-118">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="07572-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="07572-119">Bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="07572-119">Creates a web app.</span></span> |
| [<span data-ttu-id="07572-120">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="07572-120">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="07572-121">Web uygulamanızın yayımlama profili alın.</span><span class="sxs-lookup"><span data-stu-id="07572-121">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="07572-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="07572-122">Next steps</span></span>

<span data-ttu-id="07572-123">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="07572-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="07572-124">Azure App Service Web Apps ek Azure Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="07572-124">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
