---
title: "Öğretici: Azure Active Directory Tümleştirme ile ScreenSteps | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile ScreenSteps arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: b6ded8ba1adf03fdccbdb7573c09fae1857c8b16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="e5afb-103">Öğretici: Azure Active Directory Tümleştirme ScreenSteps ile</span><span class="sxs-lookup"><span data-stu-id="e5afb-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="e5afb-104">Bu öğreticide, Azure Active Directory (Azure AD) ile ScreenSteps tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e5afb-104">In this tutorial, you learn how to integrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e5afb-105">ScreenSteps Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e5afb-105">Integrating ScreenSteps with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e5afb-106">ScreenSteps erişimi, Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5afb-106">You can control in Azure AD who has access to ScreenSteps.</span></span>
- <span data-ttu-id="e5afb-107">Otomatik olarak için ScreenSteps (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5afb-107">You can enable your users to automatically get signed-on to ScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e5afb-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="e5afb-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="e5afb-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e5afb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5afb-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e5afb-110">Prerequisites</span></span>

<span data-ttu-id="e5afb-111">Azure AD tümleştirme ScreenSteps ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="e5afb-111">To configure Azure AD integration with ScreenSteps, you need the following items:</span></span>

- <span data-ttu-id="e5afb-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e5afb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e5afb-113">Bir ScreenSteps çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="e5afb-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e5afb-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e5afb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e5afb-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e5afb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e5afb-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e5afb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e5afb-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e5afb-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e5afb-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e5afb-118">Scenario description</span></span>
<span data-ttu-id="e5afb-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e5afb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e5afb-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e5afb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e5afb-121">Galeriden ScreenSteps ekleme</span><span class="sxs-lookup"><span data-stu-id="e5afb-121">Adding ScreenSteps from the gallery</span></span>
2. <span data-ttu-id="e5afb-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e5afb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-the-gallery"></a><span data-ttu-id="e5afb-123">Galeriden ScreenSteps ekleme</span><span class="sxs-lookup"><span data-stu-id="e5afb-123">Adding ScreenSteps from the gallery</span></span>
<span data-ttu-id="e5afb-124">Azure AD ScreenSteps tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden ScreenSteps eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5afb-124">To configure the integration of ScreenSteps into Azure AD, you need to add ScreenSteps from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e5afb-125">**Galeriden ScreenSteps eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e5afb-125">**To add ScreenSteps from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e5afb-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e5afb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="e5afb-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e5afb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e5afb-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e5afb-129">Then go to **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="e5afb-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e5afb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="e5afb-133">Arama kutusuna **ScreenSteps**seçin **ScreenSteps** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="e5afb-133">In the search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button to add the application.</span></span>

    ![Sonuçlar listesinde ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e5afb-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e5afb-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e5afb-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı ScreenSteps sınayın.</span><span class="sxs-lookup"><span data-stu-id="e5afb-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e5afb-137">Tekli çalışmaya oturum için Azure AD ScreenSteps karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="e5afb-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ScreenSteps is to a user in Azure AD.</span></span> <span data-ttu-id="e5afb-138">Diğer bir deyişle, bir Azure AD kullanıcısının ScreenSteps ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5afb-138">In other words, a link relationship between an Azure AD user and the related user in ScreenSteps needs to be established.</span></span>

<span data-ttu-id="e5afb-139">ScreenSteps içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="e5afb-139">In ScreenSteps, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e5afb-140">Yapılandırma ve Azure AD çoklu oturum açma ScreenSteps ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e5afb-140">To configure and test Azure AD single sign-on with ScreenSteps, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e5afb-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e5afb-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e5afb-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="e5afb-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e5afb-143">**[ScreenSteps test kullanıcısı oluşturma](#create-a-screensteps-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı ScreenSteps sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="e5afb-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - to have a counterpart of Britta Simon in ScreenSteps that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e5afb-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e5afb-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e5afb-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e5afb-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e5afb-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e5afb-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e5afb-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma ScreenSteps uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e5afb-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="e5afb-148">**Azure AD çoklu oturum açma ile ScreenSteps yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e5afb-148">**To configure Azure AD single sign-on with ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="e5afb-149">Azure portalında üzerinde **ScreenSteps** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e5afb-149">In the Azure portal, on the **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="e5afb-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e5afb-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. <span data-ttu-id="e5afb-153">Üzerinde **ScreenSteps etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e5afb-153">On the **ScreenSteps Domain and URLs** section, perform the following steps:</span></span>

    ![ScreenSteps etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="e5afb-155">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<tenantname>.ScreenSteps.com`</span><span class="sxs-lookup"><span data-stu-id="e5afb-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e5afb-156">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="e5afb-156">This value is not real.</span></span> <span data-ttu-id="e5afb-157">Bu değer, gerçek oturum açma, bu öğreticinin ilerleyen bölümlerinde açıklanan URL ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e5afb-157">Update this value with the actual Sign-On URL, which is explained later in this tutorial.</span></span> 

4. <span data-ttu-id="e5afb-158">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e5afb-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. <span data-ttu-id="e5afb-160">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e5afb-160">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e5afb-162">Üzerinde **ScreenSteps yapılandırma** 'yi tıklatın **yapılandırma ScreenSteps** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e5afb-162">On the **ScreenSteps Configuration** section, click **Configure ScreenSteps** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e5afb-163">Kopya **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="e5afb-163">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![ScreenSteps yapılandırma](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. <span data-ttu-id="e5afb-165">Farklı web tarayıcısı penceresinde ScreenSteps şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e5afb-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

8. <span data-ttu-id="e5afb-166">Tıklatın **hesap ayarları**.</span><span class="sxs-lookup"><span data-stu-id="e5afb-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="e5afb-167">![Hesap Yönetimi](./media/active-directory-saas-screensteps-tutorial/ic778523.png "hesap yönetimi")</span><span class="sxs-lookup"><span data-stu-id="e5afb-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span></span>

9. <span data-ttu-id="e5afb-168">Tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e5afb-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="e5afb-169">![Uzaktan kimlik doğrulama](./media/active-directory-saas-screensteps-tutorial/ic778524.png "uzaktan kimlik doğrulama")</span><span class="sxs-lookup"><span data-stu-id="e5afb-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

10. <span data-ttu-id="e5afb-170">Tıklatın **tek oturum açma uç noktası oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e5afb-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="e5afb-171">![Uzaktan kimlik doğrulama](./media/active-directory-saas-screensteps-tutorial/ic778525.png "uzaktan kimlik doğrulama")</span><span class="sxs-lookup"><span data-stu-id="e5afb-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

11. <span data-ttu-id="e5afb-172">İçinde **oluşturmak tek oturum açma uç noktası** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e5afb-172">In the **Create Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="e5afb-173">![Bir kimlik doğrulama uç noktası oluşturma](./media/active-directory-saas-screensteps-tutorial/ic778526.png "bir kimlik doğrulama uç noktası oluşturma")</span><span class="sxs-lookup"><span data-stu-id="e5afb-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="e5afb-174">a.</span><span class="sxs-lookup"><span data-stu-id="e5afb-174">a.</span></span> <span data-ttu-id="e5afb-175">İçinde **başlık** metin kutusuna, bir başlık yazın.</span><span class="sxs-lookup"><span data-stu-id="e5afb-175">In the **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="e5afb-176">b.</span><span class="sxs-lookup"><span data-stu-id="e5afb-176">b.</span></span> <span data-ttu-id="e5afb-177">Gelen **modu** listesinde **SAML**.</span><span class="sxs-lookup"><span data-stu-id="e5afb-177">From the **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="e5afb-178">c.</span><span class="sxs-lookup"><span data-stu-id="e5afb-178">c.</span></span> <span data-ttu-id="e5afb-179">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5afb-179">Click **Create**.</span></span>

12. <span data-ttu-id="e5afb-180">**Düzen** yeni uç noktası.</span><span class="sxs-lookup"><span data-stu-id="e5afb-180">**Edit** the new endpoint.</span></span>

    <span data-ttu-id="e5afb-181">![Uç noktayı Düzenle](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Düzenle uç noktası")</span><span class="sxs-lookup"><span data-stu-id="e5afb-181">![Edit endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

13. <span data-ttu-id="e5afb-182">İçinde **Düzenle tek oturum açma uç noktası** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e5afb-182">In the **Edit Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="e5afb-183">![Uzaktan kimlik doğrulama uç noktası](./media/active-directory-saas-screensteps-tutorial/ic778527.png "uzaktan kimlik doğrulama uç noktası")</span><span class="sxs-lookup"><span data-stu-id="e5afb-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="e5afb-184">a.</span><span class="sxs-lookup"><span data-stu-id="e5afb-184">a.</span></span> <span data-ttu-id="e5afb-185">Tıklatın **yeni SAML sertifika dosyası karşıya yükleme**ve Azure portalından yüklediğiniz sertifikayı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e5afb-185">Click **Upload new SAML Certificate file**, and then upload the certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="e5afb-186">b.</span><span class="sxs-lookup"><span data-stu-id="e5afb-186">b.</span></span> <span data-ttu-id="e5afb-187">Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyaladığınız değeri **uzaktan oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="e5afb-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="e5afb-188">c.</span><span class="sxs-lookup"><span data-stu-id="e5afb-188">c.</span></span> <span data-ttu-id="e5afb-189">Yapıştır **Sign-Out URL** Azure portalından kopyaladığınız değeri **oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="e5afb-189">Paste **Sign-Out URL** value, which you have copied from the Azure portal into the **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="e5afb-190">d.</span><span class="sxs-lookup"><span data-stu-id="e5afb-190">d.</span></span> <span data-ttu-id="e5afb-191">Seçin bir **grup** olduğunda bunlar sağlanan için kullanıcılara atamak için.</span><span class="sxs-lookup"><span data-stu-id="e5afb-191">Select a **Group** to assign users to when they are provisioned.</span></span>
    
    <span data-ttu-id="e5afb-192">e.</span><span class="sxs-lookup"><span data-stu-id="e5afb-192">e.</span></span> <span data-ttu-id="e5afb-193">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="e5afb-193">Click **Update**.</span></span>

    <span data-ttu-id="e5afb-194">f.</span><span class="sxs-lookup"><span data-stu-id="e5afb-194">f.</span></span> <span data-ttu-id="e5afb-195">Kopya **SAML tüketici URL** Pano ve yapıştırma için **oturum açma URL'si** metin kutusuna **ScreenSteps etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="e5afb-195">Copy the **SAML Consumer URL** to the clipboard and paste in to the **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="e5afb-196">g.</span><span class="sxs-lookup"><span data-stu-id="e5afb-196">g.</span></span> <span data-ttu-id="e5afb-197">Geri dönüp **Düzenle tek oturum açma uç noktası**.</span><span class="sxs-lookup"><span data-stu-id="e5afb-197">Return to the **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="e5afb-198">h.</span><span class="sxs-lookup"><span data-stu-id="e5afb-198">h.</span></span> <span data-ttu-id="e5afb-199">' I tıklatın **olun hesabı için varsayılan** düğmesini ScreenSteps oturum tüm kullanıcılar için bu uç noktası kullan.</span><span class="sxs-lookup"><span data-stu-id="e5afb-199">Click the **Make default for account** button to use this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="e5afb-200">Alternatif olarak tıklayabilirsiniz **eklemek için Site** belirli sitelerin Bu uç noktayı kullanmak için düğmesini **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="e5afb-200">Alternatively you can click the **Add to Site** button to use this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="e5afb-201">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e5afb-201">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e5afb-202">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="e5afb-202">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e5afb-203">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e5afb-203">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e5afb-204">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5afb-204">Create an Azure AD test user</span></span>

<span data-ttu-id="e5afb-205">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="e5afb-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="e5afb-207">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e5afb-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e5afb-208">Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e5afb-208">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e5afb-210">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e5afb-210">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e5afb-212">Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="e5afb-212">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Ekle düğmesi](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e5afb-214">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e5afb-214">In the **User** dialog box, perform the following steps:</span></span>

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e5afb-216">a.</span><span class="sxs-lookup"><span data-stu-id="e5afb-216">a.</span></span> <span data-ttu-id="e5afb-217">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e5afb-217">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e5afb-218">b.</span><span class="sxs-lookup"><span data-stu-id="e5afb-218">b.</span></span> <span data-ttu-id="e5afb-219">İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="e5afb-219">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="e5afb-220">c.</span><span class="sxs-lookup"><span data-stu-id="e5afb-220">c.</span></span> <span data-ttu-id="e5afb-221">Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="e5afb-221">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="e5afb-222">d.</span><span class="sxs-lookup"><span data-stu-id="e5afb-222">d.</span></span> <span data-ttu-id="e5afb-223">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5afb-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="e5afb-224">ScreenSteps test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5afb-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="e5afb-225">Bu bölümde, ScreenSteps içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e5afb-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="e5afb-226">Çalışmak [ScreenSteps istemci destek ekibi](https://www.screensteps.com/contact) ScreenSteps platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="e5afb-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add the users in the ScreenSteps platform.</span></span> <span data-ttu-id="e5afb-227">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="e5afb-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e5afb-228">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="e5afb-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="e5afb-229">Bu bölümde, Britta ScreenSteps için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e5afb-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ScreenSteps.</span></span>

![Kullanıcı rolü atayın][200] 

<span data-ttu-id="e5afb-231">**ScreenSteps için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e5afb-231">**To assign Britta Simon to ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="e5afb-232">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e5afb-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e5afb-234">Uygulamalar listesinde **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="e5afb-234">In the applications list, select **ScreenSteps**.</span></span>

    ![Uygulamalar listesinde ScreenSteps bağlantı](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. <span data-ttu-id="e5afb-236">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e5afb-236">In the menu on the left, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="e5afb-238">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e5afb-238">Click **Add** button.</span></span> <span data-ttu-id="e5afb-239">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e5afb-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="e5afb-241">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e5afb-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e5afb-242">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e5afb-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e5afb-243">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e5afb-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e5afb-244">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="e5afb-244">Test single sign-on</span></span>

<span data-ttu-id="e5afb-245">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="e5afb-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e5afb-246">Erişim paneli ScreenSteps parçasında tıklattığınızda, otomatik olarak ScreenSteps uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="e5afb-246">When you click the ScreenSteps tile in the Access Panel, you should get automatically signed-on to your ScreenSteps application.</span></span>
<span data-ttu-id="e5afb-247">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e5afb-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e5afb-248">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e5afb-248">Additional resources</span></span>

* [<span data-ttu-id="e5afb-249">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="e5afb-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e5afb-250">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e5afb-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

