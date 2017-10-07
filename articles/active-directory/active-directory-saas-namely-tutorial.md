---
title: "Öğretici: Azure Active Directory Tümleştirme ile öğesine | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory arasında ve öğesine."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: b0477ca6fa52a21abea7de458f8a99a01e8c25c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a><span data-ttu-id="35b1a-103">Öğretici: Azure Active Directory Tümleştirme ile özelliği</span><span class="sxs-lookup"><span data-stu-id="35b1a-103">Tutorial: Azure Active Directory integration with Namely</span></span>

<span data-ttu-id="35b1a-104">Bu öğreticide, bilgi nasıl toointegrate Azure Active Directory (Azure AD) öğesine sahip.</span><span class="sxs-lookup"><span data-stu-id="35b1a-104">In this tutorial, you learn how toointegrate Namely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="35b1a-105">Yani Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="35b1a-105">Integrating Namely with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="35b1a-106">Erişim tooNamely sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="35b1a-106">You can control in Azure AD who has access tooNamely</span></span>
- <span data-ttu-id="35b1a-107">Kullanıcıların tooautomatically get açan tooNamely (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="35b1a-107">You can enable your users tooautomatically get signed-on tooNamely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="35b1a-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="35b1a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="35b1a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="35b1a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35b1a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="35b1a-110">Prerequisites</span></span>

<span data-ttu-id="35b1a-111">Yani, sizinle tooconfigure Azure AD tümleştirme aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="35b1a-111">tooconfigure Azure AD integration with Namely, you need hello following items:</span></span>

- <span data-ttu-id="35b1a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="35b1a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="35b1a-113">Bir öğesine çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="35b1a-113">A Namely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="35b1a-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="35b1a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="35b1a-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="35b1a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="35b1a-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="35b1a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="35b1a-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35b1a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="35b1a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="35b1a-118">Scenario description</span></span>
<span data-ttu-id="35b1a-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="35b1a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="35b1a-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="35b1a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="35b1a-121">Yani hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="35b1a-121">Adding Namely from hello gallery</span></span>
2. <span data-ttu-id="35b1a-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="35b1a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-namely-from-hello-gallery"></a><span data-ttu-id="35b1a-123">Yani hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="35b1a-123">Adding Namely from hello gallery</span></span>
<span data-ttu-id="35b1a-124">tooconfigure hello tümleştirilmesi, yani Azure AD, yani listesinden hello galeri tooyour yönetilen SaaS uygulamaları tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="35b1a-124">tooconfigure hello integration of Namely into Azure AD, you need tooadd Namely from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="35b1a-125">**Yani Galerisi'nden hello tooadd hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="35b1a-125">**tooadd Namely from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="35b1a-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="35b1a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="35b1a-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="35b1a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="35b1a-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="35b1a-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="35b1a-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="35b1a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="35b1a-133">Merhaba arama kutusuna yazın **öğesine**.</span><span class="sxs-lookup"><span data-stu-id="35b1a-133">In hello search box, type **Namely**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. <span data-ttu-id="35b1a-135">Merhaba Sonuçlar panelinde seçin **öğesine**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="35b1a-135">In hello results panel, select **Namely**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="35b1a-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="35b1a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="35b1a-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile "Britta Simon" adlı bir test kullanıcı öğesine göre test etme.</span><span class="sxs-lookup"><span data-stu-id="35b1a-138">In this section, you configure and test Azure AD single sign-on with Namely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="35b1a-139">Tek toowork'ın oturum açma hangi hello karşılık gelen, yani tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="35b1a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Namely is tooa user in Azure AD.</span></span> <span data-ttu-id="35b1a-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı arasındaki bağlantıyı ilişki öğesine kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="35b1a-140">In other words, a link relationship between an Azure AD user and hello related user in Namely needs toobe established.</span></span>

<span data-ttu-id="35b1a-141">Yani, hello hello değeri olarak atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="35b1a-141">In Namely, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="35b1a-142">tooconfigure ve Azure AD çoklu oturum açmayı test adlı, sizinle yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="35b1a-142">tooconfigure and test Azure AD single sign-on with Namely, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="35b1a-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="35b1a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="35b1a-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="35b1a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="35b1a-145">**[Oluşturma bir öğesine test kullanıcısı](#creating-a-namely-test-user)**  -toohave bir Britta Simon karşılık gelen adlı başka bir deyişle bağlantılı toohello Azure AD kullanıcı gösterimini içinde.</span><span class="sxs-lookup"><span data-stu-id="35b1a-145">**[Creating a Namely test user](#creating-a-namely-test-user)** - toohave a counterpart of Britta Simon in Namely that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="35b1a-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="35b1a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="35b1a-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="35b1a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="35b1a-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="35b1a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="35b1a-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirmek ve çoklu oturum açma, yani uygulama yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="35b1a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Namely application.</span></span>

<span data-ttu-id="35b1a-150">**tooconfigure Azure AD çoklu oturum açma ile öğesine, gerçekleştirme adımları izleyerek hello:**</span><span class="sxs-lookup"><span data-stu-id="35b1a-150">**tooconfigure Azure AD single sign-on with Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="35b1a-151">Merhaba hello üzerinde Azure portal'ın **öğesine** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="35b1a-151">In hello Azure portal, on hello **Namely** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="35b1a-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="35b1a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. <span data-ttu-id="35b1a-155">Merhaba üzerinde **adlı etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="35b1a-155">On hello **Namely Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    <span data-ttu-id="35b1a-157">a.</span><span class="sxs-lookup"><span data-stu-id="35b1a-157">a.</span></span> <span data-ttu-id="35b1a-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.namely.com`</span><span class="sxs-lookup"><span data-stu-id="35b1a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com`</span></span>

    <span data-ttu-id="35b1a-159">b.</span><span class="sxs-lookup"><span data-stu-id="35b1a-159">b.</span></span> <span data-ttu-id="35b1a-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.namely.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="35b1a-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="35b1a-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="35b1a-161">These values are not real.</span></span> <span data-ttu-id="35b1a-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="35b1a-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="35b1a-163">Kişi [öğesine istemci destek ekibi](https://www.namely.com/contact/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="35b1a-163">Contact [Namely Client support team](https://www.namely.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="35b1a-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="35b1a-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. <span data-ttu-id="35b1a-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="35b1a-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="35b1a-168">Merhaba üzerinde **öğesine yapılandırma** 'yi tıklatın **öğesine yapılandırma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="35b1a-168">On hello **Namely Configuration** section, click **Configure Namely** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="35b1a-169">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="35b1a-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. <span data-ttu-id="35b1a-171">Başka bir tarayıcı penceresinde tooyour üzerinde öğesine şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="35b1a-171">In another browser window, sign on tooyour Namely company site as an administrator.</span></span>

8. <span data-ttu-id="35b1a-172">Merhaba üstte Hello araç çubuğunda **şirket**.</span><span class="sxs-lookup"><span data-stu-id="35b1a-172">In hello toolbar on hello top, click **Company**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. <span data-ttu-id="35b1a-174">Merhaba tıklatın **ayarları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="35b1a-174">Click hello **Settings** tab.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. <span data-ttu-id="35b1a-176">Tıklatın **SAML**.</span><span class="sxs-lookup"><span data-stu-id="35b1a-176">Click **SAML**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. <span data-ttu-id="35b1a-178">Merhaba üzerinde **SAML ayarları** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="35b1a-178">On hello **SAML Settings** page, perform hello following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    <span data-ttu-id="35b1a-180">a.</span><span class="sxs-lookup"><span data-stu-id="35b1a-180">a.</span></span> <span data-ttu-id="35b1a-181">Tıklatın **etkinleştirmek SAML**.</span><span class="sxs-lookup"><span data-stu-id="35b1a-181">Click **Enable SAML**.</span></span> 

    <span data-ttu-id="35b1a-182">b.</span><span class="sxs-lookup"><span data-stu-id="35b1a-182">b.</span></span> <span data-ttu-id="35b1a-183">Merhaba, **kimlik sağlayıcısı SSO URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="35b1a-183">In hello **Identity provider SSO url** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="35b1a-184">c.</span><span class="sxs-lookup"><span data-stu-id="35b1a-184">c.</span></span> <span data-ttu-id="35b1a-185">İndirilen sertifikanızı kopyalama Merhaba içeriğine Not Defteri'nde açın ve hello yapıştırma **kimlik sağlayıcısı sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="35b1a-185">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **Identity provider certificate** textbox.</span></span>
     
    <span data-ttu-id="35b1a-186">d.</span><span class="sxs-lookup"><span data-stu-id="35b1a-186">d.</span></span> <span data-ttu-id="35b1a-187">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35b1a-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="35b1a-188">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="35b1a-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="35b1a-189">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="35b1a-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="35b1a-190">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="35b1a-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="35b1a-191">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="35b1a-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="35b1a-192">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="35b1a-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="35b1a-194">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="35b1a-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="35b1a-195">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="35b1a-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="35b1a-197">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="35b1a-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="35b1a-199">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="35b1a-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="35b1a-201">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="35b1a-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="35b1a-203">a.</span><span class="sxs-lookup"><span data-stu-id="35b1a-203">a.</span></span> <span data-ttu-id="35b1a-204">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="35b1a-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="35b1a-205">b.</span><span class="sxs-lookup"><span data-stu-id="35b1a-205">b.</span></span> <span data-ttu-id="35b1a-206">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="35b1a-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="35b1a-207">c.</span><span class="sxs-lookup"><span data-stu-id="35b1a-207">c.</span></span> <span data-ttu-id="35b1a-208">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="35b1a-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="35b1a-209">d.</span><span class="sxs-lookup"><span data-stu-id="35b1a-209">d.</span></span> <span data-ttu-id="35b1a-210">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35b1a-210">Click **Create**.</span></span>
 
### <a name="creating-a-namely-test-user"></a><span data-ttu-id="35b1a-211">Oluşturma bir öğesine test kullanıcısı</span><span class="sxs-lookup"><span data-stu-id="35b1a-211">Creating a Namely test user</span></span>

<span data-ttu-id="35b1a-212">Bu bölümde Hello amacı toocreate Britta Simon öğesine adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="35b1a-212">hello objective of this section is toocreate a user called Britta Simon in Namely.</span></span>

<span data-ttu-id="35b1a-213">**toocreate Britta Simon öğesine, adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="35b1a-213">**toocreate a user called Britta Simon in Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="35b1a-214">Oturum açma tooyour yönetici olarak öğesine site şirket.</span><span class="sxs-lookup"><span data-stu-id="35b1a-214">Sign-on tooyour Namely company site as an administrator.</span></span>

2. <span data-ttu-id="35b1a-215">Merhaba üstte Hello araç çubuğunda **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="35b1a-215">In hello toolbar on hello top, click **People**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. <span data-ttu-id="35b1a-217">Merhaba tıklatın **Directory** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="35b1a-217">Click hello **Directory** tab.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. <span data-ttu-id="35b1a-219">Tıklatın **yeni bir kişiye eklemek**.</span><span class="sxs-lookup"><span data-stu-id="35b1a-219">Click **Add New Person**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. <span data-ttu-id="35b1a-221">Merhaba üzerinde **Yeni Kişi Ekle** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="35b1a-221">On hello **Add New Person** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="35b1a-222">a.</span><span class="sxs-lookup"><span data-stu-id="35b1a-222">a.</span></span> <span data-ttu-id="35b1a-223">Merhaba, **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="35b1a-223">In hello **First name** textbox, type **Britta**.</span></span>

    <span data-ttu-id="35b1a-224">b.</span><span class="sxs-lookup"><span data-stu-id="35b1a-224">b.</span></span> <span data-ttu-id="35b1a-225">Merhaba, **Soyadı** metin kutusuna, türü **Simon**.</span><span class="sxs-lookup"><span data-stu-id="35b1a-225">In hello **Last name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="35b1a-226">c.</span><span class="sxs-lookup"><span data-stu-id="35b1a-226">c.</span></span> <span data-ttu-id="35b1a-227">Merhaba, **e-posta** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="35b1a-227">In hello **Email** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="35b1a-228">d.</span><span class="sxs-lookup"><span data-stu-id="35b1a-228">d.</span></span> <span data-ttu-id="35b1a-229">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35b1a-229">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="35b1a-230">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="35b1a-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="35b1a-231">Bu bölümde, erişim tooNamely vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="35b1a-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNamely.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="35b1a-233">**tooassign Britta Simon tooNamely hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="35b1a-233">**tooassign Britta Simon tooNamely, perform hello following steps:**</span></span>

1. <span data-ttu-id="35b1a-234">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="35b1a-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="35b1a-236">Merhaba uygulamalar listesinde **öğesine**.</span><span class="sxs-lookup"><span data-stu-id="35b1a-236">In hello applications list, select **Namely**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. <span data-ttu-id="35b1a-238">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="35b1a-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="35b1a-240">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="35b1a-240">Click **Add** button.</span></span> <span data-ttu-id="35b1a-241">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="35b1a-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="35b1a-243">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="35b1a-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="35b1a-244">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="35b1a-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="35b1a-245">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="35b1a-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="35b1a-246">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="35b1a-246">Testing single sign-on</span></span>

<span data-ttu-id="35b1a-247">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="35b1a-247">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="35b1a-248">Merhaba tıklattığınızda öğesine hello erişim paneli döşeme, otomatik olarak oturum açma tooyour öğesine uygulama almanız gerekir</span><span class="sxs-lookup"><span data-stu-id="35b1a-248">When you click hello Namely tile in hello Access Panel, you should get automatically signed-on tooyour Namely application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="35b1a-249">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="35b1a-249">Additional resources</span></span>

* [<span data-ttu-id="35b1a-250">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="35b1a-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="35b1a-251">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="35b1a-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png

