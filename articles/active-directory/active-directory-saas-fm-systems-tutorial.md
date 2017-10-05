---
title: "Öğretici: Azure Active Directory Tümleştirme ile FM:Systems | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile FM:Systems arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f78c58c5-6e98-458b-8991-78624a245665
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3a597d228f6c9234ec2fd2644ec3ac50b98f3b6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fmsystems"></a><span data-ttu-id="2e51b-103">Öğretici: Azure Active Directory Tümleştirme FM:Systems ile</span><span class="sxs-lookup"><span data-stu-id="2e51b-103">Tutorial: Azure Active Directory integration with FM:Systems</span></span>

<span data-ttu-id="2e51b-104">Bu öğreticide, Azure Active Directory (Azure AD) ile FM:Systems tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2e51b-104">In this tutorial, you learn how to integrate FM:Systems with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2e51b-105">FM:Systems Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="2e51b-105">Integrating FM:Systems with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2e51b-106">FM:Systems erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2e51b-106">You can control in Azure AD who has access to FM:Systems</span></span>
- <span data-ttu-id="2e51b-107">Otomatik olarak Azure AD hesaplarına sahip (çoklu oturum açma) FM:Systems için açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2e51b-107">You can enable your users to automatically get signed-on to FM:Systems (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2e51b-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="2e51b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2e51b-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2e51b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e51b-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2e51b-110">Prerequisites</span></span>

<span data-ttu-id="2e51b-111">Azure AD tümleştirme FM:Systems ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="2e51b-111">To configure Azure AD integration with FM:Systems, you need the following items:</span></span>

- <span data-ttu-id="2e51b-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="2e51b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2e51b-113">Bir FM:Systems çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="2e51b-113">An FM:Systems single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2e51b-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="2e51b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2e51b-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="2e51b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2e51b-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="2e51b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2e51b-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2e51b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2e51b-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="2e51b-118">Scenario description</span></span>
<span data-ttu-id="2e51b-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="2e51b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2e51b-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="2e51b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2e51b-121">Galeriden FM:Systems ekleme</span><span class="sxs-lookup"><span data-stu-id="2e51b-121">Adding FM:Systems from the gallery</span></span>
2. <span data-ttu-id="2e51b-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2e51b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fmsystems-from-the-gallery"></a><span data-ttu-id="2e51b-123">Galeriden FM:Systems ekleme</span><span class="sxs-lookup"><span data-stu-id="2e51b-123">Adding FM:Systems from the gallery</span></span>
<span data-ttu-id="2e51b-124">Azure AD FM:Systems tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden FM:Systems eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e51b-124">To configure the integration of FM:Systems into Azure AD, you need to add FM:Systems from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2e51b-125">**Galeriden FM:Systems eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2e51b-125">**To add FM:Systems from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2e51b-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2e51b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2e51b-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="2e51b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2e51b-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2e51b-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="2e51b-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2e51b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="2e51b-133">Arama kutusuna **FM:Systems**.</span><span class="sxs-lookup"><span data-stu-id="2e51b-133">In the search box, type **FM:Systems**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_search.png)

5. <span data-ttu-id="2e51b-135">Sonuçlar panelinde seçin **FM:Systems**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2e51b-135">In the results panel, select **FM:Systems**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2e51b-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2e51b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2e51b-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı FM:Systems sınayın.</span><span class="sxs-lookup"><span data-stu-id="2e51b-138">In this section, you configure and test Azure AD single sign-on with FM:Systems based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2e51b-139">Tekli çalışmaya oturum için Azure AD FM:Systems karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="2e51b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FM:Systems is to a user in Azure AD.</span></span> <span data-ttu-id="2e51b-140">Diğer bir deyişle, bir Azure AD kullanıcısının FM:Systems ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e51b-140">In other words, a link relationship between an Azure AD user and the related user in FM:Systems needs to be established.</span></span>

<span data-ttu-id="2e51b-141">FM:Systems içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="2e51b-141">In FM:Systems, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2e51b-142">Yapılandırma ve Azure AD çoklu oturum açma FM:Systems ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="2e51b-142">To configure and test Azure AD single sign-on with FM:Systems, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2e51b-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="2e51b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2e51b-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="2e51b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2e51b-145">**[Bir FM:Systems test kullanıcısı oluşturma](#creating-an-fmsystems-test-user)**  - bir Britta Simon karşılık gelen kullanıcı Azure AD gösterimini bağlı FM:Systems içinde olması.</span><span class="sxs-lookup"><span data-stu-id="2e51b-145">**[Creating an FM:Systems test user](#creating-an-fmsystems-test-user)** - to have a counterpart of Britta Simon in FM:Systems that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2e51b-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="2e51b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2e51b-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="2e51b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2e51b-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2e51b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2e51b-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma FM:Systems uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2e51b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FM:Systems application.</span></span>

<span data-ttu-id="2e51b-150">**Azure AD çoklu oturum açma ile FM:Systems yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2e51b-150">**To configure Azure AD single sign-on with FM:Systems, perform the following steps:**</span></span>

1. <span data-ttu-id="2e51b-151">Azure portalında üzerinde **FM:Systems** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="2e51b-151">In the Azure portal, on the **FM:Systems** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="2e51b-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="2e51b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_samlbase.png)

3. <span data-ttu-id="2e51b-155">Üzerinde **FM:Systems etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2e51b-155">On the **FM:Systems Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_url.png)

    <span data-ttu-id="2e51b-157">İçinde **yanıt URL'si** metin, FM:Systems yazın **yanıt URL'si**, şu biçimi kullanarak URL'yi yazın:`https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span><span class="sxs-lookup"><span data-stu-id="2e51b-157">In the **Reply URL** textbox, type your FM:Systems **Reply URL**, type the URL using the following pattern: `https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2e51b-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="2e51b-158">This value is not real.</span></span> <span data-ttu-id="2e51b-159">Bu değer ile gerçek yanıt URL'si güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2e51b-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="2e51b-160">Kişi [FM:Systems destek ekibi](https://fmsystems.com/ask-us/) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="2e51b-160">Contact [FM:Systems support team](https://fmsystems.com/ask-us/) to get this value.</span></span>
 
4. <span data-ttu-id="2e51b-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2e51b-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_certificate.png) 

5. <span data-ttu-id="2e51b-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2e51b-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-fm-systems-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2e51b-165">Çoklu oturum açma yapılandırmak için **FM:Systems** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [FM:Systems destek ekibi](https://fmsystems.com/ask-us/).</span><span class="sxs-lookup"><span data-stu-id="2e51b-165">To configure single sign-on on **FM:Systems** side, you need to send the downloaded **Metadata XML** to [FM:Systems support team](https://fmsystems.com/ask-us/).</span></span> <span data-ttu-id="2e51b-166">Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2e51b-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span> <span data-ttu-id="2e51b-167">SSO, aboneliğiniz için etkinleştirildiğinde, bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="2e51b-167">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="2e51b-168">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="2e51b-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2e51b-169">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="2e51b-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2e51b-170">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2e51b-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2e51b-171">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2e51b-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="2e51b-172">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="2e51b-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="2e51b-174">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2e51b-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2e51b-175">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2e51b-175">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2e51b-177">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2e51b-177">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2e51b-179">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="2e51b-179">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2e51b-181">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2e51b-181">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2e51b-183">a.</span><span class="sxs-lookup"><span data-stu-id="2e51b-183">a.</span></span> <span data-ttu-id="2e51b-184">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2e51b-184">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2e51b-185">b.</span><span class="sxs-lookup"><span data-stu-id="2e51b-185">b.</span></span> <span data-ttu-id="2e51b-186">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="2e51b-186">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2e51b-187">c.</span><span class="sxs-lookup"><span data-stu-id="2e51b-187">c.</span></span> <span data-ttu-id="2e51b-188">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="2e51b-188">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2e51b-189">d.</span><span class="sxs-lookup"><span data-stu-id="2e51b-189">d.</span></span> <span data-ttu-id="2e51b-190">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2e51b-190">Click **Create**.</span></span>
 
### <a name="creating-an-fmsystems-test-user"></a><span data-ttu-id="2e51b-191">Bir FM:Systems test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2e51b-191">Creating an FM:Systems test user</span></span>

1. <span data-ttu-id="2e51b-192">Bir web tarayıcısı penceresinde FM:Systems şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2e51b-192">In a web browser window, log into your FM:Systems company site as an administrator.</span></span>

2. <span data-ttu-id="2e51b-193">Git **Sistem Yönetimi \> Güvenliği Yönet \> kullanıcılar \> kullanıcı listesi**.</span><span class="sxs-lookup"><span data-stu-id="2e51b-193">Go to **System Administration \> Manage Security \> Users \> User list**.</span></span>
   
    <span data-ttu-id="2e51b-194">![Sistem Yönetimi](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "Sistem Yönetimi")</span><span class="sxs-lookup"><span data-stu-id="2e51b-194">![System Administration](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "System Administration")</span></span>

3. <span data-ttu-id="2e51b-195">Tıklatın **yeni kullanıcı oluştur**.</span><span class="sxs-lookup"><span data-stu-id="2e51b-195">Click **Create new user**.</span></span>
   
    <span data-ttu-id="2e51b-196">![Yeni kullanıcı oluşturmak](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "yeni kullanıcı oluşturun")</span><span class="sxs-lookup"><span data-stu-id="2e51b-196">![Create New User](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Create New User")</span></span>

4. <span data-ttu-id="2e51b-197">İçinde **kullanıcı oluştur** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2e51b-197">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="2e51b-198">![Kullanıcı oluşturma](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "kullanıcı oluştur")</span><span class="sxs-lookup"><span data-stu-id="2e51b-198">![Create User](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Create User")</span></span>
   
    <span data-ttu-id="2e51b-199">a.</span><span class="sxs-lookup"><span data-stu-id="2e51b-199">a.</span></span> <span data-ttu-id="2e51b-200">Tür **kullanıcıadı**, **parola**, **parolayı onaylayın**, **e-posta** ve **çalışan kimliği** , bir Geçerli bir Azure Active Directory hesabı ilgili metin kutularına içine sağlamak istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="2e51b-200">Type the **UserName**, the **Password**, **Confirm Password**, **E-mail** and the **Employee ID** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="2e51b-201">b.</span><span class="sxs-lookup"><span data-stu-id="2e51b-201">b.</span></span> <span data-ttu-id="2e51b-202">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2e51b-202">Click **Next**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2e51b-203">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="2e51b-203">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2e51b-204">Bu bölümde, Britta FM:Systems erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2e51b-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FM:Systems.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="2e51b-206">**FM:Systems için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2e51b-206">**To assign Britta Simon to FM:Systems, perform the following steps:**</span></span>

1. <span data-ttu-id="2e51b-207">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2e51b-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="2e51b-209">Uygulamalar listesinde **FM:Systems**.</span><span class="sxs-lookup"><span data-stu-id="2e51b-209">In the applications list, select **FM:Systems**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_app.png) 

3. <span data-ttu-id="2e51b-211">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="2e51b-211">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="2e51b-213">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2e51b-213">Click **Add** button.</span></span> <span data-ttu-id="2e51b-214">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2e51b-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="2e51b-216">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="2e51b-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2e51b-217">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2e51b-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2e51b-218">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2e51b-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2e51b-219">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="2e51b-219">Testing single sign-on</span></span>

<span data-ttu-id="2e51b-220">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="2e51b-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2e51b-221">Erişim paneli FM:Systems parçasında tıklattığınızda, otomatik olarak FM:Systems uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="2e51b-221">When you click the FM:Systems tile in the Access Panel, you should get automatically signed-on to your FM:Systems application.</span></span>
<span data-ttu-id="2e51b-222">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2e51b-222">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2e51b-223">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2e51b-223">Additional resources</span></span>

* [<span data-ttu-id="2e51b-224">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="2e51b-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2e51b-225">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="2e51b-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_203.png

