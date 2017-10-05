---
title: "Öğretici: Azure Active Directory Tümleştirme ile Intacct | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Intacct arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: c203b192b9da0d280cbd7f6c123219242ee4a3d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="a9188-103">Öğretici: Azure Active Directory Tümleştirme Intacct ile</span><span class="sxs-lookup"><span data-stu-id="a9188-103">Tutorial: Azure Active Directory integration with Intacct</span></span>

<span data-ttu-id="a9188-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Intacct tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="a9188-104">In this tutorial, you learn how to integrate Intacct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a9188-105">Intacct Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a9188-105">Integrating Intacct with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a9188-106">Intacct erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a9188-106">You can control in Azure AD who has access to Intacct</span></span>
- <span data-ttu-id="a9188-107">Otomatik olarak için Intacct (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a9188-107">You can enable your users to automatically get signed-on to Intacct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a9188-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="a9188-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a9188-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a9188-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9188-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a9188-110">Prerequisites</span></span>

<span data-ttu-id="a9188-111">Azure AD tümleştirme Intacct ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="a9188-111">To configure Azure AD integration with Intacct, you need the following items:</span></span>

- <span data-ttu-id="a9188-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="a9188-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a9188-113">Bir Intacct çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="a9188-113">An Intacct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a9188-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="a9188-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a9188-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a9188-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a9188-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="a9188-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a9188-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a9188-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a9188-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="a9188-118">Scenario description</span></span>
<span data-ttu-id="a9188-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="a9188-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a9188-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="a9188-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a9188-121">Galeriden Intacct ekleme</span><span class="sxs-lookup"><span data-stu-id="a9188-121">Adding Intacct from the gallery</span></span>
2. <span data-ttu-id="a9188-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a9188-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intacct-from-the-gallery"></a><span data-ttu-id="a9188-123">Galeriden Intacct ekleme</span><span class="sxs-lookup"><span data-stu-id="a9188-123">Adding Intacct from the gallery</span></span>
<span data-ttu-id="a9188-124">Azure AD Intacct tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Intacct eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9188-124">To configure the integration of Intacct into Azure AD, you need to add Intacct from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a9188-125">**Galeriden Intacct eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a9188-125">**To add Intacct from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a9188-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a9188-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a9188-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a9188-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a9188-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a9188-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="a9188-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a9188-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="a9188-133">Arama kutusuna **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="a9188-133">In the search box, type **Intacct**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. <span data-ttu-id="a9188-135">Sonuçlar panelinde seçin **Intacct**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a9188-135">In the results panel, select **Intacct**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a9188-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a9188-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a9188-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Intacct sınayın.</span><span class="sxs-lookup"><span data-stu-id="a9188-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a9188-139">Tekli çalışmaya oturum için Azure AD Intacct karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="a9188-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intacct is to a user in Azure AD.</span></span> <span data-ttu-id="a9188-140">Diğer bir deyişle, bir Azure AD kullanıcısının Intacct ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9188-140">In other words, a link relationship between an Azure AD user and the related user in Intacct needs to be established.</span></span>

<span data-ttu-id="a9188-141">Intacct içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="a9188-141">In Intacct, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a9188-142">Yapılandırma ve Azure AD çoklu oturum açma Intacct ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a9188-142">To configure and test Azure AD single sign-on with Intacct, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a9188-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a9188-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a9188-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="a9188-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a9188-145">**[Bir Intacct test kullanıcısı oluşturma](#creating-an-intacct-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Intacct sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="a9188-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - to have a counterpart of Britta Simon in Intacct that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a9188-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a9188-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a9188-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a9188-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a9188-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a9188-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a9188-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Intacct uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a9188-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intacct application.</span></span>

<span data-ttu-id="a9188-150">**Azure AD çoklu oturum açma ile Intacct yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a9188-150">**To configure Azure AD single sign-on with Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="a9188-151">Azure portalında üzerinde **Intacct** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a9188-151">In the Azure portal, on the **Intacct** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="a9188-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a9188-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. <span data-ttu-id="a9188-155">Üzerinde **Intacct etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a9188-155">On the **Intacct Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    <span data-ttu-id="a9188-157">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="a9188-157">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > <span data-ttu-id="a9188-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="a9188-158">This value is not real.</span></span> <span data-ttu-id="a9188-159">Bu değer ile gerçek yanıt URL'si güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a9188-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="a9188-160">Kişi [Intacct destek ekibi](https://us.intacct.com/support) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="a9188-160">Contact [Intacct support team](https://us.intacct.com/support) to get this value.</span></span>

4. <span data-ttu-id="a9188-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a9188-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. <span data-ttu-id="a9188-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a9188-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a9188-165">Üzerinde **Intacct yapılandırma** 'yi tıklatın **yapılandırma Intacct** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="a9188-165">On the **Intacct Configuration** section, click **Configure Intacct** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a9188-166">Kopya **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="a9188-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. <span data-ttu-id="a9188-168">Farklı web tarayıcısı penceresinde Intacct şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a9188-168">In a different web browser window, sign in to your Intacct company site as an administrator.</span></span>

8. <span data-ttu-id="a9188-169">Tıklatın **şirket** sekmesini ve ardından **şirket bilgisi**.</span><span class="sxs-lookup"><span data-stu-id="a9188-169">Click the **Company** tab, and then click **Company Info**.</span></span>

    <span data-ttu-id="a9188-170">![Şirket](./media/active-directory-saas-intacct-tutorial/ic790037.png "şirket")</span><span class="sxs-lookup"><span data-stu-id="a9188-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span></span>

9. <span data-ttu-id="a9188-171">Tıklatın **güvenlik** sekmesini ve ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="a9188-171">Click the **Security** tab, and then click **Edit**.</span></span>

    <span data-ttu-id="a9188-172">![Güvenlik](./media/active-directory-saas-intacct-tutorial/ic790038.png "güvenlik")</span><span class="sxs-lookup"><span data-stu-id="a9188-172">![Security](./media/active-directory-saas-intacct-tutorial/ic790038.png "Security")</span></span>

10. <span data-ttu-id="a9188-173">İçinde **tek oturum açma (SSO)** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a9188-173">In the **Single sign on (SSO)** section, perform the following steps:</span></span>

    <span data-ttu-id="a9188-174">![Çoklu oturum açmayı](./media/active-directory-saas-intacct-tutorial/ic790039.png "çoklu oturum açmayı")</span><span class="sxs-lookup"><span data-stu-id="a9188-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span></span>

    <span data-ttu-id="a9188-175">a.</span><span class="sxs-lookup"><span data-stu-id="a9188-175">a.</span></span> <span data-ttu-id="a9188-176">Seçin **etkinleştirmek çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a9188-176">Select **Enable single sign on**.</span></span>

    <span data-ttu-id="a9188-177">b.</span><span class="sxs-lookup"><span data-stu-id="a9188-177">b.</span></span> <span data-ttu-id="a9188-178">Olarak **kimlik sağlayıcısı türü**seçin **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="a9188-178">As **Identity provider type**, select **SAML 2.0**.</span></span>

    <span data-ttu-id="a9188-179">c.</span><span class="sxs-lookup"><span data-stu-id="a9188-179">c.</span></span> <span data-ttu-id="a9188-180">İçinde **veren URL'si** metin değerini yapıştırın **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="a9188-180">In **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="a9188-181">d.</span><span class="sxs-lookup"><span data-stu-id="a9188-181">d.</span></span> <span data-ttu-id="a9188-182">İçinde **oturum açma URL'si** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="a9188-182">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a9188-183">e.</span><span class="sxs-lookup"><span data-stu-id="a9188-183">e.</span></span> <span data-ttu-id="a9188-184">Açık, **base-64** kodlanmış sertifika Not Defteri'nde, içeriğini, panoya kopyalayın ve yapıştırın kendisine **sertifika** kutusu.</span><span class="sxs-lookup"><span data-stu-id="a9188-184">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** box.</span></span>
   
    <span data-ttu-id="a9188-185">f.</span><span class="sxs-lookup"><span data-stu-id="a9188-185">f.</span></span> <span data-ttu-id="a9188-186">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a9188-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a9188-187">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="a9188-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a9188-188">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="a9188-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a9188-189">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a9188-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a9188-190">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9188-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="a9188-191">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="a9188-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="a9188-193">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a9188-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a9188-194">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a9188-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a9188-196">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="a9188-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a9188-198">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="a9188-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a9188-200">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a9188-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a9188-202">a.</span><span class="sxs-lookup"><span data-stu-id="a9188-202">a.</span></span> <span data-ttu-id="a9188-203">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a9188-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a9188-204">b.</span><span class="sxs-lookup"><span data-stu-id="a9188-204">b.</span></span> <span data-ttu-id="a9188-205">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="a9188-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a9188-206">c.</span><span class="sxs-lookup"><span data-stu-id="a9188-206">c.</span></span> <span data-ttu-id="a9188-207">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="a9188-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a9188-208">d.</span><span class="sxs-lookup"><span data-stu-id="a9188-208">d.</span></span> <span data-ttu-id="a9188-209">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a9188-209">Click **Create**.</span></span>
 
### <a name="creating-an-intacct-test-user"></a><span data-ttu-id="a9188-210">Bir Intacct test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9188-210">Creating an Intacct test user</span></span>

<span data-ttu-id="a9188-211">Intacct için oturum açabilmeniz bunlar için Azure AD kullanıcıları ayarlamak için bunların Intacct sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a9188-211">To set up Azure AD users so they can sign in to Intacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="a9188-212">Intacct için sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="a9188-212">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="a9188-213">**Kullanıcı hesaplarını sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a9188-213">**To provision user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="a9188-214">Oturum açın, **Intacct** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="a9188-214">Sign in to your **Intacct** tenant.</span></span>

2. <span data-ttu-id="a9188-215">Tıklatın **şirket** sekmesini ve ardından **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="a9188-215">Click the **Company** tab, and then click **Users**.</span></span>

    <span data-ttu-id="a9188-216">![Kullanıcıların](./media/active-directory-saas-intacct-tutorial/ic790041.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="a9188-216">![Users](./media/active-directory-saas-intacct-tutorial/ic790041.png "Users")</span></span>
3. <span data-ttu-id="a9188-217">Tıklatın **Ekle** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a9188-217">Click the **Add** tab.</span></span>

    <span data-ttu-id="a9188-218">![Ekleme](./media/active-directory-saas-intacct-tutorial/ic790042.png "ekleme")</span><span class="sxs-lookup"><span data-stu-id="a9188-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span></span>
4. <span data-ttu-id="a9188-219">İçinde **kullanıcı bilgilerini** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a9188-219">In the **User Information** section, perform the following steps:</span></span>

    <span data-ttu-id="a9188-220">![Kullanıcı bilgilerini](./media/active-directory-saas-intacct-tutorial/ic790043.png "kullanıcı bilgileri")</span><span class="sxs-lookup"><span data-stu-id="a9188-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span></span>

    <span data-ttu-id="a9188-221">a.</span><span class="sxs-lookup"><span data-stu-id="a9188-221">a.</span></span> <span data-ttu-id="a9188-222">Girin **kullanıcı kimliği**, **Soyadı**, **ad**, **e-posta adresi**, **başlık**ve **Telefon** sağlamayı istediğiniz bir Azure AD hesabının **kullanıcı bilgilerini** bölümü.</span><span class="sxs-lookup"><span data-stu-id="a9188-222">Enter the **User ID**, the **Last name**, **First name**, the **Email address**, the **Title**, and the **Phone** of an Azure AD account that you want to provision into the **User Information** section.</span></span>

    <span data-ttu-id="a9188-223">b.</span><span class="sxs-lookup"><span data-stu-id="a9188-223">b.</span></span> <span data-ttu-id="a9188-224">Seçin **yönetici ayrıcalıkları** sağlamak istediğiniz bir Azure AD hesabının.</span><span class="sxs-lookup"><span data-stu-id="a9188-224">Select the **Admin privileges** of an Azure AD account that you want to provision.</span></span>
   
    <span data-ttu-id="a9188-225">c.</span><span class="sxs-lookup"><span data-stu-id="a9188-225">c.</span></span> <span data-ttu-id="a9188-226">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a9188-226">Click **Save**.</span></span> <span data-ttu-id="a9188-227">Azure AD hesap sahibi bir e-posta alır ve bunu etkinleştirilmeden önce kendi hesabı onaylamak için bir bağlantı izler.</span><span class="sxs-lookup"><span data-stu-id="a9188-227">The Azure AD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="a9188-228">Azure AD kullanıcı hesaplarını sağlamak için diğer Intacct kullanıcı hesabı oluşturma araçlarını veya Intacct tarafından sağlanan API'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9188-228">To provision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a9188-229">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="a9188-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a9188-230">Bu bölümde, Britta Intacct için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a9188-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intacct.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="a9188-232">**Intacct için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a9188-232">**To assign Britta Simon to Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="a9188-233">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a9188-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="a9188-235">Uygulamalar listesinde **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="a9188-235">In the applications list, select **Intacct**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. <span data-ttu-id="a9188-237">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a9188-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="a9188-239">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a9188-239">Click **Add** button.</span></span> <span data-ttu-id="a9188-240">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a9188-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="a9188-242">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="a9188-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a9188-243">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a9188-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a9188-244">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a9188-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a9188-245">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="a9188-245">Testing single sign-on</span></span>

<span data-ttu-id="a9188-246">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test.</span><span class="sxs-lookup"><span data-stu-id="a9188-246">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="a9188-247">Erişim paneli Intacct parçasında tıklattığınızda, otomatik olarak Intacct uygulamanıza oturum açmanız.</span><span class="sxs-lookup"><span data-stu-id="a9188-247">When you click the Intacct tile in the Access Panel, you should be automatically signed in to your Intacct application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a9188-248">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a9188-248">Additional resources</span></span>

* [<span data-ttu-id="a9188-249">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="a9188-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a9188-250">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="a9188-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

