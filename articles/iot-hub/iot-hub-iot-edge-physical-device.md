---
title: "Azure IOT kenarıyla fiziksel bir aygıtı aaaUse | Microsoft Docs"
description: "Nasıl toouse bir Texas Instruments SensorTag aygıt toosend veri tooan IOT hub Raspberry Pi 3 cihazda çalışan IOT sınır ağ geçidi üzerinden. Merhaba ağ geçidi, Azure IOT kenar kullanılarak oluşturulur."
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
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="b0fd9-104">Azure IOT kenar Raspberry Pi'yi tooforward cihaz bulut iletilerini tooIoT Hub kullanın</span><span class="sxs-lookup"><span data-stu-id="b0fd9-104">Use Azure IoT Edge on a Raspberry Pi tooforward device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="b0fd9-105">Bu kılavuz hello [Bluetooth düşük enerji örnek] [ lnk-ble-samplecode] nasıl gösterir toouse [Azure IOT kenar] [ lnk-sdk] için:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-105">This walkthrough of hello [Bluetooth low energy sample][lnk-ble-samplecode] shows you how toouse [Azure IoT Edge][lnk-sdk] to:</span></span>

* <span data-ttu-id="b0fd9-106">Cihaz bulut telemetri tooIoT Hub fiziksel CİHAZDAN iletin.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-106">Forward device-to-cloud telemetry tooIoT Hub from a physical device.</span></span>
* <span data-ttu-id="b0fd9-107">IOT hub'ı tooa fiziksel CİHAZDAN rota komutları.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-107">Route commands from IoT Hub tooa physical device.</span></span>

<span data-ttu-id="b0fd9-108">Bu kılavuzda aşağıdaki konular ele alınmaktadır:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-108">This walkthrough covers:</span></span>

* <span data-ttu-id="b0fd9-109">**Mimari**: hello Bluetooth düşük enerji örnek hakkında önemli mimari bilgiler.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-109">**Architecture**: important architectural information about hello Bluetooth low energy sample.</span></span>
* <span data-ttu-id="b0fd9-110">**Derleme ve çalıştırma**: hello adımları gerekli toobuild ve çalışma hello örnek.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-110">**Build and run**: hello steps required toobuild and run hello sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="b0fd9-111">Mimari</span><span class="sxs-lookup"><span data-stu-id="b0fd9-111">Architecture</span></span>

<span data-ttu-id="b0fd9-112">Merhaba anlatım nasıl toobuild ve Raspberry Pi 3 IOT sınır ağ geçidi çalıştırılmasında Raspbian Linux çalıştıran gösterir.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-112">hello walkthrough shows you how toobuild and run an IoT Edge gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="b0fd9-113">Merhaba ağ geçidi IOT kenar kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-113">hello gateway is built using IoT Edge.</span></span> <span data-ttu-id="b0fd9-114">Merhaba örnek bir Texas Instruments SensorTag Bluetooth düşük enerji (bırak) cihaz toocollect sıcaklık verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-114">hello sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device toocollect temperature data.</span></span>

<span data-ttu-id="b0fd9-115">Merhaba IOT sınır ağ geçidi çalıştırdığınızda bu:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-115">When you run hello IoT Edge gateway it:</span></span>

* <span data-ttu-id="b0fd9-116">Tooa SensorTag aygıt Hello Bluetooth düşük enerji (bırak) protokolünü kullanarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-116">Connects tooa SensorTag device using hello Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="b0fd9-117">TooIoT Hub bağlayan hello HTTP protokolünü kullanarak.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-117">Connects tooIoT Hub using hello HTTP protocol.</span></span>
* <span data-ttu-id="b0fd9-118">Telemetri hello SensorTag aygıt tooIoT Hub iletir.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-118">Forwards telemetry from hello SensorTag device tooIoT Hub.</span></span>
* <span data-ttu-id="b0fd9-119">IOT hub'ı toohello SensorTag aygıttan komutları yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-119">Routes commands from IoT Hub toohello SensorTag device.</span></span>

<span data-ttu-id="b0fd9-120">Merhaba ağ geçidi IOT kenar modülleri aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-120">hello gateway contains hello following IoT Edge modules:</span></span>

* <span data-ttu-id="b0fd9-121">A *bırak Modülü* verilerle bir bırak aygıt tooreceive sıcaklık hello aygıt ve gönderme komutları toohello aygıt arabirimleri.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-121">A *BLE module* that interfaces with a BLE device tooreceive temperature data from hello device and send commands toohello device.</span></span>
* <span data-ttu-id="b0fd9-122">A *bırak bulut toodevice Modülü* bırak yönergeler hello için içine IOT Hub'ından gönderilen JSON iletileri çevirir *bırak Modülü*.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-122">A *BLE cloud toodevice module* that translates JSON messages sent from IoT Hub into BLE instructions for hello *BLE module*.</span></span>
* <span data-ttu-id="b0fd9-123">A *Günlükçü Modülü* tüm ağ geçidi iletileri tooa yerel dosya kaydeder.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-123">A *logger module* that logs all gateway messages tooa local file.</span></span>
* <span data-ttu-id="b0fd9-124">Bir *kimlik eşleme Modülü* bırak aygıt MAC adresi ile Azure IOT Hub cihaz kimlikleri arasında çevirir.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="b0fd9-125">Bir *IOT hub'ı Modülü* telemetri verileri tooan IOT hub'ı yükler ve IOT hub'ından cihaz komutlarını alır.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-125">An *IoT Hub module* that uploads telemetry data tooan IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="b0fd9-126">A *bırak yazıcı Modülü* hello bırak cihaz telemetrisinden yorumlar ve biçimlendirilmiş veriler toohello konsol tooenable sorun giderme ve hata ayıklama yazdırır.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-126">A *BLE printer module* that interprets telemetry from hello BLE device and prints formatted data toohello console tooenable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-hello-gateway"></a><span data-ttu-id="b0fd9-127">Merhaba ağ geçidi üzerinden nasıl veri akışları</span><span class="sxs-lookup"><span data-stu-id="b0fd9-127">How data flows through hello gateway</span></span>

<span data-ttu-id="b0fd9-128">Blok Diyagramı aşağıdaki hello hello telemetri karşıya yükleme veri akışı ardışık gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-128">hello following block diagram illustrates hello telemetry upload data flow pipeline:</span></span>

![Telemetri karşıya yükleme ağ geçidi ardışık düzen](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="b0fd9-130">öğeyi telemetri bırak aygıt tooIoT seyahat alan hello Hub adımlardır:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-130">hello steps that an item of telemetry takes traveling from a BLE device tooIoT Hub are:</span></span>

1. <span data-ttu-id="b0fd9-131">Merhaba bırak aygıt sıcaklık örnek oluşturur ve Bluetooth toohello bırak hello ağ geçidi modülünde üzerinden gönderir.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-131">hello BLE device generates a temperature sample and sends it over Bluetooth toohello BLE module in hello gateway.</span></span>
1. <span data-ttu-id="b0fd9-132">Merhaba bırak modülü hello örnek alır ve toohello Aracısı hello aygıtın hello MAC adresi birlikte yayımlar.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-132">hello BLE module receives hello sample and publishes it toohello broker along with hello MAC address of hello device.</span></span>
1. <span data-ttu-id="b0fd9-133">Hello kimlik eşleme modülü bu iletiyi alır ve bir iç tablo tootranslate hello hello aygıt MAC adresi bir IOT Hub cihaz kimliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-133">hello identity mapping module picks up this message and uses an internal table tootranslate hello MAC address of hello device into an IoT Hub device identity.</span></span> <span data-ttu-id="b0fd9-134">Bir IOT Hub cihaz kimliği, bir cihaz kimliği ve aygıt anahtarı oluşur.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-134">An IoT Hub device identity consists of a device ID and device key.</span></span>
1. <span data-ttu-id="b0fd9-135">Merhaba kimlik eşleme modülü hello sıcaklık örnek verileri, hello MAC adresi hello aygıt, hello cihaz kimliği ve hello aygıt anahtarı içeren yeni bir ileti yayımlar.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-135">hello identity mapping module publishes a new message that contains hello temperature sample data, hello MAC address of hello device, hello device ID, and hello device key.</span></span>
1. <span data-ttu-id="b0fd9-136">Merhaba IOT hub'ı Modülü (Merhaba kimlik eşleme modülü tarafından oluşturulan) bu yeni bir ileti alır ve tooIoT Hub yayımlar.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-136">hello IoT Hub module receives this new message (generated by hello identity mapping module) and publishes it tooIoT Hub.</span></span>
1. <span data-ttu-id="b0fd9-137">Merhaba Günlükçü modülü hello Aracısı tooa yerel dosyadan tüm iletileri günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-137">hello logger module logs all messages from hello broker tooa local file.</span></span>

<span data-ttu-id="b0fd9-138">Blok Diyagramı aşağıdaki hello hello aygıt komutu veri akışı ardışık gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-138">hello following block diagram illustrates hello device command data flow pipeline:</span></span>

![Cihaz komut ağ geçidi ardışık düzeni](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="b0fd9-140">Yeni komut iletileri için IOT hub hello Hello IOT Hub'ın modül düzenli aralıklarla yoklar.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-140">hello IoT Hub module periodically polls hello IoT hub for new command messages.</span></span>
1. <span data-ttu-id="b0fd9-141">Merhaba IOT hub'ı modülü yeni bir komut iletisi aldığında, onu toohello Aracısı yayımlar.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-141">When hello IoT Hub module receives a new command message, it publishes it toohello broker.</span></span>
1. <span data-ttu-id="b0fd9-142">Merhaba kimlik eşleme modülü hello komutu iletiyi alır ve bir iç tablo tootranslate hello IOT Hub cihaz kimliği tooa aygıt MAC adresi kullanır.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-142">hello identity mapping module picks up hello command message and uses an internal table tootranslate hello IoT Hub device ID tooa device MAC address.</span></span> <span data-ttu-id="b0fd9-143">Ardından, hello özellikleri eşlemesinde hello iletisinin hello hedef aygıt hello MAC adresini içeren yeni bir ileti yayımlar.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-143">It then publishes a new message that includes hello MAC address of hello target device in hello properties map of hello message.</span></span>
1. <span data-ttu-id="b0fd9-144">Merhaba bırak bulut-cihaz modülü bu iletiyi alır ve hello uygun bırak yönerge hello bırak modülü için çevirir.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-144">hello BLE Cloud-to-Device module picks up this message and translates it into hello proper BLE instruction for hello BLE module.</span></span> <span data-ttu-id="b0fd9-145">Ardından, yeni bir ileti yayımlar.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="b0fd9-146">Merhaba bırak modülü bu iletiyi alır ve hello bırak aygıtla iletişim kurarak hello g/ç yönerge çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-146">hello BLE module picks up this message and executes hello I/O instruction by communicating with hello BLE device.</span></span>
1. <span data-ttu-id="b0fd9-147">Merhaba Günlükçü modülü hello Aracısı tooa disk dosyasından tüm iletileri günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-147">hello logger module logs all messages from hello broker tooa disk file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0fd9-148">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b0fd9-148">Prerequisites</span></span>

<span data-ttu-id="b0fd9-149">toocomplete Bu öğreticide, bir etkin Azure aboneliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-149">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="b0fd9-150">Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-150">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b0fd9-151">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="b0fd9-151">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

<span data-ttu-id="b0fd9-152">Tooremotely erişim hello komut satırı Raspberry Pi'yi hello üzerinde Masaüstü makine tooenable üzerinde SSH istemcisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-152">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="b0fd9-153">Windows, bir SSH istemcisi içermez.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-153">Windows does not include an SSH client.</span></span> <span data-ttu-id="b0fd9-154">Kullanmanızı öneririz [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="b0fd9-154">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="b0fd9-155">Çoğu Linux dağıtımları ve Mac OS komut satırı SSH yardımcı programını hello içerir.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-155">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="b0fd9-156">Daha fazla bilgi için bkz: [SSH kullanarak Linux veya Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="b0fd9-156">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="b0fd9-157">Donanımınızın hazırlama</span><span class="sxs-lookup"><span data-stu-id="b0fd9-157">Prepare your hardware</span></span>

<span data-ttu-id="b0fd9-158">Bu öğreticide kullandığınız varsayılır bir [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) aygıt bağlı tooa Raspberry Pi 3 Raspbian çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-158">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected tooa Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="b0fd9-159">Raspbian yükleyin</span><span class="sxs-lookup"><span data-stu-id="b0fd9-159">Install Raspbian</span></span>

<span data-ttu-id="b0fd9-160">Seçenekler tooinstall Raspbian Raspberry Pi 3 aygıtınızda aşağıdaki hello birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-160">You can use either of hello following options tooinstall Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="b0fd9-161">tooinstall hello en son sürümünü Raspbian, kullanım hello [NOOBS] [ lnk-noobs] grafik kullanıcı arabirimi.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-161">tooinstall hello latest version of Raspbian, use hello [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="b0fd9-162">El ile [karşıdan] [ lnk-raspbian] ve hello son hello Raspbian işletim sistemi tooan SD kart görüntüsü yazma.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-162">Manually [download][lnk-raspbian] and write hello latest image of hello Raspbian operating system tooan SD card.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="b0fd9-163">Oturum açma ve hello terminal erişim</span><span class="sxs-lookup"><span data-stu-id="b0fd9-163">Sign in and access hello terminal</span></span>

<span data-ttu-id="b0fd9-164">İki seçenek tooaccess, Raspberry Pi'yi bir terminal ortamına sahip:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-164">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

* <span data-ttu-id="b0fd9-165">Klavye varsa ve bağlı tooyour Raspberry Pi'yi izlemek, hello Raspbian GUI tooaccess bir terminal penceresi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-165">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

* <span data-ttu-id="b0fd9-166">Erişim hello komut satırında Masaüstü makinenizden SSH kullanarak, Raspberry Pi'yi.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-166">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="b0fd9-167">Merhaba GUI içinde bir terminal penceresi kullanın</span><span class="sxs-lookup"><span data-stu-id="b0fd9-167">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="b0fd9-168">Merhaba varsayılan kimlik bilgilerini Raspbian olan kullanıcı adı **PI** ve parola **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-168">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="b0fd9-169">Merhaba Görev Çubuğu'nda hello GUI, hello başlatabilirsiniz **Terminal** gibi bir izleyici arar hello simgesini kullanarak yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-169">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="b0fd9-170">Oturum SSH oturum</span><span class="sxs-lookup"><span data-stu-id="b0fd9-170">Sign in with SSH</span></span>

<span data-ttu-id="b0fd9-171">Komut satırı erişimi tooyour Raspberry Pi'yi için SSH kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-171">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="b0fd9-172">Merhaba makale [SSH (Secure Shell)] [ lnk-pi-ssh] açıklar nasıl tooconfigure, Raspberry Pi'yi üzerinde SSH ve nasıl tooconnect gelen [Windows] [ lnk-ssh-windows] veya [Linux ve Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="b0fd9-172">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="b0fd9-173">Kullanıcı adıyla oturum **PI** ve parola **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-173">Sign in with username **pi** and password **raspberry**.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="b0fd9-174">BlueZ 5.37 yükleyin</span><span class="sxs-lookup"><span data-stu-id="b0fd9-174">Install BlueZ 5.37</span></span>

<span data-ttu-id="b0fd9-175">Merhaba bırak modülleri toohello Bluetooth donanım hello BlueZ yığını ile görüşün.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-175">hello BLE modules talk toohello Bluetooth hardware via hello BlueZ stack.</span></span> <span data-ttu-id="b0fd9-176">BlueZ 5.37 sürümü hello modülleri toowork için doğru ihtiyacınız var.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-176">You need version 5.37 of BlueZ for hello modules toowork correctly.</span></span> <span data-ttu-id="b0fd9-177">Bu yönergeleri hello BlueZ doğru sürümünün yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-177">These instructions make sure hello correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="b0fd9-178">Merhaba geçerli bluetooth arka plan programı durdurun:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-178">Stop hello current bluetooth daemon:</span></span>

    ```sh
    sudo systemctl stop bluetooth
    ```

1. <span data-ttu-id="b0fd9-179">Merhaba BlueZ bağımlılıkları yükler:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-179">Install hello BlueZ dependencies:</span></span>

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. <span data-ttu-id="b0fd9-180">Merhaba BlueZ kaynak kodu bluez.org yükleyin:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-180">Download hello BlueZ source code from bluez.org:</span></span>

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="b0fd9-181">Merhaba kaynak kodu sıkıştırmasını açın:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-181">Unzip hello source code:</span></span>

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="b0fd9-182">Dizinleri toohello yeni oluşturulan klasör değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-182">Change directories toohello newly created folder:</span></span>

    ```sh
    cd bluez-5.37
    ```

1. <span data-ttu-id="b0fd9-183">Yerleşik hello BlueZ kod toobe yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-183">Configure hello BlueZ code toobe built:</span></span>

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. <span data-ttu-id="b0fd9-184">BlueZ oluşturun:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-184">Build BlueZ:</span></span>

    ```sh
    make
    ```

1. <span data-ttu-id="b0fd9-185">Bunu yaptıktan sonra BlueZ yükleme oluşturma:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-185">Install BlueZ once it is done building:</span></span>

    ```sh
    sudo make install
    ```

1. <span data-ttu-id="b0fd9-186">Değişiklik systemd hizmet yapılandırması toohello yeni bluetooth arka plan programı hello dosyasında işaret şekilde bluetooth `/lib/systemd/system/bluetooth.service`.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-186">Change systemd service configuration for bluetooth so it points toohello new bluetooth daemon in hello file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="b0fd9-187">Merhaba 'ExecStart' satır metnini izleyen hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-187">Replace hello 'ExecStart' line with hello following text:</span></span>

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="b0fd9-188">Bağlantı toohello SensorTag aygıtı Raspberry Pi 3 cihazınızdan etkinleştir</span><span class="sxs-lookup"><span data-stu-id="b0fd9-188">Enable connectivity toohello SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="b0fd9-189">Çalışan hello örnek önce Raspberry Pi 3 toohello SensorTag aygıt bağlanabilir tooverify gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-189">Before running hello sample, you need tooverify that your Raspberry Pi 3 can connect toohello SensorTag device.</span></span>

1. <span data-ttu-id="b0fd9-190">Merhaba olun `rfkill` yardımcı programı yüklenir:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-190">Ensure hello `rfkill` utility is installed:</span></span>

    ```sh
    sudo apt-get install rfkill
    ```

1. <span data-ttu-id="b0fd9-191">Bluetooth hello Raspberry Pi 3 üzerinde engelini kaldırmak ve hello sürüm numarası olup olmadığını denetleyin **5.37**:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-191">Unblock bluetooth on hello Raspberry Pi 3 and check that hello version number is **5.37**:</span></span>

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. <span data-ttu-id="b0fd9-192">tooenter hello etkileşimli bluetooth Kabuk hello bluetooth hizmetini başlatın ve hello yürütme **bluetoothctl** komutu:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-192">tooenter hello interactive bluetooth shell, start hello bluetooth service and execute hello **bluetoothctl** command :</span></span>

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="b0fd9-193">Merhaba komutu girin **güç açma** toopower hello bluetooth denetleyici ayarlama.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-193">Enter hello command **power on** toopower up hello bluetooth controller.</span></span> <span data-ttu-id="b0fd9-194">Merhaba komut çıktısı benzer toohello aşağıdaki döndürür:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-194">hello command returns output similar toohello following:</span></span>

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="b0fd9-195">Merhaba etkileşimli bluetooth Kabuğu'nda hello komutu girin **taraması** tooscan bluetooth cihazları için.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-195">In hello interactive bluetooth shell, enter hello command **scan on** tooscan for bluetooth devices.</span></span> <span data-ttu-id="b0fd9-196">Merhaba komut çıktısı benzer toohello aşağıdaki döndürür:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-196">hello command returns output similar toohello following:</span></span>

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="b0fd9-197">Merhaba SensorTag aygıt bulunabilirlik hello küçük (yeşil LED flash hello) düğmesini tıklatarak olun.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-197">Make hello SensorTag device discoverable by pressing hello small button (hello green LED should flash).</span></span> <span data-ttu-id="b0fd9-198">Merhaba Raspberry Pi 3 hello SensorTag aygıtı keşfet:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-198">hello Raspberry Pi 3 should discover hello SensorTag device:</span></span>

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="b0fd9-199">Bu örnekte, bu hello hello SensorTag aygıt MAC adresi görebilirsiniz **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-199">In this example, you can see that hello MAC address of hello SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="b0fd9-200">Merhaba girerek taramayı kapatabilirsiniz **kapalı tarama** komutu:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-200">Turn off scanning by entering hello **scan off** command:</span></span>

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="b0fd9-201">MAC adresini girerek kullanarak tooyour SensorTag aygıtı bağlayın **bağlanmak \<MAC adresi\>**.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-201">Connect tooyour SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="b0fd9-202">örnek çıktı aşağıdaki hello daha anlaşılır olması için kısaltılır:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-202">hello following sample output is abbreviated for clarity:</span></span>

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
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

    > <span data-ttu-id="b0fd9-203">Merhaba GATT hello kullanarak yeniden hello aygıtın özelliklerini listeleyebilirsiniz **liste öznitelikleri** komutu.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-203">You can list hello GATT characteristics of hello device again using hello **list-attributes** command.</span></span>

1. <span data-ttu-id="b0fd9-204">Artık hello kullanarak hello aygıttan bağlantısını **bağlantısını** komut ve hello kullanarak hello bluetooth Kabuğu'ndan çıkmak **çıkın** komutu:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-204">You can now disconnect from hello device using hello **disconnect** command and then exit from hello bluetooth shell using hello **quit** command:</span></span>

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="b0fd9-205">Şimdi Raspberry Pi 3'te hazır toorun hello bırak IOT kenar örnek demektir.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-205">You're now ready toorun hello BLE IoT Edge sample on your Raspberry Pi 3.</span></span>

## <a name="run-hello-iot-edge-ble-sample"></a><span data-ttu-id="b0fd9-206">Merhaba IOT kenar Bırak örneğini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="b0fd9-206">Run hello IoT Edge BLE sample</span></span>

<span data-ttu-id="b0fd9-207">toorun hello IOT kenar bırak örnek toocomplete üç görevler gerekir:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-207">toorun hello IoT Edge BLE sample, you need toocomplete three tasks:</span></span>

* <span data-ttu-id="b0fd9-208">İki örnek cihazlar IOT Hub'ınıza yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-208">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="b0fd9-209">IOT kenar Raspberry Pi 3 aygıtınızda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-209">Build IoT Edge on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="b0fd9-210">Yapılandırın ve Raspberry Pi 3 aygıtınızda hello bırak örnek çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-210">Configure and run hello BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="b0fd9-211">Yazma Hello anda IOT kenar yalnızca bırak modülleri Linux üzerinde çalışan ağ geçitleri de destekler.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-211">At hello time of writing, IoT Edge only supports BLE modules in gateways running on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="b0fd9-212">İki örnek cihazlar IOT hub'ınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b0fd9-212">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="b0fd9-213">[IOT hub oluşturma] [ lnk-create-hub] Azure aboneliğinizde bu kılavuzda, hub toocomplete hello adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-213">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need hello name of your hub toocomplete this walkthrough.</span></span> <span data-ttu-id="b0fd9-214">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-214">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="b0fd9-215">Adlı bir aygıt Ekle **SensorTag_01** tooyour IOT hub ve kendi kimliği ve cihaz anahtarını not edin.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-215">Add one device called **SensorTag_01** tooyour IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="b0fd9-216">Merhaba kullanabilirsiniz [aygıt explorer veya iothub-explorer] [ lnk-explorer-tools] tooadd oluşturduğunuz hello önceki adımı ve tooretrieve anahtarıyla bu cihaz toohello IOT hub araçları.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-216">You can use hello [device explorer or iothub-explorer][lnk-explorer-tools] tools tooadd this device toohello IoT hub you created in hello previous step and tooretrieve its key.</span></span> <span data-ttu-id="b0fd9-217">Merhaba ağ geçidi yapılandırdığınızda bu cihaz toohello SensorTag aygıt eşleyin.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-217">You map this device toohello SensorTag device when you configure hello gateway.</span></span>

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a><span data-ttu-id="b0fd9-218">Azure IOT kenar, Böğürtlenli Pi 3 derleme</span><span class="sxs-lookup"><span data-stu-id="b0fd9-218">Build Azure IoT Edge on your Raspberry Pi 3</span></span>

<span data-ttu-id="b0fd9-219">Bağımlılıklar için Azure IOT kenar yükleyin:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-219">Install dependencies for Azure IoT Edge:</span></span>

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

<span data-ttu-id="b0fd9-220">Kullanım hello aşağıdaki tooclone IOT kenar ve tüm alt submodules tooyour giriş dizini komutlar:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-220">Use hello following commands tooclone IoT Edge and all its submodules tooyour home directory:</span></span>

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

<span data-ttu-id="b0fd9-221">Merhaba IOT kenar havuzu tam bir kopyasını Raspberry Pi 3'te olduğunda komut hello SDK içeren hello klasöründen aşağıdaki hello kullanarak oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-221">When you have a complete copy of hello IoT Edge repository on your Raspberry Pi 3, you can build it using hello following command from hello folder that contains hello SDK:</span></span>

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="b0fd9-222">Yapılandırma ve hello bırak örnek Raspberry Pi 3'te çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b0fd9-222">Configure and run hello BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="b0fd9-223">toobootstrap ve çalışma hello örnek, hello ağ geçidi katılan her IOT kenar modülü yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-223">toobootstrap and run hello sample, you must configure each IoT Edge module that participates in hello gateway.</span></span> <span data-ttu-id="b0fd9-224">Bu yapılandırma bir JSON dosyası sağlanır ve tüm beş katılımcı IOT kenar modülleri yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-224">This configuration is provided in a JSON file and you must configure all five participating IoT Edge modules.</span></span> <span data-ttu-id="b0fd9-225">Merhaba depoya adlı örnek bir JSON dosyası olduğu **ağ geçidi\_sample.json** başlangıç noktası kendi yapılandırma dosyası oluşturmak için hello olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-225">There is a sample JSON file in hello repository called **gateway\_sample.json** that you can use as hello starting point for building your own configuration file.</span></span> <span data-ttu-id="b0fd9-226">Bu bir dosyadır hello **ble_gateway/samples/src** hello IOT kenar havuzu yerel kopyasını klasöründe.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-226">This file is in hello **samples/ble_gateway/src** folder in local copy of hello IoT Edge repository.</span></span>

<span data-ttu-id="b0fd9-227">Hello aşağıdaki bölümlerde bu yapılandırma hello bırak örnek için dosya ve o hello IOT kenar havuzu varsayın tooedit hello nasıl olduğunu açıklamak **/home/pi/iot-edge /** klasörü Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-227">hello following sections describe how tooedit this configuration file for hello BLE sample and assume that hello IoT Edge repository is in hello **/home/pi/iot-edge/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="b0fd9-228">Merhaba deposu başka bir yerde ise, hello yollar uygun şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-228">If hello repository is elsewhere, adjust hello paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="b0fd9-229">Günlükçü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b0fd9-229">Logger configuration</span></span>

<span data-ttu-id="b0fd9-230">Merhaba ağ geçidi deposu hello bulunan varsayılarak **/home/pi/iot-edge /** klasörünü hello Günlükçü Modülü aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-230">Assuming hello gateway repository is located in hello **/home/pi/iot-edge/** folder, configure hello logger module as follows:</span></span>

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

#### <a name="ble-module-configuration"></a><span data-ttu-id="b0fd9-231">BIRAK modül yapılandırması</span><span class="sxs-lookup"><span data-stu-id="b0fd9-231">BLE module configuration</span></span>

<span data-ttu-id="b0fd9-232">Merhaba bırak cihaz için Hello örnek yapılandırma Texas Instruments SensorTag aygıt varsayar.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-232">hello sample configuration for hello BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="b0fd9-233">Çevre bir GATT çalışması gerekir, ancak tooupdate hello GATT karakteristiğini kimlikleri ve veri gerekebilir gibi çalışabilir standart herhangi bırak aygıt.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-233">Any standard BLE device that can operate as a GATT peripheral should work but you may need tooupdate hello GATT characteristic IDs and data.</span></span> <span data-ttu-id="b0fd9-234">SensorTag Cihazınızı Hello MAC adresini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-234">Add hello MAC address of your SensorTag device:</span></span>

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

<span data-ttu-id="b0fd9-235">SensorTag aygıt kullanmıyorsanız tooupdate hello GATT karakteristiğini kimlikleri ve veri değerlerini gerekip gerekmediğini bırak aygıt toodetermine için hello belgelerini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-235">If you are not using a SensorTag device, review hello documentation for your BLE device toodetermine whether you need tooupdate hello GATT characteristic IDs and data values.</span></span>

#### <a name="iot-hub-module"></a><span data-ttu-id="b0fd9-236">IOT hub'ı Modülü</span><span class="sxs-lookup"><span data-stu-id="b0fd9-236">IoT Hub module</span></span>

<span data-ttu-id="b0fd9-237">IOT Hub'ınızı Hello adını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-237">Add hello name of your IoT Hub.</span></span> <span data-ttu-id="b0fd9-238">Merhaba sonek değeri genellikle **azure devices.net**:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-238">hello suffix value is typically **azure-devices.net**:</span></span>

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

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="b0fd9-239">Kimlik eşleme modülü yapılandırması</span><span class="sxs-lookup"><span data-stu-id="b0fd9-239">Identity mapping module configuration</span></span>

<span data-ttu-id="b0fd9-240">Merhaba MAC adresini SensorTag cihaz ve hello cihaz kimliği ve başlangıç anahtarı eklemek **SensorTag_01** tooyour IOT hub'ı eklediğiniz aygıt:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-240">Add hello MAC address of your SensorTag device and hello device ID and key of hello **SensorTag_01** device you added tooyour IoT Hub:</span></span>

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

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="b0fd9-241">BIRAK yazıcı modülü yapılandırması</span><span class="sxs-lookup"><span data-stu-id="b0fd9-241">BLE Printer module configuration</span></span>

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

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="b0fd9-242">BLEC2D modülü yapılandırması</span><span class="sxs-lookup"><span data-stu-id="b0fd9-242">BLEC2D Module Configuration</span></span>

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

#### <a name="routing-configuration"></a><span data-ttu-id="b0fd9-243">Yönlendirme yapılandırması</span><span class="sxs-lookup"><span data-stu-id="b0fd9-243">Routing Configuration</span></span>

<span data-ttu-id="b0fd9-244">Merhaba aşağıdaki yapılandırmayı sağlar hello aşağıdaki IOT kenar modülleri arasında yönlendirme:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-244">hello following configuration ensures hello following routing between IoT Edge modules:</span></span>

* <span data-ttu-id="b0fd9-245">Merhaba **Günlükçü** modülü alır ve tüm iletileri günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-245">hello **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="b0fd9-246">Merhaba **SensorTag** modül gönderir iletileri tooboth hello **eşleme** ve **bırak yazıcı** modüller.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-246">hello **SensorTag** module sends messages tooboth hello **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="b0fd9-247">Merhaba **eşleme** modül gönderir iletileri toohello **Iothub** tooyour IOT hub'ı gönderilen modülü toobe.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-247">hello **mapping** module sends messages toohello **IoTHub** module toobe sent up tooyour IoT Hub.</span></span>
* <span data-ttu-id="b0fd9-248">Merhaba **Iothub** modül gönderir iletileri geri toohello **eşleme** modülü.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-248">hello **IoTHub** module sends messages back toohello **mapping** module.</span></span>
* <span data-ttu-id="b0fd9-249">Merhaba **eşleme** modül gönderir iletileri toohello **BLEC2D** modülü.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-249">hello **mapping** module sends messages toohello **BLEC2D** module.</span></span>
* <span data-ttu-id="b0fd9-250">Merhaba **BLEC2D** modül gönderir iletileri geri toohello **algılayıcı etiketi** modülü.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-250">hello **BLEC2D** module sends messages back toohello **Sensor Tag** module.</span></span>

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

<span data-ttu-id="b0fd9-251">toorun hello örnek, geçişi hello yol toohello JSON yapılandırma dosyası bir parametre toohello olarak **bırak\_ağ geçidi** ikili.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-251">toorun hello sample, pass hello path toohello JSON configuration file as a parameter toohello **ble\_gateway** binary.</span></span> <span data-ttu-id="b0fd9-252">Merhaba aşağıdaki komut hello kullandığınız varsayar **gateway_sample.json** yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-252">hello following command assumes you are using hello **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="b0fd9-253">Hello bu komutu yürütmek **IOT kenar** hello Raspberry Pi'yi klasörü:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-253">Execute this command from hello **iot-edge** folder on hello Raspberry Pi:</span></span>

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="b0fd9-254">Toopress gerekebilir hello küçük düğmesini hello SensorTag aygıt toomake üzerinde bulunabilir, hello örneği çalıştırmadan önce.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-254">You may need toopress hello small button on hello SensorTag device toomake it discoverable before you run hello sample.</span></span>

<span data-ttu-id="b0fd9-255">Merhaba örneği çalıştırdığınızda, hello kullanabilirsiniz [aygıt explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) veya hello [iothub-explorer](https://github.com/Azure/iothub-explorer) aracı toomonitor hello iletileri hello IOT sınır ağ geçidi hello SensorTag aygıttan iletir.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-255">When you run hello sample, you can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toomonitor hello messages hello IoT Edge gateway forwards from hello SensorTag device.</span></span> <span data-ttu-id="b0fd9-256">Örneğin, ıothub explorer kullanarak cihaz bulut iletilerini komutu aşağıdaki hello kullanarak izleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-256">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="b0fd9-257">Buluttan cihaza iletileri gönderme</span><span class="sxs-lookup"><span data-stu-id="b0fd9-257">Send cloud-to-device messages</span></span>

<span data-ttu-id="b0fd9-258">Merhaba bırak modülü IOT hub'ı toohello aygıttan gönderen komutları da destekler.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-258">hello BLE module also supports sending commands from IoT Hub toohello device.</span></span> <span data-ttu-id="b0fd9-259">Merhaba kullanabilirsiniz [aygıt explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) veya hello [iothub-explorer](https://github.com/Azure/iothub-explorer) aracı toosend JSON iletileri bu hello bırak ağ geçidi modülü toohello bırak aygıtta iletir.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-259">You can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toosend JSON messages that hello BLE gateway module forwards on toohello BLE device.</span></span>

<span data-ttu-id="b0fd9-260">Merhaba Texas Instruments SensorTag cihaz kullanıyorsanız, IOT Hub'ından komutlar göndererek hello kırmızı LED, yeşil LED veya sesli uyaran kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-260">If you are using hello Texas Instruments SensorTag device, you can turn on hello red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="b0fd9-261">IOT Hub'ından komutları göndermeden önce ilk iki JSON iletileri sırayla aşağıdaki hello gönderin.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-261">Before you send commands from IoT Hub, first send hello following two JSON messages in order.</span></span> <span data-ttu-id="b0fd9-262">Ardından herhangi bir hello komutları tooturn hello ışık veya sesli uyaran gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0fd9-262">Then you can send any of hello commands tooturn on hello lights or buzzer.</span></span>

1. <span data-ttu-id="b0fd9-263">Tüm LED'leri ve (devre dışı bırakma) hello sesli uyaran sıfırlama:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-263">Reset all LEDs and hello buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="b0fd9-264">G/ç 'uzaktan' yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-264">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="b0fd9-265">Şimdi komutları tooturn hello ışık veya sesli uyaran hello SensorTag cihazdaki aşağıdaki hello hiçbirini gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-265">Now you can send any of hello following commands tooturn on hello lights or buzzer on hello SensorTag device:</span></span>

* <span data-ttu-id="b0fd9-266">Merhaba kırmızı LED üzerinde açın:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-266">Turn on hello red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="b0fd9-267">Merhaba yeşil LED üzerinde açın:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-267">Turn on hello green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="b0fd9-268">Merhaba sesli uyaran üzerinde açın:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-268">Turn on hello buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="b0fd9-269">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="b0fd9-269">Next Steps</span></span>

<span data-ttu-id="b0fd9-270">Toogain IOT kenar daha gelişmiş bir anlayış istiyorsanız ve bazı kod örnekleri ile denemeler hello aşağıdaki ziyaret Geliştirici öğreticiler ve kaynaklar:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-270">If you want toogain a more advanced understanding of IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="b0fd9-271">[Azure IOT kenar][lnk-sdk]</span><span class="sxs-lookup"><span data-stu-id="b0fd9-271">[Azure IoT Edge][lnk-sdk]</span></span>

<span data-ttu-id="b0fd9-272">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="b0fd9-272">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="b0fd9-273">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="b0fd9-273">[IoT Hub developer guide][lnk-devguide]</span></span>

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
