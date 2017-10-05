---
title: "Azure’da ilk Java web uygulamanızı oluşturma"
description: "Basit bir Java uygulaması dağıtarak App Service'te web uygulamalarının nasıl çalıştırılacağını öğrenin."
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: b91b9bde5eb8ea0d7e2196056b635fe54095e748
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="725fb-103">Azure’da ilk Java web uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="725fb-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="725fb-104">[Azure Uygulama Hizmeti](../app-service/app-service-value-prop-what-is.md)’nin [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) özelliği, yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="725fb-104">The [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="725fb-105">Bu hızlı başlangıçta, [Java EE Geliştiricileri için Eclipse IDE](http://www.eclipse.org/) kullanarak App Service’e nasıl Java web uygulaması dağıtılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="725fb-105">This quickstart shows how to deploy a Java web app to App Service by using the [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

!["Merhaba Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="725fb-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="725fb-108">Prerequisites</span></span>

<span data-ttu-id="725fb-109">Bu hızlı başlangıcı tamamlamak için şunları yükleyin:</span><span class="sxs-lookup"><span data-stu-id="725fb-109">To complete this quickstart, install:</span></span>

* <span data-ttu-id="725fb-110">Ücretsiz [Java EE Geliştiricileri için Eclipse IDE](http://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="725fb-110">The free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="725fb-111">Bu hızlı başlangıçta Eclipse Neon kullanılır.</span><span class="sxs-lookup"><span data-stu-id="725fb-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="725fb-112">[Eclipse için Azure Araç Takımı](/azure/azure-toolkit-for-eclipse-installation).</span><span class="sxs-lookup"><span data-stu-id="725fb-112">The [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="725fb-113">Eclipse’te dinamik web projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="725fb-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="725fb-114">Eclipse’te **Dosya** > **Yeni** > **Dinamik Web Projesi**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="725fb-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="725fb-115">**Yeni Dinamik Web Projesi** iletişim kutusunda, projeyi **MyFirstJavaOnAzureWebApp** olarak adlandırın ve **Son**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="725fb-115">In the **New Dynamic Web Project** dialog box, name the project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![Yeni Dinamik Web Projesi iletişim kutusu](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="725fb-117">JSP sayfası ekleme</span><span class="sxs-lookup"><span data-stu-id="725fb-117">Add a JSP page</span></span>

<span data-ttu-id="725fb-118">Proje Gezgini görüntülenmiyorsa, gezgini geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="725fb-118">If Project Explorer is not displayed, restore it.</span></span>

![Eclipse için Java EE çalışma alanı](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="725fb-120">Proje Gezgini'nde **MyFirstJavaOnAzureWebApp** projesini genişletin.</span><span class="sxs-lookup"><span data-stu-id="725fb-120">In Project Explorer, expand the **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="725fb-121">**WebContent**’e sağ tıklayın ve **Yeni** > **JSP Dosyası**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="725fb-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![Proje Gezgini'nde yeni JSP dosyasına yönelik menü](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="725fb-123">**Yeni JSP Dosyası** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="725fb-123">In the **New JSP File** dialog box:</span></span>

* <span data-ttu-id="725fb-124">Dosyayı **index.jsp** olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="725fb-124">Name the file **index.jsp**.</span></span>
* <span data-ttu-id="725fb-125">**Son**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="725fb-125">Select **Finish**.</span></span>

  ![Yeni JSP Dosyası iletişim kutusu](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="725fb-127">index.jsp dosyasında, `<body></body>` öğesini aşağıdaki işaretlemeyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="725fb-127">In the index.jsp file, replace the `<body></body>` element with the following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="725fb-128">Değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="725fb-128">Save the changes.</span></span>

## <a name="publish-the-web-app-to-azure"></a><span data-ttu-id="725fb-129">Web uygulamasını Azure’da yayımlama</span><span class="sxs-lookup"><span data-stu-id="725fb-129">Publish the web app to Azure</span></span>

<span data-ttu-id="725fb-130">Proje Gezgini’nde projeye sağ tıklayın ve **Azure** > **Azure Web App olarak yayımla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="725fb-130">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Azure Web App Olarak Yayımla bağlam menüsü](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="725fb-132">**Azure Oturum Açma** iletişim kutusunda **Etkileşimli** seçeneğini değiştirmeyin ve **Oturum aç**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="725fb-132">In the **Azure Sign In** dialog box, keep the **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="725fb-133">Oturum açma yönergelerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="725fb-133">Follow the sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="725fb-134">Web Uygulaması Dağıtma iletişim kutusu</span><span class="sxs-lookup"><span data-stu-id="725fb-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="725fb-135">Azure hesabınızda oturum açtıktan sonra, **Web Uygulaması Dağıtma** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="725fb-135">After you have signed in to your Azure account, the **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="725fb-136">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="725fb-136">Select **Create**.</span></span>

![Web Uygulaması Dağıtma iletişim kutusu](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="725fb-138">App Service Oluşturma iletişim kutusu</span><span class="sxs-lookup"><span data-stu-id="725fb-138">Create App Service dialog box</span></span>

<span data-ttu-id="725fb-139">**App Service Oluşturma** iletişim kutusu varsayılan değerlerle açılır.</span><span class="sxs-lookup"><span data-stu-id="725fb-139">The **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="725fb-140">Aşağıdaki görüntüde gösterilen **170602185241** sayısı, sizin iletişim kutunuzda farklıdır.</span><span class="sxs-lookup"><span data-stu-id="725fb-140">The number **170602185241** shown in the following image is different in your dialog box.</span></span>

![App Service Oluşturma iletişim kutusu](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="725fb-142">**App Service Oluşturma** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="725fb-142">In the **Create App Service** dialog box:</span></span>

* <span data-ttu-id="725fb-143">Web uygulaması için oluşturulan adı değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="725fb-143">Keep the generated name for the web app.</span></span> <span data-ttu-id="725fb-144">Bu ad Azure genelinde benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="725fb-144">This name must be unique across Azure.</span></span> <span data-ttu-id="725fb-145">Ad, web uygulamasının URL adresinin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="725fb-145">The name is part of the URL address for the web app.</span></span> <span data-ttu-id="725fb-146">Örneğin, web uygulamasının adı **MyJavaWebApp** ise URL şu şekildedir: *myjavawebapp.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="725fb-146">For example: if the web app name is **MyJavaWebApp**, the URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="725fb-147">Varsayılan web kapsayıcısını değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="725fb-147">Keep the default web container.</span></span>
* <span data-ttu-id="725fb-148">Bir Azure aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="725fb-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="725fb-149">**App Service planı** sekmesinde:</span><span class="sxs-lookup"><span data-stu-id="725fb-149">On the **App service plan** tab:</span></span>

  * <span data-ttu-id="725fb-150">**Yeni oluştur**: App Service planının adı olan varsayılan değeri değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="725fb-150">**Create new**: Keep the default, which is the name of the App Service plan.</span></span>
  * <span data-ttu-id="725fb-151">**Konum**: **Batı Avrupa**’yı veya size yakın olan bir konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="725fb-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="725fb-152">**Fiyatlandırma katmanı**: Ücretsiz seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="725fb-152">**Pricing tier**: Select the free option.</span></span> <span data-ttu-id="725fb-153">Özellikler için bkz. [App Service fiyatlandırması](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="725fb-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![App Service Oluşturma iletişim kutusu](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="725fb-155">Kaynak grubu sekmesi</span><span class="sxs-lookup"><span data-stu-id="725fb-155">Resource group tab</span></span>

<span data-ttu-id="725fb-156">**Kaynak grubu** sekmesini seçin. Kaynak grubu için oluşturulmuş varsayılan değeri değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="725fb-156">Select the **Resource group** tab. Keep the default generated value for the resource group.</span></span>

![Kaynak grubu sekmesi](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="725fb-158">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="725fb-158">Select **Create**.</span></span>

<!--
### The JDK tab

Select the **JDK** tab. Keep the default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="725fb-159">Azure Araç Takımı web uygulamasını oluşturur ve bir ilerleme durumu iletişim kutusu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="725fb-159">The Azure Toolkit creates the web app and displays a progress dialog box.</span></span>

![App Service Oluşturma İlerleme Durumu iletişim kutusu](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="725fb-161">Web Uygulaması Dağıtma iletişim kutusu</span><span class="sxs-lookup"><span data-stu-id="725fb-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="725fb-162">**Web Uygulaması Dağıtma** iletişim kutusunda **Köke dağıt**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="725fb-162">In the **Deploy Web App** dialog box, select **Deploy to root**.</span></span> <span data-ttu-id="725fb-163">*wingtiptoys.azurewebsites.net* adresinde bir uygulama hizmetiniz varsa ve köke dağıtmazsanız, **MyFirstJavaOnAzureWebApp** adlı web uygulaması *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp* adresine dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="725fb-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy to the root, the web app named **MyFirstJavaOnAzureWebApp** is deployed to *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![Web Uygulaması Dağıtma iletişim kutusu](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="725fb-165">İletişim kutusunda Azure, JDK ve web kapsayıcısı seçimleri gösterilir.</span><span class="sxs-lookup"><span data-stu-id="725fb-165">The dialog box shows the Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="725fb-166">Web uygulamasını Azure’da yayımlamak için **Dağıt**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="725fb-166">Select **Deploy** to publish the web app to Azure.</span></span>

<span data-ttu-id="725fb-167">Yayımlama işlemi tamamlandığında, **Azure Etkinlik Günlüğü** iletişim kutusundaki **Yayımlandı** bağlantısını seçin.</span><span class="sxs-lookup"><span data-stu-id="725fb-167">When the publishing finishes, select the **Published** link in the **Azure Activity Log** dialog box.</span></span>

![Azure Etkinlik Günlüğü iletişim kutusu](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="725fb-169">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="725fb-169">Congratulations!</span></span> <span data-ttu-id="725fb-170">Web uygulamanızı başarılı bir şekilde Azure’da dağıttınız.</span><span class="sxs-lookup"><span data-stu-id="725fb-170">You have successfully deployed your web app to Azure.</span></span> 

!["Merhaba Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-the-web-app"></a><span data-ttu-id="725fb-173">Web uygulamasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="725fb-173">Update the web app</span></span>

<span data-ttu-id="725fb-174">Örnek JSP kodunu farklı bir ileti olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="725fb-174">Change the sample JSP code to a different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="725fb-175">Değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="725fb-175">Save the changes.</span></span>

<span data-ttu-id="725fb-176">Proje Gezgini’nde projeye sağ tıklayın ve **Azure** > **Azure Web App olarak yayımla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="725fb-176">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="725fb-177">**Web Uygulaması Dağıtma** iletişim kutusu açılır ve daha önce oluşturduğunuz uygulama hizmetini gösterir.</span><span class="sxs-lookup"><span data-stu-id="725fb-177">The **Deploy Web App** dialog box appears and shows the app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="725fb-178">Her yayımlama işleminde **Köke dağıt**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="725fb-178">Select **Deploy to root** each time you publish.</span></span>
>

<span data-ttu-id="725fb-179">Web uygulamasını seçip **Dağıt**’ı seçin. Bunu yaptığınızda değişiklikler yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="725fb-179">Select the web app and select **Deploy**, which publishes the changes.</span></span>

<span data-ttu-id="725fb-180">**Yayımlanıyor** bağlantısı göründüğünde, web uygulamasına gitmek ve değişiklikleri görmek için bu bağlantıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="725fb-180">When the **Publishing** link appears, select it to browse to the web app and see the changes.</span></span>

## <a name="manage-the-web-app"></a><span data-ttu-id="725fb-181">Web uygulamasını yönetme</span><span class="sxs-lookup"><span data-stu-id="725fb-181">Manage the web app</span></span>

<span data-ttu-id="725fb-182">Oluşturduğunuz web uygulamasını görmek için <a href="https://portal.azure.com" target="_blank">Azure portalına</a> gidin.</span><span class="sxs-lookup"><span data-stu-id="725fb-182">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to see the web app that you created.</span></span>

<span data-ttu-id="725fb-183">Soldaki menüden **Kaynak Grupları**'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="725fb-183">From the left menu, select **Resource Groups**.</span></span>

![Portalda kaynak gruplarına gitme](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="725fb-185">Kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="725fb-185">Select the resource group.</span></span> <span data-ttu-id="725fb-186">Sayfada bu hızlı başlangıçta oluşturduğunuz kaynaklar gösterilir.</span><span class="sxs-lookup"><span data-stu-id="725fb-186">The page shows the resources that you created in this quickstart.</span></span>

![myResourceGroup kaynak grubu](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="725fb-188">Web uygulamasını (önceki resimde **webapp-170602193915**) seçin.</span><span class="sxs-lookup"><span data-stu-id="725fb-188">Select the web app (**webapp-170602193915** in the preceding image).</span></span>

<span data-ttu-id="725fb-189">**Genel Bakış** sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="725fb-189">The **Overview** page appears.</span></span> <span data-ttu-id="725fb-190">Bu sayfada uygulamanın nasıl çalıştığına ilişkin bir görünüm sağlanır.</span><span class="sxs-lookup"><span data-stu-id="725fb-190">This page gives you a view of how the app is doing.</span></span> <span data-ttu-id="725fb-191">Buradan göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="725fb-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="725fb-192">Sayfanın sol tarafındaki sekmeler, açabileceğiniz farklı yapılandırmaları gösterir.</span><span class="sxs-lookup"><span data-stu-id="725fb-192">The tabs on the left side of the page show the different configurations that you can open.</span></span> 

![Azure portalında App Service sayfası](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="725fb-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="725fb-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="725fb-195">Özel etki alanı eşleme</span><span class="sxs-lookup"><span data-stu-id="725fb-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
