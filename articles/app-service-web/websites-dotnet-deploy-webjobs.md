---
title: "aaaDeploy Visual Studio'yu kullanarak Web işleri"
description: "Bilgi nasıl toodeploy Azure Web işleri tooAzure App Service Web Apps Visual Studio kullanarak."
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
ms.openlocfilehash: 5fc5d9562e8836348f5ab6844fb6c23ff40a321c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="ccc70-103">Visual Studio kullanarak WebJobs dağıtma</span><span class="sxs-lookup"><span data-stu-id="ccc70-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="ccc70-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ccc70-104">Overview</span></span>
<span data-ttu-id="ccc70-105">Bu konuda, nasıl toouse Visual Studio toodeploy bir konsol uygulaması proje tooa web uygulamasında açıklanmaktadır [uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714) olarak bir [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="ccc70-105">This topic explains how toouse Visual Studio toodeploy a Console Application project tooa web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="ccc70-106">Nasıl kullanarak Web işleri toodeploy hello hakkında bilgi için [Azure Portal](https://portal.azure.com), bkz: [Web işleri ile Çalıştır arka plan görevleri](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="ccc70-106">For information about how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="ccc70-107">Visual Studio Web işleri etkin konsol uygulama projesi dağıtırken, iki görevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="ccc70-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="ccc70-108">Kopya çalışma zamanı toohello uygun hello web uygulaması klasördeki dosyaları (*App_Data/işleri/sürekli* sürekli Webjob'lar için *App_Data/işleri/tetiklenen* zamanlanmış ve isteğe bağlı Webjob için).</span><span class="sxs-lookup"><span data-stu-id="ccc70-108">Copies runtime files toohello appropriate folder in hello web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="ccc70-109">Ayarlayan [Azure zamanlayıcı işlerinin](#scheduler) belirli zamanlarda zamanlanmış toorun olan Web işleri için.</span><span class="sxs-lookup"><span data-stu-id="ccc70-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled toorun at particular times.</span></span> <span data-ttu-id="ccc70-110">(Bu sürekli Webjob'lar için gerekli değildir.)</span><span class="sxs-lookup"><span data-stu-id="ccc70-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="ccc70-111">WebJobs kullanan bir proje öğeleri eklenen tooit aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="ccc70-111">A WebJobs-enabled project has hello following items added tooit:</span></span>

* <span data-ttu-id="ccc70-112">Merhaba [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="ccc70-112">hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="ccc70-113">A [webjob yayımlama settings.json](#publishsettings) dağıtım ve Zamanlayıcı ayarlarını içeren dosya.</span><span class="sxs-lookup"><span data-stu-id="ccc70-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Bir Web işi ne tooa konsol uygulaması tooenable dağıtım eklenir gösteren diyagram](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="ccc70-115">Konsol uygulama projesi varolan bu öğeleri tooan ekleyin veya bir şablon toocreate yeni bir Web işleri etkin konsol uygulama projesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="ccc70-115">You can add these items tooan existing Console Application project or use a template toocreate a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="ccc70-116">Bir proje bir Web işi kendisi tarafından dağıtabilir veya hello web projesi dağıtma olduğunda otomatik olarak dağıtan şekilde tooa web projesi bağlayın.</span><span class="sxs-lookup"><span data-stu-id="ccc70-116">You can deploy a project as a WebJob by itself, or link it tooa web project so that it automatically deploys whenever you deploy hello web project.</span></span> <span data-ttu-id="ccc70-117">toolink projeleri, Visual Studio içerir hello WebJobs etkin projesinde hello adını bir [webjobs list.json](#webjobslist) hello web projesi dosyasında.</span><span class="sxs-lookup"><span data-stu-id="ccc70-117">toolink projects, Visual Studio includes hello name of hello WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in hello web project.</span></span>

![Web işi projesinin tooweb projesi bağlanıyor gösteren diyagram](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="ccc70-119">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ccc70-119">Prerequisites</span></span>
<span data-ttu-id="ccc70-120">.NET için Azure SDK'sı hello yüklediğinizde, Web işleri dağıtım özelliklerini Visual Studio'da kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="ccc70-120">WebJobs deployment features are available in Visual Studio when you install hello Azure SDK for .NET:</span></span>

* <span data-ttu-id="ccc70-121">[.NET (Visual Studio) için Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ccc70-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="ccc70-122"><a id="convert"></a>Mevcut bir konsol uygulama projesi için Web işleri dağıtımı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ccc70-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="ccc70-123">İki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="ccc70-123">You have two options:</span></span>

* <span data-ttu-id="ccc70-124">[Bir web projesi ile otomatik dağıtımı etkinleştirmek](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="ccc70-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="ccc70-125">Bir web projesi dağıttığınızda, otomatik olarak bir Web işi olarak dağıtan mevcut bir konsol uygulama projesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ccc70-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="ccc70-126">Merhaba, Webjob'da toorun istediğinizde bu seçeneği kullanın hello çalıştırmak aynı web uygulaması ile ilgili web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="ccc70-126">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>
* <span data-ttu-id="ccc70-127">[Bir web projesi dağıtımıdır etkinleştirmek](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="ccc70-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="ccc70-128">Mevcut bir konsol uygulama projesi toodeploy bir Web işi kendisi tarafından hiçbir bağlantı tooa web projesi ile yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ccc70-128">Configure an existing Console Application project toodeploy as a WebJob by itself, with no link tooa web project.</span></span> <span data-ttu-id="ccc70-129">Bir web uygulamasında bir Webjob'un toorun kendisi tarafından hello web uygulamasında çalışan hiçbir web uygulaması ile istediğinizde bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="ccc70-129">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="ccc70-130">Bu toodo isteyebilirsiniz, web uygulaması kaynaklarınıza bağımsız olarak, Web işi kaynaklarınızı toobe mümkün tooscale sipariş.</span><span class="sxs-lookup"><span data-stu-id="ccc70-130">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="ccc70-131"><a id="convertlink"></a>Bir web projesi ile otomatik WebJobs dağıtımı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ccc70-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="ccc70-132">Sağ hello web projesinde **Çözüm Gezgini**ve ardından **Ekle** > **Azure Web işi olarak mevcut proje**.</span><span class="sxs-lookup"><span data-stu-id="ccc70-132">Right-click hello web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Azure Web işi olarak mevcut proje](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="ccc70-134">Merhaba [Azure Web işine Ekle](#configure) iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ccc70-134">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="ccc70-135">Merhaba, **proje adı** aşağı açılan listesinden, select hello konsol uygulama projesi tooadd bir Web işi olarak.</span><span class="sxs-lookup"><span data-stu-id="ccc70-135">In hello **Project name** drop-down list, select hello Console Application project tooadd as a WebJob.</span></span>
   
    ![Azure Web işine Ekle iletişim kutusunda proje seçme](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="ccc70-137">Tam hello [Azure Web işine Ekle](#configure) iletişim ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ccc70-137">Complete hello [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="ccc70-138"><a id="convertnolink"></a>Bir web projesi olmadan Web işleri dağıtımı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ccc70-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="ccc70-139">Sağ hello konsol uygulama projesi **Çözüm Gezgini**ve ardından **Azure Web işi olarak Yayımla...** .</span><span class="sxs-lookup"><span data-stu-id="ccc70-139">Right-click hello Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Azure Web işi Yayımla](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="ccc70-141">Merhaba [Azure Web işine Ekle](#configure) hello seçili hello proje ile iletişim kutusu görünür **proje adı** kutusu.</span><span class="sxs-lookup"><span data-stu-id="ccc70-141">hello [Add Azure WebJob](#configure) dialog box appears, with hello project selected in hello **Project name** box.</span></span>
2. <span data-ttu-id="ccc70-142">Tam hello [Azure Web işine Ekle](#configure) iletişim kutusunu ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ccc70-142">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="ccc70-143">Merhaba **Web'i Yayımla** Sihirbazı görünür.</span><span class="sxs-lookup"><span data-stu-id="ccc70-143">hello **Publish Web** wizard appears.</span></span>  <span data-ttu-id="ccc70-144">Toopublish hemen istemiyorsanız hello sihirbazı kapatın.</span><span class="sxs-lookup"><span data-stu-id="ccc70-144">If you do not want toopublish immediately, close hello wizard.</span></span> <span data-ttu-id="ccc70-145">girmiş olduğunuz hello ayarları kaydedilir için çok istediğinizde,[hello projesini dağıtma](#deploy).</span><span class="sxs-lookup"><span data-stu-id="ccc70-145">hello settings that you've entered are saved for when you do want too[deploy hello project](#deploy).</span></span>

## <span data-ttu-id="ccc70-146"><a id="create"></a>Yeni bir Web işleri etkin projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ccc70-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="ccc70-147">Yeni bir Web işleri etkin proje toocreate, hello konsol uygulaması proje şablonu ve etkinleştir WebJobs dağıtım kullanabilirsiniz açıklandığı gibi [hello önceki bölümde](#convert).</span><span class="sxs-lookup"><span data-stu-id="ccc70-147">toocreate a new WebJobs-enabled project, you can use hello Console Application project template and enable WebJobs deployment as explained in [hello previous section](#convert).</span></span> <span data-ttu-id="ccc70-148">Alternatif olarak, hello WebJobs yeni proje şablonunu kullanarak şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ccc70-148">As an alternative, you can use hello WebJobs new-project template:</span></span>

* [<span data-ttu-id="ccc70-149">Bağımsız bir Web işi için Hello WebJobs yeni proje şablonu kullanın</span><span class="sxs-lookup"><span data-stu-id="ccc70-149">Use hello WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="ccc70-150">Proje oluşturma ve toodeploy kendi başına hiçbir bağlantı tooa web projesi ile bir Web işi olarak yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ccc70-150">Create a project and configure it toodeploy by itself as a WebJob, with no link tooa web project.</span></span> <span data-ttu-id="ccc70-151">Bir web uygulamasında bir Webjob'un toorun kendisi tarafından hello web uygulamasında çalışan hiçbir web uygulaması ile istediğinizde bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="ccc70-151">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="ccc70-152">Bu toodo isteyebilirsiniz, web uygulaması kaynaklarınıza bağımsız olarak, Web işi kaynaklarınızı toobe mümkün tooscale sipariş.</span><span class="sxs-lookup"><span data-stu-id="ccc70-152">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="ccc70-153">Bir Web işi bağlantılı tooa web projesi için Hello WebJobs yeni proje şablonu kullanın</span><span class="sxs-lookup"><span data-stu-id="ccc70-153">Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>](#createlink)
  
    <span data-ttu-id="ccc70-154">Bir web projesi yokken aynı çözüm dağıtılan hello bir Web işi olarak otomatik olarak yapılandırılan toodeploy bir proje oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ccc70-154">Create a project that is configured toodeploy automatically as a WebJob when a web project in hello same solution is deployed.</span></span> <span data-ttu-id="ccc70-155">Merhaba, Webjob'da toorun istediğinizde bu seçeneği kullanın hello çalıştırmak aynı web uygulaması ile ilgili web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="ccc70-155">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="ccc70-156">Merhaba WebJobs yeni proje şablonu otomatik olarak NuGet paketlerini yükler ve kod içerir *Program.cs* hello için [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span><span class="sxs-lookup"><span data-stu-id="ccc70-156">hello WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for hello [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="ccc70-157">Toouse hello Web işleri SDK'si istemiyorsanız, kaldırmak veya hello değiştirme `host.RunAndBlock` deyiminde *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="ccc70-157">If you don't want toouse hello WebJobs SDK, remove or change hello `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="ccc70-158"><a id="createnolink"></a>Bağımsız bir Web işi için Hello WebJobs yeni proje şablonu kullanın</span><span class="sxs-lookup"><span data-stu-id="ccc70-158"><a id="createnolink"></a> Use hello WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="ccc70-159">Tıklatın **dosya** > **yeni proje**ve ardından hello **yeni proje** iletişim kutusunda **bulut**  >   **Azure Web işi (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="ccc70-159">Click **File** > **New Project**, and then in hello **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![Web işi şablon gösteren yeni proje iletişim kutusu](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="ccc70-161">Daha önce gösterilen hello yönergeleri izleyerek çok[konsol uygulama projesi bağımsız bir Web işleri proje hello olun](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="ccc70-161">Follow hello directions shown earlier too[make hello Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="ccc70-162"><a id="createlink"></a>Bir Web işi bağlantılı tooa web projesi için Hello WebJobs yeni proje şablonu kullanın</span><span class="sxs-lookup"><span data-stu-id="ccc70-162"><a id="createlink"></a> Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>
1. <span data-ttu-id="ccc70-163">Sağ hello web projesinde **Çözüm Gezgini**ve ardından **Ekle** > **yeni Azure Web işi projesi**.</span><span class="sxs-lookup"><span data-stu-id="ccc70-163">Right-click hello web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![Yeni Azure Web işi projesinin menü girişi](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="ccc70-165">Merhaba [Azure Web işine Ekle](#configure) iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ccc70-165">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="ccc70-166">Tam hello [Azure Web işine Ekle](#configure) iletişim kutusunu ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ccc70-166">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="ccc70-167"><a id="configure"></a>Hello Azure Web işine Ekle iletişim kutusu</span><span class="sxs-lookup"><span data-stu-id="ccc70-167"><a id="configure"></a>hello Add Azure WebJob dialog</span></span>
<span data-ttu-id="ccc70-168">Merhaba **Azure Web işine Ekle** iletişim hello Web işi adı girin ve modu ayarı, Web işi için çalıştırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ccc70-168">hello **Add Azure WebJob** dialog lets you enter hello WebJob name and run mode setting for your WebJob.</span></span> 

![Azure Web işi iletişim ekleyin](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="ccc70-170">Bu iletişim kutusunu Hello alanları karşılık toofields hello üzerinde **yeni iş** hello Azure Portal ile görüşün.</span><span class="sxs-lookup"><span data-stu-id="ccc70-170">hello fields in this dialog correspond toofields on hello **New Job** dialog of hello Azure Portal.</span></span> <span data-ttu-id="ccc70-171">Daha fazla bilgi için bkz: [Web işleri ile Çalıştır arka plan görevleri](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="ccc70-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="ccc70-172">Komut satırı dağıtımı hakkında daha fazla bilgi için bkz: [etkinleştirme komut satırı veya Azure Web işleri sürekli teslim](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span><span class="sxs-lookup"><span data-stu-id="ccc70-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="ccc70-173">Bir Web işi dağıtırsanız ve toochange hello türüne WebJob dağıtın ve istediğiniz karar toodelete hello Web işleri yayımlama settings.json dosyası gerekir.</span><span class="sxs-lookup"><span data-stu-id="ccc70-173">If you deploy a WebJob and then decide you want toochange hello type of WebJob and redeploy, you'll need toodelete hello webjobs-publish-settings.json file.</span></span> <span data-ttu-id="ccc70-174">Bu, Visual Studio Web işi hello türünü değiştirebilmeniz için seçenekleri yeniden yayımlama hello Göster hale getirir.</span><span class="sxs-lookup"><span data-stu-id="ccc70-174">This will make Visual Studio show hello publishing options again, so you can change hello type of WebJob.</span></span>
> * <span data-ttu-id="ccc70-175">Bir Web işi dağıtmak ve daha sonra değiştirirseniz çalıştırma modundan sürekli toonon sürekli hello veya, yeniden dağıtırken Visual Studio Azure içinde yeni bir Web işi tersi yönde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ccc70-175">If you deploy a WebJob and later change hello run mode from continuous toonon-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="ccc70-176">Diğer zamanlama ayarlarını değiştirmek, ancak bırakın çalıştırma modu aynı hello veya zamanlanmış ve isteğe bağlı arasında geçiş yapma, Visual Studio güncelleştirmeleri mevcut iş hello yerine yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ccc70-176">If you change other scheduling settings but leave run mode hello same or switch between Scheduled and On Demand, Visual Studio updates hello existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="ccc70-177"><a id="publishsettings"></a>Web işi yayımlama settings.json</span><span class="sxs-lookup"><span data-stu-id="ccc70-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="ccc70-178">Bir konsol uygulaması Web işleri dağıtımı için yapılandırdığınızda, Visual Studio hello yükler [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet paketi ve planlama bilgilerini de depolar bir *webjob yayımlama settings.json*  hello proje dosyasında *özellikleri* hello WebJobs projesinin klasör.</span><span class="sxs-lookup"><span data-stu-id="ccc70-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in hello project *Properties* folder of hello WebJobs project.</span></span> <span data-ttu-id="ccc70-179">Bu dosyayı bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ccc70-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="ccc70-180">Visual Studio IntelliSense sağlar ve bu dosyayı doğrudan düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccc70-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="ccc70-181">Merhaba dosya şeması depolandı [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) ve orada görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="ccc70-181">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="ccc70-182"><a id="webjobslist"></a>Web işleri list.json</span><span class="sxs-lookup"><span data-stu-id="ccc70-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="ccc70-183">WebJobs kullanan proje tooa web projesi bağladığınızda, Visual Studio hello WebJobs projesinde hello adını depolar bir *webjobs list.json* hello web projesinin dosyasında *özellikleri* klasör.</span><span class="sxs-lookup"><span data-stu-id="ccc70-183">When you link a WebJobs-enabled project tooa web project, Visual Studio stores hello name of hello WebJobs project in a *webjobs-list.json* file in hello web project's *Properties* folder.</span></span> <span data-ttu-id="ccc70-184">Merhaba listesi hello aşağıdaki örnekte gösterildiği gibi birden çok Web işleri projeleri içerebilir:</span><span class="sxs-lookup"><span data-stu-id="ccc70-184">hello list might contain multiple WebJobs projects, as shown in hello following example:</span></span>

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

<span data-ttu-id="ccc70-185">Visual Studio IntelliSense sağlar ve bu dosyayı doğrudan düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccc70-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="ccc70-186">Merhaba dosya şeması depolandı [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) ve orada görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="ccc70-186">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="ccc70-187"><a id="deploy"></a>Web işleri projesini dağıtma</span><span class="sxs-lookup"><span data-stu-id="ccc70-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="ccc70-188">Tooa web projesi bağlantılı Web işleri proje hello web projesi ile otomatik olarak dağıtır.</span><span class="sxs-lookup"><span data-stu-id="ccc70-188">A WebJobs project that you have linked tooa web project deploys automatically with hello web project.</span></span> <span data-ttu-id="ccc70-189">Web projesi dağıtımı hakkında daha fazla bilgi için bkz: [nasıl toodeploy tooWeb uygulamaları](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ccc70-189">For information about web project deployment, see [How toodeploy tooWeb Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="ccc70-190">toodeploy WebJobs proje kendisi tarafından sağ hello projesinde **Çözüm Gezgini** tıklatıp **Azure Web işi olarak Yayımla...** .</span><span class="sxs-lookup"><span data-stu-id="ccc70-190">toodeploy a WebJobs project by itself, right-click hello project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Azure Web işi Yayımla](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="ccc70-192">Bağımsız bir Web işi için aynı hello **Web'i Yayımla** web projeleri görünür, ancak daha az ayarları kullanılabilir toochange ile kullanılan Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="ccc70-192">For an independent WebJob, hello same **Publish Web** wizard that is used for web projects appears, but with fewer settings available toochange.</span></span>

## <span data-ttu-id="ccc70-193"><a id="nextsteps"></a>Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="ccc70-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="ccc70-194">Bu makalede açıklanan nasıl Visual Studio'yu kullanarak Web işleri toodeploy.</span><span class="sxs-lookup"><span data-stu-id="ccc70-194">This article has explained how toodeploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="ccc70-195">Azure Web işleri toodeploy nasıl görürüm hakkında daha fazla bilgi için [Azure Web işleri - önerilen kaynaklar - dağıtım](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span><span class="sxs-lookup"><span data-stu-id="ccc70-195">For more information about how toodeploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

