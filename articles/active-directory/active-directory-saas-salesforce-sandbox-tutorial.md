---
title: "Öğretici: Salesforce korumalı alan Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse Salesforce korumalı alan nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="82068-103">Öğretici: Azure Active Directory Tümleştirme ile Salesforce korumalı alan</span><span class="sxs-lookup"><span data-stu-id="82068-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="82068-104">Bu öğreticinin Hello hedefi tooshow hello tümleştirilmesi Azure ve Salesforce korumalı alan ' dir.</span><span class="sxs-lookup"><span data-stu-id="82068-104">hello objective of this tutorial is tooshow hello integration of Azure and Salesforce Sandbox.</span></span>  

>[!TIP]
><span data-ttu-id="82068-105">Geri bildirim için bkz: Merhaba [Azure destek sayfası](http://go.microsoft.com/fwlink/?LinkId=521878).</span><span class="sxs-lookup"><span data-stu-id="82068-105">For feedback, see hello [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span></span> 
> 

<span data-ttu-id="82068-106">Kuruluşunuz çeşitli geliştirme gibi amaçlar için farklı ortamlarda birden çok kopyasını özelliği toocreate sınama ve eğitim aşılmasını hello veri ve uygulamaları, Salesforce üretimde olmadan hello sanal verin Kuruluş.</span><span class="sxs-lookup"><span data-stu-id="82068-106">Sandboxes give you hello ability toocreate multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising hello data and applications in your Salesforce production organization.</span></span>  

<span data-ttu-id="82068-107">Daha fazla ayrıntı için bkz: [korumalı alan genel bakış](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span><span class="sxs-lookup"><span data-stu-id="82068-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span></span>

<span data-ttu-id="82068-108">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="82068-108">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="82068-109">Geçerli bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="82068-109">A valid Azure subscription</span></span>
* <span data-ttu-id="82068-110">Bir korumalı alan Salesforce.com'da</span><span class="sxs-lookup"><span data-stu-id="82068-110">A sandbox in Salesforce.com</span></span>

<span data-ttu-id="82068-111">Geçerli bir korumalı alan Salesforce.com'da henüz yoksa, toocontact Salesforce gerekir.</span><span class="sxs-lookup"><span data-stu-id="82068-111">If you don’t have a valid sandbox in Salesforce.com yet, you need toocontact Salesforce.</span></span>

<span data-ttu-id="82068-112">Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:</span><span class="sxs-lookup"><span data-stu-id="82068-112">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="82068-113">Salesforce korumalı alan için etkinleştirme hello uygulama tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="82068-113">Enabling hello application integration for Salesforce Sandbox</span></span>
2. <span data-ttu-id="82068-114">Çoklu oturum açma (SSO) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="82068-114">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="82068-115">Etki alanınızı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="82068-115">Enabling your domain</span></span>
4. <span data-ttu-id="82068-116">Kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="82068-116">Configuring user provisioning</span></span>
5. <span data-ttu-id="82068-117">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="82068-117">Assigning users</span></span>

<span data-ttu-id="82068-118">![Senaryo](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "senaryosu")</span><span class="sxs-lookup"><span data-stu-id="82068-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a><span data-ttu-id="82068-119">Salesforce korumalı alan için Hello uygulama tümleştirmeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="82068-119">Enable hello application integration for Salesforce Sandbox</span></span>
<span data-ttu-id="82068-120">Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi Salesforce korumalı alan için.</span><span class="sxs-lookup"><span data-stu-id="82068-120">hello objective of this section is toooutline how tooenable hello application integration for Salesforce sandbox.</span></span>

<span data-ttu-id="82068-121">**Salesforce korumalı alan için tooenable hello uygulama tümleştirmesi hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="82068-121">**tooenable hello application integration for Salesforce sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="82068-122">Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="82068-122">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="82068-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="82068-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="82068-124">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="82068-124">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="82068-125">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="82068-125">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="82068-126">![Uygulamaları](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="82068-126">![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="82068-127">tooopen hello **uygulama Galerisi**, tıklatın **uygulama Ekle**ve ardından **my kuruluş toouse için uygulama ekleme**.</span><span class="sxs-lookup"><span data-stu-id="82068-127">tooopen hello **Application Gallery**, click **Add An App**, and then click **Add an application for my organization toouse**.</span></span>
   
   <span data-ttu-id="82068-128">![Neler toodo istiyorsunuz? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Neler toodo istiyorsunuz?")</span><span class="sxs-lookup"><span data-stu-id="82068-128">![What do you want toodo?](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want toodo?")</span></span>
5. <span data-ttu-id="82068-129">Merhaba, **arama kutusu**, türü **Salesforce korumalı alan**.</span><span class="sxs-lookup"><span data-stu-id="82068-129">In hello **search box**, type **Salesforce Sandbox**.</span></span>
   
   <span data-ttu-id="82068-130">![Uygulama Galerisi](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "uygulama Galerisi")</span><span class="sxs-lookup"><span data-stu-id="82068-130">![Application Gallery](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span></span>
6. <span data-ttu-id="82068-131">Merhaba sonuçlar bölmesinde seçin **Salesforce korumalı alan**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="82068-131">In hello results pane, select **Salesforce Sandbox**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="82068-132">![Salesforce korumalı alan](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce korumalı alan")</span><span class="sxs-lookup"><span data-stu-id="82068-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span></span>
   
## <a name="configur-single-sign-on-sso"></a><span data-ttu-id="82068-133">Configur çoklu oturum açma (SSO)</span><span class="sxs-lookup"><span data-stu-id="82068-133">Configur single sign-on (SSO)</span></span>

<span data-ttu-id="82068-134">Bu bölümde Hello amacı nasıl tooenable kullanıcılar tooauthenticate tooSalesforce Federasyon kullanarak Azure AD'de hesabıyla hello SAML protokolünü temel toooutline ' dir.</span><span class="sxs-lookup"><span data-stu-id="82068-134">hello objective of this section is toooutline how tooenable users tooauthenticate tooSalesforce with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="82068-135">**tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="82068-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="82068-136">Merhaba hello üzerinde Klasik Azure portalı içinde **Salesforce korumalı alan** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **tek oturum yapılandırma üzerinde aktar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="82068-136">In hello Azure classic portal, on hello **Salesforce Sandbox** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="82068-137">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="82068-137">![Configure single sign-on](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="82068-138">Merhaba üzerinde **nasıl tooSalesforce Sandbox üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="82068-138">On hello **How would you like users toosign on tooSalesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="82068-139">![Salesforce korumalı alan](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce korumalı alan")</span><span class="sxs-lookup"><span data-stu-id="82068-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span></span>
3. <span data-ttu-id="82068-140">Merhaba üzerinde **uygulama URL'sini Yapılandır** sayfasında hello **oturum üzerinde URL'si** metin kutusuna, desen aşağıdaki hello kullanarak URL'nizi yazın `http://company.my.salesforce.com`ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="82068-140">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type your URL using hello following pattern `http://company.my.salesforce.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="82068-141">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="82068-141">![Configure App URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span></span>
4. <span data-ttu-id="82068-142">Zaten başka bir Salesforce korumalı alan örneği için çoklu oturum açmayı dizininizde yapılandırdıktan sonra hello yapılandırmanız da gerekir **tanımlayıcısı** toohave hello hello aynı değere **URL üzerinde oturum**.</span><span class="sxs-lookup"><span data-stu-id="82068-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure hello **Identifier** toohave hello same value as hello **Sign on URL**.</span></span> 
 * <span data-ttu-id="82068-143">Merhaba **tanımlayıcısı** alan hello denetleyerek bulunabilir **Göster Gelişmiş ayarları** hello onay kutusuna **uygulama URL'sini yapılandırın** hello iletişim sayfası.</span><span class="sxs-lookup"><span data-stu-id="82068-143">hello **Identifier** field can be found by checking hello **Show advanced settings** checkbox on hello **Configure App URL** page of hello dialog.</span></span>
5. <span data-ttu-id="82068-144">Merhaba üzerinde **çoklu oturum açma sırasında Salesforce korumalı alan yapılandırmak** sayfasında, **indirme sertifika**ve ardından hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="82068-144">On hello **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="82068-145">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="82068-145">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="82068-146">Farklı web tarayıcısı penceresinde, Salesforce korumalı alan yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="82068-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span></span>
7. <span data-ttu-id="82068-147">Hello içinde hello üst menüsünde **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="82068-147">In hello menu on hello top, click **Setup**.</span></span>
   
   <span data-ttu-id="82068-148">![Kurulum](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="82068-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span></span>
8. <span data-ttu-id="82068-149">Merhaba Gezinti hello sol taraftaki bölmede **güvenlik denetimleri**ve ardından **çoklu oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="82068-149">In hello navigation pane on hello left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="82068-150">![Çoklu oturum açma ayarları](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="82068-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span></span>
9. <span data-ttu-id="82068-151">Hello çoklu oturum açma ayarları bölümü, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="82068-151">On hello Single Sign-On Settings section, perform hello following steps:</span></span>
   
   <span data-ttu-id="82068-152">![Çoklu oturum açma ayarları](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="82068-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span></span>  
 1.  <span data-ttu-id="82068-153">Seçin **SAML etkin**.</span><span class="sxs-lookup"><span data-stu-id="82068-153">Select **SAML Enabled**.</span></span> 
 2.  <span data-ttu-id="82068-154">**Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="82068-154">Click **New**.</span></span>
10. <span data-ttu-id="82068-155">SAML çoklu oturum açma ayarları bölümü Hello üzerinde hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="82068-155">On hello SAML Single Sign-On Settings section, perform hello following steps:</span></span>
    
    <span data-ttu-id="82068-156">![SAML çoklu oturum açma ayarları](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML çoklu oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="82068-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span></span>  
 1. <span data-ttu-id="82068-157">Merhaba adı metin kutusuna hello yapılandırma hello adını yazın (örneğin: *SPSSOWAAD\_Test*).</span><span class="sxs-lookup"><span data-stu-id="82068-157">In hello Name textbox, type hello name of hello configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 
 2. <span data-ttu-id="82068-158">Merhaba hello üzerinde Klasik Azure portalı içinde **çoklu oturum açma sırasında Salesforce korumalı alan yapılandırmak** iletişim kutusu sayfası, kopyalama hello **veren URL'si** değer ve hello yapıştırma **veren**metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="82068-158">In hello Azure classic portal, on hello **Configure single sign-on at Salesforce Sandbox** dialogue page, copy hello **Issuer URL** value, and then paste it into hello **Issuer** textbox.</span></span>
 3. <span data-ttu-id="82068-159">Merhaba, **varlık kimliği** metin kutusuna, türü **https://test.salesforce.com** bu hello tooyour dizin eklediğiniz ilk Salesforce korumalı alan örneği ise.</span><span class="sxs-lookup"><span data-stu-id="82068-159">In hello **Entity Id** textbox, type **https://test.salesforce.com** if this is hello first Salesforce Sandbox instance that you are adding tooyour directory.</span></span> <span data-ttu-id="82068-160">Salesforce korumalı alan, sonra da hello için bir örneği zaten eklediyseniz **varlık kimliği** hello türü **oturum üzerinde URL'si**, şu biçimde olmalıdır:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="82068-160">If you have already added an instance of Salesforce Sandbox, then for hello **Entity ID** type in hello **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>   
 4. <span data-ttu-id="82068-161">Tıklatın **Gözat** tooupload hello sertifika indirilir.</span><span class="sxs-lookup"><span data-stu-id="82068-161">Click **Browse** tooupload hello downloaded certificate.</span></span>  
 5. <span data-ttu-id="82068-162">Olarak **SAML kimlik türü**seçin **onaylamayı içeren hello Federasyon kimliği hello kullanıcı nesnesinden**.</span><span class="sxs-lookup"><span data-stu-id="82068-162">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span> 
 6. <span data-ttu-id="82068-163">Olarak **SAML kimlik konumu**seçin **kimliktir hello NameIdentifier öğesinde hello konu deyimi**.</span><span class="sxs-lookup"><span data-stu-id="82068-163">As **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>
 7. <span data-ttu-id="82068-164">Merhaba hello üzerinde Klasik Azure portalı içinde **çoklu oturum açma sırasında Salesforce korumalı alan yapılandırmak** iletişim kutusu sayfası, kopyalama hello **uzaktan oturum açma URL'si** değer ve hello yapıştırma **kimlik sağlayıcısı Oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="82068-164">In hello Azure classic portal, on hello **Configure single sign-on at Salesforce Sandbox** dialogue page, copy hello **Remote Login URL** value, and then paste it into hello **Identity Provider Login URL** textbox.</span></span> 
 8. <span data-ttu-id="82068-165">SAML oturum kapatma SFDC desteklemez.</span><span class="sxs-lookup"><span data-stu-id="82068-165">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="82068-166">Geçici bir çözüm olarak Yapıştır 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' hello içine **kimlik sağlayıcısı oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="82068-166">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into hello **Identity Provider Logout URL** textbox.</span></span>
 9. <span data-ttu-id="82068-167">Olarak **hizmet sağlayıcısı tarafından başlatılan bağlama isteği**seçin **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="82068-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 
 10. <span data-ttu-id="82068-168">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="82068-168">Click **Save**.</span></span>
11. <span data-ttu-id="82068-169">Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="82068-169">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="82068-170">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="82068-170">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span></span>

## <a name="enable-your-domain"></a><span data-ttu-id="82068-171">Etki alanınızı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="82068-171">Enable your domain</span></span>
<span data-ttu-id="82068-172">Bu bölümde, bir etki alanı zaten oluşturduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="82068-172">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="82068-173">Daha fazla ayrıntı için bkz: [etki alanı adınız tanımlama](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="82068-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="82068-174">**tooenable etki alanınızı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="82068-174">**tooenable your domain, perform hello following steps:**</span></span>

1. <span data-ttu-id="82068-175">Merhaba sol gezinti bölmesinde **etki alanı yönetimi**ve ardından **My etki alanı.**</span><span class="sxs-lookup"><span data-stu-id="82068-175">In hello left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
   <span data-ttu-id="82068-176">![Etki alanım](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "etki alanım")</span><span class="sxs-lookup"><span data-stu-id="82068-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="82068-177">Lütfen etki alanınızı doğru yapılandırılmış olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="82068-177">Please make sure that your domain has been configured correctly.</span></span> 
   > 
2. <span data-ttu-id="82068-178">Merhaba, **oturum açma sayfası ayarları** 'yi tıklatın **Düzenle**, sonra **kimlik doğrulama hizmeti**seçin hello önceki gelen oturum açma SAML tek ayar hello hello adı bölümünde ve son olarak tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="82068-178">In hello **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select hello name of hello SAML Single Sign-On Setting from hello previous section, and finally click **Save**.</span></span>
   
   <span data-ttu-id="82068-179">![Etki alanım](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "etki alanım")</span><span class="sxs-lookup"><span data-stu-id="82068-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span></span>

<span data-ttu-id="82068-180">Yapılandırılmış bir etki alanınız hemen kullanıcılarınızın hello etki alanı URL'si toologin toohello Salesforce korumalı alan kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="82068-180">As soon as you have a domain configured, your users should use hello domain URL toologin toohello Salesforce sandbox.</span></span>  

<span data-ttu-id="82068-181">Merhaba URL tooget hello değeri hello önceki bölümde oluşturduğunuz hello SSO profil'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="82068-181">tooget hello value of hello URL, click hello SSO profile you have created in hello previous section.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="82068-182">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="82068-182">Configure user provisioning</span></span>
<span data-ttu-id="82068-183">Bu bölümde Hello amacı olan toooutline nasıl tooenable Active Directory kullanıcısı kullanıcı sağlamayı tooSalesforce korumalı alan hesapları.</span><span class="sxs-lookup"><span data-stu-id="82068-183">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooSalesforce Sandbox.</span></span>

<span data-ttu-id="82068-184">**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="82068-184">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="82068-185">Merhaba üst gezinti çubuğundaki hello Salesforce portalında kullanıcı menünüze adı tooexpand seçin:</span><span class="sxs-lookup"><span data-stu-id="82068-185">In hello Salesforce portal, in hello top navigation bar, select your name tooexpand your user menu:</span></span>
   
   <span data-ttu-id="82068-186">![Ayarlarımı](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "ayarlarım")</span><span class="sxs-lookup"><span data-stu-id="82068-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span></span>
2. <span data-ttu-id="82068-187">Kullanıcı menüsünden seçin **My ayarları** tooopen, **My ayarları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="82068-187">From your user menu, select **My Settings** tooopen your **My Settings** page.</span></span>
3. <span data-ttu-id="82068-188">Merhaba sol bölmede **kişisel** tooexpand kişisel bölüm hello ve ardından **sıfırlama My güvenlik belirteci**:</span><span class="sxs-lookup"><span data-stu-id="82068-188">In hello left pane, click **Personal** tooexpand hello Personal section, and then click **Reset My Security Token**:</span></span>
   
   <span data-ttu-id="82068-189">![Ayarlarımı](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "ayarlarım")</span><span class="sxs-lookup"><span data-stu-id="82068-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span></span>
4. <span data-ttu-id="82068-190">Merhaba üzerinde **sıfırlama My güvenlik belirteci** sayfasında, **güvenlik belirteci sıfırlama** toorequest Salesforce.com güvenlik belirteci içeren bir e-posta.</span><span class="sxs-lookup"><span data-stu-id="82068-190">On hello **Reset My Security Token** page, click **Reset Security Token** toorequest an email that contains your Salesforce.com security token.</span></span>
   
   <span data-ttu-id="82068-191">![Yeni bir belirteç](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "yeni belirteci")</span><span class="sxs-lookup"><span data-stu-id="82068-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span></span>
5. <span data-ttu-id="82068-192">Bir e-posta ile Salesforce.com için e-posta kutunuzu kontrol edin "**salesforce.com.com güvenlik onaylama**" konu olarak.</span><span class="sxs-lookup"><span data-stu-id="82068-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span></span>
6. <span data-ttu-id="82068-193">Bu e-posta ve kopyalama hello güvenlik belirteci değerini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="82068-193">Review this email and copy hello security token value.</span></span>
7. <span data-ttu-id="82068-194">Merhaba hello üzerinde Klasik Azure portalı içinde **salesforce korumalı alan** uygulama tümleştirme sayfası, tıklatın **kullanıcı sağlamayı Yapılandır** tooopen hello **yapılandırma kullanıcı sağlamayı**iletişim.</span><span class="sxs-lookup"><span data-stu-id="82068-194">In hello Azure classic portal, on hello **salesforce Sandbox** application integration page, click **Configure user provisioning** tooopen hello **Configure User Provisioning** dialog.</span></span>
   
   <span data-ttu-id="82068-195">![Kullanıcı sağlamayı Yapılandır](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "kullanıcı sağlamayı Yapılandır")</span><span class="sxs-lookup"><span data-stu-id="82068-195">![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span></span>
8. <span data-ttu-id="82068-196">Merhaba üzerinde **, Salesforce korumalı alan kimlik bilgileri tooenable otomatik kullanıcı sağlamayı girin** sayfasında, yapılandırma ayarlarını aşağıdaki hello sağlayın:</span><span class="sxs-lookup"><span data-stu-id="82068-196">On hello **Enter your Salesforce Sandbox credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
   <span data-ttu-id="82068-197">![Salesforce korumalı alan](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce korumalı alan")</span><span class="sxs-lookup"><span data-stu-id="82068-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span></span>   
 1. <span data-ttu-id="82068-198">Merhaba, **Salesforce korumalı alan yönetici kullanıcı adı** metin kutusuna, Salesforce korumalı alan hesap hello sahip adı türü **Sistem Yöneticisi** atanan Salesforce.com profilinde.</span><span class="sxs-lookup"><span data-stu-id="82068-198">In hello **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has hello **System Administrator** profile in Salesforce.com assigned.</span></span>
 2. <span data-ttu-id="82068-199">Merhaba, **Salesforce korumalı alan yönetici parolası** metin kutusuna, bu hesap için hello parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="82068-199">In hello **Salesforce Sandbox Admin Password** textbox, type hello password for this account.</span></span>
 3. <span data-ttu-id="82068-200">Merhaba, **kullanıcı güvenlik belirteci** metin kutusuna, Yapıştır hello güvenlik belirteci değeri.</span><span class="sxs-lookup"><span data-stu-id="82068-200">In hello **User Security Token** textbox, paste hello security token value.</span></span>
 4. <span data-ttu-id="82068-201">Tıklatın **doğrulama** tooverify yapılandırmanızı.</span><span class="sxs-lookup"><span data-stu-id="82068-201">Click **Validate** tooverify your configuration.</span></span>
 5. <span data-ttu-id="82068-202">Merhaba tıklatın **sonraki** düğmesini tooopen hello **onay** sayfası.</span><span class="sxs-lookup"><span data-stu-id="82068-202">Click hello **Next** button tooopen hello **Confirmation** page.</span></span>
9. <span data-ttu-id="82068-203">Merhaba üzerinde **onay** sayfasında, **tam** toosave yapılandırmanızı.</span><span class="sxs-lookup"><span data-stu-id="82068-203">On hello **Confirmation** page, click **Complete** toosave your configuration.</span></span>
   
## <a name="assigning-users"></a><span data-ttu-id="82068-204">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="82068-204">Assigning users</span></span>

<span data-ttu-id="82068-205">tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.</span><span class="sxs-lookup"><span data-stu-id="82068-205">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="82068-206">**tooassign kullanıcılar tooSalesforce korumalı alan, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="82068-206">**tooassign users tooSalesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="82068-207">Hello Klasik Azure portalı, bir test hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82068-207">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="82068-208">Hello üzerinde ** Salesforce korumalı alan ** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.</span><span class="sxs-lookup"><span data-stu-id="82068-208">On hello **Salesforce Sandbox **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="82068-209">![Kullanıcılar atama](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "kullanıcı atama")</span><span class="sxs-lookup"><span data-stu-id="82068-209">![Assign users](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span></span>
3. <span data-ttu-id="82068-210">Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.</span><span class="sxs-lookup"><span data-stu-id="82068-210">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="82068-211">![Evet](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Evet")</span><span class="sxs-lookup"><span data-stu-id="82068-211">![Yes](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="82068-212">Şimdi 10 dakika bekleyin ve hello hesap eşitlenmiş tooSalesforce korumalı alan olduğunu doğrulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="82068-212">You should now wait for 10 minutes and verify that hello account has been synchronized tooSalesforce Sandbox.</span></span>

<span data-ttu-id="82068-213">SSO ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="82068-213">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="82068-214">Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="82068-214">For more details about hello Access Panel, see [Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

