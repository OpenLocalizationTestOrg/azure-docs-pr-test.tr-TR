---
title: "Öğretici: Azure Active Directory Tümleştirme ile Coupa | Microsoft Docs"
description: "Çoklu oturum açma, otomatik sağlama ve daha fazla etkinleştirmek için Azure Active Directory ile Coupa kullanmayı öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: c952975919cfd948f1b9ea93ff2ac2641a53f923
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="dedab-103">Öğretici: Azure Active Directory Tümleştirme Coupa ile</span><span class="sxs-lookup"><span data-stu-id="dedab-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="dedab-104">Bu öğreticinin amacı, Azure ve Coupa tümleştirmesini göstermektir.</span><span class="sxs-lookup"><span data-stu-id="dedab-104">The objective of this tutorial is to show the integration of Azure and Coupa.</span></span>  
<span data-ttu-id="dedab-105">Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="dedab-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="dedab-106">Geçerli bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="dedab-106">A valid Azure subscription</span></span>
* <span data-ttu-id="dedab-107">Bir Coupa çoklu oturum açma (SSO) abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="dedab-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="dedab-108">Bu öğreticiyi tamamladıktan sonra Coupa için atanmış Azure AD kullanıcılarının uygulama kullanarak çoklu oturum açabilirsiniz [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dedab-108">After completing this tutorial, the Azure AD users you have assigned to Coupa will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="dedab-109">Bu öğreticide gösterilen senaryo, aşağıdaki yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="dedab-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="dedab-110">Uygulama tümleştirmesi Coupa için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="dedab-110">Enabling the application integration for Coupa</span></span>
* <span data-ttu-id="dedab-111">Çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dedab-111">Configuring single sign-on</span></span>
* <span data-ttu-id="dedab-112">Kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="dedab-112">Configuring user provisioning</span></span>
* <span data-ttu-id="dedab-113">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="dedab-113">Assigning users</span></span>

<span data-ttu-id="dedab-114">![Senaryo](./media/active-directory-saas-coupa-tutorial/IC791897.png "senaryosu")</span><span class="sxs-lookup"><span data-stu-id="dedab-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-coupa"></a><span data-ttu-id="dedab-115">Coupa uygulama tümleştirmeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="dedab-115">Enable the application integration for Coupa</span></span>
<span data-ttu-id="dedab-116">Bu bölümün amacı Coupa için uygulama tümleştirme sağlamak üzere nasıl anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="dedab-116">The objective of this section is to outline how to enable the application integration for Coupa.</span></span>

<span data-ttu-id="dedab-117">**Coupa uygulama tümleştirmesini etkinleştirmek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="dedab-117">**To enable the application integration for Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="dedab-118">Azure Klasik portalında, sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dedab-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="dedab-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="dedab-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="dedab-120">Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="dedab-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="dedab-121">Dizin görünümünde uygulamaları görünümü açmak için **uygulamaları** üst menüde.</span><span class="sxs-lookup"><span data-stu-id="dedab-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="dedab-122">![Uygulamaları](./media/active-directory-saas-coupa-tutorial/IC700994.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="dedab-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="dedab-123">Tıklatın **Ekle** sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="dedab-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="dedab-124">![Uygulama ekleme](./media/active-directory-saas-coupa-tutorial/IC749321.png "uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="dedab-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="dedab-125">Üzerinde **ne yapmak istiyorsunuz** iletişim kutusunda, tıklatın **Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="dedab-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="dedab-126">![Galeriden bir uygulama eklemek](./media/active-directory-saas-coupa-tutorial/IC749322.png "Galeriden bir uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="dedab-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="dedab-127">İçinde **arama kutusu**, türü **Coupa**.</span><span class="sxs-lookup"><span data-stu-id="dedab-127">In the **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="dedab-128">![Uygulama Galerisi](./media/active-directory-saas-coupa-tutorial/IC791898.png "uygulama Galerisi")</span><span class="sxs-lookup"><span data-stu-id="dedab-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="dedab-129">Sonuçlar bölmesinde seçin **Coupa**ve ardından **tam** uygulama eklemek için.</span><span class="sxs-lookup"><span data-stu-id="dedab-129">In the results pane, select **Coupa**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="dedab-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="dedab-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="dedab-131">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="dedab-131">Configure single sign-on</span></span>

<span data-ttu-id="dedab-132">Bu bölümün amacı kullanıcıların Coupa için kendi hesabıyla SAML protokolünü temel Federasyon kullanarak Azure AD kimlik doğrulaması sağlamak nasıl anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="dedab-132">The objective of this section is to outline how to enable users to authenticate to Coupa with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="dedab-133">Coupa için çoklu oturum açmayı yapılandırma parmak izi değerinin bir sertifika almanızı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="dedab-133">Configuring single sign-on for Coupa requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="dedab-134">Bu yordama bilmiyorsanız bkz [bir sertifikanın parmak izi değerini almak nasıl](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="dedab-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="dedab-135">**Çoklu oturum açma yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="dedab-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="dedab-136">Coupa şirket sitenize yönetici olarak oturum açma.</span><span class="sxs-lookup"><span data-stu-id="dedab-136">Sign on to your Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="dedab-137">Git **Kurulum \> güvenlik denetimi**.</span><span class="sxs-lookup"><span data-stu-id="dedab-137">Go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="dedab-138">![Güvenlik denetimleri](./media/active-directory-saas-coupa-tutorial/IC791900.png "güvenlik denetimleri")</span><span class="sxs-lookup"><span data-stu-id="dedab-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="dedab-139">Bilgisayarınıza Coupa meta veri dosyası indirmek için tıklayın **karşıdan yükleme ve SP meta verileri içeri aktarma**.</span><span class="sxs-lookup"><span data-stu-id="dedab-139">To download the Coupa metadata file to your computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="dedab-140">![Coupa SP meta veri](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP meta verileri")</span><span class="sxs-lookup"><span data-stu-id="dedab-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="dedab-141">Farklı tarayıcı penceresinde, Klasik Azure portalında oturum açma.</span><span class="sxs-lookup"><span data-stu-id="dedab-141">In a different browser window, sign on to the Azure classic portal.</span></span>
5. <span data-ttu-id="dedab-142">Üzerinde **Coupa** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma yapılandırma** açmak için **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="dedab-142">On the **Coupa** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="dedab-143">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-coupa-tutorial/IC791902.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dedab-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="dedab-144">Üzerinde **Coupa için oturum açmasını nasıl istiyorsunuz** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dedab-144">On the **How would you like users to sign on to Coupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="dedab-145">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-coupa-tutorial/IC791903.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dedab-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="dedab-146">Üzerinde **uygulama URL'sini Yapılandır** sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dedab-146">On the **Configure App URL** page, perform the following steps:</span></span>
   
   <span data-ttu-id="dedab-147">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-coupa-tutorial/IC791904.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dedab-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="dedab-148">İçinde **oturum üzerinde URL'si** metin kutusuna, Coupa uygulamanıza oturum açmaya kullanıcılarınız tarafından kullanılan türü URL'si (örn: "*http://company.Coupa.com*").</span><span class="sxs-lookup"><span data-stu-id="dedab-148">In the **Sign On URL** textbox, type URL used by your users to sign on to your Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="dedab-149">İndirilen Coupa meta veri dosyanızı açın ve ardından kopyalama **AssertionConsumerService dizin/URL**.</span><span class="sxs-lookup"><span data-stu-id="dedab-149">Open your downloaded Coupa metadata file, and then copy the **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="dedab-150">İçinde **Coupa yanıt URL'si** metin kutusuna, Yapıştır **AssertionConsumerService dizin/URL** değeri.</span><span class="sxs-lookup"><span data-stu-id="dedab-150">In the **Coupa Reply URL** textbox, paste the **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="dedab-151">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dedab-151">Click **Next**.</span></span>
8. <span data-ttu-id="dedab-152">Üzerinde **çoklu oturum açma sırasında Coupa yapılandırmak** , meta veriler indirilemedi sayfasını tıklatın **karşıdan meta veri**ve ardından dosyayı bilgisayarınıza yerel olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="dedab-152">On the **Configure single sign-on at Coupa** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
   
   <span data-ttu-id="dedab-153">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-coupa-tutorial/IC791905.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dedab-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="dedab-154">Coupa şirket sitesinde Git **Kurulum \> güvenlik denetimi**.</span><span class="sxs-lookup"><span data-stu-id="dedab-154">On the Coupa company site, go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="dedab-155">![Güvenlik denetimleri](./media/active-directory-saas-coupa-tutorial/IC791900.png "güvenlik denetimleri")</span><span class="sxs-lookup"><span data-stu-id="dedab-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="dedab-156">İçinde **Coupa kimlik bilgilerini kullanarak oturum** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dedab-156">In the **Log in using Coupa credentials** section, perform the following steps:</span></span>  

   <span data-ttu-id="dedab-157">![Coupa kimlik bilgilerini kullanarak oturum](./media/active-directory-saas-coupa-tutorial/IC791906.png "Coupa kimlik bilgilerini kullanarak oturum açın")</span><span class="sxs-lookup"><span data-stu-id="dedab-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="dedab-158">Seçin **SAML kullanarak oturum**.</span><span class="sxs-lookup"><span data-stu-id="dedab-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="dedab-159">Tıklatın **Gözat** indirilen Azure Active meta veri dosyanızı karşıya yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="dedab-159">Click **Browse** to upload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="dedab-160">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dedab-160">Click **Save**.</span></span>
11. <span data-ttu-id="dedab-161">Klasik Azure portalı, çoklu oturum açma yapılandırması onay seçin ve ardından **tam** kapatmak için **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="dedab-161">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="dedab-162">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-coupa-tutorial/IC791907.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dedab-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="dedab-163">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="dedab-163">Configure user provisioning</span></span>

<span data-ttu-id="dedab-164">Azure AD kullanıcıların Coupa oturum etkinleştirmek için bunların Coupa sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="dedab-164">In order to enable Azure AD users to log into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="dedab-165">Coupa söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="dedab-165">In the case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="dedab-166">**Kullanıcı sağlamayı yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="dedab-166">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="dedab-167">Oturum, **Coupa** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="dedab-167">Log in to your **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="dedab-168">Üstteki menüde tıklatın **Kurulum**ve ardından **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="dedab-168">In the menu on the top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="dedab-169">![Kullanıcıların](./media/active-directory-saas-coupa-tutorial/IC791908.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="dedab-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="dedab-170">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dedab-170">Click **Create**.</span></span>
   
   <span data-ttu-id="dedab-171">![Kullanıcılar oluşturma](./media/active-directory-saas-coupa-tutorial/IC791909.png "kullanıcıları oluşturun")</span><span class="sxs-lookup"><span data-stu-id="dedab-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="dedab-172">İçinde **kullanıcı oluşturma** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dedab-172">In the **User Create** section, perform the following steps:</span></span>
   
   <span data-ttu-id="dedab-173">![Kullanıcı ayrıntılarını](./media/active-directory-saas-coupa-tutorial/IC791910.png "kullanıcı ayrıntıları")</span><span class="sxs-lookup"><span data-stu-id="dedab-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="dedab-174">Tür **oturum açma**, **ad**, **Soyadı**, **tek oturum açma kimliği**, **e-posta** özniteliklerini bir Geçerli bir Azure Active Directory hesabı ilgili metin kutularına içine sağlamak istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="dedab-174">Type the **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="dedab-175">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dedab-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="dedab-176">Azure Active Directory hesap sahibi etkin duruma gelmesi hesabı onaylamak için bir bağlantı içeren bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="dedab-176">The Azure Active Directory account holder will get an email with a link to confirm the account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="dedab-177">API sağlama AAD kullanıcı hesaplarına Coupa tarafından sağlanan veya herhangi diğer Coupa kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dedab-177">You can use any other Coupa user account creation tools or APIs provided by Coupa to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="dedab-178">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="dedab-178">Assign users</span></span>
<span data-ttu-id="dedab-179">Yapılandırmanızı test etmek için uygulama erişimi atayarak kullanarak izin vermek istediğiniz Azure AD kullanıcılarının vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="dedab-179">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="dedab-180">**Kullanıcılar için Coupa atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="dedab-180">**To assign users to Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="dedab-181">Klasik Azure portalında bir test hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dedab-181">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="dedab-182">Üzerinde ** Coupa ** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.</span><span class="sxs-lookup"><span data-stu-id="dedab-182">On the **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="dedab-183">![Kullanıcılar atama](./media/active-directory-saas-coupa-tutorial/IC791911.png "kullanıcı atama")</span><span class="sxs-lookup"><span data-stu-id="dedab-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="dedab-184">Test kullanıcınız seçin, **atamak**ve ardından **Evet** , atama onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="dedab-184">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="dedab-185">![Evet](./media/active-directory-saas-coupa-tutorial/IC767830.png "Evet")</span><span class="sxs-lookup"><span data-stu-id="dedab-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="dedab-186">Çoklu oturum açma ayarlarınızı test etmek isterseniz, erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="dedab-186">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="dedab-187">Erişim paneli hakkında daha fazla ayrıntı için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dedab-187">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

