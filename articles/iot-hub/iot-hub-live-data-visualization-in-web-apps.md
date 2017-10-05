---
title: "Azure IOT hub'ınızı – Web Apps algılayıcı verilerini gerçek zamanlı veri Görselleştirme | Microsoft Docs"
description: "Algılayıcı toplanan ve IOT hub'ına gönderilen sıcaklık ve nem verileri görselleştirmek için Microsoft Azure App Service Web Apps özelliğini kullanın."
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
ms.openlocfilehash: e037f5c29cabf8e5d0d3e7ded187280a0652d5c3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-the-web-apps-feature-of-azure-app-service"></a><span data-ttu-id="86a36-104">Azure App Service Web Apps özelliğini kullanarak Azure IOT hub'ınızı gerçek zamanlı algılayıcı verilerini görselleştirmek</span><span class="sxs-lookup"><span data-stu-id="86a36-104">Visualize real-time sensor data from your Azure IoT hub by using the Web Apps feature of Azure App Service</span></span>

![Uçtan uca diyagramı](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="86a36-106">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="86a36-106">What you learn</span></span>

<span data-ttu-id="86a36-107">Bu öğreticide, bir web uygulaması üzerinde barındırılan bir web uygulaması çalıştırarak IOT hub'ınızın aldığı gerçek zamanlı algılayıcı verilerini görselleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="86a36-107">In this tutorial, you learn how to visualize real-time sensor data that your IoT hub receives by running a web application that is hosted on a web app.</span></span> <span data-ttu-id="86a36-108">Power BI kullanarak IOT hub'ınızı verileri görselleştirmek denemek istiyorsanız bkz [kullanım Power BI'ı, Azure IOT hub'ı gerçek zamanlı algılayıcı verilerini görselleştirmek için](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="86a36-108">If you want to try to visualize the data in your IoT hub by using Power BI, see [Use Power BI to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="86a36-109">Neler</span><span class="sxs-lookup"><span data-stu-id="86a36-109">What you do</span></span>

- <span data-ttu-id="86a36-110">Azure portalında bir web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="86a36-110">Create a web app in the Azure portal.</span></span>
- <span data-ttu-id="86a36-111">IOT hub'ınızı bir tüketici grubu ekleyerek veri erişimi için hazırlanın.</span><span class="sxs-lookup"><span data-stu-id="86a36-111">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="86a36-112">IOT hub'ından algılayıcı verileri okumak için web uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="86a36-112">Configure the web app to read sensor data from your IoT hub.</span></span>
- <span data-ttu-id="86a36-113">Web uygulaması tarafından barındırılan bir web uygulamasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="86a36-113">Upload a web application to be hosted by the web app.</span></span>
- <span data-ttu-id="86a36-114">IOT hub'ınızı gerçek zamanlı sıcaklık ve nem verileri görmek için web uygulamasını açın.</span><span class="sxs-lookup"><span data-stu-id="86a36-114">Open the web app to see real-time temperature and humidity data from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="86a36-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="86a36-115">What you need</span></span>

- <span data-ttu-id="86a36-116">[Cihazınızı ayarlamak](iot-hub-raspberry-pi-kit-node-get-started.md), aşağıdaki gereksinimleri ele alınmaktadır:</span><span class="sxs-lookup"><span data-stu-id="86a36-116">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md), which covers the following requirements:</span></span>
  - <span data-ttu-id="86a36-117">Etkin bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="86a36-117">An active Azure subscription</span></span>
  - <span data-ttu-id="86a36-118">Aboneliğinizdeki IOT hub'ı</span><span class="sxs-lookup"><span data-stu-id="86a36-118">An Iot hub under your subscription</span></span>
  - <span data-ttu-id="86a36-119">IOT hub'ına iletileri gönderen bir istemci uygulaması</span><span class="sxs-lookup"><span data-stu-id="86a36-119">A client application that sends messages to your Iot hub</span></span>
- [<span data-ttu-id="86a36-120">Git indir</span><span class="sxs-lookup"><span data-stu-id="86a36-120">Download Git</span></span>](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a><span data-ttu-id="86a36-121">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="86a36-121">Create a web app</span></span>

1. <span data-ttu-id="86a36-122">İçinde [Azure portal](https://ms.portal.azure.com/), tıklatın **yeni** > **Web + mobil** > **Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="86a36-122">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span></span>
2. <span data-ttu-id="86a36-123">Benzersiz iş adını girin, aboneliğinizi doğrulamak, bir kaynak grubu ve select bir konum belirtin **panoya Sabitle**ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="86a36-123">Enter a unique job name, verify the subscription, specify a resource group and a location, select **Pin to dashboard**, and then click **Create**.</span></span>

   <span data-ttu-id="86a36-124">Aynı konumu, kaynak grubu seçmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="86a36-124">We recommend that you select the same location as that of your resource group.</span></span> <span data-ttu-id="86a36-125">Bunun yapılması, işlem hızı yardımcı olur ve veri aktarımı maliyeti azaltır.</span><span class="sxs-lookup"><span data-stu-id="86a36-125">Doing so assists with processing speed and reduces the cost of data transfer.</span></span>

   ![Web uygulaması oluşturma](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-the-web-app-to-read-data-from-your-iot-hub"></a><span data-ttu-id="86a36-127">IOT hub'ından veri okumak için web uygulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="86a36-127">Configure the web app to read data from your IoT hub</span></span>

1. <span data-ttu-id="86a36-128">Yalnızca sağlanan web uygulamasını açın.</span><span class="sxs-lookup"><span data-stu-id="86a36-128">Open the web app you’ve just provisioned.</span></span>
2. <span data-ttu-id="86a36-129">Tıklatın **uygulama ayarları**ve ardından, **uygulama ayarları**, aşağıdaki anahtar/değer çiftleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="86a36-129">Click **Application settings**, and then, under **App settings**, add the following key/value pairs:</span></span>

   | <span data-ttu-id="86a36-130">Anahtar</span><span class="sxs-lookup"><span data-stu-id="86a36-130">Key</span></span>                                   | <span data-ttu-id="86a36-131">Değer</span><span class="sxs-lookup"><span data-stu-id="86a36-131">Value</span></span>                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | <span data-ttu-id="86a36-132">Azure.IoT.IoTHub.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="86a36-132">Azure.IoT.IoTHub.ConnectionString</span></span>     | <span data-ttu-id="86a36-133">Iothub Gezgini'nden elde</span><span class="sxs-lookup"><span data-stu-id="86a36-133">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="86a36-134">Azure.IoT.IoTHub.ConsumerGroup</span><span class="sxs-lookup"><span data-stu-id="86a36-134">Azure.IoT.IoTHub.ConsumerGroup</span></span>        | <span data-ttu-id="86a36-135">IOT hub'ınızı ekleyin tüketici grubu adı</span><span class="sxs-lookup"><span data-stu-id="86a36-135">The name of the consumer group that you add to your IoT hub</span></span>  |

   ![Anahtar/değer çiftleri ile web uygulamanızın ayarlarını ekleyin](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. <span data-ttu-id="86a36-137">Tıklatın **uygulama ayarları**altında **genel ayarları**, iki durumlu **Web yuvaları** seçeneğini ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="86a36-137">Click **Application settings**, under **General settings**, toggle the **Web sockets** option, and then click **Save**.</span></span>

   ![Web yuvaları seçeneğini Değiştir](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-to-be-hosted-by-the-web-app"></a><span data-ttu-id="86a36-139">Web uygulaması tarafından barındırılan bir web uygulaması karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="86a36-139">Upload a web application to be hosted by the web app</span></span>

<span data-ttu-id="86a36-140">Github'da, IOT hub'ınızı gerçek zamanlı algılayıcı verileri görüntüleyen bir web uygulaması kullanılabilir yaptık.</span><span class="sxs-lookup"><span data-stu-id="86a36-140">On GitHub, we've made available a web application that displays real-time sensor data from your IoT hub.</span></span> <span data-ttu-id="86a36-141">Yapmanız gereken tek şey bir Git deposu ile iş web uygulaması Github'dan indirin ve ardından barındırmak için web uygulaması için Azure'a yüklemeniz için web uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="86a36-141">All you need to do is configure the web app to work with a Git repository, download the web application from GitHub, and then upload it to Azure for the web app to host.</span></span>

1. <span data-ttu-id="86a36-142">Web uygulamasında tıklatın **dağıtım seçenekleri** > **Kaynağı Seç** > **yerel Git deposu**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="86a36-142">In the web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**, and then click **OK**.</span></span>

   ![Yerel Git deposu kullanmak için web uygulama dağıtımı yapılandırma](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. <span data-ttu-id="86a36-144">Tıklatın **dağıtım kimlik bilgileri**, bir kullanıcı adı ve parola Azure Git deponuza bağlamak ve ardından oluşturmak **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="86a36-144">Click **Deployment Credentials**, create a user name and password to use to connect to the Git repository in Azure, and then click **Save**.</span></span>

3. <span data-ttu-id="86a36-145">Tıklatın **genel bakış**ve değeri Not **Git kopyası URL'si**.</span><span class="sxs-lookup"><span data-stu-id="86a36-145">Click **Overview**, and note the value of **Git clone url**.</span></span>

   ![Web uygulamanızın Git kopya URL'si](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. <span data-ttu-id="86a36-147">Bir komut veya yerel bilgisayarınızda terminal penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="86a36-147">Open a command or terminal window on your local computer.</span></span>

5. <span data-ttu-id="86a36-148">Web uygulaması Github'dan indirin ve barındırmak için web uygulaması için Azure'a yükleyin.</span><span class="sxs-lookup"><span data-stu-id="86a36-148">Download the web app from GitHub, and upload it to Azure for the web app to host.</span></span> <span data-ttu-id="86a36-149">Bunu yapmak için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="86a36-149">To do so, run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > <span data-ttu-id="86a36-150">\<Git kopyalama URL'si\> bulunan Git deposu URL'si **genel bakış** sayfa web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="86a36-150">\<Git clone URL\> is the URL of the Git repository found on the **Overview** page of the web app.</span></span>

## <a name="open-the-web-app-to-see-real-time-temperature-and-humidity-data-from-your-iot-hub"></a><span data-ttu-id="86a36-151">IOT hub'ınızı gerçek zamanlı sıcaklık ve nem verileri görmek için web uygulamasını açın</span><span class="sxs-lookup"><span data-stu-id="86a36-151">Open the web app to see real-time temperature and humidity data from your IoT hub</span></span>

<span data-ttu-id="86a36-152">Üzerinde **genel bakış** sayfasında web uygulamanız web uygulaması açmak için URL'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="86a36-152">On the **Overview** page of your web app, click the URL to open the web app.</span></span>

![Web uygulamanızın URL'sini alma](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

<span data-ttu-id="86a36-154">IOT hub'ından gerçek zamanlı sıcaklık ve nem veri görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="86a36-154">You should see the real-time temperature and humidity data from your IoT hub.</span></span>

![Gerçek zamanlı sıcaklık ve nem gösteren web uygulama sayfası](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> <span data-ttu-id="86a36-156">Örnek uygulama Cihazınızda çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="86a36-156">Ensure the sample application is running on your device.</span></span> <span data-ttu-id="86a36-157">Boş bir grafik alırsınız istemiyorsanız, altında öğreticileri başvurabilirsiniz [Cihazınızı](iot-hub-raspberry-pi-kit-node-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="86a36-157">If not, you will get a blank chart, you can refer to the tutorials under [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="86a36-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="86a36-158">Next steps</span></span>
<span data-ttu-id="86a36-159">IOT hub'ından gerçek zamanlı algılayıcı verilerini görselleştirmek için web uygulamanızı başarıyla kullandıysanız.</span><span class="sxs-lookup"><span data-stu-id="86a36-159">You've successfully used your web app to visualize real-time sensor data from your IoT hub.</span></span>

<span data-ttu-id="86a36-160">Azure IOT Hub verilerini görselleştirmek için alternatif bir yol için bkz: [IOT hub'ınızı gerçek zamanlı algılayıcı verilerini görselleştirmek için kullanım Power BI](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="86a36-160">For an alternative way to visualize data from Azure IoT Hub, see [Use Power BI to visualize real-time sensor data from your IoT hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
