---
title: "Öğretici: Azure Active Directory Tümleştirme SCC yaşam | Microsoft Docs"
description: "Çoklu oturum açma, otomatik sağlama ve daha fazla etkinleştirmek için Azure Active Directory ile SCC yaşam döngüsü kullanmayı öğrenin!"
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
ms.openlocfilehash: 9a30bcca720ff135d0180d73f46e78403e9bca43
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="8a92d-103">Öğretici: Azure Active Directory Tümleştirme ile SCC yaşam döngüsü</span><span class="sxs-lookup"><span data-stu-id="8a92d-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="8a92d-104">Bu öğreticinin amacı, Azure ve SCC yaşam döngüsü tümleştirmesini göstermektir.</span><span class="sxs-lookup"><span data-stu-id="8a92d-104">The objective of this tutorial is to show the integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="8a92d-105">Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="8a92d-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="8a92d-106">Geçerli bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="8a92d-106">A valid Azure subscription</span></span>
* <span data-ttu-id="8a92d-107">Bir SCC yaşam döngüsü çoklu oturum açma (SSO) abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="8a92d-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="8a92d-108">Bu öğreticiyi tamamladıktan sonra SCC yaşam döngüsü için atanmış Azure AD kullanıcıları çoklu oturum açma, SCC yaşam döngüsü şirket sitenizdeki (servis sağlayıcı tarafından başlatılan oturum açma) uygulamaya veya kullanarak okuyamayacak [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8a92d-108">After completing this tutorial, the Azure AD users you have assigned to SCC LifeCycle will be able to single sign into the application at your SCC LifeCycle company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="8a92d-109">Bu öğreticide gösterilen senaryo, aşağıdaki yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="8a92d-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="8a92d-110">Uygulama tümleştirmesi SCC yaşam döngüsü için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="8a92d-110">Enabling the application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="8a92d-111">Çoklu oturum açma (SSO) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8a92d-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="8a92d-112">Kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="8a92d-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="8a92d-113">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="8a92d-113">Assigning users</span></span>

<span data-ttu-id="8a92d-114">![Senaryo](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "senaryosu")</span><span class="sxs-lookup"><span data-stu-id="8a92d-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-scc-lifecycle"></a><span data-ttu-id="8a92d-115">SCC yaşam döngüsü için uygulama tümleştirmeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="8a92d-115">Enable the application integration for SCC LifeCycle</span></span>
<span data-ttu-id="8a92d-116">Bu bölümün amacı SCC yaşam döngüsü için uygulama tümleştirme sağlamak üzere nasıl anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="8a92d-116">The objective of this section is to outline how to enable the application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="8a92d-117">**SCC yaşam döngüsü için uygulama tümleştirmesini etkinleştirmek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8a92d-117">**To enable the application integration for SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="8a92d-118">Azure Klasik portalında, sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8a92d-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="8a92d-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="8a92d-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="8a92d-120">Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="8a92d-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8a92d-121">Dizin görünümünde uygulamaları görünümü açmak için **uygulamaları** üst menüde.</span><span class="sxs-lookup"><span data-stu-id="8a92d-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="8a92d-122">![Uygulamaları](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="8a92d-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="8a92d-123">Tıklatın **Ekle** sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="8a92d-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="8a92d-124">![Uygulama ekleme](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="8a92d-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="8a92d-125">Üzerinde **ne yapmak istiyorsunuz** iletişim kutusunda, tıklatın **Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="8a92d-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="8a92d-126">![Galeriden bir uygulama eklemek](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Galeriden bir uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="8a92d-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="8a92d-127">İçinde **arama kutusu**, türü **SCC yaşam döngüsü**.</span><span class="sxs-lookup"><span data-stu-id="8a92d-127">In the **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="8a92d-128">![Uygulama Galerisi](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "uygulama Galerisi")</span><span class="sxs-lookup"><span data-stu-id="8a92d-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="8a92d-129">Sonuçlar bölmesinde seçin **SCC yaşam döngüsü**ve ardından **tam** uygulama eklemek için.</span><span class="sxs-lookup"><span data-stu-id="8a92d-129">In the results pane, select **SCC LifeCycle**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="8a92d-130">![SCC yaşam döngüsü](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC yaşam döngüsü")</span><span class="sxs-lookup"><span data-stu-id="8a92d-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="8a92d-131">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="8a92d-131">Configure single sign-on</span></span>

<span data-ttu-id="8a92d-132">Bu bölümün amacı kullanıcıların SCC yaşam döngüsü için kendi hesabıyla SAML protokolünü temel Federasyon kullanarak Azure AD kimlik doğrulaması sağlamak nasıl anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="8a92d-132">The objective of this section is to outline how to enable users to authenticate to SCC LifeCycle with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="8a92d-133">**Çoklu oturum açma yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8a92d-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="8a92d-134">Azure Klasik portalında üzerinde **SCC yaşam döngüsü** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma özelliğini yapılandırın** açmak için ** tek oturum yapılandırma üzerinde Aktar ** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8a92d-134">In the Azure classic portal, on the **SCC LifeCycle** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="8a92d-135">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="8a92d-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="8a92d-136">Üzerinde **SCC yaşam döngüsü için oturum açmasını nasıl istiyorsunuz** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="8a92d-136">On the **How would you like users to sign on to SCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="8a92d-137">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="8a92d-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="8a92d-138">Üzerinde **uygulama URL'sini Yapılandır** sayfasında **oturum üzerinde URL'si** metin kutusuna, türü URL kullanıcılarınız tarafından şu biçimi kullanarak SCC yaşam döngüsü uygulamanıza oturum açma için kullanılan "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*" ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="8a92d-138">On the **Configure App URL** page, in the **Sign On URL** textbox, type the URL used by your users to sign on to your SCC LifeCycle application using the following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="8a92d-139">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="8a92d-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="8a92d-140">Üzerinde **çoklu oturum açma SCC yaşam döngüsü sırasında yapılandırma** sayfasında, **karşıdan meta veri**ve meta veri dosyası, bilgisayarınıza yerel olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8a92d-140">On the **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="8a92d-141">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="8a92d-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="8a92d-142">Bu meta veri dosyası SCC yaşam döngüsü Destek ekibine iletin.</span><span class="sxs-lookup"><span data-stu-id="8a92d-142">Forward that Metadata file to SCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="8a92d-143">Çoklu oturum açma SCC yaşam döngüsü destek ekibi tarafından etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a92d-143">Single sign-on has to be enabled by the SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="8a92d-144">Klasik Azure portalı, çoklu oturum açma yapılandırması onay seçin ve ardından **tam** kapatmak için **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8a92d-144">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="8a92d-145">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="8a92d-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="8a92d-146">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="8a92d-146">Configure user provisioning</span></span>

<span data-ttu-id="8a92d-147">Azure AD kullanıcıların SCC yaşam döngüsü oturum etkinleştirmek için bunların SCC yaşam döngüsü sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8a92d-147">In order to enable Azure AD users to log into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="8a92d-148">Kullanıcı SCC yaşam döngüsü için sağlama yapılandırmanız için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="8a92d-148">There is no action item for you to configure user provisioning to SCC LifeCycle.</span></span>

<span data-ttu-id="8a92d-149">Atanmış bir kullanıcı SCC yaşam döngüsü oturum açmaya çalıştığında SCC yaşam döngüsü hesap gerekirse, otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8a92d-149">When an assigned user tries to log into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="8a92d-150">API sağlama AAD kullanıcı hesaplarına SCC yaşam döngüsü tarafından sağlanan veya herhangi diğer SCC yaşam döngüsü kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a92d-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="8a92d-151">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="8a92d-151">Assign users</span></span>
<span data-ttu-id="8a92d-152">Yapılandırmanızı test etmek için uygulama erişimi atayarak kullanarak izin vermek istediğiniz Azure AD kullanıcılarının vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a92d-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="8a92d-153">**SCC yaşam döngüsü için kullanıcılara atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8a92d-153">**To assign users to SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="8a92d-154">Klasik Azure portalında bir test hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8a92d-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="8a92d-155">Üzerinde ** SCC yaşam döngüsü ** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.</span><span class="sxs-lookup"><span data-stu-id="8a92d-155">On the **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="8a92d-156">![Kullanıcılar atama](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "kullanıcı atama")</span><span class="sxs-lookup"><span data-stu-id="8a92d-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="8a92d-157">Test kullanıcınız seçin, **atamak**ve ardından **Evet** , atama onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="8a92d-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="8a92d-158">![Evet](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Evet")</span><span class="sxs-lookup"><span data-stu-id="8a92d-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="8a92d-159">SSO ayarlarınızı test etmek isterseniz, erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="8a92d-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="8a92d-160">Erişim paneli hakkında daha fazla ayrıntı için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8a92d-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

