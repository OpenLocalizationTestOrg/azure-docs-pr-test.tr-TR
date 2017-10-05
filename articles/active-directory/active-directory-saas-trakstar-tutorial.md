---
title: "Öğretici: Azure Active Directory Tümleştirme ile Trakstar | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Trakstar arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411cb8c3-95c6-4138-acf2-ffc7f663e89a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 757429aa187e6536489b6636a0a11d122c7f9378
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trakstar"></a><span data-ttu-id="82734-103">Öğretici: Azure Active Directory Tümleştirme Trakstar ile</span><span class="sxs-lookup"><span data-stu-id="82734-103">Tutorial: Azure Active Directory integration with Trakstar</span></span>

<span data-ttu-id="82734-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Trakstar tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="82734-104">In this tutorial, you learn how to integrate Trakstar with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="82734-105">Trakstar Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="82734-105">Integrating Trakstar with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="82734-106">Trakstar erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="82734-106">You can control in Azure AD who has access to Trakstar</span></span>
- <span data-ttu-id="82734-107">Otomatik olarak için Trakstar (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="82734-107">You can enable your users to automatically get signed-on to Trakstar (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="82734-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="82734-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="82734-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="82734-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82734-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="82734-110">Prerequisites</span></span>

<span data-ttu-id="82734-111">Azure AD tümleştirme Trakstar ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="82734-111">To configure Azure AD integration with Trakstar, you need the following items:</span></span>

- <span data-ttu-id="82734-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="82734-112">An Azure AD subscription</span></span>
- <span data-ttu-id="82734-113">Bir Trakstar çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="82734-113">A Trakstar single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="82734-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="82734-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="82734-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="82734-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="82734-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="82734-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="82734-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="82734-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="82734-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="82734-118">Scenario description</span></span>
<span data-ttu-id="82734-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="82734-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="82734-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="82734-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="82734-121">Galeriden Trakstar ekleme</span><span class="sxs-lookup"><span data-stu-id="82734-121">Adding Trakstar from the gallery</span></span>
2. <span data-ttu-id="82734-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="82734-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trakstar-from-the-gallery"></a><span data-ttu-id="82734-123">Galeriden Trakstar ekleme</span><span class="sxs-lookup"><span data-stu-id="82734-123">Adding Trakstar from the gallery</span></span>
<span data-ttu-id="82734-124">Azure AD Trakstar tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Trakstar eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="82734-124">To configure the integration of Trakstar into Azure AD, you need to add Trakstar from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="82734-125">**Galeriden Trakstar eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="82734-125">**To add Trakstar from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="82734-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="82734-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="82734-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="82734-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="82734-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="82734-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="82734-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="82734-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="82734-133">Arama kutusuna **Trakstar**.</span><span class="sxs-lookup"><span data-stu-id="82734-133">In the search box, type **Trakstar**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_search.png)

5. <span data-ttu-id="82734-135">Sonuçlar panelinde seçin **Trakstar**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="82734-135">In the results panel, select **Trakstar**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="82734-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="82734-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="82734-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Trakstar ile test etme</span><span class="sxs-lookup"><span data-stu-id="82734-138">In this section, you configure and test Azure AD single sign-on with Trakstar based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="82734-139">Tekli çalışmaya oturum için Azure AD Trakstar karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="82734-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Trakstar is to a user in Azure AD.</span></span> <span data-ttu-id="82734-140">Diğer bir deyişle, bir Azure AD kullanıcısının Trakstar ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="82734-140">In other words, a link relationship between an Azure AD user and the related user in Trakstar needs to be established.</span></span>

<span data-ttu-id="82734-141">Trakstar içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="82734-141">In Trakstar, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="82734-142">Yapılandırma ve Azure AD çoklu oturum açma Trakstar ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="82734-142">To configure and test Azure AD single sign-on with Trakstar, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="82734-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="82734-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="82734-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="82734-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="82734-145">**[Trakstar test kullanıcısı oluşturma](#creating-a-trakstar-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Trakstar sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="82734-145">**[Creating a Trakstar test user](#creating-a-trakstar-test-user)** - to have a counterpart of Britta Simon in Trakstar that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="82734-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="82734-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="82734-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="82734-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="82734-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="82734-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="82734-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Trakstar uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="82734-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trakstar application.</span></span>

<span data-ttu-id="82734-150">**Azure AD çoklu oturum açma ile Trakstar yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="82734-150">**To configure Azure AD single sign-on with Trakstar, perform the following steps:**</span></span>

1. <span data-ttu-id="82734-151">Azure portalında üzerinde **Trakstar** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="82734-151">In the Azure portal, on the **Trakstar** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="82734-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="82734-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_samlbase.png)

3. <span data-ttu-id="82734-155">Üzerinde **Trakstar etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="82734-155">On the **Trakstar Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_url.png)

    <span data-ttu-id="82734-157">a.</span><span class="sxs-lookup"><span data-stu-id="82734-157">a.</span></span> <span data-ttu-id="82734-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://app.trakstar.com/auth/saml/callback?namespace=<NAMESPACE>`</span><span class="sxs-lookup"><span data-stu-id="82734-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.trakstar.com/auth/saml/callback?namespace=<NAMESPACE>`</span></span>

    <span data-ttu-id="82734-159">b.</span><span class="sxs-lookup"><span data-stu-id="82734-159">b.</span></span> <span data-ttu-id="82734-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.trakstar.com`</span><span class="sxs-lookup"><span data-stu-id="82734-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.trakstar.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="82734-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="82734-161">These values are not real.</span></span> <span data-ttu-id="82734-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="82734-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="82734-163">Kişi [Trakstar istemci destek ekibi](mailto:integrations@trakstar.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="82734-163">Contact [Trakstar Client support team](mailto:integrations@trakstar.com) to get these values.</span></span> 
 
4. <span data-ttu-id="82734-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="82734-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_certificate.png) 

5. <span data-ttu-id="82734-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="82734-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trakstar-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="82734-168">Üzerinde **Trakstar yapılandırma** 'yi tıklatın **yapılandırma Trakstar** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="82734-168">On the **Trakstar Configuration** section, click **Configure Trakstar** to open **Configure sign-on** window.</span></span> <span data-ttu-id="82734-169">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="82734-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_configure.png) 

7. <span data-ttu-id="82734-171">Çoklu oturum açma yapılandırmak için **Trakstar** yan, indirilen göndermek için ihtiyacınız **sertifika (Base64)**, **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si**için [Trakstar destek ekibi](mailto:integrations@trakstar.com).</span><span class="sxs-lookup"><span data-stu-id="82734-171">To configure single sign-on on **Trakstar** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Trakstar support team](mailto:integrations@trakstar.com).</span></span> 

> [!TIP]
> <span data-ttu-id="82734-172">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="82734-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="82734-173">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="82734-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="82734-174">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="82734-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="82734-175">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="82734-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="82734-176">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="82734-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="82734-178">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="82734-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="82734-179">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="82734-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-trakstar-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="82734-181">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="82734-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-trakstar-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="82734-183">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="82734-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-trakstar-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="82734-185">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="82734-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-trakstar-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="82734-187">a.</span><span class="sxs-lookup"><span data-stu-id="82734-187">a.</span></span> <span data-ttu-id="82734-188">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="82734-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="82734-189">b.</span><span class="sxs-lookup"><span data-stu-id="82734-189">b.</span></span> <span data-ttu-id="82734-190">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="82734-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="82734-191">c.</span><span class="sxs-lookup"><span data-stu-id="82734-191">c.</span></span> <span data-ttu-id="82734-192">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="82734-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="82734-193">d.</span><span class="sxs-lookup"><span data-stu-id="82734-193">d.</span></span> <span data-ttu-id="82734-194">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="82734-194">Click **Create**.</span></span>
 
### <a name="creating-a-trakstar-test-user"></a><span data-ttu-id="82734-195">Trakstar test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="82734-195">Creating a Trakstar test user</span></span>

<span data-ttu-id="82734-196">Bu bölümün amacı Britta Simon içinde Trakstar adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="82734-196">The objective of this section is to create a user called Britta Simon in Trakstar.</span></span> <span data-ttu-id="82734-197">Çalışmak [Trakstar destek ekibi](mailto:integrations@trakstar.com) Trakstar hesap kullanıcılar eklemek için.</span><span class="sxs-lookup"><span data-stu-id="82734-197">Work with [Trakstar support team](mailto:integrations@trakstar.com) to add the users in the Trakstar account.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="82734-198">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="82734-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="82734-199">Bu bölümde, Britta Trakstar için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="82734-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trakstar.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="82734-201">**Trakstar için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="82734-201">**To assign Britta Simon to Trakstar, perform the following steps:**</span></span>

1. <span data-ttu-id="82734-202">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="82734-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="82734-204">Uygulamalar listesinde **Trakstar**.</span><span class="sxs-lookup"><span data-stu-id="82734-204">In the applications list, select **Trakstar**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_app.png) 

3. <span data-ttu-id="82734-206">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="82734-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="82734-208">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="82734-208">Click **Add** button.</span></span> <span data-ttu-id="82734-209">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="82734-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="82734-211">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="82734-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="82734-212">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="82734-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="82734-213">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="82734-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="82734-214">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="82734-214">Testing single sign-on</span></span>

<span data-ttu-id="82734-215">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="82734-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="82734-216">Erişim paneli Trakstar parçasında tıklattığınızda, otomatik olarak Trakstar uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="82734-216">When you click the Trakstar tile in the Access Panel, you should get automatically signed-on to your Trakstar application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="82734-217">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="82734-217">Additional resources</span></span>

* [<span data-ttu-id="82734-218">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="82734-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="82734-219">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="82734-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_203.png

