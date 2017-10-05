---
title: "Intellij içinde bir temel Azure web uygulaması oluşturma | Microsoft Docs"
description: "Bu öğretici bir Hello World Web uygulaması Azure için oluşturmak üzere Intellij için Azure Araç Seti kullanmayı gösterir."
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
ms.openlocfilehash: 20b2c3d86f5bde9302647f345aa99b030d78613a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="4a5e5-103">Intellij içinde bir temel Azure web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="4a5e5-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="4a5e5-104">Bu öğretici oluşturmak ve Azure Web uygulaması olarak temel bir Hello World uygulamayı kullanarak dağıtmak nasıl gösterir [Intellij için Azure Araç Seti].</span><span class="sxs-lookup"><span data-stu-id="4a5e5-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="4a5e5-105">Kolaylık olması için temel bir JSP örneği gösterilir, ancak Azure dağıtım ilgili olduğu kadar benzer adımlar bir Java servlet için uygun olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="4a5e5-106">Bu öğreticiyi tamamladıktan sonra bir web tarayıcısında görüntülediğinizde, uygulamanızın aşağıdaki çizime benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="4a5e5-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Örnek bir Web sayfası][01]

## <a name="prerequisites"></a><span data-ttu-id="4a5e5-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4a5e5-108">Prerequisites</span></span>
* <span data-ttu-id="4a5e5-109">Bir Java Geliştirme Seti (JDK), v 1.8 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="4a5e5-110">Intellij Idea Ultimate Edition.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="4a5e5-111">Bu adresten yüklenebilir <https://www.jetbrains.com/idea/download/index.html>.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="4a5e5-112">Dağıtım bir Java tabanlı web sunucusu veya uygulama sunucusu gibi [Apache Tomcat] veya [Jetty].</span><span class="sxs-lookup"><span data-stu-id="4a5e5-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="4a5e5-113">Öğesinden alınan bir Azure aboneliği <https://azure.microsoft.com/free/> veya <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="4a5e5-114">[Intellij için Azure Araç Seti].</span><span class="sxs-lookup"><span data-stu-id="4a5e5-114">The [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="4a5e5-115">Azure araç setini yükleme hakkında daha fazla bilgi için bkz: [Intellij için Azure araç setini yükleme].</span><span class="sxs-lookup"><span data-stu-id="4a5e5-115">For information about installing the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ].</span></span>

## <a name="to-create-a-hello-world-application"></a><span data-ttu-id="4a5e5-116">Merhaba Dünya uygulaması oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="4a5e5-116">To create a Hello World application</span></span>
<span data-ttu-id="4a5e5-117">İlk olarak, bir Java projesi oluşturma ile başlayacağız devre dışı.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="4a5e5-118">Intellij başlatır ve **dosya** menüsünde, ardından **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-118">Start IntelliJ and click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![Dosya yeni proje][02]
2. <span data-ttu-id="4a5e5-120">Yeni Proje iletişim kutusunda seçin **Java**, ardından **Web uygulaması**ve ardından **yeni** proje SDK eklemek için.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-120">In the New Project dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span></span>
   
    ![Yeni Proje İletişim Kutusu][03a]
   
3. <span data-ttu-id="4a5e5-122">Seçin giriş dizinini JDK iletişim kutusu, JDK yüklendiği klasörü ve ardından seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-122">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="4a5e5-123">Tıklatın **sonraki** devam etmek için yeni proje iletişim kutusunda.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-123">Click **Next** in the New Project dialog box to continue.</span></span>
   
    ![JDK giriş dizini belirtin][03b]
4. <span data-ttu-id="4a5e5-125">Bu öğreticinin amaçları doğrultusunda, proje adı **Java-Web-App-üzerinde-Azure**ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-125">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![Yeni Proje İletişim Kutusu][04]
5. <span data-ttu-id="4a5e5-127">Intellij'ın Proje Gezgini görünümü içinde genişletmek **Java-Web-App-üzerinde-Azure**, ardından **web**, çift tıklayın ve ardından **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![Açık dizin sayfası][05c]
6. <span data-ttu-id="4a5e5-129">İndex.jsp dosyası içinde Intellij açıldığında, dinamik olarak görüntülenecek metni eklemek **Merhaba Dünya!**</span><span class="sxs-lookup"><span data-stu-id="4a5e5-129">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="4a5e5-130">`<body>`Hello World! (Merhaba Dünya!) ifadesinin görüntülenmesi için metni ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-130">within the existing `<body>` element.</span></span> <span data-ttu-id="4a5e5-131">Güncelleştirilmiş `<body>` içerik, aşağıdaki örnekte benzer:</span><span class="sxs-lookup"><span data-stu-id="4a5e5-131">Your updated `<body>` content should resemble the following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="4a5e5-132">İndex.jsp kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-132">Save index.jsp.</span></span>

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a><span data-ttu-id="4a5e5-133">Bir Azure Web uygulaması kapsayıcısına uygulamanızı dağıtmak için</span><span class="sxs-lookup"><span data-stu-id="4a5e5-133">To deploy your application to an Azure Web App Container</span></span>
<span data-ttu-id="4a5e5-134">Bir Java web uygulaması azure'a dağıtabilir miyim birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-134">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="4a5e5-135">Bu öğreticide en basit açıklar: uygulamanızı Azure Web uygulaması kapsayıcıya dağıtılacak - hiçbir özel Proje türü ya da ek araçlar gereklidir.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-135">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="4a5e5-136">Bu yüzden karşıya yüklemek için gerekli kendi JDK ve web kapsayıcısı yazılım sizin için Azure tarafından sağlanacak; ihtiyacınız olan tek şey, Java Web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-136">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="4a5e5-137">Sonuç olarak, uygulamanız için yayımlama işlemi saniye, dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-137">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="4a5e5-138">Uygulamanızı yayınlamadan önce ilk modülü ayarlarını yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-138">Before you publish your application, you first need to configure your module settings.</span></span> <span data-ttu-id="4a5e5-139">Bunu yapmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="4a5e5-139">To do so, use the following steps:</span></span>

1. <span data-ttu-id="4a5e5-140">Intellij'ın Proje Gezgini'nde sağ **Java-Web-App-üzerinde-Azure** projesi.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-140">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="4a5e5-141">Bağlam menüsü görüntülendiğinde **açık modülü ayarları**.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-141">When the context menu appears, click **Open Module Settings**.</span></span>

    ![Modül Ayarları'nı açın][05a]
2. <span data-ttu-id="4a5e5-143">Proje Yapısı iletişim kutusu görüntülendiğinde:</span><span class="sxs-lookup"><span data-stu-id="4a5e5-143">When the Project Structure dialog box appears:</span></span>

   <span data-ttu-id="4a5e5-144">a.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-144">a.</span></span> <span data-ttu-id="4a5e5-145">Tıklatın **yapıları** listesinde **proje ayarları**.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-145">Click **Artifacts** in the list of **Project Settings**.</span></span>
   <span data-ttu-id="4a5e5-146">b.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-146">b.</span></span> <span data-ttu-id="4a5e5-147">Yapı adını değiştirmek **adı** boşluk veya özel karakterler içermiyor kutusuna; adı Tekdüzen Kaynak Tanımlayıcısı (URI) kullanılacağından bu gereklidir.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-147">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="4a5e5-148">c.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-148">c.</span></span> <span data-ttu-id="4a5e5-149">Değişiklik **türü** için **Web uygulaması: Arşiv**.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-149">Change the **Type** to **Web Application: Archive**.</span></span>
   <span data-ttu-id="4a5e5-150">d.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-150">d.</span></span> <span data-ttu-id="4a5e5-151">Tıklatın **Tamam** proje yapısını iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-151">Click **OK** to close the Project Structure dialog box.</span></span>

    ![Modül Ayarları'nı açın][05b]

<span data-ttu-id="4a5e5-153">Modül ayarlarınızı yapılandırdığınızda, aşağıdaki adımları kullanarak uygulamanızı Azure'a yayımlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4a5e5-153">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span></span>

1. <span data-ttu-id="4a5e5-154">Intellij'ın Proje Gezgini'nde sağ **Java-Web-App-üzerinde-Azure** projesi.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-154">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="4a5e5-155">Bağlam menüsü görüntülendiğinde seçin **Azure**ve ardından **Azure Web uygulaması olarak Yayımla...**</span><span class="sxs-lookup"><span data-stu-id="4a5e5-155">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Azure yayımlama bağlam menüsü][06]
2. <span data-ttu-id="4a5e5-157">Zaten Intellij Azure'dan oturum açmış değil, Azure hesabınızda oturum açın istenir.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-157">If you have not already signed into Azure from IntelliJ, you will be prompted to sign into your Azure account.</span></span> <span data-ttu-id="4a5e5-158">(Birden çok Azure hesabınız yoksa, bunlar aynı olması görünse bile oturum açma işlemi sırasında istemleri bazıları birden fazla kez gösterilebilir.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-158">(If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="4a5e5-159">Bu gerçekleştiğinde, oturum açma yönergelerini izlemeye devam edin.)</span><span class="sxs-lookup"><span data-stu-id="4a5e5-159">When this happens, continue to follow the sign in instructions.)</span></span>
   
    ![Azure oturum açma iletişim kutusu][07]
3. <span data-ttu-id="4a5e5-161">Azure hesabınızda oturumu başarıyla sonra **Aboneliklerini Yönet** iletişim kutusunda kimlik bilgilerinizle ilişkili Aboneliklerin listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-161">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="4a5e5-162">(Var olan ve birden çok abonelik listelenen yalnızca belirli bir alt kümesini bunları çalışmak istediğiniz, isteğe bağlı olarak kullanmak istemediğiniz abonelikleri kutusunun işaretini.) Aboneliklerinizi seçildiğinde tıklatın **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-162">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Aboneliklerini Yönetme][08]
4. <span data-ttu-id="4a5e5-164">Zaman **Azure Web uygulaması kapsayıcı Dağıt** iletişim kutusu görüntülenirse, daha önce oluşturduğunuz herhangi bir Web uygulaması kapsayıcıdaki görüntülenir; herhangi bir kapsayıcıdaki oluşturmadıysanız listesi boş olur.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-164">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
    ![Uygulama kapsayıcıları][09]
5. <span data-ttu-id="4a5e5-166">Bir Azure Web uygulaması kapsayıcısı önce oluşturmadıysanız veya yeni bir kapsayıcı uygulamanıza yayımlamak isterseniz, aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-166">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="4a5e5-167">Aksi takdirde, var olan bir Web uygulaması kapsayıcı seçin ve adım 6 atlayın.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-167">Otherwise, select an existing Web App Container and skip to step 6 below.</span></span>
   
   1. <span data-ttu-id="4a5e5-168">' I tıklatın**+**</span><span class="sxs-lookup"><span data-stu-id="4a5e5-168">Click **+**</span></span>
      
       ![Uygulama kapsayıcısı Ekle][10]
   2. <span data-ttu-id="4a5e5-170">**Yeni Web uygulaması kapsayıcı** iletişim kutusu görüntülenir, sonraki birkaç adımlar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-170">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span></span>
      
       ![Yeni uygulama kapsayıcısı][11a]
   3. <span data-ttu-id="4a5e5-172">Girin bir **DNS etiketi** Web uygulama kapsayıcısı için; bu, web uygulamanız için ana bilgisayar URL'si yaprak DNS etiketini Azure'da oluşturacak.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-172">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="4a5e5-173">Ad kullanılabilir ve adlandırma gereksinimlerini Azure Web uygulaması için uygun olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-173">Note that the name must be available and conform to Azure Web App naming requirements.</span></span>
   4. <span data-ttu-id="4a5e5-174">İçinde **Web kapsayıcısına** açılır menüsünde, uygulamanız için uygun yazılım seçin.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-174">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
       <span data-ttu-id="4a5e5-175">Şu anda, Tomcat 8, Tomcat 7 veya Jetty 9 seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="4a5e5-176">Seçilen yazılım yeni bir dağıtımını Azure tarafından sağlanacak ve JDK Oracle tarafından oluşturulan ve Azure tarafından sağlanan 8'in yeni bir dağıtım çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-176">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="4a5e5-177">İçinde **abonelik** açılır menüsünde, bu dağıtım için kullanmak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-177">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>
   6. <span data-ttu-id="4a5e5-178">İçinde **kaynak grubu** açılır menüsünde, istediğiniz Web uygulamanızı ilişkilendirmek kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-178">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="4a5e5-179">(Azure kaynak grupları, örneğin, bunlar birlikte silinebilir böylece ilgili kaynaklar gruplamak izin verir.)</span><span class="sxs-lookup"><span data-stu-id="4a5e5-179">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="4a5e5-180">Mevcut kaynak (varsa) grubu ve Atla g aşağıdaki adım seçin veya yeni bir kaynak grubu oluşturmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="4a5e5-180">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="4a5e5-181">Seçin  **&lt; &lt; yeni kaynak grubu oluştur &gt; &gt;**  içinde **kaynak grubu** açılır menü.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="4a5e5-182">**Yeni kaynak grubu** iletişim kutusu görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="4a5e5-182">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Yeni kaynak grubu][12]
      * <span data-ttu-id="4a5e5-184">İçinde **adı** metin kutusuna, yeni kaynak grubunuz için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-184">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="4a5e5-185">İçinde **bölge** açılır menüsünde, select uygun Azure veri merkezi kaynak grubunuz için konum.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-185">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="4a5e5-186">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-186">Click **OK**.</span></span>
   7. <span data-ttu-id="4a5e5-187">**App Service planı** açılır menü, seçtiğiniz kaynak grubuyla ilişkili olan uygulama hizmeti planları listeler.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-187">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="4a5e5-188">(Konum, Web uygulamanızın fiyatlandırma katmanı ve işlem örnek boyutu gibi bilgileri belirtir bir uygulama hizmeti planı.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-188">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="4a5e5-189">Tek bir uygulama hizmeti planı ayrı olarak belirli bir Web uygulaması dağıtımından korunan neden olan ve birden çok Web uygulamaları için kullanılabilir.)</span><span class="sxs-lookup"><span data-stu-id="4a5e5-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="4a5e5-190">Bir var olan App Service (varsa) planı ve Atla h aşağıdaki adım seçin veya yeni bir uygulama hizmeti planı oluşturmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="4a5e5-190">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="4a5e5-191">Seçin  **&lt; &lt; yeni uygulama hizmeti planı oluştur &gt; &gt;**  içinde **App Service planı** açılır menü.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="4a5e5-192">**Yeni uygulama hizmeti planı** iletişim kutusu görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="4a5e5-192">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Yeni uygulama hizmeti planı][13]
      * <span data-ttu-id="4a5e5-194">İçinde **adı** metin kutusuna, yeni uygulama hizmeti planınız için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-194">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="4a5e5-195">İçinde **konumu** açılır menüsünde, select uygun Azure veri merkezi plan için konum.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-195">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="4a5e5-196">İçinde **fiyatlandırma katmanı** açılır menüsünde, uygun fiyatlandırma planı seçin.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-196">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="4a5e5-197">Test amacıyla seçebileceğiniz **serbest**.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="4a5e5-198">İçinde **örnek boyutu** uygun örneğini boyut plan için aşağı açılan menüsünde seçin.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-198">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="4a5e5-199">Test amacıyla seçebileceğiniz **küçük**.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="4a5e5-200">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-200">Click **OK**.</span></span>
   8. <span data-ttu-id="4a5e5-201">(İsteğe bağlı) Varsayılan olarak, Java 8 yeni bir dağıtımını otomatik, JVM Azure tarafından web uygulaması kapsayıcıya dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span></span> <span data-ttu-id="4a5e5-202">Ancak, farklı sürüm ve JVM dağıtımını seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-202">However, you can select a different version and distribution of the JVM.</span></span> <span data-ttu-id="4a5e5-203">Bunu yapmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="4a5e5-203">To do so, use the following steps:</span></span>
      
      * <span data-ttu-id="4a5e5-204">Tıklatın **JDK** sekmesinde **yeni Web uygulaması kapsayıcı** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-204">Click the **JDK** tab in the **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="4a5e5-205">Aşağıdaki seçeneklerden birini seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4a5e5-205">You can choose from one of the following options:</span></span>
        
        * <span data-ttu-id="4a5e5-206">Varsayılan Azure tarafından sunulan JDK dağıtma</span><span class="sxs-lookup"><span data-stu-id="4a5e5-206">Deploy the default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="4a5e5-207">Bir 3. taraf JDK Azure üzerinde kullanılabilir olan ek JDKs aşağı açılan listesinden dağıtma</span><span class="sxs-lookup"><span data-stu-id="4a5e5-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="4a5e5-208">ZIP dosyası olarak ve ya da paketlenmesi gereken özel bir JDK dağıtımı Azure depolama hesabınızdaki veya genel olarak kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="4a5e5-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![Yeni uygulama kapsayıcı JDK sekmesi][11b]
   9. <span data-ttu-id="4a5e5-210">Yukarıdaki adımları tamamladıktan sonra yeni Web uygulaması kapsayıcısı iletişim kutusunda aşağıdaki çizimde benzemelidir:</span><span class="sxs-lookup"><span data-stu-id="4a5e5-210">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
       ![Yeni uygulama kapsayıcısı][14]
   10. <span data-ttu-id="4a5e5-212">Tıklatın **Tamam** yeni Web uygulaması kapsayıcı oluşturma işlemini tamamlamak için.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-212">Click **OK** to complete the creation of your new Web App container.</span></span>
       
        <span data-ttu-id="4a5e5-213">Web uygulaması kapsayıcılar listesi yenilenmesi birkaç saniye bekleyin ve listesinde yeni oluşturulan web uygulaması kapsayıcınız artık seçili olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-213">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>
6. <span data-ttu-id="4a5e5-214">Şimdi Web uygulamanızı azure'a ilk dağıtımını tamamlamak hazır olursunuz; tıklatın **Tamam** seçili Web uygulaması kapsayıcısı Java uygulamanızı dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-214">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span></span> <span data-ttu-id="4a5e5-215">Varsayılan olarak, uygulamanızın uygulama sunucusunun bir alt dizini olarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-215">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="4a5e5-216">Kök uygulaması olarak dağıtılmasını istiyorsanız, denetleme **kök Dağıt** tıklatmadan önce onay kutusunu **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-216">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
   
    ![Azure'a dağıtma][15]
7. <span data-ttu-id="4a5e5-218">Ardından, görmelisiniz **Azure etkinlik günlüğü** Görünümü Web uygulamanızı dağıtım durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-218">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
    ![İlerleme göstergesi][16]
   
    <span data-ttu-id="4a5e5-220">Web uygulamanızı Azure'a dağıtma işlemini tamamlamak için yalnızca birkaç saniye sürer.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-220">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="4a5e5-221">Uygulama hazır gördüğünüzde adlı bir bağlantı **yayımlanan** içinde **durum** sütun.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-221">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="4a5e5-222">Bağlantıya tıkladığında, dağıtılan Web uygulamanızın giriş sayfasına gideceksiniz ya da web uygulamanıza göz atmak için aşağıdaki bölümdeki adımları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-222">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span></span>

## <a name="browsing-to-your-web-app-on-azure"></a><span data-ttu-id="4a5e5-223">Azure üzerinde Web uygulamanıza gözatma</span><span class="sxs-lookup"><span data-stu-id="4a5e5-223">Browsing to your Web App on Azure</span></span>
<span data-ttu-id="4a5e5-224">Azure üzerinde Web uygulamanıza göz atmak için kullanabileceğiniz **Azure Gezgini** görünümü.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-224">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="4a5e5-225">Varsa **Azure Gezgini** görünüm zaten açık, ardından tıklayarak açabilirsiniz **Görünüm** Intellij, menüde ardından **aracı Windows**ve ardından  **Hizmet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-225">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="4a5e5-226">Daha önce oturum açmamış olan, bunu yapmanızı ister.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-226">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="4a5e5-227">Zaman **Azure Gezgini** görünümü görüntülenir, kullanma, Web uygulamanızın gözatmak için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4a5e5-227">When the **Azure Explorer** view is displayed, use follow these steps to browse to your Web App:</span></span> 

1. <span data-ttu-id="4a5e5-228">Genişletme **Azure** düğümü.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-228">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="4a5e5-229">Genişletme **Web Apps** düğümü.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-229">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="4a5e5-230">İstediğiniz Web uygulamasını sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-230">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="4a5e5-231">Bağlam menüsü görüntülendiğinde **tarayıcıda aç**.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-231">When the context menu appears, click **Open in Browser**.</span></span>
   
    ![Web uygulaması Gözat][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="4a5e5-233">Web uygulamanızı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="4a5e5-233">Updating your web app</span></span>
<span data-ttu-id="4a5e5-234">Azure Web uygulaması çalıştıran var olan bir güncelleştirme hızlı ve kolay bir işlemdir ve güncelleştirmek için iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="4a5e5-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="4a5e5-235">Varolan bir Java Web uygulaması dağıtımını güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-235">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="4a5e5-236">Aynı Web uygulama kapsayıcısı için ek bir Java uygulama yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-236">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="4a5e5-237">Her iki durumda da işlemi aynıdır ve yalnızca birkaç saniye sürer:</span><span class="sxs-lookup"><span data-stu-id="4a5e5-237">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="4a5e5-238">Intellij proje Gezgini'nde, güncelleştirmek veya var olan bir Web uygulaması kapsayıcıyı eklemek istediğiniz Java uygulaması sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-238">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="4a5e5-239">Bağlam menüsü görüntülendiğinde seçin **Azure** ve ardından **Azure Web uygulaması olarak Yayımla...**</span><span class="sxs-lookup"><span data-stu-id="4a5e5-239">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="4a5e5-240">Zaten daha önce oturum açtıktan sonra var olan Web uygulaması kapsayıcıları listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="4a5e5-241">Yayımlama veya Java uygulamanızı yeniden yayımlayın ve istediğiniz bir tanesini seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-241">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="4a5e5-242">Daha sonra birkaç saniye **Azure etkinlik günlüğü** görünümü güncelleştirilmiş dağıtımınız olarak göster **yayımlanan** ve güncelleştirilmiş uygulamanız bir web tarayıcısında doğrulayamazsınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-242">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="4a5e5-243">Başlatma, durdurma veya var olan bir web uygulamasının yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="4a5e5-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="4a5e5-244">Başlat veya Durdur (içinde dağıtılan tüm Java uygulamaları dahil), mevcut bir Azure Web uygulaması kapsayıcısı için kullanabileceğiniz **Azure Gezgini** görünümü.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-244">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="4a5e5-245">Varsa **Azure Gezgini** görünüm zaten açık, ardından tıklayarak açabilirsiniz **Görünüm** Intellij, menüde ardından **aracı Windows**ve ardından  **Hizmet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-245">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="4a5e5-246">Daha önce oturum açmamış olan, bunu yapmanızı ister.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-246">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="4a5e5-247">Zaman **Azure Gezgini** görünümü görüntülenir, kullanım başlatmak veya Web uygulamanızı durdurmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4a5e5-247">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="4a5e5-248">Genişletme **Azure** düğümü.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-248">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="4a5e5-249">Genişletme **Web Apps** düğümü.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-249">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="4a5e5-250">İstediğiniz Web uygulamasını sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-250">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="4a5e5-251">Bağlam menüsü görüntülendiğinde **Başlat**, **durdurmak**, veya **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-251">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="4a5e5-252">Yalnızca çalışan bir web uygulamasına durdurmak veya şu anda çalışmıyor bir web uygulamasını başlatmak için menü seçeneklerini Bağlam duyarlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-252">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Web uygulamasını Durdur][18]

## <a name="next-steps"></a><span data-ttu-id="4a5e5-254">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="4a5e5-254">Next Steps</span></span>
<span data-ttu-id="4a5e5-255">Java IDE’leri için Azure Araç Setleri hakkında daha fazla bilgi için aşağıdaki bağlantılara bakın:</span><span class="sxs-lookup"><span data-stu-id="4a5e5-255">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="4a5e5-256">[Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="4a5e5-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4a5e5-257">[Eclipse için Azure Araç Setini Yükleme]</span><span class="sxs-lookup"><span data-stu-id="4a5e5-257">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4a5e5-258">[Eclipse Azure'da Hello World Web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="4a5e5-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="4a5e5-259">[Eclipse için Azure Araç Seti Yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="4a5e5-259">[What's New in the Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="4a5e5-260">[Intellij için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="4a5e5-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="4a5e5-261">[Intellij için Azure araç setini yükleme]</span><span class="sxs-lookup"><span data-stu-id="4a5e5-261">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="4a5e5-262">*Intellij (Bu makalede) Azure'da Hello World Web uygulaması oluşturun*</span><span class="sxs-lookup"><span data-stu-id="4a5e5-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="4a5e5-263">[IntelliJ için Azure Araç Seti Yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="4a5e5-263">[What's New in the Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="4a5e5-264">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="4a5e5-264">See Also</span></span>
<span data-ttu-id="4a5e5-265">Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Azure Java Geliştirici Merkezi].</span><span class="sxs-lookup"><span data-stu-id="4a5e5-265">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<span data-ttu-id="4a5e5-266">Azure Web uygulamaları oluşturma hakkında ek bilgi için bkz: [Web Apps'e genel bakış].</span><span class="sxs-lookup"><span data-stu-id="4a5e5-266">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ../azure-toolkit-for-eclipse.md
[Intellij için Azure Araç Seti]: ../azure-toolkit-for-intellij.md
[Eclipse Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Eclipse için Azure Araç Setini Yükleme]: ../azure-toolkit-for-eclipse-installation.md
[Intellij için Azure araç setini yükleme]: ../azure-toolkit-for-intellij-installation.md
[Eclipse için Azure Araç Seti Yenilikleri]: ../azure-toolkit-for-eclipse-whats-new.md
[IntelliJ için Azure Araç Seti Yenilikleri]: ../azure-toolkit-for-intellij-whats-new.md

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
