---
title: Git ve Azure Visual Studio Team Services ile aaaContinuous teslim | Microsoft Docs
description: "Nasıl tooconfigure toouse Git tooautomatically ve toohello Web uygulamasını Azure App Service veya Bulut hizmetlerini özelliğinde dağıtacak projeleri, Visual Studio Team Services ekip öğrenin."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="5832c-103">Visual Studio Team Services ve Git kullanarak sürekli teslim tooAzure</span><span class="sxs-lookup"><span data-stu-id="5832c-103">Continuous delivery tooAzure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="5832c-104">Visual Studio Team Services ekip projeleri toohost bir Git deposu kaynak kodunuz için kullanabilir ve otomatik olarak oluşturun ve tooAzure web uygulamaları dağıtma veya bir yürütme toohello deposu itme her bulut Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="5832c-104">You can use Visual Studio Team Services team projects toohost a Git repository for your source code, and automatically build and deploy tooAzure web apps or cloud services whenever you push a commit toohello repository.</span></span>

<span data-ttu-id="5832c-105">Visual Studio 2013 ve Azure SDK'sını hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="5832c-105">You'll need Visual Studio 2013 and hello Azure SDK installed.</span></span> <span data-ttu-id="5832c-106">Visual Studio 2013 zaten yoksa, hello seçerek karşıdan **ücretsiz olarak başlayın** adresindeki bağlantı [www.visualstudio.com](http://www.visualstudio.com). Yükleme hello Azure SDK [burada](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="5832c-106">If you don't already have Visual Studio 2013, download it by choosing hello **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com). Install hello Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="5832c-107">Bu öğretici bir Visual Studio Team Services hesabı toocomplete gerekir: yapabilecekleriniz [ücretsiz bir Visual Studio Team Services hesabı açabilirsiniz](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="5832c-107">You need an Visual Studio Team Services account toocomplete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="5832c-108">bir bulut hizmeti tooautomatically yukarı tooset derleme ve Visual Studio Team Services kullanarak tooAzure dağıtma, şu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="5832c-108">tooset up a cloud service tooautomatically build and deploy tooAzure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="5832c-109">1: bir Git deposu oluşturma</span><span class="sxs-lookup"><span data-stu-id="5832c-109">1: Create a Git repository</span></span>
1. <span data-ttu-id="5832c-110">Visual Studio Team Services hesabı zaten yoksa, edinebilirsiniz [burada](http://go.microsoft.com/fwlink/?LinkId=397665).</span><span class="sxs-lookup"><span data-stu-id="5832c-110">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="5832c-111">Takım projesi oluşturduğunuzda, Git kaynak denetim sisteminiz seçin.</span><span class="sxs-lookup"><span data-stu-id="5832c-111">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="5832c-112">Merhaba yönergeleri tooconnect Visual Studio tooyour takım projesi izleyin.</span><span class="sxs-lookup"><span data-stu-id="5832c-112">Follow hello instructions tooconnect Visual Studio tooyour team project.</span></span>
2. <span data-ttu-id="5832c-113">İçinde **Takım Gezgini**, hello seçin **bu depoyu kopyalayın** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="5832c-113">In **Team Explorer**, choose hello **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="5832c-114">Merhaba yerel kopyasını Hello konumunu belirtin ve ardından hello **kopya** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5832c-114">Specify hello location of hello local copy and then choose hello **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a><span data-ttu-id="5832c-115">2: Proje oluşturma ve toohello depo yürütme</span><span class="sxs-lookup"><span data-stu-id="5832c-115">2: Create a project and commit it toohello repository</span></span>
1. <span data-ttu-id="5832c-116">İçinde **Takım Gezgini**, hello içinde **çözümleri** bölümünde, hello seçin **yeni** toocreate yeni bir proje hello yerel deposu ile bağlantı.</span><span class="sxs-lookup"><span data-stu-id="5832c-116">In **Team Explorer**, in hello **Solutions** section, choose hello **New** link toocreate a new project in hello local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="5832c-117">Bir web uygulaması dağıtma veya Bulut hizmeti (Azure uygulaması) aşağıdaki hello tarafından bu izlenecek adımları.</span><span class="sxs-lookup"><span data-stu-id="5832c-117">You can deploy a web app or a cloud service (Azure Application) by following hello steps in this walkthrough.</span></span> <span data-ttu-id="5832c-118">Yeni bir Azure bulut hizmeti projesi ya da yeni bir ASP.NET MVC projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5832c-118">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="5832c-119">Sonraki veya hello Proje hedefleri .NET Framework 4 hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="5832c-119">Make sure that hello project targets hello .NET Framework 4 or later.</span></span> <span data-ttu-id="5832c-120">Bir bulut hizmeti projesini oluşturuyorsanız, bir ASP.NET MVC web rolü ve çalışan rolü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5832c-120">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="5832c-121">Bir web uygulaması toocreate istiyorsanız, hello tercih **ASP.NET Web uygulaması** proje şablonu ve ardından **MVC**.</span><span class="sxs-lookup"><span data-stu-id="5832c-121">If you want toocreate a web app, choose hello **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="5832c-122">Bkz: [Azure App Service'te bir ASP.NET web uygulaması oluşturma](../app-service-web/app-service-web-get-started-dotnet.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="5832c-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="5832c-123">Merhaba çözüm hello kısayol menüsünü açın ve seçin **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="5832c-123">Open hello shortcut menu for hello solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="5832c-124">Bu hello Git Visual Studio Team Services içinde kullanmış olduğunuz ilk kez kullanıyorsanız, tooprovide bazı bilgileri tooidentify kendiniz Git içinde ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="5832c-124">If this is hello first time you've used Git in Visual Studio Team Services, you'll need tooprovide some information tooidentify yourself in Git.</span></span> <span data-ttu-id="5832c-125">Merhaba, **bekleyen değişiklikleri** alanı **Takım Gezgini**, kullanıcı adınızı girin ve e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="5832c-125">In hello **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="5832c-126">Merhaba yürütülmesi için bir açıklama girin ve ardından hello **tamamlama** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5832c-126">Enter a comment for hello commit and then choose hello **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="5832c-127">Merhaba seçenekleri tooinclude dikkat edin veya belirli değişiklikleri, iade ettiğinizde dışlayın.</span><span class="sxs-lookup"><span data-stu-id="5832c-127">Note hello options tooinclude or exclude specific changes when you check in.</span></span> <span data-ttu-id="5832c-128">Merhaba, değişirse istediğiniz dışlanır, seçin **dahil tüm**.</span><span class="sxs-lookup"><span data-stu-id="5832c-128">If hello changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="5832c-129">Yerel hello deposu kopyanızda taahhüt hello değişiklikleri şimdi seçtiğiniz.</span><span class="sxs-lookup"><span data-stu-id="5832c-129">You've now committed hello changes in your local copy of hello repository.</span></span> <span data-ttu-id="5832c-130">Ardından, hello seçerek değişiklikleri hello server ile eşitleme **eşitleme** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="5832c-130">Next, sync those changes with hello server by choosing hello **Sync** link.</span></span>

## <a name="3-connect-hello-project-tooazure"></a><span data-ttu-id="5832c-131">3: hello proje tooAzure Bağlan</span><span class="sxs-lookup"><span data-stu-id="5832c-131">3: Connect hello project tooAzure</span></span>
1. <span data-ttu-id="5832c-132">Bazı kaynak kodu ile Visual Studio Team Services bir Git deposu var, hazır tooconnect olan git deposu tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5832c-132">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready tooconnect your git repository tooAzure.</span></span>  <span data-ttu-id="5832c-133">Merhaba, [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), bulut hizmeti veya web uygulamanızı seçin veya hello + sol hello alt ve seçme simgesini seçerek yeni bir tane oluşturun **bulut hizmeti** veya **Web uygulaması**ve ardından **hızlı Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="5832c-133">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing hello + icon at hello bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="5832c-134">Bulut Hizmetleri için hello seçin **Visual Studio Team Services ile yayımlamayı ayarlayın** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="5832c-134">For cloud services, choose hello **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="5832c-135">Web uygulamaları için hello seçin **kaynak denetiminden dağıtım Ayarla** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="5832c-135">For web apps, choose hello **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="5832c-136">Merhaba sihirbazında, Visual Studio Team Services hesabınızın adını hello hello metin kutusuna yazın ve hello **şimdi Yetkilendir** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="5832c-136">In hello wizard, type hello name of your Visual Studio Team Services account in hello textbox and choose hello **Authorize Now** link.</span></span> <span data-ttu-id="5832c-137">İçinde toosign istenebilir.</span><span class="sxs-lookup"><span data-stu-id="5832c-137">You might be asked toosign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="5832c-138">Merhaba, **bağlantı isteği** açılan iletişim kutusunda, seçin **kabul** tooauthorize ekibinizin proje Visual Studio Team Services içinde Azure tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="5832c-138">In hello **Connection Request** pop-up dialog, choose **Accept** tooauthorize Azure tooconfigure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="5832c-139">Yetkilendirme başarılı olduktan sonra Visual Studio Team Services takım projeleriniz içeren bir açılır liste bakın.</span><span class="sxs-lookup"><span data-stu-id="5832c-139">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="5832c-140">Merhaba önceki adımlarda oluşturduğunuz takım projesi Hello adını seçin ve hello sihirbazın onay düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="5832c-140">Select hello name of team project that you created in hello previous steps, and choose hello wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="5832c-141">Merhaba yürütme tooyour depo, Visual Studio Team Services itme sonraki sefer yapı ve proje tooAzure dağıtın.</span><span class="sxs-lookup"><span data-stu-id="5832c-141">hello next time you push a commit tooyour repository, Visual Studio Team Services will build and deploy your project tooAzure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="5832c-142">4: yeniden tetikleyebilir ve projenizi yeniden dağıtmak</span><span class="sxs-lookup"><span data-stu-id="5832c-142">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="5832c-143">Visual Studio'da bir dosyasını açın ve onu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5832c-143">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="5832c-144">Örneğin, hello dosya değişiklik `_Layout.cshtml` hello görünümleri altında\\paylaşılan klasöründe bir MVC web rolü.</span><span class="sxs-lookup"><span data-stu-id="5832c-144">For example, change hello file `_Layout.cshtml` under hello Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="5832c-145">Hello site için Hello altbilgi metni düzenleyin ve hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5832c-145">Edit hello footer text for hello site and save hello file.</span></span>
   
    ![][18]
3. <span data-ttu-id="5832c-146">İçinde **Çözüm Gezgini**hello çözüm düğümü, proje düğümüne veya hello dosya için değiştirdiğiniz hello kısayol menüsünü açın ve ardından **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="5832c-146">In **Solution Explorer**, open hello shortcut menu for hello solution node, project node, or hello file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="5832c-147">Bir yorum yazın ve seçin **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="5832c-147">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="5832c-148">Merhaba seçin **eşitleme** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="5832c-148">Choose hello **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="5832c-149">Merhaba seçin **anında** toopush Visual Studio Team Services yürütme toohello deponuza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="5832c-149">Choose hello **Push** link toopush your commit toohello repository in Visual Studio Team Services.</span></span> <span data-ttu-id="5832c-150">(Merhaba de kullanabilirsiniz **eşitleme** toocopy işlemeleri toohello deponuz düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5832c-150">(You can also use hello **Sync** button toocopy your commits toohello repository.</span></span> <span data-ttu-id="5832c-151">Merhaba fark vardır **eşitleme** çeken hello depodan en son değişiklikleri de hello.)</span><span class="sxs-lookup"><span data-stu-id="5832c-151">hello difference is that **Sync** also pulls hello latest changes from hello repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="5832c-152">Merhaba seçin **ev** düğmesini tooreturn toohello **Takım Gezgini** giriş sayfası.</span><span class="sxs-lookup"><span data-stu-id="5832c-152">Choose hello **Home** button tooreturn toohello **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="5832c-153">Seçin **derlemeler** tooview hello derlemeler sürüyor.</span><span class="sxs-lookup"><span data-stu-id="5832c-153">Choose **Builds** tooview hello builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="5832c-154">**Takım Gezgini** bir yapı için iade tetiklenen gösterir.</span><span class="sxs-lookup"><span data-stu-id="5832c-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="5832c-155">tooview ayrıntılı günlüğü hello yapı olarak ilerledikçe, devam eden hello yapı hello adını çift.</span><span class="sxs-lookup"><span data-stu-id="5832c-155">tooview a detailed log as hello build progresses, double-click hello name of hello build in progress.</span></span>
10. <span data-ttu-id="5832c-156">Merhaba derleme sürüyor olsa da, Başlangıç Sihirbazı toolink tooAzure kullanıldığında, oluşturulan hello derleme tanımı göz atın.</span><span class="sxs-lookup"><span data-stu-id="5832c-156">While hello build is in-progress, take a look at hello build definition that was created when you used hello wizard toolink tooAzure.</span></span>  <span data-ttu-id="5832c-157">Merhaba derleme tanımı için hello kısayol menüsünü açın ve seçin **derleme tanımını Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="5832c-157">Open hello shortcut menu for hello build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="5832c-158">Merhaba, **tetikleyici** sekmesinde hello derleme tanımı toobuild her iade, varsayılan olarak ayarlandığını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5832c-158">In hello **Trigger** tab, you will see that hello build definition is set toobuild on every check-in, by default.</span></span> <span data-ttu-id="5832c-159">(Bir bulut hizmeti için Visual Studio Team Services oluşturur ve ortam otomatik olarak hazırlama hello ana dala toohello dağıtır.</span><span class="sxs-lookup"><span data-stu-id="5832c-159">(For a cloud service, Visual Studio Team Services builds and deploys hello master branch toohello staging environment automatically.</span></span> <span data-ttu-id="5832c-160">El ile adım toodeploy toohello Canlı site toodo etmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5832c-160">You still have toodo a manual step toodeploy toohello live site.</span></span> <span data-ttu-id="5832c-161">Ortamı hazırlama sahip olmayan bir web uygulaması için toohello Canlı doğrudan site hello ana dala dağıtır.</span><span class="sxs-lookup"><span data-stu-id="5832c-161">For a web app that doesn't have staging environment, it deploys hello master branch directly toohello live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="5832c-162">Merhaba, **işlem** sekmesinde, bulut hizmeti veya web uygulamasının adını toohello hello dağıtım ortamı ayarlayın görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5832c-162">In hello **Process** tab, you can see hello deployment environment is set toohello name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="5832c-163">Merhaba Varsayılanları farklı değerler istiyorsanız hello özelliklerinin değerlerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="5832c-163">Specify values for hello properties if you want different values than hello defaults.</span></span> <span data-ttu-id="5832c-164">Hello Azure yayımlama hello özelliklerdir **dağıtım** bölümü ve ayrıca gerekebilir tooset MSBuild parametreleri.</span><span class="sxs-lookup"><span data-stu-id="5832c-164">hello properties for Azure publishing are in hello **Deployment** section, and you might also need tooset MSBuild parameters.</span></span> <span data-ttu-id="5832c-165">Örneğin, bir bulut hizmeti projesini toospecify "Bulut" dışında bir hizmet yapılandırması hello MSbuild parametreler çok kümesindeki`/p:TargetProfile=[YourProfile]` nerede *[YourProfile]* hizmet yapılandırma dosyası gibi bir ad ile eşleşir ServiceConfiguration. *YourProfile*.cscfg.</span><span class="sxs-lookup"><span data-stu-id="5832c-165">For example, in a cloud service project, toospecify a service configuration other than "Cloud", set hello MSbuild parameters too`/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="5832c-166">Merhaba aşağıdaki tabloda hello kullanılabilir özellikler hello gösterilmektedir **dağıtım** bölümü:</span><span class="sxs-lookup"><span data-stu-id="5832c-166">hello following table shows hello available properties in hello **Deployment** section:</span></span>
    
    | <span data-ttu-id="5832c-167">Özellik</span><span class="sxs-lookup"><span data-stu-id="5832c-167">Property</span></span> | <span data-ttu-id="5832c-168">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5832c-168">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="5832c-169">Güvenilmeyen Sertifikalar izin ver</span><span class="sxs-lookup"><span data-stu-id="5832c-169">Allow Untrusted Certificates</span></span> |<span data-ttu-id="5832c-170">SSL sertifikaları yanlışsa, bir kök yetkilisi tarafından imzalanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5832c-170">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="5832c-171">Yükseltme izin ver</span><span class="sxs-lookup"><span data-stu-id="5832c-171">Allow Upgrade</span></span> |<span data-ttu-id="5832c-172">Merhaba dağıtım tooupdate yeni bir tane oluşturmak yerine var olan bir dağıtımını sağlar.</span><span class="sxs-lookup"><span data-stu-id="5832c-172">Allows hello deployment tooupdate an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="5832c-173">Başlangıç IP adresi korur.</span><span class="sxs-lookup"><span data-stu-id="5832c-173">Preserves hello IP address.</span></span> |
    | <span data-ttu-id="5832c-174">Silmeyin</span><span class="sxs-lookup"><span data-stu-id="5832c-174">Do Not Delete</span></span> |<span data-ttu-id="5832c-175">TRUE ise, var olan bir ilgisiz dağıtımını üzerine yazma (yükseltme izin verilir).</span><span class="sxs-lookup"><span data-stu-id="5832c-175">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="5832c-176">Yol tooDeployment ayarları</span><span class="sxs-lookup"><span data-stu-id="5832c-176">Path tooDeployment Settings</span></span> |<span data-ttu-id="5832c-177">Merhaba yol tooyour .pubxml dosya hello depodaki göreli toohello kök klasöründe bir web uygulaması için.</span><span class="sxs-lookup"><span data-stu-id="5832c-177">hello path tooyour .pubxml file for a web app, relative toohello root folder of hello repo.</span></span> <span data-ttu-id="5832c-178">Bulut Hizmetleri için yoksayıldı.</span><span class="sxs-lookup"><span data-stu-id="5832c-178">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="5832c-179">SharePoint dağıtım ortamı</span><span class="sxs-lookup"><span data-stu-id="5832c-179">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="5832c-180">aynı hello hizmet adı olarak hello.</span><span class="sxs-lookup"><span data-stu-id="5832c-180">hello same as hello service name.</span></span> |
    | <span data-ttu-id="5832c-181">Azure dağıtım ortamı</span><span class="sxs-lookup"><span data-stu-id="5832c-181">Azure Deployment Environment</span></span> |<span data-ttu-id="5832c-182">Merhaba web uygulaması veya Bulut hizmeti adı.</span><span class="sxs-lookup"><span data-stu-id="5832c-182">hello web app or cloud service name.</span></span> |
14. <span data-ttu-id="5832c-183">Bu zamana kadar yapınızın başarıyla tamamlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5832c-183">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="5832c-184">Merhaba derleme adına çift tıklayın, Visual Studio gösterir. bir **Yapı Özeti**, tüm test sonuçlarını da dahil olmak üzere, birim testi projelerini ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="5832c-184">If you double-click hello build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="5832c-185">Merhaba, [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), ilişkili hello dağıtım üzerinde hello görüntüleyebilirsiniz **dağıtımları** ortam hazırlama hello seçildiğinde sekme.</span><span class="sxs-lookup"><span data-stu-id="5832c-185">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view hello associated deployment on hello **Deployments** tab when hello staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="5832c-186">Tooyour sitenin URL'sini göz atın.</span><span class="sxs-lookup"><span data-stu-id="5832c-186">Browse tooyour site's URL.</span></span> <span data-ttu-id="5832c-187">Bir web uygulaması için yalnızca hello seçme **Gözat** hello portalda düğmesine.</span><span class="sxs-lookup"><span data-stu-id="5832c-187">For a web app, just choose  hello **Browse** button in hello portal.</span></span> <span data-ttu-id="5832c-188">Bir bulut hizmeti için hello URL'si hello seçin **Hızlı Bakış** hello bölümünü **Pano** hello hazırlama ortamını gösteren sayfası.</span><span class="sxs-lookup"><span data-stu-id="5832c-188">For a cloud service, choose hello URL in hello **Quick Glance** section of hello **Dashboard** page that shows hello Staging environment.</span></span>
    
    <span data-ttu-id="5832c-189">Bulut Hizmetleri için sürekli tümleştirme dağıtımlarından yayımlanan toohello hazırlama ortamını varsayılan olarak ' dir.</span><span class="sxs-lookup"><span data-stu-id="5832c-189">Deployments from continuous integration for cloud services are published toohello Staging environment by default.</span></span> <span data-ttu-id="5832c-190">Bu ayarı hello tarafından değiştirebilirsiniz **alternatif bir bulut hizmeti ortamını** özelliği çok**üretim**.</span><span class="sxs-lookup"><span data-stu-id="5832c-190">You can change this by setting hello **Alternate Cloud Service Environment** property too**Production**.</span></span> <span data-ttu-id="5832c-191">İşte hello site URL'si hello bulut hizmetin panosu sayfasında olduğu.</span><span class="sxs-lookup"><span data-stu-id="5832c-191">Here's where hello site URL is on hello cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="5832c-192">Yeni bir tarayıcı sekmesi tooreveal çalışan sitenizi açılır.</span><span class="sxs-lookup"><span data-stu-id="5832c-192">A new browser tab will open tooreveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="5832c-193">Yaptığınız diğer tooyour proje değişikliklerini, tetikleyici daha oluşturur ve birden çok dağıtım toplanacaktır.</span><span class="sxs-lookup"><span data-stu-id="5832c-193">If you make other changes tooyour project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="5832c-194">Etkin olarak işaretli olduğundan hello son.</span><span class="sxs-lookup"><span data-stu-id="5832c-194">hello latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="5832c-195">5: önceki bir yapı yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="5832c-195">5: Redeploy an earlier build</span></span>
<span data-ttu-id="5832c-196">Bu adım isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="5832c-196">This step is optional.</span></span> <span data-ttu-id="5832c-197">Klasik Azure portalı Merhaba, önceki bir dağıtıma seçin ve seçin **dağıtmanız** toorewind, site tooan önceki iade etme.</span><span class="sxs-lookup"><span data-stu-id="5832c-197">In hello Azure classic portal, choose an earlier deployment and choose **Redeploy** toorewind your site tooan earlier check-in.</span></span> <span data-ttu-id="5832c-198">Bu TFS'de yeni bir derlemeyi tetiklemeyi ve yeni bir giriş dağıtım geçmişiniz oluşturmak, unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5832c-198">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-hello-production-deployment"></a><span data-ttu-id="5832c-199">6: hello Üretim dağıtımı değiştirme</span><span class="sxs-lookup"><span data-stu-id="5832c-199">6: Change hello Production deployment</span></span>
<span data-ttu-id="5832c-200">Hazır olduğunuzda seçerek hello hazırlama ortamı toohello üretim ortamını yükseltebilirsiniz **takas** hello Klasik Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="5832c-200">When you are ready, you can promote hello Staging environment toohello Production environment by choosing **Swap** in hello Azure classic portal.</span></span> <span data-ttu-id="5832c-201">Yeni dağıtılan hello hazırlama ortamıdır yükseltilen tooProduction ve hello önceki üretim ortamında, varsa, bir hazırlama ortamını olur.</span><span class="sxs-lookup"><span data-stu-id="5832c-201">hello newly deployed Staging environment is promoted tooProduction, and hello previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="5832c-202">Hello etkin dağıtım hello üretim ve hazırlama ortamları için farklı olabilir, ancak son yapılar hello dağıtım geçmişini olduğu hello aynı ne olursa olsun, ortam.</span><span class="sxs-lookup"><span data-stu-id="5832c-202">hello Active deployment may be different for hello Production and Staging environments, but hello deployment history of recent builds is hello same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="5832c-203">7: bir çalışma dalı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="5832c-203">7: Deploy from a working branch.</span></span>
<span data-ttu-id="5832c-204">Git kullandığınızda, genellikle bir çalışma dalı değişiklikleri yapın ve geliştirme tamamlanmış durumuna ulaştığında hello ana dala tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5832c-204">When you use Git, you usually make changes in a working branch and integrate into hello master branch when your development reaches a finished state.</span></span> <span data-ttu-id="5832c-205">Merhaba geliştirme aşamasında bir proje toobuild istediğiniz ve hello çalışma dalı tooAzure dağıtın.</span><span class="sxs-lookup"><span data-stu-id="5832c-205">During hello development phase of a project, you'll want toobuild and deploy hello working branch tooAzure.</span></span>

1. <span data-ttu-id="5832c-206">İçinde **Takım Gezgini**, hello seçin **giriş** düğmesine ve ardından hello **dalları** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5832c-206">In **Team Explorer**, choose hello **Home** button and then choose hello **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="5832c-207">Merhaba seçin **dalı** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="5832c-207">Choose hello **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="5832c-208">"Çalışıyor" gibi hello dalın Hello adı girin ve seçin **oluşturma şube**.</span><span class="sxs-lookup"><span data-stu-id="5832c-208">Enter hello name of hello branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="5832c-209">Bu, yeni bir yerel dalı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5832c-209">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="5832c-210">Merhaba şube yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="5832c-210">Publish hello branch.</span></span> <span data-ttu-id="5832c-211">Merhaba şube adlarında seçin **yayımlanmamış dalları**ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="5832c-211">Choose hello branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="5832c-212">Varsayılan olarak, yalnızca toohello ana dala tetikleyici sürekli bir yapı değiştirir.</span><span class="sxs-lookup"><span data-stu-id="5832c-212">By default, only changes toohello master branch trigger a continuous build.</span></span> <span data-ttu-id="5832c-213">bir çalışma dalı için sürekli derlemesi tooset seçin hello **derlemeler** sayfasındaki **Takım Gezgini**ve seçin **derleme tanımını Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="5832c-213">tooset up continuous build for a working branch, choose hello **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="5832c-214">Açık hello **kaynak ayarları** sekmesi. Altında **izlenen dalları sürekli tümleştirme ve yapı**, seçin **tooadd yeni bir satır burayı**.</span><span class="sxs-lookup"><span data-stu-id="5832c-214">Open hello **Source Settings** tab. Under **Monitored branches for continuous integration and build**, choose **Click here tooadd a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="5832c-215">Uyarı/refs/çalışma gibi oluşturulan hello şube belirtin.</span><span class="sxs-lookup"><span data-stu-id="5832c-215">Specify hello branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="5832c-216">Hello kodda, açık hello kısayol menüsünü hello değiştirilen dosya için bir değişiklik yapın ve ardından **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="5832c-216">Make a change in hello code, open hello shortcut menu for hello changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="5832c-217">Merhaba seçin **eşitlenmemiş işlemeleri** hello seçin ve bağlama **eşitleme** düğmesini veya hello **anında** bağlantı toocopy hello hello çalışma dalı Visual Studio'da toohello kopyasını değiştirir Team Services.</span><span class="sxs-lookup"><span data-stu-id="5832c-217">Choose hello **Unsynced Commits** link, and choose  hello **Sync** button or hello **Push** link toocopy hello changes toohello copy of hello working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="5832c-218">Toohello gidin **derlemeler** görüntülemek ve hemen tetiklenen hello yapı hello çalışma dalı için bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5832c-218">Navigate toohello **Builds** view and find hello build that just got triggered for hello working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5832c-219">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5832c-219">Next steps</span></span>
<span data-ttu-id="5832c-220">Git Visual Studio Team Services ile kullanma hakkında daha fazla ipucu toolearn bkz [geliştirme ve Visual Studio kullanarak Git kodunuzda paylaşmak](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) ve Visual Studio Team Services toopublish tarafından yönetilmeyen bir Git deposu kullanma hakkında bilgi için tooAzure, bkz: [sürekli dağıtım tooAzure uygulama hizmeti](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5832c-220">toolearn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) and for information about using a Git repository that's not managed by Visual Studio Team Services toopublish tooAzure, see [Continuous Deployment tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="5832c-221">Visual Studio Team Services hakkında daha fazla bilgi için bkz: [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="5832c-221">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
