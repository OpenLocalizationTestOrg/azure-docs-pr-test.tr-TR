---
title: "Öğretici: Azure Active Directory Tümleştirme edici Online ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory edici Online arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4fd6b29b-1b46-4fd1-9f5e-16b1c9d892cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: b728606ded7687d424a8175d0602b6b00f398497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bgs-online"></a><span data-ttu-id="309c6-103">Öğretici: Azure Active Directory Tümleştirme edici Online ile</span><span class="sxs-lookup"><span data-stu-id="309c6-103">Tutorial: Azure Active Directory integration with BGS Online</span></span>

<span data-ttu-id="309c6-104">Bu öğreticide, bilgi nasıl toointegrate edici çevrimiçi Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="309c6-104">In this tutorial, you learn how toointegrate BGS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="309c6-105">EDİCİ çevrimiçi Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="309c6-105">Integrating BGS Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="309c6-106">Erişim tooBGS çevrimiçi olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="309c6-106">You can control in Azure AD who has access tooBGS Online</span></span>
- <span data-ttu-id="309c6-107">Kullanıcıların tooautomatically get açan tooBGS çevrimiçi (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="309c6-107">You can enable your users tooautomatically get signed-on tooBGS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="309c6-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="309c6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="309c6-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="309c6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="309c6-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="309c6-110">Prerequisites</span></span>

<span data-ttu-id="309c6-111">tooconfigure edici Online ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="309c6-111">tooconfigure Azure AD integration with BGS Online, you need hello following items:</span></span>

- <span data-ttu-id="309c6-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="309c6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="309c6-113">Bir edici çevrimiçi çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="309c6-113">A BGS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="309c6-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="309c6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="309c6-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="309c6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="309c6-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="309c6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="309c6-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="309c6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="309c6-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="309c6-118">Scenario description</span></span>
<span data-ttu-id="309c6-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="309c6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="309c6-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="309c6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="309c6-121">EDİCİ çevrimiçi hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="309c6-121">Adding BGS Online from hello gallery</span></span>
2. <span data-ttu-id="309c6-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="309c6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bgs-online-from-hello-gallery"></a><span data-ttu-id="309c6-123">EDİCİ çevrimiçi hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="309c6-123">Adding BGS Online from hello gallery</span></span>
<span data-ttu-id="309c6-124">Azure AD'ye tooconfigure hello tümleştirme edici Online hello galeri tooyour yönetilen SaaS uygulamaları listesinden edici çevrimiçi tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="309c6-124">tooconfigure hello integration of BGS Online into Azure AD, you need tooadd BGS Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="309c6-125">**tooadd edici çevrimiçi hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="309c6-125">**tooadd BGS Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="309c6-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="309c6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="309c6-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="309c6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="309c6-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="309c6-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="309c6-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="309c6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="309c6-133">Merhaba arama kutusuna yazın **edici çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="309c6-133">In hello search box, type **BGS Online**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_search.png)

5. <span data-ttu-id="309c6-135">Merhaba Sonuçlar panelinde seçin **edici çevrimiçi**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="309c6-135">In hello results panel, select **BGS Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="309c6-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="309c6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="309c6-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma edici "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Online ile test etme</span><span class="sxs-lookup"><span data-stu-id="309c6-138">In this section, you configure and test Azure AD single sign-on with BGS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="309c6-139">Tek toowork'ın oturum açma hangi hello karşılık gelen edici çevrimiçi tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="309c6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BGS Online is tooa user in Azure AD.</span></span> <span data-ttu-id="309c6-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı edici Online'da arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="309c6-140">In other words, a link relationship between an Azure AD user and hello related user in BGS Online needs toobe established.</span></span>

<span data-ttu-id="309c6-141">Çevrimiçi edici'nde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="309c6-141">In BGS Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="309c6-142">tooconfigure ve edici Online ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="309c6-142">tooconfigure and test Azure AD single sign-on with BGS Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="309c6-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="309c6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="309c6-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="309c6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="309c6-145">**[EDİCİ çevrimiçi bir test kullanıcısı oluşturma](#creating-a-bgs-online-test-user)**  -toohave Britta Simon edici bağlantılı toohello Azure AD kullanıcı gösterimi olan Online'da, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="309c6-145">**[Creating a BGS Online test user](#creating-a-bgs-online-test-user)** - toohave a counterpart of Britta Simon in BGS Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="309c6-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="309c6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="309c6-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="309c6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="309c6-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="309c6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="309c6-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma edici çevrimiçi uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="309c6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BGS Online application.</span></span>

<span data-ttu-id="309c6-150">**tooconfigure Azure AD çoklu oturum açma edici Online ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="309c6-150">**tooconfigure Azure AD single sign-on with BGS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="309c6-151">Hello hello üzerinde Azure portal'ın **edici çevrimiçi** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="309c6-151">In hello Azure portal, on hello **BGS Online** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="309c6-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="309c6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_samlbase.png)

3. <span data-ttu-id="309c6-155">Merhaba üzerinde **edici çevrimiçi etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="309c6-155">On hello **BGS Online Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_url.png)

    <span data-ttu-id="309c6-157">a.</span><span class="sxs-lookup"><span data-stu-id="309c6-157">a.</span></span> <span data-ttu-id="309c6-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="309c6-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="309c6-159">Üretim ortamı için bu deseni kullanır`https://<company name>.millwardbrown.report`</span><span class="sxs-lookup"><span data-stu-id="309c6-159">For production environment, use this pattern `https://<company name>.millwardbrown.report`</span></span> 

    <span data-ttu-id="309c6-160">Test ortamı için bu deseni kullanır`https://millwardbrown.marketingtracker.nl/mt5/`</span><span class="sxs-lookup"><span data-stu-id="309c6-160">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/`</span></span>

    <span data-ttu-id="309c6-161">b.</span><span class="sxs-lookup"><span data-stu-id="309c6-161">b.</span></span> <span data-ttu-id="309c6-162">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="309c6-162">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    
    <span data-ttu-id="309c6-163">Üretim ortamı için bu deseni kullanır`https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="309c6-163">For production environment, use this pattern `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span></span> 
      
    <span data-ttu-id="309c6-164">Test ortamı için bu deseni kullanır`https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="309c6-164">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="309c6-165">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="309c6-165">These values are not real.</span></span> <span data-ttu-id="309c6-166">Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="309c6-166">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="309c6-167">Kişi [edici çevrimiçi destek ekibi](mailTo:bgsdashboardteam@millwardbrown.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="309c6-167">Contact [BGS Online support team](mailTo:bgsdashboardteam@millwardbrown.com) tooget these values.</span></span>
 

4. <span data-ttu-id="309c6-168">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="309c6-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_certificate.png) 

5. <span data-ttu-id="309c6-170">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="309c6-170">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bgsonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="309c6-172">Merhaba üzerinde **edici çevrimiçi yapılandırma** 'yi tıklatın **edici çevrimiçi yapılandırma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="309c6-172">On hello **BGS Online Configuration** section, click **Configure BGS Online** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="309c6-173">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="309c6-173">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_configure.png) 

7. <span data-ttu-id="309c6-175">tooconfigure çoklu oturum açma üzerinde **edici çevrimiçi** yan, indirilen toosend hello ihtiyacınız **meta veri XML** ve **SAML çoklu oturum açma hizmet URL'si** çok[edici Çevrimiçi destek ekibi](mailto:bgsdashboardteam@millwardbrown.com).</span><span class="sxs-lookup"><span data-stu-id="309c6-175">tooconfigure single sign-on on **BGS Online** side, you need toosend hello downloaded **Metadata XML** and **SAML Single Sign-On Service URL** too[BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com).</span></span> 


> [!TIP]
> <span data-ttu-id="309c6-176">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="309c6-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="309c6-177">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="309c6-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="309c6-178">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="309c6-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="309c6-179">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="309c6-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="309c6-180">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="309c6-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="309c6-182">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="309c6-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="309c6-183">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="309c6-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="309c6-185">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="309c6-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="309c6-187">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="309c6-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="309c6-189">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="309c6-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="309c6-191">a.</span><span class="sxs-lookup"><span data-stu-id="309c6-191">a.</span></span> <span data-ttu-id="309c6-192">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="309c6-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="309c6-193">b.</span><span class="sxs-lookup"><span data-stu-id="309c6-193">b.</span></span> <span data-ttu-id="309c6-194">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="309c6-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="309c6-195">c.</span><span class="sxs-lookup"><span data-stu-id="309c6-195">c.</span></span> <span data-ttu-id="309c6-196">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="309c6-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="309c6-197">d.</span><span class="sxs-lookup"><span data-stu-id="309c6-197">d.</span></span> <span data-ttu-id="309c6-198">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="309c6-198">Click **Create**.</span></span>
 
### <a name="creating-a-bgs-online-test-user"></a><span data-ttu-id="309c6-199">EDİCİ çevrimiçi bir test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="309c6-199">Creating a BGS Online test user</span></span>

<span data-ttu-id="309c6-200">Bu bölümde, Britta Simon edici çevrimiçi olarak adlandırılan bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="309c6-200">In this section, you create a user called Britta Simon in BGS Online.</span></span> <span data-ttu-id="309c6-201">Çalışmak [edici çevrimiçi destek ekibi](mailto:bgsdashboardteam@millwardbrown.com) tooadd hello kullanıcılar hello edici çevrimiçi Platform.</span><span class="sxs-lookup"><span data-stu-id="309c6-201">Work with [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com) tooadd hello users in hello BGS Online platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="309c6-202">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="309c6-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="309c6-203">Bu bölümde, çevrimiçi erişim tooBGS vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="309c6-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBGS Online.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="309c6-205">**tooassign çevrimiçi Britta Simon tooBGS hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="309c6-205">**tooassign Britta Simon tooBGS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="309c6-206">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="309c6-206">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="309c6-208">Merhaba uygulamalar listesinde **edici çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="309c6-208">In hello applications list, select **BGS Online**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_app.png) 

3. <span data-ttu-id="309c6-210">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="309c6-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="309c6-212">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="309c6-212">Click **Add** button.</span></span> <span data-ttu-id="309c6-213">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="309c6-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="309c6-215">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="309c6-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="309c6-216">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="309c6-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="309c6-217">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="309c6-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="309c6-218">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="309c6-218">Testing single sign-on</span></span>

<span data-ttu-id="309c6-219">Bu bölümde, Azure AD SSO yapılandırmanızı hello erişim paneli kullanarak sınayın.</span><span class="sxs-lookup"><span data-stu-id="309c6-219">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="309c6-220">Merhaba edici çevrimiçi hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour edici çevrimiçi uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="309c6-220">When you click hello BGS Online tile in hello Access Panel, you should get automatically signed-on tooyour BGS Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="309c6-221">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="309c6-221">Additional resources</span></span>

* [<span data-ttu-id="309c6-222">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="309c6-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="309c6-223">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="309c6-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_203.png

