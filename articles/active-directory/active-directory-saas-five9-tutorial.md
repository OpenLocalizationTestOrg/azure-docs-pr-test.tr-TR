---
title: "Öğretici: Azure Active Directory Tümleştirme bağdaştırıcısıyla Five9 artı (CTI, kişi Center aracıları) | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: 2e3ea8b5f2a6eaa8ad17d39e03fa490038b14561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a><span data-ttu-id="20625-103">Öğretici: Azure Active Directory Tümleştirme bağdaştırıcısıyla Five9 artı (CTI, kişi Center aracıları)</span><span class="sxs-lookup"><span data-stu-id="20625-103">Tutorial: Azure Active Directory integration with Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>

<span data-ttu-id="20625-104">Bu öğreticide, bilgi nasıl toointegrate Five9 artı bağdaştırıcısı (CTI, kişi Center aracıları) ile Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="20625-104">In this tutorial, you learn how toointegrate Five9 Plus Adapter (CTI, Contact Center Agents) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="20625-105">Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="20625-105">Integrating Five9 Plus Adapter (CTI, Contact Center Agents) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="20625-106">Erişim tooFive9 olan Azure AD artı bağdaştırıcı (CTI, kişi Center aracıları) kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="20625-106">You can control in Azure AD who has access tooFive9 Plus Adapter (CTI, Contact Center Agents)</span></span>
- <span data-ttu-id="20625-107">Oturum açmış kullanıcıların tooautomatically get tooFive9 artı bağdaştırıcı (CTI, kişi Center aracıları) etkinleştirebilirsiniz (çoklu oturum açma) Azure AD hesaplarına sahip</span><span class="sxs-lookup"><span data-stu-id="20625-107">You can enable your users tooautomatically get signed-on tooFive9 Plus Adapter (CTI, Contact Center Agents) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="20625-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="20625-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="20625-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="20625-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20625-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="20625-110">Prerequisites</span></span>

<span data-ttu-id="20625-111">bağdaştırıcısıyla Five9 artı (aşağıdaki öğelerindeki hello ihtiyacınız CTI, kişi Center aracıları), tooconfigure Azure AD tümleştirme:</span><span class="sxs-lookup"><span data-stu-id="20625-111">tooconfigure Azure AD integration with Five9 Plus Adapter (CTI, Contact Center Agents), you need hello following items:</span></span>

- <span data-ttu-id="20625-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="20625-112">An Azure AD subscription</span></span>
- <span data-ttu-id="20625-113">Bir Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="20625-113">A Five9 Plus Adapter (CTI, Contact Center Agents) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="20625-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="20625-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="20625-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="20625-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="20625-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="20625-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="20625-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="20625-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="20625-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="20625-118">Scenario description</span></span>
<span data-ttu-id="20625-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="20625-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="20625-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="20625-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="20625-121">Merhaba Galerisi'nden Five9 artı bağdaştırıcısı (CTI, kişi Center aracıları) ekleme</span><span class="sxs-lookup"><span data-stu-id="20625-121">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery</span></span>
2. <span data-ttu-id="20625-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="20625-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-hello-gallery"></a><span data-ttu-id="20625-123">Merhaba Galerisi'nden Five9 artı bağdaştırıcısı (CTI, kişi Center aracıları) ekleme</span><span class="sxs-lookup"><span data-stu-id="20625-123">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery</span></span>
<span data-ttu-id="20625-124">Azure AD'ye tooconfigure hello tümleştirme Five9 artı bağdaştırıcısının (CTI, kişi Center aracıları) hello galeri tooyour listesinden yönetilen SaaS uygulamaları tooadd Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) gerekir.</span><span class="sxs-lookup"><span data-stu-id="20625-124">tooconfigure hello integration of Five9 Plus Adapter (CTI, Contact Center Agents) into Azure AD, you need tooadd Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="20625-125">**tooadd Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="20625-125">**tooadd Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="20625-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="20625-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="20625-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="20625-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="20625-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="20625-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="20625-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="20625-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="20625-133">Merhaba arama kutusuna yazın **Five9 artı bağdaştırıcı (CTI, kişi Center aracıları)**.</span><span class="sxs-lookup"><span data-stu-id="20625-133">In hello search box, type **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. <span data-ttu-id="20625-135">Merhaba Sonuçlar panelinde seçin **Five9 artı bağdaştırıcı (CTI, kişi Center aracıları)**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="20625-135">In hello results panel, select **Five9 Plus Adapter (CTI, Contact Center Agents)**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="20625-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="20625-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="20625-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Five9 artı "Britta Simon" adlı bir test kullanıcıya bağlı bağdaştırıcı (CTI, kişi Center aracıları) ile test etme.</span><span class="sxs-lookup"><span data-stu-id="20625-138">In this section, you configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="20625-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Five9 artı bağdaştırıcısında (CTI, kişi Center aracıları) tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="20625-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Five9 Plus Adapter (CTI, Contact Center Agents) is tooa user in Azure AD.</span></span> <span data-ttu-id="20625-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Five9 artı bağdaştırıcısında (CTI, kişi Center aracıları) arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="20625-140">In other words, a link relationship between an Azure AD user and hello related user in Five9 Plus Adapter (CTI, Contact Center Agents) needs toobe established.</span></span>

<span data-ttu-id="20625-141">Merhaba hello değeri Five9 artı bağdaştırıcısında (CTI, kişi Center aracıları) atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="20625-141">In Five9 Plus Adapter (CTI, Contact Center Agents), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="20625-142">tooconfigure ve Five9 artı bağdaştırıcı (yapı taşları aşağıdaki toocomplete hello ihtiyacınız CTI, kişi Center aracıları), Azure AD çoklu oturum açma testiyle:</span><span class="sxs-lookup"><span data-stu-id="20625-142">tooconfigure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="20625-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="20625-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="20625-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="20625-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="20625-145">**[Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) test kullanıcısı oluşturma](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)**  -toohave Britta Simon Five9 yanı sıra kullanıcı bağlantılı toohello Azure AD gösterimidir bağdaştırıcısı (CTI, kişi Center aracıları) içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="20625-145">**[Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** - toohave a counterpart of Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="20625-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="20625-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="20625-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="20625-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="20625-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="20625-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="20625-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="20625-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>

<span data-ttu-id="20625-150">**Azure AD çoklu oturum açma tooconfigure bağdaştırıcısıyla Five9 artı (CTI, kişi Center aracıları) hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="20625-150">**tooconfigure Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), perform hello following steps:**</span></span>

1. <span data-ttu-id="20625-151">Merhaba hello üzerinde Azure portal'ın **Five9 artı bağdaştırıcı (CTI, kişi Center aracıları)** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="20625-151">In hello Azure portal, on hello **Five9 Plus Adapter (CTI, Contact Center Agents)** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="20625-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="20625-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. <span data-ttu-id="20625-155">Merhaba üzerinde **Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="20625-155">On hello **Five9 Plus Adapter (CTI, Contact Center Agents) Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    <span data-ttu-id="20625-157">a.</span><span class="sxs-lookup"><span data-stu-id="20625-157">a.</span></span> <span data-ttu-id="20625-158">Merhaba, **tanımlayıcısı** metin kutusuna, türü aşağıdaki hello kullanarak bir URL düzenleri:</span><span class="sxs-lookup"><span data-stu-id="20625-158">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>

    |    <span data-ttu-id="20625-159">Ortam</span><span class="sxs-lookup"><span data-stu-id="20625-159">Environment</span></span>      |       <span data-ttu-id="20625-160">URL</span><span class="sxs-lookup"><span data-stu-id="20625-160">URL</span></span>      |
    | :-- | :-- |
    | <span data-ttu-id="20625-161">"Five9 Plus bağdaştırıcısı Microsoft Dynamics CRM için"</span><span class="sxs-lookup"><span data-stu-id="20625-161">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | <span data-ttu-id="20625-162">"Five9 Plus bağdaştırıcısı Zendesk için"</span><span class="sxs-lookup"><span data-stu-id="20625-162">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | <span data-ttu-id="20625-163">"Five9 Plus bağdaştırıcısı Aracısı Masaüstü araç seti için"</span><span class="sxs-lookup"><span data-stu-id="20625-163">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    <span data-ttu-id="20625-164">b.</span><span class="sxs-lookup"><span data-stu-id="20625-164">b.</span></span> <span data-ttu-id="20625-165">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="20625-165">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>

    |      <span data-ttu-id="20625-166">Ortam</span><span class="sxs-lookup"><span data-stu-id="20625-166">Environment</span></span>     |      <span data-ttu-id="20625-167">URL</span><span class="sxs-lookup"><span data-stu-id="20625-167">URL</span></span>      |
    | :--                  | :--           |
    | <span data-ttu-id="20625-168">"Five9 Plus bağdaştırıcısı Microsoft Dynamics CRM için"</span><span class="sxs-lookup"><span data-stu-id="20625-168">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | <span data-ttu-id="20625-169">"Five9 Plus bağdaştırıcısı Zendesk için"</span><span class="sxs-lookup"><span data-stu-id="20625-169">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | <span data-ttu-id="20625-170">"Five9 Plus bağdaştırıcısı Aracısı Masaüstü araç seti için"</span><span class="sxs-lookup"><span data-stu-id="20625-170">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. <span data-ttu-id="20625-171">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="20625-171">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. <span data-ttu-id="20625-173">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="20625-173">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="20625-175">Merhaba üzerinde **Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) yapılandırmasını** 'yi tıklatın **yapılandırma Five9 artı bağdaştırıcı (CTI, kişi Center aracıları)** tooopen **oturum açmayapılandırma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="20625-175">On hello **Five9 Plus Adapter (CTI, Contact Center Agents) Configuration** section, click **Configure Five9 Plus Adapter (CTI, Contact Center Agents)** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="20625-176">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="20625-176">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. <span data-ttu-id="20625-178">tooconfigure çoklu oturum açma üzerinde **Five9 artı bağdaştırıcı (CTI, kişi Center aracıları)** yan, indirilen toosend hello ihtiyacınız **Certificate(Base64), Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** çok[Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) destek ekibi](https://www.five9.com/about/contact).</span><span class="sxs-lookup"><span data-stu-id="20625-178">tooconfigure single sign-on on **Five9 Plus Adapter (CTI, Contact Center Agents)** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact).</span></span> <span data-ttu-id="20625-179">Ayrıca ek olarak, SSO daha fazla yapılandırmak için lütfen hello aşağıdaki toohello bağdaştırıcısı göre adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="20625-179">Also additionally, for configuring SSO further please follow hello below steps according toohello adapter:</span></span>

    <span data-ttu-id="20625-180">a.</span><span class="sxs-lookup"><span data-stu-id="20625-180">a.</span></span> <span data-ttu-id="20625-181">"Five9 artı bağdaştırıcısı Aracısı Masaüstü araç seti için" Yönetici Kılavuzu: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="20625-181">“Five9 Plus Adapter for Agent Desktop Toolkit” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="20625-182">b.</span><span class="sxs-lookup"><span data-stu-id="20625-182">b.</span></span> <span data-ttu-id="20625-183">"Five9 artı bağdaştırıcısı Microsoft Dynamics CRM için" Yönetici Kılavuzu: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="20625-183">“Five9 Plus Adapter for Microsoft Dynamics CRM” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="20625-184">c.</span><span class="sxs-lookup"><span data-stu-id="20625-184">c.</span></span> <span data-ttu-id="20625-185">"Five9 artı bağdaştırıcısı Zendesk için" Yönetici Kılavuzu: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="20625-185">“Five9 Plus Adapter for Zendesk” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span></span>


> [!TIP]
> <span data-ttu-id="20625-186">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="20625-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="20625-187">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="20625-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="20625-188">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="20625-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="20625-189">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="20625-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="20625-190">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="20625-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="20625-192">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="20625-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="20625-193">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="20625-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="20625-195">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="20625-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="20625-197">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="20625-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="20625-199">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="20625-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="20625-201">a.</span><span class="sxs-lookup"><span data-stu-id="20625-201">a.</span></span> <span data-ttu-id="20625-202">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="20625-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="20625-203">b.</span><span class="sxs-lookup"><span data-stu-id="20625-203">b.</span></span> <span data-ttu-id="20625-204">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="20625-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="20625-205">c.</span><span class="sxs-lookup"><span data-stu-id="20625-205">c.</span></span> <span data-ttu-id="20625-206">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="20625-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="20625-207">d.</span><span class="sxs-lookup"><span data-stu-id="20625-207">d.</span></span> <span data-ttu-id="20625-208">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="20625-208">Click **Create**.</span></span>
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a><span data-ttu-id="20625-209">Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="20625-209">Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user</span></span>

<span data-ttu-id="20625-210">Bu bölümde, Britta Simon Five9 artı bağdaştırıcısı (CTI, kişi Center aracıları) adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="20625-210">In this section, you create a user called Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents).</span></span> <span data-ttu-id="20625-211">Çalışmak [Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) destek ekibi](https://www.five9.com/about/contact) hello Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) platformu hello kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="20625-211">Work with [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact) to add hello users in hello Five9 Plus Adapter (CTI, Contact Center Agents) platform.</span></span> <span data-ttu-id="20625-212">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="20625-212">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="20625-213">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="20625-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="20625-214">Bu bölümde, erişim tooFive9 artı bağdaştırıcı (CTI, kişi Center aracıları) vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="20625-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFive9 Plus Adapter (CTI, Contact Center Agents).</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="20625-216">**tooassign Britta Simon tooFive9 artı bağdaştırıcı (CTI, kişi Center aracıları) hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="20625-216">**tooassign Britta Simon tooFive9 Plus Adapter (CTI, Contact Center Agents), perform hello following steps:**</span></span>

1. <span data-ttu-id="20625-217">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="20625-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="20625-219">Merhaba uygulamalar listesinde **Five9 artı bağdaştırıcı (CTI, kişi Center aracıları)**.</span><span class="sxs-lookup"><span data-stu-id="20625-219">In hello applications list, select **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. <span data-ttu-id="20625-221">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="20625-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="20625-223">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="20625-223">Click **Add** button.</span></span> <span data-ttu-id="20625-224">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="20625-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="20625-226">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="20625-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="20625-227">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="20625-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="20625-228">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="20625-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="20625-229">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="20625-229">Testing single sign-on</span></span>

<span data-ttu-id="20625-230">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="20625-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="20625-231">Merhaba Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="20625-231">When you click hello Five9 Plus Adapter (CTI, Contact Center Agents) tile in hello Access Panel, you should get automatically signed-on tooyour Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>
<span data-ttu-id="20625-232">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="20625-232">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="20625-233">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="20625-233">Additional resources</span></span>

* [<span data-ttu-id="20625-234">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="20625-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="20625-235">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="20625-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png

