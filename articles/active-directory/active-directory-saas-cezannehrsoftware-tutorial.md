---
title: "Öğretici: Azure Active Directory Tümleştirme Cezanne ik yazılımıyla | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Cezanne ik yazılımı arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a><span data-ttu-id="3d5c3-103">Öğretici: Azure Active Directory Cezanne ik yazılım ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="3d5c3-103">Tutorial: Integrate Azure Active Directory with Cezanne HR software</span></span>

<span data-ttu-id="3d5c3-104">Bu öğreticide, bilgi nasıl toointegrate Cezanne ik yazılım Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3d5c3-104">In this tutorial, you learn how toointegrate Cezanne HR software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3d5c3-105">Cezanne HR yazılım Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-105">Integrating Cezanne HR software with Azure AD provides you with hello following benefits.</span></span> <span data-ttu-id="3d5c3-106">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3d5c3-106">You can:</span></span>

- <span data-ttu-id="3d5c3-107">Erişim tooCezanne sahip Azure AD'de ik yazılım denetler.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-107">Control in Azure AD who has access tooCezanne HR software.</span></span>
- <span data-ttu-id="3d5c3-108">Kullanıcıların tooautomatically oturum açma tooCezanne ik yazılımıyla çoklu oturum açma (SSO) ile Azure AD hesaplarına etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-108">Enable your users tooautomatically sign in tooCezanne HR software with single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3d5c3-109">Hesaplarınızı tek bir merkezi konumda yönetme: Azure portal hello.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="3d5c3-110">toolearn yazılım olarak Azure AD ile hizmet (SaaS) uygulama tümleştirmesi hakkında daha fazla bilgi görmek [uygulama erişimi ve SSO ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3d5c3-110">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and SSO with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d5c3-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3d5c3-111">Prerequisites</span></span>

<span data-ttu-id="3d5c3-112">tooconfigure Cezanne ik yazılım ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="3d5c3-112">tooconfigure Azure AD integration with Cezanne HR software, you need hello following items:</span></span>

- <span data-ttu-id="3d5c3-113">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="3d5c3-113">An Azure AD subscription</span></span>
- <span data-ttu-id="3d5c3-114">Cezanne HR yazılım abonelik SSO'su etkin</span><span class="sxs-lookup"><span data-stu-id="3d5c3-114">A Cezanne HR software SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3d5c3-115">tootest hello adımları Bu öğreticide, bir üretim ortamında kullanmamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-115">tootest hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="3d5c3-116">Bu öğreticide tootest hello adımları bu önerileri izleyin:</span><span class="sxs-lookup"><span data-stu-id="3d5c3-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="3d5c3-117">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-117">Don't use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3d5c3-118">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d5c3-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3d5c3-119">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="3d5c3-119">Scenario description</span></span>
<span data-ttu-id="3d5c3-120">Bu öğreticide, Azure AD SSO bir test ortamında test.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-120">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="3d5c3-121">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="3d5c3-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="3d5c3-122">Merhaba Galerisi'nden Cezanne ik yazılım ekleme</span><span class="sxs-lookup"><span data-stu-id="3d5c3-122">Adding Cezanne HR software from hello gallery</span></span>
* <span data-ttu-id="3d5c3-123">Yapılandırma ve Azure AD SSO test etme</span><span class="sxs-lookup"><span data-stu-id="3d5c3-123">Configuring and testing Azure AD SSO</span></span>

## <a name="add-cezanne-hr-software-from-hello-gallery"></a><span data-ttu-id="3d5c3-124">Merhaba Galerisi'nden Cezanne ik yazılım Ekle</span><span class="sxs-lookup"><span data-stu-id="3d5c3-124">Add Cezanne HR software from hello gallery</span></span>
<span data-ttu-id="3d5c3-125">Azure AD'ye Cezanne ik yazılımın tooconfigure hello tümleştirme hello galeri tooyour listesinden yönetilen SaaS uygulamaları Cezanne ik yazılım ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-125">tooconfigure hello integration of Cezanne HR software into Azure AD, add Cezanne HR software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3d5c3-126">tooadd Cezanne ik yazılım hello galerisinden hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="3d5c3-126">tooadd Cezanne HR software from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="3d5c3-127">Merhaba,  **[Azure portal](https://portal.azure.com)**, buna hello sol bölmesinde, seçin hello **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-127">In hello **[Azure portal](https://portal.azure.com)**, in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![Merhaba "Azure Active Directory" düğmesi][1]

2. <span data-ttu-id="3d5c3-129">Seçin **kurumsal uygulamalar** > **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![Merhaba "Tüm uygulamaları" bağlantı][2]
    
3. <span data-ttu-id="3d5c3-131">tooadd hello hello üstündeki yeni bir uygulama **tüm uygulamaları** iletişim kutusunda **yeni uygulama**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-131">tooadd a new application, at hello top of hello **All applications** dialog box, select **New application**.</span></span>

    !["Yeni uygulamayı" Merhaba düğmesi][3]

4. <span data-ttu-id="3d5c3-133">Merhaba arama kutusuna yazın **Cezanne ik yazılım**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-133">In hello search box, type **Cezanne HR Software**.</span></span>

    ![Merhaba arama kutusu](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. <span data-ttu-id="3d5c3-135">Merhaba sonuçlar listesinde seçin **Cezanne ik yazılım** seçip hello **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-135">In hello results list, select **Cezanne HR Software** and then select hello **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesi](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3d5c3-137">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="3d5c3-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="3d5c3-138">Bu bölümde, yapılandırma ve Azure AD SSO Cezanne ik yazılım "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı ile test etme</span><span class="sxs-lookup"><span data-stu-id="3d5c3-138">In this section, you configure and test Azure AD SSO with Cezanne HR software based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3d5c3-139">SSO toowork için Azure AD tooknow hello Cezanne ik yazılım karşılık gelen toohello Azure AD kullanıcısının gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-139">For SSO toowork, Azure AD needs tooknow hello Cezanne HR software counterpart toohello Azure AD user.</span></span> <span data-ttu-id="3d5c3-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı arasında bir bağlantı ilişkisi hello Cezanne ik yazılım oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-140">In other words, you must establish a link relationship between an Azure AD user and hello related user in hello Cezanne HR software.</span></span>

<span data-ttu-id="3d5c3-141">tooestablish hello bağlantı ilişkisi, Ata hello Cezanne ik yazılım **kullanıcı adı** değeri hello Azure AD olarak **kullanıcıadı** değeri.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-141">tooestablish hello link relationship, assign hello Cezanne HR software **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="3d5c3-142">tooconfigure ve test Cezanne ik yazılım, yapı taşları aşağıdaki tam hello kullanarak Azure AD SSO.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-142">tooconfigure and test Azure AD SSO by using Cezanne HR software, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="3d5c3-143">Azure AD SSO yapılandırın</span><span class="sxs-lookup"><span data-stu-id="3d5c3-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="3d5c3-144">Bu bölümde, hello Azure portalında Azure AD SSO'yu etkinleştirmek ve hello aşağıdakileri yaparak Cezanne ik yazılım uygulamanızda SSO yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="3d5c3-144">In this section, you can enable Azure AD SSO in hello Azure portal and configure SSO in your Cezanne HR software application by doing hello following:</span></span>

1. <span data-ttu-id="3d5c3-145">Merhaba hello üzerinde Azure portal'ın **Cezanne ik yazılım** uygulama tümleştirmesi sayfasında, **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-145">In hello Azure portal, on hello **Cezanne HR Software** application integration page, select **Single sign-on**.</span></span>

    ![komutu "çoklu oturum açmayı" Merhaba][4]

2. <span data-ttu-id="3d5c3-147">Merhaba içinde SSO tooenable **çoklu oturum açma** iletişim kutusu, select hello **modu** olarak **SAML tabanlı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-147">tooenable SSO, in hello **Single sign-on** dialog box, select hello **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Merhaba "Modu" kutusu](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. <span data-ttu-id="3d5c3-149">Altında **Cezanne ik yazılım etki alanı ve URL'leri**, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="3d5c3-149">Under **Cezanne HR Software Domain and URLs**, do hello following:</span></span>

    ![Merhaba "Cezanne ik yazılım etki alanı ve URL'leri" bölümü](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    <span data-ttu-id="3d5c3-151">a.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-151">a.</span></span> <span data-ttu-id="3d5c3-152">Merhaba, **oturum açma URL'si** kutusuna sözdizimi aşağıdaki hello sahip bir URL yazın:`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="3d5c3-152">In hello **Sign-on URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span></span>

    <span data-ttu-id="3d5c3-153">b.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-153">b.</span></span> <span data-ttu-id="3d5c3-154">Merhaba, **yanıt URL'si** kutusuna sözdizimi aşağıdaki hello sahip bir URL yazın:`https://w3.cezanneondemand.com:443/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="3d5c3-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com:443/<tenantid>`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="3d5c3-155">Merhaba önceki değerleri gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-155">hello preceding values are not real.</span></span> <span data-ttu-id="3d5c3-156">Bunları hello gerçek yanıt URL'si ve hello oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-156">Update them with hello actual reply URL and hello sign-on URL.</span></span> <span data-ttu-id="3d5c3-157">tooobtain hello değerleri, kişi hello [Cezanne ik yazılım istemci destek ekibi](mailto:info@cezannehr.com).</span><span class="sxs-lookup"><span data-stu-id="3d5c3-157">tooobtain hello values, contact hello [Cezanne HR software client support team](mailto:info@cezannehr.com).</span></span>

4. <span data-ttu-id="3d5c3-158">Altında **SAML imzalama sertifikası**seçin **sertifika (Base64)**ve ardından hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-158">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![Merhaba "SAML imzalama sertifikası" bölümü](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. <span data-ttu-id="3d5c3-160">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-160">Select **Save**.</span></span>

    ![Merhaba "Kaydet" düğmesi](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="3d5c3-162">Altında **Cezanne ik yazılım yapılandırma**seçin **Cezanne ik yazılımı Yapılandır** tooopen hello **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-162">Under **Cezanne HR Software Configuration**, select **Configure Cezanne HR Software** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="3d5c3-163">Kopya hello **SAML varlık kimliği** ve **SAML çoklu oturum açma hizmeti** hello URL'den **hızlı başvuru** bölümü.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-163">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service** URL from hello **Quick Reference** section.</span></span>

    ![Merhaba "Cezanne ik yazılım yapılandırma" bölümü](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. <span data-ttu-id="3d5c3-165">Farklı web tarayıcısı penceresinde tooyour Cezanne ik yazılım Kiracı yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-165">In a different web browser window, sign on tooyour Cezanne HR software tenant as an administrator.</span></span>

8. <span data-ttu-id="3d5c3-166">Merhaba sol bölmesinde seçin **sistem kurulumu**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-166">In hello left pane, select **System Setup**.</span></span> <span data-ttu-id="3d5c3-167">Seçin **güvenlik ayarları** > **tek oturum açma yapılandırması**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-167">Select **Security Settings** > **Single Sign-On Configuration**.</span></span>

    ![Merhaba "Yapılandırma tek oturum açma" bağlantısı](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. <span data-ttu-id="3d5c3-169">Merhaba, **çoklu oturum açma (SSO) Hizmetleri aşağıdaki hello kullanarak kullanıcıların toolog izin** bölmesinde, select hello **SAML 2.0** onay kutusunu ve select hello **Gelişmiş Yapılandırma** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-169">In hello **Allow users toolog in using hello following Single Sign-On (SSO) services** pane, select hello **SAML 2.0** check box and select hello **Advanced Configuration** option.</span></span>

    ![Çoklu oturum açma hizmetleri seçenekleri](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. <span data-ttu-id="3d5c3-171">Seçin **yeni Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-171">Select **Add New**.</span></span>

    ![Merhaba "Yeni Ekle" düğmesi](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. <span data-ttu-id="3d5c3-173">Altında **SAML 2.0 kimlik sağlayıcısı**, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="3d5c3-173">Under **SAML 2.0 Identity Providers**, do hello following:</span></span>

    ![Merhaba "SAML 2.0 kimlik sağlayıcısı" bölümü](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    <span data-ttu-id="3d5c3-175">a.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-175">a.</span></span> <span data-ttu-id="3d5c3-176">Merhaba, **görünen adı** kutusuna, kimlik sağlayıcısının hello adı girin.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-176">In hello **Display Name** box, enter hello name of your identity provider.</span></span>

    <span data-ttu-id="3d5c3-177">b.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-177">b.</span></span> <span data-ttu-id="3d5c3-178">Merhaba, **varlık tanımlayıcısı** kutusunda, hello Yapıştır **SAML varlık kimliği** hello Azure portal ' kopyaladığınız.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-178">In hello **Entity Identifier** box, paste hello **SAML Entity ID** that you copied from hello Azure portal.</span></span> 

    <span data-ttu-id="3d5c3-179">c.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-179">c.</span></span> <span data-ttu-id="3d5c3-180">Merhaba, **SAML bağlama** liste kutusunda **POST**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-180">In hello **SAML Binding** list box, select **POST**.</span></span>

    <span data-ttu-id="3d5c3-181">d.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-181">d.</span></span> <span data-ttu-id="3d5c3-182">Merhaba, **güvenlik belirteci Hizmeti uç noktası** kutusunda, hello Yapıştır **SAML çoklu oturum açma hizmeti** hello Azure portal ' kopyaladığınız URL.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-182">In hello **Security Token Service Endpoint** box, paste hello **SAML Single Sign-On Service** URL that you copied from hello Azure portal.</span></span> 
    
    <span data-ttu-id="3d5c3-183">e.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-183">e.</span></span> <span data-ttu-id="3d5c3-184">Merhaba, **kullanıcı kimliği öznitelik adı** kutusuna `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-184">In hello **User ID Attribute Name** box, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="3d5c3-185">f.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-185">f.</span></span> <span data-ttu-id="3d5c3-186">tooupload hello Azure AD'den select hello sertifika indirilen **karşıya** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-186">tooupload hello downloaded certificate from Azure AD, select hello **Upload** button.</span></span>
    
    <span data-ttu-id="3d5c3-187">g.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-187">g.</span></span> <span data-ttu-id="3d5c3-188">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-188">Select **OK**.</span></span> 

12. <span data-ttu-id="3d5c3-189">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-189">Select **Save**.</span></span>

    ![Merhaba "Kaydet" düğmesi](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> <span data-ttu-id="3d5c3-191">Merhaba uygulama ayarlama gibi hello yönergeleri önceki hello kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3d5c3-191">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="3d5c3-192">Hello hello uygulama ekledikten sonra **Active Directory** > **kurumsal uygulamalar** bölümü, select hello **çoklu oturum açma** sekmesi. Ardından erişim hello hello belgelerinden katıştırılmış **yapılandırma** bölümü.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-192">After you add hello app from hello **Active Directory** > **Enterprise applications** section, select hello **Single sign-on** tab. Then access hello embedded documentation from hello **Configuration** section.</span></span> 

<span data-ttu-id="3d5c3-193">toolearn hello embedded belgeler özelliği hakkında daha fazla bilgi görmek [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="3d5c3-193">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3d5c3-194">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3d5c3-194">Create an Azure AD test user</span></span>
<span data-ttu-id="3d5c3-195">Bu bölümde, test kullanıcı Britta Simon hello Azure portal oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-195">In this section, you create test user Britta Simon in hello Azure portal.</span></span>

![Merhaba test kullanıcısı Britta Simon][100]

<span data-ttu-id="3d5c3-197">Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="3d5c3-197">toocreate a test user in Azure AD, do hello following:</span></span>

1. <span data-ttu-id="3d5c3-198">Merhaba, **Azure portal**, buna hello sol bölmesinde, seçin hello **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-198">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![Merhaba "Azure Active Directory" düğmesi](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3d5c3-200">Kullanıcıların, select toodisplay hello listesini **kullanıcılar ve gruplar** > **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-200">toodisplay hello list of users, select **Users and groups** > **All users**.</span></span>
    
    ![Merhaba "Tüm kullanıcılar" bağlantı](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    <span data-ttu-id="3d5c3-202">Merhaba **tüm kullanıcılar** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-202">hello **All users** dialog box opens.</span></span>

3. <span data-ttu-id="3d5c3-203">tooopen hello **kullanıcı** iletişim kutusunda **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-203">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![Merhaba "Ekle" düğmesi](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3d5c3-205">Merhaba, **kullanıcı** iletişim kutusunda, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="3d5c3-205">In hello **User** dialog box, do hello following:</span></span>
 
    ![Merhaba "Kullanıcı" iletişim kutusu](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3d5c3-207">a.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-207">a.</span></span> <span data-ttu-id="3d5c3-208">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3d5c3-209">b.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-209">b.</span></span> <span data-ttu-id="3d5c3-210">Merhaba, **kullanıcı adı** kutusuna kullanıcı Britta Simon'ın yazın **e-posta adresi**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-210">In hello **User name** box, type user Britta Simon's **email address**.</span></span>

    <span data-ttu-id="3d5c3-211">c.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-211">c.</span></span> <span data-ttu-id="3d5c3-212">Select hello **Göster parola** onay kutusunu ve ardından hello oluşturulan Not hello değeri **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-212">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="3d5c3-213">d.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-213">d.</span></span> <span data-ttu-id="3d5c3-214">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-214">Select **Create**.</span></span>
 
### <a name="create-a-cezanne-hr-software-test-user"></a><span data-ttu-id="3d5c3-215">Cezanne HR yazılım test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3d5c3-215">Create a Cezanne HR software test user</span></span>

<span data-ttu-id="3d5c3-216">tooenable Azure AD kullanıcıların toosign tooCezanne ik yazılımda bunlar Cezanne ik yazılımına sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-216">tooenable Azure AD users toosign in tooCezanne HR software, they must be provisioned into Cezanne HR software.</span></span> <span data-ttu-id="3d5c3-217">Cezanne HR yazılım Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-217">In hello case of Cezanne HR software, provisioning is a manual task.</span></span>

<span data-ttu-id="3d5c3-218">Bir kullanıcı hesabı hello aşağıdakileri yaparak sağlayın:</span><span class="sxs-lookup"><span data-stu-id="3d5c3-218">Provision a user account by doing hello following:</span></span>

1.  <span data-ttu-id="3d5c3-219">İçinde tooyour Cezanne ik yazılım şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-219">Sign in tooyour Cezanne HR software company site as an administrator.</span></span>

2.  <span data-ttu-id="3d5c3-220">Merhaba sol bölmesinde seçin **sistem kurulumu** > **kullanıcıları yönetme** > **yeni kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-220">In hello left pane, select **System Setup** > **Manage Users** > **Add New User**.</span></span>

    <span data-ttu-id="3d5c3-221">![Merhaba "Yeni Kullanıcı Ekle" bağlantı](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="3d5c3-221">![hello "Add New User" link](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span></span>

3.  <span data-ttu-id="3d5c3-222">Altında **kişi ayrıntıları**, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="3d5c3-222">Under **Person Details**, do hello following:</span></span>

    <span data-ttu-id="3d5c3-223">![Merhaba "Kişi Ayrıntıları" bölümü](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="3d5c3-223">![hello "Person Details" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span></span>
    
    <span data-ttu-id="3d5c3-224">a.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-224">a.</span></span> <span data-ttu-id="3d5c3-225">Ayarlama **iç kullanıcı** olarak **OFF**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-225">Set **Internal User** as **OFF**.</span></span>
    
    <span data-ttu-id="3d5c3-226">b.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-226">b.</span></span> <span data-ttu-id="3d5c3-227">Merhaba, **ad** kutusu, türü hello kullanıcının ilk adını, örneğin, **Britta**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-227">In hello **First Name** box, type hello user's first name, for example, **Britta**.</span></span>  
 
    <span data-ttu-id="3d5c3-228">c.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-228">c.</span></span> <span data-ttu-id="3d5c3-229">Merhaba, **Soyadı** kutusu, türü hello kullanıcının soyadını, örneğin, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-229">In hello **Last Name** box, type hello user's last name, for example, **Simon**.</span></span>
    
    <span data-ttu-id="3d5c3-230">d.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-230">d.</span></span> <span data-ttu-id="3d5c3-231">Merhaba, **e-posta** hello kullanıcının e-posta adresi, örneğin, yazın Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-231">In hello **E-mail** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>

4.  <span data-ttu-id="3d5c3-232">Altında **hesap bilgilerini**, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="3d5c3-232">Under **Account Information**, do hello following:</span></span>

    <span data-ttu-id="3d5c3-233">![Merhaba "Hesap bilgisi" bölümünde](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="3d5c3-233">![hello "Account Information" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span></span>
    
    <span data-ttu-id="3d5c3-234">a.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-234">a.</span></span> <span data-ttu-id="3d5c3-235">Merhaba, **kullanıcıadı** hello kullanıcının e-posta adresi, örneğin, yazın Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-235">In hello **Username** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="3d5c3-236">b.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-236">b.</span></span> <span data-ttu-id="3d5c3-237">Merhaba, **parola** hello kullanıcının parolasını yazın.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-237">In hello **Password** box, type hello user's password.</span></span>
    
    <span data-ttu-id="3d5c3-238">c.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-238">c.</span></span> <span data-ttu-id="3d5c3-239">Merhaba, **güvenlik rolü** kutusunda **ik Professional**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-239">In hello **Security Role** box, select **HR Professional**.</span></span>
    
    <span data-ttu-id="3d5c3-240">d.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-240">d.</span></span> <span data-ttu-id="3d5c3-241">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-241">Select **OK**.</span></span>

5. <span data-ttu-id="3d5c3-242">Merhaba üzerinde **çoklu oturum açma** sekmede hello **SAML 2.0 tanımlayıcıları** bölümünde, select **yeni Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-242">On hello **Single sign-on** tab, in hello **SAML 2.0 Identifiers** section, select **Add New**.</span></span>

    <span data-ttu-id="3d5c3-243">![Merhaba "Yeni Ekle" düğmesi](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="3d5c3-243">![hello "Add New" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span></span>

6. <span data-ttu-id="3d5c3-244">Merhaba, **kimlik sağlayıcısı** liste kutusunda, kimlik sağlayıcısı seçin.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-244">In hello **Identity Provider** list box, select your identity provider.</span></span> <span data-ttu-id="3d5c3-245">Merhaba, **kullanıcı tanımlayıcısı** kutusunda, test kullanıcı Britta Simon'ın hesabının hello e-posta adresi girin.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-245">In hello **User Identifier** box, enter hello email address for test user Britta Simon's account.</span></span>

    <span data-ttu-id="3d5c3-246">![Merhaba "Kimlik sağlayıcısı" ve "Kullanıcı tanımlayıcısı" kutuları](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="3d5c3-246">![hello "Identity Provider" and "User Identifier" boxes](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span></span>
    
7. <span data-ttu-id="3d5c3-247">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-247">Select **Save**.</span></span>

    <span data-ttu-id="3d5c3-248">![Merhaba "Kaydet" düğmesini](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="3d5c3-248">![hello "Save" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="3d5c3-249">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="3d5c3-249">Assign hello Azure AD test user</span></span>

<span data-ttu-id="3d5c3-250">Bu bölümde, test kullanıcısı Britta Simon toouse Azure SSO erişimi tooCezanne ik yazılım vererek etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-250">In this section, you enable test user Britta Simon toouse Azure SSO by granting access tooCezanne HR software.</span></span>

![Test kullanıcı erişimi][200] 

1. <span data-ttu-id="3d5c3-252">Hello Azure portal, hello uygulamaları görünümünü açın ve toohello dizini görünümü gidin.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-252">In hello Azure portal, open hello applications view and then go toohello directory view.</span></span> <span data-ttu-id="3d5c3-253">Seçin **kurumsal uygulamalar** > **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-253">Select **Enterprise applications** > **All applications**.</span></span>

    ![Merhaba "Tüm uygulamaları" bağlantı][201] 

2. <span data-ttu-id="3d5c3-255">Merhaba uygulamalar listesinde **Cezanne ik yazılım**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-255">In hello applications list, select **Cezanne HR Software**.</span></span>

    ![Merhaba "Uygulamaları" listesi](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. <span data-ttu-id="3d5c3-257">Merhaba soldaki Hello menüde seçin **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-257">In hello menu on hello left, select **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="3d5c3-259">**Add (Ekle)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-259">Select **Add**.</span></span> <span data-ttu-id="3d5c3-260">Merhaba sonra **eklemek atama** iletişim kutusunda **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-260">Then in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][203]

5. <span data-ttu-id="3d5c3-262">Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda hello **kullanıcılar** listesinde **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-262">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="3d5c3-263">Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda **seçin**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-263">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="3d5c3-264">Merhaba, **eklemek atama** iletişim kutusunda **atamak**.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-264">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-sso"></a><span data-ttu-id="3d5c3-265">Test SSO</span><span class="sxs-lookup"><span data-stu-id="3d5c3-265">Test SSO</span></span>

<span data-ttu-id="3d5c3-266">Bu bölümde, hello erişim paneli kullanarak Azure AD SSO yapılandırmanızı sınayın.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-266">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="3d5c3-267">Merhaba erişim paneli hello Cezanne ik yazılım döşeme seçtiğinizde, otomatik olarak tooyour üzerinde Cezanne ik yazılım uygulaması imzalayın.</span><span class="sxs-lookup"><span data-stu-id="3d5c3-267">When you select hello Cezanne HR software tile in hello Access Panel, you sign on automatically tooyour Cezanne HR software application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d5c3-268">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3d5c3-268">Next steps</span></span>

* [<span data-ttu-id="3d5c3-269">İlgili nasıl öğreticiler listesi Azure Active Directory ile toointegrate SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="3d5c3-269">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3d5c3-270">Uygulama erişimi ve SSO ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="3d5c3-270">What is application access and SSO with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

