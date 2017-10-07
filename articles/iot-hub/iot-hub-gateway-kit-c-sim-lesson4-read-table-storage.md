---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - Ders 4: Tablo depolama | Microsoft Docs"
description: "Intel NUC tooyour IOT hub'ından iletileri kaydetmek için tooAzure tablo depolama yazma ve bunları hello buluttan okuyun."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: verileri buluttan, IOT bulut hizmeti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 78e4b6ea-968d-401e-a7dc-8f9acdb3ec1a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 43e299d63bbbe10d4d867af25e700c3a7cc07c53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="bb75f-104">İletileri okuma Azure tablo Depolama'da kalıcı</span><span class="sxs-lookup"><span data-stu-id="bb75f-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="bb75f-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="bb75f-105">What you will do</span></span>

- <span data-ttu-id="bb75f-106">Merhaba ağ geçidi örnek uygulaması tooyour IOT hub'ı iletileri gönderir, ağ geçidi üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bb75f-106">Run hello gateway sample application on your gateway that sends messages tooyour IoT hub.</span></span>
- <span data-ttu-id="bb75f-107">Örnek kod, Azure Table depolama, ana bilgisayar tooread iletilerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bb75f-107">Run sample code on your host computer tooread messages in your Azure Table storage.</span></span>

<span data-ttu-id="bb75f-108">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="bb75f-108">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bb75f-109">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="bb75f-109">What you will learn</span></span>

<span data-ttu-id="bb75f-110">Nasıl toouse hello aracı toorun hello örnek kodu tooread iletilerinde Azure Table depolama alanınızın gulp.</span><span class="sxs-lookup"><span data-stu-id="bb75f-110">How toouse hello gulp tool toorun hello sample code tooread messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bb75f-111">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="bb75f-111">What you need</span></span>

<span data-ttu-id="bb75f-112">Başarıyla sahip görevlerin ardından hello:</span><span class="sxs-lookup"><span data-stu-id="bb75f-112">You have have successfully done hello following tasks:</span></span>

- <span data-ttu-id="bb75f-113">[Oluşturulan Hello Azure işlev uygulaması ve hello Azure depolama hesabı](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="bb75f-113">[Created hello Azure function app and hello Azure storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="bb75f-114">[Merhaba ağ geçidi örnek uygulamayı çalıştırın](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="bb75f-114">[Run hello gateway sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>
- <span data-ttu-id="bb75f-115">[IOT hub'ından iletileri okumak](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).</span><span class="sxs-lookup"><span data-stu-id="bb75f-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="bb75f-116">Azure depolama bağlantı dizelerinizi Al</span><span class="sxs-lookup"><span data-stu-id="bb75f-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="bb75f-117">Bu ders erken bir Azure depolama hesabı başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="bb75f-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="bb75f-118">tooget hello bağlantı dizesi hello Azure depolama hesabı, hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="bb75f-118">tooget hello connection string of hello Azure storage account, run hello following commands:</span></span>

* <span data-ttu-id="bb75f-119">Tüm depolama hesaplarının listesi.</span><span class="sxs-lookup"><span data-stu-id="bb75f-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="bb75f-120">Azure depolama bağlantı dizesi alın.</span><span class="sxs-lookup"><span data-stu-id="bb75f-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="bb75f-121">Kullanım `iot-gateway` hello değeri olarak `{resource group name}` Ders 2 hello değerinde değiştirilmediyse.</span><span class="sxs-lookup"><span data-stu-id="bb75f-121">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="bb75f-122">Merhaba aygıt bağlantısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="bb75f-122">Configure hello device connection</span></span>

<span data-ttu-id="bb75f-123">Güncelleştirme hello `config-azure.json` hello ana bilgisayarda çalışan hello örnek kod, Azure Table depolama iletisinde okuyabilmeniz için dosya.</span><span class="sxs-lookup"><span data-stu-id="bb75f-123">Update hello `config-azure.json` file so that hello sample code that runs on hello host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="bb75f-124">tooconfigure Merhaba cihaz bağlantısı, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="bb75f-124">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="bb75f-125">Açık hello aygıt yapılandırma dosyası `config-azure.json` hello aşağıdaki komutları çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="bb75f-125">Open hello device configuration file `config-azure.json` by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![yapılandırma](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="bb75f-127">Değiştir `[Azure storage connection string]` hello aldığınız Azure depolama bağlantı dizesi ile.</span><span class="sxs-lookup"><span data-stu-id="bb75f-127">Replace `[Azure storage connection string]` with hello Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="bb75f-128">`[IoT hub connection string]`bölümünde değiştirilmesi gereken [Azure IOT Hub'ından iletileri okumak](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) Lesson3 içinde.</span><span class="sxs-lookup"><span data-stu-id="bb75f-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="bb75f-129">Azure Table depolama alanınızın iletileri</span><span class="sxs-lookup"><span data-stu-id="bb75f-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="bb75f-130">Merhaba ağ geçidi örnek uygulamayı çalıştırın ve Azure Table depolama iletileri komutu aşağıdaki hello tarafından okuyun:</span><span class="sxs-lookup"><span data-stu-id="bb75f-130">Run hello gateway sample application and read Azure Table storage messages by hello following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="bb75f-131">Yeni ileti geldiğinde IOT hub'ınızı Azure işlevi uygulama toosave iletinizi Azure Table depolama alanına tetikler.</span><span class="sxs-lookup"><span data-stu-id="bb75f-131">Your IoT hub triggers your Azure Function application toosave message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="bb75f-132">Merhaba `gulp run` komutu tooyour IOT hub'ı iletileri gönderir ağ geçidi örnek uygulamayı çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="bb75f-132">hello `gulp run` command runs gateway sample application that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="bb75f-133">İle `table-storage` parametresi, bu da olarak çoğaltılır ileti Azure Table storage ' kayıtlı bir alt işlem tooreceive hello.</span><span class="sxs-lookup"><span data-stu-id="bb75f-133">With `table-storage` parameter, it also spawns a child process tooreceive hello saved message in your Azure Table storage.</span></span>

<span data-ttu-id="bb75f-134">gönderilen ve alınan tüm hizmetlerde Anında hello aynı konsol penceresinde hello iletileri ana makine hello.</span><span class="sxs-lookup"><span data-stu-id="bb75f-134">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="bb75f-135">Merhaba örnek uygulama örneği 40 saniye içinde otomatik olarak sona erdirir.</span><span class="sxs-lookup"><span data-stu-id="bb75f-135">hello sample application instance will terminate automatically in 40 seconds.</span></span>

   ![gulp okuma](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table_simudev.png)


## <a name="summary"></a><span data-ttu-id="bb75f-137">Özet</span><span class="sxs-lookup"><span data-stu-id="bb75f-137">Summary</span></span>

<span data-ttu-id="bb75f-138">Azure işlevi uygulamanız tarafından kaydedilen, Azure Table depolama hello örnek kodu tooread karışılama iletileri çalıştırdıysanız.</span><span class="sxs-lookup"><span data-stu-id="bb75f-138">You've run hello sample code tooread hello messages in your Azure Table storage saved by your Azure Function application.</span></span>
