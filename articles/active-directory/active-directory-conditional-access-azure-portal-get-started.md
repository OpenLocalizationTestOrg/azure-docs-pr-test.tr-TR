---
title: "Azure Active Directory'de koşullu erişim aaaGet Başlarken | Microsoft Docs"
description: "Koşullu erişim konumu koşulu kullanarak test edin."
services: active-directory
keywords: "koşullu erişim tooapps, Azure AD ile koşullu erişim toocompany kaynaklarına, koşullu erişim ilkeleri güvenli erişim"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="8cdb3-104">Azure Active Directory'de koşullu erişimi kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="8cdb3-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="8cdb3-105">Koşullu erişim, uygulamalarınızı yetkili kullanıcıların erişmek için toodefine koşulları sağlayan Azure Active Directory bir yetenektir.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-105">Conditional access is a capability of Azure Active Directory that enables you toodefine conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="8cdb3-106">Bu konu, ortamınızdaki bir konum koşula göre koşullu bir erişim test etmek için yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="8cdb3-107">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="8cdb3-107">Scenario description</span></span>

<span data-ttu-id="8cdb3-108">Birçok kuruluşta ortak gereksinimi olan tooonly hello Kurumsal intranet bağlantısı gerçekleştirilmez erişim tooapps için çok faktörlü kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-108">One common requirement in many organizations is tooonly require multi-factor authentication for access tooapps that is not performed from hello corporate intranet.</span></span> <span data-ttu-id="8cdb3-109">Azure Active Directory ile konum temelli koşullu erişim ilkesini yapılandırarak bu amacı kolayca gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="8cdb3-110">Bu konu, ilgili ilke yapılandırmaya ilişkin ayrıntılı yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="8cdb3-111">Hello İlkesi yararlanır [güvenilen IP'ler](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish hello şirket yapılan erişim denemesi arasındaki kullanıcının intranet ve diğer tüm konumları.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-111">hello policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish between access attempts made from hello corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="8cdb3-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8cdb3-112">Prerequisites</span></span>

<span data-ttu-id="8cdb3-113">Merhaba bu konuda açıklanan senaryo, özetlenen hello kavramları hakkında bilgi sahibi olduğunu varsayar [Azure Active Directory koşullu erişim](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8cdb3-113">hello scenario outlined in this topic assumes that you are familiar with hello concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="8cdb3-114">tootest bu senaryo, gerekir:</span><span class="sxs-lookup"><span data-stu-id="8cdb3-114">tootest this scenario, you need to:</span></span>

- <span data-ttu-id="8cdb3-115">Test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8cdb3-115">Create a test user</span></span> 

- <span data-ttu-id="8cdb3-116">Bir Azure AD Premium lisansı toohello test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="8cdb3-116">Assign an Azure AD Premium license toohello test user</span></span>

- <span data-ttu-id="8cdb3-117">Yönetilen bir uygulama yapılandırma ve test kullanıcı tooit atayın</span><span class="sxs-lookup"><span data-stu-id="8cdb3-117">Configure a managed app and assign your test user tooit</span></span>

- <span data-ttu-id="8cdb3-118">Güvenilen IP'leri yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="8cdb3-118">Configure trusted IPs</span></span>

<span data-ttu-id="8cdb3-119">Güvenilen IP'ler hakkında daha fazla ayrıntı gerekirse bkz [güvenilen IP'ler](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="8cdb3-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="8cdb3-120">İlke yapılandırma adımları</span><span class="sxs-lookup"><span data-stu-id="8cdb3-120">Policy configuration steps</span></span>

<span data-ttu-id="8cdb3-121">**tooconfigure koşullu erişim ilkenizi yapın:**</span><span class="sxs-lookup"><span data-stu-id="8cdb3-121">**tooconfigure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="8cdb3-122">Merhaba hello sol gezinti çubuğu üzerinde Azure portal'ı tıklatın **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-122">In hello Azure portal, on hello left navbar, click **Azure Active Directory**.</span></span> 

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="8cdb3-124">Merhaba üzerinde **Azure Active Directory** dikey penceresinde hello **Yönet** 'yi tıklatın **koşullu erişim**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-124">On hello **Azure Active Directory** blade, in hello **Manage** section, click **Conditional access**.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="8cdb3-126">Merhaba üzerinde **koşullu erişim** dikey penceresinde, tooopen hello **yeni** hello araç çubuğunda hello üstte dikey tıklayın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-126">On hello **Conditional Access** blade, tooopen hello **New** blade, in hello toolbar on hello top, click **Add**.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="8cdb3-128">Merhaba üzerinde **yeni** dikey penceresinde hello **adı** metin kutusuna, ilkeniz için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-128">On hello **New** blade, in hello **Name** textbox, type a name for your policy.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="8cdb3-130">Merhaba, **atama** 'yi tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-130">In hello **Assignment** section, click **Users and groups**.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="8cdb3-132">Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8cdb3-132">On hello **Users and groups** blade, perform hello following steps:</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="8cdb3-134">a.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-134">a.</span></span> <span data-ttu-id="8cdb3-135">Tıklatın **kullanıcıları ve grupları seçin**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="8cdb3-136">b.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-136">b.</span></span> <span data-ttu-id="8cdb3-137">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-137">Click **Select**.</span></span>

    <span data-ttu-id="8cdb3-138">c.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-138">c.</span></span> <span data-ttu-id="8cdb3-139">Merhaba üzerinde **seçin** dikey penceresinde, test kullanıcınız seçin ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-139">On hello **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="8cdb3-140">d.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-140">d.</span></span> <span data-ttu-id="8cdb3-141">Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde tıklatın **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-141">On hello **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="8cdb3-142">Merhaba üzerinde **yeni** dikey penceresinde, tooopen hello **bulut uygulamaları** dikey penceresinde hello **atama** 'yi tıklatın **bulut uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-142">On hello **New** blade, tooopen hello **Cloud apps** blade, in hello **Assignment** section, click **Cloud apps**.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="8cdb3-144">Merhaba üzerinde **bulut uygulamaları** dikey penceresinde hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8cdb3-144">On hello **Cloud apps** blade, perform hello following steps:</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="8cdb3-146">a.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-146">a.</span></span> <span data-ttu-id="8cdb3-147">Tıklatın **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-147">Click **Select apps**.</span></span>

    <span data-ttu-id="8cdb3-148">b.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-148">b.</span></span> <span data-ttu-id="8cdb3-149">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-149">Click **Select**.</span></span>

    <span data-ttu-id="8cdb3-150">c.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-150">c.</span></span> <span data-ttu-id="8cdb3-151">Merhaba üzerinde **seçin** dikey penceresinde, bulut uygulamanızı seçin ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-151">On hello **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="8cdb3-152">d.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-152">d.</span></span> <span data-ttu-id="8cdb3-153">Merhaba üzerinde **bulut uygulamaları** dikey penceresinde tıklatın **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-153">On hello **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="8cdb3-154">Merhaba üzerinde **yeni** dikey penceresinde, tooopen hello **koşullar** dikey penceresinde hello **atama** 'yi tıklatın **koşullar**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-154">On hello **New** blade, tooopen hello **Conditions** blade, in hello **Assignment** section, click **Conditions**.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="8cdb3-156">Merhaba üzerinde **koşullar** dikey penceresinde, tooopen hello **konumları** dikey penceresinde tıklatın **konumları**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-156">On hello **Conditions** blade, tooopen hello **Locations** blade, click **Locations**.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="8cdb3-158">Merhaba üzerinde **konumları** dikey penceresinde hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8cdb3-158">On hello **Locations** blade, perform hello following steps:</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="8cdb3-160">a.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-160">a.</span></span> <span data-ttu-id="8cdb3-161">Altında **yapılandırma**, tıklatın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="8cdb3-162">b.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-162">b.</span></span> <span data-ttu-id="8cdb3-163">Altında **INCLUDE**, tıklatın **tüm konumları**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="8cdb3-164">c.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-164">c.</span></span> <span data-ttu-id="8cdb3-165">Tıklatın **hariç**ve ardından **tüm güvenilen IP'leri**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="8cdb3-167">d.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-167">d.</span></span> <span data-ttu-id="8cdb3-168">**Bitti**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-168">Click **Done**.</span></span>

12. <span data-ttu-id="8cdb3-169">Merhaba üzerinde **koşullar** dikey penceresinde tıklatın **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-169">On hello **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="8cdb3-170">Merhaba üzerinde **yeni** dikey penceresinde, tooopen hello **Grant** dikey penceresinde hello **denetimleri** 'yi tıklatın **Grant**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-170">On hello **New** blade, tooopen hello **Grant** blade, in hello **Controls** section, click **Grant**.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="8cdb3-172">Merhaba üzerinde **Grant** dikey penceresinde hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8cdb3-172">On hello **Grant** blade, perform hello following steps:</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="8cdb3-174">a.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-174">a.</span></span> <span data-ttu-id="8cdb3-175">Seçin **çok faktörlü kimlik doğrulaması gerektiren**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="8cdb3-176">b.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-176">b.</span></span> <span data-ttu-id="8cdb3-177">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-177">Click **Select**.</span></span>

15. <span data-ttu-id="8cdb3-178">Merhaba üzerinde **yeni** dikey altında **ilkesini etkinleştir**, tıklatın **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-178">On hello **New** blade, under **Enable policy**, click **On**.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="8cdb3-180">Merhaba üzerinde **yeni** dikey penceresinde tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-180">On hello **New** blade, click **Create**.</span></span>


## <a name="testing-hello-policy"></a><span data-ttu-id="8cdb3-181">Merhaba ilkeyi test etme</span><span class="sxs-lookup"><span data-stu-id="8cdb3-181">Testing hello policy</span></span>

<span data-ttu-id="8cdb3-182">tootest ilkeniz, uygulamanızı bir aygıttan erişim:</span><span class="sxs-lookup"><span data-stu-id="8cdb3-182">tootest your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="8cdb3-183">İçinde yapılandırılmış güvenilen IP'ler bir IP adresi vardır</span><span class="sxs-lookup"><span data-stu-id="8cdb3-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="8cdb3-184">Yapılandırılmış güvenilen IP'leri içinde olmayan bir IP adresi var.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="8cdb3-185">Çok faktörlü kimlik doğrulaması yalnızca, yapılandırılmış güvenilen IP'leri içinde değil bir aygıttan yapılan bağlantı girişimi sırasında gerekli olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8cdb3-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="8cdb3-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8cdb3-186">Next steps</span></span>

<span data-ttu-id="8cdb3-187">Toolearn koşullu erişim hakkında daha fazla bilgi isterseniz bkz [Azure Active Directory koşullu erişim](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8cdb3-187">If you would like toolearn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

