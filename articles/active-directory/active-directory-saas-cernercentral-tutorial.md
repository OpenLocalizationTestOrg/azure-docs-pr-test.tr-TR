---
title: "Öğretici: Azure Active Directory Tümleştirme Cerner orta ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Cerner Orta arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 3493d180e8f229b7cd228769f780f10208114889
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="f1beb-103">Öğretici: Azure Active Directory Tümleştirme ile Cerner Orta</span><span class="sxs-lookup"><span data-stu-id="f1beb-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="f1beb-104">Bu öğreticide, bilgi nasıl toointegrate Cerner Orta Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f1beb-104">In this tutorial, you learn how toointegrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1beb-105">Cerner Orta Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="f1beb-105">Integrating Cerner Central with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f1beb-106">Erişim tooCerner Orta olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f1beb-106">You can control in Azure AD who has access tooCerner Central</span></span>
- <span data-ttu-id="f1beb-107">Kullanıcıların tooautomatically get açan tooCerner Orta (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f1beb-107">You can enable your users tooautomatically get signed-on tooCerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1beb-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="f1beb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f1beb-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f1beb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1beb-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f1beb-110">Prerequisites</span></span>

<span data-ttu-id="f1beb-111">tooconfigure Cerner orta ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="f1beb-111">tooconfigure Azure AD integration with Cerner Central, you need hello following items:</span></span>

- <span data-ttu-id="f1beb-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="f1beb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1beb-113">Onaylanan bir Cerner Merkezi sistem hesabı</span><span class="sxs-lookup"><span data-stu-id="f1beb-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="f1beb-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="f1beb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1beb-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="f1beb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1beb-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="f1beb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f1beb-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1beb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1beb-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="f1beb-118">Scenario description</span></span>
<span data-ttu-id="f1beb-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="f1beb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1beb-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="f1beb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1beb-121">Merhaba Galerisi'nden Cerner Orta ekleme</span><span class="sxs-lookup"><span data-stu-id="f1beb-121">Adding Cerner Central from hello gallery</span></span>
2. <span data-ttu-id="f1beb-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f1beb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-hello-gallery"></a><span data-ttu-id="f1beb-123">Merhaba Galerisi'nden Cerner Orta ekleme</span><span class="sxs-lookup"><span data-stu-id="f1beb-123">Adding Cerner Central from hello gallery</span></span>
<span data-ttu-id="f1beb-124">Azure AD'ye tooconfigure hello tümleştirme Cerner Orta, tooadd Cerner Orta hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="f1beb-124">tooconfigure hello integration of Cerner Central into Azure AD, you need tooadd Cerner Central from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f1beb-125">**tooadd Cerner Orta hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f1beb-125">**tooadd Cerner Central from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1beb-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f1beb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f1beb-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="f1beb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f1beb-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f1beb-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="f1beb-131">tooadd yeni uygulama tıklatın **yeni uygulama** düğmesi hello iletişim üstünde.</span><span class="sxs-lookup"><span data-stu-id="f1beb-131">tooadd new application, click **New application** button on top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="f1beb-133">Merhaba arama kutusuna yazın **Cerner orta**.</span><span class="sxs-lookup"><span data-stu-id="f1beb-133">In hello search box, type **Cerner Central**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. <span data-ttu-id="f1beb-135">Merhaba Sonuçlar panelinde seçin **Cerner orta**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="f1beb-135">In hello results panel, select **Cerner Central**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f1beb-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f1beb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f1beb-138">Bu bölümde, yapılandırmanız ve Cerner orta ile Azure AD çoklu oturum açmayı test "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="f1beb-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f1beb-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Cerner Orta tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="f1beb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cerner Central is tooa user in Azure AD.</span></span> <span data-ttu-id="f1beb-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Cerner Orta hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="f1beb-140">In other words, a link relationship between an Azure AD user and hello related user in Cerner Central needs toobe established.</span></span>

<span data-ttu-id="f1beb-141">tooconfigure ve Cerner orta ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="f1beb-141">tooconfigure and test Azure AD single sign-on with Cerner Central, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f1beb-142">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="f1beb-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f1beb-143">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="f1beb-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1beb-144">**[Cerner Orta test kullanıcısı oluşturma](#creating-a-cerner-central-test-user)**  -toohave Britta Simon hello kullanıcı bağlantılı toohello Azure AD gösterimidir Cerner Orta, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="f1beb-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - toohave a counterpart of Britta Simon in Cerner Central that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="f1beb-145">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="f1beb-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1beb-146">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="f1beb-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f1beb-147">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f1beb-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f1beb-148">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Cerner Orta uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f1beb-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="f1beb-149">**tooconfigure Azure AD çoklu oturum açma Cerner orta ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f1beb-149">**tooconfigure Azure AD single sign-on with Cerner Central, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1beb-150">Hello hello üzerinde Azure portal'ın **Cerner orta** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="f1beb-150">In hello Azure portal, on hello **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="f1beb-152">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="f1beb-152">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. <span data-ttu-id="f1beb-154">Merhaba üzerinde **Cerner merkezi etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f1beb-154">On hello **Cerner Central Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="f1beb-156">a.</span><span class="sxs-lookup"><span data-stu-id="f1beb-156">a.</span></span> <span data-ttu-id="f1beb-157">Merhaba, **tanımlayıcısı** metin kutusuna, desenler izleyen hello kullanarak türü başlangıç değeri:</span><span class="sxs-lookup"><span data-stu-id="f1beb-157">In hello **Identifier** textbox, type hello value using hello following patterns:</span></span>
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    <span data-ttu-id="f1beb-158">b.</span><span class="sxs-lookup"><span data-stu-id="f1beb-158">b.</span></span> <span data-ttu-id="f1beb-159">Merhaba, **yanıt URL'si** metin kutusuna, türü aşağıdaki hello kullanarak bir URL düzenleri:</span><span class="sxs-lookup"><span data-stu-id="f1beb-159">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="f1beb-160">Bu değerler hello gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="f1beb-160">These values are not hello real.</span></span> <span data-ttu-id="f1beb-161">Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f1beb-161">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="f1beb-162">Kişi [Cerner Orta destek ekibi](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="f1beb-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget these values.</span></span>
 
4. <span data-ttu-id="f1beb-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f1beb-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="f1beb-165">toogenerate hello **meta veri** url hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f1beb-165">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="f1beb-166">a.</span><span class="sxs-lookup"><span data-stu-id="f1beb-166">a.</span></span> <span data-ttu-id="f1beb-167">Tıklatın **uygulama kayıtlar**.</span><span class="sxs-lookup"><span data-stu-id="f1beb-167">Click **App registrations**.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    <span data-ttu-id="f1beb-169">b.</span><span class="sxs-lookup"><span data-stu-id="f1beb-169">b.</span></span> <span data-ttu-id="f1beb-170">Tıklatın **uç noktaları** tooopen **uç noktaları** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="f1beb-170">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    <span data-ttu-id="f1beb-172">c.</span><span class="sxs-lookup"><span data-stu-id="f1beb-172">c.</span></span> <span data-ttu-id="f1beb-173">Merhaba Kopyala düğmesine toocopy tıklatın **FEDERASYON meta veri belgesi** URL'yi kopyalayıp Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="f1beb-173">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    <span data-ttu-id="f1beb-175">d.</span><span class="sxs-lookup"><span data-stu-id="f1beb-175">d.</span></span> <span data-ttu-id="f1beb-176">Şimdi toohello özellik sayfasında gidin **Cerner orta** ve kopyalama hello **uygulama kimliği** kullanarak **kopyalama** düğmesine tıklayın ve Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="f1beb-176">Now go toohello property page of **Cerner Central** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    <span data-ttu-id="f1beb-178">e.</span><span class="sxs-lookup"><span data-stu-id="f1beb-178">e.</span></span> <span data-ttu-id="f1beb-179">Merhaba oluşturmak **meta veri URL'sini** desen aşağıdaki hello kullanarak:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="f1beb-179">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

6. <span data-ttu-id="f1beb-180">tooconfigure çoklu oturum açma üzerinde **Cerner orta** yan, gereksinim duyduğunuz toosend hello **meta veri URL'sini** çok[Cerner Orta Destek](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="f1beb-180">tooconfigure single sign-on on **Cerner Central** side, you need toosend hello **Metadata URL** too[Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="f1beb-181">Uygulama yan toocomplete hello tümleştirme'hello SSO yapılandırırlar.</span><span class="sxs-lookup"><span data-stu-id="f1beb-181">They configure hello SSO on application side toocomplete hello integration.</span></span>

> [!TIP]
> <span data-ttu-id="f1beb-182">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="f1beb-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f1beb-183">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="f1beb-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f1beb-184">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f1beb-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f1beb-185">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f1beb-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="f1beb-186">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="f1beb-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span> 

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="f1beb-188">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f1beb-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1beb-189">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f1beb-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f1beb-191">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f1beb-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f1beb-193">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="f1beb-193">tooopen hello **User** dialog, click **Add**.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f1beb-195">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f1beb-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f1beb-197">a.</span><span class="sxs-lookup"><span data-stu-id="f1beb-197">a.</span></span> <span data-ttu-id="f1beb-198">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f1beb-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1beb-199">b.</span><span class="sxs-lookup"><span data-stu-id="f1beb-199">b.</span></span> <span data-ttu-id="f1beb-200">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="f1beb-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="f1beb-201">c.</span><span class="sxs-lookup"><span data-stu-id="f1beb-201">c.</span></span> <span data-ttu-id="f1beb-202">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="f1beb-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f1beb-203">d.</span><span class="sxs-lookup"><span data-stu-id="f1beb-203">d.</span></span> <span data-ttu-id="f1beb-204">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f1beb-204">Click **Create**.</span></span>
 
### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="f1beb-205">Cerner Orta test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f1beb-205">Creating a Cerner Central test user</span></span>

<span data-ttu-id="f1beb-206">**Cerner orta** uygulama tüm Federal Kimlik sağlayıcısından kimlik doğrulamasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="f1beb-206">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="f1beb-207">Bir kullanıcı toohello uygulama giriş sayfasındaki mümkün toolog ise, Federasyon ve herhangi bir el ile sağlama için gerekli olan.</span><span class="sxs-lookup"><span data-stu-id="f1beb-207">If a user is able toolog in toohello application home page, they are federated and have no need for any manual provisioning.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f1beb-208">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="f1beb-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f1beb-209">Bu bölümde, erişim tooCerner Orta vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f1beb-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCerner Central.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="f1beb-211">**tooassign Britta Simon tooCerner Orta, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f1beb-211">**tooassign Britta Simon tooCerner Central, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1beb-212">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f1beb-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="f1beb-214">Merhaba uygulamalar listesinde **Cerner orta**.</span><span class="sxs-lookup"><span data-stu-id="f1beb-214">In hello applications list, select **Cerner Central**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. <span data-ttu-id="f1beb-216">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="f1beb-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="f1beb-218">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f1beb-218">Click **Add** button.</span></span> <span data-ttu-id="f1beb-219">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f1beb-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="f1beb-221">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="f1beb-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f1beb-222">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f1beb-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1beb-223">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f1beb-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f1beb-224">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="f1beb-224">Testing single sign-on</span></span>

<span data-ttu-id="f1beb-225">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="f1beb-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f1beb-226">Cerner Orta döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma Cerner yönetim uygulaması tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f1beb-226">When you click hello Cerner Central tile in hello Access Panel, you should get automatically signed-on tooyour Cerner Central application.</span></span> <span data-ttu-id="f1beb-227">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f1beb-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f1beb-228">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f1beb-228">Additional resources</span></span>

* [<span data-ttu-id="f1beb-229">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="f1beb-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1beb-230">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="f1beb-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

