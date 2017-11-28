---
title: "Öğretici: Azure Active Directory Tümleştirme ile FM:Systems | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile FM:Systems arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f78c58c5-6e98-458b-8991-78624a245665
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 677ef74dac663a43835d65a4d4f4fd031a0078cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fmsystems"></a><span data-ttu-id="c3885-103">Öğretici: Azure Active Directory Tümleştirme FM:Systems ile</span><span class="sxs-lookup"><span data-stu-id="c3885-103">Tutorial: Azure Active Directory integration with FM:Systems</span></span>

<span data-ttu-id="c3885-104">Bu öğreticide, bilgi nasıl toointegrate FM:Systems Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c3885-104">In this tutorial, you learn how toointegrate FM:Systems with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c3885-105">FM:Systems Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="c3885-105">Integrating FM:Systems with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c3885-106">Erişim tooFM:Systems sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c3885-106">You can control in Azure AD who has access tooFM:Systems</span></span>
- <span data-ttu-id="c3885-107">Kullanıcıların tooautomatically get açan tooFM:Systems (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c3885-107">You can enable your users tooautomatically get signed-on tooFM:Systems (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c3885-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="c3885-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c3885-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c3885-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3885-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c3885-110">Prerequisites</span></span>

<span data-ttu-id="c3885-111">tooconfigure FM:Systems ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c3885-111">tooconfigure Azure AD integration with FM:Systems, you need hello following items:</span></span>

- <span data-ttu-id="c3885-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="c3885-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c3885-113">Bir FM:Systems çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="c3885-113">An FM:Systems single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c3885-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="c3885-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c3885-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="c3885-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c3885-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c3885-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c3885-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c3885-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c3885-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="c3885-118">Scenario description</span></span>
<span data-ttu-id="c3885-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="c3885-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c3885-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="c3885-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c3885-121">Merhaba Galerisi'nden FM:Systems ekleme</span><span class="sxs-lookup"><span data-stu-id="c3885-121">Adding FM:Systems from hello gallery</span></span>
2. <span data-ttu-id="c3885-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c3885-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fmsystems-from-hello-gallery"></a><span data-ttu-id="c3885-123">Merhaba Galerisi'nden FM:Systems ekleme</span><span class="sxs-lookup"><span data-stu-id="c3885-123">Adding FM:Systems from hello gallery</span></span>
<span data-ttu-id="c3885-124">Azure AD'ye tooconfigure hello tümleştirme FM:Systems, tooadd FM:Systems hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3885-124">tooconfigure hello integration of FM:Systems into Azure AD, you need tooadd FM:Systems from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c3885-125">**tooadd FM:Systems hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c3885-125">**tooadd FM:Systems from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3885-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c3885-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c3885-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="c3885-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c3885-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c3885-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="c3885-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c3885-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="c3885-133">Merhaba arama kutusuna yazın **FM:Systems**.</span><span class="sxs-lookup"><span data-stu-id="c3885-133">In hello search box, type **FM:Systems**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_search.png)

5. <span data-ttu-id="c3885-135">Merhaba Sonuçlar panelinde seçin **FM:Systems**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="c3885-135">In hello results panel, select **FM:Systems**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c3885-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c3885-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c3885-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı FM:Systems sınayın.</span><span class="sxs-lookup"><span data-stu-id="c3885-138">In this section, you configure and test Azure AD single sign-on with FM:Systems based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c3885-139">Tek toowork'ın oturum açma hangi hello karşılık gelen FM:Systems içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3885-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FM:Systems is tooa user in Azure AD.</span></span> <span data-ttu-id="c3885-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı FM:Systems hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3885-140">In other words, a link relationship between an Azure AD user and hello related user in FM:Systems needs toobe established.</span></span>

<span data-ttu-id="c3885-141">Merhaba hello değeri FM:Systems içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="c3885-141">In FM:Systems, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c3885-142">tooconfigure ve FM:Systems ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c3885-142">tooconfigure and test Azure AD single sign-on with FM:Systems, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c3885-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="c3885-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c3885-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="c3885-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c3885-145">**[Bir FM:Systems test kullanıcısı oluşturma](#creating-an-fmsystems-test-user)**  -toohave bir Britta Simon karşılık gelen kullanıcı bağlantılı toohello Azure AD gösterimidir FM:Systems içinde.</span><span class="sxs-lookup"><span data-stu-id="c3885-145">**[Creating an FM:Systems test user](#creating-an-fmsystems-test-user)** - toohave a counterpart of Britta Simon in FM:Systems that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c3885-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="c3885-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c3885-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="c3885-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c3885-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c3885-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c3885-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma FM:Systems uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c3885-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FM:Systems application.</span></span>

<span data-ttu-id="c3885-150">**tooconfigure Azure AD çoklu oturum açma ile FM:Systems, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c3885-150">**tooconfigure Azure AD single sign-on with FM:Systems, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3885-151">Hello hello üzerinde Azure portal'ın **FM:Systems** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c3885-151">In hello Azure portal, on hello **FM:Systems** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="c3885-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="c3885-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_samlbase.png)

3. <span data-ttu-id="c3885-155">Merhaba üzerinde **FM:Systems etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c3885-155">On hello **FM:Systems Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_url.png)

    <span data-ttu-id="c3885-157">Merhaba, **yanıt URL'si** metin, FM:Systems yazın **yanıt URL'si**, desen aşağıdaki hello kullanarak türü hello URL'si:`https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span><span class="sxs-lookup"><span data-stu-id="c3885-157">In hello **Reply URL** textbox, type your FM:Systems **Reply URL**, type hello URL using hello following pattern: `https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c3885-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="c3885-158">This value is not real.</span></span> <span data-ttu-id="c3885-159">Bu değer hello gerçek yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c3885-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="c3885-160">Kişi [FM:Systems destek ekibi](https://fmsystems.com/ask-us/) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="c3885-160">Contact [FM:Systems support team](https://fmsystems.com/ask-us/) tooget this value.</span></span>
 
4. <span data-ttu-id="c3885-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c3885-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_certificate.png) 

5. <span data-ttu-id="c3885-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c3885-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-fm-systems-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c3885-165">tooconfigure çoklu oturum açma üzerinde **FM:Systems** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[FM:Systems destek ekibi](https://fmsystems.com/ask-us/).</span><span class="sxs-lookup"><span data-stu-id="c3885-165">tooconfigure single sign-on on **FM:Systems** side, you need toosend hello downloaded **Metadata XML** too[FM:Systems support team](https://fmsystems.com/ask-us/).</span></span> <span data-ttu-id="c3885-166">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c3885-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span> <span data-ttu-id="c3885-167">SSO, aboneliğiniz için etkinleştirildiğinde, bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="c3885-167">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="c3885-168">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="c3885-168">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c3885-169">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="c3885-169">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c3885-170">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c3885-170">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c3885-171">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c3885-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="c3885-172">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="c3885-172">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="c3885-174">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c3885-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3885-175">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c3885-175">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c3885-177">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c3885-177">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c3885-179">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="c3885-179">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c3885-181">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c3885-181">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c3885-183">a.</span><span class="sxs-lookup"><span data-stu-id="c3885-183">a.</span></span> <span data-ttu-id="c3885-184">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c3885-184">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c3885-185">b.</span><span class="sxs-lookup"><span data-stu-id="c3885-185">b.</span></span> <span data-ttu-id="c3885-186">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="c3885-186">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c3885-187">c.</span><span class="sxs-lookup"><span data-stu-id="c3885-187">c.</span></span> <span data-ttu-id="c3885-188">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="c3885-188">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c3885-189">d.</span><span class="sxs-lookup"><span data-stu-id="c3885-189">d.</span></span> <span data-ttu-id="c3885-190">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c3885-190">Click **Create**.</span></span>
 
### <a name="creating-an-fmsystems-test-user"></a><span data-ttu-id="c3885-191">Bir FM:Systems test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c3885-191">Creating an FM:Systems test user</span></span>

1. <span data-ttu-id="c3885-192">Bir web tarayıcısı penceresinde FM:Systems şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c3885-192">In a web browser window, log into your FM:Systems company site as an administrator.</span></span>

2. <span data-ttu-id="c3885-193">Çok Git**Sistem Yönetimi \> Güvenliği Yönet \> kullanıcılar \> kullanıcı listesi**.</span><span class="sxs-lookup"><span data-stu-id="c3885-193">Go too**System Administration \> Manage Security \> Users \> User list**.</span></span>
   
    <span data-ttu-id="c3885-194">![Sistem Yönetimi](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "Sistem Yönetimi")</span><span class="sxs-lookup"><span data-stu-id="c3885-194">![System Administration](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "System Administration")</span></span>

3. <span data-ttu-id="c3885-195">Tıklatın **yeni kullanıcı oluştur**.</span><span class="sxs-lookup"><span data-stu-id="c3885-195">Click **Create new user**.</span></span>
   
    <span data-ttu-id="c3885-196">![Yeni kullanıcı oluşturmak](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "yeni kullanıcı oluşturun")</span><span class="sxs-lookup"><span data-stu-id="c3885-196">![Create New User](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Create New User")</span></span>

4. <span data-ttu-id="c3885-197">Merhaba, **kullanıcı oluştur** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c3885-197">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c3885-198">![Kullanıcı oluşturma](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "kullanıcı oluştur")</span><span class="sxs-lookup"><span data-stu-id="c3885-198">![Create User](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Create User")</span></span>
   
    <span data-ttu-id="c3885-199">a.</span><span class="sxs-lookup"><span data-stu-id="c3885-199">a.</span></span> <span data-ttu-id="c3885-200">Türü hello **kullanıcıadı**, hello **parola**, **parolayı onayla**, **e-posta** ve hello **çalışan kimliği**geçerli bir Azure hello tooprovision istediğiniz Active Directory hesabı kutularındaki ilgili.</span><span class="sxs-lookup"><span data-stu-id="c3885-200">Type hello **UserName**, hello **Password**, **Confirm Password**, **E-mail** and hello **Employee ID** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="c3885-201">b.</span><span class="sxs-lookup"><span data-stu-id="c3885-201">b.</span></span> <span data-ttu-id="c3885-202">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c3885-202">Click **Next**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c3885-203">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="c3885-203">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c3885-204">Bu bölümde, erişim tooFM:Systems vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c3885-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFM:Systems.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="c3885-206">**tooassign Britta Simon tooFM:Systems hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c3885-206">**tooassign Britta Simon tooFM:Systems, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3885-207">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c3885-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="c3885-209">Merhaba uygulamalar listesinde **FM:Systems**.</span><span class="sxs-lookup"><span data-stu-id="c3885-209">In hello applications list, select **FM:Systems**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_app.png) 

3. <span data-ttu-id="c3885-211">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c3885-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="c3885-213">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c3885-213">Click **Add** button.</span></span> <span data-ttu-id="c3885-214">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c3885-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="c3885-216">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="c3885-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c3885-217">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c3885-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c3885-218">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c3885-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c3885-219">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="c3885-219">Testing single sign-on</span></span>

<span data-ttu-id="c3885-220">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="c3885-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c3885-221">Merhaba FM:Systems hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour FM:Systems uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3885-221">When you click hello FM:Systems tile in hello Access Panel, you should get automatically signed-on tooyour FM:Systems application.</span></span>
<span data-ttu-id="c3885-222">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c3885-222">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c3885-223">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c3885-223">Additional resources</span></span>

* [<span data-ttu-id="c3885-224">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="c3885-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c3885-225">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="c3885-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_203.png

