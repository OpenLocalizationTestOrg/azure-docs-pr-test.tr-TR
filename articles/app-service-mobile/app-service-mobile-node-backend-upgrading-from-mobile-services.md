---
title: Mobile Services tooAzure - App Service Node.js gelen aaaUpgrade
description: "Nasıl tooeasily yükseltme Mobile Services uygulama tooan mobil uygulama hizmeti öğrenin"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: c58f6df0-5aad-40a3-bddc-319c378218e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 722cda244d4f633247827f58ea6f1397137ea600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-nodejs-azure-mobile-service-tooapp-service"></a><span data-ttu-id="c5c96-103">Varolan Node.js Azure mobil hizmeti tooApp hizmet yükseltme</span><span class="sxs-lookup"><span data-stu-id="c5c96-103">Upgrade your existing Node.js Azure Mobile Service tooApp Service</span></span>
<span data-ttu-id="c5c96-104">App Service Mobile Microsoft Azure kullanarak bir yeni yolu toobuild mobil uygulamaları ' dir.</span><span class="sxs-lookup"><span data-stu-id="c5c96-104">App Service Mobile is a new way toobuild mobile applications using Microsoft Azure.</span></span> <span data-ttu-id="c5c96-105">toolearn daha, fazla [Mobile Apps nedir?].</span><span class="sxs-lookup"><span data-stu-id="c5c96-105">toolearn more, see [What are Mobile Apps?].</span></span>

<span data-ttu-id="c5c96-106">Bu konuda açıklanmaktadır nasıl Azure Mobile Services tooa varolan Node.js arka uç uygulamasından tooupgrade yeni App Service Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="c5c96-106">This topic describes how tooupgrade an existing Node.js backend application from Azure Mobile Services tooa new App Service Mobile Apps.</span></span> <span data-ttu-id="c5c96-107">Bu yükseltme gerçekleştirirken mevcut Mobile Services uygulamanızı toooperate devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c5c96-107">While you perform this upgrade, your existing Mobile Services application can continue toooperate.</span></span>  <span data-ttu-id="c5c96-108">Tooupgrade bir Node.js arka uç uygulaması gereksinim duyarsanız, çok başvurun[.NET Mobile Services yükseltme](app-service-mobile-net-upgrading-from-mobile-services.md).</span><span class="sxs-lookup"><span data-stu-id="c5c96-108">If you need tooupgrade a Node.js backend application, refer too[Upgrading your .NET Mobile Services](app-service-mobile-net-upgrading-from-mobile-services.md).</span></span>

<span data-ttu-id="c5c96-109">Bir mobil arka uç yükseltilmiş tooAzure uygulama hizmeti olduğunda, uygulama hizmeti özellikler ve öğeler faturalandırılır çok according erişim tooall sahip[uygulama hizmeti fiyatlandırma], fiyatlandırma değil Mobile Services.</span><span class="sxs-lookup"><span data-stu-id="c5c96-109">When a mobile backend is upgraded tooAzure App Service, it has access tooall App Service features and are billed according too[App Service pricing], not Mobile Services pricing.</span></span>

## <a name="migrate-vs-upgrade"></a><span data-ttu-id="c5c96-110">Yükseltme geçirme</span><span class="sxs-lookup"><span data-stu-id="c5c96-110">Migrate vs. upgrade</span></span>
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> <span data-ttu-id="c5c96-111">Önerilir Bu, [bir geçiş gerçekleştirmek](app-service-mobile-migrating-from-mobile-services.md) yükseltme geçmeden önce.</span><span class="sxs-lookup"><span data-stu-id="c5c96-111">It is recommended that you [perform a migration](app-service-mobile-migrating-from-mobile-services.md) before going through an upgrade.</span></span> <span data-ttu-id="c5c96-112">Bu şekilde, her iki sürümü, uygulamanızın koyabilirsiniz aynı App Service planı hello ve ek bir maliyet doğurur.</span><span class="sxs-lookup"><span data-stu-id="c5c96-112">This way, you can put both versions of your application on hello same App Service Plan and incur no additional cost.</span></span>
>
>

### <a name="improvements-in-mobile-apps-nodejs-server-sdk"></a><span data-ttu-id="c5c96-113">Mobile Apps Node.js sunucusu SDK yenilikleri</span><span class="sxs-lookup"><span data-stu-id="c5c96-113">Improvements in Mobile Apps Node.js server SDK</span></span>
<span data-ttu-id="c5c96-114">Yeni toohello yükseltme [Mobile Apps SDK'sı](https://www.npmjs.com/package/azure-mobile-apps) iyileştirmeler de dahil olmak üzere birçok sağlar:</span><span class="sxs-lookup"><span data-stu-id="c5c96-114">Upgrading toohello new [Mobile Apps SDK](https://www.npmjs.com/package/azure-mobile-apps) provides a lot of improvements, including:</span></span>

* <span data-ttu-id="c5c96-115">Merhaba üzerinde temel [Express framework](http://expressjs.com/en/index.html), hello yeni bir düğüm SDK hafif ve yeni düğümü sürümleriyle gelen yukarı tookeep tasarlanmıştır. Express ara yazılımını ile Merhaba uygulama davranışını özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c5c96-115">Based on hello [Express framework](http://expressjs.com/en/index.html), hello new Node SDK is light-weight and designed tookeep up with new Node versions as they come out. You can customize hello application behavior with Express middleware.</span></span>
* <span data-ttu-id="c5c96-116">Önemli performans geliştirmeleri toohello Mobile Services SDK'sı karşılaştırılan.</span><span class="sxs-lookup"><span data-stu-id="c5c96-116">Significant performance improvements compared toohello Mobile Services SDK.</span></span>
* <span data-ttu-id="c5c96-117">Bir Web sitesi ile birlikte mobil arka şimdi barındırabilir; benzer şekilde, bu kolay tooadd hello Azure Mobile SDK tooany varolan express.v4 uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="c5c96-117">You can now host a website together with your mobile backend; similarly, it's easy tooadd hello Azure Mobile SDK tooany existing express.v4 application.</span></span>
* <span data-ttu-id="c5c96-118">Platformlar arası ve yerel geliştirme için oluşturulan hello Mobile Apps SDK'sı geliştirilen ve yerel olarak Windows, Linux ve OSX platformlarda çalıştırmak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c5c96-118">Built for cross-platform and local development, hello Mobile Apps SDK can be developed and run locally on Windows, Linux, and OSX platforms.</span></span> <span data-ttu-id="c5c96-119">Kolay toouse ortak düğüm geliştirme teknikleri çalışıyor gibi sunulmuştur [Mocha](https://mochajs.org/) önceki toodeployment sınar.</span><span class="sxs-lookup"><span data-stu-id="c5c96-119">It's now easy toouse common Node development techniques like running [Mocha](https://mochajs.org/) tests prior toodeployment.</span></span>

## <span data-ttu-id="c5c96-120"><a name="overview"></a>Temel yükseltmeye genel bakış</span><span class="sxs-lookup"><span data-stu-id="c5c96-120"><a name="overview"></a>Basic upgrade overview</span></span>
<span data-ttu-id="c5c96-121">Azure App Service'te bir Node.js arka ucu yükseltme sırasında tooaid uyumluluk paketi sağlamıştır.</span><span class="sxs-lookup"><span data-stu-id="c5c96-121">tooaid in upgrading a Node.js backend, Azure App Service has provided a compatibility package.</span></span>  <span data-ttu-id="c5c96-122">Yükseltmeden sonra dağıtılan tooa yeni uygulama hizmeti site olabilir bir niew sitesi olur.</span><span class="sxs-lookup"><span data-stu-id="c5c96-122">After upgrade, you will have a niew site that can be deployed tooa new App Service site.</span></span>

<span data-ttu-id="c5c96-123">Merhaba Mobile Services istemci SDK'ları olan **değil** hello yeni mobil uygulamalar sunucusu SDK ile uyumlu.</span><span class="sxs-lookup"><span data-stu-id="c5c96-123">hello Mobile Services client SDKs are **not** compatible with hello new Mobile Apps server SDK.</span></span> <span data-ttu-id="c5c96-124">Sipariş tooprovide kesintisiz hizmet devamlılığı uygulamanız için, değişiklikleri tooa site şu anda yayımlanan istemciler hizmet veren yayınlamalıdır değil.</span><span class="sxs-lookup"><span data-stu-id="c5c96-124">In order tooprovide continuity of service for your app, you should not publish changes tooa site currently serving published clients.</span></span> <span data-ttu-id="c5c96-125">Bunun yerine, yinelenen hizmet veren yeni bir mobil uygulama oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c5c96-125">Instead, you should create a new mobile app that serves as a duplicate.</span></span> <span data-ttu-id="c5c96-126">Bu uygulama koyabilirsiniz hello üzerinde ek finansal masraf tooavoid aynı uygulama hizmeti planı.</span><span class="sxs-lookup"><span data-stu-id="c5c96-126">You can put this application on hello same App Service plan tooavoid incurring additional financial cost.</span></span>

<span data-ttu-id="c5c96-127">Merhaba uygulaması iki sürümü sonra gerekir: kalır bir hello aynı görevi görür yayımlanan uygulamalar hello joker ve diğeri, ardından yükseltin ve yeni bir istemci ile hedef sürüm.</span><span class="sxs-lookup"><span data-stu-id="c5c96-127">You will then have two versions of hello application: one that stays hello same and serves published apps in hello wild, and the other which you can then upgrade and target with a new client release.</span></span> <span data-ttu-id="c5c96-128">Taşıma ve kodunuzu test etmek, hızı, ancak yaptığınız tüm hata düzeltmeleri uygulanan tooboth alma emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c5c96-128">You can move and test your code at your pace, but you should make sure that any bug fixes you make get applied tooboth.</span></span> <span data-ttu-id="c5c96-129">Düşündüğünüz sonra joker istemci uygulamalarında istenen sayısını toohello en son sürümünü güncelleştirilen, istediğiniz hello özgün geçirilen uygulama silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c5c96-129">Once you feel that a desired number of client apps in the wild have updated toohello latest version, you can delete hello original migrated app if you desire.</span></span> <span data-ttu-id="c5c96-130">Mobil uygulamanızın aynı uygulama hizmeti planı hello barındırılıyorsa, tüm ek para ücrete neden değil.</span><span class="sxs-lookup"><span data-stu-id="c5c96-130">It doesn't incur any additional monetary costs, if hosted in hello same App Service plan as your Mobile App.</span></span>

<span data-ttu-id="c5c96-131">Merhaba tam anahat hello yükseltme işlemi için aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="c5c96-131">hello full outline for hello upgrade process is as follows:</span></span>

1. <span data-ttu-id="c5c96-132">Mevcut (geçirilen) Azure mobil hizmetiniz indirin.</span><span class="sxs-lookup"><span data-stu-id="c5c96-132">Download your existing (migrated) Azure Mobile Service.</span></span>
2. <span data-ttu-id="c5c96-133">Merhaba proje tooan Azure mobil uygulaması Dönüştür hello uyumluluk paketini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c5c96-133">Convert hello project tooan Azure Mobile App using hello compatibility package.</span></span>
3. <span data-ttu-id="c5c96-134">Farkları (örneğin, kimlik doğrulama ayarları) düzeltin.</span><span class="sxs-lookup"><span data-stu-id="c5c96-134">Correct any differences (such as authentication settings).</span></span>
4. <span data-ttu-id="c5c96-135">Dönüştürülmüş Azure mobil uygulama projesi tooa dağıtmak yeni uygulama hizmeti.</span><span class="sxs-lookup"><span data-stu-id="c5c96-135">Deploy your converted Azure Mobile App project tooa new App Service.</span></span>
5. <span data-ttu-id="c5c96-136">Yeni bir sürüm kullanmak yeni mobil uygulama hello istemci uygulamanızın serbest bırakın.</span><span class="sxs-lookup"><span data-stu-id="c5c96-136">Release a new version of your client application that use hello new Mobile App.</span></span>
6. <span data-ttu-id="c5c96-137">(İsteğe bağlı) Özgün geçirilen mobil hizmet uygulamanızı silin.</span><span class="sxs-lookup"><span data-stu-id="c5c96-137">(Optional) Delete your original migrated mobile service app.</span></span>

<span data-ttu-id="c5c96-138">Özgün geçirilen mobil hizmette herhangi bir trafik görmüyorum silme ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="c5c96-138">Deletion can occur when you don't see any traffic on your original migrated mobile service.</span></span>

## <span data-ttu-id="c5c96-139"><a name="install-npm-package"></a>Merhaba Önkoşulları Yükleme</span><span class="sxs-lookup"><span data-stu-id="c5c96-139"><a name="install-npm-package"></a> Install hello Pre-requisites</span></span>
<span data-ttu-id="c5c96-140">Yerel makinenizde [Node] yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c5c96-140">You should install [Node] on your local machine.</span></span>  <span data-ttu-id="c5c96-141">Merhaba uyumluluğu paketi de yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c5c96-141">You should also install hello compatibility package.</span></span>  <span data-ttu-id="c5c96-142">Düğüm yüklendikten sonra hello bir yeni cmd veya PowerShell komut isteminde aşağıdaki komutu çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c5c96-142">After Node is installed, you can run hello following command from a new cmd or PowerShell prompt:</span></span>

```npm i -g azure-mobile-apps-compatibility```

## <span data-ttu-id="c5c96-143"><a name="obtain-ams-scripts"></a>Azure mobil hizmetler komut dosyalarınız alın</span><span class="sxs-lookup"><span data-stu-id="c5c96-143"><a name="obtain-ams-scripts"></a> Obtain your Azure Mobile Services Scripts</span></span>
* <span data-ttu-id="c5c96-144">İçinde toohello oturum [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="c5c96-144">Log in toohello [Azure Portal].</span></span>
* <span data-ttu-id="c5c96-145">Kullanarak **tüm kaynakları** veya **uygulama hizmetleri**, Mobile Services sitenizi bulun.</span><span class="sxs-lookup"><span data-stu-id="c5c96-145">Using **All Resources** or **App Services**, find your Mobile Services site.</span></span>
* <span data-ttu-id="c5c96-146">Merhaba sitede tıklayın **Araçları** -> **Kudu** -> **Git** tooopen hello Kudu site.</span><span class="sxs-lookup"><span data-stu-id="c5c96-146">Within hello site, click on **Tools** -> **Kudu** -> **Go** tooopen hello Kudu site.</span></span>
* <span data-ttu-id="c5c96-147">Tıklayın **hata ayıklama Konsolu'nda** -> **PowerShell** tooopen hello Hata Ayıkla Konsolu.</span><span class="sxs-lookup"><span data-stu-id="c5c96-147">Click on **Debug Console** -> **PowerShell** tooopen hello Debug console.</span></span>
* <span data-ttu-id="c5c96-148">Çok gidin`site/wwwroot/App_Data/config` her bir dizinin sırayla tıklayarak</span><span class="sxs-lookup"><span data-stu-id="c5c96-148">Navigate too`site/wwwroot/App_Data/config` by clicking on each directory in turn</span></span>
* <span data-ttu-id="c5c96-149">Merhaba indirme simgesi sonraki toohello tıklatıldığında `scripts` dizin.</span><span class="sxs-lookup"><span data-stu-id="c5c96-149">Click on hello download icon next toohello `scripts` directory.</span></span>

<span data-ttu-id="c5c96-150">Bu ZIP biçiminde hello komut dosyaları indirir.</span><span class="sxs-lookup"><span data-stu-id="c5c96-150">This will download hello scripts in ZIP format.</span></span>  <span data-ttu-id="c5c96-151">Yerel makinenizde yeni bir dizin oluşturun ve hello paket `scripts.ZIP` hello dizini içindeki dosya.</span><span class="sxs-lookup"><span data-stu-id="c5c96-151">Create a new directory on your local machine and unpack hello `scripts.ZIP` file within hello directory.</span></span>  <span data-ttu-id="c5c96-152">Bu oluşturacak bir `scripts` dizin.</span><span class="sxs-lookup"><span data-stu-id="c5c96-152">This will create a `scripts` directory.</span></span>

## <span data-ttu-id="c5c96-153"><a name="scaffold-app"></a>İskele hello yeni Azure Mobile Apps arka uç</span><span class="sxs-lookup"><span data-stu-id="c5c96-153"><a name="scaffold-app"></a> Scaffold hello new Azure Mobile Apps backend</span></span>
<span data-ttu-id="c5c96-154">Merhaba betikleri dizinini içeren hello dizininden komutu aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c5c96-154">Run hello following command from hello directory containing hello scripts directory:</span></span>

```scaffold-mobile-app scripts out```

<span data-ttu-id="c5c96-155">Bu kurulmuş bir Azure Mobile Apps arka uç hello oluşturacak `out` dizin.</span><span class="sxs-lookup"><span data-stu-id="c5c96-155">This will create a scaffolded Azure Mobile Apps backend in hello `out` directory.</span></span>  <span data-ttu-id="c5c96-156">Gerekli değildir, ancak bir fikir toocheck hello olduğu `out` tercih ettiğiniz bir kaynak kod havuzunda dizin.</span><span class="sxs-lookup"><span data-stu-id="c5c96-156">Although not required, it's a good idea toocheck hello `out` directory into a source code repository of your choice.</span></span>

## <span data-ttu-id="c5c96-157"><a name="deploy-ama-app"></a>Azure Mobile Apps arka dağıtma</span><span class="sxs-lookup"><span data-stu-id="c5c96-157"><a name="deploy-ama-app"></a> Deploy your Azure Mobile Apps backend</span></span>
<span data-ttu-id="c5c96-158">Dağıtım sırasında toodo hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="c5c96-158">During deployment, you will need toodo hello following:</span></span>

1. <span data-ttu-id="c5c96-159">Yeni bir mobil uygulaması hello oluşturma [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="c5c96-159">Create a new Mobile App in hello [Azure Portal].</span></span>
2. <span data-ttu-id="c5c96-160">Merhaba çalıştırmak `createViews.sql` bağlı veritabanınızı komut.</span><span class="sxs-lookup"><span data-stu-id="c5c96-160">Run hello `createViews.sql` script on your connected database.</span></span>
3. <span data-ttu-id="c5c96-161">Bağlantılı tooyour mobil hizmeti tooyour bağlantı hello veritabanını yeni uygulama hizmeti.</span><span class="sxs-lookup"><span data-stu-id="c5c96-161">Link hello database that is linked tooyour Mobile Service tooyour new App Service.</span></span>
4. <span data-ttu-id="c5c96-162">Diğer kaynaklar (örneğin, bildirim hub'ları) toohello bağlantı yeni uygulama hizmeti.</span><span class="sxs-lookup"><span data-stu-id="c5c96-162">Link any other resources (such as Notification Hubs) toohello new App Service.</span></span>
5. <span data-ttu-id="c5c96-163">Oluşturulan hello kod tooyour yeni site dağıtın.</span><span class="sxs-lookup"><span data-stu-id="c5c96-163">Deploy hello generated code tooyour new site.</span></span>

### <a name="create-a-new-mobile-app"></a><span data-ttu-id="c5c96-164">Yeni bir mobil uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="c5c96-164">Create a new Mobile App</span></span>
1. <span data-ttu-id="c5c96-165">Merhaba oturum açma [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="c5c96-165">Log in at hello [Azure Portal].</span></span>
2. <span data-ttu-id="c5c96-166">**+YENİ** > **Web + Mobil** > **Mobil Uygulama**’ya tıklayıp Mobile Uygulama arka ucu için bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="c5c96-166">Click **+NEW** > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="c5c96-167">Hello için **kaynak grubu**, varolan bir kaynak grubu seçin veya yeni bir tane oluşturun (kullanarak Merhaba, uygulamanızın adıyla aynı.)</span><span class="sxs-lookup"><span data-stu-id="c5c96-167">For hello **Resource Group**, select an existing resource group, or create a new one (using hello same name as your app.)</span></span>

    <span data-ttu-id="c5c96-168">Başka bir App Service planı seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c5c96-168">You can either select another App Service plan or create a new one.</span></span> <span data-ttu-id="c5c96-169">Uygulama Hizmetleri planları ve nasıl toocreate farklı fiyatlandırma içinde yeni bir plan katmanı ve tercih ettiğiniz konumda bkz hakkında daha fazla bilgi için [Azure App Service planlarına ayrıntılı genel bakış](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c5c96-169">For more about App Services plans and how toocreate a new plan in a different pricing tier and in your desired location, see [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
4. <span data-ttu-id="c5c96-170">Hello için **uygulama hizmeti planı**, hello varsayılan plan (Merhaba içinde [standart katmanı](https://azure.microsoft.com/pricing/details/app-service/)) seçilidir.</span><span class="sxs-lookup"><span data-stu-id="c5c96-170">For hello **App Service plan**, hello default plan (in hello [Standard tier](https://azure.microsoft.com/pricing/details/app-service/)) is selected.</span></span> <span data-ttu-id="c5c96-171">Aynı zamanda başka bir plan da seçebilir veya [yeni bir tane oluşturabilirsiniz](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="c5c96-171">You can also  select a different plan, or [create a new one](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan).</span></span> <span data-ttu-id="c5c96-172">Merhaba uygulama hizmeti planının ayarları belirlemek hello [konumu, özellikleri, maliyeti ve işlem kaynaklarını](https://azure.microsoft.com/pricing/details/app-service/) uygulamanızla ilişkili.</span><span class="sxs-lookup"><span data-stu-id="c5c96-172">hello App Service plan's settings determine hello [location, features, cost and compute resources](https://azure.microsoft.com/pricing/details/app-service/) associated with your app.</span></span>

    <span data-ttu-id="c5c96-173">Merhaba planla ilgili kararı verdikten sonra tıklayın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="c5c96-173">After you decide on hello plan, click **Create**.</span></span> <span data-ttu-id="c5c96-174">Merhaba mobil uygulama arka ucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c5c96-174">This creates hello Mobile App backend.</span></span>

### <a name="run-createviewssql"></a><span data-ttu-id="c5c96-175">CreateViews.SQL Çalıştır</span><span class="sxs-lookup"><span data-stu-id="c5c96-175">Run CreateViews.SQL</span></span>
<span data-ttu-id="c5c96-176">Merhaba kurulmuş uygulama adlı bir dosyayı içeren `createViews.sql`.</span><span class="sxs-lookup"><span data-stu-id="c5c96-176">hello scaffolded app contains a file called `createViews.sql`.</span></span>  <span data-ttu-id="c5c96-177">Bu komut dosyasını hedef veritabanında yürütülmelidir.</span><span class="sxs-lookup"><span data-stu-id="c5c96-177">This script must be executed against the target database.</span></span>  <span data-ttu-id="c5c96-178">Merhaba hello hedef veritabanı için bağlantı dizesini elde edilebilir geçirilen mobil hizmetinizden hello gelen **ayarları** altında dikey **bağlantı dizeleri**.</span><span class="sxs-lookup"><span data-stu-id="c5c96-178">hello connection string for hello target database can be obtained from your migrated mobile service from hello **Settings** blade under **Connection Strings**.</span></span>  <span data-ttu-id="c5c96-179">Bu adlı `MS_TableConnectionString`.</span><span class="sxs-lookup"><span data-stu-id="c5c96-179">It is named `MS_TableConnectionString`.</span></span>

<span data-ttu-id="c5c96-180">Bu komut dosyasından SQL Server Management Studio veya Visual Studio içinde çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c5c96-180">You can run this script from within SQL Server Management Studio or Visual Studio.</span></span>

### <a name="link-hello-database-tooyour-app-service"></a><span data-ttu-id="c5c96-181">Bağlantı hello veritabanı tooyour uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="c5c96-181">Link hello Database tooyour App Service</span></span>
<span data-ttu-id="c5c96-182">Merhaba varolan veritabanı tooyour uygulama hizmeti bağlantı:</span><span class="sxs-lookup"><span data-stu-id="c5c96-182">Link hello existing database tooyour App Service:</span></span>

* <span data-ttu-id="c5c96-183">Merhaba, [Azure Portal], uygulama hizmetiniz açın.</span><span class="sxs-lookup"><span data-stu-id="c5c96-183">In hello [Azure Portal], open your App Service.</span></span>
* <span data-ttu-id="c5c96-184">Seçin **tüm ayarları** -> **veri bağlantıları**.</span><span class="sxs-lookup"><span data-stu-id="c5c96-184">Select **All Settings** -> **Data Connections**.</span></span>
* <span data-ttu-id="c5c96-185">Tıklayın **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="c5c96-185">Click on **+ Add**.</span></span>
* <span data-ttu-id="c5c96-186">Hello açılır, seçin **SQL veritabanı**</span><span class="sxs-lookup"><span data-stu-id="c5c96-186">In hello drop-down, select **SQL Database**</span></span>
* <span data-ttu-id="c5c96-187">Altında **SQL veritabanı**mevcut veritabanını seçin, ardından tıklayın **seçin**.</span><span class="sxs-lookup"><span data-stu-id="c5c96-187">Under **SQL Database**, select your existing database, then click on **Select**.</span></span>
* <span data-ttu-id="c5c96-188">Altında **bağlantı dizesi**, hello veritabanı için hello kullanıcı adını ve parolasını girin, ardından tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="c5c96-188">Under **Connection string**, enter hello username and password for hello database, then click on **OK**.</span></span>
* <span data-ttu-id="c5c96-189">Merhaba, **veri bağlantıları ekleme** dikey penceresinde, tıklatıldığında **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="c5c96-189">In hello **Add data connections** blade, click on **OK**.</span></span>

<span data-ttu-id="c5c96-190">Merhaba kullanıcı adı ve parola geçirilen mobil hizmetinizi hello hedef veritabanı için bağlantı dizesi hello görüntüleyerek bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="c5c96-190">hello username and password can be found by viewing hello Connection String for hello target database in your migrated Mobile Service.</span></span>

### <a name="set-up-authentication"></a><span data-ttu-id="c5c96-191">Kimlik doğrulamasını ayarlama</span><span class="sxs-lookup"><span data-stu-id="c5c96-191">Set up authentication</span></span>
<span data-ttu-id="c5c96-192">Azure Mobile Apps tooconfigure Azure Active Directory, Facebook, Google, Microsoft ve Twitter kimlik doğrulaması hello hizmet içinde verir.</span><span class="sxs-lookup"><span data-stu-id="c5c96-192">Azure Mobile Apps allows you tooconfigure Azure Active Directory, Facebook, Google, Microsoft and Twitter authentication within hello service.</span></span>  <span data-ttu-id="c5c96-193">Özel kimlik doğrulama ayrı olarak geliştirilen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="c5c96-193">Custom authentication will need toobe developed separately.</span></span>  <span data-ttu-id="c5c96-194">Hello başvuran [kimlik doğrulaması kavramlarını] belgelerine ve [kimlik doğrulaması Hızlı Başlangıç] daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="c5c96-194">Refer to hello [Authentication Concepts] documentation and [Authentication Quickstart] documentation for more information.</span></span>  

## <span data-ttu-id="c5c96-195"><a name="updating-clients"></a>Mobil istemcilerin güncelleştir</span><span class="sxs-lookup"><span data-stu-id="c5c96-195"><a name="updating-clients"></a>Update Mobile clients</span></span>
<span data-ttu-id="c5c96-196">İşletimsel bir mobil uygulama arka ucu olduktan sonra hangi içereceği tükettiği istemci uygulamanızı yeni bir sürümünü çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c5c96-196">Once you have an operational Mobile App backend, you can work on a new version of your client application which consumes it.</span></span> <span data-ttu-id="c5c96-197">Mobile Apps istemci SDK'in hello yeni bir sürümünü de içerir ve benzer toohello sunucu yükseltme yukarıdaki, tüm başvurular toohello Mobile Services SDK'ları önce tooremove gerekir Mobile Apps sürümler yükleme.</span><span class="sxs-lookup"><span data-stu-id="c5c96-197">Mobile Apps also includes a new version of hello client SDKs, and similar toohello server upgrade above, you will need tooremove all references toohello Mobile Services SDKs before installing the Mobile Apps versions.</span></span>

<span data-ttu-id="c5c96-198">Merhaba ana değişiklikleri hello sürümleri arasında hello oluşturucular artık bir uygulama anahtarı iste biridir.</span><span class="sxs-lookup"><span data-stu-id="c5c96-198">One of hello main changes between hello versions is that hello constructors no longer require an application key.</span></span>
<span data-ttu-id="c5c96-199">Artık yalnızca mobil uygulamanızın hello URL'de geçirdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="c5c96-199">You now simply pass in hello URL of your Mobile App.</span></span> <span data-ttu-id="c5c96-200">Örneğin, hello .NET istemcilerde hello `MobileServiceClient` Oluşturucusu olan şimdi:</span><span class="sxs-lookup"><span data-stu-id="c5c96-200">For example, on hello .NET clients, hello `MobileServiceClient` constructor is now:</span></span>

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net" // URL of hello Mobile App
        );

<span data-ttu-id="c5c96-201">Yükleme hakkında bilgi edinebilirsiniz yeni SDK'ları hello ve aşağıdaki hello bağlantıları üzerinden hello yeni yapısını kullanarak:</span><span class="sxs-lookup"><span data-stu-id="c5c96-201">You can read about installing hello new SDKs and using hello new structure via hello links below:</span></span>

* [<span data-ttu-id="c5c96-202">Android 2.2 veya sonraki sürümü</span><span class="sxs-lookup"><span data-stu-id="c5c96-202">Android version 2.2 or later</span></span>](app-service-mobile-android-how-to-use-client-library.md)
* [<span data-ttu-id="c5c96-203">iOS sürüm 3.0.0 veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="c5c96-203">iOS version 3.0.0 or later</span></span>](app-service-mobile-ios-how-to-use-client-library.md)
* [<span data-ttu-id="c5c96-204">.NET (Windows/Xamarin) sürüm 2.0.0 veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="c5c96-204">.NET (Windows/Xamarin) version 2.0.0 or later</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)
* [<span data-ttu-id="c5c96-205">Apache Cordova sürüm 2.0 veya üstü</span><span class="sxs-lookup"><span data-stu-id="c5c96-205">Apache Cordova version 2.0 or later</span></span>](app-service-mobile-cordova-how-to-use-client-library.md)

<span data-ttu-id="c5c96-206">Olmuştur gibi bazı değişiklikler vardır de uygulamanız anında iletme bildirimleri kullanın, her platform için belirli kayıt yönergeleri hello Not yapıyorsa.</span><span class="sxs-lookup"><span data-stu-id="c5c96-206">If your application makes use of push notifications, make note of hello specific registration instructions for each platform, as there have been some changes there as well.</span></span>

<span data-ttu-id="c5c96-207">Merhaba yeni istemci sürümü hazır olduğunda, yükseltilen sunucu projenizi karşı deneyin.</span><span class="sxs-lookup"><span data-stu-id="c5c96-207">When you have hello new client version ready, try it out against your upgraded server project.</span></span> <span data-ttu-id="c5c96-208">Çalışır durumda olduğunu doğrulandıktan sonra uygulama toocustomers yeni bir sürümü serbest bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c5c96-208">After validating that it works, you can release a new version of your application toocustomers.</span></span> <span data-ttu-id="c5c96-209">Sonuç olarak, müşterilerinizin bu güncelleştirmeler bir fırsat tooreceive beklendiğinden sonra hello Mobile Services sürümü, uygulamanızın silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c5c96-209">Eventually, once your customers have had a chance tooreceive these updates, you can delete hello Mobile Services version of your app.</span></span> <span data-ttu-id="c5c96-210">Bu noktada, tamamen tooan mobil uygulama hizmeti yükselttikten hello en son mobil uygulamalar sunucusu SDK kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c5c96-210">At this point, you have completely upgraded tooan App Service Mobile App using hello latest Mobile Apps server SDK.</span></span>

<!-- URLs. -->

[Azure portal]: https://portal.azure.com/
[Azure classic portal]: https://manage.windowsazure.com/
[Mobile Apps nedir?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: https://www.npmjs.com/package/azure-mobile-apps
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web Job]: ../app-service-web/websites-webjobs-resources.md
[How toouse hello .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[uygulama hizmeti fiyatlandırma]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[kimlik doğrulaması kavramlarını]: ../app-service/app-service-authentication-overview.md
[kimlik doğrulaması Hızlı Başlangıç]: app-service-mobile-auth.md

[Azure Portal]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js package]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
