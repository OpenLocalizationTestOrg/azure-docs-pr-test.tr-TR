---
title: "Öğretici: Azure Active Directory Tümleştirme ile Allocadia | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Allocadia arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c415fc55-6dc1-49f2-a8a2-2fc6e3790d65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: jeedes
ms.openlocfilehash: 8e97c365383ecdb72cc1cd449b522b75875fc1db
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-allocadia"></a><span data-ttu-id="3087a-103">Öğretici: Azure Active Directory Tümleştirme Allocadia ile</span><span class="sxs-lookup"><span data-stu-id="3087a-103">Tutorial: Azure Active Directory integration with Allocadia</span></span>

<span data-ttu-id="3087a-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Allocadia tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3087a-104">In this tutorial, you learn how to integrate Allocadia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3087a-105">Allocadia Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="3087a-105">Integrating Allocadia with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3087a-106">Allocadia erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="3087a-106">You can control in Azure AD who has access to Allocadia</span></span>
- <span data-ttu-id="3087a-107">Otomatik olarak için Allocadia (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="3087a-107">You can enable your users to automatically get signed-on to Allocadia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3087a-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="3087a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3087a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3087a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3087a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3087a-110">Prerequisites</span></span>

<span data-ttu-id="3087a-111">Azure AD tümleştirme Allocadia ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="3087a-111">To configure Azure AD integration with Allocadia, you need the following items:</span></span>

- <span data-ttu-id="3087a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="3087a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3087a-113">Bir Allocadia çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="3087a-113">An Allocadia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3087a-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="3087a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3087a-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="3087a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3087a-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="3087a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3087a-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3087a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3087a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="3087a-118">Scenario description</span></span>
<span data-ttu-id="3087a-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="3087a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3087a-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="3087a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3087a-121">Galeriden Allocadia ekleme</span><span class="sxs-lookup"><span data-stu-id="3087a-121">Adding Allocadia from the gallery</span></span>
2. <span data-ttu-id="3087a-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="3087a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-allocadia-from-the-gallery"></a><span data-ttu-id="3087a-123">Galeriden Allocadia ekleme</span><span class="sxs-lookup"><span data-stu-id="3087a-123">Adding Allocadia from the gallery</span></span>
<span data-ttu-id="3087a-124">Azure AD Allocadia tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Allocadia eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3087a-124">To configure the integration of Allocadia into Azure AD, you need to add Allocadia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3087a-125">**Galeriden Allocadia eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3087a-125">**To add Allocadia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3087a-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3087a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3087a-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="3087a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3087a-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3087a-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="3087a-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3087a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="3087a-133">Arama kutusuna **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="3087a-133">In the search box, type **Allocadia**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_search.png)

5. <span data-ttu-id="3087a-135">Sonuçlar panelinde seçin **Allocadia**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3087a-135">In the results panel, select **Allocadia**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3087a-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="3087a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3087a-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Allocadia ile test etme</span><span class="sxs-lookup"><span data-stu-id="3087a-138">In this section, you configure and test Azure AD single sign-on with Allocadia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3087a-139">Tekli çalışmaya oturum için Azure AD Allocadia karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="3087a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Allocadia is to a user in Azure AD.</span></span> <span data-ttu-id="3087a-140">Diğer bir deyişle, bir Azure AD kullanıcısının Allocadia ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3087a-140">In other words, a link relationship between an Azure AD user and the related user in Allocadia needs to be established.</span></span>

<span data-ttu-id="3087a-141">Allocadia içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="3087a-141">In Allocadia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3087a-142">Yapılandırma ve Azure AD çoklu oturum açma Allocadia ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="3087a-142">To configure and test Azure AD single sign-on with Allocadia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3087a-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="3087a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3087a-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="3087a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3087a-145">**[Bir Allocadia test kullanıcısı oluşturma](#creating-an-allocadia-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Allocadia sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="3087a-145">**[Creating an Allocadia test user](#creating-an-allocadia-test-user)** - to have a counterpart of Britta Simon in Allocadia that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3087a-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="3087a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3087a-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3087a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3087a-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3087a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3087a-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Allocadia uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3087a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Allocadia application.</span></span>

<span data-ttu-id="3087a-150">**Azure AD çoklu oturum açma ile Allocadia yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3087a-150">**To configure Azure AD single sign-on with Allocadia, perform the following steps:**</span></span>

1. <span data-ttu-id="3087a-151">Azure portalında üzerinde **Allocadia** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="3087a-151">In the Azure portal, on the **Allocadia** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="3087a-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="3087a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_samlbase.png)

3. <span data-ttu-id="3087a-155">Üzerinde **Allocadia etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3087a-155">On the **Allocadia Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_url.png)

    <span data-ttu-id="3087a-157">a.</span><span class="sxs-lookup"><span data-stu-id="3087a-157">a.</span></span> <span data-ttu-id="3087a-158">İçinde **tanımlayıcısı** metin kutusuna, aşağıdaki desenleri kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="3087a-158">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
       
     <span data-ttu-id="3087a-159">Test ortamı için-`https://na2standby.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="3087a-159">For test environment -  `https://na2standby.allocadia.com`</span></span>
    
     <span data-ttu-id="3087a-160">Üretim ortamı için-`https://na2.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="3087a-160">For production environment - `https://na2.allocadia.com`</span></span>

    <span data-ttu-id="3087a-161">b.</span><span class="sxs-lookup"><span data-stu-id="3087a-161">b.</span></span> <span data-ttu-id="3087a-162">İçinde **yanıt URL'si** metin kutusuna, aşağıdaki desenleri kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="3087a-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    
     <span data-ttu-id="3087a-163">Test ortamı için-`https://na2standby.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="3087a-163">For test environment - `https://na2standby.allocadia.com/allocadia/saml/SSO`</span></span>
    
     <span data-ttu-id="3087a-164">Üretim ortamı için-`https://na2.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="3087a-164">For production environment - `https://na2.allocadia.com/allocadia/saml/SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3087a-165">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="3087a-165">These values are not real.</span></span> <span data-ttu-id="3087a-166">Bu değerler gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3087a-166">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="3087a-167">Kişi [Allocadia destek ekibi](mailTo:support@allocadia.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="3087a-167">Contact [Allocadia support team](mailTo:support@allocadia.com) to get these values.</span></span>

4. <span data-ttu-id="3087a-168">Allocadia uygulaması SAML onaylar belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="3087a-168">Allocadia application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="3087a-169">Bu uygulama için aşağıdaki talep yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3087a-169">Configure the following claims for this application.</span></span> <span data-ttu-id="3087a-170">Bu öznitelik değerlerini yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="3087a-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="3087a-171">Aşağıdaki ekran görüntüsünde, bu yapılandırma için bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="3087a-171">The following screenshot shows an example for this configuration.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_attributes.png)
    
5. <span data-ttu-id="3087a-173">İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği görüntüde gösterildiği gibi yapılandırın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3087a-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="3087a-174">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="3087a-174">Attribute Name</span></span> | <span data-ttu-id="3087a-175">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="3087a-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="3087a-176">FirstName</span><span class="sxs-lookup"><span data-stu-id="3087a-176">firstname</span></span> | <span data-ttu-id="3087a-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="3087a-177">user.givenname</span></span> |
    | <span data-ttu-id="3087a-178">Soyadı</span><span class="sxs-lookup"><span data-stu-id="3087a-178">lastname</span></span> | <span data-ttu-id="3087a-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="3087a-179">user.surname</span></span> |
    | <span data-ttu-id="3087a-180">E-posta</span><span class="sxs-lookup"><span data-stu-id="3087a-180">email</span></span> | <span data-ttu-id="3087a-181">User.Mail</span><span class="sxs-lookup"><span data-stu-id="3087a-181">user.mail</span></span> |
    
    <span data-ttu-id="3087a-182">a.</span><span class="sxs-lookup"><span data-stu-id="3087a-182">a.</span></span> <span data-ttu-id="3087a-183">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3087a-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="3087a-185">b.</span><span class="sxs-lookup"><span data-stu-id="3087a-185">b.</span></span> <span data-ttu-id="3087a-186">İçinde **adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="3087a-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="3087a-188">c.</span><span class="sxs-lookup"><span data-stu-id="3087a-188">c.</span></span> <span data-ttu-id="3087a-189">Gelen **değeri** listesinde, ilgili satır için gösterilen öznitelik değeri yazın.</span><span class="sxs-lookup"><span data-stu-id="3087a-189">From the **Value** list, type the attribute value shown for that row.</span></span>
 
    <span data-ttu-id="3087a-190">d.</span><span class="sxs-lookup"><span data-stu-id="3087a-190">d.</span></span> <span data-ttu-id="3087a-191">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3087a-191">Click **Ok**.</span></span>



6. <span data-ttu-id="3087a-192">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3087a-192">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_certificate.png) 


7. <span data-ttu-id="3087a-194">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3087a-194">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-allocadia-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3087a-196">Çoklu oturum açma yapılandırmak için **Allocadia** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [Allocadia destek ekibi](mailTo:support@allocadia.com).</span><span class="sxs-lookup"><span data-stu-id="3087a-196">To configure single sign-on on **Allocadia** side, you need to send the downloaded **Metadata XML** to [Allocadia support team](mailTo:support@allocadia.com).</span></span> <span data-ttu-id="3087a-197">Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3087a-197">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3087a-198">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="3087a-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3087a-199">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="3087a-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3087a-200">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3087a-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3087a-201">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3087a-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="3087a-202">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="3087a-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="3087a-204">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3087a-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3087a-205">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3087a-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-allocadia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3087a-207">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="3087a-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-allocadia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3087a-209">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="3087a-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-allocadia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3087a-211">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3087a-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-allocadia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3087a-213">a.</span><span class="sxs-lookup"><span data-stu-id="3087a-213">a.</span></span> <span data-ttu-id="3087a-214">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3087a-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3087a-215">b.</span><span class="sxs-lookup"><span data-stu-id="3087a-215">b.</span></span> <span data-ttu-id="3087a-216">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="3087a-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3087a-217">c.</span><span class="sxs-lookup"><span data-stu-id="3087a-217">c.</span></span> <span data-ttu-id="3087a-218">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="3087a-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3087a-219">d.</span><span class="sxs-lookup"><span data-stu-id="3087a-219">d.</span></span> <span data-ttu-id="3087a-220">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3087a-220">Click **Create**.</span></span>
 
### <a name="creating-an-allocadia-test-user"></a><span data-ttu-id="3087a-221">Bir Allocadia test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3087a-221">Creating an Allocadia test user</span></span>

<span data-ttu-id="3087a-222">Uygulama, sadece kullanıcı zaman sağlama destekler.</span><span class="sxs-lookup"><span data-stu-id="3087a-222">Application supports Just in time user provisioning.</span></span> <span data-ttu-id="3087a-223">Kimlik doğrulamasından sonra kullanıcılar uygulamada otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3087a-223">After authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3087a-224">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="3087a-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3087a-225">Bu bölümde, Britta Allocadia için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="3087a-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Allocadia.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="3087a-227">**Allocadia için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3087a-227">**To assign Britta Simon to Allocadia, perform the following steps:**</span></span>

1. <span data-ttu-id="3087a-228">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3087a-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="3087a-230">Uygulamalar listesinde **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="3087a-230">In the applications list, select **Allocadia**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_app.png) 

3. <span data-ttu-id="3087a-232">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="3087a-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="3087a-234">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3087a-234">Click **Add** button.</span></span> <span data-ttu-id="3087a-235">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3087a-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="3087a-237">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="3087a-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3087a-238">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3087a-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3087a-239">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3087a-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3087a-240">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="3087a-240">Testing single sign-on</span></span>

<span data-ttu-id="3087a-241">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="3087a-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3087a-242">Erişim paneli Allocadia parçasında tıklattığınızda, otomatik olarak Allocadia uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="3087a-242">When you click the Allocadia tile in the Access Panel, you should get automatically signed-on to your Allocadia application.</span></span>
<span data-ttu-id="3087a-243">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="3087a-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3087a-244">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3087a-244">Additional resources</span></span>

* [<span data-ttu-id="3087a-245">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="3087a-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3087a-246">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="3087a-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_203.png

