---
title: "Öğretici: Azure Active Directory Tümleştirme SCC yaşam | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile SCC yaşam döngüsü arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 63623c5bd2d951612040f0121615a406bf83e890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="09188-103">Öğretici: Azure Active Directory Tümleştirme ile SCC yaşam döngüsü</span><span class="sxs-lookup"><span data-stu-id="09188-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>

<span data-ttu-id="09188-104">Bu öğreticide, bilgi nasıl toointegrate SCC yaşam döngüsü Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="09188-104">In this tutorial, you learn how toointegrate SCC LifeCycle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="09188-105">SCC yaşam döngüsü Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="09188-105">Integrating SCC LifeCycle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="09188-106">Erişim tooSCC yaşam döngüsü sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="09188-106">You can control in Azure AD who has access tooSCC LifeCycle</span></span>
- <span data-ttu-id="09188-107">Kullanıcıların tooautomatically get açan tooSCC yaşam döngüsü (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="09188-107">You can enable your users tooautomatically get signed-on tooSCC LifeCycle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="09188-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="09188-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="09188-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="09188-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09188-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="09188-110">Prerequisites</span></span>

<span data-ttu-id="09188-111">tooconfigure SCC yaşam döngüsü ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="09188-111">tooconfigure Azure AD integration with SCC LifeCycle, you need hello following items:</span></span>

- <span data-ttu-id="09188-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="09188-112">An Azure AD subscription</span></span>
- <span data-ttu-id="09188-113">Bir SCC yaşam döngüsü çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="09188-113">An SCC LifeCycle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="09188-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="09188-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="09188-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="09188-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="09188-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="09188-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="09188-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="09188-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="09188-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="09188-118">Scenario description</span></span>
<span data-ttu-id="09188-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="09188-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="09188-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="09188-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="09188-121">Merhaba Galerisi'nden SCC yaşam döngüsü ekleme</span><span class="sxs-lookup"><span data-stu-id="09188-121">Adding SCC LifeCycle from hello gallery</span></span>
2. <span data-ttu-id="09188-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="09188-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scc-lifecycle-from-hello-gallery"></a><span data-ttu-id="09188-123">Merhaba Galerisi'nden SCC yaşam döngüsü ekleme</span><span class="sxs-lookup"><span data-stu-id="09188-123">Adding SCC LifeCycle from hello gallery</span></span>
<span data-ttu-id="09188-124">Azure AD'ye tooconfigure hello tümleştirme SCC yaşam döngüsünün tooadd SCC yaşam döngüsü hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="09188-124">tooconfigure hello integration of SCC LifeCycle into Azure AD, you need tooadd SCC LifeCycle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="09188-125">**tooadd SCC yaşam döngüsü hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="09188-125">**tooadd SCC LifeCycle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="09188-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="09188-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="09188-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="09188-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="09188-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="09188-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="09188-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="09188-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="09188-133">Merhaba arama kutusuna yazın **SCC yaşam döngüsü**.</span><span class="sxs-lookup"><span data-stu-id="09188-133">In hello search box, type **SCC LifeCycle**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_search.png)

5. <span data-ttu-id="09188-135">Merhaba Sonuçlar panelinde seçin **SCC yaşam döngüsü**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="09188-135">In hello results panel, select **SCC LifeCycle**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="09188-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="09188-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="09188-138">Bu bölümde, yapılandırmanız ve SCC yaşam döngüsü ile Azure AD çoklu oturum açmayı test "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="09188-138">In this section, you configure and test Azure AD single sign-on with SCC LifeCycle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="09188-139">Tek toowork'ın oturum açma hangi hello karşılık gelen SCC yaşam döngüsü içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="09188-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SCC LifeCycle is tooa user in Azure AD.</span></span> <span data-ttu-id="09188-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı SCC yaşam döngüsü hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="09188-140">In other words, a link relationship between an Azure AD user and hello related user in SCC LifeCycle needs toobe established.</span></span>

<span data-ttu-id="09188-141">Merhaba hello değeri SCC çevriminin atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="09188-141">In SCC LifeCycle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="09188-142">tooconfigure ve SCC yaşam döngüsü ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="09188-142">tooconfigure and test Azure AD single sign-on with SCC LifeCycle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="09188-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="09188-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="09188-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="09188-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="09188-145">**[SCC yaşam döngüsü test kullanıcısı oluşturma](#creating-an-scc-lifecycle-test-user)**  -toohave Britta Simon bağlantılı toohello Azure AD kullanıcı gösterimini SCC yaşam döngüsü içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="09188-145">**[Creating an SCC LifeCycle test user](#creating-an-scc-lifecycle-test-user)** - toohave a counterpart of Britta Simon in SCC LifeCycle that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="09188-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="09188-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="09188-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="09188-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="09188-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="09188-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="09188-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma SCC yaşam döngüsü uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="09188-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SCC LifeCycle application.</span></span>

<span data-ttu-id="09188-150">**tooconfigure Azure AD çoklu oturum açma SCC yaşam hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="09188-150">**tooconfigure Azure AD single sign-on with SCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="09188-151">Hello hello üzerinde Azure portal'ın **SCC yaşam döngüsü** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="09188-151">In hello Azure portal, on hello **SCC LifeCycle** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="09188-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="09188-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_samlbase.png)

3. <span data-ttu-id="09188-155">Merhaba üzerinde **SCC yaşam döngüsü etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="09188-155">On hello **SCC LifeCycle Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_url.png)

    <span data-ttu-id="09188-157">a.</span><span class="sxs-lookup"><span data-stu-id="09188-157">a.</span></span> <span data-ttu-id="09188-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<sub-domain>.scc.com/ic7/welcome/customer/PICTtest.aspx`</span><span class="sxs-lookup"><span data-stu-id="09188-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub-domain>.scc.com/ic7/welcome/customer/PICTtest.aspx`</span></span>

    <span data-ttu-id="09188-159">b.</span><span class="sxs-lookup"><span data-stu-id="09188-159">b.</span></span> <span data-ttu-id="09188-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="09188-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|--|
    | `https://bs1.scc.com/<entity>`|
    | `https://lifecycle.scc.com/<entity>`|
    
    > [!NOTE] 
    > <span data-ttu-id="09188-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="09188-161">These values are not real.</span></span> <span data-ttu-id="09188-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="09188-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="09188-163">Kişi [SCC yaşam döngüsü istemci destek ekibi](mailto:lifecycle.support@scc.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="09188-163">Contact [SCC LifeCycle Client support team](mailto:lifecycle.support@scc.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="09188-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="09188-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_certificate.png) 

5. <span data-ttu-id="09188-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="09188-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="09188-168">tooconfigure çoklu oturum açma üzerinde **SCC yaşam döngüsü** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[SCC yaşam döngüsü destek ekibi](mailto:lifecycle.support@scc.com).</span><span class="sxs-lookup"><span data-stu-id="09188-168">tooconfigure single sign-on on **SCC LifeCycle** side, you need toosend hello downloaded **Metadata XML** too[SCC LifeCycle support team](mailto:lifecycle.support@scc.com).</span></span> <span data-ttu-id="09188-169">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="09188-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

     >[!NOTE]
   ><span data-ttu-id="09188-170">Çoklu oturum açma hello SCC yaşam döngüsü destek ekibi tarafından etkin toobe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="09188-170">Single sign-on has toobe enabled by hello SCC LifeCycle support team.</span></span>
   > 
   > 

> [!TIP]
> <span data-ttu-id="09188-171">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="09188-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="09188-172">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="09188-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="09188-173">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="09188-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="09188-174">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="09188-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="09188-175">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="09188-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="09188-177">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="09188-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="09188-178">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="09188-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="09188-180">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="09188-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="09188-182">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="09188-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="09188-184">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="09188-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="09188-186">a.</span><span class="sxs-lookup"><span data-stu-id="09188-186">a.</span></span> <span data-ttu-id="09188-187">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="09188-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="09188-188">b.</span><span class="sxs-lookup"><span data-stu-id="09188-188">b.</span></span> <span data-ttu-id="09188-189">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="09188-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="09188-190">c.</span><span class="sxs-lookup"><span data-stu-id="09188-190">c.</span></span> <span data-ttu-id="09188-191">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="09188-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="09188-192">d.</span><span class="sxs-lookup"><span data-stu-id="09188-192">d.</span></span> <span data-ttu-id="09188-193">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="09188-193">Click **Create**.</span></span>
 
### <a name="creating-an-scc-lifecycle-test-user"></a><span data-ttu-id="09188-194">SCC yaşam döngüsü test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="09188-194">Creating an SCC LifeCycle test user</span></span>

<span data-ttu-id="09188-195">SCC yaşam döngüsü içine sipariş tooenable Azure AD kullanıcıların toolog bunların SCC yaşam döngüsü sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="09188-195">In order tooenable Azure AD users toolog into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="09188-196">TooSCC yaşam döngüsü, tooconfigure kullanıcı hazırlama için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="09188-196">There is no action item for you tooconfigure user provisioning tooSCC LifeCycle.</span></span>

<span data-ttu-id="09188-197">Atanan kullanıcı çalıştığında toolog girdiğinde SCC yaşam döngüsü, bir SCC yaşam döngüsü hesap gerekirse, otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="09188-197">When an assigned user tries toolog into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

> [!NOTE]
    > <span data-ttu-id="09188-198">Hello Azure Active Directory hesap sahibi bir e-posta alır ve onu etkinleştirilmeden önce bir bağlantı tooconfirm hesaplarında izler.</span><span class="sxs-lookup"><span data-stu-id="09188-198">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="09188-199">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="09188-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="09188-200">Bu bölümde, erişim tooSCC yaşam döngüsü vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="09188-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSCC LifeCycle.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="09188-202">**tooassign Britta Simon tooSCC yaşam döngüsü, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="09188-202">**tooassign Britta Simon tooSCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="09188-203">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="09188-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications.**</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="09188-205">Merhaba uygulamalar listesinde **SCC yaşam döngüsü**.</span><span class="sxs-lookup"><span data-stu-id="09188-205">In hello applications list, select **SCC LifeCycle**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_app.png) 

3. <span data-ttu-id="09188-207">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="09188-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="09188-209">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="09188-209">Click **Add** button.</span></span> <span data-ttu-id="09188-210">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="09188-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="09188-212">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="09188-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="09188-213">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="09188-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="09188-214">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="09188-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="09188-215">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="09188-215">Testing single sign-on</span></span>

<span data-ttu-id="09188-216">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="09188-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="09188-217">SCC yaşam döngüsü döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma yaşam döngüsü uygulama tooSCC almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="09188-217">When you click hello SCC LifeCycle tile in hello Access Panel, you should get automatically signed-on tooSCC LifeCycle application.</span></span>
<span data-ttu-id="09188-218">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="09188-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="09188-219">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="09188-219">Additional resources</span></span>

* [<span data-ttu-id="09188-220">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="09188-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="09188-221">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="09188-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_203.png

