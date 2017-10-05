---
title: "Öğretici: Azure Active Directory Tümleştirme ile Workstars | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Workstars arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 51a4a4e4-ff60-4971-b3f8-a0367b70d220
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: e17c85689fa3aebf00ebf559185032b90103b4a5
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workstars"></a><span data-ttu-id="40cef-103">Öğretici: Azure Active Directory Tümleştirme Workstars ile</span><span class="sxs-lookup"><span data-stu-id="40cef-103">Tutorial: Azure Active Directory integration with Workstars</span></span>

<span data-ttu-id="40cef-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Workstars tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="40cef-104">In this tutorial, you learn how to integrate Workstars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="40cef-105">Workstars Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="40cef-105">Integrating Workstars with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="40cef-106">Workstars erişimi, Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40cef-106">You can control in Azure AD who has access to Workstars.</span></span>
- <span data-ttu-id="40cef-107">Otomatik olarak için Workstars (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40cef-107">You can enable your users to automatically get signed-on to Workstars (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="40cef-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="40cef-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="40cef-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="40cef-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40cef-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="40cef-110">Prerequisites</span></span>

<span data-ttu-id="40cef-111">Azure AD tümleştirme Workstars ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="40cef-111">To configure Azure AD integration with Workstars, you need the following items:</span></span>

- <span data-ttu-id="40cef-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="40cef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="40cef-113">Bir Workstars çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="40cef-113">A Workstars single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="40cef-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="40cef-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="40cef-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="40cef-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="40cef-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="40cef-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="40cef-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="40cef-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="40cef-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="40cef-118">Scenario description</span></span>
<span data-ttu-id="40cef-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="40cef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="40cef-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="40cef-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="40cef-121">Galeriden Workstars ekleme</span><span class="sxs-lookup"><span data-stu-id="40cef-121">Adding Workstars from the gallery</span></span>
2. <span data-ttu-id="40cef-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="40cef-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workstars-from-the-gallery"></a><span data-ttu-id="40cef-123">Galeriden Workstars ekleme</span><span class="sxs-lookup"><span data-stu-id="40cef-123">Adding Workstars from the gallery</span></span>
<span data-ttu-id="40cef-124">Azure AD Workstars tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Workstars eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="40cef-124">To configure the integration of Workstars into Azure AD, you need to add Workstars from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="40cef-125">**Galeriden Workstars eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="40cef-125">**To add Workstars from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="40cef-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="40cef-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="40cef-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="40cef-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="40cef-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="40cef-129">Then go to **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="40cef-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="40cef-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="40cef-133">Arama kutusuna **Workstars**seçin **Workstars** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="40cef-133">In the search box, type **Workstars**, select **Workstars** from result panel then click **Add** button to add the application.</span></span>

    ![Sonuçlar listesinde Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="40cef-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="40cef-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="40cef-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Workstars sınayın.</span><span class="sxs-lookup"><span data-stu-id="40cef-136">In this section, you configure and test Azure AD single sign-on with Workstars based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="40cef-137">Tekli çalışmaya oturum için Azure AD Workstars karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="40cef-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Workstars is to a user in Azure AD.</span></span> <span data-ttu-id="40cef-138">Diğer bir deyişle, bir Azure AD kullanıcısının Workstars ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="40cef-138">In other words, a link relationship between an Azure AD user and the related user in Workstars needs to be established.</span></span>

<span data-ttu-id="40cef-139">Workstars içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="40cef-139">In Workstars, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="40cef-140">Yapılandırma ve Azure AD çoklu oturum açma Workstars ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="40cef-140">To configure and test Azure AD single sign-on with Workstars, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="40cef-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="40cef-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="40cef-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="40cef-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="40cef-143">**[Workstars test kullanıcısı oluşturma](#create-a-workstars-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Workstars sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="40cef-143">**[Create a Workstars test user](#create-a-workstars-test-user)** - to have a counterpart of Britta Simon in Workstars that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="40cef-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="40cef-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="40cef-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="40cef-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="40cef-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="40cef-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="40cef-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Workstars uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="40cef-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workstars application.</span></span>

<span data-ttu-id="40cef-148">**Azure AD çoklu oturum açma ile Workstars yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="40cef-148">**To configure Azure AD single sign-on with Workstars, perform the following steps:**</span></span>

1. <span data-ttu-id="40cef-149">Azure portalında üzerinde **Workstars** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="40cef-149">In the Azure portal, on the **Workstars** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="40cef-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="40cef-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_samlbase.png)

3. <span data-ttu-id="40cef-153">Üzerinde **Workstars etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="40cef-153">On the **Workstars Domain and URLs** section, perform the following steps:</span></span>

    ![Workstars etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_url.png)

    <span data-ttu-id="40cef-155">a.</span><span class="sxs-lookup"><span data-stu-id="40cef-155">a.</span></span> <span data-ttu-id="40cef-156">İçinde **tanımlayıcısı** metin kutusuna, URL'yi yazın:`https://workstars.com`</span><span class="sxs-lookup"><span data-stu-id="40cef-156">In the **Identifier** textbox, type the URL: `https://workstars.com`</span></span>

    <span data-ttu-id="40cef-157">b.</span><span class="sxs-lookup"><span data-stu-id="40cef-157">b.</span></span> <span data-ttu-id="40cef-158">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.workstars.com/saml/login_check`</span><span class="sxs-lookup"><span data-stu-id="40cef-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.workstars.com/saml/login_check`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="40cef-159">Değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="40cef-159">The value is not real.</span></span> <span data-ttu-id="40cef-160">Değerin gerçek yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="40cef-160">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="40cef-161">Kişi [Workstars destek ekibi](https://support.workstars.com) değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="40cef-161">Contact [Workstars support team](https://support.workstars.com) to get the value.</span></span>
 
4. <span data-ttu-id="40cef-162">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="40cef-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_certificate.png) 

5. <span data-ttu-id="40cef-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="40cef-164">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-workstars-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="40cef-166">Üzerinde **Workstars yapılandırma** 'yi tıklatın **yapılandırma Workstars** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="40cef-166">On the **Workstars Configuration** section, click **Configure Workstars** to open **Configure sign-on** window.</span></span> <span data-ttu-id="40cef-167">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="40cef-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Workstars yapılandırma](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_configure.png) 

7. <span data-ttu-id="40cef-169">Başka bir tarayıcı penceresinde Workstars şirket sitenize yönetici olarak oturum açma.</span><span class="sxs-lookup"><span data-stu-id="40cef-169">In another browser window, sign on to your Workstars company site as an administrator.</span></span>

8. <span data-ttu-id="40cef-170">Ana araç çubuğunda tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="40cef-170">In the main toolbar, click **Settings**.</span></span>

    ![Workstars ayarları](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_sett.png)

9. <span data-ttu-id="40cef-172">Git **oturum** > **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="40cef-172">Go to **Sign On** > **Settings**.</span></span>

    ![Workstars oturum açma](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_signon.png)

    ![Workstars ayarları](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_settings.png)

10. <span data-ttu-id="40cef-175">Üzerinde **tek oturum üzerinde (SAML) - ayarları** sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="40cef-175">On the **Single Sign On (SAML) - Settings** page, perform the following steps:</span></span>
    
    ![Workstars saml](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_saml.png)

    <span data-ttu-id="40cef-177">a.</span><span class="sxs-lookup"><span data-stu-id="40cef-177">a.</span></span> <span data-ttu-id="40cef-178">İçinde **kimlik sağlayıcı adı** metin kutusuna, türü **Office 365**.</span><span class="sxs-lookup"><span data-stu-id="40cef-178">In **Identity Provider Name** textbox, type **Office 365**.</span></span>

    <span data-ttu-id="40cef-179">b.</span><span class="sxs-lookup"><span data-stu-id="40cef-179">b.</span></span> <span data-ttu-id="40cef-180">İçinde **kimlik sağlayıcısı varlık kimliği** metin değerini yapıştırın **SAML varlık kimliği**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="40cef-180">In the **Identity Provider Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="40cef-181">c.</span><span class="sxs-lookup"><span data-stu-id="40cef-181">c.</span></span> <span data-ttu-id="40cef-182">Not Defteri'nde indirilen sertifika dosyasının içeriğini kopyalayın ve ardından yapıştırın **x509 sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="40cef-182">Copy the content of the downloaded certificate file in notepad, and then paste it into the **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="40cef-183">d.</span><span class="sxs-lookup"><span data-stu-id="40cef-183">d.</span></span> <span data-ttu-id="40cef-184">İçinde **SAML SSO URL** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="40cef-184">In the **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="40cef-185">e.</span><span class="sxs-lookup"><span data-stu-id="40cef-185">e.</span></span> <span data-ttu-id="40cef-186">İçinde **uzak oturum kapatma URL'si** metin değerini yapıştırın **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="40cef-186">In the **Remote Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="40cef-187">f.</span><span class="sxs-lookup"><span data-stu-id="40cef-187">f.</span></span> <span data-ttu-id="40cef-188">seçin **ad kimliği** olarak **e-posta (varsayılan)**.</span><span class="sxs-lookup"><span data-stu-id="40cef-188">select **Name ID** as **Email (Default)**.</span></span>

    <span data-ttu-id="40cef-189">g.</span><span class="sxs-lookup"><span data-stu-id="40cef-189">g.</span></span> <span data-ttu-id="40cef-190">Tıklatın **onaylayın**.</span><span class="sxs-lookup"><span data-stu-id="40cef-190">Click **Confirm**.</span></span>
    
> [!TIP]
> <span data-ttu-id="40cef-191">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="40cef-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="40cef-192">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="40cef-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="40cef-193">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="40cef-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="40cef-194">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="40cef-194">Create an Azure AD test user</span></span>

<span data-ttu-id="40cef-195">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="40cef-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="40cef-197">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="40cef-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="40cef-198">Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="40cef-198">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-workstars-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="40cef-200">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="40cef-200">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-workstars-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="40cef-202">Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="40cef-202">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Ekle düğmesi](./media/active-directory-saas-workstars-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="40cef-204">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="40cef-204">In the **User** dialog box, perform the following steps:</span></span>

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-workstars-tutorial/create_aaduser_04.png)

    <span data-ttu-id="40cef-206">a.</span><span class="sxs-lookup"><span data-stu-id="40cef-206">a.</span></span> <span data-ttu-id="40cef-207">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="40cef-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="40cef-208">b.</span><span class="sxs-lookup"><span data-stu-id="40cef-208">b.</span></span> <span data-ttu-id="40cef-209">İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="40cef-209">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="40cef-210">c.</span><span class="sxs-lookup"><span data-stu-id="40cef-210">c.</span></span> <span data-ttu-id="40cef-211">Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="40cef-211">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="40cef-212">d.</span><span class="sxs-lookup"><span data-stu-id="40cef-212">d.</span></span> <span data-ttu-id="40cef-213">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="40cef-213">Click **Create**.</span></span>
  
### <a name="create-a-workstars-test-user"></a><span data-ttu-id="40cef-214">Workstars test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="40cef-214">Create a Workstars test user</span></span>

<span data-ttu-id="40cef-215">Bu bölümde, Workstars içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="40cef-215">In this section, you create a user called Britta Simon in Workstars.</span></span> <span data-ttu-id="40cef-216">Çalışmak [Workstars destek ekibi](https://support.workstars.com) Workstars platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="40cef-216">Work with [Workstars support team](https://support.workstars.com) to add the users in the Workstars platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="40cef-217">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="40cef-217">Assign the Azure AD test user</span></span>

<span data-ttu-id="40cef-218">Bu bölümde, Britta Workstars için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="40cef-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workstars.</span></span>

![Kullanıcı rolü atayın][200] 

<span data-ttu-id="40cef-220">**Workstars için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="40cef-220">**To assign Britta Simon to Workstars, perform the following steps:**</span></span>

1. <span data-ttu-id="40cef-221">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="40cef-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="40cef-223">Uygulamalar listesinde **Workstars**.</span><span class="sxs-lookup"><span data-stu-id="40cef-223">In the applications list, select **Workstars**.</span></span>

    ![Uygulamalar listesinde Workstars bağlantı](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_app.png)  

3. <span data-ttu-id="40cef-225">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="40cef-225">In the menu on the left, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="40cef-227">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="40cef-227">Click **Add** button.</span></span> <span data-ttu-id="40cef-228">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="40cef-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="40cef-230">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="40cef-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="40cef-231">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="40cef-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="40cef-232">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="40cef-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="40cef-233">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="40cef-233">Test single sign-on</span></span>

<span data-ttu-id="40cef-234">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="40cef-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="40cef-235">Erişim paneli Workstars parçasında tıklattığınızda, otomatik olarak Workstars uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="40cef-235">When you click the Workstars tile in the Access Panel, you should get automatically signed-on to your Workstars application.</span></span>
<span data-ttu-id="40cef-236">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="40cef-236">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="40cef-237">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="40cef-237">Additional resources</span></span>

* [<span data-ttu-id="40cef-238">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="40cef-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="40cef-239">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="40cef-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_203.png

