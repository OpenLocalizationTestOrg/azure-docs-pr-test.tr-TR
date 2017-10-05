---
title: "Node.js Başlangıç Kılavuzu | Microsoft Belgeleri"
description: "Basit bir Node.js web uygulaması oluşturma ve Azure bulut hizmetine dağıtma hakkında bilgi edinin."
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
ms.openlocfilehash: 980643f35c78bbae7b1b12336331ca15ad4fb89b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="build-and-deploy-a-nodejs-application-to-an-azure-cloud-service"></a><span data-ttu-id="c358a-103">Bir Node.js uygulaması derleme ve Azure Cloud Service’e dağıtma</span><span class="sxs-lookup"><span data-stu-id="c358a-103">Build and deploy a Node.js application to an Azure Cloud Service</span></span>

<span data-ttu-id="c358a-104">Bu öğreticide Azure Cloud Service’te çalışan basit bir Node.js uygulamasını oluşturma işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c358a-104">This tutorial shows how to create a simple Node.js application running in an Azure Cloud Service.</span></span> <span data-ttu-id="c358a-105">Cloud Services, Azure’daki ölçeklenebilir bulut uygulamalarının yapı taşlarıdır.</span><span class="sxs-lookup"><span data-stu-id="c358a-105">Cloud Services are the building blocks of scalable cloud applications in Azure.</span></span> <span data-ttu-id="c358a-106">Uygulamanızın ön uç ve arka uç bileşenlerinin ayrılmasına ve bağımsız yönetimi ile ölçek artırımına imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="c358a-106">They allow the separation and independent management and scale-out of front-end and back-end components of your application.</span></span>  <span data-ttu-id="c358a-107">Cloud Services her bir rolü güvenilir bir şekilde barındırmaya yönelik sağlam bir özel sanal makine sağlar.</span><span class="sxs-lookup"><span data-stu-id="c358a-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span></span>

<span data-ttu-id="c358a-108">Cloud Services ve Azure Websites ile Virtual machines hizmetlerine benzerlikleri hakkında daha fazla bilgi için bkz. [Azure Websites, Cloud Services ve Virtual Machines karşılaştırması].</span><span class="sxs-lookup"><span data-stu-id="c358a-108">For more information on Cloud Services, and how they compare to Azure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span></span>

> [!TIP]
> <span data-ttu-id="c358a-109">Basit bir web sitesi tasarlamak mı istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="c358a-109">Looking to build a simple website?</span></span> <span data-ttu-id="c358a-110">Senaryonuz yalnızca basit bir web sitesi ön ucu içeriyorsa, [basit bir web uygulaması kullanmayı] düşünün.</span><span class="sxs-lookup"><span data-stu-id="c358a-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span></span> <span data-ttu-id="c358a-111">Web uygulamanız büyüdükçe ve gereksinimleriniz değiştikçe kolayca Cloud Services’e yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c358a-111">You can easily upgrade to a Cloud Service as your web app grows and your requirements change.</span></span>

<span data-ttu-id="c358a-112">Bu öğreticiyi izleyerek bir web rolünün içinde barındırılan basit bir web uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c358a-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span></span> <span data-ttu-id="c358a-113">Uygulamanızı yerel olarak test etmek ve ardından PowerShell komut satırı araçlarını kullanarak dağıtmak için işlem öykünücüsünü kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c358a-113">You will use the compute emulator to test your application locally, then deploy it using PowerShell command-line tools.</span></span>

<span data-ttu-id="c358a-114">Uygulama basit bir "hello world" uygulamasıdır:</span><span class="sxs-lookup"><span data-stu-id="c358a-114">The application is a simple "hello world" application:</span></span>

![Hello World web sayfasını gösteren bir web tarayıcısı][A web browser displaying the Hello World web page]

## <a name="prerequisites"></a><span data-ttu-id="c358a-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c358a-116">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="c358a-117">Bu öğretici Windows gerektiren Azure PowerShell’i kullanır.</span><span class="sxs-lookup"><span data-stu-id="c358a-117">This tutorial uses Azure PowerShell, which requires Windows.</span></span>

* <span data-ttu-id="c358a-118">[Azure PowerShell]'i yükleyip yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c358a-118">Install and configure [Azure Powershell].</span></span>
* <span data-ttu-id="c358a-119">[.NET 2.7 için Azure SDK’sını] indirip yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c358a-119">Download and install the [Azure SDK for .NET 2.7].</span></span> <span data-ttu-id="c358a-120">Yükleme kurulumunda şunları seçin:</span><span class="sxs-lookup"><span data-stu-id="c358a-120">In the install setup, select:</span></span>
  * <span data-ttu-id="c358a-121">MicrosoftAzureAuthoringTools</span><span class="sxs-lookup"><span data-stu-id="c358a-121">MicrosoftAzureAuthoringTools</span></span>
  * <span data-ttu-id="c358a-122">MicrosoftAzureComputeEmulator</span><span class="sxs-lookup"><span data-stu-id="c358a-122">MicrosoftAzureComputeEmulator</span></span>

## <a name="create-an-azure-cloud-service-project"></a><span data-ttu-id="c358a-123">Azure Cloud Service projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c358a-123">Create an Azure Cloud Service project</span></span>
<span data-ttu-id="c358a-124">Temel Node.js iskelesiyle birlikte yeni bir Azure Cloud Service projesi oluşturmak için aşağıdaki görevleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c358a-124">Perform the following tasks to create a new Azure Cloud Service project, along with basic Node.js scaffolding:</span></span>

1. <span data-ttu-id="c358a-125">**Windows PowerShell**’i Yönetici olarak çalıştırın; **Başlat Menüsü** veya **Başlangıç Ekranı**’ndan **Windows PowerShell** araması yapın.</span><span class="sxs-lookup"><span data-stu-id="c358a-125">Run **Windows PowerShell** as Administrator; from the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span>
2. <span data-ttu-id="c358a-126">Aboneliğinize [PowerShell’i bağlayın].</span><span class="sxs-lookup"><span data-stu-id="c358a-126">[Connect PowerShell] to your subscription.</span></span>
3. <span data-ttu-id="c358a-127">Projeyi oluşturmak için aşağıdaki PowerShell cmdlet'ini girin:</span><span class="sxs-lookup"><span data-stu-id="c358a-127">Enter the following PowerShell cmdlet to create to create the project:</span></span>

        New-AzureServiceProject helloworld

    ![New-AzureService helloworld komutunun sonucu][The result of the New-AzureService helloworld command]

    <span data-ttu-id="c358a-129">**New-AzureServiceProject** cmdlet’i bir Node.js uygulamasını Cloud Service’te yayımlamaya yönelik basit bir yapı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c358a-129">The **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application to a Cloud Service.</span></span> <span data-ttu-id="c358a-130">Azure’da yayımlamak için gerekli yapılandırma dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="c358a-130">It contains configuration files necessary for publishing to Azure.</span></span> <span data-ttu-id="c358a-131">Cmdlet ayrıca çalışma dizininizi hizmetin diziniyle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="c358a-131">The cmdlet also changes your working directory to the directory for the service.</span></span>

    <span data-ttu-id="c358a-132">Cmdlet aşağıdaki dosyaları oluşturur:</span><span class="sxs-lookup"><span data-stu-id="c358a-132">The cmdlet creates the following files:</span></span>

   * <span data-ttu-id="c358a-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** ve **ServiceDefinition.csdef**: Uygulamanızı yayımlamak için gereken Azure’a özel dosyalar.</span><span class="sxs-lookup"><span data-stu-id="c358a-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span></span> <span data-ttu-id="c358a-134">Daha fazla bilgi için bkz. [Azure için Barındırılan Hizmet Oluşturmaya Genel Bakış].</span><span class="sxs-lookup"><span data-stu-id="c358a-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
   * <span data-ttu-id="c358a-135">**deploymentSettings.json**: Azure PowerShell dağıtım cmdlet’leri tarafından kullanılan yerel ayarları depolar.</span><span class="sxs-lookup"><span data-stu-id="c358a-135">**deploymentSettings.json**: Stores local settings that are used by the Azure PowerShell deployment cmdlets.</span></span>
4. <span data-ttu-id="c358a-136">Yeni bir web rolü eklemek için aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="c358a-136">Enter the following command to add a new web role:</span></span>

       Add-AzureNodeWebRole

   ![The output of the Add-AzureNodeWebRole command][The output of the Add-AzureNodeWebRole command]

   <span data-ttu-id="c358a-138">**Add-AzureNodeWebRole** cmdlet’i basit bir Node.js uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c358a-138">The **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span></span> <span data-ttu-id="c358a-139">Ayrıca yeni rol için yapılandırma girdileri eklemek üzere **.csfg** ve **.csdef** dosyalarını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="c358a-139">It also modifies the **.csfg** and **.csdef** files to add configuration entries for the new role.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c358a-140">Bir rol adı belirtmezseniz varsayılan ad kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c358a-140">If you do not specify a role name, a default name is used.</span></span> <span data-ttu-id="c358a-141">Birinci cmdlet parametresi olarak bir ad sağlayabilirsiniz: `Add-AzureNodeWebRole MyRole`</span><span class="sxs-lookup"><span data-stu-id="c358a-141">You can provide a name as the first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span></span>

<span data-ttu-id="c358a-142">Node.js uygulaması web rolünün dizininde (varsayılan olarak **WebRole1**) bulunan **server.js** dosyasında tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="c358a-142">The Node.js app is defined in the file **server.js**, located in the directory for the web role (**WebRole1** by default).</span></span> <span data-ttu-id="c358a-143">Kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="c358a-143">Here is the code:</span></span>

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

<span data-ttu-id="c358a-144">Bu kod temelde [nodejs.org] web sitesindeki "Hello World" örneğiyle aynıdır, ancak bulut ortamı tarafından atanan bağlantı noktası numarasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="c358a-144">This code is essentially the same as the "Hello World" sample on the [nodejs.org] website, except it uses the port number assigned by the cloud environment.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="c358a-145">Uygulamayı Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="c358a-145">Deploy the application to Azure</span></span>

> [!NOTE]
> <span data-ttu-id="c358a-146">Bu öğreticiyi tamamlamak için bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c358a-146">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="c358a-147">[MSDN abone avantajınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) ya da [ücretsiz hesap için kaydolabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span><span class="sxs-lookup"><span data-stu-id="c358a-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="download-the-azure-publishing-settings"></a><span data-ttu-id="c358a-148">Azure yayımlama ayarlarını indirme</span><span class="sxs-lookup"><span data-stu-id="c358a-148">Download the Azure publishing settings</span></span>
<span data-ttu-id="c358a-149">Uygulamanızı Azure’a dağıtmak için öncelikle Azure aboneliğinizin yayımlama ayarlarını indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c358a-149">To deploy your application to Azure, you must first download the publishing settings for your Azure subscription.</span></span>

1. <span data-ttu-id="c358a-150">Aşağıdaki Azure PowerShell cmdlet'ini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c358a-150">Run the following Azure PowerShell cmdlet:</span></span>

       Get-AzurePublishSettingsFile

   <span data-ttu-id="c358a-151">Bu işlem, yayımlama ayarları indirme sayfasına gitmek için tarayıcınızı kullanır.</span><span class="sxs-lookup"><span data-stu-id="c358a-151">This will use your browser to navigate to the publish settings download page.</span></span> <span data-ttu-id="c358a-152">Bir Microsoft Hesabı ile oturum açmanız istenebilir.</span><span class="sxs-lookup"><span data-stu-id="c358a-152">You may be prompted to log in with a Microsoft Account.</span></span> <span data-ttu-id="c358a-153">İstenirse Azure aboneliğinizle ilişkili olan hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="c358a-153">If so, use the account associated with your Azure subscription.</span></span>

   <span data-ttu-id="c358a-154">İndirilen profili kolayca erişebileceğiniz bir dosya konumuna kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c358a-154">Save the downloaded profile to a file location you can easily access.</span></span>
2. <span data-ttu-id="c358a-155">İndirdiğiniz yayımlama profilini içeri aktarmak için aşağıdaki cmdlet'i çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c358a-155">Run following cmdlet to import the publishing profile you downloaded:</span></span>

       Import-AzurePublishSettingsFile [path to file]

    > [!NOTE]
    > <span data-ttu-id="c358a-156">Yayımlama ayarlarını indirdikten sonra, başka bir kişinin hesabınıza erişmesine imkan tanıyabilecek bilgiler içerdiğinden indirdiğiniz .publishSettings dosyasını silmeyi düşünün.</span><span class="sxs-lookup"><span data-stu-id="c358a-156">After importing the publish settings, consider deleting the downloaded .publishSettings file, because it contains information that could allow someone to access your account.</span></span>

### <a name="publish-the-application"></a><span data-ttu-id="c358a-157">Uygulamayı yayımlama</span><span class="sxs-lookup"><span data-stu-id="c358a-157">Publish the application</span></span>
<span data-ttu-id="c358a-158">Yayımlamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c358a-158">To publish, run the following commands:</span></span>

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* <span data-ttu-id="c358a-159">**-ServiceName** dağıtımın adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c358a-159">**-ServiceName** specifies the name for the deployment.</span></span> <span data-ttu-id="c358a-160">Bu bir benzersiz ad olmalıdır, aksi takdirde yayımlama işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="c358a-160">This must be a unique name, otherwise the publish process will fail.</span></span> <span data-ttu-id="c358a-161">**Get-Date** komutu, adı benzersiz hale getirmesi gereken bir tarih/saat dizesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="c358a-161">The **Get-Date** command tacks on a date/time string that should make the name unique.</span></span>
* <span data-ttu-id="c358a-162">**-Location**, uygulamanın barındırılacağı veri merkezini belirtir.</span><span class="sxs-lookup"><span data-stu-id="c358a-162">**-Location** specifies the datacenter that the application will be hosted in.</span></span> <span data-ttu-id="c358a-163">Kullanılabilir veri merkezlerinin listesini görmek için **Get-AzureLocation** cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c358a-163">To see a list of available datacenters, use the **Get-AzureLocation** cmdlet.</span></span>
* <span data-ttu-id="c358a-164">**-Launch** bir tarayıcı penceresi açar ve dağıtım tamamlandıktan sonra barındırılan hizmete gider.</span><span class="sxs-lookup"><span data-stu-id="c358a-164">**-Launch** opens a browser window and navigates to the hosted service after deployment has completed.</span></span>

<span data-ttu-id="c358a-165">Yayımlama başarılı olduktan sonra aşağıdakine benzer bir yanıt görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="c358a-165">After publishing succeeds, you will see a response similar to the following:</span></span>

![The output of the Publish-AzureService command][The output of the Publish-AzureService command]

> [!NOTE]
> <span data-ttu-id="c358a-167">Uygulamanın dağıtılması ve ilk kez yayımlandığında kullanılabilir olması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="c358a-167">It can take several minutes for the application to deploy and become available when first published.</span></span>

<span data-ttu-id="c358a-168">Dağıtım tamamlandıktan sonra bir tarayıcı penceresi açın ve bulut hizmetine gidin.</span><span class="sxs-lookup"><span data-stu-id="c358a-168">Once the deployment has completed, a browser window will open and navigate to the cloud service.</span></span>

![Hello world sayfasını gösteren bir tarayıcı penceresi; URL sayfanın Azure’da barındırıldığını gösterir.][A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.]

<span data-ttu-id="c358a-170">Uygulamanız artık Azure üzerinde çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="c358a-170">Your application is now running on Azure.</span></span>

<span data-ttu-id="c358a-171">**Publish-AzureServiceProject** cmdlet’i aşağıdaki adımları uygular:</span><span class="sxs-lookup"><span data-stu-id="c358a-171">The **Publish-AzureServiceProject** cmdlet performs the following steps:</span></span>

1. <span data-ttu-id="c358a-172">Dağıtacağınız bir paket oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c358a-172">Creates a package to deploy.</span></span> <span data-ttu-id="c358a-173">Paket, uygulama klasörünüzdeki tüm dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="c358a-173">The package contains all the files in your application folder.</span></span>
2. <span data-ttu-id="c358a-174">Mevcut değilse yeni bir **depolama hesabı** oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c358a-174">Creates a new **storage account** if one does not exist.</span></span> <span data-ttu-id="c358a-175">Azure depolama hesabı, dağıtım sırasında uygulama paketini depolamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c358a-175">The Azure storage account is used to store the application package during deployment.</span></span> <span data-ttu-id="c358a-176">Dağıtım bittikten sonra depolama hesabını güvenli bir şekilde silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c358a-176">You can safely delete the storage account after deployment is done.</span></span>
3. <span data-ttu-id="c358a-177">Henüz mevcut değilse yeni bir **bulut hizmeti** oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c358a-177">Creates a new **cloud service** if one does not already exist.</span></span> <span data-ttu-id="c358a-178">**Bulut hizmeti** uygulamanızın Azure’a dağıtıldığında barındırıldığı kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="c358a-178">A **cloud service** is the container in which your application is hosted when it is deployed to Azure.</span></span> <span data-ttu-id="c358a-179">Daha fazla bilgi için bkz. [Azure için Barındırılan Hizmet Oluşturmaya Genel Bakış].</span><span class="sxs-lookup"><span data-stu-id="c358a-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
4. <span data-ttu-id="c358a-180">Dağıtım paketini Azure’da yayımlar.</span><span class="sxs-lookup"><span data-stu-id="c358a-180">Publishes the deployment package to Azure.</span></span>

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="c358a-181">Uygulamanızı durdurma ve silme</span><span class="sxs-lookup"><span data-stu-id="c358a-181">Stopping and deleting your application</span></span>
<span data-ttu-id="c358a-182">Uygulamanızı dağıttıktan sonra ek maliyetlerden kaçınmak için devre dışı bırakmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c358a-182">After deploying your application, you may want to disable it so you can avoid extra costs.</span></span> <span data-ttu-id="c358a-183">Azure web rolü örneklerini harcanan sunucu saati başına faturalandırır.</span><span class="sxs-lookup"><span data-stu-id="c358a-183">Azure bills web role instances per hour of server time consumed.</span></span> <span data-ttu-id="c358a-184">Uygulamanız dağıtıldıktan sonra örnekler çalışmadığında ve durdurulmuş halde olduğunda bile sunucu saati harcanır.</span><span class="sxs-lookup"><span data-stu-id="c358a-184">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span></span>

1. <span data-ttu-id="c358a-185">Windows PowerShell penceresinde önceki bölümde oluşturulan hizmet dağıtımını aşağıdaki cmdlet ile durdurun:</span><span class="sxs-lookup"><span data-stu-id="c358a-185">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span></span>

       Stop-AzureService

   <span data-ttu-id="c358a-186">Hizmetin durdurulması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="c358a-186">Stopping the service may take several minutes.</span></span> <span data-ttu-id="c358a-187">Hizmet durdurulduğunda bunu belirten bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="c358a-187">When the service is stopped, you receive a message indicating that it has stopped.</span></span>

   ![The status of the Stop-AzureService command][The status of the Stop-AzureService command]
2. <span data-ttu-id="c358a-189">Hizmeti silmek için aşağıdaki cmdlet'i çağırın:</span><span class="sxs-lookup"><span data-stu-id="c358a-189">To delete the service, call the following cmdlet:</span></span>

       Remove-AzureService

   <span data-ttu-id="c358a-190">İstendiğinde hizmeti silmek için **Y** yazın.</span><span class="sxs-lookup"><span data-stu-id="c358a-190">When prompted, enter **Y** to delete the service.</span></span>

   <span data-ttu-id="c358a-191">Hizmetin silinmesi birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="c358a-191">Deleting the service may take several minutes.</span></span> <span data-ttu-id="c358a-192">Hizmet silindikten sonra bunu belirten bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="c358a-192">After the service has been deleted you receive a message indicating that the service was deleted.</span></span>

   ![The status of the Remove-AzureService command][The status of the Remove-AzureService command]

   > [!NOTE]
   > <span data-ttu-id="c358a-194">Hizmetin silinmesi, hizmet ilk kez yayımlandığında oluşturulan depolama hesabını silmez ve kullanılan depolama alanı için faturalandırılmaya devam edersiniz.</span><span class="sxs-lookup"><span data-stu-id="c358a-194">Deleting the service does not delete the storage account that was created when the service was initially published, and you will continue to be billed for storage used.</span></span> <span data-ttu-id="c358a-195">Depolama alanı başka bir işlem tarafından kullanılmıyorsa silmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c358a-195">If nothing else is using the storage, you may want to delete it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c358a-196">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c358a-196">Next steps</span></span>
<span data-ttu-id="c358a-197">Daha fazla bilgi için bkz. [Node.js Geliştirici Merkezi].</span><span class="sxs-lookup"><span data-stu-id="c358a-197">For more information, see the [Node.js Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="c358a-198">[Azure Websites, Cloud Services ve Virtual Machines karşılaştırması]: ../app-service-web/choose-web-site-cloud-service-vm.md</span><span class="sxs-lookup"><span data-stu-id="c358a-198">[Azure Websites, Cloud Services and Virtual Machines comparison]: ../app-service-web/choose-web-site-cloud-service-vm.md</span></span>
<span data-ttu-id="c358a-199">[basit bir web uygulaması kullanmayı]: ../app-service-web/app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="c358a-199">[using a lightweight web app]: ../app-service-web/app-service-web-get-started-nodejs.md</span></span>
<span data-ttu-id="c358a-200">[Azure PowerShell]: /powershell/azureps-cmdlets-docs</span><span class="sxs-lookup"><span data-stu-id="c358a-200">[Azure Powershell]: /powershell/azureps-cmdlets-docs</span></span>
<span data-ttu-id="c358a-201">[.NET 2.7 için Azure SDK’sını]: http://www.microsoft.com/en-us/download/details.aspx?id=48178</span><span class="sxs-lookup"><span data-stu-id="c358a-201">[Azure SDK for .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178</span></span>
<span data-ttu-id="c358a-202">[PowerShell’i bağlayın]: /powershell/azureps-cmdlets-docs#step-3-connect</span><span class="sxs-lookup"><span data-stu-id="c358a-202">[Connect PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect</span></span>
<span data-ttu-id="c358a-203">[nodejs.org]: http://nodejs.org/</span><span class="sxs-lookup"><span data-stu-id="c358a-203">[nodejs.org]: http://nodejs.org/</span></span>
<span data-ttu-id="c358a-204">[Azure için Barındırılan Hizmet Oluşturmaya Genel Bakış]: https://azure.microsoft.com/documentation/services/cloud-services/</span><span class="sxs-lookup"><span data-stu-id="c358a-204">[Overview of Creating a Hosted Service for Azure]: https://azure.microsoft.com/documentation/services/cloud-services/</span></span>
<span data-ttu-id="c358a-205">[Node.js Geliştirici Merkezi]: https://azure.microsoft.com/develop/nodejs/</span><span class="sxs-lookup"><span data-stu-id="c358a-205">[Node.js Developer Center]: https://azure.microsoft.com/develop/nodejs/</span></span>

<!-- IMG List -->

[The result of the New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[The output of the Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying the Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[The output of the Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[The status of the Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[The status of the Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
