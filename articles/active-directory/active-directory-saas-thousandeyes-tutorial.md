---
title: "Öğretici: Azure Active Directory Tümleştirme ile ThousandEyes | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile ThousandEyes arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: fbfbfb71809355b1b138762757a851907737730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a><span data-ttu-id="d1b5e-103">Öğretici: Azure Active Directory Tümleştirme ThousandEyes ile</span><span class="sxs-lookup"><span data-stu-id="d1b5e-103">Tutorial: Azure Active Directory integration with ThousandEyes</span></span>

<span data-ttu-id="d1b5e-104">Bu öğreticide, bilgi nasıl toointegrate ThousandEyes Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d1b5e-104">In this tutorial, you learn how toointegrate ThousandEyes with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d1b5e-105">ThousandEyes Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="d1b5e-105">Integrating ThousandEyes with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d1b5e-106">Erişim tooThousandEyes sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d1b5e-106">You can control in Azure AD who has access tooThousandEyes</span></span>
- <span data-ttu-id="d1b5e-107">Kullanıcıların tooautomatically get açan tooThousandEyes (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d1b5e-107">You can enable your users tooautomatically get signed-on tooThousandEyes (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d1b5e-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="d1b5e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d1b5e-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d1b5e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1b5e-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d1b5e-110">Prerequisites</span></span>

<span data-ttu-id="d1b5e-111">tooconfigure ThousandEyes ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d1b5e-111">tooconfigure Azure AD integration with ThousandEyes, you need hello following items:</span></span>

- <span data-ttu-id="d1b5e-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="d1b5e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d1b5e-113">Bir ThousandEyes çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="d1b5e-113">A ThousandEyes single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d1b5e-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d1b5e-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="d1b5e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d1b5e-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d1b5e-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d1b5e-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d1b5e-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="d1b5e-118">Scenario description</span></span>
<span data-ttu-id="d1b5e-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d1b5e-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="d1b5e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d1b5e-121">Merhaba Galerisi'nden ThousandEyes ekleme</span><span class="sxs-lookup"><span data-stu-id="d1b5e-121">Adding ThousandEyes from hello gallery</span></span>
2. <span data-ttu-id="d1b5e-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d1b5e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thousandeyes-from-hello-gallery"></a><span data-ttu-id="d1b5e-123">Merhaba Galerisi'nden ThousandEyes ekleme</span><span class="sxs-lookup"><span data-stu-id="d1b5e-123">Adding ThousandEyes from hello gallery</span></span>
<span data-ttu-id="d1b5e-124">Azure AD'ye tooconfigure hello tümleştirme ThousandEyes, tooadd ThousandEyes hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-124">tooconfigure hello integration of ThousandEyes into Azure AD, you need tooadd ThousandEyes from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d1b5e-125">**tooadd ThousandEyes hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d1b5e-125">**tooadd ThousandEyes from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1b5e-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d1b5e-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d1b5e-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="d1b5e-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="d1b5e-133">Merhaba arama kutusuna yazın **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-133">In hello search box, type **ThousandEyes**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. <span data-ttu-id="d1b5e-135">Merhaba Sonuçlar panelinde seçin **ThousandEyes**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-135">In hello results panel, select **ThousandEyes**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d1b5e-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d1b5e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d1b5e-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı ThousandEyes sınayın.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-138">In this section, you configure and test Azure AD single sign-on with ThousandEyes based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d1b5e-139">Tek toowork'ın oturum açma hangi hello karşılık gelen ThousandEyes içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ThousandEyes is tooa user in Azure AD.</span></span> <span data-ttu-id="d1b5e-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı ThousandEyes hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-140">In other words, a link relationship between an Azure AD user and hello related user in ThousandEyes needs toobe established.</span></span>

<span data-ttu-id="d1b5e-141">Merhaba hello değeri ThousandEyes içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-141">In ThousandEyes, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d1b5e-142">tooconfigure ve ThousandEyes ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d1b5e-142">tooconfigure and test Azure AD single sign-on with ThousandEyes, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d1b5e-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d1b5e-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d1b5e-145">**[ThousandEyes test kullanıcısı oluşturma](#creating-a-thousandeyes-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir ThousandEyes içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-145">**[Creating a ThousandEyes test user](#creating-a-thousandeyes-test-user)** - toohave a counterpart of Britta Simon in ThousandEyes that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d1b5e-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d1b5e-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d1b5e-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d1b5e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d1b5e-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma ThousandEyes uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ThousandEyes application.</span></span>

<span data-ttu-id="d1b5e-150">**tooconfigure Azure AD çoklu oturum açma ile ThousandEyes, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d1b5e-150">**tooconfigure Azure AD single sign-on with ThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1b5e-151">Hello hello üzerinde Azure portal'ın **ThousandEyes** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-151">In hello Azure portal, on hello **ThousandEyes** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="d1b5e-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. <span data-ttu-id="d1b5e-155">Merhaba üzerinde **ThousandEyes etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d1b5e-155">On hello **ThousandEyes Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    <span data-ttu-id="d1b5e-157">Merhaba, **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://app.thousandeyes.com/login/sso`</span><span class="sxs-lookup"><span data-stu-id="d1b5e-157">In hello **Sign-on URL** textbox, type a URL as: `https://app.thousandeyes.com/login/sso`</span></span>

4. <span data-ttu-id="d1b5e-158">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. <span data-ttu-id="d1b5e-160">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-160">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d1b5e-162">Merhaba üzerinde **ThousandEyes yapılandırma** 'yi tıklatın **yapılandırma ThousandEyes** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-162">On hello **ThousandEyes Configuration** section, click **Configure ThousandEyes** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d1b5e-163">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="d1b5e-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. <span data-ttu-id="d1b5e-165">Farklı web tarayıcısı penceresinde tooyour üzerinde oturum **ThousandEyes** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-165">In a different web browser window, sign on tooyour **ThousandEyes** company site as an administrator.</span></span>

8. <span data-ttu-id="d1b5e-166">Hello içinde hello üst menüsünde **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-166">In hello menu on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="d1b5e-167">![Ayarları](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="d1b5e-167">![Settings](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Settings")</span></span>

9. <span data-ttu-id="d1b5e-168">Tıklatın **hesabı**</span><span class="sxs-lookup"><span data-stu-id="d1b5e-168">Click **Account**</span></span>
   
    <span data-ttu-id="d1b5e-169">![Hesap](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "hesabı")</span><span class="sxs-lookup"><span data-stu-id="d1b5e-169">![Account](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Account")</span></span>

10. <span data-ttu-id="d1b5e-170">Merhaba tıklatın **güvenlik ve kimlik doğrulama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-170">Click hello **Security & Authentication** tab.</span></span>
   
    <span data-ttu-id="d1b5e-171">![Güvenlik ve kimlik doğrulama](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "güvenlik ve kimlik doğrulama")</span><span class="sxs-lookup"><span data-stu-id="d1b5e-171">![Security & Authentication](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Security & Authentication")</span></span>

11. <span data-ttu-id="d1b5e-172">Merhaba, **Kurulum çoklu oturum açma** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d1b5e-172">In hello **Setup Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="d1b5e-173">![Çoklu oturum açma Kurulum](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Kurulum çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="d1b5e-173">![Setup Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Setup Single Sign-On")</span></span>
  
    <span data-ttu-id="d1b5e-174">a.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-174">a.</span></span> <span data-ttu-id="d1b5e-175">Seçin **çoklu oturum açmayı etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-175">Select **Enable Single Sign-On**.</span></span>
  
    <span data-ttu-id="d1b5e-176">b.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-176">b.</span></span> <span data-ttu-id="d1b5e-177">İçinde **oturum açma sayfası URL'si** metin kutusuna, Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-177">In **Login Page URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="d1b5e-178">c.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-178">c.</span></span> <span data-ttu-id="d1b5e-179">İçinde **oturum kapatma sayfası URL'si** metin kutusuna, Yapıştır **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-179">In **Logout Page URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="d1b5e-180">d.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-180">d.</span></span> <span data-ttu-id="d1b5e-181">**Kimlik sağlayıcısı veren** metin kutusuna, Yapıştır **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-181">**Identity Provider Issuer** textbox, paste **SAML Entity ID** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="d1b5e-182">e.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-182">e.</span></span> <span data-ttu-id="d1b5e-183">İçinde **doğrulama sertifikası**, tıklatın **dosya**ve Azure portalından indirdiğiniz hello sertifikasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-183">In **Verification Certificate**, click **Choose file**, and then upload hello certificate you have downloaded from Azure portal.</span></span>
  
    <span data-ttu-id="d1b5e-184">f.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-184">f.</span></span> <span data-ttu-id="d1b5e-185">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-185">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="d1b5e-186">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="d1b5e-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d1b5e-187">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d1b5e-188">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d1b5e-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d1b5e-189">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d1b5e-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="d1b5e-190">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="d1b5e-192">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d1b5e-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1b5e-193">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d1b5e-195">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d1b5e-197">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d1b5e-199">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d1b5e-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d1b5e-201">a.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-201">a.</span></span> <span data-ttu-id="d1b5e-202">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d1b5e-203">b.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-203">b.</span></span> <span data-ttu-id="d1b5e-204">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d1b5e-205">c.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-205">c.</span></span> <span data-ttu-id="d1b5e-206">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d1b5e-207">d.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-207">d.</span></span> <span data-ttu-id="d1b5e-208">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-208">Click **Create**.</span></span>
 
### <a name="creating-a-thousandeyes-test-user"></a><span data-ttu-id="d1b5e-209">ThousandEyes test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d1b5e-209">Creating a ThousandEyes test user</span></span>

<span data-ttu-id="d1b5e-210">ThousandEyes içine sipariş tooenable Azure AD kullanıcıların toolog bunların ThousandEyes sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-210">In order tooenable Azure AD users toolog into ThousandEyes, they must be provisioned into ThousandEyes.</span></span>  
<span data-ttu-id="d1b5e-211">ThousandEyes Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-211">In hello case of ThousandEyes, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="d1b5e-212">API, kullanıcı hesaplarını ThousandEyes tooprovision Azure Active Directory tarafından sağlanan veya herhangi diğer ThousandEyes kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-212">You can use any other ThousandEyes user account creation tools or APIs provided by ThousandEyes tooprovision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="d1b5e-213">**bir kullanıcı hesabı tooThousandEyes tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d1b5e-213">**tooprovision a user account tooThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1b5e-214">ThousandEyes şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-214">Log into your ThousandEyes company site as an administrator.</span></span>

2. <span data-ttu-id="d1b5e-215">Tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-215">Click **Settings**.</span></span>
   
    <span data-ttu-id="d1b5e-216">![Ayarları](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="d1b5e-216">![Settings](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Settings")</span></span>

3. <span data-ttu-id="d1b5e-217">Tıklatın **hesap**.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-217">Click **Account**.</span></span>
   
    <span data-ttu-id="d1b5e-218">![Hesap](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "hesabı")</span><span class="sxs-lookup"><span data-stu-id="d1b5e-218">![Account](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span></span>

4. <span data-ttu-id="d1b5e-219">Merhaba tıklatın **hesapları k & ullanıcıların** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-219">Click hello **Accounts & Users** tab.</span></span>
   
    <span data-ttu-id="d1b5e-220">![K & ullanıcıların hesapları](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "hesapları ve kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="d1b5e-220">![Accounts & Users](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Accounts & Users")</span></span>

5. <span data-ttu-id="d1b5e-221">Merhaba, **Kullanıcı Ekle & hesapları** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d1b5e-221">In hello **Add Users & Accounts** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="d1b5e-222">![Kullanıcı hesapları ekleme](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "kullanıcı hesapları ekleme")</span><span class="sxs-lookup"><span data-stu-id="d1b5e-222">![Add User Accounts](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Add User Accounts")</span></span>   
  
    <span data-ttu-id="d1b5e-223">a.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-223">a.</span></span> <span data-ttu-id="d1b5e-224">İçinde **adı** metin kutusuna, tür hello gibi kullanıcı adını **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-224">In **Name** textbox, type hello name of user like **Britta Simon**.</span></span>

    <span data-ttu-id="d1b5e-225">b.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-225">b.</span></span> <span data-ttu-id="d1b5e-226">İçinde **e-posta** metin kutusuna, kullanıcının türü hello e-posta ister  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="d1b5e-226">In **Email** textbox, type hello email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="d1b5e-227">b.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-227">b.</span></span> <span data-ttu-id="d1b5e-228">Tıklatın **yeni kullanıcı Ekle tooAccount**.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-228">Click **Add New User tooAccount**.</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="d1b5e-229">Hello Azure Active Directory hesap sahibi bağlantı tooconfirm dahil olmak üzere bir e-posta almak ve hello hesabını etkinleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-229">hello Azure Active Directory account holder will get an email including a link tooconfirm and activate hello account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d1b5e-230">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="d1b5e-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d1b5e-231">Bu bölümde, erişim tooThousandEyes vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThousandEyes.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="d1b5e-233">**tooassign Britta Simon tooThousandEyes hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d1b5e-233">**tooassign Britta Simon tooThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1b5e-234">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="d1b5e-236">Merhaba uygulamalar listesinde **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-236">In hello applications list, select **ThousandEyes**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. <span data-ttu-id="d1b5e-238">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="d1b5e-240">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-240">Click **Add** button.</span></span> <span data-ttu-id="d1b5e-241">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="d1b5e-243">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d1b5e-244">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d1b5e-245">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d1b5e-246">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="d1b5e-246">Testing single sign-on</span></span>

<span data-ttu-id="d1b5e-247">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-247">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d1b5e-248">Hello erişim paneli ThousandEyes döşeme hello tıkladığınızda, otomatik olarak oturum açma ThousandEyes uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-248">When you click hello ThousandEyes tile in hello Access Panel, you should get automatically signed-on tooyour ThousandEyes application.</span></span>

<span data-ttu-id="d1b5e-249">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d1b5e-249">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d1b5e-250">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d1b5e-250">Additional resources</span></span>

* [<span data-ttu-id="d1b5e-251">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="d1b5e-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d1b5e-252">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="d1b5e-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png

