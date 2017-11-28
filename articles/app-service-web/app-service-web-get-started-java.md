---
title: "aaaCreate ilk Java web uygulamanıza Azure"
description: "Nasıl toorun web uygulama hizmetinde uygulamalar temel bir Java uygulama dağıtarak öğrenin."
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
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="983ea-103">Azure’da ilk Java web uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="983ea-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="983ea-104">Merhaba [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) özelliği [Azure App Service](../app-service/app-service-value-prop-what-is.md) düzeyde ölçeklenebilir, otomatik olarak düzeltme eki uygulama web barındırma hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="983ea-104">hello [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="983ea-105">Bu hızlı başlangıç nasıl toodeploy bir Java web uygulaması tooApp hizmet hello kullanarak gösterir [Java EE geliştiricileri için Eclipse IDE](http://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="983ea-105">This quickstart shows how toodeploy a Java web app tooApp Service by using hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

!["Merhaba Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="983ea-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="983ea-108">Prerequisites</span></span>

<span data-ttu-id="983ea-109">toocomplete Bu hızlı başlangıç yükleyin:</span><span class="sxs-lookup"><span data-stu-id="983ea-109">toocomplete this quickstart, install:</span></span>

* <span data-ttu-id="983ea-110">Merhaba ücretsiz [Java EE geliştiricileri için Eclipse IDE](http://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="983ea-110">hello free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="983ea-111">Bu hızlı başlangıçta Eclipse Neon kullanılır.</span><span class="sxs-lookup"><span data-stu-id="983ea-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="983ea-112">Merhaba [Eclipse için Azure Araç Seti](/azure/azure-toolkit-for-eclipse-installation).</span><span class="sxs-lookup"><span data-stu-id="983ea-112">hello [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="983ea-113">Eclipse’te dinamik web projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="983ea-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="983ea-114">Eclipse’te **Dosya** > **Yeni** > **Dinamik Web Projesi**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="983ea-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="983ea-115">Merhaba, **yeni dinamik Web projesi** iletişim kutusu, ad hello proje **MyFirstJavaOnAzureWebApp**seçip **son**.</span><span class="sxs-lookup"><span data-stu-id="983ea-115">In hello **New Dynamic Web Project** dialog box, name hello project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![Yeni Dinamik Web Projesi iletişim kutusu](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="983ea-117">JSP sayfası ekleme</span><span class="sxs-lookup"><span data-stu-id="983ea-117">Add a JSP page</span></span>

<span data-ttu-id="983ea-118">Proje Gezgini görüntülenmiyorsa, gezgini geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="983ea-118">If Project Explorer is not displayed, restore it.</span></span>

![Eclipse için Java EE çalışma alanı](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="983ea-120">Proje Gezgini'nde hello genişletin **MyFirstJavaOnAzureWebApp** projesi.</span><span class="sxs-lookup"><span data-stu-id="983ea-120">In Project Explorer, expand hello **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="983ea-121">**WebContent**’e sağ tıklayın ve **Yeni** > **JSP Dosyası**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="983ea-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![Proje Gezgini'nde yeni JSP dosyasına yönelik menü](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="983ea-123">Merhaba, **yeni JSP dosyası** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="983ea-123">In hello **New JSP File** dialog box:</span></span>

* <span data-ttu-id="983ea-124">Ad hello dosyası **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="983ea-124">Name hello file **index.jsp**.</span></span>
* <span data-ttu-id="983ea-125">**Son**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="983ea-125">Select **Finish**.</span></span>

  ![Yeni JSP Dosyası iletişim kutusu](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="983ea-127">Merhaba index.jsp dosyasında hello değiştirin `<body></body>` biçimlendirme aşağıdaki hello sahip öğe:</span><span class="sxs-lookup"><span data-stu-id="983ea-127">In hello index.jsp file, replace hello `<body></body>` element with hello following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="983ea-128">Merhaba değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="983ea-128">Save hello changes.</span></span>

## <a name="publish-hello-web-app-tooazure"></a><span data-ttu-id="983ea-129">Yayımlama Hello web uygulama tooAzure</span><span class="sxs-lookup"><span data-stu-id="983ea-129">Publish hello web app tooAzure</span></span>

<span data-ttu-id="983ea-130">Proje Gezgini'nde hello projesine sağ tıklayın ve ardından **Azure** > **Azure Web uygulaması olarak Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="983ea-130">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Azure Web App Olarak Yayımla bağlam menüsü](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="983ea-132">Merhaba, **Azure oturum açma** iletişim kutusu, Canlı hello **etkileşimli** seçeneğini ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="983ea-132">In hello **Azure Sign In** dialog box, keep hello **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="983ea-133">Oturum açma Hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="983ea-133">Follow hello sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="983ea-134">Web Uygulaması Dağıtma iletişim kutusu</span><span class="sxs-lookup"><span data-stu-id="983ea-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="983ea-135">Tooyour Azure hesabı imzaladıktan sonra hello **Web uygulaması dağıtma** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="983ea-135">After you have signed in tooyour Azure account, hello **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="983ea-136">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="983ea-136">Select **Create**.</span></span>

![Web Uygulaması Dağıtma iletişim kutusu](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="983ea-138">App Service Oluşturma iletişim kutusu</span><span class="sxs-lookup"><span data-stu-id="983ea-138">Create App Service dialog box</span></span>

<span data-ttu-id="983ea-139">Merhaba **App Service Oluştur** varsayılan değerlerle iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="983ea-139">hello **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="983ea-140">Merhaba numarası **170602185241** aşağıdaki hello görüntü farklı iletişim kutusunda gösterilir.</span><span class="sxs-lookup"><span data-stu-id="983ea-140">hello number **170602185241** shown in hello following image is different in your dialog box.</span></span>

![App Service Oluşturma iletişim kutusu](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="983ea-142">Merhaba, **App Service Oluştur** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="983ea-142">In hello **Create App Service** dialog box:</span></span>

* <span data-ttu-id="983ea-143">Merhaba web uygulaması için oluşturulan hello adı bırakın.</span><span class="sxs-lookup"><span data-stu-id="983ea-143">Keep hello generated name for hello web app.</span></span> <span data-ttu-id="983ea-144">Bu ad Azure genelinde benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="983ea-144">This name must be unique across Azure.</span></span> <span data-ttu-id="983ea-145">Merhaba adı hello URL adresi hello web uygulaması için bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="983ea-145">hello name is part of hello URL address for hello web app.</span></span> <span data-ttu-id="983ea-146">Örneğin: hello web uygulaması adı ise **MyJavaWebApp**, URL hello *myjavawebapp.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="983ea-146">For example: if hello web app name is **MyJavaWebApp**, hello URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="983ea-147">Merhaba varsayılan web kapsayıcısını tutun.</span><span class="sxs-lookup"><span data-stu-id="983ea-147">Keep hello default web container.</span></span>
* <span data-ttu-id="983ea-148">Bir Azure aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="983ea-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="983ea-149">Merhaba üzerinde **uygulama hizmeti planı** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="983ea-149">On hello **App service plan** tab:</span></span>

  * <span data-ttu-id="983ea-150">**Yeni Oluştur**: hello uygulama hizmeti planı hello adıdır hello varsayılan tutun.</span><span class="sxs-lookup"><span data-stu-id="983ea-150">**Create new**: Keep hello default, which is hello name of hello App Service plan.</span></span>
  * <span data-ttu-id="983ea-151">**Konum**: **Batı Avrupa**’yı veya size yakın olan bir konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="983ea-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="983ea-152">**Fiyatlandırma katmanı**: Merhaba boş seçeneği seçin.</span><span class="sxs-lookup"><span data-stu-id="983ea-152">**Pricing tier**: Select hello free option.</span></span> <span data-ttu-id="983ea-153">Özellikler için bkz. [App Service fiyatlandırması](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="983ea-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![App Service Oluşturma iletişim kutusu](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="983ea-155">Kaynak grubu sekmesi</span><span class="sxs-lookup"><span data-stu-id="983ea-155">Resource group tab</span></span>

<span data-ttu-id="983ea-156">Select hello **kaynak grubu** sekmesi. Merhaba kaynak grubu için Hello oluşturulan varsayılan değeri koruyun.</span><span class="sxs-lookup"><span data-stu-id="983ea-156">Select hello **Resource group** tab. Keep hello default generated value for hello resource group.</span></span>

![Kaynak grubu sekmesi](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="983ea-158">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="983ea-158">Select **Create**.</span></span>

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="983ea-159">Hello Azure Araç Seti hello web uygulamasını oluşturur ve ilerleme durumu iletişim kutusu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="983ea-159">hello Azure Toolkit creates hello web app and displays a progress dialog box.</span></span>

![App Service Oluşturma İlerleme Durumu iletişim kutusu](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="983ea-161">Web Uygulaması Dağıtma iletişim kutusu</span><span class="sxs-lookup"><span data-stu-id="983ea-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="983ea-162">Merhaba, **Web uygulaması dağıtma** iletişim kutusunda **tooroot dağıtmak**.</span><span class="sxs-lookup"><span data-stu-id="983ea-162">In hello **Deploy Web App** dialog box, select **Deploy tooroot**.</span></span> <span data-ttu-id="983ea-163">Bir uygulama hizmeti varsa *wingtiptoys.azurewebsites.net* ve toohello kök, adlı hello web uygulamasına dağıtma **MyFirstJavaOnAzureWebApp** çok dağıtılan *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span><span class="sxs-lookup"><span data-stu-id="983ea-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy toohello root, hello web app named **MyFirstJavaOnAzureWebApp** is deployed too*wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![Web Uygulaması Dağıtma iletişim kutusu](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="983ea-165">Merhaba iletişim kutusunu gösterir hello Azure, JDK ve web kapsayıcısı seçimleri.</span><span class="sxs-lookup"><span data-stu-id="983ea-165">hello dialog box shows hello Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="983ea-166">Seçin **dağıtma** toopublish hello web uygulama tooAzure.</span><span class="sxs-lookup"><span data-stu-id="983ea-166">Select **Deploy** toopublish hello web app tooAzure.</span></span>

<span data-ttu-id="983ea-167">Yayımlama Hello sona erdiğinde, hello seçin **yayımlanan** hello bağlantıyı **Azure etkinlik günlüğü** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="983ea-167">When hello publishing finishes, select hello **Published** link in hello **Azure Activity Log** dialog box.</span></span>

![Azure Etkinlik Günlüğü iletişim kutusu](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="983ea-169">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="983ea-169">Congratulations!</span></span> <span data-ttu-id="983ea-170">Web uygulaması tooAzure başarıyla dağıtmış.</span><span class="sxs-lookup"><span data-stu-id="983ea-170">You have successfully deployed your web app tooAzure.</span></span> 

!["Merhaba Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a><span data-ttu-id="983ea-173">Güncelleştirme hello web uygulaması</span><span class="sxs-lookup"><span data-stu-id="983ea-173">Update hello web app</span></span>

<span data-ttu-id="983ea-174">Merhaba örnek JSP kod tooa farklı ileti değiştirin.</span><span class="sxs-lookup"><span data-stu-id="983ea-174">Change hello sample JSP code tooa different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="983ea-175">Merhaba değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="983ea-175">Save hello changes.</span></span>

<span data-ttu-id="983ea-176">Proje Gezgini'nde hello projesine sağ tıklayın ve ardından **Azure** > **Azure Web uygulaması olarak Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="983ea-176">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="983ea-177">Merhaba **Web uygulaması dağıtma** iletişim kutusu belirir ve daha önce oluşturduğunuz uygulama hizmeti hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="983ea-177">hello **Deploy Web App** dialog box appears and shows hello app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="983ea-178">Seçin **tooroot dağıtmak** yayımladığınız her zaman.</span><span class="sxs-lookup"><span data-stu-id="983ea-178">Select **Deploy tooroot** each time you publish.</span></span>
>

<span data-ttu-id="983ea-179">Merhaba web uygulaması seçip **dağıtma**, hello değişiklikleri yayımlar.</span><span class="sxs-lookup"><span data-stu-id="983ea-179">Select hello web app and select **Deploy**, which publishes hello changes.</span></span>

<span data-ttu-id="983ea-180">Ne zaman hello **yayımlama** toobrowse toohello web uygulamasını seçin ve hello değişiklikleri görmek bağlantısı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="983ea-180">When hello **Publishing** link appears, select it toobrowse toohello web app and see hello changes.</span></span>

## <a name="manage-hello-web-app"></a><span data-ttu-id="983ea-181">Merhaba web uygulamasını yönetme</span><span class="sxs-lookup"><span data-stu-id="983ea-181">Manage hello web app</span></span>

<span data-ttu-id="983ea-182">Toohello Git <a href="https://portal.azure.com" target="_blank">Azure portal</a> oluşturduğunuz toosee hello web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="983ea-182">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toosee hello web app that you created.</span></span>

<span data-ttu-id="983ea-183">Merhaba sol menüden seçin **kaynak grupları**.</span><span class="sxs-lookup"><span data-stu-id="983ea-183">From hello left menu, select **Resource Groups**.</span></span>

![Portal gezinme tooresource grupları](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="983ea-185">Merhaba kaynak grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="983ea-185">Select hello resource group.</span></span> <span data-ttu-id="983ea-186">Başlangıç sayfası, bu hızlı başlangıç, oluşturduğunuz hello kaynakları gösterir.</span><span class="sxs-lookup"><span data-stu-id="983ea-186">hello page shows hello resources that you created in this quickstart.</span></span>

![myResourceGroup kaynak grubu](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="983ea-188">Select hello web uygulaması (**webapp 170602193915** görüntü önceki hello içinde).</span><span class="sxs-lookup"><span data-stu-id="983ea-188">Select hello web app (**webapp-170602193915** in hello preceding image).</span></span>

<span data-ttu-id="983ea-189">Merhaba **genel bakış** sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="983ea-189">hello **Overview** page appears.</span></span> <span data-ttu-id="983ea-190">Bu sayfayı hello uygulama nasıl çalıştığını bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="983ea-190">This page gives you a view of how hello app is doing.</span></span> <span data-ttu-id="983ea-191">Buradan göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="983ea-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="983ea-192">Merhaba sekmeler hello sayfasının sol tarafında hello hello açabilirsiniz farklı yapılandırmaları gösterir.</span><span class="sxs-lookup"><span data-stu-id="983ea-192">hello tabs on hello left side of hello page show hello different configurations that you can open.</span></span> 

![Azure portalında App Service sayfası](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="983ea-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="983ea-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="983ea-195">Özel etki alanı eşleme</span><span class="sxs-lookup"><span data-stu-id="983ea-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
