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
# <a name="create-your-first-java-web-app-in-azure"></a>Azure’da ilk Java web uygulamanızı oluşturma

Merhaba [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) özelliği [Azure App Service](../app-service/app-service-value-prop-what-is.md) düzeyde ölçeklenebilir, otomatik olarak düzeltme eki uygulama web barındırma hizmeti sağlar. Bu hızlı başlangıç nasıl toodeploy bir Java web uygulaması tooApp hizmet hello kullanarak gösterir [Java EE geliştiricileri için Eclipse IDE](http://www.eclipse.org/).

!["Merhaba Azure!" örnek web uygulaması](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu hızlı başlangıç yükleyin:

* Merhaba ücretsiz [Java EE geliştiricileri için Eclipse IDE](http://www.eclipse.org/downloads/). Bu hızlı başlangıçta Eclipse Neon kullanılır.
* Merhaba [Eclipse için Azure Araç Seti](/azure/azure-toolkit-for-eclipse-installation).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a>Eclipse’te dinamik web projesi oluşturma

Eclipse’te **Dosya** > **Yeni** > **Dinamik Web Projesi**’ni seçin.

Merhaba, **yeni dinamik Web projesi** iletişim kutusu, ad hello proje **MyFirstJavaOnAzureWebApp**seçip **son**.
   
![Yeni Dinamik Web Projesi iletişim kutusu](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a>JSP sayfası ekleme

Proje Gezgini görüntülenmiyorsa, gezgini geri yükleyin.

![Eclipse için Java EE çalışma alanı](./media/app-service-web-get-started-java/pe.png)

Proje Gezgini'nde hello genişletin **MyFirstJavaOnAzureWebApp** projesi.
**WebContent**’e sağ tıklayın ve **Yeni** > **JSP Dosyası**’nı seçin.

![Proje Gezgini'nde yeni JSP dosyasına yönelik menü](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

Merhaba, **yeni JSP dosyası** iletişim kutusunda:

* Ad hello dosyası **index.jsp**.
* **Son**’u seçin.

  ![Yeni JSP Dosyası iletişim kutusu](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

Merhaba index.jsp dosyasında hello değiştirin `<body></body>` biçimlendirme aşağıdaki hello sahip öğe:

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

Merhaba değişiklikleri kaydedin.

## <a name="publish-hello-web-app-tooazure"></a>Yayımlama Hello web uygulama tooAzure

Proje Gezgini'nde hello projesine sağ tıklayın ve ardından **Azure** > **Azure Web uygulaması olarak Yayımla**.

![Azure Web App Olarak Yayımla bağlam menüsü](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

Merhaba, **Azure oturum açma** iletişim kutusu, Canlı hello **etkileşimli** seçeneğini ve ardından **oturum**.

Oturum açma Hello yönergeleri izleyin.

### <a name="deploy-web-app-dialog-box"></a>Web Uygulaması Dağıtma iletişim kutusu

Tooyour Azure hesabı imzaladıktan sonra hello **Web uygulaması dağıtma** iletişim kutusu görüntülenir.

**Oluştur**’u seçin.

![Web Uygulaması Dağıtma iletişim kutusu](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a>App Service Oluşturma iletişim kutusu

Merhaba **App Service Oluştur** varsayılan değerlerle iletişim kutusu görüntülenir. Merhaba numarası **170602185241** aşağıdaki hello görüntü farklı iletişim kutusunda gösterilir.

![App Service Oluşturma iletişim kutusu](./media/app-service-web-get-started-java/cas1.png)

Merhaba, **App Service Oluştur** iletişim kutusunda:

* Merhaba web uygulaması için oluşturulan hello adı bırakın. Bu ad Azure genelinde benzersiz olmalıdır. Merhaba adı hello URL adresi hello web uygulaması için bir parçasıdır. Örneğin: hello web uygulaması adı ise **MyJavaWebApp**, URL hello *myjavawebapp.azurewebsites.net*.
* Merhaba varsayılan web kapsayıcısını tutun.
* Bir Azure aboneliği seçin.
* Merhaba üzerinde **uygulama hizmeti planı** sekmesi:

  * **Yeni Oluştur**: hello uygulama hizmeti planı hello adıdır hello varsayılan tutun.
  * **Konum**: **Batı Avrupa**’yı veya size yakın olan bir konumu seçin.
  * **Fiyatlandırma katmanı**: Merhaba boş seçeneği seçin. Özellikler için bkz. [App Service fiyatlandırması](https://azure.microsoft.com/pricing/details/app-service/).

   ![App Service Oluşturma iletişim kutusu](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a>Kaynak grubu sekmesi

Select hello **kaynak grubu** sekmesi. Merhaba kaynak grubu için Hello oluşturulan varsayılan değeri koruyun.

![Kaynak grubu sekmesi](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

**Oluştur**’u seçin.

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

Hello Azure Araç Seti hello web uygulamasını oluşturur ve ilerleme durumu iletişim kutusu görüntüler.

![App Service Oluşturma İlerleme Durumu iletişim kutusu](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a>Web Uygulaması Dağıtma iletişim kutusu

Merhaba, **Web uygulaması dağıtma** iletişim kutusunda **tooroot dağıtmak**. Bir uygulama hizmeti varsa *wingtiptoys.azurewebsites.net* ve toohello kök, adlı hello web uygulamasına dağıtma **MyFirstJavaOnAzureWebApp** çok dağıtılan *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.

![Web Uygulaması Dağıtma iletişim kutusu](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

Merhaba iletişim kutusunu gösterir hello Azure, JDK ve web kapsayıcısı seçimleri.

Seçin **dağıtma** toopublish hello web uygulama tooAzure.

Yayımlama Hello sona erdiğinde, hello seçin **yayımlanan** hello bağlantıyı **Azure etkinlik günlüğü** iletişim kutusu.

![Azure Etkinlik Günlüğü iletişim kutusu](./media/app-service-web-get-started-java/aal.png)

Tebrikler! Web uygulaması tooAzure başarıyla dağıtmış. 

!["Merhaba Azure!" örnek web uygulaması](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a>Güncelleştirme hello web uygulaması

Merhaba örnek JSP kod tooa farklı ileti değiştirin.

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

Merhaba değişiklikleri kaydedin.

Proje Gezgini'nde hello projesine sağ tıklayın ve ardından **Azure** > **Azure Web uygulaması olarak Yayımla**.

Merhaba **Web uygulaması dağıtma** iletişim kutusu belirir ve daha önce oluşturduğunuz uygulama hizmeti hello gösterir. 

> [!NOTE]
> Seçin **tooroot dağıtmak** yayımladığınız her zaman.
>

Merhaba web uygulaması seçip **dağıtma**, hello değişiklikleri yayımlar.

Ne zaman hello **yayımlama** toobrowse toohello web uygulamasını seçin ve hello değişiklikleri görmek bağlantısı görüntülenir.

## <a name="manage-hello-web-app"></a>Merhaba web uygulamasını yönetme

Toohello Git <a href="https://portal.azure.com" target="_blank">Azure portal</a> oluşturduğunuz toosee hello web uygulaması.

Merhaba sol menüden seçin **kaynak grupları**.

![Portal gezinme tooresource grupları](media/app-service-web-get-started-java/rg.png)

Merhaba kaynak grubu seçin. Başlangıç sayfası, bu hızlı başlangıç, oluşturduğunuz hello kaynakları gösterir.

![myResourceGroup kaynak grubu](media/app-service-web-get-started-java/rg2.png)

Select hello web uygulaması (**webapp 170602193915** görüntü önceki hello içinde).

Merhaba **genel bakış** sayfası görüntülenir. Bu sayfayı hello uygulama nasıl çalıştığını bir görünümünü sağlar. Buradan göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz. Merhaba sekmeler hello sayfasının sol tarafında hello hello açabilirsiniz farklı yapılandırmaları gösterir. 

![Azure portalında App Service sayfası](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a>Sonraki adımlar

> [!div class="nextstepaction"]
> [Özel etki alanı eşleme](app-service-web-tutorial-custom-domain.md)
