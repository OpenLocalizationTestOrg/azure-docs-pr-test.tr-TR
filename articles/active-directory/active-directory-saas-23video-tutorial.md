---
title: "Öğretici: Azure Active Directory Tümleştirme ile 23 Video | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile 23 Video arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e73dd1d-3995-4a73-b9cf-1b2318d49cb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: ffcd665506c21e25c84367af5b6a3afb8e319af7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-23-video"></a><span data-ttu-id="f9091-103">Öğretici: Azure Active Directory Tümleştirme ile 23 Video</span><span class="sxs-lookup"><span data-stu-id="f9091-103">Tutorial: Azure Active Directory integration with 23 Video</span></span>

<span data-ttu-id="f9091-104">Bu öğreticide, Azure Active Directory (Azure AD) ile 23 Video tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f9091-104">In this tutorial, you learn how to integrate 23 Video with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f9091-105">23 tümleştirme Video Azure AD ile aşağıdaki faydaları sağlar:</span><span class="sxs-lookup"><span data-stu-id="f9091-105">Integrating 23 Video with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f9091-106">23 Video erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f9091-106">You can control in Azure AD who has access to 23 Video</span></span>
- <span data-ttu-id="f9091-107">Otomatik olarak Azure AD hesaplarına sahip (çoklu oturum açma) 23 video açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f9091-107">You can enable your users to automatically get signed-on to 23 Video (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f9091-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="f9091-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f9091-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f9091-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9091-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f9091-110">Prerequisites</span></span>

<span data-ttu-id="f9091-111">Azure AD Tümleştirmesi ile 23 Video yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="f9091-111">To configure Azure AD integration with 23 Video, you need the following items:</span></span>

- <span data-ttu-id="f9091-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="f9091-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f9091-113">Abonelik bir 23 Video çoklu oturum açma etkin</span><span class="sxs-lookup"><span data-stu-id="f9091-113">A 23 Video single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f9091-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="f9091-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f9091-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f9091-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f9091-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="f9091-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f9091-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f9091-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f9091-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="f9091-118">Scenario description</span></span>
<span data-ttu-id="f9091-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="f9091-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f9091-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="f9091-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f9091-121">Galeriden 23 Video ekleme</span><span class="sxs-lookup"><span data-stu-id="f9091-121">Adding 23 Video from the gallery</span></span>
2. <span data-ttu-id="f9091-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f9091-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-23-video-from-the-gallery"></a><span data-ttu-id="f9091-123">Galeriden 23 Video ekleme</span><span class="sxs-lookup"><span data-stu-id="f9091-123">Adding 23 Video from the gallery</span></span>
<span data-ttu-id="f9091-124">Azure AD 23 Video tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden 23 Video eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9091-124">To configure the integration of 23 Video into Azure AD, you need to add 23 Video from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f9091-125">**Galeriden 23 Video eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f9091-125">**To add 23 Video from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f9091-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f9091-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f9091-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="f9091-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f9091-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f9091-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="f9091-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f9091-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="f9091-133">Arama kutusuna **23 Video**.</span><span class="sxs-lookup"><span data-stu-id="f9091-133">In the search box, type **23 Video**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-23video-tutorial/tutorial_23video_search.png)

5. <span data-ttu-id="f9091-135">Sonuçlar panelinde seçin **23 Video**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f9091-135">In the results panel, select **23 Video**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-23video-tutorial/tutorial_23video_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f9091-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f9091-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f9091-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı 23 Video ile test etme</span><span class="sxs-lookup"><span data-stu-id="f9091-138">In this section, you configure and test Azure AD single sign-on with 23 Video based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f9091-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen 23 videoda bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="f9091-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 23 Video is to a user in Azure AD.</span></span> <span data-ttu-id="f9091-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı 23 arasında bir bağlantı ilişkisi Video kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9091-140">In other words, a link relationship between an Azure AD user and the related user in 23 Video needs to be established.</span></span>

<span data-ttu-id="f9091-141">23 videoda değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="f9091-141">In 23 Video, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f9091-142">Yapılandırmak ve Azure AD çoklu oturum açma ile 23 Video sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f9091-142">To configure and test Azure AD single sign-on with 23 Video, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f9091-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f9091-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f9091-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="f9091-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f9091-145">**[23 Video test kullanıcısı oluşturma](#creating-a-23-video-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı 23 Video sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="f9091-145">**[Creating a 23 Video test user](#creating-a-23-video-test-user)** - to have a counterpart of Britta Simon in 23 Video that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f9091-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f9091-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f9091-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f9091-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f9091-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f9091-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f9091-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma 23 Video uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f9091-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 23 Video application.</span></span>

<span data-ttu-id="f9091-150">**Azure AD çoklu oturum açma ile 23 Video yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f9091-150">**To configure Azure AD single sign-on with 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="f9091-151">Azure portalında üzerinde **23 Video** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="f9091-151">In the Azure portal, on the **23 Video** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="f9091-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f9091-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-23video-tutorial/tutorial_23video_samlbase.png)

3. <span data-ttu-id="f9091-155">Üzerinde **23 Video etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f9091-155">On the **23 Video Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-23video-tutorial/tutorial_23video_url.png)

    <span data-ttu-id="f9091-157">a.</span><span class="sxs-lookup"><span data-stu-id="f9091-157">a.</span></span> <span data-ttu-id="f9091-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.23video.com`</span><span class="sxs-lookup"><span data-stu-id="f9091-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.23video.com`</span></span>

    <span data-ttu-id="f9091-159">b.</span><span class="sxs-lookup"><span data-stu-id="f9091-159">b.</span></span> <span data-ttu-id="f9091-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://www.23video.com/saml/trust/<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="f9091-160">In the **Identifier** textbox, type a URL using the following pattern: `https://www.23video.com/saml/trust/<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f9091-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="f9091-161">These values are not real.</span></span> <span data-ttu-id="f9091-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f9091-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f9091-163">Kişi [23 Video istemci destek ekibi](mailto:support@23company.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="f9091-163">Contact [23 Video Client support team](mailto:support@23company.com) to get these values.</span></span> 
 
4. <span data-ttu-id="f9091-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f9091-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-23video-tutorial/tutorial_23video_certificate.png) 

5. <span data-ttu-id="f9091-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f9091-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-23video-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f9091-168">Üzerinde **23 Video yapılandırma** 'yi tıklatın **yapılandırma 23 Video** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="f9091-168">On the **23 Video Configuration** section, click **Configure 23 Video** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f9091-169">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="f9091-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-23video-tutorial/tutorial_23video_configure.png) 

7. <span data-ttu-id="f9091-171">Çoklu oturum açma yapılandırmak için **23 Video** yan, indirilen göndermek için ihtiyacınız **sertifika (Base64)**, **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si**için [23 Video destek ekibi](mailto:support@23company.com).</span><span class="sxs-lookup"><span data-stu-id="f9091-171">To configure single sign-on on **23 Video** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [23 Video support team](mailto:support@23company.com).</span></span> 


> [!TIP]
> <span data-ttu-id="f9091-172">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="f9091-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f9091-173">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="f9091-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f9091-174">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f9091-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f9091-175">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9091-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="f9091-176">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="f9091-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="f9091-178">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f9091-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f9091-179">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f9091-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-23video-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f9091-181">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f9091-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-23video-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f9091-183">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="f9091-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-23video-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f9091-185">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f9091-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-23video-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f9091-187">a.</span><span class="sxs-lookup"><span data-stu-id="f9091-187">a.</span></span> <span data-ttu-id="f9091-188">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f9091-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f9091-189">b.</span><span class="sxs-lookup"><span data-stu-id="f9091-189">b.</span></span> <span data-ttu-id="f9091-190">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="f9091-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f9091-191">c.</span><span class="sxs-lookup"><span data-stu-id="f9091-191">c.</span></span> <span data-ttu-id="f9091-192">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="f9091-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f9091-193">d.</span><span class="sxs-lookup"><span data-stu-id="f9091-193">d.</span></span> <span data-ttu-id="f9091-194">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9091-194">Click **Create**.</span></span>
 
### <a name="creating-a-23-video-test-user"></a><span data-ttu-id="f9091-195">23 Video test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9091-195">Creating a 23 Video test user</span></span>

<span data-ttu-id="f9091-196">Bu bölümün amacı, 23 videoda Britta Simon adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="f9091-196">The objective of this section is to create a user called Britta Simon in 23 Video.</span></span>

<span data-ttu-id="f9091-197">**23 videoda Britta Simon adlı bir kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f9091-197">**To create a user called Britta Simon in 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="f9091-198">23 Video şirket sitenize yönetici olarak oturum açma.</span><span class="sxs-lookup"><span data-stu-id="f9091-198">Sign on to your 23 Video company site as administrator.</span></span>

2. <span data-ttu-id="f9091-199">Git **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="f9091-199">Go to **Settings**.</span></span>
 
3. <span data-ttu-id="f9091-200">İçinde **kullanıcılar** 'yi tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="f9091-200">In **Users** section, click **Configure**.</span></span>
   
    ![Kullanıcı atama][400]

4. <span data-ttu-id="f9091-202">Tıklatın **yeni bir kullanıcı eklemek**.</span><span class="sxs-lookup"><span data-stu-id="f9091-202">Click **Add a new user**.</span></span> 
   
    ![Kullanıcı atama][401]

5. <span data-ttu-id="f9091-204">İçinde **bu siteye katılmaları için davet** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f9091-204">In the **Invite someone to join this site** section, perform the following steps:</span></span>
   
    ![Kullanıcı atama][402]

    <span data-ttu-id="f9091-206">a.</span><span class="sxs-lookup"><span data-stu-id="f9091-206">a.</span></span> <span data-ttu-id="f9091-207">İçinde **e-posta adresleri** metin kutusuna, Azure AD'de Britta Simon'ın e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="f9091-207">In the **E-mail addresses** textbox, type Britta Simon's email address in Azure AD.</span></span>  
 
    <span data-ttu-id="f9091-208">b.</span><span class="sxs-lookup"><span data-stu-id="f9091-208">b.</span></span> <span data-ttu-id="f9091-209">Tıklatın **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="f9091-209">Click **Add the user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f9091-210">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="f9091-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f9091-211">Bu bölümde, Britta 23 videoya erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f9091-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 23 Video.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="f9091-213">**23 videoya Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f9091-213">**To assign Britta Simon to 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="f9091-214">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f9091-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="f9091-216">Uygulamalar listesinde **23 Video**.</span><span class="sxs-lookup"><span data-stu-id="f9091-216">In the applications list, select **23 Video**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-23video-tutorial/tutorial_23video_app.png) 

3. <span data-ttu-id="f9091-218">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="f9091-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="f9091-220">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f9091-220">Click **Add** button.</span></span> <span data-ttu-id="f9091-221">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f9091-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="f9091-223">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="f9091-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f9091-224">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f9091-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f9091-225">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f9091-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f9091-226">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="f9091-226">Testing single sign-on</span></span>

<span data-ttu-id="f9091-227">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="f9091-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="f9091-228">Erişim paneli 23 Video parçasında tıklattığınızda, otomatik olarak 23 Video uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="f9091-228">When you click the 23 Video tile in the Access Panel, you should get automatically signed-on to your 23 Video application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f9091-229">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f9091-229">Additional resources</span></span>

* [<span data-ttu-id="f9091-230">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="f9091-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f9091-231">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="f9091-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-23video-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-23video-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-23video-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-23video-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-23video-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-23video-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-23video-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-23video-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-23video-tutorial/tutorial_general_203.png

[400]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_10.png
[401]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_11.png
[402]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_12.png
