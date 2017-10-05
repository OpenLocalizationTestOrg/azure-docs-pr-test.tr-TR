---
title: "Öğretici: Azure Active Directory Tümleştirme ile Workfront | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Workfront arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: f7ba8d4895474de0da0e04da5f31959963ae65ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workfront"></a><span data-ttu-id="51887-103">Öğretici: Azure Active Directory Tümleştirme Workfront ile</span><span class="sxs-lookup"><span data-stu-id="51887-103">Tutorial: Azure Active Directory integration with Workfront</span></span>

<span data-ttu-id="51887-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Workfront tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="51887-104">In this tutorial, you learn how to integrate Workfront with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="51887-105">Workfront Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="51887-105">Integrating Workfront with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="51887-106">Workfront erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="51887-106">You can control in Azure AD who has access to Workfront</span></span>
- <span data-ttu-id="51887-107">Otomatik olarak için Workfront (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="51887-107">You can enable your users to automatically get signed-on to Workfront (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="51887-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="51887-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="51887-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="51887-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51887-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="51887-110">Prerequisites</span></span>

<span data-ttu-id="51887-111">Azure AD tümleştirme Workfront ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="51887-111">To configure Azure AD integration with Workfront, you need the following items:</span></span>

- <span data-ttu-id="51887-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="51887-112">An Azure AD subscription</span></span>
- <span data-ttu-id="51887-113">Bir Workfront çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="51887-113">A Workfront single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="51887-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="51887-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="51887-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="51887-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="51887-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="51887-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="51887-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="51887-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="51887-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="51887-118">Scenario description</span></span>
<span data-ttu-id="51887-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="51887-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="51887-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="51887-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="51887-121">Galeriden Workfront ekleme</span><span class="sxs-lookup"><span data-stu-id="51887-121">Adding Workfront from the gallery</span></span>
2. <span data-ttu-id="51887-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="51887-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workfront-from-the-gallery"></a><span data-ttu-id="51887-123">Galeriden Workfront ekleme</span><span class="sxs-lookup"><span data-stu-id="51887-123">Adding Workfront from the gallery</span></span>
<span data-ttu-id="51887-124">Azure AD Workfront tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Workfront eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="51887-124">To configure the integration of Workfront into Azure AD, you need to add Workfront from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="51887-125">**Galeriden Workfront eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="51887-125">**To add Workfront from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="51887-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="51887-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="51887-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="51887-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="51887-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="51887-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="51887-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="51887-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="51887-133">Arama kutusuna **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="51887-133">In the search box, type **Workfront**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_search.png)

5. <span data-ttu-id="51887-135">Sonuçlar panelinde seçin **Workfront**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="51887-135">In the results panel, select **Workfront**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="51887-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="51887-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="51887-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Workfront ile test etme</span><span class="sxs-lookup"><span data-stu-id="51887-138">In this section, you configure and test Azure AD single sign-on with Workfront based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="51887-139">Tekli çalışmaya oturum için Azure AD Workfront karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="51887-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workfront is to a user in Azure AD.</span></span> <span data-ttu-id="51887-140">Diğer bir deyişle, bir Azure AD kullanıcısının Workfront ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51887-140">In other words, a link relationship between an Azure AD user and the related user in Workfront needs to be established.</span></span>

<span data-ttu-id="51887-141">Workfront içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="51887-141">In Workfront, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="51887-142">Yapılandırma ve Azure AD çoklu oturum açma Workfront ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="51887-142">To configure and test Azure AD single sign-on with Workfront, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="51887-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="51887-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="51887-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="51887-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="51887-145">**[Workfront test kullanıcısı oluşturma](#creating-a-workfront-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Workfront sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="51887-145">**[Creating a Workfront test user](#creating-a-workfront-test-user)** - to have a counterpart of Britta Simon in Workfront that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="51887-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="51887-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="51887-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="51887-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="51887-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="51887-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="51887-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Workfront uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="51887-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workfront application.</span></span>

<span data-ttu-id="51887-150">**Azure AD çoklu oturum açma ile Workfront yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="51887-150">**To configure Azure AD single sign-on with Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="51887-151">Azure portalında üzerinde **Workfront** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="51887-151">In the Azure portal, on the **Workfront** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="51887-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="51887-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_samlbase.png)

3. <span data-ttu-id="51887-155">Üzerinde **Workfront etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="51887-155">On the **Workfront Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_url.png)

    <span data-ttu-id="51887-157">a.</span><span class="sxs-lookup"><span data-stu-id="51887-157">a.</span></span> <span data-ttu-id="51887-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.attask-ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="51887-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.attask-ondemand.com`</span></span>

    <span data-ttu-id="51887-159">b.</span><span class="sxs-lookup"><span data-stu-id="51887-159">b.</span></span> <span data-ttu-id="51887-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.attasksandbox.com/SAML2`</span><span class="sxs-lookup"><span data-stu-id="51887-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.attasksandbox.com/SAML2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="51887-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="51887-161">These values are not real.</span></span> <span data-ttu-id="51887-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="51887-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="51887-163">Kişi [Workfront istemci destek ekibi](https://www.workfront.com/contact-us/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="51887-163">Contact [Workfront Client support team](https://www.workfront.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="51887-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="51887-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the Certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_certificate.png) 

5. <span data-ttu-id="51887-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="51887-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workfront-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="51887-168">Üzerinde **Workfront yapılandırma** 'yi tıklatın **yapılandırma Workfront** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="51887-168">On the **Workfront Configuration** section, click **Configure Workfront** to open **Configure sign-on** window.</span></span> <span data-ttu-id="51887-169">Kopya **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="51887-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_configure.png) 

7. <span data-ttu-id="51887-171">Workfront şirket sitenize yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="51887-171">Sign-on to your Workfront company site as administrator.</span></span>

8. <span data-ttu-id="51887-172">Git **tek oturum açma yapılandırması**.</span><span class="sxs-lookup"><span data-stu-id="51887-172">Go to **Single Sign On Configuration**.</span></span>

9. <span data-ttu-id="51887-173">Üzerinde **çoklu oturum açma** iletişim kutusunda, aşağıdaki adımları uygulayın</span><span class="sxs-lookup"><span data-stu-id="51887-173">On the **Single Sign-On** dialog, perform the following steps</span></span>
    
    ![Çoklu oturum açmayı yapılandırın][23]
   
    <span data-ttu-id="51887-175">a.</span><span class="sxs-lookup"><span data-stu-id="51887-175">a.</span></span> <span data-ttu-id="51887-176">Olarak **türü**seçin **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="51887-176">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="51887-177">b.</span><span class="sxs-lookup"><span data-stu-id="51887-177">b.</span></span> <span data-ttu-id="51887-178">Seçin **hizmet sağlayıcı kimliği**.</span><span class="sxs-lookup"><span data-stu-id="51887-178">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="51887-179">c.</span><span class="sxs-lookup"><span data-stu-id="51887-179">c.</span></span> <span data-ttu-id="51887-180">Yapıştır **SAML çoklu oturum açma hizmet URL'si** içine **oturum açma portalı URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="51887-180">Paste the **SAML Single Sign-On Service URL** into the **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="51887-181">d.</span><span class="sxs-lookup"><span data-stu-id="51887-181">d.</span></span> <span data-ttu-id="51887-182">Yapıştır **tek Sign-Out hizmeti URL'si** içine **Sign-Out URL** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="51887-182">Paste **Single Sign-Out Service URL** into the **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="51887-183">e.</span><span class="sxs-lookup"><span data-stu-id="51887-183">e.</span></span> <span data-ttu-id="51887-184">Yapıştır **değişiklik parola URL'si** içine **değişiklik parola URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="51887-184">Paste **Change Password URL** into the **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="51887-185">f.</span><span class="sxs-lookup"><span data-stu-id="51887-185">f.</span></span> <span data-ttu-id="51887-186">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="51887-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="51887-187">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="51887-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="51887-188">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="51887-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="51887-189">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="51887-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="51887-190">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="51887-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="51887-191">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="51887-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="51887-193">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="51887-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="51887-194">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="51887-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workfront-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="51887-196">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="51887-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workfront-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="51887-198">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="51887-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workfront-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="51887-200">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="51887-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workfront-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="51887-202">a.</span><span class="sxs-lookup"><span data-stu-id="51887-202">a.</span></span> <span data-ttu-id="51887-203">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="51887-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="51887-204">b.</span><span class="sxs-lookup"><span data-stu-id="51887-204">b.</span></span> <span data-ttu-id="51887-205">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="51887-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="51887-206">c.</span><span class="sxs-lookup"><span data-stu-id="51887-206">c.</span></span> <span data-ttu-id="51887-207">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="51887-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="51887-208">d.</span><span class="sxs-lookup"><span data-stu-id="51887-208">d.</span></span> <span data-ttu-id="51887-209">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="51887-209">Click **Create**.</span></span>
 
### <a name="creating-a-workfront-test-user"></a><span data-ttu-id="51887-210">Workfront test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="51887-210">Creating a Workfront test user</span></span>

<span data-ttu-id="51887-211">Bu bölümün amacı Britta Simon içinde Workfront adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="51887-211">The objective of this section is to create a user called Britta Simon in Workfront.</span></span>

<span data-ttu-id="51887-212">**İçinde Workfront Britta Simon adlı bir kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="51887-212">**To create a user called Britta Simon in Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="51887-213">Workfront şirket sitenize yönetici olarak oturum açma.</span><span class="sxs-lookup"><span data-stu-id="51887-213">Sign on to your Workfront company site as administrator.</span></span>
2. <span data-ttu-id="51887-214">Üstteki menüde tıklatın **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="51887-214">In the menu on the top, click **People**.</span></span>
3. <span data-ttu-id="51887-215">Tıklatın **yeni bir kişiye**.</span><span class="sxs-lookup"><span data-stu-id="51887-215">Click **New Person**.</span></span> 
4. <span data-ttu-id="51887-216">Yeni bir kişiye iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="51887-216">On the New Person dialog, perform the following steps:</span></span>
   
    ![Bir Workfront test kullanıcısı oluşturma][21] 
   
    <span data-ttu-id="51887-218">a.</span><span class="sxs-lookup"><span data-stu-id="51887-218">a.</span></span> <span data-ttu-id="51887-219">İçinde **ad** metin kutusuna, "Britta." yazın</span><span class="sxs-lookup"><span data-stu-id="51887-219">In the **First Name** textbox, type "Britta."</span></span>
   
    <span data-ttu-id="51887-220">b.</span><span class="sxs-lookup"><span data-stu-id="51887-220">b.</span></span> <span data-ttu-id="51887-221">İçinde **Soyadı** metin kutusuna, "Simon." yazın</span><span class="sxs-lookup"><span data-stu-id="51887-221">In the **Last Name** textbox, type "Simon."</span></span>
   
    <span data-ttu-id="51887-222">c.</span><span class="sxs-lookup"><span data-stu-id="51887-222">c.</span></span> <span data-ttu-id="51887-223">İçinde **e-posta adresi** metin kutusuna, Azure Active Directory'de Britta Simon'ın e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="51887-223">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="51887-224">d.</span><span class="sxs-lookup"><span data-stu-id="51887-224">d.</span></span> <span data-ttu-id="51887-225">Tıklatın **kişiyi ekler**.</span><span class="sxs-lookup"><span data-stu-id="51887-225">Click **Add Person**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="51887-226">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="51887-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="51887-227">Bu bölümde, Britta Workfront için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="51887-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workfront.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="51887-229">**Workfront için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="51887-229">**To assign Britta Simon to Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="51887-230">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="51887-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="51887-232">Uygulamalar listesinde **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="51887-232">In the applications list, select **Workfront**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_app.png) 

3. <span data-ttu-id="51887-234">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="51887-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="51887-236">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="51887-236">Click **Add** button.</span></span> <span data-ttu-id="51887-237">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="51887-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="51887-239">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="51887-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="51887-240">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="51887-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="51887-241">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="51887-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="51887-242">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="51887-242">Testing single sign-on</span></span>

<span data-ttu-id="51887-243">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="51887-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="51887-244">Erişim paneli Workfront parçasında tıkladığınızda, oturum açma sayfasına Workfront uygulamasının almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="51887-244">When you click the Workfront tile in the Access Panel, you should get login page of Workfront application.</span></span>
<span data-ttu-id="51887-245">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="51887-245">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="51887-246">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="51887-246">Additional resources</span></span>

* [<span data-ttu-id="51887-247">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="51887-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="51887-248">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="51887-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_04.png
[21]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_08.png
[23]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_06.png
[100]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_203.png

