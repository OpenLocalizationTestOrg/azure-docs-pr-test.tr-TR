---
title: "Öğretici: Azure Active Directory Tümleştirme ile Druva | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Druva arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: b23e73c47b9a00893e036b67826e4b7ead819a1d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a><span data-ttu-id="634dd-103">Öğretici: Azure Active Directory Tümleştirme Druva ile</span><span class="sxs-lookup"><span data-stu-id="634dd-103">Tutorial: Azure Active Directory integration with Druva</span></span>

<span data-ttu-id="634dd-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Druva tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="634dd-104">In this tutorial, you learn how to integrate Druva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="634dd-105">Druva Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="634dd-105">Integrating Druva with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="634dd-106">Druva erişimi, Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="634dd-106">You can control in Azure AD who has access to Druva.</span></span>
- <span data-ttu-id="634dd-107">Otomatik olarak için Druva (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="634dd-107">You can enable your users to automatically get signed-on to Druva (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="634dd-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="634dd-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="634dd-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="634dd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="634dd-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="634dd-110">Prerequisites</span></span>

<span data-ttu-id="634dd-111">Azure AD tümleştirme Druva ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="634dd-111">To configure Azure AD integration with Druva, you need the following items:</span></span>

- <span data-ttu-id="634dd-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="634dd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="634dd-113">Bir Druva çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="634dd-113">A Druva single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="634dd-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="634dd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="634dd-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="634dd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="634dd-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="634dd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="634dd-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="634dd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="634dd-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="634dd-118">Scenario description</span></span>
<span data-ttu-id="634dd-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="634dd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="634dd-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="634dd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="634dd-121">Galeriden Druva ekleme</span><span class="sxs-lookup"><span data-stu-id="634dd-121">Adding Druva from the gallery</span></span>
2. <span data-ttu-id="634dd-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="634dd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-druva-from-the-gallery"></a><span data-ttu-id="634dd-123">Galeriden Druva ekleme</span><span class="sxs-lookup"><span data-stu-id="634dd-123">Adding Druva from the gallery</span></span>
<span data-ttu-id="634dd-124">Azure AD Druva tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Druva eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="634dd-124">To configure the integration of Druva into Azure AD, you need to add Druva from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="634dd-125">**Galeriden Druva eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="634dd-125">**To add Druva from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="634dd-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="634dd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="634dd-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="634dd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="634dd-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="634dd-129">Then go to **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="634dd-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="634dd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="634dd-133">Arama kutusuna **Druva**seçin **Druva** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="634dd-133">In the search box, type **Druva**, select **Druva** from result panel then click **Add** button to add the application.</span></span>

    ![Sonuçlar listesinde Druva](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="634dd-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="634dd-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="634dd-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Druva sınayın.</span><span class="sxs-lookup"><span data-stu-id="634dd-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="634dd-137">Tekli çalışmaya oturum için Azure AD Druva karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="634dd-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Druva is to a user in Azure AD.</span></span> <span data-ttu-id="634dd-138">Diğer bir deyişle, bir Azure AD kullanıcısının Druva ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="634dd-138">In other words, a link relationship between an Azure AD user and the related user in Druva needs to be established.</span></span>

<span data-ttu-id="634dd-139">Druva içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="634dd-139">In Druva, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="634dd-140">Yapılandırma ve Azure AD çoklu oturum açma Druva ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="634dd-140">To configure and test Azure AD single sign-on with Druva, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="634dd-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="634dd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="634dd-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="634dd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="634dd-143">**[Druva test kullanıcısı oluşturma](#create-a-druva-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Druva sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="634dd-143">**[Create a Druva test user](#create-a-druva-test-user)** - to have a counterpart of Britta Simon in Druva that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="634dd-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="634dd-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="634dd-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="634dd-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="634dd-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="634dd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="634dd-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Druva uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="634dd-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Druva application.</span></span>

<span data-ttu-id="634dd-148">**Azure AD çoklu oturum açma ile Druva yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="634dd-148">**To configure Azure AD single sign-on with Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="634dd-149">Azure portalında üzerinde **Druva** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="634dd-149">In the Azure portal, on the **Druva** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="634dd-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="634dd-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. <span data-ttu-id="634dd-153">Üzerinde **Druva etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="634dd-153">On the **Druva Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    <span data-ttu-id="634dd-155">İçinde **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://cloud.druva.com/home`</span><span class="sxs-lookup"><span data-stu-id="634dd-155">In the **Sign-on URL** textbox, type the URL: `https://cloud.druva.com/home`</span></span>

4. <span data-ttu-id="634dd-156">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="634dd-156">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. <span data-ttu-id="634dd-158">Özel öznitelik eşlemelerini eklemenizi gerektirir belirli bir biçimde SAML onaylar Druva uygulamanızı bekler, **SAML belirteci öznitelikleri** yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="634dd-158">Your Druva application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. <span data-ttu-id="634dd-160">İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** iletişim kutusunda, önceki görüntüde gösterildiği gibi SAML belirteci özniteliği yapılandırın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="634dd-160">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>

    | <span data-ttu-id="634dd-161">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="634dd-161">Attribute Name</span></span>      | <span data-ttu-id="634dd-162">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="634dd-162">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="634dd-163">insync\_auth\_belirteci</span><span class="sxs-lookup"><span data-stu-id="634dd-163">insync\_auth\_token</span></span> |<span data-ttu-id="634dd-164">Oluşturulan belirteç değerini girin</span><span class="sxs-lookup"><span data-stu-id="634dd-164">Enter the token generated value</span></span> |
    
    <span data-ttu-id="634dd-165">a.</span><span class="sxs-lookup"><span data-stu-id="634dd-165">a.</span></span> <span data-ttu-id="634dd-166">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="634dd-166">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="634dd-169">b.</span><span class="sxs-lookup"><span data-stu-id="634dd-169">b.</span></span> <span data-ttu-id="634dd-170">İçinde **adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="634dd-170">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="634dd-171">c.</span><span class="sxs-lookup"><span data-stu-id="634dd-171">c.</span></span> <span data-ttu-id="634dd-172">Gelen **değeri** listesinde, ilgili satır için gösterilen öznitelik değeri yazın.</span><span class="sxs-lookup"><span data-stu-id="634dd-172">From the **Value** list, type the attribute value shown for that row.</span></span> <span data-ttu-id="634dd-173">Belirteç oluşturulan değerini daha sonra öğreticide açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="634dd-173">The token generated value is explained later in tutorial.</span></span>
    
    <span data-ttu-id="634dd-174">d.</span><span class="sxs-lookup"><span data-stu-id="634dd-174">d.</span></span> <span data-ttu-id="634dd-175">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="634dd-175">Click **Ok**.</span></span>    

7. <span data-ttu-id="634dd-176">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="634dd-176">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="634dd-178">Üzerinde **Druva yapılandırma** 'yi tıklatın **yapılandırma Druva** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="634dd-178">On the **Druva Configuration** section, click **Configure Druva** to open **Configure sign-on** window.</span></span> <span data-ttu-id="634dd-179">Kopya **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="634dd-179">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. <span data-ttu-id="634dd-181">Farklı web tarayıcısı penceresinde Druva şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="634dd-181">In a different web browser window, log in to your Druva company site as an administrator.</span></span>

10. <span data-ttu-id="634dd-182">Git **yönetmek \> ayarları**.</span><span class="sxs-lookup"><span data-stu-id="634dd-182">Go to **Manage \> Settings**.</span></span>

    <span data-ttu-id="634dd-183">![Ayarları](./media/active-directory-saas-druva-tutorial/ic795091.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="634dd-183">![Settings](./media/active-directory-saas-druva-tutorial/ic795091.png "Settings")</span></span>

11. <span data-ttu-id="634dd-184">Çoklu oturum açma ayarları iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="634dd-184">On the Single Sign-On Settings dialog, perform the following steps:</span></span>

    <span data-ttu-id="634dd-185">![Çoklu oturum açma ayarları](./media/active-directory-saas-druva-tutorial/ic795092.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="634dd-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="634dd-186">a.</span><span class="sxs-lookup"><span data-stu-id="634dd-186">a.</span></span> <span data-ttu-id="634dd-187">Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyaladığınız değeri **kimlik sağlayıcısı oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="634dd-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **ID Provider Login URL** textbox.</span></span>
    
    <span data-ttu-id="634dd-188">b.</span><span class="sxs-lookup"><span data-stu-id="634dd-188">b.</span></span> <span data-ttu-id="634dd-189">Yapıştır **Sign-Out URL** Azure portalından kopyaladığınız değeri **kimlik sağlayıcısı oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="634dd-189">Paste **Sign-Out URL** value, which you have copied from the Azure portal into the **ID Provider Logout URL** textbox.</span></span>
    
     <span data-ttu-id="634dd-190">c.</span><span class="sxs-lookup"><span data-stu-id="634dd-190">c.</span></span> <span data-ttu-id="634dd-191">Base-64 kodlanmış sertifikanızı Not Defteri'nde açın, içeriğini, panoya kopyalayın ve yapıştırın kendisine **kimlik sağlayıcısının sertifikasını** metin kutusu</span><span class="sxs-lookup"><span data-stu-id="634dd-191">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **ID Provider Certificate** textbox</span></span>
     
     <span data-ttu-id="634dd-192">d.</span><span class="sxs-lookup"><span data-stu-id="634dd-192">d.</span></span> <span data-ttu-id="634dd-193">Açmak için **ayarları** sayfasında, **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="634dd-193">To open the **Settings** page, click **Save**.</span></span>

12. <span data-ttu-id="634dd-194">Üzerinde **ayarları** sayfasında, **SSO belirteç Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="634dd-194">On the **Settings** page, click **Generate SSO Token**.</span></span>

    <span data-ttu-id="634dd-195">![Ayarları](./media/active-directory-saas-druva-tutorial/ic795093.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="634dd-195">![Settings](./media/active-directory-saas-druva-tutorial/ic795093.png "Settings")</span></span>

13. <span data-ttu-id="634dd-196">Üzerinde **tek oturum açma kimlik doğrulaması belirteci** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="634dd-196">On the **Single Sign-on Authentication Token** dialog, perform the following steps:</span></span>

    <span data-ttu-id="634dd-197">![SSO belirteci](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO belirteci")</span><span class="sxs-lookup"><span data-stu-id="634dd-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span></span>
    
    <span data-ttu-id="634dd-198">a.</span><span class="sxs-lookup"><span data-stu-id="634dd-198">a.</span></span> <span data-ttu-id="634dd-199">Tıklatın **kopya**, Yapıştır kopyaladığınız değeri **değeri** metin kutusuna **özniteliği eklemek** bölümü.</span><span class="sxs-lookup"><span data-stu-id="634dd-199">Click **Copy**, Paste copied value in the **Value** textbox in the **Add Attribute** section.</span></span>
    
    <span data-ttu-id="634dd-200">b.</span><span class="sxs-lookup"><span data-stu-id="634dd-200">b.</span></span> <span data-ttu-id="634dd-201">**Kapat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="634dd-201">Click **Close**.</span></span>

> [!TIP]
> <span data-ttu-id="634dd-202">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="634dd-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="634dd-203">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="634dd-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="634dd-204">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="634dd-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="634dd-205">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="634dd-205">Create an Azure AD test user</span></span>

<span data-ttu-id="634dd-206">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="634dd-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="634dd-208">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="634dd-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="634dd-209">Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="634dd-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="634dd-211">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="634dd-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="634dd-213">Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="634dd-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Ekle düğmesi](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="634dd-215">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="634dd-215">In the **User** dialog box, perform the following steps:</span></span>

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    <span data-ttu-id="634dd-217">a.</span><span class="sxs-lookup"><span data-stu-id="634dd-217">a.</span></span> <span data-ttu-id="634dd-218">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="634dd-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="634dd-219">b.</span><span class="sxs-lookup"><span data-stu-id="634dd-219">b.</span></span> <span data-ttu-id="634dd-220">İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="634dd-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="634dd-221">c.</span><span class="sxs-lookup"><span data-stu-id="634dd-221">c.</span></span> <span data-ttu-id="634dd-222">Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="634dd-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="634dd-223">d.</span><span class="sxs-lookup"><span data-stu-id="634dd-223">d.</span></span> <span data-ttu-id="634dd-224">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="634dd-224">Click **Create**.</span></span>
 
### <a name="create-a-druva-test-user"></a><span data-ttu-id="634dd-225">Druva test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="634dd-225">Create a Druva test user</span></span>

<span data-ttu-id="634dd-226">Azure AD kullanıcıları için Druva oturum açmak etkinleştirmek için bunların Druva sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="634dd-226">In order to enable Azure AD users to log in to Druva, they must be provisioned into Druva.</span></span> <span data-ttu-id="634dd-227">Druva söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="634dd-227">In the case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="634dd-228">**Kullanıcı sağlamayı yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="634dd-228">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="634dd-229">Oturum, **Druva** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="634dd-229">Log in to your **Druva** company site as administrator.</span></span>

2. <span data-ttu-id="634dd-230">Git **yönetmek \> kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="634dd-230">Go to **Manage \> Users**.</span></span>
   
   <span data-ttu-id="634dd-231">![Kullanıcıları yönetme](./media/active-directory-saas-druva-tutorial/ic795097.png "kullanıcıları yönetme")</span><span class="sxs-lookup"><span data-stu-id="634dd-231">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795097.png "Manage Users")</span></span>

3. <span data-ttu-id="634dd-232">Tıklatın **Yeni Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="634dd-232">Click **Create New**.</span></span>
   
   <span data-ttu-id="634dd-233">![Kullanıcıları yönetme](./media/active-directory-saas-druva-tutorial/ic795098.png "kullanıcıları yönetme")</span><span class="sxs-lookup"><span data-stu-id="634dd-233">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795098.png "Manage Users")</span></span>

4. <span data-ttu-id="634dd-234">Yeni kullanıcı oluştur iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="634dd-234">On the Create New User dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="634dd-235">![NewUser oluşturma](./media/active-directory-saas-druva-tutorial/ic795099.png "NewUser oluşturma")</span><span class="sxs-lookup"><span data-stu-id="634dd-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span></span>
   
   <span data-ttu-id="634dd-236">a.</span><span class="sxs-lookup"><span data-stu-id="634dd-236">a.</span></span> <span data-ttu-id="634dd-237">İçinde **e-posta adresi** metin kutusuna, bir kullanıcı gibi e-posta girin  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="634dd-237">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="634dd-238">b.</span><span class="sxs-lookup"><span data-stu-id="634dd-238">b.</span></span> <span data-ttu-id="634dd-239">İçinde **adı** metin gibi kullanıcı adını girin **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="634dd-239">In the **Name** textbox, enter the name of user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="634dd-240">c.</span><span class="sxs-lookup"><span data-stu-id="634dd-240">c.</span></span> <span data-ttu-id="634dd-241">Tıklatın **kullanıcı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="634dd-241">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="634dd-242">API Azure AD kullanıcı hesaplarını sağlamak için Druva tarafından sağlanan veya herhangi diğer Druva kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="634dd-242">You can use any other Druva user account creation tools or APIs provided by Druva to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="634dd-243">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="634dd-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="634dd-244">Bu bölümde, Britta Druva için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="634dd-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Druva.</span></span>

![Kullanıcı rolü atayın][200] 

<span data-ttu-id="634dd-246">**Druva için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="634dd-246">**To assign Britta Simon to Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="634dd-247">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="634dd-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="634dd-249">Uygulamalar listesinde **Druva**.</span><span class="sxs-lookup"><span data-stu-id="634dd-249">In the applications list, select **Druva**.</span></span>

    ![Uygulamalar listesinde Druva bağlantı](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. <span data-ttu-id="634dd-251">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="634dd-251">In the menu on the left, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="634dd-253">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="634dd-253">Click **Add** button.</span></span> <span data-ttu-id="634dd-254">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="634dd-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="634dd-256">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="634dd-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="634dd-257">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="634dd-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="634dd-258">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="634dd-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="634dd-259">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="634dd-259">Test single sign-on</span></span>

<span data-ttu-id="634dd-260">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="634dd-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="634dd-261">Erişim paneli Druva parçasında tıklattığınızda, otomatik olarak Druva uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="634dd-261">When you click the Druva tile in the Access Panel, you should get automatically signed-on to your Druva application.</span></span>
<span data-ttu-id="634dd-262">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="634dd-262">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="634dd-263">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="634dd-263">Additional resources</span></span>

* [<span data-ttu-id="634dd-264">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="634dd-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="634dd-265">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="634dd-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

