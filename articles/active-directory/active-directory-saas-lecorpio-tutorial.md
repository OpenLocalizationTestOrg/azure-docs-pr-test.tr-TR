---
title: "Öğretici: Azure Active Directory Tümleştirme ile Lecorpio | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Lecorpio arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 35c94e2d9d8a938971f85ea732a74a7e1655545e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lecorpio"></a><span data-ttu-id="d6e14-103">Öğretici: Azure Active Directory Tümleştirme Lecorpio ile</span><span class="sxs-lookup"><span data-stu-id="d6e14-103">Tutorial: Azure Active Directory integration with Lecorpio</span></span>

<span data-ttu-id="d6e14-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Lecorpio tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d6e14-104">In this tutorial, you learn how to integrate Lecorpio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d6e14-105">Lecorpio Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="d6e14-105">Integrating Lecorpio with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d6e14-106">Lecorpio erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d6e14-106">You can control in Azure AD who has access to Lecorpio</span></span>
- <span data-ttu-id="d6e14-107">Otomatik olarak için Lecorpio (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d6e14-107">You can enable your users to automatically get signed-on to Lecorpio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d6e14-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="d6e14-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d6e14-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d6e14-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6e14-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d6e14-110">Prerequisites</span></span>

<span data-ttu-id="d6e14-111">Azure AD tümleştirme Lecorpio ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="d6e14-111">To configure Azure AD integration with Lecorpio, you need the following items:</span></span>

- <span data-ttu-id="d6e14-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="d6e14-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d6e14-113">Bir Lecorpio çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="d6e14-113">A Lecorpio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d6e14-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="d6e14-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d6e14-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d6e14-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d6e14-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="d6e14-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d6e14-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d6e14-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d6e14-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="d6e14-118">Scenario description</span></span>
<span data-ttu-id="d6e14-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="d6e14-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d6e14-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="d6e14-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d6e14-121">Galeriden Lecorpio ekleme</span><span class="sxs-lookup"><span data-stu-id="d6e14-121">Adding Lecorpio from the gallery</span></span>
2. <span data-ttu-id="d6e14-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d6e14-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lecorpio-from-the-gallery"></a><span data-ttu-id="d6e14-123">Galeriden Lecorpio ekleme</span><span class="sxs-lookup"><span data-stu-id="d6e14-123">Adding Lecorpio from the gallery</span></span>
<span data-ttu-id="d6e14-124">Azure AD Lecorpio tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Lecorpio eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6e14-124">To configure the integration of Lecorpio into Azure AD, you need to add Lecorpio from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d6e14-125">**Galeriden Lecorpio eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d6e14-125">**To add Lecorpio from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d6e14-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d6e14-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d6e14-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="d6e14-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d6e14-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d6e14-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="d6e14-131">Tıklatın **yeni uygulama** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d6e14-131">Click **New application** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="d6e14-133">Arama kutusuna **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="d6e14-133">In the search box, type **Lecorpio**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_search.png)

5. <span data-ttu-id="d6e14-135">Sonuçlar panelinde seçin **Lecorpio**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d6e14-135">In the results panel, select **Lecorpio**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d6e14-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d6e14-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d6e14-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Lecorpio ile test etme</span><span class="sxs-lookup"><span data-stu-id="d6e14-138">In this section, you configure and test Azure AD single sign-on with Lecorpio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d6e14-139">Tekli çalışmaya oturum için Azure AD Lecorpio karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="d6e14-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lecorpio is to a user in Azure AD.</span></span> <span data-ttu-id="d6e14-140">Diğer bir deyişle, bir Azure AD kullanıcısının Lecorpio ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6e14-140">In other words, a link relationship between an Azure AD user and the related user in Lecorpio needs to be established.</span></span>

<span data-ttu-id="d6e14-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Lecorpio içinde.</span><span class="sxs-lookup"><span data-stu-id="d6e14-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lecorpio.</span></span>

<span data-ttu-id="d6e14-142">Yapılandırma ve Azure AD çoklu oturum açma Lecorpio ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d6e14-142">To configure and test Azure AD single sign-on with Lecorpio, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d6e14-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d6e14-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d6e14-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="d6e14-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d6e14-145">**[Lecorpio test kullanıcısı oluşturma](#creating-a-lecorpio-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Lecorpio sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="d6e14-145">**[Creating a Lecorpio test user](#creating-a-lecorpio-test-user)** - to have a counterpart of Britta Simon in Lecorpio that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d6e14-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d6e14-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d6e14-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d6e14-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d6e14-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d6e14-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d6e14-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Lecorpio uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d6e14-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lecorpio application.</span></span>

<span data-ttu-id="d6e14-150">**Azure AD çoklu oturum açma ile Lecorpio yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d6e14-150">**To configure Azure AD single sign-on with Lecorpio, perform the following steps:**</span></span>

1. <span data-ttu-id="d6e14-151">Azure portalında üzerinde **Lecorpio** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="d6e14-151">In the Azure portal, on the **Lecorpio** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="d6e14-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d6e14-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_samlbase.png)

3. <span data-ttu-id="d6e14-155">Üzerinde **Lecorpio etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d6e14-155">On the **Lecorpio Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_url.png)

    <span data-ttu-id="d6e14-157">a.</span><span class="sxs-lookup"><span data-stu-id="d6e14-157">a.</span></span> <span data-ttu-id="d6e14-158">İçinde **oturum açma URL'si** metin kutusuna, şu biçimi kullanarak değeri yazın:`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="d6e14-158">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    <span data-ttu-id="d6e14-159">b.</span><span class="sxs-lookup"><span data-stu-id="d6e14-159">b.</span></span> <span data-ttu-id="d6e14-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="d6e14-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d6e14-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="d6e14-161">These values are not the real.</span></span> <span data-ttu-id="d6e14-162">Bu değerleri tanımlayıcısı ve gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d6e14-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="d6e14-163">Burada dizesinin benzersiz değeri tanımlayıcıda kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="d6e14-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="d6e14-164">Kişi [Lecorpio istemci destek ekibi](mailto:info@lecorpio.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="d6e14-164">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) to get these values.</span></span> 
 
4. <span data-ttu-id="d6e14-165">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d6e14-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_certificate.png) 

5. <span data-ttu-id="d6e14-167">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d6e14-167">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lecorpio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d6e14-169">Çoklu oturum açma yapılandırmak için **Lecorpio** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [Lecorpio destek ekibi](mailto:info@lecorpio.com).</span><span class="sxs-lookup"><span data-stu-id="d6e14-169">To configure single sign-on on **Lecorpio** side, you need to send the downloaded **Metadata XML** to [Lecorpio support team](mailto:info@lecorpio.com).</span></span>

> [!TIP]
> <span data-ttu-id="d6e14-170">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="d6e14-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d6e14-171">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="d6e14-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d6e14-172">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d6e14-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d6e14-173">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d6e14-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="d6e14-174">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="d6e14-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="d6e14-176">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d6e14-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d6e14-177">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d6e14-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d6e14-179">Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="d6e14-179">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d6e14-181">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d6e14-181">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d6e14-183">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d6e14-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d6e14-185">a.</span><span class="sxs-lookup"><span data-stu-id="d6e14-185">a.</span></span> <span data-ttu-id="d6e14-186">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d6e14-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d6e14-187">b.</span><span class="sxs-lookup"><span data-stu-id="d6e14-187">b.</span></span> <span data-ttu-id="d6e14-188">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="d6e14-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d6e14-189">c.</span><span class="sxs-lookup"><span data-stu-id="d6e14-189">c.</span></span> <span data-ttu-id="d6e14-190">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="d6e14-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d6e14-191">d.</span><span class="sxs-lookup"><span data-stu-id="d6e14-191">d.</span></span> <span data-ttu-id="d6e14-192">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d6e14-192">Click **Create**.</span></span>
 
### <a name="creating-a-lecorpio-test-user"></a><span data-ttu-id="d6e14-193">Lecorpio test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d6e14-193">Creating a Lecorpio test user</span></span>

<span data-ttu-id="d6e14-194">Bu bölümde, Lecorpio içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d6e14-194">In this section, you create a user called Britta Simon in Lecorpio.</span></span> 

<span data-ttu-id="d6e14-195">Kişi [Lecorpio istemci destek ekibi](mailto:info@lecorpio.com) Lecorpio uygulamada kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="d6e14-195">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) to add the users in the Lecorpio application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d6e14-196">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="d6e14-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d6e14-197">Bu bölümde, Britta Lecorpio için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d6e14-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lecorpio.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="d6e14-199">**Lecorpio için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d6e14-199">**To assign Britta Simon to Lecorpio, perform the following steps:**</span></span>

1. <span data-ttu-id="d6e14-200">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d6e14-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="d6e14-202">Uygulamalar listesinde **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="d6e14-202">In the applications list, select **Lecorpio**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_app.png) 

3. <span data-ttu-id="d6e14-204">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d6e14-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="d6e14-206">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d6e14-206">Click **Add** button.</span></span> <span data-ttu-id="d6e14-207">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d6e14-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="d6e14-209">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="d6e14-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d6e14-210">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d6e14-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d6e14-211">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d6e14-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d6e14-212">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="d6e14-212">Testing single sign-on</span></span>

<span data-ttu-id="d6e14-213">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="d6e14-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d6e14-214">Erişim paneli Lecorpio parçasında tıklattığınızda, otomatik olarak Lecorpio uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="d6e14-214">When you click the Lecorpio tile in the Access Panel, you should get automatically signed-on to your Lecorpio application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d6e14-215">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d6e14-215">Additional resources</span></span>

* [<span data-ttu-id="d6e14-216">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="d6e14-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d6e14-217">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="d6e14-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_203.png

