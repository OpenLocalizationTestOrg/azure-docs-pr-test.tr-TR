---
title: Mobile Engagement REST API'leri ile aaaAuthenticate
description: "Açıklar nasıl Azure Mobile Engagement REST API'leri ile tooauthenticate"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 9b54aa5ec3da4bcf55ffe5b7e8d1759095d0c486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a><span data-ttu-id="cc504-103">Mobil katılım REST API'leri ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="cc504-103">Authenticate with Mobile Engagement REST APIs</span></span>
## <a name="overview"></a><span data-ttu-id="cc504-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="cc504-104">Overview</span></span>
<span data-ttu-id="cc504-105">Bu belgede nasıl tooget geçerli bir AAD Oauth belirteci hello Mobile Engagement REST API'leri ile tooauthenticate açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cc504-105">This document describes how tooget a valid AAD Oauth token tooauthenticate with hello Mobile Engagement REST APIs.</span></span> 

<span data-ttu-id="cc504-106">Geçerli bir Azure aboneliğinizin olması ve aşağıdakilerden birini kullanarak bir Mobile Engagement uygulaması oluşturdunuz varsayılır bizim [Geliştirici öğreticileri](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cc504-106">It is assumed that you have a valid Azure subscription and you have created a Mobile Engagement app using one of our [Developer Tutorials](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="cc504-107">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="cc504-107">Authentication</span></span>
<span data-ttu-id="cc504-108">Bir Microsoft Azure Active Directory token kimlik doğrulaması için kullanılan OAuth tabanlı.</span><span class="sxs-lookup"><span data-stu-id="cc504-108">A Microsoft Azure Active Directory based OAuth token is used for authentication.</span></span> 

<span data-ttu-id="cc504-109">Sipariş tooauthentication bir API istekte bir authorization üstbilgisi form aşağıdaki Merhaba tooevery isteği eklenmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="cc504-109">In order tooauthentication an API request, an authorization header must be added tooevery request which is of hello following form:</span></span>

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> <span data-ttu-id="cc504-110">Azure Active Directory belirteçleri 1 saat içinde süresi dolacak.</span><span class="sxs-lookup"><span data-stu-id="cc504-110">Azure Active Directory tokens expire in 1 hour.</span></span>
> 
> 

<span data-ttu-id="cc504-111">Bir belirteç birkaç yolu tooget vardır.</span><span class="sxs-lookup"><span data-stu-id="cc504-111">There are several ways tooget a token.</span></span> <span data-ttu-id="cc504-112">API genellikle bir bulut hizmetinden adlı hello itibaren toouse bir API anahtarı istiyor.</span><span class="sxs-lookup"><span data-stu-id="cc504-112">Since hello APIs are generally called from a cloud service, you want toouse an API key.</span></span> <span data-ttu-id="cc504-113">API anahtarını Azure terminolojisi içinde bir hizmet asıl parola adı verilir.</span><span class="sxs-lookup"><span data-stu-id="cc504-113">An API key in Azure terminology is called a Service principal password.</span></span> <span data-ttu-id="cc504-114">Merhaba aşağıdaki yordamda açıklanmıştır tek yönlü toosetting onu el ile ayarlama.</span><span class="sxs-lookup"><span data-stu-id="cc504-114">hello following procedure describes one way toosetting it up manually.</span></span>

### <a name="one-time-setup-using-script"></a><span data-ttu-id="cc504-115">Tek seferlik kurulumu (kod kullanılarak)</span><span class="sxs-lookup"><span data-stu-id="cc504-115">One-time setup (using script)</span></span>
<span data-ttu-id="cc504-116">Merhaba kümesi hello kurulum için en az zaman alır, ancak hello en izin verilen varsayılanlarını kullanır bir PowerShell komut dosyası kullanarak tooperform hello Kurulum aşağıdaki yönergeleri izlemelidir.</span><span class="sxs-lookup"><span data-stu-id="cc504-116">You should follow hello set of instructions below tooperform hello setup using a PowerShell script which takes hello minimum time for setup but uses hello most permissible defaults.</span></span> <span data-ttu-id="cc504-117">İsteğe bağlı olarak, ayrıca hello hello yönergelerini izleyebilirsiniz [el ile kuruluma](mobile-engagement-api-authentication-manual.md) hello doğrudan Azure portal ve yüksekse yapılandırma bunu.</span><span class="sxs-lookup"><span data-stu-id="cc504-117">Optionally, you can also follow hello instructions in hello [manual setup](mobile-engagement-api-authentication-manual.md) for doing this from hello Azure portal directly and do finer configuration.</span></span> 

1. <span data-ttu-id="cc504-118">Merhaba Azure PowerShell'in en son sürümünü almak [burada](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="cc504-118">Get hello latest version of Azure PowerShell from [here](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="cc504-119">Bu bkz hello yükleme yönergeleri ile ilgili daha fazla bilgi için [bağlantı](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cc504-119">For more information on hello download instructions, you can see this [link](/powershell/azure/overview).</span></span>  
2. <span data-ttu-id="cc504-120">Azure PowerShell yüklendikten sonra hello sahip tooensure kullanım hello aşağıdaki komutları **Azure Modülü** yüklü:</span><span class="sxs-lookup"><span data-stu-id="cc504-120">Once Azure PowerShell is installed, use hello following commands tooensure that you have hello **Azure module** installed:</span></span>
   
    <span data-ttu-id="cc504-121">a.</span><span class="sxs-lookup"><span data-stu-id="cc504-121">a.</span></span> <span data-ttu-id="cc504-122">Hello Azure PowerShell modülü hello kullanılabilir modülleri listesinde kullanılabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="cc504-122">Make sure hello Azure PowerShell module is available in hello list of available modules.</span></span> 
   
        Get-Module –ListAvailable 
   
    ![Mevcut Azure modülleri][1]
   
    <span data-ttu-id="cc504-124">b.</span><span class="sxs-lookup"><span data-stu-id="cc504-124">b.</span></span> <span data-ttu-id="cc504-125">Merhaba listesinin içinde hello Azure PowerShell modülü bulamazsanız toorun hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="cc504-125">If you do not find hello Azure PowerShell module in hello above list then you need toorun hello following:</span></span>
   
        Import-Module Azure 
3. <span data-ttu-id="cc504-126">Çalıştırarak oturum açma toohello Azure Kaynak Yöneticisi'nden PowerShell komutunu aşağıdaki ve Azure hesabınız için kullanıcı adı ve parola sağlayarak hello:</span><span class="sxs-lookup"><span data-stu-id="cc504-126">Login toohello Azure Resource Manager from PowerShell by running hello following command and providing your user name and password for your Azure account:</span></span> 
   
        Login-AzureRmAccount
4. <span data-ttu-id="cc504-127">Birden çok aboneliğiniz varsa, hello aşağıdaki değeri çalıştırmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="cc504-127">If you have multiple subscriptions then you should run hello following:</span></span>
   
    <span data-ttu-id="cc504-128">a.</span><span class="sxs-lookup"><span data-stu-id="cc504-128">a.</span></span> <span data-ttu-id="cc504-129">Tüm abonelikleri ve kopyalama hello Subscriptionıd istediğiniz hello aboneliğin listesini toouse alın.</span><span class="sxs-lookup"><span data-stu-id="cc504-129">Get a list of all your subscriptions and copy hello SubscriptionId of hello subscription you want toouse.</span></span> <span data-ttu-id="cc504-130">Bu abonelik aynı olan hello adımıdır mobil katılım uygulamasını hello olduğundan emin olun kullanarak toointeract hello API'leri.</span><span class="sxs-lookup"><span data-stu-id="cc504-130">Make sure this subscription is hello same one which has hello Mobile Engagement App which you are going toointeract with using hello APIs.</span></span> 
   
        Get-AzureRmSubscription
   
    <span data-ttu-id="cc504-131">b.</span><span class="sxs-lookup"><span data-stu-id="cc504-131">b.</span></span> <span data-ttu-id="cc504-132">Çalışma hello aşağıdaki kullanılan sağlayan hello Subscriptionıd tooconfigure hello abonelik toobe komutu.</span><span class="sxs-lookup"><span data-stu-id="cc504-132">Run hello following command providing hello SubscriptionId tooconfigure hello subscription toobe used.</span></span>
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. <span data-ttu-id="cc504-133">Merhaba Hello metni kopyalayın [yeni AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) tooyour yerel makine komut dosyası ve bir PowerShell cmdlet'ini olarak kaydedin (örneğin `APIAuth.ps1`) ve bu yürütme `.\APIAuth.ps1`.</span><span class="sxs-lookup"><span data-stu-id="cc504-133">Copy hello text for hello [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script tooyour local machine and save it as a PowerShell cmdlet (e.g. `APIAuth.ps1`) and execute it `.\APIAuth.ps1`.</span></span> 
6. <span data-ttu-id="cc504-134">Merhaba komut dosyası, giriş için bir tooprovide ister **principalName**.</span><span class="sxs-lookup"><span data-stu-id="cc504-134">hello script will ask you tooprovide an input for **principalName**.</span></span> <span data-ttu-id="cc504-135">Active Directory uygulamanız (örneğin APIAuth) toouse toocreate istediğiniz uygun bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="cc504-135">Provide a suitable name here that you want toouse toocreate your Active Directory application (e.g. APIAuth).</span></span> 
7. <span data-ttu-id="cc504-136">Merhaba betik tamamlandıktan sonra ihtiyacınız olacak dört değerleri aşağıdaki hello görüntülenir tooauthenticate program aracılığıyla AD ile nedenle emin toocopy olun bunları.</span><span class="sxs-lookup"><span data-stu-id="cc504-136">After hello script completes, it will display hello following four values that you will need tooauthenticate programmatically with AD so make sure toocopy them.</span></span> 
   
    <span data-ttu-id="cc504-137">**Tenantıd**, **Subscriptionıd**, **ApplicationId**, ve **gizli**.</span><span class="sxs-lookup"><span data-stu-id="cc504-137">**TenantId**, **SubscriptionId**, **ApplicationId**, and **Secret**.</span></span>
   
    <span data-ttu-id="cc504-138">Tenantıd olarak kullanacağınız `{TENANT_ID}`, ApplicationId olarak `{CLIENT_ID}` ve gizli olarak `{CLIENT_SECRET}`.</span><span class="sxs-lookup"><span data-stu-id="cc504-138">You will use TenantId as `{TENANT_ID}`, ApplicationId as `{CLIENT_ID}` and Secret as `{CLIENT_SECRET}`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cc504-139">Varsayılan güvenlik ilkenizin bir PowerShell komut dosyalarının çalışmasını engelleyebilir.</span><span class="sxs-lookup"><span data-stu-id="cc504-139">Your default security policy may block you from running a PowerShell scripts.</span></span> <span data-ttu-id="cc504-140">Gerekiyorsa, komutu aşağıdaki hello kullanarak, yürütme İlkesi tooallow komut dosyası yürütme geçici olarak yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="cc504-140">If so, you temporarily configure your execution policy tooallow script execution using hello following command:</span></span>
   > 
   > <span data-ttu-id="cc504-141">Set-ExecutionPolicy RemoteSigned</span><span class="sxs-lookup"><span data-stu-id="cc504-141">Set-ExecutionPolicy RemoteSigned</span></span>
   > 
   > 
8. <span data-ttu-id="cc504-142">İşte nasıl hello PS cmdlet'leri kümesini aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="cc504-142">Here is how hello set of PS cmdlets would look like.</span></span> 
   
    ![][3]
9. <span data-ttu-id="cc504-143">Hello Azure Yönetim Portalı'nda toohello komut dosyasının sağlanan yeni bir AD uygulamasını hello adıyla, oluşturulduğunu denetleyin **principalName** altında **Şirketimin sahip olduğu uygulamalar Göster**.</span><span class="sxs-lookup"><span data-stu-id="cc504-143">Check in hello Azure Management portal that a new AD application was created with hello name you provided toohello script called **principalName** under **Show Applications my company owns**.</span></span>
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a><span data-ttu-id="cc504-144">Adımları tooget geçerli bir belirteci</span><span class="sxs-lookup"><span data-stu-id="cc504-144">Steps tooget a valid token</span></span>
1. <span data-ttu-id="cc504-145">Şu parametreler hello ile Merhaba API çağrısı ve emin tooreplace hello KİRACI olun\_kimliği, istemci\_kimliği ve istemci\_gizli anahtarı:</span><span class="sxs-lookup"><span data-stu-id="cc504-145">Call hello API with hello following parameters and make sure tooreplace hello TENANT\_ID, CLIENT\_ID and CLIENT\_SECRET:</span></span>
   
   * <span data-ttu-id="cc504-146">**İstek URL'si** olarak *https://login.microsoftonline.com/ {KİRACI\_kimliği} / oauth2/belirteci*</span><span class="sxs-lookup"><span data-stu-id="cc504-146">**Request URL** as *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span></span>
   * <span data-ttu-id="cc504-147">**HTTP Content-Type üstbilgisi** olarak *uygulama/x-www-form-urlencoded*</span><span class="sxs-lookup"><span data-stu-id="cc504-147">**HTTP Content-Type header** as *application/x-www-form-urlencoded*</span></span>
   * <span data-ttu-id="cc504-148">**HTTP isteği gövdesinin** olarak *vermek\_türü = istemci\_kimlik bilgileri & client_id = {istemci\_kimliği} & client_secret = {istemci\_gizli} & resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span><span class="sxs-lookup"><span data-stu-id="cc504-148">**HTTP Request Body** as *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span></span>
     
     <span data-ttu-id="cc504-149">Merhaba, bir örnek isteği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="cc504-149">hello following is an example request:</span></span>
     
       <span data-ttu-id="cc504-150">POST / {TENANT_ID} / oauth2/token HTTP/1.1 ana: login.microsoftonline.com Content-Type: uygulama/x-www-form-urlencoded grant_type client_credentials & client_id = {CLIENT_ID} = & client_secret {CLIENT_SECRET} = & çözüm kaynağına https % 3A % = 2f%2Fmanagement.Core.Windows.NET%2f</span><span class="sxs-lookup"><span data-stu-id="cc504-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span></span>
     
     <span data-ttu-id="cc504-151">Bir örnek yanıt şöyledir:</span><span class="sxs-lookup"><span data-stu-id="cc504-151">Here is an example response:</span></span>
     
       <span data-ttu-id="cc504-152">HTTP/1.1 200 Tamam Content-Type: uygulama/json; Charset = utf-8 İçerik-Uzunluk: 1234</span><span class="sxs-lookup"><span data-stu-id="cc504-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span></span>
     
       <span data-ttu-id="cc504-153">{"token_type": "Bearer", "expires_in": "3599", "expires_on": "1445395811", "not_before": "144 5391911","kaynak": "https://management.core.windows.net/", "access_token": {ACCESS_TOKEN}}</span><span class="sxs-lookup"><span data-stu-id="cc504-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span></span>
     
     <span data-ttu-id="cc504-154">Bu örnek hello POST parametrelerinin URL kodlaması dahil `resource` değerdir gerçekten `https://management.core.windows.net/`.</span><span class="sxs-lookup"><span data-stu-id="cc504-154">This example included URL encoding of hello POST parameters, `resource` value is actually `https://management.core.windows.net/`.</span></span> <span data-ttu-id="cc504-155">Tooalso URL kodlama dikkatli olun `{CLIENT_SECRET}` gibi özel karakterleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="cc504-155">Be careful tooalso URL encode `{CLIENT_SECRET}` as it may contain special characters.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="cc504-156">Test etmek için bir HTTP istemci aracı gibi kullanabilirsiniz [Fiddler](http://www.telerik.com/fiddler) veya [Chrome Postman uzantısı](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span><span class="sxs-lookup"><span data-stu-id="cc504-156">For testing, you can use an HTTP client tool like [Fiddler](http://www.telerik.com/fiddler) or [Chrome Postman extension](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span></span> 
     > 
     > 
2. <span data-ttu-id="cc504-157">Artık her API çağrısı hello yetkilendirme istek üstbilgisi içerir:</span><span class="sxs-lookup"><span data-stu-id="cc504-157">Now in every API call, include hello authorization request header:</span></span>
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    <span data-ttu-id="cc504-158">Döndürülen, 401 durum kodu onay hello yanıt gövdesi alırsanız, hello belirtecinin süresi size.</span><span class="sxs-lookup"><span data-stu-id="cc504-158">If you get a 401 status code returned, check hello response body, it might tell you hello token is expired.</span></span> <span data-ttu-id="cc504-159">Bu durumda, yeni belirteç alın.</span><span class="sxs-lookup"><span data-stu-id="cc504-159">In that case, get a new token.</span></span>

## <a name="using-hello-apis"></a><span data-ttu-id="cc504-160">Merhaba API kullanma</span><span class="sxs-lookup"><span data-stu-id="cc504-160">Using hello APIs</span></span>
<span data-ttu-id="cc504-161">Geçerli bir belirteci sahip olduğunuza göre hazır toomake hello API çağrıları aynıdır.</span><span class="sxs-lookup"><span data-stu-id="cc504-161">Now that you have a valid token, you are ready toomake hello API calls.</span></span>

1. <span data-ttu-id="cc504-162">Her API isteği toopass hello önceki bölümde edindiğiniz bir geçerli, süresi dolmamış belirteci gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc504-162">In each API request, you will need toopass a valid, unexpired token which you obtained in hello previous section.</span></span>
2. <span data-ttu-id="cc504-163">Bazı parametreler tooplug hello isteği uygulamanızı tanımlayan URI gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc504-163">You will need tooplug in some parameters into hello request URI which identifies your application.</span></span> <span data-ttu-id="cc504-164">Merhaba isteğin URI hello aşağıdaki gibi görünür</span><span class="sxs-lookup"><span data-stu-id="cc504-164">hello request URI looks like hello following</span></span>
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    <span data-ttu-id="cc504-165">tooget hello parametreleri, uygulama adınız ve Pano'e tıklayın ve tüm hello aşağıdakilerle 3 parametre hello gibi bir sayfa görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="cc504-165">tooget hello parameters, click on your application name and click Dashboard and you will see a page like hello following with all hello 3 parameters.</span></span>
   
   * <span data-ttu-id="cc504-166">**1** `{subscription-id}`</span><span class="sxs-lookup"><span data-stu-id="cc504-166">**1** `{subscription-id}`</span></span>
   * <span data-ttu-id="cc504-167">**2** `{app-collection}`</span><span class="sxs-lookup"><span data-stu-id="cc504-167">**2** `{app-collection}`</span></span>
   * <span data-ttu-id="cc504-168">**3** `{app-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="cc504-168">**3** `{app-resource-name}`</span></span>
   * <span data-ttu-id="cc504-169">**4** bilgisayarınızı kaynak grubu adı toobe giderek **MobileEngagement** yeni bir tane oluşturduğunuz sürece.</span><span class="sxs-lookup"><span data-stu-id="cc504-169">**4** Your Resource Group name is going toobe **MobileEngagement** unless you created a new one.</span></span> 
     
     ![Mobile Engagement API URI parametreleri][2]

> [!NOTE]
> <br/>
> 
> 1. <span data-ttu-id="cc504-171">Merhaba, bu gibi hello API kök adresi yoksay önceki API'leri.</span><span class="sxs-lookup"><span data-stu-id="cc504-171">Ignore hello API Root Address as this was for hello previous APIs.</span></span><br/>
> 2. <span data-ttu-id="cc504-172">Daha sonra Klasik Azure portalını kullanarak hello uygulama oluşturduysanız hello uygulama adından kendisini farklı toouse hello Uygulama kaynağı adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc504-172">If you created hello app using Azure Classic portal then you need toouse hello Application Resource name which is different than hello Application name itself.</span></span> <span data-ttu-id="cc504-173">Hello Azure Portal hello uygulama oluşturduysanız hello uygulama adının kendisi (Uygulama kaynağı adı ve hello yeni portalında oluşturulan uygulamalar için uygulama adı arasında hiçbir ayrım yoktur) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc504-173">If you created hello app in hello Azure Portal then you should use hello App Name itself (there is no differentiation between Application Resource Name and App Name for apps created in hello new portal).</span></span>  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



