---
title: "Azure IOT Hub için aaaDeveloper Kılavuzu | Microsoft Docs"
description: "Hello Azure IOT Hub Geliştirici Kılavuzu uç noktaları, güvenlik, hello kimlik kayıt defteri, cihaz yönetimi, doğrudan yöntemleri, cihaz çiftlerini, dosya yüklemeleri, işleri, hello IOT hub'ı sorgu dili ve mesajlaşma tartışmalarını içerir."
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
ms.openlocfilehash: 2d3f18399e4cef6f9c4850a5caeb170a2d091a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-developer-guide"></a><span data-ttu-id="a5e48-103">Azure IOT Hub Geliştirici Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="a5e48-103">Azure IoT Hub developer guide</span></span>

<span data-ttu-id="a5e48-104">Azure IOT Hub, milyonlarca cihaza arasında güvenilir ve güvenli çift yönlü iletişimler sağlayan tam olarak yönetilen hizmet etkinleştirin ve bir çözüm arka ucu ' dir.</span><span class="sxs-lookup"><span data-stu-id="a5e48-104">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span>

<span data-ttu-id="a5e48-105">Azure IOT Hub ile sağlar:</span><span class="sxs-lookup"><span data-stu-id="a5e48-105">Azure IoT Hub provides you with:</span></span>

* <span data-ttu-id="a5e48-106">Cihaz başına güvenlik kimlik bilgileri kullanılarak güvenli iletişim ve erişim denetimi.</span><span class="sxs-lookup"><span data-stu-id="a5e48-106">Secure communications by using per-device security credentials and access control.</span></span>
* <span data-ttu-id="a5e48-107">Birden çok cihaz Bulut ve bulut-cihaz hiper ölçekli iletişim seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="a5e48-107">Multiple device-to-cloud and cloud-to-device hyper-scale communication options.</span></span>
* <span data-ttu-id="a5e48-108">Sorgulanabilir depolama aygıt başına durum bilgilerini ve meta verileri.</span><span class="sxs-lookup"><span data-stu-id="a5e48-108">Queryable storage of per-device state information and meta-data.</span></span>
* <span data-ttu-id="a5e48-109">Merhaba en popüler diller ve platformlar için cihaz kitaplıklarını ile kolay cihaz bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="a5e48-109">Easy device connectivity with device libraries for hello most popular languages and platforms.</span></span>

<span data-ttu-id="a5e48-110">Bu IOT Hub geliştirici kılavuzu makaleleri aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="a5e48-110">This IoT Hub developer guide includes hello following articles:</span></span>

* <span data-ttu-id="a5e48-111">[Cihaz bulut iletişimi Kılavuzu] [ lnk-d2c-guidance] cihaz bulut iletilerini, cihaz çifti'nın bildirilen özellikleri ve karşıya dosya yükleme arasında seçtiğiniz yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a5e48-111">[Device-to-cloud communication guidance][lnk-d2c-guidance] helps you choose between device-to-cloud messages, device twin's reported properties, and file upload.</span></span>
* <span data-ttu-id="a5e48-112">[Bulut-cihaz iletişimi Kılavuzu] [ lnk-c2d-guidance] doğrudan yöntemleri, cihaz çifti'nın istenen özellikleri ve bulut-cihaz iletilerini arasında seçtiğiniz yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a5e48-112">[Cloud-to-device communication guidance][lnk-c2d-guidance] helps you choose between direct methods, device twin's desired properties, and cloud-to-device messages.</span></span>
* <span data-ttu-id="a5e48-113">[Cihaz Bulut ve bulut cihaz IOT Hub ile Mesajlaşma] [ devguide-messaging] IOT hub'ı gösteren hello Mesajlaşma özellikleri (cihaz Bulut ve bulut-cihaz) açıklar.</span><span class="sxs-lookup"><span data-stu-id="a5e48-113">[Device-to-cloud and cloud-to-device messaging with IoT Hub][devguide-messaging] describes hello messaging features (device-to-cloud and cloud-to-device) that IoT Hub exposes.</span></span>
  * <span data-ttu-id="a5e48-114">[Cihaz bulut iletilerini tooIoT Hub Gönder][devguide-messages-d2c].</span><span class="sxs-lookup"><span data-stu-id="a5e48-114">[Send device-to-cloud messages tooIoT Hub][devguide-messages-d2c].</span></span>
  * <span data-ttu-id="a5e48-115">[Merhaba yerleşik uç noktasından cihaz bulut iletilerini okumanızı][devguide-builtin].</span><span class="sxs-lookup"><span data-stu-id="a5e48-115">[Read device-to-cloud messages from hello built-in endpoint][devguide-builtin].</span></span>
  * <span data-ttu-id="a5e48-116">[Özel uç noktaları ve yönlendirme kuralları için cihaz bulut iletilerini kullanmak][devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="a5e48-116">[Use custom endpoints and routing rules for device-to-cloud messages][devguide-custom].</span></span>
  * <span data-ttu-id="a5e48-117">[IOT Hub'ından bulut-cihaz iletilerini göndermek][devguide-messages-c2d].</span><span class="sxs-lookup"><span data-stu-id="a5e48-117">[Send cloud-to-device messages from IoT Hub][devguide-messages-c2d].</span></span>
  * <span data-ttu-id="a5e48-118">[Oluşturun ve IOT hub'ı iletileri okumak][devguide-format].</span><span class="sxs-lookup"><span data-stu-id="a5e48-118">[Create and read IoT Hub messages][devguide-format].</span></span>
* <span data-ttu-id="a5e48-119">[Bir CİHAZDAN dosyaları karşıya yükleme] [ devguide-upload] aygıttan dosyaları karşıya nasıl yükleneceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="a5e48-119">[Upload files from a device][devguide-upload] describes how you can upload files from a device.</span></span> <span data-ttu-id="a5e48-120">Merhaba makale ayrıca bildirimleri hello karşıya yükleme işlemi gönderebilir hello gibi konular hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="a5e48-120">hello article also includes information about topics such as hello notifications hello upload process can send.</span></span>
* <span data-ttu-id="a5e48-121">[IOT Hub cihaz kimliklerini yönetmek] [ devguide-identities] hangi bilgilerin açıklar her IOT hub'ın kimlik kayıt defteri depolarına ve nasıl erişmek ve değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5e48-121">[Manage device identities in IoT Hub][devguide-identities] describes what information each IoT hub's identity registry stores, and how you can access and modify it.</span></span>
* <span data-ttu-id="a5e48-122">[Erişim tooIoT Hub kontrol] [ devguide-security] hello güvenlik modeli kullanılan toogrant erişim tooIoT Hub işlevselliği cihazlar ve bulut bileşenleri için açıklar.</span><span class="sxs-lookup"><span data-stu-id="a5e48-122">[Control access tooIoT Hub][devguide-security] describes hello security model used toogrant access tooIoT Hub functionality for both devices and cloud components.</span></span> <span data-ttu-id="a5e48-123">Merhaba makale belirteçleri ve X.509 sertifikalarını ve erişim izni verebilir hello izinleri ayrıntılarını kullanma hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="a5e48-123">hello article includes information about using tokens and X.509 certificates, and details of hello permissions you can grant.</span></span>
* <span data-ttu-id="a5e48-124">[Cihaz çiftlerini toosynchronize durumu ve yapılandırmaları kullanma] [ devguide-device-twins] hello açıklar *cihaz çifti* kullanıma sunan bir aygıt, aygıtla eşitleme gibi kavram ve hello işlevi çifti.</span><span class="sxs-lookup"><span data-stu-id="a5e48-124">[Use device twins toosynchronize state and configurations][devguide-device-twins] describes hello *device twin* concept and hello functionality it exposes such as synchronizing a device with its device twin.</span></span> <span data-ttu-id="a5e48-125">Merhaba makale bir cihaz çiftine depolanır hello verileri hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="a5e48-125">hello article includes information about hello data stored in a device twin.</span></span>
* <span data-ttu-id="a5e48-126">[Bir cihazda doğrudan bir yöntem çağırma] [ devguide-directmethods] hello yaşam döngüsünü nasıl tooinvoke yöntemleri arka uç uygulama ve tanıtıcı hello cihaza yöntemi aygıtınızda doğrudan hakkında bilgi doğrudan bir yöntem açıklar.</span><span class="sxs-lookup"><span data-stu-id="a5e48-126">[Invoke a direct method on a device][devguide-directmethods] describes hello lifecycle of a direct method, information about how tooinvoke methods on a device from your back-end app and handle hello direct method on your device.</span></span>
* <span data-ttu-id="a5e48-127">[Zamanlama işlerini birden çok aygıta] [ devguide-jobs] işleri birden çok aygıta nasıl zamanlayabilirsiniz açıklar.</span><span class="sxs-lookup"><span data-stu-id="a5e48-127">[Schedule jobs on multiple devices][devguide-jobs] describes how you can schedule jobs on multiple devices.</span></span> <span data-ttu-id="a5e48-128">Merhaba nasıl toosubmit işlerin makalede cihaz çifti kullanarak bir cihazı güncelleştirme doğrudan bir yöntem yürütülen görevleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="a5e48-128">hello article describes how toosubmit jobs that perform tasks as executing a direct method, updating a device using a device twin.</span></span> <span data-ttu-id="a5e48-129">Ayrıca, nasıl tooquery hello işin durumunu açıklar.</span><span class="sxs-lookup"><span data-stu-id="a5e48-129">It also describes how tooquery hello status of a job.</span></span>
* <span data-ttu-id="a5e48-130">[Başvuru - iletişim protokolü seçin] [ devguide-protocol] IOT Hub cihaz iletişimi için destekler ve listeleri hello açık olması gereken bağlantı noktalarını hello iletişim protokolleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="a5e48-130">[Reference - choose a communication protocol][devguide-protocol] describes hello communication protocols that IoT Hub supports for device communication and lists hello ports that should be open.</span></span>
* <span data-ttu-id="a5e48-131">[Başvuru - IOT Hub uç noktaları] [ devguide-endpoints] açıklar çalışma zamanı ve yönetim işlemleri için her IOT hub'ı sunan çeşitli uç noktaları hello.</span><span class="sxs-lookup"><span data-stu-id="a5e48-131">[Reference - IoT Hub endpoints][devguide-endpoints] describes hello various endpoints that each IoT hub exposes for runtime and management operations.</span></span> <span data-ttu-id="a5e48-132">Merhaba ayrıca makalede IOT hub'ınıza ek uç noktaları oluşturabilirsiniz nasıl ve nasıl toouse bir alan ağ geçidi tooenable aygıtları bağlantı tooyour IOT Hub uç noktaları standart senaryolarda.</span><span class="sxs-lookup"><span data-stu-id="a5e48-132">hello article also describes how you can create additional endpoints in your IoT hub, and how toouse a field gateway tooenable devices connectivity tooyour IoT Hub endpoints in non-standard scenarios.</span></span>
* <span data-ttu-id="a5e48-133">[Başvuru - cihaz çiftlerini, işler ve ileti yönlendirme için IOT hub'ı sorgu dili] [ devguide-query] hub'ınızın cihaz çiftlerini ve işleri hakkında tooretrieve bilgileri sağlayan bu IOT hub'ı sorgu dili açıklar.</span><span class="sxs-lookup"><span data-stu-id="a5e48-133">[Reference - IoT Hub query language for device twins, jobs, and message routing][devguide-query] describes that IoT Hub query language that enables you tooretrieve information from your hub about your device twins and jobs.</span></span>
* <span data-ttu-id="a5e48-134">[Başvuru - kotalar ve azaltma] [ devguide-quotas] hello IOT Hub hizmeti ve davranış almanız olasıdır toosee kota aştıklarında azaltma hello ayarlamak hello kotaları özetler.</span><span class="sxs-lookup"><span data-stu-id="a5e48-134">[Reference - quotas and throttling][devguide-quotas] summarizes hello quotas set in hello IoT Hub service and hello throttling behavior you can expect toosee when you exceed a quota.</span></span>
* <span data-ttu-id="a5e48-135">[Başvuru - fiyatlandırma] [ devguide-pricing] farklı SKU'ları ve IOT hub'ı ve IOT Hub tarafından nasıl çeşitli IOT hub'ı işlevler olarak ölçülen hello iletileri ile ilgili ayrıntılar için fiyatlandırma hakkında genel bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="a5e48-135">[Reference - pricing][devguide-pricing] provides general information on different SKUs and pricing for IoT Hub and details on how hello various IoT Hub functionalities are metered as messages by IoT Hub.</span></span>
* <span data-ttu-id="a5e48-136">[Başvuru - cihazını ve hizmetini SDK'ları] [ devguide-sdks] listeleri hello Azure IOT SDK'ları toodevelop kullanabilirsiniz, IOT hub ile etkileşim hem cihaz hem de hizmet uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="a5e48-136">[Reference - Device and service SDKs][devguide-sdks] lists hello Azure IoT SDKs you can use toodevelop both device and service apps that interact with your IoT hub.</span></span> <span data-ttu-id="a5e48-137">Merhaba makale bağlantılar tooonline API belgelerine içerir.</span><span class="sxs-lookup"><span data-stu-id="a5e48-137">hello article includes links tooonline API documentation.</span></span>
* <span data-ttu-id="a5e48-138">[Başvuru - IOT Hub MQTT Destek] [ devguide-mqtt] hello MQTT Protokolü IOT hub'ı nasıl desteklediği hakkında ayrıntılı bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="a5e48-138">[Reference - IoT Hub MQTT support][devguide-mqtt] provides detailed information about how IoT Hub supports hello MQTT protocol.</span></span> <span data-ttu-id="a5e48-139">Merhaba makale hello MQTT Protokolü yerleşik toohello Azure IOT SDK'ları hello desteğini açıklar ve hello MQTT protokolü kullanarak doğrudan hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a5e48-139">hello article describes hello support for hello MQTT protocol built-in toohello Azure IoT SDKs and provides information about using hello MQTT protocol directly.</span></span>
* <span data-ttu-id="a5e48-140">[Sözlük] [ devguide-glossary] ortak IOT Hub ile ilgili terimlerin bir listesi.</span><span class="sxs-lookup"><span data-stu-id="a5e48-140">[Glossary][devguide-glossary] a list of common IoT Hub-related terms.</span></span>

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
