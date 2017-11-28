---
title: "Bellenim güncelleştirmeleri desteklemek için Node.js kullanarak Azure IOT paketi için Raspberry Pi'yi bağlanma | Microsoft Docs"
description: "Microsoft Azure IOT Starter Kit Böğürtlenli pi 3 kullanın ve Azure IOT paketi. Uzaktan izleme çözümüne Raspberry Pi'yi bağlanmak için kullanım Node.js telemetri algılayıcı buluta göndermek ve bir uzak bellenim güncelleştirme gerçekleştirin."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 54503d5d6a636239d240509d7d09cf334234bac7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-enable-remote-firmware-updates-using-nodejs"></a><span data-ttu-id="34bf6-104">Raspberry Pi 3 Uzaktan izleme çözümüne bağlama ve Node.js kullanarak uzak Bellenim güncelleştirmeleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="34bf6-104">Connect your Raspberry Pi 3 to the remote monitoring solution and enable remote firmware updates using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="34bf6-105">Bu öğretici Raspberry Pi 3 için Microsoft Azure IOT Starter Kit kullanmayı gösterir:</span><span class="sxs-lookup"><span data-stu-id="34bf6-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="34bf6-106">Bulut ile iletişim kurabilen bir sıcaklık ve nem okuyucu geliştirin.</span><span class="sxs-lookup"><span data-stu-id="34bf6-106">Develop a temperature and humidity reader that can communicate with the cloud.</span></span>
* <span data-ttu-id="34bf6-107">Etkinleştirmek ve bir uzak bellenim güncelleştirme için güncelleştirme istemci uygulaması Raspberry Pi'yi üzerinde gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="34bf6-107">Enable and perform a remote firmware update to update the client application on the Raspberry Pi.</span></span>

<span data-ttu-id="34bf6-108">Öğretici kullanır:</span><span class="sxs-lookup"><span data-stu-id="34bf6-108">The tutorial uses:</span></span>

- <span data-ttu-id="34bf6-109">Raspbian işletim sistemi, Node.js programlama dili ve Node.js için Microsoft Azure IOT SDK'sı bir örnek aygıt uygulamak için.</span><span class="sxs-lookup"><span data-stu-id="34bf6-109">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="34bf6-110">IOT paketi Uzaktan izleme çözümü bulut tabanlı arka uç önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="34bf6-110">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="34bf6-111">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="34bf6-111">Overview</span></span>

<span data-ttu-id="34bf6-112">Bu öğreticide, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="34bf6-112">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="34bf6-113">Önceden yapılandırılmış Uzaktan izleme çözümü örneği Azure aboneliğinize dağıtın.</span><span class="sxs-lookup"><span data-stu-id="34bf6-113">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="34bf6-114">Bu adım, otomatik olarak dağıtır ve birden çok Azure hizmetlerini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="34bf6-114">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="34bf6-115">Bilgisayarınız ve Uzaktan izleme çözümü ile iletişim kurmak için aygıt ve algılayıcılar ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="34bf6-115">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="34bf6-116">Uzaktan izleme çözümüne bağlama için örnek cihaz kod güncelleştirin ve çözüm panosunda görüntüleyebilirsiniz telemetri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="34bf6-116">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>
- <span data-ttu-id="34bf6-117">İstemci uygulaması güncelleştirmek için örnek aygıt kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="34bf6-117">Use the sample device code to update the client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="34bf6-118">Uzaktan izleme çözümü Azure aboneliğinizde Azure Hizmetleri kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="34bf6-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="34bf6-119">Dağıtım gerçek Kurumsal Mimarisi yansıtır.</span><span class="sxs-lookup"><span data-stu-id="34bf6-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="34bf6-120">Gereksiz Azure tüketim ücretleri önlemek için kendisiyle tamamladığınızda azureiotsuite.com önceden yapılandırılmış çözüm örneğiniz silin.</span><span class="sxs-lookup"><span data-stu-id="34bf6-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="34bf6-121">Önceden yapılandırılmış çözümü yeniden gerekiyorsa, kolayca yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34bf6-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="34bf6-122">Uzaktan izleme çözümü çalışırken tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="34bf6-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="34bf6-123">İndirme ve örnek yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34bf6-123">Download and configure the sample</span></span>

<span data-ttu-id="34bf6-124">Şimdi, indirin ve Uzaktan izleme istemci uygulaması, Raspberry Pi'yi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="34bf6-124">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="34bf6-125">Node.js yükleme</span><span class="sxs-lookup"><span data-stu-id="34bf6-125">Install Node.js</span></span>

<span data-ttu-id="34bf6-126">Henüz yapmadıysanız, Node.js, Raspberry Pi'yi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="34bf6-126">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="34bf6-127">Node.js için IOT SDK'sı 0.11.5 Node.js veya sonraki sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="34bf6-127">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="34bf6-128">Aşağıdaki adımlar, Raspberry Pi'yi Node.js v6.10.2 yükleme gösterir:</span><span class="sxs-lookup"><span data-stu-id="34bf6-128">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="34bf6-129">Raspberry Pi'yi güncelleştirmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="34bf6-129">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="34bf6-130">Raspberry Pi'yi Node.js ikilileri indirmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="34bf6-130">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="34bf6-131">İkili dosyaları yüklemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="34bf6-131">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="34bf6-132">Node.js v6.10.2 başarıyla yüklediniz doğrulamak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="34bf6-132">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="34bf6-133">Depoları kopyalama</span><span class="sxs-lookup"><span data-stu-id="34bf6-133">Clone the repositories</span></span>

<span data-ttu-id="34bf6-134">Henüz yapmadıysanız, gerekli depoları, Pi üzerinde aşağıdaki komutları çalıştırarak kopyalama:</span><span class="sxs-lookup"><span data-stu-id="34bf6-134">If you haven't done so already, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="34bf6-135">Güncelleştirme cihaz bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="34bf6-135">Update the device connection string</span></span>

<span data-ttu-id="34bf6-136">Örnek yapılandırma dosyasını açın **nano** Düzenleyicisi aşağıdaki komutu kullanarak:</span><span class="sxs-lookup"><span data-stu-id="34bf6-136">Open the sample configuration file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="34bf6-137">Cihaz kimliği ve oluşturulan ve bu öğreticinin başlangıcında kaydedilen IOT hub'ı bilgi yer tutucu değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="34bf6-137">Replace the placeholder values with the device id and IoT Hub information you created and saved at the start of this tutorial.</span></span>

<span data-ttu-id="34bf6-138">İşiniz bittiğinde, deviceınfo dosyasının içeriğini aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="34bf6-138">When you are done, the contents of the deviceinfo file should look like the following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="34bf6-139">Değişikliklerinizi kaydetmek (**Ctrl-O**, **Enter**) ve düzenleyiciden çıkın (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="34bf6-139">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="34bf6-140">Örnek çalıştırın</span><span class="sxs-lookup"><span data-stu-id="34bf6-140">Run the sample</span></span>

<span data-ttu-id="34bf6-141">Örnek önkoşul paketleri yüklemek için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="34bf6-141">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advance/1.0
npm install
```

<span data-ttu-id="34bf6-142">Örnek program Raspberry Pi'yi şimdi çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34bf6-142">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="34bf6-143">Aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="34bf6-143">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/1.0/remote_monitoring.js
```

<span data-ttu-id="34bf6-144">Aşağıdaki örnek çıkış Raspberry Pi'yi komut satırına bakın çıkış örneğidir:</span><span class="sxs-lookup"><span data-stu-id="34bf6-144">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Böğürtlenli Pi uygulamadan çıktı][img-raspberry-output]

<span data-ttu-id="34bf6-146">Tuşuna **Ctrl-C** herhangi bir zamanda programı'ndan çıkmak için.</span><span class="sxs-lookup"><span data-stu-id="34bf6-146">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="34bf6-147">Çözüm panosunda tıklatın **aygıtları** ziyaret etmek için **aygıtları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="34bf6-147">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="34bf6-148">Böğürtlenli Pi seçin **cihaz listesi**.</span><span class="sxs-lookup"><span data-stu-id="34bf6-148">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="34bf6-149">Ardından **yöntemleri**:</span><span class="sxs-lookup"><span data-stu-id="34bf6-149">Then choose **Methods**:</span></span>

    ![Panoda aygıtları listele][img-list-devices]

1. <span data-ttu-id="34bf6-151">Üzerinde **yöntemi çağırma** sayfasında, **InitiateFirmwareUpdate** içinde **yöntemi** açılır.</span><span class="sxs-lookup"><span data-stu-id="34bf6-151">On the **Invoke Method** page, choose **InitiateFirmwareUpdate** in the **Method** dropdown.</span></span>

1. <span data-ttu-id="34bf6-152">İçinde **FWPackageURI** alanına, **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span><span class="sxs-lookup"><span data-stu-id="34bf6-152">In the **FWPackageURI** field, enter **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span></span> <span data-ttu-id="34bf6-153">Bu dosya 2.0 sürümünde bellenimin uygulamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="34bf6-153">This file contains the implementation of version 2.0 of the firmware.</span></span>

1. <span data-ttu-id="34bf6-154">Seçin **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="34bf6-154">Choose **InvokeMethod**.</span></span> <span data-ttu-id="34bf6-155">Uygulamasını Raspberry Pi'yi çözüm panosuna geri bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="34bf6-155">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard.</span></span> <span data-ttu-id="34bf6-156">Ardından, bellenim güncelleştirme işlemi'nin yeni bellenim sürümünü indirerek başlar:</span><span class="sxs-lookup"><span data-stu-id="34bf6-156">It then starts the firmware update process by downloading the new version of the firmware:</span></span>

    ![Yöntem geçmişini göster][img-method-history]

## <a name="observe-the-firmware-update-process"></a><span data-ttu-id="34bf6-158">İşlem güncelleştirme bellenim inceleyin</span><span class="sxs-lookup"><span data-stu-id="34bf6-158">Observe the firmware update process</span></span>

<span data-ttu-id="34bf6-159">Cihazda ve çözüm panosunda bildirilen özelliklerini görüntüleyerek çalışan işlem güncelleştirme bellenim görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="34bf6-159">You can observe the firmware update process as it runs on the device and by viewing the reported properties in the solution dashboard:</span></span>

1. <span data-ttu-id="34bf6-160">Üzerinde Raspberry Pi'yi güncelleştirme işleminin devam görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="34bf6-160">You can view the progress in of the update process on the Raspberry Pi:</span></span>

    ![Güncelleştirme ilerlemesini Göster][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="34bf6-162">Güncelleştirme tamamlandığında Uzaktan izleme uygulama sessizce yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="34bf6-162">The remote monitoring app restarts silently when the update completes.</span></span> <span data-ttu-id="34bf6-163">Komutunu `ps -ef` çalıştığından doğrulanamadı.</span><span class="sxs-lookup"><span data-stu-id="34bf6-163">Use the command `ps -ef` to verify it is running.</span></span> <span data-ttu-id="34bf6-164">İşlemi sonlandırmak istiyorsanız kullanın `kill` işlem kimlikli komutu.</span><span class="sxs-lookup"><span data-stu-id="34bf6-164">If you want to terminate the process, use the `kill` command with the process id.</span></span>

1. <span data-ttu-id="34bf6-165">Çözüm Portalı'nda bir aygıt tarafından belirlendiği şekilde, bellenim güncelleştirme durumunu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34bf6-165">You can view the status of the firmware update, as reported by the device, in the solution portal.</span></span> <span data-ttu-id="34bf6-166">Aşağıdaki ekran görüntüsü durum ve süresini, güncelleştirme işlemini yeni üretici yazılımı sürümüne ve her bir aşamaya gösterir:</span><span class="sxs-lookup"><span data-stu-id="34bf6-166">The following screenshot shows the status and duration of each stage of the update process, and the new firmware version:</span></span>

    ![İş durumunu göster][img-job-status]

    <span data-ttu-id="34bf6-168">Panosuna geri gidin, cihaz yine bellenim güncelleştirme aşağıdaki telemetri gönderiyor doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34bf6-168">If you navigate back to the dashboard, you can verify the device is still sending telemetry following the firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="34bf6-169">Azure hesabınızda çalıştıran uzaktan izleme çözümü bırakırsanız çalıştırıldığında için faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="34bf6-169">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="34bf6-170">Uzaktan izleme çözümü çalışırken tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="34bf6-170">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="34bf6-171">Bunu kullanmayı bitirdikten sonra önceden yapılandırılmış çözümü Azure hesabınızdan silin.</span><span class="sxs-lookup"><span data-stu-id="34bf6-171">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34bf6-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="34bf6-172">Next steps</span></span>

<span data-ttu-id="34bf6-173">Ziyaret [Azure IOT Geliştirme Merkezi](https://azure.microsoft.com/develop/iot/) daha fazla örnekleri ve Azure IOT belgeler.</span><span class="sxs-lookup"><span data-stu-id="34bf6-173">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
