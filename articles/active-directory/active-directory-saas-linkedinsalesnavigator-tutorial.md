---
title: "Öğretici: Azure Active Directory Tümleştirme ile LinkedInSalesNavigator | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile LinkedInSalesNavigator arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7a9fa8f3-d611-4ffe-8d50-04e9586b24da
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: ef26a16e79d9c9b0654634960b57dc59827b2c24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-sales-navigator"></a><span data-ttu-id="ecf39-103">Öğretici: Azure Active Directory Tümleştirme ile LinkedIn satış Gezgini</span><span class="sxs-lookup"><span data-stu-id="ecf39-103">Tutorial: Azure Active Directory integration with LinkedIn Sales Navigator</span></span>

<span data-ttu-id="ecf39-104">Bu öğreticide, Azure Active Directory (Azure AD) ile LinkedIn satış Gezgini tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ecf39-104">In this tutorial, you learn how to integrate LinkedIn Sales Navigator with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ecf39-105">LinkedIn satış Gezgini Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="ecf39-105">Integrating LinkedIn Sales Navigator with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ecf39-106">LinkedIn satış Gezgini erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ecf39-106">You can control in Azure AD who has access to LinkedIn Sales Navigator</span></span>
- <span data-ttu-id="ecf39-107">Azure AD hesaplarına otomatik olarak (çoklu oturum açma) LinkedIn satış Gezgini açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ecf39-107">You can enable your users to automatically get signed-on to LinkedIn Sales Navigator (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ecf39-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="ecf39-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ecf39-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, Gözat [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ecf39-109">If you want to know more details about SaaS app integration with Azure AD, browse [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ecf39-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ecf39-110">Prerequisites</span></span>

<span data-ttu-id="ecf39-111">Azure AD tümleştirme LinkedIn satış Gezgini ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="ecf39-111">To configure Azure AD integration with LinkedIn Sales Navigator, you need the following items:</span></span>

- <span data-ttu-id="ecf39-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="ecf39-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ecf39-113">Bir LinkedIn satış Gezgini çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="ecf39-113">A LinkedIn Sales Navigator single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ecf39-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="ecf39-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ecf39-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ecf39-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ecf39-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmaktan kaçının.</span><span class="sxs-lookup"><span data-stu-id="ecf39-116">Avoid using your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ecf39-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ecf39-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ecf39-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="ecf39-118">Scenario description</span></span>
<span data-ttu-id="ecf39-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="ecf39-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ecf39-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="ecf39-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ecf39-121">Galeriden LinkedIn satış Gezgini ekleme</span><span class="sxs-lookup"><span data-stu-id="ecf39-121">Adding LinkedIn Sales Navigator from the gallery</span></span>
2. <span data-ttu-id="ecf39-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ecf39-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-sales-navigator-from-the-gallery"></a><span data-ttu-id="ecf39-123">Galeriden LinkedIn satış Gezgini ekleme</span><span class="sxs-lookup"><span data-stu-id="ecf39-123">Adding LinkedIn Sales Navigator from the gallery</span></span>
<span data-ttu-id="ecf39-124">Azure AD LinkedIn satış Gezgini tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden LinkedIn satış Gezgini eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecf39-124">To configure the integration of LinkedIn Sales Navigator into Azure AD, you need to add LinkedIn Sales Navigator from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ecf39-125">**Galeriden LinkedIn satış Gezgini eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ecf39-125">**To add LinkedIn Sales Navigator from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ecf39-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ecf39-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ecf39-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="ecf39-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ecf39-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ecf39-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="ecf39-131">Tıklatın **yeni uygulama** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ecf39-131">Click **New application** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="ecf39-133">Arama kutusuna **LinkedIn satış Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="ecf39-133">In the search box, type **LinkedIn Sales Navigator**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_search.png)

5. <span data-ttu-id="ecf39-135">Sonuçlar panelinde seçin **LinkedIn satış Gezgini**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ecf39-135">In the results panel, select **LinkedIn Sales Navigator**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ecf39-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ecf39-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ecf39-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma LinkedIn satış "Britta Simon" adlı bir test kullanıcı tabanlı Gezgini ile test etme.</span><span class="sxs-lookup"><span data-stu-id="ecf39-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Sales Navigator based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ecf39-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen LinkedIn satış Gezgininde bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="ecf39-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Sales Navigator is to a user in Azure AD.</span></span> <span data-ttu-id="ecf39-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı LinkedIn satış Gezgininde arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecf39-140">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Sales Navigator needs to be established.</span></span>

<span data-ttu-id="ecf39-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** LinkedIn satış Gezgininde.</span><span class="sxs-lookup"><span data-stu-id="ecf39-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Sales Navigator.</span></span>

<span data-ttu-id="ecf39-142">Yapılandırma ve Azure AD çoklu oturum açma LinkedIn satış Gezgini ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ecf39-142">To configure and test Azure AD single sign-on with LinkedIn Sales Navigator, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ecf39-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ecf39-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ecf39-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="ecf39-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ecf39-145">**[Bir LinkedIn satış Gezgini test kullanıcısı oluşturma](#creating-a-linkedin-sales-navigator-test-user)**  - LinkedIn satış Gezgininde, kullanıcının Azure AD gösterimini bağlı Britta Simon, karşılık gelen sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="ecf39-145">**[Creating a LinkedIn Sales Navigator test user](#creating-a-linkedin-sales-navigator-test-user)** - to have a counterpart of Britta Simon in LinkedIn Sales Navigator that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="ecf39-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ecf39-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ecf39-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ecf39-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ecf39-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ecf39-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ecf39-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma LinkedIn satış Gezgini uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ecf39-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Sales Navigator application.</span></span>

<span data-ttu-id="ecf39-150">**Azure AD çoklu oturum açma LinkedIn satış Gezgini ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ecf39-150">**To configure Azure AD single sign-on with LinkedIn Sales Navigator, perform the following steps:**</span></span>

1. <span data-ttu-id="ecf39-151">Azure portalında üzerinde **LinkedIn satış Gezgini** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="ecf39-151">In the Azure portal, on the **LinkedIn Sales Navigator** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="ecf39-153">Üzerinde **çoklu oturum açma** iletişim, **modu** seçin **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ecf39-153">On the **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_samlbase.png)

3. <span data-ttu-id="ecf39-155">Farklı web tarayıcısı penceresinde için oturum, **LinkedIn satış Gezgini** yönetici olarak Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="ecf39-155">In a different web browser window, sign-on to your **LinkedIn Sales Navigator** website as an administrator.</span></span>

4. <span data-ttu-id="ecf39-156">İçinde **hesap Merkezi'nde**, tıklatın **genel ayarları** altında **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="ecf39-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="ecf39-157">Ayrıca, seçin **satış Gezgini** aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="ecf39-157">Also, select **Sales Navigator** from the dropdown list.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="ecf39-159">Tıklatın **veya yük ve tek tek alanların formdan kopyalamak için burayı tıklatın** kopyalayıp **varlık kimliği** ve **onaylama tüketici erişim (ACS) Url**.</span><span class="sxs-lookup"><span data-stu-id="ecf39-159">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_031.png)

6. <span data-ttu-id="ecf39-161">Azure Portal'da altında **LinkedIn satış Gezgini etki alanı ve URL'leri** bölümünde, uygulamada yapılandırmak istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modunda başlatılır.</span><span class="sxs-lookup"><span data-stu-id="ecf39-161">On Azure portal, under **LinkedIn Sales Navigator Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url1.png)

    <span data-ttu-id="ecf39-163">a.</span><span class="sxs-lookup"><span data-stu-id="ecf39-163">a.</span></span> <span data-ttu-id="ecf39-164">İçinde **tanımlayıcısı** metin girin **varlık kimliği** LinkedIn portalından kopyalandığından</span><span class="sxs-lookup"><span data-stu-id="ecf39-164">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="ecf39-165">b.</span><span class="sxs-lookup"><span data-stu-id="ecf39-165">b.</span></span> <span data-ttu-id="ecf39-166">İçinde **yanıt URL'si** metin girin **onaylama tüketici erişim (ACS) Url** LinkedIn portalından kopyalandığından</span><span class="sxs-lookup"><span data-stu-id="ecf39-166">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="ecf39-167">Denetleyin **Göster Gelişmiş URL ayarları**, uygulamada yapılandırmak istiyorsanız **SP** modunda başlatılır.</span><span class="sxs-lookup"><span data-stu-id="ecf39-167">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url2.png)

    <span data-ttu-id="ecf39-169">İçinde **oturum açma URL'si** metin kutusuna, şu biçimi kullanarak değeri yazın:`https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span><span class="sxs-lookup"><span data-stu-id="ecf39-169">In the **Sign-on URL** textbox, type the value using the following pattern: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span></span>

8. <span data-ttu-id="ecf39-170">**LinkedIn satış Gezgini** uygulama SAML belirteci öznitelikleri yapılandırmanıza özel öznitelik eşlemelerini ekleyin gerektiren belirli bir biçimde SAML onaylar bekler.</span><span class="sxs-lookup"><span data-stu-id="ecf39-170">Your **LinkedIn Sales Navigator** application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="ecf39-171">Aşağıdaki ekran görüntüsünde bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="ecf39-171">The following screenshot shows an example.</span></span> <span data-ttu-id="ecf39-172">Varsayılan değer olan **kullanıcı tanımlayıcısı** olan **user.userprincipalname** ancak LinkedIn satış Gezgini kullanıcının e-posta adresiyle eşlenmesi için bekliyor.</span><span class="sxs-lookup"><span data-stu-id="ecf39-172">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Sales Navigator expects it to be mapped with the user's email address.</span></span> <span data-ttu-id="ecf39-173">Kullanabileceğiniz **user.mail** özniteliği listeden veya kuruluş yapılandırmanızı temel alarak uygun öznitelik değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="ecf39-173">You can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/updateusermail.png)
    
9. <span data-ttu-id="ecf39-175">İçinde **kullanıcı öznitelikleri** 'yi tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** ve özniteliklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ecf39-175">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="ecf39-176">Kullanıcı adında dört talep eklemesi gerekiyor **e-posta**, **departmanı**, **firstname**, ve **lastname** ve ile eşlenecek değer ise **user.mail**, **user.department**, **user.givenname**, ve **user.surname** sırasıyla</span><span class="sxs-lookup"><span data-stu-id="ecf39-176">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="ecf39-177">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="ecf39-177">Attribute Name</span></span> | <span data-ttu-id="ecf39-178">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="ecf39-178">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="ecf39-179">E-posta</span><span class="sxs-lookup"><span data-stu-id="ecf39-179">email</span></span>| <span data-ttu-id="ecf39-180">User.Mail</span><span class="sxs-lookup"><span data-stu-id="ecf39-180">user.mail</span></span> |
    | <span data-ttu-id="ecf39-181">Bölüm</span><span class="sxs-lookup"><span data-stu-id="ecf39-181">department</span></span>| <span data-ttu-id="ecf39-182">User.Department</span><span class="sxs-lookup"><span data-stu-id="ecf39-182">user.department</span></span> |
    | <span data-ttu-id="ecf39-183">FirstName</span><span class="sxs-lookup"><span data-stu-id="ecf39-183">firstname</span></span>| <span data-ttu-id="ecf39-184">User.givenName</span><span class="sxs-lookup"><span data-stu-id="ecf39-184">user.givenname</span></span> |
    | <span data-ttu-id="ecf39-185">Soyadı</span><span class="sxs-lookup"><span data-stu-id="ecf39-185">lastname</span></span>| <span data-ttu-id="ecf39-186">User.surname</span><span class="sxs-lookup"><span data-stu-id="ecf39-186">user.surname</span></span> |
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/userattribute.png)
    
    <span data-ttu-id="ecf39-188">a.</span><span class="sxs-lookup"><span data-stu-id="ecf39-188">a.</span></span> <span data-ttu-id="ecf39-189">Tıklayın **özniteliği eklemek** özniteliği iletişim kutusunu açın.</span><span class="sxs-lookup"><span data-stu-id="ecf39-189">Click on **Add Attribute** to open the attribute dialog.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_04.png)
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_05.png)
   
    <span data-ttu-id="ecf39-192">b.</span><span class="sxs-lookup"><span data-stu-id="ecf39-192">b.</span></span> <span data-ttu-id="ecf39-193">İçinde **adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="ecf39-193">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="ecf39-194">c.</span><span class="sxs-lookup"><span data-stu-id="ecf39-194">c.</span></span> <span data-ttu-id="ecf39-195">Gelen **değeri** listesinde, ilgili satır için gösterilen öznitelik değeri yazın.</span><span class="sxs-lookup"><span data-stu-id="ecf39-195">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ecf39-196">d.</span><span class="sxs-lookup"><span data-stu-id="ecf39-196">d.</span></span> <span data-ttu-id="ecf39-197">Tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="ecf39-197">Click **Ok**</span></span>

10. <span data-ttu-id="ecf39-198">Aşağıdaki adımları gerçekleştirin **adı** öznitelik -</span><span class="sxs-lookup"><span data-stu-id="ecf39-198">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="ecf39-199">a.</span><span class="sxs-lookup"><span data-stu-id="ecf39-199">a.</span></span> <span data-ttu-id="ecf39-200">Özniteliği açmak için tıklatın **öznitelik Düzenle** penceresi.</span><span class="sxs-lookup"><span data-stu-id="ecf39-200">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/url_update.png)

    <span data-ttu-id="ecf39-202">b.</span><span class="sxs-lookup"><span data-stu-id="ecf39-202">b.</span></span> <span data-ttu-id="ecf39-203">URL değerinden silme **ad alanı**.</span><span class="sxs-lookup"><span data-stu-id="ecf39-203">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="ecf39-204">c.</span><span class="sxs-lookup"><span data-stu-id="ecf39-204">c.</span></span> <span data-ttu-id="ecf39-205">Tıklatın **Tamam** ayarı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="ecf39-205">Click **Ok** to save the setting.</span></span>

11. <span data-ttu-id="ecf39-206">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ecf39-206">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_certificate.png) 

12. <span data-ttu-id="ecf39-208">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ecf39-208">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="ecf39-210">Git **LinkedIn yönetici ayarları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="ecf39-210">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="ecf39-211">Tıklatın **karşıya yükleme XML dosyası** Azure portalından indirdiğiniz meta veri XML dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ecf39-211">Click **Upload XML file** to upload the Metadata XML file that you have downloaded from the Azure portal.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="ecf39-213">Tıklatın **üzerinde** SSO'yu etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ecf39-213">Click **On** to enable SSO.</span></span> <span data-ttu-id="ecf39-214">SSO durumu değişir **bağlı** için **bağlandı**</span><span class="sxs-lookup"><span data-stu-id="ecf39-214">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_05.png)


> [!TIP]
> <span data-ttu-id="ecf39-216">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="ecf39-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ecf39-217">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="ecf39-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ecf39-218">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ecf39-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ecf39-219">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf39-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="ecf39-220">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="ecf39-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="ecf39-222">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ecf39-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ecf39-223">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ecf39-223">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ecf39-225">Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="ecf39-225">Go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ecf39-227">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ecf39-227">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ecf39-229">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ecf39-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ecf39-231">a.</span><span class="sxs-lookup"><span data-stu-id="ecf39-231">a.</span></span> <span data-ttu-id="ecf39-232">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ecf39-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ecf39-233">b.</span><span class="sxs-lookup"><span data-stu-id="ecf39-233">b.</span></span> <span data-ttu-id="ecf39-234">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="ecf39-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ecf39-235">c.</span><span class="sxs-lookup"><span data-stu-id="ecf39-235">c.</span></span> <span data-ttu-id="ecf39-236">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="ecf39-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ecf39-237">d.</span><span class="sxs-lookup"><span data-stu-id="ecf39-237">d.</span></span> <span data-ttu-id="ecf39-238">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecf39-238">Click **Create**.</span></span>
 
### <a name="creating-a-linkedin-sales-navigator-test-user"></a><span data-ttu-id="ecf39-239">Bir LinkedIn satış Gezgini test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf39-239">Creating a LinkedIn Sales Navigator test user</span></span>

<span data-ttu-id="ecf39-240">Bağlantılı satış Gezgin uygulaması sadece kullanıcı zamanı (JIT) sağlama ve kimlik doğrulama kullanıcılar uygulamada otomatik olarak oluşturulduktan sonra destekler.</span><span class="sxs-lookup"><span data-stu-id="ecf39-240">Linked Sales Navigator Application supports Just in Time (JIT) user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="ecf39-241">Etkinleştirme **otomatik olarak lisansları atama** kullanıcıya bir lisans atamak için.</span><span class="sxs-lookup"><span data-stu-id="ecf39-241">Activate **Automatically assign licenses** to assign a license to the user.</span></span>
   
   ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ecf39-243">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="ecf39-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ecf39-244">Bu bölümde, Britta LinkedIn satış Gezgini'ne erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ecf39-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Sales Navigator.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="ecf39-246">**LinkedIn satış Gezgini Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ecf39-246">**To assign Britta Simon to LinkedIn Sales Navigator, perform the following steps:**</span></span>

1. <span data-ttu-id="ecf39-247">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ecf39-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="ecf39-249">Uygulamalar listesinde **LinkedIn satış Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="ecf39-249">In the applications list, select **LinkedIn Sales Navigator**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_app.png) 

3. <span data-ttu-id="ecf39-251">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="ecf39-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="ecf39-253">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ecf39-253">Click **Add** button.</span></span> <span data-ttu-id="ecf39-254">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ecf39-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="ecf39-256">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="ecf39-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ecf39-257">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ecf39-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ecf39-258">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ecf39-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ecf39-259">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="ecf39-259">Testing single sign-on</span></span>

<span data-ttu-id="ecf39-260">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="ecf39-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ecf39-261">Erişim paneli LinkedIn satış Gezgini parçasında tıklattığınızda, kişisel LinkedIn hesap ayrıntılarını sağlamak için sahip olduğu kuruluş sayfasına yönlendirilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecf39-261">When you click the LinkedIn Sales Navigator tile in the Access Panel, you should be redirected to Organizational page where you have to provide your personal LinkedIn account details.</span></span> <span data-ttu-id="ecf39-262">Kişisel hesabınızı LinkedIn iş hesabınızla bağlar.</span><span class="sxs-lookup"><span data-stu-id="ecf39-262">It links your personal account with your LinkedIn business account.</span></span> <span data-ttu-id="ecf39-263">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="ecf39-263">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ecf39-264">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ecf39-264">Additional resources</span></span>

* [<span data-ttu-id="ecf39-265">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="ecf39-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ecf39-266">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="ecf39-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_203.png

