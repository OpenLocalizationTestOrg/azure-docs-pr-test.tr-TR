---
title: "aaaCreate Intellij temel Azure web uygulamasında | Microsoft Docs"
description: "Bu öğretici nasıl toouse hello Azure Araç Seti için Intellij toocreate bir Hello World Web uygulaması için Azure gösterir."
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4667497213cac3ddf754d164e614c809f338cce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="7f582-103">Intellij içinde bir temel Azure web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f582-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="7f582-104">Bu öğreticide gösterilmiştir nasıl toocreate ve hello kullanarak bir Web uygulaması gibi temel bir Hello World uygulama tooAzure dağıtma [Intellij için Azure Araç Seti].</span><span class="sxs-lookup"><span data-stu-id="7f582-104">This tutorial shows how toocreate and deploy a basic Hello World application tooAzure as a Web App by using hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="7f582-105">Kolaylık olması için temel bir JSP örneği gösterilir, ancak Azure dağıtım ilgili olduğu kadar benzer adımlar bir Java servlet için uygun olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7f582-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="7f582-106">Bu öğreticiyi tamamladıktan sonra uygulamanızı bir web tarayıcısında görüntülediğinizde çizim aşağıdaki benzer toohello görünür:</span><span class="sxs-lookup"><span data-stu-id="7f582-106">When you have completed this tutorial, your application will look similar toohello following illustration when you view it in a web browser:</span></span>

![Örnek bir Web sayfası][01]

## <a name="prerequisites"></a><span data-ttu-id="7f582-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7f582-108">Prerequisites</span></span>
* <span data-ttu-id="7f582-109">Bir Java Geliştirme Seti (JDK), v 1.8 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="7f582-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="7f582-110">Intellij Idea Ultimate Edition.</span><span class="sxs-lookup"><span data-stu-id="7f582-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="7f582-111">Bu adresten yüklenebilir <https://www.jetbrains.com/idea/download/index.html>.</span><span class="sxs-lookup"><span data-stu-id="7f582-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="7f582-112">Dağıtım bir Java tabanlı web sunucusu veya uygulama sunucusu gibi [Apache Tomcat] veya [Jetty].</span><span class="sxs-lookup"><span data-stu-id="7f582-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="7f582-113">Öğesinden alınan bir Azure aboneliği <https://azure.microsoft.com/free/> veya <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="7f582-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="7f582-114">Merhaba [Intellij için Azure Araç Seti].</span><span class="sxs-lookup"><span data-stu-id="7f582-114">hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="7f582-115">Hello Azure araç setini yükleme hakkında daha fazla bilgi için bkz: [yükleme hello Intellij için Azure Araç Seti].</span><span class="sxs-lookup"><span data-stu-id="7f582-115">For information about installing hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="7f582-116">toocreate Merhaba Dünya uygulaması</span><span class="sxs-lookup"><span data-stu-id="7f582-116">toocreate a Hello World application</span></span>
<span data-ttu-id="7f582-117">İlk olarak, bir Java projesi oluşturma ile başlayacağız devre dışı.</span><span class="sxs-lookup"><span data-stu-id="7f582-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="7f582-118">Intellij başlatın ve hello tıklatın **dosya** menüsünde, ardından **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="7f582-118">Start IntelliJ and click hello **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![Dosya yeni proje][02]
2. <span data-ttu-id="7f582-120">Merhaba yeni proje iletişim kutusunda seçin **Java**, ardından **Web uygulaması**ve ardından **yeni** tooadd proje SDK.</span><span class="sxs-lookup"><span data-stu-id="7f582-120">In hello New Project dialog box, select **Java**, then **Web Application**, and then click **New** tooadd a Project SDK.</span></span>
   
    ![Yeni Proje İletişim Kutusu][03a]
   
3. <span data-ttu-id="7f582-122">JDK iletişim kutusu için Hello giriş dizini seçin, select Merhaba, JDK yüklendiği klasörü ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7f582-122">In hello Select Home Directory for JDK dialog box, select hello folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="7f582-123">Tıklatın **sonraki** hello yeni proje iletişim kutusu toocontinue içinde.</span><span class="sxs-lookup"><span data-stu-id="7f582-123">Click **Next** in hello New Project dialog box toocontinue.</span></span>
   
    ![JDK giriş dizini belirtin][03b]
4. <span data-ttu-id="7f582-125">Bu öğreticinin amaçları doğrultusunda hello proje adı **Java-Web-App-üzerinde-Azure**ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="7f582-125">For purposes of this tutorial, name hello project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![Yeni Proje İletişim Kutusu][04]
5. <span data-ttu-id="7f582-127">Intellij'ın Proje Gezgini görünümü içinde genişletmek **Java-Web-App-üzerinde-Azure**, ardından **web**, çift tıklayın ve ardından **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="7f582-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![Açık dizin sayfası][05c]
6. <span data-ttu-id="7f582-129">İndex.jsp dosyası içinde Intellij açıldığında, metin toodynamically görünümünde eklemek **Merhaba Dünya!**</span><span class="sxs-lookup"><span data-stu-id="7f582-129">When your index.jsp file opens in IntelliJ, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="7f582-130">Merhaba varolan içinde `<body>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="7f582-130">within hello existing `<body>` element.</span></span> <span data-ttu-id="7f582-131">Güncelleştirilmiş `<body>` içeriği aşağıdaki örneğine hello benzer:</span><span class="sxs-lookup"><span data-stu-id="7f582-131">Your updated `<body>` content should resemble hello following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="7f582-132">İndex.jsp kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7f582-132">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a><span data-ttu-id="7f582-133">toodeploy, uygulama tooan Azure Web uygulaması kapsayıcısı</span><span class="sxs-lookup"><span data-stu-id="7f582-133">toodeploy your application tooan Azure Web App Container</span></span>
<span data-ttu-id="7f582-134">Java web uygulaması tooAzure dağıtabilir miyim birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="7f582-134">There are several ways by which you can deploy a Java web application tooAzure.</span></span> <span data-ttu-id="7f582-135">Bu öğretici hello basit açıklar: uygulamanızı dağıtılan tooan Azure Web uygulaması kapsayıcı olacaktır - hiçbir özel Proje türü ya da ek araçlar gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7f582-135">This tutorial describes one of hello simplest: your application will be deployed tooan Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="7f582-136">Merhaba JDK ve hello web kapsayıcısı yazılım; böylece hiçbir gerek tooupload kendi sizin için Azure tarafından sağlanacak; ihtiyacınız olan tek şey, Java Web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="7f582-136">hello JDK and hello web container software will be provided for you by Azure, so there is no need tooupload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="7f582-137">Sonuç olarak, uygulamanız için yayımlama işlemi hello saniye, dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="7f582-137">As a result, hello publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="7f582-138">Uygulamanızı yayınlamadan önce modülü ayarlarınızı ilk tooconfigure gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f582-138">Before you publish your application, you first need tooconfigure your module settings.</span></span> <span data-ttu-id="7f582-139">toodo, bu nedenle, hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="7f582-139">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="7f582-140">Intellij'ın Proje Gezgini'nde hello sağ **Java-Web-App-üzerinde-Azure** projesi.</span><span class="sxs-lookup"><span data-stu-id="7f582-140">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="7f582-141">Merhaba bağlam menüsü görüntülendiğinde **açık modülü ayarları**.</span><span class="sxs-lookup"><span data-stu-id="7f582-141">When hello context menu appears, click **Open Module Settings**.</span></span>

    ![Modül Ayarları'nı açın][05a]
2. <span data-ttu-id="7f582-143">Merhaba Proje Yapısı iletişim kutusu görüntülendiğinde:</span><span class="sxs-lookup"><span data-stu-id="7f582-143">When hello Project Structure dialog box appears:</span></span>

   <span data-ttu-id="7f582-144">a.</span><span class="sxs-lookup"><span data-stu-id="7f582-144">a.</span></span> <span data-ttu-id="7f582-145">Tıklatın **yapıları** hello listesinde **proje ayarları**.</span><span class="sxs-lookup"><span data-stu-id="7f582-145">Click **Artifacts** in hello list of **Project Settings**.</span></span>
   <span data-ttu-id="7f582-146">b.</span><span class="sxs-lookup"><span data-stu-id="7f582-146">b.</span></span> <span data-ttu-id="7f582-147">Merhaba hello yapı adını değiştir **adı** boşluk veya özel karakterler içermiyor kutusuna; hello adı hello Tekdüzen Kaynak Tanımlayıcısı (URI) kullanılacağından bu gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7f582-147">Change hello artifact name in hello **Name** box so that it doesn't contain whitespace or special characters; this is necessary since hello name will be used in hello Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="7f582-148">c.</span><span class="sxs-lookup"><span data-stu-id="7f582-148">c.</span></span> <span data-ttu-id="7f582-149">Değişiklik hello **türü** çok**Web uygulaması: Arşiv**.</span><span class="sxs-lookup"><span data-stu-id="7f582-149">Change hello **Type** too**Web Application: Archive**.</span></span>
   <span data-ttu-id="7f582-150">d.</span><span class="sxs-lookup"><span data-stu-id="7f582-150">d.</span></span> <span data-ttu-id="7f582-151">Tıklatın **Tamam** tooclose hello Proje Yapısı iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="7f582-151">Click **OK** tooclose hello Project Structure dialog box.</span></span>

    ![Modül Ayarları'nı açın][05b]

<span data-ttu-id="7f582-153">Modül ayarlarınızı yapılandırdığınızda, aşağıdaki adımları hello kullanarak uygulama tooAzure yayımlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7f582-153">When you have configured your module settings, you can publish your application tooAzure by using hello following steps:</span></span>

1. <span data-ttu-id="7f582-154">Intellij'ın Proje Gezgini'nde hello sağ **Java-Web-App-üzerinde-Azure** projesi.</span><span class="sxs-lookup"><span data-stu-id="7f582-154">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="7f582-155">Merhaba bağlam menüsü görüntülendiğinde seçin **Azure**ve ardından **Azure Web uygulaması olarak Yayımla...**</span><span class="sxs-lookup"><span data-stu-id="7f582-155">When hello context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Azure yayımlama bağlam menüsü][06]
2. <span data-ttu-id="7f582-157">Zaten Intellij Azure'dan oturum açmış değil, Azure hesabınızda istendiğinde toosign olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7f582-157">If you have not already signed into Azure from IntelliJ, you will be prompted toosign into your Azure account.</span></span> <span data-ttu-id="7f582-158">(Birden çok Azure hesabınız yoksa, toobe göründükleri olsa bile bazı hello istemleri hello oturum açma işlemi sırasında birden fazla kez gösterilebilir aynı hello.</span><span class="sxs-lookup"><span data-stu-id="7f582-158">(If you have multiple Azure accounts, some of hello prompts during hello sign in process may be shown more than once, even if they appear toobe hello same.</span></span> <span data-ttu-id="7f582-159">Bu durumda, yönergeleri toofollow hello oturum devam.)</span><span class="sxs-lookup"><span data-stu-id="7f582-159">When this happens, continue toofollow hello sign in instructions.)</span></span>
   
    ![Azure oturum açma iletişim kutusu][07]
3. <span data-ttu-id="7f582-161">Azure hesabınızda oturumu başarıyla sonra hello **Aboneliklerini Yönet** iletişim kutusunda kimlik bilgilerinizle ilişkili Aboneliklerin listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7f582-161">After you have successfully signed into your Azure account, hello **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="7f582-162">(Listelenen birden çok abonelik ve yalnızca belirli bir alt kümesini ile toowork istiyorsanız, isteğe bağlı olarak toouse istemediğiniz hello abonelikleri temizleyin.) Aboneliklerinizi seçildiğinde tıklatın **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="7f582-162">(If there are multiple subscriptions listed and you want toowork with only a specific subset of them, you may optionally uncheck hello subscriptions you don't want toouse.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Aboneliklerini Yönetme][08]
4. <span data-ttu-id="7f582-164">Ne zaman hello **tooAzure Web uygulaması kapsayıcı dağıtma** iletişim kutusu görüntülenirse, daha önce oluşturduğunuz herhangi bir Web uygulaması kapsayıcıdaki görüntülenir; herhangi bir kapsayıcıdaki oluşturmadıysanız hello listesi boş olur.</span><span class="sxs-lookup"><span data-stu-id="7f582-164">When hello **Deploy tooAzure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, hello list will be empty.</span></span>
   
    ![Uygulama kapsayıcıları][09]
5. <span data-ttu-id="7f582-166">Bir Azure Web uygulaması kapsayıcısı önce ya da toopublish isterseniz, uygulama tooa yeni kapsayıcı oluşturmadıysanız, hello aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="7f582-166">If you have not created an Azure Web App Container before, or if you would like toopublish your application tooa new container, use hello following steps.</span></span> <span data-ttu-id="7f582-167">Aksi takdirde, var olan bir Web uygulaması kapsayıcıyı seçin ve toostep aşağıda 6 atlayın.</span><span class="sxs-lookup"><span data-stu-id="7f582-167">Otherwise, select an existing Web App Container and skip toostep 6 below.</span></span>
   
   1. <span data-ttu-id="7f582-168">' I tıklatın**+**</span><span class="sxs-lookup"><span data-stu-id="7f582-168">Click **+**</span></span>
      
       ![Uygulama kapsayıcısı Ekle][10]
   2. <span data-ttu-id="7f582-170">Merhaba **yeni Web uygulaması kapsayıcı** iletişim kutusu görüntülenir, olacağı Merhaba sonraki birkaç adım kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7f582-170">hello **New Web App Container** dialog box will be displayed, which will be used for hello next several steps.</span></span>
      
       ![Yeni uygulama kapsayıcısı][11a]
   3. <span data-ttu-id="7f582-172">Girin bir **DNS etiketi** Web uygulama kapsayıcısı için; bu hello yaprak DNS etiketi hello konak URL'nin, web uygulamanız için Azure içinde oluşturacak.</span><span class="sxs-lookup"><span data-stu-id="7f582-172">Enter a **DNS Label** for your Web App Container; this will form hello leaf DNS label of hello host URL for your web application in Azure.</span></span> <span data-ttu-id="7f582-173">Bu hello adı kullanılabilir ve tooAzure Web uygulaması adlandırma gereksinimlerini uygun unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7f582-173">Note that hello name must be available and conform tooAzure Web App naming requirements.</span></span>
   4. <span data-ttu-id="7f582-174">Hello içinde **Web kapsayıcısına** açılır menü, uygulamanız için uygun yazılım select hello.</span><span class="sxs-lookup"><span data-stu-id="7f582-174">In hello **Web Container** drop-down menu, select hello appropriate software for your application.</span></span>
      
       <span data-ttu-id="7f582-175">Şu anda, Tomcat 8, Tomcat 7 veya Jetty 9 seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f582-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="7f582-176">Seçili hello yazılım yeni bir dağıtımını Azure tarafından sağlanacak ve JDK Oracle tarafından oluşturulan ve Azure tarafından sağlanan 8'in yeni bir dağıtım çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="7f582-176">A recent distribution of hello selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="7f582-177">Merhaba, **abonelik** açılır menü, bu dağıtım için kullanmak istediğiniz toouse select hello abonelik.</span><span class="sxs-lookup"><span data-stu-id="7f582-177">In hello **Subscription** drop-down menu, select hello subscription you want toouse for this deployment.</span></span>
   6. <span data-ttu-id="7f582-178">Merhaba, **kaynak grubu** açılır menüsünde, istediğiniz tooassociate Web uygulamanızı seçin hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="7f582-178">In hello **Resource Group** drop-down menu, select hello Resource Group with which you want tooassociate your Web App.</span></span> <span data-ttu-id="7f582-179">(Örneğin, bunlar birlikte silinebilir böylece, toogroup kaynakları birlikte ilgili azure kaynak gruplarını izin.)</span><span class="sxs-lookup"><span data-stu-id="7f582-179">(Azure Resource Groups allow you toogroup related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="7f582-180">Atla toostep g veya kullanım hello aşağıdaki yeni bir kaynak grubu toocreate adımlar ve (varsa), var olan bir kaynak grubunu seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7f582-180">You can select an existing Resource Group (if you have any) and skip toostep g below, or use hello following steps toocreate a new Resource Group:</span></span>
      
      * <span data-ttu-id="7f582-181">Seçin  **&lt; &lt; yeni kaynak grubu oluştur &gt; &gt;**  hello içinde **kaynak grubu** açılır menü.</span><span class="sxs-lookup"><span data-stu-id="7f582-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in hello **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="7f582-182">Merhaba **yeni kaynak grubu** iletişim kutusu görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="7f582-182">hello **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Yeni kaynak grubu][12]
      * <span data-ttu-id="7f582-184">Merhaba hello içinde **adı** metin kutusuna, yeni kaynak grubunuz için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="7f582-184">In hello hello **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="7f582-185">Merhaba hello içinde **bölge** açılır menüsünde, select hello uygun Azure veri merkezi kaynak grubunuz için konum.</span><span class="sxs-lookup"><span data-stu-id="7f582-185">In hello hello **Region** drop-down menu, select hello appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="7f582-186">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7f582-186">Click **OK**.</span></span>
   7. <span data-ttu-id="7f582-187">Merhaba **App Service planı** açılır menü Merhaba, seçili kaynak grubu ile ilişkili hello uygulama hizmeti planları listeler.</span><span class="sxs-lookup"><span data-stu-id="7f582-187">hello **App Service Plan** drop-down menu lists hello app service plans that are associated with hello Resource Group that you selected.</span></span> <span data-ttu-id="7f582-188">(Web uygulamanızı, fiyatlandırma katmanı ve hello işlem örnek boyutu hello hello konumunu gibi bilgileri belirtir bir uygulama hizmeti planı.</span><span class="sxs-lookup"><span data-stu-id="7f582-188">(An App Service Plan specifies information such as hello location of your Web App, hello pricing tier and hello compute instance size.</span></span> <span data-ttu-id="7f582-189">Tek bir uygulama hizmeti planı ayrı olarak belirli bir Web uygulaması dağıtımından korunan neden olan ve birden çok Web uygulamaları için kullanılabilir.)</span><span class="sxs-lookup"><span data-stu-id="7f582-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="7f582-190">(Varsa) var olan bir uygulama hizmeti planı seçebilirsiniz ve toostep h aşağıdaki atlayacak veya adımları toocreate yeni bir uygulama hizmeti planı aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="7f582-190">You can select an existing App Service Plan (if you have any) and skip toostep h below, or use hello following steps toocreate a new App Service Plan:</span></span>
      
      * <span data-ttu-id="7f582-191">Seçin  **&lt; &lt; yeni uygulama hizmeti planı oluştur &gt; &gt;**  hello içinde **App Service planı** açılır menü.</span><span class="sxs-lookup"><span data-stu-id="7f582-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in hello **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="7f582-192">Merhaba **yeni uygulama hizmeti planı** iletişim kutusu görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="7f582-192">hello **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Yeni uygulama hizmeti planı][13]
      * <span data-ttu-id="7f582-194">Merhaba hello içinde **adı** metin kutusuna, yeni uygulama hizmeti planınız için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="7f582-194">In hello hello **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="7f582-195">Merhaba hello içinde **konumu** açılır menüsünde, select hello uygun Azure veri merkezi hello planı için konum.</span><span class="sxs-lookup"><span data-stu-id="7f582-195">In hello hello **Location** drop-down menu, select hello appropriate Azure data center location for hello plan.</span></span>
      * <span data-ttu-id="7f582-196">Merhaba hello içinde **fiyatlandırma katmanı** açılır menüsünde, select hello hello planlama fiyatlandırma uygun.</span><span class="sxs-lookup"><span data-stu-id="7f582-196">In hello hello **Pricing Tier** drop-down menu, select hello appropriate pricing for hello plan.</span></span> <span data-ttu-id="7f582-197">Test amacıyla seçebileceğiniz **serbest**.</span><span class="sxs-lookup"><span data-stu-id="7f582-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="7f582-198">Merhaba hello içinde **örnek boyutu** açılır menü, hello planı için seçme hello uygun örnek boyutu.</span><span class="sxs-lookup"><span data-stu-id="7f582-198">In hello hello **Instance Size** drop-down menu, select hello appropriate instance size for hello plan.</span></span> <span data-ttu-id="7f582-199">Test amacıyla seçebileceğiniz **küçük**.</span><span class="sxs-lookup"><span data-stu-id="7f582-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="7f582-200">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7f582-200">Click **OK**.</span></span>
   8. <span data-ttu-id="7f582-201">(İsteğe bağlı) Varsayılan olarak, Java 8 yeni bir dağıtımını otomatik, JVM Azure tooyour web uygulaması kapsayıcı tarafından dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="7f582-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure tooyour web app container.</span></span> <span data-ttu-id="7f582-202">Ancak, farklı sürüm ve hello JVM dağıtımını seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f582-202">However, you can select a different version and distribution of hello JVM.</span></span> <span data-ttu-id="7f582-203">toodo, bu nedenle, hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="7f582-203">toodo so, use hello following steps:</span></span>
      
      * <span data-ttu-id="7f582-204">Merhaba tıklatın **JDK** hello sekmesinde **yeni Web uygulaması kapsayıcı** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="7f582-204">Click hello **JDK** tab in hello **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="7f582-205">Seçenekler aşağıdaki hello birini seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7f582-205">You can choose from one of hello following options:</span></span>
        
        * <span data-ttu-id="7f582-206">Merhaba varsayılan Azure tarafından sunulan JDK dağıtma</span><span class="sxs-lookup"><span data-stu-id="7f582-206">Deploy hello default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="7f582-207">Bir 3. taraf JDK Azure üzerinde kullanılabilir olan ek JDKs aşağı açılan listesinden dağıtma</span><span class="sxs-lookup"><span data-stu-id="7f582-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="7f582-208">ZIP dosyası olarak ve ya da paketlenmesi gereken özel bir JDK dağıtımı Azure depolama hesabınızdaki veya genel olarak kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="7f582-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![Yeni uygulama kapsayıcı JDK sekmesi][11b]
   9. <span data-ttu-id="7f582-210">Tüm hello yukarıdaki adımları tamamladıktan sonra hello yeni Web uygulaması kapsayıcısı iletişim kutusunda aşağıdaki çizimde hello benzemelidir:</span><span class="sxs-lookup"><span data-stu-id="7f582-210">Once you have completed all of hello above steps, hello New Web App Container dialog box should resemble hello following illustration:</span></span>
      
       ![Yeni uygulama kapsayıcısı][14]
   10. <span data-ttu-id="7f582-212">Tıklatın **Tamam** yeni Web uygulaması kapsayıcısının toocomplete hello oluşturma.</span><span class="sxs-lookup"><span data-stu-id="7f582-212">Click **OK** toocomplete hello creation of your new Web App container.</span></span>
       
        <span data-ttu-id="7f582-213">Merhaba Web uygulaması kapsayıcıları toobe hello listesi için birkaç saniye bekleyin yenilenir ve hello listesinde yeni oluşturulan web uygulaması kapsayıcınız artık seçili olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7f582-213">Wait a few seconds for hello list of hello Web App containers toobe refreshed, and your newly-created web app container should now be selected in hello list.</span></span>
6. <span data-ttu-id="7f582-214">Hazır toocomplete hello ilk dağıtımı, Web uygulaması tooAzure sunulmuştur; tıklatın **Tamam** toodeploy, Java uygulama toohello seçili Web uygulaması kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="7f582-214">You are now ready toocomplete hello initial deployment of your Web App tooAzure; click **OK** toodeploy your Java application toohello selected Web App container.</span></span> <span data-ttu-id="7f582-215">Varsayılan olarak, uygulamanızı bir alt dizin hello uygulama sunucusu dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="7f582-215">By default, your application will be deployed as a subdirectory of hello application server.</span></span> <span data-ttu-id="7f582-216">Merhaba kök uygulaması dağıtılan toobe istiyorsanız hello denetleyin **tooroot dağıtmak** tıklatmadan önce onay kutusunu **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7f582-216">If you want it toobe deployed as hello root application, check hello **Deploy tooroot** checkbox before clicking **OK**.</span></span>
   
    ![TooAzure dağıtma][15]
7. <span data-ttu-id="7f582-218">Ardından, hello görmelisiniz **Azure etkinlik günlüğü** hello dağıtım durumu, Web uygulamanızın gösterecektir görünümü.</span><span class="sxs-lookup"><span data-stu-id="7f582-218">Next, you should see hello **Azure Activity Log** view, which will indicate hello deployment status of your Web App.</span></span>
   
    ![İlerleme göstergesi][16]
   
    <span data-ttu-id="7f582-220">Merhaba, Web uygulaması tooAzure dağıtma işlemi, yalnızca birkaç saniye almalıdır toocomplete.</span><span class="sxs-lookup"><span data-stu-id="7f582-220">hello process of deploying your Web App tooAzure should take only a few seconds toocomplete.</span></span> <span data-ttu-id="7f582-221">Uygulama hazır gördüğünüzde adlı bir bağlantı **yayımlanan** hello içinde **durum** sütun.</span><span class="sxs-lookup"><span data-stu-id="7f582-221">When your application ready, you will see a link named **Published** in hello **Status** column.</span></span> <span data-ttu-id="7f582-222">Hello bağlantısını tıklattığınızda sizi tooyour dağıtılmış Web uygulamanızın giriş sayfasına götürür veya bölüm toobrowse tooyour web uygulama aşağıdaki hello hello adımları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f582-222">When you click hello link, it will take you tooyour deployed Web App's home page, or you can use hello steps in hello following section toobrowse tooyour web app.</span></span>

## <a name="browsing-tooyour-web-app-on-azure"></a><span data-ttu-id="7f582-223">Gözatma tooyour Azure üzerinde Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="7f582-223">Browsing tooyour Web App on Azure</span></span>
<span data-ttu-id="7f582-224">toobrowse tooyour Azure Web uygulamasında, kullanabileceğiniz hello **Azure Gezgini** görünümü.</span><span class="sxs-lookup"><span data-stu-id="7f582-224">toobrowse tooyour Web App on Azure, you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="7f582-225">Merhaba, **Azure Gezgini** görünüm zaten açık, ardından tıklayarak açabilirsiniz **Görünüm** Intellij, menüde ardından **aracı Windows**ve ardından  **Hizmet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="7f582-225">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="7f582-226">Daha önce oturum açmamış olan, bu toodo şekilde ister.</span><span class="sxs-lookup"><span data-stu-id="7f582-226">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="7f582-227">Ne zaman hello **Azure Gezgini** görünümü görüntülenir, kullanma, bu adımları toobrowse tooyour Web uygulaması izleyin:</span><span class="sxs-lookup"><span data-stu-id="7f582-227">When hello **Azure Explorer** view is displayed, use follow these steps toobrowse tooyour Web App:</span></span> 

1. <span data-ttu-id="7f582-228">Merhaba genişletin **Azure** düğümü.</span><span class="sxs-lookup"><span data-stu-id="7f582-228">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="7f582-229">Merhaba genişletin **Web Apps** düğümü.</span><span class="sxs-lookup"><span data-stu-id="7f582-229">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="7f582-230">Web uygulaması sağ hello istenen.</span><span class="sxs-lookup"><span data-stu-id="7f582-230">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="7f582-231">Merhaba bağlam menüsü görüntülendiğinde **tarayıcıda aç**.</span><span class="sxs-lookup"><span data-stu-id="7f582-231">When hello context menu appears, click **Open in Browser**.</span></span>
   
    ![Web uygulaması Gözat][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="7f582-233">Web uygulamanızı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="7f582-233">Updating your web app</span></span>
<span data-ttu-id="7f582-234">Azure Web uygulaması çalıştıran var olan bir güncelleştirme hızlı ve kolay bir işlemdir ve güncelleştirmek için iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="7f582-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="7f582-235">Varolan bir Java Web uygulaması dağıtımını hello güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f582-235">You can update hello deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="7f582-236">Ek bir Java uygulaması toohello yayımlayabilirsiniz aynı Web uygulama kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7f582-236">You can publish an additional Java application toohello same Web App Container.</span></span>

<span data-ttu-id="7f582-237">Her iki durumda da hello işlemi aynıdır ve yalnızca birkaç saniye sürer:</span><span class="sxs-lookup"><span data-stu-id="7f582-237">In either case, hello process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="7f582-238">Merhaba Intellij proje Gezgini'nde tooupdate istediğiniz ya da Web uygulaması kapsayıcı varolan tooan eklemek Merhaba Java uygulaması sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7f582-238">In hello IntelliJ project explorer, right-click hello Java application you want tooupdate or add tooan existing Web App Container.</span></span>
2. <span data-ttu-id="7f582-239">Merhaba bağlam menüsü görüntülendiğinde seçin **Azure** ve ardından **Azure Web uygulaması olarak Yayımla...**</span><span class="sxs-lookup"><span data-stu-id="7f582-239">When hello context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="7f582-240">Zaten daha önce oturum açtıktan sonra var olan Web uygulaması kapsayıcıları listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7f582-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="7f582-241">Select toopublish istediğiniz ya da Java uygulama tooand tıklatmanız yeniden yayımlama hello **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7f582-241">Select hello one you want toopublish or re-publish your Java application tooand click **OK**.</span></span>

<span data-ttu-id="7f582-242">Daha sonra birkaç saniye hello **Azure etkinlik günlüğü** görünümü güncelleştirilmiş dağıtımınız olarak göster **yayımlanan** ve mümkün tooverify güncelleştirilmiş uygulamanız bir web tarayıcısında olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7f582-242">A few seconds later, hello **Azure Activity Log** view will show your updated deployment as **Published** and you will be able tooverify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="7f582-243">Başlatma, durdurma veya var olan bir web uygulamasının yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="7f582-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="7f582-244">toostart veya mevcut bir Azure Web uygulaması kapsayıcısı (tüm dağıtılan hello Java uygulamaları içine dahil), durdurmak, hello kullanabilirsiniz **Azure Gezgini** görünümü.</span><span class="sxs-lookup"><span data-stu-id="7f582-244">toostart or stop an existing Azure Web App container, (including all hello deployed Java applications in it), you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="7f582-245">Merhaba, **Azure Gezgini** görünüm zaten açık, ardından tıklayarak açabilirsiniz **Görünüm** Intellij, menüde ardından **aracı Windows**ve ardından  **Hizmet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="7f582-245">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="7f582-246">Daha önce oturum açmamış olan, bu toodo şekilde ister.</span><span class="sxs-lookup"><span data-stu-id="7f582-246">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="7f582-247">Ne zaman hello **Azure Gezgini** görünümü görüntülenir, kullanım bu adımları toostart izleyin veya Web uygulamanızı durdurun:</span><span class="sxs-lookup"><span data-stu-id="7f582-247">When hello **Azure Explorer** view is displayed, use follow these steps toostart or stop your Web App:</span></span> 

1. <span data-ttu-id="7f582-248">Merhaba genişletin **Azure** düğümü.</span><span class="sxs-lookup"><span data-stu-id="7f582-248">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="7f582-249">Merhaba genişletin **Web Apps** düğümü.</span><span class="sxs-lookup"><span data-stu-id="7f582-249">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="7f582-250">Web uygulaması sağ hello istenen.</span><span class="sxs-lookup"><span data-stu-id="7f582-250">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="7f582-251">Merhaba bağlam menüsü görüntülendiğinde **Başlat**, **durdurmak**, veya **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="7f582-251">When hello context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="7f582-252">Yalnızca çalışan bir web uygulamasına durdurmak veya şu anda çalışmıyor bir web uygulamasını başlatmak için hello menü seçeneklerine Bağlam duyarlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7f582-252">Note that hello menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Web uygulamasını Durdur][18]

## <a name="next-steps"></a><span data-ttu-id="7f582-254">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="7f582-254">Next Steps</span></span>
<span data-ttu-id="7f582-255">Java IDE hello Azure araç takımları hakkında daha fazla bilgi için bağlantılar aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="7f582-255">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="7f582-256">[Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="7f582-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="7f582-257">[Yükleme hello Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="7f582-257">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="7f582-258">[Eclipse Azure'da Hello World Web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="7f582-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="7f582-259">[Yeni hello Eclipse için Azure Araç Seti nedir]</span><span class="sxs-lookup"><span data-stu-id="7f582-259">[What's New in hello Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="7f582-260">[Intellij için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="7f582-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="7f582-261">[yükleme hello Intellij için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="7f582-261">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="7f582-262">*Intellij (Bu makalede) Azure'da Hello World Web uygulaması oluşturun*</span><span class="sxs-lookup"><span data-stu-id="7f582-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="7f582-263">[Yeni hello Intellij için Azure Araç Seti nedir]</span><span class="sxs-lookup"><span data-stu-id="7f582-263">[What's New in hello Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="7f582-264">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7f582-264">See Also</span></span>
<span data-ttu-id="7f582-265">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi].</span><span class="sxs-lookup"><span data-stu-id="7f582-265">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<span data-ttu-id="7f582-266">Azure Web uygulamaları oluşturma hakkında ek bilgi için bkz: Merhaba [Web Apps'e genel bakış].</span><span class="sxs-lookup"><span data-stu-id="7f582-266">For additional information about creating Azure Web Apps, see hello [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ../azure-toolkit-for-eclipse.md
[Intellij için Azure Araç Seti]: ../azure-toolkit-for-intellij.md
[Eclipse Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Yükleme hello Eclipse için Azure Araç Seti]: ../azure-toolkit-for-eclipse-installation.md
[yükleme hello Intellij için Azure Araç Seti]: ../azure-toolkit-for-intellij-installation.md
[Yeni hello Eclipse için Azure Araç Seti nedir]: ../azure-toolkit-for-eclipse-whats-new.md
[Yeni hello Intellij için Azure Araç Seti nedir]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Web Apps'e genel bakış]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png
