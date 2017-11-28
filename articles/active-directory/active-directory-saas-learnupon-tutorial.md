---
title: "Öğretici: Azure Active Directory Tümleştirme ile LearnUpon | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile LearnUpon arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: b6ac8acc244e9029be01ede5e0865c280171217d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="42e0a-103">Öğretici: Azure Active Directory Tümleştirme LearnUpon ile</span><span class="sxs-lookup"><span data-stu-id="42e0a-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="42e0a-104">Bu öğreticide, Azure Active Directory (Azure AD) ile LearnUpon tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="42e0a-104">In this tutorial, you learn how to integrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42e0a-105">LearnUpon Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="42e0a-105">Integrating LearnUpon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="42e0a-106">LearnUpon erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="42e0a-106">You can control in Azure AD who has access to LearnUpon</span></span>
- <span data-ttu-id="42e0a-107">Otomatik olarak için LearnUpon (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="42e0a-107">You can enable your users to automatically get signed-on to LearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="42e0a-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="42e0a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="42e0a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="42e0a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42e0a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="42e0a-110">Prerequisites</span></span>

<span data-ttu-id="42e0a-111">Azure AD tümleştirme LearnUpon ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="42e0a-111">To configure Azure AD integration with LearnUpon, you need the following items:</span></span>

- <span data-ttu-id="42e0a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="42e0a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42e0a-113">Bir LearnUpon çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="42e0a-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42e0a-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="42e0a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42e0a-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="42e0a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42e0a-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="42e0a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42e0a-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42e0a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42e0a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="42e0a-118">Scenario description</span></span>
<span data-ttu-id="42e0a-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="42e0a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42e0a-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="42e0a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42e0a-121">Galeriden LearnUpon ekleme</span><span class="sxs-lookup"><span data-stu-id="42e0a-121">Adding LearnUpon from the gallery</span></span>
2. <span data-ttu-id="42e0a-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="42e0a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-the-gallery"></a><span data-ttu-id="42e0a-123">Galeriden LearnUpon ekleme</span><span class="sxs-lookup"><span data-stu-id="42e0a-123">Adding LearnUpon from the gallery</span></span>
<span data-ttu-id="42e0a-124">Azure AD LearnUpon tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden LearnUpon eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="42e0a-124">To configure the integration of LearnUpon into Azure AD, you need to add LearnUpon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="42e0a-125">**Galeriden LearnUpon eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="42e0a-125">**To add LearnUpon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="42e0a-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="42e0a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="42e0a-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="42e0a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="42e0a-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="42e0a-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="42e0a-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="42e0a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="42e0a-133">Arama kutusuna **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="42e0a-133">In the search box, type **LearnUpon**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. <span data-ttu-id="42e0a-135">Sonuçlar panelinde seçin **LearnUpon**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="42e0a-135">In the results panel, select **LearnUpon**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="42e0a-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="42e0a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="42e0a-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı LearnUpon sınayın.</span><span class="sxs-lookup"><span data-stu-id="42e0a-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="42e0a-139">Tekli çalışmaya oturum için Azure AD LearnUpon karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="42e0a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LearnUpon is to a user in Azure AD.</span></span> <span data-ttu-id="42e0a-140">Diğer bir deyişle, bir Azure AD kullanıcısının LearnUpon ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="42e0a-140">In other words, a link relationship between an Azure AD user and the related user in LearnUpon needs to be established.</span></span>

<span data-ttu-id="42e0a-141">LearnUpon içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="42e0a-141">In LearnUpon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="42e0a-142">Yapılandırma ve Azure AD çoklu oturum açma LearnUpon ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="42e0a-142">To configure and test Azure AD single sign-on with LearnUpon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="42e0a-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="42e0a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="42e0a-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="42e0a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42e0a-145">**[LearnUpon test kullanıcısı oluşturma](#creating-a-learnupon-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı LearnUpon sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="42e0a-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - to have a counterpart of Britta Simon in LearnUpon that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="42e0a-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="42e0a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42e0a-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="42e0a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="42e0a-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="42e0a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="42e0a-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma LearnUpon uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="42e0a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="42e0a-150">**Azure AD çoklu oturum açma ile LearnUpon yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="42e0a-150">**To configure Azure AD single sign-on with LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="42e0a-151">Azure portalında üzerinde **LearnUpon** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="42e0a-151">In the Azure portal, on the **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="42e0a-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="42e0a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. <span data-ttu-id="42e0a-155">Üzerinde **LearnUpon etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="42e0a-155">On the **LearnUpon Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="42e0a-157">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.learnupon.com/saml/consumer`</span><span class="sxs-lookup"><span data-stu-id="42e0a-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="42e0a-158">Lütfen bu gerçek değer olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="42e0a-158">Please note that this is not the real value.</span></span> <span data-ttu-id="42e0a-159">Bu değer ile gerçek yanıt URL'si güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="42e0a-159">you have to update this value with the actual Reply URL.</span></span> <span data-ttu-id="42e0a-160">Bu değer kişi almak için [LearnUpon destek ekibi](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="42e0a-160">To get this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



4. <span data-ttu-id="42e0a-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (ham)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="42e0a-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. <span data-ttu-id="42e0a-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="42e0a-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="42e0a-165">Üzerinde **LearnUpon yapılandırma** 'yi tıklatın **yapılandırma LearnUpon** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="42e0a-165">On the **LearnUpon Configuration** section, click **Configure LearnUpon** to open **Configure sign-on** window.</span></span> <span data-ttu-id="42e0a-166">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="42e0a-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. <span data-ttu-id="42e0a-168">Başka bir tarayıcı örneği ve oturum açma LearnUpon bir yönetici hesabıyla açın.</span><span class="sxs-lookup"><span data-stu-id="42e0a-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

8. <span data-ttu-id="42e0a-169">Tıklatın **ayarları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="42e0a-169">Click the **settings** tab.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. <span data-ttu-id="42e0a-171">Tıklatın **çoklu oturum açma - SAML**ve ardından **genel ayarları** SAML ayarlarını yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="42e0a-171">Click **Single Sign On - SAML**, and then click **General Settings** to configure SAML settings.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. <span data-ttu-id="42e0a-173">İçinde **genel ayarları** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="42e0a-173">In the **General Settings** section, perform the following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="42e0a-175">a.</span><span class="sxs-lookup"><span data-stu-id="42e0a-175">a.</span></span> <span data-ttu-id="42e0a-176">Seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="42e0a-176">Select **Enabled**.</span></span>

    <span data-ttu-id="42e0a-177">b.</span><span class="sxs-lookup"><span data-stu-id="42e0a-177">b.</span></span> <span data-ttu-id="42e0a-178">Seçin **sürüm** olarak **2.0**.</span><span class="sxs-lookup"><span data-stu-id="42e0a-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="42e0a-179">c.</span><span class="sxs-lookup"><span data-stu-id="42e0a-179">c.</span></span> <span data-ttu-id="42e0a-180">Seçin **Skip koşullar** olarak **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="42e0a-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="42e0a-181">d.</span><span class="sxs-lookup"><span data-stu-id="42e0a-181">d.</span></span> <span data-ttu-id="42e0a-182">İçinde **SAML belirteci sonrası parametre adı** metin kutusuna, doğrulandı ve kimlik doğrulaması - örneğin SAML onayı içeren isteği SAML tüketici URL'ye post parametresinin adı belirtilen yukarıda türü **SAMLResponse** .</span><span class="sxs-lookup"><span data-stu-id="42e0a-182">In the **SAML Token Post param name** textbox, type the name of request post parameter to the SAML consumer URL indicated above that contains the SAML Assertion to be verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="42e0a-183">e.</span><span class="sxs-lookup"><span data-stu-id="42e0a-183">e.</span></span> <span data-ttu-id="42e0a-184">İçinde **ad tanımlayıcısı biçimi** metin kutusuna, where, SAML onayı kullanıcı tanımlayıcısı (e-posta adresi) gösteren değeri bulunduğu - örneğin türü **urn: OASIS: adları: tc: SAML:1.1:nameid-biçimi: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="42e0a-184">In the **Name Identifier Format** textbox, type the value that indicates where in your SAML Assertion the users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="42e0a-185">f.</span><span class="sxs-lookup"><span data-stu-id="42e0a-185">f.</span></span> <span data-ttu-id="42e0a-186">İçinde **tanımlamak sağlayıcı konumu** metin kutusuna, karşıya yüklenen simge, Azure portalı oturum açma ekranından tıklatırsanız kullanıcıları gönderildiği gösteren değeri yazın.</span><span class="sxs-lookup"><span data-stu-id="42e0a-186">In the **Identify Provider Location** textbox, type the value that indicates where the users are sent to if they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="42e0a-187">g.</span><span class="sxs-lookup"><span data-stu-id="42e0a-187">g.</span></span> <span data-ttu-id="42e0a-188">İçinde **oturum kapatma URL'si** metin kutusuna, Yapıştır **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="42e0a-188">In the **Sign out URL** textbox, paste the **Sign-Out URL** which you have copied from the Azure portal.</span></span>
    
    <span data-ttu-id="42e0a-189">h.</span><span class="sxs-lookup"><span data-stu-id="42e0a-189">h.</span></span> <span data-ttu-id="42e0a-190">Tıklatın **parmak baskı siparişi yönetmek**ve indirilen sertifikanızın parmak izi karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="42e0a-190">Click **Manage finger prints**, and then upload the finger print of your downloaded certificate.</span></span>

11. <span data-ttu-id="42e0a-191">Tıklatın **kullanıcı ayarlarını**ve ardından aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="42e0a-191">Click **User Settings**, and then perform the following steps:</span></span>
   
     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="42e0a-193">a.</span><span class="sxs-lookup"><span data-stu-id="42e0a-193">a.</span></span> <span data-ttu-id="42e0a-194">İçinde **ilk ad tanımlayıcısı biçimi** metin kutusuna, bize, SAML onayı burada kullanıcılar firstname içinde söyler değerin bulunduğu - örneğin türü: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="42e0a-194">In the **First Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="42e0a-195">b.</span><span class="sxs-lookup"><span data-stu-id="42e0a-195">b.</span></span> <span data-ttu-id="42e0a-196">İçinde **son ad tanımlayıcısı biçimi** metin kutusuna, bize, SAML onayı burada kullanıcılar lastname içinde söyler değerin bulunduğu - örneğin türü: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname** .</span><span class="sxs-lookup"><span data-stu-id="42e0a-196">In the **Last Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="42e0a-197">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="42e0a-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="42e0a-198">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="42e0a-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="42e0a-199">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="42e0a-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="42e0a-200">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="42e0a-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="42e0a-201">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="42e0a-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="42e0a-203">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="42e0a-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="42e0a-204">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="42e0a-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="42e0a-206">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="42e0a-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="42e0a-208">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="42e0a-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="42e0a-210">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="42e0a-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="42e0a-212">a.</span><span class="sxs-lookup"><span data-stu-id="42e0a-212">a.</span></span> <span data-ttu-id="42e0a-213">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="42e0a-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42e0a-214">b.</span><span class="sxs-lookup"><span data-stu-id="42e0a-214">b.</span></span> <span data-ttu-id="42e0a-215">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="42e0a-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="42e0a-216">c.</span><span class="sxs-lookup"><span data-stu-id="42e0a-216">c.</span></span> <span data-ttu-id="42e0a-217">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="42e0a-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="42e0a-218">d.</span><span class="sxs-lookup"><span data-stu-id="42e0a-218">d.</span></span> <span data-ttu-id="42e0a-219">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="42e0a-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="42e0a-220">LearnUpon test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="42e0a-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="42e0a-221">Bu bölümün amacı Britta Simon içinde LearnUpon adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="42e0a-221">The objective of this section is to create a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="42e0a-222">LearnUpon yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="42e0a-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="42e0a-223">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="42e0a-223">There is no action item for you in this section.</span></span> <span data-ttu-id="42e0a-224">Yeni bir kullanıcı henüz yoksa LearnUpon erişme denemesi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="42e0a-224">A new user will be created during an attempt to access LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="42e0a-225">[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="42e0a-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="42e0a-226">Bir kullanıcı el ile oluşturmanız gerekiyorsa, başvurmanız gerekir [LearnUpon destek ekibi](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="42e0a-226">If you need to create an user manually, you need to contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="42e0a-227">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="42e0a-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="42e0a-228">Bu bölümde, Britta LearnUpon için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="42e0a-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LearnUpon.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="42e0a-230">**LearnUpon için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="42e0a-230">**To assign Britta Simon to LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="42e0a-231">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="42e0a-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="42e0a-233">Uygulamalar listesinde **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="42e0a-233">In the applications list, select **LearnUpon**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. <span data-ttu-id="42e0a-235">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="42e0a-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="42e0a-237">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="42e0a-237">Click **Add** button.</span></span> <span data-ttu-id="42e0a-238">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="42e0a-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="42e0a-240">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="42e0a-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="42e0a-241">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="42e0a-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42e0a-242">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="42e0a-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="42e0a-243">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="42e0a-243">Testing single sign-on</span></span>

<span data-ttu-id="42e0a-244">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="42e0a-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="42e0a-245">Erişim paneli LearnUpon parçasında tıklattığınızda, otomatik olarak LearnUpon uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="42e0a-245">When you click the LearnUpon tile in the Access Panel, you should get automatically signed-on to your LearnUpon application.</span></span>
<span data-ttu-id="42e0a-246">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="42e0a-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="42e0a-247">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="42e0a-247">Additional resources</span></span>

* [<span data-ttu-id="42e0a-248">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="42e0a-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42e0a-249">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="42e0a-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

