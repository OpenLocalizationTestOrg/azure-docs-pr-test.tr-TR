---
title: "Öğretici: Azure Active Directory Tümleştirme ile PlanMyLeave | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile PlanMyLeave arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: ba418a641b339a0d94a3c7b2596d37fbd88a30c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="57958-103">Öğretici: Azure Active Directory Tümleştirme PlanMyLeave ile</span><span class="sxs-lookup"><span data-stu-id="57958-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="57958-104">Bu öğreticide, Azure Active Directory (Azure AD) ile PlanMyLeave tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="57958-104">In this tutorial, you learn how to integrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="57958-105">PlanMyLeave Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="57958-105">Integrating PlanMyLeave with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="57958-106">PlanMyLeave erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="57958-106">You can control in Azure AD who has access to PlanMyLeave</span></span>
- <span data-ttu-id="57958-107">Otomatik olarak için PlanMyLeave (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="57958-107">You can enable your users to automatically get signed-on to PlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="57958-108">Hesaplarınızı bir merkezi konumda - Azure Yönetim Portalı'nı yönetme</span><span class="sxs-lookup"><span data-stu-id="57958-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="57958-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="57958-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57958-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="57958-110">Prerequisites</span></span>

<span data-ttu-id="57958-111">Azure AD tümleştirme PlanMyLeave ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="57958-111">To configure Azure AD integration with PlanMyLeave, you need the following items:</span></span>

- <span data-ttu-id="57958-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="57958-112">An Azure AD subscription</span></span>
- <span data-ttu-id="57958-113">Bir PlanMyLeave çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="57958-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="57958-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="57958-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="57958-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="57958-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="57958-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="57958-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="57958-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57958-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="57958-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="57958-118">Scenario description</span></span>
<span data-ttu-id="57958-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="57958-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="57958-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="57958-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="57958-121">Galeriden PlanMyLeave ekleme</span><span class="sxs-lookup"><span data-stu-id="57958-121">Adding PlanMyLeave from the gallery</span></span>
2. <span data-ttu-id="57958-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="57958-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-the-gallery"></a><span data-ttu-id="57958-123">Galeriden PlanMyLeave ekleme</span><span class="sxs-lookup"><span data-stu-id="57958-123">Adding PlanMyLeave from the gallery</span></span>
<span data-ttu-id="57958-124">Azure AD PlanMyLeave tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden PlanMyLeave eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="57958-124">To configure the integration of PlanMyLeave into Azure AD, you need to add PlanMyLeave from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="57958-125">**Galeriden PlanMyLeave eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="57958-125">**To add PlanMyLeave from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="57958-126">İçinde  **[Azure Yönetim Portalı](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="57958-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="57958-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="57958-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="57958-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="57958-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="57958-131">Tıklatın **Ekle** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="57958-131">Click **Add** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="57958-133">Arama kutusuna **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="57958-133">In the search box, type **PlanMyLeave**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="57958-135">Sonuçlar panelinde seçin **PlanMyLeave**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="57958-135">In the results panel, select **PlanMyLeave**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="57958-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="57958-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="57958-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı PlanMyLeave sınayın.</span><span class="sxs-lookup"><span data-stu-id="57958-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="57958-139">Tekli çalışmaya oturum için Azure AD PlanMyLeave karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="57958-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PlanMyLeave is to a user in Azure AD.</span></span> <span data-ttu-id="57958-140">Diğer bir deyişle, bir Azure AD kullanıcısının PlanMyLeave ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="57958-140">In other words, a link relationship between an Azure AD user and the related user in PlanMyLeave needs to be established.</span></span>

<span data-ttu-id="57958-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** PlanMyLeave içinde.</span><span class="sxs-lookup"><span data-stu-id="57958-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="57958-142">Yapılandırma ve Azure AD çoklu oturum açma PlanMyLeave ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="57958-142">To configure and test Azure AD single sign-on with PlanMyLeave, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="57958-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="57958-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="57958-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="57958-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="57958-145">**[PlanMyLeave test kullanıcısı oluşturma](#creating-a-planmyleave-test-user)**  - Britta Simon, karşılık gelen her, Azure AD gösterimine bağlı PlanMyLeave sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="57958-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - to have a counterpart of Britta Simon in PlanMyLeave that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="57958-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="57958-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="57958-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="57958-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="57958-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="57958-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="57958-149">Bu bölümde, Azure AD çoklu oturum açma Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma PlanMyLeave uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="57958-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="57958-150">**Azure AD çoklu oturum açma ile PlanMyLeave yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="57958-150">**To configure Azure AD single sign-on with PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="57958-151">Azure Yönetim Portalı'nda üzerinde **PlanMyLeave** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="57958-151">In the Azure Management portal, on the **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="57958-153">Üzerinde **çoklu oturum açma** iletişim sayfası olarak **modu** seçin **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="57958-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="57958-155">Üzerinde **PlanMyLeave etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="57958-155">On the **PlanMyLeave Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="57958-157">a.</span><span class="sxs-lookup"><span data-stu-id="57958-157">a.</span></span> <span data-ttu-id="57958-158">İçinde **oturum üzerinde URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company-name>.planmyleave.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="57958-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="57958-159">b.</span><span class="sxs-lookup"><span data-stu-id="57958-159">b.</span></span> <span data-ttu-id="57958-160">İçinde **tanımlayıcı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company-name>.planmyleave.com`</span><span class="sxs-lookup"><span data-stu-id="57958-160">In the **Identifer** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="57958-161">Lütfen bu gerçek değerlerin olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="57958-161">Please note that these are not the real values.</span></span> <span data-ttu-id="57958-162">Bu değerler gerçek oturum üzerinde URL ve tanımlayıcıdır ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="57958-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="57958-163">Kişi [PlanMyLeave destek ekibi](mailto:support@planmyleave.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="57958-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) to get these values.</span></span>

4. <span data-ttu-id="57958-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **yeni sertifika oluştur**.</span><span class="sxs-lookup"><span data-stu-id="57958-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="57958-166">Üzerinde **yeni sertifika oluştur** iletişim kutusunda, Takvim simgesine tıklayın ve bir **sona erme tarihi**.</span><span class="sxs-lookup"><span data-stu-id="57958-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="57958-167">Ardından **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="57958-167">Then click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="57958-169">Üzerinde **SAML imzalama sertifikası** bölümünde, select **yeni sertifika etkin hale getirin** tıklatıp **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="57958-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="57958-171">Açılır pencere üzerinde **geçiş sertifikası** penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="57958-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="57958-173">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="57958-173">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="57958-175">Üzerinde **PlanMyLeave yapılandırma** 'yi tıklatın **yapılandırma PlanMyLeave** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="57958-175">On the **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** to open **Configure sign-on** window.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="57958-178">Farklı web tarayıcısı penceresinde PlanMyLeave Kiracı yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="57958-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="57958-179">Git **sistem kurulumu**.</span><span class="sxs-lookup"><span data-stu-id="57958-179">Go to **System Setup**.</span></span> <span data-ttu-id="57958-180">Sonra da **güvenlik yönetimi** bölümünde **şirket SAML ayarları** .</span><span class="sxs-lookup"><span data-stu-id="57958-180">Then on the **Security Management** section click **Company SAML settings** .</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="57958-182">Üzerinde **SAML ayarları** bölümünde, düzenleyici simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="57958-182">On the **SAML Settings** section, click editor icon.</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="57958-184">Üzerinde **güncelleştirme SAML ayarlarını** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="57958-184">On the **Update SAML Settings** section, perform the following steps:</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="57958-186">a.</span><span class="sxs-lookup"><span data-stu-id="57958-186">a.</span></span>  <span data-ttu-id="57958-187">İçinde **oturum açma URL'si** metin kutusuna, put değerini **SAML çoklu oturum açma hizmet URL'si** Azure AD uygulama yapılandırma penceresinden.</span><span class="sxs-lookup"><span data-stu-id="57958-187">In the **Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="57958-188">b.</span><span class="sxs-lookup"><span data-stu-id="57958-188">b.</span></span>  <span data-ttu-id="57958-189">Açık, indirilen sertifika dosyasını Not Defteri'nde kopyalayın yalnızca içeriği---başlamak sertifika---ve---bitiş---'ın sertifikasını, Pano içine arasında ve kendisine yapıştırma **sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="57958-189">Open your downloaded certificate file in notepad, copy only the content between the ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>

    <span data-ttu-id="57958-190">c.</span><span class="sxs-lookup"><span data-stu-id="57958-190">c.</span></span> <span data-ttu-id="57958-191">Ayarlama "**etkin**"için"**Evet**".</span><span class="sxs-lookup"><span data-stu-id="57958-191">Set "**Is Enable**" to "**Yes**".</span></span>

    <span data-ttu-id="57958-192">d.</span><span class="sxs-lookup"><span data-stu-id="57958-192">d.</span></span> <span data-ttu-id="57958-193">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="57958-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="57958-194">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="57958-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="57958-195">Bu bölümün amacı, Britta Simon adlı Azure Yönetim Portalı'nda bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="57958-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="57958-197">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="57958-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="57958-198">İçinde **Azure Yönetim Portalı**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="57958-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="57958-200">Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="57958-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="57958-202">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="57958-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="57958-204">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="57958-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="57958-206">a.</span><span class="sxs-lookup"><span data-stu-id="57958-206">a.</span></span> <span data-ttu-id="57958-207">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="57958-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="57958-208">b.</span><span class="sxs-lookup"><span data-stu-id="57958-208">b.</span></span> <span data-ttu-id="57958-209">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="57958-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="57958-210">c.</span><span class="sxs-lookup"><span data-stu-id="57958-210">c.</span></span> <span data-ttu-id="57958-211">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="57958-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="57958-212">d.</span><span class="sxs-lookup"><span data-stu-id="57958-212">d.</span></span> <span data-ttu-id="57958-213">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="57958-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="57958-214">PlanMyLeave test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="57958-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="57958-215">Bu bölümün amacı Britta Simon içinde PlanMyLeave adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="57958-215">The objective of this section is to create a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="57958-216">PlanMyLeave yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="57958-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="57958-217">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="57958-217">There is no action item for you in this section.</span></span> <span data-ttu-id="57958-218">Yeni bir kullanıcı henüz yoksa PlanMyLeave erişme denemesi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="57958-218">A new user will be created during an attempt to access PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="57958-219">Bir kullanıcı el ile oluşturmanız gerekiyorsa, başvurmanız gerekir [PlanMyLeave destek ekibi](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="57958-219">If you need to create an user manually, you need to contact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="57958-220">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="57958-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="57958-221">Bu bölümde, Britta PlanMyLeave için kendi erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="57958-221">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to PlanMyLeave.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="57958-223">**PlanMyLeave için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="57958-223">**To assign Britta Simon to PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="57958-224">Azure Yönetim Portalı'nda uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="57958-224">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="57958-226">Uygulamalar listesinde **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="57958-226">In the applications list, select **PlanMyLeave**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="57958-228">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="57958-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="57958-230">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="57958-230">Click **Add** button.</span></span> <span data-ttu-id="57958-231">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="57958-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="57958-233">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="57958-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="57958-234">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="57958-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="57958-235">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="57958-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="57958-236">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="57958-236">Testing single sign-on</span></span>

<span data-ttu-id="57958-237">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="57958-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="57958-238">Erişim paneli PlanMyLeave parçasında tıklattığınızda, otomatik olarak PlanMyLeave uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="57958-238">When you click the PlanMyLeave tile in the Access Panel, you should get automatically signed-on to your PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="57958-239">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="57958-239">Additional resources</span></span>

* [<span data-ttu-id="57958-240">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="57958-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57958-241">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="57958-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png