---
title: aaaNode.js Getting Started Guide | Microsoft Docs
description: "Nasıl toocreate basit bir Node.js web uygulaması ve tooan Azure bulut hizmeti dağıtmak öğrenin."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a><span data-ttu-id="7bdc4-103">Derleme ve bir Node.js uygulaması tooan Azure bulut hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="7bdc4-103">Build and deploy a Node.js application tooan Azure Cloud Service</span></span>

<span data-ttu-id="7bdc4-104">Bu öğreticide gösterilmiştir nasıl toocreate basit bir Node.js uygulama bir Azure bulut hizmeti çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-104">This tutorial shows how toocreate a simple Node.js application running in an Azure Cloud Service.</span></span> <span data-ttu-id="7bdc4-105">Bulut, azure'daki ölçeklenebilir bulut uygulamalarının yapı taşları hello hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-105">Cloud Services are hello building blocks of scalable cloud applications in Azure.</span></span> <span data-ttu-id="7bdc4-106">Merhaba ayırma ve bağımsız yönetimi ile uygulamanızın ön uç ve arka uç bileşenlerinin genişleme sağlarlar.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-106">They allow hello separation and independent management and scale-out of front-end and back-end components of your application.</span></span>  <span data-ttu-id="7bdc4-107">Cloud Services her bir rolü güvenilir bir şekilde barındırmaya yönelik sağlam bir özel sanal makine sağlar.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span></span>

<span data-ttu-id="7bdc4-108">Bulut Hizmetleri ve bunların nasıl tooAzure Web siteleri ve sanal makineleri karşılaştırın hakkında daha fazla bilgi için bkz: [Azure Websites, Cloud Services ve sanal makineleri karşılaştırma].</span><span class="sxs-lookup"><span data-stu-id="7bdc4-108">For more information on Cloud Services, and how they compare tooAzure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span></span>

> [!TIP]
> <span data-ttu-id="7bdc4-109">Toobuild basit bir Web sitesi mi arıyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="7bdc4-109">Looking toobuild a simple website?</span></span> <span data-ttu-id="7bdc4-110">Senaryonuz yalnızca basit bir web sitesi ön ucu içeriyorsa, [basit bir web uygulaması kullanmayı] düşünün.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span></span> <span data-ttu-id="7bdc4-111">Web uygulamanız büyüdükçe ve gereksinimleriniz değiştikçe kolayca bulut hizmeti tooa yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-111">You can easily upgrade tooa Cloud Service as your web app grows and your requirements change.</span></span>

<span data-ttu-id="7bdc4-112">Bu öğreticiyi izleyerek bir web rolünün içinde barındırılan basit bir web uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span></span> <span data-ttu-id="7bdc4-113">Merhaba işlem öykünücüsü tootest uygulamanızı yerel olarak kullanın ardından PowerShell komut satırı araçlarını kullanarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-113">You will use hello compute emulator tootest your application locally, then deploy it using PowerShell command-line tools.</span></span>

<span data-ttu-id="7bdc4-114">Merhaba, basit bir "hello world" uygulaması uygulamadır:</span><span class="sxs-lookup"><span data-stu-id="7bdc4-114">hello application is a simple "hello world" application:</span></span>

![Merhaba Hello World web sayfasını gösteren bir web tarayıcısı][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a><span data-ttu-id="7bdc4-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7bdc4-116">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="7bdc4-117">Bu öğretici Windows gerektiren Azure PowerShell’i kullanır.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-117">This tutorial uses Azure PowerShell, which requires Windows.</span></span>

* <span data-ttu-id="7bdc4-118">[Azure PowerShell]'i yükleyip yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-118">Install and configure [Azure Powershell].</span></span>
* <span data-ttu-id="7bdc4-119">Merhaba yükleyip [.NET 2.7 için Azure SDK].</span><span class="sxs-lookup"><span data-stu-id="7bdc4-119">Download and install hello [Azure SDK for .NET 2.7].</span></span> <span data-ttu-id="7bdc4-120">Kurulum Hello yüklemek, seçin:</span><span class="sxs-lookup"><span data-stu-id="7bdc4-120">In hello install setup, select:</span></span>
  * <span data-ttu-id="7bdc4-121">MicrosoftAzureAuthoringTools</span><span class="sxs-lookup"><span data-stu-id="7bdc4-121">MicrosoftAzureAuthoringTools</span></span>
  * <span data-ttu-id="7bdc4-122">MicrosoftAzureComputeEmulator</span><span class="sxs-lookup"><span data-stu-id="7bdc4-122">MicrosoftAzureComputeEmulator</span></span>

## <a name="create-an-azure-cloud-service-project"></a><span data-ttu-id="7bdc4-123">Azure Cloud Service projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="7bdc4-123">Create an Azure Cloud Service project</span></span>
<span data-ttu-id="7bdc4-124">Aşağıdaki görevler toocreate temel Node.js iskelesiyle birlikte yeni bir Azure bulut hizmeti projesi hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7bdc4-124">Perform hello following tasks toocreate a new Azure Cloud Service project, along with basic Node.js scaffolding:</span></span>

1. <span data-ttu-id="7bdc4-125">Çalıştırma **Windows PowerShell** yönetici olarak; hello **Başlat menüsü** veya **Başlat ekranında**, arama **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-125">Run **Windows PowerShell** as Administrator; from hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span>
2. <span data-ttu-id="7bdc4-126">[PowerShell'i bağlayın] tooyour abonelik.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-126">[Connect PowerShell] tooyour subscription.</span></span>
3. <span data-ttu-id="7bdc4-127">PowerShell cmdlet toocreate toocreate hello proje aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="7bdc4-127">Enter hello following PowerShell cmdlet toocreate toocreate hello project:</span></span>

        New-AzureServiceProject helloworld

    ![Merhaba hello New-AzureService helloworld komutunun sonucu][hello result of hello New-AzureService helloworld command]

    <span data-ttu-id="7bdc4-129">Merhaba **New-AzureServiceProject** cmdlet'i bir Node.js uygulaması tooa bulut hizmeti yayımlamak için basit bir yapı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-129">hello **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application tooa Cloud Service.</span></span> <span data-ttu-id="7bdc4-130">Yayımlama tooAzure için gerekli yapılandırma dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-130">It contains configuration files necessary for publishing tooAzure.</span></span> <span data-ttu-id="7bdc4-131">Merhaba cmdlet'i ayrıca hello hizmeti için çalışma dizini toohello dizini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-131">hello cmdlet also changes your working directory toohello directory for hello service.</span></span>

    <span data-ttu-id="7bdc4-132">Merhaba cmdlet aşağıdaki dosyaları hello oluşturur:</span><span class="sxs-lookup"><span data-stu-id="7bdc4-132">hello cmdlet creates hello following files:</span></span>

   * <span data-ttu-id="7bdc4-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** ve **ServiceDefinition.csdef**: Uygulamanızı yayımlamak için gereken Azure’a özel dosyalar.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span></span> <span data-ttu-id="7bdc4-134">Daha fazla bilgi için bkz. [Azure için Barındırılan Hizmet Oluşturmaya Genel Bakış].</span><span class="sxs-lookup"><span data-stu-id="7bdc4-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
   * <span data-ttu-id="7bdc4-135">**deploymentSettings.json**: hello Azure PowerShell dağıtım cmdlet'leri tarafından kullanılan yerel ayarları depolar.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-135">**deploymentSettings.json**: Stores local settings that are used by hello Azure PowerShell deployment cmdlets.</span></span>
4. <span data-ttu-id="7bdc4-136">Komut tooadd yeni bir web rolü aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="7bdc4-136">Enter hello following command tooadd a new web role:</span></span>

       Add-AzureNodeWebRole

   ![Merhaba hello Add-AzureNodeWebRole komutunun çıktısı][hello output of hello Add-AzureNodeWebRole command]

   <span data-ttu-id="7bdc4-138">Merhaba **Add-AzureNodeWebRole** cmdlet'i basit bir Node.js uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-138">hello **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span></span> <span data-ttu-id="7bdc4-139">Ayrıca hello değiştirdiği **.csfg** ve **.csdef** tooadd hello yeni rol için yapılandırma girdileri dosyaları.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-139">It also modifies hello **.csfg** and **.csdef** files tooadd configuration entries for hello new role.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7bdc4-140">Bir rol adı belirtmezseniz varsayılan ad kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-140">If you do not specify a role name, a default name is used.</span></span> <span data-ttu-id="7bdc4-141">Bir ad hello birinci cmdlet parametresi olarak sağlayabilirsiniz:`Add-AzureNodeWebRole MyRole`</span><span class="sxs-lookup"><span data-stu-id="7bdc4-141">You can provide a name as hello first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span></span>

<span data-ttu-id="7bdc4-142">Merhaba Node.js uygulaması hello dosyasında tanımlanan **server.js**hello web rolü için hello dizininde bulunan (**WebRole1** varsayılan olarak).</span><span class="sxs-lookup"><span data-stu-id="7bdc4-142">hello Node.js app is defined in hello file **server.js**, located in hello directory for hello web role (**WebRole1** by default).</span></span> <span data-ttu-id="7bdc4-143">Merhaba kod aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="7bdc4-143">Here is hello code:</span></span>

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

<span data-ttu-id="7bdc4-144">Bu kod temelde "Hello World" Merhaba aynı örnek üzerinde hello hello olan [nodejs.org] Web sitesi, hello bulut ortamı tarafından atanan hello bağlantı noktası numarasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-144">This code is essentially hello same as hello "Hello World" sample on hello [nodejs.org] website, except it uses hello port number assigned by hello cloud environment.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="7bdc4-145">Merhaba uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="7bdc4-145">Deploy hello application tooAzure</span></span>

> [!NOTE]
> <span data-ttu-id="7bdc4-146">toocomplete Bu öğretici bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-146">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="7bdc4-147">[MSDN abone avantajınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) ya da [ücretsiz hesap için kaydolabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span><span class="sxs-lookup"><span data-stu-id="7bdc4-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="download-hello-azure-publishing-settings"></a><span data-ttu-id="7bdc4-148">Hello Azure indirme ayarları yayımlama</span><span class="sxs-lookup"><span data-stu-id="7bdc4-148">Download hello Azure publishing settings</span></span>
<span data-ttu-id="7bdc4-149">toodeploy, uygulama tooAzure önce ayarları Azure aboneliğinizin yayımlama hello indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-149">toodeploy your application tooAzure, you must first download hello publishing settings for your Azure subscription.</span></span>

1. <span data-ttu-id="7bdc4-150">Merhaba aşağıdaki Azure PowerShell cmdlet'ini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7bdc4-150">Run hello following Azure PowerShell cmdlet:</span></span>

       Get-AzurePublishSettingsFile

   <span data-ttu-id="7bdc4-151">Bu, tarayıcınızı kullanır toonavigate toohello yayımlama ayarları indirme sayfası.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-151">This will use your browser toonavigate toohello publish settings download page.</span></span> <span data-ttu-id="7bdc4-152">Bir Microsoft Account istendiğinde toolog olabilir.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-152">You may be prompted toolog in with a Microsoft Account.</span></span> <span data-ttu-id="7bdc4-153">Bu durumda, Azure aboneliğinizle ilişkili hello hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-153">If so, use hello account associated with your Azure subscription.</span></span>

   <span data-ttu-id="7bdc4-154">Kolayca erişebilirsiniz indirilen hello profil tooa dosya konumuna kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-154">Save hello downloaded profile tooa file location you can easily access.</span></span>
2. <span data-ttu-id="7bdc4-155">Cmdlet'i tooimport hello profil indirdiğiniz yayımlama çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7bdc4-155">Run following cmdlet tooimport hello publishing profile you downloaded:</span></span>

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > <span data-ttu-id="7bdc4-156">Merhaba aldıktan sonra yayımlama ayarları, birisi verebilecek bilgiler içerdiğinden indirdiğiniz .publishSettings dosyasını hello silme göz önünde bulundurun tooaccess hesabınızı.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-156">After importing hello publish settings, consider deleting hello downloaded .publishSettings file, because it contains information that could allow someone tooaccess your account.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="7bdc4-157">Merhaba uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="7bdc4-157">Publish hello application</span></span>
<span data-ttu-id="7bdc4-158">toopublish, hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7bdc4-158">toopublish, run hello following commands:</span></span>

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* <span data-ttu-id="7bdc4-159">**-ServiceName** hello dağıtım hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-159">**-ServiceName** specifies hello name for hello deployment.</span></span> <span data-ttu-id="7bdc4-160">Bu benzersiz bir ad olmalıdır, aksi takdirde hello yayımlama işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-160">This must be a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="7bdc4-161">Merhaba **Get-Date** komutu tacks hello adın benzersiz olması bir tarih dizesi.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-161">hello **Get-Date** command tacks on a date/time string that should make hello name unique.</span></span>
* <span data-ttu-id="7bdc4-162">**-Location** hello uygulama içinde barındırılan hello datacenter belirtir.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-162">**-Location** specifies hello datacenter that hello application will be hosted in.</span></span> <span data-ttu-id="7bdc4-163">toosee kullanılabilir veri merkezlerinin, kullanım hello listesini **Get-AzureLocation** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-163">toosee a list of available datacenters, use hello **Get-AzureLocation** cmdlet.</span></span>
* <span data-ttu-id="7bdc4-164">**-Launch** bir tarayıcı penceresi açar ve dağıtım tamamlandıktan sonra barındırılan toohello hizmet gider.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-164">**-Launch** opens a browser window and navigates toohello hosted service after deployment has completed.</span></span>

<span data-ttu-id="7bdc4-165">Yayımlama başarılı olduktan sonra yanıt benzer toohello aşağıdaki görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="7bdc4-165">After publishing succeeds, you will see a response similar toohello following:</span></span>

![Merhaba hello Publish-AzureService komutunun çıktısı][hello output of hello Publish-AzureService command]

> [!NOTE]
> <span data-ttu-id="7bdc4-167">Bu hello uygulama toodeploy için birkaç dakika sürer ve ilk kez yayımlandığında kullanılabilir hale gelir.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-167">It can take several minutes for hello application toodeploy and become available when first published.</span></span>

<span data-ttu-id="7bdc4-168">Merhaba dağıtım tamamlandıktan sonra bir tarayıcı penceresi açın ve toohello bulut hizmetine gidin.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-168">Once hello deployment has completed, a browser window will open and navigate toohello cloud service.</span></span>

![Merhaba hello world sayfasını gösteren bir tarayıcı penceresi; Merhaba URL hello sayfanın Azure'da barındırıldığını gösterir.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

<span data-ttu-id="7bdc4-170">Uygulamanız artık Azure üzerinde çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-170">Your application is now running on Azure.</span></span>

<span data-ttu-id="7bdc4-171">Merhaba **Publish-AzureServiceProject** cmdlet'i hello aşağıdaki adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="7bdc4-171">hello **Publish-AzureServiceProject** cmdlet performs hello following steps:</span></span>

1. <span data-ttu-id="7bdc4-172">Bir paket toodeploy oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-172">Creates a package toodeploy.</span></span> <span data-ttu-id="7bdc4-173">Hello paket, uygulama klasöründeki tüm hello dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-173">hello package contains all hello files in your application folder.</span></span>
2. <span data-ttu-id="7bdc4-174">Mevcut değilse yeni bir **depolama hesabı** oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-174">Creates a new **storage account** if one does not exist.</span></span> <span data-ttu-id="7bdc4-175">Hello Azure depolama hesabı, dağıtım sırasında kullanılan toostore hello uygulama paketi değil.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-175">hello Azure storage account is used toostore hello application package during deployment.</span></span> <span data-ttu-id="7bdc4-176">Dağıtımını gerçekleştirdikten sonra hello depolama hesabı güvenle silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-176">You can safely delete hello storage account after deployment is done.</span></span>
3. <span data-ttu-id="7bdc4-177">Henüz mevcut değilse yeni bir **bulut hizmeti** oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-177">Creates a new **cloud service** if one does not already exist.</span></span> <span data-ttu-id="7bdc4-178">A **bulut hizmeti** , uygulamanızın barındırıldığını dağıtılan tooAzure olduğunda hello kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-178">A **cloud service** is hello container in which your application is hosted when it is deployed tooAzure.</span></span> <span data-ttu-id="7bdc4-179">Daha fazla bilgi için bkz. [Azure için Barındırılan Hizmet Oluşturmaya Genel Bakış].</span><span class="sxs-lookup"><span data-stu-id="7bdc4-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
4. <span data-ttu-id="7bdc4-180">Merhaba dağıtım paketi tooAzure yayımlar.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-180">Publishes hello deployment package tooAzure.</span></span>

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="7bdc4-181">Uygulamanızı durdurma ve silme</span><span class="sxs-lookup"><span data-stu-id="7bdc4-181">Stopping and deleting your application</span></span>
<span data-ttu-id="7bdc4-182">Uygulamanızı dağıttıktan sonra toodisable isteyebilirsiniz, ek maliyetlerden kaçınmak için.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-182">After deploying your application, you may want toodisable it so you can avoid extra costs.</span></span> <span data-ttu-id="7bdc4-183">Azure web rolü örneklerini harcanan sunucu saati başına faturalandırır.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-183">Azure bills web role instances per hour of server time consumed.</span></span> <span data-ttu-id="7bdc4-184">Uygulamanızı dağıtıldığında Hello örnekler çalışmadığında ve hello durdurulmuş durumda olsa bile sunucu saati harcanır.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-184">Server time is consumed once your application is deployed, even if hello instances are not running and are in hello stopped state.</span></span>

1. <span data-ttu-id="7bdc4-185">Merhaba Windows PowerShell penceresinde hello hizmet dağıtımı cmdlet aşağıdaki hello ile Merhaba önceki bölümde oluşturduğunuz durdurun:</span><span class="sxs-lookup"><span data-stu-id="7bdc4-185">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

       Stop-AzureService

   <span data-ttu-id="7bdc4-186">Merhaba hizmetin durdurulması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-186">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="7bdc4-187">Merhaba hizmet durdurulduğunda bunu belirten bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-187">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

   ![Hello hello Stop-AzureService komutunun durumu][hello status of hello Stop-AzureService command]
2. <span data-ttu-id="7bdc4-189">toodelete hello hizmeti, cmdlet aşağıdaki çağrı hello:</span><span class="sxs-lookup"><span data-stu-id="7bdc4-189">toodelete hello service, call hello following cmdlet:</span></span>

       Remove-AzureService

   <span data-ttu-id="7bdc4-190">İstendiğinde, girin **Y** toodelete hello hizmet.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-190">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="7bdc4-191">Merhaba hizmetin silinmesi birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-191">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="7bdc4-192">Merhaba hizmet silindikten sonra hello hizmeti silinmiş olduğunu belirten bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-192">After hello service has been deleted you receive a message indicating that hello service was deleted.</span></span>

   ![Merhaba Remove-AzureService komutunun Hello durumu][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > <span data-ttu-id="7bdc4-194">Merhaba hizmetin silinmesi hello hizmet ilk kez yayımlandığında oluşturulan hello depolama hesabı silmez ve kullanılan depolama alanı için fatura toobe devam eder.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-194">Deleting hello service does not delete hello storage account that was created when hello service was initially published, and you will continue toobe billed for storage used.</span></span> <span data-ttu-id="7bdc4-195">Hiçbir şey hello depo kullanıyorsa toodelete isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7bdc4-195">If nothing else is using hello storage, you may want toodelete it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bdc4-196">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7bdc4-196">Next steps</span></span>
<span data-ttu-id="7bdc4-197">Daha fazla bilgi için bkz: Merhaba [Node.js Geliştirici Merkezi].</span><span class="sxs-lookup"><span data-stu-id="7bdc4-197">For more information, see hello [Node.js Developer Center].</span></span>

<!-- URL List -->

[Azure Websites, Cloud Services ve sanal makineleri karşılaştırma]: ../app-service-web/choose-web-site-cloud-service-vm.md
[basit bir web uygulaması kullanmayı]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure PowerShell]: /powershell/azureps-cmdlets-docs
[.NET 2.7 için Azure SDK]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[PowerShell'i bağlayın]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Azure için Barındırılan Hizmet Oluşturmaya Genel Bakış]: https://azure.microsoft.com/documentation/services/cloud-services/
[Node.js Geliştirici Merkezi]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
