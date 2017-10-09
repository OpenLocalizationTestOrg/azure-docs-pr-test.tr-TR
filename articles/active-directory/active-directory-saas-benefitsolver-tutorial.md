---
title: "Öğretici: Azure Active Directory Tümleştirme ile Benefitsolver | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse Benefitsolver nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="0ae26-103">Öğretici: Azure Active Directory Tümleştirme Benefitsolver ile</span><span class="sxs-lookup"><span data-stu-id="0ae26-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="0ae26-104">Merhaba amacı Bu öğretici, Azure ve Benefitsolver tooshow hello tümleştirme ' dir.</span><span class="sxs-lookup"><span data-stu-id="0ae26-104">hello objective of this tutorial is tooshow hello integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="0ae26-105">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="0ae26-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="0ae26-106">Geçerli bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="0ae26-106">A valid Azure subscription</span></span>
* <span data-ttu-id="0ae26-107">Bir Benefitsolver çoklu oturum açma (SSO) abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="0ae26-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="0ae26-108">Bu öğreticiyi tamamladıktan sonra tooBenefitsolver atamış hello Azure AD kullanıcıların mümkün toosingle oturum hello kullanarak hello uygulamaya olacaktır [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0ae26-108">After completing this tutorial, hello Azure AD users you have assigned tooBenefitsolver will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="0ae26-109">Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:</span><span class="sxs-lookup"><span data-stu-id="0ae26-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="0ae26-110">Merhaba uygulama tümleştirmesi Benefitsolver için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="0ae26-110">Enabling hello application integration for Benefitsolver</span></span>
2. <span data-ttu-id="0ae26-111">Çoklu oturum açma (SSO) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0ae26-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="0ae26-112">Kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="0ae26-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="0ae26-113">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="0ae26-113">Assigning users</span></span>

<span data-ttu-id="0ae26-114">![Senaryo](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "senaryosu")</span><span class="sxs-lookup"><span data-stu-id="0ae26-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-benefitsolver"></a><span data-ttu-id="0ae26-115">Merhaba uygulama tümleştirmesi Benefitsolver için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="0ae26-115">Enabling hello application integration for Benefitsolver</span></span>
<span data-ttu-id="0ae26-116">Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi Benefitsolver için.</span><span class="sxs-lookup"><span data-stu-id="0ae26-116">hello objective of this section is toooutline how tooenable hello application integration for Benefitsolver.</span></span>

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a><span data-ttu-id="0ae26-117">tooenable hello uygulama tümleştirmesi Benefitsolver için hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0ae26-117">tooenable hello application integration for Benefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="0ae26-118">Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0ae26-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="0ae26-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="0ae26-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="0ae26-120">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="0ae26-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="0ae26-121">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="0ae26-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="0ae26-122">![Uygulamaları](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="0ae26-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="0ae26-123">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="0ae26-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="0ae26-124">![Uygulama ekleme](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="0ae26-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="0ae26-125">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="0ae26-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="0ae26-126">![Galeriden bir uygulama eklemek](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Galeriden bir uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="0ae26-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="0ae26-127">Merhaba, **arama kutusu**, türü **Benefitsolver**.</span><span class="sxs-lookup"><span data-stu-id="0ae26-127">In hello **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="0ae26-128">![Uygulama Galerisi](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "uygulama Galerisi")</span><span class="sxs-lookup"><span data-stu-id="0ae26-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="0ae26-129">Merhaba sonuçlar bölmesinde seçin **Benefitsolver**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="0ae26-129">In hello results pane, select **Benefitsolver**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="0ae26-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="0ae26-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="0ae26-131">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0ae26-131">Configure single sign-on</span></span>

<span data-ttu-id="0ae26-132">Bu bölümde Hello amacı nasıl tooenable kullanıcılar tooauthenticate tooBenefitsolver Federasyon kullanarak Azure AD'de hesabıyla hello SAML protokolünü temel toooutline ' dir.</span><span class="sxs-lookup"><span data-stu-id="0ae26-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooBenefitsolver with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="0ae26-133">Benefitsolver uygulamanızı hello SAML onaylar tooadd özel öznitelik eşlemelerini tooyour gerektiren belirli bir biçimde, bekliyor **saml belirteci öznitelikleri** yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="0ae26-133">Your Benefitsolver application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> 

<span data-ttu-id="0ae26-134">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="0ae26-134">hello following screenshot shows an example for this.</span></span>

<span data-ttu-id="0ae26-135">![Öznitelikleri](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="0ae26-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="0ae26-136">**tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0ae26-136">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ae26-137">Merhaba hello üzerinde Klasik Azure portalı içinde **Benefitsolver** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **tek oturum yapılandırma üzerinde aktar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="0ae26-137">In hello Azure classic portal, on hello **Benefitsolver** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="0ae26-138">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="0ae26-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="0ae26-139">Merhaba üzerinde **nasıl tooBenefitsolver üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0ae26-139">On hello **How would you like users toosign on tooBenefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="0ae26-140">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="0ae26-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="0ae26-141">Merhaba üzerinde **uygulama ayarlarını yapılandır** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0ae26-141">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="0ae26-142">![Uygulama ayarlarını yapılandırmak](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "uygulaması ayarlarını yapılandır")</span><span class="sxs-lookup"><span data-stu-id="0ae26-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="0ae26-143">Merhaba, **oturum üzerinde URL'si** metin kutusuna, türü **http://azure.benefitsolver.com**.</span><span class="sxs-lookup"><span data-stu-id="0ae26-143">In hello **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="0ae26-144">Merhaba, **yanıt URL'si** metin kutusuna, türü **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span><span class="sxs-lookup"><span data-stu-id="0ae26-144">In hello **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="0ae26-145">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0ae26-145">Click **Next**.</span></span>
4. <span data-ttu-id="0ae26-146">Hello üzerinde **çoklu oturum açma sırasında Benefitsolver yapılandırma** sayfası, toodownload meta verileriniz tıklatın **karşıdan meta veri**ve hello meta veri dosyası, bilgisayarınıza yerel olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0ae26-146">On hello **Configure single sign-on at Benefitsolver** page, toodownload your metadata, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="0ae26-147">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="0ae26-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="0ae26-148">İndirilen hello meta veri dosyası tooyour Benefitsolver Destek ekibine gönderin.</span><span class="sxs-lookup"><span data-stu-id="0ae26-148">Send hello downloaded metadata file tooyour Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="0ae26-149">Benefitsolver destek ekibinize toodo hello gerçek SSO yapılandırmasına sahip.</span><span class="sxs-lookup"><span data-stu-id="0ae26-149">Your Benefitsolver support team has toodo hello actual SSO configuration.</span></span> <span data-ttu-id="0ae26-150">SSO, aboneliğiniz için etkinleştirildiğinde, bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="0ae26-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="0ae26-151">Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0ae26-151">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="0ae26-152">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="0ae26-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="0ae26-153">Hello içinde hello üst menüsünde **öznitelikleri** tooopen hello **SAML belirteci öznitelikleri** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0ae26-153">In hello menu on hello top, click **Attributes** tooopen hello **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="0ae26-154">![Öznitelikleri](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="0ae26-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="0ae26-155">tooadd hello gerekli öznitelik eşlemelerini hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0ae26-155">tooadd hello required attribute mappings, perform hello following steps:</span></span>
   
   <span data-ttu-id="0ae26-156">![Öznitelikleri](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="0ae26-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="0ae26-157">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="0ae26-157">Attribute Name</span></span> | <span data-ttu-id="0ae26-158">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="0ae26-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="0ae26-159">İstemci kimliği</span><span class="sxs-lookup"><span data-stu-id="0ae26-159">ClientID</span></span> |<span data-ttu-id="0ae26-160">Bu değer tooget Benefitsolver destek ekibinden gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ae26-160">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="0ae26-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="0ae26-161">ClientKey</span></span> |<span data-ttu-id="0ae26-162">Bu değer tooget Benefitsolver destek ekibinden gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ae26-162">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="0ae26-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="0ae26-163">LogoutURL</span></span> |<span data-ttu-id="0ae26-164">Bu değer tooget Benefitsolver destek ekibinden gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ae26-164">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="0ae26-165">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="0ae26-165">EmployeeID</span></span> |<span data-ttu-id="0ae26-166">Bu değer tooget Benefitsolver destek ekibinden gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ae26-166">You need tooget this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="0ae26-167">Yukarıdaki hello tablosundaki her veri satırı için tıklatın **kullanıcı özniteliği eklemek**.</span><span class="sxs-lookup"><span data-stu-id="0ae26-167">For each data row in hello table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="0ae26-168">Merhaba, **öznitelik adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="0ae26-168">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
   3. <span data-ttu-id="0ae26-169">Merhaba, **öznitelik değeri** metin kutusuna, ilgili satır için gösterilen select hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="0ae26-169">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
   4. <span data-ttu-id="0ae26-170">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0ae26-170">Click **Complete**.</span></span>
9. <span data-ttu-id="0ae26-171">Tıklatın **değişiklikleri uygulamak**.</span><span class="sxs-lookup"><span data-stu-id="0ae26-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="0ae26-172">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="0ae26-172">Configure user provisioning</span></span>
<span data-ttu-id="0ae26-173">Benefitsolver içine sipariş tooenable Azure AD kullanıcıların toolog bunların Benefitsolver sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0ae26-173">In order tooenable Azure AD users toolog into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="0ae26-174">Benefitsolver Hello durumda çalışan uygulamanızda Census dosyası sisteminizden HRIS (genellikle her gece) aracılığıyla doldurulmuş verilerdir.</span><span class="sxs-lookup"><span data-stu-id="0ae26-174">In hello case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="0ae26-175">API AAD kullanıcı hesaplarının Benefitsolver tooprovision tarafından sağlanan veya herhangi diğer Benefitsolver kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ae26-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver tooprovision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="0ae26-176">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="0ae26-176">Assigning users</span></span>
<span data-ttu-id="0ae26-177">tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ae26-177">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a><span data-ttu-id="0ae26-178">tooassign kullanıcılar tooBenefitsolver hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0ae26-178">tooassign users tooBenefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="0ae26-179">Hello Klasik Azure portalı, bir test hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0ae26-179">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="0ae26-180">Hello üzerinde ** Benefitsolver ** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.</span><span class="sxs-lookup"><span data-stu-id="0ae26-180">On hello **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="0ae26-181">![Kullanıcılar atama](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "kullanıcı atama")</span><span class="sxs-lookup"><span data-stu-id="0ae26-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="0ae26-182">Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.</span><span class="sxs-lookup"><span data-stu-id="0ae26-182">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="0ae26-183">![Evet](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Evet")</span><span class="sxs-lookup"><span data-stu-id="0ae26-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="0ae26-184">Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="0ae26-184">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="0ae26-185">Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0ae26-185">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

