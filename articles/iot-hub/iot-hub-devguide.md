---
title: "Azure IOT Hub Geliştirici Kılavuzu | Microsoft Docs"
description: "Azure IOT Hub Geliştirici Kılavuzu uç noktaları, güvenlik, kimlik kayıt defteri, cihaz yönetimi, doğrudan yöntemleri, cihaz çiftlerini, dosya yüklemeleri, işleri, IOT hub'ı sorgu dili tartışmalarını içerir ve mesajlaşma."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: d534ff9d-2de5-4995-bb2d-84a02693cb2e
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: adb9a12899e9040cd83d522c734448989636fe29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-hub-developer-guide"></a><span data-ttu-id="6ca99-103">Azure IOT Hub Geliştirici Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="6ca99-103">Azure IoT Hub developer guide</span></span>

<span data-ttu-id="6ca99-104">Azure IOT Hub, milyonlarca cihaza arasında güvenilir ve güvenli çift yönlü iletişimler sağlayan tam olarak yönetilen hizmet etkinleştirin ve bir çözüm arka ucu ' dir.</span><span class="sxs-lookup"><span data-stu-id="6ca99-104">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span>

<span data-ttu-id="6ca99-105">Azure IOT Hub ile sağlar:</span><span class="sxs-lookup"><span data-stu-id="6ca99-105">Azure IoT Hub provides you with:</span></span>

* <span data-ttu-id="6ca99-106">Cihaz başına güvenlik kimlik bilgileri kullanılarak güvenli iletişim ve erişim denetimi.</span><span class="sxs-lookup"><span data-stu-id="6ca99-106">Secure communications by using per-device security credentials and access control.</span></span>
* <span data-ttu-id="6ca99-107">Birden çok cihaz Bulut ve bulut-cihaz hiper ölçekli iletişim seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="6ca99-107">Multiple device-to-cloud and cloud-to-device hyper-scale communication options.</span></span>
* <span data-ttu-id="6ca99-108">Sorgulanabilir depolama aygıt başına durum bilgilerini ve meta verileri.</span><span class="sxs-lookup"><span data-stu-id="6ca99-108">Queryable storage of per-device state information and meta-data.</span></span>
* <span data-ttu-id="6ca99-109">En popüler diller ve platformlar için cihaz kitaplıklarını ile kolay cihaz bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="6ca99-109">Easy device connectivity with device libraries for the most popular languages and platforms.</span></span>

<span data-ttu-id="6ca99-110">Bu IOT Hub Geliştirici Kılavuzu, aşağıdaki makaleler içerir:</span><span class="sxs-lookup"><span data-stu-id="6ca99-110">This IoT Hub developer guide includes the following articles:</span></span>

* <span data-ttu-id="6ca99-111">[Cihaz bulut iletişimi Kılavuzu] [ lnk-d2c-guidance] cihaz bulut iletilerini, cihaz çifti'nın bildirilen özellikleri ve karşıya dosya yükleme arasında seçtiğiniz yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="6ca99-111">[Device-to-cloud communication guidance][lnk-d2c-guidance] helps you choose between device-to-cloud messages, device twin's reported properties, and file upload.</span></span>
* <span data-ttu-id="6ca99-112">[Bulut-cihaz iletişimi Kılavuzu] [ lnk-c2d-guidance] doğrudan yöntemleri, cihaz çifti'nın istenen özellikleri ve bulut-cihaz iletilerini arasında seçtiğiniz yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="6ca99-112">[Cloud-to-device communication guidance][lnk-c2d-guidance] helps you choose between direct methods, device twin's desired properties, and cloud-to-device messages.</span></span>
* <span data-ttu-id="6ca99-113">[Cihaz Bulut ve bulut cihaz IOT Hub ile Mesajlaşma] [ devguide-messaging] IOT hub'ı sunan Mesajlaşma özellikleri (cihaz Bulut ve bulut-cihaz) açıklar.</span><span class="sxs-lookup"><span data-stu-id="6ca99-113">[Device-to-cloud and cloud-to-device messaging with IoT Hub][devguide-messaging] describes the messaging features (device-to-cloud and cloud-to-device) that IoT Hub exposes.</span></span>
  * <span data-ttu-id="6ca99-114">[IOT Hub cihaz bulut iletilerini göndermek][devguide-messages-d2c].</span><span class="sxs-lookup"><span data-stu-id="6ca99-114">[Send device-to-cloud messages to IoT Hub][devguide-messages-d2c].</span></span>
  * <span data-ttu-id="6ca99-115">[Yerleşik uç noktasından cihaz bulut iletilerini okumanızı][devguide-builtin].</span><span class="sxs-lookup"><span data-stu-id="6ca99-115">[Read device-to-cloud messages from the built-in endpoint][devguide-builtin].</span></span>
  * <span data-ttu-id="6ca99-116">[Özel uç noktaları ve yönlendirme kuralları için cihaz bulut iletilerini kullanmak][devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="6ca99-116">[Use custom endpoints and routing rules for device-to-cloud messages][devguide-custom].</span></span>
  * <span data-ttu-id="6ca99-117">[IOT Hub'ından bulut-cihaz iletilerini göndermek][devguide-messages-c2d].</span><span class="sxs-lookup"><span data-stu-id="6ca99-117">[Send cloud-to-device messages from IoT Hub][devguide-messages-c2d].</span></span>
  * <span data-ttu-id="6ca99-118">[Oluşturun ve IOT hub'ı iletileri okumak][devguide-format].</span><span class="sxs-lookup"><span data-stu-id="6ca99-118">[Create and read IoT Hub messages][devguide-format].</span></span>
* <span data-ttu-id="6ca99-119">[Bir CİHAZDAN dosyaları karşıya yükleme] [ devguide-upload] aygıttan dosyaları karşıya nasıl yükleneceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="6ca99-119">[Upload files from a device][devguide-upload] describes how you can upload files from a device.</span></span> <span data-ttu-id="6ca99-120">Makale ayrıca karşıya yükleme işlemi gönderebilirsiniz bildirimleri gibi konular hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="6ca99-120">The article also includes information about topics such as the notifications the upload process can send.</span></span>
* <span data-ttu-id="6ca99-121">[IOT Hub cihaz kimliklerini yönetmek] [ devguide-identities] hangi bilgilerin açıklar her IOT hub'ın kimlik kayıt defteri depolarına ve nasıl erişmek ve değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ca99-121">[Manage device identities in IoT Hub][devguide-identities] describes what information each IoT hub's identity registry stores, and how you can access and modify it.</span></span>
* <span data-ttu-id="6ca99-122">[IOT Hub'ına erişim denetim] [ devguide-security] hem de IOT hub'ı işlevselliği erişim ve bileşenleri bulut için kullanılan güvenlik modeli açıklanır.</span><span class="sxs-lookup"><span data-stu-id="6ca99-122">[Control access to IoT Hub][devguide-security] describes the security model used to grant access to IoT Hub functionality for both devices and cloud components.</span></span> <span data-ttu-id="6ca99-123">Makaleyi belirteçleri ve X.509 sertifikalarını ve erişim izni verebilir izinleri ayrıntılarını kullanma hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="6ca99-123">The article includes information about using tokens and X.509 certificates, and details of the permissions you can grant.</span></span>
* <span data-ttu-id="6ca99-124">[Durum ve yapılandırmaları eşitlemek için cihaz çiftlerini kullanmak] [ devguide-device-twins] açıklar *cihaz çifti* kavram ve kullanıma sunan bir aygıt, cihaz çifti ile eşitleme gibi işlevselliği.</span><span class="sxs-lookup"><span data-stu-id="6ca99-124">[Use device twins to synchronize state and configurations][devguide-device-twins] describes the *device twin* concept and the functionality it exposes such as synchronizing a device with its device twin.</span></span> <span data-ttu-id="6ca99-125">Makale bir cihaz çiftine depolanan verileri hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="6ca99-125">The article includes information about the data stored in a device twin.</span></span>
* <span data-ttu-id="6ca99-126">[Bir cihazda doğrudan bir yöntem çağırma] [ devguide-directmethods] doğrudan bir yöntem, arka uç uygulama cihaza yöntemleri çağırma ve Cihazınızda doğrudan yöntemi işlemek hakkında bilgi yaşam döngüsü açıklar.</span><span class="sxs-lookup"><span data-stu-id="6ca99-126">[Invoke a direct method on a device][devguide-directmethods] describes the lifecycle of a direct method, information about how to invoke methods on a device from your back-end app and handle the direct method on your device.</span></span>
* <span data-ttu-id="6ca99-127">[Zamanlama işlerini birden çok aygıta] [ devguide-jobs] işleri birden çok aygıta nasıl zamanlayabilirsiniz açıklar.</span><span class="sxs-lookup"><span data-stu-id="6ca99-127">[Schedule jobs on multiple devices][devguide-jobs] describes how you can schedule jobs on multiple devices.</span></span> <span data-ttu-id="6ca99-128">Makale olarak cihaz çiftine kullanarak bir cihazı güncelleştirme doğrudan bir yöntem yürütülen görevleri gerçekleştiren iş göndermek açıklar.</span><span class="sxs-lookup"><span data-stu-id="6ca99-128">The article describes how to submit jobs that perform tasks as executing a direct method, updating a device using a device twin.</span></span> <span data-ttu-id="6ca99-129">Ayrıca, bir işin durumunu sorgulamak nasıl açıklanır.</span><span class="sxs-lookup"><span data-stu-id="6ca99-129">It also describes how to query the status of a job.</span></span>
* <span data-ttu-id="6ca99-130">[Başvuru - iletişim protokolü seçin] [ devguide-protocol] IOT Hub cihaz iletişimi destekler ve açık olması gereken bağlantı noktalarını listeler iletişim protokolleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="6ca99-130">[Reference - choose a communication protocol][devguide-protocol] describes the communication protocols that IoT Hub supports for device communication and lists the ports that should be open.</span></span>
* <span data-ttu-id="6ca99-131">[Başvuru - IOT Hub uç noktaları] [ devguide-endpoints] her IOT hub'ı çalışma zamanı ve yönetim işlemleri için kullanıma sunan çeşitli uç noktaları açıklar.</span><span class="sxs-lookup"><span data-stu-id="6ca99-131">[Reference - IoT Hub endpoints][devguide-endpoints] describes the various endpoints that each IoT hub exposes for runtime and management operations.</span></span> <span data-ttu-id="6ca99-132">Makalede ayrıca, IOT hub'ınıza ek uç noktaları nasıl oluşturabileceğinizi ve bir alan ağ geçidi, IOT Hub uç noktaları standart senaryolarda aygıtları bağlantıyı etkinleştirmek için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6ca99-132">The article also describes how you can create additional endpoints in your IoT hub, and how to use a field gateway to enable devices connectivity to your IoT Hub endpoints in non-standard scenarios.</span></span>
* <span data-ttu-id="6ca99-133">[Başvuru - cihaz çiftlerini, işler ve ileti yönlendirme için IOT hub'ı sorgu dili] [ devguide-query] hub'ınızın cihaz çiftlerini ve işleri hakkında bilgi almak sağlar, IOT hub'ı sorgu dili açıklar.</span><span class="sxs-lookup"><span data-stu-id="6ca99-133">[Reference - IoT Hub query language for device twins, jobs, and message routing][devguide-query] describes that IoT Hub query language that enables you to retrieve information from your hub about your device twins and jobs.</span></span>
* <span data-ttu-id="6ca99-134">[Başvuru - kotalar ve azaltma] [ devguide-quotas] IOT Hub hizmeti ve ne zaman bir kotanın aşılmasına görmeyi beklediğiniz azaltma davranışını ayarlama kotaları özetler.</span><span class="sxs-lookup"><span data-stu-id="6ca99-134">[Reference - quotas and throttling][devguide-quotas] summarizes the quotas set in the IoT Hub service and the throttling behavior you can expect to see when you exceed a quota.</span></span>
* <span data-ttu-id="6ca99-135">[Başvuru - fiyatlandırma] [ devguide-pricing] farklı SKU'ları ve IOT Hub ve nasıl çeşitli IOT hub'ı işlevler iletileri olarak IOT Hub tarafından ölçülen ile ilgili ayrıntılar için fiyatlandırma hakkında genel bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ca99-135">[Reference - pricing][devguide-pricing] provides general information on different SKUs and pricing for IoT Hub and details on how the various IoT Hub functionalities are metered as messages by IoT Hub.</span></span>
* <span data-ttu-id="6ca99-136">[Başvuru - cihazını ve hizmetini SDK'ları] [ devguide-sdks] IOT hub'ınıza etkileşim hem cihaz hem de hizmet uygulamaları geliştirmek için kullanabileceğiniz Azure IOT SDK'ları listeler.</span><span class="sxs-lookup"><span data-stu-id="6ca99-136">[Reference - Device and service SDKs][devguide-sdks] lists the Azure IoT SDKs you can use to develop both device and service apps that interact with your IoT hub.</span></span> <span data-ttu-id="6ca99-137">Makaleyi çevrimiçi API belgeleri bağlantılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="6ca99-137">The article includes links to online API documentation.</span></span>
* <span data-ttu-id="6ca99-138">[Başvuru - IOT Hub MQTT Destek] [ devguide-mqtt] MQTT Protokolü IOT hub'ı nasıl desteklediği hakkında ayrıntılı bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ca99-138">[Reference - IoT Hub MQTT support][devguide-mqtt] provides detailed information about how IoT Hub supports the MQTT protocol.</span></span> <span data-ttu-id="6ca99-139">Makale için Azure IOT SDK'ları yerleşik MQTT protokolü desteği açıklar ve MQTT protokolü kullanarak doğrudan hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ca99-139">The article describes the support for the MQTT protocol built-in to the Azure IoT SDKs and provides information about using the MQTT protocol directly.</span></span>
* <span data-ttu-id="6ca99-140">[Sözlük] [ devguide-glossary] ortak IOT Hub ile ilgili terimlerin bir listesi.</span><span class="sxs-lookup"><span data-stu-id="6ca99-140">[Glossary][devguide-glossary] a list of common IoT Hub-related terms.</span></span>

[devguide-messaging]: iot-hub-devguide-messaging.md
[devguide-upload]: iot-hub-devguide-file-upload.md
[devguide-identities]: iot-hub-devguide-identity-registry.md
[devguide-security]: iot-hub-devguide-security.md
[devguide-device-twins]: iot-hub-devguide-device-twins.md
[devguide-directmethods]: iot-hub-devguide-direct-methods.md
[devguide-jobs]: iot-hub-devguide-jobs.md
[devguide-endpoints]: iot-hub-devguide-endpoints.md
[devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[devguide-query]: iot-hub-devguide-query-language.md
[devguide-sdks]: iot-hub-devguide-sdks.md
[devguide-mqtt]: iot-hub-mqtt-support.md
[devguide-glossary]: iot-hub-devguide-glossary.md
[devguide-pricing]: iot-hub-devguide-pricing.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[devguide-messages-d2c]: iot-hub-devguide-messages-d2c.md
[devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[devguide-custom]: iot-hub-devguide-messages-read-custom.md
[devguide-messages-c2d]: iot-hub-devguide-messages-c2d.md
[devguide-format]: iot-hub-devguide-messages-construct.md
[devguide-protocol]: iot-hub-devguide-protocols.md
