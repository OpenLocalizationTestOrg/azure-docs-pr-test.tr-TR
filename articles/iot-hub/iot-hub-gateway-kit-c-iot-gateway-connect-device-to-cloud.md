---
title: "Bir aygıt Azure IOT Hub'ına bağlanmak için bir IOT ağ geçidi kullanın | Microsoft Docs"
description: "Intel NUC IOT ağ geçidi olarak tı SensorTag bağlanmak ve bulutta Azure IOT Hub'ına algılayıcı verileri göndermek için nasıl kullanılacağını öğrenin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT ağ geçidi bulut aygıta bağlan"
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 4fb77ed0241d15338c2574fd22828507c3e40cb3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-iot-gateway-to-connect-things-to-the-cloud---sensortag-to-azure-iot-hub"></a><span data-ttu-id="dafe9-104">IOT ağ geçidi bulut - Azure IOT Hub'ına SensorTag şeyler bağlamak için kullanın</span><span class="sxs-lookup"><span data-stu-id="dafe9-104">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span></span>

> [!NOTE]
> <span data-ttu-id="dafe9-105">Bu öğretici başlamadan önce tamamlandı emin olun [Intel NUC IOT ağ geçidi olarak ayarlama](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span><span class="sxs-lookup"><span data-stu-id="dafe9-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span></span> <span data-ttu-id="dafe9-106">İçinde [Intel NUC IOT ağ geçidi olarak ayarlamak](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), Intel NUC cihazı IOT ağ geçidi olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="dafe9-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up the Intel NUC device as an IoT gateway.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="dafe9-107">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="dafe9-107">What you will learn</span></span>

<span data-ttu-id="dafe9-108">Texas Instruments SensorTag (CC2650STK) Azure IOT Hub'ına bağlanmak için bir IOT ağ geçidi kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="dafe9-108">You learn how to use an IoT gateway to connect a Texas Instruments SensorTag (CC2650STK) to Azure IoT Hub.</span></span> <span data-ttu-id="dafe9-109">IOT ağ geçidi sıcaklık ve nem verileri toplanan SensorTag Azure IOT Hub'ına gönderir.</span><span class="sxs-lookup"><span data-stu-id="dafe9-109">The IoT gateway sends temperature and humidity data collected from the SensorTag to Azure IoT Hub.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="dafe9-110">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="dafe9-110">What you will do</span></span>

- <span data-ttu-id="dafe9-111">IOT hub'ı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dafe9-111">Create an IoT hub.</span></span>
- <span data-ttu-id="dafe9-112">Bir cihaz IOT hub'ı SensorTag için kaydetme.</span><span class="sxs-lookup"><span data-stu-id="dafe9-112">Register a device in the IoT hub for the SensorTag.</span></span>
- <span data-ttu-id="dafe9-113">IOT ağ geçidi ve SensorTag arasındaki bağlantıyı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="dafe9-113">Enable the connection between the IoT gateway and the SensorTag.</span></span>
- <span data-ttu-id="dafe9-114">IOT hub'ınıza SensorTag veri göndermek için bırak örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="dafe9-114">Run a BLE sample application to send SensorTag data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="dafe9-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="dafe9-115">What you need</span></span>

- <span data-ttu-id="dafe9-116">Öğretici [Intel NUC IOT ağ geçidi olarak ayarlama](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) tamamlandı, Intel NUC IOT ağ geçidi olarak ayarlamanız içinde.</span><span class="sxs-lookup"><span data-stu-id="dafe9-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span></span>
- * <span data-ttu-id="dafe9-117">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="dafe9-117">An active Azure subscription.</span></span> <span data-ttu-id="dafe9-118">Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="dafe9-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
- <span data-ttu-id="dafe9-119">Ana bilgisayar üzerinde çalışan bir SSH istemcisi.</span><span class="sxs-lookup"><span data-stu-id="dafe9-119">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="dafe9-120">Putty'yi Windows önerilir.</span><span class="sxs-lookup"><span data-stu-id="dafe9-120">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="dafe9-121">Linux ve macOS zaten bir SSH istemcisi ile gelir.</span><span class="sxs-lookup"><span data-stu-id="dafe9-121">Linux and macOS already come with an SSH client.</span></span>
- <span data-ttu-id="dafe9-122">IP adresi ve kullanıcı adı ve SSH istemciden ağ geçidi erişim için parola.</span><span class="sxs-lookup"><span data-stu-id="dafe9-122">The IP address and the username and password to access the gateway from the SSH client.</span></span>
- <span data-ttu-id="dafe9-123">Bir Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="dafe9-123">An Internet connection.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> <span data-ttu-id="dafe9-124">Burada, SensorTag için bu yeni cihaz kaydedilir</span><span class="sxs-lookup"><span data-stu-id="dafe9-124">Here you register this new device for your SensorTag</span></span>

## <a name="enable-the-connection-between-the-iot-gateway-and-the-sensortag"></a><span data-ttu-id="dafe9-125">IOT ağ geçidi SensorTag arasındaki bağlantıyı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="dafe9-125">Enable the connection between the IoT gateway and the SensorTag</span></span>

<span data-ttu-id="dafe9-126">Bu bölümde, aşağıdaki görevleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dafe9-126">In this section, you perform the following tasks:</span></span>

- <span data-ttu-id="dafe9-127">Bluetooth bağlantısı için SensorTag MAC adresini alın.</span><span class="sxs-lookup"><span data-stu-id="dafe9-127">Get the MAC address of the SensorTag for Bluetooth connection.</span></span>
- <span data-ttu-id="dafe9-128">SensorTag IOT ağ geçidi bir Bluetooth bağlantısını başlatma.</span><span class="sxs-lookup"><span data-stu-id="dafe9-128">Initiate a Bluetooth connection from the IoT gateway to the SensorTag.</span></span>

### <a name="get-the-mac-address-of-the-sensortag-for-bluetooth-connection"></a><span data-ttu-id="dafe9-129">Bluetooth bağlantısı için SensorTag MAC adresini alın</span><span class="sxs-lookup"><span data-stu-id="dafe9-129">Get the MAC address of the SensorTag for Bluetooth connection</span></span>

1. <span data-ttu-id="dafe9-130">Ana bilgisayarda SSH istemcisi çalıştırın ve IOT ağ geçidi bağlanın.</span><span class="sxs-lookup"><span data-stu-id="dafe9-130">On the host computer, run the SSH client and connect to the IoT gateway.</span></span>
1. <span data-ttu-id="dafe9-131">Bluetooth engellemesini kaldırmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="dafe9-131">Unblock Bluetooth by running the following command:</span></span>

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. <span data-ttu-id="dafe9-132">IOT ağ geçidi Bluetooth hizmetini başlatın ve aşağıdaki komutları çalıştırarak Bluetooth yapılandırmak için Bluetooth Kabuk girin:</span><span class="sxs-lookup"><span data-stu-id="dafe9-132">Start the Bluetooth service on the IoT gateway and enter a Bluetooth shell to configure Bluetooth by running the following commands:</span></span>

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. <span data-ttu-id="dafe9-133">Güç açma Bluetooth Kabuk aşağıdaki komutu çalıştırarak Bluetooth denetleyici:</span><span class="sxs-lookup"><span data-stu-id="dafe9-133">Power on the Bluetooth controller by running the following command at the Bluetooth shell:</span></span>

   ```bash
   power on
   ```

   ![IOT ağ geçidi bluetoothctl ile Bluetooth denetleyicide güç](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="dafe9-135">Yakındaki Bluetooth cihazları için aşağıdaki komutu çalıştırarak Taramayı Başlat:</span><span class="sxs-lookup"><span data-stu-id="dafe9-135">Start scanning for nearby Bluetooth devices by running the following command:</span></span>

   ```bash
   scan on
   ```

   ![Bluetoothctl ile Bluetooth cihazları yakındaki tarama](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="dafe9-137">Üzerinde SensorTag eşleştirme düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="dafe9-137">Press the pairing button on the SensorTag.</span></span> <span data-ttu-id="dafe9-138">Yeşil SensorTag yanıp sönen üzerinde GEREKTİRİYORDU.</span><span class="sxs-lookup"><span data-stu-id="dafe9-138">The green LED on the SensorTag flashes.</span></span>
1. <span data-ttu-id="dafe9-139">Bluetooth Kabuk SensorTag bulunan görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="dafe9-139">At the Bluetooth shell, you should see the SensorTag is found.</span></span> <span data-ttu-id="dafe9-140">SensorTag MAC adresini not edin.</span><span class="sxs-lookup"><span data-stu-id="dafe9-140">Make a note of the MAC address of the SensorTag.</span></span> <span data-ttu-id="dafe9-141">Bu örnekte, SensorTag MAC adresidir `24:71:89:C0:7F:82`.</span><span class="sxs-lookup"><span data-stu-id="dafe9-141">In this example, the MAC address of the SensorTag is `24:71:89:C0:7F:82`.</span></span>
1. <span data-ttu-id="dafe9-142">Aşağıdaki komutu çalıştırarak taramayı devre dışı bırakın:</span><span class="sxs-lookup"><span data-stu-id="dafe9-142">Turn off the scan by running the following command:</span></span>

   ```bash
   scan off
   ```

   ![Bluetoothctl ile Bluetooth cihazları yakındaki Taramayı Durdur](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-the-iot-gateway-to-the-sensortag"></a><span data-ttu-id="dafe9-144">SensorTag IOT ağ geçidi bir Bluetooth bağlantısını başlatma</span><span class="sxs-lookup"><span data-stu-id="dafe9-144">Initiate a Bluetooth connection from the IoT gateway to the SensorTag</span></span>

1. <span data-ttu-id="dafe9-145">Aşağıdaki komutu çalıştırarak SensorTag Bağlan:</span><span class="sxs-lookup"><span data-stu-id="dafe9-145">Connect to the SensorTag by running the following command:</span></span>

   ```bash
   connect <MAC address>
   ```

   ![SensorTag bluetoothctl ile bağlanma](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="dafe9-147">SensorTag kesin ve aşağıdaki komutları çalıştırarak Bluetooth kabuktan çıkış:</span><span class="sxs-lookup"><span data-stu-id="dafe9-147">Disconnect from the SensorTag and exit the Bluetooth shell by running the following commands:</span></span>

   ```bash
   disconnect
   exit
   ```

   ![SensorTag bluetoothctl ile bağlantısını kesin](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

<span data-ttu-id="dafe9-149">SensorTag ve IOT ağ geçidi arasındaki bağlantı başarıyla etkinleştirdikten.</span><span class="sxs-lookup"><span data-stu-id="dafe9-149">You've successfully enabled the connection between the SensorTag and the IoT gateway.</span></span>

## <a name="run-a-ble-sample-application-to-send-sensortag-data-to-your-iot-hub"></a><span data-ttu-id="dafe9-150">IOT hub'ınıza SensorTag veri göndermek için bırak örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="dafe9-150">Run a BLE sample application to send SensorTag data to your IoT hub</span></span>

<span data-ttu-id="dafe9-151">Bluetooth düşük enerji (bırak) örnek uygulaması, Azure IOT kenar tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="dafe9-151">The Bluetooth Low Energy (BLE) sample application is provided by Azure IoT Edge.</span></span> <span data-ttu-id="dafe9-152">Örnek uygulama bırak bağlantısından veri toplar ve verileri, IOT hub'ına gönderin.</span><span class="sxs-lookup"><span data-stu-id="dafe9-152">The sample application collects data from BLE connection and send the data to you IoT hub.</span></span> <span data-ttu-id="dafe9-153">Örnek uygulamayı çalıştırmak için aktarmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="dafe9-153">To run the sample application, you need to:</span></span>

1. <span data-ttu-id="dafe9-154">Örnek uygulamayı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="dafe9-154">Configure the sample application.</span></span>
1. <span data-ttu-id="dafe9-155">Örnek uygulamayı IOT ağ geçidi üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="dafe9-155">Run the sample application on the IoT gateway.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="dafe9-156">Örnek uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dafe9-156">Configure the sample application</span></span>

1. <span data-ttu-id="dafe9-157">Aşağıdaki komutu çalıştırarak örnek uygulamasının klasöre gidin:</span><span class="sxs-lookup"><span data-stu-id="dafe9-157">Go to the folder of the sample application by running the following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. <span data-ttu-id="dafe9-158">Aşağıdaki komutu çalıştırarak yapılandırma dosyasını açın:</span><span class="sxs-lookup"><span data-stu-id="dafe9-158">Open the configuration file by running the following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="dafe9-159">Yapılandırma dosyasında aşağıdaki değerleri doldurun:</span><span class="sxs-lookup"><span data-stu-id="dafe9-159">In the configuration file, fill in the following values:</span></span>

   <span data-ttu-id="dafe9-160">**IoTHubName**: IOT hub'ın adı.</span><span class="sxs-lookup"><span data-stu-id="dafe9-160">**IoTHubName**: The name of your IoT hub.</span></span>

   <span data-ttu-id="dafe9-161">**IoTHubSuffix**: Get IoTHubSuffix anahtarından aşağı not ettiğiniz birincil aygıt bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="dafe9-161">**IoTHubSuffix**: Get IoTHubSuffix from the primary key of the device connection string that you noted down.</span></span> <span data-ttu-id="dafe9-162">Birincil anahtar, cihaz bağlantı dizesi, birincil anahtarı değil, IOT hub bağlantı dizesine elde etmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="dafe9-162">Ensure that you get the primary key of the device connection string, not the primary key of your IoT hub connection string.</span></span> <span data-ttu-id="dafe9-163">Birincil aygıt bağlantı dizesinin biçiminde anahtarıdır `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span><span class="sxs-lookup"><span data-stu-id="dafe9-163">The primary key of the device connection string is in the format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span></span>

   <span data-ttu-id="dafe9-164">**Aktarım**: varsayılan değer `amqp`.</span><span class="sxs-lookup"><span data-stu-id="dafe9-164">**Transport**: The default value is `amqp`.</span></span> <span data-ttu-id="dafe9-165">Bu değer protokolü sırasında transpotation gösterir.</span><span class="sxs-lookup"><span data-stu-id="dafe9-165">This value shows the protocol during transpotation.</span></span> <span data-ttu-id="dafe9-166">Olabilir `http`, `amqp`, veya `mqtt`.</span><span class="sxs-lookup"><span data-stu-id="dafe9-166">It could be `http`, `amqp`, or `mqtt`.</span></span>

   <span data-ttu-id="dafe9-167">**macAddress**: aşağı ettiğiniz SensorTag MAC adresidir.</span><span class="sxs-lookup"><span data-stu-id="dafe9-167">**macAddress**: The MAC address of the SensorTag that you noted down.</span></span>

   <span data-ttu-id="dafe9-168">**DeviceID**: IOT hub'ınıza oluşturduğunuz cihaz kimliği.</span><span class="sxs-lookup"><span data-stu-id="dafe9-168">**deviceID**: ID of the device that you created in your IoT hub.</span></span>

   <span data-ttu-id="dafe9-169">**deviceKey**: birincil anahtar, cihaz bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="dafe9-169">**deviceKey**: The primary key of the device connection string.</span></span>

   ![Yapılandırma dosyası bırak örnek uygulamasının tamamlayın](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. <span data-ttu-id="dafe9-171">Tuşuna `ESC` ve türü `:wq` dosyayı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="dafe9-171">Press `ESC` and type `:wq` to save the file.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="dafe9-172">Örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="dafe9-172">Run the sample application</span></span>

1. <span data-ttu-id="dafe9-173">SensorTag açık olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="dafe9-173">Make sure the SensorTag is powered on.</span></span>
1. <span data-ttu-id="dafe9-174">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="dafe9-174">Run the following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="dafe9-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dafe9-175">Next steps</span></span>

[<span data-ttu-id="dafe9-176">Azure IOT kenarıyla algılayıcı veri dönüştürme için IOT ağ geçidi kullan</span><span class="sxs-lookup"><span data-stu-id="dafe9-176">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
