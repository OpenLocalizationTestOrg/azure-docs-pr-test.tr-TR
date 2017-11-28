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
# <a name="federation-metadata"></a><span data-ttu-id="4d355-103">Federasyon meta verileri</span><span class="sxs-lookup"><span data-stu-id="4d355-103">Federation metadata</span></span>
<span data-ttu-id="4d355-104">Azure Active Directory (Azure AD), Azure AD verir tooaccept hello güvenlik belirteçleri olan hizmetler yapılandırılmış için Federasyon meta veri belgesi yayımlar.</span><span class="sxs-lookup"><span data-stu-id="4d355-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured tooaccept hello security tokens that Azure AD issues.</span></span> <span data-ttu-id="4d355-105">Merhaba Federasyon meta veri belgesi biçiminde hello açıklanan [Web Hizmetleri Federasyon dili (WS-Federation) sürüm 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), genişleten [hello OASIS güvenlik onaylama işlemi biçimlendirme dili (SAML) için meta veriler v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span><span class="sxs-lookup"><span data-stu-id="4d355-105">hello federation metadata document format is described in hello [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for hello OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="4d355-106">Kiracı özgü ve Kiracı bağımsız meta veri uç noktaları</span><span class="sxs-lookup"><span data-stu-id="4d355-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="4d355-107">Azure AD Kiracı özgü ve Kiracı bağımsız uç noktaları yayımlar.</span><span class="sxs-lookup"><span data-stu-id="4d355-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="4d355-108">Kiracı özel uç noktaları, belirli bir kiracı için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="4d355-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="4d355-109">Merhaba Kiracı özgü Federasyon meta verileri hello Kiracı, Kiracı özgü veren ve uç nokta bilgileri de dahil olmak üzere ilgili bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="4d355-109">hello tenant-specific federation metadata includes information about hello tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="4d355-110">Erişim tooa tek bir kiracı kısıtlamak uygulamaları Kiracı özel uç noktaları kullanın.</span><span class="sxs-lookup"><span data-stu-id="4d355-110">Applications that restrict access tooa single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="4d355-111">Kiracı bağımsız uç noktaları ortak tooall Azure AD kiracılarıyla bilgileri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="4d355-111">Tenant-independent endpoints provide information that is common tooall Azure AD tenants.</span></span> <span data-ttu-id="4d355-112">Bu bilgiler konumunda barındırılan tootenants geçerlidir *login.microsoftonline.com* ve kiracılar arasında paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="4d355-112">This information applies tootenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="4d355-113">Belirli bir kiracı ile ilişkili olmadığından Kiracı bağımsız uç noktaları çok kiracılı uygulamalar için önerilir.</span><span class="sxs-lookup"><span data-stu-id="4d355-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="4d355-114">Federasyon meta veri uç noktaları</span><span class="sxs-lookup"><span data-stu-id="4d355-114">Federation metadata endpoints</span></span>
<span data-ttu-id="4d355-115">Azure AD konumundaki Federasyon meta verilerini yayımlayan `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="4d355-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="4d355-116">İçin **Kiracı özel uç noktaları**, hello `TenantDomainName` şu türlerini hello biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="4d355-116">For **tenant-specific endpoints**, hello `TenantDomainName` can be one of hello following types:</span></span>

* <span data-ttu-id="4d355-117">Gibi bir kayıtlı etki alanı adı bir Azure ad Kiracı: `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="4d355-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="4d355-118">Merhaba değişmez Kiracı kimliği hello etki alanının gibi `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span><span class="sxs-lookup"><span data-stu-id="4d355-118">hello immutable tenant ID of hello domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="4d355-119">İçin **Kiracı bağımsız uç noktaları**, hello `TenantDomainName` olan `common`.</span><span class="sxs-lookup"><span data-stu-id="4d355-119">For **tenant-independent endpoints**, hello `TenantDomainName` is `common`.</span></span> <span data-ttu-id="4d355-120">Bu belge, login.microsoftonline.com barındırılan ortak tooall Azure AD kiracılarıyla hello Federasyon meta veri öğelerini listeler.</span><span class="sxs-lookup"><span data-stu-id="4d355-120">This document lists only hello Federation Metadata elements that are common tooall Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="4d355-121">Örneğin, bir kiracı özel uç noktası olabilir `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="4d355-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="4d355-122">Merhaba Kiracı bağımsız uç noktası [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span><span class="sxs-lookup"><span data-stu-id="4d355-122">hello tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="4d355-123">Bu URL'yi bir tarayıcıda yazarak hello Federasyon meta veri belgesi görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d355-123">You can view hello federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="4d355-124">Federasyon meta veri içeriğini</span><span class="sxs-lookup"><span data-stu-id="4d355-124">Contents of federation Metadata</span></span>
<span data-ttu-id="4d355-125">Merhaba aşağıdaki bölümde Azure AD tarafından yayınlanan hello belirteçleri tüketen Hizmetleri tarafından gereken bilgileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="4d355-125">hello following section provides information needed by services that consume hello tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="4d355-126">Varlık Kimliği</span><span class="sxs-lookup"><span data-stu-id="4d355-126">Entity ID</span></span>
<span data-ttu-id="4d355-127">Merhaba `EntityDescriptor` öğesi içeren bir `EntityID` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="4d355-127">hello `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="4d355-128">Merhaba hello değerini `EntityID` öznitelik hello veren temsil eder, diğer bir deyişle, hello güvenlik belirteci hizmeti (STS) verilen hello belirtecini.</span><span class="sxs-lookup"><span data-stu-id="4d355-128">hello value of hello `EntityID` attribute represents hello issuer, that is, hello security token service (STS) that issued hello token.</span></span> <span data-ttu-id="4d355-129">Bir belirteç almalarına durumunda önemli toovalidate hello veren olur.</span><span class="sxs-lookup"><span data-stu-id="4d355-129">It is important toovalidate hello issuer when you receive a token.</span></span>

<span data-ttu-id="4d355-130">Merhaba aşağıdaki meta verileri bir örnek Kiracı özgü gösterir `EntityDescriptor` öğesi ile bir `EntityID` öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d355-130">hello following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="4d355-131">Kiracı özgü ile Kiracı kimliği toocreate hello Kiracı kimliği hello Kiracı bağımsız uç noktada değiştirebilirsiniz `EntityID` değeri.</span><span class="sxs-lookup"><span data-stu-id="4d355-131">You can replace hello tenant ID in hello tenant-independent endpoint with your tenant ID toocreate a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="4d355-132">Merhaba sonuç değeri olması hello Belirteç Verenin hello aynı.</span><span class="sxs-lookup"><span data-stu-id="4d355-132">hello resulting value will be hello same as hello token issuer.</span></span> <span data-ttu-id="4d355-133">Merhaba stratejisi belirli bir kiracısı için çok kiracılı uygulama toovalidate hello veren sağlar.</span><span class="sxs-lookup"><span data-stu-id="4d355-133">hello strategy allows a multi-tenant application toovalidate hello issuer for a given tenant.</span></span>

<span data-ttu-id="4d355-134">Merhaba aşağıdaki meta verileri bir örnek Kiracı bağımsız gösterir `EntityID` öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d355-134">hello following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="4d355-135">Lütfen unutmayın, bu hello `{tenant}` sabit, yer tutucu değerdir.</span><span class="sxs-lookup"><span data-stu-id="4d355-135">Please note, that hello `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="4d355-136">Belirteç imzalama sertifikaları</span><span class="sxs-lookup"><span data-stu-id="4d355-136">Token signing certificates</span></span>
<span data-ttu-id="4d355-137">Bir hizmeti bir Azure AD kiracısı tarafından verilen bir belirteç aldığında hello hello belirtecinin imzası hello Federasyon meta veri belgesi yayımlanan bir imzalama anahtarı ile doğrulanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d355-137">When a service receives a token that is issued by a Azure AD tenant, hello signature of hello token must be validated with a signing key that is published in hello federation metadata document.</span></span> <span data-ttu-id="4d355-138">Merhaba Federasyon meta verileri hello ortak hello kiracılar belirteç imzalama için kullanan hello sertifikaları bölümünü içerir.</span><span class="sxs-lookup"><span data-stu-id="4d355-138">hello federation metadata includes hello public portion of hello certificates that hello tenants use for token signing.</span></span> <span data-ttu-id="4d355-139">Merhaba sertifika ham bayt görünür hello `KeyDescriptor` öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d355-139">hello certificate raw bytes appear in hello `KeyDescriptor` element.</span></span> <span data-ttu-id="4d355-140">Merhaba belirteç imzalama sertifikası, imzalama yalnızca zaman hello için başlangıç değerini geçerli `use` özniteliği `signing`.</span><span class="sxs-lookup"><span data-stu-id="4d355-140">hello token signing certificate is valid for signing only when hello value of hello `use` attribute is `signing`.</span></span>

<span data-ttu-id="4d355-141">Azure AD tarafından yayınlanan Federasyon meta veri belgesi, Azure AD tooupdate hello imza sertifikası olduğunda hazırlama gibi birden çok imzalama anahtarı olabilir.</span><span class="sxs-lookup"><span data-stu-id="4d355-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing tooupdate hello signing certificate.</span></span> <span data-ttu-id="4d355-142">Federasyon meta veri belgesi birden fazla sertifika bulunuyorsa, hello belirteçleri doğrularken bir hizmet hello belgedeki tüm sertifikaları desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="4d355-142">When a federation metadata document includes more than one certificate, a service that is validating hello tokens should support all certificates in hello document.</span></span>

<span data-ttu-id="4d355-143">Merhaba aşağıdaki meta verileri gösteren bir örnek `KeyDescriptor` imzalama anahtarı ile öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d355-143">hello following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

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

<span data-ttu-id="4d355-144">Merhaba `KeyDescriptor` öğe hello Federasyon meta veri belgesi; hello WS-Federasyon özgü bölüm ve hello SAML özgü bölümünde iki yerde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4d355-144">hello `KeyDescriptor` element appears in two places in hello federation metadata document; in hello WS-Federation-specific section and hello SAML-specific section.</span></span> <span data-ttu-id="4d355-145">Her iki bölümlerde yayımlanan hello sertifikalar olması hello aynı.</span><span class="sxs-lookup"><span data-stu-id="4d355-145">hello certificates published in both sections will be hello same.</span></span>

<span data-ttu-id="4d355-146">Merhaba WS-Federasyon özgü bölümünde bir WS-Federasyon meta veri okuyucusu hello sertifikalardan okuduğunuz bir `RoleDescriptor` hello öğeyle `SecurityTokenServiceType` türü.</span><span class="sxs-lookup"><span data-stu-id="4d355-146">In hello WS-Federation-specific section, a WS-Federation metadata reader would read hello certificates from a `RoleDescriptor` element with hello `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="4d355-147">Merhaba aşağıdaki meta verileri gösteren bir örnek `RoleDescriptor` öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d355-147">hello following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="4d355-148">Merhaba SAML özgü bölümünde bir WS-Federasyon meta veri okuyucusu hello sertifikalardan okuduğunuz bir `IDPSSODescriptor` öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d355-148">In hello SAML-specific section, a WS-Federation metadata reader would read hello certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="4d355-149">Merhaba aşağıdaki meta verileri gösteren bir örnek `IDPSSODescriptor` öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d355-149">hello following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="4d355-150">Kiracı özgü ve Kiracı bağımsız sertifikaların hello biçiminde farklılıkları yoktur.</span><span class="sxs-lookup"><span data-stu-id="4d355-150">There are no differences in hello format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="4d355-151">WS-Federasyon uç nokta URL'si</span><span class="sxs-lookup"><span data-stu-id="4d355-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="4d355-152">tek oturum açma ve tek WS-Federasyon protokolünde oturum kapatma için Azure AD URL'yi kullanır hello Hello Federasyon meta verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="4d355-152">hello federation metadata includes hello URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="4d355-153">Bu uç noktaya hello görünür `PassiveRequestorEndpoint` öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d355-153">This endpoint appears in hello `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="4d355-154">Merhaba aşağıdaki meta verileri gösteren bir örnek `PassiveRequestorEndpoint` öğesi için bir kiracı özel uç noktası.</span><span class="sxs-lookup"><span data-stu-id="4d355-154">hello following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="4d355-155">Merhaba Kiracı bağımsız uç noktası için hello WS-Federasyon URL hello WS-Federasyon uç hello örnek aşağıdaki gösterildiği gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="4d355-155">For hello tenant-independent endpoint, hello WS-Federation URL appears in hello WS-Federation endpoint, as shown in hello following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="4d355-156">SAML Protokolü uç nokta URL'si</span><span class="sxs-lookup"><span data-stu-id="4d355-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="4d355-157">Merhaba Federasyon meta verilerini Azure AD çoklu oturum açma ve tek SAML 2.0 protokolü oturum kapatma için kullandığı hello URL'sini içerir.</span><span class="sxs-lookup"><span data-stu-id="4d355-157">hello federation metadata includes hello URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="4d355-158">Bu uç noktalar hello görünür `IDPSSODescriptor` öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d355-158">These endpoints appear in hello `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="4d355-159">oturum açma ve oturum kapatma hello URL'leri görünür hello `SingleSignOnService` ve `SingleLogoutService` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="4d355-159">hello sign-in and sign-out URLs appear in hello `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="4d355-160">Merhaba aşağıdaki meta verileri gösteren bir örnek `PassiveResistorEndpoint` Kiracı özgü uç noktası için.</span><span class="sxs-lookup"><span data-stu-id="4d355-160">hello following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="4d355-161">Benzer şekilde hello ortak SAML 2.0 protokolü uç noktaları için hello uç noktaları hello örnek aşağıdaki gösterildiği gibi hello Kiracı bağımsız Federasyon meta verilerde yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="4d355-161">Similarly hello endpoints for hello common SAML 2.0 protocol endpoints are published in hello tenant-independent federation metadata, as shown in hello following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
