---
title: "Öğretici: Azure Active Directory Tümleştirme TOPdesk - güvenli ile | Microsoft Docs"
description: "Bilgi nasıl toouse TOPdesk - Azure Active Directory tooenable çoklu oturum açma, otomatik sağlama ve daha fazla ile güvenli!."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="dd45d-103">Öğretici: Azure Active Directory Tümleştirme TOPdesk - güvenli ile</span><span class="sxs-lookup"><span data-stu-id="dd45d-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="dd45d-104">Merhaba amacı Bu öğretici, Azure ve TOPdesk tooshow hello tümleştirme - güvenli.</span><span class="sxs-lookup"><span data-stu-id="dd45d-104">hello objective of this tutorial is tooshow hello integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="dd45d-105">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="dd45d-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="dd45d-106">Geçerli bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="dd45d-106">A valid Azure subscription</span></span>
* <span data-ttu-id="dd45d-107">TOPdesk - bir abonelik etkin güvenli çoklu oturum açma</span><span class="sxs-lookup"><span data-stu-id="dd45d-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="dd45d-108">Tamamladıktan sonra Bu öğreticide, Azure AD hello kullanıcılar güvenli olacak tooTOPdesk - atadığınız mümkün toosingle oturum hello uygulamaya TOPdesk - güvenli şirket site (servis sağlayıcı tarafından başlatılan oturum açma) konumunda olması ya da hello kullanarak [giriş Erişim paneli toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dd45d-108">After completing this tutorial, hello Azure AD users you have assigned tooTOPdesk - Secure will be able toosingle sign into hello application at your TOPdesk - Secure company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="dd45d-109">Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:</span><span class="sxs-lookup"><span data-stu-id="dd45d-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="dd45d-110">Merhaba uygulama tümleştirmesi TOPdesk - güvenli için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="dd45d-110">Enabling hello application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="dd45d-111">Çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dd45d-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="dd45d-112">Kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="dd45d-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="dd45d-113">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="dd45d-113">Assigning users</span></span>

<span data-ttu-id="dd45d-114">![Senaryo](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "senaryosu")</span><span class="sxs-lookup"><span data-stu-id="dd45d-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a><span data-ttu-id="dd45d-115">Merhaba uygulama tümleştirmesi TOPdesk - güvenli için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="dd45d-115">Enabling hello application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="dd45d-116">Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi TOPdesk - güvenli için.</span><span class="sxs-lookup"><span data-stu-id="dd45d-116">hello objective of this section is toooutline how tooenable hello application integration for TOPdesk - Secure.</span></span>

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="dd45d-117">tooenable hello uygulama tümleştirmesi TOPdesk - güvenli için hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dd45d-117">tooenable hello application integration for TOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="dd45d-118">Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dd45d-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="dd45d-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="dd45d-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="dd45d-120">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="dd45d-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="dd45d-121">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="dd45d-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="dd45d-122">![Uygulamaları](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="dd45d-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="dd45d-123">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="dd45d-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="dd45d-124">![Uygulama ekleme](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="dd45d-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="dd45d-125">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="dd45d-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="dd45d-126">![Galeriden bir uygulama eklemek](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Galeriden bir uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="dd45d-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="dd45d-127">Merhaba, **arama kutusu**, türü **TOPdesk - güvenli**.</span><span class="sxs-lookup"><span data-stu-id="dd45d-127">In hello **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="dd45d-128">![Uygulama Galerisi](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "uygulama Galerisi")</span><span class="sxs-lookup"><span data-stu-id="dd45d-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="dd45d-129">Merhaba sonuçlar bölmesinde seçin **TOPdesk - güvenli**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="dd45d-129">In hello results pane, select **TOPdesk - Secure**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="dd45d-130">![TOPdesk - güvenli](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - güvenli")</span><span class="sxs-lookup"><span data-stu-id="dd45d-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="dd45d-131">Çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dd45d-131">Configuring single sign-on</span></span>
<span data-ttu-id="dd45d-132">Bu bölümde Hello amacı olan toooutline nasıl tooenable kullanıcılar tooauthenticate tooTOPdesk - SAML Protokolü hello üzerinde temel Federasyon kullanarak Azure AD ile kendi hesaplarını güvenli.</span><span class="sxs-lookup"><span data-stu-id="dd45d-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooTOPdesk - Secure with their account in Azure AD using federation based on hello SAML protocol.</span></span>  
<span data-ttu-id="dd45d-133">Yapılandırma tek oturum açma için TOPdesk - güvenli tooupload bir logo simge dosyası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="dd45d-133">Configuring single sign-on for TOPdesk - Secure requires you tooupload a logo icon file.</span></span> <span data-ttu-id="dd45d-134">tooget hello simge dosyası, kişi hello TOPdesk destek ekibi.</span><span class="sxs-lookup"><span data-stu-id="dd45d-134">tooget hello icon file, contact hello TOPdesk support team.</span></span>

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a><span data-ttu-id="dd45d-135">tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dd45d-135">tooconfigure single sign-on, perform hello following steps:</span></span>
1. <span data-ttu-id="dd45d-136">Tooyour üzerinde oturum **TOPdesk - güvenli** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="dd45d-136">Sign on tooyour **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="dd45d-137">Merhaba, **TOPdesk** menüsünde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="dd45d-137">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="dd45d-138">![Ayarları](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="dd45d-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="dd45d-139">Tıklatın **oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="dd45d-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="dd45d-140">![Oturum açma ayarları](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="dd45d-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="dd45d-141">Merhaba genişletin **oturum açma ayarları** menüsüne ve ardından **genel**.</span><span class="sxs-lookup"><span data-stu-id="dd45d-141">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="dd45d-142">![Genel](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "genel")</span><span class="sxs-lookup"><span data-stu-id="dd45d-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="dd45d-143">Merhaba, **güvenli** hello bölümünü **SAML oturum açma** yapılandırma bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dd45d-143">In hello **Secure** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="dd45d-144">![Teknik ayarları](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "teknik ayarları")</span><span class="sxs-lookup"><span data-stu-id="dd45d-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="dd45d-145">a.</span><span class="sxs-lookup"><span data-stu-id="dd45d-145">a.</span></span> <span data-ttu-id="dd45d-146">Tıklatın **karşıdan** toodownload hello ortak meta veri dosyası ve bilgisayarınıza yerel olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="dd45d-146">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="dd45d-147">b.</span><span class="sxs-lookup"><span data-stu-id="dd45d-147">b.</span></span> <span data-ttu-id="dd45d-148">Merhaba meta veri dosyasını açın ve ardından hello bulun **AssertionConsumerService** düğümü.</span><span class="sxs-lookup"><span data-stu-id="dd45d-148">Open hello metadata file, and then locate hello **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="dd45d-149">![Onaylama işlemi tüketici hizmeti](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "onaylama tüketici hizmeti")</span><span class="sxs-lookup"><span data-stu-id="dd45d-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="dd45d-150">c.</span><span class="sxs-lookup"><span data-stu-id="dd45d-150">c.</span></span> <span data-ttu-id="dd45d-151">Kopya hello **AssertionConsumerService** değeri.</span><span class="sxs-lookup"><span data-stu-id="dd45d-151">Copy hello **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="dd45d-152">Merhaba değerinde hello **uygulama URL'sini Yapılandır** Bu öğreticinin ilerleyen bölümlerinde.</span><span class="sxs-lookup"><span data-stu-id="dd45d-152">You will need hello value in hello **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="dd45d-153">Farklı web tarayıcısı penceresinde oturum açın, **Klasik Azure portalı** yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="dd45d-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="dd45d-154">Merhaba üzerinde **TOPdesk - güvenli** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello ** tek oturum yapılandırma üzerinde Aktar ** iletişim.</span><span class="sxs-lookup"><span data-stu-id="dd45d-154">On hello **TOPdesk - Secure** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="dd45d-155">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dd45d-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="dd45d-156">Merhaba üzerinde **nasıl bölüştürüleceğini kullanıcılar toosign tooTOPdesk üzerinde-gibi güvenli** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dd45d-156">On hello **How would you like users toosign on tooTOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="dd45d-157">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dd45d-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="dd45d-158">Merhaba üzerinde **uygulama URL'sini Yapılandır** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dd45d-158">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="dd45d-159">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dd45d-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="dd45d-160">a.</span><span class="sxs-lookup"><span data-stu-id="dd45d-160">a.</span></span> <span data-ttu-id="dd45d-161">Merhaba, **TOPdesk - URL üzerinde güvenli oturum** metin kutusuna, TOPdesk - güvenli uygulama, kullanıcıların toosign tarafından kullanılan türü hello URL'si (örn: "*https://qssolutions.topdesk.net*").</span><span class="sxs-lookup"><span data-stu-id="dd45d-161">In hello **TOPdesk - Secure Sign On URL** textbox, type hello URL used by your users toosign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="dd45d-162">b.</span><span class="sxs-lookup"><span data-stu-id="dd45d-162">b.</span></span> <span data-ttu-id="dd45d-163">Merhaba, **TOPdesk – ortak yanıt URL'si** metin kutusuna, Yapıştır hello **TOPdesk - güvenli AssertionConsumerService URL** (örn: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span><span class="sxs-lookup"><span data-stu-id="dd45d-163">In hello **TOPdesk – Public Reply URL** textbox, paste hello **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="dd45d-164">c.</span><span class="sxs-lookup"><span data-stu-id="dd45d-164">c.</span></span> <span data-ttu-id="dd45d-165">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dd45d-165">Click **Next**.</span></span>

10. <span data-ttu-id="dd45d-166">Merhaba üzerinde **çoklu oturum açma sırasında TOPdesk - güvenli yapılandırma** sayfası, toodownload, meta veri dosyası tıklatın **karşıdan meta veri**ve yerel olarak bilgisayarınızda hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="dd45d-166">On hello **Configure single sign-on at TOPdesk - Secure** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
    
    <span data-ttu-id="dd45d-167">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dd45d-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="dd45d-168">bir sertifika dosyası toocreate hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dd45d-168">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="dd45d-169">![Sertifika](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "sertifika")</span><span class="sxs-lookup"><span data-stu-id="dd45d-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="dd45d-170">a.</span><span class="sxs-lookup"><span data-stu-id="dd45d-170">a.</span></span> <span data-ttu-id="dd45d-171">Açık hello indirilen meta veri dosyası.</span><span class="sxs-lookup"><span data-stu-id="dd45d-171">Open hello downloaded metadata file.</span></span>
    <span data-ttu-id="dd45d-172">b.</span><span class="sxs-lookup"><span data-stu-id="dd45d-172">b.</span></span> <span data-ttu-id="dd45d-173">Merhaba genişletin **RoleDescriptor** sahip düğümü bir **xsi: type** , **ssas'nin: ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="dd45d-173">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="dd45d-174">c.</span><span class="sxs-lookup"><span data-stu-id="dd45d-174">c.</span></span> <span data-ttu-id="dd45d-175">Merhaba Hello değerini kopyalayın **X509Certificate** düğümü.</span><span class="sxs-lookup"><span data-stu-id="dd45d-175">Copy hello value of hello **X509Certificate** node.</span></span>
    <span data-ttu-id="dd45d-176">d.</span><span class="sxs-lookup"><span data-stu-id="dd45d-176">d.</span></span> <span data-ttu-id="dd45d-177">Kopyalanan Kaydet hello **X509Certificate** yerel olarak bilgisayarınızda bir dosyada değeri.</span><span class="sxs-lookup"><span data-stu-id="dd45d-177">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="dd45d-178">Üzerinde TOPdesk - şirket sitede hello güvenli **TOPdesk** menüsünde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="dd45d-178">On your TOPdesk - Secure company site, in hello **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="dd45d-179">![Ayarları](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="dd45d-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="dd45d-180">Tıklatın **oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="dd45d-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="dd45d-181">![Oturum açma ayarları](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="dd45d-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="dd45d-182">Merhaba genişletin **oturum açma ayarları** menüsüne ve ardından **genel**.</span><span class="sxs-lookup"><span data-stu-id="dd45d-182">Expand hello **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="dd45d-183">![Genel](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "genel")</span><span class="sxs-lookup"><span data-stu-id="dd45d-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="dd45d-184">Merhaba, **ortak** 'yi tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="dd45d-184">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="dd45d-185">![Ekleme](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "ekleme")</span><span class="sxs-lookup"><span data-stu-id="dd45d-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="dd45d-186">Merhaba üzerinde **SAML Yapılandırması Yardımcısı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dd45d-186">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="dd45d-187">![SAML Yapılandırması Yardımcısı](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Yapılandırması Yardımcısı")</span><span class="sxs-lookup"><span data-stu-id="dd45d-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="dd45d-188">a.</span><span class="sxs-lookup"><span data-stu-id="dd45d-188">a.</span></span> <span data-ttu-id="dd45d-189">indirilen, meta veri dosyası, altında tooupload **Federasyon meta verileri**, tıklatın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="dd45d-189">tooupload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="dd45d-190">b.</span><span class="sxs-lookup"><span data-stu-id="dd45d-190">b.</span></span> <span data-ttu-id="dd45d-191">altında sertifikanızı dosya tooupload **sertifika (RSA)**, tıklatın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="dd45d-191">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="dd45d-192">c.</span><span class="sxs-lookup"><span data-stu-id="dd45d-192">c.</span></span> <span data-ttu-id="dd45d-193">aldığınız hello TOPdesk destek ekibinden altında tooupload hello logo dosyası **Logo simgesini**, tıklatın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="dd45d-193">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="dd45d-194">d.</span><span class="sxs-lookup"><span data-stu-id="dd45d-194">d.</span></span> <span data-ttu-id="dd45d-195">Merhaba, **kullanıcı adı özniteliği** metin kutusuna, türü **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="dd45d-195">In hello **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="dd45d-196">e.</span><span class="sxs-lookup"><span data-stu-id="dd45d-196">e.</span></span> <span data-ttu-id="dd45d-197">Merhaba, **görünen adı** metin kutusuna, yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="dd45d-197">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="dd45d-198">f.</span><span class="sxs-lookup"><span data-stu-id="dd45d-198">f.</span></span> <span data-ttu-id="dd45d-199">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dd45d-199">Click **Save**.</span></span>

17. <span data-ttu-id="dd45d-200">Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="dd45d-200">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="dd45d-201">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dd45d-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="dd45d-202">Kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="dd45d-202">Configuring user provisioning</span></span>
<span data-ttu-id="dd45d-203">Sipariş tooenable Azure AD kullanıcıların toolog TOPdesk - içine içinde güvenli, bunların TOPdesk - güvenli sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="dd45d-203">In order tooenable Azure AD users toolog into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="dd45d-204">Merhaba TOPdesk - durumda sağlama el ile bir görev güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="dd45d-204">In hello case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="dd45d-205">tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dd45d-205">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="dd45d-206">Tooyour üzerinde oturum **TOPdesk - güvenli** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="dd45d-206">Sign on tooyour **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="dd45d-207">Hello içinde hello üst menüsünde **TOPdesk \> yeni \> destek dosyalarını \> işleci**.</span><span class="sxs-lookup"><span data-stu-id="dd45d-207">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="dd45d-208">![İşleç](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "işleci")</span><span class="sxs-lookup"><span data-stu-id="dd45d-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="dd45d-209">Merhaba üzerinde **New işleci** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dd45d-209">On hello **New Operator** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="dd45d-210">![New işleci](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New işleci")</span><span class="sxs-lookup"><span data-stu-id="dd45d-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="dd45d-211">a.</span><span class="sxs-lookup"><span data-stu-id="dd45d-211">a.</span></span> <span data-ttu-id="dd45d-212">Merhaba Genel sekmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dd45d-212">Click hello General tab.</span></span>
   
    <span data-ttu-id="dd45d-213">b.</span><span class="sxs-lookup"><span data-stu-id="dd45d-213">b.</span></span> <span data-ttu-id="dd45d-214">Merhaba, **Soyadı** hello textbox **genel** bölümü, tür hello son adını tooprovision istediğiniz geçerli bir Azure Active Directory hesabı.</span><span class="sxs-lookup"><span data-stu-id="dd45d-214">In hello **Surname** textbox of hello **General** section, type hello last name of a valid Azure Active Directory account you want tooprovision.</span></span>
   
    <span data-ttu-id="dd45d-215">c.</span><span class="sxs-lookup"><span data-stu-id="dd45d-215">c.</span></span> <span data-ttu-id="dd45d-216">Seçin bir **Site** hello hello hesap için **konumu** bölümü.</span><span class="sxs-lookup"><span data-stu-id="dd45d-216">Select a **Site** for hello account in hello **Location** section.</span></span>
   
    <span data-ttu-id="dd45d-217">d.</span><span class="sxs-lookup"><span data-stu-id="dd45d-217">d.</span></span> <span data-ttu-id="dd45d-218">Merhaba, **oturum açma adı** hello textbox **TOPdesk oturum açma** bölümünde, kullanıcı oturum açma adını yazın.</span><span class="sxs-lookup"><span data-stu-id="dd45d-218">In hello **Login Name** textbox of hello **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="dd45d-219">e.</span><span class="sxs-lookup"><span data-stu-id="dd45d-219">e.</span></span> <span data-ttu-id="dd45d-220">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dd45d-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="dd45d-221">Tüm diğer TOPdesk - güvenli kullanıcı hesabı oluşturma araçlarını veya TOPdesk tarafından - API'lerinden güvenli tooprovision AAD kullanıcı hesaplarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd45d-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="dd45d-222">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="dd45d-222">Assigning users</span></span>
<span data-ttu-id="dd45d-223">tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd45d-223">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="dd45d-224">tooassign kullanıcılar tooTOPdesk - güvenli, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dd45d-224">tooassign users tooTOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="dd45d-225">Hello Klasik Azure portalı, bir test hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd45d-225">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="dd45d-226">Hello üzerinde ** TOPdesk - güvenli ** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.</span><span class="sxs-lookup"><span data-stu-id="dd45d-226">On hello **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="dd45d-227">![Kullanıcılar atama](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "kullanıcı atama")</span><span class="sxs-lookup"><span data-stu-id="dd45d-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="dd45d-228">Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.</span><span class="sxs-lookup"><span data-stu-id="dd45d-228">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="dd45d-229">![Evet](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Evet")</span><span class="sxs-lookup"><span data-stu-id="dd45d-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="dd45d-230">Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="dd45d-230">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="dd45d-231">Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dd45d-231">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

