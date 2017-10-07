---
title: "ağ geçidi tooAzure IOT paketi kullanarak bir Intel NUC aaaConnect | Microsoft Docs"
description: "Merhaba Microsoft IOT ticari ağ geçidi Seti ve hello Uzaktan izleme önceden yapılandırılmış çözümü kullanın. Hello Azure IOT sınır ağ geçidi tooenable bir SensorTag aygıt tooconnect toohello Uzaktan izleme çözümü kullanın, telemetri toohello bulut gönderebilir ve hello çözüm panodan çağrılan toomethods yanıtlayabilir."
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
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 6f98ee3c1e2311a8644da9d72d40e671e7cbcf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a><span data-ttu-id="e6f78-104">Uzaktan izleme çözümü, Azure IOT sınır ağ geçidi toohello bağlanmak ve SensorTag telemetri Gönder</span><span class="sxs-lookup"><span data-stu-id="e6f78-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send telemetry from a SensorTag</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="e6f78-105">Bu öğretici nasıl çözüm toouse SensorTag aygıt toohello Uzaktan izleme Azure IOT kenar toosend sıcaklık ve nem verileri önceden yapılandırılmış gösterir.</span><span class="sxs-lookup"><span data-stu-id="e6f78-105">This tutorial shows you how toouse Azure IoT Edge toosend temperature and humidity data from SensorTag device toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="e6f78-106">Merhaba SensorTag toohello Intel NUC ağ geçidi Bluetooth kullanarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="e6f78-106">hello SensorTag connects toohello Intel NUC gateway using Bluetooth.</span></span> <span data-ttu-id="e6f78-107">Merhaba öğretici kullanır:</span><span class="sxs-lookup"><span data-stu-id="e6f78-107">hello tutorial uses:</span></span>

- <span data-ttu-id="e6f78-108">Azure IOT kenar tooimplement bir örnek ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="e6f78-108">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="e6f78-109">Merhaba IOT paketi Uzaktan izleme çözümü hello bulut tabanlı arka uç önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="e6f78-109">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="e6f78-110">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e6f78-110">Overview</span></span>

<span data-ttu-id="e6f78-111">Bu öğreticide, hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="e6f78-111">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="e6f78-112">Merhaba Uzaktan izleme önceden yapılandırılmış çözüm tooyour Azure aboneliği örneği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="e6f78-112">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="e6f78-113">Bu adım, otomatik olarak dağıtır ve birden çok Azure hizmetlerini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="e6f78-113">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="e6f78-114">Intel NUC ağ geçidi aygıtı toocommunicate bilgisayarınızın ve hello Uzaktan izleme çözümü ile ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e6f78-114">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="e6f78-115">Intel NUC ağ geçidi tooreceive telemetrinize SensorTag aygıttan ayarlamak ve toohello Uzaktan izleme Panosu gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f78-115">Set up your Intel NUC gateway tooreceive telemetry from a SensorTag device and send it toohello remote monitoring dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

<span data-ttu-id="e6f78-116">[Texas Instruments bırak SensorTag][lnk-sensortag].</span><span class="sxs-lookup"><span data-stu-id="e6f78-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span></span> <span data-ttu-id="e6f78-117">Bu öğretici, hello SensorTag Aygıttan Bluetooth üzerinden telemetri verilerini alır.</span><span class="sxs-lookup"><span data-stu-id="e6f78-117">This tutorial retrieves telemetry data over Bluetooth from hello SensorTag device.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="e6f78-118">Uzaktan izleme çözümü hükümleri Azure aboneliğinizde Azure Hizmetleri kümesi hello.</span><span class="sxs-lookup"><span data-stu-id="e6f78-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="e6f78-119">Merhaba dağıtım gerçek Kurumsal Mimarisi yansıtır.</span><span class="sxs-lookup"><span data-stu-id="e6f78-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="e6f78-120">tooavoid gereksiz Azure tüketim ücretleri, kendisiyle tamamladığınızda azureiotsuite.com hello önceden yapılandırılmış çözüm örneğiniz silin.</span><span class="sxs-lookup"><span data-stu-id="e6f78-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="e6f78-121">Önceden yapılandırılmış çözümü yeniden hello varsa, kolayca yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f78-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="e6f78-122">Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="e6f78-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a><span data-ttu-id="e6f78-123">Bluetooth bağlantısını yapılandır</span><span class="sxs-lookup"><span data-stu-id="e6f78-123">Configure Bluetooth connectivity</span></span>

<span data-ttu-id="e6f78-124">Bluetooth hello Intel NUC tooenable hello SensorTag aygıt tooconnect üzerinde yapılandırın ve telemetri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="e6f78-124">Configure Bluetooth on hello Intel NUC tooenable hello SensorTag device tooconnect and send telemetry.</span></span>

### <a name="find-hello-mac-address-of-hello-sensortag"></a><span data-ttu-id="e6f78-125">Merhaba SensorTag Hello MAC adresini Bul</span><span class="sxs-lookup"><span data-stu-id="e6f78-125">Find hello MAC address of hello SensorTag</span></span>

1. <span data-ttu-id="e6f78-126">Merhaba Intel NUC üzerinde Hello Kabuğu'nda komut toounblock hello Bluetooth hizmeti aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e6f78-126">In hello shell on hello Intel NUC, run hello following command toounblock hello Bluetooth service:</span></span>

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. <span data-ttu-id="e6f78-127">Çalışma hello aşağıdaki toostart hello Bluetooth hello Intel NUC hizmette komutları ve hello Bluetooth Kabuk girin:</span><span class="sxs-lookup"><span data-stu-id="e6f78-127">Run hello following commands toostart hello Bluetooth service on hello Intel NUC and enter hello Bluetooth shell:</span></span>

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="e6f78-128">Komut toopower hello Bluetooth denetleyicisinde aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e6f78-128">Run hello following command toopower on hello Bluetooth controller:</span></span>

    ```bash
    power on
    ```

    <span data-ttu-id="e6f78-129">Merhaba denetleyicisi açık olduğunda, bir ileti görür **güç değiştirme başarılı**.</span><span class="sxs-lookup"><span data-stu-id="e6f78-129">When hello controller is on, you see a message **Changing power on succeeded**.</span></span>

1. <span data-ttu-id="e6f78-130">Bluetooth cihazları yakındaki komutu tooscan için aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e6f78-130">Run hello following command tooscan for nearby Bluetooth devices:</span></span>

    ```bash
    scan on
    ```

1. <span data-ttu-id="e6f78-131">Tuşuna hello güç düğmesine hello SensorTag toomake üzerinde onu bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="e6f78-131">Press hello power button on hello SensorTag toomake it discoverable.</span></span> <span data-ttu-id="e6f78-132">Merhaba yeşil ışığı yanıp sönen.</span><span class="sxs-lookup"><span data-stu-id="e6f78-132">hello green LED flashes.</span></span>

1. <span data-ttu-id="e6f78-133">Merhaba Kabuğu'nda bir ileti görüntülendiğinde bu hello denetleyicisi hello SensorTag bulduğunda, hello hello aygıtın MAC adresini not edin.</span><span class="sxs-lookup"><span data-stu-id="e6f78-133">When you see a message in hello shell that hello controller has discovered hello SensorTag, make a note of hello MAC address of hello device.</span></span> <span data-ttu-id="e6f78-134">Merhaba MAC adresi arar gibi **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="e6f78-134">hello MAC address looks like **A0:E6:F8:B5:F6:00**.</span></span> <span data-ttu-id="e6f78-135">Merhaba ağ geçidi yapılandırdığınızda, daha sonra hello öğreticide hello MAC adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6f78-135">You need hello MAC address later in hello tutorial when you configure hello gateway.</span></span>

1. <span data-ttu-id="e6f78-136">Bluetooth tarama kapalı komutu tooturn aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e6f78-136">Run hello following command tooturn off Bluetooth scanning:</span></span>

    ```bash
    scan off
    ```

1. <span data-ttu-id="e6f78-137">Komut tooverify toohello SensorTag cihazın bağlanabilmesi için aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e6f78-137">Run hello following command tooverify that you can connect toohello SensorTag device:</span></span>

    ```bash
    connect <SensorTag MAC address>
    ```

    <span data-ttu-id="e6f78-138">Başarıyla bağlanıyorsanız, selamlama iletisine hello Kabuk gösterir **bağlantı başarılı** ve hello SensorTag aygıt hakkındaki bilgileri yazdırır.</span><span class="sxs-lookup"><span data-stu-id="e6f78-138">If you connect successfully, hello shell shows hello message **Connection successful** and prints information about hello SensorTag device.</span></span> <span data-ttu-id="e6f78-139">Bağlanamıyorsanız, SensorTag hala açık olduğundan hello denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e6f78-139">If you cannot connect, check hello SensorTag is still powered on.</span></span>

1. <span data-ttu-id="e6f78-140">Şimdi SensorTag hello çıkarın ve hello aşağıdaki komutları çalıştırarak hello Bluetooth kabuktan çıkış:</span><span class="sxs-lookup"><span data-stu-id="e6f78-140">You can now disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="e6f78-141">Merhaba özel IOT kenar modülü oluşturmak</span><span class="sxs-lookup"><span data-stu-id="e6f78-141">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="e6f78-142">Şimdi hello ağ geçidi toosend iletileri toohello Uzaktan izleme çözümü sağlayan hello özel IOT kenar modülü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f78-142">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="e6f78-143">Bir ağ geçidi ve IOT kenar modülleri yapılandırma hakkında daha fazla bilgi için bkz: [Azure IOT kenar kavramları][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="e6f78-143">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="e6f78-144">Merhaba kaynak kodu hello özel IOT kenar modülleri için aşağıdaki komutları hello kullanarak Github'dan indirin:</span><span class="sxs-lookup"><span data-stu-id="e6f78-144">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="e6f78-145">Hello hello aşağıdaki komutları kullanarak özel IOT kenar modülü oluşturun:</span><span class="sxs-lookup"><span data-stu-id="e6f78-145">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="e6f78-146">Merhaba derleme betiğindeki hello libsensor2remotemonitoring.so özel IOT kenar modülü hello yapı klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="e6f78-146">hello build script places hello libsensor2remotemonitoring.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="e6f78-147">Yapılandırma ve hello IOT sınır ağ geçidi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e6f78-147">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="e6f78-148">Merhaba IOT sınır ağ geçidi toosend telemetri, SensorTag aygıt tooyour Uzaktan izleme Panosu artık yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f78-148">You can now configure hello IoT Edge gateway toosend telemetry from your SensorTag device tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="e6f78-149">Bir ağ geçidi ve IOT kenar modülleri yapılandırma hakkında daha fazla bilgi için bkz: [Azure IOT kenar kavramları][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="e6f78-149">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="e6f78-150">Bu öğreticide kullandığınız hello standart `vi` hello Intel NUC üzerindeki metin düzenleyici.</span><span class="sxs-lookup"><span data-stu-id="e6f78-150">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="e6f78-151">Değil kullandıysanız `vi` önce bir giriş öğretici gibi tamamlanmalıdır [UNIX - VI hello Düzenleyicisi Öğreticisi] [ lnk-vi-tutorial] toofamiliarize kendiniz bu düzenleyici ile.</span><span class="sxs-lookup"><span data-stu-id="e6f78-151">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="e6f78-152">Alternatif olarak, daha kullanıcı dostu hello yükleyebilirsiniz [nano](https://www.nano-editor.org/) hello komutunu kullanarak Düzenleyicisi `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="e6f78-152">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="e6f78-153">Merhaba açık hello örnek yapılandırma dosyasında **VI** Düzenleyici'yi komutu aşağıdaki hello kullanma:</span><span class="sxs-lookup"><span data-stu-id="e6f78-153">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

<span data-ttu-id="e6f78-154">Merhaba Iothub modülü hello yapılandırmasında satırlardan hello bulun:</span><span class="sxs-lookup"><span data-stu-id="e6f78-154">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="e6f78-155">Bu öğretici hello oluşturup hello kaydettiğiniz IOT hub'ı bilgi değerlerle Başlat hello yer tutucu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e6f78-155">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="e6f78-156">IoTHubName Hello değeri arar gibi **yourrmsolution37e08**, ve IoTSuffix hello değeri genellikle **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="e6f78-156">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="e6f78-157">Merhaba eşleme modülü hello yapılandırmasında satırlardan hello bulun:</span><span class="sxs-lookup"><span data-stu-id="e6f78-157">Locate hello following lines in hello configuration for hello mapping module:</span></span>

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="e6f78-158">Hello yerine **macAddress** yer tutucu hello daha önce not ettiğiniz, SensorTag MAC adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="e6f78-158">Replace hello **macAddress** placeholder with hello MAC address of your SensorTag you noted previously.</span></span> <span data-ttu-id="e6f78-159">Hello yerine **DeviceID** ve **deviceKey** hello kimliklerini ve anahtarlarını hello Uzaktan izleme çözümünde daha önce oluşturduğunuz hello iki cihazlar için yer tutucularını.</span><span class="sxs-lookup"><span data-stu-id="e6f78-159">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="e6f78-160">Merhaba SensorTag modülü hello yapılandırmasında satırlardan hello bulun:</span><span class="sxs-lookup"><span data-stu-id="e6f78-160">Locate hello following lines in hello configuration for hello SensorTag module:</span></span>

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

<span data-ttu-id="e6f78-161">Hello yerine **aygıt\_mac\_adresi** yer tutucu hello daha önce not ettiğiniz, SensorTag MAC adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="e6f78-161">Replace hello **device\_mac\_address** placeholder  with hello MAC address of your SensorTag you noted previously.</span></span>

<span data-ttu-id="e6f78-162">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e6f78-162">Save your changes.</span></span>

<span data-ttu-id="e6f78-163">Şimdi hello ağ geçidi hello aşağıdaki komutları kullanarak da çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e6f78-163">You can now run hello gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

<span data-ttu-id="e6f78-164">Merhaba IOT sınır ağ geçidi Intel NUC hello üzerinde başlatır ve SensorTag toohello Uzaktan izleme çözümü hello telemetri gönderir:</span><span class="sxs-lookup"><span data-stu-id="e6f78-164">hello IoT Edge gateway starts on hello Intel NUC and sends telemetry from hello SensorTag toohello remote monitoring solution:</span></span>

![IOT sınır ağ geçidi SensorTag hello telemetri gönderir][img-telemetry]

<span data-ttu-id="e6f78-166">Tuşuna **Ctrl-C** tooexit hello program herhangi bir zamanda.</span><span class="sxs-lookup"><span data-stu-id="e6f78-166">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="e6f78-167">Görünüm hello telemetri</span><span class="sxs-lookup"><span data-stu-id="e6f78-167">View hello telemetry</span></span>

<span data-ttu-id="e6f78-168">Merhaba ağ geçidi artık SensorTag aygıt toohello Uzaktan izleme çözümü hello telemetri gönderiyor.</span><span class="sxs-lookup"><span data-stu-id="e6f78-168">hello gateway is now sending telemetry from hello SensorTag device toohello remote monitoring solution.</span></span> <span data-ttu-id="e6f78-169">Merhaba telemetri hello çözüm panosunda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f78-169">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="e6f78-170">Merhaba çözüm panodan komutları tooyour SensorTag aygıt hello ağ geçidi üzerinden de gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f78-170">You can also send commands tooyour SensorTag device through hello gateway from hello solution dashboard.</span></span>

- <span data-ttu-id="e6f78-171">Toohello çözüm Panosu gidin.</span><span class="sxs-lookup"><span data-stu-id="e6f78-171">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="e6f78-172">Select hello aygıt hello hello SensorTag temsil eden hello ağ geçidi olarak yapılandırılmış **aygıt tooView** açılır.</span><span class="sxs-lookup"><span data-stu-id="e6f78-172">Select hello device you configured in hello gateway that represents hello SensorTag in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="e6f78-173">Merhaba telemetri hello SensorTag aygıttan hello Panoda görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e6f78-173">hello telemetry from hello SensorTag device displays on hello dashboard.</span></span>

![Merhaba SensorTag cihazlarından telemetri görüntüleme][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="e6f78-175">Merhaba Uzaktan izleme çözümü Azure hesabınızda çalışan bırakırsanız hello çalıştırıldığında için faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="e6f78-175">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="e6f78-176">Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="e6f78-176">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="e6f78-177">Bunu kullanmayı bitirdikten sonra hello önceden yapılandırılmış çözümü Azure hesabınızdan silin.</span><span class="sxs-lookup"><span data-stu-id="e6f78-177">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e6f78-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e6f78-178">Next steps</span></span>

<span data-ttu-id="e6f78-179">Merhaba ziyaret [Azure IOT Geliştirme Merkezi](https://azure.microsoft.com/develop/iot/) daha fazla örnekleri ve Azure IOT belgeler.</span><span class="sxs-lookup"><span data-stu-id="e6f78-179">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started