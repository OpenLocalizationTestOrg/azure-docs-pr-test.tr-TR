---
title: "temel Azure web uygulamasını kullanarak aaaCreate Tutulma | Microsoft Docs"
description: "Bu öğretici nasıl toouse hello Azure araç setini Eclipse toocreate için bir Hello World Web uygulaması için Azure gösterir."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: b2f42e0e7a5b98760ec02fab2fc38f9f07b1156b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a><span data-ttu-id="79f5f-103">Eclipse kullanarak bir temel Azure web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="79f5f-103">Create a basic Azure web app using Eclipse</span></span>
<span data-ttu-id="79f5f-104">Bu öğreticide gösterilmiştir nasıl toocreate ve hello kullanarak bir Web uygulaması gibi temel bir Hello World uygulama tooAzure dağıtma [Eclipse için Azure Araç Seti].</span><span class="sxs-lookup"><span data-stu-id="79f5f-104">This tutorial shows how toocreate and deploy a basic Hello World application tooAzure as a Web App by using hello [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="79f5f-105">Kolaylık olması için temel bir JSP örneği gösterilir, ancak Azure dağıtım ilgili olduğu kadar benzer adımlar bir Java servlet için uygun olacaktır.</span><span class="sxs-lookup"><span data-stu-id="79f5f-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="79f5f-106">Bu öğreticiyi tamamladıktan sonra uygulamanızı bir web tarayıcısında görüntülediğinizde çizim aşağıdaki benzer toohello görünür:</span><span class="sxs-lookup"><span data-stu-id="79f5f-106">When you have completed this tutorial, your application will look similar toohello following illustration when you view it in a web browser:</span></span>

![Önizleme Hello, World uygulama][01]

## <a name="prerequisites"></a><span data-ttu-id="79f5f-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="79f5f-108">Prerequisites</span></span>
* <span data-ttu-id="79f5f-109">Bir Java Geliştirme Seti (JDK), v 1.8 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="79f5f-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="79f5f-110">Luna olan Java EE geliştiricileri için Eclipse IDE veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="79f5f-110">Eclipse IDE for Java EE Developers, Luna or later.</span></span> <span data-ttu-id="79f5f-111">Bu adresten yüklenebilir <http://www.eclipse.org/downloads/>.</span><span class="sxs-lookup"><span data-stu-id="79f5f-111">This can be downloaded from <http://www.eclipse.org/downloads/>.</span></span>
* <span data-ttu-id="79f5f-112">Dağıtım bir Java tabanlı web sunucusu veya uygulama sunucusu gibi [Apache Tomcat] veya [Jetty].</span><span class="sxs-lookup"><span data-stu-id="79f5f-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="79f5f-113">Öğesinden alınan bir Azure aboneliği <https://azure.microsoft.com/free/> veya <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="79f5f-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="79f5f-114">Merhaba [Eclipse için Azure Araç Seti].</span><span class="sxs-lookup"><span data-stu-id="79f5f-114">hello [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="79f5f-115">Hello Azure araç setini yükleme hakkında daha fazla bilgi için bkz: [yükleme hello Eclipse için Azure Araç Seti].</span><span class="sxs-lookup"><span data-stu-id="79f5f-115">For information about installing hello Azure Toolkit, see [Installing hello Azure Toolkit for Eclipse].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="79f5f-116">toocreate Merhaba Dünya uygulaması</span><span class="sxs-lookup"><span data-stu-id="79f5f-116">toocreate a Hello World application</span></span>
<span data-ttu-id="79f5f-117">İlk olarak, bir Java projesi oluşturma ile başlayacağız devre dışı.</span><span class="sxs-lookup"><span data-stu-id="79f5f-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="79f5f-118">Eclipse başlatın ve başlangıç menüsünde tıklatın **dosya**, tıklatın **yeni**ve ardından **dinamik Web projesi**.</span><span class="sxs-lookup"><span data-stu-id="79f5f-118">Start Eclipse, and at hello menu click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="79f5f-119">(Görmüyorsanız **dinamik Web projesi** tıkladıktan sonra kullanılabilir bir proje listelenen **dosya** ve **yeni**, ardından aşağıdaki hello: tıklatın **dosya**, tıklatın **yeni**, tıklatın **proje...** , genişletin **Web**, tıklatın **dinamik Web projesi**, tıklatıp **sonraki**.)</span><span class="sxs-lookup"><span data-stu-id="79f5f-119">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do hello following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>
2. <span data-ttu-id="79f5f-120">Bu öğreticinin amaçları doğrultusunda hello proje adı **mywebapp şeklindedir**.</span><span class="sxs-lookup"><span data-stu-id="79f5f-120">For purposes of this tutorial, name hello project **MyWebApp**.</span></span> <span data-ttu-id="79f5f-121">Ekranınızın benzer toohello aşağıdaki görünür:</span><span class="sxs-lookup"><span data-stu-id="79f5f-121">Your screen will appear similar toohello following:</span></span>
   
    ![Yeni bir dinamik Web projesi oluşturma][02]
3. <span data-ttu-id="79f5f-123">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79f5f-123">Click **Finish**.</span></span>
4. <span data-ttu-id="79f5f-124">Eclipse'nın Proje Gezgini görünümü içinde genişletmek **mywebapp şeklindedir**.</span><span class="sxs-lookup"><span data-stu-id="79f5f-124">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="79f5f-125">**WebContent**'e sağ tıklayın, **Yeni**'ye tıklayın ve ardından **JSP Dosyası**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79f5f-125">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
5. <span data-ttu-id="79f5f-126">Merhaba, **yeni JSP dosyası** iletişim kutusu, ad hello dosyası **index.jsp**, hello üst klasörünü olarak **mywebapp şeklindedir/WebContent**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="79f5f-126">In hello **New JSP File** dialog box, name hello file **index.jsp**, keep hello parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>
6. <span data-ttu-id="79f5f-127">Merhaba, **JSP şablon seç** amacıyla Bu öğretici Seç iletişim kutusu **yeni JSP dosyası (html)**ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="79f5f-127">In hello **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
7. <span data-ttu-id="79f5f-128">İndex.jsp dosyası Eclipse'te açıldığında, metin toodynamically görünümünde eklemek **Merhaba Dünya!**</span><span class="sxs-lookup"><span data-stu-id="79f5f-128">When your index.jsp file opens in Eclipse, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="79f5f-129">Merhaba varolan içinde `<body>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="79f5f-129">within hello existing `<body>` element.</span></span> <span data-ttu-id="79f5f-130">Güncelleştirilmiş `<body>` içeriği aşağıdaki örneğine hello benzer:</span><span class="sxs-lookup"><span data-stu-id="79f5f-130">Your updated `<body>` content should resemble hello following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. <span data-ttu-id="79f5f-131">İndex.jsp kaydedin.</span><span class="sxs-lookup"><span data-stu-id="79f5f-131">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a><span data-ttu-id="79f5f-132">toodeploy, uygulama tooan Azure Web uygulaması kapsayıcısı</span><span class="sxs-lookup"><span data-stu-id="79f5f-132">toodeploy your application tooan Azure Web App Container</span></span>
<span data-ttu-id="79f5f-133">Java web uygulaması tooAzure dağıtabilir miyim birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="79f5f-133">There are several ways by which you can deploy a Java web application tooAzure.</span></span> <span data-ttu-id="79f5f-134">Bu öğretici hello basit açıklar: uygulamanızı dağıtılan tooan Azure Web uygulaması kapsayıcı olacaktır - hiçbir özel Proje türü ya da ek araçlar gereklidir.</span><span class="sxs-lookup"><span data-stu-id="79f5f-134">This tutorial describes one of hello simplest: your application will be deployed tooan Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="79f5f-135">Merhaba JDK ve hello web kapsayıcısı yazılım; böylece hiçbir gerek tooupload kendi sizin için Azure tarafından sağlanacak; ihtiyacınız olan tek şey, Java Web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="79f5f-135">hello JDK and hello web container software will be provided for you by Azure, so there is no need tooupload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="79f5f-136">Sonuç olarak, uygulamanız için yayımlama işlemi hello saniye, dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="79f5f-136">As a result, hello publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="79f5f-137">Eclipse'nın Proje Gezgini'nde sağ **mywebapp şeklindedir**.</span><span class="sxs-lookup"><span data-stu-id="79f5f-137">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>
2. <span data-ttu-id="79f5f-138">Merhaba bağlam menüsünden seçin **Azure**, ardından **Azure Web uygulaması olarak Yayımla...**</span><span class="sxs-lookup"><span data-stu-id="79f5f-138">In hello context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
    ![Olarak Azure Web uygulaması yayımlama][03]
   
    <span data-ttu-id="79f5f-140">Alternatif olarak, web uygulaması projenize hello Proje Gezgini seçiliyken hello tıklatabilirsiniz **Yayımla** açılır liste düğmesi hello araç ve seçim **Azure Web uygulaması olarak Yayımla** buradan:</span><span class="sxs-lookup"><span data-stu-id="79f5f-140">Alternatively, while your web application project is selected in hello Project Explorer, you can click hello **Publish** dropdown button on hello toolbar and select **Publish as Azure Web App** from there:</span></span>
   
    ![Olarak Azure Web uygulaması yayımlama][14]
3. <span data-ttu-id="79f5f-142">Zaten Eclipse Azure'dan oturum açmış değil, Azure hesabınızda istendiğinde toosign olacaktır:</span><span class="sxs-lookup"><span data-stu-id="79f5f-142">If you have not already signed into Azure from Eclipse, you will be prompted toosign into your Azure account:</span></span>
   
    ![Azure oturum açma iletişim kutusu][04]
   
    <span data-ttu-id="79f5f-144">Bazı hello istemleri hello sırasında oturum açmak, birden çok Azure hesabı varsa bunlar toobe görünse bile işlem birden fazla kez gösterilebilir aynı hello.</span><span class="sxs-lookup"><span data-stu-id="79f5f-144">If you have multiple Azure accounts, some of hello prompts during hello sign in process may be shown more than once, even if they appear toobe hello same.</span></span> <span data-ttu-id="79f5f-145">Bu gerçekleştiğinde, hello oturum açma yönergeleri izleyerek devam edin.</span><span class="sxs-lookup"><span data-stu-id="79f5f-145">When this happens, continue following hello sign in instructions.</span></span>
4. <span data-ttu-id="79f5f-146">Azure hesabınızda oturumu başarıyla sonra hello **Aboneliklerini Yönet** iletişim kutusunda kimlik bilgilerinizle ilişkili Aboneliklerin listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="79f5f-146">After you have successfully signed into your Azure account, hello **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="79f5f-147">Listelenen birden çok abonelik ve yalnızca belirli bir alt kümesini ile toowork istiyorsanız hello toouse istediğiniz olanları isteğe bağlı olarak işaretini.</span><span class="sxs-lookup"><span data-stu-id="79f5f-147">If there are multiple subscriptions listed and you want toowork with only a specific subset of them, you may optionally uncheck hello ones you do want toouse.</span></span> <span data-ttu-id="79f5f-148">Aboneliklerinizi seçildiğinde tıklatın **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="79f5f-148">When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Yönet abonelikleri iletişim kutusu][05]
5. <span data-ttu-id="79f5f-150">Ne zaman hello **tooAzure Web uygulaması kapsayıcı dağıtma** iletişim kutusu görüntülenirse, daha önce oluşturduğunuz herhangi bir Web uygulaması kapsayıcıdaki görüntülenir; herhangi bir kapsayıcıdaki oluşturmadıysanız hello listesi boş olur.</span><span class="sxs-lookup"><span data-stu-id="79f5f-150">When hello **Deploy tooAzure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, hello list will be empty.</span></span>
   
    ![Dağıt tooAzure Web uygulama kapsayıcısı iletişim kutusu][06]
6. <span data-ttu-id="79f5f-152">Bir Azure Web uygulaması kapsayıcısı önce ya da toopublish isterseniz, uygulama tooa yeni kapsayıcı oluşturmadıysanız, hello aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="79f5f-152">If you have not created an Azure Web App Container before, or if you would like toopublish your application tooa new container, use hello following steps.</span></span> <span data-ttu-id="79f5f-153">Aksi takdirde, var olan bir Web uygulaması kapsayıcıyı seçin ve toostep 7 aşağıdaki atlayın.</span><span class="sxs-lookup"><span data-stu-id="79f5f-153">Otherwise, select an existing Web App Container and skip toostep 7 below.</span></span>
   
   1. <span data-ttu-id="79f5f-154">Tıklatın **yeni...**</span><span class="sxs-lookup"><span data-stu-id="79f5f-154">Click **New...**</span></span>
      
       ![Dağıt tooAzure Web uygulama kapsayıcısı iletişim kutusu][15]
   2. <span data-ttu-id="79f5f-156">Merhaba **yeni Web uygulaması kapsayıcı** iletişim kutusu görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="79f5f-156">hello **New Web App Container** dialog box will be displayed:</span></span>
      
       ![Yeni Web uygulaması kapsayıcı iletişim kutusu][07a]
   3. <span data-ttu-id="79f5f-158">Girin bir **DNS etiketi** Web uygulama kapsayıcısı için; bu hello yaprak DNS etiketi hello konak URL'nin, web uygulamanız için Azure içinde oluşturacak.</span><span class="sxs-lookup"><span data-stu-id="79f5f-158">Enter a **DNS Label** for your Web App Container; this will form hello leaf DNS label of hello host URL for your web application in Azure.</span></span> <span data-ttu-id="79f5f-159">(Bu hello adı kullanılabilir ve tooAzure Web uygulaması adlandırma gereksinimlerini uygun unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="79f5f-159">(Note that hello name must be available and conform tooAzure Web App naming requirements.)</span></span>
   4. <span data-ttu-id="79f5f-160">Hello içinde **Web kapsayıcısına** açılır menü, uygulamanız için uygun yazılım select hello.</span><span class="sxs-lookup"><span data-stu-id="79f5f-160">In hello **Web Container** drop-down menu, select hello appropriate software for your application.</span></span>
      
       <span data-ttu-id="79f5f-161">Şu anda, Tomcat 8, Tomcat 7 veya Jetty 9 seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79f5f-161">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="79f5f-162">Seçili hello yazılım yeni bir dağıtımını Azure tarafından sağlanacak ve JDK Oracle tarafından oluşturulan ve Azure tarafından sağlanan 8'in yeni bir dağıtım çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="79f5f-162">A recent distribution of hello selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="79f5f-163">Merhaba, **abonelik** açılır menü, bu dağıtım için kullanmak istediğiniz toouse select hello abonelik.</span><span class="sxs-lookup"><span data-stu-id="79f5f-163">In hello **Subscription** drop-down menu, select hello subscription you want toouse for this deployment.</span></span>
   6. <span data-ttu-id="79f5f-164">Merhaba, **kaynak grubu** açılır menüsünde, istediğiniz tooassociate Web uygulamanızı seçin hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="79f5f-164">In hello **Resource Group** drop-down menu, select hello Resource Group with which you want tooassociate your Web App.</span></span> <span data-ttu-id="79f5f-165">(Örneğin, bunlar birlikte silinebilir böylece, toogroup kaynakları birlikte ilgili azure kaynak gruplarını izin.)</span><span class="sxs-lookup"><span data-stu-id="79f5f-165">(Azure Resource Groups allow you toogroup related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="79f5f-166">Atla toostep g veya bunlar aşağıdaki kullanım hello toocreate yeni bir kaynak grubu adımlar ve (varsa), var olan bir kaynak grubunu seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="79f5f-166">You can select an existing Resource Group (if you have any) and skip toostep g below, or use hello following these steps toocreate a new Resource Group:</span></span>
      
      * <span data-ttu-id="79f5f-167">Tıklatın **yeni...**</span><span class="sxs-lookup"><span data-stu-id="79f5f-167">Click **New...**</span></span>
      * <span data-ttu-id="79f5f-168">Merhaba **yeni kaynak grubu** iletişim kutusu görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="79f5f-168">hello **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Yeni kaynak grubu iletişim kutusu][08]
      * <span data-ttu-id="79f5f-170">Merhaba hello içinde **adı** metin kutusuna, yeni kaynak grubunuz için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="79f5f-170">In hello hello **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="79f5f-171">Merhaba hello içinde **bölge** açılır menüsünde, select hello uygun Azure veri merkezi kaynak grubunuz için konum.</span><span class="sxs-lookup"><span data-stu-id="79f5f-171">In hello hello **Region** drop-down menu, select hello appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="79f5f-172">İsteğe bağlı: varsayılan olarak, yeni bir Java 8 dağıtımını Azure tarafından otomatik olarak dağıtılacak tooyour web uygulaması kapsayıcı, JVM olarak.</span><span class="sxs-lookup"><span data-stu-id="79f5f-172">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically tooyour web app container as your JVM.</span></span> <span data-ttu-id="79f5f-173">Ancak, Web uygulamanızı gerektiriyorsa, farklı sürüm ve hello JVM dağıtımını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79f5f-173">However, you can specify a different version and distribution of hello JVM if your Web App requires it.</span></span> <span data-ttu-id="79f5f-174">toospecify hello JDK Web uygulamanız için tıklatın hello **JDK** sekmesini tıklatın ve aşağıdaki seçenekleri şu hello birini seçin:</span><span class="sxs-lookup"><span data-stu-id="79f5f-174">toospecify hello JDK for your Web App, click hello **JDK** tab, and select one of hello following options:</span></span>
        
        * <span data-ttu-id="79f5f-175">**Merhaba varsayılan Azure Web uygulamaları hizmeti tarafından sunulan JDK dağıtımı**: Bu seçenek Java 8 yeni bir dağıtımını dağıtır.</span><span class="sxs-lookup"><span data-stu-id="79f5f-175">**Deploy hello default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
        * <span data-ttu-id="79f5f-176">**Bir 3. taraf JDK Azure üzerinde kullanılabilir dağıtmak**: Bu seçenek, Microsoft Azure tarafından sağlanan JDKs hello listesinden toochoose sağlar.</span><span class="sxs-lookup"><span data-stu-id="79f5f-176">**Deploy a 3rd party JDK available on Azure**: This option allows you toochoose from hello list of JDKs which are provided by Microsoft Azure.</span></span>
        * <span data-ttu-id="79f5f-177">**Bu yükleme konumdan kendi JDK dağıtımı**: Bu seçenek, toospecify tanır bir ZIP dosyası olarak paketlenmesi gerekir ve bir genel kullanıma açık indirme konumu veya bir Azure depolama hesabı için tooeither karşıya kendi JDK dağıtımı, erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="79f5f-177">**Deploy my own JDK from this download location**: This option allows you toospecify your own JDK distribution, which must be packaged as a ZIP file and uploaded tooeither a publicly available download location or an Azure storage account for which you have access.</span></span>
          
          ![Yeni Web uygulaması kapsayıcı iletişim kutusu][07b]
   7. <span data-ttu-id="79f5f-179">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79f5f-179">Click **OK**.</span></span>
   8. <span data-ttu-id="79f5f-180">Merhaba **App Service planı** açılır menü Merhaba, seçili kaynak grubu ile ilişkili hello uygulama hizmeti planları listeler.</span><span class="sxs-lookup"><span data-stu-id="79f5f-180">hello **App Service Plan** drop-down menu lists hello app service plans that are associated with hello Resource Group that you selected.</span></span> <span data-ttu-id="79f5f-181">(Uygulama hizmeti planları, Web uygulamanızın, fiyatlandırma katmanı ve hello işlem örnek boyutu hello hello konum gibi bilgileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="79f5f-181">(App Service Plans specify information such as hello location of your Web App, hello pricing tier and hello compute instance size.</span></span> <span data-ttu-id="79f5f-182">Tek bir uygulama hizmeti planı ayrı olarak belirli bir Web uygulaması dağıtımından korunan neden olan ve birden çok Web uygulamaları için kullanılabilir.)</span><span class="sxs-lookup"><span data-stu-id="79f5f-182">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="79f5f-183">(Varsa) var olan bir uygulama hizmeti planı seçebilirsiniz ve toostep h aşağıdaki atlayacak veya bu adımları toocreate yeni bir uygulama hizmeti planı aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="79f5f-183">You can select an existing App Service Plan (if you have any) and skip toostep h below, or use hello following these steps toocreate a new App Service Plan:</span></span>
      
      * <span data-ttu-id="79f5f-184">Tıklatın **yeni...**</span><span class="sxs-lookup"><span data-stu-id="79f5f-184">Click **New...**</span></span>
      * <span data-ttu-id="79f5f-185">Merhaba **yeni uygulama hizmeti planı** iletişim kutusu görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="79f5f-185">hello **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Yeni uygulama hizmeti planı iletişim kutusu][09]
      * <span data-ttu-id="79f5f-187">Merhaba hello içinde **adı** metin kutusuna, yeni uygulama hizmeti planınız için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="79f5f-187">In hello hello **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="79f5f-188">Merhaba hello içinde **konumu** açılır menüsünde, select hello uygun Azure veri merkezi hello planı için konum.</span><span class="sxs-lookup"><span data-stu-id="79f5f-188">In hello hello **Location** drop-down menu, select hello appropriate Azure data center location for hello plan.</span></span>
      * <span data-ttu-id="79f5f-189">Merhaba hello içinde **fiyatlandırma katmanı** açılır menüsünde, select hello hello planlama fiyatlandırma uygun.</span><span class="sxs-lookup"><span data-stu-id="79f5f-189">In hello hello **Pricing Tier** drop-down menu, select hello appropriate pricing for hello plan.</span></span> <span data-ttu-id="79f5f-190">Test amacıyla seçebileceğiniz **serbest**.</span><span class="sxs-lookup"><span data-stu-id="79f5f-190">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="79f5f-191">Merhaba hello içinde **örnek boyutu** açılır menü, hello planı için seçme hello uygun örnek boyutu.</span><span class="sxs-lookup"><span data-stu-id="79f5f-191">In hello hello **Instance Size** drop-down menu, select hello appropriate instance size for hello plan.</span></span> <span data-ttu-id="79f5f-192">Test amacıyla seçebileceğiniz **küçük**.</span><span class="sxs-lookup"><span data-stu-id="79f5f-192">For testing purposes you can choose **Small**.</span></span>
   9. <span data-ttu-id="79f5f-193">Tüm hello yukarıdaki adımları tamamladıktan sonra hello yeni Web uygulaması kapsayıcısı iletişim kutusunda aşağıdaki çizimde hello benzemelidir:</span><span class="sxs-lookup"><span data-stu-id="79f5f-193">Once you have completed all of hello above steps, hello New Web App Container dialog box should resemble hello following illustration:</span></span>
      
       ![Yeni Web uygulaması kapsayıcı iletişim kutusu][10]
   10. <span data-ttu-id="79f5f-195">Tıklatın **Tamam** yeni Web uygulaması kapsayıcısının toocomplete hello oluşturma.</span><span class="sxs-lookup"><span data-stu-id="79f5f-195">Click **OK** toocomplete hello creation of your new Web App container.</span></span>
       
        <span data-ttu-id="79f5f-196">Merhaba Web uygulaması kapsayıcıları toobe hello listesi için birkaç saniye bekleyin yenilenir ve hello listesinde yeni oluşturulan web uygulaması kapsayıcınız artık seçili olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="79f5f-196">Wait a few seconds for hello list of hello Web App containers toobe refreshed, and your newly-created web app container should now be selected in hello list.</span></span>
7. <span data-ttu-id="79f5f-197">Hazır toocomplete hello ilk dağıtımı, Web uygulaması tooAzure sunulmuştur:</span><span class="sxs-lookup"><span data-stu-id="79f5f-197">You are now ready toocomplete hello initial deployment of your Web App tooAzure:</span></span>
   
    ![Dağıt tooAzure Web uygulama kapsayıcısı iletişim kutusu][11]
   
    <span data-ttu-id="79f5f-199">Tıklatın **Tamam** toodeploy, Java uygulama toohello seçili Web uygulaması kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="79f5f-199">Click **OK** toodeploy your Java application toohello selected Web App container.</span></span>
   
    <span data-ttu-id="79f5f-200">Varsayılan olarak, uygulamanızı bir alt dizin hello uygulama sunucusu dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="79f5f-200">By default, your application will be deployed as a subdirectory of hello application server.</span></span> <span data-ttu-id="79f5f-201">Merhaba kök uygulaması dağıtılan toobe istiyorsanız hello denetleyin **tooroot dağıtmak** tıklatmadan önce onay kutusunu **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="79f5f-201">If you want it toobe deployed as hello root application, check hello **Deploy tooroot** checkbox before clicking **OK**.</span></span>
8. <span data-ttu-id="79f5f-202">Ardından, hello görmelisiniz **Azure etkinlik günlüğü** hello dağıtım durumu, Web uygulamanızın gösterecektir görünümü.</span><span class="sxs-lookup"><span data-stu-id="79f5f-202">Next, you should see hello **Azure Activity Log** view, which will indicate hello deployment status of your Web App.</span></span>
   
    ![Azure etkinlik günlüğü][12]
   
    <span data-ttu-id="79f5f-204">Merhaba, Web uygulaması tooAzure dağıtma işlemi, yalnızca birkaç saniye almalıdır toocomplete.</span><span class="sxs-lookup"><span data-stu-id="79f5f-204">hello process of deploying your Web App tooAzure should take only a few seconds toocomplete.</span></span> <span data-ttu-id="79f5f-205">Uygulama hazır gördüğünüzde adlı bir bağlantı **yayımlanan** hello içinde **durum** sütun.</span><span class="sxs-lookup"><span data-stu-id="79f5f-205">When your application ready, you will see a link named **Published** in hello **Status** column.</span></span> <span data-ttu-id="79f5f-206">Merhaba bağlantısını tıklattığınızda sizi tooyour dağıtılmış Web uygulamanızın giriş sayfasına götürür.</span><span class="sxs-lookup"><span data-stu-id="79f5f-206">When you click hello link, it will take you tooyour deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="79f5f-207">Web uygulamanızı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="79f5f-207">Updating your web app</span></span>
<span data-ttu-id="79f5f-208">Azure Web uygulaması çalıştıran var olan bir güncelleştirme hızlı ve kolay bir işlemdir ve güncelleştirmek için iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="79f5f-208">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="79f5f-209">Varolan bir Java Web uygulaması dağıtımını hello güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79f5f-209">You can update hello deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="79f5f-210">Ek bir Java uygulaması toohello yayımlayabilirsiniz aynı Web uygulama kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="79f5f-210">You can publish an additional Java application toohello same Web App Container.</span></span>

<span data-ttu-id="79f5f-211">Her iki durumda da hello işlemi aynıdır ve yalnızca birkaç saniye sürer:</span><span class="sxs-lookup"><span data-stu-id="79f5f-211">In either case, hello process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="79f5f-212">Merhaba Eclipse proje Gezgini'nde tooupdate istediğiniz ya da Web uygulaması kapsayıcı varolan tooan eklemek Merhaba Java uygulaması sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79f5f-212">In hello Eclipse project explorer, right-click hello Java application you want tooupdate or add tooan existing Web App Container.</span></span>
2. <span data-ttu-id="79f5f-213">Merhaba bağlam menüsü görüntülendiğinde seçin **Azure** ve ardından **Azure Web uygulaması olarak Yayımla...**</span><span class="sxs-lookup"><span data-stu-id="79f5f-213">When hello context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="79f5f-214">Zaten daha önce oturum açtıktan sonra var olan Web uygulaması kapsayıcıları listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="79f5f-214">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="79f5f-215">Select toopublish istediğiniz ya da Java uygulama tooand tıklatmanız yeniden yayımlama hello **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="79f5f-215">Select hello one you want toopublish or re-publish your Java application tooand click **OK**.</span></span>

<span data-ttu-id="79f5f-216">Daha sonra birkaç saniye hello **Azure etkinlik günlüğü** görünümü güncelleştirilmiş dağıtımınız olarak göster **yayımlanan** ve mümkün tooverify güncelleştirilmiş uygulamanız bir web tarayıcısında olacaktır.</span><span class="sxs-lookup"><span data-stu-id="79f5f-216">A few seconds later, hello **Azure Activity Log** view will show your updated deployment as **Published** and you will be able tooverify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="79f5f-217">Başlatma, durdurma veya var olan bir web uygulamasının yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="79f5f-217">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="79f5f-218">toostart veya mevcut bir Azure Web uygulaması kapsayıcısı (tüm dağıtılan hello Java uygulamaları içine dahil), durdurmak, hello kullanabilirsiniz **Azure Gezgini** görünümü.</span><span class="sxs-lookup"><span data-stu-id="79f5f-218">toostart or stop an existing Azure Web App container, (including all hello deployed Java applications in it), you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="79f5f-219">Merhaba, **Azure Gezgini** görünüm zaten açık, ardından tıklayarak açabilirsiniz **penceresi** eclipse'te, ardından menüsünü **görünümü göster**, ardından **diğer...** , ardından **Azure**ve ardından **Azure Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="79f5f-219">If hello **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="79f5f-220">Daha önce oturum açmamış olan, bu toodo şekilde ister.</span><span class="sxs-lookup"><span data-stu-id="79f5f-220">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="79f5f-221">Ne zaman hello **Azure Gezgini** görünümü görüntülenir, kullanım bu adımları toostart izleyin veya Web uygulamanızı durdurun:</span><span class="sxs-lookup"><span data-stu-id="79f5f-221">When hello **Azure Explorer** view is displayed, use follow these steps toostart or stop your Web App:</span></span> 

1. <span data-ttu-id="79f5f-222">Merhaba genişletin **Azure** düğümü.</span><span class="sxs-lookup"><span data-stu-id="79f5f-222">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="79f5f-223">Merhaba genişletin **Web Apps** düğümü.</span><span class="sxs-lookup"><span data-stu-id="79f5f-223">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="79f5f-224">Web uygulaması sağ hello istenen.</span><span class="sxs-lookup"><span data-stu-id="79f5f-224">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="79f5f-225">Merhaba bağlam menüsü görüntülendiğinde **Başlat**, **durdurmak**, veya **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="79f5f-225">When hello context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="79f5f-226">Yalnızca çalışan bir web uygulamasına durdurmak veya şu anda çalışmıyor bir web uygulamasını başlatmak için hello menü seçeneklerine Bağlam duyarlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="79f5f-226">Note that hello menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Var olan bir Web uygulamasının durdurma][13]

## <a name="next-steps"></a><span data-ttu-id="79f5f-228">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="79f5f-228">Next Steps</span></span>
<span data-ttu-id="79f5f-229">Java IDE hello Azure araç takımları hakkında daha fazla bilgi için bağlantılar aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="79f5f-229">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="79f5f-230">[Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="79f5f-230">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="79f5f-231">[yükleme hello Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="79f5f-231">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="79f5f-232">*Eclipse (Bu makalede) Azure'da Hello World Web uygulaması oluşturun*</span><span class="sxs-lookup"><span data-stu-id="79f5f-232">*Create a Hello World Web App for Azure in Eclipse (This Article)*</span></span>
  * <span data-ttu-id="79f5f-233">[Yeni hello Eclipse için Azure Araç Seti nedir]</span><span class="sxs-lookup"><span data-stu-id="79f5f-233">[What's New in hello Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="79f5f-234">[IntelliJ için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="79f5f-234">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="79f5f-235">[Yükleme hello Intellij için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="79f5f-235">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="79f5f-236">[Intellij Azure'da Hello World Web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="79f5f-236">[Create a Hello World Web App for Azure in IntelliJ]</span></span>
  * <span data-ttu-id="79f5f-237">[Yeni hello Intellij için Azure Araç Seti nedir]</span><span class="sxs-lookup"><span data-stu-id="79f5f-237">[What's New in hello Azure Toolkit for IntelliJ]</span></span>

<span data-ttu-id="79f5f-238">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi].</span><span class="sxs-lookup"><span data-stu-id="79f5f-238">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<span data-ttu-id="79f5f-239">Azure Web uygulamaları oluşturma hakkında ek bilgi için bkz: Merhaba [Web Apps'e genel bakış].</span><span class="sxs-lookup"><span data-stu-id="79f5f-239">For additional information about creating Azure Web Apps, see hello [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ../azure-toolkit-for-eclipse.md
[IntelliJ için Azure Araç Seti]: ../azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Intellij Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web-intellij-create-hello-world-web-app.md
[yükleme hello Eclipse için Azure Araç Seti]: ../azure-toolkit-for-eclipse-installation.md
[Yükleme hello Intellij için Azure Araç Seti]: ../azure-toolkit-for-intellij-installation.md
[Yeni hello Eclipse için Azure Araç Seti nedir]: ../azure-toolkit-for-eclipse-whats-new.md
[Yeni hello Intellij için Azure Araç Seti nedir]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Web Apps'e genel bakış]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/app-service-web-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/app-service-web-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/app-service-web-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/app-service-web-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/app-service-web-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/app-service-web-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/app-service-web-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/app-service-web-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/app-service-web-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/app-service-web-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/app-service-web-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/app-service-web-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/app-service-web-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/app-service-web-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
