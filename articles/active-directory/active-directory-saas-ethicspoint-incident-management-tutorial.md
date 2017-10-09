---
title: "Öğretici: Azure Active Directory Tümleştirme EthicsPoint Olay yönetimi (EPIM) | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve EthicsPoint Olay yönetimi (EPIM) arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8cb31a4c-9309-469b-93ac-daf0d3c7a3e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 73ef5fab815cddb3728f4b23173f99e62aec5bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ethicspoint-incident-management-epim"></a><span data-ttu-id="4ad9a-103">Öğretici: Azure Active Directory Tümleştirme EthicsPoint Olay yönetimi (EPIM)</span><span class="sxs-lookup"><span data-stu-id="4ad9a-103">Tutorial: Azure Active Directory integration with EthicsPoint Incident Management (EPIM)</span></span>

<span data-ttu-id="4ad9a-104">Bu öğreticide, bilgi nasıl toointegrate Azure Active Directory (Azure AD) ile EthicsPoint Olay yönetimi (EPIM).</span><span class="sxs-lookup"><span data-stu-id="4ad9a-104">In this tutorial, you learn how toointegrate EthicsPoint Incident Management (EPIM) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4ad9a-105">EthicsPoint Olay yönetimi (EPIM) Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="4ad9a-105">Integrating EthicsPoint Incident Management (EPIM) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4ad9a-106">Erişim tooEthicsPoint Olay yönetimi (EPIM) sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4ad9a-106">You can control in Azure AD who has access tooEthicsPoint Incident Management (EPIM)</span></span>
- <span data-ttu-id="4ad9a-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooEthicsPoint (çoklu oturum açma) Olay yönetimi (EPIM) etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4ad9a-107">You can enable your users tooautomatically get signed-on tooEthicsPoint Incident Management (EPIM) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4ad9a-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="4ad9a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4ad9a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4ad9a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ad9a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4ad9a-110">Prerequisites</span></span>

<span data-ttu-id="4ad9a-111">Azure AD tümleştirme EthicsPoint Olay yönetimi (EPIM) ile tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="4ad9a-111">tooconfigure Azure AD integration with EthicsPoint Incident Management (EPIM), you need hello following items:</span></span>

- <span data-ttu-id="4ad9a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="4ad9a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4ad9a-113">Bir EthicsPoint Olay yönetimi (EPIM) çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="4ad9a-113">A EthicsPoint Incident Management (EPIM) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4ad9a-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4ad9a-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="4ad9a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4ad9a-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4ad9a-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4ad9a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4ad9a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="4ad9a-118">Scenario description</span></span>
<span data-ttu-id="4ad9a-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4ad9a-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="4ad9a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4ad9a-121">Merhaba Galerisi'nden EthicsPoint Olay yönetimi (EPIM) ekleme</span><span class="sxs-lookup"><span data-stu-id="4ad9a-121">Adding EthicsPoint Incident Management (EPIM) from hello gallery</span></span>
2. <span data-ttu-id="4ad9a-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4ad9a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ethicspoint-incident-management-epim-from-hello-gallery"></a><span data-ttu-id="4ad9a-123">Merhaba Galerisi'nden EthicsPoint Olay yönetimi (EPIM) ekleme</span><span class="sxs-lookup"><span data-stu-id="4ad9a-123">Adding EthicsPoint Incident Management (EPIM) from hello gallery</span></span>
<span data-ttu-id="4ad9a-124">tooconfigure hello tümleştirmeye EthicsPoint Olay yönetimi (EPIM) Azure AD, tooadd EthicsPoint Olay yönetimi (EPIM) hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-124">tooconfigure hello integration of EthicsPoint Incident Management (EPIM) into Azure AD, you need tooadd EthicsPoint Incident Management (EPIM) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4ad9a-125">**tooadd hello galerisinden EthicsPoint Olay yönetimi (EPIM) hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4ad9a-125">**tooadd EthicsPoint Incident Management (EPIM) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ad9a-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4ad9a-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4ad9a-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="4ad9a-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="4ad9a-133">Merhaba arama kutusuna yazın **EthicsPoint Olay yönetimi (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-133">In hello search box, type **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_search.png)

5. <span data-ttu-id="4ad9a-135">Merhaba Sonuçlar panelinde seçin **EthicsPoint Olay yönetimi (EPIM)**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-135">In hello results panel, select **EthicsPoint Incident Management (EPIM)**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4ad9a-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4ad9a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4ad9a-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile EthicsPoint Olay yönetimi ("Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı EPIM) test etme</span><span class="sxs-lookup"><span data-stu-id="4ad9a-138">In this section, you configure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM) based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4ad9a-139">Tek toowork'ın oturum açma hangi hello karşılık gelen EthicsPoint Olay yönetimi (EPIM) tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EthicsPoint Incident Management (EPIM) is tooa user in Azure AD.</span></span> <span data-ttu-id="4ad9a-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı EthicsPoint Olay yönetimi (EPIM) arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-140">In other words, a link relationship between an Azure AD user and hello related user in EthicsPoint Incident Management (EPIM) needs toobe established.</span></span>

<span data-ttu-id="4ad9a-141">Merhaba hello değeri EthicsPoint Olay yönetimi (EPIM) atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-141">In EthicsPoint Incident Management (EPIM), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4ad9a-142">tooconfigure ve test EthicsPoint Olay yönetimi (EPIM) ile Azure AD çoklu oturum açma, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="4ad9a-142">tooconfigure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4ad9a-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4ad9a-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4ad9a-145">**[EthicsPoint Olay yönetimi (EPIM) test kullanıcısı oluşturma](#creating-a-ethicspoint-incident-management-epim-test-user)**  -toohave karşılık gelen, Britta Simon EthicsPoint Olay yönetimi (EPIM) bağlantılı toohello Azure AD kullanıcı gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-145">**[Creating a EthicsPoint Incident Management (EPIM) test user](#creating-a-ethicspoint-incident-management-epim-test-user)** - toohave a counterpart of Britta Simon in EthicsPoint Incident Management (EPIM) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4ad9a-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4ad9a-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4ad9a-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4ad9a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4ad9a-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma EthicsPoint Olay yönetimi (EPIM) uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EthicsPoint Incident Management (EPIM) application.</span></span>

<span data-ttu-id="4ad9a-150">**tooconfigure EthicsPoint Olay yönetimi (EPIM) ile Azure AD çoklu oturum açma hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4ad9a-150">**tooconfigure Azure AD single sign-on with EthicsPoint Incident Management (EPIM), perform hello following steps:**</span></span>

1. <span data-ttu-id="4ad9a-151">Hello hello üzerinde Azure portal'ın **EthicsPoint Olay yönetimi (EPIM)** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-151">In hello Azure portal, on hello **EthicsPoint Incident Management (EPIM)** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="4ad9a-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_samlbase.png)

3. <span data-ttu-id="4ad9a-155">Merhaba üzerinde **EthicsPoint Olay yönetimi (EPIM) etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4ad9a-155">On hello **EthicsPoint Incident Management (EPIM) Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_url.png)

    <span data-ttu-id="4ad9a-157">a.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-157">a.</span></span> <span data-ttu-id="4ad9a-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="4ad9a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.navexglobal.com`|
    | `https://<companyname>.ethicspointvp.com`|

    <span data-ttu-id="4ad9a-159">b.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-159">b.</span></span> <span data-ttu-id="4ad9a-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.navexglobal.com/adfs/services/trust`</span><span class="sxs-lookup"><span data-stu-id="4ad9a-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.navexglobal.com/adfs/services/trust`</span></span>

    <span data-ttu-id="4ad9a-161">c.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-161">c.</span></span> <span data-ttu-id="4ad9a-162">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<servername>.navexglobal.com/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="4ad9a-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<servername>.navexglobal.com/adfs/ls/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4ad9a-163">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-163">These values are not real.</span></span> <span data-ttu-id="4ad9a-164">Bu değerleri hello gerçek yanıt URL'si, tanımlayıcı ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-164">Update these values with hello actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="4ad9a-165">Kişi [EthicsPoint Olay yönetimi (EPIM) istemci destek ekibi](http://www.navexglobal.com/company/contact-us) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-165">Contact [EthicsPoint Incident Management (EPIM) Client support team](http://www.navexglobal.com/company/contact-us) tooget these values.</span></span> 

4. <span data-ttu-id="4ad9a-166">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_certificate.png) 

5. <span data-ttu-id="4ad9a-168">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-168">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="4ad9a-170">tooconfigure çoklu oturum açma üzerinde **EthicsPoint Olay yönetimi (EPIM)** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[EthicsPoint Olay yönetimi (EPIM) desteği Takım](http://www.navexglobal.com/company/contact-us).</span><span class="sxs-lookup"><span data-stu-id="4ad9a-170">tooconfigure single sign-on on **EthicsPoint Incident Management (EPIM)** side, you need toosend hello downloaded **Metadata XML** too[EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="4ad9a-171">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="4ad9a-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4ad9a-172">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4ad9a-173">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4ad9a-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4ad9a-174">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4ad9a-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="4ad9a-175">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="4ad9a-177">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4ad9a-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ad9a-178">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4ad9a-180">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4ad9a-182">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4ad9a-184">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4ad9a-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4ad9a-186">a.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-186">a.</span></span> <span data-ttu-id="4ad9a-187">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4ad9a-188">b.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-188">b.</span></span> <span data-ttu-id="4ad9a-189">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4ad9a-190">c.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-190">c.</span></span> <span data-ttu-id="4ad9a-191">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4ad9a-192">d.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-192">d.</span></span> <span data-ttu-id="4ad9a-193">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-193">Click **Create**.</span></span>
 
### <a name="creating-a-ethicspoint-incident-management-epim-test-user"></a><span data-ttu-id="4ad9a-194">EthicsPoint Olay yönetimi (EPIM) test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4ad9a-194">Creating a EthicsPoint Incident Management (EPIM) test user</span></span>

<span data-ttu-id="4ad9a-195">Bu bölümde, Britta Simon EthicsPoint Olay yönetimi (EPIM) adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-195">In this section, you create a user called Britta Simon in EthicsPoint Incident Management (EPIM).</span></span> <span data-ttu-id="4ad9a-196">Lütfen çalışmak [EthicsPoint Olay yönetimi (EPIM) destek ekibi](http://www.navexglobal.com/company/contact-us) tooadd hello kullanıcılar hello EthicsPoint Olay yönetimi (EPIM) Platform.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-196">Please work with [EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us) tooadd hello users in hello EthicsPoint Incident Management (EPIM) platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4ad9a-197">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="4ad9a-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4ad9a-198">Bu bölümde, erişim tooEthicsPoint Olay yönetimi (EPIM) vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEthicsPoint Incident Management (EPIM).</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="4ad9a-200">**tooassign Britta Simon tooEthicsPoint Olay yönetimi (EPIM), hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4ad9a-200">**tooassign Britta Simon tooEthicsPoint Incident Management (EPIM), perform hello following steps:**</span></span>

1. <span data-ttu-id="4ad9a-201">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="4ad9a-203">Merhaba uygulamalar listesinde **EthicsPoint Olay yönetimi (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-203">In hello applications list, select **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_app.png) 

3. <span data-ttu-id="4ad9a-205">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="4ad9a-207">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-207">Click **Add** button.</span></span> <span data-ttu-id="4ad9a-208">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="4ad9a-210">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4ad9a-211">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4ad9a-212">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4ad9a-213">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="4ad9a-213">Testing single sign-on</span></span>

<span data-ttu-id="4ad9a-214">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="4ad9a-215">Merhaba EthicsPoint Olay yönetimi (EPIM) hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour EthicsPoint Olay yönetimi (EPIM) uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4ad9a-215">When you click hello EthicsPoint Incident Management (EPIM) tile in hello Access Panel, you should get automatically signed-on tooyour EthicsPoint Incident Management (EPIM) application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4ad9a-216">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4ad9a-216">Additional resources</span></span>

* [<span data-ttu-id="4ad9a-217">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="4ad9a-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4ad9a-218">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="4ad9a-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_203.png

