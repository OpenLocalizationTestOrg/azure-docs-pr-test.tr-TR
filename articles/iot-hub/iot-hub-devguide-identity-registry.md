---
title: "Azure IOT Hub kimlik kayıt defteri anlama | Microsoft Docs"
description: "Geliştirici Kılavuzu - açıklaması IOT Hub kimlik kayıt defteri ve cihazlarınızı yönetmek için kullanma. Toplu olarak içeri ve dışarı aktarma cihaz kimlikleri hakkında bilgi içerir."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0706eccd-e84c-4ae7-bbd4-2b1a22241147
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6e9c7b71fa6fc78f97c0144c735fc44778181d8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="understand-the-identity-registry-in-your-iot-hub"></a><span data-ttu-id="6a54d-104">IOT hub'ınızdaki kimlik kayıt defterinde anlama</span><span class="sxs-lookup"><span data-stu-id="6a54d-104">Understand the identity registry in your IoT hub</span></span>

<span data-ttu-id="6a54d-105">Her IOT hub'ı IOT hub'ına bağlanmasına izin verilen cihazlar hakkındaki bilgileri depolayan bir kimlik kayıt defteri sahiptir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-105">Every IoT hub has an identity registry that stores information about the devices permitted to connect to the IoT hub.</span></span> <span data-ttu-id="6a54d-106">Bir cihaz IOT hub'a bağlanmadan önce bir cihazın IOT hub'ın kimlik kayıt defterinde girişi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6a54d-106">Before a device can connect to an IoT hub, there must be an entry for that device in the IoT hub's identity registry.</span></span> <span data-ttu-id="6a54d-107">Ayrıca, bir cihaz kimlik kayıt defterinde depolanan kimlik bilgileri dayalı IOT hub ile doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-107">A device must also authenticate with the IoT hub based on credentials stored in the identity registry.</span></span>

<span data-ttu-id="6a54d-108">Kimlik kayıt defterinde depolanan cihaz kimliği büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="6a54d-108">The device ID stored in the identity registry is case-sensitive.</span></span>

<span data-ttu-id="6a54d-109">Yüksek düzeyde, kimlik kayıt defteri REST özellikli cihaz kimlik kaynakları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="6a54d-109">At a high level, the identity registry is a REST-capable collection of device identity resources.</span></span> <span data-ttu-id="6a54d-110">Bir giriş kimlik kayıt defterinde eklediğinizde, IOT Hub cihaz başına kaynakları yürütülen bulut-cihaz iletilerini içeren sıranın gibi bir dizi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6a54d-110">When you add an entry in the identity registry, IoT Hub creates a set of per-device resources such as the queue that contains in-flight cloud-to-device messages.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="6a54d-111">Kullanılması gereken durumlar</span><span class="sxs-lookup"><span data-stu-id="6a54d-111">When to use</span></span>

<span data-ttu-id="6a54d-112">Gerektiğinde kimlik kayıt defteri kullanın:</span><span class="sxs-lookup"><span data-stu-id="6a54d-112">Use the identity registry when you need to:</span></span>

* <span data-ttu-id="6a54d-113">IOT hub'ınıza bağlanın cihazları sağlamak.</span><span class="sxs-lookup"><span data-stu-id="6a54d-113">Provision devices that connect to your IoT hub.</span></span>
* <span data-ttu-id="6a54d-114">Hub'ın aygıt'e yönelik uç noktalar aygıt başına erişimi denetler.</span><span class="sxs-lookup"><span data-stu-id="6a54d-114">Control per-device access to your hub's device-facing endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="6a54d-115">Kimlik kayıt defteri herhangi bir uygulamaya özgü meta veri içermiyor.</span><span class="sxs-lookup"><span data-stu-id="6a54d-115">The identity registry does not contain any application-specific metadata.</span></span>

## <a name="identity-registry-operations"></a><span data-ttu-id="6a54d-116">Kimlik kayıt defteri işlemleri</span><span class="sxs-lookup"><span data-stu-id="6a54d-116">Identity registry operations</span></span>

<span data-ttu-id="6a54d-117">IOT Hub kimlik kayıt defteri aşağıdaki işlemleri sunar:</span><span class="sxs-lookup"><span data-stu-id="6a54d-117">The IoT Hub identity registry exposes the following operations:</span></span>

* <span data-ttu-id="6a54d-118">Cihaz kimliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="6a54d-118">Create device identity</span></span>
* <span data-ttu-id="6a54d-119">Güncelleştirme cihaz kimliği</span><span class="sxs-lookup"><span data-stu-id="6a54d-119">Update device identity</span></span>
* <span data-ttu-id="6a54d-120">Cihaz kimliği Kimliğine göre alma</span><span class="sxs-lookup"><span data-stu-id="6a54d-120">Retrieve device identity by ID</span></span>
* <span data-ttu-id="6a54d-121">Cihaz Kimliği Sil</span><span class="sxs-lookup"><span data-stu-id="6a54d-121">Delete device identity</span></span>
* <span data-ttu-id="6a54d-122">En fazla 1000 kimlikleri listesi</span><span class="sxs-lookup"><span data-stu-id="6a54d-122">List up to 1000 identities</span></span>
* <span data-ttu-id="6a54d-123">Tüm kimlikler Azure blob depolama alanına dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="6a54d-123">Export all identities to Azure blob storage</span></span>
* <span data-ttu-id="6a54d-124">Azure blob depolama alanından kimlikleri alma</span><span class="sxs-lookup"><span data-stu-id="6a54d-124">Import identities from Azure blob storage</span></span>

<span data-ttu-id="6a54d-125">Bu işlemler belirtildiği gibi iyimser eşzamanlılık kullanabilirsiniz [RFC7232][lnk-rfc7232].</span><span class="sxs-lookup"><span data-stu-id="6a54d-125">All these operations can use optimistic concurrency, as specified in [RFC7232][lnk-rfc7232].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a54d-126">Bir IOT hub'ın kimlik kayıt defterinde tüm kimlikleri almanın tek yolu kullanmaktır [verme] [ lnk-export] işlevselliği.</span><span class="sxs-lookup"><span data-stu-id="6a54d-126">The only way to retrieve all identities in an IoT hub's identity registry is to use the [Export][lnk-export] functionality.</span></span>

<span data-ttu-id="6a54d-127">Bir IOT Hub kimlik kayıt defteri:</span><span class="sxs-lookup"><span data-stu-id="6a54d-127">An IoT Hub identity registry:</span></span>

* <span data-ttu-id="6a54d-128">Herhangi bir uygulama meta veri içermiyor.</span><span class="sxs-lookup"><span data-stu-id="6a54d-128">Does not contain any application metadata.</span></span>
* <span data-ttu-id="6a54d-129">Kullanarak bir sözlük gibi erişilebilir **DeviceID** anahtar olarak.</span><span class="sxs-lookup"><span data-stu-id="6a54d-129">Can be accessed like a dictionary, by using the **deviceId** as the key.</span></span>
* <span data-ttu-id="6a54d-130">Açıklayıcı sorguları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="6a54d-130">Does not support expressive queries.</span></span>

<span data-ttu-id="6a54d-131">Bir IOT çözüm genellikle uygulamaya özgü meta veriler içeren ayrı bir çözüme özel deposu vardır.</span><span class="sxs-lookup"><span data-stu-id="6a54d-131">An IoT solution typically has a separate solution-specific store that contains application-specific metadata.</span></span> <span data-ttu-id="6a54d-132">Örneğin, bir akıllı yapı çözümü çözüme özel deposunda sıcaklık algılayıcısı dağıtıldığı yer kaydedebilir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-132">For example, the solution-specific store in a smart building solution would record the room in which a temperature sensor is deployed.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a54d-133">Yalnızca kimlik kayıt defteri aygıt yönetimi ve işlemleri sağlama için kullanın.</span><span class="sxs-lookup"><span data-stu-id="6a54d-133">Only use the identity registry for device management and provisioning operations.</span></span> <span data-ttu-id="6a54d-134">Çalışma zamanında yüksek verimlilik işlemleri kimlik kayıt defterinde işlemlerini gerçekleştirme üzerinde bağlı olmaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-134">High throughput operations at run time should not depend on performing operations in the identity registry.</span></span> <span data-ttu-id="6a54d-135">Örneğin, bir cihaz bağlantı durumunun bir komut göndermeden önce desteklenen desen olmadığı denetleniyor.</span><span class="sxs-lookup"><span data-stu-id="6a54d-135">For example, checking the connection state of a device before sending a command is not a supported pattern.</span></span> <span data-ttu-id="6a54d-136">Denetlediğinizden emin olun [oranları azaltma] [ lnk-quotas] kimlik kayıt defteri ve [aygıt sinyal] [ lnk-guidance-heartbeat] düzeni.</span><span class="sxs-lookup"><span data-stu-id="6a54d-136">Make sure to check the [throttling rates][lnk-quotas] for the identity registry, and the [device heartbeat][lnk-guidance-heartbeat] pattern.</span></span>

## <a name="disable-devices"></a><span data-ttu-id="6a54d-137">Cihazları devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="6a54d-137">Disable devices</span></span>

<span data-ttu-id="6a54d-138">Güncelleştirerek aygıtlarını devre dışı bırakabilir **durum** kimlik kayıt defterinde bir kimlik özelliği.</span><span class="sxs-lookup"><span data-stu-id="6a54d-138">You can disable devices by updating the **status** property of an identity in the identity registry.</span></span> <span data-ttu-id="6a54d-139">Genellikle, iki senaryoda bu özelliği kullanın:</span><span class="sxs-lookup"><span data-stu-id="6a54d-139">Typically, you use this property in two scenarios:</span></span>

* <span data-ttu-id="6a54d-140">Sağlama orchestration sürecinde.</span><span class="sxs-lookup"><span data-stu-id="6a54d-140">During a provisioning orchestration process.</span></span> <span data-ttu-id="6a54d-141">Daha fazla bilgi için bkz: [cihaz sağlamayı][lnk-guidance-provisioning].</span><span class="sxs-lookup"><span data-stu-id="6a54d-141">For more information, see [Device Provisioning][lnk-guidance-provisioning].</span></span>
* <span data-ttu-id="6a54d-142">Kullanıyorsanız herhangi bir nedenle bir aygıt tehlikeye veya yetkisiz duruma geldi düşünün.</span><span class="sxs-lookup"><span data-stu-id="6a54d-142">If, for any reason, you consider a device is compromised or has become unauthorized.</span></span>

## <a name="import-and-export-device-identities"></a><span data-ttu-id="6a54d-143">İçeri ve dışarı aktarma aygıt kimlikleri</span><span class="sxs-lookup"><span data-stu-id="6a54d-143">Import and export device identities</span></span>

<span data-ttu-id="6a54d-144">Zaman uyumsuz işlemleri kullanarak bir IOT hub'ın kimlik kayıt defterinden toplu cihaz kimliklerini verebilirsiniz [IOT hub'ı kaynak sağlayıcı uç][lnk-endpoints].</span><span class="sxs-lookup"><span data-stu-id="6a54d-144">You can export device identities in bulk from an IoT hub's identity registry, by using asynchronous operations on the [IoT Hub resource provider endpoint][lnk-endpoints].</span></span> <span data-ttu-id="6a54d-145">Olan kimlik kayıt defterinden okunacak aygıt kimlik verilerini kaydetmek için müşteri tarafından sağlanan blob kapsayıcısı kullanmak uzun süre çalışan işleri dışarı aktarır.</span><span class="sxs-lookup"><span data-stu-id="6a54d-145">Exports are long-running jobs that use a customer-supplied blob container to save device identity data read from the identity registry.</span></span>

<span data-ttu-id="6a54d-146">Zaman uyumsuz işlemleri kullanarak bir IOT hub'ın kimlik kayıt defterine toplu cihaz kimliklerini aktarabilirsiniz [IOT hub'ı kaynak sağlayıcı uç][lnk-endpoints].</span><span class="sxs-lookup"><span data-stu-id="6a54d-146">You can import device identities in bulk to an IoT hub's identity registry, by using asynchronous operations on the [IoT Hub resource provider endpoint][lnk-endpoints].</span></span> <span data-ttu-id="6a54d-147">İçeri aktarmalar olan kimlik kayıt defterine aygıt kimlik verilerini yazmak için bir müşteri tarafından sağlanan blob kapsayıcısında verileri kullanmak uzun süre çalışan işleri.</span><span class="sxs-lookup"><span data-stu-id="6a54d-147">Imports are long-running jobs that use data in a customer-supplied blob container to write device identity data into the identity registry.</span></span>

* <span data-ttu-id="6a54d-148">İçeri ve dışarı aktarma API'ler hakkında ayrıntılı bilgi için bkz: [IOT hub'ı kaynak sağlayıcısı REST API'leri][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="6a54d-148">For detailed information about the import and export APIs, see [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span>
* <span data-ttu-id="6a54d-149">İçeri aktarma çalıştırma hakkında daha fazla bilgi edinin ve işleri dışarı aktarmak için bkz: [toplu yönetim IOT Hub cihaz kimlikleri][lnk-bulk-identity].</span><span class="sxs-lookup"><span data-stu-id="6a54d-149">To learn more about running import and export jobs, see [Bulk management of IoT Hub device identities][lnk-bulk-identity].</span></span>

## <a name="device-provisioning"></a><span data-ttu-id="6a54d-150">Cihaz sağlama</span><span class="sxs-lookup"><span data-stu-id="6a54d-150">Device provisioning</span></span>

<span data-ttu-id="6a54d-151">Belirli bir IOT çözüm depolar cihaz verileri bu çözüm belirli gereksinimlerine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="6a54d-151">The device data that a given IoT solution stores depends on the specific requirements of that solution.</span></span> <span data-ttu-id="6a54d-152">Ancak, en az bir çözüm cihaz kimliklerini ve kimlik doğrulama anahtarları depolamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-152">But, as a minimum, a solution must store device identities and authentication keys.</span></span> <span data-ttu-id="6a54d-153">Azure IOT Hub kimlikleri, kimlik doğrulama anahtarları ve durum kodları gibi her bir cihaz için değerler saklayabilirsiniz bir kimlik kayıt defterini içerir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-153">Azure IoT Hub includes an identity registry that can store values for each device such as IDs, authentication keys, and status codes.</span></span> <span data-ttu-id="6a54d-154">Bir çözüm, herhangi bir ek aygıt veri depolamak için tablo, blob depolama veya Cosmos DB gibi diğer Azure hizmetleriyle kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a54d-154">A solution can use other Azure services such as table storage, blob storage, or Cosmos DB to store any additional device data.</span></span>

<span data-ttu-id="6a54d-155">*Cihaz sağlama* ilk cihaz veri depolarına çözümünüzdeki ekleme işlemidir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-155">*Device provisioning* is the process of adding the initial device data to the stores in your solution.</span></span> <span data-ttu-id="6a54d-156">Hub'ınıza bağlanmak yeni bir cihaz etkinleştirmek için bir cihaz kimliği ve anahtarları IOT Hub kimlik kayıt defterine eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-156">To enable a new device to connect to your hub, you must add a device ID and keys to the IoT Hub identity registry.</span></span> <span data-ttu-id="6a54d-157">Hazırlama işleminin bir parçası olarak, diğer çözüm depolarında aygıta özgü verileri başlatma gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-157">As part of the provisioning process, you might need to initialize device-specific data in other solution stores.</span></span>

## <a name="device-heartbeat"></a><span data-ttu-id="6a54d-158">Cihaz sinyal</span><span class="sxs-lookup"><span data-stu-id="6a54d-158">Device heartbeat</span></span>

<span data-ttu-id="6a54d-159">IOT Hub kimlik kayıt adlı bir alanı içeren **connectionState**.</span><span class="sxs-lookup"><span data-stu-id="6a54d-159">The IoT Hub identity registry contains a field called **connectionState**.</span></span> <span data-ttu-id="6a54d-160">Yalnızca **connectionState** geliştirme ve hata ayıklama sırasında alan.</span><span class="sxs-lookup"><span data-stu-id="6a54d-160">Only use the **connectionState** field during development and debugging.</span></span> <span data-ttu-id="6a54d-161">IOT çözümleri alanın çalışma zamanında sorgu değil.</span><span class="sxs-lookup"><span data-stu-id="6a54d-161">IoT solutions should not query the field at run time.</span></span> <span data-ttu-id="6a54d-162">Örneğin, değil sorgu **connectionState** alan bir bulut cihaz ileti veya SMS göndermeden önce bir aygıt bağlı olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="6a54d-162">For example, do not query the **connectionState** field to check if a device is connected before you send a cloud-to-device message or an SMS.</span></span>

<span data-ttu-id="6a54d-163">IOT çözümünüzün bir aygıt bağlıysa, uygulamanız gerekir bilmeniz gerekiyorsa *sinyal düzeni*.</span><span class="sxs-lookup"><span data-stu-id="6a54d-163">If your IoT solution needs to know if a device is connected, you should implement the *heartbeat pattern*.</span></span>

<span data-ttu-id="6a54d-164">Sinyal desende aygıt en az bir kez her sabit süreyi (örneğin, en az bir kez her saat) cihaz bulut iletilerini gönderir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-164">In the heartbeat pattern, the device sends device-to-cloud messages at least once every fixed amount of time (for example, at least once every hour).</span></span> <span data-ttu-id="6a54d-165">Bu nedenle, bir cihaz göndermek için herhangi bir veri sahip değilse, hala bir boş cihaz bulut iletisiyle (genellikle bir sinyal tanımlayan bir özellik) gönderir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-165">Therefore, even if a device does not have any data to send, it still sends an empty device-to-cloud message (usually with a property that identifies it as a heartbeat).</span></span> <span data-ttu-id="6a54d-166">Hizmet tarafında çözümü her cihaz için alınan son sinyal ile bir eşleme tutar.</span><span class="sxs-lookup"><span data-stu-id="6a54d-166">On the service side, the solution maintains a map with the last heartbeat received for each device.</span></span> <span data-ttu-id="6a54d-167">Çözüm aygıttan beklenen süre içinde bir sinyal iletisi almazsa, cihaz ile ilgili bir sorun olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="6a54d-167">If the solution does not receive a heartbeat message within the expected time from the device, it assumes that there is a problem with the device.</span></span>

<span data-ttu-id="6a54d-168">Daha karmaşık bir uygulama bilgileri içerebilir [izleme işlemleri] [ lnk-devguide-opmon] bağlanmak veya iletişim kurmak çalışıyor, ancak başarısız olan cihazları tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a54d-168">A more complex implementation could include the information from [operations monitoring][lnk-devguide-opmon] to identify devices that are trying to connect or communicate but failing.</span></span> <span data-ttu-id="6a54d-169">Sinyal düzeni uyguladığınızda olduğundan emin olun [IOT Hub kotaları ve kısıtlamaları][lnk-quotas].</span><span class="sxs-lookup"><span data-stu-id="6a54d-169">When you implement the heartbeat pattern, make sure to check [IoT Hub Quotas and Throttles][lnk-quotas].</span></span>

> [!NOTE]
> <span data-ttu-id="6a54d-170">Yalnızca bulut cihaz iletileri gönderilip gönderilmeyeceğini belirlemek için bağlantı durumu IOT çözümünü kullanır ve iletileri değil aygıtlarını büyük kümeleri için yayını basit kullanmayı *kısa süre sonu zamanı* düzeni.</span><span class="sxs-lookup"><span data-stu-id="6a54d-170">If an IoT solution uses the connection state solely to determine whether to send cloud-to-device messages, and messages are not broadcast to large sets of devices, consider using the simpler *short expiry time* pattern.</span></span> <span data-ttu-id="6a54d-171">Bu desen daha verimli devam ederken sinyal desenini kullanarak bir aygıtı bağlantı durumu kayıt Bakımı aynı sonucu elde eder.</span><span class="sxs-lookup"><span data-stu-id="6a54d-171">This pattern achieves the same result as maintaining a device connection state registry using the heartbeat pattern, while being more efficient.</span></span> <span data-ttu-id="6a54d-172">İleti onayları isterse, IOT Hub, hangi aygıtların hakkında iletiler alabilir ve hangi bildirebilir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-172">If you request message acknowledgements, IoT Hub can notify you about which devices are able to receive messages and which are not.</span></span>

## <a name="device-lifecycle-notifications"></a><span data-ttu-id="6a54d-173">Cihaz yaşam döngüsü bildirimleri</span><span class="sxs-lookup"><span data-stu-id="6a54d-173">Device lifecycle notifications</span></span>

<span data-ttu-id="6a54d-174">Bir cihaz kimliği oluşturulduğunda veya cihaz yaşam döngüsü bildirimleri göndererek silinmiş IOT hub'ı IOT çözümünüzü bildirebilir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-174">IoT Hub can notify your IoT solution when a device identity is created or deleted by sending device lifecycle notifications.</span></span> <span data-ttu-id="6a54d-175">Bunu yapmak için IOT çözümünüzün bir rota oluşturmak ve veri kaynağı eşit ayarlamak için gereken *DeviceLifecycleEvents*.</span><span class="sxs-lookup"><span data-stu-id="6a54d-175">To do so, your IoT solution needs to create a route and to set the Data Source equal to *DeviceLifecycleEvents*.</span></span> <span data-ttu-id="6a54d-176">Varsayılan olarak, hiçbir yaşam döngüsü bildirimleri gönderilir, diğer bir deyişle, bu tür bir yollar önceden mevcut.</span><span class="sxs-lookup"><span data-stu-id="6a54d-176">By default, no lifecycle notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="6a54d-177">Bildirim iletisi özelliklerini ve gövde içerir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-177">The notification message includes properties, and body.</span></span>

<span data-ttu-id="6a54d-178">Özellikler: İleti sistemi özellikleri ile önek `'$'` simgesi.</span><span class="sxs-lookup"><span data-stu-id="6a54d-178">Properties: Message system properties are prefixed with the `'$'` symbol.</span></span>

| <span data-ttu-id="6a54d-179">Ad</span><span class="sxs-lookup"><span data-stu-id="6a54d-179">Name</span></span> | <span data-ttu-id="6a54d-180">Değer</span><span class="sxs-lookup"><span data-stu-id="6a54d-180">Value</span></span> |
| --- | --- |
<span data-ttu-id="6a54d-181">$content-türü</span><span class="sxs-lookup"><span data-stu-id="6a54d-181">$content-type</span></span> | <span data-ttu-id="6a54d-182">uygulama/json</span><span class="sxs-lookup"><span data-stu-id="6a54d-182">application/json</span></span> |
<span data-ttu-id="6a54d-183">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="6a54d-183">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="6a54d-184">Zaman zaman bildirim gönderildi</span><span class="sxs-lookup"><span data-stu-id="6a54d-184">Time when the notification was sent</span></span> |
<span data-ttu-id="6a54d-185">$iothub-ileti-kaynak</span><span class="sxs-lookup"><span data-stu-id="6a54d-185">$iothub-message-source</span></span> | <span data-ttu-id="6a54d-186">deviceLifecycleEvents</span><span class="sxs-lookup"><span data-stu-id="6a54d-186">deviceLifecycleEvents</span></span> |
<span data-ttu-id="6a54d-187">$content-kodlama</span><span class="sxs-lookup"><span data-stu-id="6a54d-187">$content-encoding</span></span> | <span data-ttu-id="6a54d-188">UTF-8</span><span class="sxs-lookup"><span data-stu-id="6a54d-188">utf-8</span></span> |
<span data-ttu-id="6a54d-189">opType</span><span class="sxs-lookup"><span data-stu-id="6a54d-189">opType</span></span> | <span data-ttu-id="6a54d-190">**createDeviceIdentity** veya **deleteDeviceIdentity**</span><span class="sxs-lookup"><span data-stu-id="6a54d-190">**createDeviceIdentity** or **deleteDeviceIdentity**</span></span> |
<span data-ttu-id="6a54d-191">hubName</span><span class="sxs-lookup"><span data-stu-id="6a54d-191">hubName</span></span> | <span data-ttu-id="6a54d-192">IOT hub'ının adı</span><span class="sxs-lookup"><span data-stu-id="6a54d-192">Name of IoT Hub</span></span> |
<span data-ttu-id="6a54d-193">deviceId</span><span class="sxs-lookup"><span data-stu-id="6a54d-193">deviceId</span></span> | <span data-ttu-id="6a54d-194">Cihaz kimliği</span><span class="sxs-lookup"><span data-stu-id="6a54d-194">ID of the device</span></span> |
<span data-ttu-id="6a54d-195">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="6a54d-195">operationTimestamp</span></span> | <span data-ttu-id="6a54d-196">İşlemin ISO8601 zaman damgası</span><span class="sxs-lookup"><span data-stu-id="6a54d-196">ISO8601 timestamp of operation</span></span> |
<span data-ttu-id="6a54d-197">ıothub ileti şeması</span><span class="sxs-lookup"><span data-stu-id="6a54d-197">iothub-message-schema</span></span> | <span data-ttu-id="6a54d-198">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="6a54d-198">deviceLifecycleNotification</span></span> |

<span data-ttu-id="6a54d-199">Gövde: Bu bölümde, JSON biçiminde ve twin oluşturulan cihaz kimliğini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="6a54d-199">Body: This section is in JSON format and represents the twin of the created device identity.</span></span> <span data-ttu-id="6a54d-200">Örneğin,</span><span class="sxs-lookup"><span data-stu-id="6a54d-200">For example,</span></span>

```json
{
    "deviceId":"11576-ailn-test-0-67333793211",
    "etag":"AAAAAAAAAAE=",
    "properties": {
        "desired": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        },
        "reported": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        }
    }
}
```

## <a name="reference-topics"></a><span data-ttu-id="6a54d-201">Başvuru konuları:</span><span class="sxs-lookup"><span data-stu-id="6a54d-201">Reference topics:</span></span>

<span data-ttu-id="6a54d-202">Aşağıdaki başvuru konuları kimlik kayıt defteri hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="6a54d-202">The following reference topics provide you with more information about the identity registry.</span></span>

## <a name="device-identity-properties"></a><span data-ttu-id="6a54d-203">Cihaz kimlik özellikleri</span><span class="sxs-lookup"><span data-stu-id="6a54d-203">Device identity properties</span></span>

<span data-ttu-id="6a54d-204">Bir cihaz kimlikleri aşağıdaki özelliklerle JSON belgeleri olarak temsil edilir:</span><span class="sxs-lookup"><span data-stu-id="6a54d-204">Device identities are represented as JSON documents with the following properties:</span></span>

| <span data-ttu-id="6a54d-205">Özellik</span><span class="sxs-lookup"><span data-stu-id="6a54d-205">Property</span></span> | <span data-ttu-id="6a54d-206">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="6a54d-206">Options</span></span> | <span data-ttu-id="6a54d-207">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6a54d-207">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6a54d-208">deviceId</span><span class="sxs-lookup"><span data-stu-id="6a54d-208">deviceId</span></span> |<span data-ttu-id="6a54d-209">gerekli, güncelleştirmelerinin salt okunur</span><span class="sxs-lookup"><span data-stu-id="6a54d-209">required, read-only on updates</span></span> |<span data-ttu-id="6a54d-210">ASCII 7 bit alfasayısal karakterlerin büyük küçük harf duyarlı dize (en fazla 128 karakter uzunluğunda) + `{'-', ':', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`.</span><span class="sxs-lookup"><span data-stu-id="6a54d-210">A case-sensitive string (up to 128 characters long) of ASCII 7-bit alphanumeric characters + `{'-', ':', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`.</span></span> |
| <span data-ttu-id="6a54d-211">Generationıd</span><span class="sxs-lookup"><span data-stu-id="6a54d-211">generationId</span></span> |<span data-ttu-id="6a54d-212">gerekli, salt okunur</span><span class="sxs-lookup"><span data-stu-id="6a54d-212">required, read-only</span></span> |<span data-ttu-id="6a54d-213">Bir IOT hub tarafından üretilen, büyük küçük harf duyarlı dize en çok 128 karakter uzunluğunda.</span><span class="sxs-lookup"><span data-stu-id="6a54d-213">An IoT hub-generated, case-sensitive string up to 128 characters long.</span></span> <span data-ttu-id="6a54d-214">Bu değer ile aynı cihazları ayırt etmek için kullanılır **DeviceID**, silinmiş ve yeniden oluşturulacak.</span><span class="sxs-lookup"><span data-stu-id="6a54d-214">This value is used to distinguish devices with the same **deviceId**, when they have been deleted and re-created.</span></span> |
| <span data-ttu-id="6a54d-215">ETag</span><span class="sxs-lookup"><span data-stu-id="6a54d-215">etag</span></span> |<span data-ttu-id="6a54d-216">gerekli, salt okunur</span><span class="sxs-lookup"><span data-stu-id="6a54d-216">required, read-only</span></span> |<span data-ttu-id="6a54d-217">Göre zayıf bir ETag cihaz kimliğini temsil eden bir dize [RFC7232][lnk-rfc7232].</span><span class="sxs-lookup"><span data-stu-id="6a54d-217">A string representing a weak ETag for the device identity, as per [RFC7232][lnk-rfc7232].</span></span> |
| <span data-ttu-id="6a54d-218">kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="6a54d-218">auth</span></span> |<span data-ttu-id="6a54d-219">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="6a54d-219">optional</span></span> |<span data-ttu-id="6a54d-220">Kimlik doğrulama bilgileri ve güvenlik malzemeleri içeren bileşik bir nesne.</span><span class="sxs-lookup"><span data-stu-id="6a54d-220">A composite object containing authentication information and security materials.</span></span> |
| <span data-ttu-id="6a54d-221">auth.symkey</span><span class="sxs-lookup"><span data-stu-id="6a54d-221">auth.symkey</span></span> |<span data-ttu-id="6a54d-222">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="6a54d-222">optional</span></span> |<span data-ttu-id="6a54d-223">Base64 biçiminde depolanan birincil ve ikincil bir anahtar içeren bileşik bir nesne.</span><span class="sxs-lookup"><span data-stu-id="6a54d-223">A composite object containing a primary and a secondary key, stored in base64 format.</span></span> |
| <span data-ttu-id="6a54d-224">durum</span><span class="sxs-lookup"><span data-stu-id="6a54d-224">status</span></span> |<span data-ttu-id="6a54d-225">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6a54d-225">required</span></span> |<span data-ttu-id="6a54d-226">Bir erişim göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-226">An access indicator.</span></span> <span data-ttu-id="6a54d-227">Olabilir **etkin** veya **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="6a54d-227">Can be **Enabled** or **Disabled**.</span></span> <span data-ttu-id="6a54d-228">Varsa **etkin**, cihaz bağlanmasına izin verilir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-228">If **Enabled**, the device is allowed to connect.</span></span> <span data-ttu-id="6a54d-229">Varsa **devre dışı**, bu cihazı herhangi bir aygıt'e yönelik uç nokta erişemiyor.</span><span class="sxs-lookup"><span data-stu-id="6a54d-229">If **Disabled**, this device cannot access any device-facing endpoint.</span></span> |
| <span data-ttu-id="6a54d-230">statusReason</span><span class="sxs-lookup"><span data-stu-id="6a54d-230">statusReason</span></span> |<span data-ttu-id="6a54d-231">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="6a54d-231">optional</span></span> |<span data-ttu-id="6a54d-232">Cihaz kimliği durum nedeni depolayan bir 128 karakter uzunluğundaki dize.</span><span class="sxs-lookup"><span data-stu-id="6a54d-232">A 128 character-long string that stores the reason for the device identity status.</span></span> <span data-ttu-id="6a54d-233">Tüm UTF-8 karakterlere izin verilir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-233">All UTF-8 characters are allowed.</span></span> |
| <span data-ttu-id="6a54d-234">statusUpdateTime</span><span class="sxs-lookup"><span data-stu-id="6a54d-234">statusUpdateTime</span></span> |<span data-ttu-id="6a54d-235">Salt okunur</span><span class="sxs-lookup"><span data-stu-id="6a54d-235">read-only</span></span> |<span data-ttu-id="6a54d-236">Son durum güncelleştirmesi saat ve tarihi gösteren bir zamana bağlı göstergesi.</span><span class="sxs-lookup"><span data-stu-id="6a54d-236">A temporal indicator, showing the date and time of the last status update.</span></span> |
| <span data-ttu-id="6a54d-237">connectionState</span><span class="sxs-lookup"><span data-stu-id="6a54d-237">connectionState</span></span> |<span data-ttu-id="6a54d-238">Salt okunur</span><span class="sxs-lookup"><span data-stu-id="6a54d-238">read-only</span></span> |<span data-ttu-id="6a54d-239">Bağlantı durumunu gösteren bir alan: ya da **bağlı** veya **bağlantı kesildi**.</span><span class="sxs-lookup"><span data-stu-id="6a54d-239">A field indicating connection status: either **Connected** or **Disconnected**.</span></span> <span data-ttu-id="6a54d-240">Bu alan cihaz bağlantı durumunun IOT Hub görünümünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="6a54d-240">This field represents the IoT Hub view of the device connection status.</span></span> <span data-ttu-id="6a54d-241">**Önemli**: Bu alan yalnızca geliştirme/hata ayıklama amacıyla kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6a54d-241">**Important**: This field should be used only for development/debugging purposes.</span></span> <span data-ttu-id="6a54d-242">Bağlantı durumu yalnızca MQTT veya AMQP kullanarak aygıtlar için güncelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-242">The connection state is updated only for devices using MQTT or AMQP.</span></span> <span data-ttu-id="6a54d-243">Ayrıca, protokol düzeyi ping (ping MQTT veya AMQP ping) dayalıdır ve yalnızca 5 dakika cinsinden bir maksimum gecikme olabilir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-243">Also, it is based on protocol-level pings (MQTT pings, or AMQP pings), and it can have a maximum delay of only 5 minutes.</span></span> <span data-ttu-id="6a54d-244">Bu nedenlerle, olabilir hatalı pozitif sonuç gibi cihazlar bağlı olarak bildirilen ancak, kesilir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-244">For these reasons, there can be false positives, such as devices reported as connected but that are disconnected.</span></span> |
| <span data-ttu-id="6a54d-245">connectionStateUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="6a54d-245">connectionStateUpdatedTime</span></span> |<span data-ttu-id="6a54d-246">Salt okunur</span><span class="sxs-lookup"><span data-stu-id="6a54d-246">read-only</span></span> |<span data-ttu-id="6a54d-247">Son saat ve tarihi bağlantı durumunu gösteren bir zamana bağlı göstergesi güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="6a54d-247">A temporal indicator, showing the date and last time the connection state was updated.</span></span> |
| <span data-ttu-id="6a54d-248">lastActivityTime</span><span class="sxs-lookup"><span data-stu-id="6a54d-248">lastActivityTime</span></span> |<span data-ttu-id="6a54d-249">Salt okunur</span><span class="sxs-lookup"><span data-stu-id="6a54d-249">read-only</span></span> |<span data-ttu-id="6a54d-250">Zamana bağlı bir gösterge son saat ve tarihi cihazı gösteren, bağlı, alınan veya gönderilen bir ileti.</span><span class="sxs-lookup"><span data-stu-id="6a54d-250">A temporal indicator, showing the date and last time the device connected, received, or sent a message.</span></span> |

> [!NOTE]
> <span data-ttu-id="6a54d-251">Bağlantı durumu yalnızca bağlantı durumunun IOT Hub görünümünü temsil edebilir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-251">Connection state can only represent the IoT Hub view of the status of the connection.</span></span> <span data-ttu-id="6a54d-252">Ağ koşulları ve yapılandırmaları bağlı olarak bu durum güncelleştirmeleri gecikebilir.</span><span class="sxs-lookup"><span data-stu-id="6a54d-252">Updates to this state may be delayed, depending on network conditions and configurations.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="6a54d-253">Ek başvuru bilgileri</span><span class="sxs-lookup"><span data-stu-id="6a54d-253">Additional reference material</span></span>

<span data-ttu-id="6a54d-254">IOT Hub Geliştirici Kılavuzu'ndaki diğer başvuru konuları içerir:</span><span class="sxs-lookup"><span data-stu-id="6a54d-254">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="6a54d-255">[IOT Hub uç noktaları] [ lnk-endpoints] her IOT hub'ı çalışma zamanı ve yönetim işlemleri için kullanıma sunan çeşitli uç noktaları açıklar.</span><span class="sxs-lookup"><span data-stu-id="6a54d-255">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="6a54d-256">[Azaltma ve kotaları] [ lnk-quotas] kotaları açıklar ve IOT hub'ı hizmete uygulamak davranışları azaltma.</span><span class="sxs-lookup"><span data-stu-id="6a54d-256">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="6a54d-257">[Azure IOT cihaz ve hizmet SDK'ları] [ lnk-sdks] çeşitli dil IOT Hub ile etkileşim hem cihaz hem de hizmet uygulamaları geliştirirken kullanabilir SDK'ları listeler.</span><span class="sxs-lookup"><span data-stu-id="6a54d-257">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="6a54d-258">[IOT hub'ı sorgu dili] [ lnk-query] IOT Hub'ından, cihaz çiftlerini ve işleri hakkında bilgi almak için kullanabileceğiniz sorgu dili açıklar.</span><span class="sxs-lookup"><span data-stu-id="6a54d-258">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="6a54d-259">[IOT Hub MQTT Destek] [ lnk-devguide-mqtt] IOT hub'ı desteği hakkında daha fazla bilgi için MQTT Protokolü sağlar.</span><span class="sxs-lookup"><span data-stu-id="6a54d-259">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a54d-260">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6a54d-260">Next steps</span></span>

<span data-ttu-id="6a54d-261">IOT Hub kimlik kayıt defteri kullanmayı öğrendiniz artık aşağıdaki IOT Hub Geliştirici Kılavuzu konuları ilgilenen olabilir:</span><span class="sxs-lookup"><span data-stu-id="6a54d-261">Now you have learned how to use the IoT Hub identity registry, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="6a54d-262">[IOT Hub'ına erişimi denetleme][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="6a54d-262">[Control access to IoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="6a54d-263">[Cihaz çiftlerini durumu ve yapılandırmaları eşitlemek için kullanın][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="6a54d-263">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="6a54d-264">[Bir cihazda doğrudan bir yöntem çağırma][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="6a54d-264">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="6a54d-265">[Birden çok aygıta işleri zamanla][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="6a54d-265">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="6a54d-266">Bu makalede açıklanan kavramları bazıları denemek istiyorsanız, aşağıdaki IOT hub'ı öğreticide ilgilenen olabilir:</span><span class="sxs-lookup"><span data-stu-id="6a54d-266">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="6a54d-267">[Azure IOT Hub ile çalışmaya başlama][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="6a54d-267">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>

<!-- Links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-guidance-provisioning]: iot-hub-devguide-identity-registry.md#device-provisioning
[lnk-guidance-heartbeat]: iot-hub-devguide-identity-registry.md#device-heartbeat
[lnk-rfc7232]: https://tools.ietf.org/html/rfc7232
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-export]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-devguide-opmon]: iot-hub-operations-monitoring.md

[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
