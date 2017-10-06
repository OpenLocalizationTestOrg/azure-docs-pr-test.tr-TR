---
title: "Öğretici: Azure Active Directory Tümleştirme ile varlık banka | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve varlık banka arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3006ad6e-8831-41cd-94aa-7e7ae770ce7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 32cb355fbe16557eca69dbad1d3e6fbe19b53517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asset-bank"></a><span data-ttu-id="93d59-103">Öğretici: Varlık banka Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="93d59-103">Tutorial: Azure Active Directory integration with Asset Bank</span></span>

<span data-ttu-id="93d59-104">Bu öğreticide, bilgi toointegrate varlık banka nasıl Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="93d59-104">In this tutorial, you learn how toointegrate Asset Bank with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="93d59-105">Azure AD ile tümleştirme varlık banka ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="93d59-105">Integrating Asset Bank with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="93d59-106">Erişim tooAsset banka sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="93d59-106">You can control in Azure AD who has access tooAsset Bank</span></span>
- <span data-ttu-id="93d59-107">Kullanıcıların tooautomatically get açan tooAsset banka (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="93d59-107">You can enable your users tooautomatically get signed-on tooAsset Bank (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="93d59-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="93d59-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="93d59-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="93d59-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93d59-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="93d59-110">Prerequisites</span></span>

<span data-ttu-id="93d59-111">tooconfigure varlık banka ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="93d59-111">tooconfigure Azure AD integration with Asset Bank, you need hello following items:</span></span>

- <span data-ttu-id="93d59-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="93d59-112">An Azure AD subscription</span></span>
- <span data-ttu-id="93d59-113">Bir varlık banka çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="93d59-113">An Asset Bank single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="93d59-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="93d59-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="93d59-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="93d59-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="93d59-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="93d59-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="93d59-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="93d59-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="93d59-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="93d59-118">Scenario description</span></span>
<span data-ttu-id="93d59-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="93d59-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="93d59-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="93d59-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="93d59-121">Ekleme varlık banka hello Galeriden</span><span class="sxs-lookup"><span data-stu-id="93d59-121">Adding Asset Bank from hello gallery</span></span>
2. <span data-ttu-id="93d59-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="93d59-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asset-bank-from-hello-gallery"></a><span data-ttu-id="93d59-123">Ekleme varlık banka hello Galeriden</span><span class="sxs-lookup"><span data-stu-id="93d59-123">Adding Asset Bank from hello gallery</span></span>
<span data-ttu-id="93d59-124">Azure AD'ye tooconfigure hello tümleştirme varlık bankanın tooadd varlık banka hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="93d59-124">tooconfigure hello integration of Asset Bank into Azure AD, you need tooadd Asset Bank from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="93d59-125">**tooadd varlık banka hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="93d59-125">**tooadd Asset Bank from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="93d59-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="93d59-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="93d59-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="93d59-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="93d59-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="93d59-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="93d59-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="93d59-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="93d59-133">Merhaba arama kutusuna yazın **varlık banka**.</span><span class="sxs-lookup"><span data-stu-id="93d59-133">In hello search box, type **Asset Bank**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_search.png)

5. <span data-ttu-id="93d59-135">Merhaba Sonuçlar panelinde seçin **varlık banka**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="93d59-135">In hello results panel, select **Asset Bank**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="93d59-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="93d59-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="93d59-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma varlık "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı banka ile test etme</span><span class="sxs-lookup"><span data-stu-id="93d59-138">In this section, you configure and test Azure AD single sign-on with Asset Bank based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="93d59-139">Tek toowork'ın oturum açma hangi hello karşılık gelen varlık banka içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="93d59-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Asset Bank is tooa user in Azure AD.</span></span> <span data-ttu-id="93d59-140">Diğer bir deyişle, bir Azure AD kullanıcı ve varlık banka hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="93d59-140">In other words, a link relationship between an Azure AD user and hello related user in Asset Bank needs toobe established.</span></span>

<span data-ttu-id="93d59-141">Varlık Bank'hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="93d59-141">In Asset Bank, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="93d59-142">tooconfigure ve varlık banka ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="93d59-142">tooconfigure and test Azure AD single sign-on with Asset Bank, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="93d59-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="93d59-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="93d59-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="93d59-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="93d59-145">**[Bir varlık banka test kullanıcısı oluşturma](#creating-an-asset-bank-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir varlık banka içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="93d59-145">**[Creating an Asset Bank test user](#creating-an-asset-bank-test-user)** - toohave a counterpart of Britta Simon in Asset Bank that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="93d59-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="93d59-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="93d59-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="93d59-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="93d59-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="93d59-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="93d59-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma varlık banka uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="93d59-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Asset Bank application.</span></span>

<span data-ttu-id="93d59-150">**tooconfigure Azure AD çoklu oturum açma varlık banka ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="93d59-150">**tooconfigure Azure AD single sign-on with Asset Bank, perform hello following steps:**</span></span>

1. <span data-ttu-id="93d59-151">Merhaba hello üzerinde Azure portal'ın **varlık banka** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="93d59-151">In hello Azure portal, on hello **Asset Bank** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="93d59-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="93d59-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_samlbase.png)

3. <span data-ttu-id="93d59-155">Merhaba üzerinde **varlık banka etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="93d59-155">On hello **Asset Bank Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_url.png)

    <span data-ttu-id="93d59-157">a.</span><span class="sxs-lookup"><span data-stu-id="93d59-157">a.</span></span> <span data-ttu-id="93d59-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.assetbank-server.com`</span><span class="sxs-lookup"><span data-stu-id="93d59-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.assetbank-server.com`</span></span>

    <span data-ttu-id="93d59-159">b.</span><span class="sxs-lookup"><span data-stu-id="93d59-159">b.</span></span> <span data-ttu-id="93d59-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.assetbank-server.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="93d59-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.assetbank-server.com/shibboleth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="93d59-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="93d59-161">These values are not real.</span></span> <span data-ttu-id="93d59-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="93d59-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="93d59-163">Kişi [varlık banka istemci destek ekibi](mailto:support@assetbank.co.uk) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="93d59-163">Contact [Asset Bank Client support team](mailto:support@assetbank.co.uk) tooget these values.</span></span> 
 
4. <span data-ttu-id="93d59-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="93d59-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_certificate.png) 

5. <span data-ttu-id="93d59-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="93d59-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-assetbank-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="93d59-168">tooconfigure çoklu oturum açma üzerinde **varlık banka** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[varlık banka destek ekibi](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="93d59-168">tooconfigure single sign-on on **Asset Bank** side, you need toosend hello downloaded **Metadata XML** too[Asset Bank support team](mailto:support@assetbank.co.uk).</span></span> 


> [!TIP]
> <span data-ttu-id="93d59-169">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="93d59-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="93d59-170">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="93d59-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="93d59-171">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="93d59-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="93d59-172">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="93d59-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="93d59-173">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="93d59-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="93d59-175">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="93d59-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="93d59-176">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="93d59-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-assetbank-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="93d59-178">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="93d59-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-assetbank-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="93d59-180">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="93d59-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-assetbank-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="93d59-182">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="93d59-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-assetbank-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="93d59-184">a.</span><span class="sxs-lookup"><span data-stu-id="93d59-184">a.</span></span> <span data-ttu-id="93d59-185">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="93d59-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="93d59-186">b.</span><span class="sxs-lookup"><span data-stu-id="93d59-186">b.</span></span> <span data-ttu-id="93d59-187">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="93d59-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="93d59-188">c.</span><span class="sxs-lookup"><span data-stu-id="93d59-188">c.</span></span> <span data-ttu-id="93d59-189">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="93d59-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="93d59-190">d.</span><span class="sxs-lookup"><span data-stu-id="93d59-190">d.</span></span> <span data-ttu-id="93d59-191">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="93d59-191">Click **Create**.</span></span>
 
### <a name="creating-an-asset-bank-test-user"></a><span data-ttu-id="93d59-192">Bir varlık banka test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="93d59-192">Creating an Asset Bank test user</span></span>

<span data-ttu-id="93d59-193">Bu bölümde Hello amacı toocreate Britta Simon varlık Bank'adlı kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="93d59-193">hello objective of this section is toocreate a user called Britta Simon in Asset Bank.</span></span> <span data-ttu-id="93d59-194">Varlık banka yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="93d59-194">Asset Bank supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="93d59-195">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="93d59-195">There is no action item for you in this section.</span></span> <span data-ttu-id="93d59-196">Henüz yoksa yeni bir kullanıcı bir girişim tooaccess varlık banka sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="93d59-196">A new user is created during an attempt tooaccess Asset Bank if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="93d59-197">Toocreate kullanıcı el ile gerekiyorsa, toocontact hello gereksinim [varlık banka destek ekibi](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="93d59-197">If you need toocreate a user manually, you need toocontact hello [Asset Bank support team](mailto:support@assetbank.co.uk).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="93d59-198">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="93d59-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="93d59-199">Bu bölümde, erişim tooAsset banka vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="93d59-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAsset Bank.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="93d59-201">**tooassign Britta Simon tooAsset banka, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="93d59-201">**tooassign Britta Simon tooAsset Bank, perform hello following steps:**</span></span>

1. <span data-ttu-id="93d59-202">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="93d59-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="93d59-204">Merhaba uygulamalar listesinde **varlık banka**.</span><span class="sxs-lookup"><span data-stu-id="93d59-204">In hello applications list, select **Asset Bank**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_app.png) 

3. <span data-ttu-id="93d59-206">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="93d59-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="93d59-208">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="93d59-208">Click **Add** button.</span></span> <span data-ttu-id="93d59-209">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="93d59-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="93d59-211">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="93d59-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="93d59-212">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="93d59-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="93d59-213">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="93d59-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="93d59-214">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="93d59-214">Testing single sign-on</span></span>

<span data-ttu-id="93d59-215">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="93d59-215">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="93d59-216">Merhaba varlık banka hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour varlık banka uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="93d59-216">When you click hello Asset Bank tile in hello Access Panel, you should get automatically signed-on tooyour Asset Bank application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="93d59-217">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="93d59-217">Additional resources</span></span>

* [<span data-ttu-id="93d59-218">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="93d59-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="93d59-219">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="93d59-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_203.png

