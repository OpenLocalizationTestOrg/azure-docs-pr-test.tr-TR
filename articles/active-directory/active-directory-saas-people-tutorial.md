---
title: "Öğretici: Azure Active Directory Tümleştirme kişilerle | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve kişiler arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c9b6202-11dd-4bb6-a679-8fb0a7a0ef4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: d540c31867c92c4dc09db9c0833f8a8a7c02b371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-people"></a><span data-ttu-id="17514-103">Öğretici: Azure Active Directory Tümleştirme kişilerle</span><span class="sxs-lookup"><span data-stu-id="17514-103">Tutorial: Azure Active Directory integration with People</span></span>

<span data-ttu-id="17514-104">Bu öğreticide, bilgi nasıl toointegrate kişiler Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="17514-104">In this tutorial, you learn how toointegrate People with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17514-105">Kişilerin Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="17514-105">Integrating People with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="17514-106">Erişim tooPeople sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="17514-106">You can control in Azure AD who has access tooPeople</span></span>
- <span data-ttu-id="17514-107">Kullanıcıların tooautomatically get açan tooPeople (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="17514-107">You can enable your users tooautomatically get signed-on tooPeople (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="17514-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="17514-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="17514-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="17514-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17514-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="17514-110">Prerequisites</span></span>

<span data-ttu-id="17514-111">Azure AD tümleştirme kişilerle tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="17514-111">tooconfigure Azure AD integration with People, you need hello following items:</span></span>

- <span data-ttu-id="17514-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="17514-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17514-113">Bir kişi çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="17514-113">A People single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17514-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="17514-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17514-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="17514-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17514-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="17514-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="17514-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17514-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17514-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="17514-118">Scenario description</span></span>
<span data-ttu-id="17514-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="17514-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17514-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="17514-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17514-121">Merhaba galerisinden kişileri ekleme</span><span class="sxs-lookup"><span data-stu-id="17514-121">Adding People from hello gallery</span></span>
2. <span data-ttu-id="17514-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="17514-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-people-from-hello-gallery"></a><span data-ttu-id="17514-123">Merhaba galerisinden kişileri ekleme</span><span class="sxs-lookup"><span data-stu-id="17514-123">Adding People from hello gallery</span></span>
<span data-ttu-id="17514-124">Azure AD'ye tooconfigure hello tümleştirme kişilerin tooadd kişiler hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="17514-124">tooconfigure hello integration of People into Azure AD, you need tooadd People from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="17514-125">**tooadd hello galerisinden kişileri hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="17514-125">**tooadd People from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="17514-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="17514-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="17514-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="17514-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="17514-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="17514-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="17514-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="17514-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="17514-133">Merhaba arama kutusuna yazın **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="17514-133">In hello search box, type **People**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-people-tutorial/tutorial_people_search.png)

5. <span data-ttu-id="17514-135">Merhaba Sonuçlar panelinde seçin **kişiler**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="17514-135">In hello results panel, select **People**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-people-tutorial/tutorial_people_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="17514-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="17514-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="17514-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı kişilerle test etme.</span><span class="sxs-lookup"><span data-stu-id="17514-138">In this section, you configure and test Azure AD single sign-on with People based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="17514-139">Tek toowork'ın oturum açma hangi hello karşılık gelen kişilerin de tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="17514-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in People is tooa user in Azure AD.</span></span> <span data-ttu-id="17514-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı kişiler arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="17514-140">In other words, a link relationship between an Azure AD user and hello related user in People needs toobe established.</span></span>

<span data-ttu-id="17514-141">Merhaba hello değeri, kişilere atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="17514-141">In People, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="17514-142">tooconfigure ve kişilerle Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="17514-142">tooconfigure and test Azure AD single sign-on with People, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="17514-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="17514-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="17514-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="17514-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="17514-145">**[Kişiler test kullanıcısı oluşturma](#creating-a-people-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir kişi olarak, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="17514-145">**[Creating a People test user](#creating-a-people-test-user)** - toohave a counterpart of Britta Simon in People that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="17514-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="17514-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="17514-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="17514-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="17514-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="17514-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="17514-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma kişiler uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="17514-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your People application.</span></span>

<span data-ttu-id="17514-150">**tooconfigure Azure AD çoklu oturum açma, kişilerle hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="17514-150">**tooconfigure Azure AD single sign-on with People, perform hello following steps:**</span></span>

1. <span data-ttu-id="17514-151">Merhaba hello üzerinde Azure portal'ın **kişiler** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="17514-151">In hello Azure portal, on hello **People** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="17514-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="17514-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-people-tutorial/tutorial_people_samlbase.png)

3. <span data-ttu-id="17514-155">Merhaba üzerinde **kişiler etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="17514-155">On hello **People Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-people-tutorial/tutorial_people_url.png)

    <span data-ttu-id="17514-157">a.</span><span class="sxs-lookup"><span data-stu-id="17514-157">a.</span></span> <span data-ttu-id="17514-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.peoplehr.com/`</span><span class="sxs-lookup"><span data-stu-id="17514-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.peoplehr.com/`</span></span>

    <span data-ttu-id="17514-159">b.</span><span class="sxs-lookup"><span data-stu-id="17514-159">b.</span></span> <span data-ttu-id="17514-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://www.peoplehr.com`</span><span class="sxs-lookup"><span data-stu-id="17514-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.peoplehr.com`</span></span>

    <span data-ttu-id="17514-161">c.</span><span class="sxs-lookup"><span data-stu-id="17514-161">c.</span></span> <span data-ttu-id="17514-162">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span><span class="sxs-lookup"><span data-stu-id="17514-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="17514-163">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="17514-163">These values are not real.</span></span> <span data-ttu-id="17514-164">Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="17514-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="17514-165">Kişi [kişiler istemci destek ekibi](mailto:customerservices@peoplehr.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="17514-165">Contact [People Client support team](mailto:customerservices@peoplehr.com) tooget these values.</span></span>

5. <span data-ttu-id="17514-166">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="17514-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-people-tutorial/tutorial_people_certificate.png) 

6. <span data-ttu-id="17514-168">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="17514-168">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-people-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="17514-170">Uygulamanız için yapılandırılmış SSO tooget, toosign üzerinde tooyour kişiler Kiracı yönetici olarak gerekir.</span><span class="sxs-lookup"><span data-stu-id="17514-170">tooget SSO configured for your application, you need toosign-on tooyour People tenant as an administrator.</span></span>
   
8. <span data-ttu-id="17514-171">Hello'nde hello sol tarafında, menüsünü **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="17514-171">In hello menu on hello left side, click **Settings**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-people-tutorial/tutorial_people_001.png)

9. <span data-ttu-id="17514-173">Tıklatın **şirket**.</span><span class="sxs-lookup"><span data-stu-id="17514-173">Click **Company**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-people-tutorial/tutorial_people_002.png)

10. <span data-ttu-id="17514-175">Merhaba üzerinde **karşıya yükleme 'Single Sign tam On' SAML meta veri dosyası**, tıklatın **Gözat** tooupload hello indirilen meta veri dosyası.</span><span class="sxs-lookup"><span data-stu-id="17514-175">On hello **Upload 'Single Sign On' SAML meta-data file**, click **Browse** tooupload hello downloaded metadata file.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-people-tutorial/tutorial_people_003.png)

> [!TIP]
> <span data-ttu-id="17514-177">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="17514-177">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="17514-178">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="17514-178">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="17514-179">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="17514-179">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="17514-180">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="17514-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="17514-181">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="17514-181">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="17514-183">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="17514-183">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="17514-184">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="17514-184">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-people-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="17514-186">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="17514-186">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-people-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="17514-188">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="17514-188">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-people-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="17514-190">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="17514-190">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-people-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="17514-192">a.</span><span class="sxs-lookup"><span data-stu-id="17514-192">a.</span></span> <span data-ttu-id="17514-193">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="17514-193">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17514-194">b.</span><span class="sxs-lookup"><span data-stu-id="17514-194">b.</span></span> <span data-ttu-id="17514-195">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="17514-195">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="17514-196">c.</span><span class="sxs-lookup"><span data-stu-id="17514-196">c.</span></span> <span data-ttu-id="17514-197">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="17514-197">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="17514-198">d.</span><span class="sxs-lookup"><span data-stu-id="17514-198">d.</span></span> <span data-ttu-id="17514-199">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="17514-199">Click **Create**.</span></span>
 
### <a name="creating-a-people-test-user"></a><span data-ttu-id="17514-200">Kişiler test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="17514-200">Creating a People test user</span></span>

<span data-ttu-id="17514-201">Bu bölümde, kişilerin Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="17514-201">In this section, you create a user called Britta Simon in People.</span></span> <span data-ttu-id="17514-202">Çalışmak [kişiler istemci destek ekibi](mailto:customerservices@peoplehr.com) hello kişiler platformunda hello kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="17514-202">Work with [People Client support team](mailto:customerservices@peoplehr.com) to add hello users in hello People platform.</span></span> <span data-ttu-id="17514-203">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="17514-203">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="17514-204">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="17514-204">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="17514-205">Bu bölümde, erişim tooPeople vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="17514-205">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPeople.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="17514-207">**tooassign Britta Simon tooPeople hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="17514-207">**tooassign Britta Simon tooPeople, perform hello following steps:**</span></span>

1. <span data-ttu-id="17514-208">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="17514-208">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="17514-210">Merhaba uygulamalar listesinde **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="17514-210">In hello applications list, select **People**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-people-tutorial/tutorial_people_app.png) 

3. <span data-ttu-id="17514-212">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="17514-212">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="17514-214">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="17514-214">Click **Add** button.</span></span> <span data-ttu-id="17514-215">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="17514-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="17514-217">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="17514-217">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="17514-218">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="17514-218">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17514-219">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="17514-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="17514-220">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="17514-220">Testing single sign-on</span></span>

<span data-ttu-id="17514-221">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="17514-221">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="17514-222">Kişiler hello erişim paneli döşeme hello tıkladığınızda, otomatik olarak açan kişi uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="17514-222">When you click hello People tile in hello Access Panel, you should get automatically signed-on tooyour People application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="17514-223">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="17514-223">Additional resources</span></span>

* [<span data-ttu-id="17514-224">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="17514-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="17514-225">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="17514-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-people-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-people-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-people-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-people-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-people-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-people-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-people-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-people-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-people-tutorial/tutorial_general_203.png

