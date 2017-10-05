---
title: "Dağıtımı, çağrı ve web API'leri ve REST API'leri Azure Logic Apps için kimlik doğrulaması | Microsoft Docs"
description: "Dağıtma, kimlik doğrulaması ve Azure Logic Apps ile sistem tümleştirmeleri için iş akışlarında web API'leri & REST API çağrısı"
keywords: "Web API'leri, REST API'leri, bağlayıcılar, iş akışları, sistem tümleştirmeler, kimlik doğrulaması"
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 88c62d5ab046d8cf4bce5d23b776e517bb0e1d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a><span data-ttu-id="ea9e1-104">Dağıtımı, arama ve özel API'leri olarak bağlayıcılar mantıksal uygulamalar için kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ea9e1-104">Deploy, call, and authenticate custom APIs as connectors for logic apps</span></span>

<span data-ttu-id="ea9e1-105">Çalıştırdıktan sonra [özel API oluşturma](./logic-apps-create-api-app.md) eylemler veya logic apps akışlarında kullanmak için Tetikleyiciler sağlayın, bunları çağırmadan önce Apı'lerinizi dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-105">After you [create custom APIs](./logic-apps-create-api-app.md) that provide actions or triggers to use in logic apps workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="ea9e1-106">Ve bir mantıksal uygulama, en iyi deneyim için herhangi bir API'yi çağırabilirsiniz rağmen ekleyin [Swagger meta verileri](http://swagger.io/specification/) , API'nin işlemlerini ve parametrelerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-106">And although you can call any API from a logic app, for the best experience, add [Swagger metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="ea9e1-107">Bu Swagger dosyası API'nizi daha iyi ve daha kolay logic apps ile tümleştirmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-107">This Swagger file helps your API work better and integrate more easily with logic apps.</span></span>

<span data-ttu-id="ea9e1-108">API olarak dağıtabilir miyim [web uygulamaları](../app-service-web/app-service-web-overview.md), ancak API olarak dağıtmayı göz önünde bulundurun [API uygulamaları](../app-service-api/app-service-api-apps-why-best-platform.md), hangi yapabilir, işinizi daha kolay yapı, ana bilgisayar ve API'leri bulutta ve şirket içi kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-108">You can deploy your APIs as [web apps](../app-service-web/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service-api/app-service-api-apps-why-best-platform.md), which can make your job easier when you build, host, and consume APIs in the cloud and on premises.</span></span> <span data-ttu-id="ea9e1-109">Tüm Apı'lerinizi kodda değişiklik--yalnızca kodunuzun bir API uygulamasına dağıtmak yok.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-109">You don't have to change any code in your APIs -- just deploy your code to an API app.</span></span> <span data-ttu-id="ea9e1-110">Üzerinde Apı'lerinizi barındırabilir [Azure App Service](../app-service/app-service-value-prop-what-is.md), bir platform olarak-sağlayan en iyi, kolay ve en ölçeklenebilir yollarından biri, API barındırmak için sunan hizmet (PaaS).</span><span class="sxs-lookup"><span data-stu-id="ea9e1-110">You can host your APIs on [Azure App Service](../app-service/app-service-value-prop-what-is.md), a platform-as-a-service (PaaS) offering that provides one of the best, easiest, and most scalable ways for API hosting.</span></span>

<span data-ttu-id="ea9e1-111">Logic apps gelen çağrıları, API'lerine doğrulamak için kodunuzu güncelleştirin zorunda kalmamak için Azure portalında Azure Active Directory'yi ayarlama ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-111">To authenticate calls from logic apps to your APIs, you can set up Azure Active Directory in the Azure portal so you don't have to update your code.</span></span> <span data-ttu-id="ea9e1-112">Veya gerektirir ve kimlik doğrulama, API'nin kodlarda zorlayın.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-112">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="ea9e1-113">API'nizi bir web uygulaması veya API uygulaması olarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="ea9e1-113">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="ea9e1-114">Özel API'nizi mantığı uygulamadan aramadan önce Azure App Service'e API'nizi bir web uygulaması veya API uygulaması olarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-114">Before you can call your custom API from a logic app, deploy your API as a web app or API app to Azure App Service.</span></span> <span data-ttu-id="ea9e1-115">Ayrıca, Swagger belgesinin mantığı Uygulama Tasarımcısı tarafından okunabilir hale getirmek için API tanımı özelliklerini ayarlamak ve Aç [çıkış noktaları arası kaynak paylaşımı (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) web uygulaması veya API uygulaması için.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-115">Also, to make your Swagger document readable by the Logic App Designer, set the API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) for your web app or API app.</span></span>

1. <span data-ttu-id="ea9e1-116">Azure portalında web uygulaması veya API uygulaması seçin.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-116">In the Azure portal, select your web app or API app.</span></span>

2. <span data-ttu-id="ea9e1-117">Açılır ve altında dikey penceresinde **API**, seçin **API tanımı**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-117">In the blade that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="ea9e1-118">Ayarlama **API tanımı konumu** swagger.json dosyanızı URL'si.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-118">Set the **API definition location** to the URL for your swagger.json file.</span></span>

   <span data-ttu-id="ea9e1-119">Genellikle, URL şöyle görünür:`https://{name}.azurewebsites.net/swagger/docs/v1)`</span><span class="sxs-lookup"><span data-stu-id="ea9e1-119">Usually, the URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![Özel API için Swagger dosyasına bağlantı](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. <span data-ttu-id="ea9e1-121">Altında **API**, seçin **CORS**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-121">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="ea9e1-122">CORS İlkesi'ni ayarlamak **çıkış izin** için  **'*'** (tüm izin ver).</span><span class="sxs-lookup"><span data-stu-id="ea9e1-122">Set the CORS policy for **Allowed origins** to **'*'** (allow all).</span></span>

   <span data-ttu-id="ea9e1-123">Bu ayar mantığı Uygulama Tasarımcısı'ndan istekleri verir.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-123">This setting permits requests from Logic App Designer.</span></span>

   ![İstekleri mantığı Uygulama Tasarımcısı'ndan özel API'nizi izin verir.](media/logic-apps-custom-hosted-api/custom-api-cors.png)

<span data-ttu-id="ea9e1-125">Daha fazla bilgi için bu makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="ea9e1-125">For more information, see these articles:</span></span>

* [<span data-ttu-id="ea9e1-126">ASP.NET web API için Swagger meta verileri ekleme</span><span class="sxs-lookup"><span data-stu-id="ea9e1-126">Add Swagger metadata for ASP.NET web APIs</span></span>](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [<span data-ttu-id="ea9e1-127">ASP.NET web API'ları Azure App Service'e dağıtma</span><span class="sxs-lookup"><span data-stu-id="ea9e1-127">Deploy ASP.NET web APIs to Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="ea9e1-128">Özel API'nizi mantığından uygulama iş akışları çağırın.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-128">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="ea9e1-129">API tanımı özellikleri ve CORS ayarladıktan sonra özel API'nin tetikleyiciler ve Eylemler, logic app akışınıza eklemek kullanılabilir duruma gelir.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-129">After you set up the API definition properties and CORS, your custom API's triggers and actions should become available for you to include in your logic app workflow.</span></span> 

*  <span data-ttu-id="ea9e1-130">Swagger URL'lere sahip Web siteleri görüntülemek için Logic Apps Tasarımcısı'nda, abonelik Web sitelerine göz atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-130">To view the websites that have Swagger URLs, you can browse your subscription websites in the Logic Apps Designer.</span></span>

*  <span data-ttu-id="ea9e1-131">Swagger belgesinin göstererek kullanılabilir eylemler ve girişleri görüntülemek için kullanın [HTTP + Swagger eylem](../connectors/connectors-native-http-swagger.md).</span><span class="sxs-lookup"><span data-stu-id="ea9e1-131">To view available actions and inputs by pointing at a Swagger document, use the [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="ea9e1-132">Yok veya bir Swagger belgesinin kullanıma API'leri dahil olmak üzere herhangi bir API'yi çağırmak için her zaman bir istekle oluşturabilirsiniz [HTTP eylemi](../connectors/connectors-native-http.md).</span><span class="sxs-lookup"><span data-stu-id="ea9e1-132">To call any API, including APIs that don't have or expose a Swagger document, you can always create a request with the [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="authenticate-calls-to-your-custom-api"></a><span data-ttu-id="ea9e1-133">Kimlik doğrulaması, özel API çağrıları</span><span class="sxs-lookup"><span data-stu-id="ea9e1-133">Authenticate calls to your custom API</span></span>

<span data-ttu-id="ea9e1-134">Bu şekilde, özel API çağrıları güvenliğini sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ea9e1-134">You can secure calls to your custom API in these ways:</span></span>

* <span data-ttu-id="ea9e1-135">[Kod değişiklikleri](#no-code): API'nizi ile koruma [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) Azure portalı üzerinden bu nedenle, kodunuzu güncelleştirin veya API'nizi yeniden dağıtmak zorunda değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-135">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) through the Azure portal, so you don't have to update your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ea9e1-136">Varsayılan olarak, Azure portalında kapatma Azure AD kimlik doğrulaması hassas yetkilendirme sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-136">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="ea9e1-137">Örneğin, bu kimlik doğrulama API'nizi yalnızca belirli bir kiracı için değil, belirli bir kullanıcı veya uygulama kilitler.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-137">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span></span> 

* <span data-ttu-id="ea9e1-138">[API kodunu güncelleştirin](#update-code): zorlayarak API'nizi koruma [sertifika kimlik doğrulaması](#certificate), [temel kimlik doğrulaması](#basic), veya [Azure AD kimlik doğrulaması](#azure-ad-code) kodlarda.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-138">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-to-your-api-without-changing-code"></a><span data-ttu-id="ea9e1-139">Kodunu değiştirmeden, API çağrıları kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ea9e1-139">Authenticate calls to your API without changing code</span></span>

<span data-ttu-id="ea9e1-140">Bu yöntem için genel adımlar aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="ea9e1-140">Here's the general steps for this method:</span></span>

1. <span data-ttu-id="ea9e1-141">İki oluşturmak [Azure Active Directory (Azure AD) uygulama kimlikleri](../app-service-api/app-service-api-dotnet-service-principal-auth.md): mantıksal uygulamanızı, diğeri web uygulaması (veya API uygulaması) için.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-141">Create two [Azure Active Directory (Azure AD) application identities](../app-service-api/app-service-api-dotnet-service-principal-auth.md): one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="ea9e1-142">API'nizi çağrı kimliğini doğrulamak için kimlik bilgilerini (istemci kimliği ve parolası) kullanın [hizmet sorumlusu](../app-service-api/app-service-api-dotnet-service-principal-auth.md) mantıksal uygulamanız için Azure AD uygulama kimliği ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-142">To authenticate calls to your API, use the credentials (client ID and secret) for the [service principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) that's associated with the Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="ea9e1-143">Uygulama kimlikleri mantığı uygulama tanımınızı içerir.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-143">Include the application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="ea9e1-144">1. Kısım: mantıksal uygulamanız için bir Azure AD uygulama kimliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea9e1-144">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="ea9e1-145">Mantıksal uygulamanızı Azure AD karşı kimlik doğrulaması için bu Azure AD uygulama kimliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-145">Your logic app uses this Azure AD application identity to authenticate against Azure AD.</span></span> <span data-ttu-id="ea9e1-146">Yalnızca bu kimliği dizininiz için bir kez ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-146">You only have to set up this identity one time for your directory.</span></span> <span data-ttu-id="ea9e1-147">Örneğin, her mantıksal uygulama için benzersiz kimlik Oluştur olsa bile, tüm mantıksal uygulamalar için aynı kimlik kullanmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-147">For example, you can choose to use the same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="ea9e1-148">Azure portalında bu kimlikleri ayarlayabilirsiniz [Klasik Azure portalı](#app-identity-logic-classic), veya [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="ea9e1-148">You can set up these identities in the Azure portal, [Azure classic portal](#app-identity-logic-classic), or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="ea9e1-149">**Azure portalda mantıksal uygulamanızı için uygulama kimliği oluşturma**</span><span class="sxs-lookup"><span data-stu-id="ea9e1-149">**Create the application identity for your logic app in the Azure portal**</span></span>

1. <span data-ttu-id="ea9e1-150">İçinde [Azure portal](https://portal.azure.com "https://portal.azure.com"), seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-150">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="ea9e1-151">Web uygulaması veya API uygulaması olarak aynı dizinde olduğunuzu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-151">Confirm that you're in the same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="ea9e1-152">Dizinleri geçmek için profilinizi tıklatın ve başka bir dizin seçin.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-152">To switch directories, click your profile and select another directory.</span></span> <span data-ttu-id="ea9e1-153">Ya da seçin **genel bakış** > **anahtar dizini**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-153">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="ea9e1-154">Dizin menüsünde altında **Yönet**, seçin **uygulama kayıtlar** > **yeni uygulama kaydı**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-154">On the directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="ea9e1-155">Varsayılan olarak, dizininizdeki tüm uygulama kayıtları uygulama kayıtlar listesi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-155">By default, the app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="ea9e1-156">Yalnızca, uygulama kayıtlar yanındaki Arama kutusunu görüntülemek için seçin **uygulamalarım**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-156">To view only your app registrations, next to the search box, select **My apps**.</span></span> 

   ![Yeni uygulama kaydı oluşturun](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. <span data-ttu-id="ea9e1-158">Uygulama kimliğinizi bir ad verin, bırakın **uygulama türü** kümesine **Web uygulaması / API**, benzersiz bir sağlamak için bir etki alanı olarak biçimlendirilmiş dize **oturum açma URL'si**ve seçin **Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-158">Give your application identity a name, leave **Application type** set to **Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![URL için uygulama kimliği oturum adı girin ve](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   <span data-ttu-id="ea9e1-160">Mantıksal uygulamanız artık oluşturduğunuz uygulama kimliğini uygulama kayıtlar listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-160">The application identity that you created for your logic app now appears in the app registrations list.</span></span>

   ![Mantıksal uygulamanız için uygulama kimliği](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. <span data-ttu-id="ea9e1-162">Uygulama kayıtlar listesinde, yeni uygulama kimliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-162">In the app registrations list, select your new application identity.</span></span> <span data-ttu-id="ea9e1-163">Kopyalayıp kaydedin **uygulama kimliği** mantıksal uygulamanızı bölümü 3'te "istemci kimlik" olarak kullanılmak üzere.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-163">Copy and save the **Application ID** to use as the "client ID" for your logic app in Part 3.</span></span>

   ![Kopyalayın ve mantıksal uygulama için uygulama kimliği kaydedin](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. <span data-ttu-id="ea9e1-165">Uygulama Kimliği ayarlarınızı görünür durumda değilse, seçin **ayarları** veya **tüm ayarları**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-165">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="ea9e1-166">Altında **API erişimini**, seçin **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-166">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="ea9e1-167">Altında **açıklama**, anahtarınız için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-167">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="ea9e1-168">Altında **Expires**, anahtarınız için bir süre seçin.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-168">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="ea9e1-169">Oluşturmakta olduğunuz anahtar uygulama kimliğin "gizli" veya parolasını mantıksal uygulamanızı olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-169">The key that you're creating acts as the application identity's "secret" or password for your logic app.</span></span>

   ![Mantıksal uygulama kimliği için anahtar oluşturma](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="ea9e1-171">Araç çubuğunda seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-171">On the toolbar, choose **Save**.</span></span> <span data-ttu-id="ea9e1-172">Altında **değeri**, anahtarınızı artık görünür.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-172">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="ea9e1-173">**Kopyalama ve anahtarınızı kaydetmek emin olun** daha sonra kullanmak üzere anahtar gizli olduğu çıktığınızda anahtar dikey.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-173">**Make sure to copy and save your key** for later use because the key is hidden when you leave the key blade.</span></span>

   <span data-ttu-id="ea9e1-174">Mantıksal uygulamanızı bölümü 3'te yapılandırdığınızda, bu anahtarı parola ya da "gizli" olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-174">When you configure your logic app in Part 3, you specify this key as the "secret" or password.</span></span>

   ![Kopyalayın ve anahtarı için daha sonra kaydedin](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

<span data-ttu-id="ea9e1-176">**Azure Klasik Portalı'nda mantığı uygulamanız için uygulama kimliği oluşturma**</span><span class="sxs-lookup"><span data-stu-id="ea9e1-176">**Create the application identity for your logic app in the Azure classic portal**</span></span>

1. <span data-ttu-id="ea9e1-177">Klasik Azure portalında seçin [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="ea9e1-177">In the Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2. <span data-ttu-id="ea9e1-178">Web uygulaması veya API uygulaması için kullandığınız aynı dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-178">Select the same directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="ea9e1-179">Üzerinde **uygulamaları** sekmesinde, seçin **Ekle** sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-179">On the **Applications** tab, choose **Add** at the bottom of the page.</span></span>

4. <span data-ttu-id="ea9e1-180">Uygulama kimliğinizi bir ad verin ve seçin **sonraki** (sağ ok).</span><span class="sxs-lookup"><span data-stu-id="ea9e1-180">Give your application identity a name, and choose **Next** (right arrow).</span></span>

5. <span data-ttu-id="ea9e1-181">Altında **uygulama özellikleri**, benzersiz bir sağlamak için bir etki alanı olarak biçimlendirilmiş dize **oturum açma URL'si** ve **uygulama kimliği URI'si**ve seçin **tam** (onay işareti).</span><span class="sxs-lookup"><span data-stu-id="ea9e1-181">Under **App properties**, provide a unique string formatted as a domain for **Sign-on URL** and **App ID URI**, and choose **Complete** (checkmark).</span></span>

6. <span data-ttu-id="ea9e1-182">Üzerinde **yapılandırma** sekmesinde, kopyalamak ve kaydetme **istemci kimliği** bölümü 3'te kullanmak mantığı uygulamanız için.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-182">On the **Configure** tab, copy and save the **Client ID** for your logic app to use in Part 3.</span></span>

7. <span data-ttu-id="ea9e1-183">Altında **anahtarları**, açık **seçin süresi** listesi.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-183">Under **Keys**, open the **Select duration** list.</span></span> <span data-ttu-id="ea9e1-184">Anahtarınız için bir süre seçin.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-184">Select a duration for your key.</span></span>

   <span data-ttu-id="ea9e1-185">Oluşturmakta olduğunuz anahtar uygulama kimliğin "gizli" veya parolasını mantıksal uygulamanızı olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-185">The key that you're creating acts as the application identity's "secret" or password for your logic app.</span></span>

8. <span data-ttu-id="ea9e1-186">Sayfanın alt kısmındaki seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-186">At the bottom of the page, choose **Save**.</span></span> <span data-ttu-id="ea9e1-187">Birkaç saniye beklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-187">You might have to wait a few seconds.</span></span>

9. <span data-ttu-id="ea9e1-188">Altında **anahtarları**kopyaladığınızdan emin olun ve anahtarı kaydetme artık görünür.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-188">Under **Keys**, make sure to copy and save the key that now appears.</span></span> 

   <span data-ttu-id="ea9e1-189">Mantıksal uygulamanızı bölümü 3'te yapılandırdığınızda, bu anahtarı parola ya da "gizli" olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-189">When you configure your logic app in Part 3, you specify this key as the "secret" or password.</span></span>

<span data-ttu-id="ea9e1-190">Daha fazla bilgi için bilgi nasıl [uygulama hizmeti uygulamanızı Azure Active Directory oturum açma kullanacak şekilde yapılandırma](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ea9e1-190">For more information, learn how to [configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

<a name="powershell"></a>

<span data-ttu-id="ea9e1-191">**PowerShell'de mantığı uygulamanız için uygulama kimliği oluşturma**</span><span class="sxs-lookup"><span data-stu-id="ea9e1-191">**Create the application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="ea9e1-192">Bu görevi PowerShell ile Azure Resource Manager aracılığıyla gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-192">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="ea9e1-193">PowerShell'de aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ea9e1-193">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="ea9e1-194">Kopyaladığınızdan emin olun **Kiracı kimliği** (GUID) Azure AD kiracınız için **uygulama kimliği**ve kullandığınız parola.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-194">Make sure to copy the **Tenant ID** (GUID for your Azure AD tenant), the **Application ID**, and the password that you used.</span></span>

<span data-ttu-id="ea9e1-195">Daha fazla bilgi için bilgi nasıl [kaynaklarına erişmek için PowerShell ile bir hizmet sorumlusu oluşturma](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="ea9e1-195">For more information, learn how to [create a service principal with PowerShell to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="ea9e1-196">Bölüm 2: web uygulaması veya API uygulaması için bir Azure AD uygulama kimliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea9e1-196">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="ea9e1-197">Web uygulaması veya API uygulama zaten dağıtılmışsa, kimlik doğrulamasını etkinleştirmek ve Azure portalında uygulama kimliği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-197">If your web app or API app is already deployed, you can turn on authentication and create the application identity in the Azure portal.</span></span> <span data-ttu-id="ea9e1-198">Aksi takdirde, şunları yapabilirsiniz [bir Azure Resource Manager şablonu ile dağıtırken kimlik doğrulamasını etkinleştirmek](#authen-deploy).</span><span class="sxs-lookup"><span data-stu-id="ea9e1-198">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="ea9e1-199">**Uygulama Kimliği oluşturma ve kimlik doğrulama dağıtılan uygulamalar için Azure Portalı'nda Aç**</span><span class="sxs-lookup"><span data-stu-id="ea9e1-199">**Create the application identity and turn on authentication in the Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="ea9e1-200">İçinde [Azure portal](https://portal.azure.com "https://portal.azure.com"), bulma ve web uygulaması veya API uygulaması seçin.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-200">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="ea9e1-201">Altında **ayarları**, seçin **kimlik doğrulama/yetkilendirme**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-201">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="ea9e1-202">Altında **App Service kimlik doğrulaması**, kimlik doğrulamasını **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-202">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="ea9e1-203">Altında **kimlik doğrulama sağlayıcıları**, seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-203">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![Kimlik doğrulamasını etkinleştirmek](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. <span data-ttu-id="ea9e1-205">Artık web uygulaması veya API uygulaması için uygulama kimliği, aşağıda gösterildiği gibi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-205">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="ea9e1-206">Üzerinde **Azure Active Directory ayarları** dikey penceresinde ayarlamak **yönetim modu** için **Express**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-206">On the **Azure Active Directory Settings** blade, set **Management mode** to **Express**.</span></span> <span data-ttu-id="ea9e1-207">Seçin **yeni AD uygulaması oluştur**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-207">Choose **Create New AD App**.</span></span> <span data-ttu-id="ea9e1-208">Uygulama kimliğinizi bir ad verin ve seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-208">Give your application identity a name, and choose **OK**.</span></span> 

   ![Web uygulaması veya API uygulaması için uygulama kimliği oluşturma](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. <span data-ttu-id="ea9e1-210">Üzerinde **kimlik doğrulama / yetkilendirme dikey**, seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-210">On the **Authentication / Authorization blade**, choose **Save**.</span></span>

<span data-ttu-id="ea9e1-211">Artık web uygulaması veya API uygulaması ile ilişkili olan uygulama kimliği için istemci kimliği ve Kiracı kimliği bulmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-211">Now you must find the client ID and tenant ID for the application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="ea9e1-212">Bu kimlikleri bölümü 3'te kullanın.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-212">You use these IDs in Part 3.</span></span> <span data-ttu-id="ea9e1-213">Bu nedenle Azure portalı için aşağıdaki adımları devam veya [Klasik Azure portalı](#find-id-classic).</span><span class="sxs-lookup"><span data-stu-id="ea9e1-213">So continue with these steps for the Azure portal or [Azure classic portal](#find-id-classic).</span></span>

<span data-ttu-id="ea9e1-214">**Web uygulaması veya API uygulaması için uygulama kimliği'nin istemci kimliği ve Kiracı kimliği Azure portalında Bul**</span><span class="sxs-lookup"><span data-stu-id="ea9e1-214">**Find application identity's client ID and tenant ID for your web app or API app in the Azure portal**</span></span>

1. <span data-ttu-id="ea9e1-215">Altında **kimlik doğrulama sağlayıcıları**, seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-215">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   !["Azure Active Directory" seçin](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="ea9e1-217">Üzerinde **Azure Active Directory ayarları** dikey penceresinde ayarlamak **yönetim modu** için **Gelişmiş**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-217">On the **Azure Active Directory Settings** blade, set **Management mode** to **Advanced**.</span></span>

3. <span data-ttu-id="ea9e1-218">Kopya **istemci kimliği**ve bölüm 3'te kullanmak için bu GUID'i kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-218">Copy the **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="ea9e1-219">Varsa **istemci kimliği** ve **veren URL'si** yoksa, görünür, Azure portal'ı yenilemeyi deneyin ve 1. adım yineleyin.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-219">If **Client ID** and **Issuer Url** don't appear, try refreshing the Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="ea9e1-220">Altında **veren URL'si**, kopyalamak ve yalnızca GUID için bölümü 3 kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-220">Under **Issuer Url**, copy and save just the GUID for Part 3.</span></span> <span data-ttu-id="ea9e1-221">Aynı zamanda bu GUID web uygulamanızı veya API uygulamasının dağıtım şablonu, gerekirse kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-221">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="ea9e1-222">Bu GUID belirli kiracının GUID ("Kiracı kimliği") ve bu URL'de görünmelidir:`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="ea9e1-222">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="ea9e1-223">Değişikliklerinizi kaydetmeden kapatın **Azure Active Directory ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-223">Without saving your changes, close the **Azure Active Directory Settings** blade.</span></span>

<a name="find-id-classic"></a>

<span data-ttu-id="ea9e1-224">**Uygulama Kimliği'nin istemci kimliği ve Kiracı kimliği web uygulamanızı veya API uygulaması için Azure Klasik Portalı'nda bulunamıyor**</span><span class="sxs-lookup"><span data-stu-id="ea9e1-224">**Find application identity's client ID and tenant ID for your web app or API app in the Azure classic portal**</span></span>

1. <span data-ttu-id="ea9e1-225">Klasik Azure portalında seçin [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="ea9e1-225">In the Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2.  <span data-ttu-id="ea9e1-226">Web uygulaması veya API uygulaması için kullandığınız dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-226">Select the directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="ea9e1-227">İçinde **arama** kutusunda bulmak ve web uygulaması veya API uygulaması için uygulama kimliği seçin.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-227">In the **Search** box, find and select the application identity for your web app or API app.</span></span>

4. <span data-ttu-id="ea9e1-228">Üzerinde **yapılandırma** sekmesinde, kopya **istemci kimliği**ve bölüm 3'te kullanmak için bu GUID'i kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-228">On the **Configure** tab, copy the **Client ID**, and save that GUID for use in Part 3.</span></span>

5. <span data-ttu-id="ea9e1-229">İstemci kimliği alt kısmındaki aldıktan sonra **yapılandırma** sekmesinde, seçin **uç noktaları görüntülemek**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-229">After you get the client ID, at the bottom of the **Configure** tab, choose **View endpoints**.</span></span>

6. <span data-ttu-id="ea9e1-230">URL'sini kopyalayın **Federasyon meta veri belgesi**ve bu URL'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-230">Copy the URL for **Federation Metadata Document**, and browse to that URL.</span></span>

7. <span data-ttu-id="ea9e1-231">Kök açar meta veri belgesi bulabilir **EntityDescriptor kimliği** var öğesi bir **Entityıd** özniteliği bu formda:`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="ea9e1-231">In the metadata document that opens, find the root **EntityDescriptor ID** element, which has an **entityID** attribute in this form: `https://sts.windows.net/{GUID}`</span></span> 

      <span data-ttu-id="ea9e1-232">Bu öznitelik belirli kiracının GUID (Kiracı kimliği) olarak GUID'dir.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-232">The GUID in this attribute is your specific tenant's GUID (tenant ID).</span></span>

8. <span data-ttu-id="ea9e1-233">Kiracı kimliği kopyalayın ve gerekirse kullanmak için bu kimliği bölümü 3'te ve web uygulamanızı veya API uygulamasının dağıtım şablonu kullanmak üzere kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-233">Copy the tenant ID and save that ID for use in Part 3, and also to use in your web app or API app's deployment template, if necessary.</span></span>

<span data-ttu-id="ea9e1-234">Daha fazla bilgi için şu konulara bakın:</span><span class="sxs-lookup"><span data-stu-id="ea9e1-234">For more information, see these topics:</span></span>

* [<span data-ttu-id="ea9e1-235">Azure uygulama hizmetinde API uygulamaları için kullanıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ea9e1-235">User authentication for API apps in Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [<span data-ttu-id="ea9e1-236">Kimlik doğrulama ve yetkilendirme Azure uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="ea9e1-236">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

<span data-ttu-id="ea9e1-237">**Bir Azure Resource Manager şablonu ile dağıtırken kimlik doğrulamasını etkinleştirmek**</span><span class="sxs-lookup"><span data-stu-id="ea9e1-237">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="ea9e1-238">Hala mantığı uygulamanız için uygulama kimliği web uygulaması veya farklı bir API uygulaması için bir Azure AD uygulama kimliği da oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-238">You must still create an Azure AD application identity for your web app or API app that differs from the app identity for your logic app.</span></span> <span data-ttu-id="ea9e1-239">Uygulama kimliği oluşturmak için Azure portalı için Kısım 2 önceki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-239">To create the application identity, follow the previous steps in Part 2 for the Azure portal.</span></span> <span data-ttu-id="ea9e1-240">Ayrıca, 1. Bölüm adımları ancak web uygulamanızı veya API uygulamasının gerçek kullandığınızdan emin olun `https://{URL}` için **oturum açma URL'si** ve **uygulama kimliği URI'si**.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-240">You can also follow the steps in Part 1, but make sure to use your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="ea9e1-241">Bu adımları, istemci kimliği ve Kiracı kimliği, uygulamanızın dağıtım şablonu kullanmak için ve ayrıca bölümü 3 kaydetmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-241">From these steps, you have to save both the client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="ea9e1-242">Web uygulaması veya API uygulaması için Azure AD uygulama kimliği oluşturduğunuzda, Azure portalında veya Klasik Azure portalı yerine PowerShell kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-242">When you create the Azure AD application identity for your web app or API app, you must use the Azure portal or Azure classic portal, rather than PowerShell.</span></span> <span data-ttu-id="ea9e1-243">PowerShell komutunu kullanıcılar bir Web sitesine oturum için gerekli izinleri ayarlayın değil.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-243">The PowerShell commandlet doesn't set up the required permissions to sign users into a website.</span></span>

<span data-ttu-id="ea9e1-244">İstemci kimliği ve Kiracı kimliği aldıktan sonra bu kimlikleri subresource web uygulaması veya API uygulaması için dağıtım şablonunda olarak şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="ea9e1-244">After you get the client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

<span data-ttu-id="ea9e1-245">Boş web uygulaması ve bir mantıksal uygulama Azure Active Directory kimlik doğrulaması ile birlikte otomatik olarak dağıtmak için [burada tam şablonu görüntüleme](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), veya **Azure'a Dağıt** burada:</span><span class="sxs-lookup"><span data-stu-id="ea9e1-245">To automatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view the complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy to Azure** here:</span></span>

<span data-ttu-id="ea9e1-246">[![Azure’a dağıtma](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="ea9e1-246">[![Deploy to Azure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-the-authorization-section-in-your-logic-app"></a><span data-ttu-id="ea9e1-247">3. Kısım: mantıksal uygulamanızı yetkilendirme bölümünde doldurma</span><span class="sxs-lookup"><span data-stu-id="ea9e1-247">Part 3: Populate the Authorization section in your logic app</span></span>

<span data-ttu-id="ea9e1-248">Önceki şablonu zaten bu yetkilendirmesi bölümünde ayarladığınız sahip, ancak mantıksal uygulama doğrudan yazıyorsanız, tam yetkilendirme bölümü içermelidir.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-248">The previous template already has this authorization section set up, but if you are directly authoring the logic app, you must include the full authorization section.</span></span>

<span data-ttu-id="ea9e1-249">Açık mantığı uygulama tanımınızı kod görünümünde Git **HTTP** eylem bölümü Bul **yetkilendirme** bölümünde ve bu satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ea9e1-249">Open your logic app definition in code view, go to the **HTTP** action section, find the **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="ea9e1-250">Öğesi</span><span class="sxs-lookup"><span data-stu-id="ea9e1-250">Element</span></span> | <span data-ttu-id="ea9e1-251">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ea9e1-251">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="ea9e1-252">Kiracı</span><span class="sxs-lookup"><span data-stu-id="ea9e1-252">tenant</span></span> |<span data-ttu-id="ea9e1-253">Azure AD kiracısı için GUID</span><span class="sxs-lookup"><span data-stu-id="ea9e1-253">The GUID for the Azure AD tenant</span></span> |
| <span data-ttu-id="ea9e1-254">Hedef kitle</span><span class="sxs-lookup"><span data-stu-id="ea9e1-254">audience</span></span> |<span data-ttu-id="ea9e1-255">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-255">Required.</span></span> <span data-ttu-id="ea9e1-256">Erişim - web uygulaması veya API uygulaması için uygulama kimliği istemci Kimliğinden istediğiniz hedef kaynak için GUID</span><span class="sxs-lookup"><span data-stu-id="ea9e1-256">The GUID for the target resource that you want to access - the client ID from the application identity for your web app or API app</span></span> |
| <span data-ttu-id="ea9e1-257">istemci kimliği</span><span class="sxs-lookup"><span data-stu-id="ea9e1-257">clientId</span></span> |<span data-ttu-id="ea9e1-258">Access - mantıksal uygulamanızı için uygulama kimliği istemci Kimliğinden isteyen istemci için GUID</span><span class="sxs-lookup"><span data-stu-id="ea9e1-258">The GUID for the client requesting access - the client ID from the application identity for your logic app</span></span> |
| <span data-ttu-id="ea9e1-259">Gizli</span><span class="sxs-lookup"><span data-stu-id="ea9e1-259">secret</span></span> |<span data-ttu-id="ea9e1-260">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-260">Required.</span></span> <span data-ttu-id="ea9e1-261">Anahtar ya da erişim belirteci isteyen istemci için uygulama kimliği paroladan</span><span class="sxs-lookup"><span data-stu-id="ea9e1-261">The key or password from the application identity for the client that's requesting the access token</span></span> |
| <span data-ttu-id="ea9e1-262">type</span><span class="sxs-lookup"><span data-stu-id="ea9e1-262">type</span></span> |<span data-ttu-id="ea9e1-263">Kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-263">The authentication type.</span></span> <span data-ttu-id="ea9e1-264">ActiveDirectoryOAuth kimlik doğrulaması için değerdir `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-264">For ActiveDirectoryOAuth authentication, the value is `ActiveDirectoryOAuth`.</span></span> |

<span data-ttu-id="ea9e1-265">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ea9e1-265">For example:</span></span>

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="ea9e1-266">Kod aracılığıyla güvenli API çağrıları</span><span class="sxs-lookup"><span data-stu-id="ea9e1-266">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="ea9e1-267">Sertifika kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ea9e1-267">Certificate authentication</span></span>

<span data-ttu-id="ea9e1-268">Web uygulaması veya API uygulaması için mantıksal uygulamanızı öğesinden gelen istekleri doğrulamak için istemci sertifikaları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-268">To validate the incoming requests from your logic app to your web app or API app, you can use client certificates.</span></span> <span data-ttu-id="ea9e1-269">Kodu ayarlamak için bilgi [TLS karşılıklı kimlik doğrulamasını yapılandırmak nasıl](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span><span class="sxs-lookup"><span data-stu-id="ea9e1-269">To set up your code, learn [how to configure TLS mutual authentication](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="ea9e1-270">İçinde **yetkilendirme** bölümünde, bu satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ea9e1-270">In the **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="ea9e1-271">Öğesi</span><span class="sxs-lookup"><span data-stu-id="ea9e1-271">Element</span></span> | <span data-ttu-id="ea9e1-272">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ea9e1-272">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="ea9e1-273">type</span><span class="sxs-lookup"><span data-stu-id="ea9e1-273">type</span></span> |<span data-ttu-id="ea9e1-274">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-274">Required.</span></span> <span data-ttu-id="ea9e1-275">Kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-275">The authentication type.</span></span> <span data-ttu-id="ea9e1-276">SSL istemci sertifikaları için değer olmalıdır `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-276">For SSL client certificates, the value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="ea9e1-277">password</span><span class="sxs-lookup"><span data-stu-id="ea9e1-277">password</span></span> |<span data-ttu-id="ea9e1-278">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-278">Required.</span></span> <span data-ttu-id="ea9e1-279">İstemci sertifikası (PFX dosyası) erişmek için parola</span><span class="sxs-lookup"><span data-stu-id="ea9e1-279">The password for accessing the client certificate (PFX file)</span></span> |
| <span data-ttu-id="ea9e1-280">PFX</span><span class="sxs-lookup"><span data-stu-id="ea9e1-280">pfx</span></span> |<span data-ttu-id="ea9e1-281">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-281">Required.</span></span> <span data-ttu-id="ea9e1-282">Base64 ile kodlanmış içeriği istemci sertifikasını (PFX dosyası)</span><span class="sxs-lookup"><span data-stu-id="ea9e1-282">Base64-encoded contents of the client certificate (PFX file)</span></span> |

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="ea9e1-283">Temel kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ea9e1-283">Basic authentication</span></span>

<span data-ttu-id="ea9e1-284">Web uygulaması veya API uygulaması mantıksal uygulamanızı öğesinden gelen istekleri doğrulamak için bir kullanıcı adı ve parola gibi temel kimlik doğrulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-284">To validate incoming requests from your logic app to your web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="ea9e1-285">Temel kimlik doğrulaması genel bir desen olduğundan ve web uygulaması veya API uygulaması oluşturmak için kullanılan herhangi bir dilde bu kimlik doğrulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-285">Basic authentication is a common pattern, and you can use this authentication in any language used to build your web app or API app.</span></span>

<span data-ttu-id="ea9e1-286">İçinde **yetkilendirme** bölümünde, bu satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ea9e1-286">In the **Authorization** section, include this line:</span></span>

<span data-ttu-id="ea9e1-287">`{"type": "basic", "username": "username", "password": "password"}`.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-287">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="ea9e1-288">Öğesi</span><span class="sxs-lookup"><span data-stu-id="ea9e1-288">Element</span></span> | <span data-ttu-id="ea9e1-289">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ea9e1-289">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ea9e1-290">type</span><span class="sxs-lookup"><span data-stu-id="ea9e1-290">type</span></span> |<span data-ttu-id="ea9e1-291">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-291">Required.</span></span> <span data-ttu-id="ea9e1-292">Kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-292">The authentication type.</span></span> <span data-ttu-id="ea9e1-293">Temel kimlik doğrulaması için değer olmalıdır `Basic`.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-293">For basic authentication, the value must be `Basic`.</span></span> |
| <span data-ttu-id="ea9e1-294">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="ea9e1-294">username</span></span> |<span data-ttu-id="ea9e1-295">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-295">Required.</span></span> <span data-ttu-id="ea9e1-296">Kimlik doğrulaması için kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="ea9e1-296">The username for authentication</span></span> |
| <span data-ttu-id="ea9e1-297">password</span><span class="sxs-lookup"><span data-stu-id="ea9e1-297">password</span></span> |<span data-ttu-id="ea9e1-298">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-298">Required.</span></span> <span data-ttu-id="ea9e1-299">Kimlik doğrulaması için parola</span><span class="sxs-lookup"><span data-stu-id="ea9e1-299">The password for authentication</span></span> |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="ea9e1-300">Kod aracılığıyla Azure Active Directory kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ea9e1-300">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="ea9e1-301">Varsayılan olarak, Azure portalında kapatma Azure AD kimlik doğrulaması hassas yetkilendirme sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-301">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="ea9e1-302">Örneğin, bu kimlik doğrulama API'nizi yalnızca belirli bir kiracı için değil, belirli bir kullanıcı veya uygulama kilitler.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-302">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span></span> 

<span data-ttu-id="ea9e1-303">Mantıksal uygulamanızı kodlarda için API erişimini kısıtlamak için JSON web token (JWT) sahip üstbilgi ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-303">To restrict API access to your logic app through code, extract the header that has the JSON web token (JWT).</span></span> <span data-ttu-id="ea9e1-304">Arayanın Kimliği denetleyin ve eşleşmeyen istekleri reddedecek.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-304">Check the caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="ea9e1-305">Ayrıca, bu kimlik doğrulama kendi kodunuzu tamamen uygulamak ve Azure portalını kullanma yükleneceği öğrenin nasıl [Azure uygulamanızı şirket içi Active Directory ile kimlik doğrulaması](../app-service-web/web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="ea9e1-305">Going further, to implement this authentication entirely in your own code, and not use the Azure portal, learn how to [authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>

<span data-ttu-id="ea9e1-306">Mantıksal uygulamanız için bir uygulama kimliği oluşturmak ve bu kimlik, API çağrısı için kullanmak için önceki adımları izlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="ea9e1-306">To create an application identity for your logic app and use that identity to call your API, you must follow the previous steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea9e1-307">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ea9e1-307">Next steps</span></span>

* [<span data-ttu-id="ea9e1-308">Tanılama günlükleri ve Uyarıları ile mantığı uygulama performansını kontrol etme</span><span class="sxs-lookup"><span data-stu-id="ea9e1-308">Check logic app performance with diagnostic logs and alerts</span></span>](logic-apps-monitor-your-logic-apps.md)