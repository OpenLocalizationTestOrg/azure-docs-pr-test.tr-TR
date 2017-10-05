---
title: "Mobil katılım REST API'leri ile kimlik doğrulaması"
description: "Azure Mobile Engagement REST API'leri ile kimlik doğrulaması açıklar"
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
ms.openlocfilehash: b05181d9252c0a804648e01b4058019278ae5abe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a><span data-ttu-id="d76b9-103">Mobil katılım REST API'leri ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d76b9-103">Authenticate with Mobile Engagement REST APIs</span></span>
## <a name="overview"></a><span data-ttu-id="d76b9-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d76b9-104">Overview</span></span>
<span data-ttu-id="d76b9-105">Bu belge, geçerli bir AAD Oauth Mobile Engagement REST API'leri ile kimlik doğrulaması belirteci alma açıklar.</span><span class="sxs-lookup"><span data-stu-id="d76b9-105">This document describes how to get a valid AAD Oauth token to authenticate with the Mobile Engagement REST APIs.</span></span> 

<span data-ttu-id="d76b9-106">Geçerli bir Azure aboneliğinizin olması ve aşağıdakilerden birini kullanarak bir Mobile Engagement uygulaması oluşturdunuz varsayılır bizim [Geliştirici öğreticileri](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d76b9-106">It is assumed that you have a valid Azure subscription and you have created a Mobile Engagement app using one of our [Developer Tutorials](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="d76b9-107">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d76b9-107">Authentication</span></span>
<span data-ttu-id="d76b9-108">Bir Microsoft Azure Active Directory token kimlik doğrulaması için kullanılan OAuth tabanlı.</span><span class="sxs-lookup"><span data-stu-id="d76b9-108">A Microsoft Azure Active Directory based OAuth token is used for authentication.</span></span> 

<span data-ttu-id="d76b9-109">Kimlik doğrulaması bir API isteğinin sırada bir authorization üstbilgisi aşağıdaki biçimi olan her istek için eklenmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="d76b9-109">In order to authentication an API request, an authorization header must be added to every request which is of the following form:</span></span>

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> <span data-ttu-id="d76b9-110">Azure Active Directory belirteçleri 1 saat içinde süresi dolacak.</span><span class="sxs-lookup"><span data-stu-id="d76b9-110">Azure Active Directory tokens expire in 1 hour.</span></span>
> 
> 

<span data-ttu-id="d76b9-111">Bir belirteç almak üzere birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="d76b9-111">There are several ways to get a token.</span></span> <span data-ttu-id="d76b9-112">API'ler genellikle bir bulut hizmetinden adlı olduğundan, bir API anahtarı kullanmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="d76b9-112">Since the APIs are generally called from a cloud service, you want to use an API key.</span></span> <span data-ttu-id="d76b9-113">API anahtarını Azure terminolojisi içinde bir hizmet asıl parola adı verilir.</span><span class="sxs-lookup"><span data-stu-id="d76b9-113">An API key in Azure terminology is called a Service principal password.</span></span> <span data-ttu-id="d76b9-114">El ile ayarlama bir yolu aşağıdaki yordamda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d76b9-114">The following procedure describes one way to setting it up manually.</span></span>

### <a name="one-time-setup-using-script"></a><span data-ttu-id="d76b9-115">Tek seferlik kurulumu (kod kullanılarak)</span><span class="sxs-lookup"><span data-stu-id="d76b9-115">One-time setup (using script)</span></span>
<span data-ttu-id="d76b9-116">Kurulum için en az zaman alır, ancak en izin verilen Varsayılanları kullanan bir PowerShell Betiği kullanılarak Kurulumu gerçekleştirmek için aşağıdaki yönergeleri kümesi izlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="d76b9-116">You should follow the set of instructions below to perform the setup using a PowerShell script which takes the minimum time for setup but uses the most permissible defaults.</span></span> <span data-ttu-id="d76b9-117">İsteğe bağlı olarak, aynı zamanda yönergelerini izleyebilirsiniz [el ile kuruluma](mobile-engagement-api-authentication-manual.md) doğrudan Azure portal ve yüksekse yapılandırma bunu.</span><span class="sxs-lookup"><span data-stu-id="d76b9-117">Optionally, you can also follow the instructions in the [manual setup](mobile-engagement-api-authentication-manual.md) for doing this from the Azure portal directly and do finer configuration.</span></span> 

1. <span data-ttu-id="d76b9-118">Azure PowerShell en son sürümünü alın [burada](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="d76b9-118">Get the latest version of Azure PowerShell from [here](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="d76b9-119">Yükleme yönergeleri ile ilgili daha fazla bilgi için bu gördüğünüz [bağlantı](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d76b9-119">For more information on the download instructions, you can see this [link](/powershell/azure/overview).</span></span>  
2. <span data-ttu-id="d76b9-120">Azure PowerShell yüklendikten sonra sahip olduğunuzdan emin olmak için aşağıdaki komutları kullanın **Azure Modülü** yüklü:</span><span class="sxs-lookup"><span data-stu-id="d76b9-120">Once Azure PowerShell is installed, use the following commands to ensure that you have the **Azure module** installed:</span></span>
   
    <span data-ttu-id="d76b9-121">a.</span><span class="sxs-lookup"><span data-stu-id="d76b9-121">a.</span></span> <span data-ttu-id="d76b9-122">Azure PowerShell modülü mevcut modülleri, listesinde kullanılabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d76b9-122">Make sure the Azure PowerShell module is available in the list of available modules.</span></span> 
   
        Get-Module –ListAvailable 
   
    ![Mevcut Azure modülleri][1]
   
    <span data-ttu-id="d76b9-124">b.</span><span class="sxs-lookup"><span data-stu-id="d76b9-124">b.</span></span> <span data-ttu-id="d76b9-125">Azure PowerShell modülü yukarıdaki listede bulamazsanız, aşağıdaki çalıştırmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d76b9-125">If you do not find the Azure PowerShell module in the above list then you need to run the following:</span></span>
   
        Import-Module Azure 
3. <span data-ttu-id="d76b9-126">Oturum açma için Azure kaynak yöneticisi için aşağıdaki komutu çalıştırın ve Azure hesabınız için kullanıcı adı ve parola sağlayarak powershell'den:</span><span class="sxs-lookup"><span data-stu-id="d76b9-126">Login to the Azure Resource Manager from PowerShell by running the following command and providing your user name and password for your Azure account:</span></span> 
   
        Login-AzureRmAccount
4. <span data-ttu-id="d76b9-127">Birden çok aboneliğiniz varsa sonra aşağıdaki çalıştırmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d76b9-127">If you have multiple subscriptions then you should run the following:</span></span>
   
    <span data-ttu-id="d76b9-128">a.</span><span class="sxs-lookup"><span data-stu-id="d76b9-128">a.</span></span> <span data-ttu-id="d76b9-129">Tüm aboneliklerinizi listesini almak ve kullanmak istediğiniz aboneliği Subscriptionıd kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d76b9-129">Get a list of all your subscriptions and copy the SubscriptionId of the subscription you want to use.</span></span> <span data-ttu-id="d76b9-130">Bu abonelik API'leri kullanılarak ile etkileşimde olacak mobil katılım uygulamasını olduğu adla aynı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d76b9-130">Make sure this subscription is the same one which has the Mobile Engagement App which you are going to interact with using the APIs.</span></span> 
   
        Get-AzureRmSubscription
   
    <span data-ttu-id="d76b9-131">b.</span><span class="sxs-lookup"><span data-stu-id="d76b9-131">b.</span></span> <span data-ttu-id="d76b9-132">Kullanılacak aboneliği yapılandırmak için Subscriptionıd sağlayarak aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d76b9-132">Run the following command providing the SubscriptionId to configure the subscription to be used.</span></span>
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. <span data-ttu-id="d76b9-133">Metni kopyalayın [yeni AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) yerel makinenize betik ve PowerShell cmdlet'ini olarak kaydedin (örneğin `APIAuth.ps1`) ve bu yürütme `.\APIAuth.ps1`.</span><span class="sxs-lookup"><span data-stu-id="d76b9-133">Copy the text for the [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script to your local machine and save it as a PowerShell cmdlet (e.g. `APIAuth.ps1`) and execute it `.\APIAuth.ps1`.</span></span> 
6. <span data-ttu-id="d76b9-134">Komut dosyası için bir giriş sağlama ister **principalName**.</span><span class="sxs-lookup"><span data-stu-id="d76b9-134">The script will ask you to provide an input for **principalName**.</span></span> <span data-ttu-id="d76b9-135">Active Directory uygulamanız (örneğin APIAuth) oluşturmak için kullanmak istediğiniz uygun bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="d76b9-135">Provide a suitable name here that you want to use to create your Active Directory application (e.g. APIAuth).</span></span> 
7. <span data-ttu-id="d76b9-136">Komut dosyası tamamlandıktan sonra aşağıdaki görüntüleyecektir program aracılığıyla AD ile kimlik doğrulaması için gereken dört değerden böylece bunları kopyalamak emin olun.</span><span class="sxs-lookup"><span data-stu-id="d76b9-136">After the script completes, it will display the following four values that you will need to authenticate programmatically with AD so make sure to copy them.</span></span> 
   
    <span data-ttu-id="d76b9-137">**Tenantıd**, **Subscriptionıd**, **ApplicationId**, ve **gizli**.</span><span class="sxs-lookup"><span data-stu-id="d76b9-137">**TenantId**, **SubscriptionId**, **ApplicationId**, and **Secret**.</span></span>
   
    <span data-ttu-id="d76b9-138">Tenantıd olarak kullanacağınız `{TENANT_ID}`, ApplicationId olarak `{CLIENT_ID}` ve gizli olarak `{CLIENT_SECRET}`.</span><span class="sxs-lookup"><span data-stu-id="d76b9-138">You will use TenantId as `{TENANT_ID}`, ApplicationId as `{CLIENT_ID}` and Secret as `{CLIENT_SECRET}`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d76b9-139">Varsayılan güvenlik ilkenizin bir PowerShell komut dosyalarının çalışmasını engelleyebilir.</span><span class="sxs-lookup"><span data-stu-id="d76b9-139">Your default security policy may block you from running a PowerShell scripts.</span></span> <span data-ttu-id="d76b9-140">Bu durumda, geçici olarak komut dosyası yürütme aşağıdaki komutu kullanarak izin vermek için yürütme ilkesi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="d76b9-140">If so, you temporarily configure your execution policy to allow script execution using the following command:</span></span>
   > 
   > <span data-ttu-id="d76b9-141">Set-ExecutionPolicy RemoteSigned</span><span class="sxs-lookup"><span data-stu-id="d76b9-141">Set-ExecutionPolicy RemoteSigned</span></span>
   > 
   > 
8. <span data-ttu-id="d76b9-142">İşte nasıl PS cmdlet'leri kümesini aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="d76b9-142">Here is how the set of PS cmdlets would look like.</span></span> 
   
    ![][3]
9. <span data-ttu-id="d76b9-143">Azure Yönetim Portalı'nda yeni bir AD uygulamasını adlı komut dosyasına verdiğiniz adla oluşturulduğunu denetleyin **principalName** altında **Şirketimin sahip olduğu uygulamalar Göster**.</span><span class="sxs-lookup"><span data-stu-id="d76b9-143">Check in the Azure Management portal that a new AD application was created with the name you provided to the script called **principalName** under **Show Applications my company owns**.</span></span>
   
    ![][4]

#### <a name="steps-to-get-a-valid-token"></a><span data-ttu-id="d76b9-144">Geçerli bir belirteci almak için adımlar</span><span class="sxs-lookup"><span data-stu-id="d76b9-144">Steps to get a valid token</span></span>
1. <span data-ttu-id="d76b9-145">API aşağıdaki parametrelerle çağırın ve KİRACI değiştirdiğinizden emin olun\_kimliği, istemci\_kimliği ve istemci\_gizli anahtarı:</span><span class="sxs-lookup"><span data-stu-id="d76b9-145">Call the API with the following parameters and make sure to replace the TENANT\_ID, CLIENT\_ID and CLIENT\_SECRET:</span></span>
   
   * <span data-ttu-id="d76b9-146">**İstek URL'si** olarak *https://login.microsoftonline.com/ {KİRACI\_kimliği} / oauth2/belirteci*</span><span class="sxs-lookup"><span data-stu-id="d76b9-146">**Request URL** as *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span></span>
   * <span data-ttu-id="d76b9-147">**HTTP Content-Type üstbilgisi** olarak *uygulama/x-www-form-urlencoded*</span><span class="sxs-lookup"><span data-stu-id="d76b9-147">**HTTP Content-Type header** as *application/x-www-form-urlencoded*</span></span>
   * <span data-ttu-id="d76b9-148">**HTTP isteği gövdesinin** olarak *vermek\_türü = istemci\_kimlik bilgileri & client_id = {istemci\_kimliği} & client_secret = {istemci\_gizli} & resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span><span class="sxs-lookup"><span data-stu-id="d76b9-148">**HTTP Request Body** as *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span></span>
     
     <span data-ttu-id="d76b9-149">Bir örnek isteği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d76b9-149">The following is an example request:</span></span>
     
       <span data-ttu-id="d76b9-150">POST / {TENANT_ID} / oauth2/token HTTP/1.1 ana: login.microsoftonline.com Content-Type: uygulama/x-www-form-urlencoded grant_type client_credentials & client_id = {CLIENT_ID} = & client_secret {CLIENT_SECRET} = & çözüm kaynağına https % 3A % = 2f%2Fmanagement.Core.Windows.NET%2f</span><span class="sxs-lookup"><span data-stu-id="d76b9-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span></span>
     
     <span data-ttu-id="d76b9-151">Bir örnek yanıt şöyledir:</span><span class="sxs-lookup"><span data-stu-id="d76b9-151">Here is an example response:</span></span>
     
       <span data-ttu-id="d76b9-152">HTTP/1.1 200 Tamam Content-Type: uygulama/json; Charset = utf-8 İçerik-Uzunluk: 1234</span><span class="sxs-lookup"><span data-stu-id="d76b9-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span></span>
     
       <span data-ttu-id="d76b9-153">{"token_type": "Bearer", "expires_in": "3599", "expires_on": "1445395811", "not_before": "144 5391911","kaynak": "https://management.core.windows.net/", "access_token": {ACCESS_TOKEN}}</span><span class="sxs-lookup"><span data-stu-id="d76b9-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span></span>
     
     <span data-ttu-id="d76b9-154">Bu örnek POST parametreleri, URL kodlaması dahil `resource` değerdir gerçekten `https://management.core.windows.net/`.</span><span class="sxs-lookup"><span data-stu-id="d76b9-154">This example included URL encoding of the POST parameters, `resource` value is actually `https://management.core.windows.net/`.</span></span> <span data-ttu-id="d76b9-155">Ayrıca URL dikkatli olun kodlamak `{CLIENT_SECRET}` gibi özel karakterleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="d76b9-155">Be careful to also URL encode `{CLIENT_SECRET}` as it may contain special characters.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="d76b9-156">Test etmek için bir HTTP istemci aracı gibi kullanabilirsiniz [Fiddler](http://www.telerik.com/fiddler) veya [Chrome Postman uzantısı](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span><span class="sxs-lookup"><span data-stu-id="d76b9-156">For testing, you can use an HTTP client tool like [Fiddler](http://www.telerik.com/fiddler) or [Chrome Postman extension](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span></span> 
     > 
     > 
2. <span data-ttu-id="d76b9-157">Artık her API çağrısı yetkilendirme istek üstbilgisi içerir:</span><span class="sxs-lookup"><span data-stu-id="d76b9-157">Now in every API call, include the authorization request header:</span></span>
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    <span data-ttu-id="d76b9-158">Döndürülen bir 401 durum kodu alırsanız, yanıt gövdesini denetleyin, belirtecin süresi doldu size.</span><span class="sxs-lookup"><span data-stu-id="d76b9-158">If you get a 401 status code returned, check the response body, it might tell you the token is expired.</span></span> <span data-ttu-id="d76b9-159">Bu durumda, yeni belirteç alın.</span><span class="sxs-lookup"><span data-stu-id="d76b9-159">In that case, get a new token.</span></span>

## <a name="using-the-apis"></a><span data-ttu-id="d76b9-160">API'ler kullanma</span><span class="sxs-lookup"><span data-stu-id="d76b9-160">Using the APIs</span></span>
<span data-ttu-id="d76b9-161">Geçerli bir belirteci sahip olduğunuza göre API çağrılarını yapmaya hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="d76b9-161">Now that you have a valid token, you are ready to make the API calls.</span></span>

1. <span data-ttu-id="d76b9-162">Her API isteği önceki bölümde aldığınız bir geçerli, süresi dolmamış belirteci geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="d76b9-162">In each API request, you will need to pass a valid, unexpired token which you obtained in the previous section.</span></span>
2. <span data-ttu-id="d76b9-163">Bazı parametreler, uygulamanızın tanımlayan URI isteği içine takın gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="d76b9-163">You will need to plug in some parameters into the request URI which identifies your application.</span></span> <span data-ttu-id="d76b9-164">İstek URI'si aşağıdaki gibi görünür</span><span class="sxs-lookup"><span data-stu-id="d76b9-164">The request URI looks like the following</span></span>
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    <span data-ttu-id="d76b9-165">Parametreleri Al, uygulama adına tıklayın ve Pano ve tüm 3 parametrelerle aşağıdaki gibi bir sayfa görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d76b9-165">To get the parameters, click on your application name and click Dashboard and you will see a page like the following with all the 3 parameters.</span></span>
   
   * <span data-ttu-id="d76b9-166">**1** `{subscription-id}`</span><span class="sxs-lookup"><span data-stu-id="d76b9-166">**1** `{subscription-id}`</span></span>
   * <span data-ttu-id="d76b9-167">**2** `{app-collection}`</span><span class="sxs-lookup"><span data-stu-id="d76b9-167">**2** `{app-collection}`</span></span>
   * <span data-ttu-id="d76b9-168">**3** `{app-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="d76b9-168">**3** `{app-resource-name}`</span></span>
   * <span data-ttu-id="d76b9-169">**4** bilgisayarınızı kaynak grubu adı olması geçmeye **MobileEngagement** yeni bir tane oluşturduğunuz sürece.</span><span class="sxs-lookup"><span data-stu-id="d76b9-169">**4** Your Resource Group name is going to be **MobileEngagement** unless you created a new one.</span></span> 
     
     ![Mobile Engagement API URI parametreleri][2]

> [!NOTE]
> <br/>
> 
> 1. <span data-ttu-id="d76b9-171">Önceki yönelik API'ler, bu gibi API kök adresi yoksay.</span><span class="sxs-lookup"><span data-stu-id="d76b9-171">Ignore the API Root Address as this was for the previous APIs.</span></span><br/>
> 2. <span data-ttu-id="d76b9-172">Azure Klasik portalı kullanarak uygulama oluşturduysanız, uygulama adı kendisini farklı uygulama kaynağı adı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d76b9-172">If you created the app using Azure Classic portal then you need to use the Application Resource name which is different than the Application name itself.</span></span> <span data-ttu-id="d76b9-173">Azure Portalı'nda uygulama oluşturduysanız, uygulama adı kendisini (Uygulama kaynağı adı ve yeni portalında oluşturulan uygulamalar için uygulama adı arasında hiçbir ayrım yoktur) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d76b9-173">If you created the app in the Azure Portal then you should use the App Name itself (there is no differentiation between Application Resource Name and App Name for apps created in the new portal).</span></span>  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



