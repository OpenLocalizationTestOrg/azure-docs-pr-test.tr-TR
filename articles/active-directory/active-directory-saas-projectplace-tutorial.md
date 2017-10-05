---
title: "Öğretici: Azure Active Directory Tümleştirme ile Projectplace | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Projectplace arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 298059ca-b652-4577-916a-c31393d53d7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: bb9dd10c887cb0e42e544066d9b0dcfa554e10ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-projectplace"></a><span data-ttu-id="c532c-103">Öğretici: Azure Active Directory Tümleştirme Projectplace ile</span><span class="sxs-lookup"><span data-stu-id="c532c-103">Tutorial: Azure Active Directory integration with Projectplace</span></span>

<span data-ttu-id="c532c-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Projectplace tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c532c-104">In this tutorial, you learn how to integrate Projectplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c532c-105">Projectplace Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="c532c-105">Integrating Projectplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c532c-106">Projectplace erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c532c-106">You can control in Azure AD who has access to Projectplace</span></span>
- <span data-ttu-id="c532c-107">Otomatik olarak için Projectplace (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c532c-107">You can enable your users to automatically get signed-on to Projectplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c532c-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="c532c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c532c-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c532c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c532c-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c532c-110">Prerequisites</span></span>

<span data-ttu-id="c532c-111">Azure AD tümleştirme Projectplace ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="c532c-111">To configure Azure AD integration with Projectplace, you need the following items:</span></span>

- <span data-ttu-id="c532c-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="c532c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c532c-113">Bir Projectplace çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="c532c-113">A Projectplace single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c532c-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="c532c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c532c-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c532c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c532c-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c532c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c532c-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c532c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c532c-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="c532c-118">Scenario description</span></span>
<span data-ttu-id="c532c-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="c532c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c532c-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="c532c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c532c-121">Galeriden Projectplace ekleme</span><span class="sxs-lookup"><span data-stu-id="c532c-121">Adding Projectplace from the gallery</span></span>
2. <span data-ttu-id="c532c-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c532c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-projectplace-from-the-gallery"></a><span data-ttu-id="c532c-123">Galeriden Projectplace ekleme</span><span class="sxs-lookup"><span data-stu-id="c532c-123">Adding Projectplace from the gallery</span></span>
<span data-ttu-id="c532c-124">Azure AD Projectplace tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Projectplace eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c532c-124">To configure the integration of Projectplace into Azure AD, you need to add Projectplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c532c-125">**Galeriden Projectplace eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c532c-125">**To add Projectplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c532c-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c532c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c532c-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="c532c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c532c-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c532c-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="c532c-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c532c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="c532c-133">Arama kutusuna **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="c532c-133">In the search box, type **Projectplace**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_search.png)

5. <span data-ttu-id="c532c-135">Sonuçlar panelinde seçin **Projectplace**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c532c-135">In the results panel, select **Projectplace**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c532c-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c532c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c532c-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Projectplace sınayın.</span><span class="sxs-lookup"><span data-stu-id="c532c-138">In this section, you configure and test Azure AD single sign-on with Projectplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c532c-139">Tekli çalışmaya oturum için Azure AD Projectplace karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="c532c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Projectplace is to a user in Azure AD.</span></span> <span data-ttu-id="c532c-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve Projectplace ilgili kullanıcı arasındaki bağlantıyı ilişki kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c532c-140">In other words, a link relationship between an Azure AD user and the related user in Projectplace needs to be established.</span></span>

<span data-ttu-id="c532c-141">Projectplace içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="c532c-141">In Projectplace, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c532c-142">Yapılandırma ve Azure AD çoklu oturum açma Projectplace ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c532c-142">To configure and test Azure AD single sign-on with Projectplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c532c-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c532c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c532c-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="c532c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c532c-145">**[Projectplace test kullanıcısı oluşturma](#creating-a-projectplace-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Projectplace sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="c532c-145">**[Creating a Projectplace test user](#creating-a-projectplace-test-user)** - to have a counterpart of Britta Simon in Projectplace that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c532c-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c532c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c532c-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c532c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c532c-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c532c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c532c-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Projectplace uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c532c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Projectplace application.</span></span>

<span data-ttu-id="c532c-150">**Azure AD çoklu oturum açma ile Projectplace yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c532c-150">**To configure Azure AD single sign-on with Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="c532c-151">Azure portalında üzerinde **Projectplace** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c532c-151">In the Azure portal, on the **Projectplace** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="c532c-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c532c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_samlbase.png)

3. <span data-ttu-id="c532c-155">Üzerinde **Projectplace etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c532c-155">On the **Projectplace Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_url.png)

    <span data-ttu-id="c532c-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company>.projectplace.com`</span><span class="sxs-lookup"><span data-stu-id="c532c-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.projectplace.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c532c-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="c532c-158">This value is not real.</span></span> <span data-ttu-id="c532c-159">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c532c-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="c532c-160">Kişi [Projectplace istemci destek ekibi](https://success.planview.com/Projectplace/Support) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="c532c-160">Contact [Projectplace Client support team](https://success.planview.com/Projectplace/Support) to get this value.</span></span> 
 
4. <span data-ttu-id="c532c-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c532c-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_certificate.png) 

5. <span data-ttu-id="c532c-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c532c-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-projectplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="c532c-165">Çoklu oturum açma yapılandırmak için **Projectplace** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [Projectplace destek ekibi](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="c532c-165">To configure single sign-on on **Projectplace** side, you need to send the downloaded **Metadata XML** to [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="c532c-166">Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c532c-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="c532c-167">Tek oturum açma tarafından gerçekleştirilmek üzere yapılandırılmış [Projectplace destek ekibi](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="c532c-167">The single sign-on configuration has to be performed by the [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="c532c-168">Yapılandırma tamamlandıktan hemen sonra bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="c532c-168">You will get a notification as soon as the configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="c532c-169">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="c532c-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c532c-170">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="c532c-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c532c-171">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c532c-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c532c-172">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c532c-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="c532c-173">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="c532c-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="c532c-175">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c532c-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c532c-176">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c532c-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-projectplace-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c532c-178">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c532c-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-projectplace-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c532c-180">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="c532c-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-projectplace-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c532c-182">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c532c-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-projectplace-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c532c-184">a.</span><span class="sxs-lookup"><span data-stu-id="c532c-184">a.</span></span> <span data-ttu-id="c532c-185">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c532c-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c532c-186">b.</span><span class="sxs-lookup"><span data-stu-id="c532c-186">b.</span></span> <span data-ttu-id="c532c-187">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="c532c-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c532c-188">c.</span><span class="sxs-lookup"><span data-stu-id="c532c-188">c.</span></span> <span data-ttu-id="c532c-189">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="c532c-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c532c-190">d.</span><span class="sxs-lookup"><span data-stu-id="c532c-190">d.</span></span> <span data-ttu-id="c532c-191">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c532c-191">Click **Create**.</span></span>
 
### <a name="creating-a-projectplace-test-user"></a><span data-ttu-id="c532c-192">Projectplace test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c532c-192">Creating a Projectplace test user</span></span>

<span data-ttu-id="c532c-193">Azure AD kullanıcıların Projectplace oturum etkinleştirmek için bunların Projectplace sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c532c-193">In order to enable Azure AD users to log into Projectplace, they must be provisioned into Projectplace.</span></span> <span data-ttu-id="c532c-194">Projectplace söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="c532c-194">In the case of Projectplace, provisioning is a manual task.</span></span>

<span data-ttu-id="c532c-195">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c532c-195">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c532c-196">Oturum, **Projectplace** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="c532c-196">Log in to your **Projectplace** company site as an administrator.</span></span>

2. <span data-ttu-id="c532c-197">Git **kişiler**ve ardından **üyeleri**.</span><span class="sxs-lookup"><span data-stu-id="c532c-197">Go to **People**, and then click **Members**.</span></span>
   
    <span data-ttu-id="c532c-198">![Kişiler](./media/active-directory-saas-projectplace-tutorial/ic790228.png "kişiler")</span><span class="sxs-lookup"><span data-stu-id="c532c-198">![People](./media/active-directory-saas-projectplace-tutorial/ic790228.png "People")</span></span>

3. <span data-ttu-id="c532c-199">Tıklatın **üye ekleme**.</span><span class="sxs-lookup"><span data-stu-id="c532c-199">Click **Add Member**.</span></span>
   
    <span data-ttu-id="c532c-200">![Üye eklemek](./media/active-directory-saas-projectplace-tutorial/ic790232.png "üyeleri Ekle")</span><span class="sxs-lookup"><span data-stu-id="c532c-200">![Add Members](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Add Members")</span></span>

4. <span data-ttu-id="c532c-201">İçinde **Üye Ekle** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c532c-201">In the **Add Member** section, perform the following steps:</span></span>
   
    <span data-ttu-id="c532c-202">![Yeni üyeler](./media/active-directory-saas-projectplace-tutorial/ic790233.png "yeni üyeler")</span><span class="sxs-lookup"><span data-stu-id="c532c-202">![New Members](./media/active-directory-saas-projectplace-tutorial/ic790233.png "New Members")</span></span>
   
    <span data-ttu-id="c532c-203">a.</span><span class="sxs-lookup"><span data-stu-id="c532c-203">a.</span></span> <span data-ttu-id="c532c-204">İçinde **yeni üyeler** metin kutusuna, istediğiniz ilgili metin kutularına sağlamayı geçerli bir AAD hesabıyla e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="c532c-204">In the **New Members** textbox, type the email address of a valid AAD account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="c532c-205">b.</span><span class="sxs-lookup"><span data-stu-id="c532c-205">b.</span></span> <span data-ttu-id="c532c-206">Tıklatın **Gönder**.</span><span class="sxs-lookup"><span data-stu-id="c532c-206">Click **Send**.</span></span>

   <span data-ttu-id="c532c-207">Azure Active Directory hesap sahibi için etkin hale önce hesabı onaylamak için bir bağlantı içeren bir e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="c532c-207">An email including a link to confirm the account before it becomes active is sent to the Azure Active Directory account holder.</span></span>

>[!NOTE]
><span data-ttu-id="c532c-208">API sağlama AAD kullanıcı hesaplarına Projectplace tarafından sağlanan veya herhangi diğer Projectplace kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c532c-208">You can use any other Projectplace user account creation tools or APIs provided by Projectplace to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c532c-209">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="c532c-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c532c-210">Bu bölümde, Britta Projectplace için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c532c-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Projectplace.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="c532c-212">**Projectplace için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c532c-212">**To assign Britta Simon to Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="c532c-213">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c532c-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="c532c-215">Uygulamalar listesinde **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="c532c-215">In the applications list, select **Projectplace**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_app.png) 

3. <span data-ttu-id="c532c-217">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c532c-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="c532c-219">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c532c-219">Click **Add** button.</span></span> <span data-ttu-id="c532c-220">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c532c-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="c532c-222">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="c532c-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c532c-223">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c532c-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c532c-224">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c532c-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c532c-225">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="c532c-225">Testing single sign-on</span></span>

<span data-ttu-id="c532c-226">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="c532c-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c532c-227">Erişim paneli Projectplace parçasında tıklattığınızda, otomatik olarak Projectplace uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="c532c-227">When you click the Projectplace tile in the Access Panel, you should get automatically signed-on to your Projectplace application.</span></span>
<span data-ttu-id="c532c-228">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c532c-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c532c-229">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c532c-229">Additional resources</span></span>

* [<span data-ttu-id="c532c-230">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="c532c-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c532c-231">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="c532c-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_203.png

