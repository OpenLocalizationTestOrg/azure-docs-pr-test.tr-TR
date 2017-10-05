---
title: "Azure Resource Manager tabanlı PowerShell komutları için Azure Web uygulaması | Microsoft Docs"
description: "Yeni Azure Resource Manager tabanlı PowerShell komutlarının Azure Web uygulamaları yönetmek için nasıl kullanılacağını öğrenin."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 8d574f051a327ba0409e6f25a5886af673d3d5e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-powershell-to-manage-azure-web-apps"></a><span data-ttu-id="0ac90-103">Azure Web uygulamaları yönetmek için Azure Resource Manager tabanlı PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="0ac90-103">Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0ac90-104">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0ac90-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="0ac90-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ac90-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="0ac90-106">Microsoft Azure PowerShell sürümü 1.0.0 yeni komutları eklenmiştir, kullanıcı Web uygulamaları yönetmek için Azure Resource Manager tabanlı PowerShell komutlarını kullanma olanağı verir.</span><span class="sxs-lookup"><span data-stu-id="0ac90-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give the user the ability to use Azure Resource Manager-based PowerShell commands to manage Web Apps.</span></span>

<span data-ttu-id="0ac90-107">Kaynak gruplarını yönetme hakkında bilgi edinmek için [Azure PowerShell kullanarak Azure Resource Manager ile](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="0ac90-107">To learn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="0ac90-108">Parametreleri ve seçenekleri PowerShell cmdlet'lerinin tam listesi hakkında bilgi edinmek için [Cmdlet başvurusu, Web uygulamasını Azure Resource Manager tabanlı PowerShell cmdlet'lerinin tam](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="0ac90-108">To learn about the full list of parameters and options for the PowerShell cmdlets, see the [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="0ac90-109">Uygulama hizmeti yönetme planları</span><span class="sxs-lookup"><span data-stu-id="0ac90-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="0ac90-110">Bir uygulama hizmeti planı oluştur</span><span class="sxs-lookup"><span data-stu-id="0ac90-110">Create an App Service Plan</span></span>
<span data-ttu-id="0ac90-111">Bir uygulama hizmeti planı oluşturmak için kullanın **yeni AzureRmAppServicePlan** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0ac90-111">To create an app service plan, use the **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="0ac90-112">Farklı Parametreler açıklamalarını şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0ac90-112">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="0ac90-113">**Ad**: uygulama hizmeti planının adı.</span><span class="sxs-lookup"><span data-stu-id="0ac90-113">**Name**: name of the app service plan.</span></span>
* <span data-ttu-id="0ac90-114">**Konum**: hizmet planı konumu.</span><span class="sxs-lookup"><span data-stu-id="0ac90-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="0ac90-115">**ResourceGroupName**: yeni oluşturulan uygulama hizmeti planı içeren kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="0ac90-115">**ResourceGroupName**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="0ac90-116">**Katman**: İstenen fiyatlandırma Katmanı (varsayılan serbest, paylaşılan, temel, standart ve Premium diğer seçeneklerdir.)</span><span class="sxs-lookup"><span data-stu-id="0ac90-116">**Tier**:  the desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="0ac90-117">**WorkerSize**: (varsayılan temel, standart veya Premium katmanı parametresi belirtildiyse, küçük. çalışan boyutu</span><span class="sxs-lookup"><span data-stu-id="0ac90-117">**WorkerSize**: the size of workers (Default is small if the Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="0ac90-118">Diğer Orta ve büyük seçenekleridir.)</span><span class="sxs-lookup"><span data-stu-id="0ac90-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="0ac90-119">**NumberofWorkers**: uygulamasında çalışan sayısı hizmet planı (varsayılan değer 1'dir).</span><span class="sxs-lookup"><span data-stu-id="0ac90-119">**NumberofWorkers**: the number of workers in the app service plan (Default value is 1).</span></span> 

<span data-ttu-id="0ac90-120">Bu cmdlet kullanılarak örnek:</span><span class="sxs-lookup"><span data-stu-id="0ac90-120">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="0ac90-121">Bir uygulama hizmeti ortamı'nda bir uygulama hizmeti planı oluştur</span><span class="sxs-lookup"><span data-stu-id="0ac90-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="0ac90-122">Uygulama hizmeti ortamı'nda bir uygulama hizmeti planı oluşturmak için aynı komutunu **yeni AzureRmAppServicePlan** komutu ek parametre ana'nın adını ve ana'nın kaynak grubu adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="0ac90-122">To create an app service plan in an app service environment, use the same command **New-AzureRmAppServicePlan** command with extra parameters to specify the ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="0ac90-123">Bu cmdlet kullanılarak örnek:</span><span class="sxs-lookup"><span data-stu-id="0ac90-123">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="0ac90-124">Uygulama hizmeti ortamı hakkında daha fazla bilgi edinmek için [uygulama hizmeti ortamı giriş](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="0ac90-124">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="0ac90-125">Var olan uygulama hizmeti planları listesi</span><span class="sxs-lookup"><span data-stu-id="0ac90-125">List Existing App Service Plans</span></span>
<span data-ttu-id="0ac90-126">Var olan uygulama hizmeti planları listelemek için kullanın **Get-AzureRmAppServicePlan** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0ac90-126">To list the existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="0ac90-127">Aboneliğinizdeki tüm uygulama hizmeti planları listelemek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="0ac90-127">To list all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="0ac90-128">Belirli kaynak grubundaki tüm uygulama hizmeti planları listelemek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="0ac90-128">To list all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="0ac90-129">Belirli uygulama hizmeti planı almak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="0ac90-129">To get a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="0ac90-130">Var olan bir App Service planı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="0ac90-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="0ac90-131">Var olan bir uygulama hizmeti planı ayarları değiştirmek için kullanın **kümesi AzureRmAppServicePlan** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0ac90-131">To change the settings for an existing app service plan, use the **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="0ac90-132">Katmanı, çalışan boyutu ve çalışanların sayısını değiştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0ac90-132">You can change the tier, worker size, and the number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="0ac90-133">Bir uygulama hizmeti planı ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="0ac90-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="0ac90-134">Var olan bir uygulama hizmeti planı ölçeklendirmek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="0ac90-134">To scale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-the-worker-size-of-an-app-service-plan"></a><span data-ttu-id="0ac90-135">Bir uygulama hizmeti planı çalışan boyutunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="0ac90-135">Changing the worker size of an App Service Plan</span></span>
<span data-ttu-id="0ac90-136">Var olan bir uygulama hizmeti planında çalışanları boyutunu değiştirmek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="0ac90-136">To change the size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-the-tier-of-an-app-service-plan"></a><span data-ttu-id="0ac90-137">Bir uygulama hizmeti planı katmanını değiştirme</span><span class="sxs-lookup"><span data-stu-id="0ac90-137">Changing the Tier of an App Service Plan</span></span>
<span data-ttu-id="0ac90-138">Var olan bir uygulama hizmeti planı katmanını değiştirmek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="0ac90-138">To change the tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="0ac90-139">Var olan bir uygulama hizmeti planı silme</span><span class="sxs-lookup"><span data-stu-id="0ac90-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="0ac90-140">Var olan bir uygulama hizmeti planı silmek için tüm atanmış web uygulamaları taşınmış veya silinmiş ilk gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ac90-140">To delete an existing app service plan, all assigned web apps need to be moved or deleted first.</span></span> <span data-ttu-id="0ac90-141">Ardından kullanarak **Kaldır AzureRmAppServicePlan** cmdlet uygulama hizmeti planı silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ac90-141">Then using the **Remove-AzureRmAppServicePlan** cmdlet you can delete the app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="0ac90-142">App Service Web uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="0ac90-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="0ac90-143">Web Uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ac90-143">Create a Web App</span></span>
<span data-ttu-id="0ac90-144">Bir web uygulaması oluşturmak için kullanın **yeni AzureRmWebApp** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0ac90-144">To create a web app, use the **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="0ac90-145">Farklı Parametreler açıklamalarını şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0ac90-145">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="0ac90-146">**Ad**: web uygulamasının adı.</span><span class="sxs-lookup"><span data-stu-id="0ac90-146">**Name**: name for the web app.</span></span>
* <span data-ttu-id="0ac90-147">**AppServicePlan**: web uygulamasını barındırmak için kullanılan hizmeti planının adı.</span><span class="sxs-lookup"><span data-stu-id="0ac90-147">**AppServicePlan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="0ac90-148">**ResourceGroupName**: uygulama hizmeti planı barındıran kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="0ac90-148">**ResourceGroupName**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="0ac90-149">**Konum**: web uygulaması konumu.</span><span class="sxs-lookup"><span data-stu-id="0ac90-149">**Location**: the web app location.</span></span>

<span data-ttu-id="0ac90-150">Bu cmdlet kullanılarak örnek:</span><span class="sxs-lookup"><span data-stu-id="0ac90-150">Example to use this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="0ac90-151">Bir uygulama hizmeti ortamı'nda bir Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ac90-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="0ac90-152">Uygulama hizmeti ortamı (ASE'de) bir web uygulaması oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="0ac90-152">To create a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="0ac90-153">Aynı **yeni AzureRmWebApp** ana adının ve kaynak grubu adı, ana belirtmek için ek parametreler komutuyla ait.</span><span class="sxs-lookup"><span data-stu-id="0ac90-153">Use the same **New-AzureRmWebApp** command with extra parameters to specify the ASE name and the resource group name that the ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="0ac90-154">Uygulama hizmeti ortamı hakkında daha fazla bilgi edinmek için [uygulama hizmeti ortamı giriş](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="0ac90-154">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="0ac90-155">Var olan bir Web uygulamasının Sil</span><span class="sxs-lookup"><span data-stu-id="0ac90-155">Delete an existing Web App</span></span>
<span data-ttu-id="0ac90-156">Kullanabileceğiniz mevcut bir web uygulamasını silmek için **Kaldır AzureRmWebApp** cmdlet, web uygulamasının adını ve kaynak grubu adı belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ac90-156">To delete an existing web app you can use the **Remove-AzureRmWebApp** cmdlet, you need to specify the name of the web app and the resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="0ac90-157">Var olan Web Apps listesi</span><span class="sxs-lookup"><span data-stu-id="0ac90-157">List existing Web Apps</span></span>
<span data-ttu-id="0ac90-158">Mevcut web uygulamaları listelemek için kullanmak **Get-AzureRmWebApp** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0ac90-158">To list the existing web apps, use the **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="0ac90-159">Aboneliğinizdeki tüm web uygulamaları listelemek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="0ac90-159">To list all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="0ac90-160">Belirli bir kaynak grubunun altındaki tüm web uygulamaları listelemek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="0ac90-160">To list all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="0ac90-161">Belirli web uygulamasını almak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="0ac90-161">To get a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="0ac90-162">Var olan bir Web uygulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0ac90-162">Configure an existing Web App</span></span>
<span data-ttu-id="0ac90-163">Var olan bir web uygulaması için yapılandırmaları ve ayarları değiştirmek için kullanın **kümesi AzureRmWebApp** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0ac90-163">To change the settings and configurations for an existing web app, use the **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="0ac90-164">Parametrelerin tam bir listesi için denetleme [Cmdlet başvuru bağlantısı](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="0ac90-164">For a full list of parameters, check the [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="0ac90-165">(1) örnek: bağlantı dizelerini değiştirmek için bu cmdlet'i kullanın.</span><span class="sxs-lookup"><span data-stu-id="0ac90-165">Example (1): use this cmdlet to change connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="0ac90-166">(2) örnek: ekleme veya uygulama ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="0ac90-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="0ac90-167">(3) örnek: 64-bit modunda çalıştırmak için web uygulaması ayarlayın</span><span class="sxs-lookup"><span data-stu-id="0ac90-167">Example (3):  set the web app to run in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-the-state-of-an-existing-web-app"></a><span data-ttu-id="0ac90-168">Var olan bir Web uygulamasının durumunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="0ac90-168">Change the state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="0ac90-169">Bir web uygulaması yeniden</span><span class="sxs-lookup"><span data-stu-id="0ac90-169">Restart a web app</span></span>
<span data-ttu-id="0ac90-170">Bir web uygulaması yeniden başlatmak için web uygulamasının adını ve kaynak grubu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ac90-170">To restart a web app, you must specify the name and resource group of the web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="0ac90-171">Bir web uygulamasını Durdur</span><span class="sxs-lookup"><span data-stu-id="0ac90-171">Stop a web app</span></span>
<span data-ttu-id="0ac90-172">Bir web uygulaması durdurmak için web uygulamasının adını ve kaynak grubu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ac90-172">To stop a web app, you must specify the name and resource group of the web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="0ac90-173">Bir web uygulaması başlatın</span><span class="sxs-lookup"><span data-stu-id="0ac90-173">Start a web app</span></span>
<span data-ttu-id="0ac90-174">Bir web uygulaması başlatmak için web uygulamasının adını ve kaynak grubu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ac90-174">To start a web app, you must specify the name and resource group of the web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="0ac90-175">Web uygulaması yayımlama profillerini yönet</span><span class="sxs-lookup"><span data-stu-id="0ac90-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="0ac90-176">Her web uygulaması, uygulamalarınızı yayımlamak için kullanılan bir yayımlama profili varsa, çeşitli işlemleri profilleri yayımlama çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="0ac90-176">Each web app has a publishing profile that can be used to publish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="0ac90-177">Yayımlama profilini Al</span><span class="sxs-lookup"><span data-stu-id="0ac90-177">Get Publishing Profile</span></span>
<span data-ttu-id="0ac90-178">Bir web uygulaması için yayımlama profili almak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="0ac90-178">To get the publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="0ac90-179">Bu komut, bir metin dosyasına yayımlama profili iyi çıkış olarak komut satırı için yayımlama profili görüntülemektedir.</span><span class="sxs-lookup"><span data-stu-id="0ac90-179">This command echoes the publishing profile to the command line as well output the publishing profile to a text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="0ac90-180">Yayımlama profilini Sıfırla</span><span class="sxs-lookup"><span data-stu-id="0ac90-180">Reset Publishing Profile</span></span>
<span data-ttu-id="0ac90-181">FTP ve web yayımlama parolası her ikisi de sıfırlamak için web uygulaması için kullanım dağıtın:</span><span class="sxs-lookup"><span data-stu-id="0ac90-181">To reset both the publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="0ac90-182">Web uygulaması sertifikaları yönetme</span><span class="sxs-lookup"><span data-stu-id="0ac90-182">Manage Web App Certificates</span></span>
<span data-ttu-id="0ac90-183">Web uygulaması sertifikaları yönetme hakkında bilgi edinmek için [PowerShell kullanarak SSL sertifikalarını bağlama](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="0ac90-183">To learn about how to manage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="0ac90-184">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="0ac90-184">Next Steps</span></span>
* <span data-ttu-id="0ac90-185">Azure Resource Manager PowerShell desteği hakkında bilgi edinmek için [Azure PowerShell kullanarak Azure Resource Manager ile.](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="0ac90-185">To learn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="0ac90-186">Uygulama hizmeti ortamları hakkında bilgi edinmek için [uygulama hizmeti ortamı giriş.](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="0ac90-186">To learn about App Service Environments, see [Introduction to App Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="0ac90-187">PowerShell kullanarak uygulama hizmeti SSL sertifikalarını yönetme hakkında bilgi edinmek için [PowerShell kullanarak SSL sertifikalarını bağlama.](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="0ac90-187">To learn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="0ac90-188">Azure Web uygulamaları için Azure Resource Manager tabanlı PowerShell cmdlet'lerinin tam listesi hakkında bilgi edinmek için [, Web uygulamaları Azure Resource Manager PowerShell cmdlet'lerinin Azure Cmdlet başvurusu.](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="0ac90-188">To learn about the full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="0ac90-189">Uygulama hizmeti CLI kullanarak yönetme hakkında bilgi edinmek için [Using Azure Resource Manager-Based XPlat CLI Azure Web uygulaması için.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span><span class="sxs-lookup"><span data-stu-id="0ac90-189">To learn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

