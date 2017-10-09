---
title: "Service Fabric Eclipse için eklenti aaaAzure | Microsoft Docs"
description: "Service Fabric eklenti Hello ile Eclipse için kullanmaya başlayın."
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
ms.openlocfilehash: 4ba5a28a6282387249a2bd4e62314e891ff04162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a><span data-ttu-id="20378-103">Eclipse Java uygulama geliştirmesi için Service Fabric eklentisi</span><span class="sxs-lookup"><span data-stu-id="20378-103">Service Fabric plug-in for Eclipse Java application development</span></span>
<span data-ttu-id="20378-104">Eclipse en yaygın olarak kullanılan hello biridir Java geliştiriciler için tümleşik geliştirme ortamlarını (IDE).</span><span class="sxs-lookup"><span data-stu-id="20378-104">Eclipse is one of hello most widely used integrated development environments (IDEs) for Java developers.</span></span> <span data-ttu-id="20378-105">Bu makalede, sizi tanımlamak nasıl tooset, Eclipse geliştirme ortamı toowork Azure Service Fabric ile ayarlama.</span><span class="sxs-lookup"><span data-stu-id="20378-105">In this article, we describe how tooset up your Eclipse development environment toowork with Azure Service Fabric.</span></span> <span data-ttu-id="20378-106">Tooinstall hello Service Fabric eklentisi, Service Fabric uygulaması oluşturma ve Service Fabric uygulaması tooa yerel veya uzak Service Fabric kümenizdeki Eclipse Neon dağıtmak öğrenin.</span><span class="sxs-lookup"><span data-stu-id="20378-106">Learn how tooinstall hello Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application tooa local or remote Service Fabric cluster in Eclipse Neon.</span></span>

## <a name="install-or-update-hello-service-fabric-plug-in-in-eclipse-neon"></a><span data-ttu-id="20378-107">Yükleme veya hello Service Fabric Eclipse Neon eklenti güncelleştir</span><span class="sxs-lookup"><span data-stu-id="20378-107">Install or update hello Service Fabric plug-in in Eclipse Neon</span></span>
<span data-ttu-id="20378-108">Eclipse'te Service Fabric eklentisi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20378-108">You can install a Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="20378-109">Merhaba eklentisi oluşturma ve Java Hizmetleri dağıtma hello işlemini kolaylaştırmaya yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="20378-109">hello plug-in can help simplify hello process of building and deploying Java services.</span></span>

1.  <span data-ttu-id="20378-110">Eclipse Neon hello en son sürümünü ve en son sürümünü Buildship hello olduğundan emin olun (1.0.17 veya sonraki bir sürümü) yüklü:</span><span class="sxs-lookup"><span data-stu-id="20378-110">Ensure that you have hello latest version of Eclipse Neon and hello latest version of Buildship (1.0.17 or a later version) installed:</span></span>
    -   <span data-ttu-id="20378-111">Eclipse Neon içinde yüklü bileşenlerin toocheck hello sürümleri Git çok**yardımcı** > **Yükleme ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="20378-111">toocheck hello versions of installed components, in Eclipse Neon, go too**Help** > **Installation Details**.</span></span>
    -   <span data-ttu-id="20378-112">tooupdate Buildship, bkz: [Eclipse Buildship: Eclipse için eklentilerini Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="20378-112">tooupdate Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>
    -   <span data-ttu-id="20378-113">için toocheck ve güncelleştirmeleri yükleme için Eclipse Neon Git çok**yardımcı** > **Güncelleştirmeleri denetle**.</span><span class="sxs-lookup"><span data-stu-id="20378-113">toocheck for and install updates for Eclipse Neon, go too**Help** > **Check for Updates**.</span></span>

2.  <span data-ttu-id="20378-114">tooinstall hello Service Fabric Eclipse Neon içinde eklenti Git çok**yardımcı** > **yeni yazılımı yükle**.</span><span class="sxs-lookup"><span data-stu-id="20378-114">tooinstall hello Service Fabric plug-in, in Eclipse Neon, go too**Help** > **Install New Software**.</span></span>
  1.    <span data-ttu-id="20378-115">Merhaba, **çalışmak** kutusuna **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="20378-115">In hello **Work with** box, enter **http://dl.microsoft.com/eclipse**.</span></span>
  2.    <span data-ttu-id="20378-116">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="20378-116">Click **Add**.</span></span>

         ![Eclipse Neon için Service Fabric eklentisi][sf-eclipse-plugin-install]
  3.    <span data-ttu-id="20378-118">Merhaba Service Fabric eklenti seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="20378-118">Select hello Service Fabric plug-in, and then click **Next**.</span></span>
  4.    <span data-ttu-id="20378-119">Merhaba yükleme adımlarını tamamlayın ve hello Microsoft Yazılımı Lisans koşulları kabul edin.</span><span class="sxs-lookup"><span data-stu-id="20378-119">Complete hello installation steps, and then accept hello Microsoft Software License Terms.</span></span>

<span data-ttu-id="20378-120">Hello Service yüklü Fabric eklenti zaten varsa, hello en son sürümüne sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="20378-120">If you already have hello Service Fabric plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="20378-121">kullanılabilir güncelleştirmeleri toocheck Git çok**yardımcı** > **Yükleme ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="20378-121">toocheck for available updates, go too**Help** > **Installation Details**.</span></span> <span data-ttu-id="20378-122">Yüklü eklentileri listesi Merhaba, Service Fabric seçin ve ardından **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="20378-122">In hello list of installed plug-ins, select Service Fabric, and then click **Update**.</span></span> <span data-ttu-id="20378-123">Kullanılabilir güncelleştirmeler yüklenir.</span><span class="sxs-lookup"><span data-stu-id="20378-123">Available updates will be installed.</span></span>

> [!NOTE]
> <span data-ttu-id="20378-124">Yükleme veya hello Service Fabric eklenti güncelleştirme yavaşsa, tooan Eclipse ayarı nedeniyle olabilir.</span><span class="sxs-lookup"><span data-stu-id="20378-124">If installing or updating hello Service Fabric plug-in is slow, it might be due tooan Eclipse setting.</span></span> <span data-ttu-id="20378-125">Eclipse Eclipse örneğinizle kayıtlı tüm değişiklikleri tooupdate sitelerindeki meta verileri toplar.</span><span class="sxs-lookup"><span data-stu-id="20378-125">Eclipse collects metadata on all changes tooupdate sites that are registered with your Eclipse instance.</span></span> <span data-ttu-id="20378-126">toospeed denetleniyor ve Service Fabric eklenti güncelleştirmeyi yükleme işlemini hello Git çok**kullanılabilir yazılım siteleri**.</span><span class="sxs-lookup"><span data-stu-id="20378-126">toospeed up hello process of checking for and installing a Service Fabric plug-in update, go too**Available Software Sites**.</span></span> <span data-ttu-id="20378-127">Merhaba toohello Service Fabric eklenti konumu (http://dl.microsoft.com/eclipse/azure/servicefabric) işaret eden bir dışında tüm siteler için Hello onay kutularını temizleyin.</span><span class="sxs-lookup"><span data-stu-id="20378-127">Clear hello check boxes for all sites except for hello one that points toohello Service Fabric plug-in location (http://dl.microsoft.com/eclipse/azure/servicefabric).</span></span>

## <a name="create-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="20378-128">Eclipse’te Service Fabric uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="20378-128">Create a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="20378-129">Eclipse Neon içinde çok Git**dosya** > **yeni** > **diğer**.</span><span class="sxs-lookup"><span data-stu-id="20378-129">In Eclipse Neon, go too**File** > **New** > **Other**.</span></span> <span data-ttu-id="20378-130">**Service Fabric Projesi**’ni seçip **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="20378-130">Select  **Service Fabric Project**, and then click **Next**.</span></span>

    ![Service Fabric Yeni Proje sayfa 1][create-application/p1]

2.  <span data-ttu-id="20378-132">Projeniz için bir ad girip **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="20378-132">Enter a name for your project, and then click **Next**.</span></span>

    ![Service Fabric Yeni Proje sayfa 2][create-application/p2]

3.  <span data-ttu-id="20378-134">Şablonları Hello listesinde seçin **hizmet şablonu**.</span><span class="sxs-lookup"><span data-stu-id="20378-134">In hello list of templates, select **Service Template**.</span></span> <span data-ttu-id="20378-135">Hizmet şablonu türünüzü (Aktör, Durum Bilgisi Olmayan, Kapsayıcı veya Konuk İkili) seçip **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="20378-135">Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.</span></span>

    ![Service Fabric Yeni Proje sayfa 3][create-application/p3]

4.  <span data-ttu-id="20378-137">Merhaba hizmet adı girin ve hizmet ayrıntılarını ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="20378-137">Enter hello service name and service details, and then click **Finish**.</span></span>

    ![Service Fabric Yeni Proje sayfa 4][create-application/p4]

5. <span data-ttu-id="20378-139">Hello ilk Service Fabric projenizi oluşturduğunuzda **açık ilişkili perspektif** iletişim kutusu, tıklatın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="20378-139">When you create your first Service Fabric project, in hello **Open Associated Perspective** dialog box, click **Yes**.</span></span>

    ![Service Fabric Yeni Proje sayfa 5][create-application/p5]

6.  <span data-ttu-id="20378-141">Yeni projeniz şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="20378-141">Your new project looks like this:</span></span>

    ![Service Fabric Yeni Proje sayfa 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="20378-143">Eclips’te Service Fabric uygulaması derleme ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="20378-143">Build and deploy a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="20378-144">Yeni Service Fabric uygulamanıza sağ tıklayın ve ardından **Service Fabric**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="20378-144">Right-click your new Service Fabric application, and then select **Service Fabric**.</span></span>

    ![Service Fabric sağ tıklama menüsü][publish/RightClick]

2. <span data-ttu-id="20378-146">Merhaba alt menüde hello seçeneği belirleyin:</span><span class="sxs-lookup"><span data-stu-id="20378-146">In hello submenu, select hello option you want:</span></span>
    -   <span data-ttu-id="20378-147">Temizleme, olmadan toobuild hello uygulama'yı tıklatın **yapı uygulama**.</span><span class="sxs-lookup"><span data-stu-id="20378-147">toobuild hello application without cleaning, click **Build Application**.</span></span>
    -   <span data-ttu-id="20378-148">toodo hello uygulamasının temiz bir yapı tıklatın **yeniden uygulama**.</span><span class="sxs-lookup"><span data-stu-id="20378-148">toodo a clean build of hello application, click **Rebuild Application**.</span></span>
    -   <span data-ttu-id="20378-149">Yerleşik yapılarının tooclean hello uygulama'yı tıklatın **temiz uygulama**.</span><span class="sxs-lookup"><span data-stu-id="20378-149">tooclean hello application of built artifacts, click **Clean Application**.</span></span>

3.  <span data-ttu-id="20378-150">Bu menüden ayrıca uygulamanızı dağıtabilir, dağıtımını kaldırabilir ve yayımlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="20378-150">From this menu, you also can deploy, undeploy, and publish your application:</span></span>
    -   <span data-ttu-id="20378-151">toodeploy tooyour yerel küme, tıklatın **dağıtmak uygulama**.</span><span class="sxs-lookup"><span data-stu-id="20378-151">toodeploy tooyour local cluster, click **Deploy Application**.</span></span>
    -   <span data-ttu-id="20378-152">Merhaba, **uygulamasını Yayımla** iletişim kutusunda, bir yayımlama profili seçin:</span><span class="sxs-lookup"><span data-stu-id="20378-152">In hello **Publish Application** dialog box, select a publish profile:</span></span>
        -  <span data-ttu-id="20378-153">**Local.json**</span><span class="sxs-lookup"><span data-stu-id="20378-153">**Local.json**</span></span>
        -  <span data-ttu-id="20378-154">**Cloud.json**</span><span class="sxs-lookup"><span data-stu-id="20378-154">**Cloud.json**</span></span>

     <span data-ttu-id="20378-155">Bu JavaScript nesne gösterimi (JSON) dosyaları gerekli tooconnect tooyour yerel veya buluta (Azure'a) küme bilgilerini (örneğin, bağlantı uç ve güvenlik bilgileri) depolar.</span><span class="sxs-lookup"><span data-stu-id="20378-155">These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required tooconnect tooyour local or cloud (Azure) cluster.</span></span>

  ![Service Fabric Yayımla menüsü][publish/Publish]

<span data-ttu-id="20378-157">Bir alternatif bir yol toodeploy yapılandırmaları Service Fabric uygulamanızı Eclipse kullanılarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="20378-157">An alternate way toodeploy your Service Fabric application is by using Eclipse run configurations.</span></span>

  1.    <span data-ttu-id="20378-158">Çok Git**çalıştırmak** > **yapılandırmaları Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="20378-158">Go too**Run** > **Run Configurations**.</span></span>
  2.    <span data-ttu-id="20378-159">Altında **Gradle proje**seçin hello **ServiceFabricDeployer** yapılandırma çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="20378-159">Under **Gradle Project**, select hello **ServiceFabricDeployer** run configuration.</span></span>
  3.    <span data-ttu-id="20378-160">Merhaba üzerinde hello sağ bölmede **bağımsız değişkenleri** sekmesinde için **publishProfile**seçin **yerel** veya **bulut**.</span><span class="sxs-lookup"><span data-stu-id="20378-160">In hello right pane, on hello **Arguments** tab, for **publishProfile**, select **local** or **cloud**.</span></span>  <span data-ttu-id="20378-161">Merhaba varsayılandır **yerel**.</span><span class="sxs-lookup"><span data-stu-id="20378-161">hello default is **local**.</span></span> <span data-ttu-id="20378-162">Uzak toodeploy tooa veya Bulut küme, select **bulut**.</span><span class="sxs-lookup"><span data-stu-id="20378-162">toodeploy tooa remote or cloud cluster, select **cloud**.</span></span>
  4.    <span data-ttu-id="20378-163">Merhaba uygun bilgileri hello doldurulur tooensure yayımlama profillerini, düzenleme **Local.json** veya **Cloud.json** gerektiğinde.</span><span class="sxs-lookup"><span data-stu-id="20378-163">tooensure that hello proper information is populated in hello publish profiles, edit **Local.json** or **Cloud.json** as needed.</span></span> <span data-ttu-id="20378-164">Uç nokta bilgilerini ve güvenlik kimlik bilgilerini ekleyebilir ya da güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20378-164">You can add or update endpoint details and security credentials.</span></span>
  5.    <span data-ttu-id="20378-165">Emin **çalışma dizini** toohello uygulamasıyla toodeploy işaret eder.</span><span class="sxs-lookup"><span data-stu-id="20378-165">Ensure that **Working Directory** points toohello application you want toodeploy.</span></span> <span data-ttu-id="20378-166">toochange Merhaba uygulama, hello tıklatın **çalışma** düğmesine tıklayın ve ardından istediğiniz hello uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="20378-166">toochange hello application, click hello **Workspace** button, and then select hello application you want.</span></span>
  6.    <span data-ttu-id="20378-167">**Uygula** ve ardından **Çalıştır** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="20378-167">Click **Apply**, and then click **Run**.</span></span>

<span data-ttu-id="20378-168">Uygulamanız birkaç dakika içinde derlenip dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="20378-168">Your application builds and deploys within a few moments.</span></span> <span data-ttu-id="20378-169">Service Fabric Explorer hello dağıtım durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20378-169">You can monitor hello deployment status in Service Fabric Explorer.</span></span>  

## <a name="add-a-service-fabric-service-tooyour-service-fabric-application"></a><span data-ttu-id="20378-170">Service Fabric hizmeti tooyour Service Fabric uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="20378-170">Add a Service Fabric service tooyour Service Fabric application</span></span>

<span data-ttu-id="20378-171">tooadd bir Service Fabric hizmeti tooan mevcut Service Fabric uygulaması, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="20378-171">tooadd a Service Fabric service tooan existing Service Fabric application, do hello following steps:</span></span>

1.  <span data-ttu-id="20378-172">Bir hizmete tooadd istediğiniz ve ardından sağ hello proje **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="20378-172">Right-click hello project you want tooadd a service to, and then click **Service Fabric**.</span></span>

    ![Service Fabric Hizmet Ekleme sayfa 1][add-service/p1]

2.  <span data-ttu-id="20378-174">Tıklatın **Service Fabric Hizmet Ekle**, ve tam hello hizmeti toohello projesi adımları tooadd ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="20378-174">Click **Add Service Fabric Service**, and complete hello set of steps tooadd a service toohello project.</span></span>
3.  <span data-ttu-id="20378-175">Tooadd tooyour proje istediğiniz ve ardından select hello hizmet şablonu **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="20378-175">Select hello service template you want tooadd tooyour project, and then click **Next**.</span></span>

    ![Service Fabric Hizmet Ekleme sayfa 2][add-service/p2]

4.  <span data-ttu-id="20378-177">Hello hizmet adı (ve diğer ayrıntıları gerektiği gibi) girin ve hello ardından **Hizmet Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="20378-177">Enter hello service name (and other details, as needed), and then click hello **Add Service** button.</span></span>  

    ![Service Fabric Hizmet Ekleme sayfa 3][add-service/p3]

5.  <span data-ttu-id="20378-179">Merhaba hizmet eklendikten sonra genel proje yapınızı proje aşağıdaki benzer toohello görünür:</span><span class="sxs-lookup"><span data-stu-id="20378-179">After hello service is added, your overall project structure looks similar toohello following project:</span></span>

    ![Service Fabric Hizmet Ekleme sayfa 4][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a><span data-ttu-id="20378-181">Service Fabric Java uygulamanızın Bildirim sürümlerini düzenleme</span><span class="sxs-lookup"><span data-stu-id="20378-181">Edit Manifest versions of your Service Fabric Java application</span></span>

<span data-ttu-id="20378-182">tooedit bildirim sürümleri hello projeye sağ tıklayın, çok Git**Service Fabric** seçip **bildirim sürümleri Düzenle...**  gelen hello menüsü açılır.</span><span class="sxs-lookup"><span data-stu-id="20378-182">tooedit manifest versions, right click on hello project, go too**Service Fabric** and select **Edit Manifest Versions...** from hello menu dropdown.</span></span> <span data-ttu-id="20378-183">Başlangıç Sihirbazı'nda hello bildirim uygulama bildirimi, hizmet bildirimi için ve hello sürümleri için güncelleştirebilirsiniz **kod**, **Config** ve **veri** paketler.</span><span class="sxs-lookup"><span data-stu-id="20378-183">In hello wizard, you can update hello manifest versions for application manifest, service manifest and hello versions for **Code**, **Config** and **Data** packages.</span></span>

<span data-ttu-id="20378-184">Merhaba seçeneğini işaretlerseniz **otomatik olarak uygulama ve hizmet sürümleri güncelleştirme** ve bir sürümüne güncelleştirin, ardından hello bildirim sürümlerini otomatik olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="20378-184">If you check hello option **Automatically update application and service versions** and then update a version, then hello manifest versions will be automatically updated.</span></span> <span data-ttu-id="20378-185">toogive örnek ilk seçtiğiniz hello onay kutusunu ve ardından güncelleştirme hello sürümü **kod** 0.0.0 sürümünden too0.0.1 ve tıklayarak **son**, bildirimi sürümü ve uygulama bildirimi hizmeti sürümü otomatik olarak güncelleştirilen too0.0.1 olacaktır.</span><span class="sxs-lookup"><span data-stu-id="20378-185">toogive an example, you first select hello check-box, then update hello version of **Code** version from 0.0.0 too0.0.1 and click on **Finish**, then service manifest version and application manifest version will be automatically updated too0.0.1.</span></span>

## <a name="upgrade-your-service-fabric-java-application"></a><span data-ttu-id="20378-186">Service Fabric Java uygulamanızı yükseltme</span><span class="sxs-lookup"><span data-stu-id="20378-186">Upgrade your Service Fabric Java application</span></span>

<span data-ttu-id="20378-187">Bir yükseltme senaryosu için oluşturduğunuz hello söyleyin **App1** hello Service Fabric Eclipse'te eklentisini kullanarak proje.</span><span class="sxs-lookup"><span data-stu-id="20378-187">For an upgrade scenario, say you created hello **App1** project by using hello Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="20378-188">Merhaba eklenti toocreate kullanarak adlı bir uygulama dağıttıktan **fabric: / App1Application**.</span><span class="sxs-lookup"><span data-stu-id="20378-188">You deployed it by using hello plug-in toocreate an application named **fabric:/App1Application**.</span></span> <span data-ttu-id="20378-189">Merhaba uygulama türü **App1AppicationType**, ve hello uygulama sürümü 1.0.</span><span class="sxs-lookup"><span data-stu-id="20378-189">hello application type is **App1AppicationType**, and hello application version is 1.0.</span></span> <span data-ttu-id="20378-190">Şimdi, kullanılabilirliğini kesintiye uğratmadan uygulamanızı tooupgrade istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="20378-190">Now, you want tooupgrade your application without interrupting availability.</span></span>

<span data-ttu-id="20378-191">İlk olarak, herhangi bir değişiklik tooyour uygulama ve değiştiren hello hizmeti yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="20378-191">First, make any changes tooyour application, and then rebuild hello modified service.</span></span> <span data-ttu-id="20378-192">Güncelleştirme hello hello hizmeti (ve kod, yapılandırma veya ilgili olarak veri) için güncelleştirilmiş hello sürümleri ile hizmetin bildirim dosyası (ServiceManifest.xml) değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="20378-192">Update hello modified service’s manifest file (ServiceManifest.xml) with hello updated versions for hello service (and Code, Config, or Data, as relevant).</span></span> <span data-ttu-id="20378-193">Ayrıca, güncelleştirilmiş hello sürüm numarasıyla Merhaba uygulaması için hello uygulama bildirimi (ApplicationManifest.xml) değiştirin ve değiştirilen hizmet hello.</span><span class="sxs-lookup"><span data-stu-id="20378-193">Also, modify hello application’s manifest (ApplicationManifest.xml) with hello updated version number for hello application and hello modified service.</span></span>  

<span data-ttu-id="20378-194">tooupgrade Eclipse Neon kullanarak uygulamanızı yinelenen çalıştırma yapılandırma profili oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20378-194">tooupgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile.</span></span> <span data-ttu-id="20378-195">Ardından tooupgrade kullanın uygulamanız gerektiğinde.</span><span class="sxs-lookup"><span data-stu-id="20378-195">Then, use it tooupgrade your application as needed.</span></span>

1.  <span data-ttu-id="20378-196">Çok Git**çalıştırmak** > **yapılandırmaları Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="20378-196">Go too**Run** > **Run Configurations**.</span></span> <span data-ttu-id="20378-197">Hello sol hello küçük oka toohello solundaki bölmesinde **Gradle proje**.</span><span class="sxs-lookup"><span data-stu-id="20378-197">In hello left pane, click hello small arrow toohello left of **Gradle Project**.</span></span>
2.  <span data-ttu-id="20378-198">**ServiceFabricDeployer**’a sağ tıklayıp **Yinelenen**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="20378-198">Right-click **ServiceFabricDeployer**, and then select **Duplicate**.</span></span> <span data-ttu-id="20378-199">Bu yapılandırma için **ServiceFabricUpgrader** gibi yeni bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="20378-199">Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.</span></span>
3.  <span data-ttu-id="20378-200">Merhaba sağ masasındaki hello **bağımsız değişkenleri** sekmesinde, değiştirmek **- Pconfig 'dağıtma' =** çok**- Pconfig 'yükseltme' =**ve ardından **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="20378-200">In hello right panel, on hello **Arguments** tab, change **-Pconfig='deploy'** too**-Pconfig='upgrade'**, and then click **Apply**.</span></span>

<span data-ttu-id="20378-201">Bu işlem oluşturur ve bir çalışma yapılandırma profili kaydeder uygulamanız hiçbir zaman tooupgrade kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="20378-201">This process creates and saves a run configuration profile you can use at any time tooupgrade your application.</span></span> <span data-ttu-id="20378-202">Ayrıca hello en son güncelleştirilen uygulama türü sürümü hello uygulama bildirim dosyasından alır.</span><span class="sxs-lookup"><span data-stu-id="20378-202">It also gets hello latest updated application type version from hello application manifest file.</span></span>

<span data-ttu-id="20378-203">Merhaba uygulama yükseltme, birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="20378-203">hello application upgrade takes a few minutes.</span></span> <span data-ttu-id="20378-204">Service Fabric Explorer'da uygulama yükseltme hello izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20378-204">You can monitor hello application upgrade in Service Fabric Explorer.</span></span>

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="20378-205">Maven ile kullanılan eski Service Fabric Java uygulamaları toobe geçirme</span><span class="sxs-lookup"><span data-stu-id="20378-205">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="20378-206">Service Fabric Java kitaplıkları yakın zamanda Service Fabric Java SDK tooMaven depodan taşınmış.</span><span class="sxs-lookup"><span data-stu-id="20378-206">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="20378-207">Eclipse, kullanarak Oluştur hello yeni uygulamalar üretir (Maven ile mümkün toowork olacaktır) en son güncelleştirilen projeleri, ancak varolan Service Fabric durum bilgisiz veya hello Service Fabric Java SDK kullanmakta olduğunuz aktör Java uygulamalarını güncelleştirebilirsiniz önceki sürümlerde, toouse hello Service Fabric Java bağımlılıklardan Maven.</span><span class="sxs-lookup"><span data-stu-id="20378-207">While hello new applications you generate using Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="20378-208">Lütfen belirtilen hello adımları [burada](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure eski uygulamanızı Maven ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="20378-208">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

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
