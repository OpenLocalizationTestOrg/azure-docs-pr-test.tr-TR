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
# <a name="azure-monitoring-rest-api-walkthrough"></a>REST API izlenecek izleme azure
Bu makalede, kodunuzu kullanabilmeniz için kimlik doğrulaması yapmak gösterilmiştir [Microsoft Azure İzleyici REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn931943.aspx).         

Azure İzleyici API program aracılığıyla kullanılabilir varsayılan ölçüm tanımlarını (CPU süresi, istekleri, vb. gibi ölçüm türü), ayrıntı düzeyi ve ölçüm değerleri almak mümkün kılar. Alınan sonra verileri Azure SQL Database, Azure Cosmos DB ya da Azure Data Lake gibi ayrı veri deposundaki kaydedilebilir. Buradan, gerektiği gibi ek çözümleme gerçekleştirilebilir.

Bu makalede gösterdiği gibi çeşitli ölçüm veri noktaları ile çalışma yanı sıra, monitör API'si, uyarı kuralları, etkinlik günlükleri görüntüle ve daha fazlasını listelemek mümkün kılar. Kullanılabilir işlemleri tam bir listesi için bkz: [Microsoft Azure İzleyici REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn931943.aspx).

## <a name="authenticating-azure-monitor-requests"></a>Azure İzleyici istekleri kimlik doğrulaması
İlk istek kimliğini doğrulamak için bir adımdır.

Azure İzleyici API karşı yürütülen tüm görevler Azure Resource Manager kimlik doğrulama modeli kullanır. Bu nedenle, tüm istekleri Azure Active Directory (Azure AD) ile kimlik doğrulaması gerekir. İstemci uygulaması kimliğini doğrulamak için bir Azure AD hizmet sorumlusu oluşturmak ve kimlik doğrulama (JWT) belirteci almak için bir yaklaşımdır. Aşağıdaki örnek betik, bir Azure AD hizmeti PowerShell aracılığıyla asıl oluşturmayı gösterir. Üzerinde daha ayrıntılı bir kılavuz için belgelere bakın [kaynaklara erişmek için bir hizmet sorumlusu oluşturmak için Azure PowerShell kullanarak](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password). Ayrıca mümkün [Azure Portalı aracılığıyla hizmet sorumlusu oluşturmak](../azure-resource-manager/resource-group-create-service-principal-portal.md).

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

Azure İzleyici API sorgulamak için istemci uygulamasının daha önce oluşturulan hizmet asıl kimlik doğrulaması için kullanmanız gerekir. Aşağıdaki örnek PowerShell komut dosyasını bir gösterir yaklaşımını kullanarak [Active Directory kimlik doğrulama Kitaplığı](../active-directory/active-directory-authentication-libraries.md) JWT kimlik doğrulama belirteci alma yardımcı olmak için (ADAL). JWT belirteci Azure İzleyici REST API istekleri HTTP yetkilendirme parametresinde bir parçası olarak geçirilir.

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

Kimlik Doğrulama kurulumu adım tamamlandıktan sonra sorguları karşı Azure İzleyici REST API sonra çalıştırılabilir. İki yararlı sorgular şunlardır:

1. Bir kaynak için ölçüm açıklamalarının listesi
2. Ölçü değerlerini alma

## <a name="retrieve-metric-definitions"></a>Ölçüm tanımlarını Al
> [!NOTE]
> Azure İzleyici REST API'sini kullanarak ölçüm tanımlarını almak için "2016-03-01" API sürümü kullanın.
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
Bir Azure mantıksal uygulama için ölçüm tanımlarını aşağıdaki ekran görüntüsüne benzer görünür:

![Alt "JSON görünüm ölçüm tanımı yanıtının."](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

Daha fazla bilgi için bkz: [Azure İzleyici REST API kaynak ölçüm tanımlarını listesinde](https://msdn.microsoft.com/library/azure/mt743621.aspx) belgeleri.

## <a name="retrieve-metric-values"></a>Ölçü değerlerini alma
Kullanılabilir ölçüm tanımlarını bilinen sonra ardından ilgili ölçüm değerleri almak mümkündür. Filtreleme tüm istekler için ölçüm kişinin adı 'value' (değil ' localizedValue') kullanın (örneğin, 'CPU zamanı' ve 'İsteklerini' Ölçüm veri noktalarını almaya). Hiçbir filtre belirtilmezse, varsayılan ölçü döndürülür.

> [!NOTE]
> Azure İzleyici REST API'sini kullanarak ölçüm değerleri almak için "2016-06-01" API sürümü kullanın.
>
>

**Yöntem**: Al

**İstek URI'si**: https://management.azure.com/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/*{ Kaynak-sağlayıcısı-namespace}*/*{kaynak türü}*/*{kaynak-adı}*/providers/microsoft.insights/metrics?$filter= *{filtre}*& api-version =*{apiVersion}*

Örneğin, 1 saatlik bir zaman çizgisi ve belirli bir zaman aralığı için RunsSucceeded ölçüm veri noktalarını almak için isteği aşağıdaki gibi olur:

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

Sonuç ekran aşağıdaki örneğe benzer görünür:

![Alt "JSON yanıt ortalama yanıt süresi ölçüm değeri gösterme"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

Birden çok veri veya toplama noktası almak için ölçüm tanımı adları ve toplama türleri filtre için aşağıdaki örnekte görüldüğü gibi ekleyin:

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a>ARMClient kullanın
(Yukarıda gösterildiği gibi) PowerShell kullanarak alternatif kullanmaktır [ARMClient](https://github.com/projectkudu/ARMClient) Windows makinenizde. ARMClient Azure AD kimlik doğrulaması (ve sonuçta elde edilen JWT belirteci) otomatik olarak yönetir. ARMClient kullanımını ölçüm verileri almak için aşağıdaki adımları özetlemektedir:

1. Yükleme [Chocolatey](https://chocolatey.org/) ve [ARMClient](https://github.com/projectkudu/ARMClient).
2. Bir terminal penceresi yazın *armclient.exe oturum açma*. Azure'da oturum açma ister.
3. Tür *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*
4. Tür *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*

![Alt "Azure Monitoring REST API'si ile çalışmaya kullanma ARMClient"](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-the-resource-id"></a>Kaynak Kimliği alma
REST API kullanarak gerçekten kullanılabilir ölçüm tanımlarını, ayrıntı düzeyi ve ilgili değerleri anlamanıza yardımcı olabilir. Bilgi kullanıldığında yararlı olduğunu [Azure Yönetimi Kitaplığı](https://msdn.microsoft.com/library/azure/mt417623.aspx).

Önceki kod için kullanılacak kaynak kimliği istenen Azure kaynak tam yoludur. Örneğin, bir Azure Web uygulaması karşı sorgulamak için kaynak kimliği olur:

*/Subscriptions/{Subscription-id}/resourceGroups/{Resource-Group-Name}/providers/Microsoft.Web/Sites/{Site-Name}/*

Aşağıdaki listede kaynak kimliği biçimlerinden çeşitli Azure kaynakları için birkaç örnek içerir:

* **IOT hub'ı** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-adı}*
* **SQL esnek havuzu** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Sql/servers/*{havuzu-db}*/elasticpools/*{sql-havuzu-adı}*
* **SQL veritabanı (v12)** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Sql/servers/*{sunucu-adı}* /databases/*{veritabanı-adı}*
* **Hizmet veri yolu** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.ServiceBus/*{ad}* / *{servicebus-adı}*
* **VM ölçek kümesi** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{ VM-adı}*
* **Sanal makineleri** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Compute/virtualMachines/*{vm-adı}*
* **Olay hub'ları** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.EventHub/namespaces/*{ eventhub-namespace}*

Azure kaynak Gezgini, istenen kaynak Azure portalında ve PowerShell veya Azure CLI aracılığıyla görüntüleme kullanımı dahil olmak üzere kaynak kimliği alma için alternatif bir yaklaşım vardır.

### <a name="azure-resource-explorer"></a>Azure Resource Manager
İstenen kaynak için kaynak Kimliğini bulmak için kullanmak için yararlı bir yaklaşım ise [Azure kaynak Gezgini](https://resources.azure.com) aracı. İstenen kaynağa gidin ve ardından, olduğu gibi aşağıdaki ekran görüntüsünde gösterilen tanıtıcı bakın:

![Alt "Azure kaynak Gezgini"](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a>Azure portalına
Kaynak Kimliği de Azure portalından elde edilebilir. Bunu yapmak için istenen kaynağa gidin ve ardından Özellikler'i seçin. Kaynak Kimliği özellikleri dikey penceresinde, aşağıdaki ekran görüntüsünde görülen görüntülenir:

!["Alt kaynak kimliği özellikleri dikey penceresinde Azure portalında görüntülenen"](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a>Azure PowerShell
Kaynak Kimliği, Azure PowerShell cmdlet'leri kullanılarak alınabilir. Örneğin, bir Azure Web uygulaması için kaynak Kimliğini almak için aşağıdaki ekran görüntüsünde olduğu gibi Get-AzureRmWebApp cmdlet'ini yürütün:

!["PowerShell elde alt kaynak kimliği"](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a>Azure CLI
Azure CLI kullanarak kaynak kimliği almak için 'azure webapp Göster' komutunu yürütün belirtme '--json' seçeneği, aşağıdaki ekran görüntüsünde gösterildiği gibi:

!["PowerShell elde alt kaynak kimliği"](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a>Etkinlik günlüğü verilerini alma
Ölçüm tanımlarını ve ilgili değerleri ile çalışma ek olarak, ayrıca Azure kaynaklarla ilgili ek ilginç Öngörüler almak mümkündür. Örnek olarak, sorguyu mümkündür [etkinlik günlüğü](https://msdn.microsoft.com/library/azure/dn931934.aspx) veri. Aşağıdaki örnek, Azure aboneliği için sorgu etkinlik günlüğü verileri belirli bir tarih aralığı içinde Azure İzleyici REST API'sini kullanarak gösterir:

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a>Sonraki adımlar
* Gözden geçirme [izleme genel bakış](monitoring-overview.md).
* Görünüm [desteklenen Azure İzleyicisi ile ölçümleri](monitoring-supported-metrics.md).
* Gözden geçirme [Microsoft Azure izlemek REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn931943.aspx).
* Gözden geçirme [Azure Yönetimi Kitaplığı](https://msdn.microsoft.com/library/azure/mt417623.aspx).
