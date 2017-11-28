---
title: "Öğretici: Azure Active Directory Tümleştirme ile Lucidchart | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Lucidchart arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 774e5f423097650a3cae8e8ca13b2c65b8470736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a><span data-ttu-id="2f171-103">Öğretici: Azure Active Directory Tümleştirme Lucidchart ile</span><span class="sxs-lookup"><span data-stu-id="2f171-103">Tutorial: Azure Active Directory integration with Lucidchart</span></span>

<span data-ttu-id="2f171-104">Bu öğreticide, bilgi nasıl toointegrate Lucidchart Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2f171-104">In this tutorial, you learn how toointegrate Lucidchart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f171-105">Lucidchart Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="2f171-105">Integrating Lucidchart with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2f171-106">Erişim tooLucidchart sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2f171-106">You can control in Azure AD who has access tooLucidchart</span></span>
- <span data-ttu-id="2f171-107">Kullanıcıların tooautomatically get açan tooLucidchart (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2f171-107">You can enable your users tooautomatically get signed-on tooLucidchart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2f171-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="2f171-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2f171-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2f171-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f171-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2f171-110">Prerequisites</span></span>

<span data-ttu-id="2f171-111">tooconfigure Lucidchart ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2f171-111">tooconfigure Azure AD integration with Lucidchart, you need hello following items:</span></span>

- <span data-ttu-id="2f171-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="2f171-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f171-113">Bir Lucidchart çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="2f171-113">A Lucidchart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2f171-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="2f171-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2f171-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="2f171-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f171-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="2f171-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2f171-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f171-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f171-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="2f171-118">Scenario description</span></span>
<span data-ttu-id="2f171-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="2f171-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2f171-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="2f171-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2f171-121">Merhaba Galerisi'nden Lucidchart ekleme</span><span class="sxs-lookup"><span data-stu-id="2f171-121">Adding Lucidchart from hello gallery</span></span>
2. <span data-ttu-id="2f171-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2f171-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lucidchart-from-hello-gallery"></a><span data-ttu-id="2f171-123">Merhaba Galerisi'nden Lucidchart ekleme</span><span class="sxs-lookup"><span data-stu-id="2f171-123">Adding Lucidchart from hello gallery</span></span>
<span data-ttu-id="2f171-124">Azure AD'ye tooconfigure hello tümleştirme Lucidchart, tooadd Lucidchart hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f171-124">tooconfigure hello integration of Lucidchart into Azure AD, you need tooadd Lucidchart from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2f171-125">**tooadd Lucidchart hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2f171-125">**tooadd Lucidchart from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f171-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2f171-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2f171-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="2f171-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2f171-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2f171-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="2f171-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2f171-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="2f171-133">Merhaba arama kutusuna yazın **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="2f171-133">In hello search box, type **Lucidchart**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_search.png)

5. <span data-ttu-id="2f171-135">Merhaba Sonuçlar panelinde seçin **Lucidchart**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="2f171-135">In hello results panel, select **Lucidchart**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2f171-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2f171-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2f171-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Lucidchart sınayın.</span><span class="sxs-lookup"><span data-stu-id="2f171-138">In this section, you configure and test Azure AD single sign-on with Lucidchart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2f171-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Lucidchart içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f171-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lucidchart is tooa user in Azure AD.</span></span> <span data-ttu-id="2f171-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Lucidchart hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f171-140">In other words, a link relationship between an Azure AD user and hello related user in Lucidchart needs toobe established.</span></span>

<span data-ttu-id="2f171-141">Merhaba hello değeri Lucidchart içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="2f171-141">In Lucidchart, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2f171-142">tooconfigure ve Lucidchart ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2f171-142">tooconfigure and test Azure AD single sign-on with Lucidchart, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2f171-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="2f171-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2f171-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="2f171-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2f171-145">**[Lucidchart test kullanıcısı oluşturma](#creating-a-lucidchart-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Lucidchart içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="2f171-145">**[Creating a Lucidchart test user](#creating-a-lucidchart-test-user)** - toohave a counterpart of Britta Simon in Lucidchart that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2f171-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2f171-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2f171-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="2f171-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2f171-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2f171-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2f171-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Lucidchart uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2f171-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lucidchart application.</span></span>

<span data-ttu-id="2f171-150">**tooconfigure Azure AD çoklu oturum açma ile Lucidchart, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2f171-150">**tooconfigure Azure AD single sign-on with Lucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f171-151">Hello hello üzerinde Azure portal'ın **Lucidchart** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="2f171-151">In hello Azure portal, on hello **Lucidchart** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="2f171-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2f171-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

3. <span data-ttu-id="2f171-155">Merhaba üzerinde **Lucidchart etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2f171-155">On hello **Lucidchart Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_url.png)

    <span data-ttu-id="2f171-157">Merhaba, **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://chart2.office.lucidchart.com/saml/sso/azure`</span><span class="sxs-lookup"><span data-stu-id="2f171-157">In hello **Sign-on URL** textbox, type a URL as: `https://chart2.office.lucidchart.com/saml/sso/azure`</span></span>

4. <span data-ttu-id="2f171-158">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2f171-158">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

5. <span data-ttu-id="2f171-160">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2f171-160">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lucidchart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2f171-162">Farklı web tarayıcısı penceresinde Lucidchart şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2f171-162">In a different web browser window, log into your Lucidchart company site as an administrator.</span></span>

7. <span data-ttu-id="2f171-163">Hello içinde hello üst menüsünde **takım**.</span><span class="sxs-lookup"><span data-stu-id="2f171-163">In hello menu on hello top, click **Team**.</span></span>
   
    <span data-ttu-id="2f171-164">![Takım](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "ekibi")</span><span class="sxs-lookup"><span data-stu-id="2f171-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span></span>

8. <span data-ttu-id="2f171-165">Tıklatın **uygulamaları \> SAML yönetmek**.</span><span class="sxs-lookup"><span data-stu-id="2f171-165">Click **Applications \> Manage SAML**.</span></span>
   
    <span data-ttu-id="2f171-166">![SAML yönetmek](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "SAML yönetme")</span><span class="sxs-lookup"><span data-stu-id="2f171-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML")</span></span>

9. <span data-ttu-id="2f171-167">Merhaba üzerinde **SAML kimlik doğrulaması ayarlarını** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2f171-167">On hello **SAML Authentication Settings** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="2f171-168">a.</span><span class="sxs-lookup"><span data-stu-id="2f171-168">a.</span></span> <span data-ttu-id="2f171-169">Seçin **SAML kimlik doğrulamasını etkinleştir**ve ardından **isteğe bağlı**.</span><span class="sxs-lookup"><span data-stu-id="2f171-169">Select **Enable SAML Authentication**, and then click **Optional**.</span></span>

    <span data-ttu-id="2f171-170">![SAML kimlik doğrulaması ayarlarını](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML kimlik doğrulama ayarları")</span><span class="sxs-lookup"><span data-stu-id="2f171-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings")</span></span>
 
    <span data-ttu-id="2f171-171">b.</span><span class="sxs-lookup"><span data-stu-id="2f171-171">b.</span></span> <span data-ttu-id="2f171-172">Merhaba, **etki alanı** metin kutusuna, etki alanınızın yazın ve ardından **değişiklik sertifika**.</span><span class="sxs-lookup"><span data-stu-id="2f171-172">In hello **Domain** textbox, type your domain, and then click **Change Certificate**.</span></span>

    <span data-ttu-id="2f171-173">![Sertifika değiştirme](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "sertifika değiştirme")</span><span class="sxs-lookup"><span data-stu-id="2f171-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate")</span></span>
 
    <span data-ttu-id="2f171-174">c.</span><span class="sxs-lookup"><span data-stu-id="2f171-174">c.</span></span> <span data-ttu-id="2f171-175">İndirilen meta veri dosyası, içerik kopyalama hello açın ve hello yapıştırma **meta veriler karşıya** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="2f171-175">Open your downloaded metadata file, copy hello content, and then paste it into hello **Upload Metadata** textbox.</span></span>

    <span data-ttu-id="2f171-176">![Meta veriler karşıya](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "meta veriler karşıya yükle")</span><span class="sxs-lookup"><span data-stu-id="2f171-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata")</span></span>
 
    <span data-ttu-id="2f171-177">d.</span><span class="sxs-lookup"><span data-stu-id="2f171-177">d.</span></span> <span data-ttu-id="2f171-178">Seçin **yeni kullanıcılar toohello takım otomatik olarak Ekle**ve ardından **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="2f171-178">Select **Automatically Add new users toohello team**, and then click **Save changes**.</span></span>

    <span data-ttu-id="2f171-179">![Değişiklikleri kaydetmek](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Değişiklikleri Kaydet")</span><span class="sxs-lookup"><span data-stu-id="2f171-179">![Save Changes](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Save Changes")</span></span>

> [!TIP]
> <span data-ttu-id="2f171-180">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="2f171-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2f171-181">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="2f171-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2f171-182">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2f171-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2f171-183">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2f171-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="2f171-184">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="2f171-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="2f171-186">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2f171-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f171-187">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2f171-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2f171-189">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2f171-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2f171-191">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="2f171-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2f171-193">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2f171-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2f171-195">a.</span><span class="sxs-lookup"><span data-stu-id="2f171-195">a.</span></span> <span data-ttu-id="2f171-196">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2f171-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2f171-197">b.</span><span class="sxs-lookup"><span data-stu-id="2f171-197">b.</span></span> <span data-ttu-id="2f171-198">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="2f171-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2f171-199">c.</span><span class="sxs-lookup"><span data-stu-id="2f171-199">c.</span></span> <span data-ttu-id="2f171-200">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="2f171-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2f171-201">d.</span><span class="sxs-lookup"><span data-stu-id="2f171-201">d.</span></span> <span data-ttu-id="2f171-202">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f171-202">Click **Create**.</span></span>
 
### <a name="creating-a-lucidchart-test-user"></a><span data-ttu-id="2f171-203">Lucidchart test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2f171-203">Creating a Lucidchart test user</span></span>

<span data-ttu-id="2f171-204">TooLucidchart sağlama, tooconfigure kullanıcı için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="2f171-204">There is no action item for you tooconfigure user provisioning tooLucidchart.</span></span>  <span data-ttu-id="2f171-205">Atanmış bir kullanıcı hello erişim paneli kullanılarak Lucidchart toolog çalıştığında Lucidchart hello kullanıcı var olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="2f171-205">When an assigned user tries toolog into Lucidchart using hello access panel, Lucidchart checks whether hello user exists.</span></span>  

<span data-ttu-id="2f171-206">Hiçbir kullanıcı hesabı varsa kullanılabilir henüz, Lucidchart tarafından otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2f171-206">If there is no user account available yet, it is automatically created by Lucidchart.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2f171-207">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="2f171-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2f171-208">Bu bölümde, erişim tooLucidchart vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2f171-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLucidchart.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="2f171-210">**tooassign Britta Simon tooLucidchart hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2f171-210">**tooassign Britta Simon tooLucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f171-211">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2f171-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="2f171-213">Merhaba uygulamalar listesinde **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="2f171-213">In hello applications list, select **Lucidchart**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_app.png) 

3. <span data-ttu-id="2f171-215">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="2f171-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="2f171-217">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2f171-217">Click **Add** button.</span></span> <span data-ttu-id="2f171-218">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2f171-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="2f171-220">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="2f171-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2f171-221">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2f171-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2f171-222">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2f171-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2f171-223">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="2f171-223">Testing single sign-on</span></span>

<span data-ttu-id="2f171-224">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="2f171-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2f171-225">Merhaba Lucidchart hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Lucidchart uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f171-225">When you click hello Lucidchart tile in hello Access Panel, you should get automatically signed-on tooyour Lucidchart application.</span></span>
<span data-ttu-id="2f171-226">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2f171-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2f171-227">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2f171-227">Additional resources</span></span>

* [<span data-ttu-id="2f171-228">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="2f171-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f171-229">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="2f171-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_203.png

