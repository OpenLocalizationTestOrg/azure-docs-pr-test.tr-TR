---
title: "Eclipse için Azure araç setini kullanarak bir Docker kapsayıcısı yay önyükleme uygulama yayımlama | Microsoft Docs"
description: "Eclipse için Azure araç setini kullanarak bir web uygulaması için Microsoft Azure Docker kapsayıcısı yayımlamak öğrenin."
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
ms.openlocfilehash: fcb60fcfbda26f5f37bfb0edcb01f8737188b6bc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="f80f4-103">Eclipse için Azure araç setini kullanarak bir Docker kapsayıcısı yay önyükleme uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="f80f4-103">Publish a Spring Boot app as a Docker container by using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="f80f4-104">[Yay Framework] Java geliştiriciler kuruluş düzeyinde uygulamalar oluşturmanıza yardımcı olan bir açık kaynaklı bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="f80f4-104">The [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="f80f4-105">Yerleşik daha popüler projelerden biri üzerinde üst o platformudur [yay önyükleme], tek başına Java uygulamaları oluşturmak için basitleştirilmiş bir yaklaşım sağlar.</span><span class="sxs-lookup"><span data-stu-id="f80f4-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="f80f4-106">[Docker] geliştiricilere yardımcı olan bir açık kaynak çözümü dağıtımını, ölçeklendirme ve kapsayıcılarında çalışan kendi uygulamalarını yönetimini otomatikleştirmek olduğu.</span><span class="sxs-lookup"><span data-stu-id="f80f4-106">[Docker] is an open-source solution that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="f80f4-107">Bu öğreticide, Eclipse için Azure Araç Seti kullanarak Microsoft Azure için Docker kapsayıcısı olarak yay önyükleme uygulama dağıtma adımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f80f4-107">This tutorial walks you through the steps to deploy a Spring Boot application as a Docker container to Microsoft Azure by using the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repository"></a><span data-ttu-id="f80f4-108">Varsayılan yay önyükleme Docker depoyu kopyalayın</span><span class="sxs-lookup"><span data-stu-id="f80f4-108">Clone the default Spring Boot Docker repository</span></span>

### <a name="import-the-public-repository"></a><span data-ttu-id="f80f4-109">Genel depo alma</span><span class="sxs-lookup"><span data-stu-id="f80f4-109">Import the public repository</span></span>

<span data-ttu-id="f80f4-110">Aşağıdaki adımlar, yerel bilgisayarınızın yay önyükleme Docker depoya Intellij kullanarak kopyalama aracılığıyla yol.</span><span class="sxs-lookup"><span data-stu-id="f80f4-110">The following steps walk you through cloning the Spring Boot Docker repository to your local computer by using IntelliJ.</span></span> <span data-ttu-id="f80f4-111">Bir komut satırı kullanmak istiyorsanız, bkz: [Linux Azure kapsayıcı Hizmeti'nde bir yay önyükleme uygulamasını dağıtmak][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="f80f4-111">If you want to use a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="f80f4-112">Eclipse açın.</span><span class="sxs-lookup"><span data-stu-id="f80f4-112">Open Eclipse.</span></span>

1. <span data-ttu-id="f80f4-113">Tıklatın **dosya** > **alma**.</span><span class="sxs-lookup"><span data-stu-id="f80f4-113">Click **File** > **Import**.</span></span>

   ![Dosya alma menüsü][CL01]

1. <span data-ttu-id="f80f4-115">Zaman **alma** iletişim kutusunu açar:</span><span class="sxs-lookup"><span data-stu-id="f80f4-115">When the **Import** dialog box opens:</span></span>

   <span data-ttu-id="f80f4-116">a.</span><span class="sxs-lookup"><span data-stu-id="f80f4-116">a.</span></span> <span data-ttu-id="f80f4-117">Genişletme **Git**.</span><span class="sxs-lookup"><span data-stu-id="f80f4-117">Expand **Git**.</span></span>

   <span data-ttu-id="f80f4-118">b.</span><span class="sxs-lookup"><span data-stu-id="f80f4-118">b.</span></span> <span data-ttu-id="f80f4-119">Seçin **Git projeleri**.</span><span class="sxs-lookup"><span data-stu-id="f80f4-119">Select **Projects from Git**.</span></span>
   
   <span data-ttu-id="f80f4-120">c.</span><span class="sxs-lookup"><span data-stu-id="f80f4-120">c.</span></span> <span data-ttu-id="f80f4-121">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f80f4-121">Click **Next**.</span></span>

   ![İçeri aktarma iletişim kutusu][CL02]

1. <span data-ttu-id="f80f4-123">Üzerinde **depo kaynağı seçin** sayfa:</span><span class="sxs-lookup"><span data-stu-id="f80f4-123">On the **Select Repository Source** page:</span></span>

   <span data-ttu-id="f80f4-124">a.</span><span class="sxs-lookup"><span data-stu-id="f80f4-124">a.</span></span> <span data-ttu-id="f80f4-125">Seçin **kopyalama URI**.</span><span class="sxs-lookup"><span data-stu-id="f80f4-125">Select **Clone URI**.</span></span>
   
   <span data-ttu-id="f80f4-126">b.</span><span class="sxs-lookup"><span data-stu-id="f80f4-126">b.</span></span> <span data-ttu-id="f80f4-127">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f80f4-127">Click **Next**.</span></span>

   ![Depo Kaynağı Seç sayfası][CL03]

1. <span data-ttu-id="f80f4-129">Üzerinde **kaynak Git deposu** sayfa:</span><span class="sxs-lookup"><span data-stu-id="f80f4-129">On the **Source Git Repository** page:</span></span>

   <span data-ttu-id="f80f4-130">a.</span><span class="sxs-lookup"><span data-stu-id="f80f4-130">a.</span></span> <span data-ttu-id="f80f4-131">İçin **URI**, girin `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span><span class="sxs-lookup"><span data-stu-id="f80f4-131">For **URI**, enter `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span></span> <span data-ttu-id="f80f4-132">Bu adımı otomatik olarak doldurur **konak** ve **deposu yolu** alanları doğru değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="f80f4-132">This step should automatically populate the **Host** and **Repository path** fields with the correct values.</span></span>
   
   <span data-ttu-id="f80f4-133">b.</span><span class="sxs-lookup"><span data-stu-id="f80f4-133">b.</span></span> <span data-ttu-id="f80f4-134">Yay önyükleme depo ortak olduğundan Git kullanıcı adı ve parola girmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f80f4-134">The Spring Boot repository is public, so you should not have to enter your Git username and password.</span></span>
   
   <span data-ttu-id="f80f4-135">c.</span><span class="sxs-lookup"><span data-stu-id="f80f4-135">c.</span></span> <span data-ttu-id="f80f4-136">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f80f4-136">Click **Next**.</span></span>

   ![Kaynak Git deposu sayfası][CL04]

1. <span data-ttu-id="f80f4-138">Üzerinde **dal seçimi** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="f80f4-138">On the **Branch Selection** page, click **Next**.</span></span>

   ![Dal seçimi sayfası][CL05]

1. <span data-ttu-id="f80f4-140">Üzerinde **yerel hedef** sayfa:</span><span class="sxs-lookup"><span data-stu-id="f80f4-140">On the **Local Destination** page:</span></span>

   <span data-ttu-id="f80f4-141">a.</span><span class="sxs-lookup"><span data-stu-id="f80f4-141">a.</span></span> <span data-ttu-id="f80f4-142">Yerel klasör, Yerel Depodaki istediğiniz yeri belirtin.</span><span class="sxs-lookup"><span data-stu-id="f80f4-142">Specify the local folder where you want your local repo.</span></span>
   
   <span data-ttu-id="f80f4-143">b.</span><span class="sxs-lookup"><span data-stu-id="f80f4-143">b.</span></span> <span data-ttu-id="f80f4-144">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f80f4-144">Click **Next**.</span></span>

   ![Yerel hedef sayfası][CL06]

1. <span data-ttu-id="f80f4-146">Üzerinde **projeleri içeri aktarmada kullanmak için sihirbaz seçin** sayfa:</span><span class="sxs-lookup"><span data-stu-id="f80f4-146">On the **Select a wizard to use for importing projects** page:</span></span>

   <span data-ttu-id="f80f4-147">a.</span><span class="sxs-lookup"><span data-stu-id="f80f4-147">a.</span></span> <span data-ttu-id="f80f4-148">Seçin **genel bir proje olarak içe aktar**.</span><span class="sxs-lookup"><span data-stu-id="f80f4-148">Select **Import as a general project**.</span></span>
   
   <span data-ttu-id="f80f4-149">b.</span><span class="sxs-lookup"><span data-stu-id="f80f4-149">b.</span></span> <span data-ttu-id="f80f4-150">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f80f4-150">Click **Next**.</span></span>

   !["Projeleri içeri aktarmada kullanmak için bir sihirbaz Seç" sayfasını][CL07]

1. <span data-ttu-id="f80f4-152">Üzerinde **projeleri içeri aktar** sayfa:</span><span class="sxs-lookup"><span data-stu-id="f80f4-152">On the **Import Projects** page:</span></span>

   <span data-ttu-id="f80f4-153">a.</span><span class="sxs-lookup"><span data-stu-id="f80f4-153">a.</span></span> <span data-ttu-id="f80f4-154">Proje adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="f80f4-154">Specify your project name.</span></span>
   
   <span data-ttu-id="f80f4-155">b.</span><span class="sxs-lookup"><span data-stu-id="f80f4-155">b.</span></span> <span data-ttu-id="f80f4-156">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f80f4-156">Click **Finish**.</span></span>

   ![Projeleri sayfasını içeri aktarma][CL08]

1. <span data-ttu-id="f80f4-158">Depo başarıyla kopyalanması için Eclipse'te listelenen tüm dosyaları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f80f4-158">When the repository is cloned successfully, you see all the files listed in Eclipse.</span></span>

   ![Yerel deposu][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a><span data-ttu-id="f80f4-160">Yerel depodan bir Maven projesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="f80f4-160">Create a Maven project from your local repository</span></span>

<span data-ttu-id="f80f4-161">Yay önyükleme Docker deposu, Bu öğretici için kullanacağınız tamamlanmış bir Maven projesi içerir.</span><span class="sxs-lookup"><span data-stu-id="f80f4-161">The Spring Boot Docker repository contains a completed Maven project, which you will use for this tutorial.</span></span> 

1. <span data-ttu-id="f80f4-162">Tıklatın **dosya** > **alma**.</span><span class="sxs-lookup"><span data-stu-id="f80f4-162">Click **File** > **Import**.</span></span>

   ![Dosya menüsünde Import komutu][CL01]

1. <span data-ttu-id="f80f4-164">Zaman **alma** iletişim kutusunu açar:</span><span class="sxs-lookup"><span data-stu-id="f80f4-164">When the **Import** dialog box opens:</span></span>

   <span data-ttu-id="f80f4-165">a.</span><span class="sxs-lookup"><span data-stu-id="f80f4-165">a.</span></span> <span data-ttu-id="f80f4-166">Genişletme **Maven**.</span><span class="sxs-lookup"><span data-stu-id="f80f4-166">Expand **Maven**.</span></span>
   
   <span data-ttu-id="f80f4-167">b.</span><span class="sxs-lookup"><span data-stu-id="f80f4-167">b.</span></span> <span data-ttu-id="f80f4-168">Seçin **varolan Maven projelerini**.</span><span class="sxs-lookup"><span data-stu-id="f80f4-168">Select **Existing Maven Projects**.</span></span>
   
   <span data-ttu-id="f80f4-169">c.</span><span class="sxs-lookup"><span data-stu-id="f80f4-169">c.</span></span> <span data-ttu-id="f80f4-170">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f80f4-170">Click **Next**.</span></span>

   ![İçeri aktarma iletişim kutusu][MV01]

1. <span data-ttu-id="f80f4-172">Üzerinde **Maven projelerini** sayfa:</span><span class="sxs-lookup"><span data-stu-id="f80f4-172">On the **Maven Projects** page:</span></span>

   <span data-ttu-id="f80f4-173">a.</span><span class="sxs-lookup"><span data-stu-id="f80f4-173">a.</span></span> <span data-ttu-id="f80f4-174">İçin **kök dizini**, belirtin **tam** yerel deponuza klasöründe.</span><span class="sxs-lookup"><span data-stu-id="f80f4-174">For **Root Directory**, specify the **complete** folder in your local repository.</span></span>
   
   <span data-ttu-id="f80f4-175">b.</span><span class="sxs-lookup"><span data-stu-id="f80f4-175">b.</span></span> <span data-ttu-id="f80f4-176">Genişletme **Gelişmiş** bölümünde ve özel bir adı **adı şablonu**.</span><span class="sxs-lookup"><span data-stu-id="f80f4-176">Expand the **Advanced** section, and enter a custom name for **Name template**.</span></span>
   
   <span data-ttu-id="f80f4-177">c.</span><span class="sxs-lookup"><span data-stu-id="f80f4-177">c.</span></span> <span data-ttu-id="f80f4-178">Kutusunu seçin **pom.xml** proje dosyasında.</span><span class="sxs-lookup"><span data-stu-id="f80f4-178">Select the box for the **pom.xml** file in the project.</span></span>
   
   <span data-ttu-id="f80f4-179">d.</span><span class="sxs-lookup"><span data-stu-id="f80f4-179">d.</span></span> <span data-ttu-id="f80f4-180">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f80f4-180">Click **Finish**.</span></span>

   ![Maven Projeler sayfası][MV02]

1. <span data-ttu-id="f80f4-182">Bir Maven projesi başarıyla açıldığında, Eclipse'te listelenen ikinci bir proje bakın.</span><span class="sxs-lookup"><span data-stu-id="f80f4-182">When the Maven project is opened successfully, you see a second project listed in Eclipse.</span></span>

   ![Yerel bir Maven projesi][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a><span data-ttu-id="f80f4-184">Maven kullanarak yay önyükleme uygulamanızı oluşturun</span><span class="sxs-lookup"><span data-stu-id="f80f4-184">Build your Spring Boot app by using Maven</span></span>

1. <span data-ttu-id="f80f4-185">Eclipse proje Gezgini'nde bir Maven projesi seçin.</span><span class="sxs-lookup"><span data-stu-id="f80f4-185">In the Eclipse Project Explorer, select the Maven project.</span></span>

1. <span data-ttu-id="f80f4-186">Tıklatın **çalıştırmak** > **Çalıştır** > **Maven derleme**.</span><span class="sxs-lookup"><span data-stu-id="f80f4-186">Click **Run** > **Run As** > **Maven build**.</span></span>

   ![Maven çalıştırılacak komutları derleme][BU01]

1. <span data-ttu-id="f80f4-188">Uygulamanız başarılı bir şekilde yapılandırıldığında, konsol penceresi durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="f80f4-188">When your application is successfully built, the console window shows the status.</span></span>

   ![Başarılı Maven derleme][BU02]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="f80f4-190">Docker kapsayıcısı kullanarak Azure için web uygulamanızı yayınlama</span><span class="sxs-lookup"><span data-stu-id="f80f4-190">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="f80f4-191">Eclipse proje Gezgini'nde bir Maven projesi seçin.</span><span class="sxs-lookup"><span data-stu-id="f80f4-191">In the Eclipse Project Explorer, select the Maven project.</span></span>

1. <span data-ttu-id="f80f4-192">Azure'ı tıklatın **Yayımla** menüsüne ve ardından **Docker kapsayıcısı olarak Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="f80f4-192">Click the Azure **Publish** menu, and then click **Publish as Docker Container**.</span></span>

   ![Docker kapsayıcısı komut olarak Yayımla][PU01]

1. <span data-ttu-id="f80f4-194">Zaman **dağıtma Docker kapsayıcısı Azure üzerinde** iletişim kutusu görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="f80f4-194">When the **Deploying Docker Container on Azure** dialog box appears:</span></span>

   <span data-ttu-id="f80f4-195">a.</span><span class="sxs-lookup"><span data-stu-id="f80f4-195">a.</span></span> <span data-ttu-id="f80f4-196">Özel bir Docker görüntü adı girin.</span><span class="sxs-lookup"><span data-stu-id="f80f4-196">Enter a custom Docker image name.</span></span>
   
   <span data-ttu-id="f80f4-197">b.</span><span class="sxs-lookup"><span data-stu-id="f80f4-197">b.</span></span> <span data-ttu-id="f80f4-198">İçin **dağıtmak için yapı**, yolunu belirtin **gs-yay-önyükleme-docker-0.1.0.jar** dosyası yalnızca oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="f80f4-198">For **Artifact to deploy**, specify the path to the **gs-spring-boot-docker-0.1.0.jar** file you just built.</span></span>

   ![Docker seçeneklerini belirtin][PU02]

   <span data-ttu-id="f80f4-200">Herhangi bir varolan Docker ana bilgisayar görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f80f4-200">Any existing Docker hosts are displayed.</span></span> 

1. <span data-ttu-id="f80f4-201">Varolan bir ana bilgisayara dağıtmak isterseniz, 5. adıma atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f80f4-201">If you choose to deploy to an existing host, you can skip to step 5.</span></span> <span data-ttu-id="f80f4-202">Aksi halde, bir ana bilgisayar oluşturmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="f80f4-202">Otherwise, use the following steps to create a host:</span></span>

   <span data-ttu-id="f80f4-203">a.</span><span class="sxs-lookup"><span data-stu-id="f80f4-203">a.</span></span> <span data-ttu-id="f80f4-204">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f80f4-204">Click **Add**.</span></span>

      ![Yeni bir Docker ana bilgisayar Ekle][PU03]

   <span data-ttu-id="f80f4-206">b.</span><span class="sxs-lookup"><span data-stu-id="f80f4-206">b.</span></span> <span data-ttu-id="f80f4-207">Zaman **oluşturma Docker ana** iletişim kutusu görüntülenirse, varsayılan değerleri kabul etmeyi tercih edebilirsiniz veya yeni Docker ana bilgisayarınız için özel ayarlar belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f80f4-207">When the **Create Docker Host** dialog box appears, you can choose to accept the defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="f80f4-208">(Çeşitli ayarları ayrıntılı açıklamaları için bkz: [Intellij için Azure araç setini kullanarak bir web uygulaması Docker kapsayıcısı yayımlama][Publish Container with Azure Toolkit].) Tıklatın **sonraki** zaman belirttiğiniz kullanmak için hangi ayarları.</span><span class="sxs-lookup"><span data-stu-id="f80f4-208">(For detailed descriptions of the various settings, see [Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings to use.</span></span>

      ![Docker ana bilgisayar seçeneklerini belirtin][PU04]

   <span data-ttu-id="f80f4-210">c.</span><span class="sxs-lookup"><span data-stu-id="f80f4-210">c.</span></span> <span data-ttu-id="f80f4-211">Azure anahtar Kasası'ndan varolan oturum açma kimlik bilgilerini kullanmayı seçebilirsiniz veya yeni Docker oturum açma kimlik bilgilerini girmeyi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f80f4-211">You can choose to use existing login credentials from an Azure key vault, or you can choose to enter new Docker login credentials.</span></span> <span data-ttu-id="f80f4-212">Tıklatın **son** zaman belirttiğiniz seçeneklerinizi.</span><span class="sxs-lookup"><span data-stu-id="f80f4-212">Click **Finish** when you have specified your options.</span></span>

      ![Docker ana bilgisayar kimlik bilgilerini belirtin][PU05]

1. <span data-ttu-id="f80f4-214">Docker ana bilgisayarınız seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="f80f4-214">Select your Docker host, and then click **Next**.</span></span>

   ![Kullanmak için Docker ana bilgisayar seçin][PU06]

1. <span data-ttu-id="f80f4-216">Sihirbazın son sayfasında **dağıtma Docker kapsayıcısı Azure üzerinde** iletişim kutusunda, aşağıdaki seçenekleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="f80f4-216">On the last page of the **Deploying Docker Container on Azure** dialog box, specify the following options:</span></span>

   <span data-ttu-id="f80f4-217">a.</span><span class="sxs-lookup"><span data-stu-id="f80f4-217">a.</span></span> <span data-ttu-id="f80f4-218">Varsayılan ayarı kabul edebilirsiniz veya özel bir Docker kapsayıcısı barındıracak kapsayıcının adını belirtmek seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f80f4-218">You can choose to specify a custom name for the container that will host your Docker container, or you can accept the default.</span></span>

   <span data-ttu-id="f80f4-219">b.</span><span class="sxs-lookup"><span data-stu-id="f80f4-219">b.</span></span> <span data-ttu-id="f80f4-220">TCP bağlantı noktaları docker ana bilgisayarınız için aşağıdaki sözdizimini kullanarak girin: *[dış bağlantı noktası]*:*[iç bağlantı noktası]*.</span><span class="sxs-lookup"><span data-stu-id="f80f4-220">Enter the TCP ports for your docker host by using the following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="f80f4-221">Örneğin, **80:8080** bir dış bağlantı noktası 80 ve varsayılan iç yay önyükleme bağlantı noktası 8080 belirtir.</span><span class="sxs-lookup"><span data-stu-id="f80f4-221">For example, **80:8080** specifies an external port of 80 and the default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="f80f4-222">İç bağlantı noktası (örneğin, application.yml dosyasını düzenleyerek) özelleştirdiyseniz, doğru Azure üzerinde gerçekleşmesi için yönlendirme için bağlantı noktası numarasını belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f80f4-222">If you have customized your internal port (for example, by editing the application.yml file), you need to specify the port number for the correct routing to occur in Azure.</span></span>

   <span data-ttu-id="f80f4-223">c.</span><span class="sxs-lookup"><span data-stu-id="f80f4-223">c.</span></span> <span data-ttu-id="f80f4-224">Bu seçenekleri yapılandırdıktan sonra tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="f80f4-224">After you configure these options, click **Finish**.</span></span>

   ![Azure üzerinde bir Docker kapsayıcısı dağıtma][PU07]

1. <span data-ttu-id="f80f4-226">Azure Araç Seti yayımlama tamamlandığında, Azure etkinlik günlüğü görüntüler **yayımlanan** durum.</span><span class="sxs-lookup"><span data-stu-id="f80f4-226">When the Azure Toolkit has finished publishing, the Azure Activity Log displays **Published** for the status.</span></span>

   ![Docker ana başarıyla dağıtıldı][PU08]

## <a name="next-steps"></a><span data-ttu-id="f80f4-228">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f80f4-228">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
<span data-ttu-id="f80f4-229">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="f80f4-229">[Docker]: https://www.docker.com/</span></span>
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
<span data-ttu-id="f80f4-230">[yay önyükleme]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="f80f4-230">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="f80f4-231">[Yay Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="f80f4-231">[Spring Framework]: https://spring.io/</span></span>

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
