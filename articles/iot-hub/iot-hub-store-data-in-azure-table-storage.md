---
title: "aaaSave IOT hub'ınızı tooAzure veri depolama iletileri | Microsoft Docs"
description: "Bir Azure işlevi uygulama toosave, IOT hub iletileri tooyour Azure tablo depolaması kullanın. Merhaba IOT hub iletileri IOT aygıtınızdan gönderilen algılayıcı verileri gibi bilgileri içerir."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT veri depolama, IOT algılayıcı veri depolama"
ms.assetid: 62fd14fd-aaaa-4b3d-8367-75c1111b6269
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: be72d9ba9a781822926364351b50f58f5d96e94a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a><span data-ttu-id="bf414-105">Algılayıcı verileri tooyour Azure tablo depolaması içeren IOT hub iletileri kaydetme</span><span class="sxs-lookup"><span data-stu-id="bf414-105">Save IoT hub messages that contain sensor data tooyour Azure table storage</span></span>

![Uçtan uca diyagramı](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="bf414-107">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="bf414-107">What you learn</span></span>

<span data-ttu-id="bf414-108">Toocreate bir Azure storage hesabını ve Azure app toostore IOT hub iletileri tablo depolama alanınızın nasıl işlev öğrenin.</span><span class="sxs-lookup"><span data-stu-id="bf414-108">You learn how toocreate an Azure storage account and an Azure function app toostore IoT hub messages in your table storage.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="bf414-109">Neler</span><span class="sxs-lookup"><span data-stu-id="bf414-109">What you do</span></span>

- <span data-ttu-id="bf414-110">Bir Azure Storage hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bf414-110">Create an Azure storage account.</span></span>
- <span data-ttu-id="bf414-111">IOT hub'ınızı bağlantısı tooread iletileri hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="bf414-111">Prepare your IoT hub connection tooread messages.</span></span>
- <span data-ttu-id="bf414-112">Oluşturun ve bir Azure işlevi uygulamayı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="bf414-112">Create and deploy an Azure function app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bf414-113">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="bf414-113">What you need</span></span>

- <span data-ttu-id="bf414-114">[Cihazınızı ayarlamak](iot-hub-raspberry-pi-kit-node-get-started.md) gereksinimlerine toocover hello:</span><span class="sxs-lookup"><span data-stu-id="bf414-114">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md) toocover hello following requirements:</span></span>
  - <span data-ttu-id="bf414-115">Etkin bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="bf414-115">An active Azure subscription</span></span>
  - <span data-ttu-id="bf414-116">Aboneliğinizdeki IOT hub'ı</span><span class="sxs-lookup"><span data-stu-id="bf414-116">An IoT hub under your subscription</span></span> 
  - <span data-ttu-id="bf414-117">Tooyour IOT hub'ı iletileri gönderir çalışan bir uygulama</span><span class="sxs-lookup"><span data-stu-id="bf414-117">A running application that sends messages tooyour IoT hub</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="bf414-118">Azure Storage hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bf414-118">Create an Azure storage account</span></span>

1. <span data-ttu-id="bf414-119">Merhaba, [Azure portal](https://portal.azure.com/), tıklatın **yeni** > **depolama** > **depolama hesabı**  >   **Oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="bf414-119">In hello [Azure portal](https://portal.azure.com/), click **New** > **Storage** > **Storage account** > **Create**.</span></span>

2. <span data-ttu-id="bf414-120">Merhaba hello depolama hesabı için gerekli bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="bf414-120">Enter hello necessary information for hello storage account:</span></span>

   ![Hello Azure portal depolama hesabı oluşturma](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * <span data-ttu-id="bf414-122">**Ad**: hello depolama hesabının hello adı.</span><span class="sxs-lookup"><span data-stu-id="bf414-122">**Name**: hello name of hello storage account.</span></span> <span data-ttu-id="bf414-123">Merhaba adı genel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bf414-123">hello name must be globally unique.</span></span>

   * <span data-ttu-id="bf414-124">**Kaynak grubu**: kullanım hello aynı IOT hub'ınızı kullanan kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="bf414-124">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="bf414-125">**PIN toodashboard**: hello panodan tooyour IOT hub'ı kolay erişim için bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="bf414-125">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

3. <span data-ttu-id="bf414-126">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bf414-126">Click **Create**.</span></span>

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a><span data-ttu-id="bf414-127">IOT hub'ınızı bağlantısı tooread iletileri hazırlama</span><span class="sxs-lookup"><span data-stu-id="bf414-127">Prepare your IoT hub connection tooread messages</span></span>

<span data-ttu-id="bf414-128">IOT hub'ı bir yerleşik olay hub ile uyumlu uç tooenable uygulamaları tooread IOT hub iletileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="bf414-128">IoT hub exposes a built-in event hub-compatible endpoint tooenable applications tooread IoT hub messages.</span></span> <span data-ttu-id="bf414-129">Bu sırada, uygulamaları tüketici grupları tooread verileri IOT hub'ınızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="bf414-129">Meanwhile, applications use consumer groups tooread data from your IoT hub.</span></span> <span data-ttu-id="bf414-130">Bir Azure işlevi uygulama tooread verileri IOT hub'ından oluşturmadan önce aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="bf414-130">Before you create an Azure function app tooread data from your IoT hub, do hello following:</span></span>

- <span data-ttu-id="bf414-131">IOT hub uç noktanızı Hello bağlantı dizesini edinin.</span><span class="sxs-lookup"><span data-stu-id="bf414-131">Get hello connection string of your IoT hub endpoint.</span></span>
- <span data-ttu-id="bf414-132">IOT hub'ınız için bir tüketici grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bf414-132">Create a consumer group for your IoT hub.</span></span>

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a><span data-ttu-id="bf414-133">IOT hub uç noktanızı Hello bağlantı dizesi alma</span><span class="sxs-lookup"><span data-stu-id="bf414-133">Get hello connection string of your IoT hub endpoint</span></span>

1. <span data-ttu-id="bf414-134">IOT hub'ınızı açın.</span><span class="sxs-lookup"><span data-stu-id="bf414-134">Open your IoT hub.</span></span>

2. <span data-ttu-id="bf414-135">Merhaba üzerinde **IOT hub'ı** bölmesi altında **ileti**, tıklatın **uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="bf414-135">On hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="bf414-136">Hello bölmesini altında sağ **yerleşik uç noktaları**, tıklatın **olayları**.</span><span class="sxs-lookup"><span data-stu-id="bf414-136">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="bf414-137">Merhaba, **özellikleri** bölmesinde, aşağıdaki değerleri Not hello:</span><span class="sxs-lookup"><span data-stu-id="bf414-137">In hello **Properties** pane, note hello following values:</span></span>
   - <span data-ttu-id="bf414-138">Olay hub ile uyumlu uç noktası</span><span class="sxs-lookup"><span data-stu-id="bf414-138">Event hub-compatible endpoint</span></span>
   - <span data-ttu-id="bf414-139">Olay hub ile uyumlu adı</span><span class="sxs-lookup"><span data-stu-id="bf414-139">Event hub-compatible name</span></span>

   ![IOT hub uç noktanızı Hello bağlantı dizesi hello Azure portal Al](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. <span data-ttu-id="bf414-141">Merhaba, **IOT hub'ı** bölmesi altında **ayarları**, tıklatın **paylaşılan erişim ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="bf414-141">In hello **IoT Hub** pane, under **Settings**, click **Shared access policies**.</span></span>

6. <span data-ttu-id="bf414-142">Tıklatın **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="bf414-142">Click **iothubowner**.</span></span>

7. <span data-ttu-id="bf414-143">Not hello **birincil anahtar** değeri.</span><span class="sxs-lookup"><span data-stu-id="bf414-143">Note hello **Primary key** value.</span></span>

8. <span data-ttu-id="bf414-144">IOT hub uç noktanızı Hello bağlantı dizesi gibi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="bf414-144">Create hello connection string of your IoT hub endpoint as follows:</span></span>

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > <span data-ttu-id="bf414-145">Değiştir `<Event Hub-compatible endpoint>` ve `<Primary key>` daha önce not ettiğiniz hello değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="bf414-145">Replace `<Event Hub-compatible endpoint>` and `<Primary key>` with hello values that you noted earlier.</span></span>

### <a name="create-a-consumer-group-for-your-iot-hub"></a><span data-ttu-id="bf414-146">IOT hub'ınız için bir tüketici grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="bf414-146">Create a consumer group for your IoT hub</span></span>

1. <span data-ttu-id="bf414-147">IOT hub'ınızı açın.</span><span class="sxs-lookup"><span data-stu-id="bf414-147">Open your IoT hub.</span></span>

2. <span data-ttu-id="bf414-148">Merhaba, **IOT hub'ı** bölmesi altında **ileti**, tıklatın **uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="bf414-148">In hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="bf414-149">Hello bölmesini altında sağ **yerleşik uç noktaları**, tıklatın **olayları**.</span><span class="sxs-lookup"><span data-stu-id="bf414-149">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="bf414-150">Merhaba, **özellikleri** bölmesi altında **tüketici grupları**, bir ad girin ve ardından bir not edin.</span><span class="sxs-lookup"><span data-stu-id="bf414-150">In hello **Properties** pane, under **Consumer groups**, enter a name, and then make a note of it.</span></span>

5. <span data-ttu-id="bf414-151">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bf414-151">Click **Save**.</span></span>

## <a name="create-and-deploy-an-azure-function-app"></a><span data-ttu-id="bf414-152">Oluşturma ve bir Azure işlevi uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="bf414-152">Create and deploy an Azure function app</span></span>

1. <span data-ttu-id="bf414-153">Merhaba, [Azure portal](https://portal.azure.com/), tıklatın **yeni** > **işlem** > **işlev uygulaması**  >   **Oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="bf414-153">In hello [Azure portal](https://portal.azure.com/), click **New** > **Compute** > **Function App** > **Create**.</span></span>

2. <span data-ttu-id="bf414-154">Merhaba hello işlev uygulaması için gerekli bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="bf414-154">Enter hello necessary information for hello function app.</span></span>

   ![Hello Azure portal işlev uygulaması oluşturma](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * <span data-ttu-id="bf414-156">**Uygulama adı**: hello işlevi uygulamasının hello adı.</span><span class="sxs-lookup"><span data-stu-id="bf414-156">**App name**: hello name of hello function app.</span></span> <span data-ttu-id="bf414-157">Merhaba adı genel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bf414-157">hello name must be globally unique.</span></span>

   * <span data-ttu-id="bf414-158">**Kaynak grubu**: kullanım hello aynı IOT hub'ınızı kullanan kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="bf414-158">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="bf414-159">**Depolama hesabı**: Merhaba oluşturduğunuz depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="bf414-159">**Storage Account**: hello storage account that you created.</span></span>

   * <span data-ttu-id="bf414-160">**PIN toodashboard**: hello panosundan kolay erişim toohello işlev uygulaması için bu seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="bf414-160">**Pin toodashboard**: Check this option for easy access toohello function app from hello dashboard.</span></span>

3. <span data-ttu-id="bf414-161">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bf414-161">Click **Create**.</span></span>

4. <span data-ttu-id="bf414-162">Merhaba işlev uygulaması oluşturulduktan sonra açın.</span><span class="sxs-lookup"><span data-stu-id="bf414-162">After hello function app has been created, open it.</span></span>

5. <span data-ttu-id="bf414-163">Merhaba işlevi uygulamada hello aşağıdakileri yaparak yeni bir işlev oluşturun:</span><span class="sxs-lookup"><span data-stu-id="bf414-163">In hello function app, create a new function by doing hello following:</span></span>

   <span data-ttu-id="bf414-164">a.</span><span class="sxs-lookup"><span data-stu-id="bf414-164">a.</span></span> <span data-ttu-id="bf414-165">Tıklatın **yeni işlev**.</span><span class="sxs-lookup"><span data-stu-id="bf414-165">Click **New Function**.</span></span>

   <span data-ttu-id="bf414-166">b.</span><span class="sxs-lookup"><span data-stu-id="bf414-166">b.</span></span> <span data-ttu-id="bf414-167">Seçin **JavaScript** için **dil**, ve **veri işleme** için **senaryo**.</span><span class="sxs-lookup"><span data-stu-id="bf414-167">Select **JavaScript** for **Language**, and **Data Processing** for **Scenario**.</span></span>

   <span data-ttu-id="bf414-168">c.</span><span class="sxs-lookup"><span data-stu-id="bf414-168">c.</span></span> <span data-ttu-id="bf414-169">Tıklatın **bu işlev oluşturma**ve ardından **yeni işlev**.</span><span class="sxs-lookup"><span data-stu-id="bf414-169">Click **Create this function**, and then click **New Function**.</span></span>

   <span data-ttu-id="bf414-170">d.</span><span class="sxs-lookup"><span data-stu-id="bf414-170">d.</span></span> <span data-ttu-id="bf414-171">Seçin **JavaScript** hello dilin ve **veri işleme** hello senaryosu için.</span><span class="sxs-lookup"><span data-stu-id="bf414-171">Select **JavaScript** for hello language, and **Data Processing** for hello scenario.</span></span>

   <span data-ttu-id="bf414-172">e.</span><span class="sxs-lookup"><span data-stu-id="bf414-172">e.</span></span> <span data-ttu-id="bf414-173">Merhaba tıklatın **EventHubTrigger JavaScript** şablonu.</span><span class="sxs-lookup"><span data-stu-id="bf414-173">Click hello **EventHubTrigger-JavaScript** template.</span></span>

   <span data-ttu-id="bf414-174">f.</span><span class="sxs-lookup"><span data-stu-id="bf414-174">f.</span></span> <span data-ttu-id="bf414-175">Merhaba hello şablonu için gerekli bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="bf414-175">Enter hello necessary information for hello template.</span></span>

      * <span data-ttu-id="bf414-176">**İşlevinizin adı**: hello işlevinin hello adı.</span><span class="sxs-lookup"><span data-stu-id="bf414-176">**Name your function**: hello name of hello function.</span></span>

      * <span data-ttu-id="bf414-177">**Olay hub'ı adı**: daha önce not ettiğiniz hello olay hub ile uyumlu adı.</span><span class="sxs-lookup"><span data-stu-id="bf414-177">**Event Hub name**: hello event hub-compatible name that you noted earlier.</span></span>

      * <span data-ttu-id="bf414-178">**Olay Hub bağlantısı**: tooadd hello bağlantı dizesi, oluşturduğunuz hello IOT hub uç tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="bf414-178">**Event Hub connection**: tooadd hello connection string of hello IoT hub endpoint that you created, click **New**.</span></span>

   <span data-ttu-id="bf414-179">g.</span><span class="sxs-lookup"><span data-stu-id="bf414-179">g.</span></span> <span data-ttu-id="bf414-180">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bf414-180">Click **Create**.</span></span>

6. <span data-ttu-id="bf414-181">Bir çıkış hello işlevinin hello aşağıdakileri yaparak yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="bf414-181">Configure an output of hello function by doing hello following:</span></span>

   <span data-ttu-id="bf414-182">a.</span><span class="sxs-lookup"><span data-stu-id="bf414-182">a.</span></span> <span data-ttu-id="bf414-183">Tıklatın **tümleştirmek** > **yeni çıktı** > **Azure Table Storage** > **seçin**.</span><span class="sxs-lookup"><span data-stu-id="bf414-183">Click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

      ![Tablo depolama tooyour işlev uygulaması hello Azure portal Ekle](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   <span data-ttu-id="bf414-185">b.</span><span class="sxs-lookup"><span data-stu-id="bf414-185">b.</span></span> <span data-ttu-id="bf414-186">Merhaba gerekli bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="bf414-186">Enter hello necessary information.</span></span>

      * <span data-ttu-id="bf414-187">**Tablo parametre adı**: kullanım `outputTable`, hangi kullanılacak hello Azure işlevin kodu.</span><span class="sxs-lookup"><span data-stu-id="bf414-187">**Table parameter name**: Use `outputTable`, which will be used in hello Azure function's code.</span></span>
      
      * <span data-ttu-id="bf414-188">**Tablo adı**: kullanım `deviceData`.</span><span class="sxs-lookup"><span data-stu-id="bf414-188">**Table name**: Use `deviceData`.</span></span>

      * <span data-ttu-id="bf414-189">**Depolama hesabı bağlantısı**: tıklatın **yeni**ve ardından seçin veya depolama hesabınızı girin.</span><span class="sxs-lookup"><span data-stu-id="bf414-189">**Storage account connection**: Click **New**, and then select or enter your storage account.</span></span> <span data-ttu-id="bf414-190">Merhaba depolama hesabı görüntülenmiyorsa bkz [depolama hesabı gereksinimleri](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="bf414-190">If hello storage account is not displayed, see [Storage account requirements](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span></span>
      
   <span data-ttu-id="bf414-191">c.</span><span class="sxs-lookup"><span data-stu-id="bf414-191">c.</span></span> <span data-ttu-id="bf414-192">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bf414-192">Click **Save**.</span></span>

7. <span data-ttu-id="bf414-193">Altında **Tetikleyicileri**, tıklatın **Azure olay hub'ı (eventHubMessages)**.</span><span class="sxs-lookup"><span data-stu-id="bf414-193">Under **Triggers**, click **Azure Event Hub (eventHubMessages)**.</span></span>

8. <span data-ttu-id="bf414-194">Altında **Event Hub tüketici grubu**, oluşturulan ve ardından hello tüketici grubu hello adını **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="bf414-194">Under **Event Hub consumer group**, enter hello name of hello consumer group that you created, and then click **Save**.</span></span>

9. <span data-ttu-id="bf414-195">Sol hello üzerinde oluşturulan hello işlevi tıklayın ve ardından **dosyaları görüntüle** hello sağ üzerinde.</span><span class="sxs-lookup"><span data-stu-id="bf414-195">Click hello function you've created on hello left and then click **View Files** on hello right.</span></span>

10. <span data-ttu-id="bf414-196">Merhaba kodla `index.js` hello aşağıdaki ile:</span><span class="sxs-lookup"><span data-stu-id="bf414-196">Replace hello code in `index.js` with hello following:</span></span>

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in hello IoT hub.
   // hello message payload is persisted in an Azure storage table
 
   module.exports = function (context, iotHubMessage) {
    context.log('Message received: ' + JSON.stringify(iotHubMessage));
    var date = Date.now();
    var partitionKey = Math.floor(date / (24 * 60 * 60 * 1000)) + '';
    var rowKey = date + '';
    context.bindings.outputTable = {
     "partitionKey": partitionKey,
     "rowKey": rowKey,
     "message": JSON.stringify(iotHubMessage)
    };
    context.done();
   };
   ```

11. <span data-ttu-id="bf414-197">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bf414-197">Click **Save**.</span></span>

<span data-ttu-id="bf414-198">Merhaba işlev uygulaması oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="bf414-198">You have now created hello function app.</span></span> <span data-ttu-id="bf414-199">Tablo deponuzda IOT hub'ınızın aldığı iletileri depolar.</span><span class="sxs-lookup"><span data-stu-id="bf414-199">It stores messages that your IoT hub receives in your table storage.</span></span>

> [!NOTE]
> <span data-ttu-id="bf414-200">Merhaba kullanabilirsiniz **çalıştırmak** düğmesini tootest hello işlev uygulaması.</span><span class="sxs-lookup"><span data-stu-id="bf414-200">You can use hello **Run** button tootest hello function app.</span></span> <span data-ttu-id="bf414-201">Tıkladığınızda **çalıştırmak**, hello sınama iletisi tooyour IOT hub'ı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="bf414-201">When you click **Run**, hello test message is sent tooyour IoT hub.</span></span> <span data-ttu-id="bf414-202">Merhaba varış hello iletisinin hello işlevi uygulama toostart tetiklemek ve hello ileti tooyour tablo depolama Kaydet gerekir.</span><span class="sxs-lookup"><span data-stu-id="bf414-202">hello arrival of hello message should trigger hello function app toostart and then save hello message tooyour table storage.</span></span> <span data-ttu-id="bf414-203">Merhaba **günlükleri** bölmesinde hello işleminin hello ayrıntıları kaydeder.</span><span class="sxs-lookup"><span data-stu-id="bf414-203">hello **Logs** pane records hello details of hello process.</span></span>

## <a name="verify-your-message-in-your-table-storage"></a><span data-ttu-id="bf414-204">Tablo depolama alanınızın iletinize doğrulayın</span><span class="sxs-lookup"><span data-stu-id="bf414-204">Verify your message in your table storage</span></span>

1. <span data-ttu-id="bf414-205">Merhaba örnek uygulaması, aygıt toosend iletileri tooyour IOT hub'ına çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bf414-205">Run hello sample application on your device toosend messages tooyour IoT hub.</span></span>

2. <span data-ttu-id="bf414-206">[Azure Storage Gezgini yükleyip](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="bf414-206">[Download and install Azure Storage Explorer](http://storageexplorer.com/).</span></span>

3. <span data-ttu-id="bf414-207">Depolama Gezgini'ni açın, **Azure Hesap Ekle** > **oturum**ve ardından tooyour Azure hesabı açın.</span><span class="sxs-lookup"><span data-stu-id="bf414-207">Open Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in tooyour Azure account.</span></span>

4. <span data-ttu-id="bf414-208">Azure aboneliğiniz tıklayın > **depolama hesapları** > depolama hesabınız > **tabloları** > **deviceData**.</span><span class="sxs-lookup"><span data-stu-id="bf414-208">Click your Azure subscription > **Storage Accounts** > your storage account > **Tables** > **deviceData**.</span></span>

   <span data-ttu-id="bf414-209">Hello oturum, aygıt tooyour IOT hub'dan gönderilen iletileri görmelisiniz `deviceData` tablo.</span><span class="sxs-lookup"><span data-stu-id="bf414-209">You should see messages sent from your device tooyour IoT hub logged in hello `deviceData` table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf414-210">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bf414-210">Next steps</span></span>

<span data-ttu-id="bf414-211">Azure depolama hesabı ve tablo deponuzda IOT hub'ınızın aldığı iletileri depolayan Azure işlev uygulaması başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="bf414-211">You’ve successfully created your Azure storage account and Azure function app, which stores messages that your IoT hub receives in your table storage.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
