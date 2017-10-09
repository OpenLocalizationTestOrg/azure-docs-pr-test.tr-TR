---
title: "Öğretici: Azure Active Directory Tümleştirme ile PagerDuty | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile PagerDuty arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c3cfbedac3bf075e2d8cd833d5de7ca0bc9468b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="5d198-103">Öğretici: Azure Active Directory Tümleştirme PagerDuty ile</span><span class="sxs-lookup"><span data-stu-id="5d198-103">Tutorial: Azure Active Directory integration with PagerDuty</span></span>

<span data-ttu-id="5d198-104">Bu öğreticide, bilgi nasıl toointegrate PagerDuty Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5d198-104">In this tutorial, you learn how toointegrate PagerDuty with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5d198-105">PagerDuty Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="5d198-105">Integrating PagerDuty with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5d198-106">Erişim tooPagerDuty sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5d198-106">You can control in Azure AD who has access tooPagerDuty</span></span>
- <span data-ttu-id="5d198-107">Kullanıcıların tooautomatically get açan tooPagerDuty (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5d198-107">You can enable your users tooautomatically get signed-on tooPagerDuty (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5d198-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="5d198-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5d198-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5d198-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d198-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5d198-110">Prerequisites</span></span>

<span data-ttu-id="5d198-111">tooconfigure PagerDuty ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5d198-111">tooconfigure Azure AD integration with PagerDuty, you need hello following items:</span></span>

- <span data-ttu-id="5d198-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="5d198-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5d198-113">Bir PagerDuty çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="5d198-113">A PagerDuty single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5d198-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="5d198-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5d198-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="5d198-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5d198-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="5d198-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5d198-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5d198-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5d198-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="5d198-118">Scenario description</span></span>
<span data-ttu-id="5d198-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="5d198-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5d198-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="5d198-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5d198-121">Merhaba Galerisi'nden PagerDuty ekleme</span><span class="sxs-lookup"><span data-stu-id="5d198-121">Adding PagerDuty from hello gallery</span></span>
2. <span data-ttu-id="5d198-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="5d198-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pagerduty-from-hello-gallery"></a><span data-ttu-id="5d198-123">Merhaba Galerisi'nden PagerDuty ekleme</span><span class="sxs-lookup"><span data-stu-id="5d198-123">Adding PagerDuty from hello gallery</span></span>
<span data-ttu-id="5d198-124">Azure AD'ye tooconfigure hello tümleştirme PagerDuty, tooadd PagerDuty hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="5d198-124">tooconfigure hello integration of PagerDuty into Azure AD, you need tooadd PagerDuty from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5d198-125">**tooadd PagerDuty hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5d198-125">**tooadd PagerDuty from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d198-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="5d198-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="5d198-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="5d198-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5d198-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5d198-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="5d198-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5d198-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="5d198-133">Merhaba arama kutusuna yazın **PagerDuty**seçin **PagerDuty** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="5d198-133">In hello search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5d198-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="5d198-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5d198-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı PagerDuty sınayın.</span><span class="sxs-lookup"><span data-stu-id="5d198-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5d198-137">Tek toowork'ın oturum açma hangi hello karşılık gelen PagerDuty içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="5d198-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PagerDuty is tooa user in Azure AD.</span></span> <span data-ttu-id="5d198-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı PagerDuty hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="5d198-138">In other words, a link relationship between an Azure AD user and hello related user in PagerDuty needs toobe established.</span></span>

<span data-ttu-id="5d198-139">Merhaba hello değeri PagerDuty içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="5d198-139">In PagerDuty, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5d198-140">tooconfigure ve PagerDuty ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5d198-140">tooconfigure and test Azure AD single sign-on with PagerDuty, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5d198-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="5d198-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5d198-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="5d198-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5d198-143">**[PagerDuty test kullanıcısı oluşturma](#create-a-pagerduty-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir PagerDuty içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="5d198-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - toohave a counterpart of Britta Simon in PagerDuty that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5d198-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="5d198-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5d198-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="5d198-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5d198-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5d198-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5d198-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma PagerDuty uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5d198-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PagerDuty application.</span></span>

<span data-ttu-id="5d198-148">**tooconfigure Azure AD çoklu oturum açma ile PagerDuty, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5d198-148">**tooconfigure Azure AD single sign-on with PagerDuty, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d198-149">Hello hello üzerinde Azure portal'ın **PagerDuty** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="5d198-149">In hello Azure portal, on hello **PagerDuty** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="5d198-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="5d198-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. <span data-ttu-id="5d198-153">Merhaba üzerinde **PagerDuty etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5d198-153">On hello **PagerDuty Domain and URLs** section, perform hello following steps:</span></span>

    ![PagerDuty etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    <span data-ttu-id="5d198-155">a.</span><span class="sxs-lookup"><span data-stu-id="5d198-155">a.</span></span> <span data-ttu-id="5d198-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="5d198-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    <span data-ttu-id="5d198-157">b.</span><span class="sxs-lookup"><span data-stu-id="5d198-157">b.</span></span> <span data-ttu-id="5d198-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="5d198-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5d198-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="5d198-159">These values are not real.</span></span> <span data-ttu-id="5d198-160">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="5d198-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5d198-161">Kişi [PagerDuty istemci destek ekibi](https://www.pagerduty.com/support/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="5d198-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) tooget these values.</span></span> 

4. <span data-ttu-id="5d198-162">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5d198-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. <span data-ttu-id="5d198-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5d198-164">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5d198-166">Merhaba üzerinde **PagerDuty yapılandırma** 'yi tıklatın **yapılandırma PagerDuty** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="5d198-166">On hello **PagerDuty Configuration** section, click **Configure PagerDuty** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5d198-167">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="5d198-167">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![PagerDuty yapılandırma](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. <span data-ttu-id="5d198-169">Farklı web tarayıcısı penceresinde Pagerduty şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5d198-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>

8. <span data-ttu-id="5d198-170">Hello içinde hello üst menüsünde **hesap ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="5d198-170">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="5d198-171">![Hesap ayarları](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "hesap ayarları")</span><span class="sxs-lookup"><span data-stu-id="5d198-171">![Account Settings](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Account Settings")</span></span>

9. <span data-ttu-id="5d198-172">Tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="5d198-172">Click **Single Sign-on**.</span></span>
   
    <span data-ttu-id="5d198-173">![Çoklu oturum açma](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="5d198-173">![Single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single sign-on")</span></span>

10. <span data-ttu-id="5d198-174">Merhaba üzerinde **etkinleştirmek çoklu oturum açma (SSO)** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5d198-174">On hello **Enable Single Sign-on (SSO)** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="5d198-175">![Çoklu oturum açmayı etkinleştir](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "çoklu oturum açmayı etkinleştir")</span><span class="sxs-lookup"><span data-stu-id="5d198-175">![Enable single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Enable single sign-on")</span></span>
   
    <span data-ttu-id="5d198-176">a.</span><span class="sxs-lookup"><span data-stu-id="5d198-176">a.</span></span> <span data-ttu-id="5d198-177">Not Defteri'nde, kopyalama hello panonuza bunu içerik Azure portalından indirdiğiniz, base-64 kodlanmış sertifikasını açın ve ardından toohello yapıştırın **X.509 sertifikası** metin kutusu</span><span class="sxs-lookup"><span data-stu-id="5d198-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>
  
    <span data-ttu-id="5d198-178">b.</span><span class="sxs-lookup"><span data-stu-id="5d198-178">b.</span></span> <span data-ttu-id="5d198-179">Merhaba, **oturum açma URL'si** metin kutusuna, Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="5d198-179">In hello **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="5d198-180">c.</span><span class="sxs-lookup"><span data-stu-id="5d198-180">c.</span></span> <span data-ttu-id="5d198-181">Merhaba, **oturum kapatma URL'si** metin kutusuna, Yapıştır **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="5d198-181">In hello **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="5d198-182">d.</span><span class="sxs-lookup"><span data-stu-id="5d198-182">d.</span></span> <span data-ttu-id="5d198-183">Seçin **tek oturum açma kapatma**.</span><span class="sxs-lookup"><span data-stu-id="5d198-183">Select **Turn on Single Sign-on**.</span></span>
 
    <span data-ttu-id="5d198-184">e.</span><span class="sxs-lookup"><span data-stu-id="5d198-184">e.</span></span> <span data-ttu-id="5d198-185">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="5d198-185">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="5d198-186">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="5d198-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5d198-187">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="5d198-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5d198-188">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5d198-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5d198-189">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5d198-189">Create an Azure AD test user</span></span>

<span data-ttu-id="5d198-190">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="5d198-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="5d198-192">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5d198-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d198-193">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="5d198-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5d198-195">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="5d198-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5d198-197">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="5d198-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5d198-199">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5d198-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5d198-201">a.</span><span class="sxs-lookup"><span data-stu-id="5d198-201">a.</span></span> <span data-ttu-id="5d198-202">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5d198-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5d198-203">b.</span><span class="sxs-lookup"><span data-stu-id="5d198-203">b.</span></span> <span data-ttu-id="5d198-204">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="5d198-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5d198-205">c.</span><span class="sxs-lookup"><span data-stu-id="5d198-205">c.</span></span> <span data-ttu-id="5d198-206">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="5d198-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5d198-207">d.</span><span class="sxs-lookup"><span data-stu-id="5d198-207">d.</span></span> <span data-ttu-id="5d198-208">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5d198-208">Click **Create**.</span></span>
 
### <a name="create-a-pagerduty-test-user"></a><span data-ttu-id="5d198-209">PagerDuty test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5d198-209">Create a PagerDuty test user</span></span>

<span data-ttu-id="5d198-210">tooenable Azure AD kullanıcıların toolog tooPagerDuty bunların PagerDuty sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5d198-210">tooenable Azure AD users toolog in tooPagerDuty, they must be provisioned into PagerDuty.</span></span>  
<span data-ttu-id="5d198-211">PagerDuty Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="5d198-211">In hello case of PagerDuty, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="5d198-212">API, kullanıcı hesaplarını Pagerduty tooprovision Azure Active Directory tarafından sağlanan veya herhangi diğer Pagerduty kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d198-212">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty tooprovision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="5d198-213">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5d198-213">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d198-214">İçinde tooyour oturum **Pagerduty** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="5d198-214">Log in tooyour **Pagerduty** tenant.</span></span>

2. <span data-ttu-id="5d198-215">Hello içinde hello üst menüsünde **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="5d198-215">In hello menu on hello top, click **Users**.</span></span>

3. <span data-ttu-id="5d198-216">Tıklatın **kullanıcıları eklemek**.</span><span class="sxs-lookup"><span data-stu-id="5d198-216">Click **Add Users**.</span></span>
   
    <span data-ttu-id="5d198-217">![Kullanıcıları ekleme](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="5d198-217">![Add Users](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Add Users")</span></span>

4.  <span data-ttu-id="5d198-218">Merhaba üzerinde **ekibinizin davet** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5d198-218">On hello **Invite your team** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="5d198-219">![Davet Et ekibinizin](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "ekibinizin davet et")</span><span class="sxs-lookup"><span data-stu-id="5d198-219">![Invite your team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team")</span></span>

    <span data-ttu-id="5d198-220">a.</span><span class="sxs-lookup"><span data-stu-id="5d198-220">a.</span></span> <span data-ttu-id="5d198-221">Türü hello **ilk ve son adı** gibi kullanıcının **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5d198-221">Type hello **First and Last Name** of user like **Britta Simon**.</span></span> 
   
    <span data-ttu-id="5d198-222">b.</span><span class="sxs-lookup"><span data-stu-id="5d198-222">b.</span></span> <span data-ttu-id="5d198-223">Girin **e-posta** kullanıcının adresi ister  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="5d198-223">Enter **Email** address of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="5d198-224">c.</span><span class="sxs-lookup"><span data-stu-id="5d198-224">c.</span></span> <span data-ttu-id="5d198-225">Tıklatın **Ekle**ve ardından **Gönder başvurulmasını**.</span><span class="sxs-lookup"><span data-stu-id="5d198-225">Click **Add**, and then click **Send Invites**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="5d198-226">Tüm eklenen kullanıcıların davet toocreate PagerDuty hesabı alır.</span><span class="sxs-lookup"><span data-stu-id="5d198-226">All added users will receive an invite toocreate a PagerDuty account.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5d198-227">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="5d198-227">Assign hello Azure AD test user</span></span>

<span data-ttu-id="5d198-228">Bu bölümde, erişim tooPagerDuty vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5d198-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPagerDuty.</span></span>

![Merhaba kullanıcı rolü atayın][200]

<span data-ttu-id="5d198-230">**tooassign Britta Simon tooPagerDuty hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5d198-230">**tooassign Britta Simon tooPagerDuty, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d198-231">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5d198-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="5d198-233">Merhaba uygulamalar listesinde **PagerDuty**.</span><span class="sxs-lookup"><span data-stu-id="5d198-233">In hello applications list, select **PagerDuty**.</span></span>

    ![Merhaba PagerDuty bağlantı hello uygulamalar listesinde](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. <span data-ttu-id="5d198-235">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="5d198-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="5d198-237">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5d198-237">Click **Add** button.</span></span> <span data-ttu-id="5d198-238">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5d198-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="5d198-240">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="5d198-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5d198-241">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5d198-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5d198-242">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5d198-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5d198-243">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="5d198-243">Test single sign-on</span></span>

<span data-ttu-id="5d198-244">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="5d198-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5d198-245">Tıkladığınızda hello PagerDuty hello erişim Panelyou parçasında otomatik olarak oturum açma tooyour PagerDuty uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5d198-245">When you click hello PagerDuty tile in hello Access Panelyou should get automatically signed-on tooyour PagerDuty application.</span></span>

<span data-ttu-id="5d198-246">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5d198-246">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5d198-247">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="5d198-247">Additional resources</span></span>

* [<span data-ttu-id="5d198-248">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="5d198-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5d198-249">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="5d198-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

