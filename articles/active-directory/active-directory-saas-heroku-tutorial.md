---
title: "Öğretici: Azure Active Directory Tümleştirme ile Heroku | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Heroku arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d7d72ec6-4a60-4524-8634-26d8fbbcc833
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee11db647fd385140f1dbcab2586dfafffe5d912
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-heroku"></a><span data-ttu-id="72bf2-103">Öğretici: Azure Active Directory Tümleştirme Heroku ile</span><span class="sxs-lookup"><span data-stu-id="72bf2-103">Tutorial: Azure Active Directory integration with Heroku</span></span>

<span data-ttu-id="72bf2-104">Bu öğreticide, bilgi nasıl toointegrate Heroku Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="72bf2-104">In this tutorial, you learn how toointegrate Heroku with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="72bf2-105">Heroku Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="72bf2-105">Integrating Heroku with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="72bf2-106">Erişim tooHeroku sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="72bf2-106">You can control in Azure AD who has access tooHeroku</span></span>
- <span data-ttu-id="72bf2-107">Kullanıcıların tooautomatically get açan tooHeroku (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="72bf2-107">You can enable your users tooautomatically get signed-on tooHeroku (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="72bf2-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="72bf2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="72bf2-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="72bf2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72bf2-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="72bf2-110">Prerequisites</span></span>

<span data-ttu-id="72bf2-111">tooconfigure Heroku ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="72bf2-111">tooconfigure Azure AD integration with Heroku, you need hello following items:</span></span>

- <span data-ttu-id="72bf2-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="72bf2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="72bf2-113">Bir Heroku çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="72bf2-113">A Heroku single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="72bf2-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="72bf2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="72bf2-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="72bf2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="72bf2-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="72bf2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="72bf2-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="72bf2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="72bf2-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="72bf2-118">Scenario description</span></span>
<span data-ttu-id="72bf2-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="72bf2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="72bf2-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="72bf2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="72bf2-121">Merhaba Galerisi'nden Heroku ekleme</span><span class="sxs-lookup"><span data-stu-id="72bf2-121">Adding Heroku from hello gallery</span></span>
2. <span data-ttu-id="72bf2-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="72bf2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-heroku-from-hello-gallery"></a><span data-ttu-id="72bf2-123">Merhaba Galerisi'nden Heroku ekleme</span><span class="sxs-lookup"><span data-stu-id="72bf2-123">Adding Heroku from hello gallery</span></span>
<span data-ttu-id="72bf2-124">Azure AD'ye tooconfigure hello tümleştirme Heroku, tooadd Heroku hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="72bf2-124">tooconfigure hello integration of Heroku into Azure AD, you need tooadd Heroku from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="72bf2-125">**tooadd Heroku hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="72bf2-125">**tooadd Heroku from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="72bf2-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="72bf2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="72bf2-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="72bf2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="72bf2-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="72bf2-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="72bf2-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="72bf2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="72bf2-133">Merhaba arama kutusuna yazın **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="72bf2-133">In hello search box, type **Heroku**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_search.png)

5. <span data-ttu-id="72bf2-135">Merhaba Sonuçlar panelinde seçin **Heroku**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="72bf2-135">In hello results panel, select **Heroku**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="72bf2-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="72bf2-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="72bf2-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Heroku ile test etme</span><span class="sxs-lookup"><span data-stu-id="72bf2-138">In this section, you configure and test Azure AD single sign-on with Heroku based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="72bf2-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Heroku içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="72bf2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Heroku is tooa user in Azure AD.</span></span> <span data-ttu-id="72bf2-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Heroku hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="72bf2-140">In other words, a link relationship between an Azure AD user and hello related user in Heroku needs toobe established.</span></span>

<span data-ttu-id="72bf2-141">Merhaba hello değeri Heroku içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="72bf2-141">In Heroku, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="72bf2-142">tooconfigure ve Heroku ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="72bf2-142">tooconfigure and test Azure AD single sign-on with Heroku, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="72bf2-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="72bf2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="72bf2-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="72bf2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="72bf2-145">**[Heroku test kullanıcısı oluşturma](#creating-a-heroku-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Heroku içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="72bf2-145">**[Creating a Heroku test user](#creating-a-heroku-test-user)** - toohave a counterpart of Britta Simon in Heroku that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="72bf2-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="72bf2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="72bf2-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="72bf2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="72bf2-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="72bf2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="72bf2-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Heroku uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="72bf2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Heroku application.</span></span>

<span data-ttu-id="72bf2-150">**tooconfigure Azure AD çoklu oturum açma ile Heroku, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="72bf2-150">**tooconfigure Azure AD single sign-on with Heroku, perform hello following steps:**</span></span>

1. <span data-ttu-id="72bf2-151">Hello hello üzerinde Azure portal'ın **Heroku** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="72bf2-151">In hello Azure portal, on hello **Heroku** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="72bf2-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="72bf2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_samlbase.png)

3. <span data-ttu-id="72bf2-155">Merhaba üzerinde **Heroku etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="72bf2-155">On hello **Heroku Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_url.png)

    <span data-ttu-id="72bf2-157">a.</span><span class="sxs-lookup"><span data-stu-id="72bf2-157">a.</span></span> <span data-ttu-id="72bf2-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="72bf2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>    
    `https://sso.heroku.com/saml/<company-name>/init`

    <span data-ttu-id="72bf2-159">b.</span><span class="sxs-lookup"><span data-stu-id="72bf2-159">b.</span></span> <span data-ttu-id="72bf2-160">Merhaba, **tanımlayıcı URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="72bf2-160">In hello **Identifier URL** textbox, type a URL using hello following pattern:</span></span>            
    `https://sso.heroku.com/saml/<company-name>`

    > [!NOTE]
    ><span data-ttu-id="72bf2-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="72bf2-161">These values are not real.</span></span> <span data-ttu-id="72bf2-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="72bf2-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="72bf2-163">Bu makalenin sonraki bölümlerinde açıklanan Heroku ekibinden bu değerleri alır.</span><span class="sxs-lookup"><span data-stu-id="72bf2-163">You get these values from Heroku team, which is described in later sections of this article.</span></span> 
        
4. <span data-ttu-id="72bf2-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="72bf2-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_certificate.png) 

5. <span data-ttu-id="72bf2-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="72bf2-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-heroku-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="72bf2-168">tooenable Heroku, SSO hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="72bf2-168">tooenable SSO in Heroku, perform hello following steps:</span></span>
   
    <span data-ttu-id="72bf2-169">a.</span><span class="sxs-lookup"><span data-stu-id="72bf2-169">a.</span></span> <span data-ttu-id="72bf2-170">İçinde toohello Heroku hesabı yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="72bf2-170">Log in toohello Heroku account as an administrator.</span></span>

    <span data-ttu-id="72bf2-171">b.</span><span class="sxs-lookup"><span data-stu-id="72bf2-171">b.</span></span> <span data-ttu-id="72bf2-172">Merhaba tıklatın **ayarları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="72bf2-172">Click hello **Settings** tab.</span></span>

    <span data-ttu-id="72bf2-173">c.</span><span class="sxs-lookup"><span data-stu-id="72bf2-173">c.</span></span> <span data-ttu-id="72bf2-174">Merhaba üzerinde **tek oturum açma sayfasına**, tıklatın **meta veriler karşıya**.</span><span class="sxs-lookup"><span data-stu-id="72bf2-174">On hello **Single Sign On Page**, click **Upload Metadata**.</span></span>

    <span data-ttu-id="72bf2-175">d.</span><span class="sxs-lookup"><span data-stu-id="72bf2-175">d.</span></span> <span data-ttu-id="72bf2-176">Azure portal hello indirmiş hello meta veri dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="72bf2-176">Upload hello metadata file, which you have downloaded from hello Azure portal.</span></span>

    <span data-ttu-id="72bf2-177">e.</span><span class="sxs-lookup"><span data-stu-id="72bf2-177">e.</span></span> <span data-ttu-id="72bf2-178">Merhaba Kurulumu başarılı olduğunda, Yöneticiler bir onay iletişim kutusu bakın ve son kullanıcılar için SSO oturum açma hello hello URL'sini görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="72bf2-178">When hello setup is successful, administrators see a confirmation dialog and hello URL of hello SSO Login for end users is displayed.</span></span> 

    <span data-ttu-id="72bf2-179">f.</span><span class="sxs-lookup"><span data-stu-id="72bf2-179">f.</span></span> <span data-ttu-id="72bf2-180">Kopya hello **Heroku oturum açma URL'si** ve **Heroku varlık kimliği** değerleri ve çok Geri Git**Heroku etki alanı ve URL'leri** bölümünde Azure portalında ve bu değerleri helloyapıştırma**Oturum açma URL'si** ve **tanımlayıcısı** kutularındaki sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="72bf2-180">Copy hello **Heroku Login URL** and **Heroku Entity ID** values and go back too**Heroku Domain and URLs** section in Azure portal and paste these values into hello **Sign-On Url** and **Identifier** textboxes respectively.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_52.png) 
    
8. <span data-ttu-id="72bf2-182">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="72bf2-182">Click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="72bf2-183">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="72bf2-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="72bf2-184">Bu uygulamayı hello ekledikten sonra **Active Directory kuruluş uygulamaları** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="72bf2-184">After adding this app from hello **Active Directory Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="72bf2-185">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="72bf2-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="72bf2-186">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="72bf2-186">Creating an Azure AD test user</span></span>

<span data-ttu-id="72bf2-187">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="72bf2-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="72bf2-189">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="72bf2-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="72bf2-190">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="72bf2-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-heroku-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="72bf2-192">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="72bf2-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-heroku-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="72bf2-194">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="72bf2-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-heroku-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="72bf2-196">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="72bf2-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-heroku-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="72bf2-198">a.</span><span class="sxs-lookup"><span data-stu-id="72bf2-198">a.</span></span> <span data-ttu-id="72bf2-199">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="72bf2-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="72bf2-200">b.</span><span class="sxs-lookup"><span data-stu-id="72bf2-200">b.</span></span> <span data-ttu-id="72bf2-201">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="72bf2-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="72bf2-202">c.</span><span class="sxs-lookup"><span data-stu-id="72bf2-202">c.</span></span> <span data-ttu-id="72bf2-203">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="72bf2-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="72bf2-204">d.</span><span class="sxs-lookup"><span data-stu-id="72bf2-204">d.</span></span> <span data-ttu-id="72bf2-205">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="72bf2-205">Click **Create**.</span></span>
 
### <a name="creating-a-heroku-test-user"></a><span data-ttu-id="72bf2-206">Heroku test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="72bf2-206">Creating a Heroku test user</span></span>

<span data-ttu-id="72bf2-207">Bu bölümde, Heroku içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="72bf2-207">In this section, you create a user called Britta Simon in Heroku.</span></span> <span data-ttu-id="72bf2-208">Heroku yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="72bf2-208">Heroku supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="72bf2-209">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="72bf2-209">There is no action item for you in this section.</span></span> <span data-ttu-id="72bf2-210">Yeni bir kullanıcı hello kullanıcı henüz yoksa Heroku erişirken oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="72bf2-210">A new user is created when accessing Heroku if hello user doesn't exist yet.</span></span> <span data-ttu-id="72bf2-211">Merhaba hesabı sağlandıktan sonra hello son kullanıcı bir doğrulama e-posta alır ve tooclick hello bildirim bağlantı.</span><span class="sxs-lookup"><span data-stu-id="72bf2-211">After hello account is provisioned, hello end user receives a verification email and needs tooclick hello acknowledgement link.</span></span>

>[!NOTE]
><span data-ttu-id="72bf2-212">Toocreate kullanıcı el ile gerekiyorsa, toocontact hello gereksinim [Heroku istemci destek ekibi](https://www.heroku.com/support).</span><span class="sxs-lookup"><span data-stu-id="72bf2-212">If you need toocreate a user manually, you need toocontact hello [Heroku Client support team](https://www.heroku.com/support).</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="72bf2-213">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="72bf2-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="72bf2-214">Bu bölümde, erişim tooHeroku vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="72bf2-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHeroku.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="72bf2-216">**tooassign Britta Simon tooHeroku hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="72bf2-216">**tooassign Britta Simon tooHeroku, perform hello following steps:**</span></span>

1. <span data-ttu-id="72bf2-217">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="72bf2-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="72bf2-219">Merhaba uygulamalar listesinde **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="72bf2-219">In hello applications list, select **Heroku**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_app.png) 

3. <span data-ttu-id="72bf2-221">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="72bf2-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="72bf2-223">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="72bf2-223">Click **Add** button.</span></span> <span data-ttu-id="72bf2-224">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="72bf2-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="72bf2-226">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="72bf2-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="72bf2-227">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="72bf2-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="72bf2-228">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="72bf2-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="72bf2-229">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="72bf2-229">Testing single sign-on</span></span>

<span data-ttu-id="72bf2-230">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="72bf2-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="72bf2-231">Merhaba Heroku hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Heroku uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="72bf2-231">When you click hello Heroku tile in hello Access Panel, you should get automatically signed-on tooyour Heroku application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="72bf2-232">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="72bf2-232">Additional resources</span></span>

* [<span data-ttu-id="72bf2-233">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="72bf2-233">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="72bf2-234">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="72bf2-234">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_203.png
