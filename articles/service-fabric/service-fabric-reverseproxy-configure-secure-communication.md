---
title: "Service Fabric aaaAzure ters proxy güvenli iletişim | Microsoft Docs"
description: "Ters proxy tooenable güvenli uçtan uca iletişimi yapılandırın."
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/10/2017
ms.author: kavyako
ms.openlocfilehash: e1248dffe2c324373ad0d09d3f5f094db74480d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-service-with-hello-reverse-proxy"></a><span data-ttu-id="64630-103">Tooa güvenli service hello ters proxy ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="64630-103">Connect tooa secure service with hello reverse proxy</span></span>

<span data-ttu-id="64630-104">Bu makalede nasıl tooestablish arasındaki güvenli bir bağlantı hello ters proxy ve bu nedenle bir bitiş tooend güvenli kanal Etkinleştirme Hizmetleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="64630-104">This article explains how tooestablish secure connection between hello reverse proxy and services, thus enabling an end tooend secure channel.</span></span>

<span data-ttu-id="64630-105">Yalnızca ters proxy yapılandırılmış toolisten HTTPS üzerinden olduğunda toosecure hizmetlerine bağlanan desteklenir.</span><span class="sxs-lookup"><span data-stu-id="64630-105">Connecting toosecure services is supported only when reverse proxy is configured toolisten on HTTPS.</span></span> <span data-ttu-id="64630-106">Merhaba belgenin kalan hello böyledir varsayar.</span><span class="sxs-lookup"><span data-stu-id="64630-106">Rest of hello document assumes this is hello case.</span></span>
<span data-ttu-id="64630-107">Çok başvuran[ters proxy Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure hello ters proxy Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="64630-107">Refer too[Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure hello reverse proxy in Service Fabric.</span></span>

## <a name="secure-connection-establishment-between-hello-reverse-proxy-and-services"></a><span data-ttu-id="64630-108">Merhaba ters proxy ve hizmetleri arasında güvenli bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="64630-108">Secure connection establishment between hello reverse proxy and services</span></span> 

### <a name="reverse-proxy-authenticating-tooservices"></a><span data-ttu-id="64630-109">Ters proxy tooservices kimlik doğrulaması:</span><span class="sxs-lookup"><span data-stu-id="64630-109">Reverse proxy authenticating tooservices:</span></span>
<span data-ttu-id="64630-110">Merhaba ters proxy kendisi ile belirtilen sertifikasını kullanarak tooservices tanımlayan ***reverseProxyCertificate*** hello özelliğinde **küme** [kaynak türü bölümü](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="64630-110">hello reverse proxy identifies itself tooservices using its certificate, specified with ***reverseProxyCertificate*** property in hello **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="64630-111">Hizmetleri hello ters Ara sunucu tarafından sunulan hello mantığı tooverify hello sertifikası uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64630-111">Services can implement hello logic tooverify hello certificate presented by hello reverse proxy.</span></span> <span data-ttu-id="64630-112">Merhaba Hizmetleri kabul hello istemci sertifikası ayrıntıları yapılandırma ayarları hello yapılandırma paketi olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64630-112">hello services can specify hello accepted client certificate details as configuration settings in hello configuration package.</span></span> <span data-ttu-id="64630-113">Bu, çalışma zamanında okuyabilir ve hello ters Ara sunucu tarafından sunulan toovalidate hello sertifikası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="64630-113">This can be read at runtime and used toovalidate hello certificate presented by hello reverse proxy.</span></span> <span data-ttu-id="64630-114">Çok başvuran[uygulama parametreleri yönetmek](service-fabric-manage-multiple-environment-app-configuration.md) tooadd hello yapılandırma ayarları.</span><span class="sxs-lookup"><span data-stu-id="64630-114">Refer too[Manage application parameters](service-fabric-manage-multiple-environment-app-configuration.md) tooadd hello configuration settings.</span></span> 

### <a name="reverse-proxy-verifying-hello-services-identity-via-hello-certificate-presented-by-hello-service"></a><span data-ttu-id="64630-115">Ters proxy hello hizmeti tarafından sunulan hello sertifikası aracılığıyla Hello hizmetin kimlik doğrulama:</span><span class="sxs-lookup"><span data-stu-id="64630-115">Reverse proxy verifying hello service's identity via hello certificate presented by hello service:</span></span>
<span data-ttu-id="64630-116">tooperform sunucu sertifika doğrulaması hello Hizmetleri tarafından sunulan hello sertifikaların ters proxy seçenekleri aşağıdaki hello birini destekler: None, ServiceCommonNameAndIssuer ve ServiceCertificateThumbprints.</span><span class="sxs-lookup"><span data-stu-id="64630-116">tooperform server certificate validation of hello certificates presented by hello services, reverse proxy supports one of hello following options: None, ServiceCommonNameAndIssuer, and ServiceCertificateThumbprints.</span></span>
<span data-ttu-id="64630-117">Bu üç seçenekten birini tooselect hello belirtin **ApplicationCertificateValidationPolicy** ApplicationGateway/Http öğesinin altında hello Parametreler bölümünde [fabricSettings](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="64630-117">tooselect one of these three options, specify hello **ApplicationCertificateValidationPolicy** in hello parameters section of ApplicationGateway/Http element under [fabricSettings](service-fabric-cluster-fabric-settings.md).</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "None"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="64630-118">Bu seçeneklerin her biri için ek yapılandırma hakkında ayrıntılı bilgi için toohello sonraki bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="64630-118">Refer toohello next section for details about additional configuration for each of these options.</span></span>

### <a name="service-certificate-validation-options"></a><span data-ttu-id="64630-119">Hizmet sertifika doğrulama seçenekleri</span><span class="sxs-lookup"><span data-stu-id="64630-119">Service certificate validation options</span></span> 

- <span data-ttu-id="64630-120">**Hiçbiri**: ters proxy hello yönlendirilirken hizmeti sertifika doğrulaması atlar ve hello güvenli bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="64630-120">**None**: Reverse proxy skips verification of hello proxied service certificate and establishes hello secure connection.</span></span> <span data-ttu-id="64630-121">Merhaba varsayılan davranış budur.</span><span class="sxs-lookup"><span data-stu-id="64630-121">This is hello default behavior.</span></span>
<span data-ttu-id="64630-122">Merhaba belirtin **ApplicationCertificateValidationPolicy** değerle **hiçbiri** hello Parametreler bölümünde ApplicationGateway/Http öğesi.</span><span class="sxs-lookup"><span data-stu-id="64630-122">Specify hello **ApplicationCertificateValidationPolicy** with value **None** in hello parameters section of ApplicationGateway/Http element.</span></span>

- <span data-ttu-id="64630-123">**ServiceCommonNameAndIssuer**: ters proxy doğrular hello sertifika sunulan sertifikanın ortak adı ve hemen verenin parmak izi göre hello hizmeti tarafından: hello belirtin **ApplicationCertificateValidationPolicy**  değerle **ServiceCommonNameAndIssuer** ApplicationGateway/Http öğesinin hello Parametreler bölümünde.</span><span class="sxs-lookup"><span data-stu-id="64630-123">**ServiceCommonNameAndIssuer**: Reverse proxy verifies hello certificate presented by hello service based on certificate's common name and immediate issuer's thumbprint: Specify hello **ApplicationCertificateValidationPolicy** with value **ServiceCommonNameAndIssuer** in hello parameters section of ApplicationGateway/Http element.</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCommonNameAndIssuer"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="64630-124">toospecify hello listesine hizmet ortak adı ve verenin parmak izlerini eklemek bir **Http/ApplicationGateway/ServiceCommonNameAndIssuer** öğesinin aşağıda gösterildiği gibi fabricSettings altında.</span><span class="sxs-lookup"><span data-stu-id="64630-124">toospecify hello list of service common name and issuer thumbprints, add a **ApplicationGateway/Http/ServiceCommonNameAndIssuer** element under fabricSettings, as shown below.</span></span> <span data-ttu-id="64630-125">Birden çok sertifika ortak adı ve verenin parmak izi çiftleri hello parametreleri dizi öğesindeki eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="64630-125">Multiple certificate common name and issuer thumbprint pairs can be added in hello parameters array element.</span></span> 

<span data-ttu-id="64630-126">Merhaba uç nokta ters proxy toopresents ortak olan bir sertifika bağlanılıyorsa hello değerleri burada belirtilen adı ve verenin parmak iziyle eşleşen, SSL kanalı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="64630-126">If hello endpoint reverse proxy is connecting toopresents a certificate who's common name and  issuer thumbprint matches any of hello values specified here, SSL channel is established.</span></span> <span data-ttu-id="64630-127">Hata toomatch hello sertifika ayrıntıları ters proxy hello istemcinin isteğini 502 (hatalı ağ geçidi) durum kodu ile başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="64630-127">Upon failure toomatch hello certificate details, reverse proxy fails hello client's request with a 502 (Bad Gateway) status code.</span></span> <span data-ttu-id="64630-128">HTTP durum satırı Hello hello tümcecik "Geçersiz SSL sertifikası" da içerir</span><span class="sxs-lookup"><span data-stu-id="64630-128">hello HTTP status line will also contain hello phrase "Invalid SSL Certificate."</span></span> 

```json
{
"fabricSettings": [
          ...
          {
             "name": "ApplicationGateway/Http/ServiceCommonNameAndIssuer",
            "parameters": [
              {
                "name": "WinFabric-Test-Certificate-CN1",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 b4 22 11"
              },
              {
                "name": "WinFabric-Test-Certificate-CN2",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 11 33 44"
              }
            ]
          }
        ],
        ...
}
```


- <span data-ttu-id="64630-129">**ServiceCertificateThumbprints**: ters proxy kendi parmak izine dayanan hello yönlendirilirken hizmet sertifika doğrulama.</span><span class="sxs-lookup"><span data-stu-id="64630-129">**ServiceCertificateThumbprints**: Reverse proxy will verify hello proxied service certificate based on its thumbprint.</span></span> <span data-ttu-id="64630-130">Merhaba Hizmetleri ile otomatik olarak imzalanan sertifikaları yapılandırıldığında bu rota toogo seçebilirsiniz: hello belirtin **ApplicationCertificateValidationPolicy** değerle **ServiceCertificateThumbprints**ApplicationGateway/Http öğesinin hello Parametreler bölümünde.</span><span class="sxs-lookup"><span data-stu-id="64630-130">You can choose toogo this route when hello services are configured with self signed certificates: Specify hello **ApplicationCertificateValidationPolicy** with value **ServiceCertificateThumbprints** in hello parameters section of ApplicationGateway/Http element.</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCertificateThumbprints"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="64630-131">Ayrıca hello parmak izleriyle belirtin bir **ServiceCertificateThumbprints** giriş parametreleri bölümüne ApplicationGateway/Http öğesinin altında.</span><span class="sxs-lookup"><span data-stu-id="64630-131">Also specify hello thumbprints with a **ServiceCertificateThumbprints** entry under parameters section of ApplicationGateway/Http element.</span></span> <span data-ttu-id="64630-132">Birden çok parmak izleri aşağıda gösterildiği gibi hello değeri alanına, virgülle ayrılmış bir liste olarak belirtilebilir:</span><span class="sxs-lookup"><span data-stu-id="64630-132">Multiple thumbprints can be specified as a comma-separated list in hello value field, as shown below:</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "ServiceCertificateThumbprints",
                "value": "78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 bf,78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 b9"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="64630-133">Bu yapılandırma girişte Hello sertifikanın parmak izini hello sunucu listeleniyorsa, ters proxy hello SSL bağlantı başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="64630-133">If hello thumbprint of hello server certificate is listed in this config entry, reverse proxy succeeds hello SSL connection.</span></span> <span data-ttu-id="64630-134">Aksi takdirde hello bağlantıyı sonlandırır ve istemcinin isteğini 502 (hatalı ağ geçidi) ile başarısız hello.</span><span class="sxs-lookup"><span data-stu-id="64630-134">Otherwise, it terminates hello connection and fails hello client's request with a 502 (Bad Gateway).</span></span> <span data-ttu-id="64630-135">HTTP durum satırı Hello hello tümcecik "Geçersiz SSL sertifikası" da içerir</span><span class="sxs-lookup"><span data-stu-id="64630-135">hello HTTP status line will also contain hello phrase "Invalid SSL Certificate."</span></span>

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a><span data-ttu-id="64630-136">Hizmetleri güvenli yanı sıra güvenli uç noktalarını kullanıma sunar, uç nokta seçme mantığı</span><span class="sxs-lookup"><span data-stu-id="64630-136">Endpoint selection logic when services expose secure as well as unsecured endpoints</span></span>
<span data-ttu-id="64630-137">Service fabric, bir hizmet için birden fazla uç noktası yapılandırılmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="64630-137">Service fabric supports configuring  multiple endpoints for a service.</span></span> <span data-ttu-id="64630-138">Bkz. [Bir hizmet bildiriminde kaynak belirtme](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="64630-138">See [Specify resources in a service manifest](service-fabric-service-manifest-resources.md).</span></span>

<span data-ttu-id="64630-139">Ters proxy üzerinde hello dayalı hello uç noktaları tooforward hello isteği birini seçer **ListenerName** sorgu parametresi.</span><span class="sxs-lookup"><span data-stu-id="64630-139">Reverse proxy selects one of hello endpoints tooforward hello request based on hello  **ListenerName** query parameter.</span></span> <span data-ttu-id="64630-140">Bu belirtilmezse, herhangi bir uç nokta hello uç noktalar listesinden seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64630-140">If this is not specified, it can pick any endpoint from hello endpoints list.</span></span> <span data-ttu-id="64630-141">Şimdi bu bir HTTP veya HTTPS uç noktası olabilir.</span><span class="sxs-lookup"><span data-stu-id="64630-141">Now this can be an HTTP or HTTPS endpoint.</span></span> <span data-ttu-id="64630-142">"Güvenli yalnızca modunda" Merhaba ters proxy toooperate istediğiniz senaryolar/gereksinimleri olabilir yani</span><span class="sxs-lookup"><span data-stu-id="64630-142">There might be scenarios/requirements where you want hello reverse proxy toooperate in a "secure only mode", i.e</span></span> <span data-ttu-id="64630-143">Merhaba güvenli ters proxy tooforward istekleri toounsecured uç noktaları istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="64630-143">you don't want hello secure reverse proxy tooforward requests toounsecured endpoints.</span></span> <span data-ttu-id="64630-144">Bu hello belirterek sağlanabilir **SecureOnlyMode** yapılandırma girdisi değerle **true** hello Parametreler bölümünde ApplicationGateway/Http öğesi.</span><span class="sxs-lookup"><span data-stu-id="64630-144">This can be achieved by specifying hello **SecureOnlyMode** configuration entry with value **true** in hello parameters section of ApplicationGateway/Http element.</span></span>   

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "SecureOnlyMode",
                "value": true
              }
            ]
          }
        ],
        ...
}
```

> 
> <span data-ttu-id="64630-145">İçinde çalışırken **SecureOnlyMode**, istemci belirtilmişse bir **ListenerName** tooan HTTP(unsecured) endpoint karşılık gelen ters proxy hello isteği bir 404 (bulunamadı) HTTP durum kodu ile başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="64630-145">When operating in **SecureOnlyMode**, if client has specified a **ListenerName** corresponding tooan HTTP(unsecured) endpoint, reverse proxy fails hello request with a 404 (Not Found) HTTP status code.</span></span>

## <a name="setting-up-client-certificate-authentication-through-hello-reverse-proxy"></a><span data-ttu-id="64630-146">İstemci sertifikası kimlik doğrulaması hello ters proxy aracılığıyla ayarlama</span><span class="sxs-lookup"><span data-stu-id="64630-146">Setting up client certificate authentication through hello reverse proxy</span></span>
<span data-ttu-id="64630-147">SSL sonlandırma hello ters proxy olur ve tüm hello istemci sertifikası veriler kaybolur.</span><span class="sxs-lookup"><span data-stu-id="64630-147">SSL termination happens at hello reverse proxy and all hello client certificate data is lost.</span></span> <span data-ttu-id="64630-148">Merhaba Hizmetleri tooperform istemci sertifikası kimlik doğrulaması için hello ayarlamak **ForwardClientCertificate** hello Parametreler bölümünde ApplicationGateway/Http öğesinin ayarlama.</span><span class="sxs-lookup"><span data-stu-id="64630-148">For hello services tooperform client certificate authentication, set hello **ForwardClientCertificate** setting in hello parameters section of ApplicationGateway/Http element.</span></span>

1. <span data-ttu-id="64630-149">Zaman **ForwardClientCertificate** çok ayarlanır**false**ters proxy istekte hello için istemci sertifikası, SSL el sıkışması sırasında hello istemcisiyle.</span><span class="sxs-lookup"><span data-stu-id="64630-149">When **ForwardClientCertificate** is set too**false**, reverse proxy will not request for hello client certificate during its SSL handshake with hello client.</span></span>
<span data-ttu-id="64630-150">Merhaba varsayılan davranış budur.</span><span class="sxs-lookup"><span data-stu-id="64630-150">This is hello default behavior.</span></span>

2. <span data-ttu-id="64630-151">Zaman **ForwardClientCertificate** çok ayarlanır**doğru**, ters proxy istekleri hello istemci sertifikasının hello istemcisi ile kendi SSL el sıkışması sırasında.</span><span class="sxs-lookup"><span data-stu-id="64630-151">When **ForwardClientCertificate** is set too**true**, reverse proxy requests for hello client's certificate during its SSL handshake with hello client.</span></span>
<span data-ttu-id="64630-152">Ardından adlı özel bir HTTP üstbilgisi sertifika verilerinde hello istemci iletir **X istemci sertifikası**.</span><span class="sxs-lookup"><span data-stu-id="64630-152">It will then forward hello client certificate data in a custom HTTP header named **X-Client-Certificate**.</span></span> <span data-ttu-id="64630-153">Merhaba üstbilgi değeri hello base64 ile kodlanmış PEM biçiminde hello istemci sertifikasının dizesidir.</span><span class="sxs-lookup"><span data-stu-id="64630-153">hello header value is hello base64 encoded PEM format string of hello client's certificate.</span></span> <span data-ttu-id="64630-154">Merhaba hizmeti başarılı/hello istekle ilgili durum kodu hello sertifika verileri denetledikten sonra başarısız.</span><span class="sxs-lookup"><span data-stu-id="64630-154">hello service can succeed/fail hello request with appropriate status code after inspecting hello certificate data.</span></span>
<span data-ttu-id="64630-155">Merhaba istemci sertifika sunmuyorsa ters proxy boş bir başlık iletir ve hello hizmeti tanıtıcı hello çalışması olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="64630-155">If hello client does not present a certificate, reverse proxy forwards an empty header and let hello service handle hello case.</span></span>

> <span data-ttu-id="64630-156">Ters proxy yalnızca iletici ' dir.</span><span class="sxs-lookup"><span data-stu-id="64630-156">Reverse proxy is a mere forwarder.</span></span> <span data-ttu-id="64630-157">Hello istemci sertifikasının herhangi doğrulaması gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="64630-157">It will not perform any validation of hello client's certificate.</span></span>


## <a name="next-steps"></a><span data-ttu-id="64630-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="64630-158">Next steps</span></span>
* <span data-ttu-id="64630-159">Çok başvuran[ters proxy tooconnect toosecure hizmetlerini yapılandırma](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) için Azure Resource Manager şablonu güvenli ters proxy hello farklı hizmet sertifika doğrulama seçeneklerini tooconfigure örnekleri.</span><span class="sxs-lookup"><span data-stu-id="64630-159">Refer too[Configure reverse proxy tooconnect toosecure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples tooconfigure secure reverse proxy with hello different service certificate validation options.</span></span>
* <span data-ttu-id="64630-160">HTTP iletişimi Hizmetleri'nde arasında örneğine bakın bir [örnek proje github'da](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="64630-160">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="64630-161">Güvenilir hizmetler remoting ile uzak yordam çağrıları</span><span class="sxs-lookup"><span data-stu-id="64630-161">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="64630-162">Web API OWIN güvenilir Hizmetleri'nde kullanır</span><span class="sxs-lookup"><span data-stu-id="64630-162">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="64630-163">Küme sertifikalarını yönetme</span><span class="sxs-lookup"><span data-stu-id="64630-163">Manage cluster certificates</span></span>](service-fabric-cluster-security-update-certs-azure.md)
