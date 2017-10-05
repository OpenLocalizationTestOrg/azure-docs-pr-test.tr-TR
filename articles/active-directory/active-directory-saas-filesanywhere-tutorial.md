---
title: "Öğretici: Azure Active Directory Tümleştirme ile FilesAnywhere | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile FilesAnywhere arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 4153056bd21006061c6ad8ff9cf3c17de9248628
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a><span data-ttu-id="e9b54-103">Öğretici: Azure Active Directory Tümleştirme FilesAnywhere ile</span><span class="sxs-lookup"><span data-stu-id="e9b54-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span></span>

<span data-ttu-id="e9b54-104">Bu öğreticide, Azure Active Directory (Azure AD) ile FilesAnywhere tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e9b54-104">In this tutorial, you learn how to integrate FilesAnywhere with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e9b54-105">FilesAnywhere Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e9b54-105">Integrating FilesAnywhere with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e9b54-106">FilesAnywhere erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e9b54-106">You can control in Azure AD who has access to FilesAnywhere</span></span>
- <span data-ttu-id="e9b54-107">Otomatik olarak için FilesAnywhere (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e9b54-107">You can enable your users to automatically get signed-on to FilesAnywhere (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e9b54-108">Hesaplarınızı bir merkezi konumda - Azure Yönetim Portalı'nı yönetme</span><span class="sxs-lookup"><span data-stu-id="e9b54-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="e9b54-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e9b54-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9b54-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e9b54-110">Prerequisites</span></span>

<span data-ttu-id="e9b54-111">Azure AD tümleştirme FilesAnywhere ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="e9b54-111">To configure Azure AD integration with FilesAnywhere, you need the following items:</span></span>

- <span data-ttu-id="e9b54-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e9b54-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e9b54-113">Bir FilesAnywhere çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="e9b54-113">A FilesAnywhere single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="e9b54-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e9b54-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="e9b54-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e9b54-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e9b54-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9b54-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="e9b54-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9b54-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="e9b54-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e9b54-118">Scenario description</span></span>
<span data-ttu-id="e9b54-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e9b54-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e9b54-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e9b54-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e9b54-121">Galeriden FilesAnywhere ekleme</span><span class="sxs-lookup"><span data-stu-id="e9b54-121">Adding FilesAnywhere from the gallery</span></span>
2. <span data-ttu-id="e9b54-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e9b54-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-filesanywhere-from-the-gallery"></a><span data-ttu-id="e9b54-123">Galeriden FilesAnywhere ekleme</span><span class="sxs-lookup"><span data-stu-id="e9b54-123">Adding FilesAnywhere from the gallery</span></span>
<span data-ttu-id="e9b54-124">Azure AD FilesAnywhere tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden FilesAnywhere eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9b54-124">To configure the integration of FilesAnywhere into Azure AD, you need to add FilesAnywhere from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e9b54-125">**Galeriden FilesAnywhere eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e9b54-125">**To add FilesAnywhere from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e9b54-126">İçinde  **[Azure Yönetim Portalı](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e9b54-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e9b54-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e9b54-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e9b54-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e9b54-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="e9b54-131">Tıklatın **Ekle** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e9b54-131">Click **Add** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="e9b54-133">Arama kutusuna **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="e9b54-133">In the search box, type **FilesAnywhere**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. <span data-ttu-id="e9b54-135">Sonuçlar panelinde seçin **FilesAnywhere**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e9b54-135">In the results panel, select **FilesAnywhere**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e9b54-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e9b54-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e9b54-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı FilesAnywhere sınayın.</span><span class="sxs-lookup"><span data-stu-id="e9b54-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e9b54-139">Tekli çalışmaya oturum için Azure AD FilesAnywhere karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="e9b54-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FilesAnywhere is to a user in Azure AD.</span></span> <span data-ttu-id="e9b54-140">Diğer bir deyişle, bir Azure AD kullanıcısının FilesAnywhere ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9b54-140">In other words, a link relationship between an Azure AD user and the related user in FilesAnywhere needs to be established.</span></span>

<span data-ttu-id="e9b54-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** FilesAnywhere içinde.</span><span class="sxs-lookup"><span data-stu-id="e9b54-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FilesAnywhere.</span></span>

<span data-ttu-id="e9b54-142">Yapılandırma ve Azure AD çoklu oturum açma FilesAnywhere ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e9b54-142">To configure and test Azure AD single sign-on with FilesAnywhere, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e9b54-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e9b54-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e9b54-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="e9b54-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e9b54-145">**[FilesAnywhere test kullanıcısı oluşturma](#creating-a-filesanywhere-test-user)**  - Britta Simon, karşılık gelen her, Azure AD gösterimine bağlı FilesAnywhere sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="e9b54-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - to have a counterpart of Britta Simon in FilesAnywhere that is linked to the Azure AD representation of her.</span></span>
3. <span data-ttu-id="e9b54-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e9b54-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
4. <span data-ttu-id="e9b54-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e9b54-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e9b54-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e9b54-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e9b54-149">Bu bölümde, Azure AD çoklu oturum açma Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma FilesAnywhere uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e9b54-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FilesAnywhere application.</span></span>

<span data-ttu-id="e9b54-150">**Azure AD çoklu oturum açma ile FilesAnywhere yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e9b54-150">**To configure Azure AD single sign-on with FilesAnywhere, perform the following steps:**</span></span>

1. <span data-ttu-id="e9b54-151">Azure Yönetim Portalı'nda üzerinde **FilesAnywhere** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e9b54-151">In the Azure Management portal, on the **FilesAnywhere** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="e9b54-153">Üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e9b54-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. <span data-ttu-id="e9b54-155">Üzerinde **FilesAnywhere etki alanı ve URL'leri** uygulamada yapılandırmak istiyorsanız, bölüm **IDP başlatılan modu**:</span><span class="sxs-lookup"><span data-stu-id="e9b54-155">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    <span data-ttu-id="e9b54-157">a.</span><span class="sxs-lookup"><span data-stu-id="e9b54-157">a.</span></span> <span data-ttu-id="e9b54-158">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span><span class="sxs-lookup"><span data-stu-id="e9b54-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span></span>
> [!NOTE]
> <span data-ttu-id="e9b54-159">Lütfen unutmayın değeri **215** olan bir **ClientID** ve yalnızca bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="e9b54-159">Please note that the value **215** is a **clientid** and is just an example.</span></span> <span data-ttu-id="e9b54-160">Gerçek ClientID değeri ile değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9b54-160">You need to replace it with the actual clientid value.</span></span>

4. <span data-ttu-id="e9b54-161">Üzerinde **FilesAnywhere etki alanı ve URL'leri** uygulamada yapılandırmak istiyorsanız, bölüm **SP tarafından başlatılan modu**, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e9b54-161">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    <span data-ttu-id="e9b54-163">a.</span><span class="sxs-lookup"><span data-stu-id="e9b54-163">a.</span></span> <span data-ttu-id="e9b54-164">Tıklayın **Göster Gelişmiş URL ayarları** seçeneği</span><span class="sxs-lookup"><span data-stu-id="e9b54-164">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="e9b54-165">b.</span><span class="sxs-lookup"><span data-stu-id="e9b54-165">b.</span></span> <span data-ttu-id="e9b54-166">İçinde **oturum üzerinde URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<sub domain>.filesanywhere.com/`</span><span class="sxs-lookup"><span data-stu-id="e9b54-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<sub domain>.filesanywhere.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e9b54-167">Lütfen bu gerçek değerlerin olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e9b54-167">Please note that these are not the real values.</span></span> <span data-ttu-id="e9b54-168">Gerçek oturum üzerinde URL'si ve yanıt URL'si bu değerleri güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9b54-168">You have to update these values with the actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="e9b54-169">Kişi [FilesAnywhere destek ekibi](mailto:support@FilesAnywhere.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="e9b54-169">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) to get these values.</span></span> 

5. <span data-ttu-id="e9b54-170">FilesAnywhere yazılım uygulaması SAML onaylar belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="e9b54-170">FilesAnywhere Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="e9b54-171">Lütfen bu uygulama için aşağıdaki talep yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e9b54-171">Please configure the following claims for this application.</span></span> <span data-ttu-id="e9b54-172">Bu öznitelik değerlerini yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="e9b54-172">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="e9b54-173">Aşağıdaki ekran görüntüsünde bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="e9b54-173">The following screenshot shows an example for this.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    <span data-ttu-id="e9b54-175">Kullanıcılar oturum açtığında ile FilesAnywhere değeri elde **ClientID** özniteliğini [FilesAnywhere takım](mailto:support@FilesAnywhere.com).</span><span class="sxs-lookup"><span data-stu-id="e9b54-175">When the users signs up with FilesAnywhere they get the value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span></span> <span data-ttu-id="e9b54-176">FilesAnywhere tarafından sağlanan benzersiz değeri olan "İstemci kimliği" özniteliğini eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9b54-176">You have to add the "Client Id" attribute with the unique value provided by FilesAnywhere.</span></span> <span data-ttu-id="e9b54-177">Yukarıda gösterilen bu öznitelikler gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e9b54-177">All these attributes shown above are required.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="e9b54-178">Lütfen unutmayın değeri **2331** , **ClientID** yalnızca bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="e9b54-178">Please note that the value **2331** of **clientid** is just an example.</span></span> <span data-ttu-id="e9b54-179">Gerçek değer sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9b54-179">You need to provide the actual value.</span></span>


6. <span data-ttu-id="e9b54-180">İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** iletişim kutusunda, yukarıdaki resimde gösterildiği gibi SAML belirteci özniteliği yapılandırın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e9b54-180">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="e9b54-181">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="e9b54-181">Attribute Name</span></span> | <span data-ttu-id="e9b54-182">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="e9b54-182">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="e9b54-183">istemci kimliği</span><span class="sxs-lookup"><span data-stu-id="e9b54-183">clientid</span></span> | <span data-ttu-id="e9b54-184">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="e9b54-184">*"uniquevalue"*</span></span> |

    <span data-ttu-id="e9b54-185">a.</span><span class="sxs-lookup"><span data-stu-id="e9b54-185">a.</span></span> <span data-ttu-id="e9b54-186">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e9b54-186">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    <span data-ttu-id="e9b54-189">b.</span><span class="sxs-lookup"><span data-stu-id="e9b54-189">b.</span></span> <span data-ttu-id="e9b54-190">İçinde **adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="e9b54-190">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="e9b54-191">c.</span><span class="sxs-lookup"><span data-stu-id="e9b54-191">c.</span></span> <span data-ttu-id="e9b54-192">Gelen **değeri** listesinde, ilgili satır için gösterilen öznitelik değeri yazın.</span><span class="sxs-lookup"><span data-stu-id="e9b54-192">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="e9b54-193">d.</span><span class="sxs-lookup"><span data-stu-id="e9b54-193">d.</span></span> <span data-ttu-id="e9b54-194">Tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="e9b54-194">Click **Ok**</span></span>

7. <span data-ttu-id="e9b54-195">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e9b54-195">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e9b54-197">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e9b54-197">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. <span data-ttu-id="e9b54-199">Üzerinde **FilesAnywhere yapılandırma** 'yi tıklatın **yapılandırma FilesAnywhere** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e9b54-199">On the **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** to open **Configure sign-on** window.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. <span data-ttu-id="e9b54-202">SSO yapılandırma FilesAnywhere sonunda, uygulamanız için tam almak için başvurun [FilesAnywhere destek ekibi](mailto:support@FilesAnywhere.com) ve indirilen SAML belirteç imzalama sertifikası ve çoklu oturum açma (SSO) URL verin.</span><span class="sxs-lookup"><span data-stu-id="e9b54-202">To get SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them the downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e9b54-203">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e9b54-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="e9b54-204">Bu bölümün amacı, Britta Simon adlı Azure Yönetim Portalı'nda bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="e9b54-204">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="e9b54-206">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e9b54-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e9b54-207">İçinde **Azure Yönetim Portalı**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e9b54-207">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e9b54-209">Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="e9b54-209">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e9b54-211">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e9b54-211">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e9b54-213">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e9b54-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e9b54-215">a.</span><span class="sxs-lookup"><span data-stu-id="e9b54-215">a.</span></span> <span data-ttu-id="e9b54-216">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e9b54-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e9b54-217">b.</span><span class="sxs-lookup"><span data-stu-id="e9b54-217">b.</span></span> <span data-ttu-id="e9b54-218">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="e9b54-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e9b54-219">c.</span><span class="sxs-lookup"><span data-stu-id="e9b54-219">c.</span></span> <span data-ttu-id="e9b54-220">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="e9b54-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e9b54-221">d.</span><span class="sxs-lookup"><span data-stu-id="e9b54-221">d.</span></span> <span data-ttu-id="e9b54-222">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e9b54-222">Click **Create**.</span></span> 



### <a name="creating-a-filesanywhere-test-user"></a><span data-ttu-id="e9b54-223">FilesAnywhere test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e9b54-223">Creating a FilesAnywhere test user</span></span>

<span data-ttu-id="e9b54-224">Uygulama, süresi kullanıcı sağlama ve kimlik doğrulama kullanıcılar uygulamada otomatik olarak oluşturulacak sonra hemen destekler.</span><span class="sxs-lookup"><span data-stu-id="e9b54-224">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e9b54-225">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="e9b54-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e9b54-226">Bu bölümde, Britta FilesAnywhere için kendi erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e9b54-226">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FilesAnywhere.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="e9b54-228">**FilesAnywhere için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e9b54-228">**To assign Britta Simon to FilesAnywhere, perform the following steps:**</span></span>

1. <span data-ttu-id="e9b54-229">Azure Yönetim Portalı'nda uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e9b54-229">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e9b54-231">Uygulamalar listesinde **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="e9b54-231">In the applications list, select **FilesAnywhere**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. <span data-ttu-id="e9b54-233">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e9b54-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="e9b54-235">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e9b54-235">Click **Add** button.</span></span> <span data-ttu-id="e9b54-236">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e9b54-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="e9b54-238">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e9b54-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e9b54-239">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e9b54-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e9b54-240">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e9b54-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="e9b54-241">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e9b54-241">Testing single sign-on</span></span>

<span data-ttu-id="e9b54-242">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="e9b54-242">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e9b54-243">Erişim paneli FilesAnywhere parçasında tıklattığınızda, otomatik olarak FilesAnywhere uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="e9b54-243">When you click the FilesAnywhere tile in the Access Panel, you should get automatically signed-on to your FilesAnywhere application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="e9b54-244">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e9b54-244">Additional resources</span></span>

* [<span data-ttu-id="e9b54-245">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="e9b54-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e9b54-246">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e9b54-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
