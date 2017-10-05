---
title: "Azure IOT Hub güvenliği anlama | Microsoft Docs"
description: "Geliştirici Kılavuzu - cihaz uygulamaları ve arka uç uygulamalar için IOT Hub'ına erişimi denetleme. Güvenlik belirteçleri ve X.509 sertifikalarını desteği hakkında bilgiler içerir."
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
ms.openlocfilehash: e4fe5400ffcf4446392015aada031dd4dfbf238a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="control-access-to-iot-hub"></a><span data-ttu-id="56097-104">IoT Hub’a erişimi denetleme</span><span class="sxs-lookup"><span data-stu-id="56097-104">Control access to IoT Hub</span></span>

<span data-ttu-id="56097-105">Bu makalede, IOT hub'ınızı güvenliğini sağlamak için seçenekleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="56097-105">This article describes the options for securing your IoT hub.</span></span> <span data-ttu-id="56097-106">IOT hub'ı kullanan *izinleri* her IOT hub uç erişim vermek için.</span><span class="sxs-lookup"><span data-stu-id="56097-106">IoT Hub uses *permissions* to grant access to each IoT hub endpoint.</span></span> <span data-ttu-id="56097-107">İzinleri işlevselliğine dayalı bir IOT hub'ına erişimi sınırlayın.</span><span class="sxs-lookup"><span data-stu-id="56097-107">Permissions limit the access to an IoT hub based on functionality.</span></span>

<span data-ttu-id="56097-108">Bu makalede açıklanır:</span><span class="sxs-lookup"><span data-stu-id="56097-108">This article describes:</span></span>

* <span data-ttu-id="56097-109">IOT hub'ınızı erişmek için bir aygıt veya arka uç uygulaması için erişim izni verebilir farklı izinler.</span><span class="sxs-lookup"><span data-stu-id="56097-109">The different permissions that you can grant to a device or back-end app to access your IoT hub.</span></span>
* <span data-ttu-id="56097-110">Kimlik doğrulama işlemi ve belirteçleri izinleri doğrulamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="56097-110">The authentication process and the tokens it uses to verify permissions.</span></span>
* <span data-ttu-id="56097-111">Belirli kaynaklara erişimi sınırlamak için kimlik bilgilerini kapsam yapma.</span><span class="sxs-lookup"><span data-stu-id="56097-111">How to scope credentials to limit access to specific resources.</span></span>
* <span data-ttu-id="56097-112">X.509 sertifikaları IOT hub'ı destekler.</span><span class="sxs-lookup"><span data-stu-id="56097-112">IoT Hub support for X.509 certificates.</span></span>
* <span data-ttu-id="56097-113">Var olan cihaz kimlik kayıt defterleri veya kimlik doğrulama şemasını kullanan özel cihaz kimlik doğrulama mekanizmaları.</span><span class="sxs-lookup"><span data-stu-id="56097-113">Custom device authentication mechanisms that use existing device identity registries or authentication schemes.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="56097-114">Kullanılması gereken durumlar</span><span class="sxs-lookup"><span data-stu-id="56097-114">When to use</span></span>

<span data-ttu-id="56097-115">IOT Hub uç noktaları hiçbirini erişmek için uygun izinlere sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="56097-115">You must have appropriate permissions to access any of the IoT Hub endpoints.</span></span> <span data-ttu-id="56097-116">Örneğin, bir cihaz IOT Hub'ına gönderir her ileti yanı sıra güvenlik kimlik bilgileri içeren bir belirteç eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="56097-116">For example, a device must include a token containing security credentials along with every message it sends to IoT Hub.</span></span>

## <a name="access-control-and-permissions"></a><span data-ttu-id="56097-117">Erişim denetimi ve izinleri</span><span class="sxs-lookup"><span data-stu-id="56097-117">Access control and permissions</span></span>

<span data-ttu-id="56097-118">Erişim izni verebilir [izinleri](#iot-hub-permissions) aşağıdaki yollarla:</span><span class="sxs-lookup"><span data-stu-id="56097-118">You can grant [permissions](#iot-hub-permissions) in the following ways:</span></span>

* <span data-ttu-id="56097-119">**IOT hub düzeyi paylaşılan erişim ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="56097-119">**IoT hub-level shared access policies**.</span></span> <span data-ttu-id="56097-120">Paylaşılan erişim ilkeleri, herhangi bir birleşimini vermek [izinleri](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="56097-120">Shared access policies can grant any combination of [permissions](#iot-hub-permissions).</span></span> <span data-ttu-id="56097-121">İlkeleri tanımlayabilirsiniz [Azure portal][lnk-management-portal], veya program aracılığıyla kullanarak [IOT hub'ı kaynak sağlayıcısı REST API'leri][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="56097-121">You can define policies in the [Azure portal][lnk-management-portal], or programmatically by using the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="56097-122">Yeni oluşturulan bir IOT hub aşağıdaki varsayılan ilkeleri vardır:</span><span class="sxs-lookup"><span data-stu-id="56097-122">A newly created IoT hub has the following default policies:</span></span>

  * <span data-ttu-id="56097-123">**iothubowner**: tüm izinleri ilkesiyle.</span><span class="sxs-lookup"><span data-stu-id="56097-123">**iothubowner**: Policy with all permissions.</span></span>
  * <span data-ttu-id="56097-124">**Hizmet**: ilke ile **ServiceConnect** izni.</span><span class="sxs-lookup"><span data-stu-id="56097-124">**service**: Policy with **ServiceConnect** permission.</span></span>
  * <span data-ttu-id="56097-125">**Aygıt**: ilke ile **DeviceConnect** izni.</span><span class="sxs-lookup"><span data-stu-id="56097-125">**device**: Policy with **DeviceConnect** permission.</span></span>
  * <span data-ttu-id="56097-126">**registryRead**: ilke ile **RegistryRead** izni.</span><span class="sxs-lookup"><span data-stu-id="56097-126">**registryRead**: Policy with **RegistryRead** permission.</span></span>
  * <span data-ttu-id="56097-127">**registryReadWrite**: ilke ile **RegistryRead** ve RegistryWrite izinleri.</span><span class="sxs-lookup"><span data-stu-id="56097-127">**registryReadWrite**: Policy with **RegistryRead** and RegistryWrite permissions.</span></span>
  * <span data-ttu-id="56097-128">**Cihaz başına güvenlik kimlik bilgileri**.</span><span class="sxs-lookup"><span data-stu-id="56097-128">**Per-device security credentials**.</span></span> <span data-ttu-id="56097-129">Her IOT hub'ı içeren bir [kimlik kayıt defteri][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="56097-129">Each IoT Hub contains an [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="56097-130">Bu kimlik kayıt defterinde her cihaz için vermek güvenlik kimlik bilgileri yapılandırabilirsiniz **DeviceConnect** karşılık gelen cihaz Uç noktalara kapsamlı izinleri.</span><span class="sxs-lookup"><span data-stu-id="56097-130">For each device in this identity registry, you can configure security credentials that grant **DeviceConnect** permissions scoped to the corresponding device endpoints.</span></span>

<span data-ttu-id="56097-131">Örneğin, tipik bir IOT çözüm içinde:</span><span class="sxs-lookup"><span data-stu-id="56097-131">For example, in a typical IoT solution:</span></span>

* <span data-ttu-id="56097-132">Aygıt Yönetimi bileşeni kullanır *registryReadWrite* ilkesi.</span><span class="sxs-lookup"><span data-stu-id="56097-132">The device management component uses the *registryReadWrite* policy.</span></span>
* <span data-ttu-id="56097-133">Olay işlemcisi bileşeni kullanır *hizmet* ilkesi.</span><span class="sxs-lookup"><span data-stu-id="56097-133">The event processor component uses the *service* policy.</span></span>
* <span data-ttu-id="56097-134">Çalışma zamanı aygıt iş mantığı bileşeni kullanır *hizmet* ilkesi.</span><span class="sxs-lookup"><span data-stu-id="56097-134">The run-time device business logic component uses the *service* policy.</span></span>
* <span data-ttu-id="56097-135">Tek bir cihazı IOT hub'ın kimlik kayıt defterinde depolanan kimlik bilgilerini kullanarak bağlanın.</span><span class="sxs-lookup"><span data-stu-id="56097-135">Individual devices connect using credentials stored in the IoT hub's identity registry.</span></span>

> [!NOTE]
> <span data-ttu-id="56097-136">Bkz: [izinleri](#iot-hub-permissions) ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="56097-136">See [permissions](#iot-hub-permissions) for detailed information.</span></span>

## <a name="authentication"></a><span data-ttu-id="56097-137">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="56097-137">Authentication</span></span>

<span data-ttu-id="56097-138">Azure IOT Hub kimlik kayıt defteri güvenlik kimlik bilgileri ve paylaşılan erişim ilkeleri karşı bir belirteç doğrulayarak uç noktaları erişim verir.</span><span class="sxs-lookup"><span data-stu-id="56097-138">Azure IoT Hub grants access to endpoints by verifying a token against the shared access policies and identity registry security credentials.</span></span>

<span data-ttu-id="56097-139">Simetrik anahtarlar gibi güvenlik kimlik bilgileri hiçbir zaman kablo üzerinden gönderilir.</span><span class="sxs-lookup"><span data-stu-id="56097-139">Security credentials, such as symmetric keys, are never sent over the wire.</span></span>

> [!NOTE]
> <span data-ttu-id="56097-140">Tüm sağlayıcıları olarak Azure IOT Hub kaynak sağlayıcısı, Azure aboneliğinizin güvenli [Azure Resource Manager][lnk-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="56097-140">The Azure IoT Hub resource provider is secured through your Azure subscription, as are all providers in the [Azure Resource Manager][lnk-azure-resource-manager].</span></span>

<span data-ttu-id="56097-141">Güvenlik belirteçleri oluşturmak ve nasıl kullanılacağını hakkında daha fazla bilgi için bkz: [IOT hub'ı güvenlik belirteçleri][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="56097-141">For more information about how to construct and use security tokens, see [IoT Hub security tokens][lnk-sas-tokens].</span></span>

### <a name="protocol-specifics"></a><span data-ttu-id="56097-142">Protokol özellikleri</span><span class="sxs-lookup"><span data-stu-id="56097-142">Protocol specifics</span></span>

<span data-ttu-id="56097-143">Desteklenen her protokolü, MQTT, AMQP ve HTTP gibi farklı yollarla belirteçleri taşımaları.</span><span class="sxs-lookup"><span data-stu-id="56097-143">Each supported protocol, such as MQTT, AMQP, and HTTP, transports tokens in different ways.</span></span>

<span data-ttu-id="56097-144">MQTT kullanırken BAĞLAN paket DeviceID ClientID, {iothubhostname} sahiptir. / {DeviceID} Username alanı ve parola alanına bir SAS belirteci.</span><span class="sxs-lookup"><span data-stu-id="56097-144">When using MQTT, the CONNECT packet has the deviceId as the ClientId, {iothubhostname}/{deviceId} in the Username field, and a SAS token in the Password field.</span></span> <span data-ttu-id="56097-145">{iothubhostname} tam CName IOT hub (örneğin, contoso.azure-devices.net) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="56097-145">{iothubhostname} should be the full CName of the IoT hub (for example, contoso.azure-devices.net).</span></span>

<span data-ttu-id="56097-146">Kullanırken [AMQP][lnk-amqp], IOT hub'ı destekleyen [SASL DÜZ] [ lnk-sasl-plain] ve [AMQP talep tabanlı-güvenlik] [ lnk-cbs].</span><span class="sxs-lookup"><span data-stu-id="56097-146">When using [AMQP][lnk-amqp], IoT Hub supports [SASL PLAIN][lnk-sasl-plain] and [AMQP Claims-Based-Security][lnk-cbs].</span></span>

<span data-ttu-id="56097-147">AMQP talep tabanlı-güvenlik kullanırsanız, bu belirteçleri iletmek nasıl standart belirtir.</span><span class="sxs-lookup"><span data-stu-id="56097-147">If you use AMQP claims-based-security, the standard specifies how to transmit these tokens.</span></span>

<span data-ttu-id="56097-148">SASL DÜZ için **kullanıcıadı** olabilir:</span><span class="sxs-lookup"><span data-stu-id="56097-148">For SASL PLAIN, the **username** can be:</span></span>

* <span data-ttu-id="56097-149">`{policyName}@sas.root.{iothubName}`IOT hub düzeyindeki belirteçleri kullanıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="56097-149">`{policyName}@sas.root.{iothubName}` if using IoT hub-level tokens.</span></span>
* <span data-ttu-id="56097-150">`{deviceId}@sas.{iothubname}`cihaz kapsamlı belirteçleri kullanıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="56097-150">`{deviceId}@sas.{iothubname}` if using device-scoped tokens.</span></span>

<span data-ttu-id="56097-151">Parola alanı belirteci açıklandığı gibi her iki durumda da içeren [IOT hub'ı güvenlik belirteçleri][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="56097-151">In both cases, the password field contains the token, as described in [IoT Hub security tokens][lnk-sas-tokens].</span></span>

<span data-ttu-id="56097-152">HTTP kimlik doğrulaması geçerli bir belirteç içine ekleyerek uygulayan **yetkilendirme** istek üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="56097-152">HTTP implements authentication by including a valid token in the **Authorization** request header.</span></span>

#### <a name="example"></a><span data-ttu-id="56097-153">Örnek</span><span class="sxs-lookup"><span data-stu-id="56097-153">Example</span></span>

<span data-ttu-id="56097-154">Kullanıcı adı (DeviceID büyük küçük harfe duyarlı):`iothubname.azure-devices.net/DeviceId`</span><span class="sxs-lookup"><span data-stu-id="56097-154">Username (DeviceId is case-sensitive): `iothubname.azure-devices.net/DeviceId`</span></span>

<span data-ttu-id="56097-155">Parola (oluşturmak SAS belirteci ile [aygıt explorer] [ lnk-device-explorer] aracı):`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span><span class="sxs-lookup"><span data-stu-id="56097-155">Password (Generate SAS token with the [device explorer][lnk-device-explorer] tool): `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span></span>

> [!NOTE]
> <span data-ttu-id="56097-156">[Azure IOT SDK'ları] [ lnk-sdks] belirteçleri hizmete bağlanmada olduğunda otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="56097-156">The [Azure IoT SDKs][lnk-sdks] automatically generate tokens when connecting to the service.</span></span> <span data-ttu-id="56097-157">Bazı durumlarda, tüm protokoller veya tüm kimlik doğrulama yöntemleri Azure IOT SDK'ları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="56097-157">In some cases, the Azure IoT SDKs do not support all the protocols or all the authentication methods.</span></span>

### <a name="special-considerations-for-sasl-plain"></a><span data-ttu-id="56097-158">SASL DÜZ için özel hususlar</span><span class="sxs-lookup"><span data-stu-id="56097-158">Special considerations for SASL PLAIN</span></span>

<span data-ttu-id="56097-159">SASL DÜZ AMQP ile kullanırken, bir IOT hub'ına bağlanan bir istemci her TCP bağlantısı için tek bir belirteci kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56097-159">When using SASL PLAIN with AMQP, a client connecting to an IoT hub can use a single token for each TCP connection.</span></span> <span data-ttu-id="56097-160">Belirtecin süresi dolduğunda, TCP bağlantısı hizmet bağlantısını keser ve bir reconnect tetikler.</span><span class="sxs-lookup"><span data-stu-id="56097-160">When the token expires, the TCP connection disconnects from the service and triggers a reconnect.</span></span> <span data-ttu-id="56097-161">Bu davranış değil sorunlu sırada bir arka uç uygulaması için bir cihaz uygulaması için aşağıdaki nedenlerle zarar:</span><span class="sxs-lookup"><span data-stu-id="56097-161">This behavior, while not problematic for a back-end app, is damaging for a device app for the following reasons:</span></span>

* <span data-ttu-id="56097-162">Ağ geçidi genellikle birçok aygıtlar adına bağlayın.</span><span class="sxs-lookup"><span data-stu-id="56097-162">Gateways usually connect on behalf of many devices.</span></span> <span data-ttu-id="56097-163">SASL DÜZ kullanırken, bunlar bir IOT hub'ına bağlanan her aygıt için ayrı bir TCP bağlantı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="56097-163">When using SASL PLAIN, they have to create a distinct TCP connection for each device connecting to an IoT hub.</span></span> <span data-ttu-id="56097-164">Bu senaryoda önemli ölçüde güç ve ağ kaynakları tüketiminin artırır ve her cihaz bağlantı gecikmesi artırır.</span><span class="sxs-lookup"><span data-stu-id="56097-164">This scenario considerably increases the consumption of power and networking resources, and increases the latency of each device connection.</span></span>
* <span data-ttu-id="56097-165">Kaynak kısıtlı cihazları olumsuz her belirteç süresi dolduktan sonra yeniden bağlanmayı kaynak kullanımının yüksek etkilenir.</span><span class="sxs-lookup"><span data-stu-id="56097-165">Resource-constrained devices are adversely affected by the increased use of resources to reconnect after each token expiration.</span></span>

## <a name="scope-iot-hub-level-credentials"></a><span data-ttu-id="56097-166">Kapsam IOT hub düzeyindeki kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="56097-166">Scope IoT hub-level credentials</span></span>

<span data-ttu-id="56097-167">Sınırlı kaynak URI'si ile belirteçleri oluşturarak IOT hub'ı düzeyinde güvenlik ilkelerinin kapsamını belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56097-167">You can scope IoT hub-level security policies by creating tokens with a restricted resource URI.</span></span> <span data-ttu-id="56097-168">Örneğin, bir CİHAZDAN cihaz bulut iletilerini göndermek için uç nokta **/devices/ {DeviceID} / iletileri/olayları**.</span><span class="sxs-lookup"><span data-stu-id="56097-168">For example, the endpoint to send device-to-cloud messages from a device is **/devices/{deviceId}/messages/events**.</span></span> <span data-ttu-id="56097-169">Bir IOT hub düzeyindeki paylaşılan erişim ilkesi ile de kullanabileceğiniz **DeviceConnect** , resourceURI olan bir belirteç imzalamak için izinleri **/devices/ {DeviceID}**.</span><span class="sxs-lookup"><span data-stu-id="56097-169">You can also use an IoT hub-level shared access policy with **DeviceConnect** permissions to sign a token whose resourceURI is **/devices/{deviceId}**.</span></span> <span data-ttu-id="56097-170">Bu yaklaşım, yalnızca cihaz adına iletileri göndermek için kullanılabilen bir belirteç oluşturur **DeviceID**.</span><span class="sxs-lookup"><span data-stu-id="56097-170">This approach creates a token that is only usable to send messages on behalf of device **deviceId**.</span></span>

<span data-ttu-id="56097-171">Bu mekanizma benzer [olay hub'ları Yayımcı ilkesi][lnk-event-hubs-publisher-policy]ve özel kimlik doğrulama yöntemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="56097-171">This mechanism is similar to the [Event Hubs publisher policy][lnk-event-hubs-publisher-policy], and enables you to implement custom authentication methods.</span></span>

## <a name="security-tokens"></a><span data-ttu-id="56097-172">Güvenlik belirteçleri</span><span class="sxs-lookup"><span data-stu-id="56097-172">Security tokens</span></span>

<span data-ttu-id="56097-173">IOT Hub, aygıtları ve kablo anahtarları göndermekten kaçınmanız Hizmetleri kimlik doğrulaması için güvenlik belirteçlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="56097-173">IoT Hub uses security tokens to authenticate devices and services to avoid sending keys on the wire.</span></span> <span data-ttu-id="56097-174">Ayrıca, güvenlik belirteçlerini geçerlilik tarihi ve kapsam sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="56097-174">Additionally, security tokens are limited in time validity and scope.</span></span> <span data-ttu-id="56097-175">[Azure IOT SDK'ları] [ lnk-sdks] otomatik olarak özel bir yapılandırma gerektirmeden belirteçleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="56097-175">[Azure IoT SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span></span> <span data-ttu-id="56097-176">Bazı senaryolar oluşturmak ve güvenlik belirteçlerini doğrudan kullanmanızı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="56097-176">Some scenarios do require you to generate and use security tokens directly.</span></span> <span data-ttu-id="56097-177">Bu tür senaryoları şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="56097-177">Such scenarios include:</span></span>

* <span data-ttu-id="56097-178">MQTT, AMQP veya HTTP yüzeyleri doğrudan kullanın.</span><span class="sxs-lookup"><span data-stu-id="56097-178">The direct use of the MQTT, AMQP, or HTTP surfaces.</span></span>
* <span data-ttu-id="56097-179">Açıklandığı gibi belirteci hizmeti düzeni uyarlamasını [özel cihaz kimlik doğrulamasını][lnk-custom-auth].</span><span class="sxs-lookup"><span data-stu-id="56097-179">The implementation of the token service pattern, as explained in [Custom device authentication][lnk-custom-auth].</span></span>

<span data-ttu-id="56097-180">IOT Hub ayrıca kullanarak IOT Hub ile kimlik doğrulaması cihazları sağlar [X.509 sertifikalarını][lnk-x509].</span><span class="sxs-lookup"><span data-stu-id="56097-180">IoT Hub also allows devices to authenticate with IoT Hub using [X.509 certificates][lnk-x509].</span></span>

### <a name="security-token-structure"></a><span data-ttu-id="56097-181">Güvenlik belirteci yapısı</span><span class="sxs-lookup"><span data-stu-id="56097-181">Security token structure</span></span>

<span data-ttu-id="56097-182">Cihazlara zaman sınırlı erişim ve IOT Hub'ındaki belirli işlevleri hizmet vermek için güvenlik belirteçleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="56097-182">You use security tokens to grant time-bounded access to devices and services to specific functionality in IoT Hub.</span></span> <span data-ttu-id="56097-183">IOT Hub'ına bağlanmak için yetkilendirme almak için cihazları ve Hizmetleri paylaşılan erişim veya simetrik anahtarı ile imzalanmış güvenlik belirteçleri göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="56097-183">To get authorization to connect to IoT Hub, devices and services must send security tokens signed with either a shared access or symmetric key.</span></span> <span data-ttu-id="56097-184">Bu anahtarlar, kimlik kayıt defterinde bir cihaz kimliği ile depolanır.</span><span class="sxs-lookup"><span data-stu-id="56097-184">These keys are stored with a device identity in the identity registry.</span></span>

<span data-ttu-id="56097-185">Paylaşılan Erişim İlkesi izinleri ile ilişkili tüm işlevlere paylaşılan erişim anahtarı verir erişimi olan bir belirteci imzalayan.</span><span class="sxs-lookup"><span data-stu-id="56097-185">A token signed with a shared access key grants access to all the functionality associated with the shared access policy permissions.</span></span> <span data-ttu-id="56097-186">Bir belirteci imzalayan aygıt kimliğin simetrik anahtar yalnızca verir ile **DeviceConnect** ilişkili cihaz kimliği için izni.</span><span class="sxs-lookup"><span data-stu-id="56097-186">A token signed with a device identity's symmetric key only grants the **DeviceConnect** permission for the associated device identity.</span></span>

<span data-ttu-id="56097-187">Güvenlik belirteci biçimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="56097-187">The security token has the following format:</span></span>

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

<span data-ttu-id="56097-188">Beklenen değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="56097-188">Here are the expected values:</span></span>

| <span data-ttu-id="56097-189">Değer</span><span class="sxs-lookup"><span data-stu-id="56097-189">Value</span></span> | <span data-ttu-id="56097-190">Açıklama</span><span class="sxs-lookup"><span data-stu-id="56097-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="56097-191">{İmza}</span><span class="sxs-lookup"><span data-stu-id="56097-191">{signature}</span></span> |<span data-ttu-id="56097-192">Bir HMAC SHA256 imza dize biçiminde: `{URL-encoded-resourceURI} + "\n" + expiry`.</span><span class="sxs-lookup"><span data-stu-id="56097-192">An HMAC-SHA256 signature string of the form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span></span> <span data-ttu-id="56097-193">**Önemli**: anahtar base64 kodlaması kodunu çözdü ve HMAC SHA256 hesaplama gerçekleştirmek için anahtar olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="56097-193">**Important**: The key is decoded from base64 and used as key to perform the HMAC-SHA256 computation.</span></span> |
| <span data-ttu-id="56097-194">{resourceURI}</span><span class="sxs-lookup"><span data-stu-id="56097-194">{resourceURI}</span></span> |<span data-ttu-id="56097-195">IOT hub'ı (Protokol) ana bilgisayar adı ile başlayarak, bu belirteci ile erişilen uç noktalar için URI öneki (tarafından kesim).</span><span class="sxs-lookup"><span data-stu-id="56097-195">URI prefix (by segment) of the endpoints that can be accessed with this token, starting with host name of the IoT hub (no protocol).</span></span> <span data-ttu-id="56097-196">Örneğin, `myHub.azure-devices.net/devices/device1`</span><span class="sxs-lookup"><span data-stu-id="56097-196">For example, `myHub.azure-devices.net/devices/device1`</span></span> |
| <span data-ttu-id="56097-197">{süre sonu}</span><span class="sxs-lookup"><span data-stu-id="56097-197">{expiry}</span></span> |<span data-ttu-id="56097-198">UTF8 dizeleri dönemi: 00:00:00 UTC üzerinde 1 Ocak 1970'ten beri geçen saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="56097-198">UTF8 strings for number of seconds since the epoch 00:00:00 UTC on 1 January 1970.</span></span> |
| <span data-ttu-id="56097-199">{URL-kodlanmış-resourceURI}</span><span class="sxs-lookup"><span data-stu-id="56097-199">{URL-encoded-resourceURI}</span></span> |<span data-ttu-id="56097-200">Düşük küçük kaynak URI'si için URL kodlaması durumda</span><span class="sxs-lookup"><span data-stu-id="56097-200">Lower case URL-encoding of the lower case resource URI</span></span> |
| <span data-ttu-id="56097-201">{policyName}</span><span class="sxs-lookup"><span data-stu-id="56097-201">{policyName}</span></span> |<span data-ttu-id="56097-202">Bu belirteç başvurduğu paylaşılan erişim ilkesinin adı.</span><span class="sxs-lookup"><span data-stu-id="56097-202">The name of the shared access policy to which this token refers.</span></span> <span data-ttu-id="56097-203">Yüklenmesinden belirteç aygıt kayıt defteri kimlik bilgilerini ifade eder.</span><span class="sxs-lookup"><span data-stu-id="56097-203">Absent if the token refers to device-registry credentials.</span></span> |

<span data-ttu-id="56097-204">**Not önek üzerinde**: URI öneki segmente göre ve karakter tarafından hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="56097-204">**Note on prefix**: The URI prefix is computed by segment and not by character.</span></span> <span data-ttu-id="56097-205">Örneğin `/a/b` için bir önek `/a/b/c` ancak için `/a/bc`.</span><span class="sxs-lookup"><span data-stu-id="56097-205">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span></span>

<span data-ttu-id="56097-206">Aşağıdaki Node.js parçacığını adlı bir işlev gösterir **generateSasToken** girişleri belirtecinden hesaplar `resourceUri, signingKey, policyName, expiresInMins`.</span><span class="sxs-lookup"><span data-stu-id="56097-206">The following Node.js snippet shows a function called **generateSasToken** that computes the token from the inputs `resourceUri, signingKey, policyName, expiresInMins`.</span></span> <span data-ttu-id="56097-207">Sonraki bölümlerde farklı belirteci kullanım örnekleri için farklı girişleri başlatmak nasıl ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="56097-207">The next sections detail how to initialize the different inputs for the different token use cases.</span></span>

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

<span data-ttu-id="56097-208">Bir karşılaştırma bir güvenlik belirteci üretmek için eşdeğer Python kodu verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="56097-208">As a comparison, the equivalent Python code to generate a security token is:</span></span>

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
> <span data-ttu-id="56097-209">Belirtecin süresi geçerliliğini IOT hub'ı makinelerde doğrulanır beri belirteci oluşturur makine saatinde kayması en az olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="56097-209">Since the time validity of the token is validated on IoT Hub machines, the drift on the clock of the machine that generates the token must be minimal.</span></span>

### <a name="use-sas-tokens-in-a-device-app"></a><span data-ttu-id="56097-210">SAS belirteci bir aygıt uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="56097-210">Use SAS tokens in a device app</span></span>

<span data-ttu-id="56097-211">Almak için iki yolla **DeviceConnect** güvenlik belirteçleri IOT Hub ile izinlerle: kullanın bir [simetrik cihaz kimlik kayıt defteri anahtarından](#use-a-symmetric-key-in-the-identity-registry), veya bir [paylaşılan erişim anahtarı](#use-a-shared-access-policy).</span><span class="sxs-lookup"><span data-stu-id="56097-211">There are two ways to obtain **DeviceConnect** permissions with IoT Hub with security tokens: use a [symmetric device key from the identity registry](#use-a-symmetric-key-in-the-identity-registry), or use a [shared access key](#use-a-shared-access-policy).</span></span>

<span data-ttu-id="56097-212">Tüm işlevlere aygıtlardan erişilebilir önekiyle uç noktalarda tasarıma göre sunulur unutmayın `/devices/{deviceId}`.</span><span class="sxs-lookup"><span data-stu-id="56097-212">Remember that all functionality accessible from devices is exposed by design on endpoints with prefix `/devices/{deviceId}`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56097-213">IOT hub'ı belirli bir aygıtın kimliğini doğrulayan tek yolu cihazı kimlik simetrik anahtar kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="56097-213">The only way that IoT Hub authenticates a specific device is using the device identity symmetric key.</span></span> <span data-ttu-id="56097-214">Cihazın işlevselliğini erişmek için bir paylaşılan erişim ilkesi kullanıldığında durumlarda güvenilir bir alt bileşen olarak güvenlik belirteci veren bileşen çözümü dikkate almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="56097-214">In cases when a shared access policy is used to access device functionality, the solution must consider the component issuing the security token as a trusted subcomponent.</span></span>

<span data-ttu-id="56097-215">Aygıt'e yönelik uç noktalar (yedeklemiş Protokolü) şunlardır:</span><span class="sxs-lookup"><span data-stu-id="56097-215">The device-facing endpoints are (irrespective of the protocol):</span></span>

| <span data-ttu-id="56097-216">Uç Nokta</span><span class="sxs-lookup"><span data-stu-id="56097-216">Endpoint</span></span> | <span data-ttu-id="56097-217">İşlev</span><span class="sxs-lookup"><span data-stu-id="56097-217">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |<span data-ttu-id="56097-218">Cihaz-bulut iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="56097-218">Send device-to-cloud messages.</span></span> |
| `{iot hub host name}/devices/{deviceId}/devicebound` |<span data-ttu-id="56097-219">Bulut-cihaz iletilerini alır.</span><span class="sxs-lookup"><span data-stu-id="56097-219">Receive cloud-to-device messages.</span></span> |

### <a name="use-a-symmetric-key-in-the-identity-registry"></a><span data-ttu-id="56097-220">Simetrik anahtar kimlik kayıt defterinde kullanma</span><span class="sxs-lookup"><span data-stu-id="56097-220">Use a symmetric key in the identity registry</span></span>

<span data-ttu-id="56097-221">Bir aygıt kimliğin simetrik anahtar policyName bir belirteç oluşturmak için kullanırken (`skn`) öğesi belirtecin atlanmış.</span><span class="sxs-lookup"><span data-stu-id="56097-221">When using a device identity's symmetric key to generate a token, the policyName (`skn`) element of the token is omitted.</span></span>

<span data-ttu-id="56097-222">Örneğin, tüm cihaz işlevlerini erişmek için oluşturulan bir belirteç aşağıdaki parametreleri içermelidir:</span><span class="sxs-lookup"><span data-stu-id="56097-222">For example, a token created to access all device functionality should have the following parameters:</span></span>

* <span data-ttu-id="56097-223">Kaynak URI'si: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="56097-223">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="56097-224">imzalama anahtarı: herhangi bir simetrik anahtar için `{device id}` kimliği</span><span class="sxs-lookup"><span data-stu-id="56097-224">signing key: any symmetric key for the `{device id}` identity,</span></span>
* <span data-ttu-id="56097-225">hiçbir ilke adı</span><span class="sxs-lookup"><span data-stu-id="56097-225">no policy name,</span></span>
* <span data-ttu-id="56097-226">Tüm süre sonu zamanı.</span><span class="sxs-lookup"><span data-stu-id="56097-226">any expiration time.</span></span>

<span data-ttu-id="56097-227">Önceki Node.js işlevini kullanarak bir örnek olabilir:</span><span class="sxs-lookup"><span data-stu-id="56097-227">An example using the preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

<span data-ttu-id="56097-228">Device1 tüm işlevlere erişimi verir, sonuç şöyle olacaktır:</span><span class="sxs-lookup"><span data-stu-id="56097-228">The result, which grants access to all functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> <span data-ttu-id="56097-229">.NET kullanarak bir SAS belirteci oluşturmak mümkündür [aygıt explorer] [ lnk-device-explorer] aracını veya platformlar arası, düğüm tabanlı [iothub-explorer] [ lnk-iothub-explorer]komut satırı yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="56097-229">It is possible to generate a SAS token using the .NET [device explorer][lnk-device-explorer] tool or the cross-platform, node-based [iothub-explorer][lnk-iothub-explorer] command-line utility.</span></span>

### <a name="use-a-shared-access-policy"></a><span data-ttu-id="56097-230">Bir paylaşılan erişim ilkesi kullanın</span><span class="sxs-lookup"><span data-stu-id="56097-230">Use a shared access policy</span></span>

<span data-ttu-id="56097-231">Paylaşılan Erişim İlkesi tarafından bir belirteç oluşturduğunuzda `skn` ilkesinin adı alanı.</span><span class="sxs-lookup"><span data-stu-id="56097-231">When you create a token from a shared access policy, set the `skn` field to the name of the policy.</span></span> <span data-ttu-id="56097-232">Bu ilke vermelidir **DeviceConnect** izni.</span><span class="sxs-lookup"><span data-stu-id="56097-232">This policy must grant the **DeviceConnect** permission.</span></span>

<span data-ttu-id="56097-233">Cihazın işlevselliğini erişmek için paylaşılan erişim ilkeleri kullanarak için iki ana senaryo şunlardır:</span><span class="sxs-lookup"><span data-stu-id="56097-233">The two main scenarios for using shared access policies to access device functionality are:</span></span>

* <span data-ttu-id="56097-234">[protokol ağ geçidi bulut][lnk-endpoints],</span><span class="sxs-lookup"><span data-stu-id="56097-234">[cloud protocol gateways][lnk-endpoints],</span></span>
* <span data-ttu-id="56097-235">[simge Hizmetleri] [ lnk-custom-auth] özel kimlik doğrulama şemasını gerçekleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="56097-235">[token services][lnk-custom-auth] used to implement custom authentication schemes.</span></span>

<span data-ttu-id="56097-236">Paylaşılan Erişim İlkesi potansiyel herhangi bir aygıt bağlanmak için erişim izni verebilir, doğru kaynak URI'si güvenlik belirteçleri oluşturmak kullanmak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="56097-236">Since the shared access policy can potentially grant access to connect as any device, it is important to use the correct resource URI when creating security tokens.</span></span> <span data-ttu-id="56097-237">Bu ayar, kaynak URI'si kullanarak belirli bir cihaza belirteci kapsam zorunda belirteci Hizmetleri için özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="56097-237">This setting is especially important for token services, which have to scope the token to a specific device using the resource URI.</span></span> <span data-ttu-id="56097-238">Bu zaten tüm aygıtlar için trafiği eşlemlerse protokolü ağ geçitleri için daha az ilgili noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="56097-238">This point is less relevant for protocol gateways as they are already mediating traffic for all devices.</span></span>

<span data-ttu-id="56097-239">Örnek olarak, önceden oluşturulmuş kullanarak bir belirteç hizmet paylaşılan erişim ilkesi adlı **aygıt** aşağıdaki parametrelerle bir belirteç oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="56097-239">As an example, a token service using the pre-created shared access policy called **device** would create a token with the following parameters:</span></span>

* <span data-ttu-id="56097-240">Kaynak URI'si: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="56097-240">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="56097-241">imzalama anahtarı: anahtarlarını birini `device` İlkesi</span><span class="sxs-lookup"><span data-stu-id="56097-241">signing key: one of the keys of the `device` policy,</span></span>
* <span data-ttu-id="56097-242">İlke adı: `device`,</span><span class="sxs-lookup"><span data-stu-id="56097-242">policy name: `device`,</span></span>
* <span data-ttu-id="56097-243">Tüm süre sonu zamanı.</span><span class="sxs-lookup"><span data-stu-id="56097-243">any expiration time.</span></span>

<span data-ttu-id="56097-244">Önceki Node.js işlevini kullanarak bir örnek olabilir:</span><span class="sxs-lookup"><span data-stu-id="56097-244">An example using the preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="56097-245">Device1 tüm işlevlere erişimi verir, sonuç şöyle olacaktır:</span><span class="sxs-lookup"><span data-stu-id="56097-245">The result, which grants access to all functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

<span data-ttu-id="56097-246">Bir protokol ağ geçidi yalnızca kaynak URI'si ayarı tüm aygıtlar için aynı belirteci kullanabilirsiniz için `myhub.azure-devices.net/devices`.</span><span class="sxs-lookup"><span data-stu-id="56097-246">A protocol gateway could use the same token for all devices simply setting the resource URI to `myhub.azure-devices.net/devices`.</span></span>

### <a name="use-security-tokens-from-service-components"></a><span data-ttu-id="56097-247">Hizmet bileşenleri gelen güvenlik belirteçleri kullanın</span><span class="sxs-lookup"><span data-stu-id="56097-247">Use security tokens from service components</span></span>

<span data-ttu-id="56097-248">Hizmet bileşenleri, yalnızca daha önce açıklandığı gibi uygun izinleri verme paylaşılan erişim ilkeleri kullanan güvenlik belirteçleri üretebilir.</span><span class="sxs-lookup"><span data-stu-id="56097-248">Service components can only generate security tokens using shared access policies granting the appropriate permissions as explained previously.</span></span>

<span data-ttu-id="56097-249">Bitiş noktasında kullanıma sunulan hizmet işlevleri şöyledir:</span><span class="sxs-lookup"><span data-stu-id="56097-249">Here is the service functions exposed on the endpoints:</span></span>

| <span data-ttu-id="56097-250">Uç Nokta</span><span class="sxs-lookup"><span data-stu-id="56097-250">Endpoint</span></span> | <span data-ttu-id="56097-251">İşlev</span><span class="sxs-lookup"><span data-stu-id="56097-251">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices` |<span data-ttu-id="56097-252">Oluştur, Güncelleştir, alabilir ve cihaz kimliklerini silebilir.</span><span class="sxs-lookup"><span data-stu-id="56097-252">Create, update, retrieve, and delete device identities.</span></span> |
| `{iot hub host name}/messages/events` |<span data-ttu-id="56097-253">Cihaz bulut iletilerini alır.</span><span class="sxs-lookup"><span data-stu-id="56097-253">Receive device-to-cloud messages.</span></span> |
| `{iot hub host name}/servicebound/feedback` |<span data-ttu-id="56097-254">Bulut-cihaz iletilerini için bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="56097-254">Receive feedback for cloud-to-device messages.</span></span> |
| `{iot hub host name}/devicebound` |<span data-ttu-id="56097-255">Bulut cihaz iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="56097-255">Send cloud-to-device messages.</span></span> |

<span data-ttu-id="56097-256">Örnek olarak, önceden oluşturulmuş kullanarak bir hizmet oluşturma adlı erişim ilkesi paylaşılan **registryRead** aşağıdaki parametrelerle bir belirteç oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="56097-256">As an example, a service generating using the pre-created shared access policy called **registryRead** would create a token with the following parameters:</span></span>

* <span data-ttu-id="56097-257">Kaynak URI'si: `{IoT hub name}.azure-devices.net/devices`,</span><span class="sxs-lookup"><span data-stu-id="56097-257">resource URI: `{IoT hub name}.azure-devices.net/devices`,</span></span>
* <span data-ttu-id="56097-258">imzalama anahtarı: anahtarlarını birini `registryRead` İlkesi</span><span class="sxs-lookup"><span data-stu-id="56097-258">signing key: one of the keys of the `registryRead` policy,</span></span>
* <span data-ttu-id="56097-259">İlke adı: `registryRead`,</span><span class="sxs-lookup"><span data-stu-id="56097-259">policy name: `registryRead`,</span></span>
* <span data-ttu-id="56097-260">Tüm süre sonu zamanı.</span><span class="sxs-lookup"><span data-stu-id="56097-260">any expiration time.</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="56097-261">Tüm aygıt kimlikleri okuma erişimi vermeniz, sonuç şöyle olacaktır:</span><span class="sxs-lookup"><span data-stu-id="56097-261">The result, which would grant access to read all device identities, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a><span data-ttu-id="56097-262">Desteklenen X.509 sertifikaları</span><span class="sxs-lookup"><span data-stu-id="56097-262">Supported X.509 certificates</span></span>

<span data-ttu-id="56097-263">Bir cihaz IOT Hub ile kimlik doğrulaması için herhangi bir X.509 sertifika kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56097-263">You can use any X.509 certificate to authenticate a device with IoT Hub.</span></span> <span data-ttu-id="56097-264">Sertifikaları dahil et:</span><span class="sxs-lookup"><span data-stu-id="56097-264">Certificates include:</span></span>

* <span data-ttu-id="56097-265">**Varolan bir X.509 sertifikası**.</span><span class="sxs-lookup"><span data-stu-id="56097-265">**An existing X.509 certificate**.</span></span> <span data-ttu-id="56097-266">Bir aygıt zaten kendisiyle ilişkilendirilmiş bir X.509 sertifikası olabilir.</span><span class="sxs-lookup"><span data-stu-id="56097-266">A device may already have an X.509 certificate associated with it.</span></span> <span data-ttu-id="56097-267">Cihaz IOT Hub ile kimlik doğrulaması için bu sertifikayı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56097-267">The device can use this certificate to authenticate with IoT Hub.</span></span>
* <span data-ttu-id="56097-268">**A otomatik olarak oluşturulan ve X-509 Sertifika'otomatik olarak imzalanan**.</span><span class="sxs-lookup"><span data-stu-id="56097-268">**A self-generated and self-signed X-509 certificate**.</span></span> <span data-ttu-id="56097-269">Bir aygıt üreticisi veya şirket içi dağıtıcı, bu sertifikalar oluşturmak ve karşılık gelen özel anahtar (ve sertifika) cihazda depolamak.</span><span class="sxs-lookup"><span data-stu-id="56097-269">A device manufacturer or in-house deployer can generate these certificates and store the corresponding private key (and certificate) on the device.</span></span> <span data-ttu-id="56097-270">Araçları gibi kullanabilir [OpenSSL] [ lnk-openssl] ve [Windows SelfSignedCertificate] [ lnk-selfsigned] bu amaç için yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="56097-270">You can use tools such as [OpenSSL][lnk-openssl] and [Windows SelfSignedCertificate][lnk-selfsigned] utility for this purpose.</span></span>
* <span data-ttu-id="56097-271">**X.509 sertifikası CA tarafından imzalanmış**.</span><span class="sxs-lookup"><span data-stu-id="56097-271">**CA-signed X.509 certificate**.</span></span> <span data-ttu-id="56097-272">Bir aygıtı belirlemek ve IOT Hub ile kimlik doğrulaması için oluşturulan ve bir sertifika yetkilisi (CA) tarafından imzalanmış bir X.509 sertifikası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56097-272">To identify a device and authenticate it with IoT Hub, you can use an X.509 certificate generated and signed by a Certification Authority (CA).</span></span> <span data-ttu-id="56097-273">IOT hub'ı yalnızca sunulan parmak izi yapılandırılmış parmak iziyle eşleştiğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="56097-273">IoT Hub only verifies that the thumbprint presented matches the configured thumbprint.</span></span> <span data-ttu-id="56097-274">Iothub sertifika zinciri doğrulamaz.</span><span class="sxs-lookup"><span data-stu-id="56097-274">IotHub does not validate the certificate chain.</span></span>

<span data-ttu-id="56097-275">Bir aygıt ya da bir X.509 sertifikası veya bir güvenlik belirteci kimlik doğrulaması, ancak ikisini için kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="56097-275">A device may either use an X.509 certificate or a security token for authentication, but not both.</span></span>

### <a name="register-an-x509-certificate-for-a-device"></a><span data-ttu-id="56097-276">Bir aygıt bir X.509 sertifikası Kaydet</span><span class="sxs-lookup"><span data-stu-id="56097-276">Register an X.509 certificate for a device</span></span>

<span data-ttu-id="56097-277">[Azure IOT hizmeti SDK'sı için C#] [ lnk-service-sdk] (sürüm 1.0.8+) destekleyen bir X.509 sertifikası için kimlik doğrulaması kullanan bir cihazı kaydetme.</span><span class="sxs-lookup"><span data-stu-id="56097-277">The [Azure IoT Service SDK for C#][lnk-service-sdk] (version 1.0.8+) supports registering a device that uses an X.509 certificate for authentication.</span></span> <span data-ttu-id="56097-278">İçeri/dışarı aktarma aygıtların gibi diğer API'leri X.509 sertifikalarını da destekler.</span><span class="sxs-lookup"><span data-stu-id="56097-278">Other APIs such as import/export of devices also support X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="56097-279">C\# desteği</span><span class="sxs-lookup"><span data-stu-id="56097-279">C\# Support</span></span>

<span data-ttu-id="56097-280">**RegistryManager** sınıfı bir cihazı kaydetmek için programlı bir yolunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="56097-280">The **RegistryManager** class provides a programmatic way to register a device.</span></span> <span data-ttu-id="56097-281">Özellikle, **AddDeviceAsync** ve **UpdateDeviceAsync** yöntemleri kaydetmek ve bir cihaz IOT Hub kimlik kayıt defterinde güncelleştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="56097-281">In particular, the **AddDeviceAsync** and **UpdateDeviceAsync** methods enable you to register and update a device in the IoT Hub identity registry.</span></span> <span data-ttu-id="56097-282">Bu iki yöntem ele bir **aygıt** örnek giriş olarak.</span><span class="sxs-lookup"><span data-stu-id="56097-282">These two methods take a **Device** instance as input.</span></span> <span data-ttu-id="56097-283">**Aygıt** sınıfı içeren bir **kimlik doğrulaması** birincil ve ikincil X.509 sertifika parmak izlerini belirtmenize olanak tanır özelliği.</span><span class="sxs-lookup"><span data-stu-id="56097-283">The **Device** class includes an **Authentication** property that allows you to specify primary and secondary X.509 certificate thumbprints.</span></span> <span data-ttu-id="56097-284">Parmak izi SHA-1 karma (DER ikili kodlama kullanılarak depolanır) X.509 sertifikası değerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="56097-284">The thumbprint represents a SHA-1 hash of the X.509 certificate (stored using binary DER encoding).</span></span> <span data-ttu-id="56097-285">Birincil bir parmak izi veya ikincil bir parmak izi veya her ikisini belirtme seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="56097-285">You have the option of specifying a primary thumbprint or a secondary thumbprint or both.</span></span> <span data-ttu-id="56097-286">Birincil ve ikincil parmak izleri sertifika geçiş senaryoları işlemek için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="56097-286">Primary and secondary thumbprints are supported to handle certificate rollover scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="56097-287">IOT hub'ı gerektirmez veya tüm X.509 sertifika parmak izini yalnızca depolar.</span><span class="sxs-lookup"><span data-stu-id="56097-287">IoT Hub does not require or store the entire X.509 certificate, only the thumbprint.</span></span>

<span data-ttu-id="56097-288">Örnek C işte\# kod parçacığını bir X.509 sertifikası kullanarak bir cihazı kaydetmek için:</span><span class="sxs-lookup"><span data-stu-id="56097-288">Here is a sample C\# code snippet to register a device using an X.509 certificate:</span></span>

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

### <a name="use-an-x509-certificate-during-run-time-operations"></a><span data-ttu-id="56097-289">Çalıştırma işlemleri sırasında bir X.509 sertifikası kullanın</span><span class="sxs-lookup"><span data-stu-id="56097-289">Use an X.509 certificate during run-time operations</span></span>

<span data-ttu-id="56097-290">[.NET için Azure IOT cihaz SDK'sı] [ lnk-client-sdk] (sürüm 1.0.11+) X.509 sertifikalarını kullanımını destekler.</span><span class="sxs-lookup"><span data-stu-id="56097-290">The [Azure IoT device SDK for .NET][lnk-client-sdk] (version 1.0.11+) supports the use of X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="56097-291">C\# desteği</span><span class="sxs-lookup"><span data-stu-id="56097-291">C\# Support</span></span>

<span data-ttu-id="56097-292">Sınıf **DeviceAuthenticationWithX509Certificate** oluşturmayı destekler **DeviceClient** X.509 sertifikası kullanarak örnekleri.</span><span class="sxs-lookup"><span data-stu-id="56097-292">The class **DeviceAuthenticationWithX509Certificate** supports the creation of **DeviceClient** instances using an X.509 certificate.</span></span> <span data-ttu-id="56097-293">X.509 sertifikasının özel anahtarı içerir (PKCS #12 olarak da bilinir) PFX biçiminde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="56097-293">The X.509 certificate must be in the PFX (also called PKCS #12) format that includes the private key.</span></span>

<span data-ttu-id="56097-294">Örnek kod parçacığı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="56097-294">Here is a sample code snippet:</span></span>

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a><span data-ttu-id="56097-295">Özel cihaz kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="56097-295">Custom device authentication</span></span>

<span data-ttu-id="56097-296">IOT hub'ı kullanabilirsiniz [kimlik kayıt defteri] [ lnk-identity-registry] cihaz başına güvenlik kimlik bilgilerini yapılandırmak ve denetimini kullanarak erişmek için [belirteçleri][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="56097-296">You can use the IoT Hub [identity registry][lnk-identity-registry] to configure per-device security credentials and access control using [tokens][lnk-sas-tokens].</span></span> <span data-ttu-id="56097-297">Bir IOT çözümündeki bir özel kimlik kayıt defteri ve/veya kimlik doğrulama düzeni zaten varsa, oluşturmayı göz önünde bulundurun bir *belirteç hizmeti* bu altyapı IOT Hub ile tümleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="56097-297">If an IoT solution already has a custom identity registry and/or authentication scheme, consider creating a *token service* to integrate this infrastructure with IoT Hub.</span></span> <span data-ttu-id="56097-298">Bu şekilde, çözümünüz içinde diğer IOT özelliklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56097-298">In this way, you can use other IoT features in your solution.</span></span>

<span data-ttu-id="56097-299">Bir belirteci hizmeti bir özel bulut hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="56097-299">A token service is a custom cloud service.</span></span> <span data-ttu-id="56097-300">IOT hub'ı kullanan *paylaşılan erişim ilkesi* ile **DeviceConnect** oluşturma izni *aygıt kapsamlı* belirteçleri.</span><span class="sxs-lookup"><span data-stu-id="56097-300">It uses an IoT Hub *shared access policy* with **DeviceConnect** permissions to create *device-scoped* tokens.</span></span> <span data-ttu-id="56097-301">Bu belirteçler IOT hub'ınıza bağlanmak bir aygıt etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="56097-301">These tokens enable a device to connect to your IoT hub.</span></span>

![Belirteç Hizmeti deseninin adımları][img-tokenservice]

<span data-ttu-id="56097-303">Belirteç Hizmeti deseninin ana adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="56097-303">Here are the main steps of the token service pattern:</span></span>

1. <span data-ttu-id="56097-304">IOT Hub'ı paylaşılan erişim ilkesi ile oluşturma **DeviceConnect** IOT hub'ınız için izinleri.</span><span class="sxs-lookup"><span data-stu-id="56097-304">Create an IoT Hub shared access policy with **DeviceConnect** permissions for your IoT hub.</span></span> <span data-ttu-id="56097-305">Bu ilkede oluşturabilirsiniz [Azure portal] [ lnk-management-portal] veya program aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="56097-305">You can create this policy in the [Azure portal][lnk-management-portal] or programmatically.</span></span> <span data-ttu-id="56097-306">Belirteç hizmetine bu ilkeyi oluşturduğu Belirteçleri imzalamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="56097-306">The token service uses this policy to sign the tokens it creates.</span></span>
1. <span data-ttu-id="56097-307">Bir cihaz IOT hub'ınızı erişim gerektiğinde, imzalı bir belirteç belirteci Hizmeti'nden ister.</span><span class="sxs-lookup"><span data-stu-id="56097-307">When a device needs to access your IoT hub, it requests a signed token from your token service.</span></span> <span data-ttu-id="56097-308">Cihaz belirteci hizmeti belirteç oluşturmak için kullandığı cihaz kimliğini belirlemek için özel kimlik kayıt defteri/kimlik doğrulama düzeniyle doğrulayabilir.</span><span class="sxs-lookup"><span data-stu-id="56097-308">The device can authenticate with your custom identity registry/authentication scheme to determine the device identity that the token service uses to create the token.</span></span>
1. <span data-ttu-id="56097-309">Belirteç hizmetine bir belirteci döndürür.</span><span class="sxs-lookup"><span data-stu-id="56097-309">The token service returns a token.</span></span> <span data-ttu-id="56097-310">Belirteç kullanılarak oluşturulan `/devices/{deviceId}` olarak `resourceURI`, ile `deviceId` kimlik doğrulaması gerçekleştirilen aygıt olarak.</span><span class="sxs-lookup"><span data-stu-id="56097-310">The token is created by using `/devices/{deviceId}` as `resourceURI`, with `deviceId` as the device being authenticated.</span></span> <span data-ttu-id="56097-311">Belirteç hizmetine paylaşılan erişim ilkesi belirteç oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="56097-311">The token service uses the shared access policy to construct the token.</span></span>
1. <span data-ttu-id="56097-312">Cihaz belirteci doğrudan IOT hub ile kullanır.</span><span class="sxs-lookup"><span data-stu-id="56097-312">The device uses the token directly with the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="56097-313">Bir .NET sınıfını kullanabilirsiniz [SharedAccessSignatureBuilder] [ lnk-dotnet-sas] veya Java sınıfı [IotHubServiceSasToken] [ lnk-java-sas] bir belirteç oluşturmak için Belirteç Hizmeti.</span><span class="sxs-lookup"><span data-stu-id="56097-313">You can use the .NET class [SharedAccessSignatureBuilder][lnk-dotnet-sas] or the Java class [IotHubServiceSasToken][lnk-java-sas] to create a token in your token service.</span></span>

<span data-ttu-id="56097-314">Belirteç hizmetine belirteci süre sonu istendiği gibi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56097-314">The token service can set the token expiration as desired.</span></span> <span data-ttu-id="56097-315">Belirtecin süresi dolduğunda, IOT hub cihaz bağlantısı sunucularının.</span><span class="sxs-lookup"><span data-stu-id="56097-315">When the token expires, the IoT hub severs the device connection.</span></span> <span data-ttu-id="56097-316">Ardından, cihaz belirteci Hizmeti'nden yeni bir belirteç istemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="56097-316">Then, the device must request a new token from the token service.</span></span> <span data-ttu-id="56097-317">Kısa süre sonu zamanı hem cihaz hem de belirteç hizmetine üzerindeki yükü artırır.</span><span class="sxs-lookup"><span data-stu-id="56097-317">A short expiry time increases the load on both the device and the token service.</span></span>

<span data-ttu-id="56097-318">Hub'ınıza bağlanmak bir aygıt için hala onu IOT Hub kimlik kayıt defterine eklemeniz gerekir — cihaz bir belirteç ve aygıt anahtarı bağlanmak için kullanıyor olsa da.</span><span class="sxs-lookup"><span data-stu-id="56097-318">For a device to connect to your hub, you must still add it to the IoT Hub identity registry — even though the device is using a token and not a device key to connect.</span></span> <span data-ttu-id="56097-319">Bu nedenle, etkinleştirme veya cihaz kimliklerini devre dışı bırakarak aygıt başına erişim denetimi kullanmaya devam edebilirsiniz [kimlik kayıt defteri][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="56097-319">Therefore, you can continue to use per-device access control by enabling or disabling device identities in the [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="56097-320">Bu yaklaşım, uzun süre sonu zamanlarında belirteçleri kullanarak riskleri azaltır.</span><span class="sxs-lookup"><span data-stu-id="56097-320">This approach mitigates the risks of using tokens with long expiry times.</span></span>

### <a name="comparison-with-a-custom-gateway"></a><span data-ttu-id="56097-321">Özel bir ağ geçidi ile karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="56097-321">Comparison with a custom gateway</span></span>

<span data-ttu-id="56097-322">Belirteç Hizmeti düzeni, IOT Hub ile bir özel kimlik kayıt defteri/kimlik doğrulaması düzeni uygulamak için önerilen yoludur.</span><span class="sxs-lookup"><span data-stu-id="56097-322">The token service pattern is the recommended way to implement a custom identity registry/authentication scheme with IoT Hub.</span></span> <span data-ttu-id="56097-323">IOT hub'ı çoğu çözüm trafiği işlemeye devam ettiğinden bu deseni önerilir.</span><span class="sxs-lookup"><span data-stu-id="56097-323">This pattern is recommended because IoT Hub continues to handle most of the solution traffic.</span></span> <span data-ttu-id="56097-324">Ancak, özel kimlik doğrulama şeması böylece protokolüyle birbirine, gerektirebilecek bir *özel ağ geçidi* tüm trafiğini işlemek için.</span><span class="sxs-lookup"><span data-stu-id="56097-324">However, if the custom authentication scheme is so intertwined with the protocol, you may require a *custom gateway* to process all the traffic.</span></span> <span data-ttu-id="56097-325">Böyle bir senaryo örneği kullanarak[Aktarım Katmanı Güvenliği (TLS) ve önceden paylaşılan anahtarı (PSKs)][lnk-tls-psk].</span><span class="sxs-lookup"><span data-stu-id="56097-325">An example of such a scenario is using[Transport Layer Security (TLS) and pre-shared keys (PSKs)][lnk-tls-psk].</span></span> <span data-ttu-id="56097-326">Daha fazla bilgi için bkz: [protokol ağ geçidi] [ lnk-protocols] konu.</span><span class="sxs-lookup"><span data-stu-id="56097-326">For more information, see the [protocol gateway][lnk-protocols] topic.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="56097-327">Başvuru konuları:</span><span class="sxs-lookup"><span data-stu-id="56097-327">Reference topics:</span></span>

<span data-ttu-id="56097-328">Aşağıdaki başvuru konuları IOT hub'ınıza erişimini denetleme hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="56097-328">The following reference topics provide you with more information about controlling access to your IoT hub.</span></span>

## <a name="iot-hub-permissions"></a><span data-ttu-id="56097-329">IOT hub'ı izinleri</span><span class="sxs-lookup"><span data-stu-id="56097-329">IoT Hub permissions</span></span>

<span data-ttu-id="56097-330">Aşağıdaki tabloda, IOT hub'ınıza erişimi denetlemek için kullanabileceğiniz izinleri listeler.</span><span class="sxs-lookup"><span data-stu-id="56097-330">The following table lists the permissions you can use to control access to your IoT hub.</span></span>

| <span data-ttu-id="56097-331">İzin</span><span class="sxs-lookup"><span data-stu-id="56097-331">Permission</span></span> | <span data-ttu-id="56097-332">Notlar</span><span class="sxs-lookup"><span data-stu-id="56097-332">Notes</span></span> |
| --- | --- |
| <span data-ttu-id="56097-333">**RegistryRead**</span><span class="sxs-lookup"><span data-stu-id="56097-333">**RegistryRead**</span></span> |<span data-ttu-id="56097-334">Okuma kimlik kayıt defterine erişim verir.</span><span class="sxs-lookup"><span data-stu-id="56097-334">Grants read access to the identity registry.</span></span> <span data-ttu-id="56097-335">Daha fazla bilgi için bkz: [kimlik kayıt defteri][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="56097-335">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="56097-336">Bu izin, arka uç bulut Hizmetleri tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="56097-336">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="56097-337">**RegistryReadWrite**</span><span class="sxs-lookup"><span data-stu-id="56097-337">**RegistryReadWrite**</span></span> |<span data-ttu-id="56097-338">Verir okuma ve yazma erişimi kimlik kayıt defterine.</span><span class="sxs-lookup"><span data-stu-id="56097-338">Grants read and write access to the identity registry.</span></span> <span data-ttu-id="56097-339">Daha fazla bilgi için bkz: [kimlik kayıt defteri][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="56097-339">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="56097-340">Bu izin, arka uç bulut Hizmetleri tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="56097-340">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="56097-341">**ServiceConnect**</span><span class="sxs-lookup"><span data-stu-id="56097-341">**ServiceConnect**</span></span> |<span data-ttu-id="56097-342">Hizmet dönük iletişim ve uç nokta izleme buluta verir erişin.</span><span class="sxs-lookup"><span data-stu-id="56097-342">Grants access to cloud service-facing communication and monitoring endpoints.</span></span> <br/><span data-ttu-id="56097-343">Cihaz bulut iletilerini, bulut-cihaz iletilerini göndermek ve karşılık gelen teslim alındı bildirimleri almak için izin verir.</span><span class="sxs-lookup"><span data-stu-id="56097-343">Grants permission to receive device-to-cloud messages, send cloud-to-device messages, and retrieve the corresponding delivery acknowledgments.</span></span> <br/><span data-ttu-id="56097-344">Karşıya yükleme dosyası için teslim bildirimleri almak için izin verir.</span><span class="sxs-lookup"><span data-stu-id="56097-344">Grants permission to retrieve delivery acknowledgements for file uploads.</span></span> <br/><span data-ttu-id="56097-345">Etiketler ve istenen özelliklerini güncelleştirmek için bildirilen özelliklerini almak ve sorguları çalıştırmak için cihaz çiftlerini erişmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="56097-345">Grants permission to access device twins to update tags and desired properties, retrieve reported properties, and run queries.</span></span> <br/><span data-ttu-id="56097-346">Bu izin, arka uç bulut Hizmetleri tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="56097-346">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="56097-347">**DeviceConnect**</span><span class="sxs-lookup"><span data-stu-id="56097-347">**DeviceConnect**</span></span> |<span data-ttu-id="56097-348">Aygıt'te Uç noktalara erişimi verir.</span><span class="sxs-lookup"><span data-stu-id="56097-348">Grants access to device-facing endpoints.</span></span> <br/><span data-ttu-id="56097-349">Cihaz bulut iletilerini göndermek ve bulut-cihaz iletilerini izni verir.</span><span class="sxs-lookup"><span data-stu-id="56097-349">Grants permission to send device-to-cloud messages and receive cloud-to-device messages.</span></span> <br/><span data-ttu-id="56097-350">Bir CİHAZDAN karşıya dosya yükleme gerçekleştirme izni verir.</span><span class="sxs-lookup"><span data-stu-id="56097-350">Grants permission to perform file upload from a device.</span></span> <br/><span data-ttu-id="56097-351">Cihaz çifti istenen özellik bildirimleri almak ve cihaz çifti güncelleştirme izni verir özellikleri bildirdi.</span><span class="sxs-lookup"><span data-stu-id="56097-351">Grants permission to receive device twin desired property notifications and update device twin reported properties.</span></span> <br/><span data-ttu-id="56097-352">Verir dosya gerçekleştirme izni yükler.</span><span class="sxs-lookup"><span data-stu-id="56097-352">Grants permission to perform file uploads.</span></span> <br/><span data-ttu-id="56097-353">Bu izin, cihazlar tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="56097-353">This permission is used by devices.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="56097-354">Ek başvuru bilgileri</span><span class="sxs-lookup"><span data-stu-id="56097-354">Additional reference material</span></span>

<span data-ttu-id="56097-355">IOT Hub Geliştirici Kılavuzu'ndaki diğer başvuru konuları içerir:</span><span class="sxs-lookup"><span data-stu-id="56097-355">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="56097-356">[IOT Hub uç noktaları] [ lnk-endpoints] her IOT hub'ı çalışma zamanı ve yönetim işlemleri için kullanıma sunan çeşitli uç noktaları açıklar.</span><span class="sxs-lookup"><span data-stu-id="56097-356">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="56097-357">[Azaltma ve kotaları] [ lnk-quotas] kotaları açıklar ve IOT hub'ı hizmete uygulamak davranışları azaltma.</span><span class="sxs-lookup"><span data-stu-id="56097-357">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="56097-358">[Azure IOT cihaz ve hizmet SDK'ları] [ lnk-sdks] çeşitli dil IOT Hub ile etkileşim hem cihaz hem de hizmet uygulamaları geliştirirken kullanabilir SDK'ları listeler.</span><span class="sxs-lookup"><span data-stu-id="56097-358">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="56097-359">[IOT hub'ı sorgu dili] [ lnk-query] IOT Hub'ından, cihaz çiftlerini ve işleri hakkında bilgi almak için kullanabileceğiniz sorgu dili açıklar.</span><span class="sxs-lookup"><span data-stu-id="56097-359">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="56097-360">[IOT Hub MQTT Destek] [ lnk-devguide-mqtt] IOT hub'ı desteği hakkında daha fazla bilgi için MQTT Protokolü sağlar.</span><span class="sxs-lookup"><span data-stu-id="56097-360">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56097-361">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="56097-361">Next steps</span></span>

<span data-ttu-id="56097-362">IOT hub'ı erişimi denetlemek öğrendiniz artık aşağıdaki IOT Hub Geliştirici Kılavuzu konuları ilgilenen olabilir:</span><span class="sxs-lookup"><span data-stu-id="56097-362">Now you have learned how to control access IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="56097-363">[Cihaz çiftlerini durumu ve yapılandırmaları eşitlemek için kullanın][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="56097-363">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="56097-364">[Bir cihazda doğrudan bir yöntem çağırma][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="56097-364">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="56097-365">[Birden çok aygıta işleri zamanla][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="56097-365">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="56097-366">Bu makalede açıklanan kavramları bazıları denemek istiyorsanız, aşağıdaki IOT hub'ı öğreticilerde ilgilenen olabilir:</span><span class="sxs-lookup"><span data-stu-id="56097-366">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorials:</span></span>

* <span data-ttu-id="56097-367">[Azure IOT Hub ile çalışmaya başlama][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="56097-367">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>
* <span data-ttu-id="56097-368">[IOT Hub ile bulut-cihaz iletilerini göndermek nasıl][lnk-c2d-tutorial]</span><span class="sxs-lookup"><span data-stu-id="56097-368">[How to send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial]</span></span>
* <span data-ttu-id="56097-369">[IOT Hub cihaz-bulut iletileri işleme][lnk-d2c-tutorial]</span><span class="sxs-lookup"><span data-stu-id="56097-369">[How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial]</span></span>

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
