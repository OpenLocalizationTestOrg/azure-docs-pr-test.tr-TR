---
title: "Öğretici: Azure Active Directory Tümleştirme ile Panopto | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Panopto arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 725fba1227cfc9c4850f9e2d6fd0b13e88eafa20
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="740e8-103">Öğretici: Azure Active Directory Tümleştirme Panopto ile</span><span class="sxs-lookup"><span data-stu-id="740e8-103">Tutorial: Azure Active Directory integration with Panopto</span></span>

<span data-ttu-id="740e8-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Panopto tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="740e8-104">In this tutorial, you learn how to integrate Panopto with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="740e8-105">Panopto Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="740e8-105">Integrating Panopto with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="740e8-106">Panopto erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="740e8-106">You can control in Azure AD who has access to Panopto</span></span>
- <span data-ttu-id="740e8-107">Otomatik olarak için Panopto (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="740e8-107">You can enable your users to automatically get signed-on to Panopto (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="740e8-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="740e8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="740e8-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="740e8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="740e8-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="740e8-110">Prerequisites</span></span>

<span data-ttu-id="740e8-111">Azure AD tümleştirme Panopto ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="740e8-111">To configure Azure AD integration with Panopto, you need the following items:</span></span>

- <span data-ttu-id="740e8-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="740e8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="740e8-113">Bir Panopto çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="740e8-113">A Panopto single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="740e8-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="740e8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="740e8-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="740e8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="740e8-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="740e8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="740e8-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="740e8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="740e8-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="740e8-118">Scenario description</span></span>
<span data-ttu-id="740e8-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="740e8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="740e8-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="740e8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="740e8-121">Galeriden Panopto ekleme</span><span class="sxs-lookup"><span data-stu-id="740e8-121">Adding Panopto from the gallery</span></span>
2. <span data-ttu-id="740e8-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="740e8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panopto-from-the-gallery"></a><span data-ttu-id="740e8-123">Galeriden Panopto ekleme</span><span class="sxs-lookup"><span data-stu-id="740e8-123">Adding Panopto from the gallery</span></span>
<span data-ttu-id="740e8-124">Azure AD Panopto tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Panopto eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="740e8-124">To configure the integration of Panopto into Azure AD, you need to add Panopto from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="740e8-125">**Galeriden Panopto eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="740e8-125">**To add Panopto from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="740e8-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="740e8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="740e8-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="740e8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="740e8-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="740e8-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="740e8-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="740e8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="740e8-133">Arama kutusuna **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="740e8-133">In the search box, type **Panopto**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_search.png)

5. <span data-ttu-id="740e8-135">Sonuçlar panelinde seçin **Panopto**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="740e8-135">In the results panel, select **Panopto**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="740e8-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="740e8-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="740e8-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Panopto ile test etme</span><span class="sxs-lookup"><span data-stu-id="740e8-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="740e8-139">Tekli çalışmaya oturum için Azure AD Panopto karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="740e8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Panopto is to a user in Azure AD.</span></span> <span data-ttu-id="740e8-140">Diğer bir deyişle, bir Azure AD kullanıcısının Panopto ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="740e8-140">In other words, a link relationship between an Azure AD user and the related user in Panopto needs to be established.</span></span>

<span data-ttu-id="740e8-141">Panopto içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="740e8-141">In Panopto, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="740e8-142">Yapılandırma ve Azure AD çoklu oturum açma Panopto ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="740e8-142">To configure and test Azure AD single sign-on with Panopto, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="740e8-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="740e8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="740e8-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="740e8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="740e8-145">**[Panopto test kullanıcısı oluşturma](#creating-a-panopto-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Panopto sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="740e8-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - to have a counterpart of Britta Simon in Panopto that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="740e8-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="740e8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="740e8-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="740e8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="740e8-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="740e8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="740e8-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Panopto uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="740e8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Panopto application.</span></span>

<span data-ttu-id="740e8-150">**Azure AD çoklu oturum açma ile Panopto yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="740e8-150">**To configure Azure AD single sign-on with Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="740e8-151">Azure portalında üzerinde **Panopto** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="740e8-151">In the Azure portal, on the **Panopto** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="740e8-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="740e8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_samlbase.png)

3. <span data-ttu-id="740e8-155">Üzerinde **Panopto etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="740e8-155">On the **Panopto Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_url.png)

    <span data-ttu-id="740e8-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<tenant-name>.panopto.com`</span><span class="sxs-lookup"><span data-stu-id="740e8-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.panopto.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="740e8-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="740e8-158">This value is not real.</span></span> <span data-ttu-id="740e8-159">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="740e8-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="740e8-160">Kişi [Panopto istemci destek ekibi](mailto:support@panopto.com‎) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="740e8-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) to get this value.</span></span> 
 
4. <span data-ttu-id="740e8-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="740e8-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_certificate.png) 

5. <span data-ttu-id="740e8-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="740e8-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panopto-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="740e8-165">Üzerinde **Panopto yapılandırma** 'yi tıklatın **yapılandırma Panopto** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="740e8-165">On the **Panopto Configuration** section, click **Configure Panopto** to open **Configure sign-on** window.</span></span> <span data-ttu-id="740e8-166">Kopya **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="740e8-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_configure.png) 

7. <span data-ttu-id="740e8-168">Farklı web tarayıcısı penceresinde Panopto şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="740e8-168">In a different web browser window, log in to your Panopto company site as an administrator.</span></span>

8. <span data-ttu-id="740e8-169">Sol taraftaki araç çubuğunda tıklatın **sistem**ve ardından **kimlik sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="740e8-169">In the toolbar on the left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="740e8-170">![Sistem](./media/active-directory-saas-panopto-tutorial/ic777670.png "sistem")</span><span class="sxs-lookup"><span data-stu-id="740e8-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span></span>
9. <span data-ttu-id="740e8-171">Tıklatın **Sağlayıcı eklemek**.</span><span class="sxs-lookup"><span data-stu-id="740e8-171">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="740e8-172">![Kimlik sağlayıcılar](./media/active-directory-saas-panopto-tutorial/ic777671.png "kimlik sağlayıcıları")</span><span class="sxs-lookup"><span data-stu-id="740e8-172">![Identity Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "Identity Providers")</span></span>
   
10. <span data-ttu-id="740e8-173">SAML sağlayıcısı bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="740e8-173">In the SAML provider section, perform the following steps:</span></span>
   
    <span data-ttu-id="740e8-174">![SaaS yapılandırma](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS yapılandırma")</span><span class="sxs-lookup"><span data-stu-id="740e8-174">![SaaS configuration](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS configuration")</span></span>
    
    <span data-ttu-id="740e8-175">a.</span><span class="sxs-lookup"><span data-stu-id="740e8-175">a.</span></span> <span data-ttu-id="740e8-176">Gelen **sağlayıcı türü** listesinde **SAML20**.</span><span class="sxs-lookup"><span data-stu-id="740e8-176">From the **Provider Type** list, select **SAML20**.</span></span>    
    
    <span data-ttu-id="740e8-177">b.</span><span class="sxs-lookup"><span data-stu-id="740e8-177">b.</span></span> <span data-ttu-id="740e8-178">İçinde **örnek adı** metin kutusuna, örnek için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="740e8-178">In the **Instance Name** textbox, type a name for the instance.</span></span>

    <span data-ttu-id="740e8-179">c.</span><span class="sxs-lookup"><span data-stu-id="740e8-179">c.</span></span> <span data-ttu-id="740e8-180">İçinde **anlaşılır bir açıklama** metin kutusuna, kolay bir açıklama yazın.</span><span class="sxs-lookup"><span data-stu-id="740e8-180">In the **Friendly Description** textbox, type a friendly description.</span></span>
    
    <span data-ttu-id="740e8-181">d.</span><span class="sxs-lookup"><span data-stu-id="740e8-181">d.</span></span> <span data-ttu-id="740e8-182">İçinde **Sıçrama sayfa URL'si** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="740e8-182">In **Bounce Page Url** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="740e8-183">e.</span><span class="sxs-lookup"><span data-stu-id="740e8-183">e.</span></span> <span data-ttu-id="740e8-184">İçinde **veren** metin değerini yapıştırın **SAML varlık kimliği**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="740e8-184">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="740e8-185">f.</span><span class="sxs-lookup"><span data-stu-id="740e8-185">f.</span></span> <span data-ttu-id="740e8-186">Azure portalından indirmiş, base-64 kodlanmış sertifika açmak içinde içeriğini panonuza kopyalayın ve yapıştırın kendisine **ortak anahtar** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="740e8-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy the content of it in to your clipboard, and then paste it to the **Public Key**  textbox.</span></span>

11. <span data-ttu-id="740e8-187">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="740e8-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="740e8-188">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="740e8-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="740e8-189">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="740e8-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="740e8-190">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="740e8-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="740e8-191">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="740e8-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="740e8-192">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="740e8-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="740e8-194">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="740e8-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="740e8-195">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="740e8-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panopto-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="740e8-197">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="740e8-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panopto-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="740e8-199">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="740e8-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panopto-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="740e8-201">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="740e8-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panopto-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="740e8-203">a.</span><span class="sxs-lookup"><span data-stu-id="740e8-203">a.</span></span> <span data-ttu-id="740e8-204">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="740e8-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="740e8-205">b.</span><span class="sxs-lookup"><span data-stu-id="740e8-205">b.</span></span> <span data-ttu-id="740e8-206">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="740e8-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="740e8-207">c.</span><span class="sxs-lookup"><span data-stu-id="740e8-207">c.</span></span> <span data-ttu-id="740e8-208">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="740e8-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="740e8-209">d.</span><span class="sxs-lookup"><span data-stu-id="740e8-209">d.</span></span> <span data-ttu-id="740e8-210">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="740e8-210">Click **Create**.</span></span>
 
### <a name="creating-a-panopto-test-user"></a><span data-ttu-id="740e8-211">Panopto test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="740e8-211">Creating a Panopto test user</span></span>

<span data-ttu-id="740e8-212">Kullanıcı için Panopto hazırlama yapılandırmanız için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="740e8-212">There is no action item for you to configure user provisioning to Panopto.</span></span>  
<span data-ttu-id="740e8-213">Atanmış bir kullanıcı erişim paneli kullanılarak Panopto için oturum açma girişiminde bulunduğunda, Panopto kullanıcının var olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="740e8-213">When an assigned user tries to log in to Panopto using the access panel, Panopto checks whether the user exists.</span></span>  

<span data-ttu-id="740e8-214">Hiçbir kullanıcı hesabı varsa kullanılabilir henüz, Panopto tarafından otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="740e8-214">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="740e8-215">API Azure AD kullanıcı hesaplarını sağlamak için Panopto tarafından sağlanan veya herhangi diğer Panopto kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="740e8-215">You can use any other Panopto user account creation tools or APIs provided by Panopto to provision Azure AD user accounts.</span></span>
>
>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="740e8-216">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="740e8-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="740e8-217">Bu bölümde, Britta Panopto için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="740e8-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Panopto.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="740e8-219">**Panopto için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="740e8-219">**To assign Britta Simon to Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="740e8-220">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="740e8-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="740e8-222">Uygulamalar listesinde **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="740e8-222">In the applications list, select **Panopto**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_app.png) 

3. <span data-ttu-id="740e8-224">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="740e8-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="740e8-226">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="740e8-226">Click **Add** button.</span></span> <span data-ttu-id="740e8-227">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="740e8-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="740e8-229">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="740e8-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="740e8-230">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="740e8-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="740e8-231">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="740e8-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="740e8-232">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="740e8-232">Testing single sign-on</span></span>

<span data-ttu-id="740e8-233">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="740e8-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="740e8-234">Erişim paneli Panopto parçasında tıkladığınızda, oturum açma sayfasına Panopto uygulamasının otomatik olarak almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="740e8-234">When you click the Panopto tile in the Access Panel, you should get automatically login page of Panopto application.</span></span>
<span data-ttu-id="740e8-235">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="740e8-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="740e8-236">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="740e8-236">Additional resources</span></span>

* [<span data-ttu-id="740e8-237">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="740e8-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="740e8-238">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="740e8-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_203.png

