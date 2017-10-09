---
title: "Öğretici: Azure Active Directory Tümleştirme ile BetterWorks | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile BetterWorks arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 9803593124318ea82e5a8888cc5a95b5da84472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a><span data-ttu-id="88931-103">Öğretici: Azure Active Directory Tümleştirme BetterWorks ile</span><span class="sxs-lookup"><span data-stu-id="88931-103">Tutorial: Azure Active Directory integration with BetterWorks</span></span>

<span data-ttu-id="88931-104">Bu öğreticide, bilgi nasıl toointegrate BetterWorks Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88931-104">In this tutorial, you learn how toointegrate BetterWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="88931-105">BetterWorks Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="88931-105">Integrating BetterWorks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="88931-106">Erişim tooBetterWorks sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="88931-106">You can control in Azure AD who has access tooBetterWorks</span></span>
- <span data-ttu-id="88931-107">Kullanıcıların tooautomatically get açan tooBetterWorks (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="88931-107">You can enable your users tooautomatically get signed-on tooBetterWorks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="88931-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="88931-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="88931-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="88931-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88931-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="88931-110">Prerequisites</span></span>

<span data-ttu-id="88931-111">tooconfigure BetterWorks ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="88931-111">tooconfigure Azure AD integration with BetterWorks, you need hello following items:</span></span>

- <span data-ttu-id="88931-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="88931-112">An Azure AD subscription</span></span>
- <span data-ttu-id="88931-113">Bir BetterWorks çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="88931-113">A BetterWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="88931-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="88931-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="88931-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="88931-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="88931-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="88931-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="88931-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88931-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="88931-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="88931-118">Scenario description</span></span>
<span data-ttu-id="88931-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="88931-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="88931-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="88931-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="88931-121">Merhaba Galerisi'nden BetterWorks ekleme</span><span class="sxs-lookup"><span data-stu-id="88931-121">Adding BetterWorks from hello gallery</span></span>
2. <span data-ttu-id="88931-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="88931-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-betterworks-from-hello-gallery"></a><span data-ttu-id="88931-123">Merhaba Galerisi'nden BetterWorks ekleme</span><span class="sxs-lookup"><span data-stu-id="88931-123">Adding BetterWorks from hello gallery</span></span>
<span data-ttu-id="88931-124">Azure AD'ye tooconfigure hello tümleştirme BetterWorks, tooadd BetterWorks hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="88931-124">tooconfigure hello integration of BetterWorks into Azure AD, you need tooadd BetterWorks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="88931-125">**tooadd BetterWorks hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="88931-125">**tooadd BetterWorks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="88931-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="88931-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="88931-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="88931-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="88931-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="88931-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="88931-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="88931-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="88931-133">Merhaba arama kutusuna yazın **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="88931-133">In hello search box, type **BetterWorks**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_search.png)

5. <span data-ttu-id="88931-135">Merhaba Sonuçlar panelinde seçin **BetterWorks**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="88931-135">In hello results panel, select **BetterWorks**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="88931-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="88931-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="88931-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı BetterWorks ile test etme</span><span class="sxs-lookup"><span data-stu-id="88931-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="88931-139">Tek toowork'ın oturum açma hangi hello karşılık gelen BetterWorks içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="88931-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BetterWorks is tooa user in Azure AD.</span></span> <span data-ttu-id="88931-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı BetterWorks hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="88931-140">In other words, a link relationship between an Azure AD user and hello related user in BetterWorks needs toobe established.</span></span>

<span data-ttu-id="88931-141">Merhaba hello değeri BetterWorks içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="88931-141">In BetterWorks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="88931-142">tooconfigure ve BetterWorks ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="88931-142">tooconfigure and test Azure AD single sign-on with BetterWorks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="88931-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="88931-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="88931-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="88931-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="88931-145">**[BetterWorks test kullanıcısı oluşturma](#creating-a-betterworks-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir BetterWorks içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="88931-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - toohave a counterpart of Britta Simon in BetterWorks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="88931-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="88931-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="88931-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="88931-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="88931-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="88931-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="88931-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma BetterWorks uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="88931-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BetterWorks application.</span></span>

<span data-ttu-id="88931-150">**tooconfigure Azure AD çoklu oturum açma ile BetterWorks, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="88931-150">**tooconfigure Azure AD single sign-on with BetterWorks, perform hello following steps:**</span></span>

1. <span data-ttu-id="88931-151">Hello hello üzerinde Azure portal'ın **BetterWorks** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="88931-151">In hello Azure portal, on hello **BetterWorks** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="88931-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="88931-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_samlbase.png)

3. <span data-ttu-id="88931-155">Merhaba üzerinde **BetterWorks etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP başlatılan modu**:</span><span class="sxs-lookup"><span data-stu-id="88931-155">On hello **BetterWorks Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url.png)

    <span data-ttu-id="88931-157">a.</span><span class="sxs-lookup"><span data-stu-id="88931-157">a.</span></span> <span data-ttu-id="88931-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://app.betterworks.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="88931-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://app.betterworks.com/saml2/metadata/`</span></span>

    <span data-ttu-id="88931-159">b.</span><span class="sxs-lookup"><span data-stu-id="88931-159">b.</span></span> <span data-ttu-id="88931-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://app.betterworks.com/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="88931-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://app.betterworks.com/saml2/acs/`</span></span>

4. <span data-ttu-id="88931-161">Merhaba üzerinde **BetterWorks etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **SP tarafından başlatılan modu**, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="88931-161">On hello **BetterWorks Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url1.png)

    <span data-ttu-id="88931-163">a.</span><span class="sxs-lookup"><span data-stu-id="88931-163">a.</span></span> <span data-ttu-id="88931-164">Tıklatın hello üzerinde **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="88931-164">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="88931-165">b.</span><span class="sxs-lookup"><span data-stu-id="88931-165">b.</span></span> <span data-ttu-id="88931-166">Merhaba, **oturum üzerinde URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://app.betterworks.com`</span><span class="sxs-lookup"><span data-stu-id="88931-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://app.betterworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="88931-167">Bunlar gerçek değerleri değildir.</span><span class="sxs-lookup"><span data-stu-id="88931-167">These are not real values.</span></span> <span data-ttu-id="88931-168">Bu değerleri hello ile yanıt URL'si, kimlik ve üzerinde gerçek oturum URL'yi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="88931-168">Update these values with hello Reply URL, Identifier and actual Sign On URL.</span></span> <span data-ttu-id="88931-169">Kişi [BetterWorks destek ekibi](mailto:support@betterworks.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="88931-169">Contact [BetterWorks support team](mailto:support@betterworks.com) tooget these values.</span></span>
 
4. <span data-ttu-id="88931-170">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="88931-170">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_certificate.png)  

5. <span data-ttu-id="88931-172">BetterWorks uygulama hello SAML onaylar belirli bir biçimde bekler.</span><span class="sxs-lookup"><span data-stu-id="88931-172">BetterWorks application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="88931-173">Bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="88931-173">Configure hello following claims for this application.</span></span> <span data-ttu-id="88931-174">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**özniteliği**" Merhaba uygulama sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="88931-174">You can manage hello values of these attributes from hello "**Attribute**" tab of hello application.</span></span> <span data-ttu-id="88931-175">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="88931-175">hello following screenshot shows an example for this.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_attribute.png)

6. <span data-ttu-id="88931-177">Merhaba üzerinde **SAML belirteci öznitelikleri** iletişim kutusunda, hello aşağıdaki tabloda, gösterilen her satır için gerçekleştirme adımları izleyerek hello:</span><span class="sxs-lookup"><span data-stu-id="88931-177">On hello **SAML token attributes** dialog, for each row shown in hello table below, perform hello following steps:</span></span>
 
   | <span data-ttu-id="88931-178">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="88931-178">Attribute Name</span></span> | <span data-ttu-id="88931-179">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="88931-179">Attribute Value</span></span> |
   | -------------- |  ------------ |
   | <span data-ttu-id="88931-180">saml_token</span><span class="sxs-lookup"><span data-stu-id="88931-180">saml_token</span></span>     | <span data-ttu-id="88931-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span><span class="sxs-lookup"><span data-stu-id="88931-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span></span> |

   <span data-ttu-id="88931-182">a.</span><span class="sxs-lookup"><span data-stu-id="88931-182">a.</span></span> <span data-ttu-id="88931-183">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="88931-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_05.png)

   <span data-ttu-id="88931-186">b.</span><span class="sxs-lookup"><span data-stu-id="88931-186">b.</span></span> <span data-ttu-id="88931-187">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="88931-187">In hello **Name** textbox, type hello attribute name shown for that row.</span></span> 

   <span data-ttu-id="88931-188">c.</span><span class="sxs-lookup"><span data-stu-id="88931-188">c.</span></span> <span data-ttu-id="88931-189">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="88931-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
   <span data-ttu-id="88931-190">d.</span><span class="sxs-lookup"><span data-stu-id="88931-190">d.</span></span> <span data-ttu-id="88931-191">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="88931-191">Click **Ok**.</span></span>

7. <span data-ttu-id="88931-192">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="88931-192">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-betterworks-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="88931-194">tooconfigure çoklu oturum açma üzerinde **BetterWorks** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[BetterWorks destek ekibi](mailto:support@betterworks.com).</span><span class="sxs-lookup"><span data-stu-id="88931-194">tooconfigure single sign-on on **BetterWorks** side, you need toosend hello downloaded **Metadata XML** too[BetterWorks support team](mailto:support@betterworks.com).</span></span>


> [!TIP]
> <span data-ttu-id="88931-195">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="88931-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="88931-196">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="88931-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="88931-197">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="88931-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="88931-198">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="88931-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="88931-199">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="88931-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="88931-201">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="88931-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="88931-202">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="88931-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-betterworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="88931-204">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="88931-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-betterworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="88931-206">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="88931-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="88931-208">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="88931-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="88931-210">a.</span><span class="sxs-lookup"><span data-stu-id="88931-210">a.</span></span> <span data-ttu-id="88931-211">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="88931-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="88931-212">b.</span><span class="sxs-lookup"><span data-stu-id="88931-212">b.</span></span> <span data-ttu-id="88931-213">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="88931-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="88931-214">c.</span><span class="sxs-lookup"><span data-stu-id="88931-214">c.</span></span> <span data-ttu-id="88931-215">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="88931-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="88931-216">d.</span><span class="sxs-lookup"><span data-stu-id="88931-216">d.</span></span> <span data-ttu-id="88931-217">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="88931-217">Click **Create**.</span></span>
 
### <a name="creating-a-betterworks-test-user"></a><span data-ttu-id="88931-218">BetterWorks test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="88931-218">Creating a BetterWorks test user</span></span>

<span data-ttu-id="88931-219">Bu bölümde, BetterWorks içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="88931-219">In this section, you create a user called Britta Simon in BetterWorks.</span></span> <span data-ttu-id="88931-220">Çalışmak [BetterWorks destek ekibi](mailto:support@betterworks.com) tooadd hello kullanıcılar hello BetterWorks Platform.</span><span class="sxs-lookup"><span data-stu-id="88931-220">Work with [BetterWorks support team](mailto:support@betterworks.com) tooadd hello users in hello BetterWorks platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="88931-221">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="88931-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="88931-222">Bu bölümde, erişim tooBetterWorks vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="88931-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBetterWorks.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="88931-224">**tooassign Britta Simon tooBetterWorks hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="88931-224">**tooassign Britta Simon tooBetterWorks, perform hello following steps:**</span></span>

1. <span data-ttu-id="88931-225">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="88931-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="88931-227">Merhaba uygulamalar listesinde **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="88931-227">In hello applications list, select **BetterWorks**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_app.png) 

3. <span data-ttu-id="88931-229">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="88931-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="88931-231">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="88931-231">Click **Add** button.</span></span> <span data-ttu-id="88931-232">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="88931-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="88931-234">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="88931-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="88931-235">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="88931-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="88931-236">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="88931-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="88931-237">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="88931-237">Testing single sign-on</span></span>

<span data-ttu-id="88931-238">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="88931-238">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="88931-239">Hello erişim paneli BetterWorks döşeme hello tıkladığınızda, otomatik olarak oturum açma BetterWorks uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="88931-239">When you click hello BetterWorks tile in hello Access Panel, you should get automatically signed-on tooyour BetterWorks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="88931-240">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="88931-240">Additional resources</span></span>

* [<span data-ttu-id="88931-241">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="88931-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="88931-242">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="88931-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png

