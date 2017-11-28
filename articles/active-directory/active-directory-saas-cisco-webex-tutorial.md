---
title: "Öğretici: Azure Active Directory Tümleştirme ile Cisco Webex | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse Cisco Webex nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
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
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="23443-103">Öğretici: Cisco Webex Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="23443-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="23443-104">Merhaba amacı Bu öğretici, Azure ve Cisco Webex tooshow hello tümleştirme ' dir.</span><span class="sxs-lookup"><span data-stu-id="23443-104">hello objective of this tutorial is tooshow hello integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="23443-105">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="23443-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="23443-106">Geçerli bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="23443-106">A valid Azure subscription</span></span>
* <span data-ttu-id="23443-107">Cisco Webex Kiracı</span><span class="sxs-lookup"><span data-stu-id="23443-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="23443-108">Bu öğreticiyi tamamladıktan sonra Azure AD kullanıcılarının atamış Webex olacaktır tooCisco mümkün toosingle oturum hello uygulamasına, Cisco Webex şirket sitenizdeki (servis sağlayıcı tarafından başlatılan oturum açma) hello veya hello kullanarak [giriş toohello Erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="23443-108">After completing this tutorial, hello Azure AD users you have assigned tooCisco Webex will be able toosingle sign into hello application at your Cisco Webex company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="23443-109">Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:</span><span class="sxs-lookup"><span data-stu-id="23443-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="23443-110">Merhaba uygulama tümleştirmesi Cisco Webex için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="23443-110">Enabling hello application integration for Cisco Webex</span></span>
* <span data-ttu-id="23443-111">Çoklu oturum açma (SSO) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="23443-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="23443-112">Kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="23443-112">Configuring user provisioning</span></span>
* <span data-ttu-id="23443-113">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="23443-113">Assigning users</span></span>

<span data-ttu-id="23443-114">![Senaryo](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "senaryosu")</span><span class="sxs-lookup"><span data-stu-id="23443-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-cisco-webex"></a><span data-ttu-id="23443-115">Cisco Webex için Hello uygulama tümleştirmeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="23443-115">Enable hello application integration for Cisco Webex</span></span>
<span data-ttu-id="23443-116">Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi Cisco Webex için.</span><span class="sxs-lookup"><span data-stu-id="23443-116">hello objective of this section is toooutline how tooenable hello application integration for Cisco Webex.</span></span>

<span data-ttu-id="23443-117">**Cisco Webex için tooenable hello uygulama tümleştirmesi hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="23443-117">**tooenable hello application integration for Cisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="23443-118">Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="23443-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="23443-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="23443-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="23443-120">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="23443-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="23443-121">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="23443-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="23443-122">![Uygulamaları](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="23443-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="23443-123">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="23443-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="23443-124">![Uygulama ekleme](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="23443-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="23443-125">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="23443-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="23443-126">![Galeriden bir uygulama eklemek](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Galeriden bir uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="23443-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="23443-127">Merhaba, **arama kutusu**, türü **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="23443-127">In hello **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="23443-128">![Uygulama Galerisi](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "uygulama Galerisi")</span><span class="sxs-lookup"><span data-stu-id="23443-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="23443-129">Merhaba sonuçlar bölmesinde seçin **Cisco Webex**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="23443-129">In hello results pane, select **Cisco Webex**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="23443-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="23443-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="23443-131">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="23443-131">Configure single sign-on</span></span>

<span data-ttu-id="23443-132">Bu bölümde Hello amacı nasıl hello SAML protokolünü kullanarak Federasyon Azure AD'de hesabıyla tooenable kullanıcılar tooauthenticate tooCisco Webex temel toooutline ' dir.</span><span class="sxs-lookup"><span data-stu-id="23443-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCisco Webex with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="23443-133">Bu yordam bir parçası, gerekli toocreate base-64 kodlanmış sertifika olur.</span><span class="sxs-lookup"><span data-stu-id="23443-133">As part of this procedure, you are required toocreate a base-64 encoded certificate.</span></span> <span data-ttu-id="23443-134">Bu yordama bilmiyorsanız bkz [nasıl tooconvert bir ikili sertifika bir metin dosyasına](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="23443-134">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="23443-135">**tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="23443-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="23443-136">Merhaba hello üzerinde Klasik Azure portalı içinde **Cisco Webex** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="23443-136">In hello Azure classic portal, on hello **Cisco Webex** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="23443-137">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="23443-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="23443-138">Merhaba üzerinde **nasıl kullanıcılar toosign tooCisco Webex üzerinde gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="23443-138">On hello **How would you like users toosign on tooCisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="23443-139">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="23443-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="23443-140">Merhaba üzerinde **uygulama URL'sini Yapılandır** sayfasında, aşağıdaki adımları hello gerçekleştirmek ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="23443-140">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="23443-141">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="23443-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="23443-142">Merhaba, **URL SING** metin kutusuna, Cisco Webex Kiracı URL'nizi yazın (örneğin: *http://contoso.webex.com*).</span><span class="sxs-lookup"><span data-stu-id="23443-142">In hello **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="23443-143">Merhaba, **Cisco Webex yanıt URL'si** metin kutusuna, türü, **Cisco Webex AssertionConsumerService URL** (örn: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).</span><span class="sxs-lookup"><span data-stu-id="23443-143">In hello **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="23443-144">Merhaba üzerinde **çoklu oturum açma sırasında Cisco Webex yapılandırma** sayfası, toodownload, sertifikanızı tıklatın **indirme sertifika**ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="23443-144">On hello **Configure single sign-on at Cisco Webex** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="23443-145">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="23443-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="23443-146">Farklı web tarayıcısı penceresinde Cisco Webex şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="23443-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="23443-147">Hello içinde hello üst menüsünde **Site Yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="23443-147">In hello menu on hello top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="23443-148">![Site Yönetimi](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Yönetimi")</span><span class="sxs-lookup"><span data-stu-id="23443-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="23443-149">Merhaba, **sitesi yönetme** 'yi tıklatın **SSO yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="23443-149">In hello **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="23443-150">![SSO yapılandırma](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO yapılandırma")</span><span class="sxs-lookup"><span data-stu-id="23443-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="23443-151">Hello Federe Web SSO yapılandırma bölümü, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="23443-151">In hello Federated Web SSO Configuration section, perform hello following steps:</span></span>
   
   <span data-ttu-id="23443-152">![SSO yapılandırma Federasyon](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federasyon SSO yapılandırma")</span><span class="sxs-lookup"><span data-stu-id="23443-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="23443-153">Merhaba gelen **Federasyon Protokolü** listesinde **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="23443-153">From hello **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="23443-154">Oluşturma bir **Base-64 kodlanmış** indirilen sertifikanızı dosyasından.</span><span class="sxs-lookup"><span data-stu-id="23443-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="23443-155">Daha fazla ayrıntı için bkz: [nasıl tooconvert bir ikili sertifika bir metin dosyasına](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="23443-155">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="23443-156">Base-64 kodlanmış sertifikanızı not defteri sonra bunu içerik kopyalama hello açın.</span><span class="sxs-lookup"><span data-stu-id="23443-156">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   4. <span data-ttu-id="23443-157">Tıklatın **SAML meta verileri içeri aktarma**ve ardından, base-64 kodlanmış sertifika yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="23443-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="23443-158">Hello hello üzerinde Klasik Azure portalı içinde **çoklu oturum açma sırasında Cisco Webex yapılandırma** iletişim sayfası, kopyalama hello **veren URL'si** değer ve hello yapıştırma **SAML (IDP kimliği)veren** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="23443-158">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Issuer URL** value, and then paste it into hello **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="23443-159">Hello hello üzerinde Klasik Azure portalı içinde **çoklu oturum açma sırasında Cisco Webex yapılandırma** iletişim sayfası, kopyalama hello **uzaktan oturum açma URL'si** değer ve hello yapıştırma **müşteri SSO hizmeti oturum açma URL** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="23443-159">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Login URL** value, and then paste it into hello **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="23443-160">Merhaba gelen **NameID biçimi** listesinde **e-posta adresi**.</span><span class="sxs-lookup"><span data-stu-id="23443-160">From hello **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="23443-161">Merhaba, **AuthnContextClassRef** metin kutusuna, türü **urn: OASIS: adları: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="23443-161">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="23443-162">Hello hello üzerinde Klasik Azure portalı içinde **çoklu oturum açma sırasında Cisco Webex yapılandırma** iletişim sayfası, kopyalama hello **uzak oturum kapatma URL'si** değer ve hello yapıştırma **müşteri SSO hizmet oturum kapatma URL** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="23443-162">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Logout URL** value, and then paste it into hello **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="23443-163">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="23443-163">Click **Update**.</span></span>
9. <span data-ttu-id="23443-164">Merhaba hello üzerinde Klasik Azure portalı içinde **çoklu oturum açma sırasında Cisco Webex yapılandırma** iletişim sayfa hello tek oturum açma yapılandırması onay seçin ve ardından **tam**.</span><span class="sxs-lookup"><span data-stu-id="23443-164">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="23443-165">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="23443-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="23443-166">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="23443-166">Configure user provisioning</span></span>

<span data-ttu-id="23443-167">Cisco Webex içine sipariş tooenable Azure AD kullanıcıların toolog bunların Cisco Webex sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="23443-167">In order tooenable Azure AD users toolog into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="23443-168">Cisco Webex Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="23443-168">In hello case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="23443-169">**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**</span><span class="sxs-lookup"><span data-stu-id="23443-169">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="23443-170">İçinde tooyour oturum **Cisco Webex** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="23443-170">Log in tooyour **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="23443-171">Çok Git**kullanıcıları yönetme \> Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="23443-171">Go too**Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="23443-172">![Kullanıcıları ekleme](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="23443-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="23443-173">Hello kullanıcı ekle bölümü, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="23443-173">On hello Add User section, perform hello following steps:</span></span>
   
   <span data-ttu-id="23443-174">![Kullanıcı Ekle](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Kullanıcı Ekle")</span><span class="sxs-lookup"><span data-stu-id="23443-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="23443-175">Olarak **hesap türü**seçin **konak**.</span><span class="sxs-lookup"><span data-stu-id="23443-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="23443-176">Metin kutuları aşağıdaki hello var olan bir Azure AD kullanıcısının hello bilgilerini yazın: **ad, Soyadı**, **kullanıcı adı**, **e-posta**, **parola**, **Parolayı onaylayın**.</span><span class="sxs-lookup"><span data-stu-id="23443-176">Type hello information of an existing Azure AD user into hello following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="23443-177">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="23443-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="23443-178">API AAD kullanıcı hesapları Cisco Webex tooprovision tarafından sağlanan veya herhangi diğer Cisco Webex kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23443-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="23443-179">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="23443-179">Assign users</span></span>
<span data-ttu-id="23443-180">tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.</span><span class="sxs-lookup"><span data-stu-id="23443-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="23443-181">**tooassign kullanıcılar tooCisco Webex, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="23443-181">**tooassign users tooCisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="23443-182">Hello Klasik Azure portalı, bir test hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="23443-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="23443-183">Hello üzerinde **Cisco Webex** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.</span><span class="sxs-lookup"><span data-stu-id="23443-183">On hello **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="23443-184">![Kullanıcılar atama](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "kullanıcı atama")</span><span class="sxs-lookup"><span data-stu-id="23443-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="23443-185">Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.</span><span class="sxs-lookup"><span data-stu-id="23443-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="23443-186">![Evet](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Evet")</span><span class="sxs-lookup"><span data-stu-id="23443-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="23443-187">Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="23443-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="23443-188">Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="23443-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

