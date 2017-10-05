---
title: REST API izlenecek izleme azure | Microsoft Docs
description: "Nasıl isteklerine kimlik doğrulaması ve Azure izleme REST API'sini kullanın."
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
ms.openlocfilehash: 454a85c4752ec9c7522ef147d5ce594ef5992c32
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-monitoring-rest-api-walkthrough"></a><span data-ttu-id="08cd3-103">REST API izlenecek izleme azure</span><span class="sxs-lookup"><span data-stu-id="08cd3-103">Azure Monitoring REST API Walkthrough</span></span>
<span data-ttu-id="08cd3-104">Bu makalede, kodunuzu kullanabilmeniz için kimlik doğrulaması yapmak gösterilmiştir [Microsoft Azure İzleyici REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="08cd3-104">This article shows you how to perform authentication so your code can use the [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>         

<span data-ttu-id="08cd3-105">Azure İzleyici API program aracılığıyla kullanılabilir varsayılan ölçüm tanımlarını (CPU süresi, istekleri, vb. gibi ölçüm türü), ayrıntı düzeyi ve ölçüm değerleri almak mümkün kılar.</span><span class="sxs-lookup"><span data-stu-id="08cd3-105">The Azure Monitor API makes it possible to programmatically retrieve the available default metric definitions (the type of metric such as CPU Time, Requests, etc.), granularity, and metric values.</span></span> <span data-ttu-id="08cd3-106">Alınan sonra verileri Azure SQL Database, Azure Cosmos DB ya da Azure Data Lake gibi ayrı veri deposundaki kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="08cd3-106">Once retrieved, the data can be saved in a separate data store such as Azure SQL Database, Azure Cosmos DB, or Azure Data Lake.</span></span> <span data-ttu-id="08cd3-107">Buradan, gerektiği gibi ek çözümleme gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="08cd3-107">From there additional analysis can be performed as needed.</span></span>

<span data-ttu-id="08cd3-108">Bu makalede gösterdiği gibi çeşitli ölçüm veri noktaları ile çalışma yanı sıra, monitör API'si, uyarı kuralları, etkinlik günlükleri görüntüle ve daha fazlasını listelemek mümkün kılar.</span><span class="sxs-lookup"><span data-stu-id="08cd3-108">Besides working with various metric data points, as this article demonstrates, the Monitor API makes it possible to list alert rules, view activity logs, and much more.</span></span> <span data-ttu-id="08cd3-109">Kullanılabilir işlemleri tam bir listesi için bkz: [Microsoft Azure İzleyici REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="08cd3-109">For a full list of available operations, see the [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

## <a name="authenticating-azure-monitor-requests"></a><span data-ttu-id="08cd3-110">Azure İzleyici istekleri kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="08cd3-110">Authenticating Azure Monitor Requests</span></span>
<span data-ttu-id="08cd3-111">İlk istek kimliğini doğrulamak için bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="08cd3-111">The first step is to authenticate the request.</span></span>

<span data-ttu-id="08cd3-112">Azure İzleyici API karşı yürütülen tüm görevler Azure Resource Manager kimlik doğrulama modeli kullanır.</span><span class="sxs-lookup"><span data-stu-id="08cd3-112">All the tasks executed against the Azure Monitor API use the Azure Resource Manager authentication model.</span></span> <span data-ttu-id="08cd3-113">Bu nedenle, tüm istekleri Azure Active Directory (Azure AD) ile kimlik doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="08cd3-113">Therefore, all requests must be authenticated with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="08cd3-114">İstemci uygulaması kimliğini doğrulamak için bir Azure AD hizmet sorumlusu oluşturmak ve kimlik doğrulama (JWT) belirteci almak için bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="08cd3-114">One approach to authenticate the client application is to create an Azure AD service principal and retrieve the authentication (JWT) token.</span></span> <span data-ttu-id="08cd3-115">Aşağıdaki örnek betik, bir Azure AD hizmeti PowerShell aracılığıyla asıl oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="08cd3-115">The following sample script demonstrates creating an Azure AD service principal via PowerShell.</span></span> <span data-ttu-id="08cd3-116">Üzerinde daha ayrıntılı bir kılavuz için belgelere bakın [kaynaklara erişmek için bir hizmet sorumlusu oluşturmak için Azure PowerShell kullanarak](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span><span class="sxs-lookup"><span data-stu-id="08cd3-116">For a more detailed walk-through, refer to the documentation on [using Azure PowerShell to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span></span> <span data-ttu-id="08cd3-117">Ayrıca mümkün [Azure Portalı aracılığıyla hizmet sorumlusu oluşturmak](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="08cd3-117">It is also possible to [create a service principal via the Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

```PowerShell
$subscriptionId = "{azure-subscription-id}"
$resourceGroupName = "{resource-group-name}"
$location = "centralus"

# Authenticate to a specific Azure subscription.
Login-AzureRmAccount -SubscriptionId $subscriptionId

# Password for the service principal
$pwd = "{service-principal-password}"

# Create a new Azure AD application
$azureAdApplication = New-AzureRmADApplication `
                        -DisplayName "My Azure Monitor" `
                        -HomePage "https://localhost/azure-monitor" `
                        -IdentifierUris "https://localhost/azure-monitor" `
                        -Password $pwd

# Create a new service principal associated with the designated application
New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

# Assign Reader role to the newly created service principal
New-AzureRmRoleAssignment -RoleDefinitionName Reader `
                          -ServicePrincipalName $azureAdApplication.ApplicationId.Guid

```

<span data-ttu-id="08cd3-118">Azure İzleyici API sorgulamak için istemci uygulamasının daha önce oluşturulan hizmet asıl kimlik doğrulaması için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="08cd3-118">To query the Azure Monitor API, the client application should use the previously created service principal to authenticate.</span></span> <span data-ttu-id="08cd3-119">Aşağıdaki örnek PowerShell komut dosyasını bir gösterir yaklaşımını kullanarak [Active Directory kimlik doğrulama Kitaplığı](../active-directory/active-directory-authentication-libraries.md) JWT kimlik doğrulama belirteci alma yardımcı olmak için (ADAL).</span><span class="sxs-lookup"><span data-stu-id="08cd3-119">The following example PowerShell script shows one approach, using the [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) to help get the JWT authentication token.</span></span> <span data-ttu-id="08cd3-120">JWT belirteci Azure İzleyici REST API istekleri HTTP yetkilendirme parametresinde bir parçası olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="08cd3-120">The JWT token is passed as part of an HTTP Authorization parameter in requests to the Azure Monitor REST API.</span></span>

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

<span data-ttu-id="08cd3-121">Kimlik Doğrulama kurulumu adım tamamlandıktan sonra sorguları karşı Azure İzleyici REST API sonra çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="08cd3-121">Once the authentication setup step is complete, queries can then be executed against the Azure Monitor REST API.</span></span> <span data-ttu-id="08cd3-122">İki yararlı sorgular şunlardır:</span><span class="sxs-lookup"><span data-stu-id="08cd3-122">There are two helpful queries:</span></span>

1. <span data-ttu-id="08cd3-123">Bir kaynak için ölçüm açıklamalarının listesi</span><span class="sxs-lookup"><span data-stu-id="08cd3-123">List the metric definitions for a resource</span></span>
2. <span data-ttu-id="08cd3-124">Ölçü değerlerini alma</span><span class="sxs-lookup"><span data-stu-id="08cd3-124">Retrieve the metric values</span></span>

## <a name="retrieve-metric-definitions"></a><span data-ttu-id="08cd3-125">Ölçüm tanımlarını Al</span><span class="sxs-lookup"><span data-stu-id="08cd3-125">Retrieve Metric Definitions</span></span>
> [!NOTE]
> <span data-ttu-id="08cd3-126">Azure İzleyici REST API'sini kullanarak ölçüm tanımlarını almak için "2016-03-01" API sürümü kullanın.</span><span class="sxs-lookup"><span data-stu-id="08cd3-126">To retrieve metric definitions using the Azure Monitor REST API, use "2016-03-01" as the API version.</span></span>
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
<span data-ttu-id="08cd3-127">Bir Azure mantıksal uygulama için ölçüm tanımlarını aşağıdaki ekran görüntüsüne benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="08cd3-127">For an Azure Logic App, the metric definitions would appear similar to the following screenshot:</span></span>

![Alt "JSON görünüm ölçüm tanımı yanıtının."](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

<span data-ttu-id="08cd3-129">Daha fazla bilgi için bkz: [Azure İzleyici REST API kaynak ölçüm tanımlarını listesinde](https://msdn.microsoft.com/library/azure/mt743621.aspx) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="08cd3-129">For more information, see the [List the metric definitions for a resource in Azure Monitor REST API](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentation.</span></span>

## <a name="retrieve-metric-values"></a><span data-ttu-id="08cd3-130">Ölçü değerlerini alma</span><span class="sxs-lookup"><span data-stu-id="08cd3-130">Retrieve Metric Values</span></span>
<span data-ttu-id="08cd3-131">Kullanılabilir ölçüm tanımlarını bilinen sonra ardından ilgili ölçüm değerleri almak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="08cd3-131">Once the available metric definitions are known, it is then possible to retrieve the related metric values.</span></span> <span data-ttu-id="08cd3-132">Filtreleme tüm istekler için ölçüm kişinin adı 'value' (değil ' localizedValue') kullanın (örneğin, 'CPU zamanı' ve 'İsteklerini' Ölçüm veri noktalarını almaya).</span><span class="sxs-lookup"><span data-stu-id="08cd3-132">Use the metric’s name ‘value’ (not the ‘localizedValue’) for any filtering requests (for example, retrieve the ‘CpuTime’ and ‘Requests’ metric data points).</span></span> <span data-ttu-id="08cd3-133">Hiçbir filtre belirtilmezse, varsayılan ölçü döndürülür.</span><span class="sxs-lookup"><span data-stu-id="08cd3-133">If no filters are specified, the default metric is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="08cd3-134">Azure İzleyici REST API'sini kullanarak ölçüm değerleri almak için "2016-06-01" API sürümü kullanın.</span><span class="sxs-lookup"><span data-stu-id="08cd3-134">To retrieve metric values using the Azure Monitor REST API, use "2016-06-01" as the API version.</span></span>
>
>

<span data-ttu-id="08cd3-135">**Yöntem**: Al</span><span class="sxs-lookup"><span data-stu-id="08cd3-135">**Method**: GET</span></span>

<span data-ttu-id="08cd3-136">**İstek URI'si**: https://management.azure.com/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/*{ Kaynak-sağlayıcısı-namespace}*/*{kaynak türü}*/*{kaynak-adı}*/providers/microsoft.insights/metrics?$filter= *{filtre}*& api-version =*{apiVersion}*</span><span class="sxs-lookup"><span data-stu-id="08cd3-136">**Request URI**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*</span></span>

<span data-ttu-id="08cd3-137">Örneğin, 1 saatlik bir zaman çizgisi ve belirli bir zaman aralığı için RunsSucceeded ölçüm veri noktalarını almak için isteği aşağıdaki gibi olur:</span><span class="sxs-lookup"><span data-stu-id="08cd3-137">For example, to retrieve the RunsSucceeded metric data points for the given time range and for a time grain of 1 hour, the request would be as follows:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

<span data-ttu-id="08cd3-138">Sonuç ekran aşağıdaki örneğe benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="08cd3-138">The result would appear similar to the example following screenshot:</span></span>

![Alt "JSON yanıt ortalama yanıt süresi ölçüm değeri gösterme"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

<span data-ttu-id="08cd3-140">Birden çok veri veya toplama noktası almak için ölçüm tanımı adları ve toplama türleri filtre için aşağıdaki örnekte görüldüğü gibi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="08cd3-140">To retrieve multiple data or aggregation points, add the metric definition names and aggregation types to the filter, as seen in the following example:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a><span data-ttu-id="08cd3-141">ARMClient kullanın</span><span class="sxs-lookup"><span data-stu-id="08cd3-141">Use ARMClient</span></span>
<span data-ttu-id="08cd3-142">(Yukarıda gösterildiği gibi) PowerShell kullanarak alternatif kullanmaktır [ARMClient](https://github.com/projectkudu/ARMClient) Windows makinenizde.</span><span class="sxs-lookup"><span data-stu-id="08cd3-142">An alternative to using PowerShell (as shown above), is to use [ARMClient](https://github.com/projectkudu/ARMClient) on your Windows machine.</span></span> <span data-ttu-id="08cd3-143">ARMClient Azure AD kimlik doğrulaması (ve sonuçta elde edilen JWT belirteci) otomatik olarak yönetir.</span><span class="sxs-lookup"><span data-stu-id="08cd3-143">ARMClient handles the Azure AD authentication (and resulting JWT token) automatically.</span></span> <span data-ttu-id="08cd3-144">ARMClient kullanımını ölçüm verileri almak için aşağıdaki adımları özetlemektedir:</span><span class="sxs-lookup"><span data-stu-id="08cd3-144">The following steps outline use of ARMClient for retrieving metric data:</span></span>

1. <span data-ttu-id="08cd3-145">Yükleme [Chocolatey](https://chocolatey.org/) ve [ARMClient](https://github.com/projectkudu/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="08cd3-145">Install [Chocolatey](https://chocolatey.org/) and [ARMClient](https://github.com/projectkudu/ARMClient).</span></span>
2. <span data-ttu-id="08cd3-146">Bir terminal penceresi yazın *armclient.exe oturum açma*.</span><span class="sxs-lookup"><span data-stu-id="08cd3-146">In a terminal window, type *armclient.exe login*.</span></span> <span data-ttu-id="08cd3-147">Azure'da oturum açma ister.</span><span class="sxs-lookup"><span data-stu-id="08cd3-147">This prompts you to log in to Azure.</span></span>
3. <span data-ttu-id="08cd3-148">Tür *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span><span class="sxs-lookup"><span data-stu-id="08cd3-148">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span></span>
4. <span data-ttu-id="08cd3-149">Tür *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span><span class="sxs-lookup"><span data-stu-id="08cd3-149">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span></span>

![Alt "Azure Monitoring REST API'si ile çalışmaya kullanma ARMClient"](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-the-resource-id"></a><span data-ttu-id="08cd3-151">Kaynak Kimliği alma</span><span class="sxs-lookup"><span data-stu-id="08cd3-151">Retrieve the Resource ID</span></span>
<span data-ttu-id="08cd3-152">REST API kullanarak gerçekten kullanılabilir ölçüm tanımlarını, ayrıntı düzeyi ve ilgili değerleri anlamanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="08cd3-152">Using the REST API can really help to understand the available metric definitions, granularity, and related values.</span></span> <span data-ttu-id="08cd3-153">Bilgi kullanıldığında yararlı olduğunu [Azure Yönetimi Kitaplığı](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="08cd3-153">That information is helpful when using the [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>

<span data-ttu-id="08cd3-154">Önceki kod için kullanılacak kaynak kimliği istenen Azure kaynak tam yoludur.</span><span class="sxs-lookup"><span data-stu-id="08cd3-154">For the preceding code, the resource ID to use is the full path to the desired Azure resource.</span></span> <span data-ttu-id="08cd3-155">Örneğin, bir Azure Web uygulaması karşı sorgulamak için kaynak kimliği olur:</span><span class="sxs-lookup"><span data-stu-id="08cd3-155">For example, to query against an Azure Web App, the resource ID would be:</span></span>

<span data-ttu-id="08cd3-156">*/Subscriptions/{Subscription-id}/resourceGroups/{Resource-Group-Name}/providers/Microsoft.Web/Sites/{Site-Name}/*</span><span class="sxs-lookup"><span data-stu-id="08cd3-156">*/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*</span></span>

<span data-ttu-id="08cd3-157">Aşağıdaki listede kaynak kimliği biçimlerinden çeşitli Azure kaynakları için birkaç örnek içerir:</span><span class="sxs-lookup"><span data-stu-id="08cd3-157">The following list contains a few examples of resource ID formats for various Azure resources:</span></span>

* <span data-ttu-id="08cd3-158">**IOT hub'ı** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-adı}*</span><span class="sxs-lookup"><span data-stu-id="08cd3-158">**IoT Hub** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span></span>
* <span data-ttu-id="08cd3-159">**SQL esnek havuzu** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Sql/servers/*{havuzu-db}*/elasticpools/*{sql-havuzu-adı}*</span><span class="sxs-lookup"><span data-stu-id="08cd3-159">**Elastic SQL Pool** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span></span>
* <span data-ttu-id="08cd3-160">**SQL veritabanı (v12)** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Sql/servers/*{sunucu-adı}* /databases/*{veritabanı-adı}*</span><span class="sxs-lookup"><span data-stu-id="08cd3-160">**SQL Database (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*</span></span>
* <span data-ttu-id="08cd3-161">**Hizmet veri yolu** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.ServiceBus/*{ad}* / *{servicebus-adı}*</span><span class="sxs-lookup"><span data-stu-id="08cd3-161">**Service Bus** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*</span></span>
* <span data-ttu-id="08cd3-162">**VM ölçek kümesi** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{ VM-adı}*</span><span class="sxs-lookup"><span data-stu-id="08cd3-162">**VM Scale Sets** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*</span></span>
* <span data-ttu-id="08cd3-163">**Sanal makineleri** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Compute/virtualMachines/*{vm-adı}*</span><span class="sxs-lookup"><span data-stu-id="08cd3-163">**VMs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*</span></span>
* <span data-ttu-id="08cd3-164">**Olay hub'ları** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.EventHub/namespaces/*{ eventhub-namespace}*</span><span class="sxs-lookup"><span data-stu-id="08cd3-164">**Event Hubs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*</span></span>

<span data-ttu-id="08cd3-165">Azure kaynak Gezgini, istenen kaynak Azure portalında ve PowerShell veya Azure CLI aracılığıyla görüntüleme kullanımı dahil olmak üzere kaynak kimliği alma için alternatif bir yaklaşım vardır.</span><span class="sxs-lookup"><span data-stu-id="08cd3-165">There are alternative approaches to retrieving the resource ID, including using Azure Resource Explorer, viewing the desired resource in the Azure portal, and via PowerShell or the Azure CLI.</span></span>

### <a name="azure-resource-explorer"></a><span data-ttu-id="08cd3-166">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="08cd3-166">Azure Resource Explorer</span></span>
<span data-ttu-id="08cd3-167">İstenen kaynak için kaynak Kimliğini bulmak için kullanmak için yararlı bir yaklaşım ise [Azure kaynak Gezgini](https://resources.azure.com) aracı.</span><span class="sxs-lookup"><span data-stu-id="08cd3-167">To find the resource ID for a desired resource, one helpful approach is to use the [Azure Resource Explorer](https://resources.azure.com) tool.</span></span> <span data-ttu-id="08cd3-168">İstenen kaynağa gidin ve ardından, olduğu gibi aşağıdaki ekran görüntüsünde gösterilen tanıtıcı bakın:</span><span class="sxs-lookup"><span data-stu-id="08cd3-168">Navigate to the desired resource and then look at the ID shown, as in the following screenshot:</span></span>

![Alt "Azure kaynak Gezgini"](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a><span data-ttu-id="08cd3-170">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="08cd3-170">Azure portal</span></span>
<span data-ttu-id="08cd3-171">Kaynak Kimliği de Azure portalından elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="08cd3-171">The resource ID can also be obtained from the Azure portal.</span></span> <span data-ttu-id="08cd3-172">Bunu yapmak için istenen kaynağa gidin ve ardından Özellikler'i seçin.</span><span class="sxs-lookup"><span data-stu-id="08cd3-172">To do so, navigate to the desired resource and then select Properties.</span></span> <span data-ttu-id="08cd3-173">Kaynak Kimliği özellikleri dikey penceresinde, aşağıdaki ekran görüntüsünde görülen görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="08cd3-173">The Resource ID is displayed in the Properties blade, as seen in the following screenshot:</span></span>

!["Alt kaynak kimliği özellikleri dikey penceresinde Azure portalında görüntülenen"](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a><span data-ttu-id="08cd3-175">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="08cd3-175">Azure PowerShell</span></span>
<span data-ttu-id="08cd3-176">Kaynak Kimliği, Azure PowerShell cmdlet'leri kullanılarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="08cd3-176">The resource ID can be retrieved using Azure PowerShell cmdlets as well.</span></span> <span data-ttu-id="08cd3-177">Örneğin, bir Azure Web uygulaması için kaynak Kimliğini almak için aşağıdaki ekran görüntüsünde olduğu gibi Get-AzureRmWebApp cmdlet'ini yürütün:</span><span class="sxs-lookup"><span data-stu-id="08cd3-177">For example, to obtain the resource ID for an Azure Web App, execute the Get-AzureRmWebApp cmdlet, as in the following screenshot:</span></span>

!["PowerShell elde alt kaynak kimliği"](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a><span data-ttu-id="08cd3-179">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="08cd3-179">Azure CLI</span></span>
<span data-ttu-id="08cd3-180">Azure CLI kullanarak kaynak kimliği almak için 'azure webapp Göster' komutunu yürütün belirtme '--json' seçeneği, aşağıdaki ekran görüntüsünde gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="08cd3-180">To retrieve the resource ID using the Azure CLI, execute the 'azure webapp show' command, specifying the '--json' option, as shown in the following screenshot:</span></span>

!["PowerShell elde alt kaynak kimliği"](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a><span data-ttu-id="08cd3-182">Etkinlik günlüğü verilerini alma</span><span class="sxs-lookup"><span data-stu-id="08cd3-182">Retrieve Activity Log Data</span></span>
<span data-ttu-id="08cd3-183">Ölçüm tanımlarını ve ilgili değerleri ile çalışma ek olarak, ayrıca Azure kaynaklarla ilgili ek ilginç Öngörüler almak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="08cd3-183">In addition to working with metric definitions and related values, it is also possible to retrieve additional interesting insights related to Azure resources.</span></span> <span data-ttu-id="08cd3-184">Örnek olarak, sorguyu mümkündür [etkinlik günlüğü](https://msdn.microsoft.com/library/azure/dn931934.aspx) veri.</span><span class="sxs-lookup"><span data-stu-id="08cd3-184">As an example, it is possible to query [activity log](https://msdn.microsoft.com/library/azure/dn931934.aspx) data.</span></span> <span data-ttu-id="08cd3-185">Aşağıdaki örnek, Azure aboneliği için sorgu etkinlik günlüğü verileri belirli bir tarih aralığı içinde Azure İzleyici REST API'sini kullanarak gösterir:</span><span class="sxs-lookup"><span data-stu-id="08cd3-185">The following sample demonstrates using the Azure Monitor REST API to query activity log data within a specific date range for an Azure subscription:</span></span>

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a><span data-ttu-id="08cd3-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="08cd3-186">Next steps</span></span>
* <span data-ttu-id="08cd3-187">Gözden geçirme [izleme genel bakış](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="08cd3-187">Review the [Overview of Monitoring](monitoring-overview.md).</span></span>
* <span data-ttu-id="08cd3-188">Görünüm [desteklenen Azure İzleyicisi ile ölçümleri](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="08cd3-188">View the [Supported metrics with Azure Monitor](monitoring-supported-metrics.md).</span></span>
* <span data-ttu-id="08cd3-189">Gözden geçirme [Microsoft Azure izlemek REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="08cd3-189">Review the [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>
* <span data-ttu-id="08cd3-190">Gözden geçirme [Azure Yönetimi Kitaplığı](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="08cd3-190">Review the [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>
