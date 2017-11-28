---
title: "aaaBuild Azure hiper ölçekli uygulamada | Microsoft Docs"
description: "Nasıl toouse farklı Azure Hizmetleri toomaximize hello Azure ASP.NET uygulama performansını öğrenin."
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: erikre
editor: 
ms.assetid: a4d49ac7-0f97-4997-84c5-cdb9c4465757
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/23/2017
ms.author: cephalin
ms.openlocfilehash: 7952647b49a82c286c6a737eb41a7f23a13fd75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="632af-103">Azure'da hiper ölçekli web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="632af-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="632af-104">Bu öğretici, nasıl ASP.NET web uygulamasını Azure toomaximize kullanıcı çıkışı tooscale istekleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="632af-104">This tutorial shows you how tooscale out an ASP.NET web app in Azure toomaximize user requests.</span></span>

<span data-ttu-id="632af-105">Bu öğreticiye başlamadan önce emin olun [Azure CLI yüklü hello](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) makinenizde.</span><span class="sxs-lookup"><span data-stu-id="632af-105">Before starting this tutorial, ensure that [hello Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="632af-106">Ayrıca, gereksinim duyduğunuz [Visual Studio](https://www.visualstudio.com/vs/) , LocalMachine toorun hello örnek uygulamanızın üzerinde.</span><span class="sxs-lookup"><span data-stu-id="632af-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine toorun hello sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="632af-107">1. adım - Get örnek uygulama</span><span class="sxs-lookup"><span data-stu-id="632af-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="632af-108">Bu adımda, hello yerel ASP.NET projesi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="632af-108">In this step, you set up hello local ASP.NET project.</span></span>

### <a name="clone-hello-application-repository"></a><span data-ttu-id="632af-109">Kopya hello uygulama havuzu</span><span class="sxs-lookup"><span data-stu-id="632af-109">Clone hello application repository</span></span>

<span data-ttu-id="632af-110">Tercih ettiğiniz komut satırı Terminalini açın hello ve `CD` tooa çalışma dizini.</span><span class="sxs-lookup"><span data-stu-id="632af-110">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span> <span data-ttu-id="632af-111">Ardından, çalışma hello aşağıdaki tooclone Merhaba örnek uygulaması komutları.</span><span class="sxs-lookup"><span data-stu-id="632af-111">Then, run hello following commands tooclone hello sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a><span data-ttu-id="632af-112">Visual Studio'da Hello örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="632af-112">Run hello sample application in Visual Studio</span></span>

<span data-ttu-id="632af-113">Merhaba çözümü Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="632af-113">Open hello solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="632af-114">Tür `F5` toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="632af-114">Type `F5` toorun hello application.</span></span>

<span data-ttu-id="632af-115">Bu örnek ASP.NET web uygulaması hello varsayılan şablondan gelir ve kullanıcı oturumlarını ve kullandığı hello çıktı önbelleği devam ettirir.</span><span class="sxs-lookup"><span data-stu-id="632af-115">This sample ASP.NET web application comes from hello default template, and persists user sessions and uses hello output cache.</span></span> <span data-ttu-id="632af-116">Bir göz atalım `HighScaleApp\Controllers\HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="632af-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="632af-117">Merhaba `Index()` yöntemi, bir veri toohello oturum ekler.</span><span class="sxs-lookup"><span data-stu-id="632af-117">hello `Index()` method adds a piece of data toohello session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="632af-118">Ve hello `About()` ve `Contact()` yöntemlerini çıkışı önbelleğe.</span><span class="sxs-lookup"><span data-stu-id="632af-118">And hello `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a><span data-ttu-id="632af-119">2. adım - tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="632af-119">Step 2 - Deploy tooAzure</span></span>
<span data-ttu-id="632af-120">Bu adımda, Azure web uygulaması oluşturun ve örnek ASP.NET uygulama tooit dağıtın.</span><span class="sxs-lookup"><span data-stu-id="632af-120">In this step, you create an Azure web app and deploy your sample ASP.NET application tooit.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="632af-121">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="632af-121">Create a resource group</span></span>   
<span data-ttu-id="632af-122">Kullanım [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) toocreate bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) hello Batı Avrupa bölgede.</span><span class="sxs-lookup"><span data-stu-id="632af-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) toocreate a [resource group](../azure-resource-manager/resource-group-overview.md) in hello West Europe region.</span></span> <span data-ttu-id="632af-123">Bir kaynak grubu burada tüm yerleştirdiğiniz olduğu gibi hello web app ve herhangi bir SQL veritabanı arka uç toomanage birlikte, istediğiniz Azure kaynakları hello.</span><span class="sxs-lookup"><span data-stu-id="632af-123">A resource group is where you put all hello Azure resources that you want toomanage together, such as hello web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="632af-124">toosee hangi olası değerler için kullanabilmeniz için `---location`, hello kullan [az appservice listesi-konumları](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) komutu.</span><span class="sxs-lookup"><span data-stu-id="632af-124">toosee what possible values you can use for `---location`, use hello [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="632af-125">App Service planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="632af-125">Create an App Service plan</span></span>
<span data-ttu-id="632af-126">Kullanım [az uygulama hizmeti planı oluşturma](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate "B1" [uygulama hizmeti planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="632af-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="632af-127">Bir uygulama hizmeti planı herhangi bir sayıda tooscale yedeklemek istediğiniz veya birlikte üzerinden aynı hello uygulamalar dahil edebileceğiniz bir ölçek birimi olan uygulama hizmeti altyapı.</span><span class="sxs-lookup"><span data-stu-id="632af-127">An App Service plan is a scale unit, which can include any number of apps that you want tooscale up or out together over hello same App Service infrastructure.</span></span> <span data-ttu-id="632af-128">Her plan da atanmış bir [fiyatlandırma katmanı](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="632af-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="632af-129">Daha yüksek katmanları daha iyi donanım ve daha fazla genişleme örnekleri gibi daha fazla özellik içerir.</span><span class="sxs-lookup"><span data-stu-id="632af-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="632af-130">Bu öğretici için toothree örnekleri genişleme sağlayan hello en az katman B1 olur.</span><span class="sxs-lookup"><span data-stu-id="632af-130">For this tutorial, B1 is hello minimum tier that enables scale out toothree instances.</span></span> <span data-ttu-id="632af-131">Her zaman yukarı veya aşağı daha sonra çalıştırarak fiyatlandırma katmanı hello uygulamanızı taşıyabilirsiniz [az uygulama hizmeti planı güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span><span class="sxs-lookup"><span data-stu-id="632af-131">You can always move your app up or down hello pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="632af-132">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="632af-132">Create a web app</span></span>
<span data-ttu-id="632af-133">Kullanım [az appservice web oluşturmak](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate benzersiz bir ada sahip bir web uygulaması olarak `$appName`.</span><span class="sxs-lookup"><span data-stu-id="632af-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="632af-134">Dağıtım kimlik bilgilerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="632af-134">Set deployment credentials</span></span>
<span data-ttu-id="632af-135">Kullanım [az appservice web dağıtım kullanıcısı ayarlanmadı](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset hesap düzeyinde dağıtımınız için uygulama hizmeti kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="632af-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="632af-136">Git dağıtımı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="632af-136">Configure Git deployment</span></span>
<span data-ttu-id="632af-137">Kullanım [az appservice web kaynak denetimi config-yerel-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure yerel Git dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="632af-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="632af-138">Bu komut, hello şu şekilde görünen bir çıktı sunar:</span><span class="sxs-lookup"><span data-stu-id="632af-138">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="632af-139">Kullanım Merhaba, Git URL'si tooconfigure uzak döndürdü.</span><span class="sxs-lookup"><span data-stu-id="632af-139">Use hello returned URL tooconfigure your Git remote.</span></span> <span data-ttu-id="632af-140">Merhaba aşağıdaki komut çıktısı örneğinde önceki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="632af-140">hello following command uses hello preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a><span data-ttu-id="632af-141">Merhaba örnek uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="632af-141">Deploy hello sample application</span></span>
<span data-ttu-id="632af-142">Örnek uygulamanız şimdi hazır toodeploy şunlardır.</span><span class="sxs-lookup"><span data-stu-id="632af-142">You are now ready toodeploy your sample application.</span></span> <span data-ttu-id="632af-143">`git push` öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="632af-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="632af-144">Parola istendiğinde, ne zaman çalıştırıldığı belirtilen hello parola kullanmak `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="632af-144">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-tooazure-web-app"></a><span data-ttu-id="632af-145">TooAzure web uygulaması Gözat</span><span class="sxs-lookup"><span data-stu-id="632af-145">Browse tooAzure web app</span></span>
<span data-ttu-id="632af-146">Kullanım [az appservice web Gözat](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee uygulamanızı Azure üzerinde çalışırken bu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="632af-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a><span data-ttu-id="632af-147">3. adım - tooRedis Bağlan</span><span class="sxs-lookup"><span data-stu-id="632af-147">Step 3 - Connect tooRedis</span></span>
<span data-ttu-id="632af-148">Bu adımda, Azure Redis önbelleği dış, birlikte bulunan önbellek tooyour Azure web uygulaması ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="632af-148">In this step, you set up Azure Redis Cache as an external, colocated cache tooyour Azure web app.</span></span> <span data-ttu-id="632af-149">Sayfa çıktısının Redis toocache hızlı bir şekilde kullanabilirler.</span><span class="sxs-lookup"><span data-stu-id="632af-149">You can quickly utilize Redis toocache your page output.</span></span> <span data-ttu-id="632af-150">Web uygulamalarınızı daha sonra ölçeklendirdiğinizde Ayrıca, Redis kalıcı yardımcı olan birden çok kullanıcı oturumlarında örnekleri güvenilir.</span><span class="sxs-lookup"><span data-stu-id="632af-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="632af-151">Azure Redis Cache oluşturma</span><span class="sxs-lookup"><span data-stu-id="632af-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="632af-152">Kullanım [az redis oluşturma](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate bir Azure Redis önbelleği ve JSON hello çıkış.</span><span class="sxs-lookup"><span data-stu-id="632af-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate an Azure Redis Cache and save hello JSON output.</span></span> <span data-ttu-id="632af-153">Benzersiz bir ad kullanmak `$cacheName`.</span><span class="sxs-lookup"><span data-stu-id="632af-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a><span data-ttu-id="632af-154">Merhaba uygulama toouse Redis yapılandırın</span><span class="sxs-lookup"><span data-stu-id="632af-154">Configure hello application toouse Redis</span></span>
<span data-ttu-id="632af-155">Önbelleğinizi Hello bağlantı dizesi biçimi.</span><span class="sxs-lookup"><span data-stu-id="632af-155">Format hello connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="632af-156">Merhaba ikinci satırı şuna benzer bir çıktı vermeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="632af-156">hello second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="632af-157">Visual Studio'da adlı proje kök web yapılandırma dosyası oluşturma `redis.config` ve Yapıştır hello aşağıdaki kod içine.</span><span class="sxs-lookup"><span data-stu-id="632af-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste hello following code into it.</span></span> <span data-ttu-id="632af-158">İçinde `value`, hello PowerShell çıkış hello bağlantı dizesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="632af-158">In `value`, use hello connection string from hello PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="632af-159">Merhaba bakarsanız `.gitignore` dosya Git deponuzu bu dosyayı kaynak denetiminden dışlandı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="632af-159">If you look at hello `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="632af-160">Bu şekilde, hassas bilgilerinizi güvenli tutulur.</span><span class="sxs-lookup"><span data-stu-id="632af-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="632af-161">Açık `Web.config`.</span><span class="sxs-lookup"><span data-stu-id="632af-161">Open `Web.config`.</span></span> <span data-ttu-id="632af-162">Bildirim hello `<appSettings file="redis.config">` oluşturduğunuz hello ayarını alır öğesi `redis.config`.</span><span class="sxs-lookup"><span data-stu-id="632af-162">Notice hello `<appSettings file="redis.config">` element, which gets hello setting you created in `redis.config`.</span></span> 

<span data-ttu-id="632af-163">Merhaba geçersiz kılınan bulma içeren bölümü `<sessionState>` ve `<caching>`.</span><span class="sxs-lookup"><span data-stu-id="632af-163">Find hello commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="632af-164">Bu bölümde açıklamadan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="632af-164">Uncomment this section.</span></span>

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="632af-165">Bu kod hello Redis bağlantı dizesi için tanımladığınız görünür `RedisConnection`.</span><span class="sxs-lookup"><span data-stu-id="632af-165">This code looks for hello Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="632af-166">Uygulamanız artık Redis toomanage oturumlar ve önbelleğe alma kullanır.</span><span class="sxs-lookup"><span data-stu-id="632af-166">Your application now uses Redis toomanage sessions and caching.</span></span> <span data-ttu-id="632af-167">Tür `F5` toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="632af-167">Type `F5` toorun hello application.</span></span> <span data-ttu-id="632af-168">İsterseniz, şimdi toohello önbelleğe kaydedilen bir Redis yönetim istemci toovisualize hello veriler indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="632af-168">If you like, you can download a Redis management client toovisualize hello data that is now saved toohello cache.</span></span>

### <a name="configure-hello-connection-string-in-azure"></a><span data-ttu-id="632af-169">Azure'da Hello bağlantı dizesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="632af-169">Configure hello connection string in Azure</span></span>

<span data-ttu-id="632af-170">Azure'da, uygulama toowork için ihtiyacınız tooconfigure aynı Redis bağlantı dizesi, Azure web uygulamanızda hello.</span><span class="sxs-lookup"><span data-stu-id="632af-170">For your application toowork in Azure, you need tooconfigure hello same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="632af-171">Bu yana `redis.config` tutulmaz kaynak denetiminde değil dağıtılan tooAzure Git dağıtımı çalıştırdığınızda.</span><span class="sxs-lookup"><span data-stu-id="632af-171">Since `redis.config` is not maintained in source control, it is not deployed tooAzure when you run Git deployment.</span></span>

<span data-ttu-id="632af-172">Kullanım [az appservice web yapılandırma appsettings güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd hello bağlantı dizesi hello ile aynı adı (`RedisConnection`).</span><span class="sxs-lookup"><span data-stu-id="632af-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd hello connection string with hello same name (`RedisConnection`).</span></span>

<span data-ttu-id="632af-173">appSettings güncelleştirme--az appservice web yapılandırma ayarları "RedisConnection $connstring ="--$appName--kaynak-grubu myResourceGroup adı</span><span class="sxs-lookup"><span data-stu-id="632af-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="632af-174">Unutmayın `$connstring` Merhaba biçimlendirilmiş bağlantı dizesi içeriyor.</span><span class="sxs-lookup"><span data-stu-id="632af-174">Remember that `$connstring` contains hello formatted connection string.</span></span>

### <a name="redeploy-hello-application-tooazure"></a><span data-ttu-id="632af-175">Merhaba uygulama tooAzure yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="632af-175">Redeploy hello application tooAzure</span></span>
<span data-ttu-id="632af-176">Git komutları toopush değişiklikleri tooAzure kullanın</span><span class="sxs-lookup"><span data-stu-id="632af-176">Use Git commands toopush your changes tooAzure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="632af-177">Parola istendiğinde, ne zaman çalıştırıldığı belirtilen hello parola kullanmak `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="632af-177">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="632af-178">Toohello Azure web uygulaması Gözat</span><span class="sxs-lookup"><span data-stu-id="632af-178">Browse toohello Azure web app</span></span>
<span data-ttu-id="632af-179">Kullanım [az appservice web Gözat](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee hello değişiklikleri Canlı Azure'da.</span><span class="sxs-lookup"><span data-stu-id="632af-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee hello changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a><span data-ttu-id="632af-180">4. adım - ölçek toomultiple örnekleri</span><span class="sxs-lookup"><span data-stu-id="632af-180">Step 4 - Scale toomultiple instances</span></span>
<span data-ttu-id="632af-181">Hello uygulama hizmeti planı hello ölçek birimi, Azure web uygulamaları için değil.</span><span class="sxs-lookup"><span data-stu-id="632af-181">hello App Service plan is hello scale unit for your Azure web apps.</span></span> <span data-ttu-id="632af-182">tooscale web uygulamanızı çıkışı hello uygulama hizmeti planı ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="632af-182">tooscale out your web app, you scale hello App Service plan.</span></span>

<span data-ttu-id="632af-183">Kullanım [az uygulama hizmeti planı güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/plan#update) olan tooscale hello uygulama hizmeti planı toothree örnekleri, çıkışı hello fiyatlandırma katmanı hello B1 tarafından izin verilen maksimum sayıyı.</span><span class="sxs-lookup"><span data-stu-id="632af-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale out hello App Service plan toothree instances, which is hello maximum number allowed by hello B1 pricing tier.</span></span> <span data-ttu-id="632af-184">B1 fiyatlandırma katmanı hello önceki uygulama hizmeti planı oluştururken seçtiğiniz hello olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="632af-184">Remember that B1 is hello pricing tier that you chose when you created hello App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="632af-185">Adım 5 - ölçek coğrafi olarak</span><span class="sxs-lookup"><span data-stu-id="632af-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="632af-186">Coğrafi olarak ölçekleme hello Azure bulut birden çok bölgede uygulamanızı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="632af-186">When scaling geographically, you run your app in multiple regions of hello Azure cloud.</span></span> <span data-ttu-id="632af-187">Bu kurulum yük bakiyelerini Coğrafya hakkında daha fazla temel uygulamanızı ve uygulama daha yakından tooclient tarayıcılar koyarak hello yanıt süresini azaltır.</span><span class="sxs-lookup"><span data-stu-id="632af-187">This setup load-balances your app further based on geography and lowers hello response time by placing your app closer tooclient browsers.</span></span>

<span data-ttu-id="632af-188">Bu adımda, ASP.NET web uygulaması tooa ikinci bölgenizi ile ölçeklendirme [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="632af-188">In this step, you scale your ASP.NET web app tooa second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="632af-189">Hello adım Hello sonunda, Batı Avrupa (önceden oluşturulmuş) çalıştıran bir web uygulaması ve Güneydoğu Asya (henüz oluşturulmadı) çalıştıran bir web uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="632af-189">At hello end of hello step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="632af-190">Her iki uygulamalar aynı trafik Yöneticisi URL hello sunulacak.</span><span class="sxs-lookup"><span data-stu-id="632af-190">Both apps will be served from hello same Traffic Manager URL.</span></span>

### <a name="scale-up-hello-europe-app-toostandard-tier"></a><span data-ttu-id="632af-191">Avrupa uygulama tooStandard katmanı Hello ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="632af-191">Scale up hello Europe app tooStandard tier</span></span>
<span data-ttu-id="632af-192">App Service içinde Azure Traffic Manager ile tümleştirme hello standart fiyatlandırma katmanı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="632af-192">In App Service, integration with Azure Traffic Manager requires hello Standard pricing tier.</span></span> <span data-ttu-id="632af-193">Kullanım [az uygulama hizmeti planı güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale uygulama hizmeti planı tooS1 ayarlama.</span><span class="sxs-lookup"><span data-stu-id="632af-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale up your App Service plan tooS1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="632af-194">Traffic Manager profili oluşturma</span><span class="sxs-lookup"><span data-stu-id="632af-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="632af-195">Kullanım [az ağ trafik Yöneticisi profili oluştur](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate trafik Yöneticisi profili ve tooyour kaynak grubunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="632af-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate a Traffic Manager profile and add it tooyour resource group.</span></span> <span data-ttu-id="632af-196">Benzersiz bir DNS adı $dnsName kullanın.</span><span class="sxs-lookup"><span data-stu-id="632af-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="632af-197">`--routing-method Performance`belirleyen bu profili [kullanıcı trafiği toohello yakın endpoint yönlendirir](../traffic-manager/traffic-manager-routing-methods.md).</span><span class="sxs-lookup"><span data-stu-id="632af-197">`--routing-method Performance` specifies that this profile [routes user traffic toohello closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-hello-resource-id-of-hello-europe-app"></a><span data-ttu-id="632af-198">Merhaba kaynak hello Avrupa uygulama Kimliğini Al</span><span class="sxs-lookup"><span data-stu-id="632af-198">Get hello resource ID of hello Europe app</span></span>
<span data-ttu-id="632af-199">Kullanım [az appservice web Göster](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) , web uygulamanızın tooget hello kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="632af-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a><span data-ttu-id="632af-200">Trafik Yöneticisi uç noktası hello Avrupa uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="632af-200">Add a Traffic Manager endpoint for hello Europe app</span></span>
<span data-ttu-id="632af-201">Kullanmak [az ağ trafik Yöneticisi uç noktası oluşturma](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd bir uç nokta tooyour trafik Yöneticisi profili ve kullanım hello kaynak kimliği web uygulamanızın hello hedef.</span><span class="sxs-lookup"><span data-stu-id="632af-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd an endpoint tooyour Traffic Manager profile and use hello resource ID of your web app as hello target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a><span data-ttu-id="632af-202">Merhaba trafik Yöneticisi uç nokta URL'sini alma</span><span class="sxs-lookup"><span data-stu-id="632af-202">Get hello Traffic Manager endpoint URL</span></span>
<span data-ttu-id="632af-203">Traffic Manager profilinizin şimdi bu noktaları tooyour var olan web uygulamasının bir uç nokta vardır.</span><span class="sxs-lookup"><span data-stu-id="632af-203">Your Traffic Manager profile now has an endpoint that points tooyour existing web app.</span></span> <span data-ttu-id="632af-204">Kullanım [az ağ trafik Yöneticisi profili Göster](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget URL'sini.</span><span class="sxs-lookup"><span data-stu-id="632af-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="632af-205">Merhaba çıkış tarayıcınıza kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="632af-205">Copy hello output into your browser.</span></span> <span data-ttu-id="632af-206">Web uygulamanızı yeniden görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="632af-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="632af-207">Bir Azure Redis önbelleği Asya'da oluşturma</span><span class="sxs-lookup"><span data-stu-id="632af-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="632af-208">Şimdi, Azure web uygulaması toohello Güneydoğu Asya bölgenizi çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="632af-208">Now, you replicate your Azure web app toohello Southeast Asia region.</span></span> <span data-ttu-id="632af-209">toostart, kullanım [az redis oluşturma](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate bir ikinci Azure Redis Önbelleği'nde Güneydoğu Asya.</span><span class="sxs-lookup"><span data-stu-id="632af-209">toostart, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="632af-210">Bu önbellek Asya'da uygulamanızla birlikte bulunan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="632af-210">This cache needs toobe colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="632af-211">`--name $cacheName-asia`verir hello hello ile Merhaba Batı Avrupa önbelleği, önbellek hello adı `-asia` soneki.</span><span class="sxs-lookup"><span data-stu-id="632af-211">`--name $cacheName-asia` gives hello cache hello name of hello West Europe cache, with hello `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="632af-212">Asya'da bir uygulama hizmeti planı oluştur</span><span class="sxs-lookup"><span data-stu-id="632af-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="632af-213">Kullanım [az uygulama hizmeti planı oluşturma](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate ikinci bir uygulama hizmeti planı hello Güneydoğu Asya bölgesinde, hello kullanarak aynı S1 katmanı hello Batı Avrupa plan.</span><span class="sxs-lookup"><span data-stu-id="632af-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate a second App Service plan in hello Southeast Asia region, using hello same S1 tier as hello West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="632af-214">Asya'da bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="632af-214">Create a web app in Asia</span></span>
<span data-ttu-id="632af-215">Kullanım [az appservice web oluşturmak](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate ikinci bir web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="632af-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="632af-216">`--name $appName-asia`verir hello hello Batı Avrupa uygulamasının uygulama hello adı ile Merhaba `-asia` soneki.</span><span class="sxs-lookup"><span data-stu-id="632af-216">`--name $appName-asia` gives hello app hello name of hello West Europe app, with hello `-asia` suffix.</span></span>

### <a name="configure-hello-connection-string-for-redis"></a><span data-ttu-id="632af-217">Redis için Hello bağlantı dizesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="632af-217">Configure hello connection string for Redis</span></span>
<span data-ttu-id="632af-218">Kullanım [az appservice web yapılandırma appsettings güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) hello Güneydoğu Asya önbelleği için tooadd toohello web uygulaması hello bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="632af-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web app hello connection string for hello Southeast Asia cache.</span></span>

<span data-ttu-id="632af-219">appSettings güncelleştirme--az appservice web yapılandırma ayarları "RedisConnection = $($redis.hostname): $($redis.sslPort), parola = $($redis.accessKeys.primaryKey) ssl = True, abortConnect = False"--ad $appName-Asya--kaynak-grubu myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="632af-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-hello-asia-app"></a><span data-ttu-id="632af-220">Merhaba Asya uygulaması için Git dağıtımı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="632af-220">Configure Git deployment for hello Asia app.</span></span>
<span data-ttu-id="632af-221">Kullanım [az appservice web kaynak denetimi config-yerel-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure yerel Git dağıtımı hello ikinci web uygulaması için.</span><span class="sxs-lookup"><span data-stu-id="632af-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment for hello second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="632af-222">Bu komut, hello şu şekilde görünen bir çıktı sunar:</span><span class="sxs-lookup"><span data-stu-id="632af-222">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="632af-223">Kullanım hello ikinci Git URL'si tooconfigure yerel deponuza için Uzak döndürdü.</span><span class="sxs-lookup"><span data-stu-id="632af-223">Use hello returned URL tooconfigure a second Git remote for your local repository.</span></span> <span data-ttu-id="632af-224">Merhaba aşağıdaki komut çıktısı örneğinde önceki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="632af-224">hello following command uses hello preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="632af-225">Örnek uygulamanızı dağıtma</span><span class="sxs-lookup"><span data-stu-id="632af-225">Deploy your sample application</span></span>
<span data-ttu-id="632af-226">Çalıştırma `git push` toodeploy örnek uygulama toohello ikinci Git uzaktan.</span><span class="sxs-lookup"><span data-stu-id="632af-226">Run `git push` toodeploy your sample application toohello second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="632af-227">Parola istendiğinde, ne zaman çalıştırıldığı belirtilen hello parola kullanmak `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="632af-227">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-asia-app"></a><span data-ttu-id="632af-228">Toohello Asya uygulama Gözat</span><span class="sxs-lookup"><span data-stu-id="632af-228">Browse toohello Asia app</span></span>
<span data-ttu-id="632af-229">Kullanım [az appservice web Gözat](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) uygulamanızı Canlı Azure'da çalışan tooverify.</span><span class="sxs-lookup"><span data-stu-id="632af-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a><span data-ttu-id="632af-230">Merhaba kaynak hello Asya uygulama Kimliğini Al</span><span class="sxs-lookup"><span data-stu-id="632af-230">Get hello resource ID of hello Asia app</span></span>
<span data-ttu-id="632af-231">Kullanım [az appservice web Göster](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) web uygulamanızın Güneydoğu Asya tooget hello kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="632af-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a><span data-ttu-id="632af-232">Trafik Yöneticisi uç noktası hello Asya uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="632af-232">Add a Traffic Manager endpoint for hello Asia app</span></span>
<span data-ttu-id="632af-233">Kullanım [az ağ trafik Yöneticisi uç noktası oluşturma](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd ikinci bir uç nokta toohello trafik Yöneticisi profili.</span><span class="sxs-lookup"><span data-stu-id="632af-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd a second endpoint toohello Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a><span data-ttu-id="632af-234">Bölge tanımlayıcısı tooweb uygulamalar ekleme</span><span class="sxs-lookup"><span data-stu-id="632af-234">Add region identifier tooweb apps</span></span>
<span data-ttu-id="632af-235">Kullanım [az appservice web yapılandırma appsettings güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd bölgeye özgü ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="632af-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="632af-236">Uygulama kodunuz, bu uygulama ayarı zaten kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="632af-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="632af-237">Bir göz atalım `HighScaleApp\Views\Home\Index.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="632af-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="632af-238">Tamamlandı!</span><span class="sxs-lookup"><span data-stu-id="632af-238">Complete!</span></span>

<span data-ttu-id="632af-239">Şimdi, farklı coğrafi bölgelerde tarayıcılardan Traffic Manager profilinizin tooaccess hello URL'yi deneyin.</span><span class="sxs-lookup"><span data-stu-id="632af-239">Now, try tooaccess hello URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="632af-240">Avrupa istemci tarayıcılarından "ASP.NET Batı Avrupa" göstermesi gerekir ve Asya istemci tarayıcısından "ASP.NET Güneydoğu Asya" göstermesi gerekir</span><span class="sxs-lookup"><span data-stu-id="632af-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="632af-241">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="632af-241">More resources</span></span>
