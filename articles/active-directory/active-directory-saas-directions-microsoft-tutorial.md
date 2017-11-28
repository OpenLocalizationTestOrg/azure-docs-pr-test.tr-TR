---
title: "Öğretici: Azure Active Directory Tümleştirme yönergeleri Microsoft ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve yönergeleri arasında Microsoft yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e0c8986f-2acd-418d-a306-437abc44b640
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f9c068c71eb00a4c779c91c8ee0f0dc9d6ba85ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-directions-on-microsoft"></a><span data-ttu-id="642f8-103">Öğretici: Azure Active Directory Tümleştirme ile Microsoft yönergeleri</span><span class="sxs-lookup"><span data-stu-id="642f8-103">Tutorial: Azure Active Directory integration with Directions on Microsoft</span></span>

<span data-ttu-id="642f8-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Microsoft yönergeler tümleştirileceği nasıl öğrenin.</span><span class="sxs-lookup"><span data-stu-id="642f8-104">In this tutorial, you learn how to integrate Directions on Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="642f8-105">Yönergeleri Microsoft Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="642f8-105">Integrating Directions on Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="642f8-106">Microsoft yönergeleri erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="642f8-106">You can control in Azure AD who has access to Directions on Microsoft</span></span>
- <span data-ttu-id="642f8-107">Otomatik olarak Microsoft (çoklu oturum açma) yönergeleri için Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="642f8-107">You can enable your users to automatically get signed-on to Directions on Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="642f8-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="642f8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="642f8-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="642f8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="642f8-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="642f8-110">Prerequisites</span></span>

<span data-ttu-id="642f8-111">Azure AD tümleştirme yönergeleri Microsoft ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="642f8-111">To configure Azure AD integration with Directions on Microsoft, you need the following items:</span></span>

- <span data-ttu-id="642f8-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="642f8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="642f8-113">Abonelik yönergeleri Microsoft Çoklu oturum açma üzerinde etkin</span><span class="sxs-lookup"><span data-stu-id="642f8-113">A Directions on Microsoft single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="642f8-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="642f8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="642f8-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="642f8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="642f8-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="642f8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="642f8-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="642f8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="642f8-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="642f8-118">Scenario description</span></span>
<span data-ttu-id="642f8-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="642f8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="642f8-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="642f8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="642f8-121">Galerisi'nden Microsoft ekleme yönergeleri</span><span class="sxs-lookup"><span data-stu-id="642f8-121">Adding Directions on Microsoft from the gallery</span></span>
2. <span data-ttu-id="642f8-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="642f8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-directions-on-microsoft-from-the-gallery"></a><span data-ttu-id="642f8-123">Galerisi'nden Microsoft ekleme yönergeleri</span><span class="sxs-lookup"><span data-stu-id="642f8-123">Adding Directions on Microsoft from the gallery</span></span>
<span data-ttu-id="642f8-124">Yönergeleri tümleştirme Microsoft Azure AD ile yapılandırmak için yönergeleri Microsoft Galeriden yönetilen SaaS uygulamaları listenize eklemek gerekir.</span><span class="sxs-lookup"><span data-stu-id="642f8-124">To configure the integration of Directions on Microsoft into Azure AD, you need to add Directions on Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="642f8-125">**Yönergeleri Microsoft Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="642f8-125">**To add Directions on Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="642f8-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="642f8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="642f8-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="642f8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="642f8-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="642f8-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="642f8-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="642f8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="642f8-133">Arama kutusuna **yönergeleri Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="642f8-133">In the search box, type **Directions on Microsoft**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_search.png)

5. <span data-ttu-id="642f8-135">Sonuçlar panelinde seçin **yönergeleri Microsoft**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="642f8-135">In the results panel, select **Directions on Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="642f8-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="642f8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="642f8-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcıyı temel alarak Microsoft yönergeleri ile test etme</span><span class="sxs-lookup"><span data-stu-id="642f8-138">In this section, you configure and test Azure AD single sign-on with Directions on Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="642f8-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen Microsoft yönde bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="642f8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Directions on Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="642f8-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı Microsoft yönde arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="642f8-140">In other words, a link relationship between an Azure AD user and the related user in Directions on Microsoft needs to be established.</span></span>

<span data-ttu-id="642f8-141">Microsoft yönde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="642f8-141">In Directions on Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="642f8-142">Yapılandırma ve Azure AD çoklu oturum açma yönergeleri Microsoft ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="642f8-142">To configure and test Azure AD single sign-on with Directions on Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="642f8-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="642f8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="642f8-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="642f8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="642f8-145">**[Bir yönde Microsoft test kullanıcısı oluşturma](#creating-a-directions-on-microsoft-test-user)**  - kullanıcı Azure AD gösterimini bağlantılı Microsoft yönde Britta Simon, karşılık gelen sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="642f8-145">**[Creating a Directions on Microsoft test user](#creating-a-directions-on-microsoft-test-user)** - to have a counterpart of Britta Simon in Directions on Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="642f8-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="642f8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="642f8-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="642f8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="642f8-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="642f8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="642f8-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve Microsoft uygulaması'nda, yönde çoklu oturum açmayı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="642f8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Directions on Microsoft application.</span></span>

<span data-ttu-id="642f8-150">**Azure AD çoklu oturum açma yönergeleri Microsoft yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="642f8-150">**To configure Azure AD single sign-on with Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="642f8-151">Azure portalında üzerinde **yönergeleri Microsoft** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="642f8-151">In the Azure portal, on the **Directions on Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="642f8-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="642f8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_samlbase.png)

3. <span data-ttu-id="642f8-155">Üzerinde **Microsoft Domain ve URL'ler hakkında yönergeleri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="642f8-155">On the **Directions on Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_url.png)

    <span data-ttu-id="642f8-157">a.</span><span class="sxs-lookup"><span data-stu-id="642f8-157">a.</span></span> <span data-ttu-id="642f8-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="642f8-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://www.directionsonmicrosoft.com/user/login` |
    | `https://<subdomain>.devcloud.acquia-sites.com/<companyname>` |

    <span data-ttu-id="642f8-159">b.</span><span class="sxs-lookup"><span data-stu-id="642f8-159">b.</span></span> <span data-ttu-id="642f8-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="642f8-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://rhelmdirectionsonmicrosoftcomtest.devcloud.acquia-sites.com/simplesaml/<companyname>` |
    | `https://www.directionsonmicrosoft.com/simplesaml/<companyname>` |

    > [!NOTE] 
    > <span data-ttu-id="642f8-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="642f8-161">These values are not real.</span></span> <span data-ttu-id="642f8-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="642f8-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="642f8-163">Kişi [Microsoft Client yönünden destek ekibi](mailto:service@DirectionsOnMicrosoft.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="642f8-163">Contact [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com) to get these values.</span></span> 
 
4. <span data-ttu-id="642f8-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="642f8-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_certificate.png) 

5. <span data-ttu-id="642f8-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="642f8-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="642f8-168">Çoklu oturum açma yapılandırmak için **yönergeleri Microsoft** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [yönergeleri Microsoft destek ekibi](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="642f8-168">To configure single sign-on on **Directions on Microsoft** side, you need to send the downloaded **Metadata XML** to [Directions on Microsoft support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="642f8-169">Federasyon site üyeliğinize bulmak Microsoft destek ekibi yönünden etkinleştirmek için e-postanızdaki şirketinizin bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="642f8-169">To enable the Directions on Microsoft support team to locate your federated site membership, include your company information in your email.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="642f8-170">Microsoft yönergeleri için çoklu oturum açmayı gereken tarafından etkinleştirilmesi [Microsoft Client yönünden destek ekibi](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="642f8-170">Single sign-on for Directions on Microsoft needs to be enabled by the [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="642f8-171">Çoklu oturum açma etkin olduğunda bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="642f8-171">You will receive a notification when single sign-on has been enabled.</span></span>

> [!TIP]
> <span data-ttu-id="642f8-172">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="642f8-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="642f8-173">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="642f8-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="642f8-174">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="642f8-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="642f8-175">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="642f8-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="642f8-176">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="642f8-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="642f8-178">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="642f8-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="642f8-179">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="642f8-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="642f8-181">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="642f8-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="642f8-183">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="642f8-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="642f8-185">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="642f8-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="642f8-187">a.</span><span class="sxs-lookup"><span data-stu-id="642f8-187">a.</span></span> <span data-ttu-id="642f8-188">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="642f8-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="642f8-189">b.</span><span class="sxs-lookup"><span data-stu-id="642f8-189">b.</span></span> <span data-ttu-id="642f8-190">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="642f8-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="642f8-191">c.</span><span class="sxs-lookup"><span data-stu-id="642f8-191">c.</span></span> <span data-ttu-id="642f8-192">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="642f8-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="642f8-193">d.</span><span class="sxs-lookup"><span data-stu-id="642f8-193">d.</span></span> <span data-ttu-id="642f8-194">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="642f8-194">Click **Create**.</span></span>
 
### <a name="creating-a-directions-on-microsoft-test-user"></a><span data-ttu-id="642f8-195">Bir yönde Microsoft test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="642f8-195">Creating a Directions on Microsoft test user</span></span>

<span data-ttu-id="642f8-196">Kullanıcı yönergeleri Microsoft hazırlama yapılandırmanız için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="642f8-196">There is no action item for you to configure user provisioning to Directions on Microsoft.</span></span>  

<span data-ttu-id="642f8-197">Atanmış bir kullanıcı erişim paneli kullanılarak Microsoft yönergeleri oturum denediğinde yönergeleri Microsoft denetler kullanıcının var olup olmadığını.</span><span class="sxs-lookup"><span data-stu-id="642f8-197">When an assigned user tries to log in to Directions on Microsoft using the access panel, Directions on Microsoft checks whether the user exists.</span></span> <span data-ttu-id="642f8-198">Hiçbir kullanıcı hesabı varsa kullanılabilir henüz, yönergeleri Microsoft tarafından otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="642f8-198">If there is no user account available yet, it is automatically created by Directions on Microsoft.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="642f8-199">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="642f8-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="642f8-200">Bu bölümde, Microsoft tarafından gönderilen yönergeleri için erişim vererek, Azure çoklu oturum açma kullanılacak Britta Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="642f8-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Directions on Microsoft.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="642f8-202">**Microsoft yönergeleri Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="642f8-202">**To assign Britta Simon to Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="642f8-203">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="642f8-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="642f8-205">Uygulamalar listesinde **yönergeleri Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="642f8-205">In the applications list, select **Directions on Microsoft**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_app.png) 

3. <span data-ttu-id="642f8-207">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="642f8-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="642f8-209">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="642f8-209">Click **Add** button.</span></span> <span data-ttu-id="642f8-210">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="642f8-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="642f8-212">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="642f8-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="642f8-213">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="642f8-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="642f8-214">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="642f8-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="642f8-215">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="642f8-215">Testing single sign-on</span></span>

<span data-ttu-id="642f8-216">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="642f8-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="642f8-217">Yönergeleri erişim Paneli'nde Microsoft kutucuğa tıkladığınızda, otomatik olarak Microsoft uygulaması'nda, yönergeleri için açan.</span><span class="sxs-lookup"><span data-stu-id="642f8-217">When you click the Directions on Microsoft tile in the Access Panel, you should get automatically signed-on to your Directions on Microsoft application.</span></span>

<span data-ttu-id="642f8-218">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="642f8-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="642f8-219">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="642f8-219">Additional resources</span></span>

* [<span data-ttu-id="642f8-220">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="642f8-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="642f8-221">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="642f8-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_203.png

