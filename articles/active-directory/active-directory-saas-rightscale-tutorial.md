---
title: "Öğretici: Azure Active Directory Tümleştirme ile Rightscale | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Rightscale arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 53b927804a1e0f895778a164386459a4ea816f98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a><span data-ttu-id="bcacd-103">Öğretici: Azure Active Directory Tümleştirme Rightscale ile</span><span class="sxs-lookup"><span data-stu-id="bcacd-103">Tutorial: Azure Active Directory integration with Rightscale</span></span>

<span data-ttu-id="bcacd-104">Bu öğreticide, bilgi nasıl toointegrate Rightscale Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bcacd-104">In this tutorial, you learn how toointegrate Rightscale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bcacd-105">Rightscale Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="bcacd-105">Integrating Rightscale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bcacd-106">Erişim tooRightscale sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="bcacd-106">You can control in Azure AD who has access tooRightscale</span></span>
- <span data-ttu-id="bcacd-107">Kullanıcıların tooautomatically get açan tooRightscale (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="bcacd-107">You can enable your users tooautomatically get signed-on tooRightscale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bcacd-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="bcacd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bcacd-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bcacd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bcacd-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bcacd-110">Prerequisites</span></span>

<span data-ttu-id="bcacd-111">tooconfigure Rightscale ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="bcacd-111">tooconfigure Azure AD integration with Rightscale, you need hello following items:</span></span>

- <span data-ttu-id="bcacd-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="bcacd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bcacd-113">Bir Rightscale çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="bcacd-113">A Rightscale single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bcacd-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="bcacd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bcacd-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="bcacd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bcacd-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="bcacd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bcacd-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bcacd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bcacd-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="bcacd-118">Scenario description</span></span>
<span data-ttu-id="bcacd-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="bcacd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bcacd-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="bcacd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bcacd-121">Merhaba Galerisi'nden Rightscale ekleme</span><span class="sxs-lookup"><span data-stu-id="bcacd-121">Adding Rightscale from hello gallery</span></span>
2. <span data-ttu-id="bcacd-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="bcacd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightscale-from-hello-gallery"></a><span data-ttu-id="bcacd-123">Merhaba Galerisi'nden Rightscale ekleme</span><span class="sxs-lookup"><span data-stu-id="bcacd-123">Adding Rightscale from hello gallery</span></span>
<span data-ttu-id="bcacd-124">Azure AD'ye tooconfigure hello tümleştirme Rightscale, tooadd Rightscale hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="bcacd-124">tooconfigure hello integration of Rightscale into Azure AD, you need tooadd Rightscale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bcacd-125">**tooadd Rightscale hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bcacd-125">**tooadd Rightscale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bcacd-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="bcacd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bcacd-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="bcacd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bcacd-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="bcacd-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="bcacd-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bcacd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="bcacd-133">Merhaba arama kutusuna yazın **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="bcacd-133">In hello search box, type **Rightscale**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. <span data-ttu-id="bcacd-135">Merhaba Sonuçlar panelinde seçin **Rightscale**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="bcacd-135">In hello results panel, select **Rightscale**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bcacd-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="bcacd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bcacd-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Rightscale sınayın.</span><span class="sxs-lookup"><span data-stu-id="bcacd-138">In this section, you configure and test Azure AD single sign-on with Rightscale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bcacd-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Rightscale içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="bcacd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rightscale is tooa user in Azure AD.</span></span> <span data-ttu-id="bcacd-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Rightscale hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="bcacd-140">In other words, a link relationship between an Azure AD user and hello related user in Rightscale needs toobe established.</span></span>

<span data-ttu-id="bcacd-141">Merhaba hello değeri Rightscale içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="bcacd-141">In Rightscale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bcacd-142">tooconfigure ve Rightscale ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="bcacd-142">tooconfigure and test Azure AD single sign-on with Rightscale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bcacd-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="bcacd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bcacd-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="bcacd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bcacd-145">**[Rightscale test kullanıcısı oluşturma](#creating-a-rightscale-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Rightscale içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="bcacd-145">**[Creating a Rightscale test user](#creating-a-rightscale-test-user)** - toohave a counterpart of Britta Simon in Rightscale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bcacd-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="bcacd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bcacd-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="bcacd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bcacd-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bcacd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bcacd-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Rightscale uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bcacd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rightscale application.</span></span>

<span data-ttu-id="bcacd-150">**tooconfigure Azure AD çoklu oturum açma ile Rightscale, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bcacd-150">**tooconfigure Azure AD single sign-on with Rightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="bcacd-151">Hello hello üzerinde Azure portal'ın **Rightscale** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="bcacd-151">In hello Azure portal, on hello **Rightscale** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="bcacd-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="bcacd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. <span data-ttu-id="bcacd-155">Merhaba üzerinde **Rightscale etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP başlatılan modu** hello uygulama zaten Azure ile önceden tümleştirilmiştir, tooperform herhangi bir adım yoktur.</span><span class="sxs-lookup"><span data-stu-id="bcacd-155">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **IDP initiated mode** you do not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. <span data-ttu-id="bcacd-157">Merhaba üzerinde **Rightscale etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **SP tarafından başlatılan modu**, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bcacd-157">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    <span data-ttu-id="bcacd-159">a.</span><span class="sxs-lookup"><span data-stu-id="bcacd-159">a.</span></span> <span data-ttu-id="bcacd-160">Tıklatın hello üzerinde **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="bcacd-160">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="bcacd-161">b.</span><span class="sxs-lookup"><span data-stu-id="bcacd-161">b.</span></span> <span data-ttu-id="bcacd-162">Merhaba, **oturum üzerinde URL'si** metin kutusuna, türü hello URL'si:`https://login.rightscale.com/`</span><span class="sxs-lookup"><span data-stu-id="bcacd-162">In hello **Sign On URL** textbox, type hello URL: `https://login.rightscale.com/`</span></span>

5. <span data-ttu-id="bcacd-163">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="bcacd-163">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. <span data-ttu-id="bcacd-165">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bcacd-165">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="bcacd-167">Merhaba üzerinde **Rightscale yapılandırma** 'yi tıklatın **yapılandırma Rightscale** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="bcacd-167">On hello **Rightscale Configuration** section, click **Configure Rightscale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bcacd-168">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="bcacd-168">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="bcacd-169">![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="bcacd-169">![Configure Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span></span>
8. <span data-ttu-id="bcacd-170">Uygulamanız için yapılandırılmış SSO tooget, toosign üzerinde tooyour RightScale Kiracı yönetici olarak gerekir.</span><span class="sxs-lookup"><span data-stu-id="bcacd-170">tooget SSO configured for your application, you need toosign-on tooyour RightScale tenant as an administrator.</span></span>

    <span data-ttu-id="bcacd-171">a.</span><span class="sxs-lookup"><span data-stu-id="bcacd-171">a.</span></span> <span data-ttu-id="bcacd-172">Hello'nde hello üstte, hello menüsünü **ayarları** sekmesinde ve seçin **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="bcacd-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    <span data-ttu-id="bcacd-174">b.</span><span class="sxs-lookup"><span data-stu-id="bcacd-174">b.</span></span> <span data-ttu-id="bcacd-175">Merhaba tıklayın "**yeni**" düğmesine tooadd **bilgisayarınızı SAML kimlik sağlayıcısı**.</span><span class="sxs-lookup"><span data-stu-id="bcacd-175">Click hello "**new**" button tooadd **Your SAML Identity Providers**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    <span data-ttu-id="bcacd-177">c.</span><span class="sxs-lookup"><span data-stu-id="bcacd-177">c.</span></span> <span data-ttu-id="bcacd-178">Merhaba metin kutusuna **görünen adı**, şirket adınızı girin.</span><span class="sxs-lookup"><span data-stu-id="bcacd-178">In hello textbox of **Display Name**, input your company name.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    <span data-ttu-id="bcacd-180">d.</span><span class="sxs-lookup"><span data-stu-id="bcacd-180">d.</span></span> <span data-ttu-id="bcacd-181">Seçin **izin RightScale tarafından başlatılan SSO'yu bir bulma ipucu kullanarak** ve giriş, **etki alanı adı** metin kutusu altında hello içinde.</span><span class="sxs-lookup"><span data-stu-id="bcacd-181">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in hello below textbox.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    <span data-ttu-id="bcacd-183">e.</span><span class="sxs-lookup"><span data-stu-id="bcacd-183">e.</span></span> <span data-ttu-id="bcacd-184">Yapıştırma hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan **SAML SSO Endpoint** RightScale içinde.</span><span class="sxs-lookup"><span data-stu-id="bcacd-184">Paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal into **SAML SSO Endpoint** in RightScale.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    <span data-ttu-id="bcacd-186">f.</span><span class="sxs-lookup"><span data-stu-id="bcacd-186">f.</span></span> <span data-ttu-id="bcacd-187">Yapıştırma hello değerini **SAML varlık kimliği** Azure portalından kopyalanan **SAML Entityıd** RightScale içinde.</span><span class="sxs-lookup"><span data-stu-id="bcacd-187">Paste hello value of **SAML Entity ID** which you have copied from Azure portal into **SAML EntityID** in RightScale.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    <span data-ttu-id="bcacd-189">g.</span><span class="sxs-lookup"><span data-stu-id="bcacd-189">g.</span></span> <span data-ttu-id="bcacd-190">Tıklatın **tarayıcı** Azure Portalı'ndan indirilen düğmesi tooupload hello sertifika.</span><span class="sxs-lookup"><span data-stu-id="bcacd-190">Click **Browser** button tooupload hello certificate which you downloaded from Azure portal.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    <span data-ttu-id="bcacd-192">h.</span><span class="sxs-lookup"><span data-stu-id="bcacd-192">h.</span></span> <span data-ttu-id="bcacd-193">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bcacd-193">Click **Save**.</span></span>
<CE>
> [!TIP]
> <span data-ttu-id="bcacd-194">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="bcacd-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bcacd-195">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="bcacd-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bcacd-196">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bcacd-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bcacd-197">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bcacd-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="bcacd-198">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="bcacd-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="bcacd-200">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bcacd-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bcacd-201">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="bcacd-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bcacd-203">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="bcacd-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bcacd-205">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="bcacd-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bcacd-207">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bcacd-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bcacd-209">a.</span><span class="sxs-lookup"><span data-stu-id="bcacd-209">a.</span></span> <span data-ttu-id="bcacd-210">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bcacd-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bcacd-211">b.</span><span class="sxs-lookup"><span data-stu-id="bcacd-211">b.</span></span> <span data-ttu-id="bcacd-212">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="bcacd-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bcacd-213">c.</span><span class="sxs-lookup"><span data-stu-id="bcacd-213">c.</span></span> <span data-ttu-id="bcacd-214">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="bcacd-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bcacd-215">d.</span><span class="sxs-lookup"><span data-stu-id="bcacd-215">d.</span></span> <span data-ttu-id="bcacd-216">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bcacd-216">Click **Create**.</span></span>
 
### <a name="creating-a-rightscale-test-user"></a><span data-ttu-id="bcacd-217">Rightscale test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bcacd-217">Creating a Rightscale test user</span></span>

<span data-ttu-id="bcacd-218">Bu bölümde, RightScale içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bcacd-218">In this section, you create a user called Britta Simon in RightScale.</span></span> <span data-ttu-id="bcacd-219">Çalışmak [Rightscale istemci destek ekibi](mailto:support@rightscale.com) tooadd hello kullanıcılar hello RightScale Platform.</span><span class="sxs-lookup"><span data-stu-id="bcacd-219">Work with [Rightscale Client support team](mailto:support@rightscale.com) tooadd hello users in hello RightScale platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bcacd-220">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="bcacd-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bcacd-221">Bu bölümde, erişim tooRightscale vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="bcacd-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRightscale.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="bcacd-223">**tooassign Britta Simon tooRightscale hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bcacd-223">**tooassign Britta Simon tooRightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="bcacd-224">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="bcacd-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="bcacd-226">Merhaba uygulamalar listesinde **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="bcacd-226">In hello applications list, select **Rightscale**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. <span data-ttu-id="bcacd-228">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="bcacd-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="bcacd-230">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bcacd-230">Click **Add** button.</span></span> <span data-ttu-id="bcacd-231">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bcacd-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="bcacd-233">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="bcacd-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bcacd-234">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bcacd-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bcacd-235">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bcacd-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bcacd-236">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="bcacd-236">Testing single sign-on</span></span>

<span data-ttu-id="bcacd-237">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="bcacd-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="bcacd-238">Merhaba RightScale hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour RightScale uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bcacd-238">When you click hello RightScale tile in hello Access Panel, you should get automatically signed-on tooyour RightScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bcacd-239">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="bcacd-239">Additional resources</span></span>

* [<span data-ttu-id="bcacd-240">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="bcacd-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bcacd-241">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="bcacd-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

