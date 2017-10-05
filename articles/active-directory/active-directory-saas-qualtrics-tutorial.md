---
title: "Öğretici: Azure Active Directory Tümleştirme ile Qualtrics | Microsoft Docs"
description: "Çoklu oturum açma, otomatik sağlama ve daha fazla etkinleştirmek için Azure Active Directory ile Qualtrics kullanmayı öğrenin!"
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
ms.openlocfilehash: 2fcde595a40dafda7549f5bccb582b57585b314e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="5995a-103">Öğretici: Azure Active Directory Tümleştirme Qualtrics ile</span><span class="sxs-lookup"><span data-stu-id="5995a-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="5995a-104">Bu öğreticinin amacı, Azure ve Qualtrics tümleştirmesini göstermektir.</span><span class="sxs-lookup"><span data-stu-id="5995a-104">The objective of this tutorial is to show the integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="5995a-105">Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="5995a-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="5995a-106">Geçerli bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="5995a-106">A valid Azure subscription</span></span>
* <span data-ttu-id="5995a-107">Bir Qualtrics çoklu oturum açma (SSO) abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="5995a-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="5995a-108">Bu öğreticiyi tamamladıktan sonra Qualtrics için atanmış Azure AD kullanıcıları çoklu oturum açma Qualtrics şirket sitenizdeki (servis sağlayıcı tarafından başlatılan oturum açma) uygulamaya veya kullanarak okuyamayacak [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5995a-108">After completing this tutorial, the Azure AD users you have assigned to Qualtrics will be able to single sign into the application at your Qualtrics company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="5995a-109">Bu öğreticide gösterilen senaryo, aşağıdaki yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="5995a-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="5995a-110">Uygulama tümleştirmesi Qualtrics için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="5995a-110">Enabling the application integration for Qualtrics</span></span>
2. <span data-ttu-id="5995a-111">Çoklu oturum açma (SSO) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5995a-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="5995a-112">Kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="5995a-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="5995a-113">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="5995a-113">Assigning users</span></span>

<span data-ttu-id="5995a-114">![Senaryo](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "senaryosu")</span><span class="sxs-lookup"><span data-stu-id="5995a-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-qualtrics"></a><span data-ttu-id="5995a-115">Uygulama tümleştirmesi Qualtrics için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="5995a-115">Enabling the application integration for Qualtrics</span></span>
<span data-ttu-id="5995a-116">Bu bölümün amacı Qualtrics için uygulama tümleştirme sağlamak üzere nasıl anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="5995a-116">The objective of this section is to outline how to enable the application integration for Qualtrics.</span></span>

<span data-ttu-id="5995a-117">**Qualtrics uygulama tümleştirmesini etkinleştirmek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5995a-117">**To enable the application integration for Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="5995a-118">Azure Klasik portalında, sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5995a-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="5995a-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="5995a-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="5995a-120">Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="5995a-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="5995a-121">Dizin görünümünde uygulamaları görünümü açmak için **uygulamaları** üst menüde.</span><span class="sxs-lookup"><span data-stu-id="5995a-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="5995a-122">![Uygulamaları](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="5995a-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="5995a-123">Tıklatın **Ekle** sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="5995a-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="5995a-124">![Uygulama ekleme](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="5995a-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="5995a-125">Üzerinde **ne yapmak istiyorsunuz** iletişim kutusunda, tıklatın **Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="5995a-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="5995a-126">![Galeriden bir uygulama eklemek](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Galeriden bir uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="5995a-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="5995a-127">İçinde **arama kutusu**, türü **Qualtrics**.</span><span class="sxs-lookup"><span data-stu-id="5995a-127">In the **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="5995a-128">![Uygulama Galerisi](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "uygulama Galerisi")</span><span class="sxs-lookup"><span data-stu-id="5995a-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="5995a-129">Sonuçlar bölmesinde seçin **Qualtrics**ve ardından **tam** uygulama eklemek için.</span><span class="sxs-lookup"><span data-stu-id="5995a-129">In the results pane, select **Qualtrics**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="5995a-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="5995a-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="5995a-131">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5995a-131">Configure single sign-on</span></span>

<span data-ttu-id="5995a-132">Bu bölümün amacı kullanıcıların Qualtrics için kendi hesabıyla SAML protokolünü temel Federasyon kullanarak Azure AD kimlik doğrulaması sağlamak nasıl anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="5995a-132">The objective of this section is to outline how to enable users to authenticate to Qualtrics with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="5995a-133">**Çoklu oturum açma yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5995a-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="5995a-134">Azure Klasik portalında üzerinde **Qualtrics** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma özelliğini yapılandırın** açmak için **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5995a-134">In the Azure classic portal, on the **Qualtrics** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="5995a-135">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="5995a-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="5995a-136">Üzerinde **Qualtrics için oturum açmasını nasıl istiyorsunuz** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5995a-136">On the **How would you like users to sign on to Qualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="5995a-137">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="5995a-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="5995a-138">Üzerinde **uygulama URL'sini Yapılandır** sayfasında **üzerinde Qualtrics oturum URL'si** metin kutusuna, URL'nizi yazın (örneğin: "*https://ssotest2ut1.qualtrics.com*") ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5995a-138">On the **Configure App URL** page, in the **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="5995a-139">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="5995a-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="5995a-140">Üzerinde **çoklu oturum açma sırasında Qualtrics yapılandırma** sayfasında, **karşıdan meta veri**ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5995a-140">On the **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save the metadata file on your computer.</span></span>
   
   <span data-ttu-id="5995a-141">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="5995a-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="5995a-142">Meta veri dosyası Qualtrics Destek ekibine gönderin.</span><span class="sxs-lookup"><span data-stu-id="5995a-142">Send the metadata file to the Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="5995a-143">SSO yapılandırma Qualtrics destek ekibi tarafından gerçekleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5995a-143">The SSO configuration has to be performed by the Qualtrics support team.</span></span> <span data-ttu-id="5995a-144">Yapılandırma tamamlandıktan hemen sonra bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="5995a-144">You will get a notification as soon as the configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="5995a-145">Klasik Azure portalı, çoklu oturum açma yapılandırması onay seçin ve ardından **tam** kapatmak için **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5995a-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="5995a-146">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="5995a-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="5995a-147">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="5995a-147">Configure user provisioning</span></span>

<span data-ttu-id="5995a-148">Kullanıcı için Qualtrics hazırlama yapılandırmanız için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="5995a-148">There is no action item for you to configure user provisioning to Qualtrics.</span></span> <span data-ttu-id="5995a-149">Atanmış bir kullanıcı erişim paneli kullanılarak Qualtrics oturum açmaya çalıştığında Qualtrics kullanıcının var olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="5995a-149">When an assigned user tries to log into Qualtrics using the access panel, Qualtrics checks whether the user exists.</span></span>  

<span data-ttu-id="5995a-150">Hiçbir kullanıcı hesabı varsa kullanılabilir henüz, Qualtrics tarafından otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5995a-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="5995a-151">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="5995a-151">Assign users</span></span>
<span data-ttu-id="5995a-152">Yapılandırmanızı test etmek için uygulama erişimi atayarak kullanarak izin vermek istediğiniz Azure AD kullanıcılarının vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5995a-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="5995a-153">**Kullanıcılar için Qualtrics atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5995a-153">**To assign users to Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="5995a-154">Klasik Azure portalında bir test hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5995a-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="5995a-155">Üzerinde **Qualtrics** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.</span><span class="sxs-lookup"><span data-stu-id="5995a-155">On the **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="5995a-156">![Kullanıcılar atama](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "kullanıcı atama")</span><span class="sxs-lookup"><span data-stu-id="5995a-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="5995a-157">Test kullanıcınız seçin, **atamak**ve ardından **Evet** , atama onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="5995a-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="5995a-158">![Evet](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Evet")</span><span class="sxs-lookup"><span data-stu-id="5995a-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="5995a-159">SSO ayarlarınızı test etmek isterseniz, erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="5995a-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="5995a-160">Erişim paneli hakkında daha fazla ayrıntı için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5995a-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

