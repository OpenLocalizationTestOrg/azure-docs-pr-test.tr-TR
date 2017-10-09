---
title: "Öğretici: Azure Active Directory Tümleştirme ile AppBlade | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile AppBlade arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3360d7aa-6518-4f99-88bd-b7f7258183e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 06f3d8fcee97945c867bca6f3aebe15ecef04617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appblade"></a><span data-ttu-id="f53b4-103">Öğretici: Azure Active Directory Tümleştirme AppBlade ile</span><span class="sxs-lookup"><span data-stu-id="f53b4-103">Tutorial: Azure Active Directory integration with AppBlade</span></span>

<span data-ttu-id="f53b4-104">Bu öğreticide, bilgi nasıl toointegrate AppBlade Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f53b4-104">In this tutorial, you learn how toointegrate AppBlade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f53b4-105">AppBlade Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="f53b4-105">Integrating AppBlade with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f53b4-106">Erişim tooAppBlade sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f53b4-106">You can control in Azure AD who has access tooAppBlade</span></span>
- <span data-ttu-id="f53b4-107">Kullanıcıların tooautomatically get açan tooAppBlade (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f53b4-107">You can enable your users tooautomatically get signed-on tooAppBlade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f53b4-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="f53b4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f53b4-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f53b4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f53b4-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f53b4-110">Prerequisites</span></span>

<span data-ttu-id="f53b4-111">tooconfigure AppBlade ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="f53b4-111">tooconfigure Azure AD integration with AppBlade, you need hello following items:</span></span>

- <span data-ttu-id="f53b4-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="f53b4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f53b4-113">Bir AppBlade çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="f53b4-113">An AppBlade single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f53b4-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="f53b4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f53b4-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="f53b4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f53b4-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="f53b4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f53b4-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f53b4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f53b4-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="f53b4-118">Scenario description</span></span>
<span data-ttu-id="f53b4-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="f53b4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f53b4-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="f53b4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f53b4-121">Merhaba Galerisi'nden AppBlade ekleme</span><span class="sxs-lookup"><span data-stu-id="f53b4-121">Adding AppBlade from hello gallery</span></span>
2. <span data-ttu-id="f53b4-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f53b4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appblade-from-hello-gallery"></a><span data-ttu-id="f53b4-123">Merhaba Galerisi'nden AppBlade ekleme</span><span class="sxs-lookup"><span data-stu-id="f53b4-123">Adding AppBlade from hello gallery</span></span>
<span data-ttu-id="f53b4-124">Azure AD'ye tooconfigure hello tümleştirme AppBlade, tooadd AppBlade hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="f53b4-124">tooconfigure hello integration of AppBlade into Azure AD, you need tooadd AppBlade from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f53b4-125">**tooadd AppBlade hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f53b4-125">**tooadd AppBlade from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f53b4-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f53b4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f53b4-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="f53b4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f53b4-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f53b4-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="f53b4-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f53b4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="f53b4-133">Merhaba arama kutusuna yazın **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="f53b4-133">In hello search box, type **AppBlade**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_search.png)

5. <span data-ttu-id="f53b4-135">Merhaba Sonuçlar panelinde seçin **AppBlade**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="f53b4-135">In hello results panel, select **AppBlade**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f53b4-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f53b4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f53b4-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı AppBlade ile test etme</span><span class="sxs-lookup"><span data-stu-id="f53b4-138">In this section, you configure and test Azure AD single sign-on with AppBlade based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f53b4-139">Tek toowork'ın oturum açma hangi hello karşılık gelen AppBlade içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="f53b4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AppBlade is tooa user in Azure AD.</span></span> <span data-ttu-id="f53b4-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı AppBlade hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="f53b4-140">In other words, a link relationship between an Azure AD user and hello related user in AppBlade needs toobe established.</span></span>

<span data-ttu-id="f53b4-141">Merhaba hello değeri AppBlade içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="f53b4-141">In AppBlade, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f53b4-142">tooconfigure ve AppBlade ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="f53b4-142">tooconfigure and test Azure AD single sign-on with AppBlade, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f53b4-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="f53b4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f53b4-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="f53b4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f53b4-145">**[Bir AppBlade test kullanıcısı oluşturma](#creating-an-appblade-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir AppBlade içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="f53b4-145">**[Creating an AppBlade test user](#creating-an-appblade-test-user)** - toohave a counterpart of Britta Simon in AppBlade that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f53b4-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="f53b4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f53b4-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="f53b4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f53b4-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f53b4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f53b4-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma AppBlade uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f53b4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AppBlade application.</span></span>

<span data-ttu-id="f53b4-150">**tooconfigure Azure AD çoklu oturum açma ile AppBlade, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f53b4-150">**tooconfigure Azure AD single sign-on with AppBlade, perform hello following steps:**</span></span>

1. <span data-ttu-id="f53b4-151">Hello hello üzerinde Azure portal'ın **AppBlade** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="f53b4-151">In hello Azure portal, on hello **AppBlade** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="f53b4-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="f53b4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_samlbase.png)

3. <span data-ttu-id="f53b4-155">Merhaba üzerinde **AppBlade etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f53b4-155">On hello **AppBlade Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_url.png)

    <span data-ttu-id="f53b4-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.appblade.com/saml/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="f53b4-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.appblade.com/saml/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f53b4-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="f53b4-158">This value is not real.</span></span> <span data-ttu-id="f53b4-159">Güncelleştirme hello değerle hello gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="f53b4-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="f53b4-160">Kişi [AppBlade istemci destek ekibi](mailto:support@appblade.com) tooget hello değeri.</span><span class="sxs-lookup"><span data-stu-id="f53b4-160">Contact [AppBlade Client support team](mailto:support@appblade.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="f53b4-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f53b4-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_certificate.png) 

5. <span data-ttu-id="f53b4-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f53b4-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-appblade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f53b4-165">tooconfigure çoklu oturum açma üzerinde **AppBlade** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[AppBlade destek ekibi](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="f53b4-165">tooconfigure single sign-on on **AppBlade** side, you need toosend hello downloaded **Metadata XML** too[AppBlade support team](mailto:support@appblade.com).</span></span> <span data-ttu-id="f53b4-166">Ayrıca, lütfen tooconfigure hello isteyin **SSO veren URL'si** olarak `https://appblade.com/saml`.</span><span class="sxs-lookup"><span data-stu-id="f53b4-166">Also, please ask them tooconfigure hello **SSO Issuer URL** as `https://appblade.com/saml`.</span></span> <span data-ttu-id="f53b4-167">Bu ayar için çoklu oturum açma toowork gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f53b4-167">This setting is required for single sign-on toowork.</span></span>


> [!TIP]
> <span data-ttu-id="f53b4-168">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="f53b4-168">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f53b4-169">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="f53b4-169">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f53b4-170">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f53b4-170">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f53b4-171">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f53b4-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="f53b4-172">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="f53b4-172">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="f53b4-174">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f53b4-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f53b4-175">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f53b4-175">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-appblade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f53b4-177">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f53b4-177">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-appblade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f53b4-179">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="f53b4-179">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-appblade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f53b4-181">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f53b4-181">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-appblade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f53b4-183">a.</span><span class="sxs-lookup"><span data-stu-id="f53b4-183">a.</span></span> <span data-ttu-id="f53b4-184">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f53b4-184">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f53b4-185">b.</span><span class="sxs-lookup"><span data-stu-id="f53b4-185">b.</span></span> <span data-ttu-id="f53b4-186">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="f53b4-186">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f53b4-187">c.</span><span class="sxs-lookup"><span data-stu-id="f53b4-187">c.</span></span> <span data-ttu-id="f53b4-188">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="f53b4-188">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f53b4-189">d.</span><span class="sxs-lookup"><span data-stu-id="f53b4-189">d.</span></span> <span data-ttu-id="f53b4-190">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f53b4-190">Click **Create**.</span></span>
 
### <a name="creating-an-appblade-test-user"></a><span data-ttu-id="f53b4-191">Bir AppBlade test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f53b4-191">Creating an AppBlade test user</span></span>

<span data-ttu-id="f53b4-192">Bu bölümde Hello amacı toocreate Britta Simon içinde AppBlade adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="f53b4-192">hello objective of this section is toocreate a user called Britta Simon in AppBlade.</span></span> <span data-ttu-id="f53b4-193">AppBlade yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="f53b4-193">AppBlade supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="f53b4-194">**Kullanıcı sağlama için etki alanı adınızı AppBlade ile yapılandırıldığından emin olun. Works sağlama yalnızca hello yalnızca zaman kullanıcı sonra.**</span><span class="sxs-lookup"><span data-stu-id="f53b4-194">**Make sure that your domain name is configured with AppBlade for user provisioning. After that only hello just-in-time user provisioning works.**</span></span>

<span data-ttu-id="f53b4-195">Hello kullanıcının hello kullanıcı otomatik olarak belirttiğiniz hello izin düzeyine sahip bir üye olarak hello hesap katılacak sonra AppBlade tarafından hesabınız için yapılandırılan hello etki alanı ile biten bir e-posta adresi varsa, "Temel" (yalnızca yükleyebilmek için bir temel kullanıcı biri mi uygulamalar için), "Ekip üyesine" (yeni uygulama sürümleri karşıya ve projeleri yönetme bir kullanıcı) ya da "Yönetici" (tam yönetici ayrıcalıkları toohello hesabı).</span><span class="sxs-lookup"><span data-stu-id="f53b4-195">If hello user has an email address ending with hello domain configured by AppBlade for your account, then hello user will automatically join hello account as a member with hello permission level you specify, which is one of "Basic" (a basic user who can only install applications), "Team Member" (a user who can upload new app versions and manage projects), or "Administrator" (full admin privileges toohello account).</span></span> <span data-ttu-id="f53b4-196">Normalde bir Basic seçin ve sonra kullanıcıların bir yönetici oturum açma aracılığıyla el ile yükseltmeniz (AppBlade tooconfigure ya da, bir yönetici e-posta tabanlı oturum açma önceden gerekiyor veya bir kullanıcı oturum açtıktan sonra hello müşteri adına Yükselt).</span><span class="sxs-lookup"><span data-stu-id="f53b4-196">Normally one would choose Basic and then promote users manually via an Admin login (AppBlade needs tooconfigure either an email-based admin login in advance or promote a user on behalf of hello customer after login).</span></span>

<span data-ttu-id="f53b4-197">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="f53b4-197">There is no action item for you in this section.</span></span> <span data-ttu-id="f53b4-198">Henüz yoksa yeni bir kullanıcı bir girişim tooaccess AppBlade sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f53b4-198">A new user is created during an attempt tooaccess AppBlade if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="f53b4-199">Toocreate kullanıcı el ile gerekiyorsa, toocontact hello gereksinim [AppBlade destek ekibi](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="f53b4-199">If you need toocreate a user manually, you need toocontact hello [AppBlade support team](mailto:support@appblade.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f53b4-200">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="f53b4-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f53b4-201">Bu bölümde, erişim tooAppBlade vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f53b4-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAppBlade.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="f53b4-203">**tooassign Britta Simon tooAppBlade hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f53b4-203">**tooassign Britta Simon tooAppBlade, perform hello following steps:**</span></span>

1. <span data-ttu-id="f53b4-204">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f53b4-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="f53b4-206">Merhaba uygulamalar listesinde **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="f53b4-206">In hello applications list, select **AppBlade**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_app.png) 

3. <span data-ttu-id="f53b4-208">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="f53b4-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="f53b4-210">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f53b4-210">Click **Add** button.</span></span> <span data-ttu-id="f53b4-211">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f53b4-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="f53b4-213">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="f53b4-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f53b4-214">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f53b4-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f53b4-215">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f53b4-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f53b4-216">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="f53b4-216">Testing single sign-on</span></span>

<span data-ttu-id="f53b4-217">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="f53b4-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="f53b4-218">Merhaba AppBlade hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour AppBlade uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f53b4-218">When you click hello AppBlade tile in hello Access Panel, you should get automatically signed-on tooyour AppBlade application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f53b4-219">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f53b4-219">Additional resources</span></span>

* [<span data-ttu-id="f53b4-220">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="f53b4-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f53b4-221">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="f53b4-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_203.png

