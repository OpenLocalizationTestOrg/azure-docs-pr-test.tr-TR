---
title: "Öğretici: Azure Active Directory Tümleştirme ile 123ContactForm | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile 123ContactForm arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 931255887845edd1aa7f53b9051a82a2f898e055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a><span data-ttu-id="79590-103">Öğretici: Azure Active Directory Tümleştirme 123ContactForm ile</span><span class="sxs-lookup"><span data-stu-id="79590-103">Tutorial: Azure Active Directory integration with 123ContactForm</span></span>

<span data-ttu-id="79590-104">Bu öğreticide, bilgi nasıl toointegrate 123ContactForm Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="79590-104">In this tutorial, you learn how toointegrate 123ContactForm with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79590-105">123ContactForm Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="79590-105">Integrating 123ContactForm with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="79590-106">Erişim too123ContactForm sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="79590-106">You can control in Azure AD who has access too123ContactForm</span></span>
- <span data-ttu-id="79590-107">Oturum açma, kullanıcıların tooautomatically get too123ContactForm etkinleştirebilirsiniz (çoklu oturum açma) Azure AD hesaplarına sahip</span><span class="sxs-lookup"><span data-stu-id="79590-107">You can enable your users tooautomatically get signed-on too123ContactForm (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79590-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="79590-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="79590-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="79590-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79590-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="79590-110">Prerequisites</span></span>

<span data-ttu-id="79590-111">tooconfigure 123ContactForm ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="79590-111">tooconfigure Azure AD integration with 123ContactForm, you need hello following items:</span></span>

- <span data-ttu-id="79590-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="79590-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79590-113">Bir 123ContactForm çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="79590-113">A 123ContactForm single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79590-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="79590-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79590-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="79590-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79590-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="79590-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79590-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79590-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79590-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="79590-118">Scenario description</span></span>
<span data-ttu-id="79590-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="79590-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79590-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="79590-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79590-121">Merhaba Galerisi'nden 123ContactForm ekleme</span><span class="sxs-lookup"><span data-stu-id="79590-121">Adding 123ContactForm from hello gallery</span></span>
2. <span data-ttu-id="79590-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="79590-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-123contactform-from-hello-gallery"></a><span data-ttu-id="79590-123">Merhaba Galerisi'nden 123ContactForm ekleme</span><span class="sxs-lookup"><span data-stu-id="79590-123">Adding 123ContactForm from hello gallery</span></span>
<span data-ttu-id="79590-124">Azure AD'ye tooconfigure hello tümleştirme 123ContactForm, tooadd 123ContactForm hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="79590-124">tooconfigure hello integration of 123ContactForm into Azure AD, you need tooadd 123ContactForm from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="79590-125">**Merhaba galerisinden tooadd 123ContactForm hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="79590-125">**tooadd 123ContactForm from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="79590-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="79590-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="79590-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="79590-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="79590-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="79590-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="79590-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="79590-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="79590-133">Merhaba arama kutusuna yazın **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="79590-133">In hello search box, type **123ContactForm**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. <span data-ttu-id="79590-135">Merhaba Sonuçlar panelinde seçin **123ContactForm**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="79590-135">In hello results panel, select **123ContactForm**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="79590-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="79590-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="79590-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı 123ContactForm ile test etme</span><span class="sxs-lookup"><span data-stu-id="79590-138">In this section, you configure and test Azure AD single sign-on with 123ContactForm based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="79590-139">Tek toowork'ın oturum açma hangi hello karşılık gelen 123ContactForm içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="79590-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 123ContactForm is tooa user in Azure AD.</span></span> <span data-ttu-id="79590-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı 123ContactForm hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="79590-140">In other words, a link relationship between an Azure AD user and hello related user in 123ContactForm needs toobe established.</span></span>

<span data-ttu-id="79590-141">Merhaba hello değeri 123ContactForm içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="79590-141">In 123ContactForm, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="79590-142">tooconfigure ve 123ContactForm ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="79590-142">tooconfigure and test Azure AD single sign-on with 123ContactForm, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="79590-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="79590-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="79590-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="79590-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79590-145">**[123ContactForm test kullanıcısı oluşturma](#creating-a-123contactform-test-user)**  -toohave bir Britta Simon karşılık gelen kullanıcı bağlantılı toohello Azure AD gösterimidir 123ContactForm içinde.</span><span class="sxs-lookup"><span data-stu-id="79590-145">**[Creating a 123ContactForm test user](#creating-a-123contactform-test-user)** - toohave a counterpart of Britta Simon in 123ContactForm that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="79590-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="79590-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79590-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="79590-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="79590-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="79590-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="79590-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma 123ContactForm uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="79590-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 123ContactForm application.</span></span>

<span data-ttu-id="79590-150">**tooconfigure Azure AD çoklu oturum açma ile 123ContactForm, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="79590-150">**tooconfigure Azure AD single sign-on with 123ContactForm, perform hello following steps:**</span></span>

1. <span data-ttu-id="79590-151">Hello hello üzerinde Azure portal'ın **123ContactForm** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="79590-151">In hello Azure portal, on hello **123ContactForm** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="79590-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="79590-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. <span data-ttu-id="79590-155">Merhaba üzerinde **123ContactForm etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP başlatılan modu**, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79590-155">On hello **123ContactForm Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-123contactform-tutorial/url1.png)

    <span data-ttu-id="79590-157">a.</span><span class="sxs-lookup"><span data-stu-id="79590-157">a.</span></span> <span data-ttu-id="79590-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span><span class="sxs-lookup"><span data-stu-id="79590-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span></span>

    <span data-ttu-id="79590-159">b.</span><span class="sxs-lookup"><span data-stu-id="79590-159">b.</span></span> <span data-ttu-id="79590-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span><span class="sxs-lookup"><span data-stu-id="79590-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span></span>

4. <span data-ttu-id="79590-161">Tooconfigure hello uygulamada istiyorsanız **SP tarafından başlatılan modu**, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79590-161">If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-123contactform-tutorial/url2.png)

    <span data-ttu-id="79590-163">a.</span><span class="sxs-lookup"><span data-stu-id="79590-163">a.</span></span> <span data-ttu-id="79590-164">Merhaba tıklatın **Göster Gelişmiş URL ayarları** seçeneği</span><span class="sxs-lookup"><span data-stu-id="79590-164">Click hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="79590-165">b.</span><span class="sxs-lookup"><span data-stu-id="79590-165">b.</span></span> <span data-ttu-id="79590-166">Merhaba, **oturum üzerinde URL'si** metin kutusuna, URL'yi yazın:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span><span class="sxs-lookup"><span data-stu-id="79590-166">In hello **Sign On URL** textbox, type a URL as: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="79590-167">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="79590-167">These values are not real.</span></span> <span data-ttu-id="79590-168">Bu değer gerçek URL'leri ve hello öğreticinin ilerleyen bölümlerinde açıklanan tanımlayıcısı tooupdate gerekir.</span><span class="sxs-lookup"><span data-stu-id="79590-168">You'll need tooupdate these value from actual URLs and Identifier which is explained later in hello tutorial.</span></span>
    
5. <span data-ttu-id="79590-169">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="79590-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. <span data-ttu-id="79590-171">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="79590-171">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="79590-173">tooconfigure çoklu oturum açma üzerinde **123ContactForm** tarafı, çok Git[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79590-173">tooconfigure single sign-on on **123ContactForm** side, go too[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) and perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    <span data-ttu-id="79590-175">a.</span><span class="sxs-lookup"><span data-stu-id="79590-175">a.</span></span> <span data-ttu-id="79590-176">Merhaba, **e-posta** metin kutusuna, hello kullanıcı yani, türü hello e-posta</span><span class="sxs-lookup"><span data-stu-id="79590-176">In hello **Email** textbox, type hello email of hello user i.e</span></span> <span data-ttu-id="79590-177">**BrittaSimon@Contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="79590-177">**BrittaSimon@Contoso.com**.</span></span>

    <span data-ttu-id="79590-178">b.</span><span class="sxs-lookup"><span data-stu-id="79590-178">b.</span></span> <span data-ttu-id="79590-179">Tıklatın **karşıya** ve hello Azure Portalı'ndan indirilen meta veri XML dosyasını bulun.</span><span class="sxs-lookup"><span data-stu-id="79590-179">Click **Upload** and browse hello Metadata XML file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="79590-180">c.</span><span class="sxs-lookup"><span data-stu-id="79590-180">c.</span></span> <span data-ttu-id="79590-181">Tıklatın **gönderme FORM**.</span><span class="sxs-lookup"><span data-stu-id="79590-181">Click **SUBMIT FORM**.</span></span>

8. <span data-ttu-id="79590-182">Merhaba üzerinde **Microsoft Azure AD çoklu oturum açma - uygulama ayarlarını yapılandır** hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79590-182">On hello **Microsoft Azure AD - Single sign-on - Configure App Settings** perform hello following steps:</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-123contactform-tutorial/url3.png)

    <span data-ttu-id="79590-184">a.</span><span class="sxs-lookup"><span data-stu-id="79590-184">a.</span></span> <span data-ttu-id="79590-185">Tooconfigure hello uygulamada istiyorsanız **IDP başlatılan modu**, kopya hello **TANIMLAYICISI** değer Örneğiniz için ve yapıştırın **tanımlayıcısı** metin kutusuna **123ContactForm etki alanı ve URL'leri** Azure Portal'daki bölümü.</span><span class="sxs-lookup"><span data-stu-id="79590-185">If you wish tooconfigure hello application in **IDP initiated mode**, copy hello **IDENTIFIER** value for your instance and paste it in **Identifier** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="79590-186">b.</span><span class="sxs-lookup"><span data-stu-id="79590-186">b.</span></span> <span data-ttu-id="79590-187">Tooconfigure hello uygulamada istiyorsanız **IDP başlatılan modu**, kopya hello **yanıt URL'si** değer Örneğiniz için ve yapıştırın **yanıt URL'si** metin kutusuna **123ContactForm etki alanı ve URL'leri** Azure Portal'daki bölümü.</span><span class="sxs-lookup"><span data-stu-id="79590-187">If you wish tooconfigure hello application in **IDP initiated mode**, copy hello **REPLY URL** value for your instance and paste it in **Reply URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="79590-188">c.</span><span class="sxs-lookup"><span data-stu-id="79590-188">c.</span></span> <span data-ttu-id="79590-189">Tooconfigure hello uygulamada istiyorsanız **SP tarafından başlatılan modu**, kopya hello **oturum ON URL'si** değer Örneğiniz için ve yapıştırın **oturum üzerinde URL'si** metin kutusuna **123ContactForm etki alanı ve URL'leri** Azure Portal'daki bölümü.</span><span class="sxs-lookup"><span data-stu-id="79590-189">If you wish tooconfigure hello application in **SP initiated mode**, copy hello **SIGN ON URL** value for your instance and paste it in **Sign On URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="79590-190">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="79590-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="79590-191">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="79590-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="79590-192">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="79590-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="79590-193">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="79590-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="79590-194">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="79590-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="79590-196">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="79590-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="79590-197">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="79590-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="79590-199">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="79590-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="79590-201">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="79590-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="79590-203">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79590-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79590-205">a.</span><span class="sxs-lookup"><span data-stu-id="79590-205">a.</span></span> <span data-ttu-id="79590-206">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="79590-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79590-207">b.</span><span class="sxs-lookup"><span data-stu-id="79590-207">b.</span></span> <span data-ttu-id="79590-208">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="79590-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="79590-209">c.</span><span class="sxs-lookup"><span data-stu-id="79590-209">c.</span></span> <span data-ttu-id="79590-210">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="79590-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="79590-211">d.</span><span class="sxs-lookup"><span data-stu-id="79590-211">d.</span></span> <span data-ttu-id="79590-212">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79590-212">Click **Create**.</span></span>
 
### <a name="creating-a-123contactform-test-user"></a><span data-ttu-id="79590-213">123ContactForm test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="79590-213">Creating a 123ContactForm test user</span></span>

<span data-ttu-id="79590-214">Uygulama, süresi kullanıcı sağlama ve kimlik doğrulama kullanıcılar hello uygulamada otomatik olarak oluşturulacak sonra hemen destekler.</span><span class="sxs-lookup"><span data-stu-id="79590-214">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="79590-215">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="79590-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="79590-216">Bu bölümde, erişim too123ContactForm vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="79590-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too123ContactForm.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="79590-218">**tooassign Britta Simon too123ContactForm hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="79590-218">**tooassign Britta Simon too123ContactForm, perform hello following steps:**</span></span>

1. <span data-ttu-id="79590-219">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="79590-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="79590-221">Merhaba uygulamalar listesinde **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="79590-221">In hello applications list, select **123ContactForm**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. <span data-ttu-id="79590-223">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="79590-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="79590-225">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="79590-225">Click **Add** button.</span></span> <span data-ttu-id="79590-226">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="79590-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="79590-228">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="79590-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="79590-229">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="79590-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79590-230">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="79590-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="79590-231">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="79590-231">Testing single sign-on</span></span>

<span data-ttu-id="79590-232">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="79590-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="79590-233">Merhaba 123ContactForm hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour 123ContactForm uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="79590-233">When you click hello 123ContactForm tile in hello Access Panel, you should get automatically signed-on tooyour 123ContactForm application.</span></span>
<span data-ttu-id="79590-234">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="79590-234">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="79590-235">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="79590-235">Additional resources</span></span>

* [<span data-ttu-id="79590-236">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="79590-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79590-237">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="79590-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png

