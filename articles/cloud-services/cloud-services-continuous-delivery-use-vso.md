---
title: "Visual Studio Team Services Azure içinde aaaContinuous teslimiyle | Microsoft Docs"
description: "Nasıl tooconfigure tooautomatically ve toohello Web uygulamasını Azure App Service veya Bulut hizmetlerini özelliğinde dağıtacak projeleri, Visual Studio Team Services ekip öğrenin."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: eae75729e1c1a55f9bc3375604a8192f329d0042
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services"></a><span data-ttu-id="7feb0-103">Visual Studio Team Services kullanarak kesintisiz teslim tooAzure</span><span class="sxs-lookup"><span data-stu-id="7feb0-103">Continuous delivery tooAzure using Visual Studio Team Services</span></span>
<span data-ttu-id="7feb0-104">Visual Studio Team Services takım projeleri tooautomatically yapınızı yapılandırın ve tooAzure web uygulamaları dağıtma veya Bulut Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="7feb0-104">You can configure your Visual Studio Team Services team projects tooautomatically build and deploy tooAzure web apps or cloud services.</span></span>  <span data-ttu-id="7feb0-105">(Nasıl tooset yukarı sürekli bir yapı ve sistem kullanarak dağıtma hakkında bilgi için bir *şirket içi* Team Foundation Server, bkz: [Azure bulut Hizmetleri için devamlı teslim](cloud-services-dotnet-continuous-delivery.md).)</span><span class="sxs-lookup"><span data-stu-id="7feb0-105">(For information on how tooset up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="7feb0-106">Bu öğreticide Visual Studio 2013 ve Azure SDK'sını hello olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="7feb0-106">This tutorial assumes you have Visual Studio 2013 and hello Azure SDK installed.</span></span> <span data-ttu-id="7feb0-107">Visual Studio 2013 zaten yoksa, hello seçerek karşıdan **ücretsiz olarak başlayın** adresindeki bağlantı [www.visualstudio.com](http://www.visualstudio.com). Yükleme hello Azure SDK [burada](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="7feb0-107">If you don't already have Visual Studio 2013, download it by choosing hello **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com). Install hello Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="7feb0-108">Bu öğretici bir Visual Studio Team Services hesabı toocomplete gerekir: yapabilecekleriniz [ücretsiz bir Visual Studio Team Services hesabı açabilirsiniz](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="7feb0-108">You need an Visual Studio Team Services account toocomplete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="7feb0-109">bir bulut hizmeti tooautomatically yukarı tooset derleme ve Visual Studio Team Services kullanarak tooAzure dağıtma, şu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="7feb0-109">tooset up a cloud service tooautomatically build and deploy tooAzure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="7feb0-110">1: takım projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="7feb0-110">1: Create a team project</span></span>
<span data-ttu-id="7feb0-111">Hello yönergeleri izleyerek [burada](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate ekibinizin proje ve tooVisual Studio bağlayın.</span><span class="sxs-lookup"><span data-stu-id="7feb0-111">Follow hello instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate your team project and link it tooVisual Studio.</span></span> <span data-ttu-id="7feb0-112">Bu kılavuz, kaynak denetim çözümü Team Foundation sürüm denetimi (TFVC'yi) kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="7feb0-112">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="7feb0-113">Sürüm denetimi için toouse Git istiyorsanız, bkz: [hello Git sürüm bu kılavuzun](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span><span class="sxs-lookup"><span data-stu-id="7feb0-113">If you want toouse Git for version control, see [hello Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-toosource-control"></a><span data-ttu-id="7feb0-114">2: bir proje toosource denetiminde denetleyin</span><span class="sxs-lookup"><span data-stu-id="7feb0-114">2: Check in a project toosource control</span></span>
1. <span data-ttu-id="7feb0-115">Visual Studio'da toodeploy istediğiniz ya da yeni bir tane oluşturun hello çözümü açın.</span><span class="sxs-lookup"><span data-stu-id="7feb0-115">In Visual Studio, open hello solution you want toodeploy, or create a new one.</span></span>
   <span data-ttu-id="7feb0-116">Bir web uygulaması dağıtma veya Bulut hizmeti (Azure uygulaması) aşağıdaki hello tarafından bu izlenecek adımları.</span><span class="sxs-lookup"><span data-stu-id="7feb0-116">You can deploy a web app or a cloud service (Azure Application) by following hello steps in this walkthrough.</span></span>
   <span data-ttu-id="7feb0-117">Yeni bir çözüm toocreate istiyorsanız, yeni bir Azure bulut hizmeti projesi ya da yeni bir ASP.NET MVC projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7feb0-117">If you want toocreate a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="7feb0-118">Proje hedefleri .NET Framework 4 veya 4.5 hello ve bir bulut hizmeti projesini oluşturuyorsanız, bir ASP.NET MVC web rolü ve çalışan rolü eklemek ve hello web rolü için Internet uygulamasını seçin emin olun.</span><span class="sxs-lookup"><span data-stu-id="7feb0-118">Make sure that hello project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for hello web role.</span></span> <span data-ttu-id="7feb0-119">İstendiğinde, seçin **Internet uygulama**.</span><span class="sxs-lookup"><span data-stu-id="7feb0-119">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="7feb0-120">Toocreate bir web uygulaması istiyorsanız hello ASP.NET Web uygulaması proje şablonunu seçin ve ardından MVC seçin.</span><span class="sxs-lookup"><span data-stu-id="7feb0-120">If you want toocreate a web app, choose hello ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="7feb0-121">Bkz: [Azure App Service'te bir ASP.NET web uygulaması oluşturma](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="7feb0-121">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7feb0-122">Visual Studio Team Services, şu anda yalnızca Visual Studio Web uygulamalarının CI dağıtımları destekler.</span><span class="sxs-lookup"><span data-stu-id="7feb0-122">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="7feb0-123">Web sitesi projeleri kapsamının dışında ' dir.</span><span class="sxs-lookup"><span data-stu-id="7feb0-123">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="7feb0-124">Merhaba çözüm hello bağlam menüsünü açın ve seçin **Çözüm Ekle tooSource denetim**.</span><span class="sxs-lookup"><span data-stu-id="7feb0-124">Open hello context menu for hello solution, and choose **Add Solution tooSource Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="7feb0-125">Kabul etmek veya hello varsayılanları değiştirmek ve hello seçin **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7feb0-125">Accept or change hello defaults and choose hello **OK** button.</span></span> <span data-ttu-id="7feb0-126">Kaynak Denetim simgelerini Hello işlemi tamamlandıktan sonra görünür **Çözüm Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="7feb0-126">Once hello process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="7feb0-127">Merhaba çözüm hello kısayol menüsünü açın ve seçin **iade**.</span><span class="sxs-lookup"><span data-stu-id="7feb0-127">Open hello shortcut menu for hello solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="7feb0-128">Merhaba, **bekleyen değişiklikleri** alanı **Takım Gezgini**hello iade için bir açıklama yazın ve hello seçin **iade** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7feb0-128">In hello **Pending Changes** area of **Team Explorer**, type a comment for hello check-in and choose hello **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="7feb0-129">Merhaba seçenekleri tooinclude dikkat edin veya belirli değişiklikleri, iade ettiğinizde dışlayın.</span><span class="sxs-lookup"><span data-stu-id="7feb0-129">Note hello options tooinclude or exclude specific changes when you check in.</span></span> <span data-ttu-id="7feb0-130">Değişiklikleri dışlanır isterseniz, hello seçin **dahil tüm** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="7feb0-130">If desired changes are excluded, choose hello **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-hello-project-tooazure"></a><span data-ttu-id="7feb0-131">3: hello proje tooAzure Bağlan</span><span class="sxs-lookup"><span data-stu-id="7feb0-131">3: Connect hello project tooAzure</span></span>
1. <span data-ttu-id="7feb0-132">Bazı kaynak kodu ile VS Team Services takım projesi içine sahip olduğunuza göre hazır tooconnect olan ekibinizin proje tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7feb0-132">Now that you have a VS Team Services team project with some source code in it, you are ready tooconnect your team project tooAzure.</span></span>  <span data-ttu-id="7feb0-133">Merhaba, [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), bulut hizmeti veya web uygulamanızı seçin veya hello seçerek yeni bir tane oluşturun  **+**  hello sol alt ve seçme simgesine **bulut hizmeti** veya **Web uygulaması** ve ardından **hızlı Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="7feb0-133">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing hello **+** icon at hello bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="7feb0-134">Merhaba seçin **Visual Studio Team Services ile yayımlamayı ayarlayın** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="7feb0-134">Choose hello **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="7feb0-135">Hello sihirbazında, hello metin kutusuna hello Visual Studio Team Services hesabınızın adını yazın ve hello **şimdi Yetkilendir** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="7feb0-135">In hello wizard, type hello name of your Visual Studio Team Services account in hello textbox and click hello **Authorize Now** link.</span></span> <span data-ttu-id="7feb0-136">İçinde toosign istenebilir.</span><span class="sxs-lookup"><span data-stu-id="7feb0-136">You might be asked toosign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="7feb0-137">Merhaba, **bağlantı isteği** açılan iletişim kutusunda, hello seçin **kabul** düğmesini tooauthorize ekibinizin proje VS Team Services içinde Azure tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="7feb0-137">In hello **Connection Request** pop-up dialog, choose hello **Accept** button tooauthorize Azure tooconfigure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="7feb0-138">Yetkilendirme başarılı olduğunda, Visual Studio Team Services takım projelerinin listesini içeren bir açılır bakın.</span><span class="sxs-lookup"><span data-stu-id="7feb0-138">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="7feb0-139">Merhaba önceki adımlarda oluşturduğunuz takım projesi Hello adını seçin ve ardından hello sihirbazın onay düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="7feb0-139">Choose  hello name of team project that you created in hello previous steps, and then choose hello wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="7feb0-140">Projenizi bağlandıktan sonra değişiklikler tooyour Visual Studio Team Services takım projesinde denetleme bazı yönergeler görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7feb0-140">After your project is linked, you will see some instructions for checking in changes tooyour Visual Studio Team Services team project.</span></span>  <span data-ttu-id="7feb0-141">Sonraki iade, Visual Studio Team Services oluşturup, proje tooAzure dağıtacak.</span><span class="sxs-lookup"><span data-stu-id="7feb0-141">On your next check-in, Visual Studio Team Services will build and deploy your project tooAzure.</span></span>  <span data-ttu-id="7feb0-142">Try hello tıklatarak bunu şimdi **Visual Studio'dan iade** bağlamak ve ardından hello **başlatma Visual Studio** bağlantı (veya eşdeğer hello **Visual Studio** hello altındaki düğmesi Merhaba portal ekran).</span><span class="sxs-lookup"><span data-stu-id="7feb0-142">Try this now by clicking hello **Check In from Visual Studio** link, and then hello **Launch Visual Studio** link (or hello equivalent **Visual Studio** button at hello bottom of hello portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="7feb0-143">4: yeniden tetikleyebilir ve projenizi yeniden dağıtmak</span><span class="sxs-lookup"><span data-stu-id="7feb0-143">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="7feb0-144">Visual Studio'nun içinde **Takım Gezgini**, hello seçin **Kaynak Denetim Gezgini** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="7feb0-144">In Visual Studio's **Team Explorer**, choose hello **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="7feb0-145">Tooyour çözüm dosyasını gidin ve açın.</span><span class="sxs-lookup"><span data-stu-id="7feb0-145">Navigate tooyour solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="7feb0-146">İçinde **Çözüm Gezgini**, bir dosyasını açın ve değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7feb0-146">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="7feb0-147">Örneğin, hello dosya değişiklik `_Layout.cshtml` hello görünümleri altında\\paylaşılan klasöründe bir MVC web rolü.</span><span class="sxs-lookup"><span data-stu-id="7feb0-147">For example, change hello file `_Layout.cshtml` under hello Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="7feb0-148">Merhaba logosu hello site için düzenleyin ve seçin **Ctrl + S** toosave hello dosya.</span><span class="sxs-lookup"><span data-stu-id="7feb0-148">Edit hello logo for hello site and choose **Ctrl+S** toosave hello file.</span></span>
   
    ![][18]
5. <span data-ttu-id="7feb0-149">İçinde **Takım Gezgini**, hello seçin **bekleyen değişiklikleri** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="7feb0-149">In **Team Explorer**, choose hello **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="7feb0-150">Bir açıklama girin ve ardından hello **iade** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7feb0-150">Enter a comment and then choose hello **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="7feb0-151">Merhaba seçin **ev** düğmesini tooreturn toohello **Takım Gezgini** giriş sayfası.</span><span class="sxs-lookup"><span data-stu-id="7feb0-151">Choose hello **Home** button tooreturn toohello **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="7feb0-152">Merhaba seçin **derlemeler** bağlantı tooview hello derlemeler sürüyor.</span><span class="sxs-lookup"><span data-stu-id="7feb0-152">Choose hello **Builds** link tooview hello builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="7feb0-153">**Takım Gezgini** bir yapı için iade tetiklenen gösterir.</span><span class="sxs-lookup"><span data-stu-id="7feb0-153">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="7feb0-154">İlerleme tooview ayrıntılı günlüğü hello derlemede Hello adını hello yapı ilerledikçe çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7feb0-154">Double-click hello name of hello build in progress tooview a detailed log as hello build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="7feb0-155">Merhaba derleme sürüyor olsa da, Başlangıç Sihirbazı'nı kullanarak TFS tooAzure bağlandığında, oluşturulan hello derleme tanımı göz atın.</span><span class="sxs-lookup"><span data-stu-id="7feb0-155">While hello build is in-progress, take a look at hello build definition that was created when you linked TFS tooAzure by using hello wizard.</span></span>  <span data-ttu-id="7feb0-156">Merhaba derleme tanımı için hello kısayol menüsünü açın ve seçin **derleme tanımını Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="7feb0-156">Open hello shortcut menu for hello build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="7feb0-157">Merhaba, **tetikleyici** sekmesinde hello derleme tanımı toobuild her iade varsayılan olarak ayarlandığını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7feb0-157">In hello **Trigger** tab, you will see that hello build definition is set toobuild on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="7feb0-158">Merhaba, **işlem** sekmesinde, bulut hizmeti veya web uygulamasının adını toohello hello dağıtım ortamı ayarlayın görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7feb0-158">In hello **Process** tab, you can see hello deployment environment is set toohello name of your cloud service or web app.</span></span> <span data-ttu-id="7feb0-159">Web uygulamaları ile çalışıyorsanız, gördüğünüz hello özellikleri burada gösterilen olanlardan farklı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7feb0-159">If you are working with web apps, hello properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="7feb0-160">Merhaba Varsayılanları farklı değerler istiyorsanız hello özelliklerinin değerlerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="7feb0-160">Specify values for hello properties if you want different values than hello defaults.</span></span> <span data-ttu-id="7feb0-161">Hello Azure yayımlama hello özelliklerdir **dağıtım** bölümü.</span><span class="sxs-lookup"><span data-stu-id="7feb0-161">hello properties for Azure publishing are in hello **Deployment** section.</span></span>
    
     <span data-ttu-id="7feb0-162">Merhaba aşağıdaki tabloda hello kullanılabilir özellikler hello gösterilmektedir **dağıtım** bölümü:</span><span class="sxs-lookup"><span data-stu-id="7feb0-162">hello following table shows hello available properties in hello **Deployment** section:</span></span>
    
    | <span data-ttu-id="7feb0-163">Özellik</span><span class="sxs-lookup"><span data-stu-id="7feb0-163">Property</span></span> | <span data-ttu-id="7feb0-164">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="7feb0-164">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="7feb0-165">Güvenilmeyen Sertifikalar izin ver</span><span class="sxs-lookup"><span data-stu-id="7feb0-165">Allow Untrusted Certificates</span></span> |<span data-ttu-id="7feb0-166">SSL sertifikaları yanlışsa, bir kök yetkilisi tarafından imzalanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7feb0-166">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="7feb0-167">Yükseltme izin ver</span><span class="sxs-lookup"><span data-stu-id="7feb0-167">Allow Upgrade</span></span> |<span data-ttu-id="7feb0-168">Merhaba dağıtım tooupdate yeni bir tane oluşturmak yerine var olan bir dağıtımını sağlar.</span><span class="sxs-lookup"><span data-stu-id="7feb0-168">Allows hello deployment tooupdate an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="7feb0-169">Başlangıç IP adresi korur.</span><span class="sxs-lookup"><span data-stu-id="7feb0-169">Preserves hello IP address.</span></span> |
    | <span data-ttu-id="7feb0-170">Silmeyin</span><span class="sxs-lookup"><span data-stu-id="7feb0-170">Do Not Delete</span></span> |<span data-ttu-id="7feb0-171">TRUE ise, var olan bir ilgisiz dağıtımını üzerine yazma (yükseltme izin verilir).</span><span class="sxs-lookup"><span data-stu-id="7feb0-171">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="7feb0-172">Yol tooDeployment ayarları</span><span class="sxs-lookup"><span data-stu-id="7feb0-172">Path tooDeployment Settings</span></span> |<span data-ttu-id="7feb0-173">Merhaba yol tooyour .pubxml dosya hello depodaki göreli toohello kök klasöründe bir web uygulaması için.</span><span class="sxs-lookup"><span data-stu-id="7feb0-173">hello path tooyour .pubxml file for a web app, relative toohello root folder of hello repo.</span></span> <span data-ttu-id="7feb0-174">Bulut Hizmetleri için yoksayıldı.</span><span class="sxs-lookup"><span data-stu-id="7feb0-174">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="7feb0-175">SharePoint dağıtım ortamı</span><span class="sxs-lookup"><span data-stu-id="7feb0-175">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="7feb0-176">aynı hello hizmet adı olarak hello.</span><span class="sxs-lookup"><span data-stu-id="7feb0-176">hello same as hello service name.</span></span> |
    | <span data-ttu-id="7feb0-177">Azure dağıtım ortamı</span><span class="sxs-lookup"><span data-stu-id="7feb0-177">Azure Deployment Environment</span></span> |<span data-ttu-id="7feb0-178">Merhaba web uygulaması veya Bulut hizmeti adı.</span><span class="sxs-lookup"><span data-stu-id="7feb0-178">hello web app or cloud service name.</span></span> |
12. <span data-ttu-id="7feb0-179">Birden fazla hizmet yapılandırma (.cscfg dosyaları) kullanıyorsanız, hello istenen hizmet yapılandırmasını hello belirtebilirsiniz **MSBuild bağımsız değişkenleri Gelişmiş, yapı** ayarı.</span><span class="sxs-lookup"><span data-stu-id="7feb0-179">If you are using multiple service configurations (.cscfg files), you can specify hello desired service configuration in hello **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="7feb0-180">Örneğin, toouse ServiceConfiguration.Test.cscfg, ayarlar MSBuild bağımsız değişkenleri satırı seçeneği `/p:TargetProfile=Test`.</span><span class="sxs-lookup"><span data-stu-id="7feb0-180">For example, toouse ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="7feb0-181">Bu zamana kadar yapınızın başarıyla tamamlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7feb0-181">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="7feb0-182">Merhaba derleme adına çift tıklayın, Visual Studio gösterir. bir **Yapı Özeti**, tüm test sonuçlarını da dahil olmak üzere, birim testi projelerini ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="7feb0-182">If you double-click hello build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="7feb0-183">Merhaba, [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), ilişkili hello dağıtım üzerinde hello görüntüleyebilirsiniz **dağıtımları** ortam hazırlama hello seçildiğinde sekme.</span><span class="sxs-lookup"><span data-stu-id="7feb0-183">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view hello associated deployment on hello **Deployments** tab when hello staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="7feb0-184">Tooyour sitenin URL'sini göz atın.</span><span class="sxs-lookup"><span data-stu-id="7feb0-184">Browse tooyour site's URL.</span></span> <span data-ttu-id="7feb0-185">Bir web uygulaması için hello tıklatmanız **Gözat** düğmesi hello komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="7feb0-185">For a web app, just click hello **Browse** button on hello command bar.</span></span> <span data-ttu-id="7feb0-186">Bir bulut hizmeti için hello URL'si hello seçin **Hızlı Bakış** hello bölümünü **Pano** hello hazırlama ortamını bir bulut hizmeti için gösteren sayfası.</span><span class="sxs-lookup"><span data-stu-id="7feb0-186">For a cloud service, choose hello URL in hello **Quick Glance** section of hello **Dashboard** page that shows hello Staging environment for a cloud service.</span></span> <span data-ttu-id="7feb0-187">Bulut Hizmetleri için sürekli tümleştirme dağıtımlarından yayımlanan toohello hazırlama ortamını varsayılan olarak ' dir.</span><span class="sxs-lookup"><span data-stu-id="7feb0-187">Deployments from continuous integration for cloud services are published toohello Staging environment by default.</span></span> <span data-ttu-id="7feb0-188">Bu ayarı hello tarafından değiştirebilirsiniz **alternatif bir bulut hizmeti ortamını** özelliği çok**üretim**.</span><span class="sxs-lookup"><span data-stu-id="7feb0-188">You can change this by setting hello **Alternate Cloud Service Environment** property too**Production**.</span></span> <span data-ttu-id="7feb0-189">Bu ekran hello burada site URL'si hello bulut hizmetin panosu sayfasında gösterilir.</span><span class="sxs-lookup"><span data-stu-id="7feb0-189">This screenshot shows where hello site URL is on hello cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="7feb0-190">Yeni bir tarayıcı sekmesi tooreveal çalışan sitenizi açılır.</span><span class="sxs-lookup"><span data-stu-id="7feb0-190">A new browser tab will open tooreveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="7feb0-191">Bulut Hizmetleri için diğer değişiklikleri tooyour proje yaparsanız, tetikleyici daha oluşturur ve birden çok dağıtım toplanacaktır.</span><span class="sxs-lookup"><span data-stu-id="7feb0-191">For cloud services, if you make other changes tooyour project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="7feb0-192">Merhaba en son etkin olarak işaretlenmiş.</span><span class="sxs-lookup"><span data-stu-id="7feb0-192">hello latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="7feb0-193">5: önceki bir yapı yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="7feb0-193">5: Redeploy an earlier build</span></span>
<span data-ttu-id="7feb0-194">Bu adım isteğe bağlıdır ve toocloud Hizmetleri geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="7feb0-194">This step applies toocloud services and is optional.</span></span> <span data-ttu-id="7feb0-195">Klasik Azure portalı Merhaba, önceki bir dağıtıma seçin ve hello seçin **dağıtmanız** toorewind, site tooan önceki iade düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7feb0-195">In hello Azure classic portal, choose an earlier deployment and then choose hello **Redeploy** button toorewind your site tooan earlier check-in.</span></span>  <span data-ttu-id="7feb0-196">Bu TFS'de yeni bir derlemeyi tetiklemeyi ve yeni bir giriş dağıtım geçmişiniz oluşturmak, unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7feb0-196">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-hello-production-deployment"></a><span data-ttu-id="7feb0-197">6: hello Üretim dağıtımı değiştirme</span><span class="sxs-lookup"><span data-stu-id="7feb0-197">6: Change hello Production deployment</span></span>
<span data-ttu-id="7feb0-198">Bu adım yalnızca toocloud Hizmetleri, web uygulamaları geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="7feb0-198">This step applies only toocloud services, not web apps.</span></span> <span data-ttu-id="7feb0-199">Hazır olduğunuzda hello seçerek hello hazırlama ortamı toohello üretim ortamını yükseltebilirsiniz **takas** hello Klasik Azure portalı düğmesini.</span><span class="sxs-lookup"><span data-stu-id="7feb0-199">When you are ready, you can promote hello Staging environment toohello production environment by choosing hello **Swap** button in hello Azure classic portal.</span></span> <span data-ttu-id="7feb0-200">Yeni dağıtılan hello hazırlama ortamıdır yükseltilen tooProduction ve hello önceki üretim ortamında, varsa, bir hazırlama ortamını olur.</span><span class="sxs-lookup"><span data-stu-id="7feb0-200">hello newly deployed Staging environment is promoted tooProduction, and hello previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="7feb0-201">Hello etkin dağıtım hello üretim ve hazırlama ortamları için farklı olabilir, ancak son yapılar hello dağıtım geçmişini olduğu hello aynı ne olursa olsun, ortam.</span><span class="sxs-lookup"><span data-stu-id="7feb0-201">hello Active deployment may be different for hello Production and Staging environments, but hello deployment history of recent builds is hello same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="7feb0-202">7: birim testleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7feb0-202">7: Run unit tests</span></span>
<span data-ttu-id="7feb0-203">Bu adım, bulut Hizmetleri yalnızca tooweb uygulamaları geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="7feb0-203">This step applies only tooweb apps, not cloud services.</span></span> <span data-ttu-id="7feb0-204">dağıtımınızdaki kalite kapısı tooput, birim testleri çalıştırabilirsiniz ve başarısız olursa hello dağıtım durdurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7feb0-204">tooput a quality gate on your deployment, you can run unit tests and if they fail, you can stop hello deployment.</span></span>

1. <span data-ttu-id="7feb0-205">Visual Studio'da birim testi projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7feb0-205">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="7feb0-206">Proje başvuruları toohello proje tootest istediğiniz ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7feb0-206">Add project references toohello project you want tootest.</span></span>
   
   ![][40]
3. <span data-ttu-id="7feb0-207">Bazı birim testleri ekleme.</span><span class="sxs-lookup"><span data-stu-id="7feb0-207">Add some unit tests.</span></span> <span data-ttu-id="7feb0-208">tooget başlatıldı, her zaman geçirir kukla bir test deneyin.</span><span class="sxs-lookup"><span data-stu-id="7feb0-208">tooget started, try a dummy test that will always pass.</span></span>
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. <span data-ttu-id="7feb0-209">Merhaba derleme tanımı düzenleme, hello seçin **işlem** sekmesini tıklatın ve hello genişletin **Test** düğümü.</span><span class="sxs-lookup"><span data-stu-id="7feb0-209">Edit hello build definition, choose hello **Process** tab, and expand hello **Test** node.</span></span>
5. <span data-ttu-id="7feb0-210">Set hello **başarısız yapı test hatasında** tooTrue.</span><span class="sxs-lookup"><span data-stu-id="7feb0-210">Set hello **Fail build on test failure** tooTrue.</span></span> <span data-ttu-id="7feb0-211">Bu, hello testleri geçilir sürece hello dağıtım karşılaşılmaz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7feb0-211">This means that hello deployment won't occur unless hello tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="7feb0-212">Yeni bir derleme sırası.</span><span class="sxs-lookup"><span data-stu-id="7feb0-212">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="7feb0-213">Merhaba derleme devam ederken üzerinde ilerleme durumunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7feb0-213">While hello build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="7feb0-214">Merhaba yapı yapıldığında hello test sonuçlarını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7feb0-214">When hello build is done, check hello test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="7feb0-215">Başarısız olacak bir test oluşturmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="7feb0-215">Try creating a test that will fail.</span></span> <span data-ttu-id="7feb0-216">Yeni bir test hello kopyalayarak birinci eklemek, yeniden adlandırın ve beklenen bir özel durum NotImplementedException olduğunu bildiren kod hello satırını açıklama.</span><span class="sxs-lookup"><span data-stu-id="7feb0-216">Add a new test by copying hello first one, rename it, and comment out hello line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="7feb0-217">Merhaba iade tooqueue yeni bir yapı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7feb0-217">Check in hello change tooqueue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="7feb0-218">Merhaba test sonuçları toosee hello hata ayrıntılarını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="7feb0-218">View hello test results toosee details about hello failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="7feb0-219">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7feb0-219">Next steps</span></span>
<span data-ttu-id="7feb0-220">Birim testi Visual Studio Team Services içinde hakkında daha fazla bilgi için bkz: [birim testleri, derlemede çalıştırılan](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span><span class="sxs-lookup"><span data-stu-id="7feb0-220">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="7feb0-221">Git kullanıyorsanız, bkz: [Git kodunuzda paylaşmak](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) ve [sürekli dağıtım tooAzure uygulama hizmeti](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="7feb0-221">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="7feb0-222">Visual Studio Team Services hakkında daha fazla bilgi için bkz: [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="7feb0-222">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
