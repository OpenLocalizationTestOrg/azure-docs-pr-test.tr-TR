---
title: "Öğretici: Azure Active Directory Tümleştirme ile @Task| Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory arasında yapılandırmayı öğrenin ve @Task."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: ebb19ca6cbaf04106fbce937d95651e709854cfd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="ef91d-103">Öğretici: Azure Active Directory ile tümleştirme@Task</span><span class="sxs-lookup"><span data-stu-id="ef91d-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="ef91d-104">Bu öğreticinin amacı nasıl tümleştirileceği Göster sağlamaktır @Task Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ef91d-104">The objective of this tutorial is to show you how to integrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="ef91d-105">Tümleştirme @Task Azure AD ile aşağıdaki faydaları sağlar:</span><span class="sxs-lookup"><span data-stu-id="ef91d-105">Integrating @Task with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="ef91d-106">Erişebilen Azure AD'de kontrol edebilirsiniz@Task</span><span class="sxs-lookup"><span data-stu-id="ef91d-106">You can control in Azure AD who has access to @Task</span></span>
* <span data-ttu-id="ef91d-107">Oturum açma için otomatik olarak almak, kullanıcılarınızın etkinleştirebilirsiniz @Task (çoklu oturum açma) Azure AD hesaplarına sahip</span><span class="sxs-lookup"><span data-stu-id="ef91d-107">You can enable your users to automatically get signed-on to @Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="ef91d-108">Hesaplarınızı bir merkezi konumda - Klasik Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="ef91d-108">You can manage your accounts in one central location - the Azure classic Portal</span></span>

<span data-ttu-id="ef91d-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ef91d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef91d-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ef91d-110">Prerequisites</span></span>
<span data-ttu-id="ef91d-111">Azure AD ile tümleştirme yapılandırmak için @Task, aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="ef91d-111">To configure Azure AD integration with @Task, you need the following items:</span></span>

* <span data-ttu-id="ef91d-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="ef91d-112">An Azure AD subscription</span></span>
* <span data-ttu-id="ef91d-113">Bir @Task çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="ef91d-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ef91d-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="ef91d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="ef91d-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ef91d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="ef91d-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef91d-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="ef91d-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ef91d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="ef91d-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="ef91d-118">Scenario Description</span></span>
<span data-ttu-id="ef91d-119">Bu öğreticinin amacı, Azure AD çoklu oturum açma bir test ortamında test etmenizi hale getirmektir.</span><span class="sxs-lookup"><span data-stu-id="ef91d-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="ef91d-120">Bu öğreticide verilen senaryoda üç ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="ef91d-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="ef91d-121">Ekleme @Task galerisinden</span><span class="sxs-lookup"><span data-stu-id="ef91d-121">Adding @Task from the gallery</span></span> 
2. <span data-ttu-id="ef91d-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ef91d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-the-gallery"></a><span data-ttu-id="ef91d-123">Ekleme @Task galerisinden</span><span class="sxs-lookup"><span data-stu-id="ef91d-123">Adding @Task from the gallery</span></span>
<span data-ttu-id="ef91d-124">Tümleştirmesini yapılandırmak için @Task eklemenize gerek Azure AD ile @Task yönetilen SaaS uygulamaları listenize galerisinden.</span><span class="sxs-lookup"><span data-stu-id="ef91d-124">To configure the integration of @Task into Azure AD, you need to add @Task from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ef91d-125">**Eklenecek @Task Galeriden, aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ef91d-125">**To add @Task from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ef91d-126">İçinde **Klasik Azure portalı**, sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 
2. <span data-ttu-id="ef91d-128">Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="ef91d-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ef91d-129">Dizin görünümünde uygulamaları görünümü açmak için **uygulamaları** üst menüde.</span><span class="sxs-lookup"><span data-stu-id="ef91d-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Uygulamalar][2] 
4. <span data-ttu-id="ef91d-131">Tıklatın **Ekle** sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="ef91d-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Uygulamalar][3] 
5. <span data-ttu-id="ef91d-133">Üzerinde **ne yapmak istiyorsunuz** iletişim kutusunda, tıklatın **Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Uygulamalar][4] 
6. <span data-ttu-id="ef91d-135">Arama kutusuna  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="ef91d-135">In the search box, type **@Task**.</span></span>
   
    ![Uygulamalar][5] 
7. <span data-ttu-id="ef91d-137">Sonuçlar bölmesinde seçin  **@Task** ve ardından **tam** uygulama eklemek için.</span><span class="sxs-lookup"><span data-stu-id="ef91d-137">In the results pane, select **@Task**, and then click **Complete** to add the application.</span></span>
   
    ![Uygulamalar][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ef91d-139">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ef91d-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ef91d-140">Nasıl yapılandırılacağı ve Azure AD çoklu oturum açma ile test göstermek için bu bölümün amacı olan @Task "Britta Simon" adlı bir test kullanıcı tabanlı.</span><span class="sxs-lookup"><span data-stu-id="ef91d-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ef91d-141">Tekli çalışmaya oturum için Azure AD içinde karşılık gelen kullanıcının bilmek ister @Task bir kullanıcı Azure AD'de sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="ef91d-141">For single sign-on to work, Azure AD needs to know what the counterpart user in @Task to an user in Azure AD is.</span></span> <span data-ttu-id="ef91d-142">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı arasında bir bağlantı ilişki @Task kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef91d-142">In other words, a link relationship between an Azure AD user and the related user in @Task needs to be established.</span></span>   
<span data-ttu-id="ef91d-143">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** içinde @Task.</span><span class="sxs-lookup"><span data-stu-id="ef91d-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in @Task.</span></span>

<span data-ttu-id="ef91d-144">Yapılandırma ve Azure AD çoklu oturum açma ile test etmek için @Task, aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ef91d-144">To configure and test Azure AD single sign-on with @Task, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ef91d-145">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ef91d-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ef91d-146">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="ef91d-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ef91d-147">**[Oluşturma bir @Tasktest kullanıcı](#creating-a-halogen-software-test-user)**  - Britta Simon, karşılık gelen olmasını @Taskthat her, Azure AD gösterimine bağlandı.</span><span class="sxs-lookup"><span data-stu-id="ef91d-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in @Taskthat is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="ef91d-148">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ef91d-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ef91d-149">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ef91d-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ef91d-150">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ef91d-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="ef91d-151">Azure AD çoklu oturum açma Klasik Azure portalındaki etkinleştirmek ve çoklu oturum açma içinde yapılandırmak için bu bölümün amacı olan, @Task uygulama.</span><span class="sxs-lookup"><span data-stu-id="ef91d-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your @Task application.</span></span>

<span data-ttu-id="ef91d-152">**Azure AD çoklu oturum açma ile yapılandırmak için @Task, aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ef91d-152">**To configure Azure AD single sign-on with @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="ef91d-153">Azure Klasik portalında üzerinde  **@Task**  uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma özelliğini yapılandırın** açmak için **yapılandırma çoklu oturum açma** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ef91d-153">In the Azure classic portal, on the **@Task** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][6] 
2. <span data-ttu-id="ef91d-155">Üzerinde **oturum kullanıcılara nasıl istiyorsunuz @Task**  sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-155">On the **How would you like users to sign on to @Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD çoklu oturum açma][7] 
3. <span data-ttu-id="ef91d-157">Üzerinde **uygulama ayarlarını yapılandır** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ef91d-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Uygulama ayarlarını yapılandırın][8] 
   
     <span data-ttu-id="ef91d-159">a.</span><span class="sxs-lookup"><span data-stu-id="ef91d-159">a.</span></span> <span data-ttu-id="ef91d-160">İçinde **oturum üzerinde URL'si** metin kutusuna, türü URL'yi, kullanıcılarınıza oturum açma tarafından kullanılan, @Task uygulama (örn:*https://<Tenant name>.attask ondemand.com*).</span><span class="sxs-lookup"><span data-stu-id="ef91d-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="ef91d-161">b.</span><span class="sxs-lookup"><span data-stu-id="ef91d-161">b.</span></span> <span data-ttu-id="ef91d-162">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef91d-162">Click **Next**.</span></span>
4. <span data-ttu-id="ef91d-163">Üzerinde **çoklu oturum açma sırasında yapılandırma @Task**  sayfasında, **karşıdan meta veri**, yerel olarak bilgisayarınızda meta veri dosyasını kaydedin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-163">On the **Configure single sign-on at @Task** page, click **Download metadata**, save the metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![Azure AD Connect nedir?][9] 
5. <span data-ttu-id="ef91d-165">Oturum açma için sizin @Task yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="ef91d-165">Sign-on to your @Task company site as administrator.</span></span>
6. <span data-ttu-id="ef91d-166">Git **tek oturum açma yapılandırması**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-166">Go to **Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="ef91d-167">Üzerinde **çoklu oturum açma** iletişim kutusunda, aşağıdaki adımları uygulayın</span><span class="sxs-lookup"><span data-stu-id="ef91d-167">On the **Single Sign-On** dialog, perform the following steps</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][23]
   
    <span data-ttu-id="ef91d-169">a.</span><span class="sxs-lookup"><span data-stu-id="ef91d-169">a.</span></span> <span data-ttu-id="ef91d-170">Olarak **türü**seçin **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="ef91d-171">b.</span><span class="sxs-lookup"><span data-stu-id="ef91d-171">b.</span></span> <span data-ttu-id="ef91d-172">Seçin **hizmet sağlayıcı kimliği**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="ef91d-173">c.</span><span class="sxs-lookup"><span data-stu-id="ef91d-173">c.</span></span> <span data-ttu-id="ef91d-174">Azure Klasik portalı üzerinde kopyalama **uzaktan oturum açma URL'si**ve ardından yapıştırın **oturum açma portalı URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="ef91d-174">On the Azure classic portal, copy the **Remote Login URL**, and then paste it into the **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="ef91d-175">d.</span><span class="sxs-lookup"><span data-stu-id="ef91d-175">d.</span></span> <span data-ttu-id="ef91d-176">Azure Klasik portalı üzerinde kopyalama **tek Sign-Out hizmeti URL'si**ve ardından yapıştırın **Sign-Out URL** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="ef91d-176">On the Azure classic portal, copy the **Single Sign-Out Service URL**, and then paste it into the **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="ef91d-177">e.</span><span class="sxs-lookup"><span data-stu-id="ef91d-177">e.</span></span> <span data-ttu-id="ef91d-178">Azure Klasik portalı üzerinde kopyalama **değişiklik parola URL'si**ve ardından yapıştırın **değişiklik parola URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="ef91d-178">On the Azure classic portal, copy the **Change Password URL**, and then paste it into the **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="ef91d-179">f.</span><span class="sxs-lookup"><span data-stu-id="ef91d-179">f.</span></span> <span data-ttu-id="ef91d-180">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef91d-180">Click **Save**.</span></span>
8. <span data-ttu-id="ef91d-181">Klasik Azure portalı, çoklu oturum açma yapılandırması onay seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-181">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Azure AD Connect nedir?][10]
9. <span data-ttu-id="ef91d-183">Üzerinde **tek oturum açma onay** sayfasında, **tam**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-183">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Connect nedir?][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ef91d-185">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ef91d-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="ef91d-186">Bu bölümün amacı, Britta Simon adlı Klasik Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="ef91d-186">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Azure AD Kullanıcı oluşturma][20]

<span data-ttu-id="ef91d-188">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ef91d-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ef91d-189">İçinde **Klasik Azure portalı**, sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-189">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="ef91d-191">Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="ef91d-191">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ef91d-192">Üstteki menüde kullanıcıların listesini görüntülemek için tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-192">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="ef91d-194">Açmak için **Kullanıcı Ekle** iletişim kutusunda, araç çubuğunda alt tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-194">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="ef91d-196">Üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ef91d-196">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="ef91d-198">a.</span><span class="sxs-lookup"><span data-stu-id="ef91d-198">a.</span></span> <span data-ttu-id="ef91d-199">Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="ef91d-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="ef91d-200">b.</span><span class="sxs-lookup"><span data-stu-id="ef91d-200">b.</span></span> <span data-ttu-id="ef91d-201">Kullanıcı adı **textbox**, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-201">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="ef91d-202">c.</span><span class="sxs-lookup"><span data-stu-id="ef91d-202">c.</span></span> <span data-ttu-id="ef91d-203">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef91d-203">Click **Next**.</span></span>
6. <span data-ttu-id="ef91d-204">Üzerinde **kullanıcı profili** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ef91d-204">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="ef91d-206">a.</span><span class="sxs-lookup"><span data-stu-id="ef91d-206">a.</span></span> <span data-ttu-id="ef91d-207">İçinde **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-207">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="ef91d-208">b.</span><span class="sxs-lookup"><span data-stu-id="ef91d-208">b.</span></span> <span data-ttu-id="ef91d-209">İçinde **Soyadı** metin kutusuna, türü, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-209">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="ef91d-210">c.</span><span class="sxs-lookup"><span data-stu-id="ef91d-210">c.</span></span> <span data-ttu-id="ef91d-211">İçinde **görünen adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-211">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="ef91d-212">d.</span><span class="sxs-lookup"><span data-stu-id="ef91d-212">d.</span></span> <span data-ttu-id="ef91d-213">İçinde **rol** listesinde **kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-213">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="ef91d-214">e.</span><span class="sxs-lookup"><span data-stu-id="ef91d-214">e.</span></span> <span data-ttu-id="ef91d-215">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef91d-215">Click **Next**.</span></span>

7. <span data-ttu-id="ef91d-216">Üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-216">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="ef91d-218">Üzerinde **Get geçici parola** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ef91d-218">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="ef91d-220">a.</span><span class="sxs-lookup"><span data-stu-id="ef91d-220">a.</span></span> <span data-ttu-id="ef91d-221">Değerini yazmak **yeni parola**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-221">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="ef91d-222">b.</span><span class="sxs-lookup"><span data-stu-id="ef91d-222">b.</span></span> <span data-ttu-id="ef91d-223">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef91d-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="ef91d-224">Oluşturma bir @Task test kullanıcısı</span><span class="sxs-lookup"><span data-stu-id="ef91d-224">Creating an @Task test user</span></span>
<span data-ttu-id="ef91d-225">Bu bölümün amacı Britta Simon adlı bir kullanıcı oluşturmaktır @Task.</span><span class="sxs-lookup"><span data-stu-id="ef91d-225">The objective of this section is to create a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="ef91d-226">**Britta Simon adlı bir kullanıcı oluşturmak için @Task, aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ef91d-226">**To create a user called Britta Simon in @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="ef91d-227">Oturum, @Task Yöneticisi olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="ef91d-227">Sign on to your @Task company site as administrator.</span></span>
2. <span data-ttu-id="ef91d-228">Üstteki menüde tıklatın **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-228">In the menu on the top, click **People**.</span></span>
3. <span data-ttu-id="ef91d-229">Tıklatın **yeni bir kişiye**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="ef91d-230">Yeni bir kişiye iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ef91d-230">On the New Person dialog, perform the following steps:</span></span>
   
    ![Oluşturma bir @Task test kullanıcısı][21] 
   
    <span data-ttu-id="ef91d-232">a.</span><span class="sxs-lookup"><span data-stu-id="ef91d-232">a.</span></span> <span data-ttu-id="ef91d-233">İçinde **ad** metin kutusuna, "Britta" yazın.</span><span class="sxs-lookup"><span data-stu-id="ef91d-233">In the **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="ef91d-234">b.</span><span class="sxs-lookup"><span data-stu-id="ef91d-234">b.</span></span> <span data-ttu-id="ef91d-235">İçinde **Soyadı** metin kutusuna, "Simon" yazın.</span><span class="sxs-lookup"><span data-stu-id="ef91d-235">In the **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="ef91d-236">c.</span><span class="sxs-lookup"><span data-stu-id="ef91d-236">c.</span></span> <span data-ttu-id="ef91d-237">İçinde **e-posta adresi** metin kutusuna, Azure Active Directory'de Britta Simon'ın e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="ef91d-237">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="ef91d-238">d.</span><span class="sxs-lookup"><span data-stu-id="ef91d-238">d.</span></span> <span data-ttu-id="ef91d-239">Tıklatın **kişiyi ekler**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-239">Click **Add Person**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ef91d-240">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="ef91d-240">Assigning the Azure AD test user</span></span>
<span data-ttu-id="ef91d-241">Her erişim vererek, Azure çoklu oturum açma kullanılacak Britta Simon etkinleştirmek için bu bölümün amacı olan @Task.</span><span class="sxs-lookup"><span data-stu-id="ef91d-241">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to @Task.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="ef91d-243">**Britta Simon atamak için @Task, aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ef91d-243">**To assign Britta Simon to @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="ef91d-244">Azure Klasik portalı üzerinde dizin görünümünde uygulamaları görünümü açmak için tıklatın **uygulamaları** üst menüde.</span><span class="sxs-lookup"><span data-stu-id="ef91d-244">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Kullanıcı atama][201] 
2. <span data-ttu-id="ef91d-246">Uygulamalar listesinde  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="ef91d-246">In the applications list, select **@Task**.</span></span>
   
    ![Kullanıcı atama][202] 
3. <span data-ttu-id="ef91d-248">Üstteki menüde tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-248">In the menu on the top, click **Users**.</span></span>
   
    ![Kullanıcı atama][203] 
4. <span data-ttu-id="ef91d-250">Kullanıcılar listesinden seçin **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-250">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="ef91d-251">Araç çubuğunda alt tıklatın **atamak**.</span><span class="sxs-lookup"><span data-stu-id="ef91d-251">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Kullanıcı atama][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="ef91d-253">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="ef91d-253">Testing Single Sign-On</span></span>
<span data-ttu-id="ef91d-254">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="ef91d-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="ef91d-255">Tıkladığınızda @Task döşeme erişim panelinde otomatik olarak oturum açmayı almanız gerekir, @Task uygulama.</span><span class="sxs-lookup"><span data-stu-id="ef91d-255">When you click the @Task tile in the Access Panel, you should get automatically signed-on to your @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ef91d-256">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ef91d-256">Additional Resources</span></span>
* [<span data-ttu-id="ef91d-257">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="ef91d-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ef91d-258">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="ef91d-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






