---
title: "IOT paketi C toosupport bellenim kullanarak aaaConnect Raspberry Pi'yi tooAzure güncelleştirmeleri | Microsoft Docs"
description: "Microsoft Azure IOT Starter Kit Merhaba hello Raspberry Pi 3 ve Azure IOT paketi kullanır. Uzaktan izleme çözümü, Raspberry Pi'yi toohello C tooconnect kullanın, telemetri algılayıcı toohello bulut göndermek ve uzak bellenim güncelleştirme gerçekleştirin."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 36d39c6d754ddb025fd3f6b74d7795ed907b754c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a><span data-ttu-id="3b40c-104">Uzaktan izleme çözümü, Raspberry Pi 3 toohello bağlanmak ve C kullanarak uzak Bellenim güncelleştirmeleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="3b40c-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and enable remote firmware updates using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="3b40c-105">Bu öğretici nasıl toouse hello Microsoft Azure IOT Starter Kit Raspberry Pi 3 gösterir:</span><span class="sxs-lookup"><span data-stu-id="3b40c-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="3b40c-106">Merhaba bulut ile iletişim kurabilen bir sıcaklık ve nem okuyucu geliştirin.</span><span class="sxs-lookup"><span data-stu-id="3b40c-106">Develop a temperature and humidity reader that can communicate with hello cloud.</span></span>
* <span data-ttu-id="3b40c-107">Etkinleştirmek ve bir uzak bellenim güncelleştirme tooupdate hello istemci uygulaması Raspberry Pi'yi hello üzerinde gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="3b40c-107">Enable and perform a remote firmware update tooupdate hello client application on hello Raspberry Pi.</span></span>

<span data-ttu-id="3b40c-108">Merhaba öğretici kullanır:</span><span class="sxs-lookup"><span data-stu-id="3b40c-108">hello tutorial uses:</span></span>

* <span data-ttu-id="3b40c-109">Raspbian işletim sistemi, hello C programlama dili ve C tooimplement örnek cihaz için Microsoft Azure IOT SDK'sı hello.</span><span class="sxs-lookup"><span data-stu-id="3b40c-109">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
* <span data-ttu-id="3b40c-110">Merhaba IOT paketi Uzaktan izleme çözümü hello bulut tabanlı arka uç önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="3b40c-110">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="3b40c-111">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3b40c-111">Overview</span></span>

<span data-ttu-id="3b40c-112">Bu öğreticide, hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="3b40c-112">In this tutorial, you complete hello following steps:</span></span>

* <span data-ttu-id="3b40c-113">Merhaba Uzaktan izleme önceden yapılandırılmış çözüm tooyour Azure aboneliği örneği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="3b40c-113">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="3b40c-114">Bu adım, otomatik olarak dağıtır ve birden çok Azure hizmetlerini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="3b40c-114">This step automatically deploys and configures multiple Azure services.</span></span>
* <span data-ttu-id="3b40c-115">Aygıt ve algılayıcılar toocommunicate bilgisayarınızın ve hello ile Uzaktan izleme çözümü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3b40c-115">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
* <span data-ttu-id="3b40c-116">Merhaba örnek aygıt kodu tooconnect toohello Uzaktan izleme çözümü güncelleştirin ve hello çözüm panosunda görüntüleyebilirsiniz telemetri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="3b40c-116">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>
* <span data-ttu-id="3b40c-117">Merhaba örnek aygıt kodu tooupdate hello istemci uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b40c-117">Use hello sample device code tooupdate hello client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="3b40c-118">Uzaktan izleme çözümü hükümleri Azure aboneliğinizde Azure Hizmetleri kümesi hello.</span><span class="sxs-lookup"><span data-stu-id="3b40c-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="3b40c-119">Merhaba dağıtım gerçek Kurumsal Mimarisi yansıtır.</span><span class="sxs-lookup"><span data-stu-id="3b40c-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="3b40c-120">tooavoid gereksiz Azure tüketim ücretleri, kendisiyle tamamladığınızda azureiotsuite.com hello önceden yapılandırılmış çözüm örneğiniz silin.</span><span class="sxs-lookup"><span data-stu-id="3b40c-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="3b40c-121">Önceden yapılandırılmış çözümü yeniden hello varsa, kolayca yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b40c-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="3b40c-122">Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="3b40c-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="3b40c-123">İndirme ve hello örnek yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3b40c-123">Download and configure hello sample</span></span>

<span data-ttu-id="3b40c-124">Şimdi, indirin ve, Raspberry Pi'yi Merhaba Uzaktan izleme istemci uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3b40c-124">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="3b40c-125">Kopya hello depoları</span><span class="sxs-lookup"><span data-stu-id="3b40c-125">Clone hello repositories</span></span>

<span data-ttu-id="3b40c-126">Henüz yapmadıysanız, komutları, Pi üzerinde aşağıdaki çalıştırarak depoları hello kopya hello gerekli:</span><span class="sxs-lookup"><span data-stu-id="3b40c-126">If you haven't done so already, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="3b40c-127">Merhaba cihaz bağlantı dizesi güncelleştir</span><span class="sxs-lookup"><span data-stu-id="3b40c-127">Update hello device connection string</span></span>

<span data-ttu-id="3b40c-128">Merhaba açık hello örnek yapılandırma dosyasında **nano** Düzenleyici'yi komutu aşağıdaki hello kullanma:</span><span class="sxs-lookup"><span data-stu-id="3b40c-128">Open hello sample configuration file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="3b40c-129">Bilgilerle oluşturulur ve bu öğreticinin hello başlangıcında kaydedilmiş hello cihaz kimliği ve IOT hub'ı Hello yer tutucu değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3b40c-129">Replace hello placeholder values with hello device ID and IoT Hub information you created and saved at hello start of this tutorial.</span></span>

<span data-ttu-id="3b40c-130">İşiniz bittiğinde, hello deviceınfo dosyasının Merhaba içeriğine hello örnek aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="3b40c-130">When you are done, hello contents of hello deviceinfo file should look like hello following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="3b40c-131">Değişikliklerinizi kaydetmek (**Ctrl-O**, **Enter**) ve çıkış hello Düzenleyicisi'ni (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="3b40c-131">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="3b40c-132">Merhaba örnek oluşturma</span><span class="sxs-lookup"><span data-stu-id="3b40c-132">Build hello sample</span></span>

<span data-ttu-id="3b40c-133">Zaten yapmadıysanız, hello önkoşul hello Microsoft Azure IOT cihaz SDK'sı için C Raspberry Pi'yi hello üzerinde komutları bir terminalde aşağıdaki hello çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="3b40c-133">If you have not already done so, install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="3b40c-134">Merhaba örnek çözümü Raspberry Pi'yi hello üzerinde şimdi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3b40c-134">You can now build hello sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

<span data-ttu-id="3b40c-135">Bu gibi durumlarda, hello örnek programı şimdi Raspberry Pi'yi hello üzerinde çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b40c-135">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="3b40c-136">Merhaba komutu girin:</span><span class="sxs-lookup"><span data-stu-id="3b40c-136">Enter hello command:</span></span>

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

<span data-ttu-id="3b40c-137">Merhaba aşağıdaki örnek çıkış hello komut isteminde hello Raspberry Pi'yi gördüğünüz hello çıkış örneğidir:</span><span class="sxs-lookup"><span data-stu-id="3b40c-137">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Böğürtlenli Pi uygulamadan çıktı][img-raspberry-output]

<span data-ttu-id="3b40c-139">Tuşuna **Ctrl-C** tooexit hello program herhangi bir zamanda.</span><span class="sxs-lookup"><span data-stu-id="3b40c-139">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="3b40c-140">Merhaba çözüm panosunda tıklatın **aygıtları** toovisit hello **aygıtları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="3b40c-140">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="3b40c-141">Hello Raspberry Pi'yi seçin **cihaz listesi**.</span><span class="sxs-lookup"><span data-stu-id="3b40c-141">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="3b40c-142">Ardından **yöntemleri**:</span><span class="sxs-lookup"><span data-stu-id="3b40c-142">Then choose **Methods**:</span></span>

    ![Panoda aygıtları listele][img-list-devices]

1. <span data-ttu-id="3b40c-144">Merhaba üzerinde **yöntemi çağırma** sayfasında, **InitiateFirmwareUpdate** hello içinde **yöntemi** açılır.</span><span class="sxs-lookup"><span data-stu-id="3b40c-144">On hello **Invoke Method** page, choose **InitiateFirmwareUpdate** in hello **Method** dropdown.</span></span>

1. <span data-ttu-id="3b40c-145">Merhaba, **FWPackageURI** alanına, **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span><span class="sxs-lookup"><span data-stu-id="3b40c-145">In hello **FWPackageURI** field, enter **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span></span> <span data-ttu-id="3b40c-146">Bu Arşiv hello uygulamasını hello bellenim 2.0 sürümünü içerir.</span><span class="sxs-lookup"><span data-stu-id="3b40c-146">This archive file contains hello implementation of version 2.0 of hello firmware.</span></span>

1. <span data-ttu-id="3b40c-147">Seçin **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="3b40c-147">Choose **InvokeMethod**.</span></span> <span data-ttu-id="3b40c-148">Merhaba Raspberry Pi'yi Hello uygulamasına bir bildirim geri toohello çözüm Panosu gönderir.</span><span class="sxs-lookup"><span data-stu-id="3b40c-148">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard.</span></span> <span data-ttu-id="3b40c-149">Ardından, hello bellenim güncelleştirme işlemi'nin hello yeni hello bellenim sürümünü indirerek başlar:</span><span class="sxs-lookup"><span data-stu-id="3b40c-149">It then starts hello firmware update process by downloading hello new version of hello firmware:</span></span>

    ![Yöntem geçmişini göster][img-method-history]

## <a name="observe-hello-firmware-update-process"></a><span data-ttu-id="3b40c-151">Merhaba bellenim güncelleştirme işlemini inceleyin</span><span class="sxs-lookup"><span data-stu-id="3b40c-151">Observe hello firmware update process</span></span>

<span data-ttu-id="3b40c-152">Merhaba cihazda çalışan gibi hello bellenim güncelleştirme işlemi görebilirsiniz ve hello görüntüleyerek hello çözüm Panosu özelliklerinde bildirdi:</span><span class="sxs-lookup"><span data-stu-id="3b40c-152">You can observe hello firmware update process as it runs on hello device and by viewing hello reported properties in hello solution dashboard:</span></span>

1. <span data-ttu-id="3b40c-153">Merhaba güncelleştirme işleminin hello ediyor Raspberry Pi'yi hello üzerinde görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3b40c-153">You can view hello progress in of hello update process on hello Raspberry Pi:</span></span>

    ![Güncelleştirme ilerlemesini Göster][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="3b40c-155">Merhaba güncelleştirme tamamlandığında hello Uzaktan izleme uygulama sessizce yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="3b40c-155">hello remote monitoring app restarts silently when hello update completes.</span></span> <span data-ttu-id="3b40c-156">Merhaba komutunu `ps -ef` çalıştığından tooverify.</span><span class="sxs-lookup"><span data-stu-id="3b40c-156">Use hello command `ps -ef` tooverify it is running.</span></span> <span data-ttu-id="3b40c-157">Tooterminate hello işlem istiyorsanız hello kullanın `kill` hello işlem kimlikli komutu.</span><span class="sxs-lookup"><span data-stu-id="3b40c-157">If you want tooterminate hello process, use hello `kill` command with hello process id.</span></span>

1. <span data-ttu-id="3b40c-158">Merhaba çözüm portalında hello aygıt tarafından bildirilen şekilde hello bellenim güncelleştirme hello durumunu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b40c-158">You can view hello status of hello firmware update, as reported by hello device, in hello solution portal.</span></span> <span data-ttu-id="3b40c-159">Merhaba aşağıdaki ekran görüntüsü hello durumu ve her aşamanın hello güncelleştirme işlemini hello yeni üretici yazılımı sürümüne ve süresini gösterir:</span><span class="sxs-lookup"><span data-stu-id="3b40c-159">hello following screenshot shows hello status and duration of each stage of hello update process, and hello new firmware version:</span></span>

    ![İş durumunu göster][img-job-status]

    <span data-ttu-id="3b40c-161">Geri toohello Pano giderseniz, hello aygıt hala hello bellenim güncelleştirme aşağıdaki telemetri gönderiyor doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b40c-161">If you navigate back toohello dashboard, you can verify hello device is still sending telemetry following hello firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="3b40c-162">Merhaba Uzaktan izleme çözümü Azure hesabınızda çalışan bırakırsanız hello çalıştırıldığında için faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="3b40c-162">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="3b40c-163">Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="3b40c-163">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="3b40c-164">Bunu kullanmayı bitirdikten sonra hello önceden yapılandırılmış çözümü Azure hesabınızdan silin.</span><span class="sxs-lookup"><span data-stu-id="3b40c-164">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b40c-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3b40c-165">Next steps</span></span>

<span data-ttu-id="3b40c-166">Merhaba ziyaret [Azure IOT Geliştirme Merkezi](https://azure.microsoft.com/develop/iot/) daha fazla örnekleri ve Azure IOT belgeler.</span><span class="sxs-lookup"><span data-stu-id="3b40c-166">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md