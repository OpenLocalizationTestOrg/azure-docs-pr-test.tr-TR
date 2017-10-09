---
title: "Öğretici: Azure Active Directory Tümleştirme ile UNIFI | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile UNIFI arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1f49ee4-d2d4-4a82-9baf-0587ca1f20f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: af7cc1167b5c0cff2a1f4cdaa8a2b93f5a718f81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-unifi"></a><span data-ttu-id="8a926-103">Öğretici: Azure Active Directory Tümleştirme UNIFI ile</span><span class="sxs-lookup"><span data-stu-id="8a926-103">Tutorial: Azure Active Directory integration with UNIFI</span></span>

<span data-ttu-id="8a926-104">Bu öğreticide, bilgi nasıl toointegrate UNIFI Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8a926-104">In this tutorial, you learn how toointegrate UNIFI with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8a926-105">UNIFI Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="8a926-105">Integrating UNIFI with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8a926-106">Erişim tooUNIFI sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8a926-106">You can control in Azure AD who has access tooUNIFI</span></span>
- <span data-ttu-id="8a926-107">Kullanıcıların tooautomatically get açan tooUNIFI (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8a926-107">You can enable your users tooautomatically get signed-on tooUNIFI (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8a926-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="8a926-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8a926-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8a926-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a926-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8a926-110">Prerequisites</span></span>

<span data-ttu-id="8a926-111">tooconfigure UNIFI ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="8a926-111">tooconfigure Azure AD integration with UNIFI, you need hello following items:</span></span>

- <span data-ttu-id="8a926-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="8a926-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8a926-113">Bir UNIFI çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="8a926-113">A UNIFI single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8a926-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="8a926-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8a926-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="8a926-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8a926-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="8a926-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8a926-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8a926-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8a926-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="8a926-118">Scenario description</span></span>
<span data-ttu-id="8a926-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="8a926-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8a926-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="8a926-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a926-121">Merhaba Galerisi'nden UNIFI ekleme</span><span class="sxs-lookup"><span data-stu-id="8a926-121">Adding UNIFI from hello gallery</span></span>
2. <span data-ttu-id="8a926-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="8a926-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-unifi-from-hello-gallery"></a><span data-ttu-id="8a926-123">Merhaba Galerisi'nden UNIFI ekleme</span><span class="sxs-lookup"><span data-stu-id="8a926-123">Adding UNIFI from hello gallery</span></span>
<span data-ttu-id="8a926-124">Azure AD'ye tooconfigure hello tümleştirme UNIFI, tooadd UNIFI hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a926-124">tooconfigure hello integration of UNIFI into Azure AD, you need tooadd UNIFI from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8a926-125">**tooadd UNIFI hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8a926-125">**tooadd UNIFI from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a926-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="8a926-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8a926-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="8a926-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8a926-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8a926-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="8a926-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8a926-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="8a926-133">Merhaba arama kutusuna yazın **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="8a926-133">In hello search box, type **UNIFI**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_search.png)

5. <span data-ttu-id="8a926-135">Merhaba Sonuçlar panelinde seçin **UNIFI**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="8a926-135">In hello results panel, select **UNIFI**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8a926-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="8a926-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8a926-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı UNIFI sınayın.</span><span class="sxs-lookup"><span data-stu-id="8a926-138">In this section, you configure and test Azure AD single sign-on with UNIFI based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8a926-139">Tek toowork'ın oturum açma hangi hello karşılık gelen UNIFI içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a926-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UNIFI is tooa user in Azure AD.</span></span> <span data-ttu-id="8a926-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı UNIFI hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a926-140">In other words, a link relationship between an Azure AD user and hello related user in UNIFI needs toobe established.</span></span>

<span data-ttu-id="8a926-141">Merhaba hello değeri UNIFI içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="8a926-141">In UNIFI, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8a926-142">tooconfigure ve UNIFI ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="8a926-142">tooconfigure and test Azure AD single sign-on with UNIFI, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8a926-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="8a926-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8a926-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="8a926-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8a926-145">**[Test kullanıcı bir UNIFI oluşturma](#creating-a-unifi-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir UNIFI içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="8a926-145">**[Creating a UNIFI test user](#creating-a-unifi-test-user)** - toohave a counterpart of Britta Simon in UNIFI that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8a926-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="8a926-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8a926-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="8a926-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8a926-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8a926-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8a926-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma UNIFI uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8a926-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UNIFI application.</span></span>

<span data-ttu-id="8a926-150">**tooconfigure Azure AD çoklu oturum açma ile UNIFI, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8a926-150">**tooconfigure Azure AD single sign-on with UNIFI, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a926-151">Hello hello üzerinde Azure portal'ın **UNIFI** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="8a926-151">In hello Azure portal, on hello **UNIFI** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="8a926-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="8a926-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_samlbase.png)

3. <span data-ttu-id="8a926-155">Merhaba üzerinde **UNIFI etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="8a926-155">On hello **UNIFI Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url1.png)

    <span data-ttu-id="8a926-157">Merhaba, **tanımlayıcısı** metin kutusuna, türü başlangıç değeri:`INVIEWlabs`</span><span class="sxs-lookup"><span data-stu-id="8a926-157">In hello **Identifier** textbox, type hello value: `INVIEWlabs`</span></span> 

4. <span data-ttu-id="8a926-158">Denetleme **Göster Gelişmiş URL ayarları**, tooconfigure hello uygulamada istiyorsanız **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="8a926-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url2.png)

    <span data-ttu-id="8a926-160">Merhaba, **oturum açma URL'si** metin kutusuna, türü hello URL'si:`https://app.discoverunifi.com/login`</span><span class="sxs-lookup"><span data-stu-id="8a926-160">In hello **Sign-on URL** textbox, type hello URL: `https://app.discoverunifi.com/login`</span></span>

5. <span data-ttu-id="8a926-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8a926-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_certificate.png) 

6. <span data-ttu-id="8a926-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8a926-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="8a926-165">Merhaba üzerinde **UNIFI yapılandırma** 'yi tıklatın **yapılandırma UNIFI** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="8a926-165">On hello **UNIFI Configuration** section, click **Configure UNIFI** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8a926-166">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="8a926-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_configure.png)

8. <span data-ttu-id="8a926-168">Farklı web tarayıcısı penceresinde tooyour üzerinde oturum **UNIFI** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="8a926-168">In a different web browser window, sign on tooyour **UNIFI** company site as administrator.</span></span>

9. <span data-ttu-id="8a926-169">Tıklatın hello üzerinde **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="8a926-169">Click on hello **Users**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/app1.png) 

10. <span data-ttu-id="8a926-171">Tıklatın hello üzerinde **yeni kimlik sağlayıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="8a926-171">Click on hello **Add New Identity Provider**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/app2.png)

11. <span data-ttu-id="8a926-173">Merhaba, **kimlik sağlayıcı Ekle** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8a926-173">In hello **Add Identity Provider** section, perform hello following steps:</span></span>   

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/app3.png) 

    <span data-ttu-id="8a926-175">a.</span><span class="sxs-lookup"><span data-stu-id="8a926-175">a.</span></span> <span data-ttu-id="8a926-176">Merhaba, **sağlayıcı adı** metin kutusuna, tür hello hello kimlik sağlayıcısı adını...</span><span class="sxs-lookup"><span data-stu-id="8a926-176">In hello **Provider Name** textbox, type hello name of hello Identity Provider..</span></span>

    <span data-ttu-id="8a926-177">b.</span><span class="sxs-lookup"><span data-stu-id="8a926-177">b.</span></span> <span data-ttu-id="8a926-178">Merhaba hello içinde **sağlayıcısı URL** metin kutusuna yapıştırın hello **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyaladığınız değeri.</span><span class="sxs-lookup"><span data-stu-id="8a926-178">In hello hello **Provider URL** textbox paste hello **SAML Single Sign-On Service URL** value, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8a926-179">c.</span><span class="sxs-lookup"><span data-stu-id="8a926-179">c.</span></span> <span data-ttu-id="8a926-180">Açık hello hello Not Defteri'nde, Azure Portalı'ndan indirilen sertifika kaldırmak hello **---başlangıç sertifika---** ve **---son SERTİFİKAYI---** etiketi ve içeriği kalan hello yapıştırın Merhaba **sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="8a926-180">Open hello Certificate that you have downloaded from hello Azure portal in notepad, remove hello **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste hello remaining content in hello **Certificate** textbox.</span></span>

    <span data-ttu-id="8a926-181">d.</span><span class="sxs-lookup"><span data-stu-id="8a926-181">d.</span></span> <span data-ttu-id="8a926-182">Select hello **varsayılan bir sağlayıcı** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="8a926-182">Select hello **is Default Provider** checkbox.</span></span>

> [!TIP]
> <span data-ttu-id="8a926-183">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="8a926-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8a926-184">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="8a926-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8a926-185">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8a926-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8a926-186">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8a926-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="8a926-187">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="8a926-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="8a926-189">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8a926-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a926-190">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="8a926-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-unifi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8a926-192">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="8a926-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-unifi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8a926-194">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="8a926-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-unifi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8a926-196">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8a926-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-unifi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8a926-198">a.</span><span class="sxs-lookup"><span data-stu-id="8a926-198">a.</span></span> <span data-ttu-id="8a926-199">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8a926-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8a926-200">b.</span><span class="sxs-lookup"><span data-stu-id="8a926-200">b.</span></span> <span data-ttu-id="8a926-201">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="8a926-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8a926-202">c.</span><span class="sxs-lookup"><span data-stu-id="8a926-202">c.</span></span> <span data-ttu-id="8a926-203">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="8a926-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8a926-204">d.</span><span class="sxs-lookup"><span data-stu-id="8a926-204">d.</span></span> <span data-ttu-id="8a926-205">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8a926-205">Click **Create**.</span></span>
 
### <a name="creating-a-unifi-test-user"></a><span data-ttu-id="8a926-206">UNIFI test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8a926-206">Creating a UNIFI test user</span></span>

<span data-ttu-id="8a926-207">Bu bölümde, Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8a926-207">In this section, you create a user called Britta Simon.</span></span> <span data-ttu-id="8a926-208">**UNIFI** hiçbir el ile yapılacak adımlar gerekli; bu nedenle otomatik kullanıcı sağlamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="8a926-208">**UNIFI** supports automatic user provisioning so no manual steps are required.</span></span> <span data-ttu-id="8a926-209">Kullanıcılar, başarılı kimlik doğrulama hello Azure AD alanından sonra otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8a926-209">Users are created automatically after successful authentication from hello Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8a926-210">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="8a926-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8a926-211">Bu bölümde, erişim tooUNIFI vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8a926-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUNIFI.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="8a926-213">**tooassign Britta Simon tooUNIFI hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8a926-213">**tooassign Britta Simon tooUNIFI, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a926-214">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8a926-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="8a926-216">Merhaba uygulamalar listesinde **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="8a926-216">In hello applications list, select **UNIFI**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_app.png) 

3. <span data-ttu-id="8a926-218">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="8a926-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="8a926-220">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8a926-220">Click **Add** button.</span></span> <span data-ttu-id="8a926-221">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8a926-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="8a926-223">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="8a926-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8a926-224">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8a926-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8a926-225">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8a926-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8a926-226">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="8a926-226">Testing single sign-on</span></span>

<span data-ttu-id="8a926-227">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="8a926-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8a926-228">UNIFI döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma tooyour UNIFI uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a926-228">When you click hello UNIFI tile in hello Access Panel, you should get automatically signed-on tooyour UNIFI application.</span></span>
<span data-ttu-id="8a926-229">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8a926-229">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8a926-230">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8a926-230">Additional resources</span></span>

* [<span data-ttu-id="8a926-231">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="8a926-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8a926-232">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="8a926-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_203.png

