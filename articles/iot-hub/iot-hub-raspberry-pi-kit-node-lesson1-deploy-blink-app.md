---
featureFlags: usabilla
title: "Raspberry Pi'yi (düğüm) tooAzure IOT - Ders 1 bağlanın: uygulama dağıtma | Microsoft Docs"
description: "Merhaba örnek Node.js uygulaması github'dan kopyalayın ve bu uygulama tooyour Raspberry Pi 3 Panosu toodeploy gulp. Bu örnek uygulama hello bağlı LED toohello Panosu her iki saniye yanıp."
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
ms.openlocfilehash: 9732df3009b8342d4872fe2318a975a6251e772b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="6d484-105">Merhaba blink uygulama oluşturun ve dağıtın</span><span class="sxs-lookup"><span data-stu-id="6d484-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="6d484-106">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="6d484-106">What you will do</span></span>
<span data-ttu-id="6d484-107">Merhaba örnek Node.js uygulaması github'dan kopyalama ve hello gulp aracı toodeploy hello örnek uygulama tooyour Raspberry Pi 3 kullanın.</span><span class="sxs-lookup"><span data-stu-id="6d484-107">Clone hello sample Node.js application from GitHub and use hello gulp tool toodeploy hello sample application tooyour Raspberry Pi 3.</span></span> <span data-ttu-id="6d484-108">Merhaba örnek uygulaması, her iki saniye hello bağlı LED toohello Panosu yanıp.</span><span class="sxs-lookup"><span data-stu-id="6d484-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="6d484-109">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="6d484-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6d484-110">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="6d484-110">What you will learn</span></span>
<span data-ttu-id="6d484-111">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="6d484-111">In this article, you will learn:</span></span>

* <span data-ttu-id="6d484-112">Nasıl toouse hello `device-discover-cli` aracı tooretrieve PI hakkında bilgi ağ.</span><span class="sxs-lookup"><span data-stu-id="6d484-112">How toouse hello `device-discover-cli` tool tooretrieve networking information about Pi.</span></span>
* <span data-ttu-id="6d484-113">Nasıl toodeploy ve çalışma hello Pi üzerinde örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="6d484-113">How toodeploy and run hello sample application on Pi.</span></span>
* <span data-ttu-id="6d484-114">Nasıl uzaktan Pi üzerinde çalışan toodeploy ve hata ayıklama uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="6d484-114">How toodeploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6d484-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="6d484-115">What you need</span></span>
<span data-ttu-id="6d484-116">Başarıyla işlemleri aşağıdaki hello tamamlamış olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6d484-116">You must have successfully completed hello following operations:</span></span>

* [<span data-ttu-id="6d484-117">Cihazınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6d484-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)
* [<span data-ttu-id="6d484-118">Merhaba araçları edinin</span><span class="sxs-lookup"><span data-stu-id="6d484-118">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a><span data-ttu-id="6d484-119">Başlangıç IP adresi ve ana bilgisayar adını Pi alın</span><span class="sxs-lookup"><span data-stu-id="6d484-119">Obtain hello IP address and host name of Pi</span></span>
<span data-ttu-id="6d484-120">Windows veya terminal macOS veya Ubuntu bir komut istemi açın ve ardından hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6d484-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run hello following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="6d484-121">Toohello aşağıdadır benzer bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="6d484-121">You should see an output that is similar toohello following:</span></span>

![Aygıt Bulma](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="6d484-123">Merhaba not edin `IP address` ve `hostname` pi'nin.</span><span class="sxs-lookup"><span data-stu-id="6d484-123">Take note of hello `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="6d484-124">Bu bilgiler bu makalenin sonraki bölümlerinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="6d484-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="6d484-125">Pi bağlı toohello aynı bilgisayarınızda olarak ağ olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="6d484-125">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="6d484-126">Pi kablolu ağ bağlantılı tooa olsa da, bilgisayarınız bağlı tooa kablosuz ağ ise, örneğin, size hello IP göremeyebilirsiniz hello devdisco çıkış adresi.</span><span class="sxs-lookup"><span data-stu-id="6d484-126">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="6d484-127">Merhaba örnek uygulaması kopyalama</span><span class="sxs-lookup"><span data-stu-id="6d484-127">Clone hello sample application</span></span>
<span data-ttu-id="6d484-128">tooopen hello örnek kod, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="6d484-128">tooopen hello sample code, follow these steps:</span></span>

1. <span data-ttu-id="6d484-129">Merhaba örnek depoyu github'dan hello aşağıdaki komutu çalıştırarak kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="6d484-129">Clone hello sample repository from GitHub by running hello following command:</span></span>
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started.git
   ```
2. <span data-ttu-id="6d484-130">Merhaba aşağıdaki komutları çalıştırarak örnek uygulama Visual Studio Code açık hello:</span><span class="sxs-lookup"><span data-stu-id="6d484-130">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
   ```bash
   cd iot-hub-node-raspberrypi-getting-started
   cd Lesson1
   code .
   ```

![Depodaki yapısı](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-mac.png)

<span data-ttu-id="6d484-132">Merhaba `app.js` hello dosyasında `app` alt hello kod toocontrol hello LED içeren hello anahtar kaynak dosyası klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="6d484-132">hello `app.js` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="6d484-133">Uygulama bağımlılıkları yükler</span><span class="sxs-lookup"><span data-stu-id="6d484-133">Install application dependencies</span></span>
<span data-ttu-id="6d484-134">Merhaba kitaplıkları ve hello aşağıdaki komutu çalıştırarak hello örnek bir uygulama için gereken diğer modüller yükleyin:</span><span class="sxs-lookup"><span data-stu-id="6d484-134">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="6d484-135">Merhaba aygıt bağlantısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="6d484-135">Configure hello device connection</span></span>
<span data-ttu-id="6d484-136">tooconfigure Merhaba cihaz bağlantısı, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="6d484-136">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="6d484-137">Hello aşağıdaki komutu çalıştırarak Hello aygıt yapılandırma dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="6d484-137">Generate hello device configuration file by running hello following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="6d484-138">Merhaba yapılandırma dosyası `config-raspberrypi.json` içinde tooPi toolog kullanmak hello kullanıcı kimlik bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="6d484-138">hello configuration file `config-raspberrypi.json` contains hello user credentials you use toolog in tooPi.</span></span> <span data-ttu-id="6d484-139">tooavoid hello sızıntısı kullanıcı kimlik bilgilerini, hello yapılandırma dosyası hello alt klasöründe oluşturulur `.iot-hub-getting-started` bilgisayarınızda hello giriş klasörünün.</span><span class="sxs-lookup"><span data-stu-id="6d484-139">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="6d484-140">Merhaba aygıt yapılandırma dosyasını Visual Studio kodda hello aşağıdaki komutu çalıştırarak açın:</span><span class="sxs-lookup"><span data-stu-id="6d484-140">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
3. <span data-ttu-id="6d484-141">Merhaba yer tutucu Değiştir `[device hostname or IP address]` başlangıç IP adresi ya da daha önce "Elde hello IP adresi ve ana bilgisayar adlarında pi'nin." aldığınız hello ana bilgisayar adına sahip</span><span class="sxs-lookup"><span data-stu-id="6d484-141">Replace hello placeholder `[device hostname or IP address]` with hello IP address or hello host name that you got previously in "Obtain hello IP address and host name of Pi."</span></span>
   
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="6d484-143">TooRaspberry Pi bağlanırken, kullanıcı adı ve parola yerine SSH anahtarı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d484-143">You can use SSH key instead of user name and password when connecting tooRaspberry Pi.</span></span> <span data-ttu-id="6d484-144">İçinde toodo bu toogenerate hello kullanarak anahtar olacaktır sipariş **ssh-keygen** ve **ssh-kopya-ID pi @\<aygıt adresi\>**.</span><span class="sxs-lookup"><span data-stu-id="6d484-144">In order toodo this you will have toogenerate hello key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="6d484-145">Bu komutlar Windows üzerinde kullanılabilir olan **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="6d484-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="6d484-146">MacOS üzerinde toorun gereken **brew yükleme ssh-kopya-ID**.</span><span class="sxs-lookup"><span data-stu-id="6d484-146">On MacOS you need toorun **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="6d484-147">Başarılı bir şekilde hello anahtar toohello Raspberry Pi'yi dosyalarını karşıya yükledikten sonra yerine **device_password** ile **device_key_path** özelliğinde **config raspberrypi.json**.</span><span class="sxs-lookup"><span data-stu-id="6d484-147">After successfully uploading hello key toohello Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="6d484-148">Güncelleştirilmiş satırları aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="6d484-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="6d484-149">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="6d484-149">Congratulations!</span></span> <span data-ttu-id="6d484-150">Merhaba ilk örnek uygulaması pi başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="6d484-150">You've successfully created hello first sample application for Pi.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="6d484-151">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="6d484-151">Deploy and run hello sample application</span></span>
### <a name="install-nodejs-and-npm-on-pi"></a><span data-ttu-id="6d484-152">Node.js ve NPM Pi üzerinde yükleme</span><span class="sxs-lookup"><span data-stu-id="6d484-152">Install Node.js and NPM on Pi</span></span>
<span data-ttu-id="6d484-153">Node.js ve NPM Pi üzerinde hello aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="6d484-153">Install Node.js and NPM on Pi by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="6d484-154">Bu görev 10 dakika toocomplete hello çalıştırmadan ilk zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="6d484-154">This task might take 10 minutes toocomplete hello first time you run it.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="6d484-155">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="6d484-155">Deploy and run hello sample app</span></span>
<span data-ttu-id="6d484-156">Dağıtma ve hello aşağıdaki komutu çalıştırarak hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6d484-156">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="6d484-157">Merhaba uygulama çalıştığını doğrulama</span><span class="sxs-lookup"><span data-stu-id="6d484-157">Verify hello app works</span></span>
<span data-ttu-id="6d484-158">Artık her iki saniye Pi yanıp sönen üzerinde hello LED görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6d484-158">You should now see hello LED on Pi blinking every two seconds.</span></span>  <span data-ttu-id="6d484-159">Merhaba hello ışığı yanıp sönen görmüyorsanız bkz [sorun giderme kılavuzu](iot-hub-raspberry-pi-kit-node-troubleshooting.md) çözümleri toocommon sorunları.</span><span class="sxs-lookup"><span data-stu-id="6d484-159">If you don’t see hello LED blinking, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>
<span data-ttu-id="6d484-160">![IŞIĞI yanıp sönen](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="6d484-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="6d484-161">Özet</span><span class="sxs-lookup"><span data-stu-id="6d484-161">Summary</span></span>
<span data-ttu-id="6d484-162">Pi ile gerekli hello araçları toowork yüklü ve örnek uygulama tooPi tooblink hello LED dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="6d484-162">You've installed hello required tools toowork with Pi and deployed a sample application tooPi tooblink hello LED.</span></span> <span data-ttu-id="6d484-163">Artık oluşturmak, dağıtmak ve Pi tooAzure IOT hub'ı toosend bağlayan başka bir örnek uygulamayı çalıştırın ve iletileri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d484-163">You can now create, deploy, and run another sample application that connects Pi tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d484-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6d484-164">Next steps</span></span>
[<span data-ttu-id="6d484-165">Hello Azure Araçları edinin</span><span class="sxs-lookup"><span data-stu-id="6d484-165">Get hello Azure tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)

