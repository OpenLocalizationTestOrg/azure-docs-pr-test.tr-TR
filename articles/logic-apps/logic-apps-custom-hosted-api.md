---
title: "aaaDeploy, çağrı ve web API'leri ve REST API'leri Azure Logic Apps için kimlik doğrulaması | Microsoft Docs"
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
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a><span data-ttu-id="d7020-104">Dağıtımı, arama ve özel API'leri olarak bağlayıcılar mantıksal uygulamalar için kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d7020-104">Deploy, call, and authenticate custom APIs as connectors for logic apps</span></span>

<span data-ttu-id="d7020-105">Çalıştırdıktan sonra [özel API oluşturma](./logic-apps-create-api-app.md) uygulamalar iş mantığı eylemler veya tetikleyicileri toouse sağlamak için bunları çağırmadan önce Apı'lerinizi dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7020-105">After you [create custom APIs](./logic-apps-create-api-app.md) that provide actions or triggers toouse in logic apps workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="d7020-106">Hello iyi deneyim için herhangi bir API'yi mantığı uygulamadan çağırıp rağmen ekleyin [Swagger meta verileri](http://swagger.io/specification/) , API'nin işlemlerini ve parametrelerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="d7020-106">And although you can call any API from a logic app, for hello best experience, add [Swagger metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="d7020-107">Bu Swagger dosyası API'nizi daha iyi ve daha kolay logic apps ile tümleştirmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d7020-107">This Swagger file helps your API work better and integrate more easily with logic apps.</span></span>

<span data-ttu-id="d7020-108">API olarak dağıtabilir miyim [web uygulamaları](../app-service-web/app-service-web-overview.md), ancak API olarak dağıtmayı göz önünde bulundurun [API uygulamaları](../app-service-api/app-service-api-apps-why-best-platform.md), hangi yapabilir, işinizi daha kolay yapı, ana bilgisayar ve API'ler hello bulutta ve şirket içi kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="d7020-108">You can deploy your APIs as [web apps](../app-service-web/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service-api/app-service-api-apps-why-best-platform.md), which can make your job easier when you build, host, and consume APIs in hello cloud and on premises.</span></span> <span data-ttu-id="d7020-109">Herhangi bir kod Apı'leriniz toochange yok--yalnızca kod tooan API uygulamanızı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d7020-109">You don't have toochange any code in your APIs -- just deploy your code tooan API app.</span></span> <span data-ttu-id="d7020-110">Üzerinde Apı'lerinizi barındırabilir [Azure App Service](../app-service/app-service-value-prop-what-is.md), bir platform olarak-sağlayan hello en iyi, kolay ve en ölçeklenebilir yollarından biri, API barındırmak için sunan hizmet (PaaS).</span><span class="sxs-lookup"><span data-stu-id="d7020-110">You can host your APIs on [Azure App Service](../app-service/app-service-value-prop-what-is.md), a platform-as-a-service (PaaS) offering that provides one of hello best, easiest, and most scalable ways for API hosting.</span></span>

<span data-ttu-id="d7020-111">logic apps tooyour API'leri çağrılarından tooauthenticate, kodunuzu tooupdate aktarıp Azure portal hello Azure Active Directory'yi ayarlama ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7020-111">tooauthenticate calls from logic apps tooyour APIs, you can set up Azure Active Directory in hello Azure portal so you don't have tooupdate your code.</span></span> <span data-ttu-id="d7020-112">Veya gerektirir ve kimlik doğrulama, API'nin kodlarda zorlayın.</span><span class="sxs-lookup"><span data-stu-id="d7020-112">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="d7020-113">API'nizi bir web uygulaması veya API uygulaması olarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="d7020-113">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="d7020-114">Özel API'nizi mantığı uygulamadan aramadan önce API'nizi bir web uygulaması veya API uygulaması tooAzure uygulama hizmeti olarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d7020-114">Before you can call your custom API from a logic app, deploy your API as a web app or API app tooAzure App Service.</span></span> <span data-ttu-id="d7020-115">Ayrıca, toomake Swagger belgenizi hello mantığı Uygulama Tasarımcısı tarafından okunabilir hello API tanımı özelliklerini ayarlama ve Aç [çıkış noktaları arası kaynak paylaşımı (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) web uygulaması veya API uygulaması için.</span><span class="sxs-lookup"><span data-stu-id="d7020-115">Also, toomake your Swagger document readable by hello Logic App Designer, set hello API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) for your web app or API app.</span></span>

1. <span data-ttu-id="d7020-116">Hello Azure portal, web uygulaması veya API uygulaması seçin.</span><span class="sxs-lookup"><span data-stu-id="d7020-116">In hello Azure portal, select your web app or API app.</span></span>

2. <span data-ttu-id="d7020-117">Açılır ve altında hello dikey penceresinde **API**, seçin **API tanımı**.</span><span class="sxs-lookup"><span data-stu-id="d7020-117">In hello blade that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="d7020-118">Set hello **API tanımı konumu** swagger.json dosyanız için toohello URL.</span><span class="sxs-lookup"><span data-stu-id="d7020-118">Set hello **API definition location** toohello URL for your swagger.json file.</span></span>

   <span data-ttu-id="d7020-119">Genellikle, hello URL şöyle görünür:`https://{name}.azurewebsites.net/swagger/docs/v1)`</span><span class="sxs-lookup"><span data-stu-id="d7020-119">Usually, hello URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![Özel API'nizi için bağlantı tooSwagger dosyası](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. <span data-ttu-id="d7020-121">Altında **API**, seçin **CORS**.</span><span class="sxs-lookup"><span data-stu-id="d7020-121">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="d7020-122">Ayarlamak için hello CORS İlkesi **çıkış izin** çok**'*'** (tüm izin ver).</span><span class="sxs-lookup"><span data-stu-id="d7020-122">Set hello CORS policy for **Allowed origins** too**'*'** (allow all).</span></span>

   <span data-ttu-id="d7020-123">Bu ayar mantığı Uygulama Tasarımcısı'ndan istekleri verir.</span><span class="sxs-lookup"><span data-stu-id="d7020-123">This setting permits requests from Logic App Designer.</span></span>

   ![Mantıksal Uygulama Tasarımcısı tooyour özel API'SİNDEN isteklere izin vermek](media/logic-apps-custom-hosted-api/custom-api-cors.png)

<span data-ttu-id="d7020-125">Daha fazla bilgi için bu makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="d7020-125">For more information, see these articles:</span></span>

* [<span data-ttu-id="d7020-126">ASP.NET web API için Swagger meta verileri ekleme</span><span class="sxs-lookup"><span data-stu-id="d7020-126">Add Swagger metadata for ASP.NET web APIs</span></span>](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [<span data-ttu-id="d7020-127">ASP.NET web API tooAzure uygulama hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="d7020-127">Deploy ASP.NET web APIs tooAzure App Service</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="d7020-128">Özel API'nizi mantığından uygulama iş akışları çağırın.</span><span class="sxs-lookup"><span data-stu-id="d7020-128">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="d7020-129">Merhaba API tanımı özellikleri ve CORS ayarladıktan sonra özel API'nin tetikleyiciler ve Eylemler, tooinclude iş akışınızda mantığı uygulama için kullanılabilir duruma gelir.</span><span class="sxs-lookup"><span data-stu-id="d7020-129">After you set up hello API definition properties and CORS, your custom API's triggers and actions should become available for you tooinclude in your logic app workflow.</span></span> 

*  <span data-ttu-id="d7020-130">Swagger URL'leri sahip tooview hello Web siteleri, abonelik sitelerinizi hello Logic Apps Tasarımcısı göz atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7020-130">tooview hello websites that have Swagger URLs, you can browse your subscription websites in hello Logic Apps Designer.</span></span>

*  <span data-ttu-id="d7020-131">tooview kullanılabilir eylemler ve Swagger belgesinin üzerine gelerek girişleri kullanın hello [HTTP + Swagger eylem](../connectors/connectors-native-http-swagger.md).</span><span class="sxs-lookup"><span data-stu-id="d7020-131">tooview available actions and inputs by pointing at a Swagger document, use hello [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="d7020-132">toocall yok veya bir Swagger belgesinin kullanıma API'leri dahil olmak üzere herhangi bir API'yi hello ile her zaman bir istek oluşturabilirsiniz [HTTP eylemi](../connectors/connectors-native-http.md).</span><span class="sxs-lookup"><span data-stu-id="d7020-132">toocall any API, including APIs that don't have or expose a Swagger document, you can always create a request with hello [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="authenticate-calls-tooyour-custom-api"></a><span data-ttu-id="d7020-133">Çağrıları tooyour özel API kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d7020-133">Authenticate calls tooyour custom API</span></span>

<span data-ttu-id="d7020-134">Bu yolla tooyour özel API çağrıları güvenliğini sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d7020-134">You can secure calls tooyour custom API in these ways:</span></span>

* <span data-ttu-id="d7020-135">[Kod değişiklikleri](#no-code): API'nizi ile koruma [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) hello Azure portal, bu nedenle yok tooupdate kodunuz varsa veya API'nizi yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d7020-135">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) through hello Azure portal, so you don't have tooupdate your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d7020-136">Varsayılan olarak, hassas yetkilendirme hello Azure portal kapatma hello Azure AD kimlik doğrulaması sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="d7020-136">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="d7020-137">Örneğin, bu kimlik doğrulama belirli Kiracı, tooa belirli kullanıcı veya uygulama, API toojust kilitler.</span><span class="sxs-lookup"><span data-stu-id="d7020-137">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

* <span data-ttu-id="d7020-138">[API kodunu güncelleştirin](#update-code): zorlayarak API'nizi koruma [sertifika kimlik doğrulaması](#certificate), [temel kimlik doğrulaması](#basic), veya [Azure AD kimlik doğrulaması](#azure-ad-code) kodlarda.</span><span class="sxs-lookup"><span data-stu-id="d7020-138">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a><span data-ttu-id="d7020-139">Çağrıları tooyour API kodunu değiştirmeden kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d7020-139">Authenticate calls tooyour API without changing code</span></span>

<span data-ttu-id="d7020-140">Bu yöntemin hello genel adımlar aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="d7020-140">Here's hello general steps for this method:</span></span>

1. <span data-ttu-id="d7020-141">İki oluşturmak [Azure Active Directory (Azure AD) uygulama kimlikleri](../app-service-api/app-service-api-dotnet-service-principal-auth.md): mantıksal uygulamanızı, diğeri web uygulaması (veya API uygulaması) için.</span><span class="sxs-lookup"><span data-stu-id="d7020-141">Create two [Azure Active Directory (Azure AD) application identities](../app-service-api/app-service-api-dotnet-service-principal-auth.md): one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="d7020-142">tooauthenticate çağrıları tooyour API'sini kullanın hello kimlik bilgileri (istemci kimliği ve parolası) Merhaba [hizmet asıl](../app-service-api/app-service-api-dotnet-service-principal-auth.md) mantıksal uygulamanız için Azure AD uygulama kimliği ile Merhaba ilişkili.</span><span class="sxs-lookup"><span data-stu-id="d7020-142">tooauthenticate calls tooyour API, use hello credentials (client ID and secret) for hello [service principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) that's associated with hello Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="d7020-143">Merhaba uygulama kimlikleri mantığı uygulama tanımınızı içerir.</span><span class="sxs-lookup"><span data-stu-id="d7020-143">Include hello application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="d7020-144">1. Kısım: mantıksal uygulamanız için bir Azure AD uygulama kimliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7020-144">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="d7020-145">Mantıksal uygulamanız bu Azure AD uygulama kimliği tooauthenticate Azure ad kullanır.</span><span class="sxs-lookup"><span data-stu-id="d7020-145">Your logic app uses this Azure AD application identity tooauthenticate against Azure AD.</span></span> <span data-ttu-id="d7020-146">Bu kimlik yukarı tooset dizininiz için bir kez yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="d7020-146">You only have tooset up this identity one time for your directory.</span></span> <span data-ttu-id="d7020-147">Örneğin, seçebileceğiniz toouse Merhaba, mantığı uygulamalarınız için aynı kimlik rağmen her mantıksal uygulama için benzersiz kimlik oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7020-147">For example, you can choose toouse hello same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="d7020-148">Hello Azure portal'ın bu kimlikleri ayarlayabilirsiniz [Klasik Azure portalı](#app-identity-logic-classic), veya [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="d7020-148">You can set up these identities in hello Azure portal, [Azure classic portal](#app-identity-logic-classic), or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="d7020-149">**Mantıksal uygulamanız için Hello uygulama kimliği hello Azure portal oluşturma**</span><span class="sxs-lookup"><span data-stu-id="d7020-149">**Create hello application identity for your logic app in hello Azure portal**</span></span>

1. <span data-ttu-id="d7020-150">Merhaba, [Azure portal](https://portal.azure.com "https://portal.azure.com"), seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d7020-150">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="d7020-151">Hello olduğunu onaylamak için web uygulaması veya API uygulaması ile aynı dizinde.</span><span class="sxs-lookup"><span data-stu-id="d7020-151">Confirm that you're in hello same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="d7020-152">tooswitch dizinler profilinizi tıklatın ve başka bir dizin seçin.</span><span class="sxs-lookup"><span data-stu-id="d7020-152">tooswitch directories, click your profile and select another directory.</span></span> <span data-ttu-id="d7020-153">Ya da seçin **genel bakış** > **anahtar dizini**.</span><span class="sxs-lookup"><span data-stu-id="d7020-153">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="d7020-154">Merhaba dizin menüsünde altında **Yönet**, seçin **uygulama kayıtlar** > **yeni uygulama kaydı**.</span><span class="sxs-lookup"><span data-stu-id="d7020-154">On hello directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="d7020-155">Varsayılan olarak, dizininizde tüm uygulama kayıtları hello uygulama kayıtlar listesi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="d7020-155">By default, hello app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="d7020-156">yalnızca, uygulama kayıtlar, sonraki toohello arama kutusunda, tooview seçin **uygulamalarım**.</span><span class="sxs-lookup"><span data-stu-id="d7020-156">tooview only your app registrations, next toohello search box, select **My apps**.</span></span> 

   ![Yeni uygulama kaydı oluşturun](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. <span data-ttu-id="d7020-158">Uygulama kimliğinizi bir ad verin, bırakın **uygulama türü** çok ayarlamak**Web uygulaması / API**, benzersiz bir sağlamak için bir etki alanı olarak biçimlendirilmiş dize **oturum açma URL'si**ve seçin **Oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="d7020-158">Give your application identity a name, leave **Application type** set too**Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![URL için uygulama kimliği oturum adı girin ve](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   <span data-ttu-id="d7020-160">mantıksal uygulamanız artık oluşturulan hello uygulama kimliği hello uygulama kayıtlar listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d7020-160">hello application identity that you created for your logic app now appears in hello app registrations list.</span></span>

   ![Mantıksal uygulamanız için uygulama kimliği](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. <span data-ttu-id="d7020-162">Merhaba uygulama kayıtlar listesinde, yeni uygulama kimliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="d7020-162">In hello app registrations list, select your new application identity.</span></span> <span data-ttu-id="d7020-163">Kopyalayın ve hello kaydedin **uygulama kimliği** mantıksal uygulamanızı bölümü 3'te "istemci kimliği" Merhaba gibi toouse.</span><span class="sxs-lookup"><span data-stu-id="d7020-163">Copy and save hello **Application ID** toouse as hello "client ID" for your logic app in Part 3.</span></span>

   ![Kopyalayın ve mantıksal uygulama için uygulama kimliği kaydedin](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. <span data-ttu-id="d7020-165">Uygulama Kimliği ayarlarınızı görünür durumda değilse, seçin **ayarları** veya **tüm ayarları**.</span><span class="sxs-lookup"><span data-stu-id="d7020-165">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="d7020-166">Altında **API erişimini**, seçin **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="d7020-166">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="d7020-167">Altında **açıklama**, anahtarınız için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="d7020-167">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="d7020-168">Altında **Expires**, anahtarınız için bir süre seçin.</span><span class="sxs-lookup"><span data-stu-id="d7020-168">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="d7020-169">Oluşturmakta olduğunuz hello anahtar hello uygulama kimliğin "gizli" veya parolasını mantıksal uygulamanızı olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="d7020-169">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

   ![Mantıksal uygulama kimliği için anahtar oluşturma](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="d7020-171">Merhaba araç çubuğunda seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d7020-171">On hello toolbar, choose **Save**.</span></span> <span data-ttu-id="d7020-172">Altında **değeri**, anahtarınızı artık görünür.</span><span class="sxs-lookup"><span data-stu-id="d7020-172">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="d7020-173">**Toocopy emin olun ve anahtarınızı kaydedin** daha sonra kullanmak üzere hello anahtarı gizli olduğu çıktığınızda hello anahtar dikey.</span><span class="sxs-lookup"><span data-stu-id="d7020-173">**Make sure toocopy and save your key** for later use because hello key is hidden when you leave hello key blade.</span></span>

   <span data-ttu-id="d7020-174">Mantıksal uygulamanızı bölümü 3'te yapılandırdığınızda, "gizli" ya da parola hello gibi bu anahtarı belirtin.</span><span class="sxs-lookup"><span data-stu-id="d7020-174">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

   ![Kopyalayın ve anahtarı için daha sonra kaydedin](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

<span data-ttu-id="d7020-176">**Merhaba Klasik Azure portalı mantıksal uygulamanızı için Hello uygulama kimliği oluşturma**</span><span class="sxs-lookup"><span data-stu-id="d7020-176">**Create hello application identity for your logic app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="d7020-177">Buna Klasik Azure portalı Merhaba, seçin [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="d7020-177">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2. <span data-ttu-id="d7020-178">Web uygulaması veya API uygulaması için kullandığınız aynı dizinde seçin hello.</span><span class="sxs-lookup"><span data-stu-id="d7020-178">Select hello same directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="d7020-179">Merhaba üzerinde **uygulamaları** sekmesinde, seçin **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="d7020-179">On hello **Applications** tab, choose **Add** at hello bottom of hello page.</span></span>

4. <span data-ttu-id="d7020-180">Uygulama kimliğinizi bir ad verin ve seçin **sonraki** (sağ ok).</span><span class="sxs-lookup"><span data-stu-id="d7020-180">Give your application identity a name, and choose **Next** (right arrow).</span></span>

5. <span data-ttu-id="d7020-181">Altında **uygulama özellikleri**, benzersiz bir sağlamak için bir etki alanı olarak biçimlendirilmiş dize **oturum açma URL'si** ve **uygulama kimliği URI'si**ve seçin **tam** (onay işareti).</span><span class="sxs-lookup"><span data-stu-id="d7020-181">Under **App properties**, provide a unique string formatted as a domain for **Sign-on URL** and **App ID URI**, and choose **Complete** (checkmark).</span></span>

6. <span data-ttu-id="d7020-182">Merhaba üzerinde **yapılandırma** sekmesinde, kopyalamak ve hello kaydetme **istemci kimliği** bölümü 3'te, logic app toouse için.</span><span class="sxs-lookup"><span data-stu-id="d7020-182">On hello **Configure** tab, copy and save hello **Client ID** for your logic app toouse in Part 3.</span></span>

7. <span data-ttu-id="d7020-183">Altında **anahtarları**açın hello **seçin süresi** listesi.</span><span class="sxs-lookup"><span data-stu-id="d7020-183">Under **Keys**, open hello **Select duration** list.</span></span> <span data-ttu-id="d7020-184">Anahtarınız için bir süre seçin.</span><span class="sxs-lookup"><span data-stu-id="d7020-184">Select a duration for your key.</span></span>

   <span data-ttu-id="d7020-185">Oluşturmakta olduğunuz hello anahtar hello uygulama kimliğin "gizli" veya parolasını mantıksal uygulamanızı olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="d7020-185">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

8. <span data-ttu-id="d7020-186">Merhaba sayfasının Hello altında seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d7020-186">At hello bottom of hello page, choose **Save**.</span></span> <span data-ttu-id="d7020-187">Birkaç saniye toowait olabilir.</span><span class="sxs-lookup"><span data-stu-id="d7020-187">You might have toowait a few seconds.</span></span>

9. <span data-ttu-id="d7020-188">Altında **anahtarları**toocopy emin olun ve artık görünür hello anahtarı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d7020-188">Under **Keys**, make sure toocopy and save hello key that now appears.</span></span> 

   <span data-ttu-id="d7020-189">Mantıksal uygulamanızı bölümü 3'te yapılandırdığınızda, "gizli" ya da parola hello gibi bu anahtarı belirtin.</span><span class="sxs-lookup"><span data-stu-id="d7020-189">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

<span data-ttu-id="d7020-190">Daha fazla bilgi için nasıl çok öğrenin [App Service uygulama toouse Azure Active Directory oturum açma yapılandırma](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d7020-190">For more information, learn how too [configure your App Service application toouse Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

<a name="powershell"></a>

<span data-ttu-id="d7020-191">**PowerShell'de mantıksal uygulamanızı için Hello uygulama kimliği oluşturma**</span><span class="sxs-lookup"><span data-stu-id="d7020-191">**Create hello application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="d7020-192">Bu görevi PowerShell ile Azure Resource Manager aracılığıyla gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7020-192">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="d7020-193">PowerShell'de aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d7020-193">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="d7020-194">Toocopy hello emin olun **Kiracı kimliği** (GUID) Azure AD kiracınız için hello **uygulama kimliği**ve kullandığınız hello parola.</span><span class="sxs-lookup"><span data-stu-id="d7020-194">Make sure toocopy hello **Tenant ID** (GUID for your Azure AD tenant), hello **Application ID**, and hello password that you used.</span></span>

<span data-ttu-id="d7020-195">Daha fazla bilgi için nasıl çok öğrenin [PowerShell tooaccess kaynaklarla bir hizmet sorumlusu oluşturma](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="d7020-195">For more information, learn how too [create a service principal with PowerShell tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="d7020-196">Bölüm 2: web uygulaması veya API uygulaması için bir Azure AD uygulama kimliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7020-196">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="d7020-197">Web uygulaması veya API uygulama zaten dağıtılmışsa, kimlik doğrulamasını etkinleştirmek ve hello Azure portal hello uygulama kimliği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d7020-197">If your web app or API app is already deployed, you can turn on authentication and create hello application identity in hello Azure portal.</span></span> <span data-ttu-id="d7020-198">Aksi takdirde, şunları yapabilirsiniz [bir Azure Resource Manager şablonu ile dağıtırken kimlik doğrulamasını etkinleştirmek](#authen-deploy).</span><span class="sxs-lookup"><span data-stu-id="d7020-198">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="d7020-199">**Hello uygulama kimliği oluşturma ve kimlik doğrulaması hello dağıtılan uygulamalar için Azure Portalı'nda Aç**</span><span class="sxs-lookup"><span data-stu-id="d7020-199">**Create hello application identity and turn on authentication in hello Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="d7020-200">Merhaba, [Azure portal](https://portal.azure.com "https://portal.azure.com"), bulma ve web uygulaması veya API uygulaması seçin.</span><span class="sxs-lookup"><span data-stu-id="d7020-200">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="d7020-201">Altında **ayarları**, seçin **kimlik doğrulama/yetkilendirme**.</span><span class="sxs-lookup"><span data-stu-id="d7020-201">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="d7020-202">Altında **App Service kimlik doğrulaması**, kimlik doğrulamasını **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="d7020-202">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="d7020-203">Altında **kimlik doğrulama sağlayıcıları**, seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d7020-203">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![Kimlik doğrulamasını etkinleştirmek](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. <span data-ttu-id="d7020-205">Artık web uygulaması veya API uygulaması için uygulama kimliği, aşağıda gösterildiği gibi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d7020-205">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="d7020-206">Merhaba üzerinde **Azure Active Directory ayarları** dikey penceresinde ayarlamak **yönetim modu** çok**Express**.</span><span class="sxs-lookup"><span data-stu-id="d7020-206">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Express**.</span></span> <span data-ttu-id="d7020-207">Seçin **yeni AD uygulaması oluştur**.</span><span class="sxs-lookup"><span data-stu-id="d7020-207">Choose **Create New AD App**.</span></span> <span data-ttu-id="d7020-208">Uygulama kimliğinizi bir ad verin ve seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="d7020-208">Give your application identity a name, and choose **OK**.</span></span> 

   ![Web uygulaması veya API uygulaması için uygulama kimliği oluşturma](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. <span data-ttu-id="d7020-210">Merhaba üzerinde **kimlik doğrulama / yetkilendirme dikey**, seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d7020-210">On hello **Authentication / Authorization blade**, choose **Save**.</span></span>

<span data-ttu-id="d7020-211">Şimdi hello istemci Kimliğini bulun ve web uygulaması veya API uygulaması ile ilişkili hello uygulama kimliği için kimlik Kiracı.</span><span class="sxs-lookup"><span data-stu-id="d7020-211">Now you must find hello client ID and tenant ID for hello application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="d7020-212">Bu kimlikleri bölümü 3'te kullanın.</span><span class="sxs-lookup"><span data-stu-id="d7020-212">You use these IDs in Part 3.</span></span> <span data-ttu-id="d7020-213">Bu nedenle hello Azure portal için aşağıdaki adımları devam veya [Klasik Azure portalı](#find-id-classic).</span><span class="sxs-lookup"><span data-stu-id="d7020-213">So continue with these steps for hello Azure portal or [Azure classic portal](#find-id-classic).</span></span>

<span data-ttu-id="d7020-214">**Uygulama Kimliği'nin istemci Kimliğini bulmak ve web uygulaması veya hello Azure portalında bir API uygulaması için kimliği Kiracı**</span><span class="sxs-lookup"><span data-stu-id="d7020-214">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure portal**</span></span>

1. <span data-ttu-id="d7020-215">Altında **kimlik doğrulama sağlayıcıları**, seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d7020-215">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   !["Azure Active Directory" seçin](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="d7020-217">Merhaba üzerinde **Azure Active Directory ayarları** dikey penceresinde ayarlamak **yönetim modu** çok**Gelişmiş**.</span><span class="sxs-lookup"><span data-stu-id="d7020-217">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Advanced**.</span></span>

3. <span data-ttu-id="d7020-218">Kopya hello **istemci kimliği**ve bölüm 3'te kullanmak için bu GUID'i kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d7020-218">Copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="d7020-219">Varsa **istemci kimliği** ve **veren URL'si** yoksa görünür hello Azure portal'ı yenilemeyi deneyin ve 1. adım yineleyin.</span><span class="sxs-lookup"><span data-stu-id="d7020-219">If **Client ID** and **Issuer Url** don't appear, try refreshing hello Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="d7020-220">Altında **veren URL'si**, kopyalama ve kaydetme yalnızca GUID için bölümü 3 hello.</span><span class="sxs-lookup"><span data-stu-id="d7020-220">Under **Issuer Url**, copy and save just hello GUID for Part 3.</span></span> <span data-ttu-id="d7020-221">Aynı zamanda bu GUID web uygulamanızı veya API uygulamasının dağıtım şablonu, gerekirse kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7020-221">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="d7020-222">Bu GUID belirli kiracının GUID ("Kiracı kimliği") ve bu URL'de görünmelidir:`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="d7020-222">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="d7020-223">Değişikliklerinizi kaydetmeden kapatın hello **Azure Active Directory ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="d7020-223">Without saving your changes, close hello **Azure Active Directory Settings** blade.</span></span>

<a name="find-id-classic"></a>

<span data-ttu-id="d7020-224">**Uygulama Kimliği'nin istemci Kimliğini bulmak ve web uygulaması veya hello Klasik Azure portalında bir API uygulaması için kimliği Kiracı**</span><span class="sxs-lookup"><span data-stu-id="d7020-224">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="d7020-225">Buna Klasik Azure portalı Merhaba, seçin [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="d7020-225">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2.  <span data-ttu-id="d7020-226">Web uygulaması veya API uygulaması için kullandığınız hello dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="d7020-226">Select hello directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="d7020-227">Merhaba, **arama** kutusunda bulmak ve web uygulaması veya API uygulaması için hello uygulama kimliği seçin.</span><span class="sxs-lookup"><span data-stu-id="d7020-227">In hello **Search** box, find and select hello application identity for your web app or API app.</span></span>

4. <span data-ttu-id="d7020-228">Merhaba üzerinde **yapılandırma** sekmesi, kopyalama hello **istemci kimliği**ve bölüm 3'te kullanmak için bu GUID'i kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d7020-228">On hello **Configure** tab, copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

5. <span data-ttu-id="d7020-229">Merhaba hello sonundaki hello istemci kimliği aldıktan sonra **yapılandırma** sekmesinde, seçin **uç noktaları görüntülemek**.</span><span class="sxs-lookup"><span data-stu-id="d7020-229">After you get hello client ID, at hello bottom of hello **Configure** tab, choose **View endpoints**.</span></span>

6. <span data-ttu-id="d7020-230">Merhaba URL'sini kopyalayın **Federasyon meta veri belgesi**ve toothat URL'ye gidin.</span><span class="sxs-lookup"><span data-stu-id="d7020-230">Copy hello URL for **Federation Metadata Document**, and browse toothat URL.</span></span>

7. <span data-ttu-id="d7020-231">Açılan hello meta veri belgesinde hello kök Bul **EntityDescriptor kimliği** sahip öğesi bir **Entityıd** özniteliği bu formda:`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="d7020-231">In hello metadata document that opens, find hello root **EntityDescriptor ID** element, which has an **entityID** attribute in this form: `https://sts.windows.net/{GUID}`</span></span> 

      <span data-ttu-id="d7020-232">Bu öznitelik Hello GUID belirli kiracının (Kiracı kimliği) olarak GUID'dir.</span><span class="sxs-lookup"><span data-stu-id="d7020-232">hello GUID in this attribute is your specific tenant's GUID (tenant ID).</span></span>

8. <span data-ttu-id="d7020-233">Merhaba Kiracı kimliği kopyalayın ve gerekirse bölümü 3 ve ayrıca toouse web uygulamanızı veya API uygulamasının dağıtım şablonu kullanmak için bu kimliği kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d7020-233">Copy hello tenant ID and save that ID for use in Part 3, and also toouse in your web app or API app's deployment template, if necessary.</span></span>

<span data-ttu-id="d7020-234">Daha fazla bilgi için şu konulara bakın:</span><span class="sxs-lookup"><span data-stu-id="d7020-234">For more information, see these topics:</span></span>

* [<span data-ttu-id="d7020-235">Azure uygulama hizmetinde API uygulamaları için kullanıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d7020-235">User authentication for API apps in Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [<span data-ttu-id="d7020-236">Kimlik doğrulama ve yetkilendirme Azure uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="d7020-236">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

<span data-ttu-id="d7020-237">**Bir Azure Resource Manager şablonu ile dağıtırken kimlik doğrulamasını etkinleştirmek**</span><span class="sxs-lookup"><span data-stu-id="d7020-237">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="d7020-238">Hala mantığı uygulamanız için hello uygulama kimlikten web uygulaması veya farklı bir API uygulaması için bir Azure AD uygulama kimliği da oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7020-238">You must still create an Azure AD application identity for your web app or API app that differs from hello app identity for your logic app.</span></span> <span data-ttu-id="d7020-239">toocreate hello uygulama kimliği, önceki izleyin hello Kısım 2'de Azure portal hello için adımları.</span><span class="sxs-lookup"><span data-stu-id="d7020-239">toocreate hello application identity, follow hello previous steps in Part 2 for hello Azure portal.</span></span> <span data-ttu-id="d7020-240">Ayrıca, 1. Bölüm hello adımları ancak web uygulamanızı veya API uygulamasının gerçek emin toouse olun `https://{URL}` için **oturum açma URL'si** ve **uygulama kimliği URI'si**.</span><span class="sxs-lookup"><span data-stu-id="d7020-240">You can also follow hello steps in Part 1, but make sure toouse your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="d7020-241">Bu adımları, hem de hello istemci kimliği ve Kiracı kimliği, uygulamanızın dağıtım şablonu kullanmak için ve ayrıca bölümü 3 toosave sahip.</span><span class="sxs-lookup"><span data-stu-id="d7020-241">From these steps, you have toosave both hello client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="d7020-242">Web uygulaması veya API uygulaması için hello Azure AD uygulama kimliği oluşturduğunuzda, PowerShell yazmak yerine hello Azure portalında veya Klasik Azure portalını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7020-242">When you create hello Azure AD application identity for your web app or API app, you must use hello Azure portal or Azure classic portal, rather than PowerShell.</span></span> <span data-ttu-id="d7020-243">Merhaba PowerShell komutunu gerekli hello izinlerini toosign kullanıcılar bir Web sitesi olarak ayarlamaz.</span><span class="sxs-lookup"><span data-stu-id="d7020-243">hello PowerShell commandlet doesn't set up hello required permissions toosign users into a website.</span></span>

<span data-ttu-id="d7020-244">Merhaba istemci kimliği ve Kiracı kimliği aldıktan sonra bu kimlikleri subresource web uygulaması veya API uygulaması için dağıtım şablonunda olarak şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d7020-244">After you get hello client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

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

<span data-ttu-id="d7020-245">tooautomatically dağıtmak boş web uygulaması ve bir mantıksal uygulama Azure Active Directory kimlik doğrulaması, birlikte [hello tam şablonu görüntüleme burada](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), veya **tooAzure dağıtmak** burada:</span><span class="sxs-lookup"><span data-stu-id="d7020-245">tooautomatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view hello complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy tooAzure** here:</span></span>

<span data-ttu-id="d7020-246">[![TooAzure dağıtma](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="d7020-246">[![Deploy tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a><span data-ttu-id="d7020-247">3. Kısım: hello yetkilendirme mantıksal uygulamanızı bölümünde doldurma</span><span class="sxs-lookup"><span data-stu-id="d7020-247">Part 3: Populate hello Authorization section in your logic app</span></span>

<span data-ttu-id="d7020-248">Merhaba önceki şablonu zaten bu yetkilendirmesi bölümünde ayarladığınız sahip, ancak doğrudan hello mantıksal uygulama yazıyorsanız, hello tam yetkilendirme bölümü içermelidir.</span><span class="sxs-lookup"><span data-stu-id="d7020-248">hello previous template already has this authorization section set up, but if you are directly authoring hello logic app, you must include hello full authorization section.</span></span>

<span data-ttu-id="d7020-249">Kod görünümünde gidin toohello mantıksal uygulama tanımını açın **HTTP** eylem bölümü, Bul hello **yetkilendirme** bölümünde ve bu satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d7020-249">Open your logic app definition in code view, go toohello **HTTP** action section, find hello **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="d7020-250">Öğesi</span><span class="sxs-lookup"><span data-stu-id="d7020-250">Element</span></span> | <span data-ttu-id="d7020-251">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d7020-251">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="d7020-252">Kiracı</span><span class="sxs-lookup"><span data-stu-id="d7020-252">tenant</span></span> |<span data-ttu-id="d7020-253">Merhaba GUID hello Azure AD kiracısı</span><span class="sxs-lookup"><span data-stu-id="d7020-253">hello GUID for hello Azure AD tenant</span></span> |
| <span data-ttu-id="d7020-254">Hedef kitle</span><span class="sxs-lookup"><span data-stu-id="d7020-254">audience</span></span> |<span data-ttu-id="d7020-255">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d7020-255">Required.</span></span> <span data-ttu-id="d7020-256">Merhaba GUID tooaccess - hello istemci web uygulaması veya API uygulaması için uygulama kimliği hello Kimliğinden istediğiniz hello hedef kaynak için</span><span class="sxs-lookup"><span data-stu-id="d7020-256">hello GUID for hello target resource that you want tooaccess - hello client ID from hello application identity for your web app or API app</span></span> |
| <span data-ttu-id="d7020-257">istemci kimliği</span><span class="sxs-lookup"><span data-stu-id="d7020-257">clientId</span></span> |<span data-ttu-id="d7020-258">access - mantıksal uygulamanızı için hello uygulama kimliği hello istemci kimliği isteyen hello istemci Merhaba GUID</span><span class="sxs-lookup"><span data-stu-id="d7020-258">hello GUID for hello client requesting access - hello client ID from hello application identity for your logic app</span></span> |
| <span data-ttu-id="d7020-259">Gizli</span><span class="sxs-lookup"><span data-stu-id="d7020-259">secret</span></span> |<span data-ttu-id="d7020-260">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d7020-260">Required.</span></span> <span data-ttu-id="d7020-261">Merhaba anahtarı veya parolayı hello uygulama kimliği hello erişim belirteci isteyen hello istemci için gelen</span><span class="sxs-lookup"><span data-stu-id="d7020-261">hello key or password from hello application identity for hello client that's requesting hello access token</span></span> |
| <span data-ttu-id="d7020-262">type</span><span class="sxs-lookup"><span data-stu-id="d7020-262">type</span></span> |<span data-ttu-id="d7020-263">Merhaba kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="d7020-263">hello authentication type.</span></span> <span data-ttu-id="d7020-264">ActiveDirectoryOAuth kimlik doğrulaması için hello değerdir `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="d7020-264">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |

<span data-ttu-id="d7020-265">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d7020-265">For example:</span></span>

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

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="d7020-266">Kod aracılığıyla güvenli API çağrıları</span><span class="sxs-lookup"><span data-stu-id="d7020-266">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="d7020-267">Sertifika kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d7020-267">Certificate authentication</span></span>

<span data-ttu-id="d7020-268">mantıksal uygulama tooyour web uygulaması veya API uygulaması toovalidate hello gelen istekleri, istemci sertifikaları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7020-268">toovalidate hello incoming requests from your logic app tooyour web app or API app, you can use client certificates.</span></span> <span data-ttu-id="d7020-269">kodunuzu, tooset öğrenin [nasıl tooconfigure TLS karşılıklı kimlik doğrulaması](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span><span class="sxs-lookup"><span data-stu-id="d7020-269">tooset up your code, learn [how tooconfigure TLS mutual authentication](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="d7020-270">Merhaba, **yetkilendirme** bölümünde, bu satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d7020-270">In hello **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="d7020-271">Öğesi</span><span class="sxs-lookup"><span data-stu-id="d7020-271">Element</span></span> | <span data-ttu-id="d7020-272">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d7020-272">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="d7020-273">type</span><span class="sxs-lookup"><span data-stu-id="d7020-273">type</span></span> |<span data-ttu-id="d7020-274">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d7020-274">Required.</span></span> <span data-ttu-id="d7020-275">Merhaba kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="d7020-275">hello authentication type.</span></span> <span data-ttu-id="d7020-276">SSL istemci sertifikaları için başlangıç değeri olmalıdır `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="d7020-276">For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="d7020-277">password</span><span class="sxs-lookup"><span data-stu-id="d7020-277">password</span></span> |<span data-ttu-id="d7020-278">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d7020-278">Required.</span></span> <span data-ttu-id="d7020-279">Merhaba istemci sertifikası (PFX dosyası) erişim için başlangıç parolası</span><span class="sxs-lookup"><span data-stu-id="d7020-279">hello password for accessing hello client certificate (PFX file)</span></span> |
| <span data-ttu-id="d7020-280">PFX</span><span class="sxs-lookup"><span data-stu-id="d7020-280">pfx</span></span> |<span data-ttu-id="d7020-281">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d7020-281">Required.</span></span> <span data-ttu-id="d7020-282">Base64 ile kodlanmış içeriği hello istemci sertifikasının (PFX dosyası)</span><span class="sxs-lookup"><span data-stu-id="d7020-282">Base64-encoded contents of hello client certificate (PFX file)</span></span> |

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="d7020-283">Temel kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d7020-283">Basic authentication</span></span>

<span data-ttu-id="d7020-284">toovalidate gelen istekleri mantığı uygulama tooyour web uygulaması veya API uygulaması temel kimlik doğrulaması, bir kullanıcı adı ve parola gibi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7020-284">toovalidate incoming requests from your logic app tooyour web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="d7020-285">Temel kimlik doğrulaması genel bir desen olduğundan ve web uygulaması veya API uygulaması herhangi kullanılan dili toobuild bu kimlik doğrulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7020-285">Basic authentication is a common pattern, and you can use this authentication in any language used toobuild your web app or API app.</span></span>

<span data-ttu-id="d7020-286">Merhaba, **yetkilendirme** bölümünde, bu satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d7020-286">In hello **Authorization** section, include this line:</span></span>

<span data-ttu-id="d7020-287">`{"type": "basic", "username": "username", "password": "password"}`.</span><span class="sxs-lookup"><span data-stu-id="d7020-287">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="d7020-288">Öğesi</span><span class="sxs-lookup"><span data-stu-id="d7020-288">Element</span></span> | <span data-ttu-id="d7020-289">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d7020-289">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d7020-290">type</span><span class="sxs-lookup"><span data-stu-id="d7020-290">type</span></span> |<span data-ttu-id="d7020-291">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d7020-291">Required.</span></span> <span data-ttu-id="d7020-292">Merhaba kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="d7020-292">hello authentication type.</span></span> <span data-ttu-id="d7020-293">Temel kimlik doğrulaması için hello değeri olmalıdır `Basic`.</span><span class="sxs-lookup"><span data-stu-id="d7020-293">For basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="d7020-294">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="d7020-294">username</span></span> |<span data-ttu-id="d7020-295">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d7020-295">Required.</span></span> <span data-ttu-id="d7020-296">kimlik doğrulaması için Hello kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="d7020-296">hello username for authentication</span></span> |
| <span data-ttu-id="d7020-297">password</span><span class="sxs-lookup"><span data-stu-id="d7020-297">password</span></span> |<span data-ttu-id="d7020-298">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d7020-298">Required.</span></span> <span data-ttu-id="d7020-299">Merhaba parola kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d7020-299">hello password for authentication</span></span> |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="d7020-300">Kod aracılığıyla Azure Active Directory kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d7020-300">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="d7020-301">Varsayılan olarak, hassas yetkilendirme hello Azure portal kapatma hello Azure AD kimlik doğrulaması sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="d7020-301">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="d7020-302">Örneğin, bu kimlik doğrulama belirli Kiracı, tooa belirli kullanıcı veya uygulama, API toojust kilitler.</span><span class="sxs-lookup"><span data-stu-id="d7020-302">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

<span data-ttu-id="d7020-303">toorestrict API erişim tooyour mantıksal uygulama kod, aracılığıyla hello JSON web token (JWT) sahip hello üstbilgi ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="d7020-303">toorestrict API access tooyour logic app through code, extract hello header that has hello JSON web token (JWT).</span></span> <span data-ttu-id="d7020-304">Merhaba çağıranının kimliğini denetleyin ve eşleşmeyen istekleri reddedecek.</span><span class="sxs-lookup"><span data-stu-id="d7020-304">Check hello caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="d7020-305">Tooimplement devam bu kimlik doğrulaması tamamen kendi kodu ve olmayan kullanım hello Azure portal, bilgi nasıl çok [Azure uygulamanızı şirket içi Active Directory ile kimlik doğrulaması](../app-service-web/web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="d7020-305">Going further, tooimplement this authentication entirely in your own code, and not use hello Azure portal, learn how too [authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>

<span data-ttu-id="d7020-306">toocreate mantıksal uygulamanız için bir uygulama kimliği ve bu kimlik toocall API'nizi kullanın, hello önceki adımları izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7020-306">toocreate an application identity for your logic app and use that identity toocall your API, you must follow hello previous steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7020-307">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d7020-307">Next steps</span></span>

* [<span data-ttu-id="d7020-308">Tanılama günlükleri ve Uyarıları ile mantığı uygulama performansını kontrol etme</span><span class="sxs-lookup"><span data-stu-id="d7020-308">Check logic app performance with diagnostic logs and alerts</span></span>](logic-apps-monitor-your-logic-apps.md)