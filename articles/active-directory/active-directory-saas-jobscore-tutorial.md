---
title: "Öğretici: Azure Active Directory Tümleştirme ile JobScore | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile JobScore arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f51b32-e55c-4c66-96e8-50a2f9c2194a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6693a5fd96bfd7fbcd7197983b5f04d061970bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscore"></a><span data-ttu-id="ec6a8-103">Öğretici: Azure Active Directory Tümleştirme JobScore ile</span><span class="sxs-lookup"><span data-stu-id="ec6a8-103">Tutorial: Azure Active Directory integration with JobScore</span></span>

<span data-ttu-id="ec6a8-104">Bu öğreticide, bilgi nasıl toointegrate JobScore Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ec6a8-104">In this tutorial, you learn how toointegrate JobScore with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ec6a8-105">JobScore Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="ec6a8-105">Integrating JobScore with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ec6a8-106">Erişim tooJobScore sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ec6a8-106">You can control in Azure AD who has access tooJobScore</span></span>
- <span data-ttu-id="ec6a8-107">Kullanıcıların tooautomatically get açan tooJobScore (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ec6a8-107">You can enable your users tooautomatically get signed-on tooJobScore (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ec6a8-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="ec6a8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ec6a8-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ec6a8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec6a8-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ec6a8-110">Prerequisites</span></span>

<span data-ttu-id="ec6a8-111">tooconfigure JobScore ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="ec6a8-111">tooconfigure Azure AD integration with JobScore, you need hello following items:</span></span>

- <span data-ttu-id="ec6a8-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="ec6a8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ec6a8-113">Bir JobScore çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="ec6a8-113">A JobScore single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ec6a8-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ec6a8-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="ec6a8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ec6a8-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ec6a8-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ec6a8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ec6a8-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="ec6a8-118">Scenario description</span></span>
<span data-ttu-id="ec6a8-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ec6a8-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="ec6a8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ec6a8-121">Merhaba Galerisi'nden JobScore ekleme</span><span class="sxs-lookup"><span data-stu-id="ec6a8-121">Adding JobScore from hello gallery</span></span>
2. <span data-ttu-id="ec6a8-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ec6a8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscore-from-hello-gallery"></a><span data-ttu-id="ec6a8-123">Merhaba Galerisi'nden JobScore ekleme</span><span class="sxs-lookup"><span data-stu-id="ec6a8-123">Adding JobScore from hello gallery</span></span>
<span data-ttu-id="ec6a8-124">Azure AD'ye tooconfigure hello tümleştirme JobScore, tooadd JobScore hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-124">tooconfigure hello integration of JobScore into Azure AD, you need tooadd JobScore from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ec6a8-125">**tooadd JobScore hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ec6a8-125">**tooadd JobScore from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec6a8-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ec6a8-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ec6a8-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="ec6a8-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="ec6a8-133">Merhaba arama kutusuna yazın **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-133">In hello search box, type **JobScore**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_search.png)

5. <span data-ttu-id="ec6a8-135">Merhaba Sonuçlar panelinde seçin **JobScore**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-135">In hello results panel, select **JobScore**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ec6a8-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ec6a8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ec6a8-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı JobScore ile test etme</span><span class="sxs-lookup"><span data-stu-id="ec6a8-138">In this section, you configure and test Azure AD single sign-on with JobScore based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ec6a8-139">Tek toowork'ın oturum açma hangi hello karşılık gelen JobScore içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in JobScore is tooa user in Azure AD.</span></span> <span data-ttu-id="ec6a8-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı JobScore hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-140">In other words, a link relationship between an Azure AD user and hello related user in JobScore needs toobe established.</span></span>

<span data-ttu-id="ec6a8-141">Merhaba hello değeri JobScore içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-141">In JobScore, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ec6a8-142">tooconfigure ve JobScore ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="ec6a8-142">tooconfigure and test Azure AD single sign-on with JobScore, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ec6a8-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ec6a8-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ec6a8-145">**[JobScore test kullanıcısı oluşturma](#creating-a-jobscore-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir JobScore içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-145">**[Creating a JobScore test user](#creating-a-jobscore-test-user)** - toohave a counterpart of Britta Simon in JobScore that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ec6a8-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ec6a8-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ec6a8-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ec6a8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ec6a8-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma JobScore uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your JobScore application.</span></span>

<span data-ttu-id="ec6a8-150">**tooconfigure Azure AD çoklu oturum açma ile JobScore, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ec6a8-150">**tooconfigure Azure AD single sign-on with JobScore, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec6a8-151">Hello hello üzerinde Azure portal'ın **JobScore** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-151">In hello Azure portal, on hello **JobScore** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="ec6a8-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_samlbase.png)

3. <span data-ttu-id="ec6a8-155">Merhaba üzerinde **JobScore etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ec6a8-155">On hello **JobScore Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_url.png)

    <span data-ttu-id="ec6a8-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://hire.jobscore.com/auth/adfs/<company name>`</span><span class="sxs-lookup"><span data-stu-id="ec6a8-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://hire.jobscore.com/auth/adfs/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ec6a8-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-158">This value is not real.</span></span> <span data-ttu-id="ec6a8-159">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="ec6a8-160">Kişi [JobScore istemci destek ekibi](mailto:support@jobscore.com) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-160">Contact [JobScore Client support team](mailto:support@jobscore.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="ec6a8-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_certificate.png) 

5. <span data-ttu-id="ec6a8-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscore-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ec6a8-165">tooconfigure çoklu oturum açma üzerinde **JobScore** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[JobScore destek ekibi](mailto:support@jobscore.com).</span><span class="sxs-lookup"><span data-stu-id="ec6a8-165">tooconfigure single sign-on on **JobScore** side, you need toosend hello downloaded **Metadata XML** too[JobScore support team](mailto:support@jobscore.com).</span></span> 

> [!TIP]
> <span data-ttu-id="ec6a8-166">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="ec6a8-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ec6a8-167">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ec6a8-168">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ec6a8-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ec6a8-169">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec6a8-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="ec6a8-170">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="ec6a8-172">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ec6a8-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec6a8-173">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscore-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ec6a8-175">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscore-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ec6a8-177">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscore-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ec6a8-179">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ec6a8-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscore-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ec6a8-181">a.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-181">a.</span></span> <span data-ttu-id="ec6a8-182">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ec6a8-183">b.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-183">b.</span></span> <span data-ttu-id="ec6a8-184">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ec6a8-185">c.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-185">c.</span></span> <span data-ttu-id="ec6a8-186">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ec6a8-187">d.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-187">d.</span></span> <span data-ttu-id="ec6a8-188">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-188">Click **Create**.</span></span>
 
### <a name="creating-a-jobscore-test-user"></a><span data-ttu-id="ec6a8-189">JobScore test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec6a8-189">Creating a JobScore test user</span></span>

<span data-ttu-id="ec6a8-190">Bu bölümde, JobScore içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-190">In this section, you create a user called Britta Simon in JobScore.</span></span> <span data-ttu-id="ec6a8-191">Çalışmak [JobScore destek ekibi](mailto:support@jobscore.com) tooadd hello kullanıcılar hello JobScore Platform.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-191">Work with [JobScore support team](mailto:support@jobscore.com) tooadd hello users in hello JobScore platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ec6a8-192">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="ec6a8-192">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ec6a8-193">Bu bölümde, erişim tooJobScore vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-193">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJobScore.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="ec6a8-195">**tooassign Britta Simon tooJobScore hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ec6a8-195">**tooassign Britta Simon tooJobScore, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec6a8-196">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-196">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="ec6a8-198">Merhaba uygulamalar listesinde **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-198">In hello applications list, select **JobScore**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_app.png) 

3. <span data-ttu-id="ec6a8-200">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-200">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="ec6a8-202">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-202">Click **Add** button.</span></span> <span data-ttu-id="ec6a8-203">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="ec6a8-205">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-205">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ec6a8-206">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ec6a8-207">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ec6a8-208">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="ec6a8-208">Testing single sign-on</span></span>

<span data-ttu-id="ec6a8-209">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-209">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ec6a8-210">Merhaba JobScore hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour JobScore uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec6a8-210">When you click hello JobScore tile in hello Access Panel, you should get automatically signed-on tooyour JobScore application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ec6a8-211">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ec6a8-211">Additional resources</span></span>

* [<span data-ttu-id="ec6a8-212">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="ec6a8-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ec6a8-213">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="ec6a8-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_203.png

