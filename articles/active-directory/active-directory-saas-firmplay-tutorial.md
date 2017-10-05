---
title: "Öğretici: Azure Active Directory Tümleştirme FirmPlay - işe alma için çalışan hakları ile | Microsoft Docs"
description: "Çoklu oturum açma FirmPlay - çalışan hakları işe alma için Azure Active Directory arasındaki yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 3cddd5b9508159089bf344dbb3882d462799747c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="0436a-103">Öğretici: Azure Active Directory Tümleştirme ile FirmPlay - işe alma için çalışan hakları</span><span class="sxs-lookup"><span data-stu-id="0436a-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="0436a-104">Bu öğreticide, Azure Active Directory (Azure AD) ile işe alma için çalışan hakları FirmPlay - tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="0436a-104">In this tutorial, you learn how to integrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0436a-105">FirmPlay - Azure AD ile işe alma için çalışan hakları tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="0436a-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0436a-106">FirmPlay - çalışan hakları işe alma için erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0436a-106">You can control in Azure AD who has access to FirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="0436a-107">Otomatik olarak FirmPlay - işe alma (çoklu oturum açma) Azure AD hesaplarına sahip çalışan hakları için açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0436a-107">You can enable your users to automatically get signed-on to FirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0436a-108">Hesaplarınızı bir merkezi konumda - Azure Yönetim Portalı'nı yönetme</span><span class="sxs-lookup"><span data-stu-id="0436a-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="0436a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0436a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0436a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0436a-110">Prerequisites</span></span>

<span data-ttu-id="0436a-111">Azure AD tümleştirme FirmPlay - işe alma, çalışan hakları ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="0436a-111">To configure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need the following items:</span></span>

- <span data-ttu-id="0436a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="0436a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0436a-113">FirmPlay - çoklu oturum açma etkin abonelik işe alma için çalışan hakları</span><span class="sxs-lookup"><span data-stu-id="0436a-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="0436a-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="0436a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="0436a-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0436a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0436a-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0436a-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="0436a-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0436a-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="0436a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="0436a-118">Scenario description</span></span>
<span data-ttu-id="0436a-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="0436a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0436a-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="0436a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0436a-121">İşe alma galerisinden çalışan hakları FirmPlay - ekleme</span><span class="sxs-lookup"><span data-stu-id="0436a-121">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
2. <span data-ttu-id="0436a-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0436a-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-the-gallery"></a><span data-ttu-id="0436a-123">İşe alma galerisinden çalışan hakları FirmPlay - ekleme</span><span class="sxs-lookup"><span data-stu-id="0436a-123">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
<span data-ttu-id="0436a-124">FirmPlay - Azure AD'ye işe alma için çalışan hakları tümleştirmesini yapılandırmak için çalışan hakları galerisinden işe alma listenize yönetilen SaaS uygulamaları için FirmPlay - eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0436a-124">To configure the integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need to add FirmPlay - Employee Advocacy for Recruiting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0436a-125">**İşe alma Galerisi'nden çalışan hakları FirmPlay - eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0436a-125">**To add FirmPlay - Employee Advocacy for Recruiting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0436a-126">İçinde  **[Azure Yönetim Portalı](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0436a-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0436a-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="0436a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0436a-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0436a-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="0436a-131">Tıklatın **Ekle** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0436a-131">Click **Add** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="0436a-133">Arama kutusuna **FirmPlay - işe alma için çalışan hakları**.</span><span class="sxs-lookup"><span data-stu-id="0436a-133">In the search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. <span data-ttu-id="0436a-135">Sonuçlar panelinde seçin **FirmPlay - işe alma için çalışan hakları**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0436a-135">In the results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0436a-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0436a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0436a-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma FirmPlay - işe alma "Britta Simon" adlı bir test kullanıcıyı temel alarak çalışan hakları ile test etme.</span><span class="sxs-lookup"><span data-stu-id="0436a-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0436a-139">Çoklu oturum açma çalışmak özelliğini için Azure AD FirmPlay ne karşılık gelen kullanıcı bilmek ister - çalışan hakları işe alma için bir kullanıcı Azure AD'de.</span><span class="sxs-lookup"><span data-stu-id="0436a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FirmPlay - Employee Advocacy for Recruiting is to a user in Azure AD.</span></span> <span data-ttu-id="0436a-140">Diğer bir deyişle, bir Azure AD kullanıcısının FirmPlay - çalışan hakları işe alma için ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0436a-140">In other words, a link relationship between an Azure AD user and the related user in FirmPlay - Employee Advocacy for Recruiting needs to be established.</span></span>

<span data-ttu-id="0436a-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** FirmPlay - işe alma için çalışan hakları içinde.</span><span class="sxs-lookup"><span data-stu-id="0436a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="0436a-142">Yapılandırma ve Azure AD çoklu oturum açma FirmPlay ile-test etmek için işe alma, çalışan hakları, aşağıdaki yapı taşları tamamlanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="0436a-142">To configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0436a-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="0436a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0436a-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="0436a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0436a-145">**[İşe alma test kullanıcısı için çalışan hakları FirmPlay - oluşturma](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)**  - FirmPlay içinde karşılık gelen Britta Simon, olmasını: çalışan başka bir deyişle işe alma için hakları bağlı her, Azure AD gösterimi.</span><span class="sxs-lookup"><span data-stu-id="0436a-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - to have a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="0436a-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="0436a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0436a-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="0436a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0436a-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0436a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0436a-149">Bu bölümde, Azure AD çoklu oturum açma Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma FirmPlay - çalışan hakları işe alma uygulaması için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0436a-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="0436a-150">**Azure AD çoklu oturum açma FirmPlay - işe alma, çalışan hakları yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0436a-150">**To configure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="0436a-151">Azure Yönetim Portalı'nda üzerinde **FirmPlay - işe alma için çalışan hakları** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="0436a-151">In the Azure Management portal, on the **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="0436a-153">Üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="0436a-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. <span data-ttu-id="0436a-155">Üzerinde **FirmPlay - işe alma etki alanı ve URL'ler için çalışan hakları** bölümünde **oturum üzerinde URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="0436a-155">On the **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="0436a-157">Lütfen bu gerçek değer olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0436a-157">Please note that this is not the real value.</span></span> <span data-ttu-id="0436a-158">Bu değer gerçek oturum üzerinde URL ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0436a-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="0436a-159">Kişi [FirmPlay - işe alma destek ekibi için çalışan hakları](mailto:engineering@firmplay.com) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="0436a-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to get this value.</span></span> 

4. <span data-ttu-id="0436a-160">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **yeni sertifika oluştur**.</span><span class="sxs-lookup"><span data-stu-id="0436a-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. <span data-ttu-id="0436a-162">Üzerinde **yeni sertifika oluştur** iletişim kutusunda, Takvim simgesine tıklayın ve bir **sona erme tarihi**.</span><span class="sxs-lookup"><span data-stu-id="0436a-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="0436a-163">Ardından **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0436a-163">Then click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="0436a-165">Üzerinde **SAML imzalama sertifikası** bölümünde, select **yeni sertifika etkin hale getirin** tıklatıp **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0436a-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. <span data-ttu-id="0436a-167">Açılır pencere üzerinde **geçiş sertifikası** penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="0436a-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="0436a-169">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0436a-169">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. <span data-ttu-id="0436a-171">Üzerinde **FirmPlay - işe alma yapılandırması için çalışan hakları** 'yi tıklatın **FirmPlay - çalışan hakları işe alma için yapılandırma** açmak için **yapılandırma oturum açma** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0436a-171">On the **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** to open **Configure sign-on** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. <span data-ttu-id="0436a-174">Uygulamanız için yapılandırılmış SSO almak için başvurun [FirmPlay - işe alma destek ekibi için çalışan hakları](mailto:engineering@firmplay.com) ve ile aşağıdakileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="0436a-174">To get SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with the following:</span></span> 

    <span data-ttu-id="0436a-175">• İndirilen **sertifika dosyası**</span><span class="sxs-lookup"><span data-stu-id="0436a-175">•  The downloaded **Certificate file**</span></span>

    <span data-ttu-id="0436a-176">• **SAML çoklu oturum açma hizmeti URL'si**</span><span class="sxs-lookup"><span data-stu-id="0436a-176">•  The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="0436a-177">• **SAML varlık kimliği**</span><span class="sxs-lookup"><span data-stu-id="0436a-177">•  The **SAML Entity ID**</span></span>

    <span data-ttu-id="0436a-178">• **Oturum kapatma URL'si**</span><span class="sxs-lookup"><span data-stu-id="0436a-178">•  The **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0436a-179">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0436a-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="0436a-180">Bu bölümün amacı, Britta Simon adlı Azure Yönetim Portalı'nda bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="0436a-180">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="0436a-182">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0436a-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0436a-183">İçinde **Azure Yönetim Portalı**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0436a-183">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0436a-185">Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="0436a-185">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0436a-187">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0436a-187">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0436a-189">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0436a-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0436a-191">a.</span><span class="sxs-lookup"><span data-stu-id="0436a-191">a.</span></span> <span data-ttu-id="0436a-192">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0436a-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0436a-193">b.</span><span class="sxs-lookup"><span data-stu-id="0436a-193">b.</span></span> <span data-ttu-id="0436a-194">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="0436a-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0436a-195">c.</span><span class="sxs-lookup"><span data-stu-id="0436a-195">c.</span></span> <span data-ttu-id="0436a-196">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="0436a-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0436a-197">d.</span><span class="sxs-lookup"><span data-stu-id="0436a-197">d.</span></span> <span data-ttu-id="0436a-198">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0436a-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="0436a-199">İşe alma test kullanıcısı için çalışan hakları FirmPlay - oluşturma</span><span class="sxs-lookup"><span data-stu-id="0436a-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="0436a-200">Bu bölümde, Britta Simon FirmPlay - işe alma için çalışan hakları adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0436a-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="0436a-201">Lütfen çalışmak [FirmPlay - işe alma destek ekibi için çalışan hakları](mailto:engineering@firmplay.com) FirmPlay - çalışan hakları işe alma platform için kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="0436a-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to add the users in the FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0436a-202">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="0436a-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0436a-203">Bu bölümde, Britta FirmPlay - işe alma için çalışan hakları için kendi erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0436a-203">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FirmPlay - Employee Advocacy for Recruiting.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="0436a-205">**Britta Simon FirmPlay - işe alma, çalışan hakları atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0436a-205">**To assign Britta Simon to FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="0436a-206">Azure Yönetim Portalı'nda uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0436a-206">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="0436a-208">Uygulamalar listesinde **FirmPlay - işe alma için çalışan hakları**.</span><span class="sxs-lookup"><span data-stu-id="0436a-208">In the applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. <span data-ttu-id="0436a-210">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="0436a-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="0436a-212">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0436a-212">Click **Add** button.</span></span> <span data-ttu-id="0436a-213">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0436a-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="0436a-215">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="0436a-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0436a-216">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0436a-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0436a-217">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0436a-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="0436a-218">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="0436a-218">Testing single sign-on</span></span>

<span data-ttu-id="0436a-219">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="0436a-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0436a-220">FirmPlay - çalışan hakları erişim panelinde, işe alma döşemeye tıklattığınızda, otomatik olarak FirmPlay - çalışan hakları işe alma uygulaması için açan.</span><span class="sxs-lookup"><span data-stu-id="0436a-220">When you click the FirmPlay - Employee Advocacy for Recruiting tile in the Access Panel, you should get automatically signed-on to your FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0436a-221">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0436a-221">Additional resources</span></span>

* [<span data-ttu-id="0436a-222">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="0436a-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0436a-223">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="0436a-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png