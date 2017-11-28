---
title: "Öğretici: Azure Active Directory Tümleştirme ile Skillport | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Skillport arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: ba504c3cae5f92767eb90d8453887904690fe0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a><span data-ttu-id="92c4b-103">Öğretici: Azure Active Directory Tümleştirme Skillport ile</span><span class="sxs-lookup"><span data-stu-id="92c4b-103">Tutorial: Azure Active Directory integration with Skillport</span></span>

<span data-ttu-id="92c4b-104">Bu öğreticide, bilgi nasıl toointegrate Skillport Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="92c4b-104">In this tutorial, you learn how toointegrate Skillport with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92c4b-105">Skillport Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="92c4b-105">Integrating Skillport with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="92c4b-106">Erişim tooSkillport sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="92c4b-106">You can control in Azure AD who has access tooSkillport</span></span>
- <span data-ttu-id="92c4b-107">Kullanıcıların tooautomatically get açan tooSkillport (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="92c4b-107">You can enable your users tooautomatically get signed-on tooSkillport (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="92c4b-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="92c4b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="92c4b-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="92c4b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92c4b-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="92c4b-110">Prerequisites</span></span>

<span data-ttu-id="92c4b-111">tooconfigure Skillport ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="92c4b-111">tooconfigure Azure AD integration with Skillport, you need hello following items:</span></span>

- <span data-ttu-id="92c4b-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="92c4b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92c4b-113">Bir Skillport çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="92c4b-113">A Skillport single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="92c4b-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="92c4b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="92c4b-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="92c4b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92c4b-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="92c4b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="92c4b-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92c4b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92c4b-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="92c4b-118">Scenario description</span></span>
<span data-ttu-id="92c4b-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="92c4b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92c4b-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="92c4b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92c4b-121">Merhaba Galerisi'nden Skillport ekleme</span><span class="sxs-lookup"><span data-stu-id="92c4b-121">Adding Skillport from hello gallery</span></span>
2. <span data-ttu-id="92c4b-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="92c4b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skillport-from-hello-gallery"></a><span data-ttu-id="92c4b-123">Merhaba Galerisi'nden Skillport ekleme</span><span class="sxs-lookup"><span data-stu-id="92c4b-123">Adding Skillport from hello gallery</span></span>
<span data-ttu-id="92c4b-124">Azure AD'ye tooconfigure hello tümleştirme Skillport, tooadd Skillport hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="92c4b-124">tooconfigure hello integration of Skillport into Azure AD, you need tooadd Skillport from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="92c4b-125">**tooadd Skillport hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="92c4b-125">**tooadd Skillport from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="92c4b-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="92c4b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="92c4b-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="92c4b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="92c4b-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="92c4b-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="92c4b-131">Tıklatın **yeni uygulama** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="92c4b-131">Click **New Application** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="92c4b-133">Merhaba arama kutusuna yazın **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="92c4b-133">In hello search box, type **Skillport**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_search.png)

5. <span data-ttu-id="92c4b-135">Merhaba Sonuçlar panelinde seçin **Skillport**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="92c4b-135">In hello results panel, select **Skillport**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="92c4b-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="92c4b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="92c4b-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Skillport sınayın.</span><span class="sxs-lookup"><span data-stu-id="92c4b-138">In this section, you configure and test Azure AD single sign-on with Skillport based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="92c4b-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Skillport içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="92c4b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Skillport is tooa user in Azure AD.</span></span> <span data-ttu-id="92c4b-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Skillport hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="92c4b-140">In other words, a link relationship between an Azure AD user and hello related user in Skillport needs toobe established.</span></span>

<span data-ttu-id="92c4b-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Skillport içinde.</span><span class="sxs-lookup"><span data-stu-id="92c4b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Skillport.</span></span>

<span data-ttu-id="92c4b-142">tooconfigure ve Skillport ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="92c4b-142">tooconfigure and test Azure AD single sign-on with Skillport, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="92c4b-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="92c4b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="92c4b-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="92c4b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="92c4b-145">**[Skillport test kullanıcısı oluşturma](#creating-a-skillport-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Skillport içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="92c4b-145">**[Creating a Skillport test user](#creating-a-skillport-test-user)** - toohave a counterpart of Britta Simon in Skillport that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="92c4b-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="92c4b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="92c4b-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="92c4b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="92c4b-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="92c4b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="92c4b-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Skillport uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="92c4b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Skillport application.</span></span>

<span data-ttu-id="92c4b-150">**tooconfigure Azure AD çoklu oturum açma ile Skillport, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="92c4b-150">**tooconfigure Azure AD single sign-on with Skillport, perform hello following steps:**</span></span>

1. <span data-ttu-id="92c4b-151">Hello hello üzerinde Azure portal'ın **Skillport** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="92c4b-151">In hello Azure  portal, on hello **Skillport** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="92c4b-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="92c4b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_samlbase.png)

3. <span data-ttu-id="92c4b-155">Merhaba üzerinde **Skillport etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="92c4b-155">On hello **Skillport Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_url.png)

    <span data-ttu-id="92c4b-157">a.</span><span class="sxs-lookup"><span data-stu-id="92c4b-157">a.</span></span> <span data-ttu-id="92c4b-158">Merhaba, **oturum açma URL'si** metin kutusuna, türü aşağıdaki hello kullanarak bir URL düzenleri:</span><span class="sxs-lookup"><span data-stu-id="92c4b-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span>
      
      <span data-ttu-id="92c4b-159">AB veri merkezi:`https://<subdomain>.skillport.eu`</span><span class="sxs-lookup"><span data-stu-id="92c4b-159">EU Datacenter: `https://<subdomain>.skillport.eu`</span></span>
   
      <span data-ttu-id="92c4b-160">ABD veri merkezi:`https://<subdomain>.skillport.com`</span><span class="sxs-lookup"><span data-stu-id="92c4b-160">US Datacenter: `https://<subdomain>.skillport.com`</span></span>
   
    <span data-ttu-id="92c4b-161">b.</span><span class="sxs-lookup"><span data-stu-id="92c4b-161">b.</span></span> <span data-ttu-id="92c4b-162">Merhaba, **yanıt URL'si** metin kutusuna, türü aşağıdaki hello kullanarak bir URL düzenleri:</span><span class="sxs-lookup"><span data-stu-id="92c4b-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span>
    
      <span data-ttu-id="92c4b-163">AB veri merkezi:`https://<subdomain>.skillport.eu/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="92c4b-163">EU Datacenter: `https://<subdomain>.skillport.eu/adfs/ls/`</span></span>
    
      <span data-ttu-id="92c4b-164">ABD veri merkezi:`https://<subdomain>.skillport.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="92c4b-164">US Datacenter: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="92c4b-165">Bu değerler hello gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="92c4b-165">These values are not hello real.</span></span> <span data-ttu-id="92c4b-166">Bu değerleri hello gerçek yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="92c4b-166">Update these values with hello actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="92c4b-167">Kişi [Skillport istemci destek ekibi](https://www.skillsoft.com/contact.asp) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="92c4b-167">Contact [Skillport Client support team](https://www.skillsoft.com/contact.asp) tooget these values.</span></span>
 
4. <span data-ttu-id="92c4b-168">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="92c4b-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_certificate.png) 

5. <span data-ttu-id="92c4b-170">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="92c4b-170">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skillport-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="92c4b-172">tooconfigure çoklu oturum açma üzerinde **Skillport** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[Skillport destek ekibi](https://www.skillsoft.com/contact.asp).</span><span class="sxs-lookup"><span data-stu-id="92c4b-172">tooconfigure single sign-on on **Skillport** side, you need toosend hello downloaded **Metadata XML** too[Skillport support team](https://www.skillsoft.com/contact.asp).</span></span> <span data-ttu-id="92c4b-173">Bunlar, toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="92c4b-173">They will set it up toohave hello SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="92c4b-174">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="92c4b-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="92c4b-175">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="92c4b-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="92c4b-177">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="92c4b-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="92c4b-178">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="92c4b-178">In hello **Azure  portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skillport-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="92c4b-180">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="92c4b-180">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skillport-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="92c4b-182">Merhaba iletişim Hello üstünde tıklatın **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="92c4b-182">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skillport-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="92c4b-184">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="92c4b-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skillport-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="92c4b-186">a.</span><span class="sxs-lookup"><span data-stu-id="92c4b-186">a.</span></span> <span data-ttu-id="92c4b-187">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="92c4b-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92c4b-188">b.</span><span class="sxs-lookup"><span data-stu-id="92c4b-188">b.</span></span> <span data-ttu-id="92c4b-189">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="92c4b-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="92c4b-190">c.</span><span class="sxs-lookup"><span data-stu-id="92c4b-190">c.</span></span> <span data-ttu-id="92c4b-191">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="92c4b-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="92c4b-192">d.</span><span class="sxs-lookup"><span data-stu-id="92c4b-192">d.</span></span> <span data-ttu-id="92c4b-193">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="92c4b-193">Click **Create**.</span></span>
 
### <a name="creating-a-skillport-test-user"></a><span data-ttu-id="92c4b-194">Skillport test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="92c4b-194">Creating a Skillport test user</span></span>

<span data-ttu-id="92c4b-195">Sipariş toocreate Skillport test kullanıcı toocontact gerek [Skillport destek ekibi](https://www.skillsoft.com/contact.asp) son kullanıcı toohello gereksinimi göre birden çok iş senaryolarını sahip oldukları gibi.</span><span class="sxs-lookup"><span data-stu-id="92c4b-195">In order toocreate Skillport test user, you need toocontact [Skillport support team](https://www.skillsoft.com/contact.asp) as they have multiple business scenarios according toohello requirement of end user.</span></span> <span data-ttu-id="92c4b-196">Bunlar, tartışma hello kullanıcılarla sonra yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="92c4b-196">They will configure it after discussion with hello users.</span></span>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="92c4b-197">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="92c4b-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="92c4b-198">Bu bölümde, erişim tooSkillport vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="92c4b-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSkillport.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="92c4b-200">**tooassign Britta Simon tooSkillport hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="92c4b-200">**tooassign Britta Simon tooSkillport, perform hello following steps:**</span></span>

1. <span data-ttu-id="92c4b-201">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="92c4b-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="92c4b-203">Merhaba uygulamalar listesinde **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="92c4b-203">In hello applications list, select **Skillport**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_app.png) 

3. <span data-ttu-id="92c4b-205">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="92c4b-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="92c4b-207">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="92c4b-207">Click **Add** button.</span></span> <span data-ttu-id="92c4b-208">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="92c4b-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="92c4b-210">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="92c4b-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="92c4b-211">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="92c4b-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="92c4b-212">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="92c4b-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="92c4b-213">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="92c4b-213">Testing single sign-on</span></span>

<span data-ttu-id="92c4b-214">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="92c4b-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="92c4b-215">Merhaba Skillport hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Skillport uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="92c4b-215">When you click hello Skillport tile in hello Access Panel, you should get automatically signed-on tooyour Skillport application.</span></span>
<span data-ttu-id="92c4b-216">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="92c4b-216">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="92c4b-217">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="92c4b-217">Additional resources</span></span>

* [<span data-ttu-id="92c4b-218">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="92c4b-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92c4b-219">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="92c4b-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_203.png

