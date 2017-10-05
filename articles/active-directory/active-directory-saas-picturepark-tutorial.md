---
title: "Öğretici: Azure Active Directory Tümleştirme ile Picturepark | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Picturepark arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 1c009aa1fdd3140a4466cf762b6c9687e74ce4c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="ded80-103">Öğretici: Azure Active Directory Tümleştirme Picturepark ile</span><span class="sxs-lookup"><span data-stu-id="ded80-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="ded80-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Picturepark tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ded80-104">In this tutorial, you learn how to integrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ded80-105">Picturepark Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="ded80-105">Integrating Picturepark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ded80-106">Picturepark erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ded80-106">You can control in Azure AD who has access to Picturepark</span></span>
- <span data-ttu-id="ded80-107">Otomatik olarak için Picturepark (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ded80-107">You can enable your users to automatically get signed-on to Picturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ded80-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="ded80-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ded80-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ded80-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ded80-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ded80-110">Prerequisites</span></span>

<span data-ttu-id="ded80-111">Azure AD tümleştirme Picturepark ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="ded80-111">To configure Azure AD integration with Picturepark, you need the following items:</span></span>

- <span data-ttu-id="ded80-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="ded80-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ded80-113">Bir Picturepark çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="ded80-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ded80-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="ded80-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ded80-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ded80-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ded80-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="ded80-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ded80-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ded80-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ded80-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="ded80-118">Scenario description</span></span>
<span data-ttu-id="ded80-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="ded80-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ded80-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="ded80-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ded80-121">Galeriden Picturepark ekleme</span><span class="sxs-lookup"><span data-stu-id="ded80-121">Adding Picturepark from the gallery</span></span>
2. <span data-ttu-id="ded80-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ded80-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-the-gallery"></a><span data-ttu-id="ded80-123">Galeriden Picturepark ekleme</span><span class="sxs-lookup"><span data-stu-id="ded80-123">Adding Picturepark from the gallery</span></span>
<span data-ttu-id="ded80-124">Azure AD Picturepark tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Picturepark eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ded80-124">To configure the integration of Picturepark into Azure AD, you need to add Picturepark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ded80-125">**Galeriden Picturepark eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ded80-125">**To add Picturepark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ded80-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ded80-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ded80-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="ded80-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ded80-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ded80-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="ded80-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ded80-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="ded80-133">Arama kutusuna **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="ded80-133">In the search box, type **Picturepark**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="ded80-135">Sonuçlar panelinde seçin **Picturepark**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ded80-135">In the results panel, select **Picturepark**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ded80-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ded80-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ded80-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Picturepark sınayın.</span><span class="sxs-lookup"><span data-stu-id="ded80-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ded80-139">Tekli çalışmaya oturum için Azure AD Picturepark karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="ded80-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Picturepark is to a user in Azure AD.</span></span> <span data-ttu-id="ded80-140">Diğer bir deyişle, bir Azure AD kullanıcısının Picturepark ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ded80-140">In other words, a link relationship between an Azure AD user and the related user in Picturepark needs to be established.</span></span>

<span data-ttu-id="ded80-141">Picturepark içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="ded80-141">In Picturepark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ded80-142">Yapılandırma ve Azure AD çoklu oturum açma Picturepark ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ded80-142">To configure and test Azure AD single sign-on with Picturepark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ded80-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ded80-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ded80-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="ded80-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ded80-145">**[Picturepark test kullanıcısı oluşturma](#creating-a-picturepark-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Picturepark sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="ded80-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - to have a counterpart of Britta Simon in Picturepark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ded80-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ded80-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ded80-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ded80-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ded80-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ded80-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ded80-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Picturepark uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ded80-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="ded80-150">**Azure AD çoklu oturum açma ile Picturepark yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ded80-150">**To configure Azure AD single sign-on with Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="ded80-151">Azure portalında üzerinde **Picturepark** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="ded80-151">In the Azure portal, on the **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="ded80-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ded80-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="ded80-155">Üzerinde **Picturepark etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ded80-155">On the **Picturepark Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="ded80-157">a.</span><span class="sxs-lookup"><span data-stu-id="ded80-157">a.</span></span> <span data-ttu-id="ded80-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.picturepark.com`</span><span class="sxs-lookup"><span data-stu-id="ded80-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="ded80-159">b.</span><span class="sxs-lookup"><span data-stu-id="ded80-159">b.</span></span> <span data-ttu-id="ded80-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="ded80-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="ded80-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="ded80-161">These values are not real.</span></span> <span data-ttu-id="ded80-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ded80-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ded80-163">Kişi [Picturepark istemci destek ekibi](https://picturepark.com/about/contact/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="ded80-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="ded80-164">Üzerinde **SAML imzalama sertifikası** bölümünde, kopyalama **parmak İZİ** sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="ded80-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="ded80-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ded80-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ded80-168">Üzerinde **Picturepark yapılandırma** 'yi tıklatın **yapılandırma Picturepark** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="ded80-168">On the **Picturepark Configuration** section, click **Configure Picturepark** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ded80-169">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="ded80-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="ded80-171">Farklı web tarayıcısı penceresinde Picturepark şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ded80-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="ded80-172">Üstteki araç çubuğunda tıklatın **Yönetimsel Araçlar**ve ardından **Yönetim Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="ded80-172">In the toolbar on the top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="ded80-173">![Yönetim Konsolu](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Yönetim Konsolu")</span><span class="sxs-lookup"><span data-stu-id="ded80-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="ded80-174">Tıklatın **kimlik doğrulaması**ve ardından **kimlik sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="ded80-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="ded80-175">![Kimlik doğrulama](./media/active-directory-saas-picturepark-tutorial/ic795063.png "kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="ded80-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="ded80-176">İçinde **kimlik sağlayıcı Yapılandırması** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ded80-176">In the **Identity provider configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="ded80-177">![Kimlik sağlayıcısı Yapılandırması](./media/active-directory-saas-picturepark-tutorial/ic795064.png "kimlik sağlayıcı yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="ded80-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="ded80-178">a.</span><span class="sxs-lookup"><span data-stu-id="ded80-178">a.</span></span> <span data-ttu-id="ded80-179">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ded80-179">Click **Add**.</span></span>
  
    <span data-ttu-id="ded80-180">b.</span><span class="sxs-lookup"><span data-stu-id="ded80-180">b.</span></span> <span data-ttu-id="ded80-181">Yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="ded80-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="ded80-182">c.</span><span class="sxs-lookup"><span data-stu-id="ded80-182">c.</span></span> <span data-ttu-id="ded80-183">Seçin **varsayılan olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="ded80-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="ded80-184">d.</span><span class="sxs-lookup"><span data-stu-id="ded80-184">d.</span></span> <span data-ttu-id="ded80-185">İçinde **veren URI** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="ded80-185">In **Issuer URI** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="ded80-186">e.</span><span class="sxs-lookup"><span data-stu-id="ded80-186">e.</span></span> <span data-ttu-id="ded80-187">İçinde **güvenilir verenin parmak iziyle** metin değerini yapıştırın **parmak izi** kopyalanan **SAML imzalama sertifikası** bölümü.</span><span class="sxs-lookup"><span data-stu-id="ded80-187">In **Trusted Issuer Thumb Print** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="ded80-188">Tıklatın **JoinDefaultUsersGroup**.</span><span class="sxs-lookup"><span data-stu-id="ded80-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="ded80-189">Ayarlamak için **Emailaddress** özniteliğini **talep** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="ded80-189">To set the **Emailaddress** attribute in the **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="ded80-190">![Yapılandırma](./media/active-directory-saas-picturepark-tutorial/ic795065.png "yapılandırma")</span><span class="sxs-lookup"><span data-stu-id="ded80-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="ded80-191">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="ded80-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ded80-192">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="ded80-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ded80-193">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ded80-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ded80-194">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ded80-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="ded80-195">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="ded80-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="ded80-197">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ded80-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ded80-198">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ded80-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ded80-200">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="ded80-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ded80-202">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="ded80-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ded80-204">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ded80-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ded80-206">a.</span><span class="sxs-lookup"><span data-stu-id="ded80-206">a.</span></span> <span data-ttu-id="ded80-207">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ded80-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ded80-208">b.</span><span class="sxs-lookup"><span data-stu-id="ded80-208">b.</span></span> <span data-ttu-id="ded80-209">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="ded80-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ded80-210">c.</span><span class="sxs-lookup"><span data-stu-id="ded80-210">c.</span></span> <span data-ttu-id="ded80-211">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="ded80-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ded80-212">d.</span><span class="sxs-lookup"><span data-stu-id="ded80-212">d.</span></span> <span data-ttu-id="ded80-213">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ded80-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="ded80-214">Picturepark test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ded80-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="ded80-215">Azure AD kullanıcıların Picturepark oturum etkinleştirmek için bunların Picturepark sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ded80-215">In order to enable Azure AD users to log into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="ded80-216">Picturepark söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="ded80-216">In the case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="ded80-217">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ded80-217">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="ded80-218">Oturum, **Picturepark** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="ded80-218">Log in to your **Picturepark** tenant.</span></span>

2. <span data-ttu-id="ded80-219">Üstteki araç çubuğunda tıklatın **Yönetimsel Araçlar**ve ardından **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="ded80-219">In the toolbar on the top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="ded80-220">![Kullanıcıların](./media/active-directory-saas-picturepark-tutorial/ic795067.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="ded80-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="ded80-221">İçinde **kullanıcılara genel bakış** sekmesini tıklatın, **yeni**.</span><span class="sxs-lookup"><span data-stu-id="ded80-221">In the **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="ded80-222">![Kullanıcı Yönetimi](./media/active-directory-saas-picturepark-tutorial/ic795068.png "kullanıcı yönetimi")</span><span class="sxs-lookup"><span data-stu-id="ded80-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="ded80-223">Üzerinde **kullanıcı oluştur** iletişim kutusunda, geçerli bir Azure Active Directory istediğiniz kullanıcı sağlamak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ded80-223">On the **Create User** dialog, perform the following steps of a valid Azure Active Directory User you want to provision:</span></span>
   
    <span data-ttu-id="ded80-224">![Kullanıcı oluşturma](./media/active-directory-saas-picturepark-tutorial/ic795069.png "kullanıcı oluştur")</span><span class="sxs-lookup"><span data-stu-id="ded80-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="ded80-225">a.</span><span class="sxs-lookup"><span data-stu-id="ded80-225">a.</span></span> <span data-ttu-id="ded80-226">İçinde **e-posta adresi** metin kutusuna, türü **e-posta adresi** kullanıcının  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="ded80-226">In the **Email Address** textbox, type the **email address** of the user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="ded80-227">b.</span><span class="sxs-lookup"><span data-stu-id="ded80-227">b.</span></span> <span data-ttu-id="ded80-228">İçinde **parola** ve **parolayı onayla** metin kutuları, türü **parola** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="ded80-228">In the **Password** and **Confirm Password** textboxes, type the **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="ded80-229">c.</span><span class="sxs-lookup"><span data-stu-id="ded80-229">c.</span></span> <span data-ttu-id="ded80-230">İçinde **ad** metin kutusuna, türü **ad** kullanıcının **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ded80-230">In the **First Name** textbox, type the **First Name** of the user **Britta**.</span></span> 
   
    <span data-ttu-id="ded80-231">d.</span><span class="sxs-lookup"><span data-stu-id="ded80-231">d.</span></span> <span data-ttu-id="ded80-232">İçinde **Soyadı** metin kutusuna, türü **Soyadı** kullanıcının **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ded80-232">In the **Last Name** textbox, type the **Last Name** of the user **Simon**.</span></span>
   
    <span data-ttu-id="ded80-233">e.</span><span class="sxs-lookup"><span data-stu-id="ded80-233">e.</span></span> <span data-ttu-id="ded80-234">İçinde **şirket** metin kutusuna, türü **şirket adı** kullanıcının.</span><span class="sxs-lookup"><span data-stu-id="ded80-234">In the **Company** textbox, type the **Company name** of the user.</span></span> 
   
    <span data-ttu-id="ded80-235">f.</span><span class="sxs-lookup"><span data-stu-id="ded80-235">f.</span></span> <span data-ttu-id="ded80-236">İçinde **Ülke** metin kutusuna, select **Ülke** kullanıcının.</span><span class="sxs-lookup"><span data-stu-id="ded80-236">In the **Country** textbox, select the **Country** of the user.</span></span>
  
    <span data-ttu-id="ded80-237">g.</span><span class="sxs-lookup"><span data-stu-id="ded80-237">g.</span></span> <span data-ttu-id="ded80-238">İçinde **ZIP** metin kutusuna, türü **posta kodu** şehrin.</span><span class="sxs-lookup"><span data-stu-id="ded80-238">In the **ZIP** textbox, type the **ZIP code** of the city.</span></span>
   
    <span data-ttu-id="ded80-239">h.</span><span class="sxs-lookup"><span data-stu-id="ded80-239">h.</span></span> <span data-ttu-id="ded80-240">İçinde **Şehir** metin kutusuna, türü **şehir adı** kullanıcının.</span><span class="sxs-lookup"><span data-stu-id="ded80-240">In the **City** textbox, type the **City name** of the user.</span></span>

    <span data-ttu-id="ded80-241">ı.</span><span class="sxs-lookup"><span data-stu-id="ded80-241">i.</span></span> <span data-ttu-id="ded80-242">Seçin bir **dil**.</span><span class="sxs-lookup"><span data-stu-id="ded80-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="ded80-243">j.</span><span class="sxs-lookup"><span data-stu-id="ded80-243">j.</span></span> <span data-ttu-id="ded80-244">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ded80-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="ded80-245">API Azure AD kullanıcı hesaplarını sağlamak için Picturepark tarafından sağlanan veya herhangi diğer Picturepark kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ded80-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ded80-246">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="ded80-246">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ded80-247">Bu bölümde, Britta Picturepark için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ded80-247">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Picturepark.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="ded80-249">**Picturepark için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ded80-249">**To assign Britta Simon to Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="ded80-250">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ded80-250">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="ded80-252">Uygulamalar listesinde **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="ded80-252">In the applications list, select **Picturepark**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="ded80-254">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="ded80-254">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="ded80-256">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ded80-256">Click **Add** button.</span></span> <span data-ttu-id="ded80-257">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ded80-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="ded80-259">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="ded80-259">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ded80-260">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ded80-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ded80-261">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ded80-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ded80-262">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="ded80-262">Testing single sign-on</span></span>

<span data-ttu-id="ded80-263">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="ded80-263">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ded80-264">Erişim paneli Picturepark parçasında tıklattığınızda, otomatik olarak Picturepark uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="ded80-264">When you click the Picturepark tile in the Access Panel, you should get automatically signed-on to your Picturepark application.</span></span> <span data-ttu-id="ded80-265">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ded80-265">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ded80-266">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ded80-266">Additional resources</span></span>

* [<span data-ttu-id="ded80-267">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="ded80-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ded80-268">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="ded80-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

