---
title: "IOT hub'ı aaaUse hello Azure portal toocreate | Microsoft Docs"
description: "Nasıl toocreate, yönetin ve hello Azure Portalı aracılığıyla Azure IOT hub'ları silin. Fiyatlandırma katmanlarına, ölçeklendirme, güvenlik ve yapılandırma Mesajlaşma hakkında bilgi içerir."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0909cd2b-4c1e-49e0-b68a-75532caf0a6a
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: 383968c90ee7ef3bff85a6c90efbf5f0e8fbb208
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-portal"></a><span data-ttu-id="c89d4-104">Hello Azure portal kullanarak IOT hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="c89d4-104">Create an IoT hub using hello Azure portal</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="c89d4-105">Bu makalede açıklanır:</span><span class="sxs-lookup"><span data-stu-id="c89d4-105">This article describes:</span></span>

* <span data-ttu-id="c89d4-106">Nasıl toofind, IOT Hub'hello Azure portal hizmetinde hello.</span><span class="sxs-lookup"><span data-stu-id="c89d4-106">How toofind hello IoT Hub service in hello Azure portal.</span></span>
* <span data-ttu-id="c89d4-107">Nasıl toocreate ve IOT hub'ları yönetin.</span><span class="sxs-lookup"><span data-stu-id="c89d4-107">How toocreate and manage IoT hubs.</span></span>

## <a name="where-toofind-hello-iot-hub-service"></a><span data-ttu-id="c89d4-108">Burada toofind hello IOT Hub hizmeti</span><span class="sxs-lookup"><span data-stu-id="c89d4-108">Where toofind hello IoT Hub service</span></span>

<span data-ttu-id="c89d4-109">Merhaba IOT Hub hizmeti aşağıdaki konumlardan hello portalında hello bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c89d4-109">You can find hello IoT Hub service in hello following locations in hello portal:</span></span>

* <span data-ttu-id="c89d4-110">Seçin **+ yeni**, ardından **nesnelerin interneti**.</span><span class="sxs-lookup"><span data-stu-id="c89d4-110">Choose **+ New**, then choose **Internet of Things**.</span></span>
* <span data-ttu-id="c89d4-111">Hello Market, seçin **nesnelerin interneti**.</span><span class="sxs-lookup"><span data-stu-id="c89d4-111">In hello Marketplace, choose **Internet of Things**.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="c89d4-112">IoT hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="c89d4-112">Create an IoT hub</span></span>

<span data-ttu-id="c89d4-113">Bir IOT hub'hello aşağıdaki yöntemleri kullanarak oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c89d4-113">You can create an IoT hub using hello following methods:</span></span>

* <span data-ttu-id="c89d4-114">Merhaba **+ yeni** seçeneği ekran görüntüsü aşağıdaki hello gösterilen hello dikey penceresini açar.</span><span class="sxs-lookup"><span data-stu-id="c89d4-114">hello **+ New** option opens hello blade shown in hello following screen shot.</span></span> <span data-ttu-id="c89d4-115">Merhaba marketplace ve bu yöntem aracılığıyla hello IOT hub oluşturma hello adımları aynıdır.</span><span class="sxs-lookup"><span data-stu-id="c89d4-115">hello steps for creating hello IoT hub through this method and through hello marketplace are identical.</span></span>
* <span data-ttu-id="c89d4-116">Hello Market, seçin **oluşturma** tooopen hello dikey ekran görüntüsü aşağıdaki hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c89d4-116">In hello Marketplace, choose **Create** tooopen hello blade shown in hello following screen shot.</span></span>

<span data-ttu-id="c89d4-117">Merhaba aşağıdaki bölümlerde açıklanmaktadır hello çeşitli adımları toocreate bir IOT hub:</span><span class="sxs-lookup"><span data-stu-id="c89d4-117">hello following sections describe hello several steps toocreate an IoT hub:</span></span>

### <a name="choose-hello-name-of-hello-iot-hub"></a><span data-ttu-id="c89d4-118">Merhaba IOT hub'ı Hello adını seçin</span><span class="sxs-lookup"><span data-stu-id="c89d4-118">Choose hello name of hello IoT hub</span></span>

<span data-ttu-id="c89d4-119">toocreate IOT hub'ı, hello IOT hub'ı adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c89d4-119">toocreate an IoT hub, you must name hello IoT hub.</span></span> <span data-ttu-id="c89d4-120">Bu ad, tüm IOT hub'ları arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c89d4-120">This name must be unique across all IoT hubs.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-hello-pricing-tier"></a><span data-ttu-id="c89d4-121">Merhaba fiyatlandırma katmanı seçin</span><span class="sxs-lookup"><span data-stu-id="c89d4-121">Choose hello pricing tier</span></span>

<span data-ttu-id="c89d4-122">Dört katmanları seçebilirsiniz: **serbest**, **standart 1** ve **standart 2**, ve **standart S3**.</span><span class="sxs-lookup"><span data-stu-id="c89d4-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span></span> <span data-ttu-id="c89d4-123">Hello ücretsiz katmanı 500 aygıtları toobe toohello IOT hub'ı bağlı yalnızca ve too8, günde 000 iletileri yedekleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="c89d4-123">hello free tier allows only 500 devices toobe connected toohello IoT hub and up too8,000 messages per day.</span></span>

<span data-ttu-id="c89d4-124">**Standart S1**: çok sayıda her küçük miktarda veri oluşturur aygıtları çözümlere için kullanım hello S1 sürümü.</span><span class="sxs-lookup"><span data-stu-id="c89d4-124">**Standard S1**: Use hello S1 edition for IoT solutions with a large number of devices that each generate small amounts of data.</span></span> <span data-ttu-id="c89d4-125">Too400, tüm bağlı aygıtlar arasında günde 000 iletileri yukarı hello S1 edition her ölçü sağlar.</span><span class="sxs-lookup"><span data-stu-id="c89d4-125">Each unit of hello S1 edition allows up too400,000 messages per day across all connected devices.</span></span>

<span data-ttu-id="c89d4-126">**Standart S2**: IOT çözümleri cihazları büyük miktarlarda verinin oluşturmak için kullanım hello S2 sürümü.</span><span class="sxs-lookup"><span data-stu-id="c89d4-126">**Standard S2**: Use hello S2 edition for IoT solutions in which devices generate large amounts of data.</span></span> <span data-ttu-id="c89d4-127">Merhaba S2 edition her ölçü too6 tüm bağlı aygıtlar arasında günde milyon iletilerine izin verir.</span><span class="sxs-lookup"><span data-stu-id="c89d4-127">Each unit of hello S2 edition allows up too6 million messages per day between all connected devices.</span></span>

<span data-ttu-id="c89d4-128">**Standart S3**: büyük miktarlarda verinin oluşturmak IOT çözümleri için kullanım hello S3 sürümü.</span><span class="sxs-lookup"><span data-stu-id="c89d4-128">**Standard S3**: Use hello S3 edition for IoT solutions that generate large amounts of data.</span></span> <span data-ttu-id="c89d4-129">Merhaba S3 edition her ölçü too300 tüm bağlı aygıtlar arasında günde milyon iletilerine izin verir.</span><span class="sxs-lookup"><span data-stu-id="c89d4-129">Each unit of hello S3 edition allows up too300 million messages per day between all connected devices.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="c89d4-130">IOT Hub, yalnızca bir ücretsiz hub Azure abonelik başına izin verir.</span><span class="sxs-lookup"><span data-stu-id="c89d4-130">IoT Hub only allows one free hub per Azure subscription.</span></span>

### <a name="iot-hub-units"></a><span data-ttu-id="c89d4-131">IOT hub'ı birimleri</span><span class="sxs-lookup"><span data-stu-id="c89d4-131">IoT hub units</span></span>

<span data-ttu-id="c89d4-132">gün başına birim başına izin verilen ileti Hello sayısı, hub'ın fiyatlandırma katmanında bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="c89d4-132">hello number of messages allowed per unit per day depends on your hub's pricing tier.</span></span> <span data-ttu-id="c89d4-133">Örneğin, IOT hub toosupport giriş 700.000 iletilerinin hello isterseniz, iki S1 katmanı birimleri seçin.</span><span class="sxs-lookup"><span data-stu-id="c89d4-133">For example, if you want hello IoT hub toosupport ingress of 700,000 messages, you choose two S1 tier units.</span></span>

### <a name="device-toocloud-partitions-and-resource-group"></a><span data-ttu-id="c89d4-134">Aygıt toocloud bölümler ve kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="c89d4-134">Device toocloud partitions and resource group</span></span>

<span data-ttu-id="c89d4-135">IOT hub'ı için bölümlerin sayısı hello değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c89d4-135">You can change hello number of partitions for an IoT hub.</span></span> <span data-ttu-id="c89d4-136">Merhaba varsayılan bölüm sayısı 4, farklı bir numara hello aşağı açılan listeden seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c89d4-136">hello default number of partitions is 4, you can choose a different number from hello drop-down list.</span></span>

<span data-ttu-id="c89d4-137">İhtiyacınız olmayan tooexplicitly boş bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c89d4-137">You do not need tooexplicitly create an empty resource group.</span></span> <span data-ttu-id="c89d4-138">Bir kaynak oluşturduğunuzda, yeni bir ya da toocreate seçin veya varolan bir kaynak grubunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="c89d4-138">When you create a resource, you can choose either toocreate a new, or use an existing resource group.</span></span>

![][5]

### <a name="choose-subscription"></a><span data-ttu-id="c89d4-139">Abonelik seçin</span><span class="sxs-lookup"><span data-stu-id="c89d4-139">Choose subscription</span></span>

<span data-ttu-id="c89d4-140">Azure IOT Hub, listeleri hello Azure abonelikleri hello kullanıcı hesabı için otomatik olarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="c89d4-140">Azure IoT Hub automatically lists hello Azure subscriptions hello user account is linked to.</span></span> <span data-ttu-id="c89d4-141">Hello Azure aboneliği tooassociate hello IOT hub'ına seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c89d4-141">You can choose hello Azure subscription tooassociate hello IoT hub to.</span></span>

### <a name="choose-hello-location"></a><span data-ttu-id="c89d4-142">Başlangıç konumu seçin</span><span class="sxs-lookup"><span data-stu-id="c89d4-142">Choose hello location</span></span>

<span data-ttu-id="c89d4-143">IOT hub'ı kullanılabilir olduğu hello bölgelerin bir listesi Hello konum seçeneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="c89d4-143">hello location option provides a list of hello regions where IoT Hub is available.</span></span>

### <a name="create-hello-iot-hub"></a><span data-ttu-id="c89d4-144">Merhaba IOT hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="c89d4-144">Create hello IoT hub</span></span>

<span data-ttu-id="c89d4-145">Önceki adımların tümünü tamamlandığı zaman hello IOT hub'ı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c89d4-145">When all previous steps are complete, you can create hello IoT hub.</span></span> <span data-ttu-id="c89d4-146">Tıklatın **oluşturma** toostart arka uç işlem toocreate hello ve seçtiğiniz hello seçeneklerle hello IOT hub'ı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="c89d4-146">Click **Create** toostart hello back-end process toocreate and deploy hello IoT hub with hello options you chose.</span></span>

<span data-ttu-id="c89d4-147">Merhaba uygun konuma sunucularda hello arka uç dağıtım toorun süredir yararlanırken birkaç dakika toocreate hello IOT hub alabilir.</span><span class="sxs-lookup"><span data-stu-id="c89d4-147">It can take a few minutes toocreate hello IoT hub as it takes time for hello back-end deployment toorun on hello appropriate location servers.</span></span>

## <a name="change-hello-settings-of-hello-iot-hub"></a><span data-ttu-id="c89d4-148">Merhaba IOT hub'ının Hello ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="c89d4-148">Change hello settings of hello IoT hub</span></span>

<span data-ttu-id="c89d4-149">IOT Hub dikey penceresinde hello oluşturulduktan sonra var olan IOT hub'ı hello ayarlarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c89d4-149">You can change hello settings of an existing IoT hub after it is created from hello IoT Hub blade.</span></span>

![][8]

<span data-ttu-id="c89d4-150">**Paylaşılan erişim ilkeleri**: cihazları ve Hizmetleri tooconnect tooIoT Hub hello izinlerini bu ilkeleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c89d4-150">**Shared access policies**: These policies define hello permissions for devices and services tooconnect tooIoT Hub.</span></span> <span data-ttu-id="c89d4-151">Bu ilkeler tıklatarak erişebilirsiniz **paylaşılan erişim ilkeleri** altında **genel**.</span><span class="sxs-lookup"><span data-stu-id="c89d4-151">You can access these policies by clicking **Shared access policies** under **General**.</span></span> <span data-ttu-id="c89d4-152">Bu dikey pencerede, varolan ilkeleri değiştirmek veya yeni bir ilke ekleme.</span><span class="sxs-lookup"><span data-stu-id="c89d4-152">In this blade, you can either modify existing policies or add a new policy.</span></span>

### <a name="create-a-policy"></a><span data-ttu-id="c89d4-153">Bir ilke oluşturun</span><span class="sxs-lookup"><span data-stu-id="c89d4-153">Create a policy</span></span>

* <span data-ttu-id="c89d4-154">Tıklatın **Ekle** tooopen bir dikey pencere.</span><span class="sxs-lookup"><span data-stu-id="c89d4-154">Click **Add** tooopen a blade.</span></span> <span data-ttu-id="c89d4-155">Merhaba yeni ilke adı buraya girin ve hello aşağıda gösterildiği gibi bu ilke ile tooassociate istediğiniz hello izinleri şekil:</span><span class="sxs-lookup"><span data-stu-id="c89d4-155">Here you can enter hello new policy name and hello permissions that you want tooassociate with this policy, as shown in hello following figure:</span></span>

    <span data-ttu-id="c89d4-156">Bu paylaşılan ilkeleriyle ilişkilendirilebilir birkaç izinleri vardır.</span><span class="sxs-lookup"><span data-stu-id="c89d4-156">There are several permissions that can be associated with these shared policies.</span></span> <span data-ttu-id="c89d4-157">Merhaba **okuma kayıt defteri** ve **kayıt defteri yazma** ilkeleri okuma ve yazma erişimi hakları toohello kimlik kayıt defteri verin.</span><span class="sxs-lookup"><span data-stu-id="c89d4-157">hello **Registry read** and **Registry write** policies grant read and write access rights toohello identity registry.</span></span> <span data-ttu-id="c89d4-158">Merhaba yazma seçeneği otomatik olarak seçme seçeneği hello okuma seçer.</span><span class="sxs-lookup"><span data-stu-id="c89d4-158">Choosing hello write option automatically chooses hello read option.</span></span>

    <span data-ttu-id="c89d4-159">Merhaba **Service bağlanma** İlkesi izni tooaccess gibi hizmet uç noktaları verir **alma cihaz bulut**.</span><span class="sxs-lookup"><span data-stu-id="c89d4-159">hello **Service connect** policy grants permission tooaccess service endpoints such as **Receive device-to-cloud**.</span></span> <span data-ttu-id="c89d4-160">Merhaba **aygıtı bağlayın** İlkesi hello IOT Hub cihaz tarafındaki uç noktalarını kullanarak ileti gönderme ve alma için izinler verir.</span><span class="sxs-lookup"><span data-stu-id="c89d4-160">hello **Device connect** policy grants permissions for sending and receiving messages using hello IoT Hub device-side endpoints.</span></span>

* <span data-ttu-id="c89d4-161">Tıklatın **oluşturma** tooadd bu yeni oluşturulmuş İlkesi toohello varolan listesi.</span><span class="sxs-lookup"><span data-stu-id="c89d4-161">Click **Create** tooadd this newly created policy toohello existing list.</span></span>

![][10]

## <a name="endpoints"></a><span data-ttu-id="c89d4-162">Uç Noktalar</span><span class="sxs-lookup"><span data-stu-id="c89d4-162">Endpoints</span></span>

<span data-ttu-id="c89d4-163">Tıklatın **uç noktaları** toodisplay değiştirdiğiniz hello IOT hub için uç nokta listesi.</span><span class="sxs-lookup"><span data-stu-id="c89d4-163">Click **Endpoints** toodisplay a list of endpoints for hello IoT hub that you are modifying.</span></span> <span data-ttu-id="c89d4-164">Uç noktaları iki tür vardır: Merhaba IOT hub'ına yerleşik uç noktaları ve uç noktaları toohello IOT hub'ı oluşturulduktan sonra ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c89d4-164">There are two types of endpoints: endpoints that are built into hello IoT hub, and endpoints that you add toohello IoT hub after its creation.</span></span>

![][11]

### <a name="built-in-endpoints"></a><span data-ttu-id="c89d4-165">Yerleşik uç noktaları</span><span class="sxs-lookup"><span data-stu-id="c89d4-165">Built-in endpoints</span></span>

<span data-ttu-id="c89d4-166">İki yerleşik uç noktalar vardır: **bulut toodevice geri bildirim** ve **olayları**.</span><span class="sxs-lookup"><span data-stu-id="c89d4-166">There are two built-in endpoints: **Cloud toodevice feedback** and **Events**.</span></span>

* <span data-ttu-id="c89d4-167">**Bulut toodevice geri bildirim** ayarları: Bu ayar iki subsettings sahiptir: **tooDevice TTL bulut** (time-to-live) ve **bekletme süresini** (saat) içindeki Merhaba iletileri için.</span><span class="sxs-lookup"><span data-stu-id="c89d4-167">**Cloud toodevice feedback** settings: This setting has two subsettings: **Cloud tooDevice TTL** (time-to-live) and **Retention time** (in hours) for hello messages.</span></span> <span data-ttu-id="c89d4-168">İlk oluşturduğunuzda, IOT hub'ı hem de bu ayarları bir saat hello varsayılan değere sahip.</span><span class="sxs-lookup"><span data-stu-id="c89d4-168">When your first create an IoT hub, both these settings have hello default value of one hour.</span></span> <span data-ttu-id="c89d4-169">tooadjust bu ayarları hello kaydırma çubuklarını kullanın veya hello değerler girin.</span><span class="sxs-lookup"><span data-stu-id="c89d4-169">tooadjust these settings, use hello sliders or type hello values.</span></span>
* <span data-ttu-id="c89d4-170">**Olayları** ayarları: Bu ayar salt okunur bazıları aşağıda verilen birkaç subsettings sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c89d4-170">**Events** settings: This setting has several subsettings, some of which are read-only.</span></span> <span data-ttu-id="c89d4-171">liste aşağıdaki hello bu ayarları açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="c89d4-171">hello following list describes these settings:</span></span>

  * <span data-ttu-id="c89d4-172">**Bölümler**: Merhaba IOT hub'ı oluşturduğunuzda varsayılan bir değer ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="c89d4-172">**Partitions**: A default value is set when hello IoT hub is created.</span></span> <span data-ttu-id="c89d4-173">Bu ayar aracılığıyla bölüm sayısı hello değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c89d4-173">You can change hello number of partitions through this setting.</span></span>

  * <span data-ttu-id="c89d4-174">**Olay Hub ile uyumlu ada ve uç nokta**: Merhaba IOT hub'ı oluşturduğunuzda olay hub'ı dahili olarak, toounder belirli koşullar erişim oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c89d4-174">**Event Hub-compatible name and endpoint**: When hello IoT hub is created, an Event Hub is created internally that you may need access toounder certain circumstances.</span></span> <span data-ttu-id="c89d4-175">Merhaba Event Hub ile uyumlu adı ve uç nokta değerleri özelleştiremezsiniz ancak tıklayarak kopyalayabilirsiniz **kopya**.</span><span class="sxs-lookup"><span data-stu-id="c89d4-175">You cannot customize hello Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span></span>

  * <span data-ttu-id="c89d4-176">**Saklama süresi**: tooone günlük varsayılan olarak ayarlanmış ancak hello açılan listeyi kullanarak değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c89d4-176">**Retention Time**: Set tooone day by default but you can change it using hello drop-down list.</span></span> <span data-ttu-id="c89d4-177">Bu değer hello cihaz bulut ayarı için gün olur.</span><span class="sxs-lookup"><span data-stu-id="c89d4-177">This value is in days for hello device-to-cloud setting.</span></span>

  * <span data-ttu-id="c89d4-178">**Tüketici grupları**: tüketici grupları birden çok okuyucular tooread iletilerden bağımsız olarak hello IOT hub'ı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c89d4-178">**Consumer Groups**: Consumer groups enable multiple readers tooread messages independently from hello IoT hub.</span></span> <span data-ttu-id="c89d4-179">Her IOT hub ile varsayılan bir tüketici grubu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c89d4-179">Every IoT hub is created with a default consumer group.</span></span> <span data-ttu-id="c89d4-180">Ancak, eklemek veya bu ayarı kullanarak tüketici grupları tooyour IOT hub'ları silin.</span><span class="sxs-lookup"><span data-stu-id="c89d4-180">However, you can add or delete consumer groups tooyour IoT hubs using this setting.</span></span>

  > [!NOTE]
  > <span data-ttu-id="c89d4-181">Merhaba varsayılan bir tüketici grubu silinmiş veya düzenlenemez.</span><span class="sxs-lookup"><span data-stu-id="c89d4-181">hello default consumer group cannot be edited or deleted.</span></span>

### <a name="custom-endpoints"></a><span data-ttu-id="c89d4-182">Özel uç noktaları</span><span class="sxs-lookup"><span data-stu-id="c89d4-182">Custom endpoints</span></span>

<span data-ttu-id="c89d4-183">Merhaba portal kullanarak IOT hub'da özel uç noktalar ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c89d4-183">You can add custom endpoints on your IoT hub using hello portal.</span></span> <span data-ttu-id="c89d4-184">Hello gelen **uç noktaları** dikey penceresinde tıklatın **Ekle** hello üst tooopen hello adresindeki **uç nokta ekleyin** dikey.</span><span class="sxs-lookup"><span data-stu-id="c89d4-184">From hello **Endpoints** blade, click **Add** at hello top tooopen hello **Add endpoint** blade.</span></span> <span data-ttu-id="c89d4-185">Merhaba gerekli bilgileri girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="c89d4-185">Enter hello required information, then click **OK**.</span></span> <span data-ttu-id="c89d4-186">Özel uç noktanızı şimdi hello ana listelenen **uç noktaları** dikey.</span><span class="sxs-lookup"><span data-stu-id="c89d4-186">Your custom endpoint is now listed in hello main **Endpoints** blade.</span></span>

![][13]

<span data-ttu-id="c89d4-187">Daha fazla bilgiyi özel uç noktalarını hakkında [başvuru - IOT hub uç noktaları][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="c89d4-187">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span></span>

## <a name="routes"></a><span data-ttu-id="c89d4-188">Yollar</span><span class="sxs-lookup"><span data-stu-id="c89d4-188">Routes</span></span>

<span data-ttu-id="c89d4-189">Tıklatın **yollar** toomanage nasıl IOT Hub, cihaz-bulut iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="c89d4-189">Click **Routes** toomanage how IoT Hub dispatches your device-to-cloud messages.</span></span>

![][14]

<span data-ttu-id="c89d4-190">Yollar tooyour IOT hub'ı tıklatarak ekleyebileceğiniz **Ekle** hello hello üstündeki **yollar*** hello gerekli bilgileri girerek ve tıklayarak dikey **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="c89d4-190">You can add routes tooyour IoT hub by clicking **Add** at hello top of hello **Routes*** blade, entering hello required information, and clicking **OK**.</span></span> <span data-ttu-id="c89d4-191">Rota hello ana sonra listelenen **yollar** dikey.</span><span class="sxs-lookup"><span data-stu-id="c89d4-191">Your route is then listed in hello main **Routes** blade.</span></span> <span data-ttu-id="c89d4-192">Bir rota hello yollar listesinde tıklayarak düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c89d4-192">You can edit a route by clicking it in hello list of routes.</span></span> <span data-ttu-id="c89d4-193">tooenable bir rota yolların hello listeyi tıklatın ve ayarlama hello **etkin** çok geçiş**devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="c89d4-193">tooenable a route, click it in hello list of routes and set hello **Enabled** toggle too**Off**.</span></span> <span data-ttu-id="c89d4-194">toosave hello Değiştir'i tıklatın **Tamam** hello dikey penceresinde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="c89d4-194">toosave hello change, click **OK** at hello bottom of hello blade.</span></span>

![][15]

## <a name="pricing-and-scale"></a><span data-ttu-id="c89d4-195">Fiyatlandırma ve ölçek</span><span class="sxs-lookup"><span data-stu-id="c89d4-195">Pricing and scale</span></span>

<span data-ttu-id="c89d4-196">var olan bir IOT hub ' Hello fiyatlandırma hello değiştirilebilir **fiyatlandırma** ayarlarla hello aşağıdaki özel durumlar:</span><span class="sxs-lookup"><span data-stu-id="c89d4-196">hello pricing of an existing IoT hub can be changed through hello **Pricing** settings, with hello following exceptions:</span></span>

* <span data-ttu-id="c89d4-197">Hello geçerli uygulamasında katmanları tooone SKU'ları, ücretli Merhaba, bir IOT hub ile boş bir SKU değiştirilemiyor veya tam tersi.</span><span class="sxs-lookup"><span data-stu-id="c89d4-197">In hello current implementation, an IoT hub with a free SKU cannot change tiers tooone of hello paid SKUs, or vice versa.</span></span>
* <span data-ttu-id="c89d4-198">Yalnızca olabilir bir ücretsiz katmanı IOT hub'hello Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="c89d4-198">There can only be one free tier IoT hub in hello Azure subscription.</span></span>

![][12]

<span data-ttu-id="c89d4-199">Yalnızca o gün gönderilen ileti sayısını hello hello hello alt katmanı için kotasına zaman daha yüksek bir toolower katmanından taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c89d4-199">You can move from a higher toolower tier only when hello number of messages sent that day do exceed hello quota for hello lower tier.</span></span> <span data-ttu-id="c89d4-200">Örneğin, günde iletilerinin Hello sayısı 400.000 aşarsa, ardından hello IOT hub değiştirilebilir katmanını hello.</span><span class="sxs-lookup"><span data-stu-id="c89d4-200">For example, if hello number of messages per day exceeds 400,000, then hello tier for hello IoT hub can be changed.</span></span> <span data-ttu-id="c89d4-201">Ancak, toohello S1 katmanı değiştirirseniz hello IOT hub'ı o gün için kısıtlanır.</span><span class="sxs-lookup"><span data-stu-id="c89d4-201">However, if you change toohello S1 tier then hello IoT hub is throttled for that day.</span></span>

## <a name="delete-hello-iot-hub"></a><span data-ttu-id="c89d4-202">Merhaba IOT hub'ını silmek</span><span class="sxs-lookup"><span data-stu-id="c89d4-202">Delete hello IoT hub</span></span>

<span data-ttu-id="c89d4-203">Toohello IOT hub'ı tıklatarak toodelete istediğiniz göz atabilirsiniz **Gözat**, ve ardından uygun hub toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="c89d4-203">You can browse toohello IoT hub you want toodelete by clicking **Browse**, and then choosing hello appropriate hub toodelete.</span></span> <span data-ttu-id="c89d4-204">toodelete IOT hub'ı Merhaba, hello tıklatın **silmek** hello IOT hub'ı adı altındaki düğme.</span><span class="sxs-lookup"><span data-stu-id="c89d4-204">toodelete hello IoT hub, click hello **Delete** button below hello IoT hub name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c89d4-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c89d4-205">Next steps</span></span>

<span data-ttu-id="c89d4-206">Azure IOT hub'ı yönetme hakkında daha fazla bu bağlantılar toolearn izleyin:</span><span class="sxs-lookup"><span data-stu-id="c89d4-206">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="c89d4-207">[Toplu IOT cihazları yönetme][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="c89d4-207">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="c89d4-208">[IOT hub'ı ölçümleri][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="c89d4-208">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="c89d4-209">[İzleme işlemleri][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="c89d4-209">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="c89d4-210">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="c89d4-210">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="c89d4-211">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="c89d4-211">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="c89d4-212">[Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="c89d4-212">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="c89d4-213">[IOT çözümünüzden plan hello güvenli][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="c89d4-213">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

[4]: ./media/iot-hub-create-through-portal/create-iothub.png
[5]: ./media/iot-hub-create-through-portal/location1.png
[8]: ./media/iot-hub-create-through-portal/portal-settings.png
[10]: ./media/iot-hub-create-through-portal/shared-access-policies.png
[11]: ./media/iot-hub-create-through-portal/messaging-settings.png
[12]: ./media/iot-hub-create-through-portal/pricing-error.png
[13]: ./media/iot-hub-create-through-portal/endpoint-creation.png
[14]: ./media/iot-hub-create-through-portal/routes-list.png
[15]: ./media/iot-hub-create-through-portal/route-edit.png

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
