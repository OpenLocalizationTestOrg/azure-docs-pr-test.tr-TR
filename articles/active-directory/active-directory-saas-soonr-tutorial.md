---
title: "Öğretici: Azure Active Directory Tümleştirme ile Soonr çalışma | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Soonr çalışma arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 76946e4af624d70f2202601ee935523ca3db4314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="8a96e-103">Öğretici: Azure Active Directory Tümleştirme ile Soonr çalışma</span><span class="sxs-lookup"><span data-stu-id="8a96e-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="8a96e-104">Bu öğreticinin amacı Soonr çalışma alanına Azure Active Directory (Azure AD) ile tümleştirme Göster sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="8a96e-104">The objective of this tutorial is to show you how to integrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="8a96e-105">Soonr çalışma alanına Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="8a96e-105">Integrating Soonr Workplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8a96e-106">Soonr çalışma alanına erişimi olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8a96e-106">You can control in Azure AD who has access to Soonr Workplace</span></span>
- <span data-ttu-id="8a96e-107">Azure AD hesaplarına otomatik olarak (çoklu oturum açma) Soonr çalışma alanına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8a96e-107">You can enable your users to automatically get signed-on to Soonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8a96e-108">Hesaplarınızı bir merkezi konumda - Klasik Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="8a96e-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="8a96e-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8a96e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a96e-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8a96e-110">Prerequisites</span></span>

<span data-ttu-id="8a96e-111">Azure AD tümleştirme Soonr çalışma alanınız ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="8a96e-111">To configure Azure AD integration with Soonr Workplace, you need the following items:</span></span>

- <span data-ttu-id="8a96e-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="8a96e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8a96e-113">Bir Soonr çalışma alanı çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="8a96e-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="8a96e-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="8a96e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="8a96e-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8a96e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8a96e-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a96e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="8a96e-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8a96e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="8a96e-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="8a96e-118">Scenario description</span></span>
<span data-ttu-id="8a96e-119">Bu öğreticinin amacı, Azure AD çoklu oturum açma bir test ortamında test etmenizi hale getirmektir.</span><span class="sxs-lookup"><span data-stu-id="8a96e-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="8a96e-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="8a96e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a96e-121">Galeriden Soonr çalışma alanına ekleme</span><span class="sxs-lookup"><span data-stu-id="8a96e-121">Adding Soonr Workplace from the gallery</span></span>
2. <span data-ttu-id="8a96e-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="8a96e-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-the-gallery"></a><span data-ttu-id="8a96e-123">Galeriden Soonr çalışma alanına ekleme</span><span class="sxs-lookup"><span data-stu-id="8a96e-123">Adding Soonr Workplace from the gallery</span></span>
<span data-ttu-id="8a96e-124">Azure AD Soonr çalışma alanına tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Soonr çalışma alanına eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a96e-124">To configure the integration of Soonr Workplace into Azure AD, you need to add Soonr Workplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8a96e-125">**Galeriden Soonr çalışma alanına eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8a96e-125">**To add Soonr Workplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8a96e-126">İçinde **Klasik Azure portalı**, sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8a96e-128">Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="8a96e-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="8a96e-129">Dizin görünümünde uygulamaları görünümü açmak için **uygulamaları** üst menüde.</span><span class="sxs-lookup"><span data-stu-id="8a96e-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Uygulamalar][2]

4. <span data-ttu-id="8a96e-131">Tıklatın **Ekle** sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="8a96e-131">Click **Add** at the bottom of the page.</span></span>

    ![Uygulamalar][3]

5. <span data-ttu-id="8a96e-133">Üzerinde **ne yapmak istiyorsunuz** iletişim kutusunda, tıklatın **Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
 
    ![Uygulamalar][4]

6. <span data-ttu-id="8a96e-135">Arama kutusuna **Soonr çalışma alanına**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-135">In the search box, type **Soonr Workplace**.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="8a96e-137">Sonuçlar bölmesinde seçin **Soonr çalışma alanına**ve ardından **tam** uygulama eklemek için.</span><span class="sxs-lookup"><span data-stu-id="8a96e-137">In the results pane, select **Soonr Workplace**, and then click **Complete** to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8a96e-139">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="8a96e-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8a96e-140">Bu bölümün amacı nasıl yapılandırılacağı ve Azure AD çoklu oturum açma Soonr çalışma alanı ile test göstermek için "Britta Simon" adlı bir test kullanıcı dayalıdır.</span><span class="sxs-lookup"><span data-stu-id="8a96e-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8a96e-141">Tekli çalışmaya oturum için Azure AD Azure AD'de bir kullanıcıya karşılık gelen kullanıcı Soonr çalışma nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="8a96e-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Soonr Workplace to an user in Azure AD is.</span></span> <span data-ttu-id="8a96e-142">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı Soonr çalışma arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a96e-142">In other words, a link relationship between an Azure AD user and the related user in Soonr Workplace needs to be established.</span></span>  

<span data-ttu-id="8a96e-143">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Soonr çalışma.</span><span class="sxs-lookup"><span data-stu-id="8a96e-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="8a96e-144">Yapılandırma ve Azure AD çoklu oturum açma Soonr çalışma alanı ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8a96e-144">To configure and test Azure AD single sign-on with Soonr Workplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8a96e-145">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="8a96e-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8a96e-146">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="8a96e-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8a96e-147">**[Soonr çalışma alanına test kullanıcısı oluşturma](#creating-a-soonr-workplace-test-user)**  - Azure AD gösterimini her için bağlantılı Soonr çalışma Britta Simon, karşılık gelen sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="8a96e-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - to have a counterpart of Britta Simon in Soonr Workplace that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="8a96e-148">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="8a96e-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8a96e-149">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8a96e-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8a96e-150">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8a96e-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8a96e-151">Bu bölümde, Azure AD çoklu oturum açma Klasik portalında etkinleştirin ve çoklu oturum açma Soonr çalışma alanına uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8a96e-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="8a96e-152">**Azure AD çoklu oturum açma Soonr çalışma alanınız ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8a96e-152">**To configure Azure AD single sign-on with Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="8a96e-153">Azure Klasik portalında üzerinde **Soonr çalışma alanına** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma yapılandırmak** açmak için **yapılandırma çoklu oturum açma** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8a96e-153">In the Azure classic portal, on the **Soonr Workplace** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın][6] 

2. <span data-ttu-id="8a96e-155">Üzerinde **Soonr çalışma alanına oturum açmasını nasıl istiyorsunuz** sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-155">On the **How would you like users to sign on to Soonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="8a96e-157">Üzerinde **uygulama ayarlarını yapılandır** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:.</span><span class="sxs-lookup"><span data-stu-id="8a96e-157">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="8a96e-159">a.</span><span class="sxs-lookup"><span data-stu-id="8a96e-159">a.</span></span> <span data-ttu-id="8a96e-160">İçinde **oturum üzerinde URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="8a96e-160">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="8a96e-161">b.</span><span class="sxs-lookup"><span data-stu-id="8a96e-161">b.</span></span> <span data-ttu-id="8a96e-162">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8a96e-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8a96e-163">Lütfen bu gerçek değer olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8a96e-163">Please note that this is not the real value.</span></span> <span data-ttu-id="8a96e-164">Bu değer gerçek oturum üzerinde URL ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a96e-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="8a96e-165">Bu değer almak için Soonr çalışma alanına Destek ekibine başvurun.</span><span class="sxs-lookup"><span data-stu-id="8a96e-165">Contact Soonr Workplace support team to get this value.</span></span>

4. <span data-ttu-id="8a96e-166">Üzerinde **çoklu oturum açma Soonr yerindeki yapılandırma** sayfasında, **karşıdan meta veri** ve dosyayı bilgisayarınıza kaydedin:</span><span class="sxs-lookup"><span data-stu-id="8a96e-166">On the **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save the file on your computer:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="8a96e-168">Uygulamanız için yapılandırılmış SSO almak için Soonr çalışma alanına destek ekibinize başvurun ve aşağıdaki verin:</span><span class="sxs-lookup"><span data-stu-id="8a96e-168">To get SSO configured for your application, contact your Soonr Workplace support team and provide them with the following:</span></span> 

    <span data-ttu-id="8a96e-169">• İndirilen **meta veri** dosyası</span><span class="sxs-lookup"><span data-stu-id="8a96e-169">•  The downloaded **Metadata** file</span></span>

    <span data-ttu-id="8a96e-170">• **Veren URL'si**</span><span class="sxs-lookup"><span data-stu-id="8a96e-170">•  The **Issuer URL**</span></span>

    <span data-ttu-id="8a96e-171">• **SAML SSO URL'si**</span><span class="sxs-lookup"><span data-stu-id="8a96e-171">•  The **SAML SSO URL**</span></span>

    <span data-ttu-id="8a96e-172">• **Tek oturum kapatma hizmeti URL'si**</span><span class="sxs-lookup"><span data-stu-id="8a96e-172">•  The **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="8a96e-173">Bu uygulamanın yerine geçen <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask çalışma alanına</a> ve başvuruda bulunabilir <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">bu</a> öğretici Azure AD ile uygulama yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="8a96e-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring the application with Azure AD.</span></span>
   
6. <span data-ttu-id="8a96e-174">Klasik Azure portalı, çoklu oturum açma yapılandırması onay seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-174">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Azure AD çoklu oturum açma][10]

7. <span data-ttu-id="8a96e-176">Üzerinde **tek oturum açma onay** sayfasında, **tam**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-176">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Azure AD çoklu oturum açma][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8a96e-178">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8a96e-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="8a96e-179">Bu bölümün amacı, Britta Simon adlı Klasik Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="8a96e-179">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Azure AD Kullanıcı oluşturma][20]

<span data-ttu-id="8a96e-181">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8a96e-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8a96e-182">İçinde **Klasik Azure portalı**, sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="8a96e-184">Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="8a96e-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="8a96e-185">Üstteki menüde kullanıcıların listesini görüntülemek için tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-185">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8a96e-187">Açmak için **Kullanıcı Ekle** iletişim kutusunda, araç çubuğunda alt tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="8a96e-189">Üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8a96e-189">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="8a96e-191">a.</span><span class="sxs-lookup"><span data-stu-id="8a96e-191">a.</span></span> <span data-ttu-id="8a96e-192">Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="8a96e-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="8a96e-193">b.</span><span class="sxs-lookup"><span data-stu-id="8a96e-193">b.</span></span> <span data-ttu-id="8a96e-194">Kullanıcı adı **textbox**, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-194">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8a96e-195">c.</span><span class="sxs-lookup"><span data-stu-id="8a96e-195">c.</span></span> <span data-ttu-id="8a96e-196">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8a96e-196">Click **Next**.</span></span>

6.  <span data-ttu-id="8a96e-197">Üzerinde **kullanıcı profili** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8a96e-197">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="8a96e-199">a.</span><span class="sxs-lookup"><span data-stu-id="8a96e-199">a.</span></span> <span data-ttu-id="8a96e-200">İçinde **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-200">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="8a96e-201">b.</span><span class="sxs-lookup"><span data-stu-id="8a96e-201">b.</span></span> <span data-ttu-id="8a96e-202">İçinde **Soyadı** metin kutusuna, türü, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-202">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="8a96e-203">c.</span><span class="sxs-lookup"><span data-stu-id="8a96e-203">c.</span></span> <span data-ttu-id="8a96e-204">İçinde **görünen adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-204">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="8a96e-205">d.</span><span class="sxs-lookup"><span data-stu-id="8a96e-205">d.</span></span> <span data-ttu-id="8a96e-206">İçinde **rol** listesinde **kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-206">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="8a96e-207">e.</span><span class="sxs-lookup"><span data-stu-id="8a96e-207">e.</span></span> <span data-ttu-id="8a96e-208">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8a96e-208">Click **Next**.</span></span>

7. <span data-ttu-id="8a96e-209">Üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-209">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="8a96e-211">Üzerinde **Get geçici parola** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8a96e-211">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="8a96e-213">a.</span><span class="sxs-lookup"><span data-stu-id="8a96e-213">a.</span></span> <span data-ttu-id="8a96e-214">Değerini yazmak **yeni parola**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-214">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="8a96e-215">b.</span><span class="sxs-lookup"><span data-stu-id="8a96e-215">b.</span></span> <span data-ttu-id="8a96e-216">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8a96e-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="8a96e-217">Soonr çalışma alanına test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8a96e-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="8a96e-218">Bu bölümün amacı Britta Simon Soonr çalışma alanında adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="8a96e-218">The objective of this section is to create a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="8a96e-219">Platform bir kullanıcı oluşturmak için Soonr çalışma alanına destek ekibi ile çalışın.</span><span class="sxs-lookup"><span data-stu-id="8a96e-219">Please work with Soonr Workplace support team to create a user in the platform.</span></span> <span data-ttu-id="8a96e-220">Soonr ile destek bileti yükseltebilirsiniz <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">burada</a>.</span><span class="sxs-lookup"><span data-stu-id="8a96e-220">You can raise the support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8a96e-221">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="8a96e-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8a96e-222">Bu bölümün amacı Britta Soonr çalışma alanına her erişim vererek, Azure çoklu oturum açma kullanılacak Simon için etkinleştirmektir.</span><span class="sxs-lookup"><span data-stu-id="8a96e-222">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Soonr Workplace.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="8a96e-224">**Britta Simon Soonr çalışma alanına atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8a96e-224">**To assign Britta Simon to Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="8a96e-225">Azure Klasik portalı üzerinde dizin görünümünde uygulamaları görünümü açmak için tıklatın **uygulamaları** üst menüde.</span><span class="sxs-lookup"><span data-stu-id="8a96e-225">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="8a96e-227">Uygulamalar listesinde **Soonr çalışma alanına**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-227">In the applications list, select **Soonr Workplace**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="8a96e-229">Üstteki menüde tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-229">In the menu on the top, click **Users**.</span></span>

    ![Kullanıcı atama][203] 

1. <span data-ttu-id="8a96e-231">Kullanıcılar listesinden seçin **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-231">In the Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="8a96e-232">Araç çubuğunda alt tıklatın **atamak**.</span><span class="sxs-lookup"><span data-stu-id="8a96e-232">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Kullanıcı atama][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="8a96e-234">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="8a96e-234">Testing single sign-on</span></span>

<span data-ttu-id="8a96e-235">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="8a96e-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="8a96e-236">Erişim paneli Soonr çalışma alanına parçasında tıklattığınızda, otomatik olarak Soonr çalışma alanına uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="8a96e-236">When you click the Soonr Workplace tile in the Access Panel, you should get automatically signed-on to your Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8a96e-237">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8a96e-237">Additional resources</span></span>

* [<span data-ttu-id="8a96e-238">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="8a96e-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8a96e-239">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="8a96e-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
