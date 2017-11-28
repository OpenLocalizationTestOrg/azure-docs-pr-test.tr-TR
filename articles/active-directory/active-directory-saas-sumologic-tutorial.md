---
title: "Öğretici: Azure Active Directory Tümleştirme ile SumoLogic | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile SumoLogic arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 2ef1bd329f5db8899f0b57744e4c0f6eed1c532f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="c9856-103">Öğretici: Azure Active Directory Tümleştirme SumoLogic ile</span><span class="sxs-lookup"><span data-stu-id="c9856-103">Tutorial: Azure Active Directory integration with SumoLogic</span></span>

<span data-ttu-id="c9856-104">Bu öğreticide, bilgi nasıl toointegrate SumoLogic Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c9856-104">In this tutorial, you learn how toointegrate SumoLogic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c9856-105">SumoLogic Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="c9856-105">Integrating SumoLogic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c9856-106">Erişim tooSumoLogic sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c9856-106">You can control in Azure AD who has access tooSumoLogic</span></span>
- <span data-ttu-id="c9856-107">Kullanıcıların tooautomatically get açan tooSumoLogic (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c9856-107">You can enable your users tooautomatically get signed-on tooSumoLogic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c9856-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="c9856-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c9856-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c9856-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9856-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c9856-110">Prerequisites</span></span>

<span data-ttu-id="c9856-111">tooconfigure SumoLogic ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c9856-111">tooconfigure Azure AD integration with SumoLogic, you need hello following items:</span></span>

- <span data-ttu-id="c9856-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="c9856-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c9856-113">Bir SumoLogic çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="c9856-113">A SumoLogic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c9856-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="c9856-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c9856-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="c9856-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c9856-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c9856-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c9856-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c9856-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c9856-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="c9856-118">Scenario description</span></span>
<span data-ttu-id="c9856-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="c9856-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c9856-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="c9856-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c9856-121">Merhaba Galerisi'nden SumoLogic ekleme</span><span class="sxs-lookup"><span data-stu-id="c9856-121">Adding SumoLogic from hello gallery</span></span>
2. <span data-ttu-id="c9856-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c9856-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumologic-from-hello-gallery"></a><span data-ttu-id="c9856-123">Merhaba Galerisi'nden SumoLogic ekleme</span><span class="sxs-lookup"><span data-stu-id="c9856-123">Adding SumoLogic from hello gallery</span></span>
<span data-ttu-id="c9856-124">Azure AD'ye tooconfigure hello tümleştirme SumoLogic, tooadd SumoLogic hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9856-124">tooconfigure hello integration of SumoLogic into Azure AD, you need tooadd SumoLogic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c9856-125">**tooadd SumoLogic hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c9856-125">**tooadd SumoLogic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9856-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c9856-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c9856-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="c9856-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c9856-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c9856-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="c9856-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c9856-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="c9856-133">Merhaba arama kutusuna yazın **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="c9856-133">In hello search box, type **SumoLogic**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. <span data-ttu-id="c9856-135">Merhaba Sonuçlar panelinde seçin **SumoLogic**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="c9856-135">In hello results panel, select **SumoLogic**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c9856-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c9856-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c9856-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı SumoLogic sınayın.</span><span class="sxs-lookup"><span data-stu-id="c9856-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c9856-139">Tek toowork'ın oturum açma hangi hello karşılık gelen SumoLogic içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9856-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SumoLogic is tooa user in Azure AD.</span></span> <span data-ttu-id="c9856-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı SumoLogic hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9856-140">In other words, a link relationship between an Azure AD user and hello related user in SumoLogic needs toobe established.</span></span>

<span data-ttu-id="c9856-141">Merhaba hello değeri SumoLogic içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="c9856-141">In SumoLogic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c9856-142">tooconfigure ve SumoLogic ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c9856-142">tooconfigure and test Azure AD single sign-on with SumoLogic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c9856-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="c9856-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c9856-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="c9856-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c9856-145">**[SumoLogic test kullanıcısı oluşturma](#creating-a-sumologic-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir SumoLogic içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="c9856-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - toohave a counterpart of Britta Simon in SumoLogic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c9856-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="c9856-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c9856-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="c9856-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c9856-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c9856-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c9856-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma SumoLogic uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c9856-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SumoLogic application.</span></span>

<span data-ttu-id="c9856-150">**tooconfigure Azure AD çoklu oturum açma ile SumoLogic, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c9856-150">**tooconfigure Azure AD single sign-on with SumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9856-151">Hello hello üzerinde Azure portal'ın **SumoLogic** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c9856-151">In hello Azure portal, on hello **SumoLogic** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="c9856-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="c9856-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. <span data-ttu-id="c9856-155">Merhaba üzerinde **SumoLogic etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c9856-155">On hello **SumoLogic Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    <span data-ttu-id="c9856-157">a.</span><span class="sxs-lookup"><span data-stu-id="c9856-157">a.</span></span> <span data-ttu-id="c9856-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenantname>.SumoLogic.com`</span><span class="sxs-lookup"><span data-stu-id="c9856-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.SumoLogic.com`</span></span>

    <span data-ttu-id="c9856-159">b.</span><span class="sxs-lookup"><span data-stu-id="c9856-159">b.</span></span> <span data-ttu-id="c9856-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="c9856-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > <span data-ttu-id="c9856-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="c9856-161">These values are not real.</span></span> <span data-ttu-id="c9856-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="c9856-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c9856-163">Kişi [SumoLogic istemci destek ekibi](https://www.sumologic.com/contact-us/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="c9856-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="c9856-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c9856-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. <span data-ttu-id="c9856-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c9856-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c9856-168">Merhaba üzerinde **SumoLogic yapılandırma** 'yi tıklatın **yapılandırma SumoLogic** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="c9856-168">On hello **SumoLogic Configuration** section, click **Configure SumoLogic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c9856-169">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="c9856-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. <span data-ttu-id="c9856-171">Farklı web tarayıcısı penceresinde tooyour SumoLogic şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c9856-171">In a different web browser window, log in tooyour SumoLogic company site as an administrator.</span></span>

8. <span data-ttu-id="c9856-172">Çok Git**Yönet \> güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="c9856-172">Go too**Manage \> Security**.</span></span>
   
    <span data-ttu-id="c9856-173">![Yönetme](./media/active-directory-saas-sumologic-tutorial/ic778556.png "yönetme")</span><span class="sxs-lookup"><span data-stu-id="c9856-173">![Manage](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Manage")</span></span>

9. <span data-ttu-id="c9856-174">Tıklatın **SAML**.</span><span class="sxs-lookup"><span data-stu-id="c9856-174">Click **SAML**.</span></span>
   
    <span data-ttu-id="c9856-175">![Genel güvenlik ayarları](./media/active-directory-saas-sumologic-tutorial/ic778557.png "genel güvenlik ayarları")</span><span class="sxs-lookup"><span data-stu-id="c9856-175">![Global security settings](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Global security settings")</span></span>

10. <span data-ttu-id="c9856-176">Merhaba gelen **bir yapılandırma seçin veya yeni bir tane oluşturun** listesinde, seçin **Azure AD**ve ardından **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="c9856-176">From hello **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="c9856-177">![SAML 2.0 yapılandırma](./media/active-directory-saas-sumologic-tutorial/ic778558.png "SAML 2.0 yapılandırma")</span><span class="sxs-lookup"><span data-stu-id="c9856-177">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span></span>

11. <span data-ttu-id="c9856-178">Merhaba üzerinde **yapılandırma SAML 2.0** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c9856-178">On hello **Configure SAML 2.0** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="c9856-179">![SAML 2.0 yapılandırma](./media/active-directory-saas-sumologic-tutorial/ic778559.png "SAML 2.0 yapılandırma")</span><span class="sxs-lookup"><span data-stu-id="c9856-179">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span></span>
   
    <span data-ttu-id="c9856-180">a.</span><span class="sxs-lookup"><span data-stu-id="c9856-180">a.</span></span> <span data-ttu-id="c9856-181">Merhaba, **yapılandırma adı** metin kutusuna, türü **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="c9856-181">In hello **Configuration Name** textbox, type **Azure AD**.</span></span> 

    <span data-ttu-id="c9856-182">b.</span><span class="sxs-lookup"><span data-stu-id="c9856-182">b.</span></span> <span data-ttu-id="c9856-183">Seçin **hata ayıklama modu**.</span><span class="sxs-lookup"><span data-stu-id="c9856-183">Select **Debug Mode**.</span></span>

    <span data-ttu-id="c9856-184">c.</span><span class="sxs-lookup"><span data-stu-id="c9856-184">c.</span></span> <span data-ttu-id="c9856-185">Merhaba, **veren** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="c9856-185">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="c9856-186">d.</span><span class="sxs-lookup"><span data-stu-id="c9856-186">d.</span></span> <span data-ttu-id="c9856-187">Merhaba, **Authn istek URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="c9856-187">In hello **Authn Request URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c9856-188">e.</span><span class="sxs-lookup"><span data-stu-id="c9856-188">e.</span></span> <span data-ttu-id="c9856-189">Base-64 kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve ardından yapıştırın içine tüm sertifika hello **X.509 sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="c9856-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="c9856-190">f.</span><span class="sxs-lookup"><span data-stu-id="c9856-190">f.</span></span> <span data-ttu-id="c9856-191">Olarak **e-posta özniteliği**seçin **kullanım SAML konu**.</span><span class="sxs-lookup"><span data-stu-id="c9856-191">As **Email Attribute**, select **Use SAML subject**.</span></span>  

    <span data-ttu-id="c9856-192">g.</span><span class="sxs-lookup"><span data-stu-id="c9856-192">g.</span></span> <span data-ttu-id="c9856-193">Seçin **SP tarafından başlatılan oturum açma yapılandırması**.</span><span class="sxs-lookup"><span data-stu-id="c9856-193">Select **SP initiated Login Configuration**.</span></span>

    <span data-ttu-id="c9856-194">h.</span><span class="sxs-lookup"><span data-stu-id="c9856-194">h.</span></span> <span data-ttu-id="c9856-195">Merhaba, **oturum açma yolunu** metin kutusuna, türü **Azure** tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="c9856-195">In hello **Login Path** textbox, type **Azure** and click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c9856-196">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="c9856-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c9856-197">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="c9856-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c9856-198">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c9856-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c9856-199">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c9856-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="c9856-200">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="c9856-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="c9856-202">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c9856-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9856-203">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c9856-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c9856-205">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c9856-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c9856-207">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="c9856-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c9856-209">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c9856-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c9856-211">a.</span><span class="sxs-lookup"><span data-stu-id="c9856-211">a.</span></span> <span data-ttu-id="c9856-212">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c9856-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c9856-213">b.</span><span class="sxs-lookup"><span data-stu-id="c9856-213">b.</span></span> <span data-ttu-id="c9856-214">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="c9856-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c9856-215">c.</span><span class="sxs-lookup"><span data-stu-id="c9856-215">c.</span></span> <span data-ttu-id="c9856-216">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="c9856-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c9856-217">d.</span><span class="sxs-lookup"><span data-stu-id="c9856-217">d.</span></span> <span data-ttu-id="c9856-218">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9856-218">Click **Create**.</span></span>
 
### <a name="creating-a-sumologic-test-user"></a><span data-ttu-id="c9856-219">SumoLogic test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c9856-219">Creating a SumoLogic test user</span></span>

<span data-ttu-id="c9856-220">Sağlanan tooSumoLogic tooSumoLogic içinde sipariş tooenable Azure AD kullanıcıların toolog içinde olmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9856-220">In order tooenable Azure AD users toolog in tooSumoLogic, they must be provisioned tooSumoLogic.</span></span>  

* <span data-ttu-id="c9856-221">SumoLogic Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="c9856-221">In hello case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="c9856-222">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c9856-222">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9856-223">İçinde tooyour oturum **SumoLogic** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="c9856-223">Log in tooyour **SumoLogic** tenant.</span></span>

2. <span data-ttu-id="c9856-224">Çok Git**Yönet \> kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c9856-224">Go too**Manage \> Users**.</span></span>
   
    <span data-ttu-id="c9856-225">![Kullanıcıların](./media/active-directory-saas-sumologic-tutorial/ic778561.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="c9856-225">![Users](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Users")</span></span>

3. <span data-ttu-id="c9856-226">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9856-226">Click **Add**.</span></span>
   
    <span data-ttu-id="c9856-227">![Kullanıcıların](./media/active-directory-saas-sumologic-tutorial/ic778562.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="c9856-227">![Users](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Users")</span></span>

4. <span data-ttu-id="c9856-228">Merhaba üzerinde **yeni kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c9856-228">On hello **New User** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="c9856-229">![Yeni kullanıcı](./media/active-directory-saas-sumologic-tutorial/ic778563.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="c9856-229">![New User](./media/active-directory-saas-sumologic-tutorial/ic778563.png "New User")</span></span> 
 
    <span data-ttu-id="c9856-230">a.</span><span class="sxs-lookup"><span data-stu-id="c9856-230">a.</span></span> <span data-ttu-id="c9856-231">Türü hello ilgili bilgileri hello tooprovision istediğiniz hello Azure AD hesabının **ad**, **Soyadı**, ve **e-posta** metin kutuları.</span><span class="sxs-lookup"><span data-stu-id="c9856-231">Type hello related information of hello Azure AD account you want tooprovision into hello **First Name**, **Last Name**, and **Email** textboxes.</span></span>
  
    <span data-ttu-id="c9856-232">b.</span><span class="sxs-lookup"><span data-stu-id="c9856-232">b.</span></span> <span data-ttu-id="c9856-233">Bir rol seçin.</span><span class="sxs-lookup"><span data-stu-id="c9856-233">Select a role.</span></span>
  
    <span data-ttu-id="c9856-234">c.</span><span class="sxs-lookup"><span data-stu-id="c9856-234">c.</span></span> <span data-ttu-id="c9856-235">Olarak **durum**seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="c9856-235">As **Status**, select **Active**.</span></span>
  
    <span data-ttu-id="c9856-236">d.</span><span class="sxs-lookup"><span data-stu-id="c9856-236">d.</span></span> <span data-ttu-id="c9856-237">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9856-237">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="c9856-238">API AAD kullanıcı hesaplarının SumoLogic tooprovision tarafından sağlanan veya herhangi diğer SumoLogic kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9856-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c9856-239">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="c9856-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c9856-240">Bu bölümde, erişim tooSumoLogic vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c9856-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSumoLogic.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="c9856-242">**tooassign Britta Simon tooSumoLogic hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c9856-242">**tooassign Britta Simon tooSumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9856-243">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c9856-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="c9856-245">Merhaba uygulamalar listesinde **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="c9856-245">In hello applications list, select **SumoLogic**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. <span data-ttu-id="c9856-247">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c9856-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="c9856-249">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c9856-249">Click **Add** button.</span></span> <span data-ttu-id="c9856-250">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c9856-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="c9856-252">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="c9856-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c9856-253">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c9856-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c9856-254">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c9856-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c9856-255">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="c9856-255">Testing single sign-on</span></span>

<span data-ttu-id="c9856-256">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c9856-256">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c9856-257">Merhaba SumoLogic hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour SumoLogic uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9856-257">When you click hello SumoLogic tile in hello Access Panel, you should get automatically signed-on tooyour SumoLogic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c9856-258">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c9856-258">Additional resources</span></span>

* [<span data-ttu-id="c9856-259">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="c9856-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c9856-260">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="c9856-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

