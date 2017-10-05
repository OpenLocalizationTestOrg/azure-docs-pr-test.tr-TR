---
title: "Azure MFA ve AD FS ile bulut kaynaklarını güvenli hale getirme | Microsoft Docs"
description: "Bu, bulutta nasıl Azure MFA ve AD FS kullanmaya başlayacağınızı açıklayan Azure Multi-Factor Authentication sayfasıdır."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 6cf4ec4f777ea1f2b852945ab82da2547946f378
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="62248-103">Azure Multi-Factor Authentication ve AD FS ile bulut kaynaklarını güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="62248-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="62248-104">Kuruluşunuz Azure Active Directory ile birleştiriliyorsa, Azure AD’nin erişebildiği kaynakları güvenli hale getirmek için Azure Multi-Factor Authentication ya da Active Directory Federation Services (AD FS) kullanın.</span><span class="sxs-lookup"><span data-stu-id="62248-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) to secure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="62248-105">Azure Active Directory kaynaklarını Azure Multi-Factor Authentication ya da Active Directory Federasyon Hizmetleri ile güvenli hale getirmek için aşağıdaki yordamları kullanın.</span><span class="sxs-lookup"><span data-stu-id="62248-105">Use the following procedures to secure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="62248-106">AD FS kullanarak Azure AD kaynaklarını güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="62248-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="62248-107">Bulut kaynağınızın güvenliğini sağlamak için, kullanıcı iki adımlı doğrulamayı başarıyla gerçekleştirdiğinde Active Directory Federation Services tarafından multipleauthn talebinin yayılması için bir talep kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62248-107">To secure your cloud resource, set up a claims rule so that Active Directory Federation Services emits the multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="62248-108">Bu talep Azure AD'ye aktarılır.</span><span class="sxs-lookup"><span data-stu-id="62248-108">This claim is passed on to Azure AD.</span></span> <span data-ttu-id="62248-109">İlerlemek için bu yordamı izleyin:</span><span class="sxs-lookup"><span data-stu-id="62248-109">Follow this procedure to walk through the steps:</span></span>


1. <span data-ttu-id="62248-110">AD FS Yönetimi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="62248-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="62248-111">Solda, **Bağlı Olan Taraf Güvenleri**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="62248-111">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="62248-112">**Microsoft Office 365 Kimlik Platformu**'na sağ tıklayın ve **Talep Kurallarını Düzenle**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="62248-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="62248-114">Verme Dönüştürme Kuralları’nda **Kural Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62248-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="62248-116">Dönüştürme Kuralı Ekleme Sihirbazı’nda, açılır menüde **Gelen Talep için Geçiş ya da Filtre**’yi seçin ve **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62248-116">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>

   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="62248-118">Kuralınıza bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="62248-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="62248-119">Gelen talep türü olarak **Kimlik Doğrulama Yöntemleri Başvuruları**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="62248-119">Select **Authentication Methods References** as the Incoming claim type.</span></span>
8. <span data-ttu-id="62248-120">**Tüm talep değerlerini geçir**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="62248-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="62248-121">![Dönüşüm Talep Kuralı Ekleme Sihirbazı](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="62248-121">![Add Transform Claim Rule Wizard](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="62248-122">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62248-122">Click **Finish**.</span></span> <span data-ttu-id="62248-123">AD FS Yönetim Konsolu'nu kapatın.</span><span class="sxs-lookup"><span data-stu-id="62248-123">Close the AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="62248-124">Federasyon kullanıcıları için Güvenilen IP'ler</span><span class="sxs-lookup"><span data-stu-id="62248-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="62248-125">Güvenilen IP'ler yöneticilerin, belirli IP adresleri ya da kendi intranetlerinden kaynaklanan taleplere sahip federasyon kullanıcıları için iki aşamalı doğrulamayı atlamasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="62248-125">Trusted IPs allow administrators to by-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="62248-126">Aşağıdaki bölümlerde, federasyon kullanıcıları intranetinden gelen talepler için Azure Multi-Factor Authentication Güvenilen IP’lerinin federasyon kullanıcılarıyla yapılandırılması ve iki aşamalı doğrulamanın atlanması açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="62248-126">The following sections describe how to configure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="62248-127">Bu, AD FS’nin bir geçiş kullanacak ya da Kurumsal Ağ İçinde talep türü ile gelen bir talep şablonunu filtreleyecek şekilde yapılandırılmasıyla gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="62248-127">This is achieved by configuring AD FS to use a pass-through or filter an incoming claim template with the Inside Corporate Network claim type.</span></span>

<span data-ttu-id="62248-128">Bu örnekte Güvenilen Taraf Güvenlerimiz için Office 365 kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="62248-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-the-ad-fs-claims-rules"></a><span data-ttu-id="62248-129">AD FS talep kurallarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="62248-129">Configure the AD FS claims rules</span></span>
<span data-ttu-id="62248-130">Yapmamız gereken ilk şey, AD FS taleplerini yapılandırmaktır.</span><span class="sxs-lookup"><span data-stu-id="62248-130">The first thing we need to do is to configure the AD FS claims.</span></span> <span data-ttu-id="62248-131">Biri Kurumsal Ağ İçinde talep türü için, diğeriyse kullanıcıların oturumunu açık şekilde tutmak için olmak üzere iki talep kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62248-131">Create two claims rules, one for the Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="62248-132">AD FS Yönetimi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="62248-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="62248-133">Solda, **Bağlı Olan Taraf Güvenleri**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="62248-133">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="62248-134">**Microsoft Office 365 Kimlik Platformu**’na sağ tıklayın ve **Talep Kurallarını Düzenle…** seçeneğini belirleyin.
   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="62248-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="62248-135">Verme Dönüştürme Kuralları’nda **Kural Ekle**’ye tıklayın.
   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="62248-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="62248-136">Dönüştürme Kuralı Ekleme Sihirbazı’nda, açılır menüde **Gelen Talep için Geçiş ya da Filtre**’yi seçin ve **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62248-136">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>
   <span data-ttu-id="62248-137">![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="62248-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="62248-138">Talep kuralı adının yanındaki kutuda kuralınıza bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="62248-138">In the box next to Claim rule name, give your rule a name.</span></span> <span data-ttu-id="62248-139">Örneğin: InsideCorpNet.</span><span class="sxs-lookup"><span data-stu-id="62248-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="62248-140">Gelen talep türü’nün yanındaki açılır menüde, **Kurumsal Ağ İçinde** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="62248-140">From the drop-down, next to Incoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="62248-141">![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="62248-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="62248-142">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62248-142">Click **Finish**.</span></span>
9. <span data-ttu-id="62248-143">Verme Dönüştürme Kuralları’nda **Kural Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62248-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="62248-144">Dönüştürme Kuralı Ekleme Sihirbazı’nda, açılır menüden **Talepleri Özel Bir Kural Kullanarak Gönder**’i seçin ve **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62248-144">On the Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from the drop-down and click **Next**.</span></span>
11. <span data-ttu-id="62248-145">Talep kuralı adı: altındaki kutuya *Kullanıcıların Oturumlarını Açık Tut* ifadesini girin.</span><span class="sxs-lookup"><span data-stu-id="62248-145">In the box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="62248-146">Özel kural kutusuna şunu girin:</span><span class="sxs-lookup"><span data-stu-id="62248-146">In the Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="62248-148">**Finish (Son)** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62248-148">Click **Finish**.</span></span>
14. <span data-ttu-id="62248-149">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62248-149">Click **Apply**.</span></span>
15. <span data-ttu-id="62248-150">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62248-150">Click **Ok**.</span></span>
16. <span data-ttu-id="62248-151">AD FS Yönetimi'ni kapatın.</span><span class="sxs-lookup"><span data-stu-id="62248-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="62248-152">Azure Multi-Factor Authentication Güvenilen IP’leri Federasyon Kullanıcıları ile Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="62248-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="62248-153">Talepler yapıldığına göre, artık güvenilen IP’leri yapılandırabiliriz.</span><span class="sxs-lookup"><span data-stu-id="62248-153">Now that the claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="62248-154">[Klasik Azure portalında](https://manage.windowsazure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="62248-154">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="62248-155">Solda, **Active Directory**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62248-155">On the left, click **Active Directory**.</span></span>
3. <span data-ttu-id="62248-156">Dizin altında, güvenilen IP'leri ayarlamak istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="62248-156">Under Directory, select the directory where you want to set up trusted IPs.</span></span>
4. <span data-ttu-id="62248-157">Seçtiğiniz Dizinde **Yapılandır**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62248-157">On the Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="62248-158">Çok faktörlü kimlik doğrulaması bölümünde, **Hizmet ayarlarını yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62248-158">In the multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="62248-159">Hizmet Ayarları sayfasındaki güvenilen IP'ler altında bulunan **İntranetimde bulunan şirket dışındaki kullanıcıların istekleri için çok öğeli kimlik doğrulamayı atla** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="62248-159">On the Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  

   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. <span data-ttu-id="62248-161">**Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62248-161">Click **save**.</span></span>
8. <span data-ttu-id="62248-162">Güncelleştirmeler uygulandıktan sonra **Kapat**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62248-162">Once the updates have been applied, click **close**.</span></span>

<span data-ttu-id="62248-163">Bu kadar!</span><span class="sxs-lookup"><span data-stu-id="62248-163">That’s it!</span></span> <span data-ttu-id="62248-164">Bu noktada, birleştirilmiş Office 365 kullanıcıları yalnızca talep kurumsal intranet dışından kaynaklandığı zaman MFA kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="62248-164">At this point, federated Office 365 users should only have to use MFA when a claim originates from outside the corporate intranet.</span></span>
