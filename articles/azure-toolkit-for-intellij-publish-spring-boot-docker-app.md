---
title: "aaaPublish yay önyükleme uygulama kullanarak bir Docker kapsayıcısı olarak hello Azure Araç Seti için Intellij | Microsoft Docs"
description: "Bilgi nasıl toopublish bir web uygulaması tooMicrosoft kullanarak bir Docker kapsayıcısı olarak Azure hello Azure Araç Seti Intellij için."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: 8964cb33fd8f61a39f091633ae9074d9658232fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="4f2c4-103">Intellij için hello Azure Araç Seti kullanarak Docker kapsayıcısı yay önyükleme uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="4f2c4-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="4f2c4-104">Merhaba [yay Framework] Java geliştiriciler kuruluş düzeyinde uygulamalar oluşturmanıza yardımcı olan bir açık kaynaklı bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="4f2c4-105">Yerleşik hello daha popüler projelerden biri üzerinde üst o platformudur [yay önyükleme], tek başına Java uygulamaları oluşturmak için basitleştirilmiş bir yaklaşım sağlar.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="4f2c4-106">[Docker] geliştiricilere yardımcı olan bir açık kaynak çözümü hello dağıtımını, ölçeklendirme ve kapsayıcılarında çalışan kendi uygulamalarını yönetimini otomatikleştirmek olduğu.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="4f2c4-107">Bu öğreticide Intellij için hello Azure Araç Seti kullanarak bir yay önyükleme uygulama Docker kapsayıcısı tooMicrosoft Azure olarak hello adımları toodeploy açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repo"></a><span data-ttu-id="4f2c4-108">Merhaba varsayılan yay önyükleme Docker depoyu kopyalama</span><span class="sxs-lookup"><span data-stu-id="4f2c4-108">Clone hello default Spring Boot Docker repo</span></span>

<span data-ttu-id="4f2c4-109">Merhaba aşağıdaki adımlar Intellij kullanarak hello yay önyükleme Docker depoyu kopyalama aracılığıyla yol.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-109">hello following steps walk you through cloning hello Spring Boot Docker repo by using IntelliJ.</span></span> <span data-ttu-id="4f2c4-110">Bir komut satırı toouse istiyorsanız, bkz: [Linux Azure kapsayıcı Hizmeti'nde bir yay önyükleme uygulamasını dağıtmak][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="4f2c4-110">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="4f2c4-111">Intellij açın.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-111">Open IntelliJ.</span></span>

1. <span data-ttu-id="4f2c4-112">Merhaba Hoş Geldiniz ekranında hello seçin **GitHub** hello seçeneğinde **sürüm denetiminden kullanıma** listesi.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-112">On hello welcome screen, select hello **GitHub** option in hello **Check out from Version Control** list.</span></span>

   ![Sürüm denetimi için GitHub seçeneği][CL01]

1. <span data-ttu-id="4f2c4-114">İstendiğinde toolog içinde olması durumunda kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-114">Enter your credentials if you are prompted toolog in.</span></span>

   * <span data-ttu-id="4f2c4-115">Bir kullanıcı adı/parola toolog tooGitHub içinde kullanıyorsanız:</span><span class="sxs-lookup"><span data-stu-id="4f2c4-115">If you are using a username/password toolog in tooGitHub:</span></span>

      ![GitHub kullanıcı adı ve parola girme iletişim kutusu][CL02a]

   * <span data-ttu-id="4f2c4-117">İçinde tooGitHub belirteci toolog kullanıyorsanız:</span><span class="sxs-lookup"><span data-stu-id="4f2c4-117">If you are using a token toolog in tooGitHub:</span></span>

      ![Bir GitHub belirteci girmek için iletişim kutusu][CL02b]

1. <span data-ttu-id="4f2c4-119">Girin **https://github.com/spring-guides/gs-spring-boot-docker.git** hello depo URL'si için yerel yolu ve klasör bilgileri belirtin ve ardından **kopya**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-119">Enter **https://github.com/spring-guides/gs-spring-boot-docker.git** for hello repo URL, specify your local path and folder information, and then click **Clone**.</span></span>

   ![Kopya Deposu iletişim kutusu][CL03]

1. <span data-ttu-id="4f2c4-121">Sorulduğunda toocreate Intellij projesinde, select **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-121">When you're prompted toocreate an IntelliJ project, select **No**.</span></span>

   ![Toocreate Intellij projesinde reddetme][CL04]

1. <span data-ttu-id="4f2c4-123">Merhaba Hoş Geldiniz sayfasında, tıklatın **projeyi içeri aktarma**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-123">On hello welcome page, click **Import Project**.</span></span>

   ![Proje Seçimi alma][CL05]

1. <span data-ttu-id="4f2c4-125">Merhaba yay önyükleme depodaki kopyaladığınız hello yolu bulun, seçin hello **tam** hello kök ve ardından altında bir klasör **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-125">Locate hello path where you cloned hello Spring Boot repo, select hello **complete** folder under hello root, and then click **OK**.</span></span>

   ![İçeri aktarma için bir klasör seçin][CL06]

1. <span data-ttu-id="4f2c4-127">İstendiğinde, seçin **mevcut kaynaklardan proje oluştur**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-127">When you're prompted, select **Create project from existing sources**.</span></span>

   ![Seçenek toocreate mevcut kaynaklardan bir proje][CL07]

1. <span data-ttu-id="4f2c4-129">Proje adı belirtin veya hello varsayılanı kabul etmek, hello doğru yolu toohello doğrulayın **tam** klasörünü ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-129">Specify your project name or accept hello default, verify hello correct path toohello **complete** folder, and then click **Next**.</span></span>

   ![Merhaba proje adı belirtin][CL08]

1. <span data-ttu-id="4f2c4-131">Alma için herhangi bir dizin özelleştirmek ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-131">Customize any directories for importing, and then click **Next**.</span></span>

   ![Dizinleri seçin][CL09]

1. <span data-ttu-id="4f2c4-133">Merhaba kitaplıkları tooimport gözden geçirin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-133">Review hello libraries tooimport, and then click **Next**.</span></span>

   ![Proje kitaplıkları gözden geçirin][CL10]

1. <span data-ttu-id="4f2c4-135">Merhaba modül yapısı gözden geçirin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-135">Review hello module structure, and then click **Next**.</span></span>

   ![Modül yapısı gözden geçirin][CL11]

1. <span data-ttu-id="4f2c4-137">JDK belirtin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-137">Specify your JDK, and then click **Next**.</span></span>

   ![Bir JDK belirtin][CL12]

1. <span data-ttu-id="4f2c4-139">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-139">Click **Finish**.</span></span>

   ![Son düğmesine][CL13]

<span data-ttu-id="4f2c4-141">Intellij hello yay önyükleme uygulama projesi alır ve hello alma sona erdiğinde hello yapısını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-141">IntelliJ imports hello Spring Boot app as a project and displays hello structure when hello import has finished.</span></span>

![Yay önyükleme Intellij uygulamada][CL14]

## <a name="build-your-spring-boot-app"></a><span data-ttu-id="4f2c4-143">Yay önyükleme derleme uygulama</span><span class="sxs-lookup"><span data-stu-id="4f2c4-143">Build your Spring Boot app</span></span>

### <a name="build-hello-app-by-using-hello-maven-pom"></a><span data-ttu-id="4f2c4-144">Merhaba Maven POM kullanarak Hello uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f2c4-144">Build hello app by using hello Maven POM</span></span>

1. <span data-ttu-id="4f2c4-145">Zaten açık değilse hello Maven araç penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-145">Open hello Maven tool window if it is not already opened.</span></span> <span data-ttu-id="4f2c4-146">Tıklatın **Görünüm** > **aracı Windows** > **Maven projelerini**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-146">Click **View** > **Tool Windows** > **Maven Projects**.</span></span>

   ![Araç pencereleri ve Maven projelerini komutları][BU01]

1. <span data-ttu-id="4f2c4-148">Merhaba Maven araç penceresinde sağ **paket** seçip **çalıştırmak Maven derleme**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-148">In hello Maven tool window, right-click **package** and select **Run Maven Build**.</span></span> <span data-ttu-id="4f2c4-149">(Maven projenize otomatik olarak gösterilmez, hello tıklatın **yeniden içeri aktarın** hello Maven araç çubuğundaki simgesini.)</span><span class="sxs-lookup"><span data-stu-id="4f2c4-149">(If your Maven project does not show up automatically, click hello **Reimport** icon on hello Maven toolbar.)</span></span>

   ![Maven derleme komutunu çalıştırın][BU02]

1. <span data-ttu-id="4f2c4-151">Intellij görüntülemesi gereken bir **Yapı Başarısı** iletisi yay önyükleme uygulamanız başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-151">IntelliJ should display a **BUILD SUCCESS** message when your Spring Boot app is successfully created.</span></span>

   ![Yapı Başarı iletisi][BU03]

### <a name="create-a-deployment-ready-artifact"></a><span data-ttu-id="4f2c4-153">Bir dağıtım için hazır yapı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f2c4-153">Create a deployment-ready artifact</span></span>

<span data-ttu-id="4f2c4-154">toopublish yay önyükleme uygulamanızı toocreate bir dağıtım için hazır yapı gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-154">toopublish your Spring Boot app, you need toocreate a deployment-ready artifact.</span></span> <span data-ttu-id="4f2c4-155">Merhaba aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="4f2c4-155">Use hello following steps:</span></span>

1. <span data-ttu-id="4f2c4-156">Web uygulaması projenizin Intellij içinde açın.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-156">Open your web app project in IntelliJ.</span></span>

1. <span data-ttu-id="4f2c4-157">Tıklatın **dosya**ve ardından **proje yapısını**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-157">Click **File**, and then click **Project Structure**.</span></span>

   ![Proje yapısı komutu][ART01]

1. <span data-ttu-id="4f2c4-159">Merhaba artı yeşil tıklayın (**+**) sembol tooadd bir yapı, tıklatın **JAR**ve ardından **boş**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-159">Click hello green plus (**+**) symbol tooadd an artifact, click **JAR**, and then click **Empty**.</span></span>

   ![Bir yapı ekleyin][ART02]

1. <span data-ttu-id="4f2c4-161">Değil tooadd ".jar" uzantısı hello ve Maven çıktı hello hello hedef klasör belirtin emin olmasını sağlarken, yapı adı.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-161">Name your artifact while making sure not tooadd hello ".jar" extension, and then specify hello target folder for hello Maven output.</span></span>

   ![Yapı özelliklerini belirtin][ART03]

1. <span data-ttu-id="4f2c4-163">Bir bildirimi, yapı (isteğe bağlı) oluşturun:</span><span class="sxs-lookup"><span data-stu-id="4f2c4-163">Create a manifest for your artifact (optional):</span></span>

   <span data-ttu-id="4f2c4-164">a.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-164">a.</span></span> <span data-ttu-id="4f2c4-165">Tıklatın **bildirimi oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-165">Click **Create Manifest**.</span></span>

      ![Merhaba oluşturmak bildirim düğmesini tıklatın][ART04a]

   <span data-ttu-id="4f2c4-167">b.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-167">b.</span></span> <span data-ttu-id="4f2c4-168">Merhaba yapı için Hello varsayılan yolu seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-168">Choose hello default path for hello artifact, and then click **OK**.</span></span>

      ![Yapı yolu belirtin][ART04b]

   <span data-ttu-id="4f2c4-170">c.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-170">c.</span></span> <span data-ttu-id="4f2c4-171">Merhaba üç nokta düğmesine (**...** ) toolocate hello ana sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-171">Click hello ellipsis (**...**) toolocate hello main class.</span></span>

      ![Ana sınıf bulunamadı][ART04c]

   <span data-ttu-id="4f2c4-173">d.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-173">d.</span></span> <span data-ttu-id="4f2c4-174">Ana sınıfınız seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-174">Choose your main class, and then click **OK**.</span></span>

      ![Ana sınıf belirtin][ART04d]

1. <span data-ttu-id="4f2c4-176">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-176">Click **OK**.</span></span>

   ![Merhaba proje yapısını iletişim kutusunu kapatın][ART05]

> [!NOTE]
> <span data-ttu-id="4f2c4-178">Intellij yapıları oluşturma hakkında daha fazla bilgi için bkz: [yapılandırma yapıları] hello JetBrains Web sitesinde.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-178">For more information about creating artifacts in IntelliJ, see [Configuring Artifacts] on hello JetBrains website.</span></span>
>

### <a name="build-hello-artifact-for-deployment"></a><span data-ttu-id="4f2c4-179">Merhaba yapı dağıtımı için derleme</span><span class="sxs-lookup"><span data-stu-id="4f2c4-179">Build hello artifact for deployment</span></span>

1. <span data-ttu-id="4f2c4-180">Tıklatın **yapı**ve ardından **yapıları**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-180">Click **Build**, and then click **Artifacts**.</span></span>

   ![Yapıları komutu derleme][BU04]

1. <span data-ttu-id="4f2c4-182">Ne zaman hello **yapı yapı** bağlam menüsü görüntülendikten sonra **yapı**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-182">When hello **Build Artifact** context menu appears, click **Build**.</span></span>

   ![Yapı bağlam menüsü oluşturma][BU05]

<span data-ttu-id="4f2c4-184">Intellij yay önyükleme uygulamanız için tamamlanan hello yapı hello proje araç penceresinde görüntülemelidir.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-184">IntelliJ should display hello completed artifact for your Spring Boot app in hello project tool window.</span></span>

   ![Oluşturulan yapı][BU06]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="4f2c4-186">Web uygulaması tooAzure Docker kapsayıcısı kullanarak yayımlama</span><span class="sxs-lookup"><span data-stu-id="4f2c4-186">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="4f2c4-187">Tooyour Azure hesabı imzalanmamış, hello adımları [oturum açma ilişkin yönergeler için hello Azure Araç Seti Intellij][Azure Sign In for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="4f2c4-187">If you have not signed in tooyour Azure account, follow hello steps in [Sign-in instructions for hello Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span></span>

1. <span data-ttu-id="4f2c4-188">Merhaba Proje Gezgini aracı penceresinde hello projesine sağ tıklayın ve ardından **Azure** > **Docker kapsayıcısı olarak Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-188">In hello Project Explorer tool window, right-click hello project, and then select **Azure** > **Publish as Docker Container**.</span></span>

   ![Docker kapsayıcısı komut olarak Yayımla][PU01]

1. <span data-ttu-id="4f2c4-190">Ne zaman hello **azure'da dağıtmak Docker kapsayıcısı** iletişim kutusu görüntülenirse, varolan herhangi Docker konağına görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-190">When hello **Deploy Docker Container on Azure** dialog box appears, any existing Docker hosts are displayed.</span></span> <span data-ttu-id="4f2c4-191">Toodeploy tooan var olan konak seçerseniz, toostep 4 atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-191">If you choose toodeploy tooan existing host, you can skip toostep 4.</span></span> <span data-ttu-id="4f2c4-192">Aksi takdirde, aşağıdaki adımları toocreate bir ana bilgisayar hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="4f2c4-192">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="4f2c4-193">a.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-193">a.</span></span> <span data-ttu-id="4f2c4-194">Merhaba artı yeşil tıklayın (**+**) simgesi.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-194">Click hello green plus (**+**) symbol.</span></span>

      ![Yeni bir Docker ana bilgisayar Ekle][PU02]

   <span data-ttu-id="4f2c4-196">b.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-196">b.</span></span> <span data-ttu-id="4f2c4-197">Ne zaman hello **oluşturma Docker ana** iletişim kutusu görüntülenirse, tooaccept hello Varsayılanları seçin veya yeni Docker ana bilgisayarınız için özel ayarlar belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-197">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="4f2c4-198">(Merhaba ayrıntılı açıklamaları için bkz: çeşitli ayarlar, [Intellij için hello Azure Araç Seti kullanarak bir web uygulaması Docker kapsayıcısı yayımlama][Publish Container with Azure Toolkit].) Tıklatın **sonraki** zaman belirttiğiniz hangi ayarları toouse.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-198">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![Docker ana bilgisayar seçeneklerini belirtin][PU03a]

   <span data-ttu-id="4f2c4-200">c.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-200">c.</span></span> <span data-ttu-id="4f2c4-201">Azure anahtar Kasası'nı toouse varolan oturum açma kimlik bilgilerini seçin veya yeni Docker oturum açma kimlik bilgileri tooenter seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-201">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="4f2c4-202">Tıklatın **son** zaman belirttiğiniz seçeneklerinizi.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-202">Click **Finish** when you have specified your options.</span></span>

      ![Docker ana bilgisayar kimlik bilgilerini belirtin][PU03b]

1. <span data-ttu-id="4f2c4-204">Docker ana bilgisayarınız seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-204">Select your Docker host, and then click **Next**.</span></span>

   ![Merhaba Docker ana toouse seçin][PU04]

1. <span data-ttu-id="4f2c4-206">Merhaba hello son sayfasında **azure'da dağıtmak Docker kapsayıcısı** iletişim kutusunda, aşağıdaki seçenekleri şu hello belirtin:</span><span class="sxs-lookup"><span data-stu-id="4f2c4-206">On hello last page of hello **Deploy Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="4f2c4-207">a.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-207">a.</span></span> <span data-ttu-id="4f2c4-208">Merhaba varsayılan kabul edebilir veya toospecify, Docker kapsayıcısı barındıracak hello kapsayıcı için bir özel ad seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-208">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="4f2c4-209">b.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-209">b.</span></span> <span data-ttu-id="4f2c4-210">Merhaba TCP bağlantı noktaları docker ana bilgisayarınız için sözdizimi aşağıdaki hello kullanarak girin: *[dış bağlantı noktası]*:*[iç bağlantı noktası]*.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-210">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="4f2c4-211">Örneğin, **80:8080** bir dış bağlantı noktası 80 ve hello varsayılan iç yay önyükleme bağlantı noktası 8080 belirtir.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-211">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="4f2c4-212">İç bağlantı noktası (örneğin, hello application.yml dosyasını düzenleyerek) özelleştirdiyseniz, azure'da hello doğru yönlendirme toooccur için toospecify hello bağlantı noktası numarası gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-212">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="4f2c4-213">c.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-213">c.</span></span> <span data-ttu-id="4f2c4-214">Bu seçenekleri yapılandırdıktan sonra tıklayın **son**.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-214">After you have configured these options, click **Finish**.</span></span>

   ![Azure üzerinde bir Docker kapsayıcısı dağıtma][PU05]

1. <span data-ttu-id="4f2c4-216">Yayımlama Hello Azure Araç Seti sona erdiğinde hello Azure etkinlik günlüğü görüntüler **yayımlanan** hello durumu.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-216">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![Docker ana başarıyla dağıtıldı][PU06]

## <a name="next-steps"></a><span data-ttu-id="4f2c4-218">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4f2c4-218">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="4f2c4-219">toolearn Intellij, kullanarak yay önyükleme uygulamaları oluşturmak için ek yöntemleri hakkında bkz [yay önyükleme projeleri oluşturma](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) hello JetBrains Web sitesinde.</span><span class="sxs-lookup"><span data-stu-id="4f2c4-219">toolearn about additional methods for creating Spring Boot apps by using IntelliJ, see [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) on hello JetBrains website.</span></span>

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[yapılandırma yapıları]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[yay önyükleme]: http://projects.spring.io/spring-boot/
[yay Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
