---
title: "Öğretici: Azure Active Directory Tümleştirme ile Marketo | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Marketo arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="c0f74-103">Öğretici: Marketo Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="c0f74-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="c0f74-104">Bu öğreticide, bilgi nasıl toointegrate Marketo Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0f74-104">In this tutorial, you learn how toointegrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0f74-105">Marketo Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="c0f74-105">Integrating Marketo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c0f74-106">Erişim tooMarketo sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c0f74-106">You can control in Azure AD who has access tooMarketo</span></span>
- <span data-ttu-id="c0f74-107">Kullanıcıların tooautomatically get açan tooMarketo (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c0f74-107">You can enable your users tooautomatically get signed-on tooMarketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0f74-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="c0f74-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c0f74-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c0f74-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0f74-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c0f74-110">Prerequisites</span></span>

<span data-ttu-id="c0f74-111">tooconfigure Marketo ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c0f74-111">tooconfigure Azure AD integration with Marketo, you need hello following items:</span></span>

- <span data-ttu-id="c0f74-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="c0f74-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0f74-113">Bir Marketo çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="c0f74-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0f74-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="c0f74-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0f74-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="c0f74-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0f74-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c0f74-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0f74-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0f74-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0f74-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="c0f74-118">Scenario description</span></span>
<span data-ttu-id="c0f74-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="c0f74-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0f74-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="c0f74-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0f74-121">Marketo hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="c0f74-121">Adding Marketo from hello gallery</span></span>
2. <span data-ttu-id="c0f74-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c0f74-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-hello-gallery"></a><span data-ttu-id="c0f74-123">Marketo hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="c0f74-123">Adding Marketo from hello gallery</span></span>
<span data-ttu-id="c0f74-124">Azure AD'ye tooconfigure hello tümleştirme Marketo, tooadd Marketo hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0f74-124">tooconfigure hello integration of Marketo into Azure AD, you need tooadd Marketo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c0f74-125">**tooadd hello Galerisi, Marketo'dan hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c0f74-125">**tooadd Marketo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0f74-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c0f74-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c0f74-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="c0f74-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c0f74-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c0f74-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="c0f74-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c0f74-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="c0f74-133">Merhaba arama kutusuna yazın **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="c0f74-133">In hello search box, type **Marketo**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="c0f74-135">Merhaba Sonuçlar panelinde seçin **Marketo**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="c0f74-135">In hello results panel, select **Marketo**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0f74-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c0f74-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0f74-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Marketo ile test etme</span><span class="sxs-lookup"><span data-stu-id="c0f74-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c0f74-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Marketo içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0f74-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Marketo is tooa user in Azure AD.</span></span> <span data-ttu-id="c0f74-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Marketo hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0f74-140">In other words, a link relationship between an Azure AD user and hello related user in Marketo needs toobe established.</span></span>

<span data-ttu-id="c0f74-141">Marketo içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="c0f74-141">In Marketo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c0f74-142">tooconfigure ve Marketo ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c0f74-142">tooconfigure and test Azure AD single sign-on with Marketo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c0f74-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="c0f74-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c0f74-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="c0f74-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0f74-145">**[Marketo test kullanıcısı oluşturma](#creating-a-marketo-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Marketo içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="c0f74-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - toohave a counterpart of Britta Simon in Marketo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c0f74-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="c0f74-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0f74-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="c0f74-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0f74-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c0f74-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0f74-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Marketo uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c0f74-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="c0f74-150">**tooconfigure Azure AD çoklu oturum açma ile Marketo, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c0f74-150">**tooconfigure Azure AD single sign-on with Marketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0f74-151">Hello hello üzerinde Azure portal'ın **Marketo** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c0f74-151">In hello Azure portal, on hello **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="c0f74-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="c0f74-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="c0f74-155">Merhaba üzerinde **Marketo etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c0f74-155">On hello **Marketo Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="c0f74-157">a.</span><span class="sxs-lookup"><span data-stu-id="c0f74-157">a.</span></span> <span data-ttu-id="c0f74-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="c0f74-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="c0f74-159">b.</span><span class="sxs-lookup"><span data-stu-id="c0f74-159">b.</span></span> <span data-ttu-id="c0f74-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="c0f74-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c0f74-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="c0f74-161">These values are not real.</span></span> <span data-ttu-id="c0f74-162">Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c0f74-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="c0f74-163">Kişi [Marketo destek ekibi](http://investors.marketo.com/contactus.cfm) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="c0f74-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) tooget these values.</span></span>
 
4. <span data-ttu-id="c0f74-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c0f74-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="c0f74-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c0f74-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c0f74-168">Merhaba üzerinde **Marketo yapılandırma** 'yi tıklatın **yapılandırma Marketo** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="c0f74-168">On hello **Marketo Configuration** section, click **Configure Marketo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c0f74-169">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="c0f74-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="c0f74-171">tooget Munchkin kimliği, uygulamanızın içinde tooMarketo yönetici kimlik bilgilerinizi kullanarak oturum açın ve aşağıdaki işlemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c0f74-171">tooget Munchkin Id of your application, log in tooMarketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="c0f74-172">a.</span><span class="sxs-lookup"><span data-stu-id="c0f74-172">a.</span></span> <span data-ttu-id="c0f74-173">Yönetici kimlik bilgilerinizi kullanarak tooMarketo uygulamada oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c0f74-173">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="c0f74-174">b.</span><span class="sxs-lookup"><span data-stu-id="c0f74-174">b.</span></span> <span data-ttu-id="c0f74-175">Merhaba tıklatın **yönetici** hello üst gezinti bölmesindeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c0f74-175">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="c0f74-177">c.</span><span class="sxs-lookup"><span data-stu-id="c0f74-177">c.</span></span> <span data-ttu-id="c0f74-178">Toohello tümleştirme menü gidin ve hello tıklayın **Munchkin bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="c0f74-178">Navigate toohello Integration menu and click hello **Munchkin link**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="c0f74-180">d.</span><span class="sxs-lookup"><span data-stu-id="c0f74-180">d.</span></span> <span data-ttu-id="c0f74-181">Hello Munchkin hello ekranda gösterilen kodu kopyalayın ve yanıt URL'nizi hello Azure AD Yapılandırma Sihirbazı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="c0f74-181">Copy hello Munchkin Id shown on hello screen and complete your Reply URL in hello Azure AD configuration wizard.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="c0f74-183">Merhaba uygulaması tooconfigure hello SSO hello aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c0f74-183">tooconfigure hello SSO in hello application, follow hello below steps:</span></span>
   
    <span data-ttu-id="c0f74-184">a.</span><span class="sxs-lookup"><span data-stu-id="c0f74-184">a.</span></span> <span data-ttu-id="c0f74-185">Yönetici kimlik bilgilerinizi kullanarak tooMarketo uygulamada oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c0f74-185">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="c0f74-186">b.</span><span class="sxs-lookup"><span data-stu-id="c0f74-186">b.</span></span> <span data-ttu-id="c0f74-187">Merhaba tıklatın **yönetici** hello üst gezinti bölmesindeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c0f74-187">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="c0f74-189">c.</span><span class="sxs-lookup"><span data-stu-id="c0f74-189">c.</span></span> <span data-ttu-id="c0f74-190">Toohello tümleştirme menü gidin ve tıklayın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c0f74-190">Navigate toohello Integration menu and click **Single Sign On**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="c0f74-192">d.</span><span class="sxs-lookup"><span data-stu-id="c0f74-192">d.</span></span> <span data-ttu-id="c0f74-193">tooenable hello SAML ayarları tıklatın **Düzenle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c0f74-193">tooenable hello SAML Settings, click **Edit** button.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="c0f74-195">e.</span><span class="sxs-lookup"><span data-stu-id="c0f74-195">e.</span></span> <span data-ttu-id="c0f74-196">**Etkin** çoklu oturum açma ayarları.</span><span class="sxs-lookup"><span data-stu-id="c0f74-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="c0f74-197">f.</span><span class="sxs-lookup"><span data-stu-id="c0f74-197">f.</span></span> <span data-ttu-id="c0f74-198">Yapıştır hello **SAML varlık kimliği**, hello içinde **verenin kimliği** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="c0f74-198">Paste hello **SAML Entity ID**, in hello **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="c0f74-199">g.</span><span class="sxs-lookup"><span data-stu-id="c0f74-199">g.</span></span> <span data-ttu-id="c0f74-200">Merhaba, **varlık kimliği** metin kutusuna, hello URL olarak girin `http://saml.marketo.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="c0f74-200">In hello **Entity ID** textbox, enter hello URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="c0f74-201">h.</span><span class="sxs-lookup"><span data-stu-id="c0f74-201">h.</span></span> <span data-ttu-id="c0f74-202">Select hello kullanıcı kimliği konumu olarak **adı tanımlayıcı öğe**.</span><span class="sxs-lookup"><span data-stu-id="c0f74-202">Select hello User ID Location as **Name Identifier element**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="c0f74-204">Kullanıcı tanımlayıcısı UPN değeri sonra değişiklik hello değeri hello özniteliği sekmesinde değilse.</span><span class="sxs-lookup"><span data-stu-id="c0f74-204">If your User Identifier is not UPN value then change hello value in hello Attribute tab.</span></span>
   
    <span data-ttu-id="c0f74-205">ı.</span><span class="sxs-lookup"><span data-stu-id="c0f74-205">i.</span></span> <span data-ttu-id="c0f74-206">Azure AD Yapılandırma Sihirbazı'ndan indirilen hello sertifikasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c0f74-206">Upload hello certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="c0f74-207">**Kaydet** hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="c0f74-207">**Save** hello settings.</span></span>
   
    <span data-ttu-id="c0f74-208">j.</span><span class="sxs-lookup"><span data-stu-id="c0f74-208">j.</span></span> <span data-ttu-id="c0f74-209">Başlangıç sayfası yeniden yönlendirme ayarlarını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="c0f74-209">Edit hello Redirect Pages settings.</span></span>
   
    <span data-ttu-id="c0f74-210">k.</span><span class="sxs-lookup"><span data-stu-id="c0f74-210">k.</span></span> <span data-ttu-id="c0f74-211">Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** hello içinde **oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="c0f74-211">Paste hello **SAML Single Sign-On Service URL** in hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="c0f74-212">l.</span><span class="sxs-lookup"><span data-stu-id="c0f74-212">l.</span></span> <span data-ttu-id="c0f74-213">Yapıştır hello **Sign-Out URL** hello içinde **oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="c0f74-213">Paste hello **Sign-Out URL** in hello **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="c0f74-214">m.</span><span class="sxs-lookup"><span data-stu-id="c0f74-214">m.</span></span> <span data-ttu-id="c0f74-215">Merhaba, **hata URL**, kopyalama, **Marketo örnek URL'si** tıklatıp **kaydetmek** düğmesini toosave ayarları.</span><span class="sxs-lookup"><span data-stu-id="c0f74-215">In hello **Error URL**, copy your **Marketo instance URL** and click **Save** button toosave settings.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="c0f74-217">tooenable hello SSO kullanıcılar için aşağıdaki eylemler tamamlandı hello:</span><span class="sxs-lookup"><span data-stu-id="c0f74-217">tooenable hello SSO for users, complete hello following actions:</span></span>
   
    <span data-ttu-id="c0f74-218">a.</span><span class="sxs-lookup"><span data-stu-id="c0f74-218">a.</span></span> <span data-ttu-id="c0f74-219">Yönetici kimlik bilgilerinizi kullanarak tooMarketo uygulamada oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c0f74-219">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="c0f74-220">b.</span><span class="sxs-lookup"><span data-stu-id="c0f74-220">b.</span></span> <span data-ttu-id="c0f74-221">Merhaba tıklatın **yönetici** hello üst gezinti bölmesindeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c0f74-221">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="c0f74-223">c.</span><span class="sxs-lookup"><span data-stu-id="c0f74-223">c.</span></span> <span data-ttu-id="c0f74-224">Toohello gidin **güvenlik** menüsüne ve ardından **oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="c0f74-224">Navigate toohello **Security** menu and click **Login Settings**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="c0f74-226">d.</span><span class="sxs-lookup"><span data-stu-id="c0f74-226">d.</span></span> <span data-ttu-id="c0f74-227">Merhaba denetleyin **gerektiren SSO** seçeneği ve **kaydetmek** hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="c0f74-227">Check hello **Require SSO** option and **Save** hello settings.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="c0f74-229">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="c0f74-229">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c0f74-230">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="c0f74-230">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c0f74-231">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c0f74-231">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0f74-232">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0f74-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0f74-233">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="c0f74-233">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="c0f74-235">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c0f74-235">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0f74-236">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c0f74-236">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0f74-238">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c0f74-238">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0f74-240">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="c0f74-240">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0f74-242">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c0f74-242">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0f74-244">a.</span><span class="sxs-lookup"><span data-stu-id="c0f74-244">a.</span></span> <span data-ttu-id="c0f74-245">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c0f74-245">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0f74-246">b.</span><span class="sxs-lookup"><span data-stu-id="c0f74-246">b.</span></span> <span data-ttu-id="c0f74-247">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="c0f74-247">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c0f74-248">c.</span><span class="sxs-lookup"><span data-stu-id="c0f74-248">c.</span></span> <span data-ttu-id="c0f74-249">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="c0f74-249">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c0f74-250">d.</span><span class="sxs-lookup"><span data-stu-id="c0f74-250">d.</span></span> <span data-ttu-id="c0f74-251">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c0f74-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="c0f74-252">Marketo test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0f74-252">Creating a Marketo test user</span></span>

<span data-ttu-id="c0f74-253">Bu bölümde, Marketo içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c0f74-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="c0f74-254">Bu adımları toocreate kullanıcı Marketo platform olarak izleyin.</span><span class="sxs-lookup"><span data-stu-id="c0f74-254">follow these steps toocreate a user in Marketo platform.</span></span>

1. <span data-ttu-id="c0f74-255">Yönetici kimlik bilgilerinizi kullanarak tooMarketo uygulamada oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c0f74-255">Log in tooMarketo app using admin credentials.</span></span>

2. <span data-ttu-id="c0f74-256">Merhaba tıklatın **yönetici** hello üst gezinti bölmesindeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c0f74-256">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="c0f74-258">Toohello gidin **güvenlik** menüsüne ve ardından **kullanıcıları ve rolleri**</span><span class="sxs-lookup"><span data-stu-id="c0f74-258">Navigate toohello **Security** menu and click **Users & Roles**</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="c0f74-260">Merhaba tıklatın **yeni kullanıcı davet** hello kullanıcılar sekmesinde bağlantı</span><span class="sxs-lookup"><span data-stu-id="c0f74-260">Click hello **Invite New User** link on hello Users tab</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="c0f74-262">Merhaba yeni kullanıcı davet Sihirbazı dolgu hello bilgisinden</span><span class="sxs-lookup"><span data-stu-id="c0f74-262">In hello Invite New User wizard fill hello following information</span></span>
   
    <span data-ttu-id="c0f74-263">a.</span><span class="sxs-lookup"><span data-stu-id="c0f74-263">a.</span></span> <span data-ttu-id="c0f74-264">Merhaba kullanıcı girin **e-posta** hello metin kutusuna adresi</span><span class="sxs-lookup"><span data-stu-id="c0f74-264">Enter hello user **Email** address in hello textbox</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="c0f74-266">b.</span><span class="sxs-lookup"><span data-stu-id="c0f74-266">b.</span></span> <span data-ttu-id="c0f74-267">Merhaba girin **ad** hello metin kutusuna</span><span class="sxs-lookup"><span data-stu-id="c0f74-267">Enter hello **First Name** in hello textbox</span></span>
   
    <span data-ttu-id="c0f74-268">c.</span><span class="sxs-lookup"><span data-stu-id="c0f74-268">c.</span></span> <span data-ttu-id="c0f74-269">Merhaba girin **Soyadı** hello metin kutusuna</span><span class="sxs-lookup"><span data-stu-id="c0f74-269">Enter hello **Last Name**  in hello textbox</span></span>
   
    <span data-ttu-id="c0f74-270">d.</span><span class="sxs-lookup"><span data-stu-id="c0f74-270">d.</span></span> <span data-ttu-id="c0f74-271">**İleri**’ye tıklayın</span><span class="sxs-lookup"><span data-stu-id="c0f74-271">Click **Next**</span></span>

6. <span data-ttu-id="c0f74-272">Merhaba, **izinleri** sekmesi, select hello **userRoles** tıklatıp **sonraki**</span><span class="sxs-lookup"><span data-stu-id="c0f74-272">In hello **Permissions** tab, select hello **userRoles** and click **Next**</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="c0f74-274">Merhaba tıklatın **Gönder** düğmesini toosend hello kullanıcı davet</span><span class="sxs-lookup"><span data-stu-id="c0f74-274">Click hello **Send** button toosend hello user invitation</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="c0f74-276">Kullanıcı hello e-posta bildirimi alır ve bağlantı ve hello parola tooactivate hello hesap Değiştir tooclick hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c0f74-276">User receives hello email notification and has tooclick hello link and change hello password tooactivate hello account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c0f74-277">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="c0f74-277">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c0f74-278">Bu bölümde, erişim tooMarketo vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c0f74-278">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMarketo.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="c0f74-280">**tooassign Britta Simon tooMarketo hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c0f74-280">**tooassign Britta Simon tooMarketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0f74-281">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c0f74-281">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="c0f74-283">Merhaba uygulamalar listesinde **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="c0f74-283">In hello applications list, select **Marketo**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="c0f74-285">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c0f74-285">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="c0f74-287">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c0f74-287">Click **Add** button.</span></span> <span data-ttu-id="c0f74-288">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c0f74-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="c0f74-290">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="c0f74-290">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c0f74-291">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c0f74-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0f74-292">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c0f74-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0f74-293">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="c0f74-293">Testing single sign-on</span></span>

<span data-ttu-id="c0f74-294">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="c0f74-294">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c0f74-295">Merhaba Marketo hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Marketo uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0f74-295">When you click hello Marketo tile in hello Access Panel, you should get automatically signed-on tooyour Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c0f74-296">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c0f74-296">Additional resources</span></span>

* [<span data-ttu-id="c0f74-297">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="c0f74-297">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0f74-298">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="c0f74-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

