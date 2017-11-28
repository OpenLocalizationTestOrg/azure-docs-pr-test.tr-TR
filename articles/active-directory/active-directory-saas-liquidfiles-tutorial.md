---
title: "Öğretici: Azure Active Directory Tümleştirme ile LiquidFiles | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile LiquidFiles arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cb517134-0b34-4a74-b40c-5a3223ca81b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 67eb888090f81e0ceb791ed45d564b98fe1eb6d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-liquidfiles"></a><span data-ttu-id="24ed0-103">Öğretici: Azure Active Directory Tümleştirme LiquidFiles ile</span><span class="sxs-lookup"><span data-stu-id="24ed0-103">Tutorial: Azure Active Directory integration with LiquidFiles</span></span>

<span data-ttu-id="24ed0-104">Bu öğreticide, bilgi nasıl toointegrate LiquidFiles Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="24ed0-104">In this tutorial, you learn how toointegrate LiquidFiles with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="24ed0-105">LiquidFiles Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="24ed0-105">Integrating LiquidFiles with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="24ed0-106">Erişim tooLiquidFiles sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="24ed0-106">You can control in Azure AD who has access tooLiquidFiles</span></span>
- <span data-ttu-id="24ed0-107">Kullanıcıların tooautomatically get açan tooLiquidFiles (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="24ed0-107">You can enable your users tooautomatically get signed-on tooLiquidFiles (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="24ed0-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="24ed0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="24ed0-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="24ed0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24ed0-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="24ed0-110">Prerequisites</span></span>

<span data-ttu-id="24ed0-111">tooconfigure LiquidFiles ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="24ed0-111">tooconfigure Azure AD integration with LiquidFiles, you need hello following items:</span></span>

- <span data-ttu-id="24ed0-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="24ed0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="24ed0-113">Bir LiquidFiles çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="24ed0-113">A LiquidFiles single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="24ed0-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="24ed0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="24ed0-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="24ed0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="24ed0-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="24ed0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="24ed0-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24ed0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="24ed0-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="24ed0-118">Scenario description</span></span>
<span data-ttu-id="24ed0-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="24ed0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="24ed0-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="24ed0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="24ed0-121">Merhaba Galerisi'nden LiquidFiles ekleme</span><span class="sxs-lookup"><span data-stu-id="24ed0-121">Adding LiquidFiles from hello gallery</span></span>
2. <span data-ttu-id="24ed0-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="24ed0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-liquidfiles-from-hello-gallery"></a><span data-ttu-id="24ed0-123">Merhaba Galerisi'nden LiquidFiles ekleme</span><span class="sxs-lookup"><span data-stu-id="24ed0-123">Adding LiquidFiles from hello gallery</span></span>
<span data-ttu-id="24ed0-124">Azure AD'ye tooconfigure hello tümleştirme LiquidFiles, tooadd LiquidFiles hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="24ed0-124">tooconfigure hello integration of LiquidFiles into Azure AD, you need tooadd LiquidFiles from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="24ed0-125">**tooadd LiquidFiles hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="24ed0-125">**tooadd LiquidFiles from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="24ed0-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="24ed0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="24ed0-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="24ed0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="24ed0-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="24ed0-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="24ed0-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="24ed0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="24ed0-133">Merhaba arama kutusuna yazın **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="24ed0-133">In hello search box, type **LiquidFiles**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_search.png)

5. <span data-ttu-id="24ed0-135">Merhaba Sonuçlar panelinde seçin **LiquidFiles**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="24ed0-135">In hello results panel, select **LiquidFiles**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="24ed0-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="24ed0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="24ed0-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı LiquidFiles sınayın.</span><span class="sxs-lookup"><span data-stu-id="24ed0-138">In this section, you configure and test Azure AD single sign-on with LiquidFiles based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="24ed0-139">Tek toowork'ın oturum açma hangi hello karşılık gelen LiquidFiles içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="24ed0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LiquidFiles is tooa user in Azure AD.</span></span> <span data-ttu-id="24ed0-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı LiquidFiles hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="24ed0-140">In other words, a link relationship between an Azure AD user and hello related user in LiquidFiles needs toobe established.</span></span>

<span data-ttu-id="24ed0-141">Merhaba hello değeri LiquidFiles içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="24ed0-141">In LiquidFiles, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="24ed0-142">tooconfigure ve LiquidFiles ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="24ed0-142">tooconfigure and test Azure AD single sign-on with LiquidFiles, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="24ed0-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="24ed0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="24ed0-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="24ed0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="24ed0-145">**[LiquidFiles test kullanıcısı oluşturma](#creating-a-liquidfiles-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir LiquidFiles içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="24ed0-145">**[Creating a LiquidFiles test user](#creating-a-liquidfiles-test-user)** - toohave a counterpart of Britta Simon in LiquidFiles that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="24ed0-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="24ed0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="24ed0-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="24ed0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="24ed0-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="24ed0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="24ed0-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma LiquidFiles uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="24ed0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LiquidFiles application.</span></span>

<span data-ttu-id="24ed0-150">**tooconfigure Azure AD çoklu oturum açma ile LiquidFiles, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="24ed0-150">**tooconfigure Azure AD single sign-on with LiquidFiles, perform hello following steps:**</span></span>

1. <span data-ttu-id="24ed0-151">Hello hello üzerinde Azure portal'ın **LiquidFiles** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="24ed0-151">In hello Azure portal, on hello **LiquidFiles** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="24ed0-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="24ed0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_samlbase.png)

3. <span data-ttu-id="24ed0-155">Merhaba üzerinde **LiquidFiles etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="24ed0-155">On hello **LiquidFiles Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_url.png)

    <span data-ttu-id="24ed0-157">a.</span><span class="sxs-lookup"><span data-stu-id="24ed0-157">a.</span></span> <span data-ttu-id="24ed0-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<YOUR_SERVER_URL>/saml/init`</span><span class="sxs-lookup"><span data-stu-id="24ed0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>/saml/init`</span></span>

    <span data-ttu-id="24ed0-159">b.</span><span class="sxs-lookup"><span data-stu-id="24ed0-159">b.</span></span> <span data-ttu-id="24ed0-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<YOUR_SERVER_URL>`</span><span class="sxs-lookup"><span data-stu-id="24ed0-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>`</span></span>

    <span data-ttu-id="24ed0-161">c.</span><span class="sxs-lookup"><span data-stu-id="24ed0-161">c.</span></span> <span data-ttu-id="24ed0-162">b.</span><span class="sxs-lookup"><span data-stu-id="24ed0-162">b.</span></span> <span data-ttu-id="24ed0-163">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<YOUR_SERVER_URL>/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="24ed0-163">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="24ed0-164">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="24ed0-164">These values are not real.</span></span> <span data-ttu-id="24ed0-165">Bu değerleri ile güncelleştirme hello gerçek oturum açma URL'si, tanıtıcısı ve yanıt URL'si.</span><span class="sxs-lookup"><span data-stu-id="24ed0-165">Update these values with hello actual Sign-On URL, Identifier and, Reply URL.</span></span> <span data-ttu-id="24ed0-166">Kişi [LiquidFiles istemci destek ekibi](https://www.liquidfiles.com/support.html) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="24ed0-166">Contact [LiquidFiles Client support team](https://www.liquidfiles.com/support.html) tooget these values.</span></span> 
 
4. <span data-ttu-id="24ed0-167">Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="24ed0-167">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_certificate.png) 

5. <span data-ttu-id="24ed0-169">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="24ed0-169">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="24ed0-171">Merhaba üzerinde **LiquidFiles yapılandırma** 'yi tıklatın **yapılandırma LiquidFiles** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="24ed0-171">On hello **LiquidFiles Configuration** section, click **Configure LiquidFiles** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="24ed0-172">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="24ed0-172">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_configure.png)
 
7. <span data-ttu-id="24ed0-174">Yönetici olarak oturum açma tooyour LiquidFiles şirket sitesi.</span><span class="sxs-lookup"><span data-stu-id="24ed0-174">Sign-on tooyour LiquidFiles company site as administrator.</span></span>

8. <span data-ttu-id="24ed0-175">Tıklatın **çoklu oturum açma** hello içinde **yönetici > yapılandırma** hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="24ed0-175">Click **Single Sign-On** in hello **Admin > Configuration** from hello menu.</span></span>

9. <span data-ttu-id="24ed0-176">Merhaba üzerinde **tek oturum açma yapılandırması** sayfasında, aşağıdaki adımları hello gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="24ed0-176">On hello **Single Sign-On Configuration** page, perform hello following steps</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-liquidfiles-tutorial/tutorial_single_01.png)

    <span data-ttu-id="24ed0-178">a.</span><span class="sxs-lookup"><span data-stu-id="24ed0-178">a.</span></span> <span data-ttu-id="24ed0-179">Olarak **tek oturum açma yönetimini**seçin **SAML 2**.</span><span class="sxs-lookup"><span data-stu-id="24ed0-179">As **Single Sign On Method**, select **SAML 2**.</span></span>

    <span data-ttu-id="24ed0-180">b.</span><span class="sxs-lookup"><span data-stu-id="24ed0-180">b.</span></span> <span data-ttu-id="24ed0-181">Merhaba, **IDP oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="24ed0-181">In hello **IDP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="24ed0-182">c.</span><span class="sxs-lookup"><span data-stu-id="24ed0-182">c.</span></span> <span data-ttu-id="24ed0-183">Merhaba, **IDP oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="24ed0-183">In hello **IDP Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="24ed0-184">d.</span><span class="sxs-lookup"><span data-stu-id="24ed0-184">d.</span></span> <span data-ttu-id="24ed0-185">Merhaba, **IDP sertifika parmak izi** metin kutusuna, Yapıştır hello **parmak İZİ** Azure portalından kopyaladığınız değeri...</span><span class="sxs-lookup"><span data-stu-id="24ed0-185">In hello **IDP Cert Fingerprint** textbox, paste hello **THUMBPRINT** value which you have copied from Azure portal..</span></span>

    <span data-ttu-id="24ed0-186">e.</span><span class="sxs-lookup"><span data-stu-id="24ed0-186">e.</span></span> <span data-ttu-id="24ed0-187">Merhaba değer Hello ad tanımlayıcısı biçimi metin kutusuna yazın **urn: OASIS: adları: tc: SAML:1.1:nameid-biçimi: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="24ed0-187">In hello Name Identifier Format textbox, type hello value **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="24ed0-188">f.</span><span class="sxs-lookup"><span data-stu-id="24ed0-188">f.</span></span> <span data-ttu-id="24ed0-189">Hello Authn bağlamı metin kutusuna, hello değeri yazın **urn: OASIS: adları: tc: SAML:2.0:ac:classes:PasswordProtectedTransport**.</span><span class="sxs-lookup"><span data-stu-id="24ed0-189">In hello Authn Context textbox, type hello value **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport**.</span></span>

    <span data-ttu-id="24ed0-190">g.</span><span class="sxs-lookup"><span data-stu-id="24ed0-190">g.</span></span> <span data-ttu-id="24ed0-191">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="24ed0-191">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="24ed0-192">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="24ed0-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="24ed0-193">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="24ed0-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="24ed0-194">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="24ed0-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="24ed0-195">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="24ed0-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="24ed0-196">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="24ed0-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="24ed0-198">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="24ed0-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="24ed0-199">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="24ed0-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="24ed0-201">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="24ed0-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="24ed0-203">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="24ed0-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="24ed0-205">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="24ed0-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="24ed0-207">a.</span><span class="sxs-lookup"><span data-stu-id="24ed0-207">a.</span></span> <span data-ttu-id="24ed0-208">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="24ed0-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="24ed0-209">b.</span><span class="sxs-lookup"><span data-stu-id="24ed0-209">b.</span></span> <span data-ttu-id="24ed0-210">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="24ed0-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="24ed0-211">c.</span><span class="sxs-lookup"><span data-stu-id="24ed0-211">c.</span></span> <span data-ttu-id="24ed0-212">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="24ed0-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="24ed0-213">d.</span><span class="sxs-lookup"><span data-stu-id="24ed0-213">d.</span></span> <span data-ttu-id="24ed0-214">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="24ed0-214">Click **Create**.</span></span>
 
### <a name="creating-a-liquidfiles-test-user"></a><span data-ttu-id="24ed0-215">LiquidFiles test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="24ed0-215">Creating a LiquidFiles test user</span></span>

<span data-ttu-id="24ed0-216">Bu bölümde Hello amacı toocreate Britta Simon içinde LiquidFiles adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="24ed0-216">hello objective of this section is toocreate a user called Britta Simon in LiquidFiles.</span></span> <span data-ttu-id="24ed0-217">İle LiquidFiles Sunucu Yöneticisi tooget kendiniz tooyour LiquidFiles uygulama günlüğü önce bir kullanıcı olarak eklenmiş çalışır.</span><span class="sxs-lookup"><span data-stu-id="24ed0-217">Work with your LiquidFiles server administrator tooget yourself added as a user before logging in tooyour LiquidFiles application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="24ed0-218">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="24ed0-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="24ed0-219">Bu bölümde, erişim tooLiquidFiles vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="24ed0-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLiquidFiles.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="24ed0-221">**tooassign Britta Simon tooLiquidFiles hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="24ed0-221">**tooassign Britta Simon tooLiquidFiles, perform hello following steps:**</span></span>

1. <span data-ttu-id="24ed0-222">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="24ed0-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="24ed0-224">Merhaba uygulamalar listesinde **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="24ed0-224">In hello applications list, select **LiquidFiles**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_app.png) 

3. <span data-ttu-id="24ed0-226">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="24ed0-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="24ed0-228">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="24ed0-228">Click **Add** button.</span></span> <span data-ttu-id="24ed0-229">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="24ed0-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="24ed0-231">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="24ed0-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="24ed0-232">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="24ed0-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="24ed0-233">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="24ed0-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="24ed0-234">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="24ed0-234">Testing single sign-on</span></span>

<span data-ttu-id="24ed0-235">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="24ed0-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="24ed0-236">Hello erişim paneli LiquidFiles döşeme hello tıkladığınızda, otomatik olarak oturum açma LiquidFiles uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="24ed0-236">When you click hello LiquidFiles tile in hello Access Panel, you should get automatically signed-on tooyour LiquidFiles application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="24ed0-237">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="24ed0-237">Additional resources</span></span>

* [<span data-ttu-id="24ed0-238">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="24ed0-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="24ed0-239">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="24ed0-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_203.png

