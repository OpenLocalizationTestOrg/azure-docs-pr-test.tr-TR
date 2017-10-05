---
title: "Azure uygulama hizmetinde API uygulamaları için kullanıcı kimlik doğrulaması | Microsoft Docs"
description: "Azure App Service'deki bir API uygulaması yalnızca kimliği doğrulanmış kullanıcılar için erişime izin vererek korumayı öğrenin."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 3896760d-46ff-4b67-b98a-edd233f24758
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: a5b713f3a60b3886d813438496d704f464d914e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a><span data-ttu-id="564bf-103">Azure uygulama hizmetinde API uygulamaları için kullanıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="564bf-103">User authentication for API Apps in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="564bf-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="564bf-104">Overview</span></span>
<span data-ttu-id="564bf-105">Bu makalede, böylece yalnızca kimliği doğrulanan kullanıcılar bunu bir Azure API uygulaması korunacak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="564bf-105">This article shows how to protect an Azure API app so that only authenticated users can call it.</span></span> <span data-ttu-id="564bf-106">Makalede, okuduğunuz varsayılır [Azure App Service kimlik doğrulamasına genel bakış](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="564bf-106">The article assumes that you have read the [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span>

<span data-ttu-id="564bf-107">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="564bf-107">You'll learn:</span></span>

* <span data-ttu-id="564bf-108">Azure Active Directory (Azure AD) ilişkin ayrıntılı bir kimlik doğrulama sağlayıcısı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="564bf-108">How to configure an authentication provider, with details for Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="564bf-109">Korumalı bir API uygulaması kullanmalarını nasıl [Active Directory Authentication Library (ADAL) JavaScript için](https://github.com/AzureAD/azure-activedirectory-library-for-js).</span><span class="sxs-lookup"><span data-stu-id="564bf-109">How to consume a protected API app by using the [Active Directory Authentication Library (ADAL) for JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js).</span></span>

<span data-ttu-id="564bf-110">Makale iki bölüm içerir:</span><span class="sxs-lookup"><span data-stu-id="564bf-110">The article contains two sections:</span></span>

* <span data-ttu-id="564bf-111">[Azure App Service'te kullanıcı kimlik doğrulamasını yapılandırmak nasıl](#authconfig) bölüm App Service tarafından desteklenen tüm çerçeveler için eşit oranda geçerlidir ve genel bir API uygulaması için kullanıcı kimlik doğrulamasını yapılandırmak nasıl açıklar .NET, Node.js ve Java dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="564bf-111">The [How to configure user authentication in Azure App Service](#authconfig) section explains in general how to configure user authentication for any API app and applies equally to all frameworks supported by App Service, including .NET, Node.js, and Java.</span></span>
* <span data-ttu-id="564bf-112">İle başlayarak [.NET API Apps öğreticileri etmeden](#tutorialstart) bölümünde, makale size yol gösterir, böylece kullanıcı kimlik doğrulaması için Azure Active Directory kullanan örnek bir uygulama .NET arka ucu ve bir AngularJS ön uç ile yapılandırma yoluyla.</span><span class="sxs-lookup"><span data-stu-id="564bf-112">Starting with the [Continuing the .NET API Apps tutorials](#tutorialstart) section, the article guides you through configuring a sample application with a .NET back end and an AngularJS front end so that it uses Azure Active Directory for user authentication.</span></span> 

## <span data-ttu-id="564bf-113"><a id="authconfig"></a>Azure App Service'te kullanıcı kimlik doğrulaması yapılandırma</span><span class="sxs-lookup"><span data-stu-id="564bf-113"><a id="authconfig"></a> How to configure user authentication in Azure App Service</span></span>
<span data-ttu-id="564bf-114">Bu bölümde, tüm API uygulamaları için geçerli olan genel yönergeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="564bf-114">This section provides general instructions that apply to any API app.</span></span> <span data-ttu-id="564bf-115">Adımları belirli yapmak listesi .NET örnek uygulaması, Git [.NET kullanmaya Başlarken öğreticilerine devam etme](#tutorialstart).</span><span class="sxs-lookup"><span data-stu-id="564bf-115">For steps specific to the To Do List .NET sample application, go to [Continuing the .NET getting-started tutorials](#tutorialstart).</span></span>

1. <span data-ttu-id="564bf-116">İçinde [Azure portal](https://portal.azure.com/), gitmek **ayarları** korumak, bulmak istediğiniz API uygulaması dikey **özellikleri** bölümünde ve ardından **kimlik doğrulama / yetkilendirme**.</span><span class="sxs-lookup"><span data-stu-id="564bf-116">In the [Azure portal](https://portal.azure.com/), navigate to the **Settings** blade of the API app that you want to protect, find the **Features** section, and then click **Authentication/ Authorization**.</span></span>
   
    ![Azure portal kimlik doğrulama/yetkilendirme](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. <span data-ttu-id="564bf-118">İçinde **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="564bf-118">In the **Authentication / Authorization** blade, click **On**.</span></span>
3. <span data-ttu-id="564bf-119">Seçeneklerden birini seçin **isteğin kimliği doğrulanmamış olduğunda gerçekleştirilecek eylem** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="564bf-119">Select one of the options from the **Action to take when request is not authenticated** drop-down list.</span></span>
   
   * <span data-ttu-id="564bf-120">API uygulamanız ulaşmak için yalnızca kimliği doğrulanmış çağrıları istiyorsanız, aşağıdakilerden birini tercih **ile oturum...**  seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="564bf-120">If you want only authenticated calls to reach your API app, choose one of the **Log in with ...** options.</span></span> <span data-ttu-id="564bf-121">Bu seçenek, API uygulaması içinde çalışan herhangi bir kod yazmak zorunda kalmadan korumanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="564bf-121">This option enables you to protect the API app without writing any code that runs in it.</span></span>
   * <span data-ttu-id="564bf-122">API uygulamanız ulaşmak için tüm çağrıları istiyorsanız, tercih **isteğine izin ver (hiçbir işlem)**.</span><span class="sxs-lookup"><span data-stu-id="564bf-122">If you want all calls to reach your API app, choose **Allow request (no action)**.</span></span> <span data-ttu-id="564bf-123">Kimlik doğrulama sağlayıcıları seçimine kimliği doğrulanmamış arayanlara yönlendirmek için bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="564bf-123">You can use this option to direct unauthenticated callers to a choice of authentication providers.</span></span> <span data-ttu-id="564bf-124">Bu seçenek ile yetkilendirme işlemek için kod yazmak zorunda.</span><span class="sxs-lookup"><span data-stu-id="564bf-124">With this option you have to write code to handle authorization.</span></span>
     
     <span data-ttu-id="564bf-125">Daha fazla bilgi için bkz. [Azure App Service’de API Apps için kimlik doğrulama ve yetkilendirme](app-service-api-authentication.md#multiple-protection-options).</span><span class="sxs-lookup"><span data-stu-id="564bf-125">For more information, see [Authentication and authorization for API Apps in Azure App Service](app-service-api-authentication.md#multiple-protection-options).</span></span>
4. <span data-ttu-id="564bf-126">Bir veya daha fazlasını seçin **kimlik doğrulama sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="564bf-126">Select one or more of the **Authentication Providers**.</span></span>
   
    <span data-ttu-id="564bf-127">Görüntüyü Azure AD tarafından doğrulanmasını tüm arayanlar gerektiren seçimler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="564bf-127">The image shows    choices that require all callers to be authenticated by Azure AD.</span></span>
   
    ![Azure portal kimlik doğrulama/yetkilendirme dikey penceresi](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    <span data-ttu-id="564bf-129">Bir kimlik doğrulama sağlayıcısı seçtiğinizde, portal bu sağlayıcı için bir yapılandırma dikey penceresinde görüntüler.</span><span class="sxs-lookup"><span data-stu-id="564bf-129">When you choose an authentication provider, the portal displays a configuration blade for that provider.</span></span> 
   
    <span data-ttu-id="564bf-130">Kimlik doğrulama sağlayıcısı yapılandırma dikey yapılandırmaya yönelik adım ayrıntılı yönergeler için bkz: [uygulama hizmeti uygulamanızı Azure Active Directory oturum açma kullanacak şekilde yapılandırmak nasıl](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="564bf-130">For detailed instructions that explain how to configure the authentication provider configuration blades, see [How to configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span> <span data-ttu-id="564bf-131">(Azure AD hakkındaki bir makalede bağlantıyı gider, ancak makale için diğer kimlik doğrulama sağlayıcıları makalelerine bağlantı sekme içerir.)</span><span class="sxs-lookup"><span data-stu-id="564bf-131">(The link goes to an article about Azure AD, but the article itself contains tabs that link to articles for the other authentication providers.)</span></span>
5. <span data-ttu-id="564bf-132">Kimlik doğrulama sağlayıcısı yapılandırma dikey bittiğinde, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="564bf-132">When you're done with the authentication provider configuration blade, click **OK**.</span></span>
6. <span data-ttu-id="564bf-133">İçinde **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="564bf-133">In the **Authentication / Authorization** blade, click **Save**.</span></span>

<span data-ttu-id="564bf-134">Bu yapıldığında, App Service API uygulaması düşmeden önce tüm API çağrıları kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="564bf-134">When this is done, App Service authenticates all API calls before they reach the API app.</span></span> <span data-ttu-id="564bf-135">Kimlik doğrulama hizmetleri aynı .NET, Node.js ve Java dahil olmak üzere uygulama hizmetini destekleyen tüm diller için çalışır.</span><span class="sxs-lookup"><span data-stu-id="564bf-135">The authentication services work the same for all languages that App service supports, including .NET, Node.js, and Java.</span></span> 

<span data-ttu-id="564bf-136">Arayan kimliği doğrulanmış API çağrıları yapma HTTP isteklerini yetkilendirme üst bilgisi kimlik doğrulama sağlayıcısının OAuth 2.0 taşıyıcı belirteci içerir.</span><span class="sxs-lookup"><span data-stu-id="564bf-136">To make authenticated API calls, the caller includes the authentication provider's OAuth 2.0 bearer token in the Authorization header of HTTP requests.</span></span> <span data-ttu-id="564bf-137">Belirteç kimlik doğrulama sağlayıcısının SDK kullanılarak edinilebilir.</span><span class="sxs-lookup"><span data-stu-id="564bf-137">The token can be acquired by using the authentication provider's SDK.</span></span>

## <span data-ttu-id="564bf-138"><a id="tutorialstart"></a>.NET API uygulamaları öğreticilerine devam etme</span><span class="sxs-lookup"><span data-stu-id="564bf-138"><a id="tutorialstart"></a> Continuing the .NET API Apps tutorials</span></span>
<span data-ttu-id="564bf-139">API uygulamaları için Node.js ve Java öğreticileri izliyorsanız, sonraki makaleyi atla [API uygulamaları için hizmet asıl kimlik doğrulaması](app-service-api-dotnet-service-principal-auth.md).</span><span class="sxs-lookup"><span data-stu-id="564bf-139">If you are following the Node.js or Java tutorials for API apps, skip to the next article, [service principal authentication for API apps](app-service-api-dotnet-service-principal-auth.md).</span></span> 

<span data-ttu-id="564bf-140">API uygulamaları için .NET Öğreticisi serisi izlediğinden ve örnek uygulama konusunda belirtildiği şekilde zaten dağıttıysanız [ilk](app-service-api-dotnet-get-started.md) ve [ikinci](app-service-api-cors-consume-javascript.md) öğreticileri, atlamak için [uygulama hizmeti ve Azure AD kimlik doğrulaması ayarlama](#azureauth) bölümü.</span><span class="sxs-lookup"><span data-stu-id="564bf-140">If you are following the .NET tutorial series for API apps and have already deployed the sample application as directed in the [first](app-service-api-dotnet-get-started.md) and [second](app-service-api-cors-consume-javascript.md) tutorials, skip to the [Set up authentication in App Service and Azure AD](#azureauth) section.</span></span>

<span data-ttu-id="564bf-141">Birinci ve ikinci öğreticileri olmadan bu öğreticiyi izleyin istiyorsanız, örnek uygulamayı dağıtmak için otomatik bir işlem kullanarak başlayacağınızı açıklayan aşağıdaki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="564bf-141">If you want to follow this tutorial without going through the first and second tutorials, do the following steps which explain how to get started by using an automated process to deploy the sample application.</span></span>

> [!NOTE]
> <span data-ttu-id="564bf-142">Aşağıdaki adımları ilk iki öğreticiler, tek bir istisna olarak kaldırdıysanız aynı başlangıç noktasına alın: Visual Studio olmaz zaten biliyor hangi web uygulaması veya her proje dağıtılan API uygulaması.</span><span class="sxs-lookup"><span data-stu-id="564bf-142">The following steps get you to the same starting point as if you did the first two tutorials, with one exception: Visual Studio won't already know which web app or API app that each project gets deployed to.</span></span> <span data-ttu-id="564bf-143">Bu öğreticideki doğru hedeflere dağıtmak açıklanmaktadır tam yönergeler olmayacaktır anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="564bf-143">That means you won't have exact instructions in this tutorial that explain how to deploy to the right targets.</span></span> <span data-ttu-id="564bf-144">Dağıtım adımları kendi yapmak nasıl getirme ile memnun değilseniz, öğretici serisinde izlemek daha iyi [ilk öğreticide](app-service-api-dotnet-get-started.md) ile başlamak daha bu dağıtım işlemi otomatik.</span><span class="sxs-lookup"><span data-stu-id="564bf-144">If you're not comfortable with figuring out how to do the deployment steps on your own, it's better to follow the tutorial series from the [first tutorial](app-service-api-dotnet-get-started.md) than to start with this automated deployment process.</span></span>
> 
> 

1. <span data-ttu-id="564bf-145">Tüm listelenen önkoşulları sahip olduğunuzdan emin olun [ilk öğreticide](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="564bf-145">Make sure that you have all of the prerequisites listed in the [first tutorial](app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="564bf-146">Listelenen önkoşullara ek olarak, bu kimlik doğrulama öğreticiler App Service web apps ve API apps Visual Studio ve Azure portal ile çalıştıktan varsayalım.</span><span class="sxs-lookup"><span data-stu-id="564bf-146">In addition to the prerequisites listed, these authentication tutorials assume that you have worked with App Service web apps and API apps in Visual Studio and the Azure portal.</span></span>
2. <span data-ttu-id="564bf-147">Tıklatın **Azure'a Dağıt** düğmesini [Yapılacaklar listesi örnek depo Benioku dosyası](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) API uygulamaları ve web uygulamasını dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="564bf-147">Click the **Deploy to Azure** button in the [To Do List sample repository readme file](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) to deploy the API apps and the web app.</span></span> <span data-ttu-id="564bf-148">Bu kullanabileceğiniz gibi web uygulaması ve API uygulama adlarının aramak için sonraki oluşturduğu Azure kaynak grubu not edin.</span><span class="sxs-lookup"><span data-stu-id="564bf-148">Make a note of the Azure resource group that gets created, as you can use this later to look up web app and API app names.</span></span>
3. <span data-ttu-id="564bf-149">İndirme veya kopyalama [Yapılacaklar listesi örnek depo](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) , ile yerel olarak Visual Studio'da karşılaşmayacağınızı kodu alın.</span><span class="sxs-lookup"><span data-stu-id="564bf-149">Download or clone the [To Do List sample repository](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) to get the code that you'll work with locally in Visual Studio.</span></span>

## <span data-ttu-id="564bf-150"><a id="azureauth"></a>Uygulama hizmeti ve Azure AD kimlik doğrulaması ayarlama</span><span class="sxs-lookup"><span data-stu-id="564bf-150"><a id="azureauth"></a> Set up authentication in App Service and Azure AD</span></span>
<span data-ttu-id="564bf-151">Artık kullanıcıların kimliğinin doğrulanmasını gerek kalmadan Azure App Service içinde çalışan uygulama vardır.</span><span class="sxs-lookup"><span data-stu-id="564bf-151">You now have the application running in Azure App Service without requiring that users be authenticated.</span></span> <span data-ttu-id="564bf-152">Bu bölümde aşağıdaki görevleri yaparak kimlik doğrulaması ekleyin:</span><span class="sxs-lookup"><span data-stu-id="564bf-152">In this section you add authentication by doing the following tasks:</span></span>

* <span data-ttu-id="564bf-153">Uygulama hizmeti orta katman API uygulamasını çağırmak için Azure Active Directory (Azure AD) kimlik doğrulama gerektirecek şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="564bf-153">Configure App Service to require Azure Active Directory (Azure AD) authentication for calling the middle tier API app.</span></span>
* <span data-ttu-id="564bf-154">Azure AD uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="564bf-154">Create an Azure AD application.</span></span>
* <span data-ttu-id="564bf-155">Taşıyıcı belirteci oturum açma işleminden sonra AngularJS ön ucu göndermek için Azure AD uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="564bf-155">Configure the Azure AD application to send the bearer token after logon to the AngularJS front end.</span></span> 

<span data-ttu-id="564bf-156">Öğretici yönergeleri izleyerek çalışırken sorunlarla karşılaşırsanız, bkz: [sorun giderme](#troubleshooting) öğreticinin sonunda bölüm.</span><span class="sxs-lookup"><span data-stu-id="564bf-156">If you run into problems while following the tutorial directions, see the [Troubleshooting](#troubleshooting) section at the end of the tutorial.</span></span> 

### <a name="configure-authentication-for-the-middle-tier-api-app"></a><span data-ttu-id="564bf-157">Orta katman API uygulaması için kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="564bf-157">Configure authentication for the middle tier API app</span></span>
1. <span data-ttu-id="564bf-158">İçinde [Azure portal](https://portal.azure.com/), gitmek **ayarları** Todolistapı projesi için oluşturduğunuz API uygulaması dikey bulmak **özellikleri** bölümünde ve ardından **kimlik doğrulama / yetkilendirme**.</span><span class="sxs-lookup"><span data-stu-id="564bf-158">In the [Azure portal](https://portal.azure.com/), navigate to the **Settings** blade of the API app that you created for the ToDoListAPI project, find the **Features** section, and then click **Authentication / Authorization**.</span></span>
   
    ![Azure portal kimlik doğrulama/yetkilendirme](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. <span data-ttu-id="564bf-160">İçinde **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="564bf-160">In the **Authentication / Authorization** blade, click **On**.</span></span>
3. <span data-ttu-id="564bf-161">İçinde **isteğin kimliği doğrulanmamış olduğunda gerçekleştirilecek eylem** aşağı açılan listesinden, **Azure Active Directory ile oturum aç**.</span><span class="sxs-lookup"><span data-stu-id="564bf-161">In the **Action to take when request is not authenticated** drop-down list, select **Log in with Azure Active Directory**.</span></span>
   
    <span data-ttu-id="564bf-162">Bu seçenek, hiçbir unauathenticated istek API uygulaması ulaşabileceği sağlar.</span><span class="sxs-lookup"><span data-stu-id="564bf-162">This option ensures that no unauathenticated requests will reach the API app.</span></span> 
4. <span data-ttu-id="564bf-163">Altında **kimlik doğrulama sağlayıcıları**, tıklatın **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="564bf-163">Under **Authentication Providers**, click **Azure Active Directory**.</span></span>
   
    ![Azure portal kimlik doğrulama/yetkilendirme dikey penceresi](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. <span data-ttu-id="564bf-165">İçinde **Azure Active Directory ayarları** dikey penceresinde tıklatın **Express**</span><span class="sxs-lookup"><span data-stu-id="564bf-165">In the **Azure Active Directory Settings** blade, click **Express**</span></span>
   
    ![Azure portal kimlik doğrulama/yetkilendirme Express seçeneği](./media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    <span data-ttu-id="564bf-167">İle **Express** seçeneği, uygulama hizmeti otomatik olarak oluşturabilir Azure AD uygulaması, Azure AD'de [Kiracı](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant).</span><span class="sxs-lookup"><span data-stu-id="564bf-167">With the **Express** option, App Service can automatically create an Azure AD application in your Azure AD [tenant](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant).</span></span> 
   
    <span data-ttu-id="564bf-168">Her Azure hesabı otomatik olarak bir tane var olduğundan, Kiracı oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="564bf-168">You don't have to create a tenant, because every Azure account automatically has one.</span></span>
6. <span data-ttu-id="564bf-169">Altında **yönetim modu**, tıklatın **yeni AD uygulaması oluştur** seçili değilse ve içinde değeri dikkat edin **oluşturma uygulama** metin kutusu; bu AAD uygulamasını Klasik Azure portalındaki daha sonra göreceğiz.</span><span class="sxs-lookup"><span data-stu-id="564bf-169">Under **Management mode**, click **Create New AD App** if it isn't already selected, and notice the value that is in the **Create App** text box; you'll look up this AAD application in the Azure classic portal later.</span></span>
   
    ![Azure portalında Azure AD ayarları](./media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    <span data-ttu-id="564bf-171">Azure, Azure AD kiracınıza belirtilen ada sahip bir Azure AD uygulaması otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="564bf-171">Azure will automatically create an Azure AD application with the indicated name in your Azure AD tenant.</span></span> <span data-ttu-id="564bf-172">Varsayılan olarak, Azure AD uygulaması aynı API uygulaması olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="564bf-172">By default, the Azure AD application is named the same as the API app.</span></span> <span data-ttu-id="564bf-173">İsterseniz, farklı bir ad girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="564bf-173">If you prefer, you can enter a different name.</span></span>
7. <span data-ttu-id="564bf-174">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="564bf-174">Click **OK**.</span></span>
8. <span data-ttu-id="564bf-175">İçinde **kimlik doğrulama / yetkilendirme** dikey penceresinde tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="564bf-175">In the **Authentication / Authorization** blade, click **Save**.</span></span>
   
    ![Kaydet’e tıklayın.](./media/app-service-api-dotnet-user-principal-auth/authsave.png)

<span data-ttu-id="564bf-177">Artık yalnızca Azure AD kiracınızdaki kullanıcıların API uygulaması çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="564bf-177">Now only users in your Azure AD tenant can call the API app.</span></span>

### <a name="optional-test-the-api-app"></a><span data-ttu-id="564bf-178">İsteğe bağlı: Test API uygulaması</span><span class="sxs-lookup"><span data-stu-id="564bf-178">Optional: Test the API app</span></span>
1. <span data-ttu-id="564bf-179">Bir tarayıcıda API uygulamasının URL'sine gidin: içinde **API uygulaması** dikey Azure portalında tıklayın altındaki bağlantı **URL**.</span><span class="sxs-lookup"><span data-stu-id="564bf-179">In a browser go to the URL of the API app: in the **API app** blade in the Azure portal, click the link under **URL**.</span></span>  
   
    <span data-ttu-id="564bf-180">Kimliği doğrulanmamış istekler API uygulamasına erişmesine izin verilmediği için oturum açma ekranına yeniden yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="564bf-180">You are redirected to a login screen because unauthenticated requests are not allowed to reach the API app.</span></span>
   
    <span data-ttu-id="564bf-181">Tarayıcınız "başarıyla oluşturuldu" sayfası kalırsa, tarayıcı zaten oturum açmış olabilirsiniz--bu durumda, bir InPrivate veya Incognito penceresi açın ve API uygulamasının URL'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="564bf-181">If your browser goes to the "successfully created" page, the browser might already be logged on -- in that case, open an InPrivate or Incognito window and go to the API app's URL.</span></span>
2. <span data-ttu-id="564bf-182">Azure AD kiracınızda bir kullanıcı için kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="564bf-182">Log on using credentials for a user in your Azure AD tenant.</span></span>
   
    <span data-ttu-id="564bf-183">Oturum açtınız, tarayıcıda "başarıyla oluşturuldu" sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="564bf-183">When you're logged on, the "successfully created" page appears in the browser.</span></span>
3. <span data-ttu-id="564bf-184">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="564bf-184">Close the browser.</span></span>

### <a name="configure-the-azure-ad-application"></a><span data-ttu-id="564bf-185">Azure AD uygulaması yapılandırma</span><span class="sxs-lookup"><span data-stu-id="564bf-185">Configure the Azure AD application</span></span>
<span data-ttu-id="564bf-186">Azure AD kimlik doğrulaması için yapılandırıldığında, uygulama hizmeti bir Azure AD uygulaması oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="564bf-186">When you configured Azure AD authentication, App Service created an Azure AD application for you.</span></span> <span data-ttu-id="564bf-187">Varsayılan olarak yeni Azure AD uygulama, taşıyıcı belirteci API uygulamasının URL'sine sağlamak üzere yapılandırıldı.</span><span class="sxs-lookup"><span data-stu-id="564bf-187">By default the new Azure AD application was configured to provide the bearer token to the API app's URL.</span></span> <span data-ttu-id="564bf-188">Bu bölümde taşıyıcı belirtecine AngularJS ön ucu yerine doğrudan orta katman API uygulamasını sağlamak için Azure AD uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="564bf-188">In this section you configure the Azure AD application to provide the bearer token to the AngularJS front end instead of directly to the middle tier API app.</span></span> <span data-ttu-id="564bf-189">API uygulaması çağırdığında AngularJS ön uç belirteci API uygulamasına gönderir.</span><span class="sxs-lookup"><span data-stu-id="564bf-189">The AngularJS front end will send the token to the API app when it calls the API app.</span></span>

> [!NOTE]
> <span data-ttu-id="564bf-190">Ön uç ve orta için uygulama işlem tutmak için olabildiğince basit, Bu öğretici kullanır tek Azure AD bir API uygulaması katmanı.</span><span class="sxs-lookup"><span data-stu-id="564bf-190">To keep the process as simple as possible, this tutorial uses a single Azure AD application for both the front end and the middle tier API app.</span></span> <span data-ttu-id="564bf-191">İki Azure AD uygulamaları başka bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="564bf-191">Another option is to use two Azure AD applications.</span></span> <span data-ttu-id="564bf-192">Bu durumda orta katman Azure AD uygulaması çağırmak için ön uç ait Azure AD uygulama izin vermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="564bf-192">In that case you would have to give the front end's Azure AD application permission to call the middle tier's Azure AD application.</span></span> <span data-ttu-id="564bf-193">Bu çok sayıda uygulama yaklaşımı her katman için izinleri üzerinde daha ayrıntılı denetim verirsiniz.</span><span class="sxs-lookup"><span data-stu-id="564bf-193">This multi-application approach would give you more granular control over permissions to each tier.</span></span>
> 
> 

1. <span data-ttu-id="564bf-194">İçinde [Klasik Azure portalı](https://manage.windowsazure.com/)gidin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="564bf-194">In the [Azure classic portal](https://manage.windowsazure.com/), go to **Azure Active Directory**.</span></span>
   
   <span data-ttu-id="564bf-195">Erişmesi gereken belirli Azure Active Directory ayarları henüz mevcut Azure portalından kullanılabilir olmadığından Klasik portal kullanmak zorunda.</span><span class="sxs-lookup"><span data-stu-id="564bf-195">You have to use the classic portal because certain Azure Active Directory settings that you need access to are not yet available in the current Azure portal.</span></span>
2. <span data-ttu-id="564bf-196">Üzerinde **Directory** sekmesinde, AAD kiracınızın tıklayın.</span><span class="sxs-lookup"><span data-stu-id="564bf-196">On the **Directory** tab, click your AAD tenant.</span></span>
   
   ![Azure AD Klasik portalında](./media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. <span data-ttu-id="564bf-198">Tıklatın **uygulamaları > Şirketimin sahip olduğu uygulamalar**ve ardından onay işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="564bf-198">Click **Applications > Applications my company owns**, and then click the check mark.</span></span>
   
   <span data-ttu-id="564bf-199">Yeni uygulama görmek için sayfayı yenilemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="564bf-199">You might also have to refresh the page to see the new application.</span></span>
4. <span data-ttu-id="564bf-200">Uygulamalar listesinde API uygulamanız için kimlik doğrulaması etkinleştirildiğinde, Azure oluşturduğunuz birinin adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="564bf-200">In the list of applications, click the name of the one that Azure created for you when you enabled authentication for your API app.</span></span>
   
   ![Azure AD uygulamalar sekmesi](./media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. <span data-ttu-id="564bf-202">**Yapılandır**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="564bf-202">Click **Configure**.</span></span>
   
   ![Azure AD Yapılandır sekmesi](./media/app-service-api-dotnet-user-principal-auth/configure.png)
6. <span data-ttu-id="564bf-204">Ayarlama **oturum açma URL'si** AngularJS web uygulamanızı, hiçbir eğik URL'si.</span><span class="sxs-lookup"><span data-stu-id="564bf-204">Set **Sign-on URL** to the URL for your AngularJS web app, no trailing slash.</span></span>
   
   <span data-ttu-id="564bf-205">Örneğin: https://todolistangular.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="564bf-205">For example: https://todolistangular.azurewebsites.net</span></span>
   
   ![Oturum açma URL'si](./media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. <span data-ttu-id="564bf-207">Ayarlama **yanıt URL'si** web uygulamanıza hiçbir eğik URL'si.</span><span class="sxs-lookup"><span data-stu-id="564bf-207">Set **Reply URL** to the URL for your web app, no trailing slash.</span></span>
   
   <span data-ttu-id="564bf-208">Örneğin: https://todolistsangular.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="564bf-208">For example: https://todolistsangular.azurewebsites.net</span></span>
8. <span data-ttu-id="564bf-209">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="564bf-209">Click **Save**.</span></span>
   
   ![Yanıt URL'si](./media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. <span data-ttu-id="564bf-211">Sayfanın alt kısmındaki tıklatın **Yönet bildirimi > indirme bildirimi**.</span><span class="sxs-lookup"><span data-stu-id="564bf-211">At the bottom of the page, click **Manage manifest > Download manifest**.</span></span>
   
   ![Bildirim indirin](./media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. <span data-ttu-id="564bf-213">Dosya, düzenleyebileceğiniz bir konuma indirin.</span><span class="sxs-lookup"><span data-stu-id="564bf-213">Download the file to a location where you can edit it.</span></span>
11. <span data-ttu-id="564bf-214">İndirilen bildirim dosyasında arama `oauth2AllowImplicitFlow` özelliği.</span><span class="sxs-lookup"><span data-stu-id="564bf-214">In the downloaded manifest file, search for the  `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="564bf-215">Bu özelliği değerini değiştirme `false` için `true`ve ardından dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="564bf-215">Change the value of this property from `false` to `true`, and then save the file.</span></span>
    
    <span data-ttu-id="564bf-216">Bu ayar, bir JavaScript tek sayfalı uygulama erişimi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="564bf-216">This setting is required for access from a JavaScript single-page application.</span></span> <span data-ttu-id="564bf-217">URL parçadaki döndürülecek Oauth 2.0 taşıyıcı belirteci sağlar.</span><span class="sxs-lookup"><span data-stu-id="564bf-217">It enables the Oauth 2.0 bearer token to be returned in the URL fragment.</span></span>
12. <span data-ttu-id="564bf-218">Tıklatın **Yönet bildirimi > karşıya yükleme bildirimi**ve önceki adımda güncelleştirilmiş dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="564bf-218">Click **Manage manifest > Upload manifest**, and upload the file that you updated in the preceding step.</span></span>
    
    ![Bildirim karşıya yükle](./media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. <span data-ttu-id="564bf-220">Kopya **istemci kimliği** değer ve bir yere alabilirsiniz ondan daha sonra kaydedin.</span><span class="sxs-lookup"><span data-stu-id="564bf-220">Copy the **Client ID** value and save it somewhere you can get it from later.</span></span>

## <a name="configure-the-todolistangular-project-to-use-authentication"></a><span data-ttu-id="564bf-221">ToDoListAngular projesi kimlik doğrulaması kullanacak şekilde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="564bf-221">Configure the ToDoListAngular project to use authentication</span></span>
<span data-ttu-id="564bf-222">Bu bölümde oturum açmış kullanıcının Azure AD'den bir taşıyıcı belirtecini almak üzere Active Directory Authentication Library (ADAL) JS için kullandığı şekilde AngularJS ön uç değiştirin.</span><span class="sxs-lookup"><span data-stu-id="564bf-222">In this section you change the AngularJS front end so that it uses Active Directory Authentication Library (ADAL) for JS to acquire a bearer token for the logged-on user from Azure AD.</span></span> <span data-ttu-id="564bf-223">Kod belirteç orta bağlayıcıya gönderilen HTTP isteklerinde aşağıdaki çizimde gösterildiği gibi içerir.</span><span class="sxs-lookup"><span data-stu-id="564bf-223">The code will include the token in HTTP requests sent to the middle tier, as shown in the following diagram.</span></span> 

![Kullanıcı kimlik doğrulama diyagramı](./media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

<span data-ttu-id="564bf-225">ToDoListAngular projesini dosyalarında aşağıdaki değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="564bf-225">Make the following changes to files in the ToDoListAngular project.</span></span>

1. <span data-ttu-id="564bf-226">Açık *Index.cshtml* dosya.</span><span class="sxs-lookup"><span data-stu-id="564bf-226">Open the *index.cshtml* file.</span></span>
2. <span data-ttu-id="564bf-227">Active Directory Authentication Library (ADAL) JS betikler için başvuru satırlardaki yorumları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="564bf-227">Uncomment the lines that reference the Active Directory Authentication Library (ADAL) for JS scripts.</span></span>
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. <span data-ttu-id="564bf-228">Açık *app/scripts/app.js* dosya.</span><span class="sxs-lookup"><span data-stu-id="564bf-228">Open the *app/scripts/app.js* file.</span></span>
4. <span data-ttu-id="564bf-229">"Kimlik doğrulaması" için işaretlenmiş kod bloğunu çıkışı açıklama ve "ile kimlik doğrulaması" için işaretlenmiş kod bloğunu açıklamadan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="564bf-229">Comment out the block of code marked for "without authentication" and uncomment the block of code marked for "with authentication".</span></span>
   
    <span data-ttu-id="564bf-230">Bu değişiklik ADAL JS kimlik doğrulama sağlayıcısı başvuruyor ve onu yapılandırma değerlerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="564bf-230">This change references the ADAL JS authentication provider and provides configuration values to it.</span></span> <span data-ttu-id="564bf-231">Aşağıdaki adımlarda Azure AD uygulaması ve API uygulaması için yapılandırma değerlerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="564bf-231">In the following steps you set the configuration values for your API app and Azure AD application.</span></span>
5. <span data-ttu-id="564bf-232">Ayarlar kodda `endpoints` değişkeni, Todolistapı projesi için oluşturduğunuz ve Azure Klasik portalından kopyalandığından istemci kimliği kümesi Azure AD uygulama kimliği bu API URL API uygulamasının URL'sine ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="564bf-232">In the code that sets the `endpoints` variable, set the API URL to the URL of the API app that you created for the ToDoListAPI project, and set the Azure AD application ID to the client ID that you copied from the Azure classic portal.</span></span>
   
    <span data-ttu-id="564bf-233">Kod artık aşağıdaki örneğe benzer.</span><span class="sxs-lookup"><span data-stu-id="564bf-233">The code is now similar to the following example.</span></span>
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. <span data-ttu-id="564bf-234">Çağrısında `adalProvider.init`ayarlayın `tenant` için Kiracı adınızı ve `clientId` önceki adımda kullanılan aynı değeri.</span><span class="sxs-lookup"><span data-stu-id="564bf-234">In the call to `adalProvider.init`, set `tenant` to your tenant name and `clientId` to same value you used in the previous step.</span></span>
   
    <span data-ttu-id="564bf-235">Kod artık aşağıdaki örneğe benzer.</span><span class="sxs-lookup"><span data-stu-id="564bf-235">The code is now similar to the following example.</span></span>
   
        adalProvider.init(
            {
                instance: 'https://login.microsoftonline.com/', 
                tenant: 'contoso.onmicrosoft.com',
                clientId: '1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3',
                extraQueryParameter: 'nux=1',
                endpoints: endpoints
            },
            $httpProvider
            );
   
    <span data-ttu-id="564bf-236">Bu değişiklikler `app.js` çağıran kodu ve çağrılan API aynı Azure AD uygulama içinde olduğunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="564bf-236">These changes to `app.js` specify that the calling code and the called API are in the same Azure AD application.</span></span>
7. <span data-ttu-id="564bf-237">Açık *app/scripts/homeCtrl.js* dosya.</span><span class="sxs-lookup"><span data-stu-id="564bf-237">Open the *app/scripts/homeCtrl.js* file.</span></span>
8. <span data-ttu-id="564bf-238">"Kimlik doğrulaması" için işaretlenmiş kod bloğunu çıkışı açıklama ve "ile kimlik doğrulaması" için işaretlenmiş kod bloğunu açıklamadan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="564bf-238">Comment out the block of code marked for "without authentication" and uncomment the block of code marked for "with authentication".</span></span>
9. <span data-ttu-id="564bf-239">Açık *app/scripts/indexCtrl.js* dosya.</span><span class="sxs-lookup"><span data-stu-id="564bf-239">Open the *app/scripts/indexCtrl.js* file.</span></span>
10. <span data-ttu-id="564bf-240">"Kimlik doğrulaması" için işaretlenmiş kod bloğunu çıkışı açıklama ve "ile kimlik doğrulaması" için işaretlenmiş kod bloğunu açıklamadan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="564bf-240">Comment out the block of code marked for "without authentication" and uncomment the block of code marked for "with authentication".</span></span>

### <a name="deploy-the-todolistangular-project-to-azure"></a><span data-ttu-id="564bf-241">ToDoListAngular projesini Azure'a dağıtma</span><span class="sxs-lookup"><span data-stu-id="564bf-241">Deploy the ToDoListAngular project to Azure</span></span>
1. <span data-ttu-id="564bf-242">**Çözüm Gezgini**’nde ToDoListAngular projesine sağ tıklayın ve ardından **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="564bf-242">In **Solution Explorer**, right-click the ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="564bf-243">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="564bf-243">Click **Publish**.</span></span>
   
    <span data-ttu-id="564bf-244">Visual Studio projesini dağıtır ve web uygulamanızın temel URL'sini bir tarayıcı penceresinde açar.</span><span class="sxs-lookup"><span data-stu-id="564bf-244">Visual Studio deploys the project and opens a browser to the web app's base URL.</span></span> <span data-ttu-id="564bf-245">Bu bir Web API temel URL'yi bir tarayıcı üzerinden Git girişimi için normal bir 403 hata sayfası gösterilir.</span><span class="sxs-lookup"><span data-stu-id="564bf-245">This will show a 403 error page, which is normal for an attempt to go to a Web API base URL from a browser.</span></span>
   
    <span data-ttu-id="564bf-246">Uygulamayı test önce için orta katman API uygulaması değişiklik çözümlenmedi.</span><span class="sxs-lookup"><span data-stu-id="564bf-246">You still have to make a change to the middle tier API app before you can test the application.</span></span>
3. <span data-ttu-id="564bf-247">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="564bf-247">Close the browser.</span></span>

## <a name="configure-the-todolistapi-project-to-use-authentication"></a><span data-ttu-id="564bf-248">Todolistapı projesi kimlik doğrulaması kullanacak şekilde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="564bf-248">Configure the ToDoListAPI project to use authentication</span></span>
<span data-ttu-id="564bf-249">Şu anda Todolistapı projesine gönderir "*" olarak `owner` Todolistdataapı değeri.</span><span class="sxs-lookup"><span data-stu-id="564bf-249">Currently the ToDoListAPI project sends "*" as the `owner` value to ToDoListDataAPI.</span></span> <span data-ttu-id="564bf-250">Bu bölümde oturum açmış kullanıcının Kimliğini göndermek için kodu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="564bf-250">In this section you change the code to send the ID of the logged-on user.</span></span>

<span data-ttu-id="564bf-251">Todolistapı projesinde aşağıdaki değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="564bf-251">Make the following changes in the ToDoListAPI project.</span></span>

1. <span data-ttu-id="564bf-252">Açık *Controllers/ToDoListController.cs* dosya ve ayarlar her eylem yöntemindeki satırı açıklamadan kaldırmasına `owner` Azure ad `NameIdentifier` talep değeri.</span><span class="sxs-lookup"><span data-stu-id="564bf-252">Open the *Controllers/ToDoListController.cs* file, and uncomment the line in each action method that sets `owner` to the Azure AD `NameIdentifier` claim value.</span></span> <span data-ttu-id="564bf-253">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="564bf-253">For example:</span></span>
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    <span data-ttu-id="564bf-254">**Önemli**: kodda açıklamadan çıkarın yok `ToDoListDataAPI` yöntemi; bu daha sonra hizmet asıl kimlik doğrulaması öğretici için gerçekleştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="564bf-254">**Important**: Don't uncomment code in the `ToDoListDataAPI` method; you'll do that later for the service principal authentication tutorial.</span></span>

### <a name="deploy-the-todolistapi-project-to-azure"></a><span data-ttu-id="564bf-255">Todolistapı projesini Azure'a dağıtma</span><span class="sxs-lookup"><span data-stu-id="564bf-255">Deploy the ToDoListAPI project to Azure</span></span>
1. <span data-ttu-id="564bf-256">İçinde **Çözüm Gezgini**, Todolistapı projesine sağ tıklayın ve ardından **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="564bf-256">In **Solution Explorer**, right-click the ToDoListAPI project, and then click **Publish**.</span></span>
2. <span data-ttu-id="564bf-257">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="564bf-257">Click **Publish**.</span></span>
   
    <span data-ttu-id="564bf-258">Visual Studio projesini dağıtır ve API uygulamasının temel URL'sini bir tarayıcı açar.</span><span class="sxs-lookup"><span data-stu-id="564bf-258">Visual Studio deploys the project and opens a browser to the API app's base URL.</span></span>
3. <span data-ttu-id="564bf-259">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="564bf-259">Close the browser.</span></span>

### <a name="test-the-application"></a><span data-ttu-id="564bf-260">Uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="564bf-260">Test the application</span></span>
1. <span data-ttu-id="564bf-261">Web uygulamasının URL'sini gidin **HTTPS değil HTTP kullanarak**.</span><span class="sxs-lookup"><span data-stu-id="564bf-261">Go to the URL of the web app, **using HTTPS, not HTTP**.</span></span>
2. <span data-ttu-id="564bf-262">Tıklatın **Yapılacaklar listesi** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="564bf-262">Click the **To Do List** tab.</span></span>
   
    <span data-ttu-id="564bf-263">Oturum açma istenir.</span><span class="sxs-lookup"><span data-stu-id="564bf-263">You are prompted to log in.</span></span>
3. <span data-ttu-id="564bf-264">AAD kiracınızda bir kullanıcının kimlik bilgileriyle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="564bf-264">Log in with the credentials of a user in your AAD tenant.</span></span>
4. <span data-ttu-id="564bf-265">**Yapılacaklar listesi** sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="564bf-265">The **To Do List** page appears.</span></span>
   
   ![Sayfa, yapılacaklar listesi](./media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   <span data-ttu-id="564bf-267">Şimdiye kadar bunların tümünü sahibi bırakıldığından Yapılacaklar öğelerini görüntülenen "*".</span><span class="sxs-lookup"><span data-stu-id="564bf-267">No to-do items are displayed because until now they have all been for owner "*".</span></span> <span data-ttu-id="564bf-268">Orta katman öğeleri oturum açan kullanıcı için şimdi isteme ve hiçbiri henüz oluşturulmadı.</span><span class="sxs-lookup"><span data-stu-id="564bf-268">Now the middle tier is requesting items for the logged-on user, and none have been created yet.</span></span>
5. <span data-ttu-id="564bf-269">Uygulamanın çalıştığını doğrulamak için yeni yapılacak iş öğeleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="564bf-269">Add new to-do items to verify that the application is working.</span></span>
6. <span data-ttu-id="564bf-270">Başka bir tarayıcı penceresinde Todolistdataapı API uygulaması için Swagger kullanıcı Arabirimi URL'sine gidin ve **ToDoList > almak**.</span><span class="sxs-lookup"><span data-stu-id="564bf-270">In another browser window, go to the Swagger UI URL for the ToDoListDataAPI API app and click **ToDoList > Get**.</span></span> <span data-ttu-id="564bf-271">İçin bir yıldız işareti girin `owner` parametre ve ardından **deneyin**.</span><span class="sxs-lookup"><span data-stu-id="564bf-271">Enter an asterisk for the `owner` parameter, and then click **Try it out**.</span></span>
   
   <span data-ttu-id="564bf-272">Yanıt yeni yapılacak iş öğeleri gerçek olduğunu gösterir. Owner özelliği Azure AD kullanıcı kimliği.</span><span class="sxs-lookup"><span data-stu-id="564bf-272">The response shows that the new to-do items have the actual Azure AD user ID in the Owner property.</span></span>
   
   ![JSON yanıt sahibinin kimliği](./media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-the-projects-from-scratch"></a><span data-ttu-id="564bf-274">Sıfırdan projeler derleme</span><span class="sxs-lookup"><span data-stu-id="564bf-274">Building the projects from scratch</span></span>
<span data-ttu-id="564bf-275">İki Web API projeleri kullanılarak oluşturulan **Azure API uygulaması** proje şablonu ve varsayılan değerleri denetleyicisi ToDoList denetleyicisiyle değiştirme.</span><span class="sxs-lookup"><span data-stu-id="564bf-275">The two Web API projects were created by using the **Azure API App** project template and replacing the default Values controller with a ToDoList controller.</span></span> 

<span data-ttu-id="564bf-276">AngularJS tek sayfalı uygulama ile Web API 2 arka plan oluşturma hakkında daha fazla bilgi için bkz: [ellere üzerindeki Laboratuvar: tek sayfa uygulama (SPA) ASP.NET Web API ve Angular.js yapı](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs).</span><span class="sxs-lookup"><span data-stu-id="564bf-276">For information about how to  create an AngularJS single-page application with a Web API 2 back end, see  [Hands On Lab: Build a Single Page Application (SPA) with ASP.NET Web API and Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs).</span></span> <span data-ttu-id="564bf-277">Azure AD kimlik doğrulama kodu ekleme hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="564bf-277">For information about how to add Azure AD authentication code, see the following resources:</span></span>

* <span data-ttu-id="564bf-278">[AngularJS tek güvenli hale getirme sayfasında Azure AD ile uygulamaları](../active-directory/active-directory-devquickstarts-angular.md).</span><span class="sxs-lookup"><span data-stu-id="564bf-278">[Securing AngularJS Single Page Apps with Azure AD](../active-directory/active-directory-devquickstarts-angular.md).</span></span>
* [<span data-ttu-id="564bf-279">ADAL JS v1 Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="564bf-279">Introducing ADAL JS v1</span></span>](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a><span data-ttu-id="564bf-280">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="564bf-280">Troubleshooting</span></span>
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* <span data-ttu-id="564bf-281">Todolistapı (orta katman) ve Todolistdataapı (veri katmanı) karıştırmayın emin olun.</span><span class="sxs-lookup"><span data-stu-id="564bf-281">Make sure that you don't confuse ToDoListAPI (middle tier) and ToDoListDataAPI (data tier).</span></span> <span data-ttu-id="564bf-282">Örneğin, veri katmanı orta katman API uygulaması için kimlik doğrulama eklediğinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="564bf-282">For example, verify that you added authentication to the middle tier API app, not the data tier.</span></span> 
* <span data-ttu-id="564bf-283">AngularJS kaynak kodu orta katman API uygulaması URL'sini (Todolistapı, Todolistdataapı değil) ve doğru Azure başvurduğundan emin olun AD istemci kimliği</span><span class="sxs-lookup"><span data-stu-id="564bf-283">Make sure that the AngularJS source code references the middle tier API app URL (ToDoListAPI, not ToDoListDataAPI)and the correct Azure AD client ID.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="564bf-284">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="564bf-284">Next steps</span></span>
<span data-ttu-id="564bf-285">Bu öğreticide bir API uygulaması için uygulama hizmeti kimlik doğrulaması kullanmak ve ADAL JS kitaplığı kullanarak API uygulamasını çağırmak öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="564bf-285">In this tutorial you learned how to use App Service authentication for an API app and how to call the API app by using the ADAL JS library.</span></span> <span data-ttu-id="564bf-286">Sonraki öğreticide şunları öğreneceksiniz nasıl [güvenli API uygulamanıza erişimi hizmeti senaryoları için](app-service-api-dotnet-service-principal-auth.md).</span><span class="sxs-lookup"><span data-stu-id="564bf-286">In the next tutorial you'll learn how to [secure access to your API app for service-to-service scenarios](app-service-api-dotnet-service-principal-auth.md).</span></span>

