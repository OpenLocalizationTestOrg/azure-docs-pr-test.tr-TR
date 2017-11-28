---
title: "Öğretici: Azure Active Directory Tümleştirme Icertis sözleşme yönetim platformuyla | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Icertis sözleşme yönetim platformu arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6627e6dd-f559-4cd4-a509-f6d9a4961b49
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 6eb99553ef9df732512a38fb0489e66b41ba94a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icertis-contract-management-platform"></a><span data-ttu-id="ebc73-103">Öğretici: Azure Active Directory Tümleştirme Icertis sözleşme yönetim platformu ile</span><span class="sxs-lookup"><span data-stu-id="ebc73-103">Tutorial: Azure Active Directory integration with Icertis Contract Management Platform</span></span>

<span data-ttu-id="ebc73-104">Bu öğreticide, bilgi nasıl toointegrate Icertis sözleşme yönetim platformu Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ebc73-104">In this tutorial, you learn how toointegrate Icertis Contract Management Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ebc73-105">Icertis sözleşme yönetim platformu Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="ebc73-105">Integrating Icertis Contract Management Platform with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ebc73-106">Erişim tooIcertis sözleşme yönetim platformu olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ebc73-106">You can control in Azure AD who has access tooIcertis Contract Management Platform</span></span>
- <span data-ttu-id="ebc73-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooIcertis sözleşme yönetim platformunu (çoklu oturum açma) etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ebc73-107">You can enable your users tooautomatically get signed-on tooIcertis Contract Management Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ebc73-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="ebc73-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ebc73-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ebc73-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebc73-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ebc73-110">Prerequisites</span></span>

<span data-ttu-id="ebc73-111">tooconfigure Icertis sözleşme yönetim platformu ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="ebc73-111">tooconfigure Azure AD integration with Icertis Contract Management Platform, you need hello following items:</span></span>

- <span data-ttu-id="ebc73-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="ebc73-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ebc73-113">Bir Icertis sözleşme yönetim platformu çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="ebc73-113">An Icertis Contract Management Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ebc73-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="ebc73-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ebc73-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="ebc73-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ebc73-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="ebc73-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ebc73-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ebc73-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ebc73-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="ebc73-118">Scenario description</span></span>
<span data-ttu-id="ebc73-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="ebc73-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ebc73-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="ebc73-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ebc73-121">Merhaba Galerisi'nden Icertis sözleşme yönetim platformu ekleme</span><span class="sxs-lookup"><span data-stu-id="ebc73-121">Adding Icertis Contract Management Platform from hello gallery</span></span>
2. <span data-ttu-id="ebc73-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ebc73-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icertis-contract-management-platform-from-hello-gallery"></a><span data-ttu-id="ebc73-123">Merhaba Galerisi'nden Icertis sözleşme yönetim platformu ekleme</span><span class="sxs-lookup"><span data-stu-id="ebc73-123">Adding Icertis Contract Management Platform from hello gallery</span></span>
<span data-ttu-id="ebc73-124">Azure AD'ye tooconfigure hello tümleştirme Icertis sözleşme yönetim platformunun tooadd Icertis sözleşme yönetim platformu hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="ebc73-124">tooconfigure hello integration of Icertis Contract Management Platform into Azure AD, you need tooadd Icertis Contract Management Platform from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ebc73-125">**tooadd Icertis sözleşme yönetim platformu hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ebc73-125">**tooadd Icertis Contract Management Platform from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebc73-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ebc73-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ebc73-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="ebc73-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ebc73-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ebc73-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="ebc73-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ebc73-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="ebc73-133">Merhaba arama kutusuna yazın **Icertis sözleşme yönetim platformu**.</span><span class="sxs-lookup"><span data-stu-id="ebc73-133">In hello search box, type **Icertis Contract Management Platform**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_search.png)

5. <span data-ttu-id="ebc73-135">Merhaba Sonuçlar panelinde seçin **Icertis sözleşme yönetim platformu**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="ebc73-135">In hello results panel, select **Icertis Contract Management Platform**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ebc73-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ebc73-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ebc73-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Icertis sözleşme yönetim platformuyla test etme.</span><span class="sxs-lookup"><span data-stu-id="ebc73-138">In this section, you configure and test Azure AD single sign-on with Icertis Contract Management Platform based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ebc73-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Icertis sözleşme Yönetimi Platform tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="ebc73-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Icertis Contract Management Platform is tooa user in Azure AD.</span></span> <span data-ttu-id="ebc73-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Icertis sözleşme Yönetimi Platform arasında bağlantı ilişki kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="ebc73-140">In other words, a link relationship between an Azure AD user and hello related user in Icertis Contract Management Platform needs toobe established.</span></span>

<span data-ttu-id="ebc73-141">Merhaba hello değeri Icertis sözleşme Yönetimi platformunda atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="ebc73-141">In Icertis Contract Management Platform, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ebc73-142">tooconfigure ve Icertis sözleşme yönetim platformu ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="ebc73-142">tooconfigure and test Azure AD single sign-on with Icertis Contract Management Platform, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ebc73-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="ebc73-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ebc73-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="ebc73-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ebc73-145">**[Bir Icertis sözleşme yönetim platformu test kullanıcısı oluşturma](#creating-an-icertis-contract-management-platform-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Icertis sözleşme Yönetimi Platform, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="ebc73-145">**[Creating an Icertis Contract Management Platform test user](#creating-an-icertis-contract-management-platform-test-user)** - toohave a counterpart of Britta Simon in Icertis Contract Management Platform that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ebc73-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="ebc73-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ebc73-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="ebc73-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ebc73-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ebc73-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ebc73-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Icertis sözleşme yönetim platformu uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ebc73-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Icertis Contract Management Platform application.</span></span>

<span data-ttu-id="ebc73-150">**Azure AD çoklu oturum açma tooconfigure Icertis sözleşme yönetim platformuyla hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ebc73-150">**tooconfigure Azure AD single sign-on with Icertis Contract Management Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebc73-151">Merhaba hello üzerinde Azure portal'ın **Icertis sözleşme yönetim platformu** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="ebc73-151">In hello Azure portal, on hello **Icertis Contract Management Platform** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="ebc73-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="ebc73-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_samlbase.png)

3. <span data-ttu-id="ebc73-155">Merhaba üzerinde **Icertis sözleşme yönetim platformu etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ebc73-155">On hello **Icertis Contract Management Platform Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_url.png)

    <span data-ttu-id="ebc73-157">a.</span><span class="sxs-lookup"><span data-stu-id="ebc73-157">a.</span></span> <span data-ttu-id="ebc73-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.icertis.com`</span><span class="sxs-lookup"><span data-stu-id="ebc73-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.icertis.com`</span></span>

    <span data-ttu-id="ebc73-159">b.</span><span class="sxs-lookup"><span data-stu-id="ebc73-159">b.</span></span> <span data-ttu-id="ebc73-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.icertis.com`</span><span class="sxs-lookup"><span data-stu-id="ebc73-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.icertis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ebc73-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="ebc73-161">These values are not real.</span></span> <span data-ttu-id="ebc73-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="ebc73-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ebc73-163">Kişi [Icertis sözleşme yönetim platformu istemci destek ekibi](https://www.icertis.com/company/contact/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="ebc73-163">Contact [Icertis Contract Management Platform Client support team](https://www.icertis.com/company/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="ebc73-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ebc73-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_certificate.png) 

5. <span data-ttu-id="ebc73-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ebc73-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-icertisicm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ebc73-168">Merhaba üzerinde **Icertis sözleşme yönetim platformu yapılandırma** 'yi tıklatın **Icertis sözleşme yönetim platformu yapılandırma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="ebc73-168">On hello **Icertis Contract Management Platform Configuration** section, click **Configure Icertis Contract Management Platform** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ebc73-169">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="ebc73-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_configure.png) 

7. <span data-ttu-id="ebc73-171">tooconfigure çoklu oturum açma üzerinde **Icertis sözleşme yönetim platformu** yan, indirilen toosend hello ihtiyacınız **meta veri XML** ve **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma Hizmet URL'si** çok[Icertis sözleşme yönetim platformu destek ekibi](https://www.icertis.com/company/contact/).</span><span class="sxs-lookup"><span data-stu-id="ebc73-171">tooconfigure single sign-on on **Icertis Contract Management Platform** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="ebc73-172">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="ebc73-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ebc73-173">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="ebc73-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ebc73-174">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ebc73-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ebc73-175">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ebc73-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="ebc73-176">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="ebc73-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="ebc73-178">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ebc73-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebc73-179">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ebc73-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ebc73-181">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="ebc73-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ebc73-183">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="ebc73-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ebc73-185">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ebc73-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ebc73-187">a.</span><span class="sxs-lookup"><span data-stu-id="ebc73-187">a.</span></span> <span data-ttu-id="ebc73-188">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ebc73-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ebc73-189">b.</span><span class="sxs-lookup"><span data-stu-id="ebc73-189">b.</span></span> <span data-ttu-id="ebc73-190">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="ebc73-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ebc73-191">c.</span><span class="sxs-lookup"><span data-stu-id="ebc73-191">c.</span></span> <span data-ttu-id="ebc73-192">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="ebc73-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ebc73-193">d.</span><span class="sxs-lookup"><span data-stu-id="ebc73-193">d.</span></span> <span data-ttu-id="ebc73-194">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ebc73-194">Click **Create**.</span></span>
 
### <a name="creating-an-icertis-contract-management-platform-test-user"></a><span data-ttu-id="ebc73-195">Bir Icertis sözleşme yönetim platformu test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ebc73-195">Creating an Icertis Contract Management Platform test user</span></span>

<span data-ttu-id="ebc73-196">Bu bölümde, Britta Simon Icertis sözleşme Yönetimi platformunda adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ebc73-196">In this section, you create a user called Britta Simon in Icertis Contract Management Platform.</span></span> <span data-ttu-id="ebc73-197">Lütfen çalışmak [Icertis sözleşme yönetim platformu destek ekibi](https://www.icertis.com/company/contact/) tooadd hello kullanıcılar hello Icertis sözleşme yönetim platformudur.</span><span class="sxs-lookup"><span data-stu-id="ebc73-197">Please work with [Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/) tooadd hello users in hello Icertis Contract Management Platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ebc73-198">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="ebc73-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ebc73-199">Bu bölümde, erişim tooIcertis sözleşme yönetim platformu vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ebc73-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIcertis Contract Management Platform.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="ebc73-201">**tooassign Britta Simon tooIcertis sözleşme yönetim platformu, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ebc73-201">**tooassign Britta Simon tooIcertis Contract Management Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebc73-202">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ebc73-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="ebc73-204">Merhaba uygulamalar listesinde **Icertis sözleşme yönetim platformu**.</span><span class="sxs-lookup"><span data-stu-id="ebc73-204">In hello applications list, select **Icertis Contract Management Platform**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_app.png) 

3. <span data-ttu-id="ebc73-206">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="ebc73-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="ebc73-208">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ebc73-208">Click **Add** button.</span></span> <span data-ttu-id="ebc73-209">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ebc73-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="ebc73-211">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="ebc73-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ebc73-212">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ebc73-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ebc73-213">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ebc73-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ebc73-214">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="ebc73-214">Testing single sign-on</span></span>

<span data-ttu-id="ebc73-215">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ebc73-215">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="ebc73-216">Merhaba Icertis sözleşme yönetim platformu hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma Icertis sözleşme yönetim platformu uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ebc73-216">When you click hello Icertis Contract Management Platform tile in hello Access Panel, you should get automatically signed-on tooyour Icertis Contract Management Platform application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ebc73-217">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ebc73-217">Additional resources</span></span>

* [<span data-ttu-id="ebc73-218">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="ebc73-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ebc73-219">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="ebc73-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_203.png

