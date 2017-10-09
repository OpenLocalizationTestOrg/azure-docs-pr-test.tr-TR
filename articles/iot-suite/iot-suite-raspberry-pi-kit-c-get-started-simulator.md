---
title: aaaConnect Raspberry Pi'yi tooAzure IOT paketi C ile sanal telemetriyi kullanarak | Microsoft Docs
description: "Microsoft Azure IOT Starter Kit Merhaba hello Raspberry Pi 3 ve Azure IOT paketi kullanır. Uzaktan izleme çözümü, Raspberry Pi'yi toohello C tooconnect kullanmak, sanal telemetriyi toohello bulut gönderebilir ve hello çözüm panodan çağrılan toomethods yanıtlayabilir."
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
ms.openlocfilehash: 3c4fa43b381385d1a7896cada34aa3aa0b8e5fb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-c"></a><span data-ttu-id="8ea50-104">Uzaktan izleme çözümü, Raspberry Pi 3 toohello bağlanmak ve C kullanarak sanal telemetriyi Gönder</span><span class="sxs-lookup"><span data-stu-id="8ea50-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send simulated telemetry using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="8ea50-105">Bu öğretici nasıl toouse hello Raspberry Pi 3 toosimulate sıcaklık ve nem veri toosend toohello bulut gösterir.</span><span class="sxs-lookup"><span data-stu-id="8ea50-105">This tutorial shows you how toouse hello Raspberry Pi 3 toosimulate temperature and humidity data toosend toohello cloud.</span></span> <span data-ttu-id="8ea50-106">Merhaba öğretici kullanır:</span><span class="sxs-lookup"><span data-stu-id="8ea50-106">hello tutorial uses:</span></span>

- <span data-ttu-id="8ea50-107">Raspbian işletim sistemi, hello C programlama dili ve C tooimplement örnek cihaz için Microsoft Azure IOT SDK'sı hello.</span><span class="sxs-lookup"><span data-stu-id="8ea50-107">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
- <span data-ttu-id="8ea50-108">Merhaba IOT paketi Uzaktan izleme çözümü hello bulut tabanlı arka uç önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="8ea50-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="8ea50-109">Uzaktan izleme çözümü hükümleri Azure aboneliğinizde Azure Hizmetleri kümesi hello.</span><span class="sxs-lookup"><span data-stu-id="8ea50-109">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="8ea50-110">Merhaba dağıtım gerçek Kurumsal Mimarisi yansıtır.</span><span class="sxs-lookup"><span data-stu-id="8ea50-110">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="8ea50-111">tooavoid gereksiz Azure tüketim ücretleri, kendisiyle tamamladığınızda azureiotsuite.com hello önceden yapılandırılmış çözüm örneğiniz silin.</span><span class="sxs-lookup"><span data-stu-id="8ea50-111">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="8ea50-112">Önceden yapılandırılmış çözümü yeniden hello varsa, kolayca yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ea50-112">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="8ea50-113">Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="8ea50-113">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="8ea50-114">İndirme ve hello örnek yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8ea50-114">Download and configure hello sample</span></span>

<span data-ttu-id="8ea50-115">Şimdi, indirin ve, Raspberry Pi'yi Merhaba Uzaktan izleme istemci uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8ea50-115">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="8ea50-116">Kopya hello depoları</span><span class="sxs-lookup"><span data-stu-id="8ea50-116">Clone hello repositories</span></span>

<span data-ttu-id="8ea50-117">Zaten yapmadıysanız, bir terminal komutlarda, Pi üzerinde aşağıdaki çalıştırarak depoları hello kopya hello gerekli:</span><span class="sxs-lookup"><span data-stu-id="8ea50-117">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="8ea50-118">Merhaba cihaz bağlantı dizesi güncelleştir</span><span class="sxs-lookup"><span data-stu-id="8ea50-118">Update hello device connection string</span></span>

<span data-ttu-id="8ea50-119">Açık hello örnek kaynak dosyasına hello **nano** Düzenleyici'yi komutu aşağıdaki hello kullanma:</span><span class="sxs-lookup"><span data-stu-id="8ea50-119">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="8ea50-120">Satırlardan hello bulun:</span><span class="sxs-lookup"><span data-stu-id="8ea50-120">Locate hello following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="8ea50-121">Merhaba cihaz ve oluşturulan ve bu öğreticinin hello başlangıcında kaydedilen IOT Hub bilgileri ile Merhaba yer tutucu değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8ea50-121">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="8ea50-122">Değişikliklerinizi kaydetmek (**Ctrl-O**, **Enter**) ve çıkış hello Düzenleyicisi'ni (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="8ea50-122">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="8ea50-123">Merhaba örnek oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ea50-123">Build hello sample</span></span>

<span data-ttu-id="8ea50-124">Hello önkoşul hello Microsoft Azure IOT cihaz SDK'sı için bir terminal komutlarda Raspberry Pi'yi hello üzerinde aşağıdaki hello çalıştırarak için C yükleyin:</span><span class="sxs-lookup"><span data-stu-id="8ea50-124">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="8ea50-125">Bu gibi durumlarda, güncelleştirilmiş hello örnek çözümü şimdi Raspberry Pi'yi hello üzerinde oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8ea50-125">You can now build hello updated sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
```

<span data-ttu-id="8ea50-126">Bu gibi durumlarda, hello örnek programı şimdi Raspberry Pi'yi hello üzerinde çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ea50-126">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="8ea50-127">Merhaba komutu girin:</span><span class="sxs-lookup"><span data-stu-id="8ea50-127">Enter hello command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="8ea50-128">Merhaba aşağıdaki örnek çıkış hello komut isteminde hello Raspberry Pi'yi gördüğünüz hello çıkış örneğidir:</span><span class="sxs-lookup"><span data-stu-id="8ea50-128">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Böğürtlenli Pi uygulamadan çıktı][img-raspberry-output]

<span data-ttu-id="8ea50-130">Tuşuna **Ctrl-C** tooexit hello program herhangi bir zamanda.</span><span class="sxs-lookup"><span data-stu-id="8ea50-130">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="8ea50-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8ea50-131">Next steps</span></span>

<span data-ttu-id="8ea50-132">Merhaba ziyaret [Azure IOT Geliştirme Merkezi](https://azure.microsoft.com/develop/iot/) daha fazla örnekleri ve Azure IOT belgeler.</span><span class="sxs-lookup"><span data-stu-id="8ea50-132">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-simulator/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
