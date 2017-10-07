---
title: aaaConnect Raspberry Pi'yi tooAzure IOT paketi ile sanal telemetriyi Node.js kullanarak | Microsoft Docs
description: "Microsoft Azure IOT Starter Kit Merhaba hello Raspberry Pi 3 ve Azure IOT paketi kullanır. Uzaktan izleme çözümü, Raspberry Pi'yi toohello node.js tooconnect kullanmak, sanal telemetriyi toohello bulut gönderebilir ve hello çözüm panodan çağrılan toomethods yanıtlayabilir."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: node.js
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: f65eeaa6e83fd89cdedae8fa8386a3e9ef8417d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a><span data-ttu-id="be2c8-104">Uzaktan izleme çözümü, Raspberry Pi 3 toohello bağlanmak ve Node.js kullanarak sanal telemetriyi Gönder</span><span class="sxs-lookup"><span data-stu-id="be2c8-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send simulated telemetry using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="be2c8-105">Bu öğretici nasıl toouse hello Raspberry Pi 3 toosimulate sıcaklık ve nem veri toosend toohello bulut gösterir.</span><span class="sxs-lookup"><span data-stu-id="be2c8-105">This tutorial shows you how toouse hello Raspberry Pi 3 toosimulate temperature and humidity data toosend toohello cloud.</span></span> <span data-ttu-id="be2c8-106">Merhaba öğretici kullanır:</span><span class="sxs-lookup"><span data-stu-id="be2c8-106">hello tutorial uses:</span></span>

- <span data-ttu-id="be2c8-107">Raspbian OS programlama dili Node.js hello ve Microsoft Azure IOT SDK'sı Node.js tooimplement örnek aygıt hello.</span><span class="sxs-lookup"><span data-stu-id="be2c8-107">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="be2c8-108">Merhaba IOT paketi Uzaktan izleme çözümü hello bulut tabanlı arka uç önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="be2c8-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="be2c8-109">Uzaktan izleme çözümü hükümleri Azure aboneliğinizde Azure Hizmetleri kümesi hello.</span><span class="sxs-lookup"><span data-stu-id="be2c8-109">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="be2c8-110">Merhaba dağıtım gerçek Kurumsal Mimarisi yansıtır.</span><span class="sxs-lookup"><span data-stu-id="be2c8-110">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="be2c8-111">tooavoid gereksiz Azure tüketim ücretleri, kendisiyle tamamladığınızda azureiotsuite.com hello önceden yapılandırılmış çözüm örneğiniz silin.</span><span class="sxs-lookup"><span data-stu-id="be2c8-111">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="be2c8-112">Önceden yapılandırılmış çözümü yeniden hello varsa, kolayca yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be2c8-112">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="be2c8-113">Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="be2c8-113">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="be2c8-114">İndirme ve hello örnek yapılandırma</span><span class="sxs-lookup"><span data-stu-id="be2c8-114">Download and configure hello sample</span></span>

<span data-ttu-id="be2c8-115">Şimdi, indirin ve, Raspberry Pi'yi Merhaba Uzaktan izleme istemci uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="be2c8-115">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="be2c8-116">Node.js yükleme</span><span class="sxs-lookup"><span data-stu-id="be2c8-116">Install Node.js</span></span>

<span data-ttu-id="be2c8-117">Henüz yapmadıysanız, Node.js, Raspberry Pi'yi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="be2c8-117">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="be2c8-118">Merhaba IOT SDK'sı Node.js için 0.11.5 Node.js veya sonraki sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="be2c8-118">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="be2c8-119">Merhaba aşağıdaki adımlarda size yol gösterecektir tooinstall Node.js v6.10.2 Raspberry Pi'yi üzerinde:</span><span class="sxs-lookup"><span data-stu-id="be2c8-119">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="be2c8-120">Komut tooupdate aşağıdaki hello Raspberry Pi'yi kullanın:</span><span class="sxs-lookup"><span data-stu-id="be2c8-120">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="be2c8-121">Komut toodownload hello Node.js ikili dosyaları tooyour Raspberry Pi'yi aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="be2c8-121">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="be2c8-122">Komut tooinstall hello ikili dosyalarını aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="be2c8-122">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="be2c8-123">Node.js v6.10.2 başarıyla yüklediniz komutu tooverify aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="be2c8-123">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="be2c8-124">Kopya hello depoları</span><span class="sxs-lookup"><span data-stu-id="be2c8-124">Clone hello repositories</span></span>

<span data-ttu-id="be2c8-125">Zaten yapmadıysanız, bir terminal komutlarda, Pi üzerinde aşağıdaki çalıştırarak depoları hello kopya hello gerekli:</span><span class="sxs-lookup"><span data-stu-id="be2c8-125">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="be2c8-126">Merhaba cihaz bağlantı dizesi güncelleştir</span><span class="sxs-lookup"><span data-stu-id="be2c8-126">Update hello device connection string</span></span>

<span data-ttu-id="be2c8-127">Açık hello örnek kaynak dosyasına hello **nano** Düzenleyici'yi komutu aşağıdaki hello kullanma:</span><span class="sxs-lookup"><span data-stu-id="be2c8-127">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="be2c8-128">Merhaba satırı bulun:</span><span class="sxs-lookup"><span data-stu-id="be2c8-128">Find hello line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="be2c8-129">Merhaba cihaz ve oluşturulan ve bu öğreticinin hello başlangıcında kaydedilen IOT Hub bilgileri ile Merhaba yer tutucu değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="be2c8-129">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="be2c8-130">Değişikliklerinizi kaydetmek (**Ctrl-O**, **Enter**) ve çıkış hello Düzenleyicisi'ni (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="be2c8-130">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="be2c8-131">Merhaba örnek çalıştırın</span><span class="sxs-lookup"><span data-stu-id="be2c8-131">Run hello sample</span></span>

<span data-ttu-id="be2c8-132">Çalışma hello aşağıdaki tooinstall hello önkoşul hello örnek komutlar:</span><span class="sxs-lookup"><span data-stu-id="be2c8-132">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

<span data-ttu-id="be2c8-133">Bu gibi durumlarda, hello örnek programı şimdi Raspberry Pi'yi hello üzerinde çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be2c8-133">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="be2c8-134">Merhaba komutu girin:</span><span class="sxs-lookup"><span data-stu-id="be2c8-134">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="be2c8-135">Merhaba aşağıdaki örnek çıkış hello komut isteminde hello Raspberry Pi'yi gördüğünüz hello çıkış örneğidir:</span><span class="sxs-lookup"><span data-stu-id="be2c8-135">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Böğürtlenli Pi uygulamadan çıktı][img-raspberry-output]

<span data-ttu-id="be2c8-137">Tuşuna **Ctrl-C** tooexit hello program herhangi bir zamanda.</span><span class="sxs-lookup"><span data-stu-id="be2c8-137">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="be2c8-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="be2c8-138">Next steps</span></span>

<span data-ttu-id="be2c8-139">Merhaba ziyaret [Azure IOT Geliştirme Merkezi](https://azure.microsoft.com/develop/iot/) daha fazla örnekleri ve Azure IOT belgeler.</span><span class="sxs-lookup"><span data-stu-id="be2c8-139">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
