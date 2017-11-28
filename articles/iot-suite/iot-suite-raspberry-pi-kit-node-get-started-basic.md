---
title: "aaaConnect Raspberry Pi'yi tooAzure IOT paketi ile gerçek algılayıcılar Node.js kullanarak | Microsoft Docs"
description: "Microsoft Azure IOT Starter Kit Merhaba hello Raspberry Pi 3 ve Azure IOT paketi kullanır. Uzaktan izleme çözümü, Raspberry Pi'yi toohello node.js tooconnect kullanın, telemetri algılayıcı toohello bulut göndermek ve hello çözüm panodan çağrılan toomethods yanıt."
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
ms.openlocfilehash: 7ffb4a7a8c04b424a1f29170f4739d89f39a2429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-nodejs"></a><span data-ttu-id="f713e-104">Uzaktan izleme çözümü, Raspberry Pi 3 toohello bağlanmak ve Node.js kullanarak gerçek algılayıcı telemetri Gönder</span><span class="sxs-lookup"><span data-stu-id="f713e-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send telemetry from a real sensor using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="f713e-105">Bu öğretici nasıl toouse hello Microsoft Azure IOT Starter Kit Raspberry Pi 3 toodevelop hello bulut ile iletişim kurabilen bir sıcaklık ve nem okuyucu gösterir.</span><span class="sxs-lookup"><span data-stu-id="f713e-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 toodevelop a temperature and humidity reader that can communicate with hello cloud.</span></span> <span data-ttu-id="f713e-106">Merhaba öğretici kullanır:</span><span class="sxs-lookup"><span data-stu-id="f713e-106">hello tutorial uses:</span></span>

- <span data-ttu-id="f713e-107">Raspbian OS programlama dili Node.js hello ve Microsoft Azure IOT SDK'sı Node.js tooimplement örnek aygıt hello.</span><span class="sxs-lookup"><span data-stu-id="f713e-107">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="f713e-108">Merhaba IOT paketi Uzaktan izleme çözümü hello bulut tabanlı arka uç önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="f713e-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="f713e-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f713e-109">Overview</span></span>

<span data-ttu-id="f713e-110">Bu öğreticide, hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="f713e-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="f713e-111">Merhaba Uzaktan izleme önceden yapılandırılmış çözüm tooyour Azure aboneliği örneği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="f713e-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="f713e-112">Bu adım, otomatik olarak dağıtır ve birden çok Azure hizmetlerini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="f713e-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="f713e-113">Aygıt ve algılayıcılar toocommunicate bilgisayarınızın ve hello ile Uzaktan izleme çözümü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f713e-113">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="f713e-114">Merhaba örnek aygıt kodu tooconnect toohello Uzaktan izleme çözümü güncelleştirin ve hello çözüm panosunda görüntüleyebilirsiniz telemetri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="f713e-114">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="f713e-115">Uzaktan izleme çözümü hükümleri Azure aboneliğinizde Azure Hizmetleri kümesi hello.</span><span class="sxs-lookup"><span data-stu-id="f713e-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="f713e-116">Merhaba dağıtım gerçek Kurumsal Mimarisi yansıtır.</span><span class="sxs-lookup"><span data-stu-id="f713e-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="f713e-117">tooavoid gereksiz Azure tüketim ücretleri, kendisiyle tamamladığınızda azureiotsuite.com hello önceden yapılandırılmış çözüm örneğiniz silin.</span><span class="sxs-lookup"><span data-stu-id="f713e-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="f713e-118">Önceden yapılandırılmış çözümü yeniden hello varsa, kolayca yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f713e-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="f713e-119">Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="f713e-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="f713e-120">İndirme ve hello örnek yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f713e-120">Download and configure hello sample</span></span>

<span data-ttu-id="f713e-121">Şimdi, indirin ve, Raspberry Pi'yi Merhaba Uzaktan izleme istemci uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f713e-121">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="f713e-122">Node.js yükleme</span><span class="sxs-lookup"><span data-stu-id="f713e-122">Install Node.js</span></span>

<span data-ttu-id="f713e-123">Node.js, Böğürtlenli Pi üzerinde yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f713e-123">Install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="f713e-124">Merhaba IOT SDK'sı Node.js için 0.11.5 Node.js veya sonraki sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f713e-124">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="f713e-125">Merhaba aşağıdaki adımlarda size yol gösterecektir tooinstall Node.js v6.10.2 Raspberry Pi'yi üzerinde:</span><span class="sxs-lookup"><span data-stu-id="f713e-125">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="f713e-126">Komut tooupdate aşağıdaki hello Raspberry Pi'yi kullanın:</span><span class="sxs-lookup"><span data-stu-id="f713e-126">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="f713e-127">Komut toodownload hello Node.js ikili dosyaları tooyour Raspberry Pi'yi aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="f713e-127">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="f713e-128">Komut tooinstall hello ikili dosyalarını aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="f713e-128">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="f713e-129">Node.js v6.10.2 başarıyla yüklediniz komutu tooverify aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="f713e-129">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="f713e-130">Kopya hello depoları</span><span class="sxs-lookup"><span data-stu-id="f713e-130">Clone hello repositories</span></span>

<span data-ttu-id="f713e-131">Zaten yapmadıysanız, komutları, Pi üzerinde aşağıdaki çalıştırarak depoları hello kopya hello gerekli:</span><span class="sxs-lookup"><span data-stu-id="f713e-131">If you haven't already done so, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git`
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="f713e-132">Merhaba cihaz bağlantı dizesi güncelleştir</span><span class="sxs-lookup"><span data-stu-id="f713e-132">Update hello device connection string</span></span>

<span data-ttu-id="f713e-133">Açık hello örnek kaynak dosyasına hello **nano** Düzenleyici'yi komutu aşağıdaki hello kullanma:</span><span class="sxs-lookup"><span data-stu-id="f713e-133">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="f713e-134">Merhaba satırı bulun:</span><span class="sxs-lookup"><span data-stu-id="f713e-134">Find hello line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="f713e-135">Merhaba cihaz ve oluşturulan ve bu öğreticinin hello başlangıcında kaydedilen IOT Hub bilgileri ile Merhaba yer tutucu değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f713e-135">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="f713e-136">Değişikliklerinizi kaydetmek (**Ctrl-O**, **Enter**) ve çıkış hello Düzenleyicisi'ni (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="f713e-136">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="f713e-137">Merhaba örnek çalıştırın</span><span class="sxs-lookup"><span data-stu-id="f713e-137">Run hello sample</span></span>

<span data-ttu-id="f713e-138">Çalışma hello aşağıdaki tooinstall hello önkoşul hello örnek komutlar:</span><span class="sxs-lookup"><span data-stu-id="f713e-138">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic
npm install
```

<span data-ttu-id="f713e-139">Bu gibi durumlarda, hello örnek programı şimdi Raspberry Pi'yi hello üzerinde çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f713e-139">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="f713e-140">Merhaba komutu girin:</span><span class="sxs-lookup"><span data-stu-id="f713e-140">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="f713e-141">Merhaba aşağıdaki örnek çıkış hello komut isteminde hello Raspberry Pi'yi gördüğünüz hello çıkış örneğidir:</span><span class="sxs-lookup"><span data-stu-id="f713e-141">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Böğürtlenli Pi uygulamadan çıktı][img-raspberry-output]

<span data-ttu-id="f713e-143">Tuşuna **Ctrl-C** tooexit hello program herhangi bir zamanda.</span><span class="sxs-lookup"><span data-stu-id="f713e-143">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="f713e-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f713e-144">Next steps</span></span>

<span data-ttu-id="f713e-145">Merhaba ziyaret [Azure IOT Geliştirme Merkezi](https://azure.microsoft.com/develop/iot/) daha fazla örnekleri ve Azure IOT belgeler.</span><span class="sxs-lookup"><span data-stu-id="f713e-145">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-basic/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
