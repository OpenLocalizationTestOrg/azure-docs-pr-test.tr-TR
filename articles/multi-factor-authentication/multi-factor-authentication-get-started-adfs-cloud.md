---
title: "Azure MFA ve AD FS ile aaaSecure bulut kaynaklarına | Microsoft Docs"
description: "Bu Azure MFA ve AD FS hello bulutta tooget nasıl kullanmaya açıklayan hello Azure multi-Factor authentication sayfasıdır."
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
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="5872e-103">Azure Multi-Factor Authentication ve AD FS ile bulut kaynaklarını güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="5872e-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="5872e-104">Kuruluşunuz Azure Active Directory ile birleştirildiyse Azure çok faktörlü kimlik doğrulaması veya Azure AD tarafından erişilen Active Directory Federasyon Hizmetleri (AD FS) toosecure kaynakları kullanın.</span><span class="sxs-lookup"><span data-stu-id="5872e-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) toosecure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="5872e-105">Aşağıdaki yordamlar toosecure Azure Active Directory kaynaklarını Azure multi-Factor Authentication veya Active Directory Federasyon Hizmetleri ile Merhaba kullanın.</span><span class="sxs-lookup"><span data-stu-id="5872e-105">Use hello following procedures toosecure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="5872e-106">AD FS kullanarak Azure AD kaynaklarını güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="5872e-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="5872e-107">toosecure, bulut kaynak kümesi bir talep kuralı böylece bir kullanıcı iki aşamalı doğrulamayı başarıyla gerçekleştirdiğinde, Active Directory Federasyon Hizmetleri hello multipleauthn talebi gösterir.</span><span class="sxs-lookup"><span data-stu-id="5872e-107">toosecure your cloud resource, set up a claims rule so that Active Directory Federation Services emits hello multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="5872e-108">Bu talep AD tooAzure üzerinde geçirilir.</span><span class="sxs-lookup"><span data-stu-id="5872e-108">This claim is passed on tooAzure AD.</span></span> <span data-ttu-id="5872e-109">Bu yordam toowalk hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="5872e-109">Follow this procedure toowalk through hello steps:</span></span>


1. <span data-ttu-id="5872e-110">AD FS Yönetimi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="5872e-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="5872e-111">Merhaba solda seçin **bağlı olan taraf güvenleri**.</span><span class="sxs-lookup"><span data-stu-id="5872e-111">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="5872e-112">**Microsoft Office 365 Kimlik Platformu**'na sağ tıklayın ve **Talep Kurallarını Düzenle**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="5872e-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="5872e-114">Verme Dönüştürme Kuralları’nda **Kural Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5872e-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="5872e-116">Açık dönüştürme talep Kuralı Ekleme Sihirbazı Merhaba, seçin **geçir veya Filtrele bir gelen talep** açılan hello ve'ı tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5872e-116">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>

   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="5872e-118">Kuralınıza bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="5872e-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="5872e-119">Seçin **kimlik doğrulama yöntemleri başvuruları** hello gelen talep türü.</span><span class="sxs-lookup"><span data-stu-id="5872e-119">Select **Authentication Methods References** as hello Incoming claim type.</span></span>
8. <span data-ttu-id="5872e-120">**Tüm talep değerlerini geçir**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="5872e-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="5872e-121">![Dönüşüm Talep Kuralı Ekleme Sihirbazı](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="5872e-121">![Add Transform Claim Rule Wizard](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="5872e-122">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5872e-122">Click **Finish**.</span></span> <span data-ttu-id="5872e-123">Merhaba AD FS Yönetim Konsolu'nu kapatın.</span><span class="sxs-lookup"><span data-stu-id="5872e-123">Close hello AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="5872e-124">Federasyon kullanıcıları için Güvenilen IP'ler</span><span class="sxs-lookup"><span data-stu-id="5872e-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="5872e-125">Güvenilen IP'ler yöneticilerin tooby geçişi iki aşamalı doğrulamayı belirli IP adresleri için ya da kendi intranetlerinden kaynaklanan taleplere sahip Federasyon kullanıcıları için izin verir.</span><span class="sxs-lookup"><span data-stu-id="5872e-125">Trusted IPs allow administrators tooby-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="5872e-126">Merhaba aşağıdaki nasıl tooconfigure Azure multi-Factor Authentication güvenilen bölümlerde IP'leri Federasyon kullanıcıları ve bir Federasyon kullanıcıları intranet içinde bir isteğin kaynaklandığı zaman atlama iki aşamalı doğrulama.</span><span class="sxs-lookup"><span data-stu-id="5872e-126">hello following sections describe how tooconfigure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="5872e-127">Bu, AD FS toouse bir geçiş veya filtre gelen talep şablonu hello Kurumsal ağın içinden talep türü ile yapılandırarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="5872e-127">This is achieved by configuring AD FS toouse a pass-through or filter an incoming claim template with hello Inside Corporate Network claim type.</span></span>

<span data-ttu-id="5872e-128">Bu örnekte Güvenilen Taraf Güvenlerimiz için Office 365 kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="5872e-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-hello-ad-fs-claims-rules"></a><span data-ttu-id="5872e-129">Merhaba AD FS talep kurallarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5872e-129">Configure hello AD FS claims rules</span></span>
<span data-ttu-id="5872e-130">toodo ihtiyacımız hello ilk tooconfigure hello AD FS talep şeydir.</span><span class="sxs-lookup"><span data-stu-id="5872e-130">hello first thing we need toodo is tooconfigure hello AD FS claims.</span></span> <span data-ttu-id="5872e-131">Biri hello Kurumsal ağın içinden talep türü ve ek bir oturum açık tutmak için iki talep kurallarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5872e-131">Create two claims rules, one for hello Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="5872e-132">AD FS Yönetimi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="5872e-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="5872e-133">Merhaba solda seçin **bağlı olan taraf güvenleri**.</span><span class="sxs-lookup"><span data-stu-id="5872e-133">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="5872e-134">**Microsoft Office 365 Kimlik Platformu**’na sağ tıklayın ve **Talep Kurallarını Düzenle…** seçeneğini belirleyin.
   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="5872e-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="5872e-135">Verme Dönüştürme Kuralları’nda **Kural Ekle**’ye tıklayın.
   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="5872e-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="5872e-136">Açık dönüştürme talep Kuralı Ekleme Sihirbazı Merhaba, seçin **geçir veya Filtrele bir gelen talep** açılan hello ve'ı tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5872e-136">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>
   <span data-ttu-id="5872e-137">![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="5872e-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="5872e-138">Merhaba kutusunu sonraki tooClaim kural adı kuralınıza bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="5872e-138">In hello box next tooClaim rule name, give your rule a name.</span></span> <span data-ttu-id="5872e-139">Örneğin: InsideCorpNet.</span><span class="sxs-lookup"><span data-stu-id="5872e-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="5872e-140">Sonraki tooIncoming hello açılır, gelen talep türü, seçin **Kurumsal ağın içinden**.</span><span class="sxs-lookup"><span data-stu-id="5872e-140">From hello drop-down, next tooIncoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="5872e-141">![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="5872e-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="5872e-142">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5872e-142">Click **Finish**.</span></span>
9. <span data-ttu-id="5872e-143">Verme Dönüştürme Kuralları’nda **Kural Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5872e-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="5872e-144">Açık dönüştürme talep Kuralı Ekleme Sihirbazı Merhaba, seçin **talepleri özel kural kullanarak Gönder** açılan hello ve'ı tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5872e-144">On hello Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from hello drop-down and click **Next**.</span></span>
11. <span data-ttu-id="5872e-145">Talep kuralı adı altındaki hello kutusuna: girin *tutmak kullanıcılar imzalı içinde*.</span><span class="sxs-lookup"><span data-stu-id="5872e-145">In hello box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="5872e-146">Merhaba özel kural kutusuna şunu girin:</span><span class="sxs-lookup"><span data-stu-id="5872e-146">In hello Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="5872e-148">**Finish (Son)** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5872e-148">Click **Finish**.</span></span>
14. <span data-ttu-id="5872e-149">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5872e-149">Click **Apply**.</span></span>
15. <span data-ttu-id="5872e-150">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5872e-150">Click **Ok**.</span></span>
16. <span data-ttu-id="5872e-151">AD FS Yönetimi'ni kapatın.</span><span class="sxs-lookup"><span data-stu-id="5872e-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="5872e-152">Azure Multi-Factor Authentication Güvenilen IP’leri Federasyon Kullanıcıları ile Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5872e-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="5872e-153">Merhaba talepler, biz güvenilen IP'leri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5872e-153">Now that hello claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="5872e-154">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="5872e-154">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="5872e-155">Hello solda tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5872e-155">On hello left, click **Active Directory**.</span></span>
3. <span data-ttu-id="5872e-156">Dizini altında hello dizini tooset güvenilen IP'leri ayarlamak istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="5872e-156">Under Directory, select hello directory where you want tooset up trusted IPs.</span></span>
4. <span data-ttu-id="5872e-157">Hello seçtiğiniz dizin, tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="5872e-157">On hello Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="5872e-158">Merhaba çok faktörlü kimlik doğrulaması bölümünde tıklayın **hizmet ayarlarını Yönet**.</span><span class="sxs-lookup"><span data-stu-id="5872e-158">In hello multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="5872e-159">Merhaba hizmet ayarları sayfasında, güvenilen IP'ler altında seçin **Atla çok / multi-Factor-authentication istekleri için Federasyon kullanıcıları intranetimde bulunan**.</span><span class="sxs-lookup"><span data-stu-id="5872e-159">On hello Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  

   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. <span data-ttu-id="5872e-161">**Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5872e-161">Click **save**.</span></span>
8. <span data-ttu-id="5872e-162">Merhaba güncelleştirmeler uygulandıktan sonra tıklayın **kapatmak**.</span><span class="sxs-lookup"><span data-stu-id="5872e-162">Once hello updates have been applied, click **close**.</span></span>

<span data-ttu-id="5872e-163">Bu kadar!</span><span class="sxs-lookup"><span data-stu-id="5872e-163">That’s it!</span></span> <span data-ttu-id="5872e-164">Bir talep dış hello Kurumsal intranet bağlantısı kaynaklandığı bu noktada, birleştirilmiş Office 365 kullanıcıları yalnızca toouse MFA olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5872e-164">At this point, federated Office 365 users should only have toouse MFA when a claim originates from outside hello corporate intranet.</span></span>
