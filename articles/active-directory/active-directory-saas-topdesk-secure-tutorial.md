---
title: "Öğretici: Azure Active Directory Tümleştirme TOPdesk - güvenli ile | Microsoft Docs"
description: "TOPdesk - kullanmayı öğrenin Azure çoklu oturum açma, otomatik sağlama ve daha fazlasını sağlamak için Active Directory'ye ile güvenli!."
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
ms.openlocfilehash: 28f0542dbe87bb34c83a7852db7c3a9fef055ce9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="773db-103">Öğretici: Azure Active Directory Tümleştirme TOPdesk - güvenli ile</span><span class="sxs-lookup"><span data-stu-id="773db-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="773db-104">Bu öğreticinin amacı, Azure ve TOPdesk - güvenli tümleştirmesini göstermektir.</span><span class="sxs-lookup"><span data-stu-id="773db-104">The objective of this tutorial is to show the integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="773db-105">Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="773db-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="773db-106">Geçerli bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="773db-106">A valid Azure subscription</span></span>
* <span data-ttu-id="773db-107">TOPdesk - bir abonelik etkin güvenli çoklu oturum açma</span><span class="sxs-lookup"><span data-stu-id="773db-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="773db-108">Bu öğreticiyi tamamladıktan sonra Azure AD kullanıcıları için TOPdesk - güvenli atamış tek oturum açın, TOPdesk - güvenli şirket site (servis sağlayıcı tarafından başlatılan oturum açma) veya kullanarak uygulamayı yapabilirsiniz [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="773db-108">After completing this tutorial, the Azure AD users you have assigned to TOPdesk - Secure will be able to single sign into the application at your TOPdesk - Secure company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="773db-109">Bu öğreticide gösterilen senaryo, aşağıdaki yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="773db-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="773db-110">Uygulama tümleştirmesi TOPdesk - güvenli için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="773db-110">Enabling the application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="773db-111">Çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="773db-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="773db-112">Kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="773db-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="773db-113">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="773db-113">Assigning users</span></span>

<span data-ttu-id="773db-114">![Senaryo](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "senaryosu")</span><span class="sxs-lookup"><span data-stu-id="773db-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-topdesk---secure"></a><span data-ttu-id="773db-115">Uygulama tümleştirmesi TOPdesk - güvenli için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="773db-115">Enabling the application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="773db-116">Bu bölümün amacı TOPdesk - güvenli için uygulama tümleştirme sağlamak üzere nasıl anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="773db-116">The objective of this section is to outline how to enable the application integration for TOPdesk - Secure.</span></span>

### <a name="to-enable-the-application-integration-for-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="773db-117">TOPdesk - uygulama tümleştirmesini etkinleştirmek için güvenli, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="773db-117">To enable the application integration for TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="773db-118">Azure Klasik portalında, sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="773db-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="773db-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="773db-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="773db-120">Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="773db-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="773db-121">Dizin görünümünde uygulamaları görünümü açmak için **uygulamaları** üst menüde.</span><span class="sxs-lookup"><span data-stu-id="773db-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="773db-122">![Uygulamaları](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="773db-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="773db-123">Tıklatın **Ekle** sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="773db-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="773db-124">![Uygulama ekleme](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="773db-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="773db-125">Üzerinde **ne yapmak istiyorsunuz** iletişim kutusunda, tıklatın **Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="773db-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="773db-126">![Galeriden bir uygulama eklemek](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Galeriden bir uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="773db-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="773db-127">İçinde **arama kutusu**, türü **TOPdesk - güvenli**.</span><span class="sxs-lookup"><span data-stu-id="773db-127">In the **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="773db-128">![Uygulama Galerisi](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "uygulama Galerisi")</span><span class="sxs-lookup"><span data-stu-id="773db-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="773db-129">Sonuçlar bölmesinde seçin **TOPdesk - güvenli**ve ardından **tam** uygulama eklemek için.</span><span class="sxs-lookup"><span data-stu-id="773db-129">In the results pane, select **TOPdesk - Secure**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="773db-130">![TOPdesk - güvenli](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - güvenli")</span><span class="sxs-lookup"><span data-stu-id="773db-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="773db-131">Çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="773db-131">Configuring single sign-on</span></span>
<span data-ttu-id="773db-132">Bu bölümün amacı kullanıcıların TOPdesk için - kimlik doğrulaması sağlamak nasıl ana hatlarını belirlemek için olduğundan SAML protokolünü temel Federasyon kullanarak Azure AD ile kendi hesaplarını güvenli.</span><span class="sxs-lookup"><span data-stu-id="773db-132">The objective of this section is to outline how to enable users to authenticate to TOPdesk - Secure with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="773db-133">Yapılandırma tek oturum açma için TOPdesk - güvenli bir logo simgesini dosyayı karşıya yüklemeyi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="773db-133">Configuring single sign-on for TOPdesk - Secure requires you to upload a logo icon file.</span></span> <span data-ttu-id="773db-134">Simge dosyası almak için TOPdesk Destek ekibine başvurun.</span><span class="sxs-lookup"><span data-stu-id="773db-134">To get the icon file, contact the TOPdesk support team.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="773db-135">Çoklu oturum açma yapılandırmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="773db-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="773db-136">Oturum, **TOPdesk - güvenli** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="773db-136">Sign on to your **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="773db-137">İçinde **TOPdesk** menüsünde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="773db-137">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="773db-138">![Ayarları](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="773db-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="773db-139">Tıklatın **oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="773db-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="773db-140">![Oturum açma ayarları](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="773db-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="773db-141">Genişletme **oturum açma ayarları** menüsüne ve ardından **genel**.</span><span class="sxs-lookup"><span data-stu-id="773db-141">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="773db-142">![Genel](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "genel")</span><span class="sxs-lookup"><span data-stu-id="773db-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="773db-143">İçinde **güvenli** bölümünü **SAML oturum açma** yapılandırma bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="773db-143">In the **Secure** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="773db-144">![Teknik ayarları](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "teknik ayarları")</span><span class="sxs-lookup"><span data-stu-id="773db-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="773db-145">a.</span><span class="sxs-lookup"><span data-stu-id="773db-145">a.</span></span> <span data-ttu-id="773db-146">Tıklatın **karşıdan** ortak meta veri dosyası indirip bilgisayarınıza yerel olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="773db-146">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="773db-147">b.</span><span class="sxs-lookup"><span data-stu-id="773db-147">b.</span></span> <span data-ttu-id="773db-148">Meta veri dosyasını açın ve ardından bulun **AssertionConsumerService** düğümü.</span><span class="sxs-lookup"><span data-stu-id="773db-148">Open the metadata file, and then locate the **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="773db-149">![Onaylama işlemi tüketici hizmeti](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "onaylama tüketici hizmeti")</span><span class="sxs-lookup"><span data-stu-id="773db-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="773db-150">c.</span><span class="sxs-lookup"><span data-stu-id="773db-150">c.</span></span> <span data-ttu-id="773db-151">Kopya **AssertionConsumerService** değeri.</span><span class="sxs-lookup"><span data-stu-id="773db-151">Copy the **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="773db-152">Değer gerekir **uygulama URL'sini Yapılandır** Bu öğreticinin ilerleyen bölümlerinde.</span><span class="sxs-lookup"><span data-stu-id="773db-152">You will need the value in the **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="773db-153">Farklı web tarayıcısı penceresinde oturum açın, **Klasik Azure portalı** yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="773db-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="773db-154">Üzerinde **TOPdesk - güvenli** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma yapılandırma** açmak için ** tek oturum yapılandırma üzerinde Aktar ** iletişim.</span><span class="sxs-lookup"><span data-stu-id="773db-154">On the **TOPdesk - Secure** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="773db-155">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="773db-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="773db-156">Üzerinde **için TOPdesk - güvenli oturum açmasını nasıl istiyorsunuz** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="773db-156">On the **How would you like users to sign on to TOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="773db-157">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="773db-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="773db-158">Üzerinde **uygulama URL'sini Yapılandır** sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="773db-158">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="773db-159">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="773db-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="773db-160">a.</span><span class="sxs-lookup"><span data-stu-id="773db-160">a.</span></span> <span data-ttu-id="773db-161">İçinde **TOPdesk - URL üzerinde güvenli oturum** metin kutusuna, türü URL kullanılan kullanıcılarınız tarafından TOPdesk - güvenli uygulama imzalamak için (örn: "*https://qssolutions.topdesk.net*").</span><span class="sxs-lookup"><span data-stu-id="773db-161">In the **TOPdesk - Secure Sign On URL** textbox, type the URL used by your users to sign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="773db-162">b.</span><span class="sxs-lookup"><span data-stu-id="773db-162">b.</span></span> <span data-ttu-id="773db-163">İçinde **TOPdesk – ortak yanıt URL'si** metin kutusuna, Yapıştır **TOPdesk - güvenli AssertionConsumerService URL** (örn: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span><span class="sxs-lookup"><span data-stu-id="773db-163">In the **TOPdesk – Public Reply URL** textbox, paste the **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="773db-164">c.</span><span class="sxs-lookup"><span data-stu-id="773db-164">c.</span></span> <span data-ttu-id="773db-165">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="773db-165">Click **Next**.</span></span>

10. <span data-ttu-id="773db-166">Üzerinde **çoklu oturum açma sırasında TOPdesk - güvenli yapılandırma** , meta veriler indirilemedi sayfasını tıklatın **karşıdan meta veri**ve ardından dosyayı bilgisayarınıza yerel olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="773db-166">On the **Configure single sign-on at TOPdesk - Secure** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
    
    <span data-ttu-id="773db-167">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="773db-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="773db-168">Bir sertifika dosyası oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="773db-168">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="773db-169">![Sertifika](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "sertifika")</span><span class="sxs-lookup"><span data-stu-id="773db-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="773db-170">a.</span><span class="sxs-lookup"><span data-stu-id="773db-170">a.</span></span> <span data-ttu-id="773db-171">İndirilen meta veri dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="773db-171">Open the downloaded metadata file.</span></span>
    <span data-ttu-id="773db-172">b.</span><span class="sxs-lookup"><span data-stu-id="773db-172">b.</span></span> <span data-ttu-id="773db-173">Genişletme **RoleDescriptor** sahip düğümü bir **xsi: type** , **ssas'nin: ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="773db-173">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="773db-174">c.</span><span class="sxs-lookup"><span data-stu-id="773db-174">c.</span></span> <span data-ttu-id="773db-175">Değerini kopyalayın **X509Certificate** düğümü.</span><span class="sxs-lookup"><span data-stu-id="773db-175">Copy the value of the **X509Certificate** node.</span></span>
    <span data-ttu-id="773db-176">d.</span><span class="sxs-lookup"><span data-stu-id="773db-176">d.</span></span> <span data-ttu-id="773db-177">Kopyalanan Kaydet **X509Certificate** yerel olarak bilgisayarınızda bir dosyada değeri.</span><span class="sxs-lookup"><span data-stu-id="773db-177">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="773db-178">Şirket site, TOPdesk üzerinde - güvenli **TOPdesk** menüsünde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="773db-178">On your TOPdesk - Secure company site, in the **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="773db-179">![Ayarları](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="773db-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="773db-180">Tıklatın **oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="773db-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="773db-181">![Oturum açma ayarları](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="773db-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="773db-182">Genişletme **oturum açma ayarları** menüsüne ve ardından **genel**.</span><span class="sxs-lookup"><span data-stu-id="773db-182">Expand the **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="773db-183">![Genel](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "genel")</span><span class="sxs-lookup"><span data-stu-id="773db-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="773db-184">İçinde **ortak** 'yi tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="773db-184">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="773db-185">![Ekleme](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "ekleme")</span><span class="sxs-lookup"><span data-stu-id="773db-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="773db-186">Üzerinde **SAML Yapılandırması Yardımcısı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="773db-186">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="773db-187">![SAML Yapılandırması Yardımcısı](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Yapılandırması Yardımcısı")</span><span class="sxs-lookup"><span data-stu-id="773db-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="773db-188">a.</span><span class="sxs-lookup"><span data-stu-id="773db-188">a.</span></span> <span data-ttu-id="773db-189">İndirilen meta veri dosyanızı altında karşıya yüklemek için **Federasyon meta verileri**, tıklatın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="773db-189">To upload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="773db-190">b.</span><span class="sxs-lookup"><span data-stu-id="773db-190">b.</span></span> <span data-ttu-id="773db-191">Sertifika dosyanızın altında karşıya yüklemek için **sertifika (RSA)**, tıklatın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="773db-191">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="773db-192">c.</span><span class="sxs-lookup"><span data-stu-id="773db-192">c.</span></span> <span data-ttu-id="773db-193">Aldığınız TOPdesk destek ekibinden altında logosu dosyayı karşıya yüklemeyi **Logo simgesini**, tıklatın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="773db-193">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="773db-194">d.</span><span class="sxs-lookup"><span data-stu-id="773db-194">d.</span></span> <span data-ttu-id="773db-195">İçinde **kullanıcı adı özniteliği** metin kutusuna, türü **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="773db-195">In the **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="773db-196">e.</span><span class="sxs-lookup"><span data-stu-id="773db-196">e.</span></span> <span data-ttu-id="773db-197">İçinde **görünen adı** metin kutusuna, yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="773db-197">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="773db-198">f.</span><span class="sxs-lookup"><span data-stu-id="773db-198">f.</span></span> <span data-ttu-id="773db-199">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="773db-199">Click **Save**.</span></span>

17. <span data-ttu-id="773db-200">Klasik Azure portalı, çoklu oturum açma yapılandırması onay seçin ve ardından **tam** kapatmak için **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="773db-200">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="773db-201">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="773db-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="773db-202">Kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="773db-202">Configuring user provisioning</span></span>
<span data-ttu-id="773db-203">Azure AD kullanıcıların TOPdesk - oturum etkinleştirmek için güvenli, bunların TOPdesk - güvenli sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="773db-203">In order to enable Azure AD users to log into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="773db-204">Söz konusu olduğunda TOPdesk - sağlama el ile bir görev güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="773db-204">In the case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="773db-205">Kullanıcı sağlamayı yapılandırmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="773db-205">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="773db-206">Oturum, **TOPdesk - güvenli** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="773db-206">Sign on to your **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="773db-207">Üstteki menüde tıklatın **TOPdesk \> yeni \> destek dosyalarını \> işleci**.</span><span class="sxs-lookup"><span data-stu-id="773db-207">In the menu on the top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="773db-208">![İşleç](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "işleci")</span><span class="sxs-lookup"><span data-stu-id="773db-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="773db-209">Üzerinde **New işleci** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="773db-209">On the **New Operator** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="773db-210">![New işleci](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New işleci")</span><span class="sxs-lookup"><span data-stu-id="773db-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="773db-211">a.</span><span class="sxs-lookup"><span data-stu-id="773db-211">a.</span></span> <span data-ttu-id="773db-212">Genel sekmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="773db-212">Click the General tab.</span></span>
   
    <span data-ttu-id="773db-213">b.</span><span class="sxs-lookup"><span data-stu-id="773db-213">b.</span></span> <span data-ttu-id="773db-214">İçinde **Soyadı** , metin kutusuna **genel** bölümünde, son sağlamak istediğiniz geçerli bir Azure Active Directory hesabının adını yazın.</span><span class="sxs-lookup"><span data-stu-id="773db-214">In the **Surname** textbox of the **General** section, type the last name of a valid Azure Active Directory account you want to provision.</span></span>
   
    <span data-ttu-id="773db-215">c.</span><span class="sxs-lookup"><span data-stu-id="773db-215">c.</span></span> <span data-ttu-id="773db-216">Seçin bir **Site** hesap için **konumu** bölümü.</span><span class="sxs-lookup"><span data-stu-id="773db-216">Select a **Site** for the account in the **Location** section.</span></span>
   
    <span data-ttu-id="773db-217">d.</span><span class="sxs-lookup"><span data-stu-id="773db-217">d.</span></span> <span data-ttu-id="773db-218">İçinde **oturum açma adı** , metin kutusuna **TOPdesk oturum açma** bölümünde, kullanıcı oturum açma adını yazın.</span><span class="sxs-lookup"><span data-stu-id="773db-218">In the **Login Name** textbox of the **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="773db-219">e.</span><span class="sxs-lookup"><span data-stu-id="773db-219">e.</span></span> <span data-ttu-id="773db-220">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="773db-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="773db-221">Tüm diğer TOPdesk - güvenli kullanıcı hesabı oluşturma araçlarını veya tarafından TOPdesk - AAD kullanıcı hesaplarını sağlamak için güvenli sağlanan API'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="773db-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="773db-222">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="773db-222">Assigning users</span></span>
<span data-ttu-id="773db-223">Yapılandırmanızı test etmek için uygulama erişimi atayarak kullanarak izin vermek istediğiniz Azure AD kullanıcılarının vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="773db-223">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="773db-224">Kullanıcılar için TOPdesk - atamak için güvenli, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="773db-224">To assign users to TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="773db-225">Klasik Azure portalında bir test hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="773db-225">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="773db-226">Üzerinde ** TOPdesk - güvenli ** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.</span><span class="sxs-lookup"><span data-stu-id="773db-226">On the **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="773db-227">![Kullanıcılar atama](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "kullanıcı atama")</span><span class="sxs-lookup"><span data-stu-id="773db-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="773db-228">Test kullanıcınız seçin, **atamak**ve ardından **Evet** , atama onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="773db-228">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="773db-229">![Evet](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Evet")</span><span class="sxs-lookup"><span data-stu-id="773db-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="773db-230">Çoklu oturum açma ayarlarınızı test etmek isterseniz, erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="773db-230">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="773db-231">Erişim paneli hakkında daha fazla ayrıntı için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="773db-231">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

