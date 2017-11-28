---
title: "Öğretici: Azure Active Directory Tümleştirme Keeper parola Yöneticisi & dijital kasası ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Keeper parola Yöneticisi & dijital kasası ve Azure Active Directory arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1a98f6a-2dae-4734-bdbf-4fba742a61d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 01e59004e6bdccfca08094f9da6f82270d5028d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-keeper-password-manager--digital-vault"></a><span data-ttu-id="96785-103">Öğretici: Azure Active Directory Tümleştirme Keeper parola Yöneticisi & dijital kasası</span><span class="sxs-lookup"><span data-stu-id="96785-103">Tutorial: Azure Active Directory integration with Keeper Password Manager & Digital Vault</span></span>

<span data-ttu-id="96785-104">Bu öğreticide, bilgi nasıl toointegrate Keeper parola Yöneticisi & dijital kasası ile Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="96785-104">In this tutorial, you learn how toointegrate Keeper Password Manager & Digital Vault with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="96785-105">Keeper parola Yöneticisi & dijital kasası Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="96785-105">Integrating Keeper Password Manager & Digital Vault with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="96785-106">Sahip Azure AD'de Denetim erişim tooKeeper parola Yöneticisi & dijital kasası</span><span class="sxs-lookup"><span data-stu-id="96785-106">You can control in Azure AD who has access tooKeeper Password Manager & Digital Vault</span></span>
- <span data-ttu-id="96785-107">Azure AD hesaplarına kullanıcılar tooautomatically get açan tooKeeper parola Yöneticisi & dijital kasası (çoklu oturum açma) etkinleştir</span><span class="sxs-lookup"><span data-stu-id="96785-107">You can enable your users tooautomatically get signed-on tooKeeper Password Manager & Digital Vault (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="96785-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="96785-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="96785-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="96785-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96785-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="96785-110">Prerequisites</span></span>

<span data-ttu-id="96785-111">tooconfigure Keeper parola Yöneticisi & dijital kasası ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="96785-111">tooconfigure Azure AD integration with Keeper Password Manager & Digital Vault, you need hello following items:</span></span>

- <span data-ttu-id="96785-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="96785-112">An Azure AD subscription</span></span>
- <span data-ttu-id="96785-113">Bir Keeper parola Yöneticisi & dijital kasası çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="96785-113">A Keeper Password Manager & Digital Vault single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="96785-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="96785-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="96785-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="96785-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="96785-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="96785-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="96785-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="96785-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="96785-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="96785-118">Scenario description</span></span>
<span data-ttu-id="96785-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="96785-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="96785-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="96785-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="96785-121">Keeper parola Yöneticisi & dijital kasası hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="96785-121">Adding Keeper Password Manager & Digital Vault from hello gallery</span></span>
2. <span data-ttu-id="96785-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="96785-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-keeper-password-manager--digital-vault-from-hello-gallery"></a><span data-ttu-id="96785-123">Keeper parola Yöneticisi & dijital kasası hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="96785-123">Adding Keeper Password Manager & Digital Vault from hello gallery</span></span>
<span data-ttu-id="96785-124">Azure AD'ye tooconfigure hello tümleştirme Keeper parola Yöneticisi & dijital kasası hello galeri tooyour listesinden yönetilen SaaS uygulamaları tooadd Keeper parola Yöneticisi & dijital kasası gerekir.</span><span class="sxs-lookup"><span data-stu-id="96785-124">tooconfigure hello integration of Keeper Password Manager & Digital Vault into Azure AD, you need tooadd Keeper Password Manager & Digital Vault from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="96785-125">**tooadd Keeper parola Yöneticisi & hello Galerisi, dijital kasadan hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="96785-125">**tooadd Keeper Password Manager & Digital Vault from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="96785-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="96785-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="96785-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="96785-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="96785-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="96785-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="96785-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="96785-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="96785-133">Merhaba arama kutusuna yazın **Keeper parola Yöneticisi & dijital kasa**.</span><span class="sxs-lookup"><span data-stu-id="96785-133">In hello search box, type **Keeper Password Manager & Digital Vault**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_search.png)

5. <span data-ttu-id="96785-135">Merhaba Sonuçlar panelinde seçin **Keeper parola Yöneticisi & dijital kasa**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="96785-135">In hello results panel, select **Keeper Password Manager & Digital Vault**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="96785-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="96785-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="96785-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Keeper parola Yöneticisi & dijital "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı kasası ile test etme</span><span class="sxs-lookup"><span data-stu-id="96785-138">In this section, you configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="96785-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Keeper parola Yöneticisi & dijital kasa tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="96785-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Keeper Password Manager & Digital Vault is tooa user in Azure AD.</span></span> <span data-ttu-id="96785-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Keeper parola Yöneticisi & dijital kasa arasındaki bağlantı ilişki kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="96785-140">In other words, a link relationship between an Azure AD user and hello related user in Keeper Password Manager & Digital Vault needs toobe established.</span></span>

<span data-ttu-id="96785-141">Keeper parola Yöneticisi & dijital kasası, hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="96785-141">In Keeper Password Manager & Digital Vault, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="96785-142">tooconfigure ve Keeper parola Yöneticisi & dijital kasası ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="96785-142">tooconfigure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="96785-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="96785-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="96785-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="96785-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="96785-145">**[Keeper parola Yöneticisi & dijital kasası test kullanıcısı oluşturma](#creating-a-keeperpasswordmanager-test-user)**  -toohave Britta Simon Keeper parola Yöneticisi & kullanıcı bağlantılı toohello Azure AD gösterimidir dijital kasası, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="96785-145">**[Creating a Keeper Password Manager & Digital Vault test user](#creating-a-keeperpasswordmanager-test-user)** - toohave a counterpart of Britta Simon in Keeper Password Manager & Digital Vault that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="96785-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="96785-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="96785-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="96785-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="96785-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="96785-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="96785-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Keeper parola Yöneticisi & dijital kasası uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="96785-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Keeper Password Manager & Digital Vault application.</span></span>

<span data-ttu-id="96785-150">**Azure AD çoklu oturum açma tooconfigure Keeper parola Yöneticisi & dijital kasası ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="96785-150">**tooconfigure Azure AD single sign-on with Keeper Password Manager & Digital Vault, perform hello following steps:**</span></span>

1. <span data-ttu-id="96785-151">Merhaba hello üzerinde Azure portal'ın **Keeper parola Yöneticisi & dijital kasa** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="96785-151">In hello Azure portal, on hello **Keeper Password Manager & Digital Vault** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="96785-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="96785-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_samlbase.png)

3. <span data-ttu-id="96785-155">Merhaba üzerinde **Keeper parola Yöneticisi & dijital kasası etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="96785-155">On hello **Keeper Password Manager & Digital Vault Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_url.png)

    <span data-ttu-id="96785-157">a.</span><span class="sxs-lookup"><span data-stu-id="96785-157">a.</span></span> <span data-ttu-id="96785-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span><span class="sxs-lookup"><span data-stu-id="96785-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span></span>

    <span data-ttu-id="96785-159">b.</span><span class="sxs-lookup"><span data-stu-id="96785-159">b.</span></span> <span data-ttu-id="96785-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="96785-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span></span>

    <span data-ttu-id="96785-161">c.</span><span class="sxs-lookup"><span data-stu-id="96785-161">c.</span></span> <span data-ttu-id="96785-162">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://{SSO CONNECT SERVER}/sso-connect`</span><span class="sxs-lookup"><span data-stu-id="96785-162">In hello **Identifier** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="96785-163">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="96785-163">These values are not real.</span></span> <span data-ttu-id="96785-164">Bu değerleri hello gerçek yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="96785-164">Update these values with hello actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="96785-165">Kişi [Keeper parola Yöneticisi ve dijital kasası istemci desteği takım](https://keepersecurity.com/contact.html) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="96785-165">Contact [Keeper Password Manager & Digital Vault Client support team](https://keepersecurity.com/contact.html) tooget these values.</span></span> 

4. <span data-ttu-id="96785-166">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="96785-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_certificate.png) 

5. <span data-ttu-id="96785-168">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="96785-168">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="96785-170">Merhaba üzerinde **Keeper parola Yöneticisi & dijital kasası yapılandırma** 'yi tıklatın **Keeper parola Yöneticisi yapılandırma & dijital kasa** tooopen **oturum açmaYapılandırma**penceresi.</span><span class="sxs-lookup"><span data-stu-id="96785-170">On hello **Keeper Password Manager & Digital Vault Configuration** section, click **Configure Keeper Password Manager & Digital Vault** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="96785-171">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="96785-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_configure.png) 

7. <span data-ttu-id="96785-173">tooconfigure çoklu oturum açma üzerinde **Keeper parola Yöneticisi & dijital kasası yapılandırma** tarafı, sırasında verilen hello yönergeleri izleyin [Keeper destek Kılavuzu](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span><span class="sxs-lookup"><span data-stu-id="96785-173">tooconfigure single sign-on on **Keeper Password Manager & Digital Vault Configuration** side, follow hello guidelines given at [Keeper Support Guide](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span></span>

> [!TIP]
> <span data-ttu-id="96785-174">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="96785-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="96785-175">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="96785-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="96785-176">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="96785-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="96785-177">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="96785-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="96785-178">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="96785-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="96785-180">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="96785-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="96785-181">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="96785-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="96785-183">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="96785-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="96785-185">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="96785-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="96785-187">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="96785-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="96785-189">a.</span><span class="sxs-lookup"><span data-stu-id="96785-189">a.</span></span> <span data-ttu-id="96785-190">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="96785-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="96785-191">b.</span><span class="sxs-lookup"><span data-stu-id="96785-191">b.</span></span> <span data-ttu-id="96785-192">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="96785-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="96785-193">c.</span><span class="sxs-lookup"><span data-stu-id="96785-193">c.</span></span> <span data-ttu-id="96785-194">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="96785-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="96785-195">d.</span><span class="sxs-lookup"><span data-stu-id="96785-195">d.</span></span> <span data-ttu-id="96785-196">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="96785-196">Click **Create**.</span></span>
 
### <a name="creating-a-keeper-password-manager--digital-vault-test-user"></a><span data-ttu-id="96785-197">Keeper parola Yöneticisi & dijital kasası test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="96785-197">Creating a Keeper Password Manager & Digital Vault test user</span></span>

<span data-ttu-id="96785-198">tooenable Azure AD kullanıcıların toolog tooKeeper parola Yöneticisi & dijital kasası, bunlar Keeper parola Yöneticisi & dijital kasası sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="96785-198">tooenable Azure AD users toolog in tooKeeper Password Manager & Digital Vault, they must be provisioned into Keeper Password Manager & Digital Vault.</span></span> <span data-ttu-id="96785-199">Uygulama, süresi kullanıcı sağlama ve kimlik doğrulama kullanıcılar hello uygulamada otomatik olarak oluşturulacak sonra hemen destekler.</span><span class="sxs-lookup"><span data-stu-id="96785-199">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="96785-200">Sizinle iletişim [Keeper Destek](https://keepersecurity.com/contact.html)toosetup kullanıcıları el ile istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="96785-200">You can contact [Keeper Support](https://keepersecurity.com/contact.html), if you want toosetup users manually.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="96785-201">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="96785-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="96785-202">Bu bölümde, Azure çoklu oturum açma Britta Simon toouse vererek etkinleştirmeniz tooKeeper parola Yöneticisi & dijital kasası erişim.</span><span class="sxs-lookup"><span data-stu-id="96785-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKeeper Password Manager & Digital Vault.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="96785-204">**tooassign Britta Simon tooKeeper parola Yöneticisi & dijital kasası hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="96785-204">**tooassign Britta Simon tooKeeper Password Manager & Digital Vault, perform hello following steps:**</span></span>

1. <span data-ttu-id="96785-205">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="96785-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="96785-207">Merhaba uygulamalar listesinde **Keeper parola Yöneticisi & dijital kasa**.</span><span class="sxs-lookup"><span data-stu-id="96785-207">In hello applications list, select **Keeper Password Manager & Digital Vault**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_app.png) 

3. <span data-ttu-id="96785-209">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="96785-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="96785-211">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="96785-211">Click **Add** button.</span></span> <span data-ttu-id="96785-212">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="96785-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="96785-214">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="96785-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="96785-215">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="96785-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="96785-216">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="96785-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="96785-217">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="96785-217">Testing single sign-on</span></span>

<span data-ttu-id="96785-218">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="96785-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="96785-219">Merhaba Keeper parola Yöneticisi & hello erişim paneli dijital kasası parçasında tıkladığınızda, oturum açma sayfasına Keeper parola Yöneticisi & dijital kasası uygulamasının almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="96785-219">When you click hello Keeper Password Manager & Digital Vault tile in hello Access Panel, you should get login page of Keeper Password Manager & Digital Vault application.</span></span> <span data-ttu-id="96785-220">Başarılı kimlik doğrulaması sırasında hello uygulamasına almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="96785-220">Upon successful authentication, you should get into hello application.</span></span> <span data-ttu-id="96785-221">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="96785-221">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="96785-222">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="96785-222">Additional resources</span></span>

* [<span data-ttu-id="96785-223">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="96785-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="96785-224">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="96785-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_203.png

