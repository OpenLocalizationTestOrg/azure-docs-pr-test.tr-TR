---
title: "Öğretici: Azure Active Directory Tümleştirme ile OpsGenie | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile OpsGenie arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: ce63726d2406d2f1415d29786f0ef92ca95b9b90
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a><span data-ttu-id="e2f36-103">Öğretici: Azure Active Directory Tümleştirme OpsGenie ile</span><span class="sxs-lookup"><span data-stu-id="e2f36-103">Tutorial: Azure Active Directory integration with OpsGenie</span></span>

<span data-ttu-id="e2f36-104">Bu öğreticide, Azure Active Directory (Azure AD) ile OpsGenie tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e2f36-104">In this tutorial, you learn how to integrate OpsGenie with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e2f36-105">OpsGenie Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e2f36-105">Integrating OpsGenie with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e2f36-106">OpsGenie erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e2f36-106">You can control in Azure AD who has access to OpsGenie</span></span>
- <span data-ttu-id="e2f36-107">Otomatik olarak için OpsGenie (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e2f36-107">You can enable your users to automatically get signed-on to OpsGenie (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e2f36-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="e2f36-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e2f36-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e2f36-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2f36-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e2f36-110">Prerequisites</span></span>

<span data-ttu-id="e2f36-111">Azure AD tümleştirme OpsGenie ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="e2f36-111">To configure Azure AD integration with OpsGenie, you need the following items:</span></span>

- <span data-ttu-id="e2f36-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e2f36-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e2f36-113">Bir OpsGenie çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="e2f36-113">A OpsGenie single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e2f36-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e2f36-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e2f36-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e2f36-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e2f36-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e2f36-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e2f36-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e2f36-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e2f36-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e2f36-118">Scenario description</span></span>
<span data-ttu-id="e2f36-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e2f36-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e2f36-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e2f36-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e2f36-121">Galeriden OpsGenie ekleme</span><span class="sxs-lookup"><span data-stu-id="e2f36-121">Adding OpsGenie from the gallery</span></span>
2. <span data-ttu-id="e2f36-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e2f36-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-opsgenie-from-the-gallery"></a><span data-ttu-id="e2f36-123">Galeriden OpsGenie ekleme</span><span class="sxs-lookup"><span data-stu-id="e2f36-123">Adding OpsGenie from the gallery</span></span>
<span data-ttu-id="e2f36-124">Azure AD OpsGenie tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden OpsGenie eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e2f36-124">To configure the integration of OpsGenie into Azure AD, you need to add OpsGenie from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e2f36-125">**Galeriden OpsGenie eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e2f36-125">**To add OpsGenie from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e2f36-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e2f36-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e2f36-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e2f36-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e2f36-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e2f36-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="e2f36-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e2f36-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="e2f36-133">Arama kutusuna **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="e2f36-133">In the search box, type **OpsGenie**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_search.png)

5. <span data-ttu-id="e2f36-135">Sonuçlar panelinde seçin **OpsGenie**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e2f36-135">In the results panel, select **OpsGenie**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e2f36-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e2f36-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e2f36-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı OpsGenie sınayın.</span><span class="sxs-lookup"><span data-stu-id="e2f36-138">In this section, you configure and test Azure AD single sign-on with OpsGenie based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e2f36-139">Tekli çalışmaya oturum için Azure AD OpsGenie karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="e2f36-139">For single sign-on to work, Azure AD needs to know what the counterpart user in OpsGenie is to a user in Azure AD.</span></span> <span data-ttu-id="e2f36-140">Diğer bir deyişle, bir Azure AD kullanıcısının OpsGenie ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e2f36-140">In other words, a link relationship between an Azure AD user and the related user in OpsGenie needs to be established.</span></span>

<span data-ttu-id="e2f36-141">OpsGenie içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="e2f36-141">In OpsGenie, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e2f36-142">Yapılandırma ve Azure AD çoklu oturum açma OpsGenie ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e2f36-142">To configure and test Azure AD single sign-on with OpsGenie, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e2f36-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e2f36-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e2f36-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="e2f36-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e2f36-145">**[OpsGenie test kullanıcısı oluşturma](#creating-a-opsgenie-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı OpsGenie sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="e2f36-145">**[Creating a OpsGenie test user](#creating-a-opsgenie-test-user)** - to have a counterpart of Britta Simon in OpsGenie that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e2f36-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e2f36-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e2f36-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e2f36-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e2f36-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e2f36-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e2f36-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma OpsGenie uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e2f36-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OpsGenie application.</span></span>

<span data-ttu-id="e2f36-150">**Azure AD çoklu oturum açma ile OpsGenie yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e2f36-150">**To configure Azure AD single sign-on with OpsGenie, perform the following steps:**</span></span>

1. <span data-ttu-id="e2f36-151">Azure portalında üzerinde **OpsGenie** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e2f36-151">In the Azure portal, on the **OpsGenie** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="e2f36-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e2f36-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

3. <span data-ttu-id="e2f36-155">Üzerinde **OpsGenie etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e2f36-155">On the **OpsGenie Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_url.png)

    <span data-ttu-id="e2f36-157">İçinde **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://app.opsgenie.com/auth/login`</span><span class="sxs-lookup"><span data-stu-id="e2f36-157">In the **Sign-on URL** textbox, type the URL: `https://app.opsgenie.com/auth/login`</span></span>

4. <span data-ttu-id="e2f36-158">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e2f36-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_certificate.png) 

5. <span data-ttu-id="e2f36-160">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e2f36-160">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-opsgenie-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e2f36-162">Üzerinde **OpsGenie yapılandırma** 'yi tıklatın **yapılandırma OpsGenie** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e2f36-162">On the **OpsGenie Configuration** section, click **Configure OpsGenie** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e2f36-163">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="e2f36-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_configure.png) 

7. <span data-ttu-id="e2f36-165">Başka bir tarayıcı örneği açın ve ardından günlük için yönetici olarak OpsGenie bileşenini.</span><span class="sxs-lookup"><span data-stu-id="e2f36-165">Open another browser instance, and then log-in to OpsGenie as an administrator.</span></span>

8. <span data-ttu-id="e2f36-166">Tıklatın **ayarları**ve ardından **çoklu oturum açma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="e2f36-166">Click **Settings**, and then click the **Single Sign On** tab.</span></span>
   
    ![OpsGenie çoklu oturum açma](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_06.png)

9. <span data-ttu-id="e2f36-168">SSO'yu etkinleştirmek için seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="e2f36-168">To enable SSO, select **Enabled**.</span></span>
   
    ![OpsGenie ayarları](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_07.png) 

10. <span data-ttu-id="e2f36-170">İçinde **sağlayıcı** 'yi tıklatın **Azure Active Directory** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="e2f36-170">In the **Provider** section, click the **Azure Active Directory** tab.</span></span>
   
    ![OpsGenie ayarları](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_08.png) 

11. <span data-ttu-id="e2f36-172">Azure Active Directory iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e2f36-172">On the Azure Active Directory dialog page, perform the following steps:</span></span>
   
    ![OpsGenie ayarları](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    <span data-ttu-id="e2f36-174">a.</span><span class="sxs-lookup"><span data-stu-id="e2f36-174">a.</span></span> <span data-ttu-id="e2f36-175">Yapıştır **tek oturum üzerinde hizmet URL'si**, Azure portalından kopyalanan **SAML 2.0 Endpoint** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="e2f36-175">Paste **Single Sign On Service URL**, which you have copied from the Azure portal into the **SAML 2.0 Endpoint** textbox.</span></span>
    
    <span data-ttu-id="e2f36-176">b.</span><span class="sxs-lookup"><span data-stu-id="e2f36-176">b.</span></span> <span data-ttu-id="e2f36-177">İndirilen base-64 kodlanmış sertifika Not Defteri'nde açın, içeriğini, panoya kopyalayın ve ardından yapıştırın **X.500 sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="e2f36-177">Open your downloaded base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **X.500 Certificate** textbox.</span></span>
    
    <span data-ttu-id="e2f36-178">c.</span><span class="sxs-lookup"><span data-stu-id="e2f36-178">c.</span></span> <span data-ttu-id="e2f36-179">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="e2f36-179">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="e2f36-180">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e2f36-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e2f36-181">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="e2f36-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e2f36-182">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e2f36-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e2f36-183">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e2f36-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="e2f36-184">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="e2f36-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="e2f36-186">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e2f36-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e2f36-187">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e2f36-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e2f36-189">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e2f36-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e2f36-191">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="e2f36-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e2f36-193">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e2f36-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e2f36-195">a.</span><span class="sxs-lookup"><span data-stu-id="e2f36-195">a.</span></span> <span data-ttu-id="e2f36-196">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e2f36-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e2f36-197">b.</span><span class="sxs-lookup"><span data-stu-id="e2f36-197">b.</span></span> <span data-ttu-id="e2f36-198">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="e2f36-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e2f36-199">c.</span><span class="sxs-lookup"><span data-stu-id="e2f36-199">c.</span></span> <span data-ttu-id="e2f36-200">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="e2f36-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e2f36-201">d.</span><span class="sxs-lookup"><span data-stu-id="e2f36-201">d.</span></span> <span data-ttu-id="e2f36-202">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e2f36-202">Click **Create**.</span></span>
 
### <a name="creating-a-opsgenie-test-user"></a><span data-ttu-id="e2f36-203">OpsGenie test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e2f36-203">Creating a OpsGenie test user</span></span>

<span data-ttu-id="e2f36-204">Bu bölümün amacı Britta Simon içinde OpsGenie adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="e2f36-204">The objective of this section is to create a user called Britta Simon in OpsGenie.</span></span> 

1. <span data-ttu-id="e2f36-205">Bir web tarayıcısı penceresinde OpsGenie Kiracı yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e2f36-205">In a web browser window, log into your OpsGenie tenant as an administrator.</span></span>

2. <span data-ttu-id="e2f36-206">Tıklayarak kullanıcıları listesine gidin **kullanıcı** sol panelinde.</span><span class="sxs-lookup"><span data-stu-id="e2f36-206">Navigate to Users list by clicking **User** in left panel.</span></span>
   
   ![OpsGenie ayarları](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_10.png) 

3. <span data-ttu-id="e2f36-208">Tıklatın **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="e2f36-208">Click **Add User**.</span></span>

4. <span data-ttu-id="e2f36-209">Üzerinde **Kullanıcı Ekle** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e2f36-209">On the **Add User** dialog, perform the following steps:</span></span>
   
   ![OpsGenie ayarları](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   <span data-ttu-id="e2f36-211">a.</span><span class="sxs-lookup"><span data-stu-id="e2f36-211">a.</span></span> <span data-ttu-id="e2f36-212">İçinde **e-posta** metin kutusuna, e-posta adresi türü BrittaSimon ele Azure Active Directory'de.</span><span class="sxs-lookup"><span data-stu-id="e2f36-212">In the **Email** textbox, type the email address of BrittaSimon addressed in Azure Active Directory.</span></span>
   
   <span data-ttu-id="e2f36-213">b.</span><span class="sxs-lookup"><span data-stu-id="e2f36-213">b.</span></span> <span data-ttu-id="e2f36-214">İçinde **tam adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e2f36-214">In the **Full Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="e2f36-215">c.</span><span class="sxs-lookup"><span data-stu-id="e2f36-215">c.</span></span> <span data-ttu-id="e2f36-216">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e2f36-216">Click **Save**.</span></span> 

>[!NOTE]
><span data-ttu-id="e2f36-217">Britta kendi profili ayarlama yönergeleri içeren bir e-posta alır.</span><span class="sxs-lookup"><span data-stu-id="e2f36-217">Britta gets an email with instructions for setting up her profile.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e2f36-218">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="e2f36-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e2f36-219">Bu bölümde, Britta OpsGenie için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e2f36-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OpsGenie.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="e2f36-221">**OpsGenie için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e2f36-221">**To assign Britta Simon to OpsGenie, perform the following steps:**</span></span>

1. <span data-ttu-id="e2f36-222">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e2f36-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e2f36-224">Uygulamalar listesinde **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="e2f36-224">In the applications list, select **OpsGenie**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_app.png) 

3. <span data-ttu-id="e2f36-226">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e2f36-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="e2f36-228">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e2f36-228">Click **Add** button.</span></span> <span data-ttu-id="e2f36-229">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e2f36-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="e2f36-231">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e2f36-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e2f36-232">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e2f36-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e2f36-233">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e2f36-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e2f36-234">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e2f36-234">Testing single sign-on</span></span>

<span data-ttu-id="e2f36-235">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="e2f36-235">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="e2f36-236">Erişim paneli OpsGenie parçasında tıklattığınızda, otomatik olarak OpsGenie uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="e2f36-236">When you click the OpsGenie tile in the Access Panel, you should get automatically signed-on to your OpsGenie application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e2f36-237">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e2f36-237">Additional resources</span></span>

* [<span data-ttu-id="e2f36-238">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="e2f36-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e2f36-239">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e2f36-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_203.png

