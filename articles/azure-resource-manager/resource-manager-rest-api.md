---
title: Resource Manager REST API'leri | Microsoft Docs
description: "Resource Manager REST API'leri kimlik doğrulama ve kullanım örnekleri genel bakış"
services: azure-resource-manager
documentationcenter: na
author: navalev
manager: timlt
editor: 
ms.assetid: e8d7a1d2-1e82-4212-8288-8697341408c5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/13/2017
ms.author: navale;tomfitz;
ms.openlocfilehash: 2f7ba23775545637de865f9ef63680ae22c62164
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="dd22f-103">Resource Manager REST API'leri</span><span class="sxs-lookup"><span data-stu-id="dd22f-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dd22f-104">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd22f-104">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="dd22f-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dd22f-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="dd22f-106">Portal</span><span class="sxs-lookup"><span data-stu-id="dd22f-106">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="dd22f-107">REST API</span><span class="sxs-lookup"><span data-stu-id="dd22f-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="dd22f-108">Yapılan her çağrı için Azure Resource Manager dağıtılan her şablon arkasında arkasında her yapılandırılan depolama hesabı var. bir veya daha fazla Azure Resource Manager'ın RESTful API çağrıları</span><span class="sxs-lookup"><span data-stu-id="dd22f-108">Behind every call to Azure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls to the Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="dd22f-109">Bu konu, bu API'leri ve nasıl bunları herhangi SDK kullanmadan çağırabilirsiniz geçer.</span><span class="sxs-lookup"><span data-stu-id="dd22f-109">This topic is devoted to those APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="dd22f-110">Bu yaklaşım, tam denetim Azure isteklerinin istediğiniz veya tercih ettiğiniz dili için SDK'sı kullanılabilir değilse veya işlemlerini desteklemediğinden, ihtiyacınız varsa yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="dd22f-110">This approach is useful if you want full control of requests to Azure, or if the SDK for your preferred language is not available or doesn't support the operations you need.</span></span>

<span data-ttu-id="dd22f-111">Bu makalede, Azure'da gösterilir, ancak yerine bunları nasıl bağlanacağını örnekleri olarak bazı işlemler kullanan her bir API aracılığıyla geçmez.</span><span class="sxs-lookup"><span data-stu-id="dd22f-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect to them.</span></span> <span data-ttu-id="dd22f-112">Temel kavramları öğrendikten sonra okuyabilirsiniz [Azure Resource Manager REST API Başvurusu](https://docs.microsoft.com/rest/api/resources/) rest API'leri kullanma hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="dd22f-112">After you understand the basics, you can read the [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) to find detailed information on how to use the rest of the APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="dd22f-113">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="dd22f-113">Authentication</span></span>
<span data-ttu-id="dd22f-114">Kimlik doğrulama kaynak yöneticisi için Azure Active Directory (AD tarafından) ele alınır.</span><span class="sxs-lookup"><span data-stu-id="dd22f-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="dd22f-115">Herhangi bir API'yi bağlanmak için önce her istek için geçmesi kimlik doğrulama belirtecini almak için Azure AD ile kimlik doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd22f-115">To connect to any API, you first need to authenticate with Azure AD to receive an authentication token that you can pass on to every request.</span></span> <span data-ttu-id="dd22f-116">Saf çağrısı REST API'lerini doğrudan tanımlamakta olduğunuz gibi bir kullanıcı adı ve parola istendiğinde tarafından kimlik doğrulaması istemediğiniz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="dd22f-116">As we are describing a pure call directly to the REST APIs, we assume that you don't want to authenticate by being prompted for a username and password.</span></span> <span data-ttu-id="dd22f-117">İki faktörlü kimlik doğrulama mekanizmaları kullanmıyorsanız varsayıyoruz.</span><span class="sxs-lookup"><span data-stu-id="dd22f-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="dd22f-118">Bu nedenle, hangi Azure AD uygulaması ve hizmet asıl oturum açmak için kullanılan adlandırılır oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd22f-118">Therefore, we create what is called an Azure AD Application and a service principal that are used to log in.</span></span> <span data-ttu-id="dd22f-119">Ancak Azure AD destekleyen birden fazla kimlik doğrulama yordamları ve bunların tümünün sonraki API istekleri için ihtiyacımız bu kimlik doğrulama belirtecini almak için kullanılabilecek unutmayın.</span><span class="sxs-lookup"><span data-stu-id="dd22f-119">But remember that Azure AD support several authentication procedures and all of them could be used to retrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="dd22f-120">İzleyin [oluşturma Azure AD uygulaması ve hizmet sorumlusu](resource-group-create-service-principal-portal.md) adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="dd22f-120">Follow [Create Azure AD Application and Service Principal](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="dd22f-121">Bir erişim belirteci oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd22f-121">Generating an Access Token</span></span>
<span data-ttu-id="dd22f-122">Azure AD kimlik doğrulaması, login.microsoftonline.com bulunan Azure AD ile çağırarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="dd22f-122">Authentication against Azure AD is done by calling out to Azure AD, located at login.microsoftonline.com.</span></span> <span data-ttu-id="dd22f-123">Kimlik doğrulaması yapmak için aşağıdaki bilgilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="dd22f-123">To authenticate, you need to have the following information:</span></span>

* <span data-ttu-id="dd22f-124">Azure AD Kiracı kimliği (genellikle aynı şirketinizin oturum açma kullanarak ancak gerekli değildir, Azure AD adı)</span><span class="sxs-lookup"><span data-stu-id="dd22f-124">Azure AD Tenant ID (the name of that Azure AD you are using to log in, often the same as your company but not necessary)</span></span>
* <span data-ttu-id="dd22f-125">Uygulama Kimliği (Azure AD uygulama oluşturma adımında taken)</span><span class="sxs-lookup"><span data-stu-id="dd22f-125">Application ID (taken during the Azure AD application creation step)</span></span>
* <span data-ttu-id="dd22f-126">(Azure AD uygulaması oluştururken seçtiğiniz) parola</span><span class="sxs-lookup"><span data-stu-id="dd22f-126">Password (that you selected while creating the Azure AD Application)</span></span>

<span data-ttu-id="dd22f-127">Aşağıdaki HTTP istek "Azure AD Kiracı kimliği", "Uygulama kimliği" ve "Parola" doğru değerlerle değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="dd22f-127">In the following HTTP request, make sure to replace "Azure AD Tenant ID", "Application ID" and "Password" with the correct values.</span></span>

<span data-ttu-id="dd22f-128">**Genel HTTP isteği:**</span><span class="sxs-lookup"><span data-stu-id="dd22f-128">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="dd22f-129">... (doğrulama başarılı olursa) olacak aşağıdaki yanıta benzer bir yanıt neden:</span><span class="sxs-lookup"><span data-stu-id="dd22f-129">... will (if authentication succeeds) result in a response similar to the following response:</span></span>

```json
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1448199959",
  "not_before": "1448196059",
  "resource": "https://management.core.windows.net/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhb...86U3JI_0InPUk_lZqWvKiEWsayA"
}
```
<span data-ttu-id="dd22f-130">(Önceki yanıtta access_token kısaltılmış okunabilirliğini artırmak için)</span><span class="sxs-lookup"><span data-stu-id="dd22f-130">(The access_token in the preceding response have been shortened to increase readability)</span></span>

<span data-ttu-id="dd22f-131">**Erişim belirteci Bash kullanarak oluşturuluyor:**</span><span class="sxs-lookup"><span data-stu-id="dd22f-131">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="dd22f-132">**PowerShell kullanarak erişim belirteci oluşturuluyor:**</span><span class="sxs-lookup"><span data-stu-id="dd22f-132">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="dd22f-133">Yanıt, bir erişim belirteci, ne kadar süreyle bu belirtecin geçerli olduğu hakkında bilgi ve hangi kaynak için bu belirteci kullanabilirsiniz hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="dd22f-133">The response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="dd22f-134">Önceki HTTP çağrısında aldığınız erişim belirtecini tüm istekleri için kaynak yöneticisi API'si geçirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd22f-134">The access token you received in the previous HTTP call must be passed in for all request to the Resource Manager API.</span></span> <span data-ttu-id="dd22f-135">"Taşıyıcı YOUR_ACCESS_TOKEN" değeriyle "Yetkilendirme" adlı bir üstbilgi değeri olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="dd22f-135">You pass it as a header value named "Authorization" with the value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="dd22f-136">"Bearer" ve erişim belirtecinizi arasındaki boşluğu dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="dd22f-136">Notice the space between "Bearer" and your access token.</span></span>

<span data-ttu-id="dd22f-137">Belirteç yukarıdaki HTTP sonucundan görebileceğiniz gibi bir belirli süre boyunca önbelleğe ve gerekir, aynı belirteci yeniden için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="dd22f-137">As you can see from the above HTTP Result, the token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="dd22f-138">Her API çağrısı için Azure AD kimlik doğrulaması mümkün olsa bile, yüksek oranda verimsiz olacaktır.</span><span class="sxs-lookup"><span data-stu-id="dd22f-138">Even if it is possible to authenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="dd22f-139">Arama Resource Manager REST API'leri</span><span class="sxs-lookup"><span data-stu-id="dd22f-139">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="dd22f-140">Bu konuda, temel kullanım REST işlemlerinin açıklamak için yalnızca birkaç API'leri kullanır.</span><span class="sxs-lookup"><span data-stu-id="dd22f-140">This topic only uses a few APIs to explain the basic usage of the REST operations.</span></span> <span data-ttu-id="dd22f-141">Tüm işlemleri hakkında daha fazla bilgi için bkz: [Azure Resource Manager REST API'leri](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="dd22f-141">For information about all the operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="dd22f-142">Tüm abonelikleri listeler</span><span class="sxs-lookup"><span data-stu-id="dd22f-142">List all subscriptions</span></span>
<span data-ttu-id="dd22f-143">Yapabileceğiniz basit işlemleri erişmek için kullanılabilir abonelikler listesine biridir.</span><span class="sxs-lookup"><span data-stu-id="dd22f-143">One of the simplest operations you can do is to list the available subscriptions that you can access.</span></span> <span data-ttu-id="dd22f-144">Aşağıdaki istekte nasıl erişim belirteci başlık olarak geçirilen bakın:</span><span class="sxs-lookup"><span data-stu-id="dd22f-144">In the following request, you see how the access token is passed in as a header:</span></span>

<span data-ttu-id="dd22f-145">(YOUR_ACCESS_TOKEN, gerçek erişim belirteci ile değiştirin.)</span><span class="sxs-lookup"><span data-stu-id="dd22f-145">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="dd22f-146">... ve sonuç olarak, bu hizmet sorumlusu erişmesine izin verilip Aboneliklerin listesini alın</span><span class="sxs-lookup"><span data-stu-id="dd22f-146">... and as a result, you get a list of subscriptions that this service principal is allowed to access</span></span>

<span data-ttu-id="dd22f-147">(Abonelik kimlikleri okunabilirlik için kısaltılmıştır)</span><span class="sxs-lookup"><span data-stu-id="dd22f-147">(Subscription IDs have been shortened for readability)</span></span>

```json
{
  "value": [
    {
      "id": "/subscriptions/3a8555...555995",
      "subscriptionId": "3a8555...555995",
      "displayName": "Azure Subscription",
      "state": "Enabled",
      "subscriptionPolicies": {
        "locationPlacementId": "Internal_2014-09-01",
        "quotaId": "Internal_2014-09-01"
      }
    }
  ]
}
```

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="dd22f-148">Belirli bir Abonelikteki tüm kaynak gruplarının listesi</span><span class="sxs-lookup"><span data-stu-id="dd22f-148">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="dd22f-149">Resource Manager API'leri kullanılarak tüm kaynaklar bir kaynak grubu içinde yuvalanmış.</span><span class="sxs-lookup"><span data-stu-id="dd22f-149">All resources available with the Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="dd22f-150">Kaynak Yöneticisi'ni kullanarak aşağıdaki HTTP GET isteği aboneliğinizde için mevcut kaynak grupları sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd22f-150">You can query Resource Manager for existing resource groups in your subscription using the following HTTP GET request.</span></span> <span data-ttu-id="dd22f-151">Nasıl abonelik kimliği URL'SİNİN bir parçası bu süre geçirilen dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="dd22f-151">Notice how the subscription ID is passed in as part of the URL this time.</span></span>

<span data-ttu-id="dd22f-152">(YOUR_ACCESS_TOKEN ve ABONELİK_KİMLİĞİ gerçek erişim belirtecini ve abonelik Kimliğinizle değiştirin)</span><span class="sxs-lookup"><span data-stu-id="dd22f-152">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="dd22f-153">Aldığınız yanıt tanımlanmış bir kaynak grubu olup olmadığına bağlıdır ve bu durumda, kaç tane.</span><span class="sxs-lookup"><span data-stu-id="dd22f-153">The response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="dd22f-154">(Abonelik kimlikleri okunabilirlik için kısaltılmıştır)</span><span class="sxs-lookup"><span data-stu-id="dd22f-154">(Subscription IDs have been shortened for readability)</span></span>

```json
{
    "value": [
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/myfirstresourcegroup",
            "name": "myfirstresourcegroup",
            "location": "eastus",
            "properties": {
                "provisioningState": "Succeeded"
            }
        },
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/mysecondresourcegroup",
            "name": "mysecondresourcegroup",
            "location": "northeurope",
            "tags": {
                "tagname1": "My first tag"
            },
            "properties": {
                "provisioningState": "Succeeded"
            }
        }
    ]
}
```

### <a name="create-a-resource-group"></a><span data-ttu-id="dd22f-155">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd22f-155">Create a resource group</span></span>
<span data-ttu-id="dd22f-156">Şu ana kadar biz yalnızca bilgi için Resource Manager API'leri sorgulama.</span><span class="sxs-lookup"><span data-stu-id="dd22f-156">So far, we've only been querying the Resource Manager APIs for information.</span></span> <span data-ttu-id="dd22f-157">Biz bazı kaynaklar oluşturun ve en basit tümünü, bir kaynak grubu tarafından başlayalım zamanı geldi.</span><span class="sxs-lookup"><span data-stu-id="dd22f-157">It's time we create some resources, and let's start by the simplest of them all, a resource group.</span></span> <span data-ttu-id="dd22f-158">Aşağıdaki HTTP isteği bir bölge/konum tercih ettiğiniz bir kaynak grubu oluşturur ve bir etiket ekler.</span><span class="sxs-lookup"><span data-stu-id="dd22f-158">The following HTTP request creates a resource group in a region/location of your choice, and adds a tag to it.</span></span>

<span data-ttu-id="dd22f-159">(YOUR_ACCESS_TOKEN, ABONELİK_KİMLİĞİ, RESOURCE_GROUP_NAME, gerçek erişim belirteci, abonelik kimliği ve oluşturmak istediğiniz kaynak grubunun adıyla değiştirin)</span><span class="sxs-lookup"><span data-stu-id="dd22f-159">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of the Resource Group you want to create)</span></span>

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  }
}
```

<span data-ttu-id="dd22f-160">Başarılı olursa, aşağıdaki yanıta benzer bir yanıt alın:</span><span class="sxs-lookup"><span data-stu-id="dd22f-160">If successful, you get a response that is similar to the following response:</span></span>

```json
{
  "id": "/subscriptions/3a8555...555995/resourceGroups/RESOURCE_GROUP_NAME",
  "name": "RESOURCE_GROUP_NAME",
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  },
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<span data-ttu-id="dd22f-161">Azure'da bir kaynak grubu başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="dd22f-161">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="dd22f-162">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="dd22f-162">Congratulations!</span></span>

### <a name="deploy-resources-to-a-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="dd22f-163">Kaynakları bir Resource Manager şablonu kullanarak bir kaynak grubuna Dağıt</span><span class="sxs-lookup"><span data-stu-id="dd22f-163">Deploy resources to a resource group using a Resource Manager Template</span></span>
<span data-ttu-id="dd22f-164">Resource Manager ile şablonları kullanarak kaynaklarınızı dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd22f-164">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="dd22f-165">Bir şablonu bazı kaynaklar ve bağımlılıklarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="dd22f-165">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="dd22f-166">Bu bölüm için Resource Manager şablonları hakkında bilginiz ve yalnızca dağıtımı başlatmak için API çağrısı yapma gösteriyoruz varsayıyoruz.</span><span class="sxs-lookup"><span data-stu-id="dd22f-166">For this section, we assume you are familiar with Resource Manager templates, and we just show you how to make the API call to start deployment.</span></span> <span data-ttu-id="dd22f-167">Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="dd22f-167">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="dd22f-168">Dağıtım şablonu, diğer API'leri çağırmak nasıl çok farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="dd22f-168">Deployment of a template doesn't differ much to how you call other APIs.</span></span> <span data-ttu-id="dd22f-169">Önemli bir özelliği, bir şablon dağıtımını oldukça uzun zaman alabilir ' dir.</span><span class="sxs-lookup"><span data-stu-id="dd22f-169">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="dd22f-170">API çağrısı yalnızca döndürür ve dağıtım yapıldığında öğrenmek için geliştirici olarak sorgulamak için dağıtım durumunu olduğunu.</span><span class="sxs-lookup"><span data-stu-id="dd22f-170">The API call just returns, and it's up to you as developer to query for status of the deployment to find out when the deployment is done.</span></span> <span data-ttu-id="dd22f-171">Daha fazla bilgi için bkz: [izlemek zaman uyumsuz Azure işlemleri](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="dd22f-171">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="dd22f-172">Bu örnekte, kullanılabilir bir genel olarak sunulan şablon kullanırız [GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="dd22f-172">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="dd22f-173">Kullanırız şablonu, Batı ABD bölgesi için bir Linux VM dağıtır.</span><span class="sxs-lookup"><span data-stu-id="dd22f-173">The template we use deploys a Linux VM to the West US region.</span></span> <span data-ttu-id="dd22f-174">Bu örnek, GitHub gibi ortak bir havuzda kullanılabilir bir şablonu kullanıyor olsa bile, bunun yerine tam şablon isteğin bir parçası geçiş yapabilir.</span><span class="sxs-lookup"><span data-stu-id="dd22f-174">Even though this example uses a template available in a public repository like GitHub, you can instead pass the full template as part of the request.</span></span> <span data-ttu-id="dd22f-175">Dağıtılan şablonu içinde kullanılan parametre değerlerini istekte sağladığımız unutmayın.</span><span class="sxs-lookup"><span data-stu-id="dd22f-175">Note that we provide parameter values in the request that are used inside the deployed template.</span></span>

<span data-ttu-id="dd22f-176">(İsteğiniz uygun değerlere ABONELİK_KİMLİĞİ, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD ve DNS_NAME_FOR_PUBLIC_IP değiştirin)</span><span class="sxs-lookup"><span data-stu-id="dd22f-176">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP to values appropriate for your request)</span></span>

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME/providers/microsoft.resources/deployments/DEPLOYMENT_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "properties": {
    "templateLink": {
      "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json",
      "contentVersion": "1.0.0.0",
    },
    "mode": "Incremental",
    "parameters": {
        "newStorageAccountName": {
          "value": "GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME"
        },
        "adminUsername": {
          "value": "ADMIN_USER_NAME"
        },
        "adminPassword": {
          "value": "ADMIN_PASSWORD"
        },
        "dnsNameForPublicIP": {
          "value": "DNS_NAME_FOR_PUBLIC_IP"
        },
        "ubuntuOSVersion": {
          "value": "15.04"
        }
    }
  }
}
```

<span data-ttu-id="dd22f-177">Bu belgelerin okunabilirliğini artırmak için bu istek için uzun JSON yanıt çıkarıldı.</span><span class="sxs-lookup"><span data-stu-id="dd22f-177">The long JSON response for this request has been omitted to improve readability of this documentation.</span></span> <span data-ttu-id="dd22f-178">Yanıt, oluşturduğunuz şablonlu dağıtımı hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="dd22f-178">The response contains information about the templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd22f-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dd22f-179">Next steps</span></span>

- <span data-ttu-id="dd22f-180">Zaman uyumsuz REST işlemlerini işleme hakkında bilgi edinmek için [izlemek zaman uyumsuz Azure işlemleri](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="dd22f-180">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
