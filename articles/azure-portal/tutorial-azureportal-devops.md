---
title: "Eğitmen: Azure Portal ile DevOps | Microsoft Belgeleri"
description: "Azure Portal'daki çeşitli DevOps iş akışları hakkında bilgi edinin."
services: azure-portal
documentationcenter: 
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: eec7d1402bdea4e5433c473dd713eed23aa80464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-devops-with-the-azure-portal"></a><span data-ttu-id="e00ae-103">Öğretici: Azure Portal ile DevOps</span><span class="sxs-lookup"><span data-stu-id="e00ae-103">Tutorial: DevOps with the Azure Portal</span></span>
<span data-ttu-id="e00ae-104">Azure platformu esnek DevOps iş akışları ile doludur.</span><span class="sxs-lookup"><span data-stu-id="e00ae-104">The Azure platform is full of flexible DevOps workflows.</span></span> <span data-ttu-id="e00ae-105">Bu öğreticide Azure Portal’ın çalışan uygulamalar geliştirme, test etme, dağıtma, sorun giderme, izleme ve yönetme özelliklerinden nasıl yararlandığını öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-105">In this tutorial, you learn how to leverage the capabilities of the Azure Portal to develop, test, deploy, troubleshoot, monitor, and manage running applications.</span></span> <span data-ttu-id="e00ae-106">Bu öğretici aşağıdakilere odaklanır:</span><span class="sxs-lookup"><span data-stu-id="e00ae-106">This tutorial focuses on the following:</span></span>

1. <span data-ttu-id="e00ae-107">Bir web uygulaması oluşturma ve sürekli dağıtımı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="e00ae-107">Creating a web app and enabling continuous deployment</span></span>
2. <span data-ttu-id="e00ae-108">Uygulama geliştirme ve test etme</span><span class="sxs-lookup"><span data-stu-id="e00ae-108">Develop and test an app</span></span>
3. <span data-ttu-id="e00ae-109">Bir uygulamayı izleme ve sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="e00ae-109">Monitoring and Troubleshooting an app</span></span>
4. <span data-ttu-id="e00ae-110">Genel uygulama yönetimi görevleri</span><span class="sxs-lookup"><span data-stu-id="e00ae-110">General application management tasks</span></span>

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a><span data-ttu-id="e00ae-111">Bir web uygulaması oluşturma ve sürekli dağıtımı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="e00ae-111">Creating a web app and enabling continuous deployment</span></span>
<span data-ttu-id="e00ae-112">[Azure Uygulama Hizmeti](https://azure.microsoft.com/services/app-service/) ile bu öğreticinin geri kalanında kullanacağınız bir web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e00ae-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in the rest of this tutorial.</span></span> <span data-ttu-id="e00ae-113">Başlangıçta kaynak kod deponuzdan çalışan Azure ortamımıza sürekli dağıtımı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-113">You’ll initially enable continuous deployment from your source code repository into our running Azure environment.</span></span>

1. <span data-ttu-id="e00ae-114">Azure Portal’da oturum açın</span><span class="sxs-lookup"><span data-stu-id="e00ae-114">Sign into the Azure Portal</span></span>
2. <span data-ttu-id="e00ae-115">**Uygulama Hizmetleri** &gt; **Simge ekle** seçeneğini belirleyin ve bir ad girin, aboneliğinizi seçin ve hizmetin kapsayıcısı olarak görev yapacak yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e00ae-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group to serve as the container for the service.</span></span>
   
   <span data-ttu-id="e00ae-116">Kaynak grupları, [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) aracılığıyla çözümün faturalama, dağıtım ve izleme gibi çeşitli bölümlerini tek bir grupta yönetmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e00ae-116">Resource groups allow you to manage various aspects of the solution such as billing, deployments and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>
   
   ![image1][image1]
3. <span data-ttu-id="e00ae-118">Birkaç dakika sonra uygulama hizmetiniz oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e00ae-118">After a few moments, your app service is created.</span></span> <span data-ttu-id="e00ae-119">Portalda hizmete ilişkin çeşitli menü seçeneklerini keşfetmek için birkaç dakikanızı ayırın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-119">Take a few minutes to explore the various menu options for the service in the portal.</span></span>
   
   ![image2][image2]    
4. <span data-ttu-id="e00ae-121">URL’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-121">Click the URL.</span></span> <span data-ttu-id="e00ae-122">Havuzlar ve depolara yönelik çeşitli mevcut seçeneklere dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-122">Notice the variety of available choices for tools and repositories.</span></span> <span data-ttu-id="e00ae-123">Ayrıca .NET, Java ve Ruby gibi seçtiğiniz dilleri ve çerçeveleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-123">You can also use the languages and frameworks of your choice including .NET, Java, and Ruby.</span></span>
   
   ![image3][image3]    
5. <span data-ttu-id="e00ae-125">Azure portalı sürekli dağıtımı yalnızca birkaç basit adımdan oluşan kolay bir işlem haline getirir.</span><span class="sxs-lookup"><span data-stu-id="e00ae-125">The Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span></span> <span data-ttu-id="e00ae-126">Azure portalında az önce oluşturduğunuz uygulama hizmetine ait simgeden ayarları seçin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-126">In the Azure portal, choose settings from the icon for the app service you just created.</span></span>
   
   ![image4][image4]
   
   <span data-ttu-id="e00ae-128">Sağ tarafta açılan dikey pencereden yayımlama bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-128">From the blade that opens on the right, scroll to the publishing section.</span></span>
   
   ![image5][image5]
6. <span data-ttu-id="e00ae-130">Ardından, uygulamanın sürekli dağıtımını etkinleştirmek için bazı ayarları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-130">Next, configure some settings to enable continuous deployment for the app.</span></span> <span data-ttu-id="e00ae-131">Dağıtım Kaynağı’na ve ardından Kaynak Seç’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-131">Click Deployment Source and then click Choose Source.</span></span> <span data-ttu-id="e00ae-132">Depo kaynakları için sahip olduğunuz çeşitli seçeneklere dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-132">Notice the variety of options you have for repository sources.</span></span>
   
   ![image6][image6]
7. <span data-ttu-id="e00ae-134">Bu örnek için GitHub'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-134">For this example choose GitHub.</span></span> <span data-ttu-id="e00ae-135">İsteğe bağlı olarak, tercih ettiğiniz depoyu seçin ve yetkilendirme kimlik bilgilerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-135">Optionally choose the repository of your choice and setup the authorization credentials.</span></span>
   
   ![image7][image7]
8. <span data-ttu-id="e00ae-137">Deponuzda yetkilendirme yaptıktan sonra dağıtmak istediğiniz bir projeyi ve dalı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-137">After authorization to your repository, you can then choose a project and branch you wish to deploy.</span></span> <span data-ttu-id="e00ae-138">Aşağıda birkaç hayali örnek listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="e00ae-138">There are several fictitious sample examples listed below.</span></span>
   
   ![image8][image8]
9. <span data-ttu-id="e00ae-140">Projenizi ve dalınızı seçtikten sonra Tamam'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-140">Once you choose your project and branch, click ok.</span></span> <span data-ttu-id="e00ae-141">Bir dağıtımın bildirimlerini görmeye başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e00ae-141">You should start to see notifications of a deployment.</span></span>
   
   ![image9][image9]
10. <span data-ttu-id="e00ae-143">Kaynak denetim deposunu Azure ile tümleştirmek üzere oluşturulan web kancasını görmek için GitHub’a geri gidin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-143">Navigate back to GitHub to see the webhook that was created to integrate the source control repo with Azure.</span></span> <span data-ttu-id="e00ae-144">Azure portalı yalnızca birkaç basit adımda GitHub ile tümleştirme olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e00ae-144">The Azure Portal enables integration with GitHub with only a few simple steps.</span></span>
    
    ![image10][image10]
11. <span data-ttu-id="e00ae-146">Sürekli dağıtımı göstermek için depoya bir miktar içeriği hızlıca ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-146">To demonstrate continuous deployment, you quickly add some content to the repository.</span></span> <span data-ttu-id="e00ae-147">Basit bir örnek için GitHub deposuna örnek bir metin dosyası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-147">For a simple example, add a sample text file to a GitHub repo.</span></span> <span data-ttu-id="e00ae-148">App Service ile .NET, Ruby, Python veya başka bir uygulama türü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-148">You are free to use .NET, Ruby, Python, or some other type of application with App Service.</span></span> <span data-ttu-id="e00ae-149">Tercih ettiğiniz depoya bir metin dosyası, ASP.NET MVC, Java ya da Ruby uygulaması eklemekten çekinmeyin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-149">Feel free to add a text file, ASP.NET MVC, Java, or Ruby application to the repo of your choice.</span></span>
    
    ![image11][image11]
12. <span data-ttu-id="e00ae-151">Değişiklikleri deponuza uyguladıktan sonra portal bildirimleri alanında yeni bir dağıtımın başladığını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-151">After committing changes to your repository, you see a new deployment initiate in the portal notifications area.</span></span> <span data-ttu-id="e00ae-152">Değişiklikleri deponuza uyguladıktan sonra hızlıca görmüyorsanız Eşitle’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-152">Click Sync if you do not quickly see changes after committing to your repository.</span></span>
    
    ![image12][image12]
13. <span data-ttu-id="e00ae-154">Bu noktada uygulama hizmeti için sayfayı yüklemeyi denerseniz bir 403 hatası alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-154">At this point, if you try and load the page for the app service, you may receive a 403 error.</span></span> <span data-ttu-id="e00ae-155">Bu örnekte bunun nedeni index.htm veya default.html dosyası gibi sayfa için tipik bir varsayılan belge ayarı olmamasıdır.</span><span class="sxs-lookup"><span data-stu-id="e00ae-155">In this example, it is because there is no typical default document setup for the page such as a file like index.htm or default.html.</span></span> <span data-ttu-id="e00ae-156">Azure Portal’daki araçlarla bu sorunu hızlıca çözebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-156">You can quickly remedy this with the tooling in the Azure Portal.</span></span>  <span data-ttu-id="e00ae-157">Azure Portal’da Ayarlar &gt; Uygulama Ayarları’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-157">In the Azure Portal choose Settings &gt; Application Settings.</span></span>
    
     ![image13][image13]
14. <span data-ttu-id="e00ae-159">Uygulama ayarları için bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="e00ae-159">A blade opens for application settings.</span></span> <span data-ttu-id="e00ae-160">“SamplePage.html” sayfasının adını girin ve Kaydet’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-160">Enter the name of the page “SamplePage.html” and click Save.</span></span> <span data-ttu-id="e00ae-161">Birkaç dakika boyunca diğer ayarları keşfedin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-161">Take a few minutes to explore the other settings.</span></span>
    
    ![image14][image14]
15. <span data-ttu-id="e00ae-163">Beklenen değişiklikleri gördüğünüzden emin olmak için tarayıcı URL’nizi isteğe bağlı olarak yenileyin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-163">Optionally refresh your browser URL to ensure you see the expected changes.</span></span> <span data-ttu-id="e00ae-164">Bu örnekte, artık sayfayı dolduran bazı basit metinler vardır.</span><span class="sxs-lookup"><span data-stu-id="e00ae-164">In this case, there is some simple text now populating the page.</span></span> <span data-ttu-id="e00ae-165">Depoda yapılan her ek değişiklik yeni bir otomatik dağıtımla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="e00ae-165">Each additional change to the repository would result in a new automatic deployment.</span></span>
    
    ![image15][image15]
    
    <span data-ttu-id="e00ae-167">Azure Portal ile sürekli dağıtımın etkinleştirilmesi kolay bir deneyimdir.</span><span class="sxs-lookup"><span data-stu-id="e00ae-167">Enabling continuous deployment with the Azure Portal is an easy experience.</span></span> <span data-ttu-id="e00ae-168">Ayrıca daha karmaşık yayın işlem hatları oluşturabilir ve otomatik derleme ile yayın yönetimi sistemlerinden yararlanma dahil olmak üzere var olan kaynak denetimi ve Azure’a dağıtılacak sürekli tümleştirme sistemleri ile diğer birçok tekniği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems to deploy to Azure, such as leveraging automated build and release management systems.</span></span>

## <a name="develop-and-test-an-app"></a><span data-ttu-id="e00ae-169">Uygulama geliştirme ve test etme</span><span class="sxs-lookup"><span data-stu-id="e00ae-169">Develop and test an app</span></span>
<span data-ttu-id="e00ae-170">Ardından, kod temelinde bazı değişiklikler yapın ve bu değişiklikleri hızlıca dağıtın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-170">Next, make some changes to the code base and rapidly deploy those changes.</span></span> <span data-ttu-id="e00ae-171">Ayrıca web uygulaması için bazı performans testleri ayarlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e00ae-171">You will also setup up some performance testing for the Web app.</span></span>

1. <span data-ttu-id="e00ae-172">Azure Portal'da gezinti bölmesinden Uygulama Hizmetleri’ni seçin ve App Service’inizi bulun.</span><span class="sxs-lookup"><span data-stu-id="e00ae-172">In the Azure Portal choose App Services from the navigation pane, and locate your App Service.</span></span>
   
   ![image16][image16]
2. <span data-ttu-id="e00ae-174">Araçlar'a tıklayın</span><span class="sxs-lookup"><span data-stu-id="e00ae-174">Click Tools</span></span>
   
   ![image17][image17]
3. <span data-ttu-id="e00ae-176">Araçlar altındaki geliştirme kategorisine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-176">Notice the develop category under Tools.</span></span> <span data-ttu-id="e00ae-177">Burada, Azure Portal’dan çıkmadan uygulamalarla çalışmamıza olanak sağlayan birkaç faydalı araç vardır.</span><span class="sxs-lookup"><span data-stu-id="e00ae-177">There are several useful tools here that allow us to work with apps without leaving the Azure Portal.</span></span> <span data-ttu-id="e00ae-178">Konsol'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-178">Click on Console.</span></span>
   
   ![image18][image18]
4. <span data-ttu-id="e00ae-180">Konsol penceresinde uygulamanız için dinamik komutlar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-180">In the console window, you can issue live commands for your app.</span></span> <span data-ttu-id="e00ae-181">Dir komutunu yazın ve enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-181">Type the dir command and hit enter.</span></span> <span data-ttu-id="e00ae-182">Yükseltilmiş ayrıcalıklar gerektiren komutlar çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-182">Note that commands requiring elevated privileges do not work.</span></span>
   
   ![image19][image19]
5. <span data-ttu-id="e00ae-184">Geliştirme kategorisine geri dönün ve Visual Studio Online’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-184">Move back to the Develop category and choose Visual Studio Online.</span></span> <span data-ttu-id="e00ae-185">Note: Visual Studio Online artık Visual Studio Team Services olarak adlandırılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e00ae-185">Note: Visual Studio Online is now named Visual Studio Team Services.</span></span>
   
   ![image20][image20]
6. <span data-ttu-id="e00ae-187">Uygulamanız için tarayıcı içi düzenleme deneyimini açın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-187">Toggle on the in-browser editing experience for your App.</span></span>
   
   ![image21][image21]
7. <span data-ttu-id="e00ae-189">Uygulamanız için bir web uzantısı yüklenir.</span><span class="sxs-lookup"><span data-stu-id="e00ae-189">A web extension installs for your app.</span></span> <span data-ttu-id="e00ae-190">Uzantılar Azure’daki uygulamalara hızlı ve kolay bir şekilde işlevsellik katar.</span><span class="sxs-lookup"><span data-stu-id="e00ae-190">Extensions quickly and easily add functionality to apps in Azure.</span></span> <span data-ttu-id="e00ae-191">Aşağıdaki ekran görüntüsünde başka uzantı türleri de mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="e00ae-191">Notice some of the other extension types available in the screenshot below.</span></span>
   
   ![image22][image22]
8. <span data-ttu-id="e00ae-193">Visual Studio Online uzantısı yüklendikten sonra Git'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-193">Once the Visual Studio Online extension installs, click Go.</span></span>
   
   ![image23][image23]
9. <span data-ttu-id="e00ae-195">Geliştirme IDE’sini doğrudan tarayıcıda gördüğünüz bir tarayıcı sekmesi açılır.</span><span class="sxs-lookup"><span data-stu-id="e00ae-195">A browser tab opens where you see a development IDE directly in the browser.</span></span> <span data-ttu-id="e00ae-196">Aşağıdaki deneyim Chrome’dadır.</span><span class="sxs-lookup"><span data-stu-id="e00ae-196">Notice the experience below is in Chrome.</span></span>
   
   ![image24][image24]
10. <span data-ttu-id="e00ae-198">Dosya düzenleme, dosya ve klasör ekleme ile canlı siteden içerik indirme gibi birkaç etkinlik gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-198">You can perform several activities such as edit files, add files and folders, and download content from the live site.</span></span> <span data-ttu-id="e00ae-199">SamplePage.html dosyasında hızlı bir düzenleme yapın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-199">Make a quick edit to the SamplePage.html file.</span></span>
    
    ![image25][image25]
11. <span data-ttu-id="e00ae-201">Birkaç dakika içinde değişiklikler otomatik olarak kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="e00ae-201">In a few moments, the changes are automatically saved.</span></span> <span data-ttu-id="e00ae-202">Sayfaya geri dönerseniz değişiklikleri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-202">If you navigate back to the page, you can see the changes.</span></span> <span data-ttu-id="e00ae-203">Bunlar gibi canlı düzenlemeler üretim ortamları için büyük olasılıkla uygun değildir.</span><span class="sxs-lookup"><span data-stu-id="e00ae-203">Keep in mind live edits like these are most likely not suitable for production environments.</span></span> <span data-ttu-id="e00ae-204">Ancak, araçlar geliştirme ve test ortamları için hızlı değişiklikler yapmayı çok kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="e00ae-204">However, the tools make it very easy to make quick changes for dev and test environments.</span></span>
    
    ![image26][image26]
    
    ![image27][image27]
12. <span data-ttu-id="e00ae-207">Araçlar dikey penceresine geri gidin ve Geliştirme kategorisi altında Performans Testi’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-207">Move back to the tools blade and under the Develop category, click on Performance Test.</span></span>
    
    ![image28][image28]
13. <span data-ttu-id="e00ae-209">Bir Team Services hesabı ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e00ae-209">You need to set a team services account.</span></span> <span data-ttu-id="e00ae-210">Daha fazla ayrıntı için buraya bakın: [Team Services Hesabı Oluşturma](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span><span class="sxs-lookup"><span data-stu-id="e00ae-210">See here for more details: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span></span>
14. <span data-ttu-id="e00ae-211">Performans testi oluşturmak için Yeni’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-211">Click on New to create a performance test.</span></span>
    
    ![image29][image29]
    
    <span data-ttu-id="e00ae-213">Çeşitli değerleri yapılandırın ve iletişim kutusunun altındaki Testi Çalıştır’a tıklayarak bir performans testi başlatın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-213">Configure the various values and click Run Test at the bottom of the dialogue to initiate a performance test.</span></span>
    
    ![image30][image30]
    
    ![image31][image31]
15. <span data-ttu-id="e00ae-216">Test çalışmaya başladıktan sonra durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-216">Once the test starts running, you can monitor the state.</span></span>
    
    ![image32][image32]
    
    <span data-ttu-id="e00ae-218">Test tamamlandıktan sonra sonuca tıklandığında daha ayrıntılı bilgi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="e00ae-218">Once the test finishes, clicking on the result shows more details.</span></span>
    
    ![image33][image33]
16. <span data-ttu-id="e00ae-220">Bu örnekte küçük bir test çalışması oluşturdunuz; bu nedenle analiz etmek için sınırlı veri olabilir, ancak çeşitli ölçümleri görebilir ve testinizi bu görünümden yeniden çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-220">In this example, you created a small test run, so there is limited data to analyze, but you can see various metrics as well as rerun your test from this view.</span></span> <span data-ttu-id="e00ae-221">Azure Portal, web performans testleri oluşturmayı, yürütmeyi ve analiz etmeyi kolay bir işlem haline getirir.</span><span class="sxs-lookup"><span data-stu-id="e00ae-221">The Azure Portal makes creating, executing, and analyzing web performance tests an easy process.</span></span> <span data-ttu-id="e00ae-222">Aşağıdaki ekran görüntüleri performans verilerini göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="e00ae-222">The screenshots below display the performance data.</span></span>
    
    ![image34][image34]
    
    ![image35][image35]
    
    ![image36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a><span data-ttu-id="e00ae-226">Bir uygulamayı izleme ve sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="e00ae-226">Monitoring and troubleshooting an app</span></span>
<span data-ttu-id="e00ae-227">Azure, çalışan uygulamaları izleme ve sorunlarını gidermeye yönelik çok sayıda özellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="e00ae-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span></span>

1. <span data-ttu-id="e00ae-228">Azure Portal’da web uygulamamız için Araçlar’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-228">In the Azure Portal for our Web app choose Tools.</span></span>
   
   ![image37][image37]
2. <span data-ttu-id="e00ae-230">Sorun Giderme kategorisi altında çalışan bir uygulamayla ilgili olası sorunları gidermek üzere araç kullanma seçeneklerinin çeşitliliğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-230">Under the Troubleshoot category, notice the various choices for using tools to troubleshoot potential issues with a running app.</span></span> <span data-ttu-id="e00ae-231">Canlı HTTP trafiğini izleme, kendi kendini onarmayı etkinleştirme, günlükleri görüntüleme ve daha fazla işlemi yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span></span>
   
   ![image38][image38]
3. <span data-ttu-id="e00ae-233">Bazı HTTP kodlarına ilişkin hızlı bir bakış için Site Ölçümleri’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-233">Choose Site Metrics to quickly get a view of some HTTP codes.</span></span>
   
   ![image39][image39]
4. <span data-ttu-id="e00ae-235">Hizmet Olarak Tanılama’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-235">Choose Diagnostics as a Service.</span></span> <span data-ttu-id="e00ae-236">Uygulamanızın türünü ve ardından Çalıştır'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-236">Choose your application type, then choose Run.</span></span>
   
   ![image40][image40]
   
   <span data-ttu-id="e00ae-238">Bir koleksiyon başlar.</span><span class="sxs-lookup"><span data-stu-id="e00ae-238">A collection begins.</span></span>
   
   ![image41][image41]
5. <span data-ttu-id="e00ae-240">Olası sorunları tanılamak için uygun günlüğünü seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-240">You may choose the appropriate log to diagnose potential issues.</span></span> <span data-ttu-id="e00ae-241">HTTP Günlükleri gibi tüm kullanılabilir veri seçeneklerini görmek için günlüğe kaydetmeyi etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e00ae-241">You need to enable logging to see all of the available data options such as HTTP Logs.</span></span>
   
   ![image42][image42]
   
   <span data-ttu-id="e00ae-243">Olası sorunları çözmeye yardımcı olmak üzere, Bellek Dökümü dosyasına tıklayarak bir DebugDiag analiz raporu indirip analiz edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-243">By clicking on the Memory Dump file you can download and analyze a DebugDiag analysis report to help find potential issues.</span></span>
   
   ![image43][image43]
6. <span data-ttu-id="e00ae-245">Daha fazla veri görüntülemek için ek günlük kaydını etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e00ae-245">To view more data, you need to enable additional logging.</span></span> <span data-ttu-id="e00ae-246">Azure Portal’da Web uygulamasına gidin ve Ayarlar’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-246">In the Azure Portal, navigate to the Web app and choose Settings.</span></span>
   
   ![image44][image44]
7. <span data-ttu-id="e00ae-248">Özellikler kategorisine inin ve Tanılama günlükleri’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-248">Scroll down to the features category, and choose Diagnostic logs.</span></span>
   
      ![image45][image45]
8. <span data-ttu-id="e00ae-250">Günlük kaydına ilişkin çeşitli seçeneklere dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-250">Notice the various options for logging.</span></span> <span data-ttu-id="e00ae-251">Web sunucusu günlüğünü açın ve Kaydet'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-251">Toggle on Web server logging and click save.</span></span>
   
   ![image46][image46]
9. <span data-ttu-id="e00ae-253">Uygulamanın araçlar alanına geri dönün ve Hizmet olarak tanılama’yı seçip Çalıştır’a tıklayarak veri koleksiyonunu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-253">Move back to the tools area for the app and choose Diagnostics as a service and click Run to rerun the data collection.</span></span>
   
   ![image47][image47]
10. <span data-ttu-id="e00ae-255">HTTP günlüğü ayarı etkin olduğunda bundan böyle HTTP Günlükleri için toplanan verileri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-255">With the HTTP logging setting enabled, you now see data collected for HTTP Logs.</span></span>
    
    ![image48][image48]
11. <span data-ttu-id="e00ae-257">HTML dosya günlüğüne tıklayarak, daha fazla araştırma için zengin bir tarayıcı tabanlı rapor oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-257">By clicking the HTML file log, you produce a rich browser-based report for further investigation.</span></span>
    
    ![image49][image49]
12. <span data-ttu-id="e00ae-259">Azure Portal’da uygulamaya yönelik araçlar bölümüne geri dönün.</span><span class="sxs-lookup"><span data-stu-id="e00ae-259">Move back to the tools section in the Azure Portal for the app.</span></span> <span data-ttu-id="e00ae-260">Araçlar bölümüne gidin ve İşlem Gezgini'ni seçin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-260">Scroll to the Tools section and choose Process Explorer.</span></span>
    
    ![image50][image50]
13. <span data-ttu-id="e00ae-262">İşlem Gezgini'ni seçerek, çalışan işlemlere ilişkin ayrıntıları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-262">By choosing Process Explorer, you can view details about running processes.</span></span> <span data-ttu-id="e00ae-263">Aşağıda işlemlerin ayrıntılarına inebilir ve hatta Azure Portal’dan işlemleri tamamen sonlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-263">Notice below you can drill into processes and even kill processes all from the Azure Portal.</span></span>
    
    ![image51][image51]
    
    ![image52][image52]
14. <span data-ttu-id="e00ae-266">Sol taraftaki Ayarları dikey penceresine geri dönün.</span><span class="sxs-lookup"><span data-stu-id="e00ae-266">Move back to the Settings blade on the left.</span></span> <span data-ttu-id="e00ae-267">Yeni destek isteği’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-267">Click New support request.</span></span>
    
    ![image53][image53]
15. <span data-ttu-id="e00ae-269">Sağdaki dikey pencereden sorunlara ilişkin ayrıntılı bilgileri doldurabilir, iletişim bilgilerini girebilir ve hatta tanılama verilerini karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-269">From the blade on the right, you can fill out details about the issues, enter contact information, and even upload diagnostic data.</span></span> <span data-ttu-id="e00ae-270">Azure Portal, Microsoft desteği ile sorunsuzca çalışmayı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e00ae-270">The Azure Portal enables working with Microsoft support a seamless experience.</span></span>
    
    ![image54][image54]
    
    ![image55][image55]
    
    <span data-ttu-id="e00ae-273">Azure Portal, çalışan uygulamalarımızı izlemeye ve sorunlarını gidermeye yardımcı olmak üzere güçlü ve bilindik araç deneyimleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="e00ae-273">The Azure Portal helps provide powerful and familiar tooling experiences to help monitor and troubleshoot our running applications.</span></span> <span data-ttu-id="e00ae-274">Ayrıca işlemleri geri dönüştürme, çeşitli veri koleksiyonlarını etkinleştirme ve devre dışı bırakma ve hatta Microsoft profesyonel desteği ile tümleştirme gibi görevleri gerçekleştirerek hızlıca önlem alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-274">You are also able to take action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span></span>

## <a name="general-application-management"></a><span data-ttu-id="e00ae-275">Genel Uygulama Yönetimi</span><span class="sxs-lookup"><span data-stu-id="e00ae-275">General Application Management</span></span>
<span data-ttu-id="e00ae-276">Uygulamaları yönetirken çoğunlukla yedekleme stratejilerini yapılandırma, kimlik sağlayıcılarını uygulama ve yönetme ile Rol tabanlı erişim denetimini yapılandırma gibi çok çeşitli etkinlikler gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e00ae-276">When managing applications, you often need to perform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span></span> <span data-ttu-id="e00ae-277">Diğer DevOps deneyimlerinde olduğu gibi Azure platformu da bu görevleri doğrudan portalda tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="e00ae-277">As with the other DevOps experiences, the Azure platform integrates these tasks directly into the portal.</span></span>

1. <span data-ttu-id="e00ae-278">Web Uygulaması veri kaybından koruduğunuzdan emin olmak için yedeklemeleri yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e00ae-278">To ensure you are keeping the Web App safe from data loss you need to configure backups.</span></span> <span data-ttu-id="e00ae-279">Web uygulamanızın Ayarlar alanına gidin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-279">Navigate to the Settings area for your Web app.</span></span>
   
   ![image56][image56]
2. <span data-ttu-id="e00ae-281">Sağdaki dikey pencerede Özellikler kategorisine inin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-281">In the blade on the right, scroll down to the Features category.</span></span>
   
    ![image57][image57]
3. <span data-ttu-id="e00ae-283">Yedeklemeler’i seçin; sağ tarafta bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="e00ae-283">Choose Backups; a blade opens on the right.</span></span>
   
   ![image58][image58]
4. <span data-ttu-id="e00ae-285">Yapılandır'a tıklayın ve sağ taraftaki dikey pencereden bir depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-285">Click Configure, choose a storage account from the blade on the right.</span></span>
   
   ![image59][image59]
5. <span data-ttu-id="e00ae-287">Bundan sonra yedeklemelerinizin tutulacağı bir depolama kapsayıcısı oluşturup seçin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-287">Now create and choose a storage container to hold your backups.</span></span> <span data-ttu-id="e00ae-288">Dikey pencerenin alt kısmındaki Oluştur’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-288">Click create at the bottom of the blade.</span></span> <span data-ttu-id="e00ae-289">Ardından kapsayıcıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-289">Then select the container.</span></span>
   
   ![image60][image60]
6. <span data-ttu-id="e00ae-291">Kapsayıcıyı seçtikten sonra zamanlamaları yapılandırabilir ve veritabanlarınızın yedeklerini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-291">Once you have chosen the container, you can configure schedules, as well as setup backups for your databases.</span></span> <span data-ttu-id="e00ae-292">Bu senaryo için Kaydet simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-292">For this scenario, click the save icon.</span></span>
   
    ![image61][image61]
7. <span data-ttu-id="e00ae-294">Kaydettikten sonra Yedeklemeler için soldaki dikey pencereye geri dönün.</span><span class="sxs-lookup"><span data-stu-id="e00ae-294">After saving, scroll back to the blade on the left for Backups.</span></span> <span data-ttu-id="e00ae-295">Uygulamayı yedeklemek için Şimdi Yedekle’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e00ae-295">Click Backup Now to back the application.</span></span>
   
    ![image62][image62]
8. <span data-ttu-id="e00ae-297">Birkaç dakika içinde bir yedeğin oluşturulduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-297">In a few moments, you see a backup created.</span></span> <span data-ttu-id="e00ae-298">Aşağıdaki ekran görüntüsünde Şimdi Geri Yükle seçeneğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-298">Notice the Restore Now option on the screen-shot below.</span></span>
   
    ![image63][image63]
9. <span data-ttu-id="e00ae-300">Şimdi Geri Yükle’ye tıklayın ve sağ taraftaki dikey pencerede bulunan seçenekleri inceleyin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-300">Click on Restore Now and examine the options to the blade on the right.</span></span> <span data-ttu-id="e00ae-301">Uygun bir yedekleme seçebilir ve gerektiğinde daha önceki bir duruma kolayca geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-301">You can choose an appropriate backup and easily restore to an earlier state as necessary.</span></span> <span data-ttu-id="e00ae-302">Azure portalı, uygulama için basit bir olağanüstü durum kurtarma stratejisi etkinleştirmemize yardımcı olmuştur.</span><span class="sxs-lookup"><span data-stu-id="e00ae-302">The Azure portal has helped us easily enable a simple disaster recovery strategy for the app.</span></span>
   
    ![image64][image64]
10. <span data-ttu-id="e00ae-304">Soldaki Ayarlar dikey penceresine geri dönün ve Özellikler altında Kimlik Doğrulama/Yetkilendirme’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-304">Move back to the Settings blade on the left, and under Features and choose Authentication/Authorization.</span></span>
    
     ![image65][image65]
11. <span data-ttu-id="e00ae-306">Sağdaki dikey pencereden App Service Kimlik Doğrulaması’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-306">In the blade on the right choose App Service Authentication.</span></span> <span data-ttu-id="e00ae-307">Popüler sağlayıcılar ile yapılandırabileceğiniz çeşitli seçeneklere dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-307">Notice the variety of options you can configure with popular providers.</span></span>
    
     ![image66][image66]
12. <span data-ttu-id="e00ae-309">Tercih ettiğiniz sağlayıcıyı seçin ve kapsam seçeneklerine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-309">Choose the provider of your choice and notice the options for the scope.</span></span> <span data-ttu-id="e00ae-310">Bir Uygulama Kimliği ve Uygulama Gizli Anahtarı belirtebilir ve uygulama için Facebook kimlik doğrulamasını kolayca etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for the app.</span></span> <span data-ttu-id="e00ae-311">Azure Portal, kimlik doğrulamasını uygulamalara yönelik hazır bir çözüm olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e00ae-311">The Azure Portal enables authentication as a turnkey solution for apps.</span></span>
    
     ![image67][image67]
13. <span data-ttu-id="e00ae-313">Ayarlar dikey penceresine geri dönün ve Kaynak Yönetimi kategorisi altında Kullanıcılar’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-313">Move back to the Settings blade and choose Users under the Resource Management category.</span></span>
    
     ![image68][image68]
14. <span data-ttu-id="e00ae-315">Sağdaki dikey pencerede rol ve kullanıcı eklemeye yönelik çeşitli seçeneklere dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e00ae-315">In the blade on the right examine the various options for adding roles and users.</span></span> <span data-ttu-id="e00ae-316">Azure Portal, uygulama için RBAC (Rol tabanlı erişim denetimi) özelliğini kolayca denetlemenize imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="e00ae-316">The Azure Portal lets you easily control RBAC (Role-based access control) for the application.</span></span>
    
     ![image69][image69]

## <a name="summary"></a><span data-ttu-id="e00ae-318">Özet</span><span class="sxs-lookup"><span data-stu-id="e00ae-318">Summary</span></span>
<span data-ttu-id="e00ae-319">Bu öğretici bir web uygulaması için sürekli dağıtımı hızlıca etkinleştirerek, çeşitli geliştirme ve test etkinlikleri gerçekleştirerek, canlı bir uygulamayı izleyip sorunlarını gidererek ve son olarak olağanüstü durum kurtarma, kimlik ve rol tabanlı erişim denetimi gibi anahtar stratejileri yöneterek Azure platformunun bazı olumlu yönlerini göstermiştir.</span><span class="sxs-lookup"><span data-stu-id="e00ae-319">This tutorial demonstrated some of the power with the Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span></span> <span data-ttu-id="e00ae-320">Azure platformu bu DevOps iş akışları için tümleştirilmiş bir deneyim sağlar ve elinizdeki metnin bağlamını koruyarak verimli bir şekilde çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00ae-320">The Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for the task at hand.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e00ae-321">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e00ae-321">Next steps</span></span>
* <span data-ttu-id="e00ae-322">Azure Resource Manager, Azure platformunda DevOps’un etkinleştirilmesi için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="e00ae-322">Azure Resource Manager is important for enabling DevOps on the Azure platform.</span></span>  <span data-ttu-id="e00ae-323">Daha fazla bilgi edinmek için bkz. [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e00ae-323">To learn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
* <span data-ttu-id="e00ae-324">Azure Uygulama Hizmeti dağıtımı hakkında daha fazla bilgi için [Uygulamanızı Azure Uygulama Hizmeti’e dağıtma](../app-service-web/web-sites-deploy.md) sayfasını ziyaret edin</span><span class="sxs-lookup"><span data-stu-id="e00ae-324">To learn more about Azure App Service deployment visit [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md)</span></span>

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
