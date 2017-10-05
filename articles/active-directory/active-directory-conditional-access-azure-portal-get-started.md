---
title: "Azure Active Directory'de koşullu erişimi kullanmaya başlama | Microsoft Docs"
description: "Koşullu erişim konumu koşulu kullanarak test edin."
services: active-directory
keywords: "uygulamaları, Azure AD ile koşullu erişim, koşullu erişim ilkeleri, şirket kaynaklarına güvenli erişim için koşullu erişim"
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
ms.openlocfilehash: cd53e8be32d1e98aaf9f72177895871dba69df86
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="7c5a8-104">Azure Active Directory'de koşullu erişimi kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="7c5a8-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="7c5a8-105">Koşullu erişim, uygulamalarınızı yetkili kullanıcıların erişebilmeniz için koşullar tanımlamanızı sağlayan Azure Active Directory bir yetenektir.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-105">Conditional access is a capability of Azure Active Directory that enables you to define conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="7c5a8-106">Bu konu, ortamınızdaki bir konum koşula göre koşullu bir erişim test etmek için yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="7c5a8-107">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="7c5a8-107">Scenario description</span></span>

<span data-ttu-id="7c5a8-108">Yalnızca Kurumsal intranet bağlantısı gerçekleştirilmez erişim uygulamalar için çok faktörlü kimlik doğrulaması gerektirmek için birçok kuruluşta bir ortak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-108">One common requirement in many organizations is to only require multi-factor authentication for access to apps that is not performed from the corporate intranet.</span></span> <span data-ttu-id="7c5a8-109">Azure Active Directory ile konum temelli koşullu erişim ilkesini yapılandırarak bu amacı kolayca gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="7c5a8-110">Bu konu, ilgili ilke yapılandırmaya ilişkin ayrıntılı yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="7c5a8-111">İlke yararlanır [güvenilen IP'leri](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) şirkete yapılan erişim denemesi ayırt etmek için intranet ve diğer tüm konumlara kullanıcının.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-111">The policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) to distinguish between access attempts made from the corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7c5a8-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7c5a8-112">Prerequisites</span></span>

<span data-ttu-id="7c5a8-113">Bu konuda açıklanan senaryo özetlenen kavramları hakkında bilgi sahibi olduğunu varsayar [Azure Active Directory koşullu erişim](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7c5a8-113">The scenario outlined in this topic assumes that you are familiar with the concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="7c5a8-114">Bu senaryoyu test etmek için gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c5a8-114">To test this scenario, you need to:</span></span>

- <span data-ttu-id="7c5a8-115">Test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c5a8-115">Create a test user</span></span> 

- <span data-ttu-id="7c5a8-116">Test kullanıcısı için bir Azure AD Premium lisansı atayın</span><span class="sxs-lookup"><span data-stu-id="7c5a8-116">Assign an Azure AD Premium license to the test user</span></span>

- <span data-ttu-id="7c5a8-117">Yönetilen bir uygulama yapılandırma ve test kullanıcınız atayın</span><span class="sxs-lookup"><span data-stu-id="7c5a8-117">Configure a managed app and assign your test user to it</span></span>

- <span data-ttu-id="7c5a8-118">Güvenilen IP'leri yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="7c5a8-118">Configure trusted IPs</span></span>

<span data-ttu-id="7c5a8-119">Güvenilen IP'ler hakkında daha fazla ayrıntı gerekirse bkz [güvenilen IP'ler](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="7c5a8-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="7c5a8-120">İlke yapılandırma adımları</span><span class="sxs-lookup"><span data-stu-id="7c5a8-120">Policy configuration steps</span></span>

<span data-ttu-id="7c5a8-121">**Koşullu erişim ilkesini yapılandırmak için aşağıdakileri yapın:**</span><span class="sxs-lookup"><span data-stu-id="7c5a8-121">**To configure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="7c5a8-122">Azure portalında sol gezinti çubuğu tıklatın **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-122">In the Azure portal, on the left navbar, click **Azure Active Directory**.</span></span> 

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="7c5a8-124">Üzerinde **Azure Active Directory** dikey penceresindeki **Yönet** 'yi tıklatın **koşullu erişim**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-124">On the **Azure Active Directory** blade, in the **Manage** section, click **Conditional access**.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="7c5a8-126">Üzerinde **koşullu erişim** açmak için dikey penceresinde **yeni** üstteki araç çubuğunda dikey tıklayın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-126">On the **Conditional Access** blade, to open the **New** blade, in the toolbar on the top, click **Add**.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="7c5a8-128">Üzerinde **yeni** dikey penceresindeki **adı** metin kutusuna, ilkeniz için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-128">On the **New** blade, in the **Name** textbox, type a name for your policy.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="7c5a8-130">İçinde **atama** 'yi tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-130">In the **Assignment** section, click **Users and groups**.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="7c5a8-132">Üzerinde **kullanıcılar ve gruplar** dikey penceresinde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7c5a8-132">On the **Users and groups** blade, perform the following steps:</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="7c5a8-134">a.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-134">a.</span></span> <span data-ttu-id="7c5a8-135">Tıklatın **kullanıcıları ve grupları seçin**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="7c5a8-136">b.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-136">b.</span></span> <span data-ttu-id="7c5a8-137">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-137">Click **Select**.</span></span>

    <span data-ttu-id="7c5a8-138">c.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-138">c.</span></span> <span data-ttu-id="7c5a8-139">Üzerinde **seçin** dikey penceresinde, test kullanıcınız seçin ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-139">On the **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="7c5a8-140">d.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-140">d.</span></span> <span data-ttu-id="7c5a8-141">Üzerinde **kullanıcılar ve gruplar** dikey penceresinde tıklatın **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-141">On the **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="7c5a8-142">Üzerinde **yeni** açmak için dikey penceresinde **bulut uygulamaları** dikey penceresinde, **atama** 'yi tıklatın **bulut uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-142">On the **New** blade, to open the **Cloud apps** blade, in the **Assignment** section, click **Cloud apps**.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="7c5a8-144">Üzerinde **bulut uygulamaları** dikey penceresinde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7c5a8-144">On the **Cloud apps** blade, perform the following steps:</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="7c5a8-146">a.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-146">a.</span></span> <span data-ttu-id="7c5a8-147">Tıklatın **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-147">Click **Select apps**.</span></span>

    <span data-ttu-id="7c5a8-148">b.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-148">b.</span></span> <span data-ttu-id="7c5a8-149">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-149">Click **Select**.</span></span>

    <span data-ttu-id="7c5a8-150">c.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-150">c.</span></span> <span data-ttu-id="7c5a8-151">Üzerinde **seçin** dikey penceresinde, bulut uygulamanızı seçin ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-151">On the **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="7c5a8-152">d.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-152">d.</span></span> <span data-ttu-id="7c5a8-153">Üzerinde **bulut uygulamaları** dikey penceresinde tıklatın **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-153">On the **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="7c5a8-154">Üzerinde **yeni** açmak için dikey penceresinde **koşullar** dikey penceresinde, **atama** 'yi tıklatın **koşullar**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-154">On the **New** blade, to open the **Conditions** blade, in the **Assignment** section, click **Conditions**.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="7c5a8-156">Üzerinde **koşullar** açmak için dikey penceresinde **konumları** dikey penceresinde tıklatın **konumları**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-156">On the **Conditions** blade, to open the **Locations** blade, click **Locations**.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="7c5a8-158">Üzerinde **konumları** dikey penceresinde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7c5a8-158">On the **Locations** blade, perform the following steps:</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="7c5a8-160">a.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-160">a.</span></span> <span data-ttu-id="7c5a8-161">Altında **yapılandırma**, tıklatın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="7c5a8-162">b.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-162">b.</span></span> <span data-ttu-id="7c5a8-163">Altında **INCLUDE**, tıklatın **tüm konumları**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="7c5a8-164">c.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-164">c.</span></span> <span data-ttu-id="7c5a8-165">Tıklatın **hariç**ve ardından **tüm güvenilen IP'leri**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="7c5a8-167">d.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-167">d.</span></span> <span data-ttu-id="7c5a8-168">**Bitti**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-168">Click **Done**.</span></span>

12. <span data-ttu-id="7c5a8-169">Üzerinde **koşullar** dikey penceresinde tıklatın **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-169">On the **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="7c5a8-170">Üzerinde **yeni** açmak için dikey penceresinde **Grant** dikey penceresinde, **denetimleri** 'yi tıklatın **Grant**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-170">On the **New** blade, to open the **Grant** blade, in the **Controls** section, click **Grant**.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="7c5a8-172">Üzerinde **Grant** dikey penceresinde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7c5a8-172">On the **Grant** blade, perform the following steps:</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="7c5a8-174">a.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-174">a.</span></span> <span data-ttu-id="7c5a8-175">Seçin **çok faktörlü kimlik doğrulaması gerektiren**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="7c5a8-176">b.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-176">b.</span></span> <span data-ttu-id="7c5a8-177">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-177">Click **Select**.</span></span>

15. <span data-ttu-id="7c5a8-178">Üzerinde **yeni** dikey altında **ilkesini etkinleştir**, tıklatın **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-178">On the **New** blade, under **Enable policy**, click **On**.</span></span>

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="7c5a8-180">Üzerinde **yeni** dikey penceresinde tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-180">On the **New** blade, click **Create**.</span></span>


## <a name="testing-the-policy"></a><span data-ttu-id="7c5a8-181">İlkeyi test etme</span><span class="sxs-lookup"><span data-stu-id="7c5a8-181">Testing the policy</span></span>

<span data-ttu-id="7c5a8-182">İlkeniz sınamak için uygulamanızı bir aygıttan erişim:</span><span class="sxs-lookup"><span data-stu-id="7c5a8-182">To test your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="7c5a8-183">İçinde yapılandırılmış güvenilen IP'ler bir IP adresi vardır</span><span class="sxs-lookup"><span data-stu-id="7c5a8-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="7c5a8-184">Yapılandırılmış güvenilen IP'leri içinde olmayan bir IP adresi var.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="7c5a8-185">Çok faktörlü kimlik doğrulaması yalnızca, yapılandırılmış güvenilen IP'leri içinde değil bir aygıttan yapılan bağlantı girişimi sırasında gerekli olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c5a8-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="7c5a8-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7c5a8-186">Next steps</span></span>

<span data-ttu-id="7c5a8-187">Koşullu erişim hakkında daha fazla bilgi edinmek istiyorsanız, bkz: [Azure Active Directory koşullu erişim](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7c5a8-187">If you would like to learn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

