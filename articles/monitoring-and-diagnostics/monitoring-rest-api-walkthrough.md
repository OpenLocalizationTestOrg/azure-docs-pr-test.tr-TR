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
# <a name="azure-monitoring-rest-api-walkthrough"></a>REST API izlenecek izleme azure
Bu makale size nasıl gösterir kodunuzu hello kullanabilmeniz için tooperform kimlik doğrulaması [Microsoft Azure İzleyici REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn931943.aspx).         

Hello Azure İzleyici API olası tooprogrammatically alma hello kullanılabilir varsayılan ölçüm tanımları (ölçümü CPU süresi, istekleri, vb. gibi hello türü), ayrıntı düzeyi ve ölçüm değerleri kolaylaştırır. Alınan sonra Azure SQL Database, Azure Cosmos DB ya da Azure Data Lake gibi ayrı veri deposundaki hello veri kaydedilebilir. Buradan, gerektiği gibi ek çözümleme gerçekleştirilebilir.

Bu makalede gösterdiği gibi çeşitli ölçüm veri noktaları ile çalışma yanı sıra hello İzleyici API olası toolist uyarı kuralları, etkinlik günlüklerini görüntüle ve çok daha kolaylaştırır. Merhaba kullanılabilir işlemleri tam bir listesi için bkz [Microsoft Azure İzleyici REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn931943.aspx).

## <a name="authenticating-azure-monitor-requests"></a>Azure İzleyici istekleri kimlik doğrulaması
Merhaba ilk adım, tooauthenticate hello isteğidir.

Hello Azure İzleyici API kullanımı hello Azure Resource Manager kimlik doğrulama modeli karşı yürütülen tüm hello görevler. Bu nedenle, tüm istekleri Azure Active Directory (Azure AD) ile kimlik doğrulaması gerekir. Bir yaklaşım tooauthenticate hello istemci uygulamanın toocreate bir Azure AD hizmet sorumlusu ve hello (JWT) kimlik doğrulama belirtecini almak. Merhaba aşağıdaki örnek komut dosyası Azure AD hizmet sorumlusu PowerShell aracılığıyla oluşturmayı gösterir. Daha ayrıntılı bir kılavuz için üzerinde toohello belgelerine başvurun. [bir hizmet asıl tooaccess kaynakları Azure PowerShell toocreate kullanarak](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password). Ayrıca çok mümkündür[hello Azure portal aracılığıyla bir hizmet sorumlusu oluşturma](../azure-resource-manager/resource-group-create-service-principal-portal.md).

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

tooquery hello Azure monitör API'si, Merhaba istemci uygulaması, daha önce oluşturduğunuz hizmet asıl tooauthenticate hello kullanmanız gerekir. Örnek PowerShell komut dosyası izleyen hello gösterir hello kullanarak bir yaklaşım [Active Directory kimlik doğrulama Kitaplığı](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp hello JWT kimlik doğrulama belirteci alın. Merhaba JWT belirteci isteklerini toohello Azure İzleyici REST API HTTP yetkilendirme parametresinde bir parçası olarak geçirilir.

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

Merhaba kimlik doğrulama Kurulumu adım tamamlandıktan sonra sorguları hello Azure İzleyici REST API'sine karşı daha sonra çalıştırılabilir. İki yararlı sorgular şunlardır:

1. Bir kaynak için liste hello ölçüm tanımları
2. Merhaba ölçüm değerlerini alma

## <a name="retrieve-metric-definitions"></a>Ölçüm tanımlarını Al
> [!NOTE]
> Hello Azure İzleyici REST API'sini kullanarak tooretrieve ölçüm tanımlarını API sürümü hello gibi "2016-03-01" kullanın.
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
Bir Azure mantıksal uygulama için aşağıdaki ekran görüntüsüne benzer toohello hello ölçüm tanımlarını görünür:

![Alt "JSON görünüm ölçüm tanımı yanıtının."](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

Merhaba daha fazla bilgi için bkz [listesinde hello ölçüm Azure İzleyici REST API kaynak tanımlarında](https://msdn.microsoft.com/library/azure/mt743621.aspx) belgeleri.

## <a name="retrieve-metric-values"></a>Ölçü değerlerini alma
Merhaba kullanılabilir ölçüm tanımlarını bilinen sonra olası tooretrieve hello sonra ilgili ölçüm değerleri olan. Merhaba ölçüm'ın ad 'değer' (değil 'localizedValue' hello) filtreleme tüm istekleri (örneğin, alma hello 'CPU zamanı' ve 'İsteklerini' Ölçüm veri noktaları) için kullanır. Hiçbir filtre belirtilirse, hello varsayılan ölçüm döndürülür.

> [!NOTE]
> Hello Azure İzleyici REST API'sini kullanarak tooretrieve ölçüm değerleri API sürümü hello gibi "2016-06-01" kullanın.
>
>

**Yöntem**: Al

**İstek URI'si**: https://management.azure.com/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/*{ Kaynak-sağlayıcısı-namespace}*/*{kaynak türü}*/*{kaynak-adı}*/providers/microsoft.insights/metrics?$filter= *{filtre}*& api-version =*{apiVersion}*

Örneğin, tooretrieve hello RunsSucceeded ölçüm veri noktaları ve bir zaman çizgisi 1 saatlik, hello istek zaman aralığı verilen hello için aşağıdaki gibi olur:

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

Merhaba sonuç aşağıdaki ekran görüntüsüne benzer toohello örnek görünür:

![Alt "JSON yanıt ortalama yanıt süresi ölçüm değeri gösterme"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

tooretrieve birden çok veri veya toplama noktalarını ekleyin hello ölçüm tanımı adları ve toplama türleri toohello filtre hello aşağıdaki örnekte görüldüğü gibi:

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
Alternatif bir toousing (yukarıda gösterildiği gibi) PowerShell olan toouse [ARMClient](https://github.com/projectkudu/ARMClient) Windows makinenizde. ARMClient hello Azure AD kimlik doğrulama (ve sonuçta elde edilen JWT belirteci) otomatik olarak yönetir. Merhaba aşağıdaki adımları ölçüm verilerini alma ARMClient kullanımını özetlemektedir:

1. Yükleme [Chocolatey](https://chocolatey.org/) ve [ARMClient](https://github.com/projectkudu/ARMClient).
2. Bir terminal penceresi yazın *armclient.exe oturum açma*. Bu tooAzure toolog ister.
3. Tür *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*
4. Tür *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*

![Alt "Merhaba Azure Monitoring REST API ile kullanma ARMClient toowork"](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a>Merhaba kaynak kimliği alma
Merhaba REST API kullanarak gerçekten toounderstand hello kullanılabilir ölçüm tanımlarını, ayrıntı düzeyi ve ilgili değerleri yardımcı olabilir. Bu bilgileri hello kullanırken faydalıdır [Azure Yönetimi Kitaplığı](https://msdn.microsoft.com/library/azure/mt417623.aspx).

Kod önceki hello için Azure kaynak hello tam yolu toohello istenen hello kaynak kimliği toouse olur. Örneğin, tooquery Azure Web uygulaması karşı hello kaynak kimliği olur:

*/Subscriptions/{Subscription-id}/resourceGroups/{Resource-Group-Name}/providers/Microsoft.Web/Sites/{Site-Name}/*

Merhaba aşağıda birkaç örnek çeşitli Azure kaynakları için kaynak kimliği biçimlerinden içerir:

* **IOT hub'ı** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-adı}*
* **SQL esnek havuzu** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Sql/servers/*{havuzu-db}*/elasticpools/*{sql-havuzu-adı}*
* **SQL veritabanı (v12)** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Sql/servers/*{sunucu-adı} */databases/*{veritabanı-adı}*
* **Hizmet veri yolu** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.ServiceBus/*{ad}* / *{servicebus-adı}*
* **VM ölçek kümesi** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{ VM-adı}*
* **Sanal makineleri** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.Compute/virtualMachines/*{vm-adı}*
* **Olay hub'ları** -/subscriptions/*{subscrıptıon-ID}*/resourceGroups/*{kaynak grubu adı}*/providers/Microsoft.EventHub/namespaces/*{ eventhub-namespace}*

Azure kaynak Gezgini, istenen hello kaynak hello Azure portal ve PowerShell veya hello Azure CLI aracılığıyla görüntüleme kullanımı dahil olmak üzere çeşitli yaklaşımlar tooretrieving hello kaynak kimliği vardır.

### <a name="azure-resource-explorer"></a>Azure Resource Manager
İstenen kaynak, bir yardımcı yaklaşım için toofind hello kaynak kimliği olan toouse hello [Azure kaynak Gezgini](https://resources.azure.com) aracı. İstenen toohello kaynak gidin ve ardından, aşağıdaki ekran görüntüsü hello olduğu gibi gösterilen hello kimliği bakın:

![Alt "Azure kaynak Gezgini"](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a>Azure portalına
Hello kaynak kimliği de Azure portal hello elde edilebilir. Bu nedenle, toodo toohello istenen kaynak gidin ve ardından Özellikler'i seçin. Merhaba kaynak kimliği hello özellikleri dikey penceresinde, aşağıdaki ekran görüntüsü hello görülen görüntülenir:

!["Hello özellikleri dikey penceresinde hello Azure portalında görüntülenen alt kaynak kimliği"](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a>Azure PowerShell
Merhaba kaynak kimliği, Azure PowerShell cmdlet'leri kullanılarak alınabilir. Örneğin, bir Azure Web uygulaması için tooobtain hello kaynak kimliği ekran aşağıdaki hello olduğu gibi hello Get-AzureRmWebApp cmdlet'ini yürütün:

!["PowerShell elde alt kaynak kimliği"](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a>Azure CLI
tooretrieve hello Azure CLI kullanarak kaynak kimliği Merhaba, hello belirtme hello 'azure webapp Göster' komutunu yürütün '--json' hello ekran aşağıdaki gösterildiği gibi seçeneği:

!["PowerShell elde alt kaynak kimliği"](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a>Etkinlik günlüğü verilerini alma
Ölçüm tanımlarını ve ilgili değerleri toplama tooworking içinde olası tooretrieve ek ilginç Öngörüler ilgili tooAzure kaynaklar da sağlar. İsteğe bağlı olarak örnek olarak, olası tooquery olan [etkinlik günlüğü](https://msdn.microsoft.com/library/azure/dn931934.aspx) veri. Merhaba aşağıdaki örnek hello Azure İzleyici REST API tooquery etkinlik günlüğü verileri belirli bir tarih aralığı içinde bir Azure aboneliği için kullanma gösterilmektedir:

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
* Gözden geçirme hello [genel bakış izleme](monitoring-overview.md).
* Görünüm hello [desteklenen Azure İzleyicisi ile ölçümleri](monitoring-supported-metrics.md).
* Gözden geçirme hello [Microsoft Azure İzleyici REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn931943.aspx).
* Gözden geçirme hello [Azure Yönetimi Kitaplığı](https://msdn.microsoft.com/library/azure/mt417623.aspx).
