---
title: "Öğretici: Azure Active Directory Tümleştirme Springer bağlantıyla | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Springer bağlantı arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 58cdf029-bdc0-43c4-a469-b921c2a669bd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: jeedes
ms.openlocfilehash: dabd2f72b3a195fc359826a4863a197e5019f5c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springer-link"></a><span data-ttu-id="66b3d-103">Öğretici: Azure Active Directory Tümleştirme Springer bağlantıyla</span><span class="sxs-lookup"><span data-stu-id="66b3d-103">Tutorial: Azure Active Directory integration with Springer Link</span></span>

<span data-ttu-id="66b3d-104">Bu öğreticide, bilgi toointegrate Springer bağlantı nasıl Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="66b3d-104">In this tutorial, you learn how toointegrate Springer Link with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="66b3d-105">Springer bağlantı Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="66b3d-105">Integrating Springer Link with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="66b3d-106">Erişim tooSpringer bağlantı sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66b3d-106">You can control in Azure AD who has access tooSpringer Link.</span></span>
- <span data-ttu-id="66b3d-107">Kullanıcıların tooautomatically get açan tooSpringer bağlantı (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66b3d-107">You can enable your users tooautomatically get signed-on tooSpringer Link (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="66b3d-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="66b3d-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="66b3d-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="66b3d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66b3d-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="66b3d-110">Prerequisites</span></span>

<span data-ttu-id="66b3d-111">tooconfigure Springer bağlantı ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="66b3d-111">tooconfigure Azure AD integration with Springer Link, you need hello following items:</span></span>

- <span data-ttu-id="66b3d-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="66b3d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="66b3d-113">Bir Springer bağlantı çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="66b3d-113">A Springer Link single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="66b3d-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="66b3d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="66b3d-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="66b3d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="66b3d-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="66b3d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="66b3d-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="66b3d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="66b3d-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="66b3d-118">Scenario description</span></span>
<span data-ttu-id="66b3d-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="66b3d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="66b3d-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="66b3d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="66b3d-121">Merhaba Galerisi'nden Springer bağlantısı ekleme</span><span class="sxs-lookup"><span data-stu-id="66b3d-121">Adding Springer Link from hello gallery</span></span>
2. <span data-ttu-id="66b3d-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="66b3d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springer-link-from-hello-gallery"></a><span data-ttu-id="66b3d-123">Merhaba Galerisi'nden Springer bağlantısı ekleme</span><span class="sxs-lookup"><span data-stu-id="66b3d-123">Adding Springer Link from hello gallery</span></span>
<span data-ttu-id="66b3d-124">Azure AD'ye tooconfigure hello tümleştirme Springer bağlantı tooadd Springer bağlantı hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="66b3d-124">tooconfigure hello integration of Springer Link into Azure AD, you need tooadd Springer Link from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="66b3d-125">**tooadd Springer bağlantı hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="66b3d-125">**tooadd Springer Link from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="66b3d-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="66b3d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="66b3d-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="66b3d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="66b3d-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="66b3d-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="66b3d-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="66b3d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="66b3d-133">Merhaba arama kutusuna yazın **Springer bağlantı**seçin **Springer bağlantı** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="66b3d-133">In hello search box, type **Springer Link**, select **Springer Link** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde springer bağlantı](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="66b3d-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="66b3d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="66b3d-136">Bu bölümde, yapılandırmak ve Azure AD çoklu oturum açma Springer "Britta Simon" adlı bir test kullanıcı tabanlı bağlantıyı sınayın.</span><span class="sxs-lookup"><span data-stu-id="66b3d-136">In this section, you configure and test Azure AD single sign-on with Springer Link based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="66b3d-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Springer bağlantısında tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="66b3d-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Springer Link is tooa user in Azure AD.</span></span> <span data-ttu-id="66b3d-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve Springer bağlantısında hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="66b3d-138">In other words, a link relationship between an Azure AD user and hello related user in Springer Link needs toobe established.</span></span>

<span data-ttu-id="66b3d-139">Merhaba hello değeri Springer bağlantıdaki atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="66b3d-139">In Springer Link, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="66b3d-140">tooconfigure ve Springer bağlantı ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="66b3d-140">tooconfigure and test Azure AD single sign-on with Springer Link, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="66b3d-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="66b3d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="66b3d-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="66b3d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="66b3d-143">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="66b3d-143">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
4. <span data-ttu-id="66b3d-144">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="66b3d-144">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="66b3d-145">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="66b3d-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="66b3d-146">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Springer bağlantı uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="66b3d-146">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Springer Link application.</span></span>

<span data-ttu-id="66b3d-147">**tooconfigure Azure AD çoklu oturum açma Springer bağlantıyla hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="66b3d-147">**tooconfigure Azure AD single sign-on with Springer Link, perform hello following steps:**</span></span>

1. <span data-ttu-id="66b3d-148">Merhaba hello üzerinde Azure portal'ın **Springer bağlantı** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="66b3d-148">In hello Azure portal, on hello **Springer Link** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="66b3d-150">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="66b3d-150">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_samlbase.png)

3. <span data-ttu-id="66b3d-152">Merhaba üzerinde **Springer bağlantı etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="66b3d-152">On hello **Springer Link Domain and URLs** section,  If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Springer bağlantı etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url1.png)

    <span data-ttu-id="66b3d-154">a.</span><span class="sxs-lookup"><span data-stu-id="66b3d-154">a.</span></span> <span data-ttu-id="66b3d-155">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://fsso.springer.com`</span><span class="sxs-lookup"><span data-stu-id="66b3d-155">In hello **Identifier** textbox, type hello URL: `https://fsso.springer.com`</span></span>

    <span data-ttu-id="66b3d-156">b.</span><span class="sxs-lookup"><span data-stu-id="66b3d-156">b.</span></span> <span data-ttu-id="66b3d-157">Merhaba, **yanıt URL'si** metin kutusuna, türü hello URL'si:`https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="66b3d-157">In hello **Reply URL** textbox, type hello URL: `https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

4. <span data-ttu-id="66b3d-158">Denetleme **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="66b3d-158">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="66b3d-159">Tooconfigure hello uygulamada istiyorsanız **SP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="66b3d-159">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Springer bağlantı etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url.png)

    <span data-ttu-id="66b3d-161">Merhaba, **oturum açma URL'si** metin kutusuna, türü hello URL'si:`https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="66b3d-161">In hello **Sign-on URL** textbox, type hello URL : `https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

5. <span data-ttu-id="66b3d-162">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="66b3d-162">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-springerlink-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="66b3d-164">toogenerate hello **meta veri** url hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="66b3d-164">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="66b3d-165">a.</span><span class="sxs-lookup"><span data-stu-id="66b3d-165">a.</span></span> <span data-ttu-id="66b3d-166">Tıklatın **uygulama kayıtlar**.</span><span class="sxs-lookup"><span data-stu-id="66b3d-166">Click **App registrations**.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appregistrations.png)
   
    <span data-ttu-id="66b3d-168">b.</span><span class="sxs-lookup"><span data-stu-id="66b3d-168">b.</span></span> <span data-ttu-id="66b3d-169">Tıklatın **uç noktaları** tooopen **uç noktaları** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="66b3d-169">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpointicon.png)

    <span data-ttu-id="66b3d-171">c.</span><span class="sxs-lookup"><span data-stu-id="66b3d-171">c.</span></span> <span data-ttu-id="66b3d-172">Merhaba Kopyala düğmesine toocopy tıklatın **FEDERASYON meta veri belgesi** URL'yi kopyalayıp Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="66b3d-172">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpoint.png)
     
    <span data-ttu-id="66b3d-174">d.</span><span class="sxs-lookup"><span data-stu-id="66b3d-174">d.</span></span> <span data-ttu-id="66b3d-175">Şimdi toohello özellik sayfasında gidin **Springer bağlantı** ve kopyalama hello **uygulama kimliği** kullanarak **kopyalama** düğmesine tıklayın ve Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="66b3d-175">Now go toohello property page of **Springer Link** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appid.png)

    <span data-ttu-id="66b3d-177">e.</span><span class="sxs-lookup"><span data-stu-id="66b3d-177">e.</span></span> <span data-ttu-id="66b3d-178">Merhaba oluşturmak **meta veri URL'sini** desen aşağıdaki hello kullanarak:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="66b3d-178">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="66b3d-179">tooconfigure çoklu oturum açma üzerinde **Springer bağlantı** yan, oluşturulan toosend hello ihtiyacınız **meta veri URL'sini** çok[Springer bağlantı destek ekibi](mailto:identity@springernature.com).</span><span class="sxs-lookup"><span data-stu-id="66b3d-179">tooconfigure single sign-on on **Springer Link** side, you need toosend hello generated **Metadata URL** too[Springer Link support team](mailto:identity@springernature.com).</span></span>

> [!TIP]
> <span data-ttu-id="66b3d-180">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="66b3d-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="66b3d-181">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="66b3d-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="66b3d-182">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="66b3d-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="66b3d-183">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="66b3d-183">Create an Azure AD test user</span></span>

<span data-ttu-id="66b3d-184">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="66b3d-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="66b3d-186">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="66b3d-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="66b3d-187">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="66b3d-187">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-springerlink-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="66b3d-189">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="66b3d-189">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-springerlink-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="66b3d-191">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="66b3d-191">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-springerlink-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="66b3d-193">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="66b3d-193">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-springerlink-tutorial/create_aaduser_04.png)

    <span data-ttu-id="66b3d-195">a.</span><span class="sxs-lookup"><span data-stu-id="66b3d-195">a.</span></span> <span data-ttu-id="66b3d-196">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="66b3d-196">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="66b3d-197">b.</span><span class="sxs-lookup"><span data-stu-id="66b3d-197">b.</span></span> <span data-ttu-id="66b3d-198">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="66b3d-198">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="66b3d-199">c.</span><span class="sxs-lookup"><span data-stu-id="66b3d-199">c.</span></span> <span data-ttu-id="66b3d-200">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="66b3d-200">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="66b3d-201">d.</span><span class="sxs-lookup"><span data-stu-id="66b3d-201">d.</span></span> <span data-ttu-id="66b3d-202">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="66b3d-202">Click **Create**.</span></span>
 
### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="66b3d-203">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="66b3d-203">Assign hello Azure AD test user</span></span>

<span data-ttu-id="66b3d-204">Bu bölümde, erişim tooSpringer bağlantı vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="66b3d-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSpringer Link.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="66b3d-206">**tooassign Britta Simon tooSpringer bağlantı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="66b3d-206">**tooassign Britta Simon tooSpringer Link, perform hello following steps:**</span></span>

1. <span data-ttu-id="66b3d-207">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="66b3d-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="66b3d-209">Merhaba uygulamalar listesinde **Springer bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="66b3d-209">In hello applications list, select **Springer Link**.</span></span>

    ![Merhaba Springer bağlantıyı bağlantı hello uygulamalar listesinde](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_app.png)  

3. <span data-ttu-id="66b3d-211">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="66b3d-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="66b3d-213">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="66b3d-213">Click **Add** button.</span></span> <span data-ttu-id="66b3d-214">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="66b3d-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="66b3d-216">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="66b3d-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="66b3d-217">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="66b3d-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="66b3d-218">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="66b3d-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="66b3d-219">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="66b3d-219">Test single sign-on</span></span>

<span data-ttu-id="66b3d-220">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="66b3d-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="66b3d-221">Merhaba Springer bağlantı hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Springer bağlantı uygulaması almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="66b3d-221">When you click hello Springer Link tile in hello Access Panel, you should get automatically signed-on tooyour Springer Link application.</span></span>
<span data-ttu-id="66b3d-222">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="66b3d-222">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="66b3d-223">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="66b3d-223">Additional resources</span></span>

* [<span data-ttu-id="66b3d-224">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="66b3d-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="66b3d-225">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="66b3d-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_203.png

