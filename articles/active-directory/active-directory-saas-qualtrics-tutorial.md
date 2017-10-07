---
title: "Öğretici: Azure Active Directory Tümleştirme ile Qualtrics | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse Qualtrics nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="47da0-103">Öğretici: Azure Active Directory Tümleştirme Qualtrics ile</span><span class="sxs-lookup"><span data-stu-id="47da0-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="47da0-104">Merhaba amacı Bu öğretici, Azure ve Qualtrics tooshow hello tümleştirme ' dir.</span><span class="sxs-lookup"><span data-stu-id="47da0-104">hello objective of this tutorial is tooshow hello integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="47da0-105">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="47da0-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="47da0-106">Geçerli bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="47da0-106">A valid Azure subscription</span></span>
* <span data-ttu-id="47da0-107">Bir Qualtrics çoklu oturum açma (SSO) abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="47da0-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="47da0-108">Bu öğreticiyi tamamladıktan sonra tooQualtrics atamış hello Azure AD kullanıcıların mümkün toosingle oturum Qualtrics şirket sitenizin (servis sağlayıcı tarafından başlatılan oturum açma) veya hello kullanarak hello uygulamaya olacaktır [giriş toohello Erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="47da0-108">After completing this tutorial, hello Azure AD users you have assigned tooQualtrics will be able toosingle sign into hello application at your Qualtrics company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="47da0-109">Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:</span><span class="sxs-lookup"><span data-stu-id="47da0-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="47da0-110">Merhaba uygulama tümleştirmesi Qualtrics için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="47da0-110">Enabling hello application integration for Qualtrics</span></span>
2. <span data-ttu-id="47da0-111">Çoklu oturum açma (SSO) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="47da0-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="47da0-112">Kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="47da0-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="47da0-113">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="47da0-113">Assigning users</span></span>

<span data-ttu-id="47da0-114">![Senaryo](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "senaryosu")</span><span class="sxs-lookup"><span data-stu-id="47da0-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-qualtrics"></a><span data-ttu-id="47da0-115">Merhaba uygulama tümleştirmesi Qualtrics için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="47da0-115">Enabling hello application integration for Qualtrics</span></span>
<span data-ttu-id="47da0-116">Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi Qualtrics için.</span><span class="sxs-lookup"><span data-stu-id="47da0-116">hello objective of this section is toooutline how tooenable hello application integration for Qualtrics.</span></span>

<span data-ttu-id="47da0-117">**tooenable hello uygulama tümleştirmesi Qualtrics için hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="47da0-117">**tooenable hello application integration for Qualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="47da0-118">Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="47da0-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="47da0-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="47da0-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="47da0-120">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="47da0-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="47da0-121">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="47da0-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="47da0-122">![Uygulamaları](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="47da0-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="47da0-123">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="47da0-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="47da0-124">![Uygulama ekleme](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="47da0-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="47da0-125">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="47da0-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="47da0-126">![Galeriden bir uygulama eklemek](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Galeriden bir uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="47da0-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="47da0-127">Merhaba, **arama kutusu**, türü **Qualtrics**.</span><span class="sxs-lookup"><span data-stu-id="47da0-127">In hello **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="47da0-128">![Uygulama Galerisi](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "uygulama Galerisi")</span><span class="sxs-lookup"><span data-stu-id="47da0-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="47da0-129">Merhaba sonuçlar bölmesinde seçin **Qualtrics**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="47da0-129">In hello results pane, select **Qualtrics**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="47da0-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="47da0-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="47da0-131">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="47da0-131">Configure single sign-on</span></span>

<span data-ttu-id="47da0-132">Bu bölümde Hello amacı nasıl tooenable kullanıcılar tooauthenticate tooQualtrics Federasyon kullanarak Azure AD'de hesabıyla hello SAML protokolünü temel toooutline ' dir.</span><span class="sxs-lookup"><span data-stu-id="47da0-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooQualtrics with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="47da0-133">**tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="47da0-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="47da0-134">Merhaba hello üzerinde Klasik Azure portalı içinde **Qualtrics** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="47da0-134">In hello Azure classic portal, on hello **Qualtrics** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="47da0-135">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="47da0-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="47da0-136">Merhaba üzerinde **nasıl tooQualtrics üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="47da0-136">On hello **How would you like users toosign on tooQualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="47da0-137">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="47da0-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="47da0-138">Hello üzerinde **uygulama URL'sini yapılandırın** sayfasında hello **üzerinde Qualtrics oturum URL'si** metin kutusuna, URL'nizi yazın (örn: "*https://ssotest2ut1.qualtrics.com*") ve ardından **Sonraki**.</span><span class="sxs-lookup"><span data-stu-id="47da0-138">On hello **Configure App URL** page, in hello **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="47da0-139">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="47da0-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="47da0-140">Merhaba üzerinde **çoklu oturum açma sırasında Qualtrics yapılandırma** sayfasında, **karşıdan meta veri**ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="47da0-140">On hello **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save hello metadata file on your computer.</span></span>
   
   <span data-ttu-id="47da0-141">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="47da0-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="47da0-142">Merhaba meta veri dosyası toohello Qualtrics Destek ekibine gönderin.</span><span class="sxs-lookup"><span data-stu-id="47da0-142">Send hello metadata file toohello Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="47da0-143">Merhaba SSO yapılandırma hello Qualtrics destek ekibi tarafından gerçekleştirilen toobe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="47da0-143">hello SSO configuration has toobe performed by hello Qualtrics support team.</span></span> <span data-ttu-id="47da0-144">Merhaba Yapılandırma tamamlandıktan hemen sonra bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="47da0-144">You will get a notification as soon as hello configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="47da0-145">Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="47da0-145">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="47da0-146">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="47da0-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="47da0-147">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="47da0-147">Configure user provisioning</span></span>

<span data-ttu-id="47da0-148">TooQualtrics sağlama, tooconfigure kullanıcı için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="47da0-148">There is no action item for you tooconfigure user provisioning tooQualtrics.</span></span> <span data-ttu-id="47da0-149">Atanmış bir kullanıcı hello erişim paneli kullanılarak Qualtrics toolog çalıştığında Qualtrics hello kullanıcı var olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="47da0-149">When an assigned user tries toolog into Qualtrics using hello access panel, Qualtrics checks whether hello user exists.</span></span>  

<span data-ttu-id="47da0-150">Hiçbir kullanıcı hesabı varsa kullanılabilir henüz, Qualtrics tarafından otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="47da0-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="47da0-151">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="47da0-151">Assign users</span></span>
<span data-ttu-id="47da0-152">tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.</span><span class="sxs-lookup"><span data-stu-id="47da0-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="47da0-153">**tooassign kullanıcılar tooQualtrics hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="47da0-153">**tooassign users tooQualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="47da0-154">Hello Klasik Azure portalı, bir test hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="47da0-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="47da0-155">Hello üzerinde **Qualtrics** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.</span><span class="sxs-lookup"><span data-stu-id="47da0-155">On hello **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="47da0-156">![Kullanıcılar atama](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "kullanıcı atama")</span><span class="sxs-lookup"><span data-stu-id="47da0-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="47da0-157">Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.</span><span class="sxs-lookup"><span data-stu-id="47da0-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="47da0-158">![Evet](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Evet")</span><span class="sxs-lookup"><span data-stu-id="47da0-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="47da0-159">SSO ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="47da0-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="47da0-160">Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="47da0-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

