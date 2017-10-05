---
title: "Azure PowerShell Betiği örnek - özel bir SSL sertifikasını bir web uygulamasına bağlama | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - bağlaması bir web uygulaması için özel bir SSL sertifikası"
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
ms.openlocfilehash: de8deccadcd9571be75447a117888bf2b3f571a0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-web-app"></a><span data-ttu-id="c12c7-103">Bir web uygulaması için özel bir SSL sertifikası bağlama</span><span class="sxs-lookup"><span data-stu-id="c12c7-103">Bind a custom SSL certificate to a web app</span></span>

<span data-ttu-id="c12c7-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur, ardından özel etki alanı adı SSL sertifikası kendisine bağlar.</span><span class="sxs-lookup"><span data-stu-id="c12c7-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> 

<span data-ttu-id="c12c7-105">Gerekirse, bulunan yönergeleri kullanarak Azure PowerShell'i yükleme [Azure PowerShell Kılavuzu](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c12c7-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="c12c7-106">Ayrıca, emin olun:</span><span class="sxs-lookup"><span data-stu-id="c12c7-106">Also, ensure that:</span></span>

- <span data-ttu-id="c12c7-107">Azure ile bir bağlantı kullanılarak oluşturulup oluşturulmadığını `az login` komutu.</span><span class="sxs-lookup"><span data-stu-id="c12c7-107">A connection with Azure has been created using the `az login` command.</span></span>
- <span data-ttu-id="c12c7-108">Etki alanı kayıt şirketinizin DNS yapılandırma sayfasına erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c12c7-108">You have access to your domain registrar's DNS configuration page.</span></span>
- <span data-ttu-id="c12c7-109">Geçerli bir sahip. PFX dosyası ve SSL sertifikasının parolası karşıya yüklemek ve bağlamak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="c12c7-109">You have a valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

## <a name="sample-script"></a><span data-ttu-id="c12c7-110">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="c12c7-110">Sample script</span></span>

<span data-ttu-id="c12c7-111">[!code-powershell[Ana](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "bir web uygulaması için özel bir SSL sertifikası bağlama")]</span><span class="sxs-lookup"><span data-stu-id="c12c7-111">[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c12c7-112">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="c12c7-112">Clean up deployment</span></span> 

<span data-ttu-id="c12c7-113">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu, web uygulaması ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c12c7-113">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="c12c7-114">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="c12c7-114">Script explanation</span></span>

<span data-ttu-id="c12c7-115">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="c12c7-115">This script uses the following commands.</span></span> <span data-ttu-id="c12c7-116">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="c12c7-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c12c7-117">Komut</span><span class="sxs-lookup"><span data-stu-id="c12c7-117">Command</span></span> | <span data-ttu-id="c12c7-118">Notlar</span><span class="sxs-lookup"><span data-stu-id="c12c7-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c12c7-119">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c12c7-119">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c12c7-120">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c12c7-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c12c7-121">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="c12c7-121">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="c12c7-122">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c12c7-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c12c7-123">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="c12c7-123">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="c12c7-124">Bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c12c7-124">Creates a web app.</span></span> |
| [<span data-ttu-id="c12c7-125">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="c12c7-125">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="c12c7-126">Fiyatlandırma katmanını değiştirmek için bir uygulama hizmeti planı değiştirir.</span><span class="sxs-lookup"><span data-stu-id="c12c7-126">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="c12c7-127">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="c12c7-127">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="c12c7-128">Web uygulamanızın yapılandırmasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="c12c7-128">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="c12c7-129">AzureRmWebAppSSLBinding yeni</span><span class="sxs-lookup"><span data-stu-id="c12c7-129">New-AzureRmWebAppSSLBinding</span></span>](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | <span data-ttu-id="c12c7-130">Bir web uygulaması için bir SSL sertifikası bağlama oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c12c7-130">Creates an SSL certificate binding for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c12c7-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c12c7-131">Next steps</span></span>

<span data-ttu-id="c12c7-132">Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c12c7-132">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c12c7-133">Azure App Service Web Apps ek Azure Powershell örnekleri bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c12c7-133">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
