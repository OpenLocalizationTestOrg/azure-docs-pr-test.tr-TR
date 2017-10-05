---
title: "Öğretici: Azure Active Directory Tümleştirme ile Lucidchart | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Lucidchart arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2dea669f03c893632c08d30feeb3173efc2d8243
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a><span data-ttu-id="e9127-103">Öğretici: Azure Active Directory Tümleştirme Lucidchart ile</span><span class="sxs-lookup"><span data-stu-id="e9127-103">Tutorial: Azure Active Directory integration with Lucidchart</span></span>

<span data-ttu-id="e9127-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Lucidchart tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e9127-104">In this tutorial, you learn how to integrate Lucidchart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e9127-105">Lucidchart Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e9127-105">Integrating Lucidchart with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e9127-106">Lucidchart erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e9127-106">You can control in Azure AD who has access to Lucidchart</span></span>
- <span data-ttu-id="e9127-107">Otomatik olarak için Lucidchart (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e9127-107">You can enable your users to automatically get signed-on to Lucidchart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e9127-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="e9127-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e9127-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e9127-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9127-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e9127-110">Prerequisites</span></span>

<span data-ttu-id="e9127-111">Azure AD tümleştirme Lucidchart ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="e9127-111">To configure Azure AD integration with Lucidchart, you need the following items:</span></span>

- <span data-ttu-id="e9127-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e9127-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e9127-113">Bir Lucidchart çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="e9127-113">A Lucidchart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e9127-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e9127-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e9127-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e9127-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e9127-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e9127-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e9127-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9127-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e9127-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e9127-118">Scenario description</span></span>
<span data-ttu-id="e9127-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e9127-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e9127-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e9127-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e9127-121">Galeriden Lucidchart ekleme</span><span class="sxs-lookup"><span data-stu-id="e9127-121">Adding Lucidchart from the gallery</span></span>
2. <span data-ttu-id="e9127-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e9127-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lucidchart-from-the-gallery"></a><span data-ttu-id="e9127-123">Galeriden Lucidchart ekleme</span><span class="sxs-lookup"><span data-stu-id="e9127-123">Adding Lucidchart from the gallery</span></span>
<span data-ttu-id="e9127-124">Azure AD Lucidchart tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Lucidchart eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9127-124">To configure the integration of Lucidchart into Azure AD, you need to add Lucidchart from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e9127-125">**Galeriden Lucidchart eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e9127-125">**To add Lucidchart from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e9127-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e9127-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e9127-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e9127-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e9127-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e9127-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="e9127-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e9127-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="e9127-133">Arama kutusuna **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="e9127-133">In the search box, type **Lucidchart**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_search.png)

5. <span data-ttu-id="e9127-135">Sonuçlar panelinde seçin **Lucidchart**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e9127-135">In the results panel, select **Lucidchart**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e9127-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e9127-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e9127-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Lucidchart sınayın.</span><span class="sxs-lookup"><span data-stu-id="e9127-138">In this section, you configure and test Azure AD single sign-on with Lucidchart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e9127-139">Tekli çalışmaya oturum için Azure AD Lucidchart karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="e9127-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lucidchart is to a user in Azure AD.</span></span> <span data-ttu-id="e9127-140">Diğer bir deyişle, bir Azure AD kullanıcısının Lucidchart ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9127-140">In other words, a link relationship between an Azure AD user and the related user in Lucidchart needs to be established.</span></span>

<span data-ttu-id="e9127-141">Lucidchart içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="e9127-141">In Lucidchart, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e9127-142">Yapılandırma ve Azure AD çoklu oturum açma Lucidchart ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e9127-142">To configure and test Azure AD single sign-on with Lucidchart, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e9127-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e9127-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e9127-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="e9127-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e9127-145">**[Lucidchart test kullanıcısı oluşturma](#creating-a-lucidchart-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Lucidchart sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="e9127-145">**[Creating a Lucidchart test user](#creating-a-lucidchart-test-user)** - to have a counterpart of Britta Simon in Lucidchart that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e9127-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e9127-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e9127-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e9127-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e9127-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e9127-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e9127-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Lucidchart uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e9127-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lucidchart application.</span></span>

<span data-ttu-id="e9127-150">**Azure AD çoklu oturum açma ile Lucidchart yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e9127-150">**To configure Azure AD single sign-on with Lucidchart, perform the following steps:**</span></span>

1. <span data-ttu-id="e9127-151">Azure portalında üzerinde **Lucidchart** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e9127-151">In the Azure portal, on the **Lucidchart** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="e9127-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e9127-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

3. <span data-ttu-id="e9127-155">Üzerinde **Lucidchart etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e9127-155">On the **Lucidchart Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_url.png)

    <span data-ttu-id="e9127-157">İçinde **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://chart2.office.lucidchart.com/saml/sso/azure`</span><span class="sxs-lookup"><span data-stu-id="e9127-157">In the **Sign-on URL** textbox, type a URL as: `https://chart2.office.lucidchart.com/saml/sso/azure`</span></span>

4. <span data-ttu-id="e9127-158">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e9127-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

5. <span data-ttu-id="e9127-160">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e9127-160">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lucidchart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e9127-162">Farklı web tarayıcısı penceresinde Lucidchart şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e9127-162">In a different web browser window, log into your Lucidchart company site as an administrator.</span></span>

7. <span data-ttu-id="e9127-163">Üstteki menüde tıklatın **takım**.</span><span class="sxs-lookup"><span data-stu-id="e9127-163">In the menu on the top, click **Team**.</span></span>
   
    <span data-ttu-id="e9127-164">![Takım](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "ekibi")</span><span class="sxs-lookup"><span data-stu-id="e9127-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span></span>

8. <span data-ttu-id="e9127-165">Tıklatın **uygulamaları \> SAML yönetmek**.</span><span class="sxs-lookup"><span data-stu-id="e9127-165">Click **Applications \> Manage SAML**.</span></span>
   
    <span data-ttu-id="e9127-166">![SAML yönetmek](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "SAML yönetme")</span><span class="sxs-lookup"><span data-stu-id="e9127-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML")</span></span>

9. <span data-ttu-id="e9127-167">Üzerinde **SAML kimlik doğrulaması ayarlarını** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e9127-167">On the **SAML Authentication Settings** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="e9127-168">a.</span><span class="sxs-lookup"><span data-stu-id="e9127-168">a.</span></span> <span data-ttu-id="e9127-169">Seçin **SAML kimlik doğrulamasını etkinleştir**ve ardından **isteğe bağlı**.</span><span class="sxs-lookup"><span data-stu-id="e9127-169">Select **Enable SAML Authentication**, and then click **Optional**.</span></span>

    <span data-ttu-id="e9127-170">![SAML kimlik doğrulaması ayarlarını](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML kimlik doğrulama ayarları")</span><span class="sxs-lookup"><span data-stu-id="e9127-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings")</span></span>
 
    <span data-ttu-id="e9127-171">b.</span><span class="sxs-lookup"><span data-stu-id="e9127-171">b.</span></span> <span data-ttu-id="e9127-172">İçinde **etki alanı** metin kutusuna, etki alanınızın yazın ve ardından **değişiklik sertifika**.</span><span class="sxs-lookup"><span data-stu-id="e9127-172">In the **Domain** textbox, type your domain, and then click **Change Certificate**.</span></span>

    <span data-ttu-id="e9127-173">![Sertifika değiştirme](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "sertifika değiştirme")</span><span class="sxs-lookup"><span data-stu-id="e9127-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate")</span></span>
 
    <span data-ttu-id="e9127-174">c.</span><span class="sxs-lookup"><span data-stu-id="e9127-174">c.</span></span> <span data-ttu-id="e9127-175">İndirilen meta veri dosyanızı açın, içeriği Kopyala ve ardından yapıştırın **meta veriler karşıya** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="e9127-175">Open your downloaded metadata file, copy the content, and then paste it into the **Upload Metadata** textbox.</span></span>

    <span data-ttu-id="e9127-176">![Meta veriler karşıya](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "meta veriler karşıya yükle")</span><span class="sxs-lookup"><span data-stu-id="e9127-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata")</span></span>
 
    <span data-ttu-id="e9127-177">d.</span><span class="sxs-lookup"><span data-stu-id="e9127-177">d.</span></span> <span data-ttu-id="e9127-178">Seçin **takım yeni kullanıcılara otomatik olarak Ekle**ve ardından **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="e9127-178">Select **Automatically Add new users to the team**, and then click **Save changes**.</span></span>

    <span data-ttu-id="e9127-179">![Değişiklikleri kaydetmek](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Değişiklikleri Kaydet")</span><span class="sxs-lookup"><span data-stu-id="e9127-179">![Save Changes](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Save Changes")</span></span>

> [!TIP]
> <span data-ttu-id="e9127-180">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e9127-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e9127-181">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="e9127-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e9127-182">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e9127-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e9127-183">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e9127-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="e9127-184">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="e9127-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="e9127-186">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e9127-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e9127-187">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e9127-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e9127-189">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e9127-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e9127-191">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="e9127-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e9127-193">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e9127-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e9127-195">a.</span><span class="sxs-lookup"><span data-stu-id="e9127-195">a.</span></span> <span data-ttu-id="e9127-196">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e9127-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e9127-197">b.</span><span class="sxs-lookup"><span data-stu-id="e9127-197">b.</span></span> <span data-ttu-id="e9127-198">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="e9127-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e9127-199">c.</span><span class="sxs-lookup"><span data-stu-id="e9127-199">c.</span></span> <span data-ttu-id="e9127-200">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="e9127-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e9127-201">d.</span><span class="sxs-lookup"><span data-stu-id="e9127-201">d.</span></span> <span data-ttu-id="e9127-202">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e9127-202">Click **Create**.</span></span>
 
### <a name="creating-a-lucidchart-test-user"></a><span data-ttu-id="e9127-203">Lucidchart test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e9127-203">Creating a Lucidchart test user</span></span>

<span data-ttu-id="e9127-204">Kullanıcı için Lucidchart hazırlama yapılandırmanız için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="e9127-204">There is no action item for you to configure user provisioning to Lucidchart.</span></span>  <span data-ttu-id="e9127-205">Atanmış bir kullanıcı erişim paneli kullanılarak Lucidchart oturum açmaya çalıştığında Lucidchart kullanıcının var olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="e9127-205">When an assigned user tries to log into Lucidchart using the access panel, Lucidchart checks whether the user exists.</span></span>  

<span data-ttu-id="e9127-206">Hiçbir kullanıcı hesabı varsa kullanılabilir henüz, Lucidchart tarafından otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e9127-206">If there is no user account available yet, it is automatically created by Lucidchart.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e9127-207">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="e9127-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e9127-208">Bu bölümde, Britta Lucidchart için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e9127-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lucidchart.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="e9127-210">**Lucidchart için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e9127-210">**To assign Britta Simon to Lucidchart, perform the following steps:**</span></span>

1. <span data-ttu-id="e9127-211">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e9127-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e9127-213">Uygulamalar listesinde **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="e9127-213">In the applications list, select **Lucidchart**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_app.png) 

3. <span data-ttu-id="e9127-215">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e9127-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="e9127-217">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e9127-217">Click **Add** button.</span></span> <span data-ttu-id="e9127-218">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e9127-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="e9127-220">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e9127-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e9127-221">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e9127-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e9127-222">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e9127-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e9127-223">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e9127-223">Testing single sign-on</span></span>

<span data-ttu-id="e9127-224">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="e9127-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e9127-225">Erişim paneli Lucidchart parçasında tıklattığınızda, otomatik olarak Lucidchart uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="e9127-225">When you click the Lucidchart tile in the Access Panel, you should get automatically signed-on to your Lucidchart application.</span></span>
<span data-ttu-id="e9127-226">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e9127-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e9127-227">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e9127-227">Additional resources</span></span>

* [<span data-ttu-id="e9127-228">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="e9127-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e9127-229">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e9127-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_203.png

