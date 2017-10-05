---
title: "Azure uygulama hizmeti - Node.js için Mobile Services'den yükseltme"
description: "Bir mobil uygulama hizmeti Mobile Services uygulamanıza kolayca yükseltmeyi öğrenin"
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
ms.openlocfilehash: ce0572e85c258aa377c3eea7923d43a30c935bb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="upgrade-your-existing-nodejs-azure-mobile-service-to-app-service"></a><span data-ttu-id="95c67-103">Varolan Node.js Azure mobil hizmetinizi App Service'e yükseltme</span><span class="sxs-lookup"><span data-stu-id="95c67-103">Upgrade your existing Node.js Azure Mobile Service to App Service</span></span>
<span data-ttu-id="95c67-104">App Service Mobile, Microsoft Azure kullanarak mobil uygulamaları oluşturmak için yeni bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="95c67-104">App Service Mobile is a new way to build mobile applications using Microsoft Azure.</span></span> <span data-ttu-id="95c67-105">Daha fazla bilgi için bkz: [Mobile Apps nedir?].</span><span class="sxs-lookup"><span data-stu-id="95c67-105">To learn more, see [What are Mobile Apps?].</span></span>

<span data-ttu-id="95c67-106">Bu konu, mevcut Node.js arka uç uygulama için yeni bir App Service Mobile Apps Azure Mobile Services yükseltme açıklar.</span><span class="sxs-lookup"><span data-stu-id="95c67-106">This topic describes how to upgrade an existing Node.js backend application from Azure Mobile Services to a new App Service Mobile Apps.</span></span> <span data-ttu-id="95c67-107">Bu yükseltme gerçekleştirirken mevcut Mobile Services uygulamanız çalışmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95c67-107">While you perform this upgrade, your existing Mobile Services application can continue to operate.</span></span>  <span data-ttu-id="95c67-108">Bir Node.js arka uç uygulaması yükseltme yapmanız oluştuysa, [.NET Mobile Services yükseltme](app-service-mobile-net-upgrading-from-mobile-services.md).</span><span class="sxs-lookup"><span data-stu-id="95c67-108">If you need to upgrade a Node.js backend application, refer to [Upgrading your .NET Mobile Services](app-service-mobile-net-upgrading-from-mobile-services.md).</span></span>

<span data-ttu-id="95c67-109">Azure App Service'e bir mobil arka uç yükseltildiğinde, tüm uygulama hizmeti özelliklerine erişebilir ve göre faturalandırılır [uygulama hizmeti fiyatlandırma], fiyatlandırma değil Mobile Services.</span><span class="sxs-lookup"><span data-stu-id="95c67-109">When a mobile backend is upgraded to Azure App Service, it has access to all App Service features and are billed according to [App Service pricing], not Mobile Services pricing.</span></span>

## <a name="migrate-vs-upgrade"></a><span data-ttu-id="95c67-110">Yükseltme geçirme</span><span class="sxs-lookup"><span data-stu-id="95c67-110">Migrate vs. upgrade</span></span>
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> <span data-ttu-id="95c67-111">Önerilir Bu, [bir geçiş gerçekleştirmek](app-service-mobile-migrating-from-mobile-services.md) yükseltme geçmeden önce.</span><span class="sxs-lookup"><span data-stu-id="95c67-111">It is recommended that you [perform a migration](app-service-mobile-migrating-from-mobile-services.md) before going through an upgrade.</span></span> <span data-ttu-id="95c67-112">Bu şekilde, aynı uygulama hizmeti planı üzerinde her iki sürümü, uygulamanızın koyun ve ek bir maliyet doğurur.</span><span class="sxs-lookup"><span data-stu-id="95c67-112">This way, you can put both versions of your application on the same App Service Plan and incur no additional cost.</span></span>
>
>

### <a name="improvements-in-mobile-apps-nodejs-server-sdk"></a><span data-ttu-id="95c67-113">Mobile Apps Node.js sunucusu SDK yenilikleri</span><span class="sxs-lookup"><span data-stu-id="95c67-113">Improvements in Mobile Apps Node.js server SDK</span></span>
<span data-ttu-id="95c67-114">Yeni yükseltme [Mobile Apps SDK'sı](https://www.npmjs.com/package/azure-mobile-apps) iyileştirmeler de dahil olmak üzere birçok sağlar:</span><span class="sxs-lookup"><span data-stu-id="95c67-114">Upgrading to the new [Mobile Apps SDK](https://www.npmjs.com/package/azure-mobile-apps) provides a lot of improvements, including:</span></span>

* <span data-ttu-id="95c67-115">Temel [Express framework](http://expressjs.com/en/index.html), yeni bir düğüm SDK hafif ve geldikleri gibi yeni düğümü sürümlerle karşılamak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="95c67-115">Based on the [Express framework](http://expressjs.com/en/index.html), the new Node SDK is light-weight and designed to keep up with new Node versions as they come out.</span></span> <span data-ttu-id="95c67-116">Express ara yazılımını ile uygulama davranışını özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95c67-116">You can customize the application behavior with Express middleware.</span></span>
* <span data-ttu-id="95c67-117">Mobile Services SDK'sına göre önemli performans geliştirmeleri.</span><span class="sxs-lookup"><span data-stu-id="95c67-117">Significant performance improvements compared to the Mobile Services SDK.</span></span>
* <span data-ttu-id="95c67-118">Bir Web sitesi ile birlikte mobil arka şimdi barındırabilir; benzer şekilde, tüm mevcut express.v4 uygulamaya Azure Mobile SDK'sı ekleme kolaydır.</span><span class="sxs-lookup"><span data-stu-id="95c67-118">You can now host a website together with your mobile backend; similarly, it's easy to add the Azure Mobile SDK to any existing express.v4 application.</span></span>
* <span data-ttu-id="95c67-119">Platformlar arası ve yerel geliştirme için yerleşik, Mobile Apps SDK'sı geliştirilen ve yerel olarak Windows, Linux ve OSX platformlarda çalıştırmak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95c67-119">Built for cross-platform and local development, the Mobile Apps SDK can be developed and run locally on Windows, Linux, and OSX platforms.</span></span> <span data-ttu-id="95c67-120">Şimdi çalışıyor gibi kullanımı kolay ortak düğüm geliştirme teknikleri olan [Mocha](https://mochajs.org/) testleri dağıtımından önce.</span><span class="sxs-lookup"><span data-stu-id="95c67-120">It's now easy to use common Node development techniques like running [Mocha](https://mochajs.org/) tests prior to deployment.</span></span>

## <span data-ttu-id="95c67-121"><a name="overview"></a>Temel yükseltmeye genel bakış</span><span class="sxs-lookup"><span data-stu-id="95c67-121"><a name="overview"></a>Basic upgrade overview</span></span>
<span data-ttu-id="95c67-122">Node.js arka ucu yükseltme yardımcı olmak için Azure App Service uyumluluğu paketi sağlamıştır.</span><span class="sxs-lookup"><span data-stu-id="95c67-122">To aid in upgrading a Node.js backend, Azure App Service has provided a compatibility package.</span></span>  <span data-ttu-id="95c67-123">Yükseltmeden sonra yeni bir uygulama hizmeti siteye dağıtılabilir bir niew sitesi olur.</span><span class="sxs-lookup"><span data-stu-id="95c67-123">After upgrade, you will have a niew site that can be deployed to a new App Service site.</span></span>

<span data-ttu-id="95c67-124">Mobile Services istemci SDK'ları olan **değil** yeni mobil uygulamalar sunucusu SDK ile uyumlu.</span><span class="sxs-lookup"><span data-stu-id="95c67-124">The Mobile Services client SDKs are **not** compatible with the new Mobile Apps server SDK.</span></span> <span data-ttu-id="95c67-125">Uygulamanız için hizmetin sürekliliği sağlamak için değişiklikleri şu anda yayımlanan istemciler hizmet veren bir site yayınlamalıdır değil.</span><span class="sxs-lookup"><span data-stu-id="95c67-125">In order to provide continuity of service for your app, you should not publish changes to a site currently serving published clients.</span></span> <span data-ttu-id="95c67-126">Bunun yerine, yinelenen hizmet veren yeni bir mobil uygulama oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="95c67-126">Instead, you should create a new mobile app that serves as a duplicate.</span></span> <span data-ttu-id="95c67-127">Bu uygulamayı ek finansal ücret oluşmasını önlemek için aynı uygulama hizmeti plan üzerinde koyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95c67-127">You can put this application on the same App Service plan to avoid incurring additional financial cost.</span></span>

<span data-ttu-id="95c67-128">Uygulamanın iki sürümlerini sonra gerekir: aynı kalır ve hizmet veren bir yayımlanan uygulamalar joker diğer, ardından yükseltin ve yeni bir istemci sürümü ile hedef.</span><span class="sxs-lookup"><span data-stu-id="95c67-128">You will then have two versions of the application: one that stays the same and serves published apps in the wild, and the other which you can then upgrade and target with a new client release.</span></span> <span data-ttu-id="95c67-129">Taşıma ve kodunuzu test etmek, hızı, ancak yaptığınız tüm hata düzeltmeleri hem de uygulandığından emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="95c67-129">You can move and test your code at your pace, but you should make sure that any bug fixes you make get applied to both.</span></span> <span data-ttu-id="95c67-130">İstediğiniz istemci uygulamaları yazılımların en son sürüme güncelleştirilmemiş istenen sayısını, özgün geçirilen uygulama silebilirsiniz olduğunu düşündüğünüz sonra.</span><span class="sxs-lookup"><span data-stu-id="95c67-130">Once you feel that a desired number of client apps in the wild have updated to the latest version, you can delete the original migrated app if you desire.</span></span> <span data-ttu-id="95c67-131">Mobil uygulamanızın aynı uygulama hizmeti planında barındırılan kullanılıyorsa, tüm ek para ücrete neden değil.</span><span class="sxs-lookup"><span data-stu-id="95c67-131">It doesn't incur any additional monetary costs, if hosted in the same App Service plan as your Mobile App.</span></span>

<span data-ttu-id="95c67-132">Yükseltme işlemi için tam anahattı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="95c67-132">The full outline for the upgrade process is as follows:</span></span>

1. <span data-ttu-id="95c67-133">Mevcut (geçirilen) Azure mobil hizmetiniz indirin.</span><span class="sxs-lookup"><span data-stu-id="95c67-133">Download your existing (migrated) Azure Mobile Service.</span></span>
2. <span data-ttu-id="95c67-134">Proje Uyumluluk Paketi kullanarak bir Azure mobil uygulaması dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="95c67-134">Convert the project to an Azure Mobile App using the compatibility package.</span></span>
3. <span data-ttu-id="95c67-135">Farkları (örneğin, kimlik doğrulama ayarları) düzeltin.</span><span class="sxs-lookup"><span data-stu-id="95c67-135">Correct any differences (such as authentication settings).</span></span>
4. <span data-ttu-id="95c67-136">Dönüştürülen Azure mobil uygulaması projeniz için yeni bir uygulama hizmeti dağıtın.</span><span class="sxs-lookup"><span data-stu-id="95c67-136">Deploy your converted Azure Mobile App project to a new App Service.</span></span>
5. <span data-ttu-id="95c67-137">Yeni mobil uygulamayı istemci uygulamanızı yeni bir sürümü kullanıma.</span><span class="sxs-lookup"><span data-stu-id="95c67-137">Release a new version of your client application that use the new Mobile App.</span></span>
6. <span data-ttu-id="95c67-138">(İsteğe bağlı) Özgün geçirilen mobil hizmet uygulamanızı silin.</span><span class="sxs-lookup"><span data-stu-id="95c67-138">(Optional) Delete your original migrated mobile service app.</span></span>

<span data-ttu-id="95c67-139">Özgün geçirilen mobil hizmette herhangi bir trafik görmüyorum silme ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="95c67-139">Deletion can occur when you don't see any traffic on your original migrated mobile service.</span></span>

## <span data-ttu-id="95c67-140"><a name="install-npm-package"></a>Önkoşulları yüklemek</span><span class="sxs-lookup"><span data-stu-id="95c67-140"><a name="install-npm-package"></a> Install the Pre-requisites</span></span>
<span data-ttu-id="95c67-141">Yerel makinenizde [Node] yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="95c67-141">You should install [Node] on your local machine.</span></span>  <span data-ttu-id="95c67-142">Uyumluluk Paketi de yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="95c67-142">You should also install the compatibility package.</span></span>  <span data-ttu-id="95c67-143">Düğüm yüklendikten sonra yeni cmd ya da PowerShell komut isteminde aşağıdaki komutu çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="95c67-143">After Node is installed, you can run the following command from a new cmd or PowerShell prompt:</span></span>

```npm i -g azure-mobile-apps-compatibility```

## <span data-ttu-id="95c67-144"><a name="obtain-ams-scripts"></a>Azure mobil hizmetler komut dosyalarınız alın</span><span class="sxs-lookup"><span data-stu-id="95c67-144"><a name="obtain-ams-scripts"></a> Obtain your Azure Mobile Services Scripts</span></span>
* <span data-ttu-id="95c67-145">[Azure Portal]’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="95c67-145">Log in to the [Azure Portal].</span></span>
* <span data-ttu-id="95c67-146">Kullanarak **tüm kaynakları** veya **uygulama hizmetleri**, Mobile Services sitenizi bulun.</span><span class="sxs-lookup"><span data-stu-id="95c67-146">Using **All Resources** or **App Services**, find your Mobile Services site.</span></span>
* <span data-ttu-id="95c67-147">Site içinde tıklayın **Araçları** -> **Kudu** -> **Git** Kudu sitesini açın.</span><span class="sxs-lookup"><span data-stu-id="95c67-147">Within the site, click on **Tools** -> **Kudu** -> **Go** to open the Kudu site.</span></span>
* <span data-ttu-id="95c67-148">Tıklayın **hata ayıklama Konsolu'nda** -> **PowerShell** hata ayıklama konsolunu açın.</span><span class="sxs-lookup"><span data-stu-id="95c67-148">Click on **Debug Console** -> **PowerShell** to open the Debug console.</span></span>
* <span data-ttu-id="95c67-149">Gidin `site/wwwroot/App_Data/config` her bir dizinin sırayla tıklayarak</span><span class="sxs-lookup"><span data-stu-id="95c67-149">Navigate to `site/wwwroot/App_Data/config` by clicking on each directory in turn</span></span>
* <span data-ttu-id="95c67-150">İndirme simgesine tıklayın `scripts` dizin.</span><span class="sxs-lookup"><span data-stu-id="95c67-150">Click on the download icon next to the `scripts` directory.</span></span>

<span data-ttu-id="95c67-151">Bu komut dosyaları ZIP biçiminde indirir.</span><span class="sxs-lookup"><span data-stu-id="95c67-151">This will download the scripts in ZIP format.</span></span>  <span data-ttu-id="95c67-152">Yerel makinenizde yeni bir dizin oluşturun ve paket `scripts.ZIP` dizin içindeki dosya.</span><span class="sxs-lookup"><span data-stu-id="95c67-152">Create a new directory on your local machine and unpack the `scripts.ZIP` file within the directory.</span></span>  <span data-ttu-id="95c67-153">Bu oluşturacak bir `scripts` dizin.</span><span class="sxs-lookup"><span data-stu-id="95c67-153">This will create a `scripts` directory.</span></span>

## <span data-ttu-id="95c67-154"><a name="scaffold-app"></a>Yeni Azure Mobile Apps arka iskele</span><span class="sxs-lookup"><span data-stu-id="95c67-154"><a name="scaffold-app"></a> Scaffold the new Azure Mobile Apps backend</span></span>
<span data-ttu-id="95c67-155">Komut dosyaları dizinini içeren dizininden aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="95c67-155">Run the following command from the directory containing the scripts directory:</span></span>

```scaffold-mobile-app scripts out```

<span data-ttu-id="95c67-156">Bu kurulmuş bir Azure Mobile Apps arka ucu oluşturacak `out` dizin.</span><span class="sxs-lookup"><span data-stu-id="95c67-156">This will create a scaffolded Azure Mobile Apps backend in the `out` directory.</span></span>  <span data-ttu-id="95c67-157">Gerekli değildir, ancak bunu denetlemek için iyi bir fikirdir `out` tercih ettiğiniz bir kaynak kod havuzunda dizin.</span><span class="sxs-lookup"><span data-stu-id="95c67-157">Although not required, it's a good idea to check the `out` directory into a source code repository of your choice.</span></span>

## <span data-ttu-id="95c67-158"><a name="deploy-ama-app"></a>Azure Mobile Apps arka dağıtma</span><span class="sxs-lookup"><span data-stu-id="95c67-158"><a name="deploy-ama-app"></a> Deploy your Azure Mobile Apps backend</span></span>
<span data-ttu-id="95c67-159">Dağıtım sırasında aşağıdakileri yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="95c67-159">During deployment, you will need to do the following:</span></span>

1. <span data-ttu-id="95c67-160">Yeni bir mobil uygulaması oluşturmak [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="95c67-160">Create a new Mobile App in the [Azure Portal].</span></span>
2. <span data-ttu-id="95c67-161">Çalıştırma `createViews.sql` bağlı veritabanınızı komut.</span><span class="sxs-lookup"><span data-stu-id="95c67-161">Run the `createViews.sql` script on your connected database.</span></span>
3. <span data-ttu-id="95c67-162">Yeni uygulama hizmetiniz için mobil hizmetinize bağlı veritabanı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="95c67-162">Link the database that is linked to your Mobile Service to your new App Service.</span></span>
4. <span data-ttu-id="95c67-163">Yeni uygulama hizmeti (gibi bildirim hub'ları) başka kaynaklar bağlayın.</span><span class="sxs-lookup"><span data-stu-id="95c67-163">Link any other resources (such as Notification Hubs) to the new App Service.</span></span>
5. <span data-ttu-id="95c67-164">Oluşturulan kod yeni sitenize dağıtın.</span><span class="sxs-lookup"><span data-stu-id="95c67-164">Deploy the generated code to your new site.</span></span>

### <a name="create-a-new-mobile-app"></a><span data-ttu-id="95c67-165">Yeni bir mobil uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="95c67-165">Create a new Mobile App</span></span>
1. <span data-ttu-id="95c67-166">[Azure Portal]’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="95c67-166">Log in at the [Azure Portal].</span></span>
2. <span data-ttu-id="95c67-167">**+YENİ** > **Web + Mobil** > **Mobil Uygulama**’ya tıklayıp Mobile Uygulama arka ucu için bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="95c67-167">Click **+NEW** > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="95c67-168">**Kaynak Grubu** için yeni bir kaynak grubu seçin ya da yeni bir tane oluşturun (uygulamanızla aynı adı kullanarak).</span><span class="sxs-lookup"><span data-stu-id="95c67-168">For the **Resource Group**, select an existing resource group, or create a new one (using the same name as your app.)</span></span>

    <span data-ttu-id="95c67-169">Başka bir App Service planı seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="95c67-169">You can either select another App Service plan or create a new one.</span></span> <span data-ttu-id="95c67-170">Uygulama hizmetleri hakkında daha fazla bilgi için planları ve farklı fiyatlandırma yeni bir plan oluşturmak nasıl katmanı ve tercih ettiğiniz konumda bkz [Azure App Service planlarına ayrıntılı genel bakış](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="95c67-170">For more about App Services plans and how to create a new plan in a different pricing tier and in your desired location, see [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
4. <span data-ttu-id="95c67-171">**App Service planı** için, varsayılan plan ([Standart katman](https://azure.microsoft.com/pricing/details/app-service/)’da) seçilidir.</span><span class="sxs-lookup"><span data-stu-id="95c67-171">For the **App Service plan**, the default plan (in the [Standard tier](https://azure.microsoft.com/pricing/details/app-service/)) is selected.</span></span> <span data-ttu-id="95c67-172">Aynı zamanda başka bir plan da seçebilir veya [yeni bir tane oluşturabilirsiniz](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="95c67-172">You can also  select a different plan, or [create a new one](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan).</span></span> <span data-ttu-id="95c67-173">App Service planının ayarları, uygulamanızla ilişkili [konumu, özellikleri, maliyeti ve işlem kaynaklarını](https://azure.microsoft.com/pricing/details/app-service/) saptar.</span><span class="sxs-lookup"><span data-stu-id="95c67-173">The App Service plan's settings determine the [location, features, cost and compute resources](https://azure.microsoft.com/pricing/details/app-service/) associated with your app.</span></span>

    <span data-ttu-id="95c67-174">Planla ilgili kararı verdikten sonra **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="95c67-174">After you decide on the plan, click **Create**.</span></span> <span data-ttu-id="95c67-175">Böylece Mobil Uygulama arka uç oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="95c67-175">This creates the Mobile App backend.</span></span>

### <a name="run-createviewssql"></a><span data-ttu-id="95c67-176">CreateViews.SQL Çalıştır</span><span class="sxs-lookup"><span data-stu-id="95c67-176">Run CreateViews.SQL</span></span>
<span data-ttu-id="95c67-177">Adlı bir dosya kurulmuş uygulamasını içeren `createViews.sql`.</span><span class="sxs-lookup"><span data-stu-id="95c67-177">The scaffolded app contains a file called `createViews.sql`.</span></span>  <span data-ttu-id="95c67-178">Bu komut dosyasını hedef veritabanında yürütülmelidir.</span><span class="sxs-lookup"><span data-stu-id="95c67-178">This script must be executed against the target database.</span></span>  <span data-ttu-id="95c67-179">Hedef veritabanı için bağlantı dizesi geçirilen mobil hizmetinden gelen elde edilebilir **ayarları** altında dikey **bağlantı dizeleri**.</span><span class="sxs-lookup"><span data-stu-id="95c67-179">The connection string for the target database can be obtained from your migrated mobile service from the **Settings** blade under **Connection Strings**.</span></span>  <span data-ttu-id="95c67-180">Bu adlı `MS_TableConnectionString`.</span><span class="sxs-lookup"><span data-stu-id="95c67-180">It is named `MS_TableConnectionString`.</span></span>

<span data-ttu-id="95c67-181">Bu komut dosyasından SQL Server Management Studio veya Visual Studio içinde çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95c67-181">You can run this script from within SQL Server Management Studio or Visual Studio.</span></span>

### <a name="link-the-database-to-your-app-service"></a><span data-ttu-id="95c67-182">Uygulama hizmetiniz için veritabanı bağlantı</span><span class="sxs-lookup"><span data-stu-id="95c67-182">Link the Database to your App Service</span></span>
<span data-ttu-id="95c67-183">Varolan bir veritabanını uygulama hizmetiniz için bağlantı:</span><span class="sxs-lookup"><span data-stu-id="95c67-183">Link the existing database to your App Service:</span></span>

* <span data-ttu-id="95c67-184">İçinde [Azure Portal], uygulama hizmetiniz açın.</span><span class="sxs-lookup"><span data-stu-id="95c67-184">In the [Azure Portal], open your App Service.</span></span>
* <span data-ttu-id="95c67-185">Seçin **tüm ayarları** -> **veri bağlantıları**.</span><span class="sxs-lookup"><span data-stu-id="95c67-185">Select **All Settings** -> **Data Connections**.</span></span>
* <span data-ttu-id="95c67-186">Tıklayın **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="95c67-186">Click on **+ Add**.</span></span>
* <span data-ttu-id="95c67-187">Aşağı açılır menüsünde, seçin **SQL veritabanı**</span><span class="sxs-lookup"><span data-stu-id="95c67-187">In the drop-down, select **SQL Database**</span></span>
* <span data-ttu-id="95c67-188">Altında **SQL veritabanı**mevcut veritabanını seçin, ardından tıklayın **seçin**.</span><span class="sxs-lookup"><span data-stu-id="95c67-188">Under **SQL Database**, select your existing database, then click on **Select**.</span></span>
* <span data-ttu-id="95c67-189">Altında **bağlantı dizesi**, veritabanı için kullanıcı adını ve parolasını girin, ardından tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="95c67-189">Under **Connection string**, enter the username and password for the database, then click on **OK**.</span></span>
* <span data-ttu-id="95c67-190">İçinde **veri bağlantıları ekleme** dikey penceresinde, tıklatıldığında **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="95c67-190">In the **Add data connections** blade, click on **OK**.</span></span>

<span data-ttu-id="95c67-191">Kullanıcı adı ve parola geçirilen mobil hizmetinizi hedef veritabanı için bağlantı dizesini görüntüleyerek bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="95c67-191">The username and password can be found by viewing the Connection String for the target database in your migrated Mobile Service.</span></span>

### <a name="set-up-authentication"></a><span data-ttu-id="95c67-192">Kimlik doğrulamasını ayarlama</span><span class="sxs-lookup"><span data-stu-id="95c67-192">Set up authentication</span></span>
<span data-ttu-id="95c67-193">Azure Mobile Apps, Azure Active Directory, Facebook, Google, Microsoft ve Twitter kimlik doğrulama hizmeti içinde yapılandırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="95c67-193">Azure Mobile Apps allows you to configure Azure Active Directory, Facebook, Google, Microsoft and Twitter authentication within the service.</span></span>  <span data-ttu-id="95c67-194">Özel kimlik doğrulama ayrı olarak geliştirilen gerekir.</span><span class="sxs-lookup"><span data-stu-id="95c67-194">Custom authentication will need to be developed separately.</span></span>  <span data-ttu-id="95c67-195">Başvurmak [kimlik doğrulaması kavramlarını] belgelerine ve [kimlik doğrulaması Hızlı Başlangıç] daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="95c67-195">Refer to the [Authentication Concepts] documentation and [Authentication Quickstart] documentation for more information.</span></span>  

## <span data-ttu-id="95c67-196"><a name="updating-clients"></a>Mobil istemcilerin güncelleştir</span><span class="sxs-lookup"><span data-stu-id="95c67-196"><a name="updating-clients"></a>Update Mobile clients</span></span>
<span data-ttu-id="95c67-197">İşletimsel bir mobil uygulama arka ucu olduktan sonra hangi içereceği tükettiği istemci uygulamanızı yeni bir sürümünü çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95c67-197">Once you have an operational Mobile App backend, you can work on a new version of your client application which consumes it.</span></span> <span data-ttu-id="95c67-198">Mobile Apps istemci SDK ' yeni bir sürümünü de içerir ve benzer sunucu yükseltme için Mobile Apps sürümleri yüklemeden önce Mobile Services SDK'ları tüm başvurularını kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="95c67-198">Mobile Apps also includes a new version of the client SDKs, and similar to the server upgrade above, you will need to remove all references to the Mobile Services SDKs before installing the Mobile Apps versions.</span></span>

<span data-ttu-id="95c67-199">Sürümleri arasında ana değişikliklerden birini oluşturucular artık bir uygulama anahtarı gerekmesidir.</span><span class="sxs-lookup"><span data-stu-id="95c67-199">One of the main changes between the versions is that the constructors no longer require an application key.</span></span>
<span data-ttu-id="95c67-200">Artık yalnızca mobil uygulamanızın URL'de geçirdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="95c67-200">You now simply pass in the URL of your Mobile App.</span></span> <span data-ttu-id="95c67-201">Örneğin, .NET istemcilerde `MobileServiceClient` Oluşturucusu olan şimdi:</span><span class="sxs-lookup"><span data-stu-id="95c67-201">For example, on the .NET clients, the `MobileServiceClient` constructor is now:</span></span>

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net" // URL of the Mobile App
        );

<span data-ttu-id="95c67-202">Yeni SDK'ye yükleme ve yeni yapısı aşağıdaki bağlantıları üzerinden kullanma hakkında bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="95c67-202">You can read about installing the new SDKs and using the new structure via the links below:</span></span>

* [<span data-ttu-id="95c67-203">Android 2.2 veya sonraki sürümü</span><span class="sxs-lookup"><span data-stu-id="95c67-203">Android version 2.2 or later</span></span>](app-service-mobile-android-how-to-use-client-library.md)
* [<span data-ttu-id="95c67-204">iOS sürüm 3.0.0 veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="95c67-204">iOS version 3.0.0 or later</span></span>](app-service-mobile-ios-how-to-use-client-library.md)
* [<span data-ttu-id="95c67-205">.NET (Windows/Xamarin) sürüm 2.0.0 veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="95c67-205">.NET (Windows/Xamarin) version 2.0.0 or later</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)
* [<span data-ttu-id="95c67-206">Apache Cordova sürüm 2.0 veya üstü</span><span class="sxs-lookup"><span data-stu-id="95c67-206">Apache Cordova version 2.0 or later</span></span>](app-service-mobile-cordova-how-to-use-client-library.md)

<span data-ttu-id="95c67-207">Olmuştur gibi bazı değişiklikler vardır de uygulamanız anında iletme bildirimleri kullanın, her platform için belirli kayıt yönergeleri not yapıyorsa.</span><span class="sxs-lookup"><span data-stu-id="95c67-207">If your application makes use of push notifications, make note of the specific registration instructions for each platform, as there have been some changes there as well.</span></span>

<span data-ttu-id="95c67-208">Yeni istemci sürümü hazır olduğunda, yükseltilen sunucu projenizi karşı deneyin.</span><span class="sxs-lookup"><span data-stu-id="95c67-208">When you have the new client version ready, try it out against your upgraded server project.</span></span> <span data-ttu-id="95c67-209">Çalışır durumda olduğunu doğrulandıktan sonra müşterilere, uygulamanızın yeni bir sürüm serbest bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95c67-209">After validating that it works, you can release a new version of your application to customers.</span></span> <span data-ttu-id="95c67-210">Sonuç olarak, müşterilerinizin bu güncelleştirmeleri almak için bir fırsat beklendiğinden sonra uygulamanızın Mobile Services sürüm silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95c67-210">Eventually, once your customers have had a chance to receive these updates, you can delete the Mobile Services version of your app.</span></span> <span data-ttu-id="95c67-211">Bu noktada, bir mobil en son mobil uygulamalar sunucusu SDK kullanarak uygulama hizmeti için tamamen yükselttiniz.</span><span class="sxs-lookup"><span data-stu-id="95c67-211">At this point, you have completely upgraded to an App Service Mobile App using the latest Mobile Apps server SDK.</span></span>

<!-- URLs. -->

<span data-ttu-id="95c67-212">[Azure portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="95c67-212">[Azure portal]: https://portal.azure.com/</span></span>
[Azure classic portal]: https://manage.windowsazure.com/
<span data-ttu-id="95c67-213">[Mobile Apps nedir?]: app-service-mobile-value-prop.md</span><span class="sxs-lookup"><span data-stu-id="95c67-213">[What are Mobile Apps?]: app-service-mobile-value-prop.md</span></span>
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: https://www.npmjs.com/package/azure-mobile-apps
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications to your mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication to your mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web Job]: ../app-service-web/websites-webjobs-resources.md
[How to use the .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services to an App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service to App Service]: app-service-mobile-migrating-from-mobile-services.md
<span data-ttu-id="95c67-214">[uygulama hizmeti fiyatlandırma]: https://azure.microsoft.com/en-us/pricing/details/app-service/</span><span class="sxs-lookup"><span data-stu-id="95c67-214">[App Service pricing]: https://azure.microsoft.com/en-us/pricing/details/app-service/</span></span>
[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
<span data-ttu-id="95c67-215">[kimlik doğrulaması kavramlarını]: ../app-service/app-service-authentication-overview.md</span><span class="sxs-lookup"><span data-stu-id="95c67-215">[Authentication Concepts]: ../app-service/app-service-authentication-overview.md</span></span>
<span data-ttu-id="95c67-216">[kimlik doğrulaması Hızlı Başlangıç]: app-service-mobile-auth.md</span><span class="sxs-lookup"><span data-stu-id="95c67-216">[Authentication Quickstart]: app-service-mobile-auth.md</span></span>

<span data-ttu-id="95c67-217">[Azure Portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="95c67-217">[Azure Portal]: https://portal.azure.com/</span></span>
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
