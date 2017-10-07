---
title: "Connect Raspberry pi (C) tooAzure IOT - Ders 1: uygulama dağıtma | Microsoft Docs"
description: "Merhaba örnek C uygulaması github'dan kopyalayın ve bu uygulama tooyour Raspberry Pi 3 Panosu toodeploy gulp. Bu örnek uygulama hello bağlı LED toohello Panosu her iki saniye yanıp."
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
ms.openlocfilehash: e90c3360c4de1873313db19561c781eb21dbf1d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="9b32a-105">Merhaba blink uygulama oluşturun ve dağıtın</span><span class="sxs-lookup"><span data-stu-id="9b32a-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="9b32a-106">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="9b32a-106">What you will do</span></span>
<span data-ttu-id="9b32a-107">Merhaba örnek C uygulaması github'dan kopyalama ve hello gulp aracı toodeploy hello örnek uygulama tooRaspberry Pi 3 kullanın.</span><span class="sxs-lookup"><span data-stu-id="9b32a-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooRaspberry Pi 3.</span></span> <span data-ttu-id="9b32a-108">Merhaba örnek uygulaması, her iki saniye hello bağlı LED toohello Panosu yanıp.</span><span class="sxs-lookup"><span data-stu-id="9b32a-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="9b32a-109">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="9b32a-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9b32a-110">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="9b32a-110">What you will learn</span></span>
<span data-ttu-id="9b32a-111">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="9b32a-111">In this article, you will learn:</span></span>

* <span data-ttu-id="9b32a-112">Nasıl toouse hello `device-discover-cli` aracı tooretrieve PI hakkında bilgi ağ.</span><span class="sxs-lookup"><span data-stu-id="9b32a-112">How toouse hello `device-discover-cli` tool tooretrieve networking information about Pi.</span></span>
* <span data-ttu-id="9b32a-113">Nasıl toodeploy ve çalışma hello Pi üzerinde örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="9b32a-113">How toodeploy and run hello sample application on Pi.</span></span>
* <span data-ttu-id="9b32a-114">Nasıl uzaktan Pi üzerinde çalışan toodeploy ve hata ayıklama uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="9b32a-114">How toodeploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9b32a-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="9b32a-115">What you need</span></span>
<span data-ttu-id="9b32a-116">Başarıyla işlemleri aşağıdaki hello tamamlamış olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9b32a-116">You must have successfully completed hello following operations:</span></span>

* [<span data-ttu-id="9b32a-117">Cihazınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9b32a-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [<span data-ttu-id="9b32a-118">Merhaba araçları edinin</span><span class="sxs-lookup"><span data-stu-id="9b32a-118">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a><span data-ttu-id="9b32a-119">Başlangıç IP adresi ve ana bilgisayar adını Pi alın</span><span class="sxs-lookup"><span data-stu-id="9b32a-119">Obtain hello IP address and host name of Pi</span></span>
<span data-ttu-id="9b32a-120">Windows veya terminal macOS veya Ubuntu bir komut istemi açın ve ardından hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9b32a-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run hello following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="9b32a-121">Toohello aşağıdadır benzer bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="9b32a-121">You should see an output that is similar toohello following:</span></span>

![Aygıt Bulma](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="9b32a-123">Merhaba not edin `IP address` ve `hostname` pi'nin.</span><span class="sxs-lookup"><span data-stu-id="9b32a-123">Take note of hello `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="9b32a-124">Bu bilgiler bu makalenin sonraki bölümlerinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b32a-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="9b32a-125">Pi bağlı toohello aynı bilgisayarınızda olarak ağ olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9b32a-125">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="9b32a-126">Pi kablolu ağ bağlantılı tooa olsa da, bilgisayarınız bağlı tooa kablosuz ağ ise, örneğin, size hello IP göremeyebilirsiniz hello devdisco çıkış adresi.</span><span class="sxs-lookup"><span data-stu-id="9b32a-126">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="9b32a-127">Açık Merhaba örnek uygulaması</span><span class="sxs-lookup"><span data-stu-id="9b32a-127">Open hello sample application</span></span>
<span data-ttu-id="9b32a-128">tooopen hello örnek uygulama, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="9b32a-128">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="9b32a-129">Merhaba örnek depoyu github'dan hello aşağıdaki komutu çalıştırarak kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="9b32a-129">Clone hello sample repository from GitHub by running hello following command:</span></span>
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. <span data-ttu-id="9b32a-130">Merhaba aşağıdaki komutları çalıştırarak örnek uygulama Visual Studio Code açık hello:</span><span class="sxs-lookup"><span data-stu-id="9b32a-130">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Depodaki yapısı](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

<span data-ttu-id="9b32a-132">Merhaba `main.c` hello dosyasında `app` alt hello kod toocontrol hello LED içeren hello anahtar kaynak dosyası klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="9b32a-132">hello `main.c` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="9b32a-133">Uygulama bağımlılıkları yükler</span><span class="sxs-lookup"><span data-stu-id="9b32a-133">Install application dependencies</span></span>
<span data-ttu-id="9b32a-134">Merhaba kitaplıkları ve hello aşağıdaki komutu çalıştırarak hello örnek bir uygulama için gereken diğer modüller yükleyin:</span><span class="sxs-lookup"><span data-stu-id="9b32a-134">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="9b32a-135">Merhaba aygıt bağlantısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="9b32a-135">Configure hello device connection</span></span>
<span data-ttu-id="9b32a-136">tooconfigure Merhaba cihaz bağlantısı, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="9b32a-136">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="9b32a-137">Hello aşağıdaki komutu çalıştırarak Hello aygıt yapılandırma dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="9b32a-137">Generate hello device configuration file by running hello following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="9b32a-138">Merhaba yapılandırma dosyası `config-raspberrypi.json` içinde tooPi toolog kullanmak hello kullanıcı kimlik bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="9b32a-138">hello configuration file `config-raspberrypi.json` contains hello user credentials you use toolog in tooPi.</span></span> <span data-ttu-id="9b32a-139">tooavoid hello sızıntısı kullanıcı kimlik bilgilerini, hello yapılandırma dosyası hello alt klasöründe oluşturulur `.iot-hub-getting-started` bilgisayarınızda hello giriş klasörünün.</span><span class="sxs-lookup"><span data-stu-id="9b32a-139">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="9b32a-140">Merhaba aygıt yapılandırma dosyasını Visual Studio kodda hello aşağıdaki komutu çalıştırarak açın:</span><span class="sxs-lookup"><span data-stu-id="9b32a-140">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. <span data-ttu-id="9b32a-141">Merhaba yer tutucu Değiştir `[device hostname or IP address]` başlangıç IP adresi ya da daha önce "Elde hello IP adresi ve ana bilgisayar adlarında pi'nin." aldığınız hello ana bilgisayar adına sahip</span><span class="sxs-lookup"><span data-stu-id="9b32a-141">Replace hello placeholder `[device hostname or IP address]` with hello IP address or hello host name that you got previously in "Obtain hello IP address and host name of Pi."</span></span>
   
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="9b32a-143">TooRaspberry Pi bağlanırken, kullanıcı adı ve parola yerine SSH anahtarı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b32a-143">You can use SSH key instead of user name and password when connecting tooRaspberry Pi.</span></span> <span data-ttu-id="9b32a-144">İçinde toodo bu toogenerate hello kullanarak anahtar olacaktır sipariş **ssh-keygen** ve **ssh-kopya-ID pi @\<aygıt adresi\>**.</span><span class="sxs-lookup"><span data-stu-id="9b32a-144">In order toodo this you will have toogenerate hello key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="9b32a-145">Bu komutlar Windows üzerinde kullanılabilir olan **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="9b32a-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="9b32a-146">MacOS üzerinde toorun gereken **brew yükleme ssh-kopya-ID**.</span><span class="sxs-lookup"><span data-stu-id="9b32a-146">On MacOS you need toorun **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="9b32a-147">Başarılı bir şekilde hello anahtar toohello Raspberry Pi'yi dosyalarını karşıya yükledikten sonra yerine **device_password** ile **device_key_path** özelliğinde **config raspberrypi.json**.</span><span class="sxs-lookup"><span data-stu-id="9b32a-147">After successfully uploading hello key toohello Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="9b32a-148">Güncelleştirilmiş satırları aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="9b32a-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="9b32a-149">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="9b32a-149">Congratulations!</span></span> <span data-ttu-id="9b32a-150">Merhaba ilk örnek uygulaması pi başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="9b32a-150">You've successfully created hello first sample application for Pi.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="9b32a-151">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9b32a-151">Deploy and run hello sample application</span></span>
### <a name="install-hello-azure-iot-hub-sdk-on-pi"></a><span data-ttu-id="9b32a-152">Pi üzerinde Hello Azure IOT Hub SDK'sını yükleyin</span><span class="sxs-lookup"><span data-stu-id="9b32a-152">Install hello Azure IoT Hub SDK on Pi</span></span>
<span data-ttu-id="9b32a-153">Hello Azure IOT Hub SDK'sı üzerinde Pi hello aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="9b32a-153">Install hello Azure IoT Hub SDK on Pi by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="9b32a-154">Bu görev, birkaç dakika toocomplete hello çalıştırmadan ilk zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="9b32a-154">This task might take a few minutes toocomplete hello first time you run it.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="9b32a-155">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9b32a-155">Deploy and run hello sample app</span></span>
<span data-ttu-id="9b32a-156">Dağıtma ve hello aşağıdaki komutu çalıştırarak hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9b32a-156">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="9b32a-157">Merhaba uygulama çalıştığını doğrulama</span><span class="sxs-lookup"><span data-stu-id="9b32a-157">Verify hello app works</span></span>
<span data-ttu-id="9b32a-158">Merhaba örnek uygulama için 20 kez Hello ışığı yanıp sonra otomatik olarak sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="9b32a-158">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="9b32a-159">Merhaba hello ışığı yanıp sönen görmüyorsanız bkz [sorun giderme kılavuzu](iot-hub-raspberry-pi-kit-c-troubleshooting.md) çözümleri toocommon sorunları.</span><span class="sxs-lookup"><span data-stu-id="9b32a-159">If you don’t see hello LED blinking, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>
<span data-ttu-id="9b32a-160">![IŞIĞI yanıp sönen](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="9b32a-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="9b32a-161">Özet</span><span class="sxs-lookup"><span data-stu-id="9b32a-161">Summary</span></span>
<span data-ttu-id="9b32a-162">Pi ile gerekli hello araçları toowork yüklü ve örnek uygulama tooPi tooblink hello LED dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="9b32a-162">You've installed hello required tools toowork with Pi and deployed a sample application tooPi tooblink hello LED.</span></span> <span data-ttu-id="9b32a-163">Artık oluşturmak, dağıtmak ve Pi tooAzure IOT hub'ı toosend bağlayan başka bir örnek uygulamayı çalıştırın ve iletileri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b32a-163">You can now create, deploy, and run another sample application that connects Pi tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b32a-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9b32a-164">Next steps</span></span>
[<span data-ttu-id="9b32a-165">Azure Araçları edinin</span><span class="sxs-lookup"><span data-stu-id="9b32a-165">Get Azure tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)

