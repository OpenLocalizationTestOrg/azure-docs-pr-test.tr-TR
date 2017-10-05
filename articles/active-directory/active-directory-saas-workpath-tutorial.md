---
title: "Öğretici: Azure Active Directory Tümleştirme ile Workpath | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Workpath arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 320b0daf-14be-4813-b59b-25a6a5070690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: f4efa56d2c0374a977c1e46dad64b596cc9c3ea8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workpath"></a><span data-ttu-id="8f5b4-103">Öğretici: Azure Active Directory Tümleştirme Workpath ile</span><span class="sxs-lookup"><span data-stu-id="8f5b4-103">Tutorial: Azure Active Directory integration with Workpath</span></span>

<span data-ttu-id="8f5b4-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Workpath tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-104">In this tutorial, you learn how to integrate Workpath with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8f5b4-105">Workpath Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-105">Integrating Workpath with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8f5b4-106">Workpath erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8f5b4-106">You can control in Azure AD who has access to Workpath</span></span>
- <span data-ttu-id="8f5b4-107">Otomatik olarak için Workpath (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8f5b4-107">You can enable your users to automatically get signed-on to Workpath (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8f5b4-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="8f5b4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8f5b4-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8f5b4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f5b4-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8f5b4-110">Prerequisites</span></span>

<span data-ttu-id="8f5b4-111">Azure AD tümleştirme Workpath ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-111">To configure Azure AD integration with Workpath, you need the following items:</span></span>

- <span data-ttu-id="8f5b4-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="8f5b4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8f5b4-113">Bir Workpath çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="8f5b4-113">A Workpath single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8f5b4-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8f5b4-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8f5b4-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8f5b4-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8f5b4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8f5b4-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="8f5b4-118">Scenario description</span></span>
<span data-ttu-id="8f5b4-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8f5b4-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8f5b4-121">Galeriden Workpath ekleme</span><span class="sxs-lookup"><span data-stu-id="8f5b4-121">Adding Workpath from the gallery</span></span>
2. <span data-ttu-id="8f5b4-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="8f5b4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workpath-from-the-gallery"></a><span data-ttu-id="8f5b4-123">Galeriden Workpath ekleme</span><span class="sxs-lookup"><span data-stu-id="8f5b4-123">Adding Workpath from the gallery</span></span>
<span data-ttu-id="8f5b4-124">Azure AD Workpath tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Workpath eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-124">To configure the integration of Workpath into Azure AD, you need to add Workpath from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8f5b4-125">**Galeriden Workpath eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8f5b4-125">**To add Workpath from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8f5b4-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8f5b4-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8f5b4-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="8f5b4-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="8f5b4-133">Arama kutusuna **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-133">In the search box, type **Workpath**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_search.png)

5. <span data-ttu-id="8f5b4-135">Sonuçlar panelinde seçin **Workpath**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-135">In the results panel, select **Workpath**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8f5b4-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="8f5b4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8f5b4-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Workpath ile test etme</span><span class="sxs-lookup"><span data-stu-id="8f5b4-138">In this section, you configure and test Azure AD single sign-on with Workpath based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8f5b4-139">Tekli çalışmaya oturum için Azure AD Workpath karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workpath is to a user in Azure AD.</span></span> <span data-ttu-id="8f5b4-140">Diğer bir deyişle, bir Azure AD kullanıcısının Workpath ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-140">In other words, a link relationship between an Azure AD user and the related user in Workpath needs to be established.</span></span>

<span data-ttu-id="8f5b4-141">Workpath içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-141">In Workpath, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8f5b4-142">Yapılandırma ve Azure AD çoklu oturum açma Workpath ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-142">To configure and test Azure AD single sign-on with Workpath, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8f5b4-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8f5b4-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8f5b4-145">**[Workpath test kullanıcısı oluşturma](#creating-a-workpath-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Workpath sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-145">**[Creating a Workpath test user](#creating-a-workpath-test-user)** - to have a counterpart of Britta Simon in Workpath that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8f5b4-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8f5b4-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8f5b4-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8f5b4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8f5b4-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Workpath uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workpath application.</span></span>

<span data-ttu-id="8f5b4-150">**Azure AD çoklu oturum açma ile Workpath yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8f5b4-150">**To configure Azure AD single sign-on with Workpath, perform the following steps:**</span></span>

1. <span data-ttu-id="8f5b4-151">Azure portalında üzerinde **Workpath** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-151">In the Azure portal, on the **Workpath** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="8f5b4-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_samlbase.png)

3. <span data-ttu-id="8f5b4-155">Üzerinde **Workpath etki alanı ve URL'leri** uygulamada yapılandırmak istiyorsanız, bölüm **IDP** başlatılan modu aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-155">On the **Workpath Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url.png)

    <span data-ttu-id="8f5b4-157">a.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-157">a.</span></span> <span data-ttu-id="8f5b4-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://api.workpath.com/v1/saml/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="8f5b4-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.workpath.com/v1/saml/metadata/<instancename>`</span></span>

    <span data-ttu-id="8f5b4-159">b.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-159">b.</span></span> <span data-ttu-id="8f5b4-160">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://api.workpath.com/v1/saml/assert/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="8f5b4-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.workpath.com/v1/saml/assert/<instancename>`</span></span>

4. <span data-ttu-id="8f5b4-161">Denetleme **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="8f5b4-162">Uygulamada yapılandırmak istiyorsanız **SP** modunda başlatılan aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-162">If you wish to configure the application in **SP** initiated mode, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url1.png)

    <span data-ttu-id="8f5b4-164">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.workpath.com/ `</span><span class="sxs-lookup"><span data-stu-id="8f5b4-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.workpath.com/ `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8f5b4-165">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-165">These values are not real.</span></span> <span data-ttu-id="8f5b4-166">Bu değerleri gerçek oturum açma URL'si, tanımlayıcı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-166">Update these values with the actual Sign-on URL, Identifier and Reply URL.</span></span> <span data-ttu-id="8f5b4-167">Kişi [Workpath destek ekibi](https://help.workpath.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-167">Contact [Workpath support team](https://help.workpath.com) to get these values.</span></span>

5. <span data-ttu-id="8f5b4-168">Workpath uygulaması SAML onaylar belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-168">Workpath application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="8f5b4-169">Bu uygulama için aşağıdaki talep yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-169">Configure the following claims for this application.</span></span> <span data-ttu-id="8f5b4-170">Bu öznitelik değerlerini yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="8f5b4-171">Aşağıdaki ekran görüntüsünde, bu yapılandırma için bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-171">The following screenshot shows an example for this configuration.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_attributes.png)
    
6. <span data-ttu-id="8f5b4-173">İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği görüntüde gösterildiği gibi yapılandırın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="8f5b4-174">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="8f5b4-174">Attribute Name</span></span> | <span data-ttu-id="8f5b4-175">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="8f5b4-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="8f5b4-176">ilk_ad</span><span class="sxs-lookup"><span data-stu-id="8f5b4-176">first_name</span></span> | <span data-ttu-id="8f5b4-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="8f5b4-177">user.givenname</span></span> |
    | <span data-ttu-id="8f5b4-178">Soyadı</span><span class="sxs-lookup"><span data-stu-id="8f5b4-178">last_name</span></span> | <span data-ttu-id="8f5b4-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="8f5b4-179">user.surname</span></span> |
    
    <span data-ttu-id="8f5b4-180">a.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-180">a.</span></span> <span data-ttu-id="8f5b4-181">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="8f5b4-183">b.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-183">b.</span></span> <span data-ttu-id="8f5b4-184">İçinde **adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="8f5b4-186">c.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-186">c.</span></span> <span data-ttu-id="8f5b4-187">Gelen **değeri** listesinde, ilgili satır için gösterilen öznitelik değeri yazın.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-187">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="8f5b4-188">d.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-188">d.</span></span> <span data-ttu-id="8f5b4-189">Bırakın **Namespace** metin kutusu boş.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-189">Leave the **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="8f5b4-190">e.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-190">e.</span></span> <span data-ttu-id="8f5b4-191">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-191">Click **Ok**.</span></span>
    

7. <span data-ttu-id="8f5b4-192">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-192">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_certificate.png) 

8. <span data-ttu-id="8f5b4-194">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-194">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="8f5b4-196">Üzerinde **Workpath yapılandırma** 'yi tıklatın **yapılandırma Workpath** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-196">On the **Workpath Configuration** section, click **Configure Workpath** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8f5b4-197">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="8f5b4-197">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_configure.png) 

10. <span data-ttu-id="8f5b4-199">Çoklu oturum açma yapılandırmak için **Workpath** yan, indirilen göndermek için ihtiyacınız **meta veri XML**, **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** için [Workpath destek ekibi](https://help.workpath.com).</span><span class="sxs-lookup"><span data-stu-id="8f5b4-199">To configure single sign-on on **Workpath** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Workpath support team](https://help.workpath.com).</span></span> 

> [!TIP]
> <span data-ttu-id="8f5b4-200">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="8f5b4-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8f5b4-201">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8f5b4-202">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8f5b4-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8f5b4-203">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8f5b4-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="8f5b4-204">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="8f5b4-206">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8f5b4-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8f5b4-207">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workpath-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8f5b4-209">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workpath-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8f5b4-211">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workpath-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8f5b4-213">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workpath-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8f5b4-215">a.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-215">a.</span></span> <span data-ttu-id="8f5b4-216">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8f5b4-217">b.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-217">b.</span></span> <span data-ttu-id="8f5b4-218">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8f5b4-219">c.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-219">c.</span></span> <span data-ttu-id="8f5b4-220">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8f5b4-221">d.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-221">d.</span></span> <span data-ttu-id="8f5b4-222">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-222">Click **Create**.</span></span>
 
### <a name="creating-a-workpath-test-user"></a><span data-ttu-id="8f5b4-223">Workpath test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8f5b4-223">Creating a Workpath test user</span></span>

<span data-ttu-id="8f5b4-224">Workpath sadece kullanıcı zaman sağlama destekler.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-224">Workpath supports Just in time user provisioning.</span></span> <span data-ttu-id="8f5b4-225">Kimlik doğrulamasından sonra kullanıcılar uygulamada otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-225">After authentication users are created in the application automatically.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8f5b4-226">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="8f5b4-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8f5b4-227">Bu bölümde, Britta Workpath için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workpath.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="8f5b4-229">**Workpath için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8f5b4-229">**To assign Britta Simon to Workpath, perform the following steps:**</span></span>

1. <span data-ttu-id="8f5b4-230">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="8f5b4-232">Uygulamalar listesinde **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-232">In the applications list, select **Workpath**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_app.png) 

3. <span data-ttu-id="8f5b4-234">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="8f5b4-236">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-236">Click **Add** button.</span></span> <span data-ttu-id="8f5b4-237">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="8f5b4-239">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8f5b4-240">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8f5b4-241">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8f5b4-242">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="8f5b4-242">Testing single sign-on</span></span>

<span data-ttu-id="8f5b4-243">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8f5b4-244">Erişim paneli Workpath parçasında tıklattığınızda, otomatik olarak Workpath uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-244">When you click the Workpath tile in the Access Panel, you should get automatically signed-on to your Workpath application.</span></span>
<span data-ttu-id="8f5b4-245">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8f5b4-245">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8f5b4-246">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8f5b4-246">Additional resources</span></span>

* [<span data-ttu-id="8f5b4-247">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="8f5b4-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8f5b4-248">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="8f5b4-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_203.png

