---
title: "Öğretici: Azure Active Directory Tümleştirme TigerText güvenli Messenger ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile TigerText güvenli Messenger arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: a3d7bb9598658c75c567c15751740d885fe4fc27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="7fc2e-103">Öğretici: Azure Active Directory Tümleştirme TigerText güvenli Messenger ile</span><span class="sxs-lookup"><span data-stu-id="7fc2e-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>

<span data-ttu-id="7fc2e-104">Bu öğreticide, bilgi TigerText güvenli toointegrate Messenger nasıl Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-104">In this tutorial, you learn how toointegrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7fc2e-105">TigerText güvenli Messenger Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="7fc2e-105">Integrating TigerText Secure Messenger with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7fc2e-106">Güvenli Messenger erişim tooTigerText sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7fc2e-106">You can control in Azure AD who has access tooTigerText Secure Messenger</span></span>
- <span data-ttu-id="7fc2e-107">Oturum açma, kullanıcıların tooautomatically get tooTigerText etkinleştirebilirsiniz kendi Azure AD hesapları ile güvenli Messenger (çoklu oturum açma)</span><span class="sxs-lookup"><span data-stu-id="7fc2e-107">You can enable your users tooautomatically get signed-on tooTigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7fc2e-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="7fc2e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7fc2e-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7fc2e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fc2e-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7fc2e-110">Prerequisites</span></span>

<span data-ttu-id="7fc2e-111">tooconfigure TigerText güvenli Messenger ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7fc2e-111">tooconfigure Azure AD integration with TigerText Secure Messenger, you need hello following items:</span></span>

- <span data-ttu-id="7fc2e-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="7fc2e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7fc2e-113">Bir TigerText güvenli Messenger çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="7fc2e-113">A TigerText Secure Messenger single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7fc2e-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7fc2e-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="7fc2e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7fc2e-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7fc2e-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7fc2e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7fc2e-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="7fc2e-118">Scenario description</span></span>
<span data-ttu-id="7fc2e-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7fc2e-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="7fc2e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7fc2e-121">Merhaba Galerisi'nden TigerText güvenli Messenger ekleme</span><span class="sxs-lookup"><span data-stu-id="7fc2e-121">Add TigerText Secure Messenger from hello gallery</span></span>
2. <span data-ttu-id="7fc2e-122">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="7fc2e-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tigertext-secure-messenger-from-hello-gallery"></a><span data-ttu-id="7fc2e-123">Merhaba Galerisi'nden TigerText güvenli Messenger ekleme</span><span class="sxs-lookup"><span data-stu-id="7fc2e-123">Add TigerText Secure Messenger from hello gallery</span></span>
<span data-ttu-id="7fc2e-124">Azure AD'ye tooconfigure hello tümleştirme TigerText güvenli Messenger tooadd TigerText güvenli Messenger hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-124">tooconfigure hello integration of TigerText Secure Messenger into Azure AD, you need tooadd TigerText Secure Messenger from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7fc2e-125">**tooadd TigerText güvenli Messenger hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7fc2e-125">**tooadd TigerText Secure Messenger from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7fc2e-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7fc2e-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7fc2e-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="7fc2e-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="7fc2e-133">Merhaba arama kutusuna yazın **TigerText güvenli Messenger**seçin **TigerText güvenli Messenger** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-133">In hello search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Galerisi'nden ekleme](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7fc2e-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="7fc2e-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="7fc2e-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı TigerText güvenli Messenger ile test etme.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7fc2e-137">Tek toowork'ın oturum açma hangi hello karşılık gelen TigerText güvenli Messenger tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TigerText Secure Messenger is tooa user in Azure AD.</span></span> <span data-ttu-id="7fc2e-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve TigerText güvenli Messenger hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-138">In other words, a link relationship between an Azure AD user and hello related user in TigerText Secure Messenger needs toobe established.</span></span>

<span data-ttu-id="7fc2e-139">Merhaba hello değeri TigerText güvenli Messenger'da atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-139">In TigerText Secure Messenger, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7fc2e-140">tooconfigure ve TigerText güvenli Messenger ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7fc2e-140">tooconfigure and test Azure AD single sign-on with TigerText Secure Messenger, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7fc2e-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7fc2e-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7fc2e-143">**[TigerText güvenli Messenger test kullanıcısı oluşturma](#create-a-tigertext-secure-messenger-test-user)**  -toohave karşılık gelen, Britta Simon TigerText güvenli Messenger kullanıcı bağlantılı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - toohave a counterpart of Britta Simon in TigerText Secure Messenger that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7fc2e-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7fc2e-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7fc2e-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="7fc2e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7fc2e-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma TigerText güvenli Messenger uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span></span>

<span data-ttu-id="7fc2e-148">**Azure AD çoklu oturum açma tooconfigure güvenli TigerText Messenger ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7fc2e-148">**tooconfigure Azure AD single sign-on with TigerText Secure Messenger, perform hello following steps:**</span></span>

1. <span data-ttu-id="7fc2e-149">Hello hello üzerinde Azure portal'ın **TigerText güvenli Messenger** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-149">In hello Azure portal, on hello **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="7fc2e-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML tabanlı oturum açma](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_samlbase.png)

3. <span data-ttu-id="7fc2e-153">Merhaba üzerinde **TigerText güvenli Messenger etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7fc2e-153">On hello **TigerText Secure Messenger Domain and URLs** section, perform hello following steps:</span></span>

    ![TigerText güvenli Messenger etki alanı ve URL'ler bölümü](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_url.png)

    <span data-ttu-id="7fc2e-155">a.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-155">a.</span></span> <span data-ttu-id="7fc2e-156">Merhaba, **oturum açma URL'si** metin kutusuna, türü URL'si olarak:`https://home.tigertext.com`</span><span class="sxs-lookup"><span data-stu-id="7fc2e-156">In hello **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span></span>

    <span data-ttu-id="7fc2e-157">b.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-157">b.</span></span> <span data-ttu-id="7fc2e-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span><span class="sxs-lookup"><span data-stu-id="7fc2e-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7fc2e-159">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-159">This value is not real.</span></span> <span data-ttu-id="7fc2e-160">Bu değer ile Merhaba güncelleştirme gerçek tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-160">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="7fc2e-161">Kişi [TigerText güvenli Messenger istemci destek ekibi](mailTo:prosupport@tigertext.com) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="7fc2e-162">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![SAML imzalama sertifikası bölümü](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_certificate.png) 

5. <span data-ttu-id="7fc2e-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-164">Click **Save** button.</span></span>

    ![Kaydet Düğmesi](./media/active-directory-saas-tigertext-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7fc2e-166">tooget tek kişi, uygulamanız için yapılandırılmış oturum [TigerText güvenli Messenger destek ekibi](mailTo:prosupport@tigertext.com) ve hello verin **yüklenen meta veri**.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-166">tooget single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them hello **Downloaded metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="7fc2e-167">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="7fc2e-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7fc2e-168">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7fc2e-169">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7fc2e-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7fc2e-170">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7fc2e-170">Create an Azure AD test user</span></span>
<span data-ttu-id="7fc2e-171">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="7fc2e-173">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7fc2e-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7fc2e-174">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tigertext-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7fc2e-176">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Kullanıcıların ve grupların tüm kullanıcılar ->](./media/active-directory-saas-tigertext-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7fc2e-178">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Ekle düğmesi](./media/active-directory-saas-tigertext-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7fc2e-180">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7fc2e-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-tigertext-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7fc2e-182">a.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-182">a.</span></span> <span data-ttu-id="7fc2e-183">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7fc2e-184">b.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-184">b.</span></span> <span data-ttu-id="7fc2e-185">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7fc2e-186">c.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-186">c.</span></span> <span data-ttu-id="7fc2e-187">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7fc2e-188">d.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-188">d.</span></span> <span data-ttu-id="7fc2e-189">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-189">Click **Create**.</span></span>
 
### <a name="create-a-tigertext-secure-messenger-test-user"></a><span data-ttu-id="7fc2e-190">TigerText güvenli Messenger test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7fc2e-190">Create a TigerText Secure Messenger test user</span></span>

<span data-ttu-id="7fc2e-191">Bu bölümde, TigerText içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-191">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="7fc2e-192">Lütfen çok ulaşmak[TigerText güvenli Messenger istemci destek ekibi](mailTo:prosupport@tigertext.com) tooadd hello kullanıcılar hello TigerText Platform.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-192">Please reach out too[TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) tooadd hello users in hello TigerText platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7fc2e-193">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="7fc2e-193">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7fc2e-194">Bu bölümde, Azure çoklu oturum açma Britta Simon toouse erişim tooTigerText vererek etkinleştirmeniz güvenli Messenger.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTigerText Secure Messenger.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="7fc2e-196">**tooassign Britta Simon tooTigerText güvenli Messenger hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7fc2e-196">**tooassign Britta Simon tooTigerText Secure Messenger, perform hello following steps:**</span></span>

1. <span data-ttu-id="7fc2e-197">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="7fc2e-199">Merhaba uygulamalar listesinde **TigerText güvenli Messenger**.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-199">In hello applications list, select **TigerText Secure Messenger**.</span></span>

    ![TigerText güvenli Messenger'da uygulama listesi](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_app.png) 

3. <span data-ttu-id="7fc2e-201">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="7fc2e-203">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-203">Click **Add** button.</span></span> <span data-ttu-id="7fc2e-204">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="7fc2e-206">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7fc2e-207">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7fc2e-208">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7fc2e-209">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="7fc2e-209">Test single sign-on</span></span>

<span data-ttu-id="7fc2e-210">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7fc2e-211">Merhaba TigerText hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour TigerText uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fc2e-211">When you click hello TigerText tile in hello Access Panel, you should get automatically signed-on tooyour TigerText application.</span></span> <span data-ttu-id="7fc2e-212">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7fc2e-212">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7fc2e-213">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7fc2e-213">Additional resources</span></span>

* [<span data-ttu-id="7fc2e-214">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="7fc2e-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7fc2e-215">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="7fc2e-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_203.png

