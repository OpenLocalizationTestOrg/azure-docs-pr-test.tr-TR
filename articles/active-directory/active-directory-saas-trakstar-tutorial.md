---
title: "Öğretici: Azure Active Directory Tümleştirme ile Trakstar | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Trakstar arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411cb8c3-95c6-4138-acf2-ffc7f663e89a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 88101355ce2674bd14e3131000bbe182a06f252a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trakstar"></a><span data-ttu-id="3e94b-103">Öğretici: Azure Active Directory Tümleştirme Trakstar ile</span><span class="sxs-lookup"><span data-stu-id="3e94b-103">Tutorial: Azure Active Directory integration with Trakstar</span></span>

<span data-ttu-id="3e94b-104">Bu öğreticide, bilgi nasıl toointegrate Trakstar Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3e94b-104">In this tutorial, you learn how toointegrate Trakstar with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3e94b-105">Trakstar Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="3e94b-105">Integrating Trakstar with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3e94b-106">Erişim tooTrakstar sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="3e94b-106">You can control in Azure AD who has access tooTrakstar</span></span>
- <span data-ttu-id="3e94b-107">Kullanıcıların tooautomatically get açan tooTrakstar (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="3e94b-107">You can enable your users tooautomatically get signed-on tooTrakstar (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3e94b-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="3e94b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3e94b-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3e94b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e94b-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3e94b-110">Prerequisites</span></span>

<span data-ttu-id="3e94b-111">tooconfigure Trakstar ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="3e94b-111">tooconfigure Azure AD integration with Trakstar, you need hello following items:</span></span>

- <span data-ttu-id="3e94b-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="3e94b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3e94b-113">Bir Trakstar çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="3e94b-113">A Trakstar single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3e94b-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="3e94b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3e94b-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="3e94b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3e94b-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="3e94b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3e94b-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3e94b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3e94b-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="3e94b-118">Scenario description</span></span>
<span data-ttu-id="3e94b-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="3e94b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3e94b-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="3e94b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e94b-121">Merhaba Galerisi'nden Trakstar ekleme</span><span class="sxs-lookup"><span data-stu-id="3e94b-121">Adding Trakstar from hello gallery</span></span>
2. <span data-ttu-id="3e94b-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="3e94b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trakstar-from-hello-gallery"></a><span data-ttu-id="3e94b-123">Merhaba Galerisi'nden Trakstar ekleme</span><span class="sxs-lookup"><span data-stu-id="3e94b-123">Adding Trakstar from hello gallery</span></span>
<span data-ttu-id="3e94b-124">Azure AD'ye tooconfigure hello tümleştirme Trakstar, tooadd Trakstar hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e94b-124">tooconfigure hello integration of Trakstar into Azure AD, you need tooadd Trakstar from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3e94b-125">**tooadd Trakstar hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3e94b-125">**tooadd Trakstar from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e94b-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3e94b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3e94b-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="3e94b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3e94b-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3e94b-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="3e94b-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3e94b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="3e94b-133">Merhaba arama kutusuna yazın **Trakstar**.</span><span class="sxs-lookup"><span data-stu-id="3e94b-133">In hello search box, type **Trakstar**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_search.png)

5. <span data-ttu-id="3e94b-135">Merhaba Sonuçlar panelinde seçin **Trakstar**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="3e94b-135">In hello results panel, select **Trakstar**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3e94b-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="3e94b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3e94b-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Trakstar ile test etme</span><span class="sxs-lookup"><span data-stu-id="3e94b-138">In this section, you configure and test Azure AD single sign-on with Trakstar based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3e94b-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Trakstar içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e94b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Trakstar is tooa user in Azure AD.</span></span> <span data-ttu-id="3e94b-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Trakstar hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e94b-140">In other words, a link relationship between an Azure AD user and hello related user in Trakstar needs toobe established.</span></span>

<span data-ttu-id="3e94b-141">Merhaba hello değeri Trakstar içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="3e94b-141">In Trakstar, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3e94b-142">tooconfigure ve Trakstar ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="3e94b-142">tooconfigure and test Azure AD single sign-on with Trakstar, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3e94b-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="3e94b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3e94b-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="3e94b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3e94b-145">**[Trakstar test kullanıcısı oluşturma](#creating-a-trakstar-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Trakstar içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="3e94b-145">**[Creating a Trakstar test user](#creating-a-trakstar-test-user)** - toohave a counterpart of Britta Simon in Trakstar that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3e94b-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="3e94b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3e94b-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="3e94b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3e94b-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3e94b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3e94b-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Trakstar uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3e94b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Trakstar application.</span></span>

<span data-ttu-id="3e94b-150">**tooconfigure Azure AD çoklu oturum açma ile Trakstar, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3e94b-150">**tooconfigure Azure AD single sign-on with Trakstar, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e94b-151">Hello hello üzerinde Azure portal'ın **Trakstar** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="3e94b-151">In hello Azure portal, on hello **Trakstar** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="3e94b-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="3e94b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_samlbase.png)

3. <span data-ttu-id="3e94b-155">Merhaba üzerinde **Trakstar etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3e94b-155">On hello **Trakstar Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_url.png)

    <span data-ttu-id="3e94b-157">a.</span><span class="sxs-lookup"><span data-stu-id="3e94b-157">a.</span></span> <span data-ttu-id="3e94b-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://app.trakstar.com/auth/saml/callback?namespace=<NAMESPACE>`</span><span class="sxs-lookup"><span data-stu-id="3e94b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.trakstar.com/auth/saml/callback?namespace=<NAMESPACE>`</span></span>

    <span data-ttu-id="3e94b-159">b.</span><span class="sxs-lookup"><span data-stu-id="3e94b-159">b.</span></span> <span data-ttu-id="3e94b-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.trakstar.com`</span><span class="sxs-lookup"><span data-stu-id="3e94b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.trakstar.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3e94b-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="3e94b-161">These values are not real.</span></span> <span data-ttu-id="3e94b-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="3e94b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3e94b-163">Kişi [Trakstar istemci destek ekibi](mailto:integrations@trakstar.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="3e94b-163">Contact [Trakstar Client support team](mailto:integrations@trakstar.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="3e94b-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3e94b-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_certificate.png) 

5. <span data-ttu-id="3e94b-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3e94b-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trakstar-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3e94b-168">Merhaba üzerinde **Trakstar yapılandırma** 'yi tıklatın **yapılandırma Trakstar** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="3e94b-168">On hello **Trakstar Configuration** section, click **Configure Trakstar** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3e94b-169">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="3e94b-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_configure.png) 

7. <span data-ttu-id="3e94b-171">tooconfigure çoklu oturum açma üzerinde **Trakstar** yan, indirilen toosend hello ihtiyacınız **sertifika (Base64)**, **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si**çok[Trakstar destek ekibi](mailto:integrations@trakstar.com).</span><span class="sxs-lookup"><span data-stu-id="3e94b-171">tooconfigure single sign-on on **Trakstar** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Trakstar support team](mailto:integrations@trakstar.com).</span></span> 

> [!TIP]
> <span data-ttu-id="3e94b-172">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="3e94b-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3e94b-173">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="3e94b-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3e94b-174">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3e94b-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3e94b-175">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3e94b-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="3e94b-176">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="3e94b-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="3e94b-178">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3e94b-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e94b-179">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3e94b-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-trakstar-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3e94b-181">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="3e94b-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-trakstar-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3e94b-183">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="3e94b-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-trakstar-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3e94b-185">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3e94b-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-trakstar-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3e94b-187">a.</span><span class="sxs-lookup"><span data-stu-id="3e94b-187">a.</span></span> <span data-ttu-id="3e94b-188">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3e94b-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3e94b-189">b.</span><span class="sxs-lookup"><span data-stu-id="3e94b-189">b.</span></span> <span data-ttu-id="3e94b-190">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="3e94b-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3e94b-191">c.</span><span class="sxs-lookup"><span data-stu-id="3e94b-191">c.</span></span> <span data-ttu-id="3e94b-192">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="3e94b-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3e94b-193">d.</span><span class="sxs-lookup"><span data-stu-id="3e94b-193">d.</span></span> <span data-ttu-id="3e94b-194">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3e94b-194">Click **Create**.</span></span>
 
### <a name="creating-a-trakstar-test-user"></a><span data-ttu-id="3e94b-195">Trakstar test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3e94b-195">Creating a Trakstar test user</span></span>

<span data-ttu-id="3e94b-196">Bu bölümde Hello amacı toocreate Britta Simon içinde Trakstar adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="3e94b-196">hello objective of this section is toocreate a user called Britta Simon in Trakstar.</span></span> <span data-ttu-id="3e94b-197">Çalışmak [Trakstar destek ekibi](mailto:integrations@trakstar.com) tooadd hello hello Trakstar hesap kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="3e94b-197">Work with [Trakstar support team](mailto:integrations@trakstar.com) tooadd hello users in hello Trakstar account.</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3e94b-198">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="3e94b-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3e94b-199">Bu bölümde, erişim tooTrakstar vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="3e94b-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTrakstar.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="3e94b-201">**tooassign Britta Simon tooTrakstar hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3e94b-201">**tooassign Britta Simon tooTrakstar, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e94b-202">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3e94b-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="3e94b-204">Merhaba uygulamalar listesinde **Trakstar**.</span><span class="sxs-lookup"><span data-stu-id="3e94b-204">In hello applications list, select **Trakstar**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_app.png) 

3. <span data-ttu-id="3e94b-206">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="3e94b-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="3e94b-208">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3e94b-208">Click **Add** button.</span></span> <span data-ttu-id="3e94b-209">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3e94b-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="3e94b-211">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="3e94b-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3e94b-212">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3e94b-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3e94b-213">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3e94b-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3e94b-214">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="3e94b-214">Testing single sign-on</span></span>

<span data-ttu-id="3e94b-215">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="3e94b-215">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="3e94b-216">Merhaba Trakstar hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Trakstar uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e94b-216">When you click hello Trakstar tile in hello Access Panel, you should get automatically signed-on tooyour Trakstar application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3e94b-217">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3e94b-217">Additional resources</span></span>

* [<span data-ttu-id="3e94b-218">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="3e94b-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e94b-219">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="3e94b-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_203.png

