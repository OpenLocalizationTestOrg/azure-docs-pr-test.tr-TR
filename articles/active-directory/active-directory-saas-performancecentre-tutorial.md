---
title: "Öğretici: Azure Active Directory Tümleştirme ile PerformanceCentre | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile PerformanceCentre arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 19781c0087093a67c70dc90072cf1a119bb2ade0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a><span data-ttu-id="2e1a8-103">Öğretici: Azure Active Directory Tümleştirme PerformanceCentre ile</span><span class="sxs-lookup"><span data-stu-id="2e1a8-103">Tutorial: Azure Active Directory integration with PerformanceCentre</span></span>

<span data-ttu-id="2e1a8-104">Bu öğreticide, bilgi nasıl toointegrate PerformanceCentre Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2e1a8-104">In this tutorial, you learn how toointegrate PerformanceCentre with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2e1a8-105">PerformanceCentre Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="2e1a8-105">Integrating PerformanceCentre with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2e1a8-106">Erişim tooPerformanceCentre sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2e1a8-106">You can control in Azure AD who has access tooPerformanceCentre</span></span>
- <span data-ttu-id="2e1a8-107">Kullanıcıların tooautomatically get açan tooPerformanceCentre (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2e1a8-107">You can enable your users tooautomatically get signed-on tooPerformanceCentre (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2e1a8-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="2e1a8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2e1a8-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2e1a8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e1a8-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2e1a8-110">Prerequisites</span></span>

<span data-ttu-id="2e1a8-111">tooconfigure PerformanceCentre ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2e1a8-111">tooconfigure Azure AD integration with PerformanceCentre, you need hello following items:</span></span>

- <span data-ttu-id="2e1a8-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="2e1a8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2e1a8-113">Bir PerformanceCentre çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="2e1a8-113">A PerformanceCentre single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2e1a8-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2e1a8-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="2e1a8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2e1a8-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2e1a8-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2e1a8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2e1a8-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="2e1a8-118">Scenario description</span></span>
<span data-ttu-id="2e1a8-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2e1a8-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="2e1a8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2e1a8-121">Merhaba Galerisi'nden PerformanceCentre ekleme</span><span class="sxs-lookup"><span data-stu-id="2e1a8-121">Adding PerformanceCentre from hello gallery</span></span>
2. <span data-ttu-id="2e1a8-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2e1a8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-performancecentre-from-hello-gallery"></a><span data-ttu-id="2e1a8-123">Merhaba Galerisi'nden PerformanceCentre ekleme</span><span class="sxs-lookup"><span data-stu-id="2e1a8-123">Adding PerformanceCentre from hello gallery</span></span>
<span data-ttu-id="2e1a8-124">Azure AD'ye tooconfigure hello tümleştirme PerformanceCentre, tooadd PerformanceCentre hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-124">tooconfigure hello integration of PerformanceCentre into Azure AD, you need tooadd PerformanceCentre from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2e1a8-125">**tooadd PerformanceCentre hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2e1a8-125">**tooadd PerformanceCentre from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e1a8-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2e1a8-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2e1a8-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="2e1a8-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="2e1a8-133">Merhaba arama kutusuna yazın **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-133">In hello search box, type **PerformanceCentre**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_search.png)

5. <span data-ttu-id="2e1a8-135">Merhaba Sonuçlar panelinde seçin **PerformanceCentre**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-135">In hello results panel, select **PerformanceCentre**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2e1a8-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2e1a8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2e1a8-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı PerformanceCentre sınayın.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-138">In this section, you configure and test Azure AD single sign-on with PerformanceCentre based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2e1a8-139">Tek toowork'ın oturum açma hangi hello karşılık gelen PerformanceCentre içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PerformanceCentre is tooa user in Azure AD.</span></span> <span data-ttu-id="2e1a8-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı PerformanceCentre hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-140">In other words, a link relationship between an Azure AD user and hello related user in PerformanceCentre needs toobe established.</span></span>

<span data-ttu-id="2e1a8-141">Merhaba hello değeri PerformanceCentre içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-141">In PerformanceCentre, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2e1a8-142">tooconfigure ve PerformanceCentre ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2e1a8-142">tooconfigure and test Azure AD single sign-on with PerformanceCentre, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2e1a8-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2e1a8-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2e1a8-145">**[PerformanceCentre test kullanıcısı oluşturma](#creating-a-performancecentre-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir PerformanceCentre içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-145">**[Creating a PerformanceCentre test user](#creating-a-performancecentre-test-user)** - toohave a counterpart of Britta Simon in PerformanceCentre that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2e1a8-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2e1a8-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2e1a8-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2e1a8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2e1a8-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma PerformanceCentre uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PerformanceCentre application.</span></span>

<span data-ttu-id="2e1a8-150">**tooconfigure Azure AD çoklu oturum açma ile PerformanceCentre, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2e1a8-150">**tooconfigure Azure AD single sign-on with PerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e1a8-151">Hello hello üzerinde Azure portal'ın **PerformanceCentre** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-151">In hello Azure portal, on hello **PerformanceCentre** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="2e1a8-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_samlbase.png)

3. <span data-ttu-id="2e1a8-155">Merhaba üzerinde **PerformanceCentre etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2e1a8-155">On hello **PerformanceCentre Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_url.png)

    <span data-ttu-id="2e1a8-157">a.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-157">a.</span></span> <span data-ttu-id="2e1a8-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`http://companyname.performancecentre.com/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="2e1a8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://companyname.performancecentre.com/saml/SSO`</span></span>

    <span data-ttu-id="2e1a8-159">b.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-159">b.</span></span> <span data-ttu-id="2e1a8-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`http://companyname.performancecentre.com`</span><span class="sxs-lookup"><span data-stu-id="2e1a8-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://companyname.performancecentre.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2e1a8-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-161">These values are not real.</span></span> <span data-ttu-id="2e1a8-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2e1a8-163">Kişi [PerformanceCentre istemci destek ekibi](https://www.performancecentre.com/contact-us/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-163">Contact [PerformanceCentre Client support team](https://www.performancecentre.com/contact-us/) tooget these values.</span></span> 

4. <span data-ttu-id="2e1a8-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_certificate.png) 

5. <span data-ttu-id="2e1a8-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-performancecentre-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2e1a8-168">Merhaba üzerinde **PerformanceCentre yapılandırma** 'yi tıklatın **yapılandırma PerformanceCentre** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-168">On hello **PerformanceCentre Configuration** section, click **Configure PerformanceCentre** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2e1a8-169">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="2e1a8-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_configure.png) 

7. <span data-ttu-id="2e1a8-171">Oturum açma tooyour **PerformanceCentre** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-171">Sign-on tooyour **PerformanceCentre** company site as administrator.</span></span>

8. <span data-ttu-id="2e1a8-172">Merhaba hello sol tarafında, sekmesini **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-172">In hello tab on hello left side, click **Configure**.</span></span>
   
    ![Azure AD çoklu oturum açma][10]

9. <span data-ttu-id="2e1a8-174">Merhaba hello sol tarafında, sekmesini **çeşitli**ve ardından **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-174">In hello tab on hello left side, click **Miscellaneous**, and then click **Single Sign On**.</span></span>
   
    ![Azure AD çoklu oturum açma][11]

10. <span data-ttu-id="2e1a8-176">Olarak **Protokolü**seçin **SAML**.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-176">As **Protocol**, select **SAML**.</span></span>
   
    ![Azure AD çoklu oturum açma][12]

11. <span data-ttu-id="2e1a8-178">Açık, indirilen meta veri dosyası Not Defteri'nde, kopyalama hello içeriği yapıştırın, hello **kimlik sağlayıcısı meta verileri** metin kutusuna ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-178">Open your downloaded metadata file in notepad, copy hello content, paste it into hello **Identity Provider Metadata** textbox, and then click **Save**.</span></span>
   
    ![Azure AD çoklu oturum açma][13]

12. <span data-ttu-id="2e1a8-180">Merhaba değerlerini hello doğrulayın **varlık taban URL** ve **varlık kimliği URL** doğru olduğundan.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-180">Verify that hello values for hello **Entity Base URL** and **Entity ID URL** are correct.</span></span>
    
     ![Azure AD çoklu oturum açma][14]

> [!TIP]
> <span data-ttu-id="2e1a8-182">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="2e1a8-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2e1a8-183">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2e1a8-184">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2e1a8-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2e1a8-185">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2e1a8-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="2e1a8-186">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="2e1a8-188">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2e1a8-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e1a8-189">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2e1a8-191">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2e1a8-193">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2e1a8-195">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2e1a8-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2e1a8-197">a.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-197">a.</span></span> <span data-ttu-id="2e1a8-198">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2e1a8-199">b.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-199">b.</span></span> <span data-ttu-id="2e1a8-200">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2e1a8-201">c.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-201">c.</span></span> <span data-ttu-id="2e1a8-202">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2e1a8-203">d.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-203">d.</span></span> <span data-ttu-id="2e1a8-204">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-204">Click **Create**.</span></span>
 
### <a name="creating-a-performancecentre-test-user"></a><span data-ttu-id="2e1a8-205">PerformanceCentre test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2e1a8-205">Creating a PerformanceCentre test user</span></span>

<span data-ttu-id="2e1a8-206">Bu bölümde Hello amacı toocreate Britta Simon içinde PerformanceCentre adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-206">hello objective of this section is toocreate a user called Britta Simon in PerformanceCentre.</span></span>

<span data-ttu-id="2e1a8-207">**toocreate PerformanceCentre içinde Britta Simon adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2e1a8-207">**toocreate a user called Britta Simon in PerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e1a8-208">Üzerinde tooyour PerformanceCentre şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-208">Sign on tooyour PerformanceCentre company site as administrator.</span></span>

2. <span data-ttu-id="2e1a8-209">Merhaba soldaki Hello menüde tıklatın **Interrelate**ve ardından **oluşturma katılımcı**.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-209">In hello menu on hello left, click **Interrelate**, and then click **Create Participant**.</span></span>
   
    ![Kullanıcı oluştur][400]

3. <span data-ttu-id="2e1a8-211">Merhaba üzerinde **arasında bir ilişki vardır - katılımcı oluşturma** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2e1a8-211">On hello **Interrelate - Create Participant** dialog, perform hello following steps:</span></span>
   
    ![Kullanıcı oluştur][401]
    
    <span data-ttu-id="2e1a8-213">a.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-213">a.</span></span> <span data-ttu-id="2e1a8-214">Merhaba gerekli öznitelikler için Britta Simon ilgili metin kutularına yazın.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-214">Type hello required attributes for Britta Simon into related textboxes.</span></span>
    
    >[!IMPORTANT]
    ><span data-ttu-id="2e1a8-215">Britta'nın kullanıcı PerformanceCentre özniteliği olmalıdır adı hello Azure AD'de kullanıcı adı hello aynı.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-215">Britta's User Name attribute in PerformanceCentre must be hello same as hello User Name in Azure AD.</span></span>
    
    <span data-ttu-id="2e1a8-216">b.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-216">b.</span></span> <span data-ttu-id="2e1a8-217">Seçin **İstemci Yöneticisi** olarak **rolünü seçin**.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-217">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="2e1a8-218">c.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-218">c.</span></span> <span data-ttu-id="2e1a8-219">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-219">Click **Save**.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2e1a8-220">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="2e1a8-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2e1a8-221">Bu bölümde, erişim tooPerformanceCentre vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPerformanceCentre.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="2e1a8-223">**tooassign Britta Simon tooPerformanceCentre hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2e1a8-223">**tooassign Britta Simon tooPerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e1a8-224">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="2e1a8-226">Merhaba uygulamalar listesinde **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-226">In hello applications list, select **PerformanceCentre**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_app.png) 

3. <span data-ttu-id="2e1a8-228">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="2e1a8-230">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-230">Click **Add** button.</span></span> <span data-ttu-id="2e1a8-231">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="2e1a8-233">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2e1a8-234">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2e1a8-235">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2e1a8-236">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="2e1a8-236">Testing single sign-on</span></span>

<span data-ttu-id="2e1a8-237">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="2e1a8-238">Merhaba PerformanceCentre hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour PerformanceCentre uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e1a8-238">When you click hello PerformanceCentre tile in hello Access Panel, you should get automatically signed-on tooyour PerformanceCentre application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2e1a8-239">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2e1a8-239">Additional resources</span></span>

* [<span data-ttu-id="2e1a8-240">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="2e1a8-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2e1a8-241">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="2e1a8-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png

[100]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png

