---
title: "Intellij için Azure araç setini kullanarak bir Docker kapsayıcısı yay önyükleme uygulama yayımlama | Microsoft Docs"
description: "Docker kapsayıcısı Microsoft Azure Intellij için Azure araç setini kullanarak bir web uygulaması yayımlama öğrenin."
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
ms.openlocfilehash: b771238934183c953615ac33c42a275d80657556
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="fca9d-103">Intellij için Azure araç setini kullanarak bir Docker kapsayıcısı yay önyükleme uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="fca9d-103">Publish a Spring Boot app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="fca9d-104">[Yay Framework] Java geliştiriciler kuruluş düzeyinde uygulamalar oluşturmanıza yardımcı olan bir açık kaynaklı bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="fca9d-104">The [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="fca9d-105">Yerleşik daha popüler projelerden biri üzerinde üst o platformudur [yay önyükleme], tek başına Java uygulamaları oluşturmak için basitleştirilmiş bir yaklaşım sağlar.</span><span class="sxs-lookup"><span data-stu-id="fca9d-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="fca9d-106">[Docker] geliştiricilere yardımcı olan bir açık kaynak çözümü dağıtımını, ölçeklendirme ve kapsayıcılarında çalışan kendi uygulamalarını yönetimini otomatikleştirmek olduğu.</span><span class="sxs-lookup"><span data-stu-id="fca9d-106">[Docker] is an open-source solution that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="fca9d-107">Bu öğreticide, bir yay önyükleme uygulama Docker kapsayıcısı olarak Intellij için Azure Araç Seti kullanarak Microsoft Azure'a dağıtma adımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fca9d-107">This tutorial walks you through the steps to deploy a Spring Boot application as a Docker container to Microsoft Azure by using the Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repo"></a><span data-ttu-id="fca9d-108">Varsayılan yay önyükleme Docker depoyu kopyalama</span><span class="sxs-lookup"><span data-stu-id="fca9d-108">Clone the default Spring Boot Docker repo</span></span>

<span data-ttu-id="fca9d-109">Aşağıdaki adımlar Intellij kullanarak yay önyükleme Docker depoyu kopyalama aracılığıyla yol.</span><span class="sxs-lookup"><span data-stu-id="fca9d-109">The following steps walk you through cloning the Spring Boot Docker repo by using IntelliJ.</span></span> <span data-ttu-id="fca9d-110">Bir komut satırı kullanmak istiyorsanız, bkz: [Linux Azure kapsayıcı Hizmeti'nde bir yay önyükleme uygulamasını dağıtmak][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="fca9d-110">If you want to use a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="fca9d-111">Intellij açın.</span><span class="sxs-lookup"><span data-stu-id="fca9d-111">Open IntelliJ.</span></span>

1. <span data-ttu-id="fca9d-112">Hoş Geldiniz ekranında seçin **GitHub** seçeneğini **sürüm denetiminden kullanıma** listesi.</span><span class="sxs-lookup"><span data-stu-id="fca9d-112">On the welcome screen, select the **GitHub** option in the **Check out from Version Control** list.</span></span>

   ![Sürüm denetimi için GitHub seçeneği][CL01]

1. <span data-ttu-id="fca9d-114">Oturum açmak için istenirse kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="fca9d-114">Enter your credentials if you are prompted to log in.</span></span>

   * <span data-ttu-id="fca9d-115">GitHub için oturum açmak için bir kullanıcı adı/parola kullanıyorsanız:</span><span class="sxs-lookup"><span data-stu-id="fca9d-115">If you are using a username/password to log in to GitHub:</span></span>

      ![GitHub kullanıcı adı ve parola girme iletişim kutusu][CL02a]

   * <span data-ttu-id="fca9d-117">GitHub için oturum açmak için bir belirteç kullanıyorsanız:</span><span class="sxs-lookup"><span data-stu-id="fca9d-117">If you are using a token to log in to GitHub:</span></span>

      ![Bir GitHub belirteci girmek için iletişim kutusu][CL02b]

1. <span data-ttu-id="fca9d-119">Girin **https://github.com/spring-guides/gs-spring-boot-docker.git** deposu URL'sini yerel yolu ve klasör bilgileri belirtin ve ardından **kopya**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-119">Enter **https://github.com/spring-guides/gs-spring-boot-docker.git** for the repo URL, specify your local path and folder information, and then click **Clone**.</span></span>

   ![Kopya Deposu iletişim kutusu][CL03]

1. <span data-ttu-id="fca9d-121">Intellij projesi oluşturmak için istendiğinde seçin **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-121">When you're prompted to create an IntelliJ project, select **No**.</span></span>

   ![Intellij projesi oluşturmak reddetme][CL04]

1. <span data-ttu-id="fca9d-123">Hoş Geldiniz sayfasında, tıklatın **projeyi içeri aktarma**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-123">On the welcome page, click **Import Project**.</span></span>

   ![Proje Seçimi alma][CL05]

1. <span data-ttu-id="fca9d-125">Yay önyükleme depoyu kopyaladığınız yolu bulun, seçin **tam** kök ve ardından altında bir klasör **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-125">Locate the path where you cloned the Spring Boot repo, select the **complete** folder under the root, and then click **OK**.</span></span>

   ![İçeri aktarma için bir klasör seçin][CL06]

1. <span data-ttu-id="fca9d-127">İstendiğinde, seçin **mevcut kaynaklardan proje oluştur**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-127">When you're prompted, select **Create project from existing sources**.</span></span>

   ![Mevcut kaynaklardan bir proje oluşturmak için seçeneği][CL07]

1. <span data-ttu-id="fca9d-129">Proje adı belirtin veya varsayılanı kabul etmek, doğru yolunu doğrulayın **tam** klasörünü ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-129">Specify your project name or accept the default, verify the correct path to the **complete** folder, and then click **Next**.</span></span>

   ![Proje adı belirtin][CL08]

1. <span data-ttu-id="fca9d-131">Alma için herhangi bir dizin özelleştirmek ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-131">Customize any directories for importing, and then click **Next**.</span></span>

   ![Dizinleri seçin][CL09]

1. <span data-ttu-id="fca9d-133">Kitaplıkları içeri aktarın ve ardından gözden **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-133">Review the libraries to import, and then click **Next**.</span></span>

   ![Proje kitaplıkları gözden geçirin][CL10]

1. <span data-ttu-id="fca9d-135">Modül yapısı gözden geçirin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-135">Review the module structure, and then click **Next**.</span></span>

   ![Modül yapısı gözden geçirin][CL11]

1. <span data-ttu-id="fca9d-137">JDK belirtin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-137">Specify your JDK, and then click **Next**.</span></span>

   ![Bir JDK belirtin][CL12]

1. <span data-ttu-id="fca9d-139">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fca9d-139">Click **Finish**.</span></span>

   ![Son düğmesine][CL13]

<span data-ttu-id="fca9d-141">Intellij yay önyükleme uygulamayı bir proje olarak içe aktarır ve alma işlemini tamamladığında yapısını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="fca9d-141">IntelliJ imports the Spring Boot app as a project and displays the structure when the import has finished.</span></span>

![Yay önyükleme Intellij uygulamada][CL14]

## <a name="build-your-spring-boot-app"></a><span data-ttu-id="fca9d-143">Yay önyükleme derleme uygulama</span><span class="sxs-lookup"><span data-stu-id="fca9d-143">Build your Spring Boot app</span></span>

### <a name="build-the-app-by-using-the-maven-pom"></a><span data-ttu-id="fca9d-144">Maven POM kullanarak uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="fca9d-144">Build the app by using the Maven POM</span></span>

1. <span data-ttu-id="fca9d-145">Zaten açık değilse Maven aracı penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="fca9d-145">Open the Maven tool window if it is not already opened.</span></span> <span data-ttu-id="fca9d-146">Tıklatın **Görünüm** > **aracı Windows** > **Maven projelerini**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-146">Click **View** > **Tool Windows** > **Maven Projects**.</span></span>

   ![Araç pencereleri ve Maven projelerini komutları][BU01]

1. <span data-ttu-id="fca9d-148">Maven araç penceresinde sağ **paket** seçip **çalıştırmak Maven derleme**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-148">In the Maven tool window, right-click **package** and select **Run Maven Build**.</span></span> <span data-ttu-id="fca9d-149">(Maven projenize otomatik olarak gösterilmez, tıklatın **yeniden içeri aktarın** Maven araç çubuğundaki simgeye.)</span><span class="sxs-lookup"><span data-stu-id="fca9d-149">(If your Maven project does not show up automatically, click the **Reimport** icon on the Maven toolbar.)</span></span>

   ![Maven derleme komutunu çalıştırın][BU02]

1. <span data-ttu-id="fca9d-151">Intellij görüntülemesi gereken bir **Yapı Başarısı** iletisi yay önyükleme uygulamanız başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="fca9d-151">IntelliJ should display a **BUILD SUCCESS** message when your Spring Boot app is successfully created.</span></span>

   ![Yapı Başarı iletisi][BU03]

### <a name="create-a-deployment-ready-artifact"></a><span data-ttu-id="fca9d-153">Bir dağıtım için hazır yapı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fca9d-153">Create a deployment-ready artifact</span></span>

<span data-ttu-id="fca9d-154">Yay önyükleme uygulamanızı yayımlamak için bir dağıtım için hazır yapı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fca9d-154">To publish your Spring Boot app, you need to create a deployment-ready artifact.</span></span> <span data-ttu-id="fca9d-155">Aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="fca9d-155">Use the following steps:</span></span>

1. <span data-ttu-id="fca9d-156">Web uygulaması projenizin Intellij içinde açın.</span><span class="sxs-lookup"><span data-stu-id="fca9d-156">Open your web app project in IntelliJ.</span></span>

1. <span data-ttu-id="fca9d-157">Tıklatın **dosya**ve ardından **proje yapısını**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-157">Click **File**, and then click **Project Structure**.</span></span>

   ![Proje yapısı komutu][ART01]

1. <span data-ttu-id="fca9d-159">Yeşil artı (**+**) bir yapı eklemek için Sembol **JAR**ve ardından **boş**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-159">Click the green plus (**+**) symbol to add an artifact, click **JAR**, and then click **Empty**.</span></span>

   ![Bir yapı ekleyin][ART02]

1. <span data-ttu-id="fca9d-161">".Jar" uzantısı eklememek emin olmasını sağlarken, yapı adlandırın ve ardından Maven çıktısı için hedef klasör belirtin.</span><span class="sxs-lookup"><span data-stu-id="fca9d-161">Name your artifact while making sure not to add the ".jar" extension, and then specify the target folder for the Maven output.</span></span>

   ![Yapı özelliklerini belirtin][ART03]

1. <span data-ttu-id="fca9d-163">Bir bildirimi, yapı (isteğe bağlı) oluşturun:</span><span class="sxs-lookup"><span data-stu-id="fca9d-163">Create a manifest for your artifact (optional):</span></span>

   <span data-ttu-id="fca9d-164">a.</span><span class="sxs-lookup"><span data-stu-id="fca9d-164">a.</span></span> <span data-ttu-id="fca9d-165">Tıklatın **bildirimi oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-165">Click **Create Manifest**.</span></span>

      ![Oluşturma bildirim düğmesini tıklatın][ART04a]

   <span data-ttu-id="fca9d-167">b.</span><span class="sxs-lookup"><span data-stu-id="fca9d-167">b.</span></span> <span data-ttu-id="fca9d-168">Yapı için varsayılan yolu seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-168">Choose the default path for the artifact, and then click **OK**.</span></span>

      ![Yapı yolu belirtin][ART04b]

   <span data-ttu-id="fca9d-170">c.</span><span class="sxs-lookup"><span data-stu-id="fca9d-170">c.</span></span> <span data-ttu-id="fca9d-171">Üç nokta işaretine (**...** ) ana sınıf bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="fca9d-171">Click the ellipsis (**...**) to locate the main class.</span></span>

      ![Ana sınıf bulunamadı][ART04c]

   <span data-ttu-id="fca9d-173">d.</span><span class="sxs-lookup"><span data-stu-id="fca9d-173">d.</span></span> <span data-ttu-id="fca9d-174">Ana sınıfınız seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-174">Choose your main class, and then click **OK**.</span></span>

      ![Ana sınıf belirtin][ART04d]

1. <span data-ttu-id="fca9d-176">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fca9d-176">Click **OK**.</span></span>

   ![Proje Yapısı iletişim kutusunu kapatın][ART05]

> [!NOTE]
> <span data-ttu-id="fca9d-178">Intellij yapıları oluşturma hakkında daha fazla bilgi için bkz: [yapılandırma yapıları] JetBrains Web sitesinde.</span><span class="sxs-lookup"><span data-stu-id="fca9d-178">For more information about creating artifacts in IntelliJ, see [Configuring Artifacts] on the JetBrains website.</span></span>
>

### <a name="build-the-artifact-for-deployment"></a><span data-ttu-id="fca9d-179">Dağıtım için yapı derleme</span><span class="sxs-lookup"><span data-stu-id="fca9d-179">Build the artifact for deployment</span></span>

1. <span data-ttu-id="fca9d-180">Tıklatın **yapı**ve ardından **yapıları**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-180">Click **Build**, and then click **Artifacts**.</span></span>

   ![Yapıları komutu derleme][BU04]

1. <span data-ttu-id="fca9d-182">Zaman **yapı yapı** bağlam menüsü görüntülendikten sonra **yapı**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-182">When the **Build Artifact** context menu appears, click **Build**.</span></span>

   ![Yapı bağlam menüsü oluşturma][BU05]

<span data-ttu-id="fca9d-184">Intellij yay önyükleme uygulamanız için tamamlanan yapı proje araç penceresinde görüntülemelidir.</span><span class="sxs-lookup"><span data-stu-id="fca9d-184">IntelliJ should display the completed artifact for your Spring Boot app in the project tool window.</span></span>

   ![Oluşturulan yapı][BU06]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="fca9d-186">Docker kapsayıcısı kullanarak Azure için web uygulamanızı yayınlama</span><span class="sxs-lookup"><span data-stu-id="fca9d-186">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="fca9d-187">Azure hesabınızda oturum açmanızdan değil, adımları [oturum açma ilişkin yönergeler için Azure Araç Seti Intellij][Azure Sign In for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="fca9d-187">If you have not signed in to your Azure account, follow the steps in [Sign-in instructions for the Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span></span>

1. <span data-ttu-id="fca9d-188">Proje Gezgini araç penceresi projeye sağ tıklayın ve ardından **Azure** > **Docker kapsayıcısı olarak Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-188">In the Project Explorer tool window, right-click the project, and then select **Azure** > **Publish as Docker Container**.</span></span>

   ![Docker kapsayıcısı komut olarak Yayımla][PU01]

1. <span data-ttu-id="fca9d-190">Zaman **azure'da dağıtmak Docker kapsayıcısı** iletişim kutusu görüntülenirse, varolan herhangi Docker konağına görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="fca9d-190">When the **Deploy Docker Container on Azure** dialog box appears, any existing Docker hosts are displayed.</span></span> <span data-ttu-id="fca9d-191">Varolan bir ana bilgisayara dağıtmak isterseniz, 4. adıma atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fca9d-191">If you choose to deploy to an existing host, you can skip to step 4.</span></span> <span data-ttu-id="fca9d-192">Aksi halde, bir ana bilgisayar oluşturmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="fca9d-192">Otherwise, use the following steps to create a host:</span></span>

   <span data-ttu-id="fca9d-193">a.</span><span class="sxs-lookup"><span data-stu-id="fca9d-193">a.</span></span> <span data-ttu-id="fca9d-194">Yeşil artı (**+**) simgesi.</span><span class="sxs-lookup"><span data-stu-id="fca9d-194">Click the green plus (**+**) symbol.</span></span>

      ![Yeni bir Docker ana bilgisayar Ekle][PU02]

   <span data-ttu-id="fca9d-196">b.</span><span class="sxs-lookup"><span data-stu-id="fca9d-196">b.</span></span> <span data-ttu-id="fca9d-197">Zaman **oluşturma Docker ana** iletişim kutusu görüntülenirse, varsayılan değerleri kabul etmeyi tercih edebilirsiniz veya yeni Docker ana bilgisayarınız için özel ayarlar belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fca9d-197">When the **Create Docker Host** dialog box appears, you can choose to accept the defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="fca9d-198">(Çeşitli ayarları ayrıntılı açıklamaları için bkz: [Intellij için Azure araç setini kullanarak bir web uygulaması Docker kapsayıcısı yayımlama][Publish Container with Azure Toolkit].) Tıklatın **sonraki** zaman belirttiğiniz kullanmak için hangi ayarları.</span><span class="sxs-lookup"><span data-stu-id="fca9d-198">(For detailed descriptions of the various settings, see [Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings to use.</span></span>

      ![Docker ana bilgisayar seçeneklerini belirtin][PU03a]

   <span data-ttu-id="fca9d-200">c.</span><span class="sxs-lookup"><span data-stu-id="fca9d-200">c.</span></span> <span data-ttu-id="fca9d-201">Azure anahtar Kasası'ndan varolan oturum açma kimlik bilgilerini kullanmayı seçebilirsiniz veya yeni Docker oturum açma kimlik bilgilerini girmeyi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fca9d-201">You can choose to use existing login credentials from an Azure key vault, or you can choose to enter new Docker login credentials.</span></span> <span data-ttu-id="fca9d-202">Tıklatın **son** zaman belirttiğiniz seçeneklerinizi.</span><span class="sxs-lookup"><span data-stu-id="fca9d-202">Click **Finish** when you have specified your options.</span></span>

      ![Docker ana bilgisayar kimlik bilgilerini belirtin][PU03b]

1. <span data-ttu-id="fca9d-204">Docker ana bilgisayarınız seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-204">Select your Docker host, and then click **Next**.</span></span>

   ![Kullanmak için Docker konağı seçin][PU04]

1. <span data-ttu-id="fca9d-206">Sihirbazın son sayfasında **azure'da dağıtmak Docker kapsayıcısı** iletişim kutusunda, aşağıdaki seçenekleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="fca9d-206">On the last page of the **Deploy Docker Container on Azure** dialog box, specify the following options:</span></span>

   <span data-ttu-id="fca9d-207">a.</span><span class="sxs-lookup"><span data-stu-id="fca9d-207">a.</span></span> <span data-ttu-id="fca9d-208">Varsayılan ayarı kabul edebilirsiniz veya özel bir Docker kapsayıcısı barındıracak kapsayıcının adını belirtmek seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fca9d-208">You can choose to specify a custom name for the container that will host your Docker container, or you can accept the default.</span></span>

   <span data-ttu-id="fca9d-209">b.</span><span class="sxs-lookup"><span data-stu-id="fca9d-209">b.</span></span> <span data-ttu-id="fca9d-210">TCP bağlantı noktaları docker ana bilgisayarınız için aşağıdaki sözdizimini kullanarak girin: *[dış bağlantı noktası]*:*[iç bağlantı noktası]*.</span><span class="sxs-lookup"><span data-stu-id="fca9d-210">Enter the TCP ports for your docker host by using the following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="fca9d-211">Örneğin, **80:8080** bir dış bağlantı noktası 80 ve varsayılan iç yay önyükleme bağlantı noktası 8080 belirtir.</span><span class="sxs-lookup"><span data-stu-id="fca9d-211">For example, **80:8080** specifies an external port of 80 and the default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="fca9d-212">İç bağlantı noktası (örneğin, application.yml dosyasını düzenleyerek) özelleştirdiyseniz, doğru Azure üzerinde gerçekleşmesi için yönlendirme için bağlantı noktası numarasını belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fca9d-212">If you have customized your internal port (for example, by editing the application.yml file), you need to specify the port number for the correct routing to occur in Azure.</span></span>

   <span data-ttu-id="fca9d-213">c.</span><span class="sxs-lookup"><span data-stu-id="fca9d-213">c.</span></span> <span data-ttu-id="fca9d-214">Bu seçenekleri yapılandırdıktan sonra tıklayın **son**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-214">After you have configured these options, click **Finish**.</span></span>

   ![Azure üzerinde bir Docker kapsayıcısı dağıtma][PU05]

1. <span data-ttu-id="fca9d-216">Azure Araç Seti yayımlama tamamlandığında, Azure etkinlik günlüğü görüntüler **yayımlanan** durum.</span><span class="sxs-lookup"><span data-stu-id="fca9d-216">When the Azure Toolkit has finished publishing, the Azure Activity Log displays **Published** for the status.</span></span>

   ![Docker ana başarıyla dağıtıldı][PU06]

## <a name="next-steps"></a><span data-ttu-id="fca9d-218">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fca9d-218">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="fca9d-219">Intellij kullanarak yay önyükleme uygulamaları oluşturmak için ek yöntemleri hakkında bilgi edinmek için [yay önyükleme projeleri oluşturma](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) JetBrains Web sitesinde.</span><span class="sxs-lookup"><span data-stu-id="fca9d-219">To learn about additional methods for creating Spring Boot apps by using IntelliJ, see [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) on the JetBrains website.</span></span>

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
<span data-ttu-id="fca9d-220">[yapılandırma yapıları]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html</span><span class="sxs-lookup"><span data-stu-id="fca9d-220">[Configuring Artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html</span></span>
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
<span data-ttu-id="fca9d-221">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="fca9d-221">[Docker]: https://www.docker.com/</span></span>
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
<span data-ttu-id="fca9d-222">[yay önyükleme]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="fca9d-222">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="fca9d-223">[Yay Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="fca9d-223">[Spring Framework]: https://spring.io/</span></span>

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
