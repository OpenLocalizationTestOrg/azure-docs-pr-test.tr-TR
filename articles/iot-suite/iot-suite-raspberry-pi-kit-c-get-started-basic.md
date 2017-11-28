---
title: "aaaConnect Raspberry Pi'yi tooAzure IOT paketi ile gerçek algılayıcılar C kullanarak | Microsoft Docs"
description: "Microsoft Azure IOT Starter Kit Merhaba hello Raspberry Pi 3 ve Azure IOT paketi kullanır. Uzaktan izleme çözümü, Raspberry Pi'yi toohello C tooconnect kullanın, telemetri algılayıcı toohello bulut göndermek ve hello çözüm panodan çağrılan toomethods yanıt."
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
ms.openlocfilehash: 7dac55ae5fde4c6f8e3ea6a7debf9a6822dc07ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-c"></a><span data-ttu-id="c04e3-104">Uzaktan izleme çözümü, Raspberry Pi 3 toohello bağlanmak ve C kullanarak gerçek algılayıcı telemetri Gönder</span><span class="sxs-lookup"><span data-stu-id="c04e3-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send telemetry from a real sensor using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="c04e3-105">Bu öğretici nasıl toouse hello Microsoft Azure IOT Starter Kit Raspberry Pi 3 toodevelop hello bulut ile iletişim kurabilen bir sıcaklık ve nem okuyucu gösterir.</span><span class="sxs-lookup"><span data-stu-id="c04e3-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 toodevelop a temperature and humidity reader that can communicate with hello cloud.</span></span> <span data-ttu-id="c04e3-106">Merhaba öğretici kullanır:</span><span class="sxs-lookup"><span data-stu-id="c04e3-106">hello tutorial uses:</span></span>

- <span data-ttu-id="c04e3-107">Raspbian işletim sistemi, hello C programlama dili ve C tooimplement örnek cihaz için Microsoft Azure IOT SDK'sı hello.</span><span class="sxs-lookup"><span data-stu-id="c04e3-107">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
- <span data-ttu-id="c04e3-108">Merhaba IOT paketi Uzaktan izleme çözümü hello bulut tabanlı arka uç önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="c04e3-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="c04e3-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c04e3-109">Overview</span></span>

<span data-ttu-id="c04e3-110">Bu öğreticide, hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="c04e3-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="c04e3-111">Merhaba Uzaktan izleme önceden yapılandırılmış çözüm tooyour Azure aboneliği örneği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="c04e3-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="c04e3-112">Bu adım, otomatik olarak dağıtır ve birden çok Azure hizmetlerini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="c04e3-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="c04e3-113">Aygıt ve algılayıcılar toocommunicate bilgisayarınızın ve hello ile Uzaktan izleme çözümü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c04e3-113">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="c04e3-114">Merhaba örnek aygıt kodu tooconnect toohello Uzaktan izleme çözümü güncelleştirin ve hello çözüm panosunda görüntüleyebilirsiniz telemetri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="c04e3-114">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="c04e3-115">Uzaktan izleme çözümü hükümleri Azure aboneliğinizde Azure Hizmetleri kümesi hello.</span><span class="sxs-lookup"><span data-stu-id="c04e3-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="c04e3-116">Merhaba dağıtım gerçek Kurumsal Mimarisi yansıtır.</span><span class="sxs-lookup"><span data-stu-id="c04e3-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="c04e3-117">tooavoid gereksiz Azure tüketim ücretleri, kendisiyle tamamladığınızda azureiotsuite.com hello önceden yapılandırılmış çözüm örneğiniz silin.</span><span class="sxs-lookup"><span data-stu-id="c04e3-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="c04e3-118">Önceden yapılandırılmış çözümü yeniden hello varsa, kolayca yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c04e3-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="c04e3-119">Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="c04e3-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="c04e3-120">İndirme ve hello örnek yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c04e3-120">Download and configure hello sample</span></span>

<span data-ttu-id="c04e3-121">Şimdi, indirin ve, Raspberry Pi'yi Merhaba Uzaktan izleme istemci uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c04e3-121">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="c04e3-122">Kopya hello depoları</span><span class="sxs-lookup"><span data-stu-id="c04e3-122">Clone hello repositories</span></span>

<span data-ttu-id="c04e3-123">Zaten yapmadıysanız, bir terminal komutlarda, Pi üzerinde aşağıdaki çalıştırarak depoları hello kopya hello gerekli:</span><span class="sxs-lookup"><span data-stu-id="c04e3-123">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
git clone --recursive https://github.com/WiringPi/WiringPi.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="c04e3-124">Merhaba cihaz bağlantı dizesi güncelleştir</span><span class="sxs-lookup"><span data-stu-id="c04e3-124">Update hello device connection string</span></span>

<span data-ttu-id="c04e3-125">Açık hello örnek kaynak dosyasına hello **nano** Düzenleyici'yi komutu aşağıdaki hello kullanma:</span><span class="sxs-lookup"><span data-stu-id="c04e3-125">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="c04e3-126">Satırlardan hello bulun:</span><span class="sxs-lookup"><span data-stu-id="c04e3-126">Locate hello following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="c04e3-127">Merhaba cihaz ve oluşturulan ve bu öğreticinin hello başlangıcında kaydedilen IOT Hub bilgileri ile Merhaba yer tutucu değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c04e3-127">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="c04e3-128">Değişikliklerinizi kaydetmek (**Ctrl-O**, **Enter**) ve çıkış hello Düzenleyicisi'ni (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="c04e3-128">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="c04e3-129">Merhaba örnek oluşturma</span><span class="sxs-lookup"><span data-stu-id="c04e3-129">Build hello sample</span></span>

<span data-ttu-id="c04e3-130">Hello önkoşul hello Microsoft Azure IOT cihaz SDK'sı için bir terminal komutlarda Raspberry Pi'yi hello üzerinde aşağıdaki hello çalıştırarak için C yükleyin:</span><span class="sxs-lookup"><span data-stu-id="c04e3-130">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="c04e3-131">Bu gibi durumlarda, güncelleştirilmiş hello örnek çözümü şimdi Raspberry Pi'yi hello üzerinde oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c04e3-131">You can now build hello updated sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
```

<span data-ttu-id="c04e3-132">Bu gibi durumlarda, hello örnek programı şimdi Raspberry Pi'yi hello üzerinde çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c04e3-132">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="c04e3-133">Merhaba komutu girin:</span><span class="sxs-lookup"><span data-stu-id="c04e3-133">Enter hello command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="c04e3-134">Merhaba aşağıdaki örnek çıkış hello komut isteminde hello Raspberry Pi'yi gördüğünüz hello çıkış örneğidir:</span><span class="sxs-lookup"><span data-stu-id="c04e3-134">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Böğürtlenli Pi uygulamadan çıktı][img-raspberry-output]

<span data-ttu-id="c04e3-136">Tuşuna **Ctrl-C** tooexit hello program herhangi bir zamanda.</span><span class="sxs-lookup"><span data-stu-id="c04e3-136">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="c04e3-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c04e3-137">Next steps</span></span>

<span data-ttu-id="c04e3-138">Merhaba ziyaret [Azure IOT Geliştirme Merkezi](https://azure.microsoft.com/develop/iot/) daha fazla örnekleri ve Azure IOT belgeler.</span><span class="sxs-lookup"><span data-stu-id="c04e3-138">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-basic/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
