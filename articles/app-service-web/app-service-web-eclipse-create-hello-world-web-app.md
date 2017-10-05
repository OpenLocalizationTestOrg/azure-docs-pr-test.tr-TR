---
title: "Eclipse kullanarak bir temel Azure web uygulaması oluşturma | Microsoft Docs"
description: "Bu öğretici bir Hello World Web uygulaması için Azure oluşturmak için Eclipse için Azure Araç Seti kullanmayı gösterir."
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
ms.openlocfilehash: 683d6828546995a4dc60d8cac0669f356501c723
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a><span data-ttu-id="c3ada-103">Eclipse kullanarak bir temel Azure web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="c3ada-103">Create a basic Azure web app using Eclipse</span></span>
<span data-ttu-id="c3ada-104">Bu öğretici oluşturmak ve Azure Web uygulaması olarak temel bir Hello World uygulamayı kullanarak dağıtmak nasıl gösterir [Eclipse için Azure Araç Takımı].</span><span class="sxs-lookup"><span data-stu-id="c3ada-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="c3ada-105">Kolaylık olması için temel bir JSP örneği gösterilir, ancak Azure dağıtım ilgili olduğu kadar benzer adımlar bir Java servlet için uygun olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c3ada-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="c3ada-106">Bu öğreticiyi tamamladıktan sonra bir web tarayıcısında görüntülediğinizde, uygulamanızın aşağıdaki çizime benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="c3ada-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Önizleme Hello, World uygulama][01]

## <a name="prerequisites"></a><span data-ttu-id="c3ada-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c3ada-108">Prerequisites</span></span>
* <span data-ttu-id="c3ada-109">Bir Java Geliştirme Seti (JDK), v 1.8 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="c3ada-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="c3ada-110">Luna olan Java EE geliştiricileri için Eclipse IDE veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="c3ada-110">Eclipse IDE for Java EE Developers, Luna or later.</span></span> <span data-ttu-id="c3ada-111">Bu adresten yüklenebilir <http://www.eclipse.org/downloads/>.</span><span class="sxs-lookup"><span data-stu-id="c3ada-111">This can be downloaded from <http://www.eclipse.org/downloads/>.</span></span>
* <span data-ttu-id="c3ada-112">Dağıtım bir Java tabanlı web sunucusu veya uygulama sunucusu gibi [Apache Tomcat] veya [Jetty].</span><span class="sxs-lookup"><span data-stu-id="c3ada-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="c3ada-113">Öğesinden alınan bir Azure aboneliği <https://azure.microsoft.com/free/> veya <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="c3ada-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="c3ada-114">[Eclipse için Azure Araç Takımı].</span><span class="sxs-lookup"><span data-stu-id="c3ada-114">The [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="c3ada-115">Azure araç setini yükleme hakkında daha fazla bilgi için bkz: [Azure araç setini Eclipse için yükleme].</span><span class="sxs-lookup"><span data-stu-id="c3ada-115">For information about installing the Azure Toolkit, see [Installing the Azure Toolkit for Eclipse].</span></span>

## <a name="to-create-a-hello-world-application"></a><span data-ttu-id="c3ada-116">Merhaba Dünya uygulaması oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="c3ada-116">To create a Hello World application</span></span>
<span data-ttu-id="c3ada-117">İlk olarak, bir Java projesi oluşturma ile başlayacağız devre dışı.</span><span class="sxs-lookup"><span data-stu-id="c3ada-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="c3ada-118">Eclipse başlatın ve menüsünde tıklatın **dosya**, tıklatın **yeni**ve ardından **dinamik Web projesi**.</span><span class="sxs-lookup"><span data-stu-id="c3ada-118">Start Eclipse, and at the menu click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="c3ada-119">(Görmüyorsanız **dinamik Web projesi** tıkladıktan sonra kullanılabilir bir proje listelenen **dosya** ve **yeni**, aşağıdakileri yapın: tıklatın **dosya**,'ı tıklatın **yeni**, tıklatın **proje...** , genişletin **Web**, tıklatın **dinamik Web projesi**, tıklatıp **sonraki**.)</span><span class="sxs-lookup"><span data-stu-id="c3ada-119">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>
2. <span data-ttu-id="c3ada-120">Bu öğreticinin amaçları doğrultusunda, proje adı **mywebapp şeklindedir**.</span><span class="sxs-lookup"><span data-stu-id="c3ada-120">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="c3ada-121">Ekranınızın aşağıdakine benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="c3ada-121">Your screen will appear similar to the following:</span></span>
   
    ![Yeni bir dinamik Web projesi oluşturma][02]
3. <span data-ttu-id="c3ada-123">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c3ada-123">Click **Finish**.</span></span>
4. <span data-ttu-id="c3ada-124">Eclipse'nın Proje Gezgini görünümü içinde genişletmek **mywebapp şeklindedir**.</span><span class="sxs-lookup"><span data-stu-id="c3ada-124">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="c3ada-125">**WebContent**'e sağ tıklayın, **Yeni**'ye tıklayın ve ardından **JSP Dosyası**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c3ada-125">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
5. <span data-ttu-id="c3ada-126">İçinde **yeni JSP dosyası** iletişim kutusunda, dosya adı **index.jsp**, üst klasör olarak tutun **mywebapp şeklindedir/WebContent**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="c3ada-126">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>
6. <span data-ttu-id="c3ada-127">İçinde **JSP şablon seç** amacıyla Bu öğretici Seç iletişim kutusu **yeni JSP dosyası (html)**ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="c3ada-127">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
7. <span data-ttu-id="c3ada-128">İndex.jsp dosyası Eclipse'te açıldığında, dinamik olarak görüntülenecek metni eklemek **Merhaba Dünya!**</span><span class="sxs-lookup"><span data-stu-id="c3ada-128">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="c3ada-129">`<body>`Hello World! (Merhaba Dünya!) ifadesinin görüntülenmesi için metni ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c3ada-129">within the existing `<body>` element.</span></span> <span data-ttu-id="c3ada-130">Güncelleştirilmiş `<body>` içerik, aşağıdaki örnekte benzer:</span><span class="sxs-lookup"><span data-stu-id="c3ada-130">Your updated `<body>` content should resemble the following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. <span data-ttu-id="c3ada-131">İndex.jsp kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c3ada-131">Save index.jsp.</span></span>

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a><span data-ttu-id="c3ada-132">Bir Azure Web uygulaması kapsayıcısına uygulamanızı dağıtmak için</span><span class="sxs-lookup"><span data-stu-id="c3ada-132">To deploy your application to an Azure Web App Container</span></span>
<span data-ttu-id="c3ada-133">Bir Java web uygulaması azure'a dağıtabilir miyim birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="c3ada-133">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="c3ada-134">Bu öğreticide en basit açıklar: uygulamanızı Azure Web uygulaması kapsayıcıya dağıtılacak - hiçbir özel Proje türü ya da ek araçlar gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c3ada-134">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="c3ada-135">Bu yüzden karşıya yüklemek için gerekli kendi JDK ve web kapsayıcısı yazılım sizin için Azure tarafından sağlanacak; ihtiyacınız olan tek şey, Java Web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="c3ada-135">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="c3ada-136">Sonuç olarak, uygulamanız için yayımlama işlemi saniye, dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="c3ada-136">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="c3ada-137">Eclipse'nın Proje Gezgini'nde sağ **mywebapp şeklindedir**.</span><span class="sxs-lookup"><span data-stu-id="c3ada-137">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>
2. <span data-ttu-id="c3ada-138">Bağlam menüsünü **Azure**, ardından **Azure Web uygulaması olarak Yayımla...**</span><span class="sxs-lookup"><span data-stu-id="c3ada-138">In the context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
    ![Olarak Azure Web uygulaması yayımlama][03]
   
    <span data-ttu-id="c3ada-140">Alternatif olarak, web uygulama projesi Proje Gezgini'nde seçiliyken tıklayabilirsiniz **Yayımla** seçin ve araç çubuğundaki açılır düğmesini **Azure Web uygulaması olarak Yayımla** buradan:</span><span class="sxs-lookup"><span data-stu-id="c3ada-140">Alternatively, while your web application project is selected in the Project Explorer, you can click the **Publish** dropdown button on the toolbar and select **Publish as Azure Web App** from there:</span></span>
   
    ![Olarak Azure Web uygulaması yayımlama][14]
3. <span data-ttu-id="c3ada-142">Zaten Eclipse Azure'dan oturum açmış değil, Azure hesabınızda oturum açın istenir:</span><span class="sxs-lookup"><span data-stu-id="c3ada-142">If you have not already signed into Azure from Eclipse, you will be prompted to sign into your Azure account:</span></span>
   
    ![Azure oturum açma iletişim kutusu][04]
   
    <span data-ttu-id="c3ada-144">Birden çok Azure hesabınız yoksa, oturum açma işlemi sırasında istemleri bazıları aynı olması göründükleri olsa bile birden fazla kez gösterilebilir.</span><span class="sxs-lookup"><span data-stu-id="c3ada-144">If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="c3ada-145">Bu gerçekleştiğinde, oturum açma yönergeleri izleyerek devam edin.</span><span class="sxs-lookup"><span data-stu-id="c3ada-145">When this happens, continue following the sign in instructions.</span></span>
4. <span data-ttu-id="c3ada-146">Azure hesabınızda oturumu başarıyla sonra **Aboneliklerini Yönet** iletişim kutusunda kimlik bilgilerinizle ilişkili Aboneliklerin listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c3ada-146">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="c3ada-147">Birden çok abonelik listelenir ve bunların yalnızca belirli bir alt kümesiyle çalışmak istediğiniz varsa, isteğe bağlı olarak kullanmak istediğiniz olanları işaretini.</span><span class="sxs-lookup"><span data-stu-id="c3ada-147">If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the ones you do want to use.</span></span> <span data-ttu-id="c3ada-148">Aboneliklerinizi seçildiğinde tıklatın **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="c3ada-148">When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Yönet abonelikleri iletişim kutusu][05]
5. <span data-ttu-id="c3ada-150">Zaman **Azure Web uygulaması kapsayıcı Dağıt** iletişim kutusu görüntülenirse, daha önce oluşturduğunuz herhangi bir Web uygulaması kapsayıcıdaki görüntülenir; herhangi bir kapsayıcıdaki oluşturmadıysanız listesi boş olur.</span><span class="sxs-lookup"><span data-stu-id="c3ada-150">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
    ![Dağıt Azure Web uygulaması kapsayıcı iletişim kutusu][06]
6. <span data-ttu-id="c3ada-152">Bir Azure Web uygulaması kapsayıcısı önce oluşturmadıysanız veya yeni bir kapsayıcı uygulamanıza yayımlamak isterseniz, aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="c3ada-152">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="c3ada-153">Aksi takdirde, var olan bir Web uygulaması kapsayıcıyı seçin ve adım 7'ye atlayın.</span><span class="sxs-lookup"><span data-stu-id="c3ada-153">Otherwise, select an existing Web App Container and skip to step 7 below.</span></span>
   
   1. <span data-ttu-id="c3ada-154">Tıklatın **yeni...**</span><span class="sxs-lookup"><span data-stu-id="c3ada-154">Click **New...**</span></span>
      
       ![Dağıt Azure Web uygulaması kapsayıcı iletişim kutusu][15]
   2. <span data-ttu-id="c3ada-156">**Yeni Web uygulaması kapsayıcı** iletişim kutusu görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="c3ada-156">The **New Web App Container** dialog box will be displayed:</span></span>
      
       ![Yeni Web uygulaması kapsayıcı iletişim kutusu][07a]
   3. <span data-ttu-id="c3ada-158">Girin bir **DNS etiketi** Web uygulama kapsayıcısı için; bu, web uygulamanız için ana bilgisayar URL'si yaprak DNS etiketini Azure'da oluşturacak.</span><span class="sxs-lookup"><span data-stu-id="c3ada-158">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="c3ada-159">(Ad kullanılabilir ve adlandırma gereksinimlerini Azure Web uygulaması için uygun olduğunu unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="c3ada-159">(Note that the name must be available and conform to Azure Web App naming requirements.)</span></span>
   4. <span data-ttu-id="c3ada-160">İçinde **Web kapsayıcısına** açılır menüsünde, uygulamanız için uygun yazılım seçin.</span><span class="sxs-lookup"><span data-stu-id="c3ada-160">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
       <span data-ttu-id="c3ada-161">Şu anda, Tomcat 8, Tomcat 7 veya Jetty 9 seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3ada-161">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="c3ada-162">Seçilen yazılım yeni bir dağıtımını Azure tarafından sağlanacak ve JDK Oracle tarafından oluşturulan ve Azure tarafından sağlanan 8'in yeni bir dağıtım çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="c3ada-162">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="c3ada-163">İçinde **abonelik** açılır menüsünde, bu dağıtım için kullanmak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="c3ada-163">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>
   6. <span data-ttu-id="c3ada-164">İçinde **kaynak grubu** açılır menüsünde, istediğiniz Web uygulamanızı ilişkilendirmek kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="c3ada-164">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="c3ada-165">(Azure kaynak grupları, örneğin, bunlar birlikte silinebilir böylece ilgili kaynaklar gruplamak izin verir.)</span><span class="sxs-lookup"><span data-stu-id="c3ada-165">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="c3ada-166">Mevcut kaynak (varsa) grubu ve Atla g aşağıdaki adım seçin veya aşağıdaki yeni bir kaynak grubu oluşturmak üzere şu adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="c3ada-166">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following these steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="c3ada-167">Tıklatın **yeni...**</span><span class="sxs-lookup"><span data-stu-id="c3ada-167">Click **New...**</span></span>
      * <span data-ttu-id="c3ada-168">**Yeni kaynak grubu** iletişim kutusu görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="c3ada-168">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Yeni kaynak grubu iletişim kutusu][08]
      * <span data-ttu-id="c3ada-170">İçinde **adı** metin kutusuna, yeni kaynak grubunuz için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="c3ada-170">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="c3ada-171">İçinde **bölge** açılır menüsünde, select uygun Azure veri merkezi kaynak grubunuz için konum.</span><span class="sxs-lookup"><span data-stu-id="c3ada-171">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="c3ada-172">İsteğe bağlı: varsayılan olarak, yeni bir Java 8 dağıtımını Azure tarafından otomatik olarak, web app kapsayıcıya, JVM dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="c3ada-172">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically to your web app container as your JVM.</span></span> <span data-ttu-id="c3ada-173">Ancak, Web uygulamanızı gerektiriyorsa, farklı sürüm ve JVM dağıtımını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3ada-173">However, you can specify a different version and distribution of the JVM if your Web App requires it.</span></span> <span data-ttu-id="c3ada-174">Web uygulamanız için JDK belirtmek için tıklatın **JDK** sekmesini tıklatın ve aşağıdaki seçeneklerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="c3ada-174">To specify the JDK for your Web App, click the **JDK** tab, and select one of the following options:</span></span>
        
        * <span data-ttu-id="c3ada-175">**Azure Web uygulamaları hizmeti tarafından sunulan JDK varsayılan dağıtmak**: Bu seçenek Java 8 yeni bir dağıtımını dağıtır.</span><span class="sxs-lookup"><span data-stu-id="c3ada-175">**Deploy the default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
        * <span data-ttu-id="c3ada-176">**Bir 3. taraf JDK Azure üzerinde kullanılabilir dağıtmak**: Bu seçenek, Microsoft Azure tarafından sağlanan JDKs listesinden seçim yapmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="c3ada-176">**Deploy a 3rd party JDK available on Azure**: This option allows you to choose from the list of JDKs which are provided by Microsoft Azure.</span></span>
        * <span data-ttu-id="c3ada-177">**Bu yükleme konumdan kendi JDK dağıtımı**: Bu seçenek, bir ZIP dosyası olarak paketlenir ve genel kullanıma açık indirme konumu ya da erişim elinizde bir Azure depolama hesabı karşıya kendi JDK dağıtım belirtmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="c3ada-177">**Deploy my own JDK from this download location**: This option allows you to specify your own JDK distribution, which must be packaged as a ZIP file and uploaded to either a publicly available download location or an Azure storage account for which you have access.</span></span>
          
          ![Yeni Web uygulaması kapsayıcı iletişim kutusu][07b]
   7. <span data-ttu-id="c3ada-179">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c3ada-179">Click **OK**.</span></span>
   8. <span data-ttu-id="c3ada-180">**App Service planı** açılır menü, seçtiğiniz kaynak grubuyla ilişkili olan uygulama hizmeti planları listeler.</span><span class="sxs-lookup"><span data-stu-id="c3ada-180">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="c3ada-181">(Uygulama hizmeti planları, Web uygulamanızın, fiyatlandırma katmanı ve işlem örnek boyutu konumu gibi bilgileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="c3ada-181">(App Service Plans specify information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="c3ada-182">Tek bir uygulama hizmeti planı ayrı olarak belirli bir Web uygulaması dağıtımından korunan neden olan ve birden çok Web uygulamaları için kullanılabilir.)</span><span class="sxs-lookup"><span data-stu-id="c3ada-182">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="c3ada-183">Bir var olan App Service (varsa) planı ve Atla h aşağıdaki adım seçin veya yeni bir uygulama hizmeti planı oluşturmak üzere şu adımları aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="c3ada-183">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="c3ada-184">Tıklatın **yeni...**</span><span class="sxs-lookup"><span data-stu-id="c3ada-184">Click **New...**</span></span>
      * <span data-ttu-id="c3ada-185">**Yeni uygulama hizmeti planı** iletişim kutusu görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="c3ada-185">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Yeni uygulama hizmeti planı iletişim kutusu][09]
      * <span data-ttu-id="c3ada-187">İçinde **adı** metin kutusuna, yeni uygulama hizmeti planınız için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="c3ada-187">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="c3ada-188">İçinde **konumu** açılır menüsünde, select uygun Azure veri merkezi plan için konum.</span><span class="sxs-lookup"><span data-stu-id="c3ada-188">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="c3ada-189">İçinde **fiyatlandırma katmanı** açılır menüsünde, uygun fiyatlandırma planı seçin.</span><span class="sxs-lookup"><span data-stu-id="c3ada-189">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="c3ada-190">Test amacıyla seçebileceğiniz **serbest**.</span><span class="sxs-lookup"><span data-stu-id="c3ada-190">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="c3ada-191">İçinde **örnek boyutu** uygun örneğini boyut plan için aşağı açılan menüsünde seçin.</span><span class="sxs-lookup"><span data-stu-id="c3ada-191">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="c3ada-192">Test amacıyla seçebileceğiniz **küçük**.</span><span class="sxs-lookup"><span data-stu-id="c3ada-192">For testing purposes you can choose **Small**.</span></span>
   9. <span data-ttu-id="c3ada-193">Yukarıdaki adımları tamamladıktan sonra yeni Web uygulaması kapsayıcısı iletişim kutusunda aşağıdaki çizimde benzemelidir:</span><span class="sxs-lookup"><span data-stu-id="c3ada-193">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
       ![Yeni Web uygulaması kapsayıcı iletişim kutusu][10]
   10. <span data-ttu-id="c3ada-195">Tıklatın **Tamam** yeni Web uygulaması kapsayıcı oluşturma işlemini tamamlamak için.</span><span class="sxs-lookup"><span data-stu-id="c3ada-195">Click **OK** to complete the creation of your new Web App container.</span></span>
       
        <span data-ttu-id="c3ada-196">Web uygulaması kapsayıcılar listesi yenilenmesi birkaç saniye bekleyin ve listesinde yeni oluşturulan web uygulaması kapsayıcınız artık seçili olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c3ada-196">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>
7. <span data-ttu-id="c3ada-197">Şimdi Web uygulamanızı azure'a ilk dağıtımını tamamlamak hazırsınız:</span><span class="sxs-lookup"><span data-stu-id="c3ada-197">You are now ready to complete the initial deployment of your Web App to Azure:</span></span>
   
    ![Dağıt Azure Web uygulaması kapsayıcı iletişim kutusu][11]
   
    <span data-ttu-id="c3ada-199">Tıklatın **Tamam** seçili Web uygulaması kapsayıcısı Java uygulamanızı dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="c3ada-199">Click **OK** to deploy your Java application to the selected Web App container.</span></span>
   
    <span data-ttu-id="c3ada-200">Varsayılan olarak, uygulamanızın uygulama sunucusunun bir alt dizini olarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="c3ada-200">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="c3ada-201">Kök uygulaması olarak dağıtılmasını istiyorsanız, denetleme **kök Dağıt** tıklatmadan önce onay kutusunu **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="c3ada-201">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
8. <span data-ttu-id="c3ada-202">Ardından, görmelisiniz **Azure etkinlik günlüğü** Görünümü Web uygulamanızı dağıtım durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="c3ada-202">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
    ![Azure etkinlik günlüğü][12]
   
    <span data-ttu-id="c3ada-204">Web uygulamanızı Azure'a dağıtma işlemini tamamlamak için yalnızca birkaç saniye sürer.</span><span class="sxs-lookup"><span data-stu-id="c3ada-204">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="c3ada-205">Uygulama hazır gördüğünüzde adlı bir bağlantı **yayımlanan** içinde **durum** sütun.</span><span class="sxs-lookup"><span data-stu-id="c3ada-205">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="c3ada-206">Bağlantıya tıkladığında, dağıtılan Web uygulamanızın giriş sayfasına gideceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c3ada-206">When you click the link, it will take you to your deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="c3ada-207">Web uygulamanızı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="c3ada-207">Updating your web app</span></span>
<span data-ttu-id="c3ada-208">Azure Web uygulaması çalıştıran var olan bir güncelleştirme hızlı ve kolay bir işlemdir ve güncelleştirmek için iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="c3ada-208">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="c3ada-209">Varolan bir Java Web uygulaması dağıtımını güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3ada-209">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="c3ada-210">Aynı Web uygulama kapsayıcısı için ek bir Java uygulama yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3ada-210">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="c3ada-211">Her iki durumda da işlemi aynıdır ve yalnızca birkaç saniye sürer:</span><span class="sxs-lookup"><span data-stu-id="c3ada-211">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="c3ada-212">Eclipse proje Gezgini'nde, güncelleştirmek veya var olan bir Web uygulaması kapsayıcıyı eklemek istediğiniz Java uygulaması sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c3ada-212">In the Eclipse project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="c3ada-213">Bağlam menüsü görüntülendiğinde seçin **Azure** ve ardından **Azure Web uygulaması olarak Yayımla...**</span><span class="sxs-lookup"><span data-stu-id="c3ada-213">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="c3ada-214">Zaten daha önce oturum açtıktan sonra var olan Web uygulaması kapsayıcıları listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c3ada-214">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="c3ada-215">Yayımlama veya Java uygulamanızı yeniden yayımlayın ve istediğiniz bir tanesini seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="c3ada-215">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="c3ada-216">Daha sonra birkaç saniye **Azure etkinlik günlüğü** görünümü güncelleştirilmiş dağıtımınız olarak göster **yayımlanan** ve güncelleştirilmiş uygulamanız bir web tarayıcısında doğrulayamazsınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c3ada-216">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="c3ada-217">Başlatma, durdurma veya var olan bir web uygulamasının yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="c3ada-217">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="c3ada-218">Başlat veya Durdur (içinde dağıtılan tüm Java uygulamaları dahil), mevcut bir Azure Web uygulaması kapsayıcısı için kullanabileceğiniz **Azure Gezgini** görünümü.</span><span class="sxs-lookup"><span data-stu-id="c3ada-218">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="c3ada-219">Varsa **Azure Gezgini** görünüm zaten açık, ardından tıklayarak açabilirsiniz **penceresi** eclipse'te, ardından menüsünü **görünümü göster**, ardından **diğer...** , ardından **Azure**ve ardından **Azure Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="c3ada-219">If the **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="c3ada-220">Daha önce oturum açmamış olan, bunu yapmanızı ister.</span><span class="sxs-lookup"><span data-stu-id="c3ada-220">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="c3ada-221">Zaman **Azure Gezgini** görünümü görüntülenir, kullanım başlatmak veya Web uygulamanızı durdurmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c3ada-221">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="c3ada-222">Genişletme **Azure** düğümü.</span><span class="sxs-lookup"><span data-stu-id="c3ada-222">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="c3ada-223">Genişletme **Web Apps** düğümü.</span><span class="sxs-lookup"><span data-stu-id="c3ada-223">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="c3ada-224">İstediğiniz Web uygulamasını sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c3ada-224">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="c3ada-225">Bağlam menüsü görüntülendiğinde **Başlat**, **durdurmak**, veya **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="c3ada-225">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="c3ada-226">Yalnızca çalışan bir web uygulamasına durdurmak veya şu anda çalışmıyor bir web uygulamasını başlatmak için menü seçeneklerini Bağlam duyarlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c3ada-226">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Var olan bir Web uygulamasının durdurma][13]

## <a name="next-steps"></a><span data-ttu-id="c3ada-228">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="c3ada-228">Next Steps</span></span>
<span data-ttu-id="c3ada-229">Java IDE’leri için Azure Araç Setleri hakkında daha fazla bilgi için aşağıdaki bağlantılara bakın:</span><span class="sxs-lookup"><span data-stu-id="c3ada-229">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="c3ada-230">[Eclipse için Azure Araç Takımı]</span><span class="sxs-lookup"><span data-stu-id="c3ada-230">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c3ada-231">[Azure araç setini Eclipse için yükleme]</span><span class="sxs-lookup"><span data-stu-id="c3ada-231">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c3ada-232">*Eclipse (Bu makalede) Azure'da Hello World Web uygulaması oluşturun*</span><span class="sxs-lookup"><span data-stu-id="c3ada-232">*Create a Hello World Web App for Azure in Eclipse (This Article)*</span></span>
  * <span data-ttu-id="c3ada-233">[Eclipse için Azure Araç Seti Yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="c3ada-233">[What's New in the Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="c3ada-234">[IntelliJ için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="c3ada-234">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c3ada-235">[IntelliJ için Azure Araç Setini Yükleme]</span><span class="sxs-lookup"><span data-stu-id="c3ada-235">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c3ada-236">[Intellij Azure'da Hello World Web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="c3ada-236">[Create a Hello World Web App for Azure in IntelliJ]</span></span>
  * <span data-ttu-id="c3ada-237">[IntelliJ için Azure Araç Seti Yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="c3ada-237">[What's New in the Azure Toolkit for IntelliJ]</span></span>

<span data-ttu-id="c3ada-238">Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Azure Java Geliştirici Merkezi].</span><span class="sxs-lookup"><span data-stu-id="c3ada-238">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<span data-ttu-id="c3ada-239">Azure Web uygulamaları oluşturma hakkında ek bilgi için bkz: [Web Apps'e genel bakış].</span><span class="sxs-lookup"><span data-stu-id="c3ada-239">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

<span data-ttu-id="c3ada-240">[Eclipse için Azure Araç Takımı]: ../azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="c3ada-240">[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="c3ada-241">[IntelliJ için Azure Araç Seti]: ../azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="c3ada-241">[Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij.md</span></span>
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
<span data-ttu-id="c3ada-242">[Intellij Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="c3ada-242">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="c3ada-243">[Azure araç setini Eclipse için yükleme]: ../azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="c3ada-243">[Installing the Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="c3ada-244">[IntelliJ için Azure Araç Setini Yükleme]: ../azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="c3ada-244">[Installing the Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="c3ada-245">[Eclipse için Azure Araç Seti Yenilikleri]: ../azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="c3ada-245">[What's New in the Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="c3ada-246">[IntelliJ için Azure Araç Seti Yenilikleri]: ../azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="c3ada-246">[What's New in the Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="c3ada-247">[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="c3ada-247">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="c3ada-248">[Web Apps'e genel bakış]: ./app-service-web-overview.md</span><span class="sxs-lookup"><span data-stu-id="c3ada-248">[Web Apps Overview]: ./app-service-web-overview.md</span></span>
<span data-ttu-id="c3ada-249">[Apache Tomcat]: http://tomcat.apache.org/</span><span class="sxs-lookup"><span data-stu-id="c3ada-249">[Apache Tomcat]: http://tomcat.apache.org/</span></span>
<span data-ttu-id="c3ada-250">[Jetty]: http://www.eclipse.org/jetty/</span><span class="sxs-lookup"><span data-stu-id="c3ada-250">[Jetty]: http://www.eclipse.org/jetty/</span></span>

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
