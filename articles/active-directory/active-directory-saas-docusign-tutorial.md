---
title: "Öğretici: Azure Active Directory Tümleştirme ile DocuSign | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile DocuSign arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="3aaf8-103">Öğretici: Azure Active Directory Tümleştirme DocuSign ile</span><span class="sxs-lookup"><span data-stu-id="3aaf8-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="3aaf8-104">Bu öğreticide, bilgi nasıl toointegrate DocuSign Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3aaf8-104">In this tutorial, you learn how toointegrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3aaf8-105">DocuSign Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="3aaf8-105">Integrating DocuSign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3aaf8-106">Erişim tooDocuSign sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="3aaf8-106">You can control in Azure AD who has access tooDocuSign</span></span>
- <span data-ttu-id="3aaf8-107">Kullanıcıların tooautomatically get açan tooDocuSign (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="3aaf8-107">You can enable your users tooautomatically get signed-on tooDocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3aaf8-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="3aaf8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3aaf8-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3aaf8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3aaf8-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3aaf8-110">Prerequisites</span></span>

<span data-ttu-id="3aaf8-111">tooconfigure DocuSign ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="3aaf8-111">tooconfigure Azure AD integration with DocuSign, you need hello following items:</span></span>

- <span data-ttu-id="3aaf8-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="3aaf8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3aaf8-113">Bir DocuSign çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="3aaf8-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3aaf8-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3aaf8-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="3aaf8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3aaf8-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3aaf8-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3aaf8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3aaf8-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="3aaf8-118">Scenario description</span></span>
<span data-ttu-id="3aaf8-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3aaf8-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="3aaf8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3aaf8-121">Merhaba Galerisi'nden DocuSign ekleme</span><span class="sxs-lookup"><span data-stu-id="3aaf8-121">Adding DocuSign from hello gallery</span></span>
2. <span data-ttu-id="3aaf8-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="3aaf8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-hello-gallery"></a><span data-ttu-id="3aaf8-123">Merhaba Galerisi'nden DocuSign ekleme</span><span class="sxs-lookup"><span data-stu-id="3aaf8-123">Adding DocuSign from hello gallery</span></span>
<span data-ttu-id="3aaf8-124">Azure AD'ye tooconfigure hello tümleştirme DocuSign, tooadd DocuSign hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-124">tooconfigure hello integration of DocuSign into Azure AD, you need tooadd DocuSign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3aaf8-125">**tooadd DocuSign hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3aaf8-125">**tooadd DocuSign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3aaf8-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3aaf8-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3aaf8-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="3aaf8-131">Tıklatın **yeni uygulama** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="3aaf8-133">Merhaba arama kutusuna yazın **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-133">In hello search box, type **DocuSign**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="3aaf8-135">Merhaba Sonuçlar panelinde seçin **DocuSign**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-135">In hello results panel, select **DocuSign**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3aaf8-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="3aaf8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3aaf8-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı DocuSign ile test etme</span><span class="sxs-lookup"><span data-stu-id="3aaf8-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3aaf8-139">Tek toowork'ın oturum açma hangi hello karşılık gelen DocuSign içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in DocuSign is tooa user in Azure AD.</span></span> <span data-ttu-id="3aaf8-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı DocuSign hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-140">In other words, a link relationship between an Azure AD user and hello related user in DocuSign needs toobe established.</span></span>

<span data-ttu-id="3aaf8-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** DocuSign içinde.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in DocuSign.</span></span>

<span data-ttu-id="3aaf8-142">tooconfigure ve DocuSign ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="3aaf8-142">tooconfigure and test Azure AD single sign-on with DocuSign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3aaf8-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3aaf8-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3aaf8-145">**[DocuSign test kullanıcısı oluşturma](#creating-a-docusign-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir DocuSign içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - toohave a counterpart of Britta Simon in DocuSign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3aaf8-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3aaf8-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3aaf8-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3aaf8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3aaf8-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma DocuSign uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="3aaf8-150">**tooconfigure Azure AD çoklu oturum açma ile DocuSign, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3aaf8-150">**tooconfigure Azure AD single sign-on with DocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="3aaf8-151">Hello hello üzerinde Azure portal'ın **DocuSign** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-151">In hello Azure portal, on hello **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="3aaf8-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="3aaf8-155">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base 64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-155">On hello **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="3aaf8-157">Merhaba üzerinde **DocuSign yapılandırma** bölüm Azure portalının tıklatın **yapılandırma DocuSign** tooopen yapılandırma oturum açma penceresi.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-157">On hello **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** tooopen Configure sign-on window.</span></span> <span data-ttu-id="3aaf8-158">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="3aaf8-158">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="3aaf8-160">Farklı bir web tarayıcısı penceresinde, oturum açma tooyour **DocuSign Yönetici portalı** yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-160">In a different web browser window, login tooyour **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="3aaf8-161">Merhaba Gezinti menüsünde hello sol tıklayın **etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-161">In hello navigation menu on hello left, click **Domains**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırma][51]

7. <span data-ttu-id="3aaf8-163">Merhaba sağ bölmesinde tıklatın **talep etki alanı**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-163">On hello right pane, click **Claim Domain**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırma][52]

8. <span data-ttu-id="3aaf8-165">Merhaba üzerinde **bir etki alanı talep** iletişim kutusunda, hello **etki alanı adı** metin kutusuna, şirket etki alanınızı yazın ve ardından **talep**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-165">On hello **Claim a domain** dialog, in hello **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="3aaf8-166">Merhaba etki alanını doğrulayın ve hello durumu etkin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-166">Make sure that you verify hello domain and hello status is active.</span></span>
   
    ![Çoklu oturum açmayı yapılandırma][53]

9. <span data-ttu-id="3aaf8-168">Merhaba sol tarafındaki menüde tıklatın **kimlik sağlayıcıları**</span><span class="sxs-lookup"><span data-stu-id="3aaf8-168">In menu on hello left side, click **Identity Providers**</span></span>  
   
    ![Çoklu oturum açmayı yapılandırma][54]
10. <span data-ttu-id="3aaf8-170">Merhaba sağ bölmede **kimlik sağlayıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-170">In hello right pane, click **Add Identity Provider**.</span></span> 
   
    ![Çoklu oturum açmayı yapılandırma][55]

11. <span data-ttu-id="3aaf8-172">Merhaba üzerinde **kimlik sağlayıcı ayarları** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3aaf8-172">On hello **Identity Provider Settings** page, perform hello following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırma][56]

    <span data-ttu-id="3aaf8-174">a.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-174">a.</span></span> <span data-ttu-id="3aaf8-175">Merhaba, **adı** metin kutusuna, yapılandırmanızı için benzersiz bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-175">In hello **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="3aaf8-176">Boşluk kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-176">Do not use spaces.</span></span>

    <span data-ttu-id="3aaf8-177">b.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-177">b.</span></span> <span data-ttu-id="3aaf8-178">Yapıştır **SAML varlık kimliği** hello içine **kimlik sağlayıcısı veren** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-178">Paste **SAML Entity ID** into hello **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="3aaf8-179">c.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-179">c.</span></span> <span data-ttu-id="3aaf8-180">Yapıştır **SAML çoklu oturum açma hizmet URL'si** hello içine **kimlik sağlayıcısı oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-180">Paste **SAML Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="3aaf8-181">d.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-181">d.</span></span> <span data-ttu-id="3aaf8-182">Yapıştır **Sign-Out URL** hello içine **kimlik sağlayıcısı oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-182">Paste **Sign-Out URL** into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="3aaf8-183">e.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-183">e.</span></span> <span data-ttu-id="3aaf8-184">Seçin **AuthN isteği oturum**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="3aaf8-185">f.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-185">f.</span></span> <span data-ttu-id="3aaf8-186">Olarak **AuthN gönderme isteği tarafından**seçin **POST**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="3aaf8-187">g.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-187">g.</span></span> <span data-ttu-id="3aaf8-188">Olarak **gönderme oturum kapatma isteği tarafından**seçin **almak**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="3aaf8-189">Merhaba, **özel eşleme özniteliği** bölümünde, hello alan seçin, Azure AD talep ile toomap istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-189">In hello **Custom Attribute Mapping** section, choose hello field you want toomap with Azure AD Claim.</span></span> <span data-ttu-id="3aaf8-190">Bu örnekte, hello **emailaddress** talep hello değeri ile eşleşen **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-190">In this example, hello **emailaddress** claim is mapped with hello value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="3aaf8-191">Bu hello varsayılan talep e-posta talebi için Azure AD'den adıdır.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-191">It is hello default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="3aaf8-192">Kullanım hello uygun **kullanıcı tanımlayıcısı** toomap hello Azure AD tooDocuSign kullanıcı eşlemesi kullanıcıdan.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-192">Use hello appropriate **User identifier** toomap hello user from Azure AD tooDocuSign user mapping.</span></span> <span data-ttu-id="3aaf8-193">Seçin uygun alan hello ve kuruluş ayarlarınızı temel alan hello uygun değeri girin.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-193">Select hello proper Field and enter hello appropriate value based on your organization settings.</span></span>
          
    ![Çoklu oturum açmayı yapılandırma][57]

13. <span data-ttu-id="3aaf8-195">Merhaba, **kimlik sağlayıcısı sertifikası** 'yi tıklatın **sertifika Ekle**ve Azure AD Portalı'ndan indirilen hello sertifika yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-195">In hello **Identity Provider Certificate** section, click **Add Certificate**, and then upload hello certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![Çoklu oturum açmayı yapılandırma][58]

14. <span data-ttu-id="3aaf8-197">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-197">Click **Save**.</span></span>

15. <span data-ttu-id="3aaf8-198">Merhaba, **kimlik sağlayıcıları** 'yi tıklatın **Eylemler**ve ardından **uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-198">In hello **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Çoklu oturum açmayı yapılandırma][59]
 
16. <span data-ttu-id="3aaf8-200">Merhaba, **uç noktalarını görüntüle SAML 2.0** bölümünde **DocuSign Yönetici portalı**, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3aaf8-200">In hello **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform hello following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırma][60]
   
    <span data-ttu-id="3aaf8-202">a.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-202">a.</span></span> <span data-ttu-id="3aaf8-203">Kopyalama hello **servis sağlayıcı veren URL'sini**ve hello yapıştırma **tanımlayıcısı** textbox üzerinde **DocuSign etki alanı ve URL'ler** hello Azure portal aşağıdaki hello bölümü Desen: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-203">Copy hello **Service Provider Issuer URL**, and then paste into hello **Identifier** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="3aaf8-204">b.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-204">b.</span></span> <span data-ttu-id="3aaf8-205">Kopyalama hello **hizmet sağlayıcı oturum açma URL'si**ve hello yapıştırma **oturum üzerinde URL'si** textbox üzerinde **DocuSign etki alanı ve URL'leri** hello Azure portal aşağıdaki hello bölümü Desen: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-205">Copy hello **Service Provider Login URL**, and then paste into hello **Sign On URL** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="3aaf8-207">c.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-207">c.</span></span>  <span data-ttu-id="3aaf8-208">Tıklatın **Kapat**</span><span class="sxs-lookup"><span data-stu-id="3aaf8-208">Click **Close**</span></span>
    
17. <span data-ttu-id="3aaf8-209">Hello Azure portal, tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-209">On hello Azure portal, click **Save**.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="3aaf8-211">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="3aaf8-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3aaf8-212">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3aaf8-213">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3aaf8-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3aaf8-214">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3aaf8-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="3aaf8-215">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="3aaf8-217">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3aaf8-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3aaf8-218">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3aaf8-220">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3aaf8-222">Merhaba iletişim Hello üstünde tıklatın **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3aaf8-224">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3aaf8-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3aaf8-226">a.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-226">a.</span></span> <span data-ttu-id="3aaf8-227">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3aaf8-228">b.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-228">b.</span></span> <span data-ttu-id="3aaf8-229">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3aaf8-230">c.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-230">c.</span></span> <span data-ttu-id="3aaf8-231">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3aaf8-232">d.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-232">d.</span></span> <span data-ttu-id="3aaf8-233">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="3aaf8-234">DocuSign test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3aaf8-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="3aaf8-235">Uygulamanızın desteklediği **zaman kullanıcı hazırlama, sadece** ve kimlik doğrulama kullanıcılar hello uygulamada otomatik olarak oluşturulduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-235">Application supports **Just in time user provisioning** and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3aaf8-236">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="3aaf8-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3aaf8-237">Bu bölümde, kendi erişim tooDocuSign vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooDocuSign.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="3aaf8-239">**tooassign Britta Simon tooDocuSign hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3aaf8-239">**tooassign Britta Simon tooDocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="3aaf8-240">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="3aaf8-242">Merhaba uygulamalar listesinde **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-242">In hello applications list, select **DocuSign**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="3aaf8-244">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="3aaf8-246">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-246">Click **Add** button.</span></span> <span data-ttu-id="3aaf8-247">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="3aaf8-249">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3aaf8-250">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3aaf8-251">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3aaf8-252">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="3aaf8-252">Testing single sign-on</span></span>

<span data-ttu-id="3aaf8-253">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3aaf8-254">Merhaba DocuSign hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour DocuSign uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3aaf8-254">When you click hello DocuSign tile in hello Access Panel, you should get automatically signed-on tooyour DocuSign application.</span></span>
<span data-ttu-id="3aaf8-255">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3aaf8-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3aaf8-256">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3aaf8-256">Additional resources</span></span>

* [<span data-ttu-id="3aaf8-257">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="3aaf8-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3aaf8-258">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="3aaf8-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="3aaf8-259">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="3aaf8-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

