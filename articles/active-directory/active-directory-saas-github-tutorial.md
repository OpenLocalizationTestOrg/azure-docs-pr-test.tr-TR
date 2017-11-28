---
title: "Öğretici: Azure Active Directory Tümleştirme github | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve GitHub arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="79b69-103">Öğretici: Azure Active Directory Tümleştirme github</span><span class="sxs-lookup"><span data-stu-id="79b69-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="79b69-104">Bu öğreticide, bilgi nasıl toointegrate GitHub Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="79b69-104">In this tutorial, you learn how toointegrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79b69-105">GitHub Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="79b69-105">Integrating GitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="79b69-106">Erişim tooGitHub sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="79b69-106">You can control in Azure AD who has access tooGitHub</span></span>
- <span data-ttu-id="79b69-107">Kullanıcıların tooautomatically get açan tooGitHub (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="79b69-107">You can enable your users tooautomatically get signed-on tooGitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79b69-108">Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="79b69-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="79b69-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="79b69-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79b69-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="79b69-110">Prerequisites</span></span>

<span data-ttu-id="79b69-111">tooconfigure GitHub ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="79b69-111">tooconfigure Azure AD integration with GitHub, you need hello following items:</span></span>

- <span data-ttu-id="79b69-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="79b69-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79b69-113">Bir GitHub çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="79b69-113">A GitHub single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="79b69-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="79b69-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="79b69-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="79b69-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79b69-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="79b69-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="79b69-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79b69-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="79b69-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="79b69-118">Scenario description</span></span>
<span data-ttu-id="79b69-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="79b69-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79b69-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="79b69-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79b69-121">GitHub hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="79b69-121">Adding GitHub from hello gallery</span></span>
2. <span data-ttu-id="79b69-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="79b69-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-github-from-hello-gallery"></a><span data-ttu-id="79b69-123">GitHub hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="79b69-123">Adding GitHub from hello gallery</span></span>
<span data-ttu-id="79b69-124">Azure AD'ye tooconfigure hello tümleştirme GitHub, tooadd GitHub hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="79b69-124">tooconfigure hello integration of GitHub into Azure AD, you need tooadd GitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="79b69-125">**tooadd hello galeri Github'dan hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="79b69-125">**tooadd GitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="79b69-126">Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="79b69-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="79b69-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="79b69-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="79b69-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="79b69-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="79b69-131">Tıklatın **Ekle** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="79b69-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="79b69-133">Merhaba arama kutusuna yazın **Github.com'u**.</span><span class="sxs-lookup"><span data-stu-id="79b69-133">In hello search box, type **GitHub.com**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. <span data-ttu-id="79b69-135">Merhaba Sonuçlar panelinde seçin **GitHub**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="79b69-135">In hello results panel, select **GitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="79b69-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="79b69-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="79b69-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı GitHub ile test etme.</span><span class="sxs-lookup"><span data-stu-id="79b69-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="79b69-139">Tek toowork'ın oturum açma hangi hello karşılık gelen github tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="79b69-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in GitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="79b69-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve github hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="79b69-140">In other words, a link relationship between an Azure AD user and hello related user in GitHub needs toobe established.</span></span>

<span data-ttu-id="79b69-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** github'da.</span><span class="sxs-lookup"><span data-stu-id="79b69-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in GitHub.</span></span>

<span data-ttu-id="79b69-142">tooconfigure ve GitHub ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="79b69-142">tooconfigure and test Azure AD single sign-on with GitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="79b69-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="79b69-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="79b69-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="79b69-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79b69-145">**[GitHub test kullanıcısı oluşturma](#creating-a-GitHub-test-user)**  -toohave Britta Simon her bağlantılı toohello Azure AD gösterimidir github'da, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="79b69-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - toohave a counterpart of Britta Simon in GitHub that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="79b69-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="79b69-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79b69-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="79b69-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="79b69-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="79b69-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="79b69-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma GitHub uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="79b69-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="79b69-150">**tooconfigure Azure AD çoklu oturum açma github, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="79b69-150">**tooconfigure Azure AD single sign-on with GitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="79b69-151">Merhaba üzerinde hello Azure Yönetim Portalı'nda **GitHub** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="79b69-151">In hello Azure Management portal, on hello **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="79b69-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="79b69-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. <span data-ttu-id="79b69-155">Merhaba üzerinde **GitHub etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79b69-155">On hello **GitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    <span data-ttu-id="79b69-157">a.</span><span class="sxs-lookup"><span data-stu-id="79b69-157">a.</span></span> <span data-ttu-id="79b69-158">Merhaba, **oturum açma URL'si** metin kutusuna, türü hello değeri olarak:`https://github.com/orgs/<entity-id>/sso`</span><span class="sxs-lookup"><span data-stu-id="79b69-158">In hello **Sign-on URL** textbox, type hello value as: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="79b69-159">b.</span><span class="sxs-lookup"><span data-stu-id="79b69-159">b.</span></span> <span data-ttu-id="79b69-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://github.com/orgs/<entity-id>`</span><span class="sxs-lookup"><span data-stu-id="79b69-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="79b69-161">Lütfen bu hello gerçek değerler olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="79b69-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="79b69-162">Bu oturum açma hello gerçek URL ve tanımlayıcıdır değerlerle tooupdate var.</span><span class="sxs-lookup"><span data-stu-id="79b69-162">You have tooupdate these values with hello actual Sing-on URL and Identifier.</span></span> <span data-ttu-id="79b69-163">Burada, toouse hello benzersiz değerini hello tanımlayıcı dizesinde öneririz.</span><span class="sxs-lookup"><span data-stu-id="79b69-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="79b69-164">Bu değerleri tooGitHub yönetici bölüm tooretrieve gidin.</span><span class="sxs-lookup"><span data-stu-id="79b69-164">Go tooGitHub Admin section tooretrieve these values.</span></span> 

4. <span data-ttu-id="79b69-165">Merhaba üzerinde **kullanıcı öznitelikleri** bölümünde, select **kullanıcı tanımlayıcısı** user.mail olarak.</span><span class="sxs-lookup"><span data-stu-id="79b69-165">On hello **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. <span data-ttu-id="79b69-167">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **yeni sertifika oluştur**.</span><span class="sxs-lookup"><span data-stu-id="79b69-167">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. <span data-ttu-id="79b69-169">Merhaba üzerinde **yeni sertifika oluştur** iletişim kutusunda, hello Takvim simgesine tıklayın ve bir **sona erme tarihi**.</span><span class="sxs-lookup"><span data-stu-id="79b69-169">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="79b69-170">Ardından **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="79b69-170">Then click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="79b69-172">Merhaba üzerinde **SAML imzalama sertifikası** bölümünde, select **yeni sertifika etkin hale getirin** tıklatıp **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="79b69-172">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. <span data-ttu-id="79b69-174">Merhaba açılır pencere üzerinde **geçiş sertifikası** penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="79b69-174">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="79b69-176">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="79b69-176">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. <span data-ttu-id="79b69-178">Merhaba üzerinde **GitHub yapılandırma** 'yi tıklatın **yapılandırma GitHub** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="79b69-178">On hello **GitHub Configuration** section, click **Configure GitHub** tooopen **Configure sign-on** window.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. <span data-ttu-id="79b69-181">Farklı web tarayıcısı penceresinde GitHub kuruluş sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="79b69-181">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

12. <span data-ttu-id="79b69-182">Çok gidin**ayarları** tıklatıp **güvenlik**</span><span class="sxs-lookup"><span data-stu-id="79b69-182">Navigate too**Settings** and click **Security**</span></span>

    ![Ayarlar](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. <span data-ttu-id="79b69-184">Merhaba denetleyin **etkinleştirmek SAML kimlik doğrulaması** hello çoklu oturum açma yapılandırma alanları ortaya kutusu.</span><span class="sxs-lookup"><span data-stu-id="79b69-184">Check hello **Enable SAML authentication** box, revealing hello Single Sign-on configuration fields.</span></span> <span data-ttu-id="79b69-185">Ardından, Azure AD yapılandırmasına hello tek oturum açma değeri tooupdate hello tek oturum açma URL'si kullanın.</span><span class="sxs-lookup"><span data-stu-id="79b69-185">Then, use hello single sign-on URL value tooupdate hello Single sign-on URL on Azure AD configuration.</span></span>

    ![Ayarlar](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. <span data-ttu-id="79b69-187">Alanları aşağıdaki hello yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="79b69-187">Configure hello following fields:</span></span>

    <span data-ttu-id="79b69-188">a.</span><span class="sxs-lookup"><span data-stu-id="79b69-188">a.</span></span> <span data-ttu-id="79b69-189">**URL üzerinde oturum**: girin **SAML çoklu oturum açma hizmet URL'si** hello gelen **yapılandırma GitHub** Azure AD bölüm</span><span class="sxs-lookup"><span data-stu-id="79b69-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="79b69-190">b.</span><span class="sxs-lookup"><span data-stu-id="79b69-190">b.</span></span> <span data-ttu-id="79b69-191">**Veren**: girin **SAML varlık kimliği** hello gelen **yapılandırma GitHub** Azure AD bölüm</span><span class="sxs-lookup"><span data-stu-id="79b69-191">**Issuer**: Enter **SAML Entity ID** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="79b69-192">c.</span><span class="sxs-lookup"><span data-stu-id="79b69-192">c.</span></span> <span data-ttu-id="79b69-193">**Ortak sertifika**: açık hello "Sertifika başlayın" ve "Son SERTİFİKAYI" gibi bir not defteri ve kopyalama hello içerik Azure AD'den sertifika indirilir</span><span class="sxs-lookup"><span data-stu-id="79b69-193">**Public Certificate**: Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![Ayarlar](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. <span data-ttu-id="79b69-195">Tıklayın **Test SAML Yapılandırması** tooconfirm, hiçbir doğrulama hataları veya SSO sırasında hatalar.</span><span class="sxs-lookup"><span data-stu-id="79b69-195">Click on **Test SAML configuration** tooconfirm that no validation failures or errors during SSO.</span></span>

    ![Ayarlar](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. <span data-ttu-id="79b69-197">Tıklatın **Kaydet**</span><span class="sxs-lookup"><span data-stu-id="79b69-197">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="79b69-198">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="79b69-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="79b69-199">Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="79b69-199">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="79b69-201">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="79b69-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="79b69-202">Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="79b69-202">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="79b69-204">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="79b69-204">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="79b69-206">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="79b69-206">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="79b69-208">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79b69-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79b69-210">a.</span><span class="sxs-lookup"><span data-stu-id="79b69-210">a.</span></span> <span data-ttu-id="79b69-211">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="79b69-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79b69-212">b.</span><span class="sxs-lookup"><span data-stu-id="79b69-212">b.</span></span> <span data-ttu-id="79b69-213">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="79b69-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="79b69-214">c.</span><span class="sxs-lookup"><span data-stu-id="79b69-214">c.</span></span> <span data-ttu-id="79b69-215">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="79b69-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="79b69-216">d.</span><span class="sxs-lookup"><span data-stu-id="79b69-216">d.</span></span> <span data-ttu-id="79b69-217">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79b69-217">Click **Create**.</span></span> 


### <a name="creating-a-github-test-user"></a><span data-ttu-id="79b69-218">GitHub test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="79b69-218">Creating a GitHub test user</span></span>

<span data-ttu-id="79b69-219">GitHub içine sipariş tooenable Azure AD kullanıcıların toolog bunların GitHub sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="79b69-219">In order tooenable Azure AD users toolog into GitHub, they must be provisioned into GitHub.</span></span>  
<span data-ttu-id="79b69-220">GitHub Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="79b69-220">In hello case of GitHub, provisioning is a manual task.</span></span>

<span data-ttu-id="79b69-221">**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**</span><span class="sxs-lookup"><span data-stu-id="79b69-221">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="79b69-222">İçinde tooyour GitHub şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="79b69-222">Log in tooyour GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="79b69-223">Tıklatın **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="79b69-223">Click **People**.</span></span>

    <span data-ttu-id="79b69-224">![Kişiler](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "kişiler")</span><span class="sxs-lookup"><span data-stu-id="79b69-224">![People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="79b69-225">Tıklatın **davet üye**.</span><span class="sxs-lookup"><span data-stu-id="79b69-225">Click **Invite member**.</span></span>

    <span data-ttu-id="79b69-226">![Kullanıcıları davet](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "kullanıcıları davet et")</span><span class="sxs-lookup"><span data-stu-id="79b69-226">![Invite Users](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="79b69-227">Merhaba üzerinde **davet üye** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79b69-227">On hello **Invite member** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="79b69-228">a.</span><span class="sxs-lookup"><span data-stu-id="79b69-228">a.</span></span> <span data-ttu-id="79b69-229">Merhaba, **e-posta** metin kutusuna, Britta Simon hesabının hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="79b69-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="79b69-230">![Kişileri davet edin](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "kişileri davet edin")</span><span class="sxs-lookup"><span data-stu-id="79b69-230">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>
    
    <span data-ttu-id="79b69-231">b.</span><span class="sxs-lookup"><span data-stu-id="79b69-231">b.</span></span> <span data-ttu-id="79b69-232">Tıklatın **Gönder davet**.</span><span class="sxs-lookup"><span data-stu-id="79b69-232">Click **Send Invitation**.</span></span>

    <span data-ttu-id="79b69-233">![Kişileri davet edin](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "kişileri davet edin")</span><span class="sxs-lookup"><span data-stu-id="79b69-233">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="79b69-234">Hello Azure Active Directory hesap sahibi bir e-posta almak ve bunu etkinleştirilmeden önce bağlantı tooconfirm hesaplarında izleyin.</span><span class="sxs-lookup"><span data-stu-id="79b69-234">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="79b69-235">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="79b69-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="79b69-236">Bu bölümde, kendi erişim tooGitHub vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="79b69-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooGitHub.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="79b69-238">**tooassign Britta Simon tooGitHub hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="79b69-238">**tooassign Britta Simon tooGitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="79b69-239">Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="79b69-239">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="79b69-241">Merhaba uygulamalar listesinde **Github.com'u**.</span><span class="sxs-lookup"><span data-stu-id="79b69-241">In hello applications list, select **GitHub.com**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. <span data-ttu-id="79b69-243">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="79b69-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="79b69-245">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="79b69-245">Click **Add** button.</span></span> <span data-ttu-id="79b69-246">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="79b69-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="79b69-248">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="79b69-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="79b69-249">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="79b69-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79b69-250">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="79b69-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="79b69-251">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="79b69-251">Testing single sign-on</span></span>

<span data-ttu-id="79b69-252">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="79b69-252">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="79b69-253">Merhaba GitHub hello erişim paneli parçasında tıkladığınızda, oturum açma GitHub uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="79b69-253">When you click hello GitHub tile in hello Access Panel, you should get signed-on tooyour GitHub application.</span></span> <span data-ttu-id="79b69-254">Bir kuruluş hesabı ancak gerek toolog sonra kişisel hesabınızla oturum.</span><span class="sxs-lookup"><span data-stu-id="79b69-254">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="79b69-255">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="79b69-255">Additional resources</span></span>

* [<span data-ttu-id="79b69-256">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="79b69-256">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79b69-257">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="79b69-257">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
