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
# <a name="service-bus-management-libraries"></a><span data-ttu-id="1e421-103">Hizmet veri yolu yönetim kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="1e421-103">Service Bus management libraries</span></span>

<span data-ttu-id="1e421-104">Hello Azure hizmet veri yolu yönetim kitaplıklarını dinamik olarak hizmet veri yolu ad alanları ve varlıkları sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e421-104">hello Azure Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span></span> <span data-ttu-id="1e421-105">Bu karmaşık dağıtımlar ve mesajlaşma senaryolarına olanak sağlar ve mümkün kılar tooprogrammatically hangi varlıkları tooprovision belirler.</span><span class="sxs-lookup"><span data-stu-id="1e421-105">This enables complex deployments and messaging scenarios, and makes it possible tooprogrammatically determine what entities tooprovision.</span></span> <span data-ttu-id="1e421-106">Bu kitaplıklar, .NET için şu anda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1e421-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="1e421-107">Desteklenen işlevi</span><span class="sxs-lookup"><span data-stu-id="1e421-107">Supported functionality</span></span>

* <span data-ttu-id="1e421-108">Namespace oluşturma, güncelleştirme, silme</span><span class="sxs-lookup"><span data-stu-id="1e421-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="1e421-109">Kuyruk oluşturma, güncelleştirme, silme</span><span class="sxs-lookup"><span data-stu-id="1e421-109">Queue creation, update, deletion</span></span>
* <span data-ttu-id="1e421-110">Konu oluşturma, güncelleştirme, silme</span><span class="sxs-lookup"><span data-stu-id="1e421-110">Topic creation, update, deletion</span></span>
* <span data-ttu-id="1e421-111">Abonelik oluşturma, güncelleştirme, silme</span><span class="sxs-lookup"><span data-stu-id="1e421-111">Subscription creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e421-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1e421-112">Prerequisites</span></span>

<span data-ttu-id="1e421-113">Hello hizmet veri yolu yönetim kitaplıklarını kullanmaya tooget hello Azure Active Directory (AAD) hizmeti ile kimlik doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e421-113">tooget started using hello Service Bus management libraries, you must authenticate with hello Azure Active Directory (AAD) service.</span></span> <span data-ttu-id="1e421-114">AAD Azure kaynaklarına erişim tooyour sağlayan bir hizmet sorumlusu kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1e421-114">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="1e421-115">Bir hizmet sorumlusu oluşturma hakkında daha fazla bilgi için Bu makalelerden birine bakın:</span><span class="sxs-lookup"><span data-stu-id="1e421-115">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="1e421-116">Hello Azure portal toocreate Active Directory Uygulama ve kaynaklarına erişebilir hizmet sorumlusu kullanın</span><span class="sxs-lookup"><span data-stu-id="1e421-116">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [<span data-ttu-id="1e421-117">Bir hizmet asıl tooaccess kaynakları Azure PowerShell toocreate kullanın</span><span class="sxs-lookup"><span data-stu-id="1e421-117">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="1e421-118">Bir hizmet asıl tooaccess kaynakları Azure CLI toocreate kullanın</span><span class="sxs-lookup"><span data-stu-id="1e421-118">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

<span data-ttu-id="1e421-119">Bu öğreticiler sağladığını bir `AppId` (istemci kimliği) `TenantId`, ve `ClientSecret` (kimlik doğrulama anahtarı), her biri hello yönetim kitaplıklarını tarafından kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1e421-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="1e421-120">Bilmeniz gereken **sahibi** toorun istediğiniz hello kaynak grubu için izinleri.</span><span class="sxs-lookup"><span data-stu-id="1e421-120">You must have **Owner** permissions for hello resource group on which you wish toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="1e421-121">Programlama modeli</span><span class="sxs-lookup"><span data-stu-id="1e421-121">Programming pattern</span></span>

<span data-ttu-id="1e421-122">Desen toomanipulate hello herhangi bir Service Bus kaynak ortak bir protokolle izler:</span><span class="sxs-lookup"><span data-stu-id="1e421-122">hello pattern toomanipulate any Service Bus resource follows a common protocol:</span></span>

1. <span data-ttu-id="1e421-123">Azure Active hello kullanarak Directory'den bir belirteç elde **Microsoft.IdentityModel.Clients.activedirectory tarafından** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="1e421-123">Obtain a token from Azure Active Directory using hello **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span></span>
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. <span data-ttu-id="1e421-124">Merhaba oluşturmak `ServiceBusManagementClient` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="1e421-124">Create hello `ServiceBusManagementClient` object.</span></span>

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. <span data-ttu-id="1e421-125">Set hello `CreateOrUpdate` parametreleri tooyour belirtilen değerleri.</span><span class="sxs-lookup"><span data-stu-id="1e421-125">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. <span data-ttu-id="1e421-126">Merhaba çağrısı yürütün.</span><span class="sxs-lookup"><span data-stu-id="1e421-126">Execute hello call.</span></span>

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a><span data-ttu-id="1e421-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1e421-127">Next steps</span></span>
* [<span data-ttu-id="1e421-128">.NET Yönetim örnek</span><span class="sxs-lookup"><span data-stu-id="1e421-128">.NET management sample</span></span>](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [<span data-ttu-id="1e421-129">Microsoft.Azure.Management.ServiceBus API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="1e421-129">Microsoft.Azure.Management.ServiceBus API reference</span></span>](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
