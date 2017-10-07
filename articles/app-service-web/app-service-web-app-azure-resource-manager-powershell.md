---
title: "aaaAzure Resource Manager tabanlı PowerShell komutları için Azure Web uygulaması | Microsoft Docs"
description: "Nasıl toouse hello yeni Azure Resource Manager tabanlı PowerShell komutları toomanage Azure Web Apps hakkında bilgi edinin."
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
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a><span data-ttu-id="86e89-103">Azure Resource Manager-based PowerShell tooManage Azure Web uygulamaları kullanma</span><span class="sxs-lookup"><span data-stu-id="86e89-103">Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="86e89-104">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="86e89-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="86e89-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="86e89-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="86e89-106">Microsoft Azure PowerShell sürümü 1.0.0 yeni komutları eklenmiştir, hello kullanıcı hello özelliği toouse Azure Resource Manager tabanlı PowerShell komutları toomanage Web Apps verin.</span><span class="sxs-lookup"><span data-stu-id="86e89-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage Web Apps.</span></span>

<span data-ttu-id="86e89-107">Kaynak gruplarını yönetme hakkında toolearn bkz [Azure PowerShell kullanarak Azure Resource Manager ile](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="86e89-107">toolearn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="86e89-108">toolearn parametreleri hello PowerShell cmdlet'leri için seçenekler ve hello tam listesi hakkında bkz hello [Cmdlet başvurusu, Web uygulamasını Azure Resource Manager tabanlı PowerShell cmdlet'lerinin tam](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="86e89-108">toolearn about hello full list of parameters and options for hello PowerShell cmdlets, see hello [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="86e89-109">Uygulama hizmeti yönetme planları</span><span class="sxs-lookup"><span data-stu-id="86e89-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="86e89-110">Bir uygulama hizmeti planı oluştur</span><span class="sxs-lookup"><span data-stu-id="86e89-110">Create an App Service Plan</span></span>
<span data-ttu-id="86e89-111">bir uygulama hizmeti planı toocreate hello kullan **yeni AzureRmAppServicePlan** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="86e89-111">toocreate an app service plan, use hello **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="86e89-112">Merhaba farklı parametreler açıklamalarını şunlardır:</span><span class="sxs-lookup"><span data-stu-id="86e89-112">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="86e89-113">**Ad**: hello uygulama hizmeti planının adı.</span><span class="sxs-lookup"><span data-stu-id="86e89-113">**Name**: name of hello app service plan.</span></span>
* <span data-ttu-id="86e89-114">**Konum**: hizmet planı konumu.</span><span class="sxs-lookup"><span data-stu-id="86e89-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="86e89-115">**ResourceGroupName**: yeni oluşturulan hello uygulama hizmeti planı içeren kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="86e89-115">**ResourceGroupName**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="86e89-116">**Katman**: hello istenen fiyatlandırma Katmanı (varsayılan serbest, paylaşılan, temel, standart ve Premium diğer seçeneklerdir.)</span><span class="sxs-lookup"><span data-stu-id="86e89-116">**Tier**:  hello desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="86e89-117">**WorkerSize**: Merhaba boyutu çalışanı (varsayılan temel, standart veya Premium hello katmanı parametresi belirtildiyse, küçük.</span><span class="sxs-lookup"><span data-stu-id="86e89-117">**WorkerSize**: hello size of workers (Default is small if hello Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="86e89-118">Diğer Orta ve büyük seçenekleridir.)</span><span class="sxs-lookup"><span data-stu-id="86e89-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="86e89-119">**NumberofWorkers**: (varsayılan değer 1'dir) hello uygulama hizmeti planında hello çalışan sayısı.</span><span class="sxs-lookup"><span data-stu-id="86e89-119">**NumberofWorkers**: hello number of workers in hello app service plan (Default value is 1).</span></span> 

<span data-ttu-id="86e89-120">Örnek toouse Bu cmdlet:</span><span class="sxs-lookup"><span data-stu-id="86e89-120">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="86e89-121">Bir uygulama hizmeti ortamı'nda bir uygulama hizmeti planı oluştur</span><span class="sxs-lookup"><span data-stu-id="86e89-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="86e89-122">toocreate bir uygulama hizmeti planı uygulama hizmeti ortamı'nda, kullanım hello aynı komut **yeni AzureRmAppServicePlan** ek parametreler toospecify hello ana'nın adı ve ana'nın kaynak grubu adıyla komutu.</span><span class="sxs-lookup"><span data-stu-id="86e89-122">toocreate an app service plan in an app service environment, use hello same command **New-AzureRmAppServicePlan** command with extra parameters toospecify hello ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="86e89-123">Örnek toouse Bu cmdlet:</span><span class="sxs-lookup"><span data-stu-id="86e89-123">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="86e89-124">uygulama hizmeti ortamı, denetimi hakkında daha fazla toolearn [giriş tooApp hizmeti ortamı](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="86e89-124">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="86e89-125">Var olan uygulama hizmeti planları listesi</span><span class="sxs-lookup"><span data-stu-id="86e89-125">List Existing App Service Plans</span></span>
<span data-ttu-id="86e89-126">toolist hello var olan uygulama hizmeti planları kullanın **Get-AzureRmAppServicePlan** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="86e89-126">toolist hello existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="86e89-127">toolist, aboneliğinizdeki tüm uygulama hizmeti planları kullanın:</span><span class="sxs-lookup"><span data-stu-id="86e89-127">toolist all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="86e89-128">toolist belirli kaynak grubundaki tüm uygulama hizmeti planları kullanın:</span><span class="sxs-lookup"><span data-stu-id="86e89-128">toolist all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="86e89-129">tooget belirli uygulama hizmeti planı kullanın:</span><span class="sxs-lookup"><span data-stu-id="86e89-129">tooget a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="86e89-130">Var olan bir App Service planı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="86e89-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="86e89-131">var olan bir uygulama hizmeti planı toochange hello ayarlarını kullan hello **kümesi AzureRmAppServicePlan** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="86e89-131">toochange hello settings for an existing app service plan, use hello **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="86e89-132">Merhaba katmanı, çalışan boyutu ve çalışan hello sayısı değiştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="86e89-132">You can change hello tier, worker size, and hello number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="86e89-133">Bir uygulama hizmeti planı ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="86e89-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="86e89-134">tooscale bir var olan uygulama hizmeti planı, kullanın:</span><span class="sxs-lookup"><span data-stu-id="86e89-134">tooscale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a><span data-ttu-id="86e89-135">Bir uygulama hizmeti planı Hello çalışan boyutu değiştirme</span><span class="sxs-lookup"><span data-stu-id="86e89-135">Changing hello worker size of an App Service Plan</span></span>
<span data-ttu-id="86e89-136">çalışan bir var olan uygulama hizmeti planında, kullanım toochange hello boyutu:</span><span class="sxs-lookup"><span data-stu-id="86e89-136">toochange hello size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a><span data-ttu-id="86e89-137">Merhaba bir uygulama hizmeti planı katmanını değiştirme</span><span class="sxs-lookup"><span data-stu-id="86e89-137">Changing hello Tier of an App Service Plan</span></span>
<span data-ttu-id="86e89-138">toochange hello katmanına bir var olan uygulama hizmeti planı, kullanın:</span><span class="sxs-lookup"><span data-stu-id="86e89-138">toochange hello tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="86e89-139">Var olan bir uygulama hizmeti planı silme</span><span class="sxs-lookup"><span data-stu-id="86e89-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="86e89-140">toodelete var olan bir uygulama hizmeti planı, tüm web uygulamaları gerek toobe taşınmış veya silinmiş ilk atanır.</span><span class="sxs-lookup"><span data-stu-id="86e89-140">toodelete an existing app service plan, all assigned web apps need toobe moved or deleted first.</span></span> <span data-ttu-id="86e89-141">Hello kullanarak **Kaldır AzureRmAppServicePlan** cmdlet hello uygulama hizmeti planı silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86e89-141">Then using hello **Remove-AzureRmAppServicePlan** cmdlet you can delete hello app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="86e89-142">App Service Web uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="86e89-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="86e89-143">Web Uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="86e89-143">Create a Web App</span></span>
<span data-ttu-id="86e89-144">toocreate bir web uygulaması kullanın hello **yeni AzureRmWebApp** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="86e89-144">toocreate a web app, use hello **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="86e89-145">Merhaba farklı parametreler açıklamalarını şunlardır:</span><span class="sxs-lookup"><span data-stu-id="86e89-145">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="86e89-146">**Ad**: hello web uygulamasının adı.</span><span class="sxs-lookup"><span data-stu-id="86e89-146">**Name**: name for hello web app.</span></span>
* <span data-ttu-id="86e89-147">**AppServicePlan**: hello hizmet planı toohost hello web uygulaması kullanılan ad.</span><span class="sxs-lookup"><span data-stu-id="86e89-147">**AppServicePlan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="86e89-148">**ResourceGroupName**: hello uygulama hizmeti planı barındıran kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="86e89-148">**ResourceGroupName**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="86e89-149">**Konum**: Merhaba web uygulama konumu.</span><span class="sxs-lookup"><span data-stu-id="86e89-149">**Location**: hello web app location.</span></span>

<span data-ttu-id="86e89-150">Örnek toouse Bu cmdlet:</span><span class="sxs-lookup"><span data-stu-id="86e89-150">Example toouse this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="86e89-151">Bir uygulama hizmeti ortamı'nda bir Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="86e89-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="86e89-152">toocreate bir web uygulaması bir uygulama hizmeti ortamı (ana).</span><span class="sxs-lookup"><span data-stu-id="86e89-152">toocreate a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="86e89-153">Kullanım hello aynı **yeni AzureRmWebApp** ek parametreler toospecify hello ana adı hello ana ait hello kaynak grubu adı ile komutu.</span><span class="sxs-lookup"><span data-stu-id="86e89-153">Use hello same **New-AzureRmWebApp** command with extra parameters toospecify hello ASE name and hello resource group name that hello ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="86e89-154">uygulama hizmeti ortamı, denetimi hakkında daha fazla toolearn [giriş tooApp hizmeti ortamı](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="86e89-154">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="86e89-155">Var olan bir Web uygulamasının Sil</span><span class="sxs-lookup"><span data-stu-id="86e89-155">Delete an existing Web App</span></span>
<span data-ttu-id="86e89-156">toodelete hello kullanabileceğiniz var olan bir web uygulamasının **Kaldır AzureRmWebApp** cmdlet'ini toospecify hello hello web uygulaması adını ve hello kaynak grubu adı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="86e89-156">toodelete an existing web app you can use hello **Remove-AzureRmWebApp** cmdlet, you need toospecify hello name of hello web app and hello resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="86e89-157">Var olan Web Apps listesi</span><span class="sxs-lookup"><span data-stu-id="86e89-157">List existing Web Apps</span></span>
<span data-ttu-id="86e89-158">toolist hello varolan web uygulamaları, hello kullanma **Get-AzureRmWebApp** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="86e89-158">toolist hello existing web apps, use hello **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="86e89-159">toolist, aboneliğinizdeki tüm web uygulamaları kullanın:</span><span class="sxs-lookup"><span data-stu-id="86e89-159">toolist all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="86e89-160">toolist belirli kaynak grubundaki tüm web uygulamaları kullanın:</span><span class="sxs-lookup"><span data-stu-id="86e89-160">toolist all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="86e89-161">tooget belirli web uygulaması kullanın:</span><span class="sxs-lookup"><span data-stu-id="86e89-161">tooget a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="86e89-162">Var olan bir Web uygulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="86e89-162">Configure an existing Web App</span></span>
<span data-ttu-id="86e89-163">toochange hello ayarları ve var olan bir web uygulaması için yapılandırmaları kullanmak hello **kümesi AzureRmWebApp** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="86e89-163">toochange hello settings and configurations for an existing web app, use hello **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="86e89-164">Parametrelerin tam bir listesi için hello denetleyin [Cmdlet başvuru bağlantısı](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="86e89-164">For a full list of parameters, check hello [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="86e89-165">Örnek (1): Bu cmdlet toochange bağlantı dizelerini kullanın</span><span class="sxs-lookup"><span data-stu-id="86e89-165">Example (1): use this cmdlet toochange connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="86e89-166">(2) örnek: ekleme veya uygulama ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="86e89-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="86e89-167">(3) örnek: Merhaba web uygulama toorun 64-bit modunda ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="86e89-167">Example (3):  set hello web app toorun in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a><span data-ttu-id="86e89-168">Var olan bir Web uygulamasının Hello durumunu değiştir</span><span class="sxs-lookup"><span data-stu-id="86e89-168">Change hello state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="86e89-169">Bir web uygulaması yeniden</span><span class="sxs-lookup"><span data-stu-id="86e89-169">Restart a web app</span></span>
<span data-ttu-id="86e89-170">bir web uygulaması toorestart, hello web uygulamasının hello ad ve kaynak grubu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e89-170">toorestart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="86e89-171">Bir web uygulamasını Durdur</span><span class="sxs-lookup"><span data-stu-id="86e89-171">Stop a web app</span></span>
<span data-ttu-id="86e89-172">bir web uygulaması toostop, hello web uygulamasının hello ad ve kaynak grubu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e89-172">toostop a web app, you must specify hello name and resource group of hello web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="86e89-173">Bir web uygulaması başlatın</span><span class="sxs-lookup"><span data-stu-id="86e89-173">Start a web app</span></span>
<span data-ttu-id="86e89-174">bir web uygulaması toostart, hello web uygulamasının hello ad ve kaynak grubu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e89-174">toostart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="86e89-175">Web uygulaması yayımlama profillerini yönet</span><span class="sxs-lookup"><span data-stu-id="86e89-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="86e89-176">Her web uygulaması kullanılan toopublish olabilir bir yayımlama profili uygulamalarınızı sahip, çeşitli işlemleri profilleri yayımlama çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="86e89-176">Each web app has a publishing profile that can be used toopublish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="86e89-177">Yayımlama profilini Al</span><span class="sxs-lookup"><span data-stu-id="86e89-177">Get Publishing Profile</span></span>
<span data-ttu-id="86e89-178">Yayımlama profilini kullan bir web uygulaması için tooget hello:</span><span class="sxs-lookup"><span data-stu-id="86e89-178">tooget hello publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="86e89-179">Bu komut, profil toohello komut satırı de yayımlama hello profili tooa metin dosyası yayımlama hello çıktı görüntülemektedir.</span><span class="sxs-lookup"><span data-stu-id="86e89-179">This command echoes hello publishing profile toohello command line as well output hello publishing profile tooa text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="86e89-180">Yayımlama profilini Sıfırla</span><span class="sxs-lookup"><span data-stu-id="86e89-180">Reset Publishing Profile</span></span>
<span data-ttu-id="86e89-181">tooreset her ikisi de hello yayımlama parolası kullanmak bir web uygulaması için FTP ve web dağıtmak için:</span><span class="sxs-lookup"><span data-stu-id="86e89-181">tooreset both hello publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="86e89-182">Web uygulaması sertifikaları yönetme</span><span class="sxs-lookup"><span data-stu-id="86e89-182">Manage Web App Certificates</span></span>
<span data-ttu-id="86e89-183">toolearn nasıl toomanage web uygulaması sertifikalar hakkında bkz [PowerShell kullanarak SSL sertifikalarını bağlama](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="86e89-183">toolearn about how toomanage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="86e89-184">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="86e89-184">Next Steps</span></span>
* <span data-ttu-id="86e89-185">Azure Resource Manager PowerShell desteği hakkında toolearn bakın [Azure PowerShell kullanarak Azure Resource Manager ile.](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="86e89-185">toolearn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="86e89-186">Uygulama hizmeti ortamları hakkında toolearn bakın [giriş tooApp hizmeti ortamı.](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="86e89-186">toolearn about App Service Environments, see [Introduction tooApp Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="86e89-187">PowerShell kullanarak uygulama hizmeti SSL sertifikaların yönetilmesi hakkında toolearn bakın [PowerShell kullanarak SSL sertifikalarını bağlama.](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="86e89-187">toolearn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="86e89-188">toolearn hello tam listesi için Azure Web uygulamaları, Azure Resource Manager tabanlı PowerShell cmdlet'leri hakkında bkz [, Web uygulamaları Azure Resource Manager PowerShell cmdlet'lerinin Azure Cmdlet başvurusu.](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="86e89-188">toolearn about hello full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="86e89-189">Uygulama hizmeti, CLI kullanarak yönetme hakkında toolearn bkz [Using Azure Resource Manager-Based XPlat CLI Azure Web uygulaması için.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span><span class="sxs-lookup"><span data-stu-id="86e89-189">toolearn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

