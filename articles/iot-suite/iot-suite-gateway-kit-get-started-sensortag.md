---
title: "Azure IOT paketi bir Intel NUC kullanarak bir ağ geçidine bağlanmak | Microsoft Docs"
description: "Microsoft IOT ticari ağ geçidi Seti ve önceden yapılandırılmış Uzaktan izleme çözümü kullanın. Azure IOT sınır ağ geçidi SensorTag aygıtını Uzaktan izleme çözümüne bağlama, buluta telemetri göndermesine ve çözüm panodan çağrılan yöntemler yanıtlamak üzere etkinleştirmek için kullanın."
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
ms.openlocfilehash: bda16be1094276fcecef1e708f9d7db307d94a89
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-azure-iot-edge-gateway-to-the-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a><span data-ttu-id="19c4e-104">Önceden yapılandırılmış Uzaktan izleme çözümü, Azure IOT kenar ağ geçidine bağlanmak ve telemetri SensorTag gönderin</span><span class="sxs-lookup"><span data-stu-id="19c4e-104">Connect your Azure IoT Edge gateway to the remote monitoring preconfigured solution and send telemetry from a SensorTag</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="19c4e-105">Bu öğretici, Azure IOT kenar Uzaktan izleme önceden yapılandırılmış çözümü SensorTag aygıttan sıcaklık ve nem veri göndermek için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="19c4e-105">This tutorial shows you how to use Azure IoT Edge to send temperature and humidity data from SensorTag device to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="19c4e-106">SensorTag Intel NUC ağ geçidine Bluetooth kullanarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="19c4e-106">The SensorTag connects to the Intel NUC gateway using Bluetooth.</span></span> <span data-ttu-id="19c4e-107">Öğretici kullanır:</span><span class="sxs-lookup"><span data-stu-id="19c4e-107">The tutorial uses:</span></span>

- <span data-ttu-id="19c4e-108">Bir örnek ağ geçidi uygulamak için Azure IOT kenar.</span><span class="sxs-lookup"><span data-stu-id="19c4e-108">Azure IoT Edge to implement a sample gateway.</span></span>
- <span data-ttu-id="19c4e-109">IOT paketi Uzaktan izleme çözümü bulut tabanlı arka uç önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="19c4e-109">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="19c4e-110">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="19c4e-110">Overview</span></span>

<span data-ttu-id="19c4e-111">Bu öğreticide, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="19c4e-111">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="19c4e-112">Önceden yapılandırılmış Uzaktan izleme çözümü örneği Azure aboneliğinize dağıtın.</span><span class="sxs-lookup"><span data-stu-id="19c4e-112">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="19c4e-113">Bu adım, otomatik olarak dağıtır ve birden çok Azure hizmetlerini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="19c4e-113">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="19c4e-114">Bilgisayarınız ve Uzaktan izleme çözümü ile iletişim kurmak için Intel NUC ağ geçidi aygıtınızı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="19c4e-114">Set up your Intel NUC gateway device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="19c4e-115">Intel NUC ağ geçidiniz SensorTag aygıttan telemetri almasına ve Uzaktan izleme Panosu göndermek için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="19c4e-115">Set up your Intel NUC gateway to receive telemetry from a SensorTag device and send it to the remote monitoring dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

<span data-ttu-id="19c4e-116">[Texas Instruments bırak SensorTag][lnk-sensortag].</span><span class="sxs-lookup"><span data-stu-id="19c4e-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span></span> <span data-ttu-id="19c4e-117">Bu öğretici, SensorTag Aygıttan Bluetooth üzerinden telemetri verilerini alır.</span><span class="sxs-lookup"><span data-stu-id="19c4e-117">This tutorial retrieves telemetry data over Bluetooth from the SensorTag device.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="19c4e-118">Uzaktan izleme çözümü Azure aboneliğinizde Azure Hizmetleri kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="19c4e-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="19c4e-119">Dağıtım gerçek Kurumsal Mimarisi yansıtır.</span><span class="sxs-lookup"><span data-stu-id="19c4e-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="19c4e-120">Gereksiz Azure tüketim ücretleri önlemek için kendisiyle tamamladığınızda azureiotsuite.com önceden yapılandırılmış çözüm örneğiniz silin.</span><span class="sxs-lookup"><span data-stu-id="19c4e-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="19c4e-121">Önceden yapılandırılmış çözümü yeniden gerekiyorsa, kolayca yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19c4e-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="19c4e-122">Uzaktan izleme çözümü çalışırken tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="19c4e-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a><span data-ttu-id="19c4e-123">Bluetooth bağlantısını yapılandır</span><span class="sxs-lookup"><span data-stu-id="19c4e-123">Configure Bluetooth connectivity</span></span>

<span data-ttu-id="19c4e-124">Bluetooth SensorTag aygıtını bağlanmak ve telemetri göndermek üzere etkinleştirmek için Intel NUC üzerinde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="19c4e-124">Configure Bluetooth on the Intel NUC to enable the SensorTag device to connect and send telemetry.</span></span>

### <a name="find-the-mac-address-of-the-sensortag"></a><span data-ttu-id="19c4e-125">SensorTag MAC adresini Bul</span><span class="sxs-lookup"><span data-stu-id="19c4e-125">Find the MAC address of the SensorTag</span></span>

1. <span data-ttu-id="19c4e-126">Intel NUC üzerinde kabuğunda Bluetooth hizmeti engellemesini kaldırmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="19c4e-126">In the shell on the Intel NUC, run the following command to unblock the Bluetooth service:</span></span>

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. <span data-ttu-id="19c4e-127">Intel NUC Bluetooth hizmetini başlatın ve Bluetooth Kabuk girmek için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="19c4e-127">Run the following commands to start the Bluetooth service on the Intel NUC and enter the Bluetooth shell:</span></span>

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="19c4e-128">Aşağıdaki komutu güç Bluetooth denetleyicisinde çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="19c4e-128">Run the following command to power on the Bluetooth controller:</span></span>

    ```bash
    power on
    ```

    <span data-ttu-id="19c4e-129">Denetleyici açık olduğunda, bir ileti görür **güç değiştirme başarılı**.</span><span class="sxs-lookup"><span data-stu-id="19c4e-129">When the controller is on, you see a message **Changing power on succeeded**.</span></span>

1. <span data-ttu-id="19c4e-130">Yakındaki Bluetooth aygıtlarını taramak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="19c4e-130">Run the following command to scan for nearby Bluetooth devices:</span></span>

    ```bash
    scan on
    ```

1. <span data-ttu-id="19c4e-131">Bulunabilir duruma getirmek için SensorTag güç düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="19c4e-131">Press the power button on the SensorTag to make it discoverable.</span></span> <span data-ttu-id="19c4e-132">Yeşil ışığı yanıp sönen.</span><span class="sxs-lookup"><span data-stu-id="19c4e-132">The green LED flashes.</span></span>

1. <span data-ttu-id="19c4e-133">Denetleyici SensorTag buldu Kabuğu'nda bir ileti gördüğünüzde, aygıtın MAC adresini not edin.</span><span class="sxs-lookup"><span data-stu-id="19c4e-133">When you see a message in the shell that the controller has discovered the SensorTag, make a note of the MAC address of the device.</span></span> <span data-ttu-id="19c4e-134">MAC adresi benzer **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="19c4e-134">The MAC address looks like **A0:E6:F8:B5:F6:00**.</span></span> <span data-ttu-id="19c4e-135">Ağ geçidi yapılandırdığınızda öğreticide daha sonra MAC adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="19c4e-135">You need the MAC address later in the tutorial when you configure the gateway.</span></span>

1. <span data-ttu-id="19c4e-136">Bluetooth tarama devre dışı bırakmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="19c4e-136">Run the following command to turn off Bluetooth scanning:</span></span>

    ```bash
    scan off
    ```

1. <span data-ttu-id="19c4e-137">SensorTag cihaza bağlanabildiğini doğrulamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="19c4e-137">Run the following command to verify that you can connect to the SensorTag device:</span></span>

    ```bash
    connect <SensorTag MAC address>
    ```

    <span data-ttu-id="19c4e-138">Başarıyla bağlanıyorsanız, kabuk iletisi gösterir **bağlantı başarılı** ve SensorTag aygıt hakkındaki bilgileri yazdırır.</span><span class="sxs-lookup"><span data-stu-id="19c4e-138">If you connect successfully, the shell shows the message **Connection successful** and prints information about the SensorTag device.</span></span> <span data-ttu-id="19c4e-139">Bağlanamıyorsanız, onay SensorTag hala açık.</span><span class="sxs-lookup"><span data-stu-id="19c4e-139">If you cannot connect, check the SensorTag is still powered on.</span></span>

1. <span data-ttu-id="19c4e-140">Şimdi, SensorTag bağlantısını kesmek ve aşağıdaki komutları çalıştırarak Bluetooth kabuktan çıkış:</span><span class="sxs-lookup"><span data-stu-id="19c4e-140">You can now disconnect from the SensorTag and exit the Bluetooth shell by running the following commands:</span></span>

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-the-custom-iot-edge-module"></a><span data-ttu-id="19c4e-141">Özel IOT kenar modülü oluşturmak</span><span class="sxs-lookup"><span data-stu-id="19c4e-141">Build the custom IoT Edge module</span></span>

<span data-ttu-id="19c4e-142">Şimdi, Uzaktan izleme çözümüne iletileri göndermek ağ geçidi sağlayan özel IOT kenar modülü de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19c4e-142">You can now build the custom IoT Edge module that enables the gateway to send messages to the remote monitoring solution.</span></span> <span data-ttu-id="19c4e-143">Bir ağ geçidi ve IOT kenar modülleri yapılandırma hakkında daha fazla bilgi için bkz: [Azure IOT kenar kavramları][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="19c4e-143">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="19c4e-144">Kaynak kodu özel IOT kenar modülleri için aşağıdaki komutları kullanarak Github'dan yükleyin:</span><span class="sxs-lookup"><span data-stu-id="19c4e-144">Download the source code for the custom IoT Edge modules from GitHub using the following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="19c4e-145">Aşağıdaki komutları kullanarak özel IOT kenar modülü oluşturun:</span><span class="sxs-lookup"><span data-stu-id="19c4e-145">Build the custom IoT Edge module using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="19c4e-146">Derleme betiğinin libsensor2remotemonitoring.so özel IOT kenar modülü oluşturma klasöründe yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="19c4e-146">The build script places the libsensor2remotemonitoring.so custom IoT Edge module in the build folder.</span></span>

## <a name="configure-and-run-the-iot-edge-gateway"></a><span data-ttu-id="19c4e-147">Yapılandırma ve IOT sınır ağ geçidi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="19c4e-147">Configure and run the IoT Edge gateway</span></span>

<span data-ttu-id="19c4e-148">Telemetri, Uzaktan izleme Panosu SensorTag cihazınızdan göndermek için IOT sınır ağ geçidi artık yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19c4e-148">You can now configure the IoT Edge gateway to send telemetry from your SensorTag device to your remote monitoring dashboard.</span></span> <span data-ttu-id="19c4e-149">Bir ağ geçidi ve IOT kenar modülleri yapılandırma hakkında daha fazla bilgi için bkz: [Azure IOT kenar kavramları][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="19c4e-149">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="19c4e-150">Bu öğreticide kullandığınız standart `vi` Intel NUC üzerindeki metin düzenleyici.</span><span class="sxs-lookup"><span data-stu-id="19c4e-150">In this tutorial, you use the standard `vi` text editor on the Intel NUC.</span></span> <span data-ttu-id="19c4e-151">Değil kullandıysanız `vi` önce bir giriş öğretici gibi tamamlanacaksa [UNIX - VI Düzenleyicisi Öğreticisi] [ lnk-vi-tutorial] bu düzenleyicisiyle tanımak için.</span><span class="sxs-lookup"><span data-stu-id="19c4e-151">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - The vi Editor Tutorial][lnk-vi-tutorial] to familiarize yourself with this editor.</span></span> <span data-ttu-id="19c4e-152">Alternatif olarak, daha kullanıcı dostu yükleyebilirsiniz [nano](https://www.nano-editor.org/) komutunu kullanarak Düzenleyicisi `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="19c4e-152">Alternatively, you can install the more user-friendly [nano](https://www.nano-editor.org/) editor using the command `smart install nano -y`.</span></span>

<span data-ttu-id="19c4e-153">Örnek yapılandırma dosyasını açın **VI** Düzenleyicisi aşağıdaki komutu kullanarak:</span><span class="sxs-lookup"><span data-stu-id="19c4e-153">Open the sample configuration file in the **vi** editor using the following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

<span data-ttu-id="19c4e-154">Iothub modülü yapılandırmasında aşağıdaki satırları bulun:</span><span class="sxs-lookup"><span data-stu-id="19c4e-154">Locate the following lines in the configuration for the IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="19c4e-155">Oluşturulan ve bu öğreticinin başlangıcında kaydedilen IOT hub'ı bilgilerle yer tutucu değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="19c4e-155">Replace the placeholder values with the IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="19c4e-156">IoTHubName değeri benzer **yourrmsolution37e08**, ve IoTSuffix değeri genellikle **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="19c4e-156">The value for IoTHubName looks like **yourrmsolution37e08**, and the value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="19c4e-157">Eşleşme modülü yapılandırmasında aşağıdaki satırları bulun:</span><span class="sxs-lookup"><span data-stu-id="19c4e-157">Locate the following lines in the configuration for the mapping module:</span></span>

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="19c4e-158">Değiştir **macAddress** yer tutucu daha önce not ettiğiniz, SensorTag MAC adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="19c4e-158">Replace the **macAddress** placeholder with the MAC address of your SensorTag you noted previously.</span></span> <span data-ttu-id="19c4e-159">Değiştir **DeviceID** ve **deviceKey** kimliklerini ve anahtarlarını Uzaktan izleme çözümünde daha önce oluşturduğunuz iki cihazlar için yer tutucularını.</span><span class="sxs-lookup"><span data-stu-id="19c4e-159">Replace the **deviceID** and **deviceKey** placeholders with the IDs and keys for the two devices you created in the remote monitoring solution previously.</span></span>

<span data-ttu-id="19c4e-160">SensorTag modülü yapılandırmasında aşağıdaki satırları bulun:</span><span class="sxs-lookup"><span data-stu-id="19c4e-160">Locate the following lines in the configuration for the SensorTag module:</span></span>

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

<span data-ttu-id="19c4e-161">Değiştir **aygıt\_mac\_adresi** yer tutucu daha önce not ettiğiniz, SensorTag MAC adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="19c4e-161">Replace the **device\_mac\_address** placeholder  with the MAC address of your SensorTag you noted previously.</span></span>

<span data-ttu-id="19c4e-162">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="19c4e-162">Save your changes.</span></span>

<span data-ttu-id="19c4e-163">Aşağıdaki komutları kullanarak ağ geçidi artık çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="19c4e-163">You can now run the gateway using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

<span data-ttu-id="19c4e-164">IOT sınır ağ geçidi üzerinde Intel NUC başlar ve telemetri SensorTag Uzaktan izleme çözümüne gönderir:</span><span class="sxs-lookup"><span data-stu-id="19c4e-164">The IoT Edge gateway starts on the Intel NUC and sends telemetry from the SensorTag to the remote monitoring solution:</span></span>

![IOT sınır ağ geçidi SensorTag telemetri gönderir][img-telemetry]

<span data-ttu-id="19c4e-166">Tuşuna **Ctrl-C** herhangi bir zamanda programı'ndan çıkmak için.</span><span class="sxs-lookup"><span data-stu-id="19c4e-166">Press **Ctrl-C** to exit the program at any time.</span></span>

## <a name="view-the-telemetry"></a><span data-ttu-id="19c4e-167">Telemetriyi görüntüleyebilir</span><span class="sxs-lookup"><span data-stu-id="19c4e-167">View the telemetry</span></span>

<span data-ttu-id="19c4e-168">Ağ geçidi artık telemetri SensorTag aygıttan Uzaktan izleme çözümüne gönderiyor.</span><span class="sxs-lookup"><span data-stu-id="19c4e-168">The gateway is now sending telemetry from the SensorTag device to the remote monitoring solution.</span></span> <span data-ttu-id="19c4e-169">Çözüm panosunda telemetri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19c4e-169">You can view the telemetry on the solution dashboard.</span></span> <span data-ttu-id="19c4e-170">Ayrıca komutları ağ geçidi üzerinden SensorTag aygıtınıza çözüm panosunda da gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19c4e-170">You can also send commands to your SensorTag device through the gateway from the solution dashboard.</span></span>

- <span data-ttu-id="19c4e-171">Çözüm panosuna gidin.</span><span class="sxs-lookup"><span data-stu-id="19c4e-171">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="19c4e-172">Yapılandırdığınız SensorTag temsil eden ağ geçidi cihazı seçin **cihaz görünümüne** açılır.</span><span class="sxs-lookup"><span data-stu-id="19c4e-172">Select the device you configured in the gateway that represents the SensorTag in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="19c4e-173">SensorTag cihaz telemetrisinden Panoda görüntüler.</span><span class="sxs-lookup"><span data-stu-id="19c4e-173">The telemetry from the SensorTag device displays on the dashboard.</span></span>

![Telemetri SensorTag cihazlarından görüntüleme][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="19c4e-175">Azure hesabınızda çalıştıran uzaktan izleme çözümü bırakırsanız çalıştırıldığında için faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="19c4e-175">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="19c4e-176">Uzaktan izleme çözümü çalışırken tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="19c4e-176">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="19c4e-177">Bunu kullanmayı bitirdikten sonra önceden yapılandırılmış çözümü Azure hesabınızdan silin.</span><span class="sxs-lookup"><span data-stu-id="19c4e-177">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="19c4e-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="19c4e-178">Next steps</span></span>

<span data-ttu-id="19c4e-179">Ziyaret [Azure IOT Geliştirme Merkezi](https://azure.microsoft.com/develop/iot/) daha fazla örnekleri ve Azure IOT belgeler.</span><span class="sxs-lookup"><span data-stu-id="19c4e-179">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started