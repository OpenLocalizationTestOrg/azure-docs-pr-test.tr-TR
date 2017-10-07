---
title: "Azure IOT kenarıyla IOT ağ geçidi aaaData dönüştürme | Microsoft Docs"
description: "Azure IOT kenarından özelleştirilmiş bir modül üzerinden algılayıcı veri IOT ağ geçidi tooconvert hello biçimini kullanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT ağ geçidi veri dönüştürme, IOT ağ geçidi veri dönüştürme"
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a><span data-ttu-id="2a3ff-104">Azure IOT kenarıyla algılayıcı veri dönüştürme için IOT ağ geçidi kullan</span><span class="sxs-lookup"><span data-stu-id="2a3ff-104">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>

> [!NOTE]
> <span data-ttu-id="2a3ff-105">Bu öğretici başlamadan önce sırayla dersleri aşağıdaki tamamlanmış hello olduğunuz emin olun:</span><span class="sxs-lookup"><span data-stu-id="2a3ff-105">Before you start this tutorial, make sure you’ve completed hello following lessons in sequence:</span></span>
> * [<span data-ttu-id="2a3ff-106">Intel NUC cihazını IoT ağ geçidi olarak ayarlama</span><span class="sxs-lookup"><span data-stu-id="2a3ff-106">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [<span data-ttu-id="2a3ff-107">IOT ağ geçidi tooconnect şeyler toohello bulut - SensorTag tooAzure IOT hub'ı kullanın</span><span class="sxs-lookup"><span data-stu-id="2a3ff-107">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

<span data-ttu-id="2a3ff-108">Tek bir IOT ağ geçidinin amacı, toplanan tooprocess toohello bulut göndermeden önce verilerdir.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-108">One purpose of an Iot gateway is tooprocess collected data before sending it toohello cloud.</span></span> <span data-ttu-id="2a3ff-109">Azure IOT kenar oluşturulan ve birleştirilmiş tooform hello veri işleme iş akışı olabilen modülleri tanıtır.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-109">Azure IoT Edge introduces modules which can be created and assembled tooform hello data processing workflow.</span></span> <span data-ttu-id="2a3ff-110">Bir modül bir ileti alır, üzerinde bazı eylemleri gerçekleştirir ve sonra taşıyın diğer modüller tooprocess için.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-110">A module receives a message, performs some action on it, and then move it on for other modules tooprocess.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="2a3ff-111">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="2a3ff-111">What you learn</span></span>

<span data-ttu-id="2a3ff-112">Nasıl toocreate modülü tooconvert hello SensorTag farklı bir biçime gelen iletileri öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-112">You learn how toocreate a module tooconvert messages from hello SensorTag into a different format.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="2a3ff-113">Neler</span><span class="sxs-lookup"><span data-stu-id="2a3ff-113">What you do</span></span>

* <span data-ttu-id="2a3ff-114">Bir modül tooconvert hello .json biçimine alınan bir ileti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-114">Create a module tooconvert a received message into hello .json format.</span></span>
* <span data-ttu-id="2a3ff-115">Merhaba modülü derleyin.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-115">Compile hello module.</span></span>
* <span data-ttu-id="2a3ff-116">Merhaba modülü toohello bırak örnek uygulaması, Azure IOT kenarından ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-116">Add hello module toohello BLE sample application from Azure IoT Edge.</span></span>
* <span data-ttu-id="2a3ff-117">Merhaba örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-117">Run hello sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2a3ff-118">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="2a3ff-118">What you need</span></span>

* <span data-ttu-id="2a3ff-119">aşağıdaki sırayla tamamlandı öğreticileri hello:</span><span class="sxs-lookup"><span data-stu-id="2a3ff-119">hello following tutorials completed in sequence:</span></span>
  * [<span data-ttu-id="2a3ff-120">Intel NUC cihazını IoT ağ geçidi olarak ayarlama</span><span class="sxs-lookup"><span data-stu-id="2a3ff-120">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [<span data-ttu-id="2a3ff-121">IOT ağ geçidi tooconnect şeyler toohello bulut - SensorTag tooAzure IOT hub'ı kullanın</span><span class="sxs-lookup"><span data-stu-id="2a3ff-121">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* <span data-ttu-id="2a3ff-122">Ana bilgisayar üzerinde çalışan bir SSH istemcisi.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-122">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="2a3ff-123">Putty'yi Windows önerilir.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-123">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="2a3ff-124">Linux ve macOS zaten bir SSH istemcisi ile gelir.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-124">Linux and macOS already come with an SSH client.</span></span>
* <span data-ttu-id="2a3ff-125">Başlangıç IP adresi ve hello kullanıcı adı ve parola tooaccess hello ağ geçidi'nden hello SSH istemcisi.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-125">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
* <span data-ttu-id="2a3ff-126">Bir Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-126">An Internet connection.</span></span>

## <a name="create-a-module"></a><span data-ttu-id="2a3ff-127">Bir modül oluşturma</span><span class="sxs-lookup"><span data-stu-id="2a3ff-127">Create a module</span></span>

1. <span data-ttu-id="2a3ff-128">Merhaba ana bilgisayarda hello SSH istemcisi çalıştırın ve toohello IOT ağ geçidi bağlanın.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-128">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="2a3ff-129">Hello aşağıdaki komutları çalıştırarak hello dönüştürme GitHub toohello giriş dizinine hello IOT ağ geçidi modülünden Hello kaynak dosyalarını kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="2a3ff-129">Clone hello source files of hello conversion module from GitHub toohello home directory of hello IoT gateway by running hello following commands:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   <span data-ttu-id="2a3ff-130">Merhaba C programlama dili yazılmış yerel bir Azure kenar modül budur.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-130">This is a native Azure Edge module written in hello C programming language.</span></span> <span data-ttu-id="2a3ff-131">Merhaba modülü bir aşağıdaki hello alınan iletilerin hello biçime dönüştürür:</span><span class="sxs-lookup"><span data-stu-id="2a3ff-131">hello module converts hello format of received messages into hello following one:</span></span>

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a><span data-ttu-id="2a3ff-132">Merhaba modülü derleme</span><span class="sxs-lookup"><span data-stu-id="2a3ff-132">Compile hello module</span></span>

<span data-ttu-id="2a3ff-133">toocompile hello modülü, hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2a3ff-133">toocompile hello module, run hello following commands:</span></span>

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

<span data-ttu-id="2a3ff-134">Size bir `libmy_module.so` hello derleme tamamlandıktan sonra dosya.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-134">You get a `libmy_module.so` file after hello compile is completed.</span></span> <span data-ttu-id="2a3ff-135">Bu dosyanın hello mutlak yolu not edin.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-135">Make a note of hello absolute path of this file.</span></span>

## <a name="add-hello-module-toohello-ble-sample-application"></a><span data-ttu-id="2a3ff-136">Merhaba modülü toohello bırak örnek uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="2a3ff-136">Add hello module toohello BLE sample application</span></span>

1. <span data-ttu-id="2a3ff-137">Hello aşağıdaki komutu çalıştırarak toohello örnekleri klasöre gidin:</span><span class="sxs-lookup"><span data-stu-id="2a3ff-137">Go toohello samples folder by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. <span data-ttu-id="2a3ff-138">Merhaba aşağıdaki komutu çalıştırarak Hello yapılandırma dosyasını açın:</span><span class="sxs-lookup"><span data-stu-id="2a3ff-138">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="2a3ff-139">Aşağıdaki kod toohello hello ekleyerek bir modül ekleyin `modules` bölümü.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-139">Add a module by inserting hello following code toohello `modules` section.</span></span>

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. <span data-ttu-id="2a3ff-140">Değiştir `[Your libmy_module.so path]` hello libmy_module.so hello mutlak yolu ile Merhaba kodda ' dosyası.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-140">Replace `[Your libmy_module.so path]` in hello code with hello absolute path of hello libmy_module.so\` file.</span></span>
1. <span data-ttu-id="2a3ff-141">Merhaba Hello kodla `links` bir aşağıdaki hello bölümle:</span><span class="sxs-lookup"><span data-stu-id="2a3ff-141">Replace hello code in hello `links` section with hello following one:</span></span>

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. <span data-ttu-id="2a3ff-142">Tuşuna `ESC`ve ardından `:wq` toosave hello dosya.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-142">Press `ESC`, and then type `:wq` toosave hello file.</span></span>

## <a name="run-hello-sample-application"></a><span data-ttu-id="2a3ff-143">Merhaba örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="2a3ff-143">Run hello sample application</span></span>

1. <span data-ttu-id="2a3ff-144">Merhaba SensorTag açma.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-144">Power on hello SensorTag.</span></span>
1. <span data-ttu-id="2a3ff-145">Merhaba SSL_CERT_FILE ortam değişkeni hello aşağıdaki komutu çalıştırarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="2a3ff-145">Set hello SSL_CERT_FILE environment variable by running hello following command:</span></span>

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. <span data-ttu-id="2a3ff-146">Merhaba aşağıdaki komutu çalıştırarak hello eklenen modülüyle Hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2a3ff-146">Run hello sample application with hello added module by running hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="2a3ff-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2a3ff-147">Next steps</span></span>

<span data-ttu-id="2a3ff-148">Kullanım hello IOT ağ geçidi tooconvert hello iletiden SensorTag hello .json biçime başarıyla seçtiğiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3ff-148">You’ve successfully use hello IoT gateway tooconvert hello message from SensorTag into hello .json format.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
