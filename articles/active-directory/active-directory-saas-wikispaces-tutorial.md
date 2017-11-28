---
title: "Öğretici: Azure Active Directory Tümleştirme ile Wikispaces | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Wikispaces arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 665b95aa-f7f5-4406-9e2a-6fc299a1599c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: eb5b72e60b415cb657b70ba530df731ae14b0425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wikispaces"></a><span data-ttu-id="4c7c2-103">Öğretici: Azure Active Directory Tümleştirme Wikispaces ile</span><span class="sxs-lookup"><span data-stu-id="4c7c2-103">Tutorial: Azure Active Directory integration with Wikispaces</span></span>

<span data-ttu-id="4c7c2-104">Bu öğreticide, bilgi nasıl toointegrate Wikispaces Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4c7c2-104">In this tutorial, you learn how toointegrate Wikispaces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4c7c2-105">Wikispaces Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="4c7c2-105">Integrating Wikispaces with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4c7c2-106">Erişim tooWikispaces sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4c7c2-106">You can control in Azure AD who has access tooWikispaces</span></span>
- <span data-ttu-id="4c7c2-107">Kullanıcıların tooautomatically get açan tooWikispaces (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4c7c2-107">You can enable your users tooautomatically get signed-on tooWikispaces (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4c7c2-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="4c7c2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4c7c2-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4c7c2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c7c2-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4c7c2-110">Prerequisites</span></span>

<span data-ttu-id="4c7c2-111">tooconfigure Wikispaces ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="4c7c2-111">tooconfigure Azure AD integration with Wikispaces, you need hello following items:</span></span>

- <span data-ttu-id="4c7c2-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="4c7c2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4c7c2-113">Bir Wikispaces çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="4c7c2-113">A Wikispaces single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4c7c2-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4c7c2-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="4c7c2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4c7c2-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4c7c2-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c7c2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4c7c2-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="4c7c2-118">Scenario description</span></span>
<span data-ttu-id="4c7c2-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4c7c2-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="4c7c2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4c7c2-121">Merhaba Galerisi'nden Wikispaces ekleme</span><span class="sxs-lookup"><span data-stu-id="4c7c2-121">Adding Wikispaces from hello gallery</span></span>
2. <span data-ttu-id="4c7c2-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4c7c2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wikispaces-from-hello-gallery"></a><span data-ttu-id="4c7c2-123">Merhaba Galerisi'nden Wikispaces ekleme</span><span class="sxs-lookup"><span data-stu-id="4c7c2-123">Adding Wikispaces from hello gallery</span></span>
<span data-ttu-id="4c7c2-124">Azure AD'ye tooconfigure hello tümleştirme Wikispaces, tooadd Wikispaces hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-124">tooconfigure hello integration of Wikispaces into Azure AD, you need tooadd Wikispaces from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4c7c2-125">**tooadd Wikispaces hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4c7c2-125">**tooadd Wikispaces from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c7c2-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4c7c2-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4c7c2-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="4c7c2-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="4c7c2-133">Merhaba arama kutusuna yazın **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-133">In hello search box, type **Wikispaces**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_search.png)

5. <span data-ttu-id="4c7c2-135">Merhaba Sonuçlar panelinde seçin **Wikispaces**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-135">In hello results panel, select **Wikispaces**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4c7c2-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4c7c2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4c7c2-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Wikispaces sınayın.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-138">In this section, you configure and test Azure AD single sign-on with Wikispaces based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4c7c2-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Wikispaces içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wikispaces is tooa user in Azure AD.</span></span> <span data-ttu-id="4c7c2-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Wikispaces hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-140">In other words, a link relationship between an Azure AD user and hello related user in Wikispaces needs toobe established.</span></span>

<span data-ttu-id="4c7c2-141">Merhaba hello değeri Wikispaces içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-141">In Wikispaces, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4c7c2-142">tooconfigure ve Wikispaces ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="4c7c2-142">tooconfigure and test Azure AD single sign-on with Wikispaces, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4c7c2-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4c7c2-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4c7c2-145">**[Wikispaces test kullanıcısı oluşturma](#creating-a-wikispaces-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Wikispaces içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-145">**[Creating a Wikispaces test user](#creating-a-wikispaces-test-user)** - toohave a counterpart of Britta Simon in Wikispaces that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4c7c2-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4c7c2-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4c7c2-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4c7c2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4c7c2-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Wikispaces uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wikispaces application.</span></span>

<span data-ttu-id="4c7c2-150">**tooconfigure Azure AD çoklu oturum açma ile Wikispaces, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4c7c2-150">**tooconfigure Azure AD single sign-on with Wikispaces, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c7c2-151">Hello hello üzerinde Azure portal'ın **Wikispaces** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-151">In hello Azure portal, on hello **Wikispaces** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="4c7c2-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_samlbase.png)

3. <span data-ttu-id="4c7c2-155">Merhaba üzerinde **Wikispaces etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4c7c2-155">On hello **Wikispaces Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_url.png)

    <span data-ttu-id="4c7c2-157">a.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-157">a.</span></span> <span data-ttu-id="4c7c2-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.wikispaces.net`</span><span class="sxs-lookup"><span data-stu-id="4c7c2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.wikispaces.net`</span></span>

    <span data-ttu-id="4c7c2-159">b.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-159">b.</span></span> <span data-ttu-id="4c7c2-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://session.wikispaces.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="4c7c2-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://session.wikispaces.net/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4c7c2-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-161">These values are not real.</span></span> <span data-ttu-id="4c7c2-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4c7c2-163">Kişi [Wikispaces istemci destek ekibi](https://www.wikispaces.com/site/help) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-163">Contact [Wikispaces Client support team](https://www.wikispaces.com/site/help) tooget these values.</span></span> 

4. <span data-ttu-id="4c7c2-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_certificate.png) 

5. <span data-ttu-id="4c7c2-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wikispaces-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4c7c2-168">tooconfigure çoklu oturum açma üzerinde **Wikispaces** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[Wikispaces destek ekibi](https://www.wikispaces.com/site/help).</span><span class="sxs-lookup"><span data-stu-id="4c7c2-168">tooconfigure single sign-on on **Wikispaces** side, you need toosend hello downloaded **Metadata XML** too[Wikispaces support team](https://www.wikispaces.com/site/help).</span></span> <span data-ttu-id="4c7c2-169">Merhaba Yapılandırma tamamlandıktan hemen sonra bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-169">You will get a notification as soon as hello configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="4c7c2-170">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="4c7c2-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4c7c2-171">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4c7c2-172">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4c7c2-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4c7c2-173">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c7c2-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="4c7c2-174">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="4c7c2-176">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4c7c2-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c7c2-177">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4c7c2-179">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4c7c2-181">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4c7c2-183">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4c7c2-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4c7c2-185">a.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-185">a.</span></span> <span data-ttu-id="4c7c2-186">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4c7c2-187">b.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-187">b.</span></span> <span data-ttu-id="4c7c2-188">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4c7c2-189">c.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-189">c.</span></span> <span data-ttu-id="4c7c2-190">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4c7c2-191">d.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-191">d.</span></span> <span data-ttu-id="4c7c2-192">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-192">Click **Create**.</span></span>
 
### <a name="creating-a-wikispaces-test-user"></a><span data-ttu-id="4c7c2-193">Wikispaces test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c7c2-193">Creating a Wikispaces test user</span></span>

<span data-ttu-id="4c7c2-194">TooWikispaces içinde sipariş tooenable Azure AD kullanıcıların toolog bunların Wikispaces sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-194">In order tooenable Azure AD users toolog in tooWikispaces, they must be provisioned into Wikispaces.</span></span> <span data-ttu-id="4c7c2-195">Wikispaces Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-195">In hello case of Wikispaces, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="4c7c2-196">bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4c7c2-196">tooprovision a user accounts, perform hello following steps:</span></span>
1. <span data-ttu-id="4c7c2-197">İçinde tooyour oturum **Wikispaces** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-197">Log in tooyour **Wikispaces** company site as an administrator.</span></span>

2. <span data-ttu-id="4c7c2-198">Çok Git**üyeleri**.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-198">Go too**Members**.</span></span>
   
    <span data-ttu-id="4c7c2-199">![Üyeleri](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "üyeleri")</span><span class="sxs-lookup"><span data-stu-id="4c7c2-199">![Members](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Members")</span></span>

3. <span data-ttu-id="4c7c2-200">Merhaba tıklatın **kişileri davet**.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-200">Click hello **Invite People**.</span></span>
   
    <span data-ttu-id="4c7c2-201">![Kişileri davet edin](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "kişileri davet edin")</span><span class="sxs-lookup"><span data-stu-id="4c7c2-201">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "Invite People")</span></span>

4. <span data-ttu-id="4c7c2-202">Merhaba, **kişileri davet** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4c7c2-202">In hello **Invite People** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="4c7c2-203">![Kişileri davet edin](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "kişileri davet edin")</span><span class="sxs-lookup"><span data-stu-id="4c7c2-203">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "Invite People")</span></span>
   
    <span data-ttu-id="4c7c2-204">a.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-204">a.</span></span> <span data-ttu-id="4c7c2-205">Türü hello **kullanıcı adlarını veya e-posta adresi** , metin kutuları hello tooprovision istediğiniz geçerli bir AAD hesabıyla ilgili.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-205">Type hello **Usernames or Email Address** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="4c7c2-206">b.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-206">b.</span></span> <span data-ttu-id="4c7c2-207">Tıklatın **Gönder**.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-207">Click **Send**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="4c7c2-208">Hello Azure Active Directory hesap sahibi etkin hale önce bir bağlantı tooconfirm hello hesabı da dahil olmak üzere bir e-posta alır.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-208">hello Azure Active Directory account holder receives an email including a link tooconfirm hello account before it becomes active.</span></span>
    
> [!NOTE]
> <span data-ttu-id="4c7c2-209">API AAD kullanıcı hesaplarının Wikispaces tooprovision tarafından sağlanan veya herhangi diğer Wikispaces kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-209">You can use any other Wikispaces user account creation tools or APIs provided by Wikispaces tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4c7c2-210">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="4c7c2-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4c7c2-211">Bu bölümde, erişim tooWikispaces vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWikispaces.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="4c7c2-213">**tooassign Britta Simon tooWikispaces hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4c7c2-213">**tooassign Britta Simon tooWikispaces, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c7c2-214">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="4c7c2-216">Merhaba uygulamalar listesinde **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-216">In hello applications list, select **Wikispaces**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_app.png) 

3. <span data-ttu-id="4c7c2-218">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="4c7c2-220">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-220">Click **Add** button.</span></span> <span data-ttu-id="4c7c2-221">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="4c7c2-223">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4c7c2-224">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4c7c2-225">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4c7c2-226">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="4c7c2-226">Testing single sign-on</span></span>

<span data-ttu-id="4c7c2-227">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4c7c2-228">Hello erişim paneli Wikispaces döşeme hello tıkladığınızda, otomatik olarak oturum açma Wikispaces uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c7c2-228">When you click hello Wikispaces tile in hello Access Panel, you should get automatically signed-on tooyour Wikispaces application.</span></span>
<span data-ttu-id="4c7c2-229">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4c7c2-229">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4c7c2-230">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4c7c2-230">Additional resources</span></span>

* [<span data-ttu-id="4c7c2-231">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="4c7c2-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4c7c2-232">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="4c7c2-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_203.png

