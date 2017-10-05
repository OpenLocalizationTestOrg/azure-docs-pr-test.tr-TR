---
title: "Öğretici: Azure Active Directory Tümleştirme ile Aha! | Microsoft Belgeleri"
description: "Çoklu oturum açma Azure Active Directory ile Aha arasında yapılandırmayı öğrenin!."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7723864b2e1ab2d5b69d86f0fa18416b9d3f9aa3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="97047-104">Öğretici: Azure Active Directory Tümleştirme ile Aha!</span><span class="sxs-lookup"><span data-stu-id="97047-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="97047-105">Bu öğreticide, Aha tümleştirmek öğrenin!</span><span class="sxs-lookup"><span data-stu-id="97047-105">In this tutorial, you learn how to integrate Aha!</span></span> <span data-ttu-id="97047-106">Azure ile Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="97047-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="97047-107">AHA tümleştirme!</span><span class="sxs-lookup"><span data-stu-id="97047-107">Integrating Aha!</span></span> <span data-ttu-id="97047-108">Azure AD ile aşağıdaki faydaları sağlar:</span><span class="sxs-lookup"><span data-stu-id="97047-108">with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="97047-109">Aha erişimi, Azure AD'de kontrol edebilirsiniz!</span><span class="sxs-lookup"><span data-stu-id="97047-109">You can control in Azure AD who has access to Aha!</span></span>
- <span data-ttu-id="97047-110">Otomatik olarak Aha için açan kullanıcılarınıza etkinleştirebilirsiniz!</span><span class="sxs-lookup"><span data-stu-id="97047-110">You can enable your users to automatically get signed-on to Aha!</span></span> <span data-ttu-id="97047-111">(Çoklu oturum açma) Azure AD hesaplarına sahip</span><span class="sxs-lookup"><span data-stu-id="97047-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="97047-112">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="97047-112">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="97047-113">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="97047-113">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97047-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="97047-114">Prerequisites</span></span>

<span data-ttu-id="97047-115">Azure AD tümleştirme Aha ile yapılandırmak için!, aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="97047-115">To configure Azure AD integration with Aha!, you need the following items:</span></span>

- <span data-ttu-id="97047-116">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="97047-116">An Azure AD subscription</span></span>
- <span data-ttu-id="97047-117">Bir Aha!</span><span class="sxs-lookup"><span data-stu-id="97047-117">An Aha!</span></span> <span data-ttu-id="97047-118">Çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="97047-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="97047-119">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="97047-119">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="97047-120">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="97047-120">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="97047-121">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="97047-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="97047-122">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="97047-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="97047-123">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="97047-123">Scenario description</span></span>
<span data-ttu-id="97047-124">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="97047-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="97047-125">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="97047-125">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="97047-126">AHA ekleme!</span><span class="sxs-lookup"><span data-stu-id="97047-126">Adding Aha!</span></span> <span data-ttu-id="97047-127">Galeriden</span><span class="sxs-lookup"><span data-stu-id="97047-127">from the gallery</span></span>
2. <span data-ttu-id="97047-128">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="97047-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-the-gallery"></a><span data-ttu-id="97047-129">AHA ekleme!</span><span class="sxs-lookup"><span data-stu-id="97047-129">Adding Aha!</span></span> <span data-ttu-id="97047-130">Galeriden</span><span class="sxs-lookup"><span data-stu-id="97047-130">from the gallery</span></span>
<span data-ttu-id="97047-131">Aha tümleştirmesini yapılandırmak için!</span><span class="sxs-lookup"><span data-stu-id="97047-131">To configure the integration of Aha!</span></span> <span data-ttu-id="97047-132">Azure AD ile Aha eklemeniz gerekir!</span><span class="sxs-lookup"><span data-stu-id="97047-132">into Azure AD, you need to add Aha!</span></span> <span data-ttu-id="97047-133">Yönetilen SaaS uygulamaları listenize Galeriden.</span><span class="sxs-lookup"><span data-stu-id="97047-133">from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="97047-134">**AHA eklemek için! Galeriden, aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="97047-134">**To add Aha! from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="97047-135">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="97047-135">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="97047-137">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="97047-137">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="97047-138">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="97047-138">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="97047-140">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="97047-140">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="97047-142">Arama kutusuna **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="97047-142">In the search box, type **Aha!**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="97047-144">Sonuçlar panelinde seçin **Aha!**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="97047-144">In the results panel, select **Aha!**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="97047-146">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="97047-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="97047-147">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Aha ile test etme!</span><span class="sxs-lookup"><span data-stu-id="97047-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="97047-148">"Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="97047-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="97047-149">Tekli çalışmaya oturum için Azure AD Aha ne karşılık gelen kullanıcı bilmesi gerekir!</span><span class="sxs-lookup"><span data-stu-id="97047-149">For single sign-on to work, Azure AD needs to know what the counterpart user in Aha!</span></span> <span data-ttu-id="97047-150">bir kullanıcı için Azure AD içinde değil.</span><span class="sxs-lookup"><span data-stu-id="97047-150">is to a user in Azure AD.</span></span> <span data-ttu-id="97047-151">Diğer bir deyişle, bir bağlantı arasındaki ilişki bir Azure AD kullanıcısının Aha ilgili kullanıcı!</span><span class="sxs-lookup"><span data-stu-id="97047-151">In other words, a link relationship between an Azure AD user and the related user in Aha!</span></span> <span data-ttu-id="97047-152">kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="97047-152">needs to be established.</span></span>

<span data-ttu-id="97047-153">Aha,!, değeri atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="97047-153">In Aha!, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="97047-154">Yapılandırma ve Azure AD çoklu oturum açma Aha ile test!, aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="97047-154">To configure and test Azure AD single sign-on with Aha!, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="97047-155">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="97047-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="97047-156">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="97047-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="97047-157">**[Oluşturma bir Aha! test kullanıcısı](#creating-an-aha-test-user)**  - Aha içinde karşılık gelen Britta Simon biri için!</span><span class="sxs-lookup"><span data-stu-id="97047-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - to have a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="97047-158">Bu kullanıcı Azure AD gösterimini bağlanır.</span><span class="sxs-lookup"><span data-stu-id="97047-158">that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="97047-159">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="97047-159">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="97047-160">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="97047-160">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="97047-161">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="97047-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="97047-162">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirme ve çoklu oturum açma, Aha yapılandırma!</span><span class="sxs-lookup"><span data-stu-id="97047-162">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="97047-163">Uygulama.</span><span class="sxs-lookup"><span data-stu-id="97047-163">application.</span></span>

<span data-ttu-id="97047-164">**Azure AD çoklu oturum açma ile Aha yapılandırmak için!, aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="97047-164">**To configure Azure AD single sign-on with Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="97047-165">Azure portalında üzerinde **Aha!**</span><span class="sxs-lookup"><span data-stu-id="97047-165">In the Azure portal, on the **Aha!**</span></span> <span data-ttu-id="97047-166">Uygulama Tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="97047-166">application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="97047-168">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="97047-168">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="97047-170">Üzerinde **Aha! Etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="97047-170">On the **Aha! Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="97047-172">a.</span><span class="sxs-lookup"><span data-stu-id="97047-172">a.</span></span> <span data-ttu-id="97047-173">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.aha.io/session/new`</span><span class="sxs-lookup"><span data-stu-id="97047-173">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="97047-174">b.</span><span class="sxs-lookup"><span data-stu-id="97047-174">b.</span></span> <span data-ttu-id="97047-175">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.aha.io`</span><span class="sxs-lookup"><span data-stu-id="97047-175">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="97047-176">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="97047-176">These values are not real.</span></span> <span data-ttu-id="97047-177">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="97047-177">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="97047-178">Kişi [Aha! İstemci destek ekibi](https://www.aha.io/company/contact) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="97047-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="97047-179">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="97047-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="97047-181">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="97047-181">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="97047-183">Farklı web tarayıcısı penceresinde, Aha oturum!</span><span class="sxs-lookup"><span data-stu-id="97047-183">In a different web browser window, log in to your Aha!</span></span> <span data-ttu-id="97047-184">Yönetici olarak şirket sitesi.</span><span class="sxs-lookup"><span data-stu-id="97047-184">company site as an administrator.</span></span>

7. <span data-ttu-id="97047-185">Üstteki menüde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="97047-185">In the menu on the top, click **Settings**.</span></span>

    <span data-ttu-id="97047-186">![Ayarları](./media/active-directory-saas-aha-tutorial/IC798950.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="97047-186">![Settings](./media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="97047-187">Tıklatın **hesap**.</span><span class="sxs-lookup"><span data-stu-id="97047-187">Click **Account**.</span></span>
   
    <span data-ttu-id="97047-188">![Profil](./media/active-directory-saas-aha-tutorial/IC798951.png "profili")</span><span class="sxs-lookup"><span data-stu-id="97047-188">![Profile](./media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="97047-189">Tıklatın **güvenlik ve çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="97047-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="97047-190">![Güvenlik ve çoklu oturum açma](./media/active-directory-saas-aha-tutorial/IC798952.png "güvenlik ve çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="97047-190">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="97047-191">İçinde **çoklu oturum açma** bölümünde olarak **kimlik sağlayıcısı**seçin **SAML2.0**.</span><span class="sxs-lookup"><span data-stu-id="97047-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="97047-192">![Güvenlik ve çoklu oturum açma](./media/active-directory-saas-aha-tutorial/IC798953.png "güvenlik ve çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="97047-192">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="97047-193">Üzerinde **çoklu oturum açma** yapılandırma sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="97047-193">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
    
    <span data-ttu-id="97047-194">![Çoklu oturum açma](./media/active-directory-saas-aha-tutorial/IC798954.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="97047-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="97047-195">a.</span><span class="sxs-lookup"><span data-stu-id="97047-195">a.</span></span> <span data-ttu-id="97047-196">İçinde **adı** metin kutusuna, yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="97047-196">In the **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="97047-197">b.</span><span class="sxs-lookup"><span data-stu-id="97047-197">b.</span></span> <span data-ttu-id="97047-198">İçin **kullanarak yapılandırma**seçin **meta veri dosyası**.</span><span class="sxs-lookup"><span data-stu-id="97047-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="97047-199">c.</span><span class="sxs-lookup"><span data-stu-id="97047-199">c.</span></span> <span data-ttu-id="97047-200">İndirilen meta veri dosyanızı karşıya yüklemek için tıklayın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="97047-200">To upload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="97047-201">d.</span><span class="sxs-lookup"><span data-stu-id="97047-201">d.</span></span> <span data-ttu-id="97047-202">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="97047-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="97047-203">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="97047-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="97047-204">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="97047-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="97047-205">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="97047-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="97047-206">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="97047-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="97047-207">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="97047-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="97047-209">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="97047-209">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="97047-210">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="97047-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="97047-212">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="97047-212">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="97047-214">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="97047-214">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="97047-216">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="97047-216">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="97047-218">a.</span><span class="sxs-lookup"><span data-stu-id="97047-218">a.</span></span> <span data-ttu-id="97047-219">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="97047-219">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="97047-220">b.</span><span class="sxs-lookup"><span data-stu-id="97047-220">b.</span></span> <span data-ttu-id="97047-221">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="97047-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="97047-222">c.</span><span class="sxs-lookup"><span data-stu-id="97047-222">c.</span></span> <span data-ttu-id="97047-223">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="97047-223">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="97047-224">d.</span><span class="sxs-lookup"><span data-stu-id="97047-224">d.</span></span> <span data-ttu-id="97047-225">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="97047-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="97047-226">Oluşturma bir Aha!</span><span class="sxs-lookup"><span data-stu-id="97047-226">Creating an Aha!</span></span> <span data-ttu-id="97047-227">Test kullanıcısı</span><span class="sxs-lookup"><span data-stu-id="97047-227">test user</span></span>

<span data-ttu-id="97047-228">Azure AD kullanıcıların AHA için oturum açma!, Aha sağlanmalıdır!.</span><span class="sxs-lookup"><span data-stu-id="97047-228">To enable Azure AD users to log in to Aha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="97047-229">Aha durumunda!, otomatik bir görev olduğundan sağlama.</span><span class="sxs-lookup"><span data-stu-id="97047-229">In the case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="97047-230">Sizin için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="97047-230">There is no action item for you.</span></span>

<span data-ttu-id="97047-231">Kullanıcıları otomatik olarak ilk tek oturum açma girişimi sırasında gerekirse oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="97047-231">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="97047-232">Diğer bir Aha kullanabilirsiniz!</span><span class="sxs-lookup"><span data-stu-id="97047-232">You can use any other Aha!</span></span> <span data-ttu-id="97047-233">kullanıcı hesabı oluşturma araçlarını veya Aha tarafından sağlanan API'leri!</span><span class="sxs-lookup"><span data-stu-id="97047-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="97047-234">AAD kullanıcı hesaplarını sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="97047-234">to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="97047-235">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="97047-235">Assigning the Azure AD test user</span></span>

<span data-ttu-id="97047-236">Bu bölümde, Britta Aha için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirmek!.</span><span class="sxs-lookup"><span data-stu-id="97047-236">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Aha!.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="97047-238">**İçin Aha Britta Simon atamak!, aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="97047-238">**To assign Britta Simon to Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="97047-239">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="97047-239">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="97047-241">Uygulamalar listesinde **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="97047-241">In the applications list, select **Aha!**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="97047-243">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="97047-243">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="97047-245">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="97047-245">Click **Add** button.</span></span> <span data-ttu-id="97047-246">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="97047-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="97047-248">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="97047-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="97047-249">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="97047-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="97047-250">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="97047-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="97047-251">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="97047-251">Testing single sign-on</span></span>

<span data-ttu-id="97047-252">Çoklu oturum açma ayarlarınızı test etmek isterseniz, erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="97047-252">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="97047-253">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="97047-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="97047-254">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="97047-254">Additional resources</span></span>

* [<span data-ttu-id="97047-255">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="97047-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="97047-256">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="97047-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

