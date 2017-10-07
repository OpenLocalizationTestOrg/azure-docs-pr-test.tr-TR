---
title: "Öğretici: Azure Active Directory Tümleştirme ile PostBeyond | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile PostBeyond arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 09992f08-ec50-4472-997f-ccbe719039e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 38019fd24a603732e91a1b5f7bfed5ab4edb017f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-postbeyond"></a><span data-ttu-id="c81d9-103">Öğretici: Azure Active Directory Tümleştirme PostBeyond ile</span><span class="sxs-lookup"><span data-stu-id="c81d9-103">Tutorial: Azure Active Directory integration with PostBeyond</span></span>

<span data-ttu-id="c81d9-104">Bu öğreticide, bilgi nasıl toointegrate PostBeyond Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c81d9-104">In this tutorial, you learn how toointegrate PostBeyond with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c81d9-105">PostBeyond Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="c81d9-105">Integrating PostBeyond with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c81d9-106">Erişim tooPostBeyond sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c81d9-106">You can control in Azure AD who has access tooPostBeyond</span></span>
- <span data-ttu-id="c81d9-107">Kullanıcıların tooautomatically get açan tooPostBeyond (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c81d9-107">You can enable your users tooautomatically get signed-on tooPostBeyond (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c81d9-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="c81d9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c81d9-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c81d9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c81d9-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c81d9-110">Prerequisites</span></span>

<span data-ttu-id="c81d9-111">tooconfigure PostBeyond ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c81d9-111">tooconfigure Azure AD integration with PostBeyond, you need hello following items:</span></span>

- <span data-ttu-id="c81d9-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="c81d9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c81d9-113">Bir PostBeyond çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="c81d9-113">A PostBeyond single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c81d9-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="c81d9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c81d9-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="c81d9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c81d9-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c81d9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c81d9-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c81d9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c81d9-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="c81d9-118">Scenario description</span></span>
<span data-ttu-id="c81d9-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="c81d9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c81d9-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="c81d9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c81d9-121">Merhaba Galerisi'nden PostBeyond ekleme</span><span class="sxs-lookup"><span data-stu-id="c81d9-121">Adding PostBeyond from hello gallery</span></span>
2. <span data-ttu-id="c81d9-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c81d9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-postbeyond-from-hello-gallery"></a><span data-ttu-id="c81d9-123">Merhaba Galerisi'nden PostBeyond ekleme</span><span class="sxs-lookup"><span data-stu-id="c81d9-123">Adding PostBeyond from hello gallery</span></span>
<span data-ttu-id="c81d9-124">Azure AD'ye PostBeyond tooconfigure hello tümleştirilmesi, tooadd PostBeyond hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="c81d9-124">tooconfigure hello integration of PostBeyond into Azure AD, you need tooadd PostBeyond from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c81d9-125">**tooadd PostBeyond hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c81d9-125">**tooadd PostBeyond from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c81d9-126">Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c81d9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c81d9-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="c81d9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c81d9-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c81d9-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="c81d9-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c81d9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="c81d9-133">Merhaba arama kutusuna yazın **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="c81d9-133">In hello search box, type **PostBeyond**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_search.png)

5. <span data-ttu-id="c81d9-135">Merhaba Sonuçlar panelinde seçin **PostBeyond**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="c81d9-135">In hello results panel, select **PostBeyond**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c81d9-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c81d9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c81d9-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı PostBeyond sınayın.</span><span class="sxs-lookup"><span data-stu-id="c81d9-138">In this section, you configure and test Azure AD single sign-on with PostBeyond based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c81d9-139">Tek toowork'ın oturum açma hangi hello karşılık gelen PostBeyond içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="c81d9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PostBeyond is tooa user in Azure AD.</span></span> <span data-ttu-id="c81d9-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı PostBeyond hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="c81d9-140">In other words, a link relationship between an Azure AD user and hello related user in PostBeyond needs toobe established.</span></span>

<span data-ttu-id="c81d9-141">Merhaba hello değeri PostBeyond içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="c81d9-141">In PostBeyond, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c81d9-142">tooconfigure ve PostBeyond ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c81d9-142">tooconfigure and test Azure AD single sign-on with PostBeyond, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c81d9-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="c81d9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c81d9-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="c81d9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c81d9-145">**[PostBeyond test kullanıcısı oluşturma](#creating-a-postbeyond-test-user) ** -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir PostBeyond içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="c81d9-145">**[Creating a PostBeyond test user](#creating-a-postbeyond-test-user)** - toohave a counterpart of Britta Simon in PostBeyond that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c81d9-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="c81d9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c81d9-147">**[Çoklu oturum açmayı test](#testing-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="c81d9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c81d9-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c81d9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c81d9-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma PostBeyond uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c81d9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PostBeyond application.</span></span>

<span data-ttu-id="c81d9-150">**tooconfigure Azure AD çoklu oturum açma ile PostBeyond, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c81d9-150">**tooconfigure Azure AD single sign-on with PostBeyond, perform hello following steps:**</span></span>

1. <span data-ttu-id="c81d9-151">Hello hello üzerinde Azure portal'ın **PostBeyond** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c81d9-151">In hello Azure portal, on hello **PostBeyond** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="c81d9-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="c81d9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_samlbase.png)

3. <span data-ttu-id="c81d9-155">Merhaba üzerinde **PostBeyond etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c81d9-155">On hello **PostBeyond Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_url.png)

    <span data-ttu-id="c81d9-157">a.</span><span class="sxs-lookup"><span data-stu-id="c81d9-157">a.</span></span> <span data-ttu-id="c81d9-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.postbeyond.com`</span><span class="sxs-lookup"><span data-stu-id="c81d9-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.postbeyond.com`</span></span>

    <span data-ttu-id="c81d9-159">b.</span><span class="sxs-lookup"><span data-stu-id="c81d9-159">b.</span></span> <span data-ttu-id="c81d9-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.postbeyond.com`</span><span class="sxs-lookup"><span data-stu-id="c81d9-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.postbeyond.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c81d9-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="c81d9-161">These values are not real.</span></span> <span data-ttu-id="c81d9-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="c81d9-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c81d9-163">Kişi [PostBeyond istemci destek ekibi](mailto:sso@postbeyond.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="c81d9-163">Contact [PostBeyond Client support team](mailto:sso@postbeyond.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="c81d9-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c81d9-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_certificate.png) 

5. <span data-ttu-id="c81d9-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c81d9-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-postbeyond-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c81d9-168">Merhaba üzerinde **PostBeyond yapılandırma** 'yi tıklatın **yapılandırma PostBeyond** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="c81d9-168">On hello **PostBeyond Configuration** section, click **Configure PostBeyond** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c81d9-169">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="c81d9-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_configure.png) 

7. <span data-ttu-id="c81d9-171">tooconfigure çoklu oturum açma üzerinde **PostBeyond** yan, indirilen toosend hello ihtiyacınız **Certificate(Base64)**, **SAML varlık kimliği**, **SAML çoklu oturum açma Hizmet URL'si** ve **Sign-Out URL** çok[PostBeyond destek ekibi](mailto:sso@postbeyond.com).</span><span class="sxs-lookup"><span data-stu-id="c81d9-171">tooconfigure single sign-on on **PostBeyond** side, you need toosend hello downloaded **Certificate(Base64)**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** too[PostBeyond support team](mailto:sso@postbeyond.com).</span></span> <span data-ttu-id="c81d9-172">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c81d9-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c81d9-173">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="c81d9-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c81d9-174">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="c81d9-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c81d9-175">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c81d9-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c81d9-176">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c81d9-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="c81d9-177">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="c81d9-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="c81d9-179">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c81d9-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c81d9-180">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c81d9-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c81d9-182">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c81d9-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c81d9-184">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="c81d9-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c81d9-186">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c81d9-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c81d9-188">a.</span><span class="sxs-lookup"><span data-stu-id="c81d9-188">a.</span></span> <span data-ttu-id="c81d9-189">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c81d9-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c81d9-190">b.</span><span class="sxs-lookup"><span data-stu-id="c81d9-190">b.</span></span> <span data-ttu-id="c81d9-191">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="c81d9-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c81d9-192">c.</span><span class="sxs-lookup"><span data-stu-id="c81d9-192">c.</span></span> <span data-ttu-id="c81d9-193">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="c81d9-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c81d9-194">d.</span><span class="sxs-lookup"><span data-stu-id="c81d9-194">d.</span></span> <span data-ttu-id="c81d9-195">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c81d9-195">Click **Create**.</span></span>
 
### <a name="creating-a-postbeyond-test-user"></a><span data-ttu-id="c81d9-196">PostBeyond test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c81d9-196">Creating a PostBeyond test user</span></span>

<span data-ttu-id="c81d9-197">Bu bölümde, PostBeyond içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c81d9-197">In this section, you create a user called Britta Simon in PostBeyond.</span></span> <span data-ttu-id="c81d9-198">Bilmiyorsanız tooadd Britta Simon PostBeyond içinde lütfen nasıl ile [PostBeyond destek ekibi](mailto:sso@postbeyond.com) tooadd hello test kullanıcısı ve SSO etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c81d9-198">If you don't know how tooadd Britta Simon in PostBeyond, please work with [PostBeyond support team](mailto:sso@postbeyond.com) tooadd hello test user and enable SSO.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c81d9-199">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="c81d9-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c81d9-200">Bu bölümde, erişim tooPostBeyond vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c81d9-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPostBeyond.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="c81d9-202">**tooassign Britta Simon tooPostBeyond hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c81d9-202">**tooassign Britta Simon tooPostBeyond, perform hello following steps:**</span></span>

1. <span data-ttu-id="c81d9-203">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c81d9-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="c81d9-205">Merhaba uygulamalar listesinde **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="c81d9-205">In hello applications list, select **PostBeyond**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_app.png) 

3. <span data-ttu-id="c81d9-207">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c81d9-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="c81d9-209">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c81d9-209">Click **Add** button.</span></span> <span data-ttu-id="c81d9-210">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c81d9-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="c81d9-212">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="c81d9-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c81d9-213">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c81d9-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c81d9-214">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c81d9-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c81d9-215">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="c81d9-215">Testing single sign-on</span></span>

<span data-ttu-id="c81d9-216">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c81d9-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="c81d9-217">Merhaba PostBeyond kutucuğa tıkladığınızda de erişim paneli Merhaba, toohello PostBeyond oturum almalısınız sayfasında.</span><span class="sxs-lookup"><span data-stu-id="c81d9-217">When you click hello PostBeyond tile in hello Access Panel, you should get toohello PostBeyond sign in page.</span></span> <span data-ttu-id="c81d9-218">Tıklayın **oturum Office 365 oturum**, Azure AD kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="c81d9-218">Click on **Sign in with Office 365**, enter your Azure AD credentials.</span></span> <span data-ttu-id="c81d9-219">Ardından, PostBeyond oturum açmanız.</span><span class="sxs-lookup"><span data-stu-id="c81d9-219">Then, you should be logged in into PostBeyond.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c81d9-220">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c81d9-220">Additional resources</span></span>

* [<span data-ttu-id="c81d9-221">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="c81d9-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c81d9-222">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="c81d9-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_203.png

