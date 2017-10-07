---
title: "Connect Arduino (C) tooAzure IOT - Ders 3: örneği çalıştırmak | Microsoft Docs"
description: "Dağıtma ve örnek uygulama tooAdafruit tooyour IOT hub'ı iletileri gönderir ve hello ışığı yanıp yumuşatma M0 WiFi çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT bulut hizmeti, arduino veri toocloud Gönder"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="c39df-104">Örnek uygulama toosend cihaz bulut iletilerini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="c39df-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="c39df-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="c39df-105">What you will do</span></span>
<span data-ttu-id="c39df-106">Bu makale toodeploy ve Adafruit yumuşatma M0 WiFi Arduino örnek bir uygulama çalıştırılmasında bu gönderdiği iletileri tooyour IOT hub'ın nasıl tahtası gösterir.</span><span class="sxs-lookup"><span data-stu-id="c39df-106">This article will show you how toodeploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages tooyour IoT hub.</span></span>

<span data-ttu-id="c39df-107">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="c39df-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c39df-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="c39df-108">What you will learn</span></span>
<span data-ttu-id="c39df-109">Nasıl toouse hello aracı toodeploy gulp ve Arduino Panonuzda hello örnek Arduino uygulamayı çalıştırın öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c39df-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c39df-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="c39df-110">What you need</span></span>
* <span data-ttu-id="c39df-111">Bu görev başlamadan önce başarılı bir şekilde tamamladınız gerekir [bir Azure işlevi uygulama ve bir depolama hesabı tooprocess deposu IOT hub ve iletileri oluşturmak][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="c39df-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="c39df-112">IOT hub ve cihaz bağlantı dizeleri alma</span><span class="sxs-lookup"><span data-stu-id="c39df-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="c39df-113">Merhaba cihaz bağlantı dizesi kullanılan tooconnect Arduino Panosu tooyour IOT hub'ınızın olan.</span><span class="sxs-lookup"><span data-stu-id="c39df-113">hello device connection string is used tooconnect your Arduino board tooyour IoT hub.</span></span> <span data-ttu-id="c39df-114">Merhaba IOT hub bağlantı dizesine kullanılan tooconnect, Arduino temsil eden IOT hub toohello cihaz kimliğinizi tahtası hello IOT hub ' dir.</span><span class="sxs-lookup"><span data-stu-id="c39df-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents your Arduino board in hello IoT hub.</span></span>

* <span data-ttu-id="c39df-115">Azure CLI komutu aşağıdaki hello çalıştırarak kaynak grubunuzdaki tüm IOT hub listesi:</span><span class="sxs-lookup"><span data-stu-id="c39df-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="c39df-116">Kullanım `iot-sample` hello değeri olarak `{resource group name}` hello değeri değiştirirseniz alamadık.</span><span class="sxs-lookup"><span data-stu-id="c39df-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="c39df-117">Azure CLI komutu aşağıdaki hello çalıştırarak Hello IOT hub bağlantı dizesine alın:</span><span class="sxs-lookup"><span data-stu-id="c39df-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="c39df-118">`{my hub name}`IOT hub'ınızı oluşturduğunuzda ve Arduino panonuzu kayıtlı belirttiğiniz hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="c39df-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="c39df-119">Merhaba cihaz bağlantı dizesi hello aşağıdaki komutu çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="c39df-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="c39df-120">Kullanım `mym0wifi` hello değeri olarak `{device id}` hello değeri değiştirirseniz alamadık.</span><span class="sxs-lookup"><span data-stu-id="c39df-120">Use `mym0wifi` as hello value of `{device id}` if you didn't change hello value.</span></span>
## <a name="configure-hello-device-connection"></a><span data-ttu-id="c39df-121">Merhaba aygıt bağlantısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="c39df-121">Configure hello device connection</span></span>
<span data-ttu-id="c39df-122">tooconfigure Merhaba cihaz bağlantısı, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c39df-122">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="c39df-123">Merhaba seri bağlantı noktası hello aygıt bulma CLI hello cihazının alın:</span><span class="sxs-lookup"><span data-stu-id="c39df-123">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="c39df-124">Toohello aşağıdadır benzer bir çıktı görmeniz ve hello usb Arduino panonuzu COM bağlantı noktasını Bul:</span><span class="sxs-lookup"><span data-stu-id="c39df-124">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![Aygıt Bulma][device-discovery]

2. <span data-ttu-id="c39df-126">Açık hello dosya `config.json` hello Ders klasörü ve COM bağlantı noktası numarası bulunan hello hello değerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c39df-126">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > <span data-ttu-id="c39df-128">Windows platformunda hello COM bağlantı noktası için hello biçimi olan `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="c39df-128">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="c39df-129">MacOS veya Ubuntu, ile başlayan `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="c39df-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="c39df-130">Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="c39df-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="c39df-131">Açık hello aygıt yapılandırma dosyası `config-arduino.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="c39df-131">Open hello device configuration file `config-arduino.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config arduino.json][config-arduino-json]

5. <span data-ttu-id="c39df-133">Merhaba değişikliklerini aşağıdaki hello olun `config-arduino.json` dosyası:</span><span class="sxs-lookup"><span data-stu-id="c39df-133">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   * <span data-ttu-id="c39df-134">Değiştir **[Wi-Fi SSID]** toohello Internet bağlı, Wi-Fi SSID ile.</span><span class="sxs-lookup"><span data-stu-id="c39df-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="c39df-135">Değiştir **[Wi-Fi parola]** Wi-Fi parolanızla.</span><span class="sxs-lookup"><span data-stu-id="c39df-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="c39df-136">Wi-Fi parola gerektirmez, hello dize kaldırın.</span><span class="sxs-lookup"><span data-stu-id="c39df-136">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="c39df-137">Değiştir **[IOT cihaz bağlantı dizesi]** hello ile `device connection string` , elde edilen.</span><span class="sxs-lookup"><span data-stu-id="c39df-137">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="c39df-138">Değiştir **[IOT hub bağlantı dizesine]** hello ile `iot hub connection string` , elde edilen.</span><span class="sxs-lookup"><span data-stu-id="c39df-138">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c39df-139">Gerekmeyen `azure_storage_connection_string` bu makalede.</span><span class="sxs-lookup"><span data-stu-id="c39df-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="c39df-140">Olduğu gibi tutun.</span><span class="sxs-lookup"><span data-stu-id="c39df-140">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="c39df-141">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c39df-141">Deploy and run hello sample application</span></span>
<span data-ttu-id="c39df-142">Dağıtma ve hello aşağıdaki komutu çalıştırarak Arduino Panonuzda hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c39df-142">Deploy and run hello sample application on your Arduino board by running hello following command:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="c39df-143">Merhaba varsayılan gulp görev çalıştırır `install-tools` ve `run` sırayla görevler.</span><span class="sxs-lookup"><span data-stu-id="c39df-143">hello default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="c39df-144">Olduğunda, [hello blink uygulama][deployed-the-blink-app], bu görevleri ayrı ayrı çalıştı.</span><span class="sxs-lookup"><span data-stu-id="c39df-144">When you [deployed hello blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="c39df-145">Merhaba örnek uygulaması çalıştığını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="c39df-145">Verify that hello sample application works</span></span>
<span data-ttu-id="c39df-146">Merhaba GPIO'yu #0 yerleşik LED her iki saniye yanıp sönen görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c39df-146">You should see hello GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="c39df-147">Merhaba ışığı yanıp her zaman, Merhaba örnek uygulaması bir ileti tooyour IOT hub'ı gönderir ve o hello iletisi tooyour IOT hub'ı başarıyla gönderildi doğrular.</span><span class="sxs-lookup"><span data-stu-id="c39df-147">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="c39df-148">Ayrıca, hello IOT hub tarafından alınan her ileti hello konsol penceresinde yazdırılır.</span><span class="sxs-lookup"><span data-stu-id="c39df-148">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="c39df-149">Merhaba örnek uygulaması, 20 ileti gönderdikten sonra otomatik olarak sona erer.</span><span class="sxs-lookup"><span data-stu-id="c39df-149">hello sample application terminates automatically after sending 20 messages.</span></span>

![Örnek uygulama ile gönderilen ve alınan iletileri][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="c39df-151">Özet</span><span class="sxs-lookup"><span data-stu-id="c39df-151">Summary</span></span>
<span data-ttu-id="c39df-152">Dağıtılan artık ve Arduino Panosu toosend cihaz bulut iletilerini tooyour IOT hub'ınızı üzerinde hello yeni blink örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c39df-152">You've deployed and run hello new blink sample application on your Arduino board toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="c39df-153">Toohello depolama hesabı yazıldığı şekilde şimdi iletilerinizi izleyin.</span><span class="sxs-lookup"><span data-stu-id="c39df-153">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c39df-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c39df-154">Next steps</span></span>
<span data-ttu-id="c39df-155">[İletileri okuma Azure Depolama'da kalıcı][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="c39df-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md