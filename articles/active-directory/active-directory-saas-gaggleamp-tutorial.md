---
title: "Öğretici: Azure Active Directory Tümleştirme ile GaggleAMP | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile GaggleAMP arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9cc1a4b7-964b-406b-9e0c-05cb1a7c9856
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: c591cf99aecc4153e378c42a530b80deeca63158
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gaggleamp"></a><span data-ttu-id="c52c3-103">Öğretici: Azure Active Directory Tümleştirme GaggleAMP ile</span><span class="sxs-lookup"><span data-stu-id="c52c3-103">Tutorial: Azure Active Directory integration with GaggleAMP</span></span>

<span data-ttu-id="c52c3-104">Bu öğreticide, Azure Active Directory (Azure AD) ile GaggleAMP tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c52c3-104">In this tutorial, you learn how to integrate GaggleAMP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c52c3-105">GaggleAMP Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="c52c3-105">Integrating GaggleAMP with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c52c3-106">GaggleAMP erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c52c3-106">You can control in Azure AD who has access to GaggleAMP</span></span>
- <span data-ttu-id="c52c3-107">Otomatik olarak için GaggleAMP (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c52c3-107">You can enable your users to automatically get signed-on to GaggleAMP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c52c3-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="c52c3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c52c3-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c52c3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c52c3-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c52c3-110">Prerequisites</span></span>

<span data-ttu-id="c52c3-111">Azure AD tümleştirme GaggleAMP ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="c52c3-111">To configure Azure AD integration with GaggleAMP, you need the following items:</span></span>

- <span data-ttu-id="c52c3-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="c52c3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c52c3-113">Bir GaggleAMP çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="c52c3-113">A GaggleAMP single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c52c3-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="c52c3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c52c3-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c52c3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c52c3-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c52c3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c52c3-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c52c3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c52c3-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="c52c3-118">Scenario description</span></span>
<span data-ttu-id="c52c3-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="c52c3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c52c3-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="c52c3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c52c3-121">Galeriden GaggleAMP ekleme</span><span class="sxs-lookup"><span data-stu-id="c52c3-121">Adding GaggleAMP from the gallery</span></span>
2. <span data-ttu-id="c52c3-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c52c3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gaggleamp-from-the-gallery"></a><span data-ttu-id="c52c3-123">Galeriden GaggleAMP ekleme</span><span class="sxs-lookup"><span data-stu-id="c52c3-123">Adding GaggleAMP from the gallery</span></span>
<span data-ttu-id="c52c3-124">Azure AD GaggleAMP tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden GaggleAMP eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c52c3-124">To configure the integration of GaggleAMP into Azure AD, you need to add GaggleAMP from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c52c3-125">**Galeriden GaggleAMP eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c52c3-125">**To add GaggleAMP from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c52c3-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c52c3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c52c3-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="c52c3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c52c3-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c52c3-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="c52c3-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c52c3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="c52c3-133">Arama kutusuna **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="c52c3-133">In the search box, type **GaggleAMP**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_search.png)

5. <span data-ttu-id="c52c3-135">Sonuçlar panelinde seçin **GaggleAMP**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c52c3-135">In the results panel, select **GaggleAMP**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c52c3-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c52c3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c52c3-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı GaggleAMP sınayın.</span><span class="sxs-lookup"><span data-stu-id="c52c3-138">In this section, you configure and test Azure AD single sign-on with GaggleAMP based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c52c3-139">Tekli çalışmaya oturum için Azure AD GaggleAMP karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="c52c3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in GaggleAMP is to a user in Azure AD.</span></span> <span data-ttu-id="c52c3-140">Diğer bir deyişle, bir Azure AD kullanıcısının GaggleAMP ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c52c3-140">In other words, a link relationship between an Azure AD user and the related user in GaggleAMP needs to be established.</span></span>

<span data-ttu-id="c52c3-141">GaggleAMP içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="c52c3-141">In GaggleAMP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c52c3-142">Yapılandırma ve Azure AD çoklu oturum açma GaggleAMP ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c52c3-142">To configure and test Azure AD single sign-on with GaggleAMP, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c52c3-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c52c3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c52c3-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="c52c3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c52c3-145">**[GaggleAMP test kullanıcısı oluşturma](#creating-a-gaggleamp-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı GaggleAMP sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="c52c3-145">**[Creating a GaggleAMP test user](#creating-a-gaggleamp-test-user)** - to have a counterpart of Britta Simon in GaggleAMP that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c52c3-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c52c3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c52c3-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c52c3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c52c3-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c52c3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c52c3-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma GaggleAMP uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c52c3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your GaggleAMP application.</span></span>

<span data-ttu-id="c52c3-150">**Azure AD çoklu oturum açma ile GaggleAMP yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c52c3-150">**To configure Azure AD single sign-on with GaggleAMP, perform the following steps:**</span></span>

1. <span data-ttu-id="c52c3-151">Azure portalında üzerinde **GaggleAMP** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c52c3-151">In the Azure portal, on the **GaggleAMP** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="c52c3-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c52c3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_samlbase.png)

3. <span data-ttu-id="c52c3-155">Üzerinde **GaggleAMP etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c52c3-155">On the **GaggleAMP Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_url.png)

     <span data-ttu-id="c52c3-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.gaggleamp.com`</span><span class="sxs-lookup"><span data-stu-id="c52c3-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.gaggleamp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c52c3-158">Değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="c52c3-158">The value is not real.</span></span> <span data-ttu-id="c52c3-159">Değerin gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c52c3-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="c52c3-160">Kişi [GaggleAMP istemci destek ekibi](mailto:sales@gaggleamp.com) değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="c52c3-160">Contact [GaggleAMP Client support team](mailto:sales@gaggleamp.com) to get the value.</span></span> 
 
4. <span data-ttu-id="c52c3-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c52c3-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_certificate.png) 

5. <span data-ttu-id="c52c3-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c52c3-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c52c3-165">Üzerinde **GaggleAMP yapılandırma** 'yi tıklatın **yapılandırma GaggleAMP** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="c52c3-165">On the **GaggleAMP Configuration** section, click **Configure GaggleAMP** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c52c3-166">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="c52c3-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_configure.png) 

7. <span data-ttu-id="c52c3-168">Başka bir tarayıcı örneğinde Gaggle tarafınızdan takım desteklemek için oluşturulan SAML SSO sayfasına gidin (örneğin: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span><span class="sxs-lookup"><span data-stu-id="c52c3-168">In another browser instance, navigate to the SAML SSO page created for you by the Gaggle support team (for example: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span></span>

8. <span data-ttu-id="c52c3-169">Üzerinde **SAML SSO** sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c52c3-169">On your **SAML SSO** page, perform the following steps:</span></span>  
   
    ![GaggleAMP çoklu oturum açma](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_06.png) 
 
    <span data-ttu-id="c52c3-171">a.</span><span class="sxs-lookup"><span data-stu-id="c52c3-171">a.</span></span> <span data-ttu-id="c52c3-172">İçinde **kimlik sağlayıcısı veren** metin değerini yapıştırın **veren URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="c52c3-172">In the **Identity Provider Issuer** textbox, paste the value of **Issuer URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="c52c3-173">b.</span><span class="sxs-lookup"><span data-stu-id="c52c3-173">b.</span></span> <span data-ttu-id="c52c3-174">İçinde **kimlik sağlayıcısı tek oturum açma URL'si** metin değerini yapıştırın **çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="c52c3-174">In the **Identity Provider Single Sign-On URL** textbox, paste the  value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="c52c3-175">c.</span><span class="sxs-lookup"><span data-stu-id="c52c3-175">c.</span></span> <span data-ttu-id="c52c3-176">Tıklatın **Kaydet**</span><span class="sxs-lookup"><span data-stu-id="c52c3-176">Click **Save**</span></span>      

    <span data-ttu-id="c52c3-177">d.</span><span class="sxs-lookup"><span data-stu-id="c52c3-177">d.</span></span> <span data-ttu-id="c52c3-178">Gönderme **sertifika (Base64)** sertifika için [GaggleAMP destek ekibi](mailto:sales@gaggleamp.com).</span><span class="sxs-lookup"><span data-stu-id="c52c3-178">Send the **Certificate (Base64)** certificate to your [GaggleAMP support team](mailto:sales@gaggleamp.com).</span></span>

> [!TIP]
> <span data-ttu-id="c52c3-179">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="c52c3-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c52c3-180">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="c52c3-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c52c3-181">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c52c3-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c52c3-182">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c52c3-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="c52c3-183">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="c52c3-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="c52c3-185">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c52c3-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c52c3-186">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c52c3-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c52c3-188">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c52c3-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c52c3-190">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="c52c3-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c52c3-192">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c52c3-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c52c3-194">a.</span><span class="sxs-lookup"><span data-stu-id="c52c3-194">a.</span></span> <span data-ttu-id="c52c3-195">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c52c3-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c52c3-196">b.</span><span class="sxs-lookup"><span data-stu-id="c52c3-196">b.</span></span> <span data-ttu-id="c52c3-197">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="c52c3-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c52c3-198">c.</span><span class="sxs-lookup"><span data-stu-id="c52c3-198">c.</span></span> <span data-ttu-id="c52c3-199">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="c52c3-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c52c3-200">d.</span><span class="sxs-lookup"><span data-stu-id="c52c3-200">d.</span></span> <span data-ttu-id="c52c3-201">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c52c3-201">Click **Create**.</span></span>
 
### <a name="creating-a-gaggleamp-test-user"></a><span data-ttu-id="c52c3-202">GaggleAMP test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c52c3-202">Creating a GaggleAMP test user</span></span>

<span data-ttu-id="c52c3-203">Bu bölümün amacı Britta Simon içinde GaggleAMP adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="c52c3-203">The objective of this section is to create a user called Britta Simon in GaggleAMP.</span></span> <span data-ttu-id="c52c3-204">GaggleAMP yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="c52c3-204">GaggleAMP supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="c52c3-205">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="c52c3-205">There is no action item for you in this section.</span></span> <span data-ttu-id="c52c3-206">Yeni bir kullanıcı henüz yoksa GaggleAMP erişme denemesi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c52c3-206">A new user is created during an attempt to access GaggleAMP if it doesn't exist yet.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c52c3-207">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="c52c3-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c52c3-208">Bu bölümde, Britta GaggleAMP için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c52c3-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to GaggleAMP.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="c52c3-210">**GaggleAMP için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c52c3-210">**To assign Britta Simon to GaggleAMP, perform the following steps:**</span></span>

1. <span data-ttu-id="c52c3-211">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c52c3-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="c52c3-213">Uygulamalar listesinde **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="c52c3-213">In the applications list, select **GaggleAMP**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_app.png) 

3. <span data-ttu-id="c52c3-215">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c52c3-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="c52c3-217">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c52c3-217">Click **Add** button.</span></span> <span data-ttu-id="c52c3-218">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c52c3-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="c52c3-220">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="c52c3-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c52c3-221">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c52c3-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c52c3-222">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c52c3-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c52c3-223">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="c52c3-223">Testing single sign-on</span></span>

<span data-ttu-id="c52c3-224">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="c52c3-224">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="c52c3-225">Erişim paneli GaggleAMP parçasında tıklattığınızda, otomatik olarak GaggleAMP uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="c52c3-225">When you click the GaggleAMP tile in the Access Panel, you should get automatically signed-on to your GaggleAMP application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c52c3-226">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c52c3-226">Additional resources</span></span>

* [<span data-ttu-id="c52c3-227">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="c52c3-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c52c3-228">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="c52c3-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_203.png

