---
title: "Azure Web uygulaması için Resource Manager tabanlı platformlar arası komut satırı araçları aaaAzure | Microsoft Docs"
description: "Nasıl toouse hello yeni Azure Resource Manager tabanlı platformlar arası komut satırı araçları toomanage Azure Web Apps hakkında bilgi edinin."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="b4caf-103">Azure uygulama hizmeti için Azure Resource Manager tabanlı XPlat CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="b4caf-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b4caf-104">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b4caf-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="b4caf-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4caf-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="b4caf-106">Microsoft Azure platformlar arası komut satırı araçları sürüm 0.10.5 Hello sürümle yeni komutları eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="b4caf-106">With hello release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="b4caf-107">Bu komutlar hello kullanıcı hello özelliği toouse Azure Resource Manager tabanlı PowerShell komutları toomanage uygulama hizmeti verin.</span><span class="sxs-lookup"><span data-stu-id="b4caf-107">These commands give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage App Service.</span></span>

<span data-ttu-id="b4caf-108">Kaynak gruplarını yönetme hakkında toolearn bkz [hello Azure CLI toomanage Azure kullanmak kaynaklar ve kaynak grupları](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b4caf-108">toolearn about managing Resource Groups, see [Use hello Azure CLI toomanage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="b4caf-109">Ayrıca, denemenin [Azure CLI 2.0](https://github.com/Azure/azure-cli), yeni nesil CLI hello kaynak yönetimi dağıtım modeli için Python içinde yazılmış.</span><span class="sxs-lookup"><span data-stu-id="b4caf-109">Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for hello resource management deployment model.</span></span>
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="b4caf-110">Uygulama hizmeti yönetme planları</span><span class="sxs-lookup"><span data-stu-id="b4caf-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="b4caf-111">Bir uygulama hizmeti planı oluştur</span><span class="sxs-lookup"><span data-stu-id="b4caf-111">Create an App Service Plan</span></span>
<span data-ttu-id="b4caf-112">bir uygulama hizmeti planı toocreate hello kullan **azure appserviceplan oluşturma** komutu.</span><span class="sxs-lookup"><span data-stu-id="b4caf-112">toocreate an app service plan, use hello **azure appserviceplan create** command.</span></span>

<span data-ttu-id="b4caf-113">Merhaba farklı parametreler açıklamalarını şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b4caf-113">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="b4caf-114">**--kaynak-grubu**: yeni oluşturulan hello uygulama hizmeti planı içeren kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="b4caf-114">**--resource-group**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="b4caf-115">**--ad**: hello uygulama hizmeti planının adı.</span><span class="sxs-lookup"><span data-stu-id="b4caf-115">**--name**: name of hello app service plan.</span></span>
* <span data-ttu-id="b4caf-116">**--Konum**: uygulama hizmeti planı konumu.</span><span class="sxs-lookup"><span data-stu-id="b4caf-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="b4caf-117">**--sku**: hello istenen fiyatlandırma sku (Merhaba Seçenekler şunlardır: F1 (ücretsiz).</span><span class="sxs-lookup"><span data-stu-id="b4caf-117">**--sku**:  hello desired pricing sku (hello options are: F1 (Free).</span></span> <span data-ttu-id="b4caf-118">D1 (paylaşılan).</span><span class="sxs-lookup"><span data-stu-id="b4caf-118">D1 (Shared).</span></span> <span data-ttu-id="b4caf-119">B1 (temel küçük), B2 (temel ortamı) ve B3 (Basic büyük).</span><span class="sxs-lookup"><span data-stu-id="b4caf-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="b4caf-120">S1 (standart küçük), S2 (standart ortamı) ve S3 (standart büyük).</span><span class="sxs-lookup"><span data-stu-id="b4caf-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="b4caf-121">P1 (Premium küçük), P2 (Premium ortamı) ve P3 (Premium büyük).)</span><span class="sxs-lookup"><span data-stu-id="b4caf-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="b4caf-122">**--örnekleri**: (varsayılan değer 1'dir) hello uygulama hizmeti planında hello çalışan sayısı.</span><span class="sxs-lookup"><span data-stu-id="b4caf-122">**--instances**: hello number of workers in hello app service plan (Default value is 1).</span></span>

<span data-ttu-id="b4caf-123">Örnek toouse Bu cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b4caf-123">Example toouse this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="b4caf-124">Linux uygulama hizmeti planı oluştur</span><span class="sxs-lookup"><span data-stu-id="b4caf-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="b4caf-125">Kullanarak, hello aynı **azure appserviceplan oluşturma** hello ile komutu ek parametre **--islinux true**.</span><span class="sxs-lookup"><span data-stu-id="b4caf-125">Using hello same **azure appserviceplan create** command, with hello extra parameter **--islinux true**.</span></span> <span data-ttu-id="b4caf-126">Not hello kısıtlamaları ve özetlenen bölgeleri [giriş tooApp Linux hizmeti](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="b4caf-126">Note hello restrictions and regions outlined in [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="b4caf-127">Var olan uygulama hizmeti planları listesi</span><span class="sxs-lookup"><span data-stu-id="b4caf-127">List Existing App Service Plans</span></span>
<span data-ttu-id="b4caf-128">toolist hello var olan uygulama hizmeti planları kullanın **azure appserviceplan listesi** komutu.</span><span class="sxs-lookup"><span data-stu-id="b4caf-128">toolist hello existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="b4caf-129">toolist belirli kaynak grubundaki tüm uygulama hizmeti planları kullanın:</span><span class="sxs-lookup"><span data-stu-id="b4caf-129">toolist all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="b4caf-130">tooget belirli uygulama hizmeti planı kullanmak **azure appserviceplan Göster** komutu:</span><span class="sxs-lookup"><span data-stu-id="b4caf-130">tooget a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="b4caf-131">Var olan bir App Service planı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="b4caf-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="b4caf-132">var olan bir uygulama hizmeti planı toochange hello ayarlarını kullan hello **azure appserviceplan config** komutu.</span><span class="sxs-lookup"><span data-stu-id="b4caf-132">toochange hello settings for an existing app service plan, use hello **azure appserviceplan config** command.</span></span> <span data-ttu-id="b4caf-133">Merhaba sku ve çalışan hello sayısı değiştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b4caf-133">You can change hello sku, and hello number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="b4caf-134">Bir uygulama hizmeti planı ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="b4caf-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="b4caf-135">tooscale bir var olan uygulama hizmeti planı, kullanın:</span><span class="sxs-lookup"><span data-stu-id="b4caf-135">tooscale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a><span data-ttu-id="b4caf-136">Bir uygulama hizmeti planı SKU'su Hello değiştirme</span><span class="sxs-lookup"><span data-stu-id="b4caf-136">Changing hello SKU of an App Service Plan</span></span>
<span data-ttu-id="b4caf-137">toochange hello SKU'su bir var olan uygulama hizmeti planı, kullanın:</span><span class="sxs-lookup"><span data-stu-id="b4caf-137">toochange hello sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="b4caf-138">Var olan bir uygulama hizmeti planı silme</span><span class="sxs-lookup"><span data-stu-id="b4caf-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="b4caf-139">toodelete var olan bir uygulama hizmeti planı, tüm taşınmış veya silinmiş ilk uygulamaları gerek toobe atanır.</span><span class="sxs-lookup"><span data-stu-id="b4caf-139">toodelete an existing app service plan, all assigned apps need toobe moved or deleted first.</span></span> <span data-ttu-id="b4caf-140">Hello kullanarak **azure webapp silme** komutu hello uygulama hizmeti planı silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4caf-140">Then using hello **azure webapp delete** command you can delete hello app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="b4caf-141">Uygulama hizmeti uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="b4caf-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="b4caf-142">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b4caf-142">Create a web app</span></span>
<span data-ttu-id="b4caf-143">toocreate bir web uygulaması kullanın hello **azure webapp oluşturmak** komutu.</span><span class="sxs-lookup"><span data-stu-id="b4caf-143">toocreate a web app, use hello **azure webapp create** command.</span></span>

<span data-ttu-id="b4caf-144">Merhaba farklı parametreler açıklamalarını şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b4caf-144">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="b4caf-145">**--ad**: hello web uygulamasının adı.</span><span class="sxs-lookup"><span data-stu-id="b4caf-145">**--name**: name for hello web app.</span></span>
* <span data-ttu-id="b4caf-146">**--planı**: hello hizmet planı toohost hello web uygulaması kullanılan ad.</span><span class="sxs-lookup"><span data-stu-id="b4caf-146">**--plan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="b4caf-147">**--kaynak-grubu**: hello uygulama hizmeti planı barındıran kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="b4caf-147">**--resource-group**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="b4caf-148">**--Konum**: Merhaba web uygulama konumu.</span><span class="sxs-lookup"><span data-stu-id="b4caf-148">**--location**: hello web app location.</span></span>

<span data-ttu-id="b4caf-149">Örnek toouse Bu cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b4caf-149">Example toouse this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="b4caf-150">Mevcut bir uygulamayı Sil</span><span class="sxs-lookup"><span data-stu-id="b4caf-150">Delete an existing app</span></span>
<span data-ttu-id="b4caf-151">Mevcut bir uygulamayı toodelete hello kullanabilir **azure webapp silme** komutu.</span><span class="sxs-lookup"><span data-stu-id="b4caf-151">toodelete an existing app, you can use hello **azure webapp delete** command.</span></span> <span data-ttu-id="b4caf-152">Toospecify hello hello uygulama adını ve hello kaynak grubu adı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="b4caf-152">You need toospecify hello name of hello app and hello resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="b4caf-153">Var olan uygulamalar listesi</span><span class="sxs-lookup"><span data-stu-id="b4caf-153">List existing apps</span></span>
<span data-ttu-id="b4caf-154">toolist hello mevcut uygulamaları, hello kullanma **azure webapp listesi** komutu.</span><span class="sxs-lookup"><span data-stu-id="b4caf-154">toolist hello existing apps, use hello **azure webapp list** command.</span></span>

<span data-ttu-id="b4caf-155">belirli bir kaynak grubundaki tüm uygulamalar toolist kullanın:</span><span class="sxs-lookup"><span data-stu-id="b4caf-155">toolist all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="b4caf-156">tooget belirli bir uygulamayı kullanmak hello **azure webapp Göster** komutu.</span><span class="sxs-lookup"><span data-stu-id="b4caf-156">tooget a specific app, use hello **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="b4caf-157">Mevcut bir uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b4caf-157">Configure an existing app</span></span>
<span data-ttu-id="b4caf-158">toochange hello ayarları ve var olan bir uygulama için yapılandırmaları kullanmak hello **azure webapp yapılandırma kümesi** komutu.</span><span class="sxs-lookup"><span data-stu-id="b4caf-158">toochange hello settings and configurations for an existing app, use hello **azure webapp config set** command.</span></span>

<span data-ttu-id="b4caf-159">(1) örnek: bir uygulamanın hello php sürümünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="b4caf-159">Example (1): change hello php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="b4caf-160">(2) örnek: ekleme veya uygulama ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="b4caf-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="b4caf-161">hangi diğer yapılandırma değiştirilebilir, tooknow kullanım hello **set -h azure webapp config** komutu.</span><span class="sxs-lookup"><span data-stu-id="b4caf-161">tooknow what other configuration can be changed, use hello **azure webapp config set -h** command.</span></span>

### <a name="change-hello-state-of-an-existing-app"></a><span data-ttu-id="b4caf-162">Mevcut bir uygulamayı Hello durumunu değiştir</span><span class="sxs-lookup"><span data-stu-id="b4caf-162">Change hello state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="b4caf-163">Bir uygulamayı yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="b4caf-163">Restart an app</span></span>
<span data-ttu-id="b4caf-164">toorestart uygulama bir hello uygulamasının hello ad ve kaynak grubu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4caf-164">toorestart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="b4caf-165">Bir uygulamayı durdurun</span><span class="sxs-lookup"><span data-stu-id="b4caf-165">Stop an app</span></span>
<span data-ttu-id="b4caf-166">toostop uygulama bir hello uygulamasının hello ad ve kaynak grubu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4caf-166">toostop an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="b4caf-167">Bir uygulamayı başlatın</span><span class="sxs-lookup"><span data-stu-id="b4caf-167">Start an app</span></span>
<span data-ttu-id="b4caf-168">toostart uygulama bir hello uygulamasının hello ad ve kaynak grubu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4caf-168">toostart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="b4caf-169">Uygulama yayımlama profillerini yönet</span><span class="sxs-lookup"><span data-stu-id="b4caf-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="b4caf-170">Her uygulamanın kodunuzu kullanılan toopublish olabilir bir yayımlama profili yok.</span><span class="sxs-lookup"><span data-stu-id="b4caf-170">Each app has a publishing profile that can be used toopublish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="b4caf-171">Yayımlama profilini Al</span><span class="sxs-lookup"><span data-stu-id="b4caf-171">Get Publishing Profile</span></span>
<span data-ttu-id="b4caf-172">Yayımlama profilini bir uygulama kullanmak için tooget hello:</span><span class="sxs-lookup"><span data-stu-id="b4caf-172">tooget hello publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="b4caf-173">Bu komut, kullanıcı adı ve parola toohello komut satırı profili yayımlama hello görüntülemektedir.</span><span class="sxs-lookup"><span data-stu-id="b4caf-173">This command echoes hello publishing profile username and password toohello command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="b4caf-174">Uygulama ana bilgisayar adlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="b4caf-174">Manage app hostnames</span></span>
<span data-ttu-id="b4caf-175">toomanage konak adı bağlamaları, uygulamanız için kullanmak hello **azure webapp config ana bilgisayar adları** komutu</span><span class="sxs-lookup"><span data-stu-id="b4caf-175">toomanage hostname bindings for your app, use hello **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="b4caf-176">Liste konak adı bağlamaları</span><span class="sxs-lookup"><span data-stu-id="b4caf-176">List hostname bindings</span></span>
<span data-ttu-id="b4caf-177">bir uygulama tooget hello geçerli konak adı bağlamaları kullanın:</span><span class="sxs-lookup"><span data-stu-id="b4caf-177">tooget hello current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="b4caf-178">Konak adı bağlamaları Ekle</span><span class="sxs-lookup"><span data-stu-id="b4caf-178">Add hostname bindings</span></span>
<span data-ttu-id="b4caf-179">tooadd konak adı bağlamaları tooan uygulama, kullanın:</span><span class="sxs-lookup"><span data-stu-id="b4caf-179">tooadd hostname bindings tooan app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="b4caf-180">Konak adı bağlamaları Sil</span><span class="sxs-lookup"><span data-stu-id="b4caf-180">Delete hostname bindings</span></span>
<span data-ttu-id="b4caf-181">toodelete konak adı bağlamaları kullanın:</span><span class="sxs-lookup"><span data-stu-id="b4caf-181">toodelete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="b4caf-182">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="b4caf-182">Next Steps</span></span>
* <span data-ttu-id="b4caf-183">Azure Resource Manager CLI desteği hakkında toolearn bakın [hello Azure CLI toomanage Azure kullanmak kaynaklar ve kaynak grupları.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="b4caf-183">toolearn about Azure Resource Manager CLI support, see [Use hello Azure CLI toomanage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="b4caf-184">Uygulama hizmeti PowerShell kullanarak yönetme hakkında toolearn bkz [Using Azure Resource Manager-Based PowerShell tooManage Azure Web uygulamaları.](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="b4caf-184">toolearn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="b4caf-185">toolearn Linux üzerinde Azure App Service hakkında bkz [giriş tooApp Linux hizmeti](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="b4caf-185">toolearn about Azure App Service on Linux, see [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>
