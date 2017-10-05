---
title: "Azure IOT paketi ile gerçek algılayıcılar Node.js kullanarak Raspberry Pi'yi bağlanma | Microsoft Docs"
description: "Microsoft Azure IOT Starter Kit Böğürtlenli pi 3 kullanın ve Azure IOT paketi. Uzaktan izleme çözümüne Raspberry Pi'yi bağlanmak için kullanım Node.js telemetri algılayıcı buluta göndermek ve çözüm panodan çağrılan yöntemler yanıt verir."
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
ms.openlocfilehash: 91546157cc8eabf68706391ce706038d8dc5f82d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-nodejs"></a><span data-ttu-id="a377b-104">Raspberry Pi 3 Uzaktan izleme çözümüne bağlama ve Node.js kullanarak gerçek algılayıcı telemetri Gönder</span><span class="sxs-lookup"><span data-stu-id="a377b-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send telemetry from a real sensor using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="a377b-105">Bu öğretici, Microsoft Azure IOT Starter Kit Raspberry Pi 3 Bulutu ile iletişim kurabilen bir sıcaklık ve nem okuyucu geliştirmek için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a377b-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to develop a temperature and humidity reader that can communicate with the cloud.</span></span> <span data-ttu-id="a377b-106">Öğretici kullanır:</span><span class="sxs-lookup"><span data-stu-id="a377b-106">The tutorial uses:</span></span>

- <span data-ttu-id="a377b-107">Raspbian işletim sistemi, Node.js programlama dili ve Node.js için Microsoft Azure IOT SDK'sı bir örnek aygıt uygulamak için.</span><span class="sxs-lookup"><span data-stu-id="a377b-107">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="a377b-108">IOT paketi Uzaktan izleme çözümü bulut tabanlı arka uç önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="a377b-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="a377b-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="a377b-109">Overview</span></span>

<span data-ttu-id="a377b-110">Bu öğreticide, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="a377b-110">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="a377b-111">Önceden yapılandırılmış Uzaktan izleme çözümü örneği Azure aboneliğinize dağıtın.</span><span class="sxs-lookup"><span data-stu-id="a377b-111">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="a377b-112">Bu adım, otomatik olarak dağıtır ve birden çok Azure hizmetlerini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="a377b-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="a377b-113">Bilgisayarınız ve Uzaktan izleme çözümü ile iletişim kurmak için aygıt ve algılayıcılar ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a377b-113">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="a377b-114">Uzaktan izleme çözümüne bağlama için örnek cihaz kod güncelleştirin ve çözüm panosunda görüntüleyebilirsiniz telemetri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="a377b-114">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="a377b-115">Uzaktan izleme çözümü Azure aboneliğinizde Azure Hizmetleri kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a377b-115">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="a377b-116">Dağıtım gerçek Kurumsal Mimarisi yansıtır.</span><span class="sxs-lookup"><span data-stu-id="a377b-116">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="a377b-117">Gereksiz Azure tüketim ücretleri önlemek için kendisiyle tamamladığınızda azureiotsuite.com önceden yapılandırılmış çözüm örneğiniz silin.</span><span class="sxs-lookup"><span data-stu-id="a377b-117">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="a377b-118">Önceden yapılandırılmış çözümü yeniden gerekiyorsa, kolayca yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a377b-118">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="a377b-119">Uzaktan izleme çözümü çalışırken tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="a377b-119">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="a377b-120">İndirme ve örnek yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a377b-120">Download and configure the sample</span></span>

<span data-ttu-id="a377b-121">Şimdi, indirin ve Uzaktan izleme istemci uygulaması, Raspberry Pi'yi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a377b-121">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="a377b-122">Node.js yükleme</span><span class="sxs-lookup"><span data-stu-id="a377b-122">Install Node.js</span></span>

<span data-ttu-id="a377b-123">Node.js, Böğürtlenli Pi üzerinde yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a377b-123">Install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="a377b-124">Node.js için IOT SDK'sı 0.11.5 Node.js veya sonraki sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a377b-124">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="a377b-125">Aşağıdaki adımlar, Raspberry Pi'yi Node.js v6.10.2 yükleme gösterir:</span><span class="sxs-lookup"><span data-stu-id="a377b-125">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="a377b-126">Raspberry Pi'yi güncelleştirmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="a377b-126">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="a377b-127">Raspberry Pi'yi Node.js ikilileri indirmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="a377b-127">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="a377b-128">İkili dosyaları yüklemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="a377b-128">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="a377b-129">Node.js v6.10.2 başarıyla yüklediniz doğrulamak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="a377b-129">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="a377b-130">Depoları kopyalama</span><span class="sxs-lookup"><span data-stu-id="a377b-130">Clone the repositories</span></span>

<span data-ttu-id="a377b-131">Zaten yapmadıysanız, gerekli depoları, Pi üzerinde aşağıdaki komutları çalıştırarak kopyalama:</span><span class="sxs-lookup"><span data-stu-id="a377b-131">If you haven't already done so, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git`
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="a377b-132">Güncelleştirme cihaz bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="a377b-132">Update the device connection string</span></span>

<span data-ttu-id="a377b-133">Örnek kaynak dosyasında açma **nano** Düzenleyicisi aşağıdaki komutu kullanarak:</span><span class="sxs-lookup"><span data-stu-id="a377b-133">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="a377b-134">Satırı bulun:</span><span class="sxs-lookup"><span data-stu-id="a377b-134">Find the line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="a377b-135">Aygıt ve oluşturulan ve bu öğreticinin başlangıcında kaydedilen IOT hub'ı bilgi yer tutucu değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a377b-135">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="a377b-136">Değişikliklerinizi kaydetmek (**Ctrl-O**, **Enter**) ve düzenleyiciden çıkın (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="a377b-136">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="a377b-137">Örnek çalıştırın</span><span class="sxs-lookup"><span data-stu-id="a377b-137">Run the sample</span></span>

<span data-ttu-id="a377b-138">Örnek önkoşul paketleri yüklemek için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a377b-138">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic
npm install
```

<span data-ttu-id="a377b-139">Örnek program Raspberry Pi'yi şimdi çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a377b-139">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="a377b-140">Aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="a377b-140">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="a377b-141">Aşağıdaki örnek çıkış Raspberry Pi'yi komut satırına bakın çıkış örneğidir:</span><span class="sxs-lookup"><span data-stu-id="a377b-141">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Böğürtlenli Pi uygulamadan çıktı][img-raspberry-output]

<span data-ttu-id="a377b-143">Tuşuna **Ctrl-C** herhangi bir zamanda programı'ndan çıkmak için.</span><span class="sxs-lookup"><span data-stu-id="a377b-143">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="a377b-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a377b-144">Next steps</span></span>

<span data-ttu-id="a377b-145">Ziyaret [Azure IOT Geliştirme Merkezi](https://azure.microsoft.com/develop/iot/) daha fazla örnekleri ve Azure IOT belgeler.</span><span class="sxs-lookup"><span data-stu-id="a377b-145">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-basic/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
