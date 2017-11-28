---
title: "ağ geçidi tooAzure IOT paketi kullanarak bir Intel NUC aaaConnect | Microsoft Docs"
description: "Merhaba Microsoft IOT ticari ağ geçidi Seti ve hello Uzaktan izleme önceden yapılandırılmış çözümü kullanın. Kullanım hello Azure IOT sınır ağ geçidi tooconnect toohello Uzaktan izleme çözümü, sanal telemetriyi toohello bulut gönderebilir ve toomethods hello çözüm panodan çağrılan yanıtlayabilir."
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
ms.openlocfilehash: 46b545fc21b054191c8f78ace20fc628f839a819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a><span data-ttu-id="c01a6-104">Uzaktan izleme çözümü, Azure IOT sınır ağ geçidi toohello bağlanmak ve sanal telemetriyi Gönder</span><span class="sxs-lookup"><span data-stu-id="c01a6-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send simulated telemetry</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="c01a6-105">Bu öğretici nasıl çözüm toouse Azure IOT kenar toosimulate sıcaklık ve nem toosend toohello Uzaktan izleme verilerini önceden yapılandırılmış gösterir.</span><span class="sxs-lookup"><span data-stu-id="c01a6-105">This tutorial shows you how toouse Azure IoT Edge toosimulate temperature and humidity data toosend toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="c01a6-106">Merhaba öğretici kullanır:</span><span class="sxs-lookup"><span data-stu-id="c01a6-106">hello tutorial uses:</span></span>

- <span data-ttu-id="c01a6-107">Azure IOT kenar tooimplement bir örnek ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="c01a6-107">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="c01a6-108">Merhaba IOT paketi Uzaktan izleme çözümü hello bulut tabanlı arka uç önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="c01a6-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="c01a6-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c01a6-109">Overview</span></span>

<span data-ttu-id="c01a6-110">Bu öğreticide, hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="c01a6-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="c01a6-111">Merhaba Uzaktan izleme önceden yapılandırılmış çözüm tooyour Azure aboneliği örneği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="c01a6-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="c01a6-112">Bu adım, otomatik olarak dağıtır ve birden çok Azure hizmetlerini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="c01a6-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="c01a6-113">Intel NUC ağ geçidi aygıtı toocommunicate bilgisayarınızın ve hello Uzaktan izleme çözümü ile ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c01a6-113">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="c01a6-114">IOT sınır ağ geçidi toosend hello çözüm panosunda görüntüleyebilirsiniz telemetri benzetimli hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c01a6-114">Configure hello IoT Edge gateway toosend simulated telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="c01a6-115">Uzaktan izleme çözümü hükümleri Azure aboneliğinizde Azure Hizmetleri kümesi hello.</span><span class="sxs-lookup"><span data-stu-id="c01a6-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="c01a6-116">Merhaba dağıtım gerçek Kurumsal Mimarisi yansıtır.</span><span class="sxs-lookup"><span data-stu-id="c01a6-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="c01a6-117">tooavoid gereksiz Azure tüketim ücretleri, kendisiyle tamamladığınızda azureiotsuite.com hello önceden yapılandırılmış çözüm örneğiniz silin.</span><span class="sxs-lookup"><span data-stu-id="c01a6-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="c01a6-118">Önceden yapılandırılmış çözümü yeniden hello varsa, kolayca yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c01a6-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="c01a6-119">Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="c01a6-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

<span data-ttu-id="c01a6-120">Bir cihaz kimliği gibi kullanarak ikinci bir cihaz Hello önceki adımları tooadd yineleyin **device02**.</span><span class="sxs-lookup"><span data-stu-id="c01a6-120">Repeat hello previous steps tooadd a second device using a Device ID such as **device02**.</span></span> <span data-ttu-id="c01a6-121">Merhaba örnek verileri iki sanal aygıtlardan hello ağ geçidi toohello Uzaktan izleme çözümünde gönderir.</span><span class="sxs-lookup"><span data-stu-id="c01a6-121">hello sample sends data from two simulated devices in hello gateway toohello remote monitoring solution.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="c01a6-122">Merhaba özel IOT kenar modülü oluşturmak</span><span class="sxs-lookup"><span data-stu-id="c01a6-122">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="c01a6-123">Şimdi hello ağ geçidi toosend iletileri toohello Uzaktan izleme çözümü sağlayan hello özel IOT kenar modülü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c01a6-123">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="c01a6-124">Bir ağ geçidi ve IOT kenar modülleri yapılandırma hakkında daha fazla bilgi için bkz: [Azure IOT kenar kavramları][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="c01a6-124">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="c01a6-125">Merhaba kaynak kodu hello özel IOT kenar modülleri için aşağıdaki komutları hello kullanarak Github'dan indirin:</span><span class="sxs-lookup"><span data-stu-id="c01a6-125">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="c01a6-126">Hello hello aşağıdaki komutları kullanarak özel IOT kenar modülü oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c01a6-126">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="c01a6-127">Merhaba derleme betiğindeki hello libsimulator.so özel IOT kenar modülü hello yapı klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="c01a6-127">hello build script places hello libsimulator.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="c01a6-128">Yapılandırma ve hello IOT sınır ağ geçidi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c01a6-128">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="c01a6-129">Merhaba IOT sınır ağ geçidi toosend sanal telemetriyi tooyour Uzaktan izleme Panosu artık yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c01a6-129">You can now configure hello IoT Edge gateway toosend simulated telemetry tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="c01a6-130">Bir ağ geçidi ve IOT kenar modülleri yapılandırma hakkında daha fazla bilgi için bkz: [Azure IOT kenar kavramları][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="c01a6-130">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="c01a6-131">Bu öğreticide kullandığınız hello standart `vi` hello Intel NUC üzerindeki metin düzenleyici.</span><span class="sxs-lookup"><span data-stu-id="c01a6-131">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="c01a6-132">Değil kullandıysanız `vi` önce bir giriş öğretici gibi tamamlanmalıdır [UNIX - VI hello Düzenleyicisi Öğreticisi] [ lnk-vi-tutorial] toofamiliarize kendiniz bu düzenleyici ile.</span><span class="sxs-lookup"><span data-stu-id="c01a6-132">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="c01a6-133">Alternatif olarak, daha kullanıcı dostu hello yükleyebilirsiniz [nano](https://www.nano-editor.org/) hello komutunu kullanarak Düzenleyicisi `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="c01a6-133">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="c01a6-134">Merhaba açık hello örnek yapılandırma dosyasında **VI** Düzenleyici'yi komutu aşağıdaki hello kullanma:</span><span class="sxs-lookup"><span data-stu-id="c01a6-134">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

<span data-ttu-id="c01a6-135">Merhaba Iothub modülü hello yapılandırmasında satırlardan hello bulun:</span><span class="sxs-lookup"><span data-stu-id="c01a6-135">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="c01a6-136">Bu öğretici hello oluşturup hello kaydettiğiniz IOT hub'ı bilgi değerlerle Başlat hello yer tutucu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c01a6-136">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="c01a6-137">IoTHubName Hello değeri arar gibi **yourrmsolution37e08**, ve IoTSuffix hello değeri genellikle **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="c01a6-137">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="c01a6-138">Merhaba eşleme modülü hello yapılandırmasında satırlardan hello bulun:</span><span class="sxs-lookup"><span data-stu-id="c01a6-138">Locate hello following lines in hello configuration for hello mapping module:</span></span>

```json
args": [
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  },
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="c01a6-139">Hello yerine **DeviceID** ve **deviceKey** hello kimliklerini ve anahtarlarını hello Uzaktan izleme çözümünde daha önce oluşturduğunuz hello iki cihazlar için yer tutucularını.</span><span class="sxs-lookup"><span data-stu-id="c01a6-139">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="c01a6-140">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c01a6-140">Save your changes.</span></span>

<span data-ttu-id="c01a6-141">Şimdi hello aşağıdaki hello kullanarak IOT sınır ağ geçidi komutları çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c01a6-141">You can now run hello IoT Edge gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

<span data-ttu-id="c01a6-142">Merhaba ağ geçidi Intel NUC hello üzerinde başlatır ve sanal telemetriyi toohello Uzaktan izleme çözümü gönderir:</span><span class="sxs-lookup"><span data-stu-id="c01a6-142">hello gateway starts on hello Intel NUC and sends simulated telemetry toohello remote monitoring solution:</span></span>

![IOT sınır ağ geçidi sanal telemetriyi oluşturur][img-simulated telemetry]

<span data-ttu-id="c01a6-144">Tuşuna **Ctrl-C** tooexit hello program herhangi bir zamanda.</span><span class="sxs-lookup"><span data-stu-id="c01a6-144">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="c01a6-145">Görünüm hello telemetri</span><span class="sxs-lookup"><span data-stu-id="c01a6-145">View hello telemetry</span></span>

<span data-ttu-id="c01a6-146">Merhaba IOT sınır ağ geçidi artık sanal telemetriyi toohello Uzaktan izleme çözümü gönderiyor.</span><span class="sxs-lookup"><span data-stu-id="c01a6-146">hello IoT Edge gateway is now sending simulated telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="c01a6-147">Merhaba telemetri hello çözüm panosunda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c01a6-147">You can view hello telemetry on hello solution dashboard.</span></span>

- <span data-ttu-id="c01a6-148">Toohello çözüm Panosu gidin.</span><span class="sxs-lookup"><span data-stu-id="c01a6-148">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="c01a6-149">Hello hello ağ geçidi olarak yapılandırılmış hello iki cihazlar birini **aygıt tooView** açılır.</span><span class="sxs-lookup"><span data-stu-id="c01a6-149">Select one of hello two devices you configured in hello gateway in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="c01a6-150">Merhaba telemetri hello ağ geçidi aygıtlardan hello panosunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c01a6-150">hello telemetry from hello gateway devices displays on hello dashboard.</span></span>

![Telemetri benzetimli hello ağ geçidi aygıtlardan görüntüle][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="c01a6-152">Merhaba Uzaktan izleme çözümü Azure hesabınızda çalışan bırakırsanız hello çalıştırıldığında için faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="c01a6-152">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="c01a6-153">Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="c01a6-153">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="c01a6-154">Bunu kullanmayı bitirdikten sonra hello önceden yapılandırılmış çözümü Azure hesabınızdan silin.</span><span class="sxs-lookup"><span data-stu-id="c01a6-154">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c01a6-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c01a6-155">Next steps</span></span>

<span data-ttu-id="c01a6-156">Merhaba ziyaret [Azure IOT Geliştirme Merkezi](https://azure.microsoft.com/develop/iot/) daha fazla örnekleri ve Azure IOT belgeler.</span><span class="sxs-lookup"><span data-stu-id="c01a6-156">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started