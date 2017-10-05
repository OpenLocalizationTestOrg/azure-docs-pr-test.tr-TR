---
title: "Öğretici: Azure Active Directory Tümleştirme ile haberci | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile haberci arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 49211b35ab3e28e0df914061e7fa623907935638
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="95fb2-103">Öğretici: Azure Active Directory Tümleştirme haberci ile</span><span class="sxs-lookup"><span data-stu-id="95fb2-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="95fb2-104">Bu öğreticide, Azure Active Directory (Azure AD) ile haberci tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="95fb2-104">In this tutorial, you learn how to integrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="95fb2-105">Haberci Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="95fb2-105">Integrating Envoy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="95fb2-106">Haberci erişimi, Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95fb2-106">You can control in Azure AD who has access to Envoy.</span></span>
- <span data-ttu-id="95fb2-107">Otomatik olarak için haberci (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95fb2-107">You can enable your users to automatically get signed-on to Envoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="95fb2-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="95fb2-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="95fb2-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="95fb2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95fb2-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="95fb2-110">Prerequisites</span></span>

<span data-ttu-id="95fb2-111">Azure AD tümleştirme haberci ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="95fb2-111">To configure Azure AD integration with Envoy, you need the following items:</span></span>

- <span data-ttu-id="95fb2-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="95fb2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="95fb2-113">Bir haberci çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="95fb2-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="95fb2-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="95fb2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="95fb2-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="95fb2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="95fb2-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="95fb2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="95fb2-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="95fb2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="95fb2-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="95fb2-118">Scenario description</span></span>
<span data-ttu-id="95fb2-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="95fb2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="95fb2-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="95fb2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="95fb2-121">Galeriden haberci ekleme</span><span class="sxs-lookup"><span data-stu-id="95fb2-121">Adding Envoy from the gallery</span></span>
2. <span data-ttu-id="95fb2-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="95fb2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-the-gallery"></a><span data-ttu-id="95fb2-123">Galeriden haberci ekleme</span><span class="sxs-lookup"><span data-stu-id="95fb2-123">Adding Envoy from the gallery</span></span>
<span data-ttu-id="95fb2-124">Azure AD haberci tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden haberci eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="95fb2-124">To configure the integration of Envoy into Azure AD, you need to add Envoy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="95fb2-125">**Galeriden haberci eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="95fb2-125">**To add Envoy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="95fb2-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="95fb2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="95fb2-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="95fb2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="95fb2-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="95fb2-129">Then go to **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="95fb2-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="95fb2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="95fb2-133">Arama kutusuna **haberci**seçin **haberci** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="95fb2-133">In the search box, type **Envoy**, select **Envoy** from result panel then click **Add** button to add the application.</span></span>

    ![Sonuçlar listesinde haberci](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="95fb2-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="95fb2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="95fb2-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı haberci sınayın.</span><span class="sxs-lookup"><span data-stu-id="95fb2-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="95fb2-137">Tekli çalışmaya oturum için Azure AD haberci karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="95fb2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Envoy is to a user in Azure AD.</span></span> <span data-ttu-id="95fb2-138">Diğer bir deyişle, bir Azure AD kullanıcısının haberci ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="95fb2-138">In other words, a link relationship between an Azure AD user and the related user in Envoy needs to be established.</span></span>

<span data-ttu-id="95fb2-139">Haberci içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="95fb2-139">In Envoy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="95fb2-140">Yapılandırma ve Azure AD çoklu oturum açma haberci ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="95fb2-140">To configure and test Azure AD single sign-on with Envoy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="95fb2-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="95fb2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="95fb2-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="95fb2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="95fb2-143">**[Bir haberci test kullanıcısı oluşturma](#create-an-envoy-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı haberci sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="95fb2-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - to have a counterpart of Britta Simon in Envoy that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="95fb2-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="95fb2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="95fb2-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="95fb2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="95fb2-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="95fb2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="95fb2-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma haberci uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="95fb2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="95fb2-148">**Azure AD çoklu oturum açma ile haberci yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="95fb2-148">**To configure Azure AD single sign-on with Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="95fb2-149">Azure portalında üzerinde **haberci** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="95fb2-149">In the Azure portal, on the **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="95fb2-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="95fb2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. <span data-ttu-id="95fb2-153">Üzerinde **haberci etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="95fb2-153">On the **Envoy Domain and URLs** section, perform the following steps:</span></span>

    ![Haberci etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="95fb2-155">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<tenant-name>.Envoy.com`</span><span class="sxs-lookup"><span data-stu-id="95fb2-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Envoy.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="95fb2-156">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="95fb2-156">This value is not real.</span></span> <span data-ttu-id="95fb2-157">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="95fb2-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="95fb2-158">Kişi [haberci istemci destek ekibi](https://envoy.com/contact/) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="95fb2-158">Contact [Envoy Client support team](https://envoy.com/contact/) to get this value.</span></span>

4. <span data-ttu-id="95fb2-159">Üzerinde **SAML imzalama sertifikası** bölümünde, kopyalama **parmak İZİ** sertifika değerini...</span><span class="sxs-lookup"><span data-stu-id="95fb2-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate..</span></span>

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. <span data-ttu-id="95fb2-161">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="95fb2-161">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="95fb2-163">Üzerinde **haberci yapılandırma** 'yi tıklatın **yapılandırma haberci** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="95fb2-163">On the **Envoy Configuration** section, click **Configure Envoy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="95fb2-164">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="95fb2-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Haberci yapılandırma](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. <span data-ttu-id="95fb2-166">Farklı web tarayıcısı penceresinde haberci şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="95fb2-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

8. <span data-ttu-id="95fb2-167">Üstteki araç çubuğunda tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="95fb2-167">In the toolbar on the top, click **Settings**.</span></span>

    <span data-ttu-id="95fb2-168">![Haberci](./media/active-directory-saas-envoy-tutorial/ic776782.png "haberci")</span><span class="sxs-lookup"><span data-stu-id="95fb2-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span></span>

9. <span data-ttu-id="95fb2-169">Tıklatın **şirket**.</span><span class="sxs-lookup"><span data-stu-id="95fb2-169">Click **Company**.</span></span>

    <span data-ttu-id="95fb2-170">![Şirket](./media/active-directory-saas-envoy-tutorial/ic776783.png "şirket")</span><span class="sxs-lookup"><span data-stu-id="95fb2-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span></span>

10. <span data-ttu-id="95fb2-171">Tıklatın **SAML**.</span><span class="sxs-lookup"><span data-stu-id="95fb2-171">Click **SAML**.</span></span>

    <span data-ttu-id="95fb2-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="95fb2-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span></span>

11. <span data-ttu-id="95fb2-173">İçinde **SAML kimlik doğrulaması** yapılandırma bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="95fb2-173">In the **SAML Authentication** configuration section, perform the following steps:</span></span>

    <span data-ttu-id="95fb2-174">![SAML kimlik doğrulaması](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="95fb2-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="95fb2-175">Denetim merkezini konum kimliği için uygulama tarafından üretilen otomatik bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="95fb2-175">The value for the HQ location ID is auto generated by the application.</span></span>
    
    <span data-ttu-id="95fb2-176">a.</span><span class="sxs-lookup"><span data-stu-id="95fb2-176">a.</span></span> <span data-ttu-id="95fb2-177">İçinde **parmak izi** metin kutusuna, Yapıştır **parmak izi** Azure portalından kopyaladığınız sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="95fb2-177">In **Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="95fb2-178">b.</span><span class="sxs-lookup"><span data-stu-id="95fb2-178">b.</span></span> <span data-ttu-id="95fb2-179">Yapıştır **SAML çoklu oturum açma hizmet URL'si** kopyaladığınız değeri form Azure portalına **kimlik SAĞLAYICISI HTTP SAML URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="95fb2-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form the Azure portal into the **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="95fb2-180">c.</span><span class="sxs-lookup"><span data-stu-id="95fb2-180">c.</span></span> <span data-ttu-id="95fb2-181">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="95fb2-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="95fb2-182">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="95fb2-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="95fb2-183">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="95fb2-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="95fb2-184">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="95fb2-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="95fb2-185">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="95fb2-185">Create an Azure AD test user</span></span>

<span data-ttu-id="95fb2-186">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="95fb2-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="95fb2-188">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="95fb2-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="95fb2-189">Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="95fb2-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="95fb2-191">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="95fb2-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="95fb2-193">Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="95fb2-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Ekle düğmesi](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="95fb2-195">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="95fb2-195">In the **User** dialog box, perform the following steps:</span></span>

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="95fb2-197">a.</span><span class="sxs-lookup"><span data-stu-id="95fb2-197">a.</span></span> <span data-ttu-id="95fb2-198">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="95fb2-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="95fb2-199">b.</span><span class="sxs-lookup"><span data-stu-id="95fb2-199">b.</span></span> <span data-ttu-id="95fb2-200">İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="95fb2-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="95fb2-201">c.</span><span class="sxs-lookup"><span data-stu-id="95fb2-201">c.</span></span> <span data-ttu-id="95fb2-202">Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="95fb2-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="95fb2-203">d.</span><span class="sxs-lookup"><span data-stu-id="95fb2-203">d.</span></span> <span data-ttu-id="95fb2-204">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="95fb2-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="95fb2-205">Bir haberci test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="95fb2-205">Create an Envoy test user</span></span>

<span data-ttu-id="95fb2-206">Kullanıcı için haberci hazırlama yapılandırmanız için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="95fb2-206">There is no action item for you to configure user provisioning to Envoy.</span></span> <span data-ttu-id="95fb2-207">Atanmış bir kullanıcı erişim paneli kullanılarak haberci oturum açmaya çalıştığında haberci kullanıcının var olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="95fb2-207">When an assigned user tries to log into Envoy using the access panel, Envoy checks whether the user exists.</span></span> <span data-ttu-id="95fb2-208">Hiçbir kullanıcı hesabı varsa kullanılabilir henüz, haberci tarafından otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="95fb2-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="95fb2-209">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="95fb2-209">Assign the Azure AD test user</span></span>

<span data-ttu-id="95fb2-210">Bu bölümde, Britta haberci için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="95fb2-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Envoy.</span></span>

![Kullanıcı rolü atayın][200] 

<span data-ttu-id="95fb2-212">**Haberci için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="95fb2-212">**To assign Britta Simon to Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="95fb2-213">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="95fb2-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="95fb2-215">Uygulamalar listesinde **haberci**.</span><span class="sxs-lookup"><span data-stu-id="95fb2-215">In the applications list, select **Envoy**.</span></span>

    ![Uygulamalar listesinde haberci bağlantı](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. <span data-ttu-id="95fb2-217">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="95fb2-217">In the menu on the left, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="95fb2-219">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="95fb2-219">Click **Add** button.</span></span> <span data-ttu-id="95fb2-220">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="95fb2-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="95fb2-222">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="95fb2-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="95fb2-223">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="95fb2-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="95fb2-224">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="95fb2-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="95fb2-225">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="95fb2-225">Test single sign-on</span></span>

<span data-ttu-id="95fb2-226">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="95fb2-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="95fb2-227">Erişim paneli haberci parçasında tıklattığınızda, otomatik olarak haberci uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="95fb2-227">When you click the Envoy tile in the Access Panel, you should get automatically signed-on to your Envoy application.</span></span>
<span data-ttu-id="95fb2-228">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="95fb2-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="95fb2-229">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="95fb2-229">Additional resources</span></span>

* [<span data-ttu-id="95fb2-230">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="95fb2-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="95fb2-231">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="95fb2-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

