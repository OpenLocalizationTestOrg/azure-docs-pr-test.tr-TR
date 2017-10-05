---
title: "Öğretici: Azure Active Directory Tümleştirme yakınlaştırma ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve yakınlaştırma arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: aab491f162fd4d24c6ff4d8858f2edd96dda30d4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a><span data-ttu-id="b57a3-103">Öğretici: Yakınlaştırma Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="b57a3-103">Tutorial: Azure Active Directory integration with Zoom</span></span>

<span data-ttu-id="b57a3-104">Bu öğreticide, Azure Active Directory (Azure AD) ile yakınlaştırma tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="b57a3-104">In this tutorial, you learn how to integrate Zoom with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b57a3-105">Yakınlaştırma Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="b57a3-105">Integrating Zoom with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b57a3-106">Yakınlaştırma erişimi, Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b57a3-106">You can control in Azure AD who has access to Zoom.</span></span>
- <span data-ttu-id="b57a3-107">Otomatik olarak (çoklu oturum açma) yakınlaştırmak için Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b57a3-107">You can enable your users to automatically get signed-on to Zoom (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b57a3-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="b57a3-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b57a3-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b57a3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b57a3-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b57a3-110">Prerequisites</span></span>

<span data-ttu-id="b57a3-111">Azure AD tümleştirme yakınlaştırma ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="b57a3-111">To configure Azure AD integration with Zoom, you need the following items:</span></span>

- <span data-ttu-id="b57a3-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="b57a3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b57a3-113">Bir yakınlaştırma çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="b57a3-113">A Zoom single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b57a3-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="b57a3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b57a3-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b57a3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b57a3-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="b57a3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b57a3-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b57a3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b57a3-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="b57a3-118">Scenario description</span></span>
<span data-ttu-id="b57a3-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="b57a3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b57a3-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="b57a3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b57a3-121">Galeriden yakınlaştırma ekleme</span><span class="sxs-lookup"><span data-stu-id="b57a3-121">Adding Zoom from the gallery</span></span>
2. <span data-ttu-id="b57a3-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="b57a3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoom-from-the-gallery"></a><span data-ttu-id="b57a3-123">Galeriden yakınlaştırma ekleme</span><span class="sxs-lookup"><span data-stu-id="b57a3-123">Adding Zoom from the gallery</span></span>
<span data-ttu-id="b57a3-124">Azure AD'ye yakınlaştırma tümleştirmesini yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden yakınlaştırma eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b57a3-124">To configure the integration of Zoom into Azure AD, you need to add Zoom from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b57a3-125">**Yakınlaştırma Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b57a3-125">**To add Zoom from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b57a3-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b57a3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="b57a3-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="b57a3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b57a3-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b57a3-129">Then go to **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="b57a3-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b57a3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="b57a3-133">Arama kutusuna **yakınlaştırma**seçin **yakınlaştırma** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="b57a3-133">In the search box, type **Zoom**, select **Zoom** from result panel then click **Add** button to add the application.</span></span>

    ![Sonuçlar listesinde Yakınlaştır](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b57a3-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="b57a3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b57a3-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı yakınlaştırma ile test etme.</span><span class="sxs-lookup"><span data-stu-id="b57a3-136">In this section, you configure and test Azure AD single sign-on with Zoom based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b57a3-137">Tekli çalışmaya oturum için Azure AD yakınlaştırma karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="b57a3-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoom is to a user in Azure AD.</span></span> <span data-ttu-id="b57a3-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve yakınlaştırma ilgili kullanıcı arasındaki bağlantıyı ilişki kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b57a3-138">In other words, a link relationship between an Azure AD user and the related user in Zoom needs to be established.</span></span>

<span data-ttu-id="b57a3-139">Yakınlaştırma, değeri atamak **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="b57a3-139">In Zoom, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b57a3-140">Yapılandırma ve Azure AD çoklu oturum açma yakınlaştırma ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b57a3-140">To configure and test Azure AD single sign-on with Zoom, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b57a3-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="b57a3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b57a3-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="b57a3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b57a3-143">**[Yakınlaştırma test kullanıcısı oluşturma](#create-a-zoom-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı yakınlaştırma sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="b57a3-143">**[Create a Zoom test user](#create-a-zoom-test-user)** - to have a counterpart of Britta Simon in Zoom that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b57a3-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="b57a3-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b57a3-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b57a3-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b57a3-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="b57a3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b57a3-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma yakınlaştırma uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b57a3-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoom application.</span></span>

<span data-ttu-id="b57a3-148">**Azure AD çoklu oturum açma ile yakınlaştırma yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b57a3-148">**To configure Azure AD single sign-on with Zoom, perform the following steps:**</span></span>

1. <span data-ttu-id="b57a3-149">Azure portalında üzerinde **yakınlaştırma** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="b57a3-149">In the Azure portal, on the **Zoom** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="b57a3-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="b57a3-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_samlbase.png)

3. <span data-ttu-id="b57a3-153">Üzerinde **yakınlaştırma etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b57a3-153">On the **Zoom Domain and URLs** section, perform the following steps:</span></span>

    ![Etki alanı ve URL'leri tek oturum açma bilgilerini Yakınlaştır](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_url.png)

    <span data-ttu-id="b57a3-155">a.</span><span class="sxs-lookup"><span data-stu-id="b57a3-155">a.</span></span> <span data-ttu-id="b57a3-156">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="b57a3-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.zoom.us`</span></span>

    <span data-ttu-id="b57a3-157">b.</span><span class="sxs-lookup"><span data-stu-id="b57a3-157">b.</span></span> <span data-ttu-id="b57a3-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="b57a3-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.zoom.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b57a3-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="b57a3-159">These values are not real.</span></span> <span data-ttu-id="b57a3-160">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="b57a3-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b57a3-161">Kişi [yakınlaştırma istemci destek ekibi](https://support.zoom.us/hc) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="b57a3-161">Contact [Zoom Client support team](https://support.zoom.us/hc) to get these values.</span></span> 
 
4. <span data-ttu-id="b57a3-162">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b57a3-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_certificate.png) 

5. <span data-ttu-id="b57a3-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b57a3-164">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-zoom-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b57a3-166">Üzerinde **yakınlaştırma yapılandırma** 'yi tıklatın **yapılandırma yakınlaştırma** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="b57a3-166">On the **Zoom Configuration** section, click **Configure Zoom** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b57a3-167">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="b57a3-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Yakınlaştırma yapılandırma](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_configure.png) 

7. <span data-ttu-id="b57a3-169">Farklı web tarayıcısı penceresinde yakınlaştırma şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b57a3-169">In a different web browser window, log in to your Zoom company site as an administrator.</span></span>

8. <span data-ttu-id="b57a3-170">Tıklatın **çoklu oturum açma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="b57a3-170">Click the **Single Sign-On** tab.</span></span>
   
    <span data-ttu-id="b57a3-171">![Oturum açma tek sekme](./media/active-directory-saas-zoom-tutorial/IC784700.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="b57a3-171">![Single sign-on tab](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span></span>

9. <span data-ttu-id="b57a3-172">Tıklatın **güvenlik denetimi** sekmesini tıklatın ve ardından Git **çoklu oturum açma** ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b57a3-172">Click the **Security Control** tab, and then go to the **Single Sign-On** settings.</span></span>

10. <span data-ttu-id="b57a3-173">Çoklu oturum açma bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b57a3-173">In the Single Sign-On section, perform the following steps:</span></span>
   
    <span data-ttu-id="b57a3-174">![Çoklu oturum açma bölüm](./media/active-directory-saas-zoom-tutorial/IC784701.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="b57a3-174">![Single sign-on section](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span></span>
   
    <span data-ttu-id="b57a3-175">a.</span><span class="sxs-lookup"><span data-stu-id="b57a3-175">a.</span></span> <span data-ttu-id="b57a3-176">İçinde **oturum açma sayfası URL'si** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="b57a3-176">In the **Sign-in page URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="b57a3-177">b.</span><span class="sxs-lookup"><span data-stu-id="b57a3-177">b.</span></span> <span data-ttu-id="b57a3-178">İçinde **oturum kapatma sayfası URL'si** metin değerini yapıştırın **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="b57a3-178">In the **Sign-out page URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
     
    <span data-ttu-id="b57a3-179">c.</span><span class="sxs-lookup"><span data-stu-id="b57a3-179">c.</span></span> <span data-ttu-id="b57a3-180">Base-64 kodlanmış sertifikanızı Not Defteri'nde açın, içeriğini, panoya kopyalayın ve yapıştırın kendisine **kimlik sağlayıcısı sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="b57a3-180">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span></span>

    <span data-ttu-id="b57a3-181">d.</span><span class="sxs-lookup"><span data-stu-id="b57a3-181">d.</span></span> <span data-ttu-id="b57a3-182">İçinde **veren** metin değerini yapıştırın **SAML varlık kimliği**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="b57a3-182">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="b57a3-183">e.</span><span class="sxs-lookup"><span data-stu-id="b57a3-183">e.</span></span> <span data-ttu-id="b57a3-184">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b57a3-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b57a3-185">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="b57a3-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b57a3-186">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="b57a3-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b57a3-187">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b57a3-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b57a3-188">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b57a3-188">Create an Azure AD test user</span></span>

<span data-ttu-id="b57a3-189">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="b57a3-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="b57a3-191">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b57a3-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b57a3-192">Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b57a3-192">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-zoom-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b57a3-194">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="b57a3-194">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-zoom-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b57a3-196">Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="b57a3-196">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Ekle düğmesi](./media/active-directory-saas-zoom-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b57a3-198">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b57a3-198">In the **User** dialog box, perform the following steps:</span></span>

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-zoom-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b57a3-200">a.</span><span class="sxs-lookup"><span data-stu-id="b57a3-200">a.</span></span> <span data-ttu-id="b57a3-201">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b57a3-201">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b57a3-202">b.</span><span class="sxs-lookup"><span data-stu-id="b57a3-202">b.</span></span> <span data-ttu-id="b57a3-203">İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="b57a3-203">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b57a3-204">c.</span><span class="sxs-lookup"><span data-stu-id="b57a3-204">c.</span></span> <span data-ttu-id="b57a3-205">Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="b57a3-205">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b57a3-206">d.</span><span class="sxs-lookup"><span data-stu-id="b57a3-206">d.</span></span> <span data-ttu-id="b57a3-207">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b57a3-207">Click **Create**.</span></span>
 
### <a name="create-a-zoom-test-user"></a><span data-ttu-id="b57a3-208">Yakınlaştırma test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b57a3-208">Create a Zoom test user</span></span>

<span data-ttu-id="b57a3-209">Yakınlaştırma için oturum açmak Azure AD kullanıcıları etkinleştirmek için bunların yakınlaştırma sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b57a3-209">In order to enable Azure AD users to log in to Zoom, they must be provisioned into Zoom.</span></span> <span data-ttu-id="b57a3-210">Yakınlaştırma söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="b57a3-210">In the case of Zoom, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="b57a3-211">Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b57a3-211">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="b57a3-212">Oturum, **yakınlaştırma** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="b57a3-212">Log in to your **Zoom** company site as an administrator.</span></span>
 
2. <span data-ttu-id="b57a3-213">Tıklatın **hesap yönetimi** sekmesini ve ardından **kullanıcı yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="b57a3-213">Click the **Account Management** tab, and then click **User Management**.</span></span>

3. <span data-ttu-id="b57a3-214">Kullanıcı Yönetimi bölümünde tıklayın **kullanıcıları eklemek**.</span><span class="sxs-lookup"><span data-stu-id="b57a3-214">In the User Management section, click **Add users**.</span></span>
   
    <span data-ttu-id="b57a3-215">![Kullanıcı Yönetimi](./media/active-directory-saas-zoom-tutorial/IC784703.png "kullanıcı yönetimi")</span><span class="sxs-lookup"><span data-stu-id="b57a3-215">![User management](./media/active-directory-saas-zoom-tutorial/IC784703.png "User management")</span></span>

4. <span data-ttu-id="b57a3-216">Üzerinde **kullanıcıları eklemek** sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b57a3-216">On the **Add users** page, perform the following steps:</span></span>
   
    <span data-ttu-id="b57a3-217">![Kullanıcıları ekleme](./media/active-directory-saas-zoom-tutorial/IC784704.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="b57a3-217">![Add users](./media/active-directory-saas-zoom-tutorial/IC784704.png "Add users")</span></span>
   
    <span data-ttu-id="b57a3-218">a.</span><span class="sxs-lookup"><span data-stu-id="b57a3-218">a.</span></span> <span data-ttu-id="b57a3-219">Olarak **kullanıcı türü**seçin **temel**.</span><span class="sxs-lookup"><span data-stu-id="b57a3-219">As **User Type**, select **Basic**.</span></span>

    <span data-ttu-id="b57a3-220">b.</span><span class="sxs-lookup"><span data-stu-id="b57a3-220">b.</span></span> <span data-ttu-id="b57a3-221">İçinde **e-postaları** metin kutusuna, türü e-posta adresi geçerli bir Azure ad hesabına sağlamak istiyor.</span><span class="sxs-lookup"><span data-stu-id="b57a3-221">In the **Emails** textbox, type the email address of a valid Azure AD account you want to provision.</span></span>

    <span data-ttu-id="b57a3-222">c.</span><span class="sxs-lookup"><span data-stu-id="b57a3-222">c.</span></span> <span data-ttu-id="b57a3-223">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b57a3-223">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="b57a3-224">Kullanıcı hesapları sağlama Azure Active Directory yakınlaştırma API'leri sağladığı veya herhangi diğer yakınlaştırma kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b57a3-224">You can use any other Zoom user account creation tools or APIs provided by Zoom to provision Azure Active Directory user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b57a3-225">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="b57a3-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="b57a3-226">Bu bölümde, Britta yakınlaştırmak için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="b57a3-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoom.</span></span>

![Kullanıcı rolü atayın][200] 

<span data-ttu-id="b57a3-228">**Yakınlaştırma için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b57a3-228">**To assign Britta Simon to Zoom, perform the following steps:**</span></span>

1. <span data-ttu-id="b57a3-229">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b57a3-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="b57a3-231">Uygulamalar listesinde **yakınlaştırma**.</span><span class="sxs-lookup"><span data-stu-id="b57a3-231">In the applications list, select **Zoom**.</span></span>

    ![Uygulamalar listesinde yakınlaştırma bağlantı](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_app.png)  

3. <span data-ttu-id="b57a3-233">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="b57a3-233">In the menu on the left, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="b57a3-235">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b57a3-235">Click **Add** button.</span></span> <span data-ttu-id="b57a3-236">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b57a3-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="b57a3-238">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="b57a3-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b57a3-239">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b57a3-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b57a3-240">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b57a3-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b57a3-241">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="b57a3-241">Test single sign-on</span></span>

<span data-ttu-id="b57a3-242">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="b57a3-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b57a3-243">Erişim paneli yakınlaştırma parçasında tıklattığınızda, otomatik olarak yakınlaştırma uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="b57a3-243">When you click the Zoom tile in the Access Panel, you should get automatically signed-on to your Zoom application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b57a3-244">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b57a3-244">Additional resources</span></span>

* [<span data-ttu-id="b57a3-245">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="b57a3-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b57a3-246">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="b57a3-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_203.png

