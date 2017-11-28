---
title: 'Connect Arduino (C) tooAzure IOT - Ders 4: Bulut cihaz | Microsoft Docs'
description: "Örnek bir uygulama Adafruit yumuşatma M0 WiFi ve izleyiciler gelen iletileri IOT hub'ından çalışır. Yeni bir gulp görevi, IOT hub tooblink hello LED iletileri tooAdafruit yumuşatma M0 WiFi gönderir."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Web, web üzerinden öncülük arduino denetim neden arduino denetimi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="21e9c-105">Örnek uygulama tooreceive bulut-cihaz iletilerini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="21e9c-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="21e9c-106">Bu makaledeki örnek bir uygulama Adafruit yumuşatma M0 WiFi Arduino Panonuzda dağıtın.</span><span class="sxs-lookup"><span data-stu-id="21e9c-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="21e9c-107">Merhaba örnek uygulaması IOT hub'ınızı gelen iletilere izler.</span><span class="sxs-lookup"><span data-stu-id="21e9c-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="21e9c-108">Ayrıca bir gulp görev, bilgisayar toosend iletileri tooyour Arduino Panosu üzerinde IOT hub'ından çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="21e9c-108">You also run a gulp task on your computer toosend messages tooyour Arduino board from your IoT hub.</span></span> <span data-ttu-id="21e9c-109">Merhaba örnek uygulaması Merhaba iletileri aldığında, hello ışığı yanıp.</span><span class="sxs-lookup"><span data-stu-id="21e9c-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="21e9c-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="21e9c-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="21e9c-111">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="21e9c-111">What you will do</span></span>
* <span data-ttu-id="21e9c-112">Merhaba örnek uygulama tooyour IOT hub bağlayın.</span><span class="sxs-lookup"><span data-stu-id="21e9c-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="21e9c-113">Dağıtma ve hello örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="21e9c-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="21e9c-114">İletiler, IOT hub tooyour Arduino Panosu tooblink hello LED gönderin.</span><span class="sxs-lookup"><span data-stu-id="21e9c-114">Send messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="21e9c-115">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="21e9c-115">What you will learn</span></span>
<span data-ttu-id="21e9c-116">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="21e9c-116">In this article, you will learn:</span></span>
* <span data-ttu-id="21e9c-117">Nasıl IOT hub'ından toomonitor gelen iletileri.</span><span class="sxs-lookup"><span data-stu-id="21e9c-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="21e9c-118">Nasıl toosend bulut-cihaz IOT hub tooyour Arduino Panosu iletileri.</span><span class="sxs-lookup"><span data-stu-id="21e9c-118">How toosend cloud-to-device messages from your IoT hub tooyour Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="21e9c-119">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="21e9c-119">What you need</span></span>
* <span data-ttu-id="21e9c-120">Arduino panonuzu ayarlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="21e9c-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="21e9c-121">tooset Arduino panonuzu yukarı nasıl görürüm toolearn [Cihazınızı yapılandırmak][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="21e9c-121">toolearn how tooset up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="21e9c-122">Azure aboneliğinizde oluşturduğunuz IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="21e9c-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="21e9c-123">toolearn nasıl toocreate IOT hub'ınızı bkz [Azure IOT Hub'ınızı oluşturması][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="21e9c-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="21e9c-124">Merhaba örnek uygulama tooyour IOT hub'ı Bağlan</span><span class="sxs-lookup"><span data-stu-id="21e9c-124">Connect hello sample application tooyour IoT hub</span></span>

1. <span data-ttu-id="21e9c-125">Merhaba depodaki klasöründe olduğunuzdan emin olun `iot-hub-c-feather-m0-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="21e9c-125">Make sure that you're in hello repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="21e9c-126">Merhaba aşağıdaki komutları çalıştırarak örnek uygulama Visual Studio Code açık hello:</span><span class="sxs-lookup"><span data-stu-id="21e9c-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="21e9c-127">Bildirim hello `app.ino` hello dosyasında `app` alt klasörü.</span><span class="sxs-lookup"><span data-stu-id="21e9c-127">Notice hello `app.ino` file in hello `app` subfolder.</span></span> <span data-ttu-id="21e9c-128">Merhaba `app.ino` hello kod toomonitor gelen iletilere hello IOT hub'ı içeren hello anahtar kaynak dosyası bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="21e9c-128">hello `app.ino` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="21e9c-129">Merhaba `blinkLED` işlevi yanıp hello LED.</span><span class="sxs-lookup"><span data-stu-id="21e9c-129">hello `blinkLED` function blinks hello LED.</span></span>

   ![Depodaki yapısında Merhaba örnek uygulaması][repo-structure]

2. <span data-ttu-id="21e9c-131">Merhaba seri bağlantı noktası hello aygıt bulma CLI hello cihazının alın:</span><span class="sxs-lookup"><span data-stu-id="21e9c-131">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="21e9c-132">Toohello aşağıdadır benzer bir çıktı görmeniz ve hello usb Arduino panonuzu COM bağlantı noktasını Bul:</span><span class="sxs-lookup"><span data-stu-id="21e9c-132">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![Aygıt Bulma][device-discovery]

3. <span data-ttu-id="21e9c-134">Açık hello dosya `config.json` hello Ders klasöründe ve COM bağlantı noktası numarası bulunan hello giriş hello değeri:</span><span class="sxs-lookup"><span data-stu-id="21e9c-134">Open hello file `config.json` in hello lesson folder and input hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > <span data-ttu-id="21e9c-136">Windows platformunda hello COM bağlantı noktası için hello biçimi olan `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="21e9c-136">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="21e9c-137">MacOS veya Ubuntu, ile başlar `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="21e9c-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="21e9c-138">Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="21e9c-138">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="21e9c-139">Merhaba değişikliklerini aşağıdaki hello olun `config-arduino.json` dosyası:</span><span class="sxs-lookup"><span data-stu-id="21e9c-139">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   <span data-ttu-id="21e9c-140">Merhaba adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı] [ create-an-azure-function-app-and-storage-account] dağıtma hello adım toohello görev atlayabilirsiniz bu bilgisayarda tüm hello yapılandırmaları, devralınan ve Merhaba örnek uygulama çalıştırılıyor.</span><span class="sxs-lookup"><span data-stu-id="21e9c-140">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="21e9c-141">Merhaba adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı] [ create-an-azure-function-app-and-storage-account] başka bir bilgisayara ihtiyacınız hello tooreplace hello yer tutucuları `config-arduino.json` dosya.</span><span class="sxs-lookup"><span data-stu-id="21e9c-141">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-arduino.json` file.</span></span> <span data-ttu-id="21e9c-142">Merhaba `config-arduino.json` giriş klasörü hello alt klasöründe bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="21e9c-142">hello `config-arduino.json` file is in hello subfolder of your home folder.</span></span>

   ![Merhaba config arduino.json dosyasının içeriği][config-arduino-json]

   * <span data-ttu-id="21e9c-144">Değiştir **[Wi-Fi SSID]** toohello Internet bağlı, Wi-Fi SSID ile.</span><span class="sxs-lookup"><span data-stu-id="21e9c-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="21e9c-145">Değiştir **[Wi-Fi parola]** Wi-Fi parolanızla.</span><span class="sxs-lookup"><span data-stu-id="21e9c-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="21e9c-146">Wi-Fi parola gerektirmez, hello dize kaldırın.</span><span class="sxs-lookup"><span data-stu-id="21e9c-146">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="21e9c-147">Değiştir **[IOT cihaz bağlantı dizesi]** hello cihaz bağlantı dizesiyle hello çalıştırarak aldığınız `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` komutu.</span><span class="sxs-lookup"><span data-stu-id="21e9c-147">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="21e9c-148">Değiştir **[IOT hub bağlantı dizesine]** hello hello çalıştırarak aldığınız IOT hub bağlantı dizesine sahip `az iot hub show-connection-string --name {my hub name}` komutu.</span><span class="sxs-lookup"><span data-stu-id="21e9c-148">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="21e9c-149">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="21e9c-149">Deploy and run hello sample application</span></span>
<span data-ttu-id="21e9c-150">Dağıtma ve hello aşağıdaki komutları çalıştırarak Arduino Panonuzda hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="21e9c-150">Deploy and run hello sample application on your Arduino board by running hello following commands:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="21e9c-151">Merhaba gulp komutu hello örnek uygulama tooyour Arduino Panosu dağıtır.</span><span class="sxs-lookup"><span data-stu-id="21e9c-151">hello gulp command deploys hello sample application tooyour Arduino board.</span></span> <span data-ttu-id="21e9c-152">Ardından, onu Merhaba uygulaması Arduino panonuzu ve ana bilgisayarınızda ayrı bir görev bilgisayar toosend 20 blink iletileri tooyour Arduino Panosu IOT hub'ından çalışır.</span><span class="sxs-lookup"><span data-stu-id="21e9c-152">Then, it runs hello application on your Arduino board and a separate task on your host computer toosend 20 blink messages tooyour Arduino board from your IoT hub.</span></span>

<span data-ttu-id="21e9c-153">Merhaba örnek uygulaması çalıştıktan sonra IOT hub'dan toomessages dinlemeyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="21e9c-153">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="21e9c-154">Bu sırada, hello gulp görev, IOT hub tooyour Arduino Panosu birkaç "blink" iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="21e9c-154">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="21e9c-155">Pano hello her blink iletiyi alır için hello örnek uygulama hello çağırır `blinkLED` işlevi tooblink hello LED.</span><span class="sxs-lookup"><span data-stu-id="21e9c-155">For each blink message that hello board receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="21e9c-156">Merhaba LED görmelisiniz hello gulp görev, IOT hub tooyour Arduino Panosu 20 ileti gönderir gibi her iki saniye blink.</span><span class="sxs-lookup"><span data-stu-id="21e9c-156">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="21e9c-157">Merhaba son hello uygulamanın çalışmasını durdurur "Durdur" bir ileti biridir.</span><span class="sxs-lookup"><span data-stu-id="21e9c-157">hello last one is a "stop" message that stops hello application from running.</span></span>

![Örnek uygulama ile komut gulp ve iletileri blink][sample-application]

## <a name="summary"></a><span data-ttu-id="21e9c-159">Özet</span><span class="sxs-lookup"><span data-stu-id="21e9c-159">Summary</span></span>
<span data-ttu-id="21e9c-160">İleti, IOT hub tooyour Arduino Panosu tooblink hello LED başarıyla gönderdik.</span><span class="sxs-lookup"><span data-stu-id="21e9c-160">You’ve successfully sent messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="21e9c-161">Merhaba sonraki görev, isteğe bağlı: hello açma ve kapatma hello LED davranışını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="21e9c-161">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21e9c-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="21e9c-162">Next steps</span></span>
<span data-ttu-id="21e9c-163">[Merhaba açma ve kapatma hello LED davranışını değiştirme][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="21e9c-163">[Change hello on and off behavior of hello LED][change-the-on-and-off-led-behavior]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md