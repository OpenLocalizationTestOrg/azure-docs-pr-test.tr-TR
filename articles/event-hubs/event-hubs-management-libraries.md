---
title: "aaaAzure olay hub'ları yönetim kitaplıklarını | Microsoft Docs"
description: "Olay hub'ları ad alanları ve varlıkları .NET yönetme"
services: event-hubs
cloud: na
documentationcenter: na
author: sethmanheim
manager: timlt
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: b7db0077f6f31397ae46e926c3c28630a157824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-management-libraries"></a>Olay hub'ları yönetim kitaplıkları

Merhaba olay hub'ları yönetim kitaplıklarını dinamik olarak Event Hubs ad alanları ve varlıkları sağlayabilirsiniz. Program aracılığıyla hangi varlıkları tooprovision belirleyebilmesi karmaşık dağıtımlar ve mesajlaşma senaryoları sağlar. Bu kitaplıklar, .NET için şu anda kullanılabilir.

## <a name="supported-functionality"></a>Desteklenen işlevi

* Namespace oluşturma, güncelleştirme, silme
* Olay hub'ları oluşturma, güncelleştirme, silme
* Tüketici grubu oluşturma, güncelleştirme, silme

## <a name="prerequisites"></a>Ön koşullar

Merhaba olay hub'ları yönetim kitaplıklarını kullanmaya tooget, Azure Active Directory'ye (AAD) kimliğini doğrulaması gerekir. AAD Azure kaynaklarına erişim tooyour sağlayan bir hizmet sorumlusu kimlik doğrulaması gerektirir. Bir hizmet sorumlusu oluşturma hakkında daha fazla bilgi için Bu makalelerden birine bakın:  

* [Hello Azure portal toocreate Active Directory Uygulama ve kaynaklarına erişebilir hizmet sorumlusu kullanın](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [Bir hizmet asıl tooaccess kaynakları Azure PowerShell toocreate kullanın](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Bir hizmet asıl tooaccess kaynakları Azure CLI toocreate kullanın](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

Bu öğreticiler sağladığını bir `AppId` (istemci kimliği) `TenantId`, ve `ClientSecret` (kimlik doğrulama anahtarı), her biri hello yönetim kitaplıklarını tarafından kimlik doğrulaması için kullanılır. Bilmeniz gereken **sahibi** toorun istediğiniz hello kaynak grubu için izinleri.

## <a name="programming-pattern"></a>Programlama modeli

Desen toomanipulate hello herhangi bir olay hub'ları kaynak ortak bir protokolle izler:

1. Hello kullanarak AAD bir belirteci edinmesine `Microsoft.IdentityModel.Clients.ActiveDirectory` kitaplığı.
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. Merhaba oluşturmak `EventHubManagementClient` nesnesi.
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. Set hello `CreateOrUpdate` parametreleri tooyour belirtilen değerleri.
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. Merhaba çağrısı yürütün.
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a>Sonraki adımlar
* [.NET Yönetim örnek](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [Microsoft.Azure.Management.EventHub başvurusu](/dotnet/api/Microsoft.Azure.Management.EventHub) 
