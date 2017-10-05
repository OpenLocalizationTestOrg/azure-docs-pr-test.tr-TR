---
title: "Öğretici: Azure Active Directory Tümleştirme M dosyalarla | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve M dosyaları arasındaki yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f2682cf7cd3e11a5a7156938fbe9d4c7f541312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="e8673-103">Öğretici: M-dosyalar Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="e8673-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="e8673-104">Bu öğreticide, Azure Active Directory (Azure AD) ile tümleştirme M dosyalarını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e8673-104">In this tutorial, you learn how to integrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e8673-105">M-dosyaları Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e8673-105">Integrating M-Files with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e8673-106">M-dosyaları erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e8673-106">You can control in Azure AD who has access to M-Files</span></span>
- <span data-ttu-id="e8673-107">Otomatik olarak M-dosyaları (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e8673-107">You can enable your users to automatically get signed-on to M-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e8673-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="e8673-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e8673-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e8673-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8673-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e8673-110">Prerequisites</span></span>

<span data-ttu-id="e8673-111">M-dosyalar ile Azure AD tümleştirme yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="e8673-111">To configure Azure AD integration with M-Files, you need the following items:</span></span>

- <span data-ttu-id="e8673-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e8673-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e8673-113">Bir M dosyaları çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="e8673-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e8673-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e8673-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e8673-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e8673-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e8673-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e8673-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e8673-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e8673-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e8673-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e8673-118">Scenario description</span></span>
<span data-ttu-id="e8673-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e8673-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e8673-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e8673-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e8673-121">M-dosyaların Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="e8673-121">Adding M-Files from the gallery</span></span>
2. <span data-ttu-id="e8673-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e8673-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-the-gallery"></a><span data-ttu-id="e8673-123">M-dosyaların Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="e8673-123">Adding M-Files from the gallery</span></span>
<span data-ttu-id="e8673-124">Azure AD M dosyaları tümleştirilmesi yapılandırmak için M dosyaların Galeriden yönetilen SaaS uygulamaları listenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8673-124">To configure the integration of M-Files into Azure AD, you need to add M-Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e8673-125">**M-dosyaların Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e8673-125">**To add M-Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e8673-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e8673-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e8673-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e8673-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e8673-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e8673-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="e8673-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e8673-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="e8673-133">Arama kutusuna **M dosyaları**.</span><span class="sxs-lookup"><span data-stu-id="e8673-133">In the search box, type **M-Files**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. <span data-ttu-id="e8673-135">Sonuçlar panelinde seçin **M dosyaları**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e8673-135">In the results panel, select **M-Files**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e8673-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e8673-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e8673-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı göre M-dosyalar ile test etme.</span><span class="sxs-lookup"><span data-stu-id="e8673-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e8673-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen M dosyalarında bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="e8673-139">For single sign-on to work, Azure AD needs to know what the counterpart user in M-Files is to a user in Azure AD.</span></span> <span data-ttu-id="e8673-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı M dosyalarında arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8673-140">In other words, a link relationship between an Azure AD user and the related user in M-Files needs to be established.</span></span>

<span data-ttu-id="e8673-141">M-dosyalarında değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="e8673-141">In M-Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e8673-142">Yapılandırmak ve Azure AD çoklu oturum açma M dosyalarla sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e8673-142">To configure and test Azure AD single sign-on with M-Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e8673-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e8673-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e8673-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="e8673-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e8673-145">**[M-dosyaları test kullanıcısı oluşturma](#creating-a-m-files-test-user)**  - Britta Simon M dosyalarında kullanıcı Azure AD gösterimini bağlı, karşılık gelen sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="e8673-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - to have a counterpart of Britta Simon in M-Files that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e8673-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e8673-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e8673-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e8673-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e8673-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e8673-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e8673-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma M dosyaları uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e8673-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="e8673-150">**Azure AD çoklu oturum açma M dosyalarıyla yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e8673-150">**To configure Azure AD single sign-on with M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="e8673-151">Azure portalında üzerinde **M dosyaları** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e8673-151">In the Azure portal, on the **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="e8673-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e8673-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. <span data-ttu-id="e8673-155">Üzerinde **M dosyaları etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e8673-155">On the **M-Files Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="e8673-157">a.</span><span class="sxs-lookup"><span data-stu-id="e8673-157">a.</span></span> <span data-ttu-id="e8673-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="e8673-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="e8673-159">b.</span><span class="sxs-lookup"><span data-stu-id="e8673-159">b.</span></span> <span data-ttu-id="e8673-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<tenantname>.cloudvault.m-files.com`</span><span class="sxs-lookup"><span data-stu-id="e8673-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e8673-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="e8673-161">These values are not real.</span></span> <span data-ttu-id="e8673-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e8673-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e8673-163">Kişi [M dosyaları istemci destek ekibi](mailto:support@m-files.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="e8673-163">Contact [M-Files Client support team](mailto:support@m-files.com) to get these values.</span></span> 
 
4. <span data-ttu-id="e8673-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e8673-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. <span data-ttu-id="e8673-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e8673-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e8673-168">Uygulamanız için yapılandırılmış SSO almak için başvurun [M dosyaları destek ekibi](mailto:support@m-files.com) ve indirilen meta veri sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8673-168">To get SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them the downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="e8673-169">SSO, M dosya masaüstü uygulaması yapılandırmak istiyorsanız, sonraki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e8673-169">Follow the next steps if you want to configure SSO for you M-File desktop application.</span></span> <span data-ttu-id="e8673-170">Yalnızca SSO M dosyaları web sürümü için yapılandırmak istiyorsanız, hiçbir ek adım gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="e8673-170">No extra steps are required if you only want to configure SSO for M-Files web version.</span></span>  

7. <span data-ttu-id="e8673-171">Azure AD ile SSO'yu etkinleştirmek için M dosya masaüstü uygulaması yapılandırmak için sonraki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e8673-171">Follow the next steps to configure the M-File desktop application to enable SSO with Azure AD.</span></span> <span data-ttu-id="e8673-172">M-dosyalarını indirmek için Git [M dosyaları karşıdan](https://www.m-files.com/en/download-latest-version) sayfası.</span><span class="sxs-lookup"><span data-stu-id="e8673-172">To download M-Files, go to [M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

8. <span data-ttu-id="e8673-173">Açık **M dosyaları masaüstü ayarlarını** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e8673-173">Open the **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="e8673-174">Ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e8673-174">Then, click **Add**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. <span data-ttu-id="e8673-176">Üzerinde **belge kasası bağlantı özelliklerini** penceresinde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e8673-176">On the **Document Vault Connection Properties** window, perform the following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="e8673-178">Sunucunun altında türü, değerleri aşağıdaki gibi bölümünde:</span><span class="sxs-lookup"><span data-stu-id="e8673-178">Under the Server section type, the values as follows:</span></span>  

    <span data-ttu-id="e8673-179">a.</span><span class="sxs-lookup"><span data-stu-id="e8673-179">a.</span></span> <span data-ttu-id="e8673-180">İçin **adı**, türü `<tenant-name>.cloudvault.m-files.com`.</span><span class="sxs-lookup"><span data-stu-id="e8673-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="e8673-181">b.</span><span class="sxs-lookup"><span data-stu-id="e8673-181">b.</span></span> <span data-ttu-id="e8673-182">İçin **bağlantı noktası numarası**, türü **4466**.</span><span class="sxs-lookup"><span data-stu-id="e8673-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="e8673-183">c.</span><span class="sxs-lookup"><span data-stu-id="e8673-183">c.</span></span> <span data-ttu-id="e8673-184">İçin **Protokolü**seçin **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="e8673-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="e8673-185">d.</span><span class="sxs-lookup"><span data-stu-id="e8673-185">d.</span></span> <span data-ttu-id="e8673-186">İçinde **kimlik doğrulaması** alan, select **belirli Windows kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="e8673-186">In the **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="e8673-187">Ardından, bir imzalama sayfası istenir.</span><span class="sxs-lookup"><span data-stu-id="e8673-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="e8673-188">Azure AD kimlik bilgilerinizi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e8673-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="e8673-189">e.</span><span class="sxs-lookup"><span data-stu-id="e8673-189">e.</span></span> <span data-ttu-id="e8673-190">İçin **kasası sunucuda**, sunucuda karşılık gelen kasayı seçin.</span><span class="sxs-lookup"><span data-stu-id="e8673-190">For the **Vault on Server**,  select the corresponding vault on server.</span></span>
 
    <span data-ttu-id="e8673-191">f.</span><span class="sxs-lookup"><span data-stu-id="e8673-191">f.</span></span> <span data-ttu-id="e8673-192">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e8673-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="e8673-193">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e8673-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e8673-194">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="e8673-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e8673-195">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e8673-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e8673-196">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e8673-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="e8673-197">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="e8673-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="e8673-199">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e8673-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e8673-200">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e8673-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e8673-202">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e8673-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e8673-204">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="e8673-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e8673-206">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e8673-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e8673-208">a.</span><span class="sxs-lookup"><span data-stu-id="e8673-208">a.</span></span> <span data-ttu-id="e8673-209">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e8673-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e8673-210">b.</span><span class="sxs-lookup"><span data-stu-id="e8673-210">b.</span></span> <span data-ttu-id="e8673-211">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="e8673-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e8673-212">c.</span><span class="sxs-lookup"><span data-stu-id="e8673-212">c.</span></span> <span data-ttu-id="e8673-213">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="e8673-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e8673-214">d.</span><span class="sxs-lookup"><span data-stu-id="e8673-214">d.</span></span> <span data-ttu-id="e8673-215">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e8673-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="e8673-216">M-dosyaları test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e8673-216">Creating a M-Files test user</span></span>

<span data-ttu-id="e8673-217">Bu bölümün amacı M dosyalarında Britta Simon adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="e8673-217">The objective of this section is to create a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="e8673-218">Çalışmak [M dosyaları destek ekibi](mailto:support@m-files.com) M dosyalarında kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="e8673-218">Work with  [M-Files support team](mailto:support@m-files.com) to add the users in the M-Files.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e8673-219">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="e8673-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e8673-220">Bu bölümde, Britta M dosyalara erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e8673-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to M-Files.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="e8673-222">**M-dosyaları Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e8673-222">**To assign Britta Simon to M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="e8673-223">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e8673-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e8673-225">Uygulamalar listesinde **M dosyaları**.</span><span class="sxs-lookup"><span data-stu-id="e8673-225">In the applications list, select **M-Files**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. <span data-ttu-id="e8673-227">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e8673-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="e8673-229">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e8673-229">Click **Add** button.</span></span> <span data-ttu-id="e8673-230">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e8673-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="e8673-232">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e8673-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e8673-233">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e8673-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e8673-234">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e8673-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e8673-235">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e8673-235">Testing single sign-on</span></span>

<span data-ttu-id="e8673-236">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="e8673-236">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="e8673-237">Erişim paneli M dosyaları parçasında tıklattığınızda, otomatik olarak dosyaları M uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="e8673-237">When you click the M-Files tile in the Access Panel, you should get automatically signed-on to your M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e8673-238">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e8673-238">Additional resources</span></span>

* [<span data-ttu-id="e8673-239">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="e8673-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e8673-240">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e8673-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

