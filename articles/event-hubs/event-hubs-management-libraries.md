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
# <a name="event-hubs-management-libraries"></a><span data-ttu-id="21df4-103">Olay hub'ları yönetim kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="21df4-103">Event Hubs management libraries</span></span>

<span data-ttu-id="21df4-104">Merhaba olay hub'ları yönetim kitaplıklarını dinamik olarak Event Hubs ad alanları ve varlıkları sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21df4-104">hello Event Hubs management libraries can dynamically provision Event Hubs namespaces and entities.</span></span> <span data-ttu-id="21df4-105">Program aracılığıyla hangi varlıkları tooprovision belirleyebilmesi karmaşık dağıtımlar ve mesajlaşma senaryoları sağlar.</span><span class="sxs-lookup"><span data-stu-id="21df4-105">This enables complex deployments and messaging scenarios, so that you can programmatically determine what entities tooprovision.</span></span> <span data-ttu-id="21df4-106">Bu kitaplıklar, .NET için şu anda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="21df4-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="21df4-107">Desteklenen işlevi</span><span class="sxs-lookup"><span data-stu-id="21df4-107">Supported functionality</span></span>

* <span data-ttu-id="21df4-108">Namespace oluşturma, güncelleştirme, silme</span><span class="sxs-lookup"><span data-stu-id="21df4-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="21df4-109">Olay hub'ları oluşturma, güncelleştirme, silme</span><span class="sxs-lookup"><span data-stu-id="21df4-109">Event Hubs creation, update, deletion</span></span>
* <span data-ttu-id="21df4-110">Tüketici grubu oluşturma, güncelleştirme, silme</span><span class="sxs-lookup"><span data-stu-id="21df4-110">Consumer Group creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21df4-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="21df4-111">Prerequisites</span></span>

<span data-ttu-id="21df4-112">Merhaba olay hub'ları yönetim kitaplıklarını kullanmaya tooget, Azure Active Directory'ye (AAD) kimliğini doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="21df4-112">tooget started using hello Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span></span> <span data-ttu-id="21df4-113">AAD Azure kaynaklarına erişim tooyour sağlayan bir hizmet sorumlusu kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="21df4-113">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="21df4-114">Bir hizmet sorumlusu oluşturma hakkında daha fazla bilgi için Bu makalelerden birine bakın:</span><span class="sxs-lookup"><span data-stu-id="21df4-114">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="21df4-115">Hello Azure portal toocreate Active Directory Uygulama ve kaynaklarına erişebilir hizmet sorumlusu kullanın</span><span class="sxs-lookup"><span data-stu-id="21df4-115">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="21df4-116">Bir hizmet asıl tooaccess kaynakları Azure PowerShell toocreate kullanın</span><span class="sxs-lookup"><span data-stu-id="21df4-116">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="21df4-117">Bir hizmet asıl tooaccess kaynakları Azure CLI toocreate kullanın</span><span class="sxs-lookup"><span data-stu-id="21df4-117">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

<span data-ttu-id="21df4-118">Bu öğreticiler sağladığını bir `AppId` (istemci kimliği) `TenantId`, ve `ClientSecret` (kimlik doğrulama anahtarı), her biri hello yönetim kitaplıklarını tarafından kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21df4-118">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="21df4-119">Bilmeniz gereken **sahibi** toorun istediğiniz hello kaynak grubu için izinleri.</span><span class="sxs-lookup"><span data-stu-id="21df4-119">You must have **Owner** permissions for hello resource group on which you want toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="21df4-120">Programlama modeli</span><span class="sxs-lookup"><span data-stu-id="21df4-120">Programming pattern</span></span>

<span data-ttu-id="21df4-121">Desen toomanipulate hello herhangi bir olay hub'ları kaynak ortak bir protokolle izler:</span><span class="sxs-lookup"><span data-stu-id="21df4-121">hello pattern toomanipulate any Event Hubs resource follows a common protocol:</span></span>

1. <span data-ttu-id="21df4-122">Hello kullanarak AAD bir belirteci edinmesine `Microsoft.IdentityModel.Clients.ActiveDirectory` kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="21df4-122">Obtain a token from AAD using hello `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span></span>
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. <span data-ttu-id="21df4-123">Merhaba oluşturmak `EventHubManagementClient` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="21df4-123">Create hello `EventHubManagementClient` object.</span></span>
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. <span data-ttu-id="21df4-124">Set hello `CreateOrUpdate` parametreleri tooyour belirtilen değerleri.</span><span class="sxs-lookup"><span data-stu-id="21df4-124">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. <span data-ttu-id="21df4-125">Merhaba çağrısı yürütün.</span><span class="sxs-lookup"><span data-stu-id="21df4-125">Execute hello call.</span></span>
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a><span data-ttu-id="21df4-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="21df4-126">Next steps</span></span>
* [<span data-ttu-id="21df4-127">.NET Yönetim örnek</span><span class="sxs-lookup"><span data-stu-id="21df4-127">.NET Management sample</span></span>](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [<span data-ttu-id="21df4-128">Microsoft.Azure.Management.EventHub başvurusu</span><span class="sxs-lookup"><span data-stu-id="21df4-128">Microsoft.Azure.Management.EventHub Reference</span></span>](/dotnet/api/Microsoft.Azure.Management.EventHub) 
