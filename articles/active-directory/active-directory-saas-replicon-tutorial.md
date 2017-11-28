---
title: "Öğretici: Azure Active Directory Tümleştirme ile Replicon | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse Replicon nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="2d6df-103">Öğretici: Azure Active Directory Tümleştirme Replicon ile</span><span class="sxs-lookup"><span data-stu-id="2d6df-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="2d6df-104">Merhaba amacı Bu öğretici, Azure ve Replicon tooshow hello tümleştirme ' dir.</span><span class="sxs-lookup"><span data-stu-id="2d6df-104">hello objective of this tutorial is tooshow hello integration of Azure and Replicon.</span></span> <span data-ttu-id="2d6df-105">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="2d6df-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="2d6df-106">Geçerli bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="2d6df-106">A valid Azure subscription</span></span>
* <span data-ttu-id="2d6df-107">Replicon Kiracı</span><span class="sxs-lookup"><span data-stu-id="2d6df-107">A Replicon tenant</span></span>

<span data-ttu-id="2d6df-108">Bu öğreticiyi tamamladıktan sonra tooReplicon atamış hello Azure AD kullanıcıların mümkün toosingle oturum Replicon şirket sitenizin (servis sağlayıcı tarafından başlatılan oturum açma) veya hello kullanarak hello uygulamaya olacaktır [giriş toohello erişim Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2d6df-108">After completing this tutorial, hello Azure AD users you have assigned tooReplicon will be able toosingle sign into hello application at your Replicon company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="2d6df-109">Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:</span><span class="sxs-lookup"><span data-stu-id="2d6df-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="2d6df-110">Merhaba uygulama tümleştirmesi Replicon için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="2d6df-110">Enabling hello application integration for Replicon</span></span>
2. <span data-ttu-id="2d6df-111">Çoklu oturum açma (SSO) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2d6df-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="2d6df-112">Kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="2d6df-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="2d6df-113">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="2d6df-113">Assigning users</span></span>

<span data-ttu-id="2d6df-114">![Senaryo](./media/active-directory-saas-replicon-tutorial/IC777798.png "senaryosu")</span><span class="sxs-lookup"><span data-stu-id="2d6df-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-replicon"></a><span data-ttu-id="2d6df-115">Merhaba uygulama tümleştirmesi Replicon için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="2d6df-115">Enable hello application integration for Replicon</span></span>
<span data-ttu-id="2d6df-116">Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi Replicon için.</span><span class="sxs-lookup"><span data-stu-id="2d6df-116">hello objective of this section is toooutline how tooenable hello application integration for Replicon.</span></span>

<span data-ttu-id="2d6df-117">**tooenable hello uygulama tümleştirmesi Replicon için hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2d6df-117">**tooenable hello application integration for Replicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d6df-118">Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2d6df-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="2d6df-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="2d6df-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="2d6df-120">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="2d6df-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="2d6df-121">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="2d6df-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="2d6df-122">![Uygulamaları](./media/active-directory-saas-replicon-tutorial/IC700994.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="2d6df-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="2d6df-123">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="2d6df-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="2d6df-124">![Uygulama ekleme](./media/active-directory-saas-replicon-tutorial/IC749321.png "uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="2d6df-124">![Add application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="2d6df-125">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="2d6df-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="2d6df-126">![Galeriden bir uygulama eklemek](./media/active-directory-saas-replicon-tutorial/IC749322.png "Galeriden bir uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="2d6df-126">![Add an application from gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="2d6df-127">Merhaba, **arama kutusu**, türü **Replicon**.</span><span class="sxs-lookup"><span data-stu-id="2d6df-127">In hello **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="2d6df-128">![Uygulama Galerisi](./media/active-directory-saas-replicon-tutorial/IC777799.png "uygulama Galerisi")</span><span class="sxs-lookup"><span data-stu-id="2d6df-128">![Application gallery](./media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="2d6df-129">Merhaba sonuçlar bölmesinde seçin **Replicon**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="2d6df-129">In hello results pane, select **Replicon**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="2d6df-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="2d6df-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="2d6df-131">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2d6df-131">Configure single sign-on</span></span>

<span data-ttu-id="2d6df-132">Bu bölümde Hello amacı nasıl tooenable kullanıcılar tooauthenticate tooReplicon Federasyon kullanarak Azure AD'de hesabıyla hello SAML protokolünü temel toooutline ' dir.</span><span class="sxs-lookup"><span data-stu-id="2d6df-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooReplicon with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="2d6df-133">**tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2d6df-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d6df-134">Merhaba hello üzerinde Klasik Azure portalı içinde **Replicon** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2d6df-134">In hello Azure classic portal, on hello **Replicon** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="2d6df-135">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-replicon-tutorial/IC777801.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="2d6df-135">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="2d6df-136">Merhaba üzerinde **nasıl tooReplicon üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2d6df-136">On hello **How would you like users toosign on tooReplicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="2d6df-137">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-replicon-tutorial/IC777802.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="2d6df-137">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="2d6df-138">Merhaba üzerinde **uygulama URL'sini Yapılandır** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2d6df-138">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="2d6df-139">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-replicon-tutorial/IC777803.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="2d6df-139">![Configure app URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="2d6df-140">Merhaba, **üzerinde Replicon oturum URL'si** metin kutusuna, Replicon Kiracı URL'nizi yazın (örneğin: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span><span class="sxs-lookup"><span data-stu-id="2d6df-140">In hello **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="2d6df-141">Merhaba, **Replicon yanıt URL'si** metin, Replicon yazın **AssertionConsumerService** URL'si (örn: *https://global.replicon.com/! / saml2/şirket/sso/post*).</span><span class="sxs-lookup"><span data-stu-id="2d6df-141">In hello **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="2d6df-142">Hello Replicon meta verilerden hello URL elde edebilirsiniz: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**.</span><span class="sxs-lookup"><span data-stu-id="2d6df-142">You can get hello URL from hello Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="2d6df-143">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2d6df-143">Click **Next**.</span></span>

4. <span data-ttu-id="2d6df-144">Hello üzerinde **çoklu oturum açma sırasında Replicon yapılandırmak** sayfası, toodownload meta verileriniz tıklatın **karşıdan meta veri**ve ardından hello meta verileri bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2d6df-144">On hello **Configure single sign-on at Replicon** page, toodownload your metadata, click **Download metadata**, and then save hello metadata on your computer.</span></span>
   
    <span data-ttu-id="2d6df-145">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-replicon-tutorial/IC777804.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="2d6df-145">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="2d6df-146">Farklı web tarayıcısı penceresinde Replicon şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2d6df-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="2d6df-147">SAML 2.0 tooconfigure hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2d6df-147">tooconfigure SAML 2.0, perform hello following steps:</span></span>
   
    <span data-ttu-id="2d6df-148">![SAML kimlik doğrulamasını etkinleştir](./media/active-directory-saas-replicon-tutorial/IC777805.png "etkinleştirmek SAML kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="2d6df-148">![Enable SAML authentication](./media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="2d6df-149">toodisplay hello **EnableSAML Authentication2** iletişim kutusunda, tooyour URL, şirket anahtarınızı sonra aşağıdaki hello ekleme: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="2d6df-149">toodisplay hello **EnableSAML Authentication2** dialog, append hello following tooyour URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="2d6df-150">Merhaba aşağıdaki hello tam URL hello şeması gösterir:</span><span class="sxs-lookup"><span data-stu-id="2d6df-150">hello following shows hello schema of hello complete URL:</span></span>  
   <span data-ttu-id="2d6df-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="2d6df-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>
   2. <span data-ttu-id="2d6df-152">Merhaba tıklatın  **+**  tooexpand hello **v20Configuration** bölümü.</span><span class="sxs-lookup"><span data-stu-id="2d6df-152">Click hello **+** tooexpand hello **v20Configuration** section.</span></span>
   3. <span data-ttu-id="2d6df-153">Merhaba tıklatın  **+**  tooexpand hello **metaDataConfiguration** bölümü.</span><span class="sxs-lookup"><span data-stu-id="2d6df-153">Click hello **+** tooexpand hello **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="2d6df-154">Tıklatın **Dosya Seç**, tooselect kimlik sağlayıcısı meta verileri XML dosyasını ve tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="2d6df-154">Click **Choose File**, tooselect your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="2d6df-155">Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2d6df-155">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="2d6df-156">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-replicon-tutorial/IC778418.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="2d6df-156">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="2d6df-157">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="2d6df-157">Configure user provisioning</span></span>

<span data-ttu-id="2d6df-158">Replicon içine sipariş tooenable Azure AD kullanıcıların toolog bunların Replicon sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2d6df-158">In order tooenable Azure AD users toolog into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="2d6df-159">Replicon Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="2d6df-159">In hello case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="2d6df-160">**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2d6df-160">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d6df-161">Bir web tarayıcısı penceresinde Replicon şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2d6df-161">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="2d6df-162">Çok Git**Yönetim \> kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2d6df-162">Go too**Administration \> Users**.</span></span>
   
    <span data-ttu-id="2d6df-163">![Kullanıcıların](./media/active-directory-saas-replicon-tutorial/IC777806.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="2d6df-163">![Users](./media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="2d6df-164">Tıklatın **+ kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="2d6df-164">Click **+Add User**.</span></span>
   
    <span data-ttu-id="2d6df-165">![Kullanıcı ekleme](./media/active-directory-saas-replicon-tutorial/IC777807.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="2d6df-165">![Add User](./media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="2d6df-166">Merhaba, **kullanıcı profili** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2d6df-166">In hello **User Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="2d6df-167">![Kullanıcı profili](./media/active-directory-saas-replicon-tutorial/IC777808.png "kullanıcı profili")</span><span class="sxs-lookup"><span data-stu-id="2d6df-167">![User profile](./media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="2d6df-168">Merhaba, **oturum açma adı** metin kutusuna, türü hello Azure AD e-posta adresini istediğiniz hello Azure AD kullanıcı tooprovision.</span><span class="sxs-lookup"><span data-stu-id="2d6df-168">In hello **Login Name** textbox, type hello Azure AD email address of hello Azure AD user you want tooprovision.</span></span>
  2. <span data-ttu-id="2d6df-169">Olarak **kimlik doğrulama türü**seçin **SSO**.</span><span class="sxs-lookup"><span data-stu-id="2d6df-169">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="2d6df-170">Merhaba, **departmanı** metin kutusuna, hello kullanıcının bölüm adını yazın.</span><span class="sxs-lookup"><span data-stu-id="2d6df-170">In hello **Department** textbox, type hello user’s department.</span></span>
  4. <span data-ttu-id="2d6df-171">Olarak **çalışan türü**seçin **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="2d6df-171">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="2d6df-172">Tıklatın **kullanıcı profili Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="2d6df-172">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="2d6df-173">API AAD kullanıcı hesaplarının Replicon tooprovision tarafından sağlanan veya herhangi diğer Replicon kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d6df-173">You can use any other Replicon user account creation tools or APIs provided by Replicon tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="2d6df-174">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="2d6df-174">Assign users</span></span>
<span data-ttu-id="2d6df-175">tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d6df-175">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="2d6df-176">**tooassign kullanıcılar tooReplicon hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2d6df-176">**tooassign users tooReplicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d6df-177">Hello Klasik Azure portalı, bir test hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2d6df-177">In hello Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="2d6df-178">Hello üzerinde **Replicon** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.</span><span class="sxs-lookup"><span data-stu-id="2d6df-178">On hello **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="2d6df-179">![Kullanıcılar atama](./media/active-directory-saas-replicon-tutorial/IC777809.png "kullanıcı atama")</span><span class="sxs-lookup"><span data-stu-id="2d6df-179">![Assign users](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="2d6df-180">Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.</span><span class="sxs-lookup"><span data-stu-id="2d6df-180">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="2d6df-181">![Evet](./media/active-directory-saas-replicon-tutorial/IC767830.png "Evet")</span><span class="sxs-lookup"><span data-stu-id="2d6df-181">![Yes](./media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="2d6df-182">Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="2d6df-182">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="2d6df-183">Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2d6df-183">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

