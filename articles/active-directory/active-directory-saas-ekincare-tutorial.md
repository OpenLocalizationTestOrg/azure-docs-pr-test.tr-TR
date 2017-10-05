---
title: "Öğretici: Azure Active Directory Tümleştirme ile eKincare | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile eKincare arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 57f56d14-83cf-4cbb-b342-fac4fc60078f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 014eaff14974bb6cd551b6fe53409ede6a6dfea1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ekincare"></a><span data-ttu-id="bdf3f-103">Öğretici: Azure Active Directory Tümleştirme eKincare ile</span><span class="sxs-lookup"><span data-stu-id="bdf3f-103">Tutorial: Azure Active Directory integration with eKincare</span></span>

<span data-ttu-id="bdf3f-104">Bu öğreticide, Azure Active Directory (Azure AD) ile eKincare tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-104">In this tutorial, you learn how to integrate eKincare with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bdf3f-105">EKincare Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="bdf3f-105">Integrating eKincare with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bdf3f-106">EKincare erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="bdf3f-106">You can control in Azure AD who has access to eKincare</span></span>
- <span data-ttu-id="bdf3f-107">Otomatik olarak Azure AD hesaplarına sahip (çoklu oturum açma) eKincare için açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="bdf3f-107">You can enable your users to automatically get signed-on to eKincare (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bdf3f-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="bdf3f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bdf3f-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bdf3f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdf3f-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bdf3f-110">Prerequisites</span></span>

<span data-ttu-id="bdf3f-111">Azure AD tümleştirme eKincare ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="bdf3f-111">To configure Azure AD integration with eKincare, you need the following items:</span></span>

- <span data-ttu-id="bdf3f-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="bdf3f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bdf3f-113">Bir eKincare çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="bdf3f-113">A eKincare single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bdf3f-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bdf3f-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="bdf3f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bdf3f-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bdf3f-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bdf3f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bdf3f-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="bdf3f-118">Scenario description</span></span>
<span data-ttu-id="bdf3f-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bdf3f-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="bdf3f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bdf3f-121">Galeriden eKincare ekleme</span><span class="sxs-lookup"><span data-stu-id="bdf3f-121">Adding eKincare from the gallery</span></span>
2. <span data-ttu-id="bdf3f-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="bdf3f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ekincare-from-the-gallery"></a><span data-ttu-id="bdf3f-123">Galeriden eKincare ekleme</span><span class="sxs-lookup"><span data-stu-id="bdf3f-123">Adding eKincare from the gallery</span></span>
<span data-ttu-id="bdf3f-124">Azure AD eKincare tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden eKincare eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-124">To configure the integration of eKincare into Azure AD, you need to add eKincare from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bdf3f-125">**Galeriden eKincare eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bdf3f-125">**To add eKincare from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bdf3f-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bdf3f-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bdf3f-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="bdf3f-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="bdf3f-133">Arama kutusuna **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-133">In the search box, type **eKincare**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_search.png)

5. <span data-ttu-id="bdf3f-135">Sonuçlar panelinde seçin **eKincare**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-135">In the results panel, select **eKincare**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bdf3f-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="bdf3f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bdf3f-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı eKincare ile test etme</span><span class="sxs-lookup"><span data-stu-id="bdf3f-138">In this section, you configure and test Azure AD single sign-on with eKincare based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bdf3f-139">Tekli çalışmaya oturum için Azure AD eKincare karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in eKincare is to a user in Azure AD.</span></span> <span data-ttu-id="bdf3f-140">Diğer bir deyişle, bir Azure AD kullanıcısının eKincare ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-140">In other words, a link relationship between an Azure AD user and the related user in eKincare needs to be established.</span></span>

<span data-ttu-id="bdf3f-141">EKincare içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-141">In eKincare, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bdf3f-142">Yapılandırma ve Azure AD çoklu oturum açma eKincare ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="bdf3f-142">To configure and test Azure AD single sign-on with eKincare, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bdf3f-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bdf3f-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bdf3f-145">**[EKincare test kullanıcısı oluşturma](#creating-a-ekincare-test-user)**  - bir Britta Simon karşılık gelen kullanıcı Azure AD gösterimini bağlı eKincare içinde olması.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-145">**[Creating a eKincare test user](#creating-a-ekincare-test-user)** - to have a counterpart of Britta Simon in eKincare that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bdf3f-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bdf3f-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bdf3f-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bdf3f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bdf3f-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma eKincare uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eKincare application.</span></span>

<span data-ttu-id="bdf3f-150">**Azure AD çoklu oturum açma ile eKincare yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bdf3f-150">**To configure Azure AD single sign-on with eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="bdf3f-151">Azure portalında üzerinde **eKincare** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-151">In the Azure portal, on the **eKincare** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="bdf3f-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_samlbase.png)

3. <span data-ttu-id="bdf3f-155">Üzerinde **eKincare etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bdf3f-155">On the **eKincare Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_url.png)

    <span data-ttu-id="bdf3f-157">a.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-157">a.</span></span> <span data-ttu-id="bdf3f-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<instancename>.ekincare.com/`</span><span class="sxs-lookup"><span data-stu-id="bdf3f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/`</span></span>

    <span data-ttu-id="bdf3f-159">b.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-159">b.</span></span> <span data-ttu-id="bdf3f-160">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<instancename>.ekincare.com/hul/saml`</span><span class="sxs-lookup"><span data-stu-id="bdf3f-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/hul/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bdf3f-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-161">These values are not real.</span></span> <span data-ttu-id="bdf3f-162">Bu değerler gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="bdf3f-163">Kişi [eKincare destek ekibi](mailto:tech@ekincare.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-163">Contact [eKincare support team](mailto:tech@ekincare.com) to get these values.</span></span>
 
4. <span data-ttu-id="bdf3f-164">eKincare uygulaması SAML onaylar belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-164">eKincare application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="bdf3f-165">Bu uygulama için aşağıdaki talep yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-165">Configure the following claims for this application.</span></span> <span data-ttu-id="bdf3f-166">Bu öznitelik değerlerini yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="bdf3f-167">Aşağıdaki ekran görüntüsünde, bu yapılandırma için bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-167">The following screenshot shows an example for this configuration.</span></span>

    <span data-ttu-id="bdf3f-168">Talep adı her zaman olacaktır **"EmployeeID"** ve hangisinin biz eşlenen kullanıcı EmployeeID içeren user.extensionattribute1 için değer.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-168">The claim name will always be **"employeeid"** and the value of which we have mapped to user.extensionattribute1, that contains the employeeid of the user.</span></span> <span data-ttu-id="bdf3f-169">Diğer iki talep adı yani</span><span class="sxs-lookup"><span data-stu-id="bdf3f-169">The other two claims' name i.e</span></span> <span data-ttu-id="bdf3f-170">**"organizationid"** ve **"Kuruluş adı"** her zaman aynı olacaktır ve bunların değerleri sırasıyla kullanıcının ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-170">**"organizationid"** and **"organizationname"** will always be same and their values contain the details of the organization of the user respectively.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ekincare-tutorial/attribute.png)
    
5. <span data-ttu-id="bdf3f-172">İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** iletişim kutusunda, yukarıdaki resimde gösterildiği gibi SAML belirteci özniteliği yapılandırın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bdf3f-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="bdf3f-173">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="bdf3f-173">Attribute Name</span></span> | <span data-ttu-id="bdf3f-174">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="bdf3f-174">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="bdf3f-175">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="bdf3f-175">employeeid</span></span> | <span data-ttu-id="bdf3f-176">*User.extensionattribute1*</span><span class="sxs-lookup"><span data-stu-id="bdf3f-176">*user.extensionattribute1*</span></span> |
    | <span data-ttu-id="bdf3f-177">organizationid</span><span class="sxs-lookup"><span data-stu-id="bdf3f-177">organizationid</span></span> | <span data-ttu-id="bdf3f-178">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="bdf3f-178">*"uniquevalue"*</span></span> |
    | <span data-ttu-id="bdf3f-179">Kuruluş adı</span><span class="sxs-lookup"><span data-stu-id="bdf3f-179">organizationname</span></span> | <span data-ttu-id="bdf3f-180">*User.CompanyName*</span><span class="sxs-lookup"><span data-stu-id="bdf3f-180">*user.companyname*</span></span> |

    <span data-ttu-id="bdf3f-181">a.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-181">a.</span></span> <span data-ttu-id="bdf3f-182">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-182">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ekincare-tutorial/04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ekincare-tutorial/05.png)
    
    <span data-ttu-id="bdf3f-185">b.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-185">b.</span></span> <span data-ttu-id="bdf3f-186">İçinde **adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="bdf3f-187">c.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-187">c.</span></span> <span data-ttu-id="bdf3f-188">Gelen **değeri** listesinde, ilgili satır için gösterilen öznitelik değeri yazın.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-188">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="bdf3f-189">d.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-189">d.</span></span> <span data-ttu-id="bdf3f-190">Tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="bdf3f-190">Click **Ok**</span></span>

6. <span data-ttu-id="bdf3f-191">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_certificate.png) 

7. <span data-ttu-id="bdf3f-193">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-193">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ekincare-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="bdf3f-195">Çoklu oturum açma yapılandırmak için **eKincare** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [eKincare destek ekibi](mailto:tech@ekincare.com).</span><span class="sxs-lookup"><span data-stu-id="bdf3f-195">To configure single sign-on on **eKincare** side, you need to send the downloaded **Metadata XML** to [eKincare support team](mailto:tech@ekincare.com).</span></span> <span data-ttu-id="bdf3f-196">Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-196">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="bdf3f-197">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="bdf3f-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bdf3f-198">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bdf3f-199">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bdf3f-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bdf3f-200">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bdf3f-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="bdf3f-201">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="bdf3f-203">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bdf3f-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bdf3f-204">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ekincare-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bdf3f-206">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ekincare-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bdf3f-208">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ekincare-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bdf3f-210">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bdf3f-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ekincare-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bdf3f-212">a.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-212">a.</span></span> <span data-ttu-id="bdf3f-213">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bdf3f-214">b.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-214">b.</span></span> <span data-ttu-id="bdf3f-215">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bdf3f-216">c.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-216">c.</span></span> <span data-ttu-id="bdf3f-217">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bdf3f-218">d.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-218">d.</span></span> <span data-ttu-id="bdf3f-219">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-219">Click **Create**.</span></span>
 
### <a name="creating-a-ekincare-test-user"></a><span data-ttu-id="bdf3f-220">EKincare test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bdf3f-220">Creating a eKincare test user</span></span>

<span data-ttu-id="bdf3f-221">Uygulama, süresi kullanıcı sağlama ve kimlik doğrulama kullanıcılar uygulamada otomatik olarak oluşturulduktan sonra hemen destekler.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-221">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bdf3f-222">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="bdf3f-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bdf3f-223">Bu bölümde, Britta eKincare erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eKincare.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="bdf3f-225">**EKincare için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bdf3f-225">**To assign Britta Simon to eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="bdf3f-226">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="bdf3f-228">Uygulamalar listesinde **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-228">In the applications list, select **eKincare**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_app.png) 

3. <span data-ttu-id="bdf3f-230">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-230">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="bdf3f-232">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-232">Click **Add** button.</span></span> <span data-ttu-id="bdf3f-233">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="bdf3f-235">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bdf3f-236">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bdf3f-237">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bdf3f-238">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="bdf3f-238">Testing single sign-on</span></span>

<span data-ttu-id="bdf3f-239">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bdf3f-240">Erişim paneli eKincare parçasında tıklattığınızda, otomatik olarak eKincare uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="bdf3f-240">When you click the eKincare tile in the Access Panel, you should get automatically signed-on to your eKincare application.</span></span>
<span data-ttu-id="bdf3f-241">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="bdf3f-241">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bdf3f-242">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="bdf3f-242">Additional resources</span></span>

* [<span data-ttu-id="bdf3f-243">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="bdf3f-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bdf3f-244">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="bdf3f-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_203.png

