---
title: "aaaPublish yay önyükleme uygulama kullanarak bir Docker kapsayıcısı olarak hello Eclipse için Azure Araç Seti | Microsoft Docs"
description: "Bilgi nasıl toopublish bir web uygulaması tooMicrosoft kullanarak bir Docker kapsayıcısı olarak Azure hello Eclipse için Azure Araç Seti."
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
ms.openlocfilehash: 29390c49c339a1ebb87cb3951b21cea01c0da15f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="38553-103">Eclipse için hello Azure Araç Seti kullanarak Docker kapsayıcısı yay önyükleme uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="38553-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="38553-104">Merhaba [yay Framework] Java geliştiriciler kuruluş düzeyinde uygulamalar oluşturmanıza yardımcı olan bir açık kaynaklı bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="38553-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="38553-105">Yerleşik hello daha popüler projelerden biri üzerinde üst o platformudur [yay önyükleme], tek başına Java uygulamaları oluşturmak için basitleştirilmiş bir yaklaşım sağlar.</span><span class="sxs-lookup"><span data-stu-id="38553-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="38553-106">[Docker] geliştiricilere yardımcı olan bir açık kaynak çözümü hello dağıtımını, ölçeklendirme ve kapsayıcılarında çalışan kendi uygulamalarını yönetimini otomatikleştirmek olduğu.</span><span class="sxs-lookup"><span data-stu-id="38553-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="38553-107">Bu öğreticide Eclipse için hello Azure Araç Seti kullanarak bir yay önyükleme uygulama Docker kapsayıcısı tooMicrosoft Azure olarak hello adımları toodeploy açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="38553-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a><span data-ttu-id="38553-108">Merhaba varsayılan yay önyükleme Docker depoyu kopyalayın</span><span class="sxs-lookup"><span data-stu-id="38553-108">Clone hello default Spring Boot Docker repository</span></span>

### <a name="import-hello-public-repository"></a><span data-ttu-id="38553-109">İçeri aktarma hello genel depo</span><span class="sxs-lookup"><span data-stu-id="38553-109">Import hello public repository</span></span>

<span data-ttu-id="38553-110">Merhaba aşağıdaki adımlar Intellij kullanarak hello yay önyükleme Docker depo tooyour yerel bilgisayar kopyalama aracılığıyla yol.</span><span class="sxs-lookup"><span data-stu-id="38553-110">hello following steps walk you through cloning hello Spring Boot Docker repository tooyour local computer by using IntelliJ.</span></span> <span data-ttu-id="38553-111">Bir komut satırı toouse istiyorsanız, bkz: [Linux Azure kapsayıcı Hizmeti'nde bir yay önyükleme uygulamasını dağıtmak][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="38553-111">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="38553-112">Eclipse açın.</span><span class="sxs-lookup"><span data-stu-id="38553-112">Open Eclipse.</span></span>

1. <span data-ttu-id="38553-113">Tıklatın **dosya** > **alma**.</span><span class="sxs-lookup"><span data-stu-id="38553-113">Click **File** > **Import**.</span></span>

   ![Dosya alma menüsü][CL01]

1. <span data-ttu-id="38553-115">Ne zaman hello **alma** iletişim kutusunu açar:</span><span class="sxs-lookup"><span data-stu-id="38553-115">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="38553-116">a.</span><span class="sxs-lookup"><span data-stu-id="38553-116">a.</span></span> <span data-ttu-id="38553-117">Genişletme **Git**.</span><span class="sxs-lookup"><span data-stu-id="38553-117">Expand **Git**.</span></span>

   <span data-ttu-id="38553-118">b.</span><span class="sxs-lookup"><span data-stu-id="38553-118">b.</span></span> <span data-ttu-id="38553-119">Seçin **Git projeleri**.</span><span class="sxs-lookup"><span data-stu-id="38553-119">Select **Projects from Git**.</span></span>
   
   <span data-ttu-id="38553-120">c.</span><span class="sxs-lookup"><span data-stu-id="38553-120">c.</span></span> <span data-ttu-id="38553-121">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38553-121">Click **Next**.</span></span>

   ![İçeri aktarma iletişim kutusu][CL02]

1. <span data-ttu-id="38553-123">Merhaba üzerinde **depo kaynağı seçin** sayfa:</span><span class="sxs-lookup"><span data-stu-id="38553-123">On hello **Select Repository Source** page:</span></span>

   <span data-ttu-id="38553-124">a.</span><span class="sxs-lookup"><span data-stu-id="38553-124">a.</span></span> <span data-ttu-id="38553-125">Seçin **kopyalama URI**.</span><span class="sxs-lookup"><span data-stu-id="38553-125">Select **Clone URI**.</span></span>
   
   <span data-ttu-id="38553-126">b.</span><span class="sxs-lookup"><span data-stu-id="38553-126">b.</span></span> <span data-ttu-id="38553-127">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38553-127">Click **Next**.</span></span>

   ![Depo Kaynağı Seç sayfası][CL03]

1. <span data-ttu-id="38553-129">Merhaba üzerinde **kaynak Git deposu** sayfa:</span><span class="sxs-lookup"><span data-stu-id="38553-129">On hello **Source Git Repository** page:</span></span>

   <span data-ttu-id="38553-130">a.</span><span class="sxs-lookup"><span data-stu-id="38553-130">a.</span></span> <span data-ttu-id="38553-131">İçin **URI**, girin `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span><span class="sxs-lookup"><span data-stu-id="38553-131">For **URI**, enter `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span></span> <span data-ttu-id="38553-132">Bu adım hello otomatik olarak doldurur **konak** ve **deposu yolu** hello alanlarla değerleri düzeltin.</span><span class="sxs-lookup"><span data-stu-id="38553-132">This step should automatically populate hello **Host** and **Repository path** fields with hello correct values.</span></span>
   
   <span data-ttu-id="38553-133">b.</span><span class="sxs-lookup"><span data-stu-id="38553-133">b.</span></span> <span data-ttu-id="38553-134">Merhaba yay önyükleme deposu ortak olduğundan Git kullanıcı adı ve parola tooenter olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="38553-134">hello Spring Boot repository is public, so you should not have tooenter your Git username and password.</span></span>
   
   <span data-ttu-id="38553-135">c.</span><span class="sxs-lookup"><span data-stu-id="38553-135">c.</span></span> <span data-ttu-id="38553-136">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38553-136">Click **Next**.</span></span>

   ![Kaynak Git deposu sayfası][CL04]

1. <span data-ttu-id="38553-138">Merhaba üzerinde **dal seçimi** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="38553-138">On hello **Branch Selection** page, click **Next**.</span></span>

   ![Dal seçimi sayfası][CL05]

1. <span data-ttu-id="38553-140">Merhaba üzerinde **yerel hedef** sayfa:</span><span class="sxs-lookup"><span data-stu-id="38553-140">On hello **Local Destination** page:</span></span>

   <span data-ttu-id="38553-141">a.</span><span class="sxs-lookup"><span data-stu-id="38553-141">a.</span></span> <span data-ttu-id="38553-142">Merhaba yerel klasör, Yerel Depodaki istediğiniz yeri belirtin.</span><span class="sxs-lookup"><span data-stu-id="38553-142">Specify hello local folder where you want your local repo.</span></span>
   
   <span data-ttu-id="38553-143">b.</span><span class="sxs-lookup"><span data-stu-id="38553-143">b.</span></span> <span data-ttu-id="38553-144">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38553-144">Click **Next**.</span></span>

   ![Yerel hedef sayfası][CL06]

1. <span data-ttu-id="38553-146">Merhaba üzerinde **projeleri İçeri Aktarma Sihirbazı'nı toouse seçin** sayfa:</span><span class="sxs-lookup"><span data-stu-id="38553-146">On hello **Select a wizard toouse for importing projects** page:</span></span>

   <span data-ttu-id="38553-147">a.</span><span class="sxs-lookup"><span data-stu-id="38553-147">a.</span></span> <span data-ttu-id="38553-148">Seçin **genel bir proje olarak içe aktar**.</span><span class="sxs-lookup"><span data-stu-id="38553-148">Select **Import as a general project**.</span></span>
   
   <span data-ttu-id="38553-149">b.</span><span class="sxs-lookup"><span data-stu-id="38553-149">b.</span></span> <span data-ttu-id="38553-150">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38553-150">Click **Next**.</span></span>

   !["Projeleri İçeri Aktarma Sihirbazı'nı toouse Seç" sayfasını][CL07]

1. <span data-ttu-id="38553-152">Merhaba üzerinde **projeleri içeri aktar** sayfa:</span><span class="sxs-lookup"><span data-stu-id="38553-152">On hello **Import Projects** page:</span></span>

   <span data-ttu-id="38553-153">a.</span><span class="sxs-lookup"><span data-stu-id="38553-153">a.</span></span> <span data-ttu-id="38553-154">Proje adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="38553-154">Specify your project name.</span></span>
   
   <span data-ttu-id="38553-155">b.</span><span class="sxs-lookup"><span data-stu-id="38553-155">b.</span></span> <span data-ttu-id="38553-156">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38553-156">Click **Finish**.</span></span>

   ![Projeleri sayfasını içeri aktarma][CL08]

1. <span data-ttu-id="38553-158">Merhaba deposu başarıyla kopyalandı, Eclipse'te listelenen tüm hello dosyalarına bakın.</span><span class="sxs-lookup"><span data-stu-id="38553-158">When hello repository is cloned successfully, you see all hello files listed in Eclipse.</span></span>

   ![Yerel deposu][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a><span data-ttu-id="38553-160">Yerel depodan bir Maven projesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="38553-160">Create a Maven project from your local repository</span></span>

<span data-ttu-id="38553-161">Bu öğretici için kullanacağınız tamamlanmış bir Maven projesi Hello yay önyükleme Docker depo içerir.</span><span class="sxs-lookup"><span data-stu-id="38553-161">hello Spring Boot Docker repository contains a completed Maven project, which you will use for this tutorial.</span></span> 

1. <span data-ttu-id="38553-162">Tıklatın **dosya** > **alma**.</span><span class="sxs-lookup"><span data-stu-id="38553-162">Click **File** > **Import**.</span></span>

   ![Merhaba Dosya menüsünde komutunu alma][CL01]

1. <span data-ttu-id="38553-164">Ne zaman hello **alma** iletişim kutusunu açar:</span><span class="sxs-lookup"><span data-stu-id="38553-164">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="38553-165">a.</span><span class="sxs-lookup"><span data-stu-id="38553-165">a.</span></span> <span data-ttu-id="38553-166">Genişletme **Maven**.</span><span class="sxs-lookup"><span data-stu-id="38553-166">Expand **Maven**.</span></span>
   
   <span data-ttu-id="38553-167">b.</span><span class="sxs-lookup"><span data-stu-id="38553-167">b.</span></span> <span data-ttu-id="38553-168">Seçin **varolan Maven projelerini**.</span><span class="sxs-lookup"><span data-stu-id="38553-168">Select **Existing Maven Projects**.</span></span>
   
   <span data-ttu-id="38553-169">c.</span><span class="sxs-lookup"><span data-stu-id="38553-169">c.</span></span> <span data-ttu-id="38553-170">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38553-170">Click **Next**.</span></span>

   ![İçeri aktarma iletişim kutusu][MV01]

1. <span data-ttu-id="38553-172">Merhaba üzerinde **Maven projelerini** sayfa:</span><span class="sxs-lookup"><span data-stu-id="38553-172">On hello **Maven Projects** page:</span></span>

   <span data-ttu-id="38553-173">a.</span><span class="sxs-lookup"><span data-stu-id="38553-173">a.</span></span> <span data-ttu-id="38553-174">İçin **kök dizini**, hello belirtin **tam** yerel deponuza klasöründe.</span><span class="sxs-lookup"><span data-stu-id="38553-174">For **Root Directory**, specify hello **complete** folder in your local repository.</span></span>
   
   <span data-ttu-id="38553-175">b.</span><span class="sxs-lookup"><span data-stu-id="38553-175">b.</span></span> <span data-ttu-id="38553-176">Merhaba genişletin **Gelişmiş** bölümünde ve özel bir adı **adı şablonu**.</span><span class="sxs-lookup"><span data-stu-id="38553-176">Expand hello **Advanced** section, and enter a custom name for **Name template**.</span></span>
   
   <span data-ttu-id="38553-177">c.</span><span class="sxs-lookup"><span data-stu-id="38553-177">c.</span></span> <span data-ttu-id="38553-178">Merhaba SELECT hello kutusunu **pom.xml** hello proje dosyasında.</span><span class="sxs-lookup"><span data-stu-id="38553-178">Select hello box for hello **pom.xml** file in hello project.</span></span>
   
   <span data-ttu-id="38553-179">d.</span><span class="sxs-lookup"><span data-stu-id="38553-179">d.</span></span> <span data-ttu-id="38553-180">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38553-180">Click **Finish**.</span></span>

   ![Maven Projeler sayfası][MV02]

1. <span data-ttu-id="38553-182">Merhaba Maven projesine başarıyla açıldığında, Eclipse'te listelenen ikinci bir proje bakın.</span><span class="sxs-lookup"><span data-stu-id="38553-182">When hello Maven project is opened successfully, you see a second project listed in Eclipse.</span></span>

   ![Yerel bir Maven projesi][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a><span data-ttu-id="38553-184">Maven kullanarak yay önyükleme uygulamanızı oluşturun</span><span class="sxs-lookup"><span data-stu-id="38553-184">Build your Spring Boot app by using Maven</span></span>

1. <span data-ttu-id="38553-185">Hello Eclipse Proje Gezgini, hello Maven projesini seçin.</span><span class="sxs-lookup"><span data-stu-id="38553-185">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="38553-186">Tıklatın **çalıştırmak** > **Çalıştır** > **Maven derleme**.</span><span class="sxs-lookup"><span data-stu-id="38553-186">Click **Run** > **Run As** > **Maven build**.</span></span>

   ![Maven derleme olarak komutları toorun][BU01]

1. <span data-ttu-id="38553-188">Uygulamanız başarılı bir şekilde yapılandırıldığında, hello konsol penceresinde hello durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="38553-188">When your application is successfully built, hello console window shows hello status.</span></span>

   ![Başarılı Maven derleme][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="38553-190">Web uygulaması tooAzure Docker kapsayıcısı kullanarak yayımlama</span><span class="sxs-lookup"><span data-stu-id="38553-190">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="38553-191">Hello Eclipse Proje Gezgini, hello Maven projesini seçin.</span><span class="sxs-lookup"><span data-stu-id="38553-191">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="38553-192">Hello Azure'ı tıklatın **Yayımla** menüsüne ve ardından **Docker kapsayıcısı olarak Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="38553-192">Click hello Azure **Publish** menu, and then click **Publish as Docker Container**.</span></span>

   ![Docker kapsayıcısı komut olarak Yayımla][PU01]

1. <span data-ttu-id="38553-194">Ne zaman hello **dağıtma Docker kapsayıcısı Azure üzerinde** iletişim kutusu görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="38553-194">When hello **Deploying Docker Container on Azure** dialog box appears:</span></span>

   <span data-ttu-id="38553-195">a.</span><span class="sxs-lookup"><span data-stu-id="38553-195">a.</span></span> <span data-ttu-id="38553-196">Özel bir Docker görüntü adı girin.</span><span class="sxs-lookup"><span data-stu-id="38553-196">Enter a custom Docker image name.</span></span>
   
   <span data-ttu-id="38553-197">b.</span><span class="sxs-lookup"><span data-stu-id="38553-197">b.</span></span> <span data-ttu-id="38553-198">İçin **yapı toodeploy**, hello yolu toohello belirtin **gs-yay-önyükleme-docker-0.1.0.jar** dosyası yalnızca oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="38553-198">For **Artifact toodeploy**, specify hello path toohello **gs-spring-boot-docker-0.1.0.jar** file you just built.</span></span>

   ![Docker seçeneklerini belirtin][PU02]

   <span data-ttu-id="38553-200">Herhangi bir varolan Docker ana bilgisayar görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="38553-200">Any existing Docker hosts are displayed.</span></span> 

1. <span data-ttu-id="38553-201">Toodeploy tooan var olan konak seçerseniz, toostep 5 atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38553-201">If you choose toodeploy tooan existing host, you can skip toostep 5.</span></span> <span data-ttu-id="38553-202">Aksi takdirde, aşağıdaki adımları toocreate bir ana bilgisayar hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="38553-202">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="38553-203">a.</span><span class="sxs-lookup"><span data-stu-id="38553-203">a.</span></span> <span data-ttu-id="38553-204">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38553-204">Click **Add**.</span></span>

      ![Yeni bir Docker ana bilgisayar Ekle][PU03]

   <span data-ttu-id="38553-206">b.</span><span class="sxs-lookup"><span data-stu-id="38553-206">b.</span></span> <span data-ttu-id="38553-207">Ne zaman hello **oluşturma Docker ana** iletişim kutusu görüntülenirse, tooaccept hello Varsayılanları seçin veya yeni Docker ana bilgisayarınız için özel ayarlar belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38553-207">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="38553-208">(Merhaba ayrıntılı açıklamaları için bkz: çeşitli ayarlar, [Intellij için hello Azure Araç Seti kullanarak bir web uygulaması Docker kapsayıcısı yayımlama][Publish Container with Azure Toolkit].) Tıklatın **sonraki** zaman belirttiğiniz hangi ayarları toouse.</span><span class="sxs-lookup"><span data-stu-id="38553-208">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![Docker ana bilgisayar seçeneklerini belirtin][PU04]

   <span data-ttu-id="38553-210">c.</span><span class="sxs-lookup"><span data-stu-id="38553-210">c.</span></span> <span data-ttu-id="38553-211">Azure anahtar Kasası'nı toouse varolan oturum açma kimlik bilgilerini seçin veya yeni Docker oturum açma kimlik bilgileri tooenter seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38553-211">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="38553-212">Tıklatın **son** zaman belirttiğiniz seçeneklerinizi.</span><span class="sxs-lookup"><span data-stu-id="38553-212">Click **Finish** when you have specified your options.</span></span>

      ![Docker ana bilgisayar kimlik bilgilerini belirtin][PU05]

1. <span data-ttu-id="38553-214">Docker ana bilgisayarınız seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="38553-214">Select your Docker host, and then click **Next**.</span></span>

   ![Docker ana toouse seçin][PU06]

1. <span data-ttu-id="38553-216">Merhaba hello son sayfasında **dağıtma Docker kapsayıcısı Azure üzerinde** iletişim kutusunda, aşağıdaki seçenekleri şu hello belirtin:</span><span class="sxs-lookup"><span data-stu-id="38553-216">On hello last page of hello **Deploying Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="38553-217">a.</span><span class="sxs-lookup"><span data-stu-id="38553-217">a.</span></span> <span data-ttu-id="38553-218">Merhaba varsayılan kabul edebilir veya toospecify, Docker kapsayıcısı barındıracak hello kapsayıcı için bir özel ad seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38553-218">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="38553-219">b.</span><span class="sxs-lookup"><span data-stu-id="38553-219">b.</span></span> <span data-ttu-id="38553-220">Merhaba TCP bağlantı noktaları docker ana bilgisayarınız için sözdizimi aşağıdaki hello kullanarak girin: *[dış bağlantı noktası]*:*[iç bağlantı noktası]*.</span><span class="sxs-lookup"><span data-stu-id="38553-220">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="38553-221">Örneğin, **80:8080** bir dış bağlantı noktası 80 ve hello varsayılan iç yay önyükleme bağlantı noktası 8080 belirtir.</span><span class="sxs-lookup"><span data-stu-id="38553-221">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="38553-222">İç bağlantı noktası (örneğin, hello application.yml dosyasını düzenleyerek) özelleştirdiyseniz, azure'da hello doğru yönlendirme toooccur için toospecify hello bağlantı noktası numarası gerekir.</span><span class="sxs-lookup"><span data-stu-id="38553-222">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="38553-223">c.</span><span class="sxs-lookup"><span data-stu-id="38553-223">c.</span></span> <span data-ttu-id="38553-224">Bu seçenekleri yapılandırdıktan sonra tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="38553-224">After you configure these options, click **Finish**.</span></span>

   ![Azure üzerinde bir Docker kapsayıcısı dağıtma][PU07]

1. <span data-ttu-id="38553-226">Yayımlama Hello Azure Araç Seti sona erdiğinde hello Azure etkinlik günlüğü görüntüler **yayımlanan** hello durumu.</span><span class="sxs-lookup"><span data-stu-id="38553-226">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![Docker ana başarıyla dağıtıldı][PU08]

## <a name="next-steps"></a><span data-ttu-id="38553-228">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="38553-228">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[yay önyükleme]: http://projects.spring.io/spring-boot/
[yay Framework]: https://spring.io/

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
