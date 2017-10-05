---
title: "Öğretici: Azure Active Directory Tümleştirme ekip çalışması ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ekip çalışması arasındaki yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03760032-3d76-4b47-ab84-241f72fbd561
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: edd2f9446515531f1147a8abf99295b618b89b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamwork"></a><span data-ttu-id="5eeca-103">Öğretici: Azure Active Directory Tümleştirme ile ekip çalışması</span><span class="sxs-lookup"><span data-stu-id="5eeca-103">Tutorial: Azure Active Directory integration with Teamwork</span></span>

<span data-ttu-id="5eeca-104">Bu öğreticide, Azure Active Directory (Azure AD) ile ekip çalışması tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5eeca-104">In this tutorial, you learn how to integrate Teamwork with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5eeca-105">Ekip çalışması Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="5eeca-105">Integrating Teamwork with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5eeca-106">Ekip çalışması erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5eeca-106">You can control in Azure AD who has access to Teamwork</span></span>
- <span data-ttu-id="5eeca-107">Otomatik olarak ekip çalışması için (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5eeca-107">You can enable your users to automatically get signed-on to Teamwork (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5eeca-108">Hesaplarınızı bir merkezi konumda - Azure Yönetim Portalı'nı yönetme</span><span class="sxs-lookup"><span data-stu-id="5eeca-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="5eeca-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5eeca-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5eeca-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5eeca-110">Prerequisites</span></span>

<span data-ttu-id="5eeca-111">Azure AD tümleştirme ekip çalışması ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="5eeca-111">To configure Azure AD integration with Teamwork, you need the following items:</span></span>

- <span data-ttu-id="5eeca-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="5eeca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5eeca-113">Bir ekip çalışması çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="5eeca-113">A Teamwork single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="5eeca-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="5eeca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="5eeca-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="5eeca-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5eeca-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5eeca-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="5eeca-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5eeca-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="5eeca-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="5eeca-118">Scenario description</span></span>
<span data-ttu-id="5eeca-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="5eeca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5eeca-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="5eeca-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5eeca-121">Galeriden ekip çalışması ekleme</span><span class="sxs-lookup"><span data-stu-id="5eeca-121">Adding Teamwork from the gallery</span></span>
2. <span data-ttu-id="5eeca-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="5eeca-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-teamwork-from-the-gallery"></a><span data-ttu-id="5eeca-123">Galeriden ekip çalışması ekleme</span><span class="sxs-lookup"><span data-stu-id="5eeca-123">Adding Teamwork from the gallery</span></span>
<span data-ttu-id="5eeca-124">Azure AD ekip çalışması tümleştirilmesi yapılandırmak için ekip çalışması Galeriden yönetilen SaaS uygulamaları listenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5eeca-124">To configure the integration of Teamwork into Azure AD, you need to add Teamwork from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5eeca-125">**Galeriden ekip çalışması eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5eeca-125">**To add Teamwork from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5eeca-126">İçinde  **[Azure Yönetim Portalı](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="5eeca-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5eeca-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="5eeca-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5eeca-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5eeca-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="5eeca-131">Tıklatın **Ekle** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5eeca-131">Click **Add** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="5eeca-133">Arama kutusuna **ekip çalışması**.</span><span class="sxs-lookup"><span data-stu-id="5eeca-133">In the search box, type **Teamwork**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_001.png)

5. <span data-ttu-id="5eeca-135">Sonuçlar panelinde seçin **ekip çalışması**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5eeca-135">In the results panel, select **Teamwork**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5eeca-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="5eeca-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5eeca-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı ekip çalışması ile test etme.</span><span class="sxs-lookup"><span data-stu-id="5eeca-138">In this section, you configure and test Azure AD single sign-on with Teamwork based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5eeca-139">Tekli çalışmaya oturum için Azure AD karşılık gelen kullanıcı ekip çalışması için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="5eeca-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamwork is to a user in Azure AD.</span></span> <span data-ttu-id="5eeca-140">Diğer bir deyişle, bir Azure AD kullanıcısının ekip çalışması ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5eeca-140">In other words, a link relationship between an Azure AD user and the related user in Teamwork needs to be established.</span></span>

<span data-ttu-id="5eeca-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** ekip çalışması içinde.</span><span class="sxs-lookup"><span data-stu-id="5eeca-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamwork.</span></span>

<span data-ttu-id="5eeca-142">Yapılandırma ve Azure AD çoklu oturum açma ekip çalışması ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="5eeca-142">To configure and test Azure AD single sign-on with Teamwork, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5eeca-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="5eeca-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5eeca-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="5eeca-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5eeca-145">**[Bir ekip çalışması test kullanıcısı oluşturma](#creating-a-teamwork-test-user)**  - Britta Simon, karşılık gelen her, Azure AD gösterimine bağlı ekip çalışması sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="5eeca-145">**[Creating a Teamwork test user](#creating-a-teamwork-test-user)** - to have a counterpart of Britta Simon in Teamwork that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="5eeca-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="5eeca-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5eeca-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="5eeca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5eeca-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5eeca-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5eeca-149">Bu bölümde, Azure AD çoklu oturum açma Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma ekip çalışması uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5eeca-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamwork application.</span></span>

<span data-ttu-id="5eeca-150">**Azure AD çoklu oturum açma ekip çalışması ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5eeca-150">**To configure Azure AD single sign-on with Teamwork, perform the following steps:**</span></span>

1. <span data-ttu-id="5eeca-151">Azure Yönetim Portalı'nda üzerinde **ekip çalışması** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="5eeca-151">In the Azure Management portal, on the **Teamwork** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="5eeca-153">Üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="5eeca-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_01.png)

3. <span data-ttu-id="5eeca-155">Üzerinde **ekip çalışması etki alanı ve URL'leri** bölümünde **oturum üzerinde URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.teamwork.com`</span><span class="sxs-lookup"><span data-stu-id="5eeca-155">On the **Teamwork Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.teamwork.com`</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_02.png)

    > [!NOTE] 
    > <span data-ttu-id="5eeca-157">Lütfen bu gerçek değer olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5eeca-157">Please note that this is not the real value.</span></span> <span data-ttu-id="5eeca-158">Bu değer gerçek oturum üzerinde URL ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5eeca-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="5eeca-159">Kişi [ekip çalışması destek ekibi](mailto:support@teamwork.com) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="5eeca-159">Contact [Teamwork support team](mailto:support@teamwork.com) to get this value.</span></span> 

4. <span data-ttu-id="5eeca-160">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **yeni sertifika oluştur**.</span><span class="sxs-lookup"><span data-stu-id="5eeca-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_03.png)   

5. <span data-ttu-id="5eeca-162">Üzerinde **yeni sertifika oluştur** iletişim kutusunda, Takvim simgesine tıklayın ve bir **sona erme tarihi**.</span><span class="sxs-lookup"><span data-stu-id="5eeca-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="5eeca-163">Ardından **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5eeca-163">Then click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamwork-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="5eeca-165">Üzerinde **SAML imzalama sertifikası** bölümünde, select **yeni sertifika etkin hale getirin** tıklatıp **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5eeca-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_04.png)

7. <span data-ttu-id="5eeca-167">Açılır pencere üzerinde **geçiş sertifikası** penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5eeca-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamwork-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5eeca-169">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5eeca-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_05.png) 

9. <span data-ttu-id="5eeca-171">Uygulamanız için yapılandırılmış SSO almak için başvurun [ekip çalışması destek ekibi](mailto:support@teamwork.com) ve indirilen ile verin **meta verileri**.</span><span class="sxs-lookup"><span data-stu-id="5eeca-171">To get SSO configured for your application, contact [Teamwork support team](mailto:support@teamwork.com) and provide them with the downloaded **metadata**.</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5eeca-172">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5eeca-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="5eeca-173">Bu bölümün amacı, Britta Simon adlı Azure Yönetim Portalı'nda bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="5eeca-173">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="5eeca-175">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5eeca-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5eeca-176">İçinde **Azure Yönetim Portalı**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="5eeca-176">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamwork-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5eeca-178">Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="5eeca-178">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamwork-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5eeca-180">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5eeca-180">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamwork-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5eeca-182">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5eeca-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamwork-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5eeca-184">a.</span><span class="sxs-lookup"><span data-stu-id="5eeca-184">a.</span></span> <span data-ttu-id="5eeca-185">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5eeca-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5eeca-186">b.</span><span class="sxs-lookup"><span data-stu-id="5eeca-186">b.</span></span> <span data-ttu-id="5eeca-187">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="5eeca-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5eeca-188">c.</span><span class="sxs-lookup"><span data-stu-id="5eeca-188">c.</span></span> <span data-ttu-id="5eeca-189">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="5eeca-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5eeca-190">d.</span><span class="sxs-lookup"><span data-stu-id="5eeca-190">d.</span></span> <span data-ttu-id="5eeca-191">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5eeca-191">Click **Create**.</span></span> 



### <a name="creating-a-teamwork-test-user"></a><span data-ttu-id="5eeca-192">Bir ekip çalışması test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5eeca-192">Creating a Teamwork test user</span></span>

<span data-ttu-id="5eeca-193">Bu bölümde, ekip çalışması içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5eeca-193">In this section, you create a user called Britta Simon in Teamwork.</span></span> <span data-ttu-id="5eeca-194">Lütfen çalışmak [ekip çalışması destek ekibi](mailto:support@teamwork.com) ekip çalışması platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="5eeca-194">Please work with [Teamwork support team](mailto:support@teamwork.com) to add the users in the Teamwork platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5eeca-195">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="5eeca-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5eeca-196">Bu bölümde, ekip çalışması için kendi erişim vererek, Azure çoklu oturum açma kullanılacak Britta Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5eeca-196">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamwork.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="5eeca-198">**Ekip çalışması için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5eeca-198">**To assign Britta Simon to Teamwork, perform the following steps:**</span></span>

1. <span data-ttu-id="5eeca-199">Azure Yönetim Portalı'nda uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5eeca-199">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="5eeca-201">Uygulamalar listesinde **ekip çalışması**.</span><span class="sxs-lookup"><span data-stu-id="5eeca-201">In the applications list, select **Teamwork**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_50.png) 

3. <span data-ttu-id="5eeca-203">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="5eeca-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="5eeca-205">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5eeca-205">Click **Add** button.</span></span> <span data-ttu-id="5eeca-206">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5eeca-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="5eeca-208">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="5eeca-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5eeca-209">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5eeca-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5eeca-210">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5eeca-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="5eeca-211">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="5eeca-211">Testing single sign-on</span></span>

<span data-ttu-id="5eeca-212">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="5eeca-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5eeca-213">Erişim paneli ekip çalışması parçasında tıklattığınızda, otomatik olarak ekip çalışması uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="5eeca-213">When you click the Teamwork tile in the Access Panel, you should get automatically signed-on to your Teamwork application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="5eeca-214">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="5eeca-214">Additional resources</span></span>

* [<span data-ttu-id="5eeca-215">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="5eeca-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5eeca-216">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="5eeca-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_203.png