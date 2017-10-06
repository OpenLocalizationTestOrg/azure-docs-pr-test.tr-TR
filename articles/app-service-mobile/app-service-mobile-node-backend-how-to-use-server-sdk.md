---
title: "Merhaba Node.js arka uç sunucusu için Mobile Apps SDK'sı ile aaaHow toowork | Microsoft Docs"
description: "Nasıl toowork ile Merhaba Node.js arka uç sunucusu SDK Azure App Service Mobile Apps için öğrenin."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a><span data-ttu-id="6e264-103">Nasıl toouse hello Azure Mobile Apps Node.js SDK'sı</span><span class="sxs-lookup"><span data-stu-id="6e264-103">How toouse hello Azure Mobile Apps Node.js SDK</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="6e264-104">Bu makalede ayrıntılı bilgi ve örnekler gösteren sağlar nasıl toowork Azure App Service Mobile Apps Node.js arka ucu ile.</span><span class="sxs-lookup"><span data-stu-id="6e264-104">This article provides detailed information and examples showing how toowork with a Node.js backend in Azure App Service Mobile Apps.</span></span>

## <span data-ttu-id="6e264-105"><a name="Introduction"></a>Giriş</span><span class="sxs-lookup"><span data-stu-id="6e264-105"><a name="Introduction"></a>Introduction</span></span>
<span data-ttu-id="6e264-106">Azure App Service Mobile Apps hello yetenek tooadd mobil iyileştirilmiş veri erişimi Web API tooa web uygulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="6e264-106">Azure App Service Mobile Apps provides hello capability tooadd a mobile-optimized data access Web API tooa web application.</span></span>  <span data-ttu-id="6e264-107">Hello Azure App Service Mobile Apps SDK'sı, ASP.NET ve Node.js web uygulamaları için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="6e264-107">hello Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span></span>  <span data-ttu-id="6e264-108">Merhaba SDK işlemleri aşağıdaki hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="6e264-108">hello SDK provides hello following operations:</span></span>

* <span data-ttu-id="6e264-109">Veri erişimi için tablo işlemleri (okuma, INSERT, Update, Delete)</span><span class="sxs-lookup"><span data-stu-id="6e264-109">Table operations (Read, Insert, Update, Delete) for data access</span></span>
* <span data-ttu-id="6e264-110">Özel API işlemleri</span><span class="sxs-lookup"><span data-stu-id="6e264-110">Custom API operations</span></span>

<span data-ttu-id="6e264-111">İki işlem kimlik doğrulaması için Kurumsal kimlik için Facebook, Twitter, Google ve Microsoft yanı sıra Azure Active Directory gibi sosyal kimlik sağlayıcıları dahil olmak üzere Azure App Service tarafından izin verilen tüm kimlik sağlayıcıları üzerinden sağlar.</span><span class="sxs-lookup"><span data-stu-id="6e264-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span></span>

<span data-ttu-id="6e264-112">Her için örnek kullanım örneği hello bulabilirsiniz [örnekler dizini github'da].</span><span class="sxs-lookup"><span data-stu-id="6e264-112">You can find samples for each use case in hello [samples directory on GitHub].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="6e264-113">Desteklenen platformlar</span><span class="sxs-lookup"><span data-stu-id="6e264-113">Supported Platforms</span></span>
<span data-ttu-id="6e264-114">Hello Azure Mobile Apps düğümü SDK sürüm düğümünün ve daha sonra geçerli LTS hello destekler.</span><span class="sxs-lookup"><span data-stu-id="6e264-114">hello Azure Mobile Apps Node SDK supports hello current LTS release of Node and later.</span></span>  <span data-ttu-id="6e264-115">Makalenin yazıldığı sırada hello son LTS düğümü v4.5.0 sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="6e264-115">As of writing, hello latest LTS version is Node v4.5.0.</span></span>  <span data-ttu-id="6e264-116">Düğüm'ın diğer sürümleri çalışabilir, ancak desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="6e264-116">Other versions of Node may work, but are not supported.</span></span>

<span data-ttu-id="6e264-117">iki veritabanı sürücüleri Hello Azure Mobile Apps düğümü SDK destekler - hello düğümü mssql sürücü SQL Azure ve yerel SQL Server örnekleri destekler.</span><span class="sxs-lookup"><span data-stu-id="6e264-117">hello Azure Mobile Apps Node SDK supports two database drivers - hello node-mssql driver supports SQL Azure and local SQL Server instances.</span></span>  <span data-ttu-id="6e264-118">Merhaba sqlite3 sürücü üzerinde yalnızca tek bir örneği SQLite veritabanlarını destekler.</span><span class="sxs-lookup"><span data-stu-id="6e264-118">hello sqlite3 driver supports SQLite databases on a single instance only.</span></span>

### <span data-ttu-id="6e264-119"><a name="howto-cmdline-basicapp"></a>Nasıl yapılır: hello komut satırını kullanarak bir temel Node.js arka ucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e264-119"><a name="howto-cmdline-basicapp"></a>How to: Create a Basic Node.js backend using hello Command Line</span></span>
<span data-ttu-id="6e264-120">Her Azure App Service Mobile uygulama Node.js arka ucu bir ExpressJS uygulamayı başlatır.</span><span class="sxs-lookup"><span data-stu-id="6e264-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span></span>  <span data-ttu-id="6e264-121">ExpressJS hello en popüler web service Node.js için kullanılabilir çerçevesidir.</span><span class="sxs-lookup"><span data-stu-id="6e264-121">ExpressJS is hello most popular web service framework available for Node.js.</span></span>  <span data-ttu-id="6e264-122">Temel bir oluşturabileceğiniz [Express] şekilde uygulama:</span><span class="sxs-lookup"><span data-stu-id="6e264-122">You can create a basic [Express] application as follows:</span></span>

1. <span data-ttu-id="6e264-123">Bir komut veya PowerShell penceresi projeniz için bir dizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6e264-123">In a command or PowerShell window, create a directory for your project.</span></span>

        mkdir basicapp
2. <span data-ttu-id="6e264-124">Npm init tooinitialize hello paket yapısı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6e264-124">Run npm init tooinitialize hello package structure.</span></span>

        cd basicapp
        npm init

    <span data-ttu-id="6e264-125">Merhaba npm init komutu soruları tooinitialize hello proje kümesi sorar.</span><span class="sxs-lookup"><span data-stu-id="6e264-125">hello npm init command asks a set of questions tooinitialize hello project.</span></span>  <span data-ttu-id="6e264-126">Merhaba örnek çıktı bakın:</span><span class="sxs-lookup"><span data-stu-id="6e264-126">See hello example output:</span></span>

    ![Merhaba npm init çıktı][0]
3. <span data-ttu-id="6e264-128">Merhaba express ve azure mobile apps kitaplıkları hello npm depodan yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6e264-128">Install hello express and azure-mobile-apps libraries from hello npm repository.</span></span>

        npm install --save express azure-mobile-apps
4. <span data-ttu-id="6e264-129">Bir app.js dosya tooimplement hello temel mobil sunucusu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6e264-129">Create an app.js file tooimplement hello basic mobile server.</span></span>

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

<span data-ttu-id="6e264-130">Bu uygulama ile tek bir uç noktası mobil iyileştirilmiş Webapı oluşturur (`/tables/TodoItem`) SQL veri deposu dinamik Şeması'nı kullanarak temel kimliği doğrulanmamış erişim tooan sağlar.</span><span class="sxs-lookup"><span data-stu-id="6e264-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access tooan underlying SQL data store using a dynamic schema.</span></span>  <span data-ttu-id="6e264-131">İstemci Kitaplığı hızlı başlangıçlar izlemek için uygundur:</span><span class="sxs-lookup"><span data-stu-id="6e264-131">It is suitable for following the client library quick starts:</span></span>

* <span data-ttu-id="6e264-132">[Android istemci hızlı başlangıç]</span><span class="sxs-lookup"><span data-stu-id="6e264-132">[Android Client QuickStart]</span></span>
* <span data-ttu-id="6e264-133">[Apache Cordova istemci hızlı başlangıç]</span><span class="sxs-lookup"><span data-stu-id="6e264-133">[Apache Cordova Client QuickStart]</span></span>
* <span data-ttu-id="6e264-134">[iOS istemci hızlı başlangıç]</span><span class="sxs-lookup"><span data-stu-id="6e264-134">[iOS Client QuickStart]</span></span>
* <span data-ttu-id="6e264-135">[Windows mağazası istemci hızlı başlangıç]</span><span class="sxs-lookup"><span data-stu-id="6e264-135">[Windows Store Client QuickStart]</span></span>
* <span data-ttu-id="6e264-136">[Xamarin.iOS istemcisi hızlı başlangıç]</span><span class="sxs-lookup"><span data-stu-id="6e264-136">[Xamarin.iOS Client QuickStart]</span></span>
* <span data-ttu-id="6e264-137">[Xamarin.Android istemcisi hızlı başlangıç]</span><span class="sxs-lookup"><span data-stu-id="6e264-137">[Xamarin.Android Client QuickStart]</span></span>
* <span data-ttu-id="6e264-138">[Xamarin.Forms istemci hızlı başlangıç]</span><span class="sxs-lookup"><span data-stu-id="6e264-138">[Xamarin.Forms Client QuickStart]</span></span>

<span data-ttu-id="6e264-139">Merhaba temel bu uygulamada hello kod bulabilirsiniz [basicapp örnek github'da].</span><span class="sxs-lookup"><span data-stu-id="6e264-139">You can find hello code for this basic application in hello [basicapp sample on GitHub].</span></span>

### <span data-ttu-id="6e264-140"><a name="howto-vs2015-basicapp"></a>Nasıl yapılır: Visual Studio 2015 ile birlikte bir düğüm arka ucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e264-140"><a name="howto-vs2015-basicapp"></a>How to: Create a Node backend with Visual Studio 2015</span></span>
<span data-ttu-id="6e264-141">Visual Studio 2015 uzantısı toodevelop Node.js uygulamalarını hello IDE içinde gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6e264-141">Visual Studio 2015 requires an extension toodevelop Node.js applications within hello IDE.</span></span>  <span data-ttu-id="6e264-142">toostart, yükleme hello [Visual Studio için Node.js araçları 1.1].</span><span class="sxs-lookup"><span data-stu-id="6e264-142">toostart, install hello [Node.js Tools 1.1 for Visual Studio].</span></span>  <span data-ttu-id="6e264-143">Merhaba Visual Studio için Node.js araçları yüklendikten sonra bir Express 4.x uygulaması oluşturun:</span><span class="sxs-lookup"><span data-stu-id="6e264-143">Once hello Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span></span>

1. <span data-ttu-id="6e264-144">Açık hello **yeni proje** iletişim (gelen **dosya** > **yeni** > **proje...** ).</span><span class="sxs-lookup"><span data-stu-id="6e264-144">Open hello **New Project** dialog (from **File** > **New** > **Project...**).</span></span>
2. <span data-ttu-id="6e264-145">Genişletme **şablonları** > **JavaScript** > **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="6e264-145">Expand **Templates** > **JavaScript** > **Node.js**.</span></span>
3. <span data-ttu-id="6e264-146">Select hello **temel Azure Node.js Express 4 uygulama**.</span><span class="sxs-lookup"><span data-stu-id="6e264-146">Select hello **Basic Azure Node.js Express 4 Application**.</span></span>
4. <span data-ttu-id="6e264-147">Merhaba proje adı girin.</span><span class="sxs-lookup"><span data-stu-id="6e264-147">Fill in hello project name.</span></span>  <span data-ttu-id="6e264-148">*Tamam*’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e264-148">Click *OK*.</span></span>

    ![Visual Studio 2015 yeni proje][1]
5. <span data-ttu-id="6e264-150">Sağ hello **npm** düğümü ve select **yüklemek yeni npm paketler...** .</span><span class="sxs-lookup"><span data-stu-id="6e264-150">Right-click hello **npm** node and select **Install New npm packages...**.</span></span>
6. <span data-ttu-id="6e264-151">İlk Node.js uygulamanızı oluşturma toorefresh hello npm katalog gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="6e264-151">You may need toorefresh hello npm catalog on creating your first Node.js application.</span></span>  <span data-ttu-id="6e264-152">Tıklatın **yenileme** gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="6e264-152">Click **Refresh** if necessary.</span></span>
7. <span data-ttu-id="6e264-153">Girin *azure mobile apps* hello arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="6e264-153">Enter *azure-mobile-apps* in hello search box.</span></span>  <span data-ttu-id="6e264-154">Merhaba tıklatın **azure mobile apps 2.0.0** paketini ve ardından **paket yükleme**.</span><span class="sxs-lookup"><span data-stu-id="6e264-154">Click hello **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span></span>

    ![Yeni npm paket yüklemek için][2]
8. <span data-ttu-id="6e264-156">**Kapat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e264-156">Click **Close**.</span></span>
9. <span data-ttu-id="6e264-157">Açık hello *app.js* dosya hello Azure Mobile Apps SDK tooadd desteği.</span><span class="sxs-lookup"><span data-stu-id="6e264-157">Open hello *app.js* file tooadd support for hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="6e264-158">Satır 6 at hello sonundaki hello kitaplığı deyimleri gerektirir, hello aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6e264-158">At line 6 at hello bottom of hello library require statements, add hello following code:</span></span>

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    <span data-ttu-id="6e264-159">Diğer app.use ifadeleri satırında yaklaşık 27 hello sonra hello aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6e264-159">At approximately line 27 after hello other app.use statements, add hello following code:</span></span>

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    <span data-ttu-id="6e264-160">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6e264-160">Save hello file.</span></span>
10. <span data-ttu-id="6e264-161">Yerel olarak Merhaba uygulaması (Merhaba API http://localhost: 3000 üzerinde sunulur) çalıştırabilir veya tooAzure yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="6e264-161">Either run hello application locally (hello API is served on http://localhost:3000) or publish tooAzure.</span></span>

### <span data-ttu-id="6e264-162"><a name="create-node-backend-portal"></a>Nasıl yapılır: hello Azure portal kullanarak bir Node.js arka ucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e264-162"><a name="create-node-backend-portal"></a>How to: Create a Node.js backend using hello Azure portal</span></span>
<span data-ttu-id="6e264-163">Bir mobil uygulama arka uç hakkı hello oluşturabilirsiniz [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="6e264-163">You can create a Mobile App backend right in hello [Azure portal].</span></span> <span data-ttu-id="6e264-164">Aşağıdaki adımlar ya da istemci ve sunucu tarafından aşağıdaki hello birlikte oluşturmak hello ya da izleyebilirsiniz [mobil uygulama oluşturma](app-service-mobile-ios-get-started.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="6e264-164">You can either follow hello following steps or create a client and server together by following hello [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span></span> <span data-ttu-id="6e264-165">Başlangıç Öğreticisi bu yönergeleri basitleştirilmiş bir sürümünü içerir ve kavram projeleri kanıtı için en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="6e264-165">hello tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="6e264-166">Merhaba edilene *başlama* dikey altında **tablo API Oluştur**, seçin **Node.js** olarak, **arka uç dilinizi**.</span><span class="sxs-lookup"><span data-stu-id="6e264-166">Back in hello *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span></span>
<span data-ttu-id="6e264-167">Merhaba kutuyu "**bu tüm site içeriğini. üzerine yazacağını kabul ediyorum**", ardından **Todoıtem tablosu oluştur**.</span><span class="sxs-lookup"><span data-stu-id="6e264-167">Check hello box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span></span>

### <span data-ttu-id="6e264-168"><a name="download-quickstart"></a>Nasıl yapılır: indirme hello Node.js arka uç hızlı başlangıç kod projesi Git kullanma</span><span class="sxs-lookup"><span data-stu-id="6e264-168"><a name="download-quickstart"></a>How to: Download hello Node.js backend quickstart code project using Git</span></span>
<span data-ttu-id="6e264-169">Merhaba portalını kullanarak bir Node.js mobil uygulama arka ucu oluşturduğunuzda **Hızlı Başlangıç** dikey penceresinde bir Node.js projesi ve dağıtılan tooyour sitesi için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6e264-169">When you create a Node.js Mobile App backend by using hello portal **Quick start** blade, a Node.js project is created for you and deployed tooyour site.</span></span> <span data-ttu-id="6e264-170">Tabloları ve API'ları ekleyin ve hello portalında hello Node.js arka ucu için kod dosyaları düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="6e264-170">You can add tables and APIs and edit code files for hello Node.js backend in hello portal.</span></span> <span data-ttu-id="6e264-171">Böylece ekleyin veya tablolar ve API'ları değiştirmek sonra Merhaba projeyi yeniden yayımlamanız çeşitli dağıtım araçları toodownload hello arka uç projesi de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e264-171">You can also use various deployment tools toodownload hello backend project so that you can add or modify tables and APIs, then republish hello project.</span></span> <span data-ttu-id="6e264-172">Daha fazla bilgi için bkz: [Azure App Service Deployment Guide].</span><span class="sxs-lookup"><span data-stu-id="6e264-172">For more information, see the [Azure App Service Deployment Guide].</span></span> <span data-ttu-id="6e264-173">Merhaba aşağıdaki yordam bir Git deposu toodownload hello hızlı başlangıç proje kodunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="6e264-173">hello following procedure uses a Git repository toodownload hello quickstart project code.</span></span>

1. <span data-ttu-id="6e264-174">Zaten yapmadıysanız Git'i, yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6e264-174">Install Git, if you haven't already done so.</span></span> <span data-ttu-id="6e264-175">Merhaba adımları gerekli tooinstall Git işletim sistemleri arasında farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="6e264-175">hello steps required tooinstall Git vary between operating systems.</span></span> <span data-ttu-id="6e264-176">Bkz: [yükleme Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) işletim sistemine özgü dağıtımları ve yükleme yönergeleri için.</span><span class="sxs-lookup"><span data-stu-id="6e264-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span></span>
2. <span data-ttu-id="6e264-177">Merhaba adımları [etkinleştir hello uygulama hizmeti uygulama havuzu](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable hello Git deposu hello dağıtım kullanıcı adı ve parola Not yapmadan arka uç siteniz için.</span><span class="sxs-lookup"><span data-stu-id="6e264-177">Follow hello steps in [Enable hello App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable hello Git repository for your backend site, making a note of hello deployment username and password.</span></span>
3. <span data-ttu-id="6e264-178">Mobil uygulama arka ucu için Hello dikey penceresinde hello Not **Git kopyalama URL'si** ayarı.</span><span class="sxs-lookup"><span data-stu-id="6e264-178">In hello blade for your Mobile App backend, make a note of hello **Git clone URL** setting.</span></span>
4. <span data-ttu-id="6e264-179">Merhaba yürütme `git clone` hello Git kopyalama URL'si, gerektiğinde, aşağıdaki örnekte olduğu gibi parolanızı girmeden kullanarak komutu:</span><span class="sxs-lookup"><span data-stu-id="6e264-179">Execute hello `git clone` command using hello Git clone URL, entering your password when required, as in the following example:</span></span>

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. <span data-ttu-id="6e264-180">Olan örnek önceki hello içinde /todolist Gözat toolocal dizin ve dosyaların proje bildirimi indirildi.</span><span class="sxs-lookup"><span data-stu-id="6e264-180">Browse toolocal directory, which in hello preceding example is /todolist, and notice that project files have been downloaded.</span></span> <span data-ttu-id="6e264-181">Merhaba bulun `todoitem.json` hello dosyasında `/tables` dizin.</span><span class="sxs-lookup"><span data-stu-id="6e264-181">Locate hello `todoitem.json` file in hello `/tables` directory.</span></span>  <span data-ttu-id="6e264-182">Bu dosya, tablo üzerinde izinleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6e264-182">This file defines permissions on the table.</span></span>  <span data-ttu-id="6e264-183">Ayrıca hello bulur `todoitem.js` hello aynı dosyayı CRUD işlemi hello tablosu için komut dosyası tanımlar dizin.</span><span class="sxs-lookup"><span data-stu-id="6e264-183">Also find hello `todoitem.js` file in hello same directory, which defines that CRUD operation scripts for hello table.</span></span>
6. <span data-ttu-id="6e264-184">Tooproject dosyaları değişiklikleri yaptıktan sonra tooadd, yürütme ve ardından değişiklikleri toohello site karşıya yükleme komutları aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="6e264-184">After you have made changes tooproject files, execute hello following commands tooadd, commit, then upload the changes toohello site:</span></span>

        $ git commit -m "updated hello table script"
        $ git push origin master

    <span data-ttu-id="6e264-185">Yeni dosyalar toohello proje eklediğinizde tooexecute hello ilk gerekir `git add .` komutu.</span><span class="sxs-lookup"><span data-stu-id="6e264-185">When you add new files toohello project, you first need tooexecute hello `git add .` command.</span></span>

<span data-ttu-id="6e264-186">işlemeleri yeni bir dizi toohello site gönderilen her zaman hello site yeniden yayımlanacak.</span><span class="sxs-lookup"><span data-stu-id="6e264-186">hello site is republished every time a new set of commits is pushed toohello site.</span></span>

### <span data-ttu-id="6e264-187"><a name="howto-publish-to-azure"></a>Nasıl yapılır: Node.js arka uç tooAzure yayımlama</span><span class="sxs-lookup"><span data-stu-id="6e264-187"><a name="howto-publish-to-azure"></a>How to: Publish your Node.js backend tooAzure</span></span>
<span data-ttu-id="6e264-188">Microsoft Azure yayımlama hello Azure hizmeti için Azure App Service Mobile Apps Node.js arka ucuna birçok mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="6e264-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to hello Azure service.</span></span>  <span data-ttu-id="6e264-189">Bunlar, Visual Studio'ya tümleşik dağıtım araçları, komut satırı araçları ve kaynak denetimine bağlı sürekli dağıtım seçenekleri kullanılarak içerir.</span><span class="sxs-lookup"><span data-stu-id="6e264-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span></span>  <span data-ttu-id="6e264-190">Bu konu hakkında daha fazla bilgi için bkz: [Azure App Service Deployment Guide].</span><span class="sxs-lookup"><span data-stu-id="6e264-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span></span>

<span data-ttu-id="6e264-191">Azure uygulama hizmeti dağıtmadan önce gözden geçirmeniz gereken Node.js uygulama için ilgili bir uzmana sahiptir:</span><span class="sxs-lookup"><span data-stu-id="6e264-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span></span>

* <span data-ttu-id="6e264-192">Nasıl çok[hello düğümü sürümü belirtin]</span><span class="sxs-lookup"><span data-stu-id="6e264-192">How too[specify hello Node Version]</span></span>
* <span data-ttu-id="6e264-193">Nasıl çok[düğümü modüllerini kullanma]</span><span class="sxs-lookup"><span data-stu-id="6e264-193">How too[use Node modules]</span></span>

### <span data-ttu-id="6e264-194"><a name="howto-enable-homepage"></a>Nasıl yapılır: bir giriş sayfası, uygulamanız için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="6e264-194"><a name="howto-enable-homepage"></a>How to: Enable a Home Page for your application</span></span>
<span data-ttu-id="6e264-195">Birçok uygulama web ve mobil uygulamaları bir bileşimidir ve hello ExpressJS framework toocombine iki modelleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="6e264-195">Many applications are a combination of web and mobile apps and hello ExpressJS framework allows you toocombine the two facets.</span></span>  <span data-ttu-id="6e264-196">Bazı durumlarda, ancak, tooonly uygulayan Mobil arabirimi isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="6e264-196">Sometimes, however, you may wish tooonly implement a mobile interface.</span></span>  <span data-ttu-id="6e264-197">Bir giriş sayfası tooensure hello uygulama hizmeti çalışır durumda olduğundan yararlı tooprovide olur.</span><span class="sxs-lookup"><span data-stu-id="6e264-197">It is useful tooprovide a landing page tooensure hello app service is up and running.</span></span>  <span data-ttu-id="6e264-198">Giriş sayfası sağlayın veya geçici bir giriş sayfası etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6e264-198">You can either provide your own home page or enable a temporary home page.</span></span>  <span data-ttu-id="6e264-199">tooenable geçici bir giriş sayfası tooinstantiate Azure Mobile Apps aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="6e264-199">tooenable a temporary home page, use hello following tooinstantiate Azure Mobile Apps:</span></span>

    var mobile = azureMobileApps({ homePage: true });

<span data-ttu-id="6e264-200">Yalnızca kullanılabilen bu seçenek yerel olarak geliştirirken istiyorsanız, bu ayar tooyour ekleyebilirsiniz `azureMobile.js` dosya.</span><span class="sxs-lookup"><span data-stu-id="6e264-200">If you only want this option available when developing locally, you can add this setting tooyour `azureMobile.js` file.</span></span>

## <span data-ttu-id="6e264-201"><a name="TableOperations"></a>Tablo işlemleri</span><span class="sxs-lookup"><span data-stu-id="6e264-201"><a name="TableOperations"></a>Table operations</span></span>
<span data-ttu-id="6e264-202">Hello azure mobile apps Node.js sunucusu SDK'sı mekanizmaları tooexpose veri sağlayan bir Webapı olarak Azure SQL veritabanında depolanan tabloları.</span><span class="sxs-lookup"><span data-stu-id="6e264-202">hello azure-mobile-apps Node.js Server SDK provides mechanisms tooexpose data tables stored in Azure SQL Database as a WebAPI.</span></span>  <span data-ttu-id="6e264-203">Beş işlem sağlanır.</span><span class="sxs-lookup"><span data-stu-id="6e264-203">Five operations are provided.</span></span>

| <span data-ttu-id="6e264-204">İşlem</span><span class="sxs-lookup"><span data-stu-id="6e264-204">Operation</span></span> | <span data-ttu-id="6e264-205">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6e264-205">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6e264-206">GET /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="6e264-206">GET /tables/*tablename*</span></span> |<span data-ttu-id="6e264-207">Merhaba tabloda tüm kayıtları Al</span><span class="sxs-lookup"><span data-stu-id="6e264-207">Get all records in hello table</span></span> |
| <span data-ttu-id="6e264-208">GET /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="6e264-208">GET /tables/*tablename*/:id</span></span> |<span data-ttu-id="6e264-209">Belirli bir kayıt hello tabloda Al</span><span class="sxs-lookup"><span data-stu-id="6e264-209">Get a specific record in hello table</span></span> |
| <span data-ttu-id="6e264-210">POST /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="6e264-210">POST /tables/*tablename*</span></span> |<span data-ttu-id="6e264-211">Merhaba tabloda bir kayıt oluşturun</span><span class="sxs-lookup"><span data-stu-id="6e264-211">Create a record in hello table</span></span> |
| <span data-ttu-id="6e264-212">Düzeltme eki /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="6e264-212">PATCH /tables/*tablename*/:id</span></span> |<span data-ttu-id="6e264-213">Güncelleştirme hello tablosundan bir kayıt</span><span class="sxs-lookup"><span data-stu-id="6e264-213">Update a record in hello table</span></span> |
| <span data-ttu-id="6e264-214">DELETE /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="6e264-214">DELETE /tables/*tablename*/:id</span></span> |<span data-ttu-id="6e264-215">Merhaba tablosundan bir kayıt silme</span><span class="sxs-lookup"><span data-stu-id="6e264-215">Delete a record in hello table</span></span> |

<span data-ttu-id="6e264-216">Bu Webapı destekleyen [OData] ve hello tablo şemasını toosupport genişletir [çevrimdışı veri eşitlemeye].</span><span class="sxs-lookup"><span data-stu-id="6e264-216">This WebAPI supports [OData] and extends hello table schema toosupport [offline data sync].</span></span>

### <span data-ttu-id="6e264-217"><a name="howto-dynamicschema"></a>Nasıl yapılır: dinamik bir şema kullanarak tabloları tanımlayın</span><span class="sxs-lookup"><span data-stu-id="6e264-217"><a name="howto-dynamicschema"></a>How to: Define tables using a dynamic schema</span></span>
<span data-ttu-id="6e264-218">Bir tablo kullanılabilmesi için tanımlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6e264-218">Before a table can be used, it must be defined.</span></span>  <span data-ttu-id="6e264-219">Tabloları (burada hello sütunları hello şeması içindeki tanımlar hello Geliştirici) statik bir şema veya dinamik olarak tanımlanabilir (burada hello SDK gelen istekleri temel alan hello şema denetler).</span><span class="sxs-lookup"><span data-stu-id="6e264-219">Tables can be defined with a static schema (where hello developer defines hello columns within hello schema) or dynamically (where hello SDK controls hello schema based on incoming requests).</span></span> <span data-ttu-id="6e264-220">Ayrıca, hello Geliştirici Javascript kodu toohello tanımı ekleyerek hello Webapı belirli yönlerini kontrol edebilir.</span><span class="sxs-lookup"><span data-stu-id="6e264-220">In addition, hello developer can control specific aspects of hello WebAPI by adding Javascript code toohello definition.</span></span>

<span data-ttu-id="6e264-221">En iyi uygulama, hello tabloları dizindeki Javascript dosyasında her tablo tanımlamanız sonra tables.import() yöntemi tooimport hello tabloları kullanın.</span><span class="sxs-lookup"><span data-stu-id="6e264-221">As a best practice, you should define each table in a Javascript file in hello tables directory, then use the tables.import() method tooimport hello tables.</span></span>  <span data-ttu-id="6e264-222">Merhaba basic uygulama genişletme, hello app.js dosya ayarlanması:</span><span class="sxs-lookup"><span data-stu-id="6e264-222">Extending hello basic-app, hello app.js file would be adjusted:</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

<span data-ttu-id="6e264-223">Merhaba tabloda tanımlayın. / tables/TodoItem.js:</span><span class="sxs-lookup"><span data-stu-id="6e264-223">Define hello table in ./tables/TodoItem.js:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

<span data-ttu-id="6e264-224">Tablolar, varsayılan olarak dinamik şema kullanın.</span><span class="sxs-lookup"><span data-stu-id="6e264-224">Tables use dynamic schema by default.</span></span>  <span data-ttu-id="6e264-225">dinamik şema kapalı tooturn genel olarak, hello uygulama ayarı ayarlamak **MS_DynamicSchema** toofalse hello Azure portalı içinde.</span><span class="sxs-lookup"><span data-stu-id="6e264-225">tooturn off dynamic schema globally, set hello App Setting **MS_DynamicSchema** toofalse within hello Azure portal.</span></span>

<span data-ttu-id="6e264-226">Hello tam bir örnek bulabilirsiniz [Yapılacaklar örneği github'daki].</span><span class="sxs-lookup"><span data-stu-id="6e264-226">You can find a complete example in hello [todo sample on GitHub].</span></span>

### <span data-ttu-id="6e264-227"><a name="howto-staticschema"></a>Nasıl yapılır: statik Şeması'nı kullanarak tabloları tanımlayın</span><span class="sxs-lookup"><span data-stu-id="6e264-227"><a name="howto-staticschema"></a>How to: Define tables using a static schema</span></span>
<span data-ttu-id="6e264-228">Merhaba sütunları tooexpose hello Webapı aracılığıyla açıkça tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e264-228">You can explicitly define hello columns tooexpose via hello WebAPI.</span></span>  <span data-ttu-id="6e264-229">hello Azure mobile apps Node.js SDK'sı, sağladığınız çevrimdışı veri eşitlemeyi toohello listesi için gerekli ek sütunlar otomatik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="6e264-229">hello azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync toohello list that you provide.</span></span>  <span data-ttu-id="6e264-230">Örneğin, hızlı başlangıç istemci uygulamaları iki sütun içeren bir tablo gerektirir: metin (dize) ve (Boole) tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="6e264-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span></span>  
<span data-ttu-id="6e264-231">Merhaba tablosu (Merhaba tabloları dizininde yer alan) hello tablo tanımı JavaScript dosyasında şu şekilde tanımlanabilir:</span><span class="sxs-lookup"><span data-stu-id="6e264-231">hello table can be defined in hello table definition JavaScript file (located in hello tables directory) as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

<span data-ttu-id="6e264-232">Sonra tabloları statik olarak tanımlarsanız, başlangıçta hello tables.initialize() yöntemi toocreate hello veritabanı şemasını da çağırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6e264-232">If you define tables statically, then you must also call hello tables.initialize() method toocreate hello database schema on startup.</span></span>  <span data-ttu-id="6e264-233">Merhaba tables.initialize() yöntemi döndürür bir [Promise] böylece hello web hizmeti isteklerinin başlatılmakta hello veritabanı önce sunmuyor.</span><span class="sxs-lookup"><span data-stu-id="6e264-233">hello tables.initialize() method returns a [Promise] so that hello web service does not serve requests before hello database being initialized.</span></span>

### <span data-ttu-id="6e264-234"><a name="howto-sqlexpress-setup"></a>Nasıl yapılır: yerel makinenizde geliştirme veri deposu olarak kullanmak SQL Express'i</span><span class="sxs-lookup"><span data-stu-id="6e264-234"><a name="howto-sqlexpress-setup"></a>How to: Use SQL Express as a development data store on your local machine</span></span>
<span data-ttu-id="6e264-235">Hello Azure Mobile Apps hello AzureMobile uygulamaları düğümü SDK hello kutu dışı veri hizmet için üç seçenek sunar: SDK, veri hello kutu dışı hizmet veren için üç seçenek sağlar:</span><span class="sxs-lookup"><span data-stu-id="6e264-235">hello Azure Mobile Apps hello AzureMobile Apps Node SDK provides three options for serving data out of hello box: SDK provides three options for serving data out of hello box:</span></span>

* <span data-ttu-id="6e264-236">Kullanım hello **bellek** sürücü tooprovide bir kalıcı olmayan örnek deposuna</span><span class="sxs-lookup"><span data-stu-id="6e264-236">Use hello **memory** driver tooprovide a non-persistent example store</span></span>
* <span data-ttu-id="6e264-237">Kullanım hello **mssql** sürücü tooprovide geliştirme için SQL Express veri deposu</span><span class="sxs-lookup"><span data-stu-id="6e264-237">Use hello **mssql** driver tooprovide a SQL Express data store for development</span></span>
* <span data-ttu-id="6e264-238">Kullanım hello **mssql** sürücü tooprovide üretim için bir Azure SQL veritabanı veri deposu</span><span class="sxs-lookup"><span data-stu-id="6e264-238">Use hello **mssql** driver tooprovide an Azure SQL Database data store for production</span></span>

<span data-ttu-id="6e264-239">Hello Azure Mobile Apps Node.js SDK'sını kullanır hello [mssql Node.js paket] tooestablish ve bağlantı tooboth SQL Express ve SQL veritabanını kullan.</span><span class="sxs-lookup"><span data-stu-id="6e264-239">hello Azure Mobile Apps Node.js SDK uses hello [mssql Node.js package] tooestablish and use a connection tooboth SQL Express and SQL Database.</span></span>  <span data-ttu-id="6e264-240">Bu paket, SQL Express örneği üzerinde TCP bağlantılarını etkinleştirmenizi istemektedir.</span><span class="sxs-lookup"><span data-stu-id="6e264-240">This package requires that you enable TCP connections on your SQL Express instance.</span></span>

> [!TIP]
> <span data-ttu-id="6e264-241">Merhaba bellek sürücüsü eksiksiz test olanaklarının sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="6e264-241">hello memory driver does not provide a complete set of facilities for testing.</span></span>  <span data-ttu-id="6e264-242">Arka ucunu yerel olarak tootest isterseniz, biz SQL Express veri deposu hello kullanımını önerilir ve mssql sürücü hello.</span><span class="sxs-lookup"><span data-stu-id="6e264-242">If you wish tootest your backend locally, we recommend hello use of a SQL Express data store and hello mssql driver.</span></span>
>
>

1. <span data-ttu-id="6e264-243">İndirme ve yükleme [Microsoft SQL Server 2014 Express].</span><span class="sxs-lookup"><span data-stu-id="6e264-243">Download and install [Microsoft SQL Server 2014 Express].</span></span>  <span data-ttu-id="6e264-244">Araçlar Edition'la hello SQL Server 2014 Express yükleme emin olun.</span><span class="sxs-lookup"><span data-stu-id="6e264-244">Ensure you install hello SQL Server 2014 Express with Tools edition.</span></span>  <span data-ttu-id="6e264-245">64-bit desteği açıkça gerektirmedikçe hello 32-bit sürümü çalışırken daha az bellek kullanır.</span><span class="sxs-lookup"><span data-stu-id="6e264-245">Unless you explicitly require 64-bit support, hello 32-bit version consumes less memory when running.</span></span>
2. <span data-ttu-id="6e264-246">SQL Server 2014 Configuration Manager Hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6e264-246">Run hello SQL Server 2014 Configuration Manager.</span></span>

   1. <span data-ttu-id="6e264-247">Merhaba genişletin **SQL Server Ağ Yapılandırması** hello sol ağaç menü düğümünde.</span><span class="sxs-lookup"><span data-stu-id="6e264-247">Expand hello **SQL Server Network Configuration** node in hello left-hand tree menu.</span></span>
   2. <span data-ttu-id="6e264-248">Tıklatın **SQLEXPRESS protokolleri**.</span><span class="sxs-lookup"><span data-stu-id="6e264-248">Click **Protocols for SQLEXPRESS**.</span></span>
   3. <span data-ttu-id="6e264-249">Sağ **TCP/IP'yi** seçip **etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="6e264-249">Right-click **TCP/IP** and select **Enable**.</span></span>  <span data-ttu-id="6e264-250">Tıklatın **Tamam** hello açılan iletişim kutusunda.</span><span class="sxs-lookup"><span data-stu-id="6e264-250">Click **OK** in hello pop-up dialog.</span></span>
   4. <span data-ttu-id="6e264-251">Sağ **TCP/IP'yi** seçip **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="6e264-251">Right-click **TCP/IP** and select **Properties**.</span></span>
   5. <span data-ttu-id="6e264-252">Merhaba tıklatın **IP adreslerini** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="6e264-252">Click hello **IP Addresses** tab.</span></span>
   6. <span data-ttu-id="6e264-253">Hello bulur **IPAll** düğümü.</span><span class="sxs-lookup"><span data-stu-id="6e264-253">Find hello **IPAll** node.</span></span>  <span data-ttu-id="6e264-254">Merhaba, **TCP bağlantı noktası** alanına, **1433**.</span><span class="sxs-lookup"><span data-stu-id="6e264-254">In hello **TCP Port** field, enter **1433**.</span></span>

          ![Configure SQL Express for TCP/IP][3]
   7. <span data-ttu-id="6e264-255">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e264-255">Click **OK**.</span></span>  <span data-ttu-id="6e264-256">Tıklatın **Tamam** hello açılan iletişim kutusunda.</span><span class="sxs-lookup"><span data-stu-id="6e264-256">Click **OK** in hello pop-up dialog.</span></span>
   8. <span data-ttu-id="6e264-257">Tıklatın **SQL Server Hizmetleri** hello sol ağaç menüsünde.</span><span class="sxs-lookup"><span data-stu-id="6e264-257">Click **SQL Server Services** in hello left-hand tree menu.</span></span>
   9. <span data-ttu-id="6e264-258">Sağ **SQL Server (SQLEXPRESS)** seçip **yeniden başlatın**</span><span class="sxs-lookup"><span data-stu-id="6e264-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span></span>
   10. <span data-ttu-id="6e264-259">Merhaba SQL Server 2014 Yapılandırma Yöneticisi'ni kapatın.</span><span class="sxs-lookup"><span data-stu-id="6e264-259">Close hello SQL Server 2014 Configuration Manager.</span></span>
3. <span data-ttu-id="6e264-260">Merhaba SQL Server 2014 Management Studio'yu çalıştırın ve tooyour yerel SQL Express örneği bağlanın</span><span class="sxs-lookup"><span data-stu-id="6e264-260">Run hello SQL Server 2014 Management Studio and connect tooyour local SQL Express instance</span></span>

   1. <span data-ttu-id="6e264-261">Örneğinizi hello Object Explorer'ın sağ tıklatıp **özellikleri**</span><span class="sxs-lookup"><span data-stu-id="6e264-261">Right-click your instance in hello Object Explorer and select **Properties**</span></span>
   2. <span data-ttu-id="6e264-262">Select hello **güvenlik** sayfası.</span><span class="sxs-lookup"><span data-stu-id="6e264-262">Select hello **Security** page.</span></span>
   3. <span data-ttu-id="6e264-263">Merhaba olun **SQL Server ve Windows kimlik doğrulaması modu** seçilir</span><span class="sxs-lookup"><span data-stu-id="6e264-263">Ensure hello **SQL Server and Windows Authentication mode** is selected</span></span>
   4. <span data-ttu-id="6e264-264">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e264-264">Click **OK**</span></span>

          ![Configure SQL Express Authentication][4]
   5. <span data-ttu-id="6e264-265">Genişletme **güvenlik** > **oturumları** hello Nesne Gezgini içinde</span><span class="sxs-lookup"><span data-stu-id="6e264-265">Expand **Security** > **Logins** in hello Object Explorer</span></span>
   6. <span data-ttu-id="6e264-266">Sağ **oturumları** seçip **yeni oturum açma...**</span><span class="sxs-lookup"><span data-stu-id="6e264-266">Right-click **Logins** and select **New Login...**</span></span>
   7. <span data-ttu-id="6e264-267">Bir oturum açma adı girin.</span><span class="sxs-lookup"><span data-stu-id="6e264-267">Enter a Login name.</span></span>  <span data-ttu-id="6e264-268">**SQL Server kimlik doğrulaması**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="6e264-268">Select **SQL Server authentication**.</span></span>  <span data-ttu-id="6e264-269">Bir parola girin ve ardından hello girin aynı parolayı **parolayı onayla**.</span><span class="sxs-lookup"><span data-stu-id="6e264-269">Enter a Password, then enter hello same password in **Confirm password**.</span></span>  <span data-ttu-id="6e264-270">Merhaba parola Windows karmaşıklık gereksinimlerini karşılaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e264-270">hello password must meet Windows complexity requirements.</span></span>
   8. <span data-ttu-id="6e264-271">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e264-271">Click **OK**</span></span>

          ![Add a new user tooSQL Express][5]
   9. <span data-ttu-id="6e264-272">Yeni oturum açma sağ tıklatıp **özellikleri**</span><span class="sxs-lookup"><span data-stu-id="6e264-272">Right-click your new login and select **Properties**</span></span>
   10. <span data-ttu-id="6e264-273">Select hello **sunucu rolleri** sayfası</span><span class="sxs-lookup"><span data-stu-id="6e264-273">Select hello **Server Roles** page</span></span>
   11. <span data-ttu-id="6e264-274">Merhaba kutusunu sonraki toohello denetleyin **dbcreator** sunucu rolü</span><span class="sxs-lookup"><span data-stu-id="6e264-274">Check hello box next toohello **dbcreator** server role</span></span>
   12. <span data-ttu-id="6e264-275">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e264-275">Click **OK**</span></span>
   13. <span data-ttu-id="6e264-276">Merhaba SQL Server 2015 Management Studio'yu kapatın</span><span class="sxs-lookup"><span data-stu-id="6e264-276">Close hello SQL Server 2015 Management Studio</span></span>

<span data-ttu-id="6e264-277">Kayıt hello kullanıcı adı ve parola seçtiğiniz emin olun.</span><span class="sxs-lookup"><span data-stu-id="6e264-277">Ensure you record hello username and password you selected.</span></span>  <span data-ttu-id="6e264-278">Belirli bir veritabanını gereksinimlerinize bağlı olarak tooassign ek sunucu rollerini veya izinleri gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="6e264-278">You may need tooassign additional server roles or permissions depending on your specific database requirements.</span></span>

<span data-ttu-id="6e264-279">Merhaba Node.js uygulaması okur hello **SQLCONNSTR_MS_TableConnectionString** hello bağlantı dizesi bu veritabanı için ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="6e264-279">hello Node.js application reads hello **SQLCONNSTR_MS_TableConnectionString** environment variable for hello connection string for this database.</span></span>  <span data-ttu-id="6e264-280">Ortamınızda bu değişkeni ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e264-280">You can set this variable within your environment.</span></span>  <span data-ttu-id="6e264-281">Örneğin, bu ortam değişkenini PowerShell tooset kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6e264-281">For example, you can use PowerShell tooset this environment variable:</span></span>

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

<span data-ttu-id="6e264-282">Bir TCP/IP bağlantısı üzerinden Hello veritabanına erişmek ve hello bağlantı için bir kullanıcı adı ve parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="6e264-282">Access hello database through a TCP/IP connection and provide a username and password for hello connection.</span></span>

### <span data-ttu-id="6e264-283"><a name="howto-config-localdev"></a>Nasıl yapılır: projeniz yerel geliştirme için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6e264-283"><a name="howto-config-localdev"></a>How to: Configure your project for local development</span></span>
<span data-ttu-id="6e264-284">Azure Mobile Apps okur adlandırılan bir JavaScript dosyası *azureMobile.js* hello yerel dosya sistemi gelen.</span><span class="sxs-lookup"><span data-stu-id="6e264-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from hello local filesystem.</span></span>  <span data-ttu-id="6e264-285">Değil üretimde bu dosya tooconfigure hello Azure Mobile Apps SDK'sını kullanın - uygulaması ayarları içinde hello kullan [Azure portal] yerine.</span><span class="sxs-lookup"><span data-stu-id="6e264-285">Do not use this file tooconfigure hello Azure Mobile Apps SDK in production - use App Settings within hello [Azure portal] instead.</span></span>  <span data-ttu-id="6e264-286">Merhaba *azureMobile.js* dosyasına bir yapılandırma nesnesi.</span><span class="sxs-lookup"><span data-stu-id="6e264-286">hello *azureMobile.js* file should export a configuration object.</span></span>  <span data-ttu-id="6e264-287">Merhaba en yaygın ayarlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6e264-287">hello most common settings are:</span></span>

* <span data-ttu-id="6e264-288">Veritabanı ayarları</span><span class="sxs-lookup"><span data-stu-id="6e264-288">Database Settings</span></span>
* <span data-ttu-id="6e264-289">Tanılama günlük ayarları</span><span class="sxs-lookup"><span data-stu-id="6e264-289">Diagnostic Logging Settings</span></span>
* <span data-ttu-id="6e264-290">Alternatif CORS ayarları</span><span class="sxs-lookup"><span data-stu-id="6e264-290">Alternate CORS Settings</span></span>

<span data-ttu-id="6e264-291">Örnek *azureMobile.js* veritabanı ayarlarını aşağıdaki önceki hello uygulama dosyası:</span><span class="sxs-lookup"><span data-stu-id="6e264-291">An example *azureMobile.js* file implementing hello preceding database settings follows:</span></span>

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

<span data-ttu-id="6e264-292">Eklediğiniz öneririz *azureMobile.js* tooyour *.gitignore* dosya (veya diğer kaynak kodu denetimi dosyayı yoksay) hello bulutta saklanmasını tooprevent parolalar.</span><span class="sxs-lookup"><span data-stu-id="6e264-292">We recommend that you add *azureMobile.js* tooyour *.gitignore* file (or other source code control ignore file) tooprevent passwords from being stored in hello cloud.</span></span>  <span data-ttu-id="6e264-293">Her zaman üretim ayarlarını hello uygulama ayarlarında yapılandırmak [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="6e264-293">Always configure production settings in App Settings within hello [Azure portal].</span></span>

### <span data-ttu-id="6e264-294"><a name="howto-appsettings"></a>: Mobil uygulamanız için uygulama ayarlarını yapılandır</span><span class="sxs-lookup"><span data-stu-id="6e264-294"><a name="howto-appsettings"></a>How: Configure App Settings for your Mobile App</span></span>
<span data-ttu-id="6e264-295">Merhaba çoğu ayarlarında *azureMobile.js* dosyanız eşdeğer bir uygulama ayarı hello [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="6e264-295">Most settings in hello *azureMobile.js* file have an equivalent App Setting in hello [Azure portal].</span></span>  <span data-ttu-id="6e264-296">Liste tooconfigure aşağıdaki hello uygulama ayarlarında, uygulamanızın kullanın:</span><span class="sxs-lookup"><span data-stu-id="6e264-296">Use hello following list tooconfigure your app in App Settings:</span></span>

| <span data-ttu-id="6e264-297">Uygulama ayarı</span><span class="sxs-lookup"><span data-stu-id="6e264-297">App Setting</span></span> | <span data-ttu-id="6e264-298">*azureMobile.js* ayarı</span><span class="sxs-lookup"><span data-stu-id="6e264-298">*azureMobile.js* Setting</span></span> | <span data-ttu-id="6e264-299">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6e264-299">Description</span></span> | <span data-ttu-id="6e264-300">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="6e264-300">Valid Values</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6e264-301">**MS_MobileAppName**</span><span class="sxs-lookup"><span data-stu-id="6e264-301">**MS_MobileAppName**</span></span> |<span data-ttu-id="6e264-302">ad</span><span class="sxs-lookup"><span data-stu-id="6e264-302">name</span></span> |<span data-ttu-id="6e264-303">Merhaba uygulamasının Hello adı</span><span class="sxs-lookup"><span data-stu-id="6e264-303">hello name of hello app</span></span> |<span data-ttu-id="6e264-304">Dize</span><span class="sxs-lookup"><span data-stu-id="6e264-304">string</span></span> |
| <span data-ttu-id="6e264-305">**MS_MobileLoggingLevel**</span><span class="sxs-lookup"><span data-stu-id="6e264-305">**MS_MobileLoggingLevel**</span></span> |<span data-ttu-id="6e264-306">Logging.level</span><span class="sxs-lookup"><span data-stu-id="6e264-306">logging.level</span></span> |<span data-ttu-id="6e264-307">İletileri toolog en küçük günlük düzeyi</span><span class="sxs-lookup"><span data-stu-id="6e264-307">Minimum log level of messages toolog</span></span> |<span data-ttu-id="6e264-308">hata, uyarı, bilgi, ayrıntılı, hata ayıklama, saçma</span><span class="sxs-lookup"><span data-stu-id="6e264-308">error, warning, info, verbose, debug, silly</span></span> |
| <span data-ttu-id="6e264-309">**MS_DebugMode**</span><span class="sxs-lookup"><span data-stu-id="6e264-309">**MS_DebugMode**</span></span> |<span data-ttu-id="6e264-310">Hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="6e264-310">debug</span></span> |<span data-ttu-id="6e264-311">Etkinleştirme veya devre dışı bırak hata ayıklama modu</span><span class="sxs-lookup"><span data-stu-id="6e264-311">Enable or Disable debug mode</span></span> |<span data-ttu-id="6e264-312">TRUE, false</span><span class="sxs-lookup"><span data-stu-id="6e264-312">true, false</span></span> |
| <span data-ttu-id="6e264-313">**MS_TableSchema**</span><span class="sxs-lookup"><span data-stu-id="6e264-313">**MS_TableSchema**</span></span> |<span data-ttu-id="6e264-314">Data.Schema</span><span class="sxs-lookup"><span data-stu-id="6e264-314">data.schema</span></span> |<span data-ttu-id="6e264-315">SQL tablolarının varsayılan şema adı</span><span class="sxs-lookup"><span data-stu-id="6e264-315">Default schema name for SQL tables</span></span> |<span data-ttu-id="6e264-316">dize (varsayılan: dbo)</span><span class="sxs-lookup"><span data-stu-id="6e264-316">string (default: dbo)</span></span> |
| <span data-ttu-id="6e264-317">**MS_DynamicSchema**</span><span class="sxs-lookup"><span data-stu-id="6e264-317">**MS_DynamicSchema**</span></span> |<span data-ttu-id="6e264-318">data.dynamicSchema</span><span class="sxs-lookup"><span data-stu-id="6e264-318">data.dynamicSchema</span></span> |<span data-ttu-id="6e264-319">Etkinleştirme veya devre dışı bırak hata ayıklama modu</span><span class="sxs-lookup"><span data-stu-id="6e264-319">Enable or Disable debug mode</span></span> |<span data-ttu-id="6e264-320">TRUE, false</span><span class="sxs-lookup"><span data-stu-id="6e264-320">true, false</span></span> |
| <span data-ttu-id="6e264-321">**MS_DisableVersionHeader**</span><span class="sxs-lookup"><span data-stu-id="6e264-321">**MS_DisableVersionHeader**</span></span> |<span data-ttu-id="6e264-322">Sürüm (kümesi tooundefined)</span><span class="sxs-lookup"><span data-stu-id="6e264-322">version (set tooundefined)</span></span> |<span data-ttu-id="6e264-323">Merhaba X-ZUMO-Server-Version üstbilgi devre dışı bırakır</span><span class="sxs-lookup"><span data-stu-id="6e264-323">Disables hello X-ZUMO-Server-Version header</span></span> |<span data-ttu-id="6e264-324">TRUE, false</span><span class="sxs-lookup"><span data-stu-id="6e264-324">true, false</span></span> |
| <span data-ttu-id="6e264-325">**MS_SkipVersionCheck**</span><span class="sxs-lookup"><span data-stu-id="6e264-325">**MS_SkipVersionCheck**</span></span> |<span data-ttu-id="6e264-326">skipversioncheck</span><span class="sxs-lookup"><span data-stu-id="6e264-326">skipversioncheck</span></span> |<span data-ttu-id="6e264-327">Merhaba İstemcisi API sürümü denetimi devre dışı bırakır</span><span class="sxs-lookup"><span data-stu-id="6e264-327">Disables hello client API version check</span></span> |<span data-ttu-id="6e264-328">TRUE, false</span><span class="sxs-lookup"><span data-stu-id="6e264-328">true, false</span></span> |

<span data-ttu-id="6e264-329">tooset bir uygulama ayarı:</span><span class="sxs-lookup"><span data-stu-id="6e264-329">tooset an App Setting:</span></span>

1. <span data-ttu-id="6e264-330">İçinde toohello oturum [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="6e264-330">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="6e264-331">Seçin **tüm kaynakları** veya **uygulama hizmetleri** mobil uygulamanızın hello adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="6e264-331">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="6e264-332">Varsayılan olarak Hello ayarları dikey penceresini açar.</span><span class="sxs-lookup"><span data-stu-id="6e264-332">hello Settings blade opens by default.</span></span> <span data-ttu-id="6e264-333">' I içermiyorsa tıklatırsanız **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="6e264-333">If it doesn't, click **Settings**.</span></span>
4. <span data-ttu-id="6e264-334">Tıklatın **uygulama ayarları** hello genel menüsünde.</span><span class="sxs-lookup"><span data-stu-id="6e264-334">Click **Application settings** in hello GENERAL menu.</span></span>
5. <span data-ttu-id="6e264-335">Toohello uygulama ayarları bölümüne kaydırın.</span><span class="sxs-lookup"><span data-stu-id="6e264-335">Scroll toohello App Settings section.</span></span>
6. <span data-ttu-id="6e264-336">Uygulamanızı ayarı zaten varsa, hello değerini hello uygulama ayarı tooedit hello'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="6e264-336">If your app setting already exists, click hello value of hello app setting tooedit hello value.</span></span>
7. <span data-ttu-id="6e264-337">Uygulama ayarı yoksa hello uygulama ayarı hello anahtar kutusuna ve hello değer kutusuna hello değeri girin.</span><span class="sxs-lookup"><span data-stu-id="6e264-337">If your app setting does not exist, enter hello App Setting in hello Key box and hello value in hello Value box.</span></span>
8. <span data-ttu-id="6e264-338">Tamamlandıktan sonra tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="6e264-338">Once you are complete, click **Save**.</span></span>

<span data-ttu-id="6e264-339">Çoğu uygulama ayarlarını değiştirme hizmetini yeniden başlatma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6e264-339">Changing most app settings requires a service restart.</span></span>

### <span data-ttu-id="6e264-340"><a name="howto-use-sqlazure"></a>Nasıl yapılır: SQL Database üretim veri deposu olarak kullanın</span><span class="sxs-lookup"><span data-stu-id="6e264-340"><a name="howto-use-sqlazure"></a>How to: Use SQL Database as your production data store</span></span>
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

<span data-ttu-id="6e264-341">Bir veri deposu olarak Azure SQL veritabanı kullanan tüm Azure App Service uygulama türlerine aynıdır.</span><span class="sxs-lookup"><span data-stu-id="6e264-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span></span> <span data-ttu-id="6e264-342">Henüz yapmadıysanız, bu adımları toocreate bir mobil uygulama arka ucu izleyin.</span><span class="sxs-lookup"><span data-stu-id="6e264-342">If you have not done so already, follow these steps toocreate a Mobile App backend.</span></span>

1. <span data-ttu-id="6e264-343">İçinde toohello oturum [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="6e264-343">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="6e264-344">Merhaba hello pencerenin sol üst, hello tıklatın **+ yeni** düğmesi > **Web + mobil** > **mobil uygulama**, mobil uygulama arka ucu için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="6e264-344">In hello top left of hello window, click hello **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="6e264-345">Merhaba, **kaynak grubu** kutusunda, aynı ad hello uygulamanızı girin.</span><span class="sxs-lookup"><span data-stu-id="6e264-345">In hello **Resource Group** box, enter hello same name as your app.</span></span>
4. <span data-ttu-id="6e264-346">Merhaba varsayılan uygulama hizmeti planı seçilir.</span><span class="sxs-lookup"><span data-stu-id="6e264-346">hello Default App Service plan is selected.</span></span>  <span data-ttu-id="6e264-347">Uygulama hizmeti planınızı toochange isterseniz, uygulama hizmeti planı hello tıklayarak bunu yapabilirsiniz > **+ Yeni Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="6e264-347">If you wish toochange your App Service plan, you can do so by clicking hello App Service Plan > **+ Create New**.</span></span>  <span data-ttu-id="6e264-348">Merhaba yeni uygulama hizmeti planının adı sağlayın ve uygun bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="6e264-348">Provide a name of hello new App Service plan and select an appropriate location.</span></span>  <span data-ttu-id="6e264-349">Merhaba fiyatlandırma Katmanı'nı tıklatın ve hello hizmeti için uygun bir fiyatlandırma katmanı seçin.</span><span class="sxs-lookup"><span data-stu-id="6e264-349">Click hello Pricing tier and select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="6e264-350">Seçin **tüm görüntüle** daha seçenekleri gibi fiyatlandırma tooview **serbest** ve **paylaşılan**.</span><span class="sxs-lookup"><span data-stu-id="6e264-350">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span>  <span data-ttu-id="6e264-351">Fiyatlandırma katmanı seçildiğinde hello tıklatın **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6e264-351">Once you have selected the pricing tier, click hello **Select** button.</span></span>  <span data-ttu-id="6e264-352">Merhaba edilene **uygulama hizmeti planı** dikey penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="6e264-352">Back in hello **App Service plan** blade, click **OK**.</span></span>
5. <span data-ttu-id="6e264-353">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e264-353">Click **Create**.</span></span> <span data-ttu-id="6e264-354">Bir mobil uygulama arka ucu sağlama birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="6e264-354">Provisioning a Mobile App backend can take a couple of minutes.</span></span>  <span data-ttu-id="6e264-355">Merhaba mobil uygulama arka ucu sağlandıktan sonra hello portal hello açar **ayarları** dikey penceresinde hello mobil uygulama arka ucu için.</span><span class="sxs-lookup"><span data-stu-id="6e264-355">Once hello Mobile App backend is provisioned, hello portal opens hello **Settings** blade for hello Mobile App backend.</span></span>

<span data-ttu-id="6e264-356">Merhaba mobil uygulama arka ucu oluşturulduktan sonra tooeither seçebilirsiniz varolan bir SQL veritabanı tooyour mobil uygulama arka bağlayın veya yeni bir SQL veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6e264-356">Once hello Mobile App backend is created, you can choose tooeither connect an existing SQL database tooyour Mobile App backend or create a new SQL database.</span></span>  <span data-ttu-id="6e264-357">Bu bölümde, bir SQL veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6e264-357">In this section, we create a SQL database.</span></span>

> [!NOTE]
> <span data-ttu-id="6e264-358">Bir veritabanı hello zaten varsa hello mobil uygulama arka ucu ile aynı konumda, bunun yerine seçebilirsiniz **varolan veritabanını kullan** sonra bu veritabanını seçin.</span><span class="sxs-lookup"><span data-stu-id="6e264-358">If you already have a database in hello same location as hello mobile app backend, you can instead choose **Use an existing database** and then select that database.</span></span> <span data-ttu-id="6e264-359">bir veritabanı farklı bir konumda Hello kullanımını daha yüksek gecikme nedeniyle önerilmez.</span><span class="sxs-lookup"><span data-stu-id="6e264-359">hello use of a database in a different location is not recommended because of higher latencies.</span></span>
>
>

1. <span data-ttu-id="6e264-360">Merhaba yeni mobil uygulama arka ucunda tıklatın **ayarları** > **mobil uygulama** > **veri** > **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6e264-360">In hello new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span></span>
2. <span data-ttu-id="6e264-361">Merhaba, **veri bağlantısı Ekle** dikey penceresinde tıklatın **SQL veritabanı - gerekli ayarları Yapılandır** > **yeni bir veritabanı oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="6e264-361">In hello **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span></span>  <span data-ttu-id="6e264-362">Hello Hello hello yeni veritabanının adını girin **adı** alan.</span><span class="sxs-lookup"><span data-stu-id="6e264-362">Enter hello name of hello new database in hello **Name** field.</span></span>
3. <span data-ttu-id="6e264-363">Tıklatın **Server**.</span><span class="sxs-lookup"><span data-stu-id="6e264-363">Click **Server**.</span></span>  <span data-ttu-id="6e264-364">Merhaba, **yeni sunucu** dikey penceresinde hello bir benzersiz sunucu adı girin **sunucu adı** alan ve uygun bir sağlamak **Sunucu Yöneticisi oturum açma** ve **parola**.</span><span class="sxs-lookup"><span data-stu-id="6e264-364">In hello **New server** blade, enter a unique server name in hello **Server name** field, and provide a suitable **Server admin login** and **Password**.</span></span>  <span data-ttu-id="6e264-365">Olun **izin azure Hizmetleri tooaccess sunucusu** denetlenir.</span><span class="sxs-lookup"><span data-stu-id="6e264-365">Ensure **Allow azure services tooaccess server** is checked.</span></span>  <span data-ttu-id="6e264-366">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e264-366">Click **OK**.</span></span>

    ![Bir Azure SQL veritabanı oluşturma][6]
4. <span data-ttu-id="6e264-368">Merhaba üzerinde **yeni veritabanı** dikey penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="6e264-368">On hello **New database** blade, click **OK**.</span></span>
5. <span data-ttu-id="6e264-369">Merhaba üzerinde geri **veri bağlantısı Ekle** dikey penceresinde, select **bağlantı dizesi**, hello oturum açma ve hello veritabanı oluşturulurken sağlanan parola girin.</span><span class="sxs-lookup"><span data-stu-id="6e264-369">Back on hello **Add data connection** blade, select **Connection string**, enter hello login and password that you provided when creating hello database.</span></span>  <span data-ttu-id="6e264-370">Varolan bir veritabanını kullanıyorsanız, bu veritabanı için hello oturum açma kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="6e264-370">If you use an existing database, provide hello login credentials for that database.</span></span>  <span data-ttu-id="6e264-371">Girilen sonra tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="6e264-371">Once entered, click **OK**.</span></span>
6. <span data-ttu-id="6e264-372">Merhaba üzerinde geri **veri bağlantısı Ekle** dikey penceresinde tekrar tıklatın **Tamam** toocreate hello veritabanı.</span><span class="sxs-lookup"><span data-stu-id="6e264-372">Back on hello **Add data connection** blade again, click **OK** toocreate hello database.</span></span>

<!--- END OF ALTERNATE INCLUDE -->

<span data-ttu-id="6e264-373">Merhaba veritabanı oluşturulması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="6e264-373">Creation of hello database can take a few minutes.</span></span>  <span data-ttu-id="6e264-374">Kullanım hello **bildirimleri** alanı toomonitor hello hello dağıtımının ilerlemesini.</span><span class="sxs-lookup"><span data-stu-id="6e264-374">Use hello **Notifications** area toomonitor hello progress of hello deployment.</span></span>  <span data-ttu-id="6e264-375">Merhaba veritabanı başarıyla dağıtıldığını kadar ilerleme değil.</span><span class="sxs-lookup"><span data-stu-id="6e264-375">Do not progress until hello database has been deployed successfully.</span></span>  <span data-ttu-id="6e264-376">Başarılı bir şekilde dağıtıldığında, bir bağlantı dizesi hello SQL veritabanı örneğinde mobil arka uç uygulama ayarları için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6e264-376">Once successfully deployed, a Connection String is created for hello SQL Database instance in your Mobile backend App Settings.</span></span>  <span data-ttu-id="6e264-377">Bu uygulama ayarını hello görebilirsiniz **ayarları** > **uygulama ayarları** > **bağlantı dizeleri**.</span><span class="sxs-lookup"><span data-stu-id="6e264-377">You can see this app setting in hello **Settings** > **Application settings** > **Connection strings**.</span></span>

### <span data-ttu-id="6e264-378"><a name="howto-tables-auth"></a>Nasıl yapılır: kimlik doğrulaması için erişim tootables gerektir</span><span class="sxs-lookup"><span data-stu-id="6e264-378"><a name="howto-tables-auth"></a>How to: Require authentication for access tootables</span></span>
<span data-ttu-id="6e264-379">Merhaba tabloları uç noktası ile App Service kimlik doğrulaması toouse isterseniz, App Service kimlik doğrulaması hello yapılandırmalısınız [Azure portal] ilk.</span><span class="sxs-lookup"><span data-stu-id="6e264-379">If you wish toouse App Service Authentication with hello tables endpoint, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="6e264-380">Bir Azure uygulama hizmetinde kimlik doğrulaması yapılandırma hakkında daha fazla ayrıntı gözden geçirmek için hello Yapılandırma Kılavuzu hello kimlik sağlayıcısı için toouse düşündüğünüz:</span><span class="sxs-lookup"><span data-stu-id="6e264-380">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="6e264-381">[Nasıl tooconfigure Azure Active Directory kimlik doğrulaması]</span><span class="sxs-lookup"><span data-stu-id="6e264-381">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="6e264-382">[Nasıl tooconfigure Facebook kimlik doğrulaması]</span><span class="sxs-lookup"><span data-stu-id="6e264-382">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="6e264-383">[Nasıl tooconfigure Google kimlik doğrulama]</span><span class="sxs-lookup"><span data-stu-id="6e264-383">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="6e264-384">[Nasıl tooconfigure Microsoft Authentication]</span><span class="sxs-lookup"><span data-stu-id="6e264-384">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="6e264-385">[Nasıl tooconfigure Twitter kimlik doğrulaması]</span><span class="sxs-lookup"><span data-stu-id="6e264-385">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="6e264-386">Her tablo kullanılan toocontrol erişim toohello tablo olabilir bir erişim özelliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="6e264-386">Each table has an access property that can be used toocontrol access toohello table.</span></span>  <span data-ttu-id="6e264-387">Aşağıdaki örnek hello statik olarak tanımlanmış bir tablo ile kimlik doğrulaması gerekli gösterir.</span><span class="sxs-lookup"><span data-stu-id="6e264-387">hello following sample shows a statically defined table with authentication required.</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="6e264-388">Merhaba erişim özellik üç değerden birini alabilir</span><span class="sxs-lookup"><span data-stu-id="6e264-388">hello access property can take one of three values</span></span>

* <span data-ttu-id="6e264-389">*Anonim* Merhaba istemci uygulaması tooread veri kimlik doğrulaması olmadan izin verildiğini gösterir</span><span class="sxs-lookup"><span data-stu-id="6e264-389">*anonymous* indicates that hello client application is allowed tooread data without authentication</span></span>
* <span data-ttu-id="6e264-390">*Kimliği doğrulanmış* Merhaba istemci uygulaması geçerli bir kimlik doğrulama belirteci hello isteğiyle göndermelidir gösterir</span><span class="sxs-lookup"><span data-stu-id="6e264-390">*authenticated* indicates that hello client application must send a valid authentication token with hello request</span></span>
* <span data-ttu-id="6e264-391">*devre dışı* Bu tablo şu anda devre dışı olduğunu gösterir</span><span class="sxs-lookup"><span data-stu-id="6e264-391">*disabled* indicates that this table is currently disabled</span></span>

<span data-ttu-id="6e264-392">Merhaba erişim özelliği tanımsız ise, kimliği doğrulanmamış erişim verilir.</span><span class="sxs-lookup"><span data-stu-id="6e264-392">If hello access property is undefined, unauthenticated access is allowed.</span></span>

### <span data-ttu-id="6e264-393"><a name="howto-tables-getidentity"></a>Nasıl yapılır: tablolarınızı ile kimlik doğrulaması talep kullanın</span><span class="sxs-lookup"><span data-stu-id="6e264-393"><a name="howto-tables-getidentity"></a>How to: Use authentication claims with your tables</span></span>
<span data-ttu-id="6e264-394">Kimlik doğrulama ayarlarken, istenen çeşitli talep ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e264-394">You can set up various claims that are requested when authentication is set up.</span></span>  <span data-ttu-id="6e264-395">Bu talep hello normalde kullanılamaz `context.user` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="6e264-395">These claims are not normally available through hello `context.user` object.</span></span>  <span data-ttu-id="6e264-396">Ancak, bunlar hello kullanılarak alınabilir `context.user.getIdentity()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6e264-396">However, they can be retrieved using hello `context.user.getIdentity()` method.</span></span>  <span data-ttu-id="6e264-397">Merhaba `getIdentity()` yöntemi tooan nesne çözümler Promise döndürür.</span><span class="sxs-lookup"><span data-stu-id="6e264-397">hello `getIdentity()` method returns a Promise that resolves tooan object.</span></span>  <span data-ttu-id="6e264-398">Merhaba nesne kimlik doğrulama yöntemi (facebook, google, twitter, microsoftaccount veya aad) anahtarlanır.</span><span class="sxs-lookup"><span data-stu-id="6e264-398">hello object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span></span>

<span data-ttu-id="6e264-399">Örneğin, Microsoft Account kimlik doğrulaması ve istek hello e-posta adresleri talep ayarlama, aşağıdaki tablo denetleyici hello ile Merhaba e-posta adresi toohello kaydı ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6e264-399">For example, if you set up Microsoft Account authentication and request hello email addresses claim, you can add hello email address toohello record with hello following table controller:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

<span data-ttu-id="6e264-400">toosee hangi talepleri kullanılabilen, bir web tarayıcısı tooview hello kullan `/.auth/me` uç noktası, sitenizin.</span><span class="sxs-lookup"><span data-stu-id="6e264-400">toosee what claims are available, use a web browser tooview hello `/.auth/me` endpoint of your site.</span></span>

### <span data-ttu-id="6e264-401"><a name="howto-tables-disabled"></a>Nasıl yapılır: devre dışı bırak erişim toospecific tablo işlemleri</span><span class="sxs-lookup"><span data-stu-id="6e264-401"><a name="howto-tables-disabled"></a>How to: Disable access toospecific table operations</span></span>
<span data-ttu-id="6e264-402">Merhaba tablosundaki toplama tooappearing içinde kullanılan toocontrol tek tek işlemleri hello erişim özelliği olabilir.</span><span class="sxs-lookup"><span data-stu-id="6e264-402">In addition tooappearing on hello table, hello access property can be used toocontrol individual operations.</span></span>  <span data-ttu-id="6e264-403">Dört işlemleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6e264-403">There are four operations:</span></span>

* <span data-ttu-id="6e264-404">*Okuma* hello tablosundaki hello RESTful alma işlemi</span><span class="sxs-lookup"><span data-stu-id="6e264-404">*read* is hello RESTful GET operation on hello table</span></span>
* <span data-ttu-id="6e264-405">*INSERT* hello tablo bir hello RESTful POST işlem</span><span class="sxs-lookup"><span data-stu-id="6e264-405">*insert* is hello RESTful POST operation on hello table</span></span>
* <span data-ttu-id="6e264-406">*Güncelleştirme* hello tablosundaki hello RESTful düzeltme eki işlemi</span><span class="sxs-lookup"><span data-stu-id="6e264-406">*update* is hello RESTful PATCH operation on hello table</span></span>
* <span data-ttu-id="6e264-407">*silme* hello tablosundaki hello RESTful silme işlemi</span><span class="sxs-lookup"><span data-stu-id="6e264-407">*delete* is hello RESTful DELETE operation on hello table</span></span>

<span data-ttu-id="6e264-408">Örneğin, bir salt okunur kimliği doğrulanmamış tablo tooprovide isteyebilir:</span><span class="sxs-lookup"><span data-stu-id="6e264-408">For example, you may wish tooprovide a read-only unauthenticated table:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <span data-ttu-id="6e264-409"><a name="howto-tables-query"></a>Nasıl yapılır: Tablo işlemleriyle kullanılan hello sorgu Ayarla</span><span class="sxs-lookup"><span data-stu-id="6e264-409"><a name="howto-tables-query"></a>How to: Adjust hello query that is used with table operations</span></span>
<span data-ttu-id="6e264-410">Bir ortak tablo işlemleri için tooprovide hello veri kısıtlanmış bir görünümü gereksinimdir.</span><span class="sxs-lookup"><span data-stu-id="6e264-410">A common requirement for table operations is tooprovide a restricted view of hello data.</span></span>  <span data-ttu-id="6e264-411">Örneğin, yalnızca okuma veya kendi kayıtlarını güncelleştirmek gibi kullanıcı kimliği ile Merhaba etiketli bir tablo kimliğinin sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="6e264-411">For example, you may provide a table that is tagged with hello authenticated user ID such that you can only read or update your own records.</span></span>  <span data-ttu-id="6e264-412">Aşağıdaki tablo tanımı hello bu işlevleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="6e264-412">hello following table definition provides this functionality:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

<span data-ttu-id="6e264-413">Normalde bir sorgu yürütme işlemleri bulunduğu yerle ayarlayabilirsiniz bir sorgu özelliğe sahip yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="6e264-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span></span> <span data-ttu-id="6e264-414">Merhaba sorgu özelliği bir [QueryJS] diğer bir deyişle kullanılan tooconvert veri arka uç hello bir OData sorgu toosomething işlenebilecek nesne.</span><span class="sxs-lookup"><span data-stu-id="6e264-414">hello query property is a [QueryJS] object that is used tooconvert an OData query toosomething that hello data backend can process.</span></span>  <span data-ttu-id="6e264-415">Bir harita (gibi bir önceki hello) basit eşitlik durumlar için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6e264-415">For simple equality cases (like hello preceding one), a map can be used.</span></span> <span data-ttu-id="6e264-416">Belirli SQL yan tümceleri de ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6e264-416">You can also add specific SQL clauses:</span></span>

    context.query.where('myfield eq ?', 'value');

### <span data-ttu-id="6e264-417"><a name="howto-tables-softdelete"></a>Nasıl yapılır: bir tablo üzerinde geçici silme Yapılandır</span><span class="sxs-lookup"><span data-stu-id="6e264-417"><a name="howto-tables-softdelete"></a>How to: Configure soft delete on a table</span></span>
<span data-ttu-id="6e264-418">Geçici silme kayıtları silmez.</span><span class="sxs-lookup"><span data-stu-id="6e264-418">Soft Delete does not actually delete records.</span></span>  <span data-ttu-id="6e264-419">Bunun yerine, bunları silinmiş hello sütun tootrue ayarlayarak hello veritabanında silindi olarak işaretler.</span><span class="sxs-lookup"><span data-stu-id="6e264-419">Instead it marks them as deleted within hello database by setting hello deleted column tootrue.</span></span>  <span data-ttu-id="6e264-420">Merhaba mobil istemci SDK'sı IncludeDeleted() kullanmadıkça hello Azure Mobile Apps SDK sonuçlarından geçici olarak silinen kayıtları otomatik olarak kaldırır.</span><span class="sxs-lookup"><span data-stu-id="6e264-420">hello Azure Mobile Apps SDK automatically removes soft-deleted records from results unless hello Mobile Client SDK uses IncludeDeleted().</span></span>  <span data-ttu-id="6e264-421">Tablo yazılımla için silme, tooconfigure ayarlamak hello `softDelete` hello tablo tanımı dosyasında özellik:</span><span class="sxs-lookup"><span data-stu-id="6e264-421">tooconfigure a table for soft delete, set hello `softDelete` property in hello table definition file:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="6e264-422">Kayıt - bir istemci uygulamasından bir Webjob'un Azure işlevi aracılığıyla veya özel bir API aracılığıyla ya da Temizleme için bir mekanizma oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e264-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span></span>

### <span data-ttu-id="6e264-423"><a name="howto-tables-seeding"></a>Nasıl yapılır: veri veritabanınızla çekirdek</span><span class="sxs-lookup"><span data-stu-id="6e264-423"><a name="howto-tables-seeding"></a>How to: Seed your database with data</span></span>
<span data-ttu-id="6e264-424">Yeni bir uygulama oluştururken, veri içeren bir tablo tooseed isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="6e264-424">When creating a new application, you may wish tooseed a table with data.</span></span>  <span data-ttu-id="6e264-425">Bu gibi hello tablo tanımı JavaScript dosyası içinde yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="6e264-425">This can be done within hello table definition JavaScript file as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="6e264-426">Merhaba tablo hello Azure Mobile Apps SDK'sı tarafından oluşturulduğunda verileri dengeli yalnızca yapılır.</span><span class="sxs-lookup"><span data-stu-id="6e264-426">Seeding of data is only done when hello table is created by hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="6e264-427">Hello tablo içinde hello veritabanı zaten varsa, hiçbir veri hello tabloya eklenen.</span><span class="sxs-lookup"><span data-stu-id="6e264-427">If hello table already exists within hello database, no data is injected into hello table.</span></span>  <span data-ttu-id="6e264-428">Dinamik şema açıksa, şema dağıtılan hello verileri algılanır.</span><span class="sxs-lookup"><span data-stu-id="6e264-428">If dynamic schema is turned on, then the schema is inferred from hello seeded data.</span></span>

<span data-ttu-id="6e264-429">Merhaba açıkça çağırın öneririz `tables.initialize()` hello hizmeti çalışmaya başladığında yöntemi toocreate hello tablo.</span><span class="sxs-lookup"><span data-stu-id="6e264-429">We recommend that you explicitly call hello `tables.initialize()` method toocreate hello table when hello service starts running.</span></span>

### <span data-ttu-id="6e264-430"><a name="Swagger"></a>Nasıl yapılır: Swagger desteğini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="6e264-430"><a name="Swagger"></a>How to: Enable Swagger support</span></span>
<span data-ttu-id="6e264-431">Azure App Service Mobile Apps ile yerleşik gelen [Swagger] destekler.</span><span class="sxs-lookup"><span data-stu-id="6e264-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span></span>  <span data-ttu-id="6e264-432">tooenable Swagger desteği, bir bağımlılık olarak ilk hello swagger kullanıcı arabirimini yükleyin:</span><span class="sxs-lookup"><span data-stu-id="6e264-432">tooenable Swagger support, first install hello swagger-ui as a dependency:</span></span>

    npm install --save swagger-ui

<span data-ttu-id="6e264-433">Yüklendikten sonra Swagger destek hello Azure Mobile Apps oluşturucuda etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6e264-433">Once installed, you can enable Swagger support in hello Azure Mobile Apps constructor:</span></span>

    var mobile = azureMobileApps({ swagger: true });

<span data-ttu-id="6e264-434">Büyük olasılıkla yalnızca istediğiniz tooenable geliştirme sürümlerindeki Swagger desteği.</span><span class="sxs-lookup"><span data-stu-id="6e264-434">You probably only want tooenable Swagger support in development editions.</span></span>  <span data-ttu-id="6e264-435">Bunu yararlanarak yapmak `NODE_ENV` uygulama ayarı:</span><span class="sxs-lookup"><span data-stu-id="6e264-435">You can do this by utilizing the `NODE_ENV` app setting:</span></span>

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

<span data-ttu-id="6e264-436">Merhaba swagger uç nokta http:// bulunduğu*yoursite*.azurewebsites.net/swagger.</span><span class="sxs-lookup"><span data-stu-id="6e264-436">hello swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span></span>  <span data-ttu-id="6e264-437">Merhaba Swagger kullanıcı arabirimini hello aracılığıyla erişebilirsiniz `/swagger/ui` uç noktası.</span><span class="sxs-lookup"><span data-stu-id="6e264-437">You can access hello Swagger UI via hello `/swagger/ui` endpoint.</span></span>  <span data-ttu-id="6e264-438">Tüm uygulamanız toorequire kimlik doğrulamasını seçerseniz, Swagger bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6e264-438">if you choose toorequire authentication across your entire application, Swagger produces an error.</span></span>  <span data-ttu-id="6e264-439">En iyi sonuçlar için kimliği doğrulanmamış tooallow istekleri üzerinden hello Azure App Service kimlik doğrulaması seçin / yetkilendirme ayarları, ardından hello kullanarak kimlik doğrulaması denetimi `table.access` özelliği.</span><span class="sxs-lookup"><span data-stu-id="6e264-439">For best results, choose tooallow unauthenticated requests through in hello Azure App Service Authentication / Authorization settings, then control authentication using hello `table.access` property.</span></span>

<span data-ttu-id="6e264-440">Merhaba Swagger seçeneği tooyour de ekleyebilirsiniz `azureMobile.js` yalnızca Swagger desteği yerel olarak geliştirirken istiyorsanız, dosya.</span><span class="sxs-lookup"><span data-stu-id="6e264-440">You can also add hello Swagger option tooyour `azureMobile.js` file if you only want Swagger support when developing locally.</span></span>

## <a name="a-namepushpush-notifications"></a><span data-ttu-id="6e264-441"><a name="push">Anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="6e264-441"><a name="push">Push notifications</span></span>
<span data-ttu-id="6e264-442">Azure Notification Hubs tooenable ile Mobile Apps, tüm ana platformlarda hedeflenen toosend anında iletme bildirimleri toomillions aygıtların tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="6e264-442">Mobile Apps integrates with Azure Notification Hubs tooenable you toosend targeted push notifications toomillions of devices across all major platforms.</span></span> <span data-ttu-id="6e264-443">Bildirim hub'ları kullanarak gönderimi gönderebilir bildirimleri tooiOS, Android ve Windows cihazları.</span><span class="sxs-lookup"><span data-stu-id="6e264-443">By using Notification Hubs, you can send push notifications tooiOS, Android and Windows devices.</span></span> <span data-ttu-id="6e264-444">Bildirim hub'ları tüm hakkında daha fazla ile yapabilir toolearn bkz [Notification Hubs'a genel bakış](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6e264-444">toolearn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

### <span data-ttu-id="6e264-445"></a><a name="send-push"></a>Nasıl yapılır: anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="6e264-445"></a><a name="send-push"></a>How to: Send push notifications</span></span>
<span data-ttu-id="6e264-446">koddan hello nasıl toouse hello itme nesne toosend yayın anında bildirim tooregistered iOS cihazları gösterir:</span><span class="sxs-lookup"><span data-stu-id="6e264-446">hello following code shows how toouse hello push object toosend a broadcast push notification tooregistered iOS devices:</span></span>

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="6e264-447">Hello istemciden bir şablon İtme kaydı oluşturarak, bunun yerine bir şablon anında iletme iletisi toodevices tüm desteklenen platformlarda gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e264-447">By creating a template push registration from hello client, you can instead send a template push message toodevices on all supported platforms.</span></span> <span data-ttu-id="6e264-448">kodun gösterdiği nasıl aşağıdaki hello toosend bir şablon bildirim:</span><span class="sxs-lookup"><span data-stu-id="6e264-448">hello following code shows how toosend a template notification:</span></span>

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <span data-ttu-id="6e264-449"><a name="push-user"></a>Nasıl yapılır: gönderme anında iletme bildirimleri tooan etiketleri kullanarak kullanıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="6e264-449"><a name="push-user"></a>How to: Send push notifications tooan authenticated user using tags</span></span>
<span data-ttu-id="6e264-450">Kimliği doğrulanmış bir kullanıcı için anında iletme bildirimleri kaydolduğunda, bir kullanıcı kimliği etiketi toohello kayıt otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="6e264-450">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="6e264-451">Bu etiketi kullanarak anında iletme bildirimleri tooall aygıtları belirli bir kullanıcı tarafından kaydedilen gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e264-451">By using this tag, you can send push notifications tooall devices registered by a specific user.</span></span> <span data-ttu-id="6e264-452">Merhaba aşağıdaki kod hello hello isteği yapan kullanıcı SID'si alır ve bu kullanıcı için bir şablon anında iletme bildirimi tooevery aygıt kaydı gönderir:</span><span class="sxs-lookup"><span data-stu-id="6e264-452">hello following code gets hello SID of user making hello request and sends a template push notification tooevery device registration for that user:</span></span>

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="6e264-453">Kimliği doğrulanmış bir istemci anında iletme bildirimleri için kaydolurken kayıt denemeden önce kimlik doğrulamasının tam olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="6e264-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span>

## <span data-ttu-id="6e264-454"><a name="CustomAPI"></a>Özel API'leri</span><span class="sxs-lookup"><span data-stu-id="6e264-454"><a name="CustomAPI"></a> Custom APIs</span></span>
### <span data-ttu-id="6e264-455"><a name="howto-customapi-basic"></a>Nasıl yapılır: özel bir API tanımlayın</span><span class="sxs-lookup"><span data-stu-id="6e264-455"><a name="howto-customapi-basic"></a>How to: Define a custom API</span></span>
<span data-ttu-id="6e264-456">Ayrıca toohello API hello /tables uç noktası aracılığıyla verilere, Azure Mobile Apps özel API kapsamı sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="6e264-456">In addition toohello data access API via hello /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span></span>  <span data-ttu-id="6e264-457">Özel API'leri benzer bir şekilde toohello tablo tanımları tanımlanır ve tüm erişebilir hello aynı olanakları, kimlik doğrulaması dahil.</span><span class="sxs-lookup"><span data-stu-id="6e264-457">Custom APIs are defined in a similar way toohello table definitions and can access all hello same facilities, including authentication.</span></span>

<span data-ttu-id="6e264-458">App Service kimlik doğrulaması özel API ile toouse isterseniz, App Service kimlik doğrulaması hello yapılandırmalısınız [Azure portal] ilk.</span><span class="sxs-lookup"><span data-stu-id="6e264-458">If you wish toouse App Service Authentication with a Custom API, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="6e264-459">Bir Azure uygulama hizmetinde kimlik doğrulaması yapılandırma hakkında daha fazla ayrıntı gözden geçirmek için hello Yapılandırma Kılavuzu hello kimlik sağlayıcısı için toouse düşündüğünüz:</span><span class="sxs-lookup"><span data-stu-id="6e264-459">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="6e264-460">[Nasıl tooconfigure Azure Active Directory kimlik doğrulaması]</span><span class="sxs-lookup"><span data-stu-id="6e264-460">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="6e264-461">[Nasıl tooconfigure Facebook kimlik doğrulaması]</span><span class="sxs-lookup"><span data-stu-id="6e264-461">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="6e264-462">[Nasıl tooconfigure Google kimlik doğrulama]</span><span class="sxs-lookup"><span data-stu-id="6e264-462">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="6e264-463">[Nasıl tooconfigure Microsoft Authentication]</span><span class="sxs-lookup"><span data-stu-id="6e264-463">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="6e264-464">[Nasıl tooconfigure Twitter kimlik doğrulaması]</span><span class="sxs-lookup"><span data-stu-id="6e264-464">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="6e264-465">Özel API'leri çok tanımlanan şekilde tabloları API hello aynı hello.</span><span class="sxs-lookup"><span data-stu-id="6e264-465">Custom APIs are defined in much hello same way as hello Tables API.</span></span>

1. <span data-ttu-id="6e264-466">Oluşturma bir **API** dizini</span><span class="sxs-lookup"><span data-stu-id="6e264-466">Create an **api** directory</span></span>
2. <span data-ttu-id="6e264-467">Hello bir API tanımı JavaScript dosyası oluşturun **API** dizin.</span><span class="sxs-lookup"><span data-stu-id="6e264-467">Create an API definition JavaScript file in hello **api** directory.</span></span>
3. <span data-ttu-id="6e264-468">Kullanım hello alma yöntemini tooimport hello **API** dizin.</span><span class="sxs-lookup"><span data-stu-id="6e264-468">Use hello import method tooimport hello **api** directory.</span></span>

<span data-ttu-id="6e264-469">Daha önce kullandık hello basic uygulama örneği temel alarak hello prototip API tanımı aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6e264-469">Here is hello prototype api definition based on hello basic-app sample we used earlier.</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="6e264-470">Bir örnek hello kullanarak hello sunucu tarihi döndürür API atalım *Date.now()* yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6e264-470">Let's take an example API that returns hello server date using hello *Date.now()* method.</span></span>  <span data-ttu-id="6e264-471">Merhaba api/date.js dosya şöyledir:</span><span class="sxs-lookup"><span data-stu-id="6e264-471">Here is hello api/date.js file:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

<span data-ttu-id="6e264-472">Her bir parametreyi hello standart RESTful fiiller - GET, POST, düzeltme eki veya DELETE biridir.</span><span class="sxs-lookup"><span data-stu-id="6e264-472">Each parameter is one of hello standard RESTful verbs - GET, POST, PATCH, or DELETE.</span></span>  <span data-ttu-id="6e264-473">Merhaba yöntemdir standart bir [ExpressJS Ara] gerekli hello çıkış gönderir işlevi.</span><span class="sxs-lookup"><span data-stu-id="6e264-473">hello method is a standard [ExpressJS Middleware] function that sends hello required output.</span></span>

### <span data-ttu-id="6e264-474"><a name="howto-customapi-auth"></a>Nasıl yapılır: erişim tooa özel API için kimlik doğrulaması gerektirir</span><span class="sxs-lookup"><span data-stu-id="6e264-474"><a name="howto-customapi-auth"></a>How to: Require authentication for access tooa custom API</span></span>
<span data-ttu-id="6e264-475">Azure Mobile Apps SDK'sı hello kimlik doğrulaması uygulayan hello tabloları endpoint ve özel API'leri ile aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="6e264-475">Azure Mobile Apps SDK implements authentication in hello same way for both hello tables endpoint and custom APIs.</span></span>  <span data-ttu-id="6e264-476">Merhaba önceki bölümde geliştirilmiş kimlik doğrulaması toohello API eklemek için Ekle bir **erişim** özelliği:</span><span class="sxs-lookup"><span data-stu-id="6e264-476">To add authentication toohello API developed in hello previous section, add an **access** property:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="6e264-477">Ayrıca, kimlik doğrulama belirli işlemleri belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6e264-477">You can also specify authentication on specific operations:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="6e264-478">Merhaba hello tabloları uç noktası için kullanılan aynı belirteci kimlik doğrulaması gerektiren özel API'leri için kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e264-478">hello same token that is used for hello tables endpoint must be used for custom APIs requiring authentication.</span></span>

### <span data-ttu-id="6e264-479"><a name="howto-customapi-auth"></a>Nasıl yapılır: işlemek büyük dosya yüklemeleri</span><span class="sxs-lookup"><span data-stu-id="6e264-479"><a name="howto-customapi-auth"></a>How to: Handle large file uploads</span></span>
<span data-ttu-id="6e264-480">Azure Mobile Apps SDK'sı hello kullanır [gövde ayrıştırıcı Ara](https://github.com/expressjs/body-parser) tooaccept ve gönderiminiz gövdesi içeriği kodunu çözer.</span><span class="sxs-lookup"><span data-stu-id="6e264-480">Azure Mobile Apps SDK uses hello [body-parser middleware](https://github.com/expressjs/body-parser) tooaccept and decode body content in your submission.</span></span>  <span data-ttu-id="6e264-481">Gövde ayrıştırıcı tooaccept büyük dosya yüklemeleriyle önceden yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6e264-481">You can pre-configure body-parser tooaccept larger file uploads:</span></span>

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="6e264-482">Merhaba, Aktarımdan önce kodlanmış base-64 dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="6e264-482">hello file is base-64 encoded before transmission.</span></span>  <span data-ttu-id="6e264-483">Bu hello gerçek karşıya yükleme hello boyutu artar (ve bu nedenle boyut için hesap hello).</span><span class="sxs-lookup"><span data-stu-id="6e264-483">This increases hello size of hello actual upload (and hence hello size you must account for).</span></span>

### <span data-ttu-id="6e264-484"><a name="howto-customapi-sql"></a>Nasıl yapılır: özel SQL deyimlerini yürütmek</span><span class="sxs-lookup"><span data-stu-id="6e264-484"><a name="howto-customapi-sql"></a>How to: Execute custom SQL statements</span></span>
<span data-ttu-id="6e264-485">Hello Azure Mobile Apps SDK'sı sağlar erişim toohello tooexecute izin vererek tüm içerik hello istek nesnesi aracılığıyla parametreli SQL deyimleri toohello tanımlanmış veri sağlayıcısı kolayca:</span><span class="sxs-lookup"><span data-stu-id="6e264-485">hello Azure Mobile Apps SDK allows access toohello entire Context through hello request object, allowing you tooexecute parameterized SQL statements toohello defined data provider easily:</span></span>

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <span data-ttu-id="6e264-486"><a name="Debugging"></a>Hata ayıklama, kolay tablolar ve kolay API'leri</span><span class="sxs-lookup"><span data-stu-id="6e264-486"><a name="Debugging"></a>Debugging, Easy Tables, and Easy APIs</span></span>
### <span data-ttu-id="6e264-487"><a name="howto-diagnostic-logs"></a>Nasıl yapılır: hata ayıklama, tanılama ve Azure Mobile apps sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="6e264-487"><a name="howto-diagnostic-logs"></a>How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span></span>
<span data-ttu-id="6e264-488">Hello Azure App Service birkaç hata ayıklama ve sorun giderme tekniklerini Node.js uygulamaları için sağlar.</span><span class="sxs-lookup"><span data-stu-id="6e264-488">hello Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span></span>
<span data-ttu-id="6e264-489">Node.js mobil arka uç sorun giderme makaleleri tooget aşağıdaki toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="6e264-489">Refer toohello following articles tooget started in troubleshooting your Node.js Mobile backend:</span></span>

* <span data-ttu-id="6e264-490">[Bir Azure uygulama hizmeti izleme]</span><span class="sxs-lookup"><span data-stu-id="6e264-490">[Monitoring an Azure App Service]</span></span>
* <span data-ttu-id="6e264-491">[Azure uygulama hizmetinde tanılama günlük kaydını etkinleştir]</span><span class="sxs-lookup"><span data-stu-id="6e264-491">[Enable Diagnostic Logging in Azure App Service]</span></span>
* <span data-ttu-id="6e264-492">[Visual Studio'da bir Azure uygulama hizmeti sorunlarını giderme]</span><span class="sxs-lookup"><span data-stu-id="6e264-492">[Troubleshoot an Azure App Service in Visual Studio]</span></span>

<span data-ttu-id="6e264-493">Node.js uygulamalarını erişiminiz tanılama günlük araçları tooa çeşitli.</span><span class="sxs-lookup"><span data-stu-id="6e264-493">Node.js applications have access tooa wide range of diagnostic log tools.</span></span>  <span data-ttu-id="6e264-494">Dahili olarak, Azure Mobile Apps Node.js SDK'sı hello [Winston] tanılama günlük için.</span><span class="sxs-lookup"><span data-stu-id="6e264-494">Internally, hello Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span></span>  <span data-ttu-id="6e264-495">Günlüğü otomatik olarak etkin hata ayıklama modunu etkinleştirme veya ayarı hello tarafından **MS_DebugMode** uygulama ayarı tootrue hello içinde [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="6e264-495">Logging is automatically enabled by enabling debug mode or by setting hello **MS_DebugMode** app setting tootrue in hello [Azure portal].</span></span> <span data-ttu-id="6e264-496">Merhaba tanılama günlüklerini hello üzerinde oluşturulan günlüklerin görünür [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="6e264-496">Generated logs appear in hello Diagnostic Logs on hello [Azure portal].</span></span>

### <span data-ttu-id="6e264-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>Nasıl yapılır: hello Azure portalında kolay tabloları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="6e264-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>How to: Work with Easy Tables in hello Azure portal</span></span>
<span data-ttu-id="6e264-498">Merhaba portalında kolay tabloları oluşturma ve tabloları doğrudan hello portalında çalışmak sağlar.</span><span class="sxs-lookup"><span data-stu-id="6e264-498">Easy Tables in hello portal let you create and work with tables right in hello portal.</span></span> <span data-ttu-id="6e264-499">Tablo işlemleri hello App Service Düzenleyicisi'ni kullanarak da düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e264-499">You can even edit table operations using hello App Service Editor.</span></span>

<span data-ttu-id="6e264-500">Tıkladığınızda **kolay tabloları** arka uç site ayarlarınızda ekleyebilir, değiştirebilir veya bir tablo silme.</span><span class="sxs-lookup"><span data-stu-id="6e264-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span></span> <span data-ttu-id="6e264-501">Merhaba tablodaki verileri de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e264-501">You can also see data in hello table.</span></span>

![Kolay tablolarla çalışma](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

<span data-ttu-id="6e264-503">Merhaba aşağıdaki komutlar hello komut çubuğunda bir tablo için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="6e264-503">hello following commands are available on hello command bar for a table:</span></span>

* <span data-ttu-id="6e264-504">**İzinleri Değiştir** - hello Okuma izinlerini değiştirmek, Ekle, Güncelleştir ve hello tablosunda silme işlemleri.</span><span class="sxs-lookup"><span data-stu-id="6e264-504">**Change permissions** - modify hello permission for read, insert, update and delete operations on hello table.</span></span>
  <span data-ttu-id="6e264-505">Seçeneklerdir tooallow anonim erişim, toorequire kimlik doğrulaması veya toodisable tüm erişim toohello işlemi.</span><span class="sxs-lookup"><span data-stu-id="6e264-505">Options are tooallow anonymous access, toorequire authentication, or toodisable all access toohello operation.</span></span>
* <span data-ttu-id="6e264-506">**Komut dosyasını Düzenle** -hello komut dosyası Merhaba tablonun hello App Service Düzenleyicisi açılır.</span><span class="sxs-lookup"><span data-stu-id="6e264-506">**Edit script** - hello script file for hello table is opened in hello App Service Editor.</span></span>
* <span data-ttu-id="6e264-507">**Şemayı yönetmek** - ekleme veya sütunları silin veya hello tablosu dizini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6e264-507">**Manage schema** - add or delete columns or change hello table index.</span></span>
* <span data-ttu-id="6e264-508">**Düz tablo** -var olan bir tabloyu kesen değişmeden tüm veri satırları silme ancak hello şema bırakarak olabilir.</span><span class="sxs-lookup"><span data-stu-id="6e264-508">**Clear table** - truncates an existing table be deleting all data rows but leaving hello schema unchanged.</span></span>
* <span data-ttu-id="6e264-509">**Satırları Sil** -tek tek veri satırı silin.</span><span class="sxs-lookup"><span data-stu-id="6e264-509">**Delete rows** - delete individual rows of data.</span></span>
* <span data-ttu-id="6e264-510">**Akış günlükleri Görünüm** -günlük hizmeti siteniz için akış toohello bağlanır.</span><span class="sxs-lookup"><span data-stu-id="6e264-510">**View streaming logs** - connects you toohello streaming log service for your site.</span></span>

### <span data-ttu-id="6e264-511"><a name="work-easy-apis"></a>Nasıl yapılır: hello Azure portalında kolay API'leri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="6e264-511"><a name="work-easy-apis"></a>How to: Work with Easy APIs in hello Azure portal</span></span>
<span data-ttu-id="6e264-512">Merhaba portalında kolay API'leri, oluşturma ve özel API'lerini doğrudan hello portalında çalışmak olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="6e264-512">Easy APIs in hello portal let you create and work with custom APIs right in hello portal.</span></span> <span data-ttu-id="6e264-513">API komut dosyalarını hello App Service Düzenleyicisi'ni kullanarak düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e264-513">You can edit API scripts using hello App Service Editor.</span></span>

<span data-ttu-id="6e264-514">Tıkladığınızda **kolay API'leri** arka uç site ayarlarınızda ekleyebilir, değiştirebilir veya özel bir API uç noktasını silmek.</span><span class="sxs-lookup"><span data-stu-id="6e264-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span></span>

![Kolay API'leri ile çalışma](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

<span data-ttu-id="6e264-516">Merhaba Portalı'nda belirli bir HTTP eylemi hello erişim izinlerini değiştirmek, hello API komut dosyası App Service Düzenleyicisi'ni düzenleyin veya hello akış günlükleri görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="6e264-516">In hello portal, you can change hello access permissions for a given HTTP action, edit hello API script file in the App Service Editor, or view hello streaming logs.</span></span>

### <span data-ttu-id="6e264-517"><a name="online-editor"></a>Nasıl yapılır: Düzenle hello App Service Düzenleyicisi kodda</span><span class="sxs-lookup"><span data-stu-id="6e264-517"><a name="online-editor"></a>How to: Edit code in hello App Service Editor</span></span>
<span data-ttu-id="6e264-518">Hello Azure portal hello proje tooyour yerel bilgisayar yüklemeye gerek kalmadan Node.js arka uç komut dosyalarınızı hello App Service Düzenleyicisi'ni düzenlemenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="6e264-518">hello Azure portal lets you edit your Node.js backend script files in hello App Service Editor without having to download hello project tooyour local computer.</span></span> <span data-ttu-id="6e264-519">Merhaba çevrimiçi düzenleyicisinde tooedit komut dosyaları:</span><span class="sxs-lookup"><span data-stu-id="6e264-519">tooedit script files in hello online editor:</span></span>

1. <span data-ttu-id="6e264-520">Mobil uygulama arka uç dikey penceresinde tıklayın **tüm ayarları** > ya da **kolay tablolar** veya **kolay API'leri**, bir tablo veya API'ı tıklatın **Düzenle betik**.</span><span class="sxs-lookup"><span data-stu-id="6e264-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span></span> <span data-ttu-id="6e264-521">Merhaba komut dosyası hello App Service Düzenleyicisi açılır.</span><span class="sxs-lookup"><span data-stu-id="6e264-521">hello script file is opened in hello App Service Editor.</span></span>

    ![Uygulama hizmeti Düzenleyicisi](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. <span data-ttu-id="6e264-523">Değişiklikleri toohello kodu dosyanızda hello çevrimiçi düzenleyicisinde olun.</span><span class="sxs-lookup"><span data-stu-id="6e264-523">Make your changes toohello code file in hello online editor.</span></span> <span data-ttu-id="6e264-524">Siz yazarken değişiklikler otomatik olarak kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="6e264-524">Changes are saved automatically as you type.</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Android istemci hızlı başlangıç]: app-service-mobile-android-get-started.md
[Apache Cordova istemci hızlı başlangıç]: app-service-mobile-cordova-get-started.md
[iOS istemci hızlı başlangıç]: app-service-mobile-ios-get-started.md
[Xamarin.iOS istemcisi hızlı başlangıç]: app-service-mobile-xamarin-ios-get-started.md
[Xamarin.Android istemcisi hızlı başlangıç]: app-service-mobile-xamarin-android-get-started.md
[Xamarin.Forms istemci hızlı başlangıç]: app-service-mobile-xamarin-forms-get-started.md
[Windows mağazası istemci hızlı başlangıç]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[çevrimdışı veri eşitlemeye]: app-service-mobile-offline-data-sync.md
[Nasıl tooconfigure Azure Active Directory kimlik doğrulaması]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Nasıl tooconfigure Facebook kimlik doğrulaması]: app-service-mobile-how-to-configure-facebook-authentication.md
[Nasıl tooconfigure Google kimlik doğrulama]: app-service-mobile-how-to-configure-google-authentication.md
[Nasıl tooconfigure Microsoft Authentication]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Nasıl tooconfigure Twitter kimlik doğrulaması]: app-service-mobile-how-to-configure-twitter-authentication.md
[Azure App Service Deployment Guide]: ../app-service-web/web-sites-deploy.md
[Bir Azure uygulama hizmeti izleme]: ../app-service-web/web-sites-monitor.md
[Azure uygulama hizmetinde tanılama günlük kaydını etkinleştir]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Visual Studio'da bir Azure uygulama hizmeti sorunlarını giderme]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[hello düğümü sürümü belirtin]: ../nodejs-specify-node-version-azure-apps.md
[düğümü modüllerini kullanma]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[Azure portal]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp örnek github'da]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[Yapılacaklar örneği github'daki]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[örnekler dizini github'da]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Visual Studio için Node.js araçları 1.1]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js paket]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Ara]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
