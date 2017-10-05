---
title: "Öğretici: Azure Active Directory Tümleştirme Icertis sözleşme yönetim platformuyla | Microsoft Docs"
description: "Çoklu oturum açma Icertis sözleşme yönetim platformu ile Azure Active Directory arasındaki yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6627e6dd-f559-4cd4-a509-f6d9a4961b49
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 9dd002f71b7a960338071db869f7c8cf88071342
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icertis-contract-management-platform"></a><span data-ttu-id="3de65-103">Öğretici: Azure Active Directory Tümleştirme Icertis sözleşme yönetim platformu ile</span><span class="sxs-lookup"><span data-stu-id="3de65-103">Tutorial: Azure Active Directory integration with Icertis Contract Management Platform</span></span>

<span data-ttu-id="3de65-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Icertis sözleşme yönetim platformu tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3de65-104">In this tutorial, you learn how to integrate Icertis Contract Management Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3de65-105">Icertis sözleşme yönetim platformu Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="3de65-105">Integrating Icertis Contract Management Platform with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3de65-106">Icertis sözleşme yönetim platformu erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="3de65-106">You can control in Azure AD who has access to Icertis Contract Management Platform</span></span>
- <span data-ttu-id="3de65-107">Azure AD hesaplarına otomatik olarak Itanium tabanlı sistemler için Icertis sözleşme yönetim platformu için (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="3de65-107">You can enable your users to automatically get signed-on to Icertis Contract Management Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3de65-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="3de65-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3de65-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3de65-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3de65-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3de65-110">Prerequisites</span></span>

<span data-ttu-id="3de65-111">Azure AD tümleştirme Icertis sözleşme Yönetimi platformuyla yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="3de65-111">To configure Azure AD integration with Icertis Contract Management Platform, you need the following items:</span></span>

- <span data-ttu-id="3de65-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="3de65-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3de65-113">Bir Icertis sözleşme yönetim platformu çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="3de65-113">An Icertis Contract Management Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3de65-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="3de65-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3de65-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="3de65-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3de65-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="3de65-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3de65-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3de65-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3de65-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="3de65-118">Scenario description</span></span>
<span data-ttu-id="3de65-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="3de65-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3de65-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="3de65-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3de65-121">Galeriden Icertis sözleşme yönetim platformu ekleme</span><span class="sxs-lookup"><span data-stu-id="3de65-121">Adding Icertis Contract Management Platform from the gallery</span></span>
2. <span data-ttu-id="3de65-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="3de65-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icertis-contract-management-platform-from-the-gallery"></a><span data-ttu-id="3de65-123">Galeriden Icertis sözleşme yönetim platformu ekleme</span><span class="sxs-lookup"><span data-stu-id="3de65-123">Adding Icertis Contract Management Platform from the gallery</span></span>
<span data-ttu-id="3de65-124">Azure AD Icertis sözleşme yönetim platformu tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Icertis sözleşme yönetim platformu eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3de65-124">To configure the integration of Icertis Contract Management Platform into Azure AD, you need to add Icertis Contract Management Platform from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3de65-125">**Galeriden Icertis sözleşme yönetim platformu eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3de65-125">**To add Icertis Contract Management Platform from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3de65-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3de65-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3de65-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="3de65-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3de65-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3de65-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="3de65-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3de65-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="3de65-133">Arama kutusuna **Icertis sözleşme yönetim platformu**.</span><span class="sxs-lookup"><span data-stu-id="3de65-133">In the search box, type **Icertis Contract Management Platform**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_search.png)

5. <span data-ttu-id="3de65-135">Sonuçlar panelinde seçin **Icertis sözleşme yönetim platformu**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3de65-135">In the results panel, select **Icertis Contract Management Platform**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3de65-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="3de65-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3de65-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Icertis sözleşme yönetim platformuyla test etme.</span><span class="sxs-lookup"><span data-stu-id="3de65-138">In this section, you configure and test Azure AD single sign-on with Icertis Contract Management Platform based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3de65-139">Tekli çalışmaya oturum için Azure AD Icertis sözleşme yönetim platformu karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="3de65-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Icertis Contract Management Platform is to a user in Azure AD.</span></span> <span data-ttu-id="3de65-140">Diğer bir deyişle, bir Azure AD kullanıcısının Icertis sözleşme yönetim platformu ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3de65-140">In other words, a link relationship between an Azure AD user and the related user in Icertis Contract Management Platform needs to be established.</span></span>

<span data-ttu-id="3de65-141">Değeri Icertis sözleşme Yönetimi platformunda atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="3de65-141">In Icertis Contract Management Platform, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3de65-142">Yapılandırma ve Azure AD çoklu oturum açma Icertis sözleşme yönetim platformu ile test etmek için aşağıdaki yapı taşları tamamlanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="3de65-142">To configure and test Azure AD single sign-on with Icertis Contract Management Platform, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3de65-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="3de65-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3de65-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="3de65-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3de65-145">**[Bir Icertis sözleşme yönetim platformu test kullanıcısı oluşturma](#creating-an-icertis-contract-management-platform-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Icertis sözleşme yönetim platformu sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="3de65-145">**[Creating an Icertis Contract Management Platform test user](#creating-an-icertis-contract-management-platform-test-user)** - to have a counterpart of Britta Simon in Icertis Contract Management Platform that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3de65-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="3de65-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3de65-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3de65-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3de65-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3de65-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3de65-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Icertis sözleşme yönetim platformu uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3de65-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Icertis Contract Management Platform application.</span></span>

<span data-ttu-id="3de65-150">**Azure AD çoklu oturum açma Icertis sözleşme Yönetimi platformuyla yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3de65-150">**To configure Azure AD single sign-on with Icertis Contract Management Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="3de65-151">Azure portalında üzerinde **Icertis sözleşme yönetim platformu** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="3de65-151">In the Azure portal, on the **Icertis Contract Management Platform** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="3de65-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="3de65-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_samlbase.png)

3. <span data-ttu-id="3de65-155">Üzerinde **Icertis sözleşme yönetim platformu etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3de65-155">On the **Icertis Contract Management Platform Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_url.png)

    <span data-ttu-id="3de65-157">a.</span><span class="sxs-lookup"><span data-stu-id="3de65-157">a.</span></span> <span data-ttu-id="3de65-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.icertis.com`</span><span class="sxs-lookup"><span data-stu-id="3de65-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.icertis.com`</span></span>

    <span data-ttu-id="3de65-159">b.</span><span class="sxs-lookup"><span data-stu-id="3de65-159">b.</span></span> <span data-ttu-id="3de65-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.icertis.com`</span><span class="sxs-lookup"><span data-stu-id="3de65-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.icertis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3de65-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="3de65-161">These values are not real.</span></span> <span data-ttu-id="3de65-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3de65-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3de65-163">Kişi [Icertis sözleşme yönetim platformu istemci destek ekibi](https://www.icertis.com/company/contact/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="3de65-163">Contact [Icertis Contract Management Platform Client support team](https://www.icertis.com/company/contact/) to get these values.</span></span> 

4. <span data-ttu-id="3de65-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3de65-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_certificate.png) 

5. <span data-ttu-id="3de65-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3de65-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-icertisicm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3de65-168">Üzerinde **Icertis sözleşme yönetim platformu yapılandırma** 'yi tıklatın **Icertis sözleşme yönetim platformu yapılandırma** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="3de65-168">On the **Icertis Contract Management Platform Configuration** section, click **Configure Icertis Contract Management Platform** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3de65-169">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="3de65-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_configure.png) 

7. <span data-ttu-id="3de65-171">Çoklu oturum açma yapılandırmak için **Icertis sözleşme yönetim platformu** yan, indirilen göndermek için ihtiyacınız **meta veri XML** ve **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** için [Icertis sözleşme yönetim platformu destek ekibi](https://www.icertis.com/company/contact/).</span><span class="sxs-lookup"><span data-stu-id="3de65-171">To configure single sign-on on **Icertis Contract Management Platform** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="3de65-172">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="3de65-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3de65-173">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="3de65-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3de65-174">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3de65-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3de65-175">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3de65-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="3de65-176">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="3de65-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="3de65-178">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3de65-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3de65-179">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3de65-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3de65-181">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="3de65-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3de65-183">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="3de65-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3de65-185">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3de65-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3de65-187">a.</span><span class="sxs-lookup"><span data-stu-id="3de65-187">a.</span></span> <span data-ttu-id="3de65-188">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3de65-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3de65-189">b.</span><span class="sxs-lookup"><span data-stu-id="3de65-189">b.</span></span> <span data-ttu-id="3de65-190">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="3de65-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3de65-191">c.</span><span class="sxs-lookup"><span data-stu-id="3de65-191">c.</span></span> <span data-ttu-id="3de65-192">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="3de65-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3de65-193">d.</span><span class="sxs-lookup"><span data-stu-id="3de65-193">d.</span></span> <span data-ttu-id="3de65-194">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3de65-194">Click **Create**.</span></span>
 
### <a name="creating-an-icertis-contract-management-platform-test-user"></a><span data-ttu-id="3de65-195">Bir Icertis sözleşme yönetim platformu test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3de65-195">Creating an Icertis Contract Management Platform test user</span></span>

<span data-ttu-id="3de65-196">Bu bölümde, Britta Simon Icertis sözleşme Yönetimi platformunda adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3de65-196">In this section, you create a user called Britta Simon in Icertis Contract Management Platform.</span></span> <span data-ttu-id="3de65-197">Lütfen çalışmak [Icertis sözleşme yönetim platformu destek ekibi](https://www.icertis.com/company/contact/) Icertis sözleşme yönetim platformu kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="3de65-197">Please work with [Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/) to add the users in the Icertis Contract Management Platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3de65-198">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="3de65-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3de65-199">Bu bölümde, Britta Icertis sözleşme yönetim platformu için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="3de65-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Icertis Contract Management Platform.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="3de65-201">**Icertis sözleşme yönetim platformu için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3de65-201">**To assign Britta Simon to Icertis Contract Management Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="3de65-202">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3de65-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="3de65-204">Uygulamalar listesinde **Icertis sözleşme yönetim platformu**.</span><span class="sxs-lookup"><span data-stu-id="3de65-204">In the applications list, select **Icertis Contract Management Platform**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_app.png) 

3. <span data-ttu-id="3de65-206">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="3de65-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="3de65-208">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3de65-208">Click **Add** button.</span></span> <span data-ttu-id="3de65-209">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3de65-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="3de65-211">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="3de65-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3de65-212">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3de65-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3de65-213">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3de65-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3de65-214">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="3de65-214">Testing single sign-on</span></span>

<span data-ttu-id="3de65-215">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="3de65-215">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="3de65-216">Erişim paneli Icertis sözleşme yönetim platformu parçasında tıklattığınızda, otomatik olarak Icertis sözleşme yönetim platformu uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="3de65-216">When you click the Icertis Contract Management Platform tile in the Access Panel, you should get automatically signed-on to your Icertis Contract Management Platform application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3de65-217">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3de65-217">Additional resources</span></span>

* [<span data-ttu-id="3de65-218">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="3de65-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3de65-219">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="3de65-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_203.png

