---
title: "Öğretici: Azure Active Directory Tümleştirme Uyarlamalı Suite ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Uyarlamalı Suite arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: af309c27ab74098c1e229c80adb11c96dc2774fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a><span data-ttu-id="b3581-103">Öğretici: Azure Active Directory Tümleştirme Uyarlamalı Suite ile</span><span class="sxs-lookup"><span data-stu-id="b3581-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span></span>

<span data-ttu-id="b3581-104">Bu öğreticide, bilgi nasıl toointegrate Uyarlamalı Suite Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b3581-104">In this tutorial, you learn how toointegrate Adaptive Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b3581-105">Uyarlamalı Suite Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="b3581-105">Integrating Adaptive Suite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b3581-106">Erişim tooAdaptive paketi olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b3581-106">You can control in Azure AD who has access tooAdaptive Suite</span></span>
- <span data-ttu-id="b3581-107">Kullanıcıların tooautomatically get açan tooAdaptive paketi (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b3581-107">You can enable your users tooautomatically get signed-on tooAdaptive Suite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b3581-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="b3581-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b3581-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b3581-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3581-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b3581-110">Prerequisites</span></span>

<span data-ttu-id="b3581-111">tooconfigure Uyarlamalı Suite ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b3581-111">tooconfigure Azure AD integration with Adaptive Suite, you need hello following items:</span></span>

- <span data-ttu-id="b3581-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="b3581-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b3581-113">Bir Uyarlamalı Suite çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="b3581-113">An Adaptive Suite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b3581-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="b3581-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b3581-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="b3581-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b3581-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="b3581-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b3581-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b3581-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b3581-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="b3581-118">Scenario description</span></span>
<span data-ttu-id="b3581-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="b3581-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b3581-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="b3581-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b3581-121">Merhaba Galerisi'nden Uyarlamalı paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="b3581-121">Adding Adaptive Suite from hello gallery</span></span>
2. <span data-ttu-id="b3581-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="b3581-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adaptive-suite-from-hello-gallery"></a><span data-ttu-id="b3581-123">Merhaba Galerisi'nden Uyarlamalı paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="b3581-123">Adding Adaptive Suite from hello gallery</span></span>
<span data-ttu-id="b3581-124">Azure AD'ye tooconfigure hello tümleştirme Uyarlamalı paketinin tooadd Uyarlamalı Suite hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3581-124">tooconfigure hello integration of Adaptive Suite into Azure AD, you need tooadd Adaptive Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b3581-125">**tooadd hello Galerisi, Uyarlamalı paketinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b3581-125">**tooadd Adaptive Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3581-126">Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b3581-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b3581-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="b3581-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b3581-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b3581-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="b3581-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b3581-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="b3581-133">Merhaba arama kutusuna yazın **Uyarlamalı Suite**.</span><span class="sxs-lookup"><span data-stu-id="b3581-133">In hello search box, type **Adaptive Suite**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. <span data-ttu-id="b3581-135">Merhaba Sonuçlar panelinde seçin **Uyarlamalı Suite**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="b3581-135">In hello results panel, select **Adaptive Suite**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b3581-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="b3581-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b3581-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Uyarlamalı "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Suite ile test etme</span><span class="sxs-lookup"><span data-stu-id="b3581-138">In this section, you configure and test Azure AD single sign-on with Adaptive Suite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b3581-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Uyarlamalı paketindeki tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3581-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adaptive Suite is tooa user in Azure AD.</span></span> <span data-ttu-id="b3581-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Uyarlamalı paketindeki arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3581-140">In other words, a link relationship between an Azure AD user and hello related user in Adaptive Suite needs toobe established.</span></span>

<span data-ttu-id="b3581-141">Uyarlamalı paketindeki hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="b3581-141">In Adaptive Suite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b3581-142">tooconfigure ve Uyarlamalı Suite ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b3581-142">tooconfigure and test Azure AD single sign-on with Adaptive Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b3581-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="b3581-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b3581-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="b3581-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b3581-145">**[Uyarlamalı Suite test kullanıcısı oluşturma](#creating-an-adaptive-suite-test-user) ** -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Uyarlamalı paketindeki, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="b3581-145">**[Creating an Adaptive Suite test user](#creating-an-adaptive-suite-test-user)** - toohave a counterpart of Britta Simon in Adaptive Suite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b3581-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="b3581-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b3581-147">**[Çoklu oturum açmayı test](#testing-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="b3581-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b3581-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b3581-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b3581-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Uyarlamalı Suite uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b3581-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Adaptive Suite application.</span></span>

<span data-ttu-id="b3581-150">**tooconfigure Azure AD çoklu oturum açma Uyarlamalı Suite ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b3581-150">**tooconfigure Azure AD single sign-on with Adaptive Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3581-151">Merhaba hello üzerinde Azure portal'ın **Uyarlamalı Suite** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="b3581-151">In hello Azure portal, on hello **Adaptive Suite** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="b3581-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="b3581-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. <span data-ttu-id="b3581-155">Merhaba üzerinde **Uyarlamalı Suite etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b3581-155">On hello **Adaptive Suite Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    <span data-ttu-id="b3581-157">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span><span class="sxs-lookup"><span data-stu-id="b3581-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    >[!NOTE]
    > <span data-ttu-id="b3581-158">Bu değer hello Uyarlamalı Suite's alabilir **SAML SSO ayarları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="b3581-158">You can get this value from hello Adaptive Suite’s **SAML SSO Settings** page.</span></span>
    >  

4. <span data-ttu-id="b3581-159">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b3581-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. <span data-ttu-id="b3581-161">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b3581-161">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b3581-163">Merhaba üzerinde **Uyarlamalı paketi yapılandırma** 'yi tıklatın **yapılandırma Uyarlamalı Suite** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="b3581-163">On hello **Adaptive Suite Configuration** section, click **Configure Adaptive Suite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b3581-164">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="b3581-164">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. <span data-ttu-id="b3581-166">Farklı web tarayıcısı penceresinde tooyour Uyarlamalı Suite şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b3581-166">In a different web browser window, log in tooyour Adaptive Suite company site as an administrator.</span></span>

8. <span data-ttu-id="b3581-167">Çok Git**yönetici**.</span><span class="sxs-lookup"><span data-stu-id="b3581-167">Go too**Admin**.</span></span>
   
    <span data-ttu-id="b3581-168">![Yönetici](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="b3581-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>

9. <span data-ttu-id="b3581-169">Merhaba, **kullanıcılar ve roller** 'yi tıklatın **SAML SSO ayarları yönetme**.</span><span class="sxs-lookup"><span data-stu-id="b3581-169">In hello **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>
   
    <span data-ttu-id="b3581-170">![SAML SSO ayarlarını Yönet](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "SAML SSO ayarlarını yönet")</span><span class="sxs-lookup"><span data-stu-id="b3581-170">![Manage SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>

10. <span data-ttu-id="b3581-171">Merhaba üzerinde **SAML SSO ayarları** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b3581-171">On hello **SAML SSO Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="b3581-172">![SAML SSO ayarları](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO ayarları")</span><span class="sxs-lookup"><span data-stu-id="b3581-172">![SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span></span>

    <span data-ttu-id="b3581-173">a.</span><span class="sxs-lookup"><span data-stu-id="b3581-173">a.</span></span> <span data-ttu-id="b3581-174">Merhaba, **kimlik sağlayıcı adı** metin kutusuna, yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="b3581-174">In hello **Identity provider name** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="b3581-175">b.</span><span class="sxs-lookup"><span data-stu-id="b3581-175">b.</span></span> <span data-ttu-id="b3581-176">Yapıştır hello **SAML varlık kimliği** değeri hello Azure portalından kopyalanan **kimlik sağlayıcısı varlık kimliği** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="b3581-176">Paste hello **SAML Entity ID** value copied from Azure portal into hello **Identity provider Entity ID** textbox.</span></span>
  
    <span data-ttu-id="b3581-177">c.</span><span class="sxs-lookup"><span data-stu-id="b3581-177">c.</span></span> <span data-ttu-id="b3581-178">Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** değeri hello Azure portalından kopyalanan **kimlik sağlayıcısı SSO URL** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="b3581-178">Paste hello **SAML Single Sign-On Service URL** value copied from Azure portal into hello **Identity provider SSO URL** textbox.</span></span>
  
    <span data-ttu-id="b3581-179">d.</span><span class="sxs-lookup"><span data-stu-id="b3581-179">d.</span></span> <span data-ttu-id="b3581-180">Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** değeri hello Azure portalından kopyalanan **özel oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="b3581-180">Paste hello **SAML Single Sign-On Service URL** value copied from Azure portal into hello **Custom logout URL** textbox.</span></span>
  
    <span data-ttu-id="b3581-181">e.</span><span class="sxs-lookup"><span data-stu-id="b3581-181">e.</span></span> <span data-ttu-id="b3581-182">tooupload indirilen sertifikanızı tıklatın **dosya**.</span><span class="sxs-lookup"><span data-stu-id="b3581-182">tooupload your downloaded certificate, click **Choose file**.</span></span>
  
    <span data-ttu-id="b3581-183">f.</span><span class="sxs-lookup"><span data-stu-id="b3581-183">f.</span></span> <span data-ttu-id="b3581-184">Merhaba, aşağıdakileri seçin:</span><span class="sxs-lookup"><span data-stu-id="b3581-184">Select hello following, for:</span></span>
    * <span data-ttu-id="b3581-185">**SAML kullanıcı kimliği**seçin **Uyarlamalı Öngörüler kullanıcının adını**.</span><span class="sxs-lookup"><span data-stu-id="b3581-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>
    * <span data-ttu-id="b3581-186">**SAML kullanıcı kimliği konumu**seçin **NameID, konu kullanıcı kimliği**.</span><span class="sxs-lookup"><span data-stu-id="b3581-186">**SAML user id location**, select **User id in NameID of Subject**.</span></span>
    * <span data-ttu-id="b3581-187">**SAML NameID biçimi**seçin **e-posta adresi**.</span><span class="sxs-lookup"><span data-stu-id="b3581-187">**SAML NameID format**, select **Email address**.</span></span>
    * <span data-ttu-id="b3581-188">**SAML'yi etkinleştir**seçin **izin SAML SSO ve doğrudan Uyarlamalı Öngörüler oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="b3581-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>
    
    <span data-ttu-id="b3581-189">g.</span><span class="sxs-lookup"><span data-stu-id="b3581-189">g.</span></span> <span data-ttu-id="b3581-190">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b3581-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b3581-191">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="b3581-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b3581-192">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="b3581-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b3581-193">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b3581-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b3581-194">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b3581-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="b3581-195">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="b3581-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="b3581-197">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b3581-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3581-198">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b3581-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b3581-200">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="b3581-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b3581-202">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="b3581-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b3581-204">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b3581-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b3581-206">a.</span><span class="sxs-lookup"><span data-stu-id="b3581-206">a.</span></span> <span data-ttu-id="b3581-207">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b3581-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b3581-208">b.</span><span class="sxs-lookup"><span data-stu-id="b3581-208">b.</span></span> <span data-ttu-id="b3581-209">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="b3581-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b3581-210">c.</span><span class="sxs-lookup"><span data-stu-id="b3581-210">c.</span></span> <span data-ttu-id="b3581-211">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="b3581-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b3581-212">d.</span><span class="sxs-lookup"><span data-stu-id="b3581-212">d.</span></span> <span data-ttu-id="b3581-213">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b3581-213">Click **Create**.</span></span>
 
### <a name="creating-an-adaptive-suite-test-user"></a><span data-ttu-id="b3581-214">Uyarlamalı Suite test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b3581-214">Creating an Adaptive Suite test user</span></span>

<span data-ttu-id="b3581-215">tooenable Azure AD kullanıcıların toolog tooAdaptive Suite'da, bunlar Uyarlamalı paketine sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3581-215">tooenable Azure AD users toolog in tooAdaptive Suite, they must be provisioned into Adaptive Suite.</span></span>  

* <span data-ttu-id="b3581-216">Uyarlamalı Suite Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="b3581-216">In hello case of Adaptive Suite, provisioning is a manual task.</span></span>

<span data-ttu-id="b3581-217">**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b3581-217">**tooconfigure user provisioning, perform hello following steps:**</span></span> 

1. <span data-ttu-id="b3581-218">İçinde tooyour oturum **Uyarlamalı Suite** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="b3581-218">Log in tooyour **Adaptive Suite** company site as an administrator.</span></span>
2. <span data-ttu-id="b3581-219">Çok Git**yönetici**.</span><span class="sxs-lookup"><span data-stu-id="b3581-219">Go too**Admin**.</span></span>
   
   <span data-ttu-id="b3581-220">![Yönetici](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="b3581-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="b3581-221">Merhaba, **kullanıcılar ve roller** 'yi tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="b3581-221">In hello **Users and Roles** section, click **Add User**.</span></span>
   
   <span data-ttu-id="b3581-222">![Kullanıcı ekleme](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="b3581-222">![Add User](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="b3581-223">Merhaba, **yeni kullanıcı** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b3581-223">In hello **New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="b3581-224">![Gönderme](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Gönder")</span><span class="sxs-lookup"><span data-stu-id="b3581-224">![Submit](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Submit")</span></span>   

   <span data-ttu-id="b3581-225">a.</span><span class="sxs-lookup"><span data-stu-id="b3581-225">a.</span></span> <span data-ttu-id="b3581-226">Türü hello **adı**, **oturum açma**, **e-posta**, **parola** geçerli bir Azure Active Directory kullanıcı ilgili hello tooprovision istiyor metin kutuları.</span><span class="sxs-lookup"><span data-stu-id="b3581-226">Type hello **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want tooprovision into hello related textboxes.</span></span>
  
   <span data-ttu-id="b3581-227">b.</span><span class="sxs-lookup"><span data-stu-id="b3581-227">b.</span></span> <span data-ttu-id="b3581-228">Seçin bir **rol**.</span><span class="sxs-lookup"><span data-stu-id="b3581-228">Select a **Role**.</span></span>
  
   <span data-ttu-id="b3581-229">c.</span><span class="sxs-lookup"><span data-stu-id="b3581-229">c.</span></span> <span data-ttu-id="b3581-230">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="b3581-230">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="b3581-231">API AAD kullanıcı hesapları Uyarlamalı Suite tooprovision tarafından sağlanan veya herhangi diğer Uyarlamalı Suite kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3581-231">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b3581-232">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="b3581-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b3581-233">Bu bölümde, erişim tooAdaptive Suite vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="b3581-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAdaptive Suite.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="b3581-235">**tooassign Britta Simon tooAdaptive Suite, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b3581-235">**tooassign Britta Simon tooAdaptive Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3581-236">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b3581-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="b3581-238">Merhaba uygulamalar listesinde **Uyarlamalı Suite**.</span><span class="sxs-lookup"><span data-stu-id="b3581-238">In hello applications list, select **Adaptive Suite**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. <span data-ttu-id="b3581-240">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="b3581-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="b3581-242">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b3581-242">Click **Add** button.</span></span> <span data-ttu-id="b3581-243">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b3581-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="b3581-245">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="b3581-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b3581-246">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b3581-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b3581-247">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b3581-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b3581-248">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="b3581-248">Testing single sign-on</span></span>

<span data-ttu-id="b3581-249">Bu bölümde Hello amacı olan tootest hello erişim paneli, Microsoft Azure AD çoklu oturum açma yapılandırması kullanılarak.</span><span class="sxs-lookup"><span data-stu-id="b3581-249">hello objective of this section is tootest your Microsoft Azure AD Single Sign-On configuration using hello Access Panel.</span></span>

<span data-ttu-id="b3581-250">Merhaba Uyarlamalı Suite hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Uyarlamalı paketi uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3581-250">When you click hello Adaptive Suite tile in hello Access Panel, you should get automatically signed-on tooyour Adaptive Suite application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b3581-251">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b3581-251">Additional resources</span></span>

* [<span data-ttu-id="b3581-252">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="b3581-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b3581-253">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="b3581-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

