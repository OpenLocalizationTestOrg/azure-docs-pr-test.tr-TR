---
title: "Öğretici: Azure Active Directory Tümleştirme Thoughtworks Mingle ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory arasındaki Thoughtworks Mingle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c17f8e13d2db3de7d228d9b27128d134f98d6cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="0ce62-103">Öğretici: Azure Active Directory Tümleştirme Thoughtworks Mingle ile</span><span class="sxs-lookup"><span data-stu-id="0ce62-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>

<span data-ttu-id="0ce62-104">Bu öğreticide, bilgi toointegrate Thoughtworks Azure Active Directory (Azure AD) ile Mingle nasıl.</span><span class="sxs-lookup"><span data-stu-id="0ce62-104">In this tutorial, you learn how toointegrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0ce62-105">Azure AD ile tümleştirme Thoughtworks Mingle ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="0ce62-105">Integrating Thoughtworks Mingle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0ce62-106">Erişim tooThoughtworks Mingle sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0ce62-106">You can control in Azure AD who has access tooThoughtworks Mingle</span></span>
- <span data-ttu-id="0ce62-107">Kullanıcıların tooautomatically get açan tooThoughtworks Mingle (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0ce62-107">You can enable your users tooautomatically get signed-on tooThoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0ce62-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="0ce62-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0ce62-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0ce62-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ce62-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0ce62-110">Prerequisites</span></span>

<span data-ttu-id="0ce62-111">tooconfigure Thoughtworks Mingle ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0ce62-111">tooconfigure Azure AD integration with Thoughtworks Mingle, you need hello following items:</span></span>

- <span data-ttu-id="0ce62-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="0ce62-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0ce62-113">Bir Thoughtworks Mingle çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="0ce62-113">A Thoughtworks Mingle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0ce62-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="0ce62-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0ce62-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="0ce62-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0ce62-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="0ce62-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0ce62-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0ce62-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0ce62-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="0ce62-118">Scenario description</span></span>
<span data-ttu-id="0ce62-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="0ce62-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0ce62-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="0ce62-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0ce62-121">Thoughtworks Mingle hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="0ce62-121">Adding Thoughtworks Mingle from hello gallery</span></span>
2. <span data-ttu-id="0ce62-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0ce62-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thoughtworks-mingle-from-hello-gallery"></a><span data-ttu-id="0ce62-123">Thoughtworks Mingle hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="0ce62-123">Adding Thoughtworks Mingle from hello gallery</span></span>
<span data-ttu-id="0ce62-124">Azure AD'ye tooconfigure hello tümleştirme Thoughtworks Mingle, tooadd Thoughtworks Mingle hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ce62-124">tooconfigure hello integration of Thoughtworks Mingle into Azure AD, you need tooadd Thoughtworks Mingle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0ce62-125">**tooadd Thoughtworks Mingle hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0ce62-125">**tooadd Thoughtworks Mingle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ce62-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0ce62-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="0ce62-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="0ce62-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0ce62-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0ce62-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="0ce62-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0ce62-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="0ce62-133">Merhaba arama kutusuna yazın **Thoughtworks Mingle**seçin **Thoughtworks Mingle** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="0ce62-133">In hello search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Thoughtworks Mingle hello sonuçları listesinde](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0ce62-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="0ce62-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="0ce62-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Thoughtworks Mingle ile test etme.</span><span class="sxs-lookup"><span data-stu-id="0ce62-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0ce62-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Thoughtworks Mingle içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ce62-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Thoughtworks Mingle is tooa user in Azure AD.</span></span> <span data-ttu-id="0ce62-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Thoughtworks Mingle arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ce62-138">In other words, a link relationship between an Azure AD user and hello related user in Thoughtworks Mingle needs toobe established.</span></span>

<span data-ttu-id="0ce62-139">Thoughtworks Mingle içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="0ce62-139">In Thoughtworks Mingle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0ce62-140">tooconfigure ve Thoughtworks Mingle ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0ce62-140">tooconfigure and test Azure AD single sign-on with Thoughtworks Mingle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0ce62-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="0ce62-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0ce62-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="0ce62-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0ce62-143">**[Thoughtworks Mingle test kullanıcısı oluşturma](#create-a-thoughtworks-mingle-test-user)**  -toohave Britta Simon Thoughtworks bağlantılı toohello Azure AD kullanıcı gösterimi olan Mingle içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="0ce62-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - toohave a counterpart of Britta Simon in Thoughtworks Mingle that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0ce62-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0ce62-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0ce62-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="0ce62-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0ce62-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0ce62-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0ce62-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Thoughtworks Mingle uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0ce62-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span></span>

<span data-ttu-id="0ce62-148">**tooconfigure Azure AD çoklu oturum açma Thoughtworks Mingle ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0ce62-148">**tooconfigure Azure AD single sign-on with Thoughtworks Mingle, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ce62-149">Hello hello üzerinde Azure portal'ın **Thoughtworks Mingle** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="0ce62-149">In hello Azure portal, on hello **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="0ce62-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0ce62-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. <span data-ttu-id="0ce62-153">Merhaba üzerinde **Thoughtworks Mingle etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0ce62-153">On hello **Thoughtworks Mingle Domain and URLs** section, perform hello following steps:</span></span>

    ![Thoughtworks Mingle etki alanı ve URL'leri tek oturum açma bilgilerini](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    <span data-ttu-id="0ce62-155">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.mingle.thoughtworks.com`</span><span class="sxs-lookup"><span data-stu-id="0ce62-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.mingle.thoughtworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0ce62-156">Merhaba değeri gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="0ce62-156">hello value is not real.</span></span> <span data-ttu-id="0ce62-157">Güncelleştirme hello değerle hello gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="0ce62-157">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="0ce62-158">Kişi [Thoughtworks Mingle istemci destek ekibi](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) tooget hello değeri.</span><span class="sxs-lookup"><span data-stu-id="0ce62-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) tooget hello value.</span></span> 
 
4. <span data-ttu-id="0ce62-159">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0ce62-159">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. <span data-ttu-id="0ce62-161">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0ce62-161">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0ce62-163">İçinde tooyour oturum **Thoughtworks Mingle** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="0ce62-163">Log in tooyour **Thoughtworks Mingle** company site as administrator.</span></span>

7. <span data-ttu-id="0ce62-164">Merhaba tıklatın **yönetici** sekmesini ve ardından **SSO Config**.</span><span class="sxs-lookup"><span data-stu-id="0ce62-164">Click hello **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="0ce62-165">![Yönetici sekmesine](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO yapılandırma")</span><span class="sxs-lookup"><span data-stu-id="0ce62-165">![Admin tab](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span></span>

8. <span data-ttu-id="0ce62-166">Merhaba, **SSO Config** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0ce62-166">In hello **SSO Config** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="0ce62-167">![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO yapılandırma")</span><span class="sxs-lookup"><span data-stu-id="0ce62-167">![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span></span>
    
    <span data-ttu-id="0ce62-168">a.</span><span class="sxs-lookup"><span data-stu-id="0ce62-168">a.</span></span> <span data-ttu-id="0ce62-169">tooupload hello meta veri dosyası, tıklatın **dosya**.</span><span class="sxs-lookup"><span data-stu-id="0ce62-169">tooupload hello metadata file, click **Choose file**.</span></span> 

    <span data-ttu-id="0ce62-170">b.</span><span class="sxs-lookup"><span data-stu-id="0ce62-170">b.</span></span> <span data-ttu-id="0ce62-171">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="0ce62-171">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="0ce62-172">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="0ce62-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0ce62-173">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="0ce62-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0ce62-174">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0ce62-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0ce62-175">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ce62-175">Create an Azure AD test user</span></span>
<span data-ttu-id="0ce62-176">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="0ce62-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="0ce62-178">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0ce62-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ce62-179">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0ce62-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0ce62-181">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="0ce62-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0ce62-183">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="0ce62-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0ce62-185">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0ce62-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0ce62-187">a.</span><span class="sxs-lookup"><span data-stu-id="0ce62-187">a.</span></span> <span data-ttu-id="0ce62-188">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0ce62-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0ce62-189">b.</span><span class="sxs-lookup"><span data-stu-id="0ce62-189">b.</span></span> <span data-ttu-id="0ce62-190">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="0ce62-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0ce62-191">c.</span><span class="sxs-lookup"><span data-stu-id="0ce62-191">c.</span></span> <span data-ttu-id="0ce62-192">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="0ce62-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0ce62-193">d.</span><span class="sxs-lookup"><span data-stu-id="0ce62-193">d.</span></span> <span data-ttu-id="0ce62-194">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0ce62-194">Click **Create**.</span></span>
 
### <a name="create-a-thoughtworks-mingle-test-user"></a><span data-ttu-id="0ce62-195">Thoughtworks Mingle test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ce62-195">Create a Thoughtworks Mingle test user</span></span>

<span data-ttu-id="0ce62-196">Sağlanan toohello Thoughtworks Mingle uygulama Azure Active Directory kullanıcı adlarını kullanarak Azure AD kullanıcıların toobe mümkün toosign için olmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ce62-196">For Azure AD users toobe able toosign in, they must be provisioned toohello Thoughtworks Mingle application using their Azure Active Directory user names.</span></span> <span data-ttu-id="0ce62-197">Thoughtworks Mingle, Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="0ce62-197">In hello case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="0ce62-198">**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0ce62-198">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ce62-199">İçinde tooyour Thoughtworks Mingle şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0ce62-199">Log in tooyour Thoughtworks Mingle company site as administrator.</span></span>

2. <span data-ttu-id="0ce62-200">tıklatın **profil**.</span><span class="sxs-lookup"><span data-stu-id="0ce62-200">Click **Profile**.</span></span>
   
    <span data-ttu-id="0ce62-201">![İlk projenizi](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "ilk projenizi")</span><span class="sxs-lookup"><span data-stu-id="0ce62-201">![Your First Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span></span>

3. <span data-ttu-id="0ce62-202">Merhaba tıklatın **yönetici** sekmesini ve ardından **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="0ce62-202">Click hello **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="0ce62-203">![Kullanıcıların](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="0ce62-203">![Users](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Users")</span></span>

4. <span data-ttu-id="0ce62-204">Tıklatın **yeni kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="0ce62-204">Click **New User**.</span></span>
   
    <span data-ttu-id="0ce62-205">![Yeni kullanıcı](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="0ce62-205">![New User](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "New User")</span></span>

5. <span data-ttu-id="0ce62-206">Merhaba üzerinde **yeni kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0ce62-206">On hello **New User** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="0ce62-207">![Yeni kullanıcı iletişim kutusu](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="0ce62-207">![New User dialog](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "New User")</span></span>  
 
    <span data-ttu-id="0ce62-208">a.</span><span class="sxs-lookup"><span data-stu-id="0ce62-208">a.</span></span> <span data-ttu-id="0ce62-209">Türü hello **oturum açma adı**, **görünen adı**, **Seç parola**, **parolayı onayla** geçerli bir Azure AD hesabının tooprovision metin kutuları Hello ilgili.</span><span class="sxs-lookup"><span data-stu-id="0ce62-209">Type hello **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span> 

    <span data-ttu-id="0ce62-210">b.</span><span class="sxs-lookup"><span data-stu-id="0ce62-210">b.</span></span> <span data-ttu-id="0ce62-211">Olarak **kullanıcı türü**seçin **tam kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="0ce62-211">As **User type**, select **Full user**.</span></span>

    <span data-ttu-id="0ce62-212">c.</span><span class="sxs-lookup"><span data-stu-id="0ce62-212">c.</span></span> <span data-ttu-id="0ce62-213">Tıklatın **bu profili oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="0ce62-213">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="0ce62-214">API AAD kullanıcı hesaplarının Thoughtworks Mingle tooprovision tarafından sağlanan veya herhangi diğer Thoughtworks Mingle kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ce62-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle tooprovision AAD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="0ce62-215">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="0ce62-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="0ce62-216">Bu bölümde, erişim tooThoughtworks Mingle vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0ce62-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThoughtworks Mingle.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="0ce62-218">**tooassign Britta Simon tooThoughtworks Mingle, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0ce62-218">**tooassign Britta Simon tooThoughtworks Mingle, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ce62-219">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0ce62-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="0ce62-221">Merhaba uygulamalar listesinde **Thoughtworks Mingle**.</span><span class="sxs-lookup"><span data-stu-id="0ce62-221">In hello applications list, select **Thoughtworks Mingle**.</span></span>

    ![Merhaba Thoughtworks Mingle bağlantıyı hello uygulamalar listesi](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. <span data-ttu-id="0ce62-223">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="0ce62-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202] 

4. <span data-ttu-id="0ce62-225">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0ce62-225">Click **Add** button.</span></span> <span data-ttu-id="0ce62-226">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0ce62-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="0ce62-228">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="0ce62-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0ce62-229">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0ce62-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0ce62-230">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0ce62-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0ce62-231">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="0ce62-231">Test single sign-on</span></span>

<span data-ttu-id="0ce62-232">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="0ce62-232">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0ce62-233">Merhaba Thoughtworks Mingle parçasında hello erişim paneli tıkladığınızda, otomatik olarak oturum açma tooyour Thoughtworks Mingle uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ce62-233">When you click hello Thoughtworks Mingle tile in hello Access Panel, you should get automatically signed-on tooyour Thoughtworks Mingle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0ce62-234">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0ce62-234">Additional resources</span></span>

* [<span data-ttu-id="0ce62-235">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="0ce62-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0ce62-236">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="0ce62-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

