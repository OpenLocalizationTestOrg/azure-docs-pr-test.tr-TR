---
title: "Azure IOT paketi C ile sanal telemetriyi kullanarak Raspberry Pi'yi bağlanma | Microsoft Docs"
description: "Microsoft Azure IOT Starter Kit Böğürtlenli pi 3 kullanın ve Azure IOT paketi. Uzaktan izleme çözümüne Raspberry Pi'yi bağlanmak için kullanım C buluta sanal telemetriyi göndermek ve çözüm panodan çağrılan yöntemler yanıt verir."
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
ms.openlocfilehash: 43b82e5fb6a309283979f23d8c87af600595bc55
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-simulated-telemetry-using-c"></a><span data-ttu-id="c7978-104">Raspberry Pi 3 Uzaktan izleme çözümüne bağlama ve C kullanarak sanal telemetriyi Gönder</span><span class="sxs-lookup"><span data-stu-id="c7978-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send simulated telemetry using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="c7978-105">Bu öğretici Raspberry Pi 3 buluta göndermek için sıcaklık ve nem veri benzetimini yapmak için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c7978-105">This tutorial shows you how to use the Raspberry Pi 3 to simulate temperature and humidity data to send to the cloud.</span></span> <span data-ttu-id="c7978-106">Öğretici kullanır:</span><span class="sxs-lookup"><span data-stu-id="c7978-106">The tutorial uses:</span></span>

- <span data-ttu-id="c7978-107">Raspbian işletim sistemi, C programlama dili ve C için Microsoft Azure IOT SDK'sı bir örnek aygıt uygulamak için.</span><span class="sxs-lookup"><span data-stu-id="c7978-107">Raspbian OS, the C programming language, and the Microsoft Azure IoT SDK for C to implement a sample device.</span></span>
- <span data-ttu-id="c7978-108">IOT paketi Uzaktan izleme çözümü bulut tabanlı arka uç önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="c7978-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="c7978-109">Uzaktan izleme çözümü Azure aboneliğinizde Azure Hizmetleri kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="c7978-109">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="c7978-110">Dağıtım gerçek Kurumsal Mimarisi yansıtır.</span><span class="sxs-lookup"><span data-stu-id="c7978-110">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="c7978-111">Gereksiz Azure tüketim ücretleri önlemek için kendisiyle tamamladığınızda azureiotsuite.com önceden yapılandırılmış çözüm örneğiniz silin.</span><span class="sxs-lookup"><span data-stu-id="c7978-111">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="c7978-112">Önceden yapılandırılmış çözümü yeniden gerekiyorsa, kolayca yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7978-112">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="c7978-113">Uzaktan izleme çözümü çalışırken tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="c7978-113">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="c7978-114">İndirme ve örnek yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c7978-114">Download and configure the sample</span></span>

<span data-ttu-id="c7978-115">Şimdi, indirin ve Uzaktan izleme istemci uygulaması, Raspberry Pi'yi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c7978-115">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-the-repositories"></a><span data-ttu-id="c7978-116">Depoları kopyalama</span><span class="sxs-lookup"><span data-stu-id="c7978-116">Clone the repositories</span></span>

<span data-ttu-id="c7978-117">Zaten yapmadıysanız, bir terminal, Pi üzerinde aşağıdaki komutları çalıştırarak gerekli depoları kopyalama:</span><span class="sxs-lookup"><span data-stu-id="c7978-117">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="c7978-118">Güncelleştirme cihaz bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="c7978-118">Update the device connection string</span></span>

<span data-ttu-id="c7978-119">Örnek kaynak dosyasında açma **nano** Düzenleyicisi aşağıdaki komutu kullanarak:</span><span class="sxs-lookup"><span data-stu-id="c7978-119">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="c7978-120">Aşağıdaki satırları bulun:</span><span class="sxs-lookup"><span data-stu-id="c7978-120">Locate the following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="c7978-121">Aygıt ve oluşturulan ve bu öğreticinin başlangıcında kaydedilen IOT hub'ı bilgi yer tutucu değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c7978-121">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="c7978-122">Değişikliklerinizi kaydetmek (**Ctrl-O**, **Enter**) ve düzenleyiciden çıkın (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="c7978-122">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="build-the-sample"></a><span data-ttu-id="c7978-123">Örnek oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7978-123">Build the sample</span></span>

<span data-ttu-id="c7978-124">Önkoşul, bir terminal Raspberry Pi'yi üzerinde aşağıdaki komutları çalıştırarak, C için Microsoft Azure IOT cihaz SDK yükleyin:</span><span class="sxs-lookup"><span data-stu-id="c7978-124">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by running the following commands in a terminal on the Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="c7978-125">Bu gibi durumlarda, güncelleştirilmiş örnek çözümü şimdi Raspberry Pi'yi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c7978-125">You can now build the updated sample solution on the Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
```

<span data-ttu-id="c7978-126">Örnek program Raspberry Pi'yi şimdi çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7978-126">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="c7978-127">Aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="c7978-127">Enter the command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="c7978-128">Aşağıdaki örnek çıkış Raspberry Pi'yi komut satırına bakın çıkış örneğidir:</span><span class="sxs-lookup"><span data-stu-id="c7978-128">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Böğürtlenli Pi uygulamadan çıktı][img-raspberry-output]

<span data-ttu-id="c7978-130">Tuşuna **Ctrl-C** herhangi bir zamanda programı'ndan çıkmak için.</span><span class="sxs-lookup"><span data-stu-id="c7978-130">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="c7978-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c7978-131">Next steps</span></span>

<span data-ttu-id="c7978-132">Ziyaret [Azure IOT Geliştirme Merkezi](https://azure.microsoft.com/develop/iot/) daha fazla örnekleri ve Azure IOT belgeler.</span><span class="sxs-lookup"><span data-stu-id="c7978-132">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-simulator/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
