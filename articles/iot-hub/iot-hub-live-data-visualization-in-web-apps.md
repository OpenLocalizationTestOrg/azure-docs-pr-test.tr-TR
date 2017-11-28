---
title: "Azure IOT hub'ınızı – Web Apps algılayıcı verilerini aaaReal zaman veri Görselleştirme | Microsoft Docs"
description: "Hello algılayıcı ' toplanan ve tooyour IOT hub gönderilen Microsoft Azure App Service toovisualize sıcaklık ve nem veri Hello Web Apps özelliğini kullanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "gerçek zamanlı veri görselleştirme, dinamik veri görselleştirme algılayıcı verileri Görselleştirme"
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a><span data-ttu-id="19348-104">Azure App Service Web Apps özelliğini hello kullanarak Azure IOT hub'ınızı gerçek zamanlı algılayıcı verilerini görselleştirmek</span><span class="sxs-lookup"><span data-stu-id="19348-104">Visualize real-time sensor data from your Azure IoT hub by using hello Web Apps feature of Azure App Service</span></span>

![Uçtan uca diyagramı](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="19348-106">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="19348-106">What you learn</span></span>

<span data-ttu-id="19348-107">Bu öğreticide, bir web uygulaması çalıştıran tarafından IOT hub'ınızın aldığı toovisualize gerçek zamanlı algılayıcı verilerini bir web uygulamasını nasıl barındırılan öğrenin.</span><span class="sxs-lookup"><span data-stu-id="19348-107">In this tutorial, you learn how toovisualize real-time sensor data that your IoT hub receives by running a web application that is hosted on a web app.</span></span> <span data-ttu-id="19348-108">Power BI kullanarak tootry toovisualize hello veri IOT hub'ınıza istiyorsanız bkz [kullanım Power BI toovisualize gerçek zamanlı algılayıcı verileri Azure IOT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="19348-108">If you want tootry toovisualize hello data in your IoT hub by using Power BI, see [Use Power BI toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="19348-109">Neler</span><span class="sxs-lookup"><span data-stu-id="19348-109">What you do</span></span>

- <span data-ttu-id="19348-110">Hello Azure portalında bir web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="19348-110">Create a web app in hello Azure portal.</span></span>
- <span data-ttu-id="19348-111">IOT hub'ınızı bir tüketici grubu ekleyerek veri erişimi için hazırlanın.</span><span class="sxs-lookup"><span data-stu-id="19348-111">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="19348-112">IOT hub'ınızı gelen Hello web uygulama tooread algılayıcı verileri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="19348-112">Configure hello web app tooread sensor data from your IoT hub.</span></span>
- <span data-ttu-id="19348-113">Merhaba web uygulaması tarafından barındırılan bir web uygulaması toobe karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="19348-113">Upload a web application toobe hosted by hello web app.</span></span>
- <span data-ttu-id="19348-114">Merhaba web uygulama toosee gerçek zamanlı sıcaklık ve nem verileri IOT hub'ından açın.</span><span class="sxs-lookup"><span data-stu-id="19348-114">Open hello web app toosee real-time temperature and humidity data from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="19348-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="19348-115">What you need</span></span>

- <span data-ttu-id="19348-116">[Cihazınızı ayarlamak](iot-hub-raspberry-pi-kit-node-get-started.md), hello gereksinimleri aşağıdaki kapsar:</span><span class="sxs-lookup"><span data-stu-id="19348-116">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md), which covers hello following requirements:</span></span>
  - <span data-ttu-id="19348-117">Etkin bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="19348-117">An active Azure subscription</span></span>
  - <span data-ttu-id="19348-118">Aboneliğinizdeki IOT hub'ı</span><span class="sxs-lookup"><span data-stu-id="19348-118">An Iot hub under your subscription</span></span>
  - <span data-ttu-id="19348-119">Tooyour IOT hub'ı iletileri gönderen bir istemci uygulaması</span><span class="sxs-lookup"><span data-stu-id="19348-119">A client application that sends messages tooyour Iot hub</span></span>
- [<span data-ttu-id="19348-120">Git indir</span><span class="sxs-lookup"><span data-stu-id="19348-120">Download Git</span></span>](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a><span data-ttu-id="19348-121">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="19348-121">Create a web app</span></span>

1. <span data-ttu-id="19348-122">Merhaba, [Azure portal](https://ms.portal.azure.com/), tıklatın **yeni** > **Web + mobil** > **Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="19348-122">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span></span>
2. <span data-ttu-id="19348-123">Benzersiz iş adını girin, hello abonelik doğrulayın, bir kaynak grubu ve select bir konum belirtin **PIN toodashboard**ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="19348-123">Enter a unique job name, verify hello subscription, specify a resource group and a location, select **Pin toodashboard**, and then click **Create**.</span></span>

   <span data-ttu-id="19348-124">Merhaba seçmenizi öneririz, kaynak grubunuzun aynı konumda.</span><span class="sxs-lookup"><span data-stu-id="19348-124">We recommend that you select hello same location as that of your resource group.</span></span> <span data-ttu-id="19348-125">Bunun yapılması, işlem hızı yardımcı olur ve veri aktarımı hello maliyetini azaltır.</span><span class="sxs-lookup"><span data-stu-id="19348-125">Doing so assists with processing speed and reduces hello cost of data transfer.</span></span>

   ![Web uygulaması oluşturma](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a><span data-ttu-id="19348-127">IOT hub'ınızı gelen Hello web uygulama tooread verileri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="19348-127">Configure hello web app tooread data from your IoT hub</span></span>

1. <span data-ttu-id="19348-128">Yalnızca sağlanan hello web uygulamasını açın.</span><span class="sxs-lookup"><span data-stu-id="19348-128">Open hello web app you’ve just provisioned.</span></span>
2. <span data-ttu-id="19348-129">Tıklatın **uygulama ayarları**ve ardından, **uygulama ayarları**, anahtar/değer çiftlerinin aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="19348-129">Click **Application settings**, and then, under **App settings**, add hello following key/value pairs:</span></span>

   | <span data-ttu-id="19348-130">Anahtar</span><span class="sxs-lookup"><span data-stu-id="19348-130">Key</span></span>                                   | <span data-ttu-id="19348-131">Değer</span><span class="sxs-lookup"><span data-stu-id="19348-131">Value</span></span>                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | <span data-ttu-id="19348-132">Azure.IoT.IoTHub.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="19348-132">Azure.IoT.IoTHub.ConnectionString</span></span>     | <span data-ttu-id="19348-133">Iothub Gezgini'nden elde</span><span class="sxs-lookup"><span data-stu-id="19348-133">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="19348-134">Azure.IoT.IoTHub.ConsumerGroup</span><span class="sxs-lookup"><span data-stu-id="19348-134">Azure.IoT.IoTHub.ConsumerGroup</span></span>        | <span data-ttu-id="19348-135">Merhaba adını hello tüketici grubu tooyour IOT hub'ı Ekle</span><span class="sxs-lookup"><span data-stu-id="19348-135">hello name of hello consumer group that you add tooyour IoT hub</span></span>  |

   ![Anahtar/değer çiftleri ile ayarları tooyour web uygulaması Ekle](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. <span data-ttu-id="19348-137">Tıklatın **uygulama ayarları**altında **genel ayarları**, iki durumlu hello **Web yuvaları** seçeneğini ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="19348-137">Click **Application settings**, under **General settings**, toggle hello **Web sockets** option, and then click **Save**.</span></span>

   ![İki durumlu hello Web yuva seçeneği](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a><span data-ttu-id="19348-139">Merhaba web uygulaması tarafından barındırılan bir web uygulaması toobe karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="19348-139">Upload a web application toobe hosted by hello web app</span></span>

<span data-ttu-id="19348-140">Github'da, IOT hub'ınızı gerçek zamanlı algılayıcı verileri görüntüleyen bir web uygulaması kullanılabilir yaptık.</span><span class="sxs-lookup"><span data-stu-id="19348-140">On GitHub, we've made available a web application that displays real-time sensor data from your IoT hub.</span></span> <span data-ttu-id="19348-141">Toodo gereken tek şey hello web uygulama toowork bir Git deposu ile yapılandırma Merhaba web uygulaması Github'dan indirin ve hello web uygulama toohost tooAzure karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="19348-141">All you need toodo is configure hello web app toowork with a Git repository, download hello web application from GitHub, and then upload it tooAzure for hello web app toohost.</span></span>

1. <span data-ttu-id="19348-142">Merhaba web uygulamasında tıklatın **dağıtım seçenekleri** > **Kaynağı Seç** > **yerel Git deposu**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="19348-142">In hello web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**, and then click **OK**.</span></span>

   ![Web uygulama dağıtım toouse hello yerel Git deponuzu yapılandırın](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. <span data-ttu-id="19348-144">Tıklatın **dağıtım kimlik bilgileri**, bir kullanıcı adı ve parola toouse tooconnect toohello Git deposu oluşturma ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="19348-144">Click **Deployment Credentials**, create a user name and password toouse tooconnect toohello Git repository in Azure, and then click **Save**.</span></span>

3. <span data-ttu-id="19348-145">Tıklatın **genel bakış**, hello değerini not edin **Git kopyası URL'si**.</span><span class="sxs-lookup"><span data-stu-id="19348-145">Click **Overview**, and note hello value of **Git clone url**.</span></span>

   ![Web uygulamanızın Hello Git kopya URL'si](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. <span data-ttu-id="19348-147">Bir komut veya yerel bilgisayarınızda terminal penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="19348-147">Open a command or terminal window on your local computer.</span></span>

5. <span data-ttu-id="19348-148">Github'dan Hello web uygulamasını indirmeye ve hello web uygulama toohost tooAzure yükleyin.</span><span class="sxs-lookup"><span data-stu-id="19348-148">Download hello web app from GitHub, and upload it tooAzure for hello web app toohost.</span></span> <span data-ttu-id="19348-149">toodo, bu nedenle, hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="19348-149">toodo so, run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > <span data-ttu-id="19348-150">\<Git kopyalama URL'si\> hello üzerinde bulunan hello Git deposu hello URL'sidir **genel bakış** hello web uygulaması sayfasında.</span><span class="sxs-lookup"><span data-stu-id="19348-150">\<Git clone URL\> is hello URL of hello Git repository found on hello **Overview** page of hello web app.</span></span>

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a><span data-ttu-id="19348-151">IOT hub'ından Hello web uygulama toosee gerçek zamanlı sıcaklık ve nem verileri açın</span><span class="sxs-lookup"><span data-stu-id="19348-151">Open hello web app toosee real-time temperature and humidity data from your IoT hub</span></span>

<span data-ttu-id="19348-152">Merhaba üzerinde **genel bakış** sayfa hello URL tooopen hello web uygulaması, web uygulamanızın ' ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="19348-152">On hello **Overview** page of your web app, click hello URL tooopen hello web app.</span></span>

![Web uygulamanızın Hello URL'sini alma](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

<span data-ttu-id="19348-154">IOT hub'ından hello gerçek zamanlı sıcaklık ve nem veri görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="19348-154">You should see hello real-time temperature and humidity data from your IoT hub.</span></span>

![Gerçek zamanlı sıcaklık ve nem gösteren web uygulama sayfası](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> <span data-ttu-id="19348-156">Merhaba örnek uygulaması aygıtınızda çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="19348-156">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="19348-157">Boş bir grafik alırsınız istemiyorsanız, toohello öğreticileri altında başvurabilir [Cihazınızı](iot-hub-raspberry-pi-kit-node-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="19348-157">If not, you will get a blank chart, you can refer toohello tutorials under [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="19348-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="19348-158">Next steps</span></span>
<span data-ttu-id="19348-159">IOT hub'ından web uygulama toovisualize gerçek zamanlı algılayıcı verilerini başarıyla kullanmış olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="19348-159">You've successfully used your web app toovisualize real-time sensor data from your IoT hub.</span></span>

<span data-ttu-id="19348-160">Bir alternatif yol toovisualize verileri için Azure IOT Hub, görmek [IOT hub'ınızı kullanın Power BI toovisualize gerçek zamanlı algılayıcı verileri](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="19348-160">For an alternative way toovisualize data from Azure IoT Hub, see [Use Power BI toovisualize real-time sensor data from your IoT hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
