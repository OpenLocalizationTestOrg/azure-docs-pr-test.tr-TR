---
title: "Öğretici: Azure Active Directory Tümleştirme ile Benefitsolver | Microsoft Docs"
description: "Çoklu oturum açma, otomatik sağlama ve daha fazla etkinleştirmek için Azure Active Directory ile Benefitsolver kullanmayı öğrenin!"
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
ms.openlocfilehash: 8a13dd5ebd872f86247158379b28bc291a9c9d83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="71609-103">Öğretici: Azure Active Directory Tümleştirme Benefitsolver ile</span><span class="sxs-lookup"><span data-stu-id="71609-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="71609-104">Bu öğreticinin amacı, Azure ve Benefitsolver tümleştirmesini göstermektir.</span><span class="sxs-lookup"><span data-stu-id="71609-104">The objective of this tutorial is to show the integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="71609-105">Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="71609-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="71609-106">Geçerli bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="71609-106">A valid Azure subscription</span></span>
* <span data-ttu-id="71609-107">Bir Benefitsolver çoklu oturum açma (SSO) abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="71609-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="71609-108">Bu öğreticiyi tamamladıktan sonra Benefitsolver için atanmış Azure AD kullanıcılarının uygulama kullanarak çoklu oturum açabilirsiniz [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="71609-108">After completing this tutorial, the Azure AD users you have assigned to Benefitsolver will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="71609-109">Bu öğreticide gösterilen senaryo, aşağıdaki yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="71609-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="71609-110">Uygulama tümleştirmesi Benefitsolver için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="71609-110">Enabling the application integration for Benefitsolver</span></span>
2. <span data-ttu-id="71609-111">Çoklu oturum açma (SSO) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="71609-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="71609-112">Kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="71609-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="71609-113">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="71609-113">Assigning users</span></span>

<span data-ttu-id="71609-114">![Senaryo](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "senaryosu")</span><span class="sxs-lookup"><span data-stu-id="71609-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-benefitsolver"></a><span data-ttu-id="71609-115">Uygulama tümleştirmesi Benefitsolver için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="71609-115">Enabling the application integration for Benefitsolver</span></span>
<span data-ttu-id="71609-116">Bu bölümün amacı Benefitsolver için uygulama tümleştirme sağlamak üzere nasıl anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="71609-116">The objective of this section is to outline how to enable the application integration for Benefitsolver.</span></span>

### <a name="to-enable-the-application-integration-for-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="71609-117">Benefitsolver uygulama tümleştirmesini etkinleştirmek için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="71609-117">To enable the application integration for Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="71609-118">Azure Klasik portalında, sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="71609-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="71609-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="71609-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="71609-120">Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="71609-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="71609-121">Dizin görünümünde uygulamaları görünümü açmak için **uygulamaları** üst menüde.</span><span class="sxs-lookup"><span data-stu-id="71609-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="71609-122">![Uygulamaları](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="71609-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="71609-123">Tıklatın **Ekle** sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="71609-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="71609-124">![Uygulama ekleme](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="71609-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="71609-125">Üzerinde **ne yapmak istiyorsunuz** iletişim kutusunda, tıklatın **Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="71609-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="71609-126">![Galeriden bir uygulama eklemek](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Galeriden bir uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="71609-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="71609-127">İçinde **arama kutusu**, türü **Benefitsolver**.</span><span class="sxs-lookup"><span data-stu-id="71609-127">In the **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="71609-128">![Uygulama Galerisi](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "uygulama Galerisi")</span><span class="sxs-lookup"><span data-stu-id="71609-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="71609-129">Sonuçlar bölmesinde seçin **Benefitsolver**ve ardından **tam** uygulama eklemek için.</span><span class="sxs-lookup"><span data-stu-id="71609-129">In the results pane, select **Benefitsolver**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="71609-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="71609-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="71609-131">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="71609-131">Configure single sign-on</span></span>

<span data-ttu-id="71609-132">Bu bölümün amacı kullanıcıların Benefitsolver için kendi hesabıyla SAML protokolünü temel Federasyon kullanarak Azure AD kimlik doğrulaması sağlamak nasıl anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="71609-132">The objective of this section is to outline how to enable users to authenticate to Benefitsolver with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="71609-133">Özel öznitelik eşlemelerini eklemenizi gerektirir belirli bir biçimde SAML onaylar Benefitsolver uygulamanızı bekler, **saml belirteci öznitelikleri** yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="71609-133">Your Benefitsolver application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> 

<span data-ttu-id="71609-134">Aşağıdaki ekran görüntüsünde bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="71609-134">The following screenshot shows an example for this.</span></span>

<span data-ttu-id="71609-135">![Öznitelikleri](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="71609-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="71609-136">**Çoklu oturum açma yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="71609-136">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="71609-137">Azure Klasik portalında üzerinde **Benefitsolver** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma özelliğini yapılandırın** açmak için **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="71609-137">In the Azure classic portal, on the **Benefitsolver** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="71609-138">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="71609-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="71609-139">Üzerinde **Benefitsolver için oturum açmasını nasıl istiyorsunuz** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="71609-139">On the **How would you like users to sign on to Benefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="71609-140">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="71609-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="71609-141">Üzerinde **uygulama ayarlarını yapılandır** sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="71609-141">On the **Configure App Settings** page, perform the following steps:</span></span>
   
   <span data-ttu-id="71609-142">![Uygulama ayarlarını yapılandırmak](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "uygulaması ayarlarını yapılandır")</span><span class="sxs-lookup"><span data-stu-id="71609-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="71609-143">İçinde **oturum üzerinde URL'si** metin kutusuna, türü **http://azure.benefitsolver.com**.</span><span class="sxs-lookup"><span data-stu-id="71609-143">In the **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="71609-144">İçinde **yanıt URL'si** metin kutusuna, türü **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span><span class="sxs-lookup"><span data-stu-id="71609-144">In the **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="71609-145">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="71609-145">Click **Next**.</span></span>
4. <span data-ttu-id="71609-146">Üzerinde **çoklu oturum açma sırasında Benefitsolver yapılandırma** meta verileriniz, indirme sayfasında, tıklatın **karşıdan meta veri**ve meta veri dosyası, bilgisayarınıza yerel olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="71609-146">On the **Configure single sign-on at Benefitsolver** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="71609-147">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="71609-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="71609-148">İndirilen meta veri dosyası Benefitsolver destek ekibinize gönderin.</span><span class="sxs-lookup"><span data-stu-id="71609-148">Send the downloaded metadata file to your Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="71609-149">Gerçek SSO yapılandırmasını yapmak Benefitsolver destek ekibinize sahiptir.</span><span class="sxs-lookup"><span data-stu-id="71609-149">Your Benefitsolver support team has to do the actual SSO configuration.</span></span> <span data-ttu-id="71609-150">SSO, aboneliğiniz için etkinleştirildiğinde, bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="71609-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="71609-151">Klasik Azure portalı, çoklu oturum açma yapılandırması onay seçin ve ardından **tam** kapatmak için **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="71609-151">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="71609-152">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="71609-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="71609-153">Üstteki menüde tıklatın **öznitelikleri** açmak için **SAML belirteci öznitelikleri** iletişim.</span><span class="sxs-lookup"><span data-stu-id="71609-153">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="71609-154">![Öznitelikleri](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="71609-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="71609-155">Gerekli öznitelik eşlemelerini eklemek için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="71609-155">To add the required attribute mappings, perform the following steps:</span></span>
   
   <span data-ttu-id="71609-156">![Öznitelikleri](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="71609-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="71609-157">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="71609-157">Attribute Name</span></span> | <span data-ttu-id="71609-158">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="71609-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="71609-159">İstemci kimliği</span><span class="sxs-lookup"><span data-stu-id="71609-159">ClientID</span></span> |<span data-ttu-id="71609-160">Bu değer, Benefitsolver destek ekibinden edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="71609-160">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="71609-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="71609-161">ClientKey</span></span> |<span data-ttu-id="71609-162">Bu değer, Benefitsolver destek ekibinden edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="71609-162">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="71609-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="71609-163">LogoutURL</span></span> |<span data-ttu-id="71609-164">Bu değer, Benefitsolver destek ekibinden edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="71609-164">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="71609-165">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="71609-165">EmployeeID</span></span> |<span data-ttu-id="71609-166">Bu değer, Benefitsolver destek ekibinden edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="71609-166">You need to get this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="71609-167">Her veri satırının için yukarıdaki tabloda **kullanıcı özniteliği eklemek**.</span><span class="sxs-lookup"><span data-stu-id="71609-167">For each data row in the table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="71609-168">İçinde **öznitelik adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="71609-168">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
   3. <span data-ttu-id="71609-169">İçinde **öznitelik değeri** metin kutusuna, ilgili satır için gösterilen öznitelik değerini seçin.</span><span class="sxs-lookup"><span data-stu-id="71609-169">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
   4. <span data-ttu-id="71609-170">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="71609-170">Click **Complete**.</span></span>
9. <span data-ttu-id="71609-171">Tıklatın **değişiklikleri uygulamak**.</span><span class="sxs-lookup"><span data-stu-id="71609-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="71609-172">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="71609-172">Configure user provisioning</span></span>
<span data-ttu-id="71609-173">Azure AD kullanıcıların Benefitsolver oturum etkinleştirmek için bunların Benefitsolver sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="71609-173">In order to enable Azure AD users to log into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="71609-174">Benefitsolver söz konusu olduğunda, çalışan uygulamanızda Census dosyası sisteminizden HRIS (genellikle her gece) aracılığıyla doldurulmuş verilerdir.</span><span class="sxs-lookup"><span data-stu-id="71609-174">In the case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="71609-175">API sağlama AAD kullanıcı hesaplarına Benefitsolver tarafından sağlanan veya herhangi diğer Benefitsolver kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71609-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver to provision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="71609-176">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="71609-176">Assigning users</span></span>
<span data-ttu-id="71609-177">Yapılandırmanızı test etmek için uygulama erişimi atayarak kullanarak izin vermek istediğiniz Azure AD kullanıcılarının vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="71609-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="71609-178">Kullanıcılar için Benefitsolver atamak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="71609-178">To assign users to Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="71609-179">Klasik Azure portalında bir test hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="71609-179">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="71609-180">Üzerinde ** Benefitsolver ** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.</span><span class="sxs-lookup"><span data-stu-id="71609-180">On the **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="71609-181">![Kullanıcılar atama](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "kullanıcı atama")</span><span class="sxs-lookup"><span data-stu-id="71609-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="71609-182">Test kullanıcınız seçin, **atamak**ve ardından **Evet** , atama onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="71609-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="71609-183">![Evet](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Evet")</span><span class="sxs-lookup"><span data-stu-id="71609-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="71609-184">Çoklu oturum açma ayarlarınızı test etmek isterseniz, erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="71609-184">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="71609-185">Erişim paneli hakkında daha fazla ayrıntı için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="71609-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

