---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 4: Tablo depolama | Microsoft Docs"
description: "IOT hub'ınıza Intel NUC iletileri kaydetmek için bunları Azure Table depolama alanına yazmak ve bunları buluttan okuyun."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: verileri buluttan, IOT bulut hizmeti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 8ca78045-ad92-4a6a-90f1-05f9668e6f0e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 72659ef3a7fd2f6011590d37176fd05503269aff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="20cb7-104">İletileri okuma Azure tablo Depolama'da kalıcı</span><span class="sxs-lookup"><span data-stu-id="20cb7-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="20cb7-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="20cb7-105">What you will do</span></span>

- <span data-ttu-id="20cb7-106">IOT hub'ına iletileri gönderir, ağ geçidi üzerinde ağ geçidi örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="20cb7-106">Run the gateway sample application on your gateway that sends messages to your IoT hub.</span></span>
- <span data-ttu-id="20cb7-107">Daha sonra ana bilgisayarınızda Azure Table depolama alanınızın iletileri okumak için örnek kod çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="20cb7-107">Then run a sample code on your host computer to read the messages in your Azure Table storage.</span></span> 

<span data-ttu-id="20cb7-108">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="20cb7-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="20cb7-109">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="20cb7-109">What you will learn</span></span>

<span data-ttu-id="20cb7-110">Gulp aracı, Azure Table depolama iletileri okumak için örnek kod çalıştırmak için nasıl kullanılır.</span><span class="sxs-lookup"><span data-stu-id="20cb7-110">How to use the gulp tool to run the sample code to read messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="20cb7-111">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="20cb7-111">What you need</span></span>

<span data-ttu-id="20cb7-112">Başarıyla sahip aşağıdaki görevleri yapılır:</span><span class="sxs-lookup"><span data-stu-id="20cb7-112">You have have successfully done the following tasks:</span></span>

- <span data-ttu-id="20cb7-113">[Oluşturulan Azure işlev uygulaması ve Azure depolama hesabı](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="20cb7-113">[Created the Azure function app and the Azure storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="20cb7-114">[Ağ geçidi örnek uygulamayı çalıştırın](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).</span><span class="sxs-lookup"><span data-stu-id="20cb7-114">[Run the gateway sample application](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).</span></span>
- <span data-ttu-id="20cb7-115">[IOT hub'ından iletileri okumak](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).</span><span class="sxs-lookup"><span data-stu-id="20cb7-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="20cb7-116">Azure depolama bağlantı dizelerinizi Al</span><span class="sxs-lookup"><span data-stu-id="20cb7-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="20cb7-117">Bu ders erken bir Azure depolama hesabı başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="20cb7-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="20cb7-118">Azure depolama hesabı bağlantı dizesini almak için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="20cb7-118">To get the connection string of the Azure storage account, run the following commands:</span></span>

* <span data-ttu-id="20cb7-119">Tüm depolama hesaplarının listesi.</span><span class="sxs-lookup"><span data-stu-id="20cb7-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="20cb7-120">Azure depolama bağlantı dizesi alın.</span><span class="sxs-lookup"><span data-stu-id="20cb7-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="20cb7-121">IOT ağ geçidi değeri olarak kullanın `{resource group name}` Ders 2 değerinde değiştirilmediyse.</span><span class="sxs-lookup"><span data-stu-id="20cb7-121">Use iot-gateway as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="20cb7-122">Aygıt bağlantısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="20cb7-122">Configure the device connection</span></span>

<span data-ttu-id="20cb7-123">Güncelleştirme `config-azure.json` ana bilgisayarda çalışan örnek kod, Azure Table depolama iletisinde okuyabilmeniz için dosya.</span><span class="sxs-lookup"><span data-stu-id="20cb7-123">Update the `config-azure.json` file so that the sample code that runs on the host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="20cb7-124">Aygıt bağlantısını yapılandırmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="20cb7-124">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="20cb7-125">Aygıt yapılandırma dosyasını açın `config-azure.json` aşağıdaki komutları çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="20cb7-125">Open the device configuration file `config-azure.json` by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![yapılandırma](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="20cb7-127">Değiştir `[Azure storage connection string]` aldığınız Azure depolama bağlantı dizesi ile.</span><span class="sxs-lookup"><span data-stu-id="20cb7-127">Replace `[Azure storage connection string]` with the Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="20cb7-128">`[IoT hub connection string]`bölümünde değiştirilmesi gereken [Azure IOT Hub'ından iletileri okumak](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) Lesson3 içinde.</span><span class="sxs-lookup"><span data-stu-id="20cb7-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="20cb7-129">Azure Table depolama alanınızın iletileri</span><span class="sxs-lookup"><span data-stu-id="20cb7-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="20cb7-130">Ağ geçidi örnek uygulamayı çalıştırın ve aşağıdaki komutu tarafından Azure Table depolama iletilerini okuyun:</span><span class="sxs-lookup"><span data-stu-id="20cb7-130">Run the gateway sample application and read Azure Table storage messages by the following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="20cb7-131">IOT hub'ınıza ileti yeni ileti geldiğinde, Azure Table depolama alanına kaydetmek için Azure işlevi uygulamanızı tetikler.</span><span class="sxs-lookup"><span data-stu-id="20cb7-131">Your IoT hub triggers your Azure Function application to save message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="20cb7-132">`gulp run` Komutu IOT hub'ına iletileri gönderen ağ geçidi örnek uygulamayı çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="20cb7-132">The `gulp run` command runs gateway sample application that sends messages to your IoT hub.</span></span> <span data-ttu-id="20cb7-133">İle `table-storage` parametresi, bu da olarak çoğaltılır, Azure Table storage ' kaydedilmiş ileti almak için bir alt işlem.</span><span class="sxs-lookup"><span data-stu-id="20cb7-133">With `table-storage` parameter, it also spawns a child process to receive the saved message in your Azure Table storage.</span></span>

<span data-ttu-id="20cb7-134">Gönderilen ve alınan tüm iletileri anında üzerinde aynı ana bilgisayar makinesi konsol penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="20cb7-134">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="20cb7-135">Örnek uygulama örneği 40 saniye içinde otomatik olarak sona erdirir.</span><span class="sxs-lookup"><span data-stu-id="20cb7-135">The sample application instance will terminate automatically in 40 seconds.</span></span>

   ![gulp okuma](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table.png)


## <a name="summary"></a><span data-ttu-id="20cb7-137">Özet</span><span class="sxs-lookup"><span data-stu-id="20cb7-137">Summary</span></span>

<span data-ttu-id="20cb7-138">Azure işlevi uygulamanız tarafından kaydedilen, Azure Table depolama iletileri okumak için örnek kod çalıştırdıysanız.</span><span class="sxs-lookup"><span data-stu-id="20cb7-138">You've run the sample code to read the messages in your Azure Table storage saved by your Azure Function application.</span></span>