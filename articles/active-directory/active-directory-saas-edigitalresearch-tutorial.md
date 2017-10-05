---
title: "Öğretici: Azure Active Directory Tümleştirme ile eDigitalResearch | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile eDigitalResearch arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c6b66ea0-16ba-45b4-b550-e81c56262b1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: f877a1dd844c40c913f3121e5288952653c312cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-edigitalresearch"></a><span data-ttu-id="41f32-103">Öğretici: Azure Active Directory Tümleştirme eDigitalResearch ile</span><span class="sxs-lookup"><span data-stu-id="41f32-103">Tutorial: Azure Active Directory integration with eDigitalResearch</span></span>

<span data-ttu-id="41f32-104">Bu öğreticide, Azure Active Directory (Azure AD) ile eDigitalResearch tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="41f32-104">In this tutorial, you learn how to integrate eDigitalResearch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="41f32-105">EDigitalResearch Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="41f32-105">Integrating eDigitalResearch with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="41f32-106">EDigitalResearch erişimi, Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41f32-106">You can control in Azure AD who has access to eDigitalResearch.</span></span>
- <span data-ttu-id="41f32-107">Otomatik olarak Azure AD hesaplarına sahip (çoklu oturum açma) eDigitalResearch için açan kullanıcılarınıza etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41f32-107">You can enable your users to automatically get signed-on to eDigitalResearch (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="41f32-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="41f32-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="41f32-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="41f32-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41f32-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="41f32-110">Prerequisites</span></span>

<span data-ttu-id="41f32-111">Azure AD tümleştirme eDigitalResearch ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="41f32-111">To configure Azure AD integration with eDigitalResearch, you need the following items:</span></span>

- <span data-ttu-id="41f32-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="41f32-112">An Azure AD subscription</span></span>
- <span data-ttu-id="41f32-113">Bir eDigitalResearch çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="41f32-113">A eDigitalResearch single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="41f32-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="41f32-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="41f32-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="41f32-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="41f32-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="41f32-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="41f32-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="41f32-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="41f32-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="41f32-118">Scenario description</span></span>
<span data-ttu-id="41f32-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="41f32-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="41f32-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="41f32-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="41f32-121">Galeriden eDigitalResearch ekleme</span><span class="sxs-lookup"><span data-stu-id="41f32-121">Adding eDigitalResearch from the gallery</span></span>
2. <span data-ttu-id="41f32-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="41f32-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-edigitalresearch-from-the-gallery"></a><span data-ttu-id="41f32-123">Galeriden eDigitalResearch ekleme</span><span class="sxs-lookup"><span data-stu-id="41f32-123">Adding eDigitalResearch from the gallery</span></span>
<span data-ttu-id="41f32-124">Azure AD eDigitalResearch tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden eDigitalResearch eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="41f32-124">To configure the integration of eDigitalResearch into Azure AD, you need to add eDigitalResearch from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="41f32-125">**Galeriden eDigitalResearch eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="41f32-125">**To add eDigitalResearch from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="41f32-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="41f32-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="41f32-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="41f32-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="41f32-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="41f32-129">Then go to **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="41f32-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="41f32-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="41f32-133">Arama kutusuna **eDigitalResearch**seçin **eDigitalResearch** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="41f32-133">In the search box, type **eDigitalResearch**, select **eDigitalResearch** from result panel then click **Add** button to add the application.</span></span>

    ![Sonuçlar listesinde eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="41f32-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="41f32-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="41f32-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı eDigitalResearch sınayın.</span><span class="sxs-lookup"><span data-stu-id="41f32-136">In this section, you configure and test Azure AD single sign-on with eDigitalResearch based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="41f32-137">Tekli çalışmaya oturum için Azure AD eDigitalResearch karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="41f32-137">For single sign-on to work, Azure AD needs to know what the counterpart user in eDigitalResearch is to a user in Azure AD.</span></span> <span data-ttu-id="41f32-138">Diğer bir deyişle, bir Azure AD kullanıcısının eDigitalResearch ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="41f32-138">In other words, a link relationship between an Azure AD user and the related user in eDigitalResearch needs to be established.</span></span>

<span data-ttu-id="41f32-139">EDigitalResearch içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="41f32-139">In eDigitalResearch, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="41f32-140">Yapılandırma ve Azure AD çoklu oturum açma eDigitalResearch ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="41f32-140">To configure and test Azure AD single sign-on with eDigitalResearch, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="41f32-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="41f32-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="41f32-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="41f32-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="41f32-143">**[EDigitalResearch test kullanıcısı oluşturma](#create-a-edigitalresearch-test-user)**  - bir Britta Simon karşılık gelen kullanıcı Azure AD gösterimini bağlı eDigitalResearch içinde olması.</span><span class="sxs-lookup"><span data-stu-id="41f32-143">**[Create a eDigitalResearch test user](#create-a-edigitalresearch-test-user)** - to have a counterpart of Britta Simon in eDigitalResearch that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="41f32-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="41f32-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="41f32-145">**[Test çoklu oturum açma](#test-single-sign-on)**  yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="41f32-145">**[Test single sign-on](#test-single-sign-on)**  to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="41f32-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="41f32-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="41f32-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma eDigitalResearch uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="41f32-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eDigitalResearch application.</span></span>

<span data-ttu-id="41f32-148">**Azure AD çoklu oturum açma ile eDigitalResearch yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="41f32-148">**To configure Azure AD single sign-on with eDigitalResearch, perform the following steps:**</span></span>

1. <span data-ttu-id="41f32-149">Azure portalında üzerinde **eDigitalResearch** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="41f32-149">In the Azure portal, on the **eDigitalResearch** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="41f32-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="41f32-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_samlbase.png)

3. <span data-ttu-id="41f32-153">Üzerinde **eDigitalResearch etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="41f32-153">On the **eDigitalResearch Domain and URLs** section, perform the following steps:</span></span>

    ![eDigitalResearch etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_url.png)

    <span data-ttu-id="41f32-155">a.</span><span class="sxs-lookup"><span data-stu-id="41f32-155">a.</span></span> <span data-ttu-id="41f32-156">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company-name>.edigitalresearch.com`</span><span class="sxs-lookup"><span data-stu-id="41f32-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<company-name>.edigitalresearch.com`</span></span>

    <span data-ttu-id="41f32-157">b.</span><span class="sxs-lookup"><span data-stu-id="41f32-157">b.</span></span> <span data-ttu-id="41f32-158">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company-name>.edigitalresearch.com/login/consume`</span><span class="sxs-lookup"><span data-stu-id="41f32-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company-name>.edigitalresearch.com/login/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="41f32-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="41f32-159">These values are not real.</span></span> <span data-ttu-id="41f32-160">Bu değerler gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="41f32-160">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="41f32-161">Kişi [eDigitalResearch destek ekibi](http://www.maruedr.com/contact) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="41f32-161">Contact [eDigitalResearch support team](http://www.maruedr.com/contact) to get these values.</span></span>
 


4. <span data-ttu-id="41f32-162">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika Base(64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="41f32-162">On the **SAML Signing Certificate** section, click **Certificate Base(64)** and then save the certificate file on your computer.</span></span>

    <span data-ttu-id="41f32-163">!</span><span class="sxs-lookup"><span data-stu-id="41f32-163">!</span></span>![Sertifika indirme bağlantısı](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_certificate.png) 

5. <span data-ttu-id="41f32-165">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="41f32-165">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="41f32-167">Üzerinde **eDigitalResearch yapılandırma** 'yi tıklatın **eDigitalResearch yapılandırma** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="41f32-167">On the **eDigitalResearch Configuration** section, click **Configure eDigitalResearch** to open **Configure sign-on** window.</span></span> <span data-ttu-id="41f32-168">Kopya **Sign-Out URL, SAML varlık kimliği** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="41f32-168">Copy the **Sign-Out URL, SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![eDigitalResearch yapılandırma](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_configure.png) 

7. <span data-ttu-id="41f32-170">Çoklu oturum açma yapılandırmak için **eDigitalResearch** yan, indirilen göndermek için ihtiyacınız **(Base64) sertifika dosyası**, **SAML varlık kimliği**, ve **oturum kapatma URL** için [eDigitalResearch destek ekibi](http://www.maruedr.com/contact).</span><span class="sxs-lookup"><span data-stu-id="41f32-170">To configure single sign-on on **eDigitalResearch** side, you need to send the downloaded **Certificate (Base64) File**, **SAML Entity ID**, and **Sign-Out URL** to [eDigitalResearch support team](http://www.maruedr.com/contact).</span></span> <span data-ttu-id="41f32-171">Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="41f32-171">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="41f32-172">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="41f32-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="41f32-173">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="41f32-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="41f32-174">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="41f32-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="41f32-175">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="41f32-175">Create an Azure AD test user</span></span>

<span data-ttu-id="41f32-176">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="41f32-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="41f32-178">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="41f32-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="41f32-179">Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="41f32-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="41f32-181">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="41f32-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="41f32-183">Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="41f32-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Ekle düğmesi](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="41f32-185">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="41f32-185">In the **User** dialog box, perform the following steps:</span></span>

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_04.png)

    <span data-ttu-id="41f32-187">a.</span><span class="sxs-lookup"><span data-stu-id="41f32-187">a.</span></span> <span data-ttu-id="41f32-188">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="41f32-188">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="41f32-189">b.</span><span class="sxs-lookup"><span data-stu-id="41f32-189">b.</span></span> <span data-ttu-id="41f32-190">İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="41f32-190">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="41f32-191">c.</span><span class="sxs-lookup"><span data-stu-id="41f32-191">c.</span></span> <span data-ttu-id="41f32-192">Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="41f32-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="41f32-193">d.</span><span class="sxs-lookup"><span data-stu-id="41f32-193">d.</span></span> <span data-ttu-id="41f32-194">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="41f32-194">Click **Create**.</span></span>
  
### <a name="create-a-edigitalresearch-test-user"></a><span data-ttu-id="41f32-195">EDigitalResearch test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="41f32-195">Create a eDigitalResearch test user</span></span>

<span data-ttu-id="41f32-196">Bu bölümün amacı Britta Simon içinde eDigitalResearch adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="41f32-196">The objective of this section is to create a user called Britta Simon in eDigitalResearch.</span></span> 

<span data-ttu-id="41f32-197">Çalışmak [eDigitalResearch destek ekibi](http://www.maruedr.com/contact) oluşturulan kullanıcı alınamadı.</span><span class="sxs-lookup"><span data-stu-id="41f32-197">Work with the [eDigitalResearch support team](http://www.maruedr.com/contact) to get users created.</span></span>     
    
 > [!NOTE]
 > <span data-ttu-id="41f32-198">Azure Active Directory hesap sahibi bir e-posta alır ve bunu etkinleştirilmeden önce kendi hesabı onaylamak için bir bağlantı izler.</span><span class="sxs-lookup"><span data-stu-id="41f32-198">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="41f32-199">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="41f32-199">Assign the Azure AD test user</span></span>

<span data-ttu-id="41f32-200">Bu bölümde, Britta eDigitalResearch erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="41f32-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eDigitalResearch.</span></span>

![Kullanıcı rolü atayın][200] 

<span data-ttu-id="41f32-202">**EDigitalResearch için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="41f32-202">**To assign Britta Simon to eDigitalResearch, perform the following steps:**</span></span>

1. <span data-ttu-id="41f32-203">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="41f32-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="41f32-205">Uygulamalar listesinde **eDigitalResearch**.</span><span class="sxs-lookup"><span data-stu-id="41f32-205">In the applications list, select **eDigitalResearch**.</span></span>

    ![Uygulamalar listesinde eDigitalResearch bağlantı](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_app.png)  

3. <span data-ttu-id="41f32-207">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="41f32-207">In the menu on the left, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="41f32-209">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="41f32-209">Click **Add** button.</span></span> <span data-ttu-id="41f32-210">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="41f32-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="41f32-212">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="41f32-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="41f32-213">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="41f32-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="41f32-214">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="41f32-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="41f32-215">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="41f32-215">Test single sign-on</span></span>

<span data-ttu-id="41f32-216">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="41f32-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="41f32-217">Erişim paneli eDigitalResearch parçasında tıklattığınızda, otomatik olarak eDigitalResearch uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="41f32-217">When you click the eDigitalResearch tile in the Access Panel, you should get automatically signed-on to your eDigitalResearch application.</span></span>
<span data-ttu-id="41f32-218">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="41f32-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="41f32-219">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="41f32-219">Additional resources</span></span>

* [<span data-ttu-id="41f32-220">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="41f32-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="41f32-221">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="41f32-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_203.png

