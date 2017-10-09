---
title: "IOT paketi Node.js toosupport bellenim kullanarak aaaConnect Raspberry Pi'yi tooAzure güncelleştirmeleri | Microsoft Docs"
description: "Microsoft Azure IOT Starter Kit Merhaba hello Raspberry Pi 3 ve Azure IOT paketi kullanır. Uzaktan izleme çözümü, Raspberry Pi'yi toohello node.js tooconnect kullanın, telemetri algılayıcı toohello bulut göndermek ve uzak bellenim güncelleştirme gerçekleştirin."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 43bd3f16ee3d292cd9cffa8bfe7d4ca721e5c39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-nodejs"></a><span data-ttu-id="ee79d-104">Uzaktan izleme çözümü, Raspberry Pi 3 toohello bağlanmak ve Node.js kullanarak uzak Bellenim güncelleştirmeleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ee79d-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and enable remote firmware updates using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="ee79d-105">Bu öğretici nasıl toouse hello Microsoft Azure IOT Starter Kit Raspberry Pi 3 gösterir:</span><span class="sxs-lookup"><span data-stu-id="ee79d-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="ee79d-106">Merhaba bulut ile iletişim kurabilen bir sıcaklık ve nem okuyucu geliştirin.</span><span class="sxs-lookup"><span data-stu-id="ee79d-106">Develop a temperature and humidity reader that can communicate with hello cloud.</span></span>
* <span data-ttu-id="ee79d-107">Etkinleştirmek ve bir uzak bellenim güncelleştirme tooupdate hello istemci uygulaması Raspberry Pi'yi hello üzerinde gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="ee79d-107">Enable and perform a remote firmware update tooupdate hello client application on hello Raspberry Pi.</span></span>

<span data-ttu-id="ee79d-108">Merhaba öğretici kullanır:</span><span class="sxs-lookup"><span data-stu-id="ee79d-108">hello tutorial uses:</span></span>

- <span data-ttu-id="ee79d-109">Raspbian OS programlama dili Node.js hello ve Microsoft Azure IOT SDK'sı Node.js tooimplement örnek aygıt hello.</span><span class="sxs-lookup"><span data-stu-id="ee79d-109">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="ee79d-110">Merhaba IOT paketi Uzaktan izleme çözümü hello bulut tabanlı arka uç önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="ee79d-110">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="ee79d-111">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ee79d-111">Overview</span></span>

<span data-ttu-id="ee79d-112">Bu öğreticide, hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="ee79d-112">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="ee79d-113">Merhaba Uzaktan izleme önceden yapılandırılmış çözüm tooyour Azure aboneliği örneği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="ee79d-113">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="ee79d-114">Bu adım, otomatik olarak dağıtır ve birden çok Azure hizmetlerini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="ee79d-114">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="ee79d-115">Aygıt ve algılayıcılar toocommunicate bilgisayarınızın ve hello ile Uzaktan izleme çözümü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ee79d-115">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="ee79d-116">Merhaba örnek aygıt kodu tooconnect toohello Uzaktan izleme çözümü güncelleştirin ve hello çözüm panosunda görüntüleyebilirsiniz telemetri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="ee79d-116">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>
- <span data-ttu-id="ee79d-117">Merhaba örnek aygıt kodu tooupdate hello istemci uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="ee79d-117">Use hello sample device code tooupdate hello client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="ee79d-118">Uzaktan izleme çözümü hükümleri Azure aboneliğinizde Azure Hizmetleri kümesi hello.</span><span class="sxs-lookup"><span data-stu-id="ee79d-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="ee79d-119">Merhaba dağıtım gerçek Kurumsal Mimarisi yansıtır.</span><span class="sxs-lookup"><span data-stu-id="ee79d-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="ee79d-120">tooavoid gereksiz Azure tüketim ücretleri, kendisiyle tamamladığınızda azureiotsuite.com hello önceden yapılandırılmış çözüm örneğiniz silin.</span><span class="sxs-lookup"><span data-stu-id="ee79d-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="ee79d-121">Önceden yapılandırılmış çözümü yeniden hello varsa, kolayca yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee79d-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="ee79d-122">Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="ee79d-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="ee79d-123">İndirme ve hello örnek yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ee79d-123">Download and configure hello sample</span></span>

<span data-ttu-id="ee79d-124">Şimdi, indirin ve, Raspberry Pi'yi Merhaba Uzaktan izleme istemci uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ee79d-124">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="ee79d-125">Node.js yükleme</span><span class="sxs-lookup"><span data-stu-id="ee79d-125">Install Node.js</span></span>

<span data-ttu-id="ee79d-126">Henüz yapmadıysanız, Node.js, Raspberry Pi'yi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ee79d-126">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="ee79d-127">Merhaba IOT SDK'sı Node.js için 0.11.5 Node.js veya sonraki sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ee79d-127">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="ee79d-128">Merhaba aşağıdaki adımlarda size yol gösterecektir tooinstall Node.js v6.10.2 Raspberry Pi'yi üzerinde:</span><span class="sxs-lookup"><span data-stu-id="ee79d-128">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="ee79d-129">Komut tooupdate aşağıdaki hello Raspberry Pi'yi kullanın:</span><span class="sxs-lookup"><span data-stu-id="ee79d-129">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="ee79d-130">Komut toodownload hello Node.js ikili dosyaları tooyour Raspberry Pi'yi aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="ee79d-130">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="ee79d-131">Komut tooinstall hello ikili dosyalarını aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="ee79d-131">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="ee79d-132">Node.js v6.10.2 başarıyla yüklediniz komutu tooverify aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="ee79d-132">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="ee79d-133">Kopya hello depoları</span><span class="sxs-lookup"><span data-stu-id="ee79d-133">Clone hello repositories</span></span>

<span data-ttu-id="ee79d-134">Henüz yapmadıysanız, komutları, Pi üzerinde aşağıdaki çalıştırarak depoları hello kopya hello gerekli:</span><span class="sxs-lookup"><span data-stu-id="ee79d-134">If you haven't done so already, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="ee79d-135">Merhaba cihaz bağlantı dizesi güncelleştir</span><span class="sxs-lookup"><span data-stu-id="ee79d-135">Update hello device connection string</span></span>

<span data-ttu-id="ee79d-136">Merhaba açık hello örnek yapılandırma dosyasında **nano** Düzenleyici'yi komutu aşağıdaki hello kullanma:</span><span class="sxs-lookup"><span data-stu-id="ee79d-136">Open hello sample configuration file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="ee79d-137">Merhaba cihaz kimliği ve oluşturulan ve bu öğreticinin hello başlangıcında kaydedilen IOT Hub bilgileri ile Merhaba yer tutucu değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ee79d-137">Replace hello placeholder values with hello device id and IoT Hub information you created and saved at hello start of this tutorial.</span></span>

<span data-ttu-id="ee79d-138">İşiniz bittiğinde, hello deviceınfo dosyasının Merhaba içeriğine hello örnek aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="ee79d-138">When you are done, hello contents of hello deviceinfo file should look like hello following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="ee79d-139">Değişikliklerinizi kaydetmek (**Ctrl-O**, **Enter**) ve çıkış hello Düzenleyicisi'ni (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="ee79d-139">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="ee79d-140">Merhaba örnek çalıştırın</span><span class="sxs-lookup"><span data-stu-id="ee79d-140">Run hello sample</span></span>

<span data-ttu-id="ee79d-141">Çalışma hello aşağıdaki tooinstall hello önkoşul hello örnek komutlar:</span><span class="sxs-lookup"><span data-stu-id="ee79d-141">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advance/1.0
npm install
```

<span data-ttu-id="ee79d-142">Bu gibi durumlarda, hello örnek programı şimdi Raspberry Pi'yi hello üzerinde çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee79d-142">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="ee79d-143">Merhaba komutu girin:</span><span class="sxs-lookup"><span data-stu-id="ee79d-143">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/1.0/remote_monitoring.js
```

<span data-ttu-id="ee79d-144">Merhaba aşağıdaki örnek çıkış hello komut isteminde hello Raspberry Pi'yi gördüğünüz hello çıkış örneğidir:</span><span class="sxs-lookup"><span data-stu-id="ee79d-144">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Böğürtlenli Pi uygulamadan çıktı][img-raspberry-output]

<span data-ttu-id="ee79d-146">Tuşuna **Ctrl-C** tooexit hello program herhangi bir zamanda.</span><span class="sxs-lookup"><span data-stu-id="ee79d-146">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="ee79d-147">Merhaba çözüm panosunda tıklatın **aygıtları** toovisit hello **aygıtları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="ee79d-147">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="ee79d-148">Hello Raspberry Pi'yi seçin **cihaz listesi**.</span><span class="sxs-lookup"><span data-stu-id="ee79d-148">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="ee79d-149">Ardından **yöntemleri**:</span><span class="sxs-lookup"><span data-stu-id="ee79d-149">Then choose **Methods**:</span></span>

    ![Panoda aygıtları listele][img-list-devices]

1. <span data-ttu-id="ee79d-151">Merhaba üzerinde **yöntemi çağırma** sayfasında, **InitiateFirmwareUpdate** hello içinde **yöntemi** açılır.</span><span class="sxs-lookup"><span data-stu-id="ee79d-151">On hello **Invoke Method** page, choose **InitiateFirmwareUpdate** in hello **Method** dropdown.</span></span>

1. <span data-ttu-id="ee79d-152">Merhaba, **FWPackageURI** alanına, **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span><span class="sxs-lookup"><span data-stu-id="ee79d-152">In hello **FWPackageURI** field, enter **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span></span> <span data-ttu-id="ee79d-153">Bu dosya hello uyarlamasını hello bellenim 2.0 sürümünü içerir.</span><span class="sxs-lookup"><span data-stu-id="ee79d-153">This file contains hello implementation of version 2.0 of hello firmware.</span></span>

1. <span data-ttu-id="ee79d-154">Seçin **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="ee79d-154">Choose **InvokeMethod**.</span></span> <span data-ttu-id="ee79d-155">Merhaba Raspberry Pi'yi Hello uygulamasına bir bildirim geri toohello çözüm Panosu gönderir.</span><span class="sxs-lookup"><span data-stu-id="ee79d-155">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard.</span></span> <span data-ttu-id="ee79d-156">Ardından, hello bellenim güncelleştirme işlemi'nin hello yeni hello bellenim sürümünü indirerek başlar:</span><span class="sxs-lookup"><span data-stu-id="ee79d-156">It then starts hello firmware update process by downloading hello new version of hello firmware:</span></span>

    ![Yöntem geçmişini göster][img-method-history]

## <a name="observe-hello-firmware-update-process"></a><span data-ttu-id="ee79d-158">Merhaba bellenim güncelleştirme işlemini inceleyin</span><span class="sxs-lookup"><span data-stu-id="ee79d-158">Observe hello firmware update process</span></span>

<span data-ttu-id="ee79d-159">Merhaba cihazda çalışan gibi hello bellenim güncelleştirme işlemi görebilirsiniz ve hello görüntüleyerek hello çözüm Panosu özelliklerinde bildirdi:</span><span class="sxs-lookup"><span data-stu-id="ee79d-159">You can observe hello firmware update process as it runs on hello device and by viewing hello reported properties in hello solution dashboard:</span></span>

1. <span data-ttu-id="ee79d-160">Merhaba güncelleştirme işleminin hello ediyor Raspberry Pi'yi hello üzerinde görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ee79d-160">You can view hello progress in of hello update process on hello Raspberry Pi:</span></span>

    ![Güncelleştirme ilerlemesini Göster][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="ee79d-162">Merhaba güncelleştirme tamamlandığında hello Uzaktan izleme uygulama sessizce yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="ee79d-162">hello remote monitoring app restarts silently when hello update completes.</span></span> <span data-ttu-id="ee79d-163">Merhaba komutunu `ps -ef` çalıştığından tooverify.</span><span class="sxs-lookup"><span data-stu-id="ee79d-163">Use hello command `ps -ef` tooverify it is running.</span></span> <span data-ttu-id="ee79d-164">Tooterminate hello işlem istiyorsanız hello kullanın `kill` hello işlem kimlikli komutu.</span><span class="sxs-lookup"><span data-stu-id="ee79d-164">If you want tooterminate hello process, use hello `kill` command with hello process id.</span></span>

1. <span data-ttu-id="ee79d-165">Merhaba çözüm portalında hello aygıt tarafından bildirilen şekilde hello bellenim güncelleştirme hello durumunu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee79d-165">You can view hello status of hello firmware update, as reported by hello device, in hello solution portal.</span></span> <span data-ttu-id="ee79d-166">Merhaba aşağıdaki ekran görüntüsü hello durumu ve her aşamanın hello güncelleştirme işlemini hello yeni üretici yazılımı sürümüne ve süresini gösterir:</span><span class="sxs-lookup"><span data-stu-id="ee79d-166">hello following screenshot shows hello status and duration of each stage of hello update process, and hello new firmware version:</span></span>

    ![İş durumunu göster][img-job-status]

    <span data-ttu-id="ee79d-168">Geri toohello Pano giderseniz, hello aygıt hala hello bellenim güncelleştirme aşağıdaki telemetri gönderiyor doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee79d-168">If you navigate back toohello dashboard, you can verify hello device is still sending telemetry following hello firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="ee79d-169">Merhaba Uzaktan izleme çözümü Azure hesabınızda çalışan bırakırsanız hello çalıştırıldığında için faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="ee79d-169">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="ee79d-170">Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="ee79d-170">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="ee79d-171">Bunu kullanmayı bitirdikten sonra hello önceden yapılandırılmış çözümü Azure hesabınızdan silin.</span><span class="sxs-lookup"><span data-stu-id="ee79d-171">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee79d-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ee79d-172">Next steps</span></span>

<span data-ttu-id="ee79d-173">Merhaba ziyaret [Azure IOT Geliştirme Merkezi](https://azure.microsoft.com/develop/iot/) daha fazla örnekleri ve Azure IOT belgeler.</span><span class="sxs-lookup"><span data-stu-id="ee79d-173">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
