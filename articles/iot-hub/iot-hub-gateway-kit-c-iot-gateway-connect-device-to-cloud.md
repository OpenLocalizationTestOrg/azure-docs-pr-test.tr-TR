---
title: "aaaUse IOT ağ geçidi tooconnect aygıt tooAzure IOT hub'ı | Microsoft Docs"
description: "Toouse IOT ağ geçidi tooconnect tı SensorTag olarak Intel NUC ve gönderme algılayıcı verileri tooAzure IOT hub'ı hello nasıl bulut öğrenin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT ağ geçidi aygıtı toocloud Bağlan"
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a><span data-ttu-id="a4767-104">IOT ağ geçidi tooconnect şeyler toohello bulut - SensorTag tooAzure IOT hub'ı kullanın</span><span class="sxs-lookup"><span data-stu-id="a4767-104">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>

> [!NOTE]
> <span data-ttu-id="a4767-105">Bu öğretici başlamadan önce tamamlandı emin olun [Intel NUC IOT ağ geçidi olarak ayarlama](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span><span class="sxs-lookup"><span data-stu-id="a4767-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span></span> <span data-ttu-id="a4767-106">İçinde [Intel NUC IOT ağ geçidi olarak ayarlamak](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), hello Intel NUC cihazı IOT ağ geçidi olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a4767-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up hello Intel NUC device as an IoT gateway.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a4767-107">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="a4767-107">What you will learn</span></span>

<span data-ttu-id="a4767-108">Hakkında bilgi edineceksiniz nasıl toouse IOT ağ geçidi tooconnect Texas Instruments SensorTag (CC2650STK) tooAzure IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="a4767-108">You learn how toouse an IoT gateway tooconnect a Texas Instruments SensorTag (CC2650STK) tooAzure IoT Hub.</span></span> <span data-ttu-id="a4767-109">Merhaba IOT ağ geçidi sıcaklık gönderir ve hello SensorTag tooAzure IOT hub'ı toplanan nem veriler.</span><span class="sxs-lookup"><span data-stu-id="a4767-109">hello IoT gateway sends temperature and humidity data collected from hello SensorTag tooAzure IoT Hub.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a4767-110">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="a4767-110">What you will do</span></span>

- <span data-ttu-id="a4767-111">IOT hub'ı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4767-111">Create an IoT hub.</span></span>
- <span data-ttu-id="a4767-112">Merhaba IOT hub'hello SensorTag için bir cihaz kaydetme.</span><span class="sxs-lookup"><span data-stu-id="a4767-112">Register a device in hello IoT hub for hello SensorTag.</span></span>
- <span data-ttu-id="a4767-113">Merhaba IOT ağ geçidi hello SensorTag arasında Hello bağlantı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a4767-113">Enable hello connection between hello IoT gateway and hello SensorTag.</span></span>
- <span data-ttu-id="a4767-114">Bir bırak örnek uygulama toosend SensorTag veri tooyour IOT hub'ı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a4767-114">Run a BLE sample application toosend SensorTag data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a4767-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="a4767-115">What you need</span></span>

- <span data-ttu-id="a4767-116">Öğretici [Intel NUC IOT ağ geçidi olarak ayarlama](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) tamamlandı, Intel NUC IOT ağ geçidi olarak ayarlamanız içinde.</span><span class="sxs-lookup"><span data-stu-id="a4767-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span></span>
- * <span data-ttu-id="a4767-117">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="a4767-117">An active Azure subscription.</span></span> <span data-ttu-id="a4767-118">Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="a4767-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
- <span data-ttu-id="a4767-119">Ana bilgisayar üzerinde çalışan bir SSH istemcisi.</span><span class="sxs-lookup"><span data-stu-id="a4767-119">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="a4767-120">Putty'yi Windows önerilir.</span><span class="sxs-lookup"><span data-stu-id="a4767-120">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="a4767-121">Linux ve macOS zaten bir SSH istemcisi ile gelir.</span><span class="sxs-lookup"><span data-stu-id="a4767-121">Linux and macOS already come with an SSH client.</span></span>
- <span data-ttu-id="a4767-122">Başlangıç IP adresi ve hello kullanıcı adı ve parola tooaccess hello ağ geçidi'nden hello SSH istemcisi.</span><span class="sxs-lookup"><span data-stu-id="a4767-122">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
- <span data-ttu-id="a4767-123">Bir Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="a4767-123">An Internet connection.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> <span data-ttu-id="a4767-124">Burada, SensorTag için bu yeni cihaz kaydedilir</span><span class="sxs-lookup"><span data-stu-id="a4767-124">Here you register this new device for your SensorTag</span></span>

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a><span data-ttu-id="a4767-125">Merhaba IOT ağ geçidi hello SensorTag arasındaki Hello bağlantıyı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a4767-125">Enable hello connection between hello IoT gateway and hello SensorTag</span></span>

<span data-ttu-id="a4767-126">Bu bölümde, hello aşağıdaki görevleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a4767-126">In this section, you perform hello following tasks:</span></span>

- <span data-ttu-id="a4767-127">Bluetooth bağlantısı için hello SensorTag Hello MAC adresini alın.</span><span class="sxs-lookup"><span data-stu-id="a4767-127">Get hello MAC address of hello SensorTag for Bluetooth connection.</span></span>
- <span data-ttu-id="a4767-128">Merhaba IOT ağ geçidi toohello SensorTag bir Bluetooth bağlantısını başlatma.</span><span class="sxs-lookup"><span data-stu-id="a4767-128">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag.</span></span>

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a><span data-ttu-id="a4767-129">Merhaba SensorTag Hello MAC adresi için Bluetooth bağlantısını Al</span><span class="sxs-lookup"><span data-stu-id="a4767-129">Get hello MAC address of hello SensorTag for Bluetooth connection</span></span>

1. <span data-ttu-id="a4767-130">Merhaba ana bilgisayarda hello SSH istemcisi çalıştırın ve toohello IOT ağ geçidi bağlanın.</span><span class="sxs-lookup"><span data-stu-id="a4767-130">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="a4767-131">Bluetooth hello aşağıdaki komutu çalıştırarak Engellemeyi Kaldır:</span><span class="sxs-lookup"><span data-stu-id="a4767-131">Unblock Bluetooth by running hello following command:</span></span>

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. <span data-ttu-id="a4767-132">Merhaba IOT ağ geçidi'nde Hello Bluetooth hizmetini başlatın ve aşağıdaki komutları çalıştırarak Bluetooth hello Bluetooth Kabuk tooconfigure girin:</span><span class="sxs-lookup"><span data-stu-id="a4767-132">Start hello Bluetooth service on hello IoT gateway and enter a Bluetooth shell tooconfigure Bluetooth by running hello following commands:</span></span>

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. <span data-ttu-id="a4767-133">Güç çalıştırarak hello Bluetooth denetleyicisinde hello hello Bluetooth Kabuk komut aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="a4767-133">Power on hello Bluetooth controller by running hello following command at hello Bluetooth shell:</span></span>

   ```bash
   power on
   ```

   ![Merhaba IOT bluetoothctl ağ geçidiyle hello Bluetooth denetleyicide güç](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="a4767-135">Yakındaki Bluetooth aygıtlar hello aşağıdaki komutu çalıştırarak Taramayı Başlat:</span><span class="sxs-lookup"><span data-stu-id="a4767-135">Start scanning for nearby Bluetooth devices by running hello following command:</span></span>

   ```bash
   scan on
   ```

   ![Bluetoothctl ile Bluetooth cihazları yakındaki tarama](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="a4767-137">Merhaba SensorTag düğmesinde eşleştirme hello tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="a4767-137">Press hello pairing button on hello SensorTag.</span></span> <span data-ttu-id="a4767-138">Merhaba yeşil hello SensorTag yanıp sönen üzerinde GEREKTİRİYORDU.</span><span class="sxs-lookup"><span data-stu-id="a4767-138">hello green LED on hello SensorTag flashes.</span></span>
1. <span data-ttu-id="a4767-139">Merhaba Bluetooth Kabuk SensorTag bulunan hello görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4767-139">At hello Bluetooth shell, you should see hello SensorTag is found.</span></span> <span data-ttu-id="a4767-140">Merhaba hello SensorTag MAC adresini not edin.</span><span class="sxs-lookup"><span data-stu-id="a4767-140">Make a note of hello MAC address of hello SensorTag.</span></span> <span data-ttu-id="a4767-141">Bu örnekte, hello hello SensorTag MAC adresi olan `24:71:89:C0:7F:82`.</span><span class="sxs-lookup"><span data-stu-id="a4767-141">In this example, hello MAC address of hello SensorTag is `24:71:89:C0:7F:82`.</span></span>
1. <span data-ttu-id="a4767-142">Merhaba aşağıdaki komutu çalıştırarak Hello tarama devre dışı bırakın:</span><span class="sxs-lookup"><span data-stu-id="a4767-142">Turn off hello scan by running hello following command:</span></span>

   ```bash
   scan off
   ```

   ![Bluetoothctl ile Bluetooth cihazları yakındaki Taramayı Durdur](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a><span data-ttu-id="a4767-144">Merhaba IOT ağ geçidi toohello SensorTag bir Bluetooth bağlantısını başlatma</span><span class="sxs-lookup"><span data-stu-id="a4767-144">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag</span></span>

1. <span data-ttu-id="a4767-145">Toohello SensorTag hello aşağıdaki komutu çalıştırarak Bağlan:</span><span class="sxs-lookup"><span data-stu-id="a4767-145">Connect toohello SensorTag by running hello following command:</span></span>

   ```bash
   connect <MAC address>
   ```

   ![Toohello SensorTag bluetoothctl ile bağlanma](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="a4767-147">Merhaba SensorTag çıkarın ve hello aşağıdaki komutları çalıştırarak hello Bluetooth kabuktan çıkış:</span><span class="sxs-lookup"><span data-stu-id="a4767-147">Disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

   ```bash
   disconnect
   exit
   ```

   ![Merhaba SensorTag bluetoothctl ile bağlantısını kesin](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

<span data-ttu-id="a4767-149">Merhaba SensorTag hello IOT ağ geçidi arasında hello bağlantısı başarıyla etkinleştirdikten.</span><span class="sxs-lookup"><span data-stu-id="a4767-149">You've successfully enabled hello connection between hello SensorTag and hello IoT gateway.</span></span>

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a><span data-ttu-id="a4767-150">Bir bırak örnek uygulama toosend SensorTag veri tooyour IOT hub çalıştırın</span><span class="sxs-lookup"><span data-stu-id="a4767-150">Run a BLE sample application toosend SensorTag data tooyour IoT hub</span></span>

<span data-ttu-id="a4767-151">Merhaba Bluetooth düşük enerji (bırak) örnek uygulaması, Azure IOT kenar tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a4767-151">hello Bluetooth Low Energy (BLE) sample application is provided by Azure IoT Edge.</span></span> <span data-ttu-id="a4767-152">Merhaba örnek uygulaması bırak bağlantısından veri toplar ve hello veri tooyou IOT hub'ı gönderin.</span><span class="sxs-lookup"><span data-stu-id="a4767-152">hello sample application collects data from BLE connection and send hello data tooyou IoT hub.</span></span> <span data-ttu-id="a4767-153">toorun Merhaba örnek uygulaması, şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a4767-153">toorun hello sample application, you need to:</span></span>

1. <span data-ttu-id="a4767-154">Merhaba örnek uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a4767-154">Configure hello sample application.</span></span>
1. <span data-ttu-id="a4767-155">Merhaba IOT ağ geçidi'nde Hello örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a4767-155">Run hello sample application on hello IoT gateway.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="a4767-156">Merhaba örnek uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a4767-156">Configure hello sample application</span></span>

1. <span data-ttu-id="a4767-157">Merhaba aşağıdaki komutu çalıştırarak Merhaba örnek uygulaması toohello klasörüne gidin:</span><span class="sxs-lookup"><span data-stu-id="a4767-157">Go toohello folder of hello sample application by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. <span data-ttu-id="a4767-158">Merhaba aşağıdaki komutu çalıştırarak Hello yapılandırma dosyasını açın:</span><span class="sxs-lookup"><span data-stu-id="a4767-158">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="a4767-159">Merhaba yapılandırma dosyasında aşağıdaki değerleri hello doldurun:</span><span class="sxs-lookup"><span data-stu-id="a4767-159">In hello configuration file, fill in hello following values:</span></span>

   <span data-ttu-id="a4767-160">**IoTHubName**: IOT hub'ınızı hello adı.</span><span class="sxs-lookup"><span data-stu-id="a4767-160">**IoTHubName**: hello name of your IoT hub.</span></span>

   <span data-ttu-id="a4767-161">**IoTHubSuffix**: Get IoTHubSuffix aşağı not ettiğiniz hello birincil anahtarı hello cihaz bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="a4767-161">**IoTHubSuffix**: Get IoTHubSuffix from hello primary key of hello device connection string that you noted down.</span></span> <span data-ttu-id="a4767-162">Merhaba birincil anahtarı hello cihaz bağlantı dizesi alma, IOT hub bağlantı dizenizi birincil anahtarı hello değil emin olun.</span><span class="sxs-lookup"><span data-stu-id="a4767-162">Ensure that you get hello primary key of hello device connection string, not hello primary key of your IoT hub connection string.</span></span> <span data-ttu-id="a4767-163">Merhaba birincil hello cihaz bağlantı dizesi anahtarıdır hello biçiminde `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span><span class="sxs-lookup"><span data-stu-id="a4767-163">hello primary key of hello device connection string is in hello format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span></span>

   <span data-ttu-id="a4767-164">**Aktarım**: hello varsayılan değer `amqp`.</span><span class="sxs-lookup"><span data-stu-id="a4767-164">**Transport**: hello default value is `amqp`.</span></span> <span data-ttu-id="a4767-165">Bu değer hello protokolü sırasında transpotation gösterir.</span><span class="sxs-lookup"><span data-stu-id="a4767-165">This value shows hello protocol during transpotation.</span></span> <span data-ttu-id="a4767-166">Olabilir `http`, `amqp`, veya `mqtt`.</span><span class="sxs-lookup"><span data-stu-id="a4767-166">It could be `http`, `amqp`, or `mqtt`.</span></span>

   <span data-ttu-id="a4767-167">**macAddress**: hello aşağı ettiğiniz SensorTag MAC adresini hello.</span><span class="sxs-lookup"><span data-stu-id="a4767-167">**macAddress**: hello MAC address of hello SensorTag that you noted down.</span></span>

   <span data-ttu-id="a4767-168">**DeviceID**: IOT hub'ınıza oluşturulan hello aygıtın kimliği.</span><span class="sxs-lookup"><span data-stu-id="a4767-168">**deviceID**: ID of hello device that you created in your IoT hub.</span></span>

   <span data-ttu-id="a4767-169">**deviceKey**: hello birincil anahtar hello cihaz bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="a4767-169">**deviceKey**: hello primary key of hello device connection string.</span></span>

   ![Merhaba bırak örnek uygulaması, tam hello yapılandırma dosyası](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. <span data-ttu-id="a4767-171">Tuşuna `ESC` ve türü `:wq` toosave hello dosya.</span><span class="sxs-lookup"><span data-stu-id="a4767-171">Press `ESC` and type `:wq` toosave hello file.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="a4767-172">Merhaba örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="a4767-172">Run hello sample application</span></span>

1. <span data-ttu-id="a4767-173">SensorTag açık olduğundan emin hello olun.</span><span class="sxs-lookup"><span data-stu-id="a4767-173">Make sure hello SensorTag is powered on.</span></span>
1. <span data-ttu-id="a4767-174">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a4767-174">Run hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="a4767-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a4767-175">Next steps</span></span>

[<span data-ttu-id="a4767-176">Azure IOT kenarıyla algılayıcı veri dönüştürme için IOT ağ geçidi kullan</span><span class="sxs-lookup"><span data-stu-id="a4767-176">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
