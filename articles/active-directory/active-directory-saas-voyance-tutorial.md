---
title: "Öğretici: Azure Active Directory Tümleştirme ile Voyance | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Voyance arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e2cb9eb6b20e8611a9f6e8529b7c85a8d86ec3e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="72731-103">Öğretici: Azure Active Directory Tümleştirme Voyance ile</span><span class="sxs-lookup"><span data-stu-id="72731-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="72731-104">Bu öğreticide, bilgi nasıl toointegrate Voyance Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="72731-104">In this tutorial, you learn how toointegrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="72731-105">Voyance Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="72731-105">Integrating Voyance with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="72731-106">Erişim tooVoyance sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="72731-106">You can control in Azure AD who has access tooVoyance</span></span>
- <span data-ttu-id="72731-107">Kullanıcıların tooautomatically get açan tooVoyance (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="72731-107">You can enable your users tooautomatically get signed-on tooVoyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="72731-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="72731-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="72731-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="72731-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72731-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="72731-110">Prerequisites</span></span>

<span data-ttu-id="72731-111">tooconfigure Voyance ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="72731-111">tooconfigure Azure AD integration with Voyance, you need hello following items:</span></span>

- <span data-ttu-id="72731-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="72731-112">An Azure AD subscription</span></span>
- <span data-ttu-id="72731-113">Bir Voyance çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="72731-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="72731-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="72731-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="72731-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="72731-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="72731-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="72731-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="72731-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="72731-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="72731-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="72731-118">Scenario description</span></span>
<span data-ttu-id="72731-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="72731-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="72731-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="72731-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="72731-121">Merhaba Galerisi'nden Voyance ekleme</span><span class="sxs-lookup"><span data-stu-id="72731-121">Adding Voyance from hello gallery</span></span>
2. <span data-ttu-id="72731-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="72731-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-hello-gallery"></a><span data-ttu-id="72731-123">Merhaba Galerisi'nden Voyance ekleme</span><span class="sxs-lookup"><span data-stu-id="72731-123">Adding Voyance from hello gallery</span></span>
<span data-ttu-id="72731-124">Azure AD'ye tooconfigure hello tümleştirme Voyance, tooadd Voyance hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="72731-124">tooconfigure hello integration of Voyance into Azure AD, you need tooadd Voyance from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="72731-125">**tooadd Voyance hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="72731-125">**tooadd Voyance from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="72731-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="72731-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="72731-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="72731-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="72731-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="72731-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="72731-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="72731-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="72731-133">Merhaba arama kutusuna yazın **Voyance**seçin **Voyance** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="72731-133">In hello search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="72731-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="72731-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="72731-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Voyance sınayın.</span><span class="sxs-lookup"><span data-stu-id="72731-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="72731-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Voyance içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="72731-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Voyance is tooa user in Azure AD.</span></span> <span data-ttu-id="72731-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Voyance hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="72731-138">In other words, a link relationship between an Azure AD user and hello related user in Voyance needs toobe established.</span></span>

<span data-ttu-id="72731-139">Merhaba hello değeri Voyance içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="72731-139">In Voyance, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="72731-140">tooconfigure ve Voyance ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="72731-140">tooconfigure and test Azure AD single sign-on with Voyance, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="72731-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="72731-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="72731-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="72731-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="72731-143">**[Voyance test kullanıcısı oluşturma](#create-a-voyance-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Voyance içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="72731-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - toohave a counterpart of Britta Simon in Voyance that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="72731-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="72731-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="72731-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="72731-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="72731-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="72731-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="72731-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Voyance uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="72731-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="72731-148">**tooconfigure Azure AD çoklu oturum açma ile Voyance, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="72731-148">**tooconfigure Azure AD single sign-on with Voyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="72731-149">Hello hello üzerinde Azure portal'ın **Voyance** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="72731-149">In hello Azure portal, on hello **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="72731-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="72731-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="72731-153">Merhaba üzerinde **Voyance etki alanı ve URL'leri** bölümünde, hello tooconfigure hello uygulamada istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="72731-153">On hello **Voyance Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Voyance etki alanı ve URL'leri tek oturum açma bilgilerini IDP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="72731-155">a.</span><span class="sxs-lookup"><span data-stu-id="72731-155">a.</span></span> <span data-ttu-id="72731-156">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="72731-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="72731-157">b.</span><span class="sxs-lookup"><span data-stu-id="72731-157">b.</span></span> <span data-ttu-id="72731-158">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="72731-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="72731-159">Denetleme **Göster Gelişmiş URL ayarları** ve adım tooconfigure hello uygulamada istiyorsanız aşağıdaki hello gerçekleştirmek **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="72731-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Voyance etki alanı ve URL'leri tek oturum açma bilgilerini SP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="72731-161">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="72731-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="72731-162">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="72731-162">These values are not real.</span></span> <span data-ttu-id="72731-163">Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="72731-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="72731-164">Kişi [Voyance istemci destek ekibi](mailto:support@nyansa.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="72731-164">Contact [Voyance Client support team](mailto:support@nyansa.com) tooget these values.</span></span> 

5. <span data-ttu-id="72731-165">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="72731-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="72731-167">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="72731-167">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="72731-169">Merhaba üzerinde **Voyance yapılandırma** 'yi tıklatın **yapılandırma Voyance** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="72731-169">On hello **Voyance Configuration** section, click **Configure Voyance** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="72731-170">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="72731-170">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Voyance yapılandırma](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="72731-172">Bir farklı web tarayıcısı penceresinde, bir yönetici olarak oturum açma tooyour Voyance Kiracı.</span><span class="sxs-lookup"><span data-stu-id="72731-172">In a different web browser window, sign-on tooyour Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="72731-173">Toohello sağ üst köşesinde hello gezinti çubuğu gidin ve bildiren hello üzerinde açılan tıklayın "**Acme University**".</span><span class="sxs-lookup"><span data-stu-id="72731-173">Go toohello top right corner of hello navigation bar and click on hello drop-down that says "**Acme University**".</span></span>
    
    ![Çoklu oturum açma uygulama yan Acme University üzerinde yapılandırma](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="72731-175">Tıklayın "**yönetici ayarları**".</span><span class="sxs-lookup"><span data-stu-id="72731-175">Click "**Admin Settings**".</span></span>

    ![Çoklu oturum açma uygulama yan yönetim ayarlarını yapılandır](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="72731-177">Tıklayın "**kullanıcı erişimini**" sekmesi.</span><span class="sxs-lookup"><span data-stu-id="72731-177">Click "**User Access**" tab.</span></span>

    ![Çoklu oturum açma uygulama yan kullanıcı erişimini yapılandırma](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="72731-179">Merhaba tıklayın "**SSO devre dışı**" SAML 2.0 kullanan bir IDP olarak düğmesi tooconfigure Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72731-179">Click hello "**SSO is disabled**" button tooconfigure Azure AD as an IdP using SAML 2.0.</span></span>

    ![Yapılandırma çoklu oturum açma uygulama yan SSO devre dışı düğmesi](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="72731-181">Çok Git**SAML v2** bölümünde ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="72731-181">Go too**SAML v2** section and perform below steps:</span></span>

    ![Çoklu oturum açma SAML uygulama tarafında yapılandırma v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="72731-183">a.</span><span class="sxs-lookup"><span data-stu-id="72731-183">a.</span></span> <span data-ttu-id="72731-184">Seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="72731-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="72731-185">b.</span><span class="sxs-lookup"><span data-stu-id="72731-185">b.</span></span> <span data-ttu-id="72731-186">Yapıştır **SAML çoklu oturum açma hizmet URL'si**, hello hello Azure portal ' Kopyalanan **IDP oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="72731-186">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal Into hello **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="72731-187">c.</span><span class="sxs-lookup"><span data-stu-id="72731-187">c.</span></span> <span data-ttu-id="72731-188">İndirilen Base64 ile kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve toohello yapıştırın **IDP Cert** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="72731-188">Open your downloaded Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="72731-189">d.</span><span class="sxs-lookup"><span data-stu-id="72731-189">d.</span></span> <span data-ttu-id="72731-190">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="72731-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="72731-191">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="72731-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="72731-192">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="72731-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="72731-193">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="72731-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="72731-194">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="72731-194">Create an Azure AD test user</span></span>

<span data-ttu-id="72731-195">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="72731-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="72731-197">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="72731-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="72731-198">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="72731-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="72731-200">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="72731-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="72731-202">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="72731-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="72731-204">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="72731-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="72731-206">a.</span><span class="sxs-lookup"><span data-stu-id="72731-206">a.</span></span> <span data-ttu-id="72731-207">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="72731-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="72731-208">b.</span><span class="sxs-lookup"><span data-stu-id="72731-208">b.</span></span> <span data-ttu-id="72731-209">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="72731-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="72731-210">c.</span><span class="sxs-lookup"><span data-stu-id="72731-210">c.</span></span> <span data-ttu-id="72731-211">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="72731-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="72731-212">d.</span><span class="sxs-lookup"><span data-stu-id="72731-212">d.</span></span> <span data-ttu-id="72731-213">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="72731-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="72731-214">Voyance test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="72731-214">Create a Voyance test user</span></span>

<span data-ttu-id="72731-215">Bu bölümde Hello amacı toocreate Britta Simon içinde Voyance adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="72731-215">hello objective of this section is toocreate a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="72731-216">Voyance yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="72731-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="72731-217">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="72731-217">There is no action item for you in this section.</span></span> <span data-ttu-id="72731-218">Henüz yoksa yeni bir kullanıcı bir girişim tooaccess Voyance sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="72731-218">A new user is created during an attempt tooaccess Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="72731-219">Toocreate kullanıcı el ile gerekiyorsa, toocontact gerek [Voyance destek ekibi](maiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="72731-219">If you need toocreate a user manually, you need toocontact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="72731-220">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="72731-220">Assign hello Azure AD test user</span></span>

<span data-ttu-id="72731-221">Bu bölümde, erişim tooVoyance vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="72731-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVoyance.</span></span>

![Merhaba kullanıcı rolü atayın][200]

<span data-ttu-id="72731-223">**tooassign Britta Simon tooVoyance hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="72731-223">**tooassign Britta Simon tooVoyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="72731-224">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="72731-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="72731-226">Merhaba uygulamalar listesinde **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="72731-226">In hello applications list, select **Voyance**.</span></span>

    ![Merhaba Voyance bağlantı hello uygulamalar listesinde](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="72731-228">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="72731-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="72731-230">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="72731-230">Click **Add** button.</span></span> <span data-ttu-id="72731-231">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="72731-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="72731-233">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="72731-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="72731-234">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="72731-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="72731-235">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="72731-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="72731-236">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="72731-236">Test single sign-on</span></span>

<span data-ttu-id="72731-237">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="72731-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="72731-238">Merhaba Voyance hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Voyance uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="72731-238">When you click hello Voyance tile in hello Access Panel, you should get automatically signed-on tooyour Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="72731-239">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="72731-239">Additional resources</span></span>

* [<span data-ttu-id="72731-240">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="72731-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="72731-241">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="72731-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

