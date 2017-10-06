---
title: "Öğretici: Azure Active Directory Tümleştirme Menlo güvenlik | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory Menlo güvenlik arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 193d12eedf31f4f08e1d141936d6e918c36a2109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="45b7f-103">Öğretici: Azure Active Directory Tümleştirme Menlo güvenlik</span><span class="sxs-lookup"><span data-stu-id="45b7f-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="45b7f-104">Bu öğreticide, bilgi nasıl toointegrate Menlo güvenlik Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="45b7f-104">In this tutorial, you learn how toointegrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="45b7f-105">Menlo güvenlik Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="45b7f-105">Integrating Menlo Security with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="45b7f-106">Erişim tooMenlo güvenlik sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="45b7f-106">You can control in Azure AD who has access tooMenlo Security</span></span>
- <span data-ttu-id="45b7f-107">Kullanıcıların tooautomatically get açan tooMenlo güvenlik (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="45b7f-107">You can enable your users tooautomatically get signed-on tooMenlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="45b7f-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="45b7f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="45b7f-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz.</span><span class="sxs-lookup"><span data-stu-id="45b7f-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="45b7f-110">[Uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="45b7f-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45b7f-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="45b7f-111">Prerequisites</span></span>

<span data-ttu-id="45b7f-112">tooconfigure Menlo güvenlik ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="45b7f-112">tooconfigure Azure AD integration with Menlo Security, you need hello following items:</span></span>

- <span data-ttu-id="45b7f-113">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="45b7f-113">An Azure AD subscription</span></span>
- <span data-ttu-id="45b7f-114">Bir Menlo güvenlik çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="45b7f-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="45b7f-115">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="45b7f-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="45b7f-116">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="45b7f-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="45b7f-117">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="45b7f-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="45b7f-118">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="45b7f-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="45b7f-119">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="45b7f-119">Scenario description</span></span>
<span data-ttu-id="45b7f-120">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="45b7f-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="45b7f-121">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="45b7f-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="45b7f-122">Merhaba Galerisi'nden Menlo güvenlik ekleme</span><span class="sxs-lookup"><span data-stu-id="45b7f-122">Adding Menlo Security from hello gallery</span></span>
2. <span data-ttu-id="45b7f-123">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="45b7f-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-hello-gallery"></a><span data-ttu-id="45b7f-124">Merhaba Galerisi'nden Menlo güvenlik ekleme</span><span class="sxs-lookup"><span data-stu-id="45b7f-124">Adding Menlo Security from hello gallery</span></span>
<span data-ttu-id="45b7f-125">Azure AD'ye tooconfigure hello tümleştirme Menlo güvenlik tooadd Menlo güvenlik hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="45b7f-125">tooconfigure hello integration of Menlo Security into Azure AD, you need tooadd Menlo Security from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="45b7f-126">**tooadd Menlo güvenlik hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="45b7f-126">**tooadd Menlo Security from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="45b7f-127">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="45b7f-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="45b7f-129">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="45b7f-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="45b7f-130">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="45b7f-130">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="45b7f-132">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="45b7f-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="45b7f-134">Merhaba arama kutusuna yazın **Menlo güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="45b7f-134">In hello search box, type **Menlo Security**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="45b7f-136">Merhaba Sonuçlar panelinde seçin **Menlo güvenlik**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="45b7f-136">In hello results panel, select **Menlo Security**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="45b7f-138">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="45b7f-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="45b7f-139">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Menlo "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı güvenliği ile test etme</span><span class="sxs-lookup"><span data-stu-id="45b7f-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="45b7f-140">Tek toowork'ın oturum açma hangi hello karşılık gelen Menlo güvenlik tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="45b7f-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Menlo Security is tooa user in Azure AD.</span></span> <span data-ttu-id="45b7f-141">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Menlo güvenlik arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="45b7f-141">In other words, a link relationship between an Azure AD user and hello related user in Menlo Security needs toobe established.</span></span>

<span data-ttu-id="45b7f-142">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Menlo güvenlik.</span><span class="sxs-lookup"><span data-stu-id="45b7f-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Menlo Security.</span></span>

<span data-ttu-id="45b7f-143">tooconfigure ve Menlo güvenlik ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="45b7f-143">tooconfigure and test Azure AD single sign-on with Menlo Security, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="45b7f-144">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="45b7f-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="45b7f-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="45b7f-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="45b7f-146">**[Menlo güvenlik test kullanıcısı oluşturma](#creating-a-menlo-security-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Menlo güvenliği, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="45b7f-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - toohave a counterpart of Britta Simon in Menlo Security that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="45b7f-147">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="45b7f-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="45b7f-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="45b7f-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="45b7f-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="45b7f-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="45b7f-150">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Menlo güvenlik uygulamanızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="45b7f-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="45b7f-151">**tooconfigure Azure AD çoklu oturum açma Menlo güvenlik, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="45b7f-151">**tooconfigure Azure AD single sign-on with Menlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="45b7f-152">Hello hello üzerinde Azure portal'ın **Menlo güvenlik** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="45b7f-152">In hello Azure portal, on hello **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="45b7f-154">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="45b7f-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="45b7f-156">Merhaba üzerinde **Menlo güvenlik etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="45b7f-156">On hello **Menlo Security Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="45b7f-158">a.</span><span class="sxs-lookup"><span data-stu-id="45b7f-158">a.</span></span> <span data-ttu-id="45b7f-159">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.menlosecurity.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="45b7f-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="45b7f-160">b.</span><span class="sxs-lookup"><span data-stu-id="45b7f-160">b.</span></span> <span data-ttu-id="45b7f-161">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="45b7f-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="45b7f-162">Bu değerler hello gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="45b7f-162">These values are not hello real.</span></span> <span data-ttu-id="45b7f-163">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="45b7f-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="45b7f-164">Kişi [Menlo güvenlik istemci destek ekibi](https://www.menlosecurity.com/menlo-contact) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="45b7f-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="45b7f-165">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="45b7f-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="45b7f-167">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="45b7f-167">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="45b7f-169">Merhaba üzerinde **Menlo Güvenlik Yapılandırması** 'yi tıklatın **Menlo Güvenlik Yapılandırması** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="45b7f-169">On hello **Menlo Security Configuration** section, click **Configure Menlo Security** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="45b7f-170">Kopya hello **SAML varlık kimliği**, ve **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="45b7f-170">Copy hello **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="45b7f-172">tooconfigure çoklu oturum açma üzerinde **Menlo güvenlik** tarafı, oturum açma toohello **Menlo güvenlik** yönetici olarak Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="45b7f-172">tooconfigure single sign-on on **Menlo Security** side, login toohello **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="45b7f-173">Altında **ayarları** çok Git**kimlik doğrulaması** ve aşağıdaki işlemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="45b7f-173">Under **Settings** go too**Authentication** and perform following actions:</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="45b7f-175">a.</span><span class="sxs-lookup"><span data-stu-id="45b7f-175">a.</span></span> <span data-ttu-id="45b7f-176">Değer hello onay kutusunu **SAML kullanarak kullanıcı kimlik doğrulamasını etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="45b7f-176">Tick hello checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="45b7f-177">b.</span><span class="sxs-lookup"><span data-stu-id="45b7f-177">b.</span></span> <span data-ttu-id="45b7f-178">Seçin **dış erişime izin ver** çok**Evet**.</span><span class="sxs-lookup"><span data-stu-id="45b7f-178">Select **Allow External Access** too**Yes**.</span></span>

    <span data-ttu-id="45b7f-179">c.</span><span class="sxs-lookup"><span data-stu-id="45b7f-179">c.</span></span> <span data-ttu-id="45b7f-180">Altında **SAML sağlayıcısı**seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="45b7f-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="45b7f-181">d.</span><span class="sxs-lookup"><span data-stu-id="45b7f-181">d.</span></span> <span data-ttu-id="45b7f-182">**SAML 2.0 Endpoint** : Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="45b7f-182">**SAML 2.0 Endpoint** : Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="45b7f-183">e.</span><span class="sxs-lookup"><span data-stu-id="45b7f-183">e.</span></span> <span data-ttu-id="45b7f-184">**Hizmet tanımlayıcısı (veren)** : Yapıştır hello **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="45b7f-184">**Service Identifier (Issuer)** : Paste hello **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="45b7f-185">f.</span><span class="sxs-lookup"><span data-stu-id="45b7f-185">f.</span></span> <span data-ttu-id="45b7f-186">**X.509 sertifikası** : açık hello **sertifika (Base64)** hello Azure Portal Not Defteri'nde indirdiğiniz ve bu kutuya yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="45b7f-186">**X.509 Certificate** : Open hello **Certificate (Base64)** downloaded from hello Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="45b7f-187">g.</span><span class="sxs-lookup"><span data-stu-id="45b7f-187">g.</span></span> <span data-ttu-id="45b7f-188">Tıklatın **kaydetmek** toosave hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="45b7f-188">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="45b7f-189">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="45b7f-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="45b7f-190">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="45b7f-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="45b7f-191">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="45b7f-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="45b7f-192">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="45b7f-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="45b7f-193">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="45b7f-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="45b7f-195">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="45b7f-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="45b7f-196">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="45b7f-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="45b7f-198">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="45b7f-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="45b7f-200">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="45b7f-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="45b7f-202">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="45b7f-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="45b7f-204">a.</span><span class="sxs-lookup"><span data-stu-id="45b7f-204">a.</span></span> <span data-ttu-id="45b7f-205">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="45b7f-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="45b7f-206">b.</span><span class="sxs-lookup"><span data-stu-id="45b7f-206">b.</span></span> <span data-ttu-id="45b7f-207">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="45b7f-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="45b7f-208">c.</span><span class="sxs-lookup"><span data-stu-id="45b7f-208">c.</span></span> <span data-ttu-id="45b7f-209">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="45b7f-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="45b7f-210">d.</span><span class="sxs-lookup"><span data-stu-id="45b7f-210">d.</span></span> <span data-ttu-id="45b7f-211">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45b7f-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="45b7f-212">Menlo güvenlik test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="45b7f-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="45b7f-213">Bu bölümde, Menlo güvenlik Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="45b7f-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="45b7f-214">Çalışmak [Menlo güvenlik istemci destek ekibi](https://www.menlosecurity.com/menlo-contact) tooadd hello kullanıcılar hello Menlo güvenlik Platform.</span><span class="sxs-lookup"><span data-stu-id="45b7f-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooadd hello users in hello Menlo Security platform.</span></span> <span data-ttu-id="45b7f-215">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="45b7f-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="45b7f-216">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="45b7f-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="45b7f-217">Bu bölümde, erişim tooMenlo güvenlik vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="45b7f-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMenlo Security.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="45b7f-219">**tooassign Britta Simon tooMenlo güvenlik hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="45b7f-219">**tooassign Britta Simon tooMenlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="45b7f-220">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="45b7f-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="45b7f-222">Merhaba uygulamalar listesinde **Menlo güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="45b7f-222">In hello applications list, select **Menlo Security**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="45b7f-224">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="45b7f-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="45b7f-226">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="45b7f-226">Click **Add** button.</span></span> <span data-ttu-id="45b7f-227">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="45b7f-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="45b7f-229">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="45b7f-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="45b7f-230">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="45b7f-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="45b7f-231">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="45b7f-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="45b7f-232">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="45b7f-232">Testing single sign-on</span></span>

<span data-ttu-id="45b7f-233">Bu bölümde, Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="45b7f-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="45b7f-234">Bir "InPrivate" veya "Incognito" modu tootrigger içinde yeni bir kimlik doğrulaması bir tarayıcı penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="45b7f-234">Open a browser window in an "InPrivate" or "Incognito" mode tootrigger a new authentication.</span></span>  <span data-ttu-id="45b7f-235">Internet Explorer'da, Ctrl + Shift + P kullanın.</span><span class="sxs-lookup"><span data-stu-id="45b7f-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="45b7f-236">Chrome'Ctrl + Shift + N kullanın.</span><span class="sxs-lookup"><span data-stu-id="45b7f-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="45b7f-237">Merhaba özel tarayıcı penceresinde Gözat tooa korumalı kaynak ve Azure AD oturum açma gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="45b7f-237">In hello private browsing window, browse tooa protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="45b7f-238">Oturum açma başarılı olduğunda, bir yalıtım oturumda çekildiği toohello istenen site olacaktır.</span><span class="sxs-lookup"><span data-stu-id="45b7f-238">Upon successful login, you will be taken toohello requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="45b7f-239">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="45b7f-239">Additional resources</span></span>

* [<span data-ttu-id="45b7f-240">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="45b7f-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="45b7f-241">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="45b7f-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

