---
title: "Öğretici: Azure Active Directory Tümleştirme ile Evernote | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Evernote arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: be94152a84bbbeacb623d7dd8b540e3981931a8e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a><span data-ttu-id="c0972-103">Öğretici: Azure Active Directory Tümleştirme Evernote ile</span><span class="sxs-lookup"><span data-stu-id="c0972-103">Tutorial: Azure Active Directory integration with Evernote</span></span>

<span data-ttu-id="c0972-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Evernote tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c0972-104">In this tutorial, you learn how to integrate Evernote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0972-105">Evernote Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="c0972-105">Integrating Evernote with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c0972-106">Evernote erişimi, Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0972-106">You can control in Azure AD who has access to Evernote.</span></span>
- <span data-ttu-id="c0972-107">Otomatik olarak için Evernote (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0972-107">You can enable your users to automatically get signed-on to Evernote (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c0972-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="c0972-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="c0972-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c0972-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0972-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c0972-110">Prerequisites</span></span>

<span data-ttu-id="c0972-111">Azure AD tümleştirme Evernote ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="c0972-111">To configure Azure AD integration with Evernote, you need the following items:</span></span>

- <span data-ttu-id="c0972-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="c0972-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0972-113">Bir Evernote çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="c0972-113">An Evernote single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0972-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="c0972-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0972-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c0972-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0972-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c0972-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0972-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0972-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0972-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="c0972-118">Scenario description</span></span>
<span data-ttu-id="c0972-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="c0972-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0972-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="c0972-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0972-121">Galeriden Evernote ekleme</span><span class="sxs-lookup"><span data-stu-id="c0972-121">Adding Evernote from the gallery</span></span>
2. <span data-ttu-id="c0972-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c0972-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evernote-from-the-gallery"></a><span data-ttu-id="c0972-123">Galeriden Evernote ekleme</span><span class="sxs-lookup"><span data-stu-id="c0972-123">Adding Evernote from the gallery</span></span>
<span data-ttu-id="c0972-124">Azure AD Evernote tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Evernote eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0972-124">To configure the integration of Evernote into Azure AD, you need to add Evernote from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c0972-125">**Galeriden Evernote eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c0972-125">**To add Evernote from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c0972-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c0972-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="c0972-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="c0972-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c0972-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c0972-129">Then go to **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="c0972-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c0972-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="c0972-133">Arama kutusuna **Evernote**seçin **Evernote** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="c0972-133">In the search box, type **Evernote**, select **Evernote** from result panel then click **Add** button to add the application.</span></span>

    ![Sonuçlar listesinde Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c0972-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="c0972-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c0972-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Evernote sınayın.</span><span class="sxs-lookup"><span data-stu-id="c0972-136">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c0972-137">Tekli çalışmaya oturum için Azure AD Evernote karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="c0972-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evernote is to a user in Azure AD.</span></span> <span data-ttu-id="c0972-138">Diğer bir deyişle, bir Azure AD kullanıcısının Evernote ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0972-138">In other words, a link relationship between an Azure AD user and the related user in Evernote needs to be established.</span></span>

<span data-ttu-id="c0972-139">Evernote içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="c0972-139">In Evernote, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c0972-140">Yapılandırma ve Azure AD çoklu oturum açma Evernote ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c0972-140">To configure and test Azure AD single sign-on with Evernote, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c0972-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c0972-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c0972-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="c0972-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0972-143">**[Bir Evernote test kullanıcısı oluşturma](#create-an-evernote-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Evernote sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="c0972-143">**[Create an Evernote test user](#create-an-evernote-test-user)** - to have a counterpart of Britta Simon in Evernote that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c0972-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c0972-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0972-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c0972-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c0972-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="c0972-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c0972-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Evernote uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c0972-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evernote application.</span></span>

<span data-ttu-id="c0972-148">**Azure AD çoklu oturum açma ile Evernote yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c0972-148">**To configure Azure AD single sign-on with Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="c0972-149">Azure portalında üzerinde **Evernote** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c0972-149">In the Azure portal, on the **Evernote** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="c0972-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c0972-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. <span data-ttu-id="c0972-153">Üzerinde **Evernote etki alanı ve URL'leri** bölümünde, uygulama tarafından başlatılan IDP modunda yapılandırmak istiyorsanız aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c0972-153">On the **Evernote Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Evernote etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    <span data-ttu-id="c0972-155">İçinde **tanımlayıcısı** metin kutusuna, URL'yi yazın:`https://www.evernote.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="c0972-155">In the **Identifier** textbox, type the URL: `https://www.evernote.com/saml2`</span></span>

4. <span data-ttu-id="c0972-156">Denetleme **Göster Gelişmiş URL ayarları** ve uygulamada yapılandırmak istiyorsanız aşağıdaki adımı gerçekleştirin **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="c0972-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Evernote etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    <span data-ttu-id="c0972-158">İçinde **URL üzerinde oturum** metin kutusuna, URL'yi yazın:`https://www.evernote.com/Login.action`</span><span class="sxs-lookup"><span data-stu-id="c0972-158">In the **Sign on URL** textbox, type the URL: `https://www.evernote.com/Login.action`</span></span>   

5. <span data-ttu-id="c0972-159">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c0972-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. <span data-ttu-id="c0972-161">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c0972-161">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="c0972-163">Üzerinde **Evernote yapılandırma** 'yi tıklatın **yapılandırma Evernote** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="c0972-163">On the **Evernote Configuration** section, click **Configure Evernote** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c0972-164">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="c0972-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Evernote yapılandırma](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. <span data-ttu-id="c0972-166">Farklı web tarayıcısı penceresinde Evernote şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c0972-166">In a different web browser window, log into your Evernote company site as an administrator.</span></span>

9. <span data-ttu-id="c0972-167">Git **'Yönetici Konsolu'**</span><span class="sxs-lookup"><span data-stu-id="c0972-167">Go to **'Admin Console'**</span></span>

    ![Yönetim Konsolu](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. <span data-ttu-id="c0972-169">Gelen **'Yönetici Konsolu'**gidin **'Security'** seçip **' çoklu oturum açma '**</span><span class="sxs-lookup"><span data-stu-id="c0972-169">From the **'Admin Console'**, go to **‘Security’** and select **‘Single Sign-On’**</span></span>

    ![SSO ayarı](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. <span data-ttu-id="c0972-171">Aşağıdaki değerleri yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="c0972-171">Configure the following values:</span></span>

    ![Sertifika ayarları](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    <span data-ttu-id="c0972-173">a.</span><span class="sxs-lookup"><span data-stu-id="c0972-173">a.</span></span>  <span data-ttu-id="c0972-174">**SSO etkinleştir:** SSO varsayılan olarak etkindir (tıklatın **devre dışı çoklu oturum açma** SSO gereksinimini kaldırmak için)</span><span class="sxs-lookup"><span data-stu-id="c0972-174">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** to remove the SSO requirement)</span></span>

    <span data-ttu-id="c0972-175">b.</span><span class="sxs-lookup"><span data-stu-id="c0972-175">b.</span></span> <span data-ttu-id="c0972-176">Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyaladığınız değeri **SAML HTTP istek URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="c0972-176">Paste **SAML Single sign-on Service URL** value, which you have copied from the Azure portal into the **SAML HTTP Request URL** textbox.</span></span>

    <span data-ttu-id="c0972-177">c.</span><span class="sxs-lookup"><span data-stu-id="c0972-177">c.</span></span> <span data-ttu-id="c0972-178">İndirilen sertifika Azure AD'den bir Not Defteri'nde açın ve "Sertifika başlayın" ve "Son SERTİFİKAYI" dahil olmak üzere içerik kopyalayıp yapıştırın **X.509 sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="c0972-178">Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into the **X.509 Certificate** textbox.</span></span> 

    <span data-ttu-id="c0972-179">d.Click **Değişiklikleri Kaydet**</span><span class="sxs-lookup"><span data-stu-id="c0972-179">d.Click **Save Changes**</span></span>

> [!TIP]
> <span data-ttu-id="c0972-180">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="c0972-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c0972-181">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="c0972-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c0972-182">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c0972-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c0972-183">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0972-183">Create an Azure AD test user</span></span>

<span data-ttu-id="c0972-184">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="c0972-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="c0972-186">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c0972-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c0972-187">Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c0972-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c0972-189">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c0972-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c0972-191">Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="c0972-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Ekle düğmesi](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c0972-193">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c0972-193">In the **User** dialog box, perform the following steps:</span></span>

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c0972-195">a.</span><span class="sxs-lookup"><span data-stu-id="c0972-195">a.</span></span> <span data-ttu-id="c0972-196">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c0972-196">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0972-197">b.</span><span class="sxs-lookup"><span data-stu-id="c0972-197">b.</span></span> <span data-ttu-id="c0972-198">İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="c0972-198">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="c0972-199">c.</span><span class="sxs-lookup"><span data-stu-id="c0972-199">c.</span></span> <span data-ttu-id="c0972-200">Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="c0972-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="c0972-201">d.</span><span class="sxs-lookup"><span data-stu-id="c0972-201">d.</span></span> <span data-ttu-id="c0972-202">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c0972-202">Click **Create**.</span></span>
 
### <a name="create-an-evernote-test-user"></a><span data-ttu-id="c0972-203">Bir Evernote test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0972-203">Create an Evernote test user</span></span>

<span data-ttu-id="c0972-204">Azure AD kullanıcıların Evernote oturum etkinleştirmek için bunların Evernote sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c0972-204">In order to enable Azure AD users to log into Evernote, they must be provisioned into Evernote.</span></span>  
<span data-ttu-id="c0972-205">Evernote söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="c0972-205">In the case of Evernote, provisioning is a manual task.</span></span>

<span data-ttu-id="c0972-206">**Kullanıcı hesaplarını sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c0972-206">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="c0972-207">Evernote şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c0972-207">Log in to your Evernote company site as an administrator.</span></span>

2. <span data-ttu-id="c0972-208">Tıklatın **'Yönetici Konsolu'**.</span><span class="sxs-lookup"><span data-stu-id="c0972-208">Click the **'Admin Console'**.</span></span>

    ![Yönetim Konsolu](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. <span data-ttu-id="c0972-210">Gelen **'Yönetici Konsolu'**gidin **'kullanıcıları eklemek'**.</span><span class="sxs-lookup"><span data-stu-id="c0972-210">From the **'Admin Console'**, go to **‘Add users’**.</span></span>

    ![Ekleme testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. <span data-ttu-id="c0972-212">**Ekip üyeleri ekleme** içinde **e-posta** metin kutusu, kullanıcı hesabının e-posta adresini yazın ve'ı tıklatın **davet edin.**</span><span class="sxs-lookup"><span data-stu-id="c0972-212">**Add team members** in the **Email** textbox, type the email address of user account and click **Invite.**</span></span>

    ![Ekleme testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. <span data-ttu-id="c0972-214">Davet gönderildikten sonra Azure Active Directory hesap sahibi daveti kabul etmek için e-posta alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c0972-214">After invitation is sent, the Azure Active Directory account holder will receive an email to accept the invitation.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c0972-215">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="c0972-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="c0972-216">Bu bölümde, Britta Evernote için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c0972-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evernote.</span></span>

![Kullanıcı rolü atayın][200] 

<span data-ttu-id="c0972-218">**Evernote için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c0972-218">**To assign Britta Simon to Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="c0972-219">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c0972-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="c0972-221">Uygulamalar listesinde **Evernote**.</span><span class="sxs-lookup"><span data-stu-id="c0972-221">In the applications list, select **Evernote**.</span></span>

    ![Uygulamalar listesinde Evernote bağlantı](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. <span data-ttu-id="c0972-223">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c0972-223">In the menu on the left, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="c0972-225">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c0972-225">Click **Add** button.</span></span> <span data-ttu-id="c0972-226">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c0972-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="c0972-228">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="c0972-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c0972-229">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c0972-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0972-230">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c0972-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c0972-231">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="c0972-231">Test single sign-on</span></span>

<span data-ttu-id="c0972-232">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="c0972-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c0972-233">Erişim paneli Evernote parçasında tıklattığınızda, Evernote uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="c0972-233">When you click the Evernote tile in the Access Panel, you should get signed-on to your Evernote application.</span></span> <span data-ttu-id="c0972-234">Hesap ancak sonra gerekirse, kişisel hesabıyla oturum kuruluş olarak günlüğü.</span><span class="sxs-lookup"><span data-stu-id="c0972-234">You'll be logging in as an Organization account but then need to log in with your personal account.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c0972-235">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c0972-235">Additional resources</span></span>

* [<span data-ttu-id="c0972-236">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="c0972-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0972-237">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="c0972-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

