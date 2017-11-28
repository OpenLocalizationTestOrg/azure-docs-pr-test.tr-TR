---
title: Uygulama proxy'si uygulama aaaHow tooconfigure | Microsoft Docs
description: "Bilgi nasıl toocreate bir yapılandırma birkaç basit adımda bir uygulama proxy'si uygulama"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a><span data-ttu-id="7f2c0-103">Nasıl tooconfigure uygulama proxy'si uygulama</span><span class="sxs-lookup"><span data-stu-id="7f2c0-103">How tooconfigure an Application Proxy application</span></span>

<span data-ttu-id="7f2c0-104">Bu makale toounderstand yardımcı nasıl tooconfigure bir Azure AD tooexpose uygulama proxy'si uygulamadaki şirket içi uygulamalar toohello bulut.</span><span class="sxs-lookup"><span data-stu-id="7f2c0-104">This article help you toounderstand how tooconfigure an Application Proxy application within Azure AD tooexpose your on-premises applications toohello cloud.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="7f2c0-105">Önerilen belgeler</span><span class="sxs-lookup"><span data-stu-id="7f2c0-105">Recommended documents</span></span> 

<span data-ttu-id="7f2c0-106">Merhaba başlangıç yapılandırmasını ve hello Yönetici portalı üzerinden bir uygulama proxy'si uygulama oluşturma hakkında toolearn izleyin hello [Azure AD uygulama proxy'si ile uygulama yayımlama](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="7f2c0-106">toolearn about hello initial configurations and creation of an Application Proxy application through hello Admin Portal, follow hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="7f2c0-107">Bağlayıcılar yapılandırma hakkında daha fazla bilgi için bkz [uygulama ara sunucusunu etkinleştirme hello Azure portal](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="7f2c0-107">For details on configuring Connectors, see [Enable Application Proxy in hello Azure portal](active-directory-application-proxy-enable.md).</span></span>

<span data-ttu-id="7f2c0-108">Sertifikaları karşıya yükleniyor ve özel etki alanlarını kullanma hakkında daha fazla bilgi için bkz: [Azure AD uygulama proxy'si özel etki alanları ile çalışma](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="7f2c0-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span>

## <a name="create-hello-applicationsetting-hello-urls"></a><span data-ttu-id="7f2c0-109">Uygulama/ayarı hello URL'leri Hello oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f2c0-109">Create hello Application/Setting hello URLs</span></span>

<span data-ttu-id="7f2c0-110">Merhaba, izliyorsanız hello adımları [Azure AD uygulama proxy'si ile uygulama yayımlama](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) belgelerine ve bu Merhaba uygulaması oluşturulurken bir hata alma hello hata ayrıntıları için bilgi ve ilgili öneriler bakın toofix Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="7f2c0-110">If you are following hello steps in hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating hello application, see hello error details for information and suggestions for how toofix hello application.</span></span> <span data-ttu-id="7f2c0-111">Çoğu hata iletileri önerilen bir düzeltmeyi içerir.</span><span class="sxs-lookup"><span data-stu-id="7f2c0-111">Most error messages include a suggested fix.</span></span> <span data-ttu-id="7f2c0-112">tooavoid sık karşılaşılan doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="7f2c0-112">tooavoid common errors, verify:</span></span>

-   <span data-ttu-id="7f2c0-113">Bir yönetici izni toocreate uygulama proxy'si uygulama ile</span><span class="sxs-lookup"><span data-stu-id="7f2c0-113">You are an administrator with permission toocreate an Application Proxy application</span></span>

-   <span data-ttu-id="7f2c0-114">Merhaba İç URL benzersizdir</span><span class="sxs-lookup"><span data-stu-id="7f2c0-114">hello internal URL is unique</span></span>

-   <span data-ttu-id="7f2c0-115">Merhaba dış URL benzersizdir</span><span class="sxs-lookup"><span data-stu-id="7f2c0-115">hello external URL is unique</span></span>

-   <span data-ttu-id="7f2c0-116">http veya https URL'leri başlangıcı hello ve sonunda bir "/"</span><span class="sxs-lookup"><span data-stu-id="7f2c0-116">hello URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="7f2c0-117">Merhaba URL bir etki alanı adı, IP adresi olmalıdır</span><span class="sxs-lookup"><span data-stu-id="7f2c0-117">hello URL should be a domain name, not an IP address</span></span>

<span data-ttu-id="7f2c0-118">Merhaba uygulaması oluşturduğunuzda hello sağ üst köşedeki hello hata iletisi görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="7f2c0-118">hello error message should display in hello top right corner when you create hello application.</span></span> <span data-ttu-id="7f2c0-119">Merhaba bildirim simgesine toosee hello hata iletileri de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f2c0-119">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Bildirim istemi](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a><span data-ttu-id="7f2c0-121">Bağlayıcılar/bağlayıcı gruplarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7f2c0-121">Configure connectors/connector groups</span></span>

<span data-ttu-id="7f2c0-122">Merhaba bağlayıcılar ve bağlayıcı grupları hakkında uyarı nedeniyle, uygulamanızın yapılandırma zorluk yaşıyorsanız, hakkında ayrıntılar için uygulama proxy'si etkinleştirme hakkında yönergeler Bkz: toodownload bağlayıcılar.</span><span class="sxs-lookup"><span data-stu-id="7f2c0-122">If you are having difficulty configuring your application because of warning about hello connectors and connector groups, see instructions on enabling Application Proxy for details on how toodownload connectors.</span></span> <span data-ttu-id="7f2c0-123">Merhaba toolearn bağlayıcılar hakkında daha fazla bilgi istiyorsanız bkz [bağlayıcılar belgelerine](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span><span class="sxs-lookup"><span data-stu-id="7f2c0-123">If you want toolearn more about connectors, see hello [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span></span>

<span data-ttu-id="7f2c0-124">Bağlayıcılar etkin olmayan, bu oluşturulamıyor tooreach hello hizmet oldukları anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7f2c0-124">If your connectors are inactive, this means that they are unable tooreach hello service.</span></span> <span data-ttu-id="7f2c0-125">Bu, genellikle tüm gereken hello bağlantı noktalarının açık olmadığından olur.</span><span class="sxs-lookup"><span data-stu-id="7f2c0-125">This is often because all hello required ports are not open.</span></span> <span data-ttu-id="7f2c0-126">toosee gerekli bağlantı noktalarının listesi, uygulama proxy'si belgelerine etkinleştirme hello hello ön koşullar bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="7f2c0-126">toosee a list of required ports, see hello pre-requisites section of hello enabling Application Proxy documentation.</span></span>

## <a name="upload-certificates-for-custom-domains"></a><span data-ttu-id="7f2c0-127">Özel etki alanları için sertifikalarını karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="7f2c0-127">Upload certificates for custom domains</span></span>

<span data-ttu-id="7f2c0-128">Özel etki alanları, dış URL'ler toospecify hello etki alanını sağlar.</span><span class="sxs-lookup"><span data-stu-id="7f2c0-128">Custom Domains allow you toospecify hello domain of your external URLs.</span></span> <span data-ttu-id="7f2c0-129">toouse özel etki alanlarını, etki alanında tooupload hello sertifikası gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f2c0-129">toouse custom domains, you need tooupload hello certificate for that domain.</span></span> <span data-ttu-id="7f2c0-130">Özel etki alanları ve sertifikaları kullanma hakkında daha fazla bilgi için bkz: [Azure AD uygulama proxy'si özel etki alanları ile çalışma](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="7f2c0-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span> 

<span data-ttu-id="7f2c0-131">Sertifikanız karşıya sorunlarla karşılaşıyorsanız hello hata iletileri hello portalında hello sertifikasıyla hello sorun hakkında ek bilgi arayın.</span><span class="sxs-lookup"><span data-stu-id="7f2c0-131">If you are encountering issues uploading your certificate, look for hello error messages in hello portal for additional information on hello problem with hello certificate.</span></span> <span data-ttu-id="7f2c0-132">Ortak sertifika sorunları şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="7f2c0-132">Common certificate problems include:</span></span>

-   <span data-ttu-id="7f2c0-133">Süresi dolan sertifika</span><span class="sxs-lookup"><span data-stu-id="7f2c0-133">Expired certificate</span></span>

-   <span data-ttu-id="7f2c0-134">Otomatik olarak imzalanan sertifika</span><span class="sxs-lookup"><span data-stu-id="7f2c0-134">Certificate is self-signed</span></span>

-   <span data-ttu-id="7f2c0-135">Sertifika hello özel anahtarı eksik</span><span class="sxs-lookup"><span data-stu-id="7f2c0-135">Certificate is missing hello private key</span></span>

<span data-ttu-id="7f2c0-136">hello tooupload hello sertifika çalışırken sağ üst köşedeki içinde Hello hata iletisi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7f2c0-136">hello error message display in hello top right corner as you try tooupload hello certificate.</span></span> <span data-ttu-id="7f2c0-137">Merhaba bildirim simgesine toosee hello hata iletileri de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f2c0-137">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Bildirim istemi](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a><span data-ttu-id="7f2c0-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7f2c0-139">Next steps</span></span>
[<span data-ttu-id="7f2c0-140">Azure AD uygulama proxy'si ile uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="7f2c0-140">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
