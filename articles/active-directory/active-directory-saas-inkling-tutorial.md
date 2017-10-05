---
title: "Öğretici: Azure Active Directory Tümleştirme ile Inkling | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Inkling arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 64c7ee45-ee8a-42f7-bf04-fd0e00833ea9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 7b0639c6515298731f88346c2e4ca82664653a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-inkling"></a><span data-ttu-id="7563a-103">Öğretici: Azure Active Directory Tümleştirme Inkling ile</span><span class="sxs-lookup"><span data-stu-id="7563a-103">Tutorial: Azure Active Directory integration with Inkling</span></span>

<span data-ttu-id="7563a-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Inkling tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7563a-104">In this tutorial, you learn how to integrate Inkling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7563a-105">Inkling Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="7563a-105">Integrating Inkling with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7563a-106">Inkling erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7563a-106">You can control in Azure AD who has access to Inkling</span></span>
- <span data-ttu-id="7563a-107">Otomatik olarak için Inkling (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7563a-107">You can enable your users to automatically get signed-on to Inkling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7563a-108">Hesaplarınızı bir merkezi konumda - Azure Yönetim Portalı'nı yönetme</span><span class="sxs-lookup"><span data-stu-id="7563a-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="7563a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7563a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7563a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7563a-110">Prerequisites</span></span>

<span data-ttu-id="7563a-111">Azure AD tümleştirme Inkling ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="7563a-111">To configure Azure AD integration with Inkling, you need the following items:</span></span>

- <span data-ttu-id="7563a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="7563a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7563a-113">Bir Inkling çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="7563a-113">An Inkling single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="7563a-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7563a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="7563a-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7563a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7563a-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7563a-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="7563a-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7563a-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="7563a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="7563a-118">Scenario description</span></span>
<span data-ttu-id="7563a-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="7563a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7563a-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="7563a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7563a-121">Galeriden Inkling ekleme</span><span class="sxs-lookup"><span data-stu-id="7563a-121">Adding Inkling from the gallery</span></span>
2. <span data-ttu-id="7563a-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7563a-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-inkling-from-the-gallery"></a><span data-ttu-id="7563a-123">Galeriden Inkling ekleme</span><span class="sxs-lookup"><span data-stu-id="7563a-123">Adding Inkling from the gallery</span></span>
<span data-ttu-id="7563a-124">Azure AD Inkling tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Inkling eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7563a-124">To configure the integration of Inkling into Azure AD, you need to add Inkling from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7563a-125">**Galeriden Inkling eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7563a-125">**To add Inkling from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7563a-126">İçinde  **[Azure Yönetim Portalı](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7563a-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7563a-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="7563a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7563a-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7563a-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="7563a-131">Tıklatın **Ekle** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7563a-131">Click **Add** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="7563a-133">Arama kutusuna **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="7563a-133">In the search box, type **Inkling**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_001.png)

5. <span data-ttu-id="7563a-135">Sonuçlar panelinde seçin **Inkling**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7563a-135">In the results panel, select **Inkling**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7563a-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7563a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7563a-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Inkling sınayın.</span><span class="sxs-lookup"><span data-stu-id="7563a-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7563a-139">Tekli çalışmaya oturum için Azure AD Inkling karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="7563a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Inkling is to a user in Azure AD.</span></span> <span data-ttu-id="7563a-140">Diğer bir deyişle, bir Azure AD kullanıcısının Inkling ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7563a-140">In other words, a link relationship between an Azure AD user and the related user in Inkling needs to be established.</span></span>

<span data-ttu-id="7563a-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Inkling içinde.</span><span class="sxs-lookup"><span data-stu-id="7563a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Inkling.</span></span>

<span data-ttu-id="7563a-142">Yapılandırma ve Azure AD çoklu oturum açma Inkling ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7563a-142">To configure and test Azure AD single sign-on with Inkling, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7563a-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="7563a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7563a-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="7563a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7563a-145">**[Bir Inkling test kullanıcısı oluşturma](#creating-an-inkling-test-user)**  - Britta Simon, karşılık gelen her, Azure AD gösterimine bağlı Inkling sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="7563a-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - to have a counterpart of Britta Simon in Inkling that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="7563a-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="7563a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7563a-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7563a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7563a-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7563a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7563a-149">Bu bölümde, Azure AD çoklu oturum açma Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma Inkling uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7563a-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Inkling application.</span></span>

<span data-ttu-id="7563a-150">**Azure AD çoklu oturum açma ile Inkling yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7563a-150">**To configure Azure AD single sign-on with Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="7563a-151">Azure Yönetim Portalı'nda üzerinde **Inkling** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7563a-151">In the Azure Management portal, on the **Inkling** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="7563a-153">Üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="7563a-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-inkling-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="7563a-155">Üzerinde **Inkling etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7563a-155">On the **Inkling Domain and URLs** section, perform the following steps:</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_01.png)

    <span data-ttu-id="7563a-157">a.</span><span class="sxs-lookup"><span data-stu-id="7563a-157">a.</span></span> <span data-ttu-id="7563a-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://api.inkling.com/saml/v2/metadata/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="7563a-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span></span>

    <span data-ttu-id="7563a-159">b.</span><span class="sxs-lookup"><span data-stu-id="7563a-159">b.</span></span> <span data-ttu-id="7563a-160">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://api.inkling.com/saml/v2/acs/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="7563a-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7563a-161">Lütfen bu gerçek değerlerin olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="7563a-161">Please note that these are not the real values.</span></span> <span data-ttu-id="7563a-162">Bu değerler gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7563a-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="7563a-163">Kişi [Inkling destek ekibi](mailto:press@inkling.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="7563a-163">Contact [Inkling support team](mailto:press@inkling.com) to get these values.</span></span>

4. <span data-ttu-id="7563a-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **yeni sertifika oluştur**.</span><span class="sxs-lookup"><span data-stu-id="7563a-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-inkling-tutorial/tutorial_general_400.png)    

5. <span data-ttu-id="7563a-166">Üzerinde **yeni sertifika oluştur** iletişim kutusunda, Takvim simgesine tıklayın ve bir **sona erme tarihi**.</span><span class="sxs-lookup"><span data-stu-id="7563a-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="7563a-167">Ardından **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7563a-167">Then click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-inkling-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="7563a-169">Üzerinde **SAML imzalama sertifikası** bölümünde, select **yeni sertifika etkin hale getirin** tıklatıp **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7563a-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_02.png)

7. <span data-ttu-id="7563a-171">Açılır pencere üzerinde **geçiş sertifikası** penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7563a-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-inkling-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="7563a-173">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7563a-173">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_03.png) 

9. <span data-ttu-id="7563a-175">Uygulamanız için yapılandırılmış SSO almak için başvurun [Inkling destek ekibi](mailto:press@inkling.com) ve verin ile indirilen **meta verileri**.</span><span class="sxs-lookup"><span data-stu-id="7563a-175">To get SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7563a-176">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7563a-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="7563a-177">Bu bölümün amacı, Britta Simon adlı Azure Yönetim Portalı'nda bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="7563a-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="7563a-179">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7563a-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7563a-180">İçinde **Azure Yönetim Portalı**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7563a-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-inkling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7563a-182">Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="7563a-182">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-inkling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7563a-184">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7563a-184">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-inkling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7563a-186">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7563a-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-inkling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7563a-188">a.</span><span class="sxs-lookup"><span data-stu-id="7563a-188">a.</span></span> <span data-ttu-id="7563a-189">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7563a-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7563a-190">b.</span><span class="sxs-lookup"><span data-stu-id="7563a-190">b.</span></span> <span data-ttu-id="7563a-191">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="7563a-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7563a-192">c.</span><span class="sxs-lookup"><span data-stu-id="7563a-192">c.</span></span> <span data-ttu-id="7563a-193">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="7563a-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7563a-194">d.</span><span class="sxs-lookup"><span data-stu-id="7563a-194">d.</span></span> <span data-ttu-id="7563a-195">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7563a-195">Click **Create**.</span></span> 



### <a name="creating-an-inkling-test-user"></a><span data-ttu-id="7563a-196">Bir Inkling test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7563a-196">Creating an Inkling test user</span></span>

<span data-ttu-id="7563a-197">Bu bölümde, Inkling içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7563a-197">In this section, you create a user called Britta Simon in Inkling.</span></span> <span data-ttu-id="7563a-198">Lütfen çalışmak [Inkling destek ekibi](mailto:press@inkling.com) Inkling platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="7563a-198">Please work with [Inkling support team](mailto:press@inkling.com) to add the users in the Inkling platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7563a-199">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="7563a-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7563a-200">Bu bölümde, Britta Inkling için kendi erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7563a-200">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Inkling.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="7563a-202">**Inkling için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7563a-202">**To assign Britta Simon to Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="7563a-203">Azure Yönetim Portalı'nda uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7563a-203">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="7563a-205">Uygulamalar listesinde **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="7563a-205">In the applications list, select **Inkling**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_50.png) 

3. <span data-ttu-id="7563a-207">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="7563a-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="7563a-209">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7563a-209">Click **Add** button.</span></span> <span data-ttu-id="7563a-210">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7563a-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="7563a-212">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="7563a-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7563a-213">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7563a-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7563a-214">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7563a-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="7563a-215">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="7563a-215">Testing single sign-on</span></span>

<span data-ttu-id="7563a-216">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="7563a-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7563a-217">Erişim paneli Inkling parçasında tıklattığınızda, otomatik olarak Inkling uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="7563a-217">When you click the Inkling tile in the Access Panel, you should get automatically signed-on to your Inkling application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7563a-218">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7563a-218">Additional resources</span></span>

* [<span data-ttu-id="7563a-219">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="7563a-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7563a-220">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="7563a-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_203.png