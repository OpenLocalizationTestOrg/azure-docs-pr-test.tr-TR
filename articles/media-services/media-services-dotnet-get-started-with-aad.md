---
title: "Azure AD kimlik doğrulama tooaccess .NET ile Azure Media Services API aaaUse | Microsoft Docs"
description: "Bu konu, nasıl toouse Azure Active Directory (Azure AD) kimlik doğrulama tooaccess Azure Media Services gösterir (AMS) API .NET ile."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 2f750e460d9e476ad92e96adeac6500cb692cd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a><span data-ttu-id="3a91f-103">.NET ile Azure AD kimlik doğrulama tooaccess Azure Media Services API kullanın</span><span class="sxs-lookup"><span data-stu-id="3a91f-103">Use Azure AD authentication tooaccess Azure Media Services API with .NET</span></span>

<span data-ttu-id="3a91f-104">4.0.0.4 windowsazure.mediaservices ile başlayarak, Azure Media Services, Azure Active Directory (Azure AD) tabanlı kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="3a91f-104">Starting with windowsazure.mediaservices 4.0.0.4, Azure Media Services supports authentication based on Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="3a91f-105">Bu konu, nasıl gösterir toouse Azure AD kimlik doğrulama tooaccess Microsoft .NET ile Azure Media Services API.</span><span class="sxs-lookup"><span data-stu-id="3a91f-105">This topic shows you how toouse Azure AD  authentication tooaccess Azure Media Services API with Microsoft .NET.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a91f-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3a91f-106">Prerequisites</span></span>

- <span data-ttu-id="3a91f-107">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="3a91f-107">An Azure account.</span></span> <span data-ttu-id="3a91f-108">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3a91f-108">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="3a91f-109">Bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="3a91f-109">A Media Services account.</span></span> <span data-ttu-id="3a91f-110">Daha fazla bilgi için bkz: [hello Azure portal kullanarak bir Azure Media Services hesabı oluşturma](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="3a91f-110">For more information, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="3a91f-111">Merhaba son [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) paket.</span><span class="sxs-lookup"><span data-stu-id="3a91f-111">hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span>
- <span data-ttu-id="3a91f-112">Merhaba konu aşina [AAD kimlik doğrulamasına genel bakış ile Azure Media Services API erişme](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="3a91f-112">Familiarity with hello topic [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="3a91f-113">Azure Media Services ile Azure AD kimlik doğrulaması kullanırken, aşağıdaki iki yöntemden biriyle doğrulayabilir:</span><span class="sxs-lookup"><span data-stu-id="3a91f-113">When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="3a91f-114">**Kullanıcı kimlik doğrulaması** Azure Media Services kaynaklarla hello uygulama toointeract kullanan bir kişinin kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="3a91f-114">**User authentication** authenticates a person who is using hello app toointeract with Azure Media Services resources.</span></span> <span data-ttu-id="3a91f-115">Merhaba etkileşimli uygulaması ilk hello kullanıcıdan kimlik bilgilerini ister.</span><span class="sxs-lookup"><span data-stu-id="3a91f-115">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="3a91f-116">İşlerini kodlama yetkili kullanıcıların toomonitor tarafından kullanılan veya canlı akış Yönetimi konsol uygulaması örneğidir.</span><span class="sxs-lookup"><span data-stu-id="3a91f-116">An example is a management console app that's used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="3a91f-117">**Hizmet asıl kimlik doğrulaması** bir hizmetin kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="3a91f-117">**Service principal authentication** authenticates a service.</span></span> <span data-ttu-id="3a91f-118">Genellikle bu kimlik doğrulama yöntemini kullanan uygulamalar, arka plan programı services, orta katman Hizmetleri veya web uygulamaları, işlev uygulamalarının, logic apps, API veya mikro gibi zamanlanmış işleri çalıştırma uygulamalardır.</span><span class="sxs-lookup"><span data-stu-id="3a91f-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.</span></span>

>[!IMPORTANT]
><span data-ttu-id="3a91f-119">Azure medya hizmeti şu anda Azure erişim denetimi hizmeti kimlik doğrulama modelini destekler.</span><span class="sxs-lookup"><span data-stu-id="3a91f-119">Azure Media Service currently supports an Azure Access Control Service  authentication model.</span></span> <span data-ttu-id="3a91f-120">Ancak, erişim denetimi yetkilendirme 1 Haziran 2018 kullanım toobe geçiyor.</span><span class="sxs-lookup"><span data-stu-id="3a91f-120">However, Access Control authorization is going toobe deprecated on June 1, 2018.</span></span> <span data-ttu-id="3a91f-121">Mümkün olan en kısa sürede tooan Azure Active Directory kimlik doğrulama modeli geçirmek öneririz.</span><span class="sxs-lookup"><span data-stu-id="3a91f-121">We recommend that you migrate tooan Azure Active Directory authentication model as soon as possible.</span></span>

## <a name="get-an-azure-ad-access-token"></a><span data-ttu-id="3a91f-122">Bir Azure AD erişim belirteci alma</span><span class="sxs-lookup"><span data-stu-id="3a91f-122">Get an Azure AD access token</span></span>

<span data-ttu-id="3a91f-123">Azure AD kimlik doğrulaması ile tooconnect toohello Azure Media Services API, hello istemci uygulamanın toorequest bir Azure AD erişim belirteci gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a91f-123">tooconnect toohello Azure Media Services API with Azure AD authentication, hello client app needs toorequest an Azure AD access token.</span></span> <span data-ttu-id="3a91f-124">Merhaba Media Services .NET İstemci SDK, birçok tooacquire bir Azure AD erişim belirteci nasıl Sarmalanan ve sizin için hello Basitleştirilmiş hakkında hello ayrıntılarının kullandığınızda [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) ve [AzureAdTokenCredentials ](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) sınıfları.</span><span class="sxs-lookup"><span data-stu-id="3a91f-124">When you use hello Media Services .NET client SDK, many of hello details about how tooacquire an Azure AD access token are wrapped and simplified for you in hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) and [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes.</span></span> 

<span data-ttu-id="3a91f-125">Örneğin, tooprovide hello Azure AD yetkilisi, Media Services kaynak URI'si ya da yerel gerekmeyen Azure AD uygulama ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="3a91f-125">For example, you don't need tooprovide hello Azure AD authority, Media Services resource URI, or native Azure AD application details.</span></span> <span data-ttu-id="3a91f-126">Bunlar hello Azure AD erişim belirteci sağlayıcısı sınıfı tarafından zaten yapılandırılmış iyi bilinen değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="3a91f-126">These are well-known values that are already configured by hello Azure AD access token provider class.</span></span> 

<span data-ttu-id="3a91f-127">Azure medya hizmeti .NET SDK'sı kullanmıyorsanız hello kullanmanızı öneririz [Azure AD kimlik doğrulama Kitaplığı](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="3a91f-127">If you are not using Azure Media Service .NET SDK, we recommend that you use hello [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="3a91f-128">Azure AD kimlik doğrulama kitaplığı ile toouse gerektiğini hello parametreleri tooget değerlerini görmek [hello Azure portal tooaccess Azure AD kimlik doğrulama ayarlarını kullanmak](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="3a91f-128">tooget values for hello parameters that you need toouse with Azure AD Authentication Library, see [Use hello Azure portal tooaccess Azure AD authentication settings](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="3a91f-129">Merhaba hello varsayılan uygulaması değiştirme hello seçeneğiniz de **AzureAdTokenProvider** kendi uygulaması.</span><span class="sxs-lookup"><span data-stu-id="3a91f-129">You also have hello option of replacing hello default implementation of hello **AzureAdTokenProvider** with your own implementation.</span></span>

## <a name="install-and-configure-azure-media-services-net-sdk"></a><span data-ttu-id="3a91f-130">Yükleme ve Azure Media Services .NET SDK'sını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3a91f-130">Install and configure Azure Media Services .NET SDK</span></span>

>[!NOTE] 
><span data-ttu-id="3a91f-131">Merhaba Media Services .NET SDK'sı ile toouse Azure AD kimlik doğrulaması, gereksinim duyduğunuz toohave hello son [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) paket.</span><span class="sxs-lookup"><span data-stu-id="3a91f-131">toouse Azure AD authentication with hello Media Services .NET SDK, you need toohave hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span> <span data-ttu-id="3a91f-132">Ayrıca, bir başvuru toohello ekleme **Microsoft.IdentityModel.Clients.activedirectory tarafından** derleme.</span><span class="sxs-lookup"><span data-stu-id="3a91f-132">Also, add a reference toohello **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly.</span></span> <span data-ttu-id="3a91f-133">Mevcut bir uygulamayı kullanıyorsanız, hello dahil **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** derleme.</span><span class="sxs-lookup"><span data-stu-id="3a91f-133">If you are using an existing app, include hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span></span> 

1. <span data-ttu-id="3a91f-134">Visual Studio'da yeni bir C# konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3a91f-134">Create a new C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="3a91f-135">Kullanım hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet paketi tooinstall **Azure Media Services .NET SDK'sı**.</span><span class="sxs-lookup"><span data-stu-id="3a91f-135">Use hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet package tooinstall **Azure Media Services .NET SDK**.</span></span> 

    <span data-ttu-id="3a91f-136">NuGet, kullanarak tooadd başvuruları hello aşağıdaki adımları gerçekleştirin: içinde **Çözüm Gezgini**hello proje adına sağ tıklayın ve ardından **Manage NuGet paketleri**.</span><span class="sxs-lookup"><span data-stu-id="3a91f-136">tooadd references by using NuGet, take hello following steps: in **Solution Explorer**, right-click hello project name, and then select **Manage NuGet packages**.</span></span> <span data-ttu-id="3a91f-137">Ardından, arama **windowsazure.mediaservices** seçip **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="3a91f-137">Then, search for **windowsazure.mediaservices** and select **Install**.</span></span>
    
    <span data-ttu-id="3a91f-138">-veya-</span><span class="sxs-lookup"><span data-stu-id="3a91f-138">-or-</span></span>

    <span data-ttu-id="3a91f-139">Çalışma hello komutunda aşağıdaki **Paket Yöneticisi Konsolu** Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3a91f-139">Run hello following command in **Package Manager Console** in Visual Studio.</span></span>

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. <span data-ttu-id="3a91f-140">Ekleme **kullanarak** tooyour kaynak kodu.</span><span class="sxs-lookup"><span data-stu-id="3a91f-140">Add **using** tooyour source code.</span></span>

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a><span data-ttu-id="3a91f-141">Kullanıcı kimlik doğrulamasını kullan</span><span class="sxs-lookup"><span data-stu-id="3a91f-141">Use user authentication</span></span>

<span data-ttu-id="3a91f-142">Merhaba kullanıcı kimlik doğrulaması seçeneği ile tooconnect toohello Azure medya hizmeti API'si, hello istemci uygulamasını kullanarak bir Azure AD belirteci hello şu parametreler toorequest gerekir:</span><span class="sxs-lookup"><span data-stu-id="3a91f-142">tooconnect toohello Azure Media Service API with hello user authentication option, hello client app needs toorequest an Azure AD token by using hello following parameters:</span></span>  

- <span data-ttu-id="3a91f-143">Azure AD Kiracı uç noktası.</span><span class="sxs-lookup"><span data-stu-id="3a91f-143">Azure AD tenant endpoint.</span></span> <span data-ttu-id="3a91f-144">Azure portal hello Hello Kiracı bilgi alınabilir.</span><span class="sxs-lookup"><span data-stu-id="3a91f-144">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="3a91f-145">Merhaba oturum açmış kullanıcı hello sağ üst köşedeki üzerine gelerek.</span><span class="sxs-lookup"><span data-stu-id="3a91f-145">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="3a91f-146">Media Services kaynak URI'si.</span><span class="sxs-lookup"><span data-stu-id="3a91f-146">Media Services resource URI.</span></span>
- <span data-ttu-id="3a91f-147">Media Services (yerel) uygulama istemci kimliği</span><span class="sxs-lookup"><span data-stu-id="3a91f-147">Media Services (native) application client ID.</span></span> 
- <span data-ttu-id="3a91f-148">Media Services (yerel) uygulama yeniden yönlendirme URI'si.</span><span class="sxs-lookup"><span data-stu-id="3a91f-148">Media Services (native) application redirect URI.</span></span> 

<span data-ttu-id="3a91f-149">Bu parametrelerin Hello değerleri bulunabilir **AzureEnvironments.AzureCloudEnvironment**.</span><span class="sxs-lookup"><span data-stu-id="3a91f-149">hello values for these parameters can be found in **AzureEnvironments.AzureCloudEnvironment**.</span></span> <span data-ttu-id="3a91f-150">Merhaba **AzureEnvironments.AzureCloudEnvironment** hello .NET SDK'sı tooget bir yardımcı hello sağ ortam değişkeni ayarlarının ortak bir Azure veri merkezi için sabittir.</span><span class="sxs-lookup"><span data-stu-id="3a91f-150">hello **AzureEnvironments.AzureCloudEnvironment** constant is a helper in hello .NET SDK tooget hello right environment variable settings for a public Azure Data Center.</span></span> 

<span data-ttu-id="3a91f-151">Önceden tanımlanmış ortam ayarları yalnızca hello ortak veri merkezlerinde Media Services erişmek için içerir.</span><span class="sxs-lookup"><span data-stu-id="3a91f-151">It contains pre-defined environment settings for accessing Media Services in hello public data centers only.</span></span> <span data-ttu-id="3a91f-152">Sovereign veya kamu bulut bölgeleri için kullandığınız **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, veya **AzureGermanCloudEnvironment** sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="3a91f-152">For sovereign or government cloud regions, you can use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, or **AzureGermanCloudEnvironment** respectively.</span></span>

<span data-ttu-id="3a91f-153">Aşağıdaki kod örneğine hello bir belirteç oluşturur:</span><span class="sxs-lookup"><span data-stu-id="3a91f-153">hello following code example creates a token:</span></span>
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
<span data-ttu-id="3a91f-154">toostart Media Services karşı programlama, toocreate gereken bir **CloudMediaContext** hello sunucu bağlamı temsil eden örneği.</span><span class="sxs-lookup"><span data-stu-id="3a91f-154">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="3a91f-155">Merhaba **CloudMediaContext** işleri, varlıklar, dosyaları, erişim ilkeleri ve bulucular dahil olmak üzere başvuruları tooimportant koleksiyonları içerir.</span><span class="sxs-lookup"><span data-stu-id="3a91f-155">hello **CloudMediaContext** includes references tooimportant collections including jobs, assets, files, access policies, and locators.</span></span> 

<span data-ttu-id="3a91f-156">Toopass hello etmeniz **kaynak medya REST Hizmetleri için URI** toohello **CloudMediaContext** Oluşturucusu.</span><span class="sxs-lookup"><span data-stu-id="3a91f-156">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="3a91f-157">Medya REST Hizmetleri, oturum açma toohello Azure portal, Azure Media Services hesabınızı seçin tooget hello kaynak URI'si seçin **API erişimini**ve ardından **tooAzure Media Services kullanıcıyla Bağlan kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="3a91f-157">tooget hello resource URI for Media REST Services, sign in toohello Azure portal, select your Azure Media Services account, select **API access**, and then select **Connect tooAzure Media Services with user authentication**.</span></span> 

<span data-ttu-id="3a91f-158">Merhaba aşağıdaki kod örneği oluşturur bir **CloudMediaContext** örneği:</span><span class="sxs-lookup"><span data-stu-id="3a91f-158">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

<span data-ttu-id="3a91f-159">Aşağıdaki örneğine hello nasıl toocreate hello Azure AD belirteci ve hello bağlamını gösterir:</span><span class="sxs-lookup"><span data-stu-id="3a91f-159">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

    namespace AADAuthSample
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Specify your Azure AD tenant domain, for example "microsoft.onmicrosoft.com".
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR AAD TENANT DOMAIN HERE}", AzureEnvironments.AzureCloudEnvironment);
    
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
            }
    
        }
    }

>[!NOTE]
><span data-ttu-id="3a91f-160">Bildiren bir özel durum alırsanız "Merhaba uzak sunucu bir hata döndürdü: (401) yetkisiz" Merhaba bkz [erişim denetimi](media-services-use-aad-auth-to-access-ams-api.md#access-control) erişme Azure Media Services API bölümle Azure AD kimlik doğrulamasına genel bakış.</span><span class="sxs-lookup"><span data-stu-id="3a91f-160">If you get an exception that says "hello remote server returned an error: (401) Unauthorized," see hello [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section of Accessing Azure Media Services API with Azure AD authentication overview.</span></span>

## <a name="use-service-principal-authentication"></a><span data-ttu-id="3a91f-161">Hizmet asıl kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="3a91f-161">Use service principal authentication</span></span>
    
<span data-ttu-id="3a91f-162">Merhaba hizmet asıl seçeneğiyle tooconnect toohello Azure Media Services API, orta katman uygulamanızın (web API ya da web uygulaması) ile şu parametreler hello toorequests bir Azure AD belirteci gerekir:</span><span class="sxs-lookup"><span data-stu-id="3a91f-162">tooconnect toohello Azure Media Services API with hello service principal option, your middle-tier app (web API or web application) needs toorequests an Azure AD token with hello following parameters:</span></span>  

- <span data-ttu-id="3a91f-163">Azure AD Kiracı uç noktası.</span><span class="sxs-lookup"><span data-stu-id="3a91f-163">Azure AD tenant endpoint.</span></span> <span data-ttu-id="3a91f-164">Azure portal hello Hello Kiracı bilgi alınabilir.</span><span class="sxs-lookup"><span data-stu-id="3a91f-164">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="3a91f-165">Merhaba oturum açmış kullanıcı hello sağ üst köşedeki üzerine gelerek.</span><span class="sxs-lookup"><span data-stu-id="3a91f-165">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="3a91f-166">Media Services kaynak URI'si.</span><span class="sxs-lookup"><span data-stu-id="3a91f-166">Media Services resource URI.</span></span>
- <span data-ttu-id="3a91f-167">Azure AD uygulama değerleri: Merhaba **istemci kimliği** ve **gizli**.</span><span class="sxs-lookup"><span data-stu-id="3a91f-167">Azure AD application values: hello **Client ID** and **Client secret**.</span></span>

<span data-ttu-id="3a91f-168">Merhaba hello değerlerini **istemci kimliği** ve **gizli** parametreleri hello Azure portalında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="3a91f-168">hello values for hello **Client ID** and **Client secret** parameters can be found in hello Azure portal.</span></span> <span data-ttu-id="3a91f-169">Daha fazla bilgi için bkz: [hello Azure portalında Azure AD kimlik doğrulaması kullanarak ile çalışmaya başlama](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="3a91f-169">For more information, see [Getting started with Azure AD authentication using hello Azure portal](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="3a91f-170">Merhaba aşağıdaki kod örneğinde bir belirteç hello kullanarak oluşturur **AzureAdTokenCredentials** alan oluşturucu **AzureAdClientSymmetricKey** bir parametre olarak:</span><span class="sxs-lookup"><span data-stu-id="3a91f-170">hello following code example creates a token by using hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientSymmetricKey** as a parameter:</span></span> 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

<span data-ttu-id="3a91f-171">Ayrıca hello belirtebilirsiniz **AzureAdTokenCredentials** alan oluşturucu **AzureAdClientCertificate** bir parametre olarak.</span><span class="sxs-lookup"><span data-stu-id="3a91f-171">You can also specify hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientCertificate** as a parameter.</span></span> 

<span data-ttu-id="3a91f-172">Hakkında yönergeler için toocreate ve Azure AD tarafından kullanılabilmesi için bkz: bir formda bir sertifika yapılandırmak [tooAzure AD sertifikalarla - elle yapılandırma adımları arka plan programı uygulamalarında kimlik doğrulama](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span><span class="sxs-lookup"><span data-stu-id="3a91f-172">For instructions about how toocreate and configure a certificate in a form that can be used by Azure AD, see [Authenticating tooAzure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span></span>

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

<span data-ttu-id="3a91f-173">toostart Media Services karşı programlama, toocreate gereken bir **CloudMediaContext** hello sunucu bağlamı temsil eden örneği.</span><span class="sxs-lookup"><span data-stu-id="3a91f-173">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="3a91f-174">Toopass hello etmeniz **kaynak medya REST Hizmetleri için URI** toohello **CloudMediaContext** Oluşturucusu.</span><span class="sxs-lookup"><span data-stu-id="3a91f-174">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="3a91f-175">Merhaba alabilirsiniz **kaynak medya REST Hizmetleri için URI** hello Azure portalı değerinden.</span><span class="sxs-lookup"><span data-stu-id="3a91f-175">You can get hello **resource URI for Media REST Services** value from hello Azure portal as well.</span></span>

<span data-ttu-id="3a91f-176">Merhaba aşağıdaki kod örneği oluşturur bir **CloudMediaContext** örneği:</span><span class="sxs-lookup"><span data-stu-id="3a91f-176">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
<span data-ttu-id="3a91f-177">Aşağıdaki örneğine hello nasıl toocreate hello Azure AD belirteci ve hello bağlamını gösterir:</span><span class="sxs-lookup"><span data-stu-id="3a91f-177">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

    namespace AADAuthSample
    {
    
        class Program
        {
            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                            new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                            AzureEnvironments.AzureCloudEnvironment);
            
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".      
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
    
                Console.ReadLine();
            }
    
        }
    }

## <a name="next-steps"></a><span data-ttu-id="3a91f-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3a91f-178">Next steps</span></span>

<span data-ttu-id="3a91f-179">Kullanmaya başlama [tooyour hesabı dosyaları karşıya yükleme](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="3a91f-179">Get started with [uploading files tooyour account](media-services-dotnet-upload-files.md).</span></span>
