---
title: "Öğretici: Azure Active Directory Tümleştirme ile Moxtra | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Moxtra arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: db2f041a44b6771b0a4f734e58d899298ef0847b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="60a18-103">Öğretici: Azure Active Directory Tümleştirme Moxtra ile</span><span class="sxs-lookup"><span data-stu-id="60a18-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="60a18-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Moxtra tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="60a18-104">In this tutorial, you learn how to integrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="60a18-105">Moxtra Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="60a18-105">Integrating Moxtra with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="60a18-106">Moxtra erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="60a18-106">You can control in Azure AD who has access to Moxtra</span></span>
- <span data-ttu-id="60a18-107">Otomatik olarak için Moxtra (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="60a18-107">You can enable your users to automatically get signed-on to Moxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="60a18-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="60a18-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="60a18-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="60a18-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60a18-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="60a18-110">Prerequisites</span></span>

<span data-ttu-id="60a18-111">Azure AD tümleştirme Moxtra ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="60a18-111">To configure Azure AD integration with Moxtra, you need the following items:</span></span>

- <span data-ttu-id="60a18-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="60a18-112">An Azure AD subscription</span></span>
- <span data-ttu-id="60a18-113">Bir Moxtra çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="60a18-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="60a18-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="60a18-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="60a18-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="60a18-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="60a18-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="60a18-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="60a18-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="60a18-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="60a18-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="60a18-118">Scenario description</span></span>
<span data-ttu-id="60a18-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="60a18-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="60a18-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="60a18-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="60a18-121">Galeriden Moxtra ekleme</span><span class="sxs-lookup"><span data-stu-id="60a18-121">Adding Moxtra from the gallery</span></span>
2. <span data-ttu-id="60a18-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="60a18-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-the-gallery"></a><span data-ttu-id="60a18-123">Galeriden Moxtra ekleme</span><span class="sxs-lookup"><span data-stu-id="60a18-123">Adding Moxtra from the gallery</span></span>
<span data-ttu-id="60a18-124">Azure AD Moxtra tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Moxtra eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="60a18-124">To configure the integration of Moxtra into Azure AD, you need to add Moxtra from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="60a18-125">**Galeriden Moxtra eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="60a18-125">**To add Moxtra from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="60a18-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="60a18-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="60a18-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="60a18-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="60a18-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="60a18-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="60a18-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="60a18-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="60a18-133">Arama kutusuna **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="60a18-133">In the search box, type **Moxtra**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="60a18-135">Sonuçlar panelinde seçin **Moxtra**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="60a18-135">In the results panel, select **Moxtra**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="60a18-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="60a18-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="60a18-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Moxtra sınayın.</span><span class="sxs-lookup"><span data-stu-id="60a18-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="60a18-139">Tekli çalışmaya oturum için Azure AD Moxtra karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="60a18-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Moxtra is to a user in Azure AD.</span></span> <span data-ttu-id="60a18-140">Diğer bir deyişle, bir Azure AD kullanıcısının Moxtra ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="60a18-140">In other words, a link relationship between an Azure AD user and the related user in Moxtra needs to be established.</span></span>

<span data-ttu-id="60a18-141">Moxtra içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="60a18-141">In Moxtra, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="60a18-142">Yapılandırma ve Azure AD çoklu oturum açma Moxtra ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="60a18-142">To configure and test Azure AD single sign-on with Moxtra, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="60a18-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="60a18-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="60a18-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="60a18-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="60a18-145">**[Moxtra test kullanıcısı oluşturma](#creating-a-moxtra-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Moxtra sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="60a18-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - to have a counterpart of Britta Simon in Moxtra that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="60a18-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="60a18-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="60a18-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="60a18-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="60a18-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="60a18-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="60a18-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Moxtra uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="60a18-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="60a18-150">**Azure AD çoklu oturum açma ile Moxtra yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="60a18-150">**To configure Azure AD single sign-on with Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="60a18-151">Azure portalında üzerinde **Moxtra** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="60a18-151">In the Azure portal, on the **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="60a18-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="60a18-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="60a18-155">Üzerinde **Moxtra etki alanı ve URL'leri** bölümünde, aşağıdaki adımı gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="60a18-155">On the **Moxtra Domain and URLs** section, perform the following step:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="60a18-157">İçinde **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="60a18-157">In the **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="60a18-158">Moxtra uygulaması SAML onaylar belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="60a18-158">Moxtra application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="60a18-159">Bu uygulama için aşağıdaki talep yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="60a18-159">Configure the following claims for this application.</span></span> <span data-ttu-id="60a18-160">Bu öznitelik değerlerini yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="60a18-160">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="60a18-161">Aşağıdaki ekran görüntüsünde, bu yapılandırma için bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="60a18-161">The following screenshot shows an example for this configuration.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="60a18-163">İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği görüntüde gösterildiği gibi yapılandırın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="60a18-163">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="60a18-164">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="60a18-164">Attribute Name</span></span> | <span data-ttu-id="60a18-165">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="60a18-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="60a18-166">FirstName</span><span class="sxs-lookup"><span data-stu-id="60a18-166">firstname</span></span> | <span data-ttu-id="60a18-167">User.givenName</span><span class="sxs-lookup"><span data-stu-id="60a18-167">user.givenname</span></span> |
    | <span data-ttu-id="60a18-168">Soyadı</span><span class="sxs-lookup"><span data-stu-id="60a18-168">lastname</span></span> | <span data-ttu-id="60a18-169">User.surname</span><span class="sxs-lookup"><span data-stu-id="60a18-169">user.surname</span></span> |
    | <span data-ttu-id="60a18-170">idpid</span><span class="sxs-lookup"><span data-stu-id="60a18-170">idpid</span></span>    | <span data-ttu-id="60a18-171">< SAML varlık kimliği ></span><span class="sxs-lookup"><span data-stu-id="60a18-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="60a18-172">Değeri **idpid** özniteliği gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="60a18-172">The value of **idpid** attribute is not real.</span></span> <span data-ttu-id="60a18-173">Gerçek değerini alabilir **hızlı başvuru** altında bölümünde **Moxtra yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="60a18-173">You can get the actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="60a18-174">a.</span><span class="sxs-lookup"><span data-stu-id="60a18-174">a.</span></span> <span data-ttu-id="60a18-175">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="60a18-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="60a18-177">b.</span><span class="sxs-lookup"><span data-stu-id="60a18-177">b.</span></span> <span data-ttu-id="60a18-178">İçinde **adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="60a18-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="60a18-180">c.</span><span class="sxs-lookup"><span data-stu-id="60a18-180">c.</span></span> <span data-ttu-id="60a18-181">Gelen **değeri** listesinde, ilgili satır için gösterilen öznitelik değeri yazın.</span><span class="sxs-lookup"><span data-stu-id="60a18-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="60a18-182">d.</span><span class="sxs-lookup"><span data-stu-id="60a18-182">d.</span></span> <span data-ttu-id="60a18-183">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="60a18-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="60a18-184">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="60a18-184">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="60a18-186">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="60a18-186">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="60a18-188">Üzerinde **Moxtra yapılandırma** 'yi tıklatın **yapılandırma Moxtra** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="60a18-188">On the **Moxtra Configuration** section, click **Configure Moxtra** to open **Configure sign-on** window.</span></span> <span data-ttu-id="60a18-189">Kopya **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="60a18-189">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="60a18-191">Başka bir tarayıcı penceresinde Moxtra şirket sitenize yönetici olarak oturum açma.</span><span class="sxs-lookup"><span data-stu-id="60a18-191">In another browser window, sign on to your Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="60a18-192">Sol taraftaki araç çubuğunda tıklatın **Yönetici Konsolu > SAML çoklu oturum açma**ve ardından **yeni**.</span><span class="sxs-lookup"><span data-stu-id="60a18-192">In the toolbar on the left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="60a18-194">Üzerinde **SAML** sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="60a18-194">On the **SAML** page, perform the following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="60a18-196">a.</span><span class="sxs-lookup"><span data-stu-id="60a18-196">a.</span></span> <span data-ttu-id="60a18-197">İçinde **adı** metin kutusuna, yapılandırmanız için bir ad yazın (örneğin: *SAML*).</span><span class="sxs-lookup"><span data-stu-id="60a18-197">In the **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="60a18-198">b.</span><span class="sxs-lookup"><span data-stu-id="60a18-198">b.</span></span> <span data-ttu-id="60a18-199">İçinde **IDP varlık kimliği** metin değerini yapıştırın **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="60a18-199">In the **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="60a18-200">c.</span><span class="sxs-lookup"><span data-stu-id="60a18-200">c.</span></span> <span data-ttu-id="60a18-201">İçinde **oturum açma URL'si** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="60a18-201">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="60a18-202">d.</span><span class="sxs-lookup"><span data-stu-id="60a18-202">d.</span></span> <span data-ttu-id="60a18-203">İçinde **AuthnContextClassRef** metin kutusuna, türü **urn: OASIS: adları: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="60a18-203">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="60a18-204">e.</span><span class="sxs-lookup"><span data-stu-id="60a18-204">e.</span></span> <span data-ttu-id="60a18-205">İçinde **NameID biçimi** metin kutusuna, türü **urn: OASIS: adları: tc: SAML:1.1:nameid-biçimi: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="60a18-205">In the **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="60a18-206">f.</span><span class="sxs-lookup"><span data-stu-id="60a18-206">f.</span></span> <span data-ttu-id="60a18-207">Not Defteri'nde, Azure Portalı'ndan indirilen açık sertifika içeriği Kopyala ve ardından yapıştırın **sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="60a18-207">Open certificate which you have downloaded from Azure portal in notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="60a18-208">g.</span><span class="sxs-lookup"><span data-stu-id="60a18-208">g.</span></span> <span data-ttu-id="60a18-209">SAML e-posta etki alanı metin kutusuna, SAML e-posta etki alanı yazın.</span><span class="sxs-lookup"><span data-stu-id="60a18-209">In the SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="60a18-210">Etki alanı doğrulama adımlarını görmek için tıklatın "**ı**" altında.</span><span class="sxs-lookup"><span data-stu-id="60a18-210">To see the steps to verify the domain, click the "**i**" below.</span></span>

    <span data-ttu-id="60a18-211">h.</span><span class="sxs-lookup"><span data-stu-id="60a18-211">h.</span></span> <span data-ttu-id="60a18-212">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="60a18-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="60a18-213">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="60a18-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="60a18-214">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="60a18-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="60a18-215">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="60a18-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="60a18-216">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="60a18-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="60a18-217">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="60a18-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="60a18-219">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="60a18-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="60a18-220">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="60a18-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="60a18-222">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="60a18-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="60a18-224">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="60a18-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="60a18-226">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="60a18-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="60a18-228">a.</span><span class="sxs-lookup"><span data-stu-id="60a18-228">a.</span></span> <span data-ttu-id="60a18-229">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="60a18-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="60a18-230">b.</span><span class="sxs-lookup"><span data-stu-id="60a18-230">b.</span></span> <span data-ttu-id="60a18-231">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="60a18-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="60a18-232">c.</span><span class="sxs-lookup"><span data-stu-id="60a18-232">c.</span></span> <span data-ttu-id="60a18-233">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="60a18-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="60a18-234">d.</span><span class="sxs-lookup"><span data-stu-id="60a18-234">d.</span></span> <span data-ttu-id="60a18-235">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="60a18-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="60a18-236">Moxtra test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="60a18-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="60a18-237">Bu bölümün amacı Britta Simon içinde Moxtra adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="60a18-237">The objective of this section is to create a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="60a18-238">**İçinde Moxtra Britta Simon adlı bir kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="60a18-238">**To create a user called Britta Simon in Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="60a18-239">Moxtra şirket sitenize yönetici olarak oturum açma.</span><span class="sxs-lookup"><span data-stu-id="60a18-239">Sign on to your Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="60a18-240">Sol taraftaki araç çubuğunda tıklatın **Yönetici Konsolu > Kullanıcı Yönetimi**ve ardından **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="60a18-240">In the toolbar on the left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="60a18-242">Üzerinde **Kullanıcı Ekle** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="60a18-242">On the **Add User** dialog, perform the following steps:</span></span>
  
    <span data-ttu-id="60a18-243">a.</span><span class="sxs-lookup"><span data-stu-id="60a18-243">a.</span></span> <span data-ttu-id="60a18-244">İçinde **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="60a18-244">In the **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="60a18-245">b.</span><span class="sxs-lookup"><span data-stu-id="60a18-245">b.</span></span> <span data-ttu-id="60a18-246">İçinde **Soyadı** metin kutusuna, türü **Simon**.</span><span class="sxs-lookup"><span data-stu-id="60a18-246">In the **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="60a18-247">c.</span><span class="sxs-lookup"><span data-stu-id="60a18-247">c.</span></span> <span data-ttu-id="60a18-248">İçinde **e-posta** metin kutusuna, Britta'nın e-posta adresi ile aynı Azure Portal'da türü.</span><span class="sxs-lookup"><span data-stu-id="60a18-248">In the **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="60a18-249">d.</span><span class="sxs-lookup"><span data-stu-id="60a18-249">d.</span></span> <span data-ttu-id="60a18-250">İçinde **bölme** metin kutusuna, türü **geliştirme**.</span><span class="sxs-lookup"><span data-stu-id="60a18-250">In the **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="60a18-251">e.</span><span class="sxs-lookup"><span data-stu-id="60a18-251">e.</span></span> <span data-ttu-id="60a18-252">İçinde **departmanı** metin kutusuna, türü **BT**.</span><span class="sxs-lookup"><span data-stu-id="60a18-252">In the **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="60a18-253">f.</span><span class="sxs-lookup"><span data-stu-id="60a18-253">f.</span></span> <span data-ttu-id="60a18-254">Seçin **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="60a18-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="60a18-255">g.</span><span class="sxs-lookup"><span data-stu-id="60a18-255">g.</span></span> <span data-ttu-id="60a18-256">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="60a18-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="60a18-257">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="60a18-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="60a18-258">Bu bölümde, Britta Moxtra için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="60a18-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Moxtra.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="60a18-260">**Moxtra için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="60a18-260">**To assign Britta Simon to Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="60a18-261">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="60a18-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="60a18-263">Uygulamalar listesinde **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="60a18-263">In the applications list, select **Moxtra**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="60a18-265">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="60a18-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="60a18-267">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="60a18-267">Click **Add** button.</span></span> <span data-ttu-id="60a18-268">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="60a18-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="60a18-270">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="60a18-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="60a18-271">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="60a18-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="60a18-272">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="60a18-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="60a18-273">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="60a18-273">Testing single sign-on</span></span>

<span data-ttu-id="60a18-274">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="60a18-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="60a18-275">Erişim paneli Moxtra parçasında tıklattığınızda, otomatik olarak Moxtra uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="60a18-275">When you click the Moxtra tile in the Access Panel, you should get automatically signed-on to your Moxtra application.</span></span>
<span data-ttu-id="60a18-276">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="60a18-276">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="60a18-277">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="60a18-277">Additional resources</span></span>

* [<span data-ttu-id="60a18-278">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="60a18-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="60a18-279">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="60a18-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

