---
title: "Öğretici: Azure Active Directory Tümleştirme github | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve GitHub arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 9dc12bc2e313bcb2000724d035156c5054d14e1c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="9bf31-103">Öğretici: Azure Active Directory Tümleştirme github</span><span class="sxs-lookup"><span data-stu-id="9bf31-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="9bf31-104">Bu öğreticide, Azure Active Directory (Azure AD) ile GitHub tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9bf31-104">In this tutorial, you learn how to integrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9bf31-105">GitHub Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="9bf31-105">Integrating GitHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9bf31-106">GitHub erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="9bf31-106">You can control in Azure AD who has access to GitHub</span></span>
- <span data-ttu-id="9bf31-107">Otomatik olarak için GitHub (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="9bf31-107">You can enable your users to automatically get signed-on to GitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9bf31-108">Hesaplarınızı bir merkezi konumda - Azure Yönetim Portalı'nı yönetme</span><span class="sxs-lookup"><span data-stu-id="9bf31-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="9bf31-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9bf31-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bf31-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9bf31-110">Prerequisites</span></span>

<span data-ttu-id="9bf31-111">Azure AD tümleştirme GitHub ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="9bf31-111">To configure Azure AD integration with GitHub, you need the following items:</span></span>

- <span data-ttu-id="9bf31-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="9bf31-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9bf31-113">Bir GitHub çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="9bf31-113">A GitHub single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="9bf31-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="9bf31-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="9bf31-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9bf31-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9bf31-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9bf31-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9bf31-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9bf31-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="9bf31-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="9bf31-118">Scenario description</span></span>
<span data-ttu-id="9bf31-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="9bf31-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9bf31-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="9bf31-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9bf31-121">Galeriden GitHub ekleme</span><span class="sxs-lookup"><span data-stu-id="9bf31-121">Adding GitHub from the gallery</span></span>
2. <span data-ttu-id="9bf31-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="9bf31-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-github-from-the-gallery"></a><span data-ttu-id="9bf31-123">Galeriden GitHub ekleme</span><span class="sxs-lookup"><span data-stu-id="9bf31-123">Adding GitHub from the gallery</span></span>
<span data-ttu-id="9bf31-124">Azure AD GitHub tümleştirilmesi yapılandırmak için GitHub Galeriden yönetilen SaaS uygulamaları listenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9bf31-124">To configure the integration of GitHub into Azure AD, you need to add GitHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9bf31-125">**Galeriden GitHub eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9bf31-125">**To add GitHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9bf31-126">İçinde  **[Azure Yönetim Portalı](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9bf31-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9bf31-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="9bf31-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9bf31-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9bf31-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="9bf31-131">Tıklatın **Ekle** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9bf31-131">Click **Add** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="9bf31-133">Arama kutusuna **Github.com'u**.</span><span class="sxs-lookup"><span data-stu-id="9bf31-133">In the search box, type **GitHub.com**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. <span data-ttu-id="9bf31-135">Sonuçlar panelinde seçin **GitHub**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9bf31-135">In the results panel, select **GitHub**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9bf31-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="9bf31-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9bf31-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı GitHub ile test etme.</span><span class="sxs-lookup"><span data-stu-id="9bf31-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9bf31-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen github bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="9bf31-139">For single sign-on to work, Azure AD needs to know what the counterpart user in GitHub is to a user in Azure AD.</span></span> <span data-ttu-id="9bf31-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı github'da arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9bf31-140">In other words, a link relationship between an Azure AD user and the related user in GitHub needs to be established.</span></span>

<span data-ttu-id="9bf31-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** github'da.</span><span class="sxs-lookup"><span data-stu-id="9bf31-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in GitHub.</span></span>

<span data-ttu-id="9bf31-142">Yapılandırma ve Azure AD çoklu oturum açma GitHub ile test etmek için aşağıdaki yapı taşları tamamlanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="9bf31-142">To configure and test Azure AD single sign-on with GitHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9bf31-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="9bf31-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9bf31-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="9bf31-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9bf31-145">**[GitHub test kullanıcısı oluşturma](#creating-a-GitHub-test-user)**  - Britta Simon, karşılık gelen her, Azure AD gösterimine bağlı GitHub sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="9bf31-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - to have a counterpart of Britta Simon in GitHub that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="9bf31-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="9bf31-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9bf31-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="9bf31-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9bf31-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9bf31-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9bf31-149">Bu bölümde, Azure AD çoklu oturum açma Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma GitHub uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9bf31-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="9bf31-150">**Azure AD çoklu oturum açma GitHub ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9bf31-150">**To configure Azure AD single sign-on with GitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="9bf31-151">Azure Yönetim Portalı'nda üzerinde **GitHub** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="9bf31-151">In the Azure Management portal, on the **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="9bf31-153">Üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="9bf31-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. <span data-ttu-id="9bf31-155">Üzerinde **GitHub etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9bf31-155">On the **GitHub Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    <span data-ttu-id="9bf31-157">a.</span><span class="sxs-lookup"><span data-stu-id="9bf31-157">a.</span></span> <span data-ttu-id="9bf31-158">İçinde **oturum açma URL'si** metin değeri olarak yazın:`https://github.com/orgs/<entity-id>/sso`</span><span class="sxs-lookup"><span data-stu-id="9bf31-158">In the **Sign-on URL** textbox, type the value as: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="9bf31-159">b.</span><span class="sxs-lookup"><span data-stu-id="9bf31-159">b.</span></span> <span data-ttu-id="9bf31-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://github.com/orgs/<entity-id>`</span><span class="sxs-lookup"><span data-stu-id="9bf31-160">In the **Identifier** textbox, type a URL using the following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9bf31-161">Lütfen bu gerçek değerlerin olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="9bf31-161">Please note that these are not the real values.</span></span> <span data-ttu-id="9bf31-162">Bu değerleri tanımlayıcısı ve gerçek oturum açma URL'si ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9bf31-162">You have to update these values with the actual Sing-on URL and Identifier.</span></span> <span data-ttu-id="9bf31-163">Burada dizesinin benzersiz değeri tanımlayıcıda kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="9bf31-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="9bf31-164">Bu değerleri almak için GitHub yönetici bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="9bf31-164">Go to GitHub Admin section to retrieve these values.</span></span> 

4. <span data-ttu-id="9bf31-165">Üzerinde **kullanıcı öznitelikleri** bölümünde, select **kullanıcı tanımlayıcısı** user.mail olarak.</span><span class="sxs-lookup"><span data-stu-id="9bf31-165">On the **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. <span data-ttu-id="9bf31-167">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **yeni sertifika oluştur**.</span><span class="sxs-lookup"><span data-stu-id="9bf31-167">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. <span data-ttu-id="9bf31-169">Üzerinde **yeni sertifika oluştur** iletişim kutusunda, Takvim simgesine tıklayın ve bir **sona erme tarihi**.</span><span class="sxs-lookup"><span data-stu-id="9bf31-169">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="9bf31-170">Ardından **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9bf31-170">Then click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="9bf31-172">Üzerinde **SAML imzalama sertifikası** bölümünde, select **yeni sertifika etkin hale getirin** tıklatıp **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9bf31-172">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. <span data-ttu-id="9bf31-174">Açılır pencere üzerinde **geçiş sertifikası** penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="9bf31-174">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="9bf31-176">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9bf31-176">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. <span data-ttu-id="9bf31-178">Üzerinde **GitHub yapılandırma** 'yi tıklatın **yapılandırma GitHub** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="9bf31-178">On the **GitHub Configuration** section, click **Configure GitHub** to open **Configure sign-on** window.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. <span data-ttu-id="9bf31-181">Farklı web tarayıcısı penceresinde GitHub kuruluş sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9bf31-181">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

12. <span data-ttu-id="9bf31-182">Gidin **ayarları** tıklatıp **güvenlik**</span><span class="sxs-lookup"><span data-stu-id="9bf31-182">Navigate to **Settings** and click **Security**</span></span>

    ![Ayarlar](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. <span data-ttu-id="9bf31-184">Denetleme **etkinleştirmek SAML kimlik doğrulaması** kutusu, çoklu oturum açma yapılandırma alanları ortaya.</span><span class="sxs-lookup"><span data-stu-id="9bf31-184">Check the **Enable SAML authentication** box, revealing the Single Sign-on configuration fields.</span></span> <span data-ttu-id="9bf31-185">Ardından, çoklu oturum açma URL'si Azure AD yapılandırmasını güncelleştirmek için tek oturum açma URL değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="9bf31-185">Then, use the single sign-on URL value to update the Single sign-on URL on Azure AD configuration.</span></span>

    ![Ayarlar](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. <span data-ttu-id="9bf31-187">Aşağıdaki alanları yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="9bf31-187">Configure the following fields:</span></span>

    <span data-ttu-id="9bf31-188">a.</span><span class="sxs-lookup"><span data-stu-id="9bf31-188">a.</span></span> <span data-ttu-id="9bf31-189">**URL üzerinde oturum**: girin **SAML çoklu oturum açma hizmet URL'si** gelen **yapılandırma GitHub** Azure AD bölüm</span><span class="sxs-lookup"><span data-stu-id="9bf31-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from the **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="9bf31-190">b.</span><span class="sxs-lookup"><span data-stu-id="9bf31-190">b.</span></span> <span data-ttu-id="9bf31-191">**Veren**: girin **SAML varlık kimliği** gelen **yapılandırma GitHub** Azure AD bölüm</span><span class="sxs-lookup"><span data-stu-id="9bf31-191">**Issuer**: Enter **SAML Entity ID** from the **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="9bf31-192">c.</span><span class="sxs-lookup"><span data-stu-id="9bf31-192">c.</span></span> <span data-ttu-id="9bf31-193">**Ortak sertifika**: indirilen sertifika Azure AD'den bir Not Defteri'nde açın ve "Sertifika başlayın" ve "Son SERTİFİKAYI" dahil olmak üzere içerik kopyalama</span><span class="sxs-lookup"><span data-stu-id="9bf31-193">**Public Certificate**: Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![Ayarlar](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. <span data-ttu-id="9bf31-195">Tıklayın **Test SAML Yapılandırması** onaylamak için hiçbir doğrulama hataları veya SSO sırasında hatalar.</span><span class="sxs-lookup"><span data-stu-id="9bf31-195">Click on **Test SAML configuration** to confirm that no validation failures or errors during SSO.</span></span>

    ![Ayarlar](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. <span data-ttu-id="9bf31-197">Tıklatın **Kaydet**</span><span class="sxs-lookup"><span data-stu-id="9bf31-197">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9bf31-198">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9bf31-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="9bf31-199">Bu bölümün amacı, Britta Simon adlı Azure Yönetim Portalı'nda bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="9bf31-199">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="9bf31-201">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9bf31-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9bf31-202">İçinde **Azure Yönetim Portalı**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9bf31-202">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9bf31-204">Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="9bf31-204">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9bf31-206">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9bf31-206">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9bf31-208">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9bf31-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9bf31-210">a.</span><span class="sxs-lookup"><span data-stu-id="9bf31-210">a.</span></span> <span data-ttu-id="9bf31-211">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9bf31-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9bf31-212">b.</span><span class="sxs-lookup"><span data-stu-id="9bf31-212">b.</span></span> <span data-ttu-id="9bf31-213">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="9bf31-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9bf31-214">c.</span><span class="sxs-lookup"><span data-stu-id="9bf31-214">c.</span></span> <span data-ttu-id="9bf31-215">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="9bf31-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9bf31-216">d.</span><span class="sxs-lookup"><span data-stu-id="9bf31-216">d.</span></span> <span data-ttu-id="9bf31-217">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9bf31-217">Click **Create**.</span></span> 


### <a name="creating-a-github-test-user"></a><span data-ttu-id="9bf31-218">GitHub test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9bf31-218">Creating a GitHub test user</span></span>

<span data-ttu-id="9bf31-219">Azure AD kullanıcıların GitHub oturum etkinleştirmek için bunların GitHub sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9bf31-219">In order to enable Azure AD users to log into GitHub, they must be provisioned into GitHub.</span></span>  
<span data-ttu-id="9bf31-220">GitHub söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="9bf31-220">In the case of GitHub, provisioning is a manual task.</span></span>

<span data-ttu-id="9bf31-221">**Kullanıcı hesaplarını sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9bf31-221">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="9bf31-222">GitHub şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9bf31-222">Log in to your GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="9bf31-223">Tıklatın **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="9bf31-223">Click **People**.</span></span>

    <span data-ttu-id="9bf31-224">![Kişiler](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "kişiler")</span><span class="sxs-lookup"><span data-stu-id="9bf31-224">![People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="9bf31-225">Tıklatın **davet üye**.</span><span class="sxs-lookup"><span data-stu-id="9bf31-225">Click **Invite member**.</span></span>

    <span data-ttu-id="9bf31-226">![Kullanıcıları davet](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "kullanıcıları davet et")</span><span class="sxs-lookup"><span data-stu-id="9bf31-226">![Invite Users](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="9bf31-227">Üzerinde **davet üye** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9bf31-227">On the **Invite member** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="9bf31-228">a.</span><span class="sxs-lookup"><span data-stu-id="9bf31-228">a.</span></span> <span data-ttu-id="9bf31-229">İçinde **e-posta** metin kutusuna, Britta Simon hesabı e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="9bf31-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="9bf31-230">![Kişileri davet edin](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "kişileri davet edin")</span><span class="sxs-lookup"><span data-stu-id="9bf31-230">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>
    
    <span data-ttu-id="9bf31-231">b.</span><span class="sxs-lookup"><span data-stu-id="9bf31-231">b.</span></span> <span data-ttu-id="9bf31-232">Tıklatın **Gönder davet**.</span><span class="sxs-lookup"><span data-stu-id="9bf31-232">Click **Send Invitation**.</span></span>

    <span data-ttu-id="9bf31-233">![Kişileri davet edin](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "kişileri davet edin")</span><span class="sxs-lookup"><span data-stu-id="9bf31-233">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="9bf31-234">Azure Active Directory hesap sahibi bir e-posta alır ve onu etkinleştirilmeden önce kendi hesabı onaylamak için bağlantıyı izleyin.</span><span class="sxs-lookup"><span data-stu-id="9bf31-234">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9bf31-235">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="9bf31-235">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9bf31-236">Bu bölümde, Britta GitHub için kendi erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9bf31-236">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to GitHub.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="9bf31-238">**GitHub için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9bf31-238">**To assign Britta Simon to GitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="9bf31-239">Azure Yönetim Portalı'nda uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9bf31-239">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="9bf31-241">Uygulamalar listesinde **Github.com'u**.</span><span class="sxs-lookup"><span data-stu-id="9bf31-241">In the applications list, select **GitHub.com**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. <span data-ttu-id="9bf31-243">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="9bf31-243">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="9bf31-245">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9bf31-245">Click **Add** button.</span></span> <span data-ttu-id="9bf31-246">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9bf31-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="9bf31-248">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="9bf31-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9bf31-249">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9bf31-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9bf31-250">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9bf31-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="9bf31-251">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="9bf31-251">Testing single sign-on</span></span>

<span data-ttu-id="9bf31-252">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="9bf31-252">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9bf31-253">Erişim paneli GitHub parçasında tıklattığınızda, GitHub uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="9bf31-253">When you click the GitHub tile in the Access Panel, you should get signed-on to your GitHub application.</span></span> <span data-ttu-id="9bf31-254">Hesap ancak sonra gerekirse, kişisel hesabıyla oturum kuruluş olarak günlüğü.</span><span class="sxs-lookup"><span data-stu-id="9bf31-254">You'll be logging in as an Organization account but then need to log in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9bf31-255">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="9bf31-255">Additional resources</span></span>

* [<span data-ttu-id="9bf31-256">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="9bf31-256">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9bf31-257">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="9bf31-257">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
