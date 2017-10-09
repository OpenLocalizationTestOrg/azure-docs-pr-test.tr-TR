---
title: "aaaDeploy Azure Service Fabric uygulamayla sürekli tümleştirme (Team Services) | Microsoft Docs"
description: "Bilgi nasıl tooset sürekli tümleştirme ve Visual Studio Team Services kullanarak bir Service Fabric uygulaması için dağıtım.  Bir uygulama tooa Service Fabric kümesi Azure dağıtın."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi
ms.openlocfilehash: ba9a632b247b0f467e7b66fbe77b4ad54fb3d9ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-with-cicd-tooa-service-fabric-cluster"></a><span data-ttu-id="ce41e-104">Bir uygulama CI/CD tooa Service Fabric kümesi oluşturup dağıtın</span><span class="sxs-lookup"><span data-stu-id="ce41e-104">Deploy an application with CI/CD tooa Service Fabric cluster</span></span>
<span data-ttu-id="ce41e-105">Bu öğretici üç bir serinin bir parçasıdır ve açıklar nasıl tooset sürekli tümleştirme ve Visual Studio Team Services kullanarak bir Azure Service Fabric uygulaması için dağıtım.</span><span class="sxs-lookup"><span data-stu-id="ce41e-105">This tutorial is part three of a series and describes how tooset up continuous integration and deployment for an Azure Service Fabric application using Visual Studio Team Services.</span></span>  <span data-ttu-id="ce41e-106">Var olan bir Service Fabric uygulaması gereklidir, hello uygulama oluşturulan [bir .NET uygulaması oluşturma](service-fabric-tutorial-create-dotnet-app.md) bir örnek olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ce41e-106">An existing Service Fabric application is needed, hello application created in [Build a .NET application](service-fabric-tutorial-create-dotnet-app.md) is used as an example.</span></span>

<span data-ttu-id="ce41e-107">Bölümünde hello serisinin üç bilgi nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="ce41e-107">In part three of hello series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ce41e-108">Kaynak denetimi tooyour projesi ekleme</span><span class="sxs-lookup"><span data-stu-id="ce41e-108">Add source control tooyour project</span></span>
> * <span data-ttu-id="ce41e-109">Yapı tanımı Team Services içinde oluşturma</span><span class="sxs-lookup"><span data-stu-id="ce41e-109">Create a build definition in Team Services</span></span>
> * <span data-ttu-id="ce41e-110">Team Services içinde bir yayın tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="ce41e-110">Create a release definition in Team Services</span></span>
> * <span data-ttu-id="ce41e-111">Otomatik olarak dağıtma ve uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="ce41e-111">Automatically deploy and upgrade an application</span></span>

<span data-ttu-id="ce41e-112">Bu öğretici serisinde öğrenin nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="ce41e-112">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * [<span data-ttu-id="ce41e-113">Bir .NET Service Fabric uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ce41e-113">Build a .NET Service Fabric application</span></span>](service-fabric-tutorial-create-dotnet-app.md)
> * [<span data-ttu-id="ce41e-114">Merhaba uygulama tooa uzak kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="ce41e-114">Deploy hello application tooa remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * <span data-ttu-id="ce41e-115">CI/CD Visual Studio Team Services kullanarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ce41e-115">Configure CI/CD using Visual Studio Team Services</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce41e-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ce41e-116">Prerequisites</span></span>
<span data-ttu-id="ce41e-117">Bu öğreticiye başlamadan önce:</span><span class="sxs-lookup"><span data-stu-id="ce41e-117">Before you begin this tutorial:</span></span>
- <span data-ttu-id="ce41e-118">Bir Azure aboneliğiniz yoksa, oluşturma bir [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="ce41e-118">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="ce41e-119">[Visual Studio 2017 yükleme](https://www.visualstudio.com/) hello yükleyip **Azure geliştirme** ve **ASP.NET ve web geliştirme** iş yükleri.</span><span class="sxs-lookup"><span data-stu-id="ce41e-119">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="ce41e-120">Merhaba Service Fabric SDK yükleme</span><span class="sxs-lookup"><span data-stu-id="ce41e-120">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)
- <span data-ttu-id="ce41e-121">Service Fabric uygulaması, örneğin oluşturun [Bu öğreticiyi izleyerek](service-fabric-tutorial-create-dotnet-app.md).</span><span class="sxs-lookup"><span data-stu-id="ce41e-121">Create a Service Fabric application, for example by [following this tutorial](service-fabric-tutorial-create-dotnet-app.md).</span></span> 
- <span data-ttu-id="ce41e-122">Azure üzerinde bir Windows Service Fabric kümesi tarafından örneğin oluşturma [Bu öğreticiyi izleyerek](service-fabric-tutorial-create-cluster-azure-ps.md)</span><span class="sxs-lookup"><span data-stu-id="ce41e-122">Create a Windows Service Fabric cluster on Azure, for example by [following this tutorial](service-fabric-tutorial-create-cluster-azure-ps.md)</span></span>
- <span data-ttu-id="ce41e-123">Oluşturma bir [Team Services hesabı](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).</span><span class="sxs-lookup"><span data-stu-id="ce41e-123">Create a [Team Services account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).</span></span>

## <a name="download-hello-voting-sample-application"></a><span data-ttu-id="ce41e-124">Merhaba oylama örnek uygulamayı indirin</span><span class="sxs-lookup"><span data-stu-id="ce41e-124">Download hello Voting sample application</span></span>
<span data-ttu-id="ce41e-125">Merhaba oylama örnek uygulaması oluşturacağınız değil, [Bu öğretici seri birini Kısım](service-fabric-tutorial-create-dotnet-app.md), yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce41e-125">If you did not build hello Voting sample application in [part one of this tutorial series](service-fabric-tutorial-create-dotnet-app.md), you can download it.</span></span> <span data-ttu-id="ce41e-126">Bir komut penceresinde komut tooclone hello örnek uygulama havuzu tooyour yerel makine aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ce41e-126">In a command window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="prepare-a-publish-profile"></a><span data-ttu-id="ce41e-127">Bir yayımlama profili hazırlama</span><span class="sxs-lookup"><span data-stu-id="ce41e-127">Prepare a publish profile</span></span>
<span data-ttu-id="ce41e-128">Artık [bir uygulama oluşturulan](service-fabric-tutorial-create-dotnet-app.md) ve [hello uygulama tooAzure dağıtılan](service-fabric-tutorial-deploy-app-to-party-cluster.md), sürekli tümleştirme hazır tooset demektir.</span><span class="sxs-lookup"><span data-stu-id="ce41e-128">Now that you've [created an application](service-fabric-tutorial-create-dotnet-app.md) and have [deployed hello application tooAzure](service-fabric-tutorial-deploy-app-to-party-cluster.md), you're ready tooset up continuous integration.</span></span>  <span data-ttu-id="ce41e-129">İlk olarak, bir yayımlama profili kullanmak için uygulama içinde Team Services içinde yürütür hello dağıtım işlemi tarafından hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="ce41e-129">First, prepare a publish profile within your application for use by hello deployment process that executes within Team Services.</span></span>  <span data-ttu-id="ce41e-130">Yayımlama Hello profil daha önceden oluşturduğunuz yapılandırılmış tootarget hello kümesine olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ce41e-130">hello publish profile should be configured tootarget hello cluster that you've previously created.</span></span>  <span data-ttu-id="ce41e-131">Visual Studio'yu başlatın ve var olan bir Service Fabric uygulaması projesini açın.</span><span class="sxs-lookup"><span data-stu-id="ce41e-131">Start Visual Studio and open an existing Service Fabric application project.</span></span>  <span data-ttu-id="ce41e-132">İçinde **Çözüm Gezgini**, hello uygulamayı sağ tıklatın ve seçin **Yayımla...** .</span><span class="sxs-lookup"><span data-stu-id="ce41e-132">In **Solution Explorer**, right-click hello application and select **Publish...**.</span></span>

<span data-ttu-id="ce41e-133">Uygulama projesi toouse sürekli tümleştirme iş akışınız için hedef profilinde seçin, örneğin bulut.</span><span class="sxs-lookup"><span data-stu-id="ce41e-133">Choose a target profile within your application project toouse for your continuous integration workflow, for example Cloud.</span></span>  <span data-ttu-id="ce41e-134">Merhaba küme bağlantı uç noktası belirtin.</span><span class="sxs-lookup"><span data-stu-id="ce41e-134">Specify hello cluster connection endpoint.</span></span>  <span data-ttu-id="ce41e-135">Merhaba denetleyin **yükseltme hello uygulama** onay kutusunu böylece her dağıtımda Team Services için uygulamanızı yükseltir.</span><span class="sxs-lookup"><span data-stu-id="ce41e-135">Check hello **Upgrade hello Application** checkbox so that your application upgrades for each deployment in Team Services.</span></span>  <span data-ttu-id="ce41e-136">Merhaba tıklatın **kaydetmek** köprü toosave hello ayarları toohello yayımlama profili ve ardından **iptal** tooclose hello iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="ce41e-136">Click hello **Save** hyperlink toosave hello settings toohello publish profile and then click **Cancel** tooclose hello dialog box.</span></span>  

![Anında iletme profili][publish-app-profile]

## <a name="share-your-visual-studio-solution-tooa-new-team-services-git-repo"></a><span data-ttu-id="ce41e-138">Visual Studio çözümü tooa Yeni Team Services Git deposuna paylaşma</span><span class="sxs-lookup"><span data-stu-id="ce41e-138">Share your Visual Studio solution tooa new Team Services Git repo</span></span>
<span data-ttu-id="ce41e-139">Takım oluşturabileceğiniz şekilde Hizmetleri tooa takım projesinde derlemeler uygulama Kaynak dosyalarınız paylaşır.</span><span class="sxs-lookup"><span data-stu-id="ce41e-139">Share your application source files tooa team project in Team Services so you can generate builds.</span></span>  

<span data-ttu-id="ce41e-140">Projeniz için yeni bir yerel Git deposu seçerek oluşturun **tooSource denetim eklemek** -> **Git** hello durum çubuğunda hello alt sağ köşesinde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ce41e-140">Create a new local Git repo for your project by selecting **Add tooSource Control** -> **Git** on hello status bar in hello lower right-hand corner of Visual Studio.</span></span> 

<span data-ttu-id="ce41e-141">Merhaba, **anında** görünümünde **Takım Gezgini**seçin hello **yayımlama Git deposuna** altında düğmesini **anında tooVisual Studio Team Services**.</span><span class="sxs-lookup"><span data-stu-id="ce41e-141">In hello **Push** view in **Team Explorer**, select hello **Publish Git Repo** button under **Push tooVisual Studio Team Services**.</span></span>

![Git deposuna Gönder][push-git-repo]

<span data-ttu-id="ce41e-143">Hello hesabınızı seçin ve e-postanızı doğrulayın **Team Services etki alanı** açılır.</span><span class="sxs-lookup"><span data-stu-id="ce41e-143">Verify your email and select your account in hello **Team Services Domain** drop-down.</span></span> <span data-ttu-id="ce41e-144">Depo adınızı girin ve **Yayımla depo**.</span><span class="sxs-lookup"><span data-stu-id="ce41e-144">Enter your repository name and select **Publish repository**.</span></span>

![Git deposuna Gönder][publish-code]

<span data-ttu-id="ce41e-146">Yayımlama Hello depodaki aynı hello yerel deposu ad hello hesabınızla yeni takım projesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ce41e-146">Publishing hello repo creates a new team project in your account with hello same name as hello local repo.</span></span> <span data-ttu-id="ce41e-147">Varolan bir takım projesinde toocreate hello depodaki tıklatın **Gelişmiş** sonraki çok**depo** ad ve bir takım projesini seçin.</span><span class="sxs-lookup"><span data-stu-id="ce41e-147">toocreate hello repo in an existing team project, click **Advanced** next too**Repository** name and select a team project.</span></span> <span data-ttu-id="ce41e-148">Seçerek kodunuzu hello Web'de de görüntüleyebilirsiniz **hello Web'de bakın**.</span><span class="sxs-lookup"><span data-stu-id="ce41e-148">You can view your code on hello web by selecting **See it on hello web**.</span></span>

## <a name="configure-continuous-delivery-with-vsts"></a><span data-ttu-id="ce41e-149">Kesintisiz teslim VSTS ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ce41e-149">Configure Continuous Delivery with VSTS</span></span>
<span data-ttu-id="ce41e-150">Bir Team Services yapı tanımı sırayla yürütülen derleme adımları kümesinden oluşan bir iş akışını açıklar.</span><span class="sxs-lookup"><span data-stu-id="ce41e-150">A Team Services build definition describes a workflow that is composed of a set of build steps that are executed sequentially.</span></span> <span data-ttu-id="ce41e-151">Yapı tanımı üreten bir Service Fabric uygulama paketi ve diğer yapıları, toodeploy tooa Service Fabric kümesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce41e-151">Create a build definition that that produces a Service Fabric application package, and other artifacts, toodeploy tooa Service Fabric cluster.</span></span> <span data-ttu-id="ce41e-152">Daha fazla bilgi edinmek [Team Services yapı tanımları](https://www.visualstudio.com/docs/build/define/create).</span><span class="sxs-lookup"><span data-stu-id="ce41e-152">Learn more about [Team Services build definitions](https://www.visualstudio.com/docs/build/define/create).</span></span> 

<span data-ttu-id="ce41e-153">Bir Team Services sürüm tanımı bir uygulama paketi tooa küme dağıtan bir iş akışını açıklar.</span><span class="sxs-lookup"><span data-stu-id="ce41e-153">A Team Services release definition describes a workflow that deploys an application package tooa cluster.</span></span> <span data-ttu-id="ce41e-154">Birlikte kullanıldığında, hello yapı tanımı ve kaynak dosyaları tooending kümenizde çalışan bir uygulama ile başlayarak hello tüm iş akışı yayın tanımı yürütün.</span><span class="sxs-lookup"><span data-stu-id="ce41e-154">When used together, hello build definition and release definition execute hello entire workflow starting with source files tooending with a running application in your cluster.</span></span> <span data-ttu-id="ce41e-155">Team Services hakkında daha fazla bilgi [yayın tanımları](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition).</span><span class="sxs-lookup"><span data-stu-id="ce41e-155">Learn more about Team Services [release definitions](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition).</span></span>

### <a name="create-a-build-definition"></a><span data-ttu-id="ce41e-156">Yapı tanımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ce41e-156">Create a build definition</span></span>
<span data-ttu-id="ce41e-157">Bir web tarayıcısı açın ve tooyour yeni takım projesi konumunda gidin: https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting.</span><span class="sxs-lookup"><span data-stu-id="ce41e-157">Open a web browser and navigate tooyour new team project at: https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting .</span></span> 

<span data-ttu-id="ce41e-158">Select hello **yapı & yayın** sekmesinde, ardından **derlemeler**, ardından **+ yeni tanımı**.</span><span class="sxs-lookup"><span data-stu-id="ce41e-158">Select hello **Build & Release** tab, then **Builds**, then **+ New definition**.</span></span>  <span data-ttu-id="ce41e-159">İçinde **bir şablon seçin**seçin hello **Azure Service Fabric uygulaması** şablonu ve tıklatın **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="ce41e-159">In **Select a template**, select hello **Azure Service Fabric Application** template and click **Apply**.</span></span> 

![Yapı şablonunu seçin][select-build-template] 

<span data-ttu-id="ce41e-161">.NET Core projesi uygulama oylama hello içerir, böylece hello bağımlılıkları geri yükleyen bir görev ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ce41e-161">hello voting application contains a .NET Core project, so add a task that restores hello dependencies.</span></span> <span data-ttu-id="ce41e-162">Merhaba, **görevleri** görünümü, select **+ görev eklemek** hello sayfanın sol.</span><span class="sxs-lookup"><span data-stu-id="ce41e-162">In hello **Tasks** view, select **+ Add Task** in hello bottom left.</span></span> <span data-ttu-id="ce41e-163">Arama "Komut satırı" toofind hello komut satırı görevi ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ce41e-163">Search on "Command Line" toofind hello command-line task, then click **Add**.</span></span> 

![Görev ekleme][add-task] 

<span data-ttu-id="ce41e-165">Merhaba yeni görevi, "dotnet.exe Çalıştır" girin **görünen adı**, "dotnet.exe" **aracı**ve "geri" **bağımsız değişkenleri**.</span><span class="sxs-lookup"><span data-stu-id="ce41e-165">In hello new task, enter "Run dotnet.exe" in **Display name**, "dotnet.exe" in **Tool**, and "restore" in **Arguments**.</span></span> 

![Yeni görev][new-task] 

<span data-ttu-id="ce41e-167">Merhaba, **Tetikleyicileri** görüntülemek için hello tıklatın **Bu tetikleyici etkinleştirmek** altında geçiş **sürekli tümleştirme**.</span><span class="sxs-lookup"><span data-stu-id="ce41e-167">In hello **Triggers** view, click hello **Enable this trigger** switch under **Continuous Integration**.</span></span> 

<span data-ttu-id="ce41e-168">Seçin **sıraya & Kaydet** ve "Barındırılan VS2017" Merhaba girin **Aracısı sırası**.</span><span class="sxs-lookup"><span data-stu-id="ce41e-168">Select **Save & queue** and enter "Hosted VS2017" as hello **Agent queue**.</span></span> <span data-ttu-id="ce41e-169">Seçin **sıra** toomanually bir yapı başlatın.</span><span class="sxs-lookup"><span data-stu-id="ce41e-169">Select **Queue** toomanually start a build.</span></span>  <span data-ttu-id="ce41e-170">Ayrıca Tetikleyiciler İtme veya iade oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ce41e-170">Builds also triggers upon push or check-in.</span></span>

<span data-ttu-id="ce41e-171">toocheck derleme ilerleme durumunuzu, anahtar toohello **derlemeler** sekmesi.  Merhaba yapı başarılı bir şekilde çalıştığından emin olun, sonra uygulama tooa kümenizi dağıtan bir yayın tanımı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ce41e-171">toocheck your build progress, switch toohello **Builds** tab.  Once you verify that hello build executes successfully, define a release definition that deploys your application tooa cluster.</span></span> 

### <a name="create-a-release-definition"></a><span data-ttu-id="ce41e-172">Bir yayın tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="ce41e-172">Create a release definition</span></span>  

<span data-ttu-id="ce41e-173">Select hello **yapı & yayın** sekmesinde, ardından **sürümleri**, ardından **+ yeni tanımı**.</span><span class="sxs-lookup"><span data-stu-id="ce41e-173">Select hello **Build & Release** tab, then **Releases**, then **+ New definition**.</span></span>  <span data-ttu-id="ce41e-174">İçinde **oluşturma yayın tanımı**seçin hello **Azure Service Fabric dağıtımı** şablonu hello listesi ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ce41e-174">In **Create release definition**, select hello **Azure Service Fabric Deployment** template from hello list and click **Next**.</span></span>  <span data-ttu-id="ce41e-175">Select hello **yapı** kaynak, hello denetleyin **sürekli dağıtım** ve'ı tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="ce41e-175">Select hello **Build** source, check hello **Continuous deployment** box, and click **Create**.</span></span> 

<span data-ttu-id="ce41e-176">Merhaba, **ortamları** görüntülemek için tıklatın **Ekle** sağında toohello **küme bağlantısı**.</span><span class="sxs-lookup"><span data-stu-id="ce41e-176">In hello **Environments** view, click **Add** toohello right of **Cluster Connection**.</span></span>  <span data-ttu-id="ce41e-177">"Mysftestcluster", küme uç noktası hello Azure Active Directory veya sertifika kimlik bilgileri ve "tcp://mysftestcluster.westus.cloudapp.azure.com:19000" Merhaba küme için bir bağlantı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="ce41e-177">Specify a connection name of "mysftestcluster", a cluster endpoint of "tcp://mysftestcluster.westus.cloudapp.azure.com:19000", and hello Azure Active Directory or certificate credentials for hello cluster.</span></span> <span data-ttu-id="ce41e-178">Azure Active Directory kimlik bilgileri için toouse tooconnect toohello hello kümesinde istediğiniz hello bilgilerini tanımlayın **kullanıcıadı** ve **parola** alanları.</span><span class="sxs-lookup"><span data-stu-id="ce41e-178">For Azure Active Directory credentials, define hello credentials you want toouse tooconnect toohello cluster in hello **Username** and **Password** fields.</span></span> <span data-ttu-id="ce41e-179">Sertifika tabanlı kimlik doğrulaması için dosyasının hello istemci sertifikası hello hello Base64 kodlaması tanımlamak **istemci sertifikası** alan.</span><span class="sxs-lookup"><span data-stu-id="ce41e-179">For certificate-based authentication, define hello Base64 encoding of hello client certificate file in hello **Client Certificate** field.</span></span>  <span data-ttu-id="ce41e-180">Merhaba Yardım açılır nasıl ilişkin bilgi için bu alan bakın değer tooget.</span><span class="sxs-lookup"><span data-stu-id="ce41e-180">See hello help pop-up on that field for info on how tooget that value.</span></span>  <span data-ttu-id="ce41e-181">Sertifikanız parola korumalıysa hello parolası hello tanımlamak **parola** alan.</span><span class="sxs-lookup"><span data-stu-id="ce41e-181">If your certificate is password-protected, define hello password in hello **Password** field.</span></span>  <span data-ttu-id="ce41e-182">Tıklatın **kaydetmek** toosave hello yayın tanımı.</span><span class="sxs-lookup"><span data-stu-id="ce41e-182">Click **Save** toosave hello release definition.</span></span>

![Küme Bağlantısı Ekle][add-cluster-connection] 

<span data-ttu-id="ce41e-184">Tıklatın **aracı üzerinde çalıştığı**seçeneğini belirleyip **barındırılan VS2017** için **dağıtım sırası**.</span><span class="sxs-lookup"><span data-stu-id="ce41e-184">Click **Run on agent**, then select **Hosted VS2017** for **Deployment queue**.</span></span> <span data-ttu-id="ce41e-185">Tıklatın **kaydetmek** toosave hello yayın tanımı.</span><span class="sxs-lookup"><span data-stu-id="ce41e-185">Click **Save** toosave hello release definition.</span></span>

![Aracısı'nı çalıştırın][run-on-agent]

<span data-ttu-id="ce41e-187">Seçin **+ yayın** -> **oluşturma yayın** -> **oluşturma** toomanually bir yayın oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ce41e-187">Select **+Release** -> **Create Release** -> **Create** toomanually create a release.</span></span>  <span data-ttu-id="ce41e-188">Merhaba dağıtımı başarılı oldu ve Merhaba uygulaması hello kümede çalışan doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ce41e-188">Verify that hello deployment succeeded and hello application is running in hello cluster.</span></span>  <span data-ttu-id="ce41e-189">Bir web tarayıcısı açın ve çok gidin[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).</span><span class="sxs-lookup"><span data-stu-id="ce41e-189">Open a web browser and navigate too[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).</span></span>  <span data-ttu-id="ce41e-190">Bu örnekte "1.0.0.20170616.3" olan Hello uygulama sürümü unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ce41e-190">Note hello application version, in this example it is "1.0.0.20170616.3".</span></span> 

## <a name="commit-and-push-changes-trigger-a-release"></a><span data-ttu-id="ce41e-191">Yürütme ve değişiklikleri gönderin, sürüm tetikleme</span><span class="sxs-lookup"><span data-stu-id="ce41e-191">Commit and push changes, trigger a release</span></span>
<span data-ttu-id="ce41e-192">Sürekli Tümleştirme ardışık düzen hello tooverify tooTeam Hizmetleri bazı kod değişikliklerini denetleyerek çalışır.</span><span class="sxs-lookup"><span data-stu-id="ce41e-192">tooverify that hello continuous integration pipeline is functioning by checking in some code changes tooTeam Services.</span></span>    

<span data-ttu-id="ce41e-193">Kodunuzu yazarken değişikliklerinizi Visual Studio tarafından otomatik olarak izlenir.</span><span class="sxs-lookup"><span data-stu-id="ce41e-193">As you write your code, your changes are automatically tracked by Visual Studio.</span></span> <span data-ttu-id="ce41e-194">Bekleyen değişiklikleri simgesi (Merhaba seçerek değişiklikleri tooyour yerel Git deposu Yürüt</span><span class="sxs-lookup"><span data-stu-id="ce41e-194">Commit changes tooyour local Git repository by selecting hello pending changes icon (</span></span>![Beklemede][pending]<span data-ttu-id="ce41e-196">) hello durum çubuğunda hello sayfanın sağ.</span><span class="sxs-lookup"><span data-stu-id="ce41e-196">) from hello status bar in hello bottom right.</span></span>

<span data-ttu-id="ce41e-197">Merhaba üzerinde **değişiklikleri** Takım Gezgini'nde görüntüleme, güncelleştirmeyi açıklayan bir ileti ekleyin ve değişikliklerinizi uygulamak.</span><span class="sxs-lookup"><span data-stu-id="ce41e-197">On hello **Changes** view in Team Explorer, add a message describing your update and commit your changes.</span></span>

![Tümünü Yürüt][changes]

<span data-ttu-id="ce41e-199">Select hello yayımdan değişiklikleri durum çubuğu simgesi (![yayımlanmamış değişiklikleri][unpublished-changes]) veya eşitleme Takım Gezgini görünümünde hello.</span><span class="sxs-lookup"><span data-stu-id="ce41e-199">Select hello unpublished changes status bar icon (![Unpublished changes][unpublished-changes]) or hello Sync view in Team Explorer.</span></span> <span data-ttu-id="ce41e-200">Seçin **anında** tooupdate kodunuzu Team Services/TFS.</span><span class="sxs-lookup"><span data-stu-id="ce41e-200">Select **Push** tooupdate your code in Team Services/TFS.</span></span>

![Değişiklikleri gönderme][push]

<span data-ttu-id="ce41e-202">Merhaba değişiklikleri tooTeam Ftp'den Tetikleyicileri otomatik olarak bir yapı hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="ce41e-202">Pushing hello changes tooTeam Services automatically triggers a build.</span></span>  <span data-ttu-id="ce41e-203">Merhaba derleme tanımı başarıyla tamamlandığında, bir yayın otomatik olarak oluşturulur ve Merhaba uygulaması hello kümede yükseltmeyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="ce41e-203">When hello build definition successfully completes, a release is automatically created and starts upgrading hello application on hello cluster.</span></span>

<span data-ttu-id="ce41e-204">toocheck derleme ilerleme durumunuzu, anahtar toohello **derlemeler** sekmesinde **Takım Gezgini** Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ce41e-204">toocheck your build progress, switch toohello **Builds** tab in **Team Explorer** in Visual Studio.</span></span>  <span data-ttu-id="ce41e-205">Merhaba yapı başarılı bir şekilde çalıştığından emin olun, sonra uygulama tooa kümenizi dağıtan bir yayın tanımı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ce41e-205">Once you verify that hello build executes successfully, define a release definition that deploys your application tooa cluster.</span></span>

<span data-ttu-id="ce41e-206">Merhaba dağıtımı başarılı oldu ve Merhaba uygulaması hello kümede çalışan doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ce41e-206">Verify that hello deployment succeeded and hello application is running in hello cluster.</span></span>  <span data-ttu-id="ce41e-207">Bir web tarayıcısı açın ve çok gidin[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).</span><span class="sxs-lookup"><span data-stu-id="ce41e-207">Open a web browser and navigate too[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).</span></span>  <span data-ttu-id="ce41e-208">Bu örnekte "1.0.0.20170815.3" olan Hello uygulama sürümü unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ce41e-208">Note hello application version, in this example it is "1.0.0.20170815.3".</span></span>

![Service Fabric Explorer][sfx1]

## <a name="update-hello-application"></a><span data-ttu-id="ce41e-210">Merhaba uygulamayı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="ce41e-210">Update hello application</span></span>
<span data-ttu-id="ce41e-211">Kod değişikliklerini hello uygulamada yapın.</span><span class="sxs-lookup"><span data-stu-id="ce41e-211">Make code changes in hello application.</span></span>  <span data-ttu-id="ce41e-212">Kaydet ve hello önceki adımları izleyerek hello değişiklikleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="ce41e-212">Save and commit hello changes, following hello previous steps.</span></span>

<span data-ttu-id="ce41e-213">Merhaba yükseltin sonra hello uygulama başlar, Service Fabric Explorer'da hello yükseltme ilerleme durumunu izleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ce41e-213">Once hello upgrade of hello application begins, you can watch hello upgrade progress in Service Fabric Explorer:</span></span>

![Service Fabric Explorer][sfx2]

<span data-ttu-id="ce41e-215">Merhaba uygulama yükseltme birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="ce41e-215">hello application upgrade may take several minutes.</span></span> <span data-ttu-id="ce41e-216">Merhaba yükseltme tamamlandıktan sonra Merhaba uygulaması hello sonraki sürümünü çalıştıran.</span><span class="sxs-lookup"><span data-stu-id="ce41e-216">When hello upgrade is complete, hello application will be running hello next version.</span></span>  <span data-ttu-id="ce41e-217">Bu örnekte "1.0.0.20170815.4".</span><span class="sxs-lookup"><span data-stu-id="ce41e-217">In this example "1.0.0.20170815.4".</span></span>

![Service Fabric Explorer][sfx3]

## <a name="next-steps"></a><span data-ttu-id="ce41e-219">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ce41e-219">Next steps</span></span>
<span data-ttu-id="ce41e-220">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="ce41e-220">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ce41e-221">Kaynak denetimi tooyour projesi ekleme</span><span class="sxs-lookup"><span data-stu-id="ce41e-221">Add source control tooyour project</span></span>
> * <span data-ttu-id="ce41e-222">Yapı tanımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ce41e-222">Create a build definition</span></span>
> * <span data-ttu-id="ce41e-223">Bir yayın tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="ce41e-223">Create a release definition</span></span>
> * <span data-ttu-id="ce41e-224">Otomatik olarak dağıtma ve uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="ce41e-224">Automatically deploy and upgrade an application</span></span>

<span data-ttu-id="ce41e-225">Dağıtılan bir uygulama ve sürekli tümleştirme yapılandırılmış göre hello aşağıdakileri deneyin:</span><span class="sxs-lookup"><span data-stu-id="ce41e-225">Now that you have deployed an application and configured continuous integration, try hello following:</span></span>
- [<span data-ttu-id="ce41e-226">Uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="ce41e-226">Upgrade an app</span></span>](service-fabric-application-upgrade.md)
- [<span data-ttu-id="ce41e-227">Bir uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="ce41e-227">Test an app</span></span>](service-fabric-testability-overview.md) 
- [<span data-ttu-id="ce41e-228">İzleme ve tanılama</span><span class="sxs-lookup"><span data-stu-id="ce41e-228">Monitor and diagnose</span></span>](service-fabric-diagnostics-overview.md)


<!-- Image References -->
[publish-app-profile]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishAppProfile.png
[push-git-repo]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishGitRepo.png
[publish-code]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishCode.png
[select-build-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectBuildTemplate.png
[add-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddTask.png
[new-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewTask.png
[set-continuous-integration]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SetContinuousIntegration.png
[add-cluster-connection]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddClusterConnection.png
[sfx1]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX1.png
[sfx2]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX2.png
[sfx3]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX3.png
[pending]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Pending.png
[changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Changes.png
[unpublished-changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/UnpublishedChanges.png
[push]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Push.png
[continuous-delivery-with-VSTS]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/VSTS-Dialog.png
[new-service-endpoint]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpoint.png
[new-service-endpoint-dialog]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpointDialog.png
[run-on-agent]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/RunOnAgent.png