---
title: "Öğretici: Azure Active Directory Tümleştirme Mimecast Yönetici Konsolu ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Mimecast Yönetici Konsolu arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 5a04a5abd9ff30d484bce0a5c97a1d3e48b69e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="e7e61-103">Öğretici: Azure Active Directory Tümleştirme Mimecast Yönetici Konsolu ile</span><span class="sxs-lookup"><span data-stu-id="e7e61-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="e7e61-104">Bu öğreticide, bilgi toointegrate Mimecast Yönetici Konsolu nasıl Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="e7e61-104">In this tutorial, you learn how toointegrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e7e61-105">Mimecast Yönetici Konsolu Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e7e61-105">Integrating Mimecast Admin Console with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e7e61-106">Erişim tooMimecast Yönetici konsolunda olan Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7e61-106">You can control in Azure AD who has access tooMimecast Admin Console.</span></span>
- <span data-ttu-id="e7e61-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooMimecast Yönetim Konsolu (çoklu oturum açma) etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7e61-107">You can enable your users tooautomatically get signed-on tooMimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e7e61-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="e7e61-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="e7e61-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e7e61-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7e61-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e7e61-110">Prerequisites</span></span>

<span data-ttu-id="e7e61-111">tooconfigure Mimecast Yönetim Konsolu ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e7e61-111">tooconfigure Azure AD integration with Mimecast Admin Console, you need hello following items:</span></span>

- <span data-ttu-id="e7e61-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e7e61-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e7e61-113">Bir Mimecast Yönetici Konsolu çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="e7e61-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e7e61-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e7e61-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e7e61-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="e7e61-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e7e61-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e7e61-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e7e61-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7e61-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e7e61-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e7e61-118">Scenario description</span></span>
<span data-ttu-id="e7e61-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e7e61-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e7e61-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e7e61-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e7e61-121">Hello Galerisi'nden Mimecast Yönetici Konsolu'nu ekleme</span><span class="sxs-lookup"><span data-stu-id="e7e61-121">Adding Mimecast Admin Console from hello gallery</span></span>
2. <span data-ttu-id="e7e61-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e7e61-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-hello-gallery"></a><span data-ttu-id="e7e61-123">Hello Galerisi'nden Mimecast Yönetici Konsolu'nu ekleme</span><span class="sxs-lookup"><span data-stu-id="e7e61-123">Adding Mimecast Admin Console from hello gallery</span></span>
<span data-ttu-id="e7e61-124">Azure AD'ye tooconfigure hello tümleştirme Mimecast yönetici konsolunun tooadd Mimecast Yönetici Konsolu hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7e61-124">tooconfigure hello integration of Mimecast Admin Console into Azure AD, you need tooadd Mimecast Admin Console from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e7e61-125">**tooadd Mimecast Yönetici Konsolu hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e7e61-125">**tooadd Mimecast Admin Console from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7e61-126">Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e7e61-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="e7e61-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e7e61-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e7e61-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e7e61-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="e7e61-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e7e61-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="e7e61-133">Hello arama kutusuna yazın **Mimecast Yönetici Konsolu**seçin **Mimecast Yönetici Konsolu** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e7e61-133">In hello search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde Mimecast Yönetim Konsolu](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e7e61-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e7e61-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e7e61-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Mimecast Yönetici Konsolu ile test etme.</span><span class="sxs-lookup"><span data-stu-id="e7e61-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e7e61-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Mimecast Yönetici konsolunda tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7e61-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Admin Console is tooa user in Azure AD.</span></span> <span data-ttu-id="e7e61-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve Mimecast Yönetici konsolunda hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7e61-138">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Admin Console needs toobe established.</span></span>

<span data-ttu-id="e7e61-139">Merhaba hello değeri Mimecast Yönetici konsolunda atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="e7e61-139">In Mimecast Admin Console, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e7e61-140">tooconfigure ve Mimecast Yönetici Konsolu ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e7e61-140">tooconfigure and test Azure AD single sign-on with Mimecast Admin Console, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e7e61-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="e7e61-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e7e61-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="e7e61-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e7e61-143">**[Mimecast Yönetici Konsolu test kullanıcısı oluşturma](#create-a-mimecast-admin-console-test-user) ** -toohave karşılık gelen, Britta Simon Mimecast Yönetici konsolunda, kullanıcı bağlantılı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="e7e61-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - toohave a counterpart of Britta Simon in Mimecast Admin Console that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e7e61-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e7e61-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e7e61-145">**[Test çoklu oturum açma](#test-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="e7e61-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e7e61-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e7e61-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e7e61-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Mimecast Yönetici Konsolu uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e7e61-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="e7e61-148">**Azure AD çoklu oturum açma tooconfigure Mimecast yönetim konsoluyla hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e7e61-148">**tooconfigure Azure AD single sign-on with Mimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7e61-149">Merhaba hello üzerinde Azure portal'ın **Mimecast Yönetici Konsolu** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e7e61-149">In hello Azure portal, on hello **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="e7e61-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e7e61-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. <span data-ttu-id="e7e61-153">Merhaba üzerinde **Mimecast Yönetici Konsolu etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e7e61-153">On hello **Mimecast Admin Console Domain and URLs** section, perform hello following steps:</span></span>

    ![Mimecast Yönetici Konsolu etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="e7e61-155">Merhaba, **oturum açma URL'si** metin kutusuna, türü hello URL'si:</span><span class="sxs-lookup"><span data-stu-id="e7e61-155">In hello **Sign-on URL** textbox, type hello URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="e7e61-156">Merhaba oturum açma URL'si belirli bölgedir.</span><span class="sxs-lookup"><span data-stu-id="e7e61-156">hello sign on URL is region specific.</span></span>

4. <span data-ttu-id="e7e61-157">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e7e61-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. <span data-ttu-id="e7e61-159">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e7e61-159">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e7e61-161">Merhaba üzerinde **Mimecast Yönetici Konsolu Yapılandırması** 'yi tıklatın **Mimecast Yönetim Konsolu** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e7e61-161">On hello **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e7e61-162">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="e7e61-162">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Mimecast Yönetici Konsolu yapılandırması](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. <span data-ttu-id="e7e61-164">Farklı web tarayıcısı penceresinde Mimecast Yönetici konsolunda bir yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e7e61-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

8. <span data-ttu-id="e7e61-165">Çok Git**Hizmetleri \> uygulama**.</span><span class="sxs-lookup"><span data-stu-id="e7e61-165">Go too**Services \> Application**.</span></span>

    <span data-ttu-id="e7e61-166">![Hizmetleri](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Hizmetleri")</span><span class="sxs-lookup"><span data-stu-id="e7e61-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

9. <span data-ttu-id="e7e61-167">Tıklatın **kimlik doğrulaması profilleri**.</span><span class="sxs-lookup"><span data-stu-id="e7e61-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="e7e61-168">![Kimlik doğrulama profilleri](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "kimlik doğrulaması profilleri")</span><span class="sxs-lookup"><span data-stu-id="e7e61-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
10. <span data-ttu-id="e7e61-169">Tıklatın **yeni kimlik doğrulama profili**.</span><span class="sxs-lookup"><span data-stu-id="e7e61-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="e7e61-170">![Yeni kimlik doğrulama profilleri](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "yeni kimlik doğrulama profilleri")</span><span class="sxs-lookup"><span data-stu-id="e7e61-170">![New Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

11. <span data-ttu-id="e7e61-171">Merhaba, **kimlik doğrulama profili** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e7e61-171">In hello **Authentication Profile** section, perform hello following steps:</span></span>

    <span data-ttu-id="e7e61-172">![Kimlik doğrulama profili](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "kimlik doğrulama profili")</span><span class="sxs-lookup"><span data-stu-id="e7e61-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="e7e61-173">a.</span><span class="sxs-lookup"><span data-stu-id="e7e61-173">a.</span></span> <span data-ttu-id="e7e61-174">Merhaba, **açıklama** metin kutusuna, yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="e7e61-174">In hello **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="e7e61-175">b.</span><span class="sxs-lookup"><span data-stu-id="e7e61-175">b.</span></span> <span data-ttu-id="e7e61-176">Seçin **Mimecast Yönetici Konsolu için SAML kimlik doğrulaması zorunlu**.</span><span class="sxs-lookup"><span data-stu-id="e7e61-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="e7e61-177">c.</span><span class="sxs-lookup"><span data-stu-id="e7e61-177">c.</span></span> <span data-ttu-id="e7e61-178">Olarak **sağlayıcı**seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e7e61-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="e7e61-179">d.</span><span class="sxs-lookup"><span data-stu-id="e7e61-179">d.</span></span> <span data-ttu-id="e7e61-180">Yapıştır **SAML varlık kimliği**, hello hello Azure portal ' Kopyalanan **veren URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="e7e61-180">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="e7e61-181">e.</span><span class="sxs-lookup"><span data-stu-id="e7e61-181">e.</span></span> <span data-ttu-id="e7e61-182">Yapıştır **SAML çoklu oturum açma hizmet URL'si**, hello hello Azure portal ' Kopyalanan **oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="e7e61-182">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Login URL** textbox.</span></span>

    <span data-ttu-id="e7e61-183">f.</span><span class="sxs-lookup"><span data-stu-id="e7e61-183">f.</span></span> <span data-ttu-id="e7e61-184">Yapıştır **SAML çoklu oturum açma hizmet URL'si**, hello hello Azure portal ' Kopyalanan **oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="e7e61-184">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="e7e61-185">Merhaba Mimecast Yönetici Konsolu hello aynı hello oturum açma URL'si değeri ve hello oturum kapatma URL'si değeri olursunuz.</span><span class="sxs-lookup"><span data-stu-id="e7e61-185">hello Login URL value and hello Logout URL value are for hello Mimecast Admin Console hello same.</span></span>
    
    <span data-ttu-id="e7e61-186">g.</span><span class="sxs-lookup"><span data-stu-id="e7e61-186">g.</span></span> <span data-ttu-id="e7e61-187">Base-64 sertifikanızı Not Defteri'nde, Azure Portalı'ndan indirilen açık hello ilk satırı Kaldır ("*--*") ve hello son satır ("*--*"), bu içerik kalan kopyalama hello Pano, içine toohello yapıştırın **kimlik sağlayıcısı sertifikası (meta verileri)** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="e7e61-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove hello first line (“*--*“) and hello last line (“*--*“), copy hello remaining content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="e7e61-188">h.</span><span class="sxs-lookup"><span data-stu-id="e7e61-188">h.</span></span> <span data-ttu-id="e7e61-189">Seçin **çoklu oturum açmaya izin verme**.</span><span class="sxs-lookup"><span data-stu-id="e7e61-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="e7e61-190">ı.</span><span class="sxs-lookup"><span data-stu-id="e7e61-190">i.</span></span> <span data-ttu-id="e7e61-191">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e7e61-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e7e61-192">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e7e61-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e7e61-193">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="e7e61-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e7e61-194">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e7e61-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e7e61-195">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e7e61-195">Create an Azure AD test user</span></span>

<span data-ttu-id="e7e61-196">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="e7e61-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="e7e61-198">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e7e61-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7e61-199">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e7e61-199">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e7e61-201">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e7e61-201">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e7e61-203">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="e7e61-203">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e7e61-205">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e7e61-205">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e7e61-207">a.</span><span class="sxs-lookup"><span data-stu-id="e7e61-207">a.</span></span> <span data-ttu-id="e7e61-208">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7e61-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e7e61-209">b.</span><span class="sxs-lookup"><span data-stu-id="e7e61-209">b.</span></span> <span data-ttu-id="e7e61-210">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="e7e61-210">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="e7e61-211">c.</span><span class="sxs-lookup"><span data-stu-id="e7e61-211">c.</span></span> <span data-ttu-id="e7e61-212">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="e7e61-212">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="e7e61-213">d.</span><span class="sxs-lookup"><span data-stu-id="e7e61-213">d.</span></span> <span data-ttu-id="e7e61-214">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e7e61-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="e7e61-215">Mimecast Yönetici Konsolu test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e7e61-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="e7e61-216">Mimecast yönetici konsoluna sipariş tooenable Azure AD kullanıcıların toolog bunlar Mimecast Yönetici konsolunda sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e7e61-216">In order tooenable Azure AD users toolog into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="e7e61-217">Mimecast Yönetici Konsolu Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="e7e61-217">In hello case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="e7e61-218">Kullanıcıların oluşturabilmeniz için önce tooregister bir etki alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7e61-218">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="e7e61-219">**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e7e61-219">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7e61-220">Tooyour üzerinde oturum **Mimecast Yönetici Konsolu** yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="e7e61-220">Sign on tooyour **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="e7e61-221">Çok Git**dizinleri \> dahili**.</span><span class="sxs-lookup"><span data-stu-id="e7e61-221">Go too**Directories \> Internal**.</span></span>
   
   <span data-ttu-id="e7e61-222">![Dizinleri](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "dizinleri")</span><span class="sxs-lookup"><span data-stu-id="e7e61-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
3. <span data-ttu-id="e7e61-223">Tıklatın **kayıt yeni bir etki alanı**.</span><span class="sxs-lookup"><span data-stu-id="e7e61-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="e7e61-224">![Yeni etki alanı kayıt](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "kayıt yeni bir etki alanı")</span><span class="sxs-lookup"><span data-stu-id="e7e61-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="e7e61-225">Yeni etki alanınızın oluşturulduktan sonra tıklatın **yeni adresi**.</span><span class="sxs-lookup"><span data-stu-id="e7e61-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="e7e61-226">![Yeni bir adres](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "yeni adresi")</span><span class="sxs-lookup"><span data-stu-id="e7e61-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
5. <span data-ttu-id="e7e61-227">Merhaba yeni adresi iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e7e61-227">In hello new address dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="e7e61-228">![Kaydet](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Kaydet")</span><span class="sxs-lookup"><span data-stu-id="e7e61-228">![Save](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="e7e61-229">a.</span><span class="sxs-lookup"><span data-stu-id="e7e61-229">a.</span></span> <span data-ttu-id="e7e61-230">Türü hello **e-posta adresi**, **genel adı**, **parola**, ve **parolayı onayla** öznitelikleri geçerli bir Azure ad hesabına istiyor metin kutuları hello içine tooprovision ilgili.</span><span class="sxs-lookup"><span data-stu-id="e7e61-230">Type hello **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span>

   <span data-ttu-id="e7e61-231">b.</span><span class="sxs-lookup"><span data-stu-id="e7e61-231">b.</span></span> <span data-ttu-id="e7e61-232">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e7e61-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="e7e61-233">Herhangi bir Mimecast Yönetim Konsolu kullanıcı hesabı oluşturma araçlarını veya Mimecast Yönetici Konsolu tooprovision Azure AD kullanıcı hesapları tarafından sağlanan API'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7e61-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console tooprovision Azure AD user accounts.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e7e61-234">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="e7e61-234">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e7e61-235">Bu bölümde, erişim tooMimecast Yönetici Konsolu vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e7e61-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Admin Console.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="e7e61-237">**tooassign Britta Simon tooMimecast yönetici konsolunu hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e7e61-237">**tooassign Britta Simon tooMimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7e61-238">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e7e61-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e7e61-240">Merhaba uygulamalar listesinde **Mimecast Yönetici Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="e7e61-240">In hello applications list, select **Mimecast Admin Console**.</span></span>

    ![Hello Mimecast yönetici konsolunu bağlantısı hello uygulamalar listesinde](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. <span data-ttu-id="e7e61-242">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e7e61-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="e7e61-244">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e7e61-244">Click **Add** button.</span></span> <span data-ttu-id="e7e61-245">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e7e61-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="e7e61-247">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e7e61-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e7e61-248">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e7e61-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e7e61-249">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e7e61-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e7e61-250">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="e7e61-250">Test single sign-on</span></span>

<span data-ttu-id="e7e61-251">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="e7e61-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e7e61-252">Merhaba Mimecast Yönetici Konsolu hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Mimecast yönetici konsol uygulaması almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7e61-252">When you click hello Mimecast Admin Console tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Admin Console application.</span></span>
<span data-ttu-id="e7e61-253">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e7e61-253">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e7e61-254">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e7e61-254">Additional resources</span></span>

* [<span data-ttu-id="e7e61-255">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="e7e61-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e7e61-256">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e7e61-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

