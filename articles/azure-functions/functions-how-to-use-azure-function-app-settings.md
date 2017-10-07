---
title: "aaaConfigure Azure işlevi uygulama ayarları | Microsoft Docs"
description: "Nasıl tooconfigure Azure işlev uygulaması ayarları hakkında bilgi edinin."
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a><span data-ttu-id="a02d6-103">Nasıl toomanage hello Azure portal'ın bir işlev uygulaması</span><span class="sxs-lookup"><span data-stu-id="a02d6-103">How toomanage a function app in hello Azure portal</span></span> 

<span data-ttu-id="a02d6-104">Azure işlevleri, bir işlev uygulaması, tek tek işlevleri için hello yürütme bağlamı sağlar.</span><span class="sxs-lookup"><span data-stu-id="a02d6-104">In Azure Functions, a function app provides hello execution context for your individual functions.</span></span> <span data-ttu-id="a02d6-105">Verilen işlevin uygulama tarafından barındırılan tooall işlevleri işlevi uygulama davranışları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="a02d6-105">Function app behaviors apply tooall functions hosted by a given function app.</span></span> <span data-ttu-id="a02d6-106">Bu konuda açıklanmaktadır nasıl tooconfigure ve işlev uygulamalarınızda hello Azure portalında yönetin.</span><span class="sxs-lookup"><span data-stu-id="a02d6-106">This topic describes how tooconfigure and manage your function apps in hello Azure portal.</span></span>

<span data-ttu-id="a02d6-107">toobegin, Git toohello [Azure portal](http://portal.azure.com) ve tooyour Azure hesabı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a02d6-107">toobegin, go toohello [Azure portal](http://portal.azure.com) and sign in tooyour Azure account.</span></span> <span data-ttu-id="a02d6-108">Merhaba arama çubuğunda hello portal hello üstündeki işlevi uygulamanızı hello adını yazın ve hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="a02d6-108">In hello search bar at hello top of hello portal, type hello name of your function app and select it from hello list.</span></span> <span data-ttu-id="a02d6-109">İşlev uygulamanızı seçtikten sonra sayfa aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="a02d6-109">After selecting your function app, you see hello following page:</span></span>

![Hello Azure portal işlevi uygulama genel bakış](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <span data-ttu-id="a02d6-111"><a name="manage-app-service-settings"></a>İşlev uygulama ayarları sekmesi</span><span class="sxs-lookup"><span data-stu-id="a02d6-111"><a name="manage-app-service-settings"></a>Function app settings tab</span></span>

![İşlev uygulama hello Azure portalına genel bakış.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

<span data-ttu-id="a02d6-113">Merhaba **ayarları** sekme kullanılabilir işlevi uygulamanız tarafından kullanılan hello işlevleri çalışma zamanı sürümü burada güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a02d6-113">hello **Settings** tab is where you can update hello Functions runtime version used by your function app.</span></span> <span data-ttu-id="a02d6-114">Ayrıca, hello konak kullanılan anahtarları toorestrict HTTP erişim tooall işlevleri hello işlevi uygulama tarafından barındırılan yöneteceğiniz unutulmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="a02d6-114">It is also where you manage hello host keys used toorestrict HTTP access tooall functions hosted by hello function app.</span></span>

<span data-ttu-id="a02d6-115">İşlevler tüketim barındırma ve App Service planları barındırma destekler.</span><span class="sxs-lookup"><span data-stu-id="a02d6-115">Functions supports both Consumption hosting and App Service hosting plans.</span></span> <span data-ttu-id="a02d6-116">Daha fazla bilgi için bkz: [Seç hello doğru hizmet planı Azure işlevleri için](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="a02d6-116">For more information, see [Choose hello correct service plan for Azure Functions](functions-scale.md).</span></span> <span data-ttu-id="a02d6-117">Merhaba tüketim planında daha iyi öngörülebilirlik için işlevleri sağlar, günlük kullanım kotası gigabayt saniye olarak ayarlayarak platform kullanımını sınırla.</span><span class="sxs-lookup"><span data-stu-id="a02d6-117">For better predictability in hello Consumption plan, Functions lets you limit platform usage by setting a daily usage quota, in gigabytes-seconds.</span></span> <span data-ttu-id="a02d6-118">Merhaba günlük kullanım kotası ulaşıldığında, hello işlev uygulaması durdurulur.</span><span class="sxs-lookup"><span data-stu-id="a02d6-118">Once hello daily usage quota is reached, hello function app is stopped.</span></span> <span data-ttu-id="a02d6-119">Kota harcama hello ulaştıktan sonucunda durduruldu bir işlev uygulaması hello yeniden etkinleştirilebilir günlük kota harcama hello kurma olarak aynı bağlamı.</span><span class="sxs-lookup"><span data-stu-id="a02d6-119">A function app stopped as a result of reaching hello spending quota can be re-enabled from hello same context as establishing hello daily spending quota.</span></span> <span data-ttu-id="a02d6-120">Merhaba bkz [Azure fiyatlandırma sayfası işlevleri](http://azure.microsoft.com/pricing/details/functions/) faturalama hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="a02d6-120">See hello [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on billing.</span></span>   

## <a name="platform-features-tab"></a><span data-ttu-id="a02d6-121">Platform Özellikleri sekmesi</span><span class="sxs-lookup"><span data-stu-id="a02d6-121">Platform features tab</span></span>

![İşlev uygulama platformu Özellikleri sekmesi.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

<span data-ttu-id="a02d6-123">İşlev uygulamalarının çalıştırmak ve hello Azure App Service platformu tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="a02d6-123">Function apps run in, and are maintained, by hello Azure App Service platform.</span></span> <span data-ttu-id="a02d6-124">Bu nedenle, işlevi uygulamalarınızı hello Azure'nın çekirdek web barındırma platformu özelliklerini erişim toomost sahip.</span><span class="sxs-lookup"><span data-stu-id="a02d6-124">As such, your function apps have access toomost of hello features of Azure's core web hosting platform.</span></span> <span data-ttu-id="a02d6-125">Merhaba **Platform özellikleri** sekme, burada erişim hello hello işlevi uygulamalarınızda kullanabileceğiniz App Service platformu özelliklerinin çoğu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a02d6-125">hello **Platform features** tab is where you access hello many features of hello App Service platform that you can use in your function apps.</span></span> 

> [!NOTE]
> <span data-ttu-id="a02d6-126">Bir işlev uygulaması hello tüketim barındırma planı üzerinde çalıştığında, tüm uygulama hizmeti özellikleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a02d6-126">Not all App Service features are available when a function app runs on hello Consumption hosting plan.</span></span>

<span data-ttu-id="a02d6-127">Bu konunun geri kalanında Hello hello hello uygulama hizmeti özelliklerinde aşağıdaki işlevleri için yararlı olan Azure portal odaklanır:</span><span class="sxs-lookup"><span data-stu-id="a02d6-127">hello rest of this topic focuses on hello following App Service features in hello Azure portal that are useful for Functions:</span></span>

+ [<span data-ttu-id="a02d6-128">Uygulama hizmeti Düzenleyicisi</span><span class="sxs-lookup"><span data-stu-id="a02d6-128">App Service editor</span></span>](#editor)
+ [<span data-ttu-id="a02d6-129">Uygulama ayarları</span><span class="sxs-lookup"><span data-stu-id="a02d6-129">Application settings</span></span>](#settings) 
+ [<span data-ttu-id="a02d6-130">Console</span><span class="sxs-lookup"><span data-stu-id="a02d6-130">Console</span></span>](#console)
+ [<span data-ttu-id="a02d6-131">Gelişmiş araçlar (Kudu)</span><span class="sxs-lookup"><span data-stu-id="a02d6-131">Advanced tools (Kudu)</span></span>](#kudu)
+ [<span data-ttu-id="a02d6-132">Dağıtım seçenekleri</span><span class="sxs-lookup"><span data-stu-id="a02d6-132">Deployment options</span></span>](#deployment)
+ [<span data-ttu-id="a02d6-133">CORS</span><span class="sxs-lookup"><span data-stu-id="a02d6-133">CORS</span></span>](#cors)
+ [<span data-ttu-id="a02d6-134">Kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="a02d6-134">Authentication</span></span>](#auth)
+ [<span data-ttu-id="a02d6-135">API tanımı</span><span class="sxs-lookup"><span data-stu-id="a02d6-135">API definition</span></span>](#swagger)

<span data-ttu-id="a02d6-136">Hakkında daha fazla bilgi için uygulama hizmeti ayarlarla toowork bkz [Azure App Service ayarlarını yapılandır](../app-service-web/web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="a02d6-136">For more information about how toowork with App Service settings, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

### <span data-ttu-id="a02d6-137"><a name="editor"></a>Uygulama hizmeti Düzenleyicisi</span><span class="sxs-lookup"><span data-stu-id="a02d6-137"><a name="editor"></a>App Service Editor</span></span>

| | |
|-|-|
| ![İşlev uygulaması App Service Düzenleyici.](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | <span data-ttu-id="a02d6-139">Hello uygulama hizmeti Düzenleyicisi toomodify JSON yapılandırma dosyalarını ve kod dosyaları aynı şekilde kullanabileceğiniz bir Gelişmiş portala düzenleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="a02d6-139">hello App Service editor is an advanced in-portal editor that you can use toomodify JSON configuration files and code files alike.</span></span> <span data-ttu-id="a02d6-140">Bu seçeneğin belirlenmesi temel bir düzenleyici olan ayrı bir tarayıcı sekmesi başlatır.</span><span class="sxs-lookup"><span data-stu-id="a02d6-140">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="a02d6-141">Bu toointegrate hello Git deposu, çalıştırma ve hata ayıklama kodu sağlar ve işlev uygulama ayarlarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a02d6-141">This enables you toointegrate with hello Git repository, run and debug code, and modify function app settings.</span></span> <span data-ttu-id="a02d6-142">Bu düzenleyici hello varsayılan işlevi uygulaması dikey ile karşılaştırıldığında, İşlevler için bir Gelişmiş geliştirme ortamı sağlar.</span><span class="sxs-lookup"><span data-stu-id="a02d6-142">This editor provides an enhanced development environment for your functions compared with hello default function app blade.</span></span>    |

![Merhaba uygulama hizmeti Düzenleyicisi](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <span data-ttu-id="a02d6-144"><a name="settings"></a>Uygulama ayarları</span><span class="sxs-lookup"><span data-stu-id="a02d6-144"><a name="settings"></a>Application settings</span></span>

| | |
|-|-|
| ![İşlev app uygulama ayarları.](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | <span data-ttu-id="a02d6-146">Uygulama hizmeti Hello **uygulama ayarları** dikey penceresinde, burada yapılandırın ve framework sürümleri, uzaktan hata ayıklama, uygulama ayarları ve bağlantı dizelerini Yönet.</span><span class="sxs-lookup"><span data-stu-id="a02d6-146">hello App Service **Application settings** blade is where you configure and manage framework versions, remote debugging, app settings, and connection strings.</span></span> <span data-ttu-id="a02d6-147">Diğer Azure ve üçüncü taraf hizmetleri ile işlevi uygulamanızı'i tümleştirdiğinizde burada bu ayarları değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a02d6-147">When you integrate your function app with other Azure and third-party services, you can modify those settings here.</span></span> |

![Uygulama ayarlarını yapılandırın](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <span data-ttu-id="a02d6-149"><a name="console"></a>Konsol</span><span class="sxs-lookup"><span data-stu-id="a02d6-149"><a name="console"></a>Console</span></span>

| | |
|-|-|
| ![Hello Azure portalında uygulama konsolunda işlevi](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | <span data-ttu-id="a02d6-151">Merhaba komut satırından işlevi uygulamanızla toointeract tercih zaman hello portala konsolu bir ideal Geliştirici aracıdır.</span><span class="sxs-lookup"><span data-stu-id="a02d6-151">hello in-portal console is an ideal developer tool when you prefer toointeract with your function app from hello command line.</span></span> <span data-ttu-id="a02d6-152">Sık kullanılan komutlar dizin ve dosya oluşturma ve gezinti yanı toplu iş dosyaları ve komut dosyaları yürütme içerir.</span><span class="sxs-lookup"><span data-stu-id="a02d6-152">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> |

![Uygulama Konsolu işlevi](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <span data-ttu-id="a02d6-154"><a name="kudu"></a>Gelişmiş araçlar (Kudu)</span><span class="sxs-lookup"><span data-stu-id="a02d6-154"><a name="kudu"></a>Advanced tools (Kudu)</span></span>

| | |
|-|-|
| ![Hello Azure portal Kudu uygulamada işlevi](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | <span data-ttu-id="a02d6-156">Merhaba uygulama hizmeti (Kudu olarak da bilinir) için Gelişmiş araçlar erişim işlevi uygulamanızı tooadvanced yönetim özelliklerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="a02d6-156">hello advanced tools for App Service (also known as Kudu) provide access tooadvanced administrative features of your function app.</span></span> <span data-ttu-id="a02d6-157">Kudu sistem bilgileri, uygulama ayarları, ortam değişkenleri, site uzantıları, HTTP üstbilgileri ve sunucu değişkenlerine yönetin.</span><span class="sxs-lookup"><span data-stu-id="a02d6-157">From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables.</span></span> <span data-ttu-id="a02d6-158">Ayrıca başlatma **Kudu** işlev uygulamanız için toohello SCM uç noktasının gibi giderek`https://<myfunctionapp>.scm.azurewebsites.net/`</span><span class="sxs-lookup"><span data-stu-id="a02d6-158">You can also launch **Kudu** by browsing toohello SCM endpoint for your function app, like `https://<myfunctionapp>.scm.azurewebsites.net/`</span></span> |

![Kudu yapılandırın](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><span data-ttu-id="a02d6-160"><a name="deployment">Dağıtım seçenekleri</span><span class="sxs-lookup"><span data-stu-id="a02d6-160"><a name="deployment">Deployment options</span></span>

| | |
|-|-|
| ![Hello Azure portal'ın işlevi uygulama dağıtım seçenekleri](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | <span data-ttu-id="a02d6-162">İşlevler işlevi kodunuzu yerel makinenizde geliştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a02d6-162">Functions lets you develop your function code on your local machine.</span></span> <span data-ttu-id="a02d6-163">Ardından, yerel bir işlev uygulaması proje tooAzure karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a02d6-163">You can then upload your local function app project tooAzure.</span></span> <span data-ttu-id="a02d6-164">Ayrıca tootraditional FTP karşıya yükleme, işlevler sağlar, GitHub, VSTS, Dropbox, Bitbucket ve diğerleri gibi popüler sürekli tümleştirme çözümleri kullanarak işlevi uygulamanızı dağıtma.</span><span class="sxs-lookup"><span data-stu-id="a02d6-164">In addition tootraditional FTP upload, Functions lets you deploy your function app using popular continuous integration solutions, like GitHub, VSTS, Dropbox, Bitbucket, and others.</span></span> <span data-ttu-id="a02d6-165">Daha fazla bilgi için bkz: [Azure işlevleri için sürekli dağıtım](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="a02d6-165">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span> <span data-ttu-id="a02d6-166">FTP veya yerel Git kullanarak el ile tooupload ayrıca gerekir [dağıtım kimlik bilgilerinizi yapılandırma](functions-continuous-deployment.md#credentials).</span><span class="sxs-lookup"><span data-stu-id="a02d6-166">tooupload manually using FTP or local Git, you also must [configure your deployment credentials](functions-continuous-deployment.md#credentials).</span></span> |


### <span data-ttu-id="a02d6-167"><a name="cors"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="a02d6-167"><a name="cors"></a>CORS</span></span>

| | |
|-|-|
| ![Hello Azure portal CORS uygulamada işlevi](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | <span data-ttu-id="a02d6-169">tooprevent kötü amaçlı kod yürütme hizmetlerinizde uygulama hizmeti blokları, dış kaynaklardan tooyour işlev uygulamalarının çağırır.</span><span class="sxs-lookup"><span data-stu-id="a02d6-169">tooprevent malicious code execution in your services, App Service blocks calls tooyour function apps from external sources.</span></span> <span data-ttu-id="a02d6-170">Çıkış noktaları arası kaynak paylaşımı (CORS) toolet "işlevlerinizi Uzak istekleri kabul edebilir çıkış izin verilen bir beyaz liste", tanımladığınız işlevlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="a02d6-170">Functions supports cross-origin resource sharing (CORS) toolet you define a "whitelist" of allowed origins from which your functions can accept remote requests.</span></span>  |

![İşlev uygulamanın yapılandırma CORS](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <span data-ttu-id="a02d6-172"><a name="auth"></a>Kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="a02d6-172"><a name="auth"></a>Authentication</span></span>

| | |
|-|-|
| ![Hello Azure portal işlevi uygulama kimlik doğrulaması](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | <span data-ttu-id="a02d6-174">İşlevler bir HTTP tetikleyicisi kullandığınızda çağrıları gerektirebilir toofirst kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="a02d6-174">When functions use an HTTP trigger, you can require calls toofirst be authenticated.</span></span> <span data-ttu-id="a02d6-175">Uygulama hizmeti, Azure Active Directory kimlik doğrulaması ve oturum açın. Facebook, Microsoft ve Twitter gibi sosyal sağlayıcılardan destekler.</span><span class="sxs-lookup"><span data-stu-id="a02d6-175">App Service supports Azure Active Directory authentication and sign in with social providers, such as Facebook, Microsoft, and Twitter.</span></span> <span data-ttu-id="a02d6-176">Özel kimlik doğrulama sağlayıcılarını yapılandırma hakkında daha fazla bilgi için bkz: [Azure App Service kimlik doğrulamasına genel bakış](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a02d6-176">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span> |

![Bir işlev uygulaması için kimlik doğrulamasını yapılandırma](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <span data-ttu-id="a02d6-178"><a name="swagger"></a>API tanımı</span><span class="sxs-lookup"><span data-stu-id="a02d6-178"><a name="swagger"></a>API definition</span></span>

| | |
|-|-|
| ![İşlevi uygulama API'si swagger tanımında hello Azure portalı](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | <span data-ttu-id="a02d6-180">İşlevlerini destekleyen Swagger tooallow istemcileri toomore kolayca kullanmalarını HTTP tetiklemeli işlevleri.</span><span class="sxs-lookup"><span data-stu-id="a02d6-180">Functions supports Swagger tooallow clients toomore easily consume your HTTP-triggered functions.</span></span> <span data-ttu-id="a02d6-181">Swagger ile API tanımları oluşturma hakkında daha fazla bilgi için [API Apps, ASP.NET ve Swagger Azure ile çalışmaya başlama](../app-service-api/app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a02d6-181">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="a02d6-182">İşlevler proxy'leri toodefine tek bir API yüzeyi birden çok işlevleri için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a02d6-182">You can also use Functions Proxies toodefine a single API surface for multiple functions.</span></span> <span data-ttu-id="a02d6-183">Daha fazla bilgi için bkz: [Azure işlevleri proxy'leri çalışma](functions-proxies.md).</span><span class="sxs-lookup"><span data-stu-id="a02d6-183">For more information, see [Working with Azure Functions Proxies](functions-proxies.md).</span></span> |

![İşlev uygulamanın API yapılandırın](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a><span data-ttu-id="a02d6-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a02d6-185">Next steps</span></span>

+ [<span data-ttu-id="a02d6-186">Azure App Service ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a02d6-186">Configure Azure App Service Settings</span></span>](../app-service-web/web-sites-configure.md)
+ [<span data-ttu-id="a02d6-187">Azure İşlevleri için sürekli dağıtım</span><span class="sxs-lookup"><span data-stu-id="a02d6-187">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)



