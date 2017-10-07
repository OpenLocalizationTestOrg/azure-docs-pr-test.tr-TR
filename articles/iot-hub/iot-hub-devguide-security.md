---
title: "Azure IOT Hub güvenlik aaaUnderstand | Microsoft Docs"
description: "Geliştirici Kılavuzu - nasıl toocontrol erişim tooIoT Hub cihaz uygulamaları ve arka uç uygulamalar için. Güvenlik belirteçleri ve X.509 sertifikalarını desteği hakkında bilgiler içerir."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 45631e70-865b-4e06-bb1d-aae1175a52ba
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 717726328a6bb5c5c334a123d0abfed711b2c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="control-access-tooiot-hub"></a><span data-ttu-id="ccd36-104">Denetim erişim tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="ccd36-104">Control access tooIoT Hub</span></span>

<span data-ttu-id="ccd36-105">Bu makalede, IOT hub'ınızı güvenliğini sağlamaya yönelik hello seçenekleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-105">This article describes hello options for securing your IoT hub.</span></span> <span data-ttu-id="ccd36-106">IOT hub'ı kullanan *izinleri* toogrant erişim tooeach IOT hub uç.</span><span class="sxs-lookup"><span data-stu-id="ccd36-106">IoT Hub uses *permissions* toogrant access tooeach IoT hub endpoint.</span></span> <span data-ttu-id="ccd36-107">İzinleri hello erişim tooan IOT hub işlevselliğine bağlı sınırlayın.</span><span class="sxs-lookup"><span data-stu-id="ccd36-107">Permissions limit hello access tooan IoT hub based on functionality.</span></span>

<span data-ttu-id="ccd36-108">Bu makalede açıklanır:</span><span class="sxs-lookup"><span data-stu-id="ccd36-108">This article describes:</span></span>

* <span data-ttu-id="ccd36-109">Merhaba farklı izinler IOT hub'ınızı tooa aygıt veya arka uç uygulama tooaccess verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd36-109">hello different permissions that you can grant tooa device or back-end app tooaccess your IoT hub.</span></span>
* <span data-ttu-id="ccd36-110">tooverify izinleri kullanan kimlik doğrulama işlemi ve hello belirteçleri hello.</span><span class="sxs-lookup"><span data-stu-id="ccd36-110">hello authentication process and hello tokens it uses tooverify permissions.</span></span>
* <span data-ttu-id="ccd36-111">Nasıl tooscope toolimit toospecific kaynaklarına erişim kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ccd36-111">How tooscope credentials toolimit access toospecific resources.</span></span>
* <span data-ttu-id="ccd36-112">X.509 sertifikaları IOT hub'ı destekler.</span><span class="sxs-lookup"><span data-stu-id="ccd36-112">IoT Hub support for X.509 certificates.</span></span>
* <span data-ttu-id="ccd36-113">Var olan cihaz kimlik kayıt defterleri veya kimlik doğrulama şemasını kullanan özel cihaz kimlik doğrulama mekanizmaları.</span><span class="sxs-lookup"><span data-stu-id="ccd36-113">Custom device authentication mechanisms that use existing device identity registries or authentication schemes.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="ccd36-114">Zaman toouse</span><span class="sxs-lookup"><span data-stu-id="ccd36-114">When toouse</span></span>

<span data-ttu-id="ccd36-115">Uygun izinleri tooaccess hello IOT Hub uç noktaları hiçbirini olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-115">You must have appropriate permissions tooaccess any of hello IoT Hub endpoints.</span></span> <span data-ttu-id="ccd36-116">Örneğin, bir aygıt tooIoT Hub, gönderdiği her ileti yanı sıra güvenlik kimlik bilgileri içeren bir belirteç eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-116">For example, a device must include a token containing security credentials along with every message it sends tooIoT Hub.</span></span>

## <a name="access-control-and-permissions"></a><span data-ttu-id="ccd36-117">Erişim denetimi ve izinleri</span><span class="sxs-lookup"><span data-stu-id="ccd36-117">Access control and permissions</span></span>

<span data-ttu-id="ccd36-118">Erişim izni verebilir [izinleri](#iot-hub-permissions) yolları aşağıdaki hello içinde:</span><span class="sxs-lookup"><span data-stu-id="ccd36-118">You can grant [permissions](#iot-hub-permissions) in hello following ways:</span></span>

* <span data-ttu-id="ccd36-119">**IOT hub düzeyi paylaşılan erişim ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="ccd36-119">**IoT hub-level shared access policies**.</span></span> <span data-ttu-id="ccd36-120">Paylaşılan erişim ilkeleri, herhangi bir birleşimini vermek [izinleri](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="ccd36-120">Shared access policies can grant any combination of [permissions](#iot-hub-permissions).</span></span> <span data-ttu-id="ccd36-121">Hello ilkeleri tanımlayabilirsiniz [Azure portal][lnk-management-portal], hello kullanarak program aracılığıyla veya [IOT hub'ı kaynak sağlayıcısı REST API'leri][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="ccd36-121">You can define policies in hello [Azure portal][lnk-management-portal], or programmatically by using hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="ccd36-122">Yeni oluşturulan bir IOT hub aşağıdaki varsayılan ilkeler hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="ccd36-122">A newly created IoT hub has hello following default policies:</span></span>

  * <span data-ttu-id="ccd36-123">**iothubowner**: tüm izinleri ilkesiyle.</span><span class="sxs-lookup"><span data-stu-id="ccd36-123">**iothubowner**: Policy with all permissions.</span></span>
  * <span data-ttu-id="ccd36-124">**Hizmet**: ilke ile **ServiceConnect** izni.</span><span class="sxs-lookup"><span data-stu-id="ccd36-124">**service**: Policy with **ServiceConnect** permission.</span></span>
  * <span data-ttu-id="ccd36-125">**Aygıt**: ilke ile **DeviceConnect** izni.</span><span class="sxs-lookup"><span data-stu-id="ccd36-125">**device**: Policy with **DeviceConnect** permission.</span></span>
  * <span data-ttu-id="ccd36-126">**registryRead**: ilke ile **RegistryRead** izni.</span><span class="sxs-lookup"><span data-stu-id="ccd36-126">**registryRead**: Policy with **RegistryRead** permission.</span></span>
  * <span data-ttu-id="ccd36-127">**registryReadWrite**: ilke ile **RegistryRead** ve RegistryWrite izinleri.</span><span class="sxs-lookup"><span data-stu-id="ccd36-127">**registryReadWrite**: Policy with **RegistryRead** and RegistryWrite permissions.</span></span>
  * <span data-ttu-id="ccd36-128">**Cihaz başına güvenlik kimlik bilgileri**.</span><span class="sxs-lookup"><span data-stu-id="ccd36-128">**Per-device security credentials**.</span></span> <span data-ttu-id="ccd36-129">Her IOT hub'ı içeren bir [kimlik kayıt defteri][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="ccd36-129">Each IoT Hub contains an [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="ccd36-130">Bu kimlik kayıt defterinde her cihaz için vermek güvenlik kimlik bilgileri yapılandırabilirsiniz **DeviceConnect** izinleri kapsamlı toohello karşılık gelen cihaz uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="ccd36-130">For each device in this identity registry, you can configure security credentials that grant **DeviceConnect** permissions scoped toohello corresponding device endpoints.</span></span>

<span data-ttu-id="ccd36-131">Örneğin, tipik bir IOT çözüm içinde:</span><span class="sxs-lookup"><span data-stu-id="ccd36-131">For example, in a typical IoT solution:</span></span>

* <span data-ttu-id="ccd36-132">Merhaba aygıt yönetimi bileşeni kullanır hello *registryReadWrite* ilkesi.</span><span class="sxs-lookup"><span data-stu-id="ccd36-132">hello device management component uses hello *registryReadWrite* policy.</span></span>
* <span data-ttu-id="ccd36-133">Merhaba olay işlemci bileşeninin kullandığı hello *hizmet* ilkesi.</span><span class="sxs-lookup"><span data-stu-id="ccd36-133">hello event processor component uses hello *service* policy.</span></span>
* <span data-ttu-id="ccd36-134">Merhaba çalışma zamanı aygıt iş mantığı bileşeni kullanır hello *hizmet* ilkesi.</span><span class="sxs-lookup"><span data-stu-id="ccd36-134">hello run-time device business logic component uses hello *service* policy.</span></span>
* <span data-ttu-id="ccd36-135">Tek bir cihazı hello IOT hub'ın kimlik kayıt defterinde depolanan kimlik bilgilerini kullanarak bağlanın.</span><span class="sxs-lookup"><span data-stu-id="ccd36-135">Individual devices connect using credentials stored in hello IoT hub's identity registry.</span></span>

> [!NOTE]
> <span data-ttu-id="ccd36-136">Bkz: [izinleri](#iot-hub-permissions) ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ccd36-136">See [permissions](#iot-hub-permissions) for detailed information.</span></span>

## <a name="authentication"></a><span data-ttu-id="ccd36-137">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ccd36-137">Authentication</span></span>

<span data-ttu-id="ccd36-138">Azure IOT Hub, bir belirteç hello paylaşılan erişim ilkeleri ve kayıt defteri güvenlik kimlik karşı doğrulayarak erişim tooendpoints verir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-138">Azure IoT Hub grants access tooendpoints by verifying a token against hello shared access policies and identity registry security credentials.</span></span>

<span data-ttu-id="ccd36-139">Simetrik anahtarlar gibi güvenlik kimlik bilgileri hiçbir zaman hello kablo üzerinden gönderilir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-139">Security credentials, such as symmetric keys, are never sent over hello wire.</span></span>

> [!NOTE]
> <span data-ttu-id="ccd36-140">Merhaba tüm sağlayıcıları gibi hello Azure IOT Hub kaynak sağlayıcısı Azure aboneliğiniz ile korunuyor [Azure Resource Manager][lnk-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="ccd36-140">hello Azure IoT Hub resource provider is secured through your Azure subscription, as are all providers in hello [Azure Resource Manager][lnk-azure-resource-manager].</span></span>

<span data-ttu-id="ccd36-141">Hakkında daha fazla bilgi için güvenlik belirteçleri tooconstruct ve kullanım bkz [IOT hub'ı güvenlik belirteçleri][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="ccd36-141">For more information about how tooconstruct and use security tokens, see [IoT Hub security tokens][lnk-sas-tokens].</span></span>

### <a name="protocol-specifics"></a><span data-ttu-id="ccd36-142">Protokol özellikleri</span><span class="sxs-lookup"><span data-stu-id="ccd36-142">Protocol specifics</span></span>

<span data-ttu-id="ccd36-143">Desteklenen her protokolü, MQTT, AMQP ve HTTP gibi farklı yollarla belirteçleri taşımaları.</span><span class="sxs-lookup"><span data-stu-id="ccd36-143">Each supported protocol, such as MQTT, AMQP, and HTTP, transports tokens in different ways.</span></span>

<span data-ttu-id="ccd36-144">MQTT kullanırken hello BAĞLAN paket hello DeviceID ClientID, {iothubhostname} hello sahiptir / {DeviceID} hello Username alanı ve SAS belirteci hello parolası alanında.</span><span class="sxs-lookup"><span data-stu-id="ccd36-144">When using MQTT, hello CONNECT packet has hello deviceId as hello ClientId, {iothubhostname}/{deviceId} in hello Username field, and a SAS token in hello Password field.</span></span> <span data-ttu-id="ccd36-145">{iothubhostname} olması hello tam CName hello IOT hub (örneğin, contoso.azure-devices.net).</span><span class="sxs-lookup"><span data-stu-id="ccd36-145">{iothubhostname} should be hello full CName of hello IoT hub (for example, contoso.azure-devices.net).</span></span>

<span data-ttu-id="ccd36-146">Kullanırken [AMQP][lnk-amqp], IOT hub'ı destekleyen [SASL DÜZ] [ lnk-sasl-plain] ve [AMQP talep tabanlı-güvenlik] [ lnk-cbs].</span><span class="sxs-lookup"><span data-stu-id="ccd36-146">When using [AMQP][lnk-amqp], IoT Hub supports [SASL PLAIN][lnk-sasl-plain] and [AMQP Claims-Based-Security][lnk-cbs].</span></span>

<span data-ttu-id="ccd36-147">AMQP talep tabanlı-güvenlik kullanırsanız, standart hello belirtir nasıl tootransmit bu belirteçleri.</span><span class="sxs-lookup"><span data-stu-id="ccd36-147">If you use AMQP claims-based-security, hello standard specifies how tootransmit these tokens.</span></span>

<span data-ttu-id="ccd36-148">SASL DÜZ için hello **kullanıcıadı** olabilir:</span><span class="sxs-lookup"><span data-stu-id="ccd36-148">For SASL PLAIN, hello **username** can be:</span></span>

* <span data-ttu-id="ccd36-149">`{policyName}@sas.root.{iothubName}`IOT hub düzeyindeki belirteçleri kullanıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="ccd36-149">`{policyName}@sas.root.{iothubName}` if using IoT hub-level tokens.</span></span>
* <span data-ttu-id="ccd36-150">`{deviceId}@sas.{iothubname}`cihaz kapsamlı belirteçleri kullanıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="ccd36-150">`{deviceId}@sas.{iothubname}` if using device-scoped tokens.</span></span>

<span data-ttu-id="ccd36-151">Her iki durumda da açıklandığı gibi hello parola alanı hello belirtecini içeren [IOT hub'ı güvenlik belirteçleri][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="ccd36-151">In both cases, hello password field contains hello token, as described in [IoT Hub security tokens][lnk-sas-tokens].</span></span>

<span data-ttu-id="ccd36-152">HTTP kimlik doğrulaması geçerli bir belirteci hello dahil ederek uygulayan **yetkilendirme** istek üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="ccd36-152">HTTP implements authentication by including a valid token in hello **Authorization** request header.</span></span>

#### <a name="example"></a><span data-ttu-id="ccd36-153">Örnek</span><span class="sxs-lookup"><span data-stu-id="ccd36-153">Example</span></span>

<span data-ttu-id="ccd36-154">Kullanıcı adı (DeviceID büyük küçük harfe duyarlı):`iothubname.azure-devices.net/DeviceId`</span><span class="sxs-lookup"><span data-stu-id="ccd36-154">Username (DeviceId is case-sensitive): `iothubname.azure-devices.net/DeviceId`</span></span>

<span data-ttu-id="ccd36-155">Parola (oluşturmak SAS belirteci hello ile [aygıt explorer] [ lnk-device-explorer] aracı):`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span><span class="sxs-lookup"><span data-stu-id="ccd36-155">Password (Generate SAS token with hello [device explorer][lnk-device-explorer] tool): `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span></span>

> [!NOTE]
> <span data-ttu-id="ccd36-156">Merhaba [Azure IOT SDK'ları] [ lnk-sdks] toohello hizmet bağlanırken belirteçleri otomatik olarak oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="ccd36-156">hello [Azure IoT SDKs][lnk-sdks] automatically generate tokens when connecting toohello service.</span></span> <span data-ttu-id="ccd36-157">Bazı durumlarda, hello Azure IOT SDK'ları desteklemez tüm hello protokolleri ya da tüm hello kimlik doğrulama yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="ccd36-157">In some cases, hello Azure IoT SDKs do not support all hello protocols or all hello authentication methods.</span></span>

### <a name="special-considerations-for-sasl-plain"></a><span data-ttu-id="ccd36-158">SASL DÜZ için özel hususlar</span><span class="sxs-lookup"><span data-stu-id="ccd36-158">Special considerations for SASL PLAIN</span></span>

<span data-ttu-id="ccd36-159">SASL DÜZ AMQP ile kullanırken, tooan IOT hub'a bağlanan bir istemci her TCP bağlantısı için tek bir belirteci kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd36-159">When using SASL PLAIN with AMQP, a client connecting tooan IoT hub can use a single token for each TCP connection.</span></span> <span data-ttu-id="ccd36-160">Merhaba belirtecinin süresi dolduğunda, hello TCP bağlantısı hello hizmet bağlantısını keser ve bir reconnect tetikler.</span><span class="sxs-lookup"><span data-stu-id="ccd36-160">When hello token expires, hello TCP connection disconnects from hello service and triggers a reconnect.</span></span> <span data-ttu-id="ccd36-161">Bu davranış değil sorunlu sırada bir arka uç uygulaması için nedenleri aşağıdaki hello için cihaz uygulaması için zarar:</span><span class="sxs-lookup"><span data-stu-id="ccd36-161">This behavior, while not problematic for a back-end app, is damaging for a device app for hello following reasons:</span></span>

* <span data-ttu-id="ccd36-162">Ağ geçidi genellikle birçok aygıtlar adına bağlayın.</span><span class="sxs-lookup"><span data-stu-id="ccd36-162">Gateways usually connect on behalf of many devices.</span></span> <span data-ttu-id="ccd36-163">SASL DÜZ kullanırken, tooan IOT hub'a bağlanan her aygıt için ayrı bir TCP bağlantı toocreate sahip.</span><span class="sxs-lookup"><span data-stu-id="ccd36-163">When using SASL PLAIN, they have toocreate a distinct TCP connection for each device connecting tooan IoT hub.</span></span> <span data-ttu-id="ccd36-164">Bu senaryoda önemli ölçüde hello tüketimi, güç ve ağ kaynaklarını artırır ve her cihaz bağlantısı hello gecikme artar.</span><span class="sxs-lookup"><span data-stu-id="ccd36-164">This scenario considerably increases hello consumption of power and networking resources, and increases hello latency of each device connection.</span></span>
* <span data-ttu-id="ccd36-165">Kaynak kısıtlı cihazları olumsuz her belirteç süresi dolduktan sonra artan hello kaynakları tooreconnect kullanımıyla etkilenir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-165">Resource-constrained devices are adversely affected by hello increased use of resources tooreconnect after each token expiration.</span></span>

## <a name="scope-iot-hub-level-credentials"></a><span data-ttu-id="ccd36-166">Kapsam IOT hub düzeyindeki kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="ccd36-166">Scope IoT hub-level credentials</span></span>

<span data-ttu-id="ccd36-167">Sınırlı kaynak URI'si ile belirteçleri oluşturarak IOT hub'ı düzeyinde güvenlik ilkelerinin kapsamını belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd36-167">You can scope IoT hub-level security policies by creating tokens with a restricted resource URI.</span></span> <span data-ttu-id="ccd36-168">Örneğin, hello uç nokta toosend cihaz bulut iletilerini aygıttan **/devices/ {DeviceID} / iletileri/olayları**.</span><span class="sxs-lookup"><span data-stu-id="ccd36-168">For example, hello endpoint toosend device-to-cloud messages from a device is **/devices/{deviceId}/messages/events**.</span></span> <span data-ttu-id="ccd36-169">Bir IOT hub düzeyindeki paylaşılan erişim ilkesi ile de kullanabileceğiniz **DeviceConnect** izinleri toosign, resourceURI olan bir belirteç **/devices/ {DeviceID}**.</span><span class="sxs-lookup"><span data-stu-id="ccd36-169">You can also use an IoT hub-level shared access policy with **DeviceConnect** permissions toosign a token whose resourceURI is **/devices/{deviceId}**.</span></span> <span data-ttu-id="ccd36-170">Bu yaklaşım, yalnızca cihaz adına kullanılabilir toosend iletileri bir belirteç oluşturur **DeviceID**.</span><span class="sxs-lookup"><span data-stu-id="ccd36-170">This approach creates a token that is only usable toosend messages on behalf of device **deviceId**.</span></span>

<span data-ttu-id="ccd36-171">Bu bir mekanizmadır benzer toohello [olay hub'ları Yayımcı ilkesi][lnk-event-hubs-publisher-policy]ve tooimplement özel kimlik doğrulama yöntemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="ccd36-171">This mechanism is similar toohello [Event Hubs publisher policy][lnk-event-hubs-publisher-policy], and enables you tooimplement custom authentication methods.</span></span>

## <a name="security-tokens"></a><span data-ttu-id="ccd36-172">Güvenlik belirteçleri</span><span class="sxs-lookup"><span data-stu-id="ccd36-172">Security tokens</span></span>

<span data-ttu-id="ccd36-173">IOT hub'ı kullanan güvenlik tooauthenticate aygıtları belirteçleri ve anahtarları hello kablo gönderme tooavoid Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="ccd36-173">IoT Hub uses security tokens tooauthenticate devices and services tooavoid sending keys on hello wire.</span></span> <span data-ttu-id="ccd36-174">Ayrıca, güvenlik belirteçlerini geçerlilik tarihi ve kapsam sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-174">Additionally, security tokens are limited in time validity and scope.</span></span> <span data-ttu-id="ccd36-175">[Azure IOT SDK'ları] [ lnk-sdks] otomatik olarak özel bir yapılandırma gerektirmeden belirteçleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ccd36-175">[Azure IoT SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span></span> <span data-ttu-id="ccd36-176">Bazı senaryolar toogenerate gerektirir ve güvenlik belirteçlerini doğrudan kullanır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-176">Some scenarios do require you toogenerate and use security tokens directly.</span></span> <span data-ttu-id="ccd36-177">Bu tür senaryoları şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="ccd36-177">Such scenarios include:</span></span>

* <span data-ttu-id="ccd36-178">Merhaba doğrudan hello MQTT, AMQP veya HTTP yüzeyleri kullanımı.</span><span class="sxs-lookup"><span data-stu-id="ccd36-178">hello direct use of hello MQTT, AMQP, or HTTP surfaces.</span></span>
* <span data-ttu-id="ccd36-179">Merhaba belirteci hizmeti düzeni uyarlamasını açıklandığı gibi hello [özel cihaz kimlik doğrulamasını][lnk-custom-auth].</span><span class="sxs-lookup"><span data-stu-id="ccd36-179">hello implementation of hello token service pattern, as explained in [Custom device authentication][lnk-custom-auth].</span></span>

<span data-ttu-id="ccd36-180">IOT Hub ayrıca sağlar aygıtları tooauthenticate IOT Hub ile kullanarak [X.509 sertifikalarını][lnk-x509].</span><span class="sxs-lookup"><span data-stu-id="ccd36-180">IoT Hub also allows devices tooauthenticate with IoT Hub using [X.509 certificates][lnk-x509].</span></span>

### <a name="security-token-structure"></a><span data-ttu-id="ccd36-181">Güvenlik belirteci yapısı</span><span class="sxs-lookup"><span data-stu-id="ccd36-181">Security token structure</span></span>

<span data-ttu-id="ccd36-182">IOT Hub ' güvenlik belirteçleri toogrant zaman sınırlı erişim toodevices ve Hizmetleri toospecific işlevini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ccd36-182">You use security tokens toogrant time-bounded access toodevices and services toospecific functionality in IoT Hub.</span></span> <span data-ttu-id="ccd36-183">paylaşılan erişim veya simetrik anahtarı ile imzalanmış güvenlik belirteçleri tooget yetkilendirme tooconnect tooIoT Hub, cihazları ve Hizmetleri göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-183">tooget authorization tooconnect tooIoT Hub, devices and services must send security tokens signed with either a shared access or symmetric key.</span></span> <span data-ttu-id="ccd36-184">Bu anahtarları hello kimlik kayıt defterinde bir cihaz kimliği ile depolanır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-184">These keys are stored with a device identity in hello identity registry.</span></span>

<span data-ttu-id="ccd36-185">Merhaba paylaşılan erişim ilkesi izinleri ile ilişkili bir paylaşılan erişim anahtarı verir erişim tooall hello işlevselliğe sahip bir belirteci imzalayan.</span><span class="sxs-lookup"><span data-stu-id="ccd36-185">A token signed with a shared access key grants access tooall hello functionality associated with hello shared access policy permissions.</span></span> <span data-ttu-id="ccd36-186">Bir belirteci imzalayan aygıt kimliğin simetrik anahtar yalnızca verir hello ile **DeviceConnect** hello izinlerini ilişkili cihaz kimliği.</span><span class="sxs-lookup"><span data-stu-id="ccd36-186">A token signed with a device identity's symmetric key only grants hello **DeviceConnect** permission for hello associated device identity.</span></span>

<span data-ttu-id="ccd36-187">Merhaba güvenlik belirteci biçimi aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="ccd36-187">hello security token has hello following format:</span></span>

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

<span data-ttu-id="ccd36-188">Merhaba beklenen değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ccd36-188">Here are hello expected values:</span></span>

| <span data-ttu-id="ccd36-189">Değer</span><span class="sxs-lookup"><span data-stu-id="ccd36-189">Value</span></span> | <span data-ttu-id="ccd36-190">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ccd36-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ccd36-191">{İmza}</span><span class="sxs-lookup"><span data-stu-id="ccd36-191">{signature}</span></span> |<span data-ttu-id="ccd36-192">HMAC SHA256 imza dizisi hello formunun: `{URL-encoded-resourceURI} + "\n" + expiry`.</span><span class="sxs-lookup"><span data-stu-id="ccd36-192">An HMAC-SHA256 signature string of hello form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span></span> <span data-ttu-id="ccd36-193">**Önemli**: hello anahtar base64 kodlaması kodunu çözdü ve anahtar tooperform hello HMAC SHA256 hesaplama kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-193">**Important**: hello key is decoded from base64 and used as key tooperform hello HMAC-SHA256 computation.</span></span> |
| <span data-ttu-id="ccd36-194">{resourceURI}</span><span class="sxs-lookup"><span data-stu-id="ccd36-194">{resourceURI}</span></span> |<span data-ttu-id="ccd36-195">Merhaba IOT hub'ı (Protokol) ana bilgisayar adı ile başlayarak, bu belirteci ile erişilen hello uç noktalar için URI öneki (tarafından kesim).</span><span class="sxs-lookup"><span data-stu-id="ccd36-195">URI prefix (by segment) of hello endpoints that can be accessed with this token, starting with host name of hello IoT hub (no protocol).</span></span> <span data-ttu-id="ccd36-196">Örneğin, `myHub.azure-devices.net/devices/device1`</span><span class="sxs-lookup"><span data-stu-id="ccd36-196">For example, `myHub.azure-devices.net/devices/device1`</span></span> |
| <span data-ttu-id="ccd36-197">{süre sonu}</span><span class="sxs-lookup"><span data-stu-id="ccd36-197">{expiry}</span></span> |<span data-ttu-id="ccd36-198">UTF8 dizeleri hello dönemi: 00:00:00 UTC üzerinde 1 Ocak 1970'ten beri geçen saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="ccd36-198">UTF8 strings for number of seconds since hello epoch 00:00:00 UTC on 1 January 1970.</span></span> |
| <span data-ttu-id="ccd36-199">{URL-kodlanmış-resourceURI}</span><span class="sxs-lookup"><span data-stu-id="ccd36-199">{URL-encoded-resourceURI}</span></span> |<span data-ttu-id="ccd36-200">Düşük hello küçük kaynak URI'si için URL kodlaması durumda</span><span class="sxs-lookup"><span data-stu-id="ccd36-200">Lower case URL-encoding of hello lower case resource URI</span></span> |
| <span data-ttu-id="ccd36-201">{policyName}</span><span class="sxs-lookup"><span data-stu-id="ccd36-201">{policyName}</span></span> |<span data-ttu-id="ccd36-202">Bu belirteç başvuruyor hello paylaşılan erişim ilkesi toowhich Hello adı.</span><span class="sxs-lookup"><span data-stu-id="ccd36-202">hello name of hello shared access policy toowhich this token refers.</span></span> <span data-ttu-id="ccd36-203">Yüklenmesinden hello belirteci toodevice kayıt defteri kimlik bilgilerini ifade eder.</span><span class="sxs-lookup"><span data-stu-id="ccd36-203">Absent if hello token refers toodevice-registry credentials.</span></span> |

<span data-ttu-id="ccd36-204">**Not önek üzerinde**: hello URI öneki segmente göre ve karakter tarafından hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-204">**Note on prefix**: hello URI prefix is computed by segment and not by character.</span></span> <span data-ttu-id="ccd36-205">Örneğin `/a/b` için bir önek `/a/b/c` ancak için `/a/bc`.</span><span class="sxs-lookup"><span data-stu-id="ccd36-205">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span></span>

<span data-ttu-id="ccd36-206">Merhaba aşağıdaki Node.js parçacığını gösterir adlı bir işlev **generateSasToken** hesaplar hello girişleri belirtecinden hello `resourceUri, signingKey, policyName, expiresInMins`.</span><span class="sxs-lookup"><span data-stu-id="ccd36-206">hello following Node.js snippet shows a function called **generateSasToken** that computes hello token from hello inputs `resourceUri, signingKey, policyName, expiresInMins`.</span></span> <span data-ttu-id="ccd36-207">Merhaba sonraki bölümlerde nasıl tooinitialize hello farklı girişleri hello farklı belirteci için kullanım ayrıntılarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-207">hello next sections detail how tooinitialize hello different inputs for hello different token use cases.</span></span>

```nodejs
var generateSasToken = function(resourceUri, signingKey, policyName, expiresInMins) {
    resourceUri = encodeURIComponent(resourceUri);

    // Set expiration in seconds
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    expires = Math.ceil(expires);
    var toSign = resourceUri + '\n' + expires;

    // Use crypto
    var hmac = crypto.createHmac('sha256', new Buffer(signingKey, 'base64'));
    hmac.update(toSign);
    var base64UriEncoded = encodeURIComponent(hmac.digest('base64'));

    // Construct autorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
};
```

<span data-ttu-id="ccd36-208">Bir karşılaştırma bir güvenlik belirteci eşdeğer Python kodu toogenerate hello:</span><span class="sxs-lookup"><span data-stu-id="ccd36-208">As a comparison, hello equivalent Python code toogenerate a security token is:</span></span>

```python
from base64 import b64encode, b64decode
from hashlib import sha256
from time import time
from urllib import quote_plus, urlencode
from hmac import HMAC

def generate_sas_token(uri, key, policy_name, expiry=3600):
    ttl = time() + expiry
    sign_key = "%s\n%d" % ((quote_plus(uri)), int(ttl))
    print sign_key
    signature = b64encode(HMAC(b64decode(key), sign_key, sha256).digest())

    rawtoken = {
        'sr' :  uri,
        'sig': signature,
        'se' : str(int(ttl))
    }

    if policy_name is not None:
        rawtoken['skn'] = policy_name

    return 'SharedAccessSignature ' + urlencode(rawtoken)
```

> [!NOTE]
> <span data-ttu-id="ccd36-209">Hello zaman hello belirtecin geçerliliğini IOT hub'ı makinelerde doğrulanır olduğundan, başlangıç saati hello belirteci oluşturur hello makinenin hello kayması en az olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-209">Since hello time validity of hello token is validated on IoT Hub machines, hello drift on hello clock of hello machine that generates hello token must be minimal.</span></span>

### <a name="use-sas-tokens-in-a-device-app"></a><span data-ttu-id="ccd36-210">SAS belirteci bir aygıt uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="ccd36-210">Use SAS tokens in a device app</span></span>

<span data-ttu-id="ccd36-211">İki yolu tooobtain vardır **DeviceConnect** güvenlik belirteçleri IOT Hub ile izinlerle: kullanmak bir [simetrik aygıt hello kimlik kayıt defteri anahtarından](#use-a-symmetric-key-in-the-identity-registry), veya bir [paylaşılan erişim anahtarı](#use-a-shared-access-policy).</span><span class="sxs-lookup"><span data-stu-id="ccd36-211">There are two ways tooobtain **DeviceConnect** permissions with IoT Hub with security tokens: use a [symmetric device key from hello identity registry](#use-a-symmetric-key-in-the-identity-registry), or use a [shared access key](#use-a-shared-access-policy).</span></span>

<span data-ttu-id="ccd36-212">Tüm işlevlere aygıtlardan erişilebilir önekiyle uç noktalarda tasarıma göre sunulur unutmayın `/devices/{deviceId}`.</span><span class="sxs-lookup"><span data-stu-id="ccd36-212">Remember that all functionality accessible from devices is exposed by design on endpoints with prefix `/devices/{deviceId}`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ccd36-213">IOT hub'ı belirli bir aygıt doğrulayacağını hello tek yolu hello aygıt kimlik simetrik anahtar kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="ccd36-213">hello only way that IoT Hub authenticates a specific device is using hello device identity symmetric key.</span></span> <span data-ttu-id="ccd36-214">Paylaşılan Erişim İlkesi kullanılan tooaccess cihazın işlevselliğini olduğunda durumlarda hello güvenlik belirteci güvenilir bir alt bileşen olarak veren hello bileşen hello çözüm dikkate almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-214">In cases when a shared access policy is used tooaccess device functionality, hello solution must consider hello component issuing hello security token as a trusted subcomponent.</span></span>

<span data-ttu-id="ccd36-215">Merhaba aygıt'e yönelik uç noktalar (yedeklemiş hello Protokolü) şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ccd36-215">hello device-facing endpoints are (irrespective of hello protocol):</span></span>

| <span data-ttu-id="ccd36-216">Uç Nokta</span><span class="sxs-lookup"><span data-stu-id="ccd36-216">Endpoint</span></span> | <span data-ttu-id="ccd36-217">İşlev</span><span class="sxs-lookup"><span data-stu-id="ccd36-217">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |<span data-ttu-id="ccd36-218">Cihaz-bulut iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-218">Send device-to-cloud messages.</span></span> |
| `{iot hub host name}/devices/{deviceId}/devicebound` |<span data-ttu-id="ccd36-219">Bulut-cihaz iletilerini alır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-219">Receive cloud-to-device messages.</span></span> |

### <a name="use-a-symmetric-key-in-hello-identity-registry"></a><span data-ttu-id="ccd36-220">Simetrik anahtar hello kimlik kayıt defterinde kullanma</span><span class="sxs-lookup"><span data-stu-id="ccd36-220">Use a symmetric key in hello identity registry</span></span>

<span data-ttu-id="ccd36-221">Bir aygıt kimliğin simetrik anahtar toogenerate bir belirteç kullanırken policyName hello (`skn`) öğesi hello belirtecinin atlanmış.</span><span class="sxs-lookup"><span data-stu-id="ccd36-221">When using a device identity's symmetric key toogenerate a token, hello policyName (`skn`) element of hello token is omitted.</span></span>

<span data-ttu-id="ccd36-222">Örneğin, bir belirteç tüm cihazın işlevselliğini sahip hello şu parametreler tooaccess oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="ccd36-222">For example, a token created tooaccess all device functionality should have hello following parameters:</span></span>

* <span data-ttu-id="ccd36-223">Kaynak URI'si: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="ccd36-223">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="ccd36-224">imzalama anahtarı: herhangi bir simetrik anahtar hello için `{device id}` kimliği</span><span class="sxs-lookup"><span data-stu-id="ccd36-224">signing key: any symmetric key for hello `{device id}` identity,</span></span>
* <span data-ttu-id="ccd36-225">hiçbir ilke adı</span><span class="sxs-lookup"><span data-stu-id="ccd36-225">no policy name,</span></span>
* <span data-ttu-id="ccd36-226">Tüm süre sonu zamanı.</span><span class="sxs-lookup"><span data-stu-id="ccd36-226">any expiration time.</span></span>

<span data-ttu-id="ccd36-227">Node.js işlevi önceki hello kullanarak bir örnek olabilir:</span><span class="sxs-lookup"><span data-stu-id="ccd36-227">An example using hello preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

<span data-ttu-id="ccd36-228">erişim tooall işlevselliği device1 için verir, hello sonuç olacaktır:</span><span class="sxs-lookup"><span data-stu-id="ccd36-228">hello result, which grants access tooall functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> <span data-ttu-id="ccd36-229">Bu olası toogenerate hello .NET kullanarak bir SAS belirteci olan [aygıt explorer] [ lnk-device-explorer] aracı veya platformlar arası, düğüm tabanlı hello [iothub-explorer] [ lnk-iothub-explorer] komut satırı yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="ccd36-229">It is possible toogenerate a SAS token using hello .NET [device explorer][lnk-device-explorer] tool or hello cross-platform, node-based [iothub-explorer][lnk-iothub-explorer] command-line utility.</span></span>

### <a name="use-a-shared-access-policy"></a><span data-ttu-id="ccd36-230">Bir paylaşılan erişim ilkesi kullanın</span><span class="sxs-lookup"><span data-stu-id="ccd36-230">Use a shared access policy</span></span>

<span data-ttu-id="ccd36-231">Paylaşılan Erişim İlkesi tarafından bir belirteç oluşturduğunuzda, hello ayarlamak `skn` hello İlkesi alan toohello adı.</span><span class="sxs-lookup"><span data-stu-id="ccd36-231">When you create a token from a shared access policy, set hello `skn` field toohello name of hello policy.</span></span> <span data-ttu-id="ccd36-232">Bu ilke hello vermelidir **DeviceConnect** izni.</span><span class="sxs-lookup"><span data-stu-id="ccd36-232">This policy must grant hello **DeviceConnect** permission.</span></span>

<span data-ttu-id="ccd36-233">paylaşılan erişim ilkeleri tooaccess cihazın işlevselliğini kullanma hello iki ana senaryo şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ccd36-233">hello two main scenarios for using shared access policies tooaccess device functionality are:</span></span>

* <span data-ttu-id="ccd36-234">[protokol ağ geçidi bulut][lnk-endpoints],</span><span class="sxs-lookup"><span data-stu-id="ccd36-234">[cloud protocol gateways][lnk-endpoints],</span></span>
* <span data-ttu-id="ccd36-235">[simge Hizmetleri] [ lnk-custom-auth] tooimplement özel kimlik doğrulama şemasını kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-235">[token services][lnk-custom-auth] used tooimplement custom authentication schemes.</span></span>

<span data-ttu-id="ccd36-236">Bu yana Hello paylaşılan erişim ilkesi potansiyel olarak erişim tooconnect herhangi bir aygıtı güvenlik belirteçleri oluşturulurken önemli toouse hello doğru kaynak URI'si olduğundan verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd36-236">Since hello shared access policy can potentially grant access tooconnect as any device, it is important toouse hello correct resource URI when creating security tokens.</span></span> <span data-ttu-id="ccd36-237">Bu ayar tooscope hello belirteci tooa belirli cihazda hello kaynak URI'si kullanarak belirteci Hizmetleri için özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-237">This setting is especially important for token services, which have tooscope hello token tooa specific device using hello resource URI.</span></span> <span data-ttu-id="ccd36-238">Bu zaten tüm aygıtlar için trafiği eşlemlerse protokolü ağ geçitleri için daha az ilgili noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-238">This point is less relevant for protocol gateways as they are already mediating traffic for all devices.</span></span>

<span data-ttu-id="ccd36-239">Örnek olarak, önceden oluşturulan hello kullanarak bir belirteç hizmet adlı erişim ilkesi paylaşılan **aygıt** bir belirteç ile şu parametreler hello oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="ccd36-239">As an example, a token service using hello pre-created shared access policy called **device** would create a token with hello following parameters:</span></span>

* <span data-ttu-id="ccd36-240">Kaynak URI'si: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="ccd36-240">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="ccd36-241">imzalama anahtarı: hello hello anahtarları birini `device` İlkesi</span><span class="sxs-lookup"><span data-stu-id="ccd36-241">signing key: one of hello keys of hello `device` policy,</span></span>
* <span data-ttu-id="ccd36-242">İlke adı: `device`,</span><span class="sxs-lookup"><span data-stu-id="ccd36-242">policy name: `device`,</span></span>
* <span data-ttu-id="ccd36-243">Tüm süre sonu zamanı.</span><span class="sxs-lookup"><span data-stu-id="ccd36-243">any expiration time.</span></span>

<span data-ttu-id="ccd36-244">Node.js işlevi önceki hello kullanarak bir örnek olabilir:</span><span class="sxs-lookup"><span data-stu-id="ccd36-244">An example using hello preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="ccd36-245">erişim tooall işlevselliği device1 için verir, hello sonuç olacaktır:</span><span class="sxs-lookup"><span data-stu-id="ccd36-245">hello result, which grants access tooall functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

<span data-ttu-id="ccd36-246">Bir protokol ağ geçidi aynı belirteci yalnızca ayarı tüm cihazlar kaynak URI'si çok hello için hello kullanabilirsiniz`myhub.azure-devices.net/devices`.</span><span class="sxs-lookup"><span data-stu-id="ccd36-246">A protocol gateway could use hello same token for all devices simply setting hello resource URI too`myhub.azure-devices.net/devices`.</span></span>

### <a name="use-security-tokens-from-service-components"></a><span data-ttu-id="ccd36-247">Hizmet bileşenleri gelen güvenlik belirteçleri kullanın</span><span class="sxs-lookup"><span data-stu-id="ccd36-247">Use security tokens from service components</span></span>

<span data-ttu-id="ccd36-248">Hizmet bileşenleri, yalnızca daha önce açıklandığı gibi hello uygun izinleri verme paylaşılan erişim ilkeleri kullanan güvenlik belirteçleri üretebilir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-248">Service components can only generate security tokens using shared access policies granting hello appropriate permissions as explained previously.</span></span>

<span data-ttu-id="ccd36-249">Merhaba bitiş noktasında kullanıma sunulan hello hizmeti işlevleri şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ccd36-249">Here is hello service functions exposed on hello endpoints:</span></span>

| <span data-ttu-id="ccd36-250">Uç Nokta</span><span class="sxs-lookup"><span data-stu-id="ccd36-250">Endpoint</span></span> | <span data-ttu-id="ccd36-251">İşlev</span><span class="sxs-lookup"><span data-stu-id="ccd36-251">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices` |<span data-ttu-id="ccd36-252">Oluştur, Güncelleştir, alabilir ve cihaz kimliklerini silebilir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-252">Create, update, retrieve, and delete device identities.</span></span> |
| `{iot hub host name}/messages/events` |<span data-ttu-id="ccd36-253">Cihaz bulut iletilerini alır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-253">Receive device-to-cloud messages.</span></span> |
| `{iot hub host name}/servicebound/feedback` |<span data-ttu-id="ccd36-254">Bulut-cihaz iletilerini için bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="ccd36-254">Receive feedback for cloud-to-device messages.</span></span> |
| `{iot hub host name}/devicebound` |<span data-ttu-id="ccd36-255">Bulut cihaz iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-255">Send cloud-to-device messages.</span></span> |

<span data-ttu-id="ccd36-256">Örnek olarak, önceden oluşturulan hello kullanma oluşturma hizmeti adlı erişim ilkesi paylaşılan **registryRead** bir belirteç ile şu parametreler hello oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="ccd36-256">As an example, a service generating using hello pre-created shared access policy called **registryRead** would create a token with hello following parameters:</span></span>

* <span data-ttu-id="ccd36-257">Kaynak URI'si: `{IoT hub name}.azure-devices.net/devices`,</span><span class="sxs-lookup"><span data-stu-id="ccd36-257">resource URI: `{IoT hub name}.azure-devices.net/devices`,</span></span>
* <span data-ttu-id="ccd36-258">imzalama anahtarı: hello hello anahtarları birini `registryRead` İlkesi</span><span class="sxs-lookup"><span data-stu-id="ccd36-258">signing key: one of hello keys of hello `registryRead` policy,</span></span>
* <span data-ttu-id="ccd36-259">İlke adı: `registryRead`,</span><span class="sxs-lookup"><span data-stu-id="ccd36-259">policy name: `registryRead`,</span></span>
* <span data-ttu-id="ccd36-260">Tüm süre sonu zamanı.</span><span class="sxs-lookup"><span data-stu-id="ccd36-260">any expiration time.</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="ccd36-261">erişim tooread tüm cihaz kimliklerini vermeniz, hello sonuç olacaktır:</span><span class="sxs-lookup"><span data-stu-id="ccd36-261">hello result, which would grant access tooread all device identities, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a><span data-ttu-id="ccd36-262">Desteklenen X.509 sertifikaları</span><span class="sxs-lookup"><span data-stu-id="ccd36-262">Supported X.509 certificates</span></span>

<span data-ttu-id="ccd36-263">Bir X.509 sertifikası tooauthenticate bir cihaz IOT Hub ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd36-263">You can use any X.509 certificate tooauthenticate a device with IoT Hub.</span></span> <span data-ttu-id="ccd36-264">Sertifikaları dahil et:</span><span class="sxs-lookup"><span data-stu-id="ccd36-264">Certificates include:</span></span>

* <span data-ttu-id="ccd36-265">**Varolan bir X.509 sertifikası**.</span><span class="sxs-lookup"><span data-stu-id="ccd36-265">**An existing X.509 certificate**.</span></span> <span data-ttu-id="ccd36-266">Bir aygıt zaten kendisiyle ilişkilendirilmiş bir X.509 sertifikası olabilir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-266">A device may already have an X.509 certificate associated with it.</span></span> <span data-ttu-id="ccd36-267">Bu sertifika tooauthenticate Hello cihaz IOT Hub ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd36-267">hello device can use this certificate tooauthenticate with IoT Hub.</span></span>
* <span data-ttu-id="ccd36-268">**A otomatik olarak oluşturulan ve X-509 Sertifika'otomatik olarak imzalanan**.</span><span class="sxs-lookup"><span data-stu-id="ccd36-268">**A self-generated and self-signed X-509 certificate**.</span></span> <span data-ttu-id="ccd36-269">Bir aygıt üreticisi veya şirket içi dağıtıcı, bu sertifikalar oluşturmak ve hello karşılık gelen özel anahtar (ve sertifika) hello aygıtta depolamak.</span><span class="sxs-lookup"><span data-stu-id="ccd36-269">A device manufacturer or in-house deployer can generate these certificates and store hello corresponding private key (and certificate) on hello device.</span></span> <span data-ttu-id="ccd36-270">Araçları gibi kullanabilir [OpenSSL] [ lnk-openssl] ve [Windows SelfSignedCertificate] [ lnk-selfsigned] bu amaç için yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="ccd36-270">You can use tools such as [OpenSSL][lnk-openssl] and [Windows SelfSignedCertificate][lnk-selfsigned] utility for this purpose.</span></span>
* <span data-ttu-id="ccd36-271">**X.509 sertifikası CA tarafından imzalanmış**.</span><span class="sxs-lookup"><span data-stu-id="ccd36-271">**CA-signed X.509 certificate**.</span></span> <span data-ttu-id="ccd36-272">bir aygıt tooidentify ve IOT Hub ile kimlik doğrulaması, oluşturulur ve bir sertifika yetkilisi (CA) tarafından imzalanmış bir X.509 sertifikası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd36-272">tooidentify a device and authenticate it with IoT Hub, you can use an X.509 certificate generated and signed by a Certification Authority (CA).</span></span> <span data-ttu-id="ccd36-273">IOT hub'ı yalnızca sunulan bu hello parmak izi doğrular hello yapılandırılmış parmak izi ile eşleşir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-273">IoT Hub only verifies that hello thumbprint presented matches hello configured thumbprint.</span></span> <span data-ttu-id="ccd36-274">Iothub hello sertifika zinciri doğrulamaz.</span><span class="sxs-lookup"><span data-stu-id="ccd36-274">IotHub does not validate hello certificate chain.</span></span>

<span data-ttu-id="ccd36-275">Bir aygıt ya da bir X.509 sertifikası veya bir güvenlik belirteci kimlik doğrulaması, ancak ikisini için kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-275">A device may either use an X.509 certificate or a security token for authentication, but not both.</span></span>

### <a name="register-an-x509-certificate-for-a-device"></a><span data-ttu-id="ccd36-276">Bir aygıt bir X.509 sertifikası Kaydet</span><span class="sxs-lookup"><span data-stu-id="ccd36-276">Register an X.509 certificate for a device</span></span>

<span data-ttu-id="ccd36-277">Merhaba [Azure IOT hizmeti SDK'sı için C#] [ lnk-service-sdk] (sürüm 1.0.8+) destekleyen bir X.509 sertifikası için kimlik doğrulaması kullanan bir cihazı kaydetme.</span><span class="sxs-lookup"><span data-stu-id="ccd36-277">hello [Azure IoT Service SDK for C#][lnk-service-sdk] (version 1.0.8+) supports registering a device that uses an X.509 certificate for authentication.</span></span> <span data-ttu-id="ccd36-278">İçeri/dışarı aktarma aygıtların gibi diğer API'leri X.509 sertifikalarını da destekler.</span><span class="sxs-lookup"><span data-stu-id="ccd36-278">Other APIs such as import/export of devices also support X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="ccd36-279">C\# desteği</span><span class="sxs-lookup"><span data-stu-id="ccd36-279">C\# Support</span></span>

<span data-ttu-id="ccd36-280">Merhaba **RegistryManager** sınıfı, bir cihaz programlı şekilde tooregister sağlar.</span><span class="sxs-lookup"><span data-stu-id="ccd36-280">hello **RegistryManager** class provides a programmatic way tooregister a device.</span></span> <span data-ttu-id="ccd36-281">Özellikle, hello **AddDeviceAsync** ve **UpdateDeviceAsync** yöntemleri tooregister etkinleştirmek ve bir aygıtı hello IOT Hub kimlik kayıt defteri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ccd36-281">In particular, hello **AddDeviceAsync** and **UpdateDeviceAsync** methods enable you tooregister and update a device in hello IoT Hub identity registry.</span></span> <span data-ttu-id="ccd36-282">Bu iki yöntem ele bir **aygıt** örnek giriş olarak.</span><span class="sxs-lookup"><span data-stu-id="ccd36-282">These two methods take a **Device** instance as input.</span></span> <span data-ttu-id="ccd36-283">Hello **aygıt** sınıfı içeren bir **kimlik doğrulaması** toospecify birincil ve ikincil X.509 sertifika parmak izlerini veren özelliği.</span><span class="sxs-lookup"><span data-stu-id="ccd36-283">hello **Device** class includes an **Authentication** property that allows you toospecify primary and secondary X.509 certificate thumbprints.</span></span> <span data-ttu-id="ccd36-284">Merhaba parmak izi SHA-1 karma hello X.509 sertifikası (DER ikili kodlama kullanılarak depolanır) değerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ccd36-284">hello thumbprint represents a SHA-1 hash of hello X.509 certificate (stored using binary DER encoding).</span></span> <span data-ttu-id="ccd36-285">Merhaba birincil bir parmak izi veya ikincil bir parmak izi veya her ikisini belirtme seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-285">You have hello option of specifying a primary thumbprint or a secondary thumbprint or both.</span></span> <span data-ttu-id="ccd36-286">Birincil ve ikincil parmak izleri desteklenen toohandle sertifika aktarma senaryolar verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-286">Primary and secondary thumbprints are supported toohandle certificate rollover scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="ccd36-287">IOT hub'ı gerektirmez veya hello tüm X.509 sertifikası, parmak izi hello depolar.</span><span class="sxs-lookup"><span data-stu-id="ccd36-287">IoT Hub does not require or store hello entire X.509 certificate, only hello thumbprint.</span></span>

<span data-ttu-id="ccd36-288">Örnek C işte\# parçacığı tooregister bir X.509 sertifikası kullanarak bir cihazı kod:</span><span class="sxs-lookup"><span data-stu-id="ccd36-288">Here is a sample C\# code snippet tooregister a device using an X.509 certificate:</span></span>

```csharp
var device = new Device(deviceId)
{
  Authentication = new AuthenticationMechanism()
  {
    X509Thumbprint = new X509Thumbprint()
    {
      PrimaryThumbprint = "921BC9694ADEB8929D4F7FE4B9A3A6DE58B0790B"
    }
  }
};
RegistryManager registryManager = RegistryManager.CreateFromConnectionString(deviceGatewayConnectionString);
await registryManager.AddDeviceAsync(device);
```

### <a name="use-an-x509-certificate-during-run-time-operations"></a><span data-ttu-id="ccd36-289">Çalıştırma işlemleri sırasında bir X.509 sertifikası kullanın</span><span class="sxs-lookup"><span data-stu-id="ccd36-289">Use an X.509 certificate during run-time operations</span></span>

<span data-ttu-id="ccd36-290">Merhaba [.NET için Azure IOT cihaz SDK'sı] [ lnk-client-sdk] (sürüm 1.0.11+) X.509 sertifikalarını hello kullanımını destekler.</span><span class="sxs-lookup"><span data-stu-id="ccd36-290">hello [Azure IoT device SDK for .NET][lnk-client-sdk] (version 1.0.11+) supports hello use of X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="ccd36-291">C\# desteği</span><span class="sxs-lookup"><span data-stu-id="ccd36-291">C\# Support</span></span>

<span data-ttu-id="ccd36-292">Merhaba sınıfı **DeviceAuthenticationWithX509Certificate** destekler hello oluşturulmasını **DeviceClient** X.509 sertifikası kullanarak örnekleri.</span><span class="sxs-lookup"><span data-stu-id="ccd36-292">hello class **DeviceAuthenticationWithX509Certificate** supports hello creation of **DeviceClient** instances using an X.509 certificate.</span></span> <span data-ttu-id="ccd36-293">Merhaba X.509 sertifikası hello özel anahtarı içeren hello (PKCS #12 olarak da bilinir) PFX biçiminde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-293">hello X.509 certificate must be in hello PFX (also called PKCS #12) format that includes hello private key.</span></span>

<span data-ttu-id="ccd36-294">Örnek kod parçacığı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ccd36-294">Here is a sample code snippet:</span></span>

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a><span data-ttu-id="ccd36-295">Özel cihaz kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ccd36-295">Custom device authentication</span></span>

<span data-ttu-id="ccd36-296">Merhaba IOT hub'ı kullanabilirsiniz [kimlik kayıt defteri] [ lnk-identity-registry] tooconfigure cihaz başına güvenlik kimlik ve erişim denetimi kullanarak [belirteçleri] [ lnk-sas-tokens] .</span><span class="sxs-lookup"><span data-stu-id="ccd36-296">You can use hello IoT Hub [identity registry][lnk-identity-registry] tooconfigure per-device security credentials and access control using [tokens][lnk-sas-tokens].</span></span> <span data-ttu-id="ccd36-297">Bir IOT çözümündeki bir özel kimlik kayıt defteri ve/veya kimlik doğrulama düzeni zaten varsa, oluşturmayı göz önünde bulundurun bir *belirteç hizmeti* toointegrate IOT Hub ile bu altyapı.</span><span class="sxs-lookup"><span data-stu-id="ccd36-297">If an IoT solution already has a custom identity registry and/or authentication scheme, consider creating a *token service* toointegrate this infrastructure with IoT Hub.</span></span> <span data-ttu-id="ccd36-298">Bu şekilde, çözümünüz içinde diğer IOT özelliklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd36-298">In this way, you can use other IoT features in your solution.</span></span>

<span data-ttu-id="ccd36-299">Bir belirteci hizmeti bir özel bulut hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-299">A token service is a custom cloud service.</span></span> <span data-ttu-id="ccd36-300">IOT hub'ı kullanan *paylaşılan erişim ilkesi* ile **DeviceConnect** izinleri toocreate *aygıt kapsamlı* belirteçleri.</span><span class="sxs-lookup"><span data-stu-id="ccd36-300">It uses an IoT Hub *shared access policy* with **DeviceConnect** permissions toocreate *device-scoped* tokens.</span></span> <span data-ttu-id="ccd36-301">Bu belirteçler bir aygıt tooconnect tooyour IOT hub'ı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ccd36-301">These tokens enable a device tooconnect tooyour IoT hub.</span></span>

![Merhaba belirteci hizmeti deseninin adımları][img-tokenservice]

<span data-ttu-id="ccd36-303">Merhaba belirteci hizmeti deseninin hello ana adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ccd36-303">Here are hello main steps of hello token service pattern:</span></span>

1. <span data-ttu-id="ccd36-304">IOT Hub'ı paylaşılan erişim ilkesi ile oluşturma **DeviceConnect** IOT hub'ınız için izinleri.</span><span class="sxs-lookup"><span data-stu-id="ccd36-304">Create an IoT Hub shared access policy with **DeviceConnect** permissions for your IoT hub.</span></span> <span data-ttu-id="ccd36-305">Bu ilke hello oluşturabilirsiniz [Azure portal] [ lnk-management-portal] veya program aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="ccd36-305">You can create this policy in hello [Azure portal][lnk-management-portal] or programmatically.</span></span> <span data-ttu-id="ccd36-306">Merhaba belirteci hizmeti oluşturduğu Bu ilke toosign hello belirteçlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-306">hello token service uses this policy toosign hello tokens it creates.</span></span>
1. <span data-ttu-id="ccd36-307">Bir cihaz IOT hub'ınızı tooaccess gerektiğinde, imzalı bir belirteç belirteci Hizmeti'nden ister.</span><span class="sxs-lookup"><span data-stu-id="ccd36-307">When a device needs tooaccess your IoT hub, it requests a signed token from your token service.</span></span> <span data-ttu-id="ccd36-308">Merhaba aygıt hello belirteci hizmeti toocreate hello belirtecini kullanır, özel kimlik kayıt defteri/kimlik doğrulama düzeni toodetermine hello cihaz kimliği ile kimlik doğrulaması yapabilir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-308">hello device can authenticate with your custom identity registry/authentication scheme toodetermine hello device identity that hello token service uses toocreate hello token.</span></span>
1. <span data-ttu-id="ccd36-309">Merhaba belirteci hizmeti bir belirteci döndürür.</span><span class="sxs-lookup"><span data-stu-id="ccd36-309">hello token service returns a token.</span></span> <span data-ttu-id="ccd36-310">Merhaba belirteci kullanılarak oluşturulan `/devices/{deviceId}` olarak `resourceURI`, ile `deviceId` kimlik doğrulaması gerçekleştirilen hello aygıt olarak.</span><span class="sxs-lookup"><span data-stu-id="ccd36-310">hello token is created by using `/devices/{deviceId}` as `resourceURI`, with `deviceId` as hello device being authenticated.</span></span> <span data-ttu-id="ccd36-311">Merhaba belirteç hizmeti hello paylaşılan erişim ilkesi tooconstruct hello belirteci kullanır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-311">hello token service uses hello shared access policy tooconstruct hello token.</span></span>
1. <span data-ttu-id="ccd36-312">Merhaba cihaz doğrudan hello IOT hub ile Merhaba belirtecini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-312">hello device uses hello token directly with hello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="ccd36-313">Merhaba .NET sınıfını kullanabilirsiniz [SharedAccessSignatureBuilder] [ lnk-dotnet-sas] veya Java sınıfı hello [IotHubServiceSasToken] [ lnk-java-sas] toocreate bir belirteç belirteci hizmetinizi.</span><span class="sxs-lookup"><span data-stu-id="ccd36-313">You can use hello .NET class [SharedAccessSignatureBuilder][lnk-dotnet-sas] or hello Java class [IotHubServiceSasToken][lnk-java-sas] toocreate a token in your token service.</span></span>

<span data-ttu-id="ccd36-314">Merhaba belirteci hizmeti hello belirteci süre sonu istendiği gibi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd36-314">hello token service can set hello token expiration as desired.</span></span> <span data-ttu-id="ccd36-315">Merhaba belirtecinin süresi dolduğunda, hello IOT hub'ı hello cihaz bağlantısı sunucularının.</span><span class="sxs-lookup"><span data-stu-id="ccd36-315">When hello token expires, hello IoT hub severs hello device connection.</span></span> <span data-ttu-id="ccd36-316">Ardından, hello aygıt hello belirteci Hizmeti'nden yeni bir belirteç istemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-316">Then, hello device must request a new token from hello token service.</span></span> <span data-ttu-id="ccd36-317">Kısa süre sonu zamanı hello cihaz ve hello belirteci hizmeti hello yükü artırır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-317">A short expiry time increases hello load on both hello device and hello token service.</span></span>

<span data-ttu-id="ccd36-318">Aygıt tooconnect tooyour hub için hala toohello IOT Hub kimlik kayıt defteri eklemelisiniz — hello aygıt bir belirteç ve olmayan bir aygıt anahtar tooconnect kullanıyor olsa da.</span><span class="sxs-lookup"><span data-stu-id="ccd36-318">For a device tooconnect tooyour hub, you must still add it toohello IoT Hub identity registry — even though hello device is using a token and not a device key tooconnect.</span></span> <span data-ttu-id="ccd36-319">Bu nedenle, etkinleştirme veya hello cihaz kimliklerini devre dışı bırakarak toouse aygıt başına erişim denetimi devam edebilirsiniz [kimlik kayıt defteri][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="ccd36-319">Therefore, you can continue toouse per-device access control by enabling or disabling device identities in hello [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="ccd36-320">Bu yaklaşım, uzun süre sonu zamanlarında belirteçleri kullanarak hello riskleri azaltır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-320">This approach mitigates hello risks of using tokens with long expiry times.</span></span>

### <a name="comparison-with-a-custom-gateway"></a><span data-ttu-id="ccd36-321">Özel bir ağ geçidi ile karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="ccd36-321">Comparison with a custom gateway</span></span>

<span data-ttu-id="ccd36-322">Merhaba belirteci hizmeti düzeni hello yolu tooimplement IOT hub'ı içeren bir özel kimlik kayıt defteri/kimlik doğrulaması şeması önerilen ' dir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-322">hello token service pattern is hello recommended way tooimplement a custom identity registry/authentication scheme with IoT Hub.</span></span> <span data-ttu-id="ccd36-323">IOT hub'ı toohandle devam ettiğinden bu deseni önerilir hello çözüm trafiğin çoğu.</span><span class="sxs-lookup"><span data-stu-id="ccd36-323">This pattern is recommended because IoT Hub continues toohandle most of hello solution traffic.</span></span> <span data-ttu-id="ccd36-324">Ancak, hello özel kimlik doğrulama düzeni şekilde hello protokolüyle birbirine, gerektirebilecek bir *özel ağ geçidi* tooprocess tüm trafiği hello.</span><span class="sxs-lookup"><span data-stu-id="ccd36-324">However, if hello custom authentication scheme is so intertwined with hello protocol, you may require a *custom gateway* tooprocess all hello traffic.</span></span> <span data-ttu-id="ccd36-325">Böyle bir senaryo örneği kullanarak[Aktarım Katmanı Güvenliği (TLS) ve önceden paylaşılan anahtarı (PSKs)][lnk-tls-psk].</span><span class="sxs-lookup"><span data-stu-id="ccd36-325">An example of such a scenario is using[Transport Layer Security (TLS) and pre-shared keys (PSKs)][lnk-tls-psk].</span></span> <span data-ttu-id="ccd36-326">Daha fazla bilgi için bkz: Merhaba [protokol ağ geçidi] [ lnk-protocols] konu.</span><span class="sxs-lookup"><span data-stu-id="ccd36-326">For more information, see hello [protocol gateway][lnk-protocols] topic.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="ccd36-327">Başvuru konuları:</span><span class="sxs-lookup"><span data-stu-id="ccd36-327">Reference topics:</span></span>

<span data-ttu-id="ccd36-328">Merhaba aşağıdaki başvuru konuları denetleme erişim tooyour IOT hub'ı hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ccd36-328">hello following reference topics provide you with more information about controlling access tooyour IoT hub.</span></span>

## <a name="iot-hub-permissions"></a><span data-ttu-id="ccd36-329">IOT hub'ı izinleri</span><span class="sxs-lookup"><span data-stu-id="ccd36-329">IoT Hub permissions</span></span>

<span data-ttu-id="ccd36-330">Merhaba aşağıdaki tabloda toocontrol erişim tooyour IOT hub'ı kullanabilirsiniz hello izinleri listeler.</span><span class="sxs-lookup"><span data-stu-id="ccd36-330">hello following table lists hello permissions you can use toocontrol access tooyour IoT hub.</span></span>

| <span data-ttu-id="ccd36-331">İzin</span><span class="sxs-lookup"><span data-stu-id="ccd36-331">Permission</span></span> | <span data-ttu-id="ccd36-332">Notlar</span><span class="sxs-lookup"><span data-stu-id="ccd36-332">Notes</span></span> |
| --- | --- |
| <span data-ttu-id="ccd36-333">**RegistryRead**</span><span class="sxs-lookup"><span data-stu-id="ccd36-333">**RegistryRead**</span></span> |<span data-ttu-id="ccd36-334">Okuma erişimi toohello kimlik kayıt defteri verir.</span><span class="sxs-lookup"><span data-stu-id="ccd36-334">Grants read access toohello identity registry.</span></span> <span data-ttu-id="ccd36-335">Daha fazla bilgi için bkz: [kimlik kayıt defteri][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="ccd36-335">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="ccd36-336">Bu izin, arka uç bulut Hizmetleri tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-336">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="ccd36-337">**RegistryReadWrite**</span><span class="sxs-lookup"><span data-stu-id="ccd36-337">**RegistryReadWrite**</span></span> |<span data-ttu-id="ccd36-338">Verir okuma ve yazma erişimi toohello kimlik kayıt defteri.</span><span class="sxs-lookup"><span data-stu-id="ccd36-338">Grants read and write access toohello identity registry.</span></span> <span data-ttu-id="ccd36-339">Daha fazla bilgi için bkz: [kimlik kayıt defteri][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="ccd36-339">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="ccd36-340">Bu izin, arka uç bulut Hizmetleri tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-340">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="ccd36-341">**ServiceConnect**</span><span class="sxs-lookup"><span data-stu-id="ccd36-341">**ServiceConnect**</span></span> |<span data-ttu-id="ccd36-342">Verir toocloud hizmet dönük iletişim ve uç nokta izleme erişin.</span><span class="sxs-lookup"><span data-stu-id="ccd36-342">Grants access toocloud service-facing communication and monitoring endpoints.</span></span> <br/><span data-ttu-id="ccd36-343">Verir izni tooreceive cihaz bulut iletilerini, bulut-cihaz iletilerini ve teslim alındı bildirimleri karşılık gelen alma hello gönderin.</span><span class="sxs-lookup"><span data-stu-id="ccd36-343">Grants permission tooreceive device-to-cloud messages, send cloud-to-device messages, and retrieve hello corresponding delivery acknowledgments.</span></span> <br/><span data-ttu-id="ccd36-344">Dosya için verir izni tooretrieve teslim onay yükler.</span><span class="sxs-lookup"><span data-stu-id="ccd36-344">Grants permission tooretrieve delivery acknowledgements for file uploads.</span></span> <br/><span data-ttu-id="ccd36-345">Verir izni tooaccess cihaz çiftlerini tooupdate etiketleri ve istenen özellikleri bildirilen özelliklerini almak ve sorgular çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ccd36-345">Grants permission tooaccess device twins tooupdate tags and desired properties, retrieve reported properties, and run queries.</span></span> <br/><span data-ttu-id="ccd36-346">Bu izin, arka uç bulut Hizmetleri tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-346">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="ccd36-347">**DeviceConnect**</span><span class="sxs-lookup"><span data-stu-id="ccd36-347">**DeviceConnect**</span></span> |<span data-ttu-id="ccd36-348">Verir toodevice'te Uç noktalara erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd36-348">Grants access toodevice-facing endpoints.</span></span> <br/><span data-ttu-id="ccd36-349">Verir izni toosend cihaz-bulut iletileri ve bulut-cihaz iletilerini.</span><span class="sxs-lookup"><span data-stu-id="ccd36-349">Grants permission toosend device-to-cloud messages and receive cloud-to-device messages.</span></span> <br/><span data-ttu-id="ccd36-350">Verir izni tooperform karşıya dosya yükleme aygıttan.</span><span class="sxs-lookup"><span data-stu-id="ccd36-350">Grants permission tooperform file upload from a device.</span></span> <br/><span data-ttu-id="ccd36-351">Verir izin tooreceive cihaz çifti istenen özelliği bildirimleri ve bildirilen özellikleri twin güncelleştirme aygıt.</span><span class="sxs-lookup"><span data-stu-id="ccd36-351">Grants permission tooreceive device twin desired property notifications and update device twin reported properties.</span></span> <br/><span data-ttu-id="ccd36-352">Verir izni tooperform dosyayı yükler.</span><span class="sxs-lookup"><span data-stu-id="ccd36-352">Grants permission tooperform file uploads.</span></span> <br/><span data-ttu-id="ccd36-353">Bu izin, cihazlar tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ccd36-353">This permission is used by devices.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="ccd36-354">Ek başvuru bilgileri</span><span class="sxs-lookup"><span data-stu-id="ccd36-354">Additional reference material</span></span>

<span data-ttu-id="ccd36-355">Merhaba IOT Hub Geliştirici Kılavuzu diğer başvuru konularına şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="ccd36-355">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="ccd36-356">[IOT Hub uç noktaları] [ lnk-endpoints] açıklar çalışma zamanı ve yönetim işlemleri için her IOT hub'ı sunan çeşitli uç noktaları hello.</span><span class="sxs-lookup"><span data-stu-id="ccd36-356">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="ccd36-357">[Azaltma ve kotaları] [ lnk-quotas] hello kotaları açıklar ve IOT Hub hizmeti toohello uygulamak davranışları azaltma.</span><span class="sxs-lookup"><span data-stu-id="ccd36-357">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="ccd36-358">[Azure IOT cihaz ve hizmet SDK'ları] [ lnk-sdks] listeleri hello çeşitli dil SDK'ları, IOT Hub ile etkileşim hem cihaz hem de hizmet uygulamaları geliştirdiğinizde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd36-358">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="ccd36-359">[IOT hub'ı sorgu dili] [ lnk-query] tooretrieve bilgilerini IOT hub'dan cihaz çiftlerini ve işleri kullanabileceğiniz hello sorgu dili açıklar.</span><span class="sxs-lookup"><span data-stu-id="ccd36-359">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="ccd36-360">[IOT Hub MQTT Destek] [ lnk-devguide-mqtt] hello MQTT protokolü için IOT hub'ı desteği hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ccd36-360">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccd36-361">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ccd36-361">Next steps</span></span>

<span data-ttu-id="ccd36-362">Nasıl toocontrol erişim IOT hub'ı öğrendiniz artık IOT Hub Geliştirici Kılavuzu konuları aşağıdaki hello ilgilenen olabilir:</span><span class="sxs-lookup"><span data-stu-id="ccd36-362">Now you have learned how toocontrol access IoT Hub, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="ccd36-363">[Cihaz çiftlerini toosynchronize durumu ve yapılandırmaları kullanacak][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="ccd36-363">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="ccd36-364">[Bir cihazda doğrudan bir yöntem çağırma][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="ccd36-364">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="ccd36-365">[Birden çok aygıta işleri zamanla][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="ccd36-365">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="ccd36-366">Bu makalede açıklanan hello kavramların bazıları çıkışı tootry isterseniz, IOT hub'ı öğreticileri aşağıdaki hello ilgilenen olabilir:</span><span class="sxs-lookup"><span data-stu-id="ccd36-366">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorials:</span></span>

* <span data-ttu-id="ccd36-367">[Azure IOT Hub ile çalışmaya başlama][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="ccd36-367">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>
* <span data-ttu-id="ccd36-368">[Toosend bulut-cihaz IOT Hub ile nasıl iletileri][lnk-c2d-tutorial]</span><span class="sxs-lookup"><span data-stu-id="ccd36-368">[How toosend cloud-to-device messages with IoT Hub][lnk-c2d-tutorial]</span></span>
* <span data-ttu-id="ccd36-369">[Nasıl tooprocess IOT hub'a cihaz-bulut iletileri][lnk-d2c-tutorial]</span><span class="sxs-lookup"><span data-stu-id="ccd36-369">[How tooprocess IoT Hub device-to-cloud messages][lnk-d2c-tutorial]</span></span>

<!-- links and images -->

[img-tokenservice]: ./media/iot-hub-devguide-security/tokenservice.png
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-openssl]: https://www.openssl.org/
[lnk-selfsigned]: https://technet.microsoft.com/library/hh848633

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-sas-tokens]: iot-hub-devguide-security.md#security-tokens
[lnk-amqp]: https://www.amqp.org/
[lnk-azure-resource-manager]: ../azure-resource-manager/resource-group-overview.md
[lnk-cbs]: https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc
[lnk-event-hubs-publisher-policy]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab
[lnk-management-portal]: https://portal.azure.com
[lnk-sasl-plain]: http://tools.ietf.org/html/rfc4616
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-dotnet-sas]: https://msdn.microsoft.com/library/microsoft.azure.devices.common.security.sharedaccesssignaturebuilder.aspx
[lnk-java-sas]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth._iot_hub_service_sas_token
[lnk-tls-psk]: https://tools.ietf.org/html/rfc4279
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-custom-auth]: iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: iot-hub-devguide-security.md#supported-x509-certificates
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-client-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
