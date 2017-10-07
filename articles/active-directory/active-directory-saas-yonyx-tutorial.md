---
title: "Öğretici: Azure Active Directory Tümleştirme Yonyx etkileşimli Kılavuzlar ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Yonyx etkileşimli kılavuzları arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 07db4e01-319b-4cb6-9b93-4577bffd3cbc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: 24e30d243143651b8d32535c76dc300931ae5746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-yonyx-interactive-guides"></a><span data-ttu-id="73c5e-103">Öğretici: Azure Active Directory Tümleştirme ile Yonyx etkileşimli kılavuzları</span><span class="sxs-lookup"><span data-stu-id="73c5e-103">Tutorial: Azure Active Directory integration with Yonyx Interactive Guides</span></span>

<span data-ttu-id="73c5e-104">Bu öğreticide, bilgi nasıl toointegrate Yonyx etkileşimli Azure Active Directory (Azure AD) ile size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="73c5e-104">In this tutorial, you learn how toointegrate Yonyx Interactive Guides with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="73c5e-105">Yonyx etkileşimli kılavuzları Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="73c5e-105">Integrating Yonyx Interactive Guides with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="73c5e-106">Erişim tooYonyx etkileşimli kılavuzları sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="73c5e-106">You can control in Azure AD who has access tooYonyx Interactive Guides</span></span>
- <span data-ttu-id="73c5e-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooYonyx etkileşimli kılavuzları (çoklu oturum açma) etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="73c5e-107">You can enable your users tooautomatically get signed-on tooYonyx Interactive Guides (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="73c5e-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="73c5e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="73c5e-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="73c5e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73c5e-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="73c5e-110">Prerequisites</span></span>

<span data-ttu-id="73c5e-111">tooconfigure Yonyx etkileşimli kılavuzları ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="73c5e-111">tooconfigure Azure AD integration with Yonyx Interactive Guides, you need hello following items:</span></span>

- <span data-ttu-id="73c5e-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="73c5e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="73c5e-113">Bir Yonyx etkileşimli kılavuzları çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="73c5e-113">A Yonyx Interactive Guides single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="73c5e-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="73c5e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="73c5e-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="73c5e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="73c5e-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="73c5e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="73c5e-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="73c5e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="73c5e-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="73c5e-118">Scenario description</span></span>
<span data-ttu-id="73c5e-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="73c5e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="73c5e-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="73c5e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="73c5e-121">Merhaba Galerisi'nden Yonyx etkileşimli kılavuzları ekleme</span><span class="sxs-lookup"><span data-stu-id="73c5e-121">Adding Yonyx Interactive Guides from hello gallery</span></span>
2. <span data-ttu-id="73c5e-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="73c5e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yonyx-interactive-guides-from-hello-gallery"></a><span data-ttu-id="73c5e-123">Merhaba Galerisi'nden Yonyx etkileşimli kılavuzları ekleme</span><span class="sxs-lookup"><span data-stu-id="73c5e-123">Adding Yonyx Interactive Guides from hello gallery</span></span>
<span data-ttu-id="73c5e-124">Azure AD'ye tooconfigure hello tümleştirme Yonyx etkileşimli kılavuzlarının tooadd Yonyx etkileşimli kılavuzları hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="73c5e-124">tooconfigure hello integration of Yonyx Interactive Guides into Azure AD, you need tooadd Yonyx Interactive Guides from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="73c5e-125">**tooadd Yonyx etkileşimli kılavuzları hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="73c5e-125">**tooadd Yonyx Interactive Guides from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="73c5e-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="73c5e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="73c5e-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="73c5e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="73c5e-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="73c5e-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="73c5e-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="73c5e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="73c5e-133">Merhaba arama kutusuna yazın **Yonyx etkileşimli kılavuzları**seçin **Yonyx etkileşimli kılavuzları** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="73c5e-133">In hello search box, type **Yonyx Interactive Guides**, select  **Yonyx Interactive Guides**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde Yonyx etkileşimli kılavuzları](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="73c5e-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="73c5e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="73c5e-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Yonyx etkileşimli "Britta Simon" adlı bir test kullanıcı tabanlı Kılavuzlar ile test etme.</span><span class="sxs-lookup"><span data-stu-id="73c5e-136">In this section, you configure and test Azure AD single sign-on with Yonyx Interactive Guides based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="73c5e-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Yonyx etkileşimli kılavuzlarındaki tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="73c5e-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Yonyx Interactive Guides is tooa user in Azure AD.</span></span> <span data-ttu-id="73c5e-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Yonyx etkileşimli kılavuzlarındaki arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="73c5e-138">In other words, a link relationship between an Azure AD user and hello related user in Yonyx Interactive Guides needs toobe established.</span></span>

<span data-ttu-id="73c5e-139">Merhaba hello değeri Yonyx etkileşimli kılavuzlarında atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="73c5e-139">In Yonyx Interactive Guides, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="73c5e-140">tooconfigure ve Yonyx etkileşimli Kılavuzlar ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="73c5e-140">tooconfigure and test Azure AD single sign-on with Yonyx Interactive Guides, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="73c5e-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="73c5e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="73c5e-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="73c5e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="73c5e-143">**[Yonyx etkileşimli kılavuzları test kullanıcısı oluşturma](#create-a-yonyx-interactive-guides-test-user)**  -toohave Britta Simon kılavuzlarındaki Yonyx etkileşimli kullanıcı bağlantılı toohello Azure AD gösterimi olan, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="73c5e-143">**[Create a Yonyx Interactive Guides test user](#create-a-yonyx-interactive-guides-test-user)** - toohave a counterpart of Britta Simon in Yonyx Interactive Guides that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="73c5e-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="73c5e-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="73c5e-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="73c5e-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="73c5e-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="73c5e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="73c5e-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Yonyx etkileşimli kılavuzları uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="73c5e-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="73c5e-148">**Azure AD çoklu oturum açma tooconfigure Yonyx etkileşimli kılavuzla hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="73c5e-148">**tooconfigure Azure AD single sign-on with Yonyx Interactive Guides, perform hello following steps:**</span></span>

1. <span data-ttu-id="73c5e-149">Merhaba hello üzerinde Azure portal'ın **Yonyx etkileşimli kılavuzları** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="73c5e-149">In hello Azure portal, on hello **Yonyx Interactive Guides** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="73c5e-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="73c5e-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_samlbase.png)

3. <span data-ttu-id="73c5e-153">Merhaba üzerinde **Yonyx etkileşimli kılavuzları etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="73c5e-153">On hello **Yonyx Interactive Guides Domain and URLs** section, perform hello following steps:</span></span>

    ![Yonyx etkileşimli kılavuzları etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_url.png)

    <span data-ttu-id="73c5e-155">a.</span><span class="sxs-lookup"><span data-stu-id="73c5e-155">a.</span></span> <span data-ttu-id="73c5e-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span><span class="sxs-lookup"><span data-stu-id="73c5e-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span></span>

    <span data-ttu-id="73c5e-157">b.</span><span class="sxs-lookup"><span data-stu-id="73c5e-157">b.</span></span> <span data-ttu-id="73c5e-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.yonyx.com`</span><span class="sxs-lookup"><span data-stu-id="73c5e-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.yonyx.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="73c5e-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="73c5e-159">These values are not real.</span></span> <span data-ttu-id="73c5e-160">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="73c5e-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="73c5e-161">Kişi [Yonyx etkileşimli kılavuzları istemci destek ekibi](mailto:support@yonyx.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="73c5e-161">Contact [Yonyx Interactive Guides Client support team](mailto:support@yonyx.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="73c5e-162">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="73c5e-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_certificate.png) 

5. <span data-ttu-id="73c5e-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="73c5e-164">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-yonyx-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="73c5e-166">Merhaba üzerinde **Yonyx etkileşimli kılavuzları yapılandırma** 'yi tıklatın **Yonyx etkileşimli kılavuzları yapılandırma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="73c5e-166">On hello **Yonyx Interactive Guides Configuration** section, click **Configure Yonyx Interactive Guides** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="73c5e-167">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="73c5e-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Yonyx etkileşimli kılavuzları yapılandırma](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_configure.png) 

7. <span data-ttu-id="73c5e-169">tooconfigure çoklu oturum açma üzerinde **Yonyx etkileşimli kılavuzları** yan, indirilen toosend hello ihtiyacınız **Certificate(Base64)**, **Sign-Out URL**, **SAML Çoklu oturum açma hizmet URL'si** **SAML varlık kimliği** çok[Yonyx etkileşimli kılavuzları destek ekibi](mailto:support@yonyx.com).</span><span class="sxs-lookup"><span data-stu-id="73c5e-169">tooconfigure single sign-on on **Yonyx Interactive Guides** side, you need toosend hello downloaded **Certificate(Base64)**, **Sign-Out URL**, **SAML Single Sign-On Service URL** **SAML Entity ID** too[Yonyx Interactive Guides support team](mailto:support@yonyx.com).</span></span> <span data-ttu-id="73c5e-170">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="73c5e-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="73c5e-171">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="73c5e-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="73c5e-172">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="73c5e-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="73c5e-173">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="73c5e-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="73c5e-174">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="73c5e-174">Create an Azure AD test user</span></span>

<span data-ttu-id="73c5e-175">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="73c5e-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

  ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="73c5e-177">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="73c5e-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="73c5e-178">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="73c5e-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-yonyx-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="73c5e-180">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="73c5e-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-yonyx-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="73c5e-182">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="73c5e-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-yonyx-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="73c5e-184">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="73c5e-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-yonyx-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="73c5e-186">a.</span><span class="sxs-lookup"><span data-stu-id="73c5e-186">a.</span></span> <span data-ttu-id="73c5e-187">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="73c5e-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="73c5e-188">b.</span><span class="sxs-lookup"><span data-stu-id="73c5e-188">b.</span></span> <span data-ttu-id="73c5e-189">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="73c5e-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="73c5e-190">c.</span><span class="sxs-lookup"><span data-stu-id="73c5e-190">c.</span></span> <span data-ttu-id="73c5e-191">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="73c5e-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="73c5e-192">d.</span><span class="sxs-lookup"><span data-stu-id="73c5e-192">d.</span></span> <span data-ttu-id="73c5e-193">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="73c5e-193">Click **Create**.</span></span>
 
### <a name="create-a-yonyx-interactive-guides-test-user"></a><span data-ttu-id="73c5e-194">Yonyx etkileşimli kılavuzları test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="73c5e-194">Create a Yonyx Interactive Guides test user</span></span>

<span data-ttu-id="73c5e-195">Bu bölümde Hello amacı toocreate Britta Simon Yonyx etkileşimli Kılavuzlar'adlı kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="73c5e-195">hello objective of this section is toocreate a user called Britta Simon in Yonyx Interactive Guides.</span></span> <span data-ttu-id="73c5e-196">Yonyx etkileşimli kılavuzları tam zamanı sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="73c5e-196">Yonyx Interactive Guides supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="73c5e-197">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="73c5e-197">There is no action item for you in this section.</span></span> <span data-ttu-id="73c5e-198">Henüz yoksa yeni bir kullanıcı bir girişim tooaccess Yonyx etkileşimli kılavuzları sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="73c5e-198">A new user is created during an attempt tooaccess Yonyx Interactive Guides if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="73c5e-199">Toocreate kullanıcı el ile gerekiyorsa, Yonyx etkileşimli kılavuzları destek ekibi ile toocontact hello gereksinim < mailto:support@yonyx.com >.</span><span class="sxs-lookup"><span data-stu-id="73c5e-199">If you need toocreate a user manually, you need toocontact hello Yonyx Interactive Guides support team via <mailto:support@yonyx.com>.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="73c5e-200">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="73c5e-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="73c5e-201">Bu bölümde, erişim tooYonyx etkileşimli kılavuzları vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="73c5e-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooYonyx Interactive Guides.</span></span>

![Merhaba kullanıcı rolü atayın][200]

<span data-ttu-id="73c5e-203">**tooassign Britta Simon tooYonyx etkileşimli kılavuzları, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="73c5e-203">**tooassign Britta Simon tooYonyx Interactive Guides, perform hello following steps:**</span></span>

1. <span data-ttu-id="73c5e-204">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="73c5e-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="73c5e-206">Merhaba uygulamalar listesinde **Yonyx etkileşimli kılavuzları**.</span><span class="sxs-lookup"><span data-stu-id="73c5e-206">In hello applications list, select **Yonyx Interactive Guides**.</span></span>

    ![Merhaba Yonyx etkileşimli kılavuzları bağlantı hello uygulamalar listesinde](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_app.png) 

3. <span data-ttu-id="73c5e-208">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="73c5e-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="73c5e-210">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="73c5e-210">Click **Add** button.</span></span> <span data-ttu-id="73c5e-211">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="73c5e-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="73c5e-213">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="73c5e-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="73c5e-214">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="73c5e-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="73c5e-215">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="73c5e-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="73c5e-216">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="73c5e-216">Test single sign-on</span></span>

<span data-ttu-id="73c5e-217">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="73c5e-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="73c5e-218">Hello erişim paneli Yonyx etkileşimli kılavuzları döşeme hello tıkladığınızda, otomatik olarak oturum açma Yonyx etkileşimli kılavuzları uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="73c5e-218">When you click hello Yonyx Interactive Guides tile in hello Access Panel, you should get automatically signed-on tooyour Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="73c5e-219">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="73c5e-219">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="73c5e-220">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="73c5e-220">Additional resources</span></span>

* [<span data-ttu-id="73c5e-221">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="73c5e-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="73c5e-222">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="73c5e-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_203.png

