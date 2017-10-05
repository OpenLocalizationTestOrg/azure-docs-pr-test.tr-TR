---
title: "Öğretici: Azure Active Directory Tümleştirme ile Cisco Webex | Microsoft Docs"
description: "Cisco Webex Azure Active Directory ile çoklu oturum açma, otomatik sağlama ve daha fazlasını sağlamak için nasıl kullanılacağını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: b44b1a5b3e988a51db3325ec8a181651fa84e768
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="b0bad-103">Öğretici: Cisco Webex Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="b0bad-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="b0bad-104">Bu öğreticinin amacı, Azure ve Cisco Webex tümleştirmesini göstermektir.</span><span class="sxs-lookup"><span data-stu-id="b0bad-104">The objective of this tutorial is to show the integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="b0bad-105">Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="b0bad-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="b0bad-106">Geçerli bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="b0bad-106">A valid Azure subscription</span></span>
* <span data-ttu-id="b0bad-107">Cisco Webex Kiracı</span><span class="sxs-lookup"><span data-stu-id="b0bad-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="b0bad-108">Bu öğreticiyi tamamladıktan sonra Cisco Webex atamış Azure AD kullanıcıları çoklu oturum açma, Cisco Webex şirket sitenizdeki (servis sağlayıcı tarafından başlatılan oturum açma) uygulamaya veya kullanarak okuyamayacak [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b0bad-108">After completing this tutorial, the Azure AD users you have assigned to Cisco Webex will be able to single sign into the application at your Cisco Webex company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="b0bad-109">Bu öğreticide gösterilen senaryo, aşağıdaki yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="b0bad-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="b0bad-110">Cisco Webex uygulama tümleştirmesi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="b0bad-110">Enabling the application integration for Cisco Webex</span></span>
* <span data-ttu-id="b0bad-111">Çoklu oturum açma (SSO) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b0bad-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="b0bad-112">Kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="b0bad-112">Configuring user provisioning</span></span>
* <span data-ttu-id="b0bad-113">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="b0bad-113">Assigning users</span></span>

<span data-ttu-id="b0bad-114">![Senaryo](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "senaryosu")</span><span class="sxs-lookup"><span data-stu-id="b0bad-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-cisco-webex"></a><span data-ttu-id="b0bad-115">Cisco Webex uygulama tümleştirmeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="b0bad-115">Enable the application integration for Cisco Webex</span></span>
<span data-ttu-id="b0bad-116">Bu bölümün amacı, Cisco Webex için uygulama tümleştirme sağlamak üzere nasıl anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="b0bad-116">The objective of this section is to outline how to enable the application integration for Cisco Webex.</span></span>

<span data-ttu-id="b0bad-117">**Cisco Webex uygulama tümleştirmesini etkinleştirmek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b0bad-117">**To enable the application integration for Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="b0bad-118">Azure Klasik portalında, sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b0bad-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="b0bad-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="b0bad-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="b0bad-120">Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="b0bad-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="b0bad-121">Dizin görünümünde uygulamaları görünümü açmak için **uygulamaları** üst menüde.</span><span class="sxs-lookup"><span data-stu-id="b0bad-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="b0bad-122">![Uygulamaları](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="b0bad-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="b0bad-123">Tıklatın **Ekle** sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="b0bad-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="b0bad-124">![Uygulama ekleme](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="b0bad-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="b0bad-125">Üzerinde **ne yapmak istiyorsunuz** iletişim kutusunda, tıklatın **Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="b0bad-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="b0bad-126">![Galeriden bir uygulama eklemek](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Galeriden bir uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="b0bad-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="b0bad-127">İçinde **arama kutusu**, türü **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="b0bad-127">In the **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="b0bad-128">![Uygulama Galerisi](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "uygulama Galerisi")</span><span class="sxs-lookup"><span data-stu-id="b0bad-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="b0bad-129">Sonuçlar bölmesinde seçin **Cisco Webex**ve ardından **tam** uygulama eklemek için.</span><span class="sxs-lookup"><span data-stu-id="b0bad-129">In the results pane, select **Cisco Webex**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="b0bad-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="b0bad-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="b0bad-131">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="b0bad-131">Configure single sign-on</span></span>

<span data-ttu-id="b0bad-132">Bu bölümün amacı kullanıcıların Cisco Webex kendi hesabıyla SAML protokolünü temel Federasyon kullanarak Azure AD kimlik doğrulaması sağlamak nasıl anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="b0bad-132">The objective of this section is to outline how to enable users to authenticate to Cisco Webex with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="b0bad-133">Bu yordam bir parçası olarak, bir base-64 kodlanmış sertifika oluşturmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b0bad-133">As part of this procedure, you are required to create a base-64 encoded certificate.</span></span> <span data-ttu-id="b0bad-134">Bu yordama bilmiyorsanız bkz [ikili bir sertifika bir metin dosyasına dönüştürme](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="b0bad-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="b0bad-135">**Çoklu oturum açma yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b0bad-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="b0bad-136">Azure Klasik portalında üzerinde **Cisco Webex** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma özelliğini yapılandırın** açmak için **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b0bad-136">In the Azure classic portal, on the **Cisco Webex** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="b0bad-137">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="b0bad-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="b0bad-138">Üzerinde **Cisco Webex oturum açmasını nasıl istiyorsunuz** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="b0bad-138">On the **How would you like users to sign on to Cisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="b0bad-139">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="b0bad-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="b0bad-140">Üzerinde **uygulama URL'sini Yapılandır** sayfasında, aşağıdaki adımları uygulayın ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="b0bad-140">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="b0bad-141">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="b0bad-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="b0bad-142">İçinde **URL SING** metin kutusuna, Cisco Webex Kiracı URL'nizi yazın (örneğin: *http://contoso.webex.com*).</span><span class="sxs-lookup"><span data-stu-id="b0bad-142">In the **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="b0bad-143">İçinde **Cisco Webex yanıt URL'si** metin kutusuna, türü, **Cisco Webex AssertionConsumerService URL** (örn: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span><span class="sxs-lookup"><span data-stu-id="b0bad-143">In the **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="b0bad-144">Üzerinde **çoklu oturum açma sırasında Cisco Webex yapılandırma** , sertifika indirmek için sayfasını tıklatın **indirme sertifika**ve ardından sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b0bad-144">On the **Configure single sign-on at Cisco Webex** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="b0bad-145">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="b0bad-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="b0bad-146">Farklı web tarayıcısı penceresinde Cisco Webex şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b0bad-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="b0bad-147">Üstteki menüde tıklatın **Site Yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="b0bad-147">In the menu on the top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="b0bad-148">![Site Yönetimi](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Yönetimi")</span><span class="sxs-lookup"><span data-stu-id="b0bad-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="b0bad-149">İçinde **sitesi yönetme** 'yi tıklatın **SSO yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="b0bad-149">In the **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="b0bad-150">![SSO yapılandırma](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO yapılandırma")</span><span class="sxs-lookup"><span data-stu-id="b0bad-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="b0bad-151">Federe Web SSO yapılandırma bölümünde aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b0bad-151">In the Federated Web SSO Configuration section, perform the following steps:</span></span>
   
   <span data-ttu-id="b0bad-152">![SSO yapılandırma Federasyon](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federasyon SSO yapılandırma")</span><span class="sxs-lookup"><span data-stu-id="b0bad-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="b0bad-153">Gelen **Federasyon Protokolü** listesinde **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="b0bad-153">From the **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="b0bad-154">Oluşturma bir **Base-64 kodlanmış** indirilen sertifikanızı dosyasından.</span><span class="sxs-lookup"><span data-stu-id="b0bad-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="b0bad-155">Daha fazla ayrıntı için bkz: [ikili bir sertifika bir metin dosyasına dönüştürme](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="b0bad-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="b0bad-156">Base-64 kodlanmış sertifikanızı Not Defteri'nde açın ve içeriğini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="b0bad-156">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span></span>
   4. <span data-ttu-id="b0bad-157">Tıklatın **SAML meta verileri içeri aktarma**ve ardından, base-64 kodlanmış sertifika yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b0bad-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="b0bad-158">Azure Klasik portalında üzerinde **çoklu oturum açma sırasında Cisco Webex yapılandırma** iletişim sayfası, kopya **veren URL'si** değer ve ardından yapıştırın **veren SAML (IDP kimliği) için** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="b0bad-158">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="b0bad-159">Azure Klasik portalında üzerinde **çoklu oturum açma sırasında Cisco Webex yapılandırma** iletişim sayfası, kopya **uzaktan oturum açma URL'si** değer ve ardından yapıştırın **müşteri SSO hizmeti oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="b0bad-159">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Login URL** value, and then paste it into the **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="b0bad-160">Gelen **NameID biçimi** listesinde **e-posta adresi**.</span><span class="sxs-lookup"><span data-stu-id="b0bad-160">From the **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="b0bad-161">İçinde **AuthnContextClassRef** metin kutusuna, türü **urn: OASIS: adları: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="b0bad-161">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="b0bad-162">Azure Klasik portalında üzerinde **çoklu oturum açma sırasında Cisco Webex yapılandırma** iletişim sayfası, kopya **uzak oturum kapatma URL'si** değer ve ardından yapıştırın **müşteri SSO hizmet oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="b0bad-162">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="b0bad-163">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="b0bad-163">Click **Update**.</span></span>
9. <span data-ttu-id="b0bad-164">Azure Klasik portalında üzerinde **çoklu oturum açma sırasında Cisco Webex yapılandırma** iletişim sayfasında, tek oturum açma yapılandırması onay seçin ve ardından **tam**.</span><span class="sxs-lookup"><span data-stu-id="b0bad-164">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="b0bad-165">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="b0bad-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="b0bad-166">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="b0bad-166">Configure user provisioning</span></span>

<span data-ttu-id="b0bad-167">Azure AD kullanıcıların Cisco Webex oturum etkinleştirmek için bunların Cisco Webex sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b0bad-167">In order to enable Azure AD users to log into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="b0bad-168">Cisco Webex söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="b0bad-168">In the case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="b0bad-169">**Kullanıcı hesaplarını sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b0bad-169">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="b0bad-170">Oturum, **Cisco Webex** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="b0bad-170">Log in to your **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="b0bad-171">Git **kullanıcıları yönetme \> kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="b0bad-171">Go to **Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="b0bad-172">![Kullanıcıları ekleme](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="b0bad-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="b0bad-173">Kullanıcı Ekle bölüm üzerinde aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b0bad-173">On the Add User section, perform the following steps:</span></span>
   
   <span data-ttu-id="b0bad-174">![Kullanıcı Ekle](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Kullanıcı Ekle")</span><span class="sxs-lookup"><span data-stu-id="b0bad-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="b0bad-175">Olarak **hesap türü**seçin **konak**.</span><span class="sxs-lookup"><span data-stu-id="b0bad-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="b0bad-176">Varolan bir Azure AD kullanıcı bilgilerinin aşağıdaki metin kutularına yazın: **ad, Soyadı**, **kullanıcı adı**, **e-posta**, **parola**, **parolayı onayla**.</span><span class="sxs-lookup"><span data-stu-id="b0bad-176">Type the information of an existing Azure AD user into the following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="b0bad-177">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b0bad-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="b0bad-178">API sağlama AAD kullanıcı hesaplarına Cisco Webex tarafından sağlanan veya herhangi diğer Cisco Webex kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0bad-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="b0bad-179">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="b0bad-179">Assign users</span></span>
<span data-ttu-id="b0bad-180">Yapılandırmanızı test etmek için uygulama erişimi atayarak kullanarak izin vermek istediğiniz Azure AD kullanıcılarının vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0bad-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="b0bad-181">**Cisco Webex kullanıcılara atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b0bad-181">**To assign users to Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="b0bad-182">Klasik Azure portalında bir test hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b0bad-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="b0bad-183">Üzerinde **Cisco Webex** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.</span><span class="sxs-lookup"><span data-stu-id="b0bad-183">On the **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="b0bad-184">![Kullanıcılar atama](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "kullanıcı atama")</span><span class="sxs-lookup"><span data-stu-id="b0bad-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="b0bad-185">Test kullanıcınız seçin, **atamak**ve ardından **Evet** , atama onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="b0bad-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="b0bad-186">![Evet](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Evet")</span><span class="sxs-lookup"><span data-stu-id="b0bad-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="b0bad-187">Çoklu oturum açma ayarlarınızı test etmek isterseniz, erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="b0bad-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="b0bad-188">Erişim paneli hakkında daha fazla ayrıntı için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b0bad-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

