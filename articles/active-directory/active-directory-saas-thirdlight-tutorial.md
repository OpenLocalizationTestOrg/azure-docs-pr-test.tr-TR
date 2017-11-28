---
title: "Öğretici: Azure Active Directory Tümleştirme ile ThirdLight | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile ThirdLight arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: a510e514f6a8c4e89220b9a6f6db29668b451b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a><span data-ttu-id="985cc-103">Öğretici: Azure Active Directory Tümleştirme ThirdLight ile</span><span class="sxs-lookup"><span data-stu-id="985cc-103">Tutorial: Azure Active Directory integration with ThirdLight</span></span>

<span data-ttu-id="985cc-104">Bu öğreticide, bilgi nasıl toointegrate ThirdLight Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="985cc-104">In this tutorial, you learn how toointegrate ThirdLight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="985cc-105">ThirdLight Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="985cc-105">Integrating ThirdLight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="985cc-106">Erişim tooThirdLight sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="985cc-106">You can control in Azure AD who has access tooThirdLight</span></span>
- <span data-ttu-id="985cc-107">Kullanıcıların tooautomatically get açan tooThirdLight (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="985cc-107">You can enable your users tooautomatically get signed-on tooThirdLight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="985cc-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="985cc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="985cc-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="985cc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="985cc-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="985cc-110">Prerequisites</span></span>

<span data-ttu-id="985cc-111">tooconfigure ThirdLight ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="985cc-111">tooconfigure Azure AD integration with ThirdLight, you need hello following items:</span></span>

- <span data-ttu-id="985cc-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="985cc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="985cc-113">Bir ThirdLight çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="985cc-113">A ThirdLight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="985cc-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="985cc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="985cc-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="985cc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="985cc-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="985cc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="985cc-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="985cc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="985cc-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="985cc-118">Scenario description</span></span>
<span data-ttu-id="985cc-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="985cc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="985cc-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="985cc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="985cc-121">Merhaba Galerisi'nden ThirdLight ekleme</span><span class="sxs-lookup"><span data-stu-id="985cc-121">Adding ThirdLight from hello gallery</span></span>
2. <span data-ttu-id="985cc-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="985cc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thirdlight-from-hello-gallery"></a><span data-ttu-id="985cc-123">Merhaba Galerisi'nden ThirdLight ekleme</span><span class="sxs-lookup"><span data-stu-id="985cc-123">Adding ThirdLight from hello gallery</span></span>
<span data-ttu-id="985cc-124">Azure AD'ye tooconfigure hello tümleştirme ThirdLight, tooadd ThirdLight hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="985cc-124">tooconfigure hello integration of ThirdLight into Azure AD, you need tooadd ThirdLight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="985cc-125">**tooadd ThirdLight hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="985cc-125">**tooadd ThirdLight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="985cc-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="985cc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="985cc-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="985cc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="985cc-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="985cc-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="985cc-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="985cc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="985cc-133">Merhaba arama kutusuna yazın **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="985cc-133">In hello search box, type **ThirdLight**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_search.png)

5. <span data-ttu-id="985cc-135">Merhaba Sonuçlar panelinde seçin **ThirdLight**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="985cc-135">In hello results panel, select **ThirdLight**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="985cc-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="985cc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="985cc-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı ThirdLight ile test etme</span><span class="sxs-lookup"><span data-stu-id="985cc-138">In this section, you configure and test Azure AD single sign-on with ThirdLight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="985cc-139">Tek toowork'ın oturum açma hangi hello karşılık gelen ThirdLight içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="985cc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ThirdLight is tooa user in Azure AD.</span></span> <span data-ttu-id="985cc-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı ThirdLight hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="985cc-140">In other words, a link relationship between an Azure AD user and hello related user in ThirdLight needs toobe established.</span></span>

<span data-ttu-id="985cc-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** ThirdLight içinde.</span><span class="sxs-lookup"><span data-stu-id="985cc-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ThirdLight.</span></span>

<span data-ttu-id="985cc-142">tooconfigure ve ThirdLight ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="985cc-142">tooconfigure and test Azure AD single sign-on with ThirdLight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="985cc-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="985cc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="985cc-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="985cc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="985cc-145">**[ThirdLight test kullanıcısı oluşturma](#creating-a-thirdlight-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir ThirdLight içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="985cc-145">**[Creating a ThirdLight test user](#creating-a-thirdlight-test-user)** - toohave a counterpart of Britta Simon in ThirdLight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="985cc-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="985cc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="985cc-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="985cc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="985cc-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="985cc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="985cc-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma ThirdLight uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="985cc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ThirdLight application.</span></span>

<span data-ttu-id="985cc-150">**tooconfigure Azure AD çoklu oturum açma ile ThirdLight, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="985cc-150">**tooconfigure Azure AD single sign-on with ThirdLight, perform hello following steps:**</span></span>

1. <span data-ttu-id="985cc-151">Hello hello üzerinde Azure portal'ın **ThirdLight** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="985cc-151">In hello Azure portal, on hello **ThirdLight** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="985cc-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="985cc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_samlbase.png)

3. <span data-ttu-id="985cc-155">Merhaba üzerinde **ThirdLight etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="985cc-155">On hello **ThirdLight Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_url.png)

    <span data-ttu-id="985cc-157">a.</span><span class="sxs-lookup"><span data-stu-id="985cc-157">a.</span></span> <span data-ttu-id="985cc-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.thirdlight.com/`</span><span class="sxs-lookup"><span data-stu-id="985cc-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.thirdlight.com/`</span></span>

    <span data-ttu-id="985cc-159">b.</span><span class="sxs-lookup"><span data-stu-id="985cc-159">b.</span></span> <span data-ttu-id="985cc-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.thirdlight.com/saml/sp`</span><span class="sxs-lookup"><span data-stu-id="985cc-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.thirdlight.com/saml/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="985cc-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="985cc-161">These values are not real.</span></span> <span data-ttu-id="985cc-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve Identiifer.</span><span class="sxs-lookup"><span data-stu-id="985cc-162">Update these values with hello actual Sign-On URL and Identiifer.</span></span> <span data-ttu-id="985cc-163">Kişi [ThirdLight istemci destek ekibi](https://www.thirdlight.com/support) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="985cc-163">Contact [ThirdLight Client support team](https://www.thirdlight.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="985cc-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="985cc-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_certificate.png) 

5. <span data-ttu-id="985cc-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="985cc-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thirdlight-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="985cc-168">Farklı web tarayıcısı penceresinde tooyour ThirdLight şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="985cc-168">In a different web browser window, log in tooyour ThirdLight company site as an administrator.</span></span>

7. <span data-ttu-id="985cc-169">Çok Git**yapılandırma \> Sistem Yönetimi**ve ardından **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="985cc-169">Go too**Configuration \> System Administration**, and then click **SAML2**.</span></span>
   
    <span data-ttu-id="985cc-170">![Sistem Yönetimi](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "Sistem Yönetimi")</span><span class="sxs-lookup"><span data-stu-id="985cc-170">![System Administration](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "System Administration")</span></span>

8. <span data-ttu-id="985cc-171">Merhaba SAML2 yapılandırma bölümünde hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="985cc-171">In hello SAML2 configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="985cc-172">![SAML çoklu oturum açma](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="985cc-172">![SAML Single Sign-On](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML Single Sign-On")</span></span>   

     <span data-ttu-id="985cc-173">a.</span><span class="sxs-lookup"><span data-stu-id="985cc-173">a.</span></span> <span data-ttu-id="985cc-174">Seçin **SAML2 çoklu oturum açmayı etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="985cc-174">Select **Enable SAML2 Single Sign-On**.</span></span>
 
     <span data-ttu-id="985cc-175">b.</span><span class="sxs-lookup"><span data-stu-id="985cc-175">b.</span></span> <span data-ttu-id="985cc-176">Olarak **IDP meta veriler için kaynak**seçin **XML yük IDP meta verilerini**.</span><span class="sxs-lookup"><span data-stu-id="985cc-176">As **Source for IdP Metadata**, select **Load IdP Metadata from XML**.</span></span>
 
     <span data-ttu-id="985cc-177">c.</span><span class="sxs-lookup"><span data-stu-id="985cc-177">c.</span></span> <span data-ttu-id="985cc-178">İndirilen hello meta veri dosyasını açın, hello içeriği Kopyala ve hello yapıştırma **IDP meta veri XML** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="985cc-178">Open hello downloaded metadata file, copy hello content, and then paste it into hello **IdP Metadata XML** textbox.</span></span> 
     
     <span data-ttu-id="985cc-179">d.</span><span class="sxs-lookup"><span data-stu-id="985cc-179">d.</span></span> <span data-ttu-id="985cc-180">Tıklatın **kaydetmek SAML2 ayarları**.</span><span class="sxs-lookup"><span data-stu-id="985cc-180">Click **Save SAML2 settings**.</span></span>

> [!TIP]
> <span data-ttu-id="985cc-181">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="985cc-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="985cc-182">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="985cc-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="985cc-183">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="985cc-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="985cc-184">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="985cc-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="985cc-185">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="985cc-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="985cc-187">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="985cc-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="985cc-188">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="985cc-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="985cc-190">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="985cc-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="985cc-192">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="985cc-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="985cc-194">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="985cc-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="985cc-196">a.</span><span class="sxs-lookup"><span data-stu-id="985cc-196">a.</span></span> <span data-ttu-id="985cc-197">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="985cc-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="985cc-198">b.</span><span class="sxs-lookup"><span data-stu-id="985cc-198">b.</span></span> <span data-ttu-id="985cc-199">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="985cc-199">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="985cc-200">c.</span><span class="sxs-lookup"><span data-stu-id="985cc-200">c.</span></span> <span data-ttu-id="985cc-201">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="985cc-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="985cc-202">d.</span><span class="sxs-lookup"><span data-stu-id="985cc-202">d.</span></span> <span data-ttu-id="985cc-203">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="985cc-203">Click **Create**.</span></span>
 
### <a name="creating-a-thirdlight-test-user"></a><span data-ttu-id="985cc-204">ThirdLight test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="985cc-204">Creating a ThirdLight test user</span></span>

<span data-ttu-id="985cc-205">tooenable Azure AD kullanıcıların toolog tooThirdLight bunların ThirdLight sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="985cc-205">tooenable Azure AD users toolog in tooThirdLight, they must be provisioned into ThirdLight.</span></span>  
<span data-ttu-id="985cc-206">ThirdLight Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="985cc-206">In hello case of ThirdLight, provisioning is a manual task.</span></span>

<span data-ttu-id="985cc-207">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="985cc-207">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="985cc-208">İçinde tooyour oturum **ThirdLight** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="985cc-208">Log in tooyour **ThirdLight** company site as an administrator.</span></span>

2. <span data-ttu-id="985cc-209">Çok Git**kullanıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="985cc-209">Go too**Users** tab.</span></span>

3. <span data-ttu-id="985cc-210">Seçin **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="985cc-210">Select **Users and Groups**.</span></span>

4. <span data-ttu-id="985cc-211">Tıklatın **yeni kullanıcı Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="985cc-211">Click **Add new User** button.</span></span>

5. <span data-ttu-id="985cc-212">Girin **hello kullanıcı adı, ad veya açıklama, e-posta, seçin hazır ya da yeni üyeler grup** tooprovision istediğiniz geçerli bir AAD hesabının.</span><span class="sxs-lookup"><span data-stu-id="985cc-212">Enter **hello Username, Name or Description, Email, Choose a Preset or Group of New Members** of a valid AAD account you want tooprovision.</span></span>

6. <span data-ttu-id="985cc-213">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="985cc-213">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="985cc-214">API AAD kullanıcı hesaplarının Thirdlight tooprovision tarafından sağlanan veya herhangi diğer Thirdlight kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="985cc-214">You can use any other Thirdlight user account creation tools or APIs provided by Thirdlight tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="985cc-215">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="985cc-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="985cc-216">Bu bölümde, erişim tooThirdLight vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="985cc-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThirdLight.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="985cc-218">**tooassign Britta Simon tooThirdLight hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="985cc-218">**tooassign Britta Simon tooThirdLight, perform hello following steps:**</span></span>

1. <span data-ttu-id="985cc-219">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="985cc-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="985cc-221">Merhaba uygulamalar listesinde **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="985cc-221">In hello applications list, select **ThirdLight**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_app.png) 

3. <span data-ttu-id="985cc-223">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="985cc-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="985cc-225">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="985cc-225">Click **Add** button.</span></span> <span data-ttu-id="985cc-226">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="985cc-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="985cc-228">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="985cc-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="985cc-229">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="985cc-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="985cc-230">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="985cc-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="985cc-231">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="985cc-231">Testing single sign-on</span></span>

<span data-ttu-id="985cc-232">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="985cc-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="985cc-233">Merhaba ThirdLight hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour ThirdLight uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="985cc-233">When you click hello ThirdLight tile in hello Access Panel, you should get automatically signed-on tooyour ThirdLight application.</span></span>
<span data-ttu-id="985cc-234">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="985cc-234">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="985cc-235">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="985cc-235">Additional resources</span></span>

* [<span data-ttu-id="985cc-236">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="985cc-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="985cc-237">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="985cc-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_203.png

