---
title: "aaaHow tooadd bir IOT hub'ı olay kaynağı tooyour Azure zaman serisi Öngörüler ortam | Microsoft Docs"
description: "Bu öğretici bir olay kaynağı başka bir deyişle tooadd tooan IOT hub'ı tooyour zaman serisi Öngörüler ortamı nasıl bağlanacağını kapsar"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: c626f9653d1c012360120fa9fc3d211d7d5beb5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-iot-hub-event-source"></a><span data-ttu-id="deaed-103">Nasıl tooadd bir IOT hub'ı olay kaynağı</span><span class="sxs-lookup"><span data-stu-id="deaed-103">How tooadd an IoT Hub event source</span></span>

<span data-ttu-id="deaed-104">Bu öğretici nasıl toouse hello Azure portal tooadd bir IOT hub'ı tooyour zaman serisi Öngörüler ortamından okuyan bir olay kaynağı kapsar.</span><span class="sxs-lookup"><span data-stu-id="deaed-104">This tutorial covers how toouse hello Azure portal tooadd an event source that reads from an IoT Hub tooyour Time Series Insights environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="deaed-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="deaed-105">Prerequisites</span></span>

<span data-ttu-id="deaed-106">Bir IOT Hub oluşturdunuz ve olayları tooit yazma.</span><span class="sxs-lookup"><span data-stu-id="deaed-106">You have created an IoT Hub and are writing events tooit.</span></span> <span data-ttu-id="deaed-107">IOT hub'ları hakkında daha fazla bilgi için bkz: <https://azure.microsoft.com/services/iot-hub/></span><span class="sxs-lookup"><span data-stu-id="deaed-107">For more information on IoT Hubs, see <https://azure.microsoft.com/services/iot-hub/></span></span>

> <span data-ttu-id="deaed-108">[Tüketici grupları] Her zaman serisi Öngörüler olay kaynağı ile herhangi bir tüketiciye paylaşılmayan kendi ayrılmış bir tüketici grubundaki toohave gerekir.</span><span class="sxs-lookup"><span data-stu-id="deaed-108">[Consumer Groups] Each Time Series Insights event source needs toohave its own dedicated consumer group that is not shared with any other consumers.</span></span> <span data-ttu-id="deaed-109">Birden çok okuyucular kullanırsa olaylarından Merhaba aynı tüketici grubu, tüm okuyucular büyük olasılıkla toosee hatalarıdır.</span><span class="sxs-lookup"><span data-stu-id="deaed-109">If multiple readers consume events from hello same consumer group, all readers are likely toosee failures.</span></span> <span data-ttu-id="deaed-110">Merhaba Ayrıntılar için bkz [IOT Hub Geliştirici Kılavuzu](../iot-hub/iot-hub-devguide.md).</span><span class="sxs-lookup"><span data-stu-id="deaed-110">For details, see hello [IoT Hub developer guide](../iot-hub/iot-hub-devguide.md).</span></span>

## <a name="choose-an-import-option"></a><span data-ttu-id="deaed-111">Bir içe aktarma seçeneği seçin</span><span class="sxs-lookup"><span data-stu-id="deaed-111">Choose an Import option</span></span>

<span data-ttu-id="deaed-112">Merhaba olay kaynağı Hello ayarlarını el ile girilebilir veya IOT hub'ı, kullanılabilir tooyou hello IOT hub'larından seçilebilir.</span><span class="sxs-lookup"><span data-stu-id="deaed-112">hello settings for hello event source can be entered manually or an IoT hub can be selected from hello IoT hubs that are available tooyou.</span></span>
<span data-ttu-id="deaed-113">Merhaba, **alma seçeneği** Seçici, aşağıdaki seçenekleri şu hello birini seçin:</span><span class="sxs-lookup"><span data-stu-id="deaed-113">In hello **Import Option** selector, choose one of hello following options:</span></span>

* <span data-ttu-id="deaed-114">IOT hub'ı ayarları sağlayın el ile</span><span class="sxs-lookup"><span data-stu-id="deaed-114">Provide IoT Hub settings manually</span></span>
* <span data-ttu-id="deaed-115">Kullanılabilir aboneliklerden IOT hub'ı kullanın</span><span class="sxs-lookup"><span data-stu-id="deaed-115">Use IoT Hub from available subscriptions</span></span>

### <a name="select-an-available-iot-hub"></a><span data-ttu-id="deaed-116">Kullanılabilir IOT hub'ı seçin</span><span class="sxs-lookup"><span data-stu-id="deaed-116">Select an available IoT Hub</span></span>

<span data-ttu-id="deaed-117">Merhaba aşağıdaki tabloda her seçenekte açıklamasını hello yeni olay kaynağı sekmesi kullanılabilir IOT hub'ı bir olay kaynağı olarak seçerken açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="deaed-117">hello following table explains each option in hello New Event Source tab with its description when selecting an available IoT Hub as an event source:</span></span>

| <span data-ttu-id="deaed-118">ÖZELLİK ADI</span><span class="sxs-lookup"><span data-stu-id="deaed-118">PROPERTY NAME</span></span> | <span data-ttu-id="deaed-119">AÇIKLAMA</span><span class="sxs-lookup"><span data-stu-id="deaed-119">DESCRIPTION</span></span> |
| --- | --- |
| <span data-ttu-id="deaed-120">Olay kaynağı adı</span><span class="sxs-lookup"><span data-stu-id="deaed-120">Event source name</span></span> | <span data-ttu-id="deaed-121">Olay kaynağı Hello adı.</span><span class="sxs-lookup"><span data-stu-id="deaed-121">hello name of your event source.</span></span> <span data-ttu-id="deaed-122">Bu ad zaman serisi Öngörüler ortamınızda benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="deaed-122">This name must be unique within your Time Series Insights environment.</span></span>
| <span data-ttu-id="deaed-123">Kaynak</span><span class="sxs-lookup"><span data-stu-id="deaed-123">Source</span></span> | <span data-ttu-id="deaed-124">Seçin **IOT hub'ı** toocreate bir IOT hub'ı olay kaynağı.</span><span class="sxs-lookup"><span data-stu-id="deaed-124">Choose **IoT Hub** toocreate an IoT Hub event source.</span></span>
| <span data-ttu-id="deaed-125">Abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="deaed-125">Subscription Id</span></span> | <span data-ttu-id="deaed-126">Bu IOT hub'ının oluşturulduğu hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="deaed-126">Select hello subscription in which this IoT hub was created.</span></span>
| <span data-ttu-id="deaed-127">IOT hub'ı adı</span><span class="sxs-lookup"><span data-stu-id="deaed-127">IoT hub name</span></span> | <span data-ttu-id="deaed-128">Merhaba IOT hub'ı Hello adını seçin.</span><span class="sxs-lookup"><span data-stu-id="deaed-128">Select hello name of hello IoT Hub.</span></span>
| <span data-ttu-id="deaed-129">IOT hub ilke adı</span><span class="sxs-lookup"><span data-stu-id="deaed-129">IoT hub policy name</span></span> | <span data-ttu-id="deaed-130">IOT hub'ı Ayarlar sekmesinde hello üzerinde bulunabilir hello paylaşılan erişim ilkesi seçin. Her paylaşılan erişim ilkesinin bir adı, ayarlayın ve erişim anahtarları izinleri vardır.</span><span class="sxs-lookup"><span data-stu-id="deaed-130">Select hello shared access policy, which can be found on hello IoT Hub settings tab. Each shared access policy has a name, permissions that you set, and access keys.</span></span> <span data-ttu-id="deaed-131">Merhaba paylaşılan erişim ilkesi için olay kaynağı *gerekir* sahip **service bağlanma** izinleri.</span><span class="sxs-lookup"><span data-stu-id="deaed-131">hello shared access policy for your event source *must* have **service connect** permissions.</span></span>
| <span data-ttu-id="deaed-132">IOT hub tüketici grubu</span><span class="sxs-lookup"><span data-stu-id="deaed-132">IoT hub consumer group</span></span> | <span data-ttu-id="deaed-133">Merhaba IOT Hub tüketici grubu tooread olaylarından hello.</span><span class="sxs-lookup"><span data-stu-id="deaed-133">hello Consumer Group tooread events from hello IoT Hub.</span></span> <span data-ttu-id="deaed-134">Yüksek oranda olduğu toouse ayrılmış bir tüketici grubu olay kaynağınız için önerilir.</span><span class="sxs-lookup"><span data-stu-id="deaed-134">It is highly recommended toouse a dedicated consumer group for your event source.</span></span>

### <a name="provide-iot-hub-settings-manually"></a><span data-ttu-id="deaed-135">IOT hub'ı ayarları sağlayın el ile</span><span class="sxs-lookup"><span data-stu-id="deaed-135">Provide IoT Hub settings manually</span></span>

<span data-ttu-id="deaed-136">Merhaba aşağıdaki tabloda her bir özellik açıklamasını ile Merhaba yeni olay kaynağı sekmesinde ayarları girerken açıklanmaktadır el ile:</span><span class="sxs-lookup"><span data-stu-id="deaed-136">hello following table explains each property in hello New Event Source tab with its description when entering settings manually:</span></span>

| <span data-ttu-id="deaed-137">ÖZELLİK ADI</span><span class="sxs-lookup"><span data-stu-id="deaed-137">PROPERTY NAME</span></span> | <span data-ttu-id="deaed-138">AÇIKLAMA</span><span class="sxs-lookup"><span data-stu-id="deaed-138">DESCRIPTION</span></span> |
| --- | --- |
| <span data-ttu-id="deaed-139">Olay kaynağı adı</span><span class="sxs-lookup"><span data-stu-id="deaed-139">Event source name</span></span> | <span data-ttu-id="deaed-140">Olay kaynağı Hello adı.</span><span class="sxs-lookup"><span data-stu-id="deaed-140">hello name of your event source.</span></span> <span data-ttu-id="deaed-141">Bu ad zaman serisi Öngörüler ortamınızda benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="deaed-141">This name must be unique within your Time Series Insights environment.</span></span>
| <span data-ttu-id="deaed-142">Kaynak</span><span class="sxs-lookup"><span data-stu-id="deaed-142">Source</span></span> | <span data-ttu-id="deaed-143">Seçin **IOT hub'ı** toocreate bir IOT hub'ı olay kaynağı.</span><span class="sxs-lookup"><span data-stu-id="deaed-143">Choose **IoT Hub** toocreate an IoT Hub event source.</span></span>
| <span data-ttu-id="deaed-144">Abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="deaed-144">Subscription Id</span></span> | <span data-ttu-id="deaed-145">Bu IOT hub'ının oluşturulduğu hello abonelik.</span><span class="sxs-lookup"><span data-stu-id="deaed-145">hello subscription in which this IoT hub was created.</span></span>
| <span data-ttu-id="deaed-146">Kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="deaed-146">Resource group</span></span> | <span data-ttu-id="deaed-147">Bu IOT hub'ının oluşturulduğu hello abonelik.</span><span class="sxs-lookup"><span data-stu-id="deaed-147">hello subscription in which this IoT hub was created.</span></span>
| <span data-ttu-id="deaed-148">IOT hub'ı adı</span><span class="sxs-lookup"><span data-stu-id="deaed-148">IoT hub name</span></span> | <span data-ttu-id="deaed-149">IOT Hub'ınızı Hello adı.</span><span class="sxs-lookup"><span data-stu-id="deaed-149">hello name of your IoT Hub.</span></span> <span data-ttu-id="deaed-150">IOT hub'ınızı oluşturduğunuzda, ona bir özel ad da vermiş</span><span class="sxs-lookup"><span data-stu-id="deaed-150">When you created your IoT hub, you also gave it a specific name</span></span>
| <span data-ttu-id="deaed-151">IOT hub ilke adı</span><span class="sxs-lookup"><span data-stu-id="deaed-151">IoT hub policy name</span></span> | <span data-ttu-id="deaed-152">IOT hub'ı Ayarlar sekmesinde hello üzerinde oluşturulabilir hello paylaşılan erişim ilkesi. Her paylaşılan erişim ilkesinin bir adı, ayarlayın ve erişim anahtarları izinleri vardır.</span><span class="sxs-lookup"><span data-stu-id="deaed-152">hello shared access policy, which can be created on hello IoT Hub settings tab. Each shared access policy has a name, permissions that you set, and access keys.</span></span> <span data-ttu-id="deaed-153">Merhaba paylaşılan erişim ilkesi için olay kaynağı *gerekir* sahip **service bağlanma** izinleri.</span><span class="sxs-lookup"><span data-stu-id="deaed-153">hello shared access policy for your event source *must* have **service connect** permissions.</span></span>
| <span data-ttu-id="deaed-154">IOT hub ilke anahtarı</span><span class="sxs-lookup"><span data-stu-id="deaed-154">IoT hub policy key</span></span> | <span data-ttu-id="deaed-155">Merhaba paylaşılan erişim anahtarı tooauthenticate erişim toohello Service Bus ad alanı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="deaed-155">hello Shared Access key used tooauthenticate access toohello Service Bus namespace.</span></span> <span data-ttu-id="deaed-156">Merhaba birincil veya ikincil anahtarı buraya girin.</span><span class="sxs-lookup"><span data-stu-id="deaed-156">Type hello primary or secondary key here.</span></span>
| <span data-ttu-id="deaed-157">IOT hub tüketici grubu</span><span class="sxs-lookup"><span data-stu-id="deaed-157">IoT hub consumer group</span></span> | <span data-ttu-id="deaed-158">Merhaba IOT Hub tüketici grubu tooread olaylarından hello.</span><span class="sxs-lookup"><span data-stu-id="deaed-158">hello Consumer Group tooread events from hello IoT Hub.</span></span> <span data-ttu-id="deaed-159">Yüksek oranda olduğu toouse ayrılmış bir tüketici grubu olay kaynağınız için önerilir.</span><span class="sxs-lookup"><span data-stu-id="deaed-159">It is highly recommended toouse a dedicated consumer group for your event source.</span></span>

## <a name="next-steps"></a><span data-ttu-id="deaed-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="deaed-160">Next steps</span></span>

1. <span data-ttu-id="deaed-161">Bir veri erişim ilkesi tooyour ortama eklemek [tanımla veri erişim ilkeleri](time-series-insights-data-access.md)</span><span class="sxs-lookup"><span data-stu-id="deaed-161">Add a data access policy tooyour environment [Define data access policies](time-series-insights-data-access.md)</span></span>
1. <span data-ttu-id="deaed-162">Merhaba, ortamınızda erişim [zaman serisi Insights portalı](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="deaed-162">Access your environment in hello [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
