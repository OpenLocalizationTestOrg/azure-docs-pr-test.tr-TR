---
title: "aaaAzure Cosmos DB Otomasyon - Powershell ile Yönetimi | Microsoft Docs"
description: "Kullanım Azure PowerShell'i Azure Cosmos DB hesaplarınızı yönetin."
services: cosmos-db
author: dmakwana
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: dimakwan
ms.openlocfilehash: 3239fb815918a0e47bff69fcd1ab6562519e429b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a><span data-ttu-id="9a3b0-103">PowerShell kullanarak bir Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a3b0-103">Create an Azure Cosmos DB account using PowerShell</span></span>

<span data-ttu-id="9a3b0-104">Merhaba aşağıdaki kılavuz Azure Powershell kullanarak Azure Cosmos DB veritabanı hesaplarınızı komutları tooautomate yönetimini açıklar.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-104">hello following guide describes commands tooautomate management of your Azure Cosmos DB database accounts using Azure Powershell.</span></span> <span data-ttu-id="9a3b0-105">Komutları toomanage hesabı anahtarları ve yük devretme öncelikleri'nde de içerir [bölgeli veritabanı hesaplarını][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="9a3b0-105">It also includes commands toomanage account keys and failover priorities in [multi-region database accounts][scaling-globally].</span></span> <span data-ttu-id="9a3b0-106">Veritabanı hesabını güncelleştirme toomodify tutarlılık ilkeleri ve Ekle/Kaldır bölgeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-106">Updating your database account allows you toomodify consistency policies and add/remove regions.</span></span> <span data-ttu-id="9a3b0-107">Ya da kullanmak için platformlar arası yönetim Azure Cosmos DB hesabınızın [Azure CLI](cli-samples.md), hello [kaynak sağlayıcısı REST API][rp-rest-api], veya hello [Azure Portal](create-documentdb-dotnet.md#create-account).</span><span class="sxs-lookup"><span data-stu-id="9a3b0-107">For cross-platform management of your Azure Cosmos DB account, you can use either [Azure CLI](cli-samples.md), hello [Resource Provider REST API][rp-rest-api], or hello [Azure portal](create-documentdb-dotnet.md#create-account).</span></span>

## <a name="getting-started"></a><span data-ttu-id="9a3b0-108">Başlarken</span><span class="sxs-lookup"><span data-stu-id="9a3b0-108">Getting Started</span></span>

<span data-ttu-id="9a3b0-109">Merhaba yönergeleri izleyin [nasıl tooinstall Azure PowerShell'i ve yapılandırma] [ powershell-install-configure] tooinstall ve tooyour Azure Resource Manager günlüğüne PowerShell'de hesap.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-109">Follow hello instructions in [How tooinstall and configure Azure PowerShell][powershell-install-configure] tooinstall and log in tooyour Azure Resource Manager account in Powershell.</span></span>

### <a name="notes"></a><span data-ttu-id="9a3b0-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="9a3b0-110">Notes</span></span>

* <span data-ttu-id="9a3b0-111">Kullanıcı onayı gerektirmeden komutları aşağıdaki tooexecute hello isterseniz hello append `-Force` bayrak toohello komutu.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-111">If you would like tooexecute hello following commands without requiring user confirmation, append hello `-Force` flag toohello command.</span></span>
* <span data-ttu-id="9a3b0-112">Aşağıdaki komutları tüm hello zaman uyumlu.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-112">All hello following commands are synchronous.</span></span>

## <span data-ttu-id="9a3b0-113"><a id="create-documentdb-account-powershell"></a>Bir Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a3b0-113"><a id="create-documentdb-account-powershell"></a> Create an Azure Cosmos DB Account</span></span>

<span data-ttu-id="9a3b0-114">Bu komut, toocreate Azure Cosmos DB veritabanı hesabı sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-114">This command allows you toocreate an Azure Cosmos DB database account.</span></span> <span data-ttu-id="9a3b0-115">Yeni veritabanı hesabınız ya da tek bölge yapılandırmak veya [bölgeli] [ scaling-globally] belirli bir ile [tutarlılık İlkesi](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="9a3b0-115">Configure your new database account as either single-region or [multi-region][scaling-globally] with a certain [consistency policy](consistency-levels.md).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="9a3b0-116">`<write-region-location>`Başlangıç konumu hello adını hello veritabanı hesabı bölgesi yazma.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-116">`<write-region-location>` hello location name of hello write region of hello database account.</span></span> <span data-ttu-id="9a3b0-117">Bu konum gerekli toohave bir yük devretme öncelik değeri 0 değil.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-117">This location is required toohave a failover priority value of 0.</span></span> <span data-ttu-id="9a3b0-118">Veritabanı hesabı başına tam olarak bir yazma bölge olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-118">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="9a3b0-119">`<read-region-location>`Başlangıç konumu hello adını hello veritabanı hesabı bölgesi okuyun.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-119">`<read-region-location>` hello location name of hello read region of hello database account.</span></span> <span data-ttu-id="9a3b0-120">Bu konum gerekli toohave 0'dan büyük bir yük devretme öncelik değeri değil.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-120">This location is required toohave a failover priority value of greater than 0.</span></span> <span data-ttu-id="9a3b0-121">Veritabanı hesabı başına birden fazla okuma bölgeler olabilir.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-121">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="9a3b0-122">`<ip-range-filter>`İzin verilen veritabanı hesabı için istemci IP listesi hello olarak dahil CIDR form toobe Hello kümesi IP adresleri ve IP adres aralıklarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-122">`<ip-range-filter>` Specifies hello set of IP addresses or IP address ranges in CIDR form toobe included as hello allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="9a3b0-123">IP adresleri/aralıklarına virgülle ayrılmış ve boşluk içermemelidir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-123">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="9a3b0-124">Daha fazla bilgi için bkz: [Azure Cosmos DB güvenlik duvarı desteği](firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="9a3b0-124">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="9a3b0-125">`<default-consistency-level>`Merhaba varsayılan tutarlılık düzeyi hello Azure Cosmos DB hesabı.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-125">`<default-consistency-level>` hello default consistency level of hello Azure Cosmos DB account.</span></span> <span data-ttu-id="9a3b0-126">Daha fazla bilgi için bkz: [Azure Cosmos veritabanı tutarlılık düzeylerini](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="9a3b0-126">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="9a3b0-127">`<max-interval>`Sınırlanmış eskime durumu tutarlılığı ile kullanıldığında, bu değer izin hello süre miktarı (saniye cinsinden) eskime durumu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-127">`<max-interval>` When used with Bounded Staleness consistency, this value represents hello time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="9a3b0-128">Bu değer için kabul edilebilir aralık 1-100'dür.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-128">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="9a3b0-129">`<max-staleness-prefix>`Sınırlanmış eskime durumu tutarlılığı ile kullanıldığında, bu değer hello izin eski istek sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-129">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents hello number of stale requests tolerated.</span></span> <span data-ttu-id="9a3b0-130">Bu değer için kabul edilebilir aralık 1 – 2,147,483,647 şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-130">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="9a3b0-131">`<resource-group-name>`Merhaba Hello adını [Azure kaynak grubu] [ azure-resource-groups] toowhich hello yeni Azure Cosmos DB veritabanı hesabı ait.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-131">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="9a3b0-132">`<resource-group-location>`hello Azure kaynak grubu toowhich hello yeni Azure Cosmos DB veritabanı hesabı Hello konumunu ait.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-132">`<resource-group-location>` hello location of hello Azure Resource Group toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="9a3b0-133">`<database-account-name>`oluşturulan hello Azure Cosmos DB veritabanı hesabı toobe Hello adı.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-133">`<database-account-name>` hello name of hello Azure Cosmos DB database account toobe created.</span></span> <span data-ttu-id="9a3b0-134">Yalnızca küçük harfler, rakamlar, hello kullanabileceği '-' karakteri ve 3-50 karakter arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-134">It can only use lowercase letters, numbers, hello '-' character, and must be between 3 and 50 characters.</span></span>

<span data-ttu-id="9a3b0-135">Örnek:</span><span class="sxs-lookup"><span data-stu-id="9a3b0-135">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a><span data-ttu-id="9a3b0-136">Notlar</span><span class="sxs-lookup"><span data-stu-id="9a3b0-136">Notes</span></span>
* <span data-ttu-id="9a3b0-137">Merhaba önceki örnekte bir veritabanı hesabı ile iki bölgede oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-137">hello preceding example creates a database account with two regions.</span></span> <span data-ttu-id="9a3b0-138">Ayrıca, olası toocreate (Merhaba yazma bölge atanır ve bir yük devretme öncelik değeri 0 olan) bir bölge veya birden çok iki bölgede bir veritabanı hesabı unutulmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-138">It is also possible toocreate a database account with either one region (which is designated as hello write region and have a failover priority value of 0) or more than two regions.</span></span> <span data-ttu-id="9a3b0-139">Daha fazla bilgi için bkz: [bölgeli veritabanı hesaplarını][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="9a3b0-139">For more information, see [multi-region database accounts][scaling-globally].</span></span>
* <span data-ttu-id="9a3b0-140">Hello konumlarına bölgeler Azure Cosmos DB genel olarak kullanılabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-140">hello locations must be regions in which Azure Cosmos DB is generally available.</span></span> <span data-ttu-id="9a3b0-141">Merhaba geçerli bölgelerin listesi hello üzerinde sağlanan [Azure bölgeleri sayfa](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="9a3b0-141">hello current list of regions is provided on hello [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

## <span data-ttu-id="9a3b0-142"><a id="update-documentdb-account-powershell"></a>Bir DocumentDB veritabanı hesabı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="9a3b0-142"><a id="update-documentdb-account-powershell"></a> Update a DocumentDB Database Account</span></span>

<span data-ttu-id="9a3b0-143">Bu komutu tooupdate sağlar, Azure Cosmos DB veritabanı hesabı özellikleri.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-143">This command allows you tooupdate your Azure Cosmos DB database account properties.</span></span> <span data-ttu-id="9a3b0-144">Bu hangi hello veritabanı hesabı bulunmaktadır hello tutarlılık ilke ve hello konumları içerir.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-144">This includes hello consistency policy and hello locations which hello database account exists in.</span></span>

> [!NOTE]
> <span data-ttu-id="9a3b0-145">Bu komut tooadd ve Kaldır bölgeler sağlar ancak toomodify yük devretme öncelikleri izin vermiyor.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-145">This command allows you tooadd and remove regions but does not allow you toomodify failover priorities.</span></span> <span data-ttu-id="9a3b0-146">toomodify yük devretme öncelikleri görmek [aşağıda](#modify-failover-priority-powershell).</span><span class="sxs-lookup"><span data-stu-id="9a3b0-146">toomodify failover priorities, see [below](#modify-failover-priority-powershell).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="9a3b0-147">`<write-region-location>`Başlangıç konumu hello adını hello veritabanı hesabı bölgesi yazma.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-147">`<write-region-location>` hello location name of hello write region of hello database account.</span></span> <span data-ttu-id="9a3b0-148">Bu konum gerekli toohave bir yük devretme öncelik değeri 0 değil.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-148">This location is required toohave a failover priority value of 0.</span></span> <span data-ttu-id="9a3b0-149">Veritabanı hesabı başına tam olarak bir yazma bölge olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-149">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="9a3b0-150">`<read-region-location>`Başlangıç konumu hello adını hello veritabanı hesabı bölgesi okuyun.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-150">`<read-region-location>` hello location name of hello read region of hello database account.</span></span> <span data-ttu-id="9a3b0-151">Bu konum gerekli toohave 0'dan büyük bir yük devretme öncelik değeri değil.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-151">This location is required toohave a failover priority value of greater than 0.</span></span> <span data-ttu-id="9a3b0-152">Veritabanı hesabı başına birden fazla okuma bölgeler olabilir.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-152">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="9a3b0-153">`<default-consistency-level>`Merhaba varsayılan tutarlılık düzeyi hello Azure Cosmos DB hesabı.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-153">`<default-consistency-level>` hello default consistency level of hello Azure Cosmos DB account.</span></span> <span data-ttu-id="9a3b0-154">Daha fazla bilgi için bkz: [Azure Cosmos veritabanı tutarlılık düzeylerini](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="9a3b0-154">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="9a3b0-155">`<ip-range-filter>`İzin verilen veritabanı hesabı için istemci IP listesi hello olarak dahil CIDR form toobe Hello kümesi IP adresleri ve IP adres aralıklarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-155">`<ip-range-filter>` Specifies hello set of IP addresses or IP address ranges in CIDR form toobe included as hello allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="9a3b0-156">IP adresleri/aralıklarına virgülle ayrılmış ve boşluk içermemelidir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-156">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="9a3b0-157">Daha fazla bilgi için bkz: [Azure Cosmos DB güvenlik duvarı desteği](firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="9a3b0-157">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="9a3b0-158">`<max-interval>`Sınırlanmış eskime durumu tutarlılığı ile kullanıldığında, bu değer izin hello süre miktarı (saniye cinsinden) eskime durumu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-158">`<max-interval>` When used with Bounded Staleness consistency, this value represents hello time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="9a3b0-159">Bu değer için kabul edilebilir aralık 1-100'dür.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-159">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="9a3b0-160">`<max-staleness-prefix>`Sınırlanmış eskime durumu tutarlılığı ile kullanıldığında, bu değer hello izin eski istek sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-160">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents hello number of stale requests tolerated.</span></span> <span data-ttu-id="9a3b0-161">Bu değer için kabul edilebilir aralık 1 – 2,147,483,647 şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-161">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="9a3b0-162">`<resource-group-name>`Merhaba Hello adını [Azure kaynak grubu] [ azure-resource-groups] toowhich hello yeni Azure Cosmos DB veritabanı hesabı ait.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-162">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="9a3b0-163">`<resource-group-location>`hello Azure kaynak grubu toowhich hello yeni Azure Cosmos DB veritabanı hesabı Hello konumunu ait.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-163">`<resource-group-location>` hello location of hello Azure Resource Group toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="9a3b0-164">`<database-account-name>`güncelleştirilmiş hello Azure Cosmos DB veritabanı hesabı toobe Hello adı.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-164">`<database-account-name>` hello name of hello Azure Cosmos DB database account toobe updated.</span></span>

<span data-ttu-id="9a3b0-165">Örnek:</span><span class="sxs-lookup"><span data-stu-id="9a3b0-165">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <span data-ttu-id="9a3b0-166"><a id="delete-documentdb-account-powershell"></a>Bir DocumentDB veritabanı hesabı silme</span><span class="sxs-lookup"><span data-stu-id="9a3b0-166"><a id="delete-documentdb-account-powershell"></a> Delete a DocumentDB Database Account</span></span>

<span data-ttu-id="9a3b0-167">Bu komut toodelete var olan bir Azure Cosmos DB veritabanı hesabını verir.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-167">This command allows you toodelete an existing Azure Cosmos DB database account.</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* <span data-ttu-id="9a3b0-168">`<resource-group-name>`Merhaba Hello adını [Azure kaynak grubu] [ azure-resource-groups] toowhich hello yeni Azure Cosmos DB veritabanı hesabı ait.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-168">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="9a3b0-169">`<database-account-name>`hello Azure Cosmos DB veritabanı hesabı toobe silinmiş Hello adı.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-169">`<database-account-name>` hello name of hello Azure Cosmos DB database account toobe deleted.</span></span>

<span data-ttu-id="9a3b0-170">Örnek:</span><span class="sxs-lookup"><span data-stu-id="9a3b0-170">Example:</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="9a3b0-171"><a id="get-documentdb-properties-powershell"></a>Bir DocumentDB veritabanı hesabı özelliklerini alır</span><span class="sxs-lookup"><span data-stu-id="9a3b0-171"><a id="get-documentdb-properties-powershell"></a> Get Properties of a DocumentDB Database Account</span></span>

<span data-ttu-id="9a3b0-172">Bu komut, var olan bir Azure Cosmos DB veritabanı hesabını tooget hello özelliklerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-172">This command allows you tooget hello properties of an existing Azure Cosmos DB database account.</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="9a3b0-173">`<resource-group-name>`Merhaba Hello adını [Azure kaynak grubu] [ azure-resource-groups] toowhich hello yeni Azure Cosmos DB veritabanı hesabı ait.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-173">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="9a3b0-174">`<database-account-name>`hello Azure Cosmos DB veritabanı hesabı Hello adı.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-174">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>

<span data-ttu-id="9a3b0-175">Örnek:</span><span class="sxs-lookup"><span data-stu-id="9a3b0-175">Example:</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="9a3b0-176"><a id="update-tags-powershell"></a>Bir Azure Cosmos DB veritabanı hesabını güncelleştirme etiketleri</span><span class="sxs-lookup"><span data-stu-id="9a3b0-176"><a id="update-tags-powershell"></a> Update Tags of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="9a3b0-177">Merhaba aşağıdaki örnekte açıklanmaktadır nasıl tooset [Azure kaynak etiketleri] [ azure-resource-tags] Azure Cosmos DB için veritabanı hesabı.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-177">hello following example describes how tooset [Azure resource tags][azure-resource-tags] for your Azure Cosmos DB database account.</span></span>

> [!NOTE]
> <span data-ttu-id="9a3b0-178">Bu komut hello ile birleştirilebilir oluşturma veya güncelleştirme komutları hello ekleyerek `-Tags` bayrağı hello karşılık gelen bir parametre ile.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-178">This command can be combined with hello create or update commands by appending hello `-Tags` flag with hello corresponding parameter.</span></span>

<span data-ttu-id="9a3b0-179">Örnek:</span><span class="sxs-lookup"><span data-stu-id="9a3b0-179">Example:</span></span>

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <span data-ttu-id="9a3b0-180"><a id="list-account-keys-powershell"></a>Liste hesabı anahtarları</span><span class="sxs-lookup"><span data-stu-id="9a3b0-180"><a id="list-account-keys-powershell"></a> List Account Keys</span></span>

<span data-ttu-id="9a3b0-181">Bir Azure Cosmos DB hesabı oluşturduğunuzda, hello hizmeti hello Azure Cosmos DB hesap erişildiğinde, kimlik doğrulaması için kullanılan iki ana erişim tuşu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-181">When you create an Azure Cosmos DB account, hello service generates two master access keys that can be used for authentication when hello Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="9a3b0-182">İki erişim tuşu sağlayarak Azure Cosmos DB tooregenerate hello herhangi kesinti tooyour Azure Cosmos DB hesap anahtarlarla sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-182">By providing two access keys, Azure Cosmos DB enables you tooregenerate hello keys with no interruption tooyour Azure Cosmos DB account.</span></span> <span data-ttu-id="9a3b0-183">Salt okunur işlemler kimlik doğrulaması için salt okunur anahtar de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-183">Read-only keys for authenticating read-only operations are also available.</span></span> <span data-ttu-id="9a3b0-184">Var. iki okuma-yazma anahtarları (birincil ve ikincil) ve iki salt okunur anahtarları (birincil ve ikincil)</span><span class="sxs-lookup"><span data-stu-id="9a3b0-184">There are two read-write keys (primary and secondary) and two read-only keys (primary and secondary).</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="9a3b0-185">`<resource-group-name>`Merhaba Hello adını [Azure kaynak grubu] [ azure-resource-groups] toowhich hello yeni Azure Cosmos DB veritabanı hesabı ait.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-185">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="9a3b0-186">`<database-account-name>`hello Azure Cosmos DB veritabanı hesabı Hello adı.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-186">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>

<span data-ttu-id="9a3b0-187">Örnek:</span><span class="sxs-lookup"><span data-stu-id="9a3b0-187">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="9a3b0-188"><a id="list-connection-strings-powershell"></a>Liste bağlantı dizeleri</span><span class="sxs-lookup"><span data-stu-id="9a3b0-188"><a id="list-connection-strings-powershell"></a> List Connection Strings</span></span>

<span data-ttu-id="9a3b0-189">MongoDB hesapları için komutu aşağıdaki hello kullanarak MongoDB uygulama toohello veritabanı hesabınızı alınabilir bağlantı dizesi tooconnect hello.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-189">For MongoDB accounts, hello connection string tooconnect your MongoDB app toohello database account can be retrieved using hello following command.</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="9a3b0-190">`<resource-group-name>`Merhaba Hello adını [Azure kaynak grubu] [ azure-resource-groups] toowhich hello yeni Azure Cosmos DB veritabanı hesabı ait.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-190">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="9a3b0-191">`<database-account-name>`hello Azure Cosmos DB veritabanı hesabı Hello adı.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-191">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>

<span data-ttu-id="9a3b0-192">Örnek:</span><span class="sxs-lookup"><span data-stu-id="9a3b0-192">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="9a3b0-193"><a id="regenerate-account-key-powershell"></a>Hesap anahtarını yeniden oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a3b0-193"><a id="regenerate-account-key-powershell"></a> Regenerate Account Key</span></span>

<span data-ttu-id="9a3b0-194">Merhaba erişim anahtarları tooyour Azure Cosmos DB hesabı değiştirmelisiniz düzenli aralıklarla toohelp tutmak bağlantılarınızı daha güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-194">You should change hello access keys tooyour Azure Cosmos DB account periodically toohelp keep your connections more secure.</span></span> <span data-ttu-id="9a3b0-195">İki erişim tuşu tooenable atanır, toomaintain bağlantıları toohello bir erişim anahtarı kullanırken, yeniden Azure Cosmos DB hesap hello diğer erişim anahtarı.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-195">Two access keys are assigned tooenable you toomaintain connections toohello Azure Cosmos DB account using one access key while you regenerate hello other access key.</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* <span data-ttu-id="9a3b0-196">`<resource-group-name>`Merhaba Hello adını [Azure kaynak grubu] [ azure-resource-groups] toowhich hello yeni Azure Cosmos DB veritabanı hesabı ait.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-196">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="9a3b0-197">`<database-account-name>`hello Azure Cosmos DB veritabanı hesabı Hello adı.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-197">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>
* <span data-ttu-id="9a3b0-198">`<key-kind>`Anahtarların hello dört türlerinden birini: ["Birincil" | " İkincil "|" PrimaryReadonly "|" Tooregenerate istediğiniz SecondaryReadonly"].</span><span class="sxs-lookup"><span data-stu-id="9a3b0-198">`<key-kind>` One of hello four types of keys: ["Primary"|"Secondary"|"PrimaryReadonly"|"SecondaryReadonly"] that you would like tooregenerate.</span></span>

<span data-ttu-id="9a3b0-199">Örnek:</span><span class="sxs-lookup"><span data-stu-id="9a3b0-199">Example:</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <span data-ttu-id="9a3b0-200"><a id="modify-failover-priority-powershell"></a>Bir Azure Cosmos DB veritabanı hesabının yük devretme öncelik değiştirme</span><span class="sxs-lookup"><span data-stu-id="9a3b0-200"><a id="modify-failover-priority-powershell"></a> Modify Failover Priority of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="9a3b0-201">Bölgeli veritabanı hesapları için Azure Cosmos DB veritabanı hesabı hello çeşitli bölgelere mevcut hello hello yük devretme önceliğini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-201">For multi-region database accounts, you can change hello failover priority of hello various regions which hello Azure Cosmos DB database account exists in.</span></span> <span data-ttu-id="9a3b0-202">Azure Cosmos DB veritabanı hesabınızda yük devretme hakkında daha fazla bilgi için bkz: [Azure Cosmos DB genel verilerle dağıtmak][distribute-data-globally].</span><span class="sxs-lookup"><span data-stu-id="9a3b0-202">For more information on failover in your Azure Cosmos DB database account, see [Distribute data globally with Azure Cosmos DB][distribute-data-globally].</span></span>

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* <span data-ttu-id="9a3b0-203">`<write-region-location>`Başlangıç konumu hello adını hello veritabanı hesabı bölgesi yazma.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-203">`<write-region-location>` hello location name of hello write region of hello database account.</span></span> <span data-ttu-id="9a3b0-204">Bu konum gerekli toohave bir yük devretme öncelik değeri 0 değil.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-204">This location is required toohave a failover priority value of 0.</span></span> <span data-ttu-id="9a3b0-205">Veritabanı hesabı başına tam olarak bir yazma bölge olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-205">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="9a3b0-206">`<read-region-location>`Başlangıç konumu hello adını hello veritabanı hesabı bölgesi okuyun.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-206">`<read-region-location>` hello location name of hello read region of hello database account.</span></span> <span data-ttu-id="9a3b0-207">Bu konum gerekli toohave 0'dan büyük bir yük devretme öncelik değeri değil.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-207">This location is required toohave a failover priority value of greater than 0.</span></span> <span data-ttu-id="9a3b0-208">Veritabanı hesabı başına birden fazla okuma bölgeler olabilir.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-208">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="9a3b0-209">`<resource-group-name>`Merhaba Hello adını [Azure kaynak grubu] [ azure-resource-groups] toowhich hello yeni Azure Cosmos DB veritabanı hesabı ait.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-209">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="9a3b0-210">`<database-account-name>`hello Azure Cosmos DB veritabanı hesabı Hello adı.</span><span class="sxs-lookup"><span data-stu-id="9a3b0-210">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>

<span data-ttu-id="9a3b0-211">Örnek:</span><span class="sxs-lookup"><span data-stu-id="9a3b0-211">Example:</span></span>

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a><span data-ttu-id="9a3b0-212">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9a3b0-212">Next steps</span></span>

* <span data-ttu-id="9a3b0-213">.NET kullanarak tooconnect bkz [bağlanma ve sorgu .NET ile](create-documentdb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="9a3b0-213">tooconnect using .NET, see [Connect and query with .NET](create-documentdb-dotnet.md).</span></span>
* <span data-ttu-id="9a3b0-214">.NET Core kullanarak tooconnect bkz [Connect ve .NET Core sorguyla](create-documentdb-dotnet-core.md).</span><span class="sxs-lookup"><span data-stu-id="9a3b0-214">tooconnect using .NET Core, see [Connect and query with .NET Core](create-documentdb-dotnet-core.md).</span></span>
* <span data-ttu-id="9a3b0-215">Node.js kullanarak tooconnect bkz [Connect ve Node.js ve MongoDB uygulama sorguyla](create-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9a3b0-215">tooconnect using Node.js, see [Connect and query with Node.js and a MongoDB app](create-mongodb-nodejs.md).</span></span>

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
