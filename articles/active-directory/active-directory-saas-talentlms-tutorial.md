---
title: "Öğretici: Azure Active Directory Tümleştirme ile TalentLMS | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile TalentLMS arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 25538086602e58fbaab0fbf223f5b03908a74922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a><span data-ttu-id="65821-103">Öğretici: Azure Active Directory Tümleştirme TalentLMS ile</span><span class="sxs-lookup"><span data-stu-id="65821-103">Tutorial: Azure Active Directory integration with TalentLMS</span></span>

<span data-ttu-id="65821-104">Bu öğreticide, bilgi nasıl toointegrate TalentLMS Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="65821-104">In this tutorial, you learn how toointegrate TalentLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65821-105">TalentLMS Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="65821-105">Integrating TalentLMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="65821-106">Erişim tooTalentLMS sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="65821-106">You can control in Azure AD who has access tooTalentLMS</span></span>
- <span data-ttu-id="65821-107">Kullanıcıların tooautomatically get açan tooTalentLMS (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="65821-107">You can enable your users tooautomatically get signed-on tooTalentLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="65821-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="65821-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="65821-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65821-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65821-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="65821-110">Prerequisites</span></span>

<span data-ttu-id="65821-111">tooconfigure TalentLMS ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="65821-111">tooconfigure Azure AD integration with TalentLMS, you need hello following items:</span></span>

- <span data-ttu-id="65821-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="65821-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65821-113">Bir TalentLMS çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="65821-113">A TalentLMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65821-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="65821-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65821-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="65821-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65821-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="65821-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65821-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65821-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65821-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="65821-118">Scenario description</span></span>
<span data-ttu-id="65821-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="65821-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65821-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="65821-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65821-121">Merhaba Galerisi'nden TalentLMS ekleme</span><span class="sxs-lookup"><span data-stu-id="65821-121">Adding TalentLMS from hello gallery</span></span>
2. <span data-ttu-id="65821-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="65821-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-talentlms-from-hello-gallery"></a><span data-ttu-id="65821-123">Merhaba Galerisi'nden TalentLMS ekleme</span><span class="sxs-lookup"><span data-stu-id="65821-123">Adding TalentLMS from hello gallery</span></span>
<span data-ttu-id="65821-124">Azure AD'ye tooconfigure hello tümleştirme TalentLMS, tooadd TalentLMS hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="65821-124">tooconfigure hello integration of TalentLMS into Azure AD, you need tooadd TalentLMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="65821-125">**tooadd TalentLMS hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="65821-125">**tooadd TalentLMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="65821-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="65821-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="65821-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="65821-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="65821-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="65821-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="65821-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="65821-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="65821-133">Merhaba arama kutusuna yazın **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="65821-133">In hello search box, type **TalentLMS**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. <span data-ttu-id="65821-135">Merhaba Sonuçlar panelinde seçin **TalentLMS**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="65821-135">In hello results panel, select **TalentLMS**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="65821-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="65821-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="65821-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı TalentLMS ile test etme</span><span class="sxs-lookup"><span data-stu-id="65821-138">In this section, you configure and test Azure AD single sign-on with TalentLMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="65821-139">Tek toowork'ın oturum açma hangi hello karşılık gelen TalentLMS içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="65821-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TalentLMS is tooa user in Azure AD.</span></span> <span data-ttu-id="65821-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı TalentLMS hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="65821-140">In other words, a link relationship between an Azure AD user and hello related user in TalentLMS needs toobe established.</span></span>

<span data-ttu-id="65821-141">Merhaba hello değeri TalentLMS içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="65821-141">In TalentLMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="65821-142">tooconfigure ve TalentLMS ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="65821-142">tooconfigure and test Azure AD single sign-on with TalentLMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="65821-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="65821-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="65821-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="65821-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65821-145">**[TalentLMS test kullanıcısı oluşturma](#creating-a-talentlms-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir TalentLMS içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="65821-145">**[Creating a TalentLMS test user](#creating-a-talentlms-test-user)** - toohave a counterpart of Britta Simon in TalentLMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="65821-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="65821-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65821-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="65821-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="65821-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="65821-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="65821-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma TalentLMS uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="65821-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TalentLMS application.</span></span>

<span data-ttu-id="65821-150">**tooconfigure Azure AD çoklu oturum açma ile TalentLMS, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="65821-150">**tooconfigure Azure AD single sign-on with TalentLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="65821-151">Hello hello üzerinde Azure portal'ın **TalentLMS** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="65821-151">In hello Azure portal, on hello **TalentLMS** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="65821-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="65821-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. <span data-ttu-id="65821-155">Merhaba üzerinde **TalentLMS etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="65821-155">On hello **TalentLMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    <span data-ttu-id="65821-157">a.</span><span class="sxs-lookup"><span data-stu-id="65821-157">a.</span></span> <span data-ttu-id="65821-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenant-name>.TalentLMSapp.com`</span><span class="sxs-lookup"><span data-stu-id="65821-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.TalentLMSapp.com`</span></span>

    <span data-ttu-id="65821-159">b.</span><span class="sxs-lookup"><span data-stu-id="65821-159">b.</span></span> <span data-ttu-id="65821-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`http://<tenant-name>.talentlms.com`</span><span class="sxs-lookup"><span data-stu-id="65821-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://<tenant-name>.talentlms.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="65821-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="65821-161">These values are not real.</span></span> <span data-ttu-id="65821-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="65821-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="65821-163">Kişi [TalentLMS istemci destek ekibi](https://www.talentlms.com/contact) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="65821-163">Contact [TalentLMS Client support team](https://www.talentlms.com/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="65821-164">Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** hello sertifikasından değeri.</span><span class="sxs-lookup"><span data-stu-id="65821-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. <span data-ttu-id="65821-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="65821-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="65821-168">Merhaba üzerinde **TalentLMS yapılandırma** 'yi tıklatın **yapılandırma TalentLMS** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="65821-168">On hello **TalentLMS Configuration** section, click **Configure TalentLMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="65821-169">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="65821-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. <span data-ttu-id="65821-171">Farklı web tarayıcısı penceresinde tooyour TalentLMS şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="65821-171">In a different web browser window, log in tooyour TalentLMS company site as an administrator.</span></span>

8. <span data-ttu-id="65821-172">Merhaba, **hesap & ayarları** bölümünde, hello tıklatın **kullanıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="65821-172">In hello **Account & Settings** section, click hello **Users** tab.</span></span>
   
    <span data-ttu-id="65821-173">![Hesap & ayarları](./media/active-directory-saas-talentlms-tutorial/IC777296.png "hesap & ayarları")</span><span class="sxs-lookup"><span data-stu-id="65821-173">![Account & Settings](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Account & Settings")</span></span>

9. <span data-ttu-id="65821-174">Tıklatın **çoklu oturum açma (SSO)**,</span><span class="sxs-lookup"><span data-stu-id="65821-174">Click **Single Sign-On (SSO)**,</span></span>

10. <span data-ttu-id="65821-175">Hello çoklu oturum açma bölümü, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="65821-175">In hello Single Sign-On section, perform hello following steps:</span></span>
   
    <span data-ttu-id="65821-176">![Çoklu oturum açma](./media/active-directory-saas-talentlms-tutorial/IC777297.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="65821-176">![Single Sign-On](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span></span>   

    <span data-ttu-id="65821-177">a.</span><span class="sxs-lookup"><span data-stu-id="65821-177">a.</span></span> <span data-ttu-id="65821-178">Merhaba gelen **SSO tümleştirme türü** listesinde **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="65821-178">From hello **SSO integration type** list, select **SAML 2.0**.</span></span>

    <span data-ttu-id="65821-179">b.</span><span class="sxs-lookup"><span data-stu-id="65821-179">b.</span></span> <span data-ttu-id="65821-180">Merhaba, **kimlik sağlayıcıyı (IDP)** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="65821-180">In hello **Identity provider (IDP)** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="65821-181">c.</span><span class="sxs-lookup"><span data-stu-id="65821-181">c.</span></span> <span data-ttu-id="65821-182">Yapıştır hello **parmak izi** hello Azure portalına değerinden **sertifika parmak izi** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="65821-182">Paste hello **Thumbprint** value from Azure portal into hello **Certificate fingerprint** textbox.</span></span>    

    <span data-ttu-id="65821-183">d.</span><span class="sxs-lookup"><span data-stu-id="65821-183">d.</span></span>  <span data-ttu-id="65821-184">Merhaba, **uzaktan oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="65821-184">In hello **Remote sign-in URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="65821-185">e.</span><span class="sxs-lookup"><span data-stu-id="65821-185">e.</span></span> <span data-ttu-id="65821-186">Merhaba, **uzak oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="65821-186">In hello **Remote sign-out URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="65821-187">f.</span><span class="sxs-lookup"><span data-stu-id="65821-187">f.</span></span> <span data-ttu-id="65821-188">Merhaba aşağıdakileri doldurun:</span><span class="sxs-lookup"><span data-stu-id="65821-188">Fill in hello following:</span></span> 

    * <span data-ttu-id="65821-189">Merhaba, **TargetedID** metin kutusuna, türü`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span><span class="sxs-lookup"><span data-stu-id="65821-189">In hello **TargetedID** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span></span>
     
    * <span data-ttu-id="65821-190">Merhaba, **ad** metin kutusuna, türü`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span><span class="sxs-lookup"><span data-stu-id="65821-190">In hello **First name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span></span>
    
    * <span data-ttu-id="65821-191">Merhaba, **Soyadı** metin kutusuna, türü`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span><span class="sxs-lookup"><span data-stu-id="65821-191">In hello **Last name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span></span>
    
    * <span data-ttu-id="65821-192">Merhaba, **e-posta** metin kutusuna, türü`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="65821-192">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>
    
11. <span data-ttu-id="65821-193">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65821-193">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="65821-194">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="65821-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="65821-195">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="65821-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="65821-196">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="65821-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="65821-197">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="65821-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="65821-198">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="65821-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="65821-200">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="65821-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="65821-201">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="65821-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="65821-203">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="65821-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="65821-205">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="65821-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="65821-207">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="65821-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="65821-209">a.</span><span class="sxs-lookup"><span data-stu-id="65821-209">a.</span></span> <span data-ttu-id="65821-210">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="65821-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65821-211">b.</span><span class="sxs-lookup"><span data-stu-id="65821-211">b.</span></span> <span data-ttu-id="65821-212">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="65821-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="65821-213">c.</span><span class="sxs-lookup"><span data-stu-id="65821-213">c.</span></span> <span data-ttu-id="65821-214">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="65821-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="65821-215">d.</span><span class="sxs-lookup"><span data-stu-id="65821-215">d.</span></span> <span data-ttu-id="65821-216">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65821-216">Click **Create**.</span></span>
 
### <a name="creating-a-talentlms-test-user"></a><span data-ttu-id="65821-217">TalentLMS test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="65821-217">Creating a TalentLMS test user</span></span>

<span data-ttu-id="65821-218">tooenable Azure AD kullanıcıların toolog tooTalentLMS bunların TalentLMS sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="65821-218">tooenable Azure AD users toolog in tooTalentLMS, they must be provisioned into TalentLMS.</span></span> <span data-ttu-id="65821-219">TalentLMS Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="65821-219">In hello case of TalentLMS, provisioning is a manual task.</span></span>

<span data-ttu-id="65821-220">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="65821-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="65821-221">İçinde tooyour oturum **TalentLMS** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="65821-221">Log in tooyour **TalentLMS** tenant.</span></span>

2. <span data-ttu-id="65821-222">Tıklatın **kullanıcılar**ve ardından **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="65821-222">Click **Users**, and then click **Add User**.</span></span>

3. <span data-ttu-id="65821-223">Merhaba üzerinde **Kullanıcı Ekle** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="65821-223">On hello **Add user** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="65821-224">![Kullanıcı ekleme](./media/active-directory-saas-talentlms-tutorial/IC777299.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="65821-224">![Add User](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Add User")</span></span>  

    <span data-ttu-id="65821-225">a.</span><span class="sxs-lookup"><span data-stu-id="65821-225">a.</span></span> <span data-ttu-id="65821-226">Merhaba, **ad** metin kutusuna, hello ilk gibi kullanıcı adını girin **Britta**.</span><span class="sxs-lookup"><span data-stu-id="65821-226">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="65821-227">b.</span><span class="sxs-lookup"><span data-stu-id="65821-227">b.</span></span> <span data-ttu-id="65821-228">Merhaba, **Soyadı** metin kutusuna, hello son gibi kullanıcı adını girin **Simon**.</span><span class="sxs-lookup"><span data-stu-id="65821-228">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="65821-229">c.</span><span class="sxs-lookup"><span data-stu-id="65821-229">c.</span></span> <span data-ttu-id="65821-230">Merhaba, **e-posta adresi** metin kutusuna, bir kullanıcı gibi hello e-posta girin  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="65821-230">In hello **Email address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="65821-231">d.</span><span class="sxs-lookup"><span data-stu-id="65821-231">d.</span></span> <span data-ttu-id="65821-232">Tıklatın **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="65821-232">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="65821-233">API AAD kullanıcı hesaplarının TalentLMS tooprovision tarafından sağlanan veya herhangi diğer TalentLMS kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65821-233">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS tooprovision AAD user accounts.</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="65821-234">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="65821-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="65821-235">Bu bölümde, erişim tooTalentLMS vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="65821-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTalentLMS.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="65821-237">**tooassign Britta Simon tooTalentLMS hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="65821-237">**tooassign Britta Simon tooTalentLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="65821-238">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="65821-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="65821-240">Merhaba uygulamalar listesinde **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="65821-240">In hello applications list, select **TalentLMS**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. <span data-ttu-id="65821-242">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="65821-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="65821-244">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="65821-244">Click **Add** button.</span></span> <span data-ttu-id="65821-245">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="65821-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="65821-247">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="65821-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="65821-248">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="65821-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65821-249">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="65821-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="65821-250">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="65821-250">Testing single sign-on</span></span>

<span data-ttu-id="65821-251">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="65821-251">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="65821-252">Merhaba erişim paneli TalentLMS döşeme hello tıkladığınızda, otomatik olarak oturum açma TalentLMS uygulama tooyour almanız gerekir</span><span class="sxs-lookup"><span data-stu-id="65821-252">When you click hello TalentLMS tile in hello Access Panel, you should get automatically signed-on tooyour TalentLMS application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="65821-253">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="65821-253">Additional resources</span></span>

* [<span data-ttu-id="65821-254">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="65821-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65821-255">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="65821-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

