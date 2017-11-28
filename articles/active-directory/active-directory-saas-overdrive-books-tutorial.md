---
title: "Öğretici: Azure Active Directory Tümleştirme Overdrive ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Overdrive arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e68cede7-1130-4813-bd55-22a9a6fc6bf5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: b0aafacdedee25587132fc88ff93829f4367b0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-overdrive"></a><span data-ttu-id="9ccfd-103">Öğretici: Azure Active Directory Tümleştirme Overdrive ile</span><span class="sxs-lookup"><span data-stu-id="9ccfd-103">Tutorial: Azure Active Directory integration with Overdrive</span></span> 

<span data-ttu-id="9ccfd-104">Bu öğreticide, bilgi nasıl toointegrate Overdrive Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-104">In this tutorial, you learn how toointegrate Overdrive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9ccfd-105">Overdrive Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="9ccfd-105">Integrating Overdrive with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9ccfd-106">Erişim tooOverdrive sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="9ccfd-106">You can control in Azure AD who has access tooOverdrive</span></span> 
- <span data-ttu-id="9ccfd-107">Kullanıcıların tooautomatically get açan tooOverdrive (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="9ccfd-107">You can enable your users tooautomatically get signed-on tooOverdrive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9ccfd-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="9ccfd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9ccfd-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9ccfd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ccfd-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9ccfd-110">Prerequisites</span></span>

<span data-ttu-id="9ccfd-111">tooconfigure Overdrive ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="9ccfd-111">tooconfigure Azure AD integration with Overdrive, you need hello following items:</span></span>

- <span data-ttu-id="9ccfd-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="9ccfd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9ccfd-113">Bir Overdrive çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="9ccfd-113">An Overdrive single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9ccfd-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9ccfd-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="9ccfd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9ccfd-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9ccfd-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9ccfd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9ccfd-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="9ccfd-118">Scenario description</span></span>
<span data-ttu-id="9ccfd-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9ccfd-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="9ccfd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9ccfd-121">Merhaba Galerisi'nden Overdrive ekleme</span><span class="sxs-lookup"><span data-stu-id="9ccfd-121">Adding Overdrive from hello gallery</span></span>
2. <span data-ttu-id="9ccfd-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="9ccfd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-overdrive-from-hello-gallery"></a><span data-ttu-id="9ccfd-123">Merhaba Galerisi'nden Overdrive ekleme</span><span class="sxs-lookup"><span data-stu-id="9ccfd-123">Adding Overdrive from hello gallery</span></span>
<span data-ttu-id="9ccfd-124">Azure AD'ye Overdrive tooconfigure hello tümleştirilmesi, tooadd Overdrive hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-124">tooconfigure hello integration of Overdrive into Azure AD, you need tooadd Overdrive from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9ccfd-125">**tooadd hello galerisinden Overdrive hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9ccfd-125">**tooadd Overdrive from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ccfd-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9ccfd-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9ccfd-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="9ccfd-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="9ccfd-133">Merhaba arama kutusuna yazın **Overdrive**.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-133">In hello search box, type **Overdrive**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_search.png)

5. <span data-ttu-id="9ccfd-135">Merhaba Sonuçlar panelinde seçin **Overdrive**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-135">In hello results panel, select **Overdrive**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9ccfd-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="9ccfd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9ccfd-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Overdrive sınayın.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-138">In this section, you configure and test Azure AD single sign-on with Overdrive based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9ccfd-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Overdrive içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Overdrive is tooa user in Azure AD.</span></span> <span data-ttu-id="9ccfd-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Overdrive hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-140">In other words, a link relationship between an Azure AD user and hello related user in Overdrive needs toobe established.</span></span>

<span data-ttu-id="9ccfd-141">Merhaba hello değeri Overdrive içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-141">In Overdrive, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9ccfd-142">tooconfigure ve Overdrive ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="9ccfd-142">tooconfigure and test Azure AD single sign-on with Overdrive, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9ccfd-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9ccfd-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9ccfd-145">**[Bir Overdrive test kullanıcısı oluşturma](#creating-an-overdrive-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Overdrive içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-145">**[Creating an Overdrive test user](#creating-an-overdrive-test-user)** - toohave a counterpart of Britta Simon in Overdrive that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9ccfd-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9ccfd-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9ccfd-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9ccfd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9ccfd-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Overdrive uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Overdrive  application.</span></span>

<span data-ttu-id="9ccfd-150">**tooconfigure Azure AD çoklu oturum açma ile Overdrive, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9ccfd-150">**tooconfigure Azure AD single sign-on with Overdrive, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ccfd-151">Hello hello üzerinde Azure portal'ın **Overdrive** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-151">In hello Azure portal, on hello **Overdrive** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="9ccfd-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_samlbase.png)

3. <span data-ttu-id="9ccfd-155">Merhaba üzerinde **Overdrive etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9ccfd-155">On hello **Overdrive Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_url.png)

    <span data-ttu-id="9ccfd-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`http://<subdomain>.libraryreserve.com`</span><span class="sxs-lookup"><span data-stu-id="9ccfd-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<subdomain>.libraryreserve.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9ccfd-158">Merhaba değeri gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-158">hello value is not real.</span></span> <span data-ttu-id="9ccfd-159">Güncelleştirme hello değerle hello gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="9ccfd-160">Kişi [Overdrive istemci destek ekibi](https://help.overdrive.com/) tooget hello değeri.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-160">Contact [Overdrive Client support team](https://help.overdrive.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="9ccfd-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_certificate.png) 

5. <span data-ttu-id="9ccfd-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9ccfd-165">tooconfigure çoklu oturum açma üzerinde **Overdrive** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[Overdrive destek ekibi](https://help.overdrive.com/).</span><span class="sxs-lookup"><span data-stu-id="9ccfd-165">tooconfigure single sign-on on **Overdrive** side, you need toosend hello downloaded **Metadata XML** too[Overdrive support team](https://help.overdrive.com/).</span></span> <span data-ttu-id="9ccfd-166">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9ccfd-167">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="9ccfd-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9ccfd-168">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9ccfd-169">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9ccfd-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9ccfd-170">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ccfd-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="9ccfd-171">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="9ccfd-173">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9ccfd-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ccfd-174">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9ccfd-176">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9ccfd-178">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9ccfd-180">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9ccfd-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9ccfd-182">a.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-182">a.</span></span> <span data-ttu-id="9ccfd-183">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9ccfd-184">b.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-184">b.</span></span> <span data-ttu-id="9ccfd-185">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9ccfd-186">c.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-186">c.</span></span> <span data-ttu-id="9ccfd-187">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9ccfd-188">d.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-188">d.</span></span> <span data-ttu-id="9ccfd-189">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-189">Click **Create**.</span></span>
 
### <a name="creating-an-overdrive-test-user"></a><span data-ttu-id="9ccfd-190">Bir Overdrive test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ccfd-190">Creating an Overdrive test user</span></span>

<span data-ttu-id="9ccfd-191">TooOverDrive sağlama, tooconfigure kullanıcı için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-191">There is no action item for you tooconfigure user provisioning tooOverDrive.</span></span>  

<span data-ttu-id="9ccfd-192">Atanan kullanıcı çalıştığında toolog zaman tooOverDrive OverDrive hesap gerekirse, otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-192">When an assigned user tries toolog in tooOverDrive, an OverDrive account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="9ccfd-193">API AAD kullanıcı hesapları OverDrive tooprovision tarafından sağlanan veya herhangi diğer OverDrive kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-193">You can use any other OverDrive user account creation tools or APIs provided by OverDrive tooprovision AAD user accounts.</span></span>
>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9ccfd-194">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="9ccfd-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9ccfd-195">Bu bölümde, erişim tooOverdrive vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOverdrive.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="9ccfd-197">**tooassign Britta Simon tooOverdrive hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9ccfd-197">**tooassign Britta Simon tooOverdrive, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ccfd-198">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="9ccfd-200">Merhaba uygulamalar listesinde **Overdrive**.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-200">In hello applications list, select **Overdrive**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_app.png) 

3. <span data-ttu-id="9ccfd-202">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="9ccfd-204">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-204">Click **Add** button.</span></span> <span data-ttu-id="9ccfd-205">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="9ccfd-207">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9ccfd-208">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9ccfd-209">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9ccfd-210">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="9ccfd-210">Testing single sign-on</span></span>

<span data-ttu-id="9ccfd-211">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-211">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9ccfd-212">Merhaba Overdrive hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Overdrive uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ccfd-212">When you click hello Overdrive tile in hello Access Panel, you should get automatically signed-on tooyour Overdrive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9ccfd-213">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="9ccfd-213">Additional resources</span></span>

* [<span data-ttu-id="9ccfd-214">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="9ccfd-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9ccfd-215">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="9ccfd-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_203.png

