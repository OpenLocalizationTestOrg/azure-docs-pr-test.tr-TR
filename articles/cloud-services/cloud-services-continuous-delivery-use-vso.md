---
title: "Visual Studio Team Services içinde Azure ile sürekli teslim | Microsoft Docs"
description: "Otomatik olarak oluşturmak ve Web uygulaması özellikle Azure uygulama hizmeti veya Bulut hizmetlerini dağıtmak için Visual Studio Team Services takım projeleriniz yapılandırmayı öğrenin."
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
ms.openlocfilehash: d80ce63eb7ddfd7c45726be887a772f9a7594b28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services"></a><span data-ttu-id="eef94-103">Visual Studio Team Services'ı kullanarak Azure'a sürekli teslim</span><span class="sxs-lookup"><span data-stu-id="eef94-103">Continuous delivery to Azure using Visual Studio Team Services</span></span>
<span data-ttu-id="eef94-104">Otomatik olarak oluşturabilir ve Azure web uygulamaları dağıtma veya Bulut Hizmetleri için Visual Studio Team Services takım projeleriniz yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eef94-104">You can configure your Visual Studio Team Services team projects to automatically build and deploy to Azure web apps or cloud services.</span></span>  <span data-ttu-id="eef94-105">(Sürekli bir yapı ayarlayın ve sistem kullanarak dağıtma hakkında bilgi için bir *şirket içi* Team Foundation Server, bkz: [Azure bulut Hizmetleri için devamlı teslim](cloud-services-dotnet-continuous-delivery.md).)</span><span class="sxs-lookup"><span data-stu-id="eef94-105">(For information on how to set up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="eef94-106">Bu öğreticide Visual Studio 2013 ve Azure SDK'ın yüklü olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="eef94-106">This tutorial assumes you have Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="eef94-107">Visual Studio 2013 yoksa seçerek karşıdan **ücretsiz olarak başlayın** adresindeki bağlantı [www.visualstudio.com](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="eef94-107">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="eef94-108">Azure SDK yüklemek [burada](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="eef94-108">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="eef94-109">Bu öğreticiyi tamamlamak için bir Visual Studio Team Services hesabınızın olması gerekir: yapabilecekleriniz [ücretsiz bir Visual Studio Team Services hesabı açabilirsiniz](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="eef94-109">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="eef94-110">Otomatik olarak oluşturmak ve Visual Studio Team Services kullanarak Azure'a dağıtmak için bir bulut hizmeti ayarlamak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="eef94-110">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="eef94-111">1: takım projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="eef94-111">1: Create a team project</span></span>
<span data-ttu-id="eef94-112">Yönergeleri izleyerek [burada](http://go.microsoft.com/fwlink/?LinkId=512980) takım projesi oluşturmak ve Visual Studio bağlamak için.</span><span class="sxs-lookup"><span data-stu-id="eef94-112">Follow the instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) to create your team project and link it to Visual Studio.</span></span> <span data-ttu-id="eef94-113">Bu kılavuz, kaynak denetim çözümü Team Foundation sürüm denetimi (TFVC'yi) kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="eef94-113">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="eef94-114">Git sürüm denetimi için kullanmak istiyorsanız, bkz: [bu kılavuzun Git sürüm](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span><span class="sxs-lookup"><span data-stu-id="eef94-114">If you want to use Git for version control, see [the Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-to-source-control"></a><span data-ttu-id="eef94-115">2: kaynak denetimi projesindeki denetleyin</span><span class="sxs-lookup"><span data-stu-id="eef94-115">2: Check in a project to source control</span></span>
1. <span data-ttu-id="eef94-116">Visual Studio'da, dağıtmak istediğiniz çözümü açın veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eef94-116">In Visual Studio, open the solution you want to deploy, or create a new one.</span></span>
   <span data-ttu-id="eef94-117">Bu izlenecek adımları izleyerek bir web uygulaması veya bir bulut hizmeti (Azure uygulaması) dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eef94-117">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span>
   <span data-ttu-id="eef94-118">Yeni bir çözüm oluşturmak istiyorsanız, yeni bir Azure bulut hizmeti projesi ya da yeni bir ASP.NET MVC projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eef94-118">If you want to create a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="eef94-119">Proje .NET Framework 4 veya 4.5 hedefler emin olun ve bir bulut hizmeti projesini oluşturuyorsanız, bir ASP.NET MVC web rolü ve çalışan rolü eklemek ve Internet uygulamasını web rolü seçin.</span><span class="sxs-lookup"><span data-stu-id="eef94-119">Make sure that the project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for the web role.</span></span> <span data-ttu-id="eef94-120">İstendiğinde, seçin **Internet uygulama**.</span><span class="sxs-lookup"><span data-stu-id="eef94-120">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="eef94-121">Bir web uygulaması oluşturmak istiyorsanız, ASP.NET Web uygulaması proje şablonunu seçin ve ardından MVC seçin.</span><span class="sxs-lookup"><span data-stu-id="eef94-121">If you want to create a web app, choose the ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="eef94-122">Bkz: [Azure App Service'te bir ASP.NET web uygulaması oluşturma](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="eef94-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="eef94-123">Visual Studio Team Services, şu anda yalnızca Visual Studio Web uygulamalarının CI dağıtımları destekler.</span><span class="sxs-lookup"><span data-stu-id="eef94-123">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="eef94-124">Web sitesi projeleri kapsamının dışında ' dir.</span><span class="sxs-lookup"><span data-stu-id="eef94-124">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="eef94-125">Çözüm için bağlam menüsünü açın ve seçin **kaynak denetimine Çözüm Ekle**.</span><span class="sxs-lookup"><span data-stu-id="eef94-125">Open the context menu for the solution, and choose **Add Solution to Source Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="eef94-126">Kabul etmek veya varsayılanları değiştirmek ve seçin **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eef94-126">Accept or change the defaults and choose the **OK** button.</span></span> <span data-ttu-id="eef94-127">İşlem tamamlandıktan sonra kaynak denetim simgelerini görünür **Çözüm Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="eef94-127">Once the process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="eef94-128">Çözüm için kısayol menüsünü açın ve seçin **iade**.</span><span class="sxs-lookup"><span data-stu-id="eef94-128">Open the shortcut menu for the solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="eef94-129">İçinde **bekleyen değişiklikleri** alanı **Takım Gezgini**iade için bir açıklama yazın ve seçin **iade** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eef94-129">In the **Pending Changes** area of **Team Explorer**, type a comment for the check-in and choose the **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="eef94-130">Dahil etmek veya belirli değişiklikler, iade ettiğinizde hariç seçenekleri not edin.</span><span class="sxs-lookup"><span data-stu-id="eef94-130">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="eef94-131">Değişiklikleri dışlanır isterseniz seçin **dahil tüm** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="eef94-131">If desired changes are excluded, choose the **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="eef94-132">3: Proje için Azure connect</span><span class="sxs-lookup"><span data-stu-id="eef94-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="eef94-133">Bazı kaynak kodu ile VS Team Services takım projesi içine sahip olduğunuza göre takım projenize Azure'a bağlanmak hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="eef94-133">Now that you have a VS Team Services team project with some source code in it, you are ready to connect your team project to Azure.</span></span>  <span data-ttu-id="eef94-134">İçinde [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), bulut hizmeti veya web uygulamanızı seçin veya seçerek yeni bir tane oluşturun  **+**  simgesini seçerek ve sol alt **bulut hizmeti**veya **Web uygulaması** ve ardından **hızlı Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="eef94-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the **+** icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="eef94-135">Seçin **Visual Studio Team Services ile yayımlamayı ayarlayın** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="eef94-135">Choose the **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="eef94-136">Sihirbazı'nda tıklatın ve metin kutusuna, Visual Studio Team Services hesabınızın adını yazın **şimdi Yetkilendir** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="eef94-136">In the wizard, type the name of your Visual Studio Team Services account in the textbox and click the **Authorize Now** link.</span></span> <span data-ttu-id="eef94-137">Oturum açmak için istenebilir.</span><span class="sxs-lookup"><span data-stu-id="eef94-137">You might be asked to sign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="eef94-138">İçinde **bağlantı isteği** açılan iletişim kutusunda, seçin **kabul** VS Team Services içinde takım projenizin yapılandırmak için Azure yetkilendirmek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eef94-138">In the **Connection Request** pop-up dialog, choose the **Accept** button to authorize Azure to configure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="eef94-139">Yetkilendirme başarılı olduğunda, Visual Studio Team Services takım projelerinin listesini içeren bir açılır bakın.</span><span class="sxs-lookup"><span data-stu-id="eef94-139">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="eef94-140">Önceki adımlarda oluşturduğunuz takım projesi adını seçin ve ardından sihirbazın onay düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="eef94-140">Choose  the name of team project that you created in the previous steps, and then choose the wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="eef94-141">Projenizi bağlandıktan sonra Visual Studio Team Services takım projenize değişiklikleri denetlemek için bazı yönergeler görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="eef94-141">After your project is linked, you will see some instructions for checking in changes to your Visual Studio Team Services team project.</span></span>  <span data-ttu-id="eef94-142">Sonraki iade, Visual Studio Team Services oluşturup projenize Azure'a dağıtacak.</span><span class="sxs-lookup"><span data-stu-id="eef94-142">On your next check-in, Visual Studio Team Services will build and deploy your project to Azure.</span></span>  <span data-ttu-id="eef94-143">Bu artık tıklayarak deneyin **Visual Studio'dan iade** bağlantı ve ardından **başlatma Visual Studio** bağlantı (veya eşdeğer **Visual Studio** alt kısmındaki düğmesi Portal ekran).</span><span class="sxs-lookup"><span data-stu-id="eef94-143">Try this now by clicking the **Check In from Visual Studio** link, and then the **Launch Visual Studio** link (or the equivalent **Visual Studio** button at the bottom of the portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="eef94-144">4: yeniden tetikleyebilir ve projenizi yeniden dağıtmak</span><span class="sxs-lookup"><span data-stu-id="eef94-144">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="eef94-145">Visual Studio'nun içinde **Takım Gezgini**, seçin **Kaynak Denetim Gezgini** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="eef94-145">In Visual Studio's **Team Explorer**, choose the **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="eef94-146">Çözüm dosyasına gidin ve açın.</span><span class="sxs-lookup"><span data-stu-id="eef94-146">Navigate to your solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="eef94-147">İçinde **Çözüm Gezgini**, bir dosyasını açın ve değiştirin.</span><span class="sxs-lookup"><span data-stu-id="eef94-147">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="eef94-148">Örneğin, dosyayı değiştirmek `_Layout.cshtml` görünümleri altında\\paylaşılan klasöründe bir MVC web rolü.</span><span class="sxs-lookup"><span data-stu-id="eef94-148">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="eef94-149">Site için logo düzenleyin ve seçin **Ctrl + S** dosyayı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="eef94-149">Edit the logo for the site and choose **Ctrl+S** to save the file.</span></span>
   
    ![][18]
5. <span data-ttu-id="eef94-150">İçinde **Takım Gezgini**, seçin **bekleyen değişiklikleri** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="eef94-150">In **Team Explorer**, choose the **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="eef94-151">Bir açıklama girin ve ardından **iade** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eef94-151">Enter a comment and then choose the **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="eef94-152">Seçin **ev** geri dönmek için düğmesini **Takım Gezgini** giriş sayfası.</span><span class="sxs-lookup"><span data-stu-id="eef94-152">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="eef94-153">Seçin **derlemeler** ediyor yapıları görüntülemek için bağlantı.</span><span class="sxs-lookup"><span data-stu-id="eef94-153">Choose the **Builds** link to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="eef94-154">**Takım Gezgini** bir yapı için iade tetiklenen gösterir.</span><span class="sxs-lookup"><span data-stu-id="eef94-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="eef94-155">Yapı Yapılandırma sürerken ayrıntılı bir günlüğünü görüntülemek için devam eden adına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eef94-155">Double-click the name of the build in progress to view a detailed log as the build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="eef94-156">Derleme Sürüyor olsa da, Sihirbazı'nı kullanarak TFS Azure'a bağlandığında, oluşturulan derleme tanımını göz atın.</span><span class="sxs-lookup"><span data-stu-id="eef94-156">While the build is in-progress, take a look at the build definition that was created when you linked TFS to Azure by using the wizard.</span></span>  <span data-ttu-id="eef94-157">Derleme tanımı için kısayol menüsünü açın ve seçin **derleme tanımını Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="eef94-157">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="eef94-158">İçinde **tetikleyici** sekmesinde derleme tanımını her iade oluşturmak için varsayılan olarak ayarlandığını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="eef94-158">In the **Trigger** tab, you will see that the build definition is set to build on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="eef94-159">İçinde **işlem** sekmesinde, dağıtım ortamı bulut hizmeti veya web uygulamasının adına ayarlayın görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eef94-159">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span> <span data-ttu-id="eef94-160">Web uygulamaları ile çalışıyorsanız, gördüğünüz özellikleri burada gösterilen olanlardan farklı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="eef94-160">If you are working with web apps, the properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="eef94-161">Varsayılanları farklı değerler istiyorsanız özelliklerinin değerlerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="eef94-161">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="eef94-162">Azure yayımlama özelliklerini bulunan **dağıtım** bölümü.</span><span class="sxs-lookup"><span data-stu-id="eef94-162">The properties for Azure publishing are in the **Deployment** section.</span></span>
    
     <span data-ttu-id="eef94-163">Kullanılabilir özellikler aşağıdaki tabloda gösterilmektedir **dağıtım** bölümü:</span><span class="sxs-lookup"><span data-stu-id="eef94-163">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="eef94-164">Özellik</span><span class="sxs-lookup"><span data-stu-id="eef94-164">Property</span></span> | <span data-ttu-id="eef94-165">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="eef94-165">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="eef94-166">Güvenilmeyen Sertifikalar izin ver</span><span class="sxs-lookup"><span data-stu-id="eef94-166">Allow Untrusted Certificates</span></span> |<span data-ttu-id="eef94-167">SSL sertifikaları yanlışsa, bir kök yetkilisi tarafından imzalanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eef94-167">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="eef94-168">Yükseltme izin ver</span><span class="sxs-lookup"><span data-stu-id="eef94-168">Allow Upgrade</span></span> |<span data-ttu-id="eef94-169">Yeni bir tane oluşturmak yerine var olan bir dağıtıma güncelleştirmek dağıtım sağlar.</span><span class="sxs-lookup"><span data-stu-id="eef94-169">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="eef94-170">IP adresi korur.</span><span class="sxs-lookup"><span data-stu-id="eef94-170">Preserves the IP address.</span></span> |
    | <span data-ttu-id="eef94-171">Silmeyin</span><span class="sxs-lookup"><span data-stu-id="eef94-171">Do Not Delete</span></span> |<span data-ttu-id="eef94-172">TRUE ise, var olan bir ilgisiz dağıtımını üzerine yazma (yükseltme izin verilir).</span><span class="sxs-lookup"><span data-stu-id="eef94-172">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="eef94-173">Dağıtım ayarları yolu</span><span class="sxs-lookup"><span data-stu-id="eef94-173">Path to Deployment Settings</span></span> |<span data-ttu-id="eef94-174">Depo kök klasörüne göreli bir web uygulaması için .pubxml dosyanızın yolu.</span><span class="sxs-lookup"><span data-stu-id="eef94-174">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="eef94-175">Bulut Hizmetleri için yoksayıldı.</span><span class="sxs-lookup"><span data-stu-id="eef94-175">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="eef94-176">SharePoint dağıtım ortamı</span><span class="sxs-lookup"><span data-stu-id="eef94-176">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="eef94-177">Aynı hizmet adı.</span><span class="sxs-lookup"><span data-stu-id="eef94-177">The same as the service name.</span></span> |
    | <span data-ttu-id="eef94-178">Azure dağıtım ortamı</span><span class="sxs-lookup"><span data-stu-id="eef94-178">Azure Deployment Environment</span></span> |<span data-ttu-id="eef94-179">Web uygulaması veya Bulut hizmeti adı.</span><span class="sxs-lookup"><span data-stu-id="eef94-179">The web app or cloud service name.</span></span> |
12. <span data-ttu-id="eef94-180">Birden fazla hizmet yapılandırma (.cscfg dosyaları) kullanıyorsanız, istenen hizmet yapılandırmasında belirtebilirsiniz **MSBuild bağımsız değişkenleri Gelişmiş, yapı** ayarı.</span><span class="sxs-lookup"><span data-stu-id="eef94-180">If you are using multiple service configurations (.cscfg files), you can specify the desired service configuration in the **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="eef94-181">Örneğin, ServiceConfiguration.Test.cscfg kullanmak için çizgi seçenek MSBuild bağımsız değişkenleri ayarlayın `/p:TargetProfile=Test`.</span><span class="sxs-lookup"><span data-stu-id="eef94-181">For example, to use ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="eef94-182">Bu zamana kadar yapınızın başarıyla tamamlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eef94-182">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="eef94-183">Derleme adına çift tıklayın, Visual Studio gösterir. bir **Yapı Özeti**, tüm test sonuçlarını da dahil olmak üzere, birim testi projelerini ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="eef94-183">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="eef94-184">İçinde [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), ilişkili dağıtım görüntüleyebilirsiniz **dağıtımları** hazırlık ortamı seçildiğinde sekme.</span><span class="sxs-lookup"><span data-stu-id="eef94-184">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="eef94-185">Sitenizin URL'ye gidin.</span><span class="sxs-lookup"><span data-stu-id="eef94-185">Browse to your site's URL.</span></span> <span data-ttu-id="eef94-186">Bir web uygulaması için tıklatmanız **Gözat** komut çubuğundan düğme.</span><span class="sxs-lookup"><span data-stu-id="eef94-186">For a web app, just click the **Browse** button on the command bar.</span></span> <span data-ttu-id="eef94-187">Bir bulut hizmeti için URL seçin **Hızlı Bakış** bölümünü **Pano** bir bulut hizmeti için hazırlama ortamını gösteren sayfası.</span><span class="sxs-lookup"><span data-stu-id="eef94-187">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment for a cloud service.</span></span> <span data-ttu-id="eef94-188">Bulut Hizmetleri için sürekli tümleştirme dağıtımlarından hazırlama ortamına varsayılan olarak yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="eef94-188">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="eef94-189">Bu ayarı değiştirebilirsiniz **alternatif bir bulut hizmeti ortamını** özelliğine **üretim**.</span><span class="sxs-lookup"><span data-stu-id="eef94-189">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="eef94-190">Bu ekran, site URL'si bulut hizmetin panosu sayfasında nerede olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="eef94-190">This screenshot shows where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="eef94-191">Çalışan sitenizi ortaya çıkarmak için yeni bir tarayıcı sekmesi açar.</span><span class="sxs-lookup"><span data-stu-id="eef94-191">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="eef94-192">Bulut Hizmetleri için projenize başka değişiklikler yapmak isterseniz, tetikleyici daha oluşturur ve birden çok dağıtım toplanacaktır.</span><span class="sxs-lookup"><span data-stu-id="eef94-192">For cloud services, if you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="eef94-193">En son etkin olarak işaretlenmiş.</span><span class="sxs-lookup"><span data-stu-id="eef94-193">The latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="eef94-194">5: önceki bir yapı yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="eef94-194">5: Redeploy an earlier build</span></span>
<span data-ttu-id="eef94-195">Bu adım isteğe bağlıdır ve bulut Hizmetleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="eef94-195">This step applies to cloud services and is optional.</span></span> <span data-ttu-id="eef94-196">Azure Klasik portalında, önceki bir dağıtıma seçin ve ardından **dağıtmanız** önceki bir iade sitenize geri sarma düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eef94-196">In the Azure classic portal, choose an earlier deployment and then choose the **Redeploy** button to rewind your site to an earlier check-in.</span></span>  <span data-ttu-id="eef94-197">Bu TFS'de yeni bir derlemeyi tetiklemeyi ve yeni bir giriş dağıtım geçmişiniz oluşturmak, unutmayın.</span><span class="sxs-lookup"><span data-stu-id="eef94-197">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="eef94-198">6: Üretim dağıtımı değiştirme</span><span class="sxs-lookup"><span data-stu-id="eef94-198">6: Change the Production deployment</span></span>
<span data-ttu-id="eef94-199">Bu adım yalnızca bulut Hizmetleri için web uygulamaları geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="eef94-199">This step applies only to cloud services, not web apps.</span></span> <span data-ttu-id="eef94-200">Hazır olduğunuzda belirleyerek üretim ortamına hazırlama ortamını yükseltebilirsiniz **takas** Klasik Azure portalındaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eef94-200">When you are ready, you can promote the Staging environment to the production environment by choosing the **Swap** button in the Azure classic portal.</span></span> <span data-ttu-id="eef94-201">Yeni dağıtılan hazırlama ortamını üretime yükseltilir ve önceki üretim ortamında, varsa, bir hazırlama ortamını olur.</span><span class="sxs-lookup"><span data-stu-id="eef94-201">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="eef94-202">Etkin dağıtım üretim ve hazırlık ortamları için farklı olabilir, ancak son yapılar dağıtım geçmişini ortamı bakılmaksızın aynı olacak.</span><span class="sxs-lookup"><span data-stu-id="eef94-202">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="eef94-203">7: birim testleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="eef94-203">7: Run unit tests</span></span>
<span data-ttu-id="eef94-204">Bu adım yalnızca web uygulamaları, bulut olmayan hizmetleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="eef94-204">This step applies only to web apps, not cloud services.</span></span> <span data-ttu-id="eef94-205">Kalite kapısı dağıtımınızı üzerinde koymak için birim testleri çalıştırabilirsiniz ve başarısız olursa, dağıtım durdurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eef94-205">To put a quality gate on your deployment, you can run unit tests and if they fail, you can stop the deployment.</span></span>

1. <span data-ttu-id="eef94-206">Visual Studio'da birim testi projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="eef94-206">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="eef94-207">Proje başvurularını test etmek istediğiniz projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="eef94-207">Add project references to the project you want to test.</span></span>
   
   ![][40]
3. <span data-ttu-id="eef94-208">Bazı birim testleri ekleme.</span><span class="sxs-lookup"><span data-stu-id="eef94-208">Add some unit tests.</span></span> <span data-ttu-id="eef94-209">Başlamak için her zaman geçirir kukla bir test deneyin.</span><span class="sxs-lookup"><span data-stu-id="eef94-209">To get started, try a dummy test that will always pass.</span></span>
   
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
4. <span data-ttu-id="eef94-210">Yapı tanımı düzenleme, seçin **işlem** sekmesini tıklatın ve genişletin **Test** düğümü.</span><span class="sxs-lookup"><span data-stu-id="eef94-210">Edit the build definition, choose the **Process** tab, and expand the **Test** node.</span></span>
5. <span data-ttu-id="eef94-211">Ayarlama **başarısız yapı test hatasında** true.</span><span class="sxs-lookup"><span data-stu-id="eef94-211">Set the **Fail build on test failure** to True.</span></span> <span data-ttu-id="eef94-212">Bu testleri geçirmezseniz dağıtım karşılaşılmaz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="eef94-212">This means that the deployment won't occur unless the tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="eef94-213">Yeni bir derleme sırası.</span><span class="sxs-lookup"><span data-stu-id="eef94-213">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="eef94-214">Derleme devam ederken üzerinde ilerleme durumunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="eef94-214">While the build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="eef94-215">Yapı işiniz bittiğinde, test sonuçlarını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="eef94-215">When the build is done, check the test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="eef94-216">Başarısız olacak bir test oluşturmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="eef94-216">Try creating a test that will fail.</span></span> <span data-ttu-id="eef94-217">Birinci kopyalayarak yeni bir test eklemek, yeniden adlandırın ve beklenen bir özel durum NotImplementedException olduğunu bildiren kod satırını açıklama.</span><span class="sxs-lookup"><span data-stu-id="eef94-217">Add a new test by copying the first one, rename it, and comment out the line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="eef94-218">Yeni bir yapıyı sıraya değişiklik denetleyin.</span><span class="sxs-lookup"><span data-stu-id="eef94-218">Check in the change to queue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="eef94-219">Hata ayrıntılarını görmek için test sonuçlarını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="eef94-219">View the test results to see details about the failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="eef94-220">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eef94-220">Next steps</span></span>
<span data-ttu-id="eef94-221">Birim testi Visual Studio Team Services içinde hakkında daha fazla bilgi için bkz: [birim testleri, derlemede çalıştırılan](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span><span class="sxs-lookup"><span data-stu-id="eef94-221">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="eef94-222">Git kullanıyorsanız, bkz: [Git kodunuzda paylaşmak](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) ve [Azure App Service için sürekli dağıtım](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="eef94-222">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="eef94-223">Visual Studio Team Services hakkında daha fazla bilgi için bkz: [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="eef94-223">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

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
