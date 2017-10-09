---
title: aaaIoT Uzaktan izleme ve Azure Logic Apps ile bildirimleri | Microsoft Docs
description: "IOT sıcaklık IOT hub'ınızı ve otomatik olarak izleme algılanan anormallikleri için e-posta bildirimleri tooyour posta göndermek için Azure mantıksal uygulamaları kullanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT, IOT bildirimleri izleme IOT Sıcaklık İzleme"
ms.assetid: 43043067-2e1f-42c9-953d-e2dce8fd86df
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 89396528ed63c37258e1b49f342f0723e686ecb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a><span data-ttu-id="4e026-104">IOT Uzaktan izleme ve IOT hub ve posta kutusu bağlanma Azure Logic Apps ile bildirimleri</span><span class="sxs-lookup"><span data-stu-id="4e026-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span></span>

![Uçtan uca diyagramı](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="4e026-106">Azure mantıksal uygulamaları bir yöntem sunar tooautomate işlemleri bir dizi adımı olarak.</span><span class="sxs-lookup"><span data-stu-id="4e026-106">Azure Logic Apps provides a way tooautomate processes as a series of steps.</span></span> <span data-ttu-id="4e026-107">Bir mantıksal uygulama çeşitli hizmetler ve protokoller bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e026-107">A logic app can connect across various services and protocols.</span></span> <span data-ttu-id="4e026-108">Bir tetikleyici ile gibi 'Bir hesap eklendiğinde', başladıktan ve 'bir anında iletme bildirimi gönderme' gibi işlemleri birleştirilmesiyle gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="4e026-108">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span></span> <span data-ttu-id="4e026-109">Bu özellik Logic Apps mükemmel bir IOT çözüm IOT için izleme, diğer kullanım senaryoları arasında anormallikleri için uyarı kaldığını gibi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="4e026-109">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="4e026-110">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="4e026-110">What you learn</span></span>

<span data-ttu-id="4e026-111">Hakkında bilgi edineceksiniz nasıl toocreate IOT hub'ınızı ve Sıcaklık İzleme ve bildirimler için posta bağlayan bir mantıksal uygulama.</span><span class="sxs-lookup"><span data-stu-id="4e026-111">You learn how toocreate a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span> <span data-ttu-id="4e026-112">Merhaba sıcaklığı 30 C olduğunda, istemci uygulaması işaretleri hello `temperatureAlert = "true"` hello iletisinde tooyour IOT hub'ı gönderir.</span><span class="sxs-lookup"><span data-stu-id="4e026-112">When hello temperature is above 30 C, hello client application marks `temperatureAlert = "true"` in hello message it sends tooyour IoT hub.</span></span> <span data-ttu-id="4e026-113">Tetikleyiciler hello mantığı uygulama toosend selamlama iletisine, bir e-posta bildirimi.</span><span class="sxs-lookup"><span data-stu-id="4e026-113">hello message triggers hello logic app toosend you an email notification.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="4e026-114">Neler</span><span class="sxs-lookup"><span data-stu-id="4e026-114">What you do</span></span>

* <span data-ttu-id="4e026-115">Hizmet veri yolu ad alanı oluşturun ve bir sıraya tooit ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4e026-115">Create a service bus namespace and add a queue tooit.</span></span>
* <span data-ttu-id="4e026-116">Bir uç nokta ve bir yönlendirme kuralı tooyour IOT hub'ı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4e026-116">Add an endpoint and a routing rule tooyour IoT hub.</span></span>
* <span data-ttu-id="4e026-117">Oluşturma, yapılandırma ve bir mantıksal uygulama test.</span><span class="sxs-lookup"><span data-stu-id="4e026-117">Create, configure, and test a logic app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4e026-118">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="4e026-118">What you need</span></span>

* <span data-ttu-id="4e026-119">Öğretici [Cihazınızı](iot-hub-raspberry-pi-kit-node-get-started.md) hangi hello gereksinimleri aşağıdaki kapsayan tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="4e026-119">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  * <span data-ttu-id="4e026-120">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="4e026-120">An active Azure subscription.</span></span>
  * <span data-ttu-id="4e026-121">Azure IOT hub'ı aboneliğinizdeki.</span><span class="sxs-lookup"><span data-stu-id="4e026-121">An Azure IoT hub under your subscription.</span></span>
  * <span data-ttu-id="4e026-122">Tooyour Azure IOT hub'ı iletileri gönderir bir istemci uygulaması.</span><span class="sxs-lookup"><span data-stu-id="4e026-122">A client application that sends messages tooyour Azure IoT hub.</span></span>

## <a name="create-service-bus-namespace-and-add-a-queue-tooit"></a><span data-ttu-id="4e026-123">Hizmet veri yolu ad alanı oluşturun ve bir sıraya tooit ekleyin</span><span class="sxs-lookup"><span data-stu-id="4e026-123">Create service bus namespace and add a queue tooit</span></span>

### <a name="create-a-service-bus-namespace"></a><span data-ttu-id="4e026-124">Hizmet veri yolu ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e026-124">Create a service bus namespace</span></span>

1. <span data-ttu-id="4e026-125">Merhaba üzerinde [Azure portal](https://portal.azure.com/), tıklatın **yeni** > **Kurumsal tümleştirme** > **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="4e026-125">On hello [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Service Bus**.</span></span>
1. <span data-ttu-id="4e026-126">Aşağıdaki bilgilerle hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="4e026-126">Provide hello following information:</span></span>

   <span data-ttu-id="4e026-127">**Ad**: hello hizmet veri yolu hello adı.</span><span class="sxs-lookup"><span data-stu-id="4e026-127">**Name**: hello name of hello service bus.</span></span>

   <span data-ttu-id="4e026-128">**Fiyatlandırma katmanı**: tıklatın **temel** > **seçin**.</span><span class="sxs-lookup"><span data-stu-id="4e026-128">**Pricing tier**: Click **Basic** > **Select**.</span></span> <span data-ttu-id="4e026-129">Merhaba temel katmanı, Bu öğretici için yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="4e026-129">hello Basic tier is sufficient for this tutorial.</span></span>

   <span data-ttu-id="4e026-130">**Kaynak grubu**: kullanım hello aynı IOT hub'ınızı kullanan kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="4e026-130">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="4e026-131">**Konum**: kullanım hello aynı IOT hub'ınızı kullandığı konum.</span><span class="sxs-lookup"><span data-stu-id="4e026-131">**Location**: Use hello same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="4e026-132">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4e026-132">Click **Create**.</span></span>

   ![Hello Azure portalına hizmet veri yolu ad alanı oluşturma](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a><span data-ttu-id="4e026-134">Hizmet veri yolu kuyruğu ekleme</span><span class="sxs-lookup"><span data-stu-id="4e026-134">Add a service bus queue</span></span>

1. <span data-ttu-id="4e026-135">Merhaba hizmet veri yolu ad alanı açın ve ardından **+ sıraya**.</span><span class="sxs-lookup"><span data-stu-id="4e026-135">Open hello service bus namespace, and then click **+ Queue**.</span></span>
1. <span data-ttu-id="4e026-136">Merhaba sıra için bir ad girin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="4e026-136">Enter a name for hello queue and then click **Create**.</span></span>
1. <span data-ttu-id="4e026-137">Merhaba hizmet veri yolu kuyruğu açın ve ardından **paylaşılan erişim ilkeleri** > **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4e026-137">Open hello service bus queue, and then click **Shared access policies** > **+ Add**.</span></span>
1. <span data-ttu-id="4e026-138">Hello İlkesi denetimi için bir ad girin **Yönet**ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="4e026-138">Enter a name for hello policy, check **Manage**, and then click **Create**.</span></span>

   ![Hizmet veri yolu kuyruğu hello Azure portal Ekle](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-tooyour-iot-hub"></a><span data-ttu-id="4e026-140">Bir uç nokta ve bir yönlendirme kuralı tooyour IOT hub'ı ekleme</span><span class="sxs-lookup"><span data-stu-id="4e026-140">Add an endpoint and a routing rule tooyour IoT hub</span></span>

### <a name="add-an-endpoint"></a><span data-ttu-id="4e026-141">Bir uç nokta ekleme</span><span class="sxs-lookup"><span data-stu-id="4e026-141">Add an endpoint</span></span>

1. <span data-ttu-id="4e026-142">IOT hub'ınızı açın, uç noktaları > + Ekle.</span><span class="sxs-lookup"><span data-stu-id="4e026-142">Open your IoT hub, click Endpoints > + Add.</span></span>
1. <span data-ttu-id="4e026-143">Aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="4e026-143">Enter hello following information:</span></span>

   <span data-ttu-id="4e026-144">**Ad**: hello uç noktanın hello adı.</span><span class="sxs-lookup"><span data-stu-id="4e026-144">**Name**: hello name of hello endpoint.</span></span>

   <span data-ttu-id="4e026-145">**Uç nokta türü**: seçin **hizmet veri yolu kuyruğu**.</span><span class="sxs-lookup"><span data-stu-id="4e026-145">**Endpoint type**: Select **Service Bus Queue**.</span></span>

   <span data-ttu-id="4e026-146">**Hizmet veri yolu ad alanı**: oluşturduğunuz hello ad alanı seçin.</span><span class="sxs-lookup"><span data-stu-id="4e026-146">**Service Bus namespace**: Select hello namespace you created.</span></span>

   <span data-ttu-id="4e026-147">**Service Bus kuyruğuna**: oluşturduğunuz Select hello sırası.</span><span class="sxs-lookup"><span data-stu-id="4e026-147">**Service Bus queue**: Select hello queue you created.</span></span>
1. <span data-ttu-id="4e026-148">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4e026-148">Click **OK**.</span></span>

   ![Bir uç nokta tooyour IOT hub'hello Azure portal Ekle](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a><span data-ttu-id="4e026-150">Yönlendirme kuralı Ekle</span><span class="sxs-lookup"><span data-stu-id="4e026-150">Add a routing rule</span></span>

1. <span data-ttu-id="4e026-151">IOT hub'ı tıklatın **yollar** > **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4e026-151">In your IoT hub, click **Routes** > **+ Add**.</span></span>
1. <span data-ttu-id="4e026-152">Aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="4e026-152">Enter hello following information:</span></span>

   <span data-ttu-id="4e026-153">**Ad**: hello yönlendirme kuralı hello adı.</span><span class="sxs-lookup"><span data-stu-id="4e026-153">**Name**: hello name of hello routing rule.</span></span>

   <span data-ttu-id="4e026-154">**Veri kaynağı**: seçin **DeviceMessages**.</span><span class="sxs-lookup"><span data-stu-id="4e026-154">**Data source**: Select **DeviceMessages**.</span></span>

   <span data-ttu-id="4e026-155">**Uç nokta**: oluşturduğunuz hello uç nokta seçin.</span><span class="sxs-lookup"><span data-stu-id="4e026-155">**Endpoint**: Select hello endpoint you created.</span></span>

   <span data-ttu-id="4e026-156">**Sorgu dizesi**: girin `temperatureAlert = "true"`.</span><span class="sxs-lookup"><span data-stu-id="4e026-156">**Query string**: Enter `temperatureAlert = "true"`.</span></span>
1. <span data-ttu-id="4e026-157">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4e026-157">Click **Save**.</span></span>

   ![Hello Azure portalında bir yönlendirme kuralı Ekle](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a><span data-ttu-id="4e026-159">Oluşturma ve bir mantıksal uygulama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4e026-159">Create and configure a logic app</span></span>

### <a name="create-a-logic-app"></a><span data-ttu-id="4e026-160">Mantıksal uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e026-160">Create a logic app</span></span>

1. <span data-ttu-id="4e026-161">Merhaba, [Azure portal](https://portal.azure.com/), tıklatın **yeni** > **Kurumsal tümleştirme** > **mantıksal uygulama**.</span><span class="sxs-lookup"><span data-stu-id="4e026-161">In hello [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Logic App**.</span></span>
1. <span data-ttu-id="4e026-162">Aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="4e026-162">Enter hello following information:</span></span>

   <span data-ttu-id="4e026-163">**Ad**: hello mantıksal uygulama hello adı.</span><span class="sxs-lookup"><span data-stu-id="4e026-163">**Name**: hello name of hello logic app.</span></span>

   <span data-ttu-id="4e026-164">**Kaynak grubu**: kullanım hello aynı IOT hub'ınızı kullanan kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="4e026-164">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="4e026-165">**Konum**: kullanım hello aynı IOT hub'ınızı kullandığı konum.</span><span class="sxs-lookup"><span data-stu-id="4e026-165">**Location**: Use hello same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="4e026-166">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4e026-166">Click **Create**.</span></span>

### <a name="configure-hello-logic-app"></a><span data-ttu-id="4e026-167">Merhaba mantıksal uygulama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4e026-167">Configure hello logic app</span></span>

1. <span data-ttu-id="4e026-168">Logic Apps Tasarımcısı hello açar hello mantığı uygulamasını açın.</span><span class="sxs-lookup"><span data-stu-id="4e026-168">Open hello logic app that opens into hello Logic Apps Designer.</span></span>
1. <span data-ttu-id="4e026-169">Hello Logic Apps Tasarımcı'da, tıklatın **boş mantıksal uygulama**.</span><span class="sxs-lookup"><span data-stu-id="4e026-169">In hello Logic Apps Designer, click **Blank Logic App**.</span></span>

   ![Hello Azure portal'ın boş mantıksal uygulama ile başlayın](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="4e026-171">Tıklatın **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="4e026-171">Click **Service Bus**.</span></span>

   ![Hizmet veri yolu toostart hello Azure portalda mantıksal uygulamanızı oluşturma seçin](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="4e026-173">Tıklatın **Service Bus – bir veya daha fazla ileti (Otomatik Tamamlama) kuyrukta geldiğinde**.</span><span class="sxs-lookup"><span data-stu-id="4e026-173">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span></span>
1. <span data-ttu-id="4e026-174">Hizmet veri yolu bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4e026-174">Create a service bus connection.</span></span>
   1. <span data-ttu-id="4e026-175">Bir bağlantı adı girin.</span><span class="sxs-lookup"><span data-stu-id="4e026-175">Enter a connection name.</span></span>
   1. <span data-ttu-id="4e026-176">Merhaba hizmet veri yolu ad alanına tıklayın > merhaba hizmet veri yolu İlkesi > **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="4e026-176">Click hello service bus namespace > hello service bus policy > **Create**.</span></span>

      ![Mantıksal uygulamanız için bir hizmet veri yolu bağlantı hello Azure portal oluşturma](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. <span data-ttu-id="4e026-178">Tıklatın **devam** hello hizmet veri yolu bağlantı oluşturulduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="4e026-178">Click **Continue** after hello service bus connection is created.</span></span>
   1. <span data-ttu-id="4e026-179">Oluşturduğunuz hello kuyruk seçip girin `175` için **en fazla ileti sayısı**</span><span class="sxs-lookup"><span data-stu-id="4e026-179">Select hello queue that you created and enter `175` for **Maximum message count**</span></span>

      ![Mantıksal uygulamanızı Hello hello hizmet veri yolu bağlantı için en fazla ileti sayısı belirtin](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. <span data-ttu-id="4e026-181">Düğme toosave hello değişiklikleri "Kaydet" seçeneğini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4e026-181">Click "Save" button toosave hello changes.</span></span>

1. <span data-ttu-id="4e026-182">SMTP hizmeti bağlantısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4e026-182">Create an SMTP service connection.</span></span>
   1. <span data-ttu-id="4e026-183">Tıklatın **yeni adım** > **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4e026-183">Click **New step** > **Add an action**.</span></span>
   1. <span data-ttu-id="4e026-184">Tür `SMTP`, hello tıklatın **SMTP** hizmet hello arama sonucunda ve ardından **SMTP - e-posta Gönder**.</span><span class="sxs-lookup"><span data-stu-id="4e026-184">Type `SMTP`, click hello **SMTP** service in hello search result, and then click **SMTP - Send Email**.</span></span>

      ![Bir SMTP bağlantı hello Azure portalda mantıksal uygulamanızı oluşturun](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. <span data-ttu-id="4e026-186">Posta Hello SMTP bilgilerini girin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="4e026-186">Enter hello SMTP information of your mailbox, and then click **Create**.</span></span>

      ![Mantıksal uygulamanızı hello Azure portal, SMTP bağlantı bilgilerini girin](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      <span data-ttu-id="4e026-188">Merhaba SMTP bilgilerini edinin [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), ve [Yahoo Posta](https://help.yahoo.com/kb/SLN4075.html).</span><span class="sxs-lookup"><span data-stu-id="4e026-188">Get hello SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span></span>
   1. <span data-ttu-id="4e026-189">E-posta adresinizi girin **gelen** ve **için**, ve `High temperature detected` için **konu** ve **gövde**.</span><span class="sxs-lookup"><span data-stu-id="4e026-189">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span></span>
   1. <span data-ttu-id="4e026-190">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4e026-190">Click **Save**.</span></span>

<span data-ttu-id="4e026-191">kaydettiğinizde hello mantıksal uygulama çalışma sıradadır.</span><span class="sxs-lookup"><span data-stu-id="4e026-191">hello logic app is in working order when you save it.</span></span>

## <a name="test-hello-logic-app"></a><span data-ttu-id="4e026-192">Test hello mantıksal uygulama</span><span class="sxs-lookup"><span data-stu-id="4e026-192">Test hello logic app</span></span>

1. <span data-ttu-id="4e026-193">Tooyour cihazı dağıtma Merhaba istemci uygulaması başlangıç [bağlanmak ESP8266 tooAzure IOT hub'ı](iot-hub-arduino-huzzah-esp8266-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4e026-193">Start hello client application that you deploy tooyour device in [Connect ESP8266 tooAzure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span></span>
1. <span data-ttu-id="4e026-194">Hello ortamı sıcaklığı 30 C. yukarıda hello SensorTag toobe geçici artırın Örneğin, Şamdan, SensorTag geçici açık.</span><span class="sxs-lookup"><span data-stu-id="4e026-194">Increase hello environment temperature around hello SensorTag toobe above 30 C. For example, light a candle around your SensorTag.</span></span>
1. <span data-ttu-id="4e026-195">Merhaba mantıksal uygulama tarafından gönderilen bir e-posta bildirim almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e026-195">You should receive an email notification sent by hello logic app.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4e026-196">E-posta hizmet sağlayıcınıza tooverify hello Gönderen Kimliği toomake hello e-posta gönderir, olduğundan emin gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="4e026-196">Your email service provider may need tooverify hello sender identity toomake sure it is you who sends hello email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e026-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4e026-197">Next steps</span></span>

<span data-ttu-id="4e026-198">IOT hub'ınızı ve Sıcaklık İzleme ve bildirimler için posta bağlayan bir mantıksal uygulama başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="4e026-198">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
