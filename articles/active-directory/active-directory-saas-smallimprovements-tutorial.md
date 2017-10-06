---
title: "Öğretici: Azure Active Directory Tümleştirme küçük geliştirmelerle | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve küçük geliştirmeler arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 59c8a112-41e1-4337-9ef3-3d7029780d61
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33213fe4b61f5005cf78bee2c05b2b1e5e71ae8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-small-improvements"></a><span data-ttu-id="c69c7-103">Öğretici: Azure Active Directory Tümleştirme küçük geliştirmelerle</span><span class="sxs-lookup"><span data-stu-id="c69c7-103">Tutorial: Azure Active Directory integration with Small Improvements</span></span>

<span data-ttu-id="c69c7-104">Bu öğreticide, bilgi nasıl toointegrate Azure Active Directory (Azure AD) ile küçük geliştirmeleri.</span><span class="sxs-lookup"><span data-stu-id="c69c7-104">In this tutorial, you learn how toointegrate Small Improvements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c69c7-105">Küçük geliştirmeler Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="c69c7-105">Integrating Small Improvements with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c69c7-106">Erişim tooSmall geliştirmeleri sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c69c7-106">You can control in Azure AD who has access tooSmall Improvements</span></span>
- <span data-ttu-id="c69c7-107">Kullanıcıların tooautomatically get açan tooSmall geliştirmeleri (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c69c7-107">You can enable your users tooautomatically get signed-on tooSmall Improvements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c69c7-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="c69c7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c69c7-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c69c7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c69c7-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c69c7-110">Prerequisites</span></span>

<span data-ttu-id="c69c7-111">tooconfigure küçük geliştirmeleri ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c69c7-111">tooconfigure Azure AD integration with Small Improvements, you need hello following items:</span></span>

- <span data-ttu-id="c69c7-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="c69c7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c69c7-113">Bir küçük geliştirmeleri çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="c69c7-113">A Small Improvements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c69c7-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="c69c7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c69c7-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="c69c7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c69c7-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c69c7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c69c7-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme alabilirsiniz [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c69c7-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c69c7-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="c69c7-118">Scenario description</span></span>
<span data-ttu-id="c69c7-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="c69c7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c69c7-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="c69c7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c69c7-121">Merhaba Galerisi'nden küçük geliştirmeler ekleme</span><span class="sxs-lookup"><span data-stu-id="c69c7-121">Adding Small Improvements from hello gallery</span></span>
2. <span data-ttu-id="c69c7-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c69c7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-small-improvements-from-hello-gallery"></a><span data-ttu-id="c69c7-123">Merhaba Galerisi'nden küçük geliştirmeler ekleme</span><span class="sxs-lookup"><span data-stu-id="c69c7-123">Adding Small Improvements from hello gallery</span></span>
<span data-ttu-id="c69c7-124">Azure AD'ye tooconfigure hello tümleştirme küçük geliştirme tooadd küçük geliştirmeleri hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="c69c7-124">tooconfigure hello integration of Small Improvements into Azure AD, you need tooadd Small Improvements from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c69c7-125">**tooadd hello Galerisi'nden küçük geliştirmeleri hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c69c7-125">**tooadd Small Improvements from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c69c7-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c69c7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c69c7-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="c69c7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c69c7-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c69c7-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="c69c7-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c69c7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="c69c7-133">Merhaba arama kutusuna yazın **küçük geliştirmeleri**.</span><span class="sxs-lookup"><span data-stu-id="c69c7-133">In hello search box, type **Small Improvements**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_search.png)

5. <span data-ttu-id="c69c7-135">Merhaba Sonuçlar panelinde seçin **küçük geliştirmeleri**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="c69c7-135">In hello results panel, select **Small Improvements**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c69c7-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c69c7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c69c7-138">Bu bölümde, yapılandırmak ve küçük "Britta Simon" adlı bir test kullanıcı doğrultusunda geliştirmeler Azure AD çoklu oturum açmayı sınayın.</span><span class="sxs-lookup"><span data-stu-id="c69c7-138">In this section, you configure and test Azure AD single sign-on with Small Improvements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c69c7-139">Tek toowork'ın oturum açma hangi hello karşılık gelen küçük geliştirmeleri tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="c69c7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Small Improvements is tooa user in Azure AD.</span></span> <span data-ttu-id="c69c7-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve küçük geliştirmeleri hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="c69c7-140">In other words, a link relationship between an Azure AD user and hello related user in Small Improvements needs toobe established.</span></span>

<span data-ttu-id="c69c7-141">Küçük yenilikleri hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="c69c7-141">In Small Improvements, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c69c7-142">tooconfigure ve küçük geliştirmeleri ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c69c7-142">tooconfigure and test Azure AD single sign-on with Small Improvements, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c69c7-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="c69c7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c69c7-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="c69c7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c69c7-145">**[Küçük geliştirmeleri test kullanıcısı oluşturma](#creating-a-small-improvements-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir küçük geliştirmeleri, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="c69c7-145">**[Creating a Small Improvements test user](#creating-a-small-improvements-test-user)** - toohave a counterpart of Britta Simon in Small Improvements that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c69c7-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="c69c7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c69c7-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="c69c7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c69c7-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c69c7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c69c7-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma küçük geliştirmeleri uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c69c7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Small Improvements application.</span></span>

<span data-ttu-id="c69c7-150">**tooconfigure Azure AD çoklu oturum açma küçük geliştirmelerle hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c69c7-150">**tooconfigure Azure AD single sign-on with Small Improvements, perform hello following steps:**</span></span>

1. <span data-ttu-id="c69c7-151">Merhaba hello üzerinde Azure portal'ın **küçük geliştirmeleri** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c69c7-151">In hello Azure portal, on hello **Small Improvements** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="c69c7-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="c69c7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_samlbase.png)

3. <span data-ttu-id="c69c7-155">Merhaba üzerinde **küçük geliştirmeler etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c69c7-155">On hello **Small Improvements Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_url.png)

    <span data-ttu-id="c69c7-157">a.</span><span class="sxs-lookup"><span data-stu-id="c69c7-157">a.</span></span> <span data-ttu-id="c69c7-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="c69c7-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    <span data-ttu-id="c69c7-159">b.</span><span class="sxs-lookup"><span data-stu-id="c69c7-159">b.</span></span> <span data-ttu-id="c69c7-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="c69c7-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c69c7-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="c69c7-161">These values are not real.</span></span> <span data-ttu-id="c69c7-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="c69c7-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c69c7-163">Kişi [küçük geliştirmeleri istemci destek ekibi](mailto:support@small-improvements.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="c69c7-163">Contact [Small Improvements Client support team](mailto:support@small-improvements.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="c69c7-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c69c7-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_certificate.png) 

5. <span data-ttu-id="c69c7-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c69c7-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c69c7-168">Merhaba üzerinde **küçük geliştirmeleri yapılandırma** 'yi tıklatın **yapılandırma küçük geliştirmeleri** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="c69c7-168">On hello **Small Improvements Configuration** section, click **Configure Small Improvements** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c69c7-169">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="c69c7-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_configure.png) 

7. <span data-ttu-id="c69c7-171">Başka bir tarayıcı penceresinde tooyour küçük geliştirmeleri şirket sitesinde yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c69c7-171">In another browser window, sign on tooyour Small Improvements company site as an administrator.</span></span>

8. <span data-ttu-id="c69c7-172">Merhaba ana Pano sayfasından tıklatın **Yönetim** hello soldaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c69c7-172">From hello main dashboard page, click **Administration** button on hello left.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_06.png) 

9. <span data-ttu-id="c69c7-174">Merhaba tıklatın **SAML SSO** gelen düğmesini **tümleştirmeler** bölümü.</span><span class="sxs-lookup"><span data-stu-id="c69c7-174">Click hello **SAML SSO** button from **Integrations** section.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_07.png) 

10. <span data-ttu-id="c69c7-176">Merhaba SSO Kurulum sayfasında hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c69c7-176">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_08.png)  

    <span data-ttu-id="c69c7-178">a.</span><span class="sxs-lookup"><span data-stu-id="c69c7-178">a.</span></span> <span data-ttu-id="c69c7-179">Merhaba, **HTTP uç noktası** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="c69c7-179">In hello **HTTP Endpoint** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c69c7-180">b.</span><span class="sxs-lookup"><span data-stu-id="c69c7-180">b.</span></span> <span data-ttu-id="c69c7-181">İndirilen sertifikanızı kopyalama Merhaba içeriğine Not Defteri'nde açın ve hello yapıştırma **x509 sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="c69c7-181">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="c69c7-182">c.</span><span class="sxs-lookup"><span data-stu-id="c69c7-182">c.</span></span> <span data-ttu-id="c69c7-183">Toohave SSO ve oturum açma form kimlik doğrulaması seçeneği kullanıcılar için kullanılabilir istiyorsanız hello denetleyin **oturum açma/parola ile çok erişmesini** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="c69c7-183">If you wish toohave SSO and Login form authentication option available for users, then check hello **Enable access via login/password too** option.</span></span>  

    <span data-ttu-id="c69c7-184">d.</span><span class="sxs-lookup"><span data-stu-id="c69c7-184">d.</span></span> <span data-ttu-id="c69c7-185">Merhaba uygun değeri tooName hello SSO oturum açma düğmesi hello girin **SAML komut istemi** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="c69c7-185">Enter hello appropriate value tooName hello SSO Login button in hello **SAML Prompt** textbox.</span></span>  

    <span data-ttu-id="c69c7-186">e.</span><span class="sxs-lookup"><span data-stu-id="c69c7-186">e.</span></span> <span data-ttu-id="c69c7-187">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c69c7-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c69c7-188">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="c69c7-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c69c7-189">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="c69c7-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c69c7-190">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c69c7-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c69c7-191">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c69c7-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="c69c7-192">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="c69c7-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="c69c7-194">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c69c7-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c69c7-195">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c69c7-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c69c7-197">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c69c7-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c69c7-199">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="c69c7-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c69c7-201">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c69c7-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c69c7-203">a.</span><span class="sxs-lookup"><span data-stu-id="c69c7-203">a.</span></span> <span data-ttu-id="c69c7-204">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c69c7-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c69c7-205">b.</span><span class="sxs-lookup"><span data-stu-id="c69c7-205">b.</span></span> <span data-ttu-id="c69c7-206">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="c69c7-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c69c7-207">c.</span><span class="sxs-lookup"><span data-stu-id="c69c7-207">c.</span></span> <span data-ttu-id="c69c7-208">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="c69c7-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c69c7-209">d.</span><span class="sxs-lookup"><span data-stu-id="c69c7-209">d.</span></span> <span data-ttu-id="c69c7-210">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c69c7-210">Click **Create**.</span></span>
 
### <a name="creating-a-small-improvements-test-user"></a><span data-ttu-id="c69c7-211">Küçük geliştirmeleri test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c69c7-211">Creating a Small Improvements test user</span></span>

<span data-ttu-id="c69c7-212">tooenable Azure AD kullanıcıların toolog tooSmall geliştirmeleri, bunlar küçük artışlarını sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c69c7-212">tooenable Azure AD users toolog in tooSmall Improvements, they must be provisioned into Small Improvements.</span></span> <span data-ttu-id="c69c7-213">Küçük geliştirmeleri Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="c69c7-213">In hello case of Small Improvements, provisioning is a manual task.</span></span>

<span data-ttu-id="c69c7-214">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c69c7-214">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c69c7-215">Yönetici olarak oturum açma tooyour küçük geliştirmeleri şirket sitesi.</span><span class="sxs-lookup"><span data-stu-id="c69c7-215">Sign-on tooyour Small Improvements company site as an administrator.</span></span>

2. <span data-ttu-id="c69c7-216">Merhaba giriş sayfasından toohello menü sol hello üzerinde gidin, tıklatın **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="c69c7-216">From hello Home page, go toohello menu on hello left, click **Administration**.</span></span>

3. <span data-ttu-id="c69c7-217">Merhaba tıklatın **kullanıcı dizini** kullanıcı yönetimi bölümünden düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c69c7-217">Click hello **User Directory** button from User Management section.</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_10.png) 

4. <span data-ttu-id="c69c7-219">Tıklatın **kullanıcıları eklemek**.</span><span class="sxs-lookup"><span data-stu-id="c69c7-219">Click **Add users**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_11.png) 

5. <span data-ttu-id="c69c7-221">Merhaba üzerinde **Kullanıcı Ekle** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c69c7-221">On hello **Add Users** dialog, perform hello following steps:</span></span> 

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_12.png)
    
    <span data-ttu-id="c69c7-223">a.</span><span class="sxs-lookup"><span data-stu-id="c69c7-223">a.</span></span> <span data-ttu-id="c69c7-224">Merhaba girin **ad** gibi kullanıcının **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c69c7-224">Enter hello **first name** of user like **Britta**.</span></span>

    <span data-ttu-id="c69c7-225">b.</span><span class="sxs-lookup"><span data-stu-id="c69c7-225">b.</span></span> <span data-ttu-id="c69c7-226">Merhaba girin **Soyadı** gibi kullanıcının **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c69c7-226">Enter hello **Last name** of user like **Simon**.</span></span>

    <span data-ttu-id="c69c7-227">c.</span><span class="sxs-lookup"><span data-stu-id="c69c7-227">c.</span></span> <span data-ttu-id="c69c7-228">Merhaba girin **e-posta** gibi kullanıcının  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="c69c7-228">Enter hello **Email** of user like **brittasimon@contoso.com**.</span></span> 

    <span data-ttu-id="c69c7-229">d.</span><span class="sxs-lookup"><span data-stu-id="c69c7-229">d.</span></span> <span data-ttu-id="c69c7-230">Tooenter hello kişisel ileti hello seçebilirsiniz **bildirim e-posta Gönder** kutusu.</span><span class="sxs-lookup"><span data-stu-id="c69c7-230">You can also choose tooenter hello personal message in hello **Send notification email** box.</span></span> <span data-ttu-id="c69c7-231">Toosend hello bildirim istemiyorsanız bu onay kutusunun işaretini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="c69c7-231">If you do not wish toosend hello notification, then uncheck this checkbox.</span></span>

    <span data-ttu-id="c69c7-232">e.</span><span class="sxs-lookup"><span data-stu-id="c69c7-232">e.</span></span> <span data-ttu-id="c69c7-233">Tıklatın **kullanıcılar oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="c69c7-233">Click **Create Users**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c69c7-234">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="c69c7-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c69c7-235">Bu bölümde, tooSmall geliştirmeleri erişim vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c69c7-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSmall Improvements.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="c69c7-237">**tooassign Britta Simon tooSmall geliştirmeleri, başlangıç aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c69c7-237">**tooassign Britta Simon tooSmall Improvements, perform hello following steps:**</span></span>

1. <span data-ttu-id="c69c7-238">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c69c7-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="c69c7-240">Merhaba uygulamalar listesinde **küçük geliştirmeleri**.</span><span class="sxs-lookup"><span data-stu-id="c69c7-240">In hello applications list, select **Small Improvements**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_app.png) 

3. <span data-ttu-id="c69c7-242">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c69c7-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="c69c7-244">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c69c7-244">Click **Add** button.</span></span> <span data-ttu-id="c69c7-245">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c69c7-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="c69c7-247">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="c69c7-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c69c7-248">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c69c7-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c69c7-249">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c69c7-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c69c7-250">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="c69c7-250">Testing single sign-on</span></span>

<span data-ttu-id="c69c7-251">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c69c7-251">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="c69c7-252">Küçük geliştirmeleri hello erişim paneli döşeme hello tıkladığınızda, otomatik olarak imzalanmış üzerinde küçük geliştirmeleri uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c69c7-252">When you click hello Small Improvements tile in hello Access Panel, you should get automatically signed-on tooyour Small Improvements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c69c7-253">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c69c7-253">Additional resources</span></span>

* [<span data-ttu-id="c69c7-254">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="c69c7-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c69c7-255">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="c69c7-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_203.png

