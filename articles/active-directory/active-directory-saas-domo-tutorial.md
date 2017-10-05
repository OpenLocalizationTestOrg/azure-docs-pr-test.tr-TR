---
title: "Öğretici: Azure Active Directory Tümleştirme ile Domo | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Domo arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 058626e4-73b3-4dc2-86ca-b060d002d70a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: 919d2262cf9f14159a13370037301005b5b69da2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-domo"></a><span data-ttu-id="2f4b0-103">Öğretici: Azure Active Directory Tümleştirme Domo ile</span><span class="sxs-lookup"><span data-stu-id="2f4b0-103">Tutorial: Azure Active Directory integration with Domo</span></span>

<span data-ttu-id="2f4b0-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Domo tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-104">In this tutorial, you learn how to integrate Domo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f4b0-105">Domo Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-105">Integrating Domo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2f4b0-106">Domo erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2f4b0-106">You can control in Azure AD who has access to Domo</span></span>
- <span data-ttu-id="2f4b0-107">Otomatik olarak için Domo (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2f4b0-107">You can enable your users to automatically get signed-on to Domo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2f4b0-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="2f4b0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2f4b0-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2f4b0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f4b0-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2f4b0-110">Prerequisites</span></span>

<span data-ttu-id="2f4b0-111">Azure AD tümleştirme Domo ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-111">To configure Azure AD integration with Domo, you need the following items:</span></span>

- <span data-ttu-id="2f4b0-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="2f4b0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f4b0-113">Bir Domo çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="2f4b0-113">A Domo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2f4b0-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2f4b0-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f4b0-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2f4b0-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f4b0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f4b0-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="2f4b0-118">Scenario description</span></span>
<span data-ttu-id="2f4b0-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2f4b0-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2f4b0-121">Galeriden Domo ekleme</span><span class="sxs-lookup"><span data-stu-id="2f4b0-121">Adding Domo from the gallery</span></span>
2. <span data-ttu-id="2f4b0-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2f4b0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-domo-from-the-gallery"></a><span data-ttu-id="2f4b0-123">Galeriden Domo ekleme</span><span class="sxs-lookup"><span data-stu-id="2f4b0-123">Adding Domo from the gallery</span></span>
<span data-ttu-id="2f4b0-124">Azure AD Domo tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Domo eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-124">To configure the integration of Domo into Azure AD, you need to add Domo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2f4b0-125">**Galeriden Domo eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2f4b0-125">**To add Domo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2f4b0-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2f4b0-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2f4b0-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="2f4b0-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="2f4b0-133">Arama kutusuna **Domo**.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-133">In the search box, type **Domo**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-domo-tutorial/tutorial_domo_search.png)

5. <span data-ttu-id="2f4b0-135">Sonuçlar panelinde seçin **Domo**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-135">In the results panel, select **Domo**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-domo-tutorial/tutorial_domo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2f4b0-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2f4b0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2f4b0-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Domo ile test etme</span><span class="sxs-lookup"><span data-stu-id="2f4b0-138">In this section, you configure and test Azure AD single sign-on with Domo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2f4b0-139">Tekli çalışmaya oturum için Azure AD Domo karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Domo is to a user in Azure AD.</span></span> <span data-ttu-id="2f4b0-140">Diğer bir deyişle, bir Azure AD kullanıcısının Domo ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-140">In other words, a link relationship between an Azure AD user and the related user in Domo needs to be established.</span></span>

<span data-ttu-id="2f4b0-141">Domo içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-141">In Domo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2f4b0-142">Yapılandırma ve Azure AD çoklu oturum açma Domo ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-142">To configure and test Azure AD single sign-on with Domo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2f4b0-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2f4b0-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2f4b0-145">**[Domo test kullanıcısı oluşturma](#creating-a-domo-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Domo sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-145">**[Creating a Domo test user](#creating-a-domo-test-user)** - to have a counterpart of Britta Simon in Domo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2f4b0-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2f4b0-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2f4b0-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2f4b0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2f4b0-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Domo uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Domo application.</span></span>

<span data-ttu-id="2f4b0-150">**Azure AD çoklu oturum açma ile Domo yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2f4b0-150">**To configure Azure AD single sign-on with Domo, perform the following steps:**</span></span>

1. <span data-ttu-id="2f4b0-151">Azure portalında üzerinde **Domo** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-151">In the Azure portal, on the **Domo** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="2f4b0-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-domo-tutorial/tutorial_domo_samlbase.png)

3. <span data-ttu-id="2f4b0-155">Üzerinde **Domo etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-155">On the **Domo Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-domo-tutorial/tutorial_domo_url.png)

    <span data-ttu-id="2f4b0-157">a.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-157">a.</span></span> <span data-ttu-id="2f4b0-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.domo.com`</span><span class="sxs-lookup"><span data-stu-id="2f4b0-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.domo.com`</span></span>

    <span data-ttu-id="2f4b0-159">b.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-159">b.</span></span> <span data-ttu-id="2f4b0-160">İçinde **tanımlayıcısı** metin kutusuna, aşağıdaki desenleri kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span>     

    | |
    |--|    
    | `https://<companyname>.domo.com` |
    | `https://<companyname>.beta.domo.com` |
    | `https://<companyname>.demo.domo.com` |
    | `https://<companyname>.dev.domo.com` | 
    | `https://<companyname>.fastage1.domo.com` |       
    | `https://<companyname>.frdev.domo.com` |       
    | `https://<companyname>.gastage.domo.com` |       
    | `https://<companyname>.load.domo.com` |       
    | `https://<companyname>.local.domo.com` |       
    | `https://<companyname>.qa.domo.com` |
    | `https://<companyname>.stage.domo.com` |
    
    > [!NOTE] 
    > <span data-ttu-id="2f4b0-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-161">These values are not real.</span></span> <span data-ttu-id="2f4b0-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2f4b0-163">Kişi [Domo istemci destek ekibi](mailto:support@domo.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-163">Contact [Domo Client support team](mailto:support@domo.com) to get these values.</span></span>

4. <span data-ttu-id="2f4b0-164">Domo uygulaması SAML onaylar belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-164">Domo application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="2f4b0-165">Bu uygulama için aşağıdaki talep yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-165">Configure the following claims for this application.</span></span> <span data-ttu-id="2f4b0-166">Bu öznitelik değerlerini yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="2f4b0-167">Aşağıdaki ekran görüntüsünde, bu yapılandırma için bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-167">The following screenshot shows an example for this configuration.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-domo-tutorial/tutorial_domo_attributes.png)
    
5. <span data-ttu-id="2f4b0-169">İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği görüntüde gösterildiği gibi yapılandırın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="2f4b0-170">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="2f4b0-170">Attribute Name</span></span> | <span data-ttu-id="2f4b0-171">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="2f4b0-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="2f4b0-172">ad</span><span class="sxs-lookup"><span data-stu-id="2f4b0-172">name</span></span> | <span data-ttu-id="2f4b0-173">User.DisplayName</span><span class="sxs-lookup"><span data-stu-id="2f4b0-173">user.displayname</span></span> |
    | <span data-ttu-id="2f4b0-174">E-posta</span><span class="sxs-lookup"><span data-stu-id="2f4b0-174">email</span></span> | <span data-ttu-id="2f4b0-175">User.Mail</span><span class="sxs-lookup"><span data-stu-id="2f4b0-175">user.mail</span></span> |
    
    <span data-ttu-id="2f4b0-176">a.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-176">a.</span></span> <span data-ttu-id="2f4b0-177">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-domo-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-domo-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="2f4b0-180">b.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-180">b.</span></span> <span data-ttu-id="2f4b0-181">İçinde **adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="2f4b0-182">c.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-182">c.</span></span> <span data-ttu-id="2f4b0-183">Gelen **değeri** listesinde, ilgili satır için gösterilen öznitelik değeri yazın.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="2f4b0-184">d.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-184">d.</span></span> <span data-ttu-id="2f4b0-185">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-185">Click **Ok**.</span></span> 
 
6. <span data-ttu-id="2f4b0-186">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-186">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-domo-tutorial/tutorial_domo_certificate.png) 

7. <span data-ttu-id="2f4b0-188">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-188">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-domo-tutorial/tutorial_general_400.png)


8. <span data-ttu-id="2f4b0-190">Üzerinde **Domo yapılandırma** 'yi tıklatın **yapılandırma Domo** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-190">On the **Domo Configuration** section, click **Configure Domo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2f4b0-191">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="2f4b0-191">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>   

   ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-domo-tutorial/tutorial_domo_configure.png) 

9. <span data-ttu-id="2f4b0-193">Çoklu oturum açma yapılandırmak için **Domo** yan, indirilen göndermek için ihtiyacınız **sertifika**, **SAML varlık kimliği**, **SAML çoklu oturum açma hizmet URL'si** ve **Sign-Out URL** için [Domo destek ekibi](mailto:support@domo.com).</span><span class="sxs-lookup"><span data-stu-id="2f4b0-193">To configure single sign-on on **Domo** side, you need to send the downloaded **Certificate**, **SAML Entity ID**, the **SAML Single Sign-On Service URL** and the **Sign-Out URL** to [Domo support team](mailto:support@domo.com).</span></span> <span data-ttu-id="2f4b0-194">Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-194">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="2f4b0-195">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="2f4b0-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2f4b0-196">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2f4b0-197">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2f4b0-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2f4b0-198">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2f4b0-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="2f4b0-199">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="2f4b0-201">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2f4b0-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2f4b0-202">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-domo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2f4b0-204">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-domo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2f4b0-206">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-domo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2f4b0-208">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-domo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2f4b0-210">a.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-210">a.</span></span> <span data-ttu-id="2f4b0-211">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2f4b0-212">b.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-212">b.</span></span> <span data-ttu-id="2f4b0-213">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2f4b0-214">c.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-214">c.</span></span> <span data-ttu-id="2f4b0-215">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2f4b0-216">d.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-216">d.</span></span> <span data-ttu-id="2f4b0-217">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-217">Click **Create**.</span></span>
 
### <a name="creating-a-domo-test-user"></a><span data-ttu-id="2f4b0-218">Domo test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2f4b0-218">Creating a Domo test user</span></span>

<span data-ttu-id="2f4b0-219">Bu bölümün amacı Britta Simon içinde Domo adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-219">The objective of this section is to create a user called Britta Simon in Domo.</span></span> <span data-ttu-id="2f4b0-220">Domo yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-220">Domo supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="2f4b0-221">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-221">There is no action item for you in this section.</span></span> <span data-ttu-id="2f4b0-222">Yeni bir kullanıcı henüz yoksa Domo erişme denemesi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-222">A new user is created during an attempt to access Domo if it doesn't exist yet.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2f4b0-223">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="2f4b0-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2f4b0-224">Bu bölümde, Britta Domo için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Domo.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="2f4b0-226">**Domo için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2f4b0-226">**To assign Britta Simon to Domo, perform the following steps:**</span></span>

1. <span data-ttu-id="2f4b0-227">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="2f4b0-229">Uygulamalar listesinde **Domo**.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-229">In the applications list, select **Domo**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-domo-tutorial/tutorial_domo_app.png) 

3. <span data-ttu-id="2f4b0-231">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="2f4b0-233">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-233">Click **Add** button.</span></span> <span data-ttu-id="2f4b0-234">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="2f4b0-236">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2f4b0-237">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2f4b0-238">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2f4b0-239">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="2f4b0-239">Testing single sign-on</span></span>

<span data-ttu-id="2f4b0-240">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="2f4b0-241">Erişim paneli Domo parçasında tıklattığınızda, otomatik olarak Domo uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-241">When you click the Domo tile in the Access Panel, you should get automatically signed-on to your Domo application.</span></span>

<span data-ttu-id="2f4b0-242">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2f4b0-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2f4b0-243">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2f4b0-243">Additional resources</span></span>

* [<span data-ttu-id="2f4b0-244">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="2f4b0-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f4b0-245">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="2f4b0-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-domo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-domo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-domo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-domo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-domo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-domo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-domo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-domo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-domo-tutorial/tutorial_general_203.png

