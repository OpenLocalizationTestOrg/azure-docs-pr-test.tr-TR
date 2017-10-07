---
title: "aaaAzure PowerShell komut dosyası örneği - bağlantı bir web uygulaması tooa depolama hesabı | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - bir web uygulaması tooa depolama hesabı Bağlan"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4831bdc-2068-4883-9474-0b34c2e3e255
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 07693366d32fbaefe92c18df67ded81661e1a2df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-storage-account"></a><span data-ttu-id="c55ac-103">Bir web uygulaması tooa depolama hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="c55ac-103">Connect a web app tooa storage account</span></span>

<span data-ttu-id="c55ac-104">Bu senaryoda, nasıl toocreate bir Azure depolama hesabı ve bir Azure web uygulaması öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c55ac-104">In this scenario you will learn how toocreate an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="c55ac-105">Uygulama ayarları kullanarak hello depolama hesabı toohello web uygulaması bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="c55ac-105">Then you will link hello storage account toohello web app using app settings.</span></span>

<span data-ttu-id="c55ac-106">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](/powershell/azure/overview)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="c55ac-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="c55ac-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="c55ac-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app tooa storage account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c55ac-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="c55ac-108">Clean up deployment</span></span> 

<span data-ttu-id="c55ac-109">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, web uygulaması ve tüm ilişkili kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="c55ac-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="c55ac-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="c55ac-110">Script explanation</span></span>

<span data-ttu-id="c55ac-111">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="c55ac-111">This script uses hello following commands.</span></span> <span data-ttu-id="c55ac-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="c55ac-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c55ac-113">Komut</span><span class="sxs-lookup"><span data-stu-id="c55ac-113">Command</span></span> | <span data-ttu-id="c55ac-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="c55ac-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c55ac-115">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c55ac-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c55ac-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c55ac-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c55ac-117">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="c55ac-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="c55ac-118">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c55ac-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c55ac-119">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="c55ac-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="c55ac-120">Bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c55ac-120">Creates a web app.</span></span> |
| [<span data-ttu-id="c55ac-121">Yeni-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="c55ac-121">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="c55ac-122">Bir depolama hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c55ac-122">Creates a Storage account.</span></span> |
| [<span data-ttu-id="c55ac-123">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="c55ac-123">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="c55ac-124">Bir Azure depolama hesabı için erişim anahtarlarını Hello alır.</span><span class="sxs-lookup"><span data-stu-id="c55ac-124">Gets hello access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="c55ac-125">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="c55ac-125">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="c55ac-126">Web uygulamanızın yapılandırmasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="c55ac-126">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c55ac-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c55ac-127">Next steps</span></span>

<span data-ttu-id="c55ac-128">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c55ac-128">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c55ac-129">Azure App Service Web Apps ek Azure Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c55ac-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
