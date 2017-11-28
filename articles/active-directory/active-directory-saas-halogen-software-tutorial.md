---
title: "Öğretici: Azure Active Directory Tümleştirme halojensiz yazılımıyla | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve halojensiz yazılımı arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: bdb67de713771d6e306f287c4b13895f6336f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="d9d53-103">Öğretici: Azure Active Directory Tümleştirme halojensiz yazılımıyla</span><span class="sxs-lookup"><span data-stu-id="d9d53-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="d9d53-104">Bu öğreticide, bilgi nasıl toointegrate halojensiz yazılım Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d9d53-104">In this tutorial, you learn how toointegrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d9d53-105">Halojensiz yazılım Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="d9d53-105">Integrating Halogen Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d9d53-106">Erişim tooHalogen yazılım sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d9d53-106">You can control in Azure AD who has access tooHalogen Software</span></span>
- <span data-ttu-id="d9d53-107">Kullanıcıların tooautomatically get açan tooHalogen yazılım (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d9d53-107">You can enable your users tooautomatically get signed-on tooHalogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d9d53-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="d9d53-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d9d53-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d9d53-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9d53-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d9d53-110">Prerequisites</span></span>

<span data-ttu-id="d9d53-111">tooconfigure halojensiz yazılım ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d9d53-111">tooconfigure Azure AD integration with Halogen Software, you need hello following items:</span></span>

- <span data-ttu-id="d9d53-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="d9d53-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d9d53-113">Bir halojensiz yazılım çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="d9d53-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d9d53-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="d9d53-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d9d53-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="d9d53-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d9d53-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="d9d53-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d9d53-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d9d53-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d9d53-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="d9d53-118">Scenario description</span></span>

<span data-ttu-id="d9d53-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="d9d53-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d9d53-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="d9d53-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d9d53-121">Merhaba Galerisi'nden halojensiz yazılım ekleme</span><span class="sxs-lookup"><span data-stu-id="d9d53-121">Adding Halogen Software from hello gallery</span></span>
2. <span data-ttu-id="d9d53-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d9d53-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-hello-gallery"></a><span data-ttu-id="d9d53-123">Merhaba Galerisi'nden halojensiz yazılım ekleme</span><span class="sxs-lookup"><span data-stu-id="d9d53-123">Adding Halogen Software from hello gallery</span></span>

<span data-ttu-id="d9d53-124">Azure AD'ye tooconfigure hello tümleştirme halojensiz yazılımın tooadd halojensiz yazılım hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9d53-124">tooconfigure hello integration of Halogen Software into Azure AD, you need tooadd Halogen Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d9d53-125">**tooadd halojensiz yazılım hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d9d53-125">**tooadd Halogen Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9d53-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d9d53-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d9d53-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d9d53-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="d9d53-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d9d53-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="d9d53-133">Merhaba arama kutusuna yazın **halojensiz yazılım**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-133">In hello search box, type **Halogen Software**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="d9d53-135">Merhaba Sonuçlar panelinde seçin **halojensiz yazılım**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="d9d53-135">In hello results panel, select **Halogen Software**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d9d53-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d9d53-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d9d53-138">Bu bölümde, yapılandırmak ve halojensiz yazılım "Britta Simon" adlı bir test kullanıcı tabanlı Azure AD çoklu oturum açmayı sınayın.</span><span class="sxs-lookup"><span data-stu-id="d9d53-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d9d53-139">Tek toowork'ın oturum açma hangi hello karşılık gelen halojensiz yazılım tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9d53-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halogen Software is tooa user in Azure AD.</span></span> <span data-ttu-id="d9d53-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı halojensiz yazılım arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9d53-140">In other words, a link relationship between an Azure AD user and hello related user in Halogen Software needs toobe established.</span></span>

<span data-ttu-id="d9d53-141">Merhaba hello değeri halojensiz yazılımda atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="d9d53-141">In Halogen Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d9d53-142">tooconfigure ve halojensiz yazılım ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d9d53-142">tooconfigure and test Azure AD single sign-on with Halogen Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d9d53-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="d9d53-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d9d53-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="d9d53-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d9d53-145">**[Halojensiz yazılım test kullanıcısı oluşturma](#creating-a-halogen-software-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir halojensiz yazılım, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="d9d53-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in Halogen Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d9d53-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="d9d53-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d9d53-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="d9d53-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d9d53-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d9d53-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d9d53-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma halojensiz yazılım uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d9d53-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="d9d53-150">**tooconfigure Azure AD çoklu oturum açma halojensiz yazılımıyla hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d9d53-150">**tooconfigure Azure AD single sign-on with Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9d53-151">Merhaba hello üzerinde Azure portal'ın **halojensiz yazılım** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-151">In hello Azure portal, on hello **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="d9d53-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="d9d53-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="d9d53-155">Merhaba üzerinde **halojensiz yazılım etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d9d53-155">On hello **Halogen Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="d9d53-157">a.</span><span class="sxs-lookup"><span data-stu-id="d9d53-157">a.</span></span> <span data-ttu-id="d9d53-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="d9d53-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="d9d53-159">b.</span><span class="sxs-lookup"><span data-stu-id="d9d53-159">b.</span></span> <span data-ttu-id="d9d53-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın: `https://global.halogensoftware.com/<companyname>`,`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="d9d53-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d9d53-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="d9d53-161">These values are not real.</span></span> <span data-ttu-id="d9d53-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="d9d53-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d9d53-163">Kişi [halojensiz yazılım istemci destek ekibi](https://support.halogensoftware.com/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="d9d53-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="d9d53-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d9d53-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="d9d53-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d9d53-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d9d53-168">Farklı bir tarayıcı penceresinde, oturum açma tooyour **halojensiz yazılım** yönetici olarak uygulama.</span><span class="sxs-lookup"><span data-stu-id="d9d53-168">In a different browser window, sign-on tooyour **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="d9d53-169">Merhaba tıklatın **seçenekleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d9d53-169">Click hello **Options** tab.</span></span> 
   
    ![Azure AD Connect nedir?][12]

8. <span data-ttu-id="d9d53-171">Merhaba sol gezinti bölmesinde **SAML Yapılandırması**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-171">In hello left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![Azure AD Connect nedir?][13]

9. <span data-ttu-id="d9d53-173">Merhaba üzerinde **SAML Yapılandırması** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d9d53-173">On hello **SAML Configuration** page, perform hello following steps:</span></span> 

    ![Azure AD Connect nedir?][14]

     <span data-ttu-id="d9d53-175">a.</span><span class="sxs-lookup"><span data-stu-id="d9d53-175">a.</span></span> <span data-ttu-id="d9d53-176">Olarak **benzersiz tanımlayıcı**seçin **NameID**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="d9d53-177">b.</span><span class="sxs-lookup"><span data-stu-id="d9d53-177">b.</span></span> <span data-ttu-id="d9d53-178">Olarak **benzersiz tanıtıcı eşlemeleri için**seçin **kullanıcıadı**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="d9d53-179">c.</span><span class="sxs-lookup"><span data-stu-id="d9d53-179">c.</span></span> <span data-ttu-id="d9d53-180">tooupload, indirilen meta veri dosyası tıklatın **Gözat** tooselect hello dosya ve ardından **dosyasını karşıya yükle**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-180">tooupload your downloaded metadata file, click **Browse** tooselect hello file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="d9d53-181">d.</span><span class="sxs-lookup"><span data-stu-id="d9d53-181">d.</span></span> <span data-ttu-id="d9d53-182">tootest hello yapılandırma tıklatın **testi**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-182">tootest hello configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="d9d53-183">Merhaba ileti için toowait gerekir "*hello SAML test tamamlanmıştır. Lütfen bu pencereyi kapatmak*".</span><span class="sxs-lookup"><span data-stu-id="d9d53-183">You need toowait for hello message "*hello SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="d9d53-184">Ardından, hello açılan tarayıcı penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="d9d53-184">Then, close hello opened browser window.</span></span> <span data-ttu-id="d9d53-185">Merhaba **etkinleştirmek SAML** onay kutusunu hello test olmuşsa yalnızca etkin.</span><span class="sxs-lookup"><span data-stu-id="d9d53-185">hello **Enable SAML** checkbox is only enabled if hello test has been completed.</span></span> 
     
     <span data-ttu-id="d9d53-186">e.</span><span class="sxs-lookup"><span data-stu-id="d9d53-186">e.</span></span> <span data-ttu-id="d9d53-187">Seçin **etkinleştirmek SAML**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="d9d53-188">f.</span><span class="sxs-lookup"><span data-stu-id="d9d53-188">f.</span></span> <span data-ttu-id="d9d53-189">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="d9d53-190">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="d9d53-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d9d53-191">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="d9d53-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d9d53-192">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d9d53-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d9d53-193">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d9d53-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="d9d53-194">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="d9d53-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="d9d53-196">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d9d53-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9d53-197">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d9d53-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d9d53-199">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d9d53-201">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="d9d53-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d9d53-203">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d9d53-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d9d53-205">a.</span><span class="sxs-lookup"><span data-stu-id="d9d53-205">a.</span></span> <span data-ttu-id="d9d53-206">Merhaba, **adı** metin kutusuna, tür adı olarak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-206">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="d9d53-207">b.</span><span class="sxs-lookup"><span data-stu-id="d9d53-207">b.</span></span> <span data-ttu-id="d9d53-208">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="d9d53-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d9d53-209">c.</span><span class="sxs-lookup"><span data-stu-id="d9d53-209">c.</span></span> <span data-ttu-id="d9d53-210">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d9d53-211">d.</span><span class="sxs-lookup"><span data-stu-id="d9d53-211">d.</span></span> <span data-ttu-id="d9d53-212">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9d53-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="d9d53-213">Halojensiz yazılım test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d9d53-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="d9d53-214">Bu bölümde Hello amacı toocreate Britta Simon halojensiz yazılım adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="d9d53-214">hello objective of this section is toocreate a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="d9d53-215">**toocreate Britta Simon halojensiz yazılımda adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d9d53-215">**toocreate a user called Britta Simon in Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9d53-216">Tooyour üzerinde oturum **halojensiz yazılım** yönetici olarak uygulama.</span><span class="sxs-lookup"><span data-stu-id="d9d53-216">Sign on tooyour **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="d9d53-217">Merhaba tıklatın **kullanıcı Merkezi** sekmesini ve ardından **kullanıcı oluştur**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-217">Click hello **User Center** tab, and then click **Create User**.</span></span>
   
    ![Azure AD Connect nedir?][300]  

3. <span data-ttu-id="d9d53-219">Merhaba üzerinde **yeni kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d9d53-219">On hello **New User** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD Connect nedir?][301]

    <span data-ttu-id="d9d53-221">a.</span><span class="sxs-lookup"><span data-stu-id="d9d53-221">a.</span></span> <span data-ttu-id="d9d53-222">Merhaba, **ad** metin kutusuna, tür ilk gibi hello kullanıcı adını **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-222">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>
    
    <span data-ttu-id="d9d53-223">b.</span><span class="sxs-lookup"><span data-stu-id="d9d53-223">b.</span></span> <span data-ttu-id="d9d53-224">Merhaba, **Soyadı** metin kutusuna, türü hello kullanıcının soyadını gibi **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-224">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span> 

    <span data-ttu-id="d9d53-225">c.</span><span class="sxs-lookup"><span data-stu-id="d9d53-225">c.</span></span> <span data-ttu-id="d9d53-226">Merhaba, **kullanıcıadı** metin kutusuna, türü **Britta Simon**, hello Azure portal olduğu gibi hello kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="d9d53-226">In hello **Username** textbox, type **Britta Simon**, hello user name as in hello Azure portal.</span></span>

    <span data-ttu-id="d9d53-227">d.</span><span class="sxs-lookup"><span data-stu-id="d9d53-227">d.</span></span> <span data-ttu-id="d9d53-228">Merhaba, **parola** metin kutusuna, Britta parolasını yazın.</span><span class="sxs-lookup"><span data-stu-id="d9d53-228">In hello **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="d9d53-229">e.</span><span class="sxs-lookup"><span data-stu-id="d9d53-229">e.</span></span> <span data-ttu-id="d9d53-230">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9d53-230">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d9d53-231">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="d9d53-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d9d53-232">Bu bölümde, erişim tooHalogen yazılım vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d9d53-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHalogen Software.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="d9d53-234">**tooassign Britta Simon tooHalogen yazılım, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d9d53-234">**tooassign Britta Simon tooHalogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9d53-235">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="d9d53-237">Merhaba uygulamalar listesinde **halojensiz yazılım**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-237">In hello applications list, select **Halogen Software**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="d9d53-239">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d9d53-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="d9d53-241">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d9d53-241">Click **Add** button.</span></span> <span data-ttu-id="d9d53-242">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d9d53-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="d9d53-244">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="d9d53-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d9d53-245">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d9d53-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d9d53-246">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d9d53-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d9d53-247">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="d9d53-247">Testing single sign-on</span></span>

<span data-ttu-id="d9d53-248">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="d9d53-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="d9d53-249">Hello halojensiz yazılım hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour halojensiz yazılım uygulaması almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9d53-249">When you click hello Halogen Software tile in hello Access Panel, you should get automatically signed-on tooyour Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d9d53-250">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d9d53-250">Additional resources</span></span>

* [<span data-ttu-id="d9d53-251">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="d9d53-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d9d53-252">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="d9d53-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
