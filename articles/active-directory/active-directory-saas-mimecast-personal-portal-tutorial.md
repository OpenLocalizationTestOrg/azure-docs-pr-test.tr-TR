---
title: "Öğretici: Azure Active Directory Tümleştirme Mimecast kişisel portalıyla | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Mimecast kişisel Portal arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ee2a8edcab36f295732ac1ebe641ed7fcfc1f2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="494b2-103">Öğretici: Azure Active Directory Tümleştirme Mimecast kişisel portalı ile</span><span class="sxs-lookup"><span data-stu-id="494b2-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="494b2-104">Bu öğreticide, bilgi nasıl toointegrate Mimecast kişisel Portal ile Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="494b2-104">In this tutorial, you learn how toointegrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="494b2-105">Mimecast kişisel Portal Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="494b2-105">Integrating Mimecast Personal Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="494b2-106">Erişim tooMimecast kişisel Portal olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="494b2-106">You can control in Azure AD who has access tooMimecast Personal Portal</span></span>
- <span data-ttu-id="494b2-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooMimecast (çoklu oturum açma) kişisel Portal etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="494b2-107">You can enable your users tooautomatically get signed-on tooMimecast Personal Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="494b2-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="494b2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="494b2-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="494b2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="494b2-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="494b2-110">Prerequisites</span></span>

<span data-ttu-id="494b2-111">tooconfigure Mimecast kişisel Portal ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="494b2-111">tooconfigure Azure AD integration with Mimecast Personal Portal, you need hello following items:</span></span>

- <span data-ttu-id="494b2-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="494b2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="494b2-113">Bir Mimecast kişisel Portal çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="494b2-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="494b2-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="494b2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="494b2-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="494b2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="494b2-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="494b2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="494b2-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="494b2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="494b2-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="494b2-118">Scenario description</span></span>
<span data-ttu-id="494b2-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="494b2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="494b2-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="494b2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="494b2-121">Merhaba Galerisi'nden Mimecast kişisel Portal ekleme</span><span class="sxs-lookup"><span data-stu-id="494b2-121">Adding Mimecast Personal Portal from hello gallery</span></span>
2. <span data-ttu-id="494b2-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="494b2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-hello-gallery"></a><span data-ttu-id="494b2-123">Merhaba Galerisi'nden Mimecast kişisel Portal ekleme</span><span class="sxs-lookup"><span data-stu-id="494b2-123">Adding Mimecast Personal Portal from hello gallery</span></span>
<span data-ttu-id="494b2-124">Azure AD'ye tooconfigure hello tümleştirme Mimecast kişisel portalı tooadd Mimecast kişisel Portal hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="494b2-124">tooconfigure hello integration of Mimecast Personal Portal into Azure AD, you need tooadd Mimecast Personal Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="494b2-125">**tooadd Mimecast kişisel Portal hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="494b2-125">**tooadd Mimecast Personal Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="494b2-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="494b2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="494b2-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="494b2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="494b2-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="494b2-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="494b2-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="494b2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="494b2-133">Merhaba arama kutusuna yazın **Mimecast kişisel Portal**.</span><span class="sxs-lookup"><span data-stu-id="494b2-133">In hello search box, type **Mimecast Personal Portal**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. <span data-ttu-id="494b2-135">Merhaba Sonuçlar panelinde seçin **Mimecast kişisel Portal**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="494b2-135">In hello results panel, select **Mimecast Personal Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="494b2-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="494b2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="494b2-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Mimecast kişisel "Britta Simon" adlı bir test kullanıcı tabanlı Portal ile test etme.</span><span class="sxs-lookup"><span data-stu-id="494b2-138">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="494b2-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Mimecast kişisel portalında tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="494b2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Personal Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="494b2-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve Mimecast kişisel portalında hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="494b2-140">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Personal Portal needs toobe established.</span></span>

<span data-ttu-id="494b2-141">Merhaba hello değeri Mimecast kişisel portalında atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="494b2-141">In Mimecast Personal Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="494b2-142">tooconfigure ve Mimecast kişisel Portal ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="494b2-142">tooconfigure and test Azure AD single sign-on with Mimecast Personal Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="494b2-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="494b2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="494b2-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="494b2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="494b2-145">**[Mimecast kişisel Portal test kullanıcısı oluşturma](#creating-a-mimecast-personal-portal-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Mimecast kişisel Portalı'nda, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="494b2-145">**[Creating a Mimecast Personal Portal test user](#creating-a-mimecast-personal-portal-test-user)** - toohave a counterpart of Britta Simon in Mimecast Personal Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="494b2-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="494b2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="494b2-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="494b2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="494b2-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="494b2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="494b2-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Mimecast kişisel portalı uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="494b2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="494b2-150">**Azure AD çoklu oturum açma tooconfigure Mimecast kişisel portalıyla hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="494b2-150">**tooconfigure Azure AD single sign-on with Mimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="494b2-151">Merhaba hello üzerinde Azure portal'ın **Mimecast kişisel Portal** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="494b2-151">In hello Azure portal, on hello **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="494b2-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="494b2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. <span data-ttu-id="494b2-155">Merhaba üzerinde **Mimecast kişisel Portal etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="494b2-155">On hello **Mimecast Personal Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="494b2-157">a.</span><span class="sxs-lookup"><span data-stu-id="494b2-157">a.</span></span> <span data-ttu-id="494b2-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="494b2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    <span data-ttu-id="494b2-159">b.</span><span class="sxs-lookup"><span data-stu-id="494b2-159">b.</span></span> <span data-ttu-id="494b2-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="494b2-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > <span data-ttu-id="494b2-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="494b2-161">These values are not real.</span></span> <span data-ttu-id="494b2-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="494b2-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="494b2-163">Kişi [Mimecast kişisel Portal istemci destek ekibi](https://www.mimecast.com/customer-success/technical-support/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="494b2-163">Contact [Mimecast Personal Portal Client support team](https://www.mimecast.com/customer-success/technical-support/) tooget these values.</span></span> 
 


4. <span data-ttu-id="494b2-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="494b2-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. <span data-ttu-id="494b2-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="494b2-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="494b2-168">Merhaba üzerinde **Mimecast kişisel Portal Yapılandırması** 'yi tıklatın **Mimecast kişisel Portal Yapılandırma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="494b2-168">On hello **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="494b2-169">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="494b2-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. <span data-ttu-id="494b2-171">Farklı web tarayıcısı penceresinde Mimecast kişisel portalınızı bir yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="494b2-171">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

8. <span data-ttu-id="494b2-172">Çok Git**Hizmetleri \> uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="494b2-172">Go too**Services \> Applications**.</span></span>
   
    <span data-ttu-id="494b2-173">![Uygulamaları](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="494b2-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

9. <span data-ttu-id="494b2-174">Tıklatın **kimlik doğrulaması profilleri**.</span><span class="sxs-lookup"><span data-stu-id="494b2-174">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="494b2-175">![Kimlik doğrulama profilleri](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "kimlik doğrulaması profilleri")</span><span class="sxs-lookup"><span data-stu-id="494b2-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

10. <span data-ttu-id="494b2-176">Tıklatın **yeni kimlik doğrulama profili**.</span><span class="sxs-lookup"><span data-stu-id="494b2-176">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="494b2-177">![Yeni kimlik doğrulama profili](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "yeni kimlik doğrulama profili")</span><span class="sxs-lookup"><span data-stu-id="494b2-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

11. <span data-ttu-id="494b2-178">Merhaba, **kimlik doğrulama profili** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="494b2-178">In hello **Authentication Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="494b2-179">![Kimlik doğrulama profili](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "kimlik doğrulama profili")</span><span class="sxs-lookup"><span data-stu-id="494b2-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="494b2-180">a.</span><span class="sxs-lookup"><span data-stu-id="494b2-180">a.</span></span> <span data-ttu-id="494b2-181">Merhaba, **açıklama** metin kutusuna, yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="494b2-181">In hello **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="494b2-182">b.</span><span class="sxs-lookup"><span data-stu-id="494b2-182">b.</span></span> <span data-ttu-id="494b2-183">Seçin **Mimecast kişisel portalı SAML kimlik doğrulaması zorunlu**.</span><span class="sxs-lookup"><span data-stu-id="494b2-183">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="494b2-184">c.</span><span class="sxs-lookup"><span data-stu-id="494b2-184">c.</span></span> <span data-ttu-id="494b2-185">Olarak **sağlayıcı**seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="494b2-185">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="494b2-186">d.</span><span class="sxs-lookup"><span data-stu-id="494b2-186">d.</span></span> <span data-ttu-id="494b2-187">İçinde **veren URL'si** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="494b2-187">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="494b2-188">e.</span><span class="sxs-lookup"><span data-stu-id="494b2-188">e.</span></span> <span data-ttu-id="494b2-189">İçinde **oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="494b2-189">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="494b2-190">f.</span><span class="sxs-lookup"><span data-stu-id="494b2-190">f.</span></span> <span data-ttu-id="494b2-191">İçinde **oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="494b2-191">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="494b2-192">g.</span><span class="sxs-lookup"><span data-stu-id="494b2-192">g.</span></span> <span data-ttu-id="494b2-193">Açık, **base-64** kodlanmış sertifika Azure portalından kopyalama hello panonuza bunu içerik indirilen Not Defteri'nde ve toohello yapıştırın **kimlik sağlayıcısı sertifikası (meta verileri)** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="494b2-193">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="494b2-194">h.</span><span class="sxs-lookup"><span data-stu-id="494b2-194">h.</span></span> <span data-ttu-id="494b2-195">Seçin **çoklu oturum açmaya izin verme**.</span><span class="sxs-lookup"><span data-stu-id="494b2-195">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="494b2-196">ı.</span><span class="sxs-lookup"><span data-stu-id="494b2-196">i.</span></span> <span data-ttu-id="494b2-197">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="494b2-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="494b2-198">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="494b2-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="494b2-199">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="494b2-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="494b2-200">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="494b2-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="494b2-201">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="494b2-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="494b2-202">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="494b2-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="494b2-204">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="494b2-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="494b2-205">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="494b2-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="494b2-207">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="494b2-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="494b2-209">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="494b2-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="494b2-211">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="494b2-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="494b2-213">a.</span><span class="sxs-lookup"><span data-stu-id="494b2-213">a.</span></span> <span data-ttu-id="494b2-214">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="494b2-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="494b2-215">b.</span><span class="sxs-lookup"><span data-stu-id="494b2-215">b.</span></span> <span data-ttu-id="494b2-216">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="494b2-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="494b2-217">c.</span><span class="sxs-lookup"><span data-stu-id="494b2-217">c.</span></span> <span data-ttu-id="494b2-218">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="494b2-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="494b2-219">d.</span><span class="sxs-lookup"><span data-stu-id="494b2-219">d.</span></span> <span data-ttu-id="494b2-220">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="494b2-220">Click **Create**.</span></span>
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="494b2-221">Mimecast kişisel Portal test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="494b2-221">Creating a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="494b2-222">Mimecast kişisel Portal içine sipariş tooenable Azure AD kullanıcıların toolog bunlar Mimecast kişisel portalına sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="494b2-222">In order tooenable Azure AD users toolog into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="494b2-223">Mimecast kişisel Portal Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="494b2-223">In hello case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="494b2-224">Kullanıcıların oluşturabilmeniz için önce tooregister bir etki alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="494b2-224">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="494b2-225">**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="494b2-225">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="494b2-226">Tooyour üzerinde oturum **Mimecast kişisel Portal** yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="494b2-226">Sign on tooyour **Mimecast Personal Portal** as administrator.</span></span>

2. <span data-ttu-id="494b2-227">Çok Git**dizinleri \> dahili**.</span><span class="sxs-lookup"><span data-stu-id="494b2-227">Go too**Directories \> Internal**.</span></span>
   
    <span data-ttu-id="494b2-228">![Dizinleri](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "dizinleri")</span><span class="sxs-lookup"><span data-stu-id="494b2-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

3. <span data-ttu-id="494b2-229">Tıklatın **kayıt yeni bir etki alanı**.</span><span class="sxs-lookup"><span data-stu-id="494b2-229">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="494b2-230">![Yeni etki alanı kayıt](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "kayıt yeni bir etki alanı")</span><span class="sxs-lookup"><span data-stu-id="494b2-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

4. <span data-ttu-id="494b2-231">Yeni etki alanınızın oluşturulduktan sonra tıklatın **yeni adresi**.</span><span class="sxs-lookup"><span data-stu-id="494b2-231">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="494b2-232">![Yeni bir adres](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "yeni adresi")</span><span class="sxs-lookup"><span data-stu-id="494b2-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

5. <span data-ttu-id="494b2-233">Merhaba yeni adresi iletişim kutusunda, aşağıdaki adımları geçerli Azure hello gerçekleştirmek tooprovision istediğiniz AD hesabı:</span><span class="sxs-lookup"><span data-stu-id="494b2-233">In hello new address dialog, perform hello following steps of a valid Azure AD account you want tooprovision:</span></span>
   
    <span data-ttu-id="494b2-234">![Kaydet](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Kaydet")</span><span class="sxs-lookup"><span data-stu-id="494b2-234">![Save](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="494b2-235">a.</span><span class="sxs-lookup"><span data-stu-id="494b2-235">a.</span></span> <span data-ttu-id="494b2-236">Merhaba, **e-posta adresi** metin kutusuna, türü **e-posta adresi** hello kullanıcı  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="494b2-236">In hello **Email Address** textbox, type **Email Address** of hello user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="494b2-237">b.</span><span class="sxs-lookup"><span data-stu-id="494b2-237">b.</span></span> <span data-ttu-id="494b2-238">Merhaba, **genel adı** metin kutusuna, türü hello **kullanıcıadı** olarak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="494b2-238">In hello **Global Name** textbox, type hello **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="494b2-239">c.</span><span class="sxs-lookup"><span data-stu-id="494b2-239">c.</span></span> <span data-ttu-id="494b2-240">Merhaba, **parola**, ve **parolayı onayla** metin kutuları, türü hello **parola** hello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="494b2-240">In hello **Password**, and **Confirm Password** textboxes, type hello **Password** of hello user.</span></span>
   
    <span data-ttu-id="494b2-241">b.</span><span class="sxs-lookup"><span data-stu-id="494b2-241">b.</span></span> <span data-ttu-id="494b2-242">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="494b2-242">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="494b2-243">Herhangi bir Mimecast kişisel Portal kullanıcı hesabı oluşturma araçlarını veya Mimecast kişisel Portal tooprovision Azure AD kullanıcı hesapları tarafından sağlanan API'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="494b2-243">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="494b2-244">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="494b2-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="494b2-245">Bu bölümde, erişim tooMimecast kişisel Portal vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="494b2-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Personal Portal.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="494b2-247">**tooassign Britta Simon tooMimecast kişisel Portal hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="494b2-247">**tooassign Britta Simon tooMimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="494b2-248">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="494b2-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="494b2-250">Merhaba uygulamalar listesinde **Mimecast kişisel Portal**.</span><span class="sxs-lookup"><span data-stu-id="494b2-250">In hello applications list, select **Mimecast Personal Portal**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. <span data-ttu-id="494b2-252">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="494b2-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="494b2-254">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="494b2-254">Click **Add** button.</span></span> <span data-ttu-id="494b2-255">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="494b2-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="494b2-257">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="494b2-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="494b2-258">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="494b2-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="494b2-259">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="494b2-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="494b2-260">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="494b2-260">Testing single sign-on</span></span>
<span data-ttu-id="494b2-261">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="494b2-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="494b2-262">Merhaba Mimecast kişisel Portal hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Mimecast kişisel Portal uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="494b2-262">When you click hello Mimecast Personal Portal tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Personal Portal application.</span></span> <span data-ttu-id="494b2-263">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="494b2-263">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="494b2-264">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="494b2-264">Additional resources</span></span>

* [<span data-ttu-id="494b2-265">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="494b2-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="494b2-266">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="494b2-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

