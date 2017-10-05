---
title: "Öğretici: Azure Active Directory Tümleştirme Capriza platformuyla | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Capriza Platform arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48d92247-f00a-47b9-8d4e-137028d9e200
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 668c094d5330be1c5f71d51d2e76170dc69d1bce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-capriza-platform"></a><span data-ttu-id="1bb4c-103">Öğretici: Azure Active Directory Tümleştirme Capriza platformuyla</span><span class="sxs-lookup"><span data-stu-id="1bb4c-103">Tutorial: Azure Active Directory integration with Capriza Platform</span></span>

<span data-ttu-id="1bb4c-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Capriza Platform tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-104">In this tutorial, you learn how to integrate Capriza Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1bb4c-105">Azure AD ile Capriza Platform tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="1bb4c-105">Integrating Capriza Platform with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1bb4c-106">Capriza Platform erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1bb4c-106">You can control in Azure AD who has access to Capriza Platform</span></span>
- <span data-ttu-id="1bb4c-107">Azure AD hesaplarına otomatik olarak Capriza platformuna (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1bb4c-107">You can enable your users to automatically get signed-on to Capriza Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1bb4c-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="1bb4c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1bb4c-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1bb4c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bb4c-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1bb4c-110">Prerequisites</span></span>

<span data-ttu-id="1bb4c-111">Azure AD tümleştirme Capriza platformuyla yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="1bb4c-111">To configure Azure AD integration with Capriza Platform, you need the following items:</span></span>

- <span data-ttu-id="1bb4c-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="1bb4c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1bb4c-113">Bir Capriza Platform çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="1bb4c-113">A Capriza Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1bb4c-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1bb4c-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1bb4c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1bb4c-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1bb4c-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1bb4c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1bb4c-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="1bb4c-118">Scenario description</span></span>
<span data-ttu-id="1bb4c-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1bb4c-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="1bb4c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1bb4c-121">Galeriden Capriza Platform ekleme</span><span class="sxs-lookup"><span data-stu-id="1bb4c-121">Adding Capriza Platform from the gallery</span></span>
2. <span data-ttu-id="1bb4c-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="1bb4c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-capriza-platform-from-the-gallery"></a><span data-ttu-id="1bb4c-123">Galeriden Capriza Platform ekleme</span><span class="sxs-lookup"><span data-stu-id="1bb4c-123">Adding Capriza Platform from the gallery</span></span>
<span data-ttu-id="1bb4c-124">Azure AD Capriza Platform tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Capriza Platform eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-124">To configure the integration of Capriza Platform into Azure AD, you need to add Capriza Platform from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1bb4c-125">**Galeriden Capriza Platform eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1bb4c-125">**To add Capriza Platform from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1bb4c-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1bb4c-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1bb4c-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="1bb4c-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="1bb4c-133">Arama kutusuna **Capriza Platform**.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-133">In the search box, type **Capriza Platform**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_search.png)

5. <span data-ttu-id="1bb4c-135">Sonuçlar panelinde seçin **Capriza Platform**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-135">In the results panel, select **Capriza Platform**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1bb4c-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="1bb4c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1bb4c-138">Bu bölümde, yapılandırmak ve Azure AD çoklu oturum açmayı test Capriza platformuyla "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="1bb4c-138">In this section, you configure and test Azure AD single sign-on with Capriza Platform based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1bb4c-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen Capriza Platform bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Capriza Platform is to a user in Azure AD.</span></span> <span data-ttu-id="1bb4c-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı Capriza Platform arasında bağlantı ilişki kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-140">In other words, a link relationship between an Azure AD user and the related user in Capriza Platform needs to be established.</span></span>

<span data-ttu-id="1bb4c-141">Değeri Capriza platformunda atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-141">In Capriza Platform, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1bb4c-142">Yapılandırmak ve Azure AD çoklu oturum açma Capriza platformuyla sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1bb4c-142">To configure and test Azure AD single sign-on with Capriza Platform, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1bb4c-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1bb4c-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1bb4c-145">**[Capriza Platform test kullanıcısı oluşturma](#creating-a-capriza-platform-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Capriza Platform sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-145">**[Creating a Capriza Platform test user](#creating-a-capriza-platform-test-user)** - to have a counterpart of Britta Simon in Capriza Platform that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1bb4c-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1bb4c-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1bb4c-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1bb4c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1bb4c-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Capriza Platform uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Capriza Platform application.</span></span>

<span data-ttu-id="1bb4c-150">**Azure AD çoklu oturum açma Capriza platformuyla yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1bb4c-150">**To configure Azure AD single sign-on with Capriza Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="1bb4c-151">Azure portalında üzerinde **Capriza Platform** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-151">In the Azure portal, on the **Capriza Platform** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="1bb4c-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_samlbase.png)

3. <span data-ttu-id="1bb4c-155">Üzerinde **Capriza Platform etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1bb4c-155">On the **Capriza Platform Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_url.png)

    <span data-ttu-id="1bb4c-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.capriza.com/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="1bb4c-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.capriza.com/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1bb4c-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-158">This value is not real.</span></span> <span data-ttu-id="1bb4c-159">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="1bb4c-160">Kişi [Capriza Platform istemci destek ekibi](mailTo:support@capriza.com) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-160">Contact [Capriza Platform Client support team](mailTo:support@capriza.com) to get this value.</span></span> 

4. <span data-ttu-id="1bb4c-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_certificate.png) 

5. <span data-ttu-id="1bb4c-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-capriza-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1bb4c-165">Üzerinde **Capriza Platform Yapılandırması** 'yi tıklatın **Capriza Platform yapılandırma** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-165">On the **Capriza Platform Configuration** section, click **Configure Capriza Platform** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1bb4c-166">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="1bb4c-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_configure.png) 

7. <span data-ttu-id="1bb4c-168">Çoklu oturum açma yapılandırmak için **Capriza Platform** yan, indirilen göndermek için ihtiyacınız **sertifika**, **Sign-Out URL**, **SAML varlık kimliği**ve **SAML çoklu oturum açma hizmet URL'si** için [Capriza Platform destek ekibi](mailTo:support@capriza.com).</span><span class="sxs-lookup"><span data-stu-id="1bb4c-168">To configure single sign-on on **Capriza Platform** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [Capriza Platform support team](mailTo:support@capriza.com).</span></span> <span data-ttu-id="1bb4c-169">Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1bb4c-170">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="1bb4c-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1bb4c-171">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1bb4c-172">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1bb4c-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1bb4c-173">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1bb4c-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="1bb4c-174">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="1bb4c-176">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1bb4c-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1bb4c-177">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-capriza-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1bb4c-179">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-capriza-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1bb4c-181">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-capriza-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1bb4c-183">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1bb4c-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-capriza-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1bb4c-185">a.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-185">a.</span></span> <span data-ttu-id="1bb4c-186">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1bb4c-187">b.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-187">b.</span></span> <span data-ttu-id="1bb4c-188">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1bb4c-189">c.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-189">c.</span></span> <span data-ttu-id="1bb4c-190">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1bb4c-191">d.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-191">d.</span></span> <span data-ttu-id="1bb4c-192">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-192">Click **Create**.</span></span>
 
### <a name="creating-a-capriza-platform-test-user"></a><span data-ttu-id="1bb4c-193">Capriza Platform test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1bb4c-193">Creating a Capriza Platform test user</span></span>

<span data-ttu-id="1bb4c-194">Bu bölümün amacı Britta Simon içinde Capriza adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-194">The objective of this section is to create a user called Britta Simon in Capriza.</span></span> <span data-ttu-id="1bb4c-195">Capriza yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-195">Capriza supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="1bb4c-196">**Kullanıcı sağlama için etki alanı adınızı Capriza ile yapılandırıldığından emin olun. Bundan sonra yalnızca tam zamanı kullanıcı sağlama çalışır.**</span><span class="sxs-lookup"><span data-stu-id="1bb4c-196">**Please make sure that your domain name is configured with Capriza for user provisioning. After that only the just-in-time user provisioning will work.**</span></span>

<span data-ttu-id="1bb4c-197">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-197">There is no action item for you in this section.</span></span> <span data-ttu-id="1bb4c-198">Yeni bir kullanıcı henüz yoksa Capriza erişme denemesi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-198">A new user will be created during an attempt to access Capriza if it doesn't exist yet.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1bb4c-199">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="1bb4c-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1bb4c-200">Bu bölümde, Britta Capriza platformuna erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Capriza Platform.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="1bb4c-202">**Britta Simon Capriza platformuna atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1bb4c-202">**To assign Britta Simon to Capriza Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="1bb4c-203">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="1bb4c-205">Uygulamalar listesinde **Capriza Platform**.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-205">In the applications list, select **Capriza Platform**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_app.png) 

3. <span data-ttu-id="1bb4c-207">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="1bb4c-209">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-209">Click **Add** button.</span></span> <span data-ttu-id="1bb4c-210">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="1bb4c-212">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1bb4c-213">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1bb4c-214">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1bb4c-215">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="1bb4c-215">Testing single sign-on</span></span>

<span data-ttu-id="1bb4c-216">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1bb4c-217">Erişim paneli Capriza Platform parçasında tıklattığınızda, otomatik olarak Capriza uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="1bb4c-217">When you click the Capriza Platform tile in the Access Panel, you should get automatically signed-on to your Capriza application.</span></span> <span data-ttu-id="1bb4c-218">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1bb4c-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1bb4c-219">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="1bb4c-219">Additional resources</span></span>

* [<span data-ttu-id="1bb4c-220">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="1bb4c-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1bb4c-221">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="1bb4c-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_203.png

