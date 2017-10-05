---
title: "Azure PowerShell ile Azure Redis önbelleğini yönetme | Microsoft Docs"
description: "Azure Redis önbelleği Azure PowerShell kullanarak için yönetim görevlerini gerçekleştirmek öğrenin."
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
ms.openlocfilehash: 0a5c95eab3fd01f611fc049e80c5c506857e0b81
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a><span data-ttu-id="bebc9-103">Azure PowerShell ile Azure Redis önbelleği Yönet</span><span class="sxs-lookup"><span data-stu-id="bebc9-103">Manage Azure Redis Cache with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bebc9-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bebc9-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="bebc9-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bebc9-105">Azure CLI</span></span>](cache-manage-cli.md)
> 
> 

<span data-ttu-id="bebc9-106">Bu konu, oluşturma gibi genel görevleri gerçekleştirmek için nasıl güncelleştirmek ve Azure Redis önbelleği örnekleri, erişim anahtarlarını yeniden nasıl ve önbellekleri hakkındaki bilgileri görüntülemek nasıl ölçeği gösterir.</span><span class="sxs-lookup"><span data-stu-id="bebc9-106">This topic shows you how to perform common tasks such as create, update, and scale your Azure Redis Cache instances, how to regenerate access keys, and how to view information about your caches.</span></span> <span data-ttu-id="bebc9-107">Azure Redis önbelleği PowerShell cmdlet'lerinin tam listesi için bkz: [Azure Redis önbelleği cmdlet'leri](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span><span class="sxs-lookup"><span data-stu-id="bebc9-107">For a complete list of Azure Redis Cache PowerShell cmdlets, see [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="bebc9-108">Klasik dağıtım modeli hakkında daha fazla bilgi için bkz: [Azure Resource Manager ve klasik dağıtım: dağıtım modelleri ve kaynaklarınızın durumunu anlamak](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span><span class="sxs-lookup"><span data-stu-id="bebc9-108">For more information about the classic deployment model, see [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bebc9-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bebc9-109">Prerequisites</span></span>
<span data-ttu-id="bebc9-110">Azure PowerShell'i zaten yüklediyseniz, Azure PowerShell sürümü 1.0.0 olmalıdır veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="bebc9-110">If you have already installed Azure PowerShell, you must have Azure PowerShell version 1.0.0 or later.</span></span> <span data-ttu-id="bebc9-111">Azure PowerShell komut isteminde bu komutla yüklediğiniz Azure PowerShell sürümü kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bebc9-111">You can check the version of Azure PowerShell that you have installed with this command at the Azure PowerShell command prompt.</span></span>

    Get-Module azure | format-table version


<span data-ttu-id="bebc9-112">İlk olarak, Azure için bu komutla oturum gerekir.</span><span class="sxs-lookup"><span data-stu-id="bebc9-112">First, you must log in to Azure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="bebc9-113">Oturum açma iletişim kutusunda Microsoft Azure e-posta adresi, Azure hesabınızı ve parolasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="bebc9-113">Specify the email address of your Azure account and its password in the Microsoft Azure sign-in dialog.</span></span>

<span data-ttu-id="bebc9-114">Ardından, birden çok Azure aboneliğiniz varsa Azure aboneliğinizi ayarlamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="bebc9-114">Next, if you have multiple Azure subscriptions, you need to set your Azure subscription.</span></span> <span data-ttu-id="bebc9-115">Geçerli Aboneliklerin listesini görmek için bu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-115">To see a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="bebc9-116">Aboneliği belirtmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-116">To specify the subscription, run the following command.</span></span> <span data-ttu-id="bebc9-117">Aşağıdaki örnekte, abonelik addır `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="bebc9-117">In the following example, the subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

<span data-ttu-id="bebc9-118">Azure Resource Manager ile Windows PowerShell kullanmadan önce aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="bebc9-118">Before you can use Windows PowerShell with Azure Resource Manager, you need the following:</span></span>

* <span data-ttu-id="bebc9-119">Windows PowerShell sürüm 3.0 veya 4.0.</span><span class="sxs-lookup"><span data-stu-id="bebc9-119">Windows PowerShell, Version 3.0 or 4.0.</span></span> <span data-ttu-id="bebc9-120">Windows PowerShell sürümü bulmak için şunu yazın:`$PSVersionTable` ve değerini doğrulayın `PSVersion` 3.0 veya 4.0.</span><span class="sxs-lookup"><span data-stu-id="bebc9-120">To find the version of Windows PowerShell, type:`$PSVersionTable` and verify the value of `PSVersion` is 3.0 or 4.0.</span></span> <span data-ttu-id="bebc9-121">Uyumlu bir sürümünü yüklemek için bkz: [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) veya [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="bebc9-121">To install a compatible version, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

<span data-ttu-id="bebc9-122">Bu öğreticide gördüğünüz herhangi bir cmdlet'in ayrıntılı yardım almak için Get-Help cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-122">To get detailed help for any cmdlet you see in this tutorial, use the Get-Help cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="bebc9-123">Örneğin, Yardım almak için `New-AzureRmRedisCache` cmdlet, türü:</span><span class="sxs-lookup"><span data-stu-id="bebc9-123">For example, to get help for the `New-AzureRmRedisCache` cmdlet, type:</span></span>

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-to-connect-to-other-clouds"></a><span data-ttu-id="bebc9-124">Diğer bulutlara bağlanma</span><span class="sxs-lookup"><span data-stu-id="bebc9-124">How to connect to other clouds</span></span>
<span data-ttu-id="bebc9-125">Varsayılan olarak Azure ortamıdır `AzureCloud`, genel Azure bulut örneği temsil eder.</span><span class="sxs-lookup"><span data-stu-id="bebc9-125">By default the Azure environment is `AzureCloud`, which represents the global Azure cloud instance.</span></span> <span data-ttu-id="bebc9-126">Farklı bir örneğine bağlanmak için `Add-AzureRmAccount` komutunu `-Environment` veya -`EnvironmentName` komut satırı anahtarıyla istenen ortama veya ortam adı.</span><span class="sxs-lookup"><span data-stu-id="bebc9-126">To connect to a different instance, use the `Add-AzureRmAccount` command with the `-Environment` or -`EnvironmentName` command line switch with the desired environment or environment name.</span></span>

<span data-ttu-id="bebc9-127">Kullanılabilir ortamlar listesini görmek için Çalıştır `Get-AzureRmEnvironment` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bebc9-127">To see the list of available environments, run the `Get-AzureRmEnvironment` cmdlet.</span></span>

### <a name="to-connect-to-the-azure-government-cloud"></a><span data-ttu-id="bebc9-128">Azure Bulutu bağlanmak için</span><span class="sxs-lookup"><span data-stu-id="bebc9-128">To connect to the Azure Government Cloud</span></span>
<span data-ttu-id="bebc9-129">Azure Bulutu bağlanmak için aşağıdaki komutlardan birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-129">To connect to the Azure Government Cloud, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

<span data-ttu-id="bebc9-130">or</span><span class="sxs-lookup"><span data-stu-id="bebc9-130">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

<span data-ttu-id="bebc9-131">Azure Bulutu önbellek oluşturmak için aşağıdaki konumlardan birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-131">To create a cache in the Azure Government Cloud, use one of the following locations.</span></span>

* <span data-ttu-id="bebc9-132">ABD hükümeti Virginia</span><span class="sxs-lookup"><span data-stu-id="bebc9-132">USGov Virginia</span></span>
* <span data-ttu-id="bebc9-133">ABD hükümeti Iowa</span><span class="sxs-lookup"><span data-stu-id="bebc9-133">USGov Iowa</span></span>

<span data-ttu-id="bebc9-134">Azure Bulutu hakkında daha fazla bilgi için bkz: [Microsoft Azure kamu](https://azure.microsoft.com/features/gov/) ve [Microsoft Azure kamu Geliştirici Kılavuzu](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="bebc9-134">For more information about the Azure Government Cloud, see [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) and [Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>

### <a name="to-connect-to-the-azure-china-cloud"></a><span data-ttu-id="bebc9-135">Azure Çin buluta bağlamak için</span><span class="sxs-lookup"><span data-stu-id="bebc9-135">To connect to the Azure China Cloud</span></span>
<span data-ttu-id="bebc9-136">Azure Çin buluta bağlanmak için aşağıdaki komutlardan birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-136">To connect to the Azure China Cloud, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

<span data-ttu-id="bebc9-137">or</span><span class="sxs-lookup"><span data-stu-id="bebc9-137">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

<span data-ttu-id="bebc9-138">Önbellek Azure Çin bulut oluşturmak için aşağıdaki konumlardan birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-138">To create a cache in the Azure China Cloud, use one of the following locations.</span></span>

* <span data-ttu-id="bebc9-139">Çin Doğu</span><span class="sxs-lookup"><span data-stu-id="bebc9-139">China East</span></span>
* <span data-ttu-id="bebc9-140">Çin Kuzey</span><span class="sxs-lookup"><span data-stu-id="bebc9-140">China North</span></span>

<span data-ttu-id="bebc9-141">Azure Çin bulut hakkında daha fazla bilgi için bkz: [AzureChinaCloud Azure Çin'de 21Vianet tarafından işletilen](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="bebc9-141">For more information about the Azure China Cloud, see [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span>

### <a name="to-connect-to-microsoft-azure-germany"></a><span data-ttu-id="bebc9-142">Microsoft Azure Almanya bağlanmak için</span><span class="sxs-lookup"><span data-stu-id="bebc9-142">To connect to Microsoft Azure Germany</span></span>
<span data-ttu-id="bebc9-143">Microsoft Azure Almanya bağlanmak için aşağıdaki komutlardan birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-143">To connect to Microsoft Azure Germany, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


<span data-ttu-id="bebc9-144">or</span><span class="sxs-lookup"><span data-stu-id="bebc9-144">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

<span data-ttu-id="bebc9-145">Microsoft Azure Almanya önbellek oluşturmak için aşağıdaki konumlardan birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-145">To create a cache in Microsoft Azure Germany, use one of the following locations.</span></span>

* <span data-ttu-id="bebc9-146">Almanya Orta</span><span class="sxs-lookup"><span data-stu-id="bebc9-146">Germany Central</span></span>
* <span data-ttu-id="bebc9-147">Almanya Kuzeydoğu</span><span class="sxs-lookup"><span data-stu-id="bebc9-147">Germany Northeast</span></span>

<span data-ttu-id="bebc9-148">Microsoft Azure Almanya hakkında daha fazla bilgi için bkz: [Microsoft Azure Almanya](https://azure.microsoft.com/overview/clouds/germany/).</span><span class="sxs-lookup"><span data-stu-id="bebc9-148">For more information about Microsoft Azure Germany, see [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).</span></span>

### <a name="properties-used-for-azure-redis-cache-powershell"></a><span data-ttu-id="bebc9-149">Azure Redis önbelleği PowerShell için kullanılan özellikleri</span><span class="sxs-lookup"><span data-stu-id="bebc9-149">Properties used for Azure Redis Cache PowerShell</span></span>
<span data-ttu-id="bebc9-150">Aşağıdaki tabloda, özellikleri ve açıklamaları oluştururken ve Azure PowerShell kullanarak Azure Redis önbelleği örneklerinizi yönetme yaygın olarak kullanılan parametreleri içerir.</span><span class="sxs-lookup"><span data-stu-id="bebc9-150">The following table contains properties and descriptions for commonly used parameters when creating and managing your Azure Redis Cache instances using Azure PowerShell.</span></span>

| <span data-ttu-id="bebc9-151">Parametre</span><span class="sxs-lookup"><span data-stu-id="bebc9-151">Parameter</span></span> | <span data-ttu-id="bebc9-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bebc9-152">Description</span></span> | <span data-ttu-id="bebc9-153">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="bebc9-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bebc9-154">Ad</span><span class="sxs-lookup"><span data-stu-id="bebc9-154">Name</span></span> |<span data-ttu-id="bebc9-155">Önbellek adı</span><span class="sxs-lookup"><span data-stu-id="bebc9-155">Name of the cache</span></span> | |
| <span data-ttu-id="bebc9-156">Konum</span><span class="sxs-lookup"><span data-stu-id="bebc9-156">Location</span></span> |<span data-ttu-id="bebc9-157">Önbellek konumu</span><span class="sxs-lookup"><span data-stu-id="bebc9-157">Location of the cache</span></span> | |
| <span data-ttu-id="bebc9-158">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="bebc9-158">ResourceGroupName</span></span> |<span data-ttu-id="bebc9-159">Kaynak grubu adı, önbellek oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="bebc9-159">Resource group name in which to create the cache</span></span> | |
| <span data-ttu-id="bebc9-160">Boyut</span><span class="sxs-lookup"><span data-stu-id="bebc9-160">Size</span></span> |<span data-ttu-id="bebc9-161">Önbellek boyutu.</span><span class="sxs-lookup"><span data-stu-id="bebc9-161">The size of the cache.</span></span> <span data-ttu-id="bebc9-162">Geçerli değerler: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5 GB, 6 GB, 13 GB, 26 GB, 53 GB'a</span><span class="sxs-lookup"><span data-stu-id="bebc9-162">Valid values are: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB</span></span> |<span data-ttu-id="bebc9-163">1 GB</span><span class="sxs-lookup"><span data-stu-id="bebc9-163">1GB</span></span> |
| <span data-ttu-id="bebc9-164">ShardCount</span><span class="sxs-lookup"><span data-stu-id="bebc9-164">ShardCount</span></span> |<span data-ttu-id="bebc9-165">Premium önbelleği kümeleme özelliği etkinleştirilmiş oluştururken oluşturmak için parça sayısı.</span><span class="sxs-lookup"><span data-stu-id="bebc9-165">The number of shards to create when creating a premium cache with clustering enabled.</span></span> <span data-ttu-id="bebc9-166">Geçerli değerler: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span><span class="sxs-lookup"><span data-stu-id="bebc9-166">Valid values are: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span></span> | |
| <span data-ttu-id="bebc9-167">SKU</span><span class="sxs-lookup"><span data-stu-id="bebc9-167">SKU</span></span> |<span data-ttu-id="bebc9-168">Önbellek SKU'su belirtir.</span><span class="sxs-lookup"><span data-stu-id="bebc9-168">Specifies the SKU of the cache.</span></span> <span data-ttu-id="bebc9-169">Geçerli değerler: temel, standart ve Premium</span><span class="sxs-lookup"><span data-stu-id="bebc9-169">Valid values are: Basic, Standard, Premium</span></span> |<span data-ttu-id="bebc9-170">Standart</span><span class="sxs-lookup"><span data-stu-id="bebc9-170">Standard</span></span> |
| <span data-ttu-id="bebc9-171">RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="bebc9-171">RedisConfiguration</span></span> |<span data-ttu-id="bebc9-172">Redis yapılandırma ayarlarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="bebc9-172">Specifies Redis configuration settings.</span></span> <span data-ttu-id="bebc9-173">Her ayarlama hakkında daha fazla bilgi için aşağıdakilere bakın [RedisConfiguration özellikleri](#redisconfiguration-properties) tablo.</span><span class="sxs-lookup"><span data-stu-id="bebc9-173">For details on each setting, see the following [RedisConfiguration properties](#redisconfiguration-properties) table.</span></span> | |
| <span data-ttu-id="bebc9-174">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="bebc9-174">EnableNonSslPort</span></span> |<span data-ttu-id="bebc9-175">SSL olmayan bağlantı noktası etkinleştirilip etkinleştirilmeyeceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="bebc9-175">Indicates whether the non-SSL port is enabled.</span></span> |<span data-ttu-id="bebc9-176">False</span><span class="sxs-lookup"><span data-stu-id="bebc9-176">False</span></span> |
| <span data-ttu-id="bebc9-177">MaxMemoryPolicy</span><span class="sxs-lookup"><span data-stu-id="bebc9-177">MaxMemoryPolicy</span></span> |<span data-ttu-id="bebc9-178">Bu parametre kullanım dışı - RedisConfiguration kullanın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-178">This parameter has been deprecated - use RedisConfiguration instead.</span></span> | |
| <span data-ttu-id="bebc9-179">StaticIP</span><span class="sxs-lookup"><span data-stu-id="bebc9-179">StaticIP</span></span> |<span data-ttu-id="bebc9-180">Önbelleğiniz bir VNET içindeki barındırma alt önbelleği için benzersiz bir IP adresi belirtir.</span><span class="sxs-lookup"><span data-stu-id="bebc9-180">When hosting your cache in a VNET, specifies a unique IP address in the subnet for the cache.</span></span> <span data-ttu-id="bebc9-181">Sağlanmazsa, bir sizin için alt ağ üzerinden seçilir.</span><span class="sxs-lookup"><span data-stu-id="bebc9-181">If not provided, one is chosen for you from the subnet.</span></span> | |
| <span data-ttu-id="bebc9-182">Alt ağ</span><span class="sxs-lookup"><span data-stu-id="bebc9-182">Subnet</span></span> |<span data-ttu-id="bebc9-183">Önbelleğinizi bir VNET içindeki barındırdığında, önbellek dağıtmak alt ağ adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="bebc9-183">When hosting your cache in a VNET, specifies the name of the subnet in which to deploy the cache.</span></span> | |
| <span data-ttu-id="bebc9-184">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="bebc9-184">VirtualNetwork</span></span> |<span data-ttu-id="bebc9-185">Önbelleğinizi bir VNET içindeki barındırdığında önbellek dağıtmak üzere VNET kaynak Kimliğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="bebc9-185">When hosting your cache in a VNET, specifies the resource ID of the VNET in which to deploy the cache.</span></span> | |
| <span data-ttu-id="bebc9-186">keyType</span><span class="sxs-lookup"><span data-stu-id="bebc9-186">KeyType</span></span> |<span data-ttu-id="bebc9-187">Erişim tuşları yenilenirken yeniden oluşturmak için hangi erişim anahtarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="bebc9-187">Specifies which access key to regenerate when renewing access keys.</span></span> <span data-ttu-id="bebc9-188">Geçerli değerler: birincil, ikincil</span><span class="sxs-lookup"><span data-stu-id="bebc9-188">Valid values are: Primary, Secondary</span></span> | |

### <a name="redisconfiguration-properties"></a><span data-ttu-id="bebc9-189">RedisConfiguration özellikleri</span><span class="sxs-lookup"><span data-stu-id="bebc9-189">RedisConfiguration properties</span></span>
| <span data-ttu-id="bebc9-190">Özellik</span><span class="sxs-lookup"><span data-stu-id="bebc9-190">Property</span></span> | <span data-ttu-id="bebc9-191">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bebc9-191">Description</span></span> | <span data-ttu-id="bebc9-192">Fiyatlandırma katmanları</span><span class="sxs-lookup"><span data-stu-id="bebc9-192">Pricing tiers</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bebc9-193">RDB yedekleme etkin</span><span class="sxs-lookup"><span data-stu-id="bebc9-193">rdb-backup-enabled</span></span> |<span data-ttu-id="bebc9-194">Olup olmadığını [Redis veri kalıcılığını](cache-how-to-premium-persistence.md) etkin</span><span class="sxs-lookup"><span data-stu-id="bebc9-194">Whether [Redis data persistence](cache-how-to-premium-persistence.md) is enabled</span></span> |<span data-ttu-id="bebc9-195">Yalnızca Premium</span><span class="sxs-lookup"><span data-stu-id="bebc9-195">Premium only</span></span> |
| <span data-ttu-id="bebc9-196">RDB depolama bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="bebc9-196">rdb-storage-connection-string</span></span> |<span data-ttu-id="bebc9-197">Depolama hesabı bağlantı dizesi [Redis veri kalıcılığını](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="bebc9-197">The connection string to the storage account for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="bebc9-198">Yalnızca Premium</span><span class="sxs-lookup"><span data-stu-id="bebc9-198">Premium only</span></span> |
| <span data-ttu-id="bebc9-199">RDB yedekleme sıklığı</span><span class="sxs-lookup"><span data-stu-id="bebc9-199">rdb-backup-frequency</span></span> |<span data-ttu-id="bebc9-200">Yedekleme sıklığı için [Redis veri kalıcılığını](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="bebc9-200">The backup frequency for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="bebc9-201">Yalnızca Premium</span><span class="sxs-lookup"><span data-stu-id="bebc9-201">Premium only</span></span> |
| <span data-ttu-id="bebc9-202">maxmemory-ayrılmış</span><span class="sxs-lookup"><span data-stu-id="bebc9-202">maxmemory-reserved</span></span> |<span data-ttu-id="bebc9-203">Yapılandırır [ayrılan bellek](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) önbellek olmayan işlemler için</span><span class="sxs-lookup"><span data-stu-id="bebc9-203">Configures the [memory reserved](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for non-cache processes</span></span> |<span data-ttu-id="bebc9-204">Standart ve Premium</span><span class="sxs-lookup"><span data-stu-id="bebc9-204">Standard and Premium</span></span> |
| <span data-ttu-id="bebc9-205">maxmemory İlkesi</span><span class="sxs-lookup"><span data-stu-id="bebc9-205">maxmemory-policy</span></span> |<span data-ttu-id="bebc9-206">Yapılandırır [çıkarma İlkesi](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) önbelleği</span><span class="sxs-lookup"><span data-stu-id="bebc9-206">Configures the [eviction policy](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for the cache</span></span> |<span data-ttu-id="bebc9-207">Tüm fiyatlandırma katmanlarına</span><span class="sxs-lookup"><span data-stu-id="bebc9-207">All pricing tiers</span></span> |
| <span data-ttu-id="bebc9-208">bildirim-keyspace-olayları</span><span class="sxs-lookup"><span data-stu-id="bebc9-208">notify-keyspace-events</span></span> |<span data-ttu-id="bebc9-209">Yapılandırır [keyspace bildirimleri](cache-configure.md#keyspace-notifications-advanced-settings)</span><span class="sxs-lookup"><span data-stu-id="bebc9-209">Configures [keyspace notifications](cache-configure.md#keyspace-notifications-advanced-settings)</span></span> |<span data-ttu-id="bebc9-210">Standart ve Premium</span><span class="sxs-lookup"><span data-stu-id="bebc9-210">Standard and Premium</span></span> |
| <span data-ttu-id="bebc9-211">max ziplist girişlerini karma</span><span class="sxs-lookup"><span data-stu-id="bebc9-211">hash-max-ziplist-entries</span></span> |<span data-ttu-id="bebc9-212">Yapılandırır [belleği en iyi duruma getirme](http://redis.io/topics/memory-optimization) küçük toplam veri türleri</span><span class="sxs-lookup"><span data-stu-id="bebc9-212">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="bebc9-213">Standart ve Premium</span><span class="sxs-lookup"><span data-stu-id="bebc9-213">Standard and Premium</span></span> |
| <span data-ttu-id="bebc9-214">karma-max-ziplist-değer</span><span class="sxs-lookup"><span data-stu-id="bebc9-214">hash-max-ziplist-value</span></span> |<span data-ttu-id="bebc9-215">Yapılandırır [belleği en iyi duruma getirme](http://redis.io/topics/memory-optimization) küçük toplam veri türleri</span><span class="sxs-lookup"><span data-stu-id="bebc9-215">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="bebc9-216">Standart ve Premium</span><span class="sxs-lookup"><span data-stu-id="bebc9-216">Standard and Premium</span></span> |
| <span data-ttu-id="bebc9-217">max intset girişlerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="bebc9-217">set-max-intset-entries</span></span> |<span data-ttu-id="bebc9-218">Yapılandırır [belleği en iyi duruma getirme](http://redis.io/topics/memory-optimization) küçük toplam veri türleri</span><span class="sxs-lookup"><span data-stu-id="bebc9-218">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="bebc9-219">Standart ve Premium</span><span class="sxs-lookup"><span data-stu-id="bebc9-219">Standard and Premium</span></span> |
| <span data-ttu-id="bebc9-220">max ziplist girişlerini zset</span><span class="sxs-lookup"><span data-stu-id="bebc9-220">zset-max-ziplist-entries</span></span> |<span data-ttu-id="bebc9-221">Yapılandırır [belleği en iyi duruma getirme](http://redis.io/topics/memory-optimization) küçük toplam veri türleri</span><span class="sxs-lookup"><span data-stu-id="bebc9-221">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="bebc9-222">Standart ve Premium</span><span class="sxs-lookup"><span data-stu-id="bebc9-222">Standard and Premium</span></span> |
| <span data-ttu-id="bebc9-223">max ziplist değeri zset</span><span class="sxs-lookup"><span data-stu-id="bebc9-223">zset-max-ziplist-value</span></span> |<span data-ttu-id="bebc9-224">Yapılandırır [belleği en iyi duruma getirme](http://redis.io/topics/memory-optimization) küçük toplam veri türleri</span><span class="sxs-lookup"><span data-stu-id="bebc9-224">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="bebc9-225">Standart ve Premium</span><span class="sxs-lookup"><span data-stu-id="bebc9-225">Standard and Premium</span></span> |
| <span data-ttu-id="bebc9-226">veritabanları</span><span class="sxs-lookup"><span data-stu-id="bebc9-226">databases</span></span> |<span data-ttu-id="bebc9-227">Veritabanı sayısı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="bebc9-227">Configures the number of databases.</span></span> <span data-ttu-id="bebc9-228">Bu özellik yalnızca önbellek oluşturma sırasında yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="bebc9-228">This property can be configured only at cache creation.</span></span> |<span data-ttu-id="bebc9-229">Standart ve Premium</span><span class="sxs-lookup"><span data-stu-id="bebc9-229">Standard and Premium</span></span> |

## <a name="to-create-a-redis-cache"></a><span data-ttu-id="bebc9-230">Redis önbelleği oluşturma</span><span class="sxs-lookup"><span data-stu-id="bebc9-230">To create a Redis Cache</span></span>
<span data-ttu-id="bebc9-231">Yeni Azure Redis önbelleği örnekleri kullanarak oluşturulur [yeni AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bebc9-231">New Azure Redis Cache instances are created using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bebc9-232">Azure portalını kullanarak bir abonelikte Redis önbelleği oluşturma ilk kez portal kaydeder `Microsoft.Cache` Bu abonelik için ad alanı.</span><span class="sxs-lookup"><span data-stu-id="bebc9-232">The first time you create a Redis cache in a subscription using the Azure portal, the portal registers the `Microsoft.Cache` namespace for that subscription.</span></span> <span data-ttu-id="bebc9-233">PowerShell kullanarak bir abonelikte ilk Redis önbelleği oluşturmayı denerseniz, aşağıdaki komutu kullanarak bu ad kaydetmeniz gerekir; Aksi takdirde cmdlet'leri gibi `New-AzureRmRedisCache` ve `Get-AzureRmRedisCache` başarısız.</span><span class="sxs-lookup"><span data-stu-id="bebc9-233">If you attempt to create the first Redis cache in a subscription using PowerShell, you must first register that namespace using the following command; otherwise cmdlets such as `New-AzureRmRedisCache` and `Get-AzureRmRedisCache` fail.</span></span>
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

<span data-ttu-id="bebc9-234">Kullanılabilir parametrelerin ve açıklamaları için listesini görmek için `New-AzureRmRedisCache`, aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-234">To see a list of available parameters and their descriptions for `New-AzureRmRedisCache`, run the following command.</span></span>

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
        The New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of the redis cache to create.

        -ResourceGroupName <String>
            Name of resource group in which to create the redis cache.

        -Location <String>
            Location in which to create the redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of the redis cache. The default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. The default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            The 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting to set
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, the default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            The number of shards to create on a Premium Cluster Cache.

        -VirtualNetwork <String>
            The exact ARM resource ID of the virtual network to deploy the redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="bebc9-235">Varsayılan parametrelere sahip bir önbellek oluşturmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-235">To create a cache with default parameters, run the following command.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

<span data-ttu-id="bebc9-236">`ResourceGroupName`, `Name`, ve `Location` Gerekli Parametreler, ancak geri kalan isteğe bağlıdır ve varsayılan değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="bebc9-236">`ResourceGroupName`, `Name`, and `Location` are required parameters, but the rest are optional and have default values.</span></span> <span data-ttu-id="bebc9-237">Önceki komutu çalıştıran standart SKU Azure Redis önbelleği örneği belirtilen adını, konumunu ve devre dışı SSL olmayan bağlantı noktası ile boyutu 1 GB olan kaynak grubunu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bebc9-237">Running the previous command creates a Standard SKU Azure Redis Cache instance with the specified name, location, and resource group, that is 1 GB in size with the non-SSL port disabled.</span></span>

<span data-ttu-id="bebc9-238">Premium önbelleği oluşturmak için P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), boyutunu belirtmek P3 (26 GB - 260 GB), ya da P4 (53 GB'a - 530 GB).</span><span class="sxs-lookup"><span data-stu-id="bebc9-238">To create a premium cache, specify a size of P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), or P4 (53 GB - 530 GB).</span></span> <span data-ttu-id="bebc9-239">Kümeleme etkinleştirmek için bir parça sayısı kullanarak belirtin `ShardCount` parametresi.</span><span class="sxs-lookup"><span data-stu-id="bebc9-239">To enable clustering, specify a shard count using the `ShardCount` parameter.</span></span> <span data-ttu-id="bebc9-240">Aşağıdaki örnek P1 premium önbelleği ile 3 parça oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bebc9-240">The following example creates a P1 premium cache with 3 shards.</span></span> <span data-ttu-id="bebc9-241">Premium P1 önbelleği 6 GB boyutunda, ve şu üç parça belirtilen bu yana toplam boyutu 18 GB (3 x 6 GB).</span><span class="sxs-lookup"><span data-stu-id="bebc9-241">A P1 premium cache is 6 GB in size, and since we specified three shards the total size is 18 GB (3 x 6 GB).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

<span data-ttu-id="bebc9-242">Değerlerini belirtmek için `RedisConfiguration` parametresi içindeki değerleri içine `{}` anahtar/değer çiftleri ister `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span><span class="sxs-lookup"><span data-stu-id="bebc9-242">To specify values for the `RedisConfiguration` parameter, enclose the values inside `{}` as key/value pairs like `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span></span> <span data-ttu-id="bebc9-243">Aşağıdaki örnek, bir standart 1 GB önbellekle oluşturur `allkeys-random` ile yapılandırılmış maxmemory İlkesi ve keyspace bildirimleri `KEA`.</span><span class="sxs-lookup"><span data-stu-id="bebc9-243">The following example creates a standard 1 GB cache with `allkeys-random` maxmemory policy and keyspace notifications configured with `KEA`.</span></span> <span data-ttu-id="bebc9-244">Daha fazla bilgi için bkz: [Keyspace bildirimleri (Gelişmiş ayarları)](cache-configure.md#keyspace-notifications-advanced-settings) ve [bellek ilkeleri](cache-configure.md#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="bebc9-244">For more information, see [Keyspace notifications (advanced settings)](cache-configure.md#keyspace-notifications-advanced-settings) and [Memory policies](cache-configure.md#memory-policies).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="to-configure-the-databases-setting-during-cache-creation"></a><span data-ttu-id="bebc9-245">Önbelleği oluşturma sırasında ayarı veritabanlarını yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="bebc9-245">To configure the databases setting during cache creation</span></span>
<span data-ttu-id="bebc9-246">`databases` Ayarı yalnızca önbellek oluşturma sırasında yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="bebc9-246">The `databases` setting can be configured only during cache creation.</span></span> <span data-ttu-id="bebc9-247">Aşağıdaki örnek, premium P3 oluşturur (26 GB) önbellek kullanarak 48 veritabanlarıyla [yeni AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bebc9-247">The following example creates a premium P3 (26 GB) cache with 48 databases using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

<span data-ttu-id="bebc9-248">Daha fazla bilgi için `databases` özelliği, bkz: [Azure Redis önbelleği varsayılan sunucu yapılandırma](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="bebc9-248">For more information on the `databases` property, see [Default Azure Redis Cache server configuration](cache-configure.md#default-redis-server-configuration).</span></span> <span data-ttu-id="bebc9-249">Kullanarak bir önbellek oluşturma hakkında daha fazla bilgi için [yeni AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet'in önceki bkz [bir Redis önbelleği oluşturmak için](#to-create-a-redis-cache) bölümü.</span><span class="sxs-lookup"><span data-stu-id="bebc9-249">For more information on creating a cache using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, see the previous [To create a Redis Cache](#to-create-a-redis-cache) section.</span></span>

## <a name="to-update-a-redis-cache"></a><span data-ttu-id="bebc9-250">Redis önbelleği güncelleştirmek için</span><span class="sxs-lookup"><span data-stu-id="bebc9-250">To update a Redis cache</span></span>
<span data-ttu-id="bebc9-251">Azure Redis önbelleği örnekleri kullanarak güncel [kümesi AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bebc9-251">Azure Redis Cache instances are updated using the [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span></span>

<span data-ttu-id="bebc9-252">Kullanılabilir parametrelerin ve açıklamaları için listesini görmek için `Set-AzureRmRedisCache`, aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-252">To see a list of available parameters and their descriptions for `Set-AzureRmRedisCache`, run the following command.</span></span>

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
        The Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of the redis cache to update.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        -Size <String>
            Size of the redis cache. The default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. The default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            The 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting to set
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. The default value is null and no change will be made to the
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            The number of shards to create on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="bebc9-253">`Set-AzureRmRedisCache` Cmdlet gibi özellikleri güncelleştirmek için kullanılabilir `Size`, `Sku`, `EnableNonSslPort`ve `RedisConfiguration` değerleri.</span><span class="sxs-lookup"><span data-stu-id="bebc9-253">The `Set-AzureRmRedisCache` cmdlet can be used to update properties such as `Size`, `Sku`, `EnableNonSslPort`, and the `RedisConfiguration` values.</span></span> 

<span data-ttu-id="bebc9-254">Aşağıdaki komut maxmemory İlkesi myCache adlı Redis Önbelleği'için güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="bebc9-254">The following command updates the maxmemory-policy for the Redis Cache named myCache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="to-scale-a-redis-cache"></a><span data-ttu-id="bebc9-255">Redis önbelleği ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="bebc9-255">To scale a Redis cache</span></span>
<span data-ttu-id="bebc9-256">`Set-AzureRmRedisCache`bir Azure Redis önbelleği ölçeklendirmek için kullanılan zaman örnek `Size`, `Sku`, veya `ShardCount` özellikleri değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="bebc9-256">`Set-AzureRmRedisCache` can be used to scale an Azure Redis cache instance when the `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> 

> [!NOTE]
> <span data-ttu-id="bebc9-257">PowerShell kullanarak önbellek ölçeklendirme aynı sınırları ve Azure portalından bir önbellek ölçeklendirme olarak yönergeleri tabidir.</span><span class="sxs-lookup"><span data-stu-id="bebc9-257">Scaling a cache using PowerShell is subject to the same limits and guidelines as scaling a cache from the Azure portal.</span></span> <span data-ttu-id="bebc9-258">Aşağıdaki kısıtlamalarla farklı bir fiyatlandırma katmanı için ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bebc9-258">You can scale to a different pricing tier with the following restrictions.</span></span>
> 
> * <span data-ttu-id="bebc9-259">Daha yüksek bir fiyatlandırma Katmanı'ndan daha düşük bir fiyatlandırma katmanı ölçek olamaz.</span><span class="sxs-lookup"><span data-stu-id="bebc9-259">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
> * <span data-ttu-id="bebc9-260">Ölçeklendirme olamaz bir **Premium** aşağı önbelleğe bir **standart** veya **temel** önbelleği.</span><span class="sxs-lookup"><span data-stu-id="bebc9-260">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
> * <span data-ttu-id="bebc9-261">Ölçeklendirme olamaz bir **standart** aşağı önbelleğe bir **temel** önbelleği.</span><span class="sxs-lookup"><span data-stu-id="bebc9-261">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
> * <span data-ttu-id="bebc9-262">Ölçeklendirme yapılabilir bir **temel** için önbelleğe bir **standart** önbellek ancak değiştiremiyor boyutu aynı anda.</span><span class="sxs-lookup"><span data-stu-id="bebc9-262">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="bebc9-263">Farklı bir boyut gerekiyorsa, istenen boyuta sonraki bir ölçeklendirme işlemi yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bebc9-263">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
> * <span data-ttu-id="bebc9-264">Ölçeklendirme olamaz bir **temel** doğrudan önbelleğe bir **Premium** önbelleği.</span><span class="sxs-lookup"><span data-stu-id="bebc9-264">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="bebc9-265">Ölçeklendirme gerekir **temel** için **standart** bir ölçeklendirme işlemi ve ardından gelen **standart** için **Premium** bir sonraki ölçeklendirme işleminde.</span><span class="sxs-lookup"><span data-stu-id="bebc9-265">You must scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
> * <span data-ttu-id="bebc9-266">Büyük bir değerden aşağı ölçeklendirme olamaz **C0 (250 MB)** boyutu.</span><span class="sxs-lookup"><span data-stu-id="bebc9-266">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>
> 
> <span data-ttu-id="bebc9-267">Daha fazla bilgi için bkz: [ölçek Azure Redis önbelleği nasıl](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="bebc9-267">For more information, see [How to Scale Azure Redis Cache](cache-how-to-scale.md).</span></span>
> 
> 

<span data-ttu-id="bebc9-268">Aşağıdaki örnek adlı bir önbellek ölçeklendirmek nasıl gösterir `myCache` 2,5 GB önbelleğe.</span><span class="sxs-lookup"><span data-stu-id="bebc9-268">The following example shows how to scale a cache named `myCache` to a 2.5 GB cache.</span></span> <span data-ttu-id="bebc9-269">Bu komut bir temel veya standart bir önbellek için çalıştığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-269">Note that this command works for both a Basic or a Standard cache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="bebc9-270">Bu komutu verildikten sonra önbelleği durumunu döndürülür (arama benzer `Get-AzureRmRedisCache`).</span><span class="sxs-lookup"><span data-stu-id="bebc9-270">After this command is issued, the status of the cache is returned (similar to calling `Get-AzureRmRedisCache`).</span></span> <span data-ttu-id="bebc9-271">Unutmayın `ProvisioningState` olan `Scaling`.</span><span class="sxs-lookup"><span data-stu-id="bebc9-271">Note that the `ProvisioningState` is `Scaling`.</span></span>

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

<span data-ttu-id="bebc9-272">Ölçeklendirme işlemi tamamlandığında, `ProvisioningState` değişikliklerini `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="bebc9-272">When the scaling operation is complete, the `ProvisioningState` changes to `Succeeded`.</span></span> <span data-ttu-id="bebc9-273">Temel standart değiştirme ve boyutunu değiştirme gibi sonraki bir ölçeklendirme işlemi yapmanız gerekirse aşağıdakine benzer bir hata iletisi veya önceki işlem tamamlanana kadar beklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bebc9-273">If you need to make a subsequent scaling operation, such as changing from Basic to Standard and then changing the size, you must wait until the previous operation is complete or you receive an error similar to the following.</span></span>

    Set-AzureRmRedisCache : Conflict: The resource '...' is not in a stable state, and is currently unable to accept the update request.

## <a name="to-get-information-about-a-redis-cache"></a><span data-ttu-id="bebc9-274">Redis önbelleği hakkında bilgi almak için</span><span class="sxs-lookup"><span data-stu-id="bebc9-274">To get information about a Redis cache</span></span>
<span data-ttu-id="bebc9-275">Önbellek kullanma hakkında bilgi alabilir [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bebc9-275">You can retrieve information about a cache using the [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span></span>

<span data-ttu-id="bebc9-276">Kullanılabilir parametrelerin ve açıklamaları için listesini görmek için `Get-AzureRmRedisCache`, aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-276">To see a list of available parameters and their descriptions for `Get-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in the specified resource group or all caches in the current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        The Get-AzureRmRedisCache cmdlet gets the details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in the specified resource group.

        If no parameters are given than it will return details about all caches the current subscription.

    PARAMETERS
        -Name <String>
            The name of the cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns the details for the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns the details of the cache specified by Name. If only the ResourceGroup
            parameter is provided, then details for all caches in the resource group are returned.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="bebc9-277">Geçerli abonelikte tüm önbellekleri hakkında bilgi döndürmek için Çalıştır `Get-AzureRmRedisCache` hiçbir parametre olmadan.</span><span class="sxs-lookup"><span data-stu-id="bebc9-277">To return information about all caches in the current subscription, run `Get-AzureRmRedisCache` without any parameters.</span></span>

    Get-AzureRmRedisCache

<span data-ttu-id="bebc9-278">Belirli bir kaynak grubundaki tüm önbellekleri hakkında bilgi döndürmek için Çalıştır `Get-AzureRmRedisCache` ile `ResourceGroupName` parametresi.</span><span class="sxs-lookup"><span data-stu-id="bebc9-278">To return information about all caches in a specific resource group, run `Get-AzureRmRedisCache` with the `ResourceGroupName` parameter.</span></span>

    Get-AzureRmRedisCache -ResourceGroupName myGroup

<span data-ttu-id="bebc9-279">Belirli bir önbellek hakkında bilgi döndürmek için Çalıştır `Get-AzureRmRedisCache` ile `Name` önbellek adını içeren parametre ve `ResourceGroupName` bu önbelleği içeren kaynak grubunu parametresiyle.</span><span class="sxs-lookup"><span data-stu-id="bebc9-279">To return information about a specific cache, run `Get-AzureRmRedisCache` with the `Name` parameter containing the name of the cache, and the `ResourceGroupName` parameter with the resource group containing that cache.</span></span>

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

## <a name="to-retrieve-the-access-keys-for-a-redis-cache"></a><span data-ttu-id="bebc9-280">Redis önbelleği erişim anahtarlarını almak için</span><span class="sxs-lookup"><span data-stu-id="bebc9-280">To retrieve the access keys for a Redis cache</span></span>
<span data-ttu-id="bebc9-281">Önbellek hesabınız için erişim tuşlarını almak için kullanabileceğiniz [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bebc9-281">To retrieve the access keys for your cache, you can use the [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span></span>

<span data-ttu-id="bebc9-282">Kullanılabilir parametrelerin ve açıklamaları için listesini görmek için `Get-AzureRmRedisCacheKey`, aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-282">To see a list of available parameters and their descriptions for `Get-AzureRmRedisCacheKey`, run the following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets the accesskeys for the specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        The Get-AzureRmRedisCacheKey cmdlet gets the access keys for the specified cache.

    PARAMETERS
        -Name <String>
            Name of the redis cache.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="bebc9-283">Önbelleğinizi tuşları almak için arama `Get-AzureRmRedisCacheKey` cmdlet'i ve önbelleğiniz adına önbellek içeren kaynak grubunun adını geçirin.</span><span class="sxs-lookup"><span data-stu-id="bebc9-283">To retrieve the keys for your cache, call the `Get-AzureRmRedisCacheKey` cmdlet and pass in the name of your cache the name of the resource group that contains the cache.</span></span>

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="to-regenerate-access-keys-for-your-redis-cache"></a><span data-ttu-id="bebc9-284">Redis önbelleği erişim anahtarlarını yeniden oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="bebc9-284">To regenerate access keys for your Redis cache</span></span>
<span data-ttu-id="bebc9-285">Önbelleğinizi erişim anahtarlarını yeniden oluşturmak için kullanabileceğiniz [yeni AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bebc9-285">To regenerate the access keys for your cache, you can use the [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span></span>

<span data-ttu-id="bebc9-286">Kullanılabilir parametrelerin ve açıklamaları için listesini görmek için `New-AzureRmRedisCacheKey`, aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-286">To see a list of available parameters and their descriptions for `New-AzureRmRedisCacheKey`, run the following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates the access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        The New-AzureRmRedisCacheKey cmdlet regenerate the access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of the redis cache.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        -KeyType <String>
            Specifies whether to regenerate the primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When the Force parameter is provided, the specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="bebc9-287">Önbellek hesabınız için birincil veya ikincil anahtarı yeniden oluşturmak için arama `New-AzureRmRedisCacheKey` cmdlet adı, kaynak grubu, geçirin ve belirtin `Primary` veya `Secondary` için `KeyType` parametresi.</span><span class="sxs-lookup"><span data-stu-id="bebc9-287">To regenerate the primary or secondary key for your cache, call the `New-AzureRmRedisCacheKey` cmdlet and pass in the name, resource group, and specify either `Primary` or `Secondary` for the `KeyType` parameter.</span></span> <span data-ttu-id="bebc9-288">Aşağıdaki örnekte, bir önbellek için ikincil erişim anahtarını yeniden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bebc9-288">In the following example, the secondary access key for a cache is regenerated.</span></span>

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want to regenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="to-delete-a-redis-cache"></a><span data-ttu-id="bebc9-289">Redis önbelleğini silmek için</span><span class="sxs-lookup"><span data-stu-id="bebc9-289">To delete a Redis cache</span></span>
<span data-ttu-id="bebc9-290">Redis önbelleği silmek için kullanın [Kaldır AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bebc9-290">To delete a Redis cache, use the [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span></span>

<span data-ttu-id="bebc9-291">Kullanılabilir parametrelerin ve açıklamaları için listesini görmek için `Remove-AzureRmRedisCache`, aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-291">To see a list of available parameters and their descriptions for `Remove-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        The Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of the redis cache to remove.

        -ResourceGroupName <String>
            Name of the resource group of the cache to remove.

        -Force
            When the Force parameter is provided, the cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes the cache and does not return any value. If the PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating the success of the operatio

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="bebc9-292">Aşağıdaki örnekte, önbelleğe adlı `myCache` kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="bebc9-292">In the following example, the cache named `myCache` is removed.</span></span>

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want to remove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="to-import-a-redis-cache"></a><span data-ttu-id="bebc9-293">Redis önbelleği içeri aktarmak için</span><span class="sxs-lookup"><span data-stu-id="bebc9-293">To import a Redis cache</span></span>
<span data-ttu-id="bebc9-294">Bir Azure Redis önbelleği örneği kullanarak içine veri aktarabilirsiniz `Import-AzureRmRedisCache` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bebc9-294">You can import data into an Azure Redis Cache instance using the `Import-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bebc9-295">İçeri/dışarı aktarma için kullanılabilir yalnızca [premium katmanı](cache-premium-tier-intro.md) önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="bebc9-295">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="bebc9-296">İçeri/dışarı aktarma hakkında daha fazla bilgi için bkz: [içeri ve dışarı aktarma Azure Redis önbelleği verilerde](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="bebc9-296">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="bebc9-297">Kullanılabilir parametrelerin ve açıklamaları için listesini görmek için `Import-AzureRmRedisCache`, aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-297">To see a list of available parameters and their descriptions for `Import-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs to Azure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Import-AzureRmRedisCache cmdlet imports data from the specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into the cache.

        -Format <String>
            Format for the blob.  Currently "rdb" is the only supported, with other formats expected in the future.

        -Force
            When the Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If the PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating the success of the
            operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="bebc9-298">Aşağıdaki komutu Azure Redis önbelleğine SAS URI tarafından belirtilen blob verileri alır.</span><span class="sxs-lookup"><span data-stu-id="bebc9-298">The following command imports data from the blob specified by the SAS uri into Azure Redis Cache.</span></span>

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="to-export-a-redis-cache"></a><span data-ttu-id="bebc9-299">Redis önbelleği dışarı aktarmak için</span><span class="sxs-lookup"><span data-stu-id="bebc9-299">To export a Redis cache</span></span>
<span data-ttu-id="bebc9-300">Verileri kullanarak bir Azure Redis önbelleği örneği verebilirsiniz `Export-AzureRmRedisCache` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bebc9-300">You can export data from an Azure Redis Cache instance using the `Export-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bebc9-301">İçeri/dışarı aktarma için kullanılabilir yalnızca [premium katmanı](cache-premium-tier-intro.md) önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="bebc9-301">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="bebc9-302">İçeri/dışarı aktarma hakkında daha fazla bilgi için bkz: [içeri ve dışarı aktarma Azure Redis önbelleği verilerde](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="bebc9-302">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="bebc9-303">Kullanılabilir parametrelerin ve açıklamaları için listesini görmek için `Export-AzureRmRedisCache`, aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-303">To see a list of available parameters and their descriptions for `Export-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache to a specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache to a specified container.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -Prefix <String>
            Prefix to use for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for the blob.  Currently "rdb" is the only supported, with other formats expected in the future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If the PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating the success of the operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="bebc9-304">Aşağıdaki komutu, SAS URI tarafından belirtilen kapsayıcı Azure Redis önbelleği örneğine gelen verileri verir.</span><span class="sxs-lookup"><span data-stu-id="bebc9-304">The following command exports data from an Azure Redis Cache instance into the container specified by the SAS uri.</span></span>

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="to-reboot-a-redis-cache"></a><span data-ttu-id="bebc9-305">Redis önbelleği yeniden başlatmak için</span><span class="sxs-lookup"><span data-stu-id="bebc9-305">To reboot a Redis cache</span></span>
<span data-ttu-id="bebc9-306">Azure Redis önbelleği örneği kullanarak yeniden `Reset-AzureRmRedisCache` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bebc9-306">You can reboot your Azure Redis Cache instance using the `Reset-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bebc9-307">Yeniden başlatma için kullanılabilir yalnızca [premium katmanı](cache-premium-tier-intro.md) önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="bebc9-307">Reboot is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="bebc9-308">Önbelleğinizi yeniden başlatma hakkında daha fazla bilgi için bkz: [önbelleğe yönetim - yeniden başlatma](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="bebc9-308">For more information about rebooting your cache, see [Cache administration - reboot](cache-administration.md#reboot).</span></span>
> 
> 

<span data-ttu-id="bebc9-309">Kullanılabilir parametrelerin ve açıklamaları için listesini görmek için `Reset-AzureRmRedisCache`, aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-309">To see a list of available parameters and their descriptions for `Reset-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Reset-AzureRmRedisCache cmdlet reboots the specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -RebootType <String>
            Which node to reboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard to reboot when rebooting a premium cache with clustering enabled.

        -Force
            When the Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If the PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating the success of the operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="bebc9-310">Aşağıdaki komutu her iki düğüm belirtilen önbelleğin yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="bebc9-310">The following command reboots both nodes of the specified cache.</span></span>

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a><span data-ttu-id="bebc9-311">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bebc9-311">Next steps</span></span>
<span data-ttu-id="bebc9-312">Azure ile Windows PowerShell kullanma hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="bebc9-312">To learn more about using Windows PowerShell with Azure, see the following resources:</span></span>

* [<span data-ttu-id="bebc9-313">MSDN'deki Azure Redis önbelleği cmdlet belgeleri</span><span class="sxs-lookup"><span data-stu-id="bebc9-313">Azure Redis Cache cmdlet documentation on MSDN</span></span>](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* <span data-ttu-id="bebc9-314">[Azure Resource Manager cmdlet'lerini](http://go.microsoft.com/fwlink/?LinkID=394765): Azure Resource Manager modülünde cmdlet'leri kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="bebc9-314">[Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): Learn to use the cmdlets in the Azure Resource Manager module.</span></span>
* <span data-ttu-id="bebc9-315">[Azure kaynaklarınızı yönetmek için kaynak gruplarını kullanma](../azure-resource-manager/resource-group-template-deploy-portal.md): Azure portalındaki kaynak gruplarını oluşturma ve yönetme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="bebc9-315">[Using Resource groups to manage your Azure resources](../azure-resource-manager/resource-group-template-deploy-portal.md): Learn how to create and manage resource groups in the Azure portal.</span></span>
* <span data-ttu-id="bebc9-316">[Azure blogu](http://blogs.msdn.com/windowsazure): Azure yeni özellikler hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="bebc9-316">[Azure blog](http://blogs.msdn.com/windowsazure): Learn about new features in Azure.</span></span>
* <span data-ttu-id="bebc9-317">[Windows PowerShell Web günlüğü](http://blogs.msdn.com/powershell): Windows PowerShell'de yeni özellikler hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="bebc9-317">[Windows PowerShell blog](http://blogs.msdn.com/powershell): Learn about new features in Windows PowerShell.</span></span>
* <span data-ttu-id="bebc9-318">["Hey, betik yazarı!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Windows PowerShell Topluluğu'ndan gerçek ipuçları ve püf noktaları alın.</span><span class="sxs-lookup"><span data-stu-id="bebc9-318">["Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Get real-world tips and tricks from the Windows PowerShell community.</span></span>

