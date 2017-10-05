---
title: "Azure'da hiper ölçekli uygulaması oluşturma | Microsoft Docs"
description: "Farklı Azure Hizmetleri Azure ASP.NET uygulama performansını en üst düzeye çıkarmak için nasıl kullanılacağını öğrenin."
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
ms.openlocfilehash: eac9c5b0d8d0f7802d88e6f4f27d9d23c406e025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="968b1-103">Azure'da hiper ölçekli web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="968b1-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="968b1-104">Bu öğretici, kullanıcı isteklerini en üst düzeye çıkarmak için azure'da ASP.NET web uygulamasını genişletmek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="968b1-104">This tutorial shows you how to scale out an ASP.NET web app in Azure to maximize user requests.</span></span>

<span data-ttu-id="968b1-105">Bu öğreticiye başlamadan önce emin olun [Azure CLI yüklenmiş](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) makinenizde.</span><span class="sxs-lookup"><span data-stu-id="968b1-105">Before starting this tutorial, ensure that [the Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="968b1-106">Ayrıca, gereksinim duyduğunuz [Visual Studio](https://www.visualstudio.com/vs/) örnek uygulamayı çalıştırmak için yerel makinenizde.</span><span class="sxs-lookup"><span data-stu-id="968b1-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine to run the sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="968b1-107">1. adım - Get örnek uygulama</span><span class="sxs-lookup"><span data-stu-id="968b1-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="968b1-108">Bu adımda, yerel ASP.NET projesi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="968b1-108">In this step, you set up the local ASP.NET project.</span></span>

### <a name="clone-the-application-repository"></a><span data-ttu-id="968b1-109">Uygulama depoyu kopyalayın</span><span class="sxs-lookup"><span data-stu-id="968b1-109">Clone the application repository</span></span>

<span data-ttu-id="968b1-110">Tercih ettiğiniz komut satırı Terminalini açın ve `CD` bir çalışma dizini için.</span><span class="sxs-lookup"><span data-stu-id="968b1-110">Open the command-line terminal of your choice and `CD` to a working directory.</span></span> <span data-ttu-id="968b1-111">Ardından örnek uygulamayı kopyalamak için aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="968b1-111">Then, run the following commands to clone the sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-the-sample-application-in-visual-studio"></a><span data-ttu-id="968b1-112">Visual Studio'da örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="968b1-112">Run the sample application in Visual Studio</span></span>

<span data-ttu-id="968b1-113">Çözümü Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="968b1-113">Open the solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="968b1-114">Tür `F5` uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="968b1-114">Type `F5` to run the application.</span></span>

<span data-ttu-id="968b1-115">Bu örnek ASP.NET web uygulaması ve varsayılan şablondan gelir ve kullanıcı devam ediyorsa oturumlar ve çıktı önbelleği kullanır.</span><span class="sxs-lookup"><span data-stu-id="968b1-115">This sample ASP.NET web application comes from the default template, and persists user sessions and uses the output cache.</span></span> <span data-ttu-id="968b1-116">Bir göz atalım `HighScaleApp\Controllers\HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="968b1-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="968b1-117">`Index()` Yöntemi veri parçası oturumuna ekler.</span><span class="sxs-lookup"><span data-stu-id="968b1-117">The `Index()` method adds a piece of data to the session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="968b1-118">Ve `About()` ve `Contact()` yöntemlerini çıkışı önbelleğe.</span><span class="sxs-lookup"><span data-stu-id="968b1-118">And the `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-to-azure"></a><span data-ttu-id="968b1-119">Adım 2 - Azure'a dağıtma</span><span class="sxs-lookup"><span data-stu-id="968b1-119">Step 2 - Deploy to Azure</span></span>
<span data-ttu-id="968b1-120">Bu adımda, Azure web uygulaması oluşturun ve ona örnek ASP.NET uygulamanızı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="968b1-120">In this step, you create an Azure web app and deploy your sample ASP.NET application to it.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="968b1-121">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="968b1-121">Create a resource group</span></span>   
<span data-ttu-id="968b1-122">Kullanım [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) oluşturmak için bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) Batı Avrupa bölgede.</span><span class="sxs-lookup"><span data-stu-id="968b1-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) to create a [resource group](../azure-resource-manager/resource-group-overview.md) in the West Europe region.</span></span> <span data-ttu-id="968b1-123">Bir kaynak grubu, olduğu gibi web uygulamasını ve herhangi bir SQL veritabanı arka uç birlikte, yönetmek istediğiniz tüm Azure kaynakları koyduğunuz yerdir.</span><span class="sxs-lookup"><span data-stu-id="968b1-123">A resource group is where you put all the Azure resources that you want to manage together, such as the web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="968b1-124">Hangi olası değerleri görmek için kullanabileceğiniz `---location`, kullanın [az appservice listesi-konumları](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) komutu.</span><span class="sxs-lookup"><span data-stu-id="968b1-124">To see what possible values you can use for `---location`, use the [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="968b1-125">App Service planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="968b1-125">Create an App Service plan</span></span>
<span data-ttu-id="968b1-126">Kullanım [az uygulama hizmeti planı oluşturma](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) "B1" oluşturmak için [uygulama hizmeti planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="968b1-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) to create a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="968b1-127">Bir uygulama hizmeti planı aynı uygulama hizmeti altyapı üzerinden veya birlikte ölçeklendirmek istediğiniz uygulamaları herhangi bir sayıda içerebilen bir ölçek birimidir.</span><span class="sxs-lookup"><span data-stu-id="968b1-127">An App Service plan is a scale unit, which can include any number of apps that you want to scale up or out together over the same App Service infrastructure.</span></span> <span data-ttu-id="968b1-128">Her plan da atanmış bir [fiyatlandırma katmanı](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="968b1-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="968b1-129">Daha yüksek katmanları daha iyi donanım ve daha fazla genişleme örnekleri gibi daha fazla özellik içerir.</span><span class="sxs-lookup"><span data-stu-id="968b1-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="968b1-130">Bu öğretici için üç örneklerine ölçek genişletme sağlayan en az katman B1 olur.</span><span class="sxs-lookup"><span data-stu-id="968b1-130">For this tutorial, B1 is the minimum tier that enables scale out to three instances.</span></span> <span data-ttu-id="968b1-131">İstediğiniz zaman, uygulamanızın yukarı veya aşağı fiyatlandırma katmanı ve daha sonra çalıştırarak taşıyabilirsiniz [az uygulama hizmeti planı güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span><span class="sxs-lookup"><span data-stu-id="968b1-131">You can always move your app up or down the pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="968b1-132">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="968b1-132">Create a web app</span></span>
<span data-ttu-id="968b1-133">Kullanım [az appservice web oluşturmak](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) benzersiz bir ad ile bir web uygulaması oluşturmak için `$appName`.</span><span class="sxs-lookup"><span data-stu-id="968b1-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="968b1-134">Dağıtım kimlik bilgilerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="968b1-134">Set deployment credentials</span></span>
<span data-ttu-id="968b1-135">Kullanım [az appservice web dağıtım kullanıcısı ayarlanmadı](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) için uygulama hizmeti hesabı düzeyinde dağıtım kimlik bilgilerinizi ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="968b1-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) to set your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="968b1-136">Git dağıtımı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="968b1-136">Configure Git deployment</span></span>
<span data-ttu-id="968b1-137">Kullanım [az appservice web kaynak denetimi config-yerel-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) yerel Git dağıtımı yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="968b1-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="968b1-138">Bu komut, aşağıdakine benzer bir çıktı sunar:</span><span class="sxs-lookup"><span data-stu-id="968b1-138">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="968b1-139">Döndürülen URL'ye Git uzaktan yapılandırmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="968b1-139">Use the returned URL to configure your Git remote.</span></span> <span data-ttu-id="968b1-140">Aşağıdaki komutu önceki çıktı örneği kullanır.</span><span class="sxs-lookup"><span data-stu-id="968b1-140">The following command uses the preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-the-sample-application"></a><span data-ttu-id="968b1-141">Örnek uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="968b1-141">Deploy the sample application</span></span>
<span data-ttu-id="968b1-142">Şimdi örnek uygulamanızı dağıtmak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="968b1-142">You are now ready to deploy your sample application.</span></span> <span data-ttu-id="968b1-143">`git push` öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="968b1-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="968b1-144">Parola istendiğinde, ne zaman çalıştırıldığı belirtilen parolayı kullanmak `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="968b1-144">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-azure-web-app"></a><span data-ttu-id="968b1-145">Azure web uygulaması'na göz atın</span><span class="sxs-lookup"><span data-stu-id="968b1-145">Browse to Azure web app</span></span>
<span data-ttu-id="968b1-146">Kullanım [az appservice web Gözat](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) uygulamanızı Azure'da çalışırken görmek için bu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="968b1-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-to-redis"></a><span data-ttu-id="968b1-147">Adım 3 - Redis için Bağlan</span><span class="sxs-lookup"><span data-stu-id="968b1-147">Step 3 - Connect to Redis</span></span>
<span data-ttu-id="968b1-148">Bu adımda, Azure Redis önbelleği, Azure web uygulamanızın bir dış, birlikte bulunan önbellek olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="968b1-148">In this step, you set up Azure Redis Cache as an external, colocated cache to your Azure web app.</span></span> <span data-ttu-id="968b1-149">Sayfa çıktısının önbelleğe almak için Redis hızlı bir şekilde kullanabilirler.</span><span class="sxs-lookup"><span data-stu-id="968b1-149">You can quickly utilize Redis to cache your page output.</span></span> <span data-ttu-id="968b1-150">Web uygulamalarınızı daha sonra ölçeklendirdiğinizde Ayrıca, Redis kalıcı yardımcı olan birden çok kullanıcı oturumlarında örnekleri güvenilir.</span><span class="sxs-lookup"><span data-stu-id="968b1-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="968b1-151">Azure Redis Cache oluşturma</span><span class="sxs-lookup"><span data-stu-id="968b1-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="968b1-152">Kullanım [az redis oluşturma](https://docs.microsoft.com/en-us/cli/azure/redis#create) bir Azure Redis önbelleği oluşturmak ve JSON kaydetmek için çıktı.</span><span class="sxs-lookup"><span data-stu-id="968b1-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create an Azure Redis Cache and save the JSON output.</span></span> <span data-ttu-id="968b1-153">Benzersiz bir ad kullanmak `$cacheName`.</span><span class="sxs-lookup"><span data-stu-id="968b1-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-the-application-to-use-redis"></a><span data-ttu-id="968b1-154">Redis kullanmak için uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="968b1-154">Configure the application to use Redis</span></span>
<span data-ttu-id="968b1-155">Önbellek hesabınız için bağlantı dizesi biçimi.</span><span class="sxs-lookup"><span data-stu-id="968b1-155">Format the connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="968b1-156">İkinci satır şuna benzer bir çıktı vermeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="968b1-156">The second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="968b1-157">Visual Studio'da adlı proje kök web yapılandırma dosyası oluşturma `redis.config` ve aşağıdaki kodu yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="968b1-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste the following code into it.</span></span> <span data-ttu-id="968b1-158">İçinde `value`, PowerShell çıkış bağlantı dizesinden kullanın.</span><span class="sxs-lookup"><span data-stu-id="968b1-158">In `value`, use the connection string from the PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="968b1-159">Bakarsanız `.gitignore` dosya Git deponuzu bu dosyayı kaynak denetiminden dışlandı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="968b1-159">If you look at the `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="968b1-160">Bu şekilde, hassas bilgilerinizi güvenli tutulur.</span><span class="sxs-lookup"><span data-stu-id="968b1-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="968b1-161">Açık `Web.config`.</span><span class="sxs-lookup"><span data-stu-id="968b1-161">Open `Web.config`.</span></span> <span data-ttu-id="968b1-162">Bildirim `<appSettings file="redis.config">` oluşturduğunuz ayarını alır öğesi `redis.config`.</span><span class="sxs-lookup"><span data-stu-id="968b1-162">Notice the `<appSettings file="redis.config">` element, which gets the setting you created in `redis.config`.</span></span> 

<span data-ttu-id="968b1-163">İçeren açıklamalı bölüm Bul `<sessionState>` ve `<caching>`.</span><span class="sxs-lookup"><span data-stu-id="968b1-163">Find the commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="968b1-164">Bu bölümde açıklamadan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="968b1-164">Uncomment this section.</span></span>

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="968b1-165">Bu kod Redis bağlantı dizesi için tanımladığınız görünür `RedisConnection`.</span><span class="sxs-lookup"><span data-stu-id="968b1-165">This code looks for the Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="968b1-166">Uygulamanızı şimdi Redis oturumlar ve önbelleğe alma yönetmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="968b1-166">Your application now uses Redis to manage sessions and caching.</span></span> <span data-ttu-id="968b1-167">Tür `F5` uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="968b1-167">Type `F5` to run the application.</span></span> <span data-ttu-id="968b1-168">İsterseniz, şimdi önbelleğe kaydedilen verileri görselleştirmek için bir Redis yönetim istemcisi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="968b1-168">If you like, you can download a Redis management client to visualize the data that is now saved to the cache.</span></span>

### <a name="configure-the-connection-string-in-azure"></a><span data-ttu-id="968b1-169">Bağlantı dizesi Azure'da yapılandırın</span><span class="sxs-lookup"><span data-stu-id="968b1-169">Configure the connection string in Azure</span></span>

<span data-ttu-id="968b1-170">Uygulamanızı Azure'da çalışması, Azure web uygulamanızda aynı Redis bağlantı dizesi yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="968b1-170">For your application to work in Azure, you need to configure the same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="968b1-171">Bu yana `redis.config` tutulmaz kaynak denetiminde onu dağıtılmazsa Azure'a Git dağıtımı çalıştırdığınızda.</span><span class="sxs-lookup"><span data-stu-id="968b1-171">Since `redis.config` is not maintained in source control, it is not deployed to Azure when you run Git deployment.</span></span>

<span data-ttu-id="968b1-172">Kullanım [az appservice web yapılandırma appsettings güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) aynı ada sahip bağlantı dizesi eklemek için (`RedisConnection`).</span><span class="sxs-lookup"><span data-stu-id="968b1-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add the connection string with the same name (`RedisConnection`).</span></span>

<span data-ttu-id="968b1-173">appSettings güncelleştirme--az appservice web yapılandırma ayarları "RedisConnection $connstring ="--$appName--kaynak-grubu myResourceGroup adı</span><span class="sxs-lookup"><span data-stu-id="968b1-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="968b1-174">Unutmayın `$connstring` biçimlendirilmiş bağlantı dizesi içeriyor.</span><span class="sxs-lookup"><span data-stu-id="968b1-174">Remember that `$connstring` contains the formatted connection string.</span></span>

### <a name="redeploy-the-application-to-azure"></a><span data-ttu-id="968b1-175">Azure için uygulamayı yeniden Dağıt</span><span class="sxs-lookup"><span data-stu-id="968b1-175">Redeploy the application to Azure</span></span>
<span data-ttu-id="968b1-176">Değişikliklerinizi Azure'a göndermek için Git komutları kullanın</span><span class="sxs-lookup"><span data-stu-id="968b1-176">Use Git commands to push your changes to Azure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="968b1-177">Parola istendiğinde, ne zaman çalıştırıldığı belirtilen parolayı kullanmak `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="968b1-177">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="968b1-178">Azure web uygulaması'na göz atın</span><span class="sxs-lookup"><span data-stu-id="968b1-178">Browse to the Azure web app</span></span>
<span data-ttu-id="968b1-179">Kullanım [az appservice web Gözat](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) Azure'da Canlı değişiklikleri görmek için.</span><span class="sxs-lookup"><span data-stu-id="968b1-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see the changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-to-multiple-instances"></a><span data-ttu-id="968b1-180">4. adım - birden çok örneği için Ölçeklendir</span><span class="sxs-lookup"><span data-stu-id="968b1-180">Step 4 - Scale to multiple instances</span></span>
<span data-ttu-id="968b1-181">Uygulama hizmeti planı, Azure web uygulamaları için ölçek birimidir.</span><span class="sxs-lookup"><span data-stu-id="968b1-181">The App Service plan is the scale unit for your Azure web apps.</span></span> <span data-ttu-id="968b1-182">Web uygulamanızı ölçeklendirmek için uygulama hizmeti planı ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="968b1-182">To scale out your web app, you scale the App Service plan.</span></span>

<span data-ttu-id="968b1-183">Kullanım [az uygulama hizmeti planı güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/plan#update) en büyük sayı olan uygulama hizmeti planı üç örneklerine ölçeklendirmek için izin verilen B1 fiyatlandırma katmanı tarafından.</span><span class="sxs-lookup"><span data-stu-id="968b1-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale out the App Service plan to three instances, which is the maximum number allowed by the B1 pricing tier.</span></span> <span data-ttu-id="968b1-184">B1 zaman uygulama hizmeti planı daha önce oluşturduğunuz seçtiğiniz fiyatlandırma katmanı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="968b1-184">Remember that B1 is the pricing tier that you chose when you created the App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="968b1-185">Adım 5 - ölçek coğrafi olarak</span><span class="sxs-lookup"><span data-stu-id="968b1-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="968b1-186">Coğrafi olarak ölçekleme sırasında Azure bulut birden çok bölgede uygulamanızı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="968b1-186">When scaling geographically, you run your app in multiple regions of the Azure cloud.</span></span> <span data-ttu-id="968b1-187">Bu kurulum yük bakiyelerini Coğrafya hakkında daha fazla temel uygulamanızı ve uygulamanıza yakın istemci tarayıcıları koyarak yanıt süresini azaltır.</span><span class="sxs-lookup"><span data-stu-id="968b1-187">This setup load-balances your app further based on geography and lowers the response time by placing your app closer to client browsers.</span></span>

<span data-ttu-id="968b1-188">Bu adımda, ASP.NET web uygulamanızı sahip ikinci bir bölge için ölçeklendirme [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="968b1-188">In this step, you scale your ASP.NET web app to a second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="968b1-189">Adımın sonunda, Batı Avrupa (önceden oluşturulmuş) çalıştıran bir web uygulaması ve Güneydoğu Asya (henüz oluşturulmadı) çalıştıran bir web uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="968b1-189">At the end of the step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="968b1-190">Her iki uygulamalar aynı trafik Yöneticisi URL'den sunulacak.</span><span class="sxs-lookup"><span data-stu-id="968b1-190">Both apps will be served from the same Traffic Manager URL.</span></span>

### <a name="scale-up-the-europe-app-to-standard-tier"></a><span data-ttu-id="968b1-191">Standart katmanı Avrupa uygulamaya ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="968b1-191">Scale up the Europe app to Standard tier</span></span>
<span data-ttu-id="968b1-192">App Service içinde Azure Traffic Manager ile tümleştirme standart fiyatlandırma katmanı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="968b1-192">In App Service, integration with Azure Traffic Manager requires the Standard pricing tier.</span></span> <span data-ttu-id="968b1-193">Kullanım [az uygulama hizmeti planı güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/plan#update) S1 için uygulama hizmeti planınızı ölçeklendirmek için.</span><span class="sxs-lookup"><span data-stu-id="968b1-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale up your App Service plan to S1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="968b1-194">Traffic Manager profili oluşturma</span><span class="sxs-lookup"><span data-stu-id="968b1-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="968b1-195">Kullanım [az ağ trafik Yöneticisi profili oluştur](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) bir trafik Yöneticisi profili oluşturun ve kaynak grubuna eklemek için.</span><span class="sxs-lookup"><span data-stu-id="968b1-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) to create a Traffic Manager profile and add it to your resource group.</span></span> <span data-ttu-id="968b1-196">Benzersiz bir DNS adı $dnsName kullanın.</span><span class="sxs-lookup"><span data-stu-id="968b1-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="968b1-197">`--routing-method Performance`belirleyen bu profili [kullanıcı trafiğini en yakın uç noktasına yönlendirir](../traffic-manager/traffic-manager-routing-methods.md).</span><span class="sxs-lookup"><span data-stu-id="968b1-197">`--routing-method Performance` specifies that this profile [routes user traffic to the closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-the-resource-id-of-the-europe-app"></a><span data-ttu-id="968b1-198">Avrupa uygulama kaynak Kimliğini Al</span><span class="sxs-lookup"><span data-stu-id="968b1-198">Get the resource ID of the Europe app</span></span>
<span data-ttu-id="968b1-199">Kullanım [az appservice web Göster](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) , web uygulamanızın kaynak kimliği alınamadı.</span><span class="sxs-lookup"><span data-stu-id="968b1-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-europe-app"></a><span data-ttu-id="968b1-200">Trafik Yöneticisi uç noktası Avrupa uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="968b1-200">Add a Traffic Manager endpoint for the Europe app</span></span>
<span data-ttu-id="968b1-201">Kullanmak [az ağ trafik Yöneticisi uç noktası oluşturma](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) bir uç nokta Traffic Manager profilinize ekleyin ve hedefi olarak, web uygulamanızın kaynak Kimliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="968b1-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add an endpoint to your Traffic Manager profile and use the resource ID of your web app as the target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-the-traffic-manager-endpoint-url"></a><span data-ttu-id="968b1-202">Trafik Yöneticisi uç nokta URL'sini alma</span><span class="sxs-lookup"><span data-stu-id="968b1-202">Get the Traffic Manager endpoint URL</span></span>
<span data-ttu-id="968b1-203">Traffic Manager profilinizin artık mevcut web uygulamanıza işaret eden bir uç nokta sahiptir.</span><span class="sxs-lookup"><span data-stu-id="968b1-203">Your Traffic Manager profile now has an endpoint that points to your existing web app.</span></span> <span data-ttu-id="968b1-204">Kullanım [az ağ trafik Yöneticisi profili Göster](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) URL'sini almak için.</span><span class="sxs-lookup"><span data-stu-id="968b1-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) to get its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="968b1-205">Çıktı tarayıcınıza kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="968b1-205">Copy the output into your browser.</span></span> <span data-ttu-id="968b1-206">Web uygulamanızı yeniden görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="968b1-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="968b1-207">Bir Azure Redis önbelleği Asya'da oluşturma</span><span class="sxs-lookup"><span data-stu-id="968b1-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="968b1-208">Şimdi, Azure web uygulamanızın Güneydoğu Asya bölgeye çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="968b1-208">Now, you replicate your Azure web app to the Southeast Asia region.</span></span> <span data-ttu-id="968b1-209">Başlatmak için kullanmak [az redis oluşturma](https://docs.microsoft.com/en-us/cli/azure/redis#create) Güneydoğu Asya ikinci bir Azure Redis önbelleği oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="968b1-209">To start, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="968b1-210">Bu önbellek Asya'da uygulamanızla birlikte olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="968b1-210">This cache needs to be colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="968b1-211">`--name $cacheName-asia`önbellek ile Batı Avrupa önbellek adını verir `-asia` soneki.</span><span class="sxs-lookup"><span data-stu-id="968b1-211">`--name $cacheName-asia` gives the cache the name of the West Europe cache, with the `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="968b1-212">Asya'da bir uygulama hizmeti planı oluştur</span><span class="sxs-lookup"><span data-stu-id="968b1-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="968b1-213">Kullanım [az uygulama hizmeti planı oluşturma](https://docs.microsoft.com/cli/azure/appservice/plan#create) Batı Avrupa plan aynı S1 katmanı kullanarak Güneydoğu Asya bölgesinde ikinci bir uygulama hizmeti planı oluşturulamadı.</span><span class="sxs-lookup"><span data-stu-id="968b1-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) to create a second App Service plan in the Southeast Asia region, using the same S1 tier as the West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="968b1-214">Asya'da bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="968b1-214">Create a web app in Asia</span></span>
<span data-ttu-id="968b1-215">Kullanım [az appservice web oluşturmak](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) ikinci bir web uygulaması oluşturma.</span><span class="sxs-lookup"><span data-stu-id="968b1-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="968b1-216">`--name $appName-asia`uygulama ile Batı Avrupa uygulama adını verir `-asia` soneki.</span><span class="sxs-lookup"><span data-stu-id="968b1-216">`--name $appName-asia` gives the app the name of the West Europe app, with the `-asia` suffix.</span></span>

### <a name="configure-the-connection-string-for-redis"></a><span data-ttu-id="968b1-217">Redis için bağlantı dizesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="968b1-217">Configure the connection string for Redis</span></span>
<span data-ttu-id="968b1-218">Kullanım [az appservice web yapılandırma appsettings güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) web uygulaması'na Güneydoğu Asya önbelleği için bağlantı dizesi eklemek için.</span><span class="sxs-lookup"><span data-stu-id="968b1-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add to the web app the connection string for the Southeast Asia cache.</span></span>

<span data-ttu-id="968b1-219">appSettings güncelleştirme--az appservice web yapılandırma ayarları "RedisConnection = $($redis.hostname): $($redis.sslPort), parola = $($redis.accessKeys.primaryKey) ssl = True, abortConnect = False"--ad $appName-Asya--kaynak-grubu myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="968b1-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-the-asia-app"></a><span data-ttu-id="968b1-220">Asya uygulaması için Git dağıtımı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="968b1-220">Configure Git deployment for the Asia app.</span></span>
<span data-ttu-id="968b1-221">Kullanım [az appservice web kaynak denetimi config-yerel-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) ikinci web uygulaması için yerel Git dağıtımı yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="968b1-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment for the second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="968b1-222">Bu komut, aşağıdakine benzer bir çıktı sunar:</span><span class="sxs-lookup"><span data-stu-id="968b1-222">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="968b1-223">Döndürülen URL için yerel deponuza uzak ikinci Git yapılandırmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="968b1-223">Use the returned URL to configure a second Git remote for your local repository.</span></span> <span data-ttu-id="968b1-224">Aşağıdaki komutu önceki çıktı örneği kullanır.</span><span class="sxs-lookup"><span data-stu-id="968b1-224">The following command uses the preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="968b1-225">Örnek uygulamanızı dağıtma</span><span class="sxs-lookup"><span data-stu-id="968b1-225">Deploy your sample application</span></span>
<span data-ttu-id="968b1-226">Çalıştırma `git push` ikinci Git remote örnek uygulamanızı dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="968b1-226">Run `git push` to deploy your sample application to the second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="968b1-227">Parola istendiğinde, ne zaman çalıştırıldığı belirtilen parolayı kullanmak `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="968b1-227">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-asia-app"></a><span data-ttu-id="968b1-228">Asya app uygulamanıza gözatma</span><span class="sxs-lookup"><span data-stu-id="968b1-228">Browse to the Asia app</span></span>
<span data-ttu-id="968b1-229">Kullanım [az appservice web Gözat](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) uygulamanızı azure'da çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="968b1-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to verify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-the-resource-id-of-the-asia-app"></a><span data-ttu-id="968b1-230">Asya uygulama kaynak Kimliğini Al</span><span class="sxs-lookup"><span data-stu-id="968b1-230">Get the resource ID of the Asia app</span></span>
<span data-ttu-id="968b1-231">Kullanım [az appservice web Göster](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) Güneydoğu Asya, web uygulamanızın kaynak kimliği alınamadı.</span><span class="sxs-lookup"><span data-stu-id="968b1-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-asia-app"></a><span data-ttu-id="968b1-232">Trafik Yöneticisi uç noktası Asya uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="968b1-232">Add a Traffic Manager endpoint for the Asia app</span></span>
<span data-ttu-id="968b1-233">Kullanım [az ağ trafik Yöneticisi uç noktası oluşturma](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) ikinci bir uç nokta Traffic Manager profili eklemek için.</span><span class="sxs-lookup"><span data-stu-id="968b1-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add a second endpoint to the Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-to-web-apps"></a><span data-ttu-id="968b1-234">Web uygulamaları için bölge tanımlayıcısı ekleme</span><span class="sxs-lookup"><span data-stu-id="968b1-234">Add region identifier to web apps</span></span>
<span data-ttu-id="968b1-235">Kullanım [az appservice web yapılandırma appsettings güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) bölgeye özgü ortam değişkeni eklemek için.</span><span class="sxs-lookup"><span data-stu-id="968b1-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="968b1-236">Uygulama kodunuz, bu uygulama ayarı zaten kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="968b1-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="968b1-237">Bir göz atalım `HighScaleApp\Views\Home\Index.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="968b1-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="968b1-238">Tamamlandı!</span><span class="sxs-lookup"><span data-stu-id="968b1-238">Complete!</span></span>

<span data-ttu-id="968b1-239">Şimdi, farklı coğrafi bölgelerde tarayıcılardan Traffic Manager profilinizin URL'sini erişmeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="968b1-239">Now, try to access the URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="968b1-240">Avrupa istemci tarayıcılarından "ASP.NET Batı Avrupa" göstermesi gerekir ve Asya istemci tarayıcısından "ASP.NET Güneydoğu Asya" göstermesi gerekir</span><span class="sxs-lookup"><span data-stu-id="968b1-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="968b1-241">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="968b1-241">More resources</span></span>
