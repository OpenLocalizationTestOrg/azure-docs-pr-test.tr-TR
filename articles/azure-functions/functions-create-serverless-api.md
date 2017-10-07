---
title: "Azure işlevleri kullanarak sunucusuz bir API aaaCreate | Microsoft Docs"
description: "Nasıl toocreate Azure işlevleri kullanarak sunucusuz bir API"
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a><span data-ttu-id="c4e22-103">Azure işlevleri kullanarak sunucusuz bir API oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4e22-103">Create a serverless API using Azure Functions</span></span>

<span data-ttu-id="c4e22-104">Bu öğreticide nasıl toobuild sağlar Azure işlevleri öğreneceksiniz yüksek düzeyde ölçeklenebilir API'leri.</span><span class="sxs-lookup"><span data-stu-id="c4e22-104">In this tutorial you will learn how Azure Functions allows you toobuild highly-scalable APIs.</span></span> <span data-ttu-id="c4e22-105">Azure işlevleri, bir uç nokta diller, Node.JS, C# ve daha fazlası da dahil olmak üzere çeşitli yerleşik HTTP tetikleyiciler ve kolay tooauthor anlamasını bağlamaları koleksiyonu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="c4e22-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings which make it easy tooauthor an endpoint in a variety of languages, including Node.JS, C#, and more.</span></span> <span data-ttu-id="c4e22-106">Bu öğreticide, bir HTTP tetikleyicisi toohandle belirli eylemler API tasarımınızda özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c4e22-106">In this tutorial, you will customize an HTTP trigger toohandle specific actions in your API design.</span></span> <span data-ttu-id="c4e22-107">Ayrıca, Azure işlevleri proxy'leri ile tümleştirme ve sahte API'leri ayarlayarak API'nizi artan için hazırlarsınız.</span><span class="sxs-lookup"><span data-stu-id="c4e22-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span></span> <span data-ttu-id="c4e22-108">Tüm bunlar gerçekleştirilir hello işlevleri sunucusuz bilgi işlem ortamı en üstünde, kaynakları ölçeklendirme hakkında tooworry yok - yalnızca, API mantığına odaklanabilir şekilde.</span><span class="sxs-lookup"><span data-stu-id="c4e22-108">All of this is accomplished on top of hello Functions serverless compute environment, so you don't have tooworry about scaling resources - you can just focus on your API logic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4e22-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c4e22-109">Prerequisites</span></span> 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

<span data-ttu-id="c4e22-110">Merhaba elde edilen işlevi Bu öğretici hello kalanı için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c4e22-110">hello resulting function will be used for hello rest of this tutorial.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="c4e22-111">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="c4e22-111">Sign in tooAzure</span></span>

<span data-ttu-id="c4e22-112">Açık hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="c4e22-112">Open hello Azure portal.</span></span> <span data-ttu-id="c4e22-113">toodo Bu, çok oturum[https://portal.azure.com](https://portal.azure.com) Azure hesabınızla.</span><span class="sxs-lookup"><span data-stu-id="c4e22-113">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

## <a name="customize-your-http-function"></a><span data-ttu-id="c4e22-114">HTTP işlevinizi özelleştirme</span><span class="sxs-lookup"><span data-stu-id="c4e22-114">Customize your HTTP function</span></span>

<span data-ttu-id="c4e22-115">Varsayılan olarak, HTTP tetiklemeli işlevin yapılandırılmış tooaccept olan herhangi bir HTTP yöntemi.</span><span class="sxs-lookup"><span data-stu-id="c4e22-115">By default, your HTTP-triggered function is configured tooaccept any HTTP method.</span></span> <span data-ttu-id="c4e22-116">Ayrıca varsayılan URL hello formunun olduğu `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span><span class="sxs-lookup"><span data-stu-id="c4e22-116">There is also a default URL of hello form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span></span> <span data-ttu-id="c4e22-117">Merhaba hızlı başlangıç, ardından izlediyseniz `<funcname>` büyük olasılıkla "HttpTriggerJS1" şöyle görünür.</span><span class="sxs-lookup"><span data-stu-id="c4e22-117">If you followed hello quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span></span> <span data-ttu-id="c4e22-118">Bu bölümde, hello işlevi toorespond yalnızca tooGET istekler değiştirecek `/api/hello` yerine rota.</span><span class="sxs-lookup"><span data-stu-id="c4e22-118">In this section, you will modify hello function toorespond only tooGET requests against `/api/hello` route instead.</span></span> 

<span data-ttu-id="c4e22-119">Tooyour işlevinde hello Azure portalına gidin.</span><span class="sxs-lookup"><span data-stu-id="c4e22-119">Navigate tooyour function in hello Azure portal.</span></span> <span data-ttu-id="c4e22-120">Seçin **tümleştir** sol gezinti hello içinde.</span><span class="sxs-lookup"><span data-stu-id="c4e22-120">Select **Integrate** in hello left navigation.</span></span>

![Bir HTTP işlevi özelleştirme](./media/functions-create-serverless-api/customizing-http.png)

<span data-ttu-id="c4e22-122">Merhaba tabloda belirtildiği gibi HTTP tetikleyicisi ayarlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4e22-122">Use the HTTP trigger settings as specified in hello table.</span></span>

| <span data-ttu-id="c4e22-123">Alan</span><span class="sxs-lookup"><span data-stu-id="c4e22-123">Field</span></span> | <span data-ttu-id="c4e22-124">Örnek değer</span><span class="sxs-lookup"><span data-stu-id="c4e22-124">Sample value</span></span> | <span data-ttu-id="c4e22-125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c4e22-125">Description</span></span> |
|---|---|---|
| <span data-ttu-id="c4e22-126">İzin verilen HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="c4e22-126">Allowed HTTP methods</span></span> | <span data-ttu-id="c4e22-127">Seçili yöntemleri</span><span class="sxs-lookup"><span data-stu-id="c4e22-127">Selected methods</span></span> | <span data-ttu-id="c4e22-128">Hangi HTTP yöntemlerini kullanılan tooinvoke olabilir belirler bu işlevi</span><span class="sxs-lookup"><span data-stu-id="c4e22-128">Determines what HTTP methods may be used tooinvoke this function</span></span> |
| <span data-ttu-id="c4e22-129">Seçili HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="c4e22-129">Selected HTTP methods</span></span> | <span data-ttu-id="c4e22-130">AL</span><span class="sxs-lookup"><span data-stu-id="c4e22-130">GET</span></span> | <span data-ttu-id="c4e22-131">Yalnızca seçili HTTP yöntemleri toobe tooinvoke bu işlev kullanılan sağlar</span><span class="sxs-lookup"><span data-stu-id="c4e22-131">Allows only selected HTTP methods toobe used tooinvoke this function</span></span> |
| <span data-ttu-id="c4e22-132">Rota şablonu</span><span class="sxs-lookup"><span data-stu-id="c4e22-132">Route template</span></span> | <span data-ttu-id="c4e22-133">/ Merhaba</span><span class="sxs-lookup"><span data-stu-id="c4e22-133">/hello</span></span> | <span data-ttu-id="c4e22-134">Kullanılan tooinvoke hangi rota belirler bu işlevi</span><span class="sxs-lookup"><span data-stu-id="c4e22-134">Determines what route is used tooinvoke this function</span></span> |

<span data-ttu-id="c4e22-135">Merhaba içermeyen Not `/api` bu genel bir ayar tarafından gerçekleştirilir gibi temel yol önekini hello rota şablonu.</span><span class="sxs-lookup"><span data-stu-id="c4e22-135">Note that you did not include hello `/api` base path prefix in hello route template, as this is handled by a global setting.</span></span>

<span data-ttu-id="c4e22-136">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c4e22-136">Click **Save**.</span></span>

<span data-ttu-id="c4e22-137">HTTP işlevlerini özelleştirme hakkında daha fazla bilgiyi [Azure işlevleri HTTP ve Web kancası bağlamaları](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span><span class="sxs-lookup"><span data-stu-id="c4e22-137">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span></span>

### <a name="test-your-api"></a><span data-ttu-id="c4e22-138">API'nizi test</span><span class="sxs-lookup"><span data-stu-id="c4e22-138">Test your API</span></span>

<span data-ttu-id="c4e22-139">Ardından, işlevi toosee hello yeni API yüzeyi ile çalışma test.</span><span class="sxs-lookup"><span data-stu-id="c4e22-139">Next, test your function toosee it working with hello new API surface.</span></span>

<span data-ttu-id="c4e22-140">Sol gezinti hello hello işlevin adını tıklayarak geri toohello geliştirme sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="c4e22-140">Navigate back toohello development page by clicking on hello function's name in hello left navigation.</span></span>

<span data-ttu-id="c4e22-141">Tıklatın **Al işlevi URL** ve hello URL'yi kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c4e22-141">Click **Get function URL** and copy hello URL.</span></span> <span data-ttu-id="c4e22-142">Merhaba kullandığını görürsünüz `/api/hello` şimdi rota.</span><span class="sxs-lookup"><span data-stu-id="c4e22-142">You should see that it uses hello `/api/hello` route now.</span></span>

<span data-ttu-id="c4e22-143">Yeni bir tarayıcı sekmesi ya da tercih edilen REST istemciniz Hello URL'sini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c4e22-143">Copy hello URL into a new browser tab or your preferred REST client.</span></span> <span data-ttu-id="c4e22-144">Tarayıcılar GET varsayılan olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="c4e22-144">Browsers will use GET by default.</span></span>

<span data-ttu-id="c4e22-145">Merhaba işlevi çalıştırın ve çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c4e22-145">Run hello function and confirm that it is working.</span></span> <span data-ttu-id="c4e22-146">Bir sorgu dizesi toosatisfy hello quickstart kodu olarak tooprovide hello "name" parametre gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c4e22-146">You may need tooprovide hello "name" parameter as a query string toosatisfy hello quickstart code.</span></span>

<span data-ttu-id="c4e22-147">Ayrıca, başka bir HTTP yöntemini tooconfirm hello işlevi yürütülmez ile Merhaba uç noktası çağrılmadan deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4e22-147">You can also try calling hello endpoint with another HTTP method tooconfirm that hello function is not executed.</span></span> <span data-ttu-id="c4e22-148">Bunun için toouse cURL, Postman veya Fiddler gibi bir REST istemcisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4e22-148">For this, you will need toouse a REST client, such as cURL, Postman, or Fiddler.</span></span>

## <a name="proxies-overview"></a><span data-ttu-id="c4e22-149">Proxy'leri genel bakış</span><span class="sxs-lookup"><span data-stu-id="c4e22-149">Proxies overview</span></span>

<span data-ttu-id="c4e22-150">Merhaba sonraki bölümde, bir proxy üzerinden API'nizi belirir.</span><span class="sxs-lookup"><span data-stu-id="c4e22-150">In hello next section, you will surface your API through a proxy.</span></span> <span data-ttu-id="c4e22-151">Azure işlevleri proxy'leri tooforward istekleri tooother kaynakları sağlayan bir önizleme özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="c4e22-151">Azure Functions Proxies is a preview feature that allows you tooforward requests tooother resources.</span></span> <span data-ttu-id="c4e22-152">Bir HTTP uç noktası HTTP tetikleyicisi ile olduğu gibi tanımlayın, ancak bu uç çağrıldığında kodu tooexecute yazmak yerine, bir URL tooa uzak uygulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="c4e22-152">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code tooexecute when that endpoint is called, you provide a URL tooa remote implementation.</span></span> <span data-ttu-id="c4e22-153">Bu, istemcilerin tooconsume için kolay olan tek bir API yüzeyi içine birden çok API kaynakları toocompose sağlar.</span><span class="sxs-lookup"><span data-stu-id="c4e22-153">This allows you toocompose multiple API sources into a single API surface which is easy for clients tooconsume.</span></span> <span data-ttu-id="c4e22-154">API'nizi mikro olarak toobuild isterseniz, bu özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="c4e22-154">This is particularly useful if you wish toobuild your API as microservices.</span></span>

<span data-ttu-id="c4e22-155">Bir proxy gibi tooany HTTP kaynak gösterebilir:</span><span class="sxs-lookup"><span data-stu-id="c4e22-155">A proxy can point tooany HTTP resource, such as:</span></span>
- <span data-ttu-id="c4e22-156">Azure İşlevleri</span><span class="sxs-lookup"><span data-stu-id="c4e22-156">Azure Functions</span></span> 
- <span data-ttu-id="c4e22-157">API uygulamaları [Azure uygulama hizmeti](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span><span class="sxs-lookup"><span data-stu-id="c4e22-157">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span></span>
- <span data-ttu-id="c4e22-158">Docker kapsayıcılarında [Linux uygulama hizmeti](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span><span class="sxs-lookup"><span data-stu-id="c4e22-158">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span></span>
- <span data-ttu-id="c4e22-159">Barındırılan herhangi bir API'yi</span><span class="sxs-lookup"><span data-stu-id="c4e22-159">Any other hosted API</span></span>

<span data-ttu-id="c4e22-160">toolearn proxy'leri hakkında daha fazla bilgi görmek [Azure işlevleri proxy'leri (Önizleme) çalışmaya].</span><span class="sxs-lookup"><span data-stu-id="c4e22-160">toolearn more about proxies, see [Working with Azure Functions Proxies (preview)].</span></span>

## <a name="create-your-first-proxy"></a><span data-ttu-id="c4e22-161">İlk proxy oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4e22-161">Create your first proxy</span></span>

<span data-ttu-id="c4e22-162">Bu bölümde, yeni bir proxy hangi görevi görür bir ön uç tooyour oluşturacağınız Genel API.</span><span class="sxs-lookup"><span data-stu-id="c4e22-162">In this section, you will create a new proxy which serves as a frontend tooyour overall API.</span></span> 

### <a name="setting-up-hello-frontend-environment"></a><span data-ttu-id="c4e22-163">Merhaba ön uç ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="c4e22-163">Setting up hello frontend environment</span></span>

<span data-ttu-id="c4e22-164">Çok Hello adımları yineleyin[bir işlev uygulaması oluşturma](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate yeni bir işlev uygulaması proxy oluşturacak içinde.</span><span class="sxs-lookup"><span data-stu-id="c4e22-164">Repeat hello steps too[Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate a new function app in which you will create your proxy.</span></span> <span data-ttu-id="c4e22-165">Bu yeni uygulama için bizim API hello ön uç hizmet verir ve önceden düzenlemekte olduğunuz hello işlev uygulaması arka ucu olarak hizmet verecektir.</span><span class="sxs-lookup"><span data-stu-id="c4e22-165">This new app will serve as hello frontend for our API, and hello function app you were previously editing will serve as a backend.</span></span>

<span data-ttu-id="c4e22-166">Tooyour yeni ön uç işlev uygulaması hello portalında gidin.</span><span class="sxs-lookup"><span data-stu-id="c4e22-166">Navigate tooyour new frontend function app in hello portal.</span></span>

<span data-ttu-id="c4e22-167">Seçin **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="c4e22-167">Select **Settings**.</span></span> <span data-ttu-id="c4e22-168">Ardından geçiş **etkinleştirmek Azure işlevleri proxy'leri (Önizleme)** çok "açık".</span><span class="sxs-lookup"><span data-stu-id="c4e22-168">Then toggle **Enable Azure Functions Proxies (preview)** too"On".</span></span>

<span data-ttu-id="c4e22-169">Seçin **Platform ayarları** ve **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="c4e22-169">Select **Platform Settings** and choose **Application Settings**.</span></span>

<span data-ttu-id="c4e22-170">Çok ilerleyin**uygulama ayarları** ve "HELLO_HOST" anahtarı ile yeni bir ayar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c4e22-170">Scroll down too**App settings** and create a new setting with key "HELLO_HOST".</span></span> <span data-ttu-id="c4e22-171">Değer toohello ana bilgisayar, arka uç işlevi uygulamanızın ayarlamak `<YourApp>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="c4e22-171">Set its value toohello host of your backend function app, such as `<YourApp>.azurewebsites.net`.</span></span> <span data-ttu-id="c4e22-172">Bu, HTTP işlevinizi test edilirken daha önce kopyaladığınız hello URL parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="c4e22-172">This is part of hello URL that you copied earlier when testing your HTTP function.</span></span> <span data-ttu-id="c4e22-173">Bu ayar daha sonra hello yapılandırmasında başvuru.</span><span class="sxs-lookup"><span data-stu-id="c4e22-173">You'll reference this setting in hello configuration later.</span></span>

> [!NOTE] 
> <span data-ttu-id="c4e22-174">Uygulama ayarları hello proxy için sabit kodlanmış ortamı bağımlılık hello ana bilgisayar yapılandırma tooprevent için önerilir.</span><span class="sxs-lookup"><span data-stu-id="c4e22-174">App settings are recommended for hello host configuration tooprevent a hard-coded environment dependency for hello proxy.</span></span> <span data-ttu-id="c4e22-175">Uygulama ayarları kullanarak hello proxy yapılandırması ortamlar arasında taşıyabilirsiniz ve hello ortama özgü uygulama ayarları uygulanacak anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c4e22-175">Using app settings means that you can move hello proxy configuration between environments, and hello environment-specific app settings will be applied.</span></span>

<span data-ttu-id="c4e22-176">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c4e22-176">Click **Save**.</span></span>

### <a name="creating-a-proxy-on-hello-frontend"></a><span data-ttu-id="c4e22-177">Bir proxy hello ön uç üzerinde oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4e22-177">Creating a proxy on hello frontend</span></span>

<span data-ttu-id="c4e22-178">Merhaba portalında geri tooyour ön uç işlevi uygulamasına gidin.</span><span class="sxs-lookup"><span data-stu-id="c4e22-178">Navigate back tooyour frontend function app in hello portal.</span></span>

<span data-ttu-id="c4e22-179">Merhaba sol gezinti bölmesinde hello oturum plus '+' sonraki çok tıklayın "Proxy'leri (Önizleme)".</span><span class="sxs-lookup"><span data-stu-id="c4e22-179">In hello left-hand navigation, click hello plus sign '+' next too"Proxies (preview)".</span></span>

![Bir proxy sunucu oluşturma](./media/functions-create-serverless-api/creating-proxy.png)

<span data-ttu-id="c4e22-181">Merhaba tabloda belirtildiği gibi proxy ayarlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4e22-181">Use proxy settings as specified in hello table.</span></span>

| <span data-ttu-id="c4e22-182">Alan</span><span class="sxs-lookup"><span data-stu-id="c4e22-182">Field</span></span> | <span data-ttu-id="c4e22-183">Örnek değer</span><span class="sxs-lookup"><span data-stu-id="c4e22-183">Sample value</span></span> | <span data-ttu-id="c4e22-184">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c4e22-184">Description</span></span> |
|---|---|---|
| <span data-ttu-id="c4e22-185">Ad</span><span class="sxs-lookup"><span data-stu-id="c4e22-185">Name</span></span> | <span data-ttu-id="c4e22-186">HelloProxy</span><span class="sxs-lookup"><span data-stu-id="c4e22-186">HelloProxy</span></span> | <span data-ttu-id="c4e22-187">Yalnızca yönetim için kullanılan bir kolay ad</span><span class="sxs-lookup"><span data-stu-id="c4e22-187">A friendly name used only for management</span></span> |
| <span data-ttu-id="c4e22-188">Rota şablonu</span><span class="sxs-lookup"><span data-stu-id="c4e22-188">Route template</span></span> | <span data-ttu-id="c4e22-189">/ api/hello</span><span class="sxs-lookup"><span data-stu-id="c4e22-189">/api/hello</span></span> | <span data-ttu-id="c4e22-190">Kullanılan tooinvoke hangi rota belirler bu proxy</span><span class="sxs-lookup"><span data-stu-id="c4e22-190">Determines what route is used tooinvoke this proxy</span></span> |
| <span data-ttu-id="c4e22-191">Arka uç URL'si</span><span class="sxs-lookup"><span data-stu-id="c4e22-191">Backend URL</span></span> | <span data-ttu-id="c4e22-192">https://%HELLO_HOST%/api/Hello</span><span class="sxs-lookup"><span data-stu-id="c4e22-192">https://%HELLO_HOST%/api/hello</span></span> | <span data-ttu-id="c4e22-193">Merhaba uç noktası toowhich hello isteği yönlendirilirken belirtir</span><span class="sxs-lookup"><span data-stu-id="c4e22-193">Specifies hello endpoint toowhich hello request should be proxied</span></span> |

<span data-ttu-id="c4e22-194">Proxy'leri sağlamaz, hello Not `/api` taban yol öneki ve hello rota şablona dahil bu gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4e22-194">Note that Proxies does not provide hello `/api` base path prefix, and this must be included in hello route template.</span></span>

<span data-ttu-id="c4e22-195">Merhaba `%HELLO_HOST%` sözdizimi, daha önce oluşturduğunuz hello uygulama ayarı başvuru.</span><span class="sxs-lookup"><span data-stu-id="c4e22-195">hello `%HELLO_HOST%` syntax will reference hello app setting you created earlier.</span></span> <span data-ttu-id="c4e22-196">Merhaba, URL tooyour özgün işlevi işaret edecek çözümlendi.</span><span class="sxs-lookup"><span data-stu-id="c4e22-196">hello resolved URL will point tooyour original function.</span></span>

<span data-ttu-id="c4e22-197">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c4e22-197">Click **Create**.</span></span>

<span data-ttu-id="c4e22-198">Merhaba Proxy URL'si kopyalayarak ve hello tarayıcıda veya test sık kullanılan HTTP istemci ile yeni proxy deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4e22-198">You can try out your new proxy by copying hello Proxy URL and testing it in hello browser or with your favorite HTTP client.</span></span>

## <a name="create-a-mock-api"></a><span data-ttu-id="c4e22-199">Sahte bir API oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4e22-199">Create a mock API</span></span>

<span data-ttu-id="c4e22-200">Ardından, çözümünüz için bir proxy toocreate sahte bir API kullanır.</span><span class="sxs-lookup"><span data-stu-id="c4e22-200">Next, you will use a proxy toocreate a mock API for your solution.</span></span> <span data-ttu-id="c4e22-201">Bu istemci geliştirme sağlar tam olarak uygulanan hello arka uç gerek olmadan tooprogress.</span><span class="sxs-lookup"><span data-stu-id="c4e22-201">This allows client development tooprogress, without needing hello backend fully implemented.</span></span> <span data-ttu-id="c4e22-202">Geliştirme, daha sonra bu mantığı destekleyen yeni bir işlev uygulaması oluşturmak ve proxy tooit yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="c4e22-202">Later in development, you could create a new function app which supports this logic and redirect your proxy tooit.</span></span>

<span data-ttu-id="c4e22-203">toocreate bu mock API, yeni bir proxy hello kullanarak bu kez oluşturacağız [App Service Düzenleyicisi](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span><span class="sxs-lookup"><span data-stu-id="c4e22-203">toocreate this mock API, we will create a new proxy, this time using hello [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span></span> <span data-ttu-id="c4e22-204">başlatıldı, tooget tooyour işlev uygulaması hello portalında gidin.</span><span class="sxs-lookup"><span data-stu-id="c4e22-204">tooget started, navigate tooyour function app in hello portal.</span></span> <span data-ttu-id="c4e22-205">Seçin **Platform özellikleri** ve Bul **App Service Düzenleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="c4e22-205">Select **Platform features** and find **App Service Editor**.</span></span> <span data-ttu-id="c4e22-206">Bu tıklandığında hello App Service Düzenleyicisi yeni sekmede açılır.</span><span class="sxs-lookup"><span data-stu-id="c4e22-206">Clicking this will open hello App Service Editor in a new tab.</span></span>

<span data-ttu-id="c4e22-207">Seçin `proxies.json` sol gezinti hello içinde.</span><span class="sxs-lookup"><span data-stu-id="c4e22-207">Select `proxies.json` in hello left navigation.</span></span> <span data-ttu-id="c4e22-208">Bu, proxy'leri tamamı için hello yapılandırma depolayan hello dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="c4e22-208">This is hello file which stores hello configuration for all of your proxies.</span></span> <span data-ttu-id="c4e22-209">Merhaba birini kullanırsanız [işlevleri dağıtım yöntemleri](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), bu kaynak denetiminde koruyacaktır hello dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="c4e22-209">If you use one of hello [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is hello file you will maintain in source control.</span></span> <span data-ttu-id="c4e22-210">Bu dosya hakkında daha fazla toolearn bkz [proxy'leri Gelişmiş Yapılandırma](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span><span class="sxs-lookup"><span data-stu-id="c4e22-210">toolearn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span></span>

<span data-ttu-id="c4e22-211">O ana kadarki izlediyseniz, proxies.json hello aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="c4e22-211">If you've followed along so far, your proxies.json should look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

<span data-ttu-id="c4e22-212">Sonraki sahte API'nizi ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c4e22-212">Next you'll add your mock API.</span></span> <span data-ttu-id="c4e22-213">Proxies.json dosyanızı hello şununla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="c4e22-213">Replace your proxies.json file with hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

<span data-ttu-id="c4e22-214">Bu yeni olmadan bir proxy, "GetUserByName" Merhaba backendUri özelliği ekler.</span><span class="sxs-lookup"><span data-stu-id="c4e22-214">This adds a new proxy, "GetUserByName", without hello backendUri property.</span></span> <span data-ttu-id="c4e22-215">Başka bir kaynak çağırmak yerine, bir yanıt geçersiz kılma kullanılarak proxy'leri hello varsayılan yanıttan değiştirir.</span><span class="sxs-lookup"><span data-stu-id="c4e22-215">Instead of calling another resource, it modifies hello default response from Proxies using a response override.</span></span> <span data-ttu-id="c4e22-216">İstek ve yanıt geçersiz kılmaları da arka uç URL'si ile birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c4e22-216">Request and response overrides can also be used in conjunction with a backend URL.</span></span> <span data-ttu-id="c4e22-217">Burada ihtiyacınız olabilecek toomodify üstbilgiler, sorgu parametreleri, vb. toolearn istek ve yanıt geçersiz kılmalar hakkında daha fazla bilgi, proxy tooa eski sistem gördüğünüzde, bu özellikle yararlı olacaktır [istekleri ve yanıtları proxy'leri değiştirme](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span><span class="sxs-lookup"><span data-stu-id="c4e22-217">This is particularly useful when proxying tooa legacy system, where you might need toomodify headers, query parameters, etc. toolearn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span></span>

<span data-ttu-id="c4e22-218">Arama hello tarafından sahte API'nizi test `/api/users/{username}` bir tarayıcı veya sık kullandığınız REST istemcisinden kullanarak uç nokta.</span><span class="sxs-lookup"><span data-stu-id="c4e22-218">Test your mock API by calling hello `/api/users/{username}` endpoint using a browser or your favorite REST client.</span></span> <span data-ttu-id="c4e22-219">Emin tooreplace olması _{username}_ olan bir kullanıcı adı temsil eden bir dize değeri.</span><span class="sxs-lookup"><span data-stu-id="c4e22-219">Be sure tooreplace _{username}_ with a string value representing a username.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4e22-220">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c4e22-220">Next steps</span></span>

<span data-ttu-id="c4e22-221">Bu öğreticide, nasıl öğrenilen toobuild ve Azure işlevleri bir API özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4e22-221">In this tutorial, you learned how toobuild and customize an API on Azure Functions.</span></span> <span data-ttu-id="c4e22-222">Ayrıca, nasıl toobring dahil olmak üzere çok sayıda API, birlikte birleşik bir API yüzeyi olarak mocks öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="c4e22-222">You also learned how toobring multiple APIs, including mocks, together as a unified API surface.</span></span> <span data-ttu-id="c4e22-223">Tüm hello sunucusuz çalışırken Azure işlevleri tarafından sağlanan modeline işlem, bu teknikler toobuild API'ler herhangi karmaşıklık çıkışı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4e22-223">You can use these techniques toobuild out APIs of any complexity, all while running on hello serverless compute model provided by Azure Functions.</span></span>

<span data-ttu-id="c4e22-224">Daha fazla API'nizi geliştirdikçe hello aşağıdaki başvurular yararlı olabilir:</span><span class="sxs-lookup"><span data-stu-id="c4e22-224">hello following references may be helpful as you develop your API further:</span></span>

- [<span data-ttu-id="c4e22-225">Azure işlevleri HTTP ve Web kancası bağlamaları</span><span class="sxs-lookup"><span data-stu-id="c4e22-225">Azure Functions HTTP and webhook bindings</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- <span data-ttu-id="c4e22-226">[Azure işlevleri proxy'leri (Önizleme) çalışmaya]</span><span class="sxs-lookup"><span data-stu-id="c4e22-226">[Working with Azure Functions Proxies (preview)]</span></span>
- [<span data-ttu-id="c4e22-227">Azure işlevleri API (Önizleme) belgeleme</span><span class="sxs-lookup"><span data-stu-id="c4e22-227">Documenting an Azure Functions API (preview)</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[Azure işlevleri proxy'leri (Önizleme) çalışmaya]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
