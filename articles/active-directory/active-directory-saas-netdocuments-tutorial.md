---
title: "Öğretici: Azure Active Directory Tümleştirme ile NetDocuments | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile NetDocuments arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee9887553595a2492642aed4cb4abcd11d9cf599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="d091a-103">Öğretici: Azure Active Directory Tümleştirme NetDocuments ile</span><span class="sxs-lookup"><span data-stu-id="d091a-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>

<span data-ttu-id="d091a-104">Bu öğreticide, bilgi nasıl toointegrate NetDocuments Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d091a-104">In this tutorial, you learn how toointegrate NetDocuments with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d091a-105">NetDocuments Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="d091a-105">Integrating NetDocuments with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d091a-106">Erişim tooNetDocuments sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d091a-106">You can control in Azure AD who has access tooNetDocuments</span></span>
- <span data-ttu-id="d091a-107">Kullanıcıların tooautomatically get açan tooNetDocuments (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d091a-107">You can enable your users tooautomatically get signed-on tooNetDocuments (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d091a-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="d091a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d091a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d091a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d091a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d091a-110">Prerequisites</span></span>

<span data-ttu-id="d091a-111">tooconfigure NetDocuments ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d091a-111">tooconfigure Azure AD integration with NetDocuments, you need hello following items:</span></span>

- <span data-ttu-id="d091a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="d091a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d091a-113">Bir NetDocuments çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="d091a-113">A NetDocuments single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d091a-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="d091a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d091a-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="d091a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d091a-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="d091a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d091a-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d091a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d091a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="d091a-118">Scenario description</span></span>
<span data-ttu-id="d091a-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="d091a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d091a-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="d091a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d091a-121">Merhaba Galerisi'nden NetDocuments ekleme</span><span class="sxs-lookup"><span data-stu-id="d091a-121">Adding NetDocuments from hello gallery</span></span>
2. <span data-ttu-id="d091a-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d091a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netdocuments-from-hello-gallery"></a><span data-ttu-id="d091a-123">Merhaba Galerisi'nden NetDocuments ekleme</span><span class="sxs-lookup"><span data-stu-id="d091a-123">Adding NetDocuments from hello gallery</span></span>
<span data-ttu-id="d091a-124">Azure AD'ye tooconfigure hello tümleştirme NetDocuments, tooadd NetDocuments hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="d091a-124">tooconfigure hello integration of NetDocuments into Azure AD, you need tooadd NetDocuments from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d091a-125">**tooadd NetDocuments hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d091a-125">**tooadd NetDocuments from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d091a-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d091a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d091a-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="d091a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d091a-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d091a-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="d091a-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d091a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="d091a-133">Merhaba arama kutusuna yazın **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="d091a-133">In hello search box, type **NetDocuments**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. <span data-ttu-id="d091a-135">Merhaba Sonuçlar panelinde seçin **NetDocuments**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="d091a-135">In hello results panel, select **NetDocuments**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d091a-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d091a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d091a-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı NetDocuments sınayın.</span><span class="sxs-lookup"><span data-stu-id="d091a-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d091a-139">Tek toowork'ın oturum açma hangi hello karşılık gelen NetDocuments içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="d091a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in NetDocuments is tooa user in Azure AD.</span></span> <span data-ttu-id="d091a-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı NetDocuments hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="d091a-140">In other words, a link relationship between an Azure AD user and hello related user in NetDocuments needs toobe established.</span></span>

<span data-ttu-id="d091a-141">Merhaba hello değeri NetDocuments içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="d091a-141">In NetDocuments, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d091a-142">tooconfigure ve NetDocuments ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d091a-142">tooconfigure and test Azure AD single sign-on with NetDocuments, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d091a-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="d091a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d091a-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="d091a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d091a-145">**[NetDocuments test kullanıcısı oluşturma](#creating-a-netdocuments-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir NetDocuments içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="d091a-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - toohave a counterpart of Britta Simon in NetDocuments that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d091a-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="d091a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d091a-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="d091a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d091a-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d091a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d091a-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma NetDocuments uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d091a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your NetDocuments application.</span></span>

<span data-ttu-id="d091a-150">**tooconfigure Azure AD çoklu oturum açma ile NetDocuments, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d091a-150">**tooconfigure Azure AD single sign-on with NetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="d091a-151">Hello hello üzerinde Azure portal'ın **NetDocuments** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="d091a-151">In hello Azure portal, on hello **NetDocuments** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="d091a-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="d091a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. <span data-ttu-id="d091a-155">Merhaba üzerinde **NetDocuments etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d091a-155">On hello **NetDocuments Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    <span data-ttu-id="d091a-157">a.</span><span class="sxs-lookup"><span data-stu-id="d091a-157">a.</span></span> <span data-ttu-id="d091a-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="d091a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    <span data-ttu-id="d091a-159">b.</span><span class="sxs-lookup"><span data-stu-id="d091a-159">b.</span></span> <span data-ttu-id="d091a-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="d091a-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d091a-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="d091a-161">These values are not real.</span></span> <span data-ttu-id="d091a-162">Bu değerler, oturum açma hello gerçek URL'si ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d091a-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="d091a-163">Kişi [NetDocuments destek ekibi](https://support.netdocuments.com/hc/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="d091a-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) tooget these values.</span></span>
 
4. <span data-ttu-id="d091a-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d091a-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. <span data-ttu-id="d091a-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d091a-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d091a-168">Farklı web tarayıcısı penceresinde NetDocuments şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d091a-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>

7. <span data-ttu-id="d091a-169">Çok Git**yönetici**.</span><span class="sxs-lookup"><span data-stu-id="d091a-169">Go too**Admin**.</span></span>

8. <span data-ttu-id="d091a-170">Tıklatın **ekleme ve kaldırma kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d091a-170">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="d091a-171">![Depo](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "deposu")</span><span class="sxs-lookup"><span data-stu-id="d091a-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

9. <span data-ttu-id="d091a-172">Tıklatın **Gelişmiş kimlik doğrulama Seçenekleri Yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="d091a-172">Click **Configure advanced authentication options**.</span></span>
    
    <span data-ttu-id="d091a-173">![Gelişmiş kimlik doğrulama Seçenekleri Yapılandır](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Gelişmiş kimlik doğrulama seçeneklerini yapılandırma")</span><span class="sxs-lookup"><span data-stu-id="d091a-173">![Configure advanced authentication options](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span></span>

10. <span data-ttu-id="d091a-174">Merhaba üzerinde **Federal Kimlik** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d091a-174">On hello **Federated Identity** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="d091a-175">![Identitty Federasyon](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Identitty Federasyon")</span><span class="sxs-lookup"><span data-stu-id="d091a-175">![Federated Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Federated Identitty")</span></span>
   
    <span data-ttu-id="d091a-176">a.</span><span class="sxs-lookup"><span data-stu-id="d091a-176">a.</span></span> <span data-ttu-id="d091a-177">Olarak **kimlik sunucu türü Federasyon**seçin **Active Directory Federasyon Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="d091a-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   
    <span data-ttu-id="d091a-178">b.</span><span class="sxs-lookup"><span data-stu-id="d091a-178">b.</span></span> <span data-ttu-id="d091a-179">Tıklatın **dosya**, tooupload hello Azure Portalı'ndan indirilen meta veri dosyası indirilir.</span><span class="sxs-lookup"><span data-stu-id="d091a-179">Click **Choose file**, tooupload hello downloaded metadata file which you have downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="d091a-180">c.</span><span class="sxs-lookup"><span data-stu-id="d091a-180">c.</span></span> <span data-ttu-id="d091a-181">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d091a-181">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="d091a-182">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="d091a-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d091a-183">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="d091a-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d091a-184">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d091a-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d091a-185">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d091a-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="d091a-186">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="d091a-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="d091a-188">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d091a-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d091a-189">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d091a-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d091a-191">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="d091a-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d091a-193">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="d091a-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d091a-195">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d091a-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d091a-197">a.</span><span class="sxs-lookup"><span data-stu-id="d091a-197">a.</span></span> <span data-ttu-id="d091a-198">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d091a-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d091a-199">b.</span><span class="sxs-lookup"><span data-stu-id="d091a-199">b.</span></span> <span data-ttu-id="d091a-200">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="d091a-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d091a-201">c.</span><span class="sxs-lookup"><span data-stu-id="d091a-201">c.</span></span> <span data-ttu-id="d091a-202">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="d091a-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d091a-203">d.</span><span class="sxs-lookup"><span data-stu-id="d091a-203">d.</span></span> <span data-ttu-id="d091a-204">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d091a-204">Click **Create**.</span></span>
 
### <a name="creating-a-netdocuments-test-user"></a><span data-ttu-id="d091a-205">NetDocuments test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d091a-205">Creating a NetDocuments test user</span></span>

<span data-ttu-id="d091a-206">tooenable Azure AD kullanıcıların toolog tooNetDocuments bunların NetDocuments sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d091a-206">tooenable Azure AD users toolog in tooNetDocuments, they must be provisioned into NetDocuments.</span></span>  
<span data-ttu-id="d091a-207">NetDocuments Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="d091a-207">In hello case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="d091a-208">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d091a-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="d091a-209">Üzerinde tooyour SING **NetDocuments** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="d091a-209">Sing on tooyour **NetDocuments** company site as administrator.</span></span>

2. <span data-ttu-id="d091a-210">Hello içinde hello üst menüsünde **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="d091a-210">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="d091a-211">![Yönetici](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="d091a-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span></span>

3. <span data-ttu-id="d091a-212">Tıklatın **ekleme ve kaldırma kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d091a-212">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="d091a-213">![Depo](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "deposu")</span><span class="sxs-lookup"><span data-stu-id="d091a-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

4. <span data-ttu-id="d091a-214">Merhaba, **e-posta adresi** metin kutusuna, türü hello e-posta adresi geçerli bir Azure Active Directory hesabı tooprovision istediğiniz ve ardından **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d091a-214">In hello **Email Address** textbox, type hello email address of a valid Azure Active Directory account you want tooprovision, and then click **Add User**.</span></span>
   
    <span data-ttu-id="d091a-215">![E-posta adresi](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "e-posta adresi")</span><span class="sxs-lookup"><span data-stu-id="d091a-215">![Email Address](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="d091a-216">Hello Azure Active Directory hesap sahibi etkin hale önce bir bağlantı tooconfirm hello hesabını içeren bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="d091a-216">hello Azure Active Directory account holder will get an email that includes a link tooconfirm hello account before it becomes active.</span></span> <span data-ttu-id="d091a-217">API, kullanıcı hesaplarını NetDocuments tooprovision Azure Active Directory tarafından sağlanan veya herhangi diğer NetDocuments kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d091a-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d091a-218">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="d091a-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d091a-219">Bu bölümde, erişim tooNetDocuments vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d091a-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetDocuments.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="d091a-221">**tooassign Britta Simon tooNetDocuments hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d091a-221">**tooassign Britta Simon tooNetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="d091a-222">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d091a-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="d091a-224">Merhaba uygulamalar listesinde **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="d091a-224">In hello applications list, select **NetDocuments**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. <span data-ttu-id="d091a-226">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d091a-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="d091a-228">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d091a-228">Click **Add** button.</span></span> <span data-ttu-id="d091a-229">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d091a-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="d091a-231">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="d091a-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d091a-232">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d091a-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d091a-233">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d091a-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d091a-234">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="d091a-234">Testing single sign-on</span></span>

<span data-ttu-id="d091a-235">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="d091a-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d091a-236">Hello erişim paneli NetDocuments döşeme hello tıkladığınızda, otomatik olarak oturum açma NetDocuments uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d091a-236">When you click hello NetDocuments tile in hello Access Panel, you should get automatically signed-on tooyour NetDocuments application.</span></span>
<span data-ttu-id="d091a-237">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d091a-237">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d091a-238">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d091a-238">Additional resources</span></span>

* [<span data-ttu-id="d091a-239">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="d091a-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d091a-240">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="d091a-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png

