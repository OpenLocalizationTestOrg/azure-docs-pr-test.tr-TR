---
title: "Azure PowerShell ile Azure Redis önbelleği aaaManage | Microsoft Docs"
description: "Bilgi nasıl tooperform yönetim görevlerini Azure PowerShell kullanarak Azure Redis önbelleği için."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1136efe5-1e33-4d91-bb49-c8e2a6dca475
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 1d526ce65c4bc05345cd6c3ff370211ed562cab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a><span data-ttu-id="47e17-103">Azure PowerShell ile Azure Redis önbelleği Yönet</span><span class="sxs-lookup"><span data-stu-id="47e17-103">Manage Azure Redis Cache with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="47e17-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="47e17-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="47e17-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="47e17-105">Azure CLI</span></span>](cache-manage-cli.md)
> 
> 

<span data-ttu-id="47e17-106">Bu konu nasıl tooperform ortak oluşturmak gibi görevleri gösterir, güncelleştirme ve Azure Redis önbelleği örneklerinizi nasıl ölçeklendirin tooregenerate erişim anahtarlarını ve nasıl tooview önbellekleri hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="47e17-106">This topic shows you how tooperform common tasks such as create, update, and scale your Azure Redis Cache instances, how tooregenerate access keys, and how tooview information about your caches.</span></span> <span data-ttu-id="47e17-107">Azure Redis önbelleği PowerShell cmdlet'lerinin tam listesi için bkz: [Azure Redis önbelleği cmdlet'leri](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span><span class="sxs-lookup"><span data-stu-id="47e17-107">For a complete list of Azure Redis Cache PowerShell cmdlets, see [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="47e17-108">Merhaba Klasik dağıtım modeli hakkında daha fazla bilgi için bkz: [Azure Resource Manager ve klasik dağıtım: dağıtım modellerini anlama ve hello kaynaklarınızın durumunu](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span><span class="sxs-lookup"><span data-stu-id="47e17-108">For more information about hello classic deployment model, see [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47e17-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="47e17-109">Prerequisites</span></span>
<span data-ttu-id="47e17-110">Azure PowerShell'i zaten yüklediyseniz, Azure PowerShell sürümü 1.0.0 olmalıdır veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="47e17-110">If you have already installed Azure PowerShell, you must have Azure PowerShell version 1.0.0 or later.</span></span> <span data-ttu-id="47e17-111">Bu komutla hello Azure PowerShell komut isteminde yüklediğiniz Azure PowerShell hello sürümü kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47e17-111">You can check hello version of Azure PowerShell that you have installed with this command at hello Azure PowerShell command prompt.</span></span>

    Get-Module azure | format-table version


<span data-ttu-id="47e17-112">İlk olarak, bu komutla tooAzure olarak oturum açmalısınız.</span><span class="sxs-lookup"><span data-stu-id="47e17-112">First, you must log in tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="47e17-113">Merhaba Microsoft Azure oturum açma iletişim kutusunda Azure hesabınızı ve kendi parolasını Hello e-posta adresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="47e17-113">Specify hello email address of your Azure account and its password in hello Microsoft Azure sign-in dialog.</span></span>

<span data-ttu-id="47e17-114">Ardından, birden çok Azure aboneliğiniz varsa, Azure aboneliğinizin tooset gerekir.</span><span class="sxs-lookup"><span data-stu-id="47e17-114">Next, if you have multiple Azure subscriptions, you need tooset your Azure subscription.</span></span> <span data-ttu-id="47e17-115">toosee geçerli aboneliklerinizi listesini bu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="47e17-115">toosee a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="47e17-116">toospecify hello abonelik, komutu aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="47e17-116">toospecify hello subscription, run hello following command.</span></span> <span data-ttu-id="47e17-117">Aşağıdaki örneğine hello hello abonelik adıdır `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="47e17-117">In hello following example, hello subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

<span data-ttu-id="47e17-118">Azure Resource Manager ile Windows PowerShell kullanabilmeniz için önce hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="47e17-118">Before you can use Windows PowerShell with Azure Resource Manager, you need hello following:</span></span>

* <span data-ttu-id="47e17-119">Windows PowerShell sürüm 3.0 veya 4.0.</span><span class="sxs-lookup"><span data-stu-id="47e17-119">Windows PowerShell, Version 3.0 or 4.0.</span></span> <span data-ttu-id="47e17-120">Windows PowerShell, türü toofind hello sürümü:`$PSVersionTable` ve hello değerini doğrulayın `PSVersion` 3.0 veya 4.0.</span><span class="sxs-lookup"><span data-stu-id="47e17-120">toofind hello version of Windows PowerShell, type:`$PSVersionTable` and verify hello value of `PSVersion` is 3.0 or 4.0.</span></span> <span data-ttu-id="47e17-121">tooinstall uyumlu bir sürümde bkz [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) veya [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="47e17-121">tooinstall a compatible version, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

<span data-ttu-id="47e17-122">tooget ayrıntılı hello Get-Help cmdlet'ini kullanın Bu öğreticide gördüğünüz herhangi bir cmdlet için Yardım.</span><span class="sxs-lookup"><span data-stu-id="47e17-122">tooget detailed help for any cmdlet you see in this tutorial, use hello Get-Help cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="47e17-123">Örneğin, tooget yardımını hello `New-AzureRmRedisCache` cmdlet, türü:</span><span class="sxs-lookup"><span data-stu-id="47e17-123">For example, tooget help for hello `New-AzureRmRedisCache` cmdlet, type:</span></span>

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-tooconnect-tooother-clouds"></a><span data-ttu-id="47e17-124">Nasıl tooconnect tooother Bulutlar</span><span class="sxs-lookup"><span data-stu-id="47e17-124">How tooconnect tooother clouds</span></span>
<span data-ttu-id="47e17-125">Varsayılan hello Azure tarafından ortamıdır `AzureCloud`, hangi hello genel Azure bulut örneği temsil eder.</span><span class="sxs-lookup"><span data-stu-id="47e17-125">By default hello Azure environment is `AzureCloud`, which represents hello global Azure cloud instance.</span></span> <span data-ttu-id="47e17-126">tooconnect tooa farklı bir örnek, kullanım hello `Add-AzureRmAccount` hello komutunu `-Environment` veya -`EnvironmentName` komut satırı anahtarıyla hello istenen ortama veya ortam adı.</span><span class="sxs-lookup"><span data-stu-id="47e17-126">tooconnect tooa different instance, use hello `Add-AzureRmAccount` command with hello `-Environment` or -`EnvironmentName` command line switch with hello desired environment or environment name.</span></span>

<span data-ttu-id="47e17-127">Merhaba çalıştırmak kullanılabilir ortamları toosee hello listesi `Get-AzureRmEnvironment` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="47e17-127">toosee hello list of available environments, run hello `Get-AzureRmEnvironment` cmdlet.</span></span>

### <a name="tooconnect-toohello-azure-government-cloud"></a><span data-ttu-id="47e17-128">tooconnect toohello Azure Bulutu</span><span class="sxs-lookup"><span data-stu-id="47e17-128">tooconnect toohello Azure Government Cloud</span></span>
<span data-ttu-id="47e17-129">tooconnect toohello Azure Bulutu komutları aşağıdaki hello birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="47e17-129">tooconnect toohello Azure Government Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

<span data-ttu-id="47e17-130">or</span><span class="sxs-lookup"><span data-stu-id="47e17-130">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

<span data-ttu-id="47e17-131">toocreate hello Azure Bulutu önbelleğinde hello aşağıdaki konumlardan birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="47e17-131">toocreate a cache in hello Azure Government Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="47e17-132">ABD hükümeti Virginia</span><span class="sxs-lookup"><span data-stu-id="47e17-132">USGov Virginia</span></span>
* <span data-ttu-id="47e17-133">ABD hükümeti Iowa</span><span class="sxs-lookup"><span data-stu-id="47e17-133">USGov Iowa</span></span>

<span data-ttu-id="47e17-134">Hello Azure Bulutu hakkında daha fazla bilgi için bkz: [Microsoft Azure kamu](https://azure.microsoft.com/features/gov/) ve [Microsoft Azure kamu Geliştirici Kılavuzu](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="47e17-134">For more information about hello Azure Government Cloud, see [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) and [Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>

### <a name="tooconnect-toohello-azure-china-cloud"></a><span data-ttu-id="47e17-135">tooconnect toohello Azure Çin bulut</span><span class="sxs-lookup"><span data-stu-id="47e17-135">tooconnect toohello Azure China Cloud</span></span>
<span data-ttu-id="47e17-136">tooconnect toohello Azure Çin bulut komutları aşağıdaki hello birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="47e17-136">tooconnect toohello Azure China Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

<span data-ttu-id="47e17-137">or</span><span class="sxs-lookup"><span data-stu-id="47e17-137">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

<span data-ttu-id="47e17-138">toocreate hello Azure Çin bulut önbelleğinde hello aşağıdaki konumlardan birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="47e17-138">toocreate a cache in hello Azure China Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="47e17-139">Çin Doğu</span><span class="sxs-lookup"><span data-stu-id="47e17-139">China East</span></span>
* <span data-ttu-id="47e17-140">Çin Kuzey</span><span class="sxs-lookup"><span data-stu-id="47e17-140">China North</span></span>

<span data-ttu-id="47e17-141">Hello Azure Çin bulut hakkında daha fazla bilgi için bkz: [AzureChinaCloud Azure Çin'de 21Vianet tarafından işletilen](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="47e17-141">For more information about hello Azure China Cloud, see [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span>

### <a name="tooconnect-toomicrosoft-azure-germany"></a><span data-ttu-id="47e17-142">tooconnect tooMicrosoft Azure Almanya</span><span class="sxs-lookup"><span data-stu-id="47e17-142">tooconnect tooMicrosoft Azure Germany</span></span>
<span data-ttu-id="47e17-143">tooconnect tooMicrosoft Azure Almanya komutları aşağıdaki hello birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="47e17-143">tooconnect tooMicrosoft Azure Germany, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


<span data-ttu-id="47e17-144">or</span><span class="sxs-lookup"><span data-stu-id="47e17-144">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

<span data-ttu-id="47e17-145">Microsoft Azure Almanya, önbellekte toocreate hello aşağıdaki konumlardan birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="47e17-145">toocreate a cache in Microsoft Azure Germany, use one of hello following locations.</span></span>

* <span data-ttu-id="47e17-146">Almanya Orta</span><span class="sxs-lookup"><span data-stu-id="47e17-146">Germany Central</span></span>
* <span data-ttu-id="47e17-147">Almanya Kuzeydoğu</span><span class="sxs-lookup"><span data-stu-id="47e17-147">Germany Northeast</span></span>

<span data-ttu-id="47e17-148">Microsoft Azure Almanya hakkında daha fazla bilgi için bkz: [Microsoft Azure Almanya](https://azure.microsoft.com/overview/clouds/germany/).</span><span class="sxs-lookup"><span data-stu-id="47e17-148">For more information about Microsoft Azure Germany, see [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).</span></span>

### <a name="properties-used-for-azure-redis-cache-powershell"></a><span data-ttu-id="47e17-149">Azure Redis önbelleği PowerShell için kullanılan özellikleri</span><span class="sxs-lookup"><span data-stu-id="47e17-149">Properties used for Azure Redis Cache PowerShell</span></span>
<span data-ttu-id="47e17-150">Aşağıdaki tablonun hello özellikleri ve açıklamaları oluştururken ve Azure PowerShell kullanarak Azure Redis önbelleği örneklerinizi yönetme yaygın olarak kullanılan parametreleri içerir.</span><span class="sxs-lookup"><span data-stu-id="47e17-150">hello following table contains properties and descriptions for commonly used parameters when creating and managing your Azure Redis Cache instances using Azure PowerShell.</span></span>

| <span data-ttu-id="47e17-151">Parametre</span><span class="sxs-lookup"><span data-stu-id="47e17-151">Parameter</span></span> | <span data-ttu-id="47e17-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="47e17-152">Description</span></span> | <span data-ttu-id="47e17-153">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="47e17-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47e17-154">Ad</span><span class="sxs-lookup"><span data-stu-id="47e17-154">Name</span></span> |<span data-ttu-id="47e17-155">Merhaba önbellek adı</span><span class="sxs-lookup"><span data-stu-id="47e17-155">Name of hello cache</span></span> | |
| <span data-ttu-id="47e17-156">Konum</span><span class="sxs-lookup"><span data-stu-id="47e17-156">Location</span></span> |<span data-ttu-id="47e17-157">Merhaba önbellek konumu</span><span class="sxs-lookup"><span data-stu-id="47e17-157">Location of hello cache</span></span> | |
| <span data-ttu-id="47e17-158">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="47e17-158">ResourceGroupName</span></span> |<span data-ttu-id="47e17-159">Hangi toocreate hello önbelleğinde kaynak grubu adı</span><span class="sxs-lookup"><span data-stu-id="47e17-159">Resource group name in which toocreate hello cache</span></span> | |
| <span data-ttu-id="47e17-160">Boyut</span><span class="sxs-lookup"><span data-stu-id="47e17-160">Size</span></span> |<span data-ttu-id="47e17-161">Merhaba önbellek boyutunu Hello.</span><span class="sxs-lookup"><span data-stu-id="47e17-161">hello size of hello cache.</span></span> <span data-ttu-id="47e17-162">Geçerli değerler: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5 GB, 6 GB, 13 GB, 26 GB, 53 GB'a</span><span class="sxs-lookup"><span data-stu-id="47e17-162">Valid values are: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB</span></span> |<span data-ttu-id="47e17-163">1 GB</span><span class="sxs-lookup"><span data-stu-id="47e17-163">1GB</span></span> |
| <span data-ttu-id="47e17-164">ShardCount</span><span class="sxs-lookup"><span data-stu-id="47e17-164">ShardCount</span></span> |<span data-ttu-id="47e17-165">premium önbelleği kümeleme özelliği etkinleştirilmiş oluştururken parça toocreate Hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="47e17-165">hello number of shards toocreate when creating a premium cache with clustering enabled.</span></span> <span data-ttu-id="47e17-166">Geçerli değerler: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span><span class="sxs-lookup"><span data-stu-id="47e17-166">Valid values are: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span></span> | |
| <span data-ttu-id="47e17-167">SKU</span><span class="sxs-lookup"><span data-stu-id="47e17-167">SKU</span></span> |<span data-ttu-id="47e17-168">Merhaba hello önbellek SKU'su belirtir.</span><span class="sxs-lookup"><span data-stu-id="47e17-168">Specifies hello SKU of hello cache.</span></span> <span data-ttu-id="47e17-169">Geçerli değerler: temel, standart ve Premium</span><span class="sxs-lookup"><span data-stu-id="47e17-169">Valid values are: Basic, Standard, Premium</span></span> |<span data-ttu-id="47e17-170">Standart</span><span class="sxs-lookup"><span data-stu-id="47e17-170">Standard</span></span> |
| <span data-ttu-id="47e17-171">RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="47e17-171">RedisConfiguration</span></span> |<span data-ttu-id="47e17-172">Redis yapılandırma ayarlarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="47e17-172">Specifies Redis configuration settings.</span></span> <span data-ttu-id="47e17-173">Merhaba aşağıdaki her ayarlama hakkında daha fazla bilgi için bkz: [RedisConfiguration özellikleri](#redisconfiguration-properties) tablo.</span><span class="sxs-lookup"><span data-stu-id="47e17-173">For details on each setting, see hello following [RedisConfiguration properties](#redisconfiguration-properties) table.</span></span> | |
| <span data-ttu-id="47e17-174">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="47e17-174">EnableNonSslPort</span></span> |<span data-ttu-id="47e17-175">Merhaba SSL olmayan bağlantı noktası etkinleştirilip etkinleştirilmeyeceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="47e17-175">Indicates whether hello non-SSL port is enabled.</span></span> |<span data-ttu-id="47e17-176">False</span><span class="sxs-lookup"><span data-stu-id="47e17-176">False</span></span> |
| <span data-ttu-id="47e17-177">MaxMemoryPolicy</span><span class="sxs-lookup"><span data-stu-id="47e17-177">MaxMemoryPolicy</span></span> |<span data-ttu-id="47e17-178">Bu parametre kullanım dışı - RedisConfiguration kullanın.</span><span class="sxs-lookup"><span data-stu-id="47e17-178">This parameter has been deprecated - use RedisConfiguration instead.</span></span> | |
| <span data-ttu-id="47e17-179">StaticIP</span><span class="sxs-lookup"><span data-stu-id="47e17-179">StaticIP</span></span> |<span data-ttu-id="47e17-180">Önbelleğinizi bir VNET içindeki barındırdığında hello alt hello önbelleği için benzersiz bir IP adresi belirtir.</span><span class="sxs-lookup"><span data-stu-id="47e17-180">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="47e17-181">Sağlanmazsa, bir sizin için hello alt ağdan seçilir.</span><span class="sxs-lookup"><span data-stu-id="47e17-181">If not provided, one is chosen for you from hello subnet.</span></span> | |
| <span data-ttu-id="47e17-182">Alt ağ</span><span class="sxs-lookup"><span data-stu-id="47e17-182">Subnet</span></span> |<span data-ttu-id="47e17-183">Önbelleğiniz bir VNET içindeki barındırdığında hangi toodeploy hello Önbelleği'nde hello alt hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="47e17-183">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="47e17-184">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="47e17-184">VirtualNetwork</span></span> |<span data-ttu-id="47e17-185">Önbelleğinizi bir VNET içindeki barındırma belirttiğinde hello kaynak Kimliğini VNET hangi toodeploy hello önbelleğinde hello.</span><span class="sxs-lookup"><span data-stu-id="47e17-185">When hosting your cache in a VNET, specifies hello resource ID of hello VNET in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="47e17-186">keyType</span><span class="sxs-lookup"><span data-stu-id="47e17-186">KeyType</span></span> |<span data-ttu-id="47e17-187">Hangi erişim tuşu belirtir erişim tuşları yenilenirken tooregenerate.</span><span class="sxs-lookup"><span data-stu-id="47e17-187">Specifies which access key tooregenerate when renewing access keys.</span></span> <span data-ttu-id="47e17-188">Geçerli değerler: birincil, ikincil</span><span class="sxs-lookup"><span data-stu-id="47e17-188">Valid values are: Primary, Secondary</span></span> | |

### <a name="redisconfiguration-properties"></a><span data-ttu-id="47e17-189">RedisConfiguration özellikleri</span><span class="sxs-lookup"><span data-stu-id="47e17-189">RedisConfiguration properties</span></span>
| <span data-ttu-id="47e17-190">Özellik</span><span class="sxs-lookup"><span data-stu-id="47e17-190">Property</span></span> | <span data-ttu-id="47e17-191">Açıklama</span><span class="sxs-lookup"><span data-stu-id="47e17-191">Description</span></span> | <span data-ttu-id="47e17-192">Fiyatlandırma katmanları</span><span class="sxs-lookup"><span data-stu-id="47e17-192">Pricing tiers</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47e17-193">RDB yedekleme etkin</span><span class="sxs-lookup"><span data-stu-id="47e17-193">rdb-backup-enabled</span></span> |<span data-ttu-id="47e17-194">Olup olmadığını [Redis veri kalıcılığını](cache-how-to-premium-persistence.md) etkin</span><span class="sxs-lookup"><span data-stu-id="47e17-194">Whether [Redis data persistence](cache-how-to-premium-persistence.md) is enabled</span></span> |<span data-ttu-id="47e17-195">Yalnızca Premium</span><span class="sxs-lookup"><span data-stu-id="47e17-195">Premium only</span></span> |
| <span data-ttu-id="47e17-196">RDB depolama bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="47e17-196">rdb-storage-connection-string</span></span> |<span data-ttu-id="47e17-197">Merhaba bağlantı dizesi toohello depolama hesabı için [Redis veri kalıcılığını](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="47e17-197">hello connection string toohello storage account for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="47e17-198">Yalnızca Premium</span><span class="sxs-lookup"><span data-stu-id="47e17-198">Premium only</span></span> |
| <span data-ttu-id="47e17-199">RDB yedekleme sıklığı</span><span class="sxs-lookup"><span data-stu-id="47e17-199">rdb-backup-frequency</span></span> |<span data-ttu-id="47e17-200">Merhaba yedekleme sıklığına [Redis veri kalıcılığını](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="47e17-200">hello backup frequency for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="47e17-201">Yalnızca Premium</span><span class="sxs-lookup"><span data-stu-id="47e17-201">Premium only</span></span> |
| <span data-ttu-id="47e17-202">maxmemory-ayrılmış</span><span class="sxs-lookup"><span data-stu-id="47e17-202">maxmemory-reserved</span></span> |<span data-ttu-id="47e17-203">Merhaba yapılandırır [ayrılan bellek](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) önbellek olmayan işlemler için</span><span class="sxs-lookup"><span data-stu-id="47e17-203">Configures hello [memory reserved](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for non-cache processes</span></span> |<span data-ttu-id="47e17-204">Standart ve Premium</span><span class="sxs-lookup"><span data-stu-id="47e17-204">Standard and Premium</span></span> |
| <span data-ttu-id="47e17-205">maxmemory İlkesi</span><span class="sxs-lookup"><span data-stu-id="47e17-205">maxmemory-policy</span></span> |<span data-ttu-id="47e17-206">Merhaba yapılandırır [çıkarma İlkesi](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) hello önbelleği</span><span class="sxs-lookup"><span data-stu-id="47e17-206">Configures hello [eviction policy](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for hello cache</span></span> |<span data-ttu-id="47e17-207">Tüm fiyatlandırma katmanlarına</span><span class="sxs-lookup"><span data-stu-id="47e17-207">All pricing tiers</span></span> |
| <span data-ttu-id="47e17-208">bildirim-keyspace-olayları</span><span class="sxs-lookup"><span data-stu-id="47e17-208">notify-keyspace-events</span></span> |<span data-ttu-id="47e17-209">Yapılandırır [keyspace bildirimleri](cache-configure.md#keyspace-notifications-advanced-settings)</span><span class="sxs-lookup"><span data-stu-id="47e17-209">Configures [keyspace notifications](cache-configure.md#keyspace-notifications-advanced-settings)</span></span> |<span data-ttu-id="47e17-210">Standart ve Premium</span><span class="sxs-lookup"><span data-stu-id="47e17-210">Standard and Premium</span></span> |
| <span data-ttu-id="47e17-211">max ziplist girişlerini karma</span><span class="sxs-lookup"><span data-stu-id="47e17-211">hash-max-ziplist-entries</span></span> |<span data-ttu-id="47e17-212">Yapılandırır [belleği en iyi duruma getirme](http://redis.io/topics/memory-optimization) küçük toplam veri türleri</span><span class="sxs-lookup"><span data-stu-id="47e17-212">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="47e17-213">Standart ve Premium</span><span class="sxs-lookup"><span data-stu-id="47e17-213">Standard and Premium</span></span> |
| <span data-ttu-id="47e17-214">karma-max-ziplist-değer</span><span class="sxs-lookup"><span data-stu-id="47e17-214">hash-max-ziplist-value</span></span> |<span data-ttu-id="47e17-215">Yapılandırır [belleği en iyi duruma getirme](http://redis.io/topics/memory-optimization) küçük toplam veri türleri</span><span class="sxs-lookup"><span data-stu-id="47e17-215">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="47e17-216">Standart ve Premium</span><span class="sxs-lookup"><span data-stu-id="47e17-216">Standard and Premium</span></span> |
| <span data-ttu-id="47e17-217">max intset girişlerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="47e17-217">set-max-intset-entries</span></span> |<span data-ttu-id="47e17-218">Yapılandırır [belleği en iyi duruma getirme](http://redis.io/topics/memory-optimization) küçük toplam veri türleri</span><span class="sxs-lookup"><span data-stu-id="47e17-218">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="47e17-219">Standart ve Premium</span><span class="sxs-lookup"><span data-stu-id="47e17-219">Standard and Premium</span></span> |
| <span data-ttu-id="47e17-220">max ziplist girişlerini zset</span><span class="sxs-lookup"><span data-stu-id="47e17-220">zset-max-ziplist-entries</span></span> |<span data-ttu-id="47e17-221">Yapılandırır [belleği en iyi duruma getirme](http://redis.io/topics/memory-optimization) küçük toplam veri türleri</span><span class="sxs-lookup"><span data-stu-id="47e17-221">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="47e17-222">Standart ve Premium</span><span class="sxs-lookup"><span data-stu-id="47e17-222">Standard and Premium</span></span> |
| <span data-ttu-id="47e17-223">max ziplist değeri zset</span><span class="sxs-lookup"><span data-stu-id="47e17-223">zset-max-ziplist-value</span></span> |<span data-ttu-id="47e17-224">Yapılandırır [belleği en iyi duruma getirme](http://redis.io/topics/memory-optimization) küçük toplam veri türleri</span><span class="sxs-lookup"><span data-stu-id="47e17-224">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="47e17-225">Standart ve Premium</span><span class="sxs-lookup"><span data-stu-id="47e17-225">Standard and Premium</span></span> |
| <span data-ttu-id="47e17-226">veritabanları</span><span class="sxs-lookup"><span data-stu-id="47e17-226">databases</span></span> |<span data-ttu-id="47e17-227">Veritabanı Hello sayısını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="47e17-227">Configures hello number of databases.</span></span> <span data-ttu-id="47e17-228">Bu özellik yalnızca önbellek oluşturma sırasında yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="47e17-228">This property can be configured only at cache creation.</span></span> |<span data-ttu-id="47e17-229">Standart ve Premium</span><span class="sxs-lookup"><span data-stu-id="47e17-229">Standard and Premium</span></span> |

## <a name="toocreate-a-redis-cache"></a><span data-ttu-id="47e17-230">toocreate bir Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="47e17-230">toocreate a Redis Cache</span></span>
<span data-ttu-id="47e17-231">Yeni Azure Redis önbelleği örnekleri hello kullanarak oluşturulur [yeni AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="47e17-231">New Azure Redis Cache instances are created using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47e17-232">Merhaba hello Azure portal kullanarak bir abonelikte Redis önbelleği oluşturma ilk kez hello portal hello kaydeder `Microsoft.Cache` Bu abonelik için ad alanı.</span><span class="sxs-lookup"><span data-stu-id="47e17-232">hello first time you create a Redis cache in a subscription using hello Azure portal, hello portal registers hello `Microsoft.Cache` namespace for that subscription.</span></span> <span data-ttu-id="47e17-233">Dener toocreate hello ilk Redis önbelleği PowerShell kullanarak bir abonelikte, komutu aşağıdaki hello kullanarak bu ad önce kaydetmeniz gerekir; Aksi takdirde cmdlet'leri gibi `New-AzureRmRedisCache` ve `Get-AzureRmRedisCache` başarısız.</span><span class="sxs-lookup"><span data-stu-id="47e17-233">If you attempt toocreate hello first Redis cache in a subscription using PowerShell, you must first register that namespace using hello following command; otherwise cmdlets such as `New-AzureRmRedisCache` and `Get-AzureRmRedisCache` fail.</span></span>
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

<span data-ttu-id="47e17-234">toosee listesini kullanılabilir parametreleri ve açıklamaları için `New-AzureRmRedisCache`çalıştırın hello aşağıdaki komutu.</span><span class="sxs-lookup"><span data-stu-id="47e17-234">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCache -detailed

    NAME
        New-AzureRmRedisCache

    SYNOPSIS
        Creates a new redis cache.


    SYNTAX
        New-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Location <String> [-RedisVersion <String>]
        [-Size <String>] [-Sku <String>] [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort
        <Boolean>] [-ShardCount <Integer>] [-VirtualNetwork <String>] [-Subnet <String>] [-StaticIP <String>]
        [<CommonParameters>]


    DESCRIPTION
        hello New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of hello redis cache toocreate.

        -ResourceGroupName <String>
            Name of resource group in which toocreate hello redis cache.

        -Location <String>
            Location in which toocreate hello redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, hello default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        -VirtualNetwork <String>
            hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="47e17-235">toocreate bir önbellek varsayılan parametrelerle hello aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="47e17-235">toocreate a cache with default parameters, run hello following command.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

<span data-ttu-id="47e17-236">`ResourceGroupName`, `Name`, ve `Location` Gerekli Parametreler, ancak hello rest isteğe bağlıdır ve varsayılan değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="47e17-236">`ResourceGroupName`, `Name`, and `Location` are required parameters, but hello rest are optional and have default values.</span></span> <span data-ttu-id="47e17-237">Merhaba önceki komutunu çalıştırarak hello belirtilen adını, konumunu ve devre dışı hello SSL olmayan bağlantı noktası ile boyutu 1 GB olan kaynak grubu ile bir standart SKU Azure Redis önbelleği örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="47e17-237">Running hello previous command creates a Standard SKU Azure Redis Cache instance with hello specified name, location, and resource group, that is 1 GB in size with hello non-SSL port disabled.</span></span>

<span data-ttu-id="47e17-238">toocreate premium önbelleği P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), dosya boyutu belirtin P3 (26 GB - 260 GB), ya da P4 (53 GB'a - 530 GB).</span><span class="sxs-lookup"><span data-stu-id="47e17-238">toocreate a premium cache, specify a size of P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), or P4 (53 GB - 530 GB).</span></span> <span data-ttu-id="47e17-239">kümeleme, tooenable belirtin hello kullanarak bir parça sayısı `ShardCount` parametresi.</span><span class="sxs-lookup"><span data-stu-id="47e17-239">tooenable clustering, specify a shard count using hello `ShardCount` parameter.</span></span> <span data-ttu-id="47e17-240">Merhaba aşağıdaki örnek P1 premium önbelleği ile 3 parça oluşturur.</span><span class="sxs-lookup"><span data-stu-id="47e17-240">hello following example creates a P1 premium cache with 3 shards.</span></span> <span data-ttu-id="47e17-241">P1 premium önbelleği 6 GB boyutunda ve üç parça toplam boyutu hello belirtilen beri 18 GB (3 x 6 GB).</span><span class="sxs-lookup"><span data-stu-id="47e17-241">A P1 premium cache is 6 GB in size, and since we specified three shards hello total size is 18 GB (3 x 6 GB).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

<span data-ttu-id="47e17-242">Merhaba toospecify değerlerini `RedisConfiguration` parametresi hello değerlerini içine alın `{}` anahtar/değer çiftleri ister `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span><span class="sxs-lookup"><span data-stu-id="47e17-242">toospecify values for hello `RedisConfiguration` parameter, enclose hello values inside `{}` as key/value pairs like `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span></span> <span data-ttu-id="47e17-243">Merhaba aşağıdaki örnekte bir standart 1 GB önbellek ile oluşturur `allkeys-random` ile yapılandırılmış maxmemory İlkesi ve keyspace bildirimleri `KEA`.</span><span class="sxs-lookup"><span data-stu-id="47e17-243">hello following example creates a standard 1 GB cache with `allkeys-random` maxmemory policy and keyspace notifications configured with `KEA`.</span></span> <span data-ttu-id="47e17-244">Daha fazla bilgi için bkz: [Keyspace bildirimleri (Gelişmiş ayarları)](cache-configure.md#keyspace-notifications-advanced-settings) ve [bellek ilkeleri](cache-configure.md#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="47e17-244">For more information, see [Keyspace notifications (advanced settings)](cache-configure.md#keyspace-notifications-advanced-settings) and [Memory policies](cache-configure.md#memory-policies).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="tooconfigure-hello-databases-setting-during-cache-creation"></a><span data-ttu-id="47e17-245">önbelleği oluşturma sırasında ayarı tooconfigure hello veritabanları</span><span class="sxs-lookup"><span data-stu-id="47e17-245">tooconfigure hello databases setting during cache creation</span></span>
<span data-ttu-id="47e17-246">Merhaba `databases` ayarı yalnızca önbellek oluşturma sırasında yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="47e17-246">hello `databases` setting can be configured only during cache creation.</span></span> <span data-ttu-id="47e17-247">Merhaba aşağıdaki örnekte oluşturur premium P3 (26 GB) önbellek hello kullanarak 48 veritabanlarıyla [yeni AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="47e17-247">hello following example creates a premium P3 (26 GB) cache with 48 databases using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

<span data-ttu-id="47e17-248">Merhaba hakkında daha fazla bilgi için `databases` özelliği, bkz: [Azure Redis önbelleği varsayılan sunucu yapılandırma](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="47e17-248">For more information on hello `databases` property, see [Default Azure Redis Cache server configuration](cache-configure.md#default-redis-server-configuration).</span></span> <span data-ttu-id="47e17-249">Hello kullanarak önbellek oluşturma hakkında daha fazla bilgi için [yeni AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet'in önceki hello bkz [toocreate bir Redis önbelleği](#to-create-a-redis-cache) bölümü.</span><span class="sxs-lookup"><span data-stu-id="47e17-249">For more information on creating a cache using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, see hello previous [toocreate a Redis Cache](#to-create-a-redis-cache) section.</span></span>

## <a name="tooupdate-a-redis-cache"></a><span data-ttu-id="47e17-250">tooupdate Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="47e17-250">tooupdate a Redis cache</span></span>
<span data-ttu-id="47e17-251">Azure Redis önbelleği örnekleri hello kullanarak güncel [kümesi AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="47e17-251">Azure Redis Cache instances are updated using hello [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span></span>

<span data-ttu-id="47e17-252">toosee listesini kullanılabilir parametreleri ve açıklamaları için `Set-AzureRmRedisCache`çalıştırın hello aşağıdaki komutu.</span><span class="sxs-lookup"><span data-stu-id="47e17-252">toosee a list of available parameters and their descriptions for `Set-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Set-AzureRmRedisCache -detailed

    NAME
        Set-AzureRmRedisCache

    SYNOPSIS
        Set redis cache updatable parameters.

    SYNTAX
        Set-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Size <String>] [-Sku <String>]
        [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort <Boolean>] [-ShardCount
        <Integer>] [<CommonParameters>]

    DESCRIPTION
        hello Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooupdate.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. hello default value is null and no change will be made toothe
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="47e17-253">Merhaba `Set-AzureRmRedisCache` cmdlet gibi kullanılan tooupdate özellikler olabilir `Size`, `Sku`, `EnableNonSslPort`ve hello `RedisConfiguration` değerleri.</span><span class="sxs-lookup"><span data-stu-id="47e17-253">hello `Set-AzureRmRedisCache` cmdlet can be used tooupdate properties such as `Size`, `Sku`, `EnableNonSslPort`, and hello `RedisConfiguration` values.</span></span> 

<span data-ttu-id="47e17-254">Merhaba hello Redis önbelleği için maxmemory İlkesi güncelleştirmeleri hello aşağıdaki komutu myCache adlı.</span><span class="sxs-lookup"><span data-stu-id="47e17-254">hello following command updates hello maxmemory-policy for hello Redis Cache named myCache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="tooscale-a-redis-cache"></a><span data-ttu-id="47e17-255">tooscale Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="47e17-255">tooscale a Redis cache</span></span>
<span data-ttu-id="47e17-256">`Set-AzureRmRedisCache`bir Azure Redis önbelleği örneği hello zaman kullanılan tooscale olabilir `Size`, `Sku`, veya `ShardCount` özellikleri değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="47e17-256">`Set-AzureRmRedisCache` can be used tooscale an Azure Redis cache instance when hello `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> 

> [!NOTE]
> <span data-ttu-id="47e17-257">PowerShell kullanarak önbellek ölçeklendirme aynı sınırlar konu toohello olduğunu ve Azure portalında bir önbellekten ölçeklendirme olarak yönergeleri hello.</span><span class="sxs-lookup"><span data-stu-id="47e17-257">Scaling a cache using PowerShell is subject toohello same limits and guidelines as scaling a cache from hello Azure portal.</span></span> <span data-ttu-id="47e17-258">Tooa kısıtlamaları aşağıdaki hello ile fiyatlandırma katmanı farklı ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47e17-258">You can scale tooa different pricing tier with hello following restrictions.</span></span>
> 
> * <span data-ttu-id="47e17-259">Bir daha yüksek fiyatlandırma katmanı tooa fiyatlandırma katmanı alt ölçeklendirme olamaz.</span><span class="sxs-lookup"><span data-stu-id="47e17-259">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
> * <span data-ttu-id="47e17-260">Ölçeklendirme olamaz bir **Premium** tooa aşağı önbellek **standart** veya **temel** önbelleği.</span><span class="sxs-lookup"><span data-stu-id="47e17-260">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
> * <span data-ttu-id="47e17-261">Ölçeklendirme olamaz bir **standart** tooa aşağı önbellek **temel** önbelleği.</span><span class="sxs-lookup"><span data-stu-id="47e17-261">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
> * <span data-ttu-id="47e17-262">Ölçeklendirme yapılabilir bir **temel** tooa önbelleğe **standart** önbellek ancak hello hello boyutta değiştiremiyor aynı anda.</span><span class="sxs-lookup"><span data-stu-id="47e17-262">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="47e17-263">Farklı bir boyut gerekiyorsa, bir sonraki ölçeklendirme işlemi istenen toohello boyutu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47e17-263">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
> * <span data-ttu-id="47e17-264">Ölçeklendirme olamaz bir **temel** doğrudan tooa önbelleğe **Premium** önbelleği.</span><span class="sxs-lookup"><span data-stu-id="47e17-264">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="47e17-265">Ölçeklendirme gerekir **temel** çok**standart** bir ölçeklendirme işlemi ve ardından gelen **standart** çok**Premium** , sonraki ölçeklendirme işlem.</span><span class="sxs-lookup"><span data-stu-id="47e17-265">You must scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
> * <span data-ttu-id="47e17-266">Büyük bir değerden toohello aşağı ölçeklendirme olamaz **C0 (250 MB)** boyutu.</span><span class="sxs-lookup"><span data-stu-id="47e17-266">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>
> 
> <span data-ttu-id="47e17-267">Daha fazla bilgi için bkz: [nasıl tooScale Azure Redis önbelleği](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="47e17-267">For more information, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>
> 
> 

<span data-ttu-id="47e17-268">Merhaba aşağıdaki örnekte nasıl tooscale bir önbellek adlı gösterir `myCache` tooa 2,5 GB önbellek.</span><span class="sxs-lookup"><span data-stu-id="47e17-268">hello following example shows how tooscale a cache named `myCache` tooa 2.5 GB cache.</span></span> <span data-ttu-id="47e17-269">Bu komut bir temel veya standart bir önbellek için çalıştığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="47e17-269">Note that this command works for both a Basic or a Standard cache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="47e17-270">Bu komutu verildikten sonra hello önbellek hello durumu döndürülür (benzer toocalling `Get-AzureRmRedisCache`).</span><span class="sxs-lookup"><span data-stu-id="47e17-270">After this command is issued, hello status of hello cache is returned (similar toocalling `Get-AzureRmRedisCache`).</span></span> <span data-ttu-id="47e17-271">Bu hello Not `ProvisioningState` olan `Scaling`.</span><span class="sxs-lookup"><span data-stu-id="47e17-271">Note that hello `ProvisioningState` is `Scaling`.</span></span>

    PS C:\> Set-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup -Size 2.5GB


    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/mygroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Scaling
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 150], [notify-keyspace-events, KEA],
                         [maxmemory-delta, 150]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : mygroup
    PrimaryKey         : ....
    SecondaryKey       : ....
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

<span data-ttu-id="47e17-272">Merhaba ölçeklendirme işlemi tamamlandıktan sonra hello `ProvisioningState` çok değişiklikleri`Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="47e17-272">When hello scaling operation is complete, hello `ProvisioningState` changes too`Succeeded`.</span></span> <span data-ttu-id="47e17-273">Toomake temel tooStandard değiştirme ve ardından hello boyutunu değiştirme gibi sonraki bir ölçeklendirme işlemi gerekiyorsa hello önceki işlem tamamlanana veya bir hata benzer toohello aşağıdaki aldığınız kadar beklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="47e17-273">If you need toomake a subsequent scaling operation, such as changing from Basic tooStandard and then changing hello size, you must wait until hello previous operation is complete or you receive an error similar toohello following.</span></span>

    Set-AzureRmRedisCache : Conflict: hello resource '...' is not in a stable state, and is currently unable tooaccept hello update request.

## <a name="tooget-information-about-a-redis-cache"></a><span data-ttu-id="47e17-274">Redis önbelleği hakkında tooget bilgi</span><span class="sxs-lookup"><span data-stu-id="47e17-274">tooget information about a Redis cache</span></span>
<span data-ttu-id="47e17-275">Hello kullanarak önbellek hakkında bilgi alabilir [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="47e17-275">You can retrieve information about a cache using hello [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span></span>

<span data-ttu-id="47e17-276">toosee listesini kullanılabilir parametreleri ve açıklamaları için `Get-AzureRmRedisCache`çalıştırın hello aşağıdaki komutu.</span><span class="sxs-lookup"><span data-stu-id="47e17-276">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in hello specified resource group or all caches in hello current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCache cmdlet gets hello details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in hello specified resource group.

        If no parameters are given than it will return details about all caches hello current subscription.

    PARAMETERS
        -Name <String>
            hello name of hello cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns hello details for hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns hello details of hello cache specified by Name. If only hello ResourceGroup
            parameter is provided, then details for all caches in hello resource group are returned.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="47e17-277">Merhaba geçerli Abonelikteki tüm önbellekleri tooreturn bilgilerini çalıştırmak `Get-AzureRmRedisCache` hiçbir parametre olmadan.</span><span class="sxs-lookup"><span data-stu-id="47e17-277">tooreturn information about all caches in hello current subscription, run `Get-AzureRmRedisCache` without any parameters.</span></span>

    Get-AzureRmRedisCache

<span data-ttu-id="47e17-278">belirli bir kaynak grubundaki tüm önbellekleri tooreturn bilgilerini çalıştırmak `Get-AzureRmRedisCache` hello ile `ResourceGroupName` parametresi.</span><span class="sxs-lookup"><span data-stu-id="47e17-278">tooreturn information about all caches in a specific resource group, run `Get-AzureRmRedisCache` with hello `ResourceGroupName` parameter.</span></span>

    Get-AzureRmRedisCache -ResourceGroupName myGroup

<span data-ttu-id="47e17-279">belirli bir önbelleği hakkında tooreturn bilgi çalıştırmak `Get-AzureRmRedisCache` hello ile `Name` hello önbellek ve hello hello adını içeren parametre `ResourceGroupName` hello kaynak grubu, önbellek içeren parametresiyle.</span><span class="sxs-lookup"><span data-stu-id="47e17-279">tooreturn information about a specific cache, run `Get-AzureRmRedisCache` with hello `Name` parameter containing hello name of hello cache, and hello `ResourceGroupName` parameter with hello resource group containing that cache.</span></span>

    PS C:\> Get-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/myGroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Succeeded
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 62], [notify-keyspace-events, KEA],
                         [maxclients, 1000]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : myGroup
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

## <a name="tooretrieve-hello-access-keys-for-a-redis-cache"></a><span data-ttu-id="47e17-280">Redis önbelleği tooretrieve hello erişim tuşları</span><span class="sxs-lookup"><span data-stu-id="47e17-280">tooretrieve hello access keys for a Redis cache</span></span>
<span data-ttu-id="47e17-281">tooretrieve hello erişim tuşları önbelleğiniz için kullanabileceğiniz hello [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="47e17-281">tooretrieve hello access keys for your cache, you can use hello [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span></span>

<span data-ttu-id="47e17-282">toosee listesini kullanılabilir parametreleri ve açıklamaları için `Get-AzureRmRedisCacheKey`çalıştırın hello aşağıdaki komutu.</span><span class="sxs-lookup"><span data-stu-id="47e17-282">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets hello accesskeys for hello specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCacheKey cmdlet gets hello access keys for hello specified cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="47e17-283">tooretrieve hello anahtarları önbelleğiniz için arama hello `Get-AzureRmRedisCacheKey` cmdlet'i ve önbelleğiniz hello adını geçişinde hello hello önbellek içeren hello kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="47e17-283">tooretrieve hello keys for your cache, call hello `Get-AzureRmRedisCacheKey` cmdlet and pass in hello name of your cache hello name of hello resource group that contains hello cache.</span></span>

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="tooregenerate-access-keys-for-your-redis-cache"></a><span data-ttu-id="47e17-284">Redis önbelleği için tooregenerate erişim tuşları</span><span class="sxs-lookup"><span data-stu-id="47e17-284">tooregenerate access keys for your Redis cache</span></span>
<span data-ttu-id="47e17-285">tooregenerate hello erişim tuşları önbelleğiniz için kullanabileceğiniz hello [yeni AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="47e17-285">tooregenerate hello access keys for your cache, you can use hello [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span></span>

<span data-ttu-id="47e17-286">toosee listesini kullanılabilir parametreleri ve açıklamaları için `New-AzureRmRedisCacheKey`çalıştırın hello aşağıdaki komutu.</span><span class="sxs-lookup"><span data-stu-id="47e17-286">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates hello access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        hello New-AzureRmRedisCacheKey cmdlet regenerate hello access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -KeyType <String>
            Specifies whether tooregenerate hello primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When hello Force parameter is provided, hello specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="47e17-287">Çağrı hello önbelleğiniz için tooregenerate hello birincil veya ikincil anahtarı `New-AzureRmRedisCacheKey` cmdlet hello geçişinde adı, kaynak grubu ve belirtin `Primary` veya `Secondary` hello için `KeyType` parametresi.</span><span class="sxs-lookup"><span data-stu-id="47e17-287">tooregenerate hello primary or secondary key for your cache, call hello `New-AzureRmRedisCacheKey` cmdlet and pass in hello name, resource group, and specify either `Primary` or `Secondary` for hello `KeyType` parameter.</span></span> <span data-ttu-id="47e17-288">Aşağıdaki örneğine hello, önbellek için hello ikincil erişim anahtarını yeniden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="47e17-288">In hello following example, hello secondary access key for a cache is regenerated.</span></span>

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want tooregenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="toodelete-a-redis-cache"></a><span data-ttu-id="47e17-289">toodelete Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="47e17-289">toodelete a Redis cache</span></span>
<span data-ttu-id="47e17-290">toodelete bir Redis önbelleği kullanma hello [Kaldır AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="47e17-290">toodelete a Redis cache, use hello [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span></span>

<span data-ttu-id="47e17-291">toosee listesini kullanılabilir parametreleri ve açıklamaları için `Remove-AzureRmRedisCache`çalıştırın hello aşağıdaki komutu.</span><span class="sxs-lookup"><span data-stu-id="47e17-291">toosee a list of available parameters and their descriptions for `Remove-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        hello Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooremove.

        -ResourceGroupName <String>
            Name of hello resource group of hello cache tooremove.

        -Force
            When hello Force parameter is provided, hello cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes hello cache and does not return any value. If hello PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating hello success of hello operatio

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="47e17-292">Adlandırılmış önbellek örneği aşağıdaki hello hello `myCache` kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="47e17-292">In hello following example, hello cache named `myCache` is removed.</span></span>

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want tooremove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="tooimport-a-redis-cache"></a><span data-ttu-id="47e17-293">tooimport Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="47e17-293">tooimport a Redis cache</span></span>
<span data-ttu-id="47e17-294">Hello kullanarak bir Azure Redis önbelleği örneğine verileri içeri aktarabilirsiniz `Import-AzureRmRedisCache` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="47e17-294">You can import data into an Azure Redis Cache instance using hello `Import-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47e17-295">İçeri/dışarı aktarma için kullanılabilir yalnızca [premium katmanı](cache-premium-tier-intro.md) önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="47e17-295">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="47e17-296">İçeri/dışarı aktarma hakkında daha fazla bilgi için bkz: [içeri ve dışarı aktarma Azure Redis önbelleği verilerde](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="47e17-296">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="47e17-297">toosee listesini kullanılabilir parametreleri ve açıklamaları için `Import-AzureRmRedisCache`çalıştırın hello aşağıdaki komutu.</span><span class="sxs-lookup"><span data-stu-id="47e17-297">toosee a list of available parameters and their descriptions for `Import-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs tooAzure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Import-AzureRmRedisCache cmdlet imports data from hello specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into hello cache.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -Force
            When hello Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If hello PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating hello success of the
            operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="47e17-298">Merhaba aşağıdaki komutu verileri Azure Redis önbelleğine hello SAS URI tarafından belirtilen hello blob alır.</span><span class="sxs-lookup"><span data-stu-id="47e17-298">hello following command imports data from hello blob specified by hello SAS uri into Azure Redis Cache.</span></span>

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="tooexport-a-redis-cache"></a><span data-ttu-id="47e17-299">tooexport Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="47e17-299">tooexport a Redis cache</span></span>
<span data-ttu-id="47e17-300">Hello kullanarak bir Azure Redis önbelleği örnekten verileri dışarı aktarabilirsiniz `Export-AzureRmRedisCache` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="47e17-300">You can export data from an Azure Redis Cache instance using hello `Export-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47e17-301">İçeri/dışarı aktarma için kullanılabilir yalnızca [premium katmanı](cache-premium-tier-intro.md) önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="47e17-301">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="47e17-302">İçeri/dışarı aktarma hakkında daha fazla bilgi için bkz: [içeri ve dışarı aktarma Azure Redis önbelleği verilerde](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="47e17-302">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="47e17-303">toosee listesini kullanılabilir parametreleri ve açıklamaları için `Export-AzureRmRedisCache`çalıştırın hello aşağıdaki komutu.</span><span class="sxs-lookup"><span data-stu-id="47e17-303">toosee a list of available parameters and their descriptions for `Export-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache tooa specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache tooa specified container.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Prefix <String>
            Prefix toouse for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="47e17-304">Merhaba aşağıdaki komutu veri hello SAS URI tarafından belirtilen hello kapsayıcısı uygulamasına Azure Redis önbelleği örneğinden dışa aktarır.</span><span class="sxs-lookup"><span data-stu-id="47e17-304">hello following command exports data from an Azure Redis Cache instance into hello container specified by hello SAS uri.</span></span>

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="tooreboot-a-redis-cache"></a><span data-ttu-id="47e17-305">tooreboot Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="47e17-305">tooreboot a Redis cache</span></span>
<span data-ttu-id="47e17-306">Azure Redis önbelleği örneğinizi hello kullanarak yeniden `Reset-AzureRmRedisCache` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="47e17-306">You can reboot your Azure Redis Cache instance using hello `Reset-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47e17-307">Yeniden başlatma için kullanılabilir yalnızca [premium katmanı](cache-premium-tier-intro.md) önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="47e17-307">Reboot is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="47e17-308">Önbelleğinizi yeniden başlatma hakkında daha fazla bilgi için bkz: [önbelleğe yönetim - yeniden başlatma](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="47e17-308">For more information about rebooting your cache, see [Cache administration - reboot](cache-administration.md#reboot).</span></span>
> 
> 

<span data-ttu-id="47e17-309">toosee listesini kullanılabilir parametreleri ve açıklamaları için `Reset-AzureRmRedisCache`çalıştırın hello aşağıdaki komutu.</span><span class="sxs-lookup"><span data-stu-id="47e17-309">toosee a list of available parameters and their descriptions for `Reset-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Reset-AzureRmRedisCache cmdlet reboots hello specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -RebootType <String>
            Which node tooreboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard tooreboot when rebooting a premium cache with clustering enabled.

        -Force
            When hello Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="47e17-310">Merhaba aşağıdaki komutu yeniden belirtilen Merhaba, her iki düğüm önbelleği.</span><span class="sxs-lookup"><span data-stu-id="47e17-310">hello following command reboots both nodes of hello specified cache.</span></span>

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a><span data-ttu-id="47e17-311">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="47e17-311">Next steps</span></span>
<span data-ttu-id="47e17-312">Azure ile Windows PowerShell'i kullanma hakkında daha fazla toolearn kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="47e17-312">toolearn more about using Windows PowerShell with Azure, see hello following resources:</span></span>

* [<span data-ttu-id="47e17-313">MSDN'deki Azure Redis önbelleği cmdlet belgeleri</span><span class="sxs-lookup"><span data-stu-id="47e17-313">Azure Redis Cache cmdlet documentation on MSDN</span></span>](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* <span data-ttu-id="47e17-314">[Azure Resource Manager cmdlet'lerini](http://go.microsoft.com/fwlink/?LinkID=394765): hello Azure Resource Manager modülünde toouse hello cmdlet'leri hakkında bilgi edinme.</span><span class="sxs-lookup"><span data-stu-id="47e17-314">[Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): Learn toouse hello cmdlets in hello Azure Resource Manager module.</span></span>
* <span data-ttu-id="47e17-315">[Azure kaynaklarınızı grupları toomanage kaynağı kullanan](../azure-resource-manager/resource-group-template-deploy-portal.md): öğrenin nasıl toocreate ve hello Azure portalında bulunan kaynak gruplarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="47e17-315">[Using Resource groups toomanage your Azure resources](../azure-resource-manager/resource-group-template-deploy-portal.md): Learn how toocreate and manage resource groups in hello Azure portal.</span></span>
* <span data-ttu-id="47e17-316">[Azure blogu](http://blogs.msdn.com/windowsazure): Azure yeni özellikler hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="47e17-316">[Azure blog](http://blogs.msdn.com/windowsazure): Learn about new features in Azure.</span></span>
* <span data-ttu-id="47e17-317">[Windows PowerShell Web günlüğü](http://blogs.msdn.com/powershell): Windows PowerShell'de yeni özellikler hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="47e17-317">[Windows PowerShell blog](http://blogs.msdn.com/powershell): Learn about new features in Windows PowerShell.</span></span>
* <span data-ttu-id="47e17-318">["Hey, betik yazarı!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Windows PowerShell topluluk hello gerçek ipuçları ve püf noktaları alın.</span><span class="sxs-lookup"><span data-stu-id="47e17-318">["Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Get real-world tips and tricks from hello Windows PowerShell community.</span></span>

