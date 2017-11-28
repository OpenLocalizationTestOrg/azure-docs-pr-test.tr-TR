---
title: "Öğretici: Azure Active Directory Tümleştirme ile 23 Video | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile 23 Video arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e73dd1d-3995-4a73-b9cf-1b2318d49cb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: 3430e4db3cd1114db62233e6699618071a3646ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-23-video"></a><span data-ttu-id="d7635-103">Öğretici: Azure Active Directory Tümleştirme ile 23 Video</span><span class="sxs-lookup"><span data-stu-id="d7635-103">Tutorial: Azure Active Directory integration with 23 Video</span></span>

<span data-ttu-id="d7635-104">Bu öğreticide, bilgi nasıl toointegrate 23 Video Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d7635-104">In this tutorial, you learn how toointegrate 23 Video with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d7635-105">23 tümleştirme Azure AD ile Video ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="d7635-105">Integrating 23 Video with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d7635-106">Erişimi olan Azure AD'de denetim too23 Video</span><span class="sxs-lookup"><span data-stu-id="d7635-106">You can control in Azure AD who has access too23 Video</span></span>
- <span data-ttu-id="d7635-107">Kullanıcılarınızın tooautomatically alma etkinleştirebilirsiniz too23 Video (çoklu oturum açma) ile Azure AD hesaplarına açan</span><span class="sxs-lookup"><span data-stu-id="d7635-107">You can enable your users tooautomatically get signed-on too23 Video (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d7635-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="d7635-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d7635-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d7635-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7635-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d7635-110">Prerequisites</span></span>

<span data-ttu-id="d7635-111">tooconfigure 23 Video ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d7635-111">tooconfigure Azure AD integration with 23 Video, you need hello following items:</span></span>

- <span data-ttu-id="d7635-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="d7635-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d7635-113">Abonelik bir 23 Video çoklu oturum açma etkin</span><span class="sxs-lookup"><span data-stu-id="d7635-113">A 23 Video single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d7635-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="d7635-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d7635-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="d7635-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d7635-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="d7635-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d7635-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d7635-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d7635-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="d7635-118">Scenario description</span></span>
<span data-ttu-id="d7635-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="d7635-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d7635-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="d7635-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d7635-121">Merhaba Galerisi'nden 23 Video ekleme</span><span class="sxs-lookup"><span data-stu-id="d7635-121">Adding 23 Video from hello gallery</span></span>
2. <span data-ttu-id="d7635-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d7635-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-23-video-from-hello-gallery"></a><span data-ttu-id="d7635-123">Merhaba Galerisi'nden 23 Video ekleme</span><span class="sxs-lookup"><span data-stu-id="d7635-123">Adding 23 Video from hello gallery</span></span>
<span data-ttu-id="d7635-124">Azure AD'ye tooconfigure hello tümleştirme 23 videonun tooadd 23 ihtiyacınız hello galeri tooyour yönetilen SaaS uygulamaları listesinden görüntü.</span><span class="sxs-lookup"><span data-stu-id="d7635-124">tooconfigure hello integration of 23 Video into Azure AD, you need tooadd 23 Video from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d7635-125">**Video hello galerisinden tooadd 23 gerçekleştirmek hello adımları izleyin:**</span><span class="sxs-lookup"><span data-stu-id="d7635-125">**tooadd 23 Video from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7635-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d7635-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d7635-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="d7635-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d7635-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d7635-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="d7635-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d7635-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="d7635-133">Merhaba arama kutusuna yazın **23 Video**.</span><span class="sxs-lookup"><span data-stu-id="d7635-133">In hello search box, type **23 Video**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-23video-tutorial/tutorial_23video_search.png)

5. <span data-ttu-id="d7635-135">Merhaba Sonuçlar panelinde seçin **23 Video**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="d7635-135">In hello results panel, select **23 Video**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-23video-tutorial/tutorial_23video_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d7635-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d7635-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d7635-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı 23 Video ile test etme</span><span class="sxs-lookup"><span data-stu-id="d7635-138">In this section, you configure and test Azure AD single sign-on with 23 Video based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d7635-139">Tek toowork'ın oturum açma hangi hello karşılık gelen 23 videoda tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7635-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 23 Video is tooa user in Azure AD.</span></span> <span data-ttu-id="d7635-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı 23 arasında bir bağlantı ilişkisi Video kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7635-140">In other words, a link relationship between an Azure AD user and hello related user in 23 Video needs toobe established.</span></span>

<span data-ttu-id="d7635-141">23 videoda hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="d7635-141">In 23 Video, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d7635-142">tooconfigure ve 23 Video ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d7635-142">tooconfigure and test Azure AD single sign-on with 23 Video, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d7635-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="d7635-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d7635-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="d7635-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d7635-145">**[23 Video test kullanıcısı oluşturma](#creating-a-23-video-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir 23 videoda, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="d7635-145">**[Creating a 23 Video test user](#creating-a-23-video-test-user)** - toohave a counterpart of Britta Simon in 23 Video that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d7635-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="d7635-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d7635-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="d7635-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d7635-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d7635-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d7635-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma 23 Video uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d7635-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 23 Video application.</span></span>

<span data-ttu-id="d7635-150">**tooconfigure Azure AD çoklu oturum açma 23 video hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d7635-150">**tooconfigure Azure AD single sign-on with 23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7635-151">Hello hello üzerinde Azure portal'ın **23 Video** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="d7635-151">In hello Azure portal, on hello **23 Video** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="d7635-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="d7635-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-23video-tutorial/tutorial_23video_samlbase.png)

3. <span data-ttu-id="d7635-155">Merhaba üzerinde **23 Video etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d7635-155">On hello **23 Video Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-23video-tutorial/tutorial_23video_url.png)

    <span data-ttu-id="d7635-157">a.</span><span class="sxs-lookup"><span data-stu-id="d7635-157">a.</span></span> <span data-ttu-id="d7635-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.23video.com`</span><span class="sxs-lookup"><span data-stu-id="d7635-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.23video.com`</span></span>

    <span data-ttu-id="d7635-159">b.</span><span class="sxs-lookup"><span data-stu-id="d7635-159">b.</span></span> <span data-ttu-id="d7635-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://www.23video.com/saml/trust/<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="d7635-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.23video.com/saml/trust/<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d7635-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="d7635-161">These values are not real.</span></span> <span data-ttu-id="d7635-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="d7635-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d7635-163">Kişi [23 Video istemci destek ekibi](mailto:support@23company.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="d7635-163">Contact [23 Video Client support team](mailto:support@23company.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="d7635-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d7635-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-23video-tutorial/tutorial_23video_certificate.png) 

5. <span data-ttu-id="d7635-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d7635-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-23video-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d7635-168">Merhaba üzerinde **23 Video yapılandırma** 'yi tıklatın **yapılandırma 23 Video** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="d7635-168">On hello **23 Video Configuration** section, click **Configure 23 Video** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d7635-169">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="d7635-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-23video-tutorial/tutorial_23video_configure.png) 

7. <span data-ttu-id="d7635-171">tooconfigure çoklu oturum açma üzerinde **23 Video** yan, indirilen toosend hello ihtiyacınız **sertifika (Base64)**, **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si**çok[23 Video destek ekibi](mailto:support@23company.com).</span><span class="sxs-lookup"><span data-stu-id="d7635-171">tooconfigure single sign-on on **23 Video** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[23 Video support team](mailto:support@23company.com).</span></span> 


> [!TIP]
> <span data-ttu-id="d7635-172">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="d7635-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d7635-173">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="d7635-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d7635-174">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d7635-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d7635-175">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7635-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="d7635-176">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="d7635-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="d7635-178">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d7635-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7635-179">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d7635-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-23video-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d7635-181">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="d7635-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-23video-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d7635-183">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="d7635-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-23video-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d7635-185">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d7635-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-23video-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d7635-187">a.</span><span class="sxs-lookup"><span data-stu-id="d7635-187">a.</span></span> <span data-ttu-id="d7635-188">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d7635-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d7635-189">b.</span><span class="sxs-lookup"><span data-stu-id="d7635-189">b.</span></span> <span data-ttu-id="d7635-190">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="d7635-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d7635-191">c.</span><span class="sxs-lookup"><span data-stu-id="d7635-191">c.</span></span> <span data-ttu-id="d7635-192">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="d7635-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d7635-193">d.</span><span class="sxs-lookup"><span data-stu-id="d7635-193">d.</span></span> <span data-ttu-id="d7635-194">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d7635-194">Click **Create**.</span></span>
 
### <a name="creating-a-23-video-test-user"></a><span data-ttu-id="d7635-195">23 Video test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7635-195">Creating a 23 Video test user</span></span>

<span data-ttu-id="d7635-196">Bu bölümde Hello amacı toocreate 23 videoda Britta Simon adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="d7635-196">hello objective of this section is toocreate a user called Britta Simon in 23 Video.</span></span>

<span data-ttu-id="d7635-197">**toocreate Britta Simon 23 videoda adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d7635-197">**toocreate a user called Britta Simon in 23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7635-198">Üzerinde tooyour 23 Video şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d7635-198">Sign on tooyour 23 Video company site as administrator.</span></span>

2. <span data-ttu-id="d7635-199">Çok Git**ayarları**.</span><span class="sxs-lookup"><span data-stu-id="d7635-199">Go too**Settings**.</span></span>
 
3. <span data-ttu-id="d7635-200">İçinde **kullanıcılar** 'yi tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="d7635-200">In **Users** section, click **Configure**.</span></span>
   
    ![Kullanıcı atama][400]

4. <span data-ttu-id="d7635-202">Tıklatın **yeni bir kullanıcı eklemek**.</span><span class="sxs-lookup"><span data-stu-id="d7635-202">Click **Add a new user**.</span></span> 
   
    ![Kullanıcı atama][401]

5. <span data-ttu-id="d7635-204">Merhaba, **davet toojoin bu site** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d7635-204">In hello **Invite someone toojoin this site** section, perform hello following steps:</span></span>
   
    ![Kullanıcı atama][402]

    <span data-ttu-id="d7635-206">a.</span><span class="sxs-lookup"><span data-stu-id="d7635-206">a.</span></span> <span data-ttu-id="d7635-207">Merhaba, **e-posta adresleri** metin kutusuna, Azure AD'de Britta Simon'ın e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="d7635-207">In hello **E-mail addresses** textbox, type Britta Simon's email address in Azure AD.</span></span>  
 
    <span data-ttu-id="d7635-208">b.</span><span class="sxs-lookup"><span data-stu-id="d7635-208">b.</span></span> <span data-ttu-id="d7635-209">Tıklatın **hello Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d7635-209">Click **Add hello user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d7635-210">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="d7635-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d7635-211">Bu bölümde, Britta Simon etkinleştirme verme tarafından toouse Azure çoklu oturum açma too23 Video erişim.</span><span class="sxs-lookup"><span data-stu-id="d7635-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too23 Video.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="d7635-213">**tooassign Britta Simon too23 Video hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d7635-213">**tooassign Britta Simon too23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7635-214">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d7635-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="d7635-216">Merhaba uygulamalar listesinde **23 Video**.</span><span class="sxs-lookup"><span data-stu-id="d7635-216">In hello applications list, select **23 Video**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-23video-tutorial/tutorial_23video_app.png) 

3. <span data-ttu-id="d7635-218">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d7635-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="d7635-220">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d7635-220">Click **Add** button.</span></span> <span data-ttu-id="d7635-221">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d7635-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="d7635-223">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="d7635-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d7635-224">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d7635-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d7635-225">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d7635-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d7635-226">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="d7635-226">Testing single sign-on</span></span>

<span data-ttu-id="d7635-227">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="d7635-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="d7635-228">Merhaba 23 Video hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma 23 tooyour Video uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7635-228">When you click hello 23 Video tile in hello Access Panel, you should get automatically signed-on tooyour 23 Video application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d7635-229">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d7635-229">Additional resources</span></span>

* [<span data-ttu-id="d7635-230">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="d7635-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d7635-231">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="d7635-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-23video-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-23video-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-23video-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-23video-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-23video-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-23video-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-23video-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-23video-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-23video-tutorial/tutorial_general_203.png

[400]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_10.png
[401]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_11.png
[402]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_12.png
