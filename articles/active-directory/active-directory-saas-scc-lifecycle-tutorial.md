---
title: "Öğretici: Azure Active Directory Tümleştirme SCC yaşam | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse SCC yaşam döngüsü nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="f7673-103">Öğretici: Azure Active Directory Tümleştirme ile SCC yaşam döngüsü</span><span class="sxs-lookup"><span data-stu-id="f7673-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="f7673-104">Merhaba amacı Bu öğretici, Azure ve SCC yaşam döngüsü tooshow hello tümleştirme ' dir.</span><span class="sxs-lookup"><span data-stu-id="f7673-104">hello objective of this tutorial is tooshow hello integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="f7673-105">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="f7673-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="f7673-106">Geçerli bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="f7673-106">A valid Azure subscription</span></span>
* <span data-ttu-id="f7673-107">Bir SCC yaşam döngüsü çoklu oturum açma (SSO) abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="f7673-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="f7673-108">Bu öğreticiyi tamamladıktan sonra Azure AD kullanıcılarının atamış yaşam döngüsü olacaktır tooSCC mümkün toosingle oturum hello uygulamasına SCC yaşam döngüsü şirket sitenizdeki (servis sağlayıcı tarafından başlatılan oturum açma) hello veya hello kullanarak [giriş Erişim paneli toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f7673-108">After completing this tutorial, hello Azure AD users you have assigned tooSCC LifeCycle will be able toosingle sign into hello application at your SCC LifeCycle company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="f7673-109">Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:</span><span class="sxs-lookup"><span data-stu-id="f7673-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="f7673-110">Merhaba uygulama tümleştirmesi SCC yaşam döngüsü için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f7673-110">Enabling hello application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="f7673-111">Çoklu oturum açma (SSO) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f7673-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="f7673-112">Kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="f7673-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="f7673-113">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="f7673-113">Assigning users</span></span>

<span data-ttu-id="f7673-114">![Senaryo](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "senaryosu")</span><span class="sxs-lookup"><span data-stu-id="f7673-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a><span data-ttu-id="f7673-115">Merhaba uygulama tümleştirmesi SCC yaşam döngüsü için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f7673-115">Enable hello application integration for SCC LifeCycle</span></span>
<span data-ttu-id="f7673-116">Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi SCC yaşam döngüsü için.</span><span class="sxs-lookup"><span data-stu-id="f7673-116">hello objective of this section is toooutline how tooenable hello application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="f7673-117">**tooenable hello uygulama tümleştirmesi SCC yaşam döngüsü için hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f7673-117">**tooenable hello application integration for SCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7673-118">Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f7673-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="f7673-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="f7673-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="f7673-120">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="f7673-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="f7673-121">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="f7673-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="f7673-122">![Uygulamaları](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="f7673-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="f7673-123">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="f7673-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="f7673-124">![Uygulama ekleme](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="f7673-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="f7673-125">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="f7673-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="f7673-126">![Galeriden bir uygulama eklemek](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Galeriden bir uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="f7673-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="f7673-127">Merhaba, **arama kutusu**, türü **SCC yaşam döngüsü**.</span><span class="sxs-lookup"><span data-stu-id="f7673-127">In hello **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="f7673-128">![Uygulama Galerisi](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "uygulama Galerisi")</span><span class="sxs-lookup"><span data-stu-id="f7673-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="f7673-129">Merhaba sonuçlar bölmesinde seçin **SCC yaşam döngüsü**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="f7673-129">In hello results pane, select **SCC LifeCycle**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="f7673-130">![SCC yaşam döngüsü](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC yaşam döngüsü")</span><span class="sxs-lookup"><span data-stu-id="f7673-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="f7673-131">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f7673-131">Configure single sign-on</span></span>

<span data-ttu-id="f7673-132">Bu bölümde Hello amacı nasıl hello SAML protokolünü kullanarak Federasyon Azure AD'de hesabıyla tooenable kullanıcılar tooauthenticate tooSCC yaşam döngüsü temel toooutline ' dir.</span><span class="sxs-lookup"><span data-stu-id="f7673-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooSCC LifeCycle with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="f7673-133">**tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f7673-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7673-134">Merhaba hello üzerinde Klasik Azure portalı içinde **SCC yaşam döngüsü** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello ** tek oturum yapılandırma üzerinde Aktar ** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f7673-134">In hello Azure classic portal, on hello **SCC LifeCycle** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="f7673-135">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="f7673-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="f7673-136">Merhaba üzerinde **nasıl tooSCC yaşam döngüsü üzerindeki kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="f7673-136">On hello **How would you like users toosign on tooSCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="f7673-137">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="f7673-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="f7673-138">Merhaba üzerinde **uygulama URL'sini Yapılandır** sayfasında hello **oturum üzerinde URL'si** metin kutusuna, türü hello URL kullanılan, kullanıcıların toosign tarafından tooyour üzerinde SCC yaşam döngüsü uygulama deseni takip hello kullanarak "*https:// bs1.SCC.com/lc7/Welcome/Customer/PICTtest.aspx*"ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="f7673-138">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type hello URL used by your users toosign on tooyour SCC LifeCycle application using hello following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="f7673-139">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="f7673-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="f7673-140">Merhaba üzerinde **çoklu oturum açma SCC yaşam döngüsü sırasında yapılandırma** sayfasında, **karşıdan meta veri**ve meta veri dosyası, bilgisayarınıza yerel olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f7673-140">On hello **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="f7673-141">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="f7673-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="f7673-142">Bu meta veri dosyası tooSCC yaşam döngüsü destek ekibi iletin.</span><span class="sxs-lookup"><span data-stu-id="f7673-142">Forward that Metadata file tooSCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="f7673-143">Çoklu oturum açma hello SCC yaşam döngüsü destek ekibi tarafından etkin toobe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f7673-143">Single sign-on has toobe enabled by hello SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="f7673-144">Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f7673-144">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="f7673-145">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="f7673-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="f7673-146">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="f7673-146">Configure user provisioning</span></span>

<span data-ttu-id="f7673-147">SCC yaşam döngüsü içine sipariş tooenable Azure AD kullanıcıların toolog bunların SCC yaşam döngüsü sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f7673-147">In order tooenable Azure AD users toolog into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="f7673-148">TooSCC yaşam döngüsü, tooconfigure kullanıcı hazırlama için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="f7673-148">There is no action item for you tooconfigure user provisioning tooSCC LifeCycle.</span></span>

<span data-ttu-id="f7673-149">Atanan kullanıcı çalıştığında toolog girdiğinde SCC yaşam döngüsü, bir SCC yaşam döngüsü hesap gerekirse, otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f7673-149">When an assigned user tries toolog into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="f7673-150">API AAD kullanıcı hesapları SCC yaşam döngüsü tooprovision tarafından sağlanan veya herhangi diğer SCC yaşam döngüsü kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7673-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="f7673-151">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="f7673-151">Assign users</span></span>
<span data-ttu-id="f7673-152">tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7673-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="f7673-153">**tooassign kullanıcılar tooSCC yaşam döngüsü, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f7673-153">**tooassign users tooSCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7673-154">Hello Klasik Azure portalı, bir test hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f7673-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="f7673-155">Hello üzerinde ** SCC yaşam döngüsü ** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.</span><span class="sxs-lookup"><span data-stu-id="f7673-155">On hello **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="f7673-156">![Kullanıcılar atama](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "kullanıcı atama")</span><span class="sxs-lookup"><span data-stu-id="f7673-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="f7673-157">Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.</span><span class="sxs-lookup"><span data-stu-id="f7673-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="f7673-158">![Evet](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Evet")</span><span class="sxs-lookup"><span data-stu-id="f7673-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="f7673-159">SSO ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="f7673-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="f7673-160">Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f7673-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

