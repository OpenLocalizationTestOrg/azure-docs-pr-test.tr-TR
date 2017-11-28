---
title: "Öğretici: Azure Active Directory Tümleştirme ile Coupa | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse Coupa nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
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
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="3e866-103">Öğretici: Azure Active Directory Tümleştirme Coupa ile</span><span class="sxs-lookup"><span data-stu-id="3e866-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="3e866-104">Merhaba amacı Bu öğretici, Azure ve Coupa tooshow hello tümleştirme ' dir.</span><span class="sxs-lookup"><span data-stu-id="3e866-104">hello objective of this tutorial is tooshow hello integration of Azure and Coupa.</span></span>  
<span data-ttu-id="3e866-105">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="3e866-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="3e866-106">Geçerli bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="3e866-106">A valid Azure subscription</span></span>
* <span data-ttu-id="3e866-107">Bir Coupa çoklu oturum açma (SSO) abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="3e866-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="3e866-108">Bu öğreticiyi tamamladıktan sonra tooCoupa atamış hello Azure AD kullanıcıların mümkün toosingle oturum hello kullanarak hello uygulamaya olacaktır [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3e866-108">After completing this tutorial, hello Azure AD users you have assigned tooCoupa will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="3e866-109">Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:</span><span class="sxs-lookup"><span data-stu-id="3e866-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="3e866-110">Merhaba uygulama tümleştirmesi Coupa için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="3e866-110">Enabling hello application integration for Coupa</span></span>
* <span data-ttu-id="3e866-111">Çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3e866-111">Configuring single sign-on</span></span>
* <span data-ttu-id="3e866-112">Kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="3e866-112">Configuring user provisioning</span></span>
* <span data-ttu-id="3e866-113">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="3e866-113">Assigning users</span></span>

<span data-ttu-id="3e866-114">![Senaryo](./media/active-directory-saas-coupa-tutorial/IC791897.png "senaryosu")</span><span class="sxs-lookup"><span data-stu-id="3e866-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-coupa"></a><span data-ttu-id="3e866-115">Merhaba uygulama tümleştirmesi Coupa için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="3e866-115">Enable hello application integration for Coupa</span></span>
<span data-ttu-id="3e866-116">Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi Coupa için.</span><span class="sxs-lookup"><span data-stu-id="3e866-116">hello objective of this section is toooutline how tooenable hello application integration for Coupa.</span></span>

<span data-ttu-id="3e866-117">**tooenable hello uygulama tümleştirmesi Coupa için hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3e866-117">**tooenable hello application integration for Coupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e866-118">Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3e866-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="3e866-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="3e866-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="3e866-120">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="3e866-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="3e866-121">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="3e866-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="3e866-122">![Uygulamaları](./media/active-directory-saas-coupa-tutorial/IC700994.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="3e866-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="3e866-123">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="3e866-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="3e866-124">![Uygulama ekleme](./media/active-directory-saas-coupa-tutorial/IC749321.png "uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="3e866-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="3e866-125">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="3e866-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="3e866-126">![Galeriden bir uygulama eklemek](./media/active-directory-saas-coupa-tutorial/IC749322.png "Galeriden bir uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="3e866-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="3e866-127">Merhaba, **arama kutusu**, türü **Coupa**.</span><span class="sxs-lookup"><span data-stu-id="3e866-127">In hello **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="3e866-128">![Uygulama Galerisi](./media/active-directory-saas-coupa-tutorial/IC791898.png "uygulama Galerisi")</span><span class="sxs-lookup"><span data-stu-id="3e866-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="3e866-129">Merhaba sonuçlar bölmesinde seçin **Coupa**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="3e866-129">In hello results pane, select **Coupa**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="3e866-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="3e866-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="3e866-131">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="3e866-131">Configure single sign-on</span></span>

<span data-ttu-id="3e866-132">Bu bölümde Hello amacı nasıl tooenable kullanıcılar tooauthenticate tooCoupa Federasyon kullanarak Azure AD'de hesabıyla hello SAML protokolünü temel toooutline ' dir.</span><span class="sxs-lookup"><span data-stu-id="3e866-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCoupa with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="3e866-133">Coupa için çoklu oturum açmayı yapılandırma tooretrieve bir sertifika parmak izi değerinden gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3e866-133">Configuring single sign-on for Coupa requires you tooretrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="3e866-134">Bu yordama bilmiyorsanız bkz [nasıl tooretrieve bir sertifikanın parmak izi değeri](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="3e866-134">If you are not familiar with this procedure, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="3e866-135">**tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3e866-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e866-136">Üzerinde tooyour Coupa şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3e866-136">Sign on tooyour Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="3e866-137">Çok Git**Kurulum \> güvenlik denetimi**.</span><span class="sxs-lookup"><span data-stu-id="3e866-137">Go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="3e866-138">![Güvenlik denetimleri](./media/active-directory-saas-coupa-tutorial/IC791900.png "güvenlik denetimleri")</span><span class="sxs-lookup"><span data-stu-id="3e866-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="3e866-139">toodownload hello Coupa meta veri dosyası tooyour bilgisayar, **indirin ve SP meta veri içe**.</span><span class="sxs-lookup"><span data-stu-id="3e866-139">toodownload hello Coupa metadata file tooyour computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="3e866-140">![Coupa SP meta veri](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP meta verileri")</span><span class="sxs-lookup"><span data-stu-id="3e866-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="3e866-141">Farklı bir tarayıcı penceresinde toohello Klasik Azure portalı üzerinde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3e866-141">In a different browser window, sign on toohello Azure classic portal.</span></span>
5. <span data-ttu-id="3e866-142">Merhaba üzerinde **Coupa** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3e866-142">On hello **Coupa** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="3e866-143">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-coupa-tutorial/IC791902.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="3e866-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="3e866-144">Merhaba üzerinde **nasıl tooCoupa üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="3e866-144">On hello **How would you like users toosign on tooCoupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="3e866-145">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-coupa-tutorial/IC791903.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="3e866-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="3e866-146">Merhaba üzerinde **uygulama URL'sini Yapılandır** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3e866-146">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="3e866-147">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-coupa-tutorial/IC791904.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="3e866-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="3e866-148">Merhaba, **oturum üzerinde URL'si** metin kutusuna, tooyour Coupa uygulama üzerinde kullanıcıların toosign tarafından kullanılan türü URL'si (örn: "*http://company.Coupa.com*").</span><span class="sxs-lookup"><span data-stu-id="3e866-148">In hello **Sign On URL** textbox, type URL used by your users toosign on tooyour Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="3e866-149">İndirilen Coupa meta veri dosyanızı açın ve ardından hello kopyalayın **AssertionConsumerService dizin/URL**.</span><span class="sxs-lookup"><span data-stu-id="3e866-149">Open your downloaded Coupa metadata file, and then copy hello **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="3e866-150">Merhaba, **Coupa yanıt URL'si** metin kutusuna, Yapıştır hello **AssertionConsumerService dizin/URL** değeri.</span><span class="sxs-lookup"><span data-stu-id="3e866-150">In hello **Coupa Reply URL** textbox, paste hello **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="3e866-151">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3e866-151">Click **Next**.</span></span>
8. <span data-ttu-id="3e866-152">Merhaba üzerinde **çoklu oturum açma sırasında Coupa yapılandırma** sayfası, toodownload, meta veri dosyası tıklatın **karşıdan meta veri**ve yerel olarak bilgisayarınızda hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3e866-152">On hello **Configure single sign-on at Coupa** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
   
   <span data-ttu-id="3e866-153">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-coupa-tutorial/IC791905.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="3e866-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="3e866-154">Merhaba Coupa şirket sitesinde çok Git**Kurulum \> güvenlik denetimi**.</span><span class="sxs-lookup"><span data-stu-id="3e866-154">On hello Coupa company site, go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="3e866-155">![Güvenlik denetimleri](./media/active-directory-saas-coupa-tutorial/IC791900.png "güvenlik denetimleri")</span><span class="sxs-lookup"><span data-stu-id="3e866-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="3e866-156">Merhaba, **Coupa kimlik bilgilerini kullanarak oturum** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3e866-156">In hello **Log in using Coupa credentials** section, perform hello following steps:</span></span>  

   <span data-ttu-id="3e866-157">![Coupa kimlik bilgilerini kullanarak oturum](./media/active-directory-saas-coupa-tutorial/IC791906.png "Coupa kimlik bilgilerini kullanarak oturum açın")</span><span class="sxs-lookup"><span data-stu-id="3e866-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="3e866-158">Seçin **SAML kullanarak oturum**.</span><span class="sxs-lookup"><span data-stu-id="3e866-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="3e866-159">Tıklatın **Gözat** tooupload indirilen, Azure Active meta veri dosyası.</span><span class="sxs-lookup"><span data-stu-id="3e866-159">Click **Browse** tooupload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="3e866-160">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3e866-160">Click **Save**.</span></span>
11. <span data-ttu-id="3e866-161">Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3e866-161">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="3e866-162">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-coupa-tutorial/IC791907.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="3e866-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="3e866-163">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="3e866-163">Configure user provisioning</span></span>

<span data-ttu-id="3e866-164">Coupa içine sipariş tooenable Azure AD kullanıcıların toolog bunların Coupa sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3e866-164">In order tooenable Azure AD users toolog into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="3e866-165">Coupa Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="3e866-165">In hello case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="3e866-166">**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3e866-166">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e866-167">İçinde tooyour oturum **Coupa** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="3e866-167">Log in tooyour **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="3e866-168">Hello içinde hello üst menüsünde **Kurulum**ve ardından **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="3e866-168">In hello menu on hello top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="3e866-169">![Kullanıcıların](./media/active-directory-saas-coupa-tutorial/IC791908.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="3e866-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="3e866-170">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3e866-170">Click **Create**.</span></span>
   
   <span data-ttu-id="3e866-171">![Kullanıcılar oluşturma](./media/active-directory-saas-coupa-tutorial/IC791909.png "kullanıcıları oluşturun")</span><span class="sxs-lookup"><span data-stu-id="3e866-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="3e866-172">Merhaba, **kullanıcı oluşturma** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3e866-172">In hello **User Create** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="3e866-173">![Kullanıcı ayrıntılarını](./media/active-directory-saas-coupa-tutorial/IC791910.png "kullanıcı ayrıntıları")</span><span class="sxs-lookup"><span data-stu-id="3e866-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="3e866-174">Türü hello **oturum açma**, **ad**, **Soyadı**, **tek oturum açma kimliği**, **e-posta** özniteliklerini bir Geçerli Azure Active Directory hesabı hello tooprovision istediğiniz metin kutuları ilgili.</span><span class="sxs-lookup"><span data-stu-id="3e866-174">Type hello **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="3e866-175">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3e866-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="3e866-176">etkin duruma gelmesi hello Azure Active Directory hesap sahibi bağlantı tooconfirm hello hesabı olan bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="3e866-176">hello Azure Active Directory account holder will get an email with a link tooconfirm hello account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="3e866-177">API AAD kullanıcı hesaplarının Coupa tooprovision tarafından sağlanan veya herhangi diğer Coupa kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e866-177">You can use any other Coupa user account creation tools or APIs provided by Coupa tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="3e866-178">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="3e866-178">Assign users</span></span>
<span data-ttu-id="3e866-179">tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e866-179">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="3e866-180">**tooassign kullanıcılar tooCoupa hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3e866-180">**tooassign users tooCoupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e866-181">Hello Klasik Azure portalı, bir test hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3e866-181">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="3e866-182">Hello üzerinde ** Coupa ** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.</span><span class="sxs-lookup"><span data-stu-id="3e866-182">On hello **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="3e866-183">![Kullanıcılar atama](./media/active-directory-saas-coupa-tutorial/IC791911.png "kullanıcı atama")</span><span class="sxs-lookup"><span data-stu-id="3e866-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="3e866-184">Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.</span><span class="sxs-lookup"><span data-stu-id="3e866-184">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="3e866-185">![Evet](./media/active-directory-saas-coupa-tutorial/IC767830.png "Evet")</span><span class="sxs-lookup"><span data-stu-id="3e866-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="3e866-186">Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="3e866-186">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="3e866-187">Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3e866-187">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

