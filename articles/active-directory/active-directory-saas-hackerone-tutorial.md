---
title: "Öğretici: Azure Active Directory Tümleştirme ile Hackerone | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Hackerone arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 657d8d4c98b7b133698a5cda0aa675da7f68c464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a><span data-ttu-id="06762-103">Öğretici: Azure Active Directory Tümleştirme HackerOne ile</span><span class="sxs-lookup"><span data-stu-id="06762-103">Tutorial: Azure Active Directory integration with HackerOne</span></span>

<span data-ttu-id="06762-104">Bu öğreticide, Azure Active Directory (Azure AD) ile HackerOne tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="06762-104">In this tutorial, you learn how to integrate HackerOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="06762-105">HackerOne Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="06762-105">Integrating HackerOne with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="06762-106">HackerOne erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="06762-106">You can control in Azure AD who has access to HackerOne</span></span>
- <span data-ttu-id="06762-107">Otomatik olarak için HackerOne (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="06762-107">You can enable your users to automatically get signed-on to HackerOne (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="06762-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="06762-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="06762-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="06762-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06762-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="06762-110">Prerequisites</span></span>

<span data-ttu-id="06762-111">Azure AD tümleştirme HackerOne ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="06762-111">To configure Azure AD integration with HackerOne, you need the following items:</span></span>

- <span data-ttu-id="06762-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="06762-112">An Azure AD subscription</span></span>
- <span data-ttu-id="06762-113">Bir HackerOne çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="06762-113">A HackerOne single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="06762-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="06762-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="06762-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="06762-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="06762-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="06762-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="06762-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="06762-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="06762-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="06762-118">Scenario description</span></span>
<span data-ttu-id="06762-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="06762-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="06762-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="06762-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="06762-121">Galeriden HackerOne ekleme</span><span class="sxs-lookup"><span data-stu-id="06762-121">Adding HackerOne from the gallery</span></span>
2. <span data-ttu-id="06762-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="06762-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hackerone-from-the-gallery"></a><span data-ttu-id="06762-123">Galeriden HackerOne ekleme</span><span class="sxs-lookup"><span data-stu-id="06762-123">Adding HackerOne from the gallery</span></span>
<span data-ttu-id="06762-124">Azure AD HackerOne tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden HackerOne eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="06762-124">To configure the integration of HackerOne into Azure AD, you need to add HackerOne from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="06762-125">**Galeriden HackerOne eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="06762-125">**To add HackerOne from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="06762-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="06762-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="06762-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="06762-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="06762-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="06762-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="06762-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="06762-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="06762-133">Arama kutusuna **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="06762-133">In the search box, type **HackerOne**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_search.png)

5. <span data-ttu-id="06762-135">Sonuçlar panelinde seçin **HackerOne**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="06762-135">In the results panel, select **HackerOne**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="06762-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="06762-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="06762-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı HackerOne ile test etme</span><span class="sxs-lookup"><span data-stu-id="06762-138">In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="06762-139">Tekli çalışmaya oturum için Azure AD HackerOne karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="06762-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HackerOne is to a user in Azure AD.</span></span> <span data-ttu-id="06762-140">Diğer bir deyişle, bir Azure AD kullanıcısının HackerOne ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="06762-140">In other words, a link relationship between an Azure AD user and the related user in HackerOne needs to be established.</span></span>

<span data-ttu-id="06762-141">HackerOne içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="06762-141">In HackerOne, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="06762-142">Yapılandırma ve Azure AD çoklu oturum açma HackerOne ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="06762-142">To configure and test Azure AD single sign-on with HackerOne, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="06762-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="06762-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="06762-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="06762-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="06762-145">**[HackerOne test kullanıcısı oluşturma](#creating-a-hackerone-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı HackerOne sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="06762-145">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - to have a counterpart of Britta Simon in HackerOne that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="06762-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="06762-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="06762-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="06762-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="06762-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="06762-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="06762-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma HackerOne uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="06762-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HackerOne application.</span></span>

<span data-ttu-id="06762-150">**Azure AD çoklu oturum açma ile HackerOne yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="06762-150">**To configure Azure AD single sign-on with HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="06762-151">Azure portalında üzerinde **HackerOne** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="06762-151">In the Azure portal, on the **HackerOne** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="06762-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="06762-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_samlbase.png)

3. <span data-ttu-id="06762-155">Üzerinde **HackerOne tek oturum açma URL'si ve tanımlayıcı** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="06762-155">On the **HackerOne Single sign-on URL and Identifier** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_url.png)

    <span data-ttu-id="06762-157">a.</span><span class="sxs-lookup"><span data-stu-id="06762-157">a.</span></span> <span data-ttu-id="06762-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://hackerone.com/<company name>/authentication`</span><span class="sxs-lookup"><span data-stu-id="06762-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://hackerone.com/<company name>/authentication`</span></span>

    <span data-ttu-id="06762-159">b.</span><span class="sxs-lookup"><span data-stu-id="06762-159">b.</span></span> <span data-ttu-id="06762-160">İçinde **tanımlayıcısı** metin kutusuna, URL'yi yazın:`https://hackerone.com/users/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="06762-160">In the **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="06762-161">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="06762-161">This value is not real.</span></span> <span data-ttu-id="06762-162">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="06762-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="06762-163">Kişi [HackerOne destek ekibi](mailto:support@hackerone.com) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="06762-163">Contact [HackerOne support team](mailto:support@hackerone.com) to get this value.</span></span> 
 
4. <span data-ttu-id="06762-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="06762-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_certificate.png) 

5. <span data-ttu-id="06762-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="06762-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="06762-168">Üzerinde **HackerOne yapılandırma** 'yi tıklatın **yapılandırma HackerOne** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="06762-168">On the **HackerOne Configuration** section, click **Configure HackerOne** to open **Configure sign-on** window.</span></span> <span data-ttu-id="06762-169">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="06762-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_configure.png) 

7. <span data-ttu-id="06762-171">Oturum açmayı HackerOne Kiracı yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="06762-171">Sign On to your HackerOne tenant as an administrator.</span></span>

8. <span data-ttu-id="06762-172">Üstteki menüde tıklayın "**ayarları**."</span><span class="sxs-lookup"><span data-stu-id="06762-172">In the menu on the top, click the "**Settings**."</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 

9. <span data-ttu-id="06762-174">Gidin "**kimlik doğrulaması**"tıklatıp"**SAML ayarları ekleme**."</span><span class="sxs-lookup"><span data-stu-id="06762-174">Navigate to "**Authentication**" and click "**Add SAML settings**."</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 

10. <span data-ttu-id="06762-176">Üzerinde **SAML ayarları** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="06762-176">On the **SAML Settings** dialog, perform the following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 

    <span data-ttu-id="06762-178">a.</span><span class="sxs-lookup"><span data-stu-id="06762-178">a.</span></span> <span data-ttu-id="06762-179">İçinde **e-posta etki alanı** metin kutusuna, kayıtlı bir etki alanı yazın.</span><span class="sxs-lookup"><span data-stu-id="06762-179">In the **Email Domain** textbox, type a registered domain.</span></span>

    <span data-ttu-id="06762-180">b.</span><span class="sxs-lookup"><span data-stu-id="06762-180">b.</span></span> <span data-ttu-id="06762-181">İçinde **üzerinde tek oturum URL'si** metin kutuları, yapıştırma değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="06762-181">In  **Single Sign On URL** textboxes, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="06762-182">c.</span><span class="sxs-lookup"><span data-stu-id="06762-182">c.</span></span> <span data-ttu-id="06762-183">Açık, **sertifika dosyası** Azure portalından indirdiğiniz Not Defteri'nde, içeriğini, panoya kopyalayın ve yapıştırın kendisine **X509 sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="06762-183">Open your **Certificate file** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X509 Certificate**  textbox.</span></span>
    
    <span data-ttu-id="06762-184">d.</span><span class="sxs-lookup"><span data-stu-id="06762-184">d.</span></span> <span data-ttu-id="06762-185">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="06762-185">Click **Save**.</span></span>

11. <span data-ttu-id="06762-186">Kimlik doğrulama ayarları iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="06762-186">On the Authentication Settings dialog, perform the following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 

    <span data-ttu-id="06762-188">a.</span><span class="sxs-lookup"><span data-stu-id="06762-188">a.</span></span> <span data-ttu-id="06762-189">Tıklatın **testi**.</span><span class="sxs-lookup"><span data-stu-id="06762-189">Click **Run test**.</span></span>

    <span data-ttu-id="06762-190">b.</span><span class="sxs-lookup"><span data-stu-id="06762-190">b.</span></span> <span data-ttu-id="06762-191">Varsa değerini **durum** alan eşittir **durumu'son test: oluşturulan**, kişi, [HackerOne destek ekibi](mailto:support@hackerone.com) yapılandırmanızı gözden istemek için.</span><span class="sxs-lookup"><span data-stu-id="06762-191">If the value of the **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) to request a review of your configuration.</span></span>

> [!TIP]
> <span data-ttu-id="06762-192">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="06762-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="06762-193">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="06762-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="06762-194">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="06762-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="06762-195">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="06762-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="06762-196">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="06762-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="06762-198">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="06762-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="06762-199">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="06762-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hackerone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="06762-201">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="06762-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hackerone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="06762-203">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="06762-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="06762-205">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="06762-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="06762-207">a.</span><span class="sxs-lookup"><span data-stu-id="06762-207">a.</span></span> <span data-ttu-id="06762-208">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="06762-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="06762-209">b.</span><span class="sxs-lookup"><span data-stu-id="06762-209">b.</span></span> <span data-ttu-id="06762-210">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="06762-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="06762-211">c.</span><span class="sxs-lookup"><span data-stu-id="06762-211">c.</span></span> <span data-ttu-id="06762-212">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="06762-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="06762-213">d.</span><span class="sxs-lookup"><span data-stu-id="06762-213">d.</span></span> <span data-ttu-id="06762-214">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="06762-214">Click **Create**.</span></span>
 
### <a name="creating-a-hackerone-test-user"></a><span data-ttu-id="06762-215">HackerOne test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="06762-215">Creating a HackerOne test user</span></span>

<span data-ttu-id="06762-216">Ardından, HackerOne içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="06762-216">Next, you create a user called Britta Simon in HackerOne.</span></span> <span data-ttu-id="06762-217">HackerOne yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="06762-217">HackerOne supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="06762-218">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="06762-218">There is no action item for you in this section.</span></span> <span data-ttu-id="06762-219">HackerOne eriştiğinizde, henüz yoksa yeni bir kullanıcı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="06762-219">When you access HackerOne, a new user is created if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="06762-220">Bir kullanıcı el ile oluşturmanız gerekiyorsa, Certify Destek ekibine başvurun gerekir.</span><span class="sxs-lookup"><span data-stu-id="06762-220">If you need to create a user manually, you need to contact the Certify support team.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="06762-221">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="06762-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="06762-222">Bu bölümde, Britta HackerOne için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="06762-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HackerOne.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="06762-224">**HackerOne için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="06762-224">**To assign Britta Simon to HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="06762-225">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="06762-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="06762-227">Uygulamalar listesinde **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="06762-227">In the applications list, select **HackerOne**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_app.png) 

3. <span data-ttu-id="06762-229">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="06762-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="06762-231">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="06762-231">Click **Add** button.</span></span> <span data-ttu-id="06762-232">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="06762-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="06762-234">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="06762-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="06762-235">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="06762-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="06762-236">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="06762-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="06762-237">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="06762-237">Testing single sign-on</span></span>

<span data-ttu-id="06762-238">Son olarak, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="06762-238">Finally, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="06762-239">Erişim paneli HackerOne parçasında tıklattığınızda, otomatik olarak HackerOne uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="06762-239">When you click the HackerOne tile in the Access Panel, you should get automatically signed-on to your HackerOne application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="06762-240">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="06762-240">Additional resources</span></span>

* [<span data-ttu-id="06762-241">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="06762-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="06762-242">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="06762-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png

