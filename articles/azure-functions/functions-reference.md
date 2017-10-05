---
title: "Azure işlevleri geliştirmek için Kılavuzu | Microsoft Docs"
description: "Azure işlevleri kavramlarını ve işlevlerinin Azure, tüm programlama dilleri ve bağlamaları geliştirmek için gereken teknikleri öğrenin."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "Geliştirici Kılavuzu, azure işlevleri, İşlevler, olay işleme, Web kancalarını, dinamik işlem, sunucusuz mimarisi"
ms.assetid: d8efe41a-bef8-4167-ba97-f3e016fcd39e
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: chrande
ms.openlocfilehash: 879be48150cfe13e31064475aa637f13f5f5f9d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-developers-guide"></a><span data-ttu-id="aacb9-104">Azure işlevleri Geliştirici Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="aacb9-104">Azure Functions developers guide</span></span>
<span data-ttu-id="aacb9-105">Azure işlevleri, belirli işlevleri birkaç temel teknik kavramlar ve bileşenler, dil veya kullandığınız bağlama bağımsız olarak paylaşın.</span><span class="sxs-lookup"><span data-stu-id="aacb9-105">In Azure Functions, specific functions share a few core technical concepts and components, regardless of the language or binding you use.</span></span> <span data-ttu-id="aacb9-106">Belirtilen dil ya da bağlama belirli Ayrıntılar öğrenme moduna geçmek önce bunların tümüne uygulanır Bu genel bakışta aracılığıyla okuduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="aacb9-106">Before you jump into learning details specific to a given language or binding, be sure to read through this overview that applies to all of them.</span></span>

<span data-ttu-id="aacb9-107">Bu makalede, zaten okuduğunuz varsayılır [Azure işlevlerine genel bakış](functions-overview.md) ve bilginiz [WebJobs SDK'sı kavramları Tetikleyicileri ve bağlamaları JobHost çalışma zamanı gibi](../app-service-web/websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="aacb9-107">This article assumes that you've already read the [Azure Functions overview](functions-overview.md) and are familiar with [WebJobs SDK concepts such as triggers, bindings, and the JobHost runtime](../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span> <span data-ttu-id="aacb9-108">Azure işlevleri WebJobs SDK dayanır.</span><span class="sxs-lookup"><span data-stu-id="aacb9-108">Azure Functions is based on the WebJobs SDK.</span></span> 

## <a name="function-code"></a><span data-ttu-id="aacb9-109">İşlev kodu</span><span class="sxs-lookup"><span data-stu-id="aacb9-109">Function code</span></span>
<span data-ttu-id="aacb9-110">A *işlevi* Azure işlevlerinde birincil kavramdır.</span><span class="sxs-lookup"><span data-stu-id="aacb9-110">A *function* is the primary concept in Azure Functions.</span></span> <span data-ttu-id="aacb9-111">Kod bir işlev için tercih ettiğiniz dilde yazmak ve kod ve yapılandırma dosyaları aynı klasöre kaydedin.</span><span class="sxs-lookup"><span data-stu-id="aacb9-111">You write code for a function in a language of your choice and save the code and configuration files in the same folder.</span></span> <span data-ttu-id="aacb9-112">Yapılandırma adlı `function.json`, JSON yapılandırma verilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="aacb9-112">The configuration is named `function.json`, which contains JSON configuration data.</span></span> <span data-ttu-id="aacb9-113">Çeşitli diller desteklenir ve her birinin bu dil için en iyi şekilde çalışması için en iyi duruma getirilmiş biraz farklı bir deneyimle vardır.</span><span class="sxs-lookup"><span data-stu-id="aacb9-113">Various languages are supported, and each one has a slightly different experience optimized to work best for that language.</span></span> 

<span data-ttu-id="aacb9-114">Function.json dosyası, işlev bağlamaları ve diğer yapılandırma ayarlarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="aacb9-114">The function.json file defines the function bindings and other configuration settings.</span></span> <span data-ttu-id="aacb9-115">Çalışma zamanı izlenecek olaylar belirlemek için bu dosyaya ve verilerini geçirin ve işlev yürütülmesini veri dönmek nasıl kullanır.</span><span class="sxs-lookup"><span data-stu-id="aacb9-115">The runtime uses this file to determine the events to monitor and how to pass data into and return data from function execution.</span></span> <span data-ttu-id="aacb9-116">Function.json dosyası örneği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="aacb9-116">The following is an example function.json file.</span></span>

```json
{
    "disabled":false,
    "bindings":[
        // ... bindings here
        {
            "type": "bindingType",
            "direction": "in",
            "name": "myParamName",
            // ... more depending on binding
        }
    ]
}
```

<span data-ttu-id="aacb9-117">Ayarlama `disabled` özelliğine `true` işlevi çalıştırılmasını engellemek için.</span><span class="sxs-lookup"><span data-stu-id="aacb9-117">Set the `disabled` property to `true` to prevent the function from being executed.</span></span>

<span data-ttu-id="aacb9-118">`bindings` Özelliktir burada Tetikleyicileri ve bağlamaları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="aacb9-118">The `bindings` property is where you configure both triggers and bindings.</span></span> <span data-ttu-id="aacb9-119">Her bağlama birkaç genel ayarları ve belirli bir bağlama türüne özgü bazı ayarlar paylaşır.</span><span class="sxs-lookup"><span data-stu-id="aacb9-119">Each binding shares a few common settings and some settings, which are specific to a particular type of binding.</span></span> <span data-ttu-id="aacb9-120">Her bağlama aşağıdaki ayarları gerektirir:</span><span class="sxs-lookup"><span data-stu-id="aacb9-120">Every binding requires the following settings:</span></span>

| <span data-ttu-id="aacb9-121">Özellik</span><span class="sxs-lookup"><span data-stu-id="aacb9-121">Property</span></span> | <span data-ttu-id="aacb9-122">Değerleri/türleri</span><span class="sxs-lookup"><span data-stu-id="aacb9-122">Values/Types</span></span> | <span data-ttu-id="aacb9-123">Yorumlar</span><span class="sxs-lookup"><span data-stu-id="aacb9-123">Comments</span></span> |
| --- | --- | --- |
| `type` |<span data-ttu-id="aacb9-124">Dize</span><span class="sxs-lookup"><span data-stu-id="aacb9-124">string</span></span> |<span data-ttu-id="aacb9-125">Bağlama türü.</span><span class="sxs-lookup"><span data-stu-id="aacb9-125">Binding type.</span></span> <span data-ttu-id="aacb9-126">Örneğin, `queueTrigger`.</span><span class="sxs-lookup"><span data-stu-id="aacb9-126">For example, `queueTrigger`.</span></span> |
| `direction` |<span data-ttu-id="aacb9-127">'in', 'out'</span><span class="sxs-lookup"><span data-stu-id="aacb9-127">'in', 'out'</span></span> |<span data-ttu-id="aacb9-128">Bağlama işlevdeki veri alma veya işlevinden veri göndermek için olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="aacb9-128">Indicates whether the binding is for receiving data into the function or sending data from the function.</span></span> |
| `name` |<span data-ttu-id="aacb9-129">Dize</span><span class="sxs-lookup"><span data-stu-id="aacb9-129">string</span></span> |<span data-ttu-id="aacb9-130">Bağlı veri işlevinde için kullanılan ad.</span><span class="sxs-lookup"><span data-stu-id="aacb9-130">The name that is used for the bound data in the function.</span></span> <span data-ttu-id="aacb9-131">C# ' ta bir bağımsız değişken adı budur; JavaScript için bir anahtar/değer listesinde anahtardır.</span><span class="sxs-lookup"><span data-stu-id="aacb9-131">For C#, this is an argument name; for JavaScript, it's the key in a key/value list.</span></span> |

## <a name="function-app"></a><span data-ttu-id="aacb9-132">İşlev uygulaması</span><span class="sxs-lookup"><span data-stu-id="aacb9-132">Function app</span></span>
<span data-ttu-id="aacb9-133">Bir işlev uygulaması birlikte Azure App Service tarafından yönetilen bir veya daha fazla tekil işlevler oluşur.</span><span class="sxs-lookup"><span data-stu-id="aacb9-133">A function app is comprised of one or more individual functions that are managed together by Azure App Service.</span></span> <span data-ttu-id="aacb9-134">Bir işlev uygulaması işlevlerde tümünün aynı fiyatlandırma planı, sürekli dağıtımı ve çalışma zamanı sürümü paylaşır.</span><span class="sxs-lookup"><span data-stu-id="aacb9-134">All of the functions in a function app share the same pricing plan, continuous deployment and runtime version.</span></span> <span data-ttu-id="aacb9-135">Çeşitli dillerde yazılmış işlevleri tüm aynı işlev uygulaması paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aacb9-135">Functions written in multiple languages can all share the same function app.</span></span> <span data-ttu-id="aacb9-136">Bir işlev uygulaması düzenlemek ve topluca işlevlerinizi yönetmek için bir yol olarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="aacb9-136">Think of a function app as a way to organize and collectively manage your functions.</span></span> 

## <a name="runtime-script-host-and-web-host"></a><span data-ttu-id="aacb9-137">Çalışma zamanı (komut dosyası ana bilgisayarı ve web ana bilgisayarı)</span><span class="sxs-lookup"><span data-stu-id="aacb9-137">Runtime (script host and web host)</span></span>
<span data-ttu-id="aacb9-138">Çalışma zamanı ya da komut dosyası ana bilgisayarı, olaylarını dinler, toplar ve verileri gönderir ve sonuçta kodunuzun çalıştığı temel Web işleri SDK'si ana bilgisayardır.</span><span class="sxs-lookup"><span data-stu-id="aacb9-138">The runtime, or script host, is the underlying WebJobs SDK host that listens for events, gathers and sends data, and ultimately runs your code.</span></span> 

<span data-ttu-id="aacb9-139">HTTP Tetikleyicileri kolaylaştırmak için de bulunmaktadır komut dosyası ana bilgisayarı üretim senaryolarında önünde sit için tasarlanmış bir web ana bilgisayarı.</span><span class="sxs-lookup"><span data-stu-id="aacb9-139">To facilitate HTTP triggers, there is also a web host that is designed to sit in front of the script host in production scenarios.</span></span> <span data-ttu-id="aacb9-140">İki ana sahip komut dosyası ana bilgisayarı Önden ayırmaya yardımcı web ana bilgisayar tarafından yönetilen trafiği sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="aacb9-140">Having two hosts helps to isolate the script host from the front end traffic managed by the web host.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="aacb9-141">Klasör yapısı</span><span class="sxs-lookup"><span data-stu-id="aacb9-141">Folder Structure</span></span>
[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

<span data-ttu-id="aacb9-142">Azure App Service'te bir işlev uygulaması için işlevleri dağıtmak için bir proje ayarlama, bu klasör yapısı, site kodu olarak davranabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aacb9-142">When setting-up a project for deploying functions to a function app in Azure App Service, you can treat this folder structure as your site code.</span></span> <span data-ttu-id="aacb9-143">Sürekli tümleştirme ve dağıtım gibi mevcut araçlar kullanabilir veya özel dağıtım yapmak için komut dosyaları zaman paket yükleme dağıtmak veya transpilation kod.</span><span class="sxs-lookup"><span data-stu-id="aacb9-143">You can use existing tools like continuous integration and deployment, or custom deployment scripts for doing deploy time package installation or code transpilation.</span></span>

> [!NOTE]
> <span data-ttu-id="aacb9-144">Dağıtmak emin olun, `host.json` dosya ve klasörleri doğrudan işlev `wwwroot` klasör.</span><span class="sxs-lookup"><span data-stu-id="aacb9-144">Make sure to deploy your `host.json` file and function folders directly to the `wwwroot` folder.</span></span> <span data-ttu-id="aacb9-145">İçermeyen `wwwroot` dağıtımlarınızı klasöründe.</span><span class="sxs-lookup"><span data-stu-id="aacb9-145">Do not include the `wwwroot` folder in your deployments.</span></span> <span data-ttu-id="aacb9-146">Aksi takdirde, şunun `wwwroot\wwwroot` klasörler.</span><span class="sxs-lookup"><span data-stu-id="aacb9-146">Otherwise, you end up with `wwwroot\wwwroot` folders.</span></span> 
> 
> 

## <span data-ttu-id="aacb9-147"><a id="fileupdate"></a>İşlev uygulama dosyaları güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="aacb9-147"><a id="fileupdate"></a> How to update function app files</span></span>
<span data-ttu-id="aacb9-148">Azure portalda yerleşik işlevi Düzenleyicisi güncelleştirmenizi sağlayan *function.json* dosyası ve bir işlev için kod dosyası.</span><span class="sxs-lookup"><span data-stu-id="aacb9-148">The function editor built into the Azure portal lets you update the *function.json* file and the code file for a function.</span></span> <span data-ttu-id="aacb9-149">Karşıya yükleme veya güncelleştirme gibi diğer dosyaları *package.json* veya *project.json* veya bağımlılıkları, zorunda diğer dağıtım yöntemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aacb9-149">To upload or update other files such as *package.json* or *project.json* or dependencies, you have to use other deployment methods.</span></span>

<span data-ttu-id="aacb9-150">İşlev uygulamalarının, uygulama hizmeti, bu nedenle tüm yerleşiktir [standart web uygulamaları için dağıtım seçenekleri](../app-service-web/web-sites-deploy.md) de işlevi uygulamaları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="aacb9-150">Function apps are built on App Service, so all the [deployment options available to standard web apps](../app-service-web/web-sites-deploy.md) are also available for function apps.</span></span> <span data-ttu-id="aacb9-151">Karşıya yükleme veya işlevi uygulama dosyalarını güncelleştirmek için kullanabileceğiniz bazı yöntemler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="aacb9-151">Here are some methods you can use to upload or update function app files.</span></span> 

#### <a name="to-use-app-service-editor"></a><span data-ttu-id="aacb9-152">Uygulama hizmeti Düzenleyicisi'ni kullanmak için</span><span class="sxs-lookup"><span data-stu-id="aacb9-152">To use App Service Editor</span></span>
1. <span data-ttu-id="aacb9-153">Azure işlevleri Portalı'nda tıklatın **işlev uygulaması ayarları**.</span><span class="sxs-lookup"><span data-stu-id="aacb9-153">In the Azure Functions portal, click **Function app settings**.</span></span>
2. <span data-ttu-id="aacb9-154">İçinde **Gelişmiş ayarları** 'yi tıklatın **uygulama hizmeti ayarlarına Git**.</span><span class="sxs-lookup"><span data-stu-id="aacb9-154">In the **Advanced Settings** section, click **Go to App Service Settings**.</span></span>
3. <span data-ttu-id="aacb9-155">Tıklatın **App Service Düzenleyicisi** uygulama menüsünden NAV altında **geliştirme araçları**.</span><span class="sxs-lookup"><span data-stu-id="aacb9-155">Click **App Service Editor** in App Menu Nav under **DEVELOPMENT TOOLS**.</span></span>
4. <span data-ttu-id="aacb9-156">tıklatın **Git**.</span><span class="sxs-lookup"><span data-stu-id="aacb9-156">click **Go**.</span></span>
   
   <span data-ttu-id="aacb9-157">Uygulama hizmeti Düzenleyicisi yüklendikten sonra göreceğiniz *host.json* altındaki dosya ve işlev klasörleri *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="aacb9-157">After App Service Editor loads, you'll see the *host.json* file and function folders under *wwwroot*.</span></span> 
5. <span data-ttu-id="aacb9-158">Bunları, düzenlemek veya sürükleyip dosyaları karşıya yüklemek için geliştirme makinenizden dosyalarını açın.</span><span class="sxs-lookup"><span data-stu-id="aacb9-158">Open files to edit them, or drag and drop from your development machine to upload files.</span></span>

#### <a name="to-use-the-function-apps-scm-kudu-endpoint"></a><span data-ttu-id="aacb9-159">İşlev uygulamanın SCM (Kudu) uç noktası kullanmak için</span><span class="sxs-lookup"><span data-stu-id="aacb9-159">To use the function app's SCM (Kudu) endpoint</span></span>
1. <span data-ttu-id="aacb9-160">Gidin: `https://<function_app_name>.scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="aacb9-160">Navigate to: `https://<function_app_name>.scm.azurewebsites.net`.</span></span>
2. <span data-ttu-id="aacb9-161">Tıklatın **Debug konsol > CMD**.</span><span class="sxs-lookup"><span data-stu-id="aacb9-161">Click **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="aacb9-162">Gidin `D:\home\site\wwwroot\` güncelleştirmek için *host.json* veya `D:\home\site\wwwroot\<function_name>` bir işlevin dosyaları güncelleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="aacb9-162">Navigate to `D:\home\site\wwwroot\` to update *host.json* or `D:\home\site\wwwroot\<function_name>` to update a function's files.</span></span>
4. <span data-ttu-id="aacb9-163">Sürükle ve bırak dosya kılavuzundaki uygun klasöre yüklemek istediğiniz bir dosya.</span><span class="sxs-lookup"><span data-stu-id="aacb9-163">Drag-and-drop a file you want to upload into the appropriate folder in the file grid.</span></span> <span data-ttu-id="aacb9-164">Dosya burada bırakamazsınız dosya kılavuzda iki alan vardır.</span><span class="sxs-lookup"><span data-stu-id="aacb9-164">There are two areas in the file grid where you can drop a file.</span></span> <span data-ttu-id="aacb9-165">İçin *.zip* dosyaları, etiketle bir kutu görünür "sürükleyin burada karşıya yükleyin ve sıkıştırmasını açın."</span><span class="sxs-lookup"><span data-stu-id="aacb9-165">For *.zip* files, a box appears with the label "Drag here to upload and unzip."</span></span> <span data-ttu-id="aacb9-166">Diğer dosya türlerinde, dosya kılavuzunda ancak "sıkıştırmasını" kutusunu dışında bırakın.</span><span class="sxs-lookup"><span data-stu-id="aacb9-166">For other file types, drop in the file grid but outside the "unzip" box.</span></span>

<!--NOTE: I've removed documentation on FTP, because it does not sync triggers on the consumption plan --DonnaM -->

#### <a name="to-use-continuous-deployment"></a><span data-ttu-id="aacb9-167">Sürekli dağıtım kullanmak için</span><span class="sxs-lookup"><span data-stu-id="aacb9-167">To use continuous deployment</span></span>
<span data-ttu-id="aacb9-168">Konudaki yönergeleri izleyerek [Azure işlevleri için sürekli dağıtım](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="aacb9-168">Follow the instructions in the topic [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span>

## <a name="parallel-execution"></a><span data-ttu-id="aacb9-169">Paralel yürütme</span><span class="sxs-lookup"><span data-stu-id="aacb9-169">Parallel execution</span></span>
<span data-ttu-id="aacb9-170">Birden çok tetikleyici olaylar tek iş parçacıklı işlevi çalışma zamanı bunları işleyebileceğinden daha hızlı gerçekleştiğinde, çalışma zamanı işlevinde birden çok kez paralel çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="aacb9-170">When multiple triggering events occur faster than a single-threaded function runtime can process them, the runtime may invoke the function multiple times in parallel.</span></span>  <span data-ttu-id="aacb9-171">Bir işlev uygulaması kullanıyorsanız [barındırma planı tüketim](functions-scale.md#how-the-consumption-plan-works), işlev uygulaması otomatik olarak ölçeğini.</span><span class="sxs-lookup"><span data-stu-id="aacb9-171">If a function app is using the [Consumption hosting plan](functions-scale.md#how-the-consumption-plan-works), the function app could scale out automatically.</span></span>  <span data-ttu-id="aacb9-172">Her bir işlev uygulaması örneği olup olmadığını barındırma planı veya bir normal tüketimi'de uygulama'yı çalıştıran [App Service barındırma planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), eşzamanlı işlev çağrılarını birden çok iş parçacığı kullanma paralel işlem.</span><span class="sxs-lookup"><span data-stu-id="aacb9-172">Each instance of the function app, whether the app runs on the Consumption hosting plan or a regular [App Service hosting plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), might process concurrent function invocations in parallel using multiple threads.</span></span>  <span data-ttu-id="aacb9-173">En fazla eşzamanlı işlev çağrılarını her işlevi app örneğindeki türü, işlev uygulaması içinde diğer işlevleri tarafından kullanılan kaynakları yanı sıra kullanılan tetikleyici göre değişir.</span><span class="sxs-lookup"><span data-stu-id="aacb9-173">The maximum number of concurrent function invocations in each function app instance varies based on the type of trigger being used as well as the resources used by other functions within the function app.</span></span>

## <a name="functions-runtime-versioning"></a><span data-ttu-id="aacb9-174">İşlevler çalışma zamanı sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="aacb9-174">Functions runtime versioning</span></span>

<span data-ttu-id="aacb9-175">Çalışma zamanı işlevleri kullanarak sürümünü yapılandırabilirsiniz `FUNCTIONS_EXTENSION_VERSION` uygulama ayarı.</span><span class="sxs-lookup"><span data-stu-id="aacb9-175">You can configure the version of the Functions runtime using the `FUNCTIONS_EXTENSION_VERSION` app setting.</span></span> <span data-ttu-id="aacb9-176">Örneğin, "~ 1" değeri, işlev uygulaması kendi ana sürüm 1 kullanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="aacb9-176">For example, the value "~1" indicates that your Function App will use 1 as its major version.</span></span> <span data-ttu-id="aacb9-177">İşlev uygulamalarının en yeni her ikincil sürüme yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="aacb9-177">Function Apps are upgraded to each new minor version as they are released.</span></span> <span data-ttu-id="aacb9-178">İşlev uygulamanızda'nün tam sürümünü görüntüleyebilirsiniz **ayarları** Azure Portalı'nda sekmesi.</span><span class="sxs-lookup"><span data-stu-id="aacb9-178">You can view the exact version of your Function App in the **Settings** tab in the Azure Portal.</span></span>

## <a name="repositories"></a><span data-ttu-id="aacb9-179">Depolar</span><span class="sxs-lookup"><span data-stu-id="aacb9-179">Repositories</span></span>
<span data-ttu-id="aacb9-180">Azure işlevleri için kod açık bir kaynaktır ve GitHub depolarının depolanır:</span><span class="sxs-lookup"><span data-stu-id="aacb9-180">The code for Azure Functions is open source and stored in GitHub repositories:</span></span>

* [<span data-ttu-id="aacb9-181">Azure işlevleri çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="aacb9-181">Azure Functions runtime</span></span>](https://github.com/Azure/azure-webjobs-sdk-script/)
* [<span data-ttu-id="aacb9-182">Azure işlevleri portalına</span><span class="sxs-lookup"><span data-stu-id="aacb9-182">Azure Functions portal</span></span>](https://github.com/projectkudu/AzureFunctionsPortal)
* [<span data-ttu-id="aacb9-183">Azure işlevleri şablonları</span><span class="sxs-lookup"><span data-stu-id="aacb9-183">Azure Functions templates</span></span>](https://github.com/Azure/azure-webjobs-sdk-templates/)
* [<span data-ttu-id="aacb9-184">Azure Web işleri SDK'si</span><span class="sxs-lookup"><span data-stu-id="aacb9-184">Azure WebJobs SDK</span></span>](https://github.com/Azure/azure-webjobs-sdk/)
* [<span data-ttu-id="aacb9-185">Azure Web işleri SDK'si uzantıları</span><span class="sxs-lookup"><span data-stu-id="aacb9-185">Azure WebJobs SDK Extensions</span></span>](https://github.com/Azure/azure-webjobs-sdk-extensions/)

## <a name="bindings"></a><span data-ttu-id="aacb9-186">Bağlamalar</span><span class="sxs-lookup"><span data-stu-id="aacb9-186">Bindings</span></span>
<span data-ttu-id="aacb9-187">Aşağıda, tüm desteklenen bağlamaları tablosu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="aacb9-187">Here is a table of all supported bindings.</span></span>

[!INCLUDE [dynamic compute](../../includes/functions-bindings.md)]

## <a name="reporting-issues"></a><span data-ttu-id="aacb9-188">Raporlama konuları</span><span class="sxs-lookup"><span data-stu-id="aacb9-188">Reporting Issues</span></span>
[!INCLUDE [Reporting Issues](../../includes/functions-reporting-issues.md)]

## <a name="next-steps"></a><span data-ttu-id="aacb9-189">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aacb9-189">Next steps</span></span>
<span data-ttu-id="aacb9-190">Daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="aacb9-190">For more information, see the following resources:</span></span>

* [<span data-ttu-id="aacb9-191">Azure İşlevleri için En İyi Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="aacb9-191">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="aacb9-192">Azure işlevleri C# Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="aacb9-192">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="aacb9-193">Azure işlevleri F # Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="aacb9-193">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="aacb9-194">Azure işlevleri NodeJS Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="aacb9-194">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="aacb9-195">Azure işlevleri Tetikleyicileri ve bağlamaları</span><span class="sxs-lookup"><span data-stu-id="aacb9-195">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* <span data-ttu-id="aacb9-196">[Azure işlevleri: Gezisine](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) Azure App Service ekip blogunda.</span><span class="sxs-lookup"><span data-stu-id="aacb9-196">[Azure Functions: The Journey](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) on the Azure App Service team blog.</span></span> <span data-ttu-id="aacb9-197">Azure işlevlerinin nasıl geliştirilmiştir geçmişi.</span><span class="sxs-lookup"><span data-stu-id="aacb9-197">A history of how Azure Functions was developed.</span></span>

