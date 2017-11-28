---
title: "Öğretici: Azure Active Directory Tümleştirme Mimecast kişisel portalıyla | Microsoft Docs"
description: "Çoklu oturum açma Mimecast kişisel Portal ile Azure Active Directory arasındaki yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: bf46da35a55608d7e4656c9dd3ad9d5f2253e225
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="65985-103">Öğretici: Azure Active Directory Tümleştirme Mimecast kişisel portalı ile</span><span class="sxs-lookup"><span data-stu-id="65985-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="65985-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Mimecast kişisel Portal tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="65985-104">In this tutorial, you learn how to integrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65985-105">Mimecast kişisel Portal Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="65985-105">Integrating Mimecast Personal Portal with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="65985-106">Mimecast kişisel Portal erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="65985-106">You can control in Azure AD who has access to Mimecast Personal Portal</span></span>
- <span data-ttu-id="65985-107">Azure AD hesaplarına otomatik olarak Mimecast kişisel portalına (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="65985-107">You can enable your users to automatically get signed-on to Mimecast Personal Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="65985-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="65985-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="65985-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65985-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65985-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="65985-110">Prerequisites</span></span>

<span data-ttu-id="65985-111">Azure AD tümleştirme Mimecast kişisel Portal ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="65985-111">To configure Azure AD integration with Mimecast Personal Portal, you need the following items:</span></span>

- <span data-ttu-id="65985-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="65985-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65985-113">Bir Mimecast kişisel Portal çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="65985-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65985-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="65985-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65985-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="65985-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65985-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="65985-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65985-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65985-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65985-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="65985-118">Scenario description</span></span>
<span data-ttu-id="65985-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="65985-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65985-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="65985-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65985-121">Galeriden Mimecast kişisel Portal ekleme</span><span class="sxs-lookup"><span data-stu-id="65985-121">Adding Mimecast Personal Portal from the gallery</span></span>
2. <span data-ttu-id="65985-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="65985-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-the-gallery"></a><span data-ttu-id="65985-123">Galeriden Mimecast kişisel Portal ekleme</span><span class="sxs-lookup"><span data-stu-id="65985-123">Adding Mimecast Personal Portal from the gallery</span></span>
<span data-ttu-id="65985-124">Azure AD Mimecast kişisel Portal tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Mimecast kişisel Portal eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="65985-124">To configure the integration of Mimecast Personal Portal into Azure AD, you need to add Mimecast Personal Portal from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="65985-125">**Galeriden Mimecast kişisel Portal eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="65985-125">**To add Mimecast Personal Portal from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="65985-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="65985-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="65985-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="65985-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="65985-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="65985-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="65985-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="65985-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="65985-133">Arama kutusuna **Mimecast kişisel Portal**.</span><span class="sxs-lookup"><span data-stu-id="65985-133">In the search box, type **Mimecast Personal Portal**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. <span data-ttu-id="65985-135">Sonuçlar panelinde seçin **Mimecast kişisel Portal**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="65985-135">In the results panel, select **Mimecast Personal Portal**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="65985-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="65985-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="65985-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Mimecast kişisel "Britta Simon" adlı bir test kullanıcı tabanlı Portal ile test etme.</span><span class="sxs-lookup"><span data-stu-id="65985-138">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="65985-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen Mimecast kişisel Portalı'nda bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="65985-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Personal Portal is to a user in Azure AD.</span></span> <span data-ttu-id="65985-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı Mimecast kişisel portalında arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="65985-140">In other words, a link relationship between an Azure AD user and the related user in Mimecast Personal Portal needs to be established.</span></span>

<span data-ttu-id="65985-141">Değeri Mimecast kişisel portalında atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="65985-141">In Mimecast Personal Portal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="65985-142">Yapılandırmak ve Azure AD çoklu oturum açma Mimecast kişisel portalıyla sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="65985-142">To configure and test Azure AD single sign-on with Mimecast Personal Portal, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="65985-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="65985-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="65985-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="65985-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65985-145">**[Mimecast kişisel Portal test kullanıcısı oluşturma](#creating-a-mimecast-personal-portal-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Mimecast kişisel Portal sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="65985-145">**[Creating a Mimecast Personal Portal test user](#creating-a-mimecast-personal-portal-test-user)** - to have a counterpart of Britta Simon in Mimecast Personal Portal that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="65985-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="65985-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65985-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="65985-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="65985-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="65985-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="65985-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Mimecast kişisel portalı uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="65985-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="65985-150">**Azure AD çoklu oturum açma Mimecast kişisel Portal ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="65985-150">**To configure Azure AD single sign-on with Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="65985-151">Azure portalında üzerinde **Mimecast kişisel Portal** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="65985-151">In the Azure portal, on the **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="65985-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="65985-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. <span data-ttu-id="65985-155">Üzerinde **Mimecast kişisel Portal etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="65985-155">On the **Mimecast Personal Portal Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="65985-157">a.</span><span class="sxs-lookup"><span data-stu-id="65985-157">a.</span></span> <span data-ttu-id="65985-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="65985-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    <span data-ttu-id="65985-159">b.</span><span class="sxs-lookup"><span data-stu-id="65985-159">b.</span></span> <span data-ttu-id="65985-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="65985-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > <span data-ttu-id="65985-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="65985-161">These values are not real.</span></span> <span data-ttu-id="65985-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="65985-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="65985-163">Kişi [Mimecast kişisel Portal istemci destek ekibi](https://www.mimecast.com/customer-success/technical-support/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="65985-163">Contact [Mimecast Personal Portal Client support team](https://www.mimecast.com/customer-success/technical-support/) to get these values.</span></span> 
 


4. <span data-ttu-id="65985-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="65985-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. <span data-ttu-id="65985-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="65985-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="65985-168">Üzerinde **Mimecast kişisel Portal Yapılandırması** 'yi tıklatın **Mimecast kişisel Portal Yapılandırma** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="65985-168">On the **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** to open **Configure sign-on** window.</span></span> <span data-ttu-id="65985-169">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="65985-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. <span data-ttu-id="65985-171">Farklı web tarayıcısı penceresinde Mimecast kişisel portalınızı bir yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="65985-171">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

8. <span data-ttu-id="65985-172">Git **Hizmetleri \> uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="65985-172">Go to **Services \> Applications**.</span></span>
   
    <span data-ttu-id="65985-173">![Uygulamaları](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="65985-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

9. <span data-ttu-id="65985-174">Tıklatın **kimlik doğrulaması profilleri**.</span><span class="sxs-lookup"><span data-stu-id="65985-174">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="65985-175">![Kimlik doğrulama profilleri](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "kimlik doğrulaması profilleri")</span><span class="sxs-lookup"><span data-stu-id="65985-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

10. <span data-ttu-id="65985-176">Tıklatın **yeni kimlik doğrulama profili**.</span><span class="sxs-lookup"><span data-stu-id="65985-176">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="65985-177">![Yeni kimlik doğrulama profili](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "yeni kimlik doğrulama profili")</span><span class="sxs-lookup"><span data-stu-id="65985-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

11. <span data-ttu-id="65985-178">İçinde **kimlik doğrulama profili** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="65985-178">In the **Authentication Profile** section, perform the following steps:</span></span>
   
    <span data-ttu-id="65985-179">![Kimlik doğrulama profili](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "kimlik doğrulama profili")</span><span class="sxs-lookup"><span data-stu-id="65985-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="65985-180">a.</span><span class="sxs-lookup"><span data-stu-id="65985-180">a.</span></span> <span data-ttu-id="65985-181">İçinde **açıklama** metin kutusuna, yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="65985-181">In the **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="65985-182">b.</span><span class="sxs-lookup"><span data-stu-id="65985-182">b.</span></span> <span data-ttu-id="65985-183">Seçin **Mimecast kişisel portalı SAML kimlik doğrulaması zorunlu**.</span><span class="sxs-lookup"><span data-stu-id="65985-183">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="65985-184">c.</span><span class="sxs-lookup"><span data-stu-id="65985-184">c.</span></span> <span data-ttu-id="65985-185">Olarak **sağlayıcı**seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="65985-185">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="65985-186">d.</span><span class="sxs-lookup"><span data-stu-id="65985-186">d.</span></span> <span data-ttu-id="65985-187">İçinde **veren URL'si** metin değerini yapıştırın **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="65985-187">In **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="65985-188">e.</span><span class="sxs-lookup"><span data-stu-id="65985-188">e.</span></span> <span data-ttu-id="65985-189">İçinde **oturum açma URL'si** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="65985-189">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="65985-190">f.</span><span class="sxs-lookup"><span data-stu-id="65985-190">f.</span></span> <span data-ttu-id="65985-191">İçinde **oturum kapatma URL'si** metin değerini yapıştırın **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="65985-191">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="65985-192">g.</span><span class="sxs-lookup"><span data-stu-id="65985-192">g.</span></span> <span data-ttu-id="65985-193">Açık, **base-64** Not Defteri'nde kodlanmış sertifika Azure Portalı'ndan indirilen, içeriğini, panoya kopyalayın ve yapıştırın kendisine **kimlik sağlayıcısı sertifikası (meta verileri)** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="65985-193">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="65985-194">h.</span><span class="sxs-lookup"><span data-stu-id="65985-194">h.</span></span> <span data-ttu-id="65985-195">Seçin **çoklu oturum açmaya izin verme**.</span><span class="sxs-lookup"><span data-stu-id="65985-195">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="65985-196">ı.</span><span class="sxs-lookup"><span data-stu-id="65985-196">i.</span></span> <span data-ttu-id="65985-197">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65985-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="65985-198">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="65985-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="65985-199">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="65985-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="65985-200">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="65985-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="65985-201">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="65985-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="65985-202">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="65985-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="65985-204">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="65985-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="65985-205">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="65985-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="65985-207">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="65985-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="65985-209">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="65985-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="65985-211">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="65985-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="65985-213">a.</span><span class="sxs-lookup"><span data-stu-id="65985-213">a.</span></span> <span data-ttu-id="65985-214">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="65985-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65985-215">b.</span><span class="sxs-lookup"><span data-stu-id="65985-215">b.</span></span> <span data-ttu-id="65985-216">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="65985-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="65985-217">c.</span><span class="sxs-lookup"><span data-stu-id="65985-217">c.</span></span> <span data-ttu-id="65985-218">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="65985-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="65985-219">d.</span><span class="sxs-lookup"><span data-stu-id="65985-219">d.</span></span> <span data-ttu-id="65985-220">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65985-220">Click **Create**.</span></span>
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="65985-221">Mimecast kişisel Portal test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="65985-221">Creating a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="65985-222">Azure AD kullanıcılarının Mimecast kişisel portalda oturum açarken etkinleştirmek için bunlar Mimecast kişisel portalına sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="65985-222">In order to enable Azure AD users to log into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="65985-223">Mimecast kişisel söz konusu olduğunda, sağlama el ile bir görev portalıdır.</span><span class="sxs-lookup"><span data-stu-id="65985-223">In the case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="65985-224">Bir etki alanı kullanıcıları oluşturabilmeniz için önce kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="65985-224">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="65985-225">**Kullanıcı sağlamayı yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="65985-225">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="65985-226">Oturum, **Mimecast kişisel Portal** yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="65985-226">Sign on to your **Mimecast Personal Portal** as administrator.</span></span>

2. <span data-ttu-id="65985-227">Git **dizinleri \> iç**.</span><span class="sxs-lookup"><span data-stu-id="65985-227">Go to **Directories \> Internal**.</span></span>
   
    <span data-ttu-id="65985-228">![Dizinleri](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "dizinleri")</span><span class="sxs-lookup"><span data-stu-id="65985-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

3. <span data-ttu-id="65985-229">Tıklatın **kayıt yeni bir etki alanı**.</span><span class="sxs-lookup"><span data-stu-id="65985-229">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="65985-230">![Yeni etki alanı kayıt](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "kayıt yeni bir etki alanı")</span><span class="sxs-lookup"><span data-stu-id="65985-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

4. <span data-ttu-id="65985-231">Yeni etki alanınızın oluşturulduktan sonra tıklatın **yeni adresi**.</span><span class="sxs-lookup"><span data-stu-id="65985-231">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="65985-232">![Yeni bir adres](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "yeni adresi")</span><span class="sxs-lookup"><span data-stu-id="65985-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

5. <span data-ttu-id="65985-233">Yeni adres iletişim kutusunda geçerli bir Azure aşağıdaki adımları sağlamak istediğiniz AD hesabı:</span><span class="sxs-lookup"><span data-stu-id="65985-233">In the new address dialog, perform the following steps of a valid Azure AD account you want to provision:</span></span>
   
    <span data-ttu-id="65985-234">![Kaydet](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Kaydet")</span><span class="sxs-lookup"><span data-stu-id="65985-234">![Save](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="65985-235">a.</span><span class="sxs-lookup"><span data-stu-id="65985-235">a.</span></span> <span data-ttu-id="65985-236">İçinde **e-posta adresi** metin kutusuna, türü **e-posta adresi** kullanıcının  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="65985-236">In the **Email Address** textbox, type **Email Address** of the user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="65985-237">b.</span><span class="sxs-lookup"><span data-stu-id="65985-237">b.</span></span> <span data-ttu-id="65985-238">İçinde **genel adı** metin kutusuna, türü **kullanıcıadı** olarak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="65985-238">In the **Global Name** textbox, type the **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="65985-239">c.</span><span class="sxs-lookup"><span data-stu-id="65985-239">c.</span></span> <span data-ttu-id="65985-240">İçinde **parola**, ve **parolayı onayla** metin kutuları, türü **parola** kullanıcının.</span><span class="sxs-lookup"><span data-stu-id="65985-240">In the **Password**, and **Confirm Password** textboxes, type the **Password** of the user.</span></span>
   
    <span data-ttu-id="65985-241">b.</span><span class="sxs-lookup"><span data-stu-id="65985-241">b.</span></span> <span data-ttu-id="65985-242">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65985-242">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="65985-243">Azure AD kullanıcı hesaplarını sağlamak için herhangi bir Mimecast kişisel Portal kullanıcı hesabı oluşturma araçlarını veya Mimecast kişisel portalı tarafından sağlanan API'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65985-243">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="65985-244">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="65985-244">Assigning the Azure AD test user</span></span>

<span data-ttu-id="65985-245">Bu bölümde, Britta Mimecast kişisel portalına erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="65985-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Personal Portal.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="65985-247">**Britta Simon Mimecast kişisel portalına atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="65985-247">**To assign Britta Simon to Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="65985-248">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="65985-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="65985-250">Uygulamalar listesinde **Mimecast kişisel Portal**.</span><span class="sxs-lookup"><span data-stu-id="65985-250">In the applications list, select **Mimecast Personal Portal**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. <span data-ttu-id="65985-252">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="65985-252">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="65985-254">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="65985-254">Click **Add** button.</span></span> <span data-ttu-id="65985-255">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="65985-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="65985-257">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="65985-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="65985-258">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="65985-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65985-259">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="65985-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="65985-260">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="65985-260">Testing single sign-on</span></span>
<span data-ttu-id="65985-261">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="65985-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="65985-262">Erişim paneli Mimecast kişisel Portal parçasında tıklattığınızda, otomatik olarak Mimecast kişisel Portal uygulamanızın açan.</span><span class="sxs-lookup"><span data-stu-id="65985-262">When you click the Mimecast Personal Portal tile in the Access Panel, you should get automatically signed-on to your Mimecast Personal Portal application.</span></span> <span data-ttu-id="65985-263">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="65985-263">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="65985-264">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="65985-264">Additional resources</span></span>

* [<span data-ttu-id="65985-265">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="65985-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65985-266">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="65985-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

