---
title: aaaAzure AD Federasyon meta verileri | Microsoft Docs
description: "Bu makalede, Azure Active Directory belirteçleri kabul Hizmetleri için Azure Active Directory yayımlar hello Federasyon meta veri belgesi açıklanmaktadır."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c2d5f80b-aa74-452c-955b-d8eb3ed62652
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 23535bcd5eeb3e9b2e17d89a9b0420fc98bd3895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="federation-metadata"></a>Federasyon meta verileri
Azure Active Directory (Azure AD), Azure AD verir tooaccept hello güvenlik belirteçleri olan hizmetler yapılandırılmış için Federasyon meta veri belgesi yayımlar. Merhaba Federasyon meta veri belgesi biçiminde hello açıklanan [Web Hizmetleri Federasyon dili (WS-Federation) sürüm 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), genişleten [hello OASIS güvenlik onaylama işlemi biçimlendirme dili (SAML) için meta veriler v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a>Kiracı özgü ve Kiracı bağımsız meta veri uç noktaları
Azure AD Kiracı özgü ve Kiracı bağımsız uç noktaları yayımlar.

Kiracı özel uç noktaları, belirli bir kiracı için tasarlanmıştır. Merhaba Kiracı özgü Federasyon meta verileri hello Kiracı, Kiracı özgü veren ve uç nokta bilgileri de dahil olmak üzere ilgili bilgiler içerir. Erişim tooa tek bir kiracı kısıtlamak uygulamaları Kiracı özel uç noktaları kullanın.

Kiracı bağımsız uç noktaları ortak tooall Azure AD kiracılarıyla bilgileri sağlayın. Bu bilgiler konumunda barındırılan tootenants geçerlidir *login.microsoftonline.com* ve kiracılar arasında paylaşılır. Belirli bir kiracı ile ilişkili olmadığından Kiracı bağımsız uç noktaları çok kiracılı uygulamalar için önerilir.

## <a name="federation-metadata-endpoints"></a>Federasyon meta veri uç noktaları
Azure AD konumundaki Federasyon meta verilerini yayımlayan `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.

İçin **Kiracı özel uç noktaları**, hello `TenantDomainName` şu türlerini hello biri olabilir:

* Gibi bir kayıtlı etki alanı adı bir Azure ad Kiracı: `contoso.onmicrosoft.com`.
* Merhaba değişmez Kiracı kimliği hello etki alanının gibi `72f988bf-86f1-41af-91ab-2d7cd011db45`.

İçin **Kiracı bağımsız uç noktaları**, hello `TenantDomainName` olan `common`. Bu belge, login.microsoftonline.com barındırılan ortak tooall Azure AD kiracılarıyla hello Federasyon meta veri öğelerini listeler.

Örneğin, bir kiracı özel uç noktası olabilir `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`. Merhaba Kiracı bağımsız uç noktası [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml). Bu URL'yi bir tarayıcıda yazarak hello Federasyon meta veri belgesi görüntüleyebilirsiniz.

## <a name="contents-of-federation-metadata"></a>Federasyon meta veri içeriğini
Merhaba aşağıdaki bölümde Azure AD tarafından yayınlanan hello belirteçleri tüketen Hizmetleri tarafından gereken bilgileri sağlar.

### <a name="entity-id"></a>Varlık Kimliği
Merhaba `EntityDescriptor` öğesi içeren bir `EntityID` özniteliği. Merhaba hello değerini `EntityID` öznitelik hello veren temsil eder, diğer bir deyişle, hello güvenlik belirteci hizmeti (STS) verilen hello belirtecini. Bir belirteç almalarına durumunda önemli toovalidate hello veren olur.

Merhaba aşağıdaki meta verileri bir örnek Kiracı özgü gösterir `EntityDescriptor` öğesi ile bir `EntityID` öğesi.

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
Kiracı özgü ile Kiracı kimliği toocreate hello Kiracı kimliği hello Kiracı bağımsız uç noktada değiştirebilirsiniz `EntityID` değeri. Merhaba sonuç değeri olması hello Belirteç Verenin hello aynı. Merhaba stratejisi belirli bir kiracısı için çok kiracılı uygulama toovalidate hello veren sağlar.

Merhaba aşağıdaki meta verileri bir örnek Kiracı bağımsız gösterir `EntityID` öğesi. Lütfen unutmayın, bu hello `{tenant}` sabit, yer tutucu değerdir.

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a>Belirteç imzalama sertifikaları
Bir hizmeti bir Azure AD kiracısı tarafından verilen bir belirteç aldığında hello hello belirtecinin imzası hello Federasyon meta veri belgesi yayımlanan bir imzalama anahtarı ile doğrulanması gerekir. Merhaba Federasyon meta verileri hello ortak hello kiracılar belirteç imzalama için kullanan hello sertifikaları bölümünü içerir. Merhaba sertifika ham bayt görünür hello `KeyDescriptor` öğesi. Merhaba belirteç imzalama sertifikası, imzalama yalnızca zaman hello için başlangıç değerini geçerli `use` özniteliği `signing`.

Azure AD tarafından yayınlanan Federasyon meta veri belgesi, Azure AD tooupdate hello imza sertifikası olduğunda hazırlama gibi birden çok imzalama anahtarı olabilir. Federasyon meta veri belgesi birden fazla sertifika bulunuyorsa, hello belirteçleri doğrularken bir hizmet hello belgedeki tüm sertifikaları desteklemelidir.

Merhaba aşağıdaki meta verileri gösteren bir örnek `KeyDescriptor` imzalama anahtarı ile öğesi.

```
<KeyDescriptor use="signing">
<KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
<X509Data>
<X509Certificate>
MIIDPjCCAiqgAwIBAgIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTIwNjA3MDcwMDAwWhcNMTQwNjA3MDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEArCz8Sn3GGXmikH2MdTeGY1D711EORX/lVXpr+ecGgqfUWF8MPB07XkYuJ54DAuYT318+2XrzMjOtqkT94VkXmxv6dFGhG8YZ8vNMPd4tdj9c0lpvWQdqXtL1TlFRpD/P6UMEigfN0c9oWDg9U7Ilymgei0UXtf1gtcQbc5sSQU0S4vr9YJp2gLFIGK11Iqg4XSGdcI0QWLLkkC6cBukhVnd6BCYbLjTYy3fNs4DzNdemJlxGl8sLexFytBF6YApvSdus3nFXaMCtBGx16HzkK9ne3lobAwL2o79bP4imEGqg+ibvyNmbrwFGnQrBc1jTF9LyQX9q+louxVfHs6ZiVwIDAQABo2IwYDBeBgNVHQEEVzBVgBCxDDsLd8xkfOLKm4Q/SzjtoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAA4IBAQAkJtxxm/ErgySlNk69+1odTMP8Oy6L0H17z7XGG3w4TqvTUSWaxD4hSFJ0e7mHLQLQD7oV/erACXwSZn2pMoZ89MBDjOMQA+e6QzGB7jmSzPTNmQgMLA8fWCfqPrz6zgH+1F1gNp8hJY57kfeVPBiyjuBmlTEBsBlzolY9dd/55qqfQk6cgSeCbHCy/RU/iep0+UsRMlSgPNNmqhj5gmN2AFVCN96zF694LwuPae5CeR2ZcVknexOWHYjFM0MgUSw0ubnGl0h9AJgGyhvNGcjQqu9vd1xkupFgaN+f7P3p3EVN5csBg5H94jEcQZT7EKeTiZ6bTrpDAnrr8tDCy8ng
</X509Certificate>
</X509Data>
</KeyInfo>
</KeyDescriptor>
  ```

Merhaba `KeyDescriptor` öğe hello Federasyon meta veri belgesi; hello WS-Federasyon özgü bölüm ve hello SAML özgü bölümünde iki yerde görüntülenir. Her iki bölümlerde yayımlanan hello sertifikalar olması hello aynı.

Merhaba WS-Federasyon özgü bölümünde bir WS-Federasyon meta veri okuyucusu hello sertifikalardan okuduğunuz bir `RoleDescriptor` hello öğeyle `SecurityTokenServiceType` türü.

Merhaba aşağıdaki meta verileri gösteren bir örnek `RoleDescriptor` öğesi.

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

Merhaba SAML özgü bölümünde bir WS-Federasyon meta veri okuyucusu hello sertifikalardan okuduğunuz bir `IDPSSODescriptor` öğesi.

Merhaba aşağıdaki meta verileri gösteren bir örnek `IDPSSODescriptor` öğesi.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
Kiracı özgü ve Kiracı bağımsız sertifikaların hello biçiminde farklılıkları yoktur.

### <a name="ws-federation-endpoint-url"></a>WS-Federasyon uç nokta URL'si
tek oturum açma ve tek WS-Federasyon protokolünde oturum kapatma için Azure AD URL'yi kullanır hello Hello Federasyon meta verileri içerir. Bu uç noktaya hello görünür `PassiveRequestorEndpoint` öğesi.

Merhaba aşağıdaki meta verileri gösteren bir örnek `PassiveRequestorEndpoint` öğesi için bir kiracı özel uç noktası.

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
Merhaba Kiracı bağımsız uç noktası için hello WS-Federasyon URL hello WS-Federasyon uç hello örnek aşağıdaki gösterildiği gibi görünür.

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a>SAML Protokolü uç nokta URL'si
Merhaba Federasyon meta verilerini Azure AD çoklu oturum açma ve tek SAML 2.0 protokolü oturum kapatma için kullandığı hello URL'sini içerir. Bu uç noktalar hello görünür `IDPSSODescriptor` öğesi.

oturum açma ve oturum kapatma hello URL'leri görünür hello `SingleSignOnService` ve `SingleLogoutService` öğeleri.

Merhaba aşağıdaki meta verileri gösteren bir örnek `PassiveResistorEndpoint` Kiracı özgü uç noktası için.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

Benzer şekilde hello ortak SAML 2.0 protokolü uç noktaları için hello uç noktaları hello örnek aşağıdaki gösterildiği gibi hello Kiracı bağımsız Federasyon meta verilerde yayımlanır.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
