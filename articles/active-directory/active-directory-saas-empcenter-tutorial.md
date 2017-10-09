---
title: "Öğretici: Azure Active Directory Tümleştirme ile EmpCenter | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile EmpCenter arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a00ecf6e-917a-4284-b998-41506931585e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: cce5d86db550327eb73660fb78cea7e6d5428890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-empcenter"></a><span data-ttu-id="c4e28-103">Öğretici: Azure Active Directory Tümleştirme EmpCenter ile</span><span class="sxs-lookup"><span data-stu-id="c4e28-103">Tutorial: Azure Active Directory integration with EmpCenter</span></span>

<span data-ttu-id="c4e28-104">Bu öğreticide, bilgi nasıl toointegrate EmpCenter Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c4e28-104">In this tutorial, you learn how toointegrate EmpCenter with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c4e28-105">EmpCenter Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="c4e28-105">Integrating EmpCenter with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c4e28-106">Erişim tooEmpCenter sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c4e28-106">You can control in Azure AD who has access tooEmpCenter</span></span>
- <span data-ttu-id="c4e28-107">Kullanıcıların tooautomatically get açan tooEmpCenter (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c4e28-107">You can enable your users tooautomatically get signed-on tooEmpCenter (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c4e28-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="c4e28-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c4e28-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c4e28-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4e28-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c4e28-110">Prerequisites</span></span>

<span data-ttu-id="c4e28-111">tooconfigure EmpCenter ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c4e28-111">tooconfigure Azure AD integration with EmpCenter, you need hello following items:</span></span>

- <span data-ttu-id="c4e28-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="c4e28-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c4e28-113">Bir EmpCenter çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="c4e28-113">An EmpCenter single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c4e28-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="c4e28-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c4e28-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="c4e28-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c4e28-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c4e28-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c4e28-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c4e28-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c4e28-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="c4e28-118">Scenario description</span></span>
<span data-ttu-id="c4e28-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="c4e28-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c4e28-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="c4e28-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c4e28-121">Merhaba Galerisi'nden EmpCenter ekleme</span><span class="sxs-lookup"><span data-stu-id="c4e28-121">Adding EmpCenter from hello gallery</span></span>
2. <span data-ttu-id="c4e28-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c4e28-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-empcenter-from-hello-gallery"></a><span data-ttu-id="c4e28-123">Merhaba Galerisi'nden EmpCenter ekleme</span><span class="sxs-lookup"><span data-stu-id="c4e28-123">Adding EmpCenter from hello gallery</span></span>
<span data-ttu-id="c4e28-124">Azure AD'ye tooconfigure hello tümleştirme EmpCenter, tooadd EmpCenter hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4e28-124">tooconfigure hello integration of EmpCenter into Azure AD, you need tooadd EmpCenter from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c4e28-125">**tooadd EmpCenter hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c4e28-125">**tooadd EmpCenter from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4e28-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c4e28-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c4e28-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="c4e28-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c4e28-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c4e28-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="c4e28-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c4e28-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="c4e28-133">Merhaba arama kutusuna yazın **EmpCenter**.</span><span class="sxs-lookup"><span data-stu-id="c4e28-133">In hello search box, type **EmpCenter**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_search.png)

5. <span data-ttu-id="c4e28-135">Merhaba Sonuçlar panelinde seçin **EmpCenter**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="c4e28-135">In hello results panel, select **EmpCenter**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c4e28-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c4e28-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c4e28-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı EmpCenter sınayın.</span><span class="sxs-lookup"><span data-stu-id="c4e28-138">In this section, you configure and test Azure AD single sign-on with EmpCenter based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c4e28-139">Tek toowork'ın oturum açma hangi hello karşılık gelen EmpCenter içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4e28-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EmpCenter is tooa user in Azure AD.</span></span> <span data-ttu-id="c4e28-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı EmpCenter hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4e28-140">In other words, a link relationship between an Azure AD user and hello related user in EmpCenter needs toobe established.</span></span>

<span data-ttu-id="c4e28-141">Merhaba hello değeri EmpCenter içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="c4e28-141">In EmpCenter, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c4e28-142">tooconfigure ve EmpCenter ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c4e28-142">tooconfigure and test Azure AD single sign-on with EmpCenter, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c4e28-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="c4e28-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c4e28-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="c4e28-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c4e28-145">**[Bir EmpCenter test kullanıcısı oluşturma](#creating-an-empcenter-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir EmpCenter içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="c4e28-145">**[Creating an EmpCenter test user](#creating-an-empcenter-test-user)** - toohave a counterpart of Britta Simon in EmpCenter that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c4e28-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="c4e28-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c4e28-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="c4e28-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c4e28-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c4e28-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c4e28-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma EmpCenter uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c4e28-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EmpCenter application.</span></span>

<span data-ttu-id="c4e28-150">**tooconfigure Azure AD çoklu oturum açma ile EmpCenter, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c4e28-150">**tooconfigure Azure AD single sign-on with EmpCenter, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4e28-151">Hello hello üzerinde Azure portal'ın **EmpCenter** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c4e28-151">In hello Azure portal, on hello **EmpCenter** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="c4e28-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="c4e28-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_samlbase.png)

3. <span data-ttu-id="c4e28-155">Merhaba üzerinde **EmpCenter etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c4e28-155">On hello **EmpCenter Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_url.png)

    <span data-ttu-id="c4e28-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="c4e28-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.EmpCenter.com/<instancename>` |
    | `https://<subdomain>.workforcehosting.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="c4e28-158">Merhaba değeri gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="c4e28-158">hello value is not real.</span></span> <span data-ttu-id="c4e28-159">Güncelleştirme hello değerle hello gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="c4e28-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="c4e28-160">Kişi [EmpCenter istemci destek ekibi](http://www.workforcesoftware.com/services/customer-support/) tooget hello değeri.</span><span class="sxs-lookup"><span data-stu-id="c4e28-160">Contact [EmpCenter Client support team](http://www.workforcesoftware.com/services/customer-support/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="c4e28-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c4e28-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_certificate.png) 

5. <span data-ttu-id="c4e28-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c4e28-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c4e28-165">tooconfigure çoklu oturum açma üzerinde **EmpCenter** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[EmpCenter destek ekibi](http://www.workforcesoftware.com/services/customer-support/).</span><span class="sxs-lookup"><span data-stu-id="c4e28-165">tooconfigure single sign-on on **EmpCenter** side, you need toosend hello downloaded **Metadata XML** too[EmpCenter support team](http://www.workforcesoftware.com/services/customer-support/).</span></span> <span data-ttu-id="c4e28-166">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c4e28-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c4e28-167">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="c4e28-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c4e28-168">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="c4e28-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c4e28-169">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c4e28-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c4e28-170">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4e28-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="c4e28-171">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="c4e28-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="c4e28-173">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c4e28-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4e28-174">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c4e28-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c4e28-176">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c4e28-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c4e28-178">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="c4e28-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c4e28-180">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c4e28-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c4e28-182">a.</span><span class="sxs-lookup"><span data-stu-id="c4e28-182">a.</span></span> <span data-ttu-id="c4e28-183">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c4e28-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c4e28-184">b.</span><span class="sxs-lookup"><span data-stu-id="c4e28-184">b.</span></span> <span data-ttu-id="c4e28-185">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="c4e28-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c4e28-186">c.</span><span class="sxs-lookup"><span data-stu-id="c4e28-186">c.</span></span> <span data-ttu-id="c4e28-187">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="c4e28-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c4e28-188">d.</span><span class="sxs-lookup"><span data-stu-id="c4e28-188">d.</span></span> <span data-ttu-id="c4e28-189">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c4e28-189">Click **Create**.</span></span>
 
### <a name="creating-an-empcenter-test-user"></a><span data-ttu-id="c4e28-190">Bir EmpCenter test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4e28-190">Creating an EmpCenter test user</span></span>

<span data-ttu-id="c4e28-191">TooEmpCenter içinde sipariş tooenable Azure AD kullanıcıların toolog bunların EmpCenter sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c4e28-191">In order tooenable Azure AD users toolog in tooEmpCenter, they must be provisioned into EmpCenter.</span></span> <span data-ttu-id="c4e28-192">EmpCenter Hello durumda hello kullanıcı hesapları tarafından oluşturulan toobe gerekir, [EmpCenter destek ekibi](http://www.workforcesoftware.com/services/customer-support/).</span><span class="sxs-lookup"><span data-stu-id="c4e28-192">In hello case of EmpCenter, hello user accounts need toobe created by your [EmpCenter support team](http://www.workforcesoftware.com/services/customer-support/).</span></span>

> [!NOTE]
> <span data-ttu-id="c4e28-193">API, kullanıcı hesaplarını EmpCenter tooprovision Azure Active Directory tarafından sağlanan veya herhangi diğer EmpCenter kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4e28-193">You can use any other EmpCenter user account creation tools or APIs provided by EmpCenter tooprovision Azure Active Directory user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c4e28-194">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="c4e28-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c4e28-195">Bu bölümde, erişim tooEmpCenter vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c4e28-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEmpCenter.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="c4e28-197">**tooassign Britta Simon tooEmpCenter hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c4e28-197">**tooassign Britta Simon tooEmpCenter, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4e28-198">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c4e28-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="c4e28-200">Merhaba uygulamalar listesinde **EmpCenter**.</span><span class="sxs-lookup"><span data-stu-id="c4e28-200">In hello applications list, select **EmpCenter**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_app.png) 

3. <span data-ttu-id="c4e28-202">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c4e28-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="c4e28-204">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c4e28-204">Click **Add** button.</span></span> <span data-ttu-id="c4e28-205">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c4e28-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="c4e28-207">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="c4e28-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c4e28-208">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c4e28-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c4e28-209">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c4e28-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c4e28-210">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="c4e28-210">Testing single sign-on</span></span>


<span data-ttu-id="c4e28-211">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c4e28-211">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c4e28-212">Merhaba EmpCenter hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour EmpCenter uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4e28-212">When you click hello EmpCenter tile in hello Access Panel, you should get automatically signed-on tooyour EmpCenter application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c4e28-213">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c4e28-213">Additional resources</span></span>

* [<span data-ttu-id="c4e28-214">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="c4e28-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c4e28-215">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="c4e28-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_203.png

