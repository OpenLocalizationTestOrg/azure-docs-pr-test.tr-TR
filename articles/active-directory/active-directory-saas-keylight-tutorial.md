---
title: "Öğretici: Azure Active Directory Tümleştirme ile LockPath Keylight | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile LockPath Keylight arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 5485aeb068ba6fbdb4ea9bfc89d401e00c5b1d29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a><span data-ttu-id="e9eac-103">Öğretici: Azure Active Directory Tümleştirme LockPath Keylight ile</span><span class="sxs-lookup"><span data-stu-id="e9eac-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span></span>

<span data-ttu-id="e9eac-104">Bu öğreticide, bilgi nasıl toointegrate LockPath Keylight Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e9eac-104">In this tutorial, you learn how toointegrate LockPath Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e9eac-105">LockPath Keylight Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e9eac-105">Integrating LockPath Keylight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e9eac-106">Erişim tooLockPath Keylight sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e9eac-106">You can control in Azure AD who has access tooLockPath Keylight</span></span>
- <span data-ttu-id="e9eac-107">Kullanıcıların tooautomatically get açan tooLockPath Keylight (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e9eac-107">You can enable your users tooautomatically get signed-on tooLockPath Keylight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e9eac-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="e9eac-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e9eac-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e9eac-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9eac-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e9eac-110">Prerequisites</span></span>

<span data-ttu-id="e9eac-111">tooconfigure LockPath Keylight ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e9eac-111">tooconfigure Azure AD integration with LockPath Keylight, you need hello following items:</span></span>

- <span data-ttu-id="e9eac-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e9eac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e9eac-113">Bir LockPath Keylight çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="e9eac-113">A LockPath Keylight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e9eac-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e9eac-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e9eac-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="e9eac-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e9eac-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e9eac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e9eac-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9eac-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e9eac-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e9eac-118">Scenario description</span></span>
<span data-ttu-id="e9eac-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e9eac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e9eac-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e9eac-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e9eac-121">Merhaba Galerisi'nden LockPath Keylight ekleme</span><span class="sxs-lookup"><span data-stu-id="e9eac-121">Adding LockPath Keylight from hello gallery</span></span>
2. <span data-ttu-id="e9eac-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e9eac-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lockpath-keylight-from-hello-gallery"></a><span data-ttu-id="e9eac-123">Merhaba Galerisi'nden LockPath Keylight ekleme</span><span class="sxs-lookup"><span data-stu-id="e9eac-123">Adding LockPath Keylight from hello gallery</span></span>
<span data-ttu-id="e9eac-124">Azure AD'ye tooconfigure hello tümleştirme LockPath Keylight, tooadd LockPath Keylight hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9eac-124">tooconfigure hello integration of LockPath Keylight into Azure AD, you need tooadd LockPath Keylight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e9eac-125">**tooadd LockPath Keylight hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e9eac-125">**tooadd LockPath Keylight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9eac-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e9eac-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e9eac-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e9eac-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="e9eac-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e9eac-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="e9eac-133">Merhaba arama kutusuna yazın **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-133">In hello search box, type **LockPath Keylight**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. <span data-ttu-id="e9eac-135">Merhaba Sonuçlar panelinde seçin **LockPath Keylight**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e9eac-135">In hello results panel, select **LockPath Keylight**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e9eac-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e9eac-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e9eac-138">Bu bölümde, yapılandırmanız ve LockPath Keylight ile Azure AD çoklu oturum açmayı test "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="e9eac-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e9eac-139">Tek toowork'ın oturum açma hangi hello karşılık gelen LockPath Keylight içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9eac-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LockPath Keylight is tooa user in Azure AD.</span></span> <span data-ttu-id="e9eac-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı LockPath Keylight hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9eac-140">In other words, a link relationship between an Azure AD user and hello related user in LockPath Keylight needs toobe established.</span></span>

<span data-ttu-id="e9eac-141">Merhaba hello değeri LockPath Keylight içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="e9eac-141">In LockPath Keylight, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e9eac-142">tooconfigure ve LockPath Keylight ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e9eac-142">tooconfigure and test Azure AD single sign-on with LockPath Keylight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e9eac-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="e9eac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e9eac-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="e9eac-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e9eac-145">**[LockPath Keylight test kullanıcısı oluşturma](#creating-a-lockpath-keylight-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir LockPath Keylight içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="e9eac-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - toohave a counterpart of Britta Simon in LockPath Keylight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e9eac-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e9eac-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e9eac-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="e9eac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e9eac-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e9eac-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e9eac-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma LockPath Keylight uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e9eac-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LockPath Keylight application.</span></span>

<span data-ttu-id="e9eac-150">**tooconfigure Azure AD çoklu oturum açma LockPath Keylight ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e9eac-150">**tooconfigure Azure AD single sign-on with LockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9eac-151">Hello hello üzerinde Azure portal'ın **LockPath Keylight** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-151">In hello Azure portal, on hello **LockPath Keylight** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="e9eac-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e9eac-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. <span data-ttu-id="e9eac-155">Merhaba üzerinde **LockPath Keylight etki alanı ve URL'leri** bölümünde, aşağıdaki adımları hello gerçekleştirmek::</span><span class="sxs-lookup"><span data-stu-id="e9eac-155">On hello **LockPath Keylight Domain and URLs** section, perform hello following steps::</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    <span data-ttu-id="e9eac-157">a.</span><span class="sxs-lookup"><span data-stu-id="e9eac-157">a.</span></span> <span data-ttu-id="e9eac-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.keylightgrc.com/`</span><span class="sxs-lookup"><span data-stu-id="e9eac-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/`</span></span>

    <span data-ttu-id="e9eac-159">b.</span><span class="sxs-lookup"><span data-stu-id="e9eac-159">b.</span></span> <span data-ttu-id="e9eac-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.keylightgrc.com`</span><span class="sxs-lookup"><span data-stu-id="e9eac-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com`</span></span>

    <span data-ttu-id="e9eac-161">c.</span><span class="sxs-lookup"><span data-stu-id="e9eac-161">c.</span></span> <span data-ttu-id="e9eac-162">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.keylightgrc.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="e9eac-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="e9eac-163">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="e9eac-163">These values are not real.</span></span> <span data-ttu-id="e9eac-164">Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="e9eac-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="e9eac-165">Kişi [LockPath Keylight istemci destek ekibi](https://www.lockpath.com/contact/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="e9eac-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="e9eac-166">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Raw)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e9eac-166">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. <span data-ttu-id="e9eac-168">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e9eac-168">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="e9eac-170">Merhaba üzerinde **LockPath Keylight yapılandırma** 'yi tıklatın **yapılandırma LockPath Keylight** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e9eac-170">On hello **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e9eac-171">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="e9eac-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. <span data-ttu-id="e9eac-173">tooenable LockPath Keylight SSO hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e9eac-173">tooenable SSO in LockPath Keylight, perform hello following steps:</span></span>
   
    <span data-ttu-id="e9eac-174">a.</span><span class="sxs-lookup"><span data-stu-id="e9eac-174">a.</span></span> <span data-ttu-id="e9eac-175">Oturum açma LockPath Keylight hesabı yönetici olarak tooyour.</span><span class="sxs-lookup"><span data-stu-id="e9eac-175">Sign-on tooyour LockPath Keylight account as administrator.</span></span>
    
    <span data-ttu-id="e9eac-176">b.</span><span class="sxs-lookup"><span data-stu-id="e9eac-176">b.</span></span> <span data-ttu-id="e9eac-177">Hello içinde hello üst menüsünde **kişi**seçip **Keylight Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-177">In hello menu on hello top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/401.png) 

    <span data-ttu-id="e9eac-179">c.</span><span class="sxs-lookup"><span data-stu-id="e9eac-179">c.</span></span> <span data-ttu-id="e9eac-180">Merhaba soldaki Hello treeview içinde tıklatın **SAML**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-180">In hello treeview on hello left, click **SAML**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/402.png) 

    <span data-ttu-id="e9eac-182">d.</span><span class="sxs-lookup"><span data-stu-id="e9eac-182">d.</span></span> <span data-ttu-id="e9eac-183">Merhaba üzerinde **SAML ayarları** iletişim kutusunda, tıklatın **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-183">On hello **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/404.png) 

8. <span data-ttu-id="e9eac-185">Merhaba üzerinde **SAML ayarlarını Düzenle** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e9eac-185">On hello **Edit SAML Settings** dialog page, perform hello following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    <span data-ttu-id="e9eac-187">a.</span><span class="sxs-lookup"><span data-stu-id="e9eac-187">a.</span></span> <span data-ttu-id="e9eac-188">Ayarlama **SAML kimlik doğrulaması** çok**etkin**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-188">Set **SAML authentication** too**Active**.</span></span>

    <span data-ttu-id="e9eac-189">b.</span><span class="sxs-lookup"><span data-stu-id="e9eac-189">b.</span></span> <span data-ttu-id="e9eac-190">Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** hello hello Azure portal ' kopyaladığınız değeri **kimlik sağlayıcısı oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="e9eac-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="e9eac-191">c.</span><span class="sxs-lookup"><span data-stu-id="e9eac-191">c.</span></span> <span data-ttu-id="e9eac-192">Yapıştır hello **tek Sign-Out hizmeti URL'si** hello hello Azure portal ' kopyaladığınız değeri **kimlik sağlayıcısı oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="e9eac-192">Paste hello **Single Sign-Out Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="e9eac-193">d.</span><span class="sxs-lookup"><span data-stu-id="e9eac-193">d.</span></span> <span data-ttu-id="e9eac-194">Tıklatın **Dosya Seç** tooselect indirilen LockPath Keylight sertifika ve ardından **açık** tooupload hello sertifika.</span><span class="sxs-lookup"><span data-stu-id="e9eac-194">Click **Choose File** tooselect your downloaded LockPath Keylight certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="e9eac-195">e.</span><span class="sxs-lookup"><span data-stu-id="e9eac-195">e.</span></span> <span data-ttu-id="e9eac-196">Ayarlama **SAML kullanıcı kimliği konumu** çok**NameIdentifier öğesi hello konu deyiminin**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-196">Set **SAML User Id location** too**NameIdentifier element of hello subject statement**.</span></span>
    
    <span data-ttu-id="e9eac-197">f.</span><span class="sxs-lookup"><span data-stu-id="e9eac-197">f.</span></span> <span data-ttu-id="e9eac-198">Merhaba sağlamak **Keylight hizmet sağlayıcısı** desen aşağıdaki hello kullanarak: **https://&lt;ŞirketAdı&gt;. keylightgrc.com**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-198">Provide hello **Keylight Service Provider** using hello following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span></span>
    
    <span data-ttu-id="e9eac-199">g.</span><span class="sxs-lookup"><span data-stu-id="e9eac-199">g.</span></span> <span data-ttu-id="e9eac-200">Ayarlama **otomatik sağlama kullanıcılar** çok**etkin**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-200">Set **Auto-provision users** too**Active**.</span></span>

    <span data-ttu-id="e9eac-201">h.</span><span class="sxs-lookup"><span data-stu-id="e9eac-201">h.</span></span> <span data-ttu-id="e9eac-202">Ayarlama **otomatik sağlama hesap türü** çok**tam kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-202">Set **Auto-provision account type** too**Full User**.</span></span>

    <span data-ttu-id="e9eac-203">ı.</span><span class="sxs-lookup"><span data-stu-id="e9eac-203">i.</span></span> <span data-ttu-id="e9eac-204">Ayarlama **otomatik sağlama güvenlik rolü**seçin **SAML sahip standart kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span></span>
    
    <span data-ttu-id="e9eac-205">j.</span><span class="sxs-lookup"><span data-stu-id="e9eac-205">j.</span></span> <span data-ttu-id="e9eac-206">Ayarlama **otomatik sağlama güvenlik config**seçin **standart kullanıcı yapılandırması**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span></span>
     
    <span data-ttu-id="e9eac-207">k.</span><span class="sxs-lookup"><span data-stu-id="e9eac-207">k.</span></span> <span data-ttu-id="e9eac-208">Merhaba, **e-posta özniteliği** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="e9eac-208">In hello **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="e9eac-209">l.</span><span class="sxs-lookup"><span data-stu-id="e9eac-209">l.</span></span> <span data-ttu-id="e9eac-210">Merhaba, **ad özniteliği** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="e9eac-210">In hello **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="e9eac-211">m.</span><span class="sxs-lookup"><span data-stu-id="e9eac-211">m.</span></span> <span data-ttu-id="e9eac-212">Merhaba, **son name özniteliği** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="e9eac-212">In hello **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
    
    <span data-ttu-id="e9eac-213">n.</span><span class="sxs-lookup"><span data-stu-id="e9eac-213">n.</span></span> <span data-ttu-id="e9eac-214">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e9eac-214">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e9eac-215">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e9eac-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e9eac-216">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="e9eac-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e9eac-217">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e9eac-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e9eac-218">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e9eac-218">Creating an Azure AD test user</span></span>
<span data-ttu-id="e9eac-219">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="e9eac-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="e9eac-221">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e9eac-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9eac-222">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e9eac-222">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e9eac-224">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-224">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e9eac-226">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="e9eac-226">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e9eac-228">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e9eac-228">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e9eac-230">a.</span><span class="sxs-lookup"><span data-stu-id="e9eac-230">a.</span></span> <span data-ttu-id="e9eac-231">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-231">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e9eac-232">b.</span><span class="sxs-lookup"><span data-stu-id="e9eac-232">b.</span></span> <span data-ttu-id="e9eac-233">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="e9eac-233">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e9eac-234">c.</span><span class="sxs-lookup"><span data-stu-id="e9eac-234">c.</span></span> <span data-ttu-id="e9eac-235">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-235">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e9eac-236">d.</span><span class="sxs-lookup"><span data-stu-id="e9eac-236">d.</span></span> <span data-ttu-id="e9eac-237">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e9eac-237">Click **Create**.</span></span>
 
### <a name="creating-a-lockpath-keylight-test-user"></a><span data-ttu-id="e9eac-238">LockPath Keylight test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e9eac-238">Creating a LockPath Keylight test user</span></span>

<span data-ttu-id="e9eac-239">Bu bölümde, Britta Simon LockPath Keylight adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e9eac-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span></span> <span data-ttu-id="e9eac-240">LockPath Keylight tam zamanı sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="e9eac-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="e9eac-241">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="e9eac-241">There is no action item for you in this section.</span></span> <span data-ttu-id="e9eac-242">Yeni bir kullanıcı hello kullanıcı henüz yoksa LockPath Keylight erişirken oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e9eac-242">A new user is created when accessing LockPath Keylight if hello user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="e9eac-243">Toocreate kullanıcı el ile gerekiyorsa, toocontact hello gereksinim [LockPath Keylight istemci destek ekibi](https://www.lockpath.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="e9eac-243">If you need toocreate a user manually, you need toocontact hello [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e9eac-244">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="e9eac-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e9eac-245">Bu bölümde, erişim tooLockPath Keylight vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e9eac-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLockPath Keylight.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="e9eac-247">**tooassign Britta Simon tooLockPath Keylight, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e9eac-247">**tooassign Britta Simon tooLockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9eac-248">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e9eac-250">Merhaba uygulamalar listesinde **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-250">In hello applications list, select **LockPath Keylight**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. <span data-ttu-id="e9eac-252">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e9eac-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="e9eac-254">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e9eac-254">Click **Add** button.</span></span> <span data-ttu-id="e9eac-255">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e9eac-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="e9eac-257">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e9eac-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e9eac-258">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e9eac-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e9eac-259">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e9eac-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e9eac-260">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e9eac-260">Testing single sign-on</span></span>

<span data-ttu-id="e9eac-261">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="e9eac-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e9eac-262">LockPath Keylight döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma LockPath Keylight uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9eac-262">When you click hello LockPath Keylight tile in hello Access Panel, you should get automatically signed-on tooyour LockPath Keylight application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e9eac-263">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e9eac-263">Additional resources</span></span>

* [<span data-ttu-id="e9eac-264">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="e9eac-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e9eac-265">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e9eac-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

