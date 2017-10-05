---
title: "Öğretici: Azure Active Directory Tümleştirme ile Concur | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Concur arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eee0a5d-24fa-4986-9aef-3c543cfe3296
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 0b44437b3dcf69dae3587529da7d12e7809b9f55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-concur"></a><span data-ttu-id="58f72-103">Öğretici: Concur Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="58f72-103">Tutorial: Azure Active Directory integration with Concur</span></span>

<span data-ttu-id="58f72-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Concur tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="58f72-104">In this tutorial, you learn how to integrate Concur with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="58f72-105">Concur Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="58f72-105">Integrating Concur with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="58f72-106">Concur erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="58f72-106">You can control in Azure AD who has access to Concur</span></span>
- <span data-ttu-id="58f72-107">Otomatik olarak için Concur (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="58f72-107">You can enable your users to automatically get signed-on to Concur (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="58f72-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="58f72-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="58f72-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla bilgi bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="58f72-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58f72-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="58f72-110">Prerequisites</span></span>

<span data-ttu-id="58f72-111">Azure AD tümleştirme Concur ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="58f72-111">To configure Azure AD integration with Concur, you need the following items:</span></span>

- <span data-ttu-id="58f72-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="58f72-112">An Azure AD subscription</span></span>
- <span data-ttu-id="58f72-113">Bir Concur çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="58f72-113">A Concur single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="58f72-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="58f72-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="58f72-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="58f72-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="58f72-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="58f72-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="58f72-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="58f72-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="58f72-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="58f72-118">Scenario description</span></span>
<span data-ttu-id="58f72-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="58f72-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="58f72-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="58f72-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="58f72-121">Galeriden Concur ekleme</span><span class="sxs-lookup"><span data-stu-id="58f72-121">Adding Concur from the gallery</span></span>
2. <span data-ttu-id="58f72-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="58f72-122">Configuring and testing Azure AD single sign-on</span></span>

>[!NOTE]
><span data-ttu-id="58f72-123">Başvurmanız gerekir ayrı bir görev yapılandırmadır Concur aboneliğinizin SAML aracılığıyla Federasyon SSO [Concur istemci destek ekibi](https://www.concur.co.in/contact) gerçekleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="58f72-123">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span></span> 

## <a name="adding-concur-from-the-gallery"></a><span data-ttu-id="58f72-124">Galeriden Concur ekleme</span><span class="sxs-lookup"><span data-stu-id="58f72-124">Adding Concur from the gallery</span></span>
<span data-ttu-id="58f72-125">Azure AD Concur tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Concur eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="58f72-125">To configure the integration of Concur into Azure AD, you need to add Concur from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="58f72-126">**Galeriden Concur eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="58f72-126">**To add Concur from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="58f72-127">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="58f72-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="58f72-129">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="58f72-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="58f72-130">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="58f72-130">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="58f72-132">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="58f72-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="58f72-134">Arama kutusuna **Concur**.</span><span class="sxs-lookup"><span data-stu-id="58f72-134">In the search box, type **Concur**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-concur-tutorial/tutorial_concur_search.png)

5. <span data-ttu-id="58f72-136">Sonuçlar panelinde seçin **Concur**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="58f72-136">In the results panel, select **Concur**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-concur-tutorial/tutorial_concur_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="58f72-138">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="58f72-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="58f72-139">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Concur ile test etme</span><span class="sxs-lookup"><span data-stu-id="58f72-139">In this section, you configure and test Azure AD single sign-on with Concur based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="58f72-140">Tekli çalışmaya oturum için Azure AD Concur karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="58f72-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Concur is to a user in Azure AD.</span></span> <span data-ttu-id="58f72-141">Diğer bir deyişle, bir Azure AD kullanıcısının Concur ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="58f72-141">In other words, a link relationship between an Azure AD user and the related user in Concur needs to be established.</span></span>

<span data-ttu-id="58f72-142">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Concur içinde.</span><span class="sxs-lookup"><span data-stu-id="58f72-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Concur.</span></span>

<span data-ttu-id="58f72-143">Yapılandırma ve Azure AD çoklu oturum açma Concur ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="58f72-143">To configure and test Azure AD single sign-on with Concur, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="58f72-144">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="58f72-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="58f72-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="58f72-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="58f72-146">**[Concur test kullanıcısı oluşturma](#creating-a-concur-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Concur sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="58f72-146">**[Creating a Concur test user](#creating-a-concur-test-user)** - to have a counterpart of Britta Simon in Concur that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="58f72-147">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="58f72-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="58f72-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="58f72-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="58f72-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="58f72-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="58f72-150">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Concur uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="58f72-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Concur application.</span></span>

<span data-ttu-id="58f72-151">**Azure AD çoklu oturum açma ile Concur yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="58f72-151">**To configure Azure AD single sign-on with Concur, perform the following steps:**</span></span>

1. <span data-ttu-id="58f72-152">Azure portalında üzerinde **Concur** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="58f72-152">In the Azure portal, on the **Concur** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="58f72-154">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="58f72-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-concur-tutorial/tutorial_concur_samlbase.png)

3. <span data-ttu-id="58f72-156">Üzerinde **Concur etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="58f72-156">On the **Concur Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-concur-tutorial/tutorial_concur_url.png)

    <span data-ttu-id="58f72-158">a.</span><span class="sxs-lookup"><span data-stu-id="58f72-158">a.</span></span> <span data-ttu-id="58f72-159">İçinde **URL üzerinde oturum** metin kutusuna, şu biçimi kullanarak değeri yazın:`https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span><span class="sxs-lookup"><span data-stu-id="58f72-159">In the **Sign on URL** textbox, type the value using the following pattern: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span></span>

    <span data-ttu-id="58f72-160">b.</span><span class="sxs-lookup"><span data-stu-id="58f72-160">b.</span></span> <span data-ttu-id="58f72-161">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<customer-domain>.concursolutions.com`</span><span class="sxs-lookup"><span data-stu-id="58f72-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<customer-domain>.concursolutions.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="58f72-162">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="58f72-162">These values are not the real.</span></span> <span data-ttu-id="58f72-163">Bu değerler, URL ve tanımlayıcıdır gerçek oturum ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="58f72-163">Update these values with the actual Sign on URL and Identifier.</span></span> <span data-ttu-id="58f72-164">Kişi [Concur istemci destek ekibi](https://www.concur.co.in/contact) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="58f72-164">Contact [Concur Client support team](https://www.concur.co.in/contact) to get these values.</span></span> 

4. <span data-ttu-id="58f72-165">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="58f72-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-concur-tutorial/tutorial_concur_certificate.png) 

5. <span data-ttu-id="58f72-167">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="58f72-167">Click **Save** button.</span></span>

    <span data-ttu-id="58f72-168">![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="58f72-168">![Configure Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span></span>

6. <span data-ttu-id="58f72-169">Çoklu oturum açma yapılandırmak için **Concur** yan, indirilen göndermek için ihtiyacınız **meta veri XML** Concur desteği.</span><span class="sxs-lookup"><span data-stu-id="58f72-169">To configure single sign-on on **Concur** side, you need to send the downloaded **Metadata XML** to Concur support.</span></span> <span data-ttu-id="58f72-170">Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="58f72-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

  >[!NOTE]
  ><span data-ttu-id="58f72-171">Başvurmanız gerekir ayrı bir görev yapılandırmadır Concur aboneliğinizin SAML aracılığıyla Federasyon SSO [Concur istemci destek ekibi](https://www.concur.co.in/contact) gerçekleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="58f72-171">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span></span> 
  
<CE>

> [!TIP]
> <span data-ttu-id="58f72-172">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="58f72-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="58f72-173">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="58f72-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="58f72-174">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="58f72-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="58f72-175">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="58f72-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="58f72-176">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="58f72-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="58f72-178">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="58f72-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="58f72-179">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="58f72-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-concur-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="58f72-181">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="58f72-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-concur-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="58f72-183">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="58f72-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-concur-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="58f72-185">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="58f72-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-concur-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="58f72-187">a.</span><span class="sxs-lookup"><span data-stu-id="58f72-187">a.</span></span> <span data-ttu-id="58f72-188">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="58f72-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="58f72-189">b.</span><span class="sxs-lookup"><span data-stu-id="58f72-189">b.</span></span> <span data-ttu-id="58f72-190">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="58f72-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="58f72-191">c.</span><span class="sxs-lookup"><span data-stu-id="58f72-191">c.</span></span> <span data-ttu-id="58f72-192">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="58f72-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="58f72-193">d.</span><span class="sxs-lookup"><span data-stu-id="58f72-193">d.</span></span> <span data-ttu-id="58f72-194">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="58f72-194">Click **Create**.</span></span>
 
### <a name="creating-a-concur-test-user"></a><span data-ttu-id="58f72-195">Concur test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="58f72-195">Creating a Concur test user</span></span>

<span data-ttu-id="58f72-196">Uygulama, süresi kullanıcı sağlama ve kimlik doğrulama kullanıcılar uygulamada otomatik olarak oluşturulduktan sonra yalnızca destekler.</span><span class="sxs-lookup"><span data-stu-id="58f72-196">Application supports the Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="58f72-197">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="58f72-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="58f72-198">Bu bölümde, Britta Concur için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="58f72-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Concur.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="58f72-200">**Concur için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="58f72-200">**To assign Britta Simon to Concur, perform the following steps:**</span></span>

1. <span data-ttu-id="58f72-201">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="58f72-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="58f72-203">Uygulamalar listesinde **Concur**.</span><span class="sxs-lookup"><span data-stu-id="58f72-203">In the applications list, select **Concur**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-concur-tutorial/tutorial_concur_app.png) 

3. <span data-ttu-id="58f72-205">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="58f72-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="58f72-207">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="58f72-207">Click **Add** button.</span></span> <span data-ttu-id="58f72-208">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="58f72-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="58f72-210">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="58f72-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="58f72-211">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="58f72-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="58f72-212">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="58f72-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="58f72-213">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="58f72-213">Testing single sign-on</span></span>

<span data-ttu-id="58f72-214">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="58f72-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="58f72-215">Erişim paneli Concur parçasında tıkladığınızda, oturum açma sayfasına Concur uygulamasının almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="58f72-215">When you click the Concur tile in the Access Panel, you should get login page of Concur application.</span></span>
<span data-ttu-id="58f72-216">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="58f72-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="58f72-217">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="58f72-217">Additional resources</span></span>

* [<span data-ttu-id="58f72-218">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="58f72-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="58f72-219">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="58f72-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="58f72-220">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="58f72-220">Configure User Provisioning</span></span>](active-directory-saas-concur-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-concur-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-concur-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-concur-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-concur-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-concur-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-concur-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-concur-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-concur-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-concur-tutorial/tutorial_general_203.png

