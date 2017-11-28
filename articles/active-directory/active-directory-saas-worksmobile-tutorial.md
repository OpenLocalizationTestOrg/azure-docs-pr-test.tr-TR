---
title: "Öğretici: Azure Active Directory Tümleştirme ile WORKS mobil | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile WORKS mobil arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 80192218a2e99a921834bb53e708d5e4fab413f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-works-mobile"></a><span data-ttu-id="67e64-103">Öğretici: Azure Active Directory Tümleştirme ile WORKS mobil</span><span class="sxs-lookup"><span data-stu-id="67e64-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span></span>

<span data-ttu-id="67e64-104">Bu öğreticide, toointegrate nasıl ÇALIŞTIĞINI öğrenin mobil Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="67e64-104">In this tutorial, you learn how toointegrate WORKS MOBILE with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="67e64-105">WORKS mobil Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="67e64-105">Integrating WORKS MOBILE with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="67e64-106">Mobil erişim tooWORKS sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="67e64-106">You can control in Azure AD who has access tooWORKS MOBILE</span></span>
- <span data-ttu-id="67e64-107">Kullanıcıların tooautomatically get açan tooWORKS mobil (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="67e64-107">You can enable your users tooautomatically get signed-on tooWORKS MOBILE (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="67e64-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="67e64-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="67e64-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="67e64-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67e64-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="67e64-110">Prerequisites</span></span>

<span data-ttu-id="67e64-111">tooconfigure WORKS MOBILE ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="67e64-111">tooconfigure Azure AD integration with WORKS MOBILE, you need hello following items:</span></span>

- <span data-ttu-id="67e64-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="67e64-112">An Azure AD subscription</span></span>
- <span data-ttu-id="67e64-113">Bir WORKS mobil çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="67e64-113">A WORKS MOBILE single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="67e64-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="67e64-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="67e64-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="67e64-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="67e64-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="67e64-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="67e64-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="67e64-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="67e64-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="67e64-118">Scenario description</span></span>
<span data-ttu-id="67e64-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="67e64-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="67e64-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="67e64-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="67e64-121">Merhaba Galerisi'nden WORKS mobil ekleme</span><span class="sxs-lookup"><span data-stu-id="67e64-121">Adding WORKS MOBILE from hello gallery</span></span>
2. <span data-ttu-id="67e64-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="67e64-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-works-mobile-from-hello-gallery"></a><span data-ttu-id="67e64-123">Merhaba Galerisi'nden WORKS mobil ekleme</span><span class="sxs-lookup"><span data-stu-id="67e64-123">Adding WORKS MOBILE from hello gallery</span></span>
<span data-ttu-id="67e64-124">Azure AD'ye tooconfigure hello tümleştirme WORKS Mobile tooadd WORKS mobil hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="67e64-124">tooconfigure hello integration of WORKS MOBILE into Azure AD, you need tooadd WORKS MOBILE from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="67e64-125">**tooadd WORKS mobil hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="67e64-125">**tooadd WORKS MOBILE from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="67e64-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="67e64-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="67e64-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="67e64-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="67e64-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="67e64-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="67e64-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="67e64-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="67e64-133">Merhaba arama kutusuna yazın **WORKS mobil**.</span><span class="sxs-lookup"><span data-stu-id="67e64-133">In hello search box, type **WORKS MOBILE**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_search.png)

5. <span data-ttu-id="67e64-135">Merhaba Sonuçlar panelinde seçin **WORKS mobil**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="67e64-135">In hello results panel, select **WORKS MOBILE**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="67e64-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="67e64-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="67e64-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma WORKS "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı MOBILE ile test etme</span><span class="sxs-lookup"><span data-stu-id="67e64-138">In this section, you configure and test Azure AD single sign-on with WORKS MOBILE based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="67e64-139">Tek toowork'ın oturum açma hangi hello karşılık gelen WORKS Mobile'da tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="67e64-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in WORKS MOBILE is tooa user in Azure AD.</span></span> <span data-ttu-id="67e64-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve WORKS Mobile'da hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="67e64-140">In other words, a link relationship between an Azure AD user and hello related user in WORKS MOBILE needs toobe established.</span></span>

<span data-ttu-id="67e64-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** WORKS Mobile'da.</span><span class="sxs-lookup"><span data-stu-id="67e64-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in WORKS MOBILE.</span></span>

<span data-ttu-id="67e64-142">tooconfigure ve WORKS MOBILE ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="67e64-142">tooconfigure and test Azure AD single sign-on with WORKS MOBILE, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="67e64-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="67e64-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="67e64-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="67e64-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="67e64-145">**[WORKS mobil test kullanıcısı oluşturma](#creating-a-works-mobile-test-user)**  -toohave karşılık gelen, Britta Simon WORKS Mobile'da kullanıcı bağlantılı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="67e64-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - toohave a counterpart of Britta Simon in WORKS MOBILE that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="67e64-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="67e64-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="67e64-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="67e64-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="67e64-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="67e64-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="67e64-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma WORKS mobil uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="67e64-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your WORKS MOBILE application.</span></span>

<span data-ttu-id="67e64-150">**tooconfigure Azure AD çoklu oturum açma WORKS MOBILE ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="67e64-150">**tooconfigure Azure AD single sign-on with WORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="67e64-151">Merhaba hello üzerinde Azure portal'ın **WORKS mobil** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="67e64-151">In hello Azure portal, on hello **WORKS MOBILE** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="67e64-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="67e64-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_samlbase.png)

3. <span data-ttu-id="67e64-155">Merhaba üzerinde **WORKS mobil etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="67e64-155">On hello **WORKS MOBILE Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_url.png)

    <span data-ttu-id="67e64-157">a.</span><span class="sxs-lookup"><span data-stu-id="67e64-157">a.</span></span> <span data-ttu-id="67e64-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.worksmobile.com/jp/myservice`</span><span class="sxs-lookup"><span data-stu-id="67e64-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.worksmobile.com/jp/myservice`</span></span>

    <span data-ttu-id="67e64-159">b.</span><span class="sxs-lookup"><span data-stu-id="67e64-159">b.</span></span> <span data-ttu-id="67e64-160">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello değeri olarak`worksmobile.com`</span><span class="sxs-lookup"><span data-stu-id="67e64-160">In hello **Identifier** textbox, type hello value as `worksmobile.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="67e64-161">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="67e64-161">This value is not real.</span></span> <span data-ttu-id="67e64-162">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="67e64-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="67e64-163">Kişi [WORKS mobil istemci destek ekibi](mailto:dl_ssoinfo@worksmobile.com) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="67e64-163">Contact [WORKS MOBILE Client support team](mailto:dl_ssoinfo@worksmobile.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="67e64-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Raw)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="67e64-164">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_certificate.png) 

5. <span data-ttu-id="67e64-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="67e64-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-worksmobile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="67e64-168">Merhaba üzerinde **WORKS mobil yapılandırma** 'yi tıklatın **yapılandırma WORKS mobil** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="67e64-168">On hello **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="67e64-169">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="67e64-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_configure.png) 

7. <span data-ttu-id="67e64-171">tooget SSO yapılandırılmış uygulamanızın, kişi [WORKS mobil destek ekibi](mailto:dl_ssoinfo@worksmobile.com) ve aşağıdaki bilgilerle hello ile verin:</span><span class="sxs-lookup"><span data-stu-id="67e64-171">tooget SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with hello following information:</span></span> 

    <span data-ttu-id="67e64-172">• hello indirilen **sertifika dosyası**</span><span class="sxs-lookup"><span data-stu-id="67e64-172">• hello downloaded **Certificate file**</span></span>

    <span data-ttu-id="67e64-173">• hello **SAML çoklu oturum açma hizmet URL'si**</span><span class="sxs-lookup"><span data-stu-id="67e64-173">• hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="67e64-174">• hello **SAML varlık kimliği**</span><span class="sxs-lookup"><span data-stu-id="67e64-174">• hello **SAML Entity ID**</span></span>

    <span data-ttu-id="67e64-175">• hello **Sign-Out URL'si**</span><span class="sxs-lookup"><span data-stu-id="67e64-175">• hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="67e64-176">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="67e64-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="67e64-177">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="67e64-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="67e64-178">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="67e64-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="67e64-179">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="67e64-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="67e64-180">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="67e64-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="67e64-182">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="67e64-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="67e64-183">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="67e64-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="67e64-185">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="67e64-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="67e64-187">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="67e64-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="67e64-189">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="67e64-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="67e64-191">a.</span><span class="sxs-lookup"><span data-stu-id="67e64-191">a.</span></span> <span data-ttu-id="67e64-192">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="67e64-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="67e64-193">b.</span><span class="sxs-lookup"><span data-stu-id="67e64-193">b.</span></span> <span data-ttu-id="67e64-194">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="67e64-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="67e64-195">c.</span><span class="sxs-lookup"><span data-stu-id="67e64-195">c.</span></span> <span data-ttu-id="67e64-196">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="67e64-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="67e64-197">d.</span><span class="sxs-lookup"><span data-stu-id="67e64-197">d.</span></span> <span data-ttu-id="67e64-198">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="67e64-198">Click **Create**.</span></span>
 
### <a name="creating-a-works-mobile-test-user"></a><span data-ttu-id="67e64-199">WORKS mobil test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="67e64-199">Creating a WORKS MOBILE test user</span></span>

 <span data-ttu-id="67e64-200">Bu bölümde, Britta Simon WORKS MOBİLE'da adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="67e64-200">In this section, you create a user called Britta Simon in WORKS MOBILE.</span></span> <span data-ttu-id="67e64-201">Lütfen çalışmak [WORKS mobil destek ekibi](mailto:dl_ssoinfo@worksmobile.com) tooadd hello kullanıcılar hello WORKS mobil Platform.</span><span class="sxs-lookup"><span data-stu-id="67e64-201">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) tooadd hello users in hello WORKS MOBILE platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="67e64-202">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="67e64-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="67e64-203">Bu bölümde, erişim tooWORKS mobil vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="67e64-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWORKS MOBILE.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="67e64-205">**tooassign Britta Simon tooWORKS MOBILE, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="67e64-205">**tooassign Britta Simon tooWORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="67e64-206">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="67e64-206">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="67e64-208">Merhaba uygulamalar listesinde **WORKS mobil**.</span><span class="sxs-lookup"><span data-stu-id="67e64-208">In hello applications list, select **WORKS MOBILE**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_app.png) 

3. <span data-ttu-id="67e64-210">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="67e64-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="67e64-212">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="67e64-212">Click **Add** button.</span></span> <span data-ttu-id="67e64-213">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="67e64-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="67e64-215">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="67e64-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="67e64-216">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="67e64-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="67e64-217">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="67e64-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="67e64-218">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="67e64-218">Testing single sign-on</span></span>

<span data-ttu-id="67e64-219">Bu bölümde, Azure AD SSO yapılandırmanızı hello erişim paneli kullanarak sınayın.</span><span class="sxs-lookup"><span data-stu-id="67e64-219">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="67e64-220">Merhaba WORKS mobil hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour WORKS mobil uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="67e64-220">When you click hello WORKS MOBILE tile in hello Access Panel, you should get automatically signed-on tooyour WORKS MOBILE application.</span></span>
<span data-ttu-id="67e64-221">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="67e64-221">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="67e64-222">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="67e64-222">Additional resources</span></span>

* [<span data-ttu-id="67e64-223">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="67e64-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="67e64-224">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="67e64-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_203.png

