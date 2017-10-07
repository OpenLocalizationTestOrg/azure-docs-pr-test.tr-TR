---
title: "Öğretici: Azure Active Directory Tümleştirme ile Mindflash | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Mindflash arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdf91993-aaaa-4598-89b7-77ef8ca065d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: a1bc327ea3867287103acbb64d30f0a8d7d4c5e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mindflash"></a><span data-ttu-id="5b505-103">Öğretici: Azure Active Directory Tümleştirme Mindflash ile</span><span class="sxs-lookup"><span data-stu-id="5b505-103">Tutorial: Azure Active Directory integration with Mindflash</span></span>

<span data-ttu-id="5b505-104">Bu öğreticide, bilgi nasıl toointegrate Mindflash Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5b505-104">In this tutorial, you learn how toointegrate Mindflash with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b505-105">Mindflash Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="5b505-105">Integrating Mindflash with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5b505-106">Erişim tooMindflash sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5b505-106">You can control in Azure AD who has access tooMindflash</span></span>
- <span data-ttu-id="5b505-107">Kullanıcıların tooautomatically get açan tooMindflash (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5b505-107">You can enable your users tooautomatically get signed-on tooMindflash (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5b505-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="5b505-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5b505-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5b505-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b505-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5b505-110">Prerequisites</span></span>

<span data-ttu-id="5b505-111">tooconfigure Mindflash ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5b505-111">tooconfigure Azure AD integration with Mindflash, you need hello following items:</span></span>

- <span data-ttu-id="5b505-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="5b505-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b505-113">Bir Mindflash çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="5b505-113">A Mindflash single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5b505-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="5b505-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5b505-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="5b505-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b505-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="5b505-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5b505-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b505-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5b505-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="5b505-118">Scenario description</span></span>
<span data-ttu-id="5b505-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="5b505-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b505-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="5b505-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b505-121">Merhaba Galerisi'nden Mindflash ekleme</span><span class="sxs-lookup"><span data-stu-id="5b505-121">Adding Mindflash from hello gallery</span></span>
2. <span data-ttu-id="5b505-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="5b505-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mindflash-from-hello-gallery"></a><span data-ttu-id="5b505-123">Merhaba Galerisi'nden Mindflash ekleme</span><span class="sxs-lookup"><span data-stu-id="5b505-123">Adding Mindflash from hello gallery</span></span>
<span data-ttu-id="5b505-124">Azure AD'ye tooconfigure hello tümleştirme Mindflash, tooadd Mindflash hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b505-124">tooconfigure hello integration of Mindflash into Azure AD, you need tooadd Mindflash from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5b505-125">**tooadd Mindflash hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5b505-125">**tooadd Mindflash from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b505-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="5b505-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5b505-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="5b505-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5b505-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5b505-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="5b505-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5b505-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="5b505-133">Merhaba arama kutusuna yazın **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="5b505-133">In hello search box, type **Mindflash**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_search.png)

5. <span data-ttu-id="5b505-135">Merhaba Sonuçlar panelinde seçin **Mindflash**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="5b505-135">In hello results panel, select **Mindflash**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5b505-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="5b505-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5b505-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Mindflash sınayın.</span><span class="sxs-lookup"><span data-stu-id="5b505-138">In this section, you configure and test Azure AD single sign-on with Mindflash based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5b505-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Mindflash içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b505-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mindflash is tooa user in Azure AD.</span></span> <span data-ttu-id="5b505-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Mindflash hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b505-140">In other words, a link relationship between an Azure AD user and hello related user in Mindflash needs toobe established.</span></span>

<span data-ttu-id="5b505-141">Merhaba hello değeri Mindflash içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="5b505-141">In Mindflash, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5b505-142">tooconfigure ve Mindflash ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5b505-142">tooconfigure and test Azure AD single sign-on with Mindflash, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5b505-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="5b505-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5b505-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="5b505-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b505-145">**[Mindflash test kullanıcısı oluşturma](#creating-a-mindflash-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Mindflash içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="5b505-145">**[Creating a Mindflash test user](#creating-a-mindflash-test-user)** - toohave a counterpart of Britta Simon in Mindflash that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5b505-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="5b505-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5b505-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="5b505-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5b505-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5b505-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5b505-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Mindflash uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5b505-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mindflash application.</span></span>

<span data-ttu-id="5b505-150">**tooconfigure Azure AD çoklu oturum açma ile Mindflash, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5b505-150">**tooconfigure Azure AD single sign-on with Mindflash, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b505-151">Hello hello üzerinde Azure portal'ın **Mindflash** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="5b505-151">In hello Azure portal, on hello **Mindflash** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="5b505-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="5b505-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_samlbase.png)

3. <span data-ttu-id="5b505-155">Merhaba üzerinde **Mindflash etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5b505-155">On hello **Mindflash Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_url.png)

    <span data-ttu-id="5b505-157">a.</span><span class="sxs-lookup"><span data-stu-id="5b505-157">a.</span></span> <span data-ttu-id="5b505-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="5b505-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.mindflash.com`</span></span>

    <span data-ttu-id="5b505-159">b.</span><span class="sxs-lookup"><span data-stu-id="5b505-159">b.</span></span> <span data-ttu-id="5b505-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="5b505-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.mindflash.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5b505-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="5b505-161">These values are not real.</span></span> <span data-ttu-id="5b505-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="5b505-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5b505-163">Kişi [Mindflash istemci destek ekibi](https://www.mindflash.com/contact/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="5b505-163">Contact [Mindflash Client support team](https://www.mindflash.com/contact/) tooget these values.</span></span> 
 


4. <span data-ttu-id="5b505-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5b505-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_certificate.png) 

5. <span data-ttu-id="5b505-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5b505-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mindflash-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5b505-168">tooconfigure çoklu oturum açma üzerinde **Mindflash** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[Mindflash destek ekibi](https://www.mindflash.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="5b505-168">tooconfigure single sign-on on **Mindflash** side, you need toosend hello downloaded **Metadata XML** too[Mindflash support team](https://www.mindflash.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="5b505-169">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="5b505-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5b505-170">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="5b505-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5b505-171">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5b505-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5b505-172">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b505-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="5b505-173">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="5b505-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="5b505-175">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5b505-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b505-176">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="5b505-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mindflash-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5b505-178">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="5b505-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mindflash-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5b505-180">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="5b505-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mindflash-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5b505-182">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5b505-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mindflash-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5b505-184">a.</span><span class="sxs-lookup"><span data-stu-id="5b505-184">a.</span></span> <span data-ttu-id="5b505-185">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5b505-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b505-186">b.</span><span class="sxs-lookup"><span data-stu-id="5b505-186">b.</span></span> <span data-ttu-id="5b505-187">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="5b505-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5b505-188">c.</span><span class="sxs-lookup"><span data-stu-id="5b505-188">c.</span></span> <span data-ttu-id="5b505-189">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="5b505-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5b505-190">d.</span><span class="sxs-lookup"><span data-stu-id="5b505-190">d.</span></span> <span data-ttu-id="5b505-191">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5b505-191">Click **Create**.</span></span>
 
### <a name="creating-a-mindflash-test-user"></a><span data-ttu-id="5b505-192">Mindflash test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b505-192">Creating a Mindflash test user</span></span>

<span data-ttu-id="5b505-193">Mindflash içine sipariş tooenable Azure AD kullanıcıların toolog bunların Mindflash sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5b505-193">In order tooenable Azure AD users toolog into Mindflash, they must be provisioned into Mindflash.</span></span> <span data-ttu-id="5b505-194">Mindflash Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="5b505-194">In hello case of Mindflash, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="5b505-195">bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="5b505-195">tooprovision a user accounts, perform hello following steps:</span></span>

1. <span data-ttu-id="5b505-196">İçinde tooyour oturum **Mindflash** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="5b505-196">Log in tooyour **Mindflash** company site as an administrator.</span></span>

2. <span data-ttu-id="5b505-197">Çok Git**kullanıcıları yönetme**.</span><span class="sxs-lookup"><span data-stu-id="5b505-197">Go too**Manage Users**.</span></span>
   
    <span data-ttu-id="5b505-198">![Kullanıcıları yönetme](./media/active-directory-saas-mindflash-tutorial/ic787140.png "kullanıcıları yönetme")</span><span class="sxs-lookup"><span data-stu-id="5b505-198">![Manage Users](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Manage Users")</span></span>

3. <span data-ttu-id="5b505-199">Merhaba tıklatın **Kullanıcı Ekle**ve ardından **yeni**.</span><span class="sxs-lookup"><span data-stu-id="5b505-199">Click hello **Add Users**, and then click **New**.</span></span>

4. <span data-ttu-id="5b505-200">Merhaba, **yeni kullanıcı Ekle** bölümünde, aşağıdaki adımları geçerli Azure hello gerçekleştirmek tooprovision istediğiniz AD hesabı:</span><span class="sxs-lookup"><span data-stu-id="5b505-200">In hello **Add New Users** section, perform hello following steps of a valid Azure AD account you want tooprovision:</span></span>
   
    <span data-ttu-id="5b505-201">![Yeni kullanıcı ekleme](./media/active-directory-saas-mindflash-tutorial/ic787141.png "yeni kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="5b505-201">![Add New Users](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Add New Users")</span></span>
   
    <span data-ttu-id="5b505-202">a.</span><span class="sxs-lookup"><span data-stu-id="5b505-202">a.</span></span> <span data-ttu-id="5b505-203">Merhaba, **ad** metin kutusuna, türü **ad** hello kullanıcı **Britta**.</span><span class="sxs-lookup"><span data-stu-id="5b505-203">In hello **First name** textbox, type **First name** of hello user as **Britta**.</span></span>

    <span data-ttu-id="5b505-204">b.</span><span class="sxs-lookup"><span data-stu-id="5b505-204">b.</span></span> <span data-ttu-id="5b505-205">Merhaba, **Soyadı** metin kutusuna, türü **Soyadı** hello kullanıcı **Simon**.</span><span class="sxs-lookup"><span data-stu-id="5b505-205">In hello **Last name** textbox, type **Last name** of hello user as **Simon**.</span></span>
    
    <span data-ttu-id="5b505-206">c.</span><span class="sxs-lookup"><span data-stu-id="5b505-206">c.</span></span> <span data-ttu-id="5b505-207">Merhaba, **e-posta** metin kutusuna, türü **e-posta adresi** hello kullanıcı  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="5b505-207">In hello **Email** textbox, type **Email Address** of hello user as **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="5b505-208">b.</span><span class="sxs-lookup"><span data-stu-id="5b505-208">b.</span></span> <span data-ttu-id="5b505-209">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5b505-209">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="5b505-210">API AAD kullanıcı hesaplarının Mindflash tooprovision tarafından sağlanan veya herhangi diğer Mindflash kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b505-210">You can use any other Mindflash user account creation tools or APIs provided by Mindflash tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5b505-211">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="5b505-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5b505-212">Bu bölümde, erişim tooMindflash vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5b505-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMindflash.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="5b505-214">**tooassign Britta Simon tooMindflash hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5b505-214">**tooassign Britta Simon tooMindflash, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b505-215">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5b505-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="5b505-217">Merhaba uygulamalar listesinde **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="5b505-217">In hello applications list, select **Mindflash**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_app.png) 

3. <span data-ttu-id="5b505-219">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="5b505-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="5b505-221">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5b505-221">Click **Add** button.</span></span> <span data-ttu-id="5b505-222">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5b505-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="5b505-224">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="5b505-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5b505-225">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5b505-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b505-226">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5b505-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5b505-227">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="5b505-227">Testing single sign-on</span></span>

<span data-ttu-id="5b505-228">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="5b505-228">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5b505-229">Merhaba Mindflash hello erişim paneli parçasında tıkladığınızda, oturum açma sayfasına Mindflash uygulamasının almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b505-229">When you click hello Mindflash tile in hello Access Panel, you should get login page of Mindflash application.</span></span>
<span data-ttu-id="5b505-230">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5b505-230">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5b505-231">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="5b505-231">Additional resources</span></span>

* [<span data-ttu-id="5b505-232">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="5b505-232">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b505-233">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="5b505-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_203.png

