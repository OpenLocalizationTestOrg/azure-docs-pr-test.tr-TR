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
# <a name="connect-tooa-secure-service-with-hello-reverse-proxy"></a>Tooa güvenli service hello ters proxy ile bağlanma

Bu makalede nasıl tooestablish arasındaki güvenli bir bağlantı hello ters proxy ve bu nedenle bir bitiş tooend güvenli kanal Etkinleştirme Hizmetleri açıklanmaktadır.

Yalnızca ters proxy yapılandırılmış toolisten HTTPS üzerinden olduğunda toosecure hizmetlerine bağlanan desteklenir. Merhaba belgenin kalan hello böyledir varsayar.
Çok başvuran[ters proxy Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure hello ters proxy Service Fabric.

## <a name="secure-connection-establishment-between-hello-reverse-proxy-and-services"></a>Merhaba ters proxy ve hizmetleri arasında güvenli bağlantı kurma 

### <a name="reverse-proxy-authenticating-tooservices"></a>Ters proxy tooservices kimlik doğrulaması:
Merhaba ters proxy kendisi ile belirtilen sertifikasını kullanarak tooservices tanımlayan ***reverseProxyCertificate*** hello özelliğinde **küme** [kaynak türü bölümü](../azure-resource-manager/resource-group-authoring-templates.md). Hizmetleri hello ters Ara sunucu tarafından sunulan hello mantığı tooverify hello sertifikası uygulayabilirsiniz. Merhaba Hizmetleri kabul hello istemci sertifikası ayrıntıları yapılandırma ayarları hello yapılandırma paketi olarak belirtebilirsiniz. Bu, çalışma zamanında okuyabilir ve hello ters Ara sunucu tarafından sunulan toovalidate hello sertifikası kullanılır. Çok başvuran[uygulama parametreleri yönetmek](service-fabric-manage-multiple-environment-app-configuration.md) tooadd hello yapılandırma ayarları. 

### <a name="reverse-proxy-verifying-hello-services-identity-via-hello-certificate-presented-by-hello-service"></a>Ters proxy hello hizmeti tarafından sunulan hello sertifikası aracılığıyla Hello hizmetin kimlik doğrulama:
tooperform sunucu sertifika doğrulaması hello Hizmetleri tarafından sunulan hello sertifikaların ters proxy seçenekleri aşağıdaki hello birini destekler: None, ServiceCommonNameAndIssuer ve ServiceCertificateThumbprints.
Bu üç seçenekten birini tooselect hello belirtin **ApplicationCertificateValidationPolicy** ApplicationGateway/Http öğesinin altında hello Parametreler bölümünde [fabricSettings](service-fabric-cluster-fabric-settings.md).

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

Bu seçeneklerin her biri için ek yapılandırma hakkında ayrıntılı bilgi için toohello sonraki bölümüne bakın.

### <a name="service-certificate-validation-options"></a>Hizmet sertifika doğrulama seçenekleri 

- **Hiçbiri**: ters proxy hello yönlendirilirken hizmeti sertifika doğrulaması atlar ve hello güvenli bağlantı kurar. Merhaba varsayılan davranış budur.
Merhaba belirtin **ApplicationCertificateValidationPolicy** değerle **hiçbiri** hello Parametreler bölümünde ApplicationGateway/Http öğesi.

- **ServiceCommonNameAndIssuer**: ters proxy doğrular hello sertifika sunulan sertifikanın ortak adı ve hemen verenin parmak izi göre hello hizmeti tarafından: hello belirtin **ApplicationCertificateValidationPolicy**  değerle **ServiceCommonNameAndIssuer** ApplicationGateway/Http öğesinin hello Parametreler bölümünde.

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

toospecify hello listesine hizmet ortak adı ve verenin parmak izlerini eklemek bir **Http/ApplicationGateway/ServiceCommonNameAndIssuer** öğesinin aşağıda gösterildiği gibi fabricSettings altında. Birden çok sertifika ortak adı ve verenin parmak izi çiftleri hello parametreleri dizi öğesindeki eklenebilir. 

Merhaba uç nokta ters proxy toopresents ortak olan bir sertifika bağlanılıyorsa hello değerleri burada belirtilen adı ve verenin parmak iziyle eşleşen, SSL kanalı oluşturulur. Hata toomatch hello sertifika ayrıntıları ters proxy hello istemcinin isteğini 502 (hatalı ağ geçidi) durum kodu ile başarısız olur. HTTP durum satırı Hello hello tümcecik "Geçersiz SSL sertifikası" da içerir 

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


- **ServiceCertificateThumbprints**: ters proxy kendi parmak izine dayanan hello yönlendirilirken hizmet sertifika doğrulama. Merhaba Hizmetleri ile otomatik olarak imzalanan sertifikaları yapılandırıldığında bu rota toogo seçebilirsiniz: hello belirtin **ApplicationCertificateValidationPolicy** değerle **ServiceCertificateThumbprints**ApplicationGateway/Http öğesinin hello Parametreler bölümünde.

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

Ayrıca hello parmak izleriyle belirtin bir **ServiceCertificateThumbprints** giriş parametreleri bölümüne ApplicationGateway/Http öğesinin altında. Birden çok parmak izleri aşağıda gösterildiği gibi hello değeri alanına, virgülle ayrılmış bir liste olarak belirtilebilir:

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

Bu yapılandırma girişte Hello sertifikanın parmak izini hello sunucu listeleniyorsa, ters proxy hello SSL bağlantı başarılı olur. Aksi takdirde hello bağlantıyı sonlandırır ve istemcinin isteğini 502 (hatalı ağ geçidi) ile başarısız hello. HTTP durum satırı Hello hello tümcecik "Geçersiz SSL sertifikası" da içerir

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a>Hizmetleri güvenli yanı sıra güvenli uç noktalarını kullanıma sunar, uç nokta seçme mantığı
Service fabric, bir hizmet için birden fazla uç noktası yapılandırılmasını destekler. Bkz. [Bir hizmet bildiriminde kaynak belirtme](service-fabric-service-manifest-resources.md).

Ters proxy üzerinde hello dayalı hello uç noktaları tooforward hello isteği birini seçer **ListenerName** sorgu parametresi. Bu belirtilmezse, herhangi bir uç nokta hello uç noktalar listesinden seçebilirsiniz. Şimdi bu bir HTTP veya HTTPS uç noktası olabilir. "Güvenli yalnızca modunda" Merhaba ters proxy toooperate istediğiniz senaryolar/gereksinimleri olabilir yani Merhaba güvenli ters proxy tooforward istekleri toounsecured uç noktaları istemezsiniz. Bu hello belirterek sağlanabilir **SecureOnlyMode** yapılandırma girdisi değerle **true** hello Parametreler bölümünde ApplicationGateway/Http öğesi.   

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
> İçinde çalışırken **SecureOnlyMode**, istemci belirtilmişse bir **ListenerName** tooan HTTP(unsecured) endpoint karşılık gelen ters proxy hello isteği bir 404 (bulunamadı) HTTP durum kodu ile başarısız olur.

## <a name="setting-up-client-certificate-authentication-through-hello-reverse-proxy"></a>İstemci sertifikası kimlik doğrulaması hello ters proxy aracılığıyla ayarlama
SSL sonlandırma hello ters proxy olur ve tüm hello istemci sertifikası veriler kaybolur. Merhaba Hizmetleri tooperform istemci sertifikası kimlik doğrulaması için hello ayarlamak **ForwardClientCertificate** hello Parametreler bölümünde ApplicationGateway/Http öğesinin ayarlama.

1. Zaman **ForwardClientCertificate** çok ayarlanır**false**ters proxy istekte hello için istemci sertifikası, SSL el sıkışması sırasında hello istemcisiyle.
Merhaba varsayılan davranış budur.

2. Zaman **ForwardClientCertificate** çok ayarlanır**doğru**, ters proxy istekleri hello istemci sertifikasının hello istemcisi ile kendi SSL el sıkışması sırasında.
Ardından adlı özel bir HTTP üstbilgisi sertifika verilerinde hello istemci iletir **X istemci sertifikası**. Merhaba üstbilgi değeri hello base64 ile kodlanmış PEM biçiminde hello istemci sertifikasının dizesidir. Merhaba hizmeti başarılı/hello istekle ilgili durum kodu hello sertifika verileri denetledikten sonra başarısız.
Merhaba istemci sertifika sunmuyorsa ters proxy boş bir başlık iletir ve hello hizmeti tanıtıcı hello çalışması olanak tanır.

> Ters proxy yalnızca iletici ' dir. Hello istemci sertifikasının herhangi doğrulaması gerçekleştirmez.


## <a name="next-steps"></a>Sonraki adımlar
* Çok başvuran[ters proxy tooconnect toosecure hizmetlerini yapılandırma](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) için Azure Resource Manager şablonu güvenli ters proxy hello farklı hizmet sertifika doğrulama seçeneklerini tooconfigure örnekleri.
* HTTP iletişimi Hizmetleri'nde arasında örneğine bakın bir [örnek proje github'da](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).
* [Güvenilir hizmetler remoting ile uzak yordam çağrıları](service-fabric-reliable-services-communication-remoting.md)
* [Web API OWIN güvenilir Hizmetleri'nde kullanır](service-fabric-reliable-services-communication-webapi.md)
* [Küme sertifikalarını yönetme](service-fabric-cluster-security-update-certs-azure.md)
