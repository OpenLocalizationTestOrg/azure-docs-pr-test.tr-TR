---
title: "Öğretici: Azure Active Directory Tümleştirme ile Deputy | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Deputy arasında yapılandırmayı öğrenin."
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
ms.openlocfilehash: 51aed908208b7a40ea2ab710dffe84370b573991
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="28c2c-103">Öğretici: Azure Active Directory Tümleştirme Deputy ile</span><span class="sxs-lookup"><span data-stu-id="28c2c-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="28c2c-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Deputy tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="28c2c-104">In this tutorial, you learn how to integrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="28c2c-105">Deputy Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="28c2c-105">Integrating Deputy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="28c2c-106">Deputy erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="28c2c-106">You can control in Azure AD who has access to Deputy</span></span>
- <span data-ttu-id="28c2c-107">Otomatik olarak için Deputy (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="28c2c-107">You can enable your users to automatically get signed-on to Deputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="28c2c-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="28c2c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="28c2c-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="28c2c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28c2c-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="28c2c-110">Prerequisites</span></span>

<span data-ttu-id="28c2c-111">Azure AD tümleştirme Deputy ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="28c2c-111">To configure Azure AD integration with Deputy, you need the following items:</span></span>

- <span data-ttu-id="28c2c-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="28c2c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="28c2c-113">Bir Deputy çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="28c2c-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="28c2c-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="28c2c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="28c2c-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="28c2c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="28c2c-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="28c2c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="28c2c-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="28c2c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="28c2c-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="28c2c-118">Scenario description</span></span>
<span data-ttu-id="28c2c-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="28c2c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="28c2c-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="28c2c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="28c2c-121">Galeriden Deputy ekleme</span><span class="sxs-lookup"><span data-stu-id="28c2c-121">Adding Deputy from the gallery</span></span>
2. <span data-ttu-id="28c2c-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="28c2c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-the-gallery"></a><span data-ttu-id="28c2c-123">Galeriden Deputy ekleme</span><span class="sxs-lookup"><span data-stu-id="28c2c-123">Adding Deputy from the gallery</span></span>
<span data-ttu-id="28c2c-124">Azure AD Deputy tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Deputy eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="28c2c-124">To configure the integration of Deputy into Azure AD, you need to add Deputy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="28c2c-125">**Galeriden Deputy eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="28c2c-125">**To add Deputy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="28c2c-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="28c2c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="28c2c-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="28c2c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="28c2c-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="28c2c-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="28c2c-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="28c2c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="28c2c-133">Arama kutusuna **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="28c2c-133">In the search box, type **Deputy**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="28c2c-135">Sonuçlar panelinde seçin **Deputy**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="28c2c-135">In the results panel, select **Deputy**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="28c2c-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="28c2c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="28c2c-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Deputy ile test etme</span><span class="sxs-lookup"><span data-stu-id="28c2c-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="28c2c-139">Tekli çalışmaya oturum için Azure AD Deputy karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="28c2c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Deputy is to a user in Azure AD.</span></span> <span data-ttu-id="28c2c-140">Diğer bir deyişle, bir Azure AD kullanıcısının Deputy ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="28c2c-140">In other words, a link relationship between an Azure AD user and the related user in Deputy needs to be established.</span></span>

<span data-ttu-id="28c2c-141">Deputy içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="28c2c-141">In Deputy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="28c2c-142">Yapılandırma ve Azure AD çoklu oturum açma Deputy ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="28c2c-142">To configure and test Azure AD single sign-on with Deputy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="28c2c-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="28c2c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="28c2c-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="28c2c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="28c2c-145">**[Deputy test kullanıcısı oluşturma](#creating-a-deputy-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Deputy sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="28c2c-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - to have a counterpart of Britta Simon in Deputy that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="28c2c-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="28c2c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="28c2c-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="28c2c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="28c2c-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="28c2c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="28c2c-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Deputy uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="28c2c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="28c2c-150">**Azure AD çoklu oturum açma ile Deputy yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="28c2c-150">**To configure Azure AD single sign-on with Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="28c2c-151">Azure portalında üzerinde **Deputy** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="28c2c-151">In the Azure portal, on the **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="28c2c-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="28c2c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="28c2c-155">Üzerinde **Deputy etki alanı ve URL'leri** uygulamada yapılandırmak istiyorsanız, bölüm **IDP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="28c2c-155">On the **Deputy Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="28c2c-157">a.</span><span class="sxs-lookup"><span data-stu-id="28c2c-157">a.</span></span> <span data-ttu-id="28c2c-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="28c2c-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
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

    <span data-ttu-id="28c2c-159">b.</span><span class="sxs-lookup"><span data-stu-id="28c2c-159">b.</span></span> <span data-ttu-id="28c2c-160">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="28c2c-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
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

4. <span data-ttu-id="28c2c-161">Denetleme **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="28c2c-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="28c2c-162">Uygulamada yapılandırmak istiyorsanız **SP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="28c2c-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="28c2c-164">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="28c2c-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="28c2c-165">Deputy bölge sonekidir isteğe bağlı veya bunlardan birini kullanmalıdır: au | Belirtilmeyen | AB | olarak | la | af | bir | ent au | ent na | ent AB | ent-olarak | ent la | ent af | ent bir</span><span class="sxs-lookup"><span data-stu-id="28c2c-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="28c2c-166">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="28c2c-166">These values are not real.</span></span> <span data-ttu-id="28c2c-167">Bu değerler, gerçek tanımlayıcı, yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="28c2c-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="28c2c-168">Kişi [Deputy destek ekibi](https://www.deputy.com/call-centers-customer-support-scheduling-software) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="28c2c-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) to get these values.</span></span> 

5. <span data-ttu-id="28c2c-169">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="28c2c-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="28c2c-171">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="28c2c-171">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="28c2c-173">Üzerinde **Deputy yapılandırma** 'yi tıklatın **yapılandırma Deputy** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="28c2c-173">On the **Deputy Configuration** section, click **Configure Deputy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="28c2c-174">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="28c2c-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="28c2c-176">Aşağıdaki URL'ye gidin:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span><span class="sxs-lookup"><span data-stu-id="28c2c-176">Navigate to the following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="28c2c-177">Git **güvenlik ayarları** tıklatıp **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="28c2c-177">Go to **Security Settings** and click **Edit**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="28c2c-179">Bu **güvenlik ayarları** sayfasında, aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="28c2c-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="28c2c-181">a.</span><span class="sxs-lookup"><span data-stu-id="28c2c-181">a.</span></span> <span data-ttu-id="28c2c-182">Etkinleştirme **sosyal oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="28c2c-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="28c2c-183">b.</span><span class="sxs-lookup"><span data-stu-id="28c2c-183">b.</span></span> <span data-ttu-id="28c2c-184">Not Defteri'nde Azure portalından indirdiğiniz Base64 ile kodlanmış sertifikanızı açın, içeriğini, panoya kopyalayın ve ardından yapıştırın **OpenSSL sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="28c2c-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="28c2c-185">c.</span><span class="sxs-lookup"><span data-stu-id="28c2c-185">c.</span></span> <span data-ttu-id="28c2c-186">SAML SSO URL'si metin kutusuna yazın`https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span><span class="sxs-lookup"><span data-stu-id="28c2c-186">In the SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="28c2c-187">d.</span><span class="sxs-lookup"><span data-stu-id="28c2c-187">d.</span></span> <span data-ttu-id="28c2c-188">SAML SSO URL'si metin kutusuna Değiştir `<your subdomain>` , alt etki alanı ile.</span><span class="sxs-lookup"><span data-stu-id="28c2c-188">In the SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="28c2c-189">e.</span><span class="sxs-lookup"><span data-stu-id="28c2c-189">e.</span></span> <span data-ttu-id="28c2c-190">SAML SSO URL'si metin kutusuna Değiştir `<saml sso url>` ile **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="28c2c-190">In the SAML SSO URL textbox, replace `<saml sso url>` with the **SAML Single Sign-On Service URL** you have copied from the Azure portal.</span></span>
   
    <span data-ttu-id="28c2c-191">f.</span><span class="sxs-lookup"><span data-stu-id="28c2c-191">f.</span></span> <span data-ttu-id="28c2c-192">Tıklatın **ayarlarını kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="28c2c-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="28c2c-193">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="28c2c-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="28c2c-194">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="28c2c-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="28c2c-195">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="28c2c-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="28c2c-196">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="28c2c-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="28c2c-197">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="28c2c-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="28c2c-199">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="28c2c-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="28c2c-200">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="28c2c-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="28c2c-202">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="28c2c-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="28c2c-204">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="28c2c-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="28c2c-206">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="28c2c-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="28c2c-208">a.</span><span class="sxs-lookup"><span data-stu-id="28c2c-208">a.</span></span> <span data-ttu-id="28c2c-209">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="28c2c-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="28c2c-210">b.</span><span class="sxs-lookup"><span data-stu-id="28c2c-210">b.</span></span> <span data-ttu-id="28c2c-211">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="28c2c-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="28c2c-212">c.</span><span class="sxs-lookup"><span data-stu-id="28c2c-212">c.</span></span> <span data-ttu-id="28c2c-213">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="28c2c-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="28c2c-214">d.</span><span class="sxs-lookup"><span data-stu-id="28c2c-214">d.</span></span> <span data-ttu-id="28c2c-215">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="28c2c-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="28c2c-216">Deputy test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="28c2c-216">Creating a Deputy test user</span></span>

<span data-ttu-id="28c2c-217">Azure AD kullanıcıları için Deputy oturum açmak etkinleştirmek için bunların Deputy sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="28c2c-217">To enable Azure AD users to log in to Deputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="28c2c-218">Deputy durumunda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="28c2c-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="28c2c-219">Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="28c2c-219">To provision a user account, perform the following steps:</span></span>
1. <span data-ttu-id="28c2c-220">Deputy şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="28c2c-220">Log in to your Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="28c2c-221">Üst gezinti bölmesinde tıklatın **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="28c2c-221">On the top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="28c2c-222">![Kişiler](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "kişiler")</span><span class="sxs-lookup"><span data-stu-id="28c2c-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="28c2c-223">' I tıklatın **kişiler eklemek** düğmesini tıklatın ve tıklatın **tek bir kişinin eklemek**.</span><span class="sxs-lookup"><span data-stu-id="28c2c-223">Click the **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="28c2c-224">![Kişi Ekle](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "kişileri ekleyin")</span><span class="sxs-lookup"><span data-stu-id="28c2c-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="28c2c-225">Aşağıdaki adımları gerçekleştirin ve tıklayın **davet & Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="28c2c-225">Perform the following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="28c2c-226">![Yeni kullanıcı](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="28c2c-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="28c2c-227">a.</span><span class="sxs-lookup"><span data-stu-id="28c2c-227">a.</span></span> <span data-ttu-id="28c2c-228">İçinde **adı** metin kutusuna, bir kullanıcı gibi tür adını **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="28c2c-228">In the **Name** textbox, type name of the user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="28c2c-229">b.</span><span class="sxs-lookup"><span data-stu-id="28c2c-229">b.</span></span> <span data-ttu-id="28c2c-230">İçinde **e-posta** metin kutusuna, sağlamak istediğiniz bir Azure AD hesabının e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="28c2c-230">In the **Email** textbox, type the email address of an Azure AD account you want to provision.</span></span>
   
   <span data-ttu-id="28c2c-231">c.</span><span class="sxs-lookup"><span data-stu-id="28c2c-231">c.</span></span> <span data-ttu-id="28c2c-232">İçinde **adresindeki iş** metin kutusuna, iş adı yazın.</span><span class="sxs-lookup"><span data-stu-id="28c2c-232">In the **Work at** textbox, type the business name.</span></span>
   
   <span data-ttu-id="28c2c-233">d.</span><span class="sxs-lookup"><span data-stu-id="28c2c-233">d.</span></span> <span data-ttu-id="28c2c-234">Tıklatın **davet & Kaydet** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="28c2c-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="28c2c-235">AAD hesap sahibi bir e-posta alır ve bunu etkinleştirilmeden önce kendi hesabı onaylamak için bir bağlantı izler.</span><span class="sxs-lookup"><span data-stu-id="28c2c-235">The AAD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="28c2c-236">API sağlama AAD kullanıcı hesaplarına Deputy tarafından sağlanan veya herhangi diğer Deputy kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28c2c-236">You can use any other Deputy user account creation tools or APIs provided by Deputy to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="28c2c-237">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="28c2c-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="28c2c-238">Bu bölümde, Britta Deputy için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="28c2c-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Deputy.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="28c2c-240">**Deputy için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="28c2c-240">**To assign Britta Simon to Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="28c2c-241">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="28c2c-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="28c2c-243">Uygulamalar listesinde **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="28c2c-243">In the applications list, select **Deputy**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="28c2c-245">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="28c2c-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="28c2c-247">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="28c2c-247">Click **Add** button.</span></span> <span data-ttu-id="28c2c-248">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="28c2c-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="28c2c-250">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="28c2c-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="28c2c-251">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="28c2c-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="28c2c-252">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="28c2c-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="28c2c-253">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="28c2c-253">Testing single sign-on</span></span>

<span data-ttu-id="28c2c-254">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="28c2c-254">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="28c2c-255">Erişim paneli Deputy parçasında tıklattığınızda, otomatik olarak Deputy uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="28c2c-255">When you click the Deputy tile in the Access Panel, you should get automatically signed-on to your Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="28c2c-256">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="28c2c-256">Additional resources</span></span>

* [<span data-ttu-id="28c2c-257">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="28c2c-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="28c2c-258">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="28c2c-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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

