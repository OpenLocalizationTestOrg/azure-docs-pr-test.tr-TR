---
title: "Öğretici: Azure Active Directory Tümleştirme Origamisi ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Origamisi arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: a45f2d2b8d2271cf0fc58cb8fad92f007cb5e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a><span data-ttu-id="f032e-103">Öğretici: Azure Active Directory Tümleştirme ile Origamisi</span><span class="sxs-lookup"><span data-stu-id="f032e-103">Tutorial: Azure Active Directory integration with Origami</span></span>

<span data-ttu-id="f032e-104">Bu öğreticide, bilgi nasıl toointegrate Origamisi Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f032e-104">In this tutorial, you learn how toointegrate Origami with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f032e-105">Origamisi Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="f032e-105">Integrating Origami with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f032e-106">Erişim tooOrigami sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f032e-106">You can control in Azure AD who has access tooOrigami</span></span>
- <span data-ttu-id="f032e-107">Kullanıcıların tooautomatically get açan tooOrigami (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f032e-107">You can enable your users tooautomatically get signed-on tooOrigami (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f032e-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="f032e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f032e-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f032e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f032e-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f032e-110">Prerequisites</span></span>

<span data-ttu-id="f032e-111">tooconfigure Origamisi ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="f032e-111">tooconfigure Azure AD integration with Origami, you need hello following items:</span></span>

- <span data-ttu-id="f032e-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="f032e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f032e-113">Bir Origamisi çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="f032e-113">An Origami single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f032e-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="f032e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f032e-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="f032e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f032e-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="f032e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f032e-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f032e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f032e-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="f032e-118">Scenario description</span></span>
<span data-ttu-id="f032e-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="f032e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f032e-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="f032e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f032e-121">Merhaba Galerisi'nden Origamisi ekleme</span><span class="sxs-lookup"><span data-stu-id="f032e-121">Adding Origami from hello gallery</span></span>
2. <span data-ttu-id="f032e-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f032e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-origami-from-hello-gallery"></a><span data-ttu-id="f032e-123">Merhaba Galerisi'nden Origamisi ekleme</span><span class="sxs-lookup"><span data-stu-id="f032e-123">Adding Origami from hello gallery</span></span>
<span data-ttu-id="f032e-124">Azure AD'ye tooconfigure hello tümleştirme Origamisi, tooadd Origamisi hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="f032e-124">tooconfigure hello integration of Origami into Azure AD, you need tooadd Origami from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f032e-125">**tooadd Origamisi hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f032e-125">**tooadd Origami from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f032e-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f032e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f032e-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="f032e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f032e-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f032e-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="f032e-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f032e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="f032e-133">Merhaba arama kutusuna yazın **Origamisi**.</span><span class="sxs-lookup"><span data-stu-id="f032e-133">In hello search box, type **Origami**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. <span data-ttu-id="f032e-135">Merhaba Sonuçlar panelinde seçin **Origamisi**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="f032e-135">In hello results panel, select **Origami**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f032e-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f032e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f032e-138">Bu bölümde, yapılandırmak ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Origamisi sınayın.</span><span class="sxs-lookup"><span data-stu-id="f032e-138">In this section, you configure and test Azure AD single sign-on with Origami based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f032e-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Origamisi içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="f032e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Origami is tooa user in Azure AD.</span></span> <span data-ttu-id="f032e-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Origamisi hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="f032e-140">In other words, a link relationship between an Azure AD user and hello related user in Origami needs toobe established.</span></span>

<span data-ttu-id="f032e-141">Merhaba hello değeri Origamisi içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="f032e-141">In Origami, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f032e-142">tooconfigure ve Origamisi ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="f032e-142">tooconfigure and test Azure AD single sign-on with Origami, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f032e-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="f032e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f032e-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="f032e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f032e-145">**[Bir Origamisi test kullanıcısı oluşturma](#creating-an-origami-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Origamisi içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="f032e-145">**[Creating an Origami test user](#creating-an-origami-test-user)** - toohave a counterpart of Britta Simon in Origami that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f032e-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="f032e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f032e-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="f032e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f032e-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f032e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f032e-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Origamisi uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f032e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Origami application.</span></span>

<span data-ttu-id="f032e-150">**tooconfigure Azure AD çoklu oturum açma ile Origamisi, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f032e-150">**tooconfigure Azure AD single sign-on with Origami, perform hello following steps:**</span></span>

1. <span data-ttu-id="f032e-151">Merhaba hello üzerinde Azure portal'ın **Origamisi** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="f032e-151">In hello Azure portal, on hello **Origami** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="f032e-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="f032e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. <span data-ttu-id="f032e-155">Merhaba üzerinde **Origamisi etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f032e-155">On hello **Origami Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    <span data-ttu-id="f032e-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://live.origamirisk.com/origami/account/login?account=<companyname>`</span><span class="sxs-lookup"><span data-stu-id="f032e-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f032e-158">Merhaba değeri gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="f032e-158">hello value is not real.</span></span> <span data-ttu-id="f032e-159">Güncelleştirme hello değerle hello gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="f032e-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="f032e-160">Kişi [Origamisi istemci destek ekibi](https://wordpress.org/support/theme/origami) tooget hello değeri.</span><span class="sxs-lookup"><span data-stu-id="f032e-160">Contact [Origami Client support team](https://wordpress.org/support/theme/origami) tooget hello value.</span></span> 
 
4. <span data-ttu-id="f032e-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f032e-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. <span data-ttu-id="f032e-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f032e-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f032e-165">Merhaba üzerinde **Origamisi yapılandırma** 'yi tıklatın **yapılandırma Origamisi** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="f032e-165">On hello **Origami Configuration** section, click **Configure Origami** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f032e-166">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="f032e-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. <span data-ttu-id="f032e-168">İçinde toohello Origamisi hesabı yönetici haklarıyla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f032e-168">Log in toohello Origami account with Admin rights.</span></span>

8. <span data-ttu-id="f032e-169">Hello içinde hello üst menüsünde **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="f032e-169">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. <span data-ttu-id="f032e-171">Merhaba üzerinde tek oturum Kurulumu iletişim sayfasında hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f032e-171">On hello Single Sign On Setup dialog page, perform hello following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    <span data-ttu-id="f032e-173">a.</span><span class="sxs-lookup"><span data-stu-id="f032e-173">a.</span></span> <span data-ttu-id="f032e-174">Seçin **etkinleştirmek çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="f032e-174">Select **Enable Single Sign On**.</span></span>

    <span data-ttu-id="f032e-175">b.</span><span class="sxs-lookup"><span data-stu-id="f032e-175">b.</span></span> <span data-ttu-id="f032e-176">Merhaba, **kimlik sağlayıcısının oturum açma sayfası URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="f032e-176">In hello **Identity Provider's Sign-in Page URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f032e-177">c.</span><span class="sxs-lookup"><span data-stu-id="f032e-177">c.</span></span> <span data-ttu-id="f032e-178">Merhaba, **kimlik sağlayıcısının Sign-out sayfa URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="f032e-178">In hello **Identity Provider's Sign-out Page URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f032e-179">d.</span><span class="sxs-lookup"><span data-stu-id="f032e-179">d.</span></span> <span data-ttu-id="f032e-180">Tıklatın **Gözat** tooupload hello sertifika hello Azure portal ' indirilir.</span><span class="sxs-lookup"><span data-stu-id="f032e-180">Click **Browse** tooupload hello certificate you have downloaded from hello Azure portal.</span></span>

    <span data-ttu-id="f032e-181">e.</span><span class="sxs-lookup"><span data-stu-id="f032e-181">e.</span></span> <span data-ttu-id="f032e-182">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="f032e-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="f032e-183">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="f032e-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f032e-184">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="f032e-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f032e-185">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f032e-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f032e-186">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f032e-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="f032e-187">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="f032e-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="f032e-189">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f032e-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f032e-190">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f032e-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f032e-192">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f032e-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f032e-194">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="f032e-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f032e-196">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f032e-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f032e-198">a.</span><span class="sxs-lookup"><span data-stu-id="f032e-198">a.</span></span> <span data-ttu-id="f032e-199">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f032e-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f032e-200">b.</span><span class="sxs-lookup"><span data-stu-id="f032e-200">b.</span></span> <span data-ttu-id="f032e-201">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="f032e-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f032e-202">c.</span><span class="sxs-lookup"><span data-stu-id="f032e-202">c.</span></span> <span data-ttu-id="f032e-203">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="f032e-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f032e-204">d.</span><span class="sxs-lookup"><span data-stu-id="f032e-204">d.</span></span> <span data-ttu-id="f032e-205">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f032e-205">Click **Create**.</span></span>
 
### <a name="creating-an-origami-test-user"></a><span data-ttu-id="f032e-206">Bir Origamisi test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f032e-206">Creating an Origami test user</span></span>

<span data-ttu-id="f032e-207">Bu bölümde, içinde Origamisi Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f032e-207">In this section, you create a user called Britta Simon in Origami.</span></span> 

1. <span data-ttu-id="f032e-208">İçinde toohello Origamisi hesabı yönetici haklarıyla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f032e-208">Log in toohello Origami account with Admin rights.</span></span>

2. <span data-ttu-id="f032e-209">Hello içinde hello üst menüsünde **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="f032e-209">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. <span data-ttu-id="f032e-211">Merhaba üzerinde **kullanıcılar ve güvenlik** iletişim kutusunda, tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f032e-211">On hello **Users and Security** dialog, click **Users**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. <span data-ttu-id="f032e-213">Tıklatın **yeni kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="f032e-213">Click **Add New User**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. <span data-ttu-id="f032e-215">Merhaba yeni kullanıcı Ekle iletişim kutusunda hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f032e-215">On hello Add New User dialog, perform hello following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    <span data-ttu-id="f032e-217">a.</span><span class="sxs-lookup"><span data-stu-id="f032e-217">a.</span></span> <span data-ttu-id="f032e-218">Merhaba, **kullanıcı adı** metin kutusuna, bir kullanıcı gibi hello e-posta girin  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="f032e-218">In hello **User Name** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="f032e-219">b.</span><span class="sxs-lookup"><span data-stu-id="f032e-219">b.</span></span> <span data-ttu-id="f032e-220">Merhaba, **parola** metin kutusuna, bir parola yazın.</span><span class="sxs-lookup"><span data-stu-id="f032e-220">In hello **Password** textbox, type a password.</span></span>

    <span data-ttu-id="f032e-221">c.</span><span class="sxs-lookup"><span data-stu-id="f032e-221">c.</span></span> <span data-ttu-id="f032e-222">Merhaba, **parolayı onayla** metin kutusuna, hello parolayı yeniden girin.</span><span class="sxs-lookup"><span data-stu-id="f032e-222">In hello **Confirm Password** textbox, type hello password again.</span></span>

    <span data-ttu-id="f032e-223">d.</span><span class="sxs-lookup"><span data-stu-id="f032e-223">d.</span></span> <span data-ttu-id="f032e-224">Merhaba, **ad** metin kutusuna, hello ilk gibi kullanıcı adını girin **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f032e-224">In hello **First Name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="f032e-225">e.</span><span class="sxs-lookup"><span data-stu-id="f032e-225">e.</span></span> <span data-ttu-id="f032e-226">Merhaba, **Soyadı** metin kutusuna, hello son gibi kullanıcı adını girin **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f032e-226">In hello **Last Name** textbox, enter hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="f032e-227">f.</span><span class="sxs-lookup"><span data-stu-id="f032e-227">f.</span></span> <span data-ttu-id="f032e-228">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f032e-228">Click **Save**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. <span data-ttu-id="f032e-230">Ata **kullanıcı rolleri** ve **istemci erişimi** toohello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="f032e-230">Assign **User Roles** and **Client Access** toohello user.</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f032e-232">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="f032e-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f032e-233">Bu bölümde, erişim tooOrigami vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f032e-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOrigami.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="f032e-235">**tooassign Britta Simon tooOrigami hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f032e-235">**tooassign Britta Simon tooOrigami, perform hello following steps:**</span></span>

1. <span data-ttu-id="f032e-236">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f032e-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="f032e-238">Merhaba uygulamalar listesinde **Origamisi**.</span><span class="sxs-lookup"><span data-stu-id="f032e-238">In hello applications list, select **Origami**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. <span data-ttu-id="f032e-240">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="f032e-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="f032e-242">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f032e-242">Click **Add** button.</span></span> <span data-ttu-id="f032e-243">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f032e-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="f032e-245">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="f032e-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f032e-246">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f032e-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f032e-247">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f032e-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f032e-248">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="f032e-248">Testing single sign-on</span></span>

<span data-ttu-id="f032e-249">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="f032e-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f032e-250">Merhaba Origamisi hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Origamisi uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f032e-250">When you click hello Origami tile in hello Access Panel, you should get automatically signed-on tooyour Origami application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f032e-251">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f032e-251">Additional resources</span></span>

* [<span data-ttu-id="f032e-252">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="f032e-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f032e-253">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="f032e-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png

