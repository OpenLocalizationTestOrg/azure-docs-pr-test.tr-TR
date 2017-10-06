---
title: "Öğretici: Azure Active Directory Tümleştirme Tableau Online ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Tableau çevrimiçi arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 590b2674270c340b4750c7b6feeaf4f0df4bf853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="104e3-103">Öğretici: Azure Active Directory Tümleştirme Tableau Online ile</span><span class="sxs-lookup"><span data-stu-id="104e3-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="104e3-104">Bu öğreticide, bilgi nasıl toointegrate Tableau çevrimiçi Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="104e3-104">In this tutorial, you learn how toointegrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="104e3-105">Tableau çevrimiçi Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="104e3-105">Integrating Tableau Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="104e3-106">Erişim tooTableau çevrimiçi olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="104e3-106">You can control in Azure AD who has access tooTableau Online</span></span>
- <span data-ttu-id="104e3-107">Kullanıcıların tooautomatically get açan tooTableau çevrimiçi (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="104e3-107">You can enable your users tooautomatically get signed-on tooTableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="104e3-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="104e3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="104e3-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="104e3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="104e3-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="104e3-110">Prerequisites</span></span>

<span data-ttu-id="104e3-111">tooconfigure Tableau Online ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="104e3-111">tooconfigure Azure AD integration with Tableau Online, you need hello following items:</span></span>

- <span data-ttu-id="104e3-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="104e3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="104e3-113">Bir Tableau çevrimiçi çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="104e3-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="104e3-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="104e3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="104e3-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="104e3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="104e3-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="104e3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="104e3-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="104e3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="104e3-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="104e3-118">Scenario description</span></span>
<span data-ttu-id="104e3-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="104e3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="104e3-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="104e3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="104e3-121">Tableau çevrimiçi hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="104e3-121">Adding Tableau Online from hello gallery</span></span>
2. <span data-ttu-id="104e3-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="104e3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-hello-gallery"></a><span data-ttu-id="104e3-123">Tableau çevrimiçi hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="104e3-123">Adding Tableau Online from hello gallery</span></span>
<span data-ttu-id="104e3-124">Azure AD'ye tooconfigure hello tümleştirme Tableau Online hello galeri tooyour yönetilen SaaS uygulamaları listesinden Tableau çevrimiçi tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="104e3-124">tooconfigure hello integration of Tableau Online into Azure AD, you need tooadd Tableau Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="104e3-125">**tooadd Tableau çevrimiçi hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="104e3-125">**tooadd Tableau Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="104e3-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="104e3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="104e3-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="104e3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="104e3-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="104e3-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="104e3-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="104e3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="104e3-133">Merhaba arama kutusuna yazın **Tableau çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="104e3-133">In hello search box, type **Tableau Online**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. <span data-ttu-id="104e3-135">Merhaba Sonuçlar panelinde seçin **Tableau çevrimiçi**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="104e3-135">In hello results panel, select **Tableau Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="104e3-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="104e3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="104e3-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Tableau "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Online ile test etme</span><span class="sxs-lookup"><span data-stu-id="104e3-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="104e3-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Tableau çevrimiçi tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="104e3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Online is tooa user in Azure AD.</span></span> <span data-ttu-id="104e3-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve Tableau çevrimiçi hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="104e3-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Online needs toobe established.</span></span>

<span data-ttu-id="104e3-141">Çevrimiçi Tableau'nde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="104e3-141">In Tableau Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="104e3-142">tooconfigure ve Tableau Online ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="104e3-142">tooconfigure and test Azure AD single sign-on with Tableau Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="104e3-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="104e3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="104e3-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="104e3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="104e3-145">**[Tableau çevrimiçi bir test kullanıcısı oluşturma](#creating-a-tableau-online-test-user)**  -toohave Britta Simon Tableau, kullanıcı bağlantılı toohello Azure AD gösterimidir Online'da, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="104e3-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - toohave a counterpart of Britta Simon in Tableau Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="104e3-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="104e3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="104e3-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="104e3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="104e3-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="104e3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="104e3-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Tableau çevrimiçi uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="104e3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="104e3-150">**tooconfigure Azure AD çoklu oturum açma Tableau Online ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="104e3-150">**tooconfigure Azure AD single sign-on with Tableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="104e3-151">Hello hello üzerinde Azure portal'ın **Tableau çevrimiçi** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="104e3-151">In hello Azure portal, on hello **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="104e3-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="104e3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. <span data-ttu-id="104e3-155">Merhaba üzerinde **Tableau çevrimiçi etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="104e3-155">On hello **Tableau Online Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="104e3-157">a.</span><span class="sxs-lookup"><span data-stu-id="104e3-157">a.</span></span> <span data-ttu-id="104e3-158">Merhaba, **oturum açma URL'si** metin kutusuna, türü hello URL'si:`https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="104e3-158">In hello **Sign-on URL** textbox, type hello URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="104e3-159">b.</span><span class="sxs-lookup"><span data-stu-id="104e3-159">b.</span></span> <span data-ttu-id="104e3-160">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://sso.online.tableau.com/public/sp/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="104e3-160">In hello **Identifier** textbox, type hello URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span></span>

4. <span data-ttu-id="104e3-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="104e3-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. <span data-ttu-id="104e3-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="104e3-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="104e3-165">Farklı bir tarayıcı penceresinde oturum açma Tableau çevrimiçi uygulama tooyour.</span><span class="sxs-lookup"><span data-stu-id="104e3-165">In a different browser window, sign-on tooyour Tableau Online application.</span></span> <span data-ttu-id="104e3-166">Çok Git**ayarları** ve ardından **kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="104e3-166">Go too**Settings** and then **Authentication**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. <span data-ttu-id="104e3-168">tooenable SAML altında **kimlik doğrulama türleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="104e3-168">tooenable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="104e3-169">Merhaba denetleyin **çoklu oturum açma SAML ile** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="104e3-169">Check hello **Single sign-on with SAML** checkbox.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. <span data-ttu-id="104e3-171">Kadar aşağıya kaydırın **alma meta veri dosyasına Tableau çevrimiçi** bölümü.</span><span class="sxs-lookup"><span data-stu-id="104e3-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="104e3-172">Gözat'ı tıklatın ve Azure AD'den indirmiş hello meta veri dosyası içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="104e3-172">Click Browse and import hello metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="104e3-173">Ardından **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="104e3-173">Then, click **Apply**.</span></span>
   
   ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. <span data-ttu-id="104e3-175">Merhaba, **eşleşen onaylar** bölümünde, hello karşılık gelen kimlik sağlayıcısı onaylama adı için INSERT **e-posta adresi**, **ad**, ve **Soyadı** .</span><span class="sxs-lookup"><span data-stu-id="104e3-175">In hello **Match assertions** section, insert hello corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="104e3-176">tooget Azure AD'den bu bilgileri:</span><span class="sxs-lookup"><span data-stu-id="104e3-176">tooget this information from Azure AD:</span></span> 
  
    <span data-ttu-id="104e3-177">a.</span><span class="sxs-lookup"><span data-stu-id="104e3-177">a.</span></span> <span data-ttu-id="104e3-178">İçinde Azure portal Merhaba, üzerinde hello Git **Tableau çevrimiçi** uygulama tümleştirme sayfası.</span><span class="sxs-lookup"><span data-stu-id="104e3-178">In hello Azure portal, go on hello **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="104e3-179">b.</span><span class="sxs-lookup"><span data-stu-id="104e3-179">b.</span></span> <span data-ttu-id="104e3-180">Merhaba öznitelikleri hello bölümünde **"görüntülemek ve diğer tüm kullanıcı öznitelikleri Düzenle"** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="104e3-180">In hello attributes section, Select hello **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="104e3-182">c.</span><span class="sxs-lookup"><span data-stu-id="104e3-182">c.</span></span> <span data-ttu-id="104e3-183">Merhaba ad alanı değeri bu öznitelikler için kopyalayın: givenname, e-posta ve kullanarak Soyadı hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="104e3-183">Copy hello namespace value for these attributes: givenname, email and surname by using hello following steps:</span></span>

   ![Azure AD çoklu oturum açma](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="104e3-185">d.</span><span class="sxs-lookup"><span data-stu-id="104e3-185">d.</span></span> <span data-ttu-id="104e3-186">Tıklatın **user.givenname** değeri</span><span class="sxs-lookup"><span data-stu-id="104e3-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="104e3-187">e.</span><span class="sxs-lookup"><span data-stu-id="104e3-187">e.</span></span> <span data-ttu-id="104e3-188">Hello Hello değerini kopyalayın **ad alanı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="104e3-188">Copy hello value from hello **namespace** textbox.</span></span>

   ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="104e3-190">f.</span><span class="sxs-lookup"><span data-stu-id="104e3-190">f.</span></span> <span data-ttu-id="104e3-191">Merhaba e-posta ve Soyadı toocopy hello namesapce değerleri hello önceki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="104e3-191">toocopy hello namesapce values for hello email and surname follow hello preceding steps.</span></span>

    <span data-ttu-id="104e3-192">g.</span><span class="sxs-lookup"><span data-stu-id="104e3-192">g.</span></span> <span data-ttu-id="104e3-193">Geçiş toohello Tableau çevrimiçi uygulama sonra ayarlamak hello **çevrimiçi öznitelikleri Tableau** gibi bölümünde:</span><span class="sxs-lookup"><span data-stu-id="104e3-193">Switch toohello Tableau Online application, then set hello **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="104e3-194">E-posta: **posta** veya **userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="104e3-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="104e3-195">Ad: **givenname**</span><span class="sxs-lookup"><span data-stu-id="104e3-195">First name: **givenname**</span></span>
     * <span data-ttu-id="104e3-196">Soyadı: **Soyadı**</span><span class="sxs-lookup"><span data-stu-id="104e3-196">Last name: **surname**</span></span>
   
   ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> <span data-ttu-id="104e3-198">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="104e3-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="104e3-199">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="104e3-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="104e3-200">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="104e3-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="104e3-201">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="104e3-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="104e3-202">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="104e3-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="104e3-204">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="104e3-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="104e3-205">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="104e3-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="104e3-207">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="104e3-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="104e3-209">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="104e3-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="104e3-211">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="104e3-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="104e3-213">a.</span><span class="sxs-lookup"><span data-stu-id="104e3-213">a.</span></span> <span data-ttu-id="104e3-214">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="104e3-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="104e3-215">b.</span><span class="sxs-lookup"><span data-stu-id="104e3-215">b.</span></span> <span data-ttu-id="104e3-216">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="104e3-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="104e3-217">c.</span><span class="sxs-lookup"><span data-stu-id="104e3-217">c.</span></span> <span data-ttu-id="104e3-218">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="104e3-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="104e3-219">d.</span><span class="sxs-lookup"><span data-stu-id="104e3-219">d.</span></span> <span data-ttu-id="104e3-220">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="104e3-220">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="104e3-221">Tableau çevrimiçi bir test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="104e3-221">Creating a Tableau Online test user</span></span>

<span data-ttu-id="104e3-222">Bu bölümde, Britta Simon Tableau çevrimiçi olarak adlandırılan bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="104e3-222">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="104e3-223">Üzerinde **Tableau çevrimiçi**, tıklatın **ayarları** ve ardından **kimlik doğrulaması** bölümü.</span><span class="sxs-lookup"><span data-stu-id="104e3-223">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="104e3-224">Çok ilerleyin**Kullanıcıları Seç** bölümü.</span><span class="sxs-lookup"><span data-stu-id="104e3-224">Scroll down too**Select Users** section.</span></span> <span data-ttu-id="104e3-225">Tıklatın **kullanıcıları eklemek** ve ardından **e-posta adreslerini girin**.</span><span class="sxs-lookup"><span data-stu-id="104e3-225">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="104e3-227">Seçin **çoklu oturum açma (SSO) kimlik doğrulaması için kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="104e3-227">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="104e3-228">Merhaba, **e-posta adreslerini girin** textbox ekleyinbritta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="104e3-228">In hello **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="104e3-230">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="104e3-230">Click **Create**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="104e3-231">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="104e3-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="104e3-232">Bu bölümde, çevrimiçi erişim tooTableau vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="104e3-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Online.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="104e3-234">**tooassign çevrimiçi Britta Simon tooTableau hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="104e3-234">**tooassign Britta Simon tooTableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="104e3-235">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="104e3-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="104e3-237">Merhaba uygulamalar listesinde **Tableau çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="104e3-237">In hello applications list, select **Tableau Online**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. <span data-ttu-id="104e3-239">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="104e3-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="104e3-241">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="104e3-241">Click **Add** button.</span></span> <span data-ttu-id="104e3-242">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="104e3-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="104e3-244">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="104e3-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="104e3-245">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="104e3-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="104e3-246">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="104e3-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="104e3-247">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="104e3-247">Testing single sign-on</span></span>

<span data-ttu-id="104e3-248">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="104e3-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="104e3-249">Merhaba Tableau çevrimiçi hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Tableau çevrimiçi uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="104e3-249">When you click hello Tableau Online tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="104e3-250">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="104e3-250">Additional resources</span></span>

* [<span data-ttu-id="104e3-251">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="104e3-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="104e3-252">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="104e3-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

