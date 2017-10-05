---
title: "Azure IOT - Ders 3 Connect Intel Edison (C): ileti gönderme | Microsoft Docs"
description: "Dağıtma ve IOT hub'ına iletileri gönderir ve ışığı yanıp Intel Edison'u bir örnek uygulamayı çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT bulut hizmeti arduino bulut için veri gönderme"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 12672b64-795a-4dfc-86fd-df53ed3eeef7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d104618ebb37a19c83f161beceb5c71bc89bbb56
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="bc1de-104">Cihaz bulut iletilerini göndermek için bir örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="bc1de-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="bc1de-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="bc1de-105">What you will do</span></span>
<span data-ttu-id="bc1de-106">Bu makalede, dağıtmak ve bir örnek uygulamanın IOT hub'ına iletileri gönderir Intel Edison'u çalıştırmak nasıl yapacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="bc1de-106">This article will show you how to deploy and run a sample application on Intel Edison that sends messages to your IoT hub.</span></span> <span data-ttu-id="bc1de-107">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="bc1de-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bc1de-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="bc1de-108">What you will learn</span></span>
<span data-ttu-id="bc1de-109">Gulp aracı dağıtmak ve örnek C uygulama Edison'u üzerinde çalıştırmak için nasıl kullanılacağını öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="bc1de-109">You will learn how to use the gulp tool to deploy and run the sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bc1de-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="bc1de-110">What you need</span></span>
* <span data-ttu-id="bc1de-111">Bu görev başlamadan önce başarılı bir şekilde tamamladınız gerekir [bir Azure işlevi uygulama ve işlemek ve IOT hub iletileri depolamak için bir depolama hesabı oluştur][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="bc1de-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="bc1de-112">IOT hub ve cihaz bağlantı dizeleri alma</span><span class="sxs-lookup"><span data-stu-id="bc1de-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="bc1de-113">Cihaz bağlantı dizesi Edison'u IOT hub'ınıza bağlanmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bc1de-113">The device connection string is used to connect Edison to your IoT hub.</span></span> <span data-ttu-id="bc1de-114">IOT hub bağlantı dizesine Edison'u IOT hub'ı temsil eden cihaz kimliği IOT hub'ınıza bağlanmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bc1de-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents Edison in the IoT hub.</span></span>

* <span data-ttu-id="bc1de-115">Kaynak grubunuzdaki tüm IOT hub aşağıdaki Azure CLI komutu çalıştırarak listesi:</span><span class="sxs-lookup"><span data-stu-id="bc1de-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="bc1de-116">Kullanım `iot-sample` değeri olarak `{resource group name}` değeri değiştirirseniz alamadık.</span><span class="sxs-lookup"><span data-stu-id="bc1de-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="bc1de-117">IOT hub bağlantı dizesine aşağıdaki Azure CLI komutu çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="bc1de-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="bc1de-118">`{my hub name}`ne zaman IOT hub'ınızı oluşturduğunuz ve Edison'u kayıtlı belirtilen adıdır.</span><span class="sxs-lookup"><span data-stu-id="bc1de-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="bc1de-119">Cihaz bağlantı dizesi, aşağıdaki komutu çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="bc1de-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="bc1de-120">Kullanım `myinteledison` değeri olarak `{device id}` değeri değiştirirseniz alamadık.</span><span class="sxs-lookup"><span data-stu-id="bc1de-120">Use `myinteledison` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="bc1de-121">Aygıt bağlantısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="bc1de-121">Configure the device connection</span></span>
1. <span data-ttu-id="bc1de-122">Yapılandırma dosyası, aşağıdaki komutları çalıştırarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="bc1de-122">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```
   > [!NOTE]
   > <span data-ttu-id="bc1de-123">Çalıştırma **yükleme araçları gulp** yanı, Ders 1'de yapmadıysanız.</span><span class="sxs-lookup"><span data-stu-id="bc1de-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="bc1de-124">Aygıt yapılandırma dosyasını açın `config-edison.json` aşağıdaki komutu çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="bc1de-124">Open the device configuration file `config-edison.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson3/config.png)

3. <span data-ttu-id="bc1de-126">İçinde aşağıdaki değişiklikleri yapın `config-edison.json` dosyası:</span><span class="sxs-lookup"><span data-stu-id="bc1de-126">Make the following replacements in the `config-edison.json` file:</span></span>

   * <span data-ttu-id="bc1de-127">Değiştir **[aygıt ana bilgisayar adı veya IP adresi]** , düşürüleceği Cihazınızı yapılandırıldığında aygıt IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="bc1de-127">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="bc1de-128">Değiştir **[IOT cihaz bağlantı dizesi]** ile `device connection string` , elde edilen.</span><span class="sxs-lookup"><span data-stu-id="bc1de-128">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="bc1de-129">Değiştir **[IOT hub bağlantı dizesine]** ile `iot hub connection string` , elde edilen.</span><span class="sxs-lookup"><span data-stu-id="bc1de-129">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bc1de-130">Gerekmeyen `azure_storage_connection_string` bu makalede.</span><span class="sxs-lookup"><span data-stu-id="bc1de-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="bc1de-131">Olduğu gibi tutun.</span><span class="sxs-lookup"><span data-stu-id="bc1de-131">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="bc1de-132">Dağıtma ve örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="bc1de-132">Deploy and run the sample application</span></span>
<span data-ttu-id="bc1de-133">Dağıtma ve aşağıdaki komutu çalıştırarak Edison'u üzerinde örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="bc1de-133">Deploy and run the sample application on Edison by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="bc1de-134">Örnek uygulama çalıştığını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="bc1de-134">Verify that the sample application works</span></span>
<span data-ttu-id="bc1de-135">Her iki saniye yanıp sönen Edison'u için bağlı LED görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc1de-135">You should see the LED that is connected to Edison blinking every two seconds.</span></span> <span data-ttu-id="bc1de-136">IŞIĞI yanıp her zaman, örnek uygulamayı IOT hub'ınıza ileti gönderir ve iletinin IOT hub'ınıza başarıyla gönderildi doğrular.</span><span class="sxs-lookup"><span data-stu-id="bc1de-136">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="bc1de-137">Ayrıca, IOT hub tarafından alınan her ileti konsol penceresinde yazdırılır.</span><span class="sxs-lookup"><span data-stu-id="bc1de-137">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="bc1de-138">Örnek uygulama, 20 ileti gönderdikten sonra otomatik olarak sona erer.</span><span class="sxs-lookup"><span data-stu-id="bc1de-138">The sample application terminates automatically after sending 20 messages.</span></span>

![Örnek uygulama ile gönderilen ve alınan iletileri][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="bc1de-140">Özet</span><span class="sxs-lookup"><span data-stu-id="bc1de-140">Summary</span></span>
<span data-ttu-id="bc1de-141">Dağıtılan artık ve IOT hub'ına cihaz bulut iletilerini göndermek için Edison'u yeni blink örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bc1de-141">You've deployed and run the new blink sample application on Edison to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="bc1de-142">Depolama hesabına yazılan gibi şimdi iletilerinizi izleyin.</span><span class="sxs-lookup"><span data-stu-id="bc1de-142">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc1de-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bc1de-143">Next steps</span></span>
<span data-ttu-id="bc1de-144">[İletileri okuma Azure Depolama'da kalıcı][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="bc1de-144">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run_c.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-c-lesson3-read-table-storage.md