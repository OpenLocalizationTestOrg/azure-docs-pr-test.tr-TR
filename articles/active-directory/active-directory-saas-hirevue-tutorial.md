---
title: "Öğretici: Azure Active Directory Tümleştirme ile HireVue | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile HireVue arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aadfc342-14db-4d74-a83d-f0c76f0cf63c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f890633ee4f13919c32a43d7b6cf30f2270ef6a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hirevue"></a><span data-ttu-id="2f0b7-103">Öğretici: Azure Active Directory Tümleştirme HireVue ile</span><span class="sxs-lookup"><span data-stu-id="2f0b7-103">Tutorial: Azure Active Directory integration with HireVue</span></span>

<span data-ttu-id="2f0b7-104">Bu öğreticide, bilgi nasıl toointegrate HireVue Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2f0b7-104">In this tutorial, you learn how toointegrate HireVue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f0b7-105">HireVue Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="2f0b7-105">Integrating HireVue with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2f0b7-106">Erişim tooHireVue sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2f0b7-106">You can control in Azure AD who has access tooHireVue</span></span>
- <span data-ttu-id="2f0b7-107">Kullanıcıların tooautomatically get açan tooHireVue (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2f0b7-107">You can enable your users tooautomatically get signed-on tooHireVue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2f0b7-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="2f0b7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2f0b7-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2f0b7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f0b7-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2f0b7-110">Prerequisites</span></span>

<span data-ttu-id="2f0b7-111">tooconfigure HireVue ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2f0b7-111">tooconfigure Azure AD integration with HireVue, you need hello following items:</span></span>

- <span data-ttu-id="2f0b7-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="2f0b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f0b7-113">Bir HireVue çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="2f0b7-113">A HireVue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2f0b7-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2f0b7-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="2f0b7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f0b7-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2f0b7-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f0b7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f0b7-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="2f0b7-118">Scenario description</span></span>
<span data-ttu-id="2f0b7-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2f0b7-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="2f0b7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2f0b7-121">Merhaba Galerisi'nden HireVue ekleme</span><span class="sxs-lookup"><span data-stu-id="2f0b7-121">Adding HireVue from hello gallery</span></span>
2. <span data-ttu-id="2f0b7-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2f0b7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hirevue-from-hello-gallery"></a><span data-ttu-id="2f0b7-123">Merhaba Galerisi'nden HireVue ekleme</span><span class="sxs-lookup"><span data-stu-id="2f0b7-123">Adding HireVue from hello gallery</span></span>
<span data-ttu-id="2f0b7-124">Azure AD'ye tooconfigure hello tümleştirme HireVue, tooadd HireVue hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-124">tooconfigure hello integration of HireVue into Azure AD, you need tooadd HireVue from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2f0b7-125">**tooadd HireVue hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2f0b7-125">**tooadd HireVue from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f0b7-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2f0b7-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2f0b7-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="2f0b7-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="2f0b7-133">Merhaba arama kutusuna yazın **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-133">In hello search box, type **HireVue**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_search.png)

5. <span data-ttu-id="2f0b7-135">Merhaba Sonuçlar panelinde seçin **HireVue**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-135">In hello results panel, select **HireVue**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2f0b7-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2f0b7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2f0b7-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı HireVue sınayın.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-138">In this section, you configure and test Azure AD single sign-on with HireVue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2f0b7-139">Tek toowork'ın oturum açma hangi hello karşılık gelen HireVue içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HireVue is tooa user in Azure AD.</span></span> <span data-ttu-id="2f0b7-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı HireVue hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-140">In other words, a link relationship between an Azure AD user and hello related user in HireVue needs toobe established.</span></span>

<span data-ttu-id="2f0b7-141">Merhaba hello değeri HireVue içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-141">In HireVue, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2f0b7-142">tooconfigure ve HireVue ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2f0b7-142">tooconfigure and test Azure AD single sign-on with HireVue, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2f0b7-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2f0b7-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2f0b7-145">**[HireVue test kullanıcısı oluşturma](#creating-a-hirevue-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir HireVue içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-145">**[Creating a HireVue test user](#creating-a-hirevue-test-user)** - toohave a counterpart of Britta Simon in HireVue that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2f0b7-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2f0b7-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2f0b7-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2f0b7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2f0b7-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma HireVue uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HireVue application.</span></span>

<span data-ttu-id="2f0b7-150">**tooconfigure Azure AD çoklu oturum açma ile HireVue, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2f0b7-150">**tooconfigure Azure AD single sign-on with HireVue, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f0b7-151">Hello hello üzerinde Azure portal'ın **HireVue** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-151">In hello Azure portal, on hello **HireVue** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="2f0b7-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_samlbase.png)

3. <span data-ttu-id="2f0b7-155">Merhaba üzerinde **HireVue etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2f0b7-155">On hello **HireVue Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_url.png)

    <span data-ttu-id="2f0b7-157">a.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-157">a.</span></span> <span data-ttu-id="2f0b7-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="2f0b7-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>

    | <span data-ttu-id="2f0b7-159">Ortam</span><span class="sxs-lookup"><span data-stu-id="2f0b7-159">Environment</span></span> | <span data-ttu-id="2f0b7-160">URL</span><span class="sxs-lookup"><span data-stu-id="2f0b7-160">URL</span></span> |
    |-------------|---|
    | <span data-ttu-id="2f0b7-161">Üretim</span><span class="sxs-lookup"><span data-stu-id="2f0b7-161">Production</span></span> | `https://<companyname>.hirevue.com` |
    | <span data-ttu-id="2f0b7-162">Hazırlama</span><span class="sxs-lookup"><span data-stu-id="2f0b7-162">Staging</span></span>    | `https://<companyname>.stghv.com` |
    
    <span data-ttu-id="2f0b7-163">b.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-163">b.</span></span> <span data-ttu-id="2f0b7-164">Merhaba, **tanımlayıcısı** metin kutusuna, URL'yi yazın:</span><span class="sxs-lookup"><span data-stu-id="2f0b7-164">In hello **Identifier** textbox, type a URL as:</span></span>
    
    | <span data-ttu-id="2f0b7-165">Ortam</span><span class="sxs-lookup"><span data-stu-id="2f0b7-165">Environment</span></span> | <span data-ttu-id="2f0b7-166">URN</span><span class="sxs-lookup"><span data-stu-id="2f0b7-166">URN</span></span> |
    |-------------|-----|
    | <span data-ttu-id="2f0b7-167">Üretim</span><span class="sxs-lookup"><span data-stu-id="2f0b7-167">Production</span></span> |`urn:federation:hirevue.com:saml:sp:prod` |
    | <span data-ttu-id="2f0b7-168">Hazırlama</span><span class="sxs-lookup"><span data-stu-id="2f0b7-168">Staging</span></span>    | `urn:federation:hirevue.com:saml:sp:staging`|
    
    > [!NOTE] 
    > <span data-ttu-id="2f0b7-169">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-169">These values are not real.</span></span> <span data-ttu-id="2f0b7-170">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-170">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2f0b7-171">Kişi [HireVue istemci destek ekibi](mailto:samlsupport@hirevue.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-171">Contact [HireVue Client support team](mailto:samlsupport@hirevue.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="2f0b7-172">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-172">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_certificate.png) 

5. <span data-ttu-id="2f0b7-174">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-174">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hirevue-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2f0b7-176">Merhaba üzerinde **HireVue yapılandırma** 'yi tıklatın **yapılandırma HireVue** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-176">On hello **HireVue Configuration** section, click **Configure HireVue** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2f0b7-177">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="2f0b7-177">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_configure.png) 

7. <span data-ttu-id="2f0b7-179">tooconfigure çoklu oturum açma üzerinde **HireVue** yan, indirilen toosend hello ihtiyacınız **Certificate(Base64)** ve **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** çok[HireVue destek ekibi](mailto:samlsupport@hirevue.com).</span><span class="sxs-lookup"><span data-stu-id="2f0b7-179">tooconfigure single sign-on on **HireVue** side, you need toosend hello downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[HireVue support team](mailto:samlsupport@hirevue.com).</span></span> <span data-ttu-id="2f0b7-180">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-180">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="2f0b7-181">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="2f0b7-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2f0b7-182">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2f0b7-183">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2f0b7-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2f0b7-184">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2f0b7-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="2f0b7-185">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="2f0b7-187">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2f0b7-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f0b7-188">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hirevue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2f0b7-190">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hirevue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2f0b7-192">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hirevue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2f0b7-194">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2f0b7-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hirevue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2f0b7-196">a.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-196">a.</span></span> <span data-ttu-id="2f0b7-197">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2f0b7-198">b.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-198">b.</span></span> <span data-ttu-id="2f0b7-199">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2f0b7-200">c.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-200">c.</span></span> <span data-ttu-id="2f0b7-201">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2f0b7-202">d.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-202">d.</span></span> <span data-ttu-id="2f0b7-203">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-203">Click **Create**.</span></span>
 
### <a name="creating-a-hirevue-test-user"></a><span data-ttu-id="2f0b7-204">HireVue test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2f0b7-204">Creating a HireVue test user</span></span>

<span data-ttu-id="2f0b7-205">Bu bölümde, HireVue içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-205">In this section, you create a user called Britta Simon in HireVue.</span></span> <span data-ttu-id="2f0b7-206">Lütfen çalışmak [HireVue destek ekibi](mailto:samlsupport@hirevue.com) tooadd hello kullanıcılar hello HireVue Platform.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-206">Please work with [HireVue support team](mailto:samlsupport@hirevue.com) tooadd hello users in hello HireVue platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2f0b7-207">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="2f0b7-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2f0b7-208">Bu bölümde, erişim tooHireVue vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHireVue.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="2f0b7-210">**tooassign Britta Simon tooHireVue hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2f0b7-210">**tooassign Britta Simon tooHireVue, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f0b7-211">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="2f0b7-213">Merhaba uygulamalar listesinde **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-213">In hello applications list, select **HireVue**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_app.png) 

3. <span data-ttu-id="2f0b7-215">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="2f0b7-217">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-217">Click **Add** button.</span></span> <span data-ttu-id="2f0b7-218">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="2f0b7-220">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2f0b7-221">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2f0b7-222">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2f0b7-223">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="2f0b7-223">Testing single sign-on</span></span>

<span data-ttu-id="2f0b7-224">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2f0b7-225">Merhaba HireVue hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour HireVue uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f0b7-225">When you click hello HireVue tile in hello Access Panel, you should get automatically signed-on tooyour HireVue application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2f0b7-226">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2f0b7-226">Additional resources</span></span>

* [<span data-ttu-id="2f0b7-227">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="2f0b7-227">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f0b7-228">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="2f0b7-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_203.png

