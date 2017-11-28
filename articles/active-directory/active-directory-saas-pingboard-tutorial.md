---
title: "Öğretici: Azure Active Directory Tümleştirme ile Pingboard | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Pingboard arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 0a916b1f9ef32d8124aa11284d2115bb4fc0bbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="5585f-103">Öğretici: Azure Active Directory Tümleştirme Pingboard ile</span><span class="sxs-lookup"><span data-stu-id="5585f-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="5585f-104">Bu öğreticide, bilgi nasıl toointegrate Pingboard Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5585f-104">In this tutorial, you learn how toointegrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5585f-105">Pingboard Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="5585f-105">Integrating Pingboard with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5585f-106">Erişim tooPingboard sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5585f-106">You can control in Azure AD who has access tooPingboard</span></span>
- <span data-ttu-id="5585f-107">Kullanıcıların tooautomatically get açan tooPingboard (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5585f-107">You can enable your users tooautomatically get signed-on tooPingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5585f-108">Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5585f-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="5585f-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5585f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5585f-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5585f-110">Prerequisites</span></span>

<span data-ttu-id="5585f-111">tooconfigure Pingboard ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5585f-111">tooconfigure Azure AD integration with Pingboard, you need hello following items:</span></span>

- <span data-ttu-id="5585f-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="5585f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5585f-113">Bir Pingboard çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="5585f-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5585f-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="5585f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5585f-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="5585f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5585f-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5585f-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="5585f-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5585f-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5585f-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="5585f-118">Scenario description</span></span>
<span data-ttu-id="5585f-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="5585f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5585f-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="5585f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5585f-121">Merhaba Galerisi'nden Pingboard ekleme</span><span class="sxs-lookup"><span data-stu-id="5585f-121">Adding Pingboard from hello gallery</span></span>
2. <span data-ttu-id="5585f-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="5585f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-hello-gallery"></a><span data-ttu-id="5585f-123">Merhaba Galerisi'nden Pingboard ekleme</span><span class="sxs-lookup"><span data-stu-id="5585f-123">Adding Pingboard from hello gallery</span></span>
<span data-ttu-id="5585f-124">Azure AD'ye tooconfigure hello tümleştirme Pingboard, tooadd Pingboard hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="5585f-124">tooconfigure hello integration of Pingboard into Azure AD, you need tooadd Pingboard from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5585f-125">**tooadd Pingboard hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5585f-125">**tooadd Pingboard from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5585f-126">Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="5585f-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5585f-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="5585f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5585f-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5585f-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="5585f-131">Tıklatın **Ekle** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5585f-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="5585f-133">Merhaba arama kutusuna yazın **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="5585f-133">In hello search box, type **Pingboard**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="5585f-135">Merhaba Sonuçlar panelinde seçin **Pingboard**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="5585f-135">In hello results panel, select **Pingboard**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5585f-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="5585f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5585f-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Pingboard sınayın.</span><span class="sxs-lookup"><span data-stu-id="5585f-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5585f-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Pingboard içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="5585f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pingboard is tooa user in Azure AD.</span></span> <span data-ttu-id="5585f-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Pingboard hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="5585f-140">In other words, a link relationship between an Azure AD user and hello related user in Pingboard needs toobe established.</span></span>

<span data-ttu-id="5585f-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Pingboard içinde.</span><span class="sxs-lookup"><span data-stu-id="5585f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Pingboard.</span></span>

<span data-ttu-id="5585f-142">tooconfigure ve Pingboard ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5585f-142">tooconfigure and test Azure AD single sign-on with Pingboard, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5585f-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="5585f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5585f-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="5585f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5585f-145">**[Pingboard test kullanıcısı oluşturma](#creating-a-pingboard-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir Pingboard içinde Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="5585f-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - toohave a counterpart of Britta Simon in Pingboard that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="5585f-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="5585f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5585f-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="5585f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5585f-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5585f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5585f-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma Pingboard uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5585f-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="5585f-150">**tooconfigure Azure AD çoklu oturum açma ile Pingboard, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5585f-150">**tooconfigure Azure AD single sign-on with Pingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="5585f-151">Merhaba üzerinde hello Azure Yönetim Portalı'nda **Pingboard** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="5585f-151">In hello Azure Management portal, on hello **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="5585f-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="5585f-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="5585f-155">Merhaba üzerinde **Pingboard etki alanı ve URL'leri** bölümünde, hello tooconfigure hello uygulamada istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="5585f-155">On hello **Pingboard Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="5585f-157">a.</span><span class="sxs-lookup"><span data-stu-id="5585f-157">a.</span></span> <span data-ttu-id="5585f-158">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello değeri olarak:`http://<entity-id>.pingboard.com/sp`</span><span class="sxs-lookup"><span data-stu-id="5585f-158">In hello **Identifier** textbox, type hello value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="5585f-159">b.</span><span class="sxs-lookup"><span data-stu-id="5585f-159">b.</span></span> <span data-ttu-id="5585f-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<entity-id>.pingboard.com/auth/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="5585f-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5585f-161">Lütfen bu hello gerçek değerler olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="5585f-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="5585f-162">Tooupdate hello gerçek tanımlayıcısı ve yanıt URL'si ile bu değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="5585f-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="5585f-163">Burada, toouse hello benzersiz değerini hello tanımlayıcı dizesinde öneririz.</span><span class="sxs-lookup"><span data-stu-id="5585f-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="5585f-164">Kişi [Pingboard istemci destek ekibi](https://support.pingboard.com/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="5585f-164">Contact [Pingboard Client support team](https://support.pingboard.com/) tooget these values.</span></span> 

4. <span data-ttu-id="5585f-165">Denetleme **Göster Gelişmiş URL ayarları**, tooconfigure hello uygulamada istiyorsanız **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="5585f-165">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="5585f-167">a.</span><span class="sxs-lookup"><span data-stu-id="5585f-167">a.</span></span> <span data-ttu-id="5585f-168">Merhaba, **oturum açma URL'si** metin kutusuna, türü hello değeri olarak:`http://<sub-domain>.pingboard.com/sign_in`</span><span class="sxs-lookup"><span data-stu-id="5585f-168">In hello **Sign-on URL** textbox, type hello value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="5585f-169">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5585f-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="5585f-171">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5585f-171">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5585f-173">tooconfigure SSO Pingboard tarafında, yeni bir tarayıcı penceresi açın ve tooyour Pingboard hesap oturum.</span><span class="sxs-lookup"><span data-stu-id="5585f-173">tooconfigure SSO on Pingboard side, open a new browser window and log in tooyour Pingboard Account.</span></span> <span data-ttu-id="5585f-174">Üzerinde çoklu oturum açma yukarı Pingboard yönetici tooset olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5585f-174">You must be a Pingboard admin tooset up single sign on.</span></span>

8. <span data-ttu-id="5585f-175">Merhaba üst menüsünden seçin **uygulamaları > tümleştirmeler**</span><span class="sxs-lookup"><span data-stu-id="5585f-175">From hello top menu select **Apps > Integrations**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  <span data-ttu-id="5585f-177">Merhaba üzerinde **tümleştirmeler** sayfasında, hello Bul **"Azure Active Directory"** döşeme ve tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5585f-177">On hello **Integrations** page, find hello **"Azure Active Directory"** tile, and click it.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. <span data-ttu-id="5585f-179">Tıklatın izleyen hello kalıcı olarak **"Yapılandırma"**</span><span class="sxs-lookup"><span data-stu-id="5585f-179">In hello modal that follows click **"Configure"**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. <span data-ttu-id="5585f-181">Sayfa aşağıdaki hello üzerinde "Azure SSO tümleştirme etkin olduğunu." fark edeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="5585f-181">On hello following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="5585f-182">Açık hello indirilen bir not defteri ve Yapıştır hello içerik meta veri XML dosyasında **IDP meta verileri**.</span><span class="sxs-lookup"><span data-stu-id="5585f-182">Open hello downloaded Metadata XML file in a notepad and paste hello content in **IDP Metadata**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. <span data-ttu-id="5585f-184">Merhaba dosya doğrulanacak ve her şey doğruysa, çoklu oturum açma şimdi etkinleştirilir</span><span class="sxs-lookup"><span data-stu-id="5585f-184">hello file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5585f-185">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5585f-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="5585f-186">Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="5585f-186">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="5585f-188">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5585f-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5585f-189">Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="5585f-189">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5585f-191">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="5585f-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5585f-193">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5585f-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5585f-195">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5585f-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5585f-197">a.</span><span class="sxs-lookup"><span data-stu-id="5585f-197">a.</span></span> <span data-ttu-id="5585f-198">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5585f-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5585f-199">b.</span><span class="sxs-lookup"><span data-stu-id="5585f-199">b.</span></span> <span data-ttu-id="5585f-200">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="5585f-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5585f-201">c.</span><span class="sxs-lookup"><span data-stu-id="5585f-201">c.</span></span> <span data-ttu-id="5585f-202">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="5585f-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5585f-203">d.</span><span class="sxs-lookup"><span data-stu-id="5585f-203">d.</span></span> <span data-ttu-id="5585f-204">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5585f-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="5585f-205">Pingboard test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5585f-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="5585f-206">Pingboard içine sipariş tooenable Azure AD kullanıcıların toolog bunların Pingboard sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5585f-206">In order tooenable Azure AD users toolog into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="5585f-207">Pingboard Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="5585f-207">In hello case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="5585f-208">**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**</span><span class="sxs-lookup"><span data-stu-id="5585f-208">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="5585f-209">İçinde tooyour Pingboard şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5585f-209">Log in tooyour Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="5585f-210">Tıklatın **"Çalışan Ekle"** düğmesini **Directory** sayfası.</span><span class="sxs-lookup"><span data-stu-id="5585f-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="5585f-212">Merhaba üzerinde **"Çalışan Ekle"** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="5585f-212">On hello **“Add Employee”** dialog page, perform hello following steps.</span></span>

    ![Kişileri davet edin](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="5585f-214">a.</span><span class="sxs-lookup"><span data-stu-id="5585f-214">a.</span></span> <span data-ttu-id="5585f-215">Merhaba, **tam adı** metin kutusuna, tür Britta Simon hello tam adı.</span><span class="sxs-lookup"><span data-stu-id="5585f-215">In hello **Full Name** textbox, type hello full name of Britta Simon.</span></span>

    <span data-ttu-id="5585f-216">b.</span><span class="sxs-lookup"><span data-stu-id="5585f-216">b.</span></span> <span data-ttu-id="5585f-217">Merhaba, **e-posta** metin kutusuna, Britta Simon hesabının hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="5585f-217">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="5585f-218">c.</span><span class="sxs-lookup"><span data-stu-id="5585f-218">c.</span></span> <span data-ttu-id="5585f-219">Merhaba, **iş unvanı** metin kutusuna, Britta Simon türü hello iş unvanı.</span><span class="sxs-lookup"><span data-stu-id="5585f-219">In hello **Job Title** textbox, type hello job title of Britta Simon.</span></span>

    <span data-ttu-id="5585f-220">d.</span><span class="sxs-lookup"><span data-stu-id="5585f-220">d.</span></span> <span data-ttu-id="5585f-221">Merhaba, **konumu** açılan listesinde, Britta Simon select başlangıç konumu.</span><span class="sxs-lookup"><span data-stu-id="5585f-221">In hello **Location** dropdown, select hello location  of Britta Simon.</span></span>
    
    <span data-ttu-id="5585f-222">e.</span><span class="sxs-lookup"><span data-stu-id="5585f-222">e.</span></span> <span data-ttu-id="5585f-223">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5585f-223">Click **Add**.</span></span>   

4. <span data-ttu-id="5585f-224">Bir onay ekranı tooconfirm hello eklenmesi kullanıcı gelecektir.</span><span class="sxs-lookup"><span data-stu-id="5585f-224">A confirmation screen will come up tooconfirm hello addition of user.</span></span>
    
    ![Onayla](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="5585f-226">Hello Azure Active Directory hesap sahibi bir e-posta almak ve bunu etkinleştirilmeden önce bağlantı tooconfirm hesaplarında izleyin.</span><span class="sxs-lookup"><span data-stu-id="5585f-226">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5585f-227">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="5585f-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5585f-228">Bu bölümde, kendi erişim tooPingboard vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5585f-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPingboard.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="5585f-230">**tooassign Britta Simon tooPingboard hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5585f-230">**tooassign Britta Simon tooPingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="5585f-231">Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5585f-231">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="5585f-233">Merhaba uygulamalar listesinde **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="5585f-233">In hello applications list, select **Pingboard**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="5585f-235">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="5585f-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="5585f-237">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5585f-237">Click **Add** button.</span></span> <span data-ttu-id="5585f-238">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5585f-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="5585f-240">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="5585f-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5585f-241">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5585f-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5585f-242">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5585f-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5585f-243">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="5585f-243">Testing single sign-on</span></span>

<span data-ttu-id="5585f-244">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="5585f-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5585f-245">Merhaba Pingboard hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Pingboard uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5585f-245">When you click hello Pingboard tile in hello Access Panel, you should get automatically signed-on tooyour Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5585f-246">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="5585f-246">Additional resources</span></span>

* [<span data-ttu-id="5585f-247">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="5585f-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5585f-248">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="5585f-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
