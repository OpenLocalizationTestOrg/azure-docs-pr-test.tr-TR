---
title: "Öğretici: Azure Active Directory Tümleştirme ile MobileXpense | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile MobileXpense arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e649fc4e-3e15-4948-b977-00bfe9f7db13
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: jeedes
ms.openlocfilehash: 030a1fc9f36d6fcfa607552d85ce232e36eaa64b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mobilexpense"></a><span data-ttu-id="157ae-103">Öğretici: Azure Active Directory Tümleştirme MobileXpense ile</span><span class="sxs-lookup"><span data-stu-id="157ae-103">Tutorial: Azure Active Directory integration with MobileXpense</span></span>

<span data-ttu-id="157ae-104">Bu öğreticide, Azure Active Directory (Azure AD) ile MobileXpense tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="157ae-104">In this tutorial, you learn how to integrate MobileXpense with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="157ae-105">MobileXpense Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="157ae-105">Integrating MobileXpense with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="157ae-106">MobileXpense erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="157ae-106">You can control in Azure AD who has access to MobileXpense</span></span>
- <span data-ttu-id="157ae-107">Otomatik olarak için MobileXpense (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="157ae-107">You can enable your users to automatically get signed-on to MobileXpense (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="157ae-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="157ae-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="157ae-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="157ae-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="157ae-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="157ae-110">Prerequisites</span></span>

<span data-ttu-id="157ae-111">Azure AD tümleştirme MobileXpense ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="157ae-111">To configure Azure AD integration with MobileXpense, you need the following items:</span></span>

- <span data-ttu-id="157ae-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="157ae-112">An Azure AD subscription</span></span>
- <span data-ttu-id="157ae-113">Bir MobileXpense çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="157ae-113">A MobileXpense single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="157ae-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="157ae-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="157ae-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="157ae-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="157ae-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="157ae-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="157ae-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="157ae-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="157ae-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="157ae-118">Scenario description</span></span>
<span data-ttu-id="157ae-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="157ae-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="157ae-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="157ae-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="157ae-121">Galeriden MobileXpense ekleme</span><span class="sxs-lookup"><span data-stu-id="157ae-121">Adding MobileXpense from the gallery</span></span>
2. <span data-ttu-id="157ae-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="157ae-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mobilexpense-from-the-gallery"></a><span data-ttu-id="157ae-123">Galeriden MobileXpense ekleme</span><span class="sxs-lookup"><span data-stu-id="157ae-123">Adding MobileXpense from the gallery</span></span>
<span data-ttu-id="157ae-124">Azure AD MobileXpense tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden MobileXpense eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="157ae-124">To configure the integration of MobileXpense into Azure AD, you need to add MobileXpense from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="157ae-125">**Galeriden MobileXpense eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="157ae-125">**To add MobileXpense from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="157ae-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="157ae-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="157ae-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="157ae-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="157ae-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="157ae-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="157ae-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="157ae-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="157ae-133">Arama kutusuna **MobileXpense**.</span><span class="sxs-lookup"><span data-stu-id="157ae-133">In the search box, type **MobileXpense**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_search.png)

5. <span data-ttu-id="157ae-135">Sonuçlar panelinde seçin **MobileXpense**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="157ae-135">In the results panel, select **MobileXpense**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="157ae-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="157ae-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="157ae-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı MobileXpense ile test etme</span><span class="sxs-lookup"><span data-stu-id="157ae-138">In this section, you configure and test Azure AD single sign-on with MobileXpense based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="157ae-139">Tekli çalışmaya oturum için Azure AD MobileXpense karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="157ae-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MobileXpense is to a user in Azure AD.</span></span> <span data-ttu-id="157ae-140">Diğer bir deyişle, bir Azure AD kullanıcısının MobileXpense ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="157ae-140">In other words, a link relationship between an Azure AD user and the related user in MobileXpense needs to be established.</span></span>

<span data-ttu-id="157ae-141">MobileXpense içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="157ae-141">In MobileXpense, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="157ae-142">Yapılandırma ve Azure AD çoklu oturum açma MobileXpense ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="157ae-142">To configure and test Azure AD single sign-on with MobileXpense, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="157ae-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="157ae-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="157ae-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="157ae-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="157ae-145">**[MobileXpense test kullanıcısı oluşturma](#creating-a-mobilexpense-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı MobileXpense sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="157ae-145">**[Creating a MobileXpense test user](#creating-a-mobilexpense-test-user)** - to have a counterpart of Britta Simon in MobileXpense that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="157ae-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="157ae-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="157ae-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="157ae-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="157ae-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="157ae-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="157ae-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma MobileXpense uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="157ae-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MobileXpense application.</span></span>

<span data-ttu-id="157ae-150">**Azure AD çoklu oturum açma ile MobileXpense yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="157ae-150">**To configure Azure AD single sign-on with MobileXpense, perform the following steps:**</span></span>

1. <span data-ttu-id="157ae-151">Azure portalında üzerinde **MobileXpense** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="157ae-151">In the Azure portal, on the **MobileXpense** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="157ae-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="157ae-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_samlbase.png)

3. <span data-ttu-id="157ae-155">Üzerinde **MobileXpense etki alanı ve URL'leri** uygulamada yapılandırmak istiyorsanız, bölüm **IDP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="157ae-155">On the **MobileXpense Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url11.png)

    <span data-ttu-id="157ae-157">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="157ae-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span></span>

4. <span data-ttu-id="157ae-158">Denetleme **Göster Gelişmiş URL ayarları**, uygulamada yapılandırmak istiyorsanız **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="157ae-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url22.png)

<span data-ttu-id="157ae-160">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın::`https://<sub domain>.mobilexpense.com/<customername>`</span><span class="sxs-lookup"><span data-stu-id="157ae-160">In the **Sign-on URL** textbox, type a URL using the following pattern:: `https://<sub domain>.mobilexpense.com/<customername>`</span></span>

> [!NOTE] 
> <span data-ttu-id="157ae-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="157ae-161">These values are not real.</span></span> <span data-ttu-id="157ae-162">Bu değerler gerçek yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="157ae-162">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="157ae-163">Kişi [MobileXpense istemci destek ekibi](http://www.mobilexpense.net/contact) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="157ae-163">Contact [MobileXpense Client support team](http://www.mobilexpense.net/contact) to get these values.</span></span> 

5. <span data-ttu-id="157ae-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="157ae-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_certificate.png) 

6. <span data-ttu-id="157ae-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="157ae-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="157ae-168">Çoklu oturum açma yapılandırmak için **MobileXpense** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [MobileXpense destek ekibi](http://www.mobilexpense.net/contact).</span><span class="sxs-lookup"><span data-stu-id="157ae-168">To configure single sign-on on **MobileXpense** side, you need to send the downloaded **Metadata XML** to [MobileXpense support team](http://www.mobilexpense.net/contact).</span></span>

> [!TIP]
> <span data-ttu-id="157ae-169">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="157ae-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="157ae-170">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="157ae-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="157ae-171">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="157ae-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="157ae-172">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="157ae-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="157ae-173">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="157ae-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="157ae-175">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="157ae-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="157ae-176">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="157ae-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="157ae-178">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="157ae-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="157ae-180">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="157ae-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="157ae-182">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="157ae-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="157ae-184">a.</span><span class="sxs-lookup"><span data-stu-id="157ae-184">a.</span></span> <span data-ttu-id="157ae-185">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="157ae-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="157ae-186">b.</span><span class="sxs-lookup"><span data-stu-id="157ae-186">b.</span></span> <span data-ttu-id="157ae-187">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="157ae-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="157ae-188">c.</span><span class="sxs-lookup"><span data-stu-id="157ae-188">c.</span></span> <span data-ttu-id="157ae-189">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="157ae-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="157ae-190">d.</span><span class="sxs-lookup"><span data-stu-id="157ae-190">d.</span></span> <span data-ttu-id="157ae-191">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="157ae-191">Click **Create**.</span></span>
 
### <a name="creating-a-mobilexpense-test-user"></a><span data-ttu-id="157ae-192">MobileXpense test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="157ae-192">Creating a MobileXpense test user</span></span>

<span data-ttu-id="157ae-193">Bu bölümde, MobileXpense içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="157ae-193">In this section, you create a user called Britta Simon in MobileXpense.</span></span> <span data-ttu-id="157ae-194">ile çalışma [MobileXpense destek ekibi](http://www.mobilexpense.net/contact) MobileXpense platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="157ae-194">work with [MobileXpense support team](http://www.mobilexpense.net/contact) to add the users in the MobileXpense platform.</span></span> <span data-ttu-id="157ae-195">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="157ae-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="157ae-196">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="157ae-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="157ae-197">Bu bölümde, Britta MobileXpense için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="157ae-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MobileXpense.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="157ae-199">**MobileXpense için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="157ae-199">**To assign Britta Simon to MobileXpense, perform the following steps:**</span></span>

1. <span data-ttu-id="157ae-200">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="157ae-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="157ae-202">Uygulamalar listesinde **MobileXpense**.</span><span class="sxs-lookup"><span data-stu-id="157ae-202">In the applications list, select **MobileXpense**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_app.png) 

3. <span data-ttu-id="157ae-204">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="157ae-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="157ae-206">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="157ae-206">Click **Add** button.</span></span> <span data-ttu-id="157ae-207">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="157ae-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="157ae-209">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="157ae-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="157ae-210">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="157ae-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="157ae-211">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="157ae-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="157ae-212">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="157ae-212">Testing single sign-on</span></span>

<span data-ttu-id="157ae-213">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="157ae-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="157ae-214">Erişim paneli MobileXpense parçasında tıklattığınızda, otomatik olarak MobileXpense uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="157ae-214">When you click the MobileXpense tile in the Access Panel, you should get automatically signed-on to your MobileXpense application.</span></span>
<span data-ttu-id="157ae-215">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="157ae-215">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="157ae-216">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="157ae-216">Additional resources</span></span>

* [<span data-ttu-id="157ae-217">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="157ae-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="157ae-218">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="157ae-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_203.png

