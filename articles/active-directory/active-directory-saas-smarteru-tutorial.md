---
title: "Öğretici: Azure Active Directory Tümleştirme ile SmarterU | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile SmarterU arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: a3b81b557c47e31f09e61bcf75dd23f370e642e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a><span data-ttu-id="06a9a-103">Öğretici: Azure Active Directory Tümleştirme SmarterU ile</span><span class="sxs-lookup"><span data-stu-id="06a9a-103">Tutorial: Azure Active Directory integration with SmarterU</span></span>

<span data-ttu-id="06a9a-104">Bu öğreticide, bilgi nasıl toointegrate SmarterU Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="06a9a-104">In this tutorial, you learn how toointegrate SmarterU with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="06a9a-105">SmarterU Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="06a9a-105">Integrating SmarterU with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="06a9a-106">Erişim tooSmarterU sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="06a9a-106">You can control in Azure AD who has access tooSmarterU</span></span>
- <span data-ttu-id="06a9a-107">Kullanıcıların tooautomatically get açan tooSmarterU (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="06a9a-107">You can enable your users tooautomatically get signed-on tooSmarterU (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="06a9a-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="06a9a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="06a9a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="06a9a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06a9a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="06a9a-110">Prerequisites</span></span>

<span data-ttu-id="06a9a-111">tooconfigure SmarterU ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="06a9a-111">tooconfigure Azure AD integration with SmarterU, you need hello following items:</span></span>

- <span data-ttu-id="06a9a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="06a9a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="06a9a-113">Bir SmarterU çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="06a9a-113">A SmarterU single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="06a9a-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="06a9a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="06a9a-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="06a9a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="06a9a-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="06a9a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="06a9a-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="06a9a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="06a9a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="06a9a-118">Scenario description</span></span>
<span data-ttu-id="06a9a-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="06a9a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="06a9a-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="06a9a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="06a9a-121">Merhaba Galerisi'nden SmarterU ekleme</span><span class="sxs-lookup"><span data-stu-id="06a9a-121">Adding SmarterU from hello gallery</span></span>
2. <span data-ttu-id="06a9a-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="06a9a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-smarteru-from-hello-gallery"></a><span data-ttu-id="06a9a-123">Merhaba Galerisi'nden SmarterU ekleme</span><span class="sxs-lookup"><span data-stu-id="06a9a-123">Adding SmarterU from hello gallery</span></span>
<span data-ttu-id="06a9a-124">Azure AD'ye tooconfigure hello tümleştirme SmarterU, tooadd SmarterU hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="06a9a-124">tooconfigure hello integration of SmarterU into Azure AD, you need tooadd SmarterU from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="06a9a-125">**tooadd SmarterU hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="06a9a-125">**tooadd SmarterU from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="06a9a-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="06a9a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="06a9a-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="06a9a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="06a9a-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="06a9a-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="06a9a-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="06a9a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="06a9a-133">Merhaba arama kutusuna yazın **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="06a9a-133">In hello search box, type **SmarterU**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_search.png)

5. <span data-ttu-id="06a9a-135">Merhaba Sonuçlar panelinde seçin **SmarterU**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="06a9a-135">In hello results panel, select **SmarterU**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="06a9a-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="06a9a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="06a9a-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı SmarterU ile test etme</span><span class="sxs-lookup"><span data-stu-id="06a9a-138">In this section, you configure and test Azure AD single sign-on with SmarterU based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="06a9a-139">Tek toowork'ın oturum açma hangi hello karşılık gelen SmarterU içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="06a9a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SmarterU is tooa user in Azure AD.</span></span> <span data-ttu-id="06a9a-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı SmarterU hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="06a9a-140">In other words, a link relationship between an Azure AD user and hello related user in SmarterU needs toobe established.</span></span>

<span data-ttu-id="06a9a-141">Merhaba hello değeri SmarterU içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="06a9a-141">In SmarterU, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="06a9a-142">tooconfigure ve SmarterU ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="06a9a-142">tooconfigure and test Azure AD single sign-on with SmarterU, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="06a9a-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="06a9a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="06a9a-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="06a9a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="06a9a-145">**[SmarterU test kullanıcısı oluşturma](#creating-a-smarteru-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir SmarterU içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="06a9a-145">**[Creating a SmarterU test user](#creating-a-smarteru-test-user)** - toohave a counterpart of Britta Simon in SmarterU that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="06a9a-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="06a9a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="06a9a-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="06a9a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="06a9a-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="06a9a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="06a9a-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma SmarterU uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="06a9a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SmarterU application.</span></span>

<span data-ttu-id="06a9a-150">**tooconfigure Azure AD çoklu oturum açma ile SmarterU, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="06a9a-150">**tooconfigure Azure AD single sign-on with SmarterU, perform hello following steps:**</span></span>

1. <span data-ttu-id="06a9a-151">Hello hello üzerinde Azure portal'ın **SmarterU** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="06a9a-151">In hello Azure portal, on hello **SmarterU** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="06a9a-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="06a9a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_samlbase.png)

3. <span data-ttu-id="06a9a-155">Merhaba üzerinde **SmarterU etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="06a9a-155">On hello **SmarterU Domain and URLs** section, perform hello following steps:</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_url.png)

    <span data-ttu-id="06a9a-157">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://www.smarteru.com/`</span><span class="sxs-lookup"><span data-stu-id="06a9a-157">In hello **Identifier** textbox, type hello URL: `https://www.smarteru.com/`</span></span>

4. <span data-ttu-id="06a9a-158">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="06a9a-158">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_certificate.png) 

5. <span data-ttu-id="06a9a-160">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="06a9a-160">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smarteru-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="06a9a-162">Farklı web tarayıcısı penceresinde tooyour SmarterU şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="06a9a-162">In a different web browser window, log in tooyour SmarterU company site as an administrator.</span></span>

7. <span data-ttu-id="06a9a-163">Merhaba üstte Hello araç çubuğunda **hesap ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="06a9a-163">In hello toolbar on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="06a9a-164">![Hesap ayarları](./media/active-directory-saas-smarteru-tutorial/IC777326.png "hesap ayarları")</span><span class="sxs-lookup"><span data-stu-id="06a9a-164">![Account Settings](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Account Settings")</span></span>

8. <span data-ttu-id="06a9a-165">Merhaba hesap yapılandırma sayfasında hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="06a9a-165">On hello account configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="06a9a-166">![Dış yetkilendirme](./media/active-directory-saas-smarteru-tutorial/IC777327.png "dış yetkilendirme")</span><span class="sxs-lookup"><span data-stu-id="06a9a-166">![External Authorization](./media/active-directory-saas-smarteru-tutorial/IC777327.png "External Authorization")</span></span> 
 
      <span data-ttu-id="06a9a-167">a.</span><span class="sxs-lookup"><span data-stu-id="06a9a-167">a.</span></span> <span data-ttu-id="06a9a-168">Seçin **etkinleştirmek dış yetkilendirme**.</span><span class="sxs-lookup"><span data-stu-id="06a9a-168">Select **Enable External Authorization**.</span></span>
  
      <span data-ttu-id="06a9a-169">b.</span><span class="sxs-lookup"><span data-stu-id="06a9a-169">b.</span></span> <span data-ttu-id="06a9a-170">Merhaba, **ana oturum açma denetimi** bölümü, select hello **SmarterU** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="06a9a-170">In hello **Master Login Control** section, select hello **SmarterU** tab.</span></span>
  
      <span data-ttu-id="06a9a-171">c.</span><span class="sxs-lookup"><span data-stu-id="06a9a-171">c.</span></span> <span data-ttu-id="06a9a-172">Merhaba, **kullanıcı varsayılan oturum açma** bölümü, select hello **SmarterU** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="06a9a-172">In hello **User Default Login** section, select hello **SmarterU** tab.</span></span>
  
      <span data-ttu-id="06a9a-173">d.</span><span class="sxs-lookup"><span data-stu-id="06a9a-173">d.</span></span> <span data-ttu-id="06a9a-174">Seçin **etkinleştirmek Okta**.</span><span class="sxs-lookup"><span data-stu-id="06a9a-174">Select **Enable Okta**.</span></span>
  
      <span data-ttu-id="06a9a-175">e.</span><span class="sxs-lookup"><span data-stu-id="06a9a-175">e.</span></span> <span data-ttu-id="06a9a-176">Merhaba hello indirilen meta veri dosyasının içeriğini kopyalayın ve hello yapıştırma **Okta meta veri** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="06a9a-176">Copy hello content of hello downloaded metadata file, and then paste it into hello **Okta Metadata** textbox.</span></span>
  
      <span data-ttu-id="06a9a-177">f.</span><span class="sxs-lookup"><span data-stu-id="06a9a-177">f.</span></span> <span data-ttu-id="06a9a-178">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="06a9a-178">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="06a9a-179">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="06a9a-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="06a9a-180">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="06a9a-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="06a9a-181">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="06a9a-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="06a9a-182">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="06a9a-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="06a9a-183">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="06a9a-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="06a9a-185">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="06a9a-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="06a9a-186">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="06a9a-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smarteru-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="06a9a-188">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="06a9a-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smarteru-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="06a9a-190">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="06a9a-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smarteru-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="06a9a-192">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="06a9a-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smarteru-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="06a9a-194">a.</span><span class="sxs-lookup"><span data-stu-id="06a9a-194">a.</span></span> <span data-ttu-id="06a9a-195">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="06a9a-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="06a9a-196">b.</span><span class="sxs-lookup"><span data-stu-id="06a9a-196">b.</span></span> <span data-ttu-id="06a9a-197">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="06a9a-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="06a9a-198">c.</span><span class="sxs-lookup"><span data-stu-id="06a9a-198">c.</span></span> <span data-ttu-id="06a9a-199">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="06a9a-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="06a9a-200">d.</span><span class="sxs-lookup"><span data-stu-id="06a9a-200">d.</span></span> <span data-ttu-id="06a9a-201">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="06a9a-201">Click **Create**.</span></span>
 
### <a name="creating-a-smarteru-test-user"></a><span data-ttu-id="06a9a-202">SmarterU test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="06a9a-202">Creating a SmarterU test user</span></span>

<span data-ttu-id="06a9a-203">tooenable Azure AD kullanıcıların toolog tooSmarterU bunların SmarterU sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="06a9a-203">tooenable Azure AD users toolog in tooSmarterU, they must be provisioned into SmarterU.</span></span>

<span data-ttu-id="06a9a-204">SmarterU, sağlama el ile bir görev olduğunda.</span><span class="sxs-lookup"><span data-stu-id="06a9a-204">When SmarterU, provisioning is a manual task.</span></span>

<span data-ttu-id="06a9a-205">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="06a9a-205">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="06a9a-206">İçinde tooyour oturum **SmarterU** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="06a9a-206">Log in tooyour **SmarterU** tenant.</span></span>

2. <span data-ttu-id="06a9a-207">Çok Git**kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="06a9a-207">Go too**Users**.</span></span>

3. <span data-ttu-id="06a9a-208">Merhaba kullanıcı bölümünde hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="06a9a-208">In hello user section, perform hello following steps:</span></span>
   
    <span data-ttu-id="06a9a-209">![Yeni kullanıcı](./media/active-directory-saas-smarteru-tutorial/IC777329.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="06a9a-209">![New User](./media/active-directory-saas-smarteru-tutorial/IC777329.png "New User")</span></span>  

    <span data-ttu-id="06a9a-210">a.</span><span class="sxs-lookup"><span data-stu-id="06a9a-210">a.</span></span> <span data-ttu-id="06a9a-211">Tıklatın **+ kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="06a9a-211">Click **+User**.</span></span>
    
    <span data-ttu-id="06a9a-212">b.</span><span class="sxs-lookup"><span data-stu-id="06a9a-212">b.</span></span> <span data-ttu-id="06a9a-213">Türü hello ilişkili öznitelik değerlerini hello Azure AD kullanıcı hesabının kutularındaki aşağıdaki hello: **birincil e-posta**, **çalışan kimliği**, **parola**,  **Parolayı doğrulayın**, **verilen ad**, **Soyadı**.</span><span class="sxs-lookup"><span data-stu-id="06a9a-213">Type hello related attribute values of hello Azure AD user account into hello following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span></span>
    
    <span data-ttu-id="06a9a-214">c.</span><span class="sxs-lookup"><span data-stu-id="06a9a-214">c.</span></span> <span data-ttu-id="06a9a-215">Tıklatın **etkin**.</span><span class="sxs-lookup"><span data-stu-id="06a9a-215">Click **Active**.</span></span> 
    
    <span data-ttu-id="06a9a-216">d.</span><span class="sxs-lookup"><span data-stu-id="06a9a-216">d.</span></span> <span data-ttu-id="06a9a-217">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="06a9a-217">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="06a9a-218">API AAD kullanıcı hesaplarının SmarterU tooprovision tarafından sağlanan veya herhangi diğer SmarterU kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06a9a-218">You can use any other SmarterU user account creation tools or APIs provided by SmarterU tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="06a9a-219">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="06a9a-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="06a9a-220">Bu bölümde, erişim tooSmarterU vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="06a9a-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSmarterU.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="06a9a-222">**tooassign Britta Simon tooSmarterU hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="06a9a-222">**tooassign Britta Simon tooSmarterU, perform hello following steps:**</span></span>

1. <span data-ttu-id="06a9a-223">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="06a9a-223">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="06a9a-225">Merhaba uygulamalar listesinde **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="06a9a-225">In hello applications list, select **SmarterU**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_app.png) 

3. <span data-ttu-id="06a9a-227">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="06a9a-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="06a9a-229">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="06a9a-229">Click **Add** button.</span></span> <span data-ttu-id="06a9a-230">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="06a9a-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="06a9a-232">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="06a9a-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="06a9a-233">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="06a9a-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="06a9a-234">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="06a9a-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="06a9a-235">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="06a9a-235">Testing single sign-on</span></span>

<span data-ttu-id="06a9a-236">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="06a9a-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="06a9a-237">Merhaba SmarterU hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour SmarterU uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="06a9a-237">When you click hello SmarterU tile in hello Access Panel, you should get automatically signed-on tooyour SmarterU application.</span></span>
<span data-ttu-id="06a9a-238">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="06a9a-238">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 


## <a name="additional-resources"></a><span data-ttu-id="06a9a-239">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="06a9a-239">Additional resources</span></span>

* [<span data-ttu-id="06a9a-240">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="06a9a-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="06a9a-241">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="06a9a-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_203.png

