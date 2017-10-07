---
title: "aaaAzure PowerShell komut dosyası örneği - bağ özel bir SSL sertifikası tooa web uygulaması | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - BIND özel bir SSL sertifikası tooa web uygulaması"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 23e83b74-614a-49a0-bc08-7542120eeec5
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6e249ceedb9e2b8872dd0bc8b0aea0d718b28dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="960fb-103">Özel SSL sertifika tooa web uygulama bağlama</span><span class="sxs-lookup"><span data-stu-id="960fb-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="960fb-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur, ardından özel etki alanı adı tooit hello SSL sertifikasını bağlar.</span><span class="sxs-lookup"><span data-stu-id="960fb-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> 

<span data-ttu-id="960fb-105">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="960fb-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="960fb-106">Ayrıca, emin olun:</span><span class="sxs-lookup"><span data-stu-id="960fb-106">Also, ensure that:</span></span>

- <span data-ttu-id="960fb-107">Hello kullanarak Azure ile bağlantı oluşturuldu `az login` komutu.</span><span class="sxs-lookup"><span data-stu-id="960fb-107">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="960fb-108">Erişim tooyour etki alanı kayıt şirketinizin DNS yapılandırma sayfası vardır.</span><span class="sxs-lookup"><span data-stu-id="960fb-108">You have access tooyour domain registrar's DNS configuration page.</span></span>
- <span data-ttu-id="960fb-109">Geçerli bir sahip. PFX dosyası ve kendi parolasını hello SSL sertifikası, tooupload istediğiniz ve bağlayın.</span><span class="sxs-lookup"><span data-stu-id="960fb-109">You have a valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

## <a name="sample-script"></a><span data-ttu-id="960fb-110">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="960fb-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="960fb-111">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="960fb-111">Clean up deployment</span></span> 

<span data-ttu-id="960fb-112">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, web uygulaması ve tüm ilişkili kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="960fb-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="960fb-113">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="960fb-113">Script explanation</span></span>

<span data-ttu-id="960fb-114">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="960fb-114">This script uses hello following commands.</span></span> <span data-ttu-id="960fb-115">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="960fb-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="960fb-116">Komut</span><span class="sxs-lookup"><span data-stu-id="960fb-116">Command</span></span> | <span data-ttu-id="960fb-117">Notlar</span><span class="sxs-lookup"><span data-stu-id="960fb-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="960fb-118">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="960fb-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="960fb-119">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="960fb-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="960fb-120">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="960fb-120">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="960fb-121">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="960fb-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="960fb-122">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="960fb-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="960fb-123">Bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="960fb-123">Creates a web app.</span></span> |
| [<span data-ttu-id="960fb-124">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="960fb-124">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="960fb-125">Bir uygulama hizmeti planı toochange fiyatlandırma katmanı değiştirir.</span><span class="sxs-lookup"><span data-stu-id="960fb-125">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="960fb-126">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="960fb-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="960fb-127">Web uygulamanızın yapılandırmasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="960fb-127">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="960fb-128">AzureRmWebAppSSLBinding yeni</span><span class="sxs-lookup"><span data-stu-id="960fb-128">New-AzureRmWebAppSSLBinding</span></span>](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | <span data-ttu-id="960fb-129">Bir web uygulaması için bir SSL sertifikası bağlama oluşturur.</span><span class="sxs-lookup"><span data-stu-id="960fb-129">Creates an SSL certificate binding for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="960fb-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="960fb-130">Next steps</span></span>

<span data-ttu-id="960fb-131">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="960fb-131">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="960fb-132">Azure App Service Web Apps ek Azure Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="960fb-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
