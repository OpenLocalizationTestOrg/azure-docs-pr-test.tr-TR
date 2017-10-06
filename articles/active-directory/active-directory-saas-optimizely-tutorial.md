---
title: "Öğretici: Azure Active Directory Tümleştirme ile Optimizely | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Optimizely arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 868aefae27ca155d2963f3dcfcd79bbb564b48ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a><span data-ttu-id="fb53d-103">Öğretici: Azure Active Directory Tümleştirme Optimizely ile</span><span class="sxs-lookup"><span data-stu-id="fb53d-103">Tutorial: Azure Active Directory integration with Optimizely</span></span>

<span data-ttu-id="fb53d-104">Bu öğreticide, bilgi nasıl toointegrate Optimizely Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fb53d-104">In this tutorial, you learn how toointegrate Optimizely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fb53d-105">Optimizely Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="fb53d-105">Integrating Optimizely with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fb53d-106">Erişim tooOptimizely sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="fb53d-106">You can control in Azure AD who has access tooOptimizely</span></span>
- <span data-ttu-id="fb53d-107">Kullanıcıların tooautomatically get açan tooOptimizely (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="fb53d-107">You can enable your users tooautomatically get signed-on tooOptimizely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fb53d-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="fb53d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fb53d-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fb53d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb53d-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fb53d-110">Prerequisites</span></span>

<span data-ttu-id="fb53d-111">tooconfigure Optimizely ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="fb53d-111">tooconfigure Azure AD integration with Optimizely, you need hello following items:</span></span>

- <span data-ttu-id="fb53d-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="fb53d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fb53d-113">Bir Optimizely çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="fb53d-113">An Optimizely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fb53d-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="fb53d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fb53d-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="fb53d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fb53d-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="fb53d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fb53d-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fb53d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fb53d-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="fb53d-118">Scenario description</span></span>
<span data-ttu-id="fb53d-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="fb53d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fb53d-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="fb53d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fb53d-121">Merhaba Galerisi'nden Optimizely ekleme</span><span class="sxs-lookup"><span data-stu-id="fb53d-121">Adding Optimizely from hello gallery</span></span>
2. <span data-ttu-id="fb53d-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="fb53d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-optimizely-from-hello-gallery"></a><span data-ttu-id="fb53d-123">Merhaba Galerisi'nden Optimizely ekleme</span><span class="sxs-lookup"><span data-stu-id="fb53d-123">Adding Optimizely from hello gallery</span></span>
<span data-ttu-id="fb53d-124">Azure AD'ye tooconfigure hello tümleştirme Optimizely, tooadd Optimizely hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb53d-124">tooconfigure hello integration of Optimizely into Azure AD, you need tooadd Optimizely from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fb53d-125">**tooadd Optimizely hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fb53d-125">**tooadd Optimizely from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb53d-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fb53d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fb53d-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="fb53d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fb53d-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fb53d-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="fb53d-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fb53d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="fb53d-133">Merhaba arama kutusuna yazın **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="fb53d-133">In hello search box, type **Optimizely**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. <span data-ttu-id="fb53d-135">Merhaba Sonuçlar panelinde seçin **Optimizely**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="fb53d-135">In hello results panel, select **Optimizely**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fb53d-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="fb53d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fb53d-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Optimizely ile test etme</span><span class="sxs-lookup"><span data-stu-id="fb53d-138">In this section, you configure and test Azure AD single sign-on with Optimizely based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fb53d-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Optimizely içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb53d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Optimizely is tooa user in Azure AD.</span></span> <span data-ttu-id="fb53d-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Optimizely hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb53d-140">In other words, a link relationship between an Azure AD user and hello related user in Optimizely needs toobe established.</span></span>

<span data-ttu-id="fb53d-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Optimizely içinde.</span><span class="sxs-lookup"><span data-stu-id="fb53d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Optimizely.</span></span>

<span data-ttu-id="fb53d-142">tooconfigure ve Optimizely ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="fb53d-142">tooconfigure and test Azure AD single sign-on with Optimizely, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fb53d-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="fb53d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fb53d-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="fb53d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fb53d-145">**[Bir Optimizely test kullanıcısı oluşturma](#creating-an-optimizely-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Optimizely içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="fb53d-145">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - toohave a counterpart of Britta Simon in Optimizely that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fb53d-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="fb53d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fb53d-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="fb53d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fb53d-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fb53d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fb53d-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Optimizely uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fb53d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Optimizely application.</span></span>

<span data-ttu-id="fb53d-150">**tooconfigure Azure AD çoklu oturum açma ile Optimizely, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fb53d-150">**tooconfigure Azure AD single sign-on with Optimizely, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb53d-151">Hello hello üzerinde Azure portal'ın **Optimizely** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="fb53d-151">In hello Azure portal, on hello **Optimizely** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="fb53d-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="fb53d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. <span data-ttu-id="fb53d-155">Merhaba üzerinde **Optimizely etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fb53d-155">On hello **Optimizely Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    <span data-ttu-id="fb53d-157">a.</span><span class="sxs-lookup"><span data-stu-id="fb53d-157">a.</span></span> <span data-ttu-id="fb53d-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://app.optimizely.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="fb53d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.optimizely.net/<instance name>`</span></span>

    <span data-ttu-id="fb53d-159">b.</span><span class="sxs-lookup"><span data-stu-id="fb53d-159">b.</span></span> <span data-ttu-id="fb53d-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`urn:auth0:optimizely:contoso`</span><span class="sxs-lookup"><span data-stu-id="fb53d-160">In hello **Identifier** textbox, type a URL using hello following pattern:  `urn:auth0:optimizely:contoso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fb53d-161">Bu değerler hello gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="fb53d-161">These values are not hello real.</span></span> <span data-ttu-id="fb53d-162">Oturum açma hello gerçek URL'si ve hello öğreticinin ilerleyen bölümlerinde açıklanan tanımlayıcısı ile Merhaba değeri güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="fb53d-162">You will update hello value with hello actual Sign-on URL and Identifier, which is explained later in hello tutorial.</span></span> 

4. <span data-ttu-id="fb53d-163">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fb53d-163">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. <span data-ttu-id="fb53d-165">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fb53d-165">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fb53d-167">Merhaba üzerinde **Optimizely yapılandırma** 'yi tıklatın **yapılandırma Optimizely** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="fb53d-167">On hello **Optimizely Configuration** section, click **Configure Optimizely** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fb53d-168">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="fb53d-168">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. <span data-ttu-id="fb53d-170">tooconfigure çoklu oturum açma üzerinde **Optimizely** tarafı, Optimizely hesap yöneticinize başvurun ve sağlamak indirilen hello **sertifika (Base64)**, ve **SAML çoklu oturum açma hizmet URL'si** .</span><span class="sxs-lookup"><span data-stu-id="fb53d-170">tooconfigure single sign-on on **Optimizely** side, contact your Optimizely Account Manager and provide hello downloaded **Certificate (Base64)**, and **SAML Single Sign-On Service URL**.</span></span> 

8. <span data-ttu-id="fb53d-171">Yanıt tooyour e-posta ile Optimizely, hello oturum üzerinde URL'si (SP tarafından başlatılan SSO'yu) ve hello tanımlayıcı (hizmet sağlayıcısı varlık kimliği) değerlerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="fb53d-171">In response tooyour email, Optimizely provides you with hello Sign On URL (SP-initiated SSO) and hello Identifier (Service Provider Entity ID) values.</span></span>

    <span data-ttu-id="fb53d-172">a.</span><span class="sxs-lookup"><span data-stu-id="fb53d-172">a.</span></span> <span data-ttu-id="fb53d-173">Kopya hello **SP tarafından başlatılan SSO'yu URL** Optimizely ve hello içine yapıştırma tarafından sağlanan **oturum üzerinde URL'si** metin kutusuna **Optimizely etki alanı ve URL'leri** Azure Portal'daki bölümü</span><span class="sxs-lookup"><span data-stu-id="fb53d-173">Copy hello **SP-initiated SSO URL** provided by Optimizely, and paste into hello **Sign On URL** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

    <span data-ttu-id="fb53d-174">b.</span><span class="sxs-lookup"><span data-stu-id="fb53d-174">b.</span></span> <span data-ttu-id="fb53d-175">Kopya hello **hizmet sağlayıcısı varlık kimliği** Optimizely ve hello içine yapıştırma tarafından sağlanan **tanımlayıcısı** metin kutusuna **Optimizely etki alanı ve URL'leri** Azure Portal'daki bölümü</span><span class="sxs-lookup"><span data-stu-id="fb53d-175">Copy hello **Service Provider Entity ID** provided by Optimizely, and paste into hello **Identifier** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

9. <span data-ttu-id="fb53d-176">Farklı bir tarayıcı penceresinde oturum açma Optimizely uygulama tooyour.</span><span class="sxs-lookup"><span data-stu-id="fb53d-176">In a different browser window, sign-on tooyour Optimizely application.</span></span>

10. <span data-ttu-id="fb53d-177">Hesap adı hello üst, sağ alt köşesinde tıklatın ve ardından **hesap ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="fb53d-177">Click you account name in hello top right corner and then **Account Settings**.</span></span>
   
    ![Azure AD çoklu oturum açma](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. <span data-ttu-id="fb53d-179">Merhaba hesap sekmesinde hello kutuyu **etkinleştirmek SSO** çoklu oturum açma hello içinde altında **genel bakış** bölüm.</span><span class="sxs-lookup"><span data-stu-id="fb53d-179">In hello Account tab, check hello box **Enable SSO** under Single Sign On in hello **Overview** section.</span></span>
   
    ![Azure AD çoklu oturum açma](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. <span data-ttu-id="fb53d-181">Tıklatın **Kaydet**</span><span class="sxs-lookup"><span data-stu-id="fb53d-181">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="fb53d-182">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="fb53d-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fb53d-183">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="fb53d-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fb53d-184">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fb53d-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fb53d-185">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fb53d-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="fb53d-186">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="fb53d-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="fb53d-188">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fb53d-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb53d-189">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fb53d-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fb53d-191">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="fb53d-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fb53d-193">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="fb53d-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fb53d-195">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fb53d-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fb53d-197">a.</span><span class="sxs-lookup"><span data-stu-id="fb53d-197">a.</span></span> <span data-ttu-id="fb53d-198">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fb53d-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fb53d-199">b.</span><span class="sxs-lookup"><span data-stu-id="fb53d-199">b.</span></span> <span data-ttu-id="fb53d-200">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="fb53d-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="fb53d-201">c.</span><span class="sxs-lookup"><span data-stu-id="fb53d-201">c.</span></span> <span data-ttu-id="fb53d-202">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="fb53d-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fb53d-203">d.</span><span class="sxs-lookup"><span data-stu-id="fb53d-203">d.</span></span> <span data-ttu-id="fb53d-204">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fb53d-204">Click **Create**.</span></span>
 
### <a name="creating-an-optimizely-test-user"></a><span data-ttu-id="fb53d-205">Bir Optimizely test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fb53d-205">Creating an Optimizely test user</span></span>

<span data-ttu-id="fb53d-206">Bu bölümde, Optimizely içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fb53d-206">In this section, you create a user called Britta Simon in Optimizely.</span></span>

1. <span data-ttu-id="fb53d-207">Merhaba giriş sayfasında, seçin **ortak** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="fb53d-207">On hello home page, select **Collaborators** tab.</span></span>

2. <span data-ttu-id="fb53d-208">tooadd yeni bir ortak çalışanı toohello projesi tıklatın **yeni bir ortak çalışanı**.</span><span class="sxs-lookup"><span data-stu-id="fb53d-208">tooadd new collaborator toohello project, click **New Collaborator**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. <span data-ttu-id="fb53d-210">Merhaba e-posta adresini doldurduğunuzda ve bir rol atayın.</span><span class="sxs-lookup"><span data-stu-id="fb53d-210">Fill in hello email address and assign them a role.</span></span> <span data-ttu-id="fb53d-211">Tıklatın **davet**.</span><span class="sxs-lookup"><span data-stu-id="fb53d-211">Click **Invite**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. <span data-ttu-id="fb53d-213">Bir e-posta davet alırlar.</span><span class="sxs-lookup"><span data-stu-id="fb53d-213">They receive an email invite.</span></span> <span data-ttu-id="fb53d-214">Merhaba e-posta adresini kullanarak toolog içinde tooOptimizely sahiptirler.</span><span class="sxs-lookup"><span data-stu-id="fb53d-214">Using hello email address, they have toolog in tooOptimizely.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fb53d-215">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="fb53d-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fb53d-216">Bu bölümde, erişim tooOptimizely vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="fb53d-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOptimizely.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="fb53d-218">**tooassign Britta Simon tooOptimizely hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fb53d-218">**tooassign Britta Simon tooOptimizely, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb53d-219">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fb53d-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="fb53d-221">Merhaba uygulamalar listesinde **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="fb53d-221">In hello applications list, select **Optimizely**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. <span data-ttu-id="fb53d-223">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="fb53d-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="fb53d-225">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fb53d-225">Click **Add** button.</span></span> <span data-ttu-id="fb53d-226">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fb53d-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="fb53d-228">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="fb53d-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fb53d-229">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fb53d-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fb53d-230">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fb53d-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fb53d-231">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="fb53d-231">Testing single sign-on</span></span>

<span data-ttu-id="fb53d-232">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="fb53d-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fb53d-233">Merhaba Optimizely hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Optimizely uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb53d-233">When you click hello Optimizely tile in hello Access Panel, you should get automatically signed-on tooyour Optimizely application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fb53d-234">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="fb53d-234">Additional resources</span></span>

* [<span data-ttu-id="fb53d-235">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="fb53d-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fb53d-236">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="fb53d-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

