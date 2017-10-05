---
featureFlags: usabilla
title: "Azure IOT - Ders 1 Böğürtlenli Pi (düğüm) bağlanma: uygulama dağıtma | Microsoft Docs"
description: "Github'dan örnek Node.js uygulaması kopyalayın ve bu uygulamayı Raspberry Pi 3 panonuzu dağıtmak için gulp. Bu örnek uygulama panosuna her iki saniye bağlı ışığı yanıp."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Böğürtlenli pi öncülük blink, blink neden Böğürtlenli pi ile"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: a5a03a57-fe86-416f-90ff-6eca17775842
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8b73000c166950172c07b8e188025dc9da5bc011
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="64143-105">Blink uygulaması oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="64143-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="64143-106">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="64143-106">What you will do</span></span>
<span data-ttu-id="64143-107">Örnek Node.js uygulaması github'dan kopyalama ve Raspberry Pi 3 örnek uygulamayı dağıtmak için gulp aracını kullanın.</span><span class="sxs-lookup"><span data-stu-id="64143-107">Clone the sample Node.js application from GitHub and use the gulp tool to deploy the sample application to your Raspberry Pi 3.</span></span> <span data-ttu-id="64143-108">Örnek uygulama panosuna her iki saniye bağlı ışığı yanıp.</span><span class="sxs-lookup"><span data-stu-id="64143-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="64143-109">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="64143-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="64143-110">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="64143-110">What you will learn</span></span>
<span data-ttu-id="64143-111">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="64143-111">In this article, you will learn:</span></span>

* <span data-ttu-id="64143-112">Nasıl kullanılacağını `device-discover-cli` PI hakkında ağ bilgilerini almak için aracı.</span><span class="sxs-lookup"><span data-stu-id="64143-112">How to use the `device-discover-cli` tool to retrieve networking information about Pi.</span></span>
* <span data-ttu-id="64143-113">Nasıl dağıtmak ve Pi üzerinde örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="64143-113">How to deploy and run the sample application on Pi.</span></span>
* <span data-ttu-id="64143-114">Dağıtma ve hata ayıklama uygulamaları uzaktan Pi üzerinde çalışan.</span><span class="sxs-lookup"><span data-stu-id="64143-114">How to deploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="64143-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="64143-115">What you need</span></span>
<span data-ttu-id="64143-116">Aşağıdaki işlemleri başarıyla tamamlandı gerekir:</span><span class="sxs-lookup"><span data-stu-id="64143-116">You must have successfully completed the following operations:</span></span>

* [<span data-ttu-id="64143-117">Cihazınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="64143-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)
* [<span data-ttu-id="64143-118">Araçları edinin</span><span class="sxs-lookup"><span data-stu-id="64143-118">Get the tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

## <a name="obtain-the-ip-address-and-host-name-of-pi"></a><span data-ttu-id="64143-119">Pi IP adresi ve ana bilgisayar adını alın</span><span class="sxs-lookup"><span data-stu-id="64143-119">Obtain the IP address and host name of Pi</span></span>
<span data-ttu-id="64143-120">Windows veya terminal macOS veya Ubuntu bir komut istemi açın ve aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="64143-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run the following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="64143-121">Aşağıdakine benzer bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="64143-121">You should see an output that is similar to the following:</span></span>

![Aygıt Bulma](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="64143-123">Not edin `IP address` ve `hostname` pi'nin.</span><span class="sxs-lookup"><span data-stu-id="64143-123">Take note of the `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="64143-124">Bu bilgiler bu makalenin sonraki bölümlerinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="64143-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="64143-125">Pi bilgisayarınızın aynı ağa bağlı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="64143-125">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="64143-126">Örneğin, pi kablolu bir ağa bağlıyken, bilgisayarınızın kablosuz bir ağa bağlıysa, IP adresi devdisco çıkışı göremeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64143-126">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="64143-127">Örnek uygulamayı kopyalama</span><span class="sxs-lookup"><span data-stu-id="64143-127">Clone the sample application</span></span>
<span data-ttu-id="64143-128">Örnek kod açmak için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="64143-128">To open the sample code, follow these steps:</span></span>

1. <span data-ttu-id="64143-129">Aşağıdaki komutu çalıştırarak github'dan örnek depoyu kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="64143-129">Clone the sample repository from GitHub by running the following command:</span></span>
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started.git
   ```
2. <span data-ttu-id="64143-130">Örnek uygulama, aşağıdaki komutları çalıştırarak Visual Studio kodda açın:</span><span class="sxs-lookup"><span data-stu-id="64143-130">Open the sample application in Visual Studio Code by running the following commands:</span></span>
   
   ```bash
   cd iot-hub-node-raspberrypi-getting-started
   cd Lesson1
   code .
   ```

![Depodaki yapısı](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-mac.png)

<span data-ttu-id="64143-132">`app.js` Dosyasını `app` alt denetim LED koda içeren anahtar kaynak dosyası klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="64143-132">The `app.js` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="64143-133">Uygulama bağımlılıkları yükler</span><span class="sxs-lookup"><span data-stu-id="64143-133">Install application dependencies</span></span>
<span data-ttu-id="64143-134">Kitaplıklar ve örnek uygulama için aşağıdaki komutu çalıştırarak gereken diğer modüller yükleyin:</span><span class="sxs-lookup"><span data-stu-id="64143-134">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="64143-135">Aygıt bağlantısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="64143-135">Configure the device connection</span></span>
<span data-ttu-id="64143-136">Aygıt bağlantısını yapılandırmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="64143-136">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="64143-137">Aşağıdaki komutu çalıştırarak aygıt yapılandırma dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="64143-137">Generate the device configuration file by running the following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="64143-138">Yapılandırma dosyası `config-raspberrypi.json` Pi oturum açmak için kullandığınız kullanıcı kimlik bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="64143-138">The configuration file `config-raspberrypi.json` contains the user credentials you use to log in to Pi.</span></span> <span data-ttu-id="64143-139">Kullanıcı kimlik bilgilerini sızıntısını önlemek için yapılandırma dosyası alt klasöründe oluşturulur `.iot-hub-getting-started` bilgisayarınızda giriş klasörünün.</span><span class="sxs-lookup"><span data-stu-id="64143-139">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="64143-140">Aygıt yapılandırma dosyası, aşağıdaki komutu çalıştırarak Visual Studio kodda açın:</span><span class="sxs-lookup"><span data-stu-id="64143-140">Open the device configuration file in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
3. <span data-ttu-id="64143-141">Yer tutucu Değiştir `[device hostname or IP address]` IP adresini ya da daha önce alındı ana bilgisayar adına sahip "Pi IP adresi ve ana bilgisayar adını alın."</span><span class="sxs-lookup"><span data-stu-id="64143-141">Replace the placeholder `[device hostname or IP address]` with the IP address or the host name that you got previously in "Obtain the IP address and host name of Pi."</span></span>
   
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="64143-143">Raspberry Pi'yi bağlanırken, kullanıcı adı ve parola yerine SSH anahtarı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64143-143">You can use SSH key instead of user name and password when connecting to Raspberry Pi.</span></span> <span data-ttu-id="64143-144">Bunu kullanarak anahtar oluşturmak için olacaktır yapmak için **ssh-keygen** ve **ssh-kopya-ID pi @\<aygıt adresi\>**.</span><span class="sxs-lookup"><span data-stu-id="64143-144">In order to do this you will have to generate the key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="64143-145">Bu komutlar Windows üzerinde kullanılabilir olan **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="64143-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="64143-146">MacOS üzerinde çalıştırmanız gerekir. **brew yükleme ssh-kopya-ID**.</span><span class="sxs-lookup"><span data-stu-id="64143-146">On MacOS you need to run **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="64143-147">Başarılı bir şekilde anahtar Raspberry Pi'yi dosyalarını karşıya yükledikten sonra yerine **device_password** ile **device_key_path** özelliğinde **config raspberrypi.json**.</span><span class="sxs-lookup"><span data-stu-id="64143-147">After successfully uploading the key to the Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="64143-148">Güncelleştirilmiş satırları aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="64143-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="64143-149">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="64143-149">Congratulations!</span></span> <span data-ttu-id="64143-150">Pi ilk örnek uygulama başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="64143-150">You've successfully created the first sample application for Pi.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="64143-151">Dağıtma ve örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="64143-151">Deploy and run the sample application</span></span>
### <a name="install-nodejs-and-npm-on-pi"></a><span data-ttu-id="64143-152">Node.js ve NPM Pi üzerinde yükleme</span><span class="sxs-lookup"><span data-stu-id="64143-152">Install Node.js and NPM on Pi</span></span>
<span data-ttu-id="64143-153">Node.js ve NPM Pi üzerinde aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="64143-153">Install Node.js and NPM on Pi by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="64143-154">Bu görev, ilk çalıştırdığınızda tamamlamak için 10 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="64143-154">This task might take 10 minutes to complete the first time you run it.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="64143-155">Dağıtma ve örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="64143-155">Deploy and run the sample app</span></span>
<span data-ttu-id="64143-156">Dağıtma ve aşağıdaki komutu çalıştırarak örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="64143-156">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="64143-157">Uygulama çalıştığını doğrulama</span><span class="sxs-lookup"><span data-stu-id="64143-157">Verify the app works</span></span>
<span data-ttu-id="64143-158">Artık her iki saniye Pi yanıp sönen üzerinde LED görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="64143-158">You should now see the LED on Pi blinking every two seconds.</span></span>  <span data-ttu-id="64143-159">IŞIĞI yanıp sönen görmüyorsanız bkz [sorun giderme kılavuzu](iot-hub-raspberry-pi-kit-node-troubleshooting.md) yaygın sorunların çözümleri için.</span><span class="sxs-lookup"><span data-stu-id="64143-159">If you don’t see the LED blinking, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span></span>
<span data-ttu-id="64143-160">![IŞIĞI yanıp sönen](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="64143-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="64143-161">Özet</span><span class="sxs-lookup"><span data-stu-id="64143-161">Summary</span></span>
<span data-ttu-id="64143-162">Pi ile çalışmak için gerekli araçları yüklü ve bir örnek uygulama ile Pi LED blink dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="64143-162">You've installed the required tools to work with Pi and deployed a sample application to Pi to blink the LED.</span></span> <span data-ttu-id="64143-163">Şimdi oluşturmanıza, dağıtmanıza ve Pi ileti gönderme ve alma için Azure IOT hub'a bağlanan başka bir örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="64143-163">You can now create, deploy, and run another sample application that connects Pi to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64143-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="64143-164">Next steps</span></span>
[<span data-ttu-id="64143-165">Azure Araçları edinin</span><span class="sxs-lookup"><span data-stu-id="64143-165">Get the Azure tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)

