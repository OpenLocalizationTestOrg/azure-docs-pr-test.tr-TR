---
title: "aaaAzure izleme REST API gözden geçirme | Microsoft Docs"
description: "Nasıl tooauthenticate tooand kullanım hello Azure izleme REST API istekleri."
author: mcollier
manager: 
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 565e6a88-3131-4a48-8b82-3effc9a3d5c6
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: mcollier
ms.openlocfilehash: b8ae3a03fd21af872f1dc5fed40a101a24ca1652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitoring-rest-api-walkthrough"></a><span data-ttu-id="b2816-103">REST API izlenecek izleme azure</span><span class="sxs-lookup"><span data-stu-id="b2816-103">Azure Monitoring REST API Walkthrough</span></span>
<span data-ttu-id="b2816-104">Bu makale size nasıl gösterir kodunuzu hello kullanabilmeniz için tooperform kimlik doğrulaması [Microsoft Azure İzleyici REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2816-104">This article shows you how tooperform authentication so your code can use hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>         

<span data-ttu-id="b2816-105">Hello Azure İzleyici API olası tooprogrammatically alma hello kullanılabilir varsayılan ölçüm tanımları (ölçümü CPU süresi, istekleri, vb. gibi hello türü), ayrıntı düzeyi ve ölçüm değerleri kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="b2816-105">hello Azure Monitor API makes it possible tooprogrammatically retrieve hello available default metric definitions (hello type of metric such as CPU Time, Requests, etc.), granularity, and metric values.</span></span> <span data-ttu-id="b2816-106">Alınan sonra Azure SQL Database, Azure Cosmos DB ya da Azure Data Lake gibi ayrı veri deposundaki hello veri kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="b2816-106">Once retrieved, hello data can be saved in a separate data store such as Azure SQL Database, Azure Cosmos DB, or Azure Data Lake.</span></span> <span data-ttu-id="b2816-107">Buradan, gerektiği gibi ek çözümleme gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="b2816-107">From there additional analysis can be performed as needed.</span></span>

<span data-ttu-id="b2816-108">Bu makalede gösterdiği gibi çeşitli ölçüm veri noktaları ile çalışma yanı sıra hello İzleyici API olası toolist uyarı kuralları, etkinlik günlüklerini görüntüle ve çok daha kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="b2816-108">Besides working with various metric data points, as this article demonstrates, hello Monitor API makes it possible toolist alert rules, view activity logs, and much more.</span></span> <span data-ttu-id="b2816-109">Merhaba kullanılabilir işlemleri tam bir listesi için bkz [Microsoft Azure İzleyici REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2816-109">For a full list of available operations, see hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

## <a name="authenticating-azure-monitor-requests"></a><span data-ttu-id="b2816-110">Azure İzleyici istekleri kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="b2816-110">Authenticating Azure Monitor Requests</span></span>
<span data-ttu-id="b2816-111">Merhaba ilk adım, tooauthenticate hello isteğidir.</span><span class="sxs-lookup"><span data-stu-id="b2816-111">hello first step is tooauthenticate hello request.</span></span>

<span data-ttu-id="b2816-112">Hello Azure İzleyici API kullanımı hello Azure Resource Manager kimlik doğrulama modeli karşı yürütülen tüm hello görevler.</span><span class="sxs-lookup"><span data-stu-id="b2816-112">All hello tasks executed against hello Azure Monitor API use hello Azure Resource Manager authentication model.</span></span> <span data-ttu-id="b2816-113">Bu nedenle, tüm istekleri Azure Active Directory (Azure AD) ile kimlik doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2816-113">Therefore, all requests must be authenticated with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="b2816-114">Bir yaklaşım tooauthenticate hello istemci uygulamanın toocreate bir Azure AD hizmet sorumlusu ve hello (JWT) kimlik doğrulama belirtecini almak.</span><span class="sxs-lookup"><span data-stu-id="b2816-114">One approach tooauthenticate hello client application is toocreate an Azure AD service principal and retrieve hello authentication (JWT) token.</span></span> <span data-ttu-id="b2816-115">Merhaba aşağıdaki örnek komut dosyası Azure AD hizmet sorumlusu PowerShell aracılığıyla oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b2816-115">hello following sample script demonstrates creating an Azure AD service principal via PowerShell.</span></span> <span data-ttu-id="b2816-116">Daha ayrıntılı bir kılavuz için üzerinde toohello belgelerine başvurun. [bir hizmet asıl tooaccess kaynakları Azure PowerShell toocreate kullanarak](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span><span class="sxs-lookup"><span data-stu-id="b2816-116">For a more detailed walk-through, refer toohello documentation on [using Azure PowerShell toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span></span> <span data-ttu-id="b2816-117">Ayrıca çok mümkündür[hello Azure portal aracılığıyla bir hizmet sorumlusu oluşturma](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b2816-117">It is also possible too[create a service principal via hello Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

```PowerShell
$subscriptionId = "{azure-subscription-id}"
$resourceGroupName = "{resource-group-name}"
$location = "centralus"

# Authenticate tooa specific Azure subscription.
Login-AzureRmAccount -SubscriptionId $subscriptionId

# Password for hello service principal
$pwd = "{service-principal-password}"

# Create a new Azure AD application
$azureAdApplication = New-AzureRmADApplication `
                        -DisplayName "My Azure Monitor" `
                        -HomePage "https://localhost/azure-monitor" `
                        -IdentifierUris "https://localhost/azure-monitor" `
                        -Password $pwd

# Create a new service principal associated with hello designated application
New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

# Assign Reader role toohello newly created service principal
New-AzureRmRoleAssignment -RoleDefinitionName Reader `
                          -ServicePrincipalName $azureAdApplication.ApplicationId.Guid

```

<span data-ttu-id="b2816-118">tooquery hello Azure monitör API'si, Merhaba istemci uygulaması, daha önce oluşturduğunuz hizmet asıl tooauthenticate hello kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2816-118">tooquery hello Azure Monitor API, hello client application should use hello previously created service principal tooauthenticate.</span></span> <span data-ttu-id="b2816-119">Örnek PowerShell komut dosyası izleyen hello gösterir hello kullanarak bir yaklaşım [Active Directory kimlik doğrulama Kitaplığı](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp hello JWT kimlik doğrulama belirteci alın.</span><span class="sxs-lookup"><span data-stu-id="b2816-119">hello following example PowerShell script shows one approach, using hello [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp get hello JWT authentication token.</span></span> <span data-ttu-id="b2816-120">Merhaba JWT belirteci isteklerini toohello Azure İzleyici REST API HTTP yetkilendirme parametresinde bir parçası olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="b2816-120">hello JWT token is passed as part of an HTTP Authorization parameter in requests toohello Azure Monitor REST API.</span></span>

```PowerShell
$azureAdApplication = Get-AzureRmADApplication -IdentifierUri "https://localhost/azure-monitor"

$subscription = Get-AzureRmSubscription -SubscriptionId $subscriptionId

$clientId = $azureAdApplication.ApplicationId.Guid
$tenantId = $subscription.TenantId
$authUrl = "https://login.microsoftonline.com/${tenantId}"

$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl
$cred = New-Object -TypeName Microsoft.IdentityModel.Clients.ActiveDirectory.ClientCredential -ArgumentList ($clientId, $pwd)

$result = $AuthContext.AcquireToken("https://management.core.windows.net/", $cred)

# Build an array of HTTP header values
$authHeader = @{
'Content-Type'='application/json'
'Accept'='application/json'
'Authorization'=$result.CreateAuthorizationHeader()
}
```

<span data-ttu-id="b2816-121">Merhaba kimlik doğrulama Kurulumu adım tamamlandıktan sonra sorguları hello Azure İzleyici REST API'sine karşı daha sonra çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="b2816-121">Once hello authentication setup step is complete, queries can then be executed against hello Azure Monitor REST API.</span></span> <span data-ttu-id="b2816-122">İki yararlı sorgular şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b2816-122">There are two helpful queries:</span></span>

1. <span data-ttu-id="b2816-123">Bir kaynak için liste hello ölçüm tanımları</span><span class="sxs-lookup"><span data-stu-id="b2816-123">List hello metric definitions for a resource</span></span>
2. <span data-ttu-id="b2816-124">Merhaba ölçüm değerlerini alma</span><span class="sxs-lookup"><span data-stu-id="b2816-124">Retrieve hello metric values</span></span>

## <a name="retrieve-metric-definitions"></a><span data-ttu-id="b2816-125">Ölçüm tanımlarını Al</span><span class="sxs-lookup"><span data-stu-id="b2816-125">Retrieve Metric Definitions</span></span>
> [!NOTE]
> <span data-ttu-id="b2816-126">Hello Azure İzleyici REST API'sini kullanarak tooretrieve ölçüm tanımlarını API sürümü hello gibi "2016-03-01" kullanın.</span><span class="sxs-lookup"><span data-stu-id="b2816-126">tooretrieve metric definitions using hello Azure Monitor REST API, use "2016-03-01" as hello API version.</span></span>
>
>

```PowerShell
$apiVersion = "2016-03-01"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metricDefinitions?api-version=${apiVersion}"

Invoke-RestMethod -Uri $request `
                  -Headers $authHeader `
                  -Method Get `
                  -Verbose
```
<span data-ttu-id="b2816-127">Bir Azure mantıksal uygulama için aşağıdaki ekran görüntüsüne benzer toohello hello ölçüm tanımlarını görünür:</span><span class="sxs-lookup"><span data-stu-id="b2816-127">For an Azure Logic App, hello metric definitions would appear similar toohello following screenshot:</span></span>

![Alt "JSON görünüm ölçüm tanımı yanıtının."](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

<span data-ttu-id="b2816-129">Merhaba daha fazla bilgi için bkz [listesinde hello ölçüm Azure İzleyici REST API kaynak tanımlarında](https://msdn.microsoft.com/library/azure/mt743621.aspx) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="b2816-129">For more information, see hello [List hello metric definitions for a resource in Azure Monitor REST API](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentation.</span></span>

## <a name="retrieve-metric-values"></a><span data-ttu-id="b2816-130">Ölçü değerlerini alma</span><span class="sxs-lookup"><span data-stu-id="b2816-130">Retrieve Metric Values</span></span>
<span data-ttu-id="b2816-131">Merhaba kullanılabilir ölçüm tanımlarını bilinen sonra olası tooretrieve hello sonra ilgili ölçüm değerleri olan.</span><span class="sxs-lookup"><span data-stu-id="b2816-131">Once hello available metric definitions are known, it is then possible tooretrieve hello related metric values.</span></span> <span data-ttu-id="b2816-132">Merhaba ölçüm'ın ad 'değer' (değil 'localizedValue' hello) filtreleme tüm istekleri (örneğin, alma hello 'CPU zamanı' ve 'İsteklerini' Ölçüm veri noktaları) için kullanır.</span><span class="sxs-lookup"><span data-stu-id="b2816-132">Use hello metric’s name ‘value’ (not hello ‘localizedValue’) for any filtering requests (for example, retrieve hello ‘CpuTime’ and ‘Requests’ metric data points).</span></span> <span data-ttu-id="b2816-133">Hiçbir filtre belirtilirse, hello varsayılan ölçüm döndürülür.</span><span class="sxs-lookup"><span data-stu-id="b2816-133">If no filters are specified, hello default metric is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="b2816-134">Hello Azure İzleyici REST API'sini kullanarak tooretrieve ölçüm değerleri API sürümü hello gibi "2016-06-01" kullanın.</span><span class="sxs-lookup"><span data-stu-id="b2816-134">tooretrieve metric values using hello Azure Monitor REST API, use "2016-06-01" as hello API version.</span></span>
>
>

<span data-ttu-id="b2816-135">**Yöntem**: Al</span><span class="sxs-lookup"><span data-stu-id="b2816-135">**Method**: GET</span></span>

<span data-ttu-id="b2816-136">**İstek URI'si**: https://management.azure.com/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/*{ Kaynak-sağlayıcısı-namespace}*/*{kaynak türü}*/*{kaynak-adı}*/providers/microsoft.insights/metrics?$filter= *{filtre}*& api-version =*{apiVersion}*</span><span class="sxs-lookup"><span data-stu-id="b2816-136">**Request URI**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*</span></span>

<span data-ttu-id="b2816-137">Örneğin, tooretrieve hello RunsSucceeded ölçüm veri noktaları ve bir zaman çizgisi 1 saatlik, hello istek zaman aralığı verilen hello için aşağıdaki gibi olur:</span><span class="sxs-lookup"><span data-stu-id="b2816-137">For example, tooretrieve hello RunsSucceeded metric data points for hello given time range and for a time grain of 1 hour, hello request would be as follows:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

<span data-ttu-id="b2816-138">Merhaba sonuç aşağıdaki ekran görüntüsüne benzer toohello örnek görünür:</span><span class="sxs-lookup"><span data-stu-id="b2816-138">hello result would appear similar toohello example following screenshot:</span></span>

![Alt "JSON yanıt ortalama yanıt süresi ölçüm değeri gösterme"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

<span data-ttu-id="b2816-140">tooretrieve birden çok veri veya toplama noktalarını ekleyin hello ölçüm tanımı adları ve toplama türleri toohello filtre hello aşağıdaki örnekte görüldüğü gibi:</span><span class="sxs-lookup"><span data-stu-id="b2816-140">tooretrieve multiple data or aggregation points, add hello metric definition names and aggregation types toohello filter, as seen in hello following example:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a><span data-ttu-id="b2816-141">ARMClient kullanın</span><span class="sxs-lookup"><span data-stu-id="b2816-141">Use ARMClient</span></span>
<span data-ttu-id="b2816-142">Alternatif bir toousing (yukarıda gösterildiği gibi) PowerShell olan toouse [ARMClient](https://github.com/projectkudu/ARMClient) Windows makinenizde.</span><span class="sxs-lookup"><span data-stu-id="b2816-142">An alternative toousing PowerShell (as shown above), is toouse [ARMClient](https://github.com/projectkudu/ARMClient) on your Windows machine.</span></span> <span data-ttu-id="b2816-143">ARMClient hello Azure AD kimlik doğrulama (ve sonuçta elde edilen JWT belirteci) otomatik olarak yönetir.</span><span class="sxs-lookup"><span data-stu-id="b2816-143">ARMClient handles hello Azure AD authentication (and resulting JWT token) automatically.</span></span> <span data-ttu-id="b2816-144">Merhaba aşağıdaki adımları ölçüm verilerini alma ARMClient kullanımını özetlemektedir:</span><span class="sxs-lookup"><span data-stu-id="b2816-144">hello following steps outline use of ARMClient for retrieving metric data:</span></span>

1. <span data-ttu-id="b2816-145">Yükleme [Chocolatey](https://chocolatey.org/) ve [ARMClient](https://github.com/projectkudu/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="b2816-145">Install [Chocolatey](https://chocolatey.org/) and [ARMClient](https://github.com/projectkudu/ARMClient).</span></span>
2. <span data-ttu-id="b2816-146">Bir terminal penceresi yazın *armclient.exe oturum açma*.</span><span class="sxs-lookup"><span data-stu-id="b2816-146">In a terminal window, type *armclient.exe login*.</span></span> <span data-ttu-id="b2816-147">Bu tooAzure toolog ister.</span><span class="sxs-lookup"><span data-stu-id="b2816-147">This prompts you toolog in tooAzure.</span></span>
3. <span data-ttu-id="b2816-148">Tür *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span><span class="sxs-lookup"><span data-stu-id="b2816-148">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span></span>
4. <span data-ttu-id="b2816-149">Tür *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span><span class="sxs-lookup"><span data-stu-id="b2816-149">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span></span>

![Alt "Merhaba Azure Monitoring REST API ile kullanma ARMClient toowork"](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a><span data-ttu-id="b2816-151">Merhaba kaynak kimliği alma</span><span class="sxs-lookup"><span data-stu-id="b2816-151">Retrieve hello Resource ID</span></span>
<span data-ttu-id="b2816-152">Merhaba REST API kullanarak gerçekten toounderstand hello kullanılabilir ölçüm tanımlarını, ayrıntı düzeyi ve ilgili değerleri yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b2816-152">Using hello REST API can really help toounderstand hello available metric definitions, granularity, and related values.</span></span> <span data-ttu-id="b2816-153">Bu bilgileri hello kullanırken faydalıdır [Azure Yönetimi Kitaplığı](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2816-153">That information is helpful when using hello [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>

<span data-ttu-id="b2816-154">Kod önceki hello için Azure kaynak hello tam yolu toohello istenen hello kaynak kimliği toouse olur.</span><span class="sxs-lookup"><span data-stu-id="b2816-154">For hello preceding code, hello resource ID toouse is hello full path toohello desired Azure resource.</span></span> <span data-ttu-id="b2816-155">Örneğin, tooquery Azure Web uygulaması karşı hello kaynak kimliği olur:</span><span class="sxs-lookup"><span data-stu-id="b2816-155">For example, tooquery against an Azure Web App, hello resource ID would be:</span></span>

<span data-ttu-id="b2816-156">*/Subscriptions/{Subscription-id}/resourceGroups/{Resource-Group-Name}/providers/Microsoft.Web/Sites/{Site-Name}/*</span><span class="sxs-lookup"><span data-stu-id="b2816-156">*/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*</span></span>

<span data-ttu-id="b2816-157">Merhaba aşağıda birkaç örnek çeşitli Azure kaynakları için kaynak kimliği biçimlerinden içerir:</span><span class="sxs-lookup"><span data-stu-id="b2816-157">hello following list contains a few examples of resource ID formats for various Azure resources:</span></span>

* <span data-ttu-id="b2816-158">**IOT hub'ı** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-adı}*</span><span class="sxs-lookup"><span data-stu-id="b2816-158">**IoT Hub** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span></span>
* <span data-ttu-id="b2816-159">**SQL esnek havuzu** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Sql/servers/*{havuzu-db}*/elasticpools/*{sql-havuzu-adı}*</span><span class="sxs-lookup"><span data-stu-id="b2816-159">**Elastic SQL Pool** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span></span>
* <span data-ttu-id="b2816-160">**SQL veritabanı (v12)** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Sql/servers/*{sunucu-adı} */databases/*{veritabanı-adı}*</span><span class="sxs-lookup"><span data-stu-id="b2816-160">**SQL Database (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*</span></span>
* <span data-ttu-id="b2816-161">**Hizmet veri yolu** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.ServiceBus/*{ad}* / *{servicebus-adı}*</span><span class="sxs-lookup"><span data-stu-id="b2816-161">**Service Bus** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*</span></span>
* <span data-ttu-id="b2816-162">**VM ölçek kümesi** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{ VM-adı}*</span><span class="sxs-lookup"><span data-stu-id="b2816-162">**VM Scale Sets** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*</span></span>
* <span data-ttu-id="b2816-163">**Sanal makineleri** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Compute/virtualMachines/*{vm-adı}*</span><span class="sxs-lookup"><span data-stu-id="b2816-163">**VMs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*</span></span>
* <span data-ttu-id="b2816-164">**Olay hub'ları** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.EventHub/namespaces/*{ eventhub-namespace}*</span><span class="sxs-lookup"><span data-stu-id="b2816-164">**Event Hubs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*</span></span>

<span data-ttu-id="b2816-165">Azure kaynak Gezgini, istenen hello kaynak hello Azure portal ve PowerShell veya hello Azure CLI aracılığıyla görüntüleme kullanımı dahil olmak üzere çeşitli yaklaşımlar tooretrieving hello kaynak kimliği vardır.</span><span class="sxs-lookup"><span data-stu-id="b2816-165">There are alternative approaches tooretrieving hello resource ID, including using Azure Resource Explorer, viewing hello desired resource in hello Azure portal, and via PowerShell or hello Azure CLI.</span></span>

### <a name="azure-resource-explorer"></a><span data-ttu-id="b2816-166">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b2816-166">Azure Resource Explorer</span></span>
<span data-ttu-id="b2816-167">İstenen kaynak, bir yardımcı yaklaşım için toofind hello kaynak kimliği olan toouse hello [Azure kaynak Gezgini](https://resources.azure.com) aracı.</span><span class="sxs-lookup"><span data-stu-id="b2816-167">toofind hello resource ID for a desired resource, one helpful approach is toouse hello [Azure Resource Explorer](https://resources.azure.com) tool.</span></span> <span data-ttu-id="b2816-168">İstenen toohello kaynak gidin ve ardından, aşağıdaki ekran görüntüsü hello olduğu gibi gösterilen hello kimliği bakın:</span><span class="sxs-lookup"><span data-stu-id="b2816-168">Navigate toohello desired resource and then look at hello ID shown, as in hello following screenshot:</span></span>

![Alt "Azure kaynak Gezgini"](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a><span data-ttu-id="b2816-170">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="b2816-170">Azure portal</span></span>
<span data-ttu-id="b2816-171">Hello kaynak kimliği de Azure portal hello elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="b2816-171">hello resource ID can also be obtained from hello Azure portal.</span></span> <span data-ttu-id="b2816-172">Bu nedenle, toodo toohello istenen kaynak gidin ve ardından Özellikler'i seçin.</span><span class="sxs-lookup"><span data-stu-id="b2816-172">toodo so, navigate toohello desired resource and then select Properties.</span></span> <span data-ttu-id="b2816-173">Merhaba kaynak kimliği hello özellikleri dikey penceresinde, aşağıdaki ekran görüntüsü hello görülen görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="b2816-173">hello Resource ID is displayed in hello Properties blade, as seen in hello following screenshot:</span></span>

!["Hello özellikleri dikey penceresinde hello Azure portalında görüntülenen alt kaynak kimliği"](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a><span data-ttu-id="b2816-175">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2816-175">Azure PowerShell</span></span>
<span data-ttu-id="b2816-176">Merhaba kaynak kimliği, Azure PowerShell cmdlet'leri kullanılarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="b2816-176">hello resource ID can be retrieved using Azure PowerShell cmdlets as well.</span></span> <span data-ttu-id="b2816-177">Örneğin, bir Azure Web uygulaması için tooobtain hello kaynak kimliği ekran aşağıdaki hello olduğu gibi hello Get-AzureRmWebApp cmdlet'ini yürütün:</span><span class="sxs-lookup"><span data-stu-id="b2816-177">For example, tooobtain hello resource ID for an Azure Web App, execute hello Get-AzureRmWebApp cmdlet, as in hello following screenshot:</span></span>

!["PowerShell elde alt kaynak kimliği"](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a><span data-ttu-id="b2816-179">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b2816-179">Azure CLI</span></span>
<span data-ttu-id="b2816-180">tooretrieve hello Azure CLI kullanarak kaynak kimliği Merhaba, hello belirtme hello 'azure webapp Göster' komutunu yürütün '--json' hello ekran aşağıdaki gösterildiği gibi seçeneği:</span><span class="sxs-lookup"><span data-stu-id="b2816-180">tooretrieve hello resource ID using hello Azure CLI, execute hello 'azure webapp show' command, specifying hello '--json' option, as shown in hello following screenshot:</span></span>

!["PowerShell elde alt kaynak kimliği"](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a><span data-ttu-id="b2816-182">Etkinlik günlüğü verilerini alma</span><span class="sxs-lookup"><span data-stu-id="b2816-182">Retrieve Activity Log Data</span></span>
<span data-ttu-id="b2816-183">Ölçüm tanımlarını ve ilgili değerleri toplama tooworking içinde olası tooretrieve ek ilginç Öngörüler ilgili tooAzure kaynaklar da sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2816-183">In addition tooworking with metric definitions and related values, it is also possible tooretrieve additional interesting insights related tooAzure resources.</span></span> <span data-ttu-id="b2816-184">İsteğe bağlı olarak örnek olarak, olası tooquery olan [etkinlik günlüğü](https://msdn.microsoft.com/library/azure/dn931934.aspx) veri.</span><span class="sxs-lookup"><span data-stu-id="b2816-184">As an example, it is possible tooquery [activity log](https://msdn.microsoft.com/library/azure/dn931934.aspx) data.</span></span> <span data-ttu-id="b2816-185">Merhaba aşağıdaki örnek hello Azure İzleyici REST API tooquery etkinlik günlüğü verileri belirli bir tarih aralığı içinde bir Azure aboneliği için kullanma gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="b2816-185">hello following sample demonstrates using hello Azure Monitor REST API tooquery activity log data within a specific date range for an Azure subscription:</span></span>

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a><span data-ttu-id="b2816-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b2816-186">Next steps</span></span>
* <span data-ttu-id="b2816-187">Gözden geçirme hello [genel bakış izleme](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b2816-187">Review hello [Overview of Monitoring](monitoring-overview.md).</span></span>
* <span data-ttu-id="b2816-188">Görünüm hello [desteklenen Azure İzleyicisi ile ölçümleri](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="b2816-188">View hello [Supported metrics with Azure Monitor](monitoring-supported-metrics.md).</span></span>
* <span data-ttu-id="b2816-189">Gözden geçirme hello [Microsoft Azure İzleyici REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2816-189">Review hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>
* <span data-ttu-id="b2816-190">Gözden geçirme hello [Azure Yönetimi Kitaplığı](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2816-190">Review hello [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>
