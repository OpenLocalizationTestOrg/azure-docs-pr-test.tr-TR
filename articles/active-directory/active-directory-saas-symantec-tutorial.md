---
title: "Öğretici: Azure Active Directory Tümleştirme Symantec Web güvenlik hizmetini (WSS) | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Symantec Web güvenlik hizmetini (WSS) arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9f02b3d4ce2073110c55af4b567b0e3b5a88404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="3d40e-103">Öğretici: Azure Active Directory Tümleştirme Symantec Web güvenlik hizmetini (WSS)</span><span class="sxs-lookup"><span data-stu-id="3d40e-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="3d40e-104">Bu öğreticide, WSS hello Azure AD sağlanan bir son kullanıcı doğrulanabilmesi toointegrate Azure Active Directory (Azure AD) hesabınızla, Symantec Web güvenlik hizmetini (WSS) nasıl hesap öğreneceksiniz SAML kimlik doğrulaması kullanarak ve kullanıcı zorunlu veya grubu düzeyi ilkesi kuralları.</span><span class="sxs-lookup"><span data-stu-id="3d40e-104">In this tutorial, you will learn how toointegrate your Symantec Web Security Service (WSS) account with your Azure Active Directory (Azure AD) account so that WSS can authenticate an end user provisioned in hello Azure AD using SAML authentication and enforce user or group level policy rules.</span></span>

<span data-ttu-id="3d40e-105">Symantec Web güvenlik hizmetini (WSS) Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="3d40e-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3d40e-106">Tüm hello son kullanıcılar ve gruplar WSS hesabınızdan, Azure AD portalı tarafından kullanılan yönetin.</span><span class="sxs-lookup"><span data-stu-id="3d40e-106">Manage all of hello end users and groups used by your WSS account from your Azure AD portal.</span></span> 

- <span data-ttu-id="3d40e-107">Merhaba son kullanıcıların tooauthenticate kendilerini Azure AD kimlik bilgilerini kullanarak WSS içindeki izin verir.</span><span class="sxs-lookup"><span data-stu-id="3d40e-107">Allow hello end users tooauthenticate themselves in WSS using their Azure AD credentials.</span></span>

- <span data-ttu-id="3d40e-108">Kullanıcının Hello zorlama etkinleştirmek ve WSS hesabınızda tanımlanan düzeyi ilke kuralları gruplayın.</span><span class="sxs-lookup"><span data-stu-id="3d40e-108">Enable hello enforcement of user and group level policy rules defined in your WSS account.</span></span>

<span data-ttu-id="3d40e-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3d40e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d40e-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3d40e-110">Prerequisites</span></span>

<span data-ttu-id="3d40e-111">Azure AD tümleştirme Symantec Web güvenlik hizmetini (WSS) tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="3d40e-111">tooconfigure Azure AD integration with Symantec Web Security Service (WSS), you need hello following items:</span></span>

- <span data-ttu-id="3d40e-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="3d40e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3d40e-113">Bir Symantec Web güvenlik hizmetini (WSS) hesabı</span><span class="sxs-lookup"><span data-stu-id="3d40e-113">A Symantec Web Security Service (WSS) account</span></span>

> [!NOTE]
> <span data-ttu-id="3d40e-114">tootest hello bu öğreticideki adımlar, üretim amaç için kullanılmakta olan bir WSS hesabı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="3d40e-114">tootest hello steps in this tutorial, we do not recommend using a WSS account that is currently being used for production purpose.</span></span>

<span data-ttu-id="3d40e-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="3d40e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3d40e-116">Gerekli olmadığı sürece, şu anda bu test için üretim amaçla kullanılan WSS hesabınızı kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="3d40e-116">Do not use your WSS account that is currently being used for production purpose for this test unless it is necessary.</span></span>
- <span data-ttu-id="3d40e-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d40e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3d40e-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="3d40e-118">Scenario description</span></span>
<span data-ttu-id="3d40e-119">Bu öğreticide, Azure AD hesabınızda tanımlanan hello son kullanıcı kimlik bilgilerini kullanarak, Azure AD tooenable tek oturum açma tooWSS yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="3d40e-119">In this tutorial, you will configure your Azure AD tooenable single sign-on tooWSS using hello end user credentials defined in your Azure AD account.</span></span>
<span data-ttu-id="3d40e-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="3d40e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3d40e-121">Merhaba Galerisi'nden Hello Symantec Web güvenlik hizmetini (WSS) uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="3d40e-121">Adding hello Symantec Web Security Service (WSS) app from hello gallery</span></span>
2. <span data-ttu-id="3d40e-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="3d40e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a><span data-ttu-id="3d40e-123">Merhaba Galerisi'nden Symantec Web güvenlik hizmetini (WSS) ekleme</span><span class="sxs-lookup"><span data-stu-id="3d40e-123">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
<span data-ttu-id="3d40e-124">tooconfigure hello tümleştirmeye Symantec Web güvenlik hizmetini (WSS) Azure AD, hello galeri tooyour yönetilen SaaS uygulamaları listesinden tooadd Symantec Web güvenlik hizmetini (WSS) gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d40e-124">tooconfigure hello integration of Symantec Web Security Service (WSS) into Azure AD, you need tooadd Symantec Web Security Service (WSS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3d40e-125">**tooadd hello galerisinden Symantec Web güvenlik hizmetini (WSS) hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3d40e-125">**tooadd Symantec Web Security Service (WSS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d40e-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3d40e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="3d40e-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="3d40e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3d40e-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3d40e-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="3d40e-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3d40e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="3d40e-133">Merhaba arama kutusuna yazın **Symantec Web güvenlik hizmetini (WSS)**seçin **Symantec Web güvenlik hizmetini (WSS)** sonuç panelinden ardından **Ekle** düğmesini tooadd hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="3d40e-133">In hello search box, type **Symantec Web Security Service (WSS)**, select **Symantec Web Security Service (WSS)** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde Symantec Web güvenlik hizmetini (WSS)](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3d40e-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="3d40e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3d40e-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile Symantec Web güvenlik hizmeti ("Britta Simon" adlı bir test kullanıcı tabanlı WSS) test etme.</span><span class="sxs-lookup"><span data-stu-id="3d40e-136">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3d40e-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Symantec Web güvenlik hizmetini (WSS) tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d40e-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Symantec Web Security Service (WSS) is tooa user in Azure AD.</span></span> <span data-ttu-id="3d40e-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Symantec Web güvenlik hizmetini (WSS) arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d40e-138">In other words, a link relationship between an Azure AD user and hello related user in Symantec Web Security Service (WSS) needs toobe established.</span></span>

<span data-ttu-id="3d40e-139">Symantec Web güvenlik hizmetini (WSS) içindeki hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="3d40e-139">In Symantec Web Security Service (WSS), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3d40e-140">tooconfigure ve test Symantec Web güvenlik hizmetini (WSS) Azure AD çoklu oturum açma, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="3d40e-140">tooconfigure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3d40e-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="3d40e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3d40e-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="3d40e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3d40e-143">**[Symantec Web güvenlik hizmetini (WSS) test kullanıcısı oluşturma](#create-a-symantec-web-security-service-wss-test-user)**  -toohave karşılık gelen, Britta Simon Symantec Web güvenlik hizmetini (WSS), kullanıcı bağlantılı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="3d40e-143">**[Create a Symantec Web Security Service (WSS) test user](#create-a-symantec-web-security-service-wss-test-user)** - toohave a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3d40e-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="3d40e-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3d40e-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="3d40e-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3d40e-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="3d40e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3d40e-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Symantec Web güvenlik hizmetini (WSS) uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3d40e-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="3d40e-148">**tooconfigure Symantec Web güvenlik hizmetini (WSS) ile Azure AD çoklu oturum açma hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3d40e-148">**tooconfigure Azure AD single sign-on with Symantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="3d40e-149">Hello hello üzerinde Azure portal'ın **Symantec Web güvenlik hizmetini (WSS)** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="3d40e-149">In hello Azure portal, on hello **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="3d40e-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="3d40e-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="3d40e-153">Merhaba üzerinde **Symantec Web güvenlik hizmetini (WSS) etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3d40e-153">On hello **Symantec Web Security Service (WSS) Domain and URLs** section, perform hello following steps:</span></span>

    ![Symantec Web güvenlik hizmetini (WSS) etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="3d40e-155">a.</span><span class="sxs-lookup"><span data-stu-id="3d40e-155">a.</span></span> <span data-ttu-id="3d40e-156">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="3d40e-156">In hello **Identifier** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    <span data-ttu-id="3d40e-157">b.</span><span class="sxs-lookup"><span data-stu-id="3d40e-157">b.</span></span> <span data-ttu-id="3d40e-158">Merhaba, **yanıt URL'si** metin kutusuna, türü hello URL'si:`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span><span class="sxs-lookup"><span data-stu-id="3d40e-158">In hello **Reply URL** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span></span>

    > [!NOTE]
    > <span data-ttu-id="3d40e-159">Merhaba temasa [Symantec Web güvenlik hizmetini (WSS) istemci destek ekibi](https://www.symantec.com/contact-us) için hello başlangıç değerleri, **tanımlayıcısı** ve **yanıt URL'si** herhangi bir nedenden dolayı çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="3d40e-159">Please contact hello [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) if hello values for hello **Identifier** and **Reply URL** are not working for some reason.</span></span>

4. <span data-ttu-id="3d40e-160">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3d40e-160">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="3d40e-162">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3d40e-162">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="3d40e-164">tooconfigure çoklu oturum açma hello Symantec Web güvenlik hizmetini (WSS) yan üzerinde toohello WSS çevrimiçi belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="3d40e-164">tooconfigure single sign-on on hello Symantec Web Security Service (WSS) side, refer toohello WSS online documentation.</span></span> <span data-ttu-id="3d40e-165">indirilen hello **meta veri XML** dosya hello WSS Portalı'na içeri toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d40e-165">hello downloaded **Metadata XML** file will need toobe imported into hello WSS portal.</span></span> <span data-ttu-id="3d40e-166">Kişi hello [Symantec Web güvenlik hizmetini (WSS) destek ekibi](https://www.symantec.com/contact-us) hello WSS portal hello yapılandırmasına yardıma ihtiyacınız varsa.</span><span class="sxs-lookup"><span data-stu-id="3d40e-166">Contact hello [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) if you need assistance with hello configuration on hello WSS portal.</span></span>

> [!TIP]
> <span data-ttu-id="3d40e-167">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="3d40e-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3d40e-168">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="3d40e-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3d40e-169">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3d40e-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3d40e-170">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3d40e-170">Create an Azure AD test user</span></span>

<span data-ttu-id="3d40e-171">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="3d40e-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="3d40e-173">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3d40e-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d40e-174">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3d40e-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3d40e-176">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="3d40e-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3d40e-178">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="3d40e-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3d40e-180">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3d40e-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3d40e-182">a.</span><span class="sxs-lookup"><span data-stu-id="3d40e-182">a.</span></span> <span data-ttu-id="3d40e-183">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3d40e-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3d40e-184">b.</span><span class="sxs-lookup"><span data-stu-id="3d40e-184">b.</span></span> <span data-ttu-id="3d40e-185">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="3d40e-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="3d40e-186">c.</span><span class="sxs-lookup"><span data-stu-id="3d40e-186">c.</span></span> <span data-ttu-id="3d40e-187">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="3d40e-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="3d40e-188">d.</span><span class="sxs-lookup"><span data-stu-id="3d40e-188">d.</span></span> <span data-ttu-id="3d40e-189">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3d40e-189">Click **Create**.</span></span>
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="3d40e-190">Symantec Web güvenlik hizmetini (WSS) test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3d40e-190">Create a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="3d40e-191">Bu bölümde, Britta Simon Symantec Web güvenlik hizmetini (WSS) adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3d40e-191">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="3d40e-192">Merhaba karşılık gelen son kullanıcı adı hello WSS Portalı'nda el ile oluşturulabilir veya hello kullanıcıları/grupları (~ 15 dakika) birkaç dakika sonra hello Azure AD'ye eşitlenen toobe toohello WSS Portalı'nda sağlanan bekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d40e-192">hello corresponding end username can be manually created in hello WSS portal or you can wait for hello users/groups provisioned in hello Azure AD toobe synchronized toohello WSS portal after a few minutes (~15 minutes).</span></span> <span data-ttu-id="3d40e-193">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="3d40e-193">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="3d40e-194">kullanılan toobrowse Web siteleri olacaktır hello son kullanıcı makinenin Hello ortak IP adresini de hello Symantec Web güvenlik hizmetini (WSS) Portalı'nda sağlanan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d40e-194">hello public IP address of hello end user machine, which will be used toobrowse websites also need toobe provisioned in hello Symantec Web Security Service (WSS) portal.</span></span>

> [!NOTE]
> <span data-ttu-id="3d40e-195">Lütfen [burayı](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget makinenizi ortak IP adresi.</span><span class="sxs-lookup"><span data-stu-id="3d40e-195">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget your machine's public IPaddress.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="3d40e-196">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="3d40e-196">Assign hello Azure AD test user</span></span>

<span data-ttu-id="3d40e-197">Bu bölümde, erişim tooSymantec Web güvenlik hizmetini (WSS) vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="3d40e-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSymantec Web Security Service (WSS).</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="3d40e-199">**tooassign Britta Simon tooSymantec Web güvenlik hizmetini (WSS) hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3d40e-199">**tooassign Britta Simon tooSymantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="3d40e-200">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3d40e-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="3d40e-202">Merhaba uygulamalar listesinde **Symantec Web güvenlik hizmetini (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="3d40e-202">In hello applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![Merhaba uygulamalar listesinde Hello Symantec Web güvenlik hizmetini (WSS) bağlantısı](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. <span data-ttu-id="3d40e-204">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="3d40e-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="3d40e-206">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3d40e-206">Click **Add** button.</span></span> <span data-ttu-id="3d40e-207">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3d40e-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="3d40e-209">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="3d40e-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3d40e-210">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3d40e-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3d40e-211">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3d40e-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3d40e-212">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="3d40e-212">Test single sign-on</span></span>

<span data-ttu-id="3d40e-213">Bu bölümde, WSS hesap toouse yapılandırdığınız göre hello çoklu oturum açma işlevselliğini test edeceksiniz SAML kimlik doğrulaması için Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d40e-213">In this section, you'll test hello single sign-on functionality now that you've configured your WSS account toouse your Azure AD for SAML authentication.</span></span>

<span data-ttu-id="3d40e-214">Web tarayıcınızı açın ve sonra da yeniden yönlendirilen toohello Azure oturum açma sayfası olacak toobrowse tooa site çalışırsanız, web tarayıcısı tooproxy trafiği tooWSS yapılandırdıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="3d40e-214">After you have configured your web browser tooproxy traffic tooWSS, when you open your web browser and try toobrowse tooa site then you'll be redirected toohello Azure sign-on page.</span></span> <span data-ttu-id="3d40e-215">Hello Azure AD (diğer bir deyişle, BrittaSimon) sağlanmış hello test son kullanıcı Hello kimlik bilgilerini girin ve ilişkili parola.</span><span class="sxs-lookup"><span data-stu-id="3d40e-215">Enter hello credentials of hello test end user that has been provisioned in hello Azure AD (that is, BrittaSimon) and associated password.</span></span> <span data-ttu-id="3d40e-216">Kimlik doğrulaması yapıldıktan sonra seçtiğiniz mümkün toobrowse toohello Web sitesi olması.</span><span class="sxs-lookup"><span data-stu-id="3d40e-216">Once authenticated, you'll be able toobrowse toohello website that you chose.</span></span> <span data-ttu-id="3d40e-217">Kullanıcı olarak BrittaSimon toobrowse toothat site çalıştığınızda hello WSS blok sayfasını görmelisiniz sonra tooa belirli bir siteye gözatma hello WSS yan tooblock BrittaSimon ilke kuralı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d40e-217">Should you create a policy rule on hello WSS side tooblock BrittaSimon from browsing tooa particular site then you should see hello WSS block page when you attempt toobrowse toothat site as user BrittaSimon.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3d40e-218">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3d40e-218">Additional resources</span></span>

* [<span data-ttu-id="3d40e-219">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="3d40e-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3d40e-220">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="3d40e-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

