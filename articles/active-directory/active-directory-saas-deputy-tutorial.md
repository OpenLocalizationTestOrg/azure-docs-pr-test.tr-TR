---
title: "Öğretici: Azure Active Directory Tümleştirme ile Deputy | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Deputy arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 42f65b758682ce2513b6bb38ef40a19f955c88c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="32d01-103">Öğretici: Azure Active Directory Tümleştirme Deputy ile</span><span class="sxs-lookup"><span data-stu-id="32d01-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="32d01-104">Bu öğreticide, bilgi nasıl toointegrate Deputy Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32d01-104">In this tutorial, you learn how toointegrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32d01-105">Deputy Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="32d01-105">Integrating Deputy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="32d01-106">Erişim tooDeputy sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="32d01-106">You can control in Azure AD who has access tooDeputy</span></span>
- <span data-ttu-id="32d01-107">Kullanıcıların tooautomatically get açan tooDeputy (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="32d01-107">You can enable your users tooautomatically get signed-on tooDeputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="32d01-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="32d01-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="32d01-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32d01-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32d01-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="32d01-110">Prerequisites</span></span>

<span data-ttu-id="32d01-111">tooconfigure Deputy ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="32d01-111">tooconfigure Azure AD integration with Deputy, you need hello following items:</span></span>

- <span data-ttu-id="32d01-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="32d01-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32d01-113">Bir Deputy çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="32d01-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32d01-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="32d01-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32d01-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="32d01-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32d01-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="32d01-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32d01-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32d01-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32d01-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="32d01-118">Scenario description</span></span>
<span data-ttu-id="32d01-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="32d01-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32d01-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="32d01-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32d01-121">Merhaba Galerisi'nden Deputy ekleme</span><span class="sxs-lookup"><span data-stu-id="32d01-121">Adding Deputy from hello gallery</span></span>
2. <span data-ttu-id="32d01-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="32d01-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-hello-gallery"></a><span data-ttu-id="32d01-123">Merhaba Galerisi'nden Deputy ekleme</span><span class="sxs-lookup"><span data-stu-id="32d01-123">Adding Deputy from hello gallery</span></span>
<span data-ttu-id="32d01-124">Azure AD'ye tooconfigure hello tümleştirme Deputy, tooadd Deputy hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="32d01-124">tooconfigure hello integration of Deputy into Azure AD, you need tooadd Deputy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="32d01-125">**tooadd Deputy hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="32d01-125">**tooadd Deputy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="32d01-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="32d01-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="32d01-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="32d01-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="32d01-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="32d01-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="32d01-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="32d01-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="32d01-133">Merhaba arama kutusuna yazın **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="32d01-133">In hello search box, type **Deputy**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="32d01-135">Merhaba Sonuçlar panelinde seçin **Deputy**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="32d01-135">In hello results panel, select **Deputy**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="32d01-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="32d01-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="32d01-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Deputy ile test etme</span><span class="sxs-lookup"><span data-stu-id="32d01-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="32d01-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Deputy içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="32d01-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Deputy is tooa user in Azure AD.</span></span> <span data-ttu-id="32d01-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Deputy hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="32d01-140">In other words, a link relationship between an Azure AD user and hello related user in Deputy needs toobe established.</span></span>

<span data-ttu-id="32d01-141">Merhaba hello değeri Deputy içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="32d01-141">In Deputy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="32d01-142">tooconfigure ve Deputy ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="32d01-142">tooconfigure and test Azure AD single sign-on with Deputy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="32d01-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="32d01-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="32d01-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="32d01-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32d01-145">**[Deputy test kullanıcısı oluşturma](#creating-a-deputy-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Deputy içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="32d01-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - toohave a counterpart of Britta Simon in Deputy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="32d01-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="32d01-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32d01-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="32d01-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="32d01-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="32d01-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="32d01-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Deputy uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="32d01-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="32d01-150">**tooconfigure Azure AD çoklu oturum açma ile Deputy, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="32d01-150">**tooconfigure Azure AD single sign-on with Deputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="32d01-151">Hello hello üzerinde Azure portal'ın **Deputy** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="32d01-151">In hello Azure portal, on hello **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="32d01-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="32d01-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="32d01-155">Merhaba üzerinde **Deputy etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="32d01-155">On hello **Deputy Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="32d01-157">a.</span><span class="sxs-lookup"><span data-stu-id="32d01-157">a.</span></span> <span data-ttu-id="32d01-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="32d01-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="32d01-159">b.</span><span class="sxs-lookup"><span data-stu-id="32d01-159">b.</span></span> <span data-ttu-id="32d01-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="32d01-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. <span data-ttu-id="32d01-161">Denetleme **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="32d01-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="32d01-162">Tooconfigure hello uygulamada istiyorsanız **SP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="32d01-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="32d01-164">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="32d01-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="32d01-165">Deputy bölge sonekidir isteğe bağlı veya bunlardan birini kullanmalıdır: au | Belirtilmeyen | AB | olarak | la | af | bir | ent au | ent na | ent AB | ent-olarak | ent la | ent af | ent bir</span><span class="sxs-lookup"><span data-stu-id="32d01-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="32d01-166">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="32d01-166">These values are not real.</span></span> <span data-ttu-id="32d01-167">Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="32d01-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="32d01-168">Kişi [Deputy destek ekibi](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="32d01-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget these values.</span></span> 

5. <span data-ttu-id="32d01-169">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="32d01-169">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="32d01-171">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="32d01-171">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="32d01-173">Merhaba üzerinde **Deputy yapılandırma** 'yi tıklatın **yapılandırma Deputy** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="32d01-173">On hello **Deputy Configuration** section, click **Configure Deputy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="32d01-174">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="32d01-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="32d01-176">URL aşağıdaki toohello gidin:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span><span class="sxs-lookup"><span data-stu-id="32d01-176">Navigate toohello following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="32d01-177">Çok Git**güvenlik ayarları** tıklatıp **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="32d01-177">Go too**Security Settings** and click **Edit**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="32d01-179">Bu **güvenlik ayarları** sayfasında, aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="32d01-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="32d01-181">a.</span><span class="sxs-lookup"><span data-stu-id="32d01-181">a.</span></span> <span data-ttu-id="32d01-182">Etkinleştirme **sosyal oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="32d01-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="32d01-183">b.</span><span class="sxs-lookup"><span data-stu-id="32d01-183">b.</span></span> <span data-ttu-id="32d01-184">Not Defteri'nde, kopyalama hello panonuza bunu içerik Azure portalından indirdiğiniz, Base64 ile kodlanmış sertifikasını açın ve toohello Yapıştır **OpenSSL sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="32d01-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="32d01-185">c.</span><span class="sxs-lookup"><span data-stu-id="32d01-185">c.</span></span> <span data-ttu-id="32d01-186">Merhaba SAML SSO URL'si metin kutusuna yazın`https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span><span class="sxs-lookup"><span data-stu-id="32d01-186">In hello SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="32d01-187">d.</span><span class="sxs-lookup"><span data-stu-id="32d01-187">d.</span></span> <span data-ttu-id="32d01-188">Merhaba SAML SSO URL metin kutusunda, yerine `<your subdomain>` , alt etki alanı ile.</span><span class="sxs-lookup"><span data-stu-id="32d01-188">In hello SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="32d01-189">e.</span><span class="sxs-lookup"><span data-stu-id="32d01-189">e.</span></span> <span data-ttu-id="32d01-190">Hello SAML SSO URL metin kutusunda, yerine `<saml sso url>` hello ile **SAML çoklu oturum açma hizmet URL'si** hello Azure portal ' kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="32d01-190">In hello SAML SSO URL textbox, replace `<saml sso url>` with hello **SAML Single Sign-On Service URL** you have copied from hello Azure portal.</span></span>
   
    <span data-ttu-id="32d01-191">f.</span><span class="sxs-lookup"><span data-stu-id="32d01-191">f.</span></span> <span data-ttu-id="32d01-192">Tıklatın **ayarlarını kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="32d01-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="32d01-193">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="32d01-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="32d01-194">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="32d01-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="32d01-195">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="32d01-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="32d01-196">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="32d01-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="32d01-197">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="32d01-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="32d01-199">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="32d01-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="32d01-200">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="32d01-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="32d01-202">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="32d01-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="32d01-204">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="32d01-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32d01-206">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="32d01-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32d01-208">a.</span><span class="sxs-lookup"><span data-stu-id="32d01-208">a.</span></span> <span data-ttu-id="32d01-209">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32d01-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32d01-210">b.</span><span class="sxs-lookup"><span data-stu-id="32d01-210">b.</span></span> <span data-ttu-id="32d01-211">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="32d01-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="32d01-212">c.</span><span class="sxs-lookup"><span data-stu-id="32d01-212">c.</span></span> <span data-ttu-id="32d01-213">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="32d01-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="32d01-214">d.</span><span class="sxs-lookup"><span data-stu-id="32d01-214">d.</span></span> <span data-ttu-id="32d01-215">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="32d01-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="32d01-216">Deputy test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="32d01-216">Creating a Deputy test user</span></span>

<span data-ttu-id="32d01-217">tooenable Azure AD kullanıcıların toolog tooDeputy bunların Deputy sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="32d01-217">tooenable Azure AD users toolog in tooDeputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="32d01-218">Deputy durumunda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="32d01-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="32d01-219">bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="32d01-219">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="32d01-220">Tooyour Deputy şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="32d01-220">Log in tooyour Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="32d01-221">Merhaba üst gezinti bölmesinde tıklatın **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="32d01-221">On hello top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="32d01-222">![Kişiler](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "kişiler")</span><span class="sxs-lookup"><span data-stu-id="32d01-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="32d01-223">Hello tıklatın **eklemek kişiler** düğmesini tıklatın ve'ı tıklatın **tek bir kişinin eklemek**.</span><span class="sxs-lookup"><span data-stu-id="32d01-223">Click hello **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="32d01-224">![Kişi Ekle](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "kişileri ekleyin")</span><span class="sxs-lookup"><span data-stu-id="32d01-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="32d01-225">Merhaba aşağıdaki adımları gerçekleştirin ve tıklatın **davet & Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="32d01-225">Perform hello following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="32d01-226">![Yeni kullanıcı](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="32d01-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="32d01-227">a.</span><span class="sxs-lookup"><span data-stu-id="32d01-227">a.</span></span> <span data-ttu-id="32d01-228">Merhaba, **adı** metin kutusuna, hello kullanıcı gibi tür adını **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32d01-228">In hello **Name** textbox, type name of hello user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="32d01-229">b.</span><span class="sxs-lookup"><span data-stu-id="32d01-229">b.</span></span> <span data-ttu-id="32d01-230">Merhaba, **e-posta** metin kutusuna, tooprovision istediğiniz bir Azure AD hesabının hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="32d01-230">In hello **Email** textbox, type hello email address of an Azure AD account you want tooprovision.</span></span>
   
   <span data-ttu-id="32d01-231">c.</span><span class="sxs-lookup"><span data-stu-id="32d01-231">c.</span></span> <span data-ttu-id="32d01-232">Merhaba, **adresindeki iş** metin kutusuna, tür hello iş adı.</span><span class="sxs-lookup"><span data-stu-id="32d01-232">In hello **Work at** textbox, type hello business name.</span></span>
   
   <span data-ttu-id="32d01-233">d.</span><span class="sxs-lookup"><span data-stu-id="32d01-233">d.</span></span> <span data-ttu-id="32d01-234">Tıklatın **davet & Kaydet** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="32d01-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="32d01-235">Merhaba AAD hesap sahibi bir e-posta alır ve onu etkinleştirilmeden önce bir bağlantı tooconfirm hesaplarında izler.</span><span class="sxs-lookup"><span data-stu-id="32d01-235">hello AAD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="32d01-236">API, kullanıcı hesaplarını Deputy tooprovision AAD tarafından sağlanan veya herhangi diğer Deputy kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32d01-236">You can use any other Deputy user account creation tools or APIs provided by Deputy tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="32d01-237">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="32d01-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="32d01-238">Bu bölümde, erişim tooDeputy vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="32d01-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDeputy.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="32d01-240">**tooassign Britta Simon tooDeputy hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="32d01-240">**tooassign Britta Simon tooDeputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="32d01-241">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="32d01-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="32d01-243">Merhaba uygulamalar listesinde **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="32d01-243">In hello applications list, select **Deputy**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="32d01-245">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="32d01-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="32d01-247">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="32d01-247">Click **Add** button.</span></span> <span data-ttu-id="32d01-248">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="32d01-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="32d01-250">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="32d01-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="32d01-251">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="32d01-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32d01-252">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="32d01-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="32d01-253">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="32d01-253">Testing single sign-on</span></span>

<span data-ttu-id="32d01-254">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="32d01-254">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="32d01-255">Deputy döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma Deputy uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="32d01-255">When you click hello Deputy tile in hello Access Panel, you should get automatically signed-on tooyour Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32d01-256">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="32d01-256">Additional resources</span></span>

* [<span data-ttu-id="32d01-257">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="32d01-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32d01-258">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="32d01-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

