---
title: "Öğretici: Azure Active Directory Tümleştirme Adobe Creative bulut ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Adobe Creative bulut arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="2de03-103">Öğretici: Adobe Creative bulut Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="2de03-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="2de03-104">Bu öğreticide, bilgi Adobe Creative toointegrate bulut nasıl Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="2de03-104">In this tutorial, you learn how toointegrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2de03-105">Adobe Creative bulut Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="2de03-105">Integrating Adobe Creative Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2de03-106">Erişim tooAdobe yaratıcı bulut sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2de03-106">You can control in Azure AD who has access tooAdobe Creative Cloud</span></span>
- <span data-ttu-id="2de03-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooAdobe (çoklu oturum açma) yaratıcı bulut etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2de03-107">You can enable your users tooautomatically get signed-on tooAdobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2de03-108">Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2de03-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="2de03-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2de03-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2de03-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2de03-110">Prerequisites</span></span>

<span data-ttu-id="2de03-111">tooconfigure Adobe Creative bulut ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2de03-111">tooconfigure Azure AD integration with Adobe Creative Cloud, you need hello following items:</span></span>

- <span data-ttu-id="2de03-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="2de03-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2de03-113">Bir Adobe Creative bulut çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="2de03-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2de03-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="2de03-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2de03-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="2de03-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2de03-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2de03-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2de03-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2de03-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2de03-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="2de03-118">Scenario description</span></span>
<span data-ttu-id="2de03-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="2de03-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2de03-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="2de03-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2de03-121">Adobe Creative bulut hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="2de03-121">Adding Adobe Creative Cloud from hello gallery</span></span>
2. <span data-ttu-id="2de03-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2de03-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a><span data-ttu-id="2de03-123">Adobe Creative bulut hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="2de03-123">Adding Adobe Creative Cloud from hello gallery</span></span>
<span data-ttu-id="2de03-124">Azure AD'ye tooconfigure hello tümleştirme Adobe Creative bulutun tooadd Adobe Creative bulut hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="2de03-124">tooconfigure hello integration of Adobe Creative Cloud into Azure AD, you need tooadd Adobe Creative Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2de03-125">**tooadd Adobe Creative bulut hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2de03-125">**tooadd Adobe Creative Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2de03-126">Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2de03-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2de03-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="2de03-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2de03-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2de03-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="2de03-131">Tıklatın **Ekle** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2de03-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="2de03-133">Merhaba arama kutusuna yazın **Adobe Creative bulut**.</span><span class="sxs-lookup"><span data-stu-id="2de03-133">In hello search box, type **Adobe Creative Cloud**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="2de03-135">Merhaba Sonuçlar panelinde seçin **Adobe Creative bulut**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="2de03-135">In hello results panel, select **Adobe Creative Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2de03-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2de03-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2de03-138">Bu bölümde, yapılandırmak ve Adobe Creative bulut "Britta Simon" adlı bir test kullanıcı tabanlı Azure AD çoklu oturum açmayı sınayın.</span><span class="sxs-lookup"><span data-stu-id="2de03-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2de03-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Adobe Creative bulutta tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="2de03-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Creative Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="2de03-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve Adobe Creative bulutta hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2de03-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Creative Cloud needs toobe established.</span></span>

<span data-ttu-id="2de03-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Adobe Creative bulutta.</span><span class="sxs-lookup"><span data-stu-id="2de03-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="2de03-142">tooconfigure ve Adobe Creative bulut ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2de03-142">tooconfigure and test Azure AD single sign-on with Adobe Creative Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2de03-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="2de03-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2de03-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="2de03-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2de03-145">**[Adobe Creative bulut test kullanıcısı oluşturma](#creating-an-adobe-creative-cloud-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir Adobe Creative bulutta Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="2de03-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - toohave a counterpart of Britta Simon in Adobe Creative Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="2de03-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2de03-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2de03-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="2de03-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2de03-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2de03-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2de03-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma, Adobe Creative bulut uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2de03-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="2de03-150">**Azure AD çoklu oturum açma tooconfigure Adobe Creative bulutla hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2de03-150">**tooconfigure Azure AD single sign-on with Adobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="2de03-151">Hello üzerinde hello Azure Yönetim Portalı'nda **Adobe Creative bulut** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="2de03-151">In hello Azure Management portal, on hello **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="2de03-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2de03-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="2de03-155">Merhaba üzerinde **Adobe Creative bulut etki alanı ve URL'leri** bölümünde, hello tooconfigure hello uygulamada istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="2de03-155">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="2de03-157">a.</span><span class="sxs-lookup"><span data-stu-id="2de03-157">a.</span></span> <span data-ttu-id="2de03-158">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello değeri olarak:`https://www.okta.com/saml2/service-provider/<token>`</span><span class="sxs-lookup"><span data-stu-id="2de03-158">In hello **Identifier** textbox, type hello value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="2de03-159">b.</span><span class="sxs-lookup"><span data-stu-id="2de03-159">b.</span></span> <span data-ttu-id="2de03-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="2de03-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2de03-161">Lütfen bu hello gerçek değerler olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2de03-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="2de03-162">Tooupdate hello gerçek tanımlayıcısı ve yanıt URL'si ile bu değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="2de03-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="2de03-163">Burada, toouse hello benzersiz değerini hello tanımlayıcı dizesinde öneririz.</span><span class="sxs-lookup"><span data-stu-id="2de03-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="2de03-164">Bir kullanıcı toocreate el ile gerekiyorsa, toocontact hello Adobe Creative bulut destek ekibi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2de03-164">If you need toocreate an user manually, you need toocontact hello Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="2de03-165">Merhaba üzerinde **Adobe Creative bulut etki alanı ve URL'leri** bölümünde, hello tooconfigure hello uygulamada istiyorsanız aşağıdaki adımları gerçekleştirin **SP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="2de03-165">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="2de03-167">a.</span><span class="sxs-lookup"><span data-stu-id="2de03-167">a.</span></span> <span data-ttu-id="2de03-168">Tıklatın hello üzerinde **Göster Gelişmiş URL ayarları** seçeneği</span><span class="sxs-lookup"><span data-stu-id="2de03-168">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="2de03-169">b.</span><span class="sxs-lookup"><span data-stu-id="2de03-169">b.</span></span> <span data-ttu-id="2de03-170">Merhaba, **oturum açma URL'si** metin kutusuna, türü hello değeri olarak:`https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="2de03-170">In hello **Sign-on URL** textbox, type hello value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="2de03-171">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2de03-171">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="2de03-173">Merhaba üzerinde **Adobe Creative bulut Yapılandırması** 'yi tıklatın **Adobe Creative bulut yapılandırma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="2de03-173">On hello **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2de03-174">Lütfen hello kopyalayın **SAML varlık kimliği** ve **SAML SSO hizmet URL'si** hızlı başvuru bölümünden.</span><span class="sxs-lookup"><span data-stu-id="2de03-174">Please copy hello **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="2de03-176">Bir farklı web tarayıcısı penceresinde, bir yönetici olarak oturum açma tooyour Adobe Creative bulut Kiracı.</span><span class="sxs-lookup"><span data-stu-id="2de03-176">In a different web browser window, sign-on tooyour Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="2de03-177">Çok Git**kimlik** sol gezinti bölmesinde hello ve etki alanınızı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2de03-177">Go too**Identity** on hello left navigation pane and click your domain.</span></span> <span data-ttu-id="2de03-178">Merhaba aşağıdaki adımları gerçekleştirin **tek oturum yapılandırması gerekli** bölümü.</span><span class="sxs-lookup"><span data-stu-id="2de03-178">Then perform hello following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="2de03-179">![Ayarları](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="2de03-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="2de03-180">Tıklatın **Gözat** tooupload hello sertifika çok Azure AD'den indirilen**IDP sertifika**.</span><span class="sxs-lookup"><span data-stu-id="2de03-180">Click **Browse** tooupload hello downloaded certificate from Azure AD too**IDP Certificate**.</span></span>

10. <span data-ttu-id="2de03-181">Merhaba, **IDP veren** hello değerini put textbox **SAML varlık kimliği** öğesinden kopyalanan **yapılandırma oturum açma** Azure portalı bölümünde.</span><span class="sxs-lookup"><span data-stu-id="2de03-181">In hello **IDP issuer** textbox, put hello value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="2de03-182">Merhaba, **IDP oturum açma URL'si** hello değerini put textbox **SAML SSO hizmet URL'si** öğesinden kopyalanan **yapılandırma oturum açma** Azure portalı bölümünde.</span><span class="sxs-lookup"><span data-stu-id="2de03-182">In hello **IDP Login URL** textbox, put hello value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="2de03-183">Seçin **HTTP - yeniden yönlendirme** olarak **IDP bağlama**.</span><span class="sxs-lookup"><span data-stu-id="2de03-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="2de03-184">Seçin **e-posta adresi** olarak **kullanıcı oturum açma ayarı**.</span><span class="sxs-lookup"><span data-stu-id="2de03-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="2de03-185">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2de03-185">Click **Save** button.</span></span>

15. <span data-ttu-id="2de03-186">Merhaba Pano artık hello XML sunmak **"Meta veriler indirme"** dosya.</span><span class="sxs-lookup"><span data-stu-id="2de03-186">hello dashboard will now present hello XML **"Download Metadata"** file.</span></span> <span data-ttu-id="2de03-187">Adobe EntityDescriptor URL ve AssertionConsumerService URL'sini içerir.</span><span class="sxs-lookup"><span data-stu-id="2de03-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="2de03-188">Lütfen hello dosyasını açın ve hello Azure AD uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2de03-188">Please open hello file and configure them in hello Azure AD application.</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="2de03-191">a.</span><span class="sxs-lookup"><span data-stu-id="2de03-191">a.</span></span> <span data-ttu-id="2de03-192">Kullanım hello EntityDescriptor değeri Adobe için sağlanan **tanımlayıcısı** hello üzerinde **uygulama ayarlarını yapılandır** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2de03-192">Use hello EntityDescriptor value Adobe provided you for **Identifier** on hello **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="2de03-193">b.</span><span class="sxs-lookup"><span data-stu-id="2de03-193">b.</span></span> <span data-ttu-id="2de03-194">Kullanım hello AssertionConsumerService değeri Adobe için sağlanan **yanıt URL'si** hello üzerinde **uygulama ayarlarını yapılandır** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2de03-194">Use hello AssertionConsumerService value Adobe provided you for **Reply URL** on hello **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2de03-195">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2de03-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="2de03-196">Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="2de03-196">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="2de03-198">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2de03-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2de03-199">Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2de03-199">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2de03-201">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="2de03-201">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2de03-203">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2de03-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2de03-205">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2de03-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2de03-207">a.</span><span class="sxs-lookup"><span data-stu-id="2de03-207">a.</span></span> <span data-ttu-id="2de03-208">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2de03-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2de03-209">b.</span><span class="sxs-lookup"><span data-stu-id="2de03-209">b.</span></span> <span data-ttu-id="2de03-210">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="2de03-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2de03-211">c.</span><span class="sxs-lookup"><span data-stu-id="2de03-211">c.</span></span> <span data-ttu-id="2de03-212">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="2de03-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2de03-213">d.</span><span class="sxs-lookup"><span data-stu-id="2de03-213">d.</span></span> <span data-ttu-id="2de03-214">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2de03-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="2de03-215">Adobe Creative bulut test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2de03-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="2de03-216">Adobe Creative buluta sipariş tooenable Azure AD kullanıcıların toolog bunlar Adobe Creative bulutunu sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2de03-216">In order tooenable Azure AD users toolog into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="2de03-217">Adobe Creative bulut Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="2de03-217">In hello case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="2de03-218">**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**</span><span class="sxs-lookup"><span data-stu-id="2de03-218">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="2de03-219">Tooyour içinde Adobe Creative bulut şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2de03-219">Log in tooyour Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="2de03-220">Tıklatın **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="2de03-220">Click **People**.</span></span>

    <span data-ttu-id="2de03-221">![Kişiler](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "kişiler")</span><span class="sxs-lookup"><span data-stu-id="2de03-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="2de03-222">Tıklatın **davet kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="2de03-222">Click **Invite User**.</span></span>

    <span data-ttu-id="2de03-223">![Kullanıcıları davet](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "kullanıcıları davet et")</span><span class="sxs-lookup"><span data-stu-id="2de03-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="2de03-224">Merhaba üzerinde **kişileri davet** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2de03-224">On hello **Invite People** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="2de03-225">![Kişileri davet edin](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "kişileri davet edin")</span><span class="sxs-lookup"><span data-stu-id="2de03-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="2de03-226">a.</span><span class="sxs-lookup"><span data-stu-id="2de03-226">a.</span></span> <span data-ttu-id="2de03-227">Merhaba, **e-posta** metin kutusuna, Britta Simon hesabının hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="2de03-227">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="2de03-228">b.</span><span class="sxs-lookup"><span data-stu-id="2de03-228">b.</span></span> <span data-ttu-id="2de03-229">Tıklatın **davet**.</span><span class="sxs-lookup"><span data-stu-id="2de03-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2de03-230">Hello Azure Active Directory hesap sahibi bir e-posta almak ve bunu etkinleştirilmeden önce bağlantı tooconfirm hesaplarında izleyin.</span><span class="sxs-lookup"><span data-stu-id="2de03-230">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2de03-231">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="2de03-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2de03-232">Bu bölümde, kendi erişim tooAdobe yaratıcı bulut vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2de03-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAdobe Creative Cloud.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="2de03-234">**tooassign Britta Simon tooAdobe yaratıcı bulut hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2de03-234">**tooassign Britta Simon tooAdobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="2de03-235">Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2de03-235">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="2de03-237">Merhaba uygulamalar listesinde **Adobe Creative bulut**.</span><span class="sxs-lookup"><span data-stu-id="2de03-237">In hello applications list, select **Adobe Creative Cloud**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="2de03-239">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="2de03-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="2de03-241">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2de03-241">Click **Add** button.</span></span> <span data-ttu-id="2de03-242">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2de03-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="2de03-244">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="2de03-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2de03-245">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2de03-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2de03-246">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2de03-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2de03-247">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="2de03-247">Testing single sign-on</span></span>

<span data-ttu-id="2de03-248">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="2de03-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2de03-249">Merhaba Adobe Creative bulut hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Adobe Creative bulut uygulaması almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2de03-249">When you click hello Adobe Creative Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2de03-250">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2de03-250">Additional resources</span></span>

* [<span data-ttu-id="2de03-251">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="2de03-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2de03-252">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="2de03-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png