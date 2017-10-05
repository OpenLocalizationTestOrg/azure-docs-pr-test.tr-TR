---
title: "Öğretici: Azure Active Directory Tümleştirme ile görüntü geçiş | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve görüntü geçişi arasındaki yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 0bfbbaee7a74df6508584b7c8846fd07c2dc15c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a><span data-ttu-id="7c5a2-103">Öğretici: Azure Active Directory Tümleştirme ile görüntü geçişi</span><span class="sxs-lookup"><span data-stu-id="7c5a2-103">Tutorial: Azure Active Directory integration with Image Relay</span></span>

<span data-ttu-id="7c5a2-104">Bu öğreticide, görüntü geçiş Azure Active Directory (Azure AD) ile tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-104">In this tutorial, you learn how to integrate Image Relay with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7c5a2-105">Görüntü geçiş Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="7c5a2-105">Integrating Image Relay with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7c5a2-106">Görüntü geçiş erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7c5a2-106">You can control in Azure AD who has access to Image Relay</span></span>
- <span data-ttu-id="7c5a2-107">Azure AD hesaplarına otomatik olarak görüntü geçişi (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7c5a2-107">You can enable your users to automatically get signed-on to Image Relay (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7c5a2-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="7c5a2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7c5a2-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7c5a2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c5a2-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7c5a2-110">Prerequisites</span></span>

<span data-ttu-id="7c5a2-111">Azure AD Tümleştirmesi ile görüntü geçişi yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c5a2-111">To configure Azure AD integration with Image Relay, you need the following items:</span></span>

- <span data-ttu-id="7c5a2-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="7c5a2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7c5a2-113">Bir görüntü geçiş çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="7c5a2-113">An Image Relay single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7c5a2-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7c5a2-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c5a2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7c5a2-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7c5a2-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7c5a2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7c5a2-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="7c5a2-118">Scenario description</span></span>
<span data-ttu-id="7c5a2-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7c5a2-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="7c5a2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7c5a2-121">Galeriden görüntü geçiş ekleme</span><span class="sxs-lookup"><span data-stu-id="7c5a2-121">Adding Image Relay from the gallery</span></span>
2. <span data-ttu-id="7c5a2-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7c5a2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-image-relay-from-the-gallery"></a><span data-ttu-id="7c5a2-123">Galeriden görüntü geçiş ekleme</span><span class="sxs-lookup"><span data-stu-id="7c5a2-123">Adding Image Relay from the gallery</span></span>
<span data-ttu-id="7c5a2-124">Azure AD görüntü geçiş tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden görüntü geçiş eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-124">To configure the integration of Image Relay into Azure AD, you need to add Image Relay from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7c5a2-125">**Galeriden görüntü geçiş eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7c5a2-125">**To add Image Relay from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7c5a2-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7c5a2-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7c5a2-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="7c5a2-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="7c5a2-133">Arama kutusuna **görüntü geçiş**.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-133">In the search box, type **Image Relay**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. <span data-ttu-id="7c5a2-135">Sonuçlar panelinde seçin **görüntü geçiş**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-135">In the results panel, select **Image Relay**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7c5a2-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7c5a2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7c5a2-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma görüntü "Britta Simon" adlı bir test kullanıcı tabanlı geçiş ile test etme.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-138">In this section, you configure and test Azure AD single sign-on with Image Relay based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7c5a2-139">Tekli çalışmaya oturum için Azure AD görüntü geçiş karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Image Relay is to a user in Azure AD.</span></span> <span data-ttu-id="7c5a2-140">Diğer bir deyişle, bir Azure AD kullanıcısının görüntü geçiş ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-140">In other words, a link relationship between an Azure AD user and the related user in Image Relay needs to be established.</span></span>

<span data-ttu-id="7c5a2-141">Görüntü geçiş değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-141">In Image Relay, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7c5a2-142">Yapılandırma ve Azure AD çoklu oturum açma görüntü geçiş ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c5a2-142">To configure and test Azure AD single sign-on with Image Relay, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7c5a2-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7c5a2-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7c5a2-145">**[Bir görüntü geçiş test kullanıcısı oluşturma](#creating-an-image-relay-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlantılı görüntü geçişi sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-145">**[Creating an Image Relay test user](#creating-an-image-relay-test-user)** - to have a counterpart of Britta Simon in Image Relay that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7c5a2-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7c5a2-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7c5a2-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7c5a2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7c5a2-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma görüntü geçiş uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Image Relay application.</span></span>

<span data-ttu-id="7c5a2-150">**Azure AD çoklu oturum açma ile görüntü geçişi yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7c5a2-150">**To configure Azure AD single sign-on with Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="7c5a2-151">Azure portalında üzerinde **görüntü geçiş** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-151">In the Azure portal, on the **Image Relay** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="7c5a2-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. <span data-ttu-id="7c5a2-155">Üzerinde **görüntü geçiş etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7c5a2-155">On the **Image Relay Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    <span data-ttu-id="7c5a2-157">a.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-157">a.</span></span> <span data-ttu-id="7c5a2-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.imagerelay.com/`</span><span class="sxs-lookup"><span data-stu-id="7c5a2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.imagerelay.com/`</span></span>

    <span data-ttu-id="7c5a2-159">b.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-159">b.</span></span> <span data-ttu-id="7c5a2-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.imagerelay.com/sso/metadata`</span><span class="sxs-lookup"><span data-stu-id="7c5a2-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.imagerelay.com/sso/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7c5a2-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-161">These values are not real.</span></span> <span data-ttu-id="7c5a2-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7c5a2-163">Kişi [görüntü geçiş istemci destek ekibi](http://support.imagerelay.com/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-163">Contact [Image Relay Client support team](http://support.imagerelay.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="7c5a2-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. <span data-ttu-id="7c5a2-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7c5a2-168">Üzerinde **görüntü geçiş yapılandırma** 'yi tıklatın **yapılandırma görüntü geçiş** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-168">On the **Image Relay Configuration** section, click **Configure Image Relay** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7c5a2-169">Kopya **Sign-Out hizmet URL'sini ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="7c5a2-169">Copy the **Sign-Out Service URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. <span data-ttu-id="7c5a2-171">Başka bir tarayıcı penceresinde görüntü geçiş şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-171">In another browser window, sign in to your Image Relay company site as an administrator.</span></span>

8. <span data-ttu-id="7c5a2-172">Üstteki araç çubuğunda tıklatın **kullanıcılar ve izinler** iş yükü.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-172">In the toolbar on the top, click the **Users & Permissions** workload.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. <span data-ttu-id="7c5a2-174">Tıklatın **oluşturma yeni izni**.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-174">Click **Create New Permission**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. <span data-ttu-id="7c5a2-176">İçinde **tek oturum açma ayarları** iş yükü, select **bu grup için yalnızca oturum açma aracılığıyla çoklu oturum açma** onay kutusunu işaretleyin ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-176">In the **Single Sign On Settings** workload, select the **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. <span data-ttu-id="7c5a2-178">Git **hesap ayarları**.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-178">Go to **Account Settings**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. <span data-ttu-id="7c5a2-180">Git **tek oturum açma ayarları** iş yükü.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-180">Go to the **Single Sign On Settings** workload.</span></span>
    
     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. <span data-ttu-id="7c5a2-182">Üzerinde **SAML ayarları** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7c5a2-182">On the **SAML Settings** dialog, perform the following steps:</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    <span data-ttu-id="7c5a2-184">a.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-184">a.</span></span> <span data-ttu-id="7c5a2-185">İçinde **oturum açma URL'si** metin değerini yapıştırın **çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-185">In **Login URL** textbox, paste the value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7c5a2-186">b.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-186">b.</span></span> <span data-ttu-id="7c5a2-187">İçinde **oturum kapatma URL'si** metin değerini yapıştırın **tek Sign-Out hizmeti URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-187">In **Logout URL**  textbox, paste the value of **Single Sign-Out Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7c5a2-188">c.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-188">c.</span></span> <span data-ttu-id="7c5a2-189">Olarak **ad kimliği biçimi**seçin **urn: OASIS: adları: tc: SAML:1.1:nameid-biçimi: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-189">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="7c5a2-190">d.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-190">d.</span></span> <span data-ttu-id="7c5a2-191">Olarak **bağlama seçenekleri hizmet sağlayıcısı (görüntü geçiş) gelen istekleri için**seçin **POST bağlama**.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-191">As **Binding Options for Requests from the Service Provider (Image Relay)**, select **POST Binding**.</span></span>

    <span data-ttu-id="7c5a2-192">e.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-192">e.</span></span> <span data-ttu-id="7c5a2-193">Altında **x.509 sertifikası**, tıklatın **güncelleştirme sertifika**.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-193">Under **x.509 Certificate**, click **Update Certificate**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    <span data-ttu-id="7c5a2-195">f.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-195">f.</span></span> <span data-ttu-id="7c5a2-196">İndirilen sertifika Not Defteri'nde açın, içeriği Kopyala ve x.509 sertifikası metin kutusuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-196">Open the downloaded certificate in notepad, copy the content, and then paste it into the x.509 Certificate textbox.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    <span data-ttu-id="7c5a2-198">g.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-198">g.</span></span> <span data-ttu-id="7c5a2-199">İçinde **Just-In-Time kullanıcı sağlamayı** bölümünde, select **Just-In-Time kullanıcı sağlamayı etkinleştirin**.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-199">In **Just-In-Time User Provisioning** section, select the **Enable Just-In-Time User Provisioning**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    <span data-ttu-id="7c5a2-201">h.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-201">h.</span></span> <span data-ttu-id="7c5a2-202">İzin grubu seçin (örneğin, **SSO temel**) yalnızca çoklu oturum açma oturum açmaya izin.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-202">Select the permission group (for example, **SSO Basic**) which is allowed to sign in only through single sign-on.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    <span data-ttu-id="7c5a2-204">ı.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-204">i.</span></span> <span data-ttu-id="7c5a2-205">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-205">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7c5a2-206">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="7c5a2-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7c5a2-207">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7c5a2-208">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7c5a2-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7c5a2-209">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c5a2-209">Creating an Azure AD test user</span></span>
<span data-ttu-id="7c5a2-210">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="7c5a2-212">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7c5a2-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7c5a2-213">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-213">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7c5a2-215">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-215">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7c5a2-217">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-217">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7c5a2-219">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7c5a2-219">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7c5a2-221">a.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-221">a.</span></span> <span data-ttu-id="7c5a2-222">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-222">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7c5a2-223">b.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-223">b.</span></span> <span data-ttu-id="7c5a2-224">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-224">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7c5a2-225">c.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-225">c.</span></span> <span data-ttu-id="7c5a2-226">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-226">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7c5a2-227">d.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-227">d.</span></span> <span data-ttu-id="7c5a2-228">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-228">Click **Create**.</span></span>
 
### <a name="creating-an-image-relay-test-user"></a><span data-ttu-id="7c5a2-229">Bir görüntü geçiş test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c5a2-229">Creating an Image Relay test user</span></span>

<span data-ttu-id="7c5a2-230">Bu bölümün amacı Britta Simon de görüntü geçişi adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-230">The objective of this section is to create a user called Britta Simon in Image Relay.</span></span>

<span data-ttu-id="7c5a2-231">**Görüntü geçiş Britta Simon adlı bir kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7c5a2-231">**To create a user called Britta Simon in Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="7c5a2-232">Görüntü geçiş şirket sitenize yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-232">Sign-on to your Image Relay company site as an administrator.</span></span>

2. <span data-ttu-id="7c5a2-233">Git **kullanıcılar ve izinler** seçip **SSO kullanıcı oluştur**.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-233">Go to **Users & Permissions**     and select **Create SSO User**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. <span data-ttu-id="7c5a2-235">Girin **e-posta**, **ad**, **Soyadı**, ve **şirket** sağlamak ve izin grubu (seçmek istediğiniz kullanıcının Örneğin, SSO temel) yalnızca çoklu oturum açma oturum açarak Grup olduğu.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-235">Enter the **Email**, **First Name**, **Last Name**, and **Company** of the user you want to provision and select the permission group (for example, SSO Basic) which is the group that can sign in only through single sign-on.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. <span data-ttu-id="7c5a2-237">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-237">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7c5a2-238">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="7c5a2-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7c5a2-239">Bu bölümde, Britta görüntü geçişi erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Image Relay.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="7c5a2-241">**Görüntü geçişi Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7c5a2-241">**To assign Britta Simon to Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="7c5a2-242">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="7c5a2-244">Uygulamalar listesinde **görüntü geçiş**.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-244">In the applications list, select **Image Relay**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. <span data-ttu-id="7c5a2-246">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="7c5a2-248">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-248">Click **Add** button.</span></span> <span data-ttu-id="7c5a2-249">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="7c5a2-251">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7c5a2-252">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7c5a2-253">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7c5a2-254">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="7c5a2-254">Testing single sign-on</span></span>

<span data-ttu-id="7c5a2-255">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-255">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>    

<span data-ttu-id="7c5a2-256">Erişim paneli görüntü geçiş parçasında tıklattığınızda, otomatik olarak görüntü geçiş uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="7c5a2-256">When you click the Image Relay tile in the Access Panel, you should get automatically signed-on to your Image Relay application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7c5a2-257">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7c5a2-257">Additional resources</span></span>

* [<span data-ttu-id="7c5a2-258">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="7c5a2-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7c5a2-259">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="7c5a2-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

