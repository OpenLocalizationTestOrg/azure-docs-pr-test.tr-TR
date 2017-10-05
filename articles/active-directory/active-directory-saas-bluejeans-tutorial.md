---
title: "Öğretici: Azure Active Directory Tümleştirme ile BlueJeans | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile BlueJeans arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 03bf65852b8d3cf14aebf155891a028db86e78d0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a><span data-ttu-id="3335e-103">Öğretici: Azure Active Directory Tümleştirme BlueJeans ile</span><span class="sxs-lookup"><span data-stu-id="3335e-103">Tutorial: Azure Active Directory integration with BlueJeans</span></span>

<span data-ttu-id="3335e-104">Bu öğreticide, Azure Active Directory (Azure AD) ile BlueJeans tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3335e-104">In this tutorial, you learn how to integrate BlueJeans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3335e-105">BlueJeans Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="3335e-105">Integrating BlueJeans with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3335e-106">BlueJeans erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="3335e-106">You can control in Azure AD who has access to BlueJeans</span></span>
- <span data-ttu-id="3335e-107">Otomatik olarak için BlueJeans (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="3335e-107">You can enable your users to automatically get signed-on to BlueJeans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3335e-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="3335e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3335e-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3335e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3335e-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3335e-110">Prerequisites</span></span>

<span data-ttu-id="3335e-111">Azure AD tümleştirme BlueJeans ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="3335e-111">To configure Azure AD integration with BlueJeans, you need the following items:</span></span>

- <span data-ttu-id="3335e-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="3335e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3335e-113">Bir BlueJeans çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="3335e-113">A BlueJeans single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3335e-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="3335e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3335e-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="3335e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3335e-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="3335e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3335e-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3335e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3335e-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="3335e-118">Scenario description</span></span>
<span data-ttu-id="3335e-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="3335e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3335e-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="3335e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3335e-121">Galeriden BlueJeans ekleme</span><span class="sxs-lookup"><span data-stu-id="3335e-121">Adding BlueJeans from the gallery</span></span>
2. <span data-ttu-id="3335e-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="3335e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bluejeans-from-the-gallery"></a><span data-ttu-id="3335e-123">Galeriden BlueJeans ekleme</span><span class="sxs-lookup"><span data-stu-id="3335e-123">Adding BlueJeans from the gallery</span></span>
<span data-ttu-id="3335e-124">Azure AD BlueJeans tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden BlueJeans eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3335e-124">To configure the integration of BlueJeans into Azure AD, you need to add BlueJeans from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3335e-125">**Galeriden BlueJeans eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3335e-125">**To add BlueJeans from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3335e-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3335e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3335e-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="3335e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3335e-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3335e-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="3335e-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3335e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="3335e-133">Arama kutusuna **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="3335e-133">In the search box, type **BlueJeans**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. <span data-ttu-id="3335e-135">Sonuçlar panelinde seçin **BlueJeans**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3335e-135">In the results panel, select **BlueJeans**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3335e-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="3335e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3335e-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı BlueJeans ile test etme</span><span class="sxs-lookup"><span data-stu-id="3335e-138">In this section, you configure and test Azure AD single sign-on with BlueJeans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3335e-139">Tekli çalışmaya oturum için Azure AD BlueJeans karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="3335e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BlueJeans is to a user in Azure AD.</span></span> <span data-ttu-id="3335e-140">Diğer bir deyişle, bir Azure AD kullanıcısının BlueJeans ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3335e-140">In other words, a link relationship between an Azure AD user and the related user in BlueJeans needs to be established.</span></span>

<span data-ttu-id="3335e-141">BlueJeans içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="3335e-141">In BlueJeans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3335e-142">Yapılandırma ve Azure AD çoklu oturum açma BlueJeans ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="3335e-142">To configure and test Azure AD single sign-on with BlueJeans, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3335e-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="3335e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3335e-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="3335e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3335e-145">**[BlueJeans test kullanıcısı oluşturma](#creating-a-bluejeans-test-user)**  - Britta Simon BlueJeans içinde kullanıcı Azure AD gösterimini bağlı, karşılık gelen sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="3335e-145">**[Creating a BlueJeans test user](#creating-a-bluejeans-test-user)** - to have a counterpart of Britta Simon in BlueJeans that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3335e-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="3335e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3335e-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3335e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3335e-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3335e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3335e-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma BlueJeans uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3335e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BlueJeans application.</span></span>

<span data-ttu-id="3335e-150">**Azure AD çoklu oturum açma ile BlueJeans yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3335e-150">**To configure Azure AD single sign-on with BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="3335e-151">Azure portalında üzerinde **BlueJeans** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="3335e-151">In the Azure portal, on the **BlueJeans** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="3335e-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="3335e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. <span data-ttu-id="3335e-155">Üzerinde **BlueJeans etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3335e-155">On the **BlueJeans Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    <span data-ttu-id="3335e-157">a.</span><span class="sxs-lookup"><span data-stu-id="3335e-157">a.</span></span> <span data-ttu-id="3335e-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="3335e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    <span data-ttu-id="3335e-159">b.</span><span class="sxs-lookup"><span data-stu-id="3335e-159">b.</span></span> <span data-ttu-id="3335e-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="3335e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3335e-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="3335e-161">These values are not real.</span></span> <span data-ttu-id="3335e-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3335e-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3335e-163">Kişi [BlueJeans istemci destek ekibi](https://support.bluejeans.com/contact) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="3335e-163">Contact [BlueJeans Client support team](https://support.bluejeans.com/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="3335e-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3335e-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. <span data-ttu-id="3335e-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3335e-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3335e-168">Üzerinde **BlueJeans yapılandırma** 'yi tıklatın **yapılandırma BlueJeans** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="3335e-168">On the **BlueJeans Configuration** section, click **Configure BlueJeans** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3335e-169">Kopya **Sign-Out URL, değişiklik parola URL'si ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="3335e-169">Copy the **Sign-Out URL, Change Password URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. <span data-ttu-id="3335e-171">Farklı web tarayıcısı penceresinde oturum açın, **BlueJeans** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="3335e-171">In a different web browser window, log in to your **BlueJeans** company site as an administrator.</span></span>

8. <span data-ttu-id="3335e-172">Git **yönetici \> grup ayarları \> güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="3335e-172">Go to **ADMIN \> Group Settings \> Security**.</span></span>
   
   <span data-ttu-id="3335e-173">![Yönetici](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="3335e-173">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span></span>

9. <span data-ttu-id="3335e-174">İçinde **güvenlik** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3335e-174">In the **Security** section, perform the following steps:</span></span>
   
   <span data-ttu-id="3335e-175">![SAML çoklu oturum açma](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="3335e-175">![SAML Single Sign On](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span></span>   
   
   <span data-ttu-id="3335e-176">a.</span><span class="sxs-lookup"><span data-stu-id="3335e-176">a.</span></span> <span data-ttu-id="3335e-177">Seçin **SAML çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="3335e-177">Select **SAML Single Sign On**.</span></span>
  
   <span data-ttu-id="3335e-178">b.</span><span class="sxs-lookup"><span data-stu-id="3335e-178">b.</span></span> <span data-ttu-id="3335e-179">Seçin **otomatik sağlamayı etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="3335e-179">Select **Enable automatic provisioning**.</span></span>

10. <span data-ttu-id="3335e-180">Aşağıdaki adımlarla geçin:</span><span class="sxs-lookup"><span data-stu-id="3335e-180">Move on with the following steps:</span></span>

    <span data-ttu-id="3335e-181">![Sertifika yolu](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "sertifika yolu")</span><span class="sxs-lookup"><span data-stu-id="3335e-181">![Certificate Path](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Certificate Path")</span></span>
    
    <span data-ttu-id="3335e-182">a.</span><span class="sxs-lookup"><span data-stu-id="3335e-182">a.</span></span> <span data-ttu-id="3335e-183">Tıklatın **Dosya Seç**ve indirilen sertifika yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3335e-183">Click **Choose File**, and then upload the downloaded certificate.</span></span>
   
    <span data-ttu-id="3335e-184">b.</span><span class="sxs-lookup"><span data-stu-id="3335e-184">b.</span></span> <span data-ttu-id="3335e-185">Yapıştır **SAML çoklu oturum açma hizmet URL'si** içine **oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="3335e-185">Paste **SAML Single Sign-On Service URL** into the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="3335e-186">c.</span><span class="sxs-lookup"><span data-stu-id="3335e-186">c.</span></span> <span data-ttu-id="3335e-187">Yapıştır **değişiklik parola URL'si** içine **parola değişikliği URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="3335e-187">Paste **Change Password URL** into the **Password Change URL** textbox.</span></span>
   
    <span data-ttu-id="3335e-188">d.</span><span class="sxs-lookup"><span data-stu-id="3335e-188">d.</span></span> <span data-ttu-id="3335e-189">Yapıştır **Sign-Out URL** içine **oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="3335e-189">Paste **Sign-Out URL** into the **Logout URL** textbox.</span></span>

11. <span data-ttu-id="3335e-190">Aşağıdaki adımlarla geçin:</span><span class="sxs-lookup"><span data-stu-id="3335e-190">Move on with the following steps:</span></span>
    
    <span data-ttu-id="3335e-191">![Değişiklikleri kaydetmek](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Değişiklikleri Kaydet")</span><span class="sxs-lookup"><span data-stu-id="3335e-191">![Save Changes](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Save Changes")</span></span>
    
    <span data-ttu-id="3335e-192">a.</span><span class="sxs-lookup"><span data-stu-id="3335e-192">a.</span></span> <span data-ttu-id="3335e-193">İçinde **kullanıcı kimliği** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="3335e-193">In the **User id** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="3335e-194">b.</span><span class="sxs-lookup"><span data-stu-id="3335e-194">b.</span></span> <span data-ttu-id="3335e-195">İçinde **e-posta** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="3335e-195">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="3335e-196">c.</span><span class="sxs-lookup"><span data-stu-id="3335e-196">c.</span></span> <span data-ttu-id="3335e-197">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="3335e-197">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="3335e-198">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="3335e-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3335e-199">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="3335e-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3335e-200">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3335e-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3335e-201">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3335e-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="3335e-202">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="3335e-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="3335e-204">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3335e-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3335e-205">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3335e-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3335e-207">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="3335e-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3335e-209">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="3335e-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3335e-211">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3335e-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3335e-213">a.</span><span class="sxs-lookup"><span data-stu-id="3335e-213">a.</span></span> <span data-ttu-id="3335e-214">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3335e-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3335e-215">b.</span><span class="sxs-lookup"><span data-stu-id="3335e-215">b.</span></span> <span data-ttu-id="3335e-216">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="3335e-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3335e-217">c.</span><span class="sxs-lookup"><span data-stu-id="3335e-217">c.</span></span> <span data-ttu-id="3335e-218">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="3335e-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3335e-219">d.</span><span class="sxs-lookup"><span data-stu-id="3335e-219">d.</span></span> <span data-ttu-id="3335e-220">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3335e-220">Click **Create**.</span></span>
 
### <a name="creating-a-bluejeans-test-user"></a><span data-ttu-id="3335e-221">BlueJeans test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3335e-221">Creating a BlueJeans test user</span></span>

<span data-ttu-id="3335e-222">Azure AD kullanıcıları için BlueJeans oturum açmak etkinleştirmek için bunların BlueJeans sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3335e-222">To enable Azure AD users to log in to BlueJeans, they must be provisioned into BlueJeans.</span></span>  

<span data-ttu-id="3335e-223">BlueJeans durumunda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="3335e-223">In case of BlueJeans, provisioning is a manual task.</span></span>

<span data-ttu-id="3335e-224">**Kullanıcı hesaplarını sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3335e-224">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="3335e-225">Oturum, **BlueJeans** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="3335e-225">Log in to your **BlueJeans** company site as an administrator.</span></span>

2. <span data-ttu-id="3335e-226">Git **yönetici \> kullanıcıları yönetme \> kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="3335e-226">Go to **ADMIN \> Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="3335e-227">![Yönetici](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="3335e-227">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span></span>
   
   >[!IMPORTANT]
   ><span data-ttu-id="3335e-228">**Kullanıcı Ekle** sekmesi kullanılabilir yalnızca IF, içinde **Güvenlik sekmesinde**, **otomatik sağlamayı etkinleştirmek** işaretli değildir.</span><span class="sxs-lookup"><span data-stu-id="3335e-228">The **Add User** tab is only available if, in the **Security tab**, **Enable automatic provisioning** is unchecked.</span></span> 
   
3. <span data-ttu-id="3335e-229">İçinde **Kullanıcı Ekle** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3335e-229">In the **Add User** section, perform the following steps:</span></span>

    <span data-ttu-id="3335e-230">![Kullanıcı ekleme](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="3335e-230">![Add User](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Add User")</span></span>
    
    <span data-ttu-id="3335e-231">a.</span><span class="sxs-lookup"><span data-stu-id="3335e-231">a.</span></span> <span data-ttu-id="3335e-232">Tür a **BlueJeans kullanıcı adı**, bir **e-posta adresi**, **BlueJeans toplantı kimliği**, **yönetici parolası**, **tam adı** , **şirket** istediğiniz ilgili metin kutularına sağlamayı geçerli bir AAD hesabının.</span><span class="sxs-lookup"><span data-stu-id="3335e-232">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, the **Company** of a valid AAD account you want to provision into the related textboxes.</span></span>
    
    <span data-ttu-id="3335e-233">b.</span><span class="sxs-lookup"><span data-stu-id="3335e-233">b.</span></span> <span data-ttu-id="3335e-234">Tıklatın **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="3335e-234">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="3335e-235">API sağlama AAD kullanıcı hesaplarına BlueJeans tarafından sağlanan veya herhangi diğer BlueJeans kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3335e-235">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3335e-236">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="3335e-236">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3335e-237">Bu bölümde, Britta BlueJeans için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="3335e-237">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BlueJeans.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="3335e-239">**BlueJeans için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3335e-239">**To assign Britta Simon to BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="3335e-240">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3335e-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="3335e-242">Uygulamalar listesinde **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="3335e-242">In the applications list, select **BlueJeans**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. <span data-ttu-id="3335e-244">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="3335e-244">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="3335e-246">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3335e-246">Click **Add** button.</span></span> <span data-ttu-id="3335e-247">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3335e-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="3335e-249">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="3335e-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3335e-250">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3335e-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3335e-251">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3335e-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3335e-252">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="3335e-252">Testing single sign-on</span></span>

<span data-ttu-id="3335e-253">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="3335e-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3335e-254">Erişim paneli BlueJeans parçasında tıkladığınızda, oturum açma sayfasına BlueJeans uygulamasının almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3335e-254">When you click the BlueJeans tile in the Access Panel, you should get login page of BlueJeans application.</span></span>
<span data-ttu-id="3335e-255">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3335e-255">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3335e-256">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3335e-256">Additional resources</span></span>

* [<span data-ttu-id="3335e-257">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="3335e-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3335e-258">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="3335e-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

