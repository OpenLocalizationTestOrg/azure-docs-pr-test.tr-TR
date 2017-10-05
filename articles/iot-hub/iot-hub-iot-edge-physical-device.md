---
title: "Bir fiziksel aygıt ile Azure IOT kenar kullanın | Microsoft Docs"
description: "Texas Instruments SensorTag aygıt bir IOT hub'ı Raspberry Pi 3 cihazda çalışan IOT sınır ağ geçidi aracılığıyla veri göndermek için nasıl kullanılacağını. Ağ geçidi, Azure IOT kenar kullanılarak oluşturulur."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: 02962a91c739a53dfcf947bcc736e5c293b9384f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-to-forward-device-to-cloud-messages-to-iot-hub"></a><span data-ttu-id="bce2c-104">Azure IOT kenar üzerinde Raspberry Pi'yi IOT Hub'ına cihaz bulut iletilerini iletmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="bce2c-104">Use Azure IoT Edge on a Raspberry Pi to forward device-to-cloud messages to IoT Hub</span></span>

<span data-ttu-id="bce2c-105">Bu kılavuz [Bluetooth düşük enerji örnek] [ lnk-ble-samplecode] nasıl kullanılacağını gösterir [Azure IOT kenar] [ lnk-sdk] için:</span><span class="sxs-lookup"><span data-stu-id="bce2c-105">This walkthrough of the [Bluetooth low energy sample][lnk-ble-samplecode] shows you how to use [Azure IoT Edge][lnk-sdk] to:</span></span>

* <span data-ttu-id="bce2c-106">Cihaz bulut telemetri IOT Hub'ına fiziksel CİHAZDAN iletin.</span><span class="sxs-lookup"><span data-stu-id="bce2c-106">Forward device-to-cloud telemetry to IoT Hub from a physical device.</span></span>
* <span data-ttu-id="bce2c-107">Bir fiziksel aygıt için rota komutları IOT hub'dan.</span><span class="sxs-lookup"><span data-stu-id="bce2c-107">Route commands from IoT Hub to a physical device.</span></span>

<span data-ttu-id="bce2c-108">Bu kılavuzda aşağıdaki konular ele alınmaktadır:</span><span class="sxs-lookup"><span data-stu-id="bce2c-108">This walkthrough covers:</span></span>

* <span data-ttu-id="bce2c-109">**Mimari**: Bluetooth düşük enerji örnek hakkında önemli mimari bilgiler.</span><span class="sxs-lookup"><span data-stu-id="bce2c-109">**Architecture**: important architectural information about the Bluetooth low energy sample.</span></span>
* <span data-ttu-id="bce2c-110">**Derleme ve çalıştırma**: örneği derlemek ve çalıştırmak için gerekli adımlar.</span><span class="sxs-lookup"><span data-stu-id="bce2c-110">**Build and run**: the steps required to build and run the sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="bce2c-111">Mimari</span><span class="sxs-lookup"><span data-stu-id="bce2c-111">Architecture</span></span>

<span data-ttu-id="bce2c-112">İzlenecek yol oluşturun ve IOT sınır ağ geçidi Raspbian Linux çalıştıran bir Raspberry Pi 3 üzerinde çalışmasını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="bce2c-112">The walkthrough shows you how to build and run an IoT Edge gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="bce2c-113">Ağ geçidi IOT kenar kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bce2c-113">The gateway is built using IoT Edge.</span></span> <span data-ttu-id="bce2c-114">Örnek bir Texas Instruments SensorTag Bluetooth düşük enerji (bırak) aygıtı sıcaklık verileri toplamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="bce2c-114">The sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device to collect temperature data.</span></span>

<span data-ttu-id="bce2c-115">IOT sınır ağ geçidi çalıştırdığınızda bu:</span><span class="sxs-lookup"><span data-stu-id="bce2c-115">When you run the IoT Edge gateway it:</span></span>

* <span data-ttu-id="bce2c-116">Bir SensorTag cihazda Bluetooth düşük enerji (bırak) protokolünü kullanarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="bce2c-116">Connects to a SensorTag device using the Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="bce2c-117">IOT Hub HTTP protokolünü kullanarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="bce2c-117">Connects to IoT Hub using the HTTP protocol.</span></span>
* <span data-ttu-id="bce2c-118">Telemetri SensorTag cihazın IOT Hub'ına iletir.</span><span class="sxs-lookup"><span data-stu-id="bce2c-118">Forwards telemetry from the SensorTag device to IoT Hub.</span></span>
* <span data-ttu-id="bce2c-119">IOT hub'ı komutları SensorTag aygıta yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="bce2c-119">Routes commands from IoT Hub to the SensorTag device.</span></span>

<span data-ttu-id="bce2c-120">Ağ geçidi aşağıdaki IOT kenar modüllerini içerir:</span><span class="sxs-lookup"><span data-stu-id="bce2c-120">The gateway contains the following IoT Edge modules:</span></span>

* <span data-ttu-id="bce2c-121">A *bırak Modülü* aygıttan sıcaklık veri almak ve cihaza komut gönderme için bırak aygıtıyla arabirimleri.</span><span class="sxs-lookup"><span data-stu-id="bce2c-121">A *BLE module* that interfaces with a BLE device to receive temperature data from the device and send commands to the device.</span></span>
* <span data-ttu-id="bce2c-122">A *aygıt modülü bırak buluta* bırak yönergeler için içine IOT Hub'ından gönderilen JSON iletileri çevirir *bırak Modülü*.</span><span class="sxs-lookup"><span data-stu-id="bce2c-122">A *BLE cloud to device module* that translates JSON messages sent from IoT Hub into BLE instructions for the *BLE module*.</span></span>
* <span data-ttu-id="bce2c-123">A *Günlükçü Modülü* , tüm ağ geçidi iletilerini yerel bir dosyaya kaydeder.</span><span class="sxs-lookup"><span data-stu-id="bce2c-123">A *logger module* that logs all gateway messages to a local file.</span></span>
* <span data-ttu-id="bce2c-124">Bir *kimlik eşleme Modülü* bırak aygıt MAC adresi ile Azure IOT Hub cihaz kimlikleri arasında çevirir.</span><span class="sxs-lookup"><span data-stu-id="bce2c-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="bce2c-125">Bir *IOT hub'ı Modülü* bir IOT hub'ına telemetri verileri yükler ve IOT hub'ından cihaz komutlarını alır.</span><span class="sxs-lookup"><span data-stu-id="bce2c-125">An *IoT Hub module* that uploads telemetry data to an IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="bce2c-126">A *bırak yazıcı Modülü* bırak cihaz telemetrisinden yorumlar ve baskı siparişi biçimlendirilmiş sorun giderme ve hata ayıklamayı etkinleştirmek için konsola veri.</span><span class="sxs-lookup"><span data-stu-id="bce2c-126">A *BLE printer module* that interprets telemetry from the BLE device and prints formatted data to the console to enable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-the-gateway"></a><span data-ttu-id="bce2c-127">Veri ağ geçidi üzerinden nasıl akar</span><span class="sxs-lookup"><span data-stu-id="bce2c-127">How data flows through the gateway</span></span>

<span data-ttu-id="bce2c-128">Aşağıdaki Blok Diyagramı telemetri karşıya yükleme veri akışı ardışık gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="bce2c-128">The following block diagram illustrates the telemetry upload data flow pipeline:</span></span>

![Telemetri karşıya yükleme ağ geçidi ardışık düzen](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="bce2c-130">IOT Hub'ına bırak aygıttan seyahat öğeyi telemetri götüren adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bce2c-130">The steps that an item of telemetry takes traveling from a BLE device to IoT Hub are:</span></span>

1. <span data-ttu-id="bce2c-131">BIRAK aygıt sıcaklık örnek oluşturur ve ağ geçidi bırak modülünde Bluetooth üzerinden gönderir.</span><span class="sxs-lookup"><span data-stu-id="bce2c-131">The BLE device generates a temperature sample and sends it over Bluetooth to the BLE module in the gateway.</span></span>
1. <span data-ttu-id="bce2c-132">BIRAK modülü örnek alır ve aygıtın MAC adresi birlikte Aracısı yayımlar.</span><span class="sxs-lookup"><span data-stu-id="bce2c-132">The BLE module receives the sample and publishes it to the broker along with the MAC address of the device.</span></span>
1. <span data-ttu-id="bce2c-133">Kimlik eşleme modülü bu iletiyi alır ve bir IOT Hub cihaz kimliği aygıt MAC adresi çevirmek için bir iç tablosunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="bce2c-133">The identity mapping module picks up this message and uses an internal table to translate the MAC address of the device into an IoT Hub device identity.</span></span> <span data-ttu-id="bce2c-134">Bir IOT Hub cihaz kimliği, bir cihaz kimliği ve aygıt anahtarı oluşur.</span><span class="sxs-lookup"><span data-stu-id="bce2c-134">An IoT Hub device identity consists of a device ID and device key.</span></span>
1. <span data-ttu-id="bce2c-135">Kimlik eşleme modülü sıcaklık örnek verileri, cihaz, cihaz kimliği ve aygıt anahtarı MAC adresi içeren yeni bir ileti yayımlar.</span><span class="sxs-lookup"><span data-stu-id="bce2c-135">The identity mapping module publishes a new message that contains the temperature sample data, the MAC address of the device, the device ID, and the device key.</span></span>
1. <span data-ttu-id="bce2c-136">IOT hub'ı Modülü (kimlik eşleme modülü tarafından oluşturulan) bu yeni bir ileti alır ve IOT Hub'ına yayımlar.</span><span class="sxs-lookup"><span data-stu-id="bce2c-136">The IoT Hub module receives this new message (generated by the identity mapping module) and publishes it to IoT Hub.</span></span>
1. <span data-ttu-id="bce2c-137">Günlükçü modülü tüm iletileri Aracısı'ndan yerel bir dosyaya kaydeder.</span><span class="sxs-lookup"><span data-stu-id="bce2c-137">The logger module logs all messages from the broker to a local file.</span></span>

<span data-ttu-id="bce2c-138">Cihaz komutu veri akışı ardışık aşağıdaki blok diyagramını gösterir:</span><span class="sxs-lookup"><span data-stu-id="bce2c-138">The following block diagram illustrates the device command data flow pipeline:</span></span>

![Cihaz komut ağ geçidi ardışık düzeni](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="bce2c-140">IOT hub'ı modülü IOT hub'ı yeni komut iletileri için düzenli aralıklarla yoklar.</span><span class="sxs-lookup"><span data-stu-id="bce2c-140">The IoT Hub module periodically polls the IoT hub for new command messages.</span></span>
1. <span data-ttu-id="bce2c-141">IOT hub'ı modülü yeni bir komut iletisi aldığında, belgeyi broker yayımlar.</span><span class="sxs-lookup"><span data-stu-id="bce2c-141">When the IoT Hub module receives a new command message, it publishes it to the broker.</span></span>
1. <span data-ttu-id="bce2c-142">Kimlik eşleme modülü komutu iletinin seçer ve bir aygıt MAC adresi için IOT Hub cihaz kimliği çevirmek için bir iç tablosunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="bce2c-142">The identity mapping module picks up the command message and uses an internal table to translate the IoT Hub device ID to a device MAC address.</span></span> <span data-ttu-id="bce2c-143">Ardından, ileti özelliklerini eşlemesinde hedef aygıt MAC adresi içeren yeni bir ileti yayımlar.</span><span class="sxs-lookup"><span data-stu-id="bce2c-143">It then publishes a new message that includes the MAC address of the target device in the properties map of the message.</span></span>
1. <span data-ttu-id="bce2c-144">BIRAK bulut-cihaz modülü bu iletiyi alır ve doğru bırak yönerge bırak modülü için çevirir.</span><span class="sxs-lookup"><span data-stu-id="bce2c-144">The BLE Cloud-to-Device module picks up this message and translates it into the proper BLE instruction for the BLE module.</span></span> <span data-ttu-id="bce2c-145">Ardından, yeni bir ileti yayımlar.</span><span class="sxs-lookup"><span data-stu-id="bce2c-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="bce2c-146">BIRAK modülü bu iletiyi alır ve g/ç yönerge bırak aygıtla iletişim kurarak çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="bce2c-146">The BLE module picks up this message and executes the I/O instruction by communicating with the BLE device.</span></span>
1. <span data-ttu-id="bce2c-147">Günlükçü modülü tüm iletileri Aracısı'ndan bir disk dosyasına kaydeder.</span><span class="sxs-lookup"><span data-stu-id="bce2c-147">The logger module logs all messages from the broker to a disk file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bce2c-148">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bce2c-148">Prerequisites</span></span>

<span data-ttu-id="bce2c-149">Bu öğreticiyi tamamlamak için etkin bir Azure aboneliğinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bce2c-149">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="bce2c-150">Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bce2c-150">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="bce2c-151">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="bce2c-151">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

<span data-ttu-id="bce2c-152">Komut satırı Raspberry Pi'yi üzerinde uzaktan erişim sağlamak için Masaüstü makinenizde SSH istemcisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="bce2c-152">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="bce2c-153">Windows, bir SSH istemcisi içermez.</span><span class="sxs-lookup"><span data-stu-id="bce2c-153">Windows does not include an SSH client.</span></span> <span data-ttu-id="bce2c-154">Kullanmanızı öneririz [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="bce2c-154">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="bce2c-155">Çoğu Linux dağıtımları ve Mac OS komut satırı SSH yardımcı programı içerir.</span><span class="sxs-lookup"><span data-stu-id="bce2c-155">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="bce2c-156">Daha fazla bilgi için bkz: [SSH kullanarak Linux veya Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="bce2c-156">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="bce2c-157">Donanımınızın hazırlama</span><span class="sxs-lookup"><span data-stu-id="bce2c-157">Prepare your hardware</span></span>

<span data-ttu-id="bce2c-158">Bu öğreticide kullandığınız varsayılır bir [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) aygıt bağlı Raspbian çalıştıran bir Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="bce2c-158">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected to a Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="bce2c-159">Raspbian yükleyin</span><span class="sxs-lookup"><span data-stu-id="bce2c-159">Install Raspbian</span></span>

<span data-ttu-id="bce2c-160">Raspbian Raspberry Pi 3 aygıtınızda yüklemek için aşağıdaki seçeneklerden birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bce2c-160">You can use either of the following options to install Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="bce2c-161">Raspbian en son sürümünü yüklemek için kullandığınız [NOOBS] [ lnk-noobs] grafik kullanıcı arabirimi.</span><span class="sxs-lookup"><span data-stu-id="bce2c-161">To install the latest version of Raspbian, use the [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="bce2c-162">El ile [karşıdan] [ lnk-raspbian] ve en son Raspbian işletim sistemi görüntüsünü bir SD kartına yazma.</span><span class="sxs-lookup"><span data-stu-id="bce2c-162">Manually [download][lnk-raspbian] and write the latest image of the Raspbian operating system to an SD card.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="bce2c-163">Oturum açma ve terminal erişim</span><span class="sxs-lookup"><span data-stu-id="bce2c-163">Sign in and access the terminal</span></span>

<span data-ttu-id="bce2c-164">Raspberry Pi'yi terminal ortamda erişmek için iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="bce2c-164">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

* <span data-ttu-id="bce2c-165">Klavye ve monitör, Raspberry Pi'yi bağlı varsa, bir terminal penceresi erişmek için Raspbian GUI kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bce2c-165">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

* <span data-ttu-id="bce2c-166">Masaüstü makinenizden SSH kullanarak, Raspberry Pi'yi komut satırında erişin.</span><span class="sxs-lookup"><span data-stu-id="bce2c-166">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="bce2c-167">GUI içinde bir terminal penceresi kullanın</span><span class="sxs-lookup"><span data-stu-id="bce2c-167">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="bce2c-168">Kullanıcı adı Raspbian için varsayılan kimlik bilgileri olan **PI** ve parola **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="bce2c-168">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="bce2c-169">GUI görev çubuğunda, başlatabilirsiniz **Terminal** gibi bir izleyici arar simgesini kullanarak yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="bce2c-169">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="bce2c-170">Oturum SSH oturum</span><span class="sxs-lookup"><span data-stu-id="bce2c-170">Sign in with SSH</span></span>

<span data-ttu-id="bce2c-171">SSH, Raspberry Pi'yi komut satırı erişimi için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bce2c-171">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="bce2c-172">Makaleyi [SSH (Secure Shell)] [ lnk-pi-ssh] , Raspberry Pi'yi SSH yapılandırma ve bağlanması açıklar [Windows] [ lnk-ssh-windows] veya [ Linux ve Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="bce2c-172">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="bce2c-173">Kullanıcı adıyla oturum **PI** ve parola **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="bce2c-173">Sign in with username **pi** and password **raspberry**.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="bce2c-174">BlueZ 5.37 yükleyin</span><span class="sxs-lookup"><span data-stu-id="bce2c-174">Install BlueZ 5.37</span></span>

<span data-ttu-id="bce2c-175">Bluetooth donanım BlueZ yığın aracılığıyla bırak modülleri konuşun.</span><span class="sxs-lookup"><span data-stu-id="bce2c-175">The BLE modules talk to the Bluetooth hardware via the BlueZ stack.</span></span> <span data-ttu-id="bce2c-176">Doğru çalışması için BlueZ modülleri için 5.37 sürümü gerekir.</span><span class="sxs-lookup"><span data-stu-id="bce2c-176">You need version 5.37 of BlueZ for the modules to work correctly.</span></span> <span data-ttu-id="bce2c-177">Bu yönergeleri BlueZ doğru sürümünün yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="bce2c-177">These instructions make sure the correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="bce2c-178">Geçerli bluetooth arka plan programı durdurun:</span><span class="sxs-lookup"><span data-stu-id="bce2c-178">Stop the current bluetooth daemon:</span></span>

    ```sh
    sudo systemctl stop bluetooth
    ```

1. <span data-ttu-id="bce2c-179">BlueZ bağımlılıkları yükler:</span><span class="sxs-lookup"><span data-stu-id="bce2c-179">Install the BlueZ dependencies:</span></span>

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. <span data-ttu-id="bce2c-180">BlueZ kaynak kodu bluez.org yükleyin:</span><span class="sxs-lookup"><span data-stu-id="bce2c-180">Download the BlueZ source code from bluez.org:</span></span>

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="bce2c-181">Kaynak kodu sıkıştırmasını açın:</span><span class="sxs-lookup"><span data-stu-id="bce2c-181">Unzip the source code:</span></span>

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="bce2c-182">Yeni oluşturulan klasöre dizinleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="bce2c-182">Change directories to the newly created folder:</span></span>

    ```sh
    cd bluez-5.37
    ```

1. <span data-ttu-id="bce2c-183">Oluşturulacak BlueZ kod yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="bce2c-183">Configure the BlueZ code to be built:</span></span>

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. <span data-ttu-id="bce2c-184">BlueZ oluşturun:</span><span class="sxs-lookup"><span data-stu-id="bce2c-184">Build BlueZ:</span></span>

    ```sh
    make
    ```

1. <span data-ttu-id="bce2c-185">Bunu yaptıktan sonra BlueZ yükleme oluşturma:</span><span class="sxs-lookup"><span data-stu-id="bce2c-185">Install BlueZ once it is done building:</span></span>

    ```sh
    sudo make install
    ```

1. <span data-ttu-id="bce2c-186">Yeni bluetooth arka plan programı dosyasına işaret şekilde bluetooth systemd hizmet yapılandırmasını değiştirme `/lib/systemd/system/bluetooth.service`.</span><span class="sxs-lookup"><span data-stu-id="bce2c-186">Change systemd service configuration for bluetooth so it points to the new bluetooth daemon in the file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="bce2c-187">'ExecStart' satırın aşağıdaki metinle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="bce2c-187">Replace the 'ExecStart' line with the following text:</span></span>

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-to-the-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="bce2c-188">Bağlantı SensorTag aygıta Raspberry Pi 3 aygıtınızdan etkinleştir</span><span class="sxs-lookup"><span data-stu-id="bce2c-188">Enable connectivity to the SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="bce2c-189">Örneği çalıştırmadan önce Raspberry Pi 3 SensorTag aygıta bağlanabileceği doğrulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bce2c-189">Before running the sample, you need to verify that your Raspberry Pi 3 can connect to the SensorTag device.</span></span>

1. <span data-ttu-id="bce2c-190">Olun `rfkill` yardımcı programı yüklenir:</span><span class="sxs-lookup"><span data-stu-id="bce2c-190">Ensure the `rfkill` utility is installed:</span></span>

    ```sh
    sudo apt-get install rfkill
    ```

1. <span data-ttu-id="bce2c-191">Bluetooth Raspberry Pi 3'te engelini kaldırmak ve sürüm numarasını olup olmadığını denetleyin **5.37**:</span><span class="sxs-lookup"><span data-stu-id="bce2c-191">Unblock bluetooth on the Raspberry Pi 3 and check that the version number is **5.37**:</span></span>

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. <span data-ttu-id="bce2c-192">Etkileşimli bluetooth Kabuk girmek için bluetooth hizmetini başlatın ve yürütme **bluetoothctl** komutu:</span><span class="sxs-lookup"><span data-stu-id="bce2c-192">To enter the interactive bluetooth shell, start the bluetooth service and execute the **bluetoothctl** command :</span></span>

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="bce2c-193">Aşağıdaki komutu girin **güç açma** güç bluetooth denetleyicisi kurmak için.</span><span class="sxs-lookup"><span data-stu-id="bce2c-193">Enter the command **power on** to power up the bluetooth controller.</span></span> <span data-ttu-id="bce2c-194">Komut çıktısı aşağıdakine benzer döndürür:</span><span class="sxs-lookup"><span data-stu-id="bce2c-194">The command returns output similar to the following:</span></span>

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="bce2c-195">Etkileşimli bluetooth Kabuğu'nda komutu girin **taraması** bluetooth cihazları için taramak için.</span><span class="sxs-lookup"><span data-stu-id="bce2c-195">In the interactive bluetooth shell, enter the command **scan on** to scan for bluetooth devices.</span></span> <span data-ttu-id="bce2c-196">Komut çıktısı aşağıdakine benzer döndürür:</span><span class="sxs-lookup"><span data-stu-id="bce2c-196">The command returns output similar to the following:</span></span>

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="bce2c-197">SensorTag aygıt bulunabilir (yeşil LED flash) küçük düğmesine basarak olun.</span><span class="sxs-lookup"><span data-stu-id="bce2c-197">Make the SensorTag device discoverable by pressing the small button (the green LED should flash).</span></span> <span data-ttu-id="bce2c-198">Raspberry Pi 3 SensorTag aygıtı keşfet:</span><span class="sxs-lookup"><span data-stu-id="bce2c-198">The Raspberry Pi 3 should discover the SensorTag device:</span></span>

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="bce2c-199">Bu örnekte, SensorTag aygıt MAC adresi olduğunu görebilirsiniz **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="bce2c-199">In this example, you can see that the MAC address of the SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="bce2c-200">Girerek taramayı kapatabilirsiniz **kapalı tarama** komutu:</span><span class="sxs-lookup"><span data-stu-id="bce2c-200">Turn off scanning by entering the **scan off** command:</span></span>

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="bce2c-201">MAC adresini girerek kullanarak SensorTag Cihazınızı bağlanmak **bağlanmak \<MAC adresi\>**.</span><span class="sxs-lookup"><span data-stu-id="bce2c-201">Connect to your SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="bce2c-202">Aşağıdaki örnek çıkış daha anlaşılır olması için kısaltılır:</span><span class="sxs-lookup"><span data-stu-id="bce2c-202">The following sample output is abbreviated for clarity:</span></span>

    ```sh
    Attempting to connect to A0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > <span data-ttu-id="bce2c-203">Kullanarak yeniden aygıtın GATT özelliklerini listeleyebilirsiniz **liste öznitelikleri** komutu.</span><span class="sxs-lookup"><span data-stu-id="bce2c-203">You can list the GATT characteristics of the device again using the **list-attributes** command.</span></span>

1. <span data-ttu-id="bce2c-204">Cihazı kullanarak artık bağlantısını kesebilirsiniz **bağlantısını** komut ve kullanarak bluetooth Kabuğu'ndan çıkın **çıkın** komutu:</span><span class="sxs-lookup"><span data-stu-id="bce2c-204">You can now disconnect from the device using the **disconnect** command and then exit from the bluetooth shell using the **quit** command:</span></span>

    ```sh
    Attempting to disconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="bce2c-205">Artık Raspberry Pi 3'te bırak IOT kenar örneği çalıştırmak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="bce2c-205">You're now ready to run the BLE IoT Edge sample on your Raspberry Pi 3.</span></span>

## <a name="run-the-iot-edge-ble-sample"></a><span data-ttu-id="bce2c-206">IOT kenar Bırak örneğini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="bce2c-206">Run the IoT Edge BLE sample</span></span>

<span data-ttu-id="bce2c-207">IOT kenar bırak örneği çalıştırmak için üç görevleri tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="bce2c-207">To run the IoT Edge BLE sample, you need to complete three tasks:</span></span>

* <span data-ttu-id="bce2c-208">İki örnek cihazlar IOT Hub'ınıza yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bce2c-208">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="bce2c-209">IOT kenar Raspberry Pi 3 aygıtınızda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bce2c-209">Build IoT Edge on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="bce2c-210">Yapılandırın ve Raspberry Pi 3 aygıtınızda Bırak örneğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bce2c-210">Configure and run the BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="bce2c-211">Yazma zaman IOT kenar yalnızca bırak modülleri Linux üzerinde çalışan ağ geçitleri de destekler.</span><span class="sxs-lookup"><span data-stu-id="bce2c-211">At the time of writing, IoT Edge only supports BLE modules in gateways running on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="bce2c-212">İki örnek cihazlar IOT hub'ınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bce2c-212">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="bce2c-213">[IOT hub oluşturma] [ lnk-create-hub] Azure aboneliğinizde bu yönlendirmeyi tamamlamak için hub adı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="bce2c-213">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need the name of your hub to complete this walkthrough.</span></span> <span data-ttu-id="bce2c-214">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bce2c-214">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="bce2c-215">Adlı bir aygıt Ekle **SensorTag_01** IOT hub ve kendi kimliği ve cihaz anahtarını Not.</span><span class="sxs-lookup"><span data-stu-id="bce2c-215">Add one device called **SensorTag_01** to your IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="bce2c-216">Kullanabileceğiniz [aygıt explorer veya iothub-explorer] [ lnk-explorer-tools] araçları önceki adımda oluşturduğunuz IOT hub'ına bu cihazı eklemeniz ve kendi anahtarını almak için.</span><span class="sxs-lookup"><span data-stu-id="bce2c-216">You can use the [device explorer or iothub-explorer][lnk-explorer-tools] tools to add this device to the IoT hub you created in the previous step and to retrieve its key.</span></span> <span data-ttu-id="bce2c-217">Ağ geçidi yapılandırdığınızda bu aygıtın SensorTag cihaza eşleyin.</span><span class="sxs-lookup"><span data-stu-id="bce2c-217">You map this device to the SensorTag device when you configure the gateway.</span></span>

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a><span data-ttu-id="bce2c-218">Azure IOT kenar, Böğürtlenli Pi 3 derleme</span><span class="sxs-lookup"><span data-stu-id="bce2c-218">Build Azure IoT Edge on your Raspberry Pi 3</span></span>

<span data-ttu-id="bce2c-219">Bağımlılıklar için Azure IOT kenar yükleyin:</span><span class="sxs-lookup"><span data-stu-id="bce2c-219">Install dependencies for Azure IoT Edge:</span></span>

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

<span data-ttu-id="bce2c-220">IOT kenarı ve kendi submodules giriş dizininize kopyalamak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="bce2c-220">Use the following commands to clone IoT Edge and all its submodules to your home directory:</span></span>

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

<span data-ttu-id="bce2c-221">IOT kenar havuzu tam bir kopyasını Raspberry Pi 3'te olduğunda, SDK'sı içerir klasöründen aşağıdaki komutu kullanarak oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bce2c-221">When you have a complete copy of the IoT Edge repository on your Raspberry Pi 3, you can build it using the following command from the folder that contains the SDK:</span></span>

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-the-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="bce2c-222">Yapılandırma ve Raspberry Pi 3'te bırak örnek çalıştırma</span><span class="sxs-lookup"><span data-stu-id="bce2c-222">Configure and run the BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="bce2c-223">Bootstrap ve örneği çalıştırmak için ağ geçidi katılan her IOT kenar modülü yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bce2c-223">To bootstrap and run the sample, you must configure each IoT Edge module that participates in the gateway.</span></span> <span data-ttu-id="bce2c-224">Bu yapılandırma bir JSON dosyası sağlanır ve tüm beş katılımcı IOT kenar modülleri yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bce2c-224">This configuration is provided in a JSON file and you must configure all five participating IoT Edge modules.</span></span> <span data-ttu-id="bce2c-225">Adlı depo örnek bir JSON dosyası olduğu **ağ geçidi\_sample.json** kendi yapılandırma dosyası oluşturmak için başlangıç noktası olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bce2c-225">There is a sample JSON file in the repository called **gateway\_sample.json** that you can use as the starting point for building your own configuration file.</span></span> <span data-ttu-id="bce2c-226">Bu dosya **ble_gateway/samples/src** IOT kenar depoyu yerel kopyasını klasöründe.</span><span class="sxs-lookup"><span data-stu-id="bce2c-226">This file is in the **samples/ble_gateway/src** folder in local copy of the IoT Edge repository.</span></span>

<span data-ttu-id="bce2c-227">Aşağıdaki bölümlerde nasıl bırak örnek için bu yapılandırma dosyasını düzenleyin ve IOT kenar deposu içinde olduğu varsayılır **/home/pi/iot-edge /** klasörü Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="bce2c-227">The following sections describe how to edit this configuration file for the BLE sample and assume that the IoT Edge repository is in the **/home/pi/iot-edge/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="bce2c-228">Havuz başka bir yerde ise, yolları uygun şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="bce2c-228">If the repository is elsewhere, adjust the paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="bce2c-229">Günlükçü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bce2c-229">Logger configuration</span></span>

<span data-ttu-id="bce2c-230">Ağ geçidi deposu varsayılarak bulunduğu **/home/pi/iot-edge /** klasörünü Günlükçü Modülü aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="bce2c-230">Assuming the gateway repository is located in the **/home/pi/iot-edge/** folder, configure the logger module as follows:</span></span>

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a><span data-ttu-id="bce2c-231">BIRAK modül yapılandırması</span><span class="sxs-lookup"><span data-stu-id="bce2c-231">BLE module configuration</span></span>

<span data-ttu-id="bce2c-232">BIRAK cihaz için örnek yapılandırma Texas Instruments SensorTag aygıt varsayar.</span><span class="sxs-lookup"><span data-stu-id="bce2c-232">The sample configuration for the BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="bce2c-233">Çevre bir GATT çalışmalıdır olarak çalışabilir herhangi bir standart bırak aygıtı ancak, verilere ve GATT özellik kimlikleri güncelleştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="bce2c-233">Any standard BLE device that can operate as a GATT peripheral should work but you may need to update the GATT characteristic IDs and data.</span></span> <span data-ttu-id="bce2c-234">SensorTag cihazınızın MAC adresini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bce2c-234">Add the MAC address of your SensorTag device:</span></span>

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

<span data-ttu-id="bce2c-235">SensorTag aygıt kullanmıyorsanız GATT karakteristiğini kimlikleri ve veri değerleri güncelleştirme gerekip gerekmediğini belirlemek bırak cihazınız için belgelerini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="bce2c-235">If you are not using a SensorTag device, review the documentation for your BLE device to determine whether you need to update the GATT characteristic IDs and data values.</span></span>

#### <a name="iot-hub-module"></a><span data-ttu-id="bce2c-236">IOT hub'ı Modülü</span><span class="sxs-lookup"><span data-stu-id="bce2c-236">IoT Hub module</span></span>

<span data-ttu-id="bce2c-237">IOT hub'ınızın adını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bce2c-237">Add the name of your IoT Hub.</span></span> <span data-ttu-id="bce2c-238">Sonek genellikle değerdir **azure devices.net**:</span><span class="sxs-lookup"><span data-stu-id="bce2c-238">The suffix value is typically **azure-devices.net**:</span></span>

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="bce2c-239">Kimlik eşleme modülü yapılandırması</span><span class="sxs-lookup"><span data-stu-id="bce2c-239">Identity mapping module configuration</span></span>

<span data-ttu-id="bce2c-240">MAC adresi SensorTag Cihazınızı cihaz kimliği ve anahtarı eklemek **SensorTag_01** aygıt IOT Hub'ınıza eklendi:</span><span class="sxs-lookup"><span data-stu-id="bce2c-240">Add the MAC address of your SensorTag device and the device ID and key of the **SensorTag_01** device you added to your IoT Hub:</span></span>

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="bce2c-241">BIRAK yazıcı modülü yapılandırması</span><span class="sxs-lookup"><span data-stu-id="bce2c-241">BLE Printer module configuration</span></span>

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="bce2c-242">BLEC2D modülü yapılandırması</span><span class="sxs-lookup"><span data-stu-id="bce2c-242">BLEC2D Module Configuration</span></span>

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a><span data-ttu-id="bce2c-243">Yönlendirme yapılandırması</span><span class="sxs-lookup"><span data-stu-id="bce2c-243">Routing Configuration</span></span>

<span data-ttu-id="bce2c-244">Aşağıdaki yapılandırma aşağıdaki IOT kenar modülleri arasında yönlendirme sağlar:</span><span class="sxs-lookup"><span data-stu-id="bce2c-244">The following configuration ensures the following routing between IoT Edge modules:</span></span>

* <span data-ttu-id="bce2c-245">**Günlükçü** modülü alır ve tüm iletileri günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="bce2c-245">The **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="bce2c-246">**SensorTag** modülü hem de iletileri gönderir **eşleme** ve **bırak yazıcı** modüller.</span><span class="sxs-lookup"><span data-stu-id="bce2c-246">The **SensorTag** module sends messages to both the **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="bce2c-247">**Eşleme** modülü iletileri gönderir **Iothub** IOT Hub'ına gönderilen modülü.</span><span class="sxs-lookup"><span data-stu-id="bce2c-247">The **mapping** module sends messages to the **IoTHub** module to be sent up to your IoT Hub.</span></span>
* <span data-ttu-id="bce2c-248">**Iothub** modül gönderir iletileri başa **eşleme** modülü.</span><span class="sxs-lookup"><span data-stu-id="bce2c-248">The **IoTHub** module sends messages back to the **mapping** module.</span></span>
* <span data-ttu-id="bce2c-249">**Eşleme** modülü iletileri gönderir **BLEC2D** modülü.</span><span class="sxs-lookup"><span data-stu-id="bce2c-249">The **mapping** module sends messages to the **BLEC2D** module.</span></span>
* <span data-ttu-id="bce2c-250">**BLEC2D** modül gönderir iletileri başa **algılayıcı etiketi** modülü.</span><span class="sxs-lookup"><span data-stu-id="bce2c-250">The **BLEC2D** module sends messages back to the **Sensor Tag** module.</span></span>

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

<span data-ttu-id="bce2c-251">Örneği çalıştırmak için bir parametre olarak JSON yapılandırma dosyası yolu geçirmek **bırak\_ağ geçidi** ikili.</span><span class="sxs-lookup"><span data-stu-id="bce2c-251">To run the sample, pass the path to the JSON configuration file as a parameter to the **ble\_gateway** binary.</span></span> <span data-ttu-id="bce2c-252">Aşağıdaki komut, kullanmakta olduğunuz varsayar **gateway_sample.json** yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="bce2c-252">The following command assumes you are using the **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="bce2c-253">Bu komutu yürütmek **IOT kenar** Raspberry Pi'yi klasörü:</span><span class="sxs-lookup"><span data-stu-id="bce2c-253">Execute this command from the **iot-edge** folder on the Raspberry Pi:</span></span>

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="bce2c-254">Küçük bir düğme örneği çalıştırmadan önce bulunabilir yapmak için SensorTag aygıtta basmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="bce2c-254">You may need to press the small button on the SensorTag device to make it discoverable before you run the sample.</span></span>

<span data-ttu-id="bce2c-255">Örneği çalıştırdığınızda, kullanabileceğiniz [aygıt explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) veya [iothub-explorer](https://github.com/Azure/iothub-explorer) IOT sınır ağ geçidi iletir SensorTag aygıttan iletileri izlemek için aracı.</span><span class="sxs-lookup"><span data-stu-id="bce2c-255">When you run the sample, you can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to monitor the messages the IoT Edge gateway forwards from the SensorTag device.</span></span> <span data-ttu-id="bce2c-256">Örneğin, ıothub explorer kullanarak aşağıdaki komutu kullanarak cihaz bulut iletilerini izleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bce2c-256">For example, using iothub-explorer you can monitor device-to-cloud messages using the following command:</span></span>

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="bce2c-257">Buluttan cihaza iletileri gönderme</span><span class="sxs-lookup"><span data-stu-id="bce2c-257">Send cloud-to-device messages</span></span>

<span data-ttu-id="bce2c-258">BIRAK modülü gönderen komutlarından IOT Hub cihaz için de destekler.</span><span class="sxs-lookup"><span data-stu-id="bce2c-258">The BLE module also supports sending commands from IoT Hub to the device.</span></span> <span data-ttu-id="bce2c-259">Kullanabilirsiniz [aygıt explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) veya [iothub-explorer](https://github.com/Azure/iothub-explorer) bırak ağ geçidi modülü açın bırak aygıt iletir JSON iletileri gönderme aracı.</span><span class="sxs-lookup"><span data-stu-id="bce2c-259">You can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to send JSON messages that the BLE gateway module forwards on to the BLE device.</span></span>

<span data-ttu-id="bce2c-260">Texas Instruments SensorTag cihaz kullanıyorsanız, IOT Hub'ından komutlar göndererek kırmızı LED, yeşil LED veya sesli uyaran kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bce2c-260">If you are using the Texas Instruments SensorTag device, you can turn on the red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="bce2c-261">İlk IOT Hub'ından komutları göndermeden önce aşağıdaki iki JSON ileti sırada gönderin.</span><span class="sxs-lookup"><span data-stu-id="bce2c-261">Before you send commands from IoT Hub, first send the following two JSON messages in order.</span></span> <span data-ttu-id="bce2c-262">Ardından, ışık veya sesli uyaran için komutlardan herhangi birini gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bce2c-262">Then you can send any of the commands to turn on the lights or buzzer.</span></span>

1. <span data-ttu-id="bce2c-263">Tüm LED'leri ve sesli uyaran sıfırlama (devre dışı bırakma):</span><span class="sxs-lookup"><span data-stu-id="bce2c-263">Reset all LEDs and the buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="bce2c-264">G/ç 'uzaktan' yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="bce2c-264">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="bce2c-265">Şimdi ışık veya sesli uyaran SensorTag cihazda etkinleştirmek için aşağıdaki komutlardan herhangi birini gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bce2c-265">Now you can send any of the following commands to turn on the lights or buzzer on the SensorTag device:</span></span>

* <span data-ttu-id="bce2c-266">Üzerinde kırmızı LED açın:</span><span class="sxs-lookup"><span data-stu-id="bce2c-266">Turn on the red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="bce2c-267">Yeşil LED üzerinde açın:</span><span class="sxs-lookup"><span data-stu-id="bce2c-267">Turn on the green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="bce2c-268">Sesli uyaran üzerinde açın:</span><span class="sxs-lookup"><span data-stu-id="bce2c-268">Turn on the buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="bce2c-269">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="bce2c-269">Next Steps</span></span>

<span data-ttu-id="bce2c-270">IOT kenar daha gelişmiş anlamak ve bazı kod örnekleri ile denemek istiyorsanız, aşağıdaki Geliştirici öğreticiler ve kaynakları ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="bce2c-270">If you want to gain a more advanced understanding of IoT Edge and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="bce2c-271">[Azure IOT kenar][lnk-sdk]</span><span class="sxs-lookup"><span data-stu-id="bce2c-271">[Azure IoT Edge][lnk-sdk]</span></span>

<span data-ttu-id="bce2c-272">Daha fazla IOT hub'ı özelliklerini keşfetmek için bkz:</span><span class="sxs-lookup"><span data-stu-id="bce2c-272">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="bce2c-273">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="bce2c-273">[IoT Hub developer guide][lnk-devguide]</span></span>

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
