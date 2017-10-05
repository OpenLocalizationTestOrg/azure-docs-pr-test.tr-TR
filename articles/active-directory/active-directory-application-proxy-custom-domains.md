---
title: "Azure AD uygulama proxy'si özel etki alanlarında | Microsoft Docs"
description: "Uygulama için URL'yi, kullanıcılarınıza eriştiği bakılmaksızın aynı böylece Azure AD uygulama proxy'si özel etki alanlarında yönetin."
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
ms.openlocfilehash: 1dde300780c8d1f7ea9eee4c92de06bcf70a1f12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="98153-103">Azure AD uygulama proxy'si özel etki alanları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="98153-103">Working with custom domains in Azure AD Application Proxy</span></span>

<span data-ttu-id="98153-104">Azure Active Directory Uygulama proxy'si aracılığıyla uygulama yayımladığınızda, kullanıcılarınız uzaktan çalışırken gitmek için bir dış URL oluşturun.</span><span class="sxs-lookup"><span data-stu-id="98153-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users to go to when they're working remotely.</span></span> <span data-ttu-id="98153-105">Varsayılan etki alanını bu URL'yi alır *yourtenant.msappproxy.net*.</span><span class="sxs-lookup"><span data-stu-id="98153-105">This URL gets the default domain *yourtenant.msappproxy.net*.</span></span> <span data-ttu-id="98153-106">Gider ve Kiracı adlı bir uygulama yayımladıysanız dış URL'yi https://expenses-contoso.msappproxy.net olacaktır sonra Örneğin, Contoso adlı.</span><span class="sxs-lookup"><span data-stu-id="98153-106">For example, if you published an app named Expenses and your tenant is named Contoso, then the external URL would be https://expenses-contoso.msappproxy.net.</span></span> <span data-ttu-id="98153-107">Kendi etki alanı adınızı kullanmak istiyorsanız, uygulamanız için özel bir etki alanı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="98153-107">If you want to use your own domain name, configure a custom domain for your application.</span></span> 

<span data-ttu-id="98153-108">Mümkün olduğunda, uygulamalarınız için özel etki alanları ayarlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="98153-108">We recommend that you set up custom domains for your applications whenever possible.</span></span> <span data-ttu-id="98153-109">Özel etki alanlarını avantajlarından bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="98153-109">Some of the benefits of custom domains include:</span></span>

- <span data-ttu-id="98153-110">İçinde veya ağınızın dışındaki çalıştıkları olup olmadığını, kullanıcılarınızın uygulamaya aynı URL'ye sahip alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98153-110">Your users can get to the application with the same URL, whether they are working inside or outside of your network.</span></span>
- <span data-ttu-id="98153-111">Tüm uygulamalar aynı iç ve dış URL'ler varsa, başka bir işaret eden bir uygulama bağlantılar, kurumsal ağ dışından bile çalışmaya devam.</span><span class="sxs-lookup"><span data-stu-id="98153-111">If all of your applications have the same internal and external URLs, then links in one application that point to another continue to work even outside the corporate network.</span></span> 
- <span data-ttu-id="98153-112">Marka bilgilerinizi denetlemek ve istediğiniz URL'leri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="98153-112">You control your branding, and create the URLs you want.</span></span> 


## <a name="configure-a-custom-domain"></a><span data-ttu-id="98153-113">Özel bir etki alanı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="98153-113">Configure a custom domain</span></span>

### <a name="prerequisites"></a><span data-ttu-id="98153-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="98153-114">Prerequisites</span></span>

<span data-ttu-id="98153-115">Özel bir etki alanı yapılandırmadan önce hazırlanan aşağıdaki gereksinimlere sahip olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="98153-115">Before you configure a custom domain, make sure that you have the following requirements prepared:</span></span> 
- <span data-ttu-id="98153-116">A [Azure Active Directory'ye eklenen etki alanını doğruladıysanız](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="98153-116">A [verified domain added to Azure Active Directory](active-directory-domains-add-azure-portal.md).</span></span>
- <span data-ttu-id="98153-117">Bir PFX dosyası biçiminde etki alanı için özel bir sertifika.</span><span class="sxs-lookup"><span data-stu-id="98153-117">A custom certificate for the domain, in the form of a PFX file.</span></span> 
- <span data-ttu-id="98153-118">Bir şirket içi uygulama [uygulaması Proxy üzerinden yayımlanan](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="98153-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

### <a name="configure-your-custom-domain"></a><span data-ttu-id="98153-119">Özel etki alanınızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="98153-119">Configure your custom domain</span></span>

<span data-ttu-id="98153-120">Bu üç gereksinimleri hazır olduğunda, özel etki alanı oluşturmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="98153-120">When you have those three requirements ready, follow these steps to set up your custom domain:</span></span>

1. <span data-ttu-id="98153-121">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="98153-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="98153-122">Gidin **Azure Active Directory** > **kurumsal uygulamalar** > **tüm uygulamaları** ve yönetmek istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="98153-122">Navigate to **Azure Active Directory** > **Enterprise applications** > **All applications** and choose the app you want to manage.</span></span>
3. <span data-ttu-id="98153-123">Seçin **uygulama proxy'si**.</span><span class="sxs-lookup"><span data-stu-id="98153-123">Select **Application Proxy**.</span></span> 
4. <span data-ttu-id="98153-124">Dış URL alanında açılır listeden özel etki alanınızı seçmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="98153-124">In the External URL field, use the dropdown list to select your custom domain.</span></span> <span data-ttu-id="98153-125">Listede etki alanınızı görmüyorsanız, ardından bunu henüz doğrulanmış kurmadı.</span><span class="sxs-lookup"><span data-stu-id="98153-125">If you don't see your domain in the list, then it hasn't been verified yet.</span></span> 
5. <span data-ttu-id="98153-126">Seçin **Kaydet**</span><span class="sxs-lookup"><span data-stu-id="98153-126">Select **Save**</span></span>
5. <span data-ttu-id="98153-127">**Sertifika** hale devre dışı bırakıldı alan etkin.</span><span class="sxs-lookup"><span data-stu-id="98153-127">The **Certificate** field that was disabled becomes enabled.</span></span> <span data-ttu-id="98153-128">Bu alanı seçin.</span><span class="sxs-lookup"><span data-stu-id="98153-128">Select this field.</span></span> 

   ![Bir sertifikayı karşıya yüklemek için tıklayın](./media/active-directory-application-proxy-custom-domains/certificate.png)

   <span data-ttu-id="98153-130">Bu etki alanı için bir sertifika Karşıya zaten sertifika alanındaki sertifika bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="98153-130">If you already uploaded a certificate for this domain, the Certificate field displays the certificate information.</span></span> 

6. <span data-ttu-id="98153-131">PFX sertifikasını karşıya yükleyin ve sertifikanın parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="98153-131">Upload the PFX certificate and enter the password for the certificate.</span></span> 
7. <span data-ttu-id="98153-132">Seçin **kaydetmek** yaptığınız değişiklikleri kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="98153-132">Select **Save** to save your changes.</span></span> 
8. <span data-ttu-id="98153-133">Ekleme bir [DNS kaydı](../dns/dns-operations-recordsets-portal.md) yeni dış URL msappproxy.net etki alanına yeniden yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="98153-133">Add a [DNS record](../dns/dns-operations-recordsets-portal.md) that redirects the new external URL to the msappproxy.net domain.</span></span> 

>[!TIP] 
><span data-ttu-id="98153-134">Özel etki alanı başına bir sertifika karşıya yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="98153-134">You only need to upload one certificate per custom domain.</span></span> <span data-ttu-id="98153-135">Bir sertifika karşıya yükledikten sonra yeni bir uygulama yayımlama ve DNS kaydı dışında ek yapılandırma gerekmez, özel etki alanı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98153-135">Once you upload a certificate, you can choose the custom domain when you publish a new app and not have to do additional configuration except for the DNS record.</span></span> 

## <a name="manage-certificates"></a><span data-ttu-id="98153-136">Sertifikaları yönetme</span><span class="sxs-lookup"><span data-stu-id="98153-136">Manage certificates</span></span>

### <a name="certificate-format"></a><span data-ttu-id="98153-137">Sertifika biçimi</span><span class="sxs-lookup"><span data-stu-id="98153-137">Certificate format</span></span>
<span data-ttu-id="98153-138">Sertifika imza yöntemleri sınırlaması yoktur.</span><span class="sxs-lookup"><span data-stu-id="98153-138">There is no restriction on the certificate signature methods.</span></span> <span data-ttu-id="98153-139">Tüm Eliptik Eğri Şifrelemesi (ECC), konu alternatif adı (SAN) ve diğer ortak sertifika türleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="98153-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span></span> 

<span data-ttu-id="98153-140">İstenen dış URL'yi joker eşleştiği sürece bir joker sertifikası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98153-140">You can use a wildcard certificate as long as the wildcard matches the desired external URL.</span></span> 

<span data-ttu-id="98153-141">Otomatik olarak imzalanan sertifikalar, de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98153-141">You can use self-signed certificates, as well.</span></span> <span data-ttu-id="98153-142">Özel sertifika yetkilisi kullanıyorsanız, sertifika için CDP (sertifika iptal noktası dağıtım noktası) ortak olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="98153-142">If you’re using a private certificate authority, the CDP (certificate revocation point distribution point) for the certificate should be public.</span></span>

### <a name="changing-the-domain"></a><span data-ttu-id="98153-143">Etki alanını değiştirme</span><span class="sxs-lookup"><span data-stu-id="98153-143">Changing the domain</span></span>
<span data-ttu-id="98153-144">Tüm doğrulanmış etki alanları, uygulamanız için dış URL'yi açılır listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="98153-144">All verified domains appear in the External URL dropdown list for your application.</span></span> <span data-ttu-id="98153-145">Etki alanını değiştirmek için yalnızca bu alan uygulama için güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="98153-145">To change the domain, just update that field for the application.</span></span> <span data-ttu-id="98153-146">İstediğiniz etki alanının listede yoksa [doğrulanmış bir etki alanına eklemek](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="98153-146">If the domain you want isn't in the list, [add it as a verified domain](active-directory-domains-add-azure-portal.md).</span></span> <span data-ttu-id="98153-147">İlişkili bir sertifikanız henüz, sertifika eklemek için 5-7 adımları bir etki alanı seçerseniz.</span><span class="sxs-lookup"><span data-stu-id="98153-147">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 to add the certificate.</span></span> <span data-ttu-id="98153-148">Ardından, yeni dış URL'yi yeniden yönlendirmek için DNS kaydı güncelleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="98153-148">Then, make sure you update the DNS record to redirect from the new external URL.</span></span> 

### <a name="certificate-management"></a><span data-ttu-id="98153-149">Sertifika yönetimi</span><span class="sxs-lookup"><span data-stu-id="98153-149">Certificate management</span></span>
<span data-ttu-id="98153-150">Bir dış ana bilgisayarda uygulamaları paylaşmak sürece birden çok uygulama için aynı sertifikayı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98153-150">You can use the same certificate for multiple applications unless the applications share an external host.</span></span> 

<span data-ttu-id="98153-151">Bir sertifikanın süresi dolduğunda, portal üzerinden başka bir sertifikayı karşıya yüklemek için bildiren bir uyarı alın.</span><span class="sxs-lookup"><span data-stu-id="98153-151">You get a warning when a certificate expires, telling you to upload another certificate through the portal.</span></span> <span data-ttu-id="98153-152">Sertifika iptal edilirse, kullanıcılarınızın uygulama erişirken bir güvenlik uyarısı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98153-152">If the certificate is revoked, your users may see a security warning when accessing the application.</span></span> <span data-ttu-id="98153-153">Biz için sertifikalar iptal denetimlerini yerine getirmiyor.</span><span class="sxs-lookup"><span data-stu-id="98153-153">We don’t perform revocation checks for certificates.</span></span>  <span data-ttu-id="98153-154">Belirli bir uygulamada bir sertifikayı güncelleştirmek için uygulamaya gidin ve yeni sertifikayı karşıya yüklemek için yayımlanan uygulamalar özel etki alanlarını yapılandırma için 5-7 adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="98153-154">To update the certificate for a given application, navigate to the application and follow steps 5-7 for configuring custom domains on published applications to upload a new certificate.</span></span> <span data-ttu-id="98153-155">Eski sertifikayı diğer uygulamalar tarafından kullanılmadığından, otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="98153-155">If the old certificate is not being used by other applications, it is deleted automatically.</span></span> 

<span data-ttu-id="98153-156">Şu anda sertifikalar ilgili uygulamalar bağlamında yönetmeniz gereken tüm sertifika yönetimi tek tek uygulama sayfaları olduğundan.</span><span class="sxs-lookup"><span data-stu-id="98153-156">Currently all certificate management is through individual application pages so you need to manage certificates in the context of the relevant applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="98153-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="98153-157">Next steps</span></span>
* <span data-ttu-id="98153-158">[Çoklu oturum açmayı etkinleştir](active-directory-application-proxy-sso-using-kcd.md) yayımlanan uygulamalarınızı Azure AD kimlik doğrulamasına sahip.</span><span class="sxs-lookup"><span data-stu-id="98153-158">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) to your published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="98153-159">[Koşullu erişimi etkinleştirme](active-directory-application-proxy-conditional-access.md) , yayımlanan uygulamalar için.</span><span class="sxs-lookup"><span data-stu-id="98153-159">[Enable conditional access](active-directory-application-proxy-conditional-access.md) to your published apps.</span></span>
* [<span data-ttu-id="98153-160">Azure AD ile özel etki alanı adınızı ekleme</span><span class="sxs-lookup"><span data-stu-id="98153-160">Add your custom domain name to Azure AD</span></span>](active-directory-domains-add-azure-portal.md)


