---
title: "Öğretici: Azure Active Directory Tümleştirme ile Merhaba bulut BC | Microsoft Docs"
description: "Nasıl tooconfigure çoklu oturum açma Azure Active Directory içinde BC arasındaki hello bulut öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7dc40d2c-6349-40cb-b304-b098bd03a66c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/1/2017
ms.author: jeedes
ms.openlocfilehash: e81ffb522b2c96c7e9b2919abd8d3b199c295eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bc-in-hello-cloud"></a><span data-ttu-id="3c0fa-103">Öğretici: Azure Active Directory Tümleştirme hello bulut BC ile</span><span class="sxs-lookup"><span data-stu-id="3c0fa-103">Tutorial: Azure Active Directory integration with BC in hello Cloud</span></span>

<span data-ttu-id="3c0fa-104">Bu öğreticide, nasıl toointegrate BC içinde hello bulut Azure Active Directory (Azure AD) ile bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-104">In this tutorial, you learn how toointegrate BC in hello Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3c0fa-105">Hello Azure AD ile bulut içinde BC tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="3c0fa-105">Integrating BC in hello Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3c0fa-106">Merhaba bulut erişim tooBC olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="3c0fa-106">You can control in Azure AD who has access tooBC in hello Cloud</span></span>
- <span data-ttu-id="3c0fa-107">Kullanıcıların tooautomatically get açan tooBC hello (çoklu oturum açma) bulut kendi Azure AD hesapları ile de etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="3c0fa-107">You can enable your users tooautomatically get signed-on tooBC in hello Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3c0fa-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="3c0fa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3c0fa-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3c0fa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c0fa-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3c0fa-110">Prerequisites</span></span>

<span data-ttu-id="3c0fa-111">tooconfigure hello bulut BC ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="3c0fa-111">tooconfigure Azure AD integration with BC in hello Cloud, you need hello following items:</span></span>

- <span data-ttu-id="3c0fa-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="3c0fa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3c0fa-113">Merhaba bulut çoklu oturum etkin abonelikte içinde BC</span><span class="sxs-lookup"><span data-stu-id="3c0fa-113">A BC in hello Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3c0fa-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3c0fa-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="3c0fa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3c0fa-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3c0fa-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3c0fa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3c0fa-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="3c0fa-118">Scenario description</span></span>
<span data-ttu-id="3c0fa-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3c0fa-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="3c0fa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3c0fa-121">Merhaba hello galerisinden bulut BC ekleme</span><span class="sxs-lookup"><span data-stu-id="3c0fa-121">Adding BC in hello Cloud from hello gallery</span></span>
2. <span data-ttu-id="3c0fa-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="3c0fa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bc-in-hello-cloud-from-hello-gallery"></a><span data-ttu-id="3c0fa-123">Merhaba hello galerisinden bulut BC ekleme</span><span class="sxs-lookup"><span data-stu-id="3c0fa-123">Adding BC in hello Cloud from hello gallery</span></span>
<span data-ttu-id="3c0fa-124">Merhaba tümleştirilmesi hello Azure AD bulutunu BC tooconfigure, tooadd BC hello bulut hello galeri tooyour yönetilen SaaS uygulamaları listesinden de gerekir.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-124">tooconfigure hello integration of BC in hello Cloud into Azure AD, you need tooadd BC in hello Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3c0fa-125">**tooadd BC hello hello galerisinden, bulut içindeki hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3c0fa-125">**tooadd BC in hello Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c0fa-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3c0fa-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3c0fa-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="3c0fa-131">tooadd yeni uygulama tıklatın **Ekle** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-131">tooadd new application, click **Add** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="3c0fa-133">Merhaba arama kutusuna yazın **hello bulut BC**.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-133">In hello search box, type **BC in hello Cloud**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_search.png)

5. <span data-ttu-id="3c0fa-135">Merhaba Sonuçlar panelinde seçin **hello bulut BC**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-135">In hello results panel, select **BC in hello Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3c0fa-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="3c0fa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3c0fa-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile BC "Britta Simon." olarak adlandırılan bir test kullanıcı bulut tabanlı hello test</span><span class="sxs-lookup"><span data-stu-id="3c0fa-138">In this section, you configure and test Azure AD single sign-on with BC in hello Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3c0fa-139">Tek toowork'ın oturum açma Azure AD tooknow hangi hello gereken hello bulut BC karşılık gelen kullanıcı Azure AD'de tooa kullanıcı olduğu.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BC in hello Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="3c0fa-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı hello bulut BC hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-140">In other words, a link relationship between an Azure AD user and hello related user in BC in hello Cloud needs toobe established.</span></span>

<span data-ttu-id="3c0fa-141">Merhaba bulut içinde BC içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-141">In BC in hello Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3c0fa-142">tooconfigure ve hello bulut BC ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="3c0fa-142">tooconfigure and test Azure AD single sign-on with BC in hello Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3c0fa-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3c0fa-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3c0fa-145">**[Bir BC hello bulut test kullanıcısı oluşturma](#creating-a-bc-in-the-cloud-test-user)**  -toohave Britta Simon hello kullanıcı bağlantılı toohello Azure AD gösterimidir bulut BC içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-145">**[Creating a BC in hello Cloud test user](#creating-a-bc-in-the-cloud-test-user)** - toohave a counterpart of Britta Simon in BC in hello Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3c0fa-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3c0fa-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3c0fa-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3c0fa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3c0fa-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma, BC hello bulut uygulamasında yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BC in hello Cloud application.</span></span>

<span data-ttu-id="3c0fa-150">**tooconfigure Azure AD çoklu oturum açma hello bulut BC ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3c0fa-150">**tooconfigure Azure AD single sign-on with BC in hello Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c0fa-151">Merhaba hello üzerinde Azure portal'ın **hello bulut BC** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-151">In hello Azure portal, on hello **BC in hello Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="3c0fa-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_samlbase.png)

3. <span data-ttu-id="3c0fa-155">Merhaba üzerinde **BC hello bulut etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3c0fa-155">On hello **BC in hello Cloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_url.png)

    <span data-ttu-id="3c0fa-157">a.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-157">a.</span></span> <span data-ttu-id="3c0fa-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span><span class="sxs-lookup"><span data-stu-id="3c0fa-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span></span>

    <span data-ttu-id="3c0fa-159">b.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-159">b.</span></span> <span data-ttu-id="3c0fa-160">Merhaba, **tanımlayıcısı** metin kutusuna, URL'yi yazın:`https://app.bcinthecloud.com`</span><span class="sxs-lookup"><span data-stu-id="3c0fa-160">In hello **Identifier** textbox, type a URL as: `https://app.bcinthecloud.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3c0fa-161">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-161">This value is not real.</span></span> <span data-ttu-id="3c0fa-162">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="3c0fa-163">Kişi [hello bulut istemci destek ekibi BC](https://www.bcinthecloud.com/supportcenter/) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-163">Contact [BC in hello Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) tooget this value.</span></span> 
 
4. <span data-ttu-id="3c0fa-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_certificate.png) 

5. <span data-ttu-id="3c0fa-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3c0fa-168">tooconfigure çoklu oturum açma üzerinde **hello bulut BC** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[hello bulut destek ekibi BC](https://www.bcinthecloud.com/supportcenter/).</span><span class="sxs-lookup"><span data-stu-id="3c0fa-168">tooconfigure single sign-on on **BC in hello Cloud** side, you need toosend hello downloaded **Metadata XML** too[BC in hello Cloud support team](https://www.bcinthecloud.com/supportcenter/).</span></span>

> [!TIP]
> <span data-ttu-id="3c0fa-169">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="3c0fa-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3c0fa-170">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3c0fa-171">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3c0fa-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3c0fa-172">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3c0fa-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="3c0fa-173">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="3c0fa-175">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3c0fa-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c0fa-176">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3c0fa-178">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3c0fa-180">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3c0fa-182">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3c0fa-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3c0fa-184">a.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-184">a.</span></span> <span data-ttu-id="3c0fa-185">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3c0fa-186">b.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-186">b.</span></span> <span data-ttu-id="3c0fa-187">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3c0fa-188">c.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-188">c.</span></span> <span data-ttu-id="3c0fa-189">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3c0fa-190">d.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-190">d.</span></span> <span data-ttu-id="3c0fa-191">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-191">Click **Create**.</span></span>
 
### <a name="creating-a-bc-in-hello-cloud-test-user"></a><span data-ttu-id="3c0fa-192">Bir BC hello bulut test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3c0fa-192">Creating a BC in hello Cloud test user</span></span>

<span data-ttu-id="3c0fa-193">Bu bölümde, Britta Simon içinde BC hello bulut adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-193">In this section, you create a user called Britta Simon in BC in hello Cloud.</span></span> <span data-ttu-id="3c0fa-194">Çalışmak [hello bulut istemci destek ekibi BC](https://www.bcinthecloud.com/supportcenter/) hello bulut uygulaması hello BC hello kullanıcılar eklemek için.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-194">Work with [BC in hello Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to add hello users in hello BC in hello Cloud application.</span></span> <span data-ttu-id="3c0fa-195">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3c0fa-196">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="3c0fa-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3c0fa-197">Bu bölümde, erişim tooBC hello bulut içinde vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBC in hello Cloud.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="3c0fa-199">**tooassign Britta Simon tooBC hello bulut içinde hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3c0fa-199">**tooassign Britta Simon tooBC in hello Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c0fa-200">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="3c0fa-202">Merhaba uygulamalar listesinde **hello bulut BC**.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-202">In hello applications list, select **BC in hello Cloud**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_app.png) 

3. <span data-ttu-id="3c0fa-204">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="3c0fa-206">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-206">Click **Add** button.</span></span> <span data-ttu-id="3c0fa-207">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="3c0fa-209">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3c0fa-210">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3c0fa-211">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3c0fa-212">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="3c0fa-212">Testing single sign-on</span></span>

<span data-ttu-id="3c0fa-213">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

 <span data-ttu-id="3c0fa-214">Merhaba bulut hello erişim paneli parçasında hello BC tıklattığınızda hello bulut uygulama otomatik olarak oturum açma BC tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3c0fa-214">When you click hello BC in hello Cloud tile in hello Access Panel, you should get automatically signed-on tooyour BC in hello Cloud application.</span></span> <span data-ttu-id="3c0fa-215">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3c0fa-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3c0fa-216">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3c0fa-216">Additional resources</span></span>

* [<span data-ttu-id="3c0fa-217">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="3c0fa-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3c0fa-218">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="3c0fa-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_203.png

