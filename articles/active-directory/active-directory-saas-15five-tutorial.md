---
title: "Öğretici: Azure Active Directory Tümleştirme ile 15Five | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile 15Five arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2fb301c2-7d7a-4046-8ee1-7dc9e7684806
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: ea36774747a0fcfa4ace1aefb2d46dba815d92c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-15five"></a><span data-ttu-id="90a0b-103">Öğretici: Azure Active Directory Tümleştirme 15Five ile</span><span class="sxs-lookup"><span data-stu-id="90a0b-103">Tutorial: Azure Active Directory integration with 15Five</span></span>

<span data-ttu-id="90a0b-104">Bu öğreticide, Azure Active Directory (Azure AD) ile 15Five tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="90a0b-104">In this tutorial, you learn how to integrate 15Five with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="90a0b-105">15Five Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="90a0b-105">Integrating 15Five with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="90a0b-106">15Five erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="90a0b-106">You can control in Azure AD who has access to 15Five</span></span>
- <span data-ttu-id="90a0b-107">Otomatik olarak 15Five için açan kullanıcılarınıza etkinleştirebilirsiniz (çoklu oturum açma) Azure AD hesaplarına sahip</span><span class="sxs-lookup"><span data-stu-id="90a0b-107">You can enable your users to automatically get signed-on to 15Five (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="90a0b-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="90a0b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="90a0b-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="90a0b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90a0b-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="90a0b-110">Prerequisites</span></span>

<span data-ttu-id="90a0b-111">Azure AD tümleştirme 15Five ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="90a0b-111">To configure Azure AD integration with 15Five, you need the following items:</span></span>

- <span data-ttu-id="90a0b-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="90a0b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="90a0b-113">Bir 15Five çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="90a0b-113">A 15Five single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="90a0b-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="90a0b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="90a0b-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="90a0b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="90a0b-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="90a0b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="90a0b-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="90a0b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="90a0b-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="90a0b-118">Scenario description</span></span>
<span data-ttu-id="90a0b-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="90a0b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="90a0b-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="90a0b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="90a0b-121">Galeriden 15Five ekleme</span><span class="sxs-lookup"><span data-stu-id="90a0b-121">Adding 15Five from the gallery</span></span>
2. <span data-ttu-id="90a0b-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="90a0b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-15five-from-the-gallery"></a><span data-ttu-id="90a0b-123">Galeriden 15Five ekleme</span><span class="sxs-lookup"><span data-stu-id="90a0b-123">Adding 15Five from the gallery</span></span>
<span data-ttu-id="90a0b-124">Azure AD 15Five tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden 15Five eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="90a0b-124">To configure the integration of 15Five into Azure AD, you need to add 15Five from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="90a0b-125">**Galeriden 15Five eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="90a0b-125">**To add 15Five from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="90a0b-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="90a0b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="90a0b-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="90a0b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="90a0b-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="90a0b-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="90a0b-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="90a0b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="90a0b-133">Arama kutusuna **15Five**.</span><span class="sxs-lookup"><span data-stu-id="90a0b-133">In the search box, type **15Five**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-15five-tutorial/tutorial_15five_search.png)

5. <span data-ttu-id="90a0b-135">Sonuçlar panelinde seçin **15Five**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="90a0b-135">In the results panel, select **15Five**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-15five-tutorial/tutorial_15five_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="90a0b-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="90a0b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="90a0b-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı 15Five ile test etme</span><span class="sxs-lookup"><span data-stu-id="90a0b-138">In this section, you configure and test Azure AD single sign-on with 15Five based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="90a0b-139">Tekli çalışmaya oturum için Azure AD 15Five karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="90a0b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 15Five is to a user in Azure AD.</span></span> <span data-ttu-id="90a0b-140">Diğer bir deyişle, bir Azure AD kullanıcısının 15Five ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="90a0b-140">In other words, a link relationship between an Azure AD user and the related user in 15Five needs to be established.</span></span>

<span data-ttu-id="90a0b-141">15Five içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="90a0b-141">In 15Five, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="90a0b-142">Yapılandırma ve Azure AD çoklu oturum açma 15Five ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="90a0b-142">To configure and test Azure AD single sign-on with 15Five, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="90a0b-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="90a0b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="90a0b-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="90a0b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="90a0b-145">**[15Five test kullanıcısı oluşturma](#creating-a-15five-test-user)**  - bir Britta Simon karşılık gelen kullanıcı Azure AD gösterimini bağlı 15Five içinde olması.</span><span class="sxs-lookup"><span data-stu-id="90a0b-145">**[Creating a 15Five test user](#creating-a-15five-test-user)** - to have a counterpart of Britta Simon in 15Five that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="90a0b-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="90a0b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="90a0b-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="90a0b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="90a0b-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="90a0b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="90a0b-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma 15Five uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="90a0b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 15Five application.</span></span>

<span data-ttu-id="90a0b-150">**Azure AD çoklu oturum açma ile 15Five yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="90a0b-150">**To configure Azure AD single sign-on with 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="90a0b-151">Azure portalında üzerinde **15Five** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="90a0b-151">In the Azure portal, on the **15Five** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="90a0b-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="90a0b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-15five-tutorial/tutorial_15five_samlbase.png)

3. <span data-ttu-id="90a0b-155">Üzerinde **15Five etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="90a0b-155">On the **15Five Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-15five-tutorial/tutorial_15five_url.png)

    <span data-ttu-id="90a0b-157">a.</span><span class="sxs-lookup"><span data-stu-id="90a0b-157">a.</span></span> <span data-ttu-id="90a0b-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.15five.com`</span><span class="sxs-lookup"><span data-stu-id="90a0b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.15five.com`</span></span>

    <span data-ttu-id="90a0b-159">b.</span><span class="sxs-lookup"><span data-stu-id="90a0b-159">b.</span></span> <span data-ttu-id="90a0b-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.15five.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="90a0b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.15five.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="90a0b-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="90a0b-161">These values are not real.</span></span> <span data-ttu-id="90a0b-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="90a0b-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="90a0b-163">Kişi [15Five istemci destek ekibi](https://www.15five.com/contact/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="90a0b-163">Contact [15Five Client support team](https://www.15five.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="90a0b-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="90a0b-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-15five-tutorial/tutorial_15five_certificate.png) 

5. <span data-ttu-id="90a0b-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="90a0b-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-15five-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="90a0b-168">Çoklu oturum açma yapılandırmak için **15Five** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [15Five destek ekibi](https://www.15five.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="90a0b-168">To configure single sign-on on **15Five** side, you need to send the downloaded **Metadata XML** to [15Five support team](https://www.15five.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="90a0b-169">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="90a0b-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="90a0b-170">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="90a0b-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="90a0b-171">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="90a0b-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="90a0b-172">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="90a0b-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="90a0b-173">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="90a0b-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="90a0b-175">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="90a0b-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="90a0b-176">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="90a0b-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-15five-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="90a0b-178">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="90a0b-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-15five-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="90a0b-180">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="90a0b-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-15five-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="90a0b-182">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="90a0b-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-15five-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="90a0b-184">a.</span><span class="sxs-lookup"><span data-stu-id="90a0b-184">a.</span></span> <span data-ttu-id="90a0b-185">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="90a0b-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="90a0b-186">b.</span><span class="sxs-lookup"><span data-stu-id="90a0b-186">b.</span></span> <span data-ttu-id="90a0b-187">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="90a0b-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="90a0b-188">c.</span><span class="sxs-lookup"><span data-stu-id="90a0b-188">c.</span></span> <span data-ttu-id="90a0b-189">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="90a0b-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="90a0b-190">d.</span><span class="sxs-lookup"><span data-stu-id="90a0b-190">d.</span></span> <span data-ttu-id="90a0b-191">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="90a0b-191">Click **Create**.</span></span>
 
### <a name="creating-a-15five-test-user"></a><span data-ttu-id="90a0b-192">15Five test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="90a0b-192">Creating a 15Five test user</span></span>

<span data-ttu-id="90a0b-193">Azure AD kullanıcıları için 15Five oturum açmak etkinleştirmek için bunların 15Five sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="90a0b-193">To enable Azure AD users to log in to 15Five, they must be provisioned into 15Five.</span></span> <span data-ttu-id="90a0b-194">15Five, sağlama olduğunda el ile bir görev.</span><span class="sxs-lookup"><span data-stu-id="90a0b-194">When 15Five, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="90a0b-195">Kullanıcı sağlamayı yapılandırmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="90a0b-195">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="90a0b-196">Oturum, **15Five** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="90a0b-196">Log in to your **15Five** company site as administrator.</span></span>

2. <span data-ttu-id="90a0b-197">Git **şirket yönetmek**.</span><span class="sxs-lookup"><span data-stu-id="90a0b-197">Go to **Manage Company**.</span></span>
   
    <span data-ttu-id="90a0b-198">![Şirket yönetmek](./media/active-directory-saas-15five-tutorial/IC784675.png "şirket yönetme")</span><span class="sxs-lookup"><span data-stu-id="90a0b-198">![Manage Company](./media/active-directory-saas-15five-tutorial/IC784675.png "Manage Company")</span></span>

3. <span data-ttu-id="90a0b-199">Git **kişiler \> kişileri ekleyin**.</span><span class="sxs-lookup"><span data-stu-id="90a0b-199">Go to **People \> Add People**.</span></span>
   
    <span data-ttu-id="90a0b-200">![Kişiler](./media/active-directory-saas-15five-tutorial/IC784676.png "kişiler")</span><span class="sxs-lookup"><span data-stu-id="90a0b-200">![People](./media/active-directory-saas-15five-tutorial/IC784676.png "People")</span></span>

4. <span data-ttu-id="90a0b-201">Yeni bir kişiye eklemek bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="90a0b-201">In the Add New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="90a0b-202">![Yeni bir kişiye eklemek](./media/active-directory-saas-15five-tutorial/IC784677.png "yeni bir kişiye ekleme")</span><span class="sxs-lookup"><span data-stu-id="90a0b-202">![Add New Person](./media/active-directory-saas-15five-tutorial/IC784677.png "Add New Person")</span></span>
   
    <span data-ttu-id="90a0b-203">a.</span><span class="sxs-lookup"><span data-stu-id="90a0b-203">a.</span></span> <span data-ttu-id="90a0b-204">Tür **ad**, **Soyadı**, **başlık**, **e-posta adresi** istediğiniz içine sağlamak için geçerli bir Azure Active Directory hesabı ilgili metin kutuları.</span><span class="sxs-lookup"><span data-stu-id="90a0b-204">Type the **First Name**, **Last Name**, **Title**, **Email address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="90a0b-205">b.</span><span class="sxs-lookup"><span data-stu-id="90a0b-205">b.</span></span> <span data-ttu-id="90a0b-206">**Bitti**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="90a0b-206">Click **Done**.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="90a0b-207">Azure AD hesap sahibi etkin duruma gelmesi hesabı onaylamak için bir bağlantı içeren bir e-posta alır.</span><span class="sxs-lookup"><span data-stu-id="90a0b-207">The Azure AD account holder receives an email including a link to confirm the account before it becomes active.</span></span>
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="90a0b-208">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="90a0b-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="90a0b-209">Bu bölümde, Britta 15Five erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="90a0b-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 15Five.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="90a0b-211">**15Five için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="90a0b-211">**To assign Britta Simon to 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="90a0b-212">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="90a0b-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="90a0b-214">Uygulamalar listesinde **15Five**.</span><span class="sxs-lookup"><span data-stu-id="90a0b-214">In the applications list, select **15Five**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-15five-tutorial/tutorial_15five_app.png) 

3. <span data-ttu-id="90a0b-216">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="90a0b-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="90a0b-218">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="90a0b-218">Click **Add** button.</span></span> <span data-ttu-id="90a0b-219">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="90a0b-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="90a0b-221">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="90a0b-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="90a0b-222">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="90a0b-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="90a0b-223">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="90a0b-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="90a0b-224">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="90a0b-224">Testing single sign-on</span></span>

<span data-ttu-id="90a0b-225">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="90a0b-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="90a0b-226">Erişim paneli 15Five parçasında tıkladığınızda, oturum açma sayfasına 15Five uygulamasının almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90a0b-226">When you click the 15Five tile in the Access Panel, you should get login page of 15Five application.</span></span>
<span data-ttu-id="90a0b-227">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="90a0b-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="90a0b-228">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="90a0b-228">Additional resources</span></span>

* [<span data-ttu-id="90a0b-229">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="90a0b-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="90a0b-230">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="90a0b-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-15five-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-15five-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-15five-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-15five-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-15five-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-15five-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-15five-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-15five-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-15five-tutorial/tutorial_general_203.png

