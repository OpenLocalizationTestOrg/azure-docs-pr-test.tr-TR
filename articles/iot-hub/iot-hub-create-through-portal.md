---
title: "IOT hub'ı oluşturmak için Azure portalını kullanma | Microsoft Docs"
description: "Nasıl oluşturmak, yönetmek ve Azure Portalı aracılığıyla Azure IOT hub'ları silin. Fiyatlandırma katmanlarına, ölçeklendirme, güvenlik ve yapılandırma Mesajlaşma hakkında bilgi içerir."
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
ms.openlocfilehash: bca7eea5f44bbed3b784b56edaac235161b43e5e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-portal"></a><span data-ttu-id="31128-104">Azure portalını kullanarak IOT hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="31128-104">Create an IoT hub using the Azure portal</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="31128-105">Bu makalede açıklanır:</span><span class="sxs-lookup"><span data-stu-id="31128-105">This article describes:</span></span>

* <span data-ttu-id="31128-106">IOT Hub hizmeti Azure Portalı'nda bulmak nasıl.</span><span class="sxs-lookup"><span data-stu-id="31128-106">How to find the IoT Hub service in the Azure portal.</span></span>
* <span data-ttu-id="31128-107">Oluşturun ve IOT hub'ları yönetmek nasıl.</span><span class="sxs-lookup"><span data-stu-id="31128-107">How to create and manage IoT hubs.</span></span>

## <a name="where-to-find-the-iot-hub-service"></a><span data-ttu-id="31128-108">IOT Hub hizmeti nerede bulacağını</span><span class="sxs-lookup"><span data-stu-id="31128-108">Where to find the IoT Hub service</span></span>

<span data-ttu-id="31128-109">IOT hub'ı servis Portalı'nda aşağıdaki konumlarda bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="31128-109">You can find the IoT Hub service in the following locations in the portal:</span></span>

* <span data-ttu-id="31128-110">Seçin **+ yeni**, ardından **nesnelerin interneti**.</span><span class="sxs-lookup"><span data-stu-id="31128-110">Choose **+ New**, then choose **Internet of Things**.</span></span>
* <span data-ttu-id="31128-111">Marketi'ndeki seçin **nesnelerin interneti**.</span><span class="sxs-lookup"><span data-stu-id="31128-111">In the Marketplace, choose **Internet of Things**.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="31128-112">IoT hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="31128-112">Create an IoT hub</span></span>

<span data-ttu-id="31128-113">IOT hub'ı aşağıdaki yöntemleri kullanarak oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="31128-113">You can create an IoT hub using the following methods:</span></span>

* <span data-ttu-id="31128-114">**+ Yeni** seçeneği aşağıdaki ekran görüntüsünde gösterilen dikey penceresini açar.</span><span class="sxs-lookup"><span data-stu-id="31128-114">The **+ New** option opens the blade shown in the following screen shot.</span></span> <span data-ttu-id="31128-115">IOT hub'ı Marketi ve bu yöntem aracılığıyla oluşturma adımları aynıdır.</span><span class="sxs-lookup"><span data-stu-id="31128-115">The steps for creating the IoT hub through this method and through the marketplace are identical.</span></span>
* <span data-ttu-id="31128-116">Marketi'ndeki seçin **oluşturma** aşağıdaki ekran görüntüsünde gösterilen dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="31128-116">In the Marketplace, choose **Create** to open the blade shown in the following screen shot.</span></span>

<span data-ttu-id="31128-117">Aşağıdaki bölümlerde, IOT hub'ı oluşturma adımları açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="31128-117">The following sections describe the several steps to create an IoT hub:</span></span>

### <a name="choose-the-name-of-the-iot-hub"></a><span data-ttu-id="31128-118">IOT hub adını seçin</span><span class="sxs-lookup"><span data-stu-id="31128-118">Choose the name of the IoT hub</span></span>

<span data-ttu-id="31128-119">IOT hub'ı oluşturmak için IOT hub'ı adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="31128-119">To create an IoT hub, you must name the IoT hub.</span></span> <span data-ttu-id="31128-120">Bu ad, tüm IOT hub'ları arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="31128-120">This name must be unique across all IoT hubs.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-the-pricing-tier"></a><span data-ttu-id="31128-121">Fiyatlandırma katmanı seçin</span><span class="sxs-lookup"><span data-stu-id="31128-121">Choose the pricing tier</span></span>

<span data-ttu-id="31128-122">Dört katmanları seçebilirsiniz: **serbest**, **standart 1** ve **standart 2**, ve **standart S3**.</span><span class="sxs-lookup"><span data-stu-id="31128-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span></span> <span data-ttu-id="31128-123">Ücretsiz katmanı yalnızca 500 cihazların 8.000 iletileri günde en fazla ve IOT hub'ına bağlı izin verir.</span><span class="sxs-lookup"><span data-stu-id="31128-123">The free tier allows only 500 devices to be connected to the IoT hub and up to 8,000 messages per day.</span></span>

<span data-ttu-id="31128-124">**Standart S1**: S1 edition IOT çözümleri için çok sayıda her küçük miktarda veri oluşturur aygıtları kullanın.</span><span class="sxs-lookup"><span data-stu-id="31128-124">**Standard S1**: Use the S1 edition for IoT solutions with a large number of devices that each generate small amounts of data.</span></span> <span data-ttu-id="31128-125">S1 sürümünün her birimi, tüm cihazlarda günde 400.000’e kadar ileti aktarılmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="31128-125">Each unit of the S1 edition allows up to 400,000 messages per day across all connected devices.</span></span>

<span data-ttu-id="31128-126">**Standart S2**: S2 edition IOT çözümleri cihazları büyük miktarlarda verinin oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="31128-126">**Standard S2**: Use the S2 edition for IoT solutions in which devices generate large amounts of data.</span></span> <span data-ttu-id="31128-127">S2 edition her ölçü tüm bağlı aygıtlar arasında günde 6 milyon iletilerine izin verir.</span><span class="sxs-lookup"><span data-stu-id="31128-127">Each unit of the S2 edition allows up to 6 million messages per day between all connected devices.</span></span>

<span data-ttu-id="31128-128">**Standart S3**: S3 edition büyük miktarlarda veri üreten IOT çözümleri için kullanır.</span><span class="sxs-lookup"><span data-stu-id="31128-128">**Standard S3**: Use the S3 edition for IoT solutions that generate large amounts of data.</span></span> <span data-ttu-id="31128-129">S3 edition her ölçü tüm bağlı aygıtlar arasında günde en çok 300 milyon iletilerine izin verir.</span><span class="sxs-lookup"><span data-stu-id="31128-129">Each unit of the S3 edition allows up to 300 million messages per day between all connected devices.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="31128-130">IOT Hub, yalnızca bir ücretsiz hub Azure abonelik başına izin verir.</span><span class="sxs-lookup"><span data-stu-id="31128-130">IoT Hub only allows one free hub per Azure subscription.</span></span>

### <a name="iot-hub-units"></a><span data-ttu-id="31128-131">IOT hub'ı birimleri</span><span class="sxs-lookup"><span data-stu-id="31128-131">IoT hub units</span></span>

<span data-ttu-id="31128-132">Gün başına birim başına izin verilen ileti sayısını, hub'ın fiyatlandırma katmanında bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="31128-132">The number of messages allowed per unit per day depends on your hub's pricing tier.</span></span> <span data-ttu-id="31128-133">Örneğin, IOT hub'ı giriş 700.000 iletilerinin desteklemek için isterseniz, iki S1 katmanı birimleri seçin.</span><span class="sxs-lookup"><span data-stu-id="31128-133">For example, if you want the IoT hub to support ingress of 700,000 messages, you choose two S1 tier units.</span></span>

### <a name="device-to-cloud-partitions-and-resource-group"></a><span data-ttu-id="31128-134">Cihaz bulut bölümleri ve kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="31128-134">Device to cloud partitions and resource group</span></span>

<span data-ttu-id="31128-135">IOT hub'ı için bölümlerin sayısı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31128-135">You can change the number of partitions for an IoT hub.</span></span> <span data-ttu-id="31128-136">Bölüm varsayılan sayısı 4, aşağı açılan listeden farklı bir numara seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31128-136">The default number of partitions is 4, you can choose a different number from the drop-down list.</span></span>

<span data-ttu-id="31128-137">Açıkça bir boş bir kaynak grubu oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="31128-137">You do not need to explicitly create an empty resource group.</span></span> <span data-ttu-id="31128-138">Bir kaynak oluşturduğunuzda, yeni ya da seçin veya varolan bir kaynak grubunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="31128-138">When you create a resource, you can choose either to create a new, or use an existing resource group.</span></span>

![][5]

### <a name="choose-subscription"></a><span data-ttu-id="31128-139">Abonelik seçin</span><span class="sxs-lookup"><span data-stu-id="31128-139">Choose subscription</span></span>

<span data-ttu-id="31128-140">Azure IOT hub'ı otomatik olarak kullanıcı hesabı bağlandığı Azure aboneliklerini listeler.</span><span class="sxs-lookup"><span data-stu-id="31128-140">Azure IoT Hub automatically lists the Azure subscriptions the user account is linked to.</span></span> <span data-ttu-id="31128-141">IOT hub'ına ilişkilendirmek için Azure aboneliği seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31128-141">You can choose the Azure subscription to associate the IoT hub to.</span></span>

### <a name="choose-the-location"></a><span data-ttu-id="31128-142">Konumu seçin</span><span class="sxs-lookup"><span data-stu-id="31128-142">Choose the location</span></span>

<span data-ttu-id="31128-143">Konum seçeneği IOT hub'ı kullanılabilir olduğu bölgelerin bir listesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="31128-143">The location option provides a list of the regions where IoT Hub is available.</span></span>

### <a name="create-the-iot-hub"></a><span data-ttu-id="31128-144">IOT hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="31128-144">Create the IoT hub</span></span>

<span data-ttu-id="31128-145">Önceki adımların tümünü tamamlandığı zaman, IOT hub'ı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31128-145">When all previous steps are complete, you can create the IoT hub.</span></span> <span data-ttu-id="31128-146">Tıklatın **oluşturma** oluşturmak ve seçtiğiniz seçeneklerle IOT hub'ı dağıtmak için arka uç işlemini başlatmak üzere.</span><span class="sxs-lookup"><span data-stu-id="31128-146">Click **Create** to start the back-end process to create and deploy the IoT hub with the options you chose.</span></span>

<span data-ttu-id="31128-147">Süren uygun konuma sunucularda çalıştırmak için arka uç dağıtım için IOT hub'ı oluşturmak için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="31128-147">It can take a few minutes to create the IoT hub as it takes time for the back-end deployment to run on the appropriate location servers.</span></span>

## <a name="change-the-settings-of-the-iot-hub"></a><span data-ttu-id="31128-148">IOT hub'ının ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="31128-148">Change the settings of the IoT hub</span></span>

<span data-ttu-id="31128-149">IOT Hub dikey penceresinden oluşturulduktan sonra var olan IOT hub'ı ayarlarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31128-149">You can change the settings of an existing IoT hub after it is created from the IoT Hub blade.</span></span>

![][8]

<span data-ttu-id="31128-150">**Paylaşılan erişim ilkeleri**: IOT Hub'ına bağlanmak için gerekli izinlere cihazları ve Hizmetleri için bu ilkeleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="31128-150">**Shared access policies**: These policies define the permissions for devices and services to connect to IoT Hub.</span></span> <span data-ttu-id="31128-151">Bu ilkeler tıklatarak erişebilirsiniz **paylaşılan erişim ilkeleri** altında **genel**.</span><span class="sxs-lookup"><span data-stu-id="31128-151">You can access these policies by clicking **Shared access policies** under **General**.</span></span> <span data-ttu-id="31128-152">Bu dikey pencerede, varolan ilkeleri değiştirmek veya yeni bir ilke ekleme.</span><span class="sxs-lookup"><span data-stu-id="31128-152">In this blade, you can either modify existing policies or add a new policy.</span></span>

### <a name="create-a-policy"></a><span data-ttu-id="31128-153">Bir ilke oluşturun</span><span class="sxs-lookup"><span data-stu-id="31128-153">Create a policy</span></span>

* <span data-ttu-id="31128-154">Tıklatın **Ekle** bir dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="31128-154">Click **Add** to open a blade.</span></span> <span data-ttu-id="31128-155">Burada yeni ilke adını ve aşağıdaki çizimde gösterildiği gibi bu ilke ile ilişkilendirmek istediğiniz izinleri girebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="31128-155">Here you can enter the new policy name and the permissions that you want to associate with this policy, as shown in the following figure:</span></span>

    <span data-ttu-id="31128-156">Bu paylaşılan ilkeleriyle ilişkilendirilebilir birkaç izinleri vardır.</span><span class="sxs-lookup"><span data-stu-id="31128-156">There are several permissions that can be associated with these shared policies.</span></span> <span data-ttu-id="31128-157">**Okuma kayıt defteri** ve **kayıt defteri yazma** ilkeleri kimlik kayıt defterini okuma ve yazma erişimi hakkı verin.</span><span class="sxs-lookup"><span data-stu-id="31128-157">The **Registry read** and **Registry write** policies grant read and write access rights to the identity registry.</span></span> <span data-ttu-id="31128-158">Yazma seçeneği otomatik olarak seçme okuma seçeneğini seçer.</span><span class="sxs-lookup"><span data-stu-id="31128-158">Choosing the write option automatically chooses the read option.</span></span>

    <span data-ttu-id="31128-159">**Service bağlanma** İlkesi hizmet uç noktaları gibi erişim izni verir **alma cihaz bulut**.</span><span class="sxs-lookup"><span data-stu-id="31128-159">The **Service connect** policy grants permission to access service endpoints such as **Receive device-to-cloud**.</span></span> <span data-ttu-id="31128-160">**Aygıtı bağlayın** İlkesi IOT Hub cihaz tarafındaki uç kullanarak ileti gönderme ve alma için izinler verir.</span><span class="sxs-lookup"><span data-stu-id="31128-160">The **Device connect** policy grants permissions for sending and receiving messages using the IoT Hub device-side endpoints.</span></span>

* <span data-ttu-id="31128-161">Tıklatın **oluşturma** bu yeni ilke varolan listesine oluşturulan eklemek için.</span><span class="sxs-lookup"><span data-stu-id="31128-161">Click **Create** to add this newly created policy to the existing list.</span></span>

![][10]

## <a name="endpoints"></a><span data-ttu-id="31128-162">Uç Noktalar</span><span class="sxs-lookup"><span data-stu-id="31128-162">Endpoints</span></span>

<span data-ttu-id="31128-163">Tıklatın **uç noktaları** değiştirdiğiniz IOT hub'ı uç noktaları listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="31128-163">Click **Endpoints** to display a list of endpoints for the IoT hub that you are modifying.</span></span> <span data-ttu-id="31128-164">Uç noktaları iki tür vardır: IOT hub'ına yerleşik uç noktaları ve IOT hub'ına oluşturulduktan sonra eklediğiniz uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="31128-164">There are two types of endpoints: endpoints that are built into the IoT hub, and endpoints that you add to the IoT hub after its creation.</span></span>

![][11]

### <a name="built-in-endpoints"></a><span data-ttu-id="31128-165">Yerleşik uç noktaları</span><span class="sxs-lookup"><span data-stu-id="31128-165">Built-in endpoints</span></span>

<span data-ttu-id="31128-166">İki yerleşik uç noktalar vardır: **aygıt geri bildirim buluta** ve **olayları**.</span><span class="sxs-lookup"><span data-stu-id="31128-166">There are two built-in endpoints: **Cloud to device feedback** and **Events**.</span></span>

* <span data-ttu-id="31128-167">**Cihaz geri bildirim buluta** ayarları: Bu ayar iki subsettings sahiptir: **aygıt TTL bulut** (time-to-live) ve **bekletme süresini** (saat) içindeki iletiler için.</span><span class="sxs-lookup"><span data-stu-id="31128-167">**Cloud to device feedback** settings: This setting has two subsettings: **Cloud to Device TTL** (time-to-live) and **Retention time** (in hours) for the messages.</span></span> <span data-ttu-id="31128-168">İlk IOT hub'ı oluşturduğunuzda, hem bu ayarları bir saatlik varsayılan değere sahip.</span><span class="sxs-lookup"><span data-stu-id="31128-168">When your first create an IoT hub, both these settings have the default value of one hour.</span></span> <span data-ttu-id="31128-169">Bu ayarları ayarlamak için kaydırma çubuklarını kullanın veya değerleri yazın.</span><span class="sxs-lookup"><span data-stu-id="31128-169">To adjust these settings, use the sliders or type the values.</span></span>
* <span data-ttu-id="31128-170">**Olayları** ayarları: Bu ayar salt okunur bazıları aşağıda verilen birkaç subsettings sahiptir.</span><span class="sxs-lookup"><span data-stu-id="31128-170">**Events** settings: This setting has several subsettings, some of which are read-only.</span></span> <span data-ttu-id="31128-171">Aşağıdaki listede, bu ayarları açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="31128-171">The following list describes these settings:</span></span>

  * <span data-ttu-id="31128-172">**Bölümler**: IOT hub'ı oluşturduğunuzda varsayılan bir değer ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="31128-172">**Partitions**: A default value is set when the IoT hub is created.</span></span> <span data-ttu-id="31128-173">Bu ayar aracılığıyla bölüm sayısı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31128-173">You can change the number of partitions through this setting.</span></span>

  * <span data-ttu-id="31128-174">**Olay Hub ile uyumlu ada ve uç nokta**: zaman IOT hub'ı oluşturulur, bir olay hub'ı belirli koşullar altında erişimi gerekebilir dahili olarak oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="31128-174">**Event Hub-compatible name and endpoint**: When the IoT hub is created, an Event Hub is created internally that you may need access to under certain circumstances.</span></span> <span data-ttu-id="31128-175">Event Hub ile uyumlu adı ve uç nokta değerleri özelleştiremezsiniz ancak tıklayarak kopyalayabilirsiniz **kopya**.</span><span class="sxs-lookup"><span data-stu-id="31128-175">You cannot customize the Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span></span>

  * <span data-ttu-id="31128-176">**Saklama süresi**: varsayılan olarak bir gün olarak ayarlayın ancak açılan listeyi kullanarak değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31128-176">**Retention Time**: Set to one day by default but you can change it using the drop-down list.</span></span> <span data-ttu-id="31128-177">Bu değer, cihaz bulut ayarı için gün olur.</span><span class="sxs-lookup"><span data-stu-id="31128-177">This value is in days for the device-to-cloud setting.</span></span>

  * <span data-ttu-id="31128-178">**Tüketici grupları**: tüketici grupları iletileri IOT hub'ından bağımsız olarak okumak birden çok okuyucular etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="31128-178">**Consumer Groups**: Consumer groups enable multiple readers to read messages independently from the IoT hub.</span></span> <span data-ttu-id="31128-179">Her IOT hub ile varsayılan bir tüketici grubu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="31128-179">Every IoT hub is created with a default consumer group.</span></span> <span data-ttu-id="31128-180">Ancak, eklemek veya bu ayarı kullanarak, IOT hub tüketici grupları silin.</span><span class="sxs-lookup"><span data-stu-id="31128-180">However, you can add or delete consumer groups to your IoT hubs using this setting.</span></span>

  > [!NOTE]
  > <span data-ttu-id="31128-181">Varsayılan bir tüketici grubu silinmiş veya düzenlenemez.</span><span class="sxs-lookup"><span data-stu-id="31128-181">The default consumer group cannot be edited or deleted.</span></span>

### <a name="custom-endpoints"></a><span data-ttu-id="31128-182">Özel uç noktaları</span><span class="sxs-lookup"><span data-stu-id="31128-182">Custom endpoints</span></span>

<span data-ttu-id="31128-183">Portalı kullanarak, IOT hub'ına özel uç noktalar ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31128-183">You can add custom endpoints on your IoT hub using the portal.</span></span> <span data-ttu-id="31128-184">Gelen **uç noktaları** dikey penceresinde tıklatın **Ekle** açmak için üst **uç nokta ekleme** dikey.</span><span class="sxs-lookup"><span data-stu-id="31128-184">From the **Endpoints** blade, click **Add** at the top to open the **Add endpoint** blade.</span></span> <span data-ttu-id="31128-185">Gerekli bilgileri girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="31128-185">Enter the required information, then click **OK**.</span></span> <span data-ttu-id="31128-186">Özel uç noktanızı şimdi ana listelenen **uç noktaları** dikey.</span><span class="sxs-lookup"><span data-stu-id="31128-186">Your custom endpoint is now listed in the main **Endpoints** blade.</span></span>

![][13]

<span data-ttu-id="31128-187">Daha fazla bilgiyi özel uç noktalarını hakkında [başvuru - IOT hub uç noktaları][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="31128-187">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span></span>

## <a name="routes"></a><span data-ttu-id="31128-188">Yollar</span><span class="sxs-lookup"><span data-stu-id="31128-188">Routes</span></span>

<span data-ttu-id="31128-189">Tıklatın **yollar** nasıl IOT Hub, cihaz bulut iletilerini gönderir yönetmek için.</span><span class="sxs-lookup"><span data-stu-id="31128-189">Click **Routes** to manage how IoT Hub dispatches your device-to-cloud messages.</span></span>

![][14]

<span data-ttu-id="31128-190">Tıklayarak IOT hub'ınıza yollar ekleyebilirsiniz **Ekle** en üstündeki **yollar*** gerekli bilgileri girerek ve tıklayarak dikey **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="31128-190">You can add routes to your IoT hub by clicking **Add** at the top of the **Routes*** blade, entering the required information, and clicking **OK**.</span></span> <span data-ttu-id="31128-191">Rota sonra ana listelenen **yollar** dikey.</span><span class="sxs-lookup"><span data-stu-id="31128-191">Your route is then listed in the main **Routes** blade.</span></span> <span data-ttu-id="31128-192">Bir rota yollar listesinde tıklayarak düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31128-192">You can edit a route by clicking it in the list of routes.</span></span> <span data-ttu-id="31128-193">Bir rota etkinleştirmek için yollar listesinde tıklatın ve ayarlamak **etkin** geç **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="31128-193">To enable a route, click it in the list of routes and set the **Enabled** toggle to **Off**.</span></span> <span data-ttu-id="31128-194">Değişikliği kaydetmek için tıklatın **Tamam** dikey pencerenin altındaki.</span><span class="sxs-lookup"><span data-stu-id="31128-194">To save the change, click **OK** at the bottom of the blade.</span></span>

![][15]

## <a name="pricing-and-scale"></a><span data-ttu-id="31128-195">Fiyatlandırma ve ölçek</span><span class="sxs-lookup"><span data-stu-id="31128-195">Pricing and scale</span></span>

<span data-ttu-id="31128-196">Var olan bir IOT hub ' fiyatlandırma üzerinden değiştirilebilir **fiyatlandırma** aşağıdaki istisnalar dışında ayarları:</span><span class="sxs-lookup"><span data-stu-id="31128-196">The pricing of an existing IoT hub can be changed through the **Pricing** settings, with the following exceptions:</span></span>

* <span data-ttu-id="31128-197">Geçerli uygulama, bir IOT hub ile boş bir SKU katmanları Ücretli SKU birine değiştirilemiyor veya tam tersi.</span><span class="sxs-lookup"><span data-stu-id="31128-197">In the current implementation, an IoT hub with a free SKU cannot change tiers to one of the paid SKUs, or vice versa.</span></span>
* <span data-ttu-id="31128-198">Yalnızca olabilir ücretsiz katmanı IOT hub'ın bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="31128-198">There can only be one free tier IoT hub in the Azure subscription.</span></span>

![][12]

<span data-ttu-id="31128-199">Yalnızca o gün gönderilen ileti sayısını alt katmanı için kota aştıklarında, daha yüksek alt katmanına taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31128-199">You can move from a higher to lower tier only when the number of messages sent that day do exceed the quota for the lower tier.</span></span> <span data-ttu-id="31128-200">Gün başına ileti sayısını 400.000 aşarsa, örneğin, ardından katman IOT hub'ı için değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="31128-200">For example, if the number of messages per day exceeds 400,000, then the tier for the IoT hub can be changed.</span></span> <span data-ttu-id="31128-201">Ancak, S1 katmanı değiştirirseniz, IOT hub'ı o gün için kısıtlanır.</span><span class="sxs-lookup"><span data-stu-id="31128-201">However, if you change to the S1 tier then the IoT hub is throttled for that day.</span></span>

## <a name="delete-the-iot-hub"></a><span data-ttu-id="31128-202">IOT hub'ını silmek</span><span class="sxs-lookup"><span data-stu-id="31128-202">Delete the IoT hub</span></span>

<span data-ttu-id="31128-203">IOT hub'ı tıklatarak silmek gözatabilirsiniz **Gözat**ve silmek için uygun hub'ı seçerek.</span><span class="sxs-lookup"><span data-stu-id="31128-203">You can browse to the IoT hub you want to delete by clicking **Browse**, and then choosing the appropriate hub to delete.</span></span> <span data-ttu-id="31128-204">IOT hub'ını silmek için tıklatın **silmek** IOT hub'ı adı altındaki düğme.</span><span class="sxs-lookup"><span data-stu-id="31128-204">To delete the IoT hub, click the **Delete** button below the IoT hub name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31128-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="31128-205">Next steps</span></span>

<span data-ttu-id="31128-206">Azure IOT hub'ı yönetme hakkında daha fazla bilgi için bu bağlantıları izleyin:</span><span class="sxs-lookup"><span data-stu-id="31128-206">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="31128-207">[Toplu IOT cihazları yönetme][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="31128-207">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="31128-208">[IOT hub'ı ölçümleri][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="31128-208">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="31128-209">[İzleme işlemleri][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="31128-209">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="31128-210">Daha fazla IOT hub'ı özelliklerini keşfetmek için bkz:</span><span class="sxs-lookup"><span data-stu-id="31128-210">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="31128-211">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="31128-211">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="31128-212">[Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="31128-212">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="31128-213">[IOT çözümünüzden zemin oluşturan güvenli][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="31128-213">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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
