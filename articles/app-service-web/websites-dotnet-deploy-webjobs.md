---
title: "Visual Studio kullanarak WebJobs dağıtma"
description: "Azure App Service Web Apps'e Visual Studio kullanarak Azure Web işleri dağıtmayı öğrenin."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 5b0808afdadcf4d86a9a2d07ee6fc63b80b22993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="524c4-103">Visual Studio kullanarak WebJobs dağıtma</span><span class="sxs-lookup"><span data-stu-id="524c4-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="524c4-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="524c4-104">Overview</span></span>
<span data-ttu-id="524c4-105">Bu konuda, bir web uygulamasında bir konsol uygulama projesi dağıtmak için Visual Studio kullanımı açıklanmaktadır [uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714) olarak bir [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="524c4-105">This topic explains how to use Visual Studio to deploy a Console Application project to a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="524c4-106">Web işleri kullanarak dağıtma hakkında bilgi için [Azure Portal](https://portal.azure.com), bkz: [Web işleri ile Çalıştır arka plan görevleri](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="524c4-106">For information about how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="524c4-107">Visual Studio Web işleri etkin konsol uygulama projesi dağıtırken, iki görevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="524c4-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="524c4-108">Web uygulamasında uygun klasöre çalışma zamanı dosyalarını kopyalar (*App_Data/işleri/sürekli* sürekli Webjob'lar için *App_Data/işleri/tetiklenen* zamanlanmış ve isteğe bağlı Webjob için).</span><span class="sxs-lookup"><span data-stu-id="524c4-108">Copies runtime files to the appropriate folder in the web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="524c4-109">Ayarlayan [Azure zamanlayıcı işlerinin](#scheduler) belirli zamanlarda çalışmak üzere zamanlanmış Web işleri için.</span><span class="sxs-lookup"><span data-stu-id="524c4-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled to run at particular times.</span></span> <span data-ttu-id="524c4-110">(Bu sürekli Webjob'lar için gerekli değildir.)</span><span class="sxs-lookup"><span data-stu-id="524c4-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="524c4-111">WebJobs kullanan bir proje için eklenen aşağıdaki öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="524c4-111">A WebJobs-enabled project has the following items added to it:</span></span>

* <span data-ttu-id="524c4-112">[Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="524c4-112">The [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="524c4-113">A [webjob yayımlama settings.json](#publishsettings) dağıtım ve Zamanlayıcı ayarlarını içeren dosya.</span><span class="sxs-lookup"><span data-stu-id="524c4-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Bir Web işi olarak dağıtımını etkinleştirmek için bir konsol uygulaması için eklenen gösteren diyagram](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="524c4-115">Bu öğeleri varolan bir konsol uygulaması projesine ekleyin veya yeni bir Web işleri etkin konsol uygulama projesi oluşturmak için bir şablon kullanın.</span><span class="sxs-lookup"><span data-stu-id="524c4-115">You can add these items to an existing Console Application project or use a template to create a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="524c4-116">Bir Web işi tek başına bir proje dağıtma veya böylece web projesini dağıtma olduğunda otomatik olarak dağıtan bir web projesi Bağla.</span><span class="sxs-lookup"><span data-stu-id="524c4-116">You can deploy a project as a WebJob by itself, or link it to a web project so that it automatically deploys whenever you deploy the web project.</span></span> <span data-ttu-id="524c4-117">Visual Studio projeleri bağlamak için Web işleri etkin projesinde adını içeren bir [webjobs list.json](#webjobslist) web projesi dosyasında.</span><span class="sxs-lookup"><span data-stu-id="524c4-117">To link projects, Visual Studio includes the name of the WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in the web project.</span></span>

![Web projesine bağlama Web işi projesinin gösteren diyagram](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="524c4-119">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="524c4-119">Prerequisites</span></span>
<span data-ttu-id="524c4-120">.NET için Azure SDK'yı yüklediğinizde Visual Studio'da Web işleri dağıtım özellikleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="524c4-120">WebJobs deployment features are available in Visual Studio when you install the Azure SDK for .NET:</span></span>

* <span data-ttu-id="524c4-121">[.NET (Visual Studio) için Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="524c4-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="524c4-122"><a id="convert"></a>Mevcut bir konsol uygulama projesi için Web işleri dağıtımı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="524c4-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="524c4-123">İki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="524c4-123">You have two options:</span></span>

* <span data-ttu-id="524c4-124">[Bir web projesi ile otomatik dağıtımı etkinleştirmek](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="524c4-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="524c4-125">Bir web projesi dağıttığınızda, otomatik olarak bir Web işi olarak dağıtan mevcut bir konsol uygulama projesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="524c4-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="524c4-126">İlgili web uygulamasını çalıştıran web uygulamasında, WebJob çalıştırmak istediğinizde bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="524c4-126">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>
* <span data-ttu-id="524c4-127">[Bir web projesi dağıtımıdır etkinleştirmek](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="524c4-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="524c4-128">Bir Web işi tek başına bir web projesi bağlantısı dağıtmak için mevcut bir konsol uygulama projesi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="524c4-128">Configure an existing Console Application project to deploy as a WebJob by itself, with no link to a web project.</span></span> <span data-ttu-id="524c4-129">Bir Web işi, bir web uygulamasında kendisi tarafından web uygulamasında çalışan hiçbir web uygulaması ile çalıştırmak istediğinizde bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="524c4-129">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="524c4-130">Web uygulaması kaynaklarınıza bağımsız olarak, Web işi kaynaklarınızı ölçeklemek için bunun isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="524c4-130">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="524c4-131"><a id="convertlink"></a>Bir web projesi ile otomatik WebJobs dağıtımı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="524c4-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="524c4-132">Web projesine sağ tıklayın **Çözüm Gezgini**ve ardından **Ekle** > **Azure Web işi olarak mevcut proje**.</span><span class="sxs-lookup"><span data-stu-id="524c4-132">Right-click the web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Azure Web işi olarak mevcut proje](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="524c4-134">[Azure Web işine Ekle](#configure) iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="524c4-134">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="524c4-135">İçinde **proje adı** konsol uygulaması proje bir Web işi eklemek için aşağı açılan listesinde seçin.</span><span class="sxs-lookup"><span data-stu-id="524c4-135">In the **Project name** drop-down list, select the Console Application project to add as a WebJob.</span></span>
   
    ![Azure Web işine Ekle iletişim kutusunda proje seçme](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="524c4-137">Tamamlamak [Azure Web işine Ekle](#configure) iletişim ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="524c4-137">Complete the [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="524c4-138"><a id="convertnolink"></a>Bir web projesi olmadan Web işleri dağıtımı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="524c4-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="524c4-139">Konsol uygulaması projesine sağ tıklayın **Çözüm Gezgini**ve ardından **Azure Web işi olarak Yayımla...** .</span><span class="sxs-lookup"><span data-stu-id="524c4-139">Right-click the Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Azure Web işi Yayımla](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="524c4-141">[Azure Web işine Ekle](#configure) iletişim kutusu görüntülenirse, seçili proje ile **proje adı** kutusu.</span><span class="sxs-lookup"><span data-stu-id="524c4-141">The [Add Azure WebJob](#configure) dialog box appears, with the project selected in the **Project name** box.</span></span>
2. <span data-ttu-id="524c4-142">Tamamlamak [Azure Web işine Ekle](#configure) iletişim kutusunu ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="524c4-142">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="524c4-143">**Web'i Yayımla** Sihirbazı görünür.</span><span class="sxs-lookup"><span data-stu-id="524c4-143">The **Publish Web** wizard appears.</span></span>  <span data-ttu-id="524c4-144">Hemen yayımlamak istemiyorsanız sihirbazı kapatın.</span><span class="sxs-lookup"><span data-stu-id="524c4-144">If you do not want to publish immediately, close the wizard.</span></span> <span data-ttu-id="524c4-145">Aşağıdakileri yapmak istediğinizde, girdiğiniz ayarları için kaydedilir [projesini dağıtma](#deploy).</span><span class="sxs-lookup"><span data-stu-id="524c4-145">The settings that you've entered are saved for when you do want to [deploy the project](#deploy).</span></span>

## <span data-ttu-id="524c4-146"><a id="create"></a>Yeni bir Web işleri etkin projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="524c4-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="524c4-147">Web işleri etkin yeni bir proje oluşturmak için konsol uygulaması proje şablonunu kullanın ve Web işleri dağıtım açıklandığı gibi etkinleştirin [önceki bölümde](#convert).</span><span class="sxs-lookup"><span data-stu-id="524c4-147">To create a new WebJobs-enabled project, you can use the Console Application project template and enable WebJobs deployment as explained in [the previous section](#convert).</span></span> <span data-ttu-id="524c4-148">Alternatif olarak, Web işleri yeni proje şablonunu kullanarak şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="524c4-148">As an alternative, you can use the WebJobs new-project template:</span></span>

* [<span data-ttu-id="524c4-149">Bağımsız bir Web işi için Web işleri yeni proje şablonu kullanın</span><span class="sxs-lookup"><span data-stu-id="524c4-149">Use the WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="524c4-150">Proje oluşturma ve tek başına bir web projesi bağlantısı ile bir Web işi olarak dağıtmak için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="524c4-150">Create a project and configure it to deploy by itself as a WebJob, with no link to a web project.</span></span> <span data-ttu-id="524c4-151">Bir Web işi, bir web uygulamasında kendisi tarafından web uygulamasında çalışan hiçbir web uygulaması ile çalıştırmak istediğinizde bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="524c4-151">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="524c4-152">Web uygulaması kaynaklarınıza bağımsız olarak, Web işi kaynaklarınızı ölçeklemek için bunun isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="524c4-152">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="524c4-153">Bir web projesi bağlı bir Web işi için Web işleri yeni proje şablonu kullanın</span><span class="sxs-lookup"><span data-stu-id="524c4-153">Use the WebJobs new-project template for a WebJob linked to a web project</span></span>](#createlink)
  
    <span data-ttu-id="524c4-154">Bir web projesi aynı çözümde dağıtıldığında bir Web işi olarak otomatik olarak dağıtmak için yapılandırılmış bir proje oluşturun.</span><span class="sxs-lookup"><span data-stu-id="524c4-154">Create a project that is configured to deploy automatically as a WebJob when a web project in the same solution is deployed.</span></span> <span data-ttu-id="524c4-155">İlgili web uygulamasını çalıştıran web uygulamasında, WebJob çalıştırmak istediğinizde bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="524c4-155">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="524c4-156">Web işleri yeni proje şablonu otomatik olarak NuGet paketlerini yükler ve kod içerir *Program.cs* için [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span><span class="sxs-lookup"><span data-stu-id="524c4-156">The WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for the [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="524c4-157">WebJobs SDK'yı kullanmak istemiyorsanız, kaldırma veya değiştirme `host.RunAndBlock` deyiminde *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="524c4-157">If you don't want to use the WebJobs SDK, remove or change the `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="524c4-158"><a id="createnolink"></a>Bağımsız bir Web işi için Web işleri yeni proje şablonu kullanın</span><span class="sxs-lookup"><span data-stu-id="524c4-158"><a id="createnolink"></a> Use the WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="524c4-159">Tıklatın **dosya** > **yeni proje**ve ardından **yeni proje** iletişim kutusunda **bulut**  >   **Azure Web işi (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="524c4-159">Click **File** > **New Project**, and then in the **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![Web işi şablon gösteren yeni proje iletişim kutusu](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="524c4-161">Önceki için gösterilen yönergeleri izleyin [bağımsız bir Web işleri proje proje konsol uygulaması olun](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="524c4-161">Follow the directions shown earlier to [make the Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="524c4-162"><a id="createlink"></a>Bir web projesi bağlı bir Web işi için Web işleri yeni proje şablonu kullanın</span><span class="sxs-lookup"><span data-stu-id="524c4-162"><a id="createlink"></a> Use the WebJobs new-project template for a WebJob linked to a web project</span></span>
1. <span data-ttu-id="524c4-163">Web projesine sağ tıklayın **Çözüm Gezgini**ve ardından **Ekle** > **yeni Azure Web işi projesi**.</span><span class="sxs-lookup"><span data-stu-id="524c4-163">Right-click the web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![Yeni Azure Web işi projesinin menü girişi](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="524c4-165">[Azure Web işine Ekle](#configure) iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="524c4-165">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="524c4-166">Tamamlamak [Azure Web işine Ekle](#configure) iletişim kutusunu ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="524c4-166">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="524c4-167"><a id="configure"></a>Azure Web işine Ekle iletişim kutusu</span><span class="sxs-lookup"><span data-stu-id="524c4-167"><a id="configure"></a>The Add Azure WebJob dialog</span></span>
<span data-ttu-id="524c4-168">**Azure Web işine Ekle** iletişim Web işi adı girin ve modu ayarı, Web işi için çalıştırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="524c4-168">The **Add Azure WebJob** dialog lets you enter the WebJob name and run mode setting for your WebJob.</span></span> 

![Azure Web işi iletişim ekleyin](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="524c4-170">Bu iletişim kutusunu alanları üzerindeki alanlarına karşılık gelen **yeni iş** Azure Portal'ın iletişim.</span><span class="sxs-lookup"><span data-stu-id="524c4-170">The fields in this dialog correspond to fields on the **New Job** dialog of the Azure Portal.</span></span> <span data-ttu-id="524c4-171">Daha fazla bilgi için bkz: [Web işleri ile Çalıştır arka plan görevleri](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="524c4-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="524c4-172">Komut satırı dağıtımı hakkında daha fazla bilgi için bkz: [etkinleştirme komut satırı veya Azure Web işleri sürekli teslim](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span><span class="sxs-lookup"><span data-stu-id="524c4-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="524c4-173">Bir Web işi dağıtın ve ardından Web işi ve yeniden dağıtın türünü değiştirmek istediğiniz karar verirseniz, Web işleri yayımlama settings.json dosyayı silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="524c4-173">If you deploy a WebJob and then decide you want to change the type of WebJob and redeploy, you'll need to delete the webjobs-publish-settings.json file.</span></span> <span data-ttu-id="524c4-174">Web işi türünü değiştirebilmeniz için bu Visual Studio yayımlama seçeneklerini gösterme hale getirir.</span><span class="sxs-lookup"><span data-stu-id="524c4-174">This will make Visual Studio show the publishing options again, so you can change the type of WebJob.</span></span>
> * <span data-ttu-id="524c4-175">Bir Web işi dağıtırsanız ve daha sonra çalışma modunda gelen sürekli sürekli olmayan veya tersi değiştirmek Visual Studio, yeniden dağıtırken Azure'da yeni bir Web işi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="524c4-175">If you deploy a WebJob and later change the run mode from continuous to non-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="524c4-176">Diğer zamanlama ayarlarını değiştirmek, ancak bırakın aynı çalıştırma modu veya zamanlanmış ve isteğe bağlı arasında geçiş yapma, Visual Studio güncelleştirmeleri varolan işi yerine yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="524c4-176">If you change other scheduling settings but leave run mode the same or switch between Scheduled and On Demand, Visual Studio updates the existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="524c4-177"><a id="publishsettings"></a>Web işi yayımlama settings.json</span><span class="sxs-lookup"><span data-stu-id="524c4-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="524c4-178">Bir konsol uygulaması Web işleri dağıtımı için yapılandırdığınızda, Visual Studio yükler [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet paketi ve planlama bilgilerini de depolar bir *webjob yayımlama settings.json*  proje dosyasında *özellikleri* WebJobs projesinin klasör.</span><span class="sxs-lookup"><span data-stu-id="524c4-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs the [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in the project *Properties* folder of the WebJobs project.</span></span> <span data-ttu-id="524c4-179">Bu dosyayı bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="524c4-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="524c4-180">Visual Studio IntelliSense sağlar ve bu dosyayı doğrudan düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="524c4-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="524c4-181">Dosya şeması konumunda depolanan [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) ve orada görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="524c4-181">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="524c4-182"><a id="webjobslist"></a>Web işleri list.json</span><span class="sxs-lookup"><span data-stu-id="524c4-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="524c4-183">WebJobs kullanan bir proje bir web projesi bağladığınızda, Visual Studio Web işleri projesinde adını depolar bir *webjobs list.json* web projesinin dosyasında *özellikleri* klasör.</span><span class="sxs-lookup"><span data-stu-id="524c4-183">When you link a WebJobs-enabled project to a web project, Visual Studio stores the name of the WebJobs project in a *webjobs-list.json* file in the web project's *Properties* folder.</span></span> <span data-ttu-id="524c4-184">Liste, aşağıdaki örnekte gösterildiği gibi birden çok Web işleri projeleri içerebilir:</span><span class="sxs-lookup"><span data-stu-id="524c4-184">The list might contain multiple WebJobs projects, as shown in the following example:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

<span data-ttu-id="524c4-185">Visual Studio IntelliSense sağlar ve bu dosyayı doğrudan düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="524c4-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="524c4-186">Dosya şeması konumunda depolanan [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) ve orada görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="524c4-186">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="524c4-187"><a id="deploy"></a>Web işleri projesini dağıtma</span><span class="sxs-lookup"><span data-stu-id="524c4-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="524c4-188">Bir web projesi bağlı bir Web işleri proje ile web projesi otomatik olarak dağıtır.</span><span class="sxs-lookup"><span data-stu-id="524c4-188">A WebJobs project that you have linked to a web project deploys automatically with the web project.</span></span> <span data-ttu-id="524c4-189">Web projesi dağıtımı hakkında daha fazla bilgi için bkz: [Web uygulamalarını dağıtmak nasıl](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="524c4-189">For information about web project deployment, see [How to deploy to Web Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="524c4-190">Tek başına bir Web işleri projeyi dağıtmak için projeye sağ **Çözüm Gezgini** tıklatıp **Azure Web işi olarak Yayımla...** .</span><span class="sxs-lookup"><span data-stu-id="524c4-190">To deploy a WebJobs project by itself, right-click the project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Azure Web işi Yayımla](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="524c4-192">Bir bağımsız Web işi için aynı **Web'i Yayımla** web projeleri görünür, ancak daha az ayarları değiştirmek kullanılabilir olan kullanılan Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="524c4-192">For an independent WebJob, the same **Publish Web** wizard that is used for web projects appears, but with fewer settings available to change.</span></span>

## <span data-ttu-id="524c4-193"><a id="nextsteps"></a>Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="524c4-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="524c4-194">Bu makalede, Visual Studio kullanarak Web işleri dağıtma açıklandığı.</span><span class="sxs-lookup"><span data-stu-id="524c4-194">This article has explained how to deploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="524c4-195">Azure Web işleri dağıtma hakkında daha fazla bilgi için bkz: [Azure Web işleri - önerilen kaynaklar - dağıtım](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span><span class="sxs-lookup"><span data-stu-id="524c4-195">For more information about how to deploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

