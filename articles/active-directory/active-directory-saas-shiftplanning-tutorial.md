---
title: "Öğretici: Azure Active Directory Tümleştirme ile Humanity | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Humanity arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 327cc1e3d0836e79376e0a3cd5a4422a967f5943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="31303-103">Öğretici: Azure Active Directory Tümleştirme Humanity ile</span><span class="sxs-lookup"><span data-stu-id="31303-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="31303-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Humanity tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="31303-104">In this tutorial, you learn how to integrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="31303-105">Humanity Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="31303-105">Integrating Humanity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="31303-106">Humanity erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="31303-106">You can control in Azure AD who has access to Humanity</span></span>
- <span data-ttu-id="31303-107">Otomatik olarak için Humanity (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="31303-107">You can enable your users to automatically get signed-on to Humanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="31303-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="31303-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="31303-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="31303-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31303-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="31303-110">Prerequisites</span></span>

<span data-ttu-id="31303-111">Azure AD tümleştirme Humanity ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="31303-111">To configure Azure AD integration with Humanity, you need the following items:</span></span>

- <span data-ttu-id="31303-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="31303-112">An Azure AD subscription</span></span>
- <span data-ttu-id="31303-113">Bir Humanity çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="31303-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="31303-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="31303-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="31303-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="31303-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="31303-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="31303-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="31303-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="31303-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="31303-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="31303-118">Scenario description</span></span>
<span data-ttu-id="31303-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="31303-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="31303-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="31303-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="31303-121">Galeriden Humanity ekleme</span><span class="sxs-lookup"><span data-stu-id="31303-121">Adding Humanity from the gallery</span></span>
2. <span data-ttu-id="31303-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="31303-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-the-gallery"></a><span data-ttu-id="31303-123">Galeriden Humanity ekleme</span><span class="sxs-lookup"><span data-stu-id="31303-123">Adding Humanity from the gallery</span></span>
<span data-ttu-id="31303-124">Azure AD'ye Humanity tümleştirmesini yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Humanity eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="31303-124">To configure the integration of Humanity into Azure AD, you need to add Humanity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="31303-125">**Galeriden Humanity eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="31303-125">**To add Humanity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="31303-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="31303-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="31303-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="31303-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="31303-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="31303-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="31303-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="31303-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="31303-133">Arama kutusuna **Humanity**.</span><span class="sxs-lookup"><span data-stu-id="31303-133">In the search box, type **Humanity**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. <span data-ttu-id="31303-135">Sonuçlar panelinde seçin **Humanity**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="31303-135">In the results panel, select **Humanity**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="31303-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="31303-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="31303-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Humanity ile test etme</span><span class="sxs-lookup"><span data-stu-id="31303-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="31303-139">Tekli çalışmaya oturum için Azure AD Humanity karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="31303-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Humanity is to a user in Azure AD.</span></span> <span data-ttu-id="31303-140">Diğer bir deyişle, bir Azure AD kullanıcısının Humanity ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="31303-140">In other words, a link relationship between an Azure AD user and the related user in Humanity needs to be established.</span></span>

<span data-ttu-id="31303-141">Humanity içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="31303-141">In Humanity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="31303-142">Yapılandırmak ve Azure AD çoklu oturum açma ile Humanity sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="31303-142">To configure and test Azure AD single sign-on with Humanity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="31303-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="31303-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="31303-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="31303-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="31303-145">**[Humanity test kullanıcısı oluşturma](#creating-a-humanity-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Humanity sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="31303-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - to have a counterpart of Britta Simon in Humanity that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="31303-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="31303-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="31303-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="31303-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="31303-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="31303-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="31303-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Humanity uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="31303-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="31303-150">**Azure AD çoklu oturum açma ile Humanity yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="31303-150">**To configure Azure AD single sign-on with Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="31303-151">Azure portalında üzerinde **Humanity** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="31303-151">In the Azure portal, on the **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="31303-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="31303-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. <span data-ttu-id="31303-155">Üzerinde **Humanity etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="31303-155">On the **Humanity Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="31303-157">a.</span><span class="sxs-lookup"><span data-stu-id="31303-157">a.</span></span> <span data-ttu-id="31303-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://company.humanity.com/includes/saml/`</span><span class="sxs-lookup"><span data-stu-id="31303-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="31303-159">b.</span><span class="sxs-lookup"><span data-stu-id="31303-159">b.</span></span> <span data-ttu-id="31303-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="31303-160">In the **Identifier** textbox, type a URL using the following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="31303-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="31303-161">These values are not real.</span></span> <span data-ttu-id="31303-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="31303-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="31303-163">Kişi [Humanity istemci destek ekibi](https://www.humanity.com/support/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="31303-163">Contact [Humanity Client support team](https://www.humanity.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="31303-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="31303-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. <span data-ttu-id="31303-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="31303-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="31303-168">Üzerinde **Humanity yapılandırma** 'yi tıklatın **yapılandırma Humanity** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="31303-168">On the **Humanity Configuration** section, click **Configure Humanity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="31303-169">Kopya **SAML çoklu oturum açma hizmet URL'si ve Sign-Out URL** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="31303-169">Copy the **SAML Single Sign-On Service URL, and Sign-Out URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. <span data-ttu-id="31303-171">Farklı web tarayıcısı penceresinde oturum açın, **Humanity** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="31303-171">In a different web browser window, log in to your **Humanity** company site as an administrator.</span></span>

8. <span data-ttu-id="31303-172">Üstteki menüde tıklatın **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="31303-172">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="31303-173">![Yönetici](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="31303-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

9. <span data-ttu-id="31303-174">Altında **tümleştirme**, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="31303-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="31303-175">![Çoklu oturum açma](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="31303-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

10. <span data-ttu-id="31303-176">İçinde **çoklu oturum açma** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="31303-176">In the **Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="31303-177">![Çoklu oturum açma](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="31303-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="31303-178">a.</span><span class="sxs-lookup"><span data-stu-id="31303-178">a.</span></span> <span data-ttu-id="31303-179">Seçin **SAML etkin**.</span><span class="sxs-lookup"><span data-stu-id="31303-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="31303-180">b.</span><span class="sxs-lookup"><span data-stu-id="31303-180">b.</span></span> <span data-ttu-id="31303-181">Seçin **parola oturum açma izin**.</span><span class="sxs-lookup"><span data-stu-id="31303-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="31303-182">c.</span><span class="sxs-lookup"><span data-stu-id="31303-182">c.</span></span> <span data-ttu-id="31303-183">Yapıştır **SAML çoklu oturum açma hizmet URL'si** içine değer **SAML veren URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="31303-183">Paste the **SAML Single Sign-On Service URL** value into the **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="31303-184">d.</span><span class="sxs-lookup"><span data-stu-id="31303-184">d.</span></span> <span data-ttu-id="31303-185">Yapıştır **Sign-Out URL** içine değer **uzak oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="31303-185">Paste the **Sign-Out URL** value into the **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="31303-186">e.</span><span class="sxs-lookup"><span data-stu-id="31303-186">e.</span></span> <span data-ttu-id="31303-187">Base-64 kodlanmış sertifikanızı Not Defteri'nde açın, içeriğini, panoya kopyalayın ve yapıştırın kendisine **X.509 sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="31303-187">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>

11. <span data-ttu-id="31303-188">Tıklatın **ayarlarını kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="31303-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="31303-189">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="31303-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="31303-190">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="31303-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="31303-191">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="31303-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="31303-192">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="31303-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="31303-193">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="31303-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="31303-195">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="31303-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="31303-196">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="31303-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="31303-198">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="31303-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="31303-200">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="31303-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="31303-202">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="31303-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="31303-204">a.</span><span class="sxs-lookup"><span data-stu-id="31303-204">a.</span></span> <span data-ttu-id="31303-205">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="31303-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="31303-206">b.</span><span class="sxs-lookup"><span data-stu-id="31303-206">b.</span></span> <span data-ttu-id="31303-207">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="31303-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="31303-208">c.</span><span class="sxs-lookup"><span data-stu-id="31303-208">c.</span></span> <span data-ttu-id="31303-209">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="31303-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="31303-210">d.</span><span class="sxs-lookup"><span data-stu-id="31303-210">d.</span></span> <span data-ttu-id="31303-211">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="31303-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="31303-212">Humanity test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="31303-212">Creating a Humanity test user</span></span>

<span data-ttu-id="31303-213">Azure AD kullanıcıları için Humanity oturum açmak etkinleştirmek için bunların Humanity sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="31303-213">In order to enable Azure AD users to log in to Humanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="31303-214">Humanity söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="31303-214">In the case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="31303-215">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="31303-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="31303-216">Oturum, **Humanity** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="31303-216">Log in to your **Humanity** company site as an administrator.</span></span>

2. <span data-ttu-id="31303-217">Tıklatın **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="31303-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="31303-218">![Yönetici](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="31303-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

3. <span data-ttu-id="31303-219">Tıklatın **personel**.</span><span class="sxs-lookup"><span data-stu-id="31303-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="31303-220">![Personel](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "personel")</span><span class="sxs-lookup"><span data-stu-id="31303-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span></span>

4. <span data-ttu-id="31303-221">Altında **Eylemler**, tıklatın **eklemek çalışanlar**.</span><span class="sxs-lookup"><span data-stu-id="31303-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="31303-222">![Çalışanlar eklemek](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "çalışanları ekleme")</span><span class="sxs-lookup"><span data-stu-id="31303-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

5. <span data-ttu-id="31303-223">İçinde **eklemek çalışanlar** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="31303-223">In the **Add Employees** section, perform the following steps:</span></span>
   
    <span data-ttu-id="31303-224">![Çalışanlar Kaydet](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "çalışanlar Kaydet")</span><span class="sxs-lookup"><span data-stu-id="31303-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="31303-225">a.</span><span class="sxs-lookup"><span data-stu-id="31303-225">a.</span></span> <span data-ttu-id="31303-226">Tür **ad**, **Soyadı**, ve **e-posta** istediğiniz ilgili metin kutularına sağlamayı geçerli bir AAD hesabının.</span><span class="sxs-lookup"><span data-stu-id="31303-226">Type the **First Name**, **Last Name**, and **Email** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="31303-227">b.</span><span class="sxs-lookup"><span data-stu-id="31303-227">b.</span></span> <span data-ttu-id="31303-228">Tıklatın **çalışanlar kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="31303-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="31303-229">API sağlama AAD kullanıcı hesaplarına Humanity tarafından sağlanan veya herhangi diğer Humanity kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31303-229">You can use any other Humanity user account creation tools or APIs provided by Humanity to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="31303-230">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="31303-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="31303-231">Bu bölümde, Britta Humanity için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="31303-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Humanity.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="31303-233">**Humanity için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="31303-233">**To assign Britta Simon to Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="31303-234">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="31303-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="31303-236">Uygulamalar listesinde **Humanity**.</span><span class="sxs-lookup"><span data-stu-id="31303-236">In the applications list, select **Humanity**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. <span data-ttu-id="31303-238">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="31303-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="31303-240">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="31303-240">Click **Add** button.</span></span> <span data-ttu-id="31303-241">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="31303-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="31303-243">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="31303-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="31303-244">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="31303-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="31303-245">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="31303-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="31303-246">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="31303-246">Testing single sign-on</span></span>

<span data-ttu-id="31303-247">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="31303-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="31303-248">Erişim paneli Humanity parçasında tıklattığınızda, otomatik olarak Humanity uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="31303-248">When you click the Humanity tile in the Access Panel, you should get automatically signed-on to your Humanity application.</span></span>
<span data-ttu-id="31303-249">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="31303-249">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="31303-250">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="31303-250">Additional resources</span></span>

* [<span data-ttu-id="31303-251">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="31303-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="31303-252">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="31303-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

