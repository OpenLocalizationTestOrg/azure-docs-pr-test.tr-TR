---
title: "Öğretici: Hello Azure Portal ile DevOps | Microsoft Docs"
description: "Bilgi hello Azure Portal'ın çeşitli DevOps iş akışları hello."
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
ms.openlocfilehash: 4c32dbbd4e4b1c3809ef4b01e1496e350183ebde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-devops-with-hello-azure-portal"></a><span data-ttu-id="04c77-103">Öğretici: Hello Azure Portal ile DevOps</span><span class="sxs-lookup"><span data-stu-id="04c77-103">Tutorial: DevOps with hello Azure Portal</span></span>
<span data-ttu-id="04c77-104">Hello Azure platformu esnek DevOps iş akışları ile doludur.</span><span class="sxs-lookup"><span data-stu-id="04c77-104">hello Azure platform is full of flexible DevOps workflows.</span></span> <span data-ttu-id="04c77-105">Bu öğreticide, nasıl tooleverage hello hello Azure Portal toodevelop özelliklerini sınamak, dağıtma, sorun giderme, izlemek ve çalışan uygulamaları yönetmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="04c77-105">In this tutorial, you learn how tooleverage hello capabilities of hello Azure Portal toodevelop, test, deploy, troubleshoot, monitor, and manage running applications.</span></span> <span data-ttu-id="04c77-106">Bu öğretici hello aşağıdakilere odaklanır:</span><span class="sxs-lookup"><span data-stu-id="04c77-106">This tutorial focuses on hello following:</span></span>

1. <span data-ttu-id="04c77-107">Bir web uygulaması oluşturma ve sürekli dağıtımı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="04c77-107">Creating a web app and enabling continuous deployment</span></span>
2. <span data-ttu-id="04c77-108">Uygulama geliştirme ve test etme</span><span class="sxs-lookup"><span data-stu-id="04c77-108">Develop and test an app</span></span>
3. <span data-ttu-id="04c77-109">Bir uygulamayı izleme ve sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="04c77-109">Monitoring and Troubleshooting an app</span></span>
4. <span data-ttu-id="04c77-110">Genel uygulama yönetimi görevleri</span><span class="sxs-lookup"><span data-stu-id="04c77-110">General application management tasks</span></span>

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a><span data-ttu-id="04c77-111">Bir web uygulaması oluşturma ve sürekli dağıtımı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="04c77-111">Creating a web app and enabling continuous deployment</span></span>
<span data-ttu-id="04c77-112">Bir Web uygulaması ile oluşturma [Azure App Service](https://azure.microsoft.com/services/app-service/), bu öğreticinin hello kalan kullanması.</span><span class="sxs-lookup"><span data-stu-id="04c77-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in hello rest of this tutorial.</span></span> <span data-ttu-id="04c77-113">Başlangıçta kaynak kod deponuzdan çalışan Azure ortamımıza sürekli dağıtımı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="04c77-113">You’ll initially enable continuous deployment from your source code repository into our running Azure environment.</span></span>

1. <span data-ttu-id="04c77-114">Azure portalında oturum açın hello</span><span class="sxs-lookup"><span data-stu-id="04c77-114">Sign into hello Azure Portal</span></span>
2. <span data-ttu-id="04c77-115">Seçin **uygulama hizmetleri** &gt; **Ekle simgesi** ve bir ad girin, aboneliğinizi seçin ve yeni bir kaynak grubu tooserve hello hizmeti için hello kapsayıcı olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="04c77-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group tooserve as hello container for hello service.</span></span>
   
   <span data-ttu-id="04c77-116">Kaynak grupları toomanage izin hello çözüm faturalandırma, dağıtımlar ve aracılığıyla tek bir grup olarak tüm izleme gibi çeşitli yönlerini [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04c77-116">Resource groups allow you toomanage various aspects of hello solution such as billing, deployments and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>
   
   ![image1][image1]
3. <span data-ttu-id="04c77-118">Birkaç dakika sonra uygulama hizmetiniz oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="04c77-118">After a few moments, your app service is created.</span></span> <span data-ttu-id="04c77-119">Birkaç dakika tooexplore hello hello hizmet çeşitli menü seçeneklerini hello Portalı'nda alın.</span><span class="sxs-lookup"><span data-stu-id="04c77-119">Take a few minutes tooexplore hello various menu options for hello service in hello portal.</span></span>
   
   ![image2][image2]    
4. <span data-ttu-id="04c77-121">Merhaba URL'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="04c77-121">Click hello URL.</span></span> <span data-ttu-id="04c77-122">Merhaba çeşitli havuzlar ve depolara mevcut seçeneklere dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="04c77-122">Notice hello variety of available choices for tools and repositories.</span></span> <span data-ttu-id="04c77-123">Merhaba dilleri ve çerçeveleri .NET, Java ve Ruby gibi seçtiğiniz de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04c77-123">You can also use hello languages and frameworks of your choice including .NET, Java, and Ruby.</span></span>
   
   ![image3][image3]    
5. <span data-ttu-id="04c77-125">Hello Azure portalı sürekli dağıtımı yalnızca birkaç basit adımdan oluşan kolay bir işlem yapar.</span><span class="sxs-lookup"><span data-stu-id="04c77-125">hello Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span></span> <span data-ttu-id="04c77-126">Hello Azure portalı, yeni oluşturduğunuz hello uygulama hizmeti için hello simgesinden ayarlarını seçin.</span><span class="sxs-lookup"><span data-stu-id="04c77-126">In hello Azure portal, choose settings from hello icon for hello app service you just created.</span></span>
   
   ![image4][image4]
   
   <span data-ttu-id="04c77-128">Merhaba sağ açar hello dikey penceresinden bölüm yayımlama toohello kaydırın.</span><span class="sxs-lookup"><span data-stu-id="04c77-128">From hello blade that opens on hello right, scroll toohello publishing section.</span></span>
   
   ![image5][image5]
6. <span data-ttu-id="04c77-130">Ardından, hello uygulaması için bazı ayarları tooenable sürekli dağıtım yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="04c77-130">Next, configure some settings tooenable continuous deployment for hello app.</span></span> <span data-ttu-id="04c77-131">Dağıtım Kaynağı’na ve ardından Kaynak Seç’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="04c77-131">Click Deployment Source and then click Choose Source.</span></span> <span data-ttu-id="04c77-132">Merhaba çeşitli depo kaynakları için sahip olduğunuz seçeneklere dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="04c77-132">Notice hello variety of options you have for repository sources.</span></span>
   
   ![image6][image6]
7. <span data-ttu-id="04c77-134">Bu örnek için GitHub'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="04c77-134">For this example choose GitHub.</span></span> <span data-ttu-id="04c77-135">İsteğe bağlı olarak, tercih ettiğiniz hello depoyu seçin ve hello yetkilendirme kimlik bilgilerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="04c77-135">Optionally choose hello repository of your choice and setup hello authorization credentials.</span></span>
   
   ![image7][image7]
8. <span data-ttu-id="04c77-137">Yetkilendirme tooyour depo sonra bir proje ve toodeploy istediğiniz dalı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04c77-137">After authorization tooyour repository, you can then choose a project and branch you wish toodeploy.</span></span> <span data-ttu-id="04c77-138">Aşağıda birkaç hayali örnek listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="04c77-138">There are several fictitious sample examples listed below.</span></span>
   
   ![image8][image8]
9. <span data-ttu-id="04c77-140">Projenizi ve dalınızı seçtikten sonra Tamam'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="04c77-140">Once you choose your project and branch, click ok.</span></span> <span data-ttu-id="04c77-141">Bir dağıtımın bildirimlerini toosee başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="04c77-141">You should start toosee notifications of a deployment.</span></span>
   
   ![image9][image9]
10. <span data-ttu-id="04c77-143">Toointegrate hello kaynak denetim deposunu Azure ile oluşturulan geri tooGitHub toosee hello Web kancası gidin.</span><span class="sxs-lookup"><span data-stu-id="04c77-143">Navigate back tooGitHub toosee hello webhook that was created toointegrate hello source control repo with Azure.</span></span> <span data-ttu-id="04c77-144">Hello Azure Portal yalnızca birkaç basit adımda GitHub ile tümleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="04c77-144">hello Azure Portal enables integration with GitHub with only a few simple steps.</span></span>
    
    ![image10][image10]
11. <span data-ttu-id="04c77-146">toodemonstrate sürekli dağıtımı hızlıca bazı içerik toohello deposunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="04c77-146">toodemonstrate continuous deployment, you quickly add some content toohello repository.</span></span> <span data-ttu-id="04c77-147">Basit bir örnek için bir örnek metin dosyası tooa GitHub deposuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="04c77-147">For a simple example, add a sample text file tooa GitHub repo.</span></span> <span data-ttu-id="04c77-148">Ücretsiz toouse .NET, Ruby, Python veya başka türden bir App Service uygulama var.</span><span class="sxs-lookup"><span data-stu-id="04c77-148">You are free toouse .NET, Ruby, Python, or some other type of application with App Service.</span></span> <span data-ttu-id="04c77-149">Ücretsiz tooadd bir metin dosyası eşitleyerek tercih ettiğiniz ASP.NET MVC, Java ya da Ruby uygulaması toohello deposu.</span><span class="sxs-lookup"><span data-stu-id="04c77-149">Feel free tooadd a text file, ASP.NET MVC, Java, or Ruby application toohello repo of your choice.</span></span>
    
    ![image11][image11]
12. <span data-ttu-id="04c77-151">Değişiklikleri tooyour depo uyguladıktan sonra yeni bir gördüğünüz dağıtım hello portal bildirimleri alanında başlatın.</span><span class="sxs-lookup"><span data-stu-id="04c77-151">After committing changes tooyour repository, you see a new deployment initiate in hello portal notifications area.</span></span> <span data-ttu-id="04c77-152">Hızlı bir şekilde değişiklikleri tooyour depo uyguladıktan sonra görmüyorsanız Eşitle'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="04c77-152">Click Sync if you do not quickly see changes after committing tooyour repository.</span></span>
    
    ![image12][image12]
13. <span data-ttu-id="04c77-154">Bu noktada, deneyin ve hello uygulama hizmeti hello sayfa yükleme, 403 hatası alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04c77-154">At this point, if you try and load hello page for hello app service, you may receive a 403 error.</span></span> <span data-ttu-id="04c77-155">Başlangıç sayfa dosyası index.htm veya default.html gibi için tipik varsayılan belge Kurulum olduğundan bu örnekte, bu değildir.</span><span class="sxs-lookup"><span data-stu-id="04c77-155">In this example, it is because there is no typical default document setup for hello page such as a file like index.htm or default.html.</span></span> <span data-ttu-id="04c77-156">Hızlı bir şekilde bu hello Azure Portal tooling hello ile çözebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04c77-156">You can quickly remedy this with hello tooling in hello Azure Portal.</span></span>  <span data-ttu-id="04c77-157">Ayarlar Hello Azure Portal'ı seçin &gt; uygulama ayarları.</span><span class="sxs-lookup"><span data-stu-id="04c77-157">In hello Azure Portal choose Settings &gt; Application Settings.</span></span>
    
     ![image13][image13]
14. <span data-ttu-id="04c77-159">Uygulama ayarları için bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="04c77-159">A blade opens for application settings.</span></span> <span data-ttu-id="04c77-160">Merhaba hello "SamplePage.html" sayfasının adını girin ve Kaydet'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="04c77-160">Enter hello name of hello page “SamplePage.html” and click Save.</span></span> <span data-ttu-id="04c77-161">Birkaç dakika tooexplore hello diğer ayarlar olur.</span><span class="sxs-lookup"><span data-stu-id="04c77-161">Take a few minutes tooexplore hello other settings.</span></span>
    
    ![image14][image14]
15. <span data-ttu-id="04c77-163">İsteğe bağlı olarak beklenen hello değişiklikleri görmek için tarayıcı URL tooensure yenileyin.</span><span class="sxs-lookup"><span data-stu-id="04c77-163">Optionally refresh your browser URL tooensure you see hello expected changes.</span></span> <span data-ttu-id="04c77-164">Bu durumda, şimdi hello sayfayı dolduran bazı basit metinler yoktur.</span><span class="sxs-lookup"><span data-stu-id="04c77-164">In this case, there is some simple text now populating hello page.</span></span> <span data-ttu-id="04c77-165">Her ek değişiklik toohello deposu içinde yeni bir otomatik dağıtım neden olur.</span><span class="sxs-lookup"><span data-stu-id="04c77-165">Each additional change toohello repository would result in a new automatic deployment.</span></span>
    
    ![image15][image15]
    
    <span data-ttu-id="04c77-167">Hello Azure Portal ile sürekli dağıtımın etkinleştirilmesi kolay bir deneyimdir.</span><span class="sxs-lookup"><span data-stu-id="04c77-167">Enabling continuous deployment with hello Azure Portal is an easy experience.</span></span> <span data-ttu-id="04c77-168">Ayrıca, daha karmaşık yayın işlem hatları oluşturabilir ve varolan kaynak denetimi ve otomatik derleme ve sürüm yönetimi sistemleri yararlanarak gibi sürekli tümleştirme sistemleri toodeploy tooAzure, diğer birçok tekniği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04c77-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems toodeploy tooAzure, such as leveraging automated build and release management systems.</span></span>

## <a name="develop-and-test-an-app"></a><span data-ttu-id="04c77-169">Uygulama geliştirme ve test etme</span><span class="sxs-lookup"><span data-stu-id="04c77-169">Develop and test an app</span></span>
<span data-ttu-id="04c77-170">Ardından, bazı değişiklikler toohello kodu temel yapın ve bu değişiklikleri hızlıca dağıtın.</span><span class="sxs-lookup"><span data-stu-id="04c77-170">Next, make some changes toohello code base and rapidly deploy those changes.</span></span> <span data-ttu-id="04c77-171">Merhaba Web uygulaması için test bazı performans ayarlama Kurulum.</span><span class="sxs-lookup"><span data-stu-id="04c77-171">You will also setup up some performance testing for hello Web app.</span></span>

1. <span data-ttu-id="04c77-172">Hello Azure Portal hello Gezinti bölmesinden uygulama Hizmetleri'ni seçin ve App service'inizi bulun.</span><span class="sxs-lookup"><span data-stu-id="04c77-172">In hello Azure Portal choose App Services from hello navigation pane, and locate your App Service.</span></span>
   
   ![image16][image16]
2. <span data-ttu-id="04c77-174">Araçlar'a tıklayın</span><span class="sxs-lookup"><span data-stu-id="04c77-174">Click Tools</span></span>
   
   ![image17][image17]
3. <span data-ttu-id="04c77-176">Kategori Araçlar altındaki geliştirme hello dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="04c77-176">Notice hello develop category under Tools.</span></span> <span data-ttu-id="04c77-177">Bize hello Azure Portal ayrılmadan uygulamalarıyla toowork sağlayan birkaç faydalı araç burada vardır.</span><span class="sxs-lookup"><span data-stu-id="04c77-177">There are several useful tools here that allow us toowork with apps without leaving hello Azure Portal.</span></span> <span data-ttu-id="04c77-178">Konsol'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="04c77-178">Click on Console.</span></span>
   
   ![image18][image18]
4. <span data-ttu-id="04c77-180">Merhaba konsol penceresinde uygulamanız için dinamik komutlar gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04c77-180">In hello console window, you can issue live commands for your app.</span></span> <span data-ttu-id="04c77-181">Type hello dir komutunu ve isabet girin.</span><span class="sxs-lookup"><span data-stu-id="04c77-181">Type hello dir command and hit enter.</span></span> <span data-ttu-id="04c77-182">Yükseltilmiş ayrıcalıklar gerektiren komutlar çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="04c77-182">Note that commands requiring elevated privileges do not work.</span></span>
   
   ![image19][image19]
5. <span data-ttu-id="04c77-184">Toohello geliştirme kategorisine geri dönün ve Visual Studio Online'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="04c77-184">Move back toohello Develop category and choose Visual Studio Online.</span></span> <span data-ttu-id="04c77-185">Note: Visual Studio Online artık Visual Studio Team Services olarak adlandırılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="04c77-185">Note: Visual Studio Online is now named Visual Studio Team Services.</span></span>
   
   ![image20][image20]
6. <span data-ttu-id="04c77-187">Merhaba tarayıcı içi düzenleme deneyimini uygulamanız için Değiştir'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="04c77-187">Toggle on hello in-browser editing experience for your App.</span></span>
   
   ![image21][image21]
7. <span data-ttu-id="04c77-189">Uygulamanız için bir web uzantısı yüklenir.</span><span class="sxs-lookup"><span data-stu-id="04c77-189">A web extension installs for your app.</span></span> <span data-ttu-id="04c77-190">Uzantıları hızla ve kolayca Azure'da işlevselliği tooapps ekleyin.</span><span class="sxs-lookup"><span data-stu-id="04c77-190">Extensions quickly and easily add functionality tooapps in Azure.</span></span> <span data-ttu-id="04c77-191">Merhaba bazıları kullanılabilir hello ekran görüntüsünde başka uzantı türleri dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="04c77-191">Notice some of hello other extension types available in hello screenshot below.</span></span>
   
   ![image22][image22]
8. <span data-ttu-id="04c77-193">Merhaba Visual Studio Online uzantısı yüklendikten sonra Git'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="04c77-193">Once hello Visual Studio Online extension installs, click Go.</span></span>
   
   ![image23][image23]
9. <span data-ttu-id="04c77-195">Bir tarayıcı sekmesi geliştirme IDE'sini doğrudan hello tarayıcıda gördüğünüz açar.</span><span class="sxs-lookup"><span data-stu-id="04c77-195">A browser tab opens where you see a development IDE directly in hello browser.</span></span> <span data-ttu-id="04c77-196">Aşağıdaki bildirim hello deneyim Chrome ' ' dir.</span><span class="sxs-lookup"><span data-stu-id="04c77-196">Notice hello experience below is in Chrome.</span></span>
   
   ![image24][image24]
10. <span data-ttu-id="04c77-198">Dosya düzenleme gibi çeşitli etkinlikleri gerçekleştirmek, dosya ve klasör ekleyin ve hello Canlı siteden içerik indirme.</span><span class="sxs-lookup"><span data-stu-id="04c77-198">You can perform several activities such as edit files, add files and folders, and download content from hello live site.</span></span> <span data-ttu-id="04c77-199">Bir hızlı düzenleme toohello SamplePage.html dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="04c77-199">Make a quick edit toohello SamplePage.html file.</span></span>
    
    ![image25][image25]
11. <span data-ttu-id="04c77-201">Birkaç dakika sonra hello değişiklikler otomatik olarak kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="04c77-201">In a few moments, hello changes are automatically saved.</span></span> <span data-ttu-id="04c77-202">Geri toohello sayfa giderseniz, hello değişiklikleri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04c77-202">If you navigate back toohello page, you can see hello changes.</span></span> <span data-ttu-id="04c77-203">Bunlar gibi canlı düzenlemeler üretim ortamları için büyük olasılıkla uygun değildir.</span><span class="sxs-lookup"><span data-stu-id="04c77-203">Keep in mind live edits like these are most likely not suitable for production environments.</span></span> <span data-ttu-id="04c77-204">Ancak, hello Araçlar geliştirme için çok kolay toomake hızlı değişiklikler yapın ve sınama ortamlarında.</span><span class="sxs-lookup"><span data-stu-id="04c77-204">However, hello tools make it very easy toomake quick changes for dev and test environments.</span></span>
    
    ![image26][image26]
    
    ![image27][image27]
12. <span data-ttu-id="04c77-207">Toohello Araçlar dikey penceresine geri dönün ve hello geliştirme kategorisi altında performans Testi'ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="04c77-207">Move back toohello tools blade and under hello Develop category, click on Performance Test.</span></span>
    
    ![image28][image28]
13. <span data-ttu-id="04c77-209">Tooset team services hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="04c77-209">You need tooset a team services account.</span></span> <span data-ttu-id="04c77-210">Daha fazla ayrıntı için buraya bakın: [Team Services Hesabı Oluşturma](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span><span class="sxs-lookup"><span data-stu-id="04c77-210">See here for more details: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span></span>
14. <span data-ttu-id="04c77-211">Yeni toocreate üzerinde bir performans testi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="04c77-211">Click on New toocreate a performance test.</span></span>
    
    ![image29][image29]
    
    <span data-ttu-id="04c77-213">Yapılandırma çeşitli değerleri hello ve hello iletişim tooinitiate bir performans testi hello altındaki testi Çalıştır'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="04c77-213">Configure hello various values and click Run Test at hello bottom of hello dialogue tooinitiate a performance test.</span></span>
    
    ![image30][image30]
    
    ![image31][image31]
15. <span data-ttu-id="04c77-216">Merhaba test çalışmaya başladıktan sonra hello durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04c77-216">Once hello test starts running, you can monitor hello state.</span></span>
    
    ![image32][image32]
    
    <span data-ttu-id="04c77-218">Merhaba test tamamlandıktan sonra hello sonuca tıklandığında daha ayrıntılı bilgi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="04c77-218">Once hello test finishes, clicking on hello result shows more details.</span></span>
    
    ![image33][image33]
16. <span data-ttu-id="04c77-220">Bu örnekte, küçük bir test çalışması, sınırlı veri tooanalyze yoktur ancak sizin çeşitli ölçümleri görebilir yanı sıra testinizi bu görünümden yeniden oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="04c77-220">In this example, you created a small test run, so there is limited data tooanalyze, but you can see various metrics as well as rerun your test from this view.</span></span> <span data-ttu-id="04c77-221">Hello Azure Portal oluşturma, yürütme ve kolay bir işlem web performans testlerini çözümleme yapar.</span><span class="sxs-lookup"><span data-stu-id="04c77-221">hello Azure Portal makes creating, executing, and analyzing web performance tests an easy process.</span></span> <span data-ttu-id="04c77-222">Merhaba ekran görüntüleri hello performans verilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="04c77-222">hello screenshots below display hello performance data.</span></span>
    
    ![image34][image34]
    
    ![image35][image35]
    
    ![image36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a><span data-ttu-id="04c77-226">Bir uygulamayı izleme ve sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="04c77-226">Monitoring and troubleshooting an app</span></span>
<span data-ttu-id="04c77-227">Azure, çalışan uygulamaları izleme ve sorunlarını gidermeye yönelik çok sayıda özellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="04c77-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span></span>

1. <span data-ttu-id="04c77-228">Hello Azure Portal'da Web uygulamamız için Araçlar seçin.</span><span class="sxs-lookup"><span data-stu-id="04c77-228">In hello Azure Portal for our Web app choose Tools.</span></span>
   
   ![image37][image37]
2. <span data-ttu-id="04c77-230">Merhaba sorun giderme kategorisi altında çalışan bir uygulamayla araçları tootroubleshoot olası sorunları kullanma seçeneklerinin çeşitliliğine hello dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="04c77-230">Under hello Troubleshoot category, notice hello various choices for using tools tootroubleshoot potential issues with a running app.</span></span> <span data-ttu-id="04c77-231">Canlı HTTP trafiğini izleme, kendi kendini onarmayı etkinleştirme, günlükleri görüntüleme ve daha fazla işlemi yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04c77-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span></span>
   
   ![image38][image38]
3. <span data-ttu-id="04c77-233">Site ölçümleri tooquickly get bazı HTTP kodlarına ilişkin bir görünüm seçin.</span><span class="sxs-lookup"><span data-stu-id="04c77-233">Choose Site Metrics tooquickly get a view of some HTTP codes.</span></span>
   
   ![image39][image39]
4. <span data-ttu-id="04c77-235">Hizmet Olarak Tanılama’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="04c77-235">Choose Diagnostics as a Service.</span></span> <span data-ttu-id="04c77-236">Uygulamanızın türünü ve ardından Çalıştır'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="04c77-236">Choose your application type, then choose Run.</span></span>
   
   ![image40][image40]
   
   <span data-ttu-id="04c77-238">Bir koleksiyon başlar.</span><span class="sxs-lookup"><span data-stu-id="04c77-238">A collection begins.</span></span>
   
   ![image41][image41]
5. <span data-ttu-id="04c77-240">Merhaba uygun günlük toodiagnose olası sorunları seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04c77-240">You may choose hello appropriate log toodiagnose potential issues.</span></span> <span data-ttu-id="04c77-241">HTTP günlükleri gibi tüm hello kullanılabilir veri seçeneklerini tooenable günlük toosee gerekir.</span><span class="sxs-lookup"><span data-stu-id="04c77-241">You need tooenable logging toosee all of hello available data options such as HTTP Logs.</span></span>
   
   ![image42][image42]
   
   <span data-ttu-id="04c77-243">Karşıdan yüklemek ve bir DebugDiag analiz hello bellek dökümü dosyasına tıklayarak analiz raporu toohelp olası sorunları bulma.</span><span class="sxs-lookup"><span data-stu-id="04c77-243">By clicking on hello Memory Dump file you can download and analyze a DebugDiag analysis report toohelp find potential issues.</span></span>
   
   ![image43][image43]
6. <span data-ttu-id="04c77-245">tooview daha fazla veri tooenable ek günlük gerekir.</span><span class="sxs-lookup"><span data-stu-id="04c77-245">tooview more data, you need tooenable additional logging.</span></span> <span data-ttu-id="04c77-246">Hello Azure Portal, toohello Web uygulamasına gidin ve Ayarlar'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="04c77-246">In hello Azure Portal, navigate toohello Web app and choose Settings.</span></span>
   
   ![image44][image44]
7. <span data-ttu-id="04c77-248">Toohello özellikler kategorisine kaydırın ve tanılama günlükleri'ni seçin.</span><span class="sxs-lookup"><span data-stu-id="04c77-248">Scroll down toohello features category, and choose Diagnostic logs.</span></span>
   
      ![image45][image45]
8. <span data-ttu-id="04c77-250">Günlük için çeşitli seçenekler hello dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="04c77-250">Notice hello various options for logging.</span></span> <span data-ttu-id="04c77-251">Web sunucusu günlüğünü açın ve Kaydet'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="04c77-251">Toggle on Web server logging and click save.</span></span>
   
   ![image46][image46]
9. <span data-ttu-id="04c77-253">Hello uygulama toohello Araçlar alanına geri dönün ve hizmet olarak Tanılama'ı seçin ve Çalıştır toorerun hello veri toplama'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="04c77-253">Move back toohello tools area for hello app and choose Diagnostics as a service and click Run toorerun hello data collection.</span></span>
   
   ![image47][image47]
10. <span data-ttu-id="04c77-255">Merhaba HTTP günlüğü ayarı etkin HTTP günlükleri için toplanan verileri bakın.</span><span class="sxs-lookup"><span data-stu-id="04c77-255">With hello HTTP logging setting enabled, you now see data collected for HTTP Logs.</span></span>
    
    ![image48][image48]
11. <span data-ttu-id="04c77-257">Merhaba HTML dosya günlüğüne tıklayarak, daha fazla araştırma için zengin bir tarayıcı tabanlı rapor üretir.</span><span class="sxs-lookup"><span data-stu-id="04c77-257">By clicking hello HTML file log, you produce a rich browser-based report for further investigation.</span></span>
    
    ![image49][image49]
12. <span data-ttu-id="04c77-259">Merhaba uygulaması için Azure Portal hello toohello Araçlar bölümüne geri dönün.</span><span class="sxs-lookup"><span data-stu-id="04c77-259">Move back toohello tools section in hello Azure Portal for hello app.</span></span> <span data-ttu-id="04c77-260">Toohello Araçlar bölümüne kaydırın ve işlem Gezgini'ni seçin.</span><span class="sxs-lookup"><span data-stu-id="04c77-260">Scroll toohello Tools section and choose Process Explorer.</span></span>
    
    ![image50][image50]
13. <span data-ttu-id="04c77-262">İşlem Gezgini'ni seçerek, çalışan işlemlere ilişkin ayrıntıları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04c77-262">By choosing Process Explorer, you can view details about running processes.</span></span> <span data-ttu-id="04c77-263">Aşağıda işlemlerin ayrıntılarına inebilir ve hatta tüm hello Azure Portal işlemlerini sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="04c77-263">Notice below you can drill into processes and even kill processes all from hello Azure Portal.</span></span>
    
    ![image51][image51]
    
    ![image52][image52]
14. <span data-ttu-id="04c77-266">Merhaba soldaki toohello ayarları dikey geri dönün.</span><span class="sxs-lookup"><span data-stu-id="04c77-266">Move back toohello Settings blade on hello left.</span></span> <span data-ttu-id="04c77-267">Yeni destek isteği’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="04c77-267">Click New support request.</span></span>
    
    ![image53][image53]
15. <span data-ttu-id="04c77-269">Merhaba sağ Hello dikey penceresinden, hello sorunlar hakkındaki ayrıntıları doldurun, kişi bilgilerini girin ve hatta tanılama verilerini karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04c77-269">From hello blade on hello right, you can fill out details about hello issues, enter contact information, and even upload diagnostic data.</span></span> <span data-ttu-id="04c77-270">Hello Azure Portal, Microsoft desteği ile sorunsuzca çalışmayı sağlar.</span><span class="sxs-lookup"><span data-stu-id="04c77-270">hello Azure Portal enables working with Microsoft support a seamless experience.</span></span>
    
    ![image54][image54]
    
    ![image55][image55]
    
    <span data-ttu-id="04c77-273">Hello Azure Portal, güçlü ve bilindik deneyimleri toohelp İzleyici tooling sağlanmasına yardımcı olur ve çalışan uygulamalarımızı giderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04c77-273">hello Azure Portal helps provide powerful and familiar tooling experiences toohelp monitor and troubleshoot our running applications.</span></span> <span data-ttu-id="04c77-274">Siz de mümkün tootake eylem hızlı bir şekilde işlemleri geri dönüştürme, etkinleştirme ve çeşitli veri koleksiyonlarını devre dışı bırakma ve hatta Microsoft Profesyonel desteği ile tümleştirme gibi görevleri gerçekleştirerek olursunuz.</span><span class="sxs-lookup"><span data-stu-id="04c77-274">You are also able tootake action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span></span>

## <a name="general-application-management"></a><span data-ttu-id="04c77-275">Genel Uygulama Yönetimi</span><span class="sxs-lookup"><span data-stu-id="04c77-275">General Application Management</span></span>
<span data-ttu-id="04c77-276">Uygulamaları yönetirken çoğunlukla tooperform çok çeşitli yedekleme stratejilerini yapılandırma, uygulama ve kimlik sağlayıcılarını yönetme ve rol tabanlı erişim denetimini yapılandırma gibi etkinlikler gerekir.</span><span class="sxs-lookup"><span data-stu-id="04c77-276">When managing applications, you often need tooperform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span></span> <span data-ttu-id="04c77-277">İle diğer DevOps deneyimlerinde hello gibi hello Azure platformu bu görevleri doğrudan hello portalda tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="04c77-277">As with hello other DevOps experiences, hello Azure platform integrates these tasks directly into hello portal.</span></span>

1. <span data-ttu-id="04c77-278">tutma tooensure hello Web uygulaması veri kaybına karşı güvenli, tooconfigure yedeklemeleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="04c77-278">tooensure you are keeping hello Web App safe from data loss you need tooconfigure backups.</span></span> <span data-ttu-id="04c77-279">Web uygulamanız için toohello ayarlar alanına gidin.</span><span class="sxs-lookup"><span data-stu-id="04c77-279">Navigate toohello Settings area for your Web app.</span></span>
   
   ![image56][image56]
2. <span data-ttu-id="04c77-281">Merhaba sağ üzerinde Hello dikey penceresinde toohello özellikler kategorisine kaydırın.</span><span class="sxs-lookup"><span data-stu-id="04c77-281">In hello blade on hello right, scroll down toohello Features category.</span></span>
   
    ![image57][image57]
3. <span data-ttu-id="04c77-283">Yedeklemeleri seçin; Merhaba doğru bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="04c77-283">Choose Backups; a blade opens on hello right.</span></span>
   
   ![image58][image58]
4. <span data-ttu-id="04c77-285">Yapılandır'ı tıklatın, bir depolama hesabı hello sağ hello dikey penceresinde aşağıdakilerden birini seçin.</span><span class="sxs-lookup"><span data-stu-id="04c77-285">Click Configure, choose a storage account from hello blade on hello right.</span></span>
   
   ![image59][image59]
5. <span data-ttu-id="04c77-287">Şimdi oluşturun ve bir depolama kapsayıcısı toohold Yedeklemelerinizin seçin.</span><span class="sxs-lookup"><span data-stu-id="04c77-287">Now create and choose a storage container toohold your backups.</span></span> <span data-ttu-id="04c77-288">Merhaba dikey penceresinde hello alt kısmındaki Oluştur'u tıklatın.</span><span class="sxs-lookup"><span data-stu-id="04c77-288">Click create at hello bottom of hello blade.</span></span> <span data-ttu-id="04c77-289">Ardından hello kapsayıcısı seçin.</span><span class="sxs-lookup"><span data-stu-id="04c77-289">Then select hello container.</span></span>
   
   ![image60][image60]
6. <span data-ttu-id="04c77-291">Merhaba kapsayıcıyı seçtikten sonra zamanlamaları gibi yedeklerini veritabanınız için yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04c77-291">Once you have chosen hello container, you can configure schedules, as well as setup backups for your databases.</span></span> <span data-ttu-id="04c77-292">Bu senaryo için hello Kaydet simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="04c77-292">For this scenario, click hello save icon.</span></span>
   
    ![image61][image61]
7. <span data-ttu-id="04c77-294">Kaydettikten sonra yedeklemeler için hello sol geri toohello dikey penceresini kaydırarak.</span><span class="sxs-lookup"><span data-stu-id="04c77-294">After saving, scroll back toohello blade on hello left for Backups.</span></span> <span data-ttu-id="04c77-295">Şimdi Yedekle tooback hello uygulama'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="04c77-295">Click Backup Now tooback hello application.</span></span>
   
    ![image62][image62]
8. <span data-ttu-id="04c77-297">Birkaç dakika içinde bir yedeğin oluşturulduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="04c77-297">In a few moments, you see a backup created.</span></span> <span data-ttu-id="04c77-298">Bildirim hello hello aşağıdaki ekran görüntüsünde şimdi geri yükle seçeneğini.</span><span class="sxs-lookup"><span data-stu-id="04c77-298">Notice hello Restore Now option on hello screen-shot below.</span></span>
   
    ![image63][image63]
9. <span data-ttu-id="04c77-300">Şimdi Geri Yükle'yi tıklatın ve hello seçenekleri toohello dikey penceresinde hello sağ inceleyin.</span><span class="sxs-lookup"><span data-stu-id="04c77-300">Click on Restore Now and examine hello options toohello blade on hello right.</span></span> <span data-ttu-id="04c77-301">Bir uygun yedekleme ve kolayca geri yükleme tooan önceki gerektiğinde durum seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04c77-301">You can choose an appropriate backup and easily restore tooan earlier state as necessary.</span></span> <span data-ttu-id="04c77-302">Hello Azure portal bize kolayca hello uygulama için bir basit olağanüstü durum kurtarma stratejisi etkinleştirmek Yardım.</span><span class="sxs-lookup"><span data-stu-id="04c77-302">hello Azure portal has helped us easily enable a simple disaster recovery strategy for hello app.</span></span>
   
    ![image64][image64]
10. <span data-ttu-id="04c77-304">Merhaba soldaki ve Özellikler altında toohello ayarları dikey geri dönün ve kimlik doğrulama/Yetkilendirme'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="04c77-304">Move back toohello Settings blade on hello left, and under Features and choose Authentication/Authorization.</span></span>
    
     ![image65][image65]
11. <span data-ttu-id="04c77-306">Merhaba dikey penceresinde hello sağ App Service kimlik doğrulaması seçin.</span><span class="sxs-lookup"><span data-stu-id="04c77-306">In hello blade on hello right choose App Service Authentication.</span></span> <span data-ttu-id="04c77-307">Merhaba çeşitli popüler sağlayıcılar ile yapılandırabileceğiniz seçeneklere dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="04c77-307">Notice hello variety of options you can configure with popular providers.</span></span>
    
     ![image66][image66]
12. <span data-ttu-id="04c77-309">Tercih ettiğiniz Hello sağlayıcıyı seçin ve hello kapsam hello seçeneklerini dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="04c77-309">Choose hello provider of your choice and notice hello options for hello scope.</span></span> <span data-ttu-id="04c77-310">Bir uygulama kimliği ve uygulama gizli anahtarı sağlayın ve hızlı bir şekilde hello uygulama için Facebook kimlik doğrulamasını etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="04c77-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for hello app.</span></span> <span data-ttu-id="04c77-311">Hello Azure Portal uygulamaları için hazır bir çözüm olarak kimlik doğrulamasını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="04c77-311">hello Azure Portal enables authentication as a turnkey solution for apps.</span></span>
    
     ![image67][image67]
13. <span data-ttu-id="04c77-313">Toohello ayarları dikey geri dönün ve hello kaynak yönetimi kategorisi altında kullanıcılar'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="04c77-313">Move back toohello Settings blade and choose Users under hello Resource Management category.</span></span>
    
     ![image68][image68]
14. <span data-ttu-id="04c77-315">Merhaba dikey penceresinde hello sağ içinde inceleyin rol ve kullanıcı eklemek için çeşitli seçenekler hello.</span><span class="sxs-lookup"><span data-stu-id="04c77-315">In hello blade on hello right examine hello various options for adding roles and users.</span></span> <span data-ttu-id="04c77-316">Hello Azure Portal hello uygulama için RBAC (rol tabanlı erişim denetimi) kolayca denetlemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="04c77-316">hello Azure Portal lets you easily control RBAC (Role-based access control) for hello application.</span></span>
    
     ![image69][image69]

## <a name="summary"></a><span data-ttu-id="04c77-318">Özet</span><span class="sxs-lookup"><span data-stu-id="04c77-318">Summary</span></span>
<span data-ttu-id="04c77-319">Hızlı bir şekilde bir web uygulaması için sürekli dağıtımı etkinleştirme, çeşitli geliştirme gerçekleştirme ve etkinlikleri test, izleme ve canlı uygulama sorunlarını giderme ve son olarak anahtarını yönetme tarafından bu öğreticinin hello Azure platformu ile Merhaba güç bazıları gösterilmektedir Olağanüstü durum kurtarma, kimlik ve rol tabanlı erişim denetimi gibi stratejiler.</span><span class="sxs-lookup"><span data-stu-id="04c77-319">This tutorial demonstrated some of hello power with hello Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span></span> <span data-ttu-id="04c77-320">Hello Azure platformu bu DevOps iş akışları için tümleşik bir deneyim sağlar ve elinizdeki hello görev bağlamının kalarak verimli bir şekilde çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04c77-320">hello Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for hello task at hand.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04c77-321">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="04c77-321">Next steps</span></span>
* <span data-ttu-id="04c77-322">Azure Resource Manager DevOps hello Azure platformu üzerinde etkinleştirilmesi için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="04c77-322">Azure Resource Manager is important for enabling DevOps on hello Azure platform.</span></span>  <span data-ttu-id="04c77-323">toolearn daha ziyaret [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04c77-323">toolearn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
* <span data-ttu-id="04c77-324">Azure uygulama hizmeti dağıtımı hakkında daha fazla ziyaret toolearn [, uygulama tooAzure uygulama hizmeti dağıtma](../app-service-web/web-sites-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="04c77-324">toolearn more about Azure App Service deployment visit [Deploy your app tooAzure App Service](../app-service-web/web-sites-deploy.md)</span></span>

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
