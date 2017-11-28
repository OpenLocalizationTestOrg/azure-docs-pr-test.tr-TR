---
title: "Azure AD uygulama proxy'si aaaCustom alanlarında | Microsoft Docs"
description: "Azure AD uygulama proxy'si özel etki alanlarında olan hello uygulama için bu hello URL'yi hello şekilde aynı kullanıcılarınız, nerede erişim bağımsız olarak yönetin."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7a433c411976077210a2435c3c087991c7430755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="440b5-103">Azure AD uygulama proxy'si özel etki alanları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="440b5-103">Working with custom domains in Azure AD Application Proxy</span></span>

<span data-ttu-id="440b5-104">Azure Active Directory Uygulama proxy'si aracılığıyla uygulama yayımladığınızda, uzaktan çalışıyorsanız, kullanıcıların toogo toowhen için bir dış URL oluşturun.</span><span class="sxs-lookup"><span data-stu-id="440b5-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users toogo toowhen they're working remotely.</span></span> <span data-ttu-id="440b5-105">Bu URL'yi hello varsayılan etki alanı alır *yourtenant.msappproxy.net*.</span><span class="sxs-lookup"><span data-stu-id="440b5-105">This URL gets hello default domain *yourtenant.msappproxy.net*.</span></span> <span data-ttu-id="440b5-106">Örneğin, yayımladıysanız, bir uygulama giderleri adlı ve Kiracı Contoso adlı ardından hello dış URL https://expenses-contoso.msappproxy.net olacaktır.</span><span class="sxs-lookup"><span data-stu-id="440b5-106">For example, if you published an app named Expenses and your tenant is named Contoso, then hello external URL would be https://expenses-contoso.msappproxy.net.</span></span> <span data-ttu-id="440b5-107">Kendi etki alanı adınızı toouse istiyorsanız, uygulamanız için özel bir etki alanı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="440b5-107">If you want toouse your own domain name, configure a custom domain for your application.</span></span> 

<span data-ttu-id="440b5-108">Mümkün olduğunda, uygulamalarınız için özel etki alanları ayarlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="440b5-108">We recommend that you set up custom domains for your applications whenever possible.</span></span> <span data-ttu-id="440b5-109">Özel etki alanlarını hello avantajlarından bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="440b5-109">Some of hello benefits of custom domains include:</span></span>

- <span data-ttu-id="440b5-110">Kullanıcılarınızın toohello uygulamayla alabilirsiniz içinde veya ağınızın dışındaki çalıştıkları olup olmadığını aynı URL'ye hello.</span><span class="sxs-lookup"><span data-stu-id="440b5-110">Your users can get toohello application with hello same URL, whether they are working inside or outside of your network.</span></span>
- <span data-ttu-id="440b5-111">Tüm uygulamalarınızın sahip Merhaba, aynı iç ve dış URL'ler tooanother işaret eden bir uygulama bağlantıları toowork hello kurumsal ağ dışından bile devam edin.</span><span class="sxs-lookup"><span data-stu-id="440b5-111">If all of your applications have hello same internal and external URLs, then links in one application that point tooanother continue toowork even outside hello corporate network.</span></span> 
- <span data-ttu-id="440b5-112">Marka bilgilerinizi denetlemek ve istediğiniz hello URL'leri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="440b5-112">You control your branding, and create hello URLs you want.</span></span> 


## <a name="configure-a-custom-domain"></a><span data-ttu-id="440b5-113">Özel bir etki alanı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="440b5-113">Configure a custom domain</span></span>

### <a name="prerequisites"></a><span data-ttu-id="440b5-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="440b5-114">Prerequisites</span></span>

<span data-ttu-id="440b5-115">Özel bir etki alanı yapılandırmadan önce hello hazırlanmış gereksinimlerine sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="440b5-115">Before you configure a custom domain, make sure that you have hello following requirements prepared:</span></span> 
- <span data-ttu-id="440b5-116">A [doğrulanmış etki alanı eklenen tooAzure Active Directory](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="440b5-116">A [verified domain added tooAzure Active Directory](active-directory-domains-add-azure-portal.md).</span></span>
- <span data-ttu-id="440b5-117">Bir PFX dosyası hello biçiminde hello etki alanı için özel bir sertifika.</span><span class="sxs-lookup"><span data-stu-id="440b5-117">A custom certificate for hello domain, in hello form of a PFX file.</span></span> 
- <span data-ttu-id="440b5-118">Bir şirket içi uygulama [uygulaması Proxy üzerinden yayımlanan](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="440b5-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

### <a name="configure-your-custom-domain"></a><span data-ttu-id="440b5-119">Özel etki alanınızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="440b5-119">Configure your custom domain</span></span>

<span data-ttu-id="440b5-120">Bu üç gereksinimleri hazır olduğunda, bu adımları tooset özel etki alanınızı ayarlama izleyin:</span><span class="sxs-lookup"><span data-stu-id="440b5-120">When you have those three requirements ready, follow these steps tooset up your custom domain:</span></span>

1. <span data-ttu-id="440b5-121">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="440b5-121">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="440b5-122">Çok gidin**Azure Active Directory** > **kurumsal uygulamalar** > **tüm uygulamaları** ve hello uygulamayı seçin toomanage istiyor.</span><span class="sxs-lookup"><span data-stu-id="440b5-122">Navigate too**Azure Active Directory** > **Enterprise applications** > **All applications** and choose hello app you want toomanage.</span></span>
3. <span data-ttu-id="440b5-123">Seçin **uygulama proxy'si**.</span><span class="sxs-lookup"><span data-stu-id="440b5-123">Select **Application Proxy**.</span></span> 
4. <span data-ttu-id="440b5-124">Merhaba dış URL alanına hello açılır liste tooselect özel etki alanınızı kullanacak.</span><span class="sxs-lookup"><span data-stu-id="440b5-124">In hello External URL field, use hello dropdown list tooselect your custom domain.</span></span> <span data-ttu-id="440b5-125">Merhaba liste etki alanınızda görmüyorsanız, ardından bunu henüz doğrulanmış kurmadı.</span><span class="sxs-lookup"><span data-stu-id="440b5-125">If you don't see your domain in hello list, then it hasn't been verified yet.</span></span> 
5. <span data-ttu-id="440b5-126">Seçin **Kaydet**</span><span class="sxs-lookup"><span data-stu-id="440b5-126">Select **Save**</span></span>
5. <span data-ttu-id="440b5-127">Merhaba **sertifika** hale devre dışı bırakıldı alan etkin.</span><span class="sxs-lookup"><span data-stu-id="440b5-127">hello **Certificate** field that was disabled becomes enabled.</span></span> <span data-ttu-id="440b5-128">Bu alanı seçin.</span><span class="sxs-lookup"><span data-stu-id="440b5-128">Select this field.</span></span> 

   ![Bir sertifika tooupload tıklatın](./media/active-directory-application-proxy-custom-domains/certificate.png)

   <span data-ttu-id="440b5-130">Bu etki alanı için bir sertifika Karşıya zaten hello sertifika alanı hello sertifika bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="440b5-130">If you already uploaded a certificate for this domain, hello Certificate field displays hello certificate information.</span></span> 

6. <span data-ttu-id="440b5-131">Hello PFX sertifikasını karşıya yükleme ve hello sertifikanın hello parola girin.</span><span class="sxs-lookup"><span data-stu-id="440b5-131">Upload hello PFX certificate and enter hello password for hello certificate.</span></span> 
7. <span data-ttu-id="440b5-132">Seçin **kaydetmek** toosave değişikliklerinizi.</span><span class="sxs-lookup"><span data-stu-id="440b5-132">Select **Save** toosave your changes.</span></span> 
8. <span data-ttu-id="440b5-133">Ekleme bir [DNS kaydı](../dns/dns-operations-recordsets-portal.md) yeniden yönlendirmeleri yeni dış URL toohello msappproxy.net etki hello.</span><span class="sxs-lookup"><span data-stu-id="440b5-133">Add a [DNS record](../dns/dns-operations-recordsets-portal.md) that redirects hello new external URL toohello msappproxy.net domain.</span></span> 

>[!TIP] 
><span data-ttu-id="440b5-134">Özel etki alanı başına tooupload bir sertifika yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="440b5-134">You only need tooupload one certificate per custom domain.</span></span> <span data-ttu-id="440b5-135">Bir sertifika karşıya yükledikten sonra yeni bir uygulama yayımlama ve hello DNS kaydı dışında toodo ek yapılandırmaya sahip olmayan hello özel etki alanı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="440b5-135">Once you upload a certificate, you can choose hello custom domain when you publish a new app and not have toodo additional configuration except for hello DNS record.</span></span> 

## <a name="manage-certificates"></a><span data-ttu-id="440b5-136">Sertifikaları yönetme</span><span class="sxs-lookup"><span data-stu-id="440b5-136">Manage certificates</span></span>

### <a name="certificate-format"></a><span data-ttu-id="440b5-137">Sertifika biçimi</span><span class="sxs-lookup"><span data-stu-id="440b5-137">Certificate format</span></span>
<span data-ttu-id="440b5-138">Merhaba sertifika imza yöntemleri sınırlaması yoktur.</span><span class="sxs-lookup"><span data-stu-id="440b5-138">There is no restriction on hello certificate signature methods.</span></span> <span data-ttu-id="440b5-139">Tüm Eliptik Eğri Şifrelemesi (ECC), konu alternatif adı (SAN) ve diğer ortak sertifika türleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="440b5-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span></span> 

<span data-ttu-id="440b5-140">İstenen hello dış URL Hello joker eşleştiği sürece bir joker sertifikası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="440b5-140">You can use a wildcard certificate as long as hello wildcard matches hello desired external URL.</span></span> 

<span data-ttu-id="440b5-141">Otomatik olarak imzalanan sertifikalar, de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="440b5-141">You can use self-signed certificates, as well.</span></span> <span data-ttu-id="440b5-142">Özel sertifika yetkilisi kullanıyorsanız, hello CDP (sertifika iptal noktası dağıtım noktası) hello sertifikası için ortak olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="440b5-142">If you’re using a private certificate authority, hello CDP (certificate revocation point distribution point) for hello certificate should be public.</span></span>

### <a name="changing-hello-domain"></a><span data-ttu-id="440b5-143">Merhaba etki alanını değiştirme</span><span class="sxs-lookup"><span data-stu-id="440b5-143">Changing hello domain</span></span>
<span data-ttu-id="440b5-144">Tüm doğrulanmış etki hello dış URL aşağı açılan listesinde, uygulamanız için görünür.</span><span class="sxs-lookup"><span data-stu-id="440b5-144">All verified domains appear in hello External URL dropdown list for your application.</span></span> <span data-ttu-id="440b5-145">toochange hello etki alanı, hello uygulama için alan yalnızca güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="440b5-145">toochange hello domain, just update that field for hello application.</span></span> <span data-ttu-id="440b5-146">Merhaba etki hello listede yoksa [doğrulanmış bir etki alanına eklemek](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="440b5-146">If hello domain you want isn't in hello list, [add it as a verified domain](active-directory-domains-add-azure-portal.md).</span></span> <span data-ttu-id="440b5-147">İlişkili bir sertifika henüz sahip olmayan bir etki alanı seçin, adım 5-7 tooadd hello sertifika izleyin.</span><span class="sxs-lookup"><span data-stu-id="440b5-147">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 tooadd hello certificate.</span></span> <span data-ttu-id="440b5-148">Ardından, hello DNS kaydı tooredirect hello yeni dış URL'den güncelleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="440b5-148">Then, make sure you update hello DNS record tooredirect from hello new external URL.</span></span> 

### <a name="certificate-management"></a><span data-ttu-id="440b5-149">Sertifika yönetimi</span><span class="sxs-lookup"><span data-stu-id="440b5-149">Certificate management</span></span>
<span data-ttu-id="440b5-150">Bir dış konak hello uygulamaları paylaşmak sürece birden çok uygulama için aynı sertifika hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="440b5-150">You can use hello same certificate for multiple applications unless hello applications share an external host.</span></span> 

<span data-ttu-id="440b5-151">Bir sertifikanın süresi dolduğunda tooupload bildiren bir uyarı elde hello portalı üzerinden başka bir sertifika.</span><span class="sxs-lookup"><span data-stu-id="440b5-151">You get a warning when a certificate expires, telling you tooupload another certificate through hello portal.</span></span> <span data-ttu-id="440b5-152">Merhaba sertifika iptal edilirse, kullanıcılarınızın Merhaba uygulaması erişirken bir güvenlik uyarısı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="440b5-152">If hello certificate is revoked, your users may see a security warning when accessing hello application.</span></span> <span data-ttu-id="440b5-153">Biz için sertifikalar iptal denetimlerini yerine getirmiyor.</span><span class="sxs-lookup"><span data-stu-id="440b5-153">We don’t perform revocation checks for certificates.</span></span>  <span data-ttu-id="440b5-154">belirli bir uygulamada tooupdate hello sertifika toohello uygulama gidin ve yayımlanmış uygulamalar tooupload yeni bir sertifika özel etki alanlarını yapılandırma için 5-7 adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="440b5-154">tooupdate hello certificate for a given application, navigate toohello application and follow steps 5-7 for configuring custom domains on published applications tooupload a new certificate.</span></span> <span data-ttu-id="440b5-155">Merhaba eski sertifika diğer uygulamalar tarafından kullanılmadığından, otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="440b5-155">If hello old certificate is not being used by other applications, it is deleted automatically.</span></span> 

<span data-ttu-id="440b5-156">Şu anda hello ilgili uygulamalar Merhaba içeriğine toomanage sertifikaları gereksinim duyduğunuz tüm sertifika yönetimi tek tek uygulama sayfaları olduğundan.</span><span class="sxs-lookup"><span data-stu-id="440b5-156">Currently all certificate management is through individual application pages so you need toomanage certificates in hello context of hello relevant applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="440b5-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="440b5-157">Next steps</span></span>
* <span data-ttu-id="440b5-158">[Çoklu oturum açmayı etkinleştir](active-directory-application-proxy-sso-using-kcd.md) tooyour yayımlanan uygulamaları Azure AD kimlik doğrulaması ile.</span><span class="sxs-lookup"><span data-stu-id="440b5-158">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) tooyour published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="440b5-159">[Koşullu erişimi etkinleştirme](active-directory-application-proxy-conditional-access.md) tooyour yayımlanan uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="440b5-159">[Enable conditional access](active-directory-application-proxy-conditional-access.md) tooyour published apps.</span></span>
* [<span data-ttu-id="440b5-160">Özel etki alanı adı tooAzure AD ekleyin</span><span class="sxs-lookup"><span data-stu-id="440b5-160">Add your custom domain name tooAzure AD</span></span>](active-directory-domains-add-azure-portal.md)


