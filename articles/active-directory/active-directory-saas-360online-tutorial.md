---
title: "Öğretici: Azure Active Directory Tümleştirme ile 360 çevrimiçi | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile 360 çevrimiçi arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cda8eba6-843f-4a09-8c55-0aaf6e593d75
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 629c7db04b0f9c880da6dfa8eac7fe14ecd8a215
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-360-online"></a><span data-ttu-id="f1d9e-103">Öğretici: Azure Active Directory Tümleştirme ile 360 çevrimiçi</span><span class="sxs-lookup"><span data-stu-id="f1d9e-103">Tutorial: Azure Active Directory integration with 360 Online</span></span>

<span data-ttu-id="f1d9e-104">Bu öğreticide, Azure Active Directory (Azure AD) ile 360 çevrimiçi tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-104">In this tutorial, you learn how to integrate 360 Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1d9e-105">360 çevrimiçi Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="f1d9e-105">Integrating 360 Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f1d9e-106">360 çevrimiçi erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f1d9e-106">You can control in Azure AD who has access to 360 Online</span></span>
- <span data-ttu-id="f1d9e-107">Otomatik olarak Azure AD hesaplarına sahip 360 çevrimiçi (çoklu oturum açma) için açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f1d9e-107">You can enable your users to automatically get signed-on to 360 Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1d9e-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="f1d9e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f1d9e-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f1d9e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1d9e-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f1d9e-110">Prerequisites</span></span>

<span data-ttu-id="f1d9e-111">Azure AD Tümleştirmesi ile 360 çevrimiçi yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="f1d9e-111">To configure Azure AD integration with 360 Online, you need the following items:</span></span>

- <span data-ttu-id="f1d9e-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="f1d9e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1d9e-113">Abonelik bir 360 çevrimiçi çoklu oturum açma etkin</span><span class="sxs-lookup"><span data-stu-id="f1d9e-113">A 360 Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f1d9e-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1d9e-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f1d9e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1d9e-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f1d9e-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1d9e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1d9e-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="f1d9e-118">Scenario description</span></span>
<span data-ttu-id="f1d9e-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1d9e-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="f1d9e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1d9e-121">360 çevrimiçi galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="f1d9e-121">Adding 360 Online from the gallery</span></span>
2. <span data-ttu-id="f1d9e-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f1d9e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-360-online-from-the-gallery"></a><span data-ttu-id="f1d9e-123">360 çevrimiçi galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="f1d9e-123">Adding 360 Online from the gallery</span></span>
<span data-ttu-id="f1d9e-124">Azure AD 360 çevrimiçi tümleştirilmesi yapılandırmak için 360 çevrimiçi galeriden yönetilen SaaS uygulamaları listenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-124">To configure the integration of 360 Online into Azure AD, you need to add 360 Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f1d9e-125">**360 çevrimiçi Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f1d9e-125">**To add 360 Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f1d9e-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f1d9e-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f1d9e-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="f1d9e-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="f1d9e-133">Arama kutusuna **360 çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-133">In the search box, type **360 Online**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-360online-tutorial/tutorial_360online_search.png)

5. <span data-ttu-id="f1d9e-135">Sonuçlar panelinde seçin **360 çevrimiçi**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-135">In the results panel, select **360 Online**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-360online-tutorial/tutorial_360online_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f1d9e-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f1d9e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f1d9e-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı 360 çevrimiçi ile test etme</span><span class="sxs-lookup"><span data-stu-id="f1d9e-138">In this section, you configure and test Azure AD single sign-on with 360 Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f1d9e-139">Tekli çalışmaya oturum için Azure AD 360 çevrimiçi karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 360 Online is to a user in Azure AD.</span></span> <span data-ttu-id="f1d9e-140">Diğer bir deyişle, bir Azure AD kullanıcısının 360 ilgili kullanıcı arasında bir bağlantı ilişkisi çevrimiçi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-140">In other words, a link relationship between an Azure AD user and the related user in 360 Online needs to be established.</span></span>

<span data-ttu-id="f1d9e-141">360 çevrimiçi değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-141">In 360 Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f1d9e-142">Yapılandırmak ve Azure AD çoklu oturum açma ile 360 çevrimiçi sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f1d9e-142">To configure and test Azure AD single sign-on with 360 Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f1d9e-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f1d9e-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1d9e-145">**[360 çevrimiçi test kullanıcısı oluşturma](#creating-a-360-online-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı 360 çevrimiçi sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-145">**[Creating a 360 Online test user](#creating-a-360-online-test-user)** - to have a counterpart of Britta Simon in 360 Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f1d9e-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1d9e-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f1d9e-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f1d9e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f1d9e-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma 360 çevrimiçi uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 360 Online application.</span></span>

<span data-ttu-id="f1d9e-150">**Azure AD çoklu oturum açma ile 360 çevrimiçi yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f1d9e-150">**To configure Azure AD single sign-on with 360 Online, perform the following steps:**</span></span>

1. <span data-ttu-id="f1d9e-151">Azure portalında üzerinde **360 çevrimiçi** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-151">In the Azure portal, on the **360 Online** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="f1d9e-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-360online-tutorial/tutorial_360online_samlbase.png)

3. <span data-ttu-id="f1d9e-155">Üzerinde **360 çevrimiçi etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f1d9e-155">On the **360 Online Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-360online-tutorial/tutorial_360online_url.png)

    <span data-ttu-id="f1d9e-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.public360online.com`</span><span class="sxs-lookup"><span data-stu-id="f1d9e-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.public360online.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f1d9e-158">Değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-158">The value is not real.</span></span> <span data-ttu-id="f1d9e-159">Değerin gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="f1d9e-160">Kişi [360 çevrimiçi istemci destek ekibi](mailto:360online@software-innovation.com) değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-160">Contact [360 Online Client support team](mailto:360online@software-innovation.com) to get the value.</span></span> 
 
4. <span data-ttu-id="f1d9e-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-360online-tutorial/tutorial_360online_certificate.png) 

5. <span data-ttu-id="f1d9e-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-360online-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f1d9e-165">Çoklu oturum açma yapılandırmak için **360 çevrimiçi** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [360 çevrimiçi destek ekibi](mailto:360online@software-innovation.com).</span><span class="sxs-lookup"><span data-stu-id="f1d9e-165">To configure single sign-on on **360 Online** side, you need to send the downloaded **Metadata XML** to [360 Online support team](mailto:360online@software-innovation.com).</span></span> 

> [!TIP]
> <span data-ttu-id="f1d9e-166">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="f1d9e-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f1d9e-167">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f1d9e-168">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f1d9e-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f1d9e-169">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f1d9e-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="f1d9e-170">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="f1d9e-172">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f1d9e-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f1d9e-173">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-360online-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f1d9e-175">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-360online-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f1d9e-177">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-360online-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f1d9e-179">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f1d9e-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-360online-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f1d9e-181">a.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-181">a.</span></span> <span data-ttu-id="f1d9e-182">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1d9e-183">b.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-183">b.</span></span> <span data-ttu-id="f1d9e-184">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f1d9e-185">c.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-185">c.</span></span> <span data-ttu-id="f1d9e-186">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f1d9e-187">d.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-187">d.</span></span> <span data-ttu-id="f1d9e-188">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-188">Click **Create**.</span></span>
 
### <a name="creating-a-360-online-test-user"></a><span data-ttu-id="f1d9e-189">360 çevrimiçi test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f1d9e-189">Creating a 360 Online test user</span></span>

<span data-ttu-id="f1d9e-190">Bu bölümde, Britta Simon içinde 360 çevrimiçi olarak adlandırılan bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-190">In this section, you create a user called Britta Simon in 360 Online.</span></span> <span data-ttu-id="f1d9e-191">ile iletişime geçmeniz [360 çevrimiçi destek ekibi](mailto:360online@software-innovation.com).</span><span class="sxs-lookup"><span data-stu-id="f1d9e-191">you need to contact [360 Online support team](mailto:360online@software-innovation.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f1d9e-192">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="f1d9e-192">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f1d9e-193">Bu bölümde, Britta 360 çevrimiçi erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 360 Online.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="f1d9e-195">**360 çevrimiçi Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f1d9e-195">**To assign Britta Simon to 360 Online, perform the following steps:**</span></span>

1. <span data-ttu-id="f1d9e-196">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="f1d9e-198">Uygulamalar listesinde **360 çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-198">In the applications list, select **360 Online**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-360online-tutorial/tutorial_360online_app.png) 

3. <span data-ttu-id="f1d9e-200">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-200">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="f1d9e-202">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-202">Click **Add** button.</span></span> <span data-ttu-id="f1d9e-203">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="f1d9e-205">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f1d9e-206">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1d9e-207">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f1d9e-208">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="f1d9e-208">Testing single sign-on</span></span>

<span data-ttu-id="f1d9e-209">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-209">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f1d9e-210">360 çevrimiçi kutucuğa tıkladığınızda erişim panelinde, otomatik olarak 360 çevrimiçi uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="f1d9e-210">When you click the 360 Online tile in the Access Panel, you should get automatically signed-on to your 360 Online application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f1d9e-211">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f1d9e-211">Additional resources</span></span>

* [<span data-ttu-id="f1d9e-212">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="f1d9e-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1d9e-213">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="f1d9e-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-360online-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-360online-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-360online-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-360online-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-360online-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-360online-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-360online-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-360online-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-360online-tutorial/tutorial_general_203.png

