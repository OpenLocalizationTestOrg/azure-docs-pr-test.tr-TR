---
title: "Öğretici: Azure Active Directory Tümleştirme ile Hightail | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Hightail arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: ba55f9b62d274aa3eb91723c62b53f54de0891b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="75c86-103">Öğretici: Azure Active Directory Tümleştirme Hightail ile</span><span class="sxs-lookup"><span data-stu-id="75c86-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="75c86-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Hightail tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="75c86-104">In this tutorial, you learn how to integrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="75c86-105">Hightail Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="75c86-105">Integrating Hightail with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="75c86-106">Hightail erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="75c86-106">You can control in Azure AD who has access to Hightail</span></span>
- <span data-ttu-id="75c86-107">Otomatik olarak için Hightail (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="75c86-107">You can enable your users to automatically get signed-on to Hightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="75c86-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="75c86-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="75c86-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="75c86-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75c86-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="75c86-110">Prerequisites</span></span>

<span data-ttu-id="75c86-111">Azure AD tümleştirme Hightail ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="75c86-111">To configure Azure AD integration with Hightail, you need the following items:</span></span>

- <span data-ttu-id="75c86-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="75c86-112">An Azure AD subscription</span></span>
- <span data-ttu-id="75c86-113">Bir Hightail çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="75c86-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="75c86-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="75c86-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="75c86-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="75c86-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="75c86-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="75c86-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="75c86-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="75c86-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="75c86-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="75c86-118">Scenario description</span></span>
<span data-ttu-id="75c86-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="75c86-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="75c86-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="75c86-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="75c86-121">Galeriden Hightail ekleme</span><span class="sxs-lookup"><span data-stu-id="75c86-121">Adding Hightail from the gallery</span></span>
2. <span data-ttu-id="75c86-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="75c86-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-the-gallery"></a><span data-ttu-id="75c86-123">Galeriden Hightail ekleme</span><span class="sxs-lookup"><span data-stu-id="75c86-123">Adding Hightail from the gallery</span></span>
<span data-ttu-id="75c86-124">Azure AD Hightail tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Hightail eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="75c86-124">To configure the integration of Hightail into Azure AD, you need to add Hightail from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="75c86-125">**Galeriden Hightail eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="75c86-125">**To add Hightail from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="75c86-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="75c86-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="75c86-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="75c86-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="75c86-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="75c86-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="75c86-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="75c86-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="75c86-133">Arama kutusuna **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="75c86-133">In the search box, type **Hightail**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. <span data-ttu-id="75c86-135">Sonuçlar panelinde seçin **Hightail**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="75c86-135">In the results panel, select **Hightail**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="75c86-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="75c86-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="75c86-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Hightail sınayın.</span><span class="sxs-lookup"><span data-stu-id="75c86-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="75c86-139">Tekli çalışmaya oturum için Azure AD Hightail karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="75c86-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Hightail is to a user in Azure AD.</span></span> <span data-ttu-id="75c86-140">Diğer bir deyişle, bir Azure AD kullanıcısının Hightail ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="75c86-140">In other words, a link relationship between an Azure AD user and the related user in Hightail needs to be established.</span></span>

<span data-ttu-id="75c86-141">Hightail içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="75c86-141">In Hightail, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="75c86-142">Yapılandırma ve Azure AD çoklu oturum açma Hightail ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="75c86-142">To configure and test Azure AD single sign-on with Hightail, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="75c86-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="75c86-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="75c86-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="75c86-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="75c86-145">**[Hightail test kullanıcısı oluşturma](#creating-a-hightail-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Hightail sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="75c86-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - to have a counterpart of Britta Simon in Hightail that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="75c86-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="75c86-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="75c86-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="75c86-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="75c86-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="75c86-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="75c86-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Hightail uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="75c86-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="75c86-150">**Azure AD çoklu oturum açma ile Hightail yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="75c86-150">**To configure Azure AD single sign-on with Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="75c86-151">Azure portalında üzerinde **Hightail** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="75c86-151">In the Azure portal, on the **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="75c86-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="75c86-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. <span data-ttu-id="75c86-155">Üzerinde **Hightail etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="75c86-155">On the **Hightail Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     <span data-ttu-id="75c86-157">İçinde **yanıt URL'si** metin olarak URL'yi yazın:`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span><span class="sxs-lookup"><span data-stu-id="75c86-157">In the **Reply URL** textbox, type the URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="75c86-158">Önceki değerin gerçek değeri değil.</span><span class="sxs-lookup"><span data-stu-id="75c86-158">The preceding value is not real value.</span></span> <span data-ttu-id="75c86-159">Değer, gerçek yanıt, öğreticide daha sonra açıklanan URL ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="75c86-159">You will update the value with the actual Reply URL, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="75c86-160">Üzerinde **Hightail etki alanı ve URL'leri** uygulamada yapılandırmak istiyorsanız, bölüm **SP tarafından başlatılan modu**, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="75c86-160">On the **Hightail Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="75c86-162">a.</span><span class="sxs-lookup"><span data-stu-id="75c86-162">a.</span></span> <span data-ttu-id="75c86-163">Tıklatın **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="75c86-163">Click the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="75c86-164">b.</span><span class="sxs-lookup"><span data-stu-id="75c86-164">b.</span></span> <span data-ttu-id="75c86-165">İçinde **oturum üzerinde URL'si** metin olarak URL'yi yazın:`https://www.hightail.com/loginSSO`</span><span class="sxs-lookup"><span data-stu-id="75c86-165">In the **Sign On URL** textbox, type the URL as: `https://www.hightail.com/loginSSO`</span></span>

4. <span data-ttu-id="75c86-166">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="75c86-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. <span data-ttu-id="75c86-168">Hightail uygulama belirli bir biçimde SAML onaylar bekler.</span><span class="sxs-lookup"><span data-stu-id="75c86-168">Hightail application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="75c86-169">Lütfen bu uygulama için aşağıdaki talep yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="75c86-169">Please configure the following claims for this application.</span></span> <span data-ttu-id="75c86-170">Bu öznitelik değerlerini yönetebilirsiniz **"Atrribute"** uygulama sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="75c86-170">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="75c86-171">Aşağıdaki ekran görüntüsünde bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="75c86-171">The following screenshot shows an example for this.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. <span data-ttu-id="75c86-173">İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği görüntüde gösterildiği gibi yapılandırın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="75c86-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="75c86-174">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="75c86-174">Attribute Name</span></span> | <span data-ttu-id="75c86-175">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="75c86-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="75c86-176">FirstName</span><span class="sxs-lookup"><span data-stu-id="75c86-176">FirstName</span></span> | <span data-ttu-id="75c86-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="75c86-177">user.givenname</span></span> |
    | <span data-ttu-id="75c86-178">Soyadı</span><span class="sxs-lookup"><span data-stu-id="75c86-178">LastName</span></span> | <span data-ttu-id="75c86-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="75c86-179">user.surname</span></span> |
    | <span data-ttu-id="75c86-180">E-posta</span><span class="sxs-lookup"><span data-stu-id="75c86-180">Email</span></span> | <span data-ttu-id="75c86-181">User.Mail</span><span class="sxs-lookup"><span data-stu-id="75c86-181">user.mail</span></span> |    
    | <span data-ttu-id="75c86-182">Userıdentity</span><span class="sxs-lookup"><span data-stu-id="75c86-182">UserIdentity</span></span> | <span data-ttu-id="75c86-183">User.Mail</span><span class="sxs-lookup"><span data-stu-id="75c86-183">user.mail</span></span> |
    
    <span data-ttu-id="75c86-184">a.</span><span class="sxs-lookup"><span data-stu-id="75c86-184">a.</span></span> <span data-ttu-id="75c86-185">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="75c86-185">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="75c86-188">b.</span><span class="sxs-lookup"><span data-stu-id="75c86-188">b.</span></span> <span data-ttu-id="75c86-189">İçinde **adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="75c86-189">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="75c86-190">c.</span><span class="sxs-lookup"><span data-stu-id="75c86-190">c.</span></span> <span data-ttu-id="75c86-191">Gelen **değeri** listesinde, ilgili satır için gösterilen öznitelik değeri yazın.</span><span class="sxs-lookup"><span data-stu-id="75c86-191">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="75c86-192">d.</span><span class="sxs-lookup"><span data-stu-id="75c86-192">d.</span></span> <span data-ttu-id="75c86-193">Bırakın **Namespace** boş.</span><span class="sxs-lookup"><span data-stu-id="75c86-193">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="75c86-194">e.</span><span class="sxs-lookup"><span data-stu-id="75c86-194">e.</span></span> <span data-ttu-id="75c86-195">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="75c86-195">Click **Ok**.</span></span>

7. <span data-ttu-id="75c86-196">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="75c86-196">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="75c86-198">Üzerinde **Hightail yapılandırma** 'yi tıklatın **yapılandırma Hightail** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="75c86-198">On the **Hightail Configuration** section, click **Configure Hightail** to open **Configure sign-on** window.</span></span> <span data-ttu-id="75c86-199">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="75c86-199">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    ><span data-ttu-id="75c86-201">Çoklu oturum açma Hightail uygulamaya yapılandırmadan önce lütfen beyaz liste Hightail ile e-posta etki alanınızı team böylece bu etki alanını kullanan tüm kullanıcılar tekli oturum açma işlevini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75c86-201">Before configuring the Single Sign On at Hightail app, please white list your email domain with Hightail team so that all the users who are using this domain can use Single Sign On functionality.</span></span>


9. <span data-ttu-id="75c86-202">Uygulamanız için yapılandırılmış SSO almak için Hightail kiracınız yönetici olarak oturum gerekir.</span><span class="sxs-lookup"><span data-stu-id="75c86-202">To get SSO configured for your application, you need to sign-on to your Hightail tenant as an administrator.</span></span>
   
    <span data-ttu-id="75c86-203">a.</span><span class="sxs-lookup"><span data-stu-id="75c86-203">a.</span></span> <span data-ttu-id="75c86-204">Üstteki menüde tıklatın **hesap** sekmesinde ve seçin **yapılandırma SAML**.</span><span class="sxs-lookup"><span data-stu-id="75c86-204">In the menu on the top, click the **Account** tab and select **Configure SAML**.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    <span data-ttu-id="75c86-206">b.</span><span class="sxs-lookup"><span data-stu-id="75c86-206">b.</span></span> <span data-ttu-id="75c86-207">Onay kutusunu işaretleyin **SAML kimlik doğrulamasını etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="75c86-207">Select the checkbox of **Enable SAML Authentication**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    <span data-ttu-id="75c86-209">c.</span><span class="sxs-lookup"><span data-stu-id="75c86-209">c.</span></span> <span data-ttu-id="75c86-210">Base-64 kodlanmış sertifikanızı Azure portalından indirdiğiniz Not Defteri'nde açın, içeriğini, panoya kopyalayın ve yapıştırın kendisine **SAML belirteç imzalama sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="75c86-210">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Token Signing Certificate** textbox.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    <span data-ttu-id="75c86-212">d.</span><span class="sxs-lookup"><span data-stu-id="75c86-212">d.</span></span> <span data-ttu-id="75c86-213">İçinde **SAML yetkilisi (Kimlik sağlayıcısı)** metin kutusuna, değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="75c86-213">In the **SAML Authority (Identity Provider)** textbox, paste the value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    <span data-ttu-id="75c86-215">e.</span><span class="sxs-lookup"><span data-stu-id="75c86-215">e.</span></span> <span data-ttu-id="75c86-216">Uygulamada yapılandırmak istiyorsanız **IDP başlatılan modu** seçin **"Kimlik sağlayıcıyı (IDP) başlatılan oturum açma"**.</span><span class="sxs-lookup"><span data-stu-id="75c86-216">If you wish to configure the application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="75c86-217">Varsa **SP tarafından başlatılan modu** seçin **"Hizmet sağlayıcısı (SP) başlatılan oturum açma"**.</span><span class="sxs-lookup"><span data-stu-id="75c86-217">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    <span data-ttu-id="75c86-219">f.</span><span class="sxs-lookup"><span data-stu-id="75c86-219">f.</span></span> <span data-ttu-id="75c86-220">Örneğiniz için SAML tüketici URL'sini kopyalayın ve yapıştırın **yanıt URL'si** metin kutusuna **Hightail etki alanı ve URL'leri** Azure Portal'daki bölümü.</span><span class="sxs-lookup"><span data-stu-id="75c86-220">Copy the SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="75c86-221">g.</span><span class="sxs-lookup"><span data-stu-id="75c86-221">g.</span></span> <span data-ttu-id="75c86-222">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="75c86-222">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="75c86-223">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="75c86-223">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="75c86-224">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="75c86-224">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="75c86-225">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="75c86-225">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="75c86-226">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="75c86-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="75c86-227">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="75c86-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="75c86-229">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="75c86-229">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="75c86-230">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="75c86-230">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="75c86-232">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="75c86-232">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="75c86-234">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="75c86-234">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="75c86-236">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="75c86-236">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="75c86-238">a.</span><span class="sxs-lookup"><span data-stu-id="75c86-238">a.</span></span> <span data-ttu-id="75c86-239">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="75c86-239">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="75c86-240">b.</span><span class="sxs-lookup"><span data-stu-id="75c86-240">b.</span></span> <span data-ttu-id="75c86-241">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="75c86-241">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="75c86-242">c.</span><span class="sxs-lookup"><span data-stu-id="75c86-242">c.</span></span> <span data-ttu-id="75c86-243">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="75c86-243">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="75c86-244">d.</span><span class="sxs-lookup"><span data-stu-id="75c86-244">d.</span></span> <span data-ttu-id="75c86-245">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="75c86-245">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="75c86-246">Hightail test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="75c86-246">Creating a Hightail test user</span></span>

<span data-ttu-id="75c86-247">Bu bölümün amacı Britta Simon içinde Hightail adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="75c86-247">The objective of this section is to create a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="75c86-248">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="75c86-248">There is no action item for you in this section.</span></span> <span data-ttu-id="75c86-249">Yalnızca zaman kullanıcı hazırlama özel taleplere dayanarak destekler hightail.</span><span class="sxs-lookup"><span data-stu-id="75c86-249">Hightail supports just-in-time user provisioning based on the custom claims.</span></span> <span data-ttu-id="75c86-250">Özel talep bölümünde gösterildiği gibi yapılandırdıysanız  **[yapılandırma Azure AD çoklu oturum açma](#configuring-azure-ad-single-sign-on)**  yukarıdaki kullanıcı henüz yok uygulamada otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="75c86-250">If you have configured the custom claims as shown in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in the application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="75c86-251">Bir kullanıcı el ile oluşturmanız gerekiyorsa, başvurmanız gerekir [Hightail destek ekibi](mailto:support@hightail.com).</span><span class="sxs-lookup"><span data-stu-id="75c86-251">If you need to create a user manually, you need to contact the [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="75c86-252">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="75c86-252">Assigning the Azure AD test user</span></span>

<span data-ttu-id="75c86-253">Bu bölümde, Britta Hightail için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="75c86-253">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Hightail.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="75c86-255">**Hightail için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="75c86-255">**To assign Britta Simon to Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="75c86-256">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="75c86-256">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="75c86-258">Uygulamalar listesinde **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="75c86-258">In the applications list, select **Hightail**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. <span data-ttu-id="75c86-260">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="75c86-260">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="75c86-262">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="75c86-262">Click **Add** button.</span></span> <span data-ttu-id="75c86-263">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="75c86-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="75c86-265">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="75c86-265">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="75c86-266">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="75c86-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="75c86-267">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="75c86-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="75c86-268">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="75c86-268">Testing single sign-on</span></span>

<span data-ttu-id="75c86-269">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="75c86-269">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="75c86-270">Erişim paneli Hightail parçasında tıklattığınızda, otomatik olarak Hightail uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="75c86-270">When you click the Hightail tile in the Access Panel, you should get automatically signed-on to your Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="75c86-271">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="75c86-271">Additional resources</span></span>

* [<span data-ttu-id="75c86-272">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="75c86-272">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="75c86-273">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="75c86-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

