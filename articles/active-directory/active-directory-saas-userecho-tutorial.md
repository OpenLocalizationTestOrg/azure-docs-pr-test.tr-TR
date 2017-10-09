---
title: "Öğretici: Azure Active Directory Tümleştirme ile UserEcho | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile UserEcho arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: efe4a94ed6e5d22d153565d4782850eac4dff37b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a><span data-ttu-id="655d8-103">Öğretici: Azure Active Directory Tümleştirme UserEcho ile</span><span class="sxs-lookup"><span data-stu-id="655d8-103">Tutorial: Azure Active Directory integration with UserEcho</span></span>

<span data-ttu-id="655d8-104">Bu öğreticide, bilgi nasıl toointegrate UserEcho Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="655d8-104">In this tutorial, you learn how toointegrate UserEcho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="655d8-105">UserEcho Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="655d8-105">Integrating UserEcho with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="655d8-106">Erişim tooUserEcho sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="655d8-106">You can control in Azure AD who has access tooUserEcho</span></span>
- <span data-ttu-id="655d8-107">Kullanıcıların tooautomatically get açan tooUserEcho (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="655d8-107">You can enable your users tooautomatically get signed-on tooUserEcho (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="655d8-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="655d8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="655d8-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="655d8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="655d8-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="655d8-110">Prerequisites</span></span>

<span data-ttu-id="655d8-111">tooconfigure UserEcho ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="655d8-111">tooconfigure Azure AD integration with UserEcho, you need hello following items:</span></span>

- <span data-ttu-id="655d8-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="655d8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="655d8-113">Bir UserEcho çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="655d8-113">A UserEcho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="655d8-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="655d8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="655d8-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="655d8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="655d8-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="655d8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="655d8-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="655d8-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="655d8-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="655d8-118">Scenario description</span></span>
<span data-ttu-id="655d8-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="655d8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="655d8-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="655d8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="655d8-121">Merhaba Galerisi'nden UserEcho ekleme</span><span class="sxs-lookup"><span data-stu-id="655d8-121">Adding UserEcho from hello gallery</span></span>
2. <span data-ttu-id="655d8-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="655d8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-userecho-from-hello-gallery"></a><span data-ttu-id="655d8-123">Merhaba Galerisi'nden UserEcho ekleme</span><span class="sxs-lookup"><span data-stu-id="655d8-123">Adding UserEcho from hello gallery</span></span>
<span data-ttu-id="655d8-124">Azure AD'ye tooconfigure hello tümleştirme UserEcho, tooadd UserEcho hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="655d8-124">tooconfigure hello integration of UserEcho into Azure AD, you need tooadd UserEcho from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="655d8-125">**tooadd UserEcho hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="655d8-125">**tooadd UserEcho from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="655d8-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="655d8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="655d8-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="655d8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="655d8-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="655d8-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="655d8-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="655d8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="655d8-133">Merhaba arama kutusuna yazın **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="655d8-133">In hello search box, type **UserEcho**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_search.png)

5. <span data-ttu-id="655d8-135">Merhaba Sonuçlar panelinde seçin **UserEcho**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="655d8-135">In hello results panel, select **UserEcho**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="655d8-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="655d8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="655d8-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı UserEcho sınayın.</span><span class="sxs-lookup"><span data-stu-id="655d8-138">In this section, you configure and test Azure AD single sign-on with UserEcho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="655d8-139">Tek toowork'ın oturum açma hangi hello karşılık gelen UserEcho içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="655d8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UserEcho is tooa user in Azure AD.</span></span> <span data-ttu-id="655d8-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı UserEcho hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="655d8-140">In other words, a link relationship between an Azure AD user and hello related user in UserEcho needs toobe established.</span></span>

<span data-ttu-id="655d8-141">Merhaba hello değeri UserEcho içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="655d8-141">In UserEcho, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="655d8-142">tooconfigure ve UserEcho ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="655d8-142">tooconfigure and test Azure AD single sign-on with UserEcho, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="655d8-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="655d8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="655d8-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="655d8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="655d8-145">**[UserEcho test kullanıcısı oluşturma](#creating-a-userecho-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir UserEcho içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="655d8-145">**[Creating a UserEcho test user](#creating-a-userecho-test-user)** - toohave a counterpart of Britta Simon in UserEcho that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="655d8-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="655d8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="655d8-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="655d8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="655d8-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="655d8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="655d8-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma UserEcho uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="655d8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UserEcho application.</span></span>

<span data-ttu-id="655d8-150">**tooconfigure Azure AD çoklu oturum açma ile UserEcho, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="655d8-150">**tooconfigure Azure AD single sign-on with UserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="655d8-151">Hello hello üzerinde Azure portal'ın **UserEcho** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="655d8-151">In hello Azure portal, on hello **UserEcho** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="655d8-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="655d8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_samlbase.png)

3. <span data-ttu-id="655d8-155">Merhaba üzerinde **UserEcho etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="655d8-155">On hello **UserEcho Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_url.png)

    <span data-ttu-id="655d8-157">a.</span><span class="sxs-lookup"><span data-stu-id="655d8-157">a.</span></span> <span data-ttu-id="655d8-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.userecho.com/`</span><span class="sxs-lookup"><span data-stu-id="655d8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.userecho.com/`</span></span>

    <span data-ttu-id="655d8-159">b.</span><span class="sxs-lookup"><span data-stu-id="655d8-159">b.</span></span> <span data-ttu-id="655d8-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.userecho.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="655d8-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.userecho.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="655d8-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="655d8-161">These values are not real.</span></span> <span data-ttu-id="655d8-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="655d8-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="655d8-163">Kişi [UserEcho istemci destek ekibi](https://feedback.userecho.com/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="655d8-163">Contact [UserEcho Client support team](https://feedback.userecho.com/) tooget these values.</span></span> 

4. <span data-ttu-id="655d8-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="655d8-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_certificate.png) 

5. <span data-ttu-id="655d8-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="655d8-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="655d8-168">Merhaba üzerinde **UserEcho yapılandırma** 'yi tıklatın **yapılandırma UserEcho** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="655d8-168">On hello **UserEcho Configuration** section, click **Configure UserEcho** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="655d8-169">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="655d8-169">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_configure.png) 

7. <span data-ttu-id="655d8-171">Başka bir tarayıcı penceresinde tooyour UserEcho şirket sitesinde yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="655d8-171">In another browser window, sign on tooyour UserEcho company site as an administrator.</span></span>

8. <span data-ttu-id="655d8-172">Merhaba araç hello üstte, kullanıcı adı tooexpand hello menüsünü tıklatın ve ardından **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="655d8-172">In hello toolbar on hello top, click your user name tooexpand hello menu, and then click **Setup**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 

9. <span data-ttu-id="655d8-174">Tıklatın **tümleştirmeler**.</span><span class="sxs-lookup"><span data-stu-id="655d8-174">Click **Integrations**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_07.png) 

10. <span data-ttu-id="655d8-176">Tıklatın **Web sitesi**ve ardından **çoklu oturum açma (SAML2)**.</span><span class="sxs-lookup"><span data-stu-id="655d8-176">Click **Website**, and then click **Single sign-on (SAML2)**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_08.png) 

11. <span data-ttu-id="655d8-178">Merhaba üzerinde **çoklu oturum açma (SAML)** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="655d8-178">On hello **Single sign-on (SAML)** page, perform hello following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_09.png)
    
    <span data-ttu-id="655d8-180">a.</span><span class="sxs-lookup"><span data-stu-id="655d8-180">a.</span></span> <span data-ttu-id="655d8-181">Olarak **SAML etkin**seçin **Evet**.</span><span class="sxs-lookup"><span data-stu-id="655d8-181">As **SAML-enabled**, select **Yes**.</span></span>
    
    <span data-ttu-id="655d8-182">b.</span><span class="sxs-lookup"><span data-stu-id="655d8-182">b.</span></span> <span data-ttu-id="655d8-183">Yapıştır **SAML çoklu oturum açma hizmet URL'si**, hello hello Azure portal ' Kopyalanan **SAML SSO URL** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="655d8-183">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **SAML SSO URL** textbox.</span></span>
    
    <span data-ttu-id="655d8-184">c.</span><span class="sxs-lookup"><span data-stu-id="655d8-184">c.</span></span> <span data-ttu-id="655d8-185">Yapıştır **Sign-Out URL**, hello hello Azure portal ' Kopyalanan **uzak logoout URL** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="655d8-185">Paste **Sign-Out URL**, which you have copied from hello Azure portal into hello **Remote logoout URL** textbox.</span></span>
    
    <span data-ttu-id="655d8-186">d.</span><span class="sxs-lookup"><span data-stu-id="655d8-186">d.</span></span> <span data-ttu-id="655d8-187">İndirilen sertifikanızı kopyalama Merhaba içeriğine Not Defteri'nde açın ve hello yapıştırma **X.509 sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="655d8-187">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **X.509 Certificate** textbox.</span></span>
    
    <span data-ttu-id="655d8-188">e.</span><span class="sxs-lookup"><span data-stu-id="655d8-188">e.</span></span> <span data-ttu-id="655d8-189">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="655d8-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="655d8-190">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="655d8-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="655d8-191">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="655d8-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="655d8-192">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="655d8-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="655d8-193">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="655d8-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="655d8-194">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="655d8-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="655d8-196">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="655d8-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="655d8-197">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="655d8-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-userecho-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="655d8-199">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="655d8-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-userecho-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="655d8-201">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="655d8-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-userecho-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="655d8-203">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="655d8-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-userecho-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="655d8-205">a.</span><span class="sxs-lookup"><span data-stu-id="655d8-205">a.</span></span> <span data-ttu-id="655d8-206">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="655d8-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="655d8-207">b.</span><span class="sxs-lookup"><span data-stu-id="655d8-207">b.</span></span> <span data-ttu-id="655d8-208">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="655d8-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="655d8-209">c.</span><span class="sxs-lookup"><span data-stu-id="655d8-209">c.</span></span> <span data-ttu-id="655d8-210">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="655d8-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="655d8-211">d.</span><span class="sxs-lookup"><span data-stu-id="655d8-211">d.</span></span> <span data-ttu-id="655d8-212">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="655d8-212">Click **Create**.</span></span>
 
### <a name="creating-a-userecho-test-user"></a><span data-ttu-id="655d8-213">UserEcho test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="655d8-213">Creating a UserEcho test user</span></span>

<span data-ttu-id="655d8-214">Bu bölümde Hello amacı toocreate Britta Simon içinde UserEcho adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="655d8-214">hello objective of this section is toocreate a user called Britta Simon in UserEcho.</span></span>

<span data-ttu-id="655d8-215">**toocreate UserEcho içinde Britta Simon adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="655d8-215">**toocreate a user called Britta Simon in UserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="655d8-216">Yönetici olarak oturum açma tooyour UserEcho şirket sitesi.</span><span class="sxs-lookup"><span data-stu-id="655d8-216">Sign-on tooyour UserEcho company site as an administrator.</span></span>

2. <span data-ttu-id="655d8-217">Merhaba araç hello üstte, kullanıcı adı tooexpand hello menüsünü tıklatın ve ardından **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="655d8-217">In hello toolbar on hello top, click your user name tooexpand hello menu, and then click **Setup**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png)

3. <span data-ttu-id="655d8-219">Tıklatın **kullanıcılar**, tooexpand hello **kullanıcılar** bölümü.</span><span class="sxs-lookup"><span data-stu-id="655d8-219">Click **Users**, tooexpand hello **Users** section.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_10.png)

4. <span data-ttu-id="655d8-221">**Kullanıcılar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="655d8-221">Click **Users**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_11.png)

5. <span data-ttu-id="655d8-223">Tıklatın **yeni bir kullanıcı davet**.</span><span class="sxs-lookup"><span data-stu-id="655d8-223">Click **Invite a new user**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_12.png)

6. <span data-ttu-id="655d8-225">Merhaba üzerinde **yeni bir kullanıcı davet** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="655d8-225">On hello **Invite a new user** dialog, perform hello following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_13.png)

    <span data-ttu-id="655d8-227">a.</span><span class="sxs-lookup"><span data-stu-id="655d8-227">a.</span></span> <span data-ttu-id="655d8-228">Merhaba, **adı** metin kutusuna, hello kullanıcı Britta Simon gibi türünün adı.</span><span class="sxs-lookup"><span data-stu-id="655d8-228">In hello **Name** textbox, type name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="655d8-229">b.</span><span class="sxs-lookup"><span data-stu-id="655d8-229">b.</span></span>  <span data-ttu-id="655d8-230">Merhaba, **e-posta** türü hello kullanıcının e-posta adresi metin kutusuna, ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="655d8-230">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="655d8-231">c.</span><span class="sxs-lookup"><span data-stu-id="655d8-231">c.</span></span> <span data-ttu-id="655d8-232">Tıklatın **davet**.</span><span class="sxs-lookup"><span data-stu-id="655d8-232">Click **Invite**.</span></span>

<span data-ttu-id="655d8-233">Davetiye UserEcho kullanarak kendi toostart sağlayan tooBritta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="655d8-233">An invitation is sent tooBritta, which enables her toostart using UserEcho.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="655d8-234">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="655d8-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="655d8-235">Bu bölümde, erişim tooUserEcho vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="655d8-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUserEcho.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="655d8-237">**tooassign Britta Simon tooUserEcho hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="655d8-237">**tooassign Britta Simon tooUserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="655d8-238">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="655d8-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="655d8-240">Merhaba uygulamalar listesinde **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="655d8-240">In hello applications list, select **UserEcho**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_app.png) 

3. <span data-ttu-id="655d8-242">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="655d8-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="655d8-244">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="655d8-244">Click **Add** button.</span></span> <span data-ttu-id="655d8-245">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="655d8-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="655d8-247">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="655d8-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="655d8-248">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="655d8-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="655d8-249">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="655d8-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="655d8-250">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="655d8-250">Testing single sign-on</span></span>

<span data-ttu-id="655d8-251">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="655d8-251">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="655d8-252">Merhaba UserEcho hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour UserEcho uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="655d8-252">When you click hello UserEcho tile in hello Access Panel, you should get automatically signed-on tooyour UserEcho application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="655d8-253">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="655d8-253">Additional resources</span></span>

* [<span data-ttu-id="655d8-254">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="655d8-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="655d8-255">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="655d8-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_203.png

