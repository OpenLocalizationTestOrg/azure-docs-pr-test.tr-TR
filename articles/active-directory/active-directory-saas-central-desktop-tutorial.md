---
title: "Öğretici: Azure Active Directory Tümleştirme Merkezi Masaüstü ile | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse Merkezi Masaüstü nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="44e66-103">Öğretici: Azure Active Directory Tümleştirme ile Merkezi Masaüstü</span><span class="sxs-lookup"><span data-stu-id="44e66-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="44e66-104">Merhaba amacı Bu öğretici, Azure ve Merkezi Masaüstü tooshow hello tümleştirme ' dir.</span><span class="sxs-lookup"><span data-stu-id="44e66-104">hello objective of this tutorial is tooshow hello integration of Azure and Central Desktop.</span></span> <span data-ttu-id="44e66-105">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="44e66-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="44e66-106">Geçerli bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="44e66-106">A valid Azure subscription</span></span>
* <span data-ttu-id="44e66-107">Merkezi bir masaüstü çoklu oturum açma etkin Abonelik / Merkezi Masaüstü Kiracı</span><span class="sxs-lookup"><span data-stu-id="44e66-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="44e66-108">Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:</span><span class="sxs-lookup"><span data-stu-id="44e66-108">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="44e66-109">Merhaba uygulama tümleştirmesi Merkezi Masaüstü için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="44e66-109">Enabling hello application integration for Central Desktop</span></span>
* <span data-ttu-id="44e66-110">Çoklu oturum açma (SSO) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="44e66-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="44e66-111">Kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="44e66-111">Configuring user provisioning</span></span>
* <span data-ttu-id="44e66-112">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="44e66-112">Assigning users</span></span>

<span data-ttu-id="44e66-113">![Senaryo](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "senaryosu")</span><span class="sxs-lookup"><span data-stu-id="44e66-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-central-desktop"></a><span data-ttu-id="44e66-114">Merhaba uygulama tümleştirmesi Merkezi Masaüstü için etkinleştirmek</span><span class="sxs-lookup"><span data-stu-id="44e66-114">Enable hello application integration for Central Desktop</span></span>
<span data-ttu-id="44e66-115">Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi Merkezi Masaüstü için.</span><span class="sxs-lookup"><span data-stu-id="44e66-115">hello objective of this section is toooutline how tooenable hello application integration for Central Desktop.</span></span>

<span data-ttu-id="44e66-116">**Merkezi Masaüstü tooenable hello uygulama tümleştirmesi hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="44e66-116">**tooenable hello application integration for Central Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="44e66-117">Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="44e66-117">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="44e66-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="44e66-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="44e66-119">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="44e66-119">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="44e66-120">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="44e66-120">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="44e66-121">![Uygulamaları](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="44e66-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="44e66-122">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="44e66-122">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="44e66-123">![Uygulama ekleme](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="44e66-123">![Add application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="44e66-124">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="44e66-124">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="44e66-125">![Galeriden bir uygulama eklemek](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Galeriden bir uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="44e66-125">![Add an application from gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="44e66-126">Merhaba, **arama kutusu**, türü **Merkezi Masaüstü**.</span><span class="sxs-lookup"><span data-stu-id="44e66-126">In hello **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="44e66-127">![Uygulama Galerisi](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "uygulama Galerisi")</span><span class="sxs-lookup"><span data-stu-id="44e66-127">![Application gallery](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="44e66-128">Merhaba sonuçlar bölmesinde seçin **Merkezi Masaüstü**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="44e66-128">In hello results pane, select **Central Desktop**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="44e66-129">![Merkezi Masaüstü](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Merkezi Masaüstü")</span><span class="sxs-lookup"><span data-stu-id="44e66-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="44e66-130">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="44e66-130">Configure single sign-on</span></span>

<span data-ttu-id="44e66-131">Bu bölümde Hello amacı nasıl hello SAML protokolünü kullanarak Federasyon Azure AD'de hesabıyla tooenable kullanıcılar tooauthenticate tooCentral Masaüstü temel toooutline ' dir.</span><span class="sxs-lookup"><span data-stu-id="44e66-131">hello objective of this section is toooutline how tooenable users tooauthenticate tooCentral Desktop with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="44e66-132">Bu yordam bir parçası, gerekli tooupload base-64 kodlanmış sertifika tooyour Merkezi Masaüstü Kiracı olur.</span><span class="sxs-lookup"><span data-stu-id="44e66-132">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour Central Desktop tenant.</span></span>  
<span data-ttu-id="44e66-133">Bu yordama bilmiyorsanız bkz [nasıl tooconvert bir ikili sertifika bir metin dosyasına](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="44e66-133">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="44e66-134">**tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="44e66-134">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="44e66-135">Merhaba hello üzerinde Klasik Azure portalı içinde **Merkezi Masaüstü** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello ** tek oturum yapılandırma üzerinde Aktar ** iletişim.</span><span class="sxs-lookup"><span data-stu-id="44e66-135">In hello Azure classic portal, on hello **Central Desktop** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
   <span data-ttu-id="44e66-136">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="44e66-136">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="44e66-137">Merhaba üzerinde **nasıl tooCentral Masaüstü üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="44e66-137">On hello **How would you like users toosign on tooCentral Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="44e66-138">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="44e66-138">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="44e66-139">Merhaba üzerinde **uygulama URL'sini Yapılandır** sayfasında, aşağıdaki adımları hello gerçekleştirmek ve ardından **sonraki**:</span><span class="sxs-lookup"><span data-stu-id="44e66-139">On hello **Configure App URL** page, perform hello following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="44e66-140">Merhaba, **Merkezi Masaüstü Oturum açma URL'si** metin kutusuna, Merkezi Masaüstü kiracınızın türü hello URL'si (örn: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="44e66-140">In hello **Central Desktop Sign In URL** textbox, type hello URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="44e66-141">Merkezi Masaüstü AssertionConsumerService URL'nizi Hello Merkezi Masaüstü yanıt URL'si metin kutusuna yazın (örneğin: https://contoso.centraldesktop.com/saml2-assertion.php).</span><span class="sxs-lookup"><span data-stu-id="44e66-141">In hello Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="44e66-142">Merhaba değer hello Merkezi Masaüstü meta verileri alabilir (örn: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="44e66-142">You can get hello value from hello central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="44e66-143">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="44e66-143">![Configure app URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="44e66-144">Merhaba üzerinde **çoklu oturum açma sırasında Merkezi Masaüstü yapılandırma** sayfası, toodownload, sertifikanızı tıklatın **indirme sertifika**ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="44e66-144">On hello **Configure single sign-on at Central Desktop** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
  <span data-ttu-id="44e66-145">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="44e66-145">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="44e66-146">İçinde tooyour oturum **Merkezi Masaüstü** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="44e66-146">Log in tooyour **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="44e66-147">Çok Git**ayarları**, tıklatın **Gelişmiş**ve ardından **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="44e66-147">Go too**Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="44e66-148">![Kurulum - Gelişmiş](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Kurulum - Gelişmiş")</span><span class="sxs-lookup"><span data-stu-id="44e66-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="44e66-149">Merhaba üzerinde **tek oturum açma ayarları** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="44e66-149">On hello **Single Sign On Settings** page, perform hello following steps:</span></span>
   
  <span data-ttu-id="44e66-150">![Çoklu oturum açma ayarları](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="44e66-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="44e66-151">Seçin **etkinleştir SAML v2 çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="44e66-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="44e66-152">Hello hello üzerinde Klasik Azure Portalı'nda **çoklu oturum açma sırasında Merkezi Masaüstü yapılandırma** sayfası, kopyalama hello **veren URL'si** değer ve hello yapıştırma **SSO URL** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="44e66-152">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Issuer URL** value, and then paste it into hello **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="44e66-153">Merhaba hello üzerinde Klasik Azure Portalı'nda **çoklu oturum açma sırasında Merkezi Masaüstü yapılandırma** sayfası, kopyalama hello **uzaktan oturum açma URL'si** değer ve hello yapıştırma **SSO oturum açma URL'si**metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="44e66-153">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Remote Login URL** value, and then paste it into hello **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="44e66-154">Merhaba hello üzerinde Klasik Azure Portalı'nda **çoklu oturum açma sırasında Merkezi Masaüstü yapılandırma** sayfası, kopyalama hello **tek Sign-Out hizmeti URL'si** değer ve hello yapıştırma **SSO oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="44e66-154">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="44e66-155">Merhaba, **ileti imzası doğrulama yöntemi** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="44e66-155">In hello **Message Signature Verification Method** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="44e66-156">![İleti imzası doğrulama yöntemi](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "ileti imzası doğrulama yöntemi")</span><span class="sxs-lookup"><span data-stu-id="44e66-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="44e66-157">Seçin **sertifika**.</span><span class="sxs-lookup"><span data-stu-id="44e66-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="44e66-158">Merhaba gelen **SSO sertifika** listesinde **RSH SHA256**.</span><span class="sxs-lookup"><span data-stu-id="44e66-158">From hello **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="44e66-159">İndirilen hello sertifikadan kopyalama hello hello metin dosyasının içeriğini bir metin dosyası oluşturun ve hello yapıştırın **SSO sertifika** alan.</span><span class="sxs-lookup"><span data-stu-id="44e66-159">Create a text file from hello downloaded certificate, copy hello content of hello text file, and then paste it into hello **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="44e66-160">Daha fazla ayrıntı için bkz: [nasıl tooconvert bir ikili sertifika bir metin dosyasına](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="44e66-160">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="44e66-161">Seçin **bir bağlantı tooyour SAMLv2 oturum açma sayfasını görüntülemek**.</span><span class="sxs-lookup"><span data-stu-id="44e66-161">Select **Display a link tooyour SAMLv2 login page**.</span></span>
9. <span data-ttu-id="44e66-162">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="44e66-162">Click **Update**.</span></span>
10. <span data-ttu-id="44e66-163">Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="44e66-163">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="44e66-164">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="44e66-164">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="44e66-165">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="44e66-165">Configure user provisioning</span></span>

<span data-ttu-id="44e66-166">AAD kullanıcılar toobe mümkün toosign için bunların sağlanan toohello Merkezi Masaüstü uygulaması olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="44e66-166">For AAD users toobe able toosign in, they must be provisioned toohello Central Desktop application.</span></span> <span data-ttu-id="44e66-167">Bu bölümde, nasıl Merkezi Masaüstü toocreate AAD kullanıcı hesapları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="44e66-167">This section describes how toocreate AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="44e66-168">**tooprovision kullanıcı hesapları tooCentral Masaüstü:**</span><span class="sxs-lookup"><span data-stu-id="44e66-168">**tooprovision user accounts tooCentral Desktop:**</span></span>
1. <span data-ttu-id="44e66-169">İçinde tooyour Merkezi Masaüstü Kiracı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="44e66-169">Log in tooyour Central Desktop tenant.</span></span>
2. <span data-ttu-id="44e66-170">Çok Git**kişiler \> iç üyeleri**.</span><span class="sxs-lookup"><span data-stu-id="44e66-170">Go too**People \> Internal Members**.</span></span>
3. <span data-ttu-id="44e66-171">Tıklatın **iç üye eklemek**.</span><span class="sxs-lookup"><span data-stu-id="44e66-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="44e66-172">![Kişiler](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "kişiler")</span><span class="sxs-lookup"><span data-stu-id="44e66-172">![People](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="44e66-173">Merhaba, **yeni üyeler e-posta adresi** metin kutusuna, tooprovision istediğiniz ve ardından bir AAD hesabıyla yazın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="44e66-173">In hello **Email Address of New Members** textbox, type an AAD account you want tooprovision, and then click **Next**.</span></span>
   
  <span data-ttu-id="44e66-174">![E-posta adreslerini yeni üyeler](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "e-posta adreslerini yeni üyeler")</span><span class="sxs-lookup"><span data-stu-id="44e66-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="44e66-175">Tıklatın **Ekle iç üyeleri**.</span><span class="sxs-lookup"><span data-stu-id="44e66-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="44e66-176">![İç üye ekleme](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "iç üye ekleme")</span><span class="sxs-lookup"><span data-stu-id="44e66-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="44e66-177">eklediğiniz hello kullanıcılar tooclick tooactivate hello hesabına ihtiyaç duydukları onay bağlantısı içeren bir e-posta alır.</span><span class="sxs-lookup"><span data-stu-id="44e66-177">hello users you have added will receive an email that includes a confirmation link they need tooclick tooactivate hello account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="44e66-178">API AAD kullanıcı hesaplarını Merkezi Masaüstü tooprovision tarafından sağlanan veya herhangi diğer Merkezi Masaüstü kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="44e66-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop tooprovision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="44e66-179">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="44e66-179">Assign users</span></span>
<span data-ttu-id="44e66-180">tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.</span><span class="sxs-lookup"><span data-stu-id="44e66-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="44e66-181">**tooassign kullanıcılar tooCentral Masaüstü hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="44e66-181">**tooassign users tooCentral Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="44e66-182">Hello Klasik Azure portalı, bir test hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="44e66-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="44e66-183">Hello üzerinde **Merkezi Masaüstü** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.</span><span class="sxs-lookup"><span data-stu-id="44e66-183">On hello **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="44e66-184">![Kullanıcılar atama](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "kullanıcı atama")</span><span class="sxs-lookup"><span data-stu-id="44e66-184">![Assign users](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="44e66-185">Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.</span><span class="sxs-lookup"><span data-stu-id="44e66-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="44e66-186">![Evet](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Evet")</span><span class="sxs-lookup"><span data-stu-id="44e66-186">![Yes](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="44e66-187">Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="44e66-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="44e66-188">Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="44e66-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

