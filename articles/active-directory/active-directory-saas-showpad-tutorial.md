---
title: "Öğretici: Azure Active Directory Tümleştirme ile Showpad | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Showpad arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48b6bee0-dbc5-4863-964d-75b25e517741
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2c8c306b4b94c368a93f92123d3abe9fe35167db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-showpad"></a><span data-ttu-id="66eaf-103">Öğretici: Azure Active Directory Tümleştirme Showpad ile</span><span class="sxs-lookup"><span data-stu-id="66eaf-103">Tutorial: Azure Active Directory integration with Showpad</span></span>

<span data-ttu-id="66eaf-104">Bu öğreticide, bilgi nasıl toointegrate Showpad Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="66eaf-104">In this tutorial, you learn how toointegrate Showpad with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="66eaf-105">Showpad Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="66eaf-105">Integrating Showpad with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="66eaf-106">Erişim tooShowpad sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="66eaf-106">You can control in Azure AD who has access tooShowpad</span></span>
- <span data-ttu-id="66eaf-107">Kullanıcıların tooautomatically get açan tooShowpad (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="66eaf-107">You can enable your users tooautomatically get signed-on tooShowpad (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="66eaf-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="66eaf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="66eaf-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="66eaf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66eaf-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="66eaf-110">Prerequisites</span></span>

<span data-ttu-id="66eaf-111">tooconfigure Showpad ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="66eaf-111">tooconfigure Azure AD integration with Showpad, you need hello following items:</span></span>

- <span data-ttu-id="66eaf-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="66eaf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="66eaf-113">Bir Showpad çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="66eaf-113">A Showpad single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="66eaf-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="66eaf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="66eaf-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="66eaf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="66eaf-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="66eaf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="66eaf-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="66eaf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="66eaf-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="66eaf-118">Scenario description</span></span>
<span data-ttu-id="66eaf-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="66eaf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="66eaf-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="66eaf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="66eaf-121">Merhaba Galerisi'nden Showpad ekleme</span><span class="sxs-lookup"><span data-stu-id="66eaf-121">Adding Showpad from hello gallery</span></span>
2. <span data-ttu-id="66eaf-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="66eaf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-showpad-from-hello-gallery"></a><span data-ttu-id="66eaf-123">Merhaba Galerisi'nden Showpad ekleme</span><span class="sxs-lookup"><span data-stu-id="66eaf-123">Adding Showpad from hello gallery</span></span>

<span data-ttu-id="66eaf-124">Azure AD'ye tooconfigure hello tümleştirme Showpad, tooadd Showpad hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="66eaf-124">tooconfigure hello integration of Showpad into Azure AD, you need tooadd Showpad from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="66eaf-125">**tooadd Showpad hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="66eaf-125">**tooadd Showpad from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="66eaf-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="66eaf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="66eaf-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="66eaf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="66eaf-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="66eaf-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="66eaf-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="66eaf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="66eaf-133">Merhaba arama kutusuna yazın **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="66eaf-133">In hello search box, type **Showpad**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_search.png)

5. <span data-ttu-id="66eaf-135">Merhaba Sonuçlar panelinde seçin **Showpad**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="66eaf-135">In hello results panel, select **Showpad**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="66eaf-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="66eaf-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="66eaf-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Showpad ile test etme</span><span class="sxs-lookup"><span data-stu-id="66eaf-138">In this section, you configure and test Azure AD single sign-on with Showpad based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="66eaf-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Showpad içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="66eaf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Showpad is tooa user in Azure AD.</span></span> <span data-ttu-id="66eaf-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Showpad hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="66eaf-140">In other words, a link relationship between an Azure AD user and hello related user in Showpad needs toobe established.</span></span>

<span data-ttu-id="66eaf-141">Merhaba hello değeri Showpad içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="66eaf-141">In Showpad, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="66eaf-142">tooconfigure ve Showpad ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="66eaf-142">tooconfigure and test Azure AD single sign-on with Showpad, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="66eaf-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="66eaf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="66eaf-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="66eaf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="66eaf-145">**[Showpad test kullanıcısı oluşturma](#creating-a-showpad-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Showpad içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="66eaf-145">**[Creating a Showpad test user](#creating-a-showpad-test-user)** - toohave a counterpart of Britta Simon in Showpad that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="66eaf-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="66eaf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="66eaf-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="66eaf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="66eaf-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="66eaf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="66eaf-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Showpad uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="66eaf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Showpad application.</span></span>

<span data-ttu-id="66eaf-150">**tooconfigure Azure AD çoklu oturum açma ile Showpad, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="66eaf-150">**tooconfigure Azure AD single sign-on with Showpad, perform hello following steps:**</span></span>

1. <span data-ttu-id="66eaf-151">Hello hello üzerinde Azure portal'ın **Showpad** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="66eaf-151">In hello Azure portal, on hello **Showpad** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="66eaf-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="66eaf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_samlbase.png)

3. <span data-ttu-id="66eaf-155">Merhaba üzerinde **Showpad etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="66eaf-155">On hello **Showpad Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_url.png)

    <span data-ttu-id="66eaf-157">a.</span><span class="sxs-lookup"><span data-stu-id="66eaf-157">a.</span></span> <span data-ttu-id="66eaf-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<comapany-name>.showpad.biz/login`</span><span class="sxs-lookup"><span data-stu-id="66eaf-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<comapany-name>.showpad.biz/login`</span></span>

    <span data-ttu-id="66eaf-159">b.</span><span class="sxs-lookup"><span data-stu-id="66eaf-159">b.</span></span> <span data-ttu-id="66eaf-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company-name>.showpad.biz`</span><span class="sxs-lookup"><span data-stu-id="66eaf-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company-name>.showpad.biz`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="66eaf-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="66eaf-161">These values are not real.</span></span> <span data-ttu-id="66eaf-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="66eaf-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="66eaf-163">Kişi [Showpad destek ekibi](https://help.showpad.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="66eaf-163">Contact [Showpad support team](https://help.showpad.com) tooget these values.</span></span> 
 


4. <span data-ttu-id="66eaf-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="66eaf-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_certificate.png) 

5. <span data-ttu-id="66eaf-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="66eaf-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-showpad-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="66eaf-168">Yönetici olarak oturum açma tooyour Showpad Kiracı.</span><span class="sxs-lookup"><span data-stu-id="66eaf-168">Sign-on tooyour Showpad tenant as an administrator.</span></span>

7. <span data-ttu-id="66eaf-169">Hello'nde hello üstte, hello menüsünü **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="66eaf-169">In hello menu on hello top, click hello **Settings**.</span></span>
   
    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_001.png) 

8. <span data-ttu-id="66eaf-171">Çok gidin"**çoklu oturum açma**"tıklatıp"**etkinleştirmek**."</span><span class="sxs-lookup"><span data-stu-id="66eaf-171">Navigate too"**Single Sign-On**" and click "**Enable**."</span></span>
   
    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_002.png)

9. <span data-ttu-id="66eaf-173">Merhaba üzerinde **SAML 2.0 hizmet ekleme** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="66eaf-173">On hello **Add a SAML 2.0 Service** dialog, perform hello following steps:</span></span>
   
    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_003.png) 
   
    <span data-ttu-id="66eaf-175">a.</span><span class="sxs-lookup"><span data-stu-id="66eaf-175">a.</span></span> <span data-ttu-id="66eaf-176">Merhaba, **adı** metin kutusuna, tür hello tanımlayıcı sağlayıcı adını (örneğin: şirketinizin adını).</span><span class="sxs-lookup"><span data-stu-id="66eaf-176">In hello **Name** textbox, type hello name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="66eaf-177">b.</span><span class="sxs-lookup"><span data-stu-id="66eaf-177">b.</span></span> <span data-ttu-id="66eaf-178">Olarak **meta veri kaynağı**seçin **XML**.</span><span class="sxs-lookup"><span data-stu-id="66eaf-178">As **Metadata Source**, select **XML**.</span></span>
   
    <span data-ttu-id="66eaf-179">c.</span><span class="sxs-lookup"><span data-stu-id="66eaf-179">c.</span></span> <span data-ttu-id="66eaf-180">Azure portal hello indirmiş, meta veri XML dosyası Merhaba içeriğine kopyalayın ve hello yapıştırma **meta veri XML** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="66eaf-180">Copy hello content of metadata XML file, which you have downloaded from hello Azure portal, and then paste it into hello **Metadata XML** textbox.</span></span>
   
    <span data-ttu-id="66eaf-181">d.</span><span class="sxs-lookup"><span data-stu-id="66eaf-181">d.</span></span> <span data-ttu-id="66eaf-182">Seçin **otomatik sağlama hesapları için yeni kullanıcılar oturum açtığında**.</span><span class="sxs-lookup"><span data-stu-id="66eaf-182">Select **Auto-provision accounts for new users when they log in**.</span></span>
   
    <span data-ttu-id="66eaf-183">e.</span><span class="sxs-lookup"><span data-stu-id="66eaf-183">e.</span></span> <span data-ttu-id="66eaf-184">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="66eaf-184">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="66eaf-185">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="66eaf-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="66eaf-186">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="66eaf-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="66eaf-187">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="66eaf-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="66eaf-188">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="66eaf-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="66eaf-189">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="66eaf-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="66eaf-191">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="66eaf-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="66eaf-192">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="66eaf-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-showpad-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="66eaf-194">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="66eaf-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-showpad-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="66eaf-196">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="66eaf-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-showpad-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="66eaf-198">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="66eaf-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-showpad-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="66eaf-200">a.</span><span class="sxs-lookup"><span data-stu-id="66eaf-200">a.</span></span> <span data-ttu-id="66eaf-201">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="66eaf-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="66eaf-202">b.</span><span class="sxs-lookup"><span data-stu-id="66eaf-202">b.</span></span> <span data-ttu-id="66eaf-203">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="66eaf-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="66eaf-204">c.</span><span class="sxs-lookup"><span data-stu-id="66eaf-204">c.</span></span> <span data-ttu-id="66eaf-205">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="66eaf-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="66eaf-206">d.</span><span class="sxs-lookup"><span data-stu-id="66eaf-206">d.</span></span> <span data-ttu-id="66eaf-207">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="66eaf-207">Click **Create**.</span></span>
 
### <a name="creating-a-showpad-test-user"></a><span data-ttu-id="66eaf-208">Showpad test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="66eaf-208">Creating a Showpad test user</span></span>

<span data-ttu-id="66eaf-209">Bu bölümde Hello amacı toocreate Britta Simon içinde Showpad adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="66eaf-209">hello objective of this section is toocreate a user called Britta Simon in Showpad.</span></span> 

<span data-ttu-id="66eaf-210">Yalnızca zaman sağlama Showpad destekler.</span><span class="sxs-lookup"><span data-stu-id="66eaf-210">Showpad supports just-in-time provisioning.</span></span> <span data-ttu-id="66eaf-211">Sağlamayı etkinleştirdiğiniz  **[yapılandırma Azure AD çoklu oturum açma](#configuring-azure-ad-single-sign-on)**.</span><span class="sxs-lookup"><span data-stu-id="66eaf-211">You have enabled provisioning in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**.</span></span> 

<span data-ttu-id="66eaf-212">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="66eaf-212">There is no action item for you in this section.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="66eaf-213">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="66eaf-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="66eaf-214">Bu bölümde, erişim tooShowpad vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="66eaf-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooShowpad.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="66eaf-216">**tooassign Britta Simon tooShowpad hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="66eaf-216">**tooassign Britta Simon tooShowpad, perform hello following steps:**</span></span>

1. <span data-ttu-id="66eaf-217">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="66eaf-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="66eaf-219">Merhaba uygulamalar listesinde **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="66eaf-219">In hello applications list, select **Showpad**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_app.png) 

3. <span data-ttu-id="66eaf-221">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="66eaf-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="66eaf-223">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="66eaf-223">Click **Add** button.</span></span> <span data-ttu-id="66eaf-224">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="66eaf-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="66eaf-226">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="66eaf-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="66eaf-227">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="66eaf-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="66eaf-228">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="66eaf-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="66eaf-229">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="66eaf-229">Testing single sign-on</span></span>

<span data-ttu-id="66eaf-230">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="66eaf-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="66eaf-231">Merhaba Showpad hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooShowpad uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="66eaf-231">When you click hello Showpad tile in hello Access Panel, you should get automatically signed-on tooShowpad application.</span></span>
<span data-ttu-id="66eaf-232">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="66eaf-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="66eaf-233">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="66eaf-233">Additional resources</span></span>

* [<span data-ttu-id="66eaf-234">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="66eaf-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="66eaf-235">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="66eaf-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_203.png

