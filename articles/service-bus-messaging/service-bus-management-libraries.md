---
title: "aaaAzure hizmet veri yolu yönetim kitaplıklarını | Microsoft Docs"
description: "Hizmet veri yolu ad alanları ve .NET varlıklardan Mesajlaşma yönetin."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: 9e4ad91f22815ca0838e6e4647a3606109b2b441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-management-libraries"></a>Hizmet veri yolu yönetim kitaplıkları

Hello Azure hizmet veri yolu yönetim kitaplıklarını dinamik olarak hizmet veri yolu ad alanları ve varlıkları sağlayabilirsiniz. Bu karmaşık dağıtımlar ve mesajlaşma senaryolarına olanak sağlar ve mümkün kılar tooprogrammatically hangi varlıkları tooprovision belirler. Bu kitaplıklar, .NET için şu anda kullanılabilir.

## <a name="supported-functionality"></a>Desteklenen işlevi

* Namespace oluşturma, güncelleştirme, silme
* Kuyruk oluşturma, güncelleştirme, silme
* Konu oluşturma, güncelleştirme, silme
* Abonelik oluşturma, güncelleştirme, silme

## <a name="prerequisites"></a>Ön koşullar

Hello hizmet veri yolu yönetim kitaplıklarını kullanmaya tooget hello Azure Active Directory (AAD) hizmeti ile kimlik doğrulaması gerekir. AAD Azure kaynaklarına erişim tooyour sağlayan bir hizmet sorumlusu kimlik doğrulaması gerektirir. Bir hizmet sorumlusu oluşturma hakkında daha fazla bilgi için Bu makalelerden birine bakın:  

* [Hello Azure portal toocreate Active Directory Uygulama ve kaynaklarına erişebilir hizmet sorumlusu kullanın](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [Bir hizmet asıl tooaccess kaynakları Azure PowerShell toocreate kullanın](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Bir hizmet asıl tooaccess kaynakları Azure CLI toocreate kullanın](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

Bu öğreticiler sağladığını bir `AppId` (istemci kimliği) `TenantId`, ve `ClientSecret` (kimlik doğrulama anahtarı), her biri hello yönetim kitaplıklarını tarafından kimlik doğrulaması için kullanılır. Bilmeniz gereken **sahibi** toorun istediğiniz hello kaynak grubu için izinleri.

## <a name="programming-pattern"></a>Programlama modeli

Desen toomanipulate hello herhangi bir Service Bus kaynak ortak bir protokolle izler:

1. Azure Active hello kullanarak Directory'den bir belirteç elde **Microsoft.IdentityModel.Clients.activedirectory tarafından** kitaplığı.
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. Merhaba oluşturmak `ServiceBusManagementClient` nesnesi.

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. Set hello `CreateOrUpdate` parametreleri tooyour belirtilen değerleri.

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. Merhaba çağrısı yürütün.

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a>Sonraki adımlar
* [.NET Yönetim örnek](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [Microsoft.Azure.Management.ServiceBus API Başvurusu](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
