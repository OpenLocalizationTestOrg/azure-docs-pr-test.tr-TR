---
title: "Öğretici: Azure Active Directory Tümleştirme ile FreshDesk | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile FreshDesk arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: f4b47e345a40b64f69ad8a4618564662b4a6c879
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="f97fd-103">Öğretici: Azure Active Directory Tümleştirme FreshDesk ile</span><span class="sxs-lookup"><span data-stu-id="f97fd-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="f97fd-104">Bu öğreticide, Azure Active Directory (Azure AD) ile FreshDesk tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f97fd-104">In this tutorial, you learn how to integrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f97fd-105">FreshDesk Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="f97fd-105">Integrating FreshDesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f97fd-106">FreshDesk erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f97fd-106">You can control in Azure AD who has access to FreshDesk</span></span>
- <span data-ttu-id="f97fd-107">Otomatik olarak için FreshDesk (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f97fd-107">You can enable your users to automatically get signed-on to FreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f97fd-108">Hesaplarınızı bir merkezi konumda - Azure Yönetim Portalı'nı yönetme</span><span class="sxs-lookup"><span data-stu-id="f97fd-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="f97fd-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f97fd-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f97fd-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f97fd-110">Prerequisites</span></span>

<span data-ttu-id="f97fd-111">Azure AD tümleştirme FreshDesk ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="f97fd-111">To configure Azure AD integration with FreshDesk, you need the following items:</span></span>

- <span data-ttu-id="f97fd-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="f97fd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f97fd-113">Bir FreshDesk çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="f97fd-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f97fd-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="f97fd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f97fd-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f97fd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f97fd-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f97fd-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f97fd-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f97fd-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f97fd-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="f97fd-118">Scenario description</span></span>
<span data-ttu-id="f97fd-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="f97fd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f97fd-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="f97fd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f97fd-121">Galeriden FreshDesk ekleme</span><span class="sxs-lookup"><span data-stu-id="f97fd-121">Adding FreshDesk from the gallery</span></span>
2. <span data-ttu-id="f97fd-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f97fd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-the-gallery"></a><span data-ttu-id="f97fd-123">Galeriden FreshDesk ekleme</span><span class="sxs-lookup"><span data-stu-id="f97fd-123">Adding FreshDesk from the gallery</span></span>
<span data-ttu-id="f97fd-124">Azure AD FreshDesk tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden FreshDesk eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f97fd-124">To configure the integration of FreshDesk into Azure AD, you need to add FreshDesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f97fd-125">**Galeriden FreshDesk eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f97fd-125">**To add FreshDesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f97fd-126">İçinde  **[Azure Yönetim Portalı](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f97fd-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f97fd-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="f97fd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f97fd-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f97fd-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="f97fd-131">Tıklatın **Ekle** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f97fd-131">Click **Add** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="f97fd-133">Arama kutusuna **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="f97fd-133">In the search box, type **FreshDesk**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="f97fd-135">Sonuçlar panelinde seçin **FreshDesk**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f97fd-135">In the results panel, select **FreshDesk**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f97fd-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f97fd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f97fd-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı FreshDesk sınayın.</span><span class="sxs-lookup"><span data-stu-id="f97fd-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f97fd-139">Tekli çalışmaya oturum için Azure AD FreshDesk karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="f97fd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshDesk is to a user in Azure AD.</span></span> <span data-ttu-id="f97fd-140">Diğer bir deyişle, bir Azure AD kullanıcısının FreshDesk ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f97fd-140">In other words, a link relationship between an Azure AD user and the related user in FreshDesk needs to be established.</span></span>

<span data-ttu-id="f97fd-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** FreshDesk içinde.</span><span class="sxs-lookup"><span data-stu-id="f97fd-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FreshDesk.</span></span>

<span data-ttu-id="f97fd-142">Yapılandırma ve Azure AD çoklu oturum açma FreshDesk ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f97fd-142">To configure and test Azure AD single sign-on with FreshDesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f97fd-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f97fd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f97fd-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="f97fd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f97fd-145">**[FreshDesk test kullanıcısı oluşturma](#creating-a-freshdesk-test-user)**  - Britta Simon, karşılık gelen her, Azure AD gösterimine bağlı FreshDesk sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="f97fd-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - to have a counterpart of Britta Simon in FreshDesk that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="f97fd-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f97fd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f97fd-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f97fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f97fd-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f97fd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f97fd-149">Bu bölümde, Azure AD çoklu oturum açma Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma FreshDesk uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f97fd-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="f97fd-150">**Azure AD çoklu oturum açma ile FreshDesk yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f97fd-150">**To configure Azure AD single sign-on with FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="f97fd-151">Azure Yönetim Portalı'nda üzerinde **FreshDesk** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="f97fd-151">In the Azure Management portal, on the **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="f97fd-153">Üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f97fd-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="f97fd-155">Üzerinde **FreshDesk etki alanı ve URL'leri** bölümünde, lütfen **oturum açma URL'si** olarak: `https://<tenant-name>.freshdesk.com` veya başka bir değer Freshdesk önerdiği.</span><span class="sxs-lookup"><span data-stu-id="f97fd-155">On the **FreshDesk Domain and URLs** section, please enter the **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="f97fd-157">Lütfen bu gerçek değer olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f97fd-157">Please note that this is not the real value.</span></span> <span data-ttu-id="f97fd-158">Değerin gerçek oturum açma URL'si ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f97fd-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="f97fd-159">Kişi [FreshDesk istemci destek ekibi](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="f97fd-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="f97fd-160">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika** ve sertifikayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f97fd-160">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="f97fd-162">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f97fd-162">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f97fd-164">Üzerinde **FreshDesk yapılandırma** 'yi tıklatın **yapılandırma FreshDesk** yapılandırma oturum açma penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="f97fd-164">On the **FreshDesk Configuration** section, click **Configure FreshDesk** to open Configure sign-on window.</span></span> <span data-ttu-id="f97fd-165">SAML çoklu oturum açma hizmet URL'si ve Sign-Out URL'den kopyalama **hızlı başvuru** bölümü.</span><span class="sxs-lookup"><span data-stu-id="f97fd-165">Copy the SAML Single Sign-On Service URL and Sign-Out URL from the **Quick Reference** section.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="f97fd-167">Farklı web tarayıcısı penceresinde Freshdesk şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f97fd-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="f97fd-168">Üstteki menüde tıklatın **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="f97fd-168">In the menu on the top, click **Admin**.</span></span>
   
   <span data-ttu-id="f97fd-169">![Yönetici](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="f97fd-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="f97fd-170">İçinde **genel ayarları** sekmesini tıklatın, **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="f97fd-170">In the **General Settings** tab, click **Security**.</span></span>
   
   <span data-ttu-id="f97fd-171">![Güvenlik](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "güvenlik")</span><span class="sxs-lookup"><span data-stu-id="f97fd-171">![Security](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="f97fd-172">İçinde **güvenlik** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f97fd-172">In the **Security** section, perform the following steps:</span></span>
   
    <span data-ttu-id="f97fd-173">![Çoklu oturum açmayı](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "çoklu oturum açmayı")</span><span class="sxs-lookup"><span data-stu-id="f97fd-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="f97fd-174">a.</span><span class="sxs-lookup"><span data-stu-id="f97fd-174">a.</span></span> <span data-ttu-id="f97fd-175">İçin **çoklu oturum açma (SSO)**seçin **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="f97fd-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="f97fd-176">b.</span><span class="sxs-lookup"><span data-stu-id="f97fd-176">b.</span></span> <span data-ttu-id="f97fd-177">Seçin **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="f97fd-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="f97fd-178">c.</span><span class="sxs-lookup"><span data-stu-id="f97fd-178">c.</span></span> <span data-ttu-id="f97fd-179">Tür **SAML çoklu oturum açma hizmet URL'si** Azure portalına kopyalanan **SAML oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="f97fd-179">Type the **SAML Single Sign-On Service URL** you copied from Azure portal into the **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="f97fd-180">d.</span><span class="sxs-lookup"><span data-stu-id="f97fd-180">d.</span></span> <span data-ttu-id="f97fd-181">Tür **Sign-Out URL** Azure portalına kopyalanan **oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="f97fd-181">Type the **Sign-Out URL**  you copied from Azure portal into the **Logout URL** textbox.</span></span>

    <span data-ttu-id="f97fd-182">e.</span><span class="sxs-lookup"><span data-stu-id="f97fd-182">e.</span></span> <span data-ttu-id="f97fd-183">Kopya **parmak izi** değer Azure Portalı'ndan indirilen sertifikasından ve yapıştırın **güvenlik sertifika parmak izi** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="f97fd-183">Copy the **Thumbprint** value from the downloaded certificate from Azure portal and paste it into the **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="f97fd-184">Daha fazla ayrıntı için bkz: [bir sertifikanın parmak izi değerini almak nasıl](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="f97fd-184">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="f97fd-185">f.</span><span class="sxs-lookup"><span data-stu-id="f97fd-185">f.</span></span> <span data-ttu-id="f97fd-186">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f97fd-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f97fd-187">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f97fd-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="f97fd-188">Bu bölümün amacı, Britta Simon adlı Azure Yönetim Portalı'nda bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="f97fd-188">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="f97fd-190">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f97fd-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f97fd-191">İçinde **Azure Yönetim Portalı**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f97fd-191">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f97fd-193">Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="f97fd-193">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f97fd-195">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f97fd-195">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f97fd-197">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f97fd-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f97fd-199">a.</span><span class="sxs-lookup"><span data-stu-id="f97fd-199">a.</span></span> <span data-ttu-id="f97fd-200">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f97fd-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f97fd-201">b.</span><span class="sxs-lookup"><span data-stu-id="f97fd-201">b.</span></span> <span data-ttu-id="f97fd-202">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="f97fd-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f97fd-203">c.</span><span class="sxs-lookup"><span data-stu-id="f97fd-203">c.</span></span> <span data-ttu-id="f97fd-204">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="f97fd-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f97fd-205">d.</span><span class="sxs-lookup"><span data-stu-id="f97fd-205">d.</span></span> <span data-ttu-id="f97fd-206">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f97fd-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="f97fd-207">FreshDesk test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f97fd-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="f97fd-208">Azure AD kullanıcıların FreshDesk oturum etkinleştirmek için bunların FreshDesk sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f97fd-208">In order to enable Azure AD users to log into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="f97fd-209">FreshDesk söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="f97fd-209">In the case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="f97fd-210">**Kullanıcı hesaplarını sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f97fd-210">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="f97fd-211">Oturum, **Freshdesk** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="f97fd-211">Log in to your **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="f97fd-212">Üstteki menüde tıklatın **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="f97fd-212">In the menu on the top, click **Admin**.</span></span>
   
   <span data-ttu-id="f97fd-213">![Yönetici](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="f97fd-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="f97fd-214">İçinde **genel ayarları** sekmesini tıklatın, **aracıları**.</span><span class="sxs-lookup"><span data-stu-id="f97fd-214">In the **General Settings** tab, click **Agents**.</span></span>
   
   <span data-ttu-id="f97fd-215">![Aracıları](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "aracıları")</span><span class="sxs-lookup"><span data-stu-id="f97fd-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="f97fd-216">Tıklatın **yeni aracı**.</span><span class="sxs-lookup"><span data-stu-id="f97fd-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="f97fd-217">![Yeni aracı](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "yeni aracı")</span><span class="sxs-lookup"><span data-stu-id="f97fd-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="f97fd-218">Aracı bilgileri iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f97fd-218">On the Agent Information dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="f97fd-219">![Aracı bilgilerini](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "aracısı bilgileri")</span><span class="sxs-lookup"><span data-stu-id="f97fd-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
   <span data-ttu-id="f97fd-220">a.</span><span class="sxs-lookup"><span data-stu-id="f97fd-220">a.</span></span> <span data-ttu-id="f97fd-221">İçinde **tam adı** metin kutusuna, sağlamak istediğiniz Azure AD hesabının adını yazın.</span><span class="sxs-lookup"><span data-stu-id="f97fd-221">In the **Full Name** textbox, type the name of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="f97fd-222">b.</span><span class="sxs-lookup"><span data-stu-id="f97fd-222">b.</span></span> <span data-ttu-id="f97fd-223">İçinde **e-posta** metin kutusuna, sağlamak istediğiniz Azure AD hesabının e-posta adresini yazın Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f97fd-223">In the **Email** textbox, type the Azure AD email address of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="f97fd-224">c.</span><span class="sxs-lookup"><span data-stu-id="f97fd-224">c.</span></span> <span data-ttu-id="f97fd-225">İçinde **başlık** metin kutusuna, sağlamak istediğiniz Azure AD hesabının adını yazın.</span><span class="sxs-lookup"><span data-stu-id="f97fd-225">In the **Title** textbox, type the title of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="f97fd-226">d.</span><span class="sxs-lookup"><span data-stu-id="f97fd-226">d.</span></span> <span data-ttu-id="f97fd-227">Seçin **aracıları rolü**ve ardından **atamak**.</span><span class="sxs-lookup"><span data-stu-id="f97fd-227">Select **Agents role**, and then click **Assign**.</span></span>
       
   <span data-ttu-id="f97fd-228">e.</span><span class="sxs-lookup"><span data-stu-id="f97fd-228">e.</span></span> <span data-ttu-id="f97fd-229">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f97fd-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="f97fd-230">Azure AD hesap sahibi etkinleştirilmeden önce hesabı onaylamak için bir bağlantı içeren bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="f97fd-230">The Azure AD account holder will get an email that includes a link to confirm the account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="f97fd-231">API sağlama AAD kullanıcı hesaplarına Freshdesk tarafından sağlanan veya herhangi diğer Freshdesk kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f97fd-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk to provision AAD user accounts.</span></span> <span data-ttu-id="f97fd-232">FreshDesk için.</span><span class="sxs-lookup"><span data-stu-id="f97fd-232">to FreshDesk.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f97fd-233">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="f97fd-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f97fd-234">Bu bölümde, Britta kutusuna kendi erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f97fd-234">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Box.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="f97fd-236">**FreshDesk için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f97fd-236">**To assign Britta Simon to FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="f97fd-237">Azure Yönetim Portalı'nda uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f97fd-237">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="f97fd-239">Uygulamalar listesinde **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="f97fd-239">In the applications list, select **FreshDesk**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="f97fd-241">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="f97fd-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="f97fd-243">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f97fd-243">Click **Add** button.</span></span> <span data-ttu-id="f97fd-244">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f97fd-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="f97fd-246">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="f97fd-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f97fd-247">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f97fd-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f97fd-248">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f97fd-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f97fd-249">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="f97fd-249">Testing single sign-on</span></span>

<span data-ttu-id="f97fd-250">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="f97fd-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f97fd-251">Erişim paneli FreshDesk parçasında tıklattığınızda açan FreshDesk uygulamanıza oturum açma sayfasına almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f97fd-251">When you click the FreshDesk tile in the Access Panel, you should get login page to get signed-on to your FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f97fd-252">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f97fd-252">Additional resources</span></span>

* [<span data-ttu-id="f97fd-253">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="f97fd-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f97fd-254">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="f97fd-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

