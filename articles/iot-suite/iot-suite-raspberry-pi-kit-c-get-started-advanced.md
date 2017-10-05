---
title: "Bellenim güncelleştirmeleri desteklemek için C kullanarak Azure IOT paketi için Raspberry Pi'yi bağlanma | Microsoft Docs"
description: "Microsoft Azure IOT Starter Kit Böğürtlenli pi 3 kullanın ve Azure IOT paketi. Uzaktan izleme çözümüne Raspberry Pi'yi bağlanmak için kullanım C telemetri algılayıcı buluta göndermek ve bir uzak bellenim güncelleştirme gerçekleştirin."
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
ms.openlocfilehash: f36f6512bb30e4b109b1bd1c3cdab10300f4edc9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a><span data-ttu-id="89977-104">Raspberry Pi 3 Uzaktan izleme çözümüne bağlama ve C kullanarak uzak Bellenim güncelleştirmeleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="89977-104">Connect your Raspberry Pi 3 to the remote monitoring solution and enable remote firmware updates using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="89977-105">Bu öğretici Raspberry Pi 3 için Microsoft Azure IOT Starter Kit kullanmayı gösterir:</span><span class="sxs-lookup"><span data-stu-id="89977-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="89977-106">Bulut ile iletişim kurabilen bir sıcaklık ve nem okuyucu geliştirin.</span><span class="sxs-lookup"><span data-stu-id="89977-106">Develop a temperature and humidity reader that can communicate with the cloud.</span></span>
* <span data-ttu-id="89977-107">Etkinleştirmek ve bir uzak bellenim güncelleştirme için güncelleştirme istemci uygulaması Raspberry Pi'yi üzerinde gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="89977-107">Enable and perform a remote firmware update to update the client application on the Raspberry Pi.</span></span>

<span data-ttu-id="89977-108">Öğretici kullanır:</span><span class="sxs-lookup"><span data-stu-id="89977-108">The tutorial uses:</span></span>

* <span data-ttu-id="89977-109">Raspbian işletim sistemi, C programlama dili ve C için Microsoft Azure IOT SDK'sı bir örnek aygıt uygulamak için.</span><span class="sxs-lookup"><span data-stu-id="89977-109">Raspbian OS, the C programming language, and the Microsoft Azure IoT SDK for C to implement a sample device.</span></span>
* <span data-ttu-id="89977-110">IOT paketi Uzaktan izleme çözümü bulut tabanlı arka uç önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="89977-110">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="89977-111">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="89977-111">Overview</span></span>

<span data-ttu-id="89977-112">Bu öğreticide, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="89977-112">In this tutorial, you complete the following steps:</span></span>

* <span data-ttu-id="89977-113">Önceden yapılandırılmış Uzaktan izleme çözümü örneği Azure aboneliğinize dağıtın.</span><span class="sxs-lookup"><span data-stu-id="89977-113">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="89977-114">Bu adım, otomatik olarak dağıtır ve birden çok Azure hizmetlerini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="89977-114">This step automatically deploys and configures multiple Azure services.</span></span>
* <span data-ttu-id="89977-115">Bilgisayarınız ve Uzaktan izleme çözümü ile iletişim kurmak için aygıt ve algılayıcılar ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="89977-115">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
* <span data-ttu-id="89977-116">Uzaktan izleme çözümüne bağlama için örnek cihaz kod güncelleştirin ve çözüm panosunda görüntüleyebilirsiniz telemetri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="89977-116">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>
* <span data-ttu-id="89977-117">İstemci uygulaması güncelleştirmek için örnek aygıt kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="89977-117">Use the sample device code to update the client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="89977-118">Uzaktan izleme çözümü Azure aboneliğinizde Azure Hizmetleri kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="89977-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="89977-119">Dağıtım gerçek Kurumsal Mimarisi yansıtır.</span><span class="sxs-lookup"><span data-stu-id="89977-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="89977-120">Gereksiz Azure tüketim ücretleri önlemek için kendisiyle tamamladığınızda azureiotsuite.com önceden yapılandırılmış çözüm örneğiniz silin.</span><span class="sxs-lookup"><span data-stu-id="89977-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="89977-121">Önceden yapılandırılmış çözümü yeniden gerekiyorsa, kolayca yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89977-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="89977-122">Uzaktan izleme çözümü çalışırken tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="89977-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="89977-123">İndirme ve örnek yapılandırma</span><span class="sxs-lookup"><span data-stu-id="89977-123">Download and configure the sample</span></span>

<span data-ttu-id="89977-124">Şimdi, indirin ve Uzaktan izleme istemci uygulaması, Raspberry Pi'yi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="89977-124">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-the-repositories"></a><span data-ttu-id="89977-125">Depoları kopyalama</span><span class="sxs-lookup"><span data-stu-id="89977-125">Clone the repositories</span></span>

<span data-ttu-id="89977-126">Henüz yapmadıysanız, gerekli depoları, Pi üzerinde aşağıdaki komutları çalıştırarak kopyalama:</span><span class="sxs-lookup"><span data-stu-id="89977-126">If you haven't done so already, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="89977-127">Güncelleştirme cihaz bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="89977-127">Update the device connection string</span></span>

<span data-ttu-id="89977-128">Örnek yapılandırma dosyasını açın **nano** Düzenleyicisi aşağıdaki komutu kullanarak:</span><span class="sxs-lookup"><span data-stu-id="89977-128">Open the sample configuration file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="89977-129">Oluşturulan ve bu öğreticinin başlangıcında kaydedilen cihaz kimliği ve IOT Hub bilgilerini yer tutucu değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="89977-129">Replace the placeholder values with the device ID and IoT Hub information you created and saved at the start of this tutorial.</span></span>

<span data-ttu-id="89977-130">İşiniz bittiğinde, deviceınfo dosyasının içeriğini aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="89977-130">When you are done, the contents of the deviceinfo file should look like the following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="89977-131">Değişikliklerinizi kaydetmek (**Ctrl-O**, **Enter**) ve düzenleyiciden çıkın (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="89977-131">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="build-the-sample"></a><span data-ttu-id="89977-132">Örnek oluşturma</span><span class="sxs-lookup"><span data-stu-id="89977-132">Build the sample</span></span>

<span data-ttu-id="89977-133">Zaten yapmadıysanız, önkoşul bir terminal Raspberry Pi'yi üzerinde aşağıdaki komutları çalıştırarak C için Microsoft Azure IOT cihaz SDK yükleyin:</span><span class="sxs-lookup"><span data-stu-id="89977-133">If you have not already done so, install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by running the following commands in a terminal on the Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="89977-134">Örnek çözümü Raspberry Pi'yi şimdi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="89977-134">You can now build the sample solution on the Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

<span data-ttu-id="89977-135">Örnek program Raspberry Pi'yi şimdi çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89977-135">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="89977-136">Aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="89977-136">Enter the command:</span></span>

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

<span data-ttu-id="89977-137">Aşağıdaki örnek çıkış Raspberry Pi'yi komut satırına bakın çıkış örneğidir:</span><span class="sxs-lookup"><span data-stu-id="89977-137">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Böğürtlenli Pi uygulamadan çıktı][img-raspberry-output]

<span data-ttu-id="89977-139">Tuşuna **Ctrl-C** herhangi bir zamanda programı'ndan çıkmak için.</span><span class="sxs-lookup"><span data-stu-id="89977-139">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="89977-140">Çözüm panosunda tıklatın **aygıtları** ziyaret etmek için **aygıtları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="89977-140">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="89977-141">Böğürtlenli Pi seçin **cihaz listesi**.</span><span class="sxs-lookup"><span data-stu-id="89977-141">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="89977-142">Ardından **yöntemleri**:</span><span class="sxs-lookup"><span data-stu-id="89977-142">Then choose **Methods**:</span></span>

    ![Panoda aygıtları listele][img-list-devices]

1. <span data-ttu-id="89977-144">Üzerinde **yöntemi çağırma** sayfasında, **InitiateFirmwareUpdate** içinde **yöntemi** açılır.</span><span class="sxs-lookup"><span data-stu-id="89977-144">On the **Invoke Method** page, choose **InitiateFirmwareUpdate** in the **Method** dropdown.</span></span>

1. <span data-ttu-id="89977-145">İçinde **FWPackageURI** alanına, **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span><span class="sxs-lookup"><span data-stu-id="89977-145">In the **FWPackageURI** field, enter **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span></span> <span data-ttu-id="89977-146">Bu Arşiv 2.0 sürümünde bellenimin uygulamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="89977-146">This archive file contains the implementation of version 2.0 of the firmware.</span></span>

1. <span data-ttu-id="89977-147">Seçin **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="89977-147">Choose **InvokeMethod**.</span></span> <span data-ttu-id="89977-148">Uygulamasını Raspberry Pi'yi çözüm panosuna geri bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="89977-148">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard.</span></span> <span data-ttu-id="89977-149">Ardından, bellenim güncelleştirme işlemi'nin yeni bellenim sürümünü indirerek başlar:</span><span class="sxs-lookup"><span data-stu-id="89977-149">It then starts the firmware update process by downloading the new version of the firmware:</span></span>

    ![Yöntem geçmişini göster][img-method-history]

## <a name="observe-the-firmware-update-process"></a><span data-ttu-id="89977-151">İşlem güncelleştirme bellenim inceleyin</span><span class="sxs-lookup"><span data-stu-id="89977-151">Observe the firmware update process</span></span>

<span data-ttu-id="89977-152">Cihazda ve çözüm panosunda bildirilen özelliklerini görüntüleyerek çalışan işlem güncelleştirme bellenim görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="89977-152">You can observe the firmware update process as it runs on the device and by viewing the reported properties in the solution dashboard:</span></span>

1. <span data-ttu-id="89977-153">Üzerinde Raspberry Pi'yi güncelleştirme işleminin devam görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="89977-153">You can view the progress in of the update process on the Raspberry Pi:</span></span>

    ![Güncelleştirme ilerlemesini Göster][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="89977-155">Güncelleştirme tamamlandığında Uzaktan izleme uygulama sessizce yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="89977-155">The remote monitoring app restarts silently when the update completes.</span></span> <span data-ttu-id="89977-156">Komutunu `ps -ef` çalıştığından doğrulanamadı.</span><span class="sxs-lookup"><span data-stu-id="89977-156">Use the command `ps -ef` to verify it is running.</span></span> <span data-ttu-id="89977-157">İşlemi sonlandırmak istiyorsanız kullanın `kill` işlem kimlikli komutu.</span><span class="sxs-lookup"><span data-stu-id="89977-157">If you want to terminate the process, use the `kill` command with the process id.</span></span>

1. <span data-ttu-id="89977-158">Çözüm Portalı'nda bir aygıt tarafından belirlendiği şekilde, bellenim güncelleştirme durumunu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89977-158">You can view the status of the firmware update, as reported by the device, in the solution portal.</span></span> <span data-ttu-id="89977-159">Aşağıdaki ekran görüntüsü durum ve süresini, güncelleştirme işlemini yeni üretici yazılımı sürümüne ve her bir aşamaya gösterir:</span><span class="sxs-lookup"><span data-stu-id="89977-159">The following screenshot shows the status and duration of each stage of the update process, and the new firmware version:</span></span>

    ![İş durumunu göster][img-job-status]

    <span data-ttu-id="89977-161">Panosuna geri gidin, cihaz yine bellenim güncelleştirme aşağıdaki telemetri gönderiyor doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89977-161">If you navigate back to the dashboard, you can verify the device is still sending telemetry following the firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="89977-162">Azure hesabınızda çalıştıran uzaktan izleme çözümü bırakırsanız çalıştırıldığında için faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="89977-162">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="89977-163">Uzaktan izleme çözümü çalışırken tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="89977-163">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="89977-164">Bunu kullanmayı bitirdikten sonra önceden yapılandırılmış çözümü Azure hesabınızdan silin.</span><span class="sxs-lookup"><span data-stu-id="89977-164">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89977-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="89977-165">Next steps</span></span>

<span data-ttu-id="89977-166">Ziyaret [Azure IOT Geliştirme Merkezi](https://azure.microsoft.com/develop/iot/) daha fazla örnekleri ve Azure IOT belgeler.</span><span class="sxs-lookup"><span data-stu-id="89977-166">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md