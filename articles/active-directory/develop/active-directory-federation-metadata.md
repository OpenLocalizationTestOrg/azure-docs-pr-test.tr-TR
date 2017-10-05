---
title: Azure AD Federasyon meta verileri | Microsoft Docs
description: "Bu makalede, Azure Active Directory belirteçleri kabul Hizmetleri için Azure Active Directory yayımladığı Federasyon meta veri belgesi açıklanmaktadır."
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
ms.openlocfilehash: ecafb02a6ac13d1c3cd1fe77ef710cd8525e32b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="federation-metadata"></a><span data-ttu-id="69925-103">Federasyon meta verileri</span><span class="sxs-lookup"><span data-stu-id="69925-103">Federation metadata</span></span>
<span data-ttu-id="69925-104">Azure Active Directory (Azure AD) Azure AD verir güvenlik belirteçleri kabul etmesi için yapılandırılmış bir Federasyon meta veri belgesi Hizmetleri için yayımlar.</span><span class="sxs-lookup"><span data-stu-id="69925-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured to accept the security tokens that Azure AD issues.</span></span> <span data-ttu-id="69925-105">Federasyon meta veri belgesi biçimi açıklanan [Web Hizmetleri Federasyon dili (WS-Federation) sürüm 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), genişleten [OASISgüvenlikonaylamaişlemibiçimlendirmedili(SAML)v2.0içinmetaveriler](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span><span class="sxs-lookup"><span data-stu-id="69925-105">The federation metadata document format is described in the [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for the OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="69925-106">Kiracı özgü ve Kiracı bağımsız meta veri uç noktaları</span><span class="sxs-lookup"><span data-stu-id="69925-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="69925-107">Azure AD Kiracı özgü ve Kiracı bağımsız uç noktaları yayımlar.</span><span class="sxs-lookup"><span data-stu-id="69925-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="69925-108">Kiracı özel uç noktaları, belirli bir kiracı için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="69925-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="69925-109">Kiracı özgü Federasyon meta verilerinin Kiracı özgü düzenleyici ve uç nokta bilgileri de dahil olmak üzere, Kiracı hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="69925-109">The tenant-specific federation metadata includes information about the tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="69925-110">Tek bir kiracı için erişimi kısıtlamak uygulamaları Kiracı özel uç noktaları kullanın.</span><span class="sxs-lookup"><span data-stu-id="69925-110">Applications that restrict access to a single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="69925-111">Kiracı bağımsız uç noktalar tüm Azure AD kiracıları için genel bilgileri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="69925-111">Tenant-independent endpoints provide information that is common to all Azure AD tenants.</span></span> <span data-ttu-id="69925-112">Konumunda barındırılan kiracılar bu bilgileri uygulandığı *login.microsoftonline.com* ve kiracılar arasında paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="69925-112">This information applies to tenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="69925-113">Belirli bir kiracı ile ilişkili olmadığından Kiracı bağımsız uç noktaları çok kiracılı uygulamalar için önerilir.</span><span class="sxs-lookup"><span data-stu-id="69925-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="69925-114">Federasyon meta veri uç noktaları</span><span class="sxs-lookup"><span data-stu-id="69925-114">Federation metadata endpoints</span></span>
<span data-ttu-id="69925-115">Azure AD konumundaki Federasyon meta verilerini yayımlayan `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="69925-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="69925-116">İçin **Kiracı özel uç noktaları**, `TenantDomainName` aşağıdaki türlerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="69925-116">For **tenant-specific endpoints**, the `TenantDomainName` can be one of the following types:</span></span>

* <span data-ttu-id="69925-117">Gibi bir kayıtlı etki alanı adı bir Azure ad Kiracı: `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="69925-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="69925-118">Değişmez etki alanı kimliği gibi Kiracı `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span><span class="sxs-lookup"><span data-stu-id="69925-118">The immutable tenant ID of the domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="69925-119">İçin **Kiracı bağımsız uç noktaları**, `TenantDomainName` olan `common`.</span><span class="sxs-lookup"><span data-stu-id="69925-119">For **tenant-independent endpoints**, the `TenantDomainName` is `common`.</span></span> <span data-ttu-id="69925-120">Bu belge, login.microsoftonline.com barındırılan tüm Azure AD kiracıları için ortak olan Federasyon meta veri öğeleri listeler.</span><span class="sxs-lookup"><span data-stu-id="69925-120">This document lists only the Federation Metadata elements that are common to all Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="69925-121">Örneğin, bir kiracı özel uç noktası olabilir `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="69925-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="69925-122">Kiracı bağımsız uç noktası [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span><span class="sxs-lookup"><span data-stu-id="69925-122">The tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="69925-123">Bu URL'yi bir tarayıcıda yazarak, Federasyon meta veri belgesi görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69925-123">You can view the federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="69925-124">Federasyon meta veri içeriğini</span><span class="sxs-lookup"><span data-stu-id="69925-124">Contents of federation Metadata</span></span>
<span data-ttu-id="69925-125">Aşağıdaki bölümde, Azure AD tarafından yayınlanan belirteçleri tüketen Hizmetleri tarafından gereken bilgileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="69925-125">The following section provides information needed by services that consume the tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="69925-126">Varlık Kimliği</span><span class="sxs-lookup"><span data-stu-id="69925-126">Entity ID</span></span>
<span data-ttu-id="69925-127">`EntityDescriptor` Öğesi içeren bir `EntityID` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="69925-127">The `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="69925-128">Değeri `EntityID` öznitelik veren, belirteç veren diğer bir deyişle, güvenlik belirteci hizmeti (STS) temsil eder.</span><span class="sxs-lookup"><span data-stu-id="69925-128">The value of the `EntityID` attribute represents the issuer, that is, the security token service (STS) that issued the token.</span></span> <span data-ttu-id="69925-129">Bir belirteç aldığınızda veren doğrulamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="69925-129">It is important to validate the issuer when you receive a token.</span></span>

<span data-ttu-id="69925-130">Aşağıdaki meta verileri kiracıya özgü bir örnek gösterilir `EntityDescriptor` öğesi ile bir `EntityID` öğesi.</span><span class="sxs-lookup"><span data-stu-id="69925-130">The following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="69925-131">Kiracı bağımsız uç noktada Kiracı kimliği Kiracı özgü oluşturmak için Kiracı Kimliğinizle değiştirin `EntityID` değeri.</span><span class="sxs-lookup"><span data-stu-id="69925-131">You can replace the tenant ID in the tenant-independent endpoint with your tenant ID to create a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="69925-132">Sonuç değeri Belirteç Verenin aynı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="69925-132">The resulting value will be the same as the token issuer.</span></span> <span data-ttu-id="69925-133">Belirli bir kiracı için veren doğrulamak çok kiracılı uygulama stratejisi sağlar.</span><span class="sxs-lookup"><span data-stu-id="69925-133">The strategy allows a multi-tenant application to validate the issuer for a given tenant.</span></span>

<span data-ttu-id="69925-134">Aşağıdaki meta verileri, Kiracı bağımsız bir örnek göstermektedir `EntityID` öğesi.</span><span class="sxs-lookup"><span data-stu-id="69925-134">The following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="69925-135">Lütfen aşağıdakilere dikkat edin, `{tenant}` sabit, yer tutucu değerdir.</span><span class="sxs-lookup"><span data-stu-id="69925-135">Please note, that the `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="69925-136">Belirteç imzalama sertifikaları</span><span class="sxs-lookup"><span data-stu-id="69925-136">Token signing certificates</span></span>
<span data-ttu-id="69925-137">Bir hizmeti bir Azure AD kiracısı tarafından verilen bir belirteç aldığında, Federasyon meta veri belgesi yayımlanan bir imzalama anahtarı ile belirtecinin imzası doğrulanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="69925-137">When a service receives a token that is issued by a Azure AD tenant, the signature of the token must be validated with a signing key that is published in the federation metadata document.</span></span> <span data-ttu-id="69925-138">Federasyon meta verilerinin kiracılar belirteç imzalama için kullanan sertifikaları ortak kısmını içerir.</span><span class="sxs-lookup"><span data-stu-id="69925-138">The federation metadata includes the public portion of the certificates that the tenants use for token signing.</span></span> <span data-ttu-id="69925-139">Sertifika ham bayt görünür `KeyDescriptor` öğesi.</span><span class="sxs-lookup"><span data-stu-id="69925-139">The certificate raw bytes appear in the `KeyDescriptor` element.</span></span> <span data-ttu-id="69925-140">Belirteç imzalama sertifikasının yalnızca imzalamak için geçerli değeri `use` özniteliği `signing`.</span><span class="sxs-lookup"><span data-stu-id="69925-140">The token signing certificate is valid for signing only when the value of the `use` attribute is `signing`.</span></span>

<span data-ttu-id="69925-141">Azure AD tarafından yayınlanan Federasyon meta veri belgesi imzalama sertifikasını güncelleştirmek Azure AD zaman hazırlama gibi birden çok imzalama anahtarı olabilir.</span><span class="sxs-lookup"><span data-stu-id="69925-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing to update the signing certificate.</span></span> <span data-ttu-id="69925-142">Federasyon meta veri belgesi birden fazla sertifika bulunuyorsa, belirteçleri doğrularken bir hizmet belgesinde tüm sertifikaları desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="69925-142">When a federation metadata document includes more than one certificate, a service that is validating the tokens should support all certificates in the document.</span></span>

<span data-ttu-id="69925-143">Aşağıdaki meta verileri bir örnek göstermektedir `KeyDescriptor` imzalama anahtarı ile öğesi.</span><span class="sxs-lookup"><span data-stu-id="69925-143">The following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

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

<span data-ttu-id="69925-144">`KeyDescriptor` Öğe Federasyon meta veri belgesi; WS-Federasyon özgü bölüm ve SAML özgü bölümünde iki yerde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="69925-144">The `KeyDescriptor` element appears in two places in the federation metadata document; in the WS-Federation-specific section and the SAML-specific section.</span></span> <span data-ttu-id="69925-145">Her iki bölümlerde yayımlanan sertifikalar aynı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="69925-145">The certificates published in both sections will be the same.</span></span>

<span data-ttu-id="69925-146">WS-Federasyon özgü bölümünde bir WS-Federasyon meta veri okuyucusu sertifikalardan okuduğunuz bir `RoleDescriptor` öğeyle `SecurityTokenServiceType` türü.</span><span class="sxs-lookup"><span data-stu-id="69925-146">In the WS-Federation-specific section, a WS-Federation metadata reader would read the certificates from a `RoleDescriptor` element with the `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="69925-147">Aşağıdaki meta verileri bir örnek göstermektedir `RoleDescriptor` öğesi.</span><span class="sxs-lookup"><span data-stu-id="69925-147">The following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="69925-148">SAML özgü bölümünde bir WS-Federasyon meta veri okuyucusu sertifikalardan okuduğunuz bir `IDPSSODescriptor` öğesi.</span><span class="sxs-lookup"><span data-stu-id="69925-148">In the SAML-specific section, a WS-Federation metadata reader would read the certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="69925-149">Aşağıdaki meta verileri bir örnek göstermektedir `IDPSSODescriptor` öğesi.</span><span class="sxs-lookup"><span data-stu-id="69925-149">The following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="69925-150">Kiracı özgü ve Kiracı bağımsız sertifikaların biçiminde farklılıkları yoktur.</span><span class="sxs-lookup"><span data-stu-id="69925-150">There are no differences in the format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="69925-151">WS-Federasyon uç nokta URL'si</span><span class="sxs-lookup"><span data-stu-id="69925-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="69925-152">Federasyon meta verilerini Azure AD kullanımları tek oturum açma ve WS-Federasyon protokolünde oturum kapatma tek URL içerir.</span><span class="sxs-lookup"><span data-stu-id="69925-152">The federation metadata includes the URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="69925-153">Bu uç noktaya görünür `PassiveRequestorEndpoint` öğesi.</span><span class="sxs-lookup"><span data-stu-id="69925-153">This endpoint appears in the `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="69925-154">Aşağıdaki meta verileri bir örnek göstermektedir `PassiveRequestorEndpoint` öğesi için bir kiracı özel uç noktası.</span><span class="sxs-lookup"><span data-stu-id="69925-154">The following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="69925-155">Kiracı bağımsız uç noktası için WS-Federasyon URL WS-Federasyon uç aşağıdaki örnekte gösterildiği gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="69925-155">For the tenant-independent endpoint, the WS-Federation URL appears in the WS-Federation endpoint, as shown in the following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="69925-156">SAML Protokolü uç nokta URL'si</span><span class="sxs-lookup"><span data-stu-id="69925-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="69925-157">Federasyon meta verilerinin tek oturum açma ve tek SAML 2.0 protokolü oturum kapatma için Azure AD kullanır URL'sini içerir.</span><span class="sxs-lookup"><span data-stu-id="69925-157">The federation metadata includes the URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="69925-158">Bu uç noktalar görünür `IDPSSODescriptor` öğesi.</span><span class="sxs-lookup"><span data-stu-id="69925-158">These endpoints appear in the `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="69925-159">Oturum açma ve oturum kapatma URL'leri görünür `SingleSignOnService` ve `SingleLogoutService` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="69925-159">The sign-in and sign-out URLs appear in the `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="69925-160">Aşağıdaki meta verileri bir örnek göstermektedir `PassiveResistorEndpoint` Kiracı özgü uç noktası için.</span><span class="sxs-lookup"><span data-stu-id="69925-160">The following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="69925-161">Benzer şekilde uç noktaları ortak SAML 2.0 protokolü uç noktaları için aşağıdaki örnekte gösterildiği gibi Kiracı bağımsız Federasyon meta verilerinde yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="69925-161">Similarly the endpoints for the common SAML 2.0 protocol endpoints are published in the tenant-independent federation metadata, as shown in the following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
