---
title: "Eclipse için Azure Service Fabric eklentisi | Microsoft Docs"
description: "Eclipse için Service Fabric eklentisini kullanmaya başlayın."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2016
ms.author: saysa
ms.openlocfilehash: 98c1b99972b9ad7a396d72b98e727286f6822e42
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a><span data-ttu-id="3868a-103">Eclipse Java uygulama geliştirmesi için Service Fabric eklentisi</span><span class="sxs-lookup"><span data-stu-id="3868a-103">Service Fabric plug-in for Eclipse Java application development</span></span>
<span data-ttu-id="3868a-104">Eclipse, Java geliştiricileri için en yaygın kullanılan tümleşik geliştirme ortamlarından (IDE’ler) biridir.</span><span class="sxs-lookup"><span data-stu-id="3868a-104">Eclipse is one of the most widely used integrated development environments (IDEs) for Java developers.</span></span> <span data-ttu-id="3868a-105">Bu makalede, Azure Service Fabric ile çalışmak için Eclipse geliştirme ortamınızı ayarlama işlemi ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3868a-105">In this article, we describe how to set up your Eclipse development environment to work with Azure Service Fabric.</span></span> <span data-ttu-id="3868a-106">Service Fabric eklentisini kurma, Service fabric uygulamaları oluşturup Service Fabric uygulamanızı yerel veya Eclipse Neon’daki uzak bir Service Fabric kümesine dağıtma hakkında bilgi edinin yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="3868a-106">Learn how to install the Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application to a local or remote Service Fabric cluster in Eclipse Neon.</span></span>

## <a name="install-or-update-the-service-fabric-plug-in-in-eclipse-neon"></a><span data-ttu-id="3868a-107">Eclipse Neon’da Service Fabric eklentisi yükleme veya güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="3868a-107">Install or update the Service Fabric plug-in in Eclipse Neon</span></span>
<span data-ttu-id="3868a-108">Eclipse'te Service Fabric eklentisi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3868a-108">You can install a Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="3868a-109">Eklenti, Java hizmetleri oluşturup dağıtma işlemini kolaylaştırmaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="3868a-109">The plug-in can help simplify the process of building and deploying Java services.</span></span>

1.  <span data-ttu-id="3868a-110">En son Eclipse Neon sürümüne sahip olduğunuzdan ve en son Buildship sürümünün (1.0.17 veya sonraki bir sürüm) yüklü olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="3868a-110">Ensure that you have the latest version of Eclipse Neon and the latest version of Buildship (1.0.17 or a later version) installed:</span></span>
    -   <span data-ttu-id="3868a-111">**Yardım** > **Yükleme Ayrıntıları**’nı seçerek Eclipse Neon’da yüklü bileşenlerin sürümlerini denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3868a-111">To check the versions of installed components, in Eclipse Neon, go to **Help** > **Installation Details**.</span></span>
    -   <span data-ttu-id="3868a-112">Buildship’i güncelleştirmek için bkz. [Eclipse Buildship: Gradle için Eclipse Eklentileri][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="3868a-112">To update Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>
    -   <span data-ttu-id="3868a-113">Eclipse Neon güncelleştirmelerini denetleyip yüklemek için **Yardım** > **Güncelleştirmeleri Denetle** menüsüne gidin.</span><span class="sxs-lookup"><span data-stu-id="3868a-113">To check for and install updates for Eclipse Neon, go to **Help** > **Check for Updates**.</span></span>

2.  <span data-ttu-id="3868a-114">Service Fabric eklentisini yüklemek için, Eclipse Neon’da **Yardım** > **Yeni Yazılım Yükle**’ye gidin.</span><span class="sxs-lookup"><span data-stu-id="3868a-114">To install the Service Fabric plug-in, in Eclipse Neon, go to **Help** > **Install New Software**.</span></span>
  1.    <span data-ttu-id="3868a-115">**Birlikte çalışın** kutusuna şunu girin: **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="3868a-115">In the **Work with** box, enter **http://dl.microsoft.com/eclipse**.</span></span>
  2.    <span data-ttu-id="3868a-116">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3868a-116">Click **Add**.</span></span>

         ![Eclipse Neon için Service Fabric eklentisi][sf-eclipse-plugin-install]
  3.    <span data-ttu-id="3868a-118">Service Fabric eklentisini seçip **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3868a-118">Select the Service Fabric plug-in, and then click **Next**.</span></span>
  4.    <span data-ttu-id="3868a-119">Yükleme adımlarını tamamlayın ve ardından Microsoft Yazılım Lisans Koşulları’nı kabul edin.</span><span class="sxs-lookup"><span data-stu-id="3868a-119">Complete the installation steps, and then accept the Microsoft Software License Terms.</span></span>

<span data-ttu-id="3868a-120">Service Fabric eklentisi zaten yüklüyse, en yeni sürümü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3868a-120">If you already have the Service Fabric plug-in installed, make sure that you have the latest version.</span></span> <span data-ttu-id="3868a-121">Kullanılabilir güncelleştirmeleri denetlemek için **Yardım** > **Yükleme Ayrıntıları**’na gidin.</span><span class="sxs-lookup"><span data-stu-id="3868a-121">To check for available updates, go to **Help** > **Installation Details**.</span></span> <span data-ttu-id="3868a-122">Yüklü eklentiler listesinde Service Fabric’i seçip **Güncelleştir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3868a-122">In the list of installed plug-ins, select Service Fabric, and then click **Update**.</span></span> <span data-ttu-id="3868a-123">Kullanılabilir güncelleştirmeler yüklenir.</span><span class="sxs-lookup"><span data-stu-id="3868a-123">Available updates will be installed.</span></span>

> [!NOTE]
> <span data-ttu-id="3868a-124">Service Fabric eklentisi yavaş yükleniyor veya güncelleştiriliyorsa, bunun nedeni bir Eclipse ayarı olabilir.</span><span class="sxs-lookup"><span data-stu-id="3868a-124">If installing or updating the Service Fabric plug-in is slow, it might be due to an Eclipse setting.</span></span> <span data-ttu-id="3868a-125">Eclipse, Eclipse örneğinize kaydedilmiş siteleri güncelleştirmek üzere tüm değişikliklere ait meta verileri toplar.</span><span class="sxs-lookup"><span data-stu-id="3868a-125">Eclipse collects metadata on all changes to update sites that are registered with your Eclipse instance.</span></span> <span data-ttu-id="3868a-126">Bir Service Fabric eklenti güncelleştirmesini denetleme ve yükleme işlemini hızlandırmak için **Kullanılabilir Yazılım Siteleri** bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="3868a-126">To speed up the process of checking for and installing a Service Fabric plug-in update, go to **Available Software Sites**.</span></span> <span data-ttu-id="3868a-127">Service Fabric eklenti konumunu (http://dl.microsoft.com/eclipse/azure/servicefabric) işaret eden site dışındaki tüm sitelerin onay kutularını temizleyin.</span><span class="sxs-lookup"><span data-stu-id="3868a-127">Clear the check boxes for all sites except for the one that points to the Service Fabric plug-in location (http://dl.microsoft.com/eclipse/azure/servicefabric).</span></span>

## <a name="create-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="3868a-128">Eclipse’te Service Fabric uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="3868a-128">Create a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="3868a-129">Eclipse Neon’da **Dosya** > **Yeni** > **Diğer** öğesine gidin.</span><span class="sxs-lookup"><span data-stu-id="3868a-129">In Eclipse Neon, go to **File** > **New** > **Other**.</span></span> <span data-ttu-id="3868a-130">**Service Fabric Projesi**’ni seçip **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3868a-130">Select  **Service Fabric Project**, and then click **Next**.</span></span>

    ![Service Fabric Yeni Proje sayfa 1][create-application/p1]

2.  <span data-ttu-id="3868a-132">Projeniz için bir ad girip **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3868a-132">Enter a name for your project, and then click **Next**.</span></span>

    ![Service Fabric Yeni Proje sayfa 2][create-application/p2]

3.  <span data-ttu-id="3868a-134">Şablonlar listesinde **Hizmet Şablonu**’nu seçin.</span><span class="sxs-lookup"><span data-stu-id="3868a-134">In the list of templates, select **Service Template**.</span></span> <span data-ttu-id="3868a-135">Hizmet şablonu türünüzü (Aktör, Durum Bilgisi Olmayan, Kapsayıcı veya Konuk İkili) seçip **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3868a-135">Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.</span></span>

    ![Service Fabric Yeni Proje sayfa 3][create-application/p3]

4.  <span data-ttu-id="3868a-137">Hizmet adını ve hizmet ayrıntılarını girip **Son**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3868a-137">Enter the service name and service details, and then click **Finish**.</span></span>

    ![Service Fabric Yeni Proje sayfa 4][create-application/p4]

5. <span data-ttu-id="3868a-139">İlk Service Fabric projenizi oluşturduktan sonra, **İlişkili Perspektifi Aç** iletişim kutusunda **Evet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3868a-139">When you create your first Service Fabric project, in the **Open Associated Perspective** dialog box, click **Yes**.</span></span>

    ![Service Fabric Yeni Proje sayfa 5][create-application/p5]

6.  <span data-ttu-id="3868a-141">Yeni projeniz şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="3868a-141">Your new project looks like this:</span></span>

    ![Service Fabric Yeni Proje sayfa 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="3868a-143">Eclips’te Service Fabric uygulaması derleme ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="3868a-143">Build and deploy a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="3868a-144">Yeni Service Fabric uygulamanıza sağ tıklayın ve ardından **Service Fabric**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="3868a-144">Right-click your new Service Fabric application, and then select **Service Fabric**.</span></span>

    ![Service Fabric sağ tıklama menüsü][publish/RightClick]

2. <span data-ttu-id="3868a-146">Alt menüde istediğiniz seçeneği belirleyin:</span><span class="sxs-lookup"><span data-stu-id="3868a-146">In the submenu, select the option you want:</span></span>
    -   <span data-ttu-id="3868a-147">Uygulamayı temizlemeden derlemek için **Uygulamayı Derle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3868a-147">To build the application without cleaning, click **Build Application**.</span></span>
    -   <span data-ttu-id="3868a-148">Uygulamanın temiz bir derlemesini gerçekleştirmek için **Uygulamayı Yeniden Derle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3868a-148">To do a clean build of the application, click **Rebuild Application**.</span></span>
    -   <span data-ttu-id="3868a-149">Derlenen yapıtları uygulamadan temizlemek için **Uygulamayı Temizle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3868a-149">To clean the application of built artifacts, click **Clean Application**.</span></span>

3.  <span data-ttu-id="3868a-150">Bu menüden ayrıca uygulamanızı dağıtabilir, dağıtımını kaldırabilir ve yayımlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3868a-150">From this menu, you also can deploy, undeploy, and publish your application:</span></span>
    -   <span data-ttu-id="3868a-151">Yerel kümenize dağıtmak için **Uygulamayı Dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3868a-151">To deploy to your local cluster, click **Deploy Application**.</span></span>
    -   <span data-ttu-id="3868a-152">**Uygulamayı Yayımla** iletişim kutusunda bir yayımlama profili seçin:</span><span class="sxs-lookup"><span data-stu-id="3868a-152">In the **Publish Application** dialog box, select a publish profile:</span></span>
        -  <span data-ttu-id="3868a-153">**Local.json**</span><span class="sxs-lookup"><span data-stu-id="3868a-153">**Local.json**</span></span>
        -  <span data-ttu-id="3868a-154">**Cloud.json**</span><span class="sxs-lookup"><span data-stu-id="3868a-154">**Cloud.json**</span></span>

     <span data-ttu-id="3868a-155">Bu JavaScript Nesne Gösterimi (JSON) dosyaları, yerel veya bulut (Azure) kümenize bağlanmak için gereken bilgileri (bağlantı uç noktaları ve güvenlik bilgileri gibi) depolar.</span><span class="sxs-lookup"><span data-stu-id="3868a-155">These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required to connect to your local or cloud (Azure) cluster.</span></span>

  ![Service Fabric Yayımla menüsü][publish/Publish]

<span data-ttu-id="3868a-157">Service Fabric uygulamanızı dağıtmanın alternatif bir yolu, Eclipse çalıştırma yapılandırmalarının kullanılmasıdır.</span><span class="sxs-lookup"><span data-stu-id="3868a-157">An alternate way to deploy your Service Fabric application is by using Eclipse run configurations.</span></span>

  1.    <span data-ttu-id="3868a-158">**Çalıştır** > **Çalıştırma Yapılandırmaları** öğesine gidin.</span><span class="sxs-lookup"><span data-stu-id="3868a-158">Go to **Run** > **Run Configurations**.</span></span>
  2.    <span data-ttu-id="3868a-159">**Grade Projesi** altındaki **ServiceFabricDeployer** çalıştırma yapılandırmasını seçin.</span><span class="sxs-lookup"><span data-stu-id="3868a-159">Under **Gradle Project**, select the **ServiceFabricDeployer** run configuration.</span></span>
  3.    <span data-ttu-id="3868a-160">Sağ bölmedeki **Bağımsız Değişkenler** sekmesinde **publishProfile** için **yerel** veya **bulut** seçeneğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="3868a-160">In the right pane, on the **Arguments** tab, for **publishProfile**, select **local** or **cloud**.</span></span>  <span data-ttu-id="3868a-161">Varsayılan seçenek **yerel**’dir.</span><span class="sxs-lookup"><span data-stu-id="3868a-161">The default is **local**.</span></span> <span data-ttu-id="3868a-162">Uzak kümeye veya bulut kümesine dağıtmak için **bulut** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="3868a-162">To deploy to a remote or cloud cluster, select **cloud**.</span></span>
  4.    <span data-ttu-id="3868a-163">Yayımlama profillerine doğru bilgilerin doldurulduğundan emin olmak için **Local.json** veya **Cloud.json** dosyasını gereken şekilde düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="3868a-163">To ensure that the proper information is populated in the publish profiles, edit **Local.json** or **Cloud.json** as needed.</span></span> <span data-ttu-id="3868a-164">Uç nokta bilgilerini ve güvenlik kimlik bilgilerini ekleyebilir ya da güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3868a-164">You can add or update endpoint details and security credentials.</span></span>
  5.    <span data-ttu-id="3868a-165">**Çalışma Dizini** öğesinin, dağıtmak istediğiniz uygulamayı işaret ettiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="3868a-165">Ensure that **Working Directory** points to the application you want to deploy.</span></span> <span data-ttu-id="3868a-166">Uygulamayı değiştirmek için, **Çalışma Alanı** düğmesine tıklayın ve istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="3868a-166">To change the application, click the **Workspace** button, and then select the application you want.</span></span>
  6.    <span data-ttu-id="3868a-167">**Uygula** ve ardından **Çalıştır** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3868a-167">Click **Apply**, and then click **Run**.</span></span>

<span data-ttu-id="3868a-168">Uygulamanız birkaç dakika içinde derlenip dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="3868a-168">Your application builds and deploys within a few moments.</span></span> <span data-ttu-id="3868a-169">Dağıtım durumunu Service Fabric Explorer’dan izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3868a-169">You can monitor the deployment status in Service Fabric Explorer.</span></span>  

## <a name="add-a-service-fabric-service-to-your-service-fabric-application"></a><span data-ttu-id="3868a-170">Service Fabric uygulamanıza Service Fabric hizmeti ekleme</span><span class="sxs-lookup"><span data-stu-id="3868a-170">Add a Service Fabric service to your Service Fabric application</span></span>

<span data-ttu-id="3868a-171">Var olan bir Service Fabric uygulamasına Service Fabric hizmeti eklemek için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="3868a-171">To add a Service Fabric service to an existing Service Fabric application, do the following steps:</span></span>

1.  <span data-ttu-id="3868a-172">Hizmet eklemek istediğiniz projeye sağ tıklayın ve ardından **Service Fabric**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3868a-172">Right-click the project you want to add a service to, and then click **Service Fabric**.</span></span>

    ![Service Fabric Hizmet Ekleme sayfa 1][add-service/p1]

2.  <span data-ttu-id="3868a-174">**Service Fabric Hizmeti Ekle**’ye tıklayın ve projeye bir hizmet eklemek için adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="3868a-174">Click **Add Service Fabric Service**, and complete the set of steps to add a service to the project.</span></span>
3.  <span data-ttu-id="3868a-175">Projenize eklemek istediğiniz hizmet şablonunu seçip **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3868a-175">Select the service template you want to add to your project, and then click **Next**.</span></span>

    ![Service Fabric Hizmet Ekleme sayfa 2][add-service/p2]

4.  <span data-ttu-id="3868a-177">Hizmet adını (ve gereken diğer ayrıntıları) girip **Hizmet Ekle** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3868a-177">Enter the service name (and other details, as needed), and then click the **Add Service** button.</span></span>  

    ![Service Fabric Hizmet Ekleme sayfa 3][add-service/p3]

5.  <span data-ttu-id="3868a-179">Hizmet eklendikten sonra projenizin genel yapısı aşağıdaki projeye benzer:</span><span class="sxs-lookup"><span data-stu-id="3868a-179">After the service is added, your overall project structure looks similar to the following project:</span></span>

    ![Service Fabric Hizmet Ekleme sayfa 4][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a><span data-ttu-id="3868a-181">Service Fabric Java uygulamanızın Bildirim sürümlerini düzenleme</span><span class="sxs-lookup"><span data-stu-id="3868a-181">Edit Manifest versions of your Service Fabric Java application</span></span>

<span data-ttu-id="3868a-182">Bildirim sürümlerini düzenlemek için projeye sağ tıklayın, **Service Fabric**'e gidin ve açılan menüden **Bildirim Sürümlerini Düzenle...** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="3868a-182">To edit manifest versions, right click on the project, go to **Service Fabric** and select **Edit Manifest Versions...** from the menu dropdown.</span></span> <span data-ttu-id="3868a-183">Sihirbazda uygulama bildiriminin ve hizmet bildiriminin yanı sıra **Kod**, **Yapılandırma** ve **Veriler** adlı paketlere ilişkin sürümlere yönelik bildirim sürümlerini güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3868a-183">In the wizard, you can update the manifest versions for application manifest, service manifest and the versions for **Code**, **Config** and **Data** packages.</span></span>

<span data-ttu-id="3868a-184">**Uygulama ve hizmet sürümlerini otomatik olarak güncelleştir** seçeneğini işaretler ve ardından bir sürümü güncelleştirirseniz bildirim sürümleri de otomatik olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3868a-184">If you check the option **Automatically update application and service versions** and then update a version, then the manifest versions will be automatically updated.</span></span> <span data-ttu-id="3868a-185">Örneğin, onay kutusunu işaretleyip **Kod** sürümünü 0.0.0'dan 0.0.1'e güncelleştirir ve ardından **Son**'a tıklarsanız hizmet bildirim sürümü ve uygulama bildirim sürümü otomatik olarak 0.0.1'e güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3868a-185">To give an example, you first select the check-box, then update the version of **Code** version from 0.0.0 to 0.0.1 and click on **Finish**, then service manifest version and application manifest version will be automatically updated to 0.0.1.</span></span>

## <a name="upgrade-your-service-fabric-java-application"></a><span data-ttu-id="3868a-186">Service Fabric Java uygulamanızı yükseltme</span><span class="sxs-lookup"><span data-stu-id="3868a-186">Upgrade your Service Fabric Java application</span></span>

<span data-ttu-id="3868a-187">Bir yükseltme senaryosu için, Eclips’te Service Fabric eklentisini kullanarak **App1** projesini oluşturduğunuzu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="3868a-187">For an upgrade scenario, say you created the **App1** project by using the Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="3868a-188">**fabric:/App1Application** adlı bir uygulama oluşturmak için eklentiyi kullanarak projeyi dağıttınız.</span><span class="sxs-lookup"><span data-stu-id="3868a-188">You deployed it by using the plug-in to create an application named **fabric:/App1Application**.</span></span> <span data-ttu-id="3868a-189">Uygulama türü **App1AppicationType**, uygulama sürümü ise 1.0’dır.</span><span class="sxs-lookup"><span data-stu-id="3868a-189">The application type is **App1AppicationType**, and the application version is 1.0.</span></span> <span data-ttu-id="3868a-190">Şimdi de uygulamanızı kesinti olmadan yükseltmek istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="3868a-190">Now, you want to upgrade your application without interrupting availability.</span></span>

<span data-ttu-id="3868a-191">İlk olarak, uygulamanızda değişiklikleri yapın ve değiştirilen hizmeti yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="3868a-191">First, make any changes to your application, and then rebuild the modified service.</span></span> <span data-ttu-id="3868a-192">Değiştirilen hizmetin bildirim dosyasını (ServiceManifest.xml) hizmetin güncel sürümleriyle (ve uygun olan Kod, Yapılandırma ya da Veriler ile) güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3868a-192">Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the service (and Code, Config, or Data, as relevant).</span></span> <span data-ttu-id="3868a-193">Uygulamanın bildirim dosyasını (ApplicationManifest.xml), uygulamanın ve değiştirilen hizmetin güncel sürüm numarasıyla da değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3868a-193">Also, modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application and the modified service.</span></span>  

<span data-ttu-id="3868a-194">Eclipse Neon kullanarak uygulamanızı yükseltmek için, yinelenen bir çalıştırma yapılandırma profili oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3868a-194">To upgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile.</span></span> <span data-ttu-id="3868a-195">Ardından, uygulamanızı gereken şekilde yükseltmek için bu profili kullanın.</span><span class="sxs-lookup"><span data-stu-id="3868a-195">Then, use it to upgrade your application as needed.</span></span>

1.  <span data-ttu-id="3868a-196">**Çalıştır** > **Çalıştırma Yapılandırmaları** öğesine gidin.</span><span class="sxs-lookup"><span data-stu-id="3868a-196">Go to **Run** > **Run Configurations**.</span></span> <span data-ttu-id="3868a-197">Sol bölmede, **Grade Projesi** öğesinin sol tarafında bulunan küçük oka tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3868a-197">In the left pane, click the small arrow to the left of **Gradle Project**.</span></span>
2.  <span data-ttu-id="3868a-198">**ServiceFabricDeployer**’a sağ tıklayıp **Yinelenen**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="3868a-198">Right-click **ServiceFabricDeployer**, and then select **Duplicate**.</span></span> <span data-ttu-id="3868a-199">Bu yapılandırma için **ServiceFabricUpgrader** gibi yeni bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="3868a-199">Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.</span></span>
3.  <span data-ttu-id="3868a-200">Sağ paneldeki **Bağımsız Değişkenler** sekmesinde **-Pconfig='deploy'** değerini **-Pconfig='upgrade'** olarak değiştirip **Uygula**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3868a-200">In the right panel, on the **Arguments** tab, change **-Pconfig='deploy'** to **-Pconfig='upgrade'**, and then click **Apply**.</span></span>

<span data-ttu-id="3868a-201">Bu işlem, uygulamanızı yükseltmek için dilediğiniz zaman kullanabileceğiniz bir çalıştırma yapılandırma profili oluşturup kaydeder.</span><span class="sxs-lookup"><span data-stu-id="3868a-201">This process creates and saves a run configuration profile you can use at any time to upgrade your application.</span></span> <span data-ttu-id="3868a-202">Ayrıca, en son güncelleştirilmiş uygulama türü sürümünü uygulama bildirim dosyasından alır.</span><span class="sxs-lookup"><span data-stu-id="3868a-202">It also gets the latest updated application type version from the application manifest file.</span></span>

<span data-ttu-id="3868a-203">Uygulama yükseltmesi birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="3868a-203">The application upgrade takes a few minutes.</span></span> <span data-ttu-id="3868a-204">Uygulama yükseltme işlemini Service Fabric Explorer’dan izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3868a-204">You can monitor the application upgrade in Service Fabric Explorer.</span></span>

## <a name="migrating-old-service-fabric-java-applications-to-be-used-with-maven"></a><span data-ttu-id="3868a-205">Eski Service Fabric Java uygulamalarını Maven ile kullanılmak üzere geçirme</span><span class="sxs-lookup"><span data-stu-id="3868a-205">Migrating old Service Fabric Java applications to be used with Maven</span></span>
<span data-ttu-id="3868a-206">Service Fabric Java kitaplıklarını yakın zamanda Service Fabric Java SDK’sından Maven deposuna taşıdık.</span><span class="sxs-lookup"><span data-stu-id="3868a-206">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK to Maven repository.</span></span> <span data-ttu-id="3868a-207">Eclipse kullanarak oluşturduğunuz yeni uygulamalar en son güncelleştirilen projeleri oluşturur (Maven ile çalışırlar), ancak daha önce Service Fabric Java SDK’sı kullanan mevcut Service Fabric durum bilgisi olmayan ya da aktör Java uygulamalarını Maven’ın Service Fabric Java bağımlılıklarını kullanacak şekilde güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3868a-207">While the new applications you generate using Eclipse, will generate latest updated projects (which will be able to work with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using the Service Fabric Java SDK earlier, to use the Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="3868a-208">Eski uygulamanızın Maven ile çalıştığından emin olmak için lütfen [burada](service-fabric-migrate-old-javaapp-to-use-maven.md) belirtilen adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="3868a-208">Please follow the steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) to ensure your older application works with Maven.</span></span>

<!-- Images -->

[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-eclipse/service-fabric-eclipse-plugin.png

[create-application/p1]:./media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:./media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:./media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:./media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:./media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:./media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: ./media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: ./media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: ./media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: ./media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: ./media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: ./media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
