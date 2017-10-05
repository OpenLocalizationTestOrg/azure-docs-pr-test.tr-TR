---
title: "Öğretici: Azure Active Directory Tümleştirme KnowBe4 güvenlik tanıma eğitim ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve KnowBe4 güvenlik tanıma eğitim arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b80d2212-cc5f-4adb-836c-570640810c39
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 3b18737112a8aef101fab7fac1904f7c2e194d64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-knowbe4-security-awareness-training"></a><span data-ttu-id="fc323-103">Öğretici: Azure Active Directory Tümleştirme KnowBe4 güvenlik tanıma eğitim ile</span><span class="sxs-lookup"><span data-stu-id="fc323-103">Tutorial: Azure Active Directory integration with KnowBe4 Security Awareness Training</span></span>

<span data-ttu-id="fc323-104">Bu öğreticide, Azure Active Directory (Azure AD) ile KnowBe4 güvenlik tanıma eğitim tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fc323-104">In this tutorial, you learn how to integrate KnowBe4 Security Awareness Training with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fc323-105">KnowBe4 güvenlik tanıma eğitim Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="fc323-105">Integrating KnowBe4 Security Awareness Training with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fc323-106">KnowBe4 güvenlik tanıma eğitim erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="fc323-106">You can control in Azure AD who has access to KnowBe4 Security Awareness Training</span></span>
- <span data-ttu-id="fc323-107">Azure AD hesaplarına otomatik olarak Itanium tabanlı sistemler için KnowBe4 güvenlik tanıma eğitim için (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="fc323-107">You can enable your users to automatically get signed-on to KnowBe4 Security Awareness Training (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fc323-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="fc323-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fc323-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fc323-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc323-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fc323-110">Prerequisites</span></span>

<span data-ttu-id="fc323-111">Azure AD tümleştirme KnowBe4 güvenlik tanıma eğitim ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="fc323-111">To configure Azure AD integration with KnowBe4 Security Awareness Training, you need the following items:</span></span>

- <span data-ttu-id="fc323-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="fc323-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fc323-113">Bir KnowBe4 güvenlik tanıma eğitim çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="fc323-113">A KnowBe4 Security Awareness Training single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fc323-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="fc323-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fc323-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="fc323-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fc323-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="fc323-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fc323-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fc323-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fc323-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="fc323-118">Scenario description</span></span>
<span data-ttu-id="fc323-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="fc323-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fc323-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="fc323-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fc323-121">Galeriden KnowBe4 güvenlik tanıma eğitim ekleme</span><span class="sxs-lookup"><span data-stu-id="fc323-121">Adding KnowBe4 Security Awareness Training from the gallery</span></span>
2. <span data-ttu-id="fc323-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="fc323-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-knowbe4-security-awareness-training-from-the-gallery"></a><span data-ttu-id="fc323-123">Galeriden KnowBe4 güvenlik tanıma eğitim ekleme</span><span class="sxs-lookup"><span data-stu-id="fc323-123">Adding KnowBe4 Security Awareness Training from the gallery</span></span>
<span data-ttu-id="fc323-124">Azure AD KnowBe4 güvenlik tanıma eğitim tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden KnowBe4 güvenlik tanıma eğitim eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc323-124">To configure the integration of KnowBe4 Security Awareness Training into Azure AD, you need to add KnowBe4 Security Awareness Training from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fc323-125">**Galeriden KnowBe4 güvenlik tanıma eğitim eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fc323-125">**To add KnowBe4 Security Awareness Training from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fc323-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fc323-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fc323-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="fc323-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fc323-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fc323-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="fc323-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fc323-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="fc323-133">Arama kutusuna **KnowBe4 güvenlik tanıma eğitim**.</span><span class="sxs-lookup"><span data-stu-id="fc323-133">In the search box, type **KnowBe4 Security Awareness Training**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_search.png)

5. <span data-ttu-id="fc323-135">Sonuçlar panelinde seçin **KnowBe4 güvenlik tanıma eğitim**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fc323-135">In the results panel, select **KnowBe4 Security Awareness Training**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fc323-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="fc323-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fc323-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma KnowBe4 güvenlik tanıma "Britta Simon" adlı bir test kullanıcı tabanlı eğitim ile test etme.</span><span class="sxs-lookup"><span data-stu-id="fc323-138">In this section, you configure and test Azure AD single sign-on with KnowBe4 Security Awareness Training based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fc323-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen KnowBe4 güvenlik tanıma Eğitim'deki bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="fc323-139">For single sign-on to work, Azure AD needs to know what the counterpart user in KnowBe4 Security Awareness Training is to a user in Azure AD.</span></span> <span data-ttu-id="fc323-140">Diğer bir deyişle, bir Azure AD kullanıcısının KnowBe4 güvenlik tanıma eğitim ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc323-140">In other words, a link relationship between an Azure AD user and the related user in KnowBe4 Security Awareness Training needs to be established.</span></span>

<span data-ttu-id="fc323-141">KnowBe4 güvenlik tanıma eğitim değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="fc323-141">In KnowBe4 Security Awareness Training, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fc323-142">Yapılandırma ve Azure AD çoklu oturum açma KnowBe4 güvenlik tanıma eğitim ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="fc323-142">To configure and test Azure AD single sign-on with KnowBe4 Security Awareness Training, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fc323-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="fc323-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fc323-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="fc323-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fc323-145">**[KnowBe4 güvenlik tanıma eğitim test kullanıcısı oluşturma](#creating-a-knowbe4-security-awareness-training-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı KnowBe4 güvenlik tanıma eğitim sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="fc323-145">**[Creating a KnowBe4 Security Awareness Training test user](#creating-a-knowbe4-security-awareness-training-test-user)** - to have a counterpart of Britta Simon in KnowBe4 Security Awareness Training that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fc323-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="fc323-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fc323-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="fc323-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fc323-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fc323-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fc323-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma KnowBe4 güvenlik tanıma eğitim uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fc323-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your KnowBe4 Security Awareness Training application.</span></span>

<span data-ttu-id="fc323-150">**Azure AD çoklu oturum açma KnowBe4 güvenlik tanıma eğitim ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fc323-150">**To configure Azure AD single sign-on with KnowBe4 Security Awareness Training, perform the following steps:**</span></span>

1. <span data-ttu-id="fc323-151">Azure portalında üzerinde **KnowBe4 güvenlik tanıma eğitim** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="fc323-151">In the Azure portal, on the **KnowBe4 Security Awareness Training** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="fc323-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="fc323-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_samlbase.png)

3. <span data-ttu-id="fc323-155">Üzerinde **KnowBe4 güvenlik tanıma eğitim etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fc323-155">On the **KnowBe4 Security Awareness Training Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_url.png)

    <span data-ttu-id="fc323-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="fc323-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fc323-158">Değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="fc323-158">The value is not real.</span></span> <span data-ttu-id="fc323-159">Değerin gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="fc323-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="fc323-160">Kişi [KnowBe4 güvenlik tanıma eğitim istemci destek ekibi](mailto:support@KnowBe4.com) değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="fc323-160">Contact [KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com) to get the value.</span></span> 
 

4. <span data-ttu-id="fc323-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (ham)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fc323-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_certificate.png) 

5. <span data-ttu-id="fc323-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fc323-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fc323-165">Üzerinde **KnowBe4 güvenlik tanıma eğitim Yapılandırması** 'yi tıklatın **KnowBe4 güvenlik tanıma eğitim yapılandırma** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="fc323-165">On the **KnowBe4 Security Awareness Training Configuration** section, click **Configure KnowBe4 Security Awareness Training** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fc323-166">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="fc323-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_configure.png) 

7. <span data-ttu-id="fc323-168">Çoklu oturum açma yapılandırmak için **KnowBe4 güvenlik tanıma eğitim** yan, indirilen göndermek için ihtiyacınız **sertifika (ham)**, **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** için [KnowBe4 güvenlik tanıma eğitim istemci destek ekibi](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="fc323-168">To configure single sign-on on **KnowBe4 Security Awareness Training** side, you need to send the downloaded **Certificate (Raw)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com).</span></span>

> [!TIP]
> <span data-ttu-id="fc323-169">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="fc323-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fc323-170">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="fc323-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fc323-171">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fc323-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fc323-172">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc323-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="fc323-173">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="fc323-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="fc323-175">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fc323-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fc323-176">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fc323-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fc323-178">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="fc323-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fc323-180">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="fc323-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fc323-182">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fc323-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fc323-184">a.</span><span class="sxs-lookup"><span data-stu-id="fc323-184">a.</span></span> <span data-ttu-id="fc323-185">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fc323-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fc323-186">b.</span><span class="sxs-lookup"><span data-stu-id="fc323-186">b.</span></span> <span data-ttu-id="fc323-187">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="fc323-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fc323-188">c.</span><span class="sxs-lookup"><span data-stu-id="fc323-188">c.</span></span> <span data-ttu-id="fc323-189">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="fc323-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fc323-190">d.</span><span class="sxs-lookup"><span data-stu-id="fc323-190">d.</span></span> <span data-ttu-id="fc323-191">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fc323-191">Click **Create**.</span></span>
 
### <a name="creating-a-knowbe4-security-awareness-training-test-user"></a><span data-ttu-id="fc323-192">KnowBe4 güvenlik tanıma eğitim test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc323-192">Creating a KnowBe4 Security Awareness Training test user</span></span>

<span data-ttu-id="fc323-193">Bu bölümün amacı Britta Simon KnowBe4 güvenlik tanıma eğitim adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="fc323-193">The objective of this section is to create a user called Britta Simon in KnowBe4 Security Awareness Training.</span></span> <span data-ttu-id="fc323-194">KnowBe4 güvenlik tanıma eğitim yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="fc323-194">KnowBe4 Security Awareness Training supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="fc323-195">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="fc323-195">There is no action item for you in this section.</span></span> <span data-ttu-id="fc323-196">Yeni bir kullanıcı henüz yoksa KnowBe4 güvenlik tanıma eğitim erişme denemesi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fc323-196">A new user is created during an attempt to access KnowBe4 Security Awareness Training if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="fc323-197">Bir kullanıcı el ile oluşturmanız gerekiyorsa, başvurmanız gerekir [KnowBe4 güvenlik tanıma eğitim destek ekibi](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="fc323-197">If you need to create a user manually, you need to contact the [KnowBe4 Security Awareness Training support team](mailto:support@KnowBe4.com).</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fc323-198">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="fc323-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fc323-199">Bu bölümde, Britta KnowBe4 güvenlik tanıma eğitim için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="fc323-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to KnowBe4 Security Awareness Training.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="fc323-201">**KnowBe4 güvenlik tanıma eğitim Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fc323-201">**To assign Britta Simon to KnowBe4 Security Awareness Training, perform the following steps:**</span></span>

1. <span data-ttu-id="fc323-202">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fc323-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="fc323-204">Uygulamalar listesinde **KnowBe4 güvenlik tanıma eğitim**.</span><span class="sxs-lookup"><span data-stu-id="fc323-204">In the applications list, select **KnowBe4 Security Awareness Training**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_app.png) 

3. <span data-ttu-id="fc323-206">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="fc323-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="fc323-208">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fc323-208">Click **Add** button.</span></span> <span data-ttu-id="fc323-209">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fc323-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="fc323-211">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="fc323-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fc323-212">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fc323-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fc323-213">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fc323-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fc323-214">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="fc323-214">Testing single sign-on</span></span>

<span data-ttu-id="fc323-215">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="fc323-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
  
<span data-ttu-id="fc323-216">Erişim paneli KnowBe4 güvenlik tanıma eğitim parçasında tıklattığınızda, otomatik olarak KnowBe4 güvenlik tanıma eğitim uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="fc323-216">When you click the KnowBe4 Security Awareness Training tile in the Access Panel, you should get automatically signed-on to your KnowBe4 Security Awareness Training application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fc323-217">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="fc323-217">Additional resources</span></span>

* [<span data-ttu-id="fc323-218">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="fc323-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fc323-219">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="fc323-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_203.png

