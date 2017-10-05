---
title: "Öğretici: Azure Active Directory Tümleştirme ile QuickHelp | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile QuickHelp arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 1c72b0ddee636090129dab7a5c7ec6ffd452434a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a><span data-ttu-id="014eb-103">Öğretici: Azure Active Directory Tümleştirme QuickHelp ile</span><span class="sxs-lookup"><span data-stu-id="014eb-103">Tutorial: Azure Active Directory integration with QuickHelp</span></span>

<span data-ttu-id="014eb-104">Bu öğreticide, Azure Active Directory (Azure AD) ile QuickHelp tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="014eb-104">In this tutorial, you learn how to integrate QuickHelp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="014eb-105">QuickHelp Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="014eb-105">Integrating QuickHelp with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="014eb-106">QuickHelp erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="014eb-106">You can control in Azure AD who has access to QuickHelp</span></span>
- <span data-ttu-id="014eb-107">Otomatik olarak için QuickHelp (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="014eb-107">You can enable your users to automatically get signed-on to QuickHelp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="014eb-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="014eb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="014eb-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="014eb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="014eb-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="014eb-110">Prerequisites</span></span>

<span data-ttu-id="014eb-111">Azure AD tümleştirme QuickHelp ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="014eb-111">To configure Azure AD integration with QuickHelp, you need the following items:</span></span>

- <span data-ttu-id="014eb-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="014eb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="014eb-113">Bir QuickHelp çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="014eb-113">A QuickHelp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="014eb-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="014eb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="014eb-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="014eb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="014eb-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="014eb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="014eb-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="014eb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="014eb-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="014eb-118">Scenario description</span></span>
<span data-ttu-id="014eb-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="014eb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="014eb-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="014eb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="014eb-121">Galeriden QuickHelp ekleme</span><span class="sxs-lookup"><span data-stu-id="014eb-121">Adding QuickHelp from the gallery</span></span>
2. <span data-ttu-id="014eb-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="014eb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-quickhelp-from-the-gallery"></a><span data-ttu-id="014eb-123">Galeriden QuickHelp ekleme</span><span class="sxs-lookup"><span data-stu-id="014eb-123">Adding QuickHelp from the gallery</span></span>
<span data-ttu-id="014eb-124">Azure AD QuickHelp tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden QuickHelp eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="014eb-124">To configure the integration of QuickHelp into Azure AD, you need to add QuickHelp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="014eb-125">**Galeriden QuickHelp eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="014eb-125">**To add QuickHelp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="014eb-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="014eb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="014eb-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="014eb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="014eb-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="014eb-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="014eb-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="014eb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="014eb-133">Arama kutusuna **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="014eb-133">In the search box, type **QuickHelp**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_search.png)

5. <span data-ttu-id="014eb-135">Sonuçlar panelinde seçin **QuickHelp**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="014eb-135">In the results panel, select **QuickHelp**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="014eb-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="014eb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="014eb-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı QuickHelp sınayın.</span><span class="sxs-lookup"><span data-stu-id="014eb-138">In this section, you configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="014eb-139">Tekli çalışmaya oturum için Azure AD QuickHelp karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="014eb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp is to a user in Azure AD.</span></span> <span data-ttu-id="014eb-140">Diğer bir deyişle, bir Azure AD kullanıcısının QuickHelp ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="014eb-140">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="014eb-141">QuickHelp içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="014eb-141">In QuickHelp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="014eb-142">Yapılandırma ve Azure AD çoklu oturum açma QuickHelp ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="014eb-142">To configure and test Azure AD single sign-on with QuickHelp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="014eb-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="014eb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="014eb-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="014eb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="014eb-145">**[QuickHelp test kullanıcısı oluşturma](#creating-a-quickhelp-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı QuickHelp sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="014eb-145">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - to have a counterpart of Britta Simon in QuickHelp that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="014eb-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="014eb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="014eb-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="014eb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="014eb-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="014eb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="014eb-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma QuickHelp uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="014eb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your QuickHelp application.</span></span>

<span data-ttu-id="014eb-150">**Azure AD çoklu oturum açma ile QuickHelp yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="014eb-150">**To configure Azure AD single sign-on with QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="014eb-151">Azure portalında üzerinde **QuickHelp** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="014eb-151">In the Azure portal, on the **QuickHelp** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="014eb-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="014eb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

3. <span data-ttu-id="014eb-155">Üzerinde **QuickHelp etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="014eb-155">On the **QuickHelp Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_url.png)

    <span data-ttu-id="014eb-157">a.</span><span class="sxs-lookup"><span data-stu-id="014eb-157">a.</span></span> <span data-ttu-id="014eb-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://quickhelp.com/<instancename>/#/Login`</span><span class="sxs-lookup"><span data-stu-id="014eb-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://quickhelp.com/<instancename>/#/Login`</span></span>

    <span data-ttu-id="014eb-159">b.</span><span class="sxs-lookup"><span data-stu-id="014eb-159">b.</span></span> <span data-ttu-id="014eb-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.quickhelp.com`</span><span class="sxs-lookup"><span data-stu-id="014eb-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.quickhelp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="014eb-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="014eb-161">These values are not real.</span></span> <span data-ttu-id="014eb-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="014eb-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="014eb-163">Kişi [QuickHelp istemci destek ekibi](https://support.quickhelp.com/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="014eb-163">Contact [QuickHelp Client support team](https://support.quickhelp.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="014eb-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="014eb-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

5. <span data-ttu-id="014eb-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="014eb-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-quickhelp-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="014eb-168">QuickHelp şirket sitenize yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="014eb-168">Sign-on to your QuickHelp company site as administrator.</span></span>

7. <span data-ttu-id="014eb-169">Üstteki menüde tıklatın **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="014eb-169">In the menu on the top, click **Admin**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][21]

8. <span data-ttu-id="014eb-171">İçinde **QuickHelp yönetici** menüsünde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="014eb-171">In the **QuickHelp Admin** menu, click **Settings**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][22]

9. <span data-ttu-id="014eb-173">Tıklatın **kimlik doğrulama ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="014eb-173">Click **Authentication Settings**.</span></span>

10. <span data-ttu-id="014eb-174">Üzerinde **kimlik doğrulama ayarlarını** sayfasında, aşağıdaki adımları uygulayın</span><span class="sxs-lookup"><span data-stu-id="014eb-174">On the **Authentication Settings** page, perform the following steps</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][23]
   
    <span data-ttu-id="014eb-176">a.</span><span class="sxs-lookup"><span data-stu-id="014eb-176">a.</span></span> <span data-ttu-id="014eb-177">Olarak **SSO türü**seçin **WSFederation**.</span><span class="sxs-lookup"><span data-stu-id="014eb-177">As **SSO Type**, select **WSFederation**.</span></span>
   
    <span data-ttu-id="014eb-178">b.</span><span class="sxs-lookup"><span data-stu-id="014eb-178">b.</span></span> <span data-ttu-id="014eb-179">İndirilen Azure meta veri dosyanızı karşıya yüklemek için tıklayın **Gözat**, dosyasına gidin, end'ye tıklayın **meta veriler karşıya**.</span><span class="sxs-lookup"><span data-stu-id="014eb-179">To upload your downloaded Azure metadata file, click **Browse**, navigate to the file, end then click **Upload Metadata**.</span></span>
   
    <span data-ttu-id="014eb-180">c.</span><span class="sxs-lookup"><span data-stu-id="014eb-180">c.</span></span> <span data-ttu-id="014eb-181">İçinde **e-posta** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="014eb-181">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
   
    <span data-ttu-id="014eb-182">d.</span><span class="sxs-lookup"><span data-stu-id="014eb-182">d.</span></span> <span data-ttu-id="014eb-183">İçinde **ad** metin kutusuna, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="014eb-183">In the **First Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
   
    <span data-ttu-id="014eb-184">e.</span><span class="sxs-lookup"><span data-stu-id="014eb-184">e.</span></span> <span data-ttu-id="014eb-185">İçinde **Soyadı** metin kutusuna, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="014eb-185">In the **Last Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
   
    <span data-ttu-id="014eb-186">f.</span><span class="sxs-lookup"><span data-stu-id="014eb-186">f.</span></span> <span data-ttu-id="014eb-187">İçinde **Eylem çubuğu**, tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="014eb-187">In the **Action Bar**, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="014eb-188">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="014eb-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="014eb-189">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="014eb-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="014eb-190">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="014eb-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="014eb-191">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="014eb-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="014eb-192">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="014eb-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="014eb-194">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="014eb-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="014eb-195">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="014eb-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="014eb-197">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="014eb-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="014eb-199">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="014eb-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="014eb-201">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="014eb-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="014eb-203">a.</span><span class="sxs-lookup"><span data-stu-id="014eb-203">a.</span></span> <span data-ttu-id="014eb-204">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="014eb-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="014eb-205">b.</span><span class="sxs-lookup"><span data-stu-id="014eb-205">b.</span></span> <span data-ttu-id="014eb-206">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="014eb-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="014eb-207">c.</span><span class="sxs-lookup"><span data-stu-id="014eb-207">c.</span></span> <span data-ttu-id="014eb-208">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="014eb-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="014eb-209">d.</span><span class="sxs-lookup"><span data-stu-id="014eb-209">d.</span></span> <span data-ttu-id="014eb-210">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="014eb-210">Click **Create**.</span></span>
 
### <a name="creating-a-quickhelp-test-user"></a><span data-ttu-id="014eb-211">QuickHelp test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="014eb-211">Creating a QuickHelp test user</span></span>

<span data-ttu-id="014eb-212">Bu bölümün amacı Britta Simon içinde QuickHelp adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="014eb-212">The objective of this section is to create a user called Britta Simon in QuickHelp.</span></span>
<span data-ttu-id="014eb-213">Tekli çalışmaya oturum için Azure AD ne QuickHelp Azure AD'de bir kullanıcıya karşılık gelen kullanıcı olduğunu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="014eb-213">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp to a user in Azure AD is.</span></span> <span data-ttu-id="014eb-214">Diğer bir deyişle, bir Azure AD kullanıcısının QuickHelp ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="014eb-214">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="014eb-215">Yalnızca zaman sağlama QuickHelp destekler.</span><span class="sxs-lookup"><span data-stu-id="014eb-215">QuickHelp supports just-in-time provisioning.</span></span> <span data-ttu-id="014eb-216">Bunun anlamı, gerekirse, bir kullanıcı hesabı QuickHelp içinde otomatik olarak oluşturulan ve hesap Azure AD hesabına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="014eb-216">This means, if necessary, a user account is automatically created in QuickHelp and the account is linked to the Azure AD account.</span></span>

<span data-ttu-id="014eb-217">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="014eb-217">There is no action item for you in this section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="014eb-218">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="014eb-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="014eb-219">Bu bölümde, Britta QuickHelp için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="014eb-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to QuickHelp.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="014eb-221">**QuickHelp için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="014eb-221">**To assign Britta Simon to QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="014eb-222">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="014eb-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="014eb-224">Uygulamalar listesinde **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="014eb-224">In the applications list, select **QuickHelp**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_app.png) 

3. <span data-ttu-id="014eb-226">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="014eb-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="014eb-228">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="014eb-228">Click **Add** button.</span></span> <span data-ttu-id="014eb-229">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="014eb-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="014eb-231">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="014eb-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="014eb-232">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="014eb-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="014eb-233">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="014eb-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="014eb-234">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="014eb-234">Testing single sign-on</span></span>

<span data-ttu-id="014eb-235">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="014eb-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="014eb-236">Erişim paneli QuickHelp parçasında tıklattığınızda, otomatik olarak QuickHelp uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="014eb-236">When you click the QuickHelp tile in the Access Panel, you should get automatically signed-on to your QuickHelp application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="014eb-237">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="014eb-237">Additional resources</span></span>

* [<span data-ttu-id="014eb-238">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="014eb-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="014eb-239">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="014eb-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_07.png
