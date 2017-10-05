---
title: "Öğretici: Azure Active Directory Tümleştirme fon portalı ile | Microsoft Docs"
description: "Çoklu oturum açma fon Portal ile Azure Active Directory arasındaki yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4663cc8a-976a-4c6c-b3b4-1e5df9b66744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: d0bfc793bb26c551f85706eaec857962a3415e1f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-the-funding-portal"></a><span data-ttu-id="0f0e9-103">Öğretici: Azure Active Directory Tümleştirme fon portalı ile</span><span class="sxs-lookup"><span data-stu-id="0f0e9-103">Tutorial: Azure Active Directory integration with The Funding Portal</span></span>

<span data-ttu-id="0f0e9-104">Bu öğreticide, fon Portal Azure Active Directory (Azure AD) ile tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-104">In this tutorial, you learn how to integrate The Funding Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0f0e9-105">Fon Portal Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="0f0e9-105">Integrating The Funding Portal with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0f0e9-106">Fon Portal erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0f0e9-106">You can control in Azure AD who has access to The Funding Portal</span></span>
- <span data-ttu-id="0f0e9-107">Azure AD hesaplarına otomatik olarak fon portalına (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0f0e9-107">You can enable your users to automatically get signed-on to The Funding Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0f0e9-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="0f0e9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0f0e9-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0f0e9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f0e9-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0f0e9-110">Prerequisites</span></span>

<span data-ttu-id="0f0e9-111">Azure AD tümleştirme fon Portal ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="0f0e9-111">To configure Azure AD integration with The Funding Portal, you need the following items:</span></span>

- <span data-ttu-id="0f0e9-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="0f0e9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0f0e9-113">Bir fon Portal çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="0f0e9-113">A The Funding Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0f0e9-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0f0e9-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0f0e9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0f0e9-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0f0e9-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0f0e9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0f0e9-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="0f0e9-118">Scenario description</span></span>
<span data-ttu-id="0f0e9-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0f0e9-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="0f0e9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0f0e9-121">Galeriden fon Portal ekleme</span><span class="sxs-lookup"><span data-stu-id="0f0e9-121">Adding The Funding Portal from the gallery</span></span>
2. <span data-ttu-id="0f0e9-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0f0e9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-the-funding-portal-from-the-gallery"></a><span data-ttu-id="0f0e9-123">Galeriden fon Portal ekleme</span><span class="sxs-lookup"><span data-stu-id="0f0e9-123">Adding The Funding Portal from the gallery</span></span>
<span data-ttu-id="0f0e9-124">Azure AD fon Portal tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden fon Portal eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-124">To configure the integration of The Funding Portal into Azure AD, you need to add The Funding Portal from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0f0e9-125">**Galeriden fon Portal eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0f0e9-125">**To add The Funding Portal from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0f0e9-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0f0e9-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0f0e9-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="0f0e9-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="0f0e9-133">Arama kutusuna **fon Portal**.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-133">In the search box, type **The Funding Portal**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_search.png)

5. <span data-ttu-id="0f0e9-135">Sonuçlar panelinde seçin **fon Portal**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-135">In the results panel, select **The Funding Portal**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0f0e9-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0f0e9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0f0e9-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma fon "Britta Simon" adlı bir test kullanıcı tabanlı Portal ile test etme.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-138">In this section, you configure and test Azure AD single sign-on with The Funding Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0f0e9-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen fon Portalı'nda bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in The Funding Portal is to a user in Azure AD.</span></span> <span data-ttu-id="0f0e9-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı portalında fon arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-140">In other words, a link relationship between an Azure AD user and the related user in The Funding Portal needs to be established.</span></span>

<span data-ttu-id="0f0e9-141">Fon portalında değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-141">In The Funding Portal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0f0e9-142">Yapılandırma ve Azure AD çoklu oturum açma fon portalı ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0f0e9-142">To configure and test Azure AD single sign-on with The Funding Portal, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0f0e9-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0f0e9-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0f0e9-145">**[Fon Portal test kullanıcısı oluşturma](#creating-the-funding-portal-test-user)**  - Britta Simon, karşılık gelen fon kullanıcı Azure AD gösterimini bağlantılı Portal sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-145">**[Creating The Funding Portal test user](#creating-the-funding-portal-test-user)** - to have a counterpart of Britta Simon in The Funding Portal that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0f0e9-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0f0e9-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0f0e9-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0f0e9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0f0e9-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma fon portalı uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your The Funding Portal application.</span></span>

<span data-ttu-id="0f0e9-150">**Azure AD çoklu oturum açma fon Portal ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0f0e9-150">**To configure Azure AD single sign-on with The Funding Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="0f0e9-151">Azure portalında üzerinde **fon Portal** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-151">In the Azure portal, on the **The Funding Portal** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="0f0e9-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_samlbase.png)

3. <span data-ttu-id="0f0e9-155">Üzerinde **fon Portal etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0f0e9-155">On the **The Funding Portal Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_url.png)

    <span data-ttu-id="0f0e9-157">a.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-157">a.</span></span> <span data-ttu-id="0f0e9-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.regenteducation.net/`</span><span class="sxs-lookup"><span data-stu-id="0f0e9-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.regenteducation.net/`</span></span>

    <span data-ttu-id="0f0e9-159">b.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-159">b.</span></span> <span data-ttu-id="0f0e9-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.regenteducation.net`</span><span class="sxs-lookup"><span data-stu-id="0f0e9-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.regenteducation.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0f0e9-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-161">These values are not real.</span></span> <span data-ttu-id="0f0e9-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0f0e9-163">Kişi [fon Portal istemci destek ekibi](mailto:info@regenteducation.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-163">Contact [The Funding Portal Client support team](mailto:info@regenteducation.com) to get these values.</span></span> 

4. <span data-ttu-id="0f0e9-164">Portal Finansman sağlayan uygulama "externalId1" adlı bir özniteliği içerecek şekilde SAML onaylar bekler.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-164">The Funding Portal application expects the SAML assertions to contain an attribute named "externalId1".</span></span> <span data-ttu-id="0f0e9-165">"ExternalId1" değeri, tanınan bir studentID olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-165">The value of "externalId1" should be a recognized studentID.</span></span> <span data-ttu-id="0f0e9-166">Bu uygulama için "externalId1" talep yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-166">Configure the "externalId1" claim for this application.</span></span> <span data-ttu-id="0f0e9-167">Bu öznitelik değerlerini yönetebilirsiniz **kullanıcı öznitelikleri** uygulamanın.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-167">You can manage the values of these attributes from the **User Attributes** of the application.</span></span> <span data-ttu-id="0f0e9-168">Aşağıdaki ekran görüntüsünde bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-168">The following screenshot shows an example for this.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_attribute.png)

5. <span data-ttu-id="0f0e9-170">İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği görüntüde gösterildiği gibi yapılandırın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0f0e9-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>

    | <span data-ttu-id="0f0e9-171">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="0f0e9-171">Attribute Name</span></span> | <span data-ttu-id="0f0e9-172">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="0f0e9-172">Attribute Value</span></span> |
    | ------------------- | ---------------- |
    | <span data-ttu-id="0f0e9-173">externalId1</span><span class="sxs-lookup"><span data-stu-id="0f0e9-173">externalId1</span></span> | <span data-ttu-id="0f0e9-174">User.extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="0f0e9-174">user.extensionattribute1</span></span> |

    <span data-ttu-id="0f0e9-175">a.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-175">a.</span></span> <span data-ttu-id="0f0e9-176">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="0f0e9-179">b.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-179">b.</span></span> <span data-ttu-id="0f0e9-180">İçinde **adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="0f0e9-181">c.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-181">c.</span></span> <span data-ttu-id="0f0e9-182">Gelen **öznitelik değeri** listesinde, uygulamanız için kullanmak istediğiniz özniteliği seçin.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-182">From the **Attribute Value** list, select the attribute you want to use for your implementation.</span></span> <span data-ttu-id="0f0e9-183">Örneğin, ExtensionAttribute1 StudentID değeri depoladıysanız ardından user.extensionattribute1 seçin.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-183">For example, if you have stored the StudentID value in the ExtensionAttribute1, then select user.extensionattribute1.</span></span>
    
    <span data-ttu-id="0f0e9-184">d.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-184">d.</span></span> <span data-ttu-id="0f0e9-185">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-185">Click **Ok**.</span></span>
 
6. <span data-ttu-id="0f0e9-186">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-186">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_certificate.png) 

7. <span data-ttu-id="0f0e9-188">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-188">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="0f0e9-190">Çoklu oturum açma yapılandırmak için **fon Portal** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [fon Portal destek ekibi](mailto:info@regenteducation.com).</span><span class="sxs-lookup"><span data-stu-id="0f0e9-190">To configure single sign-on on **The Funding Portal** side, you need to send the downloaded **Metadata XML** to [The Funding Portal support team](mailto:info@regenteducation.com).</span></span> <span data-ttu-id="0f0e9-191">Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-191">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0f0e9-192">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="0f0e9-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0f0e9-193">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0f0e9-194">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0f0e9-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0f0e9-195">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0f0e9-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="0f0e9-196">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="0f0e9-198">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0f0e9-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0f0e9-199">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0f0e9-201">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0f0e9-203">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0f0e9-205">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0f0e9-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0f0e9-207">a.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-207">a.</span></span> <span data-ttu-id="0f0e9-208">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0f0e9-209">b.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-209">b.</span></span> <span data-ttu-id="0f0e9-210">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0f0e9-211">c.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-211">c.</span></span> <span data-ttu-id="0f0e9-212">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0f0e9-213">d.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-213">d.</span></span> <span data-ttu-id="0f0e9-214">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-214">Click **Create**.</span></span>
 
### <a name="creating-the-funding-portal-test-user"></a><span data-ttu-id="0f0e9-215">Fon Portal test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0f0e9-215">Creating The Funding Portal test user</span></span>

<span data-ttu-id="0f0e9-216">Bu bölümde, fon Portalı'nda Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-216">In this section, you create a user called Britta Simon in The Funding Portal.</span></span> <span data-ttu-id="0f0e9-217">Çalışmak [fon Portal destek ekibi](mailto:info@regenteducation.com) test kullanıcısı eklemek ve SSO'yu etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-217">Work with [The Funding Portal support team](mailto:info@regenteducation.com) to add the test user and enable SSO.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0f0e9-218">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="0f0e9-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0f0e9-219">Bu bölümde, Britta fon portalına erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to The Funding Portal.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="0f0e9-221">**Fon portalına Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0f0e9-221">**To assign Britta Simon to The Funding Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="0f0e9-222">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="0f0e9-224">Uygulamalar listesinde **fon Portal**.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-224">In the applications list, select **The Funding Portal**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_app.png) 

3. <span data-ttu-id="0f0e9-226">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="0f0e9-228">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-228">Click **Add** button.</span></span> <span data-ttu-id="0f0e9-229">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="0f0e9-231">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0f0e9-232">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0f0e9-233">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0f0e9-234">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="0f0e9-234">Testing single sign-on</span></span>

<span data-ttu-id="0f0e9-235">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0f0e9-236">Erişim paneli fon Portal parçasında tıklattığınızda, otomatik olarak fon Portal uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="0f0e9-236">When you click the The Funding Portal tile in the Access Panel, you should get automatically signed-on to your The Funding Portal application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0f0e9-237">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0f0e9-237">Additional resources</span></span>

* [<span data-ttu-id="0f0e9-238">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="0f0e9-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0f0e9-239">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="0f0e9-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_203.png

