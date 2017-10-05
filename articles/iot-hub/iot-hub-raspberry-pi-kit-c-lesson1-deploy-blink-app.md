---
title: "Azure IOT - Ders 1 Böğürtlenli Pi (C) bağlanın: uygulama dağıtma | Microsoft Docs"
description: "Örnek C uygulama github'dan kopyalayın ve bu uygulamayı Raspberry Pi 3 panonuzu dağıtmak için gulp. Bu örnek uygulama panosuna her iki saniye bağlı ışığı yanıp."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Böğürtlenli pi öncülük blink, blink neden Böğürtlenli pi ile"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f601d1e1-2bc3-4cc5-a6b1-0467e5304dcf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2ae409c6a39521711777ec329d2507a2801cc985
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="5bdeb-105">Blink uygulaması oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="5bdeb-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="5bdeb-106">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="5bdeb-106">What you will do</span></span>
<span data-ttu-id="5bdeb-107">Örnek C uygulama github'dan kopyalama ve Raspberry Pi 3 örnek uygulamayı dağıtmak için gulp aracını kullanın.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Raspberry Pi 3.</span></span> <span data-ttu-id="5bdeb-108">Örnek uygulama panosuna her iki saniye bağlı ışığı yanıp.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="5bdeb-109">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5bdeb-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5bdeb-110">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="5bdeb-110">What you will learn</span></span>
<span data-ttu-id="5bdeb-111">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="5bdeb-111">In this article, you will learn:</span></span>

* <span data-ttu-id="5bdeb-112">Nasıl kullanılacağını `device-discover-cli` PI hakkında ağ bilgilerini almak için aracı.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-112">How to use the `device-discover-cli` tool to retrieve networking information about Pi.</span></span>
* <span data-ttu-id="5bdeb-113">Nasıl dağıtmak ve Pi üzerinde örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-113">How to deploy and run the sample application on Pi.</span></span>
* <span data-ttu-id="5bdeb-114">Dağıtma ve hata ayıklama uygulamaları uzaktan Pi üzerinde çalışan.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-114">How to deploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5bdeb-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="5bdeb-115">What you need</span></span>
<span data-ttu-id="5bdeb-116">Aşağıdaki işlemleri başarıyla tamamlandı gerekir:</span><span class="sxs-lookup"><span data-stu-id="5bdeb-116">You must have successfully completed the following operations:</span></span>

* [<span data-ttu-id="5bdeb-117">Cihazınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5bdeb-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [<span data-ttu-id="5bdeb-118">Araçları edinin</span><span class="sxs-lookup"><span data-stu-id="5bdeb-118">Get the tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-the-ip-address-and-host-name-of-pi"></a><span data-ttu-id="5bdeb-119">Pi IP adresi ve ana bilgisayar adını alın</span><span class="sxs-lookup"><span data-stu-id="5bdeb-119">Obtain the IP address and host name of Pi</span></span>
<span data-ttu-id="5bdeb-120">Windows veya terminal macOS veya Ubuntu bir komut istemi açın ve aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5bdeb-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run the following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="5bdeb-121">Aşağıdakine benzer bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="5bdeb-121">You should see an output that is similar to the following:</span></span>

![Aygıt Bulma](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="5bdeb-123">Not edin `IP address` ve `hostname` pi'nin.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-123">Take note of the `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="5bdeb-124">Bu bilgiler bu makalenin sonraki bölümlerinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="5bdeb-125">Pi bilgisayarınızın aynı ağa bağlı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-125">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="5bdeb-126">Örneğin, pi kablolu bir ağa bağlıyken, bilgisayarınızın kablosuz bir ağa bağlıysa, IP adresi devdisco çıkışı göremeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-126">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="5bdeb-127">Örnek uygulamayı Aç</span><span class="sxs-lookup"><span data-stu-id="5bdeb-127">Open the sample application</span></span>
<span data-ttu-id="5bdeb-128">Örnek uygulamayı açmak için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="5bdeb-128">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="5bdeb-129">Aşağıdaki komutu çalıştırarak github'dan örnek depoyu kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="5bdeb-129">Clone the sample repository from GitHub by running the following command:</span></span>
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. <span data-ttu-id="5bdeb-130">Örnek uygulama, aşağıdaki komutları çalıştırarak Visual Studio kodda açın:</span><span class="sxs-lookup"><span data-stu-id="5bdeb-130">Open the sample application in Visual Studio Code by running the following commands:</span></span>
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Depodaki yapısı](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

<span data-ttu-id="5bdeb-132">`main.c` Dosyasını `app` alt denetim LED koda içeren anahtar kaynak dosyası klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-132">The `main.c` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="5bdeb-133">Uygulama bağımlılıkları yükler</span><span class="sxs-lookup"><span data-stu-id="5bdeb-133">Install application dependencies</span></span>
<span data-ttu-id="5bdeb-134">Kitaplıklar ve örnek uygulama için aşağıdaki komutu çalıştırarak gereken diğer modüller yükleyin:</span><span class="sxs-lookup"><span data-stu-id="5bdeb-134">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="5bdeb-135">Aygıt bağlantısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5bdeb-135">Configure the device connection</span></span>
<span data-ttu-id="5bdeb-136">Aygıt bağlantısını yapılandırmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="5bdeb-136">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="5bdeb-137">Aşağıdaki komutu çalıştırarak aygıt yapılandırma dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="5bdeb-137">Generate the device configuration file by running the following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="5bdeb-138">Yapılandırma dosyası `config-raspberrypi.json` Pi oturum açmak için kullandığınız kullanıcı kimlik bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-138">The configuration file `config-raspberrypi.json` contains the user credentials you use to log in to Pi.</span></span> <span data-ttu-id="5bdeb-139">Kullanıcı kimlik bilgilerini sızıntısını önlemek için yapılandırma dosyası alt klasöründe oluşturulur `.iot-hub-getting-started` bilgisayarınızda giriş klasörünün.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-139">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="5bdeb-140">Aygıt yapılandırma dosyası, aşağıdaki komutu çalıştırarak Visual Studio kodda açın:</span><span class="sxs-lookup"><span data-stu-id="5bdeb-140">Open the device configuration file in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. <span data-ttu-id="5bdeb-141">Yer tutucu Değiştir `[device hostname or IP address]` IP adresini ya da daha önce alındı ana bilgisayar adına sahip "Pi IP adresi ve ana bilgisayar adını alın."</span><span class="sxs-lookup"><span data-stu-id="5bdeb-141">Replace the placeholder `[device hostname or IP address]` with the IP address or the host name that you got previously in "Obtain the IP address and host name of Pi."</span></span>
   
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="5bdeb-143">Raspberry Pi'yi bağlanırken, kullanıcı adı ve parola yerine SSH anahtarı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-143">You can use SSH key instead of user name and password when connecting to Raspberry Pi.</span></span> <span data-ttu-id="5bdeb-144">Bunu kullanarak anahtar oluşturmak için olacaktır yapmak için **ssh-keygen** ve **ssh-kopya-ID pi @\<aygıt adresi\>**.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-144">In order to do this you will have to generate the key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="5bdeb-145">Bu komutlar Windows üzerinde kullanılabilir olan **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="5bdeb-146">MacOS üzerinde çalıştırmanız gerekir. **brew yükleme ssh-kopya-ID**.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-146">On MacOS you need to run **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="5bdeb-147">Başarılı bir şekilde anahtar Raspberry Pi'yi dosyalarını karşıya yükledikten sonra yerine **device_password** ile **device_key_path** özelliğinde **config raspberrypi.json**.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-147">After successfully uploading the key to the Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="5bdeb-148">Güncelleştirilmiş satırları aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="5bdeb-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="5bdeb-149">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="5bdeb-149">Congratulations!</span></span> <span data-ttu-id="5bdeb-150">Pi ilk örnek uygulama başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-150">You've successfully created the first sample application for Pi.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="5bdeb-151">Dağıtma ve örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5bdeb-151">Deploy and run the sample application</span></span>
### <a name="install-the-azure-iot-hub-sdk-on-pi"></a><span data-ttu-id="5bdeb-152">Pi üzerinde Azure IOT Hub SDK'sını yükleyin</span><span class="sxs-lookup"><span data-stu-id="5bdeb-152">Install the Azure IoT Hub SDK on Pi</span></span>
<span data-ttu-id="5bdeb-153">Azure IOT Hub SDK'sı, aşağıdaki komutu çalıştırarak üzerinde Pi yükleyin:</span><span class="sxs-lookup"><span data-stu-id="5bdeb-153">Install the Azure IoT Hub SDK on Pi by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="5bdeb-154">Bu görev, ilk çalıştırdığınızda tamamlanması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-154">This task might take a few minutes to complete the first time you run it.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="5bdeb-155">Dağıtma ve örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5bdeb-155">Deploy and run the sample app</span></span>
<span data-ttu-id="5bdeb-156">Dağıtma ve aşağıdaki komutu çalıştırarak örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5bdeb-156">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="5bdeb-157">Uygulama çalıştığını doğrulama</span><span class="sxs-lookup"><span data-stu-id="5bdeb-157">Verify the app works</span></span>
<span data-ttu-id="5bdeb-158">Örnek uygulama için 20 kez ışığı yanıp sonra otomatik olarak sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-158">The sample application terminates automatically after the LED blinks for 20 times.</span></span> <span data-ttu-id="5bdeb-159">IŞIĞI yanıp sönen görmüyorsanız bkz [sorun giderme kılavuzu](iot-hub-raspberry-pi-kit-c-troubleshooting.md) yaygın sorunların çözümleri için.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-159">If you don’t see the LED blinking, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>
<span data-ttu-id="5bdeb-160">![IŞIĞI yanıp sönen](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="5bdeb-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="5bdeb-161">Özet</span><span class="sxs-lookup"><span data-stu-id="5bdeb-161">Summary</span></span>
<span data-ttu-id="5bdeb-162">Pi ile çalışmak için gerekli araçları yüklü ve bir örnek uygulama ile Pi LED blink dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-162">You've installed the required tools to work with Pi and deployed a sample application to Pi to blink the LED.</span></span> <span data-ttu-id="5bdeb-163">Şimdi oluşturmanıza, dağıtmanıza ve Pi ileti gönderme ve alma için Azure IOT hub'a bağlanan başka bir örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-163">You can now create, deploy, and run another sample application that connects Pi to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5bdeb-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5bdeb-164">Next steps</span></span>
[<span data-ttu-id="5bdeb-165">Azure Araçları edinin</span><span class="sxs-lookup"><span data-stu-id="5bdeb-165">Get Azure tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)

