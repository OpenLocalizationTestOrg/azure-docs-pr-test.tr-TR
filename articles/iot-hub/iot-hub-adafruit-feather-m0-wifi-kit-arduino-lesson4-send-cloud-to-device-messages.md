---
title: "Azure IOT - Ders 4 Arduino (C) bağlanın: Bulut cihaz | Microsoft Docs"
description: "Örnek bir uygulama Adafruit yumuşatma M0 WiFi ve izleyiciler gelen iletileri IOT hub'ından çalışır. Yeni bir gulp görev, IOT hub ' LED blink Adafruit yumuşatma M0 WiFi iletileri gönderir."
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
ms.openlocfilehash: b4f4c1d86b10b64c104ac812d1f650d723322be8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="36052-105">Bulut cihaz iletileri almak için bir örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="36052-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="36052-106">Bu makaledeki örnek bir uygulama Adafruit yumuşatma M0 WiFi Arduino Panonuzda dağıtın.</span><span class="sxs-lookup"><span data-stu-id="36052-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="36052-107">Örnek uygulama IOT hub'ınızı gelen iletilere izler.</span><span class="sxs-lookup"><span data-stu-id="36052-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="36052-108">Ayrıca, IOT hub'ından Arduino panonuzu iletileri göndermek için bilgisayarınızda gulp görevini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="36052-108">You also run a gulp task on your computer to send messages to your Arduino board from your IoT hub.</span></span> <span data-ttu-id="36052-109">Örnek uygulama iletileri aldığında ışığı yanıp.</span><span class="sxs-lookup"><span data-stu-id="36052-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="36052-110">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="36052-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="36052-111">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="36052-111">What you will do</span></span>
* <span data-ttu-id="36052-112">Örnek uygulama IOT hub'ınıza bağlanın.</span><span class="sxs-lookup"><span data-stu-id="36052-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="36052-113">Dağıtma ve örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="36052-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="36052-114">İletileri IOT hub'ından LED blink için Arduino panonuzu gönderin.</span><span class="sxs-lookup"><span data-stu-id="36052-114">Send messages from your IoT hub to your Arduino board to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="36052-115">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="36052-115">What you will learn</span></span>
<span data-ttu-id="36052-116">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="36052-116">In this article, you will learn:</span></span>
* <span data-ttu-id="36052-117">IOT hub'ınızı gelen iletilere izlemek nasıl.</span><span class="sxs-lookup"><span data-stu-id="36052-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="36052-118">Bulut cihaz IOT hub'ından Arduino panonuzu göndermek nasıl.</span><span class="sxs-lookup"><span data-stu-id="36052-118">How to send cloud-to-device messages from your IoT hub to your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="36052-119">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="36052-119">What you need</span></span>
* <span data-ttu-id="36052-120">Arduino panonuzu ayarlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="36052-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="36052-121">Arduino panonuzu ayarlama hakkında bilgi edinmek için bkz: [Cihazınızı yapılandırmak][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="36052-121">To learn how to set up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="36052-122">Azure aboneliğinizde oluşturduğunuz IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="36052-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="36052-123">IOT hub'ınızı oluşturmayı öğrenmek için bkz: [Azure IOT Hub'ınızı oluşturması][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="36052-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="36052-124">Örnek uygulama IOT hub'ınıza bağlanın</span><span class="sxs-lookup"><span data-stu-id="36052-124">Connect the sample application to your IoT hub</span></span>

1. <span data-ttu-id="36052-125">Depodaki klasöründe olduğunuzdan emin olun `iot-hub-c-feather-m0-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="36052-125">Make sure that you're in the repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="36052-126">Örnek uygulama, aşağıdaki komutları çalıştırarak Visual Studio kodda açın:</span><span class="sxs-lookup"><span data-stu-id="36052-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="36052-127">Bildirim `app.ino` dosyasını `app` alt klasörü.</span><span class="sxs-lookup"><span data-stu-id="36052-127">Notice the `app.ino` file in the `app` subfolder.</span></span> <span data-ttu-id="36052-128">`app.ino` IOT hub'ından gelen iletileri izlemek için kod içeren anahtar kaynak dosyası bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="36052-128">The `app.ino` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="36052-129">`blinkLED` İşlevi yanıp LED.</span><span class="sxs-lookup"><span data-stu-id="36052-129">The `blinkLED` function blinks the LED.</span></span>

   ![Depodaki yapısında örnek uygulama][repo-structure]

2. <span data-ttu-id="36052-131">Aygıtın aygıt bulma CLI ile seri bağlantı noktası alın:</span><span class="sxs-lookup"><span data-stu-id="36052-131">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="36052-132">Aşağıdakine benzer bir çıktı görmeniz ve usb Arduino panonuzu COM bağlantı noktasını Bul:</span><span class="sxs-lookup"><span data-stu-id="36052-132">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![Aygıt Bulma][device-discovery]

3. <span data-ttu-id="36052-134">Dosyayı açmak `config.json` Ders klasöründe ve giriş bulunan COM bağlantı noktası numarası değeri:</span><span class="sxs-lookup"><span data-stu-id="36052-134">Open the file `config.json` in the lesson folder and input the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > <span data-ttu-id="36052-136">COM bağlantı noktası, Windows platformunda için biçimi olan `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="36052-136">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="36052-137">MacOS veya Ubuntu, ile başlar `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="36052-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="36052-138">Yapılandırma dosyası, aşağıdaki komutları çalıştırarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="36052-138">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="36052-139">İçinde aşağıdaki değişiklikleri yapın `config-arduino.json` dosyası:</span><span class="sxs-lookup"><span data-stu-id="36052-139">Make the following replacements in the `config-arduino.json` file:</span></span>

   <span data-ttu-id="36052-140">' Ndaki adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı] [ create-an-azure-function-app-and-storage-account] dağıtma ve örnek uygulama çalıştırılıyor görev adımı atlayabilirsiniz bu bilgisayarda tüm yapılandırmaları, devralınır.</span><span class="sxs-lookup"><span data-stu-id="36052-140">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="36052-141">' Ndaki adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı] [ create-an-azure-function-app-and-storage-account] yer tutucuları değiştirmek gereken başka bir bilgisayara `config-arduino.json` dosya.</span><span class="sxs-lookup"><span data-stu-id="36052-141">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-arduino.json` file.</span></span> <span data-ttu-id="36052-142">`config-arduino.json` Giriş klasörü alt klasöründe bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="36052-142">The `config-arduino.json` file is in the subfolder of your home folder.</span></span>

   ![Config arduino.json dosyasının içeriği][config-arduino-json]

   * <span data-ttu-id="36052-144">Değiştir **[Wi-Fi SSID]** Internet'e bağlı, Wi-Fi SSID ile.</span><span class="sxs-lookup"><span data-stu-id="36052-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="36052-145">Değiştir **[Wi-Fi parola]** Wi-Fi parolanızla.</span><span class="sxs-lookup"><span data-stu-id="36052-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="36052-146">Wi-Fi parola gerektirmez, dize kaldırın.</span><span class="sxs-lookup"><span data-stu-id="36052-146">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="36052-147">Değiştir **[IOT cihaz bağlantı dizesi]** çalıştırarak aldığınız cihaz bağlantı dizesiyle `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` komutu.</span><span class="sxs-lookup"><span data-stu-id="36052-147">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="36052-148">Değiştir **[IOT hub bağlantı dizesine]** çalıştırarak aldığınız IOT hub bağlantı dizesine sahip `az iot hub show-connection-string --name {my hub name}` komutu.</span><span class="sxs-lookup"><span data-stu-id="36052-148">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="36052-149">Dağıtma ve örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="36052-149">Deploy and run the sample application</span></span>
<span data-ttu-id="36052-150">Dağıtma ve aşağıdaki komutları çalıştırarak Arduino Panonuzda örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="36052-150">Deploy and run the sample application on your Arduino board by running the following commands:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="36052-151">Gulp komutu Arduino panonuzu örnek uygulamayı dağıtır.</span><span class="sxs-lookup"><span data-stu-id="36052-151">The gulp command deploys the sample application to your Arduino board.</span></span> <span data-ttu-id="36052-152">Ardından, Arduino panonuzu ve ana bilgisayarınızda IOT hub'ından Arduino panonuzu 20 blink iletileri göndermek için ayrı bir görev uygulama çalışır.</span><span class="sxs-lookup"><span data-stu-id="36052-152">Then, it runs the application on your Arduino board and a separate task on your host computer to send 20 blink messages to your Arduino board from your IoT hub.</span></span>

<span data-ttu-id="36052-153">Örnek uygulama çalıştıktan sonra IOT hub'ından iletileri dinlemeyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="36052-153">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="36052-154">Bu sırada, gulp görev Arduino panonuzu IOT hub'ından birkaç "blink" iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="36052-154">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="36052-155">Pano alan her blink ileti için örnek uygulama çağırır `blinkLED` LED blink işlevi.</span><span class="sxs-lookup"><span data-stu-id="36052-155">For each blink message that the board receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="36052-156">Gulp görev 20 iletileri IOT hub'ından Arduino panonuzu gönderir, her iki saniye LED blink görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="36052-156">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="36052-157">Bir uygulamanın çalışmasını durduran bir "Durdur" bir iletidir.</span><span class="sxs-lookup"><span data-stu-id="36052-157">The last one is a "stop" message that stops the application from running.</span></span>

![Örnek uygulama ile komut gulp ve iletileri blink][sample-application]

## <a name="summary"></a><span data-ttu-id="36052-159">Özet</span><span class="sxs-lookup"><span data-stu-id="36052-159">Summary</span></span>
<span data-ttu-id="36052-160">IOT hub'ından LED blink için Arduino panonuz başarıyla iletileri gönderdik.</span><span class="sxs-lookup"><span data-stu-id="36052-160">You’ve successfully sent messages from your IoT hub to your Arduino board to blink the LED.</span></span> <span data-ttu-id="36052-161">Sonraki görev isteğe bağlıdır: açık ve kapalı LED davranışını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="36052-161">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36052-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="36052-162">Next steps</span></span>
<span data-ttu-id="36052-163">[Açık ve kapalı LED davranışını değiştirme][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="36052-163">[Change the on and off behavior of the LED][change-the-on-and-off-led-behavior]</span></span>


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