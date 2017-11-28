---
title: "Öğretici: Azure Active Directory Tümleştirme Symantec Web güvenlik hizmetini (WSS) | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Symantec Web güvenlik hizmetini (WSS) arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: f4575e6f5eb63cd0e1d63edd35e30be3cacc3382
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="f4325-103">Öğretici: Azure Active Directory Tümleştirme Symantec Web güvenlik hizmetini (WSS)</span><span class="sxs-lookup"><span data-stu-id="f4325-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="f4325-104">Bu öğreticide, bilgi nasıl toointegrate Azure Active Directory (Azure AD) ile Symantec Web güvenlik hizmetini (WSS).</span><span class="sxs-lookup"><span data-stu-id="f4325-104">In this tutorial, you learn how toointegrate Symantec Web Security Service (WSS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f4325-105">Symantec Web güvenlik hizmetini (WSS) Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="f4325-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f4325-106">Erişim tooSymantec Web güvenlik hizmetini (WSS) sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f4325-106">You can control in Azure AD who has access tooSymantec Web Security Service (WSS)</span></span>
- <span data-ttu-id="f4325-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooSymantec (çoklu oturum açma) Web güvenlik hizmetini (WSS) etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f4325-107">You can enable your users tooautomatically get signed-on tooSymantec Web Security Service (WSS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f4325-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="f4325-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f4325-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f4325-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4325-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f4325-110">Prerequisites</span></span>

<span data-ttu-id="f4325-111">Azure AD tümleştirme Symantec Web güvenlik hizmetini (WSS) tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="f4325-111">tooconfigure Azure AD integration with Symantec Web Security Service (WSS), you need hello following items:</span></span>

- <span data-ttu-id="f4325-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="f4325-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f4325-113">Bir Symantec Web güvenlik hizmetini (WSS) çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="f4325-113">A Symantec Web Security Service (WSS) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f4325-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="f4325-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f4325-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="f4325-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f4325-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="f4325-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f4325-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f4325-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f4325-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="f4325-118">Scenario description</span></span>
<span data-ttu-id="f4325-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="f4325-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f4325-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="f4325-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f4325-121">Merhaba Galerisi'nden Symantec Web güvenlik hizmetini (WSS) ekleme</span><span class="sxs-lookup"><span data-stu-id="f4325-121">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
2. <span data-ttu-id="f4325-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f4325-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a><span data-ttu-id="f4325-123">Merhaba Galerisi'nden Symantec Web güvenlik hizmetini (WSS) ekleme</span><span class="sxs-lookup"><span data-stu-id="f4325-123">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
<span data-ttu-id="f4325-124">tooconfigure hello tümleştirmeye Symantec Web güvenlik hizmetini (WSS) Azure AD, hello galeri tooyour yönetilen SaaS uygulamaları listesinden tooadd Symantec Web güvenlik hizmetini (WSS) gerekir.</span><span class="sxs-lookup"><span data-stu-id="f4325-124">tooconfigure hello integration of Symantec Web Security Service (WSS) into Azure AD, you need tooadd Symantec Web Security Service (WSS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f4325-125">**tooadd hello galerisinden Symantec Web güvenlik hizmetini (WSS) hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f4325-125">**tooadd Symantec Web Security Service (WSS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4325-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f4325-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f4325-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="f4325-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f4325-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f4325-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="f4325-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f4325-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="f4325-133">Merhaba arama kutusuna yazın **Symantec Web güvenlik hizmetini (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="f4325-133">In hello search box, type **Symantec Web Security Service (WSS)**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_search.png)

5. <span data-ttu-id="f4325-135">Merhaba Sonuçlar panelinde seçin **Symantec Web güvenlik hizmetini (WSS)**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="f4325-135">In hello results panel, select **Symantec Web Security Service (WSS)**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f4325-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f4325-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f4325-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile Symantec Web güvenlik hizmeti ("Britta Simon" adlı bir test kullanıcı tabanlı WSS) test etme.</span><span class="sxs-lookup"><span data-stu-id="f4325-138">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f4325-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Symantec Web güvenlik hizmetini (WSS) tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="f4325-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Symantec Web Security Service (WSS) is tooa user in Azure AD.</span></span> <span data-ttu-id="f4325-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Symantec Web güvenlik hizmetini (WSS) arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="f4325-140">In other words, a link relationship between an Azure AD user and hello related user in Symantec Web Security Service (WSS) needs toobe established.</span></span>

<span data-ttu-id="f4325-141">Symantec Web güvenlik hizmetini (WSS) içindeki hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="f4325-141">In Symantec Web Security Service (WSS), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f4325-142">tooconfigure ve test Symantec Web güvenlik hizmetini (WSS) Azure AD çoklu oturum açma, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="f4325-142">tooconfigure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f4325-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="f4325-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f4325-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="f4325-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f4325-145">**[Symantec Web güvenlik hizmetini (WSS) test kullanıcısı oluşturma](#creating-a-symantec-web-security-service-wss-test-user)**  -toohave karşılık gelen, Britta Simon Symantec Web güvenlik hizmetini (WSS), kullanıcı bağlantılı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="f4325-145">**[Creating a Symantec Web Security Service (WSS) test user](#creating-a-symantec-web-security-service-wss-test-user)** - toohave a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f4325-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="f4325-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f4325-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="f4325-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f4325-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f4325-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f4325-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Symantec Web güvenlik hizmetini (WSS) uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f4325-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="f4325-150">**tooconfigure Symantec Web güvenlik hizmetini (WSS) ile Azure AD çoklu oturum açma hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f4325-150">**tooconfigure Azure AD single sign-on with Symantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="f4325-151">Hello hello üzerinde Azure portal'ın **Symantec Web güvenlik hizmetini (WSS)** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="f4325-151">In hello Azure portal, on hello **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="f4325-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="f4325-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="f4325-155">Merhaba üzerinde **Symantec Web güvenlik hizmetini (WSS) etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f4325-155">On hello **Symantec Web Security Service (WSS) Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="f4325-157">a.</span><span class="sxs-lookup"><span data-stu-id="f4325-157">a.</span></span> <span data-ttu-id="f4325-158">Merhaba, **oturum açma URL'si** metin kutusuna, toohello engelleme İlkesi hello Symantec Web güvenlik hizmetini (WSS) göre tooblock istediğiniz Bahsetme hello url.</span><span class="sxs-lookup"><span data-stu-id="f4325-158">In hello **Sign-on URL** textbox, mention hello url, which you want tooblock according toohello blocking policy of hello Symantec Web Security Service (WSS).</span></span>  
    
    <span data-ttu-id="f4325-159">b.</span><span class="sxs-lookup"><span data-stu-id="f4325-159">b.</span></span> <span data-ttu-id="f4325-160">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="f4325-160">In hello **Identifier** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f4325-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="f4325-161">These values are not real.</span></span> <span data-ttu-id="f4325-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="f4325-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f4325-163">Kişi [Symantec Web güvenlik hizmetini (WSS) istemci destek ekibi](https://www.symantec.com/contact-us) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="f4325-163">Contact [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) tooget these values.</span></span> 

4. <span data-ttu-id="f4325-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f4325-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="f4325-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f4325-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f4325-168">tooconfigure çoklu oturum açma üzerinde **Symantec Web güvenlik hizmetini (WSS)** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[Symantec Web güvenlik hizmetini (WSS) destek ekibi](https://www.symantec.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="f4325-168">tooconfigure single sign-on on **Symantec Web Security Service (WSS)** side, you need toosend hello downloaded **Metadata XML** too[Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="f4325-169">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="f4325-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f4325-170">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="f4325-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f4325-171">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f4325-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f4325-172">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f4325-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="f4325-173">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="f4325-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="f4325-175">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f4325-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4325-176">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f4325-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f4325-178">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f4325-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f4325-180">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="f4325-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f4325-182">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f4325-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f4325-184">a.</span><span class="sxs-lookup"><span data-stu-id="f4325-184">a.</span></span> <span data-ttu-id="f4325-185">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f4325-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f4325-186">b.</span><span class="sxs-lookup"><span data-stu-id="f4325-186">b.</span></span> <span data-ttu-id="f4325-187">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="f4325-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f4325-188">c.</span><span class="sxs-lookup"><span data-stu-id="f4325-188">c.</span></span> <span data-ttu-id="f4325-189">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="f4325-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f4325-190">d.</span><span class="sxs-lookup"><span data-stu-id="f4325-190">d.</span></span> <span data-ttu-id="f4325-191">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f4325-191">Click **Create**.</span></span>
 
### <a name="creating-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="f4325-192">Symantec Web güvenlik hizmetini (WSS) test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f4325-192">Creating a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="f4325-193">Bu bölümde, Britta Simon Symantec Web güvenlik hizmetini (WSS) adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f4325-193">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="f4325-194">Çalışmak [Symantec Web güvenlik hizmetini (WSS) destek ekibi](https://www.symantec.com/contact-us) hello Symantec Web güvenlik hizmetini (WSS) platformu hello kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="f4325-194">Work with [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) to add hello users in hello Symantec Web Security Service (WSS) platform.</span></span> <span data-ttu-id="f4325-195">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="f4325-195">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="f4325-196">Ayrıca hello yanı sıra kullanıcı, ayrıntıları toosend tooaccess hello uygulama içinden çalıştığınız hello makinenin ortak IPADDRESS hello.</span><span class="sxs-lookup"><span data-stu-id="f4325-196">Also along with hello user details you need toosend hello public IPaddress of hello machine from which you are trying tooaccess hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="f4325-197">Lütfen [burayı](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget makinenizi ortak IP adresi.</span><span class="sxs-lookup"><span data-stu-id="f4325-197">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget your machine's public IPaddress.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f4325-198">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="f4325-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f4325-199">Bu bölümde, erişim tooSymantec Web güvenlik hizmetini (WSS) vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f4325-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSymantec Web Security Service (WSS).</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="f4325-201">**tooassign Britta Simon tooSymantec Web güvenlik hizmetini (WSS) hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f4325-201">**tooassign Britta Simon tooSymantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="f4325-202">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f4325-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="f4325-204">Merhaba uygulamalar listesinde **Symantec Web güvenlik hizmetini (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="f4325-204">In hello applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_app.png) 

3. <span data-ttu-id="f4325-206">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="f4325-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="f4325-208">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f4325-208">Click **Add** button.</span></span> <span data-ttu-id="f4325-209">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f4325-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="f4325-211">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="f4325-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f4325-212">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f4325-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f4325-213">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f4325-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f4325-214">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="f4325-214">Testing single sign-on</span></span>

<span data-ttu-id="f4325-215">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="f4325-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f4325-216">Symantec Web güvenlik hizmetini (WSS) hello erişim paneli döşeme hello tıkladığınızda, ilke engelleme hello yapılandırılmış sayfa engelleme yeniden yönlendirilen toohello alın.</span><span class="sxs-lookup"><span data-stu-id="f4325-216">When you click hello Symantec Web Security Service (WSS) tile in hello Access Panel, you get redirected toohello blocking page for which hello blocking policy has been configured.</span></span>
<span data-ttu-id="f4325-217">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f4325-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f4325-218">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f4325-218">Additional resources</span></span>

* [<span data-ttu-id="f4325-219">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="f4325-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f4325-220">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="f4325-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_203.png

