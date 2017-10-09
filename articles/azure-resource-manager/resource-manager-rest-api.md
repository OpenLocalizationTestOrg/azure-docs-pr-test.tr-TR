---
title: aaaResource Manager REST API'leri | Microsoft Docs
description: "Merhaba Resource Manager REST API'leri kimlik doğrulama ve kullanım örnekleri genel bakış"
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
ms.openlocfilehash: 3ccc3575c5e06c41f2fdc5317711980fc6a2f649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="24d65-103">Resource Manager REST API'leri</span><span class="sxs-lookup"><span data-stu-id="24d65-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="24d65-104">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="24d65-104">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="24d65-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="24d65-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="24d65-106">Portal</span><span class="sxs-lookup"><span data-stu-id="24d65-106">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="24d65-107">REST API</span><span class="sxs-lookup"><span data-stu-id="24d65-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="24d65-108">Kaynak Yöneticisi, dağıtılan her şablon arkasında her çağrı tooAzure arkasında her yapılandırılan depolama hesabı var. bir veya daha fazla çağrıları toohello Azure Kaynak Yöneticisi'nin RESTful API'si</span><span class="sxs-lookup"><span data-stu-id="24d65-108">Behind every call tooAzure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls toohello Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="24d65-109">Bu konuda hoşlanıyorsanız toothose olan API'ler ve nasıl bunları herhangi SDK kullanmadan çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24d65-109">This topic is devoted toothose APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="24d65-110">Bu yaklaşım, istekleri tooAzure üzerinde tam denetim istiyorsanız veya hello SDK tercih ettiğiniz dili için kullanılabilir değilse veya gereksinim duyduğunuz hello işlemlerini desteklemediğinden yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="24d65-110">This approach is useful if you want full control of requests tooAzure, or if hello SDK for your preferred language is not available or doesn't support hello operations you need.</span></span>

<span data-ttu-id="24d65-111">Bu makalede, Azure'da gösterilir, ancak yerine bazı işlemler toothem nasıl bağlanacağını örnekleri kullanan her bir API üzerinden geçmez.</span><span class="sxs-lookup"><span data-stu-id="24d65-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect toothem.</span></span> <span data-ttu-id="24d65-112">Merhaba temel kavramları öğrendikten sonra hello okuyabilirsiniz [Azure Resource Manager REST API Başvurusu](https://docs.microsoft.com/rest/api/resources/) toofind ayrıntılı nasıl toouse hello kalan hello API'ler hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="24d65-112">After you understand hello basics, you can read hello [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) toofind detailed information on how toouse hello rest of hello APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="24d65-113">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="24d65-113">Authentication</span></span>
<span data-ttu-id="24d65-114">Kimlik doğrulama kaynak yöneticisi için Azure Active Directory (AD tarafından) ele alınır.</span><span class="sxs-lookup"><span data-stu-id="24d65-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="24d65-115">tooconnect tooany API, ilk Azure AD tooreceive tooevery isteğinde geçirebilirsiniz bir kimlik doğrulama belirteci ile tooauthenticate gerekir.</span><span class="sxs-lookup"><span data-stu-id="24d65-115">tooconnect tooany API, you first need tooauthenticate with Azure AD tooreceive an authentication token that you can pass on tooevery request.</span></span> <span data-ttu-id="24d65-116">Toohello REST API'leri, bir kullanıcı adı ve parola istendiğinde tarafından tooauthenticate istemediğiniz olan varsayıyoruz doğrudan saf çağrı tanımlamakta olduğunuz gibi.</span><span class="sxs-lookup"><span data-stu-id="24d65-116">As we are describing a pure call directly toohello REST APIs, we assume that you don't want tooauthenticate by being prompted for a username and password.</span></span> <span data-ttu-id="24d65-117">İki faktörlü kimlik doğrulama mekanizmaları kullanmıyorsanız varsayıyoruz.</span><span class="sxs-lookup"><span data-stu-id="24d65-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="24d65-118">Bu nedenle, hangi Azure AD uygulaması ve içinde kullanılan toolog olan bir hizmet asıl adı verilir oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24d65-118">Therefore, we create what is called an Azure AD Application and a service principal that are used toolog in.</span></span> <span data-ttu-id="24d65-119">Ancak Azure AD birden fazla kimlik doğrulama yordamları ve bunların tümünün desteklediğini unutmayın kullanılan tooretrieve sonraki API istekleri için ihtiyacımız bu kimlik doğrulama belirteci olabilir.</span><span class="sxs-lookup"><span data-stu-id="24d65-119">But remember that Azure AD support several authentication procedures and all of them could be used tooretrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="24d65-120">İzleyin [oluşturma Azure AD uygulaması ve hizmet sorumlusu](resource-group-create-service-principal-portal.md) adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="24d65-120">Follow [Create Azure AD Application and Service Principal](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="24d65-121">Bir erişim belirteci oluşturma</span><span class="sxs-lookup"><span data-stu-id="24d65-121">Generating an Access Token</span></span>
<span data-ttu-id="24d65-122">Azure AD kimlik doğrulaması login.microsoftonline.com bulunan tooAzure AD, çağıran gerçekleştirilir. tooauthenticate, aşağıdaki bilgilerle toohave hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="24d65-122">Authentication against Azure AD is done by calling out tooAzure AD, located at login.microsoftonline.com. tooauthenticate, you need toohave hello following information:</span></span>

* <span data-ttu-id="24d65-123">Azure AD Kiracı kimliği (Merhaba ad içinde toolog kullanıyorsanız bu Azure ad, şirketinizin aynı ancak gerekli değildir genellikle hello)</span><span class="sxs-lookup"><span data-stu-id="24d65-123">Azure AD Tenant ID (hello name of that Azure AD you are using toolog in, often hello same as your company but not necessary)</span></span>
* <span data-ttu-id="24d65-124">Uygulama Kimliği (hello Azure AD uygulama oluşturma adımında taken)</span><span class="sxs-lookup"><span data-stu-id="24d65-124">Application ID (taken during hello Azure AD application creation step)</span></span>
* <span data-ttu-id="24d65-125">(Seçtiğiniz hello Azure AD uygulaması oluşturulurken) parola</span><span class="sxs-lookup"><span data-stu-id="24d65-125">Password (that you selected while creating hello Azure AD Application)</span></span>

<span data-ttu-id="24d65-126">HTTP isteği aşağıdaki hello emin tooreplace "Azure AD Kiracı kimliği", "Uygulama kimliği" ve "Parola" Merhaba doğru değerlere sahip olun.</span><span class="sxs-lookup"><span data-stu-id="24d65-126">In hello following HTTP request, make sure tooreplace "Azure AD Tenant ID", "Application ID" and "Password" with hello correct values.</span></span>

<span data-ttu-id="24d65-127">**Genel HTTP isteği:**</span><span class="sxs-lookup"><span data-stu-id="24d65-127">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="24d65-128">... (doğrulama başarılı olursa) olacak neden yanıt izleyen bir yanıt benzer toohello içinde:</span><span class="sxs-lookup"><span data-stu-id="24d65-128">... will (if authentication succeeds) result in a response similar toohello following response:</span></span>

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
<span data-ttu-id="24d65-129">(Merhaba access_token yanıt önceki hello içinde kısaltılmış tooincrease okunabilirlik edilmiştir)</span><span class="sxs-lookup"><span data-stu-id="24d65-129">(hello access_token in hello preceding response have been shortened tooincrease readability)</span></span>

<span data-ttu-id="24d65-130">**Erişim belirteci Bash kullanarak oluşturuluyor:**</span><span class="sxs-lookup"><span data-stu-id="24d65-130">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="24d65-131">**PowerShell kullanarak erişim belirteci oluşturuluyor:**</span><span class="sxs-lookup"><span data-stu-id="24d65-131">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="24d65-132">Merhaba yanıt, bir erişim belirteci, ne kadar bu belirtecin geçerli olduğu hakkında bilgi ve hangi kaynak için bu belirteci kullanabilirsiniz hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="24d65-132">hello response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="24d65-133">Merhaba erişim belirteci hello önceki HTTP çağrısında alınan tüm istek toohello için kaynak yöneticisi API'si geçirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="24d65-133">hello access token you received in hello previous HTTP call must be passed in for all request toohello Resource Manager API.</span></span> <span data-ttu-id="24d65-134">"Taşıyıcı YOUR_ACCESS_TOKEN" Merhaba değerle "Yetkilendirme" adlı bir üstbilgi değeri olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="24d65-134">You pass it as a header value named "Authorization" with hello value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="24d65-135">"Bearer" ile erişim belirtecinizi arasında Hello boşluk dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="24d65-135">Notice hello space between "Bearer" and your access token.</span></span>

<span data-ttu-id="24d65-136">HTTP sonuç yukarıda hello görüldüğü gibi hello belirteç bir belirli süre boyunca önbelleğe ve gerekir, aynı belirteci yeniden için geçerli olur.</span><span class="sxs-lookup"><span data-stu-id="24d65-136">As you can see from hello above HTTP Result, hello token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="24d65-137">Her API çağrısı için Azure ad olası tooauthenticate olsa bile, yüksek oranda verimsiz olacaktır.</span><span class="sxs-lookup"><span data-stu-id="24d65-137">Even if it is possible tooauthenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="24d65-138">Arama Resource Manager REST API'leri</span><span class="sxs-lookup"><span data-stu-id="24d65-138">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="24d65-139">Bu konuda, yalnızca birkaç API'leri tooexplain hello temel kullanımını hello REST işlemlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="24d65-139">This topic only uses a few APIs tooexplain hello basic usage of hello REST operations.</span></span> <span data-ttu-id="24d65-140">Tüm hello işlemleri hakkında daha fazla bilgi için bkz: [Azure Resource Manager REST API'leri](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="24d65-140">For information about all hello operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="24d65-141">Tüm abonelikleri listeler</span><span class="sxs-lookup"><span data-stu-id="24d65-141">List all subscriptions</span></span>
<span data-ttu-id="24d65-142">Merhaba basit işlemleri yapabileceğiniz erişebileceğiniz toolist hello kullanılabilir abonelikler biridir.</span><span class="sxs-lookup"><span data-stu-id="24d65-142">One of hello simplest operations you can do is toolist hello available subscriptions that you can access.</span></span> <span data-ttu-id="24d65-143">İstek aşağıdaki hello nasıl hello erişim belirteci başlık olarak geçirilen bakın:</span><span class="sxs-lookup"><span data-stu-id="24d65-143">In hello following request, you see how hello access token is passed in as a header:</span></span>

<span data-ttu-id="24d65-144">(YOUR_ACCESS_TOKEN, gerçek erişim belirteci ile değiştirin.)</span><span class="sxs-lookup"><span data-stu-id="24d65-144">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="24d65-145">... ve sonuç olarak, bu hizmet sorumlusu tooaccess izin verildiğini Aboneliklerin listesini alın</span><span class="sxs-lookup"><span data-stu-id="24d65-145">... and as a result, you get a list of subscriptions that this service principal is allowed tooaccess</span></span>

<span data-ttu-id="24d65-146">(Abonelik kimlikleri okunabilirlik için kısaltılmıştır)</span><span class="sxs-lookup"><span data-stu-id="24d65-146">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="24d65-147">Belirli bir Abonelikteki tüm kaynak gruplarının listesi</span><span class="sxs-lookup"><span data-stu-id="24d65-147">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="24d65-148">Bir kaynak grubu içinde hello Resource Manager API'leri ile tüm kaynaklar yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="24d65-148">All resources available with hello Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="24d65-149">Resource Manager için mevcut kaynak grupları aboneliğinizi HTTP GET isteği aşağıdaki hello kullanarak sorgulama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24d65-149">You can query Resource Manager for existing resource groups in your subscription using hello following HTTP GET request.</span></span> <span data-ttu-id="24d65-150">Nasıl hello abonelik kimliği hello URL'SİNİN bir parçası bu süre geçirilen dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="24d65-150">Notice how hello subscription ID is passed in as part of hello URL this time.</span></span>

<span data-ttu-id="24d65-151">(YOUR_ACCESS_TOKEN ve ABONELİK_KİMLİĞİ gerçek erişim belirtecini ve abonelik Kimliğinizle değiştirin)</span><span class="sxs-lookup"><span data-stu-id="24d65-151">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="24d65-152">Merhaba, get yanıtında tanımlanmış bir kaynak grubu olup olmadığına bağlıdır ve bu durumda, kaç tane.</span><span class="sxs-lookup"><span data-stu-id="24d65-152">hello response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="24d65-153">(Abonelik kimlikleri okunabilirlik için kısaltılmıştır)</span><span class="sxs-lookup"><span data-stu-id="24d65-153">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="create-a-resource-group"></a><span data-ttu-id="24d65-154">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="24d65-154">Create a resource group</span></span>
<span data-ttu-id="24d65-155">Şu ana kadar biz yalnızca bilgi için Resource Manager API'leri hello sorgulama.</span><span class="sxs-lookup"><span data-stu-id="24d65-155">So far, we've only been querying hello Resource Manager APIs for information.</span></span> <span data-ttu-id="24d65-156">Biz bazı kaynaklar oluşturabilir ve hello bunları tümü, bir kaynak grubu kolay başlayalım zamanı geldi.</span><span class="sxs-lookup"><span data-stu-id="24d65-156">It's time we create some resources, and let's start by hello simplest of them all, a resource group.</span></span> <span data-ttu-id="24d65-157">Merhaba aşağıdaki HTTP isteği bir bölge/konum tercih ettiğiniz bir kaynak grubu oluşturur ve bir etiket tooit ekler.</span><span class="sxs-lookup"><span data-stu-id="24d65-157">hello following HTTP request creates a resource group in a region/location of your choice, and adds a tag tooit.</span></span>

<span data-ttu-id="24d65-158">(YOUR_ACCESS_TOKEN, ABONELİK_KİMLİĞİ, RESOURCE_GROUP_NAME, gerçek erişim belirteci, abonelik kimliği ve hello toocreate istediğiniz kaynak grubunun adını adıyla değiştirin)</span><span class="sxs-lookup"><span data-stu-id="24d65-158">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of hello Resource Group you want toocreate)</span></span>

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

<span data-ttu-id="24d65-159">Başarılı olursa, yanıt aşağıdaki benzer toohello bir yanıt alın:</span><span class="sxs-lookup"><span data-stu-id="24d65-159">If successful, you get a response that is similar toohello following response:</span></span>

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

<span data-ttu-id="24d65-160">Azure'da bir kaynak grubu başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="24d65-160">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="24d65-161">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="24d65-161">Congratulations!</span></span>

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="24d65-162">Resource Manager şablonu kullanarak kaynak tooa kaynak grubu dağıtma</span><span class="sxs-lookup"><span data-stu-id="24d65-162">Deploy resources tooa resource group using a Resource Manager Template</span></span>
<span data-ttu-id="24d65-163">Resource Manager ile şablonları kullanarak kaynaklarınızı dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24d65-163">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="24d65-164">Bir şablonu bazı kaynaklar ve bağımlılıklarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="24d65-164">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="24d65-165">Bu bölüm için Resource Manager şablonları hakkında bilginiz ve yalnızca nasıl toomake hello API çağrısı toostart dağıtım gösteriyoruz varsayıyoruz.</span><span class="sxs-lookup"><span data-stu-id="24d65-165">For this section, we assume you are familiar with Resource Manager templates, and we just show you how toomake hello API call toostart deployment.</span></span> <span data-ttu-id="24d65-166">Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="24d65-166">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="24d65-167">Dağıtım şablonu, diğer API'leri çağırmak kadar toohow farklı değil.</span><span class="sxs-lookup"><span data-stu-id="24d65-167">Deployment of a template doesn't differ much toohow you call other APIs.</span></span> <span data-ttu-id="24d65-168">Önemli bir özelliği, bir şablon dağıtımını oldukça uzun zaman alabilir ' dir.</span><span class="sxs-lookup"><span data-stu-id="24d65-168">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="24d65-169">Merhaba API çağrısı yalnızca döndürür ve hello dağıtım yapıldığında, tooyou hello dağıtım toofind durumunu Geliştirici tooquery gibidir.</span><span class="sxs-lookup"><span data-stu-id="24d65-169">hello API call just returns, and it's up tooyou as developer tooquery for status of hello deployment toofind out when hello deployment is done.</span></span> <span data-ttu-id="24d65-170">Daha fazla bilgi için bkz: [izlemek zaman uyumsuz Azure işlemleri](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="24d65-170">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="24d65-171">Bu örnekte, kullanılabilir bir genel olarak sunulan şablon kullanırız [GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="24d65-171">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="24d65-172">Merhaba şablon kullandığımız bir Linux VM toohello Batı ABD bölgesi dağıtır.</span><span class="sxs-lookup"><span data-stu-id="24d65-172">hello template we use deploys a Linux VM toohello West US region.</span></span> <span data-ttu-id="24d65-173">Bu örnek, GitHub gibi ortak bir havuzda kullanılabilir bir şablonu kullanıyor olsa bile, bunun yerine hello tam şablon hello isteğin bir parçası geçiş yapabilir.</span><span class="sxs-lookup"><span data-stu-id="24d65-173">Even though this example uses a template available in a public repository like GitHub, you can instead pass hello full template as part of hello request.</span></span> <span data-ttu-id="24d65-174">Merhaba içinde kullanılan parametre değerlerini hello isteğindeki sağladığımız Not şablonu dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="24d65-174">Note that we provide parameter values in hello request that are used inside hello deployed template.</span></span>

<span data-ttu-id="24d65-175">(ABONELİK_KİMLİĞİ, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD ve DNS_NAME_FOR_PUBLIC_IP toovalues isteğiniz uygun değiştirin)</span><span class="sxs-lookup"><span data-stu-id="24d65-175">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP toovalues appropriate for your request)</span></span>

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

<span data-ttu-id="24d65-176">Bu istek için uzun JSON yanıt Hello belirtilmemişse tooimprove okunabilirlik bu belgelerin olmuştur.</span><span class="sxs-lookup"><span data-stu-id="24d65-176">hello long JSON response for this request has been omitted tooimprove readability of this documentation.</span></span> <span data-ttu-id="24d65-177">Merhaba yanıt oluşturduğunuz hello şablonlu dağıtımı hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="24d65-177">hello response contains information about hello templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24d65-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="24d65-178">Next steps</span></span>

- <span data-ttu-id="24d65-179">zaman uyumsuz REST işlemlerini işleme hakkında toolearn bkz [izlemek zaman uyumsuz Azure işlemleri](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="24d65-179">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
